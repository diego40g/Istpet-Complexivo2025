# Actividad 5.1: Laboratorio de Virtualización con VirtualBox

## 🎯 Objetivo
Instalar y configurar VirtualBox para crear máquinas virtuales con diferentes sistemas operativos, experimentando con configuraciones de red, snapshots y clonación.

## 📋 Recursos necesarios
- Computadora con al menos 8GB RAM y 50GB de espacio libre
- Procesador con soporte para virtualización (VT-x/AMD-V)
- VirtualBox (gratuito)
- ISOs de sistemas operativos (Ubuntu, Windows, etc.)
- Acceso a Internet para descargas

## ⏱️ Duración estimada
4-6 horas

## 🔧 Prerrequisitos técnicos

### Verificar soporte de virtualización:
**Windows:**
```powershell
# En PowerShell como administrador
Get-ComputerInfo -Property "HyperV*"
```

**Linux:**
```bash
# Verificar soporte VT-x/AMD-V
grep -E "(vmx|svm)" /proc/cpuinfo

# Verificar si está habilitado
lscpu | grep Virtualization
```

**macOS:**
```bash
# Verificar soporte
sysctl kern.hv_support
```

## 📝 Pasos a seguir

### Paso 1: Instalación de VirtualBox

#### A. Descarga e instalación:

**Para Windows:**
```
1. Ve a virtualbox.org/wiki/Downloads
2. Descarga "VirtualBox for Windows hosts"
3. Ejecuta el instalador como administrador
4. Acepta configuración por defecto
5. Instala también "Extension Pack" (opcional pero recomendado)
```

**Para macOS:**
```
1. Descarga "VirtualBox for OS X hosts"
2. Abre el archivo .dmg descargado
3. Ejecuta VirtualBox.pkg
4. Sigue el asistente de instalación
5. Autoriza en Preferencias del Sistema si es necesario
```

**Para Linux (Ubuntu/Debian):**
```bash
# Actualizar paquetes
sudo apt update

# Instalar VirtualBox
sudo apt install virtualbox virtualbox-ext-pack

# Añadir usuario al grupo vboxusers
sudo usermod -aG vboxusers $USER

# Reiniciar sesión para aplicar cambios
```

#### B. Verificación de instalación:
```bash
# Verificar versión instalada
VBoxManage --version

# Listar VMs (debe estar vacío inicialmente)
VBoxManage list vms
```

### Paso 2: Configuración inicial de VirtualBox

#### A. Configuraciones globales:
```
1. Abrir VirtualBox Manager
2. File → Preferences (o Ctrl+G)
3. Configurar:
   - Default Machine Folder: Carpeta para VMs
   - Host key: Tecla para liberar mouse/teclado
   - Update: Configurar notificaciones
   - Network: Verificar adaptadores de red
```

#### B. Crear carpeta organizada:
```
Estructura recomendada:
C:\VirtualBox\
├── ISOs\
├── VMs\
│   ├── Ubuntu-Desktop\
│   ├── Windows-Test\
│   └── Snapshots\
└── Shared\
```

### Paso 3: Creación de primera VM (Ubuntu Desktop)

#### A. Descarga de ISO:
```
1. Ve a ubuntu.com/download/desktop
2. Descarga Ubuntu 22.04 LTS (recomendado)
3. Guarda en carpeta ISOs
```

#### B. Crear nueva VM:
```
En VirtualBox Manager:
1. Clic en "New" o Ctrl+N
2. Configurar:
   - Name: Ubuntu-22.04-Desktop
   - Type: Linux
   - Version: Ubuntu (64-bit)
   - Memory: 4096 MB (4GB)
   - Hard disk: Create virtual hard disk now

3. Configurar disco duro:
   - File type: VDI (VirtualBox Disk Image)
   - Storage: Dynamically allocated
   - Size: 25 GB
```

#### C. Configurar VM antes del primer inicio:
```
1. Seleccionar la VM creada
2. Clic en "Settings"
3. Configurar:

System:
- Boot Order: Optical, Hard Disk
- Enable EFI: Deshabilitado (para simplicidad)
- Processors: 2 CPUs

Display:
- Video Memory: 128 MB
- Enable 3D Acceleration: Checked
- Graphics Controller: VBoxSVGA

Storage:
- Controller IDE: Añadir disco óptico
- Seleccionar ISO de Ubuntu descargado

Audio:
- Enable Audio: Checked
- Host Audio Driver: Auto

Network:
- Adapter 1: NAT (por defecto)
- Enable Network Adapter: Checked
```

### Paso 4: Instalación de Ubuntu

#### A. Primer arranque:
```
1. Seleccionar VM y clic "Start"
2. Debería arrancar desde ISO de Ubuntu
3. Seleccionar "Try or Install Ubuntu"
4. Elegir idioma: Español (o preferido)
```

#### B. Proceso de instalación:
```
1. Configurar teclado: Spanish
2. Actualizaciones: Install Ubuntu (instalación normal)
3. Tipo de instalación: Erase disk and install Ubuntu
4. Crear usuario:
   - Name: Usuario Test
   - Computer name: ubuntu-vm
   - Username: test
   - Password: (elige una segura)
   - Auto-login: Optional

5. Comenzar instalación (toma 15-30 minutos)
6. Reiniciar cuando termine
```

#### C. Post-instalación:
```
Después del reinicio:
1. Login con usuario creado
2. Configurar updates si se solicita
3. Explorar el desktop Ubuntu

Remover ISO:
1. Settings → Storage
2. Seleccionar ISO en Controller IDE
3. Clic en disco óptico → Remove disk
```

### Paso 5: Instalación de Guest Additions

#### A. ¿Por qué Guest Additions?
- Mejor integración con host
- Resolución de pantalla dinámica
- Shared clipboard y drag & drop
- Carpetas compartidas
- Mejor rendimiento de video

#### B. Instalación en Ubuntu:
```
1. En la VM Ubuntu ejecutándose
2. VirtualBox menu: Devices → Insert Guest Additions CD
3. En Ubuntu, abrir terminal:

sudo apt update
sudo apt install build-essential dkms linux-headers-$(uname -r)

4. Montar CD de Guest Additions:
sudo mount /dev/cdrom /mnt
cd /mnt
sudo ./VBoxLinuxAdditions.run

5. Reiniciar la VM:
sudo reboot
```

#### C. Verificar instalación:
```
# Verificar que Guest Additions están instalados
VBoxControl --version

# En VirtualBox menu, verificar que están disponibles:
- View → Full-screen Mode
- Devices → Shared Clipboard → Bidirectional
- Devices → Drag and Drop → Bidirectional
```

### Paso 6: Configuraciones avanzadas de red

#### A. Tipos de adaptadores de red:

**NAT (Network Address Translation):**
```
- VM puede acceder a Internet
- VM no es accesible desde host
- Múltiples VMs pueden usar NAT simultáneamente
```

**Bridged Adapter:**
```
- VM obtiene IP en la misma red que host
- VM es accesible desde otros equipos en la red
- Útil para servidores o testing de red
```

**Host-only Adapter:**
```
- VM solo se comunica con host
- Útil para ambientes de desarrollo aislados
- Sin acceso a Internet
```

**Internal Network:**
```
- VMs se comunican entre sí
- Sin acceso a host ni Internet
- Útil para laboratorios de red
```

#### B. Configurar red Host-only:
```
1. VirtualBox Manager → File → Host Network Manager
2. Crear nueva red: Clic "Create"
   - Name: vboxnet0
   - IPv4 Address: 192.168.56.1
   - IPv4 Network Mask: 255.255.255.0
   - DHCP Server: Enable
   - Server Address: 192.168.56.100
   - Server Mask: 255.255.255.0
   - Lower Address Bound: 192.168.56.101
   - Upper Address Bound: 192.168.56.254

3. En Settings de VM:
   - Network → Adapter 2: Host-only Adapter
   - Name: vboxnet0
   - Enable Network Adapter: Checked
```

### Paso 7: Gestión de Snapshots

#### A. ¿Qué son los Snapshots?
- Capturas del estado completo de la VM
- Permiten volver a un estado anterior
- Útiles para testing y desarrollo
- Se pueden crear múltiples snapshots

#### B. Crear snapshot:
```
1. Con la VM ejecutándose o apagada
2. VirtualBox menu: Machine → Take Snapshot
3. Configurar:
   - Name: "Fresh Ubuntu Install"
   - Description: "Sistema recién instalado con Guest Additions"
4. Clic "OK"
```

#### C. Gestionar snapshots:
```
1. En VirtualBox Manager, seleccionar VM
2. Clic en "Snapshots" (junto a Details)
3. Opciones disponibles:
   - Take: Crear nuevo snapshot
   - Restore: Volver a snapshot seleccionado
   - Delete: Eliminar snapshot
   - Clone: Crear VM nueva desde snapshot
```

### Paso 8: Clonación de VMs

#### A. Crear clon de la VM:
```
1. Apagar la VM Ubuntu
2. Click derecho en la VM → Clone
3. Configurar:
   - Name: Ubuntu-22.04-Clone
   - Path: Default
   - MAC Address Policy: Generate new MAC addresses
   - Clone type: Full clone (recomendado)
   - Snapshots: Current machine state

4. Clic "Clone"
```

#### B. Verificar clon:
```
1. Iniciar la VM clonada
2. Verificar que funciona correctamente
3. Cambiar hostname para diferenciarlo:
   sudo hostnamectl set-hostname ubuntu-clone
4. Reiniciar para aplicar cambios
```

### Paso 9: Carpetas compartidas

#### A. Configurar carpeta compartida:
```
1. Crear carpeta en host: C:\VirtualBox\Shared
2. En Settings de VM: Shared Folders
3. Clic "Add new shared folder":
   - Folder Path: C:\VirtualBox\Shared
   - Folder Name: shared
   - Auto-mount: Checked
   - Make Permanent: Checked

4. Reiniciar VM
```

#### B. Acceder desde Ubuntu:
```
# La carpeta se monta automáticamente en:
ls -la /media/sf_shared

# Si no está accesible, añadir usuario al grupo:
sudo usermod -aG vboxsf $USER

# Logout y login nuevamente
# Crear enlace simbólico en home:
ln -s /media/sf_shared ~/shared
```

### Paso 10: Creación de VM Windows (opcional)

#### A. Requisitos:
```
- ISO de Windows 10/11 (evaluation version)
- Al menos 8GB RAM total en host
- 40GB espacio libre adicional
```

#### B. Configuración recomendada:
```
VM Settings:
- Name: Windows-10-Test
- Type: Microsoft Windows
- Version: Windows 10 (64-bit)
- Memory: 4096 MB
- Hard disk: 40 GB
- Video Memory: 256 MB
- Enable 3D Acceleration: Yes
- Processors: 2 CPUs
```

## 📤 Entregables

### 1. Documentación del laboratorio
**Informe detallado que incluya:**
- Screenshots de cada paso importante
- Configuraciones utilizadas
- Problemas encontrados y soluciones
- Comparación de rendimiento entre VMs

### 2. Capturas de pantalla obligatorias
**Screenshots que demuestren:**
- VirtualBox Manager con VMs creadas
- VM Ubuntu funcionando con Guest Additions
- Configuración de red Host-only funcionando
- Snapshots manager con al menos 2 snapshots
- Carpeta compartida funcionando
- VM clonada ejecutándose

### 3. Pruebas de funcionalidad
**Documenta las siguientes pruebas:**
- Conectividad de red entre VMs
- Transferencia de archivos via carpeta compartida
- Restauración desde snapshot
- Clonación exitosa de VM

### 4. Análisis comparativo
**Tabla comparando:**
- Consumo de recursos (RAM, CPU, disco)
- Tiempo de arranque de diferentes VMs
- Rendimiento de red en diferentes modos
- Ventajas/desventajas de cada configuración

### 5. Guía de troubleshooting
**Documenta soluciones para:**
- Problemas comunes encontrados
- Errores de configuración
- Issues de rendimiento
- Problemas de red y conectividad

## 🔍 Puntos de análisis

### Durante el laboratorio, analiza:

1. **Rendimiento:**
   - ¿Cómo afecta la virtualización al rendimiento del host?
   - ¿Qué configuraciones optimizan mejor el rendimiento?

2. **Casos de uso:**
   - ¿Cuándo es útil cada tipo de configuración de red?
   - ¿En qué escenarios son útiles los snapshots?

3. **Limitaciones:**
   - ¿Qué limitaciones tiene VirtualBox vs. otros hypervisors?
   - ¿Qué recursos son más críticos para las VMs?

4. **Seguridad:**
   - ¿Qué consideraciones de seguridad hay que tener?
   - ¿Cómo aislar adecuadamente las VMs?

## ✅ Criterios de evaluación

### Excelente (90-100%)
- Creación exitosa de múltiples VMs funcionando
- Configuración avanzada de red implementada
- Guest Additions instalado y configurado
- Snapshots y clonación funcionando
- Carpetas compartidas operativas
- Documentación completa con análisis profundo
- Troubleshooting documentado con soluciones

### Bueno (80-89%)
- VM Ubuntu funcionando correctamente
- Guest Additions instalado
- Configuración básica de red
- Al menos un snapshot creado
- Documentación clara y organizada
- Algunas pruebas de funcionalidad completadas

### Satisfactorio (70-79%)
- VM básica funcionando
- Instalación de SO exitosa
- Documentación mínima requerida
- Screenshots básicos incluidos
- Cumplimiento de requisitos fundamentales

## 💡 Tips para el éxito

### Mejores prácticas:
- **Habilita virtualización** en BIOS/UEFI antes de empezar
- **Asigna recursos moderadamente** - deja RAM suficiente para host
- **Usa discos dinámicos** para ahorrar espacio
- **Crea snapshots antes de cambios importantes**
- **Documenta cada configuración** que funcione bien

### Troubleshooting común:
- **VM muy lenta:** Verificar que VT-x/AMD-V está habilitado
- **No arranca ISO:** Verificar boot order en configuración
- **Guest Additions falla:** Instalar dependencias build-essential
- **Sin conectividad:** Verificar configuración de adaptador de red
- **No encuentra shared folder:** Verificar permisos y grupo vboxsf

### Optimización:
- **Deshabilita efectos visuales** innecesarios en VMs
- **Usa SSD** si está disponible para mejor rendimiento
- **Cierra aplicaciones innecesarias** en host
- **Monitorea uso de recursos** con htop/Task Manager
