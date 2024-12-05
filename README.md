# 🌍 Relevancia del Resumen Automático de Noticias

La **tarea de resumir texto automáticamente**, especialmente noticias diarias, tiene gran relevancia para **investigadores** y **profesionales** de **Procesamiento de Lenguaje Natural (PLN)**, **IA** y **automatización de contenido**. Algunas razones clave son:

- **Avances en PLN**: Modelos como **T5** han revolucionado el PLN, permitiendo la generación automática de resúmenes coherentes y relevantes a gran escala.
  
- **Eficiencia y accesibilidad**: Resúmenes automáticos permiten a los usuarios consumir información rápida y eficientemente, manteniéndose al tanto sin leer artículos largos.

- **Aplicaciones comerciales**: Sectores como **marketing de contenidos**, **medios de comunicación** y **noticias personalizadas** se benefician de la capacidad de generar resúmenes precisos y bien estructurados, mejorando la experiencia del usuario.

---

# 📰 Utilidad del Resumen Automático de Noticias Diarias

### a. **Mejora de la experiencia del usuario en plataformas de noticias**  
Las **plataformas digitales de noticias** (como sitios web, aplicaciones móviles o newsletters) pueden utilizar modelos como T5 para ofrecer **resúmenes automáticos** de los artículos más relevantes del día. Esto no solo mejora la **experiencia del usuario** al proporcionar **información condensada** y de fácil acceso, sino que también permite a los usuarios **estar informados** sin tener que navegar a través de contenido extenso.

#### Ejemplo real:
Una **aplicación de noticias** como **Flipboard** o **Google News** podría integrar un modelo de resumen automático que ofrezca a los usuarios un **resumen personalizado** y **breve** de las noticias más relevantes, adaptado a sus intereses. De esta forma, la aplicación podría presentar solo la **información esencial**, lo cual es especialmente útil para personas con poco tiempo.


### b. **Filtrado y personalización de contenido**  
Un **sistema de resúmenes** puede ser utilizado para **filtrar contenido** de manera más efectiva, presentando solo lo más relevante para cada usuario. Esto sería especialmente útil para plataformas que ofrecen **noticias personalizadas**, como **Feedly** o **Pocket**. Los modelos de resumen no solo seleccionarían las noticias más relevantes, sino que también las condensarían, permitiendo a los usuarios consumirlas rápidamente.

#### Ejemplo real:
Un usuario que pregunta a su asistente virtual "¿Qué ha pasado en el mundo hoy?" podría recibir un **resumen breve y conciso** de las noticias más importantes, generado automáticamente por el modelo entrenado con datos de **DailyMail**. Esto mejora la **experiencia del usuario** al ofrecer información relevante de forma instantánea.

### c. **Asistentes Virtuales y Chatbots**  
Los **asistentes virtuales** (como **Siri**, **Alexa** o **Google Assistant**) podrían integrar este tipo de modelos para ofrecer **resúmenes automáticos** de noticias diarias o temas específicos a los usuarios. Estos resúmenes podrían entregarse **por voz** o en **formato de texto**, permitiendo que los usuarios se mantengan al tanto de las novedades sin tener que buscar activamente la información.

#### Ejemplo real:
Un servicio como **Pocket** o **Instapaper** podría ofrecer **resúmenes automáticos** de artículos largos, optimizados según los intereses de los usuarios. Imagina que un usuario lee a menudo sobre **tecnología** o **política**. La aplicación podría generar resúmenes de los artículos más recientes sobre estos temas, presentados de forma concisa, para facilitar la lectura rápida.

---

## 🛠️ Modelo: T5-small

El modelo T5-small fue entrenado en un gran corpus de texto, lo que significa que tiene una comprensión general del lenguaje. Sin embargo, no está específicamente preentrenado para resúmenes de noticias como el dataset DailyMail. Es por eso que necesitas realizar un *fine-tuning* con este dataset específico para que el modelo aprenda las peculiaridades de este tipo de texto.

### Tamaño adecuado
T5-small es lo suficientemente pequeño como para ser entrenado en hardware moderado, pero lo suficientemente grande como para ofrecer buenos resultados en tareas de resumen automático.

### Capacidad de fine-tuning
Puedes ajustar las últimas capas de T5-small y adaptar el modelo al dataset DailyMail para mejorar la calidad de los resúmenes generados.

### Compatibilidad
El modelo está bien soportado en plataformas como TensorFlow y PyTorch, lo que facilita su implementación y ajuste.

### Resumen
El modelo T5-small es adecuado para realizar *fine-tuning* en el dataset DailyMail para generar resúmenes automáticos de noticias. El dataset es lo suficientemente grande, pero puede requerir algunos pasos de preprocesamiento y limpieza. Si bien el modelo no está entrenado específicamente para resúmenes de noticias, su capacidad de generalización en tareas de texto lo hace una opción sólida para este problema.

---

## 🎯 Dataset: DailyMail

El dataset DailyMail está compuesto por artículos de noticias y sus resúmenes (targets) correspondientes. En términos generales, los datos están balanceados en cuanto a la longitud de los artículos y sus resúmenes, ya que cada artículo tiene un resumen de longitud variable.

El dataset DailyMail tiene un número suficientemente grande de ejemplos (aproximadamente 300,000 pares de artículos y resúmenes), lo que debería ser adecuado para realizar un entrenamiento eficaz.

---

## 🚀 Conclusiones

Durante el entrenamiento del modelo <a href="https://huggingface.co/google-t5/t5-small">**T5-Small**</a> utilizando 100,000 pares de noticias y resúmenes del conjunto de datos <a href="https://huggingface.co/datasets/abisee/cnn_dailymail">**CNN/DailyMail**</a>, se identificaron los mejores parámetros y estrategias que llevaron a obtener métricas ROUGE significativas. Las estadísticas finales alcanzadas por el modelo son las siguientes:

- **ROUGE-1**: 0.3090  
- **ROUGE-2**: 0.1209  
- **ROUGE-L**: 0.2300  
- **ROUGE-LSum**: 0.2614  

### Razones de las mejores métricas obtenidas

1. **Congelación parcial del encoder**:  
   Al congelar las primeras 5 capas del encoder durante el entrenamiento, se redujo la cantidad de parámetros ajustables. Esto permitió que el modelo aprovechara representaciones preentrenadas efectivas en las capas iniciales mientras se concentraba en ajustar las capas superiores para la tarea específica de resumen. Este enfoque puede haber prevenido problemas de sobreajuste y permitido un mejor aprendizaje en un tiempo limitado.

2. **Tasa de aprendizaje moderada (`5e-5`) y programación lineal**:  
   El uso de una tasa de aprendizaje relativamente baja, junto con un calentamiento inicial (`warmup_steps=1000`) y un programador lineal, contribuyó a una convergencia más estable. Esta configuración ayudó a evitar actualizaciones agresivas que podrían haber llevado a oscilaciones o degradación del desempeño.

3. **Regularización y estabilidad**:  
   - La **tasa de abandono (`dropout_rate=0.3`)** introdujo una robusta regularización que redujo el riesgo de sobreajuste al conjunto de entrenamiento.  
   - El **decaimiento de pesos (`weight_decay=0.01`)** contribuyó a limitar la magnitud de los pesos del modelo, mejorando la generalización en el conjunto de evaluación.

4. **Uso eficiente de recursos**:  
   - La acumulación de gradientes (`gradient_accumulation_steps=2`) permitió entrenar con un mayor tamaño de lote efectivo sin exceder los límites de memoria.  
   - El uso de punto flotante mixto (`fp16=True`) aceleró el entrenamiento y mejoró la eficiencia computacional.  

5. **Métricas ROUGE alineadas con la tarea**:  
   Las métricas ROUGE obtenidas indican un desempeño sólido considerando la capacidad del modelo (T5-Small) y el conjunto de datos empleado.  
   - **ROUGE-1** y **ROUGE-L**, que evalúan la coincidencia de n-gramas y la secuencia más larga coincidente, destacan la capacidad del modelo para capturar información relevante y estructurar resúmenes coherentes.  
   - El menor valor de **ROUGE-2**, más exigente, refleja la dificultad inherente de capturar contextos precisos en resúmenes más concisos.

## 🧠 Resultados del modelo entrenado:

Tras observar las métricas y cambiar los parámetros que mejor funcionaban, entrenamos el modelo con 100.000 registros de noticias, afinando así en el resumen de éstas.
Dada esta noticia:


  " Bitcoin surges past $100k for first time
  The price of Bitcoin `has for the first time broken past the $100,000 mark, hitting a new record high`.
  The value of the world's biggest cryptocurrency has been boosted by hopes US President-elect Donald Trump will adopt crypto-friendly policies.
  The milestone was reached hours after Trump said he would nominate former Securities and Exchange Commission (SEC) commissioner Paul Atkins to run the Wall Street regulator.
  Mr Atkins is seen as being far more pro-cryptocurrency than the current head of the SEC, Gary Gensler.
  The $100,000 milestone prompted celebrations from cryptocurrency fans around the world.
  Bitcoin's wildly fluctuating value has always attracted interest, with its backers reacting with delight when it has passed previous price thresholds - and defiance during its slumps.
  But this particular landmark has been especially keenly anticipated. `For weeks charts, memes and predictions have swirled around social media about when the price would hit the figure` thought to    be one of the holy grails of the crypto world.
  Millions of viewers even tuned in to online watch parties as the price hovered close to $100k.
  The value of a single bitcoin is one of the barometers of optimism in the cryptocurrency industry which is now estimated to be worth $3.3tn, according to analysis firm Coin Market Cap.
  Trump's election victory last month was the catalyst for the latest surge.
  The president-elect has vowed to make the US "the crypto capital of the planet" - a remarkable turnaround given as recently as 2021 he was calling Bitcoin a "scam."
  Also remarkable is just how Bitcoin's price has rocketed. `A valuation of $100k represents a 40% increase on election day in the U.S. and more than double the price it started the year at`.
  `But there's lots more to Bitcoin than the dizzying changes in its value`.
  From its enigmatic inventor to the bringing down of the so-called Crypto King, it's a story with many twists and turns, which has seen the making - and losing - of huge fortunes.
  So here's the BBC's list of the seven wildest moments - so far - in Bitcoin's tumultuous history. "


El resultado del modelo preentrenado sin fine-tuning es este:
```text
"has for the first time broken past the $100,000 mark, hitting a new record high. a valuation of $100k represents a 40% increase on election day in the U.S. and more than double the price it started the year at. but there's lots more to Bitcoin than the dizzying changes in its value. for weeks charts, memes and predictions have swirled around social media about when the price would hit the figure."
```
🔍 Observamos cómo se limita a copiar fragmentos de texto,subrayados en la noticia original, sin desarrollar nada ni dar coherencia.

Tras nuestro entrenamiento este es el resultado:
```text
"Bitcoin has for the first time broken past the $100,000 mark, hitting a new record high. The price of a single bitcoin is one of the barometers of optimism in the cryptocurrency industry. A valuation of $100k represents a 40% increase on election day in the U.S. and more than double the price it started the year at. But there's lots more to Bitcoin than the dizzying changes in its value."
```
Mostrando una clara mejoría en fluidez y comprensión, además siendo capaz de trabajar el contexto de la noticia.

---

# 💡 Reflexión final

El diseño de los hiperparámetros fue clave para maximizar el desempeño del modelo dado el tamaño del conjunto de datos y las limitaciones inherentes de T5-Small. La combinación de estrategias como la congelación parcial, una tasa de aprendizaje moderada y una adecuada regularización, junto con la calidad del conjunto de datos CNN/DailyMail, permitió al modelo alcanzar métricas competitivas en la tarea de generación de resúmenes. Estos resultados subrayan la importancia de ajustar cuidadosamente los hiperparámetros y de aprovechar técnicas como la transferencia de aprendizaje para mejorar modelos compactos.
