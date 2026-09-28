# Clase 3 — Operar con datos: vectores y matrices

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos
**Semana:** 2 · 53 diapositivas
**Idea central:** *Una matriz mezcla columnas. Proyectar es explicar.*

> Objetivo de la clase: poder calcular a mano todo lo que NumPy hace con una sola línea.

---

## Ruta de la clase (4 bloques)

| Bloque | Tema | Contenido |
|---|---|---|
| 1 | **Vectores** | Definición, suma/resta/escalar, axiomas, combinación lineal |
| 2 | **Producto punto** | Definición y propiedades, ángulo y ortogonalidad, proyección ortogonal |
| 3 | **Matrices** | Definición, suma/escalar/transpuesta, matriz × vector, producto de matrices |
| 4 | **Aplicación** | Regresión como proyección, ecuaciones normales, laboratorio en NumPy |

Cada sección sigue el mismo patrón: **explicación → ejemplos resueltos → práctica → solución**.

---

## Bloque 1 · Vectores

### Definición
Un vector es una **lista ordenada de n números reales**:

$$\mathbf{v} = (v_1, v_2, \ldots, v_n) \in \mathbb{R}^n$$

- Cada número es una **componente**; $v_i$ es la componente en la posición $i$.
- **El orden importa:** $(3,2) \neq (2,3)$.
- La **dimensión** $n$ es la cantidad de componentes. Solo se operan vectores de la misma dimensión.
- Se interpreta como punto (posición) o flecha desde el origen. Por convención se escribe como columna; su transpuesta $\mathbf{v}^T$ es la fila.
- El vector cero $\mathbf{0} = (0,\ldots,0)$ es el origen.

### Igualdad
$$\mathbf{u} = \mathbf{v} \iff u_i = v_i \ \forall i$$

Una igualdad entre vectores de $\mathbb{R}^n$ equivale a **n ecuaciones escalares**, una por componente.

> ⚠️ Ojo con la indexación: matemáticamente $v_1$ es la primera componente, pero en NumPy sería `v[0]`.

### Operaciones básicas
$$\mathbf{u} \pm \mathbf{v} = (u_1 \pm v_1, \ldots, u_n \pm v_n) \qquad k\mathbf{u} = (ku_1, \ldots, ku_n)$$

- Todo se hace **componente a componente**: nunca se mezclan posiciones.
- Geometría: $\mathbf{u}+\mathbf{v}$ es la diagonal del paralelogramo; $\mathbf{u}-\mathbf{v}$ es la flecha que va de $\mathbf{v}$ hasta $\mathbf{u}$.
- El escalar estira ($k>1$), encoge ($0<k<1$) o invierte ($k<0$). La dirección (la recta) no cambia.
- **Orden de operaciones:** igual que en aritmética — primero escalares, luego sumas.

### Los 8 axiomas de espacio vectorial

**De la suma**

1. Conmutativa: $\mathbf{u}+\mathbf{v} = \mathbf{v}+\mathbf{u}$
2. Asociativa: $(\mathbf{u}+\mathbf{v})+\mathbf{w} = \mathbf{u}+(\mathbf{v}+\mathbf{w})$
3. Neutro: $\mathbf{u}+\mathbf{0} = \mathbf{u}$
4. Opuesto: $\mathbf{u}+(-\mathbf{u}) = \mathbf{0}$

**Del escalar**

5. Distributiva sobre vectores: $k(\mathbf{u}+\mathbf{v}) = k\mathbf{u}+k\mathbf{v}$
6. Distributiva sobre escalares: $(k+m)\mathbf{u} = k\mathbf{u}+m\mathbf{u}$
7. Asociativa de escalares: $k(m\mathbf{u}) = (km)\mathbf{u}$
8. Identidad: $1\mathbf{u} = \mathbf{u}$

Cada axioma se **hereda de los números reales**, porque se opera componente a componente. Un conjunto con suma y escalar que cumple los 8 axiomas es un **espacio vectorial**: $\mathbb{R}^n$ lo es, y también las matrices del mismo tamaño.

**Consecuencias demostrables:** $0\cdot\mathbf{u} = \mathbf{0}$ y $(-1)\mathbf{u} = -\mathbf{u}$.

> Despejar vectores es idéntico a despejar números, **siempre que no se divida entre un vector** (esa operación no existe).
>
> Una verificación numérica no demuestra un axioma; solo lo ilustra en un caso particular.

### Combinación lineal, generado y subespacios

$$\mathbf{w} = c_1\mathbf{v}_1 + c_2\mathbf{v}_2 + \cdots + c_k\mathbf{v}_k$$

- Los $c_i$ son los **coeficientes** (pesos). Solo se usan las dos operaciones básicas.
- **Generado (span):** $\text{gen}\{\mathbf{v}_1,\ldots,\mathbf{v}_k\}$ es todo lo que se puede alcanzar. Con un vector no nulo → una recta por el origen; con dos no paralelos en $\mathbb{R}^2$ → el plano completo.
- **Subespacio:** $S$ es subespacio si contiene a $\mathbf{0}$ y es cerrado bajo suma y escalar.
- Preguntar si $\mathbf{w}$ es combinación lineal de otros vectores = **resolver un sistema de ecuaciones**. Si tiene solución, está en el generado; si es inconsistente, no.
- Un modelo lineal predice con una combinación lineal de variables.

> Para probar que algo **NO** es subespacio basta un contraejemplo; para probar que **SÍ**, hay que verificar las tres condiciones en general.
> Una recta que no pasa por el origen (ej. $y = 2x+1$) nunca es subespacio: no contiene al vector cero.

---

## Bloque 2 · Producto punto

### Definición
$$\mathbf{u}\cdot\mathbf{v} = \sum_{i=1}^{n} u_i v_i = u_1v_1 + u_2v_2 + \cdots + u_nv_n$$

Multiplicar posición por posición y sumar todo. **Entran dos vectores de la misma dimensión y sale un solo número (escalar).**

### Propiedades
1. Conmutativa: $\mathbf{u}\cdot\mathbf{v} = \mathbf{v}\cdot\mathbf{u}$
2. Distributiva: $\mathbf{u}\cdot(\mathbf{v}+\mathbf{w}) = \mathbf{u}\cdot\mathbf{v} + \mathbf{u}\cdot\mathbf{w}$
3. Saca escalares: $(k\mathbf{u})\cdot\mathbf{v} = k(\mathbf{u}\cdot\mathbf{v})$
4. Positividad: $\mathbf{v}\cdot\mathbf{v} = \|\mathbf{v}\|^2 \geq 0$

**Conexión clave con ciencia de datos:** una predicción lineal es un producto punto — $\hat{y} = \mathbf{w}\cdot\mathbf{x}$. Cada peso dice cuánto aporta su variable.

También: la **norma** es un caso particular del producto punto, $\|\mathbf{v}\| = \sqrt{\mathbf{v}\cdot\mathbf{v}}$.

### Ángulo y ortogonalidad

**Fundamento — ley de cosenos.** En el triángulo formado por $\mathbf{u}$, $\mathbf{v}$ y $\mathbf{u}-\mathbf{v}$:

$$\|\mathbf{u}-\mathbf{v}\|^2 = \|\mathbf{u}\|^2 + \|\mathbf{v}\|^2 - 2\|\mathbf{u}\|\|\mathbf{v}\|\cos\theta$$

Expandiendo el lado izquierdo con las propiedades del producto punto:

$$(\mathbf{u}-\mathbf{v})\cdot(\mathbf{u}-\mathbf{v}) = \|\mathbf{u}\|^2 - 2\,\mathbf{u}\cdot\mathbf{v} + \|\mathbf{v}\|^2$$

Igualando y cancelando queda la fórmula del ángulo:

$$\cos\theta = \frac{\mathbf{u}\cdot\mathbf{v}}{\|\mathbf{u}\|\,\|\mathbf{v}\|} \qquad\qquad \mathbf{u} \perp \mathbf{v} \iff \mathbf{u}\cdot\mathbf{v} = 0$$

**El signo lo dice todo antes de calcular $\theta$:**

| Signo de $\mathbf{u}\cdot\mathbf{v}$ | Ángulo |
|---|---|
| Positivo | agudo ($\theta < 90°$) |
| Cero | recto ($\theta = 90°$, ortogonales) |
| Negativo | obtuso ($\theta > 90°$) |

> Ortogonal = sin información compartida. Es la idea que sostiene **PCA y la regresión**.
> Para decidir si dos vectores son ortogonales no hace falta calcular ninguna raíz ni ningún ángulo.

### Proyección ortogonal

**Pregunta:** ¿cuál es la mejor aproximación de $\mathbf{u}$ usando solo la dirección de $\mathbf{v}$?

**Deducción:** buscamos el $c\mathbf{v}$ más cercano a $\mathbf{u}$, es decir, el que deja $\mathbf{r} = \mathbf{u}-c\mathbf{v}$ perpendicular a $\mathbf{v}$:

$$(\mathbf{u}-c\mathbf{v})\cdot\mathbf{v} = 0 \implies \mathbf{u}\cdot\mathbf{v} - c(\mathbf{v}\cdot\mathbf{v}) = 0 \implies c = \frac{\mathbf{u}\cdot\mathbf{v}}{\mathbf{v}\cdot\mathbf{v}}$$

$$\boxed{\ \text{proj}_{\mathbf{v}}\mathbf{u} = \frac{\mathbf{u}\cdot\mathbf{v}}{\mathbf{v}\cdot\mathbf{v}}\,\mathbf{v} \qquad \mathbf{r} = \mathbf{u} - \text{proj}_{\mathbf{v}}\mathbf{u}\ }$$

- La proyección es la **sombra** de $\mathbf{u}$ sobre la recta de $\mathbf{v}$: el punto de esa recta más cercano a $\mathbf{u}$.
- El **residuo siempre es perpendicular** a $\mathbf{v}$ → $\mathbf{r}\cdot\mathbf{v}=0$ es la mejor comprobación que existe. Si no da cero, hay error de cálculo.
- $\mathbf{u} = \text{proyección} + \text{residuo perpendicular}$ = parte explicada + parte no explicada.
- La distancia de $\mathbf{u}$ a la recta de $\mathbf{v}$ es exactamente $\|\mathbf{r}\|$.

**Procedimiento en 3 pasos:** (1) calcular $c$, (2) multiplicar $c$ por $\mathbf{v}$, (3) restar para obtener el residuo. Luego comprobar $\mathbf{r}\cdot\mathbf{v}=0$.

**Casos especiales notables:**
- Proyectar sobre un eje (ej. $\mathbf{v}=(1,0)$) es simplemente quedarse con esa componente.
- Proyectar sobre $(1,1,\ldots,1)$ **reemplaza cada dato por el promedio**: el modelo más simple posible.

---

## Bloque 3 · Matrices

### Definición
$$A = \begin{bmatrix} a_{11} & \cdots & a_{1n} \\ \vdots & \ddots & \vdots \\ a_{m1} & \cdots & a_{mn}\end{bmatrix} \in \mathbb{R}^{m\times n} \qquad (A^T)_{ij} = a_{ji}$$

- Una matriz es una **tabla rectangular de números**. En datos: cada **fila es una observación** (un vector) y cada **columna una variable**. Un dataset de 1000 clientes y 8 variables es una matriz $1000\times 8$.
- Notación $a_{ij}$: **primero la fila $i$, después la columna $j$**.
- La transpuesta intercambia filas por columnas: $m\times n$ pasa a $n\times m$.

**Tipos especiales:**

| Tipo | Condición |
|---|---|
| Cuadrada | $m = n$ |
| Identidad $I_n$ | unos en la diagonal, ceros fuera |
| Diagonal | ceros fuera de la diagonal |
| Simétrica | $A = A^T$, es decir $a_{ij} = a_{ji}$ |

### Suma, escalar y transpuesta
$$(A+B)_{ij} = a_{ij}+b_{ij} \qquad (kA)_{ij} = k\,a_{ij}$$

- Igual que con vectores: **entrada por entrada**. Solo se suman matrices de la misma dimensión.
- Las matrices $m\times n$ también **forman un espacio vectorial** (cumplen los 8 axiomas).

**Propiedades de la transpuesta:**
$$(A^T)^T = A \qquad (A+B)^T = A^T + B^T \qquad (kA)^T = kA^T$$

> Una matriz se despeja igual que un vector: con opuestos y escalares, nunca "dividiendo entre una matriz".
> Conviene despejar primero con letras y sustituir al final.

### Matriz por vector

**El producto que une todo lo anterior.** Dos lecturas equivalentes:

**Por filas (productos punto)**
$$(A\mathbf{x})_i = \sum_{j=1}^{n} a_{ij}x_j = (\text{fila } i)\cdot\mathbf{x}$$

**Por columnas (combinación lineal)**
$$A\mathbf{x} = x_1\mathbf{a}_1 + x_2\mathbf{a}_2 + \cdots + x_n\mathbf{a}_n$$

- **Regla de dimensiones:** $(m\times n)\cdot(n) = (m)$. Las columnas de $A$ deben igualar las componentes de $\mathbf{x}$.
- $A\mathbf{x}$ vive en el **espacio generado por las columnas de $A$** (espacio columna).
- **En ciencia de datos:** $\hat{\mathbf{y}} = X\mathbf{w}$. $X$ guarda los datos (una fila por observación) y $\mathbf{w}$ los pesos. Un solo producto predice todas las observaciones a la vez.
- La **columna de unos** en $X$ es la que permite al modelo tener **intercepto**.

### Producto de matrices

$$A_{m\times n}B_{n\times p} = C_{m\times p}, \qquad c_{ij} = \sum_{k=1}^{n} a_{ik}b_{kj}$$

Entrada $(i,j)$ = **fila $i$ de $A$ · columna $j$ de $B$**. Equivale a aplicar "matriz por vector" a cada columna de $B$.

**Propiedades:**
1. **NO es conmutativo:** $AB \neq BA$ en general (y a veces una de las dos ni existe)
2. Asociativo: $(AB)C = A(BC)$
3. Distributivo: $A(B+C) = AB+AC$
4. Identidad: $AI = IA = A$
5. Transpuesta del producto (**se invierte el orden**): $(AB)^T = B^TA^T$

> **Regla de oro:** $(m\times n)(n\times p) = (m\times p)$. Las dimensiones internas deben coincidir y desaparecen.
> Multiplicar por la izquierda transforma **filas**; por la derecha, **columnas**.

---

## Bloque 4 · Aplicación: la regresión lineal es una proyección ortogonal

Con matrices, producto punto y proyección ya se deduce la regresión lineal **sin cálculo diferencial**.

### De la geometría a la fórmula

1. Todo lo que el modelo puede predecir es $X\mathbf{w}$: combinaciones de las columnas de $X$ (su **espacio columna**).
2. La mejor predicción es la **proyección de $\mathbf{y}$ sobre ese espacio**: el residuo $\mathbf{r} = \mathbf{y}-X\mathbf{w}$ debe ser ortogonal a cada columna de $X$.
3. "Ortogonal a cada columna" se escribe con la transpuesta, y al despejar aparecen las **ecuaciones normales**:

$$X^T(\mathbf{y}-X\mathbf{w}) = \mathbf{0} \implies \boxed{X^TX\,\mathbf{w} = X^T\mathbf{y}}$$

> **Mínimos cuadrados no es un truco de cálculo: es proyectar.** Minimizar $\|\mathbf{y}-X\mathbf{w}\|^2$ equivale a exigir que el error sea perpendicular a los datos.
>
> $\mathbf{y} = \text{parte explicada } (\hat{\mathbf{y}}) + \text{residuo } (\mathbf{r})$

### Procedimiento (4 pasos)
1. Armar $X$ (con columna de unos para el intercepto) y $\mathbf{y}$.
2. Calcular $X^TX$ y $X^T\mathbf{y}$.
3. Resolver el sistema de ecuaciones normales para obtener los pesos.
4. Calcular $\hat{\mathbf{y}}$ y el residuo $\mathbf{r}$; **comprobar que $X^T\mathbf{r} = \mathbf{0}$**.

**Ejemplo resuelto** — puntos $(1,1), (2,2), (3,2)$ con modelo $\hat{y} = a+bx$:

$$X = \begin{bmatrix}1&1\\1&2\\1&3\end{bmatrix},\quad \mathbf{y} = \begin{bmatrix}1\\2\\2\end{bmatrix},\quad X^TX = \begin{bmatrix}3&6\\6&14\end{bmatrix},\quad X^T\mathbf{y} = \begin{bmatrix}5\\11\end{bmatrix}$$

$$\begin{cases}3a+6b=5\\6a+14b=11\end{cases} \implies b = 0{,}5,\ a = \tfrac{2}{3} \implies \hat{y} = 0{,}667 + 0{,}5x$$

Comprobación: $\mathbf{r} = (-0{,}167;\ 0{,}333;\ -0{,}167)$, y $X^T\mathbf{r} = (0,0)$ ✓

**Dato importante:** los residuos **siempre suman cero** cuando el modelo tiene intercepto — es la ortogonalidad con la columna de unos. Y el residuo no tiene relación lineal con $x$.

---

## Laboratorio en NumPy

```python
import numpy as np

# vectores y operaciones
u = np.array([2, -1, 3]); v = np.array([4, 5, -2])
u + v, 3*u - 2*v          # componente a componente
u @ v                     # producto punto: -3

# ángulo y proyección
cos = u @ v / (np.linalg.norm(u) * np.linalg.norm(v))
proj = (u @ v) / (v @ v) * v
r = u - proj;  r @ v      # ~0: residuo ortogonal

# matrices
A = np.array([[1, 2], [3, 4]]); B = np.array([[0, 1], [1, 0]])
A.T, A + B, A @ B, B @ A  # AB != BA

# regresión como proyección
X = np.array([[1, 0], [1, 1], [1, 2]]); y = np.array([1, 3, 4])
w = np.linalg.solve(X.T @ X, X.T @ y)   # [1.1667, 1.5]
X.T @ (y - X @ w)                       # [0, 0]
```

**Qué observar:**
- `@` es el producto matricial (`u @ v` = producto punto, `A @ B` = producto de matrices). `A * B` multiplica **entrada por entrada**.
- El residuo sale ortogonal: `r @ v` y `X.T @ (y - X @ w)` dan cero salvo redondeo del orden de `1e-16`.
- `np.linalg.lstsq(X, y)` debe dar los mismos pesos que las ecuaciones normales.
- Otros: `B.T` (transpuesta), `B.shape` (dimensión). NumPy lanza error de forma (*shape mismatch*) al sumar vectores de distinta dimensión.

---

## Cómo se conecta con el resto del curso

| Semana | Tema | Depende de |
|---|---|---|
| **2 (hoy)** | Vectores, producto punto, matrices y proyección | — |
| 3 | Matrices como transformaciones, espacio columna, rango | **Sin $A\mathbf{x}$** no hay espacio columna, rango ni sistemas lineales |
| 4 y 7 | Cómputo matricial y rendimiento / GPU | **Sin $AB$** no hay composición de transformaciones ni cómputo en GPU |
| 5 | Autovalores y estabilidad | |
| 6 | SVD y PCA | **Sin proyección** no hay regresión, ni PCA, ni SVD |

> Si se dominan $A\mathbf{x}$ y la proyección, la mitad del curso ya es reconocible.

---

## Para llevarte

- Los vectores se operan **componente a componente**, y los 8 axiomas permiten despejarlos como números.
- El producto punto da **ángulos, normas y ortogonalidad**: $\mathbf{u}\cdot\mathbf{v}=0$ significa perpendicular.
- $A\mathbf{x}$ es una **combinación lineal de columnas**; $AB$ es fila por columna y $AB \neq BA$.
- La regresión **proyecta $\mathbf{y}$ sobre el espacio columna de $X$**: $X^TX\mathbf{w} = X^T\mathbf{y}$.

### Entregable · Trabajo individual 1
Notebook en Google Colab (`lab02_operaciones.ipynb`) con las **prácticas 5, 7, 11 y 12** verificadas en NumPy.

**Próxima clase:** matrices como transformaciones, espacio columna y rango.

---

## Índice de prácticas

| # | Tema | Diapositivas (práctica / solución) |
|---|---|---|
| 1 | Identificar y comparar vectores | 05 / 06 |
| 2 | Operaciones con vectores | 09 / 10 |
| 3 | Verificar, despejar y demostrar (axiomas) | 13 / 14 |
| 4 | Combinaciones, generado y subespacios | 17 / 18 |
| 5 | Producto punto: calcular y verificar propiedades ⭐ | 21 / 22 |
| 6 | Ángulos y ortogonalidad | 25 / 26 |
| 7 | Proyectar y comprobar ⭐ | 29 / 30 |
| 8 | Leer y transponer matrices | 33 / 34 |
| 9 | Operar y despejar matrices | 37 / 38 |
| 10 | Productos matriz-vector | 41 / 42 |
| 11 | Producto de matrices ⭐ | 45 / 46 |
| 12 | Una regresión completa a mano ⭐ | 49 / 50 |

⭐ = incluida en el entregable.

**Formato de cada práctica:** en parejas · 12 minutos · sin calculadora (excepto arcocoseno en la práctica 6).
