# Analisis-de-tendencias-financieras-en-bolsa-
Creación de modelo que evalúa si el precio de una acción en especificó bajará o subirá
_________________________________________________________________________________
# 📈 Quantitative Stock Direction Predictor (Machine Learning & Time Series)

## 📌 Descripción del Proyecto
Este proyecto implementa un **pipeline completo de Machine Learning** aplicado a series temporales financieras. El objetivo principal es predecir la dirección del precio de cierre diario (clasificación binaria: si el precio subirá o bajará en la siguiente sesión de mercado) utilizando indicadores técnicos e ingeniería de características.

Para evaluar el comportamiento en distintas industrias y geografías, el análisis compara dos activos clave:
1. **NFLX (Netflix):** Un gigante tecnológico global de alta liquidez.
2. **HERDEZ.MX (Grupo Herdez):** Una empresa líder de consumo masivo y alimentos en la Bolsa Mexicana de Valores (BMV).

---

## 🛠️ Stack Tecnológico y Librerías
* **Python** como lenguaje principal de desarrollo.
* **yfinance** para la descarga automatizada de datos históricos de mercado.
* **Pandas & NumPy** para la manipulación de datos e ingeniería de características.
* **Scikit-Learn** para el preprocesamiento, modelos de *Bagging* (Random Forest) y métricas de evaluación.
* **XGBoost** para modelos de *Boosting* secuencial y optimización de rendimiento.
* **Google Colab** como entorno de experimentación y desarrollo.

---

## ⚙️ Metodología y Buenas Prácticas Aplicadas

1. **Ingeniería de Características Financieras:** 
   * Evitamos el uso de precios crudos para prevenir sesgos de escala temporal.
   * Se construyeron rezagos (*lags*), retornos porcentuales diarios (`Return_1d`) y Medias Móviles Simples (`SMA_10`, `SMA_50`) junto con ratios de momentum (`Price_vs_SMA10`).
2. **Validación Cronológica Estricta (*Time Series Split*):** 
   * Para evitar el error crítico de *data leakage* (fuga de datos del futuro), se descartó la validación cruzada aleatoria tradicional. Los modelos se entrenaron estrictamente con datos históricos pasados (80%) y se evaluaron en el futuro no visto (20%).
3. **Control de Overfitting e Iteración de Hiperparámetros:** 
   * Se realizaron barridos de profundidad (`max_depth`) mediante ciclos de iteración para identificar el punto de equilibrio entre subajuste y sobreajuste.
4. **Comparativa de Algoritmos:** 
   * Se evaluó el desempeño entre modelos basados en *Bagging* (Random Forest) y *Boosting* (XGBoost), logrando mejoras incrementales en la precisión de prueba.

---

## 📊 Resultados Clave

* **La realidad de los mercados financieros diarios:** Predecir el movimiento diario de acciones altamente líquidas como Netflix se acerca teóricamente a una caminata aleatoria, obteniendo precisiones cercanas a la línea base en modelos iniciales.
* **Efecto de la industria:** En activos con dinámicas locales o de menor volatilidad ruidosa (como Grupo Herdez), los modelos estructurados lograron capturar inercias de corto plazo, alcanzando hasta un **58% de precisión (Accuracy)** utilizando **XGBoost** con optimización de profundidad y tasas de aprendizaje graduales.
* **Importancia de Variables:** Se identificó que las métricas de *momentum* a corto plazo (relación precio vs. media móvil) concentran el mayor peso predictivo en los árboles de decisión.

---

## 🚀 Cómo Ejecutar el Proyecto

1. Clona este repositorio en tu computadora o ábrelo directamente en Google Colab.
2. Asegúrate de tener instaladas las librerías necesarias:
   ```bash
   pip install yfinance pandas numpy scikit-learn xgboost matplotlib
