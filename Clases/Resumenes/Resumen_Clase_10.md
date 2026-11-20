# Clase 10 — Cómputo matricial eficiente: vectorización, matrices dispersas (CSR) y benchmarking

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University

**Semana:** 10

**Modalidad:** asincrónica (sin sesión en vivo ni transcripción de clase).

**Material fuente:** `5 - Cómputo matricial eficiente.pdf` (guía técnica, 23 páginas, fechada el 10 de noviembre de 2026), `5 - Guia computo eficiente.pdf` (guía base, 17 páginas) y dos videos de Dot CSV: «INTRO al Natural Language Processing (NLP) #1 — ¡De PALABRAS a VECTORES!» (11 min) y «#2 — ¿Qué es un EMBEDDING?» (15 min).

**Cobertura de los PDFs:** Completo (guía técnica, páginas 1 a 23; guía base, páginas 1 a 17). Sin transcripción de clase, el alcance es todo el material.

**Nota sobre las fuentes:** los videos se transcribieron aparte (el #2 con los subtítulos automáticos de YouTube y el #1 con Whisper, porque no tiene subtítulos). Las cifras de las guías se recalcularon y coinciden. Los tiempos en milisegundos dependen de la máquina: lo que se conserva es la **proporción** entre una forma de calcular y otra. Los ejercicios de práctica de las guías no se resuelven aquí.

**Contexto.** Se pasa de «qué hace una matriz» a «cómo calcularla rápido y con poca memoria» cuando los datos son grandes. Cuatro ideas encadenadas: **vectorizar** (sin ciclos `for`), distinguir matrices **densas** de **dispersas**, guardar las dispersas en **CSR** y **medir bien** (*benchmarking*). Todo corre en Google Colab con `numpy` y `scipy`. Los videos explican de dónde vienen los vectores de texto (*embeddings*) que usan los casos de IA.

---

## 0. Guía base: la matemática a mano

Lectura previa en 8 etapas con números pequeños y 10 ejercicios; con al menos 8 correctos se está listo para la guía técnica. Etapas: vectores y matrices, operar todo a la vez, producto punto/norma/coseno, matriz por vector, matriz por matriz, ceros y densidad, CSR, costo y precisión. Lo que no repite la guía técnica:

- **Coseno.** Con $\mathbf{u}=(3,4)$ y $\mathbf{v}=(4,3)$: $\mathbf{u}\cdot\mathbf{v}=24$, $`\|\mathbf{u}\|=\|\mathbf{v}\|=5`$ y $\cos\theta=24/25=0{,}96$. Compara **dirección, no tamaño**: $(3,4)$ y $(6,8)$ dan 1.
- **Vector unitario.** $(3,4)/5=(0{,}6;\ 0{,}8)$ tiene norma 1. Si todos los vectores ya tienen norma 1, el coseno es solo $\mathbf{x}\cdot\mathbf{q}$; por eso se normaliza **una sola vez**.
- **Matriz por vector, mirando los ceros.** $A\mathbf{x}$ se puede ver por filas (cada fila punto $\mathbf{x}$) o como combinación de las columnas con los pesos de $\mathbf{x}$. Con $`A=\begin{bmatrix}0&7&0&0\\2&0&0&3\\0&0&0&0\\0&0&4&0\end{bmatrix}`$ y $\mathbf{x}=(1,2,3,4)$ resulta $(14,14,0,12)$: de 16 productos, 12 son por cero. Eso justifica las matrices dispersas.
- **Errores:** $`r_{23}\neq r_{32}`$; el producto punto es un número; $(m\times n)(n\times p)=(m\times p)$ y $AB$ no es $BA$; `*` es entrada por entrada, `@` es producto de matrices.
- **En IA:** cada capa de una red calcula $W\mathbf{x}$; si las filas de $X$ tienen norma 1, $XX^T$ contiene todas las similitudes coseno a la vez.

---

## 1. Vectorizar: operar el arreglo completo

**Vectorizar** es reemplazar un ciclo `for` sobre elementos por una sola operación sobre el arreglo completo. Un producto punto de $10^6$ números baja de 35 ms a 0,64 ms.

- **Por qué:** cada vuelta de un ciclo de Python lee el índice, busca el tipo del número y crea un objeto nuevo. NumPy guarda los números juntos y ejecuta el ciclo en código compilado, con instrucciones que procesan varios números a la vez (SIMD).
- **Regla:** si se escribe un `for` que recorre un arreglo, casi siempre existe una versión vectorizada. No cambia el resultado, cambia **quién ejecuta el ciclo**.

| Quiero… | Con ciclo | Vectorizado |
|---------|-----------|-------------|
| Producto punto | `for i in range(n): s += a[i]*b[i]` | `a @ b` |
| Suma de cuadrados | `for v in x: s += v**2` | `(x**2).sum()` |
| Contar positivos | `for v in x: if v > 0: c += 1` | `(x > 0).sum()` |
| Longitud de un vector | raíz de un ciclo de cuadrados | `np.linalg.norm(x)` |

Producto punto con $n=10^6$: ciclo sobre el arreglo NumPy 133 ms (≈ 207 veces más lento que `a @ b`), ciclo sobre listas de Python 35 ms (≈ 55), `a @ b` 0,64 ms. El ciclo sobre el arreglo NumPy es el peor porque cada `a[i]` crea un objeto numérico: **no se mezclan ciclos de Python con arreglos de NumPy**.

**Máscaras** (contar y filtrar sin ciclo), con `x = np.array([3,-1,4,-1,5,-9])`:

```python
mask = x > 0              # [True False True False True False]
mask.sum()                # 3  (True cuenta como 1)
x[mask].mean()            # 4.0
```

**Ejes y *broadcasting*.** `axis` indica en qué dirección se resume: `A.sum(axis=0)` suma por columnas (colapsa las filas) y `axis=1` por filas. Para estandarizar cada columna:

```python
Z = (X - X.mean(axis=0)) / X.std(axis=0)   # (3,3) menos (3,) -> (3,3)
```

NumPy compara las formas de derecha a izquierda; dos dimensiones son compatibles si son iguales o una vale 1, así el vector de medias se repite en cada fila.

**Errores comunes:** `*` multiplica elemento a elemento (el producto matricial es `@`); sin `axis`, `sum` suma todo en un solo número; al dividir cada fila por su norma, usar `keepdims=True` para que la norma quede de forma $(m,1)$.

### Caso de IA: el texto más parecido

Un buscador semántico guarda cada documento como un *embedding* (aquí, 128 números) y devuelve los de mayor similitud coseno con la consulta $\mathbf{q}$:

```math
\cos\theta=\frac{\mathbf{x}\cdot\mathbf{q}}{\lVert\mathbf{x}\rVert\ \lVert\mathbf{q}\rVert}
```

Con 20 000 documentos, tiempo por consulta: ciclo 56 ms; vectorizado normalizando en cada consulta 6,6 ms (≈ 8 veces más rápido); con los embeddings **normalizados de antemano** (`Xn @ qn`) 0,83 ms (≈ 67). Las tres devuelven los mismos 5 documentos (`np.argsort(-scores)[:5]`). La tercera gana porque **separa lo que se hace una vez** (normalizar la matriz) **de lo que se hace en cada consulta** (una multiplicación matriz por vector).

---

## 2. Matrices densas y dispersas

Una matriz **densa** guarda las $m\times n$ entradas, ceros incluidos; una **dispersa** guarda solo los no ceros y dónde están. Una matriz de calificaciones de 10 000 usuarios × 5 000 películas con 0,5 % de datos baja de 400 MB a unos 3 MB.

- **nnz** = número de no ceros. **Densidad** = $\mathrm{nnz}/(mn)$: con 0,5 % hay 99,5 % de ceros.
- **Memoria** (un `float64` ocupa 8 bytes; en CSR cada no cero cuesta unos 12 bytes, 8 del valor y 4 de la columna, más 4 por fila):

```math
M_{\mathrm{densa}}=8mn\ \text{bytes},\qquad M_{\mathrm{CSR}}\approx 12\mathrm{nnz}+4(m+1)\ \text{bytes}
```

| Matriz | Densidad típica | ¿Conviene? |
|--------|-----------------|------------|
| Imagen en grises 28 × 28; embeddings de documentos | 100 % | Densa |
| Calificaciones usuario × película (10 000 × 5 000) | 0,5 % | Dispersa |
| TF-IDF, palabras por documento (50 000 × 20 000) | 0,2 % | Dispersa |
| Amistades en una red social (10⁶ × 10⁶) | 0,01 % | Dispersa |
| Matriz identidad $n\times n$ | $1/n$ | Dispersa |

**Estimar la memoria antes de crear la matriz** (100 000 × 100 000 con 10 no ceros por fila, nnz = $10^6$): densa = $10^{10}\cdot8$ = **80 GB** (no cabe en un computador normal); CSR = $10^6\cdot12+100\ 001\cdot4\approx$ **12,4 MB**; ahorro ≈ 6 450 veces. Con `sparse.random(10000, 5000, density=0.005, format='csr')` la memoria es `S.data.nbytes + S.indices.nbytes + S.indptr.nbytes` ≈ 3,04 MB. **Cuidado:** `S.toarray()` crea la versión densa completa y agota la memoria; solo para matrices pequeñas.

**¿Hasta qué densidad conviene?** Matriz por vector con una matriz de 2 000 × 2 000:

| Densidad | Densa (ms) | CSR (ms) | CSR más rápida | Memoria CSR (MB) |
|----------|-----------|----------|----------------|------------------|
| 0,1 % | 1,26 | 0,007 | ≈ 180 | 0,06 |
| 1 % | 1,21 | 0,033 | ≈ 37 | 0,49 |
| 10 % | 1,31 | 0,34 | ≈ 4 | 4,8 |
| 30 % | 1,31 | 1,00 | ≈ 1,3 | 14,4 |

La densa tarda lo mismo sin importar cuántos ceros tenga; la dispersa, en proporción a nnz. **Regla práctica:** considerar formato disperso con densidad menor que 10 % y confirmar midiendo, porque cerca de 30 % la ventaja casi desaparece. En **memoria** CSR deja de convenir cuando la densidad pasa de $2/3$ (se iguala $12d=8$), pero en **tiempo** pierde ventaja mucho antes.

### Caso de IA: matriz usuario × película

Un 0 significa «no calificó». Con 10 000 × 5 000 y 0,5 % de densidad: memoria 400 MB (densa) frente a 3,04 MB (CSR), ≈ 132 veces menos; `R @ v` tarda 29 ms frente a 0,24 ms, ≈ 124 veces más rápido. Dos lecciones:

1. El promedio por película se divide entre `R.getnnz(axis=0)` (votos reales); `R.mean()` o dividir entre 10 000 mezcla los ceros de «no calificó» con calificaciones reales.
2. A escala real (millones de usuarios) la versión densa ni siquiera se puede crear.

---

## 3. Formato CSR

**CSR** (*Compressed Sparse Row*) guarda una matriz dispersa en tres arreglos: `data` (los no ceros, fila por fila), `indices` (la columna de cada uno) e `indptr` (dónde empieza cada fila dentro de `data`).

```python
A = [[0,7,0,0],
     [2,0,0,3],
     [0,0,0,0],
     [0,0,4,0]]
data    = [7, 2, 3, 4]
indices = [1, 0, 3, 2]
indptr  = [0, 1, 3, 3, 4]
```

**Regla de lectura:** la fila $i$ son los elementos desde `indptr[i]` hasta `indptr[i+1]` (sin incluir este último). Fila 1: posiciones 1:3, `data=[2,3]` en las columnas `[0,3]`, es decir $(2,0,0,3)$; fila 2: 3:3, vacía.

- `data` e `indices` tienen nnz elementos; `indptr` tiene $m+1$ y su último valor es nnz. Los no ceros de la fila $i$ son `indptr[i+1] - indptr[i]`.
- **Construir `indptr` a mano:** contar los no ceros por fila (1, 2, 0, 1) y hacer la **suma acumulada empezando en 0**: 0, 1, 3, 3, 4.
- Las listas solas **no dicen cuántas columnas** tiene la matriz: `shape` se guarda aparte. `indices` son columnas e `indptr` habla de filas: no confundirlos.

| Formato | Se usa para | Punto débil |
|---------|-------------|-------------|
| COO | Construir a partir de ternas (fila, columna, valor) | Lento para operar |
| CSR | Sacar filas y multiplicar `A @ x` | Cambiar su estructura es costoso |
| CSC | Sacar columnas | Lo mismo que CSR |
| LIL | Editar entradas una a una | Lento para cálculos grandes |

- **Construir desde ternas (COO) y convertir**, lo natural al leer datos de un archivo: `sparse.coo_matrix((vals, (filas, cols)), shape=(4,4)).tocsr()`. Si una misma posición aparece dos veces, al convertir a CSR los valores se **suman**. Desde los tres arreglos: `sparse.csr_matrix((data, indices, indptr), shape=(3,4))`.
- **Multiplicar con solo los no ceros:** $A\mathbf{x}$ con $\mathbf{x}=(1,2,3,4)$ hace 4 multiplicaciones en lugar de 16. El costo pasa de $2mn$ a $2\mathrm{nnz}$.

### Caso de IA: TF-IDF y similitud entre documentos

Cada documento es un vector con una columna por palabra del vocabulario. El peso **TF-IDF** es alto cuando una palabra aparece mucho en el documento y es rara en el resto. Como cada documento usa pocas de las miles de palabras posibles, la matriz es dispersa y scikit-learn la entrega ya en CSR (`TfidfVectorizer`).

- Cada fila de `X` viene con norma 1, así que `X @ X.T` entrega la **similitud coseno entre todos los pares** sin salir del formato disperso. Para buscar, la consulta se transforma con el mismo vocabulario y se multiplica `X @ q.T`.
- En el ejemplo de 5 documentos y 18 palabras la densidad es 28/90 ≈ 31 %; con un corpus real de 50 000 × 20 000 cae a ≈ 0,2 %: 8 GB si fuera densa frente a unos 24 MB en CSR.

---

## 4. Benchmarking

**Benchmarking** es medir cuánto tarda y cuánta memoria usa un código, de forma confiable y comparable. Sin medir, «este código es más rápido» es solo una opinión. Cinco reglas:

| Regla | Por qué |
|-------|---------|
| **Calentar** (una o dos corridas sin medir) | La primera ejecución puede cargar librerías, llenar cachés y despertar hilos |
| **Repetir** 5 a 20 veces | Una sola medición se ve afectada por lo que haga el computador en ese instante |
| Reportar la **mediana**, no el promedio | Un valor atípico arrastra al promedio y casi no mueve a la mediana |
| Usar `time.perf_counter()` | Reloj de mayor resolución para intervalos |
| Mismos datos y **verificar que el resultado coincida** | Un código rápido pero incorrecto no sirve |

Ejemplo: con $[1{,}0;\ 1{,}1;\ 0{,}9;\ 1{,}0;\ 9{,}0]$ ms el promedio es 2,6 ms (no representa a ninguna medición típica) y la mediana es 1,0 ms.

```python
def bench(f, repeticiones=7, calentamiento=2):
    for _ in range(calentamiento): f()                # se descarta
    tiempos = []
    for _ in range(repeticiones):
        t0 = time.perf_counter(); f()
        tiempos.append(time.perf_counter() - t0)
    return st.median(tiempos) * 1e3                   # mediana en ms
```

Se usa con `bench(lambda: A @ B)`; para fragmentos cortos, `timeit.repeat` hace lo mismo.

**Predecir el costo contando operaciones de punto flotante (flops):**

| Operación | Flops | Si $n$ se duplica, el costo se multiplica por |
|-----------|-------|-----------------------------------------------|
| Producto punto de dos vectores de $n$ | $2n$ | 2 |
| Matriz × vector, $n\times n$ | $2n^2$ | 4 |
| Matriz × matriz, $n\times n$ | $2n^3$ | 8 |

De dónde salen: la matriz por vector son $n$ productos punto de $2n$; la matriz por matriz son $n^2$ entradas de $2n$ cada una. Regla de tres: si $n=1\ 000$ tarda 24 ms, con $n=2\ 000$ se espera $8\cdot24=192$ ms; con $n=4\ 000$, $64\cdot24\approx1{,}5$ s. **La teoría da el orden de magnitud y la medición el valor real:** al duplicar $n$ el factor medido fue 6,4; 6,5 y 10,8 (no 8), porque las matrices pequeñas caben en la memoria caché y las grandes no.

- **Ciclos de Python frente a una sola operación** (100 × 100): tres ciclos anidados 31,0 ms frente a 0,023 ms con `A @ B`, unas **1 350 veces más rápido**; la diferencia crece con $n$.
- **Precisión como decisión de rendimiento:** `float32` ocupa la mitad de memoria que `float64` y suele ser más rápido, pero su error relativo de redondeo es de $1{,}2\cdot10^{-7}$ frente a $2{,}2\cdot10^{-16}$. Con 1 500 × 1 500: memoria 18 MB → 9 MB, tiempo 131 ms → 51 ms (×2,6), error máximo $1{,}4\cdot10^{-4}$. Aceptable para entrenar o buscar vecinos; **no** para resolver un sistema mal condicionado.

### Caso de IA: el vecino más cercano de un *embedding*

Los buscadores semánticos y los sistemas RAG guardan cada documento como vector y, para cada pregunta, buscan los más parecidos. Con 20 000 documentos de 128 dimensiones, verificados con `np.allclose`:

| Versión | Tiempo (mediana) | Veces más rápido que el ciclo |
|---------|------------------|-------------------------------|
| `ciclo` | 74,6 ms | 1 |
| `vectorizado` | 3,7 ms | ≈ 20 |
| `prenormalizado` | 0,77 ms | ≈ 97 |
| `prenorm_f32` | 0,44 ms | ≈ 170 |

Vectorizar da un factor 20; **sacar de la búsqueda lo que no cambia** (las normas) da cinco veces más; `float32` agrega otro 1,7 sin cambiar los resultados en la práctica. Con 1 000 consultas por segundo, `ciclo` necesita unos 75 núcleos y `prenorm_f32` menos de 1.

---

## 5. Proyecto integrador: un recomendador con matrices dispersas

Junta los cuatro temas y es el principio con que las plataformas de películas, música o compras sugieren «algo parecido a lo que ya le gustó». Hay 5 000 usuarios y 2 000 películas; cada usuario calificó de 1 a 5 entre 15 y 39 películas. La matriz $R$ (usuarios × películas) tiene 135 304 valores de $10^7$ posiciones: densidad 1,35 %.

1. **Construir $R$ en CSR** desde ternas (usuario, película, calificación) con COO y `.tocsr()`. Memoria: 1,64 MB frente a 80 MB si fuera densa (≈ 49 veces menos).
2. **Similitud entre películas.** Dos películas son parecidas si las mismas personas las calificaron de forma parecida: cada columna de $R$ es su «huella». Se normalizan las columnas (`Rn = R @ sparse.diags(1/norma)`) y `S = (Rn.T @ Rn).tocsr()` da el coseno entre todas ($2\ 000\times2\ 000$). **El producto de dos dispersas puede llenarse:** $R$ tiene 1,35 % de densidad y $S$ tiene 39,8 %, porque casi todo par de películas comparte alguna persona. Hay que revisar `S.nnz` y verificar contra la versión densa con `np.allclose`.
3. **Recomendar a un usuario:** puntuación = suma de las similitudes con las películas que ya calificó, ponderada por esas calificaciones (`R[u] @ S`). Se descartan las ya vistas (`puntos[R[u].indices] = -1`) y se toman las 5 mejores con `np.argsort(-puntos)[:5]`.
4. **Medir** `Rn.T @ Rn`: densa 80 MB y 338 ms; dispersa 1,64 MB y 50 ms (≈ 49 veces menos memoria, ≈ 6,7 veces más rápida). La ventaja de tiempo es menor que en el Tema 2 porque aquí el producto se llena, el caso en que lo disperso pierde fuerza. Con 500 000 usuarios y 50 000 películas la densa ocuparía 200 GB y no cabría en ningún computador.
5. **¿Funciona?** Un sistema se juzga contra una **línea base** simple: recomendar las 5 más populares no vistas (`R.getnnz(axis=0)`). Fracción de recomendaciones del género favorito (200 usuarios): populares 0,11; similitud entre películas 1,00. **Advertencia:** los datos son **sintéticos** (cada usuario califica el 80 % de sus películas en su género favorito), por eso el resultado es tan limpio; con datos reales es menor. Se conserva el método y la comparación con una línea base.

**Entregable:** (1) código que genere o cargue $R$ en CSR e imprima `shape`, `nnz` y densidad; (2) la matriz $S$ y su verificación contra la versión densa; (3) recomendaciones para tres usuarios, con una frase que explique por qué tienen sentido; (4) tabla de memoria y tiempo (dispersa frente a densa) medida con `bench`; (5) conclusión de media página: ¿cuándo conviene y cuándo no usar CSR en este problema, mirando la densidad de $R$ y de $S$?

---

## 6. Videos de apoyo: de las palabras a los *embeddings*

Explican de dónde salen los vectores de texto de los casos de IA.

### Video 1 — De palabras a vectores

- **Texto → números.** Una red neuronal solo procesa números: una imagen es una matriz de intensidades, el audio ya está digitalizado y las categorías se codifican; el texto también necesita una representación numérica. Codificar a mano las reglas gramaticales no es viable (el lenguaje cambia y tiene demasiados matices), por eso el NLP actual aprende las reglas de grandes corpus con *machine learning*.
- **Tokenización.** El texto se divide en bloques llamados ***tokens***: palabras, caracteres o subpalabras (GPT-2 y GPT-3 usan subpalabras). Con palabras es más fácil generar texto realista; con caracteres el modelo puede incluso generar palabras que no existen.
- **Una etiqueta numérica por palabra es mala idea:** la red creería que hay orden y magnitud (que «pangolín» es el doble de «teléfono», o que «tostadora» está a medio camino entre ambos), como pasa con la edad en una tabla.
- **One-hot encoding.** Cada palabra es un vector con tantas posiciones como palabras tiene el vocabulario, todo en 0 salvo un 1 en la posición de esa palabra. Cada palabra ocupa **su propia dimensión**, así que todas quedan a la misma distancia y se elimina el falso orden.
- **Dos desventajas.** (1) Gasto enorme: una frase de 20 palabras con un vocabulario de 1 000 es una matriz de 20 × 1 000 casi toda de ceros (el caso de las matrices dispersas del Tema 2). (2) Asume que todas las palabras son equidistantes, pero «teléfono» y «tostadora» están conceptualmente más cerca entre sí que de «pangolín». La solución es el *embedding*.

### Video 2 — ¿Qué es un *embedding*?

- **Reducir dimensionalidad.** Ordenar rostros según dos atributos (p. ej. edad y color de piel) convierte miles de píxeles en solo 2 dimensiones. Una red neuronal hace algo equivalente: cada capa comprime los datos (un vector de tamaño 10 que pasa por una capa de 3 neuronas queda de tamaño 3).
- **Definición.** Con un vocabulario de 10 000 palabras, los vectores one-hot son de tamaño 10 000; si la primera capa tiene 300 neuronas, cada palabra queda como un vector de tamaño 300. Ese aprendizaje de la primera capa es el ***embedding***: una codificación compacta que la red **aprende para resolver su tarea** (p. ej. acercar palabras de sentimiento similar si se clasifican opiniones). Al inicio es mala y mejora con el entrenamiento. Multiplicar la matriz de pesos por un vector one-hot equivale a seleccionar una de sus columnas ($A\mathbf{x}$ como combinación de columnas, Etapa 4 de la guía base).
- **Preentrenados y transferencia de aprendizaje.** Partir de un modelo con conocimiento previo rinde más que partir de cero (igual que una red preentrenada en visión sirve para imágenes médicas). **Word2Vec** (Google, 2013) pasa vectores de un vocabulario de 10 000 a vectores de 300. Para que sea universal hacen falta **mucho texto** y **una tarea genérica** que no condicione la estructura aprendida.
- **Estructura aprendida sin supervisión**, solo por el contexto de cada palabra: al proyectar los vectores de 300 a 3 dimensiones aparecen grupos de números, de meses del año, de palabras con la misma raíz y de campos semánticos (*cats*, *dogs*, *birds*). Una palabra ambigua como *python* tiene vecinos de informática y de Monty Python.
- **Más allá del texto:** sirve para genes, jugadas de ajedrez y cualquier variable categórica que venga como vector one-hot. Además permite «aritmética» entre palabras (rey − hombre + mujer ≈ reina), que se retoma en el video siguiente de la serie.

---

## Conceptos clave

- **Vectorizar:** una operación sobre todo el arreglo en lugar de un ciclo `for`; el resultado no cambia, sí el tiempo. `@` es producto matricial y `*` elemento a elemento; `axis` marca la dirección del resumen y *broadcasting* repite el vector en cada fila.
- **Coseno:** compara dirección; con filas de norma 1 es solo el producto punto. **Separar lo que se hace una vez de lo que se hace por consulta** (normalizar de antemano).
- **Densidad = nnz / (m·n).** Densa: $8mn$ bytes; CSR: $\approx12\mathrm{nnz}+4(m+1)$. Dispersa conviene con densidad menor que ≈ 10 %; el costo del producto pasa de $2mn$ a $2\mathrm{nnz}$.
- **CSR:** `data`, `indices`, `indptr` (fila $i$ = posiciones `indptr[i]` hasta `indptr[i+1]`; $m+1$ valores, termina en nnz). COO para construir, CSR para filas y `A @ x`, CSC para columnas, LIL para editar.
- **El producto de dos dispersas puede llenarse:** revisar `S.nnz`; no usar `.toarray()` en matrices grandes.
- **Benchmarking:** calentar, repetir, reportar la **mediana**, `time.perf_counter()` y verificar el resultado (`np.allclose`).
- **Flops:** $2n$, $2n^2$, $2n^3$ (al duplicar $n$: ×2, ×4, ×8). La teoría da el orden de magnitud; la medición, el valor real.
- **`float32`:** mitad de memoria y más rápido, con error relativo ≈ $10^{-7}$; sirve para entrenar o buscar, no para sistemas mal condicionados.
- **Datos sintéticos:** decir de dónde vienen y comparar contra una **línea base**.
- **One-hot** (grande, disperso, equidistante) frente a ***embedding*** (compacto, aprendido, palabras parecidas cerca); los preentrenados como Word2Vec se reutilizan por transferencia de aprendizaje.

---

## Fuera del PDF — logística, tareas y metodología

- **Sesión asincrónica:** el material de la semana son las dos guías y los dos videos. No se dispone de instrucciones de entrega ni de fechas; el único entregable descrito es el del proyecto integrador (sección 5).
- **Ruta de estudio de las guías:** primero la guía base (lápiz y papel, 10 ejercicios, mínimo 8 correctos) y luego la guía técnica con código en Colab.
- **Pendiente de la clase 9:** este material corresponde al bloque 2 anunciado entonces (vectorización, matrices dispersas y *benchmarking*). Las diapositivas sobre sobredeterminados y colinealidad de `4 - Matrices en accion.pdf` no aparecen en estos archivos.
