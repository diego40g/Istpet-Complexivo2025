# Tema 4: Aplicaciones en la Nube

## Tipos de aplicaciones en la nube

### Aplicaciones nativas de la nube (Cloud-native applications)

#### Definición
Aplicaciones diseñadas específicamente para aprovechar al máximo las características de la nube, construidas desde el inicio para funcionar en entornos distribuidos y escalables.

#### Características principales
- **Microservicios**: Arquitectura basada en servicios pequeños e independientes
- **Contenedores**: Empaquetado ligero y portable
- **Orquestación**: Gestión automática de contenedores
- **DevOps**: Integración de desarrollo y operaciones
- **API-first**: Diseño centrado en APIs
- **Stateless**: Sin estado persistente en la aplicación

#### Principios de diseño
1. **Resilencia**: Capacidad de recuperarse de fallos
2. **Escalabilidad**: Capacidad de crecer o decrecer según demanda
3. **Observabilidad**: Monitoreo, logging y trazabilidad
4. **Automatización**: Despliegue y gestión automática
5. **Seguridad**: Integrada desde el diseño

#### Ventajas
- Mayor agilidad en el desarrollo
- Escalabilidad automática
- Menor tiempo de inactividad
- Optimización de costos
- Facilidad de actualización

### Aplicaciones migradas (Lift and Shift)

#### Definición
Mover software existente a la nube con modificaciones mínimas o nulas en la arquitectura original.

#### Enfoques de migración

##### 1. Rehosting (Lift and Shift)
- **Descripción**: Mover aplicaciones tal como están
- **Ventajas**: Rápido, bajo riesgo
- **Desventajas**: No aprovecha beneficios de la nube

##### 2. Replatforming (Lift, Tinker and Shift)
- **Descripción**: Hacer algunas optimizaciones menores
- **Ejemplos**: Cambiar base de datos, usar servicios gestionados
- **Balance**: Beneficios moderados, complejidad moderada

##### 3. Refactoring/Re-architecting
- **Descripción**: Rediseñar la aplicación para la nube
- **Beneficios**: Máximo aprovechamiento de capacidades de la nube
- **Desafíos**: Mayor tiempo y costo

##### 4. Repurchasing
- **Descripción**: Cambiar a un producto SaaS
- **Casos**: Reemplazar CRM on-premise con Salesforce

##### 5. Retaining
- **Descripción**: Mantener aplicaciones on-premise
- **Razones**: Compliance, latencia, costo

##### 6. Retiring
- **Descripción**: Eliminar aplicaciones no necesarias
- **Beneficio**: Reducción de costos y complejidad

## Desarrollo y despliegue de aplicaciones

### Contenedores

#### ¿Qué son los contenedores?
Los contenedores son una forma de empaquetar aplicaciones y sus dependencias para que se ejecuten de manera consistente en cualquier entorno.

#### Características principales
- **Portabilidad**: Ejecutan igual en cualquier entorno
- **Eficiencia**: Menor overhead que las máquinas virtuales
- **Consistencia**: "Funciona en mi máquina" ya no es problema
- **Aislamiento**: Separación entre aplicaciones
- **Versionado**: Control de versiones de imágenes

#### Tecnologías clave

##### Docker
- **Plataforma de contenedores más popular**
- **Componentes**:
  - Docker Engine: Runtime de contenedores
  - Docker Images: Plantillas para crear contenedores
  - Dockerfile: Archivo de configuración para construir imágenes
  - Docker Registry: Repositorio de imágenes

##### Ejemplo de Dockerfile
```dockerfile
FROM node:14
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

#### Beneficios de los contenedores
- **Desarrollo**: Entornos consistentes
- **Testing**: Pruebas reproducibles
- **Despliegue**: Implementación confiable
- **Escalado**: Fácil escalamiento horizontal

### Orquestación de contenedores

#### Necesidad de orquestación
Cuando tienes muchos contenedores, necesitas herramientas para:
- Gestionar el ciclo de vida
- Balancear carga
- Escalar automáticamente
- Gestionar la red
- Manejar almacenamiento
- Asegurar alta disponibilidad

#### Kubernetes

##### ¿Qué es Kubernetes?
Sistema de orquestación de contenedores de código abierto que automatiza el despliegue, escalado y gestión de aplicaciones contenedorizadas.

##### Componentes principales
- **Cluster**: Conjunto de nodos que ejecutan aplicaciones contenedorizadas
- **Node**: Máquina de trabajo en Kubernetes
- **Pod**: Unidad básica de despliegue
- **Service**: Abstracción que define un conjunto lógico de Pods
- **Deployment**: Describe el estado deseado de la aplicación

##### Beneficios de Kubernetes
- **Escalado automático**: Horizontal Pod Autoscaler
- **Auto-healing**: Reinicia contenedores que fallan
- **Balanceo de carga**: Distribuye tráfico automáticamente
- **Actualizaciones sin tiempo de inactividad**: Rolling updates
- **Gestión de configuración**: ConfigMaps y Secrets

#### Servicios de orquestación en la nube
- **Amazon EKS** (Elastic Kubernetes Service)
- **Azure AKS** (Azure Kubernetes Service)
- **Google GKE** (Google Kubernetes Engine)
- **Docker Swarm**
- **Apache Mesos**

## Casos de uso y ejemplos

### Almacenamiento y copias de seguridad

#### Dropbox
- **Modelo**: SaaS para almacenamiento personal y empresarial
- **Características**:
  - Sincronización automática
  - Versionado de archivos
  - Colaboración en tiempo real
  - Acceso multiplataforma
- **Arquitectura**: Microservicios, almacenamiento distribuido

#### Google Drive
- **Integración**: Con suite de productividad (Google Workspace)
- **Colaboración**: Edición simultánea de documentos
- **Inteligencia**: Búsqueda inteligente con IA

### Transmisión de contenido

#### Netflix
- **Arquitectura**: Microservicios masivos en AWS
- **Tecnologías clave**:
  - CDN (Content Delivery Network)
  - Algoritmos de recomendación con ML
  - Streaming adaptativo
  - Chaos Engineering para resiliencia
- **Escalabilidad**: Maneja millones de usuarios concurrentes

#### Componentes técnicos
- **Encoding**: Optimización de video para diferentes dispositivos
- **Caching**: Almacenamiento distribuido de contenido
- **Personalización**: Recomendaciones basadas en IA
- **Monitoreo**: Observabilidad avanzada

### Software empresarial

#### Salesforce
- **Pionero en SaaS**: Primera plataforma CRM en la nube
- **Modelo multi-tenant**: Una instancia sirve múltiples clientes
- **Personalización**: Configuración sin programación
- **Ecosystem**: AppExchange con miles de aplicaciones

#### Microsoft Office 365 / Microsoft 365
- **Suite completa**: Productividad, colaboración, comunicación
- **Integración**: Ecosistema completo de herramientas
- **Seguridad**: Herramientas avanzadas de protección
- **Movilidad**: Acceso desde cualquier dispositivo

## Patrones de arquitectura en la nube

### Patrones de diseño comunes
1. **API Gateway**: Punto único de entrada para microservicios
2. **Circuit Breaker**: Prevención de fallos en cascada
3. **Event Sourcing**: Almacenar eventos en lugar de estado
4. **CQRS**: Separación de comandos y consultas
5. **Saga Pattern**: Transacciones distribuidas

### Mejores prácticas
- **Diseño para el fallo**: Asumir que los componentes fallarán
- **Idempotencia**: Operaciones seguras para repetir
- **Monitoring y alertas**: Observabilidad completa
- **Documentación de APIs**: Facilitar integración
- **Testing automatizado**: CI/CD completo

## Tecnologías emergentes

### Serverless Computing
- **Function as a Service (FaaS)**
- **Backend as a Service (BaaS)**
- **Event-driven architecture**

### Progressive Web Apps (PWAs)
- **Experiencia similar a aplicaciones nativas**
- **Funcionamiento offline**
- **Instalación desde el navegador**

### Edge Computing
- **Procesamiento cerca del usuario**
- **Menor latencia**
- **Aplicaciones IoT**

## Actividades de aprendizaje
1. Compara una aplicación nativa de la nube vs una aplicación migrada
2. Crea un contenedor Docker simple para una aplicación web
3. Investiga la arquitectura de Netflix o Spotify
4. Diseña un plan de migración para una aplicación legacy
5. Explora servicios serverless y crea una función simple

## Referencias
- The Twelve-Factor App Methodology
- Kubernetes Documentation
- Docker Best Practices
- Cloud Native Computing Foundation (CNCF)
- Microservices Patterns by Chris Richardson
