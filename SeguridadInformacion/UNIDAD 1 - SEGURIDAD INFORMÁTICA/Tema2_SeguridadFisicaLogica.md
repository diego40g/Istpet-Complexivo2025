# Tema 2: Seguridad Física y Lógica

## Índice de Contenidos
1. [Definiciones de la Seguridad Física y Lógica](#definiciones-de-la-seguridad-física-y-lógica)
2. [Seguridad Física](#seguridad-física)
3. [Seguridad Lógica](#seguridad-lógica)
4. [Seguridad en Internet](#seguridad-en-internet)
5. [Seguridad Inalámbrica](#seguridad-inalámbrica)

---

## Definiciones de la Seguridad Física y Lógica

### Concepto de Seguridad Física
La **seguridad física** se refiere a la protección de los recursos materiales y humanos, instalaciones y equipos de una organización contra amenazas físicas que puedan comprometer el funcionamiento de los sistemas de información.

**Componentes principales:**
- Protección de instalaciones y edificios
- Control de acceso a áreas sensibles
- Protección de equipos y hardware
- Seguridad del personal
- Continuidad del negocio ante desastres

### Concepto de Seguridad Lógica
La **seguridad lógica** comprende las medidas de protección de software, datos, procesos y elementos de control lógico de los sistemas de información contra amenazas que puedan afectar su integridad, confidencialidad y disponibilidad.

**Componentes principales:**
- Control de acceso a sistemas y aplicaciones
- Autenticación y autorización de usuarios
- Cifrado de datos y comunicaciones
- Monitoreo de actividades del sistema
- Gestión de vulnerabilidades de software

### Relación e Integración
```
Seguridad Integral
├── Seguridad Física (40%)
│   ├── Perímetro exterior
│   ├── Edificio y instalaciones
│   ├── Sala de servidores
│   └── Estaciones de trabajo
└── Seguridad Lógica (60%)
    ├── Sistemas operativos
    ├── Aplicaciones
    ├── Datos y bases de datos
    └── Comunicaciones de red
```

### Principios Fundamentales
- **Defensa en Profundidad**: Múltiples capas de protección
- **Principio de Menor Privilegio**: Acceso mínimo necesario
- **Separación de Funciones**: División de responsabilidades críticas
- **Monitoreo Continuo**: Supervisión constante de actividades

---

## Seguridad Física

### Protección Perimetral

#### Perímetro Exterior
**Elementos de Control:**
- **Cercas y Vallas**: Barreras físicas de diferentes alturas
- **Iluminación**: Sistemas de iluminación perimetral y de emergencia
- **Cámaras CCTV**: Videovigilancia con grabación y monitoreo
- **Sensores de Movimiento**: Detección de intrusos en zonas críticas
- **Guardias de Seguridad**: Personal especializado en seguridad física

**Zonas de Seguridad:**
```
Modelo de Anillos Concéntricos:
Anillo 1: Perímetro público (nivel básico)
Anillo 2: Perímetro del edificio (nivel medio)
Anillo 3: Áreas restringidas (nivel alto)
Anillo 4: Sala de servidores (nivel crítico)
```

#### Control de Acceso Físico
**Tecnologías de Acceso:**
- **Tarjetas de Proximidad**: RFID, NFC
- **Sistemas Biométricos**: Huella dactilar, reconocimiento facial, iris
- **Códigos de Acceso**: PIN numéricos
- **Llaves Físicas**: Para áreas específicas
- **Sistemas Multi-factor**: Combinación de métodos

### Protección de Centros de Datos

#### Diseño de Salas de Servidores
**Especificaciones Técnicas:**
- **Ubicación**: Plantas intermedias, alejadas de riesgos
- **Construcción**: Materiales resistentes al fuego y agua
- **Acceso Limitado**: Una sola entrada controlada
- **Ventanas**: Evitar ventanas o usar vidrio resistente

#### Sistemas de Soporte Crítico
**Alimentación Eléctrica:**
```
Sistemas de Energía:
├── Alimentación Principal (Red eléctrica)
├── UPS (Sistemas de alimentación ininterrumpida)
│   ├── UPS Online (doble conversión)
│   ├── UPS Line-interactive
│   └── UPS Offline (standby)
└── Generadores de Emergencia
    ├── Generadores diésel
    ├── Generadores de gas
    └── Sistemas de combustible
```

**Control Ambiental:**
- **Temperatura**: Mantenimiento entre 18-24°C
- **Humedad**: Control entre 40-60% HR
- **Filtración de Aire**: Sistemas HEPA
- **Presión Diferencial**: Para evitar contaminantes

### Sistemas de Detección y Extinción

#### Detección de Incendios
**Tipos de Detectores:**
- **Detectores de Humo**: Iónicos y fotoeléctricos
- **Detectores de Calor**: Temperatura fija y gradiente
- **Detectores de Llama**: Infrarrojos y ultravioleta
- **Sistemas de Aspiración**: VESDA (Very Early Smoke Detection)

#### Sistemas de Extinción
**Agentes de Extinción:**
- **Agua**: Sprinklers (evitar en salas de servidores)
- **Gases Inertes**: Argón, nitrógeno, CO₂
- **Agentes Limpios**: FM-200, Novec 1230
- **Polvo Químico**: Para incendios específicos

### Protección contra Desastres Naturales

#### Evaluación de Riesgos Geográficos
**Factores Naturales:**
- Actividad sísmica y terremotos
- Inundaciones y desbordamientos
- Huracanes y vientos fuertes
- Incendios forestales
- Rayos y tormentas eléctricas

#### Medidas de Mitigación
**Construcción Resistente:**
- Cimientos sísmicos reforzados
- Estructuras elevadas (inundaciones)
- Materiales resistentes al fuego
- Sistemas de drenaje adecuados

---

## Seguridad Lógica

### Control de Acceso a Sistemas

#### Modelos de Control de Acceso
**1. Control de Acceso Discrecional (DAC)**
- El propietario del recurso controla el acceso
- Flexibilidad en asignación de permisos
- Vulnerabilidad a ataques de escalamiento

**2. Control de Acceso Obligatorio (MAC)**
- Control centralizado por políticas del sistema
- Etiquetas de seguridad y niveles de clearance
- Mayor seguridad pero menor flexibilidad

**3. Control de Acceso Basado en Roles (RBAC)**
```
Estructura RBAC:
Usuarios → Roles → Permisos → Objetos

Ejemplo:
├── Administrador
│   ├── Gestión de usuarios
│   ├── Configuración de sistemas
│   └── Acceso completo a datos
├── Desarrollador
│   ├── Acceso a código fuente
│   ├── Entornos de desarrollo
│   └── Lectura de logs
└── Usuario Final
    ├── Aplicaciones autorizadas
    ├── Datos personales
    └── Recursos compartidos
```

#### Sistemas de Autenticación

**Factores de Autenticación:**
1. **Algo que sabes** (Knowledge factors)
   - Contraseñas
   - PINs
   - Preguntas de seguridad

2. **Algo que tienes** (Possession factors)
   - Tokens de hardware
   - Tarjetas inteligentes
   - Dispositivos móviles

3. **Algo que eres** (Inherence factors)
   - Huella dactilar
   - Reconocimiento facial
   - Escaneo de iris
   - Reconocimiento de voz

### Cifrado y Protección de Datos

#### Cifrado de Datos en Reposo
**Tecnologías de Cifrado:**
- **Cifrado a Nivel de Archivo**: EFS, FileVault
- **Cifrado de Disco Completo**: BitLocker, LUKS
- **Cifrado de Base de Datos**: TDE, Cell-level encryption
- **Cifrado de Backup**: Para copias de seguridad

#### Cifrado de Datos en Tránsito
**Protocolos Seguros:**
```
Protocolos de Red Seguros:
├── Capa de Transporte
│   ├── TLS/SSL (HTTPS)
│   ├── SSH (Secure Shell)
│   └── SFTP/SCP
├── Capa de Red
│   ├── IPSec
│   └── VPN protocols
└── Capa de Aplicación
    ├── PGP/GPG (Email)
    ├── Signal Protocol (Mensajería)
    └── WebRTC (Comunicaciones en tiempo real)
```

### Gestión de Vulnerabilidades

#### Ciclo de Vida de Vulnerabilidades
1. **Descubrimiento**: Identificación de la vulnerabilidad
2. **Análisis**: Evaluación de impacto y riesgo
3. **Priorización**: Clasificación por criticidad
4. **Mitigación**: Aplicación de parches o controles
5. **Verificación**: Confirmación de la corrección
6. **Documentación**: Registro y lecciones aprendidas

#### Herramientas de Evaluación
**Escáneres de Vulnerabilidades:**
- **OpenVAS**: Solución open source completa
- **Nessus**: Scanner comercial ampliamente usado
- **Qualys VMDR**: Plataforma basada en la nube
- **Rapid7 Nexpose**: Gestión integral de vulnerabilidades

---

## Seguridad en Internet

### Amenazas en Línea

#### Amenazas Web Comunes
**1. Ataques de Inyección**
- SQL Injection
- Command Injection  
- LDAP Injection
- XPath Injection

**2. Cross-Site Scripting (XSS)**
```
Tipos de XSS:
├── Reflected XSS (No persistente)
├── Stored XSS (Persistente)
└── DOM-based XSS (Basado en DOM)
```

**3. Cross-Site Request Forgery (CSRF)**
- Ejecución no autorizada de acciones
- Explotación de sesiones autenticadas
- Prevención mediante tokens CSRF

#### Malware Web
**Drive-by Downloads:**
- Descarga automática de malware
- Explotación de vulnerabilidades del navegador
- Kits de explotación (Exploit Kits)

**Ataques de Phishing:**
- Suplantación de sitios legítimos
- Robo de credenciales
- Ingeniería social avanzada

### Navegación Segura

#### Configuración del Navegador
**Medidas de Seguridad:**
- Actualizaciones automáticas habilitadas
- JavaScript restringido en sitios no confiables
- Plugins y extensiones revisadas
- Configuración de privacidad apropiada
- Certificados SSL/TLS verificados

#### Uso de Proxies y VPN
**Proxies Web:**
- Filtrado de contenido malicioso
- Cache de contenido frecuente
- Logs de navegación y auditoría

**Virtual Private Networks (VPN):**
```
Beneficios de VPN:
├── Cifrado de tráfico de red
├── Anonimización de IP
├── Bypass de restricciones geográficas
└── Protección en redes públicas
```

### Comercio Electrónico Seguro

#### Estándares de Seguridad
**PCI DSS (Payment Card Industry Data Security Standard):**
- 12 requisitos principales de seguridad
- Protección de datos de tarjetas de crédito
- Auditorías regulares obligatorias
- Certificación anual requerida

#### Tecnologías de Pago Seguro
**Métodos de Pago:**
- Tokenización de tarjetas de crédito
- 3D Secure (Verified by Visa, Mastercard SecureCode)
- Wallets digitales (PayPal, Apple Pay, Google Pay)
- Criptomonedas con escrow

---

## Seguridad Inalámbrica

### Protocolos de Seguridad WiFi

#### Evolución de Estándares
**1. WEP (Wired Equivalent Privacy)**
- Lanzado en 1997
- Cifrado RC4 de 40/104 bits
- Vulnerabilidades críticas identificadas
- **Estado actual**: Obsoleto y vulnerable

**2. WPA (Wi-Fi Protected Access)**
- Reemplazo temporal de WEP (2003)
- TKIP (Temporal Key Integrity Protocol)
- Autenticación mejorada
- **Estado actual**: Vulnerable a ataques modernos

**3. WPA2 (Wi-Fi Protected Access II)**
```
Características WPA2:
├── Cifrado AES (Advanced Encryption Standard)
├── CCMP (Counter Mode with CBC-MAC Protocol)
├── Modos de operación:
│   ├── WPA2-Personal (PSK)
│   └── WPA2-Enterprise (802.1X)
└── Requisitos de hardware específicos
```

**4. WPA3 (Wi-Fi Protected Access III)**
- Lanzado en 2018
- SAE (Simultaneous Authentication of Equals)
- Protección contra ataques de diccionario offline
- Enhanced Open para redes públicas
- Cifrado individualizado en redes abiertas

### Configuración Segura de Redes Inalámbricas

#### Configuración Básica de Seguridad
**Parámetros Esenciales:**
1. **Cambio de Credenciales Predeterminadas**
   - Usuario/contraseña de administración
   - SSID personalizado (no revelar marca/modelo)

2. **Configuración de Cifrado**
   - Usar WPA3 (o WPA2 como mínimo)
   - Contraseñas complejas de al menos 15 caracteres
   - Rotación periódica de contraseñas

3. **Configuración de Red**
   - Desactivar WPS (Wi-Fi Protected Setup)
   - Filtrado MAC (limitaciones conocidas)
   - Ocultar SSID (seguridad por oscuridad)
   - Configurar red de invitados separada

#### Configuración Empresarial Avanzada
**WPA2/WPA3-Enterprise:**
```
Arquitectura 802.1X:
Cliente WiFi ←→ Punto de Acceso ←→ Servidor RADIUS
    (Suplicante)    (Autenticador)    (Servidor de Autenticación)

Protocolos EAP soportados:
├── EAP-TLS (certificados digitales)
├── PEAP-MSCHAPv2 (usuario/contraseña)
├── EAP-TTLS (túnel seguro)
└── EAP-FAST (Cisco propietario)
```

### Amenazas Específicas de Redes WiFi

#### Ataques Comunes
**1. Ataques de Deautenticación**
- Desconexión forzada de clientes
- Facilitación de ataques WPS/WPA
- Herramientas: Aircrack-ng, MDK3

**2. Evil Twin Attacks**
- Puntos de acceso falsos
- Suplantación de redes legítimas
- Captura de credenciales

**3. Man-in-the-Middle WiFi**
- Intercepción de comunicaciones
- Modificación de tráfico
- Inyección de código malicioso

#### Herramientas de Auditoría WiFi
**Suite Aircrack-ng:**
- **Airmon-ng**: Configuración de modo monitor
- **Airodump-ng**: Captura de paquetes
- **Aireplay-ng**: Inyección de paquetes
- **Aircrack-ng**: Crackeado de claves WEP/WPA

**Otras Herramientas:**
- **Kismet**: Detector de redes inalámbricas
- **Wireshark**: Análisis de protocolos
- **Reaver**: Ataque a WPS
- **WiFite**: Automatización de auditorías

### Mejores Prácticas para Redes Inalámbricas

#### Para Organizaciones
**1. Diseño de Red Segmentada**
```
Segmentación de Red WiFi:
├── Red Corporativa (empleados)
│   ├── VLAN separada
│   ├── Políticas de acceso estrictas
│   └── Monitoreo continuo
├── Red de Invitados
│   ├── Aislamiento de red corporativa
│   ├── Ancho de banda limitado
│   └── Portal cautivo
└── Red IoT/Dispositivos
    ├── VLAN dedicada
    ├── Comunicación restringida
    └── Monitoreo especializado
```

**2. Monitoreo y Detección**
- Sistemas WIDS/WIPS (Wireless Intrusion Detection/Prevention)
- Análisis de espectro radioeléctrico
- Detección de puntos de acceso no autorizados
- Alertas de actividad sospechosa

#### Para Usuarios Finales
**Conexiones Seguras:**
- Verificación de certificados SSL/TLS
- Uso de VPN en redes públicas
- Desactivación de conexión automática
- Verificación de nombres de red (SSID)

**Configuración de Dispositivos:**
- Actualizaciones de firmware regulares
- Desactivación de servicios innecesarios
- Configuración de firewall personal
- Uso de aplicaciones de seguridad móvil

## Objetivos de Aprendizaje
- [ ] Distinguir entre seguridad física y lógica
- [ ] Implementar medidas de seguridad física básicas
- [ ] Configurar sistemas de seguridad lógica
- [ ] Aplicar principios de seguridad en Internet
- [ ] Asegurar redes inalámbricas

## Recursos Adicionales
- Guías de configuración de seguridad
- Herramientas de auditoría WiFi
- Estándares de seguridad física

## Actividades
- Auditoría de seguridad física
- Configuración de redes WiFi seguras
- Análisis de vulnerabilidades web
