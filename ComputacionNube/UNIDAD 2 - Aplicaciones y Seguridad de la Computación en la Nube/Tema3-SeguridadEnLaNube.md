# Tema 3: Seguridad en la Nube

## Fundamentos de la seguridad en la nube

### Diferencia entre seguridad "en la nube" y "de la nube"

#### Seguridad "DE la nube" (Security OF the cloud)
- **Responsabilidad del proveedor de servicios en la nube**
- **Incluye**:
  - Seguridad física de los centros de datos
  - Infraestructura de red
  - Hipervisores
  - Servicios de plataforma
  - Cumplimiento de estándares de seguridad

#### Seguridad "EN la nube" (Security IN the cloud)
- **Responsabilidad del cliente/usuario**
- **Incluye**:
  - Gestión de identidades y accesos
  - Configuración de aplicaciones
  - Sistemas operativos invitados
  - Datos del cliente
  - Cifrado de datos

## Modelo de responsabilidad compartida

### Principio fundamental
La seguridad en la nube es una responsabilidad compartida entre el proveedor de servicios en la nube y el cliente. La división de responsabilidades varía según el modelo de servicio utilizado.

### Responsabilidades por modelo de servicio

#### IaaS (Infraestructura como Servicio)
- **Proveedor responsable de**:
  - Infraestructura física
  - Red y hipervisor
  - Seguridad del host
- **Cliente responsable de**:
  - Sistema operativo
  - Aplicaciones
  - Configuración de red
  - Datos

#### PaaS (Plataforma como Servicio)
- **Proveedor responsable de**:
  - Todo lo de IaaS +
  - Sistema operativo
  - Runtime de aplicaciones
  - Middleware
- **Cliente responsable de**:
  - Aplicaciones
  - Datos
  - Gestión de usuarios

#### SaaS (Software como Servicio)
- **Proveedor responsable de**:
  - Todo lo de PaaS +
  - Aplicaciones
- **Cliente responsable de**:
  - Datos
  - Gestión de usuarios y accesos

## Medidas de seguridad clave

### Identidad y acceso (IAM - Identity and Access Management)

#### Componentes principales
- **Autenticación**: Verificar la identidad del usuario
- **Autorización**: Determinar qué puede hacer el usuario autenticado
- **Gestión de cuentas**: Crear, modificar y eliminar cuentas de usuario

#### Mejores prácticas
- **Principio de menor privilegio**: Otorgar solo los permisos mínimos necesarios
- **Autenticación multifactor (MFA)**: Usar múltiples factores para verificar identidad
- **Rotación regular de credenciales**: Cambiar passwords y claves de acceso periódicamente
- **Revisión periódica de accesos**: Auditar y actualizar permisos regularmente

#### Herramientas comunes
- AWS IAM
- Azure Active Directory
- Google Cloud Identity and Access Management
- Okta, Auth0 (soluciones de terceros)

### Cifrado de datos

#### Cifrado en tránsito
- **Propósito**: Proteger datos mientras se mueven entre ubicaciones
- **Tecnologías**:
  - TLS/SSL para comunicaciones web
  - VPN para conexiones de red
  - IPSec para túneles seguros
- **Implementación**:
  - HTTPS para aplicaciones web
  - Certificados SSL/TLS válidos
  - Protocolos seguros para APIs

#### Cifrado en reposo
- **Propósito**: Proteger datos almacenados en discos, bases de datos, etc.
- **Tecnologías**:
  - AES (Advanced Encryption Standard)
  - Cifrado a nivel de disco
  - Cifrado a nivel de base de datos
- **Gestión de claves**:
  - Servicios de gestión de claves (KMS)
  - Rotación automática de claves
  - Separación de claves y datos

### Monitoreo y auditoría

#### Componentes del monitoreo
- **Logging**: Registro detallado de eventos y actividades
- **Monitoring**: Supervisión en tiempo real de sistemas y aplicaciones
- **Alertas**: Notificaciones automáticas ante eventos sospechosos
- **Análisis**: Procesamiento y correlación de logs y métricas

#### Herramientas de monitoreo
- **Nativas de proveedores**:
  - AWS CloudTrail, CloudWatch
  - Azure Monitor, Security Center
  - Google Cloud Logging, Security Command Center
- **Soluciones de terceros**:
  - Splunk
  - Elastic Stack (ELK)
  - Datadog

#### Indicadores clave de seguridad
- Intentos de acceso fallidos
- Accesos desde ubicaciones inusuales
- Cambios en configuraciones críticas
- Transferencias de datos inusuales
- Actividad fuera del horario normal

## Frameworks y estándares de seguridad

### Marcos de referencia
- **NIST Cybersecurity Framework**
- **ISO 27001/27002**
- **COBIT**
- **CSA Cloud Controls Matrix (CCM)**

### Certificaciones y cumplimiento
- **SOC 2 (Service Organization Control 2)**
- **ISO 27001**
- **FedRAMP** (para gobierno de EE.UU.)
- **GDPR** (Reglamento General de Protección de Datos)
- **HIPAA** (para sector salud)

## Amenazas comunes en la nube

### Tipos de amenazas
1. **Violación de datos**
2. **Configuración incorrecta**
3. **Acceso no autorizado**
4. **Ataques de denegación de servicio (DDoS)**
5. **Malware y ransomware**
6. **Amenazas internas**

### Estrategias de mitigación
- Implementación de controles de seguridad por capas
- Formación y concienciación del personal
- Pruebas de penetración regulares
- Planes de respuesta a incidentes
- Copias de seguridad y planes de recuperación

## Arquitectura de seguridad en la nube

### Principios de diseño seguro
- **Defensa en profundidad**
- **Fail secure** (fallar de manera segura)
- **Seguridad por diseño**
- **Zero Trust** (confianza cero)

### Componentes arquitecturales
- **Firewalls de aplicación web (WAF)**
- **Redes privadas virtuales (VPN)**
- **Segmentación de red**
- **Sistemas de detección y prevención de intrusiones**

## Actividades de aprendizaje
1. Analiza el modelo de responsabilidad compartida para un escenario específico
2. Configura autenticación multifactor en un servicio en la nube
3. Implementa cifrado de datos en una aplicación simple
4. Diseña un plan de monitoreo de seguridad para una organización

## Referencias
- NIST Special Publication 800-144: Guidelines for Security and Privacy in Public Cloud Computing
- CSA Security Guidance for Cloud Computing
- ENISA Cloud Security Guide
