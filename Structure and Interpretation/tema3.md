# Resumen Completo: Estructuras de Datos Mutables y Sistemas con Estado  
## Basado en *Structure and Interpretation of Computer Programs* (Capítulo 3)

---

## **1. Introducción a los Datos Mutables y el Estado**

### **1.1. Mutación de Estructuras de Datos**
- **Definición**: La mutación permite modificar directamente los valores de los datos después de su creación.
- **Operaciones clave en Scheme**:
  - `set-car!`: Modifica el primer elemento (car) de un par
  - `set-cdr!`: Modifica el resto (cdr) de un par
- **Ejemplo ilustrativo**:
  ```scheme
  (define x (list 'a 'b))
  (define z1 (cons x x))
  (set-car! (car z1) 'wow) ; Afecta a ambas partes de z1
  z1 ; Resultado: ((wow b) wow b)
  ```

### **1.2. Efectos de la Mutación**
- **Estructuras compartidas**: Cuando múltiples estructuras comparten partes comunes, la mutación en una afecta a todas.
- **Detección de identidad**: 
  - `eq?`: Comprueba si dos objetos son el mismo (igualdad de punteros)
  - `equal?`: Comprueba si dos estructuras tienen el mismo contenido
- **Problemas comunes**:
  - Efectos secundarios no deseados cuando estructuras comparten componentes
  - Dificultad para razonar sobre el estado del programa

> "La mutación introduce complejidad al crear dependencias ocultas entre diferentes partes de un programa. Lo que parece una operación local puede tener efectos globales en estructuras de datos compartidas."

---

## **2. Estructuras de Datos con Estado**

### **2.1. Colas (Queues)**
- **Definición**: Estructura de datos donde los elementos se insertan en la parte trasera y se eliminan desde el frente (FIFO).
- **Operaciones esenciales**:
  - `make-queue`: Crea una cola vacía
  - `empty-queue?`: Verifica si la cola está vacía
  - `front-queue`: Devuelve el elemento frontal
  - `insert-queue!`: Inserta un elemento al final
  - `delete-queue!`: Elimina el elemento frontal

### **2.2. Implementación de Colas**
- **Representación con punteros**:
  - `front-ptr`: Apunta al primer elemento
  - `rear-ptr`: Apunta al último elemento
- **Invariante clave**: El `cdr` del último par siempre debe ser `nil`
- **Ejemplo de inserción**:
  ```scheme
  (define (insert-queue! queue item)
    (let ((new-pair (cons item '())))
      (cond ((empty-queue? queue)
             (set-front-ptr! queue new-pair)
             (set-rear-ptr! queue new-pair)
             queue)
            (else
             (set-cdr! (rear-ptr queue) new-pair)
             (set-rear-ptr! queue new-pair)
             queue))))
  ```

### **2.3. Colas de Doble Extremo (Deques)**
- **Característica**: Permite inserción y eliminación en ambos extremos
- **Operaciones adicionales**:
  - `front-insert-deque!`: Inserta en el frente
  - `rear-insert-deque!`: Inserta en la parte trasera
  - `front-delete-deque!`: Elimina desde el frente
  - `rear-delete-deque!`: Elimina desde la parte trasera

---

## **3. Sistemas de Restricciones**

### **3.1. Concepto Básico**
- **Definición**: Sistema donde los cálculos fluyen en cualquier dirección entre componentes conectados.
- **Característica clave**: **Nodireccionalidad** - el mismo sistema puede resolver diferentes variables dadas otras conocidas.
- **Ejemplo clásico**: Conversor Celsius-Fahrenheit
  - Puede calcular F dado C, o C dado F
  - Mismo sistema, diferente dirección de cálculo

### **3.2. Componentes del Sistema**
- **Conectores**: Almacenan valores y gestionan restricciones
  - `has-value?`: Verifica si tiene valor
  - `get-value`: Obtiene el valor actual
  - `set-value!`: Establece un nuevo valor
  - `forget-value!`: Olvida el valor actual
- **Restricciones**: Objetos que implementan relaciones
  - `adder`: Suma dos valores
  - `multiplier`: Multiplica dos valores
  - `constant`: Establece un valor constante
  - `probe`: Muestra cambios en valores

### **3.3. Ejemplo de Sistema de Restricciones**
```scheme
(define (celsius-fahrenheit-converter c f)
  (let ((u (make-connector))
        (v (make-connector))
        (w (make-connector))
        (x (make-connector))
        (y (make-connector)))
    (multiplier c w u)
    (multiplier v x u)
    (adder v y f)
    (constant 9 w)
    (constant 5 x)
    (constant 32 y)
    'ok))
```
- **Flujo de información**: Los valores se propagan a través de los conectores
- **Manejo de conflictos**: Si dos fuentes intentan establecer valores diferentes, el sistema detecta contradicciones

---

## **4. Simulación de Circuitos Digitales**

### **4.1. Componentes Básicos**
- **Cables (wires)**: Transportan señales (0 o 1)
- **Puertas lógicas**:
  - `and-gate`: AND lógico
  - `or-gate`: OR lógico
  - `inverter`: NOT lógico
- **Retardo de propagación**: Tiempo para que el cambio en la entrada afecte la salida

### **4.2. Circuitos Combinados**
- **Medio sumador (half-adder)**:
  ```scheme
  (define (half-adder a b s c)
    (let ((d (make-wire)) (e (make-wire)))
      (or-gate a b d)
      (and-gate a b c)
      (inverter c e)
      (and-gate d e s)
      'ok))
  ```
- **Sumador completo (full-adder)**:
  - Combina dos medio sumadores y una puerta OR
  - Maneja el acarreo (carry) de sumas anteriores

### **4.3. Agenda de Simulación**
- **Propósito**: Gestionar el orden temporal de los eventos
- **Estructura**:
  - Segmentos de tiempo ordenados
  - Cada segmento contiene una cola de acciones
- **Operaciones clave**:
  - `make-agenda`: Crea una nueva agenda
  - `current-time`: Obtiene el tiempo actual
  - `add-to-agenda!`: Añade una acción a un tiempo específico
  - `propagate`: Ejecuta todas las acciones pendientes

---

## **5. Tablas y Memoización**

### **5.1. Implementación de Tablas**
- **Estructura**: Tablas anidadas con múltiples claves
- **Operaciones básicas**:
  - `make-table`: Crea una nueva tabla
  - `lookup`: Busca un valor por clave(s)
  - `insert!`: Inserta o actualiza un valor
- **Ejemplo de implementación**:
  ```scheme
  (define (make-table)
    (let ((local-table (list '*table*)))
      (define (lookup key-1 key-2)
        (let ((subtable (assoc key-1 (cdr local-table))))
          (if subtable
              (let ((record (assoc key-2 (cdr subtable))))
                (if record (cdr record) false))
              false)))
      (define (insert! key-1 key-2 value)
        ; Implementación de inserción...)
      (define (dispatch m)
        (cond ((eq? m 'lookup-proc) lookup)
              ((eq? m 'insert-proc!) insert!)
              (else (error "Unknown operation -- TABLE" m))))
      dispatch))
  ```

### **5.2. Memoización**
- **Definición**: Técnica para optimizar funciones almacenando resultados previamente calculados
- **Implementación**:
  ```scheme
  (define (memoize f)
    (let ((table (make-table)))
      (lambda (x)
        (let ((previously-computed-result (lookup x table)))
          (or previously-computed-result
              (let ((result (f x)))
                (insert! x result table)
                result))))))
  ```
- **Ventaja**: Convierte procesos exponenciales en procesos lineales (ej.: cálculo de Fibonacci)

---

## **6. Modelos de Ambiente y Estado Local**

### **6.1. Modelo de Ambiente**
- **Marco (frame)**: Conjunto de enlaces nombre-valor
- **Encadenamiento de ambientes**: Cada marco tiene un puntero al ambiente envolvente
- **Evaluación de procedimientos**:
  1. Se crea un nuevo marco con parámetros ligados a argumentos
  2. El marco se encadena al ambiente de definición del procedimiento
  3. Se evalúa el cuerpo en este nuevo ambiente

### **6.2. Estado Local con Closures**
- **Patrón de objeto con estado**:
  ```scheme
  (define (make-withdraw balance)
    (lambda (amount)
      (if (>= balance amount)
          (begin (set! balance (- balance amount))
                 balance)
          "Fondos insuficientes")))
  ```
- **Características**:
  - El estado persiste entre llamadas
  - El estado está encapsulado (solo accesible a través de procedimientos específicos)

---

## **7. Vocabulario Técnico Esencial**

| **Término en Inglés** | **Traducción** | **Definición** |
|----------------------|---------------|---------------|
| Mutation | Mutación | Modificación directa de datos existentes |
| Side effect | Efecto secundario | Cambio en el estado del sistema durante la evaluación |
| Queue | Cola | Estructura FIFO (primero en entrar, primero en salir) |
| Deque | Cola de doble extremo | Estructura con inserción/eliminación en ambos extremos |
| Constraint system | Sistema de restricciones | Sistema donde los cálculos fluyen en cualquier dirección |
| Propagation delay | Retardo de propagación | Tiempo para que un cambio afecte a la salida |
| Agenda | Agenda | Estructura para gestionar eventos en orden temporal |
| Memoization | Memoización | Técnica de optimización mediante almacenamiento de resultados |
| Environment model | Modelo de ambiente | Modelo para entender cómo se evalúan los procedimientos |
| Local state | Estado local | Información que persiste entre llamadas a un procedimiento |

---

## **8. Principios Clave para Recordar**

1. **"La mutación introduce complejidad"**: Los programas con estado son más difíciles de razonar que los programas funcionales puros.

2. **"La compartición de estructuras es poderosa pero peligrosa"**: Las modificaciones a estructuras compartidas pueden tener efectos no deseados en otras partes del programa.

3. **"Los sistemas de restricciones son nodireccionales"**: El mismo sistema puede resolver diferentes variables dadas otras conocidas, lo que aumenta su flexibilidad.

4. **"La agenda gestiona el tiempo en simulaciones"**: Es esencial para modelar sistemas donde el orden de los eventos es crucial.

5. **"La memoización transforma la complejidad algorítmica"**: Convierte procesos exponenciales en procesos lineales mediante almacenamiento inteligente.

> "El estado es necesario para modelar el mundo real, pero debemos administrarlo con cuidado. La clave está en encapsular el estado de manera que los efectos secundarios sean predecibles y controlados."

---

## **9. Consejos para Estudiar**

1. **Dibuja diagramas de caja-puntero**: Visualiza cómo se representan las estructuras mutables y cómo los cambios afectan a las estructuras compartidas.

2. **Implementa sistemas pequeños**: Crea tu propia implementación de colas, sistemas de restricciones y tablas.

3. **Analiza el flujo de información**: En sistemas de restricciones, rastrea cómo se propagan los valores a través de los conectores.

4. **Compara enfoques**: Implementa el mismo problema con y sin mutación para entender las diferencias.

5. **Practica con ejercicios clave**:
   - Implementa un sistema de restricciones para conversiones de unidades
   - Crea una agenda de simulación para un sistema de eventos discretos
   - Escribe una versión memoizada de una función recursiva compleja

6. **Enfócate en los invariantes**: Para estructuras como colas, identifica qué condiciones deben mantenerse siempre verdaderas.

Este resumen cubre los conceptos esenciales del Capítulo 3 de SICP, enfocándose en cómo manejar el estado y la mutación en programas, y cómo diseñar sistemas modulares con comportamiento dinámico. ¡Dominar estos conceptos es fundamental para construir sistemas complejos y realistas! 

¡Fin del Capítulo 3!

[⏮️ **Capítulo Anterior: Building Abstractions with Data**](tema2.md)  
[⏭️ **Siguiente Capítulo: Metalinguistic Abstraction**](tema4.md)

