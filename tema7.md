# Resumen del Capítulo 7: Software Engineering

## Introducción
Este capítulo explora el campo de la ingeniería de software, que se enfoca en los principios y prácticas para desarrollar software de alta calidad de manera sistemática y eficiente. A diferencia de la programación individual, la ingeniería de software aborda el desarrollo de sistemas complejos que requieren trabajo en equipo, planificación a largo plazo y consideración de factores como mantenimiento, escalabilidad y usabilidad.

## 7.1 Ciclo de Vida del Software

### Fases del Desarrollo:
- **Especificación de requisitos**: Determinar qué debe hacer el sistema
- **Diseño**: Planificar la arquitectura y componentes del sistema
- **Implementación**: Escribir el código según el diseño
- **Pruebas**: Verificar que el software funciona según lo especificado
- **Despliegue**: Implementar el sistema en el entorno de producción
- **Mantenimiento**: Actualizar y corregir el software después de su lanzamiento

### Modelos de Ciclo de Vida:
- **Modelo en cascada**: Enfoque secuencial donde cada fase debe completarse antes de pasar a la siguiente
- **Modelo iterativo**: Desarrollo en iteraciones, con cada iteración produciendo una versión funcional del software
- **Modelo ágil**: Enfoque flexible que prioriza la colaboración con el cliente y la adaptación a los cambios
- **Desarrollo incremental**: Construir el sistema en incrementos funcionales

## 7.2 Especificación de Requisitos

### Tipos de Requisitos:
- **Requisitos funcionales**: Qué debe hacer el sistema
- **Requisitos no funcionales**: Cómo debe comportarse el sistema (rendimiento, seguridad, usabilidad)

### Técnicas para Recopilar Requisitos:
- Entrevistas con usuarios y stakeholders
- Observación del trabajo actual
- Análisis de documentos existentes
- Prototipado temprano

### Documento de Especificación:
- Debe ser claro, completo, consistente y verificable
- Sirve como contrato entre el cliente y el equipo de desarrollo
- Proporciona la base para el diseño y las pruebas

## 7.3 Diseño de Software

### Principios de Diseño:
- **Abstracción**: Enfocarse en aspectos esenciales ignorando detalles
- **Encapsulación**: Agrupar datos y comportamiento relacionados
- **Modularidad**: Dividir el sistema en componentes independientes
- **Cohesión**: Cada módulo debe tener una única responsabilidad bien definida
- **Acoplamiento**: Minimizar las dependencias entre módulos

### Patrones de Diseño:
- **Patrón MVC (Modelo-Vista-Controlador)**: Separa la lógica de negocio de la interfaz de usuario
- **Patrón Singleton**: Garantiza que una clase tenga solo una instancia
- **Patrón Factory**: Proporciona una interfaz para crear objetos sin especificar sus clases concretas

### Diagramas UML:
- **Diagramas de casos de uso**: Muestran la interacción entre actores y el sistema
- **Diagramas de clases**: Representan la estructura estática del sistema
- **Diagramas de secuencia**: Muestran la interacción entre objetos en un escenario específico

## 7.4 Implementación

### Buenas Prácticas:
- **Estilo de codificación consistente**: Mejora la legibilidad y mantenibilidad
- **Comentarios significativos**: Explican el "por qué" no el "qué"
- **Principio DRY (Don't Repeat Yourself)**: Evitar duplicación de código
- **KISS (Keep It Simple, Stupid)**: Mantener el diseño lo más simple posible

### Control de Versiones:
- Herramientas como Git permiten rastrear cambios en el código
- Facilita la colaboración entre múltiples desarrolladores
- Permite revertir a versiones anteriores si es necesario

## 7.5 Pruebas de Software

### Niveles de Pruebas:
- **Pruebas unitarias**: Verifican componentes individuales
- **Pruebas de integración**: Verifican la interacción entre componentes
- **Pruebas de sistema**: Verifican el sistema completo
- **Pruebas de aceptación**: Verifican que el sistema cumple con los requisitos del cliente

### Enfoques de Pruebas:
- **Pruebas de caja negra**: Se basan en especificaciones sin conocer la implementación
- **Pruebas de caja blanca**: Consideran la estructura interna del código
- **TDD (Test-Driven Development)**: Escribir pruebas antes que el código

### Automatización de Pruebas:
- Frameworks como JUnit, pytest permiten crear pruebas automatizadas
- Las pruebas automatizadas pueden ejecutarse repetidamente y de forma rápida
- Facilitan la integración continua y la entrega continua

## 7.6 Mantenimiento de Software

### Tipos de Mantenimiento:
- **Mantenimiento correctivo**: Corregir errores
- **Mantenimiento adaptativo**: Adaptar el software a cambios en el entorno
- **Mantenimiento perfectivo**: Mejorar el rendimiento o usabilidad
- **Mantenimiento preventivo**: Modificar el software para prevenir problemas futuros

### Desafíos del Mantenimiento:
- El código heredado puede carecer de documentación adecuada
- Los desarrolladores originales pueden no estar disponibles
- Los requisitos pueden haber cambiado significativamente

### Refactorización:
- Proceso de reestructurar el código sin cambiar su comportamiento externo
- Mejora la estructura interna para facilitar el mantenimiento futuro
- Debe realizarse con pruebas automatizadas para garantizar que no se introduzcan errores

## 7.7 Gestión de Proyectos de Software

### Estimación:
- Técnicas como PERT y CPM para planificar cronogramas
- Métodos de estimación basados en puntos de función o puntos de historia

### Metodologías Ágiles:
- Scrum: Trabajo en sprints cortos con revisiones regulares
- Kanban: Visualización del flujo de trabajo y limitación de trabajo en progreso
- XP (Extreme Programming): Énfasis en pruebas, refactorización y programación en pareja

### Control de Calidad:
- Revisiones de código para identificar problemas temprano
- Métricas para medir la calidad del software (cobertura de pruebas, complejidad ciclomática)
- Procesos formales como CMMI (Capability Maturity Model Integration)

## Conceptos Clave para Recordar
- **Ciclo de vida del software**: Secuencia de fases por las que pasa un sistema de software desde su concepción hasta su retirada
- **Mantenimiento correctivo vs. adaptativo vs. perfectivo**: Diferentes tipos de mantenimiento que se realizan después del lanzamiento
- **Cohesión y acoplamiento**: Principios de diseño que afectan la modularidad del software
- **TDD (Test-Driven Development)**: Enfoque de desarrollo donde se escriben pruebas antes que el código
- **Refactorización**: Proceso de mejorar la estructura del código sin cambiar su comportamiento
- **Metodologías ágiles**: Enfoques flexibles para el desarrollo de software que priorizan la adaptación a los cambios
- **Control de versiones**: Sistema para rastrear y gestionar cambios en el código fuente

Este resumen cubre los conceptos fundamentales del Capítulo 7 sobre Ingeniería de Software, ideal para prepararse para exámenes o para comprender los principios básicos de cómo se desarrolla software de calidad de manera sistemática. La ingeniería de software es esencial para crear sistemas complejos que sean mantenibles, escalables y que satisfagan las necesidades de los usuarios a largo plazo.

---

¡Fin del Capítulo 7!

[⏮️ **Capítulo Anterior: Lenguajes de Programación**](tema6.md)  
[⏭️ **Siguiente Capítulo: Abstracciones de Datos**](tema8.md)