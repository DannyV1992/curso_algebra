# Quiz 2 — Vectores, combinaciones lineales, subespacios, proyección y matrices

## Fórmulas usadas

| Concepto | Fórmula |
|---|---|
| Norma | $`\lVert\mathbf{v}\rVert=\sqrt{v_1^2+\cdots+v_n^2}`$ |
| Distancia | $d(\mathbf{u},\mathbf{v})=\lVert\mathbf{u}-\mathbf{v}\rVert$ |
| Producto punto | $`\mathbf{u}\cdot\mathbf{v}=u_1v_1+\cdots+u_nv_n`$, y $\mathbf{v}\cdot\mathbf{v}=\lVert\mathbf{v}\rVert^2$ |
| Ángulo / coseno | $\cos\theta=\dfrac{\mathbf{u}\cdot\mathbf{v}}{\lVert\mathbf{u}\rVert\lVert\mathbf{v}\rVert}$ |
| Ortogonalidad | $\mathbf{u}\perp\mathbf{v}\iff\mathbf{u}\cdot\mathbf{v}=0$ |
| Proyección ortogonal | $`\mathrm{proj}_{\mathbf{b}}\mathbf{a}=\dfrac{\mathbf{a}\cdot\mathbf{b}}{\mathbf{b}\cdot\mathbf{b}}\,\mathbf{b}`$, residuo $\mathbf{r}=\mathbf{a}-\mathrm{proj}_{\mathbf{b}}\mathbf{a}$ |
| Transpuesta | $`(A^T)_{ij}=a_{ji}`$ |
| Suma y escalar | $`(A+B)_{ij}=a_{ij}+b_{ij}`$, $`(kA)_{ij}=k\,a_{ij}`$ |
| Producto de matrices | $`(AB)_{ij}=\text{fila }i\text{ de }A\cdot\text{columna }j\text{ de }B`$; $(m\times n)(n\times p)=(m\times p)$ |

---

# Parte A — Quiz en clase

## Ejercicio 1 — Vectores en $\mathbb{R}^3$: norma, distancia, ángulo y ortogonalidad

**Datos:** $\mathbf{u}=(2,-1,2)$ y $\mathbf{v}=(1,2,2)$.

**(a)** Se eleva al cuadrado cada componente, se suman y se saca la raíz:

```math
2^2=4\qquad(-1)^2=1\qquad2^2=4
```

```math
\lVert\mathbf{u}\rVert=\sqrt{4+1+4}=\sqrt9=3
```

Para el vector unitario se divide **cada componente** entre la norma:

```math
\hat{\mathbf{u}}=\frac{\mathbf{u}}{3}=\left(\tfrac23,\ -\tfrac13,\ \tfrac23\right)
```

Verificación (la norma de $\hat{\mathbf{u}}$ debe ser 1):

```math
\lVert\hat{\mathbf{u}}\rVert=\sqrt{\tfrac49+\tfrac19+\tfrac49}=\sqrt{\tfrac99}=1\ \checkmark
```

**(b)** La distancia es la norma de la resta. Se resta componente a componente:

```math
\mathbf{u}-\mathbf{v}=(2-1,\ -1-2,\ 2-2)=(1,\ -3,\ 0)
```

```math
d(\mathbf{u},\mathbf{v})=\sqrt{1^2+(-3)^2+0^2}=\sqrt{1+9+0}=\sqrt{10}\approx3{,}162
```

**(c)** Producto punto (componente 1 con 1, 2 con 2, 3 con 3, y se suma):

```math
\mathbf{u}\cdot\mathbf{v}=2(1)+(-1)(2)+2(2)=2-2+4=4
```

La norma de $\mathbf{u}$ es $3$ (inciso a) y la de $\mathbf{v}$ es:

```math
\lVert\mathbf{v}\rVert=\sqrt{1^2+2^2+2^2}=\sqrt{1+4+4}=\sqrt9=3
```

Se sustituye en la fórmula del coseno:

```math
\cos\theta=\frac{4}{3\cdot3}=\frac49\approx0{,}4444
```

```math
\theta=\arccos\left(\tfrac49\right)\approx63{,}61^\circ
```

Como el producto punto es positivo ($4>0$), el ángulo es agudo, y $63{,}61^\circ<90^\circ$ lo confirma ✓.

**(d)** Se calcula $\mathbf{w}\cdot\mathbf{u}$ en términos de $k$ y se iguala a cero:

```math
(k,1,-1)\cdot(2,-1,2)=k(2)+1(-1)+(-1)(2)=2k-1-2=2k-3
```

```math
2k-3=0\ \Rightarrow\ 2k=3\ \Rightarrow\ k=\tfrac32=1{,}5
```

Verificación, con $k=1{,}5$:

```math
(1{,}5;\ 1;\ -1)\cdot(2,-1,2)=3-1-2=0\ \checkmark
```

---

## Ejercicio 2 — Combinaciones lineales, generado, subespacios y proyección

**(a)** **Datos:** $\mathbf{w}=(4,7)$, $`\mathbf{v}_1=(2,1)`$, $`\mathbf{v}_2=(1,3)`$.

Se plantea la combinación lineal y se multiplican los escalares por cada vector:

```math
c_1(2,1)+c_2(1,3)=(2c_1+c_2,\ \ c_1+3c_2)=(4,7)
```

Igualando componente a componente (primera con primera, segunda con segunda):

```math
\begin{cases}2c_1+c_2=4 & (1)\\ c_1+3c_2=7 & (2)\end{cases}
```

**Método de suma.** Sumar tal cual no cancela nada. Se multiplica **toda** la ecuación (1) por $-3$ para que $`c_2`$ y $`3c_2`$ queden opuestos:

```math
-3(2c_1+c_2)=-3\cdot4\ \Rightarrow\ -6c_1-3c_2=-12\qquad(1')
```

Se suman (1') y (2), lado con lado:

```math
(-6c_1+c_1)+(-3c_2+3c_2)=-12+7\ \Rightarrow\ -5c_1=-5\ \Rightarrow\ c_1=1
```

Se sustituye $`c_1=1`$ en (1) y se despeja $`c_2`$:

```math
2(1)+c_2=4\ \Rightarrow\ c_2=4-2=2
```

Verificación en el vector original:

```math
1(2,1)+2(1,3)=(2,1)+(2,6)=(4,7)=\mathbf{w}\ \checkmark
```

Resultado: $`\mathbf{w}=1\mathbf{v}_1+2\mathbf{v}_2`$.

**¿Por qué $`\mathbf{v}_1`$ y $`\mathbf{v}_2`$ generan todo $\mathbb{R}^2$?** Porque ninguno es múltiplo del otro (no apuntan en la misma dirección): no existe $k$ con $(2,1)=k(1,3)$, ya que $2=k$ exigiría $1=3k=6$, que es falso. Dos vectores no paralelos de $\mathbb{R}^2$ generan todo el plano. Se puede comprobar con un vector cualquiera $(x,y)$. El mismo procedimiento da:

```math
2c_1+c_2=x,\quad c_1+3c_2=y\ \Rightarrow\ -5c_1=y-3x\ \Rightarrow\ c_1=\frac{3x-y}{5},\qquad c_2=\frac{2y-x}{5}
```

Los coeficientes siempre existen (solo se divide entre $5\neq0$), así que **todo** $(x,y)$ es combinación lineal de $`\mathbf{v}_1`$ y $`\mathbf{v}_2`$. Con $(x,y)=(4,7)$ da $`c_1=\tfrac{12-7}{5}=1`$ y $`c_2=\tfrac{14-4}{5}=2`$, igual que arriba ✓.

**(b)** $`S=\{(x,y):y=3x\}`$. Los elementos de $S$ tienen la forma $(x,3x)$. Se verifican las tres condiciones.

**1. Contiene al vector cero.** $(0,0)$ cumple $y=3x$ porque $0=3\cdot0$. Entonces $\mathbf{0}\in S$.

**2. Cerrado bajo la suma.** Sean $(a,3a)$ y $(b,3b)$ en $S$:

```math
(a,3a)+(b,3b)=(a+b,\ 3a+3b)=(a+b,\ 3(a+b))
```

La segunda componente es el triple de la primera, así que la suma tiene la forma $(x,3x)$ con $x=a+b$. La suma está en $S$.

**3. Cerrado bajo el producto por escalar.** Sea $(a,3a)\in S$ y $k\in\mathbb{R}$:

```math
k(a,3a)=(ka,\ 3ka)=(ka,\ 3(ka))
```

La segunda componente es el triple de la primera, así que el resultado está en $S$.

Se cumplen las tres condiciones, así que **$S$ es subespacio de $`\mathbb{R}^2`$** (es la recta $y=3x$, que pasa por el origen).

**(c)** **Datos:** $\mathbf{a}=(3,1)$ y $\mathbf{b}=(2,2)$.

Se calculan los dos productos punto de la fórmula:

```math
\mathbf{a}\cdot\mathbf{b}=3(2)+1(2)=6+2=8\qquad\mathbf{b}\cdot\mathbf{b}=2(2)+2(2)=4+4=8
```

El coeficiente de la proyección es $\tfrac{8}{8}=1$, entonces:

```math
\mathrm{proj}_{\mathbf{b}}\mathbf{a}=\frac{8}{8}(2,2)=(2,2)
```

El residuo es lo que sobra de $\mathbf{a}$:

```math
\mathbf{r}=\mathbf{a}-\mathrm{proj}_{\mathbf{b}}\mathbf{a}=(3-2,\ 1-2)=(1,\ -1)
```

Comprobación de que el residuo es ortogonal a $\mathbf{b}$:

```math
\mathbf{r}\cdot\mathbf{b}=1(2)+(-1)(2)=2-2=0\ \checkmark
```

Como $\mathbf{r}\cdot\mathbf{b}=0$, entonces $\mathbf{r}\perp\mathbf{b}$. Además $\mathbf{a}=\mathrm{proj}_{\mathbf{b}}\mathbf{a}+\mathbf{r}=(2,2)+(1,-1)=(3,1)$ ✓.

---

## Ejercicio 3 — Matrices: operar, transponer, multiplicar y despejar

```math
A=\begin{bmatrix}1&2\\3&-1\end{bmatrix}\qquad B=\begin{bmatrix}0&-2\\4&1\end{bmatrix}
```

**(a)** Las filas de $A$ pasan a ser columnas: la fila 1 $(1,2)$ es la columna 1 de $`A^T`$ y la fila 2 $(3,-1)$ es la columna 2.

```math
A^T=\begin{bmatrix}1&3\\2&-1\end{bmatrix}
```

Se multiplica cada entrada por el escalar:

```math
2A^T=\begin{bmatrix}2&6\\4&-2\end{bmatrix}\qquad3B=\begin{bmatrix}0&-6\\12&3\end{bmatrix}
```

Se restan entrada por entrada:

```math
2A^T-3B=\begin{bmatrix}2-0&6-(-6)\\4-12&-2-3\end{bmatrix}=\begin{bmatrix}2&12\\-8&-5\end{bmatrix}
```

**(b)** Producto $AB$: la entrada $(i,j)$ es la fila $i$ de $A$ por la columna $j$ de $B$.

```math
AB=\begin{bmatrix}1(0)+2(4)&1(-2)+2(1)\\3(0)+(-1)(4)&3(-2)+(-1)(1)\end{bmatrix}=\begin{bmatrix}0+8&-2+2\\0-4&-6-1\end{bmatrix}=\begin{bmatrix}8&0\\-4&-7\end{bmatrix}
```

Producto $BA$ (ahora las filas son de $B$ y las columnas de $A$):

```math
BA=\begin{bmatrix}0(1)+(-2)(3)&0(2)+(-2)(-1)\\4(1)+1(3)&4(2)+1(-1)\end{bmatrix}=\begin{bmatrix}-6&2\\7&7\end{bmatrix}
```

**¿Son iguales?** No: $AB\neq BA$ (por ejemplo, la entrada $(1,1)$ vale $8$ en uno y $-6$ en el otro). **El producto de matrices no es conmutativo**: el orden importa.

**(c)** Se despeja $X$ de $2X+A=B$ con las mismas reglas que en álgebra. Se resta $A$ en ambos lados:

```math
2X+A=B\ \Rightarrow\ 2X=B-A
```

Se calcula $B-A$ entrada por entrada:

```math
B-A=\begin{bmatrix}0-1&-2-2\\4-3&1-(-1)\end{bmatrix}=\begin{bmatrix}-1&-4\\1&2\end{bmatrix}
```

Se multiplica por $\tfrac12$ (se divide cada entrada entre 2):

```math
X=\tfrac12(B-A)=\begin{bmatrix}-0{,}5&-2\\0{,}5&1\end{bmatrix}
```

Verificación: $2X+A$ debe dar $B$.

```math
2X+A=\begin{bmatrix}-1&-4\\1&2\end{bmatrix}+\begin{bmatrix}1&2\\3&-1\end{bmatrix}=\begin{bmatrix}0&-2\\4&1\end{bmatrix}=B\ \checkmark
```

**(d)** $C$ es de tamaño $3\times2$ y $A$ es de $2\times2$. El producto $(m\times n)(n\times p)$ existe solo si las dimensiones **internas coinciden**.

- **$CA$ sí se puede:** $(3\times2)(2\times2)$. Las internas son $2$ y $2$, coinciden. El resultado es de tamaño **$3\times2$** (las dimensiones externas).
- **$AC$ no se puede:** $(2\times2)(3\times2)$. Las internas son $2$ y $3$, y $2\neq3$ ($A$ tiene 2 columnas y $C$ tiene 3 filas, no se pueden emparejar fila con columna).

---

# Parte B — Ejercicio para la casa

## Ejercicio B — Buscador por similitud: de vectores a matrices

Una consulta y tres documentos son vectores de 3 características (tres temas):

```math
\mathbf{q}=(2,1,2)\qquad\mathbf{d}_1=(1,2,2)\qquad\mathbf{d}_2=(2,-2,1)\qquad\mathbf{d}_3=(1,0,-1)
```

**(a)** Se pide, para cada documento: norma, producto punto con $\mathbf{q}$, coseno y distancia. Para $\mathbf{q}$: $`\lVert\mathbf{q}\rVert=\sqrt{4+1+4}=3`$.

**Normas:**

```math
\lVert\mathbf{d}_1\rVert=\sqrt{1+4+4}=3\qquad\lVert\mathbf{d}_2\rVert=\sqrt{4+4+1}=3\qquad\lVert\mathbf{d}_3\rVert=\sqrt{1+0+1}=\sqrt2\approx1{,}414
```

**Productos punto con $\mathbf{q}$:**

```math
\mathbf{q}\cdot\mathbf{d}_1=2(1)+1(2)+2(2)=2+2+4=8
```

```math
\mathbf{q}\cdot\mathbf{d}_2=2(2)+1(-2)+2(1)=4-2+2=4
```

```math
\mathbf{q}\cdot\mathbf{d}_3=2(1)+1(0)+2(-1)=2+0-2=0
```

**Cosenos**, con $\cos(\mathbf{q},\mathbf{d})=\dfrac{\mathbf{q}\cdot\mathbf{d}}{3\lVert\mathbf{d}\rVert}$:

```math
\cos(\mathbf{q},\mathbf{d}_1)=\frac{8}{3\cdot3}=\frac89\approx0{,}889\qquad\cos(\mathbf{q},\mathbf{d}_2)=\frac{4}{3\cdot3}=\frac49\approx0{,}444\qquad\cos(\mathbf{q},\mathbf{d}_3)=\frac{0}{3\sqrt2}=0
```

**Distancias.** Se resta $\mathbf{q}-\mathbf{d}$ y se calcula la norma:

```math
\mathbf{q}-\mathbf{d}_1=(1,-1,0)\ \Rightarrow\ d=\sqrt{1+1+0}=\sqrt2\approx1{,}414
```

```math
\mathbf{q}-\mathbf{d}_2=(0,3,1)\ \Rightarrow\ d=\sqrt{0+9+1}=\sqrt{10}\approx3{,}162
```

```math
\mathbf{q}-\mathbf{d}_3=(1,1,3)\ \Rightarrow\ d=\sqrt{1+1+9}=\sqrt{11}\approx3{,}317
```

**Tabla completa:**

| Documento | $\lVert\mathbf{d}\rVert$ | $\mathbf{q}\cdot\mathbf{d}$ | $\cos(\mathbf{q},\mathbf{d})$ | $d(\mathbf{q},\mathbf{d})$ |
|---|---|---|---|---|
| $`\mathbf{d}_1`$ | $3$ | $8$ | $8/9\approx0{,}889$ | $\sqrt2\approx1{,}414$ |
| $`\mathbf{d}_2`$ | $3$ | $4$ | $4/9\approx0{,}444$ | $\sqrt{10}\approx3{,}162$ |
| $`\mathbf{d}_3`$ | $\sqrt2\approx1{,}414$ | $0$ | $0$ | $\sqrt{11}\approx3{,}317$ |

**(b)** Orden del más al menos similar según el coseno (mayor coseno = más parecido):

```math
\mathbf{d}_1\ (0{,}889)\ >\ \mathbf{d}_2\ (0{,}444)\ >\ \mathbf{d}_3\ (0)
```

**Documento ortogonal a $\mathbf{q}$:** $`\mathbf{d}_3`$, porque $`\mathbf{q}\cdot\mathbf{d}_3=0`$. No comparte ningún tema con la consulta.

**Recomendación:** $`\mathbf{d}_1`$. Tiene el mayor coseno, la menor distancia ($\sqrt2$) y el mayor producto punto ($8$): los tres criterios coinciden en que es el más parecido a la consulta.

**(c)** Las filas de $D$ son los documentos:

```math
D=\begin{bmatrix}1&2&2\\2&-2&1\\1&0&-1\end{bmatrix}
```

Producto matriz por vector: cada entrada de $D\mathbf{q}$ es el producto punto de una fila de $D$ con $\mathbf{q}$.

```math
D\mathbf{q}=\begin{bmatrix}1(2)+2(1)+2(2)\\2(2)+(-2)(1)+1(2)\\1(2)+0(1)+(-1)(2)\end{bmatrix}=\begin{bmatrix}2+2+4\\4-2+2\\2+0-2\end{bmatrix}=\begin{bmatrix}8\\4\\0\end{bmatrix}
```

**Qué representa cada entrada:** el producto punto de un documento con la consulta, es decir $`\mathbf{q}\cdot\mathbf{d}_1=8`$, $`\mathbf{q}\cdot\mathbf{d}_2=4`$ y $`\mathbf{q}\cdot\mathbf{d}_3=0`$, los mismos valores de la columna del producto punto de la tabla. Un solo producto $D\mathbf{q}$ calcula los tres a la vez.

**(d)**

```math
W=\begin{bmatrix}1&0&1\\0&1&-1\end{bmatrix}
```

$W$ tiene 2 filas y 3 columnas: tamaño **$2\times3$**. Resume los 3 temas en 2 (cada fila es una combinación de los temas).

$\mathbf{q}$ es de $3\times1$, así que $W\mathbf{q}$ es $(2\times3)(3\times1)=2\times1$:

```math
W\mathbf{q}=\begin{bmatrix}1(2)+0(1)+1(2)\\0(2)+1(1)+(-1)(2)\end{bmatrix}=\begin{bmatrix}2+0+2\\0+1-2\end{bmatrix}=\begin{bmatrix}4\\-1\end{bmatrix}
```

```math
W\mathbf{d}_1=\begin{bmatrix}1(1)+0(2)+1(2)\\0(1)+1(2)+(-1)(2)\end{bmatrix}=\begin{bmatrix}1+0+2\\0+2-2\end{bmatrix}=\begin{bmatrix}3\\0\end{bmatrix}
```

**(e)** Las filas de $W$ pasan a ser columnas: la fila 1 $(1,0,1)$ es la columna 1 de $`W^T`$ y la fila 2 $(0,1,-1)$ es la columna 2.

```math
W^T=\begin{bmatrix}1&0\\0&1\\1&-1\end{bmatrix}
```

$`W^T`$ es de $3\times2$. El producto $`WW^T`$ es $(2\times3)(3\times2)$: las dimensiones internas ($3$ y $3$) coinciden y el resultado es de **$2\times2$**.

```math
WW^T=\begin{bmatrix}1(1)+0(0)+1(1)&1(0)+0(1)+1(-1)\\0(1)+1(0)+(-1)(1)&0(0)+1(1)+(-1)(-1)\end{bmatrix}=\begin{bmatrix}2&-1\\-1&2\end{bmatrix}
```

Cada entrada de $`WW^T`$ es el producto punto entre dos filas de $W$. Por eso la matriz es simétrica: $`(WW^T)_{12}=(WW^T)_{21}=-1`$ ✓.

**(f)** Se plantea $\mathbf{q}=a\,\mathbf{d}_1+b\,\mathbf{d}_3$ y se iguala componente a componente:

```math
a(1,2,2)+b(1,0,-1)=(a+b,\ 2a,\ 2a-b)=(2,1,2)
```

```math
\begin{cases}a+b=2 & (1)\\ 2a=1 & (2)\\ 2a-b=2 & (3)\end{cases}
```

De (2): $a=\tfrac12$. De (1): $b=2-\tfrac12=\tfrac32$. Se prueban esos valores en la ecuación (3), que todavía no se usó:

```math
2a-b=2\left(\tfrac12\right)-\tfrac32=1-\tfrac32=-\tfrac12\neq2
```

Los valores que cumplen (1) y (2) **no** cumplen (3): el sistema es **inconsistente**. Por lo tanto, **$\mathbf{q}$ no es combinación lineal de $`\mathbf{d}_1`$ y $`\mathbf{d}_3`$**, es decir, $\mathbf{q}$ no está en el generado de $`\{\mathbf{d}_1,\mathbf{d}_3\}`$.
