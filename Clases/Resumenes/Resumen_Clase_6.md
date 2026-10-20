# Clase 6 — Matrices: lectura, transpuesta, tipos especiales y operaciones básicas

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University\
**Semana:** 5\
**PDF fuente:** `Material del curso.pdf` (53 diapositivas, el mismo de las clases 3, 4 y 5)\
**Cobertura del PDF:** Parcial: diapositivas 26 a 36 de 53 (hasta «Operar matrices entrada por entrada»). La clase anterior terminó en la diapositiva 25. Las diapositivas 26 a 30 (solución de la práctica 6 y proyección ortogonal) **no se trabajaron en la sesión** y se incluyen brevemente desde el PDF (sección 1). Las diapositivas 37–38 (práctica 9: operar y despejar matrices) y 39–40 en adelante (matriz por vector, producto de matrices, regresión) quedan para la siguiente clase.

**Contexto.** Se abre el bloque de matrices, el concepto más relevante del curso para la inteligencia artificial: un dataset completo es una matriz, y las operaciones de la clase (sumar, escalar, transponer) son las mismas que con vectores, aplicadas entrada por entrada. Las matrices no son nuevas, pero son la base de gráficos 3D, hojas de cálculo, imágenes y redes neuronales.

---

## 1. Práctica 6 resuelta y proyección ortogonal (diapositivas 26–30, solo PDF)

**Solución de la práctica 6:**

| Ejercicio | Resultado |
|-----------|-----------|
| a) Ángulo entre $(3,4)$ y $(4,3)$ | $\mathbf{u}\cdot\mathbf{v}=24$, $\lVert\mathbf{u}\rVert=\lVert\mathbf{v}\rVert=5$, $\cos\theta=24/25=0{,}96\Rightarrow\theta\approx16{,}26^\circ$ |
| b) ¿$(1,-2,3)\perp(4,5,2)$? | $4-10+6=0$: sí son ortogonales |
| c) $k$ para $(k,3)\perp(2,-6)$ | $2k-18=0\Rightarrow k=9$ |
| d) Ángulo entre $(1,0)$ y $(-1,1)$ | Producto $`=-1<0`$ (obtuso); $\cos\theta\approx-0{,}707\Rightarrow\theta=135^\circ$ |

**Proyección ortogonal.** Proyectar $\mathbf{u}$ sobre $\mathbf{v}$ responde: ¿cuál es la mejor aproximación de $\mathbf{u}$ usando solo la dirección de $\mathbf{v}$? Se busca el múltiplo $`c\,\mathbf{v}`$ que deja el residuo $`\mathbf{r}=\mathbf{u}-c\,\mathbf{v}`$ perpendicular a $\mathbf{v}$:

```math
(\mathbf{u}-c\mathbf{v})\cdot\mathbf{v}=0\ \Rightarrow\ c=\frac{\mathbf{u}\cdot\mathbf{v}}{\mathbf{v}\cdot\mathbf{v}},\qquad \text{proj}_{\mathbf{v}}\mathbf{u}=\frac{\mathbf{u}\cdot\mathbf{v}}{\mathbf{v}\cdot\mathbf{v}}\,\mathbf{v},\qquad \mathbf{r}=\mathbf{u}-\text{proj}_{\mathbf{v}}\mathbf{u}
```

- Procedimiento en tres pasos: calcular $c$, multiplicar $`c\,\mathbf{v}`$, restar para obtener el residuo. Comprobación: $\mathbf{r}\cdot\mathbf{v}=0$; si no da cero, hay un error de cálculo.
- Ejemplo: $\mathbf{u}=(2,3)$ sobre $\mathbf{v}=(1,1)$ → $c=5/2=2{,}5$, proyección $`(2{,}5;\,2{,}5)`$, residuo $`(-0{,}5;\,0{,}5)`$, y $\mathbf{r}\cdot\mathbf{v}=0$ ✓.
- $\mathbf{u}=\text{proyección}+\text{residuo perpendicular}$. La distancia de $\mathbf{u}$ a la recta de $\mathbf{v}$ es $\lVert\mathbf{r}\rVert$.
- **Conexión con regresión:** la proyección es la parte explicada por el modelo y el residuo es el error. Proyectar sobre $(1,1,\dots,1)$ reemplaza cada dato por el promedio (el modelo más simple): $\mathbf{u}=(1,2,3)$ da $c=2$.

---

## 2. Qué es una matriz, desde cero (diapositiva 31)

Una matriz organiza muchos vectores a la vez, **vectores que comparten la misma estructura**, unidos en una tabla rectangular de números. Es la forma natural de guardar un dataset completo.

- **Analogía:** el cubo de Rubik. Un cubo de una sola fila sería un vector; el de $2\times2$ y el de $3\times3$ son matrices. Se mide en **filas y columnas** (primero filas), no como largo por ancho.
- **Matriz $m\times n$:** $m$ filas y $n$ columnas; todas sus entradas son reales, $A\in\mathbb{R}^{m\times n}$. En matrices muy grandes se escriben solo las esquinas con puntos suspensivos.

```math
A=\begin{bmatrix}a_{11}&a_{12}&\cdots&a_{1n}\\ \vdots&\vdots&\ddots&\vdots\\ a_{m1}&a_{m2}&\cdots&a_{mn}\end{bmatrix}
```

- **Notación de posición:** $`a_{ij}`$ = primero la fila $i$, después la columna $j$. Así, $`a_{23}`$ está en la fila 2, columna 3. Se escribe entre corchetes cuadrados.
- **En datos:** cada fila es una **observación** (un vector) y cada columna es una **variable**. Un dataset de 1 000 clientes y 8 variables es una matriz $`1\,000\times8`$. Las hojas de Excel y los CSV son matrices, y también las imágenes (píxeles) y los mundos de los videojuegos 3D.
- **Las filas (y las columnas) son vectores**, por eso todo lo visto de vectores se traslada a matrices.

### Transpuesta

```math
(A^\top)_{ij}=a_{ji}
```

- Intercambia filas por columnas, conservando el orden: una matriz $m\times n$ pasa a ser $n\times m$.
- Se escribe $A^\top$ (o $A^T$).

### Tipos especiales de matrices

| Tipo | Condición | Ejemplo |
|------|-----------|---------|
| Cuadrada | $m=n$ (mismas filas que columnas) | $`\begin{bmatrix}2&7\\-1&0\end{bmatrix}`$ |
| Identidad $`I_n`$ | Unos en la diagonal y ceros fuera | $`I_3=\begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix}`$ |
| Diagonal | Ceros fuera de la diagonal (en la diagonal puede ir cualquier número) | $`\begin{bmatrix}4&0\\0&9\end{bmatrix}`$ |
| Simétrica | $A=A^\top$ | $`\begin{bmatrix}1&5\\5&3\end{bmatrix}`$ |

- **Identidad $`I_n`$:** el subíndice indica solo la dimensión. Si piden $`I_4`$, se dibuja una matriz $4\times4$ con cuatro unos en la diagonal y ceros alrededor; no se eligen otros números.
- **Ejemplo de diagonal de unos:** la matriz de correlación de un conjunto de variables tiene unos en la diagonal, porque cada variable se correlaciona perfectamente consigo misma. Además es simétrica.
- **Simétrica:** al transponer queda exactamente igual; equivale a $`a_{ij}=a_{ji}`$ para todo par de posiciones. Solo puede ocurrir en matrices cuadradas.

---

## 3. Leer entradas, filas, columnas y transpuestas (diapositiva 32)

Antes de operar hay que leer la matriz con precisión, en este orden:

1. **Dimensión:** contar filas y columnas.
2. **Entradas:** ubicar $`a_{ij}`$ (fila primero, columna después).
3. **Filas y columnas completas**, escritas como vectores.

Ejemplo con $`A=\begin{bmatrix}2&-1&0\\5&3&7\end{bmatrix}`$: es $2\times3$; $`a_{12}=-1`$; $`a_{23}=7`$; la fila 2 es $(5,3,7)$ (una observación) y la columna 3 es $(0,7)$ (una variable).

### Cómo transponer

- La primera fila pasa a ser la primera columna, la segunda fila la segunda columna, y así sucesivamente. Así, $`A^\top=\begin{bmatrix}2&5\\-1&3\\0&7\end{bmatrix}`$ ($3\times2$).
- **Error común:** pensar que transponer es "darle vuelta" invirtiendo el orden de los números (leer $7,4,3$ en lugar de $3,4,7$). Eso es incorrecto: el orden de cada fila se conserva y solo cambia su orientación.
- Una matriz simétrica se reconoce comparando con su transpuesta. En matrices pequeñas basta ver que no cambió; en matrices grandes se verifica entrada por entrada ($`s_{12}=s_{21}`$, etc.).
- Un vector columna puede escribirse en forma vertical u horizontal; ambas se aceptan.

### ¿Para qué transponer?

- **Imágenes y redes neuronales convolucionales:** los píxeles forman matrices, y rotar o transponer permite al modelo aprender a leer una imagen desde varias perspectivas (por eso el reconocimiento facial pide mover el rostro).
- **Regresión lineal por mínimos cuadrados:** transponer la matriz de datos alinea las dimensiones para multiplicar matrices.
- **Redes y grafos:** la transpuesta de una matriz de adyacencia invierte el sentido de las relaciones o flujos.
- **Generación procedural de terreno (p. ej. videojuegos):** usa configuraciones de matrices para crear relieves distintos.

---

## 4. Práctica 8: leer y transponer matrices (diapositivas 33–34)

Con $`B=\begin{bmatrix}3&0&-2&1\\4&6&5&-1\\7&-3&8&2\end{bmatrix}`$ y $`C=\begin{bmatrix}2&1\\3&2\end{bmatrix}`$:

| Ejercicio | Resolución | Resultado |
|-----------|------------|-----------|
| a) Dimensión y entradas | 3 filas y 4 columnas | $B$ es $3\times4$; $`b_{23}=5`$, $`b_{31}=7`$, $`b_{14}=1`$ |
| b) Fila 2 y columna 3 como vectores | Se leen de la matriz | Fila 2 $=(4,6,5,-1)$: una observación con 4 variables. Columna 3 $=(-2,5,8)$: una variable medida en 3 observaciones |
| c) $B^\top$ | Cada fila de $B$ se escribe como columna, en el mismo orden | $`B^\top=\begin{bmatrix}3&4&7\\0&6&-3\\-2&5&8\\1&-1&2\end{bmatrix}`$, de dimensión $4\times3$ |
| d) ¿$C$ es simétrica? $`I_3`$ | $`c_{12}=1\neq c_{21}=3`$, o sea $C\neq C^\top$ | $C$ **no** es simétrica; $`I_3`$ es la identidad $3\times3$ |

- La dimensión se invierte al transponer: $3\times4\to4\times3$.
- Para declarar que una matriz no es simétrica se escribe $C\neq C^\top$.
- En NumPy: `B.T` es la transpuesta y `B.shape` es la dimensión.

---

## 5. Operaciones con matrices: sumar, escalar y transponer (diapositivas 35–36)

Son exactamente las de vectores, **entrada por entrada**:

```math
(A+B)_{ij}=a_{ij}+b_{ij},\qquad (kA)_{ij}=k\,a_{ij}
```

- Solo se suman (o restan) matrices de la **misma dimensión**; la entrada $(i,j)$ del resultado usa únicamente las entradas $(i,j)$ de las originales. Las reglas de signos son las de siempre.
- Las matrices $m\times n$ forman un **espacio vectorial**: cumplen los 8 axiomas (conmutativa, asociativa, neutro —la matriz cero—, opuesto, distributivas e identidad). Todo lo aprendido de vectores, incluido el despeje, vale para matrices.
- Orden de trabajo: primero escalar, luego sumar o restar.

### Propiedades de la transpuesta

| Propiedad | Significado |
|-----------|-------------|
| $(A^\top)^\top=A$ | Transponer dos veces devuelve la matriz original |
| $(A+B)^\top=A^\top+B^\top$ | Da igual sumar y luego transponer, o transponer y luego sumar |
| $`(kA)^\top=k\,A^\top`$ | Da igual escalar y luego transponer, o al revés |

### Ejemplo resuelto: $`A=\begin{bmatrix}1&2\\3&4\end{bmatrix}`$, $`B=\begin{bmatrix}0&-1\\5&2\end{bmatrix}`$

- $`A+B=\begin{bmatrix}1&1\\8&6\end{bmatrix}`$ y $`2A-B=\begin{bmatrix}2&4\\6&8\end{bmatrix}-\begin{bmatrix}0&-1\\5&2\end{bmatrix}=\begin{bmatrix}2&5\\1&6\end{bmatrix}`$ (nótese $4-(-1)=5$).
- **Verificación de $(A+B)^\top=A^\top+B^\top$:** ambos lados dan $`\begin{bmatrix}1&8\\1&6\end{bmatrix}`$ ✓. Una verificación numérica ilustra la propiedad; la demostración general se hace con la notación $`a_{ij}`$.

---

## Conceptos clave

- **Matriz $m\times n$:** tabla rectangular de números; $m$ filas, $n$ columnas; $`a_{ij}`$ = fila $i$, columna $j$. En datos: filas = observaciones, columnas = variables.
- **Dimensión o *shape*:** se lee primero filas, luego columnas.
- **Transpuesta:** $`(A^\top)_{ij}=a_{ji}`$; cada fila pasa a ser columna sin cambiar su orden; $m\times n\to n\times m$.
- **Tipos:** cuadrada ($m=n$), identidad $`I_n`$ (unos en la diagonal, ceros fuera), diagonal (ceros fuera de la diagonal), simétrica ($A=A^\top$).
- **Suma y escalar:** entrada por entrada; solo con la misma dimensión; las matrices forman un espacio vectorial.
- **Propiedades de la transpuesta:** $(A^\top)^\top=A$, $(A+B)^\top=A^\top+B^\top$, $(kA)^\top=kA^\top$.
- **Proyección ortogonal (PDF):** $`\text{proj}_{\mathbf{v}}\mathbf{u}=\frac{\mathbf{u}\cdot\mathbf{v}}{\mathbf{v}\cdot\mathbf{v}}\mathbf{v}`$; el residuo siempre es perpendicular a $\mathbf{v}$.

---

## Fuera del PDF — logística, tareas y metodología

- **Quiz:** queda asignado; se dispone de una semana (unos 8 días) para resolverlo y entregarlo. Se recomienda hacerlo a conciencia: la primera prueba se parecerá mucho a él. Las consultas sobre el quiz se hacen por escrito al docente, que orienta pero no da las respuestas.
- **Primera prueba (el martes de la semana siguiente):** cubre vectores y matrices, hasta lo visto en esta clase. Durará unas 2 horas y después se dedican 25–30 minutos a material nuevo.
- **Enfoque de la prueba:** no son ejercicios mecánicos paso a paso, sino **comprender problemas, interpretar resultados y opinar**. Una respuesta generada por IA saldrá demasiado genérica y se notará.
- **Tarea de 10 ejercicios** publicada la semana anterior: el plazo llega hasta el jueves. Las tareas se dejan por una semana (unos 8 días hábiles).
- **Material en el campus:** video de matemáticas del canal *Derivando* sobre las matrices (aplicaciones en el mundo real, origen y funcionamiento), extractos de lectura y un notebook de Python. Otro video, más explicativo, se envía también por WhatsApp.
- **Encuesta de medio periodo:** se responde en el campus (evaluación intermedia del curso).
- **Visión del curso:** la IA está cambiando la forma de hacer matemática; lo que más valor tiene es entender el lenguaje matemático, interpretar procesos y respuestas, y la creatividad para plantear, resolver y aplicar problemas. De ahí el enfoque aplicado del curso.
- **Próxima clase:** completar las operaciones con matrices (práctica 9: operar y despejar matrices), seguir con **matriz por vector**, producto de matrices (filas por columnas), regresión lineal y proyecciones, acercándose cada vez más a lo que ocurre en la inteligencia artificial. Python irá entrando de forma progresiva una vez asentada la base teórica.
