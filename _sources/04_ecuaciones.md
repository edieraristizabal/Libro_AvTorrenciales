# Ecuaciones de Saint-Venant

Para modelar flujos de escombros (debris flows) y otros flujos geofísicos, se emplean un conjunto de ecuaciones de conservación que derivan de la mecánica de fluidos y medios continuos. Estas incluyen principalmente:

* Conservación de masa

* Conservación de cantidad de movimiento

* Conservación (o balance) de energía

## Forma integrada: ecuaciones tipo Saint-Venant
Las ecuaciones de Saint-Venant son una forma simplificada y promediada en profundidad de las ecuaciones de Navier–Stokes. Se utilizan para modelar flujos superficiales como ríos, avalanchas, lahares y debris flows. Estas ecuaciones resuelven la dinámica del flujo considerando solo las variaciones en el plano horizontal (x,y), y promediando las variables a lo largo de la vertical (z), lo que simplifica mucho el problema sin perder lo esencial.

Los modelos numéricos para flujos de ladera suelen usar las ecuaciones de Saint-Venant adaptadas a flujos no newtonianos, en forma de conservación de masa y momento en 1D o 2D:

$\frac{\partial h}{\partial t} + \triangledown(ℎ\vec{u}) = 𝑆_m$


$\frac{\partial(h \vec{u})}{\partial t }+ \triangledown(ℎ\vec{u} \otimes \vec{u}) = −g h \triangledown z_b+ \vec{S}_g − \frac{\vec{\tau}_b }{\rho} $
​
 
Términos clave: $z_b$: elevación del lecho (topografía), $\vec{\tau}_b$: esfuerzo basal según el modelo reológico (puede ser Bingham, Voellmy, etc.), $\vec{S}_g$: fuerzas externas (por ejemplo, presiones dispersivas, sobrepresión de poros)


### Ecuación de conservación de masa (Continuidad)
Para un flujo en una dirección horizontal (e.g. coordenada $x$), la ecuación de continuidad superficial en régimen no permanente es:


$\frac{\partial ℎ}{\partial t}+ \frac{\partial(hu)}{\partial x}=𝑆_m$  

 
Donde: $h(x,t)$: espesor del flujo [m], $u(x,t)$: velocidad media del flujo [m/s], $S_m$: fuente o pérdida de masa (por ejemplo, aporte de afluentes, erosión, infiltración) [m/s]

Esta ecuación dice que el cambio del espesor en el tiempo es igual a la diferencia entre lo que entra y lo que sale, más lo que se gana o pierde localmente.

### Ecuación de conservación de cantidad de movimiento (momento lineal)
Esta ecuación representa el balance entre fuerzas propulsoras (gravedad) y resistencias (fricción basal, turbulencia, etc.). En dos dimensiones se extiende a vectores de velocidad $\vec{u} = (u,v)$, y aparecen términos de curvatura, presión lateral y coriolis si es relevante.

$\frac{\partial(hu)}{\partial t} + \frac{\partial(hu^2)}{\partial x} = 𝑔 hsin⁡\theta − \tau_b / \rho + 𝑆_f$  

​ 
Donde: $g$: gravedad, $\theta$: pendiente del terreno, $\tau_b$: esfuerzo cortante basal [Pa] (resistencia al movimiento), $\rho$: densidad del flujo, 
$S_f$: otras fuerzas (presiones de poro, colisiones, etc.).


### Ecuación de conservación de energía (forma general)
La forma general del balance de energía para un flujo continuo es:

$\frac{𝑑}{𝑑𝑡}(𝐸_{total})=$ Potencia neta de entrada − Disipación  

Desglose de la energía total por unidad de masa:

$𝐸=𝐸_𝑝+𝐸_𝑘+𝐸_𝑖$​  
 
$E_p = g z$ → energía potencial (por altura), $E_k = \frac{1}{2} u^2$ → energía cinética, $E_i$ → energía interna (p. ej., calor, deformación interna, presión de poros), La disipación de energía aparece como términos negativos (resistencias), y depende del modelo reológico:

Viscoso: $\Phi = \mu (\partial u/\partial y)^2$

Dispersivo: término $\propto \dot\gamma^2$

Turbulento: términos como $\propto V^2/\xi$ en Voellmy


generalmente los modelos son simplificados (usan solo la ecuación de momento), tales como algunos modelos empíricos o semi-analíticos, algunos modelos usados para estimar alcance máximo o zona de detención (por ejemplo, el método de "box model" o modelos de trayectoria pura). Usan solo Fuerza neta = masa⋅aceleración. Se considera una masa movilizada fija, y se analiza cómo frena con diferentes mecanismos (fricción basal, turbulencia). A veces se reduce a un problema 1D con:

$𝑚\frac{𝑑u}{𝑑t}𝑡=𝑚𝑔sin𝜃−𝜏_𝑏$  
​
 
Pero si se requiere simular procesos dinámicos completos, como: evolución del espesor del flujo, deposición progresiva, erosión basal, bifurcaciones de cauce, es obligatorio usar ambas ecuaciones de Saint-Venant.

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
