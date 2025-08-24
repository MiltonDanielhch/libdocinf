# Resumen del Capítulo 3: Sistemas Operativos

## Introducción
Un sistema operativo es el software que controla la operación general de una computadora. Transforma el hardware en una herramienta útil al coordinar actividades internas y gestionar la comunicación con el mundo exterior. Los sistemas operativos más conocidos incluyen Windows, UNIX, Linux, Mac OS y Solaris.

## 3.1 Historia de los Sistemas Operativos

### Evolución:
- **Décadas de 1940-1950**: Computadoras grandes y poco flexibles que requerían preparación manual para cada programa (trabajo o "job").
- **Procesamiento por lotes (batch processing)**: Surgió para simplificar la configuración del programa. Los usuarios entregaban sus trabajos a un operador que los ejecutaba en grupo.
  - *Cola de trabajos (job queue)*: Estructura FIFO (primero en entrar, primero en salir) donde los trabajos esperan ejecución.
  - *Lenguaje de control de trabajos (JCL)*: Instrucciones para preparar la máquina para trabajos específicos.

- **Procesamiento interactivo**: Permitió a los usuarios interactuar directamente con programas mediante terminales remotos.
- **Tiempo real (real-time processing)**: Procesamiento que debe cumplir plazos externos específicos.
- **Compartición de tiempo (time-sharing)**: Sistema que permite a múltiples usuarios compartir una computadora simultáneamente mediante *multiprogramación*.
  - *Multiprogramación*: Divide el tiempo en intervalos y ejecuta cada trabajo solo durante un intervalo.
  - *Multitarea (multitasking)*: Similar a time-sharing pero para un solo usuario ejecutando múltiples tareas.

- **Sistemas embebidos**: Sistemas dedicados a tareas específicas (dispositivos médicos, electrónica de vehículos, teléfonos celulares). Ejemplos: VxWORKS, Windows CE, QNX.

## 3.2 Arquitectura del Sistema Operativo

### Clasificación del software:
- **Software de aplicación**: Programas para tareas específicas (hojas de cálculo, sistemas de bases de datos, juegos).
- **Software de sistema**: Realiza tareas comunes a los sistemas informáticos en general.
  - *Sistema operativo*: Núcleo del software de sistema.
  - *Software de utilidad*: Extiende o personaliza las capacidades del sistema operativo (formato de disco, compresión de datos, reproducción multimedia).

### Componentes del sistema operativo:
- **Interfaz de usuario (User Interface)**:
  - *Shell*: Interfaces basadas en texto (línea de comandos).
  - *GUI (Interfaz Gráfica de Usuario)*: Representación pictórica de objetos mediante iconos.
  - *Administrador de ventanas*: Asigna espacios en pantalla (ventanas) y controla qué aplicación está asociada con cada una.

- **Kernel (Núcleo)**:
  - *Administrador de archivos (File Manager)*: Coordina el uso del almacenamiento masivo, mantiene registros de archivos y permite organizarlos en directorios y subdirectorios.
  - *Controladores de dispositivo (Device Drivers)*: Software que se comunica con controladores de dispositivos periféricos.
  - *Administrador de memoria (Memory Manager)*: Coordina el uso de la memoria principal, implementa *memoria virtual* mediante *paginación*.
  - *Planificador (Scheduler)*: Mantiene un registro de procesos, introduce nuevos procesos y los elimina cuando terminan.
  - *Despachador (Dispatcher)*: Supervisa la ejecución de los procesos programados.

### Arranque del sistema (Booting):
- **Proceso de arranque (Boot strapping)**: Transfiere el sistema operativo del almacenamiento masivo a la memoria principal.
- **Cargador de arranque (Boot loader)**: Programa almacenado en ROM que dirige la CPU a transferir el sistema operativo a la memoria volátil.
- **Firmware**: Software almacenado en memoria no volátil (como BIOS, EFI) que realiza operaciones fundamentales de E/S.

## 3.3 Coordinación de Actividades de la Máquina

### Concepto de proceso:
- **Programa vs. Proceso**: Un programa es un conjunto estático de instrucciones, mientras que un proceso es la actividad dinámica de ejecutar un programa.
- **Estado del proceso**: Incluye la posición actual en el programa (contador de programa) y los valores en los registros de la CPU y celdas de memoria.

### Administración de procesos:
- **Tabla de procesos**: Bloque de información en memoria principal que registra todos los procesos.
- **Proceso listo**: Puede continuar su progreso.
- **Proceso en espera**: Su progreso se retrasa hasta que ocurra un evento externo.
- **Conmutación de procesos (Process switch/Context switch)**: Procedimiento para cambiar de un proceso a otro.
- **Interrupciones**: Señales que indican el final de una rebanada de tiempo (time slice), causando que la CPU complete su ciclo actual, guarde su posición y ejecute un manejador de interrupciones.

## 3.4 Manejo de la Competencia entre Procesos

### Semáforos:
- **Semáforo**: Bandera (bit en memoria) utilizada para controlar el acceso a recursos no compartibles.
- **Región crítica**: Secuencia de instrucciones que debe ejecutarse por un solo proceso a la vez.
- **Exclusión mutua**: Requisito de que solo un proceso a la vez pueda ejecutar una región crítica.
- **Soluciones**:
  - Instrucciones de deshabilitar/habilitar interrupciones
  - Instrucción test-and-set (probar y establecer)

### Interbloqueo (Deadlock):
Condición en la que dos o más procesos están bloqueados porque cada uno espera un recurso que tiene otro proceso.
- **Condiciones necesarias para el interbloqueo**:
  1. Competencia por recursos no compartibles
  2. Solicitud de recursos de forma parcial (recibir algunos recursos y luego solicitar más)
  3. Una vez asignado un recurso, no puede recuperarse por la fuerza

- **Estrategias para manejar el interbloqueo**:
  - *Detección y corrección*: Detectar el interbloqueo y corregirlo recuperando recursos.
  - *Prevención*: Evitar que se cumplan una o más condiciones del interbloqueo.
  - *Spooling*: Técnica para hacer que los recursos no compartibles parezcan compartibles (ej.: almacenar datos para imprimir más tarde).

## 3.5 Seguridad

### Ataques desde el exterior:
- **Cuentas de usuario**: Registro con nombre, contraseña y privilegios.
- **Super usuario/Administrador**: Persona con acceso privilegiado para establecer cuentas y realizar mantenimiento.
- **Software de auditoría**: Registra y analiza actividades para detectar comportamientos destructivos.
- **Sniffing software**: Software que registra actividades y las reporta a un intruso.
- **Seguridad de contraseñas**: Importancia de usar contraseñas seguras y políticas de gestión.

### Ataques desde el interior:
- **Niveles de privilegio**: 
  - *Modo privilegiado*: CPU puede ejecutar todas las instrucciones.
  - *Modo no privilegiado*: Lista de instrucciones aceptables limitada.
- **Instrucciones privilegiadas**: Instrucciones disponibles solo en modo privilegiado (ej.: cambiar registros de límites de memoria).
- **Protección de memoria**: Registros especiales que almacenan límites superior e inferior del área de memoria asignada a un proceso.

## Conceptos Clave para Recordar
- **Virtual memory**: Memoria "ficticia" creada mediante paginación que hace creer al sistema que tiene más memoria principal de la que realmente tiene.
- **Time slice**: Segmento corto de tiempo (milisegundos o microsegundos) durante el cual se permite que un proceso ejecute.
- **Context switch**: Cambio de un proceso a otro.
- **Process state**: Instantánea del estado de una máquina en un momento dado.
- **Firmware**: Software almacenado en memoria no volátil que está entre el hardware y el software tradicional.
- **Multi-factor authentication**: Autenticación que requiere más de un tipo de evidencia (algo que el usuario sabe, algo que tiene, algo relacionado con quién es).

Este resumen cubre los conceptos fundamentales del capítulo 3 sobre sistemas operativos, ideal para prepararse para exámenes o para comprender los principios básicos de cómo funcionan los sistemas operativos.

---

¡Fin del Capítulo 3!

[⏮️ **Capítulo Anterior: Manipulación de Datos y Arquitectura de Computadoras**](tema2.md)  
[⏭️ **Siguiente Capítulo: Redes e Internet**](tema4.md)