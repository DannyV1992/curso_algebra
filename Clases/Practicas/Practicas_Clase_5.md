# Prácticas de la Clase 5 — Sistemas 2×2, producto punto, norma, ángulo y ortogonalidad

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University\
**Fuente:** `Clase 5 - guia sistemas 2x2.pdf` (ejercicios 1 a 3) y `Material del curso.pdf`, diapositivas 21–22 (práctica 5) y 25 (práctica 6)\
**Resumen de la clase:** [Resumen_Clase_5.md](../Resumenes/Resumen_Clase_5.md)

---

## Guía de sistemas 2×2

Se buscan $`c_1`$ y $`c_2`$ tales que $`c_1\mathbf{v}_1+c_2\mathbf{v}_2=\mathbf{w}`$. Método en 5 pasos:

1. **Plantear** la mezcla con los vectores del enunciado.
2. **Separar por componentes:** primera posición → ecuación (1); segunda → ecuación (2).
3. **Preparar y sumar:** lograr coeficientes opuestos en una incógnita, sumar y despejar la otra.
4. **Sustituir** el valor hallado en una ecuación original y despejar la segunda incógnita.
5. **Verificar** que la combinación dé exactamente $\mathbf{w}$.

Si se suman dos igualdades, el resultado sigue siendo una igualdad ($A=B$ y $C=D\Rightarrow A+C=B+D$). Si se multiplica una ecuación, se multiplica **completa** (ambos lados).

### Ejercicio 1: $\mathbf{w}=(5,1)$, $`\mathbf{v}_1=(1,1)`$, $`\mathbf{v}_2=(1,-1)`$

**Planteo.** $`c_1(1,1)+c_2(1,-1)=(c_1+c_2,\ c_1-c_2)=(5,1)`$, luego:

```math
\begin{cases}c_1+c_2=5\quad(1)\\ c_1-c_2=1\quad(2)\end{cases}
```

**Preparar y sumar.** $`+c_2`$ y $`-c_2`$ ya son opuestos, así que se suman directamente: $`2c_1=6\Rightarrow c_1=3`$.

**Sustituir** en (1): $`3+c_2=5\Rightarrow c_2=2`$.

**Verificar.** $3(1,1)+2(1,-1)=(3,3)+(2,-2)=(5,1)$ ✓. Resultado: $`\mathbf{w}=3\mathbf{v}_1+2\mathbf{v}_2`$.

### Ejercicio 2: $\mathbf{w}=(10,6)$, $`\mathbf{v}_1=(1,2)`$, $`\mathbf{v}_2=(3,-1)`$

**Planteo.** $`c_1(1,2)+c_2(3,-1)=(c_1+3c_2,\ 2c_1-c_2)=(10,6)`$, luego:

```math
\begin{cases}c_1+3c_2=10\quad(1)\\ 2c_1-c_2=6\quad(2)\end{cases}
```

**Preparar.** Los coeficientes de $`c_2`$ son $3$ y $-1$: tienen signo opuesto pero distinto tamaño. Se multiplica la ecuación (2) **completa** por 3:

```math
3\cdot(2c_1-c_2)=3\cdot6\ \Rightarrow\ 6c_1-3c_2=18\quad(2')
```

**Sumar** (1) y (2'): $`c_2`$ se cancela.

```math
\begin{aligned}
(c_1+3c_2)+(6c_1-3c_2)&=10+18\\
7c_1&=28\\
c_1&=4
\end{aligned}
```

**Sustituir** en (1): $`4+3c_2=10\Rightarrow 3c_2=6\Rightarrow c_2=2`$. Comprobación en (2): $2\cdot4-2=6$ ✓.

**Verificar.** $4(1,2)+2(3,-1)=(4,8)+(6,-2)=(10,6)$ ✓. Resultado: $`c_1=4,\ c_2=2`$.

### Ejercicio 3: $\mathbf{w}=(4,7)$, $`\mathbf{v}_1=(2,3)`$, $`\mathbf{v}_2=(1,1)`$

**Planteo.** $`c_1(2,3)+c_2(1,1)=(2c_1+c_2,\ 3c_1+c_2)=(4,7)`$, luego:

```math
\begin{cases}2c_1+c_2=4\quad(1)\\ 3c_1+c_2=7\quad(2)\end{cases}
```

**Preparar.** $`c_2`$ tiene el mismo coeficiente y el mismo signo en ambas: sumar lo duplicaría. Se multiplica (1) completa por $-1$ para obtener signos opuestos:

```math
-1\cdot(2c_1+c_2)=-1\cdot4\ \Rightarrow\ -2c_1-c_2=-4\quad(1')
```

**Sumar** (1') y (2):

```math
(-2c_1-c_2)+(3c_1+c_2)=-4+7\ \Rightarrow\ c_1=3
```

**Sustituir** en (1): $`2\cdot3+c_2=4\Rightarrow c_2=-2`$. Comprobación en (2): $3\cdot3-2=7$ ✓.

**Verificar.** $3(2,3)-2(1,1)=(6,9)-(2,2)=(4,7)$ ✓. Resultado: $`c_1=3,\ c_2=-2`$. Un peso negativo es válido: el vector se usa en sentido contrario.

**Resumen de qué hacer antes de sumar:**

| Situación | Acción |
|-----------|--------|
| Coeficientes opuestos ($`+c_2`$ y $`-c_2`$) | Sumar directamente (ejercicio 1) |
| Opuestos pero de distinto tamaño ($`3c_2`$ y $`-c_2`$) | Multiplicar una ecuación para igualar tamaños (ejercicio 2) |
| Mismo coeficiente y mismo signo ($`+c_2`$ y $`+c_2`$) | Multiplicar una ecuación por $-1$ (ejercicio 3) |

Errores comunes: multiplicar solo un lado de la ecuación y sumar sin haber preparado la cancelación (la incógnita se duplica en vez de desaparecer).

---

## Práctica 5 — Calcular y verificar propiedades del producto punto

**Datos:** $\mathbf{a}=(1,2,-3)$, $\mathbf{b}=(4,-1,2)$, $\mathbf{c}=(0,3,1)$. El producto punto multiplica posición por posición y suma; entran dos vectores y sale **un número**.

### a) $\mathbf{a}\cdot\mathbf{b}$ y $\mathbf{b}\cdot\mathbf{c}$

```math
\mathbf{a}\cdot\mathbf{b}=1\cdot4+2\cdot(-1)+(-3)\cdot2=4-2-6=-4
```

```math
\mathbf{b}\cdot\mathbf{c}=4\cdot0+(-1)\cdot3+2\cdot1=0-3+2=-1
```

Se escriben los productos parciales antes de sumar para que se vea el signo de cada uno.

### b) $\mathbf{a}\cdot\mathbf{a}$ y $\lVert\mathbf{a}\rVert$

```math
\mathbf{a}\cdot\mathbf{a}=1^2+2^2+(-3)^2=1+4+9=14
```

La norma es la raíz del producto punto consigo mismo: $\lVert\mathbf{a}\rVert=\sqrt{14}\approx3{,}742$.

### c) Verificar la distributiva $\mathbf{a}\cdot(\mathbf{b}+\mathbf{c})=\mathbf{a}\cdot\mathbf{b}+\mathbf{a}\cdot\mathbf{c}$

**Lado izquierdo:**

1. $\mathbf{b}+\mathbf{c}=(4+0,\ -1+3,\ 2+1)=(4,2,3)$
2. $\mathbf{a}\cdot(4,2,3)=4+4-9=-1$

**Lado derecho:**

1. $\mathbf{a}\cdot\mathbf{b}=-4$ (del apartado a)
2. $\mathbf{a}\cdot\mathbf{c}=1\cdot0+2\cdot3+(-3)\cdot1=0+6-3=3$
3. Suma: $-4+3=-1$

Los dos lados dan $-1$ ✓.

### d) $(2\mathbf{a})\cdot\mathbf{b}$ de dos maneras

**Escalando primero:** $2\mathbf{a}=(2,4,-6)$ y

```math
(2\mathbf{a})\cdot\mathbf{b}=2\cdot4+4\cdot(-1)+(-6)\cdot2=8-4-12=-8
```

**Con la propiedad 3** (el escalar sale del producto punto): $2(\mathbf{a}\cdot\mathbf{b})=2\cdot(-4)=-8$.

Ambas dan $-8$ ✓.

---

## Práctica 6 — Ángulos y ortogonalidad (evaluada)

Fórmulas usadas:

```math
\cos\theta=\frac{\mathbf{u}\cdot\mathbf{v}}{\lVert\mathbf{u}\rVert\,\lVert\mathbf{v}\rVert}\qquad\mathbf{u}\perp\mathbf{v}\iff\mathbf{u}\cdot\mathbf{v}=0
```

El signo del producto punto anticipa el ángulo: positivo → agudo, cero → recto, negativo → obtuso.

### a) Ángulo entre $(3,4)$ y $(4,3)$

1. Producto punto: $3\cdot4+4\cdot3=12+12=24$
2. Normas: $\sqrt{3^2+4^2}=5$ y $\sqrt{4^2+3^2}=5$
3. Coseno: $\cos\theta=\dfrac{24}{5\cdot5}=\dfrac{24}{25}=0{,}96$
4. Ángulo: $\theta=\arccos(0{,}96)\approx16{,}26^\circ$

El producto punto es positivo, así que el ángulo es agudo, como se obtuvo.

### b) ¿Son ortogonales $(1,-2,3)$ y $(4,5,2)$?

Basta un cálculo: el producto punto.

```math
1\cdot4+(-2)\cdot5+3\cdot2=4-10+6=0
```

Da cero, luego **sí son ortogonales**.

### c) Hallar $k$ para que $(k,3)\perp(2,-6)$

Se iguala el producto punto a cero y se despeja:

```math
k\cdot2+3\cdot(-6)=0\ \Rightarrow\ 2k-18=0\ \Rightarrow\ k=9
```

**Verificación:** $(9,3)\cdot(2,-6)=18-18=0$ ✓.

### d) Ángulo entre $(1,0)$ y $(-1,1)$

1. **Predicción por el signo:** $`(1,0)\cdot(-1,1)=1\cdot(-1)+0\cdot1=-1<0`$, así que el ángulo será **obtuso**.
2. Normas: $\lVert(1,0)\rVert=1$ y $\lVert(-1,1)\rVert=\sqrt2$
3. Coseno: $\cos\theta=\dfrac{-1}{1\cdot\sqrt2}\approx-0{,}707$
4. Ángulo: $\theta=\arccos(-0{,}707)=135^\circ$

135° es mayor que 90°, de modo que coincide con la predicción.
