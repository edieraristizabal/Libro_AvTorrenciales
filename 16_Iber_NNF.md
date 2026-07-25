<p style="font-size:11px;"><em><strong>Créditos</strong>: El contenido de este capítulo ha sido tomado y adaptado de Sanz-Ramos & Bladé {cite}`sanzramos_blade_2025a` (manual de referencia del módulo Iber-NNF) y de Sanz-Ramos et al. {cite}`sanzramos_iber_2025` (caso de aplicación al lahar de 2001 del volcán Popocatépetl).</em></p>

# Iber-NNF

**Iber** es un modelo hidrodinámico bidimensional de código abierto, desarrollado originalmente para la simulación de flujo en lámina libre en ríos y estuarios {cite}`blade_iber_2014`. Desde su primera versión en 2010, su ámbito de aplicación se ha ampliado progresivamente hasta incluir procesos morfodinámicos, transporte de sedimentos y contaminantes, dinámica de madera flotante, erosión de suelos, drenaje urbano y ecohidráulica. A partir de la versión 3, Iber incorpora **Iber-NNF** (*Non-Newtonian Flows*), un módulo específico para la simulación de flujos someros no newtonianos: avalanchas de nieve densas, propagación de relaves mineros, lahares y flujos hiperconcentrados (por ejemplo, flujos cargados de madera) {cite}`sanzramos_blade_2025a`.

A diferencia del capítulo anterior, centrado en los fundamentos de los modelos reológicos (véase [Modelos reológicos](04_ModelosReologicos.md)), este capítulo describe **cómo Iber-NNF implementa dicha física** dentro de un esquema numérico de volúmenes finitos, y presenta su validación en un caso real: el lahar de 2001 del volcán Popocatépetl (México).

## Ecuaciones de gobierno

Iber-NNF resuelve, al igual que Iber, las ecuaciones de aguas someras promediadas en profundidad (2D-SWE) en un sistema de coordenadas cartesianas, adaptadas para incorporar la física no newtoniana como términos de fricción y para permitir pendientes pronunciadas:

**Ecuación de continuidad:**

$$\frac{\partial h}{\partial t}+\frac{\partial q_{x}}{\partial x}+\frac{\partial q_{y}}{\partial y}=0$$

**Ecuaciones de cantidad de movimiento:**

$$\frac{\partial q_{x}}{\partial t}+\frac{\partial}{\partial x}\left(\frac{q_{x}^{2}}{h}+g'k_{p}\frac{h^{2}}{2}\right)+\frac{\partial}{\partial y}\left(\frac{q_{x}q_{y}}{h}\right)=g'h(S_{o,x}-S_{f,x})$$

$$\frac{\partial q_{y}}{\partial t}+\frac{\partial}{\partial x}\left(\frac{q_{x}q_{y}}{h}\right)+\frac{\partial}{\partial y}\left(\frac{q_{y}^{2}}{h}+g'k_{p}\frac{h^{2}}{2}\right)=g'h(S_{o,y}-S_{f,y})$$

donde $h$ es la profundidad del flujo; $q_x$, $q_y$ son las componentes del caudal específico; $g' = g\cos^2\theta$ es la gravedad corregida por la pendiente del terreno (relevante en cauces y laderas empinadas); $k_p$ es un factor de corrección de presión no hidrostática; $S_{o,x}$, $S_{o,y}$ son las componentes de la pendiente del lecho; y $S_{f,x}$, $S_{f,y}$ son las componentes de la pendiente de fricción, calculada según el modelo reológico seleccionado a partir de $\tau = \rho g h S_f$.

Un desafío numérico central es garantizar el balance entre los términos de presión, la pendiente del lecho y la fricción, de forma que el flujo se detenga correctamente en pendientes pronunciadas y topografías complejas, sin generar movimientos artificiales. Para ello, Iber-NNF utiliza un esquema de discretización *upwind* que asegura este balance incluso en presencia de fricción no lineal y dependiente de la velocidad {cite}`sanzramos_blade_2025a`.

## Modelos reológicos implementados

La versión actual de Iber-NNF incorpora **ocho modelos reológicos**, todos ellos aplicables a la modelación de lahares excepto el modelo de Bartelt (concebido para avalanchas de nieve con fuerzas de cohesión):

| Modelo | Pendiente de fricción $S_f$ | Parámetros de calibración |
|---|---|---|
| Manning {cite}`chow_openchannel_1959` | $\dfrac{n^2 v^2}{h^{4/3}}$ | $n$ |
| Viscoso | $\dfrac{n^2 v}{h^{3}}$ | $n$ |
| Dilatante | $\dfrac{n^2 v}{h^{2}}$ | $n$ |
| Bingham simplificado {cite}`bingham_investigation_1916` | $\dfrac{1}{\rho g h}\left(\omega\tau_y+3\dfrac{\mu_B v}{h}\right)$ | $\tau_y$, $\mu_B$ |
| Voellmy {cite}`voellmy_lawinen_1955` | $\dfrac{v^2}{\xi h}+\mu$ | $\xi$, $\mu$ |
| Bartelt (avalanchas de nieve) | — | cohesión, $\mu$, $\xi$ |
| O'Brien y Julien (cuadrático) {cite}`obrien_julien_1988` | $\dfrac{\tau_y}{\rho g h}+\dfrac{K\mu_B v}{8\rho g h^2}+\dfrac{n^2 v^2}{h^{4/3}}$ | $\tau_y$, $\mu_B$, $n$, $K$ |
| Herschel–Bulkley {cite}`herschel_bulkley_1926` | $\dfrac{1}{\rho g h}\left(\tau_y+k\left(\dfrac{v}{h}\right)^{\alpha}\right)$ | $\tau_y$, $k$, $\alpha$ |

Los parámetros de calibración de cada modelo son la densidad del flujo ($\rho$), el coeficiente de Manning ($n$), el esfuerzo de cedencia ($\tau_y$), la viscosidad dinámica ($\mu_B$), el coeficiente de fricción de Coulomb ($\mu$), el coeficiente de fricción turbulenta ($\xi$), un parámetro de resistencia ($K$), un parámetro de consistencia ($k$) y la potencia de corte ($\alpha$). El modelo de Coulomb puro, usado con frecuencia en la literatura de lahares, puede reproducirse dentro de Iber-NNF haciendo $\xi \to \infty$ en el modelo de Voellmy, eliminando así el término viscoso-turbulento {cite}`sanzramos_iber_2025`.

Los fundamentos físicos, ventajas y limitaciones de cada uno de estos modelos se describen en detalle en el capítulo [Modelos reológicos](04_ModelosReologicos.md); este capítulo se centra en su implementación y desempeño dentro de Iber.

## Incorporación de sedimento (entrainment)

Iber-NNF incluye formulaciones de incorporación de material del lecho (*entrainment*), un proceso especialmente relevante para lahares y avalanchas de nieve densas, donde el volumen del flujo puede crecer sustancialmente a lo largo del recorrido {cite}`sanzramos_blade_2025a`:

- **Modelo de velocidad:** $E = K_u(u - u_{crit})$ cuando $u > u_{crit}$.
- **Modelo de altura:** función de la profundidad de la cubierta de nieve o sedimento disponible, con límites superiores de incorporación.
- **Modelo de velocidad cuadrática:** $E = K_u(u^2 - u_{crit}^2)$.
- **Modelo de esfuerzo cortante basal:** $E = K_\tau(\tau - \tau_{crit})$.

## Arquitectura del software

Iber-NNF está completamente integrado en la interfaz gráfica de Iber y se activa como un complemento (*Iber tools >> Plug-ins*). En su versión actual funciona como un módulo independiente, sin acoplamiento directo con otros módulos de cálculo de Iber (sedimentos, calidad de agua, etc.). Además de las variables hidrodinámicas estándar (profundidad, velocidad, cota de la superficie libre), Iber-NNF calcula variables específicas para la evaluación de amenaza, como la pendiente del terreno, la presión de impacto dinámica y sus valores máximos durante la simulación {cite}`sanzramos_blade_2025a`. Las futuras versiones del módulo contemplan la incorporación de cómputo paralelo en GPU, siguiendo el mismo enfoque ya utilizado en los módulos de transporte de sedimentos y hábitat de Iber, con aceleraciones reportadas de más de 100 veces {cite}`sanzramos_iber_2025`.

## Caso de aplicación: lahar de 2001 del volcán Popocatépetl

Sanz-Ramos et al. {cite}`sanzramos_iber_2025` utilizaron Iber-NNF para reconstruir el lahar de 2001 ocurrido en la quebrada de Huiloac, en el flanco norte del volcán Popocatépetl (México), un evento detonado por la fusión parcial del glaciar de la cumbre durante una fase eruptiva y que recorrió entre 12 y 13 km hasta su zona de depósito {cite}`capra_lahars_2004`.

**Configuración del modelo:**
- Dominio de estudio de 1774 ha, con elevaciones entre 2500 y 3600 m s.n.m.
- Malla de aproximadamente 180 000 elementos triangulares, con un lado medio de 15 m, acorde con la resolución del modelo digital de terreno (DTM) del INEGI.
- Hidrograma de entrada con caudal pico de 335 m³/s y una duración de 3 h, derivado de registros de geófonos a lo largo de la quebrada {cite}`munoz_salinas_lahar_2007`.
- Densidad del flujo de 1740 kg/m³.
- Parámetros de cada modelo reológico calibrados para reproducir la distancia de alcance observada por Capra et al. {cite}`capra_lahars_2004`.

**Resultados principales:**

Los modelos que solo incluyen un término de fricción dependiente de la velocidad (Manning, Viscoso, Dilatante) no lograron detener el flujo ni en pendientes suaves ni pronunciadas, generando una extensión de inundación mayor a 718 ha y velocidades de llegada muy rápidas (< 30 min), en clara discrepancia con las observaciones de campo. Los modelos de Voellmy, Bingham, O'Brien-Julien y Herschel-Bulkley sí reprodujeron adecuadamente el cese del movimiento y la extensión observada:

| Modelo | Área inundada | Profundidad máxima | Tiempo de llegada |
|---|---|---|---|
| Manning | > 718 ha | ~5 m (aguas arriba) | < 0:30 h (no se detiene) |
| Voellmy | 149 ha | > 5 m (margen izquierda) | 3:40–3:50 h |
| Bingham | 65 ha | ~4 m | 3:40–3:50 h |
| O'Brien–Julien | 74 ha | 4.0 m | 3:00–3:10 h |
| Herschel–Bulkley | 88 ha | 4.8 m | 2:50–3:00 h |

Las velocidades simuladas se compararon con las velocidades de campo estimadas por superelevación en nueve puntos de control por Muñoz-Salinas et al. {cite}`munoz_salinas_lahar_2007`. El modelo de Manning subestimó sistemáticamente la velocidad porque el flujo se dispersó en un área excesivamente amplia en lugar de concentrarse en la quebrada; Voellmy sobreestimó la velocidad en todos los puntos; y Bingham fue el que mejor reprodujo las velocidades observadas.

El tiempo de cómputo de cada simulación fue inferior a 10 minutos (malla de 15 m), aunque los autores señalan que una discretización más fina —necesaria en quebradas más estrechas o para una mejor resolución del frente— aumentaría considerablemente el costo computacional, lo que motiva el desarrollo de la versión con aceleración por GPU.

**Sensibilidad a la resolución topográfica:** los autores repitieron la simulación (modelo de Bingham) con DTM de 5, 15, 30, 60, 90 y 120 m. Los DTM más gruesos (90–120 m) suavizan excesivamente la geometría de la quebrada y no logran confinar el flujo; los DTM de 30–60 m reproducen mejor las ramificaciones observadas en la "zona de amenaza alta"; y el DTM de 5 m, sin la opción de relleno de depresiones ("*fill sinks*") de Iber, generó sumideros numéricos que detuvieron artificialmente el flujo antes de lo observado.

## Conclusiones del caso de estudio

La reconstrucción del lahar de 2001 en el Popocatépetl confirma que **la elección del modelo reológico es tan determinante como la calidad de la topografía** para reproducir correctamente tanto la fase dinámica como la fase de depósito de un lahar. Los modelos puramente dependientes de la velocidad (tipo Manning) resultan inadecuados porque no pueden representar el cese del movimiento; los modelos con un término de cedencia explícito (Bingham, O'Brien-Julien, Herschel-Bulkley) o con fricción de Coulomb (Voellmy) sí lo logran, aunque combinaciones distintas de parámetros pueden producir resultados de alcance comparables, lo que subraya la importancia de una calibración cuidadosa y de la disponibilidad de datos de campo para restringir el rango de parámetros plausibles.

```{bibliography}
:filter: docname in docnames
```
