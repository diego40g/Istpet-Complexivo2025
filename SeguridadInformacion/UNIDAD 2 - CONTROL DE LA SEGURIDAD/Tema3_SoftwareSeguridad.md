# Tema 3: Software de Seguridad

## Índice de Contenidos
1. [Tipos de Software de Seguridad](#tipos-de-software-de-seguridad)
2. [Antivirus y Anti-malware](#antivirus-y-anti-malware)
3. [Firewalls](#firewalls)
4. [Sistemas IDS/IPS](#sistemas-idsips)
5. [Gestión de Almacenamiento de Información](#gestión-de-almacenamiento-de-información)

---

## Tipos de Software de Seguridad

### Clasificación General
```
Software de Seguridad
├── Preventivo
│   ├── Antivirus/Anti-malware
│   ├── Firewalls
│   ├── Software de cifrado
│   └── Gestores de contraseñas
├── Detective
│   ├── IDS (Intrusion Detection Systems)
│   ├── SIEM (Security Information and Event Management)
│   ├── Monitores de integridad de archivos
│   └── Analizadores de logs
├── Correctivo
│   ├── IPS (Intrusion Prevention Systems)
│   ├── Software de respuesta automática
│   ├── Herramientas de limpieza de malware
│   └── Sistemas de backup y recuperación
└── Forense
    ├── Herramientas de análisis forense
    ├── Recuperación de datos
    ├── Análisis de memoria
    └── Timeline de eventos
```

### Software de Protección Endpoint

#### Antivirus Tradicionales vs Modernas Soluciones EDR
**Antivirus Tradicionales:**
- Detección basada en firmas
- Análisis heurístico básico
- Protección en tiempo real
- Actualizaciones de definiciones

**EDR (Endpoint Detection and Response):**
- Análisis comportamental avanzado
- Machine Learning e IA
- Respuesta automatizada a amenazas
- Análisis forense integrado
- Threat hunting capabilities

#### Software Anti-malware Especializado
**Herramientas Especializadas:**
- **Anti-ransomware**: CryptoPrevent, RansomFree
- **Anti-rootkit**: Malwarebytes Anti-Rootkit, ESET Online Scanner
- **Anti-spyware**: Spybot Search & Destroy, Ad-Aware
- **Sandboxing**: Cuckoo Sandbox, Sandboxie

### Herramientas de Cifrado

#### Software de Cifrado de Archivos y Discos
**Cifrado de Disco Completo:**
- **BitLocker** (Windows): Integrado en Windows Pro/Enterprise
- **FileVault** (macOS): Cifrado nativo de Apple
- **LUKS** (Linux): Linux Unified Key Setup
- **VeraCrypt**: Sucesor de TrueCrypt, multiplataforma

**Cifrado de Archivos Individual:**
- **AxCrypt**: Cifrado simple de archivos individuales
- **7-Zip**: Compresión con cifrado AES-256
- **GnuPG**: Implementación del estándar OpenPGP
- **Folder Lock**: Protección con contraseña de carpetas

#### Gestores de Contraseñas
```
Características de Gestores de Contraseñas:
├── Generación de contraseñas seguras
├── Almacenamiento cifrado
├── Sincronización entre dispositivos
├── Autofill automático
├── Auditoría de contraseñas débiles
├── Autenticación de dos factores
└── Compartición segura

Soluciones Populares:
├── Comerciales
│   ├── LastPass
│   ├── 1Password
│   ├── Dashlane
│   └── Keeper
└── Open Source
    ├── KeePass
    ├── Bitwarden
    └── Password Safe
```

---

## Antivirus y Anti-malware

### Funcionamiento de los Antivirus

#### Métodos de Detección
**1. Detección por Firmas (Signature-based)**
- Base de datos de firmas conocidas
- Hash MD5/SHA de archivos maliciosos
- Patrones de código específicos
- Actualización constante de definiciones

**2. Detección Heurística**
- Análisis de comportamiento sospechoso
- Identificación de patrones no conocidos
- Técnicas de emulación y sandboxing
- Reducción de falsos positivos

**3. Detección Comportamental**
- Monitoreo de actividades del sistema
- Análisis de llamadas al sistema
- Detección de modificaciones sospechosas
- Machine Learning para patrones anómalos

#### Arquitectura de Antivirus Moderno
```
Componentes del Antivirus:
├── Motor de Escaneo
│   ├── Parser de archivos
│   ├── Descompresores
│   ├── Emulador de código
│   └── Motor heurístico
├── Base de Datos
│   ├── Firmas de malware
│   ├── URLs maliciosas
│   ├── Certificados revocados
│   └── Reglas heurísticas
├── Interfaz de Usuario
│   ├── Dashboard de estado
│   ├── Configuración de políticas
│   ├── Logs y reportes
│   └── Alertas y notificaciones
└── Servicios del Sistema
    ├── Monitor de archivos
    ├── Monitor de red
    ├── Monitor de registro
    └── Actualizador automático
```

### Principales Fabricantes y Soluciones

#### Soluciones Empresariales
**Symantec Endpoint Protection:**
- Protección integrada contra malware
- Prevención de intrusiones (IPS)
- Control de aplicaciones y dispositivos
- Gestión centralizada

**McAfee Total Protection for Business:**
- Protección endpoint completa
- Web security y email security
- Data Loss Prevention (DLP)
- Encryption y compliance

**Kaspersky Endpoint Security:**
- Tecnología anti-malware avanzada
- Protección web y email
- Control de aplicaciones
- Gestión de vulnerabilidades

#### Soluciones para Usuarios Finales
```
Comparativa de Antivirus Populares:

┌─────────────────┬───────────────┬───────────────┬─────────────┐
│ Producto        │ Detección     │ Performance   │ Precio      │
├─────────────────┼───────────────┼───────────────┼─────────────┤
│ Bitdefender     │ Excelente     │ Alto          │ Premium     │
│ Kaspersky       │ Excelente     │ Medio         │ Medio       │
│ Norton          │ Muy Bueno     │ Alto          │ Premium     │
│ ESET            │ Muy Bueno     │ Excelente     │ Medio       │
│ Windows Defender│ Bueno         │ Excelente     │ Gratuito    │
│ Avast           │ Bueno         │ Medio         │ Freemium    │
└─────────────────┴───────────────┴───────────────┴─────────────┘
```

### Configuración y Mejores Prácticas

#### Configuración Óptima
**Configuraciones Recomendadas:**
- Escaneo en tiempo real habilitado
- Actualizaciones automáticas activas
- Escaneos programados regulares
- Quarantine de archivos sospechosos
- Integración con Windows Defender (donde aplique)

#### Falsos Positivos y Excepciones
**Gestión de Falsos Positivos:**
- Lista blanca de aplicaciones conocidas
- Exclusiones por carpeta o extensión
- Reportar falsos positivos al fabricante
- Pruebas en entorno controlado

---

## Firewalls

### Tipos de Firewalls

#### Clasificación por Ubicación
**1. Firewalls de Red (Network Firewalls)**
- Protección perimetral
- Control de tráfico entre redes
- Capacidades de alta velocidad
- Configuración centralizada

**2. Firewalls Personales (Host-based Firewalls)**
- Protección individual de equipos
- Control granular de aplicaciones
- Menor impacto en performance
- Configuración por usuario/equipo

#### Clasificación por Tecnología
```
Evolución de Firewalls:
├── Packet Filtering Firewalls (1ª Generación)
│   ├── Filtrado por IP, puerto y protocolo
│   ├── Reglas estáticas
│   └── No mantiene estado de conexión
├── Stateful Inspection Firewalls (2ª Generación)
│   ├── Seguimiento de estado de conexiones
│   ├── Tablas de estado dinámicas
│   └── Mayor seguridad que packet filtering
├── Application Layer Firewalls (3ª Generación)
│   ├── Inspección de contenido de aplicación
│   ├── Proxy de aplicaciones
│   └── Control granular por aplicación
└── Next-Generation Firewalls (NGFW)
    ├── Deep Packet Inspection (DPI)
    ├── Application awareness
    ├── User identity awareness
    ├── IPS integrado
    └── Threat intelligence
```

### Configuración de Firewalls

#### Reglas Básicas de Firewall
**Estructura de Reglas:**
```
Ejemplo de Regla:
ALLOW TCP FROM 192.168.1.0/24 TO ANY PORT 80,443
DENY TCP FROM ANY TO 192.168.1.100 PORT 22
ALLOW ICMP FROM ANY TO ANY (ping)
DENY ALL FROM ANY TO ANY (regla por defecto)
```

**Principios de Configuración:**
- **Deny by Default**: Denegar todo lo no explícitamente permitido
- **Least Privilege**: Permitir solo el mínimo necesario
- **Logging**: Registrar eventos significativos
- **Regular Review**: Revisión periódica de reglas

#### Configuración por Zonas
**Modelo de Zonas de Seguridad:**
```
Arquitectura de Zonas:
Internet (Untrusted) ←→ DMZ (Semi-trusted) ←→ LAN (Trusted)

Políticas de Zona:
├── Internet → DMZ: Servicios públicos únicamente
├── Internet → LAN: Bloqueado completamente
├── DMZ → Internet: Conexiones iniciadas desde DMZ
├── DMZ → LAN: Servicios específicos únicamente
├── LAN → DMZ: Acceso de gestión
└── LAN → Internet: Navegación web y email
```

### Firewalls de Aplicación Web (WAF)

#### Funcionalidad de WAF
**Protección Específica Web:**
- Filtrado de ataques OWASP Top 10
- Protección contra SQL injection
- Prevención de XSS (Cross-site scripting)
- Rate limiting y DDoS protection
- SSL/TLS termination

**Tipos de WAF:**
- **Network-based WAF**: Hardware dedicado
- **Host-based WAF**: Software en servidor
- **Cloud-based WAF**: Servicio en la nube

#### Principales Soluciones WAF
**Soluciones Comerciales:**
- **F5 BIG-IP ASM**: Solución enterprise completa
- **Imperva SecureSphere**: Protección avanzada de aplicaciones
- **Cloudflare WAF**: Servicio cloud global
- **AWS WAF**: Integrado con servicios AWS

**Soluciones Open Source:**
- **ModSecurity**: Motor WAF más popular
- **NAXSI**: WAF para Nginx
- **Shadow Daemon**: WAF modular

---

## Sistemas IDS/IPS

### Conceptos Fundamentales

#### Diferencias entre IDS e IPS
```
IDS vs IPS:
┌─────────────────┬─────────────────────────┬─────────────────────────┐
│ Característica  │ IDS                     │ IPS                     │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Función         │ Detecta y alerta       │ Detecta y previene      │
│ Posición        │ Out-of-band (copia)    │ In-line (tráfico real)  │
│ Respuesta       │ Pasiva (alertas)       │ Activa (bloqueo)        │
│ Latencia        │ Sin impacto            │ Puede añadir latencia   │
│ Single Point    │ No es crítico          │ Puede ser crítico       │
│ Detección       │ Análisis completo      │ Análisis en tiempo real │
└─────────────────┴─────────────────────────┴─────────────────────────┘
```

#### Métodos de Detección
**1. Signature-based Detection**
- Patrones conocidos de ataques
- Base de datos de firmas actualizada
- Baja tasa de falsos positivos
- No detecta ataques desconocidos (zero-day)

**2. Anomaly-based Detection**
- Establece línea base de comportamiento normal
- Detecta desviaciones estadísticas
- Puede detectar ataques desconocidos
- Mayor tasa de falsos positivos

**3. Hybrid Detection**
- Combinación de signature y anomaly
- Mayor cobertura de detección
- Reducción de falsos positivos
- Complejidad de configuración mayor

### Arquitectura de IDS/IPS

#### Componentes Principales
```
Arquitectura IDS/IPS:
├── Sensores de Red
│   ├── Captura de paquetes
│   ├── Análisis de protocolos
│   ├── Matching de firmas
│   └── Detección de anomalías
├── Motor de Análisis
│   ├── Correlación de eventos
│   ├── Reducción de falsos positivos
│   ├── Generación de alertas
│   └── Respuesta automática
├── Base de Datos
│   ├── Firmas de ataques
│   ├── Configuraciones de políticas
│   ├── Logs de eventos
│   └── Información de contexto
└── Consola de Gestión
    ├── Dashboard de alertas
    ├── Configuración de políticas
    ├── Reportes y análisis
    └── Gestión de incidentes
```

#### Tipos de IDS/IPS por Ubicación
**Network-based IDS/IPS (NIDS/NIPS):**
- Monitoreo de tráfico de red
- Protección de múltiples hosts
- Detección de ataques de red
- Ubicación estratégica en la red

**Host-based IDS/IPS (HIDS/HIPS):**
- Monitoreo de actividad en host específico
- Análisis de logs del sistema
- Detección de cambios en archivos
- Protección granular por sistema

### Herramientas Populares de IDS/IPS

#### Soluciones Open Source
**Snort:**
```
Características de Snort:
├── Motor de detección basado en reglas
├── Captura de paquetes en tiempo real
├── Análisis de protocolos
├── Logging flexible
├── Alertas personalizables
└── Comunidad activa de desarrollo

Arquitectura de Reglas Snort:
action protocol src_ip src_port -> dst_ip dst_port (options)

Ejemplo:
alert tcp any any -> 192.168.1.0/24 80 (msg:"Possible attack"; sid:1000001;)
```

**Suricata:**
- Multi-threading nativo
- IPv6 support completo
- Output JSON para SIEM
- Engine de scripts Lua
- IPS mode inline

**OSSEC:**
- HIDS completo
- Análisis de logs centralizado
- Monitoreo de integridad de archivos
- Detección de rootkits
- Active response capabilities

#### Soluciones Comerciales
**IBM Security QRadar:**
- SIEM con capacidades IPS integradas
- Correlación avanzada de eventos
- Machine learning para anomalías
- Threat intelligence integration

**Cisco Firepower NGIPS:**
- Next-generation IPS
- Application visibility and control
- Advanced malware protection
- Integration con Cisco security ecosystem

---

## Gestión de Almacenamiento de Información

### Clasificación de la Información

#### Niveles de Clasificación
```
Jerarquía de Clasificación:
├── Público
│   ├── Información de dominio público
│   ├── Material de marketing
│   ├── Políticas públicas
│   └── Sin restricciones de acceso
├── Interno
│   ├── Información operacional general
│   ├── Procedimientos internos
│   ├── Comunicaciones internas
│   └── Acceso limitado a empleados
├── Confidencial
│   ├── Información sensible del negocio
│   ├── Datos financieros
│   ├── Estrategias corporativas
│   └── Requiere autorización específica
└── Secreto/Crítico
    ├── Información altamente sensible
    ├── Propiedad intelectual crítica
    ├── Datos de seguridad nacional
    └── Acceso muy restringido
```

#### Marcado y Etiquetado
**Sistemas de Etiquetado:**
- **Etiquetas Visuales**: Headers, footers, marcas de agua
- **Metadata**: Etiquetas electrónicas embebidas
- **Códigos de Colores**: Sistema visual de clasificación
- **Símbolos**: Iconografía estándar de clasificación

### Políticas de Retención

#### Ciclo de Vida de la Información
```
Information Lifecycle Management (ILM):
├── Creación
│   ├── Clasificación inicial
│   ├── Asignación de propietario
│   ├── Aplicación de controles
│   └── Backup inicial
├── Uso Activo
│   ├── Acceso controlado
│   ├── Monitoreo de uso
│   ├── Backups regulares
│   └── Actualizaciones de clasificación
├── Uso Inactivo
│   ├── Archivado
│   ├── Compresión
│   ├── Migración a almacenamiento económico
│   └── Acceso limitado
└── Destrucción
    ├── Fin de período de retención
    ├── Destrucción segura
    ├── Certificación de destrucción
    └── Actualización de inventarios
```

#### Factores para Políticas de Retención
**Consideraciones Legales:**
- Regulaciones gubernamentales
- Requerimientos de auditoría
- Litigación potencial
- Compliance sectorial

**Consideraciones del Negocio:**
- Valor histórico de la información
- Costos de almacenamiento
- Riesgos de seguridad
- Facilidad de recuperación

### Backup y Recuperación

#### Estrategias de Backup
**Tipos de Backup:**
```
Estrategias de Backup:
├── Full Backup (Completo)
│   ├── Copia completa de todos los datos
│   ├── Mayor tiempo y espacio requerido
│   ├── Recuperación más rápida
│   └── Base para backups incrementales
├── Incremental Backup
│   ├── Solo archivos modificados desde último backup
│   ├── Menor tiempo y espacio
│   ├── Recuperación más lenta
│   └── Requiere cadena completa para restaurar
├── Differential Backup
│   ├── Archivos modificados desde último full backup
│   ├── Tiempo medio requerido
│   ├── Recuperación de complejidad media
│   └── Solo requiere full + último differential
└── Mirror Backup (Sincronización)
    ├── Copia exacta en tiempo real
    ├── Recuperación instantánea
    ├── Mayor costo de almacenamiento
    └── No protege contra errores de usuario
```

#### Regla 3-2-1 de Backup
**Principio 3-2-1:**
- **3 copias** de datos importantes
- **2 tipos diferentes** de medios de almacenamiento
- **1 copia offsite** (fuera del sitio)

#### Tecnologías de Backup
**Medios de Almacenamiento:**
- **Disk-to-Disk (D2D)**: Backup a discos duros
- **Disk-to-Tape (D2T)**: Backup a cintas magnéticas  
- **Disk-to-Cloud (D2C)**: Backup a servicios en la nube
- **Tape-to-Tape (T2T)**: Duplicación de cintas

### Almacenamiento Seguro

#### Tecnologías de Cifrado de Almacenamiento
**File-level Encryption:**
- Cifrado de archivos individuales
- Control granular de acceso
- Compatible con sistemas existentes
- Overhead de gestión de claves

**Block-level Encryption:**
- Cifrado transparente de dispositivos
- Sin cambios en aplicaciones
- Protección completa del dispositivo
- Gestión simplificada de claves

**Database Encryption:**
```
Niveles de Cifrado de Base de Datos:
├── Transparent Data Encryption (TDE)
│   ├── Cifrado automático de archivos de datos
│   ├── Sin cambios en aplicaciones
│   └── Protección en reposo
├── Column-level Encryption
│   ├── Cifrado de columnas específicas
│   ├── Control granular
│   └── Impacto en performance
└── Application-level Encryption
    ├── Cifrado en la aplicación
    ├── Control total sobre proceso
    └── Mayor complejidad de implementación
```

#### Gestión de Claves Criptográficas
**Key Management Systems (KMS):**
- Generación segura de claves
- Almacenamiento protegido
- Distribución controlada
- Rotación automática
- Escrow y recovery

### Destrucción Segura de Datos

#### Métodos de Sanitización
**Para Medios Magnéticos:**
- **Overwriting**: Sobrescritura con patrones específicos
- **Degaussing**: Desmagnetización con campos magnéticos intensos
- **Physical Destruction**: Destrucción física del medio

**Para Medios de Estado Sólido (SSD):**
- **Crypto Erase**: Destrucción de claves de cifrado
- **Secure Erase**: Comando ATA Secure Erase
- **Physical Destruction**: Fragmentación física de chips

#### Estándares de Sanitización
**NIST SP 800-88:**
- Clear: Eliminación básica de datos
- Purge: Eliminación resistente a recuperación forense
- Destroy: Destrucción física del medio

**DoD 5220.22-M:**
- Patrón de 3 pasadas para overwriting
- Verificación de sobrescritura
- Documentación del proceso

## Objetivos de Aprendizaje
- [ ] Identificar diferentes tipos de software de seguridad
- [ ] Configurar antivirus y firewalls básicos
- [ ] Implementar sistemas IDS/IPS
- [ ] Diseñar estrategias de almacenamiento seguro
- [ ] Establecer políticas de backup y recuperación

## Recursos Adicionales
- Comparativas de software antivirus
- Guías de configuración de firewalls
- Herramientas open source de seguridad

## Actividades
- Instalación y configuración de antivirus
- Configuración de reglas de firewall
- Simulación de ataques y detección
