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

Durante el entrenamiento del modelo **T5-Small** utilizando 100,000 pares de noticias y resúmenes del conjunto de datos **CNN/DailyMail**, se identificaron los mejores parámetros y estrategias que llevaron a obtener métricas ROUGE significativas. Las estadísticas finales alcanzadas por el modelo son las siguientes:

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

### Comparación del modelo sin entrenar vs. modelo entrenado

A continuación, se presentan ejemplos comparativos entre el desempeño del modelo **sin entrenar** y el modelo **entrenado** en la tarea de resumen de texto.  

#### Modelo sin entrenar
![Modelo sin entrenar](ruta/a/la/imagen-sin-entrenar.png)

#### Modelo entrenado
![Modelo entrenado](ruta/a/la/imagen-entrenado.png)

---

# 💡 Reflexión final

El diseño de los hiperparámetros fue clave para maximizar el desempeño del modelo dado el tamaño del conjunto de datos y las limitaciones inherentes de T5-Small. La combinación de estrategias como la congelación parcial, una tasa de aprendizaje moderada y una adecuada regularización, junto con la calidad del conjunto de datos CNN/DailyMail, permitió al modelo alcanzar métricas competitivas en la tarea de generación de resúmenes. Estos resultados subrayan la importancia de ajustar cuidadosamente los hiperparámetros y de aprovechar técnicas como la transferencia de aprendizaje para mejorar modelos compactos.


