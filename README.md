# Proyecto Properati – Parte 2: precios de propiedades en CABA con datos de seguridad

Trabajo de la Diplomatura en Data Science de Acámica. Continúa la [Parte 1](https://github.com/FreeAlejandria/Acamica-Proyecto_Properati_Part1) e intenta mejorar su mejor modelo (XGBoost) agregando información de seguridad por barrio, bajo la hipótesis de que la inseguridad influye en el valor de las propiedades.

> En el notebook la Parte 1 se menciona como “proyecto 2”.

📄 **Versión para leer sin ejecutar nada:** [`docs/Proyecto_Properati_Part2_V1.pdf`](docs/Proyecto_Properati_Part2_V1.pdf) (notebook completo con portada, resumen e índice).

## Qué incluye

1. **EDA del dataset de delitos 2019** del Gobierno de la Ciudad de Buenos Aires (117.661 registros): tipos de delito, distribución por barrio, nulos.
2. **Unificación de datasets:** normalización de nombres de barrios y unión con el dataset limpio de la Parte 1; conteo de delitos por barrio y tipo.
3. **Preprocesamiento:** escalado y one-hot encoding de barrio, tipo de propiedad y tipo de delito; se trabaja en paralelo con una versión normalizada y otra sin normalizar.
4. **XGBoost con `GridSearchCV`:** comparación con y sin atributos de seguridad. Con datos normalizados el RMSE de test bajó de 0,498 a 0,337 (**mejora del 32%**), sin señales de sobreajuste.
5. **PCA (7 componentes):** redujo el tiempo de entrenamiento a menos de la mitad, pero empeoró el RMSE de test (0,337 → 0,445) y aumentó la brecha Train/Test.

## Archivos

| Archivo | Descripción |
|---|---|
| `Proyecto_Properati_Part2.ipynb` | Notebook completo con código, salidas y conclusiones. |
| `docs/Proyecto_Properati_Part2_V1.pdf` | Versión PDF del notebook, lista para leer o compartir. |
| `delitos_2019.csv` | Delitos registrados en CABA en 2019 (datos abiertos GCBA). |
| `new_properati_Capital1_All_sin_bedrooms_clean.csv` | Dataset limpio de propiedades que sale de la Parte 1. |
| `requirements.txt` | Versiones de librerías compatibles con el código. |

## Cómo ejecutarlo

Todos los datasets necesarios están en este repositorio. El notebook se escribió con Python 3.7, scikit-learn 0.24 y XGBoost 1.4; conviene usar un entorno con las versiones de `requirements.txt`:

```bash
python -m venv .venv && source .venv/bin/activate   # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook Proyecto_Properati_Part2.ipynb
```

Cada búsqueda de hiperparámetros con `GridSearchCV` sobre XGBoost tarda bastante (en la corrida original, entre 40 minutos y más de 3 horas según el set de atributos).

## Nota sobre las salidas

La versión anterior del notebook en este repositorio se había guardado con la ejecución interrumpida a mitad del entrenamiento, por lo que faltaban todos los resultados de los modelos. Se restauraron las salidas de la corrida completa original (recuperadas del historial del repositorio) manteniendo las rutas relativas a los datasets.
