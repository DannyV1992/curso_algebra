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

**Paso 5: resolver el sistema.** Se numeran las ecuaciones: (1) $`c_1+c_2=5`$ y (2) $`c_1-c_2=1`$. Hay dos métodos y ambos dan lo mismo.

*Método 1: suma de ecuaciones.* Como $`c_2`$ aparece con signos opuestos ($`+c_2`$ y $`-c_2`$), al sumar las dos ecuaciones se cancela:

```math
\begin{aligned}
(c_1+c_2)+(c_1-c_2)&=5+1\\
2c_1&=6\\
c_1&=3
\end{aligned}
```

Se sustituye en la ecuación (1): $`3+c_2=5\Rightarrow c_2=2`$.

*Método 2: sustitución, paso a paso.* Se despeja una letra de una ecuación y se reemplaza en la **otra**, para que quede una sola incógnita.

1. **Despejar $`c_1`$ de la ecuación (1).** En $`c_1+c_2=5`$ se resta $`c_2`$ de ambos lados:

```math
c_1=5-c_2
```

   Ahora se sabe que $`c_1`$ vale "5 menos $`c_2`$". Todavía no es un número, porque $`c_2`$ no se conoce.

2. **Reemplazar en la ecuación (2).** En $`c_1-c_2=1`$ se cambia $`c_1`$ por $`(5-c_2)`$, entre paréntesis:

```math
(5-c_2)-c_2=1
```

   Se reemplaza en la otra ecuación, no en la misma: hacerlo en la misma deja una igualdad que siempre es cierta y no da información. Ahora la ecuación tiene una sola letra.

3. **Juntar los términos con $`c_2`$.** $`-c_2-c_2`$ son dos veces $`-c_2`$, o sea $`-2c_2`$:

```math
5-2c_2=1
```

4. **Restar 5 a ambos lados:**

```math
-2c_2=1-5\ \Rightarrow\ -2c_2=-4
```

5. **Dividir ambos lados entre $-2$:**

```math
c_2=\frac{-4}{-2}=2
```

6. **Volver a $`c_1`$.** Con $`c_2=2`$ se usa el despeje del paso 1:

```math
c_1=5-c_2=5-2=3
```

7. **Comprobar en las dos ecuaciones originales:** (1) $`3+2=5`$ ✓ y (2) $`3-2=1`$ ✓.

Ambos métodos dan $`c_1=3`$ y $`c_2=2`$. Se despeja primero $`c_1`$ porque no tiene número delante (su coeficiente es 1), lo que evita divisiones y fracciones.

**Paso 6: verificar.** $3(1,1)+2(1,-1)=(3,3)+(2,-2)=(5,1)$ ✓.

**Resultado:** $`\mathbf{w}=3\mathbf{v}_1+2\mathbf{v}_2`$. Como se halló una solución, $\mathbf{w}$ **sí** está en el generado de $`\mathbf{v}_1`$ y $`\mathbf{v}_2`$.

### c) ¿Están $(2,4,6)$ y $(1,2,4)$ en el generado de $(1,2,3)$?

**Qué se pregunta.** El generado de $(1,2,3)$ son todos los vectores que se obtienen multiplicando $(1,2,3)$ por algún número $c$; es decir, son sus múltiplos. La pregunta es: ¿existe un número $c$ tal que $c\cdot(1,2,3)$ dé exactamente $(2,4,6)$? ¿Y otro que dé $(1,2,4)$?

Es el mismo tipo de pregunta de la parte b), pero más simple: hay **un solo vector**, así que hay **un solo peso** ($c$ en lugar de $`c_1`$ y $`c_2`$).

#### Paso 1: escribir la mezcla con la letra $c$

Multiplicar un vector por $c$ es multiplicar cada una de sus posiciones por $c$:

```math
c\cdot(1,2,3)=(1\cdot c,\ 2\cdot c,\ 3\cdot c)=(c,\ 2c,\ 3c)
```

Esta es la "forma general" de cualquier vector del generado: la primera posición vale $c$, la segunda vale $2c$ y la tercera vale $3c$. Todo vector del generado tiene esa forma, y los que no la tienen no están en él.

#### Paso 2: comparar con el vector que se quiere obtener

Dos vectores son iguales solo si coinciden **en cada posición**. Por eso, al igualar $(c,\ 2c,\ 3c)$ con el vector objetivo, sale **una ecuación por posición**: 3 posiciones, 3 ecuaciones, y todas con la misma incógnita $c$.

#### Caso 1: el vector $(2,4,6)$

Se iguala $(c,\ 2c,\ 3c)=(2,4,6)$ posición por posición:

| Posición | Ecuación | Se despeja $c$ |
|----------|----------|----------------|
| 1 | $c=2$ | $c=2$ |
| 2 | $2c=4$ | se divide entre 2: $c=2$ |
| 3 | $3c=6$ | se divide entre 3: $c=2$ |

#### Paso 3: revisar si las tres ecuaciones están de acuerdo

Las tres piden el mismo valor, $c=2$. No hay contradicción, así que existe un peso que funciona en todas las posiciones.

#### Paso 4: verificar

$2\cdot(1,2,3)=(2,\ 4,\ 6)$ ✓.

**Conclusión:** $(2,4,6)$ **sí está** en el generado de $(1,2,3)$, con peso $c=2$.

#### Caso 2: el vector $(1,2,4)$

Se iguala $(c,\ 2c,\ 3c)=(1,2,4)$ posición por posición:

| Posición | Ecuación | Se despeja $c$ |
|----------|----------|----------------|
| 1 | $c=1$ | $c=1$ |
| 2 | $2c=2$ | se divide entre 2: $c=1$ |
| 3 | $3c=4$ | se divide entre 3: $`c=\tfrac43`$ |

#### Paso 3: revisar si las tres ecuaciones están de acuerdo

- Las posiciones 1 y 2 piden $c=1$.
- La posición 3 pide $`c=\tfrac43`$.

Un mismo número no puede valer $1$ y $`\tfrac43`$ a la vez. Las ecuaciones se contradicen: el sistema es **inconsistente**.

#### Paso 4: comprobar que de verdad falla

- Si se usa $c=1$ (lo que piden las dos primeras posiciones): $1\cdot(1,2,3)=(1,2,3)$. La tercera posición da $3$, pero se necesitaba $4$.
- Si se usa $`c=\tfrac43`$ (lo que pide la tercera): $`\tfrac43\cdot(1,2,3)=\left(\tfrac43,\ \tfrac83,\ 4\right)`$. La tercera posición ya da $4$, pero la primera da $`\tfrac43`$ y se necesitaba $1$.

Ningún $c$ acierta las tres posiciones a la vez.

**Conclusión:** $(1,2,4)$ **no está** en el generado de $(1,2,3)$. No se encuentra sobre la recta que forman los múltiplos de $(1,2,3)$.

#### Qué recordar de este ejercicio

- Con un solo vector no hay sistema que resolver con sustitución ni con suma: solo se despeja $c$ en **cada posición** y se comparan los resultados.
- **Todos iguales** → el vector sí está en el generado (y ese valor es el peso).
- **Alguno distinto** → el vector no está en el generado.

**Trampa de dimensiones:** un vector como $(2,4)$ no puede estar en el generado de $(1,2,3)$, porque los vectores del generado tienen 3 componentes y $(2,4)$ tiene 2.

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
