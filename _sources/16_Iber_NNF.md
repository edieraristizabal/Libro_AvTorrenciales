# Análisis de Modelos Reológicos para la Modelación de Lahares con Iber-NNF

[cite_start]Este documento detalla la extracción técnica de los modelos y resultados presentados en el estudio de Sanz-Ramos *et al.* (2025) sobre el lahar del volcán Popocatépetl[cite: 13, 14, 15].

---

## 1. Módulo No Newtoniano de Iber (Iber-NNF)

[cite_start]El software **Iber** es una herramienta hidrodinámica bidimensional que originalmente resuelve las ecuaciones de aguas someras promediadas en profundidad (2D-SWE)[cite: 78, 90]. [cite_start]El módulo **Iber-NNF** incorpora la física de fluidos no newtonianos utilizando modelos reológicos como términos friccionales[cite: 86, 109].

### Ecuaciones de Conservación
[cite_start]Iber-NNF resuelve las ecuaciones en un sistema de coordenadas cartesianas[cite: 90, 91]:

**Ecuación de continuidad:**
$$\frac{\partial h}{\partial t}+\frac{\partial q_{x}}{\partial x}+\frac{\partial q_{y}}{\partial y}=0$$

**Ecuaciones de cantidad de movimiento:**
$$\frac{\partial q_{x}}{\partial t}+\frac{\partial}{\partial x}(\frac{q_{x}^{2}}{h}+gk_{p}\frac{h^{2}}{2})+\frac{\partial}{\partial y}(\frac{q_{x}q_{y}}{h})=g^{\prime}h(S_{o,x}-S_{f,x})$$
$$\frac{\partial q_{y}}{\partial t}+\frac{\partial}{\partial x}(\frac{q_{x}q_{y}}{h})+\frac{\partial}{\partial y}(\frac{q_{y}^{2}}{h}+g^{\prime}k_{p}\frac{h^{2}}{2})=g^{\prime}h(S_{o,y}-S_{f,y})$$

[cite_start]Donde[cite: 108, 109]:
* $h$: profundidad del fluido.
* $q_{x}, q_{y}$: componentes del caudal específico.
* $g'$: gravedad corregida por la pendiente ($g \cos^{2}\theta$).
* $S_{o}$: pendiente del fondo.
* $S_{f}$: pendiente de fricción reológica.
* $k_{p}$: factor de presión no hidrostática.

---

## 2. Modelos Reológicos e Implementación

La pendiente de fricción $S_{f}$ se calcula según el modelo seleccionado. [cite_start]Los modelos se relacionan con el esfuerzo cortante mediante la expresión $\tau=\rho ghS_{f}$[cite: 95].

### A. Modelo de Manning
[cite_start]Basado en la resistencia dependiente de la velocidad, comúnmente usado en hidráulica convencional[cite: 96, 97]:
$$S_{f}=\frac{n^{2}v^{2}}{h^{4/3}}$$
* [cite_start]**Parámetros:** $n$ (coeficiente de Manning [cite: 117]).

### B. Modelo de Bingham (Simplificado)
[cite_start]Representa fluidos con un umbral de fluencia y viscosidad[cite: 55, 102]:
$$S_{f}=\frac{1}{\rho gh}(\omega\tau_{y}+3\frac{\mu_{B}v}{h})$$
* [cite_start]**Parámetros:** $\tau_{y}$ (esfuerzo de fluencia), $\mu_{B}$ (viscosidad dinámica)[cite: 117].
* [cite_start]**Explicación:** Incorpora tanto el esfuerzo de fluencia como el viscoso para simular comportamientos dinámicos y estáticos[cite: 56].

### C. Modelo de Voellmy
[cite_start]Suma la fricción turbulenta y la fricción seca de tipo Coulomb[cite: 54, 103]:
$$S_{f}=\frac{v^{2}}{\xi h}+\mu$$
* [cite_start]**Parámetros:** $\xi$ (coeficiente de fricción turbulenta), $\mu$ (coeficiente de fricción de Coulomb/basal)[cite: 117].

### D. Modelo Cuadrático (O'Brien y Julien)
[cite_start]Combina términos de fluencia, viscosidad y turbulencia en una ecuación cuadrática[cite: 105, 249]:
$$S_{f}=\frac{\tau_{y}}{\rho gh}+\frac{K\mu_{B}v}{8\rho gh^{2}}+\frac{n^{2}v^{2}}{h^{4/3}}$$
* [cite_start]**Parámetros:** $\tau_{y}, \mu_{B}, n$ y $K$ (parámetro de resistencia)[cite: 117].

### E. Modelo de Herschel-Bulkley
[cite_start]Captura comportamientos no lineales tras superar el esfuerzo de fluencia[cite: 107, 115]:
$$S_{f}=\frac{1}{\rho gh}(\tau_{y}+k(\frac{v}{h})^{a})$$
* [cite_start]**Parámetros:** $\tau_{y}, k$ (consistencia) y $a$ (potencia de corte o "shear power")[cite: 117].

---

## 3. Comparación de Resultados (Caso Popocatépetl)

[cite_start]Se evaluó la reconstrucción del lahar de 2001 en la garganta de Huiloac utilizando un DTM de 15 m[cite: 67, 72].

### Extensión y Depósito
* [cite_start]**Modelos tipo Manning:** Tuvieron un rendimiento deficiente[cite: 30]. [cite_start]Al carecer de términos de resistencia estática, el fluido no se detuvo y continuó fluyendo hasta salir del dominio[cite: 167, 186].
* [cite_start]**Voellmy:** Exhibió la segunda mayor extensión (149 ha) y depósitos de gran profundidad (>5 m) en la zona media-baja[cite: 172].
* [cite_start]**Bingham:** Presentó la extensión más reducida (65 ha), concentrando el flujo en la garganta[cite: 176].
* [cite_start]**O'Brien-Julien y Herschel-Bulkley:** Resultados muy similares entre sí, con extensiones de 74 ha y 88 ha respectivamente[cite: 178].

### Velocidades y Tiempos de Llegada
* [cite_start]**Velocidad:** El modelo de **Manning** llegó en menos de 0:30 h[cite: 181]. [cite_start]**Voellmy** y **Bingham** fueron los más lentos (3:40 - 3:50 h)[cite: 182].
* **Comparación:** Iber-NNF capturó bien la velocidad estimada por Muñoz-Salinas et al. {cite}`parker_2009` [cite_start]en la mayoría de los puntos de control[cite: 187, 189].

---

## 4. Referencias Bibliográficas

* **Bingham, E. C. (1916).** An investigation of the laws of plastic flow. [cite_start]*Bulletin of the Bureau of Standards*, 13(2), 309-353[cite: 425].
* **Bladé, E., Cea, L., Corestein, G., Escolano, E., Puertas, J., Vázquez-Cendón, E., Dolz, J., & Coll, A. (2014a).** Iber: herramienta de simulación numérica del flujo en ríos. [cite_start]*Revista Internacional de Métodos Numéricos Para Cálculo y Diseño En Ingeniería*, 30(1), 1-10[cite: 427].
* **Capra, L., Poblete, M. A., & Alvarado, R. (2004).** The 1997 and 2001 lahars of Popocatépetl volcano (Central Mexico): textural and sedimentological constraints on their origin and hazards. [cite_start]*Journal of Volcanology and Geothermal Research*, 131(3-4), 351-369[cite: 444].
* **Chow, V. Te. (1959).** *Open-Channel Hydraulics*. [cite_start]McGraw-Hill Book Company Inc.[cite: 450].
* **Herschel, W. H., & Bulkley, R. (1926).** Konsistenzmessungen von Gummi-Benzollösungen. [cite_start]*Kolloid-Zeitschrift*, 39(4), 291-300[cite: 487].
* **Muñoz-Salinas, E., Manea, V. C., Palacios, D., & Castillo-Rodriguez, M. (2007).** Estimation of lahar flow velocity on Popocatépetl volcano (Mexico). [cite_start]*Geomorphology*, 92(1-2), 91-99[cite: 513].
* **O'Brien, J. S., & Julien, P. Y. (1988).** Laboratory Analysis of Mudflow Properties. [cite_start]*Journal of Hydraulic Engineering*, 114(8), 877-887[cite: 518].
* **Sanz-Ramos, M., Bladé, E., Diez-Herrero, A., Vázquez-Tarrio, D., Garrote, J., Sánchez, N., & Galindo, I. (2025).** An analysis of rheological models for lahar modelling with Iber. [cite_start]*Revista Mexicana de Ciencias Geológicas*, 42(3), 160-169[cite: 13, 14, 15].
* **Voellmy, A. (1955).** Über die Zerstörungskraft von Lawinen. [cite_start]*Schweizerische Bauzeitung*, 73, 15[cite: 582].