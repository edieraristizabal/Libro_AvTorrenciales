# Modelos de dos fases (granular-fluido): 
Más allá de los modelos reológicos efectivos, en años recientes han surgido modelos basados en mezclas bifásicas, que resuelven por separado el comportamiento del sólido granular y del fluido intersticial (e.g. modelo de Iverson & Denlinger 2001; Pudasaini 2012). 
Estos modelos no suponen una reología única, sino que combinan ecuaciones de balanza para cada fase con términos de interacción (arrastre, colisión, presión de poros). Aunque proporcionan una descripción física más detallada (pudiendo reproducir la generación de sobrepresiones de poro o la sedimentación de granos), son matemáticamente más complejos y requieren muchos parámetros. 
Para un curso teórico avanzado, vale la pena mencionar que los modelos reológicos monofásicos (Bingham, HB, etc.) son a veces considerados simplificaciones “efectivas” de un sistema bifásico más complejo, y que autores como Iverson han criticado la aproximación reológica por considerarla una “ficción” conveniente. 
Sin embargo, en la práctica de la ingeniería y la geociencia aplicada, los modelos reológicos sencillos siguen siendo ampliamente usados dada su parsimonia de parámetros y la relativa facilidad de calibración frente a datos de campo.

Los modelos promediados en profundidad más simples idealizan los flujos de escombros como materiales monofásicos con densidades volumétricas fijas. 
Estos modelos incluyen tres ecuaciones de conservación: una que expresa la conservación de masa y dos que expresan la conservación de los componentes ortogonales del momento lineal, ya sea paralelo al lecho o en dirección horizontal (por ejemplo, McDougall & Hungr, 2004; Rickenmann et al., 2006). 
Las tres ecuaciones generalmente difieren de las ecuaciones estándar de aguas poco profundas solo en sus definiciones de la resistencia al flujo y de los coeficientes de tensión longitudinal. 
Su similitud con las ecuaciones de aguas poco profundas tiene ventajas significativas desde el punto de vista matemático y computacional, debido a que las ecuaciones de aguas poco profundas tienen una larga historia de análisis teórico, soluciones numéricas y aplicaciones prácticas (por ejemplo, Berger et al., 2011; Vreugdenhil, 1994). 

Sin embargo, los modelos monofásicos de flujo de escombros omiten una característica central del comportamiento de los flujos de escombros: la evolución natural de la resistencia al flujo que resulta de las interacciones cambiantes entre los constituyentes sólido y fluido durante la evolución de la velocidad del flujo y de la densidad volumétrica. 
Esta evolución indica que la resistencia al flujo es una propiedad emergente que coevoluciona con la dinámica del flujo (Iverson, 2003a), lo que implica que no es apropiado especificar a priori una resistencia al flujo en evolución.

Los modelos que tratan los flujos de escombros como materiales bifásicos, con densidades volumétricas en evolución, interacciones sólido-fluido y resistencia al flujo variable, típicamente incluyen de cuatro a seis ecuaciones de conservación. 
Una de estas ecuaciones expresa la conservación de la masa sólida y otra expresa la conservación de la masa del fluido o la conservación de la masa de la mezcla bifásica como un todo. 
Las demás ecuaciones de conservación expresan los componentes ortogonales del momento lineal, ya sea de constituyentes sólido y fluido separados pero que interactúan (por ejemplo, Bouchut et al., 2016; Meyrat et al., 2022; Pitman & Le, 2005; Pudasaini, 2012) o de una mezcla bifásica cuyos volúmenes fraccionales de sólido y fluido evolucionan a medida que los constituyentes interactúan (Iverson & George, 2014; Kowalski & McElwaine, 2013).

Los fundamentos conceptuales de estos dos enfoques son similares, pero difieren en un aspecto importante. 
Un enfoque que considera fases sólidas y fluidas distintas permite la posibilidad de una separación completa de las dos fases en cuerpos compuestos enteramente de fluido o enteramente de granos sólidos, mientras que un enfoque que considera una mezcla bifásica asume que siempre hay alguna amalgama de granos y fluido, aunque las concentraciones de granos o fluido puedan volverse muy pequeñas en algunas circunstancias.

Un aspecto fundamental en la formulación de todos los modelos bifásicos de flujo de escombros es la definición de la fase fluida. 
Una justificación proporcionada por Iverson (1997) es que la fase fluida incluye granos pequeños que pueden permanecer en suspensión por fuerzas puramente hidrodinámicas, sin necesidad de fuerzas de interacción granular, durante la duración de un flujo de escombros.
Estas partículas pequeñas en suspensión aumentan la viscosidad efectiva del fluido en relación con la viscosidad del agua pura y, en concentraciones suficientemente altas, pueden conferir cierta resistencia al flujo en la fase fluida. 
Típicamente, estas partículas pequeñas son del tamaño de arcilla y limo (<0.0625 mm), mientras que las partículas más grandes se consideran parte de la fase granular. El agua lodosa que drena de los márgenes de depósitos recientes de flujo de escombros proporciona evidencia de que las partículas del tamaño de limo y arcilla pueden permanecer en suspensión incluso después de que el movimiento del flujo de escombros cesa (por ejemplo, Logan et al., 2007).

El uso de más de tres ecuaciones de conservación en modelos bifásicos y de mezcla bifásica hace que su estructura matemática y computacional sea más compleja que la de los modelos monofásicos. 
Sin embargo, el uso de ecuaciones de conservación adicionales simplifica los modelos bifásicos y de mezcla bifásica desde un punto de vista físico, porque reduce la cantidad de supuestos necesarios en la derivación de las ecuaciones y clarifica las definiciones de los parámetros del modelo. 
El número total de ecuaciones diferenciales en cualquier modelo de flujo de escombros debe, por supuesto, igualar el número total de variables dependientes del modelo. 
Un principio básico de la física matemática, aplicable en la modelación de flujos de escombros, es que predecir el valor de un número creciente de variables dependientes permite realizar pruebas del modelo cada vez más diversas y estrictas. 
Los modelos que pueden predecir con éxito el valor del mayor número de variables dependientes de forma simultánea son los más probables de ser físicamente correctos (Iverson, 2003b).



