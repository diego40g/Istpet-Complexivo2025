# Tema 6: Redes Virtuales

## Introducción a las redes virtuales

### Definición
Las redes virtuales son abstracciones de software que permiten crear redes lógicas independientes que operan sobre una infraestructura física compartida. Esta tecnología es fundamental en los entornos de nube para proporcionar aislamiento, seguridad y flexibilidad.

### Importancia en la computación en la nube
- **Aislamiento**: Separación lógica de tráfico entre diferentes aplicaciones y usuarios
- **Seguridad**: Control granular sobre el flujo de datos
- **Escalabilidad**: Fácil expansión y modificación de topologías de red
- **Flexibilidad**: Configuración dinámica sin cambios físicos

## Componentes de las redes virtuales

### Virtual Private Cloud (VPC)
Una VPC es una red privada virtual que proporciona un entorno de red aislado dentro de la infraestructura de nube pública.

#### Características principales
- **Aislamiento lógico**: Separación completa de otros usuarios
- **Control de direccionamiento IP**: Definición de rangos de direcciones privadas
- **Subredes configurables**: División en segmentos más pequeños
- **Tablas de ruteo personalizadas**: Control del flujo de tráfico

#### Beneficios de VPC
- Seguridad mejorada con controles de acceso granulares
- Flexibilidad en la configuración de red
- Integración con recursos on-premise mediante VPN
- Escalabilidad automática según demanda

### Subredes (Subnets)
Las subredes dividen la VPC en segmentos más pequeños para organizar y aislar recursos.

#### Tipos de subredes
1. **Subredes públicas**:
   - Acceso directo a Internet
   - Recursos con direcciones IP públicas
   - Ideal para servidores web, balanceadores de carga

2. **Subredes privadas**:
   - Sin acceso directo a Internet
   - Comunicación saliente a través de NAT Gateway
   - Ideal para bases de datos, servidores de aplicaciones

3. **Subredes de base de datos**:
   - Aislamiento adicional para datos sensibles
   - Controles de acceso específicos
   - Optimizadas para workloads de base de datos

### Gateways y conectividad

#### Internet Gateway (IGW)
- Proporciona conectividad bidireccional con Internet
- Se adjunta a la VPC
- Permite tráfico entrante y saliente

#### NAT Gateway/Instance
- **NAT Gateway**: Servicio gestionado para tráfico saliente desde subredes privadas
- **NAT Instance**: VM configurada para realizar traducción de direcciones
- Solo permite tráfico saliente iniciado desde la subnet privada

#### Virtual Private Gateway (VGW)
- Punto de conexión para VPNs site-to-site
- Conecta la VPC con redes on-premise
- Soporte para múltiples conexiones VPN

## Tecnologías de virtualización de red

### Software-Defined Networking (SDN)

#### Definición
SDN es un enfoque arquitectural que permite el control programático de la red mediante la separación del plano de control del plano de datos.

#### Componentes principales
1. **Controlador SDN**: Cerebro centralizado de la red
2. **Switches programables**: Dispositivos de red controlados por software
3. **APIs northbound/southbound**: Interfaces de comunicación
4. **Aplicaciones de red**: Lógica de control de alto nivel

#### Beneficios de SDN
- **Gestión centralizada**: Control unificado de toda la red
- **Programabilidad**: Configuración mediante código
- **Flexibilidad**: Cambios rápidos en políticas y configuraciones
- **Innovación**: Desarrollo de nuevas funcionalidades de red

### Network Function Virtualization (NFV)

#### Concepto
NFV virtualiza funciones de red tradicionalmente ejecutadas en hardware dedicado, implementándolas como software en servidores estándar.

#### Funciones virtualizadas comunes
- **Virtual Firewall**: Seguridad perimetral como servicio
- **Load Balancer virtual**: Distribución de carga programática
- **Virtual Router**: Enrutamiento definido por software
- **VPN concentrator**: Terminación de túneles VPN
- **IDS/IPS virtual**: Detección y prevención de intrusiones

#### Arquitectura NFV
1. **NFVI (NFV Infrastructure)**: Infraestructura subyacente
2. **VNF (Virtual Network Functions)**: Funciones de red virtualizadas
3. **MANO (Management and Orchestration)**: Gestión y orquestación

### Open vSwitch (OVS)
Switch virtual de código abierto que implementa funcionalidades avanzadas:
- **Soporte para OpenFlow**: Protocolo SDN estándar
- **VLAN y tunneling**: Segmentación y encapsulación
- **Quality of Service (QoS)**: Gestión de ancho de banda
- **Monitoreo**: Visibilidad del tráfico de red

## Seguridad en redes virtuales

### Network Access Control Lists (NACLs)

#### Características
- Control de tráfico a nivel de subred
- Reglas stateless (sin estado)
- Orden de evaluación por número de regla
- Aplicación a todo el tráfico de la subred

#### Diferencias con Security Groups
| Aspecto | NACLs | Security Groups |
|---------|--------|-----------------|
| Nivel | Subred | Instancia |
| Estado | Stateless | Stateful |
| Reglas | Permiso y denegación | Solo permiso |
| Evaluación | Secuencial por número | Todas las reglas |

### Security Groups
Firewalls virtuales que controlan el tráfico a nivel de instancia:
- **Stateful**: Retorna tráfico automáticamente permitido
- **Reglas de ingreso y egreso**: Control bidireccional
- **Grupos como origen/destino**: Referencias entre security groups
- **Aplicación automática**: Cambios inmediatos

### Micro-segmentación
Estrategia de seguridad que crea zonas seguras pequeñas para aislar cargas de trabajo:
- **Zero Trust Network**: No confianza por defecto
- **Políticas granulares**: Control por aplicación/servicio
- **Inspección de tráfico**: Análisis profundo de paquetes
- **Respuesta automática**: Mitigación automática de amenazas

## Conectividad híbrida

### VPN Site-to-Site

#### Tipos de conexiones VPN
1. **IPsec VPN**:
   - Protocolo estándar para VPNs
   - Cifrado fuerte y autenticación
   - Compatible con la mayoría de equipos

2. **SSL/TLS VPN**:
   - Acceso basado en navegador web
   - Ideal para usuarios remotos
   - Fácil configuración cliente

#### Configuración de VPN
- **Customer Gateway**: Dispositivo o software en el lado del cliente
- **Virtual Private Gateway**: Terminación VPN en la nube
- **Túneles redundantes**: Alta disponibilidad con múltiples túneles
- **Routing dinámico**: BGP para intercambio automático de rutas

### Direct Connect / Express Route

#### Conexiones dedicadas
- **Ancho de banda garantizado**: Desde 50 Mbps hasta 100 Gbps
- **Latencia consistente**: Conexión directa sin Internet
- **Costos predictibles**: Tarifas fijas mensuales
- **Múltiples VLANs**: Separación de tráfico por servicio

#### Beneficios de conexiones dedicadas
- **Rendimiento**: Mayor throughput y menor latencia
- **Seguridad**: Tráfico no pasa por Internet público
- **Compliance**: Cumplimiento regulatorio mejorado
- **Costos**: Reducción en costos de transferencia de datos

### Híbrido y Multi-Cloud Networking

#### Arquitecturas híbridas
- **Burst to cloud**: Expansión temporal a la nube
- **DR/Backup**: Recuperación ante desastres
- **Data analytics**: Procesamiento en la nube
- **Modernización gradual**: Migración por fases

#### Desafíos de redes híbridas
- **Latencia**: Impacto en aplicaciones sensibles al tiempo
- **Ancho de banda**: Limitaciones de conectividad
- **Seguridad**: Consistencia entre entornos
- **Gestión**: Complejidad operacional aumentada

## Monitoreo y troubleshooting

### Herramientas de monitoreo

#### Flow Logs
- **VPC Flow Logs**: Captura de metadatos de tráfico IP
- **Análisis de patrones**: Identificación de anomalías
- **Troubleshooting**: Diagnóstico de problemas de conectividad
- **Seguridad**: Detección de actividad maliciosa

#### Network monitoring tools
1. **CloudWatch Network Insights**:
   - Métricas de red en tiempo real
   - Alertas automáticas
   - Dashboards personalizados

2. **AWS X-Ray / Azure Network Watcher**:
   - Trazabilidad end-to-end
   - Análisis de latencia
   - Mapeo de dependencias

3. **Herramientas de terceros**:
   - Datadog Network Performance Monitoring
   - New Relic Network
   - SolarWinds NPM

### Troubleshooting común

#### Problemas de conectividad
1. **Verificar Security Groups y NACLs**
2. **Confirmar tablas de ruteo**
3. **Validar DNS resolution**
4. **Comprobar conectividad física**

#### Herramientas de diagnóstico
- **ping/traceroute**: Conectividad básica
- **telnet/ncat**: Pruebas de puertos específicos
- **dig/nslookup**: Resolución DNS
- **iperf/iperf3**: Pruebas de throughput

## Optimización de rendimiento

### Best practices para redes virtuales

#### Diseño de arquitectura
1. **Separación por función**: Subredes especializadas
2. **Múltiples AZs**: Alta disponibilidad geográfica
3. **Sizing adecuado**: Dimensionamiento correcto de subredes
4. **Ruteo eficiente**: Minimizar saltos innecesarios

#### Optimización de tráfico
- **CDN integration**: Content Delivery Networks
- **Caching strategies**: Reducción de tráfico WAN
- **Compression**: Compresión de datos en tránsito
- **Traffic shaping**: Priorización de tráfico crítico

### Automatización y Infrastructure as Code

#### Herramientas de automatización
1. **Terraform**: Provisionamiento multi-cloud
2. **CloudFormation**: Nativo de AWS
3. **ARM Templates**: Nativo de Azure
4. **Ansible**: Configuración y orquestación

#### Ventajas de IaC para redes
- **Consistencia**: Configuraciones reproducibles
- **Versionado**: Control de cambios
- **Testing**: Validación automatizada
- **Rollback**: Reversión rápida de cambios

## Casos de uso prácticos

### Arquitectura de tres capas
```
Internet → Load Balancer (Subnet pública)
    ↓
Aplicaciones (Subnet privada)
    ↓
Base de datos (Subnet de DB)
```

#### Implementación
- **Subnet pública**: Load balancer con IP pública
- **Subnet privada**: Servidores de aplicación
- **Subnet de DB**: Bases de datos con acceso restringido

### Microservicios en contenedores
- **Service mesh**: Istio, Linkerd para comunicación entre servicios
- **Ingress controllers**: NGINX, Traefik para enrutamiento
- **Network policies**: Kubernetes para micro-segmentación

### Data lake architecture
- **Zonas de red diferenciadas**: Raw, processed, curated
- **Acceso controlado**: Políticas basadas en roles
- **Optimización de transferencias**: Compresión y paralelización

## Tendencias emergentes

### Intent-Based Networking (IBN)
- **Definición por intención**: Configuración basada en objetivos de negocio
- **Automatización inteligente**: IA para optimización continua
- **Verificación automática**: Validación de políticas en tiempo real

### Network as Code
- **GitOps para redes**: Control de versiones para configuraciones
- **CI/CD pipelines**: Testing automatizado de cambios
- **Policy as Code**: Políticas de red como código fuente

### Edge computing networking
- **5G integration**: Aprovechamiento de redes 5G
- **Ultra-low latency**: Optimización para aplicaciones críticas
- **Distributed networking**: Redes distribuidas geográficamente

## Actividades de aprendizaje

### Laboratorios prácticos
1. **Crear una VPC básica**:
   - Configurar subredes públicas y privadas
   - Implementar gateway de Internet y NAT
   - Configurar tablas de ruteo

2. **Implementar seguridad de red**:
   - Configurar Security Groups
   - Crear NACLs personalizadas
   - Establecer conexión VPN

3. **Monitoreo y troubleshooting**:
   - Habilitar Flow Logs
   - Analizar patrones de tráfico
   - Diagnosticar problemas de conectividad

### Proyectos de diseño
1. **Arquitectura híbrida**:
   - Diseñar conectividad on-premise a nube
   - Planificar migración gradual
   - Considerar aspectos de seguridad y compliance

2. **Red para microservicios**:
   - Diseñar arquitectura de red para contenedores
   - Implementar service mesh
   - Configurar políticas de red

## Referencias y recursos

### Documentación oficial
- AWS VPC User Guide
- Azure Virtual Network Documentation
- Google Cloud VPC Documentation
- Cisco SD-WAN Solution Guide

### Libros especializados
- "Network Programmability and Automation" por Jason Edelman
- "SDN: Software Defined Networks" por Thomas D. Nadeau
- "Cloud Native Networking" por Chris Haddad

### Certificaciones relacionadas
- AWS Certified Advanced Networking
- Azure Network Engineer Associate
- Google Cloud Professional Cloud Network Engineer
- Cisco DevNet Professional

### Herramientas de práctica
- GNS3 para simulación de redes
- EVE-NG para laboratorios virtuales
- Packet Tracer para conceptos básicos
- Mininet para redes SDN
