# Resumen Técnico en Español: *Structure and Interpretation of Computer Programs*

## Conceptos Fundamentales

### 1. Procesos vs. Procedimientos
- **Procedimiento**: Es la definición o descripción de cómo hacer algo (el código escrito).
- **Proceso**: Es la ejecución dinámica del procedimiento (lo que ocurre cuando se ejecuta el código).
- **Ejemplo clave**: Un procedimiento recursivo puede generar un proceso iterativo si se optimiza adecuadamente.
- **Problema común**: En lenguajes como C, Pascal o Ada, los procedimientos recursivos consumen memoria proporcional al número de llamadas, incluso cuando el proceso es iterativo en esencia.

### 2. Modelos de Evaluación
- **Evaluación de orden aplicativo**: Primero se evalúan todos los argumentos, luego se aplica el procedimiento.
- **Evaluación de orden normal**: Se sustituyen los operandos sin evaluarlos primero, expandiendo completamente antes de realizar cálculos.
- **Ejemplo ilustrativo**:
  ```scheme
  (define (p) (p))
  (define (test x y)
    (if (= x 0) 0 y))
  (test 0 (p))
  ```
  - En orden aplicativo: entra en bucle infinito (evalúa `(p)` primero)
  - En orden normal: devuelve 0 (nunca evalúa `(p)` porque el `if` no lo requiere)

### 3. Recursión
- **Recursión lineal**: 
  - Espacio y pasos crecen proporcionalmente al tamaño del problema (Θ(n))
  - Ejemplo: Cálculo recursivo del factorial
- **Recursión de árbol**:
  - Genera múltiples llamadas recursivas (como en Fibonacci)
  - Espacio Θ(n), pasos Θ(φⁿ) donde φ es la proporción áurea
  - Contiene cálculos redundantes (ej.: `(fib 3)` se calcula múltiples veces en `(fib 5)`)

### 4. Procedimientos de Alto Orden
- **Concepto clave**: Los procedimientos pueden:
  - Tomar otros procedimientos como argumentos
  - Devolver procedimientos como resultados
- **Ejemplos importantes**:
  - `average-damp`: Procedimiento que toma una función y devuelve su versión "amortiguada"
    ```scheme
    (define (average-damp f)
      (lambda (x) (average x (f x))))
    ```
  - `fixed-point`: Encuentra el punto fijo de una función
  - `sqrt` reformulado usando abstracciones:
    ```scheme
    (define (sqrt x)
      (fixed-point (average-damp (lambda (y) (/ x y))) 1.0))
    ```

### 5. Abstracción con `lambda` y `let`
- **`lambda`**: Crea procedimientos anónimos
  ```scheme
  (lambda (x) (+ x 1)) ; Incrementa en 1
  ```
- **`let`**: Sintaxis azucarada para variables locales
  ```scheme
  (let ((a (+ 1 (* x y)))
        (b (- 1 y)))
    (+ (* x (square a)) (* y b) (* a b)))
  ```
  Equivale a:
  ```scheme
  ((lambda (a b) (+ (* x (square a)) (* y b) (* a b)))
   (+ 1 (* x y)) (- 1 y))
  ```

### 6. Técnicas de Optimización
- **Exponenciación rápida** (`fast-expt`):
  - Enfoque ingenuo: Θ(n) pasos
  - Con cuadrados sucesivos: Θ(log n) pasos
  ```scheme
  (define (fast-expt b n)
    (cond ((= n 0) 1)
          ((even? n) (square (fast-expt b (/ n 2))))
          (else (* b (fast-expt b (- n 1))))))
  ```

### 7. Tests de Primalidad
- **Test de Fermat**:
  - Basado en el Pequeño Teorema de Fermat
  - Si n es primo y 0 < a < n, entonces aⁿ ≡ a (mod n)
  - Complejidad: Θ(log n)
  - **Limitación**: Los números de Carmichael pasan el test siendo compuestos
- **Test Miller-Rabin**:
  - Versión mejorada que no puede ser engañada por números de Carmichael

### 8. Métodos Numéricos
- **Búsqueda de puntos fijos**:
  - Para calcular raíces cuadradas: buscar punto fijo de y ↦ x/y
- **Método de Newton**:
  - Para encontrar ceros de funciones
  - Aplicado a raíces cuadradas: encontrar cero de y ↦ y² - x
  ```scheme
  (define (sqrt x)
    (newtons-method 
      (lambda (y) (- (square y) x)) 1.0))
  ```
- **Método de intervalo medio**:
  - Para encontrar raíces de funciones continuas
  - Ejemplo: `(half-interval-method sin 2.0 4.0)` aproxima π

## Vocabulario Técnico Clave en Español

| Término en Inglés | Traducción en Español | Definición |
|-------------------|------------------------|------------|
| Procedure | Procedimiento | Definición estática de un proceso |
| Process | Proceso | Ejecución dinámica de un procedimiento |
| Recursive | Recursivo | Que se llama a sí mismo |
| Iterative | Iterativo | Que usa variables de estado para repetir |
| Substitution model | Modelo de sustitución | Método para entender evaluación de procedimientos |
| Higher-order procedure | Procedimiento de alto orden | Toma o devuelve procedimientos |
| Lambda expression | Expresión lambda | Procedimiento anónimo |
| Fixed point | Punto fijo | Valor x donde f(x) = x |
| Primality test | Test de primalidad | Determina si un número es primo |
| Order of growth | Orden de crecimiento | Tasa de crecimiento de recursos usados |
| Normal-order evaluation | Evaluación de orden normal | Expande completamente antes de evaluar |
| Applicative-order evaluation | Evaluación de orden aplicativo | Evalúa argumentos primero |

## Frases Útiles para Estudiar

1. "La recursión de árbol genera un proceso cuyo número de pasos crece exponencialmente, mientras que el espacio requerido crece linealmente."

2. "El uso de procedimientos de alto orden nos permite expresar patrones comunes de computación como conceptos explícitos en nuestro lenguaje de programación."

3. "La técnica de amortiguación promedio (average damping) es crucial para hacer que algunos procesos de búsqueda de punto fijo converjan."

4. "La complejidad Θ(log n) significa que al duplicar el tamaño del problema, solo necesitamos una operación adicional."

5. "En Scheme, los símbolos como + y * están asociados con secuencias de instrucciones de máquina en el entorno global."

Este resumen cubre los conceptos esenciales de los primeros capítulos de SICP, enfocándose en los principios de programación funcional, análisis de procesos y técnicas de abstracción que son fundamentales para entender el enfoque del libro. ¡Es ideal para estudiantes que quieren dominar tanto los conceptos de programación como el vocabulario técnico en español!

¡Fin del Capítulo 1!

[⏮️ **Capítulo Anterior: Foreword y Prefacios**](resumen.md)  
[⏭️ **Siguiente Capítulo: Building Abstractions with Data**](tema2.md)