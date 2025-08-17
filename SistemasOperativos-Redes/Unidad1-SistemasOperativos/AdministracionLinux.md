# Administración y Gestión de Sistemas Linux

## 1. Introducción a Linux

### Filosofía y conceptos clave de Linux

#### Filosofía del software libre
- **Libertad 0**: Usar el programa como se desee
- **Libertad 1**: Estudiar cómo funciona el programa y modificarlo
- **Libertad 2**: Redistribuir copias
- **Libertad 3**: Distribuir copias de versiones modificadas

#### Principios fundamentales:
- **"Todo es un archivo"**: Dispositivos, procesos y servicios se tratan como archivos
- **Herramientas pequeñas y especializadas**: Cada programa hace una cosa bien
- **Composición de herramientas**: Combinar programas simples para tareas complejas
- **Configuración mediante archivos de texto**: Fácil edición y automatización

### Características y diferencias con otros SO

#### Características principales de Linux:
- **Código abierto**: Disponible para estudio y modificación
- **Multiusuario y multitarea**: Soporte nativo para múltiples usuarios
- **Estabilidad**: Diseñado para funcionar continuamente
- **Seguridad**: Permisos granulares y arquitectura robusta
- **Personalización**: Altamente configurable
- **Portabilidad**: Funciona en múltiples arquitecturas

#### Diferencias con otros sistemas:
| Característica | Linux | Windows | macOS |
|----------------|--------|---------|-------|
| Código | Abierto | Cerrado | Cerrado |
| Costo | Gratuito | Licencia | Incluido con HW |
| Personalización | Alta | Media | Baja |
| Línea de comandos | Poderosa | Limitada | Potente |
| Seguridad | Muy alta | Media | Alta |

### Estructura de directorios (FHS - Filesystem Hierarchy Standard)

#### Directorios principales:
```
/               # Raíz del sistema de archivos
├── bin/        # Binarios esenciales del sistema
├── boot/       # Archivos del gestor de arranque
├── dev/        # Archivos de dispositivos
├── etc/        # Archivos de configuración del sistema
├── home/       # Directorios home de usuarios
├── lib/        # Bibliotecas compartidas esenciales
├── media/      # Puntos de montaje para medios removibles
├── mnt/        # Puntos de montaje temporales
├── opt/        # Software opcional
├── proc/       # Sistema de archivos virtual (procesos)
├── root/       # Directorio home del usuario root
├── run/        # Archivos de tiempo de ejecución
├── sbin/       # Binarios del sistema (superusuario)
├── srv/        # Datos de servicios del sistema
├── sys/        # Sistema de archivos virtual (kernel)
├── tmp/        # Archivos temporales
├── usr/        # Programas y archivos de usuarios
└── var/        # Archivos variables (logs, spools)
```

## 2. Distribuciones y versiones

### Las distribuciones más populares

#### Familias principales:

**Debian y derivados:**
- **Ubuntu**: Fácil de usar, gran comunidad
- **Debian**: Muy estable, base de muchas distros
- **Linux Mint**: Interfaz familiar para usuarios Windows

**Red Hat y derivados:**
- **Fedora**: Tecnologías cutting-edge
- **CentOS/Rocky Linux**: Versión comunitaria de RHEL
- **RHEL**: Soporte empresarial

**SUSE:**
- **openSUSE**: Herramientas avanzadas de administración
- **SLES**: Soporte empresarial

**Arch y derivados:**
- **Arch Linux**: Rolling release, personalización total
- **Manjaro**: Arch más amigable

### Instalación de distribuciones de escritorio

#### Proceso general de instalación:
1. **Preparación**:
   - Descargar imagen ISO
   - Crear medio de instalación (USB/DVD)
   - Verificar compatibilidad de hardware

2. **Instalación**:
   - Arrancar desde live USB/DVD
   - Probar el sistema antes de instalar
   - Particionar el disco
   - Configurar usuario y contraseña
   - Instalar gestor de arranque

3. **Post-instalación**:
   - Actualizar el sistema
   - Instalar controladores adicionales
   - Configurar software adicional

#### Ejemplo: Instalación de Ubuntu Desktop
```bash
# Verificar integridad de la imagen ISO
sha256sum ubuntu-22.04-desktop-amd64.iso

# Crear USB booteable (Linux)
sudo dd if=ubuntu-22.04-desktop-amd64.iso of=/dev/sdX bs=4M status=progress
```

### Instalación de distribuciones de servidor (Ubuntu Server, etc.)

#### Características de instalaciones de servidor:
- **Sin interfaz gráfica**: Solo línea de comandos
- **Servicios optimizados**: Configuración para servicios de red
- **Consumo mínimo de recursos**: Sin aplicaciones innecesarias
- **Administración remota**: SSH configurado por defecto

#### Proceso de instalación Ubuntu Server:
1. Arrancar desde ISO de servidor
2. Configurar idioma y teclado
3. Configurar red (IP estática/DHCP)
4. Configurar almacenamiento
5. Crear usuario administrativo
6. Instalar OpenSSH server
7. Seleccionar snaps adicionales

## 3. Administración del sistema

### Gestión de usuarios, grupos y permisos

#### Comandos para gestión de usuarios:
```bash
# Crear usuario
sudo useradd -m -s /bin/bash usuario

# Establecer contraseña
sudo passwd usuario

# Modificar usuario
sudo usermod -aG grupo usuario

# Eliminar usuario
sudo userdel -r usuario

# Listar usuarios
cat /etc/passwd
```

#### Comandos para gestión de grupos:
```bash
# Crear grupo
sudo groupadd nombre_grupo

# Agregar usuario a grupo
sudo usermod -aG grupo usuario

# Listar grupos
cat /etc/group

# Ver grupos de un usuario
groups usuario
```

#### Sistema de permisos:
```bash
# Formato: tipo propietario grupo otros
# rwxrwxrwx
# 421421421

# Cambiar permisos
chmod 755 archivo        # rwxr-xr-x
chmod u+x archivo        # Agregar ejecución al propietario
chmod g-w archivo        # Quitar escritura al grupo

# Cambiar propietario
chown usuario:grupo archivo
```

### Gestión de paquetes (apt, dnf, zypper)

#### APT (Advanced Package Tool) - Debian/Ubuntu:
```bash
# Actualizar lista de paquetes
sudo apt update

# Actualizar paquetes instalados
sudo apt upgrade

# Instalar paquete
sudo apt install nombre_paquete

# Buscar paquete
apt search término

# Mostrar información
apt show nombre_paquete

# Eliminar paquete
sudo apt remove nombre_paquete

# Eliminar paquete y configuraciones
sudo apt purge nombre_paquete

# Limpiar caché
sudo apt autoremove && sudo apt autoclean
```

#### DNF (Dandified YUM) - Fedora/RHEL:
```bash
# Actualizar sistema
sudo dnf update

# Instalar paquete
sudo dnf install nombre_paquete

# Buscar paquete
sudo dnf search término

# Información del paquete
sudo dnf info nombre_paquete

# Eliminar paquete
sudo dnf remove nombre_paquete

# Listar paquetes instalados
sudo dnf list installed
```

#### Zypper - openSUSE:
```bash
# Actualizar repositorios
sudo zypper refresh

# Actualizar sistema
sudo zypper update

# Instalar paquete
sudo zypper install nombre_paquete

# Buscar paquete
zypper search término

# Eliminar paquete
sudo zypper remove nombre_paquete
```

### Administración del sistema de archivos

#### Sistemas de archivos comunes:
- **ext4**: Sistema por defecto en la mayoría de distribuciones
- **XFS**: Alto rendimiento para archivos grandes
- **Btrfs**: Características avanzadas (snapshots, compresión)
- **ZFS**: Sistema de archivos y gestor de volúmenes

#### Comandos de administración:
```bash
# Ver información de discos
lsblk
fdisk -l

# Mostrar uso de espacio
df -h
du -sh directorio

# Montar sistema de archivos
sudo mount /dev/sdb1 /mnt/punto_montaje

# Desmontar
sudo umount /mnt/punto_montaje

# Editar tabla de montaje permanente
sudo nano /etc/fstab
```

## 4. La línea de comandos de Linux (Bash)

### Comandos básicos y utilidades

#### Navegación y exploración:
```bash
pwd                 # Mostrar directorio actual
ls                  # Listar archivos
ls -la              # Listado detallado incluyendo ocultos
cd directorio       # Cambiar directorio
cd ..               # Directorio padre
cd ~                # Directorio home
```

#### Manipulación de archivos y directorios:
```bash
mkdir directorio    # Crear directorio
mkdir -p ruta/completa/directorio  # Crear estructura completa
rmdir directorio    # Eliminar directorio vacío
rm archivo          # Eliminar archivo
rm -rf directorio   # Eliminar directorio y contenido
cp origen destino   # Copiar archivo
cp -r origen destino # Copiar directorio
mv origen destino   # Mover/renombrar
```

#### Visualización y edición:
```bash
cat archivo         # Mostrar contenido completo
less archivo        # Mostrar contenido página por página
head archivo        # Mostrar primeras líneas
tail archivo        # Mostrar últimas líneas
tail -f archivo     # Seguir archivo en tiempo real
grep patrón archivo # Buscar patrón en archivo
find /ruta -name "*.txt"  # Buscar archivos
```

### Gestión de procesos y servicios

#### Gestión de procesos:
```bash
ps                  # Mostrar procesos actuales
ps aux              # Mostrar todos los procesos
top                 # Monitor de procesos en tiempo real
htop                # Monitor mejorado (si está instalado)
kill PID            # Terminar proceso por ID
killall nombre      # Terminar procesos por nombre
nohup comando &     # Ejecutar comando en segundo plano
```

#### Gestión de servicios (systemd):
```bash
# Ver estado de servicio
systemctl status nombre_servicio

# Iniciar servicio
sudo systemctl start nombre_servicio

# Detener servicio
sudo systemctl stop nombre_servicio

# Reiniciar servicio
sudo systemctl restart nombre_servicio

# Habilitar servicio al inicio
sudo systemctl enable nombre_servicio

# Deshabilitar servicio
sudo systemctl disable nombre_servicio

# Listar todos los servicios
systemctl list-units --type=service
```

## Laboratorios Prácticos

### Laboratorio 1: Instalación de Linux
1. Instalar Ubuntu Desktop en máquina virtual
2. Configurar usuario y permisos
3. Instalar software básico

### Laboratorio 2: Administración básica
1. Crear usuarios y grupos
2. Configurar permisos de archivos
3. Instalar software mediante línea de comandos

### Laboratorio 3: Servicios del sistema
1. Instalar y configurar servidor web (Apache/Nginx)
2. Configurar servicio SSH
3. Monitorear logs del sistema

## Scripts de ejemplo

### Script básico de backup:
```bash
#!/bin/bash
# Script de backup básico

ORIGEN="/home/usuario/documentos"
DESTINO="/backup/$(date +%Y%m%d)"

mkdir -p $DESTINO
cp -r $ORIGEN $DESTINO

echo "Backup completado: $(date)"
```

### Script de monitoreo del sistema:
```bash
#!/bin/bash
# Monitoreo básico del sistema

echo "=== Estado del Sistema ==="
echo "Fecha: $(date)"
echo "Uptime: $(uptime)"
echo "Uso de disco:"
df -h
echo "Memoria:"
free -h
echo "Procesos principales:"
ps aux --sort=-%cpu | head -10
```

## Actividades de Evaluación

1. **Práctica**: Instalar y configurar distribución Linux
2. **Scripting**: Crear scripts de administración básica
3. **Investigación**: Comparar diferentes distribuciones
4. **Proyecto**: Configurar servidor básico con servicios esenciales

## Recursos Adicionales

- Manual de comandos Linux (man pages)
- Tutoriales de Bash scripting
- Documentación oficial de distribuciones
- Certificaciones Linux (LPIC, Red Hat)

[⬅️ Anterior: Administración y Gestión de Sistemas Windows.](AdministracionWindows.md) | [Volver al índice](../TablaDeContenidos.md) | [Siguiente: Administración y Gestión de macOS. ➡️](AdministracionMacOS.md)