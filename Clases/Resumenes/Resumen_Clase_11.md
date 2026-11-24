# Clase 11 — Matrices en la IA: repaso computacional y visión por computadora

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University

**Semana:** 11

**Material fuente:** transcripción de la sesión (2 h 15 min); la herramienta HTML interactiva `6 - Matrices_que_ven.html` (17 capítulos, en `Clases/PDFs/`), que guió la sesión y sigue la guía base `5 - Guia computo eficiente.pdf` (resumida en [Resumen_Clase_10.md](Resumen_Clase_10.md)); y el cuaderno `6 - Actividad_en_clase.ipynb` (caso de dígitos escritos a mano en Python).

**Cobertura del PDF:** Parcial: capítulos 1 a 15 de 17 de la herramienta (hasta «El recorrido completo: una mini red convolucional»). El capítulo 7 (costo y memoria) solo se mencionó de pasada; lo que se anota de él sale de la herramienta. No se vieron el capítulo 16 («A escala real: fotos, filtros y lotes») ni el 17 («Resumen y lo que sigue»): quedan para estudio individual. El cuaderno no se menciona en la transcripción; se resume al final como complemento de los capítulos 8 a 15.

**Nota sobre las fuentes:** la transcripción es automática y tiene cifras y términos mal reconocidos (p. ej. «Ford» por for, «Flatenin» por flatten, «96 picosegundos» por 96 µs); se corrigieron con la herramienta. Una frase dice que dos palabras más parecidas tienen un coseno «más reducido»; es al revés: **más parecidas = coseno más cercano a 1**, y así se anota aquí. Las secciones siguen los capítulos de la herramienta (1 a 7: bases; 8 a 15: visión por computadora).

**Contexto.** Sesión de repaso con enfoque computacional para ver «la matemática retratada»: los vectores, el producto punto y la multiplicación de matrices son lo que hay detrás de los buscadores, las redes neuronales, la visión por computadora y los LLM. Los documentos de la semana anterior resultaron densos, así que la herramienta recorre la guía base de forma visual, con animaciones y preguntas rápidas (cada capítulo trae además un bloque de código en Python). La clase de ecuaciones diferenciales empieza la semana siguiente.

---

## 1. Vectores: listas con orden

- Un **vector** es una lista **ordenada** de números; el orden importa: $`(3,-1,4)\neq(-1,3,4)`$. Cada posición significa algo (en una casa: metros cuadrados, cuartos, baños, años de construida), igual que el orden de las letras: «hola» no es «aloh».
- Con 2 entradas se ve como una **flecha** desde el origen; su longitud sale de Pitágoras: $`\|\mathbf{v}\|=\sqrt{x^2+y^2}`$.
- **Suma:** entrada por entrada, $(2,1)+(1,3)=(3,4)$ (en el dibujo, flechas encadenadas). **Producto por un escalar $k$:** $`3\cdot(2,1)=(6,3)`$; con $`k>1`$ estira, con $`0<k<1`$ encoge, con $`k<0`$ da la vuelta y con $k=0$ da el vector cero.
- **Los vectores toman decisiones.** Un vector de entradas de una cámara de vehículo puede activar el freno si cruza un umbral; la suma de vectores de señales (palabras clave de enojo, tono) puede alertar a un asistente de un centro de llamadas.
- **La IA empieza convirtiendo todo en vectores:** una palabra es un vector de cientos de números (un *embedding*), una imagen se aplana en un vector, un cliente es (edad, ingreso, compras).

**Texto vectorizado y *embeddings*.** Vectorizar un texto es convertirlo en números consultables. Cuando un documento se «indexa» en una herramienta de IA empresarial, se parte en miles de fragmentos y cada uno se guarda como vector; luego el modelo consume esos vectores y **predice la siguiente palabra** según probabilidades. Matemáticamente no «lee»: opera con números.

---

## 2. Matrices: tablas de números

- Una matriz es una tabla de tamaño $`m\times n`$, **filas primero**. Ejemplo de la herramienta: una matriz $R$ de $`3\times4`$ con las estrellas que cada usuario (fila) dio a cada película (columna); un 0 es «sin calificar».
- La entrada $`a_{ij}`$ es la de la fila $i$ y la columna $j$; $`r_{23}`$ no es $`r_{32}`$. Cada valor debe poder ubicarse al 100 %, y eso es lo que hace tan manejable la matriz para una computadora.
- Una matriz son **filas apiladas** (vectores fila) o **columnas lado a lado** (vectores columna); esa doble mirada es la que se usa al multiplicar. Por eso es fácil pasar de matrices a vectores en una red neuronal.
- La **transpuesta** voltea la matriz: la fila $i$ pasa a ser la columna $i$. Una matriz de $`5\times7`$ tiene una transpuesta de $`7\times5`$.
- Las matrices son la estructura de las imágenes, las bases de datos y los **pesos de las redes neuronales**.
- **Matrices dispersas:** en muchos problemas casi todo son ceros (cada usuario califica pocas películas de miles; cada documento usa pocas palabras del diccionario). Se guardan solo las entradas distintas de cero.

---

## 3. Vectorizar: operar todo a la vez

- **Vectorizar** es escribir una sola operación para todo el arreglo en lugar de recorrerlo número por número con un ciclo. Es la forma natural de pensar en matrices y lo que vuelve rápido el cómputo en NumPy y en las redes neuronales: el resultado es el mismo, cambia quién ejecuta el ciclo (código compilado y optimizado, sin pasar cada vez por el intérprete de Python). Es como en estructuras de datos: dos algoritmos dan el mismo resultado y uno es mucho más eficiente.
- **Una operación para todo el vector:** la suma de cuadrados de $(3,-1,4,-1,5,-9)$ es $133$ y se escribe sin ciclo. Es parecido a aplicar una función a toda una lista.
- **Máscaras:** `x > 0` devuelve 1 donde se cumple y 0 donde no; sumar la máscara cuenta los positivos (3) y `x[x > 0]` trae solo esos valores, $(3,4,5)$. Es el mismo concepto de la máscara en Photoshop: una matriz encima que dice qué se quiere y qué no.
- **Centrar los datos** (restar a cada columna su media): el vector de medias se repite en cada fila (*broadcasting*) y se resta; `axis=0` es una operación por columna.

```python
(x**2).sum()           # suma de cuadrados, sin ciclo
X - X.mean(axis=0)     # restar la media de cada columna
```

- **Tiempos** de un producto punto (herramienta, mismas proporciones que en la clase 10): ciclo sobre un arreglo NumPy ≈ 133 ns por entrada, ciclo sobre listas de Python ≈ 35 ns, vectorizado ≈ 0,64 ns. Con $10^7$ números: 1,33 s, 350 ms y 6,4 ms. Los valores cambian con la máquina; la proporción (cientos de veces) se mantiene.
- **Complejidad.** Medir cuánto cuesta resolver un problema es central; ejemplo de fondo: el problema **P vs NP**. P son los problemas que una computadora resuelve rápido (ordenar números, buscar un archivo); NP son aquellos en los que una solución propuesta se puede **verificar** rápido.

---

## 4. Producto punto, norma y coseno

- El **producto punto** convierte dos vectores en **un solo número**: se multiplica posición por posición y se suma. Ejemplo: $`(1,2,3)\cdot(4,0,-1)=4+0-3=1`$.
- **Signo y ángulo:** $`\mathbf{u}\cdot\mathbf{v}=\|\mathbf{u}\|\ \|\mathbf{v}\|\cos\theta`$. Ángulo agudo, producto punto positivo (apuntan hacia el mismo lado); 90°, producto punto 0; obtuso, negativo. **Si el producto punto de dos vectores no nulos es cero, son ortogonales.**
- **Norma** (longitud): $`\|\mathbf{u}\|=\sqrt{\mathbf{u}\cdot\mathbf{u}}`$; con $`\|(3,4)\|=\sqrt{25}=5`$. La distancia es la norma de la diferencia: entre $(3,4)$ y $(4,3)$ es $`\sqrt2\approx1{,}414`$.
- **Coseno:** mide qué tan parecidos son dos vectores (1 = misma dirección, 0 = perpendiculares, −1 = opuestos). Compara dirección, no tamaño. Es la medida con que los buscadores comparan textos e imágenes. Si los vectores se dividen entre su norma (longitud 1), el coseno es solo su producto punto; por eso se normaliza una vez al inicio.

```math
\cos\theta=\frac{\mathbf{u}\cdot\mathbf{v}}{\|\mathbf{u}\|\ \|\mathbf{v}\|}
```

- **Búsqueda por imagen** (tipo Google Lens): la imagen se **vectoriza** y se compara con las demás por producto punto y coseno; las de mayor parecido (incluso en ropa, postura o fondo) salen primero. Una imagen pixelada igual encuentra coincidencias.
- **Palabras parecidas.** En un buscador semántico cada palabra es un vector y se compara con el coseno: «gato» y «perro» salen casi iguales (≈ 0,97) y «modelo» y «gato» salen 0; la diagonal es 1. Pero la misma palabra cambia de sentido según el contexto («¿qué me dice, perrito?» es un saludo, no un animal), y con solo el coseno el modelo se confundiría. Los modelos grandes lo resuelven **alimentándose de contexto** y de datos etiquetados por personas (vectores auxiliares que corrigen cuándo dos palabras parecidas en realidad están lejos). Todo eso apunta a una IA más **general**, que responda cualquier cosa y no una sola variable.

---

## 5. Matriz por vector

- **Por filas:** cada entrada de $`A\mathbf{x}`$ es el producto punto de una fila de $A$ con $`\mathbf{x}`$; el resultado tiene tantas entradas como filas tenga $A$. **Por columnas:** $`A\mathbf{x}`$ es una **combinación de las columnas** de $A$ con las entradas de $`\mathbf{x}`$ como pesos. Conviene dominar las dos; la segunda explica por qué una matriz «mezcla» sus columnas y es la base de la transformación lineal y del rango.
- **Regla de tamaños:** $`(m\times n)(n\times1)=(m\times1)`$; el número de columnas de $A$ debe ser igual al número de entradas de $`\mathbf{x}`$. Una matriz $`3\times3`$ con un vector de 3 sí; con uno de 2, no; una $`2\times4`$ con un vector de 4 sí; una $`3\times5`$ con un vector de 4, no.
- **Transformaciones** (clase 9): identidad, estirar, girar, reflejar e inclinar. Las columnas de una matriz $`2\times2`$ dicen adónde caen los vectores básicos $(1,0)$ y $(0,1)$; todo lo demás se arma combinándolos. Por eso una IA puede «leer» una matriz como una imagen.
- **Una capa de red neuronal es una matriz por vector.** La entrada $`\mathbf{x}`$ (por ejemplo 3 píxeles) se multiplica por la matriz de pesos $W$ y se suma el vector de sesgos $`\mathbf{b}`$: $`W\mathbf{x}+\mathbf{b}`$. Cada fila de $W$ es una neurona (con $W$ de $`2\times3`$ hay dos neuronas de tres pesos cada una) y todas se calculan con **una sola multiplicación**. **Entrenar** es encontrar los pesos y sesgos que funcionan mejor, mediante el descenso del gradiente (se verá en ecuaciones diferenciales).

---

## 6. Matriz por matriz

- Cada entrada del resultado es el **producto punto de una fila de la primera con una columna de la segunda**. Mirada alternativa: cada columna de $C=AB$ es $A$ por la columna correspondiente de $B$ (varias multiplicaciones matriz por vector a la vez); esta mirada es la clave de la convolución como producto de matrices (sección 13).
- Regla de tamaños: $`(m\times n)(n\times p)=(m\times p)`$; las dos $n$ deben coincidir y el costo es $`m\cdot n\cdot p`$ multiplicaciones. El **orden importa**: $A$ de $`2\times3`$ por $B$ de $`3\times2`$ da $`2\times2`$, pero $BA$ da $`3\times3`$; incluso cuando ambos productos existen, en general $`AB\neq BA`$.
- Es la operación que más trabajo da a las tarjetas gráficas: videojuegos, entrenamiento de redes y *blockchain* multiplican matrices todo el tiempo.
- **`@` frente a `*`:** `@` es el producto de matrices (fila por columna) y `*` multiplica entrada por entrada. Error frecuente: escribir `*` queriendo el producto de matrices; si los tamaños coinciden no hay error, pero el resultado es otro.
- **Todas las similitudes de una vez.** Si las filas de $E$ se dividen entre su norma (matriz $U$, filas de longitud 1), $UU^T$ guarda en la posición $(i,j)$ el coseno entre la fila $i$ y la $j$. Con 20 000 documentos son 400 millones de similitudes en una sola multiplicación; así comparan masivamente imágenes o productos muchos algoritmos.

---

## 7. Tamaño, costo y memoria (mención)

En clase solo se mencionó: el producto punto cuesta poco, matriz por vector algo más y matriz por matriz «es una locura»; densa y dispersa se tocaron como el tema de memoria. Los datos de la herramienta:

| Operación (con $`n`$) | Flops | Al duplicar $`n`$ |
|---------------------|-------|-----------------|
| Producto punto | $`\approx 2n`$ | ×2 |
| Matriz $`n\times n`$ por vector | $`2n^2`$ | ×4 |
| Matriz por matriz | $`2n^3`$ | ×8 |

- **Precisión:** un número ocupa 8 bytes en float64, 4 en float32 y 2 en float16; menos bytes es más rápido y ocupa menos memoria, pero crece el redondeo. Las redes suelen usar float32 o menos.
- **Densa o dispersa:** el formato CSR guarda solo los no ceros (≈ 12 bytes cada uno más 4 por fila; la densa gasta 8 por posición) y deja de convenir hacia el 67 % de densidad. Regla práctica: imágenes y *embeddings* son densos; texto, calificaciones y redes de amigos son dispersos. El detalle de CSR no se vio en la sesión (ver [Resumen_Clase_10.md](Resumen_Clase_10.md)).

---

## 8. Una imagen es una matriz (Parte 2: visión por computadora)

Una imagen son píxeles, y los píxeles son una matriz de números. Aquí se juntan todas las ideas anteriores.

- Cada píxel guarda un valor de **brillo**; quien programa define la escala (en la herramienta, 0 negro y 16 blanco; en fotos comunes, 0 a 255). Un dígito escrito a mano se cuadricula y a cada celda se le asigna un número: los valores altos forman el trazo y los ceros el fondo, así que con solo mirar la matriz ya se «ve» la forma.
- Una imagen de alto × ancho tiene $`\text{alto}\cdot\text{ancho}`$ valores: en grises de $`28\times28`$ son $784$. Una foto Full HD tiene más de 2 millones de píxeles (más de 6 millones de números a color); por eso se vectoriza en lugar de recorrerla.
- **Color:** tres matrices del mismo tamaño, roja, verde y azul (RGB, de 0 a 255), que forman un tensor de forma $`(\text{alto},\text{ancho},3)`$. Una foto de 100 de alto por 200 de ancho tiene forma $(100,200,3)$; el 3 son los canales.

---

## 9. Operar sobre imágenes

| Operación | Cómo | Efecto |
|-----------|------|--------|
| **Brillo** | Sumar un mismo $`k`$ a todos los píxeles: $`A+k`$ (matriz más escalar, con *broadcasting*) | Aclara; los valores fuera de [0, 16] se **recortan** (*clip*) y se «saturan», pero la figura casi siempre sobrevive |
| **Contraste** | Multiplicar por $`c`$: $`cA`$ | Con $`c>1`$ se agrandan las diferencias entre claro y oscuro; con $`c<1`$ todo se ve más gris. Sumar mueve todo lo mismo; multiplicar mueve más a los valores altos y los ceros siguen en cero |
| **Negativo** | Máximo menos el valor: $`16-A`$ (en fotos, $`255-A`$) | Fondo y trazo intercambian valores; las redes lo usan para reconocer el mismo dígito en distintos formatos |
| **Umbral** | Máscara $`A>t`$ | Trazo = 1, fondo = 0. Umbral bajo: casi todo es «objeto» y no se distingue el número; muy alto: se pierde; **a media escala** queda bien escrito |

- Brillo, contraste y negativo calculan cada píxel con su propio valor, sin mirar a los vecinos. El control de brillo bajo y alto es lo que hacen, por ejemplo, los filtros de los puestos automáticos de migración de un aeropuerto.
- **Ciclo frente a vectorizado:** una imagen de $`8\times8`$ son 64 pasos en un ciclo; una de $`224\times224\times3`$ son 150 528 valores y un ciclo tarda unos 20 ms por operación, mientras la vectorizada tarda ≈ 0,1 ms (0,64 ns por valor). Un modelo aplica miles de operaciones a miles de fotos.

---

## 10. Convolución: mirar vecindades

- Un píxel aislado no dice nada (un 9 puede estar dentro del objeto o en su orilla): hay que compararlo con sus vecinos. Un **filtro** o *kernel* ($`3\times3`$) se **desliza por toda la imagen**; en cada posición multiplica el parche por el kernel entrada por entrada y suma los 9 productos (un producto punto). El resultado indica dónde aparece lo que el filtro detecta.
- **Ejemplo** (cuaderno): parche $`\begin{bmatrix}15&2&0\\12&0&0\\8&0&0\end{bmatrix}`$ y kernel de bordes $`\begin{bmatrix}-1&-2&-1\\0&0&0\\1&2&1\end{bmatrix}`$ dan $-15-4+8=-11$.
- Repetir el cálculo en todas las posiciones produce una matriz nueva, el **mapa de características**. En el cuaderno, una imagen de $`8\times8`$ con un parche de $`3\times3`$ da un mapa de $`6\times6`$.
- **Kernels típicos:** identidad, desenfoque (promedia vecinos), **Sobel** $x$/$y$ (bordes verticales/horizontales; $`\begin{bmatrix}-1&0&1\\-2&0&2\\-1&0&1\end{bmatrix}`$ mide cuánto más brillante es la derecha que la izquierda), enfoque y **laplaciano** (cambios bruscos en cualquier dirección). Se aplican varios para que el modelo aprenda a reconocer el mismo objeto en distintas formas y orientaciones. En una red convolucional esos pesos **no se escriben a mano: se aprenden**.
- **Relleno (*padding*) y paso (*stride*):** con un parche $`3\times3`$ los píxeles de la orilla quedan con menos posiciones y la imagen se encoge (de $`6\times6`$ a $`4\times4`$). Para evitarlo se agrega un marco de ceros (relleno $p$). El paso $s$ es cuánto avanza la ventana. Con $n$ el tamaño de la imagen y $k$ el del kernel:

```math
\text{salida}=\left\lfloor\frac{n-k+2p}{s}\right\rfloor+1
```

  Por ejemplo, $`28\times28`$ con kernel $`3\times3`$ y $s=1$ da $`26\times26`$ sin relleno y $`28\times28`$ con $p=1$.
- En rigor, esta operación (suma de productos sin voltear el kernel) es una **correlación cruzada**; en visión por computadora se le llama convolución. No es la multiplicación de matrices clásica, sino un producto escalar local repetido (aunque se puede reescribir como una, sección 13).

---

## 11. Bordes y características

- Un **borde es un salto de brillo**. En una sola fila de píxeles, el kernel $`[-1,0,1]`$ (vecino derecho menos izquierdo) da 0 en zonas planas, positivo donde el brillo sube y negativo donde baja; el kernel $`3\times3`$ es la misma idea repetida en tres filas. Los bordes le sirven al modelo para saber dónde termina la figura.
- Un solo filtro ve bordes de una sola orientación, así que se usan varios; con **cuatro** (izquierdo, derecho, superior e inferior) se cubre el contorno completo. Cada dígito se transforma en 4 mapas de bordes y su suma es el mapa del contorno: esa es la **extracción de características**, mirar dónde hay bordes y de qué tipo en vez de píxeles crudos.
- **ReLU** (función de activación): $`\mathrm{ReLU}(x)=\max(0,x)`$ deja pasar lo positivo y convierte lo negativo en cero; se aplica a cada entrada del mapa. Razones: un valor negativo solo dice «aquí no hay borde izquierdo», así que no se necesita, y sin una función así apilar capas lineales equivale a una sola y la red no aprende formas complejas.

---

## 12. Pooling: resumir y encoger

- El **max pooling** de $`2\times2`$ divide el mapa en bloques que no se superponen (paso 2) y conserva el mayor valor de cada uno: $`4\times4`$ pasa a $`2\times2`$ y $`8\times8`$ a $`4\times4`$. Achica el mapa conservando lo importante, así la red lee la imagen por pedacitos cada vez más resumidos.
- **No tiene pesos que aprender.** El *mean pooling* conserva el promedio: el máximo responde a «¿hubo alguna señal fuerte aquí?» y el promedio a «¿cuánta señal hubo en total?».
- **Tolerancia a desplazamientos:** si el dígito se corre 1 o 2 píxeles, el mapa antes del pooling cambia casi por completo, pero después cambia menos (alrededor de la mitad en los ejemplos). Da cierta tolerancia, no invariancia total.

---

## 13. La convolución es un producto de matrices

1. Cada parche se aplana en una **fila**. Con una imagen de $`4\times4`$ y un kernel de $`3\times3`$ hay 4 posiciones y la matriz $P$ es de $`4\times9`$ (algunos números se repiten porque los parches se traslapan).
2. El kernel se aplana en una **columna de 9 valores**; cada resultado es el producto punto de un parche con el kernel, es decir, $`P\mathbf{k}`$ (matriz por vector, «por filas»). El vector de 4 entradas, reordenado como $`2\times2`$, es la salida de la convolución.
3. Con $F$ filtros se tienen $F$ columnas (matriz $K$ de $`9\times F`$) y **una sola multiplicación** calcula todos los filtros en todas las posiciones: con $F=3$, $`(4\times9)(9\times3)=(4\times3)`$.

**Por qué se hace así:** las GPU y las librerías de álgebra lineal (BLAS, cuBLAS) están muy optimizadas para el producto de matrices (reducir la convolución a ese caso aprovecha décadas de trabajo) y el costo queda en una forma conocida. **Costo:** los parches se traslapan, así que cada píxel se guarda unas $k^2$ veces y $P$ ocupa más memoria que la imagen (algunas librerías evitan armarla).

---

## 14. Clasificar un dígito

1. **Aplanar** la imagen de $`8\times8`$ en un vector $`\mathbf{x}`$ de 64 entradas: el píxel de la fila $i$, columna $j$ (desde 0) queda en la posición $8i+j$. Se pierde la vecindad 2D, pero este primer enfoque no la necesita.
2. **Puntajes:** $`\mathbf{z}=W\mathbf{x}+\mathbf{b}`$ con $W$ de $`10\times64`$ (640 multiplicaciones): 10 puntajes, uno por dígito. Cada fila de $W$ es una **plantilla** de $`8\times8`$ de su clase (pesos positivos apoyan la clase, negativos la contradicen) y el puntaje mide cuánto se parece la imagen a ella (un producto punto).
3. **Softmax** convierte los puntajes en probabilidades: eleva $e$ a cada puntaje (todos positivos y con las diferencias exageradas) y divide entre la suma, de modo que suman 1. El orden no cambia: el mayor puntaje sigue siendo el mayor.

```math
p_c=\frac{e^{z_c}}{e^{z_0}+\cdots+e^{z_9}}
```

4. **Predicción:** la clase con la mayor probabilidad.

**Entrenar** es encontrar $W$: se parte de pesos casi cero y se repite (1) calcular los puntajes de todas las imágenes de entrenamiento (un producto de matrices), (2) medir el error (la pérdida) y (3) mover cada peso un poquito en la dirección que lo reduce: el **descenso del gradiente**. Las plantillas pasan de ruido a «dibujar» el dígito. «La combinación de pesos prácticamente da todo.»

**Limitación:** un modelo solo conoce lo que vio al entrenarse (aquí 1 347 imágenes de entrenamiento y 450 de prueba del mismo estilo). Con trazos raros se confunde (un 1 mal trazado sale como 2 o 7) y una letra se clasifica como el dígito más parecido (una K sale como 8).

---

## 15. El recorrido completo: una mini red convolucional

| Etapa | Operación | Forma de los datos |
|-------|-----------|--------------------|
| Entrada | Imagen | $`8\times8`$ |
| Convolución | 4 filtros $`3\times3`$ (bordes izquierdo, derecho, superior e inferior), relleno 1 | 4 mapas de $`8\times8`$ |
| ReLU | Anula los negativos | 4 mapas de $`8\times8`$ |
| Pooling | $`2\times2`$ | 4 mapas de $`4\times4`$ |
| Aplanar (*flatten*) | Mapas a vector | $`4\cdot4\cdot4=64`$ valores |
| Capa densa | $`W\mathbf{x}+\mathbf{b}`$, con $`W`$ de $`10\times64`$ | 10 puntajes |
| Softmax | Probabilidades | 10 probabilidades → clase |

- La red no recibe el 7 entero: recibe sus bordes (izquierdo, derecho, superior) pedazo por pedazo. Con un solo mapa de $`4\times4`$ serían 16 valores; con los 4 mapas, 64. Estos valores entran a una red **totalmente conectada** (todas las neuronas conectadas entre sí), que «aprende cómo se ve» cada dígito.
- Todo el recorrido es una operación de matrices o de vectores. Se **aprenden 650 números** (la capa densa: $`10\cdot64`$ pesos más 10 sesgos); los 36 de los kernels ($`4\cdot9`$) están fijados a mano en este ejemplo. En una red convolucional real los kernels también se aprenden, con el mismo descenso del gradiente, y se apilan muchas capas.
- **Comparación honesta:** clasificar con los bordes frente a los píxeles crudos difiere en unas 7 de 450 imágenes. Con un conjunto de prueba tan pequeño y fácil no basta para concluir mucho; la ventaja de los filtros aparece con imágenes grandes y variadas.
- Los LLM, la visión por computadora, las redes neuronales en general y los algoritmos clásicos funcionan con estas mismas operaciones.

---

## Complemento: cuaderno `6 - Actividad_en_clase.ipynb`

Caso guiado en Python (NumPy y scikit-learn) que repite los capítulos 8 a 15 con el conjunto `load_digits`: 1 797 imágenes de $`8\times8`$ de dígitos escritos a mano.

- **Convención invertida.** El cuaderno usa `gray_r`: **0 es blanco (fondo) y 16 es negro (trazo)**, al revés que la herramienta; ambos dicen que el trazo tiene valores altos. En el 0 de ejemplo el máximo es 15.
- **Operaciones sobre la imagen:** normalizar (dividir entre 16, para evitar inestabilidad numérica), transponer (refleja la imagen respecto a su diagonal), sumar 5 (brillo, con *clip* a [0, 16]) y multiplicar por 0,5 (menos contraste).
- **Datos:** cada imagen se aplana con `.flatten()` a un vector de 64; apiladas forman la matriz $X$ de $`1797\times64`$, donde cada fila es una imagen.
- **Modelo:** regresión logística con 70 % de entrenamiento (1 257 imágenes) y 30 % de prueba (540). La predicción manual es $Z=XW+b$ con $W$ de $`64\times10`$ (la transpuesta de `coef_`, que viene de $`10\times64`$); es el mismo cálculo que $`W\mathbf{x}`$ de la sección 14, solo con el vector fila a la izquierda. El softmax se calcula restando el máximo antes de exponenciar (evita desbordamientos). En la imagen de prueba 12, la manual y la del modelo coinciden: 97,46 % para el 7, que era la etiqueta real.

| Objeto | Símbolo | Dimensiones |
|--------|---------|-------------|
| Imagen | $`A`$ | $`8\times8`$ |
| Filtro | $`F`$ | $`3\times3`$ |
| Vector de píxeles | $`\mathbf{x}`$ | $`1\times64`$ |
| Datos | $`X`$ | $`1797\times64`$ |
| Pesos | $`W`$ | $`64\times10`$ |
| Sesgos | $`\mathbf{b}`$ | 10 |
| Puntajes (*logits*) | $`Z`$ | $`1\times10`$ |
| Probabilidades | $`\mathrm{softmax}(Z)`$ | $`1\times10`$ |
| Matriz de confusión | $`C`$ | $`10\times10`$ |

- **Evaluación:** exactitud de 96,67 % en la prueba (18 errores de 540). En la **matriz de confusión** las filas son las etiquetas reales y las columnas las predicciones; la diagonal son los aciertos. La confusión más frecuente: 5 imágenes de un 8 clasificadas como 1.
- **Mapas de pesos:** al reorganizar los 64 pesos de una clase en $`8\times8`$, el contorno del 0 pesa positivo y su centro negativo: trazo en el centro descarta el 0.
- **Ejercicios:** (1) pintar el centro de un 0 con 16 cambia la predicción a 8, porque se activan los pesos negativos del 0; (2) agregar ruido gaussiano reduce la probabilidad de la clase correcta, aunque la predicción puede conservarse; (3) un 1 dibujado a mano en una matriz $`8\times8`$ fue clasificado como **2** en la salida guardada (el texto del cuaderno dice que normalmente se detecta bien): ilustra que el modelo solo conoce el estilo del conjunto de entrenamiento.
- **Autoevaluación:** (a) se vectoriza para asignar un peso a cada píxel, sin relaciones espaciales 2D; (b) el filtro es una operación local que se desliza, mientras $XW+b$ es un producto punto global sobre todos los píxeles; (c) softmax convierte puntajes en probabilidades que suman 1; (d) un peso muy negativo en la clase 8 significa que ese píxel encendido descarta el 8; (e) normalizar a $`[0,1]`$ evita que unas características dominen y ayuda a que la optimización converja.

---

## Conceptos clave

- **Vector** = lista ordenada (el orden importa); **matriz** = tabla $`m\times n`$ (filas primero) cuyas filas y columnas son vectores; la **transpuesta** voltea filas y columnas.
- **Vectorizar** = una operación sobre todo el arreglo en lugar de un ciclo; mismo resultado, cientos de veces más rápido. Las máscaras filtran por condición; `axis` indica la dirección.
- **Producto punto** = dos vectores en un número; signo y ortogonalidad dependen del ángulo. **Coseno** (más parecidos = más cerca de 1) es la medida de similitud de buscadores y *embeddings*.
- **$`A\mathbf{x}`$** = filas punto $`\mathbf{x}`$ o combinación de columnas; una capa de red es $`W\mathbf{x}+\mathbf{b}`$. **$AB$** = filas punto columnas; el orden y los tamaños importan; `@` no es `*`.
- **$UU^T$** con filas normalizadas da todas las similitudes coseno a la vez.
- **Una imagen es una matriz** (RGB: tres, forma $`(\text{alto},\text{ancho},3)`$); brillo, contraste, negativo y umbral son operaciones vectorizadas.
- **Convolución** = filtro deslizante (producto punto por parche) que detecta bordes; tamaño de salida $`\lfloor(n-k+2p)/s\rfloor+1`$; se reduce a un producto de matrices. **ReLU** aporta la no linealidad, el **pooling** resume sin pesos y **aplanar** convierte el mapa en un vector. **Softmax** da probabilidades.
- **Entrenar** = ajustar los pesos con el descenso del gradiente; el modelo solo sabe lo que vio.

---

## Fuera del PDF — logística, tareas y metodología

- **Material:** la herramienta HTML queda en el campus (se descarga y se abre en el computador) y, junto con el cuaderno, en `Clases/PDFs/`. Se recomienda recorrerla y «jugar» con ella.
- **Tarea:** la semana tendrá una tarea más liviana y divertida, sin más detalles en la sesión. Hay que confirmarla en el campus.
- **Siguiente clase:** empieza **ecuaciones diferenciales**. En *Administración de datos* se verán los LLM; se dejarán el artículo «Attention Is All You Need» y un video guía sobre cómo funcionan.
- **IA soberana:** depender de un solo proveedor de IA es un riesgo (si falla, la jornada se detiene); conviene tener un plan alternativo, como un modelo que corra local o en una nube privada. A escala de organización o de país es soberanía tecnológica.
- **Orientación profesional (preguntas de cierre):** programar no «murió», cambió la carpintería manual; el valor pasa a definir algoritmos, escalabilidad, diseño y razonamiento. Se necesitan menos programadores *junior* para la misma tarea. Perfiles con demanda: ingeniería de IA, infraestructura y DevOps, seguridad (firewall, configuración), arquitectura y gobernanza de datos; lectura sugerida: *Thinking in Systems*. Combinar datos con un dominio (finanzas, manufactura) abre la hiperespecialización. Después de la capa semántica (la IA actual) viene la **capa física** (robótica).
