# Clase 5 — Sistemas 2×2, producto punto, norma, ángulo y ortogonalidad

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University\
**Semana:** 4\
**PDFs fuente:** `Clase 5 - guia sistemas 2x2.pdf` (7 páginas) y `Material del curso.pdf` (53 diapositivas, el mismo de las clases 3 y 4)\
**Cobertura de los PDFs:**
- *Guía de sistemas 2×2:* completa (páginas 1 a 7). En clase solo se resolvió el ejercicio 1; los ejercicios 2 y 3 salen únicamente del PDF y quedaron como práctica.
- *Clase 3 y 4.pdf:* Parcial: diapositivas 21 a 25 de 53 (hasta «Práctica 6: ángulos y ortogonalidad», que se deja de tarea). Las diapositivas 19–20 (producto punto) se repasaron al inicio. La diapositiva 26 (solución de la práctica 6) y la proyección ortogonal (27–30) no se trabajaron y quedan para la siguiente clase; matrices (31 en adelante) también.

**Contexto.** Se cierra el bloque de vectores: primero se resuelve a mano el sistema de dos ecuaciones que aparece al buscar coeficientes de una combinación lineal, y luego se completa el producto punto con la norma, el ángulo entre vectores y la ortogonalidad. Después viene matrices.

---

## 1. Sistemas 2×2 por suma (guía de la clase)

Cuando se buscan $`c_1`$ y $`c_2`$ tales que $`c_1\mathbf{v}_1+c_2\mathbf{v}_2=\mathbf{w}`$, **cada componente del vector da una ecuación**: dos incógnitas, dos igualdades. Es el mismo problema de la clase anterior (¿$\mathbf{w}$ está en el generado?), ahora con el método resuelto en detalle.

### ¿Por qué se pueden sumar dos igualdades?

```math
A=B \ \text{ y } \ C=D \ \Longrightarrow\ A+C=B+D
```

- Es como sumar lo mismo a ambos lados de una balanza equilibrada: sigue equilibrada. Es una propiedad (axioma) de la igualdad.
- También se vale multiplicar una igualdad **completa** (ambos lados) por un número distinto de cero (p. ej. 3 o $-1$) para "preparar" la cancelación.
- Objetivo de sumar: hacer **desaparecer una incógnita** y quedar con una sola ecuación de una sola variable (ecuación en una variable), que se despeja con álgebra normal.

### Método en 5 pasos

| # | Paso | Qué se hace |
|---|------|-------------|
| 1 | Plantear | Escribir $`c_1\mathbf{v}_1+c_2\mathbf{v}_2=\mathbf{w}`$ con los vectores del enunciado |
| 2 | Separar por componentes | Primera componente → ecuación (1); segunda → ecuación (2) |
| 3 | Preparar y sumar | Lograr coeficientes opuestos en una incógnita, sumar y despejar la otra |
| 4 | Sustituir | Reemplazar el valor hallado en una ecuación original y despejar la segunda incógnita |
| 5 | Verificar | Calcular $`c_1\mathbf{v}_1+c_2\mathbf{v}_2`$ y comprobar que da exactamente $\mathbf{w}$ |

### Ejercicio 1 (resuelto en clase): $\mathbf{w}=(5,1)$, $`\mathbf{v}_1=(1,1)`$, $`\mathbf{v}_2=(1,-1)`$

```math
c_1(1,1)+c_2(1,-1)=(5,1)\ \Rightarrow\ \begin{cases}c_1+c_2=5\\ c_1-c_2=1\end{cases}
```

- El signo menos de $`c_2`$ viene de que la segunda componente de $`\mathbf{v}_2`$ es $-1$; si fuera $+1$, la ecuación llevaría $`+c_2`$.
- Se suman las ecuaciones **término a término** (cada $`c_1`$ con $`c_1`$, cada $`c_2`$ con $`c_2`$, y los lados derechos entre sí): $`2c_1+0=6\Rightarrow c_1=3`$.
- Si una letra aparece sola, su coeficiente es 1 ($`c_1+c_1=2c_1`$): regla básica del álgebra.
- Sustituir en (1): $`3+c_2=5\Rightarrow c_2=2`$.
- Verificación: $3(1,1)+2(1,-1)=(3,3)+(2,-2)=(5,1)$ ✓. Resultado: $`\mathbf{w}=3\mathbf{v}_1+2\mathbf{v}_2`$.
- Multiplicar los coeficientes por los vectores y sumar siempre produce un $\mathbf{w}$: ese conjunto de resultados alcanzables es el **generado**.

### ¿Qué hago antes de sumar? (ejercicios 2 y 3 de la guía)

| Situación | Acción | Ejemplo de la guía |
|-----------|--------|--------------------|
| Coeficientes opuestos ($`+c_2`$ y $`-c_2`$) | Sumar directamente | Ej. 1 |
| Coeficientes de distinto tamaño ($`3c_2`$ y $`-c_2`$) | Multiplicar una ecuación para igualar tamaños con signo opuesto | Ej. 2: $\mathbf{w}=(10,6)$, $`\mathbf{v}_1=(1,2)`$, $`\mathbf{v}_2=(3,-1)`$ → multiplicar (2) por 3 → $`c_1=4,\ c_2=2`$ |
| Mismo coeficiente y mismo signo ($`+c_2`$ y $`+c_2`$) | Multiplicar una ecuación por $-1$ | Ej. 3: $\mathbf{w}=(4,7)$, $`\mathbf{v}_1=(2,3)`$, $`\mathbf{v}_2=(1,1)`$ → $`c_1=3,\ c_2=-2`$ |

- **Errores comunes:** multiplicar solo un lado de la ecuación (se multiplica todo, incluido el lado derecho); sumar sin haber preparado la cancelación (la incógnita se duplica en vez de desaparecer).
- Un coeficiente negativo es válido: el vector se usa en sentido contrario.
- Siempre: sustituir en una ecuación **original** y verificar al final.

---

## 2. Producto punto: repaso y nuevas ideas (diapositivas 19–20)

Se multiplica posición por posición y se suma: $`\mathbf{u}\cdot\mathbf{v}=\sum u_iv_i`$. Ejemplo: $\mathbf{u}=(2,-1,3)$, $\mathbf{v}=(4,5,-2)$ → $8-5-6=-3$. Propiedades: conmutativa, distributiva, saca escalares y positividad (ver clase 4).

- **Dimensiones:** el producto punto solo se define entre vectores de la **misma dimensión**.
- **Es la base de la predicción:** los pesos $`\mathbf{w}=(0{,}5;\,2;\,-1)`$ y la observación $\mathbf{x}=(10,3,4)$ dan $\hat y=\mathbf{w}\cdot\mathbf{x}=5+6-4=7$. Ambos vectores deben tener el mismo número de componentes: un peso por cada variable.

### Cómo se obtienen los pesos (contexto de IA)

- Ejemplo: predecir una cardiopatía a partir de variables (diabetes, hipertensión, obesidad, sedentarismo, tabaquismo…). El resultado a predecir es la **variable objetivo** (*target*) y las demás son las predictoras.
- En una red neuronal los pesos **empiezan aleatorios** y se ajustan con los datos de entrenamiento mediante *backpropagation*, una función de pérdida y **descenso de gradiente** (que busca un mínimo local del error). Los define el modelo, no una persona.
- Lo que sí hace una persona es el **etiquetado de datos**, que suele ser lo más costoso.
- Un peso puede ser negativo (p. ej. hacer ejercicio reduce el riesgo). Su valor depende del problema y de los datos de entrenamiento: una misma variable puede pesar distinto según la población estudiada.
- La salida de la predicción depende de la escala de las variables y de los pesos aprendidos con esa escala.

### Escalado de variables

- Si una variable tiene valores enormes (p. ej. una calificación de 1 a 100 000 junto a otras de 1 a 10), el modelo le asigna una importancia desproporcionada.
- Dos compradores con hábitos muy parecidos pueden verse "muy diferentes" solo por el monto gastado (50 000 vs. 1 000 000): el modelo los separa por la magnitud, no por la característica.
- Solución: **escalar** con herramientas como `StandardScaler` de scikit-learn, que detecta valores extremos y lleva todo a una escala comparable.

```python
from sklearn.preprocessing import StandardScaler
X_escalado = StandardScaler().fit_transform(X)
```

---

## 3. Práctica 5: calcular y verificar propiedades (diapositivas 21–22)

Con $\mathbf{a}=(1,2,-3)$, $\mathbf{b}=(4,-1,2)$, $\mathbf{c}=(0,3,1)$. Escribir los productos parciales antes de sumarlos hace visible el error.

| Ejercicio | Procedimiento | Resultado |
|-----------|---------------|-----------|
| a) $\mathbf{a}\cdot\mathbf{b}$ y $\mathbf{b}\cdot\mathbf{c}$ | $4-2-6$ y $0-3+2$ | $-4$ y $-1$ |
| b) $\mathbf{a}\cdot\mathbf{a}$ y $\lVert\mathbf{a}\rVert$ | $1+4+9=14$, luego $\sqrt{14}$ | $\lVert\mathbf{a}\rVert\approx 3{,}742$ |
| c) Distributiva | $\mathbf{b}+\mathbf{c}=(4,2,3)$; $\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=4+4-9=-1$ y $\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}=-4+3=-1$ | $-1=-1$ ✓ |
| d) $(2\mathbf{a})\cdot\mathbf{b}$ de dos maneras | Escalando: $(2,4,-6)\cdot(4,-1,2)=8-4-12$; propiedad 3: $2(\mathbf{a}\cdot\mathbf{b})=2(-4)$ | $-8=-8$ ✓ |

- **Error frecuente (a):** $\mathbf{b}\cdot\mathbf{c}$ es $-1$, no $+1$; el signo se arrastra del producto parcial negativo.
- La distributiva es la misma de siempre del álgebra: las propiedades permiten reutilizar productos ya calculados.
- **Notación:** $\mathbf{a}\cdot\mathbf{a}$ no es "$\mathbf{a}^2$" del álgebra de números; se escribe como producto punto. Elevar al cuadrado cada componente y sumar equivale a $\mathbf{a}\cdot\mathbf{a}$.

### Norma euclidiana

```math
\lVert\mathbf{v}\rVert=\sqrt{\mathbf{v}\cdot\mathbf{v}}=\sqrt{v_1^2+v_2^2+\cdots+v_n^2}
```

- Se elevan los componentes al cuadrado, se suman y se saca la raíz. Es el teorema de Pitágoras generalizado a $n$ dimensiones.
- La norma es una **longitud (distancia desde el origen)**, siempre positiva. Es la positividad de la propiedad 4.
- Ejemplos: $\lVert(4,-1,2)\rVert=\sqrt{16+1+4}=\sqrt{21}$; $\lVert(0,3,1)\rVert=\sqrt{0+9+1}=\sqrt{10}$.
- Es la **distancia euclidiana**, la más común (la del plano cartesiano del colegio). Es la que usan algoritmos de agrupamiento como KNN y K-means.

---

## 4. Ángulo y ortogonalidad (diapositivas 23–24)

El producto punto se calcula con sumas y productos, pero guarda información geométrica: el ángulo entre los vectores.

### Fundamento: ley de cosenos

En el triángulo formado por $\mathbf{u}$, $\mathbf{v}$ y $\mathbf{u}-\mathbf{v}$:

```math
\lVert\mathbf{u}-\mathbf{v}\rVert^2=\lVert\mathbf{u}\rVert^2+\lVert\mathbf{v}\rVert^2-2\lVert\mathbf{u}\rVert\lVert\mathbf{v}\rVert\cos\theta
```

Expandiendo el lado izquierdo con el producto punto: $`(\mathbf{u}-\mathbf{v})\cdot(\mathbf{u}-\mathbf{v})=\lVert\mathbf{u}\rVert^2-2\,\mathbf{u}\cdot\mathbf{v}+\lVert\mathbf{v}\rVert^2`$. Igualando ambas expresiones y cancelando queda la fórmula del ángulo:

```math
\cos\theta=\frac{\mathbf{u}\cdot\mathbf{v}}{\lVert\mathbf{u}\rVert\,\lVert\mathbf{v}\rVert}
```

- Lo que importa **aprender** es esta fórmula; la deducción con la ley de cosenos es el porqué, no hace falta memorizarla.
- $\theta$ es el ángulo que forman dos vectores que parten del mismo punto. Funciona igual en muchas dimensiones, aunque no se pueda visualizar.

### El signo del producto punto da el tipo de ángulo

| $\mathbf{u}\cdot\mathbf{v}$ | Ángulo $\theta$ | Tipo |
|----------------------------|-----------------|------|
| $`>0`$ | $`<90^\circ`$ | Agudo |
| $=0$ | $=90^\circ$ | Recto (**ortogonales**) |
| $`<0`$ | $`>90^\circ`$ | Obtuso |

- El signo se conoce **antes** de calcular $\theta$.
- Ojo: un coseno de 0,707 es positivo, y el ángulo correspondiente (45°) es agudo. Lo que decide el tipo es el signo del producto punto; para ser obtuso el ángulo tiene que superar los 90°.

### Ortogonalidad

```math
\mathbf{u}\perp\mathbf{v}\iff\mathbf{u}\cdot\mathbf{v}=0
```

- Ortogonales = los vectores **no comparten ninguna dirección**. No hace falta calcular raíces ni ángulos para decidirlo.
- Interpretación aplicada: ángulo cercano a 0° → vectores que se comportan de forma parecida (base para formar clústers); 90° → producto punto cero, no comparten información, no hay relación entre ellos.
- Es la idea que sostiene PCA y la regresión.

### Ejemplos resueltos (diapositiva 24)

**1. Ángulo entre $\mathbf{u}=(1,1)$ y $\mathbf{v}=(1,0)$.**
- $\mathbf{u}\cdot\mathbf{v}=1\cdot1+1\cdot0=1$; $\lVert\mathbf{u}\rVert=\sqrt2$, $\lVert\mathbf{v}\rVert=1$.
- $\cos\theta=\dfrac{1}{\sqrt2\cdot1}\approx0{,}707\Rightarrow\theta=\arccos(0{,}707)=45^\circ$ (agudo, como anticipaba el signo $+1$).

**2. Forzar la ortogonalidad:** ¿qué $k$ hace que $(2,k,1)\perp(3,-1,4)$?
- Se iguala el producto punto a cero y se despeja: $6-k+4=0\Rightarrow k=10$.
- Verificación: $(2,10,1)\cdot(3,-1,4)=6-10+4=0$ ✓. Queda una ecuación de primer grado.

---

## 5. Práctica 6: ángulos y ortogonalidad (diapositiva 25)

Cuatro ejercicios, **evaluados** (ver tareas). Calculadora solo para el arcocoseno; el resto a mano, dejando visibles los productos:

- a) Ángulo entre $(3,4)$ y $(4,3)$: coseno exacto y ángulo en grados.
- b) ¿Son ortogonales $(1,-2,3)$ y $(4,5,2)$? Justificar con un solo cálculo.
- c) Hallar $k$ para que $(k,3)\perp(2,-6)$ y verificar.
- d) Ángulo entre $(1,0)$ y $(-1,1)$; predecir por el signo si será agudo u obtuso antes de calcular.

---

## Conceptos clave

- **Sumar igualdades:** $A=B$ y $C=D\Rightarrow A+C=B+D$; sirve para eliminar una incógnita. Si no se cancela, se multiplica una ecuación completa (por un número o por $-1$) y luego se suma.
- **Método 2×2:** plantear, separar por componentes, preparar y sumar, sustituir, verificar.
- **Producto punto:** da un escalar; solo entre vectores de la misma dimensión; $\hat y=\mathbf{w}\cdot\mathbf{x}$.
- **Pesos:** en una red neuronal arrancan aleatorios y los ajusta el entrenamiento; escalar las variables evita que una magnitud grande domine.
- **Norma euclidiana:** $\lVert\mathbf{v}\rVert=\sqrt{\mathbf{v}\cdot\mathbf{v}}$; longitud siempre positiva; viene de Pitágoras.
- **Ángulo:** $\cos\theta=\dfrac{\mathbf{u}\cdot\mathbf{v}}{\lVert\mathbf{u}\rVert\lVert\mathbf{v}\rVert}$.
- **Signo del producto punto:** $`>0`$ agudo, $=0$ recto, $`<0`$ obtuso.
- **Ortogonalidad:** $\mathbf{u}\cdot\mathbf{v}=0$; para exigirla se iguala a cero y se despeja.

---

## Fuera del PDF — logística, tareas y metodología

- **Verificación de subespacio (práctica 4, ejercicio d):** $`S=\{(x,2x)\}`$ es la recta $y=2x$ por el origen. Contiene al cero, es cerrado bajo la suma ($(a,2a)+(b,2b)=(a+b,2(a+b))$) y bajo los escalares (la recta pasa por el origen, así que escalar no saca el vector de ella). Por tanto es subespacio de $\mathbb{R}^2$. El docente muestra una visualización interactiva en HTML (vectores editables, 30 casos de prueba y explicación de qué es un subespacio) que se sube al campus virtual.
- **Práctica de repaso (no evaluada):** 10 ejercicios sobre vectores (concepto, dimensión, suma, resta, escalares); las hojas de respuesta se publican el viernes.
- **Práctica 6 (evaluada):** los 4 ejercicios de la diapositiva 25; se entrega a los 3 días.
- **Material en el campus:** guía de sistemas 2×2, el archivo HTML del subespacio y videos de repaso. La presentación completa ya está subida; se estudia hasta la diapositiva 30.
- **Próxima clase:** se inicia con matrices (qué es una matriz, de qué está hecha, para qué sirve; el cubo de Rubik como ejemplo de matriz 3×3), con vistas a regresión lineal a mano y, después, redes neuronales. Habrá quiz de lo visto y la primera prueba cubre vectores y matrices.
- **Asistencia:** las ausencias y llegadas tarde se justifican por WhatsApp o correo; conviene revisar el correo por si se registra una ausencia por error.
- **Recomendación:** preguntar todas las dudas y practicar a mano, dejando cada paso escrito.
