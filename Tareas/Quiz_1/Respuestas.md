# Quiz en casa #1 — Vectores, producto punto, combinaciones lineales y matrices

## Fórmulas usadas

| Concepto | Fórmula |
|---|---|
| Norma | $`\lVert\mathbf{v}\rVert=\sqrt{\mathbf{v}\cdot\mathbf{v}}=\sqrt{v_1^2+\cdots+v_n^2}`$ |
| Distancia | $d(\mathbf{u},\mathbf{v})=\lVert\mathbf{u}-\mathbf{v}\rVert$ |
| Producto punto | $`\mathbf{u}\cdot\mathbf{v}=u_1v_1+\cdots+u_nv_n`$ |
| Ángulo | $\cos\theta=\dfrac{\mathbf{u}\cdot\mathbf{v}}{\lVert\mathbf{u}\rVert\lVert\mathbf{v}\rVert}$ |
| Ortogonalidad | $\mathbf{u}\perp\mathbf{v}\iff\mathbf{u}\cdot\mathbf{v}=0$ |
| Transpuesta | $`(A^\top)_{ij}=a_{ji}`$ |
| Suma y escalar | $`(A+B)_{ij}=a_{ij}+b_{ij}`$, $`\quad(kA)_{ij}=k\cdot a_{ij}`$ |

---

# Parte A — Ejercicios base

## Ejercicio 1 — Norma

**Datos:** $`\mathbf{u}=(2,-3,6)`$.

**(a)**

```math
\lVert\mathbf{u}\rVert=\sqrt{2^2+(-3)^2+6^2}=\sqrt{4+9+36}=\sqrt{49}=7
```

**(b)** Se divide cada componente entre la norma:

```math
\hat{\mathbf{u}}=\frac{\mathbf{u}}{7}=\left(\tfrac{2}{7},\ -\tfrac{3}{7},\ \tfrac{6}{7}\right)
```

```math
\lVert\hat{\mathbf{u}}\rVert=\sqrt{\tfrac{4}{49}+\tfrac{9}{49}+\tfrac{36}{49}}=\sqrt{\tfrac{49}{49}}=\sqrt{1}=1\ \checkmark
```

**(c)** Directamente: $`-3\mathbf{u}=(-6,\ 9,\ -18)`$.

```math
\lVert-3\mathbf{u}\rVert=\sqrt{36+81+324}=\sqrt{441}=21
```

Con la propiedad: $`\lvert-3\rvert\cdot\lVert\mathbf{u}\rVert=3\cdot7=21`$.

**Conclusión:** coinciden, $`\lVert k\mathbf{u}\rVert=\lvert k\rvert\cdot\lVert\mathbf{u}\rVert`$. El signo negativo invierte el sentido pero no cambia la longitud.

---

## Ejercicio 2 — Distancia

**(a)** $A=(1,4,-2)$ y $B=(3,0,-1)$.

```math
A-B=(1-3,\ 4-0,\ -2-(-1))=(-2,\ 4,\ -1)
```

```math
d(A,B)=\sqrt{4+16+1}=\sqrt{21}\approx4{,}583
```

**(b)** Se iguala la distancia a 5 y se eleva al cuadrado:

```math
d\big((2,k),(5,-1)\big)=\sqrt{(2-5)^2+(k-(-1))^2}=\sqrt{9+(k+1)^2}=5
```

```math
9+(k+1)^2=25\ \Rightarrow\ (k+1)^2=16\ \Rightarrow\ k+1=4\ \text{ o }\ k+1=-4
```

```math
k=3\ \text{ o }\ k=-5
```

Verificación: con $k=3$, $`\sqrt{9+16}=5`$; con $k=-5$, $`\sqrt{9+(-4)^2}=\sqrt{25}=5`$ ✓.

---

## Ejercicio 3 — Producto punto

**Datos:** $`\mathbf{a}=(1,-2,3)`$, $`\mathbf{b}=(4,1,-2)`$, $`\mathbf{c}=(2,3,1)`$.

**(a)**

```math
\mathbf{a}\cdot\mathbf{b}=1(4)+(-2)(1)+3(-2)=4-2-6=-4
```

```math
\mathbf{a}\cdot\mathbf{c}=1(2)+(-2)(3)+3(1)=2-6+3=-1
```

**(b)** Distributiva $`\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}`$.

Lado izquierdo:

```math
\mathbf{b}+\mathbf{c}=(6,\ 4,\ -1)\qquad\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=6-8-3=-5
```

Lado derecho:

```math
\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}=-4+(-1)=-5
```

Ambos lados dan $-5$ ✓.

**(c)** $`(2\mathbf{a})\cdot\mathbf{c}`$ de dos maneras:

- Escalando primero: $`2\mathbf{a}=(2,-4,6)`$, entonces $2(2)+(-4)(3)+6(1)=4-12+6=-2$.
- Con la propiedad: $`2(\mathbf{a}\cdot\mathbf{c})=2(-1)=-2`$.

Coinciden ✓.

Positividad: $`\mathbf{a}\cdot\mathbf{a}=1+4+9=14`$ y $`\lVert\mathbf{a}\rVert^2=\left(\sqrt{1+4+9}\right)^2=14`$ ✓.

---

## Ejercicio 4 — Ángulo

**(a)** $`\mathbf{u}=(1,1,0)`$, $`\mathbf{v}=(0,1,1)`$.

```math
\mathbf{u}\cdot\mathbf{v}=0+1+0=1\qquad\lVert\mathbf{u}\rVert=\lVert\mathbf{v}\rVert=\sqrt2
```

```math
\cos\theta=\frac{1}{\sqrt2\cdot\sqrt2}=\frac12=0{,}5\ \Rightarrow\ \theta=60^\circ
```

**(b)** $`\mathbf{u}=(-2,1)`$, $`\mathbf{v}=(1,-3)`$.

Predicción por el signo: $`\mathbf{u}\cdot\mathbf{v}=-2-3=-5<0`$, por lo tanto el ángulo es **obtuso**.

Confirmación:

```math
\lVert\mathbf{u}\rVert=\sqrt5\qquad\lVert\mathbf{v}\rVert=\sqrt{10}\qquad\cos\theta=\frac{-5}{\sqrt5\cdot\sqrt{10}}=\frac{-5}{\sqrt{50}}=\frac{-5}{5\sqrt2}=-\frac{\sqrt2}{2}\approx-0{,}707
```

```math
\theta=\arccos(-0{,}707)=135^\circ>90^\circ\ \checkmark
```

---

## Ejercicio 5 — Ortogonalidad

**(a)** $`(2,-1,3)\cdot(3,3,-1)=6-3-3=0`$.

Como el producto punto es cero, **sí son ortogonales**.

**(b)** Se iguala el producto punto a cero:

```math
(k,2,-1)\cdot(3,-1,-5)=3k-2+5=3k+3=0\ \Rightarrow\ k=-1
```

Verificación: $`(-1,2,-1)\cdot(3,-1,-5)=-3-2+5=0`$ ✓.

**(c)** Para $(3,4)$ se intercambian las componentes y se cambia el signo de una: $`\mathbf{w}=(-4,3)`$.

```math
(3,4)\cdot(-4,3)=-12+12=0\ \checkmark
```

Cualquier múltiplo de $(-4,3)$ también sirve (los vectores de la recta perpendicular por el origen).

---

## Ejercicio 6 — Combinación lineal

**Datos:** $`\mathbf{w}=(7,11)`$, $`\mathbf{v}_1=(2,1)`$, $`\mathbf{v}_2=(1,3)`$.

**(a)** Se plantea $`c_1(2,1)+c_2(1,3)=(7,11)`$ y se separa por componentes:

```math
\begin{cases}2c_1+c_2=7 & (1)\\ c_1+3c_2=11 & (2)\end{cases}
```

**(b)** Sumar directamente no cancela nada. Se multiplica **toda** la ecuación (1) por $-3$ para que $`c_2`$ quede con coeficientes opuestos:

```math
-6c_1-3c_2=-21\qquad(1')
```

Se suma (1') con (2), término a término:

```math
-5c_1+0=-10\ \Rightarrow\ c_1=2
```

Se sustituye en (1): $`2(2)+c_2=7\Rightarrow c_2=3`$.

**(c)** Verificación:

```math
2(2,1)+3(1,3)=(4,2)+(3,9)=(7,11)=\mathbf{w}\ \checkmark
```

Resultado: $`\mathbf{w}=2\mathbf{v}_1+3\mathbf{v}_2`$.

---

## Ejercicio 7 — Generado

**(a)** Se busca $c$ con $c(2,-1,3)=(6,-3,9)$:

```math
2c=6,\quad -c=-3,\quad 3c=9\ \Rightarrow\ c=3\ \text{ en las tres posiciones}
```

**Sí está** en el generado: $(6,-3,9)=3(2,-1,3)$.

**(b)** Se plantea $`c_1(1,0,1)+c_2(0,1,1)=(x,y,z)`$, es decir $`c_1=x`$, $`c_2=y`$, $`c_1+c_2=z`$.

- Para $(1,2,3)$: $`c_1=1`$, $`c_2=2`$, y la tercera ecuación $1+2=3$ ✓. **Sí es combinación lineal**: $(1,2,3)=1(1,0,1)+2(0,1,1)$.
- Para $(1,2,4)$: $`c_1=1`$, $`c_2=2`$, pero la tercera pide $1+2=4$, que es falso. El sistema es inconsistente: **no es combinación lineal**.

---

## Ejercicio 8 — Subespacios y axiomas

**(a)** $`S=\{(x,y):y=2x\}=\{(x,2x)\}`$. Se verifican las tres condiciones:

1. **Cero:** con $x=0$, $`(0,0)=(0,2\cdot0)\in S`$ ✓.
2. **Suma:** si $(a,2a)$ y $(b,2b)$ están en $S$,

```math
(a,2a)+(b,2b)=(a+b,\ 2a+2b)=(a+b,\ 2(a+b))\in S\ \checkmark
```

3. **Escalar:** si $`(a,2a)\in S`$ y $`k\in\mathbb{R}`$,

```math
k(a,2a)=(ka,\ 2ka)=(ka,\ 2(ka))\in S\ \checkmark
```

Por lo tanto **$S$ es subespacio de $`\mathbb{R}^2`$** (es la recta $y=2x$ por el origen).

**(b)** $`T=\{(x,y):y=x+1\}`$ **no** es subespacio porque **no contiene al vector cero**: $(0,0)$ exigiría $0=0+1$, que es falso. (También falla la suma: $(0,1)$ y $(1,2)$ están en $T$, pero $(0,1)+(1,2)=(1,3)$ no, ya que $`3\neq1+1`$.) Una recta que no pasa por el origen nunca es subespacio.

**(c)** $`\mathbf{u}=(1,2)`$, $`\mathbf{v}=(-3,5)`$, $k=4$.

Conmutativa:

```math
\mathbf{u}+\mathbf{v}=(1-3,\ 2+5)=(-2,\ 7)\qquad\mathbf{v}+\mathbf{u}=(-3+1,\ 5+2)=(-2,\ 7)\ \checkmark
```

Distributiva sobre vectores:

```math
k(\mathbf{u}+\mathbf{v})=4(-2,7)=(-8,\ 28)
```

```math
k\mathbf{u}+k\mathbf{v}=(4,8)+(-12,20)=(-8,\ 28)\ \checkmark
```

Una verificación numérica ilustra el axioma en un caso; no lo demuestra en general.

---

## Ejercicio 9 — Leer y transponer matrices

```math
A=\begin{bmatrix}2&-1&0&5\\3&4&-2&1\\0&7&6&-3\end{bmatrix}
```

**(a)** $A$ tiene 3 filas y 4 columnas: es de tamaño $`3\times4`$.

- $`a_{23}`$ (fila 2, columna 3) $=-2$
- $`a_{14}`$ (fila 1, columna 4) $=5$
- $`a_{32}`$ (fila 3, columna 2) $=7$

**(b)**

- Fila 2 $`=(3,\ 4,\ -2,\ 1)`$
- Columna 3 $`=(0,\ -2,\ 6)`$

**(c)** Cada fila de $A$ pasa a ser columna, conservando el orden:

```math
A^\top=\begin{bmatrix}2&3&0\\-1&4&7\\0&-2&6\\5&1&-3\end{bmatrix}
```

Su tamaño es $`4\times3`$ (la dimensión se invierte). Además $`(A^\top)_{41}=a_{14}=5`$: es la entrada de la fila 4, columna 1 de $`A^\top`$, que coincide con $`a_{14}`$.

**(d)**

```math
B=\begin{bmatrix}1&4&-2\\4&0&5\\-2&5&3\end{bmatrix}\qquad B^\top=\begin{bmatrix}1&4&-2\\4&0&5\\-2&5&3\end{bmatrix}
```

Se compara entrada por entrada: $`b_{12}=b_{21}=4`$, $`b_{13}=b_{31}=-2`$ y $`b_{23}=b_{32}=5`$. Como $`B=B^\top`$, **$B$ sí es simétrica**.

---

## Ejercicio 10 — Sumar y escalar matrices

```math
A=\begin{bmatrix}1&-2&0\\3&4&5\end{bmatrix}\qquad B=\begin{bmatrix}2&1&-1\\0&-3&2\end{bmatrix}
```

**(a)**

```math
A+B=\begin{bmatrix}1+2&-2+1&0+(-1)\\3+0&4+(-3)&5+2\end{bmatrix}=\begin{bmatrix}3&-1&-1\\3&1&7\end{bmatrix}
```

**(b)** Primero se escala y luego se resta:

```math
3A=\begin{bmatrix}3&-6&0\\9&12&15\end{bmatrix}\qquad2B=\begin{bmatrix}4&2&-2\\0&-6&4\end{bmatrix}
```

```math
3A-2B=\begin{bmatrix}3-4&-6-2&0-(-2)\\9-0&12-(-6)&15-4\end{bmatrix}=\begin{bmatrix}-1&-8&2\\9&18&11\end{bmatrix}
```

**(c)** Se despeja sumando el opuesto de $A$ a ambos lados: $X=B-A$.

```math
X=\begin{bmatrix}2-1&1-(-2)&-1-0\\0-3&-3-4&2-5\end{bmatrix}=\begin{bmatrix}1&3&-1\\-3&-7&-3\end{bmatrix}
```

Verificación: $`A+X=\begin{bmatrix}1+1&-2+3&0-1\\3-3&4-7&5-3\end{bmatrix}=\begin{bmatrix}2&1&-1\\0&-3&2\end{bmatrix}=B`$ ✓.

**(d)** Lado izquierdo:

```math
(A+B)^\top=\begin{bmatrix}3&3\\-1&1\\-1&7\end{bmatrix}
```

Lado derecho:

```math
A^\top=\begin{bmatrix}1&3\\-2&4\\0&5\end{bmatrix}\qquad B^\top=\begin{bmatrix}2&0\\1&-3\\-1&2\end{bmatrix}\qquad A^\top+B^\top=\begin{bmatrix}3&3\\-1&1\\-1&7\end{bmatrix}
```

Ambos lados coinciden ✓.

---

# Parte B — Problemas de datos e inteligencia artificial

## Ejercicio 11 — Red neuronal: actualización de pesos

```math
W=\begin{bmatrix}0{,}5&-0{,}2&0{,}8\\1&0{,}3&-0{,}6\end{bmatrix}\quad G_1=\begin{bmatrix}2&-1&4\\-3&0&5\end{bmatrix}\quad G_2=\begin{bmatrix}0&3&-2\\1&-1&-3\end{bmatrix}\quad\eta=0{,}1
```

**(a)** $W$ es de tamaño $`2\times3`$ (2 neuronas, 3 variables de entrada). La entrada $`w_{23}=-0{,}6`$ es **el peso con que la neurona 2 usa la variable $`x_3`$**.

**(b)** Cada fila de $W$ pasa a ser columna:

```math
W^\top=\begin{bmatrix}0{,}5&1\\-0{,}2&0{,}3\\0{,}8&-0{,}6\end{bmatrix}
```

Es de tamaño $`3\times2`$. Ahora **cada fila corresponde a una variable de entrada** ($`x_1`$, $`x_2`$, $`x_3`$) y muestra los pesos que le dan la neurona 1 y la neurona 2; las columnas son las neuronas.

**(c)** Gradiente promedio:

```math
G_1+G_2=\begin{bmatrix}2+0&-1+3&4-2\\-3+1&0-1&5-3\end{bmatrix}=\begin{bmatrix}2&2&2\\-2&-1&2\end{bmatrix}
```

```math
\bar{G}=\tfrac12(G_1+G_2)=\begin{bmatrix}1&1&1\\-1&-0{,}5&1\end{bmatrix}
```

**(d)** Primero se escala el gradiente: $`0{,}1\bar{G}=\begin{bmatrix}0{,}1&0{,}1&0{,}1\\-0{,}1&-0{,}05&0{,}1\end{bmatrix}`$. Luego se resta entrada por entrada:

```math
W_{\text{nueva}}=W-0{,}1\bar{G}=\begin{bmatrix}0{,}5-0{,}1&-0{,}2-0{,}1&0{,}8-0{,}1\\1-(-0{,}1)&0{,}3-(-0{,}05)&-0{,}6-0{,}1\end{bmatrix}=\begin{bmatrix}0{,}4&-0{,}3&0{,}7\\1{,}1&0{,}35&-0{,}7\end{bmatrix}
```

**(e)** La entrada $(3,2)$ de $`(W_{\text{nueva}})^\top`$ es la entrada $(2,3)$ de $`W_{\text{nueva}}`$, es decir $-0{,}7$.

Por el otro lado: $`(W^\top)_{32}=w_{23}=-0{,}6`$ y $`(\bar{G}^\top)_{32}=\bar{g}_{23}=1`$, así que

```math
(W^\top-0{,}1\bar{G}^\top)_{32}=-0{,}6-0{,}1\cdot1=-0{,}7\ \checkmark
```

Coinciden, lo que confirma $`(W_{\text{nueva}})^\top=W^\top-0{,}1\bar{G}^\top`$ en esa entrada.

**Interpretación:** el peso que la neurona 2 da a $`x_3`$ pasó de $-0{,}6$ a $-0{,}7$, es decir, se volvió más negativo. El gradiente promedio en esa posición es positivo ($+1$), y el descenso de gradiente mueve el peso en sentido contrario al gradiente para reducir el error; la tasa $`\eta=0{,}1`$ controla qué tan grande es ese paso.

---

## Ejercicio 12 — Clasificador de correos: matrices de confusión

```math
M_1=\begin{bmatrix}90&10\\20&80\end{bmatrix}\qquad M_2=\begin{bmatrix}85&15\\25&75\end{bmatrix}
```

Filas: clase real (spam, no spam). Columnas: clase predicha (spam, no spam).

**(a)** $`M_1`$ es de tamaño $`2\times2`$.

- $`m_{12}=10`$ (fila 1, columna 2): correos **realmente spam** que el modelo **predijo como no spam** (spam que se le escapó al filtro).
- $`m_{21}=20`$ (fila 2, columna 1): correos **realmente no spam** que el modelo **predijo como spam** (correos legítimos marcados como spam por error).

**(b)**

```math
S=M_1+M_2=\begin{bmatrix}90+85&10+15\\20+25&80+75\end{bmatrix}=\begin{bmatrix}175&25\\45&155\end{bmatrix}
```

Suma de todas las entradas: $175+25+45+155=400$ ✓ (los 400 correos de los dos lotes).

**(c)** La diagonal principal tiene los aciertos (spam bien detectado y no spam bien clasificado):

```math
\text{exactitud}=\frac{175+155}{400}=\frac{330}{400}=0{,}825=82{,}5\ \%
```

**Interpretación:** el modelo clasifica correctamente aproximadamente 8 de cada 10 correos (82,5 %).

**(d)**

```math
P=\frac{1}{400}S=\begin{bmatrix}\frac{175}{400}&\frac{25}{400}\\\frac{45}{400}&\frac{155}{400}\end{bmatrix}=\begin{bmatrix}0{,}4375&0{,}0625\\0{,}1125&0{,}3875\end{bmatrix}
```

Las entradas suman $0{,}4375+0{,}0625+0{,}1125+0{,}3875=1$ ✓: cada una es la proporción de los 400 correos que cae en esa celda.

**(e)**

```math
S^\top=\begin{bmatrix}175&45\\25&155\end{bmatrix}
```

La transposición **intercambia filas por columnas**: en $`S^\top`$ las filas pasan a ser la clase predicha y las columnas la clase real.

Como $`(S^\top)_{12}=s_{21}=45`$, esa entrada corresponde a $`s_{21}`$ de $S$: son los **45 correos realmente no spam que el modelo predijo como spam** (falsas alarmas). En $`S^\top`$ se lee como fila 1 = predicho spam, columna 2 = real no spam.
