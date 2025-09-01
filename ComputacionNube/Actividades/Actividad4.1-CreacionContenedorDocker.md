# Actividad 4.1: Creación y Despliegue de un Contenedor Docker Simple

## 🎯 Objetivo
Crear, construir y desplegar una aplicación web simple usando Docker para comprender los fundamentos de la contenedorización y su aplicación práctica.

## 📋 Recursos necesarios
- Computadora con Docker Desktop instalado (Windows/Mac) o Docker Engine (Linux)
- Editor de código (VS Code, Sublime Text, etc.)
- Navegador web
- Terminal/Command Prompt

## ⏱️ Duración estimada
3-4 horas

## 📝 Pasos a seguir

### Paso 1: Instalación y configuración de Docker

#### A. Instalación según tu sistema operativo:

**Para Windows:**
```bash
1. Descarga Docker Desktop desde docker.com/products/docker-desktop
2. Ejecuta el instalador
3. Reinicia cuando sea necesario
4. Abre Docker Desktop y completa setup inicial
5. Verifica instalación: docker --version
```

**Para macOS:**
```bash
1. Descarga Docker Desktop para Mac desde docker.com
2. Arrastra Docker.app a Applications
3. Ejecuta Docker desde Applications
4. Verifica instalación: docker --version
```

**Para Linux (Ubuntu/Debian):**
```bash
# Actualizar paquetes
sudo apt update

# Instalar dependencias
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# Añadir clave GPG de Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Añadir repositorio Docker
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Instalar Docker
sudo apt update
sudo apt install docker-ce

# Verificar instalación
docker --version

# Añadir usuario al grupo docker (opcional)
sudo usermod -aG docker $USER
```

#### B. Verificación de la instalación:
```bash
# Verificar versión
docker --version

# Ejecutar contenedor de prueba
docker run hello-world

# Ver imágenes descargadas
docker images

# Ver contenedores ejecutándose
docker ps
```

### Paso 2: Creación de aplicación web simple

#### A. Estructura del proyecto:
```
mi-app-docker/
├── app.js
├── package.json
├── Dockerfile
├── .dockerignore
└── public/
    ├── index.html
    └── style.css
```

#### B. Crear directorio del proyecto:
```bash
mkdir mi-app-docker
cd mi-app-docker
```

#### C. Crear package.json:
```json
{
  "name": "mi-app-docker",
  "version": "1.0.0",
  "description": "Aplicación web simple para aprender Docker",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": ["docker", "nodejs", "web"],
  "author": "Tu Nombre",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.2"
  }
}
```

#### D. Crear app.js (servidor Node.js):
```javascript
const express = require('express');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;

// Servir archivos estáticos
app.use(express.static('public'));

// Ruta principal
app.get('/', (req, res) => {
    res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// Ruta API simple
app.get('/api/info', (req, res) => {
    res.json({
        message: '¡Hola desde Docker!',
        timestamp: new Date().toISOString(),
        hostname: require('os').hostname(),
        platform: process.platform,
        nodeVersion: process.version
    });
});

// Ruta de salud
app.get('/health', (req, res) => {
    res.status(200).json({
        status: 'OK',
        uptime: process.uptime(),
        timestamp: new Date().toISOString()
    });
});

app.listen(PORT, '0.0.0.0', () => {
    console.log(`Servidor ejecutándose en puerto ${PORT}`);
    console.log(`Hostname: ${require('os').hostname()}`);
});
```

#### E. Crear public/index.html:
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi App Docker</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>🐳 Mi Aplicación Docker</h1>
        <p>¡Bienvenido a mi primera aplicación contenerizada!</p>
        
        <div class="info-section">
            <h2>Información del Contenedor</h2>
            <div id="info-container">
                <button onclick="obtenerInfo()">Obtener Info del Servidor</button>
                <pre id="info-display"></pre>
            </div>
        </div>
        
        <div class="features">
            <h2>Características de esta aplicación:</h2>
            <ul>
                <li>✅ Servidor Node.js con Express</li>
                <li>✅ Contenedor Docker optimizado</li>
                <li>✅ API REST simple</li>
                <li>✅ Interfaz web responsiva</li>
                <li>✅ Health check endpoint</li>
            </ul>
        </div>
    </div>

    <script>
        async function obtenerInfo() {
            try {
                const response = await fetch('/api/info');
                const data = await response.json();
                document.getElementById('info-display').textContent = JSON.stringify(data, null, 2);
            } catch (error) {
                document.getElementById('info-display').textContent = 'Error: ' + error.message;
            }
        }

        // Obtener info automáticamente al cargar
        window.onload = obtenerInfo;
    </script>
</body>
</html>
```

#### F. Crear public/style.css:
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
    padding: 20px;
}

.container {
    max-width: 800px;
    margin: 0 auto;
    background: white;
    padding: 40px;
    border-radius: 15px;
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
}

h1 {
    color: #2c3e50;
    text-align: center;
    margin-bottom: 30px;
    font-size: 2.5em;
}

h2 {
    color: #3498db;
    margin: 30px 0 15px 0;
    border-bottom: 2px solid #ecf0f1;
    padding-bottom: 10px;
}

p {
    color: #7f8c8d;
    font-size: 1.2em;
    text-align: center;
    margin-bottom: 30px;
}

.info-section {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 10px;
    margin: 20px 0;
}

button {
    background: #3498db;
    color: white;
    border: none;
    padding: 12px 24px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 16px;
    transition: background 0.3s;
}

button:hover {
    background: #2980b9;
}

#info-display {
    background: #2c3e50;
    color: #ecf0f1;
    padding: 15px;
    border-radius: 5px;
    margin-top: 15px;
    font-family: 'Courier New', monospace;
    overflow-x: auto;
    min-height: 100px;
}

.features {
    margin-top: 30px;
}

.features ul {
    list-style: none;
}

.features li {
    padding: 10px 0;
    font-size: 1.1em;
    color: #2c3e50;
}

@media (max-width: 600px) {
    .container {
        padding: 20px;
    }
    
    h1 {
        font-size: 2em;
    }
}
```

### Paso 3: Creación del Dockerfile

#### A. Crear Dockerfile:
```dockerfile
# Usar imagen oficial de Node.js como base
FROM node:18-alpine

# Establecer el directorio de trabajo en el contenedor
WORKDIR /app

# Copiar archivos de dependencias
COPY package*.json ./

# Instalar dependencias
RUN npm install --only=production

# Copiar código fuente de la aplicación
COPY . .

# Crear usuario no-root para seguridad
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001

# Cambiar ownership de archivos
RUN chown -R nodejs:nodejs /app
USER nodejs

# Exponer el puerto que usa la aplicación
EXPOSE 3000

# Configurar health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD node -e "require('http').get('http://localhost:3000/health', (res) => { \
        process.exit(res.statusCode === 200 ? 0 : 1) \
    }).on('error', () => process.exit(1))"

# Comando para ejecutar la aplicación
CMD ["npm", "start"]
```

#### B. Crear .dockerignore:
```
node_modules
npm-debug.log
.git
.gitignore
README.md
.env
.dockerignore
Dockerfile
```

### Paso 4: Construcción y prueba de la imagen

#### A. Construir la imagen:
```bash
# Construir imagen
docker build -t mi-app-docker:v1.0 .

# Ver la imagen creada
docker images mi-app-docker

# Inspeccionar la imagen
docker inspect mi-app-docker:v1.0
```

#### B. Ejecutar el contenedor:
```bash
# Ejecutar contenedor
docker run -d -p 3000:3000 --name mi-app mi-app-docker:v1.0

# Verificar que está ejecutándose
docker ps

# Ver logs del contenedor
docker logs mi-app

# Probar la aplicación
# Abrir navegador en http://localhost:3000
```

#### C. Comandos útiles para gestión:
```bash
# Entrar al contenedor (debugging)
docker exec -it mi-app sh

# Ver estadísticas del contenedor
docker stats mi-app

# Detener contenedor
docker stop mi-app

# Reiniciar contenedor
docker start mi-app

# Eliminar contenedor
docker rm mi-app

# Eliminar imagen
docker rmi mi-app-docker:v1.0
```

### Paso 5: Optimización del contenedor

#### A. Crear versión multi-stage (Dockerfile.optimized):
```dockerfile
# Etapa 1: Builder
FROM node:18-alpine AS builder

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

# Etapa 2: Runtime
FROM node:18-alpine AS runtime

# Instalar dumb-init para manejo de señales
RUN apk add --no-cache dumb-init

# Crear usuario no-root
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nodejs -u 1001

WORKDIR /app

# Copiar dependencias de la etapa builder
COPY --from=builder /app/node_modules ./node_modules

# Copiar código fuente
COPY --chown=nodejs:nodejs . .

USER nodejs

EXPOSE 3000

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD node -e "require('http').get('http://localhost:3000/health', (res) => { \
        process.exit(res.statusCode === 200 ? 0 : 1) \
    }).on('error', () => process.exit(1))"

ENTRYPOINT ["dumb-init", "--"]
CMD ["npm", "start"]
```

#### B. Construir versión optimizada:
```bash
# Construir versión optimizada
docker build -f Dockerfile.optimized -t mi-app-docker:v2.0 .

# Comparar tamaños
docker images mi-app-docker
```

### Paso 6: Despliegue con Docker Compose

#### A. Crear docker-compose.yml:
```yaml
version: '3.8'

services:
  web:
    build: 
      context: .
      dockerfile: Dockerfile.optimized
    image: mi-app-docker:v2.0
    container_name: mi-app-web
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - PORT=3000
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "node", "-e", "require('http').get('http://localhost:3000/health', (res) => { process.exit(res.statusCode === 200 ? 0 : 1) }).on('error', () => process.exit(1))"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
    networks:
      - mi-app-network

networks:
  mi-app-network:
    driver: bridge
```

#### B. Ejecutar con Docker Compose:
```bash
# Ejecutar aplicación
docker-compose up -d

# Ver estado
docker-compose ps

# Ver logs
docker-compose logs -f web

# Detener aplicación
docker-compose down
```

## 📤 Entregables

### 1. Código fuente completo
**Estructura del proyecto con todos los archivos:**
- Aplicación Node.js funcional
- Dockerfile optimizado
- docker-compose.yml
- Documentación en README.md

### 2. Capturas de pantalla del proceso
**Documenta con screenshots:**
- Construcción de la imagen Docker
- Contenedor ejecutándose (docker ps)
- Aplicación funcionando en navegador
- Logs del contenedor
- Estadísticas del contenedor (docker stats)

### 3. Informe de análisis técnico
**Documento que incluya:**
- Comparación entre Dockerfile básico vs. optimizado
- Análisis de tamaño de imágenes
- Tiempo de construcción y startup
- Uso de recursos (CPU, memoria)
- Mejores prácticas identificadas

### 4. Guía de despliegue
**Manual paso a paso que incluya:**
- Prerrequisitos de instalación
- Comandos de construcción y ejecución
- Troubleshooting común
- Comandos útiles para desarrollo

### 5. Video demostración (opcional)
**Screencast de 5-10 minutos mostrando:**
- Proceso de construcción
- Ejecución del contenedor
- Aplicación funcionando
- Comandos básicos de Docker

## 🔍 Puntos de análisis

### Durante el desarrollo, analiza:

1. **Eficiencia del contenedor:**
   - ¿Cuál es el tamaño final de la imagen?
   - ¿Cuánto tiempo tarda en construirse?
   - ¿Cuánto tiempo tarda en iniciar?

2. **Seguridad:**
   - ¿Por qué es importante usar usuario no-root?
   - ¿Qué vulnerabilidades podría tener el contenedor?
   - ¿Cómo se pueden mitigar?

3. **Portabilidad:**
   - ¿El contenedor funciona igual en diferentes sistemas?
   - ¿Qué dependencias externas tiene?
   - ¿Es verdaderamente portable?

4. **Mantenimiento:**
   - ¿Es fácil actualizar la aplicación?
   - ¿Cómo se gestionan las dependencias?
   - ¿Qué sucede con los datos persistentes?

## ✅ Criterios de evaluación

### Excelente (90-100%)
- Aplicación web funcional y atractiva
- Dockerfile optimizado con mejores prácticas
- Implementación de health checks
- Docker Compose configurado correctamente
- Análisis técnico profundo
- Documentación completa
- Implementación de seguridad (usuario no-root)

### Bueno (80-89%)
- Aplicación funcional básica
- Dockerfile correcto pero no optimizado
- Configuración básica de contenedor
- Análisis técnico adecuado
- Documentación clara
- Algunas mejores prácticas implementadas

### Satisfactorio (70-79%)
- Aplicación funciona correctamente
- Dockerfile básico funcional
- Contenedor se ejecuta correctamente
- Documentación mínima requerida
- Cumplimiento de requisitos básicos

## 💡 Tips para el éxito

### Mejores prácticas Docker:
- **Usa imágenes base oficiales** y ligeras (alpine)
- **Minimiza el número de capas** en el Dockerfile
- **Usa .dockerignore** para excluir archivos innecesarios
- **Implementa health checks** para monitoreo
- **Ejecuta como usuario no-root** por seguridad

### Troubleshooting común:
- **Puerto ya en uso:** `docker ps` para ver contenedores activos
- **Problemas de permisos:** Verificar usuario y ownership
- **Imagen no actualiza:** Usar `--no-cache` en build
- **Contenedor no responde:** Revisar logs con `docker logs`

### Optimización:
- **Multi-stage builds** para reducir tamaño
- **Cache de npm** para builds más rápidos
- **Variables de entorno** para configuración
- **Volumes** para datos persistentes
