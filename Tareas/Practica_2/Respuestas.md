# Práctica en casa evaluada #2 — Norma, producto punto, ortogonalidad, proyecciones y combinaciones lineales

## Fórmulas usadas

| Concepto | Fórmula |
|---|---|
| Norma | $\lVert\mathbf{v}\rVert=\sqrt{\mathbf{v}\cdot\mathbf{v}}=\sqrt{v_1^2+\cdots+v_n^2}$ |
| Distancia | $d(\mathbf{u},\mathbf{v})=\lVert\mathbf{u}-\mathbf{v}\rVert$ |
| Ángulo | $\cos\theta=\dfrac{\mathbf{u}\cdot\mathbf{v}}{\lVert\mathbf{u}\rVert\lVert\mathbf{v}\rVert}$ |
| Ortogonalidad | $\mathbf{u}\perp\mathbf{v}\iff\mathbf{u}\cdot\mathbf{v}=0$ |
| Proyección | $`\mathrm{proj}_{\mathbf{v}}\mathbf{u}=\dfrac{\mathbf{u}\cdot\mathbf{v}}{\mathbf{v}\cdot\mathbf{v}}\mathbf{v}`$, con residuo $`\mathbf{r}=\mathbf{u}-\mathrm{proj}_{\mathbf{v}}\mathbf{u}\perp\mathbf{v}`$ |

---

## Ejercicio 1 — Norma

**Datos:** $\mathbf{u}=(3,-4,12)$.

**(a)**

$$\lVert\mathbf{u}\rVert=\sqrt{3^2+(-4)^2+12^2}=\sqrt{9+16+144}=\sqrt{169}=13$$

**(b)** Se divide cada componente entre la norma:

$$\hat{\mathbf{u}}=\frac{\mathbf{u}}{13}=\left(\tfrac{3}{13},\ -\tfrac{4}{13},\ \tfrac{12}{13}\right)$$

$$\lVert\hat{\mathbf{u}}\rVert=\sqrt{\tfrac{9}{169}+\tfrac{16}{169}+\tfrac{144}{169}}=\sqrt{\tfrac{169}{169}}=\sqrt{1}=1\ \checkmark$$

**(c)** $\mathbf{w}=(-6,8,-24)$. Directamente:

$$\lVert\mathbf{w}\rVert=\sqrt{36+64+576}=\sqrt{676}=26$$

Con la propiedad: $\lvert-2\rvert\cdot\lVert\mathbf{u}\rVert=2\cdot13=26$.

**Conclusión:** coinciden, $\lVert k\mathbf{u}\rVert=\lvert k\rvert\cdot\lVert\mathbf{u}\rVert$. El signo negativo invierte el sentido pero no cambia la longitud.

---

## Ejercicio 2 — Distancia

**Datos:** $A=(1,2,3)$, $B=(3,0,4)$, $C=(0,2,5)$.

**(a)**

$$A-B=(1-3,\ 2-0,\ 3-4)=(-2,\ 2,\ -1)$$

$$d(A,B)=\sqrt{4+4+1}=\sqrt{9}=3$$

**(b)**

$$A-C=(1-0,\ 2-2,\ 3-5)=(1,\ 0,\ -2)$$

$$d(A,C)=\sqrt{1+0+4}=\sqrt{5}\approx2{,}236$$

Como $\sqrt5<3$, el punto **$C$ está más cerca de $A$**.

**(c)** Se iguala la distancia a 5 y se eleva al cuadrado:

$$d\big((1,k),(4,0)\big)=\sqrt{(1-4)^2+(k-0)^2}=\sqrt{9+k^2}=5$$

$$9+k^2=25\ \Rightarrow\ k^2=16\ \Rightarrow\ k=4\ \text{ o }\ k=-4$$

Verificación: $\sqrt{9+16}=5$ para ambos valores.

---

## Ejercicio 3 — Producto punto

**Datos:** $\mathbf{a}=(2,-3,1)$, $\mathbf{b}=(4,1,-5)$, $\mathbf{c}=(-1,2,3)$.

**(a)**

$$\mathbf{a}\cdot\mathbf{c}=2(-1)+(-3)(2)+1(3)=-2-6+3=-5$$

$$\mathbf{b}\cdot\mathbf{c}=4(-1)+1(2)+(-5)(3)=-4+2-15=-17$$

**(b)** Distributiva $\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}$.

Lado izquierdo:

$$\mathbf{b}+\mathbf{c}=(3,\ 3,\ -2)\qquad\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=6-9-2=-5$$

Lado derecho:

$$\mathbf{a}\cdot\mathbf{b}=2(4)+(-3)(1)+1(-5)=8-3-5=0\qquad\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}=0+(-5)=-5$$

Ambos lados dan $-5$ ✓.

**(c)** $(3\mathbf{a})\cdot\mathbf{c}$ de dos maneras:

- Escalando primero: $3\mathbf{a}=(6,-9,3)$, entonces $(6)(-1)+(-9)(2)+(3)(3)=-6-18+9=-15$.
- Con la propiedad: $3(\mathbf{a}\cdot\mathbf{c})=3(-5)=-15$.

Coinciden ✓.

**(d)** $\mathbf{a}\cdot\mathbf{b}=0$ significa que **$\mathbf{a}$ y $\mathbf{b}$ son ortogonales**: forman un ángulo de $90^\circ$ y no comparten ninguna dirección.

---

## Ejercicio 4 — Ángulo

**(a)** $\mathbf{u}=(2,2)$, $\mathbf{v}=(0,3)$.

$$\mathbf{u}\cdot\mathbf{v}=0+6=6\qquad\lVert\mathbf{u}\rVert=\sqrt8=2\sqrt2\qquad\lVert\mathbf{v}\rVert=3$$

$$\cos\theta=\frac{6}{2\sqrt2\cdot3}=\frac{1}{\sqrt2}=\frac{\sqrt2}{2}\approx0{,}707\ \Rightarrow\ \theta=45^\circ$$

**(b)** $\mathbf{u}=(1,0,1)$, $\mathbf{v}=(0,1,1)$.

$$\mathbf{u}\cdot\mathbf{v}=0+0+1=1\qquad\lVert\mathbf{u}\rVert=\lVert\mathbf{v}\rVert=\sqrt2$$

$$\cos\theta=\frac{1}{\sqrt2\cdot\sqrt2}=\frac12\ \Rightarrow\ \theta=60^\circ$$

**(c)** $\mathbf{u}=(-2,1)$, $\mathbf{v}=(3,4)$.

Predicción por el signo: $\mathbf{u}\cdot\mathbf{v}=-6+4=-2<0$, por lo tanto el ángulo es **obtuso**.

Confirmación:

$$\lVert\mathbf{u}\rVert=\sqrt5\qquad\lVert\mathbf{v}\rVert=5\qquad\cos\theta=\frac{-2}{5\sqrt5}=-\frac{2\sqrt5}{25}\approx-0{,}179$$

$$\theta=\arccos(-0{,}179)\approx100{,}3^\circ>90^\circ\ \checkmark$$

---

## Ejercicio 5 — Ortogonalidad

**(a)** $\mathbf{u}=(3,-1,2)$, $\mathbf{v}=(1,5,1)$.

$$\mathbf{u}\cdot\mathbf{v}=3-5+2=0$$

Como el producto punto es cero, **sí son ortogonales**.

**(b)** Se iguala el producto punto a cero:

$$(k,3,-2)\cdot(3,k,6)=3k+3k-12=6k-12=0\ \Rightarrow\ k=2$$

Verificación: $(2,3,-2)\cdot(3,2,6)=6+6-12=0$ ✓.

**(c)** Para $(3,4)$ se intercambian las componentes y se cambia el signo de una: $\mathbf{w}=(-4,3)$.

$$(3,4)\cdot(-4,3)=-12+12=0\ \checkmark$$

Para cualquier múltiplo $t\mathbf{w}$, con $t\in\mathbb{R}$, se usa la propiedad de sacar escalares:

$$(t\mathbf{w})\cdot(3,4)=t\big(\mathbf{w}\cdot(3,4)\big)=t\cdot0=0$$

Todo múltiplo de $(-4,3)$ es ortogonal a $(3,4)$: son los vectores de la recta perpendicular por el origen.

---

## Ejercicio 6 — Proyección ortogonal

**Datos:** $\mathbf{u}=(4,7)$, $\mathbf{v}=(2,1)$.

**(a)**

$$\mathbf{u}\cdot\mathbf{v}=8+7=15\qquad\mathbf{v}\cdot\mathbf{v}=4+1=5\qquad c=\frac{15}{5}=3$$

$$\mathrm{proj}_{\mathbf{v}}\mathbf{u}=3(2,1)=(6,\ 3)$$

**(b)**

$$\mathbf{r}=\mathbf{u}-\mathrm{proj}_{\mathbf{v}}\mathbf{u}=(4-6,\ 7-3)=(-2,\ 4)$$

$$\mathbf{r}\cdot\mathbf{v}=(-2)(2)+(4)(1)=-4+4=0\ \checkmark$$

**(c)**

$$\lVert\mathbf{r}\rVert=\sqrt{4+16}=\sqrt{20}=2\sqrt5\approx4{,}472$$

Geométricamente, $\lVert\mathbf{r}\rVert$ es la **distancia perpendicular (la más corta) del punto $\mathbf{u}$ a la recta generada por $\mathbf{v}$**. La proyección $(6,3)$ es el punto de esa recta más cercano a $\mathbf{u}$.

---

## Ejercicio 7 — Proyección sobre el vector de unos

**Datos:** $\mathbf{u}=(2,6,10)$, $\mathbf{v}=(1,1,1)$.

**(a)**

$$\mathbf{u}\cdot\mathbf{v}=2+6+10=18\qquad\mathbf{v}\cdot\mathbf{v}=3\qquad c=\frac{18}{3}=6$$

$$\mathrm{proj}_{\mathbf{v}}\mathbf{u}=6(1,1,1)=(6,\ 6,\ 6)$$

**(b)** En general, para $\mathbf{v}=(1,\ldots,1)\in\mathbb{R}^n$:

$$c=\frac{\mathbf{u}\cdot\mathbf{v}}{\mathbf{v}\cdot\mathbf{v}}=\frac{u_1+\cdots+u_n}{n}$$

El coeficiente $c$ es el **promedio (media aritmética)** de las componentes de $\mathbf{u}$: $\frac{2+6+10}{3}=6$. Proyectar sobre el vector de unos reemplaza cada componente por la media.

**(c)**

$$\mathbf{r}=\mathbf{u}-\mathrm{proj}_{\mathbf{v}}\mathbf{u}=(2-6,\ 6-6,\ 10-6)=(-4,\ 0,\ 4)$$

$$\mathbf{r}\cdot\mathbf{v}=-4+0+4=0\ \checkmark$$

$$\lVert\mathbf{r}\rVert^2=16+0+16=32$$

Las componentes de $\mathbf{r}$ son las desviaciones respecto a la media; $\lVert\mathbf{r}\rVert^2$ es la suma de los cuadrados de esas desviaciones (la base de la varianza).

---

## Ejercicio 8 — Combinación lineal

**Datos:** $\mathbf{w}=(7,-7)$, $\mathbf{v}_1=(2,1)$, $\mathbf{v}_2=(1,-3)$.

**(a)** Se plantea $c_1(2,1)+c_2(1,-3)=(7,-7)$ y se separa por componentes:

$$\begin{cases}2c_1+c_2=7 & (1)\\ c_1-3c_2=-7 & (2)\end{cases}$$

**(b)** Sumar directamente no cancela nada. Se multiplica **toda** la ecuación (1) por 3 para que $c_2$ quede con coeficientes opuestos:

$$6c_1+3c_2=21\qquad(1')$$

Se suma (1') con (2), término a término:

$$7c_1+0=14\ \Rightarrow\ c_1=2$$

Se sustituye en (1): $2(2)+c_2=7\Rightarrow c_2=3$.

**(c)** Verificación:

$$2(2,1)+3(1,-3)=(4,2)+(3,-9)=(7,-7)=\mathbf{w}\ \checkmark$$

Resultado: $\mathbf{w}=2\mathbf{v}_1+3\mathbf{v}_2$.

---

## Ejercicio 9 — Generado, combinaciones y atajo con ortogonalidad

**(a)** Se busca $c$ con $c(2,-1,3)=(6,-3,9)$:

$$2c=6,\quad -c=-3,\quad 3c=9\ \Rightarrow\ c=3\ \text{ en las tres posiciones}$$

**Sí está** en el generado: $(6,-3,9)=3(2,-1,3)$.

**(b)** Se plantea $c_1(1,0,1)+c_2(0,1,1)=(x,y,z)$, es decir $c_1=x$, $c_2=y$, $c_1+c_2=z$.

- Para $(1,2,3)$: $c_1=1$, $c_2=2$, y la tercera ecuación $1+2=3$ ✓. **Sí es combinación lineal**: $(1,2,3)=1(1,0,1)+2(0,1,1)$.
- Para $(1,2,4)$: $c_1=1$, $c_2=2$, pero la tercera pide $1+2=4$, que es falso. El sistema es inconsistente: **no es combinación lineal**.

**(c)** $\mathbf{u}=(1,1)$, $\mathbf{v}=(1,-1)$:

$$\mathbf{u}\cdot\mathbf{v}=1-1=0\ \checkmark$$

Con $\mathbf{w}=(5,1)$:

$$\mathbf{w}\cdot\mathbf{u}=6\quad\mathbf{u}\cdot\mathbf{u}=2\quad c_1=\frac{6}{2}=3\qquad\qquad\mathbf{w}\cdot\mathbf{v}=5-1=4\quad\mathbf{v}\cdot\mathbf{v}=2\quad c_2=\frac{4}{2}=2$$

$$c_1\mathbf{u}+c_2\mathbf{v}=3(1,1)+2(1,-1)=(3,3)+(2,-2)=(5,1)=\mathbf{w}\ \checkmark$$

**(d)** Se parte de $\mathbf{w}=c_1\mathbf{u}+c_2\mathbf{v}$ y se hace el producto punto con $\mathbf{u}$ en ambos lados, usando distributiva y saca-escalares:

$$\mathbf{w}\cdot\mathbf{u}=c_1(\mathbf{u}\cdot\mathbf{u})+c_2(\mathbf{v}\cdot\mathbf{u})$$

Como $\mathbf{u}\perp\mathbf{v}$, se tiene $\mathbf{v}\cdot\mathbf{u}=0$ y el segundo término **se anula**:

$$\mathbf{w}\cdot\mathbf{u}=c_1(\mathbf{u}\cdot\mathbf{u})\ \Rightarrow\ c_1=\frac{\mathbf{w}\cdot\mathbf{u}}{\mathbf{u}\cdot\mathbf{u}}\quad(\mathbf{u}\neq\mathbf{0})$$

Lo mismo con $\mathbf{v}$ da $c_2$. Sin ortogonalidad, el término cruzado no se anula y habría que resolver un sistema de ecuaciones. Con ortogonalidad, cada coeficiente sale de una proyección independiente.

---

## Ejercicio 10 — Buscador semántico

| Vector | IA | Deportes | Datos | Cocina |
|---|---|---|---|---|
| $\mathbf{q}$ | 3 | 0 | 4 | 0 |
| $\mathbf{d}_1$ | 6 | 0 | 8 | 0 |
| $\mathbf{d}_2$ | 0 | 5 | 0 | 12 |
| $\mathbf{d}_3$ | 4 | 3 | 0 | 0 |
| $\mathbf{d}_4$ | 1 | 0 | 1 | 0 |

**(a) Normas**

$$\lVert\mathbf{q}\rVert=\sqrt{9+16}=5\qquad\lVert\mathbf{d}_1\rVert=\sqrt{36+64}=10\qquad\lVert\mathbf{d}_2\rVert=\sqrt{25+144}=13$$

$$\lVert\mathbf{d}_3\rVert=\sqrt{16+9}=5\qquad\lVert\mathbf{d}_4\rVert=\sqrt{1+1}=\sqrt2\approx1{,}414$$

El vector más largo es **$\mathbf{d}_2$** (norma 13), pero **no** es el más relevante: ni siquiera habla de los temas de la consulta (IA y datos). La norma mide cuánto texto o cuánta "cantidad" hay, no de qué trata.

**(b) Similitud coseno**

| Documento | Producto punto con q | Similitud coseno |
|---|---|---|
| $\mathbf{d}_1$ | $18+0+32+0=50$ | $\dfrac{50}{5\cdot10}=1$ |
| $\mathbf{d}_2$ | $0+0+0+0=0$ | $0$ |
| $\mathbf{d}_3$ | $12+0+0+0=12$ | $\dfrac{12}{5\cdot5}=0{,}48$ |
| $\mathbf{d}_4$ | $3+0+4+0=7$ | $\dfrac{7}{5\sqrt2}=\dfrac{7\sqrt2}{10}\approx0{,}990$ |

La similitud coseno es $\cos\theta=\dfrac{\mathbf{q}\cdot\mathbf{d}}{\lVert\mathbf{q}\rVert\lVert\mathbf{d}\rVert}$ para cada documento $\mathbf{d}$.

**(c) Ranking** (de más a menos relevante):

1. $\mathbf{d}_1$ (cos = 1)
2. $\mathbf{d}_4$ (cos ≈ 0,990)
3. $\mathbf{d}_3$ (cos = 0,48)
4. $\mathbf{d}_2$ (cos = 0)

El único ortogonal a $\mathbf{q}$ es **$\mathbf{d}_2$** ($\mathbf{q}\cdot\mathbf{d}_2=0$): no comparte ningún tema con la consulta (ella habla de IA y datos; el documento, de deportes y cocina). $\mathbf{d}_3$ no es ortogonal porque comparte el tema IA.

**(d) Distancias**

$$\mathbf{q}-\mathbf{d}_1=(-3,0,-4,0)\ \Rightarrow\ d(\mathbf{q},\mathbf{d}_1)=\sqrt{9+16}=5$$

$$\mathbf{q}-\mathbf{d}_4=(2,0,3,0)\ \Rightarrow\ d(\mathbf{q},\mathbf{d}_4)=\sqrt{4+9}=\sqrt{13}\approx3{,}606$$

Según la distancia, **$\mathbf{d}_4$ queda más cerca** de $\mathbf{q}$. **No coincide** con el ranking del inciso (c), donde $\mathbf{d}_1$ es el primero.

**(e)** La distancia mezcla dirección y longitud: $\mathbf{d}_1=2\mathbf{q}$ trata exactamente los mismos temas y en la misma proporción que la consulta, pero por ser un documento largo queda lejos. La similitud coseno depende solo del **ángulo** (la proporción de temas), no de la longitud; por eso un documento largo y uno corto con el mismo contenido reciben la misma similitud. Es la medida adecuada para comparar textos de distinta longitud.

**(f) Normalización**

$$\hat{\mathbf{q}}=\frac{\mathbf{q}}{5}=(0{,}6;\ 0;\ 0{,}8;\ 0)\qquad\hat{\mathbf{d}}_1=\frac{\mathbf{d}_1}{10}=(0{,}6;\ 0;\ 0{,}8;\ 0)$$

Los dos vectores normalizados son **idénticos**: tienen la misma dirección y solo diferían en longitud. Con vectores de norma 1, el denominador de la similitud coseno vale 1, así que se **reduce al producto punto**:

$$\cos\theta=\hat{\mathbf{q}}\cdot\hat{\mathbf{d}}_1=0{,}36+0{,}64=1$$
