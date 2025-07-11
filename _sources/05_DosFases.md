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

## Fenómenos físicos clave en flujos bifásicos

El modelo bifásico general de Pudasaini (2012) se distingue por incorporar de manera rigurosa una serie de mecanismos físicos que son fundamentales para describir la dinámica de los flujos de detritos. A continuación, se detallan los más importantes:

#### Arrastre Generalizado (*Generalized Drag*)

El arrastre es uno de los aspectos más básicos e importantes de un flujo bifásico, ya que influye directamente en el movimiento relativo entre las fases sólida y fluida. Un aumento en el valor del coeficiente de arrastre ($C_{DG}$) produce menos movimiento relativo (y, por tanto, menos separación) entre las fases, ralentiza el movimiento general y frena el avance del frente. Esto se debe a que un frente de flujo con una mayor intensidad de arrastre se quedará rezagado con respecto a uno con menor intensidad. Por lo tanto, una modelización adecuada del arrastre es un requisito indispensable para simular adecuadamente los flujos de detritos bifásicos.

la fuerza de arrastre (o drag) es una fuerza de fricción que surge cuando hay un movimiento relativo entre dos componentes, típicamente un objeto sólido y el fluido que lo rodea. Piénsalo como la resistencia que sientes al mover tu mano rápidamente a través del agua. Esa resistencia es el arrastre.

Un modelo bifásico resuelve ecuaciones de conservación de masa y momento por separado para la fase sólida y para la fase fluida. Esto tiene consecuencias cruciales:

* Existencia de velocidad relativa ($u_f − u_s$): Al tener ecuaciones separadas, el modelo calcula una velocidad para los sólidos ($u_s$) y otra para el fluido ($u_f$). La diferencia entre estas dos es la velocidad relativa. En un flujo de detritos real, esta diferencia es constante: el agua puede percolar a través de los sólidos, o los bloques en el frente pueden moverse más rápido que la matriz lodosa.

* El arrastre como fuerza de interacción: La fuerza de arrastre (MD) es directamente proporcional a esta velocidad relativa. Si la velocidad relativa es cero, el arrastre es cero. Si es alta, el arrastre es una fuerza dominante. Esta fuerza es el mecanismo principal de transferencia de momento entre las fases. Es la forma en que el fluido "empuja" a los sólidos, y los sólidos "frenan" al fluido.

* Simulación de Fenómenos Reales: Solo al considerar el arrastre se pueden simular fenómenos clave observados en la realidad, como: (i) Frentes ricos en bloques: Donde los sólidos más grandes, por inercia, se mueven más rápido que el fluido, y el fluido ejerce una fuerza de arrastre que los frena. (ii) Frentes fluidizados: Donde el agua a alta presión se mueve más rápido que los sólidos, los "arrastra" y reduce la fricción interna, aumentando la movilidad. (iii) Separación de fases: La diferencia de velocidades y el arrastre resultante son los que provocan que, con el tiempo, un flujo pueda desarrollar un frente más grueso y una cola más diluida.

En conclusión, el efecto de arrastre no es una propiedad del material, sino un resultado de la interacción dinámica entre fases que se mueven a diferentes velocidades. Por lo tanto, es un fenómeno que, por su propia naturaleza física, solo puede ser capturado por un modelo que trate al menos dos fases (sólidos y fluido) de forma independiente, como lo hace el modelo bifásico de Pudasaini (2012). Los modelos monofásicos, al promediar todo en un único "fluido equivalente", pierden por completo esta física esencial.

#### Flotabilidad (*Buoyancy*)

La flotabilidad es un aspecto crucial porque aumenta la movilidad del flujo al reducir la resistencia por fricción en la mezcla. Este efecto está presente siempre que haya un fluido en la mezcla. La flotabilidad reduce el esfuerzo normal de los sólidos, los esfuerzos normales laterales y el esfuerzo cortante basal (es decir, la resistencia por fricción) en un factor de $(1 - \gamma)$, donde $\gamma$ es la relación de densidades entre el fluido y el sólido. El efecto es sustancial cuando la relación de densidades es grande, como ocurre en los flujos de detritos naturales.

En el caso extremo de que el flujo sea neutramente flotante (es decir, $\gamma = 1$, como en los experimentos de Bagnold, 1954), la masa de detritos se fluidiza y puede recorrer distancias mucho más largas. Un flujo neutramente flotante muestra un comportamiento completamente diferente a uno normalmente flotante: las fases sólida y fluida se mueven juntas, la masa de detritos se fluidiza, el frente avanza mucho más lejos, la cola se queda atrás y la altura general del flujo se reduce.

#### Masa Virtual (*Virtual Mass*)

Mientras que la fuerza de arrastre considera la interacción de las fases en un campo de flujo uniforme, la masa virtual entra en juego cuando las partículas sólidas aceleran con respecto al fluido. Esta aceleración relativa obliga a que una parte del fluido circundante también se acelere, lo que induce una fuerza adicional llamada fuerza de masa virtual (que representa la energía cinética inducida en la fase fluida por las partículas sólidas).

Debido a la fuerza de masa virtual, las partículas sólidas arrastran consigo más masa de fluido, y este es "bombeado" hacia el frente del flujo. Al observar el frente, se puede ver un flujo de agua ("agua lodosa") seguido por el pulso principal de detritos. La masa sólida pierde algo de inercia y es, en cierto modo, empujada hacia atrás por el fluido. Este fenómeno de un frente liderado por un flujo de agua es observable en algunos flujos de detritos naturales. Los modelos de flujos de detritos anteriores no incluían el efecto de la masa virtual.

#### Esfuerzo Viscoso Newtoniano (*Newtonian Viscous Stress*)

La viscosidad del fluido, que puede variar según la composición del flujo, afecta sustancialmente la dinámica. Un flujo con un fluido no viscoso ($\eta_f \approx 0$) se comporta de manera muy diferente a uno con un fluido viscoso (por ejemplo, con una viscosidad de 2 Pa·s, un valor típico para flujos de detritos).

Las simulaciones demuestran que el esfuerzo viscoso controla la propagación del frente del flujo y determina cómo la masa de detritos se alarga y deforma. La cantidad de fluido en la cola de un flujo es sustancialmente mayor cuando no hay esfuerzo viscoso en comparación con un flujo que sí lo experimenta. Incluso con una pequeña cantidad de fluido en la mezcla, el efecto del esfuerzo viscoso es importante, ya que reduce sustancialmente la deformación. Por lo tanto, el efecto de la resistencia viscosa debe tenerse en cuenta en la simulación de flujos de detritos. Los modelos anteriores no incluían sistemáticamente el efecto del esfuerzo viscoso (o la viscosidad del fluido) en la dinámica de los flujos bifásicos.




