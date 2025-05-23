
# Proyecto de Ingeniería y Ciencia de Datos II 

Este proyecto ha sido desarrollado como parte de la asignatura **Ingeniería y Ciencia de Datos II** del **Máster Universitario en Ingeniería Informática** de la **Universidad de Málaga**, por el estudiante **Víctor Rodríguez Machiquez**.

Su objetivo principal es aplicar técnicas modernas de procesamiento, análisis y visualización de datos sobre un conjunto real de archivos JSON provenientes de la plataforma [VirusTotal](https://www.virustotal.com/). Estos archivos contienen reportes detallados generados por múltiples motores antivirus tras analizar muestras de archivos potencialmente maliciosos.

---

## 📂 Estructura del Proyecto

```
ProyectoCD2_VictorERM/
├── data/                     # Archivos JSON originales de VirusTotal
├── env/                      # Entorno virtual de Python
├── notebooks/                # Notebook principal con el flujo completo
│   └── proyecto2cd2.ipynb
├── outputs/                  # Gráficas y resultados generados
├── scripts/                  # Scripts auxiliares (opcional)
├── README.md                 # Este archivo
└── requirements.txt          # Dependencias necesarias
```

---

## 🔍 Fases del Análisis

El proyecto se organiza en **7 fases secuenciales**, aplicando buenas prácticas en ingeniería de datos:

1. **Introducción del Proyecto**  
   Contexto académico y objetivo general del análisis.

2. **Preprocesamiento de Datos**  
   Lectura de archivos `.json`, validación y transformación en tres `DataFrames`:
   - `df1_info`: Información general por archivo (`vhash`, país, reputación, fecha…)
   - `df2_scans`: Resultados por motor antivirus y archivo
   - `df3_limpio`: Unión enriquecida de `df1` y `df2`

3. **Limpieza de Datos**  
   Conversión de fechas, detección de duplicados, comprobación de nulos y tipos de datos.

4. **Almacenamiento en MongoDB Atlas**  
   Inserción de los tres `DataFrames` como colecciones independientes para facilitar distintos tipos de análisis:
   - `df1_info`
   - `df2_scans`
   - `df3_limpio` (colección principal para exploración y visualización)

5. **Exploración de Datos**  
   Consultas `find()` y `aggregate()` ejecutadas sobre MongoDB para detectar patrones:
   - Motores más activos
   - Países con más envíos
   - Distribución temporal de muestras

6. **Visualización de Resultados**  
   Representaciones gráficas con `matplotlib` para mostrar:
   - Top 10 antivirus por detecciones
   - Top 10 países remitentes
   - Evolución temporal de escaneos

7. **Optimización con Índices en MongoDB**  
   Mejora del rendimiento mediante la creación de índices sobre campos clave (`vhash`, `engine`, `detected`, `submitter_country`, `first_seen`).

---

## ⚙️ Dependencias

Instalación recomendada desde entorno virtual:

```bash
pip install -r requirements.txt
```

Bibliotecas utilizadas:
- `pandas`
- `matplotlib`
- `pymongo`
- `dnspython`

---

## ☁️ Conexión a MongoDB Atlas

Los datos se almacenan en una base de datos remota de MongoDB Atlas. El análisis y las visualizaciones se realizan directamente consultando las colecciones a través de `pymongo`.

> Es necesario tener acceso al clúster remoto indicado en las credenciales para ejecutar las fases 4 a 7.

---

## ✅ Resultados

Este proyecto demuestra un flujo completo de trabajo en ciencia de datos sobre archivos semiestructurados: desde la ingesta y limpieza hasta el análisis visual y la optimización del almacenamiento.

---

## ▶️ Cómo ejecutar este notebook en Google Colab
---

Para poder ejecutar este notebook en Google Colab correctamente, sigue estos pasos iniciales para preparar el entorno:

### 🗂️ 1. Montar Google Drive

Esto permite acceder a los archivos JSON desde tu unidad de Google Drive:

```python
from google.colab import drive
drive.mount('/content/drive')
````

### 📦 2. Instalar librerías necesarias

Colab no incluye por defecto algunas de las bibliotecas usadas. Ejecuta esto al inicio:

```python
!pip install pymongo dnspython pandas matplotlib seaborn
```

### 📁 3. Configurar la ruta de acceso a los archivos

Asegúrate de que la carpeta `data` con los archivos `.json` esté ubicada dentro de:

```
/content/drive/MyDrive/Colab Notebooks/data
```

Y define la ruta en una variable para usarla en el notebook:

```python
carpeta_data = "/content/drive/MyDrive/Colab Notebooks/data"
```
