# Prácticas de la Clase 3 — Vectores: componentes, operaciones y axiomas

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University\
**Fuente:** `Material del curso.pdf`, diapositivas 5–6 (práctica 1), 9–10 (práctica 2) y 13–14 (práctica 3)\
**Resumen de la clase:** [Resumen_Clase_3.md](../Resumenes/Resumen_Clase_3.md)

Cada ejercicio se resuelve paso a paso. Regla general: **antes de operar, preguntarse qué dimensión tiene cada vector**.

---

## Práctica 1 — Leer e igualar vectores

### a) Dimensión y componentes de $\mathbf{v}=(-2,0,7,1,5)$

1. Se cuentan las componentes: $-2,\ 0,\ 7,\ 1,\ 5$ son **5** números.
2. La dimensión es $n=5$, luego $\mathbf{v}\in\mathbb{R}^5$.
3. La cuarta componente es la que está en la cuarta posición: $`v_4=1`$.

### b) Hallar $a$, $b$, $c$ en $(2a-1,\ b+3,\ c)=(5,0,-4)$

Dos vectores son iguales si coinciden **posición por posición**, así que cada posición da una ecuación:

```math
\begin{cases}2a-1=5\\ b+3=0\\ c=-4\end{cases}
```

Cada ecuación se resuelve por separado:

- $2a-1=5\Rightarrow 2a=6\Rightarrow a=3$
- $b+3=0\Rightarrow b=-3$
- $c=-4$ (ya está despejada)

**Verificación:** $(2\cdot3-1,\ -3+3,\ -4)=(5,0,-4)$ ✓. Resultado: $(a,b,c)=(3,-3,-4)$.

### c) Vector de una clienta

Datos: 29 años, ingreso de 850 (miles), 6 compras, 14 meses como cliente.

1. Se fija el **orden** de las variables: (edad, ingreso, compras, meses). El orden importa: si cambia, cambia el vector.
2. Se escribe cada dato en su posición: $\mathbf{x}=(29,\ 850,\ 6,\ 14)$.
3. Hay 4 componentes: dimensión $n=4$ y $\mathbf{x}\in\mathbb{R}^4$ (un punto de $\mathbb{R}^4$).

### d) ¿Son iguales?

| Comparación | Qué se revisa | Conclusión |
|-------------|---------------|------------|
| $(1,2)$ y $(2,1)$ | Misma dimensión (2), pero $`u_1=1\neq v_1=2`$ | **No** son iguales: el orden importa |
| $(1,2)$ y $(1,2,0)$ | $\mathbb{R}^2$ frente a $\mathbb{R}^3$ | **No** son iguales: dimensiones distintas |

Para ser iguales hacen falta las dos cosas: misma dimensión **y** mismas componentes en el mismo orden.

---

## Práctica 2 — Suma, resta y escalar

**Datos:** $\mathbf{a}=(1,-2,3)$, $\mathbf{b}=(4,0,-1)$, $\mathbf{c}=(-2,5,2)$. Los tres son de $\mathbb{R}^3$, así que se pueden operar entre sí. Se opera posición por posición.

### a) $\mathbf{a}+\mathbf{b}$ y $\mathbf{b}-\mathbf{c}$

```math
\mathbf{a}+\mathbf{b}=(1+4,\ -2+0,\ 3+(-1))=(5,\ -2,\ 2)
```

```math
\mathbf{b}-\mathbf{c}=(4-(-2),\ 0-5,\ -1-2)=(6,\ -5,\ -3)
```

Error frecuente: restar un número negativo suma ($4-(-2)=6$).

### b) $-3\mathbf{a}$ y $2\mathbf{a}-\mathbf{b}+\mathbf{c}$

**$-3\mathbf{a}$:** cada componente se multiplica por $-3$.

```math
-3\mathbf{a}=(-3\cdot1,\ -3\cdot(-2),\ -3\cdot3)=(-3,\ 6,\ -9)
```

**$2\mathbf{a}-\mathbf{b}+\mathbf{c}$:** primero se escala y luego se suma o resta, de izquierda a derecha.

1. $2\mathbf{a}=(2,-4,6)$
2. $2\mathbf{a}-\mathbf{b}=(2-4,\ -4-0,\ 6-(-1))=(-2,\ -4,\ 7)$
3. $(2\mathbf{a}-\mathbf{b})+\mathbf{c}=(-2-2,\ -4+5,\ 7+2)=(-4,\ 1,\ 9)$

### c) Hallar $\mathbf{x}$ en $\mathbf{x}+\mathbf{a}=\mathbf{b}$

1. Se suma $-\mathbf{a}$ a ambos lados: $\mathbf{x}=\mathbf{b}-\mathbf{a}$.
2. Se calcula: $\mathbf{x}=(4-1,\ 0-(-2),\ -1-3)=(3,\ 2,\ -4)$.

**Verificación:** $\mathbf{x}+\mathbf{a}=(3+1,\ 2-2,\ -4+3)=(4,0,-1)=\mathbf{b}$ ✓.

### d) $(1,2)+(1,2,3)$

**No se puede.** El primero es de $\mathbb{R}^2$ y el segundo de $\mathbb{R}^3$: la tercera componente del segundo no tiene pareja con quién sumarse. La suma solo está definida entre vectores de la misma dimensión.

---

## Práctica 3 — Verificar, despejar y demostrar (tarea)

### a) Verificar $(k+m)\mathbf{u}=k\mathbf{u}+m\mathbf{u}$ con $k=3$, $m=-1$, $\mathbf{u}=(2,5,-1)$

Se calculan los dos lados por separado.

**Lado izquierdo** (se suman los escalares primero): $k+m=3+(-1)=2$.

```math
(k+m)\mathbf{u}=2\,(2,5,-1)=(4,\ 10,\ -2)
```

**Lado derecho** (se escala cada vez y luego se suma):

1. $k\mathbf{u}=3(2,5,-1)=(6,\ 15,\ -3)$
2. $m\mathbf{u}=-1(2,5,-1)=(-2,\ -5,\ 1)$
3. $k\mathbf{u}+m\mathbf{u}=(6-2,\ 15-5,\ -3+1)=(4,\ 10,\ -2)$

Ambos lados dan $(4,10,-2)$ ✓. Esto **ilustra** la propiedad en un caso; no la demuestra en general.

### b) Verificar la asociativa con $\mathbf{u}=(1,2)$, $\mathbf{v}=(-3,4)$, $\mathbf{w}=(0,-5)$

**$(\mathbf{u}+\mathbf{v})+\mathbf{w}$:**

1. $\mathbf{u}+\mathbf{v}=(1-3,\ 2+4)=(-2,\ 6)$
2. $(-2,6)+\mathbf{w}=(-2+0,\ 6-5)=(-2,\ 1)$

**$\mathbf{u}+(\mathbf{v}+\mathbf{w})$:**

1. $\mathbf{v}+\mathbf{w}=(-3+0,\ 4-5)=(-3,\ -1)$
2. $\mathbf{u}+(-3,-1)=(1-3,\ 2-1)=(-2,\ 1)$

Los dos dan $(-2,1)$ ✓.

### c) Despejar $\mathbf{x}$ en $2\mathbf{x}+\mathbf{a}=5\mathbf{b}-\mathbf{x}$, con $\mathbf{a}=(3,-6)$ y $\mathbf{b}=(1,0)$

Primero con letras, nombrando el axioma de cada paso:

| Paso | Justificación |
|------|---------------|
| $2\mathbf{x}+\mathbf{a}=5\mathbf{b}-\mathbf{x}$ | ecuación original |
| $2\mathbf{x}+\mathbf{a}+\mathbf{x}=5\mathbf{b}-\mathbf{x}+\mathbf{x}$ | sumar $\mathbf{x}$ a ambos lados |
| $3\mathbf{x}+\mathbf{a}=5\mathbf{b}$ | distributiva sobre escalares ($2\mathbf{x}+1\mathbf{x}=3\mathbf{x}$), opuesto y neutro |
| $3\mathbf{x}+\mathbf{a}-\mathbf{a}=5\mathbf{b}-\mathbf{a}$ | sumar $-\mathbf{a}$ a ambos lados |
| $3\mathbf{x}=5\mathbf{b}-\mathbf{a}$ | opuesto y neutro |
| $\tfrac13(3\mathbf{x})=\tfrac13(5\mathbf{b}-\mathbf{a})$ | multiplicar ambos lados por $\tfrac13$ |
| $\mathbf{x}=\tfrac13(5\mathbf{b}-\mathbf{a})$ | asociativa de escalares e identidad |

No se divide entre un vector: se escala por el inverso del escalar.

Luego con los datos:

1. $5\mathbf{b}=(5,0)$
2. $5\mathbf{b}-\mathbf{a}=(5-3,\ 0-(-6))=(2,\ 6)$
3. $\mathbf{x}=\tfrac13(2,6)=\left(\tfrac23,\ 2\right)$

**Verificación en la ecuación original:**

- Izquierda: $2\mathbf{x}+\mathbf{a}=\left(\tfrac43+3,\ 4-6\right)=\left(\tfrac{13}{3},\ -2\right)$
- Derecha: $5\mathbf{b}-\mathbf{x}=\left(5-\tfrac23,\ 0-2\right)=\left(\tfrac{13}{3},\ -2\right)$ ✓

### d) Demostrar que $0\cdot\mathbf{u}=\mathbf{0}$ usando solo los axiomas

Idea: escribir el escalar $0$ como $0+0$ y usar la distributiva.

| Paso | Justificación |
|------|---------------|
| $0\mathbf{u}=(0+0)\mathbf{u}$ | porque $0=0+0$ en los reales |
| $(0+0)\mathbf{u}=0\mathbf{u}+0\mathbf{u}$ | distributiva sobre escalares |
| $0\mathbf{u}=0\mathbf{u}+0\mathbf{u}$ | de los dos pasos anteriores |
| $0\mathbf{u}+(-(0\mathbf{u}))=(0\mathbf{u}+0\mathbf{u})+(-(0\mathbf{u}))$ | sumar el opuesto de $0\mathbf{u}$ a ambos lados |
| $\mathbf{0}=0\mathbf{u}+\left(0\mathbf{u}+(-(0\mathbf{u}))\right)$ | opuesto a la izquierda; asociativa a la derecha |
| $\mathbf{0}=0\mathbf{u}+\mathbf{0}$ | opuesto |
| $\mathbf{0}=0\mathbf{u}$ | neutro |

Queda demostrado: $0\cdot\mathbf{u}=\mathbf{0}$.

### Ejercicio adicional sugerido: $(-1)\mathbf{u}=-\mathbf{u}$

1. $\mathbf{u}+(-1)\mathbf{u}=1\mathbf{u}+(-1)\mathbf{u}$ (identidad)
2. $=(1+(-1))\mathbf{u}$ (distributiva sobre escalares)
3. $=0\mathbf{u}=\mathbf{0}$ (resultado del ejercicio d)
4. Se suma $-\mathbf{u}$ a ambos lados de $\mathbf{u}+(-1)\mathbf{u}=\mathbf{0}$ y se simplifica con opuesto, asociativa y neutro: $(-1)\mathbf{u}=-\mathbf{u}$.
