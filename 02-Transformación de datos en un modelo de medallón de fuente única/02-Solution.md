# 🚀 **Reto 2: Guía de Conversión y Unificación**

## 🧩 **Convertir archivo JSON a CSV: Código**

```python
import json
import csv

# Ruta de entrada JSON
json_path = r"C:\Users\msalasrobles\Documents\compras_clientes.json"
# Ruta de salida CSV
csv_path = r"C:\Users\msalasrobles\Documents\compras_clientes_convertido.csv"

# Leer JSON
with open(json_path, encoding='utf-8') as f:
    data = json.load(f)

# Extraer encabezados desde el primer objeto
headers = list(data[0].keys())

# Escribir CSV
with open(csv_path, mode='w', newline='', encoding='utf-8') as f:
    writer = csv.DictWriter(f, fieldnames=headers)
    writer.writeheader()
    writer.writerows(data)

print(f"Archivo CSV generado en: {csv_path}")
```

## 🗃️ **Unificar Archivos CSV**

```python
import pandas as pd

# Rutas de los archivos
csv1 = r"path\clientes.csv"
csv2 = r"path\ventas.csv"
output_path = r"C:\Users\msalasrobles\Documents\dataset_unificado.csv"

# Leer ambos CSV como DataFrames
df_compras = pd.read_csv(csv1)
df_clientes = pd.read_csv(csv2)

# Unificar por customerId
df_unificado = pd.merge(df_compras, df_clientes, on='customerId', how='inner')

# Guardar resultado
df_unificado.to_csv(output_path, index=False, encoding='utf-8')

print(f"Dataset unificado guardado en: {output_path}")
```

## ✅ **Resultado esperado**
- Un archivo CSV llamado  con columnas combinadas de compras y datos demográficos.
- Listo para cargar en la capa Silver de Fabric para limpieza y enriquecimiento en el Reto 3.
