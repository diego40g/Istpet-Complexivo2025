# Construcción de cables

## 1. Herramientas y materiales: Los equipos esenciales para un trabajo bien hecho

### Herramientas de terminación:

#### Crimpadoras (Crimping Tools):
**Para conectores RJ-45:**
- **Tipo básico**: Para uso ocasional y aprendizaje
- **Profesional**: Con ajuste de presión y ciclo completo
- **Premium**: Auto-ajustable con indicador de presión correcta
- **Características deseables**:
  - Cuchillas integradas para corte
  - Guías de alineación precisas
  - Mecanismo de trinquete
  - Mangos ergonómicos

**Para otros conectores:**
- **BNC**: Para cable coaxial
- **F-type**: Para cable CATV
- **Modular**: Para RJ-11, RJ-12
- **Fiber**: Para conectores de fibra óptica

#### Pelacables (Wire Strippers):
**Tipos principales:**
- **Manuales**: Control total del proceso
- **Automáticos**: Velocidad y consistencia
- **Calibrados**: Para diferentes categorías de cable
- **Coaxiales**: Especializados para cable coaxial

**Características importantes:**
- **Múltiples calibres**: Para diferentes tipos de cable
- **Corte limpio**: Sin dañar conductores
- **Ajuste preciso**: Profundidad de corte controlable
- **Ergonomía**: Uso prolongado sin fatiga

#### Herramientas de punch-down:
**Impact tools:**
- **110 punch-down tool**: Para bloques de terminación
- **66 punch-down tool**: Para bloques tradicionales
- **Krone tool**: Para sistemas europeos
- **Cuchillas intercambiables**: Para diferentes aplicaciones

**Características técnicas:**
- **Tensión ajustable**: Según tipo de cable
- **Corte automático**: Del exceso de conductor
- **Indicador de impacto**: Confirmación visual/audible
- **Diseño balanceado**: Reducir fatiga del usuario

### Herramientas de medición y prueba:

#### Cable testers básicos:
**Funciones principales:**
- **Continuity testing**: Verificar conexiones
- **Wire mapping**: Verificar pineado correcto
- **Length measurement**: Medición de longitud
- **Basic faults**: Cortos, abiertos, cruzados

**Tipos disponibles:**
- **Tone generators**: Localización de cables
- **Basic wire mappers**: Pineado y continuidad
- **Length meters**: TDR básico
- **Multi-function**: Combinación de pruebas

#### Certificadores de cable:
**Capacidades avanzadas:**
- **Performance testing**: NEXT, FEXT, atenuación
- **Category certification**: Cumplimiento de estándares
- **Frequency sweeping**: Análisis espectral
- **Detailed reporting**: Documentación profesional

**Parámetros medidos:**
- **Attenuation**: Pérdida de señal
- **NEXT**: Near End Crosstalk
- **FEXT**: Far End Crosstalk
- **Return Loss**: Reflexiones
- **ACR**: Attenuation to Crosstalk Ratio
- **Propagation delay**: Retraso de propagación

#### Herramientas de fibra óptica:
**Visual fault locator:**
- **Luz roja visible**: 650 nm típicamente
- **Localización de fallas**: Breaks, bends, conectores
- **Alcance**: Hasta 5 km en fibra monomodo
- **Seguridad**: Clase 2 o menor

**Power meter y light source:**
- **Medición de potencia**: dBm, µW
- **Pérdidas de enlace**: Atenuación total
- **Longitudes de onda**: 850, 1300, 1550 nm
- **Certificación**: Cumplimiento de estándares

**OTDR (Optical Time Domain Reflectometer):**
- **Análisis de enlace**: Ubicación exacta de eventos
- **Caracterización**: Pérdidas punto a punto
- **Documentación**: Trazas y reportes
- **Troubleshooting**: Diagnóstico avanzado

### Materiales consumibles:

#### Conectores RJ-45:
**Categorías disponibles:**
- **Cat 5e**: Para aplicaciones básicas
- **Cat 6**: Mejor rendimiento hasta 250 MHz
- **Cat 6a**: Soporte hasta 500 MHz
- **Blindados**: Para ambientes con EMI

**Características técnicas:**
- **Contactos dorados**: Resistencia a corrosión
- **Insert molded**: Mayor confiabilidad
- **Load bar**: Para facilitar terminación
- **Boot**: Protección de cable strain relief

#### Cables UTP:
**Especificaciones de compra:**
- **Categoría**: 5e, 6, 6a según requerimientos
- **Tipo de conductor**: Sólido para instalación permanente
- **Jacket rating**: CMP, CMR, CM según aplicación
- **Longitud**: Cajas de 305m (1000 ft) estándar

**Códigos de colores estándar:**
```
Par 1: Azul/Blanco-Azul           (Pins 4,5)
Par 2: Naranja/Blanco-Naranja     (Pins 1,2)
Par 3: Verde/Blanco-Verde         (Pins 3,6)  
Par 4: Café/Blanco-Café          (Pins 7,8)
```

#### Materiales de soporte:
- **Ties de velcro**: Administración de cables
- **Cable boots**: Protección de conectores
- **Cable lubricant**: Para instalación en conductos
- **Cleaning supplies**: Alcohol isopropílico, wipes
- **Labels**: Identificación y documentación

### Equipos de seguridad:

#### Protección personal:
- **Anteojos de seguridad**: Especialmente para fibra óptica
- **Guantes**: Protección contra cortes
- **Rodilleras**: Para trabajo en espacios reducidos
- **Linterna/headlamp**: Iluminación en áreas oscuras

#### Seguridad específica para fibra:
- **Disposal containers**: Para fragmentos de fibra
- **Fiber inspection microscopes**: Verificar limpieza
- **Cleaning supplies**: Alcohol, wipes sin pelusa
- **Protective caps**: Para conectores no utilizados

## 2. Proceso de terminación de cables UTP: Una guía práctica paso a paso

### Preparación del cable:

#### Paso 1: Medición y corte
1. **Medir longitud requerida**: Agregar 10-15 cm extra
2. **Marcar punto de corte**: Con marcador permanente
3. **Corte limpio**: Perpendicular al eje del cable
4. **Inspeccionar**: Verificar que todos los conductores estén intactos

#### Paso 2: Remoción del jacket
1. **Medir desde extremo**: 12-15 mm de jacket a remover
2. **Corte cuidadoso**: Con pelacables o cuchilla
3. **Verificar profundidad**: No dañar aislamiento de conductores
4. **Remover jacket**: Tirar suavemente del segmento cortado

### Desentrenzado y ordenamiento:

#### Paso 3: Separar pares
1. **Identificar pares**: Por colores establecidos
2. **Desentrenzar cuidadosamente**: Mantener mínimo desentrenzado
3. **Separar conductores**: Individualmente
4. **Inspeccionar**: Verificar que no hay daños

#### Paso 4: Ordenamiento según estándar
**Para T568B (más común):**
```
Posición | Color
---------|------------------
1        | Blanco-Naranja
2        | Naranja
3        | Blanco-Verde
4        | Azul
5        | Blanco-Azul
6        | Verde
7        | Blanco-Café
8        | Café
```

**Para T568A:**
```
Posición | Color
---------|------------------
1        | Blanco-Verde
2        | Verde
3        | Blanco-Naranja
4        | Azul
5        | Blanco-Azul
6        | Naranja
7        | Blanco-Café
8        | Café
```

### Inserción en conector:

#### Paso 5: Alineación de conductores
1. **Verificar orden**: Según estándar seleccionado
2. **Nivelar extremos**: Todos los conductores a la misma altura
3. **Corte final**: Dejar 12-13 mm de conductor expuesto
4. **Inspección final**: Verificar orden y longitud

#### Paso 6: Inserción en RJ-45
1. **Hold connector**: Pin 1 a la izquierda, clip hacia abajo
2. **Inserción suave**: Conductores hasta el fondo
3. **Verificar posicionamiento**: Cada conductor en su canal
4. **Jacket insertion**: Jacket dentro del conector ~6mm

### Crimpado:

#### Paso 7: Verificación pre-crimp
1. **Conductores hasta el fondo**: Visibles en la punta
2. **Orden correcto**: Revisar una vez más
3. **Jacket bien insertado**: Para strain relief adecuado
4. **Sin conductores cruzados**: Cada uno en su canal

#### Paso 8: Proceso de crimpado
1. **Insertar en crimpadora**: Conector completamente dentro
2. **Presión uniforme**: Apretar firmemente hasta el final
3. **Ciclo completo**: Hasta que la crimpadora se abra
4. **Inspeccionar**: Conexiones uniformes y firmes

### Verificación y prueba:

#### Paso 9: Inspección visual
1. **Contactos dorados**: Deben estar deformados uniformemente
2. **Strain relief**: Jacket bien sujeto por el conector
3. **Sin shorts**: Conductores no tocándose
4. **Alineación**: Todos los contactos paralelos

#### Paso 10: Pruebas eléctricas
1. **Continuity test**: Con cable tester básico
2. **Wire mapping**: Verificar pineado correcto
3. **Shorts and opens**: Verificar integridad
4. **Length verification**: Si está disponible

## 3. Normas de cableado T568A y T568B: La importancia de seguir un esquema de colores

### Historia de los estándares:

#### Desarrollo de T568A:
- **Primer estándar**: TIA/EIA-568-A (1995)
- **Compatibilidad**: Con cableado telefónico existente
- **Par principal**: Verde en posiciones 1,2 (como telefonía)
- **Adopción**: Principalmente en instalaciones gubernamentales

#### Evolución a T568B:
- **Estándar revisado**: TIA/EIA-568-B (2001)
- **Par principal**: Naranja en posiciones 1,2
- **Compatibilidad**: Con AT&T 258A
- **Adopción**: Más común en instalaciones comerciales

### Especificaciones técnicas detalladas:

#### T568A Pinout:
```
Pin | Color           | Par | Función (100Base-TX)
----|-----------------|-----|--------------------
1   | Blanco-Verde    | 3   | RX+
2   | Verde           | 3   | RX-
3   | Blanco-Naranja  | 2   | TX+
4   | Azul            | 1   | No usado
5   | Blanco-Azul     | 1   | No usado
6   | Naranja         | 2   | TX-
7   | Blanco-Café     | 4   | No usado
8   | Café            | 4   | No usado
```

#### T568B Pinout:
```
Pin | Color           | Par | Función (100Base-TX)
----|-----------------|-----|--------------------
1   | Blanco-Naranja  | 2   | TX+
2   | Naranja         | 2   | TX-
3   | Blanco-Verde    | 3   | RX+
4   | Azul            | 1   | No usado
5   | Blanco-Azul     | 1   | No usado
6   | Verde           | 3   | RX-
7   | Blanco-Café     | 4   | No usado
8   | Café            | 4   | No usado
```

### Tipos de cables según terminación:

#### Cable directo (Straight-through):
- **Ambos extremos igual**: T568A-T568A o T568B-T568B
- **Aplicaciones**:
  - PC a Switch
  - PC a Hub
  - Router a Switch
  - Switch a Router (puerto WAN)

#### Cable cruzado (Crossover):
- **Extremos diferentes**: T568A-T568B
- **Intercambio de pares**: TX y RX invertidos
- **Aplicaciones**:
  - PC a PC directo
  - Switch a Switch (sin uplink)
  - Hub a Hub
  - Router a Router

#### Cables cruzados modernos:
**Auto-MDI/MDIX:**
- **Detección automática**: Equipos modernos detectan tipo necesario
- **Adaptación**: Intercambian internamente TX/RX según necesidad
- **Simplicidad**: Eliminan necesidad de cables cruzados
- **Compatibilidad**: Funciona con cables directos únicamente

### Consideraciones para la selección:

#### Factores técnicos:
- **Rendimiento idéntico**: Ambos estándares funcionan igual
- **Compatibilidad**: Con equipos existentes
- **Consistency**: Usar un solo estándar en toda la instalación
- **Documentation**: Registrar estándar utilizado

#### Recomendaciones prácticas:
1. **T568B más común**: En instalaciones comerciales nuevas
2. **T568A**: Si hay infraestructura existente con este estándar
3. **Consistency**: Nunca mezclar en la misma instalación
4. **Training**: Entrenar personal en un solo estándar

### Aplicaciones específicas:

#### Para redes Ethernet:
- **10/100 Mbps**: Usa pares 2 y 3 únicamente
- **1000 Mbps**: Usa los 4 pares
- **10G**: Requiere los 4 pares con especificaciones estrictas
- **PoE**: Power over Ethernet usa pares no utilizados

#### Para telefonía:
- **Línea simple**: Par 2 (posiciones 4,5)
- **Dos líneas**: Pares 1 y 2
- **Digital**: Puede usar múltiples pares
- **Integration**: Voz y datos en la misma infraestructura

## 4. Pruebas y validación: Cómo se verifica la calidad de una conexión terminada

### Niveles de pruebas:

#### Nivel 1 - Verificación básica:
**Pruebas mínimas requeridas:**
- **Continuity**: Verificar que hay conexión eléctrica
- **Wire mapping**: Verificar pineado correcto
- **Shorts**: Verificar que no hay cortocircuitos
- **Opens**: Verificar que no hay conexiones abiertas

**Herramientas utilizadas:**
- **Cable testers básicos**: $50-200 USD
- **Tone generators**: Para localización
- **Multimetros**: Para mediciones básicas
- **Visual inspection**: Inspección física

#### Nivel 2 - Pruebas de rendimiento:
**Parámetros medidos:**
- **Attenuation**: Pérdida de señal
- **NEXT**: Diafonía en extremo cercano
- **Length**: Longitud exacta del enlace
- **Impedance**: Verificación de 100 ohmios

**Herramientas requeridas:**
- **LAN testers**: $500-2000 USD
- **Handheld analyzers**: Portables
- **Qualification testers**: Verifican capacidad para aplicación específica

#### Nivel 3 - Certificación completa:
**Todos los parámetros TIA-568:**
- **Attenuation**: A todas las frecuencias
- **NEXT**: Near End Crosstalk
- **FEXT**: Far End Crosstalk  
- **ELFEXT**: Equal Level FEXT
- **Return Loss**: Reflexiones
- **Propagation Delay**: Retraso de propagación
- **Delay Skew**: Diferencia entre pares

### Procedimientos de prueba específicos:

#### Preparación para pruebas:
1. **Documentar**: Enlaces a probar
2. **Equipment setup**: Calibrar equipos de prueba
3. **Environmental**: Registrar condiciones ambientales
4. **Adapters**: Verificar que sean apropiados para categoría

#### Secuencia de pruebas:
1. **Visual inspection**: Antes de pruebas eléctricas
2. **Basic connectivity**: Continuity y wire map
3. **Performance testing**: Según nivel requerido
4. **Documentation**: Registrar todos los resultados

### Interpretación de resultados:

#### Pass/Fail criteria:
**Para Categoría 5e:**
- **Attenuation**: Máx 24 dB @ 100 MHz
- **NEXT**: Mín 35.3 dB @ 100 MHz
- **Return Loss**: Mín 20.1 dB @ 100 MHz
- **ACR**: Mín 11.3 dB @ 100 MHz

**Para Categoría 6:**
- **Attenuation**: Máx 19.8 dB @ 250 MHz
- **NEXT**: Mín 39.9 dB @ 250 MHz  
- **Return Loss**: Mín 20.1 dB @ 250 MHz
- **ACR**: Mín 20.1 dB @ 250 MHz

#### Análisis de fallas comunes:
**Wiremap errors:**
- **Opens**: Conductor no conectado
- **Shorts**: Conductores unidos
- **Miswires**: Pineado incorrecto
- **Split pairs**: Pares no respetados

**Performance failures:**
- **High attenuation**: Cable demasiado largo o defectuoso
- **Poor NEXT**: Desentrenzado excesivo, conectores defectuosos
- **Return loss**: Impedancia no uniforme
- **Length**: Medición incorrecta o cable defectuoso

### Documentación y reportes:

#### Información requerida:
- **Cable ID**: Identificación única
- **Length**: Longitud medida
- **Test results**: Todos los parámetros
- **Pass/Fail**: Cumplimiento con estándar
- **Date/Time**: Cuándo se realizó la prueba
- **Technician**: Quien realizó la prueba

#### Formatos de reporte:
- **Individual reports**: Por cada enlace
- **Summary reports**: Consolidado del proyecto
- **Graphical**: Gráficos de frecuencia vs parámetro
- **Digital**: Base de datos para gestión

### Troubleshooting de problemas:

#### Metodología sistemática:
1. **Identify symptoms**: Qué tipo de falla
2. **Isolate problem**: Qué componente específico
3. **Verify fix**: Probar después de corrección
4. **Document**: Registrar problema y solución

#### Problemas comunes y soluciones:

**Problema: High attenuation**
- **Causas**: Cable demasiado largo, conectores defectuosos, empalmes
- **Solución**: Verificar longitud, cambiar conectores, eliminar empalmes

**Problema: Poor NEXT**
- **Causas**: Desentrenzado excesivo, conectores de baja calidad
- **Solución**: Minimizar desentrenzado, usar conectores certificados

**Problema: Wiremap errors**
- **Causas**: Terminación incorrecta, cables dañados
- **Solución**: Re-terminar según estándar, reemplazar cable dañado

## Laboratorios Prácticos Avanzados

### Lab 1: Terminación profesional
**Objetivos:**
- Dominar técnica de terminación RJ-45
- Lograr resultados consistentes y confiables
- Minimizar tiempo de terminación

**Actividades:**
1. **Practice session**: 20 terminaciones T568B
2. **Quality control**: Inspección visual detallada
3. **Speed test**: Terminación en menos de 2 minutos
4. **Troubleshooting**: Corregir terminaciones defectuosas

### Lab 2: Certificación de enlaces
**Objetivos:**
- Usar equipos de certificación profesionales
- Interpretar resultados correctamente
- Generar reportes profesionales

**Actividades:**
1. **Setup**: Configurar certificador para Cat 6
2. **Testing**: Certificar 10 enlaces diferentes
3. **Analysis**: Interpretar resultados marginales
4. **Documentation**: Generar reportes completos

### Lab 3: Troubleshooting avanzado
**Objetivos:**
- Diagnosticar problemas complejos
- Desarrollar metodología sistemática
- Documentar problemas y soluciones

**Actividades:**
1. **Fault injection**: Crear fallas conocidas
2. **Diagnosis**: Localizar y caracterizar fallas
3. **Repair**: Corregir todos los problemas
4. **Verification**: Certificar reparaciones

### Lab 4: Proyecto integrado
**Objetivos:**
- Aplicar todos los conocimientos adquiridos
- Trabajar bajo condiciones reales
- Producir documentación profesional

**Actividades:**
1. **Installation**: 50 puntos de red completos
2. **Testing**: Certificación de todos los enlaces
3. **Documentation**: As-built drawings y reportes
4. **Presentation**: Presentar resultados al cliente

## Evaluación del módulo

### Examen teórico (40%):
- **Estándares**: TIA-568, categorías de cable
- **Herramientas**: Función y aplicación correcta  
- **Procedures**: Secuencias de terminación y prueba
- **Troubleshooting**: Metodologías de diagnóstico

### Examen práctico (60%):
- **Terminación**: 10 cables RJ-45 en 30 minutos
- **Quality**: 95% pass rate en certificación
- **Troubleshooting**: Localizar y corregir 5 fallas
- **Documentation**: Completar reportes profesionales

### Criterios de aprobación:
- **Nota mínima**: 80% en cada componente
- **Quality standards**: Cumplir especificaciones TIA-568
- **Time limits**: Completar dentro de tiempo asignado
- **Professional presentation**: Documentación completa y precisa

## Recursos para desarrollo continuo

### Certificaciones profesionales:
- **BICSI Installer 1**: Certificación básica
- **BICSI Installer 2**: Nivel avanzado
- **Manufacturer programs**: Panduit, CommScope, etc.
- **Fiber optic certifications**: FOA, Corning, etc.

### Actualización tecnológica:
- **Nuevas categorías**: Cat 6a, Cat 8
- **Fiber to desktop**: Tendencias futuras
- **Power over Ethernet**: PoE+, PoE++
- **Testing standards**: Actualizaciones TIA

### Herramientas de referencia:
- **TIA standards**: Documentos oficiales
- **Manufacturer guides**: Manuales de instalación
- **Online calculators**: Para pérdidas y distancias
- **Mobile apps**: Para referencia rápida

Esta formación proporciona una base sólida para trabajar profesionalmente en instalación y certificación de sistemas de cableado estructurado, preparando al estudiante para roles técnicos en la industria de telecomunicaciones.

[⬅️ Anterior: Cableado estructurado.](./CableadoEstructurado.md) | [Volver al índice](../TablaDeContenidos.md) | 