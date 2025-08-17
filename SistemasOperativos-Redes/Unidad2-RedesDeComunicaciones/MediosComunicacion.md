# Medios de Comunicación

## 1. Definiciones de los medios de Comunicación

### ¿Qué son los medios de comunicación en redes?
Los medios de comunicación son los canales físicos o inalámbricos a través de los cuales se transmiten las señales de datos entre dispositivos de red.

### Clasificación general:

#### Medios guiados (Cableados):
- **Cable de par trenzado** (UTP/STP)
- **Cable coaxial**
- **Fibra óptica**

#### Medios no guiados (Inalámbricos):
- **Ondas de radio**
- **Microondas**
- **Infrarrojos**
- **Bluetooth**
- **Wi-Fi**

### Factores de selección de medios:
1. **Distancia**: Alcance de la transmisión
2. **Ancho de banda**: Capacidad de datos
3. **Costo**: Instalación y mantenimiento
4. **Facilidad de instalación**: Complejidad del despliegue
5. **Susceptibilidad a interferencias**: EMI/RFI
6. **Seguridad**: Resistencia a interceptación

### Equipos de transmisión

#### Transmisores:
Dispositivos que convierten datos digitales en señales apropiadas para el medio de transmisión.

**Ejemplos:**
- **Tarjetas de red (NIC)**: Ethernet, Wi-Fi
- **Módems**: DSL, cable, dial-up
- **Transceivers**: Fibra óptica, Ethernet
- **Access Points**: Wi-Fi, Bluetooth

#### Receptores:
Dispositivos que reconvierten las señales transmitidas de vuelta a datos digitales.

**Características importantes:**
- **Sensibilidad**: Capacidad de detectar señales débiles
- **Selectividad**: Capacidad de filtrar señales no deseadas
- **Linealidad**: Mantener la forma de la señal
- **Ancho de banda**: Rango de frecuencias procesadas

#### Repetidores y amplificadores:
- **Repetidores**: Regeneran señales digitales
- **Amplificadores**: Incrementan la potencia de señales analógicas
- **Hubs**: Repetidores multipuerto (obsoletos)
- **Switches**: Repetidores inteligentes con memoria

#### Conversores de medios:
- **Ethernet a Fibra**: Convertir entre UTP y fibra óptica
- **Serial a Ethernet**: Integrar dispositivos serie legacy
- **Wireless bridges**: Conectar redes cableadas inalámbricamente

## 2. Modos de transmisión

### Asíncrono

#### Definición:
Transmisión donde los datos se envían sin una señal de reloj compartida entre transmisor y receptor.

#### Características:
- **Start bit**: Indica inicio de caracter (usualmente '0')
- **Stop bit(s)**: Indica final de caracter (usualmente '1')
- **No sincronización de reloj**: Cada dispositivo mantiene su propio reloj
- **Detección de errores**: Bit de paridad opcional

#### Formato típico:
```
Start|D0|D1|D2|D3|D4|D5|D6|D7|Parity|Stop
  0  |  datos (8 bits)    |  ?   | 1
```

#### Ventajas:
- Simple de implementar
- Costo reducido
- Flexible en velocidades
- Buenos para transmisiones esporádicas

#### Desventajas:
- Overhead de start/stop bits (20-25%)
- Velocidades limitadas
- Mayor probabilidad de errores en distancias largas

#### Aplicaciones:
- **RS-232**: Comunicación serie estándar
- **Modems antiguos**: Dial-up
- **Terminales**: Acceso remoto básico

### Síncrono

#### Definición:
Transmisión donde transmisor y receptor comparten una señal de reloj común.

#### Características:
- **Clock signal**: Señal de sincronización separada o embebida
- **Frames**: Datos organizados en bloques estructurados
- **Mayor eficiencia**: Sin overhead de start/stop bits
- **Velocidades altas**: Mejor para grandes volúmenes

#### Métodos de sincronización:
1. **Reloj separado**: Línea dedicada para señal de clock
2. **Reloj embebido**: Clock recuperado de los datos (Manchester encoding)
3. **Reloj maestro**: Un dispositivo proporciona timing

#### Ventajas:
- Mayor eficiencia (menos overhead)
- Velocidades más altas
- Mejor para transmisiones continuas
- Detección de errores más sofisticada

#### Desventajas:
- Mayor complejidad
- Costo más alto
- Requiere sincronización precisa

#### Aplicaciones:
- **SONET/SDH**: Redes de transporte ópticas
- **Frame Relay**: WAN tradicional
- **Ethernet**: LANs modernas
- **USB**: Comunicación de alta velocidad

### Serial

#### Definición:
Transmisión donde los bits se envían uno tras otro por un solo canal.

#### Características:
- **Un bit a la vez**: Secuencial
- **Un canal de comunicación**: Una línea de datos
- **Adecuado para largas distancias**: Menor interferencia
- **Menor costo de cableado**: Menos conductores

#### Ventajas:
- **Costo reducido**: Menos cables
- **Largas distancias**: Menor degradación
- **Menos EMI**: Menor interferencia electromagnética
- **Sincronización más fácil**: Un solo canal de datos

#### Desventajas:
- **Velocidad limitada**: Un bit por vez
- **Complejidad de conversión**: Requiere serialización/deserialización

#### Aplicaciones comunes:
- **RS-232/RS-485**: Comunicación industrial
- **USB**: Universal Serial Bus
- **SATA**: Conexión de discos duros
- **PCIe**: Expansión de alta velocidad

### Paralelo

#### Definición:
Transmisión donde múltiples bits se envían simultáneamente por canales separados.

#### Características:
- **Múltiples bits simultáneamente**: 8, 16, 32 bits en paralelo
- **Múltiples líneas**: Un conductor por bit
- **Alta velocidad teórica**: Multiplicador por número de líneas
- **Distancias cortas**: Limitado por skew

#### Problemas principales:
1. **Clock skew**: Diferencias en tiempo de llegada
2. **Crosstalk**: Interferencia entre líneas adyacentes
3. **Costo**: Múltiples conductores
4. **Complejidad**: Sincronización de múltiples señales

#### Aplicaciones (mayormente legacy):
- **Puertos paralelos**: Impresoras antiguas (LPT)
- **IDE/PATA**: Discos duros antiguos
- **Memoria RAM**: Buses internos de computadora

### Dúplex

#### Definición:
Modo de transmisión bidireccional donde la comunicación puede fluir en una dirección a la vez.

#### Características:
- **Bidireccional**: Ambos dispositivos pueden transmitir
- **Alternado**: No simultáneo
- **Control de turno**: Protocolos para determinar quién transmite
- **Un canal físico**: Puede usar el mismo medio

#### Ejemplo de funcionamiento:
```
A ----datos----> B    (A transmite)
A               B    (pausa/cambio)
A <---datos---- B    (B transmite)
```

#### Ventajas:
- **Uso eficiente del medio**: Un solo canal para ambas direcciones
- **Costo reducido**: Menos infraestructura física
- **Control más simple**: Menos conflictos

#### Desventajas:
- **Throughput limitado**: No puede transmitir y recibir simultáneamente
- **Latencia**: Tiempo de cambio de dirección
- **Protocolos más complejos**: Control de turno

#### Aplicaciones:
- **Walkie-talkies**: Comunicación de radio
- **Modems antiguos**: Dial-up
- **Algunas implementaciones Wi-Fi**: Control de acceso al medio

### Full dúplex

#### Definición:
Modo de transmisión bidireccional donde la comunicación puede fluir en ambas direcciones simultáneamente.

#### Características:
- **Bidireccional simultáneo**: Transmisión y recepción al mismo tiempo
- **Dos canales**: Separación física o lógica
- **Mayor throughput**: Aprovecha toda la capacidad
- **Más complejo**: Requiere aislamiento entre canales

#### Métodos de implementación:
1. **Separación física**: Cables separados para TX y RX
2. **Separación por frecuencia**: Diferentes frecuencias para cada dirección
3. **Separación por tiempo**: Time division duplex (TDD)
4. **Separación por código**: Code division duplex

#### Ejemplo Ethernet full-duplex:
```
Par 1,2: A ----TX----> B
Par 3,6: A <----RX---- B
```

#### Ventajas:
- **Máximo throughput**: Uso completo del ancho de banda
- **Baja latencia**: No hay tiempo de cambio
- **Eficiencia alta**: Transmisión continua en ambas direcciones

#### Desventajas:
- **Mayor costo**: Más infraestructura física
- **Complejidad aumentada**: Aislamiento y control más sofisticado
- **Susceptibilidad a interferencias**: Echo y crosstalk

#### Aplicaciones:
- **Ethernet moderno**: Switches full-duplex
- **Teléfonos**: Conversación natural
- **Conexiones de fibra óptica**: Fibras separadas por dirección

## 3. Conectividad de redes

### Tipos de conectores

#### RJ-45 (Ethernet):
- **8 posiciones**: 8P8C (8 Position 8 Contact)
- **Aplicaciones**: Ethernet 10/100/1000 Mbps
- **Cableado**: T568A o T568B
- **Distancia máxima**: 100 metros

#### RJ-11 (Teléfono):
- **6 posiciones**: Típicamente 4 o 6 contactos
- **Aplicaciones**: Líneas telefónicas, modems DSL
- **Menor ancho de banda**: Voz y datos básicos

#### Conectores de fibra óptica:
- **SC (Subscriber Connector)**: Push-pull, común en equipos
- **LC (Lucent Connector)**: Pequeño, alta densidad
- **ST (Straight Tip)**: Bayoneta, redes antiguas
- **FC (Ferrule Connector)**: Roscado, aplicaciones críticas

#### Conectores coaxiales:
- **BNC**: Bayoneta, redes 10Base-2
- **F-type**: Cable TV, DOCSIS
- **N-type**: Aplicaciones de alta potencia
- **SMA**: Equipos de radio, antenas

### Estándares de cableado

#### T568A vs T568B:
```
T568A:                    T568B:
1. Blanco-Verde          1. Blanco-Naranja
2. Verde                 2. Naranja
3. Blanco-Naranja        3. Blanco-Verde
4. Azul                  4. Azul
5. Blanco-Azul           5. Blanco-Azul
6. Naranja               6. Verde
7. Blanco-Café           7. Blanco-Café
8. Café                  8. Café
```

#### Tipos de cables:
- **Cable directo**: Ambos extremos igual estándar
- **Cable cruzado**: Un extremo T568A, otro T568B
- **Auto-MDIX**: Switches modernos detectan automáticamente

### Dispositivos de conectividad

#### Hubs (Obsoletos):
- **Capa física**: Repetidores multipuerto
- **Half-duplex**: Un dominio de colisión
- **Colisiones**: CSMA/CD requerido
- **Bandwidth compartido**: Entre todos los puertos

#### Switches:
- **Capa de enlace**: Aprendizaje de direcciones MAC
- **Full-duplex**: Cada puerto es un dominio de colisión separado
- **Tabla MAC**: Asocia direcciones con puertos
- **Bandwidth dedicado**: Por puerto

#### Routers:
- **Capa de red**: Enrutamiento entre diferentes redes
- **Protocolos de enrutamiento**: RIP, OSPF, EIGRP, BGP
- **NAT**: Network Address Translation
- **Firewall**: Filtrado de paquetes

## 4. Redes Ethernet

### Historia y evolución:
- **1973**: Desarrollo por Bob Metcalfe (Xerox)
- **1980**: Estándar DIX Ethernet
- **1983**: IEEE 802.3
- **1995**: Fast Ethernet (100 Mbps)
- **1998**: Gigabit Ethernet
- **2002**: 10 Gigabit Ethernet

### Características principales:

#### CSMA/CD (Carrier Sense Multiple Access/Collision Detection):
1. **Carrier Sense**: Escuchar el medio antes de transmitir
2. **Multiple Access**: Múltiples estaciones pueden acceder
3. **Collision Detection**: Detectar colisiones durante transmisión
4. **Backoff Algorithm**: Retardo aleatorio después de colisión

#### Formato de trama Ethernet II:
```
|Preámbulo|SFD|MAC Dest|MAC Orig|EtherType|Datos    |FCS|
|7 bytes  |1  |6 bytes |6 bytes |2 bytes  |46-1500  |4  |
```

- **Preámbulo**: Sincronización (10101010 x 7)
- **SFD**: Start of Frame Delimiter (10101011)
- **Direcciones MAC**: 48 bits cada una
- **EtherType**: Protocolo de capa superior
- **Datos**: Payload (46-1500 bytes)
- **FCS**: Frame Check Sequence (CRC-32)

### Estándares Ethernet:

#### 10 Mbps Ethernet:
- **10Base-5**: Coaxial grueso, 500m, bus
- **10Base-2**: Coaxial delgado, 185m, bus
- **10Base-T**: Par trenzado, 100m, estrella

#### Fast Ethernet (100 Mbps):
- **100Base-TX**: 2 pares UTP Cat 5, 100m
- **100Base-FX**: Fibra óptica multimodo, 2km
- **100Base-T4**: 4 pares UTP Cat 3, 100m

#### Gigabit Ethernet (1000 Mbps):
- **1000Base-T**: 4 pares UTP Cat 5e, 100m
- **1000Base-SX**: Fibra multimodo, 550m
- **1000Base-LX**: Fibra monomodo, 5km

#### 10 Gigabit Ethernet:
- **10GBase-T**: UTP Cat 6a, 100m
- **10GBase-SR**: Fibra multimodo, 300m
- **10GBase-LR**: Fibra monomodo, 10km

## 5. Direccionamiento IPv4

### Estructura de direcciones IPv4:

#### Formato:
- **32 bits** total
- **4 octetos** de 8 bits cada uno
- **Notación decimal punteada**: 192.168.1.1

#### Ejemplo de conversión:
```
192.168.1.1 en binario:
11000000.10101000.00000001.00000001
```

### Clases de direcciones IPv4:

#### Clase A:
- **Rango**: 1.0.0.0 - 126.255.255.255
- **Primer bit**: 0
- **Máscara por defecto**: /8 (255.0.0.0)
- **Redes**: 126 redes
- **Hosts por red**: 16,777,214

#### Clase B:
- **Rango**: 128.0.0.0 - 191.255.255.255
- **Primeros bits**: 10
- **Máscara por defecto**: /16 (255.255.0.0)
- **Redes**: 16,384 redes
- **Hosts por red**: 65,534

#### Clase C:
- **Rango**: 192.0.0.0 - 223.255.255.255
- **Primeros bits**: 110
- **Máscara por defecto**: /24 (255.255.255.0)
- **Redes**: 2,097,152 redes
- **Hosts por red**: 254

#### Direcciones especiales:
- **Clase D**: 224.0.0.0 - 239.255.255.255 (Multicast)
- **Clase E**: 240.0.0.0 - 255.255.255.255 (Experimental)
- **Loopback**: 127.0.0.0/8
- **Direcciones privadas**: 
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

### Máscaras de subred:

#### CIDR (Classless Inter-Domain Routing):
Notación que especifica la cantidad de bits de red.

#### Ejemplos:
```
/24 = 255.255.255.0    (Clase C tradicional)
/16 = 255.255.0.0      (Clase B tradicional)
/8  = 255.0.0.0        (Clase A tradicional)
/30 = 255.255.255.252  (Solo 2 hosts válidos)
```

#### Cálculo de hosts:
```
Hosts disponibles = 2^(32-prefijo) - 2
/24 = 2^(32-24) - 2 = 2^8 - 2 = 254 hosts
/30 = 2^(32-30) - 2 = 2^2 - 2 = 2 hosts
```

## 6. Mecanismos de la división de subredes

### VLSM (Variable Length Subnet Mask):

#### Concepto:
Técnica que permite usar diferentes máscaras de subred dentro de la misma red classfull.

#### Proceso de subnetting:

1. **Determinar requerimientos**: Número de subredes y hosts
2. **Calcular bits necesarios**: Para subredes y hosts
3. **Crear nueva máscara**: Extender la máscara original
4. **Asignar rangos**: Distribuir direcciones IP

#### Ejemplo práctico:
Red original: 192.168.1.0/24

**Requerimientos:**
- Subred A: 60 hosts
- Subred B: 30 hosts  
- Subred C: 12 hosts
- Enlaces punto a punto: 2 hosts cada uno

**Solución:**
```
Subred A: 192.168.1.0/26   (64 hosts - 2 = 62 hosts)
Subred B: 192.168.1.64/27  (32 hosts - 2 = 30 hosts)
Subred C: 192.168.1.96/28  (16 hosts - 2 = 14 hosts)
P2P 1:    192.168.1.112/30 (4 hosts - 2 = 2 hosts)
P2P 2:    192.168.1.116/30 (4 hosts - 2 = 2 hosts)
```

### Supernetting/CIDR:

#### Concepto:
Técnica para combinar múltiples redes en una ruta agregada.

#### Ejemplo:
```
Redes originales:
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24

Supernet: 192.168.0.0/22
```

## 7. Conmutación de Capa 2 Ethernet – Switching

### Funcionamiento del Switch:

#### Proceso de aprendizaje:
1. **Recibe trama**: En un puerto específico
2. **Examina MAC origen**: Dirección del remitente
3. **Actualiza tabla MAC**: Asocia MAC con puerto
4. **Determina destino**: Busca MAC destino en tabla
5. **Reenvía o inunda**: Según conocimiento de destino

#### Estados de la tabla MAC:
- **Unknown**: Dirección no conocida (flooding)
- **Learned**: Dirección aprendida dinámicamente
- **Static**: Dirección configurada manualmente

#### Tipos de transmisión:
- **Unicast**: Una dirección MAC específica
- **Broadcast**: FF:FF:FF:FF:FF:FF
- **Multicast**: Primer bit del primer octeto = 1

### Comandos de configuración básica:

#### Cisco IOS básico:
```bash
# Acceso al modo privilegiado
enable
configure terminal

# Configuración de hostname
hostname SW1

# Configurar contraseña de consola
line console 0
password cisco
login

# Configurar contraseña de enable
enable secret class

# Configuración de VLAN de administración
interface vlan 1
ip address 192.168.1.10 255.255.255.0
no shutdown

# Configuración de puerto
interface fastethernet 0/1
description "Conexion a PC1"
duplex full
speed 100

# Guardar configuración
copy running-config startup-config
```

#### Comandos de verificación:
```bash
# Ver tabla MAC
show mac address-table

# Ver configuración de interfaces
show interfaces status
show interfaces fastethernet 0/1

# Ver información de spanning tree
show spanning-tree

# Ver estadísticas del switch
show version
show flash
```

### Características avanzadas:

#### VLANs (Virtual LANs):
- **Segmentación lógica**: Separar tráfico sin hardware adicional
- **Broadcast domains**: Cada VLAN es un dominio de broadcast separado
- **Trunk ports**: Transportan múltiples VLANs
- **Access ports**: Pertenecen a una sola VLAN

#### Spanning Tree Protocol (STP):
- **Prevención de loops**: Evita tormentas de broadcast
- **Convergencia**: Cálculo de árbol sin loops
- **Estados de puerto**: Blocking, Listening, Learning, Forwarding
- **BPDU**: Bridge Protocol Data Units

## 8. Funcionamiento del Router

### Funciones principales:

#### Enrutamiento:
- **Tabla de enrutamiento**: Base de datos de rutas conocidas
- **Protocolos de enrutamiento**: Intercambio de información
- **Métricas**: Criterios para selección de mejor ruta
- **Next hop**: Siguiente salto hacia el destino

#### Proceso de enrutamiento:
1. **Recibe paquete**: En interfaz de entrada
2. **Examina dirección destino**: IP de destino
3. **Consulta tabla de enrutamiento**: Busca ruta más específica
4. **Determina interfaz de salida**: Y next hop
5. **Reencapsula**: Nueva trama para siguiente segmento
6. **Envía paquete**: Por interfaz de salida

### Tabla de enrutamiento:

#### Componentes:
- **Red destino**: Dirección de red y máscara
- **Next hop**: Router siguiente en el camino
- **Interfaz de salida**: Puerto por donde enviar
- **Métrica**: Costo de la ruta
- **Fuente**: Cómo se aprendió la ruta

#### Tipos de rutas:
- **Conectadas directamente**: Interfaces del router
- **Estáticas**: Configuradas manualmente
- **Dinámicas**: Aprendidas por protocolos

### Comandos de configuración básica:

#### Configuración inicial:
```bash
# Modo global de configuración
enable
configure terminal

# Hostname
hostname R1

# Configuración de interfaz
interface fastethernet 0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
description "LAN interna"

interface serial 0/0/0
ip address 10.1.1.1 255.255.255.252
no shutdown
description "Enlace a R2"

# Ruta estática
ip route 192.168.2.0 255.255.255.0 10.1.1.2

# Ruta por defecto
ip route 0.0.0.0 0.0.0.0 10.1.1.2
```

#### Comandos de verificación:
```bash
# Ver tabla de enrutamiento
show ip route

# Ver configuración de interfaces
show ip interface brief
show interfaces

# Probar conectividad
ping 192.168.2.1
traceroute 192.168.2.1

# Ver protocolos de enrutamiento
show ip protocols

# Ver estadísticas
show version
show running-config
```

### Protocolos de enrutamiento:

#### RIP (Routing Information Protocol):
- **Vector distancia**: Métrica basada en hop count
- **Máximo 15 saltos**: 16 = inalcanzable
- **Actualizaciones periódicas**: Cada 30 segundos
- **Simple**: Configuración básica

#### OSPF (Open Shortest Path First):
- **Estado de enlace**: Conoce toda la topología
- **Sin límite de saltos**: Métrica basada en costo
- **Convergencia rápida**: Actualizaciones por eventos
- **Escalable**: Soporta jerarquías (áreas)

#### EIGRP (Enhanced Interior Gateway Routing Protocol):
- **Vector distancia avanzado**: Múltiples métricas
- **Protocolo propietario**: Cisco
- **Convergencia rápida**: DUAL algorithm
- **Balanceo de carga**: Múltiples rutas de costo igual

## Laboratorios Prácticos

### Lab 1: Cableado y conectores
1. Crear cables UTP directos y cruzados
2. Probar conectividad con tester de cables
3. Configurar diferentes tipos de conectores

### Lab 2: Configuración de switches
1. Configuración básica de switch Cisco
2. Crear y asignar VLANs
3. Configurar trunk ports

### Lab 3: Configuración de routers
1. Configuración básica de router
2. Configurar rutas estáticas
3. Implementar protocolos de enrutamiento dinámico

### Lab 4: Diseño de red completa
1. Planificar esquema de direccionamiento
2. Implementar VLSMs
3. Configurar conectividad completa

## Evaluación

1. **Práctica**: Construcción y prueba de cables
2. **Configuración**: Setup completo de red pequeña
3. **Troubleshooting**: Diagnóstico y solución de problemas
4. **Diseño**: Propuesta de red para escenario dado

[⬅️ Anterior: Topologías de red.](./TopologiasRed.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Tipos de cables de red. ➡️](../Unidad3-CableadoEstructurado/TiposCables.md)