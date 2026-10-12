# Práctica en casa #1 (no evaluada) — Vectores, operaciones, axiomas, combinación lineal y producto punto

Todas las respuestas coinciden con las respuestas finales del PDF.

---

## Ejercicio 1 — Leer e igualar vectores

**(a)** $\mathbf{v}=(4,-1,0,7,2,-3)$ tiene 6 componentes: $n=6$ y $\mathbf{v}\in\mathbb{R}^6$. La componente 2 es $v_2=-1$ y la componente 5 es $v_5=2$.

**(b)** Igualdad de vectores = una ecuación por posición:

$$a+2=5\Rightarrow a=3\qquad 3b=-6\Rightarrow b=-2\qquad c-1=4\Rightarrow c=5$$

Verificación: $(3+2,\ 3(-2),\ 5-1)=(5,-6,4)$ ✓.

**(c)** **No.** Por definición, dos vectores son iguales si tienen la misma dimensión y coinciden componente a componente. $(0,3)\in\mathbb{R}^2$ y $(0,3,0)\in\mathbb{R}^3$ tienen dimensiones distintas.

---

## Ejercicio 2 — Suma, resta y escalar

**Datos:** $\mathbf{u}=(2,-1,3)$, $\mathbf{v}=(-1,4,0)$.

**(a)**

$$\mathbf{u}+\mathbf{v}=(2-1,\ -1+4,\ 3+0)=(1,\ 3,\ 3)$$

$$\mathbf{u}-\mathbf{v}=(2+1,\ -1-4,\ 3-0)=(3,\ -5,\ 3)$$

**(b)**

$$2\mathbf{u}=(4,-2,6)\qquad3\mathbf{v}=(-3,12,0)$$

$$2\mathbf{u}-3\mathbf{v}=(4+3,\ -2-12,\ 6-0)=(7,\ -14,\ 6)$$

**(c)**

$$-\mathbf{u}=(-2,1,-3)\qquad2\mathbf{v}=(-2,8,0)$$

$$-\mathbf{u}+2\mathbf{v}=(-4,\ 9,\ -3)$$

---

## Ejercicio 3 — Despejar un vector

**Ecuación:** $3\mathbf{x}-\mathbf{u}=\mathbf{x}+2\mathbf{v}$, con $\mathbf{u}=(4,-2)$, $\mathbf{v}=(1,3)$.

**(a)** Con letras, nombrando cada paso:

| Paso | Justificación |
|---|---|
| $3\mathbf{x}-\mathbf{u}=\mathbf{x}+2\mathbf{v}$ | ecuación original |
| $3\mathbf{x}-\mathbf{u}+\mathbf{u}=\mathbf{x}+2\mathbf{v}+\mathbf{u}$ | sumar $\mathbf{u}$ a ambos lados |
| $3\mathbf{x}=\mathbf{x}+2\mathbf{v}+\mathbf{u}$ | opuesto ($-\mathbf{u}+\mathbf{u}=\mathbf{0}$) y neutro |
| $3\mathbf{x}-\mathbf{x}=2\mathbf{v}+\mathbf{u}$ | sumar $-\mathbf{x}$ a ambos lados (opuesto) |
| $2\mathbf{x}=2\mathbf{v}+\mathbf{u}$ | distributiva sobre escalares: $3\mathbf{x}-1\mathbf{x}=(3-1)\mathbf{x}$ |
| $\tfrac12(2\mathbf{x})=\tfrac12(2\mathbf{v}+\mathbf{u})$ | multiplicar ambos lados por $\tfrac12$ |
| $\mathbf{x}=\tfrac12(2\mathbf{v}+\mathbf{u})$ | asociativa de escalares e identidad ($1\mathbf{x}=\mathbf{x}$) |

No se divide entre un vector: se escala por el inverso del escalar.

**(b)** Se sustituyen los datos:

$$2\mathbf{v}=(2,6)\qquad2\mathbf{v}+\mathbf{u}=(6,4)\qquad\mathbf{x}=\tfrac12(6,4)=(3,\ 2)$$

Verificación en la ecuación original:

$$3\mathbf{x}-\mathbf{u}=(9,6)-(4,-2)=(5,8)\qquad\mathbf{x}+2\mathbf{v}=(3,2)+(2,6)=(5,8)\ \checkmark$$

---

## Ejercicio 4 — Verificar y demostrar con los axiomas

**(a)** Distributiva $k(\mathbf{u}+\mathbf{v})=k\mathbf{u}+k\mathbf{v}$ con $k=-2$, $\mathbf{u}=(1,0,3)$, $\mathbf{v}=(2,-1,-1)$.

Lado izquierdo:

$$\mathbf{u}+\mathbf{v}=(3,-1,2)\qquad-2(3,-1,2)=(-6,\ 2,\ -4)$$

Lado derecho:

$$k\mathbf{u}=(-2,0,-6)\qquad k\mathbf{v}=(-4,2,2)\qquad k\mathbf{u}+k\mathbf{v}=(-6,\ 2,\ -4)$$

Ambos lados dan $(-6,2,-4)$ ✓.

**(b)** Conmutativa:

$$\mathbf{u}+\mathbf{v}=(1+2,\ 0-1,\ 3-1)=(3,-1,2)\qquad\mathbf{v}+\mathbf{u}=(2+1,\ -1+0,\ -1+3)=(3,-1,2)\ \checkmark$$

**(c) Demostración de $(-1)\mathbf{u}=-\mathbf{u}$.** Antes se necesita $0\mathbf{u}=\mathbf{0}$ (demostrado en la práctica 1): $0\mathbf{u}=(0+0)\mathbf{u}=0\mathbf{u}+0\mathbf{u}$; sumando el opuesto de $0\mathbf{u}$ a ambos lados queda $\mathbf{0}=0\mathbf{u}$.

| Paso | Justificación |
|---|---|
| $\mathbf{u}+(-1)\mathbf{u}=1\mathbf{u}+(-1)\mathbf{u}$ | identidad: $\mathbf{u}=1\mathbf{u}$ |
| $=(1+(-1))\mathbf{u}$ | distributiva sobre escalares |
| $=0\mathbf{u}$ | aritmética de reales |
| $=\mathbf{0}$ | resultado previo $0\mathbf{u}=\mathbf{0}$ |

Entonces $\mathbf{u}+(-1)\mathbf{u}=\mathbf{0}$. Se suma $-\mathbf{u}$ a ambos lados por la izquierda:

$$-\mathbf{u}+\mathbf{u}+(-1)\mathbf{u}=-\mathbf{u}+\mathbf{0}\ \Rightarrow\ \mathbf{0}+(-1)\mathbf{u}=-\mathbf{u}\ \Rightarrow\ (-1)\mathbf{u}=-\mathbf{u}\quad\blacksquare$$

(Usa el axioma del opuesto, la asociativa y el neutro.)

---

## Ejercicio 5 — Calcular combinaciones lineales

**(a)**

$$2(1,0,-1)=(2,0,-2)\qquad-3(2,1,0)=(-6,-3,0)\qquad(0,4,5)$$

$$\text{Suma}=(2-6+0,\ \ 0-3+4,\ \ -2+0+5)=(-4,\ 1,\ 3)$$

**(b)**

$$4\mathbf{v}_1=(12,-4)\qquad5\mathbf{v}_2=(-10,10)\qquad4\mathbf{v}_1+5\mathbf{v}_2=(2,\ 6)$$

Los coeficientes son $4$ y $5$.

---

## Ejercicio 6 — Combinación lineal con suma directa

**Datos:** $\mathbf{w}=(7,1)$, $\mathbf{v}_1=(1,1)$, $\mathbf{v}_2=(2,-1)$.

**(a)** Se plantea $c_1(1,1)+c_2(2,-1)=(7,1)$ y se separa por componentes:

$$\begin{cases}c_1+2c_2=7 & (1)\\ c_1-c_2=1 & (2)\end{cases}$$

**(b)** La incógnita $c_1$ tiene el mismo coeficiente (1) y el mismo signo en ambas. Se restan las ecuaciones, (1) − (2):

$$(c_1+2c_2)-(c_1-c_2)=7-1\ \Rightarrow\ 3c_2=6\ \Rightarrow\ c_2=2$$

**(c)** Se sustituye en (2): $c_1-2=1\Rightarrow c_1=3$.

Verificación:

$$3(1,1)+2(2,-1)=(3,3)+(4,-2)=(7,1)=\mathbf{w}\ \checkmark$$

Resultado: $\mathbf{w}=3\mathbf{v}_1+2\mathbf{v}_2$.

---

## Ejercicio 7 — Combinación lineal multiplicando antes de sumar

**Datos:** $\mathbf{w}=(4,13)$, $\mathbf{v}_1=(2,3)$, $\mathbf{v}_2=(1,-2)$.

**(a)**

$$\begin{cases}2c_1+c_2=4 & (1)\\ 3c_1-2c_2=13 & (2)\end{cases}$$

**(b)** Al sumar directamente queda $5c_1-c_2=17$: ninguna incógnita desaparece porque los coeficientes ($c_1$: 2 y 3; $c_2$: 1 y $-2$) no son opuestos. Conviene **multiplicar la ecuación (1) completa por 2**, para que $c_2$ quede con coeficiente $2$ frente al $-2$ de (2).

**(c)**

$$2\cdot(1):\ 4c_1+2c_2=8\qquad(1')$$

Se suma (1') con (2):

$$7c_1+0=21\ \Rightarrow\ c_1=3$$

Se sustituye en (1): $2(3)+c_2=4\Rightarrow c_2=-2$.

Verificación:

$$3(2,3)-2(1,-2)=(6,9)+(-2,4)=(4,13)=\mathbf{w}\ \checkmark$$

Resultado: $\mathbf{w}=3\mathbf{v}_1-2\mathbf{v}_2$ (un coeficiente negativo es válido: el vector se usa en sentido contrario).

---

## Ejercicio 8 — Generado (span) y subespacios

**(a)** Se busca $c$ con $c(1,2,3)=(-2,-4,-6)$:

$$c=-2,\quad 2c=-4,\quad 3c=-6\ \Rightarrow\ c=-2\ \text{ en las tres}$$

**Sí está** en el generado: $(-2,-4,-6)=-2(1,2,3)$.

**(b)** Se busca $c$ con $c(1,2,3)=(3,6,8)$: la primera posición da $c=3$ y la segunda $2c=6$ también, pero la tercera pide $3c=8$, y $3(3)=9\neq8$. Contradicción: **no está** en el generado.

**(c)** $S=\{(x,3x):x\in\mathbb{R}\}$ es la recta $y=3x$. Se verifican las tres condiciones en general:

1. **Contiene al cero:** con $x=0$ se obtiene $(0,0)\in S$.
2. **Cerrado bajo la suma:** $(a,3a)+(b,3b)=(a+b,\ 3a+3b)=(a+b,\ 3(a+b))\in S$.
3. **Cerrado bajo el escalar:** $k(a,3a)=(ka,\ 3(ka))\in S$.

**Sí es subespacio** de $\mathbb{R}^2$.

**(d)** $T=\{(x,3x+1):x\in\mathbb{R}\}$ es la recta $y=3x+1$, que no pasa por el origen. Falla la condición 1: para que $(0,0)\in T$ haría falta $x=0$ y $3(0)+1=0$, y $1\neq0$. Por tanto $(0,0)\notin T$ y **no es subespacio**.

(Tampoco es cerrado bajo la suma: $(x,3x+1)+(y,3y+1)=(x+y,\ 3(x+y)+2)$, que no cumple $y=3x+1$.)

---

## Ejercicio 9 — Producto punto: calcular y verificar propiedades

**Datos:** $\mathbf{a}=(2,-1,4)$, $\mathbf{b}=(3,5,-1)$, $\mathbf{c}=(1,0,2)$.

**(a)**

$$\mathbf{a}\cdot\mathbf{b}=2(3)+(-1)(5)+4(-1)=6-5-4=-3$$

$$\mathbf{a}\cdot\mathbf{c}=2(1)+(-1)(0)+4(2)=2+0+8=10$$

**(b)**

$$\mathbf{a}\cdot\mathbf{a}=4+1+16=21\qquad\lVert\mathbf{a}\rVert=\sqrt{21}\approx4{,}583$$

**(c)** Distributiva.

Lado izquierdo:

$$\mathbf{b}+\mathbf{c}=(4,5,1)\qquad\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=8-5+4=7$$

Lado derecho:

$$\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}=-3+10=7$$

$7=7$ ✓.

**(d)** $(3\mathbf{a})\cdot\mathbf{c}$ de dos formas:

- Escalando primero: $3\mathbf{a}=(6,-3,12)$, entonces $6(1)+(-3)(0)+12(2)=6+0+24=30$.
- Con la propiedad: $3(\mathbf{a}\cdot\mathbf{c})=3(10)=30$.

Coinciden ✓.

---

## Ejercicio 10 — Producto punto en un modelo y en una ecuación

**(a)** Pesos $\mathbf{w}=(1{,}5;\ -2;\ 0{,}5)$. La predicción es $\hat{y}=\mathbf{w}\cdot\mathbf{x}$.

$$\hat{y}_1=\mathbf{w}\cdot(4,1,6)=1{,}5(4)-2(1)+0{,}5(6)=6-2+3=7$$

$$\hat{y}_2=\mathbf{w}\cdot(2,3,10)=1{,}5(2)-2(3)+0{,}5(10)=3-6+5=2$$

**(b)** Se desarrolla el producto punto y se iguala a 6:

$$(k,2,-1)\cdot(3,k,4)=3k+2k-4=5k-4=6\ \Rightarrow\ 5k=10\ \Rightarrow\ k=2$$

Verificación: $(2,2,-1)\cdot(3,2,4)=6+4-4=6$ ✓.

**(c)**

- $\mathbf{u}\cdot(\mathbf{v}\cdot\mathbf{w})$ **no tiene sentido**: $\mathbf{v}\cdot\mathbf{w}$ es un número (escalar) y el producto punto solo se define entre dos vectores de la misma dimensión; no existe "vector · número".
- $(\mathbf{u}\cdot\mathbf{v})\mathbf{w}$ **sí tiene sentido**: $\mathbf{u}\cdot\mathbf{v}$ es un número y al multiplicarlo por el vector $\mathbf{w}$ (escalar por vector) se obtiene un **vector**, múltiplo de $\mathbf{w}$.
