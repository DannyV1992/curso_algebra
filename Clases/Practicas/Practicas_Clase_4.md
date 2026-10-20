# Prácticas de la Clase 4 — Combinación lineal, generado y subespacios

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University\
**Fuente:** `Material del curso.pdf`, diapositivas 17–18 (práctica 4)\
**Resumen de la clase:** [Resumen_Clase_4.md](../Resumenes/Resumen_Clase_4.md)

Idea central: una **combinación lineal** multiplica cada vector por un peso y suma. Preguntar si $\mathbf{w}$ es combinación de unos vectores equivale a preguntar si $\mathbf{w}$ está en su **generado**, y se responde planteando un sistema con **una ecuación por componente**.

---

## Práctica 4

### a) Calcular $2(1,-1,0)+3(0,2,1)-(4,1,-2)$

Se conocen los pesos, así que solo hay que calcular.

1. **Pesos:** 2 para el primer vector, 3 para el segundo y $-1$ para el tercero (el signo menos delante equivale a multiplicar por $-1$).
2. **Escalar cada vector:**
   - $2(1,-1,0)=(2,\ -2,\ 0)$
   - $3(0,2,1)=(0,\ 6,\ 3)$
   - $-1\cdot(4,1,-2)=(-4,\ -1,\ 2)$
3. **Sumar posición por posición:**

```math
(2+0-4,\ \ -2+6-1,\ \ 0+3+2)=(-2,\ 3,\ 5)
```

**Resultado:** $(-2,3,5)$.

### b) Escribir $\mathbf{w}=(5,1)$ como combinación de $`\mathbf{v}_1=(1,1)`$ y $`\mathbf{v}_2=(1,-1)`$

Ahora se conoce el resultado y hay que **hallar los pesos** $`c_1`$ y $`c_2`$.

**Paso 1: la mezcla con letras.**

```math
c_1(1,1)+c_2(1,-1)=(5,1)
```

**Paso 2: multiplicar cada vector por su peso.**

- $`c_1(1,1)=(c_1,\ c_1)`$
- $`c_2(1,-1)=(c_2,\ -c_2)`$

**Paso 3: sumar posición por posición.** La mezcla queda $`(c_1+c_2,\ c_1-c_2)`$.

**Paso 4: igualar con $\mathbf{w}$.** Cada posición da una ecuación. El $`-c_2`$ de la segunda viene del $-1$ que tiene $`\mathbf{v}_2`$ en su segunda posición.

```math
\begin{cases}c_1+c_2=5\\ c_1-c_2=1\end{cases}
```

**Paso 5: resolver.** Como $`c_2`$ aparece con signos opuestos, conviene sumar las ecuaciones: se cancela $`c_2`$.

```math
\begin{aligned}
(c_1+c_2)+(c_1-c_2)&=5+1\\
2c_1&=6\\
c_1&=3
\end{aligned}
```

Se sustituye en la primera ecuación: $`3+c_2=5\Rightarrow c_2=2`$.

*Alternativa por sustitución:* de la primera, $`c_1=5-c_2`$; en la segunda queda $`(5-c_2)-c_2=1\Rightarrow 5-2c_2=1\Rightarrow c_2=2`$, y $`c_1=5-2=3`$. Da lo mismo.

**Paso 6: verificar.** $3(1,1)+2(1,-1)=(3,3)+(2,-2)=(5,1)$ ✓.

**Resultado:** $`\mathbf{w}=3\mathbf{v}_1+2\mathbf{v}_2`$. Como se halló una solución, $\mathbf{w}$ **sí** está en el generado de $`\mathbf{v}_1`$ y $`\mathbf{v}_2`$.

### c) ¿Están $(2,4,6)$ y $(1,2,4)$ en el generado de $(1,2,3)$?

Con **un solo vector** hay **un solo peso** $c$, pero una ecuación por cada posición. Se busca un $c$ que funcione en todas a la vez.

La mezcla es $c(1,2,3)=(c,\ 2c,\ 3c)$.

**Caso $(2,4,6)$:**

| Posición | Ecuación | Valor de $c$ |
|----------|----------|--------------|
| 1 | $c=2$ | $c=2$ |
| 2 | $2c=4$ | $c=2$ |
| 3 | $3c=6$ | $c=2$ |

Las tres piden el mismo $c=2$. **Sí está** en el generado: $2(1,2,3)=(2,4,6)$ ✓.

**Caso $(1,2,4)$:**

| Posición | Ecuación | Valor de $c$ |
|----------|----------|--------------|
| 1 | $c=1$ | $c=1$ |
| 2 | $2c=2$ | $c=1$ |
| 3 | $3c=4$ | $`c=\tfrac43`$ |

Las dos primeras piden $c=1$ y la tercera pide $`c=\tfrac43`$. Un mismo $c$ no puede valer dos cosas: el sistema es **inconsistente** y $(1,2,4)$ **no está** en el generado (no cae sobre la recta de $(1,2,3)$).

**Trampa de dimensiones:** un vector como $(2,4)$ no puede estar en el generado de vectores de $\mathbb{R}^3$, porque tiene otra dimensión.

### d) ¿Es $`S=\{(x,2x)\}`$ un subespacio de $\mathbb{R}^2$?

$S$ está formado por los vectores cuya segunda componente es el doble de la primera: es la recta $y=2x$. Hay que verificar las **tres condiciones**.

1. **Contiene al cero.** Con $x=0$ se obtiene $(0,\ 2\cdot0)=(0,0)\in S$ ✓.
2. **Cerrado bajo la suma.** Sean $(a,2a)$ y $(b,2b)$ dos elementos de $S$:

```math
(a,2a)+(b,2b)=(a+b,\ 2a+2b)=(a+b,\ 2(a+b))
```

   Tiene la forma $(x,2x)$ con $x=a+b$, luego está en $S$ ✓.
3. **Cerrado bajo el escalar.** Con $k$ cualquiera:

```math
k(a,2a)=(ka,\ 2ka)=(ka,\ 2(ka))
```

   Tiene la forma $(x,2x)$ con $x=ka$ ✓.

**Resultado:** cumple las tres condiciones, así que **sí es subespacio** de $\mathbb{R}^2$.

Observaciones:

- Para probar que algo **no** es subespacio basta un contraejemplo; para probar que sí lo es hay que verificar las tres condiciones en general, no con un caso numérico.
- Una recta que no pasa por el origen, como $y=2x+1$, nunca es subespacio: con $x=0$ da $(0,1)\neq(0,0)$, así que no contiene al cero.
