# Tema 4: Representación del Conocimiento

## Lógica formal (proposicional y de primer orden) como herramienta de representación {#logica-formal}

La **lógica formal** proporciona un framework matemático riguroso para representar y razonar con conocimiento. Ofrece sintaxis precisa, semántica bien definida y métodos de inferencia sistemáticos.

### Lógica Proposicional

#### Características Básicas
- **Unidades básicas**: Proposiciones (verdadero/falso)
- **Conectivos lógicos**: ∧ (y), ∨ (o), ¬ (no), → (implica), ↔ (si y solo si)
- **Simplicidad**: Fácil de entender y computar
- **Limitación**: No puede expresar relaciones entre objetos

#### Sintaxis
```
Proposiciones atómicas: P, Q, R, ...
Fórmulas complejas:
- ¬P (negación)
- P ∧ Q (conjunción)
- P ∨ Q (disyunción)
- P → Q (implicación)
- P ↔ Q (equivalencia)
```

#### Ejemplo Práctico
```
P: "Llueve"
Q: "Uso paraguas"
R: "Me mojo"

Reglas:
- P → Q (Si llueve, uso paraguas)
- ¬Q → R (Si no uso paraguas, me mojo)
- P ∧ ¬Q → R (Si llueve y no uso paraguas, me mojo)
```

#### Ventajas y Limitaciones
| Ventajas | Limitaciones |
|----------|--------------|
| Sintaxis simple | No expresa relaciones |
| Decidible | No maneja cuantificación |
| Eficiente computacionalmente | Limitada expresividad |
| Base sólida para otros formalismos | No representa objetos individuales |

### Lógica de Primer Orden (Lógica de Predicados)

#### Características Avanzadas
- **Objetos**: Entidades individuales del dominio
- **Predicados**: Relaciones y propiedades
- **Cuantificadores**: ∀ (para todo), ∃ (existe)
- **Funciones**: Mapeos entre objetos
- **Mayor expresividad**: Puede representar estructuras complejas

#### Sintaxis
```
Términos:
- Constantes: juan, madrid, 25
- Variables: x, y, z
- Funciones: padre(x), edad(juan)

Fórmulas atómicas:
- Predicados: Médico(juan), Mayor(x,y), Vive(x,madrid)

Conectivos lógicos: ∧, ∨, ¬, →, ↔

Cuantificadores:
- ∀x Médico(x) → Profesional(x)
- ∃x Médico(x) ∧ Joven(x)
```

#### Ejemplo Médico Completo
```
Constantes: juan, maria, hospital_central, cardiologia

Predicados:
- Médico(x): x es médico
- Especialista(x,y): x es especialista en y
- Trabaja(x,y): x trabaja en y
- Trata(x,y): x trata a y

Hechos:
- Médico(juan)
- Médico(maria)
- Especialista(juan, cardiologia)
- Trabaja(juan, hospital_central)

Reglas:
- ∀x (Médico(x) → Profesional(x))
- ∀x,y (Médico(x) ∧ Especialista(x,y) → PuedeTratar(x,y))
- ∀x,y,z (Médico(x) ∧ Trabaja(x,y) ∧ Paciente(z) → PuedeTratar(x,z))
```

#### Inferencia en Lógica de Primer Orden
- **Unificación**: Proceso de hacer coincidir términos
- **Resolución**: Método de prueba por refutación
- **Modus ponens generalizado**: Aplicación de reglas
- **Algoritmos**: SLD-resolution, tableau methods

### Comparación de Lógicas

| Aspecto | Lógica Proposicional | Lógica de Primer Orden |
|---------|---------------------|----------------------|
| Expresividad | Básica | Alta |
| Complejidad | Decidible (NP-completo) | Semi-decidible |
| Objetos | No soporta | Sí |
| Relaciones | Limitadas | Completas |
| Cuantificación | No | Sí |
| Aplicaciones | Sistemas simples | Sistemas complejos |

## Redes semánticas: estructuras gráficas para organizar conceptos {#redes-semanticas}

Las **redes semánticas** son representaciones gráficas del conocimiento donde los nodos representan conceptos y los arcos representan relaciones entre ellos. Proporcionan una forma intuitiva y visual de estructurar el conocimiento.

### Características Fundamentales

#### Componentes Básicos
- **Nodos**: Representan conceptos, objetos o entidades
- **Arcos**: Representan relaciones entre nodos
- **Etiquetas**: Especifican el tipo de relación
- **Jerarquías**: Estructuras de generalización/especialización

#### Tipos de Relaciones
- **ISA (es-un)**: Relaciones de jerarquía taxonómica
- **HAS (tiene)**: Relaciones de composición o propiedad
- **PART-OF**: Relaciones de componencia
- **INSTANCE-OF**: Relaciones de instanciación
- **CAUSE**: Relaciones causales
- **LOCATED-AT**: Relaciones espaciales

### Ejemplo de Red Semántica

```
                    Animal
                      |
                 ISA  |  ISA
                     / \
               Mamífero  Ave
                 |        |
            ISA  |   ISA  |  ISA
                / \      / \
            Perro Gato Águila Canario
              |    |     |      |
        INSTANCE-OF |     |      |
              |    |     |      |
            Firulais Michi Libertad Piolín

Propiedades:
Animal HAS respiración
Mamífero HAS pelo
Ave HAS plumas
Perro HAS ladrido
```

### Herencia en Redes Semánticas

#### Principio de Herencia
- Los nodos heredan propiedades de sus ancestros
- Permite representación económica del conocimiento
- Soporta excepciones y valores por defecto

#### Ejemplo de Herencia
```
Ave ISA Animal
Ave HAS plumas
Ave HAS vuela

Pingüino ISA Ave
Pingüino HAS no_vuela  // Excepción

Conclusiones:
- Pingüino HAS plumas (heredado de Ave)
- Pingüino HAS no_vuela (específico, sobrescribe default)
```

### Ventajas y Limitaciones

#### Ventajas
- **Intuitividad**: Fácil de entender y visualizar
- **Herencia**: Representación eficiente mediante jerarquías
- **Flexibilidad**: Fácil modificación y extensión
- **Navegabilidad**: Exploración natural del conocimiento

#### Limitaciones
- **Ambigüedad**: Falta de semántica formal precisa
- **Herencia múltiple**: Problemas con conflictos
- **Expresividad limitada**: No maneja lógica compleja
- **Escalabilidad**: Dificultad con redes muy grandes

### Variantes y Extensiones

#### Redes Semánticas Tipadas
- Clasificación de nodos y arcos por tipos
- Mayor precisión semántica
- Mejor control de consistencia

#### Redes Conceptuales
- Incorporan contexto y situaciones
- Manejo de conocimiento temporal
- Representación de eventos y procesos

## Marcos (frames) y guiones (scripts) para representar situaciones estereotípicas {#marcos-guiones}

Los **marcos** y **guiones** son estructuras de representación que capturan conocimiento sobre situaciones típicas, objetos estereotípicos y secuencias de eventos comunes.

### Marcos (Frames)

#### Concepto Fundamental
Desarrollado por Marvin Minsky, un **marco** es una estructura de datos que representa una situación estereotípica, conteniendo información sobre qué esperar y cómo usar esa información.

#### Estructura de un Marco
```
MARCO: Habitación
SLOTS:
  - Paredes: [default: 4, range: 3-8]
  - Techo: [default: presente, type: obligatorio]
  - Piso: [default: presente, type: obligatorio]
  - Puertas: [default: 1, range: 1-3]
  - Ventanas: [default: 1, range: 0-5]
  - Función: [type: livingroom | bedroom | kitchen | ...]
  - Área: [type: numeric, units: m²]

PROCEDIMIENTOS:
  - Si-necesario: calcular_área()
  - Si-añadido: validar_estructura()
  - Si-removido: verificar_integridad()
```

#### Tipos de Slots
- **Slots de valor**: Contienen información específica
- **Slots de default**: Valores por defecto
- **Slots de rango**: Restricciones de valores posibles
- **Slots procedimentales**: Código ejecutable

#### Ejemplo: Marco de "Consulta Médica"
```
MARCO: ConsultaMédica
SLOTS:
  - Paciente: [type: persona, required: true]
  - Médico: [type: médico, required: true]
  - Fecha: [type: fecha, default: hoy]
  - Síntomas: [type: lista, required: true]
  - Diagnóstico: [type: string]
  - Tratamiento: [type: lista]
  - Duración: [default: 30_minutos, range: 15-120]

PROCEDIMIENTOS:
  - Si-necesario-diagnóstico: analizar_síntomas()
  - Si-añadido-tratamiento: verificar_contraindicaciones()
```

#### Herencia en Marcos
```
MARCO: Vehículo
SLOTS:
  - Motor: [required: true]
  - Ruedas: [default: 4]
  - Combustible: [type: gasolina | diesel | eléctrico]

MARCO: Automóvil ISA Vehículo
SLOTS:
  - Ruedas: [fixed: 4]  // Sobrescribe el default
  - Asientos: [range: 2-8]
  - AireAcondicionado: [default: true]

MARCO: Motocicleta ISA Vehículo
SLOTS:
  - Ruedas: [fixed: 2]  // Sobrescribe el default
  - Casco: [required: true]
```

### Guiones (Scripts)

#### Concepto de Script
Un **guión** es una estructura que representa una secuencia estereotípica de eventos en una situación particular. Desarrollado por Roger Schank para modelar comprensión del lenguaje y situaciones.

#### Estructura de un Guión
```
GUIÓN: Restaurante
PARTICIPANTES:
  - Cliente (C)
  - Camarero (W)
  - Cocinero (Ch)
  - Cajero (Ca)

OBJETOS:
  - Mesa, menú, comida, cuenta, dinero

CONDICIONES DE ENTRADA:
  - Cliente tiene hambre
  - Cliente tiene dinero
  - Restaurante está abierto

ESCENAS:
  1. Entrada:
     - C entra al restaurante
     - W saluda a C
     - W guía a C a una mesa

  2. Pedido:
     - W entrega menú a C
     - C lee menú
     - C hace pedido a W
     - W anota pedido

  3. Preparación:
     - W entrega pedido a Ch
     - Ch prepara comida
     - W recoge comida preparada

  4. Servicio:
     - W sirve comida a C
     - C come

  5. Pago:
     - W presenta cuenta a C
     - C paga a Ca o W
     - C deja propina (opcional)

CONDICIONES DE SALIDA:
  - Cliente ya no tiene hambre
  - Cliente ha pagado
  - Mesa está libre
```

#### Variaciones y Excepciones
```
TRACK: Restaurante_FastFood (variación del guión restaurante)
DIFERENCIAS:
  - No hay camarero
  - Cliente ordena en mostrador
  - Cliente recoge su propia comida
  - Pago antes de recibir comida
```

### Aplicaciones Prácticas

#### En Sistemas de Comprensión
- **Procesamiento de lenguaje natural**: Interpretación de narrativas
- **Sistemas de diálogo**: Manejo de conversaciones
- **Robótica**: Planificación de acciones en contextos conocidos

#### En Sistemas Expertos
- **Diagnóstico médico**: Marcos para enfermedades típicas
- **Configuración**: Marcos para componentes estándar
- **Planificación**: Guiones para procedimientos estándar

### Ventajas y Limitaciones

#### Ventajas de Marcos
- **Organización**: Agrupación natural del conocimiento relacionado
- **Herencia**: Reutilización eficiente de conocimiento
- **Defaults**: Manejo de información incompleta
- **Procedimientos**: Integración de conocimiento y procesamiento

#### Ventajas de Guiones
- **Predictividad**: Expectativas sobre secuencias de eventos
- **Comprensión**: Interpretación de situaciones parciales
- **Planificación**: Guía para acciones futuras

#### Limitaciones
- **Rigidez**: Dificultad con situaciones no estereotípicas
- **Actualización**: Mantenimiento de muchas estructuras
- **Escalabilidad**: Complejidad con dominios grandes

## La ontología en la representación del conocimiento {#ontologia-representacion}

Una **ontología** en inteligencia artificial es una especificación formal y explícita de una conceptualización compartida de un dominio. Proporciona un vocabulario común y una estructura para representar conocimiento de manera que pueda ser compartida y reutilizada.

### Definición y Características

#### Componentes de una Ontología
- **Conceptos (Clases)**: Categorías fundamentales del dominio
- **Relaciones**: Conexiones entre conceptos
- **Propiedades**: Características de los conceptos
- **Instancias**: Objetos específicos del dominio
- **Axiomas**: Restricciones y reglas del dominio

#### Características Clave
- **Formalidad**: Especificación matemáticamente precisa
- **Explicititud**: Definiciones claras y no ambiguas
- **Compartida**: Consenso entre comunidades
- **Conceptualización**: Modelo abstracto del dominio

### Tipos de Ontologías

#### Por Nivel de Generalidad
- **Ontologías de alto nivel**: Conceptos muy generales (tiempo, espacio, evento)
- **Ontologías de dominio**: Específicas a un área (medicina, ingeniería)
- **Ontologías de tarea**: Para actividades específicas (diagnóstico, planificación)
- **Ontologías de aplicación**: Para aplicaciones particulares

#### Por Propósito
- **Ontologías descriptivas**: Describen un dominio existente
- **Ontologías normativas**: Definen cómo debería ser un dominio
- **Ontologías de referencia**: Estándares para interoperabilidad

### Ejemplo de Ontología Médica

#### Estructura Básica
```
ONTOLOGÍA: MedicinaGeneral

CLASES PRINCIPALES:
- Entidad
  ├── PersonaViva
  │   ├── Paciente
  │   └── PersonalMédico
  │       ├── Médico
  │       ├── Enfermero
  │       └── Especialista
  ├── Enfermedad
  │   ├── EnfermedadInfecciosa
  │   ├── EnfermedadCrónica
  │   └── EnfermedadAguda
  ├── Síntoma
  ├── Tratamiento
  │   ├── Medicamento
  │   ├── Cirugía
  │   └── Terapia
  └── Diagnóstico

RELACIONES:
- tiene_síntoma(Paciente, Síntoma)
- diagnostica(Médico, Enfermedad)
- trata_con(Médico, Tratamiento)
- causa(Enfermedad, Síntoma)
- alivia(Tratamiento, Síntoma)
- especializado_en(Especialista, ÁreaMédica)

PROPIEDADES:
- Paciente:
  * edad: entero
  * sexo: {masculino, femenino}
  * historial_médico: lista
- Medicamento:
  * dosis: cadena
  * frecuencia: cadena
  * contraindicaciones: lista

AXIOMAS:
- ∀x (Paciente(x) → PersonaViva(x))
- ∀x,y (diagnostica(x,y) → Médico(x) ∧ Enfermedad(y))
- ∀x,y (causa(x,y) → Enfermedad(x) ∧ Síntoma(y))
```

### Lenguajes de Ontologías

#### OWL (Web Ontology Language)
- **Estándar W3C**: Para la web semántica
- **Basado en lógica descriptiva**: Fundamentos matemáticos sólidos
- **Tres sublanguages**: OWL Lite, OWL DL, OWL Full
- **Herramientas**: Protégé, TopBraid, etc.

#### RDF/RDFS (Resource Description Framework)
- **Modelo de datos**: Para metadatos web
- **Triples**: Sujeto-Predicado-Objeto
- **Esquema**: RDFS para definir vocabularios

#### Ejemplo en OWL
```xml
<owl:Class rdf:ID="Médico">
  <rdfs:subClassOf rdf:resource="#PersonalMédico"/>
</owl:Class>

<owl:ObjectProperty rdf:ID="trata">
  <rdfs:domain rdf:resource="#Médico"/>
  <rdfs:range rdf:resource="#Paciente"/>
</owl:ObjectProperty>

<owl:DatatypeProperty rdf:ID="edad">
  <rdfs:domain rdf:resource="#Paciente"/>
  <rdfs:range rdf:resource="&xsd;int"/>
</owl:DatatypeProperty>
```

### Desarrollo de Ontologías

#### Metodologías
- **METHONTOLOGY**: Metodología completa para desarrollo
- **On-To-Knowledge**: Para aplicaciones basadas en conocimiento
- **SENSUS**: Desarrollo de ontologías grandes
- **Enterprise Ontology**: Para dominios empresariales

#### Proceso General
1. **Análisis de dominio**: Identificación de conceptos clave
2. **Conceptualización**: Modelo conceptual informal
3. **Formalización**: Especificación formal en lenguaje de ontologías
4. **Implementación**: Codificación en herramientas específicas
5. **Evaluación**: Validación y verificación
6. **Mantenimiento**: Evolución y actualización

### Aplicaciones de Ontologías

#### Web Semántica
- **Anotación semántica**: Enriquecimiento de contenido web
- **Búsqueda inteligente**: Búsquedas basadas en significado
- **Integración de datos**: Interoperabilidad entre sistemas

#### Sistemas de Información
- **Integración de bases de datos**: Mediación entre esquemas
- **Gestión de conocimiento**: Organización de información empresarial
- **Sistemas expertos**: Base conceptual para inferencia

#### Biomedicina
- **Gene Ontology**: Anotación de funciones genéticas
- **SNOMED CT**: Terminología médica sistemática
- **Drug Ontology**: Clasificación de medicamentos

### Ventajas y Desafíos

#### Ventajas
- **Interoperabilidad**: Comunicación entre sistemas diversos
- **Reutilización**: Aprovechamiento de conocimiento existente
- **Consistencia**: Definiciones unificadas y precisas
- **Reasoning**: Inferencia automática de conocimiento

#### Desafíos
- **Complejidad**: Desarrollo y mantenimiento costoso
- **Consenso**: Dificultad para lograr acuerdos
- **Escalabilidad**: Performance con ontologías grandes
- **Evolución**: Gestión de cambios en el tiempo

---

*Este archivo forma parte del curso de Introducción a la Inteligencia Artificial - UNIDAD 2*
