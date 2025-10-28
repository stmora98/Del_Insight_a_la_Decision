# Solución Reto 03 — Modelo Semántico, Data Agent y Dashboard de Valor (Capa Gold)

## Objetivo
Construir un ecosistema analítico completo en Microsoft Fabric que permita:
- Crear un modelo semántico Gold con datos curados
- Habilitar consultas en lenguaje natural vía Data Agent
- Diseñar visualizaciones efectivas en Power BI

## Requisitos previos
- Tablas Silver con datos limpios y transformados
- Workspace en Microsoft Fabric con permisos de administrador
- Power BI Desktop instalado (opcional, se puede usar Fabric web)

## 1. Preparar tablas Gold y relaciones

### 1.1 Crear tablas dimensionales
```sql
-- En Fabric Lakehouse, crear vista Gold de productos
CREATE OR REPLACE TABLE gold.dim_products AS
SELECT 
    productID,
    Brand,
    Category,
    perfil_producto,
    availability,
    Price as unit_price,
    Stock as current_stock
FROM silver.productos_clean;

-- Crear vista Gold de scores crediticios
CREATE OR REPLACE TABLE gold.dim_credit_scores AS
SELECT 
    customerID,
    score_normalizado,
    segmento_score,
    fecha_actualizacion
FROM silver.credit_scores_clean;
```

### 1.2 Crear tabla de hechos (ventas)
```sql
CREATE OR REPLACE TABLE gold.fact_sales AS
SELECT 
    s.saleID,
    s.productID,
    s.customerID,
    s.sale_date,
    s.quantity,
    s.unit_price,
    s.quantity * s.unit_price as valor_comercial,
    s.is_returned
FROM silver.sales_clean s;
```

## 2. Diseñar Modelo Semántico

### 2.1 Definir relaciones
En Power BI o Fabric, establecer:
- `fact_sales[productID]` → `dim_products[productID]` (muchos a uno)
- `fact_sales[customerID]` → `dim_credit_scores[customerID]` (muchos a uno)

### 2.2 Crear medidas DAX básicas
```dax
-- Medidas de ventas
Valor_Comercial_Total = SUM(fact_sales[valor_comercial])

Productos_Disponibles = 
CALCULATE(
    COUNTROWS(dim_products),
    dim_products[availability] = "In Stock"
)

-- Medidas de scores
Score_Promedio = AVERAGE(dim_credit_scores[score_normalizado])

-- KPIs derivados
Tasa_Devolución = 
DIVIDE(
    CALCULATE(COUNTROWS(fact_sales), fact_sales[is_returned] = TRUE),
    COUNTROWS(fact_sales)
)
```

### 2.3 Crear jerarquías útiles
```dax
-- Jerarquía de productos
Productos = 
HIERARCHY(
    dim_products[Brand],
    dim_products[Category],
    dim_products[productID]
)

-- Jerarquía temporal
Tiempo = 
HIERARCHY(
    fact_sales[sale_date],
    'Year',
    'Quarter',
    'Month'
)
```

## 3. Configurar Data Agent

### 3.1 Crear y conectar agente
1. En Fabric → New → Data Agent
2. Nombre: "Contoso_Retail_Agent"
3. Conectar al modelo semántico Gold
4. Habilitar preguntas frecuentes:
   ```json
   {
     "frequently_asked": [
       "¿Qué categoría tiene más productos valiosos?",
       "¿Cuál es el valor comercial total por marca?",
       "¿Cuántos productos están disponibles?",
       "¿Qué perfil de producto genera más ingresos?"
     ]
   }
   ```

### 3.2 Probar consultas de validación
```plaintext
Test 1: "Muestra el top 5 de marcas por valor comercial"
Expected: Tabla/gráfico con marcas ordenadas por Valor_Comercial_Total

Test 2: "¿Cuál es el score promedio por segmento?"
Expected: Agregación de Score_Promedio por segmento_score
```

## 4. Crear Dashboard en Power BI

### 4.1 Diseño de páginas
1. **Overview Financiero**
   - KPI: Score promedio global
   - Gráfico de barras: Score por segmento
   - Línea temporal: Evolución de scores

2. **Análisis de Ventas**
   - Treemap: Valor comercial por categoría/marca
   - Tabla: Top 10 productos por ventas
   - Gráfico de líneas: Tendencia mensual de ventas

3. **Productos y Stock**
   - Gauge: % productos disponibles
   - Matriz: Stock por categoría
   - Scatter: Precio vs Stock con perfil_producto

### 4.2 Ejemplo de configuración visual (Power BI)
```yaml
# Configuración del Treemap de Valor Comercial
Visual: Treemap
Fields:
  - Category (Group)
  - Brand (Subgroup)
  - Valor_Comercial_Total (Size)
Colors: 
  - Scheme: "Corp Blue to Red"
  - By: Valor_Comercial_Total
Title: "Valor Comercial por Categoría y Marca"
```

## 5. Validación y Pruebas

### 5.1 Checklist de validación
- [ ] Todas las relaciones están en modo single (no bidirectional)
- [ ] Medidas DAX devuelven resultados esperados
- [ ] Data Agent responde correctamente a preguntas de negocio
- [ ] Dashboard se actualiza con datos nuevos
- [ ] Permisos asignados correctamente

### 5.2 Pruebas de rendimiento
```dax
-- Medida para validar tiempo de respuesta
Tiempo_Respuesta = 
VAR Start = NOW()
VAR Result = [Medida_Compleja]
RETURN
DATEDIFF(Start, NOW(), MILLISECOND)
```

## 6. Documentación

### 6.1 Diccionario de medidas
| Medida | Descripción | DAX |
|--------|-------------|-----|
| Valor_Comercial_Total | Suma total de ventas | `SUM(fact_sales[valor_comercial])` |
| Productos_Disponibles | Conteo de productos en stock | `CALCULATE(COUNTROWS(dim_products),dim_products[availability] = "In Stock")` |

### 6.2 Relaciones y dependencias
```mermaid
graph TD
    A[fact_sales] -->|productID| B[dim_products]
    A -->|customerID| C[dim_credit_scores]
```

## Referencias
- [Docs: Semantic Models in Fabric](https://learn.microsoft.com/fabric/data-warehouse/semantic-models)
- [Power BI DAX Reference](https://learn.microsoft.com/dax/)
