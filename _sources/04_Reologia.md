
# Regímenes reológicos

La reología es el estudio de cómo los materiales se deforman bajo un esfuerzo (o estrés). Por lo tanto, los *modelos reológicos* a menudo se expresan como relaciones simples entre esfuerzo y deformación. 
Los modelos hidráulicos de aguas claras ya asumen un modelo reológico para las simulaciones hidrodinámicas. 
Asumen que el agua comienza a deformarse (movimiento o deformación) bajo cualquier esfuerzo (intersección en cero en la relación esfuerzo-deformación), la deformación aumenta linealmente con el esfuerzo, y la viscosidad del agua es la relación entre el esfuerzo y la deformación. 
Estas son las suposiciones del flujo "newtoniano". 
Existen fluidos que se desvían de estas suposiciones, incluyendo una intersección esfuerzo-deformación distinta de cero o una relación esfuerzo-deformación no lineal, o ambas.

:::{figure-md} flow taxonomy
<img src="https://i.pinimg.com/736x/a9/95/92/a99592e92c06eb073c1c7d7699c5785e.jpg" alt="Flow axonomy" width="700px">h

Modelos reológicos utilizados para simular (a) agua limpia y (b, c) flujos de lodos y flujos de escombros. Tomado de [HEC RAS Non-Newtonian User's Manual](https://www.hec.usace.army.mil/confluence/rasdocs/rasmuddebris/non-newtonian-user-s-manual/introduction-taxonomy-and-rheology-of-debris-flows).
:::

La propiedad reológica de un flujo conformado por aguas y sedimentos depende de una variedad de factores, tales como la concentración de sólidos en suspensión, la cohesión, la distribución del tamaño de las partículas (granulometría), la forma de las partículas, la fricción entre granos y la presión de poros. En general, a medida que la concentración aumenta y el tamaño de grano se vuelve más grueso, la mezcla de fluido y sedimento pasa a través de cinco clasificaciones: (1) Flujo Newtoniano (agua clara o transporte de sedimento aluvial), (2) flujo hiperconcentrado, (3) flujo de lodo, (4) flujo de detritos y (5) flujo clástico. Sin embargo, estos tipos de flujo son continuos y se solapan entre sí.

## Propiedades físicas y reológicas

**Densidad aparente (ρ):** Varía entre 1500 y 2500 kg/m³. Los flujos hiperconcentrados oscilan entre 1330 y 1800 kg/m³ y los flujos de escombros entre 1800 y 2300 kg/m³, dependiendo de la composición litológica.

**Viscosidad (μ, en Pa·s):** Comúnmente entre 0,001 y 0,1 Pa·s. Controla la resistencia al corte y depende de la concentración de sedimentos, especialmente de limo y arcilla.

**Esfuerzo cortante (τ):** Calculado mediante:

$$
τ = ρ * g * R * S
$$

donde *ρ* es la densidad, *g* la gravedad, *R* el radio hidráulico y *S* la pendiente. A mayor densidad, mayor capacidad erosiva.

**Presión intersticial (pfp):** Varía espacial y temporalmente, reduciendo la resistencia friccional cuando es alta, lo que incrementa la movilidad del flujo.

## Características hidráulicas

**Velocidad (u, en m/s):** La velocidad del flujo se puede descomponer en tres componentes (Doyle et al., 2007):
   - Velocidad superficial (*usurf*): calculada a partir de grabaciones de video.
   - Velocidad de desplazamiento (*ur*): velocidad total del flujo.
   - Velocidad del cuerpo (*ub*): velocidad media en profundidad para una ubicación dada.
   
La velocidad del cuerpo *ub* se considera proporcional a la velocidad superficial mediante un factor de corrección *k*, que varía entre 0,7 y 0,9 (Creutin et al., 2003) y está definido por una distribución vertical de velocidades (Cronin et al., 1999; Hayes et al., 2002). La velocidad del frente del flujo se usa frecuentemente en ecuaciones, ya que la cabeza del flujo, rica en bloques, juega un papel crucial en la intensidad inicial del impacto sobre estructuras (Lavigne y Suwa, 2004; Thouret et al., 2007).

**Caudal (Q, en m³/s):** Es función de la velocidad media del flujo, su capacidad de erosionar y cargar material del lecho y las orillas del canal, y la geometría del canal. La descarga se expresa mediante:
   
$$
Q(ti + 1 - ti) = ½ (Ai * ubi + Ai+1 * ubi+1)
$$

donde *A* es el área mojada, *ub* la velocidad del cuerpo y *i* representa las mediciones individuales en intervalos Δt = ti+1 - ti (Doyle et al., 2011). La tasa de descarga varía en el tiempo y el espacio debido a los ciclos de carga (*bulking*) y descarga (*debulking*) de sedimentos.

**Profundidad del flujo (H, en m):** Puede ser de 4 a 5 veces el espesor del depósito. A mayor profundidad, mayor área expuesta y mayor altura alcanzada en las estructuras.

**Movilidad del flujo:** La velocidad, el caudal, la profundidad y la relación ancho/profundidad del canal influyen en la movilidad del flujo y determinan la distancia de recorrido.


## Mecanismos de disipación de energía en flujos
Las diferencias entre flujo plástico, turbulento, dispersivo y de Coulomb se refieren a los mecanismos físicos dominantes que controlan cómo se resiste o disipa la energía del flujo en movimiento. Estos mecanismos de disipación de energía en flujos de escombros (*debris flows*), que pueden coexistir o dominar en diferentes momentos o zonas del flujo.

| Tipo de flujo            | Ecuación general del esfuerzo cortante                                                                                 | Variables principales                                                                               |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Viscoso**              | $\tau = \mu , \dot{\gamma}$                                                                                          | $\mu$: viscosidad dinámica <br> $\dot{\gamma}$: tasa de cizalla                                 |
| **Plástico (Bingham)**   | $\tau = \tau_y + \mu_p , \dot{\gamma}$                                                                             | $\tau_y$: esfuerzo de fluencia <br> $\mu_p$: viscosidad plástica                              |
| **Turbulento**           | $\tau \propto \rho , u^2$                                                                                            | $\rho$: densidad <br> $u$: velocidad promedio                                                   |
| **Dispersivo (Bagnold)** | $\tau \propto \rho_s , d^2 , \dot{\gamma}^2$                                                                        | $\rho_s$: densidad de sólidos <br> $d$: tamaño de grano <br> $\dot{\gamma}$: tasa de cizalla |
| **Coulomb**          | $\tau = \sigma_n , \tan \phi + c$                                                                                   | $\sigma_n$: presión normal <br> $\phi$: ángulo de fricción interna <br> $c$: cohesión        |
| **Dilatante**            | $\tau = \sigma_n^{\text{eff}} , \tan \phi$ con $\sigma_n^{\text{eff}} = \sigma_n + \Delta \sigma_{\text{dil}}$ | $\Delta \sigma_{\text{dil}}$: aumento de presión normal por expansión volumétrica                |


### Flujo Friccional

* **Mecanismo Dominante:** La resistencia al movimiento es controlada por la fricción de contacto entre las partículas sólidas y entre estas y el lecho. Es una resistencia seca, independiente de la velocidad.
* **Explicación:** Este es el comportamiento más simple y se rige por la ley de fricción de Coulomb. La fuerza de resistencia es directamente proporcional a la fuerza normal (el peso del material perpendicular a la pendiente) y a un coeficiente de fricción ($\mu$ o $\tan\phi$). No hay términos que dependan de la velocidad de deformación (viscosidad) ni de la turbulencia. Es la física de un sólido deslizándose sobre otro.
* **Ejemplo Intuitivo:** Imagina empujar una caja de madera pesada sobre un suelo de cemento. La fuerza que necesitas para moverla depende del peso de la caja y de la rugosidad de las superficies, no de si la empujas lenta o rápidamente.
* **Tipo de flujo:** Es el modelo ideal para avalanchas de rocas secas, deslizamientos de bloques cohesivos, o la fase inicial de un deslizamiento donde el agua aún no juega un papel dominante.

### Flujo Viscoso

* **Mecanismo Dominante:** La resistencia al movimiento proviene de la fricción interna del propio fluido intersticial, que se opone a la deformación. La resistencia es directamente proporcional a la tasa de deformación ($\dot{\gamma}$).
* **Explicación:** En este régimen, no existe un umbral de esfuerzo para iniciar el movimiento (esfuerzo de cedencia); el flujo comienza con cualquier esfuerzo, por pequeño que sea. La relación entre el esfuerzo aplicado y la deformación resultante es lineal, y la pendiente de esa relación es la viscosidad. Un fluido más viscoso ofrece más resistencia.
* **Ejemplo Intuitivo:** Compara verter agua y verter miel. Ambos fluyen inmediatamente al inclinar el recipiente, pero la miel, al ser mucho más viscosa, fluye mucho más lentamente porque su "fricción interna" es mayor.
* **Tipo de flujo:** Este comportamiento es típico de flujos muy diluidos con bajo contenido de sólidos, o de la fase fluida dentro de una mezcla más compleja. Es la base para entender la resistencia del "líquido" que transporta los sólidos.

### Flujo Plástico

* **Mecanismo Dominante:** La resistencia está dominada por un esfuerzo de cedencia o fluencia ($\tau_y$). El material se comporta como un sólido rígido hasta que el esfuerzo aplicado supera este umbral, momento en el que empieza a fluir como un fluido viscoso.
* **Explicación:** La resistencia total en un flujo plástico tiene dos componentes: una resistencia inicial constante (el esfuerzo de cedencia) y una resistencia que aumenta con la velocidad de deformación (la parte viscosa). La presencia de arcillas y limos en la matriz fluida es la que genera esta cohesión y resistencia inicial.
* **Ejemplo Intuitivo:** La pasta de dientes. Puedes poner el tubo boca abajo y no se cae (resiste la gravedad como un sólido). Necesitas apretar con una fuerza mínima (superar el esfuerzo de cedencia) para que empiece a fluir. Una vez que fluye, se comporta como un líquido muy espeso.
* **Tipo de flujo:** Es el modelo clásico para flujos de lodo (*mudflows*) y flujos de detritos ricos en finos cohesivos, donde la matriz de lodo tiene la capacidad de mantener en suspensión a las partículas más grandes cuando el flujo se detiene.

### Flujo Turbulento

* **Mecanismo Dominante:** La resistencia al flujo y el transporte de partículas provienen de la energía caótica de los remolinos (eddies) en la fase fluida.
* **Explicación:** En lugar de un flujo suave y ordenado (laminar), el movimiento es caótico, con un intenso intercambio de momento dentro del propio fluido. Esta turbulencia es la que mantiene a los sedimentos en suspensión. La resistencia en este régimen no es lineal con la velocidad, sino que es proporcional al cuadrado de la velocidad. Por eso, los flujos turbulentos pueden ser tan erosivos y destructivos.
* **Ejemplo Intuitivo:** Un río de montaña durante una creciente aquí en Antioquia. El agua no fluye de forma ordenada; hierve con remolinos que son capaces de arrancar y transportar piedras y troncos.
* **Tipo de flujo:** Es el régimen típico de los flujos hiperconcentrados y los flujos de lodo más diluidos y rápidos, donde la concentración de sólidos no es tan alta como para que las interacciones entre granos dominen.

### Flujo Dispersivo

* **Mecanismo Dominante:** La resistencia es generada por las colisiones e interacciones mecánicas entre las partículas sólidas grandes.
* **Explicación:** En flujos con alta concentración de granos gruesos, el momento se transfiere principalmente por el choque de un grano con otro. Estas colisiones generan una "presión dispersiva" que tiende a separar las partículas y se opone al cizallamiento. Este es el famoso efecto *Bagnold*. Es un comportamiento puramente granular, no viscoso. El esfuerzo dispersivo es proporcional al cuadrado del tamaño del grano y al cuadrado de la tasa de cizalla.
* **Ejemplo Intuitivo:** Imagina una caja de balines densamente empacados. Si la agitas vigorosamente, los balines chocan constantemente entre sí y contra las paredes, generando una presión interna que se opone al movimiento.
* **Tipo de flujo:** Es el mecanismo dominante en flujos de detritos granulares y secos y en el frente de muchas avalanchas de rocas, donde los bloques más grandes interactúan directamente.

### Flujo Dilatante

* **Mecanismo Dominante:** La resistencia proviene de la **expansión volumétrica (dilatancia) del esqueleto granular** cuando se somete a un esfuerzo de cizalla.
* **Explicación Detallada:** Cuando un material granular está densamente empaquetado, las partículas no pueden simplemente deslizarse unas sobre otras. Para moverse, necesitan "montarse" unas sobre otras, lo que obliga al volumen total de la masa a expandirse. Este trabajo mecánico de expansión consume energía y se manifiesta como una resistencia adicional al cizallamiento. A menudo coexiste con la fricción de Coulomb y los esfuerzos dispersivos.
* **Ejemplo Intuitivo:** Una bolsa de café en grano bien apretada. Si intentas meter la mano, sientes una fuerte resistencia. Los granos están tan juntos que para moverse necesitan separarse, y tú tienes que hacer fuerza para crear ese espacio.
* **Tipo de flujo:** Este fenómeno es especialmente importante en la **fase de iniciación del movimiento** de materiales granulares densos, como arenas compactas o la base de un flujo de detritos denso. Puede explicar por qué se necesita un esfuerzo inicial mayor para poner en movimiento una masa densa.

| Tipo de flujo       | Mecanismo de disipación principal         | Forma de disipación de energía                                                                 |
|---------------------|-------------------------------------------|------------------------------------------------------------------------------------------------|
| **Viscoso (laminar)**   | Fricción interna (viscosidad)              | Calor generado por fricción molecular entre capas del fluido                                   |
| **Plástico (Bingham, HB)** | Ruptura de estructuras cohesivas          | Trabajo mecánico necesario para superar el esfuerzo de fluencia ($\tau_y$) → pérdida irreversible |
| **Turbulento**         | Agitación caótica del fluido               | Cascada de vórtices → fricción microscópica → disipación en calor                              |
| **Dispersivo (granular)** | Colisiones inelásticas entre partículas   | Fricción interpartícula, deformación, calor, sonido, reorganización granular                    |
| **Coulomb**        | Fricción basal seca                        | Pérdida por roce entre masa movilizada y superficie subyacente (dependiente de $\tan\phi$)     |
| **Dilatante**          | Expansión volumétrica por cizalla          | Trabajo contra presión normal para permitir expansión → disipación mecánica                    |


## Números adimensionales

Existen parámetros cuantitativos que ayudan a distinguir los regímenes de flujo (plástico, turbulento, dispersivo, Coulomb) en flujos de escombros, basados en conceptos de mecánica de fluidos, reología y dinámica granular. Estos números adimensionales permiten evaluar qué tipo de comportamiento físico domina en un flujo dado. 

**Número de Bingham (Bn)**. Evalúa la importancia del umbral de fluencia (flujo plástico) frente al esfuerzo viscoso. Útil para identificar flujos tipo Bingham o Herschel–Bulkley, típicos en ambientes tropicales ricos en finos cohesivos.

$Bn=\frac{𝜏_𝑦⋅𝐿}{𝜇⋅𝑉}$
​
 
$\tau_y$: esfuerzo de fluencia (Pa). $L$: escala característica (por ejemplo, espesor del flujo). $\mu$: viscosidad plástica (Pa·s). $V$: velocidad del flujo (m/s)

* Bn ≫ 1: flujo dominantemente plástico → el esfuerzo de fluencia es más importante que el esfuerzo viscoso.

* Bn ≪ 1: flujo más viscoso o inercial → la cohesión es despreciable frente a la viscosidad o inercia.


**Número de Reynolds (Re)**. Mide la relación entre fuerzas inerciales y viscosas. Indica si el flujo es laminar o turbulento. Útil para evaluar si es más adecuado un modelo viscoso vs. turbulento (por ejemplo, aplicar Voellmy con término cuadrático cuando Re es alto)

$Re=\frac{𝜌⋅𝑉⋅𝐿}{𝜇}$
​
 
$\rho$: densidad del flujo. $V$: velocidad. $L$: altura del flujo. $\mu$: viscosidad dinámica.

* Re < 1000: régimen laminar → modelos como Bingham, Herschel–Bulkley son más válidos.

* Re > 2000–4000: régimen turbulento → la disipación turbulenta domina, apropiado para flujos rápidos y diluidos.

**Número de Savage (Sav)**. Relaciona energía cinética de partículas con presiones de confinamiento. Detecta flujo dispersivo granular. Muy útil para distinguir entre núcleo fangoso (Sav bajo) y cabeza de bloques (Sav alto) en un debris flow.

$Sav=\frac{\dot{\gamma}⋅𝑑}{(𝑃/𝜌_𝑠)^{1/2}}$
​
 
$\dot{\gamma}$: tasa de deformación. $d$: tamaño medio de grano. $P$: presión normal (típicamente $\sim \rho g h$). $\rho_s$: densidad de sólidos.

* Sav ≫ 1: flujo dispersivo/granular inercial, choques frecuentes → aplicar modelo de Bagnold o término cuadrático dispersivo.

* Sav ≪ 1: partículas confinadas, sin dispersión → flujo cohesivo o tipo lodo.

**Número de Froude (Fr)**. Indica la relación entre velocidad y gravedad. Clasifica flujo como subcrítico, crítico o supercrítico. En flujos de escombros: Fr > 1 suele asociarse a frentes dispersivos y rápidos → apropiado usar Voellmy o dispersivo.

$Fr=\frac{𝑉𝑔⋅ℎ}{V}$
​
 
$V$: velocidad del flujo. $g$: gravedad. $h$: espesor del flujo

* Fr < 1: flujo subcrítico (lento, estable)

* Fr > 1: flujo supercrítico (rápido, dominado por inercia)


**Número de Stokes (St)**. Relaciona la inercia de una partícula con la viscosidad del medio. Valores altos indican dominio de inercia granular → dispersión; valores bajos → régimen viscoso.

$St=\frac{𝜌𝑠⋅𝑑^2⋅\dot{\gamma}}{𝜇}$


| Número adimensional                        | Fórmula                                               | Descripción                                                                                                      | Valores típicos o umbrales                                              |
|---------------------------------------------|-------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Número de Froude**                       | Fr = √(u / gH)                                       | Relación entre la fuerza inercial y la fuerza gravitacional                                                     | <1: domina la gravedad<br>>1: domina la inercia                        |
| **Número de Reynolds**                     | NRe = ρ₀H(gL)¹ᐟ² / µf                               | Relación entre la fuerza inercial y la fuerza viscosa                                                           | <500: flujo laminar<br>500–12,500: flujo transicional<br>>12,500: turbulento |
| **Número de difusión de presión de poros** | NP = (L/g)¹ᐟ² µf H² / (kE)                           | Relación entre la escala temporal del flujo y la difusión normal al talud de la presión positiva del fluido de poros | -                                                                       |
| **Número inercial**                        | I = √(γ δ ̇P / ρ₀)                                   | Relación entre el esfuerzo inercial y el esfuerzo de confinamiento                                              | 1 × 10⁻⁵ – 1 × 10⁻¹ *(rango típico en flujos de detritos naturales)* (Jerolmack & Daniels, 2019) |
| **Número de Savage**                       | NS = (ρs – ρf) / ρs                                  | Relación entre el esfuerzo colisional y el esfuerzo por fricción                                                | <0.1: domina el esfuerzo por fricción<br>>0.1: domina el esfuerzo colisional |
| **Número de Bagnold**                      | NB = (1 – vs) / vs                                    | Relación entre el esfuerzo colisional y el esfuerzo viscoso                                                     | <40: domina el esfuerzo viscoso<br>>450: domina el esfuerzo colisional |
| **Número de fricción**                     | Nfric = (1 – vs) / vs · (ρs γ δ²) / µf               | Relación entre el esfuerzo por fricción y el esfuerzo viscoso                                                   | <100: domina el esfuerzo viscoso<br>>100: domina el esfuerzo por fricción |

## Modelos reológicos
Dada la complejidad de estos materiales de dos fases (sólido-líquido), no existe un modelo único que describa perfectamente todos los regímenes de flujo de escombros. En su lugar, se emplean modelos reológicos efectivos que tratan a la mezcla como un "fluido equivalente" para capturar su comportamiento general mediante unas pocas constantes. Estos modelos, aunque simplificados, permiten incorporar la física dominante (ya sea cohesión de finos, fricción granular o turbulencia) en simulaciones de flujo continuo (por ejemplo, en modelos de ladera o ecuaciones tipo aguas poco profundas). A continuación se presentan los principales modelos reológicos aplicables a flujos de escombros, junto con sus fundamentos físicos, supuestos, limitaciones y ámbitos de aplicación en contextos montañosos y tropicales.

:::{figure-md} rheology
<img src="https://www.mdpi.com/symmetry/symmetry-10-00094/article_deploy/html/images/symmetry-10-00094-g001.png" alt="rheology" width="500px">

Reologia de flujos. Tomado de [Wang et al. (2018)](https://www.mdpi.com/2073-8994/10/4/94/htm).
:::

Un rasgo distintivo de los flujos de escombros es su comportamiento viscoplástico y altamente no lineal. 
A concentraciones volumétricas de sedimento elevadas (por ejemplo, >40–50% de sólidos), la mezcla presenta un esfuerzo de fluencia (o esfuerzo de cedencia) por debajo del cual el material se comporta prácticamente como un sólido estático, y por encima del cual fluye rápidamente como un fluido pesado. 
Esto se atribuye a una red interconectada de partículas finas (arcillas, limos) y el entrelazamiento de granos que confiere una resistencia cohesiva al inicio del movimiento. 

Asimismo, una vez iniciada la fluencia, la relación entre el esfuerzo cortante ($\tau$) y la tasa de deformación ($\dot\gamma$) puede no ser constante: muchos flujos presentan comportamiento pseudoplástico (shear-thinning), donde la viscosidad aparente disminuye a mayores tasas de corte (debido a la alineación de partículas o rotura de estructuras interparticulares), mientras que otros podrían mostrar comportamiento dilatante (shear-thickening) si la agitación genera más choques entre granos a alta velocidad. 

Además, en flujos rápidos y de gran escala, pueden coexistir zonas laminares (en el núcleo más denso, de deformación lenta) y zonas turbulentas o dispersivas (en los bordes o en la cabeza del flujo, donde los granos chocan violentamente y el fluido se agita). El dominio reológico de un flujo de escombros depende en gran medida de su composición y del régimen de movimiento: por ejemplo, en flujos muy ricos en finos cohesivos (típicamente asociados a ambientes tropicales con suelos arcillosos o erupciones volcánicas que generan lahares), la cohesión interna domina y el material se asemeja a un lodo espeso con un claro umbral de fluencia, bien representado por modelos viscoplásticos como Bingham o Herschel-Bulkley. 
En cambio, en flujos con alto contenido de granos gruesos (típicos de cuencas montañosas empinadas con depósitos detríticos y bloques), la fricción granular y los choques entre partículas pueden predominar, pudiendo modelarse con esquemas de fricción tipo Coulomb o con términos turbulentos cuadráticos (e.g. modelo de Voellmy o modelos “dispersivos” de tipo Bagnold). 
Muchos flujos naturales ocupan un punto intermedio de este espectro, por lo que algunos enfoques combinan múltiples contribuciones reológicas (p. ej., el modelo “cuadrático” de O’Brien & Julien incluye simultáneamente un término cohesivo, uno viscoso lineal y uno cuadrático dispersivo). 

:::{figure-md} flow taxonomy
<img src="https://i.pinimg.com/736x/b0/85/c7/b085c7b4549b1401c87c3d79752032d5.jpg" alt="Flow axonomy" width="700px">

Taxonomía de flujos no Newtonianos con los modelos reológicos y ecuaciones utilizadas para modelar según Gibson et al., 2020. Tomado de [HEC RAS Non-Newtonian User's Manual](https://www.hec.usace.army.mil/confluence/rasdocs/rasmuddebris/non-newtonian-user-s-manual/introduction-taxonomy-and-rheology-of-debris-flows).
:::

La reología de los flujos de escombros es un campo complejo que integra conceptos de mecánica de fluidos no newtonianos, mecánica de suelos y dinámica de granulares. En contextos montañosos y tropicales, entender y modelar esta reología es crucial para predecir el comportamiento de estos flujos destructivos. Los modelos – Bingham, Herschel–Bulkley, Voellmy–Salm, entre otros – proporcionan marcos teóricos simplificados para representar distintos aspectos del flujo: cohesión de finos y viscosidad laminar en Bingham/HB, no linealidad pseudoplástica en HB, fricción basal y turbulencia en Voellmy, e interacciones granulares dispersivas en el modelo cuadrático de O’Brien. Cada modelo tiene fundamentos físicos bien establecidos (p. ej., $\tau_y$ ligado a la estructura de partículas, término $V^2$ ligado a colisiones) pero también supuestos limitantes (homogeneidad, parámetros constantes, ausencia de erosión). Por ello, no existe un modelo universal; la elección debe adaptarse al tipo de flujo y a los objetivos del análisis. 

A continuación se detalla cada modelo principal, con sus ecuaciones constitutivas, supuestos y aplicabilidad.

### Modelo de Bingham
El modelo de fluido de Bingham (ingham & Green, 1919) es uno de los más sencillos y empleados para describir flujos de detritos con alto contenido de finos. Se trata de un modelo viscoplástico: asume que el material posee un esfuerzo de fluencia $\tau_y$ (también llamado tensión umbral o cedente) que debe superarse para que ocurra deformación continua, y una vez superado ese umbral, el material fluye con un comportamiento plástico perfecto caracterizado por una viscosidad plástica aproximadamente constante $\mu_p$. Matemáticamente, la relación esfuerzo-deformación cortante se expresa como:

$\tau = \tau_y + \mu_p \dot\gamma$  

En esta formulación lineal con intercepto, $\tau_y$ representa el valor de esfuerzo cortante en el cual comienza el flujo (intercepto no nulo), mientras que $\mu_p$ es la pendiente de la relación tensión vs. tasa de corte, es decir, la viscosidad (constante) de la mezcla una vez movilizada. Por debajo de $\tau_y$, el material se comporta como un sólido rígido (no hay deformación irreversible), y por encima se comporta como un fluido newtoniano de alta viscosidad. Un ejemplo cotidiano de fluido tipo Bingham es la mayonesa, que no fluye hasta que la tensión aplicada excede cierto valor, tras lo cual se comporta como un líquido espeso. 

La ecuación de Bingham se aplica a menudo a flujos hiperconcentrados y flujos de lodo. En teoría, estos flujos de menor concentración se ajustan mejor al modelo lineal. Sin embargo, su formulación relativamente simple hace que sea más fácil de calibrar. Menos parámetros libres lo hacen menos vulnerable a problemas de equifinalidad. Por lo tanto, se ha aplicado con éxito a flujos de detritos de mayor concentración en aplicaciones de laboratorio y de campo.

El modelo de Bingham solo requiere dos datos de entrada por parte del usuario: el esfuerzo de cedencia (el intercepto de la relación esfuerzo-deformación) y la viscosidad del flujo cargado de sedimento (la pendiente de la relación esfuerzo-deformación). en el modelo HEC RAS Las opciones para estos se describen en las secciones de Esfuerzo de Cedencia y Viscosidad de la siguiente forma.

:::{figure-md} Bingham model
<img src="https://i.pinimg.com/736x/00/a8/97/00a897f9269263100dd73a4b25d9857b.jpg" width="700px">

Modelo de Bingham. Tomado de [HEC RAS Non-Newtonian User's Manual](https://www.hec.usace.army.mil/confluence/rasdocs/rasmuddebris/non-newtonian-user-s-manual/non-newtonian-transport-editor/non-newtonian-methods).
:::

El comportamiento Bingham en flujos de escombros se asocia a la presencia de una fase fina cohesiva (arcilla, limo) que genera enlaces inter-partícula y cohesión estática. Este esfuerzo cohesivo debe romperse para iniciar el flujo, de forma análoga a superar la resistencia al corte de un suelo cohesivo. Luego, la resistencia viscosa durante el flujo proviene de la fricción interna del fluido mezclado con partículas. Estudios experimentales con lodos naturales han demostrado que suspensiones de alta concentración (por ejemplo, material <2 mm de un flujo de escombros) se aproximan bien a un comportamiento de Bingham a tasas de corte moderadas y altas. Major y Pierson (1990) midieron reologías de un flujo de escombros natural y encontraron que, a tasas de deformación mayores de ~5 $s^-1$, la mezcla presentaba un límite de fluencia claro y viscosidad plástica definidas (comportándose como un Bingham plástico), con $\tau_y$ y $\mu_p$ fuertemente dependientes de la concentración de sedimento. 

El modelo de Bingham asume flujo laminar y homogéneo, con propiedades reológicas constantes durante el movimiento. Es más aplicable a flujos lentos o intermedios donde la turbulencia es despreciable y donde la cohesión de finos domina la resistencia (por eso, se recomienda para flujos con elevado contenido de finos arcillosos o limo). Por ejemplo, en flujos híper-concentrados o flujos de lodo iniciales, típicos en cuencas tropicales tras lluvias intensas, la matriz arcillosa induce un claro umbral de fluencia y altos valores de viscosidad, lo cual encaja en la idealización de Bingham. De hecho, en flujos híper-concentrados naturales se han reportado $\tau_y$ del orden de cientos de Pascales y viscosidades plásticas de $10^{-1}–10^1$ Pa·s o mayores, dependiendo de la concentración y mineralogía (valores que exceden por mucho la viscosidad del agua, 0.001 Pa·s). El modelo de Bingham se ha utilizado con éxito para simular flujos de detritos con altas concentraciones de sedimento tanto en laboratorio como en campo.

A pesar de su simplicidad, el modelo de Bingham tiene limitaciones importantes. En primer lugar, impone una relación lineal entre esfuerzo y tasa de deformación una vez iniciado el flujo, lo cual no siempre concuerda con materiales naturales: experimentos han mostrado que la relación puede ser no lineal (concavidades en la curva esfuerzo vs. deformación) debido a efectos de estructura interna o dispersión granular. Asimismo, la hipótesis de viscosidad constante solo es razonable a altas tasas de corte; a bajas tasas, muchos lodos exhiben tixotropía o variación de viscosidad (por ejemplo, la mezcla puede comportarse más rígida de lo predicho, endureciéndose al reposo). Major y Pierson notaron que por debajo de 5 $s^{-1}$ las suspensiones desviaban su comportamiento del modelo Bingham, indicando que otros procesos (formación de puente de partículas, etc.) entraban en juego. Otra limitación es que el modelo no incluye efectos granular-inerciales: si el flujo contiene una fracción importante de grava o bloques que interactúan por colisiones, el Bingham puro no capturará el aumento de resistencia a altas velocidades debido a esos choques. En tales casos, un término cuadrático (como veremos en otros modelos) sería necesario. Finalmente, la determinación de los parámetros $\tau_y$ y $\mu_p$ requiere datos experimentales (reometría, ensayos de flujo inclinado, etc.), y estos parámetros pueden variar dinámicamente si cambia la concentración (por erosión/dilución durante el recorrido), algo que el modelo base no contempla (se asume constantes). Aun con estas limitaciones, el modelo de Bingham proporciona una primera aproximación robusta para flujos donde la cohesión de finos y la viscosidad laminar son los controles primarios de la dinámica.

### Modelo de Herschel–Bulkley

El método de Herschel-Bulkley (Herschel & Bulkley, 1926) es un enfoque no lineal de dos términos para la reología de flujos. Este método eleva la deformación a una potencia, la cual puede ser mayor o menor que 1. A diferencia del método de Bingham que eleva la deformación a la potencia de 1, o el de O'Brien que utiliza un modelo cuadrático (elevando la deformación a las potencias de 1 y 2), el de Herschel-Bulkley puede elevar la deformación a potencias no enteras, ya sean mayores o menores que 1. El modelo de Herschel–Bulkley (HB) es una generalización del modelo de Bingham que permite capturar relaciones no lineales entre el esfuerzo cortante y la tasa de deformación, manteniendo a la vez la noción de un esfuerzo de fluencia. Su ecuación constitutiva se expresa típicamente como:

$\tau=\tau_y+ 𝐾 \dot\gamma^n$  

​
donde $\tau_y$ es de nuevo el esfuerzo umbral de fluencia, $K$ es el índice de consistencia (una especie de viscosidad generalizada) y $n$ es el índice de comportamiento (exponente de la ley de potencia). Cuando $n = 1$, el modelo de Herschel–Bulkley se reduce al caso Bingham simple (con $K$ equivalente a $\mu_p$). Si $n < 1$, el fluido es pseudoplástico (reóctipo adelgazante), exhibiendo viscosidad aparente decreciente con mayor tasa de corte (*shear-thinning*); por el contrario, $n > 1$ indica un comportamiento dilatante o espesante (*shear-thickening*), donde la viscosidad aparente aumenta al incrementarse $\dot\gamma$. En todos los casos, persiste la condición de umbral: por debajo de $\tau_y$ no hay deformación permanente, análogo a un sólido. 

:::{figure-md} Herschel-Bulckley model
<img src="https://i.pinimg.com/736x/2c/fb/9f/2cfb9f97792edddde512299d557b591c.jpg" width="700px">

Modelo de Herschel-Bulckley. Tomado de [HEC RAS Non-Newtonian User's Manual](https://www.hec.usace.army.mil/confluence/rasdocs/rasmuddebris/non-newtonian-user-s-manual/introduction-taxonomy-and-rheology-of-debris-flows).
:::


El modelo de Herschel-Bulkley requiere tres parámetros: El Esfuerzo de Cedencia en el modelo de Herschel-Bulkley es el mismo que en Bingham. Sin embargo, el parámetro lineal que acompaña al término de Deformación pierde sus unidades de viscosidad si la deformación se eleva a una potencia distinta de 1. Por lo tanto, K ya no es la viscosidad cuando el modelo de Herschel-Bulkley se desvía del modelo de Bingham (n≠1). Tanto $K$ como $n$ son parámetros empíricos definidos por el usuario.

:::{figure-md} Herschel-Bulckley model
<img src="https://i.pinimg.com/736x/58/ad/45/58ad45847d713f041cf494e1f1d6c2ab.jpg" width="700px">

Implementación del modelo de Herschel-Bulckley en HEC-RAS. Tomado de [HEC RAS Non-Newtonian User's Manual](https://www.hec.usace.army.mil/confluence/rasdocs/rasmuddebris/non-newtonian-user-s-manual/introduction-taxonomy-and-rheology-of-debris-flows).
:::


El modelo Herschel–Bulkley fue introducido para reflejar observaciones experimentales ya que muchos lodos naturales y sedimentos no siguen la relación lineal de Bingham, sino que presentan curvatura en la curva esfuerzo-deformación. Por ejemplo, Major y Pierson (1992) hallaron que, tras exceder $\tau_y$, los lodos podían mostrar inicialmente una pendiente alta (alta viscosidad aparente) que luego disminuía con mayor tasa de corte, sugiriendo comportamiento pseudoplástico (debido posiblemente a la destrucción progresiva de la estructura floculada). En esos casos, un exponente $n < 1$ en la fórmula HB brindaría un mejor ajuste que $n=1$. Este modelo es útil para suspensiones de finos bajo altas tasas de deformación donde la no linealidad es pronunciada. También se ha utilizado en modelación de flujos de escombros para incorporar cierta dependencia de la viscosidad con la velocidad de deformación, aportando mayor realismo que Bingham. Muchos códigos numéricos modernos (e.g. HEC-RAS 6.0) ofrecen la opción de Herschel–Bulkley generalizado justamente para permitir ajustar mejor la reología con datos de laboratorio. Típicamente, se encuentran valores de $n$ entre ~0.2 y 0.8 para lodos volcanogénicos o arcillosos (shear-thinning marcado), mientras que mezclas con arena gruesa pueden tender a $n$ cercano a 1 o incluso >1 si hay interacciones dilatantes. Por su parte, $K$ (consistencia) refleja la resistencia viscosa de la mezcla; sus unidades dependen del valor de $n$ (lo cual dificulta la interpretación física directa de $K$). Para dar una idea, un flujo con alta fracción de arcilla podría tener $\tau_y$ de varios cientos de Pa, $n \approx 0.5$ y $K$ correspondiente a viscosidades aparentes del orden de 1–10 Pa·s a tasas de corte típicas, mientras que un flujo más diluido podría tener $\tau_y$ bajo (cercano a 0) y comportamiento más Newtoniano ($n \to 1$). 

Al igual que Bingham, Herschel–Bulkley sigue siendo un modelo monofásico continuo que trata la mezcla heterogénea como un fluido efectivo. No incorpora explícitamente la física granular (colisiones, rozamiento inter-grano) ni efectos dependientes del tiempo como la tixotropía. Se asume también flujo laminar o lentamente variado, donde la tensión total se puede partir en un componente cohesivo (*yield*) más uno viscoso general. 

El modelo HB añade flexibilidad a costa de introducir más parámetros que requieren calibración. Determinar $\tau_y$, $K$ y $n$ simultáneamente exige datos reológicos detallados; frecuentemente $\tau_y$ se mide mediante pruebas de fluencia o reómetros de torsión a bajo corte, y luego $K, n$ se ajustan a curvas esfuerzo-$\dot\gamma$. La presencia de $n \neq 1$ conlleva que $K$ tenga unidades no triviales (Pa·s^n), lo cual complica su estimación a priori. Además, aunque HB captura la no linealidad, no representa explícitamente la transición sólido-fluido de manera dinámica: es decir, el mismo $\tau_y$ rige la iniciación y la detención, cuando en realidad en flujos naturales puede existir histéresis (se requiere más esfuerzo para iniciar que para mantener el flujo, debido a reestructuración interna). Por ello, a veces se usan variantes como el modelo de Papanastasiou que suaviza la transición en torno a $\tau_y$. Otra limitación es similar a Bingham: en escenarios de alto número de Reynolds o flujos muy rápidos, el modelo HB por sí solo no refleja la aparición de turbulencia ni de tensiones dispersivas por choques. En suma, Herschel–Bulkley es más general que Bingham y suele proporcionar mejores ajustes a datos reométricos de flujos de detritos reales, pero sigue siendo apropiado principalmente cuando el comportamiento está dominado por la matriz fluida y cohesiva bajo flujo laminar. En casos con componentes granulares dominantes o flujos extremadamente rápidos, será necesario complementarlo o optar por otros modelos.

### Modelo de Voellmy–Salm
El modelo de Voellmy–Salm surge originalmente en el contexto de las avalanchas de nieve (Voellmy, 1955; refinado por Salm et al., 1990) y ha sido adaptado con éxito para flujos de escombros y otros movimientos rápidos de detritos. A diferencia de los modelos viscoplásticos anteriormente descritos, Voellmy–Salm no se basa en una viscosidad de fluido, sino en una descripción de la resistencia al flujo como combinación de fricción seca y resistencia turbulenta. En esencia, este modelo asume que la fuerza resistiva por unidad de volumen (o la pendiente de energía $S_f$ equivalente) se puede descomponer en dos componentes: uno independiente de la velocidad (análogo a una fricción Coulomb constante) y otro proporcional al cuadrado de la velocidad (similar a una resistencia aerodinámica o turbulenta). Una forma típica de expresarlo es:

$𝑆_𝑓 = 𝜇_𝑓 𝑁 +\frac{𝜌_𝑚 𝑔 𝑉^2}{\xi}$  
 
donde $S_f$ es la pendiente de fricción, $\mu_f$ es el coeficiente de fricción "en seco" (análogo al $\tan\phi$ de un ángulo de fricción basal), $N$ es la fuerza normal (por unidad de área) sobre el lecho, $\rho_m$ es la densidad de la mezcla, $g$ la aceleración gravitacional, $V$ la velocidad del flujo, y $\xi$ es el coeficiente de fricción turbulenta (Voellmy). El término $\mu_f N$ representa una resistencia Coulombiana constante (proporcional al peso del material, $N \approx \rho_m g h \cos\theta$ en flujo sobre pendiente $\theta$), mientras que $\rho_m g V^2/\xi$ representa una resistencia dinámica cuadrática que crece con el cuadrado de la velocidad. En la práctica, $\mu_f$ y $\xi$ son parámetros que se calibran según el caso: $\mu_f$ típicamente varía en un rango 0.1–0.5 (adimensional) dependiendo de la pendiente de detención observada del flujo, y $\xi$ tiene unidades de [$L/T^2$] (similar a un coeficiente de *Chezy* invertido) con valores comunes entre ~100 y 1000 $m/s^2$. Un valor alto de $\xi$ indica baja resistencia turbulenta (fluidos más “suaves” o caminos menos accidentados), mientras que $\xi$ bajo significa que incluso velocidades moderadas generan gran resistencia (por ejemplo, cauces rugosos con muchos obstáculos, o flujos con intensas colisiones granulares). 

El modelo Voellmy–Salm conceptúa el flujo de detritos como un continuo granular fluido donde la resistencia al deslizamiento proviene de dos fuentes: (a) fricción basal entre el material y el lecho (y entre partículas, en promedio), representada por $\mu_f$ constante, y (b) pérdidas por energía de fluctuaciones turbulentas o dispersivas dentro del flujo, representadas por el término cuadrático. El término de fricción seca actúa como un esfuerzo de fluencia basal basado en el peso: si la componente de la gravedad paralela al plano ($\rho g h \sin\theta$) no supera $\mu_f \rho g h \cos\theta$, el flujo tenderá a frenar y detenerse, lo que es análogo a decir que $\tan\theta < \mu_f$ resulta en detención (criterio similar al de un bloque rozante en un plano inclinado). Este modelo por tanto no considera cohesión, asumiendo material sin cohesión (cohesión = 0 en términos de Mohr-Coulomb). Por otro lado, el término turbulento-inercial capta que a mayores velocidades, la agitación interna y los choques entre partículas ejercen una fuerza resistiva creciente (al igual que la resistencia del aire crece con $V^2$). En flujos de escombros rápidos, especialmente con alto contenido de bloques grandes y surcando cauces estrechos, se observa un comportamiento semejante: una vez que aceleran, la disipación adicional proviene más de la turbulencia y colisiones que de la viscosidad del fluido intersticial. El modelo Voellmy ha sido implementado en herramientas de simulación de avalanchas y flujos, como el software RAMMS (Rapid Mass Movement Simulation) para avalanchas de nieve y flujos de detritos, y en modelos de flujo bidimensionales de investigadores en Suiza, Canadá y otros países. Por ejemplo, Zimmermann et al. (2020) calibraron el modelo Voellmy–Salm en 19 flujos de ladera en los Alpes Suizos, hallando que el parámetro de fricción $\mu_f$ correlacionaba con el porcentaje de arcilla del material movilizado (más arcilla tendía a elevar ligeramente la fricción dinámica, posiblemente por mayor cohesión residual al detenerse). 

Voellmy–Salm es apropiado para flujos muy rápidos y dominados por componentes granulares. Típicamente se usa en escenarios de flujos en canales empinados o avalanchas de detritos donde el material se mueve a varios m/s y recorre largas distancias con comportamiento análogo a un flujo turbulento de alta densidad. En regiones de montaña con flujos de escombros canalizados (por ejemplo, en los Himalayas, Andes o Alpes), este modelo puede reproducir adecuadamente la rápida aceleración y luego desaceleración por rozamiento que se observa en eventos extremos. También se ha empleado en simulaciones de avalanchas de rocas o flujos de detritos generados por colapsos de presas naturales, donde la componente líquida es secundaria y el comportamiento se acerca más al de un flujo granular. Debe destacarse que $\mu_f$ y $\xi$ no se miden directamente en laboratorio sino que se calibran retrospectivamente: por ejemplo, a partir de la distancia de alcance y velocidad estimada del flujo, se eligen combinaciones de $\mu_f$ y $\xi$ que reproduzcan esos datos. Valores típicos para flujos de escombros líquidos suelen ser $\mu_f \sim 0.1–0.3$ y $\xi \sim 200–600 m/s^2$, mientras que para avalanchas de roca seca $\mu_f$ puede ser aún menor (~0.05–0.1) y $\xi$ mayor (>1000) debido a la menor resistencia basal y alta movilidad. 

Aunque eficaz para capturar la dinámica general de flujos rápidos, el modelo Voellmy–Salm es fenomenológico y tiene limitaciones. En primer lugar, al no incluir $\tau_y$ cohesivo, no modela bien el inicio de movimientos en materiales muy cohesivos o en flujos de baja velocidad: en tales casos, Voellmy predice que cualquier pendiente por encima de la fricción $\mu_f$ (p. ej. >10°) debería movilizarse, lo que no explica retardos por cohesión o umbrales de humedad necesarios para iniciar ciertos flujos tropicales. Por ello, algunas versiones extendidas incluyen un término cohesivo adicional (como un $\tau_y$ pequeño o un $\mu_f$ que disminuye con la velocidad). En segundo lugar, la naturaleza de $\xi$ es un “cajón de sastre” que engloba tanto turbulencia de fluido como dispersión granular; no distingue entre agua y sólidos ni sus interacciones de forma rigurosa. Esto significa que $\xi$ puede variar de un evento a otro sin correlación simple con parámetros físicos medibles (Zimmermann et al. encontraron que un parámetro extra de cohesión mejoraba las simulaciones pero no podía relacionarse directamente con propiedades del suelo o la saturación). Asimismo, el modelo asume condiciones de flujo permanente promedio, por lo que no captura transitorios como la fase de parada final donde la turbulencia decae y la mezcla se deposita (a menudo en la práctica, se impone que el flujo se detiene cuando $V$ cae a casi cero, pues Voellmy en teoría nunca da $\tau = 0$ a menos que $V=0$ exactamente). Pese a estas simplificaciones, la formulación Voellmy–Salm ha demostrado ser muy útil en ingeniería para estimar corridas y velocidades máximas de flujos de escombros en 2D, integrándose en códigos como RAMMS DF (de Suiza) o DAN3D (de Canadá) y permitiendo calibrar escenarios de riesgo con relativamente pocos parámetros. Su popularidad se debe a que capta bien la diferencia entre la fase inicial dominada por la gravedad (aceleración rápida limitada solo por fricción basal) y la fase avanzada dominada por la disipación turbulenta (donde la velocidad máxima se regula por el balance entre pendiente y resistencia cuadrática).

### Modelo PCM
El modelo PCM (*Perla-Chen-McClung*, Perla et al., 1980) es un modelo de fricción de dos parámetros basado en el modelo de Voellmy (1955). Fue desarrollado inicialmente para avalanchas de nieve, pero ha sido utilizado con éxito para simular la propagación de flujos de detritos por varios autores (Gamma, 2000; Horton et al., 2013; Rickenmann, 1990; Wichmann & Becht, 2004; Zimmermann et al., 1997).

El modelo, basado en el centro de masa, asume que el movimiento está controlado principalmente por un coeficiente de fricción por deslizamiento $\mu$, y una relación masa-resistencia aerodinámica $M/D$. El parámetro $\mu$ domina el comportamiento de la velocidad en la zona de alcance (*runout*).

La velocidad puede calcularse a lo largo de segmentos de pendiente más o menos homogéneos (Gamma, 2000), o  celda por celda en el camino del flujo (Horton et al., 2013; Wichmann, 2017). La velocidad $v_i$ en una celda se calcula según:

$$
v_i^2 = \alpha_i \left(\frac{M}{D}\right)_i \left(1 - e^{\beta_i}\right) + v_{i-1}^2 e^{\beta_i}
$$

donde los parámetros $\alpha_i$ y $\beta_i$ son:

$$
\alpha_i = g \left( \sin \theta_i - \mu_i \cos \theta_i \right)
$$

$$
\beta_i = -\frac{2 L_i}{(M/D)_i}
$$

y:  $v_i$: velocidad [m/s] en la celda actual,  $v_{i-1}$: velocidad en la celda anterior,  $g$: aceleración de la gravedad [m/s²],  $\theta_i$: pendiente local [°],   $L_i$: longitud de la pendiente en la celda $i$ [m],  $\mu_i$: coeficiente de fricción por deslizamiento [-],  $M/D$: relación masa-resistencia aerodinámica [m].

En transiciones cóncavas (cuando la pendiente disminuye), la velocidad previa $v_{i-1}$ se ajusta para conservar el momento lineal, según:

$$
v_i = v_{i-1} \cos \left( \theta_{i-1} - \theta_i \right) \quad \text{si} \quad \theta_{i-1} \geq \theta_i
$$

La distancia de alcance del flujo se calibra ajustando los dos parámetros de fricción.  Sin embargo, como diferentes combinaciones de $\mu$ y $M/D$ pueden producir la misma distancia de alcance en la práctica, se mantiene $M/D$ constante a lo largo del trayecto, calibrándolo una sola vez para alcanzar rangos realistas de velocidad máxima.
El coeficiente de fricción $\mu$ puede mantenerse constante o variar a lo largo del camino, por ejemplo, para representar diferentes condiciones reológicas debidas al contenido de agua.

### Modelo de Bagnold

El modelo de Bagnold (1954) con comportamiento dilatante (es decir, de espesamiento por cizalla, donde el fluido ofrece mayor resistencia a mayores esfuerzos cortantes aplicados) y diferencia tres tipos de flujos: el régimen macroviscoso, el régimen de transición y el régimen granular-inercial.

El régimen al que pertenece el flujo puede determinarse por el Número de Bagnold ($Ba$), el cual depende del diámetro del sedimento ($D$), la concentración volumétrica del sedimento ($C$), la máxima concentración de sedimento ($C_0$), la viscosidad dinámica del fluido ($\mu$) y la densidad de las partículas de sedimento ($\rho_s$).

* Número de Bagnold ($Ba$): Esta es la relación entre los esfuerzos inerciales y los viscosos.

$$Ba = \frac{\rho_s D^2 \lambda^{1/2} \dot{\gamma}}{\mu_f}$$

$\rho_s$ = densidad de las partículas sólidas

$D$ = diámetro de la partícula

$\lambda$ = concentración lineal

$\dot{\gamma}$ = tasa de cizalla (shear rate)

$\mu_f$ = viscosidad del fluido intersticial

Es importante notar que Bagnold usó la "concentración lineal" ($\lambda$), que es la relación entre el diámetro de la partícula ($D$) y la distancia media entre partículas. Se relaciona con la concentración volumétrica ($C$) así:

$$\lambda = \left[ \left( \frac{C_0}{C} \right)^{1/3} - 1 \right]^{-1}$$

Donde $C_0$ es la concentración máxima posible (aprox. 0.61-0.74).

De acuerdo con lo anterior, una ecuación describe el esfuerzo cortante como una función de la deformación del fluido para cada régimen, donde $a_v$ y $a_i$ son constantes experimentales y donde $\alpha_1$ es el ángulo de fricción dinámico (el cual es diferente del ángulo de fricción interna).

* Régimen Macroviscoso (Ba < 40): A bajas tasas de cizalla y/o bajas concentraciones. Las partículas están "lejos" y el fluido intersticial domina. El momento se transfiere a través de la viscosidad del fluido. El fluido actúa como un lubricante.
  
  El esfuerzo total ($\tau$) es dominado por el esfuerzo viscoso ($\tau_v$). La resistencia es linealmente proporcional a la tasa de cizalla (comportamiento Newtoniano o de Bingham).

$$\tau \approx \tau_v = a_v \cdot \mu_f \cdot (1 + \lambda) \cdot (1 + 0.5 \lambda) \cdot \dot{\gamma}$$

$a_v$ = constante empírica (Bagnold encontró $\approx 2.25$ para $\lambda > 5$)

$\mu_f$ = viscosidad del fluido

Forma Simplificada: $\tau_v \propto \mu_{mezcla} \cdot \dot{\gamma}$

* Régimen Granular-Inercial(Ba > 450): A altas tasas de cizalla y/o altas concentraciones. Las partículas están tan juntas que el fluido es "exprimido". El momento se transfiere a través de colisiones inerciales (choques) y fricción entre los granos. El flujo se "dilata" (expande) para poder moverse.

El esfuerzo total ($\tau$) es dominado por el esfuerzo inercial ($\tau_i$). La resistencia es proporcional al cuadrado de la tasa de cizalla (comportamiento dilatante o shear-thickening).

$$\tau \approx \tau_i = a_i \cdot \rho_s \cdot (\lambda D)^2 \cdot (\dot{\gamma})^2 \cdot \sin(\alpha_i)$$

$a_i$ = constante empírica (Bagnold encontró $\approx 0.042$)

$\alpha_i$ = ángulo de fricción dinámico (mencionado como $\alpha_1$ en tu texto, $\approx 30^\circ - 37^\circ$)

Forma Simplificada: $\tau_i \propto \rho_s D^2 \cdot (\dot{\gamma})^2$

El modelo de Bagnol tiene como suposiciones claves que el fluido entre los granos (agua) es simple (Newitoniano); no hay fuerzas electroquímicas (cohesión) entre las partículas. Esto lo hace inapropiado para flujos con alto contenido de arcilla; los granos son esféricos, rígidos, de tamaño uniforme (monodispersos) y flotabilidad neutra (en sus experimentos originales, $\rho_s = \rho_f$); el modelo describe un flujo en equilibrio, no su inicio o detención; y altas concentracione, el modelo se desarrolló para $C > 9\%$.

### Modelo cuadrático de O'Brien y Julien
El modelo reológico cuadrático de O’Brien et al. (1993) combina los cuatro componentes de esfuerzo de las mezclas de sedimentos no newtonianas: (1) cohesión entre partículas, (2) fricción interna entre el fluido y las partículas de sedimento, (3) turbulencia, y (4) impacto inercial entre partículas. El modelo cuadrático separa las relaciones de esfuerzo-deformación en estos cuatro componentes aditivos, de modo que el esfuerzo cortante es:

$$\tau_{MD} = \tau_c + \tau_v + \tau_t + \tau_d$$  

Donde: $\tau_{MD}$ = el esfuerzo cortante total de lodo y detritos (Pa), $\tau_c$ = esfuerzo de cedencia (Pa), $\tau_v$ = esfuerzo cortante viscoso (Pa), $\tau_t$ = esfuerzo cortante turbulento (Pa) (similar a la rugosidad de Manning en O’Brien et al., 1993), $\tau_d$ = esfuerzo cortante dispersivo (Pa).

En conjunto, la fórmula cuadrática busca modelar flujos de detritos en un amplio rango de concentraciones: a tasas de corte bajas prevalece $\tau_y$, a intermedias $\tau_v$, y a muy altas la componente $\tau_d$ domina (dando un comportamiento dilatante). FLO-2D, uno de los softwares comerciales pioneros para flujos de detritos, utiliza esencialmente esta ecuación cuadrática de O’Brien. Su ventaja es incorporar físicamente el efecto de choques entre partículas (importante en flujos rápidos con granos), pero al precio de introducir parámetros adicionales como $c_{Bd}$ (coeficiente empírico, típicamente 0.01), $\lambda$ (concentración lineal relacionada con la concentración por volumen) y $d_s$ (diámetro medio de partícula). Esto complica su calibración, aunque hay recomendaciones típicas (Bagnold y Takahashi sugirieron $c_{Bd}=0.01$). En contextos tropicales con flujos cargados de arena y grava, este modelo podría predecir una marcada subida de resistencia a medida que aumenta la concentración de sólidos (efecto dilatante), lo cual concuerda con observaciones de flujos que “se espesan” al incorporar escombros durante el recorrido.

O’Brien et al. (1993) formulan cada uno de estos componentes de esfuerzo para construir su modelo cuadrático, el cual se basa en la tasa de deformación ($dv_x/dz$):

$$ \tau_{MD} = \tau_c + \mu_m \left( \frac{dv_x}{dz} \right) + \rho_m l_m^2 \left( \frac{dv_x}{dz} \right)^2 + c_{Bgd} \rho_s \left( \left[ \frac{C_*}{C_v} \right]^{\frac{1}{3}} - 1 \right)^{-2} d_s^2 \left( \frac{dv_x}{dz} \right)^2 $$   

donde: $dv_x/dz$ = la tasa de corte (1/s), calculada como una función de la velocidad promediada en la profundidad y la profundidad del flujo, $\mu_m$ = viscosidad dinámica de la mezcla (Pa·s), $\rho_m$ = densidad de masa de la mezcla de sedimento (kg/m³), $l_m$ = longitud de mezcla (m), $c_{Bgd}$ = coeficiente empírico de impacto de Bagnold ($c_{Bgd} \cong 0.01$), $\rho_s$ = densidad de las partículas de sedimento (kg/m³), $C_*$ = concentración volumétrica máxima de sedimento, $C_v$ = concentración volumétrica de sedimento, $d_s$ = tamaño de grano del sedimento (m).

Takahashi (1980) identificó experimentalmente que el coeficiente de impacto de Bagnold ($c_{Bgd}$) varía entre 0.35 y 0.5, y que es significativamente mayor que el valor recomendado por Bagnold (1954 y 1956). Iverson (1997) propone aproximar la tasa de corte media ($dv_x/dz$) como $3\bar{u}/h$ para un perfil de velocidad parabólico, o como $2\bar{u}/h$ para un perfil lineal, donde $\bar{u}$ = velocidad promediada en la profundidad (m/s), $h$ = profundidad del flujo (m). 

La ecuación para la longitud de mezcla de Prandtl se define como: $l_m = kz$. donde: $k$ = el coeficiente de Von Kármán ($\cong 0.41$), $z$ = la distancia proporcional desde el contorno (lecho).

Este modelo cuadrático combina modos reológicos lineales y no lineales para calcular el esfuerzo cortante interno. El rendimiento de los modelos reológicos disminuye a medida que las mezclas se vuelven más clásticas (es decir, con altas concentraciones de partículas gruesas). 

La ecuación de O'Brien utiliza un modelo cuadrático para añadir los impactos no lineales de la colisión de partículas y la turbulencia a los términos lineales de cedencia y viscosidad del modelo de Bingham. No es tan flexible como la de Herschel-Bulkley. Los efectos no lineales son siempre una función del cuadrado de la deformación, por lo que siempre son efectos de espesamiento por cizalla (shear-thickening) fuertes. Sin embargo, el modelo de O'Brien es más fácil de parametrizar que el de Herschel-Bulkley. La ecuación de O'Brien utiliza valores físicos para desarrollar efectos cuadráticos teóricos. La desventaja de este enfoque es que si la formulación teórica no refleja los procesos del flujo geofísico, introducirá errores. Pero el beneficio de este enfoque físico-teórico es que todos los parámetros de entrada en los términos no lineales son parámetros físicos que son o bien predeterminados o relativamente intuitivos de especificar para el usuario.

Además del esfuerzo de cedencia, Gibson et al. (2020) demostraron que valores más bajos de cedencia y viscosidad son a menudo apropiados para el enfoque de O'Brien en comparación con el de Bingham, porque la ecuación de O'Brien está considerando explícitamente procesos en el término cuadrático que Bingham está agrupando (lumping) en los parámetros lineales. Y además de la viscosidad del flujo cargado de sedimento que se requiere para el modelo de Bingham, el modelo de O'Brien solo requiere la concentración volumétrica (que ya es necesaria para el aumento de volumen o bulking y para algunas estimaciones de cedencia y viscosidad) y un tamaño de grano representativo. HEC-RAS también ha expuesto el valor predeterminado de la concentración volumétrica máxima en el término de Bagnold de O'Brien (0.615 o 61.5%). Este término es aceptable para flujos de menor concentración (Cv<50%). Pero a medida que la concentración se acerca o supera este máximo teórico, los usuarios deberían aumentarlo para que sea mayor que la concentración volumétrica.

:::{figure-md} quadratic O'Brien model
<img src="https://i.pinimg.com/736x/13/ab/a5/13aba5b9705dff738d2f30616141f667.jpg" width="700px">

Implementación del modelo cuadrático de O'Brien en HEC-RAS. Tomado de [HEC RAS Non-Newtonian User's Manual](https://www.hec.usace.army.mil/confluence/rasdocs/rasmuddebris/non-newtonian-user-s-manual/introduction-taxonomy-and-rheology-of-debris-flows).
:::

### Modelo de fricción de Coulomb
Es el caso límite en que la resistencia se considera totalmente dominada por la fricción interna del material, con un criterio de falla tipo Mohr-Coulomb (esfuerzo cortante máximo = $\tau_ = \tau_c + \sigma \tan\phi$). En flujo continuo, esto equivale esencialmente a $\tau = \mu ,\sigma_n + c$ (con $c$ cohesión, a menudo cero) constante durante el movimiento. Este modelo no tiene término viscoso ni dependiente de tasa de deformación. Es adecuado solo para flujos casi secos o grandes avalanchas de rocas donde el material se comporta más como un deslave granular que como un fluido. En contextos de escombros saturados, el modelo de Coulomb puro suele ser insuficiente, aunque a veces se incluye como componente basal en modelos más completos. Por ejemplo, el “modelo Coulomb-viscoso” mencionado en literatura combina una fricción Coulomb basal con un término viscoso lineal para tener tanto cohesión (c) como fricción $\tan\phi$.

HEC-RAS simula los flujos de detritos clásticos con una aproximación de Coulomb basada en el modelo viscoso de Coulomb de Johnson y Rodine (1984) (Naef et al., 2006). Este enfoque reemplaza el esfuerzo de cedencia de Bingham ($\tau_c$) por un esfuerzo de cedencia de Coulomb de tipo geotécnico, definido como:

$$\tau_{yc} = \rho_m g h \cos\alpha \tan\phi $$  

donde: $\tau_{yc}$ = Esfuerzo de cedencia de Coulomb (Pa), $\alpha$ = ángulo de la pendiente del lecho (°), $\phi$ = ángulo de fricción de Coulomb (°), que típicamente varía entre 30° y 40° (Iverson, 1997; McArdell et al., 2007). El ángulo de fricción de Coulomb es una función del ángulo de fricción de los granos individuales y de la geometría de empaquetamiento de las partículas a lo largo del plano de falla.

## Comparación, Supuestos y Limitaciones de los Modelos
A continuación se comparan los modelos presentados, enfatizando sus supuestos fundamentales y los escenarios donde mejor se ajustan, así como sus limitaciones inherentes:

**Naturaleza de la resistencia**: Bingham y Herschel–Bulkley tratan la resistencia del flujo como una combinación de cohesión estática (*yield*) + fricción viscosa dependiente de la velocidad de deformación. Voellmy–Salm, por otro lado, lo concibe como fricción basal + término inercial cuadrático (dependiente de la velocidad de flujo). El modelo cuadrático de O’Brien combina ambas filosofías al incluir término viscoso lineal + término cuadrático. En términos simples, Bingham/HB son más centrados en la fase fluida/cohesiva, mientras Voellmy y Coulomb se centran en la fase sólida/friccional; los modelos híbridos (HB con $n<1$, O’Brien) buscan mediar entre ambos extremos.

**Umbral de fluencia vs. fricción continua**: Bingham y HB incorporan explícitamente un umbral de fluencia $\tau_y$ que debe vencerse para que haya flujo. Esto refleja bien la necesidad de cierta energía (p.ej. lluvia intensa que eleve presión de poros) para arrancar un flujo de escombros cohesivo. Voellmy–Salm carece de un verdadero $\tau_y$ cohesivo; el único umbral es gravitacional: si la pendiente local supera la fricción $\mu_f$, el material podría empezar a moverse (asumiendo saturación). Por tanto, para flujos cohesivos (p.ej. escombros tropicales arcillosos), Bingham/HB capturan la etapa de no flujo a pendientes moderadas hasta que se excede $\tau_y$, mientras Voellmy podría sobreestimar la movilidad incial (prediciendo flujo demasiado pronto). Algunos códigos combinan ambos: por ejemplo, RAMMS permite agregar un término cohesivo al modelo Voellmy para representar la resistencia en flujos lentos de ladera.

**Dependencia de la velocidad (régimen laminar vs turbulento)**: Los modelos de Bingham y HB suponen implícitamente un régimen laminar o cuasi-laminar, donde la tensión cortante se relaciona con la velocidad de deformación local. No incluyen términos cuadráticos en la velocidad absoluta del flujo, por lo que por sí solos no pueden representar la resistencia adicional que aparece con la turbulencia o con el transporte de grandes bloques a gran velocidad. En contraste, Voellmy–Salm y O’Brien sí incluyen un término cuadrático (ya sea $\propto V^2$ o $\propto \dot\gamma^2$, que en flujo rápido se relacionan) que representa esa resistencia inercial. Por ello, para flujos muy rápidos en cauces empinados (Re alto, Froude alto), un modelo puramente Bingham podría subestimar la disipación – típicamente en esos casos se han observado largos runouts que solo se explican introduciendo fricción turbulenta variable con $V$. Por otro lado, en flujos lentos (Re bajo) el término cuadrático es despreciable y modelos como Voellmy colapsan en un término constante (lo cual no refleja el aumento gradual de viscosidad a bajas velocidades, e.g. por tixotropía). En suma, flujos lentos cohesivos: Bingham/HB son preferibles; flujos rápidos no cohesivos: Voellmy es preferible; flujos intermedios: modelos combinados o calibración cuidadosa.

**Calibración y parámetros**: Los modelos presentados requieren distintos insumos paramétricos. Bingham: $\tau_y$ y $\mu_p$ medibles con reometría de lodos; Herschel–Bulkley: $\tau_y$, $K$, $n$ (difíciles de estimar sin datos detallados); Voellmy: $\mu_f$ y $\xi$ (se calibran con casos observados, no medibles directamente); O’Brien: $\tau_y$, $\mu$, más parámetros granulares ($c_{Bd}$, etc.) parcialmente empíricos. Así, los modelos viscoplásticos suelen vincularse más a propiedades intrínsecas del material (contenido de finos, humedad determinan $\tau_y$), mientras los inerciales requieren calibración macroscópica (por ejemplo, usando registros de huellas de flujo para ajustar $\mu_f$). Cabe destacar que, en cualquier caso, los modelos reológicos efectivos suelen involucrar coeficientes de ajuste. Garcés et al. (2022) recalcan la importancia de identificar los parámetros más sensibles y reconocer que múltiples combinaciones de parámetros pueden reproducir observaciones, lo que exige criterio experto para evitar calibraciones no físicas.

**Interacción con procesos de campo**: Una limitación común de los modelos reológicos simples es que no contemplan cambios en la mezcla debidos a erosión o deposición durante el recorrido. En ambientes montañosos y tropicales, los flujos de escombros a menudo erosionan material del lecho (aumentando su carga de sólidos) o se diluyen con afluentes de agua a lo largo de la trayectoria. Esto altera la reología instantáneamente (un flujo que gana sedimento puede pasar de Newtoniano a Bingham espeso en minutos). Los modelos presentados asumen generalmente propiedades homogéneas constantes; para mayor realismo, algunos modelos numéricos acoplan ecuaciones de *entrainment* (erosión) y recalculan parámetros reológicos localmente. No obstante, esa es una frontera activa de investigación, ya que incorporar la retroalimentación entre erosión y reología sigue siendo complejo.

**Validez de la aproximación continua**: Todos los modelos mencionados tratan al flujo de escombros como un continuo. Esto es razonable cuando la mezcla es muy heterogénea pero persistentemente mezclada (caso típico de flujos con matriz fluida abundante). Sin embargo, para avalanchas de rocas o flujos de detritos con gran proporción de bloques enormes, el supuesto de continuo puede fallar a escala local (bloques rodando individualmente). En tales casos, modelos discretos (DEM) o bifásicos pueden ser más apropiados.

Tabla Lista de modelos numéricos seleccionados para el cálculo del alcance de deslizamientos (adaptado de Kang y Chan (2018)).

| Modelo          | Reología                                                  | Incorpora arrastre | Referencias seleccionadas                                                 |
|-----------------|------------------------------------------------------------|--------------------|--------------------------------------------------------------------------|
| 3dDMM           | Friccional y Voellmy                                       | Sí                 | Kwan y Sun (2007)                                                       |
| DAN2D           | Friccional, Voellmy y Bingham                             | Sí                 | Hungr (1995)                                                            |
| DAN3D           | Friccional, Voellmy y Bingham                             | Sí                 | McDougall (2006)                                                        |
| FLATModel       | Friccional y Voellmy                                       | Sí                 | Medina et al. (2008)                                                    |
| FLO-2D          | Cuadrática                                                 | No                 | O’Brien (2006)                                                          |
| Flow-R          | Voellmy                                                    | No                 | Horton et al. (2013)                                                    |
| GeoFlow-SPH     | Friccional, Voellmy y Bingham                             | Sí                 | Pastor et al. (2009)                                                    |
| D-Claw          | Friccional                                                 | Sí                 | Iverson y George (2014); Iverson (2012)                                 |
| MADFLOW         | Friccional, Voellmy y Bingham                             | Sí                 | Chen y Lee (2000)                                                       |
| MassMov2D       | Voellmy y Bingham                                          | Sí                 | Begueria et al. (2009)                                                  |
| PFC             | Interacción entre partículas e interacción partícula-pared | Sí                 | Kang y Chan (2018b)                                                     |
| RAMMS           | Voellmy                                                    | No                 | Christen et al. (2010)                                                  |
| RASH3D          | Friccional, Voellmy y Cuadrática                          | Sí                 | Pirulli (2005)                                                          |
| r.avalanche     | Friccional                                                 | Sí                 | Mergili et al. (2012)                                                   |
| r.avaflow       | Friccional (sólido) y no newtoniano (fluido)               | Sí                 | Mergili et al. (2017)                                                   |
| Sassa-Wang      | Friccional                                                 | Sí                 | Wang y Sassa (2002)                                                     |
| SCIDDICA S3-hex | Basado en energía                                          | No                 | D’Ambrosio et al. (2003)                                                |
| SHALTOP-2D      | Friccional                                                 | No                 | Mangeney-Castelnau et al. (2003)                                        |
| TITAN2D         | Friccional                                                 | No                 | Pitman et al. (2003)                                                    |
| TOCHNOG         | Friccional (modelo elastoplástico)                        | Sí                 | Roddeman (2002)                                                         |
| TopFlowDF       | Friccional, Voellmy y Cuadrática                          | No                 | Scheidl y Rickenmann (2011); Han et al. (2016)                          |
| VolcFlow        | Friccional y Voellmy                                       | Sí                 | Kelfoun y Druitt (2005)                                                 |
| Wang            | Friccional                                                 | No                 | Wang et al. (2010); Kang y Chan (2018b)                                |
| Massflow        | Friccional                                                 | Sí                 | Ouyang et al. (2015)                                                    |


