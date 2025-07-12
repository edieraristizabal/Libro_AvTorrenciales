<p style="font-size:11px;"><em><strong>Créditos</strong>: El contenido de este capítulo ha sido tomado de varias fuentes, pero especialmente de Iverson & George (2024) en Advances in Debris-flow science and practice Eds. Matias Jakob, Scott McDougall, Paul Santi. (2024).</em></p>

# Ecuaciones de Saint-Venant

Para modelar flujos de escombros (*debris flows*) y otros flujos, se emplean un conjunto de ecuaciones de conservación que derivan de la mecánica de fluidos y medios continuos. Las ecuaciones de Saint-Venant son una forma simplificada y promediada en profundidad de las ecuaciones de Navier–Stokes. Se utilizan para modelar flujos superficiales como ríos, avalanchas, lahares y *debris flows*. Estas ecuaciones resuelven la dinámica del flujo considerando solo las variaciones en el plano horizontal (x,y), y promediando las variables a lo largo de la vertical (z), lo que simplifica mucho el problema sin perder lo esencial.

Las ecuaciones de flujo de aguas someras (o de aguas poco profundas) resuelven simultáneamente las ecuaciones de conservación de masa y de momento para calcular la cota del agua y la velocidad. Las fuerzas de fricción entre el fluido y el contorno sólido son las principales fuerzas de resistencia en las ecuaciones hidráulicas estándar para agua clara newtoniana. Comparado con aguas limpias, los flujos de lodo y detritos generan fuerzas resistentes adicionales. El aumento del contenido de sólidos incrementa la viscosidad de los flujos no newtonianos, generando fuerzas resistentes internas dentro del fluido. A concentraciones más altas, particularmente con partículas gruesas, la colisión y fricción entre partículas introducen fuerzas resistentes internas adicionales. La mayoría de las modificaciones teóricas y numéricas implican la integración de las nuevas fuerzas internas del fluido en la ecuación de momento. 

La aplicación del transporte no newtoniano en un modelo de aguas someras (o de aguas poco profundas) requiere calcular las pérdidas internas añadiendo un término de pendiente a la pendiente de fricción ($S_f$) en la ecuación de momento y aumentando el flujo para tener en cuenta el volumen de los sólidos. La pendiente de fricción ($S_f$) del modelo de aguas someras representa las fuerzas que actúan contra el flujo en el contorno del fluido (por ejemplo, el canal), mientras que la pendiente de lodo y detritos ($S_{MD}$) representa las pérdidas internas debidas a la viscosidad, la turbulencia y/o la dispersión dentro del fluido.

Los términos utilizados en las ecuaciones de conservación de masa y momento de Saint-Venant para modelar flujos de escombros se traducen al español de la siguiente manera:

| **Término en inglés**               | **Símbolo**   | **Traducción al español**                            |
|--------------------------------------|---------------|------------------------------------------------------|
| Newtonian friction slope             | $𝑆_𝑓$         | Pendiente de fricción newtoniana                     |
| Mud and debris friction slope        | $𝑆_{𝑀D}$       | Pendiente de fricción para lodos y escombros         |


- **Pendiente de fricción newtoniana:** Representa la resistencia al flujo generada por la fricción basal y la viscosidad interna en materiales con comportamiento newtoniano, como el agua o fluidos con viscosidad constante. En hidráulica clásica, es análoga a la pendiente de energía perdida por fricción (e.g., fórmulas de Manning o Chezy).

- **Pendiente de fricción para lodos y escombros:** Representa la resistencia basal y interna característica de flujos no newtonianos, como mezclas de lodo y escombros, que pueden mostrar comportamiento viscoplástico (por ejemplo, tipo Bingham) o hiperconcentrado.

Generalmente los modelos entonces calculan un esfuerzo cortante no newtoniano basándose en la clasificación del flujo (p. ej., flujo de lodo, flujo de detritos, etc.) y el enfoque reológico apropiado (es decir, el modelo de esfuerzo-deformación). Luego, la librería integra el cortante viscoso, turbulento y de dispersión del modelo de esfuerzo-deformación en la ecuación de momento, convirtiendo el esfuerzo cortante en una pendiente ($𝑆_{𝑀D}$) y sumando esta pendiente a la pendiente de fricción ($S_f$). Adicionalmente, debido a que estos flujos pueden contener entre un 5% y un 70% de sólidos por volumen, un modelo de lecho fijo debe aumentar el volumen del flujo para tener en cuenta el impacto del sedimento en la masa y la profundidad del flujo.

En este sentido, los modelos numéricos para flujos de ladera suelen usar las ecuaciones de Saint-Venant adaptadas a flujos no newtonianos, en forma de conservación de masa y momento en 1D o 2D de la siguiente forma:

#### Ecuación de conservación de masa (Continuidad)
Para un flujo en una dirección horizontal (e.g. coordenada $x$), la ecuación de continuidad superficial en régimen no permanente en 1D es:

$$\frac{\partial A}{\partial t} + \frac{\partial Q}{\partial x} = 𝑆_m$$
 
Donde: $Q$ es el caudal [$m_3/s$] el cual se obtiene a partir de $h(x,t)$: espesor del flujo [m], $\vec{u}(x,t)$: velocidad media del flujo [m/s] y $A$ el área de la seccion transversal del canal [$m_2$]. $S_m$ es la fuente o pérdida de masa (por ejemplo, aporte de afluentes, erosión, infiltración) [m/s]. Esta ecuación dice que el cambio del espesor en el tiempo es igual a la diferencia entre lo que entra y lo que sale, más lo que se gana o pierde localmente.

#### Ecuación de conservación de cantidad de movimiento (momento lineal)
Esta ecuación representa el balance entre fuerzas propulsoras (gravedad) y resistencias (fricción basal, turbulencia, etc.). En 1D la ecuación de conservación de momento es:

$$\frac{\partial(Q)}{\partial t} + \frac{\partial(Q\vec{u})}{\partial x} = 𝑔 hsen⁡\theta − S_{MD} + 𝑆_f$$

$$S_{MD}=\frac{\tau_{MD}}{\rho_mgR}$$
​ 
Donde: $g$: gravedad, $\theta$: pendiente del terreno, $\tau_{MD}$ el esfuerzo cortante interno y reológico, $\rho_m$ la densidad de la mezcla de sedimentos y agua ($kg/m^3$) y $R$ el radio hidráulico (m). El radio hidráulico se define como el área de la sección transversal del flujo ($A$) dividida por el perímetro mojado ($P$).

Existen modelos simplificados (usan solo la ecuación de momento), tales como algunos modelos empíricos o semi-analíticos, algunos modelos usados para estimar alcance máximo o zona de detención (por ejemplo, el método de "box model" o modelos de trayectoria pura). Usan solo Fuerza neta = masa⋅aceleración. Se considera una masa movilizada fija, y se analiza cómo frena con diferentes mecanismos (fricción basal, turbulencia). A veces se reduce a un problema 1D con:

$$𝑚\frac{\partial\vec{u}}{\partial t}=𝑚𝑔sin𝜃−𝜏_𝑏$$
​
Pero si se requiere simular procesos dinámicos completos, como evolución del espesor del flujo, deposición progresiva, erosión basal, bifurcaciones de cauce, es obligatorio usar ambas ecuaciones de Saint-Venant.

### Modelos numéricos de flujos de escombros: conservación de masa, momento y reología

| Modelo        | Conservación de masa                             | Conservación de momento                                     | Reología utilizada                                | Dimensiones | Comentarios principales                                                 |
|---------------|--------------------------------------------------|--------------------------------------------------------------|---------------------------------------------------|--------------|-------------------------------------------------------------------------|
| **HEC-RAS**   | $\displaystyle \frac{\partial h}{\partial t} + \frac{\partial (hu)}{\partial x} = S_m$ | $\displaystyle \frac{\partial (hu)}{\partial t} + \frac{\partial (hu^2)}{\partial x} = g h \sin\theta - \frac{\tau_b}{\rho}$ | Bingham, Herschel–Bulkley, lineal                 | 1D / 2D       | Hidráulica no newtoniana en cauces, incluye módulo sedimentológico     |
| **RAMMS::DF** | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = 0$             | $\displaystyle \frac{\partial (h \vec{u})}{\partial t} + \nabla \cdot (h \vec{u} \otimes \vec{u}) = -g h \nabla z - \mu g h \cos\theta - \frac{\vec{u}^2}{\xi}$ | Voellmy–Salm                                      | 2D            | Simulación de alta resolución sobre DEM, calibración con runout        |
| **FLO-2D**    | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = 0$             | $\displaystyle \frac{\partial (h \vec{u})}{\partial t} + \nabla \cdot (h \vec{u}^2) = g h \sin\theta - \tau_y - \mu \frac{u}{h} - k_d \left( \frac{u}{h} \right)^2$ | O’Brien–Julien (Bingham + dispersivo)             | 2D            | Permite erosión, deposición y flujos urbanos                           |
| **DAN3D**     | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = 0$             | $\displaystyle \frac{\partial (h \vec{u})}{\partial t} + \nabla \cdot (h \vec{u} \otimes \vec{u}) = -g h \nabla z - \frac{\tau_b}{\rho}$ | Voellmy, Coulomb, viscoplástico                   | 3D            | Simula caída, transformación y flujo tridimensional                    |
| **r.avaflow** | $\displaystyle \frac{\partial h}{\partial t} + \nabla \cdot (h \vec{u}) = S_m$           | Ecuaciones de mezcla bifásica (Pudasaini & Hutter 2007)      | Mezcla sólido-líquido no newtoniana               | 2D (raster)   | Modelo acoplado sólido-fluido, erosión dinámica                        |
| **Flow-R**    | —                                                | $\displaystyle E_{\text{kin}} = E_{\text{pot}} - E_{\text{fricción}}$ | Fricción basal (ángulo de talud)                  | 2D (raster)   | Modelo empírico-geométrico para simulación de trayectoria y runout     |
| **Box models**| —                                                | $\displaystyle m \frac{du}{dt} = m g \sin\theta - \tau_b$     | Coulombiano                                        | 1D / simplificado | Estimación rápida de distancia de detención                           |
| **RMB**       | —                                                | $\displaystyle E_k + E_p = \text{constante} - \int \tau_b dx$ | Voellmy (simplificado energético)                 | 1D            | Balance energético para flujos sin cambio de masa                      |

## Evolución histórica de los modelos de flujos

La dinámica de fluidos avanzada ofrece una amplia gama de enfoques de modelización dinámica basados en la física para los flujos de escombros. Estos modelos a menudo se centran en las ecuaciones de flujo somero (*shallow flow*) en dos dimensiones, pero varían considerablemente entre sí en términos de su concepto, complejidad y capacidad para modelar tipos específicos de fenómenos.

El trabajo pionero en la modelización de flujos fue realizado por Voellmy (1955), quien introdujo un modelo de fricción que combinaba un término de fricción seca (tipo Coulomb) y un término de resistencia viscosa-turbulenta. Este enfoque sentó las bases para muchos modelos posteriores. A partir de ahí, la comunidad científica vio una progresión significativa, con contribuciones clave de investigadores como Grigoriyan et al. (1967) y Takahashi (1991).

Un hito fundamental fue el trabajo de Savage y Hutter (1989), quienes introdujeron un conjunto de ecuaciones de conservación de masa y momento promediadas en la profundidad para flujos granulares secos. Su modelo, basado en la mecánica de suelos y la plasticidad, se convirtió en un estándar en el campo y fue posteriormente utilizado, modificado y extendido por numerosos investigadores, incluyendo a Mangeney et al. (2003, 2005), Denlinger e Iverson (2004), y McDougall y Hungr (2004, 2005).

El siguiente gran paso fue la incorporación de los efectos del fluido intersticial, reconociendo que la mayoría de los flujos de detritos no son secos. El modelo de Savage y Hutter fue extendido para incluir los efectos de la presión de poros por Iverson y Denlinger (2001), Savage e Iverson (2003), y otros como Pastor et al. (2009) y Hutter y Schneider (2010). Estos modelos, aunque representaban un gran avance, eran en su mayoría "efectivamente monofásicos" o "cuasi-bifásicos". Trataban la mezcla como un único continuo cuyas propiedades eran modificadas por la presencia del agua (por ejemplo, reduciendo la fricción basal), pero no resolvían completamente las ecuaciones de movimiento para la fase sólida y la fase fluida de forma independiente.

El desarrollo de modelos verdaderamente bifásicos fue el siguiente horizonte. Pitman y Le (2005) propusieron un modelo de "dos fluidos", y posteriormente, softwares como *GeoClaw* y su extensión *D-Claw* (Berger et al., 2011; Iverson y George, 2016) han considerado flujos de aguas someras y cuasi-bifásicos. Sin embargo, fue Pudasaini (2012) quien introdujo un modelo general bifásico que incluía de forma rigurosa varios aspectos físicos nuevos y esenciales de las mezclas sólido-fluido, como el arrastre generalizado, la masa virtual y un esfuerzo viscoso no-newtoniano. En comparación con los modelos monofásicos y otros enfoques bifásicos (ej. Kowalski y McElwaine, 2013), este marco teórico se mostró especialmente adecuado para la simulación realista de cadenas de procesos e interacciones complejas, como el impacto de un deslizamiento en un lago, el desbordamiento de la presa y el flujo de detritos resultante aguas abajo.

Paralelamente, la comunidad científica reconoció la importancia de procesos como el *entrainment* (la incorporación de material del lecho por el flujo), que puede aumentar sustancialmente el volumen y el poder destructivo de un flujo (Hungr y Evans, 2004). Se propusieron tanto leyes empíricas (Rickenmann et al., 2003; McDougall y Hungr, 2005) como conceptos mecánicos más rigurosos (Iverson, 2012) para modelar este fenómeno. No obstante, la mayoría de los modelos de *entrainment* disponibles seguían siendo monofásicos. De manera similar, aunque se reconoció la importancia de la depositación y el cambio asociado en la topografía basal, los intentos de simular explícitamente la retención y depositación del material de flujo han sido escasos en la literatura.

Desde el punto de vista numérico, se han utilizado diversos esquemas para resolver las ecuaciones de los modelos de flujo (ej. Nessyahu y Tadmor, 1990; Tai et al., 2002). Un desafío persistente ha sido la aplicación matemáticamente consistente de estos modelos, a menudo formulados en coordenadas que siguen la topografía, a las topografías arbitrarias y complejas del mundo real, que se representan en coordenadas cartesianas globales en los SIG. A pesar de estos desafíos, varios de los modelos mencionados se han implementado en herramientas computacionales ampliamente utilizadas para la cartografía de amenazas, como *DAN* (Hungr, 1995), *TITAN2D* (Pitman et al., 2003b) o *RAMMS* (Christen et al., 2010a, b).

Sin embargo, una limitación común de muchas de estas herramientas es su capacidad limitada para simular explícitamente la detención y depositación, y, sobre todo, para manejar cadenas de procesos complejas. Es en este contexto de necesidades no cubiertas donde surgieron modelos de nueva generación como `r.avaflow`, buscando integrar la física bifásica avanzada con la capacidad de simular estas complejas interacciones de procesos.

## Técnicas numéricas de solución
El núcleo matemático de casi todos los modelos prácticos de flujo de escombros basados en física consiste en ecuaciones diferenciales parciales que representan leyes de conservación de masa y momento, promediadas en profundidad, de la mecánica del continuo para flujos que son poco profundos (Iverson & George, 2014).  

Mientras que los modelos 3-D calculan flujos de momento en evolución en tres direcciones coordenadas, la mayoría de los modelos promediados en profundidad asumen que los flujos de momento normales al lecho pueden ser despreciados, lo que implica que las tensiones normales basales equilibran el peso estático del material suprayacente. 
Iverson (2005) proporcionó una evaluación cuantitativa de esta suposición y de las formas en que puede relajarse. 
Aunque la suposición de una tensión basal normal estática podría parecer muy restrictiva, la experiencia con modelos promediados en profundidad de diversos fenómenos, que van desde tsunamis e inundaciones hasta avalanchas granulares, ha mostrado que estos modelos comúnmente producen predicciones prácticas adecuadas incluso para flujos en los que la suposición se viola local o transitoriamente (George, 2010; Gray et al., 2003; LeVeque et al., 2011).

Los modelos de flujo de escombros promediados en profundidad también asumen generalmente que las variaciones dependientes de la profundidad en el momento aguas abajo son despreciables.
La idea central del promediado en profundidad es simplificar la realidad 3D a un problema 2D. En lugar de calcular la velocidad y la densidad en cada punto de la columna de flujo, el modelo calcula un único valor promedio para la velocidad y la densidad en cada celda del mapa. 
sin embargo, el momento de un flujo (su "cantidad de movimiento") es una propiedad clave para saber cuán lejos llegará y con qué fuerza impactará. El momento no depende de la velocidad (v), sino del flujo de momento, que es proporcional a la velocidad al cuadrado ($v^2$).
El problema matemático es que el promedio de los cuadrados no es igual al cuadrado del promedio.
Esto significa que al tomar la velocidad promedio que calcula el modelo y la elevamos al cuadrado para estimar el flujo de momento se subestima su valor.
Como en los modelos de flujo de agua poco profunda, se pueden hacer correcciones para los efectos de estas variaciones introduciendo coeficientes de distribución del momento (Vreugdenhil, 1994). 
Sin embargo, los valores de los coeficientes de distribución dependen de la forma de los perfiles de velocidad y densidad del flujo, que están poco restringidos para los flujos de escombros. 
Como consecuencia, la mayoría de los modelos de flujo de escombros promediados en profundidad excluyen los coeficientes por considerarlos una complicación injustificada. 
En su lugar, asumen que el momento del flujo de escombros aguas abajo puede aproximarse como uniforme a todas las profundidades.

Las ecuaciones de conservación promediadas en profundidad se derivan integrando las ecuaciones de conservación 3-D a través del espesor del flujo de escombros en la dirección coordenada que denotamos como z (Iverson, 2005). 
Sin embargo, la dirección de z no es la misma en todos los modelos. 
Las coordenadas curvilíneas adaptadas al terreno, con z rotado de modo que sea normal al lecho en todas partes, son las más rigurosas desde el punto de vista matemático y facilitan la consideración del efecto de las aceleraciones centrípetas sobre las tensiones basales (Gray et al., 1999; Pudasaini et al., 2005; Savage & Hutter, 1991). 
Sin embargo, las coordenadas curvilíneas pueden ser difíciles de emplear en simulaciones numéricas de flujo sobre terrenos tridimensionales accidentados, en parte porque las celdas computacionales adyacentes pueden tener diferencias bruscas en las direcciones z normales al lecho, lo que podría generar definiciones conflictivas de las profundidades del flujo.
Además, si la geometría del lecho cambia significativamente debido a erosión o deposición, las coordenadas curvilíneas adaptadas al terreno original pierden al menos parte de su relevancia. 
El uso de coordenadas cartesianas centradas en la Tierra, con z vertical de manera uniforme, es más simple, pero requiere cuidado en el cálculo de flujos de momento y tensiones basales, porque la orientación de los lechos inclinados no es normal a una coordenada z vertical (Denlinger & Iverson, 2004; Iverson, 2005; Iverson & George, 2019a).

### Marco Euleriano o Lagrangiano

Los métodos numéricos estándar, como los métodos clásicos de diferencias finitas, son poco adecuados para estos problemas porque pueden producir soluciones físicamente espurias, dispersión numérica o inestabilidades numéricas. 
Estas deficiencias han motivado el desarrollo de clases especializadas de técnicas numéricas de solución, incluyendo los métodos de volúmenes finitos con captura de choques proporcionados por el proyecto de software de código abierto *Clawpack* (LeVeque, 2002, www.clawpack.org).

Los flujos de escombros son fenómenos multiescala. El cuerpo principal del flujo puede tener cientos de metros de largo y moverse de forma relativamente uniforme. 
Pero el frente del flujo es una zona muy dinámica, con un borde muy definido, altas velocidades y gradientes de altura muy pronunciados. 
También puede haber ondas de choque o pulsos dentro del flujo. Si quisiéramos simular esto con precisión, necesitaríamos una resolución muy alta (celdas de menos de un metro) para capturar el frente, pero usar esa misma resolución para toda la cuenca sería computacionalmente carísimo, incluso imposible. 

El Refinamiento de Malla Adaptativo (AMR) (Berger y Oliger, 1984) es una estrategia numérica diseñada precisamente para resolver este problema. 
En lugar de usar una única malla computacional con un tamaño de celda fijo para todo el dominio, AMR utiliza una jerarquía de mallas anidadas. 
Se empieza con una malla base gruesa que cubre toda el área. Luego, durante la simulación, el software identifica automáticamente las zonas "interesantes" (donde hay altos gradientes, como el frente del flujo) y coloca sobre ellas "parches" de mallas más finas. Estos parches se mueven y cambian de tamaño dinámicamente, siguiendo al flujo. 
Existen diversas implementaciones de AMR, pero el objetivo de todas las técnicas AMR es proporcionar resoluciones de malla óptimas para lograr precisión numérica y eficiencia computacional durante toda la simulación.

Las técnicas estándar de AMR desarrolladas para ecuaciones generales de conservación hiperbólica no son adecuadas para modelar flujos poco profundos promediados en profundidad que se mueven sobre topografía variable, porque estas técnicas no pueden preservar simultáneamente estados estacionarios balanceados (como estados estáticos) y conservar masa, momento y energía. 
Se desarrollaron técnicas AMR especializadas para superar este problema en el contexto de la modelación de tsunamis (George & LeVeque, 2006; LeVeque et al., 2011). 
Posteriormente, estas técnicas se extendieron a la modelación de flujos promediados en profundidad sobre topografía, como inundaciones superficiales (Berger et al., 2011; George, 2010) y flujos de escombros (George & Iverson, 2014).

En el enfoque Euleriano (malla fija) el sistema de coordenadas o la malla computacional está fija en el espacio. El material (el flujo de escombros) se mueve a través de las celdas de esta malla fija. Es como una red de estaciones meteorológicas fijas en un mapa. Miden el viento y la lluvia a medida que las tormentas pasan por encima de ellas. Las estaciones no se mueven. El enfoque Euleriano es el que necesita AMR. Como la malla es fija, la única manera de tener alta resolución en unas zonas y baja en otras es refinando adaptativamente la malla. D-Claw es el ejemplo perfecto que da el texto: usa AMR para poner celdas de alta resolución solo en el frente del flujo, permitiéndole usar MDEs de muy alta calidad sin que el costo computacional sea prohibitivo. r.avaflow, por otro lado, usa un enfoque Euleriano pero con una malla uniforme (sin AMR), lo que lo hace computacionalmente más intensivo si se requiere alta resolución en todo el dominio.
Sin embargo, utiliza esquemas numéricos de solución de diferencias centrales no oscilatorias con disminución de la variación total (*TVD-NOC*, por sus siglas en inglés) (Nessyahu & Tadmor, 1990), que se han aplicado con éxito a problemas de flujos de masa en general (véase Mergili et al., 2017, para ejemplos).

Un método más distintivo para resolver el sistema hiperbólico de EDP en modelos promediados en profundidad de flujos de escombros es el enfoque lagrangiano sin malla conocido como hidrodinámica de partículas suavizadas (SPH, por sus siglas en inglés) (McDougall & Hungr, 2004). 
En el enfoque Lagrangiano (partículas móviles) no hay una malla fija. En su lugar, el modelo sigue a un conjunto de "partículas" o puntos computacionales que se mueven junto con el material. Es como soltar miles de boyas en un río. Para saber cómo se mueve el agua, sigues la trayectoria de cada boya. Las boyas se mueven con el flujo. 
El enfoque Lagrangiano es inherentemente adaptativo. 
La resolución espacial no la da una malla fija, sino la densidad de las partículas.
Donde el flujo se concentra o comprime, las partículas se juntan, y la resolución aumenta automáticamente.
Donde el flujo se expande, las partículas se separan, y la resolución disminuye.
Por esta razón, los métodos lagrangianos no necesitan AMR de la misma manera que los eulerianos. Su "malla" es el conjunto de partículas y ya es, por naturaleza, adaptativa.
A diferencia de los métodos eulerianos, los métodos lagrangianos formulan las EDP del modelo en un marco de referencia móvil que se traslada con el flujo. 
En las aplicaciones de SPH a flujos de escombros, la representación mecánica continua del material del flujo de escombros se reemplaza efectivamente por un conjunto de “partículas” columnares que interactúan y que abarcan el espesor del flujo a medida que se mueven aguas abajo (McDougall & Hungr, 2004). 
Además, SPH elimina los efectos de las discontinuidades en las soluciones de las EDP que gobiernan mediante el uso de una fórmula de suavizado para promediar la mecánica de interacción entre partículas vecinas.

:::{figure-md} euleriano o lagrangiano
<img src="https://i.pinimg.com/1200x/e2/38/d6/e238d69b696c047d37561b24f912ae79.jpg" width="700px">

:::

### Marcos de referencia en modelos eulerianos
Los modelos Eulerianos (r.avaflow, D-Claw, SHALTOP, TITAN2D, RAMMS) operan sobre una malla o grilla fija y observan cómo el material del flujo pasa a través de ella. La gran diferencia entre ellos radica en el sistema de coordenadas que usan para resolver las ecuaciones de la física.

*r.avaflow* resuelve las ecuaciones en coordenadas locales adaptadas al terreno. 
El modelo, en cada celda de la malla, "se para" sobre la pendiente y alinea su propio sistema de coordenadas con la topografía local. 
Su eje x siempre apunta en la dirección de máxima pendiente, su eje y es horizontal (a lo largo de la curva de nivel) y su eje z es perpendicular (normal) a la superficie del terreno.
Esto confiere ventajas en términos de fidelidad física. 
Porque la fuerza de la gravedad se descompone de forma natural y directa en dos componentes.
Pero puede presentar desafíos prácticos para modelar flujos sobre topografías complejas del mundo real. P
En general, es necesaria una transformación de las variables calculadas en coordenadas adaptadas al terreno a coordenadas cartesianas uniformes de MDE, y dicha transformación debe ser aproximada (Mergili et al., 2017).
Esta transformación puede introducir pequeñas imprecisiones numéricas.

El Enfoque de Coordenadas Cartesianas Globales utilizado por D-Claw, SHALTOP, TITAN2D, RAMMS, trabaja directamente en el mismo sistema de coordenadas que el MDE (X, Y, Z). La malla computacional está fija y alineada, por ejemplo, con los ejes Norte-Sur y Este-Oeste.
Perto la física se vuelve más complicada de formular. 
La fuerza de la gravedad ahora debe descomponerse en componentes X, Y y Z, lo cual no es tan intuitivo para un flujo que se mueve sobre una superficie inclinada.
Estos esquemas deben ser bien balanceados para entender que en una ladera inclinada pero sin flujo (un lago en reposo, por ejemplo), la fuerza de la gravedad debe ser perfectamente balanceada por el gradiente de presión del agua, para que no se genere un movimiento artificial. D-Claw y SHALTOP han desarrollado esquemas numéricos muy avanzados para lograr este balance adecuado.

Otro enfoque para abordar la dificultad de modelar con precisión flujos poco profundos sobre topografía accidentada está implementado en el modelo *SHALTOP* (Bouchut et al., 2003; Lucas et al., 2007), que resuelve las ecuaciones del modelo en coordenadas cartesianas globales pero corrige las ecuaciones para satisfacer el supuesto de flujo poco profundo aplicado en la dirección normal al lecho local. Este enfoque puede capturar aceleraciones normales al lecho debidas a la curvatura del terreno (Peruzzetto et al., 2021), pero aún requiere que las variables normales al lecho se transformen a un sistema de referencia cartesiano representado por un MDE estándar. Al igual que D-Claw, *SHALTOP* utiliza esquemas numéricos de volúmenes finitos bien balanceados para resolver sistemas hiperbólicos de ecuaciones diferenciales (Bouchut, 2004).

| Modelo | Marco Numérico | Característica Clave |
| :--- | :--- | :--- |
| **HEC-RAS** | Euleriano | Resuelve las ecuaciones sobre una malla o grilla fija. |
| **RAMMS::DF** | Euleriano | Resuelve las ecuaciones sobre una malla fija (el DEM). |
| **FLO-2D** | Euleriano | Resuelve las ecuaciones sobre una malla fija. |
| **DAN3D** | Lagrangiano | Generalmente implementado con SPH (Smoothed Particle Hydrodynamics), sigue partículas que se mueven con el flujo. |
| **r.avaflow** | Euleriano | Resuelve las ecuaciones sobre una grilla ráster fija. |
| **Flow-R** | Euleriano | Opera sobre una grilla ráster fija, calculando trayectorias de flujo desde cada celda. |
| **Box models** | Lagrangiano | Trata el deslizamiento como un único objeto (un "bloque") y sigue su centro de masa. |
| **RMB** | Lagrangiano | Realiza un balance de energía sobre la masa total a medida que se desplaza, siguiendo al objeto. |








