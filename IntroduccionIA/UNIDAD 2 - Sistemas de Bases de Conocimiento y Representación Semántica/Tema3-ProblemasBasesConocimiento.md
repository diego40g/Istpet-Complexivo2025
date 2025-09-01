# Tema 3: Problemas en las Bases de Conocimiento

## El desafío de la adquisición del conocimiento {#desafio-adquisicion-conocimiento}

La **adquisición del conocimiento** es el proceso de extraer, estructurar y formalizar el conocimiento de expertos humanos o fuentes de información para incorporarlo en sistemas de IA. Este proceso presenta múltiples desafíos que han sido reconocidos como uno de los principales cuellos de botella en el desarrollo de sistemas basados en conocimiento.

### Desafíos Principales

#### El Cuello de Botella del Conocimiento
- **Definición**: La dificultad para transferir conocimiento de expertos humanos a sistemas computacionales
- **Causas**:
  - Conocimiento tácito difícil de verbalizar
  - Falta de introspección de los expertos
  - Complejidad del dominio
  - Resistencia al cambio

#### Problemas de Comunicación
- **Brecha semántica**: Diferencias entre el lenguaje natural y la representación formal
- **Ambigüedad lingüística**: Múltiples interpretaciones de conceptos
- **Conocimiento implícito**: Suposiciones no expresadas explícitamente
- **Contexto cultural**: Interpretaciones dependientes del contexto social

#### Limitaciones de los Expertos Humanos
- **Conocimiento inconsciente**: Muchas decisiones se toman intuitivamente
- **Sesgo cognitivo**: Influencia de experiencias personales
- **Sobrecarga cognitiva**: Dificultad para expresar todo el conocimiento relevante
- **Inconsistencia temporal**: Cambios en criterios a lo largo del tiempo

### Técnicas de Adquisición

#### Métodos Directos
- **Entrevistas estructuradas**:
  - Ventajas: Control del proceso, profundización en temas
  - Desventajas: Tiempo intensivo, posible sesgo del entrevistador

- **Cuestionarios y encuestas**:
  - Ventajas: Escalabilidad, estandarización
  - Desventajas: Respuestas limitadas, falta de flexibilidad

- **Análisis de protocolo**:
  - Técnica: "Pensar en voz alta" mientras se resuelven problemas
  - Ventajas: Captura el proceso de razonamiento
  - Desventajas: Artificial, puede alterar el proceso natural

#### Métodos Indirectos
- **Análisis de casos**:
  - Estudio de decisiones pasadas
  - Identificación de patrones en el comportamiento experto
  - Extracción de reglas implícitas

- **Observación directa**:
  - Análisis del experto en su entorno natural
  - Registro de comportamientos y decisiones
  - Identificación de factores contextuales

#### Métodos Automatizados
- **Minería de datos**:
  - Extracción de patrones de grandes volúmenes de datos
  - Identificación automática de reglas
  - Validación estadística de conocimiento

- **Aprendizaje automático**:
  - Sistemas que aprenden de ejemplos
  - Generación automática de reglas
  - Refinamiento continuo del conocimiento

## El problema de la representación del conocimiento {#problema-representacion-conocimiento}

La **representación del conocimiento** se refiere a cómo se estructura y codifica el conocimiento para que pueda ser utilizado efectivamente por sistemas computacionales. Este problema implica encontrar formalismos que sean tanto comprensibles para humanos como procesables por máquinas.

### Desafíos Fundamentales

#### Expresividad vs. Tratabilidad
- **Dilema central**: Sistemas más expresivos son computacionalmente más complejos
- **Trade-off**: Balance entre capacidad de representación y eficiencia computacional
- **Ejemplos**:
  - Lógica proposicional: Simple pero limitada
  - Lógica de primer orden: Expresiva pero indecidible
  - Lógicas no monótonas: Poderosas pero complejas

#### Incompletitud del Conocimiento
- **Problema del mundo abierto**: No se puede asumir que todo el conocimiento está disponible
- **Razonamiento con incertidumbre**: Manejar información incompleta o incierta
- **Valores por defecto**: Suposiciones que pueden ser revocadas

#### Representación de Diferentes Tipos de Conocimiento

##### Conocimiento Declarativo
- **Características**: Qué es cierto en el mundo
- **Representación**: Hechos, proposiciones, reglas lógicas
- **Ejemplo**: "Todos los pájaros vuelan"

##### Conocimiento Procedural
- **Características**: Cómo hacer algo
- **Representación**: Algoritmos, procedimientos, reglas de acción
- **Ejemplo**: "Para diagnosticar, primero revisar síntomas principales"

##### Conocimiento Heurístico
- **Características**: Reglas empíricas basadas en experiencia
- **Representación**: Reglas con grados de confianza
- **Ejemplo**: "Si el paciente es joven, es menos probable que tenga problemas cardíacos"

### Formalismos de Representación

#### Lógicas Formales
- **Lógica proposicional**
- **Lógica de predicados**
- **Lógicas modales**
- **Lógicas temporales**

#### Estructuras Jerárquicas
- **Redes semánticas**
- **Marcos (frames)**
- **Ontologías**

#### Representaciones Procedurales
- **Reglas de producción**
- **Redes de Petri**
- **Máquinas de estados**

## Inconsistencias y redundancias en el conocimiento {#inconsistencias-redundancias}

Las bases de conocimiento están sujetas a problemas de **inconsistencia** (información contradictoria) y **redundancia** (información repetida), que pueden afectar significativamente el rendimiento y la confiabilidad de los sistemas.

### Inconsistencias

#### Tipos de Inconsistencias

##### Inconsistencias Lógicas
- **Definición**: Contradicciones directas en el conocimiento
- **Ejemplos**:
  ```
  Hecho1: "Juan es médico"
  Hecho2: "Juan no es médico"
  ```

##### Inconsistencias Semánticas
- **Definición**: Contradicciones en el significado o interpretación
- **Ejemplos**:
  ```
  Regla1: "Si temperatura > 38°C entonces fiebre alta"
  Regla2: "Si temperatura > 37.5°C entonces fiebre alta"
  ```

##### Inconsistencias Temporales
- **Definición**: Información que se contradice en diferentes momentos
- **Ejemplos**: Cambios en políticas o procedimientos no actualizados

#### Causas de Inconsistencias
- **Múltiples fuentes de conocimiento**
- **Evolución temporal del dominio**
- **Errores en la adquisición**
- **Diferentes perspectivas de expertos**
- **Actualizaciones parciales**

#### Detección de Inconsistencias
- **Verificación lógica**: Uso de theorem provers
- **Análisis semántico**: Comparación de significados
- **Validación cruzada**: Confrontación con múltiples expertos
- **Pruebas de casos**: Verificación con escenarios conocidos

### Redundancias

#### Tipos de Redundancias

##### Redundancia Sintáctica
- **Definición**: Misma información expresada de formas diferentes
- **Ejemplos**:
  ```
  "Juan es doctor" / "Juan es médico"
  "Temperatura alta" / "Fiebre"
  ```

##### Redundancia Semántica
- **Definición**: Información que se puede derivar de otra información existente
- **Ejemplos**:
  ```
  Regla: "Si es mamífero entonces tiene sangre caliente"
  Hecho redundante: "Los perros tienen sangre caliente"
  ```

##### Redundancia Procedimental
- **Definición**: Múltiples procedimientos que logran el mismo resultado
- **Impacto**: Ineficiencia computacional

#### Efectos de las Redundancias
- **Positive**: Mayor robustez, múltiples caminos de inferencia
- **Negativo**: Ineficiencia, mayor complejidad de mantenimiento

### Estrategias de Resolución

#### Resolución de Inconsistencias
- **Priorización**: Asignar pesos o prioridades a fuentes de conocimiento
- **Versionado**: Mantener historial de cambios
- **Consenso**: Buscar acuerdo entre múltiples expertos
- **Lógicas no monótonas**: Permitir revisión de creencias

#### Manejo de Redundancias
- **Normalización**: Estandarización de representaciones
- **Factorización**: Eliminación de duplicaciones
- **Optimización**: Mejora de eficiencia manteniendo funcionalidad

## Actualización y mantenimiento de las bases de conocimiento {#actualizacion-mantenimiento}

El **mantenimiento** de bases de conocimiento es un proceso continuo que asegura que el conocimiento permanezca actualizado, preciso y relevante a lo largo del tiempo.

### Desafíos del Mantenimiento

#### Evolución del Dominio
- **Cambios en el conocimiento**: Nuevos descubrimientos científicos
- **Cambios en procedimientos**: Actualización de mejores prácticas
- **Cambios regulatorios**: Nuevas leyes y regulaciones
- **Cambios tecnológicos**: Nuevas herramientas y métodos

#### Escalabilidad del Mantenimiento
- **Volumen creciente**: Más conocimiento requiere más esfuerzo de mantenimiento
- **Complejidad de dependencias**: Cambios que afectan múltiples componentes
- **Recursos limitados**: Restricciones de tiempo y personal experto

### Estrategias de Actualización

#### Actualización Incremental
- **Ventajas**: Cambios graduales, menor riesgo
- **Proceso**:
  1. Identificación de cambios necesarios
  2. Evaluación de impacto
  3. Implementación controlada
  4. Validación de cambios

#### Reestructuración Periódica
- **Cuándo aplicar**: Cuando los cambios incrementales son insuficientes
- **Proceso**:
  1. Revisión completa de la base de conocimiento
  2. Identificación de obsolescencias
  3. Reorganización de estructura
  4. Validación integral

### Técnicas de Mantenimiento

#### Validación Continua
- **Pruebas automatizadas**: Verificación regular de consistencia
- **Benchmarking**: Comparación con estándares conocidos
- **Feedback de usuarios**: Reporte de errores o mejoras

#### Control de Versiones
- **Historial de cambios**: Registro de todas las modificaciones
- **Rollback**: Capacidad de revertir cambios problemáticos
- **Branching**: Desarrollo paralelo de diferentes versiones

#### Métricas de Calidad
- **Completitud**: Cobertura del dominio
- **Consistencia**: Ausencia de contradicciones
- **Precisión**: Corrección de la información
- **Actualidad**: Vigencia temporal del conocimiento

### Herramientas y Metodologías

#### Sistemas de Gestión de Conocimiento
- **Características**: Interfaces para edición, validación y versionado
- **Funcionalidades**: Control de acceso, workflow de aprobación

#### Metodologías Ágiles
- **Desarrollo iterativo**: Mejoras continuas en ciclos cortos
- **Colaboración**: Participación activa de expertos del dominio
- **Adaptabilidad**: Respuesta rápida a cambios

#### Automatización
- **Extracción automática**: Actualización desde fuentes de datos
- **Validación automática**: Detección de inconsistencias
- **Alertas**: Notificación de necesidades de actualización

---

*Este archivo forma parte del curso de Introducción a la Inteligencia Artificial - UNIDAD 2*
