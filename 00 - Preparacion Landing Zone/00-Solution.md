# Solución Reto 00 — Preparación de la Landing Zone y Conexión de Datos (Microsoft Fabric)

Este documento describe, paso a paso, cómo completar el *Reto 0*: crear la zona de aterrizaje (landing zone) en Microsoft Fabric, provisionar Azure Cosmos DB con los JSON suministrados y conectar ambas plataformas.

Objetivos
- Provisionar Azure Cosmos DB (NoSQL) y cargar los datasets JSON.
- Crear un workspace y una Lakehouse en Microsoft Fabric con la estructura Bronze / Silver / Gold.
- Conectar Fabric a Cosmos DB y verificar la ingesta inicial.

Requisitos previos
- Permisos para crear recursos en Azure.
- Archivos JSON (por ejemplo `creditScore.json`, `products.json`).

Resultado esperado
- Cosmos DB con contenedores que contienen los JSON.
- Workspace en Fabric conectado a una Capacity.
- Lakehouse `Contoso_Lakehouse` con carpetas o tablas: `bronze`, `silver`, `gold`.

---

## 1. Crear Azure Cosmos DB (NoSQL)

1. Accede al portal de Azure.
2. Busca **Azure Cosmos DB** → Crear → seleccionar API **NoSQL**.
3. Rellena: resource group, account name (`contoso-cosmosdb`), region.
4. Crear la cuenta. En *Data Explorer* crea la base de datos y contenedores (por ejemplo `sales`, `credit`).
5. Carga los archivos JSON (manualmente desde Data Explorer o usando Azure Data Factory para cargas repetibles).

Verificación
- En *Data Explorer* se ven documentos JSON en el contenedor.

---

## 2. Crear Workspace en Microsoft Fabric

1. Abre Microsoft Fabric y crea un workspace llamado `ContosoData-Fabric`.
2. Asocia una Fabric Capacity (si tu organización la tiene asignada).

Verificación
- El workspace aparece en el listado y tienes permisos adecuados.

---

## 3. Crear Lakehouse y definir capas

1. En el workspace, crea una Lakehouse `Contoso_Lakehouse`.
2. Dentro, crea carpetas o tablas con la convención:
	- `bronze.*` para datos crudos
	- `silver.*` para datos limpios
	- `gold.*` para datos curados/consumo

Verificación
- Las carpetas/tablas están visibles en el navegador del Lakehouse.

---

## 4. Conectar Fabric a Azure Cosmos DB

1. En Fabric Data → New → Connection → Azure Cosmos DB.
2. Proporciona endpoint y clave (Azure Portal → Cosmos DB → Keys).
3. Testea y guarda la conexión.

Verificación
- La conexión se prueba y puedes ver containers/collections disponibles.

---

## 5. Ingesta inicial a Bronze

Opción rápida (portal):
1. Desde la conexión, selecciona el contenedor y elige *Ingest* hacia `Contoso_Lakehouse` → `bronze`.

Opción reproducible (recomendada):
1. Crear un Dataflow Gen2 o pipeline en Fabric/Data Factory que lea Cosmos DB y escriba en la Lakehouse Bronze.

Verificación
- La tabla o archivos aparecen en `bronze` con registros esperados.

---

## 6. Documentación y evidencias

1. Documento con nombres de recursos y convenciones (NO incluir claves en repositorio).
2. Capturas: Data Explorer (Cosmos), conexión en Fabric, contenido en Bronze.

---

Si confirmas, procedo a crear las guías en formato `.md` para los retos 01–06 y las guardo en sus carpetas respectivas.
