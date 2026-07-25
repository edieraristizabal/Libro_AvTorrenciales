<p style="font-size:11px;"><em><strong>Créditos</strong>: El contenido de este capítulo ha sido tomado de varias fuentes, pero especialmente de Iverson & George {cite}`iverson_george_2024` en Advances in Debris-flow science and practice Eds. Matias Jakob, Scott McDougall, Paul Santi. (2024).</em></p>

# Ecuaciones de Saint-Venant

Para modelar flujos de escombros (*debris flows*) y otros flujos, se emplean un conjunto de ecuaciones de conservación que derivan de la mecánica de fluidos y medios continuos. Las ecuaciones de Saint-Venant son una forma simplificada y promediada en profundidad de las ecuaciones de Navier–Stokes. Se utilizan para modelar flujos superficiales como ríos, avalanchas, lahares y *debris flows*. Estas ecuaciones resuelven la dinámica del flujo considerando solo las variaciones en el plano horizontal (x,y), y promediando las variables a lo largo de la vertical (z), lo que simplifica mucho el problema sin perder lo esencial. Las ecuaciones de flujo de aguas someras (o de aguas poco profundas) resuelven simultáneamente las ecuaciones de conservación de masa y de momento para calcular la cota del agua y la velocidad. 

Las fuerzas de fricción entre el fluido y el contorno sólido son las principales fuerzas de resistencia en las ecuaciones hidráulicas estándar para agua clara newtoniana. Comparado con aguas limpias, los flujos de lodo y detritos generan fuerzas resistentes adicionales. El aumento del contenido de sólidos incrementa la viscosidad de los flujos no newtonianos, generando fuerzas resistentes internas dentro del fluido. A concentraciones más altas, particularmente con partículas gruesas, la colisión y fricción entre partículas introducen fuerzas resistentes internas adicionales. La mayoría de las modificaciones teóricas y numéricas implican la integración de las nuevas fuerzas internas del fluido en la ecuación de momento. 

La aplicación del transporte no newtoniano en un modelo de aguas someras (o de aguas poco profundas) requiere calcular las pérdidas internas añadiendo un término de pendiente a la pendiente de fricción ($S_f$) en la ecuación de momento y aumentando el flujo para tener en cuenta el volumen de los sólidos. La pendiente de fricción ($S_f$) del modelo de aguas someras representa las fuerzas que actúan contra el flujo en el contorno del fluido (por ejemplo, el canal), mientras que la pendiente de lodo y detritos ($S_{MD}$) representa las pérdidas internas debidas a la viscosidad, la turbulencia y/o la dispersión dentro del fluido.

Los términos utilizados en las ecuaciones de conservación de masa y momento de Saint-Venant para modelar flujos de escombros se traducen al español de la siguiente manera:

| **Término en inglés**               | **Símbolo**   | **Traducción al español**                            |
|--------------------------------------|---------------|------------------------------------------------------|
| Newtonian friction slope             | $𝑆_𝑓$         | Pendiente de fricción newtoniana                     |
| Mud and debris friction slope        | $𝑆_{𝑀D}$       | Pendiente de fricción para lodos y escombros         |


- **Pendiente de fricción newtoniana:** Representa la resistencia al flujo generada por la fricción basal y la viscosidad interna en materiales con comportamiento newtoniano, como el agua o fluidos con viscosidad constante. En hidráulica clásica, es análoga a la pendiente de energía perdida por fricción (e.g., fórmulas de Manning o Chezy).

- **Pendiente de fricción para lodos y escombros:** Representa la resistencia basal e interna característica de flujos no newtonianos, como mezclas de lodo y escombros, que pueden mostrar comportamiento viscoplástico (por ejemplo, tipo Bingham) o hiperconcentrado.

Generalmente los modelos entonces calculan un esfuerzo cortante no newtoniano basándose en la clasificación del flujo (p. ej., flujo de lodo, flujo de detritos, etc.) y el enfoque reológico apropiado (es decir, el modelo de esfuerzo-deformación). Luego, se integra el cortante viscoso, turbulento y de dispersión del modelo de esfuerzo-deformación en la ecuación de momento, convirtiendo el esfuerzo cortante en una pendiente ($𝑆_{𝑀D}$) y sumando esta pendiente a la pendiente de fricción ($S_f$). Adicionalmente, debido a que estos flujos pueden contener entre un 5% y un 70% de sólidos por volumen, un modelo de lecho fijo debe aumentar el volumen del flujo para tener en cuenta el impacto del sedimento en la masa y la profundidad del flujo.

En este sentido, los modelos numéricos para flujos de ladera suelen usar las ecuaciones de Saint-Venant adaptadas a flujos no newtonianos, en forma de conservación de masa y momento en 1D o 2D. A continuación, se detalla su estructura para flujo de detritos.

#### 1. Ecuación de conservación de masa (Continuidad)
Esta ecuación garantiza que la materia no se crea ni se destruye; solo se desplaza o cambia de volumen ("abultamiento" o *bulking*). En la modelización de procesos de ladera, describe cómo cambian el espesor (o nivel) y la masa de la mezcla a medida que desciende por un canal o ladera.

Para un flujo en una dimensión horizontal (1D), la ecuación de continuidad se puede presentar de esta forma (asumiendo ancho unitario):

$$\frac{\partial h}{\partial t} + \frac{\partial (uh)}{\partial x} = S_m$$

Desglose de términos:
- **Variación temporal de la profundidad ($\frac{\partial h}{\partial t}$):** Representa cómo sube o baja el nivel hidrodinámico ($h$) de la onda en un punto fijo a medida que pasa el tiempo.
- **Gradiente de flujo o de masa ($\frac{\partial (uh)}{\partial x}$):** Refleja el cambio espacial del caudal. Describe cómo el movimiento del fluido (con velocidad media $u$) transporta la masa a lo largo de la coordenada $x$. En 2D, se suma la contribución ortogonal ($v$) en dirección $y$: $\frac{\partial (uh)}{\partial x} + \frac{\partial (vh)}{\partial y}$.
- **Término fuente/sumidero ("Bulking") ($S_m$):** Es vital para flujos de lodo/detritos. Consiste en la incorporación de sedimentos del lecho (erosión local) o la pérdida de masa/agua, alterando significativamente el volumen total en tránsito.

#### 2. Ecuación de conservación de cantidad de movimiento (momento lineal)
Es el derivado de la Segunda Ley de Newton para un fluido superficial. Relaciona las aceleraciones tridimensionales del evento con las fuerzas que lo impulsan (como el plano de gravedad) contra las que lo frenan (el esfuerzo material y las reologías).

En 1D, su presentación analítica se formula como:

$$\frac{\partial (uh)}{\partial t} + \frac{\partial}{\partial x} \left( u^2h + \frac{1}{2}gh^2 \right) = gh(S_0 - S_f - S_{MD})$$

**A. Lado Izquierdo (Aceleraciones e Inercia)**
- **Aceleración local ($\frac{\partial (uh)}{\partial t}$):** El cambio neto de la cantidad de movimiento local únicamente por el avance del tiempo (muy crítico a la hora de procesar o suavizar el arribo del frente brusco en flujos no estacionarios).
- **Aceleración convectiva ($\frac{\partial (u^2h)}{\partial x}$):** Transporte de cantidad de movimiento por la traslación del fluido. Explica los cambios o cuellos de botella por variaciones en la sección o velocidad topográfica.
- **Gradiente de presión hidrostática ($\frac{\partial (\frac{1}{2}gh^2)}{\partial x}$):** Fuerza que actúa empujando aguas abajo generada en la propia dinámica del terreno, yendo desde las crestas transitorias engrosadas hacia porciones menos profundas.

**B. Lado Derecho (Esfuerzos propulsores y resistivos)**
Aquí es donde radica la precisión del modelo y sus diferencias sustanciales con aguas claras. Se utilizan convencionalmente tres pendientes ("Slope") bien diferenciables:
- **Pendiente topográfica o del lecho ($S_0$):** Equivale a $\sin \theta$. Es la fuerza netamente impulsora producida por el peso topográfico que proyecta la masa pendiente abajo.
- **Pendiente de fricción basal ($S_f$):** Representa la resistencia externa en el contorno del valle (suelo). Para un flujo newtoniano clásico, se usaría la hidráulica tradicional (como la fricción de pérdida Manning $S_f = \frac{n^2 u^2}{h^{4/3}}$).
- **Pendiente de lodo y detritos ($S_{MD}$):** Representa las fundamentales *pérdidas internas* del perfil del flujo (viscosidades de la suspensión de arcillas, colisiones macrogranulares y resistencias inerciales inelásticas).

Normalmente, los modelos aplican la regla de transformar analíticamente el esfuerzo interno reológico ($\tau_{MD}$) en su representativo "pérdida de pendiente":
$$S_{MD} = \frac{\tau_{MD}}{\rho_m g R}$$
donde $\rho_m$ es la densidad de la mezcla en rotación de sedimentos y agua ($kg/m^3$) y $R$ es el perímetro y radio hidráulico ($h$ de tirante principal puro en flujos lateralizados anchos).

---

El cálculo específico de $S_{MD}$ (o la adaptación de $S_f$) se determinará según el **modelo reológico** seleccionado. Una vez definido el tipo de flujo y el mecanismo de disipación de energía, cada comportamiento hidrodinámico particular (Bingham, O'Brien, Voellmy, etc.) tendrá su sub-traducción en esta pérdida de pendiente. Para un detalle riguroso de cada modelo reológico, sus parámetros y correspondencia matemática, consulte los capítulos [Tipos de flujos](04_TiposFlujos.md) y [Modelos reológicos](04_ModelosReologicos.md).

---

Existen a su vez simplificaciones para predicciones globales en tiempo rápido usadas analíticamente para proyecciones de alcances de depositación a nivel de diseño preliminar de infraestructuras (como el método del bloque de masas integradas o "box model" referenciado en RAMMS y correlativos del RMB). Suprimiendo de manera integral la hidrodinámica promediada de Saint-Venant por un cálculo netamente acelerativo 1D clásico a todo el volumen inercial movilizado de manera fija (sintetizado localmente en Fuerza Neta = masa ⋅ aceleración):

$$𝑚\frac{\partial\vec{u}}{\partial t} = 𝑚𝑔\sin\theta−\tau_b$$

Por esto, la simulacion computacional integral que permita comprender frentes bifásicos con engrosamiento y *bulking* o el flujo transversal adaptativo a los conos y los cambios abanicos del aluvión (que prevengan cuellos de botella no previstos), exigen modelos de cálculo con integradores sobre ambas ecuaciones conjuntas acopladas de masa y momento de Saint-Venant en alta iteración temporal.

### Modelos numéricos de flujos de escombros: conservación de masa, momento y reología

| Modelo        | Conservación de masa                             | Conservación de momento                                     | Reología utilizada                                | Dimensiones | Comentarios principales                                                 |
|---------------|--------------------------------------------------|--------------------------------------------------------------|---------------------------------------------------|--------------|-------------------------------------------------------------------------|
| **HEC-RAS**   | $\displaystyle \frac{\partial h}{\partial t} + \frac{\partial (hu)}{\partial x} = S_m$ | $\displaystyle \frac{\partial (hu)}{\partial t} + \frac{\partial (hu^2)}{\partial x} = g h \sin\theta - \frac{\tau_b}{\rho}$ | Bingham, Herschel–Bulkley, lineal                 | 1D / 2D       | Hidráulica no newtoniana en cauces, incluye módulo sedimentológico     |
| **RAMMS::DF** | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = 0$             | $\displaystyle \frac{\partial (h \vec{u})}{\partial t} + \nabla \cdot (h \vec{u} \otimes \vec{u}) = -g h \nabla z - \mu g h \cos\theta - \frac{\vec{u}^2}{\xi}$ | Voellmy–Salm                                      | 2D            | Simulación de alta resolución sobre DEM, calibración con runout        |
| **FLO-2D**    | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = 0$             | $\displaystyle \frac{\partial (h \vec{u})}{\partial t} + \nabla \cdot (h \vec{u}^2) = g h \sin\theta - \tau_y - \mu \frac{u}{h} - k_d \left( \frac{u}{h} \right)^2$ | O’Brien–Julien (Bingham + dispersivo)             | 2D            | Permite erosión, deposición y flujos urbanos                           |
| **DAN3D**     | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = 0$             | $\displaystyle \frac{\partial (h \vec{u})}{\partial t} + \nabla \cdot (h \vec{u} \otimes \vec{u}) = -g h \nabla z - \frac{\tau_b}{\rho}$ | Voellmy, Coulomb, viscoplástico                   | 3D            | Simula caída, transformación y flujo tridimensional                    |
| **r.avaflow** | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = S_m$           | Ecuaciones de mezcla bifásica {cite}`pudasaini_hutter_2007`      | Mezcla sólido-líquido no newtoniana               | 2D (raster)   | Modelo acoplado sólido-fluido, erosión dinámica                        |
| **Flow-R**    | —                                                | $\displaystyle E_{\text{kin}} = E_{\text{pot}} - E_{\text{fricción}}$ | Fricción basal (ángulo de talud)                  | 2D (raster)   | Modelo empírico-geométrico para simulación de trayectoria y runout     |
| **Box models**| —                                                | $\displaystyle m \frac{du}{dt} = m g \sin\theta - \tau_b$     | Coulombiano                                        | 1D / simplificado | Estimación rápida de distancia de detención                           |
| **RMB**       | —                                                | $\displaystyle E_k + E_p = \text{constante} - \int \tau_b dx$ | Voellmy (simplificado energético)                 | 1D            | Balance energético para flujos sin cambio de masa                      |

```{bibliography}
:filter: docname in docnames
```
