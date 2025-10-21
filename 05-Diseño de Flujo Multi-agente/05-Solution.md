# 🤖 **Guía de Preparación del Entorno para Azure AI Foundry**

---

## ⚙️ **Parte 1: Preparación del entorno**

### ✅ **Requisitos previos**

- Tener acceso a **Azure AI Studio**  
- Haber creado un **proyecto en Azure AI Foundry**  
- Contar con el **dataset enriquecido** disponible en formato CSV o como tabla en **Fabric**

---

### 🔹 **Paso 1: Crear un proyecto en Azure AI Foundry**

1. Accede a **Azure AI Studio → Foundry → Crear nuevo proyecto**  
2. Asigna un nombre (ejemplo: `Proyecto_ClientesAI`)  
3. Selecciona el tipo de proyecto: **Prompt Flow**  
4. Define el objetivo:  
   > “Generar insights narrativos y clasificaciones de clientes”

---

### 🔹 **Paso 2: Subir el dataset enriquecido**

1. En el proyecto, navega a **Data Assets**.  
2. Carga el archivo desde **Fabric** o desde tu equipo local.  
3. Verifica que los campos clave estén presentes.  

**Campos requeridos:**
- `customerId`
- `total_gastado`
- `frecuencia_compra`
- `pais`
- `fecha`

📂 **Ejemplo:**  
Carga el archivo **dataset_enriquecido.csv** desde Fabric o localmente.

---

## 🧠 **Parte 2: Diseño de los flujos de prompts**

🔹 **Reto 1: Generación de resúmenes de compra**

**Prompt base:**

Dado el siguiente cliente:  
- ID: {customerId}  
- Total gastado: {total_gastado}  
- Frecuencia de compra: {frecuencia_compra}  
- País principal: {pais}  

Genera un resumen breve del comportamiento de compra.  

**Salida esperada:**

> “El cliente C001 ha gastado $1,250 en 8 compras, siendo México su país principal de actividad.”

---

🔹 **Reto 2: Clasificación de clientes**

**Prompt base:**  

Clasifica al siguiente cliente según su comportamiento:  
- Total gastado: {total_gastado}  
- Frecuencia de compra: {frecuencia_compra}  

**Categorías posibles:**  
- Alto valor  
- Frecuente  
- Ocasional  

Justifica tu clasificación.  

**Salida esperada:**

> “Cliente C002 es clasificado como ‘Frecuente’ por realizar 12 compras con un gasto moderado de $980.”

---

🔹 **Reto 3: Generación de insights narrativos**

**Prompt base:**  

Genera un reporte narrativo mensual por país. Datos:  
- País: {pais}  
- Mes: {mes}  
- Total de compras: {total_compras}  
- Monto total: {monto_total}  

**Ejemplo de salida:**  
‘En septiembre, los clientes de México realizaron X compras por un total de Y.’  

**Salida esperada:**

> “En octubre, los clientes de Colombia realizaron 320 compras por un total de $45,000.”

---

## ⚙️ **Parte 3: Implementación en Prompt Flow**

**Paso a paso**

1. Crea un nuevo Flow por reto (puedes duplicar y adaptar).  
2. Usa el componente Data Input para conectar el CSV.  
3. Usa el componente LLM Prompt para definir el prompt.  
4. Usa el componente Output Parser para estructurar la respuesta.  
5. Ejecuta el Flow y valida los resultados.  

---

## ✅ **Parte 4: Resultado esperado**

- Tres flujos funcionales en Azure AI Foundry que aplican LLMs sobre datos enriquecidos.  
- Prompts reutilizables y adaptables para otros casos de negocio.  
- Base sólida para extender hacia recomendaciones, predicciones o generación de contenido personalizado.






