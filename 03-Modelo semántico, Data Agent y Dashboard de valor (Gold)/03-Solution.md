# **Reto 3 – Modelo semántico, Data Agent y Dashboard de valor (Gold) 💎📊**

## **Guía paso a paso para la creación de soluciones en Power BI ⚙️**

### **Objetivo 🎯**
Crear un **modelo semántico**, un **Data Agent** y un **dashboard** sencillo en **Power BI**.

---

## **Narrativa contextual y pasos sugeridos 🧭**

### **Contexto 🏢**
Contoso quiere habilitar análisis de negocio sobre datos confiables.  
Tu equipo debe construir un **modelo semántico**, crear un **Data Agent** y diseñar un **dashboard** simple pero útil.

### **Objetivo del reto 🎯**
Diseñar el modelo semántico en **Gold**, crear un **Data Agent** conectado a ese modelo y construir un **dashboard** que entregue **valor al negocio**.

---

## **Fuentes de referencia 📚**
- [Modelos semánticos de Power BI - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/power-bi/)
- [Actualizar un modelo semántico mediante canalizaciones de datos (versión preliminar) - Power BI | Microsoft Learn](https://learn.microsoft.com/power-bi/connect-data/service-dataflows-semantic-models)

---

## **Pasos sugeridos 🪜**

1. Crear **tabla Gold** con agregaciones y relaciones clave.  
2. **Definir relaciones** si hay múltiples tablas.  
   - Ejemplo: si existe una tabla de clientes o transacciones, crear relaciones por `productID`.  
3. **Diseñar el modelo semántico** (medidas, dimensiones).  
   - Asegurarse de incluir medidas como:  
     - `valor_comercial_total = SUM(valor_comercial)`  
     - `productos_disponibles = COUNTIF(availability = "In Stock")`  
4. **Validar preguntas comunes** en **Copilot** o **Power BI** para asegurar que el modelo responde correctamente.  
5. Crear un **Data Agent en Fabric** conectado al modelo.  
6. **Diseñar un dashboard** en Power BI con visualizaciones como:  
   - **Score promedio por segmento (financiero)**.  
   - **Productos más vendidos y tasa de devolución (retail)**.  
   - **Tendencias semanales o mensuales**.  
7. **Publicar el dashboard** en el workspace.  

---

## **Reto 3 – Industria Retail (Set: score_productos_gold) 🛍️**

### **1️⃣ En Power BI, crea un modelo semántico**
Incluir las dimensiones siguientes:
- `Brand`
- `Category`
- `perfil_producto`
- `availability`

---

## **Medidas DAX sugeridas 🧮**

| **Medida** | **Fórmula DAX sugerida** |
|-------------|---------------------------|
| `Valor_Comercial_Total` | `SUM(score_productos_gold[valor_comercial])` |
| `Productos_Disponibles` | `COUNTROWS(FILTER(score_productos_gold, score_productos_gold[Availability] = "InStock"))` |
| `Cantidad_Productos` | `COUNT(score_productos_gold[ProductoID])` |
| `Tasa_Devolucion` | `AVERAGE(score_productos_gold[Devolucion_Binaria])` |

---

## **Validación de preguntas comunes 💬**

Prueba estas preguntas en **Copilot** o **Power BI** para validar el modelo:

- “¿Qué categoría tiene más productos valiosos?”  
- “¿Cuál es el valor comercial total por marca?”  
- “¿Cuántos productos están disponibles?”  
- “¿Qué perfil de producto genera más ingresos?”

---

## **Crea un dashboard llamado con las siguientes visualizaciones 📊**

| **Visualización** | **Tipo** | **Fuente** |
|--------------------|----------|-------------|
| 📈 Valor comercial por categoría | Gráfico de columnas | `score_productos_gold` |
| 📉 Tendencia mensual de disponibilidad | Línea temporal | `score_productos_gold` |
| 🛒 Productos más vendidos por marca | Gráfico de barras | Relación con transacciones (si aplica) |
| 🔄 Tasa de devolución por perfil | Gráfico circular | `score_productos_gold` |
| 📦 Segmento de producto vs volumen | Tabla + tarjeta | `score_productos_gold` |

---

## **Publicar el dashboard en el workspace 🚀**

- Publica el dashboard en el **workspace correspondiente**.  
- Asegúrate de que el **Data Agent** esté activo para responder preguntas desde **Copilot** o **Power BI**.  
