# Práctica 1 — Verificar, despejar y demostrar

## Axiomas usados

| # | Nombre | Enunciado |
|---|---|---|
| 1 | Conmutativa de la suma | $\mathbf{u}+\mathbf{v} = \mathbf{v}+\mathbf{u}$ |
| 2 | Asociativa de la suma | $(\mathbf{u}+\mathbf{v})+\mathbf{w} = \mathbf{u}+(\mathbf{v}+\mathbf{w})$ |
| 3 | Neutro aditivo | $\mathbf{u}+\mathbf{0} = \mathbf{u}$ |
| 4 | Opuesto | $\mathbf{u}+(-\mathbf{u}) = \mathbf{0}$ |
| 5 | Distributiva sobre vectores | $k(\mathbf{u}+\mathbf{v}) = k\mathbf{u}+k\mathbf{v}$ |
| 6 | Distributiva sobre escalares | $(k+m)\mathbf{u} = k\mathbf{u}+m\mathbf{u}$ |
| 7 | Asociativa de escalares | $k(m\mathbf{u}) = (km)\mathbf{u}$ |
| 8 | Identidad escalar | $1\mathbf{u} = \mathbf{u}$ |

---

## (a) Verificar $(k+m)\mathbf{u} = k\mathbf{u} + m\mathbf{u}$

**Datos:** $k = 3$, $m = -1$, $\mathbf{u} = (2,\,5,\,-1)$.

**Lado izquierdo** — primero el escalar, después el producto:

$$k+m = 3+(-1) = 2 \qquad\Longrightarrow\qquad (k+m)\mathbf{u} = 2\,(2,\,5,\,-1) = (4,\,10,\,-2)$$

**Lado derecho** — dos productos por escalar y una suma componente a componente:

$$k\mathbf{u} = 3\,(2,\,5,\,-1) = (6,\,15,\,-3) \qquad m\mathbf{u} = -1\,(2,\,5,\,-1) = (-2,\,-5,\,1)$$

$$k\mathbf{u} + m\mathbf{u} = (6-2,\ 15-5,\ -3+1) = (4,\,10,\,-2)$$

**Conclusión:** ambos lados dan $(4,\,10,\,-2)$, así que la igualdad se cumple en este caso.

---

## (b) Verificar la asociativa $(\mathbf{u}+\mathbf{v})+\mathbf{w} = \mathbf{u}+(\mathbf{v}+\mathbf{w})$

**Datos:** $\mathbf{u} = (1,\,2)$, $\mathbf{v} = (-3,\,4)$, $\mathbf{w} = (0,\,-5)$.

**Lado izquierdo** — se agrupa primero $\mathbf{u}+\mathbf{v}$:

$$\mathbf{u}+\mathbf{v} = (1-3,\ 2+4) = (-2,\,6) \qquad\Longrightarrow\qquad (\mathbf{u}+\mathbf{v})+\mathbf{w} = (-2+0,\ 6-5) = (-2,\,1)$$

**Lado derecho** — se agrupa primero $\mathbf{v}+\mathbf{w}$:

$$\mathbf{v}+\mathbf{w} = (-3+0,\ 4-5) = (-3,\,-1) \qquad\Longrightarrow\qquad \mathbf{u}+(\mathbf{v}+\mathbf{w}) = (1-3,\ 2-1) = (-2,\,1)$$

**Conclusión:** ambos agrupamientos dan $(-2,\,1)$: el paréntesis no cambia el resultado.

---

## (c) Despejar $\mathbf{x}$ en $2\mathbf{x} + \mathbf{a} = 5\mathbf{b} - \mathbf{x}$

**Datos:** $\mathbf{a} = (3,\,-6)$, $\mathbf{b} = (1,\,0)$.

**La idea:** se despeja igual que una ecuación numérica; las $\mathbf{x}$ a un lado, lo demás al otro, y al final se divide. La única diferencia es que se divide entre el **escalar** 3, nunca entre un vector.

Se despeja primero con letras y se sustituyen los números al final.

### Los tres pasos

Partimos de:

$$2\mathbf{x} + \mathbf{a} = 5\mathbf{b} - \mathbf{x}$$

**Paso 1 — sumar $\mathbf{x}$ a los dos lados.** A la izquierda, $2\mathbf{x}+\mathbf{x} = 3\mathbf{x}$:

$$3\mathbf{x} + \mathbf{a} = 5\mathbf{b}$$

**Paso 2 — sumar $-\mathbf{a}$ a los dos lados.** A la izquierda, $\mathbf{a}-\mathbf{a}$ se cancela:

$$3\mathbf{x} = 5\mathbf{b} - \mathbf{a}$$

**Paso 3 — multiplicar los dos lados por $\tfrac{1}{3}$.** A la izquierda, $3\mathbf{x}$ pasa a $\mathbf{x}$:

$$\boxed{\ \mathbf{x} = \tfrac{1}{3}\,(5\mathbf{b} - \mathbf{a})\ }$$


### Sustituir los datos

$$5\mathbf{b} = 5\,(1,\,0) = (5,\,0) \qquad -\mathbf{a} = (-3,\,6) \qquad 5\mathbf{b}-\mathbf{a} = (5-3,\ 0+6) = (2,\,6)$$

$$\mathbf{x} = \tfrac{1}{3}\,(2,\,6) = \left(\tfrac{2}{3},\ 2\right) \approx (0{,}667;\ 2)$$

### Comprobación

Se sustituye $\mathbf{x} = \left(\tfrac{2}{3},\,2\right)$ en la ecuación original y se calcula cada lado por separado:

$$2\mathbf{x} + \mathbf{a} = \left(\tfrac{4}{3},\,4\right) + (3,\,-6) = \left(\tfrac{4}{3}+3;\ \ 4-6\right) = \left(\tfrac{13}{3},\,-2\right)$$

$$5\mathbf{b} - \mathbf{x} = (5,\,0) - \left(\tfrac{2}{3},\,2\right) = \left(5-\tfrac{2}{3};\ \ 0-2\right) = \left(\tfrac{13}{3},\,-2\right)$$

**Conclusión:** ambos lados dan exactamente $\left(\tfrac{13}{3},\,-2\right)$, así que $\mathbf{x} = \left(\tfrac{2}{3},\,2\right)$ es la solución.