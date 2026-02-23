# Flow-R

Flow-R (Evaluación de trayectorias de flujo de peligros gravitacionales a escala regional; Horton et al., 2013) fue desarrollado principalmente para la cartografía de susceptibilidad a flujos de detritos a escala regional. Sin embargo, también se ha utilizado para otros peligros gravitacionales como caídas de rocas, avalanchas de rocas, deslizamientos superficiales y avalanchas de nieve. Fue diseñado para proporcionar flexibilidad en términos de datos y algoritmos para que su uso pueda adaptarse a la disponibilidad de datos y al proceso de interés.

La primera versión, escrita en Matlab, fue publicada en 2009 y está disponible gratuitamente (Horton, 2022). Una nueva versión, Flow-R v2, escrita en C++, fue publicada en 2020 y es comercial. Esta nueva versión abordó varias limitaciones de la primera. Proporciona un aumento sustancial en el rendimiento y un manejo eficiente de la memoria que facilita trabajar con extensiones espaciales sin restricciones. También es significativamente más amigable para el usuario y los datos (admite muchos formatos de datos).

### Componentes

Una identificación de las áreas fuente potenciales se proporciona en Flow-R v1, que consiste en una combinación de múltiples capas de datos con reglas de clasificación. Para la versión 2, las áreas fuente pueden prepararse en cualquier software GIS. Luego, Flow-R propaga la susceptibilidad a flujos de detritos desde cada área fuente. Aunque el valor inicial para propagar suele ser el valor normalizado 1, se pueden asignar valores de susceptibilidad inicial específicos a cada área fuente. Esto permite tener en cuenta diferentes valores iniciales de susceptibilidad a la falla o frecuencias en el mapa resultante (p. ej., Michoud et al., 2012). Flow-R no se basa en un enfoque de caminata aleatoria sino que propaga la susceptibilidad desde cada área fuente a través de una única propagación, cuya extensión está destinada a cubrir todos los eventos posibles. El resultado principal es una susceptibilidad espacialmente distribuida que representa áreas donde es más probable que ocurran flujos de detritos.

El alcance calculado por Flow-R se basa en algoritmos de propagación que controlan la trayectoria y la dispersión de la susceptibilidad y en leyes de fricción simples que determinan la distancia de alcance. Los algoritmos de dirección de flujo y las funciones de persistencia controlan el enrutamiento y la dispersión. Se implementan varios algoritmos de dirección de flujo, como D8 (O’Callaghan & Mark, 1984), D-infinity (Tarboron & Tarboton, 1997), Rho8 (Fairfield & Leymarie, 1991), dirección de flujo múltiple (Quinn et al., 1991), Freeman (1991), Gamma (2000) y Holmgren (1994), así como su versión modificada (Horton et al., 2013). La versión modificada del algoritmo de Holmgren es la más utilizada, ya que permite reproducir la mayoría de los algoritmos mediante su parámetro que controla la dispersión. Hay disponibles diferentes esquemas de ponderación para la función de persistencia.

Dos algoritmos están disponibles para tener en cuenta la fricción: el modelo de fricción de dos parámetros de Perla et al. (1980) y un modelo simplificado limitado por fricción (SFLM; Horton et al., 2013), que consiste en un enfoque de línea de energía combinado con una limitación de la velocidad máxima. Esta limitación tiene como objetivo mantener la energía en valores razonables en cuencas empinadas. Con velocidades máximas observadas de flujos de detritos en Suiza de 13–14 m/s (Rickenmann & Zimmermann, 1993), a menudo se utiliza un límite de 15 m/s.

### Requisitos de Datos

Flow-R es flexible en términos de requisitos de datos. El requisito mínimo es un DEM para la versión 1. Para la versión 2, también se requiere un archivo con las áreas fuente. Como Flow-R v1 proporciona una identificación de las áreas fuente potenciales, se puede proporcionar cualquier conjunto de datos considerado relevante, como mapas de uso del suelo o geológicos o cualquier producto derivado del DEM. Para la propagación, solo se requiere el DEM. Opcionalmente, se puede proporcionar un archivo raster que proporcione ángulos de recorrido espacialmente variables para tener en cuenta diferentes clases de cobertura del suelo o medidas de mitigación, por ejemplo.

### Salidas

La mayoría de los resultados de Flow-R se exportan como archivos raster en formato geotiff (Flow-R v2) o ascii (Flow-R v1). La salida principal es el valor de susceptibilidad para cada celda del área de estudio, expresado como el valor máximo y/o la suma de los valores de susceptibilidad de todas las propagaciones originadas desde diferentes áreas fuente. Para mayor comodidad, también se puede exportar la extensión general de todas las propagaciones, así como el número de propagaciones que pasan por una celda dada (solo v2). Además, se puede exportar un shapefile que contiene la extensión de cada propagación (solo v2). También se pueden exportar raster que contienen valores de energía o velocidad (valores máximos por celda) para fines informativos. Sin embargo, deben considerarse con precaución, ya que se basan en cálculos utilizando un enfoque de masa unitaria.

A menudo se aplica un enfoque multiparamétrico que consiste en calcular propagaciones con diferentes conjuntos de parámetros que representan escenarios más o menos conservadores, para proporcionar clases de susceptibilidad. Los resultados de estos escenarios se combinan mediante reclasificación para asignar una clase de susceptibilidad más alta a los escenarios menos conservadores y una clase más baja a los escenarios más conservadores.

### Calibración y Evaluación

La calibración de Flow-R se basa principalmente en un enfoque de prueba y error, utilizando un inventario de eventos observados como referencia. La calibración puede realizarse en un área más pequeña bien documentada que sea representativa de la región. Luego, los parámetros pueden aplicarse a toda la región, si es posible con eventos observados adicionales que pueden usarse para validación. El objetivo de la calibración es cubrir la extensión de los eventos observados mientras se minimizan las áreas donde es poco probable que ocurran flujos de detritos.

Alternativamente, también se ha utilizado un enfoque basado en una matriz de confusión propuesto por Scheidl y Rickenmann (2010) para calibrar Flow-R (Pastorello et al., 2017). Consiste en calcular y maximizar indicadores de precisión utilizando la extensión de eventos pasados.

Los parámetros que controlan la propagación y los que gobiernan la distancia de alcance pueden calibrarse de forma independiente, ya que no interfieren en gran medida entre sí. Para flujos de detritos, el modelo de dos parámetros de Perla (PCM) y el SFLM proporcionan resultados similares. Sin embargo, el SFLM es más fácil de calibrar y, por lo tanto, se utiliza con mayor frecuencia. Cuando se utiliza el modelo PCM, se pueden usar parámetros clásicos para flujos de detritos.


| Elemento                      | Flow-R v1                            | Flow-R v2                              |
|-------------------------------|---------------------------------------|----------------------------------------|
| DEM                           | Obligatorio                           | Obligatorio                            |
| Áreas fuente                  | Generadas por el modelo               | Preparadas en SIG externo              |
| Capas adicionales             | Opcionales: uso del suelo, geología   | Opcionales: uso del suelo, geología    |
| Ángulo de recorrido variable  | No                                    | Opcional (raster adicional)            |

