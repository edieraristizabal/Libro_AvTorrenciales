# r.randomwalk

*r.randomwalk* (Mergili, 2022; Mergili et al., 2015) representa una herramienta multifuncional para el enrutamiento de procesos de movimientos en masa. Puede utilizarse como una extensión del software de código abierto *GRASS GIS*. La arquitectura de la herramienta consiste en un núcleo programado en *C*, con un script en *Python* envolviéndolo para el pre- y postprocesamiento de los datos. Los procedimientos estadísticos automáticos, visualización y funcionalidades de evaluación están incluidos a través de scripts en *R*, que son llamados directamente desde el script en Python.

### Componentes

El núcleo de *r.randomwalk* es un algoritmo de enrutamiento de caminata aleatoria restringida acoplado a una selección de criterios de detención, incluyendo valores simples y funciones de ángulos de recorrido, así como un modelo físicamente basado simple (modelo de fricción de 2 parámetros). Las caminatas aleatorias pueden iniciarse desde un número arbitrario de puntos individuales o áreas de liberación de deslizamientos, o desde un mapa de susceptibilidad de liberación de deslizamientos, y se enrutan a través del terreno hasta que se cumplen todos los criterios de detención aplicados. Puede utilizarse un número arbitrario de diferentes criterios de detención de diferentes tipos para derivar medidas de probabilidad de que un píxel objetivo sea alcanzado (puntaje del indicador de impacto).

Las simulaciones también pueden ejecutarse con grandes cantidades de combinaciones de parámetros, y la fracción de combinaciones de parámetros que predicen un impacto en un píxel objetivo se denomina *índice del indicador de impacto*. Finalmente, puede estimarse una probabilidad de impacto basada en ángulos de recorrido calculados a partir de deslizamientos observados.

### Datos

La pieza central de datos necesaria para todos los tipos de uso de *r.randomwalk* es un DEM. Aparte de esto, los datos requeridos dependen del tipo de uso. Los píxeles fuente pueden definirse mediante un archivo de texto que proporciona coordenadas y, opcionalmente, volúmenes y otros parámetros que caracterizan la liberación de un número arbitrario de eventos (un evento por línea). Opcionalmente, el archivo de liberación puede vincularse a un mapa raster de liberación, o puede proporcionarse el mapa raster de liberación sin un archivo de liberación. También es posible definir la liberación a través de un mapa de susceptibilidad de liberación de deslizamientos, lo cual es importante para acoplar la liberación y el alcance. En aquellos casos donde se involucre calibración o evaluación, se requiere un mapa raster del área de impacto observada como entrada.

Además, el modelo necesita conjuntos de parámetros que controlan las caminatas aleatorias y los criterios de detención, así como varias otras funcionalidades, dependiendo de su uso.

### Salidas

Además de los mapas raster (como raster ASCII y visualizaciones cartográficas a través de gráficos generados en *R*), *r.randomwalk* proporciona archivos de texto que caracterizan los parámetros de enrutamiento para cada evento bajo investigación, con parámetros como el tamaño del área de impacto, distancias de recorrido horizontal y vertical, y ángulos de recorrido.

También se generan archivos y gráficos adicionales (como gráficos ROC o mapas de calor), que indican la sensibilidad de la salida a la parametrización de las ecuaciones empíricas y el procedimiento de caminata aleatoria, dependiendo de qué funcionalidades del software se utilicen.

### Calibración y evaluación

*r.randomwalk* permite el retrocálculo (*back-calculation*) del ángulo de recorrido y la distancia de desplazamiento de los eventos representados en el mapa del área de impacto. Este retrocálculo puede utilizarse para producir automáticamente una función de densidad de probabilidad de los ángulos de recorrido o distancias de desplazamiento, que luego —nuevamente automáticamente— se puede utilizar para producir un mapa de probabilidad de impacto basado en las mismas áreas fuente u otras áreas fuente arbitrarias.

El mapa de probabilidad de impacto puede evaluarse contra el mapa del área de impacto, resultando en un gráfico ROC que indica el rendimiento del modelo. Si es aplicable al flujo de trabajo específico, es posible dividir los datos en un conjunto de entrenamiento (para la derivación de la función de densidad de probabilidad) y un conjunto de evaluación (para el gráfico ROC).
