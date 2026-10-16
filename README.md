# Nu | Insurance Benefits Prediction and Data Protection

## Descripción general

Las compañías de seguros administran información personal, familiar y financiera que puede utilizarse para comprender mejor a sus clientes, identificar perfiles similares y desarrollar modelos predictivos que apoyen la toma de decisiones.

En este proyecto se analizan datos de clientes de la compañía de seguros **Sure Tomorrow** mediante técnicas de Machine Learning, vecinos cercanos y álgebra lineal.

El proyecto aborda cuatro tareas principales:

1. Encontrar clientes con características similares.
2. Predecir si un cliente recibirá beneficios de seguro.
3. Estimar la cantidad de beneficios que podría recibir.
4. Proteger los datos personales sin afectar el desempeño de los modelos.

---

## Problema de negocio

Sure Tomorrow busca aprovechar sus datos históricos para mejorar diferentes procesos relacionados con la gestión de clientes y beneficios de seguro.

La compañía necesita determinar si las técnicas de Machine Learning pueden ayudar a:

- Identificar clientes con perfiles similares.
- Apoyar estrategias de segmentación y comunicación.
- Estimar la probabilidad de que un cliente reciba beneficios.
- Predecir la cantidad de beneficios recibidos.
- Proteger la información personal almacenada.
- Mantener la calidad del modelo después de transformar los datos.

Este proyecto desarrolla y evalúa soluciones para cada una de estas necesidades.

---

## Objetivo general

Desarrollar diferentes soluciones de Machine Learning y álgebra lineal para analizar clientes de seguros, predecir beneficios y proteger información personal sin reducir la calidad de los modelos.

---

## Objetivos específicos

- Examinar la estructura y calidad de los datos.
- Corregir los tipos de datos cuando sea necesario.
- Identificar valores ausentes y registros duplicados.
- Explorar las principales características de los clientes.
- Encontrar clientes similares mediante el algoritmo de vecinos más cercanos.
- Analizar el efecto del escalado sobre las medidas de distancia.
- Construir una variable objetivo binaria relacionada con la recepción de beneficios.
- Entrenar un modelo de clasificación.
- Comparar el clasificador con modelos aleatorios de referencia.
- Implementar una regresión lineal mediante álgebra matricial.
- Predecir la cantidad de beneficios recibidos.
- Evaluar el modelo mediante RMSE y R².
- Desarrollar un método de ofuscación para proteger los datos personales.
- Comprobar que la transformación de los datos no altere la calidad de la regresión.

---

## Dataset utilizado

El análisis utiliza el archivo:

```text
insurance_us.csv
```

El dataset contiene información de clientes relacionada con:

- Género.
- Edad.
- Ingresos.
- Número de familiares.
- Cantidad de beneficios de seguro recibidos.

### Variables principales

| Variable | Descripción |
|---|---|
| `gender` | Género registrado del cliente |
| `age` | Edad del cliente |
| `income` | Ingresos estimados |
| `family_members` | Número de familiares |
| `insurance_benefits` | Cantidad de beneficios de seguro recibidos |

> Los nombres de las columnas pudieron normalizarse durante el preprocesamiento para facilitar su manipulación con Python.

---

## Metodología

El proyecto se organizó en cinco etapas principales.

### 1. Preparación de datos

- Carga del archivo `insurance_us.csv`.
- Inspección de dimensiones y tipos de datos.
- Revisión de valores ausentes.
- Búsqueda de registros duplicados.
- Normalización de nombres de columnas.
- Corrección de tipos de datos.
- Análisis estadístico inicial.

### 2. Búsqueda de clientes similares

- Selección de características personales.
- Aplicación del algoritmo de vecinos más cercanos.
- Comparación de diferentes métricas de distancia.
- Evaluación con datos originales.
- Evaluación con datos escalados.
- Análisis del impacto del escalado.

### 3. Predicción de recepción de beneficios

- Creación de una variable objetivo binaria.
- Separación entre características y objetivo.
- División entre entrenamiento y prueba.
- Entrenamiento de un modelo de clasificación.
- Evaluación mediante la métrica F1.
- Comparación con modelos aleatorios de referencia.

### 4. Predicción de la cantidad de beneficios

- Implementación de una regresión lineal personalizada.
- Cálculo de los pesos mediante operaciones matriciales.
- Generación de predicciones.
- Evaluación mediante RMSE.
- Evaluación mediante el coeficiente de determinación R².

### 5. Protección de datos personales

- Creación de una matriz invertible.
- Transformación de las características originales.
- Recuperación de los datos mediante la matriz inversa.
- Comparación de predicciones antes y después de la transformación.
- Verificación de la estabilidad de las métricas.

---

## Análisis exploratorio

Durante la inspección inicial se analizaron:

- Distribuciones de edad e ingresos.
- Cantidad de familiares por cliente.
- Frecuencia de recepción de beneficios.
- Relaciones entre las características.
- Balance de la variable objetivo binaria.
- Posibles diferencias de escala entre las variables.

Uno de los hallazgos más importantes fue la diferencia considerable de escala entre las características. Por ejemplo, los ingresos presentan valores mucho mayores que la edad o la cantidad de familiares.

Esta diferencia resulta especialmente importante para los algoritmos basados en distancias.

---

## Tarea 1: clientes similares

Se utilizó el algoritmo de vecinos más cercanos para identificar clientes con características semejantes.

La búsqueda se realizó considerando variables como:

- Edad.
- Género.
- Ingresos.
- Número de familiares.

También se comparó el comportamiento del algoritmo bajo diferentes condiciones:

- Datos originales.
- Datos escalados.
- Distancia euclidiana.
- Distancia Manhattan.

### Importancia del escalado

Los resultados mostraron que el escalado es fundamental para los algoritmos basados en distancias.

Sin escalado, las variables con valores numéricos más grandes, especialmente los ingresos, dominan el cálculo de las distancias. Esto reduce la influencia relativa de características como la edad o el número de familiares.

Después del escalado, todas las variables participan de manera más equilibrada en la identificación de clientes similares.

---

## Tarea 2: predicción de beneficios recibidos

La variable original `insurance_benefits` representa la cantidad de beneficios recibidos.

Para construir un problema de clasificación, se creó una nueva variable binaria:

```text
0 → el cliente no recibió beneficios
1 → el cliente recibió uno o más beneficios
```

Esta transformación permitió entrenar un modelo para estimar si un cliente probablemente recibirá beneficios de seguro.

### Evaluación

El modelo fue evaluado mediante la métrica F1, que combina:

- Precisión.
- Sensibilidad o recall.

También se construyeron modelos aleatorios con diferentes probabilidades para comprobar si el clasificador entrenado ofrecía un rendimiento superior a una predicción realizada al azar.

La comparación permitió determinar si el modelo encontraba patrones útiles en los datos o si su desempeño podía explicarse mediante una estrategia aleatoria.

---

## Tarea 3: regresión lineal

Se implementó una clase personalizada de regresión lineal mediante operaciones matriciales.

La solución incluyó:

- Adición del término independiente.
- Cálculo de pesos.
- Uso de la matriz transpuesta.
- Aplicación de la matriz inversa.
- Generación de predicciones.

La estructura matemática utilizada para obtener los pesos fue:

\[
w = (X^T X)^{-1} X^T y
\]

Posteriormente, las predicciones se calcularon mediante:

\[
\hat{y} = Xw
\]

### Métricas utilizadas

El modelo fue evaluado mediante:

#### RMSE

El error cuadrático medio permite medir la magnitud promedio de los errores expresada en las mismas unidades de la variable objetivo.

#### R²

El coeficiente de determinación indica qué proporción de la variabilidad del objetivo es explicada por el modelo.

La evaluación permitió medir la capacidad del modelo para estimar la cantidad de beneficios de seguro recibidos.

---

## Tarea 4: ofuscación de datos

La protección de información personal se abordó mediante una transformación matricial.

Las características originales se transformaron utilizando una matriz invertible:

\[
X' = XP
\]

Donde:

- \(X\) representa la matriz original de características.
- \(P\) representa una matriz invertible.
- \(X'\) representa las características transformadas.

Los datos originales pueden recuperarse mediante:

\[
X = X'P^{-1}
\]

### Objetivo de la transformación

La transformación busca dificultar la interpretación directa de los datos personales sin destruir la información matemática necesaria para realizar predicciones.

La matriz utilizada debe ser invertible. De lo contrario, no sería posible recuperar la información original ni demostrar matemáticamente la equivalencia del modelo.

---

## Conservación de la calidad del modelo

Si las características originales se transforman mediante:

\[
X' = XP
\]

los pesos del modelo transformado se relacionan con los pesos originales mediante:

\[
w' = P^{-1}w
\]

Por tanto:

\[
X'w' = XP P^{-1}w = Xw
\]

Esto demuestra que las predicciones pueden mantenerse iguales después de transformar las características mediante una matriz invertible.

La comparación entre los modelos entrenados con datos originales y datos transformados permitió verificar que:

- Las predicciones permanecen equivalentes o prácticamente iguales.
- El RMSE se conserva.
- El valor de R² se mantiene.
- La transformación protege la interpretación directa de los datos.
- La calidad de la regresión no se deteriora.

---

## Resultados principales

El proyecto permitió establecer las siguientes conclusiones:

- El escalado modifica significativamente la selección de vecinos cercanos.
- Los ingresos pueden dominar las distancias cuando las variables no están estandarizadas.
- La conversión del objetivo a formato binario permite abordar la recepción de beneficios como un problema de clasificación.
- Los modelos aleatorios funcionan como una referencia básica para evaluar el clasificador.
- La regresión lineal puede implementarse directamente mediante álgebra matricial.
- Las métricas RMSE y R² permiten evaluar la magnitud del error y la capacidad explicativa del modelo.
- Una matriz invertible permite transformar y recuperar las características.
- La ofuscación matricial puede proteger los datos sin afectar la calidad de las predicciones.

---

## Conclusión ejecutiva

El proyecto demostró que los datos de clientes de Sure Tomorrow pueden utilizarse para resolver diferentes necesidades mediante técnicas de Machine Learning y álgebra lineal.

El algoritmo de vecinos cercanos permitió identificar clientes con perfiles similares, aunque sus resultados dependieron considerablemente del escalado de las características.

El modelo de clasificación permitió estudiar la probabilidad de que un cliente recibiera beneficios y comparar su desempeño con estrategias aleatorias de referencia.

La regresión lineal permitió estimar la cantidad de beneficios recibidos y evaluar las predicciones mediante RMSE y R².

Finalmente, la transformación matricial mostró que es posible proteger la información personal sin reducir la calidad del modelo. Las características transformadas conservaron la información necesaria para generar predicciones equivalentes, mientras dificultaron la interpretación directa de los datos originales.

En conjunto, el proyecto evidencia que la analítica predictiva y la protección de datos pueden integrarse dentro de una misma solución técnica.

---

## Tecnologías utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- Álgebra lineal
- Google Colab
- Git
- GitHub

---

## Estructura sugerida del repositorio

```text
Nu-Insurance-Benefits-Prediction/
│
├── README.md
├── insurance_us.csv
├── Nu_Insurance_Benefits_Prediction.ipynb
├── requirements.txt
└── .gitignore
```

Si prefieres separar los archivos por carpetas:

```text
Nu-Insurance-Benefits-Prediction/
│
├── README.md
│
├── data/
│   └── insurance_us.csv
│
├── notebooks/
│   └── Nu_Insurance_Benefits_Prediction.ipynb
│
├── requirements.txt
└── .gitignore
```

> Antes de publicar `insurance_us.csv`, se recomienda confirmar que el archivo puede redistribuirse públicamente. Si no existe autorización, debe excluirse del repositorio mediante `.gitignore` y documentarse su ubicación esperada.

---

## Instalación

Clona el repositorio:

```bash
git clone https://github.com/TU-USUARIO/Nu-Insurance-Benefits-Prediction.git
```

Ingresa al directorio:

```bash
cd Nu-Insurance-Benefits-Prediction
```

Crea un entorno virtual:

```bash
python -m venv venv
```

Activa el entorno en Linux o macOS:

```bash
source venv/bin/activate
```

Activa el entorno en Windows:

```bash
venv\Scripts\activate
```

Instala las dependencias:

```bash
pip install -r requirements.txt
```

Abre el notebook:

```bash
jupyter notebook Nu_Insurance_Benefits_Prediction.ipynb
```

---

## Dependencias

El archivo `requirements.txt` puede contener:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
jupyter
```

---

## Reproducibilidad

Los procedimientos aleatorios del proyecto utilizan semillas definidas para facilitar la reproducción de resultados.

Ejemplo:

```python
random_state=12345
```

Para la generación de números aleatorios con NumPy:

```python
rng = np.random.default_rng(seed=42)
```

---

## Posibles mejoras

- Evaluar métricas de distancia adicionales.
- Optimizar el número de vecinos.
- Ajustar hiperparámetros del modelo de clasificación.
- Comparar la regresión lineal con otros algoritmos.
- Incorporar validación cruzada.
- Analizar con mayor profundidad el desbalance de clases.
- Implementar una interfaz interactiva.
- Evaluar métodos adicionales de anonimización.
- Analizar el efecto de diferentes matrices de transformación.
- Desarrollar pruebas automatizadas para validar la recuperación de datos.

---

## Autor

**Santiago Rodríguez Zaraza**

Proyecto desarrollado como parte de un portafolio profesional de Data Science y Machine Learning.

---

## Estado del proyecto

**Completado**

El proyecto incluye:

- Preparación y exploración de datos.
- Búsqueda de clientes similares.
- Escalado de características.
- Clasificación de beneficios.
- Comparación con modelos aleatorios.
- Regresión lineal personalizada.
- Evaluación mediante RMSE y R².
- Ofuscación de información personal.
- Validación de la conservación de la calidad del modelo.
