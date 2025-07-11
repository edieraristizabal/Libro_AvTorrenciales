# Interacción atmosfera-ladera-cauce

Tomado de *Kaitna et al. (2024)* Causes and triggers en Advances in Debris-flow science and practice. Eds. Matias Jakob, Scott McDougall, Paul Santi.

La lluvia convectiva ocurre cuando hay abundante humedad disponible en la atmósfera y la inestabilidad flotante de las masas de aire genera fuertes movimientos verticales. En los movimientos ascendentes, la humedad se condensa formando grandes gotas, que finalmente caen al suelo con intensidades de lluvia intensa. Este sistema básico de movimientos ascendentes y descendentes se denomina célula convectiva.

Las células convectivas se forman en ambientes favorables, crecen hasta alcanzar las tasas de lluvia más intensas y luego se disipan, en ciclos de vida que duran alrededor de 30 a 60 minutos. Pueden extenderse verticalmente hasta la tropopausa y sus escalas horizontales son del orden de unos pocos kilómetros cuadrados. 

Las tormentas convectivas pueden estar compuestas por numerosas células convectivas, por lo que pueden durar mucho más que una célula individual y cubrir áreas relativamente grandes.  Por ejemplo, los frentes fríos típicamente asociados con el paso de sistemas de baja presión presentan numerosas células convectivas y cubren regiones extensas durante varias horas. No obstante, también pueden formarse células convectivas aisladas, especialmente en áreas montañosas donde los movimientos verticales del aire se ven reforzados por el ascenso orográfico de las masas de aire y por efectos locales de calentamiento, como ocurre con las tormentas aisladas de verano en los Alpes (Barry & Chorley, 2010).

La orografía restringe físicamente el movimiento de las masas de aire, induciendo movimientos verticales y turbulencia, y afecta los procesos de precipitación (Bonacina, 1945; Roe, 2005). En general, estos movimientos verticales generan un aumento en la precipitación sobre las laderas de barlovento y una disminución sobre las laderas de sotavento. Cada ladera experimenta ambos efectos dependiendo de la dirección del viento durante las tormentas, aunque generalmente predomina el aumento. De hecho, se observan mayores cantidades de precipitación en altitudes elevadas, fenómeno conocido como realce orográfico de la precipitación.

De manera inesperada, las precipitaciones convectivas intensas no obedecen a esta regla general. La intensidad de la lluvia intensa y de corta duración, crucial para la generación de flujos de escombros, ha resultado ser menor a mayores altitudes. Este fenómeno, conocido como efecto orográfico inverso, se ha observado en varias cadenas montañosas, incluyendo los Alpes, los Apeninos italianos y las montañas de Judea en el sureste del Mediterráneo (Allamano et al., 2009; Avanzi et al., 2015; Marra et al., 2021; Mazzoglio et al., 2022). La orografía induce turbulencia en las masas de aire, lo que dificulta los movimientos verticales y redistribuye la humedad dentro de las células convectivas. Como resultado, el rendimiento total de precipitación durante la vida de las células se mantiene aproximadamente igual, pero las tasas máximas de lluvia que pueden generar las células convectivas suelen ser más bajas (Formetta et al., 2022; Marra et al., 2021, 2022).

Existen evidencias emergentes a nivel global del aumento de la precipitación convectiva debido al cambio climático (Fowler et al., 2021), lo que genera preocupación en regiones montañosas como los Alpes (Dallan et al., 2022; Libertino et al., 2019), ya que puede incrementar la probabilidad de peligros como avenidas torrenciales. Los mecanismos subyacentes incluyen:  
- una mayor capacidad de la atmósfera para retener vapor de agua a temperaturas más altas;  
- cambios en la dinámica de las células convectivas impulsados por la temperatura, que redistribuyen la humedad hacia el núcleo de las células, aumentando su intensidad máxima pero reduciendo su extensión espacial;  
- y cambios en la circulación global, que pueden modificar la frecuencia de los sistemas meteorológicos asociados a la generación de flujos de detritos (Armon et al., 2022; Berg et al., 2013; Lochbiler et al., 2017).

Estos cambios probablemente influirán en la probabilidad futura de ocurrencia de flujos de detritos (Gariano & Guzzetti, 2016).

Un marco común para evaluar cuándo los deslizamientos generan flujos de detritos es el criterio de falla de *Coulomb* (Iverson et al., 1997). Este criterio fue descrito por primera vez por Coulomb (1973) y ha sido ampliamente utilizado en mecánica de suelos y flujos granulares (e.g., Iverson & Denlinger, 2001). Se ha demostrado mediante datos de campo y laboratorio que la falla de una masa de suelo ocurre cuando:

$$
\tau = \sigma' \tan \varphi + c
$$

donde:  $\tau$ es el esfuerzo cortante medio que actúa sobre la superficie de falla,  $\sigma'$ es el esfuerzo normal efectivo,  $\varphi$ es el ángulo de fricción del suelo (por fricción superficial e interbloqueo de clastos),  $c$ es la cohesión aparente (Lambe & Whitman, 1991).

La cohesión puede originarse en distintos factores, como las fuerzas entre partículas de arcilla (Ikari & Kopf, 2011), la cementación (Cui et al., 2017), raíces y vegetación (Zhang et al., 2010) o hielo (Arenson & Springman, 2005).

El esfuerzo normal efectivo $\sigma'$ se define como:

$$
\sigma' = \sigma - p
$$

donde $\sigma$ es el esfuerzo normal total sobre la superficie de falla y $p$ es la presión de poros (Terzaghi, 1936). 

Aunque el criterio de Coulomb define la falla sobre una superficie de deslizamiento, no especifica cuándo un deslizamiento se convierte en flujo de detritos. La teoría indica que cuando la cohesión es baja o nula, y el gradiente vertical de presión de poros iguala el gradiente vertical del esfuerzo normal total, el esfuerzo efectivo es cero y el suelo puede fluir como un líquido (*licuefacción*).

Estas condiciones pueden ocurrir debido a:  
- Eventos transitorios como terremotos o deslizamientos, que alteran las estructuras y trayectorias del flujo (Sassa et al., 1996),  
- Contracción de suelos densamente empaquetados bajo cizalladura, donde el espacio poroso se reduce más rápido que la disipación de la presión de poros (Goren et al., 2010; Iverson, 2005).

Se ha planteado que la movilización en flujo de escombros ocurre principalmente en suelos sueltos, es decir, con densidades inferiores al estado crítico de equilibrio (Wood, 1990). Durante la contracción (por falla del suelo o impacto de un deslizamiento sobre un canal), la presión de poros aumenta, ya que el agua no puede disiparse. Esto es conocido como carga no drenada (Terzaghi & Peck, 1948).


## Acoplamiento

La forma más directa de acoplar áreas fuente y recorrido es evaluando primero las áreas fuente potenciales y utilizando estas en un modelo de propagación. Esto puede hacerse considerando puntos de inicio binarios (**fuente/no fuente**) o utilizando el valor de susceptibilidad o probabilidad de la zona de inicio, si está disponible, vinculando así la susceptibilidad de recorrido con la susceptibilidad de inicio (por ejemplo, Michoud et al., 2012 para caída de rocas usando el software Flow-R).

Existen pocos estudios sobre el acoplamiento de análisis estadísticos de susceptibilidad a deslizamientos con los modelos de recorrido correspondientes. Desde principios de la década de 2000 se ha escrito mucho sobre análisis estadísticos de susceptibilidad (liberación), omitiendo las consecuencias ladera abajo de los deslizamientos. Solo recientemente se han propuesto enfoques más integrados (por ejemplo, Goetz et al., 2021; Mergili et al., 2019).

Mergili et al. (2019) señalaron dos formas posibles de acoplamiento, basadas en un modelo estadístico simple de liberación de deslizamientos y la herramienta de enrutamiento r.randomwalk:

- **Enfoque ascendente (bottom-up):** para cada píxel del área de estudio (píxel objetivo), se combina la probabilidad de que haya al menos un deslizamiento en el área de captación con la probabilidad de que dicho deslizamiento alcance el píxel objetivo, basándose en la función de densidad de probabilidad empíricamente derivada del ángulo de alcance para el área de estudio.

- **Enfoque descendente (top-down):** el enrutamiento se realiza desde cada píxel del área de estudio (píxel fuente), y la probabilidad de que cada píxel objetivo sea afectado por un deslizamiento es función de la susceptibilidad de liberación y de la probabilidad de que el píxel objetivo sea alcanzado por el deslizamiento, nuevamente basada en la función de densidad de probabilidad empíricamente derivada del ángulo de alcance. Esto se resuelve escalando el número de caminatas aleatorias con la susceptibilidad de liberación de cada píxel fuente.

Mergili et al. (2019) afirman que el enfoque ascendente es estadística y matemáticamente más limpio y proporciona una probabilidad espacial real y cuantitativa. Sin embargo, este enfoque no es muy intuitivo e implica un nivel sustancial de suavizado de los patrones de susceptibilidad a deslizamientos, por lo que el resultado se correlaciona fuertemente con el tamaño de la cuenca de captación de cada píxel objetivo. El enfoque descendente, en contraste, es más intuitivo y directo. Sin embargo, la superposición de las trayectorias que parten de muchos píxeles fuente complica la derivación de una probabilidad real y conduce a una dominancia del componente de recorrido sobre el componente de liberación en los resultados finales. Las estrategias para abordar estos problemas de superposición mejorarán el acoplamiento estadístico de los modelos de liberación y recorrido.

Los métodos basados en escenarios son una alternativa práctica y con frecuencia se acoplan con estadísticas de susceptibilidad. Estos métodos implican ejecutar múltiples escenarios de flujos de escombros a partir de clases de susceptibilidad (y sus respectivas métricas de probabilidad) utilizando ubicaciones de inicio asignadas aleatoriamente, de forma uniforme o manualmente dentro de cada clase. Las zonas de inicio generadas aleatoriamente o de forma uniforme requieren que el usuario aplique una red suficientemente densa de ubicaciones potenciales de inicio de deslizamientos, y numere esas ubicaciones del 1 al n de modo que ningún escenario individual se superponga de manera poco realista. El usuario puede ejecutar cada escenario (**escenario 1 … escenario n**) múltiples veces para determinar las diferencias entre las ejecuciones del escenario.

Las zonas de inicio generadas manualmente son similares, pero tienden a basarse en el juicio experto (ubicaciones fuente potenciales observables) dentro de una clase de susceptibilidad. Las zonas de inicio generadas aleatoria o uniformemente se adaptan mejor a las pruebas estadísticas y son más prácticas en regiones más grandes. Los datos de amenaza (**hazard data**), más que solo los datos de susceptibilidad, proporcionan mejores limitaciones y discretización de los escenarios (es decir, es útil conocer el número esperado de flujos de escombros/unidad de área/unidad de tiempo para un escenario dado dentro de una clase determinada).
