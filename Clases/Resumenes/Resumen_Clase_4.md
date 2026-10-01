# Clase 4 — Combinación lineal, subespacios y producto punto

**Curso:** BCD3103 Álgebra Lineal y Ecuaciones Diferenciales · Ingeniería en Ciencia de Datos, Lead University
**Semana:** 3
**PDF fuente:** `Clase 3 y 4.pdf` (53 diapositivas, el mismo de la clase 3)
**Cobertura del PDF:** Parcial: diapositivas 15 a 20 de 53 (hasta «Calcular e interpretar el producto punto»). La clase anterior terminó en la diapositiva 14; el repaso inicial de la práctica 3 (diapositivas 13–14) se recoge al principio. La práctica del producto punto (diapositiva 21) y el resto quedan para la siguiente clase. No se saltó ninguna diapositiva del rango.

**Contexto.** Se cierra el bloque de vectores: repaso de la tarea, combinaciones lineales, generado y subespacios, y primera aproximación al producto punto. Es la base para matrices y regresión. Lo visto hasta la diapositiva 20 debe dominarse antes de la próxima sesión.

---

## 0. Repaso de la práctica 3 (diapositivas 13–14, clase anterior)

- **Distributiva sobre escalares** $(k+m)\mathbf{u}=k\mathbf{u}+m\mathbf{u}$ con $k=3$, $m=-1$, $\mathbf{u}=(2,5,-1)$: ambos lados dan $(4,10,-2)$. La asociativa de la suma también se cumple: el orden en que se agrupan las sumas no altera el resultado.
- **Despejar con incógnitas vectoriales:** se aplican las mismas reglas del álgebra de una variable. En $2\mathbf{x}+\mathbf{a}=5\mathbf{b}-\mathbf{x}$ conviene dejar la incógnita de un solo lado: se suma $\mathbf{x}$ (queda $3\mathbf{x}$) y se pasa $\mathbf{a}$ restando; luego se escala por $\tfrac13$.
- **Regla de las dimensiones:** solo se comparan u operan vectores de la misma dimensión. Si $\mathbf{b}$ tuviera 3 componentes y $\mathbf{a}$ 2, el despeje no está definido.
- **Escalar vs. vector:** en $5\mathbf{b}$ el 5 es un número que multiplica a $\mathbf{b}$; no agrega componentes. Multiplicar o sumar un vector con un escalar es válido; combinar dos vectores de dimensiones distintas, no.
- Los vectores también pueden describirse en 4 o más dimensiones (p. ej., la cuarta como tiempo en física); el álgebra permite razonar en cualquier dimensión aunque no se pueda visualizar.

---

## 1. Combinaciones lineales y subespacios (diapositivas 15–18)

Escalar y sumar varios vectores a la vez produce una **combinación lineal**: la idea detrás de cada modelo lineal y de cada subespacio.

$$\mathbf{w}=c_1\mathbf{v}_1+c_2\mathbf{v}_2+\cdots+c_k\mathbf{v}_k \qquad \text{gen}\{\mathbf{v}_1,\ldots,\mathbf{v}_k\}$$

$c_1,\ldots,c_k$ son los **coeficientes** (o pesos de la mezcla) y $\mathbf{v}_i$ los vectores.

### Lo que hay que fijar

- **Mezclar vectores con pesos:** una combinación lineal solo usa las dos operaciones básicas, escalar y sumar. Los coeficientes son los pesos; en IA son los que el modelo ajusta.
- **Generado (span):** todo lo que se puede alcanzar combinando los vectores. Parte siempre del origen.
  - Un vector no nulo genera una **recta por el origen**.
  - Dos vectores no paralelos en $\mathbb{R}^2$ generan el **plano completo**.
- **Subespacio:** un "espacio dentro del espacio". Un conjunto $S$ es subespacio si cumple tres condiciones:
  1. Contiene al vector cero.
  2. Es cerrado bajo la suma: $\mathbf{u},\mathbf{v}\in S \Rightarrow \mathbf{u}+\mathbf{v}\in S$.
  3. Es cerrado bajo el escalar: $\mathbf{u}\in S \Rightarrow k\mathbf{u}\in S$.
- **Modelo lineal:** una regresión lineal predice con una combinación lineal de las variables.
- **Pregunta frecuente:** "¿$\mathbf{w}$ es combinación lineal de $\mathbf{v}_1$ y $\mathbf{v}_2$?" equivale a "¿$\mathbf{w}$ está en el espacio que generan?".

### Ejemplos resueltos (diapositiva 16)

**1. Calcular una combinación.** $3\mathbf{v}_1-2\mathbf{v}_2$ con $\mathbf{v}_1=(1,0,2)$, $\mathbf{v}_2=(0,1,-1)$:
- Se escala cada vector: $3\mathbf{v}_1=(3,0,6)$ y $-2\mathbf{v}_2=(0,-2,2)$.
- Se suma componente a componente: $(3,-2,8)$.
- Los pesos son 3 y $-2$. El signo pertenece al coeficiente: se escalan los vectores (con un peso negativo si corresponde) y luego se suma siempre; el menos no cambia los vectores originales.
- Para expresar la combinación se escribe cada coeficiente junto a su vector, con el resultado entre paréntesis.

**2. ¿Es $\mathbf{w}$ combinación de $\mathbf{v}_1$ y $\mathbf{v}_2$?** $\mathbf{w}=(4,5)$, $\mathbf{v}_1=(2,1)$, $\mathbf{v}_2=(1,2)$. Hay que hallar los coeficientes $c_1,c_2$:

$$\begin{cases}2c_1+c_2=4\\ c_1+2c_2=5\end{cases}$$

- Se despeja $c_1=5-2c_2$ de la segunda ecuación y se sustituye en la primera: $2(5-2c_2)+c_2=4\Rightarrow c_2=2$, y entonces $c_1=1$.
- Verificación: $1\cdot(2,1)+2\cdot(1,2)=(4,5)$. Resultado: $\mathbf{w}=1\mathbf{v}_1+2\mathbf{v}_2$.
- Si el sistema tiene solución, el vector está en el generado; si es inconsistente, no lo está.

### Cómo plantear el sistema (método general)

1. Cada componente de la combinación da una ecuación: la primera coordenada de $c_1\mathbf{v}_1+c_2\mathbf{v}_2$ se iguala a la primera de $\mathbf{w}$, y así sucesivamente. Dos coeficientes desconocidos → dos ecuaciones.
2. **Sustitución:** despejar un coeficiente de una ecuación y reemplazarlo en la otra (método del ejemplo 2).
3. **Suma de ecuaciones** (eliminación): sumar miembro a miembro las dos ecuaciones; si un coeficiente se cancela, queda una ecuación con una sola incógnita. Con $c_1+c_2=5$ y $c_1-c_2=1$: $2c_1=6\Rightarrow c_1=3$.
4. Con un coeficiente conocido, se sustituye en cualquiera de las ecuaciones originales para obtener el otro ($c_2=5-3=2$).
5. Verificar en el enunciado original.

Los coeficientes $c_i$ **no** son los componentes de $\mathbf{w}$: son los números por los que hay que multiplicar cada vector para obtenerlo. Un repaso dedicado de sistemas de ecuaciones queda para la próxima clase.

### Práctica 4 (diapositivas 17–18) — soluciones

| Ejercicio | Resultado |
|-----------|-----------|
| a) $2(1,-1,0)+3(0,2,1)-(4,1,-2)$ | $(-2,3,5)$ |
| b) $\mathbf{w}=(5,1)$ como combinación de $\mathbf{v}_1=(1,1)$, $\mathbf{v}_2=(1,-1)$: $c_1+c_2=5$, $c_1-c_2=1$ | $\mathbf{w}=3\mathbf{v}_1+2\mathbf{v}_2$ |
| c) ¿$(2,4,6)$ y $(1,2,4)$ están en el generado de $(1,2,3)$? | Sí para $(2,4,6)$ ($c=2$ en las tres posiciones); no para $(1,2,4)$ |
| d) ¿$S=\{(x,2x)\}$ es subespacio de $\mathbb{R}^2$? | Sí: es la recta $y=2x$ por el origen |

- **Generado de un solo vector (c):** se busca un único escalar $c$ que funcione en todas las posiciones. En $(1,2,4)$ la primera posición pide $c=1$, pero la tercera pide $3c=4$: contradicción, luego no está en la recta.
- **Trampa de dimensiones:** $(2,4)$ no puede estar en el generado de vectores de $\mathbb{R}^3$; la regla de la misma dimensión sigue aplicando.
- **Subespacio (d)** (pendiente de verlo en Python; resuelto en el PDF): cero ($x=0$ da $(0,0)\in S$); suma ($(a,2a)+(b,2b)=(a+b,2(a+b))\in S$); escalar ($k(a,2a)=(ka,2ka)\in S$).
- Para probar que algo **no** es subespacio basta un contraejemplo; para probar que sí lo es, hay que verificar las tres condiciones en general. Una recta que no pasa por el origen (p. ej. $y=2x+1$) nunca es subespacio porque no contiene al cero.

---

## 2. Por qué importan los pesos (contexto de IA)

- Los coeficientes de una combinación lineal son los **pesos** de un modelo. Una red neuronal multiplica variables por pesos y busca, mediante **descenso de gradiente** y *backpropagation*, los coeficientes que minimizan el error.
- Las GPU son útiles porque resuelven a gran escala este tipo de operaciones matriciales.
- Los tokens de un modelo de lenguaje son vectores (texto convertido en números); las redes y los *transformers* los transforman mediante combinaciones lineales. Las imágenes y los videos se "vectorizan" (píxeles RGB → números) para entrar a modelos de visión por computadora.
- **Calidad de datos:** los pesos salen de los datos. Si hay valores atípicos o datos de mala calidad, los pesos se distorsionan y el modelo falla en producción aunque muestre buena precisión en las pruebas (*garbage in, garbage out*). Un estudio del MIT reportó que cerca del 95 % de los proyectos de IA generativa no logran impacto real, en buena parte por la calidad de los documentos y datos de entrada.
- Tener el fundamento matemático es lo que permite proponer métodos nuevos en lugar de solo reutilizar modelos existentes.

---

## 3. Producto punto: dos vectores, un número (diapositivas 19–20)

Es la operación más importante del curso: mide alineación, define la norma, calcula predicciones y es la base del producto de matrices.

**Definición algebraica**

$$\mathbf{u}\cdot\mathbf{v}=\sum_{i=1}^{n}u_iv_i=u_1v_1+u_2v_2+\cdots+u_nv_n$$

- En pocas palabras: multiplicar posición por posición y sumar todo. Entran dos vectores de la misma dimensión y sale **un solo número** (un escalar), no un vector.

**Propiedades**

| # | Propiedad | Expresión |
|---|-----------|-----------|
| 1 | Conmutativa | $\mathbf{u}\cdot\mathbf{v}=\mathbf{v}\cdot\mathbf{u}$ |
| 2 | Distributiva | $\mathbf{u}\cdot(\mathbf{v}+\mathbf{w})=\mathbf{u}\cdot\mathbf{v}+\mathbf{u}\cdot\mathbf{w}$ |
| 3 | Saca escalares | $(k\mathbf{u})\cdot\mathbf{v}=k(\mathbf{u}\cdot\mathbf{v})$ |
| 4 | Positividad | $\mathbf{v}\cdot\mathbf{v}=\|\mathbf{v}\|^2\ge 0$ |

La norma de la clase 1 es un caso particular del producto punto: $\mathbf{v}\cdot\mathbf{v}=\|\mathbf{v}\|^2$.

### Ejemplos resueltos (diapositiva 20)

**1. Calcular.** $\mathbf{u}=(2,-1,3)$, $\mathbf{v}=(4,5,-2)$:
- Productos por posición: $8,\ -5,\ -6$. Suma: $\mathbf{u}\cdot\mathbf{v}=-3$.
- Un producto punto **negativo** indica que los vectores apuntan, en conjunto, en sentidos opuestos.

**2. Una predicción es un producto punto.** Pesos $\mathbf{w}=(0{,}5;\ 2;\ -1)$ y observación $\mathbf{x}=(10,3,4)$:

$$\hat{y}=\mathbf{w}\cdot\mathbf{x}=5+6-4=7$$

- Cada peso dice cuánto aporta su variable a la predicción. Es la ecuación de una regresión lineal.
- Aplicar el producto punto reduce un vector a un solo número; por eso es la operación central de las redes neuronales y de la regresión (multiplicar un vector de pesos por un vector de variables).
- Las aplicaciones de ángulo, ortogonalidad y proyección se verán en las siguientes diapositivas.

---

## Conceptos clave

- Las reglas y axiomas del álgebra de los reales aplican a los vectores; sirven para verificar igualdades y despejar.
- **Combinación lineal:** resultado de escalar y sumar vectores; los coeficientes son los pesos.
- **Generado:** todo lo alcanzable con esas combinaciones, siempre desde el origen; un vector genera una recta, dos no paralelos en $\mathbb{R}^2$ el plano.
- **Subespacio:** contiene al cero y es cerrado bajo suma y escalar.
- **¿$\mathbf{w}$ está en el generado?** Se plantea un sistema con una ecuación por componente y se resuelve para los coeficientes; si es inconsistente, no está.
- **Sistema de 2 ecuaciones:** sustitución o suma de ecuaciones; hallar un coeficiente, sustituir y verificar.
- **Producto punto:** multiplicar posición por posición y sumar; da un escalar; $\mathbf{v}\cdot\mathbf{v}=\|\mathbf{v}\|^2$; un resultado negativo indica sentidos opuestos.
- **Predicción lineal:** $\hat{y}=\mathbf{w}\cdot\mathbf{x}$.

---

## Fuera del PDF — logística, tareas y metodología

- **Práctica de la semana:** documento con 5 ejercicios sobre lo visto (combinación lineal, pesos, generado, producto punto). Lo publica el docente; se resuelve paso a paso durante la semana.
- **Material de repaso:** videos sobre el producto punto y sobre combinaciones de vectores, más una lista de reproducción con ejercicios adicionales. Se publican en el campus junto al documento.
- **Hasta dónde debe estar claro:** hasta la diapositiva 20. La práctica de la diapositiva 21 (producto punto) se hace en clase la próxima semana.
- **Próxima clase:** repaso de sistemas de ecuaciones (primer y segundo grado) con 2–3 ejercicios, uso de pizarra digital para resolver a mano, laboratorio en Python (p. ej., verificar un subespacio) y continuación del producto punto hacia matrices.
- **Evaluación:** habrá evaluaciones cortas en clase; lo esencial es comprender el procedimiento, y se puede pedir más tiempo si hace falta. Escribir cada paso ayuda a evitar errores de cálculo.
- **Revisión:** se puede enviar al docente ejercicios resueltos (escaneados) para revisión.
- **Asistencia y cámara:** se pide cámara encendida durante la sesión; si no es posible, avisar antes por mensaje o correo para registrarlo. La justificación de ausencia o llegada tarde se envía por WhatsApp o correo.
