# Limpieza y preprocesamiento de House Prices

Actividad 3 · Estadística Aplicada · Maestría en Inteligencia Artificial
Universidad Politécnica Metropolitana de Hidalgo

## Objetivo

Construir un pipeline reproducible de limpieza y preprocesamiento de datos sobre el dataset **House Prices**, aplicando las diez técnicas solicitadas en la actividad (eliminación de duplicados, imputación, outliers, normalización/estandarización, conversión de tipos, codificación, escalado, corrección de errores tipográficos, discretización y feature engineering), dejando el conjunto listo para un análisis multivariante posterior.

## Dataset

- **Fuente:** [House Prices Dataset](https://www.kaggle.com/datasets/lespin/house-prices-dataset) en Kaggle, basado en *House Prices: Advanced Regression Techniques* (Dean De Cock, 2011).
- **Archivo usado:** `train.csv` — 1,460 viviendas de Ames, Iowa, descritas por 81 variables.
- **Variable objetivo:** `SalePrice` (precio de venta en dólares).
- Sin contar `Id` y `SalePrice`, quedan 79 predictores: 36 numéricos y 43 categóricos.

## Estructura del repositorio

```text
archive/             Datos originales de Kaggle (train.csv, test.csv, data_description.txt), sin modificar
notebooks/            Actividad_3_Limpieza_Datos.ipynb — notebook principal, ejecutable de inicio a fin
outputs/figures/      Figuras generadas por el notebook
outputs/tables/       Tablas (CSV) generadas por el notebook
```

## Técnicas aplicadas

1. Carga y diagnóstico inicial (tipos, faltantes, duplicados, estadísticos descriptivos).
2. Diccionario de variables construido a partir de `data_description.txt`.
3. Eliminación de duplicados exactos.
4. Imputación: mediana en numéricas, `Sin_dato` en categóricas.
5. Detección y tratamiento de atípicos con IQR (clipping superior en predictores; `SalePrice` y los ceros estructurales de `TotalBsmtSF` se conservan intactos).
6. Normalización (Min-Max) y estandarización (Z), con respaldo en NumPy/Pandas si scikit-learn no está disponible.
7. Conversión de tipos (`MSSubClass` a categoría, `MoSold`/`YrSold` a enteros compactos).
8. Codificación ordinal en escalas de calidad y One-Hot Encoding en el resto de categóricas nominales.
9. Escalado final de la matriz de predictores para modelado.
10. Revisión de errores tipográficos en variables categóricas.
11. Agrupación y discretización (edad de la vivienda, precio y calidad en cuartiles).
12. Feature engineering: `HouseAge`, `TotalSF`, `TotalBathrooms`, `TotalPorchSF`, `HasGarage`, `Remodeled`.

## Resultados destacados

- 7,829 celdas faltantes detectadas y reducidas a 0 tras la imputación; 0 duplicados exactos.
- La codificación amplía la matriz de 79 a 258 predictores (14 ordinales + 179 columnas One-Hot + numéricas).
- Mayor correlación con `SalePrice`: `TotalSF` (Spearman 0.820) y `TotalBathrooms` (0.704).
- `SalePrice` presenta sesgo hacia precios altos: media de USD 180,921.20 frente a una mediana de USD 163,000.00.

## Cómo ejecutar

Requisitos: Python 3.11+, `pandas`, `numpy`, `matplotlib`; opcionalmente `scikit-learn` y `seaborn` (el notebook usa una ruta de respaldo si no están instalados).

```bash
pip install pandas numpy matplotlib scikit-learn seaborn
jupyter notebook notebooks/Actividad_3_Limpieza_Datos.ipynb
```

El notebook se puede ejecutar de principio a fin sin pasos manuales adicionales; las figuras y tablas se regeneran en `outputs/`.

## Autores

- Luis David Gonzalez Romero
- Diego Alberto Ortega Carreto

Docente: Dr. Jaime Aguilar Ortiz · Periodo Septiembre–Diciembre 2026
