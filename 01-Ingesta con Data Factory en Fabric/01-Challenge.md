# 🚀 Reto 1 – Ingesta de datos desde Cosmos DB a Fabric (Bronze) + limpieza básica

## 🧭 Narrativa contextual
Contos necesita consolidar sus datos operativos en **Microsoft Fabric**.  
El equipo debe realizar la **ingesta desde Cosmos DB hacia la capa Bronze** y aplicar una **limpieza inicial de datos**.

## 🎯 Objetivo del reto
Ingerir los datos desde **Cosmos DB a Fabric** y aplicar una limpieza básica que incluya:
- Manejo de valores **nulos o vacíos**  
- Eliminación de **columnas innecesarias**  
- Normalización de **formatos básicos (fechas, texto, etc.)**

## ⚙️ Pasos sugeridos
1. **Crear un pipeline de ingesta** desde Cosmos DB hacia el Lakehouse Bronze.  
2. **Validar la carga de datos** y revisar la estructura resultante.  
3. Utilizar **notebooks** o **Dataflow Gen2** para realizar:
   - Eliminación de columnas irrelevantes  
   - Reemplazo o eliminación de valores nulos  
   - Normalización de formatos (fechas, texto, etc.)  
4. **Guardar la tabla limpia** en la capa **Bronze**.  

*Consejo:* asegúrate de documentar los pasos realizados y tomar capturas del resultado para evidenciar la transformación de los datos.
