# Examen — Vectores, producto punto, combinaciones lineales, espacios vectoriales y matrices

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

**Datos:** $\mathbf{u}=(1,-4,8)$.

**(a)** Se eleva al cuadrado cada componente, se suman y se saca la raíz:

```math
1^2=1\qquad(-4)^2=16\qquad8^2=64
```

```math
\lVert\mathbf{u}\rVert=\sqrt{1+16+64}=\sqrt{81}=9
```

Para el vector unitario se divide **cada componente** entre la norma:

```math
\hat{\mathbf{u}}=\frac{\mathbf{u}}{9}=\left(\tfrac{1}{9},\ \tfrac{-4}{9},\ \tfrac{8}{9}\right)=\left(\tfrac{1}{9},\ -\tfrac{4}{9},\ \tfrac{8}{9}\right)
```

Verificación (la norma de $\hat{\mathbf{u}}$ debe ser 1):

```math
\lVert\hat{\mathbf{u}}\rVert=\sqrt{\left(\tfrac{1}{9}\right)^2+\left(-\tfrac{4}{9}\right)^2+\left(\tfrac{8}{9}\right)^2}=\sqrt{\tfrac{1}{81}+\tfrac{16}{81}+\tfrac{64}{81}}=\sqrt{\tfrac{81}{81}}=\sqrt{1}=1\ \checkmark
```

**(b)** Se multiplica cada componente de $\mathbf{u}$ por $-2$:

```math
-2\mathbf{u}=\big(-2\cdot1,\ -2\cdot(-4),\ -2\cdot8\big)=(-2,\ 8,\ -16)
```

Norma directa:

```math
(-2)^2=4\qquad8^2=64\qquad(-16)^2=256
```

```math
\lVert-2\mathbf{u}\rVert=\sqrt{4+64+256}=\sqrt{324}=18
```

Con la propiedad, usando $\lVert\mathbf{u}\rVert=9$ del inciso (a):

```math
\lvert-2\rvert\cdot\lVert\mathbf{u}\rVert=2\cdot9=18
```

Ambos resultados son $18$ ✓.

**(c)** Se escribe la norma con $k$ y se iguala a 13:

```math
\lVert(k,3,4)\rVert=\sqrt{k^2+3^2+4^2}=\sqrt{k^2+9+16}=\sqrt{k^2+25}=13
```

Se elevan al cuadrado ambos lados para quitar la raíz:

```math
k^2+25=13^2=169
```

Se resta 25 en ambos lados:

```math
k^2=169-25=144
```

Hay dos números cuyo cuadrado es 144, el positivo y el negativo (porque $(-12)(-12)=144$):

```math
k=12\quad\text{o}\quad k=-12
```

Verificación de ambos valores:

```math
k=12:\ \sqrt{12^2+9+16}=\sqrt{144+25}=\sqrt{169}=13\ \checkmark
```

```math
k=-12:\ \sqrt{(-12)^2+9+16}=\sqrt{144+25}=\sqrt{169}=13\ \checkmark
```

---

## Ejercicio 2 — Distancia

**Datos:** $A=(3,-2,1,5)$, $B=(1,0,0,5)$, $C=(2,-1,3,3)$.

**(a)** La distancia es la norma de la resta. Primero $d(A,B)$, restando componente a componente:

```math
A-B=(3-1,\ -2-0,\ 1-0,\ 5-5)=(2,\ -2,\ 1,\ 0)
```

```math
2^2=4\qquad(-2)^2=4\qquad1^2=1\qquad0^2=0
```

```math
d(A,B)=\sqrt{4+4+1+0}=\sqrt{9}=3
```

Ahora $d(A,C)$:

```math
A-C=(3-2,\ -2-(-1),\ 1-3,\ 5-3)=(1,\ -1,\ -2,\ 2)
```

```math
1^2=1\qquad(-1)^2=1\qquad(-2)^2=4\qquad2^2=4
```

```math
d(A,C)=\sqrt{1+1+4+4}=\sqrt{10}\approx3{,}162
```

**(b)** Se comparan las dos distancias: $3$ y $\sqrt{10}\approx3{,}162$. Equivalentemente, $3=\sqrt9<\sqrt{10}$. Como $d(A,B)<d(A,C)$, **$B$ está más cerca de $A$** que $C$.

---

## Ejercicio 3 — Producto punto y propiedades

**Datos:** $\mathbf{a}=(2,-1,4)$, $\mathbf{b}=(-3,5,1)$, $\mathbf{c}=(1,2,-2)$.

**(a)** Productos parciales (componente 1 con 1, 2 con 2, 3 con 3) y luego suma:

```math
\mathbf{a}\cdot\mathbf{b}=2(-3)+(-1)(5)+4(1)=-6-5+4=-7
```

```math
\mathbf{a}\cdot\mathbf{c}=2(1)+(-1)(2)+4(-2)=2-2-8=-8
```

```math
\mathbf{b}\cdot\mathbf{c}=(-3)(1)+5(2)+1(-2)=-3+10-2=5
```

**(b)** Propiedad distributiva $(\mathbf{a}+\mathbf{b})\cdot\mathbf{c}=\mathbf{a}\cdot\mathbf{c}+\mathbf{b}\cdot\mathbf{c}$.

Lado izquierdo. Primero la suma, componente a componente:

```math
\mathbf{a}+\mathbf{b}=(2+(-3),\ -1+5,\ 4+1)=(-1,\ 4,\ 5)
```

Luego el producto punto con $\mathbf{c}$:

```math
(\mathbf{a}+\mathbf{b})\cdot\mathbf{c}=(-1)(1)+4(2)+5(-2)=-1+8-10=-3
```

Lado derecho. Se usan los productos del inciso (a) y se suman:

```math
\mathbf{a}\cdot\mathbf{c}+\mathbf{b}\cdot\mathbf{c}=-8+5=-3
```

Ambos lados dan $-3$ ✓.

**(c)** Primera igualdad: $(-3\mathbf{a})\cdot\mathbf{b}=-3(\mathbf{a}\cdot\mathbf{b})$.

Lado izquierdo. Primero se escala $\mathbf{a}$:

```math
-3\mathbf{a}=\big(-3\cdot2,\ -3\cdot(-1),\ -3\cdot4\big)=(-6,\ 3,\ -12)
```

```math
(-3\mathbf{a})\cdot\mathbf{b}=(-6)(-3)+3(5)+(-12)(1)=18+15-12=21
```

Lado derecho. Se usa $\mathbf{a}\cdot\mathbf{b}=-7$ del inciso (a):

```math
-3(\mathbf{a}\cdot\mathbf{b})=-3(-7)=21
```

Ambos lados dan $21$ ✓.

Segunda igualdad: $\mathbf{a}\cdot\mathbf{a}=\lVert\mathbf{a}\rVert^2$.

```math
\mathbf{a}\cdot\mathbf{a}=2(2)+(-1)(-1)+4(4)=4+1+16=21
```

```math
\lVert\mathbf{a}\rVert=\sqrt{2^2+(-1)^2+4^2}=\sqrt{4+1+16}=\sqrt{21}\ \Rightarrow\ \lVert\mathbf{a}\rVert^2=\left(\sqrt{21}\right)^2=21
```

Ambos dan $21$ ✓.

---

## Ejercicio 4 — Ángulo entre vectores

**(a)** $\mathbf{u}=(1,2)$, $\mathbf{v}=(3,1)$.

Producto punto y normas:

```math
\mathbf{u}\cdot\mathbf{v}=1(3)+2(1)=3+2=5
```

```math
\lVert\mathbf{u}\rVert=\sqrt{1^2+2^2}=\sqrt{1+4}=\sqrt5\qquad\lVert\mathbf{v}\rVert=\sqrt{3^2+1^2}=\sqrt{9+1}=\sqrt{10}
```

Se sustituye en la fórmula del coseno. Se usa $\sqrt5\cdot\sqrt{10}=\sqrt{50}$ y $\sqrt{50}=\sqrt{25\cdot2}=5\sqrt2$, y luego se racionaliza multiplicando arriba y abajo por $\sqrt2$:

```math
\cos\theta=\frac{5}{\sqrt5\cdot\sqrt{10}}=\frac{5}{\sqrt{50}}=\frac{5}{5\sqrt2}=\frac{1}{\sqrt2}=\frac{1\cdot\sqrt2}{\sqrt2\cdot\sqrt2}=\frac{\sqrt2}{2}\approx0{,}707
```

El ángulo cuyo coseno es $\frac{\sqrt2}{2}$ es un valor conocido:

```math
\theta=\arccos\left(\tfrac{\sqrt2}{2}\right)=45^\circ
```

**(b)** $\mathbf{u}=(2,-1,3)$, $\mathbf{v}=(-1,4,1)$.

Predicción por el signo del producto punto:

```math
\mathbf{u}\cdot\mathbf{v}=2(-1)+(-1)(4)+3(1)=-2-4+3=-3
```

Como $-3<0$, el ángulo es **obtuso** (mayor que $90^\circ$). Si fuera positivo sería agudo, y si fuera cero, recto.

Confirmación. Normas:

```math
\lVert\mathbf{u}\rVert=\sqrt{2^2+(-1)^2+3^2}=\sqrt{4+1+9}=\sqrt{14}
```

```math
\lVert\mathbf{v}\rVert=\sqrt{(-1)^2+4^2+1^2}=\sqrt{1+16+1}=\sqrt{18}=\sqrt{9\cdot2}=3\sqrt2
```

Coseno. Se usa $\sqrt{14}\cdot\sqrt2=\sqrt{28}=\sqrt{4\cdot7}=2\sqrt7$, y luego se racionaliza multiplicando arriba y abajo por $\sqrt7$:

```math
\cos\theta=\frac{-3}{\sqrt{14}\cdot3\sqrt2}=\frac{-3}{3\sqrt{28}}=\frac{-1}{2\sqrt7}=\frac{-1\cdot\sqrt7}{2\sqrt7\cdot\sqrt7}=-\frac{\sqrt7}{14}\approx-\frac{2{,}646}{14}\approx-0{,}189
```

Ángulo, con la calculadora en grados:

```math
\theta=\arccos(-0{,}189)\approx100{,}9^\circ
```

Como $100{,}9^\circ>90^\circ$, el ángulo es obtuso, tal como predijo el signo del producto punto ✓.

---

## Ejercicio 5 — Ortogonalidad

**(a)** Un solo cálculo: el producto punto.

```math
(4,-2,1)\cdot(1,3,2)=4(1)+(-2)(3)+1(2)=4-6+2=0
```

Como el producto punto es cero, **sí son ortogonales**.

**(b)** Se calcula el producto punto en términos de $k$ y se iguala a cero:

```math
(2,k,-1)\cdot(k,4,6)=2(k)+k(4)+(-1)(6)=2k+4k-6=6k-6
```

```math
6k-6=0\ \Rightarrow\ 6k=6\ \Rightarrow\ k=1
```

Verificación, sustituyendo $k=1$ en ambos vectores:

```math
(2,1,-1)\cdot(1,4,6)=2(1)+1(4)+(-1)(6)=2+4-6=0\ \checkmark
```

**(c)** Se buscan $(x,y)$ con $(x,y)\cdot(5,-2)=0$, es decir $5x-2y=0$. Hay dos incógnitas y una sola ecuación, así que se elige el valor de una y se despeja la otra. Con $x=2$:

```math
5(2)-2y=0\ \Rightarrow\ 10-2y=0\ \Rightarrow\ 10=2y\ \Rightarrow\ y=5
```

El vector es $(2,5)$. Verificación:

```math
(2,5)\cdot(5,-2)=2(5)+5(-2)=10-10=0\ \checkmark
```

Pero $(2,5)$ no tiene norma 1:

```math
\lVert(2,5)\rVert=\sqrt{2^2+5^2}=\sqrt{4+25}=\sqrt{29}
```

Para tener norma 1 se divide cada componente entre $\sqrt{29}$:

```math
\mathbf{w}=\left(\frac{2}{\sqrt{29}},\ \frac{5}{\sqrt{29}}\right)\approx(0{,}371;\ 0{,}928)
```

Comprobación de las dos condiciones.

Ortogonal a $(5,-2)$:

```math
\mathbf{w}\cdot(5,-2)=\frac{2}{\sqrt{29}}(5)+\frac{5}{\sqrt{29}}(-2)=\frac{10}{\sqrt{29}}-\frac{10}{\sqrt{29}}=0\ \checkmark
```

Norma 1:

```math
\lVert\mathbf{w}\rVert=\sqrt{\left(\tfrac{2}{\sqrt{29}}\right)^2+\left(\tfrac{5}{\sqrt{29}}\right)^2}=\sqrt{\tfrac{4}{29}+\tfrac{25}{29}}=\sqrt{\tfrac{29}{29}}=1\ \checkmark
```

(También sirve el opuesto, $-\mathbf{w}$.)

---

## Ejercicio 6 — Combinación lineal

**Datos:** $\mathbf{w}=(3,8)$, $`\mathbf{v}_1=(3,1)`$, $`\mathbf{v}_2=(1,-2)`$.

**(a)** Se plantea la combinación lineal y se multiplican los escalares por cada vector:

```math
c_1(3,1)+c_2(1,-2)=(3c_1+c_2,\ \ c_1-2c_2)=(3,8)
```

Igualando componente a componente (primera componente con primera, segunda con segunda):

```math
\begin{cases}3c_1+c_2=3 & (1)\\ c_1-2c_2=8 & (2)\end{cases}
```

**(b)** Sumar las ecuaciones directamente no cancela ninguna incógnita ($`3c_1+c_1`$ y $`c_2-2c_2`$ no se anulan). Se multiplica **toda** la ecuación (1) por 2 para que $`c_2`$ y $`-2c_2`$ queden opuestos:

```math
2\cdot(3c_1+c_2)=2\cdot3\ \Rightarrow\ 6c_1+2c_2=6\qquad(1')
```

Se suman (1') y (2), lado izquierdo con lado izquierdo y lado derecho con lado derecho:

```math
(6c_1+c_1)+(2c_2-2c_2)=6+8\ \Rightarrow\ 7c_1+0=14
```

```math
c_1=\frac{14}{7}=2
```

Se sustituye $`c_1=2`$ en la ecuación (1) y se despeja $`c_2`$:

```math
3(2)+c_2=3\ \Rightarrow\ 6+c_2=3\ \Rightarrow\ c_2=3-6=-3
```

**(c)** Verificación en el vector original:

```math
2(3,1)+(-3)(1,-2)=(6,2)+(-3,6)=(6-3,\ 2+6)=(3,8)=\mathbf{w}\ \checkmark
```

También cumple las dos ecuaciones: (1) $3(2)+(-3)=3$ ✓ y (2) $2-2(-3)=2+6=8$ ✓.

Resultado: $`\mathbf{w}=2\mathbf{v}_1-3\mathbf{v}_2`$.

---

## Ejercicio 7 — Generado

**(a)** $(-4,2,-6)$ está en el generado de $\{(2,-1,3)\}$ si existe un escalar $c$ tal que $c(2,-1,3)=(-4,2,-6)$. Se iguala componente a componente:

```math
2c=-4\ \Rightarrow\ c=-2\qquad-c=2\ \Rightarrow\ c=-2\qquad3c=-6\ \Rightarrow\ c=-2
```

El mismo $c=-2$ funciona en las tres posiciones, así que **sí está** en el generado:

```math
-2(2,-1,3)=(-4,2,-6)\ \checkmark
```

**(b)** Se plantea $`c_1(1,0,2)+c_2(0,1,1)=(x,y,z)`$. Al multiplicar y sumar:

```math
c_1(1,0,2)+c_2(0,1,1)=(c_1,\ \ c_2,\ \ 2c_1+c_2)
```

Igualando con $(x,y,z)$ queda el sistema:

```math
c_1=x,\qquad c_2=y,\qquad2c_1+c_2=z
```

Hay tres ecuaciones y solo dos incógnitas: las dos primeras dan $`c_1`$ y $`c_2`$, y la tercera comprueba si esos valores también funcionan en la última posición. Es la misma idea del generado de un solo vector, donde el mismo $c$ debe servir en todas las posiciones.

- **Para $(3,1,5)$:** $`c_1=3`$ y $`c_2=1`$. Se prueba la tercera: $2(3)+1=7$, pero el vector pide $5$, y $7\neq5$. El sistema es inconsistente, así que **no es combinación lineal**.
- **Para $(2,3,7)$:** $`c_1=2`$ y $`c_2=3`$. Se prueba la tercera: $2(2)+3=4+3=7$ ✓. **Sí es combinación lineal**:

```math
2(1,0,2)+3(0,1,1)=(2,0,4)+(0,3,3)=(2,3,7)\ \checkmark
```

---

## Ejercicio 8 — Subespacios

**(a)** $S=\{(x,y,z):z=x+y\}$. Un vector está en $S$ cuando su tercera componente es igual a la suma de las dos primeras. Se verifican las tres condiciones.

**1. Contiene al vector cero.** El vector $(0,0,0)$ cumple $z=x+y$, porque $0=0+0$. Entonces $\mathbf{0}\in S$.

**2. Cerrado bajo la suma.** Sean $`(x_1,y_1,z_1)`$ y $`(x_2,y_2,z_2)`$ en $S$, es decir $`z_1=x_1+y_1`$ y $`z_2=x_2+y_2`$. Su suma es

```math
(x_1+x_2,\ \ y_1+y_2,\ \ z_1+z_2)
```

Se verifica la condición de $S$ en la suma: la tercera componente es

```math
z_1+z_2=(x_1+y_1)+(x_2+y_2)=(x_1+x_2)+(y_1+y_2)
```

que es la suma de las dos primeras componentes de la suma. Por lo tanto, la suma está en $S$.

**3. Cerrado bajo el producto por escalar.** Sea $(x,y,z)\in S$ con $z=x+y$, y $k\in\mathbb{R}$:

```math
k(x,y,z)=(kx,\ ky,\ kz)
```

La tercera componente cumple $kz=k(x+y)=kx+ky$, que es la suma de las dos primeras. Por lo tanto, el resultado está en $S$.

Se cumplen las tres condiciones, así que **$S$ es subespacio de $\mathbb{R}^3$**.

**(b)** $T=\{(x,y):x\cdot y=0\}$. Para mostrar que no es subespacio basta un contraejemplo de una condición. Se prueba la suma:

- $(1,0)\in T$, porque $1\cdot0=0$.
- $(0,1)\in T$, porque $0\cdot1=0$.
- Su suma es $(1,0)+(0,1)=(1,1)$, y $1\cdot1=1\neq0$, así que $(1,1)\notin T$.

$T$ no es cerrado bajo la suma, por lo tanto **$T$ no es subespacio de $\mathbb{R}^2$**.

---

## Ejercicio 9 — Axiomas de espacio vectorial

**Datos:** $\mathbf{u}=(2,-1)$, $\mathbf{v}=(0,3)$, $\mathbf{w}=(-4,5)$, $k=3$, $m=-2$.

**(a)** Asociatividad: $(\mathbf{u}+\mathbf{v})+\mathbf{w}=\mathbf{u}+(\mathbf{v}+\mathbf{w})$.

Lado izquierdo (se suma primero $\mathbf{u}+\mathbf{v}$):

```math
\mathbf{u}+\mathbf{v}=(2+0,\ -1+3)=(2,\ 2)
```

```math
(\mathbf{u}+\mathbf{v})+\mathbf{w}=(2+(-4),\ 2+5)=(-2,\ 7)
```

Lado derecho (se suma primero $\mathbf{v}+\mathbf{w}$):

```math
\mathbf{v}+\mathbf{w}=(0+(-4),\ 3+5)=(-4,\ 8)
```

```math
\mathbf{u}+(\mathbf{v}+\mathbf{w})=(2+(-4),\ -1+8)=(-2,\ 7)
```

Ambos dan $(-2,7)$ ✓.

**(b)** Distributividad: $(k+m)\mathbf{u}=k\mathbf{u}+m\mathbf{u}$.

Lado izquierdo. Primero la suma de escalares:

```math
k+m=3+(-2)=1\ \Rightarrow\ (k+m)\mathbf{u}=1\cdot(2,-1)=(2,\ -1)
```

Lado derecho. Cada término por separado y luego la suma:

```math
k\mathbf{u}=3(2,-1)=(6,\ -3)\qquad m\mathbf{u}=-2(2,-1)=(-4,\ 2)
```

```math
k\mathbf{u}+m\mathbf{u}=(6+(-4),\ -3+2)=(2,\ -1)
```

Ambos dan $(2,-1)$ ✓.

**(c)** $P=\{(x,y):x>0\ \text{y}\ y>0\}$ **no es un espacio vectorial** porque **no es cerrado bajo el producto por escalar**. Ejemplo: $(1,2)\in P$ (ambas componentes positivas), pero al multiplicar por $-1$:

```math
(-1)(1,2)=(-1,\ -2)\notin P
```

porque sus componentes son negativas. Como consecuencia:

- Los elementos de $P$ **no tienen opuesto aditivo** dentro de $P$: el opuesto de $(1,2)$ es $(-1,-2)$, que no está en $P$.
- El vector cero $(0,0)$ tampoco está en $P$, porque $0>0$ es falso.

---

## Ejercicio 10 — Leer matrices

```math
A=\begin{bmatrix}3&0&-2\\1&5&4\\-1&2&0\\6&-3&7\end{bmatrix}
```

**(a)** $A$ tiene 4 filas y 3 columnas: tamaño **$4\times3$**. La entrada $`a_{ij}`$ está en la fila $i$, columna $j$:

- $`a_{31}`$ (fila 3, columna 1): $-1$.
- $`a_{23}`$ (fila 2, columna 3): $4$.
- $`a_{43}`$ (fila 4, columna 3): $7$.

**(b)**

- Fila 3: se leen las entradas de izquierda a derecha, $(-1,\ 2,\ 0)$.
- Columna 2: se leen las entradas de arriba hacia abajo, $(0,\ 5,\ 2,\ -3)$.

**(c)** Cada entrada es $`c_{ij}=i-j`$ (fila menos columna):

```math
C=\begin{bmatrix}1-1&1-2&1-3\\2-1&2-2&2-3\\3-1&3-2&3-3\end{bmatrix}=\begin{bmatrix}0&-1&-2\\1&0&-1\\2&1&0\end{bmatrix}
```

La transpuesta tiene como filas las columnas de $C$:

```math
C^T=\begin{bmatrix}0&1&2\\-1&0&1\\-2&-1&0\end{bmatrix}
```

Comparando entrada por entrada, cada entrada de $C^T$ es la opuesta de la de $C$ (por ejemplo $`c_{12}=-1`$ y $`(C^T)_{12}=1`$). Entonces

```math
C^T=-C
```

En general $`c_{ji}=j-i=-(i-j)=-c_{ij}`$, por eso al transponer cada entrada cambia de signo. La diagonal no cambia porque vale cero: $`c_{ii}=i-i=0`$.

---

## Ejercicio 11 — Transponer matrices

```math
B=\begin{bmatrix}2&-1&0&3\\4&5&-6&1\end{bmatrix}
```

**(a)** $B$ es $2\times4$, así que $B^T$ es $4\times2$. Las filas de $B$ pasan a ser columnas: la fila 1 $(2,-1,0,3)$ es la columna 1 de $B^T$ y la fila 2 $(4,5,-6,1)$ es la columna 2.

```math
B^T=\begin{bmatrix}2&4\\-1&5\\0&-6\\3&1\end{bmatrix}
```

$`(B^T)_{32}`$ es la fila 3, columna 2 de $B^T$, que vale $-6$. Por la definición $`(B^T)_{ij}=b_{ji}`$, coincide con $`b_{23}=-6`$ (fila 2, columna 3 de $B$) ✓.

**(b)** Se transpone $B^T$ (de $4\times2$ a $2\times4$): la columna 1 de $B^T$, $(2,-1,0,3)$, vuelve a ser la fila 1, y la columna 2, $(4,5,-6,1)$, vuelve a ser la fila 2.

```math
(B^T)^T=\begin{bmatrix}2&-1&0&3\\4&5&-6&1\end{bmatrix}=B\ \checkmark
```

**(c)** Una matriz es simétrica si es igual a su transpuesta, es decir, si $`m_{ij}=m_{ji}`$ (lo que hay arriba de la diagonal se refleja abajo).

$`D=\begin{bmatrix}1&2&-3\\2&0&5\\-3&5&4\end{bmatrix}`$. Se comparan las entradas simétricas:

- $`d_{12}=2`$ y $`d_{21}=2`$ ✓
- $`d_{13}=-3`$ y $`d_{31}=-3`$ ✓
- $`d_{23}=5`$ y $`d_{32}=5`$ ✓

**$D$ sí es simétrica.**

$`E=\begin{bmatrix}1&2\\3&1\end{bmatrix}`$: $`e_{12}=2`$ pero $`e_{21}=3`$, y $2\neq3$. **$E$ no es simétrica.**

Para $`\begin{bmatrix}1&x\\7&2\end{bmatrix}`$, la entrada (1,2) vale $x$ y la (2,1) vale $7$. Para que sea simétrica deben ser iguales: **$x=7$**.

---

## Ejercicio 12 — Sumar y escalar matrices

```math
A=\begin{bmatrix}2&-1&3\\0&4&-2\end{bmatrix}\qquad B=\begin{bmatrix}2&5&-3\\2&-2&4\end{bmatrix}
```

**(a)** Se suman las entradas que ocupan la misma posición:

```math
A+B=\begin{bmatrix}2+2&-1+5&3+(-3)\\0+2&4+(-2)&-2+4\end{bmatrix}=\begin{bmatrix}4&4&0\\2&2&2\end{bmatrix}
```

**(b)** Primero se multiplica cada entrada por el escalar:

```math
2A=\begin{bmatrix}2\cdot2&2(-1)&2\cdot3\\2\cdot0&2\cdot4&2(-2)\end{bmatrix}=\begin{bmatrix}4&-2&6\\0&8&-4\end{bmatrix}
```

```math
3B=\begin{bmatrix}3\cdot2&3\cdot5&3(-3)\\3\cdot2&3(-2)&3\cdot4\end{bmatrix}=\begin{bmatrix}6&15&-9\\6&-6&12\end{bmatrix}
```

Luego se restan entrada por entrada:

```math
2A-3B=\begin{bmatrix}4-6&-2-15&6-(-9)\\0-6&8-(-6)&-4-12\end{bmatrix}=\begin{bmatrix}-2&-17&15\\-6&14&-16\end{bmatrix}
```

**(c)** Se despeja $X$ igual que con vectores. Primero se suma el opuesto de $A$ a ambos lados:

```math
A+2X=B\ \Rightarrow\ A+2X-A=B-A\ \Rightarrow\ 2X=B-A
```

Luego se multiplica ambos lados por $\tfrac12$. Como no existe la división entre matrices, el escalar $2$ se quita multiplicando por su inverso, $\tfrac12$.

```math
X=\tfrac12(B-A)
```

Primero $B-A$, entrada por entrada:

```math
B-A=\begin{bmatrix}2-2&5-(-1)&-3-3\\2-0&-2-4&4-(-2)\end{bmatrix}=\begin{bmatrix}0&6&-6\\2&-6&6\end{bmatrix}
```

Luego se multiplica por $\tfrac12$ (se divide cada entrada entre 2):

```math
X=\tfrac12\begin{bmatrix}0&6&-6\\2&-6&6\end{bmatrix}=\begin{bmatrix}0&3&-3\\1&-3&3\end{bmatrix}
```

Verificación: se calcula $2X$ y se suma a $A$.

```math
2X=\begin{bmatrix}0&6&-6\\2&-6&6\end{bmatrix}
```

```math
A+2X=\begin{bmatrix}2+0&-1+6&3+(-6)\\0+2&4+(-6)&-2+6\end{bmatrix}=\begin{bmatrix}2&5&-3\\2&-2&4\end{bmatrix}=B\ \checkmark
```

**(d)** Se calcula cada lado por separado.

Lado izquierdo. Se transpone el resultado del inciso (b) (las filas pasan a ser columnas):

```math
(2A-3B)^T=\begin{bmatrix}-2&-6\\-17&14\\15&-16\end{bmatrix}
```

Lado derecho. Primero las transpuestas de $A$ y $B$:

```math
A^T=\begin{bmatrix}2&0\\-1&4\\3&-2\end{bmatrix}\qquad B^T=\begin{bmatrix}2&2\\5&-2\\-3&4\end{bmatrix}
```

Luego se escalan:

```math
2A^T=\begin{bmatrix}4&0\\-2&8\\6&-4\end{bmatrix}\qquad3B^T=\begin{bmatrix}6&6\\15&-6\\-9&12\end{bmatrix}
```

Y se restan entrada por entrada:

```math
2A^T-3B^T=\begin{bmatrix}4-6&0-6\\-2-15&8-(-6)\\6-(-9)&-4-12\end{bmatrix}=\begin{bmatrix}-2&-6\\-17&14\\15&-16\end{bmatrix}
```

Ambos lados coinciden ✓.

---

# Parte B — Problemas de datos e inteligencia artificial

## Ejercicio 13 — Imágenes en escala de grises como matrices

```math
I_1=\begin{bmatrix}120&80&40\\60&200&100\\20&140&180\end{bmatrix}\qquad I_2=\begin{bmatrix}80&120&160\\140&40&100\\180&60&20\end{bmatrix}
```

**(a)** $I_1$ tiene 3 filas y 3 columnas: tamaño **$3\times3$** (9 píxeles). La entrada $`i_{23}`$ está en la fila 2, columna 3, y vale $100$. Significa que el píxel de la **fila 2, columna 3** tiene brillo $100$: un gris medio-oscuro (0 es negro y 255 es blanco).

**(b)** Se multiplica cada entrada por $0{,}75$:

```math
\tfrac34I_1=\begin{bmatrix}0{,}75\cdot120&0{,}75\cdot80&0{,}75\cdot40\\0{,}75\cdot60&0{,}75\cdot200&0{,}75\cdot100\\0{,}75\cdot20&0{,}75\cdot140&0{,}75\cdot180\end{bmatrix}=\begin{bmatrix}90&60&30\\45&150&75\\15&105&135\end{bmatrix}
```

Efecto: **oscurece la imagen**, porque todos los brillos bajan al 75 % de su valor. Las proporciones entre píxeles se conservan y solo cambia la intensidad global.

**(c)** Primero se suman las imágenes entrada por entrada:

```math
I_1+I_2=\begin{bmatrix}120+80&80+120&40+160\\60+140&200+40&100+100\\20+180&140+60&180+20\end{bmatrix}=\begin{bmatrix}200&200&200\\200&240&200\\200&200&200\end{bmatrix}
```

Luego se multiplica por $\tfrac12$ (se divide cada entrada entre 2):

```math
M=\tfrac12(I_1+I_2)=\begin{bmatrix}100&100&100\\100&120&100\\100&100&100\end{bmatrix}
```

Observación: la mezcla es casi un **gris uniforme** (todas las entradas valen 100, salvo el centro con 120). Las dos imágenes son casi opuestas (donde una es clara la otra es oscura), de modo que al promediarlas los contrastes se compensan. Además, cada entrada de $M$ queda entre las entradas correspondientes de $I_1$ e $I_2$.

**(d)** Las filas de $I_1$ pasan a ser columnas: la fila 1 $(120,80,40)$ es la columna 1, la fila 2 $(60,200,100)$ es la columna 2 y la fila 3 $(20,140,180)$ es la columna 3.

```math
I_1^T=\begin{bmatrix}120&60&20\\80&200&140\\40&100&180\end{bmatrix}
```

La transposición **intercambia filas por columnas**: el píxel de la posición $(i,j)$ pasa a la $(j,i)$. Es un **reflejo de la imagen respecto a la diagonal principal**; los píxeles de la diagonal (120, 200, 180) no se mueven.

---

## Ejercicio 14 — Sistema de recomendación

```math
R_1=\begin{bmatrix}5&3&0&4\\2&0&4&5\\1&4&5&0\end{bmatrix}\qquad R_2=\begin{bmatrix}4&4&1&5\\3&1&5&5\\0&5&4&2\end{bmatrix}
```

(Filas: Ana, Beto, Carla. Columnas: películas 1 a 4.)

**(a)** $R_1$ tiene 3 filas (usuarios) y 4 columnas (películas): tamaño **$3\times4$**.

- $`r_{23}=4`$ (fila 2, columna 3): **Beto** calificó la **película 3** con 4.
- $`r_{22}=0`$ (fila 2, columna 2): **Beto** aún **no ha calificado** la película 2. El 0 significa «sin calificar», no una nota de cero.

**(b)** Se suman las entradas que ocupan la misma posición:

```math
T=R_1+R_2=\begin{bmatrix}5+4&3+4&0+1&4+5\\2+3&0+1&4+5&5+5\\1+0&4+5&5+4&0+2\end{bmatrix}=\begin{bmatrix}9&7&1&9\\5&1&9&10\\1&9&9&2\end{bmatrix}
```

**(c)** Se multiplica cada entrada de $T$ por $\tfrac12$ (se divide entre 2):

```math
P=\tfrac12T=\begin{bmatrix}\frac92&\frac72&\frac12&\frac92\\[2pt]\frac52&\frac12&\frac92&\frac{10}{2}\\[2pt]\frac12&\frac92&\frac92&\frac22\end{bmatrix}=\begin{bmatrix}4{,}5&3{,}5&0{,}5&4{,}5\\2{,}5&0{,}5&4{,}5&5\\0{,}5&4{,}5&4{,}5&1\end{bmatrix}
```

Interpretación: es el promedio de los dos meses. Hay que tener cuidado porque los 0 significan «sin calificar»; por ejemplo, el $0{,}5$ de Ana en la película 3 no es una calificación real (solo la calificó en el mes 2, con 1).

**(d)** Las filas de $T$ pasan a ser columnas: la fila 1 $(9,7,1,9)$ es la columna 1 de $T^T$, la fila 2 $(5,1,9,10)$ es la columna 2 y la fila 3 $(1,9,9,2)$ es la columna 3.

```math
T^T=\begin{bmatrix}9&5&1\\7&1&9\\1&9&9\\9&10&2\end{bmatrix}
```

Tamaño: **$4\times3$** (porque $T$ es $3\times4$). Ahora **cada fila es una película** y cada columna es un usuario (Ana, Beto, Carla), con la calificación acumulada de los dos meses.

La fila 4 es el vector $(9,\ 10,\ 2)$: la película 4 acumuló 9 con Ana, 10 con Beto y 2 con Carla. Es una película **muy bien valorada por Ana y Beto** y poco por Carla (que solo la calificó en el mes 2, con 2).

**(e)** Se restan las entradas que ocupan la misma posición (mes 2 menos mes 1):

```math
D=R_2-R_1=\begin{bmatrix}4-5&4-3&1-0&5-4\\3-2&1-0&5-4&5-5\\0-1&5-4&4-5&2-0\end{bmatrix}=\begin{bmatrix}-1&1&1&1\\1&1&1&0\\-1&1&-1&2\end{bmatrix}
```

La entrada más grande de $D$ es $2$, en la fila 3, columna 4: el mayor aumento es de **Carla en la película 4** (de 0 a 2).

Observación: como el 0 del mes 1 significa «sin calificar», ese $+2$ es en realidad su primera calificación, no un cambio de opinión. Si solo se comparan calificaciones reales de ambos meses, el máximo aumento es $+1$ (hay varios casos empatados, por ejemplo Ana en la película 2 y Carla en la película 2).

---

## Ejercicio 15 — Embeddings de palabras

```math
E=\begin{bmatrix}2&1&0&3\\1&2&1&2\\0&0&5&0\end{bmatrix}\qquad F=\begin{bmatrix}0&3&2&1\\3&0&1&2\\2&2&1&4\end{bmatrix}
```

(Filas: modelo, datos, gato. Columnas: dim 1 a dim 4.)

**(a)** $E$ tiene 3 filas (palabras) y 4 columnas (dimensiones): tamaño **$3\times4$**. El vector de «datos» en el modelo A es la fila 2:

```math
\mathbf{datos}=(1,\ 2,\ 1,\ 2)
```

**(b)** Con $\mathbf{modelo}=(2,1,0,3)$ y $\mathbf{datos}=(1,2,1,2)$.

Normas:

```math
\lVert\mathbf{modelo}\rVert=\sqrt{2^2+1^2+0^2+3^2}=\sqrt{4+1+0+9}=\sqrt{14}\approx3{,}742
```

```math
\lVert\mathbf{datos}\rVert=\sqrt{1^2+2^2+1^2+2^2}=\sqrt{1+4+1+4}=\sqrt{10}\approx3{,}162
```

Producto punto:

```math
\mathbf{modelo}\cdot\mathbf{datos}=2(1)+1(2)+0(1)+3(2)=2+2+0+6=10
```

Similitud coseno. Se usa $\sqrt{14}\cdot\sqrt{10}=\sqrt{140}=\sqrt{4\cdot35}=2\sqrt{35}$, y luego se racionaliza:

```math
\cos\theta=\frac{10}{\sqrt{14}\cdot\sqrt{10}}=\frac{10}{2\sqrt{35}}=\frac{5}{\sqrt{35}}=\frac{5\sqrt{35}}{35}=\frac{\sqrt{35}}{7}\approx\frac{5{,}916}{7}\approx0{,}845
```

Interpretación: un coseno de $0{,}845$ (ángulo de unos $32{,}3^\circ$) está **cerca de 1**, así que «modelo» y «datos» apuntan en direcciones **bastante parecidas**: el modelo A las considera palabras **semánticamente relacionadas**.

**(c)** Con $\mathbf{gato}=(0,0,5,0)$:

```math
\mathbf{modelo}\cdot\mathbf{gato}=2(0)+1(0)+0(5)+3(0)=0+0+0+0=0
```

El producto punto es cero, así que **sí son ortogonales**. Significa que los vectores no comparten ninguna dirección (coseno $0$, ángulo de $90^\circ$): para el modelo A, «modelo» y «gato» **no tienen relación semántica**. Se ve en los datos: «gato» solo usa la dimensión 3 y «modelo» vale 0 en esa dimensión.

**(d)** Primero se suman las matrices entrada por entrada:

```math
E+F=\begin{bmatrix}2+0&1+3&0+2&3+1\\1+3&2+0&1+1&2+2\\0+2&0+2&5+1&0+4\end{bmatrix}=\begin{bmatrix}2&4&2&4\\4&2&2&4\\2&2&6&4\end{bmatrix}
```

Luego se multiplica por $\tfrac12$ (se divide cada entrada entre 2):

```math
E_n=\tfrac12(E+F)=\begin{bmatrix}1&2&1&2\\2&1&1&2\\1&1&3&2\end{bmatrix}
```

**(e)** Las filas de $E$ pasan a ser columnas: la fila 1 (modelo) es la columna 1 de $E^T$, la fila 2 (datos) es la columna 2 y la fila 3 (gato) es la columna 3.

```math
E^T=\begin{bmatrix}2&1&0\\1&2&0\\0&1&5\\3&2&0\end{bmatrix}
```

Tamaño: **$4\times3$** (porque $E$ es $3\times4$). Ahora **cada fila es una dimensión del embedding** y cada columna es una palabra (modelo, datos, gato).

La fila 3 es $(0,\ 1,\ 5)$: describe cómo se reparte la **dimensión 3** entre las palabras. «modelo» no la usa (0), «datos» la usa poco (1) y «gato» está **casi por completo en esa dimensión** (5). Es la dimensión que distingue a «gato» de las otras dos palabras.
