# Fundamentos de los Sistemas Operativos

## 1. ¿Qué es un Sistema Operativo?

### Definición y evolución histórica

Un Sistema Operativo (SO) es un software fundamental que actúa como intermediario entre el hardware de la computadora y los programas de aplicación. Su función principal es gestionar los recursos del sistema y proporcionar una interfaz para que los usuarios puedan interactuar con la máquina.

**Evolución histórica:**
- **Década de 1940**: Los primeros computadores no tenían SO, se programaban directamente en lenguaje máquina
- **Década de 1950**: Aparecen los primeros sistemas de procesamiento por lotes (batch processing)
- **Década de 1960**: Desarrollo de sistemas de tiempo compartido y multiprogramación
- **Década de 1970**: Nacimiento de UNIX, base de muchos SO modernos
- **Década de 1980**: Aparición de interfaces gráficas y SO para computadoras personales
- **Década de 1990-2000**: Desarrollo de SO distribuidos y para dispositivos móviles

### Componentes principales de un SO

1. **Kernel (Núcleo)**: El corazón del sistema operativo
   - Gestión de procesos
   - Gestión de memoria
   - Gestión de dispositivos de E/S
   - Sistema de archivos

2. **Shell**: Interfaz de línea de comandos o gráfica

3. **Utilidades del sistema**: Herramientas para administración y mantenimiento

4. **Controladores de dispositivos**: Software que permite al SO comunicarse con el hardware

### Arquitecturas y estructuras de los SO

1. **Arquitectura monolítica**
   - Todo el SO funciona en modo kernel
   - Ejemplos: MS-DOS, primeras versiones de UNIX

2. **Arquitectura de microkernel**
   - Kernel mínimo con servicios básicos
   - Servicios adicionales ejecutan en espacio de usuario
   - Ejemplos: QNX, L4

3. **Arquitectura híbrida**
   - Combina elementos de ambas arquitecturas
   - Ejemplos: Windows NT, macOS

4. **Arquitectura de capas**
   - SO organizado en capas jerárquicas
   - Cada capa utiliza servicios de la capa inferior

## 2. Clasificación y tipos de SO

### Criterios de clasificación

#### Por número de usuarios:
- **Monousuario**: Permiten un solo usuario a la vez (MS-DOS)
- **Multiusuario**: Permiten múltiples usuarios simultáneos (UNIX, Linux)

#### Por número de tareas:
- **Monotarea**: Ejecutan una sola tarea a la vez (MS-DOS)
- **Multitarea**: Pueden ejecutar múltiples tareas simultáneamente (Windows, Linux)

#### Por número de procesadores:
- **Monoproceso**: Diseñados para un solo procesador
- **Multiproceso**: Pueden utilizar múltiples procesadores o núcleos

### SO de escritorio vs. SO de servidor

#### Sistemas Operativos de Escritorio:
- **Características**:
  - Interfaz gráfica amigable
  - Optimizados para un solo usuario
  - Soporte para multimedia
  - Facilidad de uso
- **Ejemplos**: Windows 10/11, macOS, Ubuntu Desktop

#### Sistemas Operativos de Servidor:
- **Características**:
  - Optimizados para múltiples usuarios
  - Mayor estabilidad y seguridad
  - Herramientas de administración remota
  - Soporte para servicios de red
- **Ejemplos**: Windows Server, Ubuntu Server, Red Hat Enterprise Linux

### SO para dispositivos móviles

#### Características principales:
- Gestión eficiente de batería
- Interfaz táctil
- Conectividad inalámbrica
- Gestión de aplicaciones

#### Principales SO móviles:
- **Android**: Basado en Linux, desarrollado por Google
- **iOS**: Desarrollado por Apple para dispositivos iPhone/iPad
- **HarmonyOS**: Desarrollado por Huawei

## Actividades de Refuerzo

1. **Investigación**: Investiga sobre la evolución de un SO específico (Windows, macOS o Linux)
2. **Práctica**: Identifica los componentes del SO en tu computadora
3. **Comparación**: Realiza una tabla comparativa entre SO de escritorio y servidor

## Glosario

- **Kernel**: Núcleo del sistema operativo
- **Shell**: Intérprete de comandos
- **Driver**: Controlador de dispositivo
- **Multiprogramación**: Capacidad de ejecutar múltiples programas
- **Tiempo compartido**: División del tiempo de CPU entre múltiples usuarios

 | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Administración y Gestión de Sistemas Windows. ➡️](AdministracionWindows.md)