# Clase 11 — Matrices en la IA: repaso computacional y visión por computadora

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University

**Semana:** 11

**Material fuente:** transcripción de la sesión (2 h 15 min) y `5 - Guia computo eficiente.pdf` (**guía base**, 17 páginas), que ya se había dejado la semana anterior y se resume en [Resumen_Clase_10.md](Resumen_Clase_10.md). La sesión se guió con una **herramienta HTML interactiva** (publicada en el campus) que sigue la guía base capítulo por capítulo y termina con un caso de visión por computadora; esa herramienta no está en el repositorio.

**Cobertura del PDF:** Parcial: páginas 2 a 9 de 17 (etapas 1 a 5, hasta «Matriz por matriz»): vectores y matrices, operar todo a la vez, producto punto/norma/coseno, matriz por vector y matriz por matriz, repasadas con la herramienta. Las etapas 6 a 8 (ceros y densidad, CSR, costo y precisión) solo se mencionan de pasada y el formato CSR no se vio. La sección 8 (visión por computadora) no tiene PDF y sale solo de la transcripción.

**Nota sobre las fuentes:** la transcripción es automática y tiene cifras y términos mal reconocidos (p. ej. «Ford» por for, «Flatenin» por flatten); se corrigieron con la guía base. Una frase dice que dos palabras más parecidas tienen un coseno «más reducido»; es al revés: **más parecidas = coseno más cercano a 1**, y así se anota aquí. Las secciones 1 a 6 siguen el orden de las etapas de la guía base.

**Contexto.** Sesión de repaso con enfoque computacional para ver «la matemática retratada»: los vectores, el producto punto y la multiplicación de matrices son lo que hay detrás de los buscadores, las redes neuronales, la visión por computadora y los LLM. Los documentos de la semana anterior resultaron densos (largos y cada vez más técnicos), así que la herramienta recorre la guía base de forma visual y con preguntas rápidas. La clase de ecuaciones diferenciales empieza la semana siguiente.

---

## 1. Vectores: la unidad básica

- Un **vector** es una lista **ordenada** de números; el orden importa: $(3,-1,4)\neq(-1,3,4)$. Cada posición significa algo (en una casa: metros cuadrados, cuartos, baños, años de construida), igual que el orden de las letras en el texto: «hola» no es «aloh».
- Se ve como una **flecha** con dirección y longitud; de ahí sale Pitágoras y, más adelante, la norma.
- **Operaciones:** la suma es entrada por entrada, $(2,1)+(1,3)=(3,4)$, y el producto por un escalar estira o encoge, $3\cdot(2,1)=(6,3)$.
- **Los vectores toman decisiones.** Un vector de entradas de una cámara de vehículo puede activar el freno si cruza un umbral; la suma de vectores de señales (palabras clave de enojo, tono) puede alertar a un asistente de un centro de llamadas.
- **La IA empieza convirtiendo todo en vectores:** una palabra es un vector de cientos de números (un *embedding*), una imagen se aplana en un vector, un cliente es (edad, ingreso, compras).

**Texto vectorizado y *embeddings*.** Vectorizar un texto es convertirlo en números consultables; los *embeddings* son justamente eso. Cuando un documento se «indexa» en una herramienta de IA empresarial, se parte en miles de fragmentos y cada uno se guarda como vector; luego el modelo consume esos vectores y **predice la siguiente palabra** según probabilidades. Matemáticamente no «lee»: opera con números.

---

## 2. Matrices: la estructura donde vive todo

- Una matriz es una tabla de números de tamaño $m\times n$, **filas primero**. $`r_{23}`$ es la fila 2, columna 3: cada valor debe poder ubicarse al 100 %, y eso es lo que hace tan manejable la matriz para una computadora.
- Una matriz son **filas apiladas** (vectores fila) o **columnas lado a lado** (vectores columna); esa doble mirada es la que se usa al multiplicar. Por eso es fácil pasar de matrices a vectores en una red neuronal.
- La **transpuesta** voltea la matriz: las filas pasan a ser columnas. Una matriz de $5\times7$ tiene una transpuesta de $7\times5$.
- Las matrices son la estructura de las imágenes, las bases de datos y los **pesos de las redes neuronales**.
- **Matrices dispersas:** en muchos problemas casi todo son ceros (cada usuario califica pocas películas de miles; cada documento usa pocas palabras del diccionario). Se guardan solo las entradas distintas de cero.

---

## 3. Vectorizar: operar el arreglo completo

- **Vectorizar** es escribir una sola operación para todo el arreglo en lugar de recorrerlo número por número con un ciclo. Es la forma natural de pensar en matrices y lo que vuelve rápido el cómputo en NumPy y en las redes neuronales: el resultado es el mismo, cambia la forma de ejecutarlo. Es como en estructuras de datos: dos algoritmos dan el mismo resultado y uno es mucho más eficiente.
- Ejemplo: la suma de cuadrados de $(3,-1,4,-1,5,-9)$ se escribe `(x**2).sum()` (cada entrada al cuadrado, luego la suma) y da 133, sin ciclo. Es parecido a aplicar una función a toda una lista.
- **Máscaras:** `x > 0` devuelve qué entradas cumplen la condición (aquí 3 valores) y permite traer solo los valores con ciertas características. Es el mismo concepto de la máscara en Photoshop: una matriz encima que dice qué se quiere y qué no.
- **Restar la media de cada columna:** se usa `axis=0` (una operación por columna).
- **Tiempos con $10^7$ números** (herramienta, mismas proporciones que los tiempos de la clase 10): ciclo sobre el arreglo NumPy 1,33 s; ciclo sobre listas de Python 350 ms; vectorizado 6,4 ms.
- **Complejidad.** Medir cuánto cuesta resolver un problema es central; ejemplo de fondo: el problema **P vs NP**. P son los problemas que una computadora resuelve rápido (ordenar números, buscar un archivo); NP son aquellos en los que una solución propuesta se puede **verificar** rápido.

---

## 4. Producto punto, norma y coseno

- El **producto punto** convierte dos vectores en **un solo número**: se multiplica posición por posición y se suma. Ejemplo: $(1,2,3)\cdot(4,0,-1)=4+0-3=1$.
- **Signo y ángulo:** ángulo agudo, producto punto positivo (apuntan hacia el mismo lado); 90°, producto punto 0. **Si el producto punto de dos vectores no nulos es cero, son ortogonales.**
- **Norma** (longitud): $`\|(3,4)\|=\sqrt{25}=5`$. La distancia es la norma de la diferencia.
- **Coseno:** mide qué tan parecidos son dos vectores (1 = misma dirección, 0 = perpendiculares). Es la medida con que los buscadores comparan textos e imágenes.
- **Búsqueda por imagen** (tipo Google Lens): la imagen se **vectoriza** y se compara con las demás por producto punto y coseno; las de mayor parecido (incluso en ropa, postura o fondo) salen primero. Una imagen pixelada igual encuentra coincidencias.
- **Palabras parecidas.** En un buscador semántico cada palabra es un vector y se compara con el coseno: «perro» y «perrito» quedan cerca. Pero la misma palabra cambia de sentido según el contexto («¿qué me dice, perrito?» es un saludo, no un animal), y con solo el coseno el modelo se confundiría. Los modelos grandes lo resuelven **alimentándose de contexto** y de datos etiquetados por personas (vectores auxiliares que corrigen cuándo dos palabras parecidas en realidad están lejos). Todo eso apunta a una IA más **general**, que responda cualquier cosa y no una sola variable.

---

## 5. Matriz por vector, transformaciones y capas de una red

- **Por filas:** cada entrada de $A\mathbf{x}$ es el producto punto de una fila de $A$ con $\mathbf{x}$. **Por columnas:** $A\mathbf{x}$ es una **combinación de las columnas** de $A$ con las entradas de $\mathbf{x}$ como pesos. Conviene dominar las dos.
- **Regla de tamaños:** el número de columnas de $A$ debe ser igual al número de entradas de $\mathbf{x}$. Una matriz $3\times3$ con un vector de 3 sí; con uno de 2, no; una $2\times4$ con un vector de 4 sí; una $3\times5$ con un vector de 4, no.
- **Transformaciones** (clase 9): identidad, estirar, girar, reflejar e inclinar; la matriz transforma el plano, y por eso una IA puede «leer» una matriz como una imagen.
- **Una capa de red neuronal es una matriz por vector.** La entrada $\mathbf{x}$ (por ejemplo 3 píxeles) se multiplica por la matriz de pesos $W$ y se suma el vector de sesgos $\mathbf{b}$: $W\mathbf{x}+\mathbf{b}$. Cada fila de $W$ es una neurona (con $W$ de $2\times3$ hay dos neuronas de tres pesos cada una) y todas se calculan con **una sola multiplicación**. **Entrenar** es encontrar los pesos y sesgos que funcionan mejor, mediante el descenso del gradiente (se verá en ecuaciones diferenciales).

---

## 6. Matriz por matriz

- Cada entrada del resultado es el **producto punto de una fila de la primera con una columna de la segunda**. Mirada alternativa: cada columna de $C=AB$ es $A$ por la columna correspondiente de $B$.
- Regla de tamaños: $(m\times n)(n\times p)=(m\times p)$; las dos $n$ deben coincidir. El **orden importa**.
- Es la operación que más trabajo da a las tarjetas gráficas: videojuegos, entrenamiento de redes y *blockchain* multiplican matrices todo el tiempo.
- **`@` frente a `*`:** `@` es el producto de matrices (fila por columna) y `*` multiplica entrada por entrada; dan resultados distintos.
- **Todas las similitudes de una vez.** Si las filas de $U$ se dividen entre su norma (longitud 1), $UU^T$ guarda en la posición $(i,j)$ el coseno entre la fila $i$ y la $j$. Con 20 000 documentos son 400 millones de similitudes en una sola multiplicación; así comparan masivamente imágenes o productos muchos algoritmos.

---

## 7. Costo, memoria y matrices dispersas (mención)

Cuánto gasta el computador (flops): el producto punto cuesta poco, matriz por vector algo más y matriz por matriz «es una locura». Densa y dispersa se mencionaron como el tema de memoria; el detalle de CSR no se vio (ver [Resumen_Clase_10.md](Resumen_Clase_10.md)).

---

## 8. Caso: visión por computadora (sin PDF)

Una imagen son píxeles, y los píxeles son una matriz de números. Aquí se juntan todas las ideas anteriores.

### La imagen como matriz

- Cada píxel guarda un valor de **brillo** (negro = 0, más blanco = valor más alto); quien programa define la escala (en la herramienta, 0 a 16). Un dígito escrito a mano se cuadricula y a cada celda se le asigna un número.
- Una imagen en grises de $28\times28$ tiene $28\cdot28=784$ valores. Una imagen real puede tener millones de píxeles, por eso se vectoriza en lugar de recorrerla.
- **Color:** tres matrices, roja, verde y azul (RGB). Una foto en color de 100 de alto por 200 de ancho tiene forma $(100,200,3)$; el 3 son los canales.

### Operar sobre imágenes

| Operación | Cómo | Efecto |
|-----------|------|--------|
| **Brillo** | Sumar un mismo $k$ a todos los píxeles (matriz más escalar, con *broadcasting*) | Aclara; con $k$ muy alto los valores se **recortan** al máximo (*clip*) y la imagen se satura, pero la figura casi siempre sobrevive |
| **Negativo** | Invertir el brillo (máximo menos el valor) | Fondo y trazo intercambian valores; las redes lo usan para reconocer el mismo dígito en distintos formatos |
| **Umbral** | Máscara «brillo mayor que el umbral» = trazo, el resto = fondo | Umbral bajo: no se distingue el número; muy alto: se pierde; **a media escala** queda bien escrito |

- **Ciclo frente a vectorizado:** una imagen de $8\times8$ son 64 pasos en un ciclo; una imagen de $224\times224\times3$ son 150 528 valores y un ciclo tarda unos 20 ms, mientras la operación vectorizada se aplica a todos los píxeles a la vez.

### Convolución: el filtro que recorre la imagen

- Un **filtro** o *kernel* (p. ej. $3\times3$) se **desliza por toda la imagen**; en cada posición multiplica el parche por el filtro y suma (un producto punto). El resultado indica dónde aparece lo que el filtro detecta.
- **Bordes:** un borde es un **salto de brillo**. Los filtros típicos son identidad, desenfoque, enfoque, **Sobel** (bordes en una dirección) y **laplaciano** (cambios en cualquier dirección). Se aplican varios para que el modelo aprenda a reconocer el mismo objeto en distintas formas y orientaciones.
- **Relleno (*padding*):** con un parche $3\times3$ los píxeles de la orilla quedan con menos posiciones y la imagen se encoge (de $6\times6$ a $4\times4$). Para evitarlo se agrega un marco de ceros.
- **ReLU** (función de activación): $\mathrm{ReLU}(x)=\max(0,x)$ deja pasar lo positivo y convierte lo negativo en cero. Razones: conserva las respuestas útiles del filtro y, sin una función así, apilar capas lineales equivale a una sola y la red no aprende formas complejas.
- **Pooling:** achica el mapa conservando lo importante, así la red lee la imagen por pedacitos cada vez más resumidos.
- **Aplanar (*flatten*):** el último mapa pequeño (p. ej. $4\times4=16$ valores) se convierte en **un vector** que entra a una red totalmente conectada (todas las neuronas conectadas entre sí). La red no recibe el 7 entero: recibe sus bordes, pedazo por pedazo.

### La convolución es un producto de matrices

Cada parche se aplana en una **fila** y el filtro $3\times3$ en una **columna de 9 valores**; cada resultado es el producto punto de un parche con el filtro. Con varios filtros se tienen varias columnas y todo es una sola multiplicación de matrices. **Dos razones:** las GPU y las librerías están muy optimizadas para el producto de matrices (reducir la convolución a ese caso aprovecha décadas de trabajo), y el costo es que los parches se traslapan, así que cada píxel se guarda varias veces y la matriz ocupa más memoria que la imagen (algunas librerías evitan armarla).

### Clasificar un dígito

1. La imagen se aplana y se multiplica por la matriz de pesos más el sesgo: **10 puntajes**, uno por dígito (cada fila de pesos es una «plantilla» y el puntaje mide cuánto se parece la imagen a ella, un producto punto).
2. **Softmax** convierte los puntajes en probabilidades; la predicción es el dígito con la mayor.
3. **Entrenar** es ajustar los pesos: al inicio la red falla y poco a poco encuentra la combinación que clasifica bien. «La combinación de pesos prácticamente da todo.»

Flujo completo: imagen → convolución → ReLU → pooling → aplanar → capas densas → probabilidades. Limitación: un modelo solo conoce lo que vio al entrenarse; con un conjunto de datos pequeño se confunde (un 1 mal trazado sale como 2 o 7) y una letra se clasifica como el dígito más parecido (una K sale como 8).

---

## Conceptos clave

- **Vector** = lista ordenada (el orden importa); **matriz** = tabla $m\times n$ (filas primero) cuyas filas y columnas son vectores; la **transpuesta** voltea filas y columnas.
- **Vectorizar** = una operación sobre todo el arreglo en lugar de un ciclo; mismo resultado, muchísimo más rápido. Las máscaras filtran por condición; `axis` indica la dirección.
- **Producto punto** = dos vectores en un número; signo y ortogonalidad dependen del ángulo. **Coseno** (más parecidos = más cerca de 1) es la medida de similitud de buscadores y *embeddings*.
- **$A\mathbf{x}$** = filas punto $\mathbf{x}$ o combinación de columnas; una capa de red es $W\mathbf{x}+\mathbf{b}$. **$AB$** = filas punto columnas; el orden y los tamaños importan; `@` no es `*`.
- **$UU^T$** con filas normalizadas da todas las similitudes coseno a la vez.
- **Una imagen es una matriz** (RGB: tres, forma $(\text{alto},\text{ancho},3)$); brillo, negativo y umbral son operaciones vectorizadas.
- **Convolución** = filtro deslizante (producto punto por parche) que detecta bordes; se reduce a un producto de matrices. **ReLU** aporta la no linealidad, el **pooling** resume y **aplanar** convierte el mapa en un vector. **Softmax** da probabilidades.
- Los LLM, la visión por computadora, las redes neuronales y los algoritmos clásicos funcionan con estas mismas operaciones.

---

## Fuera del PDF — logística, tareas y metodología

- **Material:** la herramienta HTML queda en el campus; se descarga y se abre en el computador. Se recomienda recorrerla y «jugar» con ella.
- **Tarea:** la semana tendrá una tarea más liviana y divertida, sin más detalles en la sesión. Hay que confirmarla en el campus.
- **Siguiente clase:** empieza **ecuaciones diferenciales**. En *Administración de datos* se verán los LLM; se dejarán el artículo «Attention Is All You Need» y un video guía sobre cómo funcionan.
- **IA soberana:** depender de un solo proveedor de IA es un riesgo (si falla, la jornada se detiene); conviene tener un plan alternativo, como un modelo que corra local o en una nube privada. A escala de organización o de país es soberanía tecnológica.
- **Orientación profesional (preguntas de cierre):** programar no «murió», cambió la carpintería manual; el valor pasa a definir algoritmos, escalabilidad, diseño y razonamiento. Se necesitan menos programadores *junior* para la misma tarea. Perfiles con demanda: ingeniería de IA, infraestructura y DevOps, seguridad (firewall, configuración), arquitectura y gobernanza de datos; lectura sugerida: *Thinking in Systems*. Combinar datos con un dominio (finanzas, manufactura) abre la hiperespecialización. Después de la capa semántica (la IA actual) viene la **capa física** (robótica).
