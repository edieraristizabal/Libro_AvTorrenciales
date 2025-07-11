# Ecuaciones de Saint-Venant

Tomado de Iverson and George (2024)

Para modelar flujos de escombros (*debris flows*) y otros flujos, se emplean un conjunto de ecuaciones de conservación que derivan de la mecánica de fluidos y medios continuos. Las ecuaciones de Saint-Venant son una forma simplificada y promediada en profundidad de las ecuaciones de Navier–Stokes. Se utilizan para modelar flujos superficiales como ríos, avalanchas, lahares y *debris flows*. Estas ecuaciones resuelven la dinámica del flujo considerando solo las variaciones en el plano horizontal (x,y), y promediando las variables a lo largo de la vertical (z), lo que simplifica mucho el problema sin perder lo esencial.

Las ecuaciones de flujo de aguas someras (o de aguas poco profundas) resuelven simultáneamente las ecuaciones de continuidad y de momento para calcular la cota del agua y la velocidad. Las fuerzas de fricción entre el fluido y el contorno sólido son las principales fuerzas de resistencia en las ecuaciones hidráulicas estándar para agua clara newtoniana. Comparado con aguas limpias, los flujos de lodo y detritos generan fuerzas resistentes adicionales. El aumento del contenido de sólidos incrementa la viscosidad de los flujos no newtonianos, generando fuerzas resistentes internas dentro del fluido. A concentraciones más altas, particularmente con partículas gruesas, la colisión y fricción entre partículas introducen fuerzas resistentes internas adicionales. La mayoría de las modificaciones teóricas y numéricas implican la integración de las nuevas fuerzas internas del fluido en la ecuación de momento. 

La aplicación del transporte no newtoniano en un modelo de aguas someras (o de aguas poco profundas) requiere calcular las pérdidas internas añadiendo un término de pendiente a la pendiente de fricción ($S_f$) en la ecuación de momento y aumentando el flujo para tener en cuenta el volumen de los sólidos. La pendiente de fricción ($S_f$) del modelo de aguas someras representa las fuerzas que actúan contra el flujo en el contorno del fluido (por ejemplo, el canal), mientras que la pendiente de lodo y detritos ($S_{MD}$) representa las pérdidas internas debidas a la viscosidad, la turbulencia y/o la dispersión dentro del fluido.

Los términos utilizados en las ecuaciones de conservación de masa y momento de Saint-Venant para modelar flujos de escombros se traducen al español de la siguiente manera:

| **Término en inglés**               | **Símbolo**   | **Traducción al español**                            |
|--------------------------------------|---------------|------------------------------------------------------|
| Newtonian friction slope             | $𝑆_𝑓$         | Pendiente de fricción newtoniana                     |
| Mud and debris friction slope        | $𝑆_𝑀$       | Pendiente de fricción para lodos y escombros         |


- **Pendiente de fricción newtoniana:** Representa la resistencia al flujo generada por la fricción basal y la viscosidad interna en materiales con comportamiento newtoniano, como el agua o fluidos con viscosidad constante. En hidráulica clásica, es análoga a la pendiente de energía perdida por fricción (e.g., fórmulas de Manning o Chezy).

- **Pendiente de fricción para lodos y escombros:** Representa la resistencia basal y interna característica de flujos no newtonianos, como mezclas de lodo y escombros, que pueden mostrar comportamiento viscoplástico (por ejemplo, tipo Bingham) o hiperconcentrado.

Generalmente los modelos entonces calculan un esfuerzo cortante no newtoniano basándose en la clasificación del flujo (p. ej., flujo de lodo, flujo de detritos, etc.) y el enfoque reológico apropiado (es decir, el modelo de esfuerzo-deformación). Luego, la librería integra el cortante viscoso, turbulento y de dispersión del modelo de esfuerzo-deformación en la ecuación de momento, convirtiendo el esfuerzo cortante en una pendiente y sumando esta pendiente a la pendiente de fricción ($S_f$). Adicionalmente, debido a que estos flujos pueden contener entre un 5% y un 70% de sólidos por volumen, un modelo de lecho fijo debe aumentar el volumen del flujo para tener en cuenta el impacto del sedimento en la masa y la profundidad del flujo.

En este sentido, los modelos numéricos para flujos de ladera suelen usar las ecuaciones de Saint-Venant adaptadas a flujos no newtonianos, en forma de conservación de masa y momento en 1D o 2D de la siguiente forma:

#### Ecuación de conservación de masa (Continuidad)
Para un flujo en una dirección horizontal (e.g. coordenada $x$), la ecuación de continuidad superficial en régimen no permanente en 1D es:

$$\frac{\partial A}{\partial t} + \frac{\partial(Q)}{\partial x} = 𝑆_m$$
 
Donde: $Q$ es el caudal [$m_3/s$] el cual se obtiene a partir de $h(x,t)$: espesor del flujo [m], $\vec{u}(x,t)$: velocidad media del flujo [m/s] y $A$ el área de la seccion transversal del canal [$m_2$]. $S_m$ es la fuente o pérdida de masa (por ejemplo, aporte de afluentes, erosión, infiltración) [m/s]. Esta ecuación dice que el cambio del espesor en el tiempo es igual a la diferencia entre lo que entra y lo que sale, más lo que se gana o pierde localmente.

#### Ecuación de conservación de cantidad de movimiento (momento lineal)
Esta ecuación representa el balance entre fuerzas propulsoras (gravedad) y resistencias (fricción basal, turbulencia, etc.). En 1D la ecuación de conservación de momento es:

$$\frac{\partial(Q)}{\partial t} + \frac{\partial(Q\vec{u})}{\partial x} = 𝑔 hsen⁡\theta − S_{MD} + 𝑆_f$$

$$S_{MD}=\frac{\tau_{MD}}{\rho_mgR}$$
​ 
Donde: $g$: gravedad, $\theta$: pendiente del terreno, $S_{MD}$: pendiente de fricción para lodos y escombros, $S_f$: pendiente de fricción newtoniana o pendiente de fricción viscosa, $\tau_{MD}$ el esfuerzo cortante interno y reológico, $\rho_m$ la densidad dela mezcla de sedimentos y agua ($kg/m^3$) y $R$ el radio hidráulico (m). 

La pendiente de fricción para lodos y escombros ($S_{MD}$) se refiere a la resistencia al movimiento introducida por la fricción interna y basal de materiales no newtonianos, como mezclas de lodo, escombros o flujos hiperconcentrados, que pueden tener comportamientos viscoplásticos o de tipo Bingham. 

La pendiente de fricción newtoniana $S_f$ se refiere a la componente del modelo que representa las fuerzas de fricción o resistencia debidas a un comportamiento fluido tipo Newtoniano (como el agua o fluidos con viscosidad constante). 

Generalmente los modelos son simplificados (usan solo la ecuación de momento), tales como algunos modelos empíricos o semi-analíticos, algunos modelos usados para estimar alcance máximo o zona de detención (por ejemplo, el método de "box model" o modelos de trayectoria pura). Usan solo Fuerza neta = masa⋅aceleración. Se considera una masa movilizada fija, y se analiza cómo frena con diferentes mecanismos (fricción basal, turbulencia). A veces se reduce a un problema 1D con:

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

## Técnicas numéricas de solución

El núcleo matemático de casi todos los modelos prácticos de flujo de escombros basados en física consiste en ecuaciones diferenciales parciales que representan leyes de conservación de masa y momento, promediadas en profundidad, de la mecánica del continuo para flujos que son poco profundos (por ejemplo, Iverson & George, 2014). 
Lo mismo ocurre con la mayoría de los modelos basados en física de deslizamientos de alta velocidad que no califican como flujos de escombros (por ejemplo, McDougall, 2017). 
Sin embargo, una fuente potencial de confusión es que categorizamos los modelos promediados en profundidad para el movimiento a través de un terreno tridimensional como modelos 2-D, mientras que McDougall (2017) los categorizó como modelos 3-D. 
El término "3-D" se refiere a modelos que no utilizan el promedio en profundidad.

Mientras que los modelos 3-D calculan flujos de momento en evolución en tres direcciones coordenadas, la mayoría de los modelos promediados en profundidad asumen que los flujos de momento normales al lecho pueden ser despreciados, lo que implica que las tensiones normales basales equilibran el peso estático del material suprayacente. 
Iverson (2005) proporcionó una evaluación cuantitativa de esta suposición y de las formas en que puede relajarse. 
Aunque la suposición de una tensión basal normal estática podría parecer muy restrictiva, la experiencia con modelos promediados en profundidad de diversos fenómenos, que van desde tsunamis e inundaciones hasta avalanchas granulares, ha mostrado que estos modelos comúnmente producen predicciones prácticas adecuadas incluso para flujos en los que la suposición se viola local o transitoriamente (por ejemplo, George, 2010; Gray et al., 2003; LeVeque et al., 2011).

Los modelos de flujo de escombros promediados en profundidad también asumen generalmente que las variaciones dependientes de la profundidad en el momento aguas abajo son despreciables.
Como en los modelos de flujo de agua poco profunda, se pueden hacer correcciones para los efectos de estas variaciones introduciendo coeficientes de distribución del momento (por ejemplo, Vreugdenhil, 1994). Sin embargo, los valores de los coeficientes de distribución dependen de la forma de los perfiles de velocidad y densidad del flujo, que están poco restringidos para los flujos de escombros. 
Como consecuencia, la mayoría de los modelos de flujo de escombros promediados en profundidad excluyen los coeficientes por considerarlos una complicación injustificada. 
En su lugar, asumen que el momento del flujo de escombros aguas abajo puede aproximarse como uniforme a todas las profundidades.

Las ecuaciones de conservación promediadas en profundidad se derivan integrando las ecuaciones de conservación 3-D a través del espesor del flujo de escombros en la dirección coordenada que denotamos como z (Iverson, 2005). 
Sin embargo, la dirección de z no es la misma en todos los modelos. 
Las coordenadas curvilíneas adaptadas al terreno, con z rotado de modo que sea normal al lecho en todas partes, son las más rigurosas desde el punto de vista matemático y facilitan la consideración del efecto de las aceleraciones centrípetas sobre las tensiones basales (Gray et al., 1999; Pudasaini et al., 2005; Savage & Hutter, 1991). 
Sin embargo, las coordenadas curvilíneas pueden ser difíciles de emplear en simulaciones numéricas de flujo sobre terrenos tridimensionales accidentados, en parte porque las celdas computacionales adyacentes pueden tener diferencias bruscas en las direcciones z normales al lecho, lo que podría generar definiciones conflictivas de las profundidades del flujo.
Además, si la geometría del lecho cambia significativamente debido a erosión o deposición, las coordenadas curvilíneas adaptadas al terreno original pierden al menos parte de su relevancia. 
El uso de coordenadas cartesianas centradas en la Tierra, con z vertical de manera uniforme, es más simple, pero requiere cuidado en el cálculo de flujos de momento y tensiones basales, porque la orientación de los lechos inclinados no es normal a una coordenada z vertical (Denlinger & Iverson, 2004; Iverson, 2005; Iverson & George, 2019a).

En todos los modelos de flujo de escombros promediados en profundidad, las cantidades fundamentales conservadas (masa y momento lineal) se expresan por unidad de área en las ecuaciones de conservación, lo que ayuda al desarrollo de técnicas numéricas de solución eficientes, en parte porque las condiciones de frontera de la superficie libre y del lecho están integradas en las ecuaciones durante el procedimiento de integración en profundidad (Iverson, 2005; Iverson & Ouyang, 2015). 
Esta característica elimina la necesidad de resolver por separado las posiciones cambiantes de las fronteras a medida que avanzan las soluciones computacionales. 
Sin embargo, durante la integración en profundidad puede ser un desafío incorporar correctamente los efectos de una frontera basal donde ocurren erosión o deposición, ya que están involucrados flujos de masa y momento a través de una superficie irregular y en evolución. 
El problema puede abordarse rigurosamente adoptando una perspectiva de dos capas, en la cual el flujo de escombros constituye la capa superior y el lecho constituye la capa inferior, y luego imponiendo la conservación de masa y momento en cada capa así como en el sistema de dos capas en su conjunto (Iverson & Ouyang, 2015). 

El núcleo matemático de los modelos de flujo de escombros basados en física y promediados en profundidad es un sistema de ecuaciones diferenciales parciales (EDP) hiperbólicas no lineales. 
Esta clase de EDP, que surge en diversos problemas que involucran propagación de ondas, presenta desafíos únicos para obtener soluciones numéricas precisas, en parte porque las ecuaciones pueden tener soluciones no únicas y discontinuas. 
Las soluciones discontinuas se aplican (aunque no se limitan) a las ondas de choque, un término tomado de la dinámica de gases pero que también se usa para describir características análogas como los saltos hidráulicos en los flujos de escombros. 
Los métodos numéricos estándar, como los métodos clásicos de diferencias finitas, son poco adecuados para estos problemas porque pueden producir soluciones físicamente espurias, dispersión numérica o inestabilidades numéricas. 
Estas deficiencias han motivado el desarrollo de clases especializadas de técnicas numéricas de solución, incluyendo los métodos de volúmenes finitos con captura de choques proporcionados por el proyecto de software de código abierto *Clawpack* (LeVeque, 2002, www.clawpack.org).

Los métodos numéricos implementados en *Clawpack* utilizan sistemas de coordenadas fijas (eulerianas) y soluciones analíticas de propagación de ondas a problemas de *Riemann*, un término que describe problemas matemáticos que involucran saltos discontinuos en los valores de las variables en las interfaces de las celdas de la malla computacional. 
Originalmente desarrollado para resolver problemas de ondas de choque (Godunov, 1959), el método de propagación de ondas de *Riemann* también proporciona un medio lógico para representar con precisión los saltos discontinuos en los datos de elevación que pueden existir al modelar flujos sobre topografía representada por MDE (George, 2008, 2010). 
La representación de saltos discontinuos es particularmente relevante para resolver frentes de flujo de escombros que avanzan sobre terrenos escarpados o impactan contra estructuras verticales.

Existen desafíos numéricos adicionales porque muchos problemas hiperbólicos, incluidos aquellos que surgen en la modelación promediada en profundidad de flujos de escombros, presentan un amplio espectro de escalas espaciales que varían en el tiempo, ubicación y extensión. 
Esta amplitud de escalas motivó el desarrollo de una estrategia computacional conocida como refinamiento de malla adaptativo (AMR, por sus siglas en inglés) (Berger y Oliger, 1984), que utiliza parches evolutivos de mallas computacionales anidadas con tamaños de celda variables basados en características dinámicas de la solución numérica. 
Existen diversas implementaciones de AMR, pero el objetivo de todas las técnicas AMR es proporcionar resoluciones de malla óptimas para lograr precisión numérica y eficiencia computacional durante toda la simulación.

Las técnicas estándar de AMR desarrolladas para ecuaciones generales de conservación hiperbólica no son adecuadas para modelar flujos poco profundos promediados en profundidad que se mueven sobre topografía variable, porque estas técnicas no pueden preservar simultáneamente estados estacionarios balanceados (como estados estáticos) y conservar masa, momento y energía. 
Se desarrollaron técnicas AMR especializadas para superar este problema en el contexto de la modelación de tsunamis (George & LeVeque, 2006; LeVeque et al., 2011). 
Posteriormente, estas técnicas se extendieron a la modelación de flujos promediados en profundidad sobre topografía, como inundaciones superficiales (Berger et al., 2011; George, 2010) y flujos de escombros (George & Iverson, 2014).

El uso de los algoritmos AMR especializados que preservan los estados balanceados también permite que D-Claw utilice mallas de alta resolución que evolucionan dinámicamente para resolver frentes de flujo que avanzan a través de terrenos complejos, mientras mantiene mallas gruesas donde no ocurre evolución de las variables (por ejemplo, en aquellas partes del dominio computacional donde no hay flujo). 
Este enfoque hace posible el uso de datos MDE modernos con resolución submétrica solo donde se necesita dentro de un dominio grande. 
Al hacerlo, el uso de AMR en D-Claw afecta drásticamente los resultados de la simulación en aquellos lugares donde existen características topográficas importantes pero de pequeña escala en ubicaciones aisladas (por ejemplo, presas, diques, edificios, etc.), que requieren resoluciones de malla finas que serían prohibitivas computacionalmente si se aplicaran a todo el dominio.

*r.avaflow* (Mergili et al., 2017) resuelve las ecuaciones de flujo de escombros bifásicas promediadas en profundidad de Pudasaini (2012). Al igual que D-Claw, *r.avaflow* emplea métodos numéricos eulerianos desarrollados específicamente para sistemas hiperbólicos de ecuaciones diferenciales. Sin embargo, utiliza esquemas numéricos de solución de diferencias centrales no oscilatorias con disminución de la variación total (*TVD-NOC*, por sus siglas en inglés) (Nessyahu & Tadmor, 1990), que se han aplicado con éxito a problemas de flujos de masa en general (véase Mergili et al., 2017, para ejemplos).

A diferencia de D-Claw, *r.avaflow* resuelve las ecuaciones en coordenadas locales adaptadas al terreno. Este enfoque confiere algunas ventajas en términos de fidelidad física, pero puede presentar desafíos prácticos para modelar flujos sobre topografías complejas del mundo real. Por ejemplo, las variables expresadas en coordenadas locales adaptadas al terreno y los MDE expresados en sistemas de coordenadas cartesianas uniformes espacialmente no siempre son compatibles. En general, es necesaria una transformación de las variables calculadas en coordenadas adaptadas al terreno a coordenadas cartesianas uniformes de MDE, y dicha transformación debe ser aproximada (Mergili et al., 2017).

Otro enfoque para abordar la dificultad de modelar con precisión flujos poco profundos sobre topografía accidentada está implementado en el modelo *SHALTOP* (Bouchut et al., 2003; Lucas et al., 2007), que resuelve las ecuaciones del modelo en coordenadas cartesianas globales pero corrige las ecuaciones para satisfacer el supuesto de flujo poco profundo aplicado en la dirección normal al lecho local. Este enfoque puede capturar aceleraciones normales al lecho debidas a la curvatura del terreno (Peruzzetto et al., 2021), pero aún requiere que las variables normales al lecho se transformen a un sistema de referencia cartesiano representado por un MDE estándar. Al igual que D-Claw, *SHALTOP* utiliza esquemas numéricos de volúmenes finitos bien balanceados para resolver sistemas hiperbólicos de ecuaciones diferenciales (Bouchut, 2004).

Otros modelos eulerianos de flujo de escombros incluyen *TITAN2D* (Pitman et al., 2003), que resuelve ecuaciones monofásicas promediadas en profundidad, y *RAMMS* (Christen et al., 2010), que fue desarrollado originalmente para modelar avalanchas de nieve pero utiliza una fórmula de resistencia al flujo tipo Voellmy monofásica para modelar flujos de escombros. Estos modelos emplean esquemas de solución por volúmenes finitos, en términos generales similares a los utilizados en D-Claw.

Un método más distintivo para resolver el sistema hiperbólico de EDP en modelos promediados en profundidad de flujos de escombros es el método lagrangiano sin malla conocido como hidrodinámica de partículas suavizadas (SPH, por sus siglas en inglés) (McDougall & Hungr, 2004). 
A diferencia de los métodos eulerianos, los métodos lagrangianos formulan las EDP del modelo en un marco de referencia móvil que se traslada con el flujo. 
En las aplicaciones de SPH a flujos de escombros, la representación mecánica continua del material del flujo de escombros se reemplaza efectivamente por un conjunto de “partículas” columnares que interactúan y que abarcan el espesor del flujo a medida que se mueven aguas abajo (McDougall & Hungr, 2004). 
Además, SPH elimina los efectos de las discontinuidades en las soluciones de las EDP que gobiernan mediante el uso de una fórmula de suavizado para promediar la mecánica de interacción entre partículas vecinas.


