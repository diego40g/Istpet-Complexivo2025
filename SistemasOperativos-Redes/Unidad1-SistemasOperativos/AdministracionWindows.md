# Administración y Gestión de Sistemas Windows

## 1. Introducción a Windows

### Historia, características y versiones

#### Historia de Windows
- **1985**: Windows 1.0 - Primera versión con interfaz gráfica
- **1990**: Windows 3.0 - Primer éxito comercial
- **1995**: Windows 95 - Introducción del botón Inicio
- **2001**: Windows XP - Mayor estabilidad basada en NT
- **2007**: Windows Vista - Nuevas características de seguridad
- **2009**: Windows 7 - Refinamiento y mejora del rendimiento
- **2012**: Windows 8 - Diseño para dispositivos táctiles
- **2015**: Windows 10 - Actualizaciones continuas
- **2021**: Windows 11 - Interfaz renovada y nuevos requisitos

#### Características principales
- **Interfaz gráfica intuitiva**: Escritorio, ventanas, menús
- **Multitarea preemptiva**: Gestión eficiente de procesos
- **Plug and Play**: Detección automática de hardware
- **Administración de usuarios**: Control de acceso y permisos
- **Compatibilidad**: Amplio soporte de aplicaciones y hardware

### Arquitectura y estructura del sistema

#### Arquitectura de Windows (basada en NT)
1. **Modo Usuario**:
   - Aplicaciones de usuario
   - Subsistemas del entorno
   - DLLs (Dynamic Link Libraries)

2. **Modo Kernel**:
   - Executive Services
   - Kernel de Windows
   - HAL (Hardware Abstraction Layer)
   - Controladores de dispositivos

#### Componentes clave:
- **Registry**: Base de datos de configuración
- **Servicios**: Procesos que se ejecutan en segundo plano
- **Procesos**: Instancias de programas en ejecución
- **Hilos**: Unidades básicas de ejecución

## 2. Instalación y configuración

### Proceso de instalación de Windows de escritorio

#### Requisitos del sistema (Windows 11)
- **Procesador**: 1 GHz o más rápido con 2 o más núcleos
- **RAM**: 4 GB para 64 bits
- **Almacenamiento**: 64 GB o más
- **Firmware del sistema**: UEFI, compatible con Arranque seguro
- **TPM**: Módulo de plataforma segura (TPM) versión 2.0

#### Pasos de instalación:
1. **Preparación**:
   - Crear medio de instalación (USB/DVD)
   - Verificar requisitos del sistema
   - Respaldar datos importantes

2. **Instalación**:
   - Arrancar desde el medio de instalación
   - Seleccionar idioma y configuración regional
   - Aceptar términos de licencia
   - Elegir tipo de instalación (limpia/actualización)
   - Particionar el disco duro
   - Completar la instalación

### Configuración inicial y personalización

#### Configuración inicial:
- **Cuentas de usuario**: Crear cuenta local o Microsoft
- **Configuración de red**: WiFi o Ethernet
- **Actualizaciones**: Instalar actualizaciones críticas
- **Configuración de privacidad**: Ajustar opciones de telemetría

#### Personalización:
- **Escritorio**: Fondos de pantalla, temas
- **Barra de tareas**: Organización de íconos
- **Menú Inicio**: Personalizar tiles y aplicaciones
- **Configuración regional**: Zona horaria, idioma

## 3. Administración del sistema

### Gestión de usuarios y permisos

#### Tipos de cuentas:
- **Administrador**: Control completo del sistema
- **Usuario estándar**: Acceso limitado
- **Invitado**: Acceso temporal y restringido

#### Herramientas de gestión:
- **Panel de Control**: Interfaz tradicional
- **Configuración**: Interfaz moderna
- **Computer Management**: Herramienta avanzada
- **Local Users and Groups**: Gestión detallada

#### Permisos de archivos:
- **Lectura**: Ver contenido
- **Escritura**: Modificar archivos
- **Ejecución**: Ejecutar programas
- **Control total**: Todos los permisos

### Administración de archivos y discos

#### Sistema de archivos:
- **NTFS**: Sistema principal de Windows
  - Soporte para archivos grandes
  - Permisos granulares
  - Cifrado y compresión
- **FAT32**: Para dispositivos removibles
- **exFAT**: Para dispositivos de gran capacidad

#### Herramientas de gestión:
- **Explorador de archivos**: Navegación básica
- **Disk Management**: Gestión de particiones
- **Disk Cleanup**: Limpieza de archivos temporales
- **Defragmenter**: Optimización del disco

### Introducción a los comandos de consola (CMD y PowerShell)

#### Command Prompt (CMD)
Comandos básicos:
```cmd
dir          # Listar archivos y carpetas
cd           # Cambiar directorio
mkdir        # Crear directorio
copy         # Copiar archivos
del          # Eliminar archivos
type         # Mostrar contenido de archivo
systeminfo   # Información del sistema
```

#### PowerShell
Comandos básicos (cmdlets):
```powershell
Get-ChildItem    # Listar elementos
Set-Location     # Cambiar ubicación
New-Item         # Crear elemento
Copy-Item        # Copiar elemento
Remove-Item      # Eliminar elemento
Get-Content      # Mostrar contenido
Get-ComputerInfo # Información del equipo
```

## 4. Windows Server

### Características y roles de Windows Server

#### Características principales:
- **Escalabilidad**: Soporte para múltiples usuarios
- **Seguridad avanzada**: Active Directory, políticas de grupo
- **Servicios de red**: DNS, DHCP, IIS
- **Virtualización**: Hyper-V
- **Administración remota**: Herramientas centralizadas

#### Roles principales:
- **Domain Controller**: Autenticación y autorización
- **File Server**: Compartición de archivos
- **Web Server (IIS)**: Servidor web
- **DNS Server**: Resolución de nombres
- **DHCP Server**: Asignación de direcciones IP

### Instalación y configuración básica

#### Opciones de instalación:
- **Server Core**: Sin interfaz gráfica (CLI únicamente)
- **Server with Desktop Experience**: Con interfaz gráfica completa

#### Configuración inicial:
1. Configurar red y nombre del servidor
2. Unirse a dominio o crear grupo de trabajo
3. Activar Windows Server
4. Instalar actualizaciones
5. Configurar roles y características

### Herramientas de administración

#### Herramientas principales:
- **Server Manager**: Administración centralizada
- **Administrative Tools**: Herramientas especializadas
- **PowerShell**: Automatización y scripting
- **Remote Desktop**: Acceso remoto
- **Windows Admin Center**: Administración basada en web

## Laboratorios Prácticos

### Laboratorio 1: Instalación de Windows
1. Crear máquina virtual
2. Instalar Windows desde ISO
3. Configuración inicial del sistema

### Laboratorio 2: Administración básica
1. Crear usuarios y grupos
2. Configurar permisos de archivos
3. Instalar software mediante línea de comandos

### Laboratorio 3: Windows Server
1. Instalar Windows Server en VM
2. Configurar roles básicos (DNS, DHCP)
3. Crear dominio Active Directory

## Actividades de Evaluación

1. **Práctica**: Instalar y configurar Windows en máquina virtual
2. **Investigación**: Comparar versiones de Windows Server
3. **Ejercicio**: Crear script de PowerShell para administración básica

## Recursos Adicionales

- Documentación oficial de Microsoft
- Tutoriales de PowerShell
- Guías de Windows Server
- Certificaciones Microsoft (MCSA, MCSE)

[⬅️ Anterior: Fundamentos de los Sistemas Operativos.](FundamentosSistemasOperativos.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Administración y Gestión de Sistemas Linux. ➡️](AdministracionLinux.md)