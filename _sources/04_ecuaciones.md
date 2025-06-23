# Ecuaciones de Saint-Venant

Para modelar flujos de escombros (debris flows) y otros flujos geofísicos, se emplean un conjunto de ecuaciones de conservación que derivan de la mecánica de fluidos y medios continuos. Las ecuaciones de Saint-Venant son una forma simplificada y promediada en profundidad de las ecuaciones de Navier–Stokes. Se utilizan para modelar flujos superficiales como ríos, avalanchas, lahares y debris flows. Estas ecuaciones resuelven la dinámica del flujo considerando solo las variaciones en el plano horizontal (x,y), y promediando las variables a lo largo de la vertical (z), lo que simplifica mucho el problema sin perder lo esencial.

Comparado con aguas limpias, los flujos de lodo y detritos generan fuerzas resistentes adicionales. El aumento del contenido de sólidos incrementa la viscosidad de los flujos no newtonianos, generando fuerzas resistentes internas dentro del fluido. A concentraciones más altas, particularmente con partículas gruesas, la colisión y fricción entre partículas introducen fuerzas resistentes internas adicionales. La mayoría de las modificaciones teóricas y numéricas implican la integración de las nuevas fuerzas internas del fluido en la ecuación de momento. Las ecuaciones promediadas en la profundidad pueden adaptarse para simulaciones no newtonianas añadiendo un término de pendiente de pérdida adicional ($S_{MD}$) al término clásico de la pendiente de fricción ($S_f$) en la ecuación de conservación de momento.

En este sentido, los modelos numéricos para flujos de ladera suelen usar las ecuaciones de Saint-Venant adaptadas a flujos no newtonianos, en forma de conservación de masa y momento en 1D o 2D de la siguiente forma:


### Ecuación de conservación de masa (Continuidad)
Para un flujo en una dirección horizontal (e.g. coordenada $x$), la ecuación de continuidad superficial en régimen no permanente es:


$\frac{\partial h}{\partial t} + \frac{\partial(ℎ\vec{u})}{\partial x} = 𝑆_m$

 
Donde: $h(x,t)$: espesor del flujo [m], $\vec{u}(x,t)$: velocidad media del flujo [m/s], $S_m$: fuente o pérdida de masa (por ejemplo, aporte de afluentes, erosión, infiltración) [m/s]

Esta ecuación dice que el cambio del espesor en el tiempo es igual a la diferencia entre lo que entra y lo que sale, más lo que se gana o pierde localmente.

### Ecuación de conservación de cantidad de movimiento (momento lineal)
Esta ecuación representa el balance entre fuerzas propulsoras (gravedad) y resistencias (fricción basal, turbulencia, etc.). En dos dimensiones se extiende a vectores de velocidad $\vec{u} = (u,v)$, y aparecen términos de curvatura, presión lateral y coriolis si es relevante.

$\frac{\partial(h\vec{u})}{\partial t} + \frac{\partial(h\vec{u}^2)}{\partial x} = 𝑔 hsen⁡\theta − S_{MD} + 𝑆_f$  

$S_{MD}=\frac{\tau_{MD}}{\rho_mgR}$

​ 
Donde: $g$: gravedad, $\theta$: pendiente del terreno, $S_{MD}$: pendiente de fricción para lodos y escombros, $S_f$: pendiente de fricción newtoniana o pendiente de fricción viscosa, $\tau_{MD}$ el esfuerzo cortante interno y reológico, $\rho_m$ la densidad dela mezcla de sedimentos y agua ($kg/m^3$) y $R$ el radio hidráulico (m). la Pendiente de fricción para lodos y escombros ($S_{MD}$) se refiere a la resistencia al movimiento introducida por la fricción interna y basal de materiales no newtonianos, como mezclas de lodo, escombros o flujos hiperconcentrados, que pueden tener comportamientos viscoplásticos o de tipo Bingham. La Pendiente de fricción newtoniana $S_f$ se refiere a la componente del modelo que representa las fuerzas de fricción o resistencia debidas a un comportamiento fluido tipo Newtoniano (como el agua o fluidos con viscosidad constante). 

Generalmente los modelos son simplificados (usan solo la ecuación de momento), tales como algunos modelos empíricos o semi-analíticos, algunos modelos usados para estimar alcance máximo o zona de detención (por ejemplo, el método de "box model" o modelos de trayectoria pura). Usan solo Fuerza neta = masa⋅aceleración. Se considera una masa movilizada fija, y se analiza cómo frena con diferentes mecanismos (fricción basal, turbulencia). A veces se reduce a un problema 1D con:

$𝑚\frac{\partial\vec{u}}{\partial t}=𝑚𝑔sin𝜃−𝜏_𝑏$  
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
