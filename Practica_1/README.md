# 📊 Proyecto SG-FOOD: Modelo de Inteligencia de Negocios

## 🧾 Descripción General

Este proyecto implementa un modelo de inteligencia de negocios para la empresa **SG-FOOD**, dedicada a la compra, distribución y comercialización de productos alimenticios en diferentes regiones del país.

La empresa enfrentaba problemas para integrar datos de múltiples sucursales con distintos formatos, dificultando los reportes generales y la toma de decisiones. Por ello, se implementó un proceso **ETL** (Extracción, Transformación y Carga) y un **modelo multidimensional** basado en esquema **estrella** para análisis OLAP.

---

## ⚙️ Fases del Proceso ETL

### 1. Extracción
- Se obtuvieron datos de **ventas** y **compras** de múltiples sucursales con diferentes estructuras.
- Los datos provienen de al menos **dos fuentes heterogéneas**.

### 2. Transformación
- Limpieza de datos (eliminación de nulos, formatos erróneos).
- Homologación de estructuras y tipos de datos.
- Normalización de nombres y claves.

### 3. Carga
- Los datos transformados fueron cargados a un **modelo estrella** en una base de datos SQL Server.
- Se generaron **tablas de hechos y dimensiones**, con claves primarias y foráneas para mantener integridad referencial.

---

## 🌟 Modelo Empresarial Implementado

### 🧩 Modelo Estrella

Se eligió el **modelo estrella** por su simplicidad, rendimiento y adecuación a análisis rápidos. Contiene dos **tablas de hechos** principales: `HechoVentas` y `HechoCompras`, relacionadas con dimensiones clave como `Producto`, `Tiempo`, `Sucursal`, `Proveedor` y `Región`.

### 📐 Diagrama Conceptual

                +-----------+
                |  Tiempo   |
                +-----------+
                    ↑
                    |
            +--------------+
            | HechoVentas  |
            +--------------+
            /      |      \
            /       |       \
            ↓        ↓        ↓
    +--------+ +----------+ +----------+
    |Producto| | Sucursal | | Región   |
    +--------+ +----------+ +----------+
                            ↑
                            |
                        (Sede de)

            +--------------+
            | HechoCompras |
            +--------------+
            /      |       \
            ↓       ↓        ↓
        +--------+ +-----------+ 
        |Producto| | Proveedor |
        +--------+ +-----------+


---

## 🗃️ Tablas del Modelo

### 🔸 Tablas de Hechos

- **HechoVentas**
  - id_venta (PK)
  - id_producto (FK)
  - id_tiempo (FK)
  - id_sucursal (FK)
  - cantidad_vendida
  - precio_unitario

- **HechoCompras**
  - id_compra (PK)
  - id_producto (FK)
  - id_proveedor (FK)
  - id_tiempo (FK)
  - cantidad_comprada
  - costo_unitario

### 🔹 Tablas de Dimensiones

- **Producto**
  - id_producto, nombre, categoría, marca

- **Tiempo**
  - id_tiempo, fecha, mes, trimestre, año

- **Sucursal**
  - id_sucursal, nombre, id_region

- **Región**
  - id_region, nombre

- **Proveedor**
  - id_proveedor, nombre, contacto

---

## 🧭 Jerarquías Definidas

- **Tiempo**: Año > Trimestre > Mes > Día
- **Producto**: Categoría > Marca > Producto
- **Sucursal**: Región > Sucursal

---

## 📊 Consultas de Análisis

El modelo permite realizar análisis como:
1. **Total de compras y ventas por año**
2. **Detección de productos con pérdida** (precio de venta < costo de compra)
3. **Top 5 productos más vendidos por unidades**
4. **Ingresos por región y año**
5. **Proveedores con mayor volumen de compras**

---


## 🧪 Resultados Esperados

- Datos limpios, normalizados y consolidados de todas las sucursales.
- Modelo de cubo listo para análisis multidimensional.
- Consultas de negocio resueltas con alto rendimiento.
- Mejora en la capacidad de análisis, monitoreo y toma de decisiones.

---

## 📌 Notas Finales

- Este proyecto fue desarrollado como parte del curso *Seminario de Sistemas 2*.
- Herramientas utilizadas: SQL Server, SSIS, SQL.
- Todos los scripts están probados y listos para ejecución.

