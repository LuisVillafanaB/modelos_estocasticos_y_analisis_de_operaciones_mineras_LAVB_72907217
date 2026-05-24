# Análisis inicial de una base de datos minera usando Python

## 1. Descripción del proyecto

Este proyecto desarrolla un análisis exploratorio inicial de una base de datos minera denominada `bd_posgrado_2026.csv`, utilizando Python en Jupyter Notebook. El análisis permite aplicar conceptos básicos de programación, tales como tipos de datos, operadores básicos, condicionales, bucles, funciones y uso de librerías.

La base de datos contiene información espacial, geoquímica y litológica, relacionada con muestras mineras.

## 2. Base de datos utilizada

El archivo utilizado fue:

`bd_posgrado_2026.csv`

La base de datos contiene las siguientes columnas:

| Variable | Descripción |
|---|---|
| X | Coordenada espacial X |
| Y | Coordenada espacial Y |
| Z | Elevación o coordenada vertical |
| P | Contenido de fósforo |
| Al | Contenido de aluminio |
| Rocktype | Tipo de roca |

## 3. Objetivo del análisis

Aplicar herramientas básicas de Python para realizar un análisis inicial de las variables químicas `P` y `Al`, identificar sus estadísticos principales, clasificarlas mediante percentiles y generar gráficos exploratorios.

## 4. Librerías utilizadas

En el análisis se utilizaron las siguientes librerías:

- `pandas`: para cargar, organizar y analizar la base de datos.
- `numpy`: para realizar cálculos numéricos.
- `matplotlib`: para elaborar gráficos básicos.

## 5. Procedimiento desarrollado

### 5.1 Carga de la base de datos

Se cargó la base de datos `bd_posgrado_2026.csv` en Jupyter Notebook usando la librería `pandas`.

```python
df = pd.read_csv("bd_posgrado_2026.csv")
df.head()
