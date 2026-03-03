#Proyecto: Predicción de Cancelación (Churn) en Telecom X

1. Introducción
Este proyecto tiene como objetivo predecir la cancelación de clientes (churn) en la empresa Telecom X utilizando técnicas de Machine Learning. La identificación temprana de clientes en riesgo de abandono es crucial para implementar estrategias de retención efectivas.

2. Datos
El conjunto de datos utilizado (datos_tratados.csv) contiene información sobre clientes de Telecom X, incluyendo datos demográficos, servicios contratados, información de facturación y el estado de Churn (si el cliente ha cancelado o no).

Variables clave:
•	CustomerID: Identificador único del cliente (eliminado en preprocesamiento).
•	Churn: Variable objetivo (Yes/No).
•	Tenure: Antigüedad del cliente en meses.
•	ChargesMonthly: Cargo mensual del cliente.
•	Contract: Tipo de contrato (Month-to-month, One year, Two year).
•	OnlineSecurity, TechSupport, SeniorCitizen, Dependents, PaperlessBilling, PaymentMethod, etc.

3. Metodología
El análisis se estructuró en las siguientes etapas:

3.1. Extracción y Carga de Datos
•	Se cargó el archivo datos_tratados.csv en un DataFrame de pandas.

3.2. Preprocesamiento y Limpieza de Datos
•	Eliminación de columnas irrelevantes: CustomerID fue eliminada.
•	Manejo de inconsistencias: Los valores 'No internet service' en columnas de servicios se reemplazaron por 'No' para unificar categorías.
•	Verificación de nulos: Se confirmó la ausencia de valores nulos.
•	Eliminación de columnas correlacionadas: ChargesDaily y ChargesTotal se eliminaron para evitar multicolinealidad, ya que presentaban alta correlación con ChargesMonthly y Tenure.

3.3. Análisis Exploratorio de Datos (EDA) y Selección de Características
•	Correlación numérica: Tenure mostró una correlación negativa con Churn.
•	Análisis de variables categóricas (Test Chi-Cuadrado): Se identificaron las variables más significativas para Churn: Contract, OnlineSecurity, TechSupport, SeniorCitizen, Dependents, PaperlessBilling y PaymentMethod. Las variables Gender y PhoneService resultaron no ser significativas y fueron eliminadas.

3.4. División de Datos (Split)
•	Los datos se dividieron en conjuntos de entrenamiento (80%) y prueba (20%) utilizando stratify=y para mantener la proporción de clases de Churn.

3.5. Codificación One-Hot (One-Hot Encoding)
•	Se aplicó One-Hot Encoding a las variables categóricas restantes para convertirlas en un formato numérico adecuado para los modelos.

3.6. Verificación de Desbalance de Clases
•	Se confirmó un desequilibrio significativo en la variable Churn en el conjunto de entrenamiento (aproximadamente 26.5% de clientes con Churn).

3.7. Entrenamiento y Evaluación de Modelos
Se entrenaron y evaluaron dos modelos iniciales:
•	Regresión Logística (sin balanceo): Mostró buena precisión para la clase 'No Churn', pero un recall bajo para la clase 'Churn'.
•	Random Forest: Rendimiento similar a la Regresión Logística sin balanceo.
•	Regresión Logística (con class_weight='balanced'): Este modelo mejoró significativamente el recall para la clase 'Churn' (0.79), lo cual es crucial para identificar clientes en riesgo.

4. Conclusiones y Recomendaciones

4.1. Modelo Seleccionado
•	La Regresión Logística con balanceo de clases es el modelo más adecuado hasta ahora debido a su alto recall en la detección de Churn. En un contexto de predicción de abandono, es más valioso identificar a la mayor cantidad posible de clientes en riesgo para intervenir, aunque esto implique una menor precisión general.

4.2. Acciones Estratégicas
•	Las estrategias de retención deben enfocarse en clientes con contratos a corto plazo, sin seguridad en línea o soporte técnico, y que son 'SeniorCitizen' o no tienen dependientes. Estas variables han demostrado ser las más influyentes en la decisión de abandonar.


