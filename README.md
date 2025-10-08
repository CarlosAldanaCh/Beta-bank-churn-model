

Beta Bank Churn – Predicción de abandono de clientes

Descripción

Proyecto de clasificación supervisada que busca predecir si un cliente de Beta Bank abandonará el banco (churn).
El objetivo principal es optimizar la métrica F1 (≥ 0.59) y comparar resultados con la métrica AUC-ROC, abordando además el desequilibrio de clases (≈80/20) en los datos.


---

Estructura del proyecto

beta_bank_churn/
├─ data/
│  └─ Churn.csv
├─ notebook/
│  └─ beta_bank_churn_model.ipynb
├─ requirements.txt
├─ README.md
└─ LICENSE


---

Objetivo del modelo

Predecir la probabilidad de abandono (Exited = 1) para que el banco identifique clientes con riesgo y aplique estrategias de retención.


---

Dataset

Archivo: data/Churn.csv
Variable objetivo: Exited
Características principales:

CreditScore, Geography, Gender, Age, Tenure, Balance,
NumOfProducts, HasCrCard, IsActiveMember, EstimatedSalary, etc.
Valores nulos: solo en Tenure (~10%), imputados con mediana y una bandera binaria (tenure_was_null).



---

Proceso de desarrollo

1. Preparación de datos

División estratificada train/test (80/20).

Codificación:

One-Hot Encoding (OHE) → Regresión Logística.

OrdinalEncoder → Árbol de Decisión y Bosque Aleatorio.


Estandarización: StandardScaler solo para Regresión Logística.


2. Modelos base

Regresión Logística

Árbol de Decisión

Random Forest


3. Técnicas de manejo de desequilibrio

class_weight='balanced' (en los tres modelos).

SMOTE (Synthetic Minority Oversampling Technique) en conjunto de entrenamiento vía imblearn.Pipeline.

Ajuste de umbral de decisión con predict_proba para maximizar F1.


4. Métricas de evaluación

F1-Score (métrica principal).

AUC-ROC (comparativa de desempeño).

Precision, Recall, Matriz de confusión para interpretación del modelo.



---

Resultados principales

Modelo	Técnica	F1	AUC-ROC	Observaciones

Regresión Logística	class_weight + umbral	0.57	0.81	Mejora moderada, sin alcanzar meta
Árbol de Decisión	class_weight + umbral	0.59	0.84	Cumple la meta
Árbol de Decisión	SMOTE + umbral	0.59	0.83	Buen balance
Random Forest	class_weight	0.63	0.86	Mejor desempeño general
Random Forest	SMOTE + umbral	0.605	0.85	Cumple meta con ligera mejora


Conclusión:
El Random Forest con class_weight='balanced' logra el mejor balance entre precisión, recall y simplicidad (F1 ≈ 0.63, AUC-ROC ≈ 0.86).
El ajuste de umbral resultó clave para optimizar F1 y mejorar la detección de clientes que abandonarían el banco.


---

Requisitos

Archivo: requirements.txt

pandas
numpy
scikit-learn
imbalanced-learn
matplotlib
seaborn

Instalación:

pip install -r requirements.txt


---

Ejecución del proyecto

1. Clonar el repositorio:

git clone https://github.com/<tu_usuario>/beta_bank_churn.git
cd beta_bank_churn


2. Instalar dependencias:

pip install -r requirements.txt


3. Abrir el notebook:

jupyter notebook notebook/beta_bank_churn_model.ipynb


4. Ejecutar todas las celdas secuencialmente para reproducir el análisis y los resultados.




---

Conclusiones finales

Se cumplieron los objetivos del proyecto: F1 ≥ 0.59 y AUC-ROC alto.

Se aplicaron dos técnicas de equilibrio (class_weight y SMOTE), además del ajuste de umbral.

El Random Forest balanceado es el modelo más robusto y listo para producción o pruebas de negocio.



---

Licencia

Este proyecto se distribuye bajo la Licencia MIT.
Consulta el archivo LICENSE para más detalles.

MIT License

Copyright (c) 2025 Carlos [Tu Apellido]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


