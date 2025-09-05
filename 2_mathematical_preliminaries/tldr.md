
## **1. Derivadas Parciales y el Gradiente**

Antes de hablar del descenso de gradiente, es crucial entender las **derivadas parciales** y el concepto de **gradiente**.

* **Derivadas Parciales:** Para una función con varias variables (como nuestra $f(x_1, x_2)$), una derivada parcial mide la tasa de cambio de la función con respecto a una de esas variables, manteniendo las otras constantes. Imagina que estás en una montaña y quieres saber qué tan empinada es la pendiente si solo te mueves hacia el este (manteniendo tu posición norte-sur constante). Esa es la idea de una derivada parcial.
    * La notación para la derivada parcial de la función $f$ con respecto a $x_1$ es $\frac{\partial f}{\partial x_1}$.
    * Por ejemplo, para nuestra función $f(x_1, x_2) = \sin(x_1)\cos(x_2) + \sin(0.5x_1)\cos(0.5x_2)$, la derivada parcial con respecto a $x_1$ es:
        $$\frac{\partial f}{\partial x_1} = \cos(x_1)\cos(x_2) + 0.5\cos(0.5x_1)\cos(0.5x_2)$$

* **El Gradiente ($\nabla f$):** El gradiente es un vector que contiene todas las derivadas parciales de una función. Es, en esencia, la dirección de mayor ascenso en la superficie de la función. Si la función tiene $n$ variables, el gradiente será un vector de $n$ dimensiones.
    * Para nuestra función $f(x_1, x_2)$, el gradiente es:
        $$\nabla f(x_1, x_2) = \begin{bmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \end{bmatrix}$$
        

---


## **2. Descenso de Gradiente (Gradient Descent)**

El **descenso de gradiente** es el algoritmo de optimización más fundamental en el aprendizaje automático. Su objetivo es encontrar el valor mínimo de una función, a menudo una **función de pérdida** que mide el error de un modelo. La intuición detrás del algoritmo es sencilla: para encontrar el fondo de un valle, debemos dar pasos en la dirección opuesta a la pendiente más pronunciada. 

### **Conceptos Clave**

* **Función de Costo o Pérdida ($J(\theta)$):** Es la función que queremos minimizar. Toma los parámetros del modelo ($\theta$) como entrada y produce un valor escalar que representa el "costo" o "error" del modelo.
* **Gradiente ($\nabla J(\theta)$):** Es un vector de derivadas parciales que apunta en la dirección de máximo ascenso de la función. Para bajar, nos movemos en la dirección opuesta, es decir, $-\nabla J(\theta)$.
* **Tasa de Aprendizaje ($\alpha$):** Un hiperparámetro crucial que determina el tamaño de cada paso.
    * Si $\alpha$ es muy pequeña, la convergencia es lenta.
    * Si $\alpha$ es muy grande, el algoritmo puede "saltar" sobre el mínimo o incluso diverger.

### **Pseudocódigo y Proceso**

El algoritmo es un proceso iterativo que se repite hasta que se alcanza una condición de parada (por ejemplo, un número máximo de iteraciones o cuando el gradiente es muy pequeño).

1.  **Inicialización:** Elige un punto de partida aleatorio para tus parámetros, $\theta_{0}$.
2.  **Bucle de Actualización:** Repite para $i = 1, 2, 3, ...$
    * Calcula el gradiente en la posición actual: $\nabla J(\theta_{i-1})$.
    * Actualiza los parámetros:
        $$\theta_i = \theta_{i-1} - \alpha \cdot \nabla J(\theta_{i-1})$$

---

## **3. Descenso de Gradiente con Momento (Momentum)**

El descenso de gradiente básico puede ser lento y oscilar en "valles" estrechos. El **momento** es una técnica que resuelve este problema al darle inercia a nuestro proceso de optimización. 

La idea es que si los pasos anteriores se movieron en una dirección similar, el algoritmo gana impulso y acelera, lo que le permite deslizarse a través de las irregularidades de la superficie de la función. Es como una pelota rodando cuesta abajo: su velocidad no solo depende de la pendiente actual, sino también de la velocidad que traía de antes.

### **Conceptos Clave**

* **Tasa de Momento ($\beta$):** Un hiperparámetro que determina cuánta "inercia" se transfiere de un paso al siguiente. Típicamente, se usa un valor como 0.9. Un valor más alto significa más inercia y pasos más suaves.
* **Velocidad ($v_t$):** Un nuevo vector que acumula el promedio ponderado de los gradientes pasados y la velocidad anterior. La velocidad es la que se usa para actualizar la posición.

### **Pseudocódigo y Proceso**

1.  **Inicialización:** Elige un punto de partida $\theta_{0}$ y una velocidad inicial $v_0 = 0$.
2.  **Bucle de Actualización:** Repite para $i = 1, 2, 3, ...$
    * Calcula el gradiente: $\nabla J(\theta_{i-1})$.
    * Actualiza la velocidad:
        $$v_i = \beta v_{i-1} + \alpha \nabla J(\theta_{i-1})$$
    * Actualiza los parámetros:
        $$\theta_i = \theta_{i-1} - v_i$$

---

## **4. La Norma del Gradiente ($\| \nabla J(\theta) \|$)**

La **norma del gradiente** es la magnitud o longitud del vector gradiente. Es una herramienta poderosa para analizar el progreso de nuestro algoritmo de optimización.

### **Conceptos Clave**

* **¿Qué nos dice?**
    * Una **norma alta** indica que la pendiente es muy pronunciada y estamos lejos de un mínimo local.
    * Una **norma baja** significa que la pendiente es plana y estamos cerca de un punto crítico (un mínimo, un máximo o un punto de silla).
* **Convergencia:** A medida que el descenso de gradiente se acerca a un mínimo, la norma del gradiente se reduce y tiende a cero. Al graficarla a lo largo de las iteraciones, podemos visualizar la velocidad de convergencia: una caída más rápida de la norma significa que el algoritmo es más eficiente.
* **Cálculo:** Se calcula como la norma euclidiana (o L2) del gradiente. Por ejemplo, en 2D:
    $$\| \nabla J(\theta) \| = \sqrt{(\frac{\partial J}{\partial \theta_1})^2 + (\frac{\partial J}{\partial \theta_2})^2}$$

