# Actividad 6.1: Creación y Configuración de VPC Básica en AWS

## 🎯 Objetivo
Crear una Virtual Private Cloud (VPC) desde cero en Amazon Web Services, configurar subredes públicas y privadas, establecer gateways de Internet y NAT, y configurar tablas de ruteo para comprender la arquitectura de redes virtuales en la nube.

## 📋 Recursos necesarios
- Cuenta de AWS (Free Tier es suficiente)
- Navegador web
- Conocimientos básicos de redes TCP/IP
- Calculadora de subredes (opcional)

## 💰 Estimación de costos
**Con AWS Free Tier:** ~$0-5 USD por mes
- VPC, subredes, tablas de ruteo: Gratuito
- Internet Gateway: Gratuito
- NAT Gateway: ~$0.045/hora (limitado en Free Tier)
- Instancias EC2: Gratuito en t2.micro (750 horas/mes)

## ⏱️ Duración estimada
3-4 horas

## 🔧 Prerrequisitos

### Configuración de cuenta AWS:
1. **Crear cuenta AWS gratuita** (si no tienes): aws.amazon.com
2. **Configurar MFA** en cuenta root (recomendado)
3. **Crear usuario IAM** con permisos administrativos
4. **Familiarizarse** con la consola de AWS

### Conocimientos recomendados:
- Direcciones IP y subnetting
- Conceptos básicos de routing
- Diferencia entre subredes públicas y privadas

## 📝 Pasos a seguir

### Paso 1: Planificación de la arquitectura de red

#### A. Diseño de la VPC:
```
Arquitectura objetivo:
┌─────────────────────────────────────────────────────────────┐
│                    VPC: 10.0.0.0/16                        │
│                                                             │
│ ┌─────────────────────┐  ┌─────────────────────────────────┐ │
│ │   Public Subnet     │  │      Private Subnet             │ │
│ │   10.0.1.0/24      │  │      10.0.2.0/24               │ │
│ │                     │  │                                 │ │
│ │  [Web Server]       │  │   [Database Server]             │ │
│ │       │             │  │            │                   │ │
│ └───────│─────────────┘  └────────────│───────────────────┘ │
│         │                             │                     │
│    [Internet Gateway]              [NAT Gateway]            │
│         │                             │                     │
└─────────│─────────────────────────────┼─────────────────────┘
          │                             │
      [Internet]                   [Route to IGW]
```

#### B. Planificación de direccionamiento:
```
VPC CIDR: 10.0.0.0/16
├── Public Subnet:  10.0.1.0/24 (AZ: us-east-1a)
├── Private Subnet: 10.0.2.0/24 (AZ: us-east-1a)
├── Public Subnet:  10.0.3.0/24 (AZ: us-east-1b) [Para HA]
└── Private Subnet: 10.0.4.0/24 (AZ: us-east-1b) [Para HA]
```

### Paso 2: Creación de la VPC

#### A. Acceder al servicio VPC:
```
1. Login en AWS Management Console
2. Buscar "VPC" en servicios
3. Seleccionar "VPC" desde el dropdown
4. Asegurarse de estar en región correcta (ej: us-east-1)
```

#### B. Crear VPC:
```
1. En VPC Dashboard, clic "Create VPC"
2. Seleccionar "VPC only"
3. Configurar:
   - Name tag: "mi-vpc-lab"
   - IPv4 CIDR: 10.0.0.0/16
   - IPv6 CIDR: No IPv6 CIDR block
   - Tenancy: Default
4. Clic "Create VPC"
```

#### C. Verificar creación:
```
1. En VPC Dashboard, verificar que aparece la nueva VPC
2. Tomar nota del VPC ID (vpc-xxxxxxxxx)
3. Verificar que el estado sea "Available"
```

### Paso 3: Creación de subredes

#### A. Crear subnet pública:
```
1. En el panel izquierdo, clic "Subnets"
2. Clic "Create subnet"
3. Configurar:
   - VPC ID: Seleccionar "mi-vpc-lab"
   - Subnet name: "public-subnet-1a"
   - Availability Zone: us-east-1a
   - IPv4 CIDR block: 10.0.1.0/24
4. Clic "Create subnet"
```

#### B. Crear subnet privada:
```
1. Clic "Create subnet" nuevamente
2. Configurar:
   - VPC ID: Seleccionar "mi-vpc-lab"
   - Subnet name: "private-subnet-1a"
   - Availability Zone: us-east-1a
   - IPv4 CIDR block: 10.0.2.0/24
3. Clic "Create subnet"
```

#### C. Crear subnets adicionales para alta disponibilidad:
```
Subnet pública en segunda AZ:
- Subnet name: "public-subnet-1b"
- Availability Zone: us-east-1b
- IPv4 CIDR block: 10.0.3.0/24

Subnet privada en segunda AZ:
- Subnet name: "private-subnet-1b"
- Availability Zone: us-east-1b
- IPv4 CIDR block: 10.0.4.0/24
```

#### D. Configurar auto-assign IP pública:
```
1. Seleccionar "public-subnet-1a"
2. Actions → "Modify auto-assign IP settings"
3. Check "Enable auto-assign public IPv4 address"
4. Clic "Save"
5. Repetir para "public-subnet-1b"
```

### Paso 4: Creación y configuración de Internet Gateway

#### A. Crear Internet Gateway:
```
1. En panel izquierdo, clic "Internet Gateways"
2. Clic "Create internet gateway"
3. Configurar:
   - Name tag: "mi-vpc-igw"
4. Clic "Create internet gateway"
```

#### B. Adjuntar IGW a la VPC:
```
1. Seleccionar el IGW recién creado
2. Actions → "Attach to VPC"
3. Seleccionar "mi-vpc-lab"
4. Clic "Attach internet gateway"
5. Verificar que el estado sea "Attached"
```

### Paso 5: Configuración de tablas de ruteo

#### A. Identificar tabla de ruteo principal:
```
1. En panel izquierdo, clic "Route Tables"
2. Identificar la tabla asociada con "mi-vpc-lab"
3. Nombrarla: Seleccionar → Tags → Add tag
   - Key: Name
   - Value: "mi-vpc-main-rt"
```

#### B. Crear tabla de ruteo para subredes públicas:
```
1. Clic "Create route table"
2. Configurar:
   - Name: "public-route-table"
   - VPC: mi-vpc-lab
3. Clic "Create route table"
```

#### C. Añadir ruta a Internet en tabla pública:
```
1. Seleccionar "public-route-table"
2. Tab "Routes" → "Edit routes"
3. "Add route":
   - Destination: 0.0.0.0/0
   - Target: Internet Gateway → mi-vpc-igw
4. Clic "Save changes"
```

#### D. Asociar subredes públicas con tabla de ruteo pública:
```
1. En "public-route-table", tab "Subnet associations"
2. "Edit subnet associations"
3. Seleccionar:
   - public-subnet-1a
   - public-subnet-1b
4. Clic "Save associations"
```

### Paso 6: Creación de NAT Gateway para subredes privadas

#### A. Crear NAT Gateway:
```
1. En panel izquierdo, clic "NAT Gateways"
2. Clic "Create NAT Gateway"
3. Configurar:
   - Name: "mi-nat-gateway"
   - Subnet: public-subnet-1a (IMPORTANTE: En subnet pública)
   - Connectivity type: Public
   - Elastic IP allocation ID: "Allocate Elastic IP"
4. Clic "Create NAT Gateway"
```

#### B. Crear tabla de ruteo para subredes privadas:
```
1. Ir a "Route Tables"
2. Clic "Create route table"
3. Configurar:
   - Name: "private-route-table"
   - VPC: mi-vpc-lab
4. Clic "Create route table"
```

#### C. Añadir ruta al NAT Gateway:
```
1. Seleccionar "private-route-table"
2. Tab "Routes" → "Edit routes"
3. "Add route":
   - Destination: 0.0.0.0/0
   - Target: NAT Gateway → mi-nat-gateway
4. Clic "Save changes"
```

#### D. Asociar subredes privadas:
```
1. En "private-route-table", tab "Subnet associations"
2. "Edit subnet associations"
3. Seleccionar:
   - private-subnet-1a
   - private-subnet-1b
4. Clic "Save associations"
```

### Paso 7: Configuración de Security Groups

#### A. Crear Security Group para instancias web:
```
1. En panel izquierdo, clic "Security Groups"
2. Clic "Create security group"
3. Configurar:
   - Security group name: "web-server-sg"
   - Description: "Security group for web servers"
   - VPC: mi-vpc-lab

4. Inbound rules:
   - Type: HTTP, Port: 80, Source: 0.0.0.0/0
   - Type: HTTPS, Port: 443, Source: 0.0.0.0/0
   - Type: SSH, Port: 22, Source: Tu IP pública

5. Outbound rules: (Dejar por defecto - All traffic)
6. Clic "Create security group"
```

#### B. Crear Security Group para base de datos:
```
1. Clic "Create security group"
2. Configurar:
   - Security group name: "database-sg"
   - Description: "Security group for database servers"
   - VPC: mi-vpc-lab

3. Inbound rules:
   - Type: MySQL/Aurora, Port: 3306, Source: web-server-sg
   - Type: SSH, Port: 22, Source: web-server-sg

4. Outbound rules: (Dejar por defecto)
5. Clic "Create security group"
```

### Paso 8: Prueba de conectividad con instancias EC2

#### A. Lanzar instancia en subnet pública:
```
1. Ir a EC2 Dashboard
2. Clic "Launch Instance"
3. Configurar:
   - Name: "web-server-test"
   - AMI: Amazon Linux 2023 (Free tier eligible)
   - Instance type: t2.micro
   - Key pair: Crear nuevo o usar existente
   - Network settings:
     * VPC: mi-vpc-lab
     * Subnet: public-subnet-1a
     * Auto-assign public IP: Enable
     * Security group: web-server-sg
4. Clic "Launch instance"
```

#### B. Lanzar instancia en subnet privada:
```
1. Clic "Launch Instance"
2. Configurar:
   - Name: "database-server-test"
   - AMI: Amazon Linux 2023
   - Instance type: t2.micro
   - Key pair: El mismo que web server
   - Network settings:
     * VPC: mi-vpc-lab
     * Subnet: private-subnet-1a
     * Auto-assign public IP: Disable
     * Security group: database-sg
3. Clic "Launch instance"
```

### Paso 9: Verificación de conectividad

#### A. Conectar a instancia pública:
```
1. Obtener IP pública de web-server-test
2. SSH desde tu computadora:
   ssh -i tu-key.pem ec2-user@IP_PUBLICA

3. Verificar conectividad a Internet:
   ping google.com
   curl http://checkip.amazonaws.com
```

#### B. Conectar a instancia privada desde pública:
```
1. Desde la instancia pública, copiar key privada (NO recomendado en producción):
   # Método alternativo: usar SSH agent forwarding
   
2. Obtener IP privada de database-server-test (ej: 10.0.2.x)

3. SSH desde instancia pública:
   ssh -i tu-key.pem ec2-user@IP_PRIVADA

4. Verificar conectividad a Internet (vía NAT):
   ping google.com
   curl http://checkip.amazonaws.com  # Debería mostrar IP del NAT Gateway
```

### Paso 10: Monitoreo y troubleshooting

#### A. Verificar Flow Logs (opcional):
```
1. En VPC Dashboard, seleccionar tu VPC
2. Tab "Flow logs" → "Create flow log"
3. Configurar:
   - Filter: All
   - Destination: Send to CloudWatch Logs
   - Log group: VPCFlowLogs
4. Clic "Create flow log"
```

#### B. Comandos útiles para troubleshooting:
```bash
# En las instancias EC2
# Verificar configuración de red
ip addr show
ip route show

# Verificar DNS
nslookup google.com

# Verificar conectividad específica
telnet google.com 80

# Verificar NAT funcionando
curl http://checkip.amazonaws.com

# Ver logs del sistema
sudo journalctl -f
```

## 📤 Entregables

### 1. Documentación arquitectural
**Informe que incluya:**
- Diagrama de red creado
- Tabla de direccionamiento utilizado
- Configuración de cada componente
- Screenshots de cada paso importante

### 2. Evidencias de funcionamiento
**Capturas de pantalla que demuestren:**
- VPC Dashboard con todos los componentes
- Tablas de ruteo configuradas correctamente
- Security Groups creados
- Instancias EC2 ejecutándose
- Conexiones SSH exitosas
- Pruebas de conectividad desde terminal

### 3. Análisis de conectividad
**Documenta las siguientes pruebas:**
- Conectividad Internet desde instancia pública
- Conectividad Internet desde instancia privada vía NAT
- Comunicación entre instancias públicas y privadas
- Verificación de reglas de Security Groups

### 4. Cálculos de costos
**Análisis económico que incluya:**
- Costo actual de los recursos creados
- Proyección de costos mensuales
- Comparación con alternativas (VPN, conexión dedicada)
- Recomendaciones de optimización

### 5. Plan de troubleshooting
**Guía que documente:**
- Problemas comunes encontrados
- Pasos de diagnóstico utilizados
- Soluciones implementadas
- Comandos útiles para debugging

## 🔍 Puntos de análisis crítico

### Durante la implementación, analiza:

1. **Arquitectura de seguridad:**
   - ¿Por qué las instancias privadas no deberían tener IP pública?
   - ¿Cuál es el papel del NAT Gateway en la seguridad?
   - ¿Cómo funcionan las capas de seguridad (NACLs + Security Groups)?

2. **Eficiencia de costos:**
   - ¿El NAT Gateway es la opción más económica?
   - ¿Cuándo considerar NAT Instance vs NAT Gateway?
   - ¿Cómo optimizar costos de transferencia de datos?

3. **Disponibilidad y resiliencia:**
   - ¿Qué sucede si falla una Availability Zone?
   - ¿Por qué es importante tener subredes en múltiples AZs?
   - ¿Cómo se puede mejorar la arquitectura para HA?

4. **Escalabilidad:**
   - ¿Cómo se añadirían más subredes?
   - ¿Qué consideraciones hay para VPCs más grandes?
   - ¿Cuándo considerar VPC peering o Transit Gateway?

## ✅ Criterios de evaluación

### Excelente (90-100%)
- VPC completa funcionando con múltiples AZs
- Instancias en subredes públicas y privadas comunicándose
- Security Groups configurados correctamente
- Flow Logs configurados y analizados
- Documentación completa con análisis arquitectural
- Troubleshooting documentado con soluciones
- Análisis de costos detallado

### Bueno (80-89%)
- VPC básica funcionando correctamente
- Conectividad entre subredes establecida
- Security Groups básicos configurados
- Instancias de prueba funcionando
- Documentación clara y organizada
- Algunas pruebas de conectividad completadas

### Satisfactorio (70-79%)
- VPC creada con componentes básicos
- Al menos una instancia funcionando en cada tipo de subnet
- Documentación mínima requerida
- Screenshots básicos incluidos
- Cumplimiento de requisitos fundamentales

## 💡 Tips para el éxito

### Mejores prácticas:
- **Planifica el direccionamiento** antes de crear subredes
- **Usa nombres descriptivos** para todos los recursos
- **Documenta cada paso** con screenshots
- **Verifica conectividad** después de cada configuración
- **Monitorea costos** regularmente en Billing Dashboard

### Troubleshooting común:
- **No hay conectividad a Internet:** Verificar IGW y tablas de ruteo
- **Instancias privadas sin Internet:** Verificar NAT Gateway y rutas
- **SSH rechazado:** Verificar Security Groups y NACLs
- **DNS no resuelve:** Verificar configuración de VPC DNS
- **Costos inesperados:** NAT Gateway cobra por hora y transferencia

### Optimización:
- **Usa NAT Instance** si el tráfico es bajo para reducir costos
- **Centraliza NAT Gateways** para múltiples AZs si es apropiado
- **Configura VPC Endpoints** para servicios AWS frecuentes
- **Implementa Flow Logs** selectivamente para reducir costos
- **Revisa Security Groups** regularmente para mantener principio de menor privilegio

### Limpieza de recursos:
```bash
# Orden recomendado para eliminar recursos:
1. Terminar instancias EC2
2. Eliminar NAT Gateway
3. Liberar Elastic IPs
4. Eliminar subredes
5. Desasociar y eliminar Internet Gateway
6. Eliminar VPC
```
