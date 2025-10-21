# 🧩 Reto 0 – Preparación de los datos y configuración de la zona de aterrizaje en Fabric  

---

## 🌍 Narrativa contextual y pasos para la puesta en marcha  

### 📖 Contexto  

Contos ha cargado dos conjuntos de datos en formato **JSON**:  
- Uno **financiero**, que incluye información de **score crediticio**.  
- Otro de **retail**, con datos de **ventas y productos**.  

Estos archivos se encuentran almacenados en **Azure Cosmos DB**, y tu misión es **preparar el entorno de trabajo en Microsoft Fabric** para dar inicio al proceso de transformación de datos.  

---

### 🎯 Objetivo del reto  

Configurar correctamente la **zona de aterrizaje (landing zone)** en **Microsoft Fabric**, estableciendo la conexión con **Cosmos DB**, cargando los datos iniciales y definiendo la estructura de capas **Bronze**, **Silver** y **Gold**.  

---

### 🪜 Pasos sugeridos  

1. Crear un workspace en Microsoft Fabric para centralizar todos los recursos del proyecto.  
2. Configurar la conexión con Azure Cosmos DB, asegurando que las credenciales y permisos sean correctos.  
3. Explorar la estructura de los datos JSON, identificando las entidades principales, relaciones y campos clave relevantes.  
4. Crear una Lakehouse y dentro de ella definir la estructura de carpetas que representen las capas del modelo:  
   - **Bronze** → Datos crudos y originales.  
   - **Silver** → Datos limpios y transformados.  
   - **Gold** → Datos listos para análisis o reportes.  
5. Documentar la estrategia de flujo entre las capas, detallando cómo se moverán y transformarán los datos desde **Bronze → Silver → Gold**.  

---
 
*Al finalizar este reto tendrás lista la base del entorno de datos en Microsoft Fabric, con todos los componentes necesarios para avanzar en los siguientes desafíos.*  
