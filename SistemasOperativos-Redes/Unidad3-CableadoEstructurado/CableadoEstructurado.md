# Cableado estructurado

## 1. Concepto y definición: Por qué un sistema organizado es crucial para las redes modernas

### Definición de cableado estructurado:
El cableado estructurado es un sistema de cableado de telecomunicaciones estandarizado que proporciona una infraestructura de cableado organizada y uniforme para soportar múltiples sistemas de información dentro de un edificio o campus.

### Características fundamentales:

#### Estandarización:
- **Normas internacionales**: Cumplimiento con estándares reconocidos
- **Compatibilidad universal**: Interoperabilidad entre fabricantes
- **Metodología consistente**: Diseño, instalación y mantenimiento
- **Documentación estándar**: Sistemas de etiquetado y registro

#### Flexibilidad:
- **Múltiples aplicaciones**: Voz, datos, video en la misma infraestructura
- **Cambios fáciles**: Reconfiguración sin recableado
- **Escalabilidad**: Crecimiento futuro considerado
- **Tecnología independiente**: No atado a un fabricante específico

#### Organización:
- **Topología jerárquica**: Estructura lógica y física
- **Administración centralizada**: Control desde puntos específicos
- **Identificación única**: Cada componente etiquetado
- **Documentación completa**: Planos, registros, pruebas

### Importancia en las redes modernas:

#### Convergencia tecnológica:
Las redes modernas manejan múltiples tipos de información:
- **Datos**: Aplicaciones de red tradicionales
- **Voz**: Telefonía IP (VoIP)
- **Video**: Videoconferencia, vigilancia IP
- **Control**: Sistemas de automatización de edificios
- **Inalámbrico**: Access points Wi-Fi

#### Beneficios económicos:
- **Reducción de costos**: Menor infraestructura física
- **Tiempo de implementación**: Instalación más rápida
- **Mantenimiento simplificado**: Menos sistemas que administrar
- **Valor de reventa**: Incrementa valor del inmueble
- **ROI mejorado**: Retorno de inversión a largo plazo

#### Eficiencia operacional:
- **Administración centralizada**: Control unificado
- **Diagnóstico simplificado**: Localización rápida de problemas
- **Cambios ágiles**: Reconfiguración sin interrupciones
- **Escalabilidad**: Crecimiento planificado
- **Documentación**: Registro completo de la infraestructura

### Problemas del cableado no estructurado:

#### Cableado punto a punto tradicional:
- **Cables dedicados**: Una aplicación por cable
- **Múltiples sistemas**: Diferentes tipos de cable
- **Administración compleja**: Sin estándares
- **Cambios costosos**: Requieren recableado
- **Documentación pobre**: Difícil mantenimiento

#### Consecuencias:
- **Costos elevados**: Multiplicidad de sistemas
- **Tiempo perdido**: Localización de fallas
- **Escalabilidad limitada**: Crecimiento difícil
- **Obsolescencia rápida**: Falta de planificación

## 2. Normas y estándares: Las guías de la industria para compatibilidad y rendimiento

### Organismos de estandarización:

#### TIA (Telecommunications Industry Association):
- **TIA-568**: Cableado de telecomunicaciones comerciales
- **TIA-569**: Espacios y rutas de telecomunicaciones
- **TIA-606**: Administración de infraestructura
- **TIA-607**: Puesta a tierra y enlaces de telecomunicaciones

#### EIA (Electronic Industries Alliance):
- **EIA/TIA-568-A/B/C**: Evolución de estándares de cableado
- **Compatibilidad**: Trabajaban conjuntamente con TIA
- **Transición**: Funciones transferidas a TIA

#### ISO/IEC (International Organization for Standardization):
- **ISO/IEC 11801**: Estándar internacional de cableado
- **Equivalencia**: Con estándares TIA/EIA
- **Adopción global**: Especialmente en Europa y Asia
- **Armonización**: Coordinación con estándares nacionales

#### IEEE (Institute of Electrical and Electronics Engineers):
- **802.3**: Estándares Ethernet
- **802.11**: Estándares Wi-Fi
- **Coordinación**: Con estándares de cableado
- **Compatibilidad**: Asegurar interoperabilidad

### TIA/EIA-568: El estándar principal

#### TIA-568-A (1995):
- **Primera versión**: Estableció fundamentos
- **Topología**: Estrella jerárquica
- **Medios reconocidos**: UTP, STP, fibra óptica
- **Distancias**: 100m para horizontal, 90m + 10m patches

#### TIA-568-B (2001):
- **Actualización**: Mejoró especificaciones
- **Nuevas categorías**: Cat 5e incluida
- **Mejores especificaciones**: NEXT, FEXT, return loss
- **Backward compatibility**: Compatible con 568-A

#### TIA-568-C (2009):
- **Versión actual**: Incluye desarrollos recientes
- **Cat 6 y 6a**: Soporte oficial
- **Alien crosstalk**: Especificaciones para cables adyacentes
- **Pruebas mejoradas**: Nuevos parámetros de certificación

### Especificaciones clave de TIA-568:

#### Topología:
```
Campus -> Building -> Floor -> Work Area
       Backbone  Horizontal  User
```

#### Distancias máximas:
- **Horizontal**: 90 metros (cable sólido)
- **Patch cords**: 5 metros en cada extremo
- **Total**: 100 metros máximo
- **Backbone**: Varía según medio (2km fibra MM, 3km fibra SM)

#### Medios reconocidos:
- **UTP 4-pair**: 100 ohm, Categorías 3, 5e, 6, 6a
- **ScTP**: 100 ohm blindado
- **Fibra multimodo**: 62.5/125 y 50/125 µm
- **Fibra monomodo**: 8.3/125 µm

### Otros estándares importantes:

#### TIA-569-B: Espacios y rutas:
- **Espacios de telecomunicaciones**: Diseño y dimensiones
- **Rutas**: Conduits, bandejas, ductos
- **Accesibilidad**: Requisitos de acceso
- **Separación**: Distancias de fuentes de interferencia

#### TIA-606-B: Administración:
- **Identificación**: Sistemas de etiquetado
- **Documentación**: Registros y planos
- **Códigos de colores**: Estandarización visual
- **Base de datos**: Gestión de información

#### TIA-607-B: Puesta a tierra:
- **TMGB**: Telecommunications Main Grounding Busbar
- **TGB**: Telecommunications Grounding Busbar
- **Equipotencialización**: Reducir diferencias de potencial
- **Protección**: Contra sobretensiones

## 3. Componentes y subsistemas: Análisis de las partes clave

### Subsistema de cableado horizontal:

#### Definición y alcance:
El cableado horizontal se extiende desde el closet de telecomunicaciones hasta el área de trabajo, sirviendo workstations individuales.

#### Componentes principales:
1. **Cable horizontal**: UTP Cat 5e/6/6a típicamente
2. **Outlet/Conector**: Jack RJ-45 en pared
3. **Patch panel**: Terminación en closet de telecomunicaciones
4. **Patch cord**: Conexión entre patch panel y switch
5. **Work area cord**: Conexión entre outlet y dispositivo

#### Especificaciones:
- **Distancia máxima**: 90 metros de cable sólido
- **Topología**: Estrella desde TC
- **Un jack por cada 10 m²**: Densidad mínima recomendada
- **Reserva**: 10% adicional para crecimiento

#### Consideraciones de diseño:
- **Ruta directa**: Evitar curvaturas excesivas
- **Separación EMI**: Distancia de fuentes de interferencia
- **Futuro crecimiento**: Planificar expansiones
- **Accesibilidad**: Para mantenimiento y cambios

### Subsistema de cableado vertical (backbone):

#### Definición y función:
El cableado backbone interconecta los closets de telecomunicaciones, cuartos de equipos y facilidades de entrada.

#### Tipos de backbone:

**Campus backbone:**
- **Interconexión**: Entre edificios
- **Medios típicos**: Fibra óptica monomodo
- **Distancias**: Hasta 3000 metros
- **Aplicaciones**: Conexión de edificios principales

**Building backbone:**
- **Interconexión**: Entre pisos del mismo edificio
- **Medios típicos**: Fibra óptica multimodo o monomodo
- **Distancias**: Hasta 500 metros (MM), 3000 metros (SM)
- **Aplicaciones**: Conexión vertical entre pisos

#### Topologías backbone:
- **Estrella jerárquica**: Centralizada desde main cross-connect
- **Distributed star**: Múltiples interconexiones
- **Mesh**: Para redundancia crítica
- **Híbrida**: Combinación según necesidades

#### Medios para backbone:
```
Aplicación           Medio              Distancia máxima
Campus backbone      Fibra SM           3000m
Building backbone    Fibra MM           500m
Building backbone    Fibra SM           3000m  
Backbone horizontal  UTP Cat 6a         100m
```

### Cuarto de telecomunicaciones (TC):

#### Función principal:
Espacio que alberga equipos de telecomunicaciones y terminaciones de cableado que sirven usuarios en un área localizada.

#### Dimensiones y especificaciones:
- **Tamaño mínimo**: 3m x 2.2m para áreas hasta 1000 m²
- **Altura mínima**: 2.6 metros
- **Puerta**: Mínimo 0.9m de ancho, abre hacia afuera
- **Cerradura**: Seguridad controlada
- **Ventilación**: Temperatura 18-24°C, humedad 30-55%

#### Componentes típicos:
1. **Patch panels**: Terminación de cables horizontales
2. **Switches de red**: Equipos activos de capa 2
3. **Rack o gabinete**: 19" estándar
4. **Administración de cables**: Cable management
5. **Alimentación**: UPS y distribución eléctrica
6. **Puesta a tierra**: TGB y enlaces equipotenciales

#### Diseño y layout:
- **Rack principal**: Equipos activos
- **Patch panels**: Encima o debajo de switches
- **Cable management**: Horizontal y vertical
- **Espacios libres**: Para crecimiento futuro
- **Accesibilidad**: Fácil acceso frontal y posterior

### Equipment Room (ER):

#### Diferencia con TC:
- **Complejidad mayor**: Equipos más sofisticados
- **Área de servicio**: Múltiples TCs o todo el edificio
- **Ambientales más estrictos**: HVAC dedicado
- **Seguridad mayor**: Control de acceso más riguroso

#### Equipos típicos:
- **Core switches**: Conmutación principal
- **Routers**: Conectividad WAN
- **Servidores**: Aplicaciones críticas
- **Storage**: Sistemas de almacenamiento
- **Comunicaciones**: PBX, sistemas de video

### Entrance Facility (EF):

#### Definición:
Punto donde servicios externos entran al edificio y se conectan al backbone del edificio.

#### Componentes:
- **Protección**: Supresores de sobretensión
- **Demarcación**: Punto de responsabilidad con proveedor
- **Cross-connect**: Interconexión de servicios
- **Equipos carrier**: Proporcionados por ISP/telco

#### Servicios típicos:
- **Internet**: Conexiones de banda ancha
- **Telefonía**: Líneas analógicas o digitales
- **Cable TV**: Distribución de video
- **Fibra óptica**: Servicios metropolitanos

## 4. Estándares Ethernet a 100 Mbps (Fast Ethernet)

### Evolución hacia Fast Ethernet:

#### Limitaciones de 10 Mbps Ethernet:
- **Ancho de banda insuficiente**: Para aplicaciones multimedia
- **Colisiones frecuentes**: En redes congestionadas
- **Half-duplex**: Compartición del medio
- **Necesidad de más velocidad**: Aplicaciones demandantes

#### Desarrollo del estándar:
- **IEEE 802.3u (1995)**: Fast Ethernet estándar
- **Compatibilidad**: Con Ethernet 10 Mbps
- **Auto-negotiation**: Detección automática de velocidad
- **Full-duplex**: Eliminación de colisiones

### 100BASE-TX: Implementación sobre cobre

#### Especificaciones técnicas:
- **Velocidad**: 100 Mbps
- **Medio**: UTP Categoría 5 o superior
- **Pares utilizados**: 2 de 4 pares (1,2 y 3,6)
- **Codificación**: 4B5B + MLT-3
- **Distancia máxima**: 100 metros

#### Cableado 100BASE-TX:
```
Pin  T568A        T568B        Función
1    Blanco-Verde Blanco-Naranja TX+
2    Verde        Naranja      TX-
3    Blanco-Naranja Blanco-Verde RX+
6    Naranja      Verde        RX-
4,5  Azul         Azul         No usado
7,8  Café         Café         No usado
```

#### Características operacionales:
- **Topología**: Estrella con switch central
- **Duplex**: Half o full-duplex
- **Auto-MDI/MDI-X**: Detección automática en equipos modernos
- **Link integrity**: Verificación continua de conexión

### 100BASE-FX: Implementación sobre fibra óptica

#### Especificaciones técnicas:
- **Velocidad**: 100 Mbps
- **Medio**: Fibra óptica multimodo 62.5/125 µm
- **Longitud de onda**: 1300 nm
- **Codificación**: 4B5B + NRZI
- **Conectores**: SC, ST típicamente

#### Distancias:
- **Half-duplex**: 412 metros máximo
- **Full-duplex**: 2000 metros máximo
- **Diferencia**: Half-duplex limitado por collision domain

#### Ventajas sobre 100BASE-TX:
- **Distancias mayores**: Hasta 2 km vs 100m
- **Inmunidad EMI**: Sin interferencias electromagnéticas
- **Seguridad**: Difícil interceptación
- **Ancho de banda futuro**: Capacidad para upgrades

### Consideraciones de diseño para Fast Ethernet:

#### Migración desde 10 Mbps:
- **Cableado existente**: Verificar categoría
- **Equipos**: Actualización de switches
- **Compatibilidad**: Operación mixta 10/100
- **Fases**: Implementación gradual

#### Cableado estructurado para 100 Mbps:
- **Categoría mínima**: Cat 5 requerida
- **Certificación**: Pruebas hasta 100 MHz
- **Patch cords**: Categoría adecuada
- **Conectores**: RJ-45 calidad comercial

#### Consideraciones de rendimiento:
- **Colisiones**: Eliminadas con full-duplex switching
- **Latencia**: Reducida significativamente
- **Throughput**: Teórico 100 Mbps, práctico ~95 Mbps
- **Escalabilidad**: Base para Gigabit futuro

### Implementación práctica:

#### Equipos requeridos:
- **Fast Ethernet switches**: 100BASE-TX ports
- **NICs**: Tarjetas de red 100 Mbps
- **Media converters**: Para conexiones fibra
- **Cable testers**: Certificación Cat 5+

#### Configuración típica:
```
Workstation -> 100BASE-TX -> Switch -> 100BASE-FX -> Core
    Cat 5         100m        24-port    2km        Router
```

#### Best practices:
- **Full-duplex**: Siempre que sea posible
- **Switch per segment**: Eliminar hubs
- **Structured cabling**: Seguir TIA-568
- **Documentation**: Mantener registros actualizados

## Laboratorios Prácticos

### Lab 1: Diseño de cableado estructurado
1. **Análisis de requerimientos**: Para oficina pequeña
2. **Diseño de topología**: Ubicación de TCs y ERs
3. **Cálculo de materiales**: Cables, conectores, equipos
4. **Documentación**: Planos y especificaciones

### Lab 2: Instalación de patch panel
1. **Preparación de cables**: Strip y ordenamiento
2. **Terminación**: Técnica punch-down
3. **Pruebas**: Continuidad y certificación
4. **Etiquetado**: Sistema de identificación

### Lab 3: Certificación de enlaces
1. **Pruebas básicas**: Continuidad y wiremap
2. **Pruebas de rendimiento**: NEXT, atenuación, return loss
3. **Interpretación**: Análisis de resultados
4. **Documentación**: Reportes de certificación

### Lab 4: Configuración Fast Ethernet
1. **Instalación**: Switches y workstations
2. **Configuración**: Velocidad y duplex
3. **Pruebas de rendimiento**: Throughput real
4. **Troubleshooting**: Diagnóstico de problemas

## Evaluación

### Conocimientos teóricos:
1. **Estándares**: Conocimiento de TIA-568 y relacionados
2. **Componentes**: Función y especificaciones
3. **Diseño**: Principios de cableado estructurado
4. **Fast Ethernet**: Implementación y características

### Habilidades prácticas:
1. **Instalación**: Técnicas de terminación
2. **Pruebas**: Uso de equipos de certificación
3. **Documentación**: Planos y registros
4. **Troubleshooting**: Diagnóstico y solución

### Proyecto integrador:
Diseño completo de sistema de cableado estructurado para edificio de 3 pisos con 150 usuarios, incluyendo:
- Análisis de requerimientos
- Diseño de topología
- Especificación de componentes
- Presupuesto detallado
- Plan de implementación
- Sistema de documentación

## Recursos adicionales

### Documentación oficial:
- TIA-568-C.0/1/2 Standards
- ISO/IEC 11801 Standard
- Manufacturer installation guides
- Certification test procedures

### Herramientas de diseño:
- CAD software for floor plans
- Cable management calculators
- Distance calculation tools
- Documentation templates

### Capacitación:
- TIA certification programs
- Manufacturer training courses
- BICSI (Building Industry Consulting Service International)
- Installer certification programs

[⬅️ Anterior: Tipos de cables de red.](./TiposCables.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Construcción de cables. ➡️](./ConstruccionCables.md)