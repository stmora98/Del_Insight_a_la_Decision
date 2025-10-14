# 🧠 AI Fabric Hackathon  

## 🎯 Objetivos del Hackathon

Al finalizar este hackathon, los participantes serán capaces de:

- Preparar, transformar y enriquecer datos financieros y aseguradores usando **Microsoft Fabric**, aplicando el modelo **medallion** para estructurar capas de valor analítico.  
- Ingestar datos desde sistemas core, fuentes externas y APIs mediante **pipelines, notebooks y conectores nativos de Fabric**.  
- Diseñar **modelos semánticos** robustos que faciliten el consumo de datos por analistas, auditores y sistemas de inteligencia.  
- Monitorear y optimizar el consumo de capacidad en **Fabric**, aplicando métricas clave para gobernanza operativa y eficiencia de recursos.  
- Construir **agentes de inteligencia artificial** con **AI Foundry** para análisis predictivo, detección de fraude y generación de insights financieros.  
- Orquestar flujos multi-agente y procesos de datos con **pipelines y triggers**, habilitando automatización inteligente en escenarios bancarios y de seguros.  
- Aplicar **controles de seguridad y gobernanza** de datos sensibles, configurando roles, permisos y políticas en workspaces de Fabric.  
- Integrar **Microsoft Purview** para trazabilidad, clasificación y cumplimiento normativo, fortaleciendo la gobernanza de datos en entornos regulados.  
- Visualizar **insights estratégicos** con **Power BI en Microsoft Fabric**, habilitando tableros interactivos para decisiones basadas en datos.  



# Agenda


| Día  | Actividad                                                                 | Tipo   |
|------|---------------------------------------------------------------------------|--------|
| Día 1 | Preparación de datos (estructuración, limpieza, perfilado)               | Reto   |
| Día 1 | Ingesta de datos desde fuentes internas y externas                      | Reto   |
| Día 1 | Transformación de datos con notebooks y pipelines                        | Reto   |
| Día 1 | Enriquecimiento de datos y creación de modelo semántico                  | Reto   |
| Día 1 | Fabric Metrics: monitoreo de capacidad, consumo y rendimiento            | Demo   |
| Día 1 | Round Table: Q&A con expertos y participantes                            | Reto   |
| Día 1 | Cierre y resumen del día                                                 | Cierre |
| Día 2 | Construcción de agente AI Foundry para análisis predictivo               | Reto   |
| Día 2 | Orquestación multi-agente con pipelines y triggers                       | Reto   |
| Día 2 | Seguridad en Fabric: roles, objetos, workspaces (opcional)               | Reto   |
| Día 2 | Integración con Microsoft Purview: linaje, clasificación, gobernanza     | Demo   |
| Día 2 | Sesión de valor: Q&A sobre adopción, impacto y próximos pasos            | Cierre |
| Día 2 | Cierre y entrega de reconocimientos                                      | Cierre |


# Arquitectura
![Arquitectura](https://github.com/stmora98/Del_Insight_a_la_Decision/blob/main/Architecture/Architecture.png)


## 🧩 00 - Parte 1: Cargar archivo CSV en Azure Cosmos DB

### 🚀 Paso 1: Crear la cuenta de Cosmos DB
1. Ve al **portal de Azure**.  
2. Crea un recurso → **Azure Cosmos DB for NoSQL**.  
3. Asigna nombre, grupo de recursos y región.  
4. Espera a que se aprovisione.  

### ⚙️ Paso 2: Crear base de datos y contenedor
1. En tu cuenta de Cosmos DB, ve a **Data Explorer**.  
2. Crea una nueva **base de datos** (ejemplo: `NombreDeLaBase`) y un **contenedor** (ejemplo: `NombreDelContenedor`).  
3. Define una **clave de partición** (ejemplo: `/claveParticion`).  
4. Habilita **TTL** si deseas limpieza automática.  

### 💾 Paso 3: Insertar JSON en Cosmos DB
1. Ve a **Data Explorer → Contenedor → Items → Upload Item**.  
2. Carga el archivo **JSON** generado.  
3. Verifica que los documentos estén visibles y bien estructurados.  

---

## ☁️ 01 - Parte 2: Preparar ingesta a Microsoft Fabric con Data Factory  

### Guía resumida para integrar datos en Microsoft Fabric usando Azure Data Factory  

### 🔧 Paso 1: Crear instancia de Azure Data Factory
- Accede al **portal de Azure** y selecciona **Crear un recurso → Data Factory**.  
- Asigna nombre, grupo de recursos y región.  

### 🔗 Paso 2: Crear Linked Services
- **Cosmos DB:** Crea un Linked Service con la clave de acceso.  
- **Fabric Lakehouse:** Configura el conector **OneLake** (token de acceso o conexión directa).  

### 🧠 Paso 3: Crear pipeline de ingesta
1. Crea un **pipeline** en **Data Factory Studio**.  
2. Añade actividad **Copy Data**:  
   - **Fuente:** Cosmos DB (selecciona el contenedor).  
   - **Destino:** Fabric Lakehouse (tabla Bronze).  
3. Mapea campos y transforma datos según sea necesario.  

### ✅ Paso 4: Ejecutar y validar
1. Ejecuta el pipeline.  
2. Verifica que los datos estén en la tabla **Bronze** de Microsoft Fabric.  
3. Usa **Notebooks Spark** para inspección y transformación adicional.  

---

### ✅ Resultado esperado
- El archivo CSV se carga como documentos **JSON en Cosmos DB**.  
- El pipeline **extrae y carga** datos en Microsoft Fabric.  
- Los datos quedan listos para **transformación en Silver** y **enriquecimiento en Gold**.  

---

## 🔄 02 – Transformación y unificación  

### 🎯 Objetivo:
Convertir un archivo **JSON** a **CSV** y unificar ambos conjuntos de datos para análisis y procesamiento posterior.  

### 🧭 Paso a paso
1. **Usar notebooks Spark** en Fabric para convertir el archivo JSON a formato CSV.  
   - Abre tu **notebook Spark en Microsoft Fabric**.  
   - Carga el archivo JSON y utiliza funciones de Spark para transformarlo y exportarlo como CSV.  

2. **Realizar una unión (join)** de los datasets utilizando el campo **ID de cliente**.  
   - Importa ambos datasets (el original y el convertido) en el notebook.  
   - Utiliza el campo **ID de cliente** como clave para realizar la unión y obtener un solo conjunto de datos.  

3. **Guardar el dataset unificado en la capa Silver.**  
   - Una vez completada la unificación, guarda el resultado en la capa Silver de Fabric para futuras transformaciones y enriquecimiento.  

> Al finalizar estos pasos, tendrás los datos preparados y listos para procesos avanzados en la capa Gold, asegurando **calidad y consistencia en la información**.  

---

## 🧹 003 - Reto 3: Limpieza y enriquecimiento  

### 🎯 Objetivo:
Limpiar los datos, enriquecer con nuevas columnas y crear un modelo semántico.  

**Pasos:**
- Eliminar duplicados.  
- Normalizar nombres de país.  
- Calcular métricas:  
  - Total gastado  
  - Frecuencia  
  - País más frecuente  
- Crear **modelo semántico** en la capa Gold utilizando **Power BI o Semantic Model en Fabric**.  

---

## 🤖 004 - Reto 4: Data Agent en Fabric  

### 🎯 Objetivo:
Crear un agente que responda preguntas sobre los datos.  

**Pasos:**
1. Crear un **Data Agent** en Fabric.  
2. Conectarlo al **modelo semántico**.  
3. Probar el funcionamiento realizando preguntas como:  
   - “¿Cuál es el cliente más frecuente en México?”  

---

## 🧬 005 - Reto 5: Azure AI Foundry + LLMs  

### 🎯 Objetivo:
Aplicar **IA generativa** sobre datos enriquecidos para extraer valor y generar nuevos conocimientos a partir de la información disponible.  

### 🧩 Subretos:

#### 🧾 Resumen de compras por cliente
**Prompt:**  
> “Resume el comportamiento de compra del cliente X.”

#### 🏷️ Clasificación de clientes
**Prompt:**  
> “Clasifica este cliente como alto valor, frecuente u ocasional.”

#### 📰 Narrativas automáticas
**Prompt:**  
> “Genera un reporte mensual por país con insights narrativos.”
```markdown
