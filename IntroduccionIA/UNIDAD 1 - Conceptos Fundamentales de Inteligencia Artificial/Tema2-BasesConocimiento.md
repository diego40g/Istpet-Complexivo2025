# Tema 2: Introducción a las Bases de Conocimiento

## ¿Qué es una base de conocimiento? {#que-es-base-conocimiento}

Una **base de conocimiento** es un repositorio estructurado que almacena información, hechos, reglas y procedimientos sobre un dominio específico, diseñado para ser utilizado por sistemas de inteligencia artificial para resolver problemas y tomar decisiones.

### Características principales:
- **Estructura organizada**: La información está clasificada y relacionada de manera lógica
- **Accesibilidad computacional**: Puede ser consultada y manipulada por programas
- **Dominio específico**: Se enfoca en áreas particulares del conocimiento
- **Actualizable**: Permite la incorporación de nuevo conocimiento
- **Inferencia**: Posibilita la derivación de nuevo conocimiento a partir del existente

### Diferencias con bases de datos tradicionales:
| Base de Datos | Base de Conocimiento |
|---------------|---------------------|
| Almacena datos | Almacena conocimiento |
| Estructura rígida | Estructura flexible |
| Consultas directas | Inferencia y razonamiento |
| Sin contexto semántico | Rica en semántica |

## Componentes de una base de conocimiento: hechos, reglas y suposiciones {#componentes-base-conocimiento}

### Hechos
**Definición**: Afirmaciones verdaderas sobre el mundo que representan conocimiento específico y concreto.

**Características**:
- Son declarativos
- Representan el estado actual del conocimiento
- Pueden ser verificables
- Forman la base empírica del sistema

**Ejemplos**:
```
- "El cielo es azul"
- "París es la capital de Francia"
- "El agua hierve a 100°C a nivel del mar"
- "Juan tiene 25 años"
```

### Reglas
**Definición**: Expresiones condicionales que establecen relaciones causa-efecto o implicaciones lógicas.

**Estructura típica**: `SI [condición] ENTONCES [conclusión]`

**Tipos de reglas**:
- **Reglas de producción**: Para generar nuevos hechos
- **Reglas de clasificación**: Para categorizar objetos
- **Reglas de diagnóstico**: Para identificar problemas
- **Reglas de procedimiento**: Para guiar acciones

**Ejemplos**:
```
- SI (temperatura > 37°C) ENTONCES (el paciente tiene fiebre)
- SI (es estudiante Y tiene beca) ENTONCES (descuento del 50%)
- SI (llueve) ENTONCES (llevar paraguas)
```

### Suposiciones (Asunciones)
**Definición**: Premisas que se asumen como verdaderas para el funcionamiento del sistema, pero que pueden no ser verificables completamente.

**Características**:
- Proporcionan contexto al conocimiento
- Simplifican el modelado del dominio
- Pueden ser revisables
- Afectan la validez de las conclusiones

**Ejemplos**:
```
- "Los sensores funcionan correctamente"
- "La información proporcionada por el usuario es veraz"
- "El comportamiento pasado predice el futuro"
- "Mundo cerrado: lo que no se conoce es falso"
```

## Diferencia entre dato, información y conocimiento {#diferencia-dato-informacion-conocimiento}

### Jerarquía del Conocimiento

#### Datos
- **Definición**: Símbolos o señales sin procesar, sin contexto ni significado
- **Características**: Objetivos, cuantificables, sin interpretación
- **Ejemplos**: 
  - Número: 25
  - Palabra: "lluvia"
  - Medición: 37.5

#### Información
- **Definición**: Datos procesados y organizados que tienen significado en un contexto específico
- **Características**: Contextualizada, interpretada, responde a preguntas básicas
- **Ejemplos**:
  - "La temperatura es de 25°C"
  - "Hoy llueve en Madrid"
  - "El paciente tiene 37.5°C de temperatura"

#### Conocimiento
- **Definición**: Información combinada con experiencia, contexto, interpretación y reflexión
- **Características**: Aplicable, predictivo, permite tomar decisiones
- **Tipos**:
  - **Explícito**: Puede ser codificado y transmitido
  - **Tácito**: Difícil de formalizar, basado en experiencia
- **Ejemplos**:
  - "Una temperatura de 25°C es ideal para actividades al aire libre"
  - "Si llueve, es probable que haya tráfico intenso"
  - "Una temperatura de 37.5°C indica fiebre leve que requiere monitoreo"

### Transformación en Sistemas de IA

```
DATOS → [Procesamiento] → INFORMACIÓN → [Interpretación] → CONOCIMIENTO
```

**Ejemplo completo**:
- **Dato**: "150, 90"
- **Información**: "Presión arterial: 150/90 mmHg"
- **Conocimiento**: "Presión arterial alta que requiere tratamiento y seguimiento médico"

## La importancia de las bases de conocimiento en los sistemas expertos {#importancia-bases-conocimiento-sistemas-expertos}

### ¿Qué son los Sistemas Expertos?
Programas de computadora que emulan la capacidad de toma de decisiones de un experto humano en un dominio específico.

### Rol de las Bases de Conocimiento

#### Núcleo del Sistema
- **Repositorio central**: Almacena toda la experiencia del dominio
- **Separación de conocimiento**: Independiente de la lógica de inferencia
- **Mantenibilidad**: Facilita actualizaciones y correcciones

#### Ventajas en Sistemas Expertos

##### Consistencia
- Eliminación de contradicciones en la toma de decisiones
- Aplicación uniforme de criterios
- Reducción de errores humanos

##### Disponibilidad
- Acceso 24/7 al conocimiento experto
- No se ve afectada por factores humanos (cansancio, estrés)
- Escalabilidad para múltiples usuarios simultáneos

##### Preservación del Conocimiento
- Captura de experiencia de expertos
- Prevención de pérdida de conocimiento (jubilaciones, renuncias)
- Documentación formal del saber especializado

##### Explicabilidad
- Capacidad de justificar decisiones
- Trazabilidad del razonamiento
- Facilita la validación y el aprendizaje

### Ejemplos de Aplicación

#### MYCIN (Medicina)
- **Dominio**: Diagnóstico de infecciones bacterianas
- **Base de conocimiento**: 600+ reglas médicas
- **Rendimiento**: Comparable a especialistas humanos

#### XCON/R1 (Ingeniería)
- **Dominio**: Configuración de sistemas informáticos
- **Base de conocimiento**: Reglas de compatibilidad de componentes
- **Impacto**: Automatización de procesos de configuración

#### PROSPECTOR (Geología)
- **Dominio**: Exploración minera
- **Base de conocimiento**: Conocimiento geológico sobre depósitos minerales
- **Resultado**: Descubrimiento de nuevos yacimientos

### Desafíos en el Desarrollo

#### Adquisición del Conocimiento
- **Problema**: Dificultad para extraer conocimiento de expertos humanos
- **Técnicas**: Entrevistas, análisis de casos, observación

#### Representación Adecuada
- **Problema**: Formalizar conocimiento informal y tácito
- **Soluciones**: Múltiples formalismos de representación

#### Validación y Verificación
- **Problema**: Garantizar corrección y completitud
- **Métodos**: Pruebas exhaustivas, revisión por pares

---

*Este archivo forma parte del curso de Introducción a la Inteligencia Artificial - UNIDAD 1*
