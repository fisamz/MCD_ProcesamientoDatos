# Procesamiento y Clasificación de Datos

**Maestría en Ciencia de Datos · Facultad de Ciencias Físico Matemáticas, UANL**

Este repositorio reúne las siete tareas del curso. Más que siete ejercicios sueltos, forman un
recorrido con un hilo conductor: **cómo representar distintos tipos de datos —texto, imagen y
sonido— para que una computadora pueda analizarlos y clasificarlos.**

En cada medio se plantea la misma pregunta de fondo con distinta forma: *¿qué manera de convertir
el dato en números funciona mejor, y por qué?* Las respuestas resultaron distintas en cada caso, y
esa comparación es el aporte central del trabajo.

---

## Hilo conductor

| Medio | Tareas | La comparación | Qué ganó |
|---|---|---|---|
| **Texto** | 1, 2, 3 | conteo simple vs pesos aprendidos | aprender de los datos |
| **Imagen** | 4, 5 | reglas fijas vs conocimiento heredado | heredar (con pocos datos) |
| **Sonido** | 6, 7 | herramienta general vs específica del dominio | la específica |

Una lección se repite en los tres medios: **la representación importa tanto como el modelo**. Elegir
cómo se describe el dato suele pesar más que qué algoritmo se le aplique después.

---

## Las tareas

### Tarea 1 — Análisis textual
**Pregunta:** ¿escribe distinto quien reseña música que quien reseña productos de belleza?

Estadística descriptiva sobre reseñas reales de Amazon (dos categorías): frecuencias de palabras,
n-gramas, puntuación, riqueza léxica y emojis. Hallazgo: las reseñas de música son más del doble
de largas y giran en torno a juicios estéticos; las de belleza son breves y hablan de resultados.
La categoría del producto condiciona *cómo* se escribe, no solo de qué se habla.

📁 [`Tarea1/`](Tarea1/)

### Tarea 2 — Vectorización y análisis de sentimiento
**Pregunta:** ¿el sentimiento del texto coincide con la calificación en estrellas?

Se convierten las reseñas en vectores (bolsa de palabras, TF-IDF) y se estudian sus propiedades:
dimensión, dispersión, y qué miden las distancias entre ellos. Luego se mide el sentimiento con el
léxico AFINN y se compara contra las estrellas. Hallazgo: la correlación es clara (ρ ≈ 0.5), pero
el léxico falla de forma sistemática en las negaciones ("never disappoints" lo lee como negativo).

📁 [`Tarea2/`](Tarea2/)

### Tarea 3 — Clasificación de textos (diseño de experimentos)
**Pregunta:** ¿cuánto se gana al aprender los pesos de las palabras en lugar de heredarlos?

Diseño experimental por etapas: primero se elige la mejor representación, luego el mejor modelo e
hiperparámetro, y solo al final se evalúa una vez sobre datos nunca vistos. Hallazgo: el modelo
que *aprende* los pesos supera al diccionario de la Tarea 2, y el error que queda no es de
polaridad (positivo/negativo) sino de intensidad (distinguir 4★ de 5★).

📁 [`Tarea3/`](Tarea3/)

### Tarea 4 — Análisis de imágenes: detección de monedas
**Pregunta:** ¿se pueden encontrar y contar monedas en una foto?

Transformada de Hough para detectar círculos, siguiendo el pipeline de la clase (gris → desenfoque
→ detección). Un paso extra: como las monedas mexicanas tienen diámetros distintos, se clasifica la
denominación y se cuenta el dinero de la foto. Hallazgo: funciona bien con buena luz, y el parámetro
de sensibilidad de Hough manda sobre todo lo demás; las sombras son el punto débil.

📁 [`Tarea4/`](Tarea4/)

### Tarea 5 — Clasificación de imágenes con redes convolucionales
**Pregunta:** ¿conviene entrenar una red desde cero o heredar una ya entrenada?

Se comparan, en igualdad de condiciones, una CNN construida desde cero contra *transfer learning*
con MobileNetV2 (pre-entrenada en ImageNet), clasificando fotos de flores. Hallazgo: con pocos
datos, heredar no es una mejora incremental sino la diferencia entre funcionar y no funcionar. La
red heredada logra más entrenando muchos menos parámetros: lo difícil —ver— ya venía aprendido.

📁 [`Tarea5/`](Tarea5/)

### Tareas 6 y 7 — Procesamiento y clasificación de audio
**Pregunta:** ¿qué representación del sonido reconoce mejor un dígito hablado?

Clasificación de dígitos 0–9 dichos en voz alta, comparando **MFCC** (diseñado para voz) contra
**wavelets** (herramienta general). Hallazgo doble: MFCC gana con claridad (99% vs 84%), porque
está hecho para el oído humano; y —lo más importante— al probar con una voz nunca antes escuchada,
la exactitud cae de 99% a 60%. Ese contraste revela que el número alto era en parte una ilusión:
el modelo reconocía voces conocidas, no solo dígitos.

📁 [`Tarea6-7_sixseven_/`](Tarea6-7_sixseven_/)

---

## Cómo está organizado

```
├── comun/            código y datos compartidos entre tareas
├── Tarea1/           análisis textual
├── Tarea2/           vectorización + sentimiento
├── Tarea3/           clasificación de textos
├── Tarea4/           detección de monedas
├── Tarea5/           CNN de flores
├── Tarea6-7_sixseven_/         clasificación de audio
└── README.md         este archivo
```

Cada carpeta contiene su notebook, su reporte (`README.md` con los hallazgos) y sus figuras. Los
datasets no se versionan (están en `.gitignore`); cada reporte incluye las instrucciones para
descargarlos.

## Herramientas

Python (Jupyter en VS Code) · pandas · scikit-learn · nltk · OpenCV · TensorFlow/Keras · librosa ·
PyWavelets

---

*Facultad de Ciencias Físico Matemáticas · Universidad Autónoma de Nuevo León*
