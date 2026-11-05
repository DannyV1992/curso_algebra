# Práctica en casa evaluada #3 — Matrices: leer, transponer, operar, despejar y multiplicar

## Fórmulas usadas

| Concepto | Fórmula |
|---|---|
| Matriz $m\times n$ | $m$ filas y $n$ columnas; $`a_{ij}`$ está en la fila $i$, columna $j$ |
| Transpuesta | $`(A^T)_{ij}=a_{ji}`$. Simétrica: $A=A^T$ |
| Suma y escalar | $`(A+B)_{ij}=a_{ij}+b_{ij}`$, $`(kA)_{ij}=k\cdot a_{ij}`$ (mismo tamaño para sumar) |
| Producto | $(m\times n)\cdot(n\times p)=(m\times p)$. La entrada $(i,j)$ de $AB$ es la fila $i$ de $A$ punto la columna $j$ de $B$ |
| Despejar | Se opera como con números, pero no se divide entre una matriz. $AB\neq BA$ en general |

---

# Parte 1 — Ejercicios a mano

## Ejercicio 1 — Leer y transponer una matriz

```math
A=\begin{bmatrix}4&-2&0&1\\3&5&-1&2\\-6&7&8&0\end{bmatrix}
```

**(a)** $A$ tiene 3 filas y 4 columnas: tamaño **$3\times4$**. En $`a_{ij}`$ el primer índice es la fila y el segundo la columna:

- $`a_{23}`$ (fila 2, columna 3): $-1$.
- $`a_{31}`$ (fila 3, columna 1): $-6$.
- $`a_{14}`$ (fila 1, columna 4): $1$.

**(b)** Cada fila de $A$ pasa a ser una columna de $A^T$, conservando el orden: la fila 1 $(4,-2,0,1)$ es la columna 1, la fila 2 $(3,5,-1,2)$ es la columna 2 y la fila 3 $(-6,7,8,0)$ es la columna 3.

```math
A^T=\begin{bmatrix}4&3&-6\\-2&5&7\\0&-1&8\\1&2&0\end{bmatrix}
```

Como $A$ es $3\times4$, $A^T$ es de tamaño **$4\times3$**.

**(c)** $`(A^T)_{42}`$ es la fila 4, columna 2 de $A^T$. La fila 4 de $A^T$ es $(1,2,0)$ y su segundo elemento es $2$. Por la definición $`(A^T)_{ij}=a_{ji}`$:

```math
(A^T)_{42}=a_{24}=2
```

Coincide con la entrada $`a_{24}`$ de $A$ (fila 2, columna 4), que vale $2$ ✓.

**(d)** Una matriz es simétrica si es igual a su transpuesta, es decir, si $`s_{ij}=s_{ji}`$.

$`S=\begin{bmatrix}2&-1&4\\-1&0&3\\4&3&5\end{bmatrix}`$. Se comparan las entradas fuera de la diagonal:

- $`s_{12}=-1`$ y $`s_{21}=-1`$ ✓
- $`s_{13}=4`$ y $`s_{31}=4`$ ✓
- $`s_{23}=3`$ y $`s_{32}=3`$ ✓

Entonces $`S^T=S`$: **$S$ sí es simétrica.**

$`T=\begin{bmatrix}1&2\\3&1\end{bmatrix}`$: $`t_{12}=2`$ pero $`t_{21}=3`$, y $2\neq3$. Entonces $`T^T=\begin{bmatrix}1&3\\2&1\end{bmatrix}\neq T`$: **$T$ no es simétrica.**

---

## Ejercicio 2 — Sumar, restar y escalar

```math
A=\begin{bmatrix}3&-2&1\\0&5&-4\end{bmatrix}\qquad B=\begin{bmatrix}-1&4&2\\6&-3&0\end{bmatrix}
```

Ambas son $2\times3$, así que se pueden sumar y restar entrada por entrada.

**(a)**

```math
A+B=\begin{bmatrix}3+(-1)&-2+4&1+2\\0+6&5+(-3)&-4+0\end{bmatrix}=\begin{bmatrix}2&2&3\\6&2&-4\end{bmatrix}
```

```math
A-B=\begin{bmatrix}3-(-1)&-2-4&1-2\\0-6&5-(-3)&-4-0\end{bmatrix}=\begin{bmatrix}4&-6&-1\\-6&8&-4\end{bmatrix}
```

**(b)** Primero se multiplica cada entrada por el escalar, por separado:

```math
3A=\begin{bmatrix}3\cdot3&3(-2)&3\cdot1\\3\cdot0&3\cdot5&3(-4)\end{bmatrix}=\begin{bmatrix}9&-6&3\\0&15&-12\end{bmatrix}
```

```math
2B=\begin{bmatrix}2(-1)&2\cdot4&2\cdot2\\2\cdot6&2(-3)&2\cdot0\end{bmatrix}=\begin{bmatrix}-2&8&4\\12&-6&0\end{bmatrix}
```

Luego se suman:

```math
3A+2B=\begin{bmatrix}9+(-2)&-6+8&3+4\\0+12&15+(-6)&-12+0\end{bmatrix}=\begin{bmatrix}7&2&7\\12&9&-12\end{bmatrix}
```

**(c)** Lado izquierdo: se transpone el resultado de (b).

```math
(3A+2B)^T=\begin{bmatrix}7&12\\2&9\\7&-12\end{bmatrix}
```

Lado derecho: se transpone cada matriz, se escala y se suma.

```math
A^T=\begin{bmatrix}3&0\\-2&5\\1&-4\end{bmatrix}\qquad B^T=\begin{bmatrix}-1&6\\4&-3\\2&0\end{bmatrix}
```

```math
3A^T=\begin{bmatrix}3\cdot3&3\cdot0\\3(-2)&3\cdot5\\3\cdot1&3(-4)\end{bmatrix}=\begin{bmatrix}9&0\\-6&15\\3&-12\end{bmatrix}
```

```math
2B^T=\begin{bmatrix}2(-1)&2\cdot6\\2\cdot4&2(-3)\\2\cdot2&2\cdot0\end{bmatrix}=\begin{bmatrix}-2&12\\8&-6\\4&0\end{bmatrix}
```

```math
3A^T+2B^T=\begin{bmatrix}9+(-2)&0+12\\-6+8&15+(-6)\\3+4&-12+0\end{bmatrix}=\begin{bmatrix}7&12\\2&9\\7&-12\end{bmatrix}
```

Ambos lados coinciden ✓.

---

## Ejercicio 3 — Despejar una matriz

```math
A=\begin{bmatrix}2&-1\\4&3\end{bmatrix}\qquad B=\begin{bmatrix}8&5\\-2&6\end{bmatrix}
```

**(a)** Se despeja $X$ en $3X+A=B$. Primero se suma el opuesto de $A$ a ambos lados:

```math
3X+A-A=B-A\ \Rightarrow\ 3X=B-A
```

Como no existe la división entre matrices, el escalar $3$ se quita multiplicando ambos lados por su inverso, $\tfrac13$:

```math
X=\tfrac13(B-A)
```

Se calcula $B-A$ entrada por entrada:

```math
B-A=\begin{bmatrix}8-2&5-(-1)\\-2-4&6-3\end{bmatrix}=\begin{bmatrix}6&6\\-6&3\end{bmatrix}
```

Y se multiplica por $\tfrac13$ (se divide cada entrada entre 3):

```math
X=\tfrac13\begin{bmatrix}6&6\\-6&3\end{bmatrix}=\begin{bmatrix}2&2\\-2&1\end{bmatrix}
```

**(b)** Verificación: se sustituye $X$ en $3X+A$.

```math
3X=\begin{bmatrix}3\cdot2&3\cdot2\\3(-2)&3\cdot1\end{bmatrix}=\begin{bmatrix}6&6\\-6&3\end{bmatrix}
```

```math
3X+A=\begin{bmatrix}6+2&6+(-1)\\-6+4&3+3\end{bmatrix}=\begin{bmatrix}8&5\\-2&6\end{bmatrix}=B\ \checkmark
```

**(c)** Se despeja $X$ en $2X-A=X+2B$. Hay $X$ en ambos lados, así que se juntan del mismo lado: se resta $X$ a ambos lados (se suma el opuesto de $X$), y se suma $A$ a ambos lados para sacar $A$ del lado izquierdo:

```math
2X-A-X=X+2B-X\ \Rightarrow\ X-A=2B\ \Rightarrow\ X=A+2B
```

Se calcula $2B$ y luego la suma:

```math
2B=\begin{bmatrix}2\cdot8&2\cdot5\\2(-2)&2\cdot6\end{bmatrix}=\begin{bmatrix}16&10\\-4&12\end{bmatrix}
```

```math
X=A+2B=\begin{bmatrix}2+16&-1+10\\4+(-4)&3+12\end{bmatrix}=\begin{bmatrix}18&9\\0&15\end{bmatrix}
```

Verificación: se calcula cada lado de la ecuación original. Lado izquierdo, primero $2X$:

```math
2X=\begin{bmatrix}2\cdot18&2\cdot9\\2\cdot0&2\cdot15\end{bmatrix}=\begin{bmatrix}36&18\\0&30\end{bmatrix}
```

```math
2X-A=\begin{bmatrix}36-2&18-(-1)\\0-4&30-3\end{bmatrix}=\begin{bmatrix}34&19\\-4&27\end{bmatrix}
```

Lado derecho:

```math
X+2B=\begin{bmatrix}18+16&9+10\\0+(-4)&15+12\end{bmatrix}=\begin{bmatrix}34&19\\-4&27\end{bmatrix}\ \checkmark
```

---

## Ejercicio 4 — Una capa de red neuronal: matriz por vector

La capa tiene 3 neuronas y 2 entradas; cada fila de $W$ son los pesos de una neurona.

```math
W=\begin{bmatrix}3&1\\-1&2\\0&5\end{bmatrix}\qquad \mathbf{x}=(4,-2)\qquad \mathbf{b}=(1,-2,4)
```

**(a)**

- $W$ tiene 3 filas (una por neurona) y 2 columnas (una por entrada): tamaño **$3\times2$**.
- $\mathbf{x}$ tiene **2 componentes** ($\mathbf{x}\in\mathbb{R}^2$).
- El producto $W\mathbf{x}$ **sí está definido**: el número de columnas de $W$ (2) es igual al número de componentes de $\mathbf{x}$ (2).
- El resultado tiene tantos componentes como filas de $W$: es un vector de **3 componentes** (una salida por neurona), pues $(3\times2)\cdot(2)=(3)$.

**(b)** Por filas, cada componente es el producto punto de una fila de $W$ con $\mathbf{x}$. Las filas de $W$ son $(3,1)$, $(-1,2)$ y $(0,5)$, y $\mathbf{x}=(4,-2)$:

```math
(3,1)\cdot(4,-2)=3\cdot4+1\cdot(-2)=12-2=10
```

```math
(-1,2)\cdot(4,-2)=(-1)\cdot4+2\cdot(-2)=-4-4=-8
```

```math
(0,5)\cdot(4,-2)=0\cdot4+5\cdot(-2)=0-10=-10
```

```math
W\mathbf{x}=(10,\ -8,\ -10)
```

**(c)** Por columnas, $W\mathbf{x}$ es una combinación lineal de las columnas de $W$ con los componentes de $\mathbf{x}$ como coeficientes:

```math
W\mathbf{x}=4\begin{bmatrix}3\\-1\\0\end{bmatrix}+(-2)\begin{bmatrix}1\\2\\5\end{bmatrix}=\begin{bmatrix}12\\-4\\0\end{bmatrix}+\begin{bmatrix}-2\\-4\\-10\end{bmatrix}=\begin{bmatrix}10\\-8\\-10\end{bmatrix}
```

Da el mismo vector que en (b) ✓.

**(d)** Se suma el vector de sesgos:

```math
\mathbf{y}=W\mathbf{x}+\mathbf{b}=(10+1,\ -8+(-2),\ -10+4)=(11,\ -10,\ -6)
```

**Interpretación:** cada componente de $\mathbf{y}$ es la salida de una neurona: la suma ponderada de las entradas con los pesos de su fila de $W$ más su sesgo. La neurona 1 da $11$, la neurona 2 da $-10$ y la neurona 3 da $-6$.

---

## Ejercicio 5 — Producto de matrices

```math
A=\begin{bmatrix}2&-1&3\\0&4&1\end{bmatrix}\qquad B=\begin{bmatrix}1&0\\-2&3\\4&-1\end{bmatrix}
```

**(a)** $A$ es $2\times3$ y $B$ es $3\times2$. Los números de adentro coinciden (3 y 3), así que **$AB$ existe**, y los de afuera dan su tamaño: $(2\times3)(3\times2)=$ **$2\times2$**.

**(b)** Cada entrada es (fila de $A$) · (columna de $B$). Las filas de $A$ son $(2,-1,3)$ y $(0,4,1)$; las columnas de $B$ son $(1,-2,4)$ y $(0,3,-1)$.

```math
c_{11}=(2,-1,3)\cdot(1,-2,4)=2\cdot1+(-1)(-2)+3\cdot4=2+2+12=16
```

```math
c_{12}=(2,-1,3)\cdot(0,3,-1)=2\cdot0+(-1)\cdot3+3\cdot(-1)=0-3-3=-6
```

```math
c_{21}=(0,4,1)\cdot(1,-2,4)=0\cdot1+4\cdot(-2)+1\cdot4=0-8+4=-4
```

```math
c_{22}=(0,4,1)\cdot(0,3,-1)=0\cdot0+4\cdot3+1\cdot(-1)=0+12-1=11
```

```math
AB=\begin{bmatrix}16&-6\\-4&11\end{bmatrix}
```

**(c)** $BA$ es $(3\times2)(2\times3)$: los números de adentro coinciden (2 y 2), así que **$BA$ también existe**, y tiene tamaño **$3\times3$**. Como $AB$ es $2\times2$ y $BA$ es $3\times3$, tienen distinto tamaño, así que **no pueden ser iguales**: $AB\neq BA$ en este caso.

**(d)** $`C=\begin{bmatrix}1&2\\0&1\end{bmatrix}`$ y $`D=\begin{bmatrix}1&0\\3&1\end{bmatrix}`$.

$CD$ (fila de $C$ · columna de $D$):

```math
CD=\begin{bmatrix}1\cdot1+2\cdot3&1\cdot0+2\cdot1\\0\cdot1+1\cdot3&0\cdot0+1\cdot1\end{bmatrix}=\begin{bmatrix}7&2\\3&1\end{bmatrix}
```

$DC$ (fila de $D$ · columna de $C$):

```math
DC=\begin{bmatrix}1\cdot1+0\cdot0&1\cdot2+0\cdot1\\3\cdot1+1\cdot0&3\cdot2+1\cdot1\end{bmatrix}=\begin{bmatrix}1&2\\3&7\end{bmatrix}
```

**No son iguales:** $CD\neq DC$. Aunque ambas matrices son del mismo tamaño y los dos productos existen, el producto de matrices no es conmutativo.

---

# Parte 2 — Ejercicios en Python

Resuelta en [Respuestas_Parte_2.ipynb](Respuestas_Parte_2.ipynb), ejecutada de arriba abajo con todas las verificaciones (`assert`) en verde. Resultados principales:

| Ejercicio | Resultado |
|---|---|
| P1 (a) | `A.shape = (2, 3)`; `A.T` de tamaño $3\times2$ |
| P1 (b) | $`3A-2B=\begin{bmatrix}4&-18&20\\20&4&-14\end{bmatrix}`$ y $(3A-2B)^T=3A^T-2B^T$ ✓ |
| P1 (c) | $4X+A=2B\Rightarrow X=\tfrac14(2B-A)$, es decir, $`X=\begin{bmatrix}0&2{,}5&-2\\-1&-1&2{,}5\end{bmatrix}`$ |
| P1 (d) | `A @ B.T` es $2\times2$ y `B.T @ A` es $3\times3$: el producto no conmuta |
| P2 (a) | $`\hat R`$ de $4\times3$; para el usuario 0: $(2{,}5;\ 2;\ 3{,}25)$ |
| P2 (b) | ECM inicial $\approx2{,}215$ |
| P2 (c) | `E @ F` es $4\times2$, igual que $U$ |
| P2 (d) | Con `U_nueva` el ECM baja a $\approx0{,}263$ |
| P2 (e) | `np.argmax` da el índice 2: se recomienda la tercera película al usuario 0 |
