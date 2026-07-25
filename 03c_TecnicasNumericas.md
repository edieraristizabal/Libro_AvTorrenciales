<p style="font-size:11px;"><em><strong>Créditos</strong>: El contenido de este capítulo ha sido tomado de varias fuentes, pero especialmente de Iverson & George {cite}`iverson_george_2024` en Advances in Debris-flow science and practice Eds. Matias Jakob, Scott McDougall, Paul Santi. (2024).</em></p>

# Técnicas numéricas de solución
El núcleo matemático de casi todos los modelos prácticos de flujo de escombros basados en física consiste en ecuaciones diferenciales parciales que representan leyes de conservación de masa y momento, promediadas en profundidad, de la mecánica del continuo para flujos que son poco profundos {cite}`iverson_george_2014`.  

Mientras que los modelos 3-D calculan flujos de momento en evolución en tres direcciones coordenadas, la mayoría de los modelos promediados en profundidad asumen que los flujos de momento normales al lecho pueden ser despreciados, lo que implica que las tensiones normales basales equilibran el peso estático del material suprayacente. 
Iverson {cite}`iverson_2005` proporcionó una evaluación cuantitativa de esta suposición y de las formas en que puede relajarse. 
Aunque la suposición de una tensión basal normal estática podría parecer muy restrictiva, la experiencia con modelos promediados en profundidad de diversos fenómenos, que van desde tsunamis e inundaciones hasta avalanchas granulares, ha mostrado que estos modelos comúnmente producen predicciones prácticas adecuadas incluso para flujos en los que la suposición se viola local o transitoriamente {cite}`george_augmented_2010,gray_tai_2003,leveque_clawpack_2011`.

Los modelos de flujo de escombros promediados en profundidad también asumen generalmente que las variaciones dependientes de la profundidad en el momento aguas abajo son despreciables.
La idea central del promediado en profundidad es simplificar la realidad 3D a un problema 2D. En lugar de calcular la velocidad y la densidad en cada punto de la columna de flujo, el modelo calcula un único valor promedio para la velocidad y la densidad en cada celda del mapa. 
sin embargo, el momento de un flujo (su "cantidad de movimiento") es una propiedad clave para saber cuán lejos llegará y con qué fuerza impactará. El momento no depende de la velocidad (v), sino del flujo de momento, que es proporcional a la velocidad al cuadrado ($v^2$).
El problema matemático es que el promedio de los cuadrados no es igual al cuadrado del promedio.
Esto significa que al tomar la velocidad promedio que calcula el modelo y la elevamos al cuadrado para estimar el flujo de momento se subestima su valor.
Como en los modelos de flujo de agua poco profunda, se pueden hacer correcciones para los efectos de estas variaciones introduciendo coeficientes de distribución del momento {cite}`vreugdenhil_swe_1994`. 
Sin embargo, los valores de los coeficientes de distribución dependen de la forma de los perfiles de velocidad y densidad del flujo, que están poco restringidos para los flujos de escombros. 
Como consecuencia, la mayoría de los modelos de flujo de escombros promediados en profundidad excluyen los coeficientes por considerarlos una complicación injustificada. 
En su lugar, asumen que el momento del flujo de escombros aguas abajo puede aproximarse como uniforme a todas las profundidades.

Las ecuaciones de conservación promediadas en profundidad se derivan integrando las ecuaciones de conservación 3-D a través del espesor del flujo de escombros en la dirección coordenada que denotamos como z {cite}`iverson_2005`. 
Sin embargo, la dirección de z no es la misma en todos los modelos. 
Las coordenadas curvilíneas adaptadas al terreno, con z rotado de modo que sea normal al lecho en todas partes, son las más rigurosas desde el punto de vista matemático y facilitan la consideración del efecto de las aceleraciones centrípetas sobre las tensiones basales {cite}`gray_granular_1999,denlinger_iverson_2004,savage_hutter_1991b`. 
Sin embargo, las coordenadas curvilíneas pueden ser difíciles de emplear en simulaciones numéricas de flujo sobre terrenos tridimensionales accidentados, en parte porque las celdas computacionales adyacentes pueden tener diferencias bruscas en las direcciones z normales al lecho, lo que podría generar definiciones conflictivas de las profundidades del flujo.
Además, si la geometría del lecho cambia significativamente debido a erosión o deposición, las coordenadas curvilíneas adaptadas al terreno original pierden al menos parte de su relevancia. 
El uso de coordenadas cartesianas centradas en la Tierra, con z vertical de manera uniforme, es más simple, pero requiere cuidado en el cálculo de flujos de momento y tensiones basales, porque la orientación de los lechos inclinados no es normal a una coordenada z vertical {cite}`denlinger_iverson_2004,iverson_2005,torresluquis_2019`.

### Marco Euleriano o Lagrangiano

Los métodos numéricos estándar, como los métodos clásicos de diferencias finitas, son poco adecuados para estos problemas porque pueden producir soluciones físicamente espurias, dispersión numérica o inestabilidades numéricas. 
Estas deficiencias han motivado el desarrollo de clases especializadas de técnicas numéricas de solución, incluyendo los métodos de volúmenes finitos con captura de choques proporcionados por el proyecto de software de código abierto *Clawpack* {cite}`leveque_numerical_2002`.

Los flujos de escombros son fenómenos multiescala. El cuerpo principal del flujo puede tener cientos de metros de largo y moverse de forma relativamente uniforme. 
Pero el frente del flujo es una zona muy dinámica, con un borde muy definido, altas velocidades y gradientes de altura muy pronunciados. 
También puede haber ondas de choque o pulsos dentro del flujo. Si quisiéramos simular esto con precisión, necesitaríamos una resolución muy alta (celdas de menos de un metro) para capturar el frente, pero usar esa misma resolución para toda la cuenca sería computacionalmente carísimo, incluso imposible. 

El Refinamiento de Malla Adaptativo (AMR) {cite}`berger_oliger_1984` es una estrategia numérica diseñada precisamente para resolver este problema. 
En lugar de usar una única malla computacional con un tamaño de celda fijo para todo el dominio, AMR utiliza una jerarquía de mallas anidadas. 
Se empieza con una malla base gruesa que cubre toda el área. Luego, durante la simulación, el software identifica automáticamente las zonas "interesantes" (donde hay altos gradientes, como el frente del flujo) y coloca sobre ellas "parches" de mallas más finas. Estos parches se mueven y cambian de tamaño dinámicamente, siguiendo al flujo. 
Existen diversas implementaciones de AMR, pero el objetivo de todas las técnicas AMR es proporcionar resoluciones de malla óptimas para lograr precisión numérica y eficiencia computacional durante toda la simulación.

Las técnicas estándar de AMR desarrolladas para ecuaciones generales de conservación hiperbólica no son adecuadas para modelar flujos poco profundos promediados en profundidad que se mueven sobre topografía variable, porque estas técnicas no pueden preservar simultáneamente estados estacionarios balanceados (como estados estáticos) y conservar masa, momento y energía. 
Se desarrollaron técnicas AMR especializadas para superar este problema en el contexto de la modelación de tsunamis {cite}`george_leveque_2006,leveque_clawpack_2011`. 
Posteriormente, estas técnicas se extendieron a la modelación de flujos promediados en profundidad sobre topografía, como inundaciones superficiales {cite}`berger_debris_2011,george_augmented_2010` y flujos de escombros {cite}`george_iverson_2014`.

En el enfoque Euleriano (malla fija) el sistema de coordenadas o la malla computacional está fija en el espacio. El material (el flujo de escombros) se mueve a través de las celdas de esta malla fija. Es como una red de estaciones meteorológicas fijas en un mapa. Miden el viento y la lluvia a medida que las tormentas pasan por encima de ellas. Las estaciones no se mueven. El enfoque Euleriano es el que necesita AMR. Como la malla es fija, la única manera de tener alta resolución en unas zonas y baja en otras es refinando adaptativamente la malla. D-Claw es el ejemplo perfecto que da el texto: usa AMR para poner celdas de alta resolución solo en el frente del flujo, permitiéndole usar MDEs de muy alta calidad sin que el costo computacional sea prohibitivo. r.avaflow, por otro lado, usa un enfoque Euleriano pero con una malla uniforme (sin AMR), lo que lo hace computacionalmente más intensivo si se requiere alta resolución en todo el dominio.
Sin embargo, utiliza esquemas numéricos de solución de diferencias centrales no oscilatorias con disminución de la variación total (*TVD-NOC*, por sus siglas en inglés) {cite}`nessyahu_tadmor_1990`, que se han aplicado con éxito a problemas de flujos de masa en general {cite}`mergili_ravaflow_2017`.

Un método más distintivo para resolver el sistema hiperbólico de EDP en modelos promediados en profundidad de flujos de escombros es el enfoque lagrangiano sin malla conocido como hidrodinámica de partículas suavizadas (SPH, por sus siglas en inglés) {cite}`mcdougall_hungr_2004`. 
En el enfoque Lagrangiano (partículas móviles) no hay una malla fija. En su lugar, el modelo sigue a un conjunto de "partículas" o puntos computacionales que se mueven junto con el material. Es como soltar miles de boyas en un río. Para saber cómo se mueve el agua, sigues la trayectoria de cada boya. Las boyas se mueven con el flujo. 
El enfoque Lagrangiano es inherentemente adaptativo. 
La resolución espacial no la da una malla fija, sino la densidad de las partículas.
Donde el flujo se concentra o comprime, las partículas se juntan, y la resolución aumenta automáticamente.
Donde el flujo se expande, las partículas se separan, y la resolución disminuye.
Por esta razón, los métodos lagrangianos no necesitan AMR de la misma manera que los eulerianos. Su "malla" es el conjunto de partículas y ya es, por naturaleza, adaptativa.
A diferencia de los métodos eulerianos, los métodos lagrangianos formulan las EDP del modelo en un marco de referencia móvil que se traslada con el flujo. 
En las aplicaciones de SPH a flujos de escombros, la representación mecánica continua del material del flujo de escombros se reemplaza efectivamente por un conjunto de “partículas” columnares que interactúan y que abarcan el espesor del flujo a medida que se mueven aguas abajo {cite}`mcdougall_hungr_2004`. 
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
Pero puede presentar desafíos prácticos para modelar flujos sobre topografías complejas del mundo real. 
En general, es necesaria una transformación de las variables calculadas en coordenadas adaptadas al terreno a coordenadas cartesianas uniformes de MDE, y dicha transformación debe ser aproximada {cite}`mergili_ravaflow_2017`.
Esta transformación puede introducir pequeñas imprecisiones numéricas.

El Enfoque de Coordenadas Cartesianas Globales utilizado por D-Claw, SHALTOP, TITAN2D, RAMMS, trabaja directamente en el mismo sistema de coordenadas que el MDE (X, Y, Z). La malla computacional está fija y alineada, por ejemplo, con los ejes Norte-Sur y Este-Oeste.
Perto la física se vuelve más complicada de formular. 
La fuerza de la gravedad ahora debe descomponerse en componentes X, Y y Z, lo cual no es tan intuitivo para un flujo que se mueve sobre una superficie inclinada.
Estos esquemas deben ser bien balanceados para entender que en una ladera inclinada pero sin flujo (un lago en reposo, por ejemplo), la fuerza de la gravedad debe ser perfectamente balanceada por el gradiente de presión del agua, para que no se genere un movimiento artificial. D-Claw y SHALTOP han desarrollado esquemas numéricos muy avanzados para lograr este balance adecuado.

Otro enfoque para abordar la dificultad de modelar con precisión flujos poco profundos sobre topografía accidentada está implementado en el modelo *SHALTOP* {cite}`bouchut_model_2003,fernandeznieto_2008`, que resuelve las ecuaciones del modelo en coordenadas cartesianas globales pero corrige las ecuaciones para satisfacer el supuesto de flujo poco profundo aplicado en la dirección normal al lecho local. Este enfoque puede capturar aceleraciones normales al lecho debidas a la curvatura del terreno {cite}`peruzzetto_simplified_2021`, pero aún requiere que las variables normales al lecho se transformen a un sistema de referencia cartesiano representado por un MDE estándar. Al igual que D-Claw, *SHALTOP* utiliza esquemas numéricos de volúmenes finitos bien balanceados para resolver sistemas hiperbólicos de ecuaciones diferenciales {cite}`bouchut_2004`.

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

```{bibliography}
:filter: docname in docnames
```
