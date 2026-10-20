# Prácticas de la Clase 6 — Matrices: lectura y transpuesta

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University\
**Fuente:** `Material del curso.pdf`, diapositivas 33–34 (práctica 8)\
**Resumen de la clase:** [Resumen_Clase_6.md](../Resumenes/Resumen_Clase_6.md)

La solución de la práctica 6 (ángulos y ortogonalidad, diapositivas 25–26) está resuelta paso a paso en [Practicas_Clase_5.md](Practicas_Clase_5.md). La práctica 9 (operar y despejar matrices, diapositivas 37–38) se resuelve cuando se cubra en clase.

Orden para leer una matriz: **dimensión** (filas × columnas, primero filas), luego **entradas** $`a_{ij}`$ (primero la fila, después la columna) y por último **filas y columnas completas** como vectores.

---

## Práctica 8 — Leer y transponer matrices

**Datos:**

```math
B=\begin{bmatrix}3&0&-2&1\\4&6&5&-1\\7&-3&8&2\end{bmatrix}\qquad C=\begin{bmatrix}2&1\\3&2\end{bmatrix}
```

### a) Dimensión de $B$ y las entradas $`b_{23}`$, $`b_{31}`$, $`b_{14}`$

1. **Dimensión:** se cuentan 3 filas y 4 columnas, luego $B$ es $3\times4$.
2. **Entradas:** en $`b_{ij}`$ el primer índice es la fila y el segundo la columna.
   - $`b_{23}`$: fila 2, columna 3. La fila 2 es $(4,6,5,-1)$ y su tercer elemento es $5$.
   - $`b_{31}`$: fila 3, columna 1. La fila 3 es $(7,-3,8,2)$ y su primer elemento es $7$.
   - $`b_{14}`$: fila 1, columna 4. La fila 1 es $(3,0,-2,1)$ y su cuarto elemento es $1$.

**Resultado:** $B\in\mathbb{R}^{3\times4}$, $`b_{23}=5`$, $`b_{31}=7`$, $`b_{14}=1`$.

### b) Fila 2 y columna 3 de $B$ como vectores

- **Fila 2:** se lee de izquierda a derecha, $(4,\ 6,\ 5,\ -1)$. Es un vector de $\mathbb{R}^4$: una observación con 4 variables.
- **Columna 3:** se lee de arriba abajo, $(-2,\ 5,\ 8)$. Es un vector de $\mathbb{R}^3$: una variable medida en 3 observaciones.

### c) Transpuesta $B^\top$

La transpuesta intercambia filas por columnas **conservando el orden**: cada fila de $B$ se escribe como columna de $B^\top$.

| Fila de $B$ | Pasa a ser | Columna de $`B^\top`$ |
|-------------|------------|-----------------------|
| Fila 1: $(3,0,-2,1)$ | → | columna 1 |
| Fila 2: $(4,6,5,-1)$ | → | columna 2 |
| Fila 3: $(7,-3,8,2)$ | → | columna 3 |

```math
B^\top=\begin{bmatrix}3&4&7\\0&6&-3\\-2&5&8\\1&-1&2\end{bmatrix}
```

La dimensión se invierte: $B$ es $3\times4$ y $B^\top$ es $4\times3$. Control rápido: $`(B^\top)_{ij}=b_{ji}`$, por ejemplo $`(B^\top)_{32}=b_{23}=5`$ ✓.

Error común: transponer no es invertir el orden de los números de una fila. El orden de cada fila se conserva y solo cambia su orientación.

### d) ¿Es $C$ simétrica? ¿Qué es $`I_3`$?

**¿$C$ es simétrica?** Una matriz es simétrica si $C=C^\top$, es decir, si $`c_{ij}=c_{ji}`$ para todo par de posiciones.

1. Se transpone: $`C^\top=\begin{bmatrix}2&3\\1&2\end{bmatrix}`$.
2. Se comparan las entradas fuera de la diagonal: $`c_{12}=1`$ pero $`c_{21}=3`$.

Como $1\neq3$, se escribe $C\neq C^\top$ y **$C$ no es simétrica**.

**$`I_3`$:** es la matriz identidad de tamaño $3\times3$. El subíndice solo indica la dimensión: unos en la diagonal y ceros fuera.

```math
I_3=\begin{bmatrix}1&0&0\\0&1&0\\0&0&1\end{bmatrix}
```

En NumPy: `B.T` da la transpuesta y `B.shape` la dimensión.
