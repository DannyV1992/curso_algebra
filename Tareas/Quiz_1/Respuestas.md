# Quiz en casa #1 — Vectores, producto punto, combinaciones lineales y matrices

## Fórmulas usadas

| Concepto | Fórmula |
|---|---|
| Norma | $`\lVert\mathbf{v}\rVert=\sqrt{v_1^2+\cdots+v_n^2}`$ |
| Distancia | $d(\mathbf{u},\mathbf{v})=\lVert\mathbf{u}-\mathbf{v}\rVert$ |
| Producto punto | $`\mathbf{u}\cdot\mathbf{v}=u_1v_1+\cdots+u_nv_n`$, y $\mathbf{v}\cdot\mathbf{v}=\lVert\mathbf{v}\rVert^2$ |
| Ángulo | $\cos\theta=\dfrac{\mathbf{u}\cdot\mathbf{v}}{\lVert\mathbf{u}\rVert\lVert\mathbf{v}\rVert}$ |
| Ortogonalidad | $\mathbf{u}\perp\mathbf{v}\iff\mathbf{u}\cdot\mathbf{v}=0$ |
| Transpuesta | $`(A^T)_{ij}=a_{ji}`$ |
| Suma y escalar | $`(A+B)_{ij}=a_{ij}+b_{ij}`$, $`(kA)_{ij}=k\,a_{ij}`$ |

---

# Parte A — Ejercicios base

## Ejercicio 1 — Norma y vector unitario

**Datos:** $\mathbf{u}=(2,-3,6)$.

**(a)** Se eleva al cuadrado cada componente, se suman y se saca la raíz:

```math
2^2=4\qquad(-3)^2=9\qquad6^2=36
```

```math
\lVert\mathbf{u}\rVert=\sqrt{4+9+36}=\sqrt{49}=7
```

**(b)** Para el vector unitario se divide **cada componente** entre la norma:

```math
\hat{\mathbf{u}}=\frac{\mathbf{u}}{7}=\left(\tfrac{2}{7},\ \tfrac{-3}{7},\ \tfrac{6}{7}\right)=\left(\tfrac{2}{7},\ -\tfrac{3}{7},\ \tfrac{6}{7}\right)
```

Verificación (la norma de $\hat{\mathbf{u}}$ debe ser 1):

```math
\lVert\hat{\mathbf{u}}\rVert=\sqrt{\left(\tfrac{2}{7}\right)^2+\left(-\tfrac{3}{7}\right)^2+\left(\tfrac{6}{7}\right)^2}=\sqrt{\tfrac{4}{49}+\tfrac{9}{49}+\tfrac{36}{49}}=\sqrt{\tfrac{49}{49}}=\sqrt{1}=1\ \checkmark
```

**(c)** Se multiplica cada componente de $\mathbf{u}$ por $-3$:

```math
-3\mathbf{u}=\big(-3\cdot2,\ -3\cdot(-3),\ -3\cdot6\big)=(-6,\ 9,\ -18)
```

Norma directa:

```math
(-6)^2=36\qquad9^2=81\qquad(-18)^2=324
```

```math
\lVert-3\mathbf{u}\rVert=\sqrt{36+81+324}=\sqrt{441}=21
```

Con la propiedad, usando $\lVert\mathbf{u}\rVert=7$ del inciso (a):

```math
\lvert-3\rvert\cdot\lVert\mathbf{u}\rVert=3\cdot7=21
```

Ambos resultados son $21$ ✓.

---

## Ejercicio 2 — Distancia

**(a)** $A=(1,4,-2)$ y $B=(3,0,-1)$. La distancia es la norma de la resta. Se resta componente a componente:

```math
A-B=(1-3,\ 4-0,\ -2-(-1))=(-2,\ 4,\ -1)
```

```math
(-2)^2=4\qquad4^2=16\qquad(-1)^2=1
```

```math
d(A,B)=\sqrt{4+16+1}=\sqrt{21}\approx4{,}583
```

**(b)** Se escribe la distancia con $k$ y se iguala a 5:

```math
d\big((2,k),(5,-1)\big)=\sqrt{(2-5)^2+(k-(-1))^2}=\sqrt{(-3)^2+(k+1)^2}=\sqrt{9+(k+1)^2}=5
```

Se elevan al cuadrado ambos lados para quitar la raíz:

```math
9+(k+1)^2=25
```

Se resta 9 en ambos lados:

```math
(k+1)^2=25-9=16
```

Hay dos números cuyo cuadrado es 16, el positivo y el negativo (porque $(-4)(-4)=16$):

```math
k+1=4\quad\text{o}\quad k+1=-4
```

Se despeja $k$ en cada caso:

```math
k=4-1=3\quad\text{o}\quad k=-4-1=-5
```

Verificación de ambos valores:

```math
k=3:\ \sqrt{(2-5)^2+(3+1)^2}=\sqrt{9+16}=\sqrt{25}=5\ \checkmark
```

```math
k=-5:\ \sqrt{(2-5)^2+(-5+1)^2}=\sqrt{9+(-4)^2}=\sqrt{9+16}=\sqrt{25}=5\ \checkmark
```

---

## Ejercicio 3 — Producto punto y propiedades

**Datos:** $\mathbf{a}=(1,-2,3)$, $\mathbf{b}=(4,1,-2)$, $\mathbf{c}=(2,3,1)$.

**(a)** Productos parciales (componente 1 con 1, 2 con 2, 3 con 3) y luego suma:

```math
\mathbf{a}\cdot\mathbf{b}=1(4)+(-2)(1)+3(-2)=4-2-6=-4
```

```math
\mathbf{a}\cdot\mathbf{c}=1(2)+(-2)(3)+3(1)=2-6+3=-1
```

**(b)** Propiedad distributiva $\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}$.

Lado izquierdo. Primero la suma, componente a componente:

```math
\mathbf{b}+\mathbf{c}=(4+2,\ 1+3,\ -2+1)=(6,\ 4,\ -1)
```

Luego el producto punto con $\mathbf{a}$:

```math
\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=1(6)+(-2)(4)+3(-1)=6-8-3=-5
```

Lado derecho. Se usan los productos del inciso (a) y se suman:

```math
\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}=-4+(-1)=-5
```

Ambos lados dan $-5$ ✓.

**(c)** Primera igualdad: $(2\mathbf{a})\cdot\mathbf{c}=2(\mathbf{a}\cdot\mathbf{c})$.

Lado izquierdo. Primero se escala $\mathbf{a}$:

```math
2\mathbf{a}=(2\cdot1,\ 2\cdot(-2),\ 2\cdot3)=(2,\ -4,\ 6)
```

```math
(2\mathbf{a})\cdot\mathbf{c}=2(2)+(-4)(3)+6(1)=4-12+6=-2
```

Lado derecho. Se usa $\mathbf{a}\cdot\mathbf{c}=-1$ del inciso (a):

```math
2(\mathbf{a}\cdot\mathbf{c})=2(-1)=-2
```

Ambos lados dan $-2$ ✓.

Segunda igualdad: $\mathbf{a}\cdot\mathbf{a}=\lVert\mathbf{a}\rVert^2$.

```math
\mathbf{a}\cdot\mathbf{a}=1(1)+(-2)(-2)+3(3)=1+4+9=14
```

```math
\lVert\mathbf{a}\rVert=\sqrt{1^2+(-2)^2+3^2}=\sqrt{1+4+9}=\sqrt{14}\ \Rightarrow\ \lVert\mathbf{a}\rVert^2=\left(\sqrt{14}\right)^2=14
```

Ambos dan $14$ ✓.

---

## Ejercicio 4 — Ángulo entre vectores

**(a)** $\mathbf{u}=(1,1,0)$, $\mathbf{v}=(0,1,1)$.

Producto punto y normas:

```math
\mathbf{u}\cdot\mathbf{v}=1(0)+1(1)+0(1)=0+1+0=1
```

```math
\lVert\mathbf{u}\rVert=\sqrt{1^2+1^2+0^2}=\sqrt{1+1+0}=\sqrt2\qquad\lVert\mathbf{v}\rVert=\sqrt{0^2+1^2+1^2}=\sqrt{0+1+1}=\sqrt2
```

Se sustituye en la fórmula del coseno. Se usa $\sqrt2\cdot\sqrt2=2$:

```math
\cos\theta=\frac{1}{\sqrt2\cdot\sqrt2}=\frac12=0{,}5
```

El ángulo cuyo coseno es $0{,}5$ es un valor conocido:

```math
\theta=\arccos(0{,}5)=60^\circ
```

**(b)** $\mathbf{u}=(-2,1)$, $\mathbf{v}=(1,-3)$.

Predicción por el signo del producto punto:

```math
\mathbf{u}\cdot\mathbf{v}=(-2)(1)+1(-3)=-2-3=-5
```

Como $`-5<0`$, el ángulo es **obtuso** (mayor que $90^\circ$). Si fuera positivo sería agudo, y si fuera cero, recto.

Confirmación. Normas:

```math
\lVert\mathbf{u}\rVert=\sqrt{(-2)^2+1^2}=\sqrt{4+1}=\sqrt5\qquad\lVert\mathbf{v}\rVert=\sqrt{1^2+(-3)^2}=\sqrt{1+9}=\sqrt{10}
```

Coseno. Se usa $\sqrt5\cdot\sqrt{10}=\sqrt{50}$ y $\sqrt{50}=\sqrt{25\cdot2}=5\sqrt2$, y luego se racionaliza multiplicando arriba y abajo por $\sqrt2$:

```math
\cos\theta=\frac{-5}{\sqrt5\cdot\sqrt{10}}=\frac{-5}{\sqrt{50}}=\frac{-5}{5\sqrt2}=\frac{-1}{\sqrt2}=-\frac{\sqrt2}{2}\approx-0{,}707
```

Ángulo, con la calculadora en grados:

```math
\theta=\arccos(-0{,}707)=135^\circ
```

Como $`135^\circ>90^\circ`$, el ángulo es obtuso, tal como predijo el signo del producto punto ✓.

---

## Ejercicio 5 — Ortogonalidad

**(a)** Un solo cálculo: el producto punto.

```math
(2,-1,3)\cdot(3,3,-1)=2(3)+(-1)(3)+3(-1)=6-3-3=0
```

Como el producto punto es cero, **sí son ortogonales**.

**(b)** Se calcula el producto punto en términos de $k$ y se iguala a cero:

```math
(k,2,-1)\cdot(3,-1,-5)=k(3)+2(-1)+(-1)(-5)=3k-2+5=3k+3
```

```math
3k+3=0\ \Rightarrow\ 3k=-3\ \Rightarrow\ k=-1
```

Verificación, sustituyendo $k=-1$ en el primer vector:

```math
(-1,2,-1)\cdot(3,-1,-5)=(-1)(3)+2(-1)+(-1)(-5)=-3-2+5=0\ \checkmark
```

**(c)** Se buscan $(x,y)$ con $(x,y)\cdot(3,4)=0$, es decir $3x+4y=0$. Hay dos incógnitas y una sola ecuación, así que se elige el valor de una y se despeja la otra. Con $x=-4$:

```math
3(-4)+4y=0\ \Rightarrow\ -12+4y=0\ \Rightarrow\ 4y=12\ \Rightarrow\ y=3
```

El vector es $(-4,3)$. Verificación:

```math
(3,4)\cdot(-4,3)=3(-4)+4(3)=-12+12=0\ \checkmark
```

El vector $(-4,3)$ no es nulo, así que cumple lo pedido. (También sirve el opuesto, $(4,-3)$.)

---

## Ejercicio 6 — Combinación lineal

**Datos:** $\mathbf{w}=(7,11)$, $`\mathbf{v}_1=(2,1)`$, $`\mathbf{v}_2=(1,3)`$.

**(a)** Se plantea la combinación lineal y se multiplican los escalares por cada vector:

```math
c_1(2,1)+c_2(1,3)=(2c_1+c_2,\ \ c_1+3c_2)=(7,11)
```

Igualando componente a componente (primera componente con primera, segunda con segunda):

```math
\begin{cases}2c_1+c_2=7 & (1)\\ c_1+3c_2=11 & (2)\end{cases}
```

**(b)** Sumar las ecuaciones directamente no cancela ninguna incógnita ($`2c_1+c_1`$ y $`c_2+3c_2`$ no se anulan). Se multiplica **toda** la ecuación (1) por $-3$ para que $`c_2`$ y $`3c_2`$ queden opuestos:

```math
-3\cdot(2c_1+c_2)=-3\cdot7\ \Rightarrow\ -6c_1-3c_2=-21\qquad(1')
```

Se suman (1') y (2), lado izquierdo con lado izquierdo y lado derecho con lado derecho:

```math
(-6c_1+c_1)+(-3c_2+3c_2)=-21+11\ \Rightarrow\ -5c_1+0=-10
```

```math
c_1=\frac{-10}{-5}=2
```

Se sustituye $`c_1=2`$ en la ecuación (1) y se despeja $`c_2`$:

```math
2(2)+c_2=7\ \Rightarrow\ 4+c_2=7\ \Rightarrow\ c_2=7-4=3
```

**(c)** Verificación en el vector original:

```math
2(2,1)+3(1,3)=(4,2)+(3,9)=(4+3,\ 2+9)=(7,11)=\mathbf{w}\ \checkmark
```

También cumple las dos ecuaciones: (1) $2(2)+3=7$ ✓ y (2) $2+3(3)=2+9=11$ ✓.

Resultado: $`\mathbf{w}=2\mathbf{v}_1+3\mathbf{v}_2`$.

---

## Ejercicio 7 — Generado

**(a)** $(6,-3,9)$ está en el generado de $`\{(2,-1,3)\}`$ si existe un escalar $c$ tal que $c(2,-1,3)=(6,-3,9)$. Se iguala componente a componente:

```math
2c=6\ \Rightarrow\ c=3\qquad-c=-3\ \Rightarrow\ c=3\qquad3c=9\ \Rightarrow\ c=3
```

El mismo $c=3$ funciona en las tres posiciones, así que **sí está** en el generado:

```math
3(2,-1,3)=(6,-3,9)\ \checkmark
```

**(b)** Se plantea $`c_1(1,0,1)+c_2(0,1,1)=(x,y,z)`$. Al multiplicar y sumar:

```math
c_1(1,0,1)+c_2(0,1,1)=(c_1,\ \ c_2,\ \ c_1+c_2)
```

Igualando con $(x,y,z)$ queda el sistema:

```math
c_1=x,\qquad c_2=y,\qquad c_1+c_2=z
```

Hay tres ecuaciones y solo dos incógnitas: las dos primeras dan $`c_1`$ y $`c_2`$, y la tercera comprueba si esos valores también funcionan en la última posición. Es la misma idea del generado de un solo vector, donde el mismo $c$ debe servir en todas las posiciones.

- **Para $(1,2,3)$:** las dos primeras ecuaciones dan $`c_1=1`$ y $`c_2=2`$. Se prueba la tercera: $1+2=3$ ✓. **Sí es combinación lineal**:

```math
1(1,0,1)+2(0,1,1)=(1,0,1)+(0,2,2)=(1,2,3)\ \checkmark
```

- **Para $(1,2,4)$:** las dos primeras ecuaciones dan $`c_1=1`$ y $`c_2=2`$. Se prueba la tercera: $1+2=3$, pero el vector pide $4$, y $3\neq4$. El sistema es inconsistente, así que **no es combinación lineal**.

---

## Ejercicio 8 — Subespacios y axiomas

**(a)** $`S=\{(x,y):y=2x\}`$. Un vector está en $S$ cuando su segunda componente es el doble de la primera; es decir, los elementos de $S$ tienen la forma $(x,2x)$. Se verifican las tres condiciones.

**1. Contiene al vector cero.** El vector $(0,0)$ cumple $y=2x$, porque $0=2\cdot0$. Entonces $\mathbf{0}\in S$.

**2. Cerrado bajo la suma.** Sean $(a,2a)$ y $(b,2b)$ en $S$. Su suma es

```math
(a,2a)+(b,2b)=(a+b,\ 2a+2b)=(a+b,\ 2(a+b))
```

La segunda componente es el doble de la primera, así que la suma tiene la forma $(x,2x)$ con $x=a+b$. Por lo tanto, la suma está en $S$.

**3. Cerrado bajo el producto por escalar.** Sea $(a,2a)\in S$ y $k\in\mathbb{R}$:

```math
k(a,2a)=(ka,\ 2ka)=(ka,\ 2(ka))
```

La segunda componente es el doble de la primera, así que el resultado tiene la forma $(x,2x)$ con $x=ka$. Por lo tanto, el resultado está en $S$.

Se cumplen las tres condiciones, así que **$S$ es subespacio de $`\mathbb{R}^2`$** (geométricamente, es la recta $y=2x$ que pasa por el origen).

**(b)** $`T=\{(x,y):y=x+1\}`$. Para mostrar que no es subespacio basta un contraejemplo de una condición. Se prueba el vector cero:

- $(0,0)\in T$ exigiría $0=0+1$, es decir $0=1$, que es falso. Entonces $(0,0)\notin T$.

$T$ no contiene al vector cero, por lo tanto **$T$ no es subespacio de $`\mathbb{R}^2`$**.

También falla la suma, como segunda comprobación:

- $(0,1)\in T$, porque $1=0+1$.
- $(1,2)\in T$, porque $2=1+1$.
- Su suma es $(0,1)+(1,2)=(1,3)$, y $3\neq1+1=2$, así que $(1,3)\notin T$.

Una recta que no pasa por el origen nunca es subespacio.

**(c)** $\mathbf{u}=(1,2)$, $\mathbf{v}=(-3,5)$, $k=4$.

Conmutatividad: $\mathbf{u}+\mathbf{v}=\mathbf{v}+\mathbf{u}$. Se calcula cada lado por separado:

```math
\mathbf{u}+\mathbf{v}=(1+(-3),\ 2+5)=(-2,\ 7)
```

```math
\mathbf{v}+\mathbf{u}=(-3+1,\ 5+2)=(-2,\ 7)
```

Ambos dan $(-2,7)$ ✓.

Distributividad sobre vectores: $k(\mathbf{u}+\mathbf{v})=k\mathbf{u}+k\mathbf{v}$.

Lado izquierdo. Se usa $\mathbf{u}+\mathbf{v}=(-2,7)$:

```math
k(\mathbf{u}+\mathbf{v})=4(-2,7)=(4\cdot(-2),\ 4\cdot7)=(-8,\ 28)
```

Lado derecho. Cada término por separado y luego la suma:

```math
k\mathbf{u}=4(1,2)=(4,\ 8)\qquad k\mathbf{v}=4(-3,5)=(-12,\ 20)
```

```math
k\mathbf{u}+k\mathbf{v}=(4+(-12),\ 8+20)=(-8,\ 28)
```

Ambos dan $(-8,28)$ ✓.

Una verificación numérica ilustra el axioma en un caso; no lo demuestra en general.

---

## Ejercicio 9 — Leer y transponer matrices

```math
A=\begin{bmatrix}2&-1&0&5\\3&4&-2&1\\0&7&6&-3\end{bmatrix}
```

**(a)** $A$ tiene 3 filas y 4 columnas: tamaño **$3\times4$**. La entrada $`a_{ij}`$ está en la fila $i$, columna $j$:

- $`a_{23}`$ (fila 2, columna 3): $-2$.
- $`a_{14}`$ (fila 1, columna 4): $5$.
- $`a_{32}`$ (fila 3, columna 2): $7$.

**(b)**

- Fila 2: se leen las entradas de izquierda a derecha, $(3,\ 4,\ -2,\ 1)$.
- Columna 3: se leen las entradas de arriba hacia abajo, $(0,\ -2,\ 6)$.

**(c)** Las filas de $A$ pasan a ser columnas: la fila 1 $(2,-1,0,5)$ es la columna 1 de $`A^T`$, la fila 2 $(3,4,-2,1)$ es la columna 2 y la fila 3 $(0,7,6,-3)$ es la columna 3.

```math
A^T=\begin{bmatrix}2&3&0\\-1&4&7\\0&-2&6\\5&1&-3\end{bmatrix}
```

Tamaño: **$4\times3$** (porque $A$ es $3\times4$, la dimensión se invierte).

$`(A^T)_{41}`$ es la fila 4, columna 1 de $`A^T`$, que vale $5$. Por la definición $`(A^T)_{ij}=a_{ji}`$, coincide con $`a_{14}=5`$ (fila 1, columna 4 de $A$) ✓.

**(d)** Se escribe $`B^T`$ pasando las filas de $B$ a columnas: la fila 1 $(1,4,-2)$ es la columna 1, la fila 2 $(4,0,5)$ es la columna 2 y la fila 3 $(-2,5,3)$ es la columna 3.

```math
B=\begin{bmatrix}1&4&-2\\4&0&5\\-2&5&3\end{bmatrix}\qquad B^T=\begin{bmatrix}1&4&-2\\4&0&5\\-2&5&3\end{bmatrix}
```

Se comparan las entradas simétricas (las que están a ambos lados de la diagonal):

- $`b_{12}=4`$ y $`b_{21}=4`$ ✓
- $`b_{13}=-2`$ y $`b_{31}=-2`$ ✓
- $`b_{23}=5`$ y $`b_{32}=5`$ ✓

Como $B=B^T$, **$B$ sí es simétrica**.

---

## Ejercicio 10 — Sumar y escalar matrices

```math
A=\begin{bmatrix}1&-2&0\\3&4&5\end{bmatrix}\qquad B=\begin{bmatrix}2&1&-1\\0&-3&2\end{bmatrix}
```

**(a)** Se suman las entradas que ocupan la misma posición:

```math
A+B=\begin{bmatrix}1+2&-2+1&0+(-1)\\3+0&4+(-3)&5+2\end{bmatrix}=\begin{bmatrix}3&-1&-1\\3&1&7\end{bmatrix}
```

**(b)** Primero se multiplica cada entrada por el escalar:

```math
3A=\begin{bmatrix}3\cdot1&3(-2)&3\cdot0\\3\cdot3&3\cdot4&3\cdot5\end{bmatrix}=\begin{bmatrix}3&-6&0\\9&12&15\end{bmatrix}
```

```math
2B=\begin{bmatrix}2\cdot2&2\cdot1&2(-1)\\2\cdot0&2(-3)&2\cdot2\end{bmatrix}=\begin{bmatrix}4&2&-2\\0&-6&4\end{bmatrix}
```

Luego se restan entrada por entrada:

```math
3A-2B=\begin{bmatrix}3-4&-6-2&0-(-2)\\9-0&12-(-6)&15-4\end{bmatrix}=\begin{bmatrix}-1&-8&2\\9&18&11\end{bmatrix}
```

**(c)** Se despeja $X$ igual que con vectores: se suma el opuesto de $A$ a ambos lados:

```math
A+X=B\ \Rightarrow\ A+X-A=B-A\ \Rightarrow\ X=B-A
```

Entrada por entrada:

```math
X=B-A=\begin{bmatrix}2-1&1-(-2)&-1-0\\0-3&-3-4&2-5\end{bmatrix}=\begin{bmatrix}1&3&-1\\-3&-7&-3\end{bmatrix}
```

Verificación: se suma $A+X$ y debe dar $B$.

```math
A+X=\begin{bmatrix}1+1&-2+3&0+(-1)\\3+(-3)&4+(-7)&5+(-3)\end{bmatrix}=\begin{bmatrix}2&1&-1\\0&-3&2\end{bmatrix}=B\ \checkmark
```

**(d)** Se calcula cada lado por separado.

Lado izquierdo. Se transpone el resultado del inciso (a) (las filas pasan a ser columnas):

```math
(A+B)^T=\begin{bmatrix}3&3\\-1&1\\-1&7\end{bmatrix}
```

Lado derecho. Primero las transpuestas de $A$ y $B$:

```math
A^T=\begin{bmatrix}1&3\\-2&4\\0&5\end{bmatrix}\qquad B^T=\begin{bmatrix}2&0\\1&-3\\-1&2\end{bmatrix}
```

Luego se suman entrada por entrada:

```math
A^T+B^T=\begin{bmatrix}1+2&3+0\\-2+1&4+(-3)\\0+(-1)&5+2\end{bmatrix}=\begin{bmatrix}3&3\\-1&1\\-1&7\end{bmatrix}
```

Ambos lados coinciden ✓.

---

# Parte B — Problemas de datos e inteligencia artificial

## Ejercicio 11 — Red neuronal: actualización de pesos

```math
W=\begin{bmatrix}0{,}5&-0{,}2&0{,}8\\1&0{,}3&-0{,}6\end{bmatrix}\qquad G_1=\begin{bmatrix}2&-1&4\\-3&0&5\end{bmatrix}\qquad G_2=\begin{bmatrix}0&3&-2\\1&-1&-3\end{bmatrix}\qquad\eta=0{,}1
```

(Filas: neurona 1 y neurona 2. Columnas: variables $`x_1`$, $`x_2`$, $`x_3`$.)

**(a)** $W$ tiene 2 filas (neuronas) y 3 columnas (variables de entrada): tamaño **$2\times3$**. La entrada $`w_{23}`$ está en la fila 2, columna 3, y vale $-0{,}6$. Significa que $`w_{23}`$ es **el peso con que la neurona 2 usa la variable $`x_3`$**.

**(b)** Las filas de $W$ pasan a ser columnas: la fila 1 $(0{,}5;\ -0{,}2;\ 0{,}8)$ es la columna 1 de $`W^T`$ y la fila 2 $(1;\ 0{,}3;\ -0{,}6)$ es la columna 2.

```math
W^T=\begin{bmatrix}0{,}5&1\\-0{,}2&0{,}3\\0{,}8&-0{,}6\end{bmatrix}
```

Tamaño: **$3\times2$**. Ahora **cada fila corresponde a una variable de entrada** ($`x_1`$, $`x_2`$, $`x_3`$) y muestra los pesos que le dan la neurona 1 y la neurona 2; las columnas son las neuronas.

**(c)** Primero se suman los gradientes de los dos lotes, entrada por entrada:

```math
G_1+G_2=\begin{bmatrix}2+0&-1+3&4+(-2)\\-3+1&0+(-1)&5+(-3)\end{bmatrix}=\begin{bmatrix}2&2&2\\-2&-1&2\end{bmatrix}
```

Luego se multiplica por $\tfrac12$ (se divide cada entrada entre 2):

```math
\bar{G}=\tfrac12(G_1+G_2)=\begin{bmatrix}1&1&1\\-1&-0{,}5&1\end{bmatrix}
```

**(d)** Primero se escala el gradiente promedio por $\eta=0{,}1$:

```math
0{,}1\bar{G}=\begin{bmatrix}0{,}1\cdot1&0{,}1\cdot1&0{,}1\cdot1\\0{,}1(-1)&0{,}1(-0{,}5)&0{,}1\cdot1\end{bmatrix}=\begin{bmatrix}0{,}1&0{,}1&0{,}1\\-0{,}1&-0{,}05&0{,}1\end{bmatrix}
```

Luego se resta de $W$ entrada por entrada:

```math
W_{\text{nueva}}=W-0{,}1\bar{G}=\begin{bmatrix}0{,}5-0{,}1&-0{,}2-0{,}1&0{,}8-0{,}1\\1-(-0{,}1)&0{,}3-(-0{,}05)&-0{,}6-0{,}1\end{bmatrix}=\begin{bmatrix}0{,}4&-0{,}3&0{,}7\\1{,}1&0{,}35&-0{,}7\end{bmatrix}
```

**(e)** Se calcula la entrada $(3,2)$ de cada lado de $`(W_{\text{nueva}})^T=W^T-0{,}1\bar{G}^T`$.

Lado izquierdo. La entrada $(3,2)$ de una transpuesta es la entrada $(2,3)$ de la matriz original:

```math
\big((W_{\text{nueva}})^T\big)_{32}=(W_{\text{nueva}})_{23}=-0{,}7
```

Lado derecho. Cada término por separado:

```math
(W^T)_{32}=w_{23}=-0{,}6\qquad(\bar{G}^T)_{32}=\bar{g}_{23}=1
```

```math
(W^T-0{,}1\bar{G}^T)_{32}=-0{,}6-0{,}1\cdot1=-0{,}6-0{,}1=-0{,}7
```

Ambos lados dan $-0{,}7$ ✓.

**Interpretación:** el peso que la neurona 2 da a $`x_3`$ pasó de $-0{,}6$ a $-0{,}7$, es decir, se volvió más negativo. El gradiente promedio en esa posición es positivo ($+1$), y el descenso de gradiente mueve el peso en sentido contrario al gradiente para reducir el error; la tasa $\eta=0{,}1$ controla qué tan grande es ese paso.

---

## Ejercicio 12 — Clasificador de correos: matrices de confusión

```math
M_1=\begin{bmatrix}90&10\\20&80\end{bmatrix}\qquad M_2=\begin{bmatrix}85&15\\25&75\end{bmatrix}
```

(Filas: clase real, en el orden spam y no spam. Columnas: clase predicha, en el mismo orden.)

**(a)** $`M_1`$ tiene 2 filas y 2 columnas: tamaño **$2\times2$**.

- $`m_{12}=10`$ (fila 1, columna 2): correos **realmente spam** que el modelo **predijo como no spam** (spam que se le escapó al filtro).
- $`m_{21}=20`$ (fila 2, columna 1): correos **realmente no spam** que el modelo **predijo como spam** (correos legítimos marcados como spam por error).

**(b)** Se suman las entradas que ocupan la misma posición:

```math
S=M_1+M_2=\begin{bmatrix}90+85&10+15\\20+25&80+75\end{bmatrix}=\begin{bmatrix}175&25\\45&155\end{bmatrix}
```

Suma de todas las entradas:

```math
175+25+45+155=400\ \checkmark
```

que son los 400 correos de los dos lotes (200 + 200).

**(c)** La diagonal principal de $S$ tiene los aciertos: $175$ (spam detectado como spam) y $155$ (no spam clasificado como no spam). Se suman y se divide entre el total:

```math
\text{exactitud}=\frac{175+155}{400}=\frac{330}{400}=0{,}825=82{,}5\ \%
```

**Interpretación:** el modelo clasifica correctamente aproximadamente 8 de cada 10 correos (82,5 %).

**(d)** Se multiplica cada entrada de $S$ por $\tfrac{1}{400}$ (se divide cada entrada entre 400):

```math
P=\frac{1}{400}S=\begin{bmatrix}\frac{175}{400}&\frac{25}{400}\\[2pt]\frac{45}{400}&\frac{155}{400}\end{bmatrix}=\begin{bmatrix}0{,}4375&0{,}0625\\0{,}1125&0{,}3875\end{bmatrix}
```

Comprobación: las entradas suman $0{,}4375+0{,}0625+0{,}1125+0{,}3875=1$ ✓. Cada entrada es la proporción de los 400 correos que cae en esa celda.

**(e)** Las filas de $S$ pasan a ser columnas: la fila 1 $(175,25)$ es la columna 1 de $`S^T`$ y la fila 2 $(45,155)$ es la columna 2.

```math
S^T=\begin{bmatrix}175&45\\25&155\end{bmatrix}
```

La transposición **intercambia filas por columnas**: en $`S^T`$ las filas pasan a ser la clase predicha y las columnas la clase real.

Por la definición $`(S^T)_{ij}=s_{ji}`$, la entrada $`(S^T)_{12}`$ corresponde a $`s_{21}=45`$. Son los **45 correos realmente no spam que el modelo predijo como spam** (falsas alarmas). En $`S^T`$ se lee como fila 1 = predicho spam, columna 2 = real no spam.
