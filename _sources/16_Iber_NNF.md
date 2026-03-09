# Análisis de Modelos Reológicos para la Modelación de Lahares con Iber-NNF

Este documento detalla la extracción técnica de los modelos y resultados presentados en el estudio de Sanz-Ramos *et al.* (2025) sobre el lahar del volcán Popocatépetl.

---

## 1. Módulo No Newtoniano de Iber (Iber-NNF)

El software **Iber** es una herramienta hidrodinámica bidimensional que originalmente resuelve las ecuaciones de aguas someras promediadas en profundidad (2D-SWE). El módulo **Iber-NNF** incorpora la física de fluidos no newtonianos utilizando modelos reológicos como términos friccionales.

### Ecuaciones de Conservación
Iber-NNF resuelve las ecuaciones en un sistema de coordenadas cartesianas:

**Ecuación de continuidad:**
$$\frac{\partial h}{\partial t}+\frac{\partial q_{x}}{\partial x}+\frac{\partial q_{y}}{\partial y}=0$$

**Ecuaciones de cantidad de movimiento:**
$$\frac{\partial q_{x}}{\partial t}+\frac{\partial}{\partial x}(\frac{q_{x}^{2}}{h}+gk_{p}\frac{h^{2}}{2})+\frac{\partial}{\partial y}(\frac{q_{x}q_{y}}{h})=g^{\prime}h(S_{o,x}-S_{f,x})$$
$$\frac{\partial q_{y}}{\partial t}+\frac{\partial}{\partial x}(\frac{q_{x}q_{y}}{h})+\frac{\partial}{\partial y}(\frac{q_{y}^{2}}{h}+g^{\prime}k_{p}\frac{h^{2}}{2})=g^{\prime}h(S_{o,y}-S_{f,y})$$

Donde:
* $h$: profundidad del fluido.
* $q_{x}, q_{y}$: componentes del caudal específico.
* $g'$: gravedad corregida por la pendiente ($g \cos^{2}\theta$).
* $S_{o}$: pendiente del fondo.
* $S_{f}$: pendiente de fricción reológica.
* $k_{p}$: factor de presión no hidrostática.

---

## 2. Modelos Reológicos e Implementación

La pendiente de fricción $S_{f}$ se calcula según el modelo seleccionado. La versión actual de Iber implementa ocho modelos reológicos: Manning, Viscoso, Dilatante, Voellmy, Bartelt, Bingham (simplificado), O'Brien-Julien (cuadrático) y Herschel-Bulkley. Todos ellos pueden usarse para modelar lahares, excepto Bartelt (pensado primordialmente para avalanchas de nieve con fuerzas de cohesión). Los modelos se relacionan con el esfuerzo cortante mediante la expresión $\tau=\rho ghS_{f}$.

### A. Modelo de Manning
Basado en la resistencia dependiente de la velocidad, comúnmente usado en hidráulica convencional:
$$S_{f}=\frac{n^{2}v^{2}}{h^{4/3}}$$
* **Parámetros:** $n$ (coeficiente de Manning ).

### B. Modelo de Bingham (Simplificado)
Representa fluidos con un umbral de fluencia y viscosidad:
$$S_{f}=\frac{1}{\rho gh}(\omega\tau_{y}+3\frac{\mu_{B}v}{h})$$
* **Parámetros:** $\tau_{y}$ (esfuerzo de fluencia), $\mu_{B}$ (viscosidad dinámica).
* **Explicación:** Incorpora tanto el esfuerzo de fluencia como el viscoso para simular comportamientos dinámicos y estáticos.

### C. Modelo de Voellmy
Suma la fricción turbulenta y la fricción seca de tipo Coulomb:
$$S_{f}=\frac{v^{2}}{\xi h}+\mu$$
* **Parámetros:** $\xi$ (coeficiente de fricción turbulenta), $\mu$ (coeficiente de fricción de Coulomb/basal).

### D. Modelo Cuadrático (O'Brien y Julien)
Combina términos de fluencia, viscosidad y turbulencia en una ecuación cuadrática:
$$S_{f}=\frac{\tau_{y}}{\rho gh}+\frac{K\mu_{B}v}{8\rho gh^{2}}+\frac{n^{2}v^{2}}{h^{4/3}}$$
* **Parámetros:** $\tau_{y}, \mu_{B}, n$ y $K$ (parámetro de resistencia).

### E. Modelo de Herschel-Bulkley
Captura comportamientos no lineales tras superar el esfuerzo de fluencia:
$$S_{f}=\frac{1}{\rho gh}(\tau_{y}+k(\frac{v}{h})^{a})$$
* **Parámetros:** $\tau_{y}, k$ (consistencia) y $a$ (potencia de corte o "shear power").


## 4. Referencias Bibliográficas

* **Bingham, E. C. (1916).** An investigation of the laws of plastic flow. *Bulletin of the Bureau of Standards*, 13(2), 309-353.
* **Bladé, E., Cea, L., Corestein, G., Escolano, E., Puertas, J., Vázquez-Cendón, E., Dolz, J., & Coll, A. (2014a).** Iber: herramienta de simulación numérica del flujo en ríos. *Revista Internacional de Métodos Numéricos Para Cálculo y Diseño En Ingeniería*, 30(1), 1-10.
* **Capra, L., Poblete, M. A., & Alvarado, R. (2004).** The 1997 and 2001 lahars of Popocatépetl volcano (Central Mexico): textural and sedimentological constraints on their origin and hazards. *Journal of Volcanology and Geothermal Research*, 131(3-4), 351-369.
* **Chow, V. Te. (1959).** *Open-Channel Hydraulics*. McGraw-Hill Book Company Inc..
* **Herschel, W. H., & Bulkley, R. (1926).** Konsistenzmessungen von Gummi-Benzollösungen. *Kolloid-Zeitschrift*, 39(4), 291-300.
* **Muñoz-Salinas, E., Manea, V. C., Palacios, D., & Castillo-Rodriguez, M. (2007).** Estimation of lahar flow velocity on Popocatépetl volcano (Mexico). *Geomorphology*, 92(1-2), 91-99.
* **O'Brien, J. S., & Julien, P. Y. (1988).** Laboratory Analysis of Mudflow Properties. *Journal of Hydraulic Engineering*, 114(8), 877-887.
* **Sanz-Ramos, M., Bladé, E., Diez-Herrero, A., Vázquez-Tarrio, D., Garrote, J., Sánchez, N., & Galindo, I. (2025).** An analysis of rheological models for lahar modelling with Iber. *Revista Mexicana de Ciencias Geológicas*, 42(3), 160-169.
* **Voellmy, A. (1955).** Über die Zerstörungskraft von Lawinen. *Schweizerische Bauzeitung*, 73, 15.