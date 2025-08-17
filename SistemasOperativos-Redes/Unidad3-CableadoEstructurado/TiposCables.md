# Tipos de cables de red

## 1. Medios de comunicación físicos: La base de las redes cableadas

### Importancia de los medios físicos:
Los medios físicos constituyen la infraestructura fundamental sobre la cual se construyen todas las redes de datos modernas. Sin una base sólida de medios de transmisión, ninguna red puede funcionar de manera confiable.

### Evolución histórica:
- **1960s**: Cable coaxial para redes mainframe
- **1970s**: Primeros cables de par trenzado para telefonía
- **1980s**: Adopción en redes de datos
- **1990s**: Introducción masiva de fibra óptica
- **2000s**: Estandarización y mejora continua

### Factores críticos en la selección:

#### Performance:
- **Ancho de banda**: Capacidad de transmisión de datos
- **Atenuación**: Pérdida de señal con la distancia
- **Distorsión**: Degradación de la forma de la señal
- **Ruido**: Interferencias que afectan la transmisión

#### Características ambientales:
- **Temperatura**: Rango de operación
- **Humedad**: Resistencia a la corrosión
- **Flexibilidad**: Facilidad de instalación
- **Durabilidad**: Vida útil esperada

#### Consideraciones económicas:
- **Costo inicial**: Inversión en materiales
- **Costo de instalación**: Mano de obra especializada
- **Mantenimiento**: Costos operativos
- **Escalabilidad**: Capacidad de expansión futura

## 2. Cable de par trenzado (UTP): Su estructura, funcionamiento y por qué es el más común

### Estructura física:

#### Composición básica:
- **Conductores**: Cobre sólido o multifilamento
- **Aislamiento**: Polietileno o materiales similares
- **Trenzado**: Pares de cables enrollados entre sí
- **Cubierta exterior**: Protección mecánica y ambiental

#### Geometría del trenzado:
```
Par 1: Blanco-Azul + Azul      (3,25 vueltas/pulgada)
Par 2: Blanco-Naranja + Naranja (3,25 vueltas/pulgada)
Par 3: Blanco-Verde + Verde     (3,25 vueltas/pulgada)
Par 4: Blanco-Café + Café      (3,25 vueltas/pulgada)
```

### Principio de funcionamiento:

#### Cancelación de ruido:
El trenzado de los cables crea un efecto de cancelación electromagnética:
- **Interferencia externa**: Afecta ambos conductores igualmente
- **Diferencial**: El receptor detecta la diferencia entre conductores
- **Cancelación**: La interferencia común se cancela

#### Impedancia característica:
- **100 ohmios**: Estándar para cables UTP Cat 5e y superiores
- **Matching**: Equipos diseñados para esta impedancia
- **Reflexiones**: Minimizadas con impedancia constante

### Ventajas del UTP:

#### Económicas:
- **Bajo costo**: Material más económico
- **Instalación simple**: No requiere herramientas especiales
- **Conectores estándar**: RJ-45 universalmente disponible
- **Mantenimiento fácil**: Diagnóstico y reparación simple

#### Técnicas:
- **Flexibilidad**: Fácil instalación en espacios reducidos
- **Compatibilidad**: Estándar internacional
- **Escalabilidad**: Soporta múltiples velocidades
- **Disponibilidad**: Ampliamente disponible

#### Operacionales:
- **Diagnóstico**: Herramientas de prueba accesibles
- **Reparación**: Fácil reemplazo de segmentos
- **Estandarización**: Procedimientos bien establecidos

### Desventajas:
- **Susceptibilidad a EMI**: Sin blindaje natural
- **Distancia limitada**: 100 metros máximo
- **Ancho de banda limitado**: Comparado con fibra
- **Crosstalk**: Interferencia entre pares

## 3. Cable de pares apantallados (STP/FTP): La protección extra contra interferencias

### Tipos de blindaje:

#### STP (Shielded Twisted Pair):
- **Blindaje individual**: Cada par tiene su propio blindaje
- **Blindaje general**: Pantalla sobre todos los pares
- **Conexión a tierra**: Crítica para efectividad
- **Aplicaciones**: Entornos industriales severos

#### FTP (Foiled Twisted Pair):
- **Pantalla de aluminio**: Una sola lámina sobre todos los pares
- **Menor costo**: Que STP completo
- **Protección moderada**: Contra interferencias comunes
- **Uso típico**: Oficinas con equipos electrónicos sensibles

#### S/FTP (Screened Foiled Twisted Pair):
- **Doble protección**: Pantalla individual y general
- **Máxima protección**: Contra interferencias
- **Costo elevado**: Mayor que UTP y FTP
- **Aplicaciones críticas**: Centros de datos, hospitales

### Efectividad del blindaje:

#### Frecuencias bajas (< 1 MHz):
- **Blindaje trenzado**: Muy efectivo
- **Pantalla metálica**: Moderadamente efectivo
- **Aplicaciones**: Señales de control industrial

#### Frecuencias altas (> 10 MHz):
- **Pantalla metálica**: Muy efectivo
- **Combinación**: STP + FTP óptimo
- **Aplicaciones**: Redes de alta velocidad

### Consideraciones de instalación:

#### Conexión a tierra:
- **Crítica**: Para efectividad del blindaje
- **Ambos extremos**: Conexión requerida
- **Loops de tierra**: Evitar diferencias de potencial
- **Inspección**: Verificación periódica

#### Conectores especiales:
- **RJ-45 blindados**: Contacto metálico continuo
- **Patches blindados**: Mantener integridad
- **Keystone shields**: Conectores de panel blindados

#### Costo vs. beneficio:
- **Análisis de ambiente**: Nivel de interferencias
- **Presupuesto**: Comparar con alternativas
- **Mantenimiento**: Complejidad adicional
- **Futuro**: Consideraciones de upgrades

## 4. Características técnicas: Propiedades mecánicas, eléctricas y categorías

### Propiedades mecánicas:

#### Flexibilidad:
- **Radio de curvatura**: Mínimo sin daño (típicamente 4x diámetro)
- **Tensión de instalación**: Máxima fuerza durante pull (típicamente 25 lbs)
- **Temperatura de instalación**: Rango operativo (-20°C a +60°C)
- **Vida útil**: Ciclos de flexión antes de falla

#### Resistencia ambiental:
- **Humedad**: Resistencia a absorción de agua
- **UV**: Estabilidad bajo luz ultravioleta
- **Químicos**: Resistencia a solventes y ácidos
- **Roedores**: Cubiertas resistentes a mordeduras

### Propiedades eléctricas:

#### Atenuación:
La pérdida de señal a lo largo del cable, medida en dB/100m:
- **Cat 5e @ 100 MHz**: 24 dB/100m máximo
- **Cat 6 @ 250 MHz**: 19.8 dB/100m máximo
- **Cat 6a @ 500 MHz**: 19.8 dB/100m máximo

#### Near-End Crosstalk (NEXT):
Interferencia entre pares en el extremo cercano:
- **Medición**: dB (mayor valor = mejor)
- **Cat 5e @ 100 MHz**: 35.3 dB mínimo
- **Cat 6 @ 250 MHz**: 39.9 dB mínimo
- **Critical**: Para operación full-duplex

#### Return Loss:
Reflexiones causadas por impedancia no uniforme:
- **Impedancia nominal**: 100 ohmios ± 15%
- **Variación**: Debe mantenerse constante
- **Medición**: dB (mayor valor = mejor)

### Categorías de cables UTP:

#### Categoría 3:
- **Ancho de banda**: Hasta 16 MHz
- **Aplicaciones**: Telefonía, 10Base-T
- **Velocidad**: 10 Mbps máximo
- **Estado**: Obsoleto para datos

#### Categoría 5:
- **Ancho de banda**: Hasta 100 MHz
- **Aplicaciones**: 100Base-TX
- **Velocidad**: 100 Mbps
- **Estado**: Reemplazado por 5e

#### Categoría 5e (Enhanced):
- **Ancho de banda**: Hasta 100 MHz
- **Aplicaciones**: 100Base-TX, 1000Base-T
- **Velocidad**: 1 Gbps
- **Características**: Mejor NEXT, FEXT
- **Status**: Estándar mínimo actual

#### Categoría 6:
- **Ancho de banda**: Hasta 250 MHz
- **Aplicaciones**: 1000Base-T, 10GBase-T (55m)
- **Velocidad**: 1-10 Gbps
- **Características**: Separador físico de pares
- **Certificación**: Más estricta que Cat 5e

#### Categoría 6a (Augmented):
- **Ancho de banda**: Hasta 500 MHz
- **Aplicaciones**: 10GBase-T (100m)
- **Velocidad**: 10 Gbps full distance
- **Características**: Blindaje mejorado
- **Diámetro**: Mayor que Cat 6

#### Categoría 7:
- **Ancho de banda**: Hasta 600 MHz
- **Características**: Pares individualment blindados
- **Conectores**: No RJ-45 estándar
- **Aplicaciones**: Limitadas por conectores

#### Categoría 8:
- **Ancho de banda**: Hasta 2000 MHz
- **Aplicaciones**: 25GBase-T, 40GBase-T
- **Distancia**: 30 metros máximo
- **Uso**: Data centers principalmente

### Comparativa de rendimiento:
```
Categoría | Frecuencia | Aplicación principal | Distancia
----------|------------|---------------------|----------
Cat 5e    | 100 MHz    | Gigabit Ethernet    | 100m
Cat 6     | 250 MHz    | 10G Ethernet        | 55m
Cat 6a    | 500 MHz    | 10G Ethernet        | 100m
Cat 8     | 2000 MHz   | 25G/40G Ethernet    | 30m
```

## 5. Cable coaxial: Su construcción, uso histórico y aplicaciones actuales

### Estructura del cable coaxial:

#### Componentes:
1. **Conductor central**: Cobre sólido o multifilamento
2. **Dieléctrico**: Aislante (polietileno, teflón)
3. **Blindaje**: Malla de cobre + lámina de aluminio
4. **Cubierta exterior**: PVC o materiales flame-retardant

#### Geometría:
- **Coaxial**: Conductores comparten el mismo eje
- **Impedancia**: 50Ω o 75Ω según aplicación
- **Simetría**: Fundamental para el rendimiento

### Tipos de cable coaxial:

#### RG-8 (Thicknet - 10Base-5):
- **Impedancia**: 50 ohmios
- **Diámetro**: ~10mm
- **Distancia**: 500 metros
- **Conectores**: N-type, AUI
- **Estado**: Obsoleto para LANs

#### RG-58 (Thinnet - 10Base-2):
- **Impedancia**: 50 ohmios
- **Diámetro**: ~5mm
- **Distancia**: 185 metros
- **Conectores**: BNC
- **Estado**: Obsoleto para LANs

#### RG-6:
- **Impedancia**: 75 ohmios
- **Aplicaciones**: Cable TV, Internet por cable
- **Distancia**: Varios kilómetros
- **Frecuencia**: Hasta 3 GHz
- **Estado**: Activo en CATV

#### RG-11:
- **Impedancia**: 75 ohmios
- **Mayor grosor**: Menor atenuación que RG-6
- **Aplicaciones**: Distribución principal CATV
- **Distancia**: Muy largas distancias

### Aplicaciones históricas:

#### Redes Ethernet originales:
- **10Base-5**: Primera implementación Ethernet
- **Topología bus**: Todos los nodos en un cable
- **Terminadores**: 50Ω en extremos
- **Vampiro taps**: Conexiones sin cortar cable

#### Problemas que llevaron al cambio:
- **Punto único de falla**: Corte afecta toda la red
- **Instalación compleja**: Requiere herramientas especiales
- **Diagnóstico difícil**: Localizar fallas problemático
- **Escalabilidad limitada**: Difícil agregar/quitar nodos

### Aplicaciones actuales:

#### DOCSIS (Data Over Cable Service Interface):
- **Internet por cable**: Banda ancha sobre CATV
- **Velocidades**: Hasta varios Gbps
- **Frecuencias**: 5-1000 MHz aproximadamente
- **Bidireccional**: Upstream y downstream

#### Televisión por cable:
- **Distribución de señal**: Desde headend hasta homes
- **Múltiples canales**: Multiplexación por frecuencia
- **Calidad**: Baja atenuación a altas frecuencias
- **Infraestructura establecida**: Red existente

#### Aplicaciones RF:
- **Antenas**: Conexión de antenas a equipos
- **Instrumentación**: Equipos de medición RF
- **Broadcast**: Televisión y radio
- **Militar/Aero**: Comunicaciones especializadas

### Ventajas del coaxial:
- **Blindaje excelente**: Inmune a EMI
- **Ancho de banda alto**: Soporta altas frecuencias
- **Distancias largas**: Menor atenuación que UTP
- **Confiabilidad**: Construcción robusta

### Desventajas:
- **Costo alto**: Más caro que UTP
- **Instalación compleja**: Requiere herramientas especiales
- **Flexibilidad limitada**: Más rígido que UTP
- **Conectores**: Más complejos y caros

## 6. Cable de fibra óptica: Cómo la luz transmite datos

### Principios físicos fundamentales:

#### Reflexión total interna:
Cuando la luz viaja de un medio más denso (núcleo) a uno menos denso (revestimiento), y el ángulo de incidencia es mayor al ángulo crítico, la luz se refleja completamente:

```
Ángulo crítico = arcsin(n₂/n₁)
Donde: n₁ = índice de refracción del núcleo
       n₂ = índice de refracción del revestimiento
```

#### Propagación de la luz:
- **Núcleo**: Índice de refracción alto (~1.46)
- **Revestimiento**: Índice menor (~1.45)
- **Diferencia**: Permite confinamiento de la luz
- **Guía de onda**: Fibra actúa como guía óptica

### Estructura de la fibra óptica:

#### Componentes principales:
1. **Núcleo (Core)**: Vidrio ultra puro donde viaja la luz
2. **Revestimiento (Cladding)**: Vidrio con menor índice de refracción
3. **Recubrimiento (Coating)**: Protección primaria de acrilato
4. **Buffer**: Protección adicional (900 µm típicamente)
5. **Cubierta exterior**: Protección mecánica y ambiental

#### Materiales:
- **Vidrio de sílice**: Ultra puro (99.99%)
- **Dopantes**: Germanio (núcleo), Flúor (revestimiento)
- **Polímeros**: Para recubrimientos protectivos
- **Aramida**: Elementos de tensión

### Tipos de fibra óptica:

#### Fibra multimodo:
**Características:**
- **Núcleo grande**: 50 o 62.5 µm
- **Múltiples modos**: Varios caminos para la luz
- **Distancias cortas**: Hasta 2 km típicamente
- **LED o laser**: Fuentes de luz más económicas

**Step-index multimodo:**
- **Índice constante**: En núcleo y revestimiento
- **Dispersión modal alta**: Ensanchamiento de pulsos
- **Ancho de banda limitado**: Por dispersión
- **Aplicaciones**: Enlaces cortos, LAN

**Graded-index multimodo:**
- **Índice variable**: Disminuye del centro hacia afuera
- **Compensación de dispersión**: Diferentes velocidades
- **Mejor rendimiento**: Que step-index
- **Aplicaciones**: LANs de alta velocidad

#### Fibra monomodo:
**Características:**
- **Núcleo pequeño**: 8-10 µm
- **Un solo modo**: Un camino para la luz
- **Largas distancias**: Hasta 80+ km
- **Laser requerido**: Fuentes de luz precisas

**Tipos de monomodo:**
- **G.652 (Standard)**: Para 1310 nm y 1550 nm
- **G.653 (Dispersion Shifted)**: Optimizada para 1550 nm
- **G.655 (Non-Zero DS)**: Balance entre dispersión y no-linearidades
- **G.657 (Bend Insensitive)**: Resistente a curvaturas

### Ventajas de la fibra óptica:

#### Técnicas:
- **Ancho de banda enorme**: Terahertz de capacidad
- **Inmune a EMI**: No hay interferencia electromagnética
- **Baja atenuación**: 0.2 dB/km @ 1550 nm
- **Seguridad**: Difícil de interceptar
- **Largas distancias**: Sin repetidores

#### Operacionales:
- **Vida útil larga**: 25+ años
- **Peso ligero**: Comparado con cobre
- **Tamaño pequeño**: Mayor densidad de fibras
- **No hay spark hazard**: Seguro en ambientes explosivos

## 7. Diferencias entre fibra monomodo y multimodo

### Comparación detallada:

| Característica | Multimodo | Monomodo |
|----------------|-----------|-----------|
| **Diámetro núcleo** | 50/62.5 µm | 8-10 µm |
| **Fuente de luz** | LED/VCSEL | Laser |
| **Distancia máxima** | 2 km | 80+ km |
| **Ancho de banda** | Moderado | Muy alto |
| **Costo inicial** | Bajo | Alto |
| **Aplicaciones** | LAN/Campus | WAN/Telecom |
| **Complejidad** | Baja | Alta |

### Selección de tipo:

#### Factores de decisión:
1. **Distancia requerida**: 
   - < 2 km → Multimodo
   - > 2 km → Monomodo
2. **Ancho de banda**:
   - < 10 Gbps → Multimodo OK
   - > 10 Gbps → Monomodo preferible
3. **Presupuesto**:
   - Limitado → Multimodo
   - Sin restricciones → Monomodo
4. **Futuro crecimiento**:
   - Limitado → Multimodo
   - Expansión planned → Monomodo

## 8. Propiedades de la fibra: Inmunidad a interferencias, ancho de banda y distancias

### Inmunidad a interferencias electromagnéticas:

#### Ventajas fundamentales:
- **No conductiva**: No hay corriente eléctrica
- **Aislamiento galvánico**: Separación eléctrica completa
- **Inmune a EMI/RFI**: Campos electromagnéticos no afectan
- **No genera interferencia**: No radiación electromagnética

#### Aplicaciones críticas:
- **Hospitales**: Cerca de equipos médicos sensibles
- **Industria**: Ambientes con motores eléctricos grandes
- **Plantas químicas**: Atmósferas potencialmente explosivas
- **Subestaciones**: Campos electromagnéticos intensos

### Ancho de banda y capacidad:

#### Ancho de banda teórico:
- **Espectro óptico**: ~300 THz disponible
- **Ventanas de transmisión**: 850, 1310, 1550 nm
- **DWDM**: Dense Wavelength Division Multiplexing
- **Capacidades actuales**: Terabits por segundo

#### Factores limitantes:
- **Dispersión cromática**: Ensanchamiento de pulsos
- **Dispersión modal**: Solo en multimodo
- **Atenuación**: Pérdida de potencia óptica
- **Efectos no-lineales**: A altas potencias

### Distancias de transmisión:

#### Multimodo:
- **OM1 (62.5/125)**: 300m @ 1 Gbps
- **OM2 (50/125)**: 550m @ 1 Gbps
- **OM3 (50/125)**: 300m @ 10 Gbps
- **OM4 (50/125)**: 400m @ 10 Gbps
- **OM5 (50/125)**: 400m @ 10 Gbps (optimizada para SWDM)

#### Monomodo:
- **OS1 (Indoor)**: 10 km @ 10 Gbps
- **OS2 (Outdoor)**: 40+ km @ 10 Gbps
- **Con amplificadores**: 100+ km posible
- **Enlaces submarinos**: Miles de kilómetros

### Consideraciones de pérdidas:

#### Fuentes de atenuación:
- **Absorción**: Impurezas en el vidrio
- **Dispersión Rayleigh**: Variaciones microscópicas
- **Curvaturas**: Macrobends y microbends
- **Empalmes**: Fusión o conectores

#### Presupuesto de potencia:
```
Potencia TX - Pérdidas totales ≥ Sensibilidad RX

Pérdidas típicas:
- Fibra: 0.3 dB/km @ 1310 nm, 0.2 dB/km @ 1550 nm
- Conectores: 0.5 dB cada uno
- Empalmes: 0.1 dB cada uno
- Margen del sistema: 3 dB
```

## Laboratorios Prácticos

### Lab 1: Identificación de cables
1. Examinar diferentes tipos de cables
2. Identificar categorías y especificaciones
3. Medir características eléctricas básicas

### Lab 2: Pruebas de cables UTP
1. Usar cable tester para certificación
2. Medir NEXT, atenuación, return loss
3. Interpretar resultados de pruebas

### Lab 3: Trabajo con fibra óptica
1. Inspeccionar conectores de fibra
2. Medir pérdidas con power meter
3. Usar OTDR para caracterización

### Lab 4: Comparación de medios
1. Instalar diferentes tipos de cables
2. Medir rendimiento en condiciones reales
3. Analizar costo vs. rendimiento

## Evaluación

1. **Teórica**: Características y aplicaciones de cada tipo
2. **Práctica**: Identificación y prueba de cables
3. **Diseño**: Selección apropiada para diferentes escenarios
4. **Análisis**: Comparación costo-beneficio de alternativas

[⬅️ Anterior: Medios de Comunicación.](../Unidad2-RedesDeComunicaciones/MediosComunicacion.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Cableado estructurado. ➡️](./CableadoEstructurado.md)