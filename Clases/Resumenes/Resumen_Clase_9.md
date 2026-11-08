# Clase 9 — Matrices en acción: transformaciones, espacio columna y nulo, y rango

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University

**Semana:** 9

**Material fuente:** `4 - Matrices en accion.pdf` (37 diapositivas; el pie de las diapositivas dice «Clase 7», pero es la presentación de esta sesión), una página HTML interactiva de rango y nulidad y un video sobre rango.

**Cobertura del PDF:** Parcial: diapositivas 1 a 14 de 37 (hasta «Rango: solución paso a paso»). Cubre el bloque 1 hasta rango. Las diapositivas 15 a 36 (sobredeterminados y colinealidad, y todo el bloque 2: vectorización, matrices dispersas, complejidad y *benchmarking*) quedan para la siguiente clase; la diapositiva 37 es el cierre de toda la presentación. En clase se resolvieron sobre el PDF las prácticas de transformaciones (diapositivas 5 y 6). De las diapositivas 7 a 14, el espacio columna y nulo se explicó con los ejemplos de la diapositiva 8 y el rango se trabajó con una página interactiva; los ejemplos y las prácticas de las diapositivas 9, 10 y 12 a 14 no se resolvieron en clase y aquí salen solo del PDF.

**Nota sobre las fuentes:** la transcripción es la fuente principal. Tiene cifras y fórmulas mal reconocidas, sobre todo en rango y nulidad (la definición de rango y la relación rango–nulidad salían al revés); los cálculos se verificaron contra el PDF. Tanto el audio como la diapositiva 7 dicen que Nul(A) vive en el espacio de salida; es el espacio de **entrada**, como muestra el propio dibujo de la diapositiva, y así se anota aquí.

**Contexto.** Se cierra el material de matrices pasando de la mecánica del cálculo a su significado geométrico: una matriz es una función que mueve el espacio. Todo lo que se calcula ya se vio; lo nuevo es ver qué hace cada operación. La presentación (37 diapositivas, pensada para dos clases) sigue «de la geometría al rendimiento» y se divide en dos bloques: el **bloque 1** (transformaciones y espacios: transformaciones, espacio columna y nulo, rango, sobredeterminados y colinealidad) y el **bloque 2** (cómputo matricial y rendimiento).

- Las matrices son las estructuras en las que están escritas las reglas de los modelos (regresión lineal, regresión logística, redes neuronales); entenderlas es entender qué hay detrás del concepto.
- **La visión geométrica es clave en ciencia de datos e IA**, porque así es como la computadora ve las matrices. Ejemplo: una máquina de soporte vectorial separa linealmente dos clases; si no son separables, el truco del *kernel* sube los datos a más dimensiones (por ejemplo a 3) y allí se aplica el corte. Por eso los ejercicios y las explicaciones HTML del curso son muy geométricos.

---

## 1. Transformaciones: una matriz es una función que mueve el espacio (diapositivas 3–6)

### Explicación (diapositiva 3)

- $A\mathbf{x}$ toma un vector y lo lleva a otro: la matriz $A$ es la regla de movimiento. Multiplicar por $A$ transforma **todo el plano a la vez**. La matriz transforma al vector, nunca al revés.
- **Las columnas lo dicen todo.** Basta ver adónde caen $`\mathbf{e}_1=(1,0)`$ y $`\mathbf{e}_2=(0,1)`$: caen en la primera y la segunda columna de $A$.

```math
A\mathbf{e}_1=\mathbf{a}_1,\qquad A\mathbf{e}_2=\mathbf{a}_2,\qquad A\mathbf{x}=x_1\mathbf{a}_1+x_2\mathbf{a}_2
```

  Aquí $`\mathbf{a}_j`$ es la columna $j$ de $A$. Con $`A=\begin{bmatrix}2&1\\0&3\end{bmatrix}`$: $`A\mathbf{e}_1=(2,0)`$ y $`A\mathbf{e}_2=(1,3)`$. Dos matrices que mandan $`\mathbf{e}_1`$ y $`\mathbf{e}_2`$ a los mismos lugares son la misma transformación.

| Transformación | Matriz | Efecto |
|----------------|--------|--------|
| Original | $`\begin{bmatrix}1&0\\0&1\end{bmatrix}`$ | No cambia nada |
| **Escala** | $`\begin{bmatrix}2&0\\0&0{,}5\end{bmatrix}`$ | Duplica $`x`$ y reduce $`y`$ a la mitad |
| **Rotación 90°** | $`\begin{bmatrix}0&-1\\1&0\end{bmatrix}`$ | Gira el plano; la longitud no cambia |
| **Reflexión** | $`\begin{bmatrix}-1&0\\0&1\end{bmatrix}`$ | Cambia el signo de $`x`$ (efecto espejo) |
| **Cizalla** (inclinar) | $`\begin{bmatrix}1&1\\0&1\end{bmatrix}`$ | Desplaza la parte superior y deja fija la base |

**Tres propiedades:** las rectas siguen siendo rectas; el origen no se mueve (lo que se mueve es el espacio); el producto aplica las transformaciones **una tras otra**: $AB$ aplica primero $B$ y luego $A$.

- **Cómo anticipar el efecto sin calcular:** un 2 en la matriz indica que escala; un signo que cambia (o un cero que reemplaza un valor negativo) indica que cambia la orientación, es decir, que refleja o rota. Con práctica se identifica a simple vista.
- **Por qué importa:** una pantalla es una matriz enorme de píxeles, y las imágenes y los videojuegos se calculan con millones de polígonos y transformaciones de matrices. Por eso la GPU, especialista en operar matrices, es tan valiosa.

### Ejemplos resueltos (diapositiva 4)

1. **Aplicar una matriz a un vector.** Con $`A=\begin{bmatrix}2&1\\0&3\end{bmatrix}`$ y $\mathbf{x}=(1,2)$: fila 1: $2\cdot1+1\cdot2=4$; fila 2: $0\cdot1+3\cdot2=6$, luego $A\mathbf{x}=(4,6)$. El vector queda estirado.
2. **Rotar 90° a la izquierda.** Con $`R=\begin{bmatrix}0&-1\\1&0\end{bmatrix}`$ y $\mathbf{x}=(3,1)$: $R\mathbf{x}=(0\cdot3-1\cdot1,\ 1\cdot3+0\cdot1)=(-1,3)$. Las columnas de $R$ son $(0,1)$ y $(-1,0)$, y la longitud se conserva: $`\|\mathbf{x}\|=\|R\mathbf{x}\|=\sqrt{10}`$.
3. **El orden importa.** Con $R$ la rotación y $`S=\begin{bmatrix}2&0\\0&1\end{bmatrix}`$ la escala en $x$:

```math
RS=\begin{bmatrix}0&-1\\2&0\end{bmatrix}\qquad SR=\begin{bmatrix}0&-2\\1&0\end{bmatrix}
```

   $RS$ **escala y luego rota**; $SR$ rota y luego escala. Con $\mathbf{x}=(1,1)$: $RS\mathbf{x}=(-1,2)$ y $SR\mathbf{x}=(-2,1)$, así que $RS\neq SR$. Por eso el producto no conmuta ni valen las costumbres de la escuela: «cualquier migaja dentro de una matriz afecta el resultado completo». El algoritmo de siempre sigue valiendo (fila por columna), con matrices de cualquier tamaño.

### Práctica y solución (diapositivas 5–6)

**Problema 1.** Con $`A=\begin{bmatrix}0&1\\1&0\end{bmatrix}`$ y $\mathbf{x}=(3,5)$, calcular $A\mathbf{x}$ y decir qué le hace $A$ a cualquier vector $(x,y)$.

- $A\mathbf{x}=(0\cdot3+1\cdot5,\ 1\cdot3+0\cdot5)=(5,3)$. En general $A(x,y)=(y,x)$: **intercambia las coordenadas**.
- Como $`\mathbf{e}_1\to(0,1)`$ y $`\mathbf{e}_2\to(1,0)`$, los dos ejes se intercambian: es una **reflexión sobre la recta** $y=x$.

**Problema 2.** Escribir la matriz que estira $x$ por 3 y cambia el signo de $y$, y aplicarla a $\mathbf{x}=(2,4)$.

- Las columnas son las imágenes de la base: $`\mathbf{e}_1\to(3,0)`$ y $`\mathbf{e}_2\to(0,-1)`$.

```math
A=\begin{bmatrix}3&0\\0&-1\end{bmatrix},\qquad A\mathbf{x}=(3\cdot2,\ (-1)\cdot4)=(6,-4)
```

- La primera fila produce la nueva $x$ (aquí el estiramiento) y la segunda la nueva $y$ (aquí el reflejo); los ceros evitan que una coordenada afecte a la otra. La **posición** de cada número importa: $`\begin{bmatrix}0&3\\-1&0\end{bmatrix}`$ tiene los mismos valores pero da $(12,-2)$.
- Si el enunciado pidiera estirar $y$ y reflejar $x$, el 3 iría en la segunda fila y el $-1$ en la primera.

**Problema 3 (cizalla).** Aplicar $`A=\begin{bmatrix}1&2\\0&1\end{bmatrix}`$ a los vértices $(0,0)$, $(1,0)$, $(1,1)$ y $(0,1)$ y dibujar la figura.

- Como $A$ manda rectas a rectas, **basta transformar los vértices**. Se escriben como columnas de una matriz y se multiplica una sola vez:

```math
\begin{bmatrix}1&2\\0&1\end{bmatrix}\begin{bmatrix}0&1&1&0\\0&0&1&1\end{bmatrix}=\begin{bmatrix}0&1&3&2\\0&0&1&1\end{bmatrix}
```

- Las imágenes son $(0,0)$, $(1,0)$, $(3,1)$ y $(2,1)$: un **paralelogramo**. La base queda fija y el «techo» se corre 2 unidades.

---

## 2. Espacio columna y espacio nulo: qué produce A y qué destruye (diapositivas 7–10)

### Explicación (diapositiva 7)

Dos subespacios cuentan toda la historia de una matriz.

- **Espacio columna** $\mathrm{Col}(A)$: todas las salidas posibles de $A$, es decir, las combinaciones lineales de sus columnas. Vive en el espacio de llegada (en los ejemplos, $\mathbb{R}^2$ a $\mathbb{R}^2$ y la entrada y la salida comparten espacio).
- **Espacio nulo** $\mathrm{Nul}(A)$: los $\mathbf{x}$ con $A\mathbf{x}=\mathbf{0}$, las entradas que $A$ anula. Si solo contiene el $\mathbf{0}$, $A$ **no pierde información**.
- $A\mathbf{x}=\mathbf{b}$ tiene solución exactamente cuando $\mathbf{b}$ está en $\mathrm{Col}(A)$.
- Un cero en la matriz «apaga» el efecto de esa posición: por eso en el problema 2 se ponen ceros.

### Ejemplos resueltos (diapositiva 8)

| Caso | Matriz | Resultado |
|------|--------|-----------|
| **1. Columnas proporcionales** | $`A=\begin{bmatrix}1&2\\2&4\end{bmatrix}`$, con $`\mathbf{c}_2=2\mathbf{c}_1`$ | $`\mathrm{Col}(A)=\mathrm{gen}\{(1,2)\}`$ (una recta). $`\mathrm{Nul}`$: $`x+2y=0`$, es decir $`t(-2,1)`$; en efecto $`A(-2,1)=(0,0)`$ |
| **2. Dos columnas independientes** | $`A=\begin{bmatrix}1&0&1\\0&1&1\end{bmatrix}`$ | $`\mathbf{c}_1=\mathbf{e}_1`$ y $`\mathbf{c}_2=\mathbf{e}_2`$ generan todo $`\mathbb{R}^2`$: rango 2, nulidad 1. $`\mathrm{Nul}`$: $`x_1=x_2=-x_3`$, es decir $`t(-1,-1,1)`$ |
| **3. Resolver $`A\mathbf{x}=\mathbf{b}`$** | La matriz del caso 1 con $`\mathbf{b}=(3,6)`$ | $`\mathbf{b}=3\mathbf{c}_1`$ está en $`\mathrm{Col}(A)`$; solución particular $`(3,0)`$. Solución general: $`\mathbf{x}=(3,0)+t(-2,1)`$ |

- **Solución general = solución particular + $\mathrm{Nul}(A)$.** Sumar un vector del espacio nulo no cambia $A\mathbf{x}$, por eso hay infinitas soluciones.
- Una matriz de columnas proporcionales **aplasta el plano sobre una recta**: entradas distintas terminan en la misma salida y la información se pierde. En el caso 2 hay 3 columnas = rango 2 + nulidad 1.

### Práctica y solución (diapositivas 9–10)

| Problema | Resultado |
|----------|-----------|
| **1.** $`A=\begin{bmatrix}1&-1\\2&-2\end{bmatrix}`$, $`\mathbf{b}=(3,6)`$ | Columnas opuestas ($`\mathbf{c}_2=-\mathbf{c}_1`$). $`\mathrm{Col}(A)=\mathrm{gen}\{(1,2)\}`$, $`\mathrm{Nul}(A)=\mathrm{gen}\{(1,1)\}`$. $`\mathbf{b}=3\mathbf{c}_1`$ sí está en $`\mathrm{Col}(A)`$: $`\mathbf{x}=(3,0)+t(1,1)`$ |
| **2.** $`A=\begin{bmatrix}1&2&3\\0&1&1\end{bmatrix}`$ | $`x_2=-x_3`$ y $`x_1=-2x_2-3x_3=-x_3`$, luego $`\mathrm{Nul}=t(-1,-1,1)`$. Dos pivotes: rango 2 y $`\mathrm{Col}(A)=\mathbb{R}^2`$ |
| **3.** $`A=\begin{bmatrix}1&0\\0&1\\1&1\end{bmatrix}`$ ($`3\times2`$) | $`\mathrm{Col}(A)=\{(x,y,x+y)\}`$: el plano $`z=x+y`$ en $`\mathbb{R}^3`$. $`(1,2,3)`$ sí es consistente ($`3=1+2`$); $`(1,2,4)`$ no ($`4\neq3`$) |

Verificación: el vector hallado en el espacio nulo debe cumplir $A\mathbf{x}=\mathbf{0}$.

---

## 3. Rango: cuánta información independiente hay (diapositivas 11–14)

### Explicación (diapositiva 11)

- **Independencia lineal:** una columna es independiente si no se puede obtener combinando las otras; una columna que sí se obtiene combinando otras no agrega dirección nueva (es **dependiente**).
- **Rango:** número de columnas independientes = dimensión de $\mathrm{Col}(A)$ = número de **pivotes** tras escalonar. Responde a «¿cuántas columnas aportan algo nuevo?». La dimensión del espacio columna es un punto (0), una recta (1), un plano (2) o, con más variables, un hiperplano.
- **Imagen mental:** tres vectores en $\mathbb{R}^3$ con rango 3 llenan el espacio; con rango 2 caen en un plano (el tercero es combinación de los otros dos); con rango 1 caen en una recta.
- **Teorema rango–nulidad**, con $n$ el número de columnas:

```math
\mathrm{rango}(A)+\mathrm{nulidad}(A)=n
```

  Ejemplo: $A$ de $4\times6$ con rango 4 tiene nulidad 2.
- **Rango completo** significa que no hay pérdida de información. **Rango bajo** significa información repetida; **nulidad > 0** significa que $A$ pierde información.
- **Idea para recordar:** una matriz es como un libro que transforma vectores (los estira, los refleja, los rota); el rango pregunta **qué partes del libro aportan algo nuevo**. En el problema 2 de transformaciones, la primera columna aporta el estiramiento de $x$ y la segunda el reflejo de $y$: las dos aportan y el rango es 2.
- **Matriz que se desconoce:** en la práctica se trabaja con matrices enormes (por ejemplo, la matriz de pesos de una red neuronal) y hay que saber cuántas filas y columnas son independientes. Una hoja de Excel también es una matriz. La GPU es especialista en operar matrices, y por eso se encareció no solo por la IA sino también por la minería de criptomonedas y los procesos *blockchain*, que consisten en resolver matrices.
- **Página interactiva (matriz $`2\times2`$ con columnas $`(a,c)`$ y $`(b,d)`$):** mientras las dos columnas sean independientes, cualquier cambio en un valor produce otra matriz distinta; ese es el máximo de combinaciones posibles y el rango es 2. Si se altera un valor hasta que una columna sea proporcional a la otra, la matriz colapsa a una recta y baja a rango 1. La matriz no se transforma: solo se ve cuántas direcciones independientes tiene. La misma página trae un ejercicio para calcular el rango de una matriz.

### Ejemplos resueltos (diapositiva 12): tres formas de calcular el rango

| Forma | Caso | Resultado |
|-------|------|-----------|
| **Una fila es múltiplo de otra** | $`A=\begin{bmatrix}1&2&3\\2&4&6\\0&1&1\end{bmatrix}`$: $`F_2=2F_1`$ (fila de ceros al eliminar) y $`\mathbf{c}_3=\mathbf{c}_1+\mathbf{c}_2`$ | Rango 2, nulidad 1, $`\mathrm{Nul}=t(1,1,-1)`$ |
| **Relación entre columnas** | $`\mathbf{v}_1=(1,2,1)`$, $`\mathbf{v}_2=(0,1,1)`$, $`\mathbf{v}_3=(1,3,2)=\mathbf{v}_1+\mathbf{v}_2`$, o sea $`\mathbf{v}_3-\mathbf{v}_1-\mathbf{v}_2=\mathbf{0}`$ | Dependientes, rango 2 |
| **Contar pivotes** | $`\begin{bmatrix}1&2&1\\2&5&3\\1&3&3\end{bmatrix}`$ con $`F_2-2F_1`$, $`F_3-F_1`$ y luego $`F_3-F_2`$ | Tres pivotes: rango 3, invertible |

Los tres caminos llegan al mismo número: filas, columnas o pivotes.

### Práctica y solución (diapositivas 13–14)

| Problema | Resultado |
|----------|-----------|
| **1.** $`A=\begin{bmatrix}1&2\\3&6\end{bmatrix}`$ | $`F_2=3F_1`$ y $`\mathbf{c}_2=2\mathbf{c}_1`$: una sola fila independiente, rango 1, nulidad 1. $`\mathrm{Nul}`$: $`x+2y=0`$, es decir $`t(-2,1)`$. Columnas dependientes |
| **2.** $`B=\begin{bmatrix}1&0&2\\0&1&3\\1&1&5\end{bmatrix}`$ | $`F_3-F_1-F_2=(0,0,0)`$ y $`\mathbf{c}_3=2\mathbf{c}_1+3\mathbf{c}_2`$. Dos pivotes: rango 2 |
| **3.** $`A`$ de $`4\times6`$ con rango 3 | Nulidad $`=6-3=3`$. Rango máximo posible $`=\min(4,6)=4`$. $`\mathrm{Col}(A)`$ tiene dimensión $`3<4`$, así que **hay $`\mathbf{b}`$ sin solución**: $`A\mathbf{x}=\mathbf{b}`$ no siempre tiene solución |

Verificación: siempre se comprueba que rango + nulidad = número de columnas.

---

## Conceptos clave

- **Transformación:** $\mathbf{x}\mapsto A\mathbf{x}$; manda rectas a rectas, fija el origen y el producto aplica una matriz tras otra. Las columnas son las imágenes de $`\mathbf{e}_1`$ y $`\mathbf{e}_2`$.
- **Tipos básicos:** escala, rotación, reflexión y cizalla. Para vértices: se escriben como columnas y se multiplican una sola vez.
- **Orden:** $RS\neq SR$; no hay conmutatividad.
- **$\mathrm{Col}(A)$** = lo que $A$ produce; **$\mathrm{Nul}(A)$** = lo que $A$ anula (vive en el espacio de entrada). $A\mathbf{x}=\mathbf{b}$ tiene solución si y solo si $\mathbf{b}\in\mathrm{Col}(A)$; la solución general es una particular más $\mathrm{Nul}(A)$.
- **Rango** = columnas independientes = pivotes; **rango + nulidad = número de columnas**. Rango bajo (o nulidad > 0) = información repetida y pérdida de información.
- **Tres caminos para el rango:** relaciones entre filas, relaciones entre columnas o contar pivotes.

---

## Fuera del PDF — logística, tareas y metodología

- **Examen:** cinco estudiantes lo presentaron con retraso por causas justificadas. Queda calificado a más tardar el día siguiente a la clase, junto con las prácticas; la práctica individual salió muy bien y el quiz de la casa 1 trae retroalimentación.
- **Práctica evaluada 3:** se habilitó el domingo (primero se había subido como documento y no como entregable). Incluye un ejercicio en Python, que forma parte de la práctica. La entrega es el lunes de la semana siguiente (la clase anterior había dicho martes). Las dudas se escriben al docente.
- **Práctica de transformaciones (diapositiva 5):** se trabajó en clase y **no se evalúa**; la resolución se comparte con el grupo.
- **Esta semana no hay entregable.** En el campus quedan la presentación, la página HTML interactiva de matrices, rango y nulidad (con un ejercicio para calcular el rango de una matriz) y videos de repaso sobre rango y transformaciones.
- **Siguiente clase:** el resto de la presentación (sobredeterminados y colinealidad, y el bloque 2: vectorización, matrices dispersas, complejidad computacional y *benchmarking*). El *benchmarking* es parte del trabajo diario en ciencia de datos e IA: medir cómo se comporta un modelo para elegir la precisión adecuada.
- **Hoja de ruta:** la semana siguiente se cierra el álgebra lineal con ejercicios y luego comienzan las **ecuaciones diferenciales**, pasando del cálculo en una variable al cálculo en varias variables (se dejan videos de transición). Antes se necesitan los **números complejos**.
