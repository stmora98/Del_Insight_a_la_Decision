# 🧩 **Reto 1: Ingesta de Datos en Microsoft Fabric con Data Factory**

> **Objetivo:** Preparar e integrar datos desde Azure Cosmos DB hacia Microsoft Fabric utilizando Azure Data Factory.  
> Este proceso establece la base del flujo de datos desde la **capa Bronze** hasta las capas **Silver** y **Gold** para su análisis posterior.

---

## ⚙️ **Parte 1: Configuración de Azure Data Factory**

### 🔹 **Paso 1: Crear instancia de Azure Data Factory**
1. Accede al **Portal de Azure**.  
2. Selecciona **Crear un recurso → Data Factory**.  
3. Asigna:
   - Un **nombre** identificativo (ejemplo: `ADF-FabricIngesta`).
   - El **grupo de recursos** correspondiente.
   - La **región** más cercana a tu entorno de Fabric.

💡 *Consejo:* Mantén el nombre coherente con tus recursos de Fabric para facilitar la administración.

---

## 🔗 **Parte 2: Configurar Conexiones (Linked Services)**

### 🔸 **Cosmos DB**
- Crea un **Linked Service** con la clave de acceso proporcionada.  
- Define la conexión hacia el **contenedor de datos** donde se almacenan los documentos JSON.

### 🔸 **Fabric Lakehouse**
- Configura el conector de **OneLake** (requiere token de acceso o conexión directa desde Fabric).  
- Verifica la autenticación y permisos para escritura en la tabla destino.

---

## 🚀 **Parte 3: Crear el Pipeline de Ingesta**

### 🧱 **Pasos detallados**
1. Abre **Azure Data Factory Studio**.  
2. Crea un **nuevo pipeline** y asígnale un nombre descriptivo (ejemplo: `Pipeline_Ingesta_Cosmos_to_Fabric`).  
3. Agrega una actividad **Copy Data**.  

   **Configuración:**
   - **Fuente:** Cosmos DB → selecciona el contenedor correspondiente.  
   - **Destino:** Fabric Lakehouse → elige la tabla en la **capa Bronze**.  
   - **Transformaciones:** mapea los campos y aplica ajustes como:
     - Conversión de fechas a formato estándar.
     - Normalización de campos y tipos de datos.

💡 *Tip:* Puedes agregar un paso de validación para asegurar que el esquema coincida con el esperado en Fabric.

---

## 🧪 **Parte 4: Ejecución y Validación**

1. Ejecuta el pipeline creado desde **Data Factory Studio**.  
2. Verifica en **Microsoft Fabric** que los datos se encuentren disponibles en la tabla **Bronze**.  
3. (Opcional) Usa **Notebooks Spark** dentro de Fabric para:
   - Visualizar los datos.  
   - Validar el formato y consistencia.  
   - Aplicar transformaciones previas al enriquecimiento.

---

## ✅ **Resultado Esperado**

Al finalizar este reto, deberías obtener:

| Elemento | Resultado |
|-----------|------------|
| **Origen de datos** | Archivo CSV cargado como documentos JSON en **Cosmos DB** |
| **Pipeline** | Configurado y ejecutado correctamente en **Azure Data Factory** |
| **Destino** | Datos disponibles en **Microsoft Fabric (Capa Bronze)** |
| **Siguiente paso** | Los datos listos para transformación en **Capa Silver** y enriquecimiento en **Capa Gold** |

---

🎯 **Conclusión:**  
Con este flujo completado, ya dispones de un **pipeline automatizado** que conecta **Cosmos DB** con **Microsoft Fabric**, sentando las bases para los siguientes retos de transformación, enriquecimiento y análisis de datos.
