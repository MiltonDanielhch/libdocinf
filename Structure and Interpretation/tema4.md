# Resumen Completo: Sistemas de Consultas y Evaluación No Determinista  
## Basado en *Structure and Interpretation of Computer Programs* (Capítulo 4)

---

## **1. Introducción a los Sistemas de Consultas**

### **1.1. Concepto Básico**
- **Definición**: Un sistema de consultas permite hacer preguntas a una base de datos declarativa mediante patrones.
- **Característica clave**: Uso de **variables** (prefijadas con `?`) para representar partes desconocidas en los patrones.
- **Ejemplo básico**:
  ```scheme
  (job ?x (computer ?type))
  ```
  Busca todos los empleados cuyo trabajo está relacionado con computadoras.

### **1.2. Base de Datos de Hechos**
- **Estructura**: Colección de afirmaciones (assertions) en forma de listas:
  ```scheme
  (address (Bitdiddle Ben) (Slumerville (Ridge Road) 10))
  (job (Bitdiddle Ben) (computer wizard))
  (salary (Bitdiddle Ben) 60000)
  (supervisor (Bitdiddle Ben) (Warbucks Oliver))
  ```
- **Características**:
  - Los hechos se almacenan como patrones simples
  - Permite consultas complejas mediante combinación de patrones

### **1.3. Reglas de Inferencia**
- **Definición**: Mecanismo para derivar nuevos hechos a partir de hechos existentes.
- **Estructura**:
  ```scheme
  (rule (lives-near ?person-1 ?person-2)
        (and (address ?person-1 (?town . ?rest-1))
             (address ?person-2 (?town . ?rest-2))
             (not (same ?person-1 ?person-2))))
  ```
- **Proceso de aplicación**:
  1. Unificar la consulta con la conclusión de la regla
  2. Evaluar el cuerpo de la regla con la unificación resultante

---

## **2. Mecanismos de Búsqueda y Unificación**

### **2.1. Unificación**
- **Definición**: Proceso de hacer coincidir dos patrones determinando valores para las variables.
- **Casos**:
  - Ambos patrones son idénticos: unificación exitosa
  - Un patrón es una variable: se liga la variable al valor del otro patrón
  - Patrones compuestos: se unifica recursivamente cada elemento

### **2.2. Flujo de Datos en el Sistema de Consultas**
- **Modelo**: Flujo de marcos (frames) que representan conjuntos de ligaduras de variables.
- **Proceso**:
  1. La consulta inicial genera un marco vacío
  2. Cada operador de consulta transforma el flujo de marcos
  3. Los resultados son todos los marcos finales que satisfacen la consulta

### **2.3. Operadores de Consulta**
| **Operador** | **Función** | **Ejemplo** |
|--------------|-------------|-------------|
| `and` | Combina condiciones (intersección) | `(and (job ?x (computer programmer)) (supervisor ?x (Bitdiddle Ben)))` |
| `or` | Alternativas (unión) | `(or (supervisor ?x (Bitdiddle Ben)) (supervisor ?x (Hacker Alyssa P)))` |
| `not` | Negación | `(and (supervisor ?x (Bitdiddle Ben)) (not (job ?x (computer programmer))))` |
| `lisp-value` | Evaluación de expresiones Scheme | `(lisp-value > ?salary 30000)` |

### **2.4. Problemas de los Sistemas de Consultas**
- **Bucles infinitos**: Cuando las reglas se referencian mutuamente sin progreso
- **Consultas redundantes**: Múltiples caminos para derivar el mismo resultado
- **Eficiencia**: Búsqueda en grandes bases de datos puede ser costosa

---

## **3. Detectores de Bucles y Optimizaciones**

### **3.1. Necesidad de Detectores de Bucles**
- **Problema**: Algunas consultas pueden generar procesos infinitos al aplicar reglas recursivamente.
- **Ejemplo**:
  ```scheme
  (rule (outranked-by ?staff-person ?boss)
        (or (supervisor ?staff-person ?boss)
            (and (supervisor ?staff-person ?middle-manager)
                 (outranked-by ?middle-manager ?boss))))
  ```
  Sin detección de bucles, `(outranked-by (Bitdiddle Ben) ?who)` podría repetirse indefinidamente.

### **3.2. Implementación del Detector de Bucles**
- **Estrategia**: Mantener un historial de consultas ya procesadas.
- **Mecanismo**:
  - Antes de aplicar una regla, verificar si la consulta ya está en el historial
  - Si está presente, abortar esa rama de búsqueda
  - Si no, añadir la consulta al historial y continuar

### **3.3. Optimizaciones Clave**
- **Indexación de la base de datos**: Organizar hechos por tipo para búsquedas más rápidas
- **Ordenamiento de conjunciones**: Evaluar las condiciones más restrictivas primero
- **Evitar renombramiento innecesario**: Usar variables únicas solo cuando es necesario

---

## **4. Evaluación No Determinista con `amb`**

### **4.1. Concepto de No Determinismo**
- **Definición**: Capacidad de un programa para explorar múltiples caminos de ejecución.
- **Forma especial `amb`**:
  ```scheme
  (amb expr1 expr2 ... exprn)
  ```
  - Evalúa las expresiones de izquierda a derecha
  - Devuelve el valor de la primera que no falla
  - Si todas fallan, el programa falla

### **4.2. Mecanismo de Backtracking**
- **Proceso**:
  1. Se elige la primera alternativa de `amb`
  2. Si se alcanza un callejón sin salida (`(require false)`), se retrocede
  3. Se prueba la siguiente alternativa disponible
  4. Se repite hasta encontrar una solución o agotar todas las opciones

### **4.3. Ejemplo Clásico: Suma Prima**
```scheme
(define (prime-sum-pair list1 list2)
  (let ((a (an-element-of list1))
        (b (an-element-of list2)))
    (require (prime? (+ a b)))
    (list a b)))

(define (an-element-of items)
  (require (not (null? items)))
  (amb (car items) (an-element-of (cdr items))))
```
- **Funcionamiento**:
  - `an-element-of` usa `amb` para elegir elementos de una lista
  - `require` filtra combinaciones que no cumplen la condición
  - El evaluador automáticamente prueba combinaciones hasta encontrar una válida

---

## **5. Aplicaciones Avanzadas**

### **5.1. Análisis Sintáctico con `amb`**
- **Gramática simple**:
  ```scheme
  (define nouns '(student professor cat class))
  (define verbs '(studies lectures eats sleeps))
  (define articles '(the a))
  
  (define (parse-sentence)
    (list 'sentence
          (parse-noun-phrase)
          (parse-verb-phrase)))
  ```
- **Ventaja**: La ambigüedad sintáctica se maneja naturalmente con `amb`
- **Ejemplo**: La frase "The professor lectures to the student in the class" tiene múltiples interpretaciones

### **5.2. Sistema de Restricciones con `amb`**
- **Ejemplo**: Resolver ecuaciones
  ```scheme
  (define (solve)
    (let ((a (an-integer-between 1 10))
          (b (an-integer-between 1 10))
          (c (an-integer-between 1 10)))
      (require (= (+ (* a a) (* b b)) (* c c)))
      (list a b c)))
  ```
  Encuentra triples pitagóricos dentro de un rango

### **5.3. Programación Lógica Básica**
- **Similitud con Prolog**: El sistema de consultas implementa un subconjunto de programación lógica
- **Limitaciones**:
  - No incluye unificación completa
  - Carece de algunos optimizadores avanzados
  - Manejo limitado de negación

---

## **6. Implementación del Sistema de Consultas**

### **6.1. Estructura General**
- **Componentes principales**:
  1. **Motor de búsqueda**: Gestiona el flujo de marcos
  2. **Unificador**: Implementa el algoritmo de unificación
  3. **Base de datos**: Almacena y recupera hechos
  4. **Evaluador de reglas**: Aplica reglas recursivamente

### **6.2. Representación de Variables**
- **Variables únicas**: Para evitar conflictos en aplicaciones de reglas
  ```scheme
  (define (make-new-variable var rule-application-id)
    (cons '? (cons rule-application-id (cdr var))))
  ```
- **Renombramiento**: Cada aplicación de regla usa variables frescas

### **6.3. Procedimiento `qeval`**
- **Función central**: Evalúa una consulta en un flujo de marcos
  ```scheme
  (define (qeval query frame-stream)
    (let ((datum (query datum query)))
      (cond ((assertion-to-be-queried? query)
             (find-assertions query frame-stream))
            ((ramification? query)
             (apply-rules query frame-stream))
            ((and? query) 
             (eval-and (conjuncts query) frame-stream))
            ; ... otros casos
            )))
  ```

### **6.4. Procedimiento `apply-a-rule`**
- **Implementación clave**:
  ```scheme
  (define (apply-a-rule rule frame)
    (let ((unified-frame
           (unify-match (rule conclusion rule) query-pattern frame)))
      (if (succeed? unified-frame)
          (evaluate (rule body rule) unified-frame)
          fail)))
  ```

---

## **7. Vocabulario Técnico Esencial**

| **Término en Inglés** | **Traducción** | **Definición** |
|----------------------|---------------|---------------|
| Pattern matching | Coincidencia de patrones | Proceso de hacer coincidir consultas con hechos |
| Unification | Unificación | Algoritmo para ligar variables en patrones |
| Frame | Marco | Conjunto de ligaduras de variables |
| Rule | Regla | Mecanismo para derivar nuevos hechos |
| Backtracking | Retroceso | Estrategia para explorar alternativas cuando falla un camino |
| Non-determinism | No determinismo | Capacidad de explorar múltiples caminos de ejecución |
| Ambiguity | Ambigüedad | Situación donde hay múltiples interpretaciones válidas |
| Query stream | Flujo de consultas | Secuencia de resultados potenciales |

---

## **8. Principios Clave para Recordar**

1. **"Las consultas son patrones que buscan coincidencias"**: El sistema de consultas funciona mediante coincidencia de patrones en una base de datos declarativa.

2. **"Las reglas extienden el poder expresivo del sistema"**: Permiten definir relaciones complejas en términos de relaciones más simples.

3. **"El no determinismo simplifica la búsqueda en espacio de soluciones"**: `amb` encapsula el patrón de búsqueda con backtracking, liberando al programador de gestionar manualmente las alternativas.

4. **"La detección de bucles es esencial para la terminación"**: Sin mecanismos adecuados, los sistemas de reglas recursivas pueden entrar en bucles infinitos.

5. **"El flujo de marcos es el modelo de ejecución fundamental"**: Todas las operaciones de consulta transforman un flujo de marcos de ligaduras.

> "El sistema de consultas representa un estilo de programación declarativo, donde especificamos qué queremos en lugar de cómo calcularlo. Este enfoque es especialmente poderoso para problemas que implican búsqueda en espacios de soluciones complejas."

---

## **9. Consejos para Estudiar**

1. **Practica con ejemplos simples**: Comienza con consultas básicas antes de pasar a reglas complejas.

2. **Visualiza el flujo de marcos**: Dibuja diagramas que muestren cómo se transforma el flujo de marcos a través de operadores de consulta.

3. **Implementa un sistema simplificado**: Crea tu propia versión básica del sistema de consultas para entender los mecanismos internos.

4. **Analiza el proceso de unificación**: Sigue paso a paso cómo se ligarían variables en diferentes escenarios.

5. **Explora las limitaciones**: Investiga casos donde el sistema de consultas falla o es ineficiente.

6. **Compara con `amb`**: Entiende cómo ambos enfoques (sistema de consultas y evaluación no determinista) resuelven problemas similares con técnicas diferentes.

Este resumen cubre los conceptos esenciales del Capítulo 4 de SICP, enfocándose en sistemas de consultas declarativas y evaluación no determinista. ¡Estos conceptos son fundamentales para entender paradigmas avanzados de programación y resolver problemas complejos de búsqueda y razonamiento!

¡Fin del Capítulo 4!

[⏮️ **Capítulo Anterior: Modularity, Objects, and State**](tema3.md)  
[⏭️ **Siguiente Capítulo: Computing with Register Machines**](tema5.md)