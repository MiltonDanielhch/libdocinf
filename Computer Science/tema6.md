# Resumen del Capítulo 6: Lenguajes de Programación

## Introducción
Este capítulo explora los lenguajes de programación, no centrándose en un lenguaje específico sino en comprender las características comunes y las diferencias entre los diversos lenguajes y sus metodologías. Los lenguajes de programación son herramientas esenciales para desarrollar programas que pueden utilizarse para expresión creativa, satisfacer curiosidad personal, crear nuevo conocimiento o resolver problemas.

## 6.1 Perspectiva Histórica

### Generaciones de Lenguajes:
- **Primera generación (Lenguajes máquina)**:
  - Programas codificados directamente como secuencias de dígitos numéricos
  - Tedioso y propenso a errores

- **Segunda generación (Lenguajes ensamblador)**:
  - Uso de mnemónicos para representar instrucciones (ej.: MOV R5, R6 en lugar de 0x4056)
  - Requiere un ensamblador para convertir a lenguaje máquina
  - Ejemplo: LD R5, Price / ADDI R0, R5, R6 / ST R0, TotalCost

- **Tercera generación (Lenguajes de alto nivel)**:
  - Primitivas más abstractas y máquina-independientes
  - Permiten expresar instrucciones en "grandes incrementos"
  - Ejemplos: FORTRAN, COBOL, C, Python
  - Requieren compiladores o intérpretes para traducción

## 6.2 Conceptos Tradicionales de Programación

### Abstracciones en Lenguajes de Alto Nivel:
- **Variables y constantes**: Almacenan datos y valores
- **Expresiones y sentencias**: Construyen operaciones y acciones
- **Estructuras de control**:
  - *Estructuras de selección*: if-else
  - *Estructuras iterativas*: while, for
  - *Procedimientos y funciones*: Unidades modulares de código

### Estructuras de Control:
- **if-else**: Permite tomar decisiones basadas en condiciones
  ```python
  if (condición):
      sentenciaA
  else:
      sentenciaB
  ```

- **while**: Permite repetir un bloque de código mientras se cumpla una condición
  ```python
  while (condición):
      cuerpo
  ```

## 6.3 Unidades Procedimentales

### Funciones:
- **Definición**: Unidades modulares que encapsulan tareas específicas
- **Encabezado de función**: Identifica el nombre y parámetros
- **Parámetros formales**: Variables definidas en la función
- **Parámetros reales**: Valores proporcionados al llamar la función

### Flujo de Control:
1. La unidad de programa llama a la función
2. El control se transfiere a la función
3. Se ejecuta la función
4. El control regresa a la unidad de llamada

### Paso de Parámetros:
- **Por valor**: Se copia el valor del parámetro real al formal
- **Por referencia**: El parámetro formal se refiere directamente a la ubicación de memoria del parámetro real

### Ejemplo de Función:
```python
def CylinderVolume(Radius, Height):
    return 3.14159 * Radius * Radius * Height
```
Esta función podría usarse en una sentencia como:
```python
Cost = CostPerVolUnit * CylinderVolume(3.45, 12.7)
```

## 6.4 Paquetes de Desarrollo de Software

### Entornos de Desarrollo Integrado (IDE):
- **Componentes principales**:
  - Editor para escribir programas
  - Traductor para convertir a lenguaje máquina
  - Herramientas de depuración para rastrear errores

### Ventajas de los IDEs:
- Facilitan el movimiento entre editor y herramientas de depuración
- Permiten manejar programas relacionados conjuntamente
- Mejoran la eficiencia del proceso de desarrollo

## 6.5 Programación Orientada a Objetos

### Conceptos Clave:
- **Objetos**: Unidades activas que contienen funciones que describen cómo responder a estímulos
- **Clases**: Plantillas para crear objetos
- **Mensajes**: Mecanismo para que los objetos se comuniquen

### Ventajas de la Programación Orientada a Objetos:
- Los objetos son unidades bien definidas cuyas descripciones están aisladas en clases reutilizables
- Proporciona un entorno natural para el enfoque de "bloques de construcción" en desarrollo de software
- Permite crear bibliotecas de clases predefinidas para construir nuevos sistemas

### Ejemplo de Sintaxis Orientada a Objetos:
```java
Laser1.fire();
Laser2.turnLeft();
```
Estas sentencias son llamadas a métodos dentro de objetos específicos.

## 6.6 Paradigmas de Programación

### Diferentes Enfoques:
- **Paradigma imperativo**: Enfocado en describir cómo resolver un problema mediante secuencias de comandos
- **Paradigma declarativo**: Enfocado en describir qué debe hacerse sin especificar cómo
- **Paradigma funcional**: Trata la computación como la evaluación de funciones matemáticas
- **Paradigma orientado a objetos**: Organiza el código en objetos que contienen datos y comportamiento

### Importancia de los Paradigmas:
- Van más allá del proceso de programación
- Representan enfoques fundamentalmente diferentes para construir soluciones a problemas
- Afectan todo el proceso de desarrollo de software

## 6.7 Procesamiento de Lenguajes

### Proceso de Traducción:
1. **Analizador léxico**: Divide el programa en unidades léxicas (tokens)
2. **Analizador sintáctico (Parser)**: Agrupa los tokens en árboles de análisis
3. **Generador de código**: Convierte los árboles de análisis en código objeto

### Compilación vs. Interpretación:
- **Compilador**: Convierte todo el programa fuente a código objeto de una vez
- **Intérprete**: Traduce y ejecuta el programa línea por línea

### Diagramas de Sintaxis:
- Herramientas visuales que describen la estructura de las expresiones en un lenguaje
- Permiten representar cómo una cadena específica se ajusta a las reglas gramaticales

## 6.8 Programación Lógica (Prolog)

### Características:
- Basada en lógica de predicados
- Los programas consisten en hechos y reglas
- El programa busca deducir conclusiones a partir de los hechos proporcionados

### Ejemplo de Programa Prolog:
```prolog
female(carol).
female(sue).
male(bill).
male(john).
parent(john, carol).
parent(sue, carol).
mother(X,Y) :- female(X), parent(X,Y).
father(X,Y) :- male(X), parent(X,Y).
```

### Problemas con la Programación Lógica:
- Las definiciones pueden llevar a conclusiones inesperadas
- Los programas reales pueden no capturar toda la multiplicidad de propósito sugerida por los ejemplos teóricos

## Conceptos Clave para Recordar

- **Paradigma de programación**: Enfoque fundamental para resolver problemas mediante programación
- **Unidad procedimental**: Bloque de código que realiza una tarea específica (función, procedimiento, método)
- **Encapsulación**: Técnica de ocultar los detalles de implementación
- **Clase**: Plantilla para crear objetos en programación orientada a objetos
- **Instancia**: Objeto específico creado a partir de una clase
- **Paso de parámetros por valor vs. por referencia**: Diferentes formas de transmitir datos a funciones
- **IDE (Entorno de Desarrollo Integrado)**: Paquete de herramientas para desarrollo de software
- **Compilador vs. Intérprete**: Diferentes métodos para traducir código fuente a código máquina
- **Árbol de análisis**: Representación estructural de cómo un programa se ajusta a las reglas gramaticales del lenguaje

Este resumen cubre los conceptos fundamentales del Capítulo 6 sobre Lenguajes de Programación, ideal para prepararse para exámenes o para comprender los principios básicos de cómo funcionan y evolucionan los lenguajes de programación. La comprensión de estos conceptos es esencial para cualquier estudiante de informática, ya que los lenguajes de programación son la herramienta principal para convertir ideas en aplicaciones funcionales.

---

¡Fin del Capítulo 6!

[⏮️ **Capítulo Anterior: Algoritmos**](tema5.md)  
[⏭️ **Siguiente Capítulo: Ingeniería de Software**](tema7.md)