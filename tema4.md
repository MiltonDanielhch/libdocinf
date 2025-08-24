# Resumen del Capítulo 4: Redes e Internet

## Introducción
Este capítulo explora los fundamentos de las redes informáticas y la Internet, explicando cómo las computadoras se conectan y comunican entre sí, y cómo ha evolucionado la World Wide Web. La conectividad de computadoras y smartphones a Internet ha facilitado la colaboración y el trabajo remoto mediante herramientas como correo electrónico, videoconferencias y aplicaciones de colaboración en la nube.

## 4.1 Fundamentos de las Redes

### Conceptos Básicos:
- **Red informática**: Sistema de comunicación que conecta computadoras y dispositivos para compartir información y recursos.
- **Protocolo**: Conjunto de reglas que regulan la comunicación entre dispositivos en una red.
- **Topologías de red**: Formas en que se organizan físicamente los dispositivos (estrella, bus, anillo, malla).

### Tipos de Redes:
- **LAN (Local Area Network)**: Cubre áreas pequeñas como oficinas o hogares.
- **WAN (Wide Area Network)**: Cubre áreas geográficas extensas, como Internet.
- **MAN (Metropolitan Area Network)**: Cubre una ciudad o área metropolitana.
- **PAN (Personal Area Network)**: Para dispositivos personales cercanos (Bluetooth).

### Tecnologías de Red:
- **Ethernet**: Tecnología cableada común para LAN que utiliza CSMA/CD (Carrier Sense Multiple Access with Collision Detection).
- **Wi-Fi**: Tecnología inalámbrica que utiliza CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance).
- **Routers**: Dispositivos que dirigen el tráfico entre diferentes redes.

## 4.2 La Arquitectura de Internet

### Estructura de Internet:
- **ISP (Proveedores de Servicios de Internet)**: Organizaciones que ofrecen acceso a Internet.
- **Backbone de Internet**: Infraestructura de alta velocidad que forma la espina dorsal de Internet.
- **Niveles de ISP**: ISP de nivel 1 (backbone global), nivel 2 (regionales) y nivel 3 (locales).

### Direcciones en Internet:
- **Dirección IP**: Identificador único para cada dispositivo en Internet (IPv4 e IPv6).
- **DNS (Domain Name System)**: Sistema que traduce nombres amigables (ej. google.com) a direcciones IP.
- **Registros de dominio**: Organizaciones que gestionan nombres de dominio (ICANN, registradores).

### Anticybersquatting Consumer Protection Act:
- Ley que limita el registro especulativo de nombres de dominio, especialmente aquellos relacionados con marcas existentes.

## 4.3 La World Wide Web

### Conceptos Clave:
- **Webpage (Página web)**: Documento codificado en HTML que se presenta en un navegador.
- **HTML (HyperText Markup Language)**: Lenguaje de marcado para crear páginas web.
- **URL (Uniform Resource Locator)**: Dirección única que identifica recursos en la Web.
- **Hipervínculos**: Enlaces que permiten navegar entre páginas web.

### Estructura HTML:
- **Encabezado (head)**: Contiene información preliminar sobre el documento (título, metadatos).
- **Cuerpo (body)**: Contiene el contenido visible de la página.
- **Etiquetas**: Elementos que definen la estructura y formato del contenido (ej. `<h1>`, `<p>`, `<a>`).

### Ejemplo de HTML básico:
```html
<html>
<head>
<title>Página de demostración</title>
</head>
<body>
<h1>Mi Página Web</h1>
<p>Haga clic <a href="http://crafty.com/demo.html">aquí</a> para otra página.</p>
</body>
</html>
```

## 4.4 Protocolos de Internet

### Modelo de Capas:
- **Capa de aplicación**: Interfaz con el usuario (HTTP, FTP, SMTP).
- **Capa de transporte**: Maneja la comunicación extremo a extremo (TCP, UDP).
- **Capa de red**: Enrutamiento de paquetes (IP).
- **Capa de enlace**: Comunicación en la red local (Ethernet, Wi-Fi).

### Proceso de Comunicación:
1. La capa de aplicación prepara el mensaje y proporciona la dirección de destino.
2. La capa de transporte divide el mensaje en segmentos.
3. La capa de red asigna direcciones intermedias a cada paquete.
4. La capa de enlace transfiere los paquetes físicamente.

### Sockets y Comunicación Cliente/Servidor:
- **Socket**: Punto final de comunicación en una red.
- **Cliente**: Solicita servicios (ej. navegador web).
- **Servidor**: Proporciona servicios (ej. servidor web).
- **Puertos**: Números que identifican aplicaciones específicas (ej. puerto 80 para HTTP).

## 4.5 Computación Distribuida

### Conceptos:
- **Sistemas distribuidos**: Múltiples computadoras trabajando juntas como un sistema unificado.
- **Cluster computing**: Varios ordenadores independientes trabajando estrechamente para proporcionar capacidad comparable a una máquina más grande.
- **Alta disponibilidad**: Característica de los sistemas distribuidos donde la falla de un nodo no detiene todo el sistema.

### Ventajas de los Sistemas Distribuidos:
- Costo menor comparado con supercomputadoras
- Mayor confiabilidad y menor costo de mantenimiento
- Escalabilidad (posibilidad de añadir más nodos según sea necesario)

## 4.6 Seguridad en Redes

### Amenazas Comunes:
- **Phishing**: Técnica para obtener información sensible haciéndose pasar por una entidad legítima.
- **Ciberataques**: Ataques maliciosos que buscan comprometer sistemas.

### Medidas de Seguridad:
- **Firewalls**: Sistemas que controlan el tráfico de red entrante y saliente.
- **Encriptación**: Protección de datos mediante algoritmos criptográficos.
- **Autenticación múltiple**: Requiere más de un tipo de verificación para acceder a sistemas.

## Conceptos Clave para Recordar
- **DNS (Domain Name System)**: Sistema que traduce nombres de dominio a direcciones IP.
- **URL (Uniform Resource Locator)**: Dirección única que identifica recursos en la Web.
- **HTML (HyperText Markup Language)**: Lenguaje estándar para crear páginas web.
- **TCP/IP**: Conjunto fundamental de protocolos que permite la comunicación en Internet.
- **Cliente/Servidor**: Modelo de arquitectura de red donde los clientes solicitan servicios y los servidores los proporcionan.
- **Socket**: Punto final de comunicación en una red que permite la transferencia de datos.

Este resumen cubre los conceptos fundamentales del Capítulo 4 sobre Redes e Internet, ideal para prepararse para exámenes o para comprender los principios básicos de cómo funcionan las redes informáticas y la Internet.

---

¡Fin del Capítulo 4!

[⏮️ **Capítulo Anterior: Sistemas Operativos**](tema3.md)  
[⏭️ **Siguiente Capítulo: Algoritmos**](tema5.md)