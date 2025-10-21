# 🧼 **Parte 1: Limpieza de datos**

- **Eliminar duplicados:** Revisa el conjunto de datos y elimina las filas que estén repetidas para evitar inconsistencias.  
- **Normalizar nombres de país:** Unifica los nombres de los países utilizando un mismo criterio de escritura y formato.  
- **Convertir fechas al formato estándar:** Asegúrate de que todas las fechas sigan el formato **DD/MM/AAAA**.  
- **Eliminar registros nulos o incompletos:** Descarta las filas que contengan datos faltantes o incompletos para mantener la calidad del análisis.

## 🧪 **Código**

```python
# Leer dataset unificado desde Bronze
df = spark.read.csv("Files/dataset_unificado.csv", header=True, inferSchema=True)

# Eliminar duplicados
df_clean = df.dropDuplicates()

# Normalizar nombres de país
from pyspark.sql.functions import trim, upper

df_clean = df_clean.withColumn("pais", upper(trim(df_clean["pais"])))

# Convertir fechas al formato estándar
from pyspark.sql.functions import to_date

df_clean = df_clean.withColumn("fecha", to_date(df_clean["fecha"], "yyyy-MM-dd"))

# Eliminar registros con campos nulos críticos
df_clean = df_clean.dropna(subset=["customerId", "monto", "fecha"])

# Mostrar resultado limpio
display(df_clean)
```

# 📈 **Parte 2: Enriquecimiento de datos**

- **Métricas derivadas por cliente**
- **Total gastado:** Suma total de las compras por cliente.
- **Frecuencia de compra:** Número de compras por cliente en el periodo.
- **País más frecuente:** País desde el que el cliente compra con mayor frecuencia.

## 🛠️ **Código**

```Python
from pyspark.sql.functions import sum, count, col, first, desc

# Total gastado y frecuencia
df_metrics = df_clean.groupBy("customerId").agg(
    sum("monto").alias("total_gastado"),
    count("fecha").alias("frecuencia_compra"),
    first("pais").alias("pais_principal")  # simplificado, se puede mejorar con mode()
)

# Unir con datos demográficos
df_final = df_metrics.join(
    df_clean.select("customerId", "edad", "segmento").dropDuplicates(),
    on="customerId",
    how="left"
)

# Guardar en capa Silver
df_final.write.mode("overwrite").csv("Lakehouse/Silver/dataset_enriquecido.csv", header=True)

# Mostrar resultado enriquecido
display(df_final)
```

# 🏆 **Parte 3: Crear modelo semántico en capa Gold**

- **Crear tabla Gold desde archivo enriquecido:** Genera una tabla en la capa Gold utilizando el archivo ya enriquecido, asegurando que contiene solo los datos procesados y limpios.  
- **Definir medidas y dimensiones:** Establece claramente las medidas (métricas cuantitativas) y dimensiones (atributos descriptivos) que formarán parte del modelo semántico.  
- **Publicar modelo para Power BI o Data Agent:** Publica el modelo semántico creado para que esté disponible y pueda ser consultado desde Power BI o Data Agent según las necesidades del negocio.

## 🛠️ **Código**
```python
# Leer desde Silver
df_gold = spark.read.csv("Lakehouse/Silver/dataset_enriquecido.csv", header=True, inferSchema=True)

# Guardar como tabla Gold
df_gold.write.mode("overwrite").saveAsTable("Gold.ClienteAnalitico")

# Verificar tabla
spark.sql("SELECT * FROM Gold.ClienteAnalitico LIMIT 10").show()
```

## Resultado esperado
- Datos limpios y enriquecidos listos en la capa Silver.
- Tabla semántica en la capa Gold con métricas por cliente.
