# Administración y Gestión de macOS

## 1. Introducción a macOS

### Historia y características únicas

#### Historia de macOS
- **1984**: System 1 (Macintosh System Software)
- **1991**: System 7 - Multitarea cooperativa
- **2001**: Mac OS X - Basado en UNIX (Darwin)
- **2012**: OS X Mountain Lion - Integración con iOS
- **2016**: macOS Sierra - Cambio de nombre
- **2020**: macOS Big Sur - Transición a Apple Silicon
- **2023**: macOS Sonoma - Versión actual

#### Características únicas de macOS:
- **Basado en UNIX**: Darwin como núcleo
- **Integración del ecosistema**: Continuidad con dispositivos Apple
- **Diseño centrado en el usuario**: Interfaz intuitiva y elegante
- **Seguridad por diseño**: Gatekeeper, System Integrity Protection
- **Optimización de hardware**: Diseñado específicamente para Mac
- **Compatibilidad universal**: Soporte para aplicaciones Intel y Apple Silicon

### Arquitectura (UNIX-based)

#### Estructura de capas:
1. **Hardware**: Procesadores Intel x86-64 y Apple Silicon (ARM64)
2. **Darwin (Kernel)**:
   - XNU kernel (híbrido)
   - BSD layer
   - Mach microkernel
3. **Core Services**:
   - Core Foundation
   - Core Data
   - Core Graphics
4. **Application Frameworks**:
   - Cocoa (Objective-C/Swift)
   - Carbon (legacy)
5. **Aqua (User Interface)**: Interfaz gráfica

#### Componentes del sistema:
- **Finder**: Explorador de archivos y escritorio
- **Dock**: Barra de aplicaciones
- **Menu Bar**: Barra de menú superior
- **Spotlight**: Sistema de búsqueda
- **Mission Control**: Gestión de espacios y ventanas

## 2. Administración y personalización

### Configuración y ajustes del sistema

#### System Preferences/System Settings (macOS 13+):

**General**:
- Apariencia (claro, oscuro, automático)
- Color de acento
- Comportamiento de barras de desplazamiento

**Desktop & Screen Saver**:
- Fondos de pantalla dinámicos
- Protectores de pantalla
- Hot corners

**Dock & Menu Bar**:
- Tamaño y posición del Dock
- Magnification y efectos
- Configuración de la barra de menú

**Security & Privacy**:
- FileVault (cifrado de disco)
- Firewall
- Privacy settings
- Gatekeeper settings

**Users & Groups**:
- Gestión de cuentas de usuario
- Configuración de login items
- Parental controls

#### Configuraciones avanzadas:
```bash
# Mostrar archivos ocultos en Finder
defaults write com.apple.finder AppleShowAllFiles -bool true
killall Finder

# Cambiar formato de captura de pantalla
defaults write com.apple.screencapture type -string "png"

# Desactivar animaciones del Dock
defaults write com.apple.dock launchanim -bool false
killall Dock
```

### Gestión de aplicaciones

#### Formas de instalar aplicaciones:

**Mac App Store**:
- Aplicaciones verificadas por Apple
- Actualizaciones automáticas
- Sandboxed para mayor seguridad

**Archivos .dmg (Disk Images)**:
- Descargar desde sitios web de desarrolladores
- Montar imagen y copiar aplicación a Applications
- Verificar firma digital

**Homebrew (Package Manager)**:
```bash
# Instalar Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Instalar aplicaciones
brew install --cask google-chrome
brew install git
```

**Instaladores .pkg**:
- Instaladores que modifican el sistema
- Requieren contraseña de administrador
- Seguir asistente de instalación

#### Gestión de aplicaciones:
- **Activity Monitor**: Monitor de procesos y recursos
- **Console**: Visualización de logs del sistema
- **System Information**: Información detallada del hardware
- **Terminal**: Acceso a línea de comandos

## 3. La Terminal de macOS

### Comandos esenciales y uso de la terminal

#### Comandos básicos (similar a Linux):
```bash
# Navegación
pwd                 # Directorio actual
ls                  # Listar archivos
ls -la              # Listado detallado
cd directorio       # Cambiar directorio

# Manipulación de archivos
mkdir directorio    # Crear directorio
cp archivo destino  # Copiar archivo
mv archivo destino  # Mover/renombrar
rm archivo          # Eliminar archivo

# Información del sistema
uname -a           # Información del kernel
sw_vers            # Versión de macOS
system_profiler    # Información detallada del hardware
```

#### Comandos específicos de macOS:
```bash
# Abrir aplicaciones
open /Applications/Safari.app
open archivo.pdf    # Abrir con aplicación por defecto
open .              # Abrir Finder en directorio actual

# Gestión de volúmenes
diskutil list       # Listar discos y particiones
diskutil info /     # Información del disco

# Configuración del sistema
pmset -g           # Configuración de energía
scutil --get ComputerName  # Nombre del equipo
networksetup -listallhardwareports  # Interfaces de red

# Spotlight desde terminal
mdfind "término de búsqueda"

# Gestión de servicios (launchctl)
launchctl list     # Servicios cargados
sudo launchctl load /path/to/service.plist
```

#### Herramientas de desarrollo:
```bash
# Xcode Command Line Tools
xcode-select --install

# Git (incluido en Command Line Tools)
git --version

# Compiladores
gcc --version
clang --version

# Python (pre-instalado)
python3 --version
```

### Automatización con scripts

#### Scripts básicos en Bash:
```bash
#!/bin/bash
# Script de backup automático

# Variables
ORIGEN="$HOME/Documents"
DESTINO="$HOME/Backups/$(date +%Y-%m-%d)"

# Crear directorio de backup
mkdir -p "$DESTINO"

# Realizar backup
cp -R "$ORIGEN" "$DESTINO"

# Notificación
osascript -e 'display notification "Backup completado" with title "Sistema de Backup"'

echo "Backup completado: $(date)"
```

#### AppleScript (específico de macOS):
```applescript
-- Script para automatizar tareas de macOS
tell application "System Events"
    -- Tomar captura de pantalla
    key code 20 using {command down, shift down}
    delay 2
    
    -- Abrir aplicación
    tell application "TextEdit" to activate
end tell

-- Mostrar notificación
display notification "Tarea completada" with title "Automation Script"
```

#### Automator:
- **Workflows**: Secuencias de acciones automatizadas
- **Services**: Acciones disponibles desde menús contextuales
- **Applications**: Aplicaciones standalone
- **Folder Actions**: Acciones que se ejecutan al modificar carpetas

#### Ejemplo de workflow básico:
1. Crear nuevo workflow en Automator
2. Agregar acción "Get Selected Finder Items"
3. Agregar acción "Copy Finder Items"
4. Especificar destino
5. Guardar como Application

### Programación con Swift (opcional):
```swift
#!/usr/bin/swift
import Foundation

// Script básico en Swift
print("Hello, macOS!")

// Ejecutar comando del sistema
let task = Process()
task.launchPath = "/bin/ls"
task.arguments = ["-la"]
task.launch()
task.waitUntilExit()
```

## Administración avanzada

### Gestión de usuarios y permisos:
```bash
# Crear usuario (requiere interfaz gráfica o sysadminctl)
sudo sysadminctl -addUser usuario -fullName "Nombre Completo" -password -

# Cambiar permisos
chmod 755 archivo
chown usuario:grupo archivo

# Gestión de grupos
sudo dscl . -create /Groups/gruponuevo
sudo dscl . -append /Groups/gruponuevo GroupMembership usuario
```

### Configuración de red:
```bash
# Ver configuración de red
networksetup -listallhardwareports
networksetup -getinfo "Wi-Fi"

# Configurar DNS
sudo networksetup -setdnsservers "Wi-Fi" 8.8.8.8 8.8.4.4

# Ver conexiones activas
netstat -an
lsof -i
```

### Mantenimiento del sistema:
```bash
# Limpiar caché
sudo rm -rf /Library/Caches/*
sudo rm -rf ~/Library/Caches/*

# Verificar y reparar permisos (versiones anteriores)
sudo diskutil verifyVolume /
sudo diskutil repairVolume /

# First Aid en versiones recientes
sudo /usr/libexec/mdutil -E /
```

## Laboratorios Prácticos

### Laboratorio 1: Configuración básica
1. Personalizar preferencias del sistema
2. Configurar usuarios y grupos
3. Instalar aplicaciones mediante diferentes métodos

### Laboratorio 2: Terminal y scripting
1. Dominar comandos básicos de Terminal
2. Crear scripts de automatización básicos
3. Usar Automator para workflows

### Laboratorio 3: Administración del sistema
1. Monitorear recursos del sistema
2. Configurar servicios de red
3. Implementar estrategias de backup

## Herramientas útiles

### Aplicaciones de terceros:
- **iTerm2**: Terminal mejorado
- **Homebrew**: Gestor de paquetes
- **BetterTouchTool**: Personalización de gestos
- **CleanMyMac**: Limpieza y optimización
- **Disk Utility**: Gestión de discos (incluido en macOS)

### Línea de comandos:
- **brew**: Gestor de paquetes
- **mas**: Mac App Store CLI
- **tmux**: Multiplexor de terminal
- **htop**: Monitor de procesos mejorado

## Actividades de Evaluación

1. **Configuración**: Personalizar completamente un macOS
2. **Automatización**: Crear workflow complejo con Automator
3. **Scripting**: Desarrollar script de administración en Bash/AppleScript
4. **Investigación**: Comparar macOS con otros sistemas UNIX

## Recursos Adicionales

- Documentación oficial de Apple Developer
- Guías de AppleScript
- Tutoriales de Automator
- Comunidad de Homebrew
- Manuales de Terminal y comandos UNIX

## Certificaciones relevantes

- Apple Certified Support Professional (ACSP)
- Apple Certified Technical Coordinator (ACTC)
- Certificaciones de desarrollo iOS/macOS

[⬅️ Anterior: Administración y Gestión de Sistemas Linux.](AdministracionLinux.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Introducción a las redes de computadoras. ➡️](../Unidad2-RedesDeComunicaciones/IntroduccionRedes.md)