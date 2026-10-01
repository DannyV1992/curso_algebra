# Clase 3 — Operar con datos: vectores y matrices (parte 1: vectores)

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University
**Semana:** 2 (la clase anterior fue feriado y esta la reemplaza)
**PDF fuente:** `Clase 3.pdf` (53 diapositivas)
**Cobertura del PDF:** Parcial: diapositivas 1 a 14 de 53 (hasta «Práctica 3: verificar, despejar y demostrar»). No se saltó ninguna diapositiva del rango. El resto (combinación lineal, producto punto, matrices, regresión) queda para la siguiente clase; solo se anota la hoja de ruta al final.

**Contexto.** Primera clase de contenido. El objetivo es adquirir el lenguaje matemático (notación, símbolos, vocabulario de demostración) que se usará en Modelado matemático y en los cursos de IA. Al terminar el bloque de vectores se debe poder calcular a mano lo que NumPy hace en una línea.

---

## 1. Ruta de la clase (diapositiva 2)

| Bloque | Tema | Contenido |
|--------|------|-----------|
| 1 | Vectores | Definición, suma/resta/escalar, principios algebraicos, combinación lineal |
| 2 | Producto punto | Definición, ángulo y ortogonalidad, proyección ortogonal |
| 3 | Matrices | Definición, suma/escalar/transpuesta, matriz por vector, producto de matrices |
| 4 | Aplicación | Regresión como proyección, ecuaciones normales, laboratorio en NumPy |

Cada tema sigue el patrón **explicación → ejemplos resueltos → práctica → solución**. Cada bloque depende del anterior.

---

## 2. Vectores: qué es un vector, desde cero (diapositivas 3–6)

### Definición

Un vector es el objeto más básico del curso: una **lista ordenada de $n$ números reales** que representa una observación, una dirección o un conjunto de pesos.

$$\mathbf{v} = (v_1, v_2, \ldots, v_n) \in \mathbb{R}^n$$

La letra (aquí $\mathbf{v}$) nombra al vector y $\in \mathbb{R}^n$ indica a qué conjunto pertenecen sus valores. No se confunde con teoría de grupos: aquí se habla de conjuntos numéricos.

**Igualdad:**

$$\mathbf{u} = \mathbf{v} \iff u_i = v_i \quad \forall i$$

### Lo que hay que fijar

- **Ordenada:** el orden importa. $(3,2) \neq (2,3)$; p. ej., un crecimiento económico de $(3,2)$ no es el de $(2,3)$.
- **Componente:** cada número; $v_i$ es la componente en la posición $i$ y representa algo (una variable, una coordenada).
- **Dimensión $n$:** cantidad de componentes. $\mathbb{R}^n$ es el conjunto de todos los vectores con $n$ componentes reales.
- **Solo se comparan u operan vectores de la misma dimensión** (como en álgebra básica, donde solo se combinan términos semejantes).
- **Punto o flecha, fila o columna:** se interpreta como posición o como flecha desde el origen. Por convención se escribe como columna; su transpuesta $\mathbf{v}^T$ es la fila.
- **Vector cero:** $\mathbf{0} = (0,\ldots,0)$ es siempre el origen.
- **Tipo de dato:** casi siempre números reales (coordenadas, temperaturas, precios). Los complejos aparecen en ingeniería específica, p. ej. computación cuántica.
- **Dimensiones:** algebraicamente se puede trabajar con las dimensiones que se quiera, aunque el ser humano solo perciba hasta la tercera.

**Ejemplo.** La trayectoria de un vuelo Costa Rica–Madrid de 10 h, con la posición guardada cada hora, da una lista de 10 coordenadas: un vector en $\mathbb{R}^{10}$. Es vector cuando ya está la lista completa y ordenada.

### Igualdad: qué exige

- Misma dimensión **y** mismas componentes en el mismo orden. Tener la misma dimensión no basta.
- $(1,2,3)$ y $(3,4,5)$ comparten un valor (el 3) pero en posiciones distintas: no son iguales.
- "Dirección" aún no está definida formalmente (se verá con el producto punto); por ahora un vector es solo la lista de sus componentes.
- Una igualdad entre vectores de $\mathbb{R}^n$ equivale a **$n$ ecuaciones escalares**, una por componente. Sirve para hallar incógnitas dentro de un vector.

### Ejemplos resueltos (diapositiva 4)

**1. Leer dimensión y componentes.** Un cliente del dataset de la clase 1: $\mathbf{x} = (34, 12, 480, 5)$ (edad, visitas, gasto, días).
- Hay 4 componentes, luego $n = 4$ y $\mathbf{x} \in \mathbb{R}^4$ (así se demuestra que algo es de 4 dimensiones).
- Tercera posición: $x_3 = 480$.

**2. Igualdad con incógnitas.** Hallar $a$ y $b$ tales que $(a+1,\ 2b) = (4,\,-6)$.
- Se igualan posiciones: $a+1=4$ y $2b=-6$.
- Se resuelve cada ecuación por separado (restando/dividiendo a ambos lados): $a=3$, $b=-3$.
- Verificación: $(3+1,\ 2\cdot(-3)) = (4,-6)$.

> Matemática vs. programación: en matemáticas la primera posición es la 1 ($x_3$); en Python/NumPy el índice empieza en 0 (`x[2]`). Son lenguajes distintos y hay que manejar ambos.

### Práctica 1 (diapositivas 5–6) — soluciones

| Ejercicio | Planteamiento | Resultado |
|-----------|---------------|-----------|
| a | $\mathbf{v}=(-2,0,7,1,5)$: contar componentes | $n=5$, $\mathbf{v}\in\mathbb{R}^5$, $v_4=1$ |
| b | $(2a-1,\ b+3,\ c)=(5,0,-4)$ → $2a-1=5,\ b+3=0,\ c=-4$ | $(a,b,c)=(3,-3,-4)$ |
| c | Clienta de 29 años, ingreso 850 (miles), 6 compras, 14 meses: $\mathbf{x}=(29,850,6,14)$ con orden (edad, ingreso, compras, meses) | Dimensión 4, punto en $\mathbb{R}^4$ |
| d | $(1,2)$ vs $(2,1)$: misma dimensión, $u_1\neq v_1$. $(1,2)$ vs $(1,2,0)$: $\mathbb{R}^2$ vs $\mathbb{R}^3$ | Ninguno es igual |

- Para indicar dimensión se escribe $n=5$; para indicar el espacio, $\mathbf{v}\in\mathbb{R}^5$. El nombre del vector puede ser cualquier letra.
- Si cambia el orden de las variables, cambia el vector.
- **Antes de operar, preguntarse siempre: ¿qué dimensión tiene cada vector?**

---

## 3. Operaciones: sumar, restar y escalar (diapositivas 7–10)

Con solo dos operaciones, **suma** y **multiplicación por un escalar**, se construye todo el álgebra lineal del curso.

$$\mathbf{u} \pm \mathbf{v} = (u_1 \pm v_1,\ \ldots,\ u_n \pm v_n) \qquad k\,\mathbf{u} = (ku_1,\ \ldots,\ ku_n)$$

### Reglas

- **Se opera posición por posición.** La componente $i$ del resultado usa solo las componentes $i$ de los vectores; nunca se mezclan posiciones.
- Por eso ambos vectores deben tener la misma dimensión: una componente sin pareja quedaría "flotando" sin operarse. Sumar $(1,2)+(1,2,3)$ **no está definido** (NumPy lanza un error de forma, *shape mismatch*).
- **Orden de operaciones:** igual que en aritmética, primero los escalares y luego las sumas/restas.
- Escribir cada componente por separado evita la mayoría de errores de signo.

### Geometría

- $\mathbf{u}+\mathbf{v}$: poner una flecha tras otra; es la **diagonal del paralelogramo** formado por $\mathbf{u}$ y $\mathbf{v}$.
- $\mathbf{u}-\mathbf{v}$: la flecha que va de $\mathbf{v}$ hasta $\mathbf{u}$.
- **Escalar** por $k$: $k>1$ estira; $0<k<1$ encoge (equivale a dividir); $k<0$ invierte el sentido. La recta que contiene al vector no cambia.
- Solo se grafican vectores de $\mathbb{R}^2$ y $\mathbb{R}^3$ (eje $z$ como tercera dimensión). En más de 3 dimensiones no hay representación directa; se usan técnicas de reducción de dimensiones. En la práctica de IA se trabaja con decenas o cientos de dimensiones.

**Conexión con ML:** "escalar" variables (p. ej. `scaler` en scikit-learn) busca que magnitudes muy distintas (salario vs. ahorro) se parezcan, para que el modelo no dé más importancia a una variable solo por tener números más grandes.

### Ejemplos resueltos (diapositiva 8)

**1. Suma y resta en $\mathbb{R}^2$.** $\mathbf{u}=(3,1)$, $\mathbf{v}=(1,2)$:

$$\mathbf{u}+\mathbf{v}=(3+1,\ 1+2)=(4,3) \qquad \mathbf{u}-\mathbf{v}=(2,-1)$$

**2. Combinar operaciones en $\mathbb{R}^3$.** $\mathbf{u}=(2,-1,4)$, $\mathbf{v}=(1,3,0)$; calcular $3\mathbf{u}-2\mathbf{v}$:
- Escalar: $3\mathbf{u}=(6,-3,12)$ y $2\mathbf{v}=(2,6,0)$.
- Restar componente a componente: $(6-2,\ -3-6,\ 12-0)=(4,-9,12)$.
- El signo menos delante de $2\mathbf{v}$ pertenece a la resta: no cambia los signos de $\mathbf{v}$ antes de restar.

### Práctica 2 (diapositivas 9–10) — soluciones

Con $\mathbf{a}=(1,-2,3)$, $\mathbf{b}=(4,0,-1)$, $\mathbf{c}=(-2,5,2)$:

| Ejercicio | Resultado |
|-----------|-----------|
| a) $\mathbf{a}+\mathbf{b}$ y $\mathbf{b}-\mathbf{c}$ | $(5,-2,2)$ y $(6,-5,-3)$ |
| b) $-3\mathbf{a}$ y $2\mathbf{a}-\mathbf{b}+\mathbf{c}$ | $(-3,6,-9)$ y $(-4,1,9)$ |
| c) $\mathbf{x}+\mathbf{a}=\mathbf{b}$ | $\mathbf{x}=\mathbf{b}-\mathbf{a}=(3,2,-4)$ |
| d) $(1,2)+(1,2,3)$ | No se puede: dimensiones distintas |

Error frecuente: en $\mathbf{b}-\mathbf{c}$ el signo de $\mathbf{c}$ se distribuye, y restar un negativo suma ($4-(-2)=6$).

---

## 4. Principios algebraicos: las ocho reglas (diapositivas 11–14)

Los axiomas de espacio vectorial permiten manipular vectores igual que números: reordenar, agrupar, factorizar y despejar.

| # | Axioma | Expresión |
|---|--------|-----------|
| 1 | Conmutativa | $\mathbf{u}+\mathbf{v}=\mathbf{v}+\mathbf{u}$ |
| 2 | Asociativa | $(\mathbf{u}+\mathbf{v})+\mathbf{w}=\mathbf{u}+(\mathbf{v}+\mathbf{w})$ |
| 3 | Neutro (vector cero) | $\mathbf{u}+\mathbf{0}=\mathbf{u}$ |
| 4 | Opuesto | $\mathbf{u}+(-\mathbf{u})=\mathbf{0}$ |
| 5 | Distributiva sobre vectores | $k(\mathbf{u}+\mathbf{v})=k\mathbf{u}+k\mathbf{v}$ |
| 6 | Distributiva sobre escalares | $(k+m)\mathbf{u}=k\mathbf{u}+m\mathbf{u}$ |
| 7 | Asociativa de escalares | $k(m\mathbf{u})=(km)\mathbf{u}$ |
| 8 | Identidad | $1\,\mathbf{u}=\mathbf{u}$ |

**Fundamento.** Cada axioma se hereda de los números reales, porque se opera componente a componente y cada componente es un real. Ejemplo (conmutativa):

$$\mathbf{u}+\mathbf{v}=(u_1+v_1,\ldots,u_n+v_n)=(v_1+u_1,\ldots,v_n+u_n)=\mathbf{v}+\mathbf{u}$$

Un conjunto con suma y escalar que cumple los 8 axiomas es un **espacio vectorial**. $\mathbb{R}^n$ lo es, y también las matrices del mismo tamaño.

Reglas que se deducen de los axiomas: $0\cdot\mathbf{u}=\mathbf{0}$ y $(-1)\mathbf{u}=-\mathbf{u}$.

### Ejemplos resueltos (diapositiva 12)

**1. Verificar la distributiva.** $k=2$, $\mathbf{u}=(1,3)$, $\mathbf{v}=(4,-1)$; ¿$k(\mathbf{u}+\mathbf{v})=k\mathbf{u}+k\mathbf{v}$?
- Izquierda (sumar y luego escalar): $2(5,2)=(10,4)$.
- Derecha (escalar y luego sumar): $(2,6)+(8,-2)=(10,4)$.
- Coinciden: se cumple.

**2. Despejar un vector.** Resolver $3\mathbf{x}-\mathbf{u}=2\mathbf{v}$ con $\mathbf{u}=(3,0)$, $\mathbf{v}=(0,6)$. Cada paso lo autoriza un axioma:

| Paso | Justificación |
|------|---------------|
| $3\mathbf{x}-\mathbf{u}+\mathbf{u}=2\mathbf{v}+\mathbf{u}$ | sumar $\mathbf{u}$ a ambos lados (opuesto) |
| $3\mathbf{x}=2\mathbf{v}+\mathbf{u}$ | neutro |
| $\tfrac13(3\mathbf{x})=\tfrac13(2\mathbf{v}+\mathbf{u})$ | escalar por $\tfrac13$ |
| $\mathbf{x}=\tfrac13(3,12)=(1,4)$ | asociativa e identidad |

- Despejar vectores es idéntico a despejar números, salvo que **no existe la división entre un vector**: se escala por el inverso del escalar (dividir por 3 = multiplicar por $\tfrac13$).
- Nombrar el axioma de cada paso es lo que convierte un cálculo en una demostración.

### Práctica 3 (diapositivas 13–14): es la tarea

Una verificación numérica no demuestra un axioma; solo lo ilustra en un caso.

- **a)** Verificar $(k+m)\mathbf{u}=k\mathbf{u}+m\mathbf{u}$ con $k=3$, $m=-1$, $\mathbf{u}=(2,5,-1)$, calculando ambos lados por separado (ambos dan $(4,10,-2)$).
- **b)** Verificar la asociativa con $\mathbf{u}=(1,2)$, $\mathbf{v}=(-3,4)$, $\mathbf{w}=(0,-5)$ (ambos lados dan $(-2,1)$).
- **c)** Despejar $\mathbf{x}$ en $2\mathbf{x}+\mathbf{a}=5\mathbf{b}-\mathbf{x}$ con $\mathbf{a}=(3,-6)$, $\mathbf{b}=(1,0)$, nombrando el axioma de cada paso (resultado: $\mathbf{x}=(\tfrac23,2)$).
- **d)** Demostrar con solo los axiomas que $0\cdot\mathbf{u}=\mathbf{0}$. Pista: escribir $0=0+0$ y usar la distributiva sobre escalares:

$$0\mathbf{u}=(0+0)\mathbf{u}=0\mathbf{u}+0\mathbf{u}\ \Rightarrow\ \text{sumar el opuesto de }0\mathbf{u}\ \Rightarrow\ \mathbf{0}=0\mathbf{u}$$

Ejercicio adicional sugerido: probar $(-1)\mathbf{u}=-\mathbf{u}$ con la misma técnica.

---

## 5. Por qué importa: vectores y modelos de IA

- Los datos entran a los modelos como vectores y matrices; un científico de datos debe manejar este lenguaje.
- **Un registro es un vector.** Un cliente con (visitas, tiempo en el sitio, gasto) $=(10,50,150)$ es un punto/flecha de $\mathbb{R}^3$ desde el origen. Un modelo "ve" una trayectoria numérica, no "clientes" ni "dólares": los patrones que no se notan a simple vista en miles de datos quedan expuestos al convertirlos en vectores.
- **Redes neuronales:** una imagen son píxeles (una matriz); se procesa por partes (convolución, *pooling*) y al final se aplana (*flatten*) a un vector de una dimensión que alimenta la red. El descenso de gradiente busca el mínimo del error moviéndose en un espacio vectorial de pesos.
- **Modelos de lenguaje (transformers):** texto → *embeddings* → transformaciones matriciales. Lectura recomendada: *Attention Is All You Need*.
- La computadora solo lee números; el álgebra lineal es el puente entre el lenguaje humano y el de la máquina.
- Las reglas de esta clase son las mismas del álgebra de los reales, aplicadas a vectores: no hay "magia nueva".

---

## Conceptos clave

- **Vector:** lista ordenada de $n$ reales; $\mathbf{v}\in\mathbb{R}^n$; el orden importa.
- **Componente y dimensión:** $v_i$ es la componente $i$; $n$ es la dimensión. Solo se operan vectores de igual dimensión.
- **Igualdad:** misma dimensión y misma componente en cada posición; equivale a $n$ ecuaciones escalares.
- **Indexación:** matemáticas desde 1, Python desde 0.
- **Operaciones:** suma, resta y escalar, siempre componente a componente; primero escalares, luego sumas.
- **Escalar $k$:** $k>1$ estira, $0<k<1$ encoge, $k<0$ invierte el sentido.
- **Suma geométrica:** diagonal del paralelogramo; $\mathbf{u}-\mathbf{v}$ va de $\mathbf{v}$ a $\mathbf{u}$.
- **Ocho axiomas:** cuatro de la suma, cuatro del escalar; heredados de $\mathbb{R}$; definen un espacio vectorial.
- **Despejar:** sumar el opuesto, escalar por el inverso; nunca dividir entre un vector.
- **Demostrar:** justificar cada igualdad con el nombre de un axioma.

---

## Fuera del PDF — logística, tareas y metodología

- **Tarea (Entregable individual 1):** la práctica 3 (diapositiva 13), resuelta **a mano**, paso a paso y con el razonamiento, subida al campus como foto o documento. Se entrega antes de las 16:00 h de la próxima clase (en 8 días). La diapositiva queda publicada en el campus.
- **Uso de IA:** no usar IA de forma agresiva en estos ejercicios, especialmente en la demostración.
- **Asistencia:** 3 ausencias implican quedar fuera. Avisar por mensaje cuando se presente algún inconveniente (conexión, trabajo).
- **Material:** la presentación completa está en el campus; se prepara un documento resumen y videos de práctica adicionales.
- **Próxima clase:** combinación lineal, producto punto y el resto de la presentación, con el laboratorio en Python/NumPy (unas 2 a 2,5 clases en total hasta llegar a regresión lineal como proyección).
- **Asesorías:** disponibles bajo solicitud, con sesión agendada por mensaje directo.
