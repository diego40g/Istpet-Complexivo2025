# Introducción a las redes de computadoras

## 1. Introducción a las Redes y Comunicaciones de Computadoras

### Arquitectura de Internet

#### ¿Qué es Internet?
Internet es una red global de redes interconectadas que utiliza protocolos estándar para permitir la comunicación entre millones de dispositivos en todo el mundo.

#### Componentes fundamentales:
- **Hosts/End systems**: Dispositivos conectados (computadoras, smartphones, servidores)
- **Links de comunicación**: Medios físicos que conectan dispositivos
- **Routers**: Dispositivos que dirigen el tráfico entre redes
- **Protocolos**: Reglas que gobiernan la comunicación
- **ISPs (Internet Service Providers)**: Proveedores de servicios de Internet

#### Estructura jerárquica de Internet:
```
Tier 1 ISPs (Backbone)
├── Tier 2 ISPs (Regionales)
│   ├── Tier 3 ISPs (Locales)
│   │   ├── Empresas
│   │   ├── Hogares
│   │   └── Instituciones educativas
│   └── Content Providers (Google, Netflix)
└── Internet Exchange Points (IXPs)
```

#### Servicios de Internet:
- **Servicios de infraestructura**: Conectividad básica IP
- **Servicios de aplicación**: Web, email, streaming, etc.

### Redes convergentes

#### Definición:
Las redes convergentes integran múltiples tipos de tráfico (datos, voz, video) sobre una única infraestructura de red, típicamente basada en IP.

#### Características principales:
- **Integración de servicios**: Voz, datos y video en una sola red
- **Eficiencia de costos**: Menor infraestructura física necesaria
- **Administración simplificada**: Un solo sistema de gestión
- **Escalabilidad**: Fácil expansión y modificación

#### Beneficios de la convergencia:
1. **Reducción de costos**:
   - Menos equipamiento físico
   - Menor complejidad de cableado
   - Administración unificada

2. **Flexibilidad**:
   - Fácil reubicación de servicios
   - Adaptación rápida a cambios
   - Integración de nuevas tecnologías

3. **Productividad**:
   - Comunicaciones unificadas
   - Colaboración mejorada
   - Acceso móvil integrado

#### Desafíos:
- **Quality of Service (QoS)**: Priorización de tráfico crítico
- **Seguridad**: Protección de múltiples tipos de datos
- **Confiabilidad**: Disponibilidad alta para servicios críticos
- **Latencia**: Minimización de retrasos para aplicaciones sensibles

## 2. Conceptos de Redes de comunicación de datos

### Definiciones fundamentales:

#### Red de computadoras:
Sistema de dispositivos interconectados que pueden comunicarse y compartir recursos.

#### Comunicación de datos:
Proceso de transmisión de información digital entre dos o más dispositivos a través de un medio de comunicación.

#### Elementos básicos de comunicación:
1. **Emisor/Transmisor**: Dispositivo que envía la información
2. **Receptor**: Dispositivo que recibe la información
3. **Mensaje**: Información que se transmite
4. **Medio**: Canal físico por el que viaja la información
5. **Protocolo**: Reglas que gobiernan la comunicación

### Tipos de datos transmitidos:
- **Texto**: Documentos, mensajes, código
- **Números**: Datos numéricos, estadísticas
- **Imágenes**: Fotografías, gráficos, diagramas
- **Audio**: Música, voz, sonidos
- **Video**: Películas, conferencias, streaming

### Modos de transmisión:

#### Por dirección:
- **Simplex**: Comunicación en una sola dirección (radio, TV)
- **Half-duplex**: Comunicación bidireccional alternada (walkie-talkie)
- **Full-duplex**: Comunicación bidireccional simultánea (teléfono)

#### Por temporización:
- **Síncrona**: Transmisión con señal de reloj compartida
- **Asíncrona**: Transmisión sin señal de reloj compartida

#### Por paralelismo:
- **Serial**: Un bit a la vez
- **Paralelo**: Múltiples bits simultáneamente

## 3. Clasificación de las redes de datos

### Por área geográfica:

#### PAN (Personal Area Network)
- **Alcance**: 1-10 metros
- **Ejemplos**: Bluetooth, USB, FireWire
- **Dispositivos**: Smartphones, tablets, auriculares, impresoras personales
- **Tecnologías**: Bluetooth 5.0, USB-C, Wi-Fi Direct

#### LAN (Local Area Network)
- **Alcance**: Edificio o campus (hasta 2 km)
- **Ejemplos**: Red de oficina, laboratorio de computación
- **Tecnologías**: Ethernet, Wi-Fi (802.11)
- **Topologías**: Estrella, bus, anillo
- **Velocidades**: 10 Mbps - 10 Gbps

#### MAN (Metropolitan Area Network)
- **Alcance**: Ciudad o área metropolitana (hasta 50 km)
- **Ejemplos**: Red municipal, campus universitario distribuido
- **Tecnologías**: Fiber Distributed Data Interface (FDDI), WiMAX
- **Propósito**: Conectar múltiples LANs en una ciudad

#### WAN (Wide Area Network)
- **Alcance**: País, continente o mundial
- **Ejemplos**: Internet, redes corporativas multinacionales
- **Tecnologías**: MPLS, Frame Relay, ATM, SONET/SDH
- **Características**: Uso de infraestructura de telecomunicaciones públicas

### Por topología física:
- **Bus**: Todos los dispositivos conectados a un cable común
- **Estrella**: Dispositivos conectados a un hub/switch central
- **Anillo**: Dispositivos conectados en forma circular
- **Malla**: Múltiples conexiones entre dispositivos
- **Árbol**: Combinación de bus y estrella

### Por método de acceso:
- **Ethernet**: CSMA/CD (Carrier Sense Multiple Access/Collision Detection)
- **Wi-Fi**: CSMA/CA (Carrier Sense Multiple Access/Collision Avoidance)
- **Token Ring**: Paso de testigo

### Por propiedad:
- **Públicas**: Internet, redes de operadores
- **Privadas**: Redes corporativas, intranets
- **Híbridas**: Combinación de públicas y privadas (VPN)

## 4. Conceptos básicos de protocolos

### ¿Qué es un protocolo?
Un protocolo es un conjunto de reglas y estándares que definen cómo los dispositivos de red se comunican entre sí.

### Funciones de los protocolos:
1. **Formato de datos**: Cómo se estructuran los mensajes
2. **Sincronización**: Cuándo enviar mensajes
3. **Control de errores**: Cómo detectar y corregir errores
4. **Control de flujo**: Cómo regular la velocidad de transmisión
5. **Direccionamiento**: Cómo identificar origen y destino

### Clasificación de protocolos:

#### Por capa del modelo OSI:
- **Capa física**: Definición de señales eléctricas, conectores
- **Capa de enlace**: Ethernet, Wi-Fi, PPP
- **Capa de red**: IP, ICMP, ARP
- **Capa de transporte**: TCP, UDP
- **Capa de aplicación**: HTTP, FTP, SMTP

#### Por función:
- **Protocolos de enrutamiento**: RIP, OSPF, BGP
- **Protocolos de transporte**: TCP (confiable), UDP (no confiable)
- **Protocolos de aplicación**: HTTP/HTTPS, FTP, SMTP, DNS

### Protocolos fundamentales:

#### Internet Protocol (IP)
- **Propósito**: Direccionamiento y enrutamiento
- **Versiones**: IPv4 (32 bits), IPv6 (128 bits)
- **Características**: Sin conexión, no confiable, mejor esfuerzo

#### Transmission Control Protocol (TCP)
- **Propósito**: Transporte confiable de datos
- **Características**: 
  - Orientado a conexión
  - Control de flujo
  - Detección y corrección de errores
  - Orden garantizado de paquetes

#### User Datagram Protocol (UDP)
- **Propósito**: Transporte rápido de datos
- **Características**:
  - Sin conexión
  - Sin garantía de entrega
  - Menor overhead
  - Ideal para streaming y gaming

#### Hypertext Transfer Protocol (HTTP/HTTPS)
- **Propósito**: Transferencia de páginas web
- **Características**:
  - Sin estado
  - Basado en texto
  - HTTPS añade seguridad TLS/SSL

### Estándares y organizaciones:
- **IEEE**: Estándares de LAN (802.x)
- **IETF**: Protocolos de Internet (RFCs)
- **ITU-T**: Estándares de telecomunicaciones
- **ISO**: Modelo OSI y otros estándares

## Actividades Prácticas

### Laboratorio 1: Exploración de red local
```bash
# Comandos para explorar la red
ipconfig /all        # Windows - Configuración IP
ifconfig             # Linux/macOS - Interfaces de red
ping google.com      # Probar conectividad
tracert/traceroute   # Rastrear ruta de paquetes
netstat -an          # Conexiones activas
arp -a               # Tabla ARP
```

### Laboratorio 2: Análisis de protocolos
1. Usar Wireshark para capturar tráfico de red
2. Identificar diferentes protocolos en la captura
3. Analizar estructura de paquetes HTTP, TCP, IP
4. Observar el proceso de three-way handshake de TCP

### Ejercicio práctico: Diseño de red
1. Diseñar la topología para una pequeña empresa
2. Determinar los dispositivos necesarios
3. Seleccionar protocolos apropiados
4. Considerar aspectos de seguridad y rendimiento

## Evaluación

### Preguntas de repaso:
1. Explique la diferencia entre Internet e internet
2. ¿Cuáles son las ventajas de las redes convergentes?
3. Compare LAN, MAN y WAN en términos de alcance y tecnologías
4. ¿Por qué son importantes los protocolos en las redes?
5. Explique la diferencia entre TCP y UDP

### Proyecto: Investigación de tecnologías emergentes
- Investigar sobre 5G, IoT, Edge Computing
- Analizar su impacto en las redes actuales
- Presentar hallazgos en formato de presentación

## Recursos adicionales

### Lecturas recomendadas:
- RFC 791: Internet Protocol (IPv4)
- RFC 793: Transmission Control Protocol
- "Computer Networking: A Top-Down Approach" - Kurose & Ross

### Herramientas útiles:
- **Wireshark**: Analizador de protocolos
- **Packet Tracer**: Simulador de redes Cisco
- **GNS3**: Simulador de redes avanzado
- **Nmap**: Escáner de redes y puertos

### Sitios web útiles:
- Internet Engineering Task Force (IETF)
- IEEE Standards Association
- Cisco Networking Academy
- Network World magazine

[⬅️ Anterior: Administración y Gestión de macOS.](../Unidad1-SistemasOperativos/AdministracionMacOS.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Topologías de red. ➡️](./TopologiasRed.md)