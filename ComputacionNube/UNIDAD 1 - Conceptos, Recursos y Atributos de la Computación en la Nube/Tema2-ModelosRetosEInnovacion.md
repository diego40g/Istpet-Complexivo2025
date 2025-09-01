# Tema 2: Modelos, Retos e Innovación de la Computación en la Nube

## Modelos de despliegue

### Nube pública
- **Definición**: Servicios ofrecidos a cualquier persona a través de la web
- **Características**:
  - Propiedad de terceros (proveedores de servicios en la nube)
  - Acceso abierto al público general
  - Recursos compartidos entre múltiples organizaciones
- **Ventajas**:
  - Menor costo inicial
  - Alta escalabilidad
  - Mantenimiento gestionado por el proveedor
- **Ejemplos**: AWS, Microsoft Azure, Google Cloud Platform

### Nube privada
- **Definición**: Recursos dedicados a una sola organización
- **Características**:
  - Uso exclusivo de una organización
  - Mayor control y personalización
  - Puede estar ubicada en las instalaciones de la organización o externamente
- **Ventajas**:
  - Mayor seguridad y privacidad
  - Control total sobre la infraestructura
  - Cumplimiento regulatorio más fácil
- **Desventajas**:
  - Mayor costo inicial
  - Responsabilidad de mantenimiento

### Nube híbrida
- **Definición**: Una combinación de nubes públicas y privadas
- **Características**:
  - Integración entre entornos públicos y privados
  - Permite mover datos y aplicaciones entre nubes
  - Flexibilidad en la colocación de cargas de trabajo
- **Casos de uso**:
  - Burst to cloud (expandir a la nube pública cuando sea necesario)
  - Mantener datos sensibles en nube privada
  - Desarrollo en nube pública, producción en nube privada

### Nube comunitaria
- **Definición**: Compartida por varias organizaciones con intereses comunes
- **Características**:
  - Uso compartido entre organizaciones con objetivos similares
  - Costos compartidos
  - Requisitos de seguridad, política y cumplimiento similares
- **Ejemplos**: Nubes para instituciones educativas, organizaciones gubernamentales

## Retos de la computación en la nube

### Seguridad y privacidad
- **Preocupaciones principales**:
  - ¿Dónde están mis datos?
  - ¿Están seguros?
  - ¿Quién tiene acceso a ellos?
- **Aspectos importantes**:
  - Cifrado de datos en tránsito y en reposo
  - Gestión de identidades y accesos
  - Cumplimiento de regulaciones (GDPR, HIPAA, etc.)

### Compatibilidad e interoperabilidad
- **Problemas**:
  - ¿Puedo mover mis aplicaciones entre diferentes proveedores?
  - Estándares diversos entre proveedores
  - APIs propietarias
- **Soluciones**:
  - Adopción de estándares abiertos
  - Uso de contenedores
  - Arquitecturas basadas en microservicios

### Dependencia del proveedor (Vendor Lock-in)
- **Riesgo**: Quedarse "encerrado" con un solo proveedor
- **Consecuencias**:
  - Dificultad para migrar
  - Pérdida de poder de negociación
  - Dependencia técnica
- **Estrategias de mitigación**:
  - Arquitectura multi-nube
  - Uso de tecnologías portables
  - Planificación de estrategias de salida

## Innovación en la nube

### Computación sin servidor (Serverless)
- **Definición**: Ejecutar código sin gestionar servidores
- **Características**:
  - Escalado automático
  - Pago por uso real
  - Sin gestión de infraestructura
- **Ejemplos**: AWS Lambda, Azure Functions, Google Cloud Functions
- **Casos de uso**:
  - APIs REST
  - Procesamiento de eventos
  - Automatización de tareas

### Edge Computing
- **Definición**: Procesar datos más cerca de donde se generan, en el "borde" de la red
- **Beneficios**:
  - Menor latencia
  - Reducción del ancho de banda
  - Mayor privacidad de datos
- **Aplicaciones**:
  - IoT (Internet de las Cosas)
  - Vehículos autónomos
  - Realidad aumentada y virtual

### Inteligencia artificial y aprendizaje automático como servicio (AI/ML as a Service)
- **Definición**: Usar poderosas herramientas de IA sin la complejidad de construirlas desde cero
- **Servicios disponibles**:
  - Reconocimiento de imágenes
  - Procesamiento de lenguaje natural
  - Análisis predictivo
- **Ejemplos**:
  - Amazon SageMaker
  - Google AI Platform
  - Azure Machine Learning

## Tendencias emergentes
- **Computación cuántica en la nube**
- **Sostenibilidad y computación verde**
- **Automatización e infraestructura como código**
- **Multi-cloud y gestión híbrida**

## Actividades de aprendizaje
1. Compara los modelos de despliegue y determina cuál sería más adecuado para diferentes tipos de organizaciones
2. Investiga casos reales de vendor lock-in y cómo se resolvieron
3. Explora servicios serverless y crea un ejemplo simple
4. Analiza el impacto del edge computing en aplicaciones IoT

## Referencias
- Cloud Computing: Principles and Paradigms
- NIST Cloud Computing Standards
- Industry reports on cloud innovation trends
