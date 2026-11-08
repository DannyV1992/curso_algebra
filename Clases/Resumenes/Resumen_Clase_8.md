# Clase 7 — Operar y despejar matrices, matriz por vector, producto de matrices y regresión logística con NumPy

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University

**Semana:** 8

**Material fuente:** `1 - Material del curso.pdf` (53 diapositivas, el mismo de las clases 3 a 6), `3 - Guia_Matrices_Operar_Despejar_Multiplicar.pdf` (3 páginas) y el notebook `Practica python.ipynb`

**Cobertura de los PDFs:** *Guía de matrices:* completa (páginas 1 a 3). Se proyectó en clase como apoyo y sus cuatro ejemplos (operar, despejar, matriz por vector y producto de matrices) están en las secciones 1, 2 y 6; los ejercicios «Ahora tú» de la página 3 quedan como práctica. *1 - Material del curso.pdf:* Parcial: diapositivas 39 a 46 de 53 (hasta «Solución de la práctica 11»). La clase anterior terminó en la diapositiva 36. Las diapositivas 37–38 (práctica 9: operar y despejar) no se resolvieron sobre el PDF: esos temas se trabajaron con los ejemplos de la guía y del notebook (sección 1). La diapositiva 51 (laboratorio NumPy) se sustituyó por el notebook de la clase (sección 6). Las diapositivas 47–53 (regresión lineal como proyección ortogonal y cierre) quedan para la siguiente clase.

**Nota sobre las fuentes:** el notebook repite los ejemplos de la guía. Varias cifras de la transcripción salieron mal reconocidas, así que todos los resultados se verificaron contra los dos PDFs y el notebook.

**Contexto.** Última sesión del bloque de matrices. Se completa el álgebra de matrices (operar, despejar, matriz por vector, producto de matrices) y se lleva a Python, donde un caso práctico de IA —predecir la fuga de clientes— usa solo esas operaciones. Idea central: lo que hace una red neuronal por dentro es multiplicar matrices, transponer, restar y escalar.

---

## 1. Operar y despejar matrices (diapositivas 37–38 y guía)

- **Operar:** suma, resta y escalar son entrada por entrada y exigen la misma dimensión. Ejemplo de la guía, con $`A=\begin{bmatrix}2&-1&3\\0&4&-2\end{bmatrix}`$ y $`B=\begin{bmatrix}1&0&-2\\3&-1&4\end{bmatrix}`$: $`2A-3B=\begin{bmatrix}1&-2&12\\-9&11&-16\end{bmatrix}`$ (entrada $(1,1)$: $2\cdot2-3\cdot1=1$).
- **Transpuesta:** cambia filas por columnas; $(A^\top)^\top=A$ y respeta la suma y el escalar, $(A+B)^\top=A^\top+B^\top$ y $`(kA)^\top=kA^\top`$.
- **Simétrica:** $A=A^\top$. Se verifica transponiendo y comparando; no confundirla con la identidad. $`D=\begin{bmatrix}1&2&-3\\2&0&5\\-3&5&4\end{bmatrix}`$ es simétrica porque su transpuesta es igual.
- **Despejar:** se hace como con números (pasar sumando o restando, multiplicar por un escalar), pero **las matrices no se dividen**: en lugar de dividir entre 2 se multiplica por $\tfrac12$.
  - $2X+A=B\Rightarrow X=\tfrac12(B-A)$.
  - $3X-A=X+B\Rightarrow 2X=A+B\Rightarrow X=\tfrac12(A+B)$.
  - Con $`A=\begin{bmatrix}3&1\\-2&4\end{bmatrix}`$ y $`B=\begin{bmatrix}7&5\\2&-6\end{bmatrix}`$ resultan $`X_a=\begin{bmatrix}2&2\\2&-5\end{bmatrix}`$ y $`X_b=\begin{bmatrix}5&3\\0&-1\end{bmatrix}`$.
- Se despeja primero con letras y se sustituye al final; después se **verifica sustituyendo** en la ecuación original.

**Práctica 9 (solo PDF), con** $`C=\begin{bmatrix}2&-1&0\\3&4&1\end{bmatrix}`$ **y** $`D=\begin{bmatrix}1&1&-2\\0&-3&5\end{bmatrix}`$:

| Ejercicio | Resultado |
|-----------|-----------|
| a) $C+D$ | $`\begin{bmatrix}3&0&-2\\3&1&6\end{bmatrix}`$ ($2\times3$) |
| b) $3C-2D$ | $`\begin{bmatrix}4&-5&4\\9&18&-7\end{bmatrix}`$ |
| c) $(C-D)^\top$ | $`\begin{bmatrix}1&3\\-2&7\\2&-4\end{bmatrix}`$, de dimensión $3\times2$ |
| d) $2X+C=D$ | $`X=\tfrac12(D-C)=\begin{bmatrix}-0{,}5&1&-1\\-1{,}5&-3{,}5&2\end{bmatrix}`$ |

---

## 2. Multiplicar una matriz por un vector (diapositivas 39–40)

Une todo lo anterior: cada entrada del resultado es un producto punto y el resultado completo es una combinación lineal.

```math
(A\mathbf{x})_i=\sum_{j=1}^{n}a_{ij}x_j=(\text{fila }i)\cdot\mathbf{x},\qquad A\mathbf{x}=x_1\mathbf{a}_1+x_2\mathbf{a}_2+\cdots+x_n\mathbf{a}_n
```

Aquí $`\mathbf{a}_j`$ es la columna $j$ de $A$.

- **Regla de dimensiones:** $(m\times n)\cdot(n)=(m)$. El número de columnas de $A$ debe ser igual al número de componentes de $\mathbf{x}$, y el resultado tiene tantos componentes como filas tiene $A$. Si $A$ tiene 3 columnas, el vector debe tener 3 componentes (en vertical o en horizontal, da igual); con 27 filas, el resultado tiene 27 componentes. Si no coinciden, el producto no existe.
- **Dos lecturas, el mismo resultado:**
  - *Por filas:* cada fila de $A$ se multiplica componente a componente con $\mathbf{x}$ y se suma.
  - *Por columnas:* cada componente de $\mathbf{x}$ multiplica a su columna (el primero a la primera, y así) y se suman las columnas escaladas.
- **Notación:** el paréntesis denota vector y el corchete denota matriz. El resultado de $A\mathbf{x}$ es un vector y puede escribirse como $(0,3)$, en fila o en columna.
- **Cuadrar en un orden no garantiza cuadrar en el otro:** el producto se evalúa siempre como $A\mathbf{x}$ y la regla se comprueba antes de calcular.

**Ejemplo (diapositiva 40):** con $`A=\begin{bmatrix}2&1\\-1&3\\0&4\end{bmatrix}`$ y $\mathbf{x}=(3,2)$, que cumple $(3\times2)\cdot(2)=(3)$:

- Por filas: $(2\cdot3+1\cdot2,\ -1\cdot3+3\cdot2,\ 0\cdot3+4\cdot2)=(8,3,8)$.
- Por columnas: $`3\begin{bmatrix}2\\-1\\0\end{bmatrix}+2\begin{bmatrix}1\\3\\4\end{bmatrix}=\begin{bmatrix}6\\-3\\0\end{bmatrix}+\begin{bmatrix}2\\6\\8\end{bmatrix}=\begin{bmatrix}8\\3\\8\end{bmatrix}`$.
- En ciencia de datos, $\hat{\mathbf{y}}=X\mathbf{w}$: $X$ guarda los datos (una fila por observación) y $\mathbf{w}$ los pesos, de modo que un solo producto predice todas las observaciones. La **columna de unos** en $X$ es la que da al modelo un intercepto (con $\mathbf{w}=(20;\ 1{,}5)$ y áreas 50, 80 y 120 m², las predicciones son 95, 140 y 200).
- **Una capa de red neuronal es $A\mathbf{x}$:** si $A$ es $2\times3$, hay 2 neuronas y 3 entradas, y cada fila de $A$ contiene los pesos de una neurona. Con $`A=\begin{bmatrix}2&-1&3\\4&0&5\end{bmatrix}`$ y $\mathbf{x}=(1,2,-1)$: $A\mathbf{x}=(-3,-1)$.

---

## 3. Práctica 10: productos matriz-vector (diapositivas 41–42)

Con $`A=\begin{bmatrix}1&-2&0\\3&1&4\end{bmatrix}`$ y $\mathbf{x}=(2,1,-1)$:

| Ejercicio | Resolución | Resultado |
|-----------|------------|-----------|
| a) Dimensiones | $A$ es $2\times3$ y $\mathbf{x}\in\mathbb{R}^3$: las 3 columnas coinciden con los 3 componentes | El producto existe y es un vector de $\mathbb{R}^2$ |
| b) Por filas y por columnas | Filas: $(2-2+0,\ 6+1-4)$. Columnas: $`2\begin{bmatrix}1\\3\end{bmatrix}+1\begin{bmatrix}-2\\1\end{bmatrix}-1\begin{bmatrix}0\\4\end{bmatrix}`$ | Ambas dan $A\mathbf{x}=(0,3)$ ✓ |
| c) ¿Existe $A$ por $(1,2)$? | $A$ tiene 3 columnas y el vector 2 componentes: no cumple la regla | **No existe** |
| d) Predicción con $\mathbf{w}=(3;\ 0{,}5)$ y $`X=\begin{bmatrix}1&2\\1&5\\1&7\end{bmatrix}`$ | $(3+0{,}5\cdot2,\ 3+0{,}5\cdot5,\ 3+0{,}5\cdot7)$ | $\hat{\mathbf{y}}=(4;\ 5{,}5;\ 6{,}5)$ |

- En (d) los pesos son dos números (3 y 0,5), no tres: coinciden con las 2 columnas de $X$, así que el producto sí existe.
- **Pesos y predicción:** una predicción multiplica cada dato por su peso y suma. Al inicio de una red neuronal los pesos se inicializan de forma aleatoria y luego se ajustan con base en el aprendizaje del modelo, buscando reducir el error de predicción (sección 7).

---

## 4. Multiplicar matrices: filas por columnas (diapositivas 43–44)

El producto $AB$ aplica «matriz por vector» a cada columna de $B$; cada entrada del resultado es un producto punto:

```math
A_{m\times n}B_{n\times p}=C_{m\times p},\qquad c_{ij}=\sum_{k=1}^{n}a_{ik}b_{kj}=(\text{fila }i\text{ de }A)\cdot(\text{columna }j\text{ de }B)
```

- **Dimensiones:** los números de adentro deben coincidir ($n$ con $n$) y los de afuera dan el tamaño del resultado ($m\times p$). Las dimensiones internas desaparecen.
- **Procedimiento:** calcular las entradas en orden —$(1,1)$, $(1,2)$, $(2,1)$, $(2,2)$—, cada una como una fila por una columna, y **al final** armar la matriz del resultado con corchetes (no con paréntesis ni comas, que son de vectores).

| Propiedad | Enunciado | Qué recordar |
|-----------|-----------|--------------|
| **No conmutativa** | $AB\neq BA$ en general | Cambiar el orden altera el producto; a veces una de las dos ni existe. Es la única regla de los números que se pierde |
| Asociativa | $(AB)C=A(BC)$ | Se puede agrupar de distinta forma sin cambiar el orden de las matrices |
| Distributiva | $A(B+C)=AB+AC$ | Se puede sumar y luego multiplicar, o al revés |
| Identidad | $AI=IA=A$ | La identidad actúa como el 1 |
| Transpuesta del producto | $(AB)^\top=B^\top A^\top$ | **Se invierte el orden** |

- Entender el porqué de cada regla (por qué no conmuta, por qué asocia, por qué distribuye) es la clave para resolver bien los exámenes: son reglas de juego, y cada estructura matemática cumple las suyas.
- La no conmutatividad se comprueba con cualquier par de matrices de entradas distintas: al invertir el orden, cada posición del resultado combina entradas diferentes.

**Ejemplo (diapositiva 44):** con $`A=\begin{bmatrix}1&2\\3&4\end{bmatrix}`$ y $`B=\begin{bmatrix}0&1\\1&0\end{bmatrix}`$:

- $`c_{11}=1\cdot0+2\cdot1=2`$, $`c_{12}=1\cdot1+2\cdot0=1`$, $`c_{21}=3\cdot0+4\cdot1=4`$, $`c_{22}=3\cdot1+4\cdot0=3`$, luego $`AB=\begin{bmatrix}2&1\\4&3\end{bmatrix}`$.
- $`BA=\begin{bmatrix}3&4\\1&2\end{bmatrix}\neq AB`$. Multiplicar por la derecha por $B$ intercambia las **columnas** de $A$; por la izquierda intercambia las **filas**.
- Cuando las dos matrices tienen el mismo número de entradas pero distinto orden (por ejemplo $2\times3$ y $3\times2$), $AB$ y $BA$ ni siquiera tienen el mismo tamaño.

---

## 5. Práctica 11: producto de matrices (diapositivas 45–46)

Con $`A=\begin{bmatrix}2&0&1\\-1&3&2\end{bmatrix}`$ ($2\times3$) y $`B=\begin{bmatrix}1&2\\0&-1\\4&1\end{bmatrix}`$ ($3\times2$):

| Ejercicio | Resultado |
|-----------|-----------|
| a) Dimensiones | $(2\times3)(3\times2)=2\times2$ para $AB$; $(3\times2)(2\times3)=3\times3$ para $BA$ |
| b) $AB$ | Entrada $(1,1)$: $2\cdot1+0\cdot0+1\cdot4=6$. Resultado: $`\begin{bmatrix}6&5\\7&-3\end{bmatrix}`$ |
| c) $BA$ | $`\begin{bmatrix}0&6&5\\1&-3&-2\\7&3&6\end{bmatrix}`$. Como tienen distinto tamaño, $AB=BA$ es imposible |
| d) $(AB)^\top=B^\top A^\top$ | $`B^\top A^\top=\begin{bmatrix}6&7\\5&-3\end{bmatrix}=(AB)^\top`$ ✓ |

La transpuesta de un producto es el producto de las transpuestas **en orden inverso**; con $A$ y $B$ de $2\times3$ y $3\times2$ se ve también en las dimensiones, $(2\times3)(3\times2)$ para $B^\top A^\top$ igual que el tamaño de $(AB)^\top$.

---

## 6. Matrices en NumPy (notebook de la clase)

El notebook repite en Python los mismos ejemplos de la guía. Las computadoras son el mejor lugar para estudiar el comportamiento de las matrices.

```python
A = np.array([[2, -1, 3],
              [0,  4, -2]])   # una matriz = lista de filas
A.shape        # (2, 3): filas x columnas
A[1, 2]        # a_23 = -2  (Python cuenta desde 0)
A[0, :]        # fila 1;  A[:, 2] columna 3
A.T            # transpuesta
A @ x          # producto matriz-vector;  A @ B producto de matrices
np.allclose(2*Xa + A, B)   # verificar un despeje
```

- **Índices:** en matemáticas $`a_{ij}`$ cuenta desde 1; en Python desde 0, por lo que $`a_{23}`$ es `A[1, 2]`.
- **`*` no es `@`:** `A * B` multiplica entrada por entrada (producto de Hadamard); el producto de matrices se escribe `A @ B`.
- Sumar matrices de distinto tamaño produce un error, igual que en matemáticas.
- Para ver la no conmutatividad con $`P=\begin{bmatrix}1&2\\3&4\end{bmatrix}`$ y $`Q=\begin{bmatrix}0&1\\1&0\end{bmatrix}`$: $PQ$ intercambia las columnas de $P$ y $QP$ intercambia sus filas.

---

## 7. Caso práctico de IA: predecir la fuga de clientes

Una empresa quiere predecir si un cliente abandona el servicio (1) o se queda (0) a partir de tres variables: **meses** de antigüedad, **compras** del último trimestre y **quejas**. Se usa **regresión logística**: la neurona más simple de una red neuronal, que clasifica entre 0 y 1 como una probabilidad.

| Paso | Fórmula | Operación de matrices |
|------|---------|-----------------------|
| Datos | $X$ de $n\times3$ | cada fila es un cliente y cada columna una variable |
| Predicción | $`z=X\mathbf{w}+b`$ | matriz por vector, más el sesgo (*bias*) |
| Probabilidad | $`p=\sigma(z)=\dfrac{1}{1+e^{-z}}`$ | función sigmoide: oscila entre 0 y 1 |
| Gradiente | $`g=\tfrac1n X^\top(p-y)`$ | transpuesta, producto, resta y escalar |
| Actualización | $`\mathbf{w}\leftarrow\mathbf{w}-\eta g`$ | resta de vectores y escalar |

- **Estandarizar** cada columna (restar su media y dividir entre su desviación estándar) para que las escalas sean comparables. Si las compras están en millones y la antigüedad en decenas, la variable de mayor escala recibiría un peso desproporcionado aunque la antigüedad pueda ser igual de importante. Estandarizar acerca los datos sin hacerlos iguales.
- **Punto de partida:** con todos los pesos en 0, la probabilidad es 0,5 para todos los clientes: equivale a lanzar una moneda.
- **Pérdida** (entropía cruzada): mide cuánto se equivoca el modelo. **Descenso del gradiente:** algoritmo de optimización que busca el mínimo local de la función de error, es decir, la combinación de pesos con menor error. $X^\top$ es $3\times n$ y $(p-y)$ tiene $n$ componentes, así que $g$ tiene 3 componentes, uno por peso.
- Los saltos son grandes al inicio (el modelo está lejos de la respuesta) y cada vez más pequeños al acercarse al mínimo. $\eta$ es la **tasa de aprendizaje** y cada repetición del ciclo es una **época**.
- **Resultado tras 200 épocas** ($\eta=0{,}5$): la pérdida baja de 0,693 a 0,412 y la exactitud pasa de 0,5 a 0,80 (matriz de confusión $`\begin{bmatrix}138&26\\34&102\end{bmatrix}`$, con filas = clase real y columnas = clase predicha). Pesos aprendidos: meses $-1{,}56$, compras $-0{,}68$, quejas $+1{,}67$, sesgo $\approx-0{,}23$.

**Interpretación de los pesos** (en unidades estandarizadas): un peso negativo reduce la probabilidad de fuga y uno positivo la aumenta.

| Variable | Peso | Lectura |
|----------|------|---------|
| Meses | $-1{,}56$ | a más antigüedad, menos probabilidad de fuga |
| Compras | $-0{,}68$ | a más compras, menos probabilidad de fuga |
| Quejas | $+1{,}67$ | a más quejas, más probabilidad de fuga (relación directa) |

- **Predecir un cliente nuevo:** es una fila más, estandarizada con la **misma** media y desviación del entrenamiento. Con 60 meses, 3 compras y 4 quejas la probabilidad de fuga es de unos 12 %; con 50 meses, 30 compras y 10 quejas sube a 81 %, es decir, un cliente con muchas quejas se pierde aunque compre y lleve tiempo.
- Cada fila de $A$ es una neurona, el producto punto es la predicción y los pesos se ajustan con la transpuesta, el producto, la resta y el escalar: es la actualización «$W-\eta\bar G$» del Quiz 1.
- **Ejercicios del notebook** (propuestos): la tasa de aprendizaje cambia la velocidad de la curva de pérdida; agregar una cuarta variable convierte $X$ en $n\times4$ y a $\mathbf{w}$ y $g$ en vectores de 4 componentes.

---

## Conceptos clave

- **Despejar matrices:** igual que con números, pero nunca se divide entre una matriz; se multiplica por escalares ($\tfrac12$) y se pasa sumando o restando. Verificar sustituyendo.
- **$A\mathbf{x}$:** requiere columnas de $A$ = componentes de $\mathbf{x}$; el resultado tiene tantos componentes como filas. Por filas son productos punto y por columnas es una combinación lineal; ambas lecturas dan lo mismo.
- **$AB$:** $(m\times n)(n\times p)=(m\times p)$; entrada $(i,j)$ = fila $i$ de $A$ por columna $j$ de $B$.
- **Propiedades del producto:** no conmutativo; asociativo; distributivo; identidad; $(AB)^\top=B^\top A^\top$.
- **NumPy:** `@` es el producto matricial y `*` es entrada por entrada; los índices empiezan en 0.
- **Predicción con pesos:** $\hat{\mathbf{y}}=X\mathbf{w}$; cada fila de una capa de red neuronal son los pesos de una neurona.
- **Descenso del gradiente:** $\mathbf{w}\leftarrow\mathbf{w}-\eta g$ con $`g=\tfrac1n X^\top(p-y)`$; minimiza el error ajustando los pesos.
- **Signo de un peso:** negativo reduce la probabilidad de la clase 1 y positivo la aumenta (con variables estandarizadas).

---

## Fuera del PDF — logística, tareas y metodología

- **Material en el campus:** el notebook de Python (matrices paso a paso, hasta el caso de IA), la guía práctica de matrices (PDF de tres páginas con tres reglas, cuatro ejemplos resueltos paso a paso y ejercicios «Ahora tú» con respuestas; conviene seguirla paso por paso) y tres videos del canal *Dot CSV* sobre regresión lineal, descenso del gradiente y, como extra, redes neuronales. El notebook de Python está hecho en Colab y se sube al campus.
- **Práctica en casa 3 (evaluada):** se entrega el próximo martes; más de la mitad es en Python (en Colab).
- **Examen y prácticas anteriores:** quedan revisados esta semana (a más tardar el jueves o el viernes). Quien no presentó el examen por una causa justificada pide la reposición por correo; se habilita por 24 horas.
- **Por qué entender el álgebra:** las matrices son la base de las redes neuronales, los *transformers* (la base práctica de los GPT) y las redes convolucionales para imágenes. Programar con ayuda de IA no elimina la necesidad de entender qué ocurre por debajo, sobre todo en sistemas a escala empresarial; las evaluaciones buscan comprender por qué se puede multiplicar un vector por una matriz y cómo eso se usa en IA.
