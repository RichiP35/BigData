markdown
# Proyecto de Big Data FASE4 - MongoDB

## Descripción General
Este proyecto almacena y gestiona datos de productos de una tienda en línea usando MongoDB.

## Estructura
- **scripts/**: Contiene scripts de inserción, consultas, agregaciones, actualizaciones y eliminación.
- **documentación/**: Incluye el diseño de la base de datos, índices, análisis de consultas y resultados, y conclusiones personales.

### Cómo Ejecutar
1. Inserta los datos: `mongo scripts/insercion_datos.js`
2. Ejecuta las consultas: `mongo scripts/consultas_basicas.js`
3. Realiza agregaciones: `mongo scripts/consultas_agregacion.js`
4. Actualiza documentos: `mongo scripts/actualizaciones.js`
5. Elimina documentos: `mongo scripts/eliminaciones.js`
Documentación
diseño_base_de_datos.md
markdown
# Diseño de la Base de Datos en MongoDB

## Nombre de la Base de Datos
`tienda_online`

## Colección
`products`

## Estructura de Documento

{
    "productId": Number,
    "name": String,
    "description": String,
    "price": Number,
    "category": String,
    "brand": String,
    "stockQuantity": Number
}
Ejemplo de Documento

`json
{
    "productId": 1,
    "name": "iPhone 13",
    "description": "Apple iPhone 13 with 128GB storage",
    "price": 3999960,
    "category": "Smartphone",
    "brand": "Apple",
    "stockQuantity": 50
}`

#### indices.md

# Índices en MongoDB

Para optimizar las consultas en la base de datos, se han creado los siguientes índices:

`javascript
db.products.createIndex({ "productId": 1 }, { unique: true })
db.products.createIndex({ "name": "text" })
db.products.createIndex({ "category": 1 })
Explicación de los Índices
productId: Índice único para identificar cada producto de manera eficiente.`

name: Índice de texto para permitir búsquedas textuales rápidas en el nombre del producto.

category: Índice para acelerar las consultas basadas en la categoría del producto.


#### consultas_y_resultados.md

# Consultas y Resultados en MongoDB

## Inserción de Documentos
`
db.products.insertMany([
  { productId: 1, name: "iPhone 13", description: "Apple iPhone 13 with 128GB storage", price: 3999960, category: "Smartphone", brand: "Apple", stockQuantity: 50 },
  // ... otros documentos
])`


Selección de Documentos
`javascript
db.products.find({ "brand": "Apple" })
Actualización de Documentos
javascript
db.products.updateOne(
    { "name": "iPhone 13" },
    { $set: { "stockQuantity": 60 } }
)`

Eliminación de Documentos
`javascript
db.products.deleteOne({ "name": "Echo Dot" })
Consultas con Filtros y Operadores
javascript
db.products.find({ "price": { $gt: 1000000 } })
db.products.find({ $and: [ { "brand": "Apple" }, { "category": "Smartphone" } ] })`

Consultas de Agregación
`javascript
db.products.aggregate([
    { $match: {} },
    { $count: "totalProducts" }
])
db.products.aggregate([
    { $group: { _id: null, totalStock: { $sum: "$stockQuantity" } } }
])
db.products.aggregate([
    { $group: { _id: null, avgPrice: { $avg: "$price" } } }
])`

Resultados
Inserción: Los documentos se insertaron correctamente en la colección products.
Selección: Las consultas devolvieron los productos esperados.
Actualización: Las actualizaciones se aplicaron correctamente a los documentos.
Eliminación: Los documentos se eliminaron correctamente.
Agregación: Los cálculos de agregación fueron precisos y útiles para el análisis.


#### conclusiones_personales.md

# Conclusiones Personales

## 1. Dominio de MongoDB y HBase
**Lo que Aprendí**: Durante el proceso, adquirí un conocimiento profundo sobre cómo manejar bases de datos NoSQL, específicamente MongoDB y HBase. Aprendí a realizar operaciones básicas y avanzadas, como inserciones, consultas, actualizaciones y eliminaciones.
**Aplicación Futura**: Este conocimiento me permitirá implementar soluciones de bases de datos eficientes y escalables en futuros proyectos de big data, optimizando la gestión y análisis de grandes volúmenes de datos.

## 2. Migración de Datos ETL (Extracción, Transformación, Carga)
**Lo que Aprendí**: Comprendí y puse en práctica el proceso ETL para migrar datos de MongoDB a HBase. Aprendí a extraer datos, transformarlos según las necesidades del sistema de destino y cargarlos eficazmente.
**Aplicación Futura**: Esta habilidad es crucial para proyectos que requieren la integración de múltiples sistemas de bases de datos, permitiéndome manejar la transferencia de datos con precisión y eficiencia.

## 3. Optimización y Rendimiento
**Lo que Aprendí**: Aprendí a optimizar consultas y mejorar el rendimiento de las bases de datos mediante la creación de índices y el uso de agregaciones. Esto resultó en tiempos de respuesta más rápidos y una mejor gestión de los recursos.
**Aplicación Futura**: La optimización de bases de datos es esencial para aplicaciones de alta demanda. Implementaré estas técnicas para asegurar que los sistemas futuros sean rápidos, confiables y escalables.

## 4. Solución de Problemas Técnicos
**Lo que Aprendí**: Durante el proyecto, enfrenté y resolví diversos desafíos técnicos, como la configuración de entornos y la conexión entre sistemas distribuidos. Esta experiencia mejoró mis habilidades de resolución de problemas y mi capacidad para abordar situaciones imprevistas.
**Aplicación Futura**: La capacidad de resolver problemas técnicos es invaluable en cualquier proyecto de TI. Continuaré perfeccionando estas habilidades para asegurar una implementación fluida y exitosa en futuros desarrollos.

## 5. Documentación y Comunicación Técnica
**Lo que Aprendí**: La documentación detallada del diseño de la base de datos, las consultas realizadas y los resultados obtenidos me enseñó la importancia de una buena comunicación técnica. Esto no solo ayuda en la comprensión del proyecto, sino que también facilita su mantenimiento y escalabilidad.
**Aplicación Futura**: Seguiré implementando prácticas sólidas de documentación en todos mis proyectos para asegurar que cualquier persona pueda entender y continuar el trabajo con facilidad.

## Reflexión Final
Este proyecto me brindó una comprensión completa de cómo gestionar bases de datos NoSQL y mejorar el rendimiento del sistema. Las habilidades y conocimientos adquiridos durante el proceso no solo me preparan para enfrentar desafíos similares en el futuro, sino que también mejoran mi capacidad para diseñar e implementar soluciones de big data más eficientes y efectivas. Estoy entusiasmado por aplicar todo lo aprendido en proyectos futuros y continuar creciendo en el campo del manejo de datos.


###Scripts en MongoDB

insercion_datos.js
`javascript
db.products.insertMany([
  { productId: 1, name: "iPhone 13", description: "Apple iPhone 13 with 128GB storage", price: 3999960, category: "Smartphone", brand: "Apple", stockQuantity: 50 },
  { productId: 2, name: "Galaxy S21", description: "Samsung Galaxy S21 with 128GB storage", price: 3399960, category: "Smartphone", brand: "Samsung", stockQuantity: 30 },
  // ... otros documentos
]);`

consultas_basicas.js
`javascript
// Seleccionar productos de la marca Apple
db.products.find({ "brand": "Apple" });
// Seleccionar productos con precio mayor a 1,000,000
db.products.find({ "price": { $gt: 1000000 } });
consultas_agregacion.js
javascript`
