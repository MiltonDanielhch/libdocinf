# Resumen Completo: Abstracción de Datos y Estructuras Complejas  
## Basado en *Structure and Interpretation of Computer Programs* (Capítulo 2)

---

## **1. Conceptos Fundamentales de Abstracción de Datos**

### **1.1. Abstracción de Datos**
- **Definición**: Técnica para ocultar los detalles de implementación de los datos, exponiendo solo una interfaz clara.
- **Objetivo**: Permitir que los programas se escriban independientemente de cómo se representan los datos concretamente.
- **Componentes clave**:
  - **Constructores**: Crean objetos de datos (ej.: `make-rat`, `make-complex`)
  - **Selectores**: Acceden a partes de los datos (ej.: `numer`, `denom`)
  - **Predicados**: Verifican propiedades de los datos (ej.: `rectangular?`, `polar?`)

### **1.2. Barrera de Abstracción**
- **Concepto**: Límite conceptual entre la implementación de un tipo de datos y su uso.
- **Ventajas**:
  - Permite cambiar la representación interna sin afectar el código que usa los datos
  - Facilita el trabajo en equipo (diferentes personas pueden trabajar en diferentes capas)
  - Reduce la complejidad cognitiva al aislar preocupaciones

> "La abstracción de datos es la metodología para estructurar sistemas de manera que gran parte del programa pueda especificarse independientemente de las elecciones realizadas en la implementación de los objetos de datos que manipula el programa."

---

## **2. Representación de Datos Compuestos**

### **2.1. Pares y Listas**
- **Par**: Estructura básica `(cons x y)` que combina dos elementos
- **Lista**: Secuencia de pares anidados terminada en `nil` (lista vacía)
- **Operaciones esenciales**:
  - `car`: Obtiene el primer elemento
  - `cdr`: Obtiene el resto de la lista
  - `cons`: Construye un nuevo par

### **2.2. Árboles**
- **Definición**: Estructura jerárquica donde cada nodo puede tener múltiples hijos
- **Representación**: Listas anidadas
- **Ejemplo de procedimiento recursivo**:
  ```scheme
  (define (count-leaves x)
    (cond ((null? x) 0)
          ((not (pair? x)) 1)
          (else (+ (count-leaves (car x))
                   (count-leaves (cdr x))))))
  ```

### **2.3. Mapas y Transformaciones**
- **`map`**: Aplica una función a cada elemento de una lista
- **`flatmap`**: Similar a `map` pero "aplanando" los resultados (útil para permutaciones y combinaciones)
- **Ejemplo de permutaciones**:
  ```scheme
  (define (permutations s)
    (if (null? s)
        (list nil)
        (flatmap (lambda (x)
                   (map (lambda (p) (cons x p))
                        (permutations (remove x s))))
                 s)))
  ```

---

## **3. Representaciones Múltiples y Tipos de Datos**

### **3.1. Sistemas de Tipos**
- **Problema**: ¿Cómo manejar múltiples representaciones para el mismo tipo abstracto de datos?
- **Solución**: Sistema de despacho basado en tipos
  - **Etiquetas de tipo**: Identifican la representación concreta (`rectangular`, `polar`)
  - **Tabla de operaciones**: Mapea (operación, tipo) → procedimiento concreto

### **3.2. Ejemplo: Números Complejos**
- **Dos representaciones**:
  - **Rectangular**: (real, imaginario)
  - **Polar**: (magnitud, ángulo)
- **Implementación con despacho**:
  ```scheme
  (define (real-part z)
    (cond ((rectangular? z) (real-part-rectangular (contents z)))
          ((polar? z) (real-part-polar (contents z)))
          (else (error "Unknown type -- REAL-PART" z))))
  ```

### **3.3. Ventajas del Sistema de Tipos**
- Permite añadir nuevas representaciones sin modificar el código existente
- Facilita la interoperabilidad entre diferentes representaciones
- Mantiene la modularidad en sistemas grandes

---

## **4. Conjuntos (Sets) y Estructuras de Datos Eficientes**

### **4.1. Representaciones de Conjuntos**
| **Representación** | **Características** | **Complejidad** |
|--------------------|---------------------|-----------------|
| **Lista no ordenada** | Elementos en cualquier orden | `element-of-set?`: Θ(n)<br>`intersection-set`: Θ(n²) |
| **Lista ordenada** | Elementos en orden ascendente | `element-of-set?`: Θ(n)<br>`intersection-set`: Θ(n) |
| **Árbol binario balanceado** | Estructura jerárquica | `element-of-set?`: Θ(log n)<br>`union-set`: Θ(n) |

### **4.2. Árboles Binarios**
- **Propiedades**:
  - Cada nodo tiene un valor, un subárbol izquierdo y uno derecho
  - En árboles de búsqueda, los valores izquierdos < nodo < valores derechos
- **Operaciones clave**:
  - `entry`: Obtiene el valor del nodo
  - `left-branch`, `right-branch`: Acceden a subárboles
  - `make-tree`: Construye un nuevo árbol

### **4.3. Conversión Lista-Árbol**
- **Procedimiento `list->tree`**:
  - Convierte una lista ordenada en un árbol binario balanceado
  - Complejidad: Θ(n) (tiempo lineal)
  - Usa estrategia divide-y-vencerás para balancear el árbol

---

## **5. Aplicaciones Avanzadas**

### **5.1. Códigos de Huffman**
- **Propósito**: Compresión de datos mediante códigos de longitud variable
- **Principio**: Símbolos frecuentes → códigos cortos; símbolos raros → códigos largos
- **Estructura de datos clave**: Árbol de Huffman
  - Hojas: Símbolos y frecuencias
  - Nodos internos: Suma de frecuencias de sus hijos
- **Procedimiento de construcción**:
  1. Crear hojas para cada símbolo
  2. Combinar las dos hojas/nodos con menor peso
  3. Repetir hasta tener un solo árbol

### **5.2. Diferenciación Simbólica**
- **Objetivo**: Calcular derivadas de expresiones algebraicas
- **Representación**: Listas que representan expresiones (ej.: `(+ x (* 3 x))`)
- **Reglas clave**:
  - Derivada de constante = 0
  - Derivada de variable = 1 si coincide con respecto a qué derivamos
  - Regla de la cadena para operaciones compuestas
- **Extensibilidad**: Sistema orientado a datos permite añadir nuevas reglas fácilmente

### **5.3. Lenguaje Pictórico**
- **Concepto**: Sistema para crear y combinar imágenes mediante operaciones de alto nivel
- **Abstracciones clave**:
  - **Marcos (frames)**: Definen sistema de coordenadas para imágenes
  - **Pintores (painters)**: Procedimientos que dibujan dentro de un marco
  - **Transformaciones**: Rotación, escalamiento, reflexión de imágenes
- **Operaciones de combinación**:
  - `beside`: Coloca imágenes lado a lado
  - `below`: Coloca imágenes una sobre otra
  - `flip-vert`, `flip-horiz`: Refleja imágenes

---

## **6. Técnicas de Programación Avanzadas**

### **6.1. Procedimientos de Alto Orden para Datos**
- **Patrones comunes**:
  - `map`: Transformar todos los elementos
  - `filter`: Seleccionar elementos que cumplen un predicado
  - `accumulate` (o `reduce`): Combinar elementos en un resultado único
- **Ejemplo de `accumulate`**:
  ```scheme
  (define (accumulate op initial sequence)
    (if (null? sequence)
        initial
        (op (car sequence)
            (accumulate op initial (cdr sequence)))))
  ```

### **6.2. Abstracción con `let` y `lambda`**
- **`lambda`**: Crea procedimientos anónimos
  ```scheme
  (lambda (x) (+ x 1)) ; Incrementa en 1
  ```
- **`let`**: Define variables locales
  ```scheme
  (let ((a (+ 1 (* x y)))
        (b (- 1 y)))
    (+ (* x (square a)) (* y b) (* a b)))
  ```

### **6.3. Programación Genérica**
- **Sistema de despacho de datos-dirigido**:
  ```scheme
  (define (deriv exp var)
    (cond ((number? exp) 0)
          ((variable? exp) (if (same-variable? exp var) 1 0))
          (else ((get 'deriv (operator exp)) (operands exp) var))))
  ```
- **Ventaja**: Permite añadir nuevas operaciones o tipos sin modificar el código existente

---

## **7. Vocabulario Técnico Esencial**

| **Término en Inglés** | **Traducción** | **Definición** |
|----------------------|---------------|---------------|
| Abstraction barrier | Barrera de abstracción | Límite entre implementación y uso de un tipo de datos |
| Constructor | Constructor | Procedimiento que crea instancias de un tipo de datos |
| Selector | Selector | Procedimiento que accede a componentes de un dato |
| Predicate | Predicado | Procedimiento que verifica propiedades (devuelve booleano) |
| Generic operation | Operación genérica | Función que funciona con múltiples representaciones |
| Tagged data | Datos etiquetados | Datos con información de su tipo incorporada |
| Prefix code | Código de prefijo | Sistema de codificación donde ningún código es prefijo de otro |
| Frame coordinate map | Mapa de coordenadas del marco | Transformación que mapea coordenadas unitarias a un marco |

---

## **8. Principios Clave para Recordar**

1. **"Programa para el interfaz, no para la implementación"**: El código debe depender de la interfaz de abstracción, no de los detalles concretos.

2. **"Las representaciones múltiples son inevitables en sistemas grandes"**: Un buen diseño de abstracción de datos facilita manejar esta complejidad.

3. **"La eficiencia depende de la representación"**: La elección de estructura de datos afecta drásticamente el rendimiento (ej.: listas vs. árboles para conjuntos).

4. **"Las operaciones genéricas permiten extensibilidad"**: Un sistema bien diseñado puede añadir nuevas representaciones sin modificar el código existente.

5. **"La recursión es natural para estructuras de datos recursivas"**: Los procedimientos que procesan árboles suelen ser recursivos en estructura.

> "La abstracción de datos no es solo una técnica de programación: es una forma de pensar sobre la complejidad. Al aislar las decisiones de representación, nos permitimos concentrarnos en el comportamiento esencial de los sistemas que construimos."

---

## **9. Consejos para Estudiar**

1. **Practica con ejemplos concretos**: Implementa sistemas pequeños de abstracción de datos (números racionales, vectores 2D).

2. **Visualiza las estructuras**: Dibuja diagramas de caja-apuntador para entender cómo se representan los datos.

3. **Enfócate en las barreras de abstracción**: Identifica claramente qué procedimientos pertenecen a cada capa.

4. **Compara representaciones**: Para un problema dado, implementa dos representaciones diferentes y compara sus ventajas.

5. **Implementa sistemas pequeños**: Crea un sistema de tipos simple con despacho basado en etiquetas.

6. **Analiza la complejidad**: Para cada operación, determina su complejidad algorítmica en términos del tamaño de los datos.

Este resumen cubre los conceptos esenciales del capítulo 2 de SICP, enfocándose en cómo construir sistemas mediante la abstracción de datos y cómo diseñar representaciones eficientes para estructuras de información complejas. ¡Dominar estos conceptos es fundamental para escribir programas modulares, mantenibles y eficientes!

¡Fin del Capítulo 2!

[⏮️ **Capítulo Anterior: The Elements of Programming**](tema1.md)  
[⏭️ **Siguiente Capítulo: Modularity, Objects, and State**](tema3.md)