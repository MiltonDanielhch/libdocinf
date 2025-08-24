# Resumen del Capítulo 9: Bases de Datos

## Introducción
Este capítulo explora los sistemas de bases de datos, que son estructuras organizadas para almacenar, gestionar y recuperar grandes volúmenes de información de manera eficiente. Las bases de datos son componentes esenciales en casi todos los sistemas informáticos modernos, desde aplicaciones empresariales hasta sistemas web y móviles. Comprender cómo funcionan los sistemas de bases de datos es fundamental para diseñar aplicaciones que manejen información de manera efectiva y segura.

## 9.1 Sistema de Gestión de Bases de Datos (SGBD)

### Componentes de un SGBD:
- **Definición**: Software que permite crear, mantener y utilizar bases de datos
- **Componentes principales**:
  - *Motor de base de datos*: Core que maneja el almacenamiento físico
  - *Lenguaje de definición de datos (DDL)*: Para definir la estructura de la base de datos
  - *Lenguaje de manipulación de datos (DML)*: Para consultar y modificar datos
  - *Diccionario de datos*: Almacena metadatos sobre la estructura de la base de datos
  - *Control de transacciones*: Gestiona operaciones atómicas

### Ventajas de los SGBD:
- **Reducción de redundancia**: Evita datos duplicados
- **Consistencia de datos**: Mantiene la integridad de la información
- **Compartición de datos**: Permite el acceso concurrente a múltiples usuarios
- **Seguridad**: Controla el acceso a los datos mediante permisos
- **Independencia de datos**: Separa la vista lógica de la física

## 9.2 Modelos de Datos

### Modelo Relacional:
- **Concepto fundamental**: Datos organizados en tablas (relaciones)
- **Componentes**:
  - *Entidad*: Objeto del mundo real representado en la base de datos
  - *Atributo*: Propiedad de una entidad (columna en una tabla)
  - *Tupla*: Registro o fila en una tabla
  - *Clave primaria*: Atributo único que identifica cada tupla
  - *Clave foránea*: Atributo que establece relaciones entre tablas

### Modelo Entidad-Relación (E-R):
- **Diagramas E-R**: Representación gráfica de entidades y sus relaciones
- **Componentes**:
  - *Entidades*: Representadas como rectángulos
  - *Atributos*: Representados como óvalos
  - *Relaciones*: Representadas como rombos
  - *Cardinalidad*: Define cuántas entidades pueden participar en una relación (uno a uno, uno a muchos, muchos a muchos)

### Otros Modelos:
- **Modelo jerárquico**: Estructura en árbol
- **Modelo en red**: Permite relaciones más complejas que el jerárquico
- **Modelo orientado a objetos**: Integra conceptos de POO en bases de datos
- **Modelo NoSQL**: Diseñado para manejar grandes volúmenes de datos no estructurados

## 9.3 Lenguaje de Consulta Estructurado (SQL)

### Componentes de SQL:
- **DDL (Data Definition Language)**:
  - `CREATE TABLE`: Define nuevas tablas
  - `ALTER TABLE`: Modifica estructuras existentes
  - `DROP TABLE`: Elimina tablas

- **DML (Data Manipulation Language)**:
  - `SELECT`: Recupera datos
  - `INSERT`: Añade nuevos registros
  - `UPDATE`: Modifica registros existentes
  - `DELETE`: Elimina registros

### Consultas Básicas:
```sql
SELECT nombre, edad FROM empleados WHERE departamento = 'Ventas';
```
- **Cláusulas importantes**:
  - `WHERE`: Condición de filtrado
  - `GROUP BY`: Agrupa resultados
  - `HAVING`: Filtra grupos
  - `ORDER BY`: Ordena resultados
  - `JOIN`: Combina datos de múltiples tablas

### Funciones de Agregación:
- `COUNT()`: Cuenta el número de registros
- `SUM()`: Suma valores numéricos
- `AVG()`: Calcula el promedio
- `MIN()`, `MAX()`: Valores mínimo y máximo

## 9.4 Normalización

### Objetivo:
- Eliminar redundancias y anomalías en el diseño de bases de datos

### Formas Normales:
- **Primera Forma Normal (1FN)**: Elimina grupos repetitivos, cada atributo debe contener un solo valor
- **Segunda Forma Normal (2FN)**: Cumple 1FN y todos los atributos no clave dependen completamente de la clave primaria
- **Tercera Forma Normal (3FN)**: Cumple 2FN y no hay dependencias transitivas entre atributos no clave
- **Forma Normal de Boyce-Codd (BCNF)**: Versión más estricta de 3FN

### Proceso de Normalización:
1. Identificar entidades y relaciones
2. Eliminar datos redundantes
3. Crear tablas separadas para grupos relacionados
4. Identificar claves primarias y foráneas
5. Verificar y aplicar formas normales

## 9.5 Transacciones e Integridad

### Transacciones:
- **Definición**: Secuencia de operaciones tratadas como una unidad lógica
- **Propiedades ACID**:
  - *Atomicidad*: La transacción se ejecuta completamente o no se ejecuta
  - *Consistencia*: Preserva la integridad de la base de datos
  - *Aislamiento*: Las transacciones no interfieren entre sí
  - *Durabilidad*: Los cambios persisten después de completar la transacción

### Control de Concurrencia:
- **Problemas**:
  - *Pérdida de actualización*: Dos transacciones sobrescriben cambios mutuamente
  - *Lectura sucia*: Leer datos modificados pero no confirmados
  - *Lectura no repetible*: Leer los mismos datos dos veces y obtener resultados diferentes
  - *Fantasma*: Nuevos registros aparecen durante una transacción

- **Mecanismos de control**:
  - *Bloqueo*: Impide que otras transacciones accedan a datos bloqueados
  - *Timestamp*: Asigna marcas de tiempo para determinar el orden de ejecución
  - *Optimista*: Permite ejecución concurrente y verifica conflictos al finalizar

## 9.6 Bases de Datos Distribuidas

### Conceptos:
- **Definición**: Base de datos que está físicamente almacenada en múltiples ubicaciones
- **Tipos**:
  - *Homogéneas*: Mismo SGBD en todos los nodos
  - *Heterogéneas*: Diferentes SGBD en los nodos

### Ventajas:
- **Disponibilidad**: Si un nodo falla, otros pueden seguir operando
- **Escalabilidad**: Posibilidad de añadir más nodos según necesidades
- **Rendimiento**: Procesamiento local de datos reduce el tráfico de red

### Desafíos:
- **Transparencia**: Ocultar la distribución al usuario
- **Consistencia**: Mantener datos sincronizados en múltiples ubicaciones
- **Fragmentación**: Dividir los datos de manera eficiente
- **Replicación**: Mantener copias de datos en múltiples nodos

## 9.7 Bases de Datos en la Web

### Integración Web:
- **Tecnologías comunes**:
  - *CGI (Common Gateway Interface)*: Interfaz para ejecutar scripts en el servidor
  - *PHP, ASP, JSP*: Lenguajes para crear páginas web dinámicas
  - *APIs REST*: Para acceder a datos mediante solicitudes HTTP

### Bases de Datos NoSQL:
- **Características**:
  - Esquema flexible o sin esquema
  - Escalabilidad horizontal
  - Alta disponibilidad
  - Diseñadas para manejar grandes volúmenes de datos

- **Tipos principales**:
  - *Documentales*: Almacenan documentos en formatos como JSON (MongoDB)
  - *Clave-valor*: Almacenamiento simple de pares clave-valor (Redis)
  - *Columnares*: Optimizadas para consultas analíticas (Cassandra)
  - *Grafos*: Para datos con relaciones complejas (Neo4j)

## 9.8 Seguridad en Bases de Datos

### Amenazas Comunes:
- **Inyección SQL**: Introducir código malicioso en consultas
- **Acceso no autorizado**: Obtener datos sin permisos adecuados
- **Exposición de datos sensibles**: Información confidencial accesible

### Medidas de Seguridad:
- **Control de acceso**: Definir permisos para usuarios y roles
  - `GRANT SELECT ON tabla TO usuario;`
  - `REVOKE INSERT ON tabla FROM usuario;`
  
- **Encriptación**: Proteger datos en reposo y en tránsito
- **Auditoría**: Monitorear y registrar actividades en la base de datos
- **Máscaras de datos**: Ocultar información sensible en entornos de desarrollo

### Buenas Prácticas:
- Validar todas las entradas de usuario
- Usar consultas parametrizadas para prevenir inyección SQL
- Aplicar el principio de mínimo privilegio
- Realizar copias de seguridad regulares

## Conceptos Clave para Recordar
- **SGBD (Sistema de Gestión de Bases de Datos)**: Software para crear y gestionar bases de datos
- **Modelo relacional**: Datos organizados en tablas con relaciones definidas
- **SQL (Structured Query Language)**: Lenguaje estándar para consultar y manipular bases de datos relacionales
- **Normalización**: Proceso para eliminar redundancias y mejorar el diseño
- **Transacción**: Unidad lógica de trabajo con propiedades ACID
- **Clave primaria vs. clave foránea**: Mecanismos para identificar registros y establecer relaciones
- **Formas normales**: Criterios para evaluar el diseño de una base de datos
- **Bases de datos NoSQL**: Sistemas diseñados para manejar datos no estructurados a gran escala

Este resumen cubre los conceptos fundamentales del Capítulo 9 sobre Bases de Datos, ideal para prepararse para exámenes o para comprender los principios básicos de cómo se organizan, gestionan y utilizan las bases de datos en sistemas informáticos. El conocimiento de bases de datos es esencial para cualquier estudiante de informática, ya que prácticamente todas las aplicaciones modernas dependen de sistemas eficientes de gestión de datos.

---

¡Fin del Capítulo 9!

[⏮️ **Capítulo Anterior: Abstracciones de Datos**](tema8.md)  
[⏭️ **Siguiente Capítulo: Gráficos por Computadora**](tema10.md)