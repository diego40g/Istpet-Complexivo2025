# Tema 1: Amenazas de la Información

## Índice de Contenidos
1. [Tipos de amenazas de la información](#tipos-de-amenazas-de-la-información)
2. [Políticas de Seguridad](#políticas-de-seguridad)
3. [Análisis de Riesgos](#análisis-de-riesgos)
4. [Ataques Informáticos](#ataques-informáticos)

---

## Tipos de amenazas de la información

### Definición de Amenazas
Una **amenaza** es cualquier circunstancia o evento con el potencial de impactar adversamente las operaciones organizacionales, activos, individuos u otras organizaciones a través del sistema de información mediante el acceso no autorizado, destrucción, divulgación, modificación de información y/o denegación de servicio.

### Clasificación de Amenazas

#### Por su Origen
- **Amenazas Internas**: Originadas desde dentro de la organización
  - Empleados descontentos
  - Accidentes por negligencia
  - Errores humanos no intencionados
  - Abuso de privilegios de acceso

- **Amenazas Externas**: Originadas desde fuera de la organización
  - Hackers y ciberdelincuentes
  - Competidores
  - Terroristas cibernéticos
  - Gobiernos hostiles

#### Por su Naturaleza
- **Amenazas Naturales**
  - Terremotos, inundaciones, incendios
  - Condiciones meteorológicas extremas
  - Cortes de energía eléctrica

- **Amenazas Humanas**
  - Espionaje industrial
  - Sabotaje
  - Robo de información
  - Ingeniería social

- **Amenazas Tecnológicas**
  - Fallas de hardware
  - Errores de software
  - Obsolescencia tecnológica
  - Incompatibilidades de sistemas

### Vectores de Amenaza Más Comunes

#### Malware
- **Virus**: Código malicioso que se replica insertándose en otros programas
- **Gusanos**: Programas autorreplicantes que se propagan a través de redes
- **Troyanos**: Software aparentemente legítimo que contiene código malicioso
- **Ransomware**: Malware que cifra archivos y exige rescate
- **Spyware**: Software que recopila información sin consentimiento

#### Ataques de Red
- **DDoS (Distributed Denial of Service)**: Saturación de servicios
- **Man-in-the-Middle**: Intercepción de comunicaciones
- **Packet Sniffing**: Captura de paquetes de red
- **IP Spoofing**: Falsificación de direcciones IP

#### Ingeniería Social
- **Phishing**: Suplantación de identidad para obtener credenciales
- **Pretexting**: Creación de escenarios falsos para obtener información
- **Baiting**: Uso de incentivos para atraer víctimas
- **Tailgating**: Acceso físico no autorizado siguiendo a personal autorizado

---

## Políticas de Seguridad

### Definición y Propósito
Las **políticas de seguridad** son documentos formales que establecen las reglas, procedimientos y directrices para proteger los activos de información de una organización. Proporcionan el marco para implementar controles de seguridad y definir responsabilidades.

### Elementos Clave de una Política de Seguridad

#### 1. Declaración de Propósito
- Objetivos de seguridad de la organización
- Alcance de la política
- Autoridad y responsabilidades

#### 2. Gestión de Accesos
```
Controles de Acceso:
├── Autenticación de usuarios
├── Autorización basada en roles
├── Principio de menor privilegio
└── Revisión periódica de accesos
```

#### 3. Uso Aceptable de Recursos
- Uso apropiado de sistemas y redes
- Prohibiciones específicas
- Responsabilidades del usuario
- Monitoreo de actividades

#### 4. Gestión de Incidentes
- Procedimientos de notificación
- Equipo de respuesta a incidentes
- Escalamiento de problemas
- Documentación y seguimiento

### Tipos de Políticas de Seguridad

#### Políticas Regulatorias
- Definen qué debe hacerse
- Obligatorias para toda la organización
- Establecen estándares mínimos

#### Políticas Consultivas
- Proporcionan recomendaciones
- Guían las mejores prácticas
- Flexibles en su implementación

#### Políticas Informativas
- Educan sobre temas específicos
- Proporcionan conocimiento general
- Apoyan la concienciación

### Implementación y Mantenimiento

#### Proceso de Desarrollo
1. **Evaluación de Necesidades**: Análisis de riesgos y requisitos
2. **Desarrollo de Borrador**: Creación de políticas preliminares
3. **Revisión y Aprobación**: Validación por stakeholders
4. **Implementación**: Despliegue y comunicación
5. **Monitoreo y Actualización**: Revisión periódica y mejoras

#### Factores Críticos de Éxito
- **Apoyo de la Alta Dirección**: Compromiso visible y recursos
- **Participación de Stakeholders**: Involucramiento de todas las partes
- **Comunicación Efectiva**: Difusión clara y accesible
- **Capacitación Continua**: Formación y concienciación del personal

---

## Análisis de Riesgos

### Conceptos Fundamentales

#### Definiciones Básicas
- **Riesgo**: Potencial de que una amenaza explote una vulnerabilidad
- **Amenaza**: Cualquier circunstancia que pueda impactar negativamente
- **Vulnerabilidad**: Debilidad que puede ser explotada
- **Activo**: Recurso valioso que requiere protección
- **Impacto**: Consecuencias de un incidente de seguridad

#### Fórmula del Riesgo
```
Riesgo = Amenaza × Vulnerabilidad × Impacto
```

### Metodologías de Análisis de Riesgo

#### 1. NIST SP 800-30
**Proceso de 9 pasos:**
1. Preparación del análisis
2. Identificación de amenazas
3. Identificación de vulnerabilidades
4. Determinación de probabilidad
5. Análisis de impacto
6. Determinación del riesgo
7. Recomendaciones de control
8. Documentación de resultados
9. Mantenimiento continuo

#### 2. ISO 27005
**Enfoque estructurado:**
- Establecimiento del contexto
- Evaluación de riesgos
- Tratamiento de riesgos
- Aceptación de riesgos
- Comunicación de riesgos
- Monitoreo y revisión

#### 3. OCTAVE (Operationally Critical Threat, Asset, and Vulnerability Evaluation)
**Características principales:**
- Enfoque dirigido por la organización
- Evaluación de riesgos de seguridad operacional
- Análisis de amenazas críticas
- Identificación de vulnerabilidades operacionales

### Proceso de Análisis de Riesgos

#### Paso 1: Identificación de Activos
```
Tipos de Activos:
├── Información y Datos
│   ├── Bases de datos
│   ├── Archivos de configuración
│   ├── Documentación del sistema
│   └── Información personal
├── Software
│   ├── Aplicaciones críticas
│   ├── Sistemas operativos
│   ├── Utilidades del sistema
│   └── Software de desarrollo
├── Hardware
│   ├── Servidores
│   ├── Dispositivos de red
│   ├── Estaciones de trabajo
│   └── Dispositivos móviles
└── Servicios
    ├── Servicios de comunicación
    ├── Servicios generales (electricidad, A/C)
    ├── Personal
    └── Ubicación física
```

#### Paso 2: Valoración de Activos
**Criterios de Valoración:**
- **Valor de Reemplazo**: Costo de reemplazar el activo
- **Valor de Productividad**: Impacto en la productividad organizacional
- **Valor de Responsabilidad**: Costos legales y regulatorios
- **Valor de Imagen**: Impacto en la reputación organizacional

#### Paso 3: Identificación de Amenazas
**Categorización de Amenazas:**
- Adversariales (ataques intencionados)
- Accidentales (errores humanos)
- Estructurales (fallas de equipos)
- Ambientales (desastres naturales)

#### Paso 4: Evaluación de Vulnerabilidades
**Métodos de Evaluación:**
- Escaneo automatizado de vulnerabilidades
- Pruebas de penetración
- Revisiones de código fuente
- Auditorías de configuración
- Evaluaciones de procesos

#### Paso 5: Cálculo del Riesgo
**Matriz de Riesgo:**

| Probabilidad | Muy Bajo | Bajo | Medio | Alto | Muy Alto |
|--------------|----------|------|-------|------|----------|
| Muy Alta     | Medio    | Alto | Alto  | Muy Alto | Muy Alto |
| Alta         | Bajo     | Medio| Alto  | Alto     | Muy Alto |
| Media        | Muy Bajo | Bajo | Medio | Alto     | Alto     |
| Baja         | Muy Bajo | Muy Bajo | Bajo | Medio | Alto |
| Muy Baja     | Muy Bajo | Muy Bajo | Muy Bajo | Bajo | Medio |

---

## Ataques Informáticos

### Clasificación de Ataques

#### Por su Objetivo
- **Ataques de Confidencialidad**: Acceso no autorizado a información
- **Ataques de Integridad**: Modificación no autorizada de datos
- **Ataques de Disponibilidad**: Denegación de servicio

#### Por su Método
- **Ataques Pasivos**: Observación sin modificación
- **Ataques Activos**: Modificación o interrupción de sistemas

### Tipos de Ataques Más Comunes

#### 1. Ataques de Malware
**Ransomware:**
- **WannaCry (2017)**: Afectó más de 300,000 computadoras en 150 países
- **Petya/NotPetya (2017)**: Causó daños por miles de millones de dólares
- **CryptoLocker (2013)**: Pionero en ransomware moderno

**Características del Ransomware:**
```
Proceso de Infección:
1. Vector de entrada (email, web, USB)
2. Ejecución del payload
3. Cifrado de archivos
4. Nota de rescate
5. Demanda de pago
```

#### 2. Ataques de Phishing
**Evolución del Phishing:**
- **Phishing Tradicional**: Emails masivos genéricos
- **Spear Phishing**: Ataques dirigidos a individuos específicos
- **Whaling**: Ataques dirigidos a ejecutivos de alto nivel
- **Vishing**: Phishing por voz/teléfono
- **Smishing**: Phishing por SMS

**Técnicas Comunes:**
- Suplantación de sitios web legítimos
- Uso de dominios similares (typosquatting)
- Ingeniería social sofisticada
- Archivos adjuntos maliciosos

#### 3. Ataques APT (Advanced Persistent Threats)
**Características de APT:**
- Ataques dirigidos y sofisticados
- Persistencia a largo plazo
- Uso de vulnerabilidades zero-day
- Técnicas de evasión avanzadas

**Fases de un Ataque APT:**
```
Ciclo de Vida APT:
1. Reconocimiento inicial
2. Compromiso inicial
3. Establecimiento de persistencia
4. Escalamiento de privilegios
5. Movimiento lateral
6. Mantenimiento del acceso
7. Exfiltración de datos
```

#### 4. Ataques DDoS Distribuidos
**Tipos de Ataques DDoS:**
- **Volumétricos**: Saturación de ancho de banda
- **De Protocolo**: Explotación de debilidades en protocolos
- **De Capa de Aplicación**: Ataques dirigidos a aplicaciones específicas

**Botnets Famosas:**
- **Mirai**: Comprometió dispositivos IoT
- **Conficker**: Una de las botnets más grandes
- **Zeus**: Enfocada en robo bancario

### Vectores de Ataque Modernos

#### 1. Ataques a IoT (Internet of Things)
**Vulnerabilidades Comunes:**
- Contraseñas predeterminadas débiles
- Falta de cifrado en comunicaciones
- Actualizaciones de firmware inexistentes
- Autenticación inadecuada

#### 2. Ataques a la Cadena de Suministro
**Ejemplos Notables:**
- **SolarWinds (2020)**: Compromiso de software de gestión de red
- **CCleaner (2017)**: Malware distribuido a través de actualizaciones
- **Target (2013)**: Compromiso a través de proveedores de HVAC

#### 3. Ataques de Ingeniería Social
**Técnicas Avanzadas:**
- **Pretexting**: Creación de escenarios falsos
- **Baiting**: Uso de curiosidad o codicia
- **Quid Pro Quo**: Ofrecimiento de servicios a cambio de información
- **Tailgating**: Acceso físico no autorizado

### Casos de Estudio Relevantes

#### Caso 1: Equifax (2017)
**Detalles del Incidente:**
- Afectó a 147 millones de personas
- Explotación de vulnerabilidad Apache Struts
- Exposición de datos personales sensibles
- Costo estimado: $4 mil millones

**Lecciones Aprendidas:**
- Importancia del patch management
- Monitoreo continuo de vulnerabilidades
- Respuesta rápida a incidentes
- Transparencia en comunicación

#### Caso 2: WannaCry (2017)
**Impacto Global:**
- 300,000+ computadoras afectadas
- Hospitales del NHS británico paralizados
- Sistemas de transporte interrumpidos
- Propagación a través de vulnerabilidad EternalBlue

**Factores Críticos:**
- Sistemas Windows sin actualizar
- Falta de segmentación de red
- Ausencia de backups adecuados
- Respuesta de emergencia inadecuada

## Objetivos de Aprendizaje
- [ ] Identificar los diferentes tipos de amenazas informáticas
- [ ] Comprender la importancia de las políticas de seguridad
- [ ] Realizar un análisis básico de riesgos
- [ ] Reconocer los principales tipos de ataques informáticos

## Recursos Adicionales
- Enlaces a documentos relevantes
- Videos explicativos
- Herramientas de análisis de riesgo

## Actividades
- Ejercicios prácticos
- Casos de estudio
- Evaluaciones
