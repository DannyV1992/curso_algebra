# Prácticas de la Clase 7 — Operar y despejar matrices, matriz por vector y producto de matrices

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University

**Fuente:** `Material del curso.pdf`, diapositivas 37–38 (práctica 9), 41–42 (práctica 10) y 45–46 (práctica 11), más los ejemplos y los ejercicios «Ahora tú» de `Clase 7 - Guia_Matrices_Operar_Despejar_Multiplicar.pdf` y los ejercicios propuestos del notebook `Practica python.ipynb`

**Resumen de la clase:** [Resumen_Clase_7.md](../Resumenes/Resumen_Clase_7.md)

La práctica 9 (diapositivas 37–38) quedó pendiente en [Practicas_Clase_6.md](Practicas_Clase_6.md) y se resuelve aquí. La práctica 12 (regresión como proyección, diapositivas 49–50) se resuelve cuando se cubra en clase.

Antes de multiplicar se comprueba siempre la dimensión: $(m\times n)\cdot(n\times p)=(m\times p)$. El número de columnas de la primera debe ser igual al número de filas (o de componentes) de la segunda, y el resultado tiene las filas de la primera y las columnas de la segunda.

---

## Práctica 9 — Operar y despejar matrices

**Datos:**

```math
C=\begin{bmatrix}2&-1&0\\3&4&1\end{bmatrix}\qquad D=\begin{bmatrix}1&1&-2\\0&-3&5\end{bmatrix}
```

### a) $C+D$

Las dos son $2\times3$, así que se suman entrada por entrada (la entrada $(i,j)$ del resultado usa solo las entradas $(i,j)$ de $C$ y $D$):

```math
C+D=\begin{bmatrix}2+1&-1+1&0+(-2)\\3+0&4+(-3)&1+5\end{bmatrix}=\begin{bmatrix}3&0&-2\\3&1&6\end{bmatrix}
```

**Resultado:** $C+D$ es de tamaño $2\times3$.

### b) $3C-2D$

Primero se escalan por separado, multiplicando cada entrada:

```math
3C=\begin{bmatrix}6&-3&0\\9&12&3\end{bmatrix}\qquad 2D=\begin{bmatrix}2&2&-4\\0&-6&10\end{bmatrix}
```

Luego se restan entrada por entrada (cuidado con el signo en $0-(-4)$ y $12-(-6)$):

```math
3C-2D=\begin{bmatrix}6-2&-3-2&0-(-4)\\9-0&12-(-6)&3-10\end{bmatrix}=\begin{bmatrix}4&-5&4\\9&18&-7\end{bmatrix}
```

### c) $(C-D)^T$ y su dimensión

```math
C-D=\begin{bmatrix}2-1&-1-1&0-(-2)\\3-0&4-(-3)&1-5\end{bmatrix}=\begin{bmatrix}1&-2&2\\3&7&-4\end{bmatrix}
```

La transpuesta tiene como columnas las filas de $C-D$, en el mismo orden:

```math
(C-D)^T=\begin{bmatrix}1&3\\-2&7\\2&-4\end{bmatrix}
```

**Resultado:** como $C-D$ es $2\times3$, su transpuesta tiene dimensión $3\times2$.

### d) Despejar $X$ en $2X+C=D$

Se despeja primero con letras. Se suma el opuesto de $C$ a ambos lados:

```math
2X+C-C=D-C\ \Rightarrow\ 2X=D-C
```

No existe la división entre matrices; el escalar $2$ se quita multiplicando por $\tfrac12$:

```math
X=\tfrac12(D-C)
```

Solo al final se sustituye:

```math
D-C=\begin{bmatrix}1-2&1-(-1)&-2-0\\0-3&-3-4&5-1\end{bmatrix}=\begin{bmatrix}-1&2&-2\\-3&-7&4\end{bmatrix}
```

```math
X=\tfrac12\begin{bmatrix}-1&2&-2\\-3&-7&4\end{bmatrix}=\begin{bmatrix}-0{,}5&1&-1\\-1{,}5&-3{,}5&2\end{bmatrix}
```

**Verificación:** $2X+C$ debe devolver $D$ entrada por entrada.

```math
2X+C=\begin{bmatrix}-1&2&-2\\-3&-7&4\end{bmatrix}+\begin{bmatrix}2&-1&0\\3&4&1\end{bmatrix}=\begin{bmatrix}1&1&-2\\0&-3&5\end{bmatrix}=D\ \checkmark
```

---

## Práctica 10 — Productos matriz-vector

**Datos:**

```math
A=\begin{bmatrix}1&-2&0\\3&1&4\end{bmatrix}\qquad \mathbf{x}=(2,\ 1,\ -1)
```

### a) Verificar que las dimensiones permiten el producto

$A$ es $2\times3$ (3 columnas) y $\mathbf{x}\in\mathbb{R}^3$ (3 componentes). El número de columnas de $A$ coincide con el número de componentes de $\mathbf{x}$, luego el producto existe. El resultado tiene tantos componentes como filas de $A$: es un vector de $\mathbb{R}^2$, pues $(2\times3)\cdot(3)=(2)$.

### b) $A\mathbf{x}$ por filas y por columnas

**Por filas.** Cada componente es el producto punto de una fila de $A$ con $\mathbf{x}$:

- Fila 1: $(1,-2,0)\cdot(2,1,-1)=1\cdot2+(-2)\cdot1+0\cdot(-1)=2-2+0=0$.
- Fila 2: $(3,1,4)\cdot(2,1,-1)=3\cdot2+1\cdot1+4\cdot(-1)=6+1-4=3$.

```math
A\mathbf{x}=(0,\ 3)
```

**Por columnas.** Cada componente de $\mathbf{x}$ multiplica a su columna (el primero a la primera, el segundo a la segunda, el tercero a la tercera) y se suman:

```math
2\begin{bmatrix}1\\3\end{bmatrix}+1\begin{bmatrix}-2\\1\end{bmatrix}+(-1)\begin{bmatrix}0\\4\end{bmatrix}=\begin{bmatrix}2\\6\end{bmatrix}+\begin{bmatrix}-2\\1\end{bmatrix}+\begin{bmatrix}0\\-4\end{bmatrix}=\begin{bmatrix}0\\3\end{bmatrix}
```

**Resultado:** las dos lecturas coinciden, $A\mathbf{x}=(0,3)$ ✓. El resultado no depende de cómo se organice el cálculo.

### c) ¿Existe el producto de $A$ por $(1,2)$?

$A$ tiene 3 columnas y el vector $(1,2)$ tiene 2 componentes. Como $3\neq2$, no se cumple la regla $(2\times3)\cdot(2)$.

**Resultado:** el producto **no existe**.

### d) Predicción con pesos $\mathbf{w}=(3;\ 0{,}5)$

```math
X=\begin{bmatrix}1&2\\1&5\\1&7\end{bmatrix}
```

$X$ es $3\times2$ y $\mathbf{w}$ tiene 2 componentes (3 y 0,5), así que el producto existe y da 3 predicciones, una por fila. Cada fila es un producto punto con los pesos:

- Fila 1: $3\cdot1+0{,}5\cdot2=3+1=4$.
- Fila 2: $3\cdot1+0{,}5\cdot5=3+2{,}5=5{,}5$.
- Fila 3: $3\cdot1+0{,}5\cdot7=3+3{,}5=6{,}5$.

```math
\hat{\mathbf{y}}=X\mathbf{w}=(4;\ 5{,}5;\ 6{,}5)
```

La columna de unos de $X$ multiplica al peso $3$, que actúa como intercepto (el valor base de la predicción); el peso $0{,}5$ indica cuánto sube la predicción por cada unidad de la segunda variable.

---

## Práctica 11 — Producto de matrices

**Datos:**

```math
A=\begin{bmatrix}2&0&1\\-1&3&2\end{bmatrix}\qquad B=\begin{bmatrix}1&2\\0&-1\\4&1\end{bmatrix}
```

### a) Dimensiones de $AB$ y de $BA$

- $AB$: $(2\times3)(3\times2)$. Los números de adentro coinciden (3 y 3) y los de afuera dan el tamaño: $2\times2$.
- $BA$: $(3\times2)(2\times3)$. Los de adentro coinciden (2 y 2) y los de afuera dan el tamaño: $3\times3$.

### b) $AB$ con los cuatro productos punto

Las filas de $A$ son $(2,0,1)$ y $(-1,3,2)$; las columnas de $B$ son $(1,0,4)$ y $(2,-1,1)$.

```math
c_{11}=2\cdot1+0\cdot0+1\cdot4=2+0+4=6\qquad c_{12}=2\cdot2+0\cdot(-1)+1\cdot1=4+0+1=5
```

```math
c_{21}=(-1)\cdot1+3\cdot0+2\cdot4=-1+0+8=7\qquad c_{22}=(-1)\cdot2+3\cdot(-1)+2\cdot1=-2-3+2=-3
```

```math
AB=\begin{bmatrix}6&5\\7&-3\end{bmatrix}
```

### c) $BA$ con los nueve productos punto

Las filas de $B$ son $(1,2)$, $(0,-1)$ y $(4,1)$; las columnas de $A$ son $(2,-1)$, $(0,3)$ y $(1,2)$.

```math
BA=\begin{bmatrix}1\cdot2+2\cdot(-1)&1\cdot0+2\cdot3&1\cdot1+2\cdot2\\0\cdot2+(-1)(-1)&0\cdot0+(-1)\cdot3&0\cdot1+(-1)\cdot2\\4\cdot2+1\cdot(-1)&4\cdot0+1\cdot3&4\cdot1+1\cdot2\end{bmatrix}=\begin{bmatrix}0&6&5\\1&-3&-2\\7&3&6\end{bmatrix}
```

**¿Puede ser $AB=BA$?** No: $AB$ es $2\times2$ y $BA$ es $3\times3$. Dos matrices de distinto tamaño nunca son iguales.

### d) Verificar $(AB)^T=B^TA^T$

Primero las transpuestas (cada fila pasa a ser columna):

```math
B^T=\begin{bmatrix}1&0&4\\2&-1&1\end{bmatrix}\qquad A^T=\begin{bmatrix}2&-1\\0&3\\1&2\end{bmatrix}
```

$B^TA^T$ es $(2\times3)(3\times2)=2\times2$, igual que $(AB)^T$. Las filas de $B^T$ son $(1,0,4)$ y $(2,-1,1)$; las columnas de $A^T$ son $(2,0,1)$ y $(-1,3,2)$:

```math
B^TA^T=\begin{bmatrix}1\cdot2+0\cdot0+4\cdot1&1\cdot(-1)+0\cdot3+4\cdot2\\2\cdot2+(-1)\cdot0+1\cdot1&2\cdot(-1)+(-1)\cdot3+1\cdot2\end{bmatrix}=\begin{bmatrix}6&7\\5&-3\end{bmatrix}
```

Por otro lado, la transpuesta del resultado de (b):

```math
(AB)^T=\begin{bmatrix}6&7\\5&-3\end{bmatrix}
```

**Verificación:** ambos coinciden, $(AB)^T=B^TA^T$ ✓. La transpuesta de un producto invierte el orden de los factores.

---

## Ejercicios de la guía y del notebook

Los cuatro ejemplos de la guía de matrices (que repite el notebook) y sus ejercicios «Ahora tú». Los resultados coinciden con las respuestas que da la guía.

### G1. $2A-3B$

```math
A=\begin{bmatrix}2&-1&3\\0&4&-2\end{bmatrix}\qquad B=\begin{bmatrix}1&0&-2\\3&-1&4\end{bmatrix}
```

```math
2A=\begin{bmatrix}4&-2&6\\0&8&-4\end{bmatrix}\qquad 3B=\begin{bmatrix}3&0&-6\\9&-3&12\end{bmatrix}
```

```math
2A-3B=\begin{bmatrix}4-3&-2-0&6-(-6)\\0-9&8-(-3)&-4-12\end{bmatrix}=\begin{bmatrix}1&-2&12\\-9&11&-16\end{bmatrix}
```

Control de la entrada $(1,1)$: $2\cdot2-3\cdot1=1$ ✓.

### G2. Despejar $X$

```math
A=\begin{bmatrix}3&1\\-2&4\end{bmatrix}\qquad B=\begin{bmatrix}7&5\\2&-6\end{bmatrix}
```

**(a)** $2X+A=B$. Se suma el opuesto de $A$ y se multiplica por $\tfrac12$:

```math
2X=B-A\ \Rightarrow\ X=\tfrac12(B-A)=\tfrac12\begin{bmatrix}4&4\\4&-10\end{bmatrix}=\begin{bmatrix}2&2\\2&-5\end{bmatrix}
```

Verificación: $`2X+A=\begin{bmatrix}4&4\\4&-10\end{bmatrix}+\begin{bmatrix}3&1\\-2&4\end{bmatrix}=\begin{bmatrix}7&5\\2&-6\end{bmatrix}=B`$ ✓.

**(b)** $3X-A=X+B$. Se juntan las $X$ del lado izquierdo restando $X$ a ambos lados y se suma $A$ a ambos lados:

```math
3X-X=A+B\ \Rightarrow\ 2X=A+B\ \Rightarrow\ X=\tfrac12(A+B)=\tfrac12\begin{bmatrix}10&6\\0&-2\end{bmatrix}=\begin{bmatrix}5&3\\0&-1\end{bmatrix}
```

Verificación: $`3X-A=\begin{bmatrix}15&9\\0&-3\end{bmatrix}-\begin{bmatrix}3&1\\-2&4\end{bmatrix}=\begin{bmatrix}12&8\\2&-7\end{bmatrix}`$ y $`X+B=\begin{bmatrix}5&3\\0&-1\end{bmatrix}+\begin{bmatrix}7&5\\2&-6\end{bmatrix}=\begin{bmatrix}12&8\\2&-7\end{bmatrix}`$ ✓.

### G3. Una capa de red neuronal: $A\mathbf{x}$

```math
A=\begin{bmatrix}2&-1&3\\4&0&5\end{bmatrix}\qquad \mathbf{x}=(1,\ 2,\ -1)
```

$A$ es $2\times3$ y $\mathbf{x}$ tiene 3 componentes: el producto existe y da 2 componentes (2 neuronas, 3 entradas; cada fila de $A$ son los pesos de una neurona).

- Fila 1: $2\cdot1+(-1)\cdot2+3\cdot(-1)=2-2-3=-3$.
- Fila 2: $4\cdot1+0\cdot2+5\cdot(-1)=4+0-5=-1$.

```math
A\mathbf{x}=(-3,\ -1)
```

Por columnas: $1\cdot(2,4)+2\cdot(-1,0)+(-1)\cdot(3,5)=(2,4)+(-2,0)+(-3,-5)=(-3,-1)$ ✓.

### G4. $AB$ y $BA$ con la guía

```math
A=\begin{bmatrix}1&2&0\\-1&3&4\end{bmatrix}\qquad B=\begin{bmatrix}2&1\\0&-3\\5&2\end{bmatrix}
```

$AB$ es $(2\times3)(3\times2)=2\times2$:

```math
AB=\begin{bmatrix}1\cdot2+2\cdot0+0\cdot5&1\cdot1+2\cdot(-3)+0\cdot2\\(-1)\cdot2+3\cdot0+4\cdot5&(-1)\cdot1+3\cdot(-3)+4\cdot2\end{bmatrix}=\begin{bmatrix}2&-5\\18&-2\end{bmatrix}
```

$BA$ es $(3\times2)(2\times3)=3\times3$, de distinto tamaño que $AB$, luego $AB\neq BA$.

Con $`P=\begin{bmatrix}1&2\\3&4\end{bmatrix}`$ y $`Q=\begin{bmatrix}0&1\\1&0\end{bmatrix}`$, ambos productos existen y aun así difieren: $`PQ=\begin{bmatrix}2&1\\4&3\end{bmatrix}`$ (intercambia las **columnas** de $P$) y $`QP=\begin{bmatrix}3&4\\1&2\end{bmatrix}`$ (intercambia las **filas** de $P$).

### G5. Ejercicios «Ahora tú» de la guía y propuestos del notebook

Los ejercicios 1 a 3 son los de «Ahora tú» de la guía (el 4 de la guía, $PQ$ y $QP$, está al final de G4); los ejercicios 4 y 5 son propuestos solo en el notebook.

**1. $A+2B$** con las matrices de G1:

```math
A+2B=\begin{bmatrix}2+2\cdot1&-1+2\cdot0&3+2\cdot(-2)\\0+2\cdot3&4+2\cdot(-1)&-2+2\cdot4\end{bmatrix}=\begin{bmatrix}4&-1&-1\\6&2&6\end{bmatrix}
```

Control de la entrada $(1,1)$ a mano: $2+2\cdot1=4$ ✓.

**2. Despejar $X$ en $A-2X=B$** (con las matrices de G2):

```math
-2X=B-A\ \Rightarrow\ X=-\tfrac12(B-A)=\tfrac12(A-B)=\tfrac12\begin{bmatrix}-4&-4\\-4&10\end{bmatrix}=\begin{bmatrix}-2&-2\\-2&5\end{bmatrix}
```

Verificación: $`A-2X=\begin{bmatrix}3&1\\-2&4\end{bmatrix}-\begin{bmatrix}-4&-4\\-4&10\end{bmatrix}=\begin{bmatrix}7&5\\2&-6\end{bmatrix}=B`$ ✓.

**3.** $`\begin{bmatrix}1&-2\\3&0\\2&5\end{bmatrix}\begin{bmatrix}4\\1\end{bmatrix}`$ es $(3\times2)(2)=(3)$:

```math
(1\cdot4+(-2)\cdot1,\ 3\cdot4+0\cdot1,\ 2\cdot4+5\cdot1)=(2,\ 12,\ 13)
```

Cada fila es una neurona con 2 pesos y las 3 salidas son lo que produce cada neurona para la entrada $(4,1)$.

**4. Tasa de aprendizaje $\eta$** en el caso de la fuga de clientes (200 épocas, pérdida inicial $0{,}693$ en los tres casos):

| $\eta$ | Pérdida tras 10 épocas | Pérdida tras 200 épocas | Lectura |
|--------|------------------------|-------------------------|---------|
| $0{,}01$ | $0{,}682$ | $0{,}554$ | Pasos muy pequeños: la curva baja lento y aún no llegó al mínimo |
| $0{,}5$ | $0{,}475$ | $0{,}412$ | Equilibrado: llega al mínimo en unas decenas de épocas |
| $5$ | $0{,}412$ | $0{,}412$ | Pasos grandes: llega casi de inmediato; en estos datos no diverge, pero una tasa demasiado grande puede hacer que el error oscile o crezca |

Una tasa pequeña necesita muchas épocas; una grande acelera, con el riesgo de pasarse del mínimo.

**5. Agregar una cuarta variable** (por ejemplo `soporte`): $X$ pasa de $n\times3$ a $n\times4$ (con $n=300$ clientes, $300\times4$), el vector de pesos $\mathbf{w}$ pasa a tener 4 componentes y el gradiente $g=\tfrac1nX^T(p-y)$ también: $X^T$ es $4\times n$ y $(p-y)$ tiene $n$ componentes, luego $g$ tiene 4 componentes, uno por peso.
