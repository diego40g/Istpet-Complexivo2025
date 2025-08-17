# Topologías de red

## 1. Matemáticas de redes

### Sistema binario

#### Conceptos fundamentales:
El sistema binario es la base de toda la computación y comunicaciones digitales, utilizando únicamente dos dígitos: 0 y 1.

#### Conversión decimal a binario:
```
Ejemplo: 192 en binario
192 ÷ 2 = 96 resto 0
96 ÷ 2 = 48 resto 0
48 ÷ 2 = 24 resto 0
24 ÷ 2 = 12 resto 0
12 ÷ 2 = 6 resto 0
6 ÷ 2 = 3 resto 0
3 ÷ 2 = 1 resto 1
1 ÷ 2 = 0 resto 1

192₁₀ = 11000000₂
```

#### Conversión binario a decimal:
```
Ejemplo: 11000000₂ a decimal
1×2⁷ + 1×2⁶ + 0×2⁵ + 0×2⁴ + 0×2³ + 0×2² + 0×2¹ + 0×2⁰
128 + 64 + 0 + 0 + 0 + 0 + 0 + 0 = 192₁₀
```

#### Operaciones binarias:
**Suma binaria:**
```
  0 + 0 = 0
  0 + 1 = 1
  1 + 0 = 1
  1 + 1 = 10 (0 con acarreo 1)
```

**Aplicación en redes:** Direcciones IP, máscaras de subred, cálculos de VLSM

### Sistema decimal

#### Base 10:
Utiliza dígitos del 0 al 9, cada posición representa una potencia de 10.

#### Conversión y representación:
```
Ejemplo: 3.456
3×10³ + 4×10² + 5×10¹ + 6×10⁰
3000 + 400 + 50 + 6 = 3.456
```

#### Aplicación en redes:
- Direcciones IP en notación decimal punteada (192.168.1.1)
- Configuración de parámetros de red
- Medidas de ancho de banda (Mbps, Gbps)

### Sistema hexadecimal

#### Base 16:
Utiliza dígitos 0-9 y letras A-F (A=10, B=11, C=12, D=13, E=14, F=15)

#### Conversión decimal a hexadecimal:
```
Ejemplo: 255 en hexadecimal
255 ÷ 16 = 15 resto 15 (F)
15 ÷ 16 = 0 resto 15 (F)

255₁₀ = FF₁₆
```

#### Conversión hexadecimal a decimal:
```
Ejemplo: FF₁₆ a decimal
F×16¹ + F×16⁰
15×16 + 15×1 = 240 + 15 = 255₁₀
```

#### Aplicación en redes:
- Direcciones MAC (00:1A:2B:3C:4D:5E)
- Direcciones IPv6 (2001:0db8:85a3::8a2e:0370:7334)
- Configuración de VLANs
- Análisis de paquetes en Wireshark

## 2. Terminología de Networking

### Términos fundamentales:

#### Host/Node (Nodo):
Cualquier dispositivo conectado a una red que puede enviar o recibir datos.
- Ejemplos: Computadoras, servidores, impresoras, smartphones

#### Bandwidth (Ancho de banda):
Capacidad máxima de transmisión de datos de un enlace de comunicación.
- Se mide en bits por segundo (bps, Kbps, Mbps, Gbps)
- No confundir con throughput (rendimiento real)

#### Latencia:
Tiempo que tarda un paquete en viajar desde el origen hasta el destino.
- Se mide en milisegundos (ms)
- Afecta especialmente a aplicaciones en tiempo real

#### Throughput (Rendimiento):
Cantidad real de datos transmitidos exitosamente por unidad de tiempo.
- Siempre menor o igual al bandwidth
- Afectado por congestión, errores, protocolo overhead

#### Packet (Paquete):
Unidad básica de datos transmitida en una red de conmutación de paquetes.
- Contiene datos del usuario y información de control
- Incluye direcciones de origen y destino

#### Frame (Trama):
Estructura de datos en la capa de enlace que encapsula paquetes.
- Específica para cada tecnología (Ethernet, Wi-Fi)
- Incluye headers y trailers para control

### Dispositivos de red:

#### Hub:
- Dispositivo de capa física (Layer 1)
- Repite señales a todos los puertos
- Crea un solo dominio de colisión
- Obsoleto en redes modernas

#### Switch:
- Dispositivo de capa de enlace (Layer 2)
- Aprende direcciones MAC
- Cada puerto es un dominio de colisión separado
- Base de las LANs modernas

#### Router:
- Dispositivo de capa de red (Layer 3)
- Enruta paquetes entre diferentes redes
- Separa dominios de broadcast
- Implementa protocolos de enrutamiento

#### Access Point (AP):
- Proporciona acceso inalámbrico a LAN cableada
- Convierte entre 802.11 y 802.3
- Puede incluir funciones de routing (router inalámbrico)

## 3. Componentes de una red Ethernet

### Historia de Ethernet:
- **1973**: Desarrollado por Bob Metcalfe en Xerox PARC
- **1980**: Estándar DIX (DEC, Intel, Xerox)
- **1983**: Estándar IEEE 802.3
- **Presente**: Base de la mayoría de LANs

### Características de Ethernet:

#### CSMA/CD (Carrier Sense Multiple Access/Collision Detection):
1. **Carrier Sense**: Escuchar antes de transmitir
2. **Multiple Access**: Múltiples dispositivos pueden acceder al medio
3. **Collision Detection**: Detectar colisiones durante la transmisión

#### Formato de trama Ethernet:
```
|Preámbulo|SFD|Dest MAC|Src MAC|Type/Len|Payload|FCS|
|7 bytes  |1  |6 bytes |6 bytes|2 bytes |46-1500|4  |
```

- **Preámbulo**: Sincronización (7 bytes de 10101010)
- **SFD**: Start Frame Delimiter (10101011)
- **Direcciones MAC**: 48 bits cada una
- **Type/Length**: Tipo de protocolo o longitud
- **Payload**: Datos (46-1500 bytes)
- **FCS**: Frame Check Sequence (CRC-32)

### Estándares Ethernet:

#### 10Base-T (10 Mbps):
- Medio: Par trenzado categoría 3
- Distancia: 100 metros
- Topología: Estrella con hubs

#### 100Base-TX (Fast Ethernet):
- Medio: Par trenzado categoría 5
- Distancia: 100 metros
- Topología: Estrella con switches

#### 1000Base-T (Gigabit Ethernet):
- Medio: Par trenzado categoría 5e/6
- Distancia: 100 metros
- 4 pares utilizados simultáneamente

#### 10GBase-T:
- Medio: Par trenzado categoría 6a/7
- Distancia: 100 metros
- Frecuencia: Hasta 500 MHz

## 4. Modelos de Red

### Grupo de trabajo (Workgroup)

#### Características:
- **Descentralizado**: Sin servidor dedicado
- **Peer-to-peer**: Cada computadora puede ser cliente y servidor
- **Pequeña escala**: Típicamente 2-10 usuarios
- **Administración local**: Cada usuario administra su máquina

#### Ventajas:
- Bajo costo de implementación
- Fácil configuración para redes pequeñas
- No requiere servidor dedicado
- Cada usuario controla sus recursos

#### Desventajas:
- Difícil administración en redes grandes
- Seguridad limitada
- No hay backup centralizado
- Dependiente de que las máquinas estén encendidas

#### Ejemplo de configuración:
```
Workgroup: OFICINA
├── PC-JUAN (recursos compartidos: Documentos, Impresora)
├── PC-MARIA (recursos compartidos: Fotos, Scanner)
└── PC-CARLOS (recursos compartidos: Videos, Impresora)
```

### Dominio

#### Características:
- **Centralizado**: Servidor de dominio (Domain Controller)
- **Autenticación centralizada**: Single Sign-On (SSO)
- **Mayor escala**: Cientos o miles de usuarios
- **Administración centralizada**: Políticas y permisos centralizados

#### Componentes principales:
- **Domain Controller (DC)**: Servidor que autentica usuarios
- **Active Directory**: Base de datos de objetos del dominio
- **DNS**: Resolución de nombres del dominio
- **DHCP**: Asignación automática de IPs

#### Ventajas:
- Administración centralizada
- Seguridad robusta
- Políticas de grupo
- Backup centralizado
- Escalabilidad

#### Desventajas:
- Mayor costo inicial
- Complejidad de configuración
- Dependencia del servidor de dominio
- Requiere administrador especializado

#### Estructura de dominio:
```
Dominio: empresa.local
├── Domain Controller (DC01)
├── Member Servers
│   ├── File Server
│   ├── Print Server
│   └── Application Server
└── Client Computers
    ├── Workstations
    └── Laptops
```

## 5. Topologías físicas de redes

### Estrella

#### Descripción:
Todos los dispositivos se conectan a un punto central (hub/switch).

#### Ventajas:
- Fácil instalación y configuración
- Fácil detección de fallas
- Una falla no afecta al resto
- Fácil agregar/quitar dispositivos

#### Desventajas:
- Punto único de falla (dispositivo central)
- Mayor cantidad de cable necesario
- Limitado por puertos del dispositivo central

#### Aplicaciones:
- LANs Ethernet modernas
- Redes domésticas
- Redes de oficina pequeña/mediana

### Anillo

#### Descripción:
Los dispositivos se conectan en forma circular, cada uno conectado a dos vecinos.

#### Características:
- Token passing para control de acceso
- Datos viajan en una dirección
- Cada nodo regenera la señal

#### Ventajas:
- No hay colisiones
- Acceso equitativo al medio
- Rendimiento predecible

#### Desventajas:
- Una falla puede afectar toda la red
- Difícil agregar/quitar nodos
- Latencia variable según posición

#### Tecnologías:
- Token Ring (IEEE 802.5)
- FDDI (Fiber Distributed Data Interface)

### Bus

#### Descripción:
Todos los dispositivos conectados a un cable común (backbone).

#### Características:
- Topología lineal
- Terminadores en los extremos
- Half-duplex

#### Ventajas:
- Fácil instalación
- Cantidad mínima de cable
- Bajo costo

#### Desventajas:
- Una falla en el cable afecta toda la red
- Colisiones frecuentes
- Difícil detectar problemas
- Performance degrada con más nodos

#### Tecnologías históricas:
- 10Base-2 (Coaxial delgado)
- 10Base-5 (Coaxial grueso)

### Árbol

#### Descripción:
Combinación de topologías estrella conectadas en jerarquía.

#### Características:
- Estructura jerárquica
- Raíz, ramas y hojas
- Escalabilidad modular

#### Ventajas:
- Escalable
- Fácil mantenimiento
- Aislamiento de fallas por segmento
- Soporta diferentes velocidades por nivel

#### Desventajas:
- Dependiente de nodos superiores
- Mayor complejidad de cableado
- Posibles cuellos de botella en niveles altos

### Malla

#### Descripción:
Múltiples conexiones entre nodos para redundancia.

#### Tipos:
**Malla completa**: Todos los nodos conectados entre sí
- n(n-1)/2 enlaces necesarios
- Máxima redundancia

**Malla parcial**: Solo algunos nodos con múltiples conexiones
- Balance entre costo y redundancia
- Rutas alternativas para tráfico crítico

#### Ventajas:
- Alta confiabilidad
- Múltiples rutas para los datos
- Excelente rendimiento
- Tolerancia a fallas

#### Desventajas:
- Alto costo de implementación
- Compleja configuración
- Gran cantidad de cable/interfaces

#### Aplicaciones:
- Redes WAN de backbone
- Redes críticas (militares, financieras)
- Internet (malla parcial)

## 6. Modelos de Capas

### Modelo ISO/OSI (7 capas)

#### Capa 7 - Aplicación:
- **Función**: Interfaz con aplicaciones de usuario
- **Protocolos**: HTTP, FTP, SMTP, DNS, DHCP
- **Ejemplos**: Navegadores web, clientes de email

#### Capa 6 - Presentación:
- **Función**: Formato, cifrado, compresión de datos
- **Servicios**: SSL/TLS, JPEG, ASCII, EBCDIC
- **Propósito**: Traducción entre formatos

#### Capa 5 - Sesión:
- **Función**: Establecer, mantener y terminar sesiones
- **Servicios**: NetBIOS, SQL sessions, RPC
- **Control**: Checkpoints, recovery

#### Capa 4 - Transporte:
- **Función**: Entrega confiable de datos extremo a extremo
- **Protocolos**: TCP (confiable), UDP (no confiable)
- **Servicios**: Segmentación, control de flujo, recuperación de errores

#### Capa 3 - Red:
- **Función**: Enrutamiento de paquetes
- **Protocolos**: IP, ICMP, ARP, routing protocols
- **Dispositivos**: Routers, Layer 3 switches

#### Capa 2 - Enlace de datos:
- **Función**: Control de acceso al medio, detección de errores
- **Protocolos**: Ethernet, Wi-Fi, PPP
- **Dispositivos**: Switches, bridges, APs

#### Capa 1 - Física:
- **Función**: Transmisión de bits sobre medio físico
- **Especificaciones**: Voltajes, conectores, cables
- **Dispositivos**: Hubs, repetidores, cables

### Modelo TCP/IP (4 capas)

#### Capa de Aplicación:
- **Equivale a**: OSI capas 5, 6, 7
- **Protocolos**: HTTP, FTP, SMTP, DNS, DHCP, SSH
- **Función**: Servicios de red para aplicaciones

#### Capa de Transporte:
- **Equivale a**: OSI capa 4
- **Protocolos**: TCP, UDP
- **Función**: Comunicación extremo a extremo

#### Capa de Internet:
- **Equivale a**: OSI capa 3
- **Protocolos**: IP, ICMP, ARP
- **Función**: Enrutamiento entre redes

#### Capa de Acceso a Red:
- **Equivale a**: OSI capas 1, 2
- **Tecnologías**: Ethernet, Wi-Fi, Frame Relay
- **Función**: Acceso al medio físico

## 7. Diferencias entre el modelo OSI y TCP/IP

### Comparación detallada:

| Aspecto | OSI | TCP/IP |
|---------|-----|--------|
| **Capas** | 7 capas | 4 capas |
| **Desarrollo** | ISO (teórico) | DARPA (práctico) |
| **Uso** | Modelo de referencia | Implementación real |
| **Flexibilidad** | Más detallado | Más práctico |
| **Adopción** | Educativo | Internet real |

### Ventajas del modelo OSI:
- Mayor detalle y granularidad
- Mejor para educación y comprensión
- Separación clara de funciones
- Estándar internacional reconocido

### Ventajas del modelo TCP/IP:
- Probado en implementación real
- Base de Internet
- Más simple de entender
- Eficiente en la práctica

### Mapeo entre modelos:
```
OSI                    TCP/IP
+------------------+   +------------------+
|   Aplicación     |   |                  |
+------------------+   |    Aplicación    |
|   Presentación   |   |                  |
+------------------+   |                  |
|     Sesión       |   |                  |
+------------------+   +------------------+
|    Transporte    |   |    Transporte    |
+------------------+   +------------------+
|       Red        |   |     Internet     |
+------------------+   +------------------+
|  Enlace de Datos |   |                  |
+------------------+   |  Acceso a Red    |
|      Física      |   |                  |
+------------------+   +------------------+
```

## Laboratorios Prácticos

### Laboratorio 1: Conversiones numéricas
1. Convertir direcciones IP entre decimal y binario
2. Calcular máscaras de subred en diferentes notaciones
3. Trabajar con direcciones MAC en hexadecimal

### Laboratorio 2: Análisis de topologías
1. Identificar topologías en redes existentes
2. Diseñar topologías para diferentes escenarios
3. Simular fallas en diferentes topologías

### Laboratorio 3: Modelos de capas
1. Usar Wireshark para identificar protocolos por capa
2. Analizar encapsulación de datos
3. Mapear protocolos reales a modelos OSI/TCP-IP

## Actividades de Evaluación

1. **Cálculos**: Conversiones entre sistemas numéricos
2. **Diseño**: Proponer topología para empresa mediana
3. **Análisis**: Comparar modelos de red (workgroup vs dominio)
4. **Investigación**: Evolución de Ethernet y tecnologías futuras

## Recursos Adicionales

- Calculadoras de subredes online
- Simuladores de redes (Packet Tracer, GNS3)
- Analizadores de protocolo (Wireshark)
- Documentación IEEE 802.3 para Ethernet

[⬅️ Anterior: Introducción a las redes de computadoras.](./IntroduccionRedes.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Medios de Comunicación. ➡️](./MediosComunicacion.md)