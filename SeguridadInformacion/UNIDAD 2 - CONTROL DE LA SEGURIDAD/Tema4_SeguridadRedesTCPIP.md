# Tema 4: Seguridad en Redes TCP/IP

## Índice de Contenidos
1. [Fundamentos de TCP/IP](#fundamentos-de-tcpip)
2. [Vulnerabilidades del Protocolo TCP/IP](#vulnerabilidades-del-protocolo-tcpip)
3. [Protocolos de Seguridad](#protocolos-de-seguridad)
4. [IPSec](#ipsec)
5. [SSL/TLS](#ssltls)
6. [Fraudes y Malware en las Redes](#fraudes-y-malware-en-las-redes)

---

## Fundamentos de TCP/IP

### Arquitectura del Protocolo TCP/IP
```
Modelo TCP/IP vs Modelo OSI:
┌─────────────────────┬─────────────────────────┐
│ Modelo TCP/IP       │ Modelo OSI              │
├─────────────────────┼─────────────────────────┤
│ Aplicación          │ Aplicación              │
│                     │ Presentación            │
│                     │ Sesión                  │
├─────────────────────┼─────────────────────────┤
│ Transporte          │ Transporte              │
├─────────────────────┼─────────────────────────┤
│ Internet            │ Red                     │
├─────────────────────┼─────────────────────────┤
│ Acceso a Red        │ Enlace de Datos         │
│                     │ Física                  │
└─────────────────────┴─────────────────────────┘
```

### Protocolos Principales

#### Capa de Internet (IP)
**Internet Protocol (IP):**
- Direccionamiento lógico de hosts
- Enrutamiento de paquetes entre redes
- Fragmentación y reensamblado
- IPv4 (32 bits) vs IPv6 (128 bits)

**Estructura del Header IPv4:**
```
IPv4 Header (20 bytes mínimo):
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
├─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┼─┤
│Version│IHL│Type of Service│          Total Length           │
├───────┼───┼───────────────┼─────────────────────────────────┤
│        Identification      │Flags│      Fragment Offset    │
├─────────────────────────────┼─────┼─────────────────────────┤
│  Time to Live │  Protocol   │         Header Checksum     │
├───────────────┼─────────────┼─────────────────────────────┤
│                    Source Address                        │
├───────────────────────────────────────────────────────────┤
│                 Destination Address                      │
└───────────────────────────────────────────────────────────┘
```

**ICMP (Internet Control Message Protocol):**
- Mensajes de error y control
- Ping (Echo Request/Reply)
- Traceroute utilities
- Redirects y unreachable messages

#### Capa de Transporte
**TCP (Transmission Control Protocol):**
```
Características TCP:
├── Orientado a conexión (3-way handshake)
├── Confiable (acknowledgments y retransmisión)
├── Control de flujo (sliding window)
├── Control de congestión
├── Secuenciación de datos
└── Detección de errores (checksum)

TCP 3-Way Handshake:
Cliente                    Servidor
   │                          │
   ├─ SYN (seq=x) ──────────→ │
   │                          │
   │ ←────── SYN+ACK (seq=y,  ├─
   │               ack=x+1)   │
   │                          │
   ├─ ACK (seq=x+1, ──────────→ │
   │      ack=y+1)             │
   │                          │
  Conexión Establecida
```

**UDP (User Datagram Protocol):**
- Sin conexión (connectionless)
- No confiable (no acknowledgments)
- Menor overhead
- Ideal para aplicaciones en tiempo real

### Direccionamiento IP y Subnetting

#### Clases de Direcciones IPv4
```
Clases de Direcciones IPv4:
├── Clase A: 1.0.0.0 a 126.255.255.255
│   ├── Mask: 255.0.0.0 (/8)
│   └── Hosts: 16,777,214 por red
├── Clase B: 128.0.0.0 a 191.255.255.255
│   ├── Mask: 255.255.0.0 (/16)
│   └── Hosts: 65,534 por red
├── Clase C: 192.0.0.0 a 223.255.255.255
│   ├── Mask: 255.255.255.0 (/24)
│   └── Hosts: 254 por red
├── Clase D: 224.0.0.0 a 239.255.255.255 (Multicast)
└── Clase E: 240.0.0.0 a 255.255.255.255 (Experimental)

Direcciones Privadas (RFC 1918):
├── 10.0.0.0/8 (10.0.0.0 a 10.255.255.255)
├── 172.16.0.0/12 (172.16.0.0 a 172.31.255.255)
└── 192.168.0.0/16 (192.168.0.0 a 192.168.255.255)
```

#### CIDR (Classless Inter-Domain Routing)
- Notación de máscara con slash (/)
- Agregación de rutas más eficiente
- Reducción del tamaño de tablas de enrutamiento
- Mayor flexibilidad en asignación de direcciones

---

## Vulnerabilidades del Protocolo TCP/IP

### Vulnerabilidades Inherentes

#### Problemas de Diseño Original
**Falta de Autenticación:**
- No hay verificación de identidad de origen
- Facilita ataques de IP spoofing
- Confianza implícita en direcciones IP
- Ausencia de integridad de datos

**Falta de Confidencialidad:**
- Transmisión en texto claro
- Facilita eavesdropping (escuchas)
- Exposición de información sensible
- Vulnerabilidad a man-in-the-middle

#### Vulnerabilidades Específicas por Protocolo

**IP (Internet Protocol):**
```
Vulnerabilidades IP:
├── IP Spoofing
│   ├── Falsificación de dirección origen
│   ├── Bypass de filtros basados en IP
│   └── Facilitación de otros ataques
├── Fragmentación IP
│   ├── Fragment overlap attacks
│   ├── Tiny fragment attacks
│   └── Fragment flood attacks
└── Source Routing
    ├── Control de ruta por atacante
    ├── Bypass de firewalls
    └── Deprecated en implementaciones modernas
```

**TCP (Transmission Control Protocol):**
```
Vulnerabilidades TCP:
├── TCP Sequence Prediction
│   ├── Predicción de números de secuencia
│   ├── Session hijacking
│   └── Connection spoofing
├── SYN Flood Attacks
│   ├── Agotamiento de recursos del servidor
│   ├── Half-open connections
│   └── Denegación de servicio
├── TCP Reset Attacks
│   ├── Terminación forzada de conexiones
│   ├── Interferencia de comunicaciones
│   └── Censura de contenido
└── TCP Window Attacks
    ├── Manipulation de ventana de recepción
    ├── Degradación de performance
    └── Buffer overflow potential
```

**UDP (User Datagram Protocol):**
- UDP Flood attacks
- UDP Spoofing (más fácil que TCP)
- Amplification attacks
- Broadcast storms

### Ataques a Nivel de Red

#### IP Spoofing Attacks
**Técnicas de Spoofing:**
```
Tipos de IP Spoofing:
├── Blind Spoofing
│   ├── Atacante no puede ver respuestas
│   ├── Requiere predicción de secuencias
│   └── Más difícil pero posible
├── Non-blind Spoofing
│   ├── Atacante en mismo segmento de red
│   ├── Puede observar tráfico
│   └── Más fácil de ejecutar
└── Subnet Spoofing
    ├── Spoofing dentro de misma subred
    ├── ARP spoofing combinado
    └── Muy efectivo en LANs
```

**Contramedidas contra IP Spoofing:**
- Ingress/Egress filtering en routers
- Anti-spoofing rules en firewalls
- Network segmentation
- Uso de protocolos autenticados

#### Session Hijacking
**Proceso de Session Hijacking:**
1. **Monitoreo**: Captura de tráfico de sesión legítima
2. **Predicción**: Análisis de números de secuencia
3. **Sincronización**: Timing preciso para intercepción
4. **Inyección**: Inserción de comandos maliciosos
5. **Mantenimiento**: Control continuado de la sesión

---

## Protocolos de Seguridad

### Panorama de Protocolos Seguros
```
Protocolos de Seguridad por Capa:
├── Capa de Aplicación
│   ├── HTTPS (HTTP sobre TLS)
│   ├── FTPS (FTP sobre TLS)
│   ├── SMTPS (SMTP sobre TLS)
│   ├── SSH (Secure Shell)
│   └── PGP/GPG (Email encryption)
├── Capa de Transporte
│   ├── TLS (Transport Layer Security)
│   ├── SSL (Secure Sockets Layer) - Deprecated
│   └── DTLS (Datagram TLS)
├── Capa de Red
│   ├── IPSec (IP Security)
│   ├── L2TP (Layer 2 Tunneling Protocol)
│   └── GRE (Generic Routing Encapsulation)
└── Capa de Enlace
    ├── WPA2/WPA3 (WiFi security)
    ├── 802.1X (Port-based authentication)
    └── MACsec (Media Access Control Security)
```

### Servicios de Seguridad Fundamentales

#### Confidencialidad
**Cifrado Simétrico:**
- AES (Advanced Encryption Standard)
- ChaCha20 (stream cipher moderno)
- Claves compartidas de sesión
- Performance alto para grandes volúmenes

**Cifrado Asimétrico:**
- RSA (Rivest-Shamir-Adleman)
- ECDH (Elliptic Curve Diffie-Hellman)
- Intercambio seguro de claves
- Firma digital de mensajes

#### Integridad
**Funciones Hash:**
- SHA-256, SHA-3 (Secure Hash Algorithm)
- Blake2 (hash function moderno)
- Detección de modificaciones
- Verificación de integridad

**HMAC (Hash-based Message Authentication Code):**
- Combinación de hash con clave secreta
- Autenticación e integridad juntos
- Resistente a ataques de extensión
- Ampliamente implementado

#### Autenticación
**Certificados Digitales:**
- X.509 certificate format
- Public Key Infrastructure (PKI)
- Certificate Authorities (CAs)
- Certificate validation chains

**Autenticación Mutua:**
- Client certificates
- Pre-shared keys (PSK)
- Kerberos authentication
- RADIUS integration

---

## IPSec

### Arquitectura IPSec
```
Arquitectura IPSec:
├── Protocolos de Seguridad
│   ├── AH (Authentication Header)
│   │   ├── Autenticación del header IP
│   │   ├── Integridad de datos
│   │   └── No provee confidencialidad
│   └── ESP (Encapsulating Security Payload)
│       ├── Confidencialidad (cifrado)
│       ├── Autenticación opcional
│       └── Integridad de datos
├── Modos de Operación
│   ├── Transport Mode
│   │   ├── Solo payload cifrado
│   │   ├── Header IP original mantenido
│   │   └── Usado en host-to-host
│   └── Tunnel Mode
│       ├── Todo el paquete IP cifrado
│       ├── Nuevo header IP añadido
│       └── Usado en site-to-site VPNs
└── Gestión de Claves
    ├── IKE (Internet Key Exchange)
    ├── Manual key configuration
    └── Automatic key rotation
```

### Internet Key Exchange (IKE)

#### IKEv1 vs IKEv2
```
Comparación IKE:
┌─────────────────────┬─────────────────┬─────────────────┐
│ Característica      │ IKEv1           │ IKEv2           │
├─────────────────────┼─────────────────┼─────────────────┤
│ Fases               │ 2 fases         │ 1 fase          │
│ Mensajes Setup      │ 9 mensajes      │ 4 mensajes      │
│ NAT Traversal       │ Limitado        │ Nativo          │
│ DoS Protection      │ Básica          │ Mejorada        │
│ Mobility Support    │ No              │ Sí (MOBIKE)     │
│ Multiple Auth       │ Complejo        │ Simplificado    │
│ Error Reporting     │ Limitado        │ Robusto         │
└─────────────────────┴─────────────────┴─────────────────┘
```

#### Proceso de Negociación IKEv2
```
IKEv2 Exchange:
Initiator                    Responder
    │                            │
    ├─ IKE_SA_INIT ─────────────→│ (HDR, SAi1, KEi, Ni)
    │                            │
    │←─ IKE_SA_INIT ──────────────┤ (HDR, SAr1, KEr, Nr)
    │                            │
    ├─ IKE_AUTH ────────────────→│ (HDR, SK{IDi, AUTH, SAi2, TSi, TSr})
    │                            │
    │←─ IKE_AUTH ─────────────────┤ (HDR, SK{IDr, AUTH, SAr2, TSi, TSr})
    │                            │
   Túnel IPSec Establecido
```

### Configuración de VPNs con IPSec

#### Site-to-Site VPN
**Configuración Típica:**
```
VPN Site-to-Site:
Sitio A (192.168.1.0/24) ←→ Internet ←→ Sitio B (192.168.2.0/24)
      │                                        │
   Gateway A                              Gateway B
   (IPSec Peer)                          (IPSec Peer)

Parámetros de Configuración:
├── Peer IP addresses (public)
├── Authentication method (PSK/certificates)
├── Encryption algorithm (AES-256)
├── Hash algorithm (SHA-256)
├── DH Group (Group 14 o superior)
├── Local/Remote networks
└── Lifetime parameters
```

#### Remote Access VPN
**Características:**
- Cliente móvil a gateway corporativo
- Autenticación de usuario individual
- Asignación dinámica de IP
- Split tunneling configuration

### Algoritmos Criptográficos en IPSec

#### Suite de Cifrado Recomendada (2024)
```
Algoritmos Seguros:
├── Cifrado
│   ├── AES-256-GCM (preferido)
│   ├── AES-128-GCM
│   └── ChaCha20-Poly1305
├── Hash/Integridad
│   ├── SHA-256 (mínimo)
│   ├── SHA-384
│   └── SHA-512
├── DH Groups
│   ├── Group 19 (256-bit ECDH)
│   ├── Group 20 (384-bit ECDH)
│   └── Group 21 (521-bit ECDH)
└── PRF (Pseudo-Random Function)
    ├── HMAC-SHA-256
    └── HMAC-SHA-384
```

---

## SSL/TLS

### Evolución de SSL/TLS
```
Historia SSL/TLS:
├── SSL 1.0 (1994) - Nunca liberado públicamente
├── SSL 2.0 (1995) - Múltiples vulnerabilidades críticas
├── SSL 3.0 (1996) - Vulnerable a POODLE attack
├── TLS 1.0 (1999) - RFC 2246, vulnerable a BEAST
├── TLS 1.1 (2006) - RFC 4346, mejoras contra BEAST
├── TLS 1.2 (2008) - RFC 5246, ampliamente usado
└── TLS 1.3 (2018) - RFC 8446, versión actual recomendada
```

### Funcionamiento de TLS

#### TLS Handshake Process
```
TLS 1.2 Handshake:
Cliente                        Servidor
   │                               │
   ├─ Client Hello ──────────────→ │
   │  (versiones, cipher suites,   │
   │   random, extensions)         │
   │                               │
   │ ←──────────── Server Hello ───┤
   │               (versión elegida,│
   │                cipher suite,   │
   │                random)        │
   │                               │
   │ ←──────────── Certificate ────┤
   │                               │
   │ ←─── Server Key Exchange ─────┤ (si es necesario)
   │                               │
   │ ←─── Certificate Request ─────┤ (opcional)
   │                               │
   │ ←──── Server Hello Done ──────┤
   │                               │
   ├─ Certificate ───────────────→ │ (si fue solicitado)
   │                               │
   ├─ Client Key Exchange ───────→ │
   │                               │
   ├─ Certificate Verify ────────→ │ (si se envió cert)
   │                               │
   ├─ Change Cipher Spec ────────→ │
   │                               │
   ├─ Finished ──────────────────→ │
   │                               │
   │ ←──── Change Cipher Spec ─────┤
   │                               │
   │ ←─────────── Finished ────────┤
   │                               │
  Comunicación Cifrada Establecida
```

#### TLS 1.3 Improvements
```
TLS 1.3 Beneficios:
├── Handshake más rápido (1-RTT, 0-RTT)
├── Cipher suites simplificados
├── Perfect Forward Secrecy mandatorio
├── Eliminación de algoritmos débiles
├── Mejor resistencia a downgrade attacks
└── Latencia reducida significativamente
```

### Certificados Digitales

#### Estructura X.509
```
Certificado X.509:
├── Version (v3)
├── Serial Number (único por CA)
├── Signature Algorithm (RSA+SHA-256, ECDSA+SHA-256)
├── Issuer (Certificate Authority information)
├── Validity Period
│   ├── Not Before (fecha inicio)
│   └── Not After (fecha expiración)
├── Subject (información del titular)
├── Subject Public Key Info
│   ├── Algorithm (RSA, ECDSA)
│   └── Public Key
├── Extensions
│   ├── Key Usage (digital signature, key encipherment)
│   ├── Extended Key Usage (server auth, client auth)
│   ├── Subject Alternative Name (SAN)
│   ├── Certificate Policies
│   └── CRL Distribution Points
└── Certificate Signature
```

#### Cadena de Certificación
```
Certificate Chain:
Root CA Certificate (Self-signed)
       │
   (signs)
       ↓
Intermediate CA Certificate
       │
   (signs)
       ↓
End Entity Certificate (Server/Client)

Validación:
├── Verificar firma de cada certificado
├── Validar fechas de vigencia
├── Comprobar revocación (CRL/OCSP)
├── Verificar cadena hasta root CA confiable
└── Validar nombre del servidor (CN/SAN)
```

### Configuración Segura de TLS

#### Cipher Suites Recomendadas
```
TLS 1.3 Cipher Suites (RFC 8446):
├── TLS_AES_256_GCM_SHA384
├── TLS_CHACHA20_POLY1305_SHA256
├── TLS_AES_128_GCM_SHA256
├── TLS_AES_128_CCM_8_SHA256
└── TLS_AES_128_CCM_SHA256

TLS 1.2 Cipher Suites Seguras:
├── ECDHE-ECDSA-AES256-GCM-SHA384
├── ECDHE-RSA-AES256-GCM-SHA384
├── ECDHE-ECDSA-CHACHA20-POLY1305
├── ECDHE-RSA-CHACHA20-POLY1305
├── ECDHE-ECDSA-AES128-GCM-SHA256
└── ECDHE-RSA-AES128-GCM-SHA256
```

#### Configuraciones del Servidor
**Apache HTTP Server:**
```apache
# TLS Configuration
SSLEngine on
SSLProtocol -all +TLSv1.2 +TLSv1.3
SSLCipherSuite ECDHE+AESGCM:ECDHE+CHACHA20:DHE+AESGCM:DHE+CHACHA20:!aNULL:!MD5:!DSS
SSLHonorCipherOrder on
SSLCompression off
SSLSessionTickets off

# Security Headers
Header set Strict-Transport-Security "max-age=63072000; includeSubDomains; preload"
Header set X-Content-Type-Options nosniff
Header set X-Frame-Options DENY
Header set X-XSS-Protection "1; mode=block"
```

**Nginx:**
```nginx
ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers ECDHE+AESGCM:ECDHE+CHACHA20:DHE+AESGCM:DHE+CHACHA20:!aNULL:!MD5:!DSS;
ssl_prefer_server_ciphers off;
ssl_session_cache shared:SSL:10m;
ssl_session_timeout 10m;
ssl_session_tickets off;
ssl_stapling on;
ssl_stapling_verify on;

# Security headers
add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;
add_header X-Content-Type-Options nosniff always;
add_header X-Frame-Options DENY always;
add_header X-XSS-Protection "1; mode=block" always;
```

---

## Fraudes y Malware en las Redes

### Tipos de Fraudes en Línea

#### Phishing y Variantes
```
Taxonomía de Phishing:
├── Email Phishing (tradicional)
│   ├── Mass phishing campaigns
│   ├── Emails genéricos a miles de usuarios
│   └── Baja tasa de éxito pero volumen alto
├── Spear Phishing (dirigido)
│   ├── Ataques personalizados
│   ├── Investigación previa de víctimas
│   └── Tasa de éxito más alta
├── Whaling (ejecutivos)
│   ├── Dirigido a alta dirección
│   ├── Información confidencial corporativa
│   └── Impacto financiero significativo
├── Vishing (voice phishing)
│   ├── Llamadas telefónicas fraudulentas
│   ├── Ingeniería social por voz
│   └── Suplantación de entidades oficiales
├── Smishing (SMS phishing)
│   ├── Mensajes de texto maliciosos
│   ├── Enlaces a sitios fraudulentos
│   └── Aprovecha confianza en SMS
└── Pharming
    ├── Redirección DNS maliciosa
    ├── Modificación de hosts files
    └── Ataques a routers domésticos
```

#### Business Email Compromise (BEC)
**Características de BEC:**
```
Tipos de Ataques BEC:
├── CEO Fraud (Fake President)
│   ├── Suplantación de ejecutivos
│   ├── Solicitudes urgentes de transferencias
│   └── Uso de información corporativa pública
├── Fake Invoice Scheme
│   ├── Facturas fraudulentas de proveedores
│   ├── Cambio de información bancaria
│   └── Timing con facturas legítimas
├── Attorney Impersonation
│   ├── Suplantación de abogados
│   ├── Transacciones confidenciales urgentes
│   └── Creación de presión temporal
└── Data Theft
    ├── Solicitud de información de empleados
    ├── Datos para ataques posteriores
    └── Preparación para otros fraudes
```

### Malware Propagado por Red

#### Gusanos de Red (Network Worms)
**Características de Worms:**
- Auto-replicación sin intervención humana
- Propagación a través de vulnerabilidades de red
- Consumo de recursos de red y sistemas
- Payload opcional (destructivo o de espionaje)

**Casos Históricos Famosos:**
```
Worms Históricos:
├── Morris Worm (1988)
│   ├── Primer worm de Internet masivo
│   ├── Explotó vulnerabilidades UNIX
│   └── 6,000 computadoras afectadas (10% de Internet)
├── Code Red (2001)
│   ├── Explotó IIS buffer overflow
│   ├── 359,000 servidores infectados
│   └── DDoS contra whitehouse.gov
├── SQL Slammer (2003)
│   ├── Explotó MS SQL Server
│   ├── Propagación extremadamente rápida
│   └── Saturación global de Internet
├── Conficker (2008)
│   ├── Múltiples vectores de propagación
│   ├── 9-15 millones de computadoras
│   └── Botnet para actividades criminales
└── WannaCry (2017)
    ├── Ransomware con capacidades de worm
    ├── Explotó EternalBlue (NSA leak)
    └── 300,000+ computadoras en 150 países
```

#### Botnets y su Funcionamiento

**Arquitectura de Botnet:**
```
Estructura de Botnet:
┌─────────────────┐
│   Botmaster     │ (Criminal operator)
│   (Command &    │
│    Control)     │
└────────┬────────┘
         │
    ┌────▼────┐
    │ C&C     │ (Command & Control Server)
    │ Server  │
    └────┬────┘
         │
    ┌────▼────┐
    │ Bots    │ (Infected computers - Zombies)
    │(Zombies)│
    └─────────┘

Protocolos C&C:
├── HTTP/HTTPS (web-based)
├── IRC (Internet Relay Chat)
├── P2P (Peer-to-peer)
├── DNS (Domain Generation Algorithm)
├── Social Media (Twitter, Telegram)
└── Blockchain (descentralizado)
```

**Actividades Criminales de Botnets:**
- **DDoS Attacks**: Denegación de servicio distribuida
- **Spam Distribution**: Envío masivo de emails
- **Credential Theft**: Robo de passwords y datos bancarios
- **Click Fraud**: Fraude publicitario automatizado
- **Cryptocurrency Mining**: Minería no autorizada
- **Data Theft**: Exfiltración de información sensible

### Advanced Persistent Threats (APT)

#### Características de APT
```
Fases de un Ataque APT:
├── 1. Reconnaissance (Reconocimiento)
│   ├── Footprinting de la organización objetivo
│   ├── Social media intelligence (SOCMINT)
│   ├── Technical intelligence gathering
│   └── Identification de vectores de entrada
├── 2. Initial Compromise (Compromiso inicial)
│   ├── Spear-phishing emails
│   ├── Watering hole attacks
│   ├── Supply chain compromise
│   └── Zero-day exploits
├── 3. Establish Foothold (Establecer presencia)
│   ├── Malware installation
│   ├── Persistence mechanisms
│   ├── Anti-forensics measures
│   └── Communication channels
├── 4. Escalate Privileges (Escalamiento)
│   ├── Local privilege escalation
│   ├── Credential dumping
│   ├── Pass-the-hash attacks
│   └── Golden ticket attacks
├── 5. Internal Reconnaissance (Reconocimiento interno)
│   ├── Network mapping
│   ├── Service enumeration
│   ├── Trust relationship mapping
│   └── Data location identification
├── 6. Lateral Movement (Movimiento lateral)
│   ├── Remote access tools (RATs)
│   ├── Windows admin shares
│   ├── RDP and SSH compromise
│   └── Service account abuse
├── 7. Maintain Presence (Mantener presencia)
│   ├── Multiple backdoors
│   ├── Legitimate tool abuse
│   ├── Schedule task persistence
│   └── Registry modification
└── 8. Complete Mission (Completar misión)
    ├── Data exfiltration
    ├── System destruction
    ├── Espionage activities
    └── Financial theft
```

#### Grupos APT Conocidos
**Grupos por Región:**
```
APT Groups (ejemplos):
├── China
│   ├── APT1 (Comment Crew)
│   ├── APT28 (Fancy Bear) - atribuido a GRU
│   ├── APT40 (Leviathan)
│   └── Lazarus Group (Corea del Norte)
├── Rusia
│   ├── APT28 (Fancy Bear)
│   ├── APT29 (Cozy Bear)
│   ├── Turla Group
│   └── Sandworm Team
├── Irán
│   ├── APT33 (Elfin)
│   ├── APT34 (OilRig)
│   └── APT39 (Chafer)
└── Otros
    ├── Equation Group (NSA-linked)
    ├── Carbanak (Criminal)
    └── Dark Halo (SolarWinds)
```

### Técnicas de Prevención y Detección

#### Defensa Contra Fraudes
**Medidas Técnicas:**
- Email authentication (SPF, DKIM, DMARC)
- Advanced email filtering
- URL reputation checking
- Sandboxing de attachments
- DNS filtering y sinkholes

**Medidas Humanas:**
- Security awareness training
- Phishing simulation exercises
- Verification procedures para transferencias
- Incident reporting mechanisms
- Regular security updates

#### Detección de Malware de Red
**Network-based Detection:**
```
Técnicas de Detección:
├── Network Traffic Analysis
│   ├── Behavioral analytics
│   ├── Protocol anomaly detection
│   ├── Communication pattern analysis
│   └── DNS exfiltration detection
├── Signature-based Detection
│   ├── Known malware signatures
│   ├── Network IOCs (Indicators of Compromise)
│   ├── URL/Domain blacklists
│   └── SSL certificate fingerprinting
├── Heuristic Detection
│   ├── Machine learning algorithms
│   ├── Statistical analysis
│   ├── Time-series analysis
│   └── Graph-based analysis
└── Threat Intelligence
    ├── External threat feeds
    ├── Industry sharing groups
    ├── Government alerts
    └── Commercial threat intelligence
```

**Herramientas de Detección:**
- **SIEM Platforms**: Splunk, QRadar, ArcSight
- **Network Analysis**: Wireshark, NetworkMiner, Moloch
- **Threat Hunting**: CrowdStrike Falcon, Carbon Black
- **Open Source**: Suricata, Zeek (Bro), YARA rules

## Objetivos de Aprendizaje
- [ ] Comprender las vulnerabilidades de TCP/IP
- [ ] Implementar protocolos de seguridad en red
- [ ] Configurar VPNs con IPSec
- [ ] Identificar y prevenir fraudes en línea
- [ ] Detectar y mitigar malware de red

## Recursos Adicionales
- RFCs de protocolos de seguridad
- Herramientas de análisis de red (Wireshark)
- Casos de estudio de ataques reales

## Actividades
- Análisis de tráfico con Wireshark
- Configuración de VPN
- Simulación de ataques de red
- Detección de malware en tráfico
