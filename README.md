# Análisis exploratorio en Python - Luis Alberto Villafana Bermúdez

## 1. Descripción de las bases de datos

Este proyecto desarrolla un análisis exploratorio inicial de una base de datos minera denominada `bd.csv`, utilizando Python en Jupyter Notebook. El análisis permite aplicar conceptos básicos de programación, tales como tipos de datos, operadores básicos, condicionales, bucles, funciones y uso de librerías.

## 2. Base de datos utilizada

El archivo utilizado fue:

`bd.csv`

La base de datos contiene las siguientes columnas:

| Variable | Descripción                     |
| -------- | ------------------------------- |
| X        | Coordenada espacial X           |
| Y        | Coordenada espacial Y           |
| Z        | Elevación o coordenada vertical |
| Fe       | Contenido de hierro             |
| Si       | Contenido de silicio            |
| P        | Contenido de fósforo            |
| Al       | Contenido de aluminio           |
| Mn       | Contenido de manganeso          |
| Rocktype | Tipo de roca                    |

## 3. Objetivo del análisis

Aplicar herramientas básicas de Python para realizar un análisis inicial de las variables químicas `Fe` y `P`, identificar sus estadísticos principales, clasificarlas mediante percentiles y generar gráficos exploratorios.

## 4. Librerías utilizadas

En el análisis se utilizaron las siguientes librerías:

- `pandas`: para cargar, organizar y analizar la base de datos.
- `numpy`: para realizar cálculos numéricos.
- `matplotlib`: para elaborar gráficos básicos.

## 5. Procedimiento desarrollado

### 5.1 Carga de la base de datos

Se cargó la base de datos `bd.csv` en Jupyter Notebook usando la librería `pandas`.

```python
lv = pd.read_csv("bd.csv")
lv.head()
```

### 5.2 Se aplicó operadores básicos para calcular lo siguiente:

- Promedio de Fe, Si, P, Al y Mn
- Valor máximo y mínimo de Fe

  # Variables químicas a analizar

  variable_quimica_evaluar = ["Fe"]

  # Estadísticos básicos

  lv[variable_quimica_evaluar].describe().T

  # Estadísticos específicos

  estadisticos = lv[variable_quimica_evaluar].agg(["mean", "min", "max", "std", "median"])

  estadisticos

- Diferencia entre el valor máximo y mínimo de Fe

  # Diferencia entre valor máximo y mínimo de Fe

  diferencia_Fe = lv["Fe"].max() - lv["Fe"].min()

  print("Diferencia entre máximo y mínimo de Fe:", diferencia_Fe)

### 5.3 Se utilizó condicionales para clasificar el contenido de Fe:

  # Calcular percentiles 33 y 66 para Fe
  Fe33_Fe = lv["Fe"].quantile(0.33)
  Fe66_Fe = lv["Fe"].quantile(0.66)

  print("Percentil 33 de Fe:", Fe33_Fe)
  print("Percentil 66 de Fe:", Fe66_Fe)

  # Función condicional para clasificar Fe
  def clasificar_Fe(valor):
      if valor < Fe33_Fe:
          return "Fe bajo"
      elif valor <= Fe66_Fe:
          return "Fe medio"
      else:
          return "Fe alto"

  # Crear nueva columna con la clasificación de Fe
  lv["Clasificacion_Fe"] = lv["Fe"].apply(clasificar_Fe)

  # Mostrar resultados
  lv[["Fe", "Clasificacion_Fe"]].head()

### 5.4 Se creó una función en Python para recibir el nombre de una variable química y me devuelva su resumen estadístico básico:

  def resumen_estadistico(variable):
      resumen = {
          "Variable": variable,
          "Promedio": lv[variable].mean(),
          "Mínimo": lv[variable].min(),
          "Máximo": lv[variable].max(),
          "Mediana": lv[variable].median(),
          "Desviación estándar": lv[variable].std(),
          "Percentil 33": lv[variable].quantile(0.33),
          "Percentil 66": lv[variable].quantile(0.66)
      }
      return pd.DataFrame([resumen])

### 5.5 Se elaboró dos gráficos:

  - Histograma de Fe
      plt.figure()
      plt.hist(lv["Fe"], bins=20, edgecolor="black")
      plt.title("Histograma del contenido de Fe")
      plt.xlabel("Contenido de Fe")
      plt.ylabel("Frecuencia")
      plt.savefig('histograma.svg')
      plt.show()

  -Gráfico de dispersión entre Fe y Si u otro elemento
      plt.figure()
      plt.scatter(lv["Fe"], lv["P"], alpha=0.7, edgecolor="black")
      plt.title("Gráfico de dispersión entre Fe y P")
      plt.xlabel("Fe")
      plt.ylabel("P")
      plt.savefig('grafico_dispersion.svg')
      plt.show()
