# 🚀 **Parte 1: Cargar archivo CSV en Azure Cosmos DB**

---

## 🧭 **Paso 1: Crear la cuenta de Cosmos DB**

1. Ve al **portal de Azure**.  
2. Crea un recurso → **Azure Cosmos DB for NoSQL**.  
3. Asigna **nombre**, **grupo de recursos** y **región**.  
4. Espera a que se **aprovisione** correctamente.

---

## 🗃️ **Paso 2: Crear base de datos y contenedor**

1. En tu cuenta de **Cosmos DB**, ve a **Data Explorer**.  
2. Crea una **nueva base de datos** (ejemplo: `NombreDeLaBase`) y un **contenedor** (ejemplo: `NombreDelContenedor`).  
3. Define una **clave de partición** (ejemplo: `/claveParticion`).  
4. Habilita **TTL** si deseas limpieza automática de datos.

---

## 💾 **Paso 3: Insertar JSON en Cosmos DB**

1. Ve a **Data Explorer → Contenedor → Items → Upload Item**.  
2. Carga el **archivo JSON generado**.  
3. Verifica que los **documentos estén visibles y bien estructurados**.

---

## ✅ **Resultado esperado**

Los datos del archivo CSV se encuentran correctamente cargados y estructurados en Azure Cosmos DB, listos para consultas y análisis posteriores.
