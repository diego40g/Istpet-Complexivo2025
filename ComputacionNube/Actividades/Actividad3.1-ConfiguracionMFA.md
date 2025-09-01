# Actividad 3.1: Configuración de Autenticación Multifactor (MFA) en Servicios de Nube

## 🎯 Objetivo
Configurar y probar autenticación multifactor en diferentes servicios de nube populares para comprender su importancia en la seguridad y experimentar con diferentes métodos de implementación.

## 📋 Recursos necesarios
- Smartphone con app de autenticación (Google Authenticator, Microsoft Authenticator, Authy)
- Cuentas en servicios de nube (Gmail, Microsoft, AWS/Azure/GCP - cuentas gratuitas)
- Acceso a Internet
- Documento para registrar el proceso

## ⏱️ Duración estimada
2-3 horas

## 🔒 Medidas de seguridad
**⚠️ IMPORTANTE: Usa solo cuentas personales o de prueba. NO uses cuentas corporativas sin autorización.**

## 📝 Pasos a seguir

### Paso 1: Preparación e instalación de herramientas

#### A. Instala aplicaciones de autenticación:
1. **Google Authenticator** (iOS/Android)
2. **Microsoft Authenticator** (iOS/Android) 
3. **Authy** (iOS/Android) - Recomendado por tener backup en la nube

#### B. Crea cuentas de prueba si no las tienes:
- **Gmail:** Cuenta personal de Google
- **Microsoft:** Cuenta personal de Outlook/Hotmail
- **AWS:** Cuenta gratuita (Free Tier)
- **GitHub:** Cuenta personal para desarrollo

#### C. Documento de registro:
Crea un documento donde registrarás cada paso, capturas de pantalla y observaciones.

### Paso 2: Configuración de MFA en Google/Gmail

#### Pasos detallados:

1. **Acceso a configuración de seguridad:**
   ```
   1. Ve a myaccount.google.com
   2. Clic en "Seguridad" (panel izquierdo)
   3. Busca "Verificación en 2 pasos"
   4. Clic en "Comenzar"
   ```

2. **Configuración paso a paso:**
   ```
   Paso 1: Confirma tu contraseña
   Paso 2: Añade número de teléfono
   Paso 3: Elige método: SMS o llamada
   Paso 4: Introduce código recibido
   Paso 5: ¡Activación completada!
   ```

3. **Añadir app de autenticación:**
   ```
   1. En "Verificación en 2 pasos" → "Configurar"
   2. Selecciona "Aplicación Authenticator"
   3. Escanea código QR con tu app
   4. Introduce código de 6 dígitos
   5. Confirma configuración
   ```

4. **Generar códigos de backup:**
   ```
   1. Busca "Códigos de backup"
   2. Clic en "Configurar" o "Ver códigos"
   3. Descarga/imprime códigos
   4. ¡IMPORTANTE: Guárdalos en lugar seguro!
   ```

#### Documentación requerida:
- Captura de pantalla del proceso de configuración
- Lista de métodos MFA disponibles en Google
- Códigos de backup (oculta algunos dígitos por seguridad)

### Paso 3: Configuración de MFA en Microsoft

#### Pasos detallados:

1. **Acceso a configuración de seguridad:**
   ```
   1. Ve a account.microsoft.com
   2. Clic en "Seguridad"
   3. Busca "Verificación en dos pasos"
   4. Clic en "Activar la verificación en dos pasos"
   ```

2. **Configuración con Microsoft Authenticator:**
   ```
   1. Descarga Microsoft Authenticator si no la tienes
   2. En la configuración, selecciona "Aplicación móvil"
   3. Selecciona "Recibir notificaciones para verificación"
   4. Escanea código QR con Microsoft Authenticator
   5. Aprueba la notificación de prueba
   ```

3. **Configuración de método de respaldo:**
   ```
   1. Configura también SMS como método secundario
   2. Añade número de teléfono
   3. Verifica con código SMS
   4. Confirma configuración
   ```

#### Documentación requerida:
- Comparación de opciones entre Google y Microsoft
- Captura del proceso de configuración
- Prueba de funcionamiento (screenshot de notificación)

### Paso 4: Configuración de MFA en AWS (Cuenta gratuita)

#### Pasos detallados:

1. **Crear cuenta AWS gratuita (si no tienes):**
   ```
   1. Ve a aws.amazon.com
   2. Clic en "Crear cuenta gratuita"
   3. Completa registro con email y tarjeta
   4. Confirma cuenta
   ```

2. **Configurar MFA para usuario root:**
   ```
   1. Accede a AWS Management Console
   2. Clic en tu nombre (esquina superior derecha)
   3. "Credenciales de seguridad"
   4. Sección "Autenticación multifactor (MFA)"
   5. Clic en "Asignar dispositivo MFA"
   ```

3. **Configuración con app virtual:**
   ```
   1. Selecciona "Dispositivo MFA virtual"
   2. Nombre del dispositivo: "Mi-Authenticator-AWS"
   3. Escanea código QR con Google/Microsoft Authenticator
   4. Introduce dos códigos consecutivos de 6 dígitos
   5. Confirma configuración
   ```

4. **Crear usuario IAM con MFA:**
   ```
   1. Ve a servicio IAM
   2. Usuarios → "Crear usuario"
   3. Nombre: "test-user-mfa"
   4. Asigna permisos básicos
   5. Después de creación, configura MFA para este usuario
   ```

#### Documentación requerida:
- Diferencias entre MFA para root vs. usuario IAM
- Captura del proceso de configuración
- Política de MFA que AWS recomienda

### Paso 5: Configuración de MFA en GitHub

#### Pasos detallados:

1. **Acceso a configuración de seguridad:**
   ```
   1. Ve a github.com y haz login
   2. Clic en tu avatar → "Settings"
   3. Panel izquierdo: "Password and authentication"
   4. Busca "Two-factor authentication"
   ```

2. **Configuración con app TOTP:**
   ```
   1. Clic en "Enable two-factor authentication"
   2. Selecciona "Set up using an app"
   3. Escanea código QR con tu app de autenticación
   4. Introduce código de 6 dígitos
   5. Descarga códigos de recovery
   ```

3. **Configuración opcional de SMS:**
   ```
   1. Después de configurar TOTP, añade SMS como backup
   2. Añade número de teléfono
   3. Verifica con código SMS
   ```

#### Documentación requerida:
- Captura de códigos de recovery
- Proceso de login con MFA activado
- Comparación con otros servicios

### Paso 6: Pruebas y análisis comparativo

#### A. Prueba de funcionamiento:
**Para cada servicio configurado:**
1. Cierra sesión completamente
2. Intenta hacer login nuevamente
3. Documenta el flujo de MFA
4. Toma capturas de pantalla del proceso

#### B. Análisis comparativo:
**Crea una tabla comparativa:**

| Servicio | Métodos MFA disponibles | Facilidad de configuración (1-10) | UX durante login (1-10) | Opciones de recovery |
|----------|------------------------|-----------------------------------|------------------------|---------------------|
| Google   | SMS, App, Hardware     | 8                                 | 9                      | Códigos backup      |
| Microsoft| App, SMS, Hardware     | 9                                 | 8                      | App notifications   |
| AWS      | App, Hardware, SMS     | 6                                 | 7                      | Contact support     |
| GitHub   | App, SMS               | 7                                 | 8                      | Recovery codes      |

### Paso 7: Simulación de escenarios de emergencia

#### A. Pérdida de dispositivo móvil:
**Simula (sin ejecutar realmente):**
1. ¿Qué harías si pierdes tu teléfono?
2. ¿Cómo recuperarías acceso a cada servicio?
3. ¿Qué códigos de backup has guardado?

#### B. Cambio de teléfono:
**Documenta el proceso para:**
1. Transferir configuración MFA a nuevo dispositivo
2. Servicios que requieren reconfiguración completa
3. Servicios que permiten transferencia fácil

## 📤 Entregables

### 1. Informe de configuración completo
**Documento que incluya:**
- Screenshots del proceso de configuración para cada servicio
- Dificultades encontradas y cómo se resolvieron
- Códigos de backup (parcialmente ocultos)
- Tiempo invertido en cada configuración

### 2. Análisis comparativo
**Tabla detallada que compare:**
- Métodos MFA disponibles
- Facilidad de configuración
- Experiencia de usuario
- Opciones de recovery
- Seguridad percibida

### 3. Guía de mejores prácticas
**Basándote en tu experiencia, crea una guía con:**
- Recomendaciones para configurar MFA
- Apps de autenticación más recomendadas
- Estrategias de backup y recovery
- Errores comunes a evitar

### 4. Plan de contingencia personal
**Documenta tu estrategia para:**
- Backup de códigos de recovery
- Gestión de múltiples cuentas con MFA
- Procedimiento ante pérdida de dispositivo
- Actualización regular de métodos MFA

### 5. Video demostración (opcional)
**Graba un video corto (3-5 min) mostrando:**
- Proceso de login con MFA en 2 servicios
- Cómo generar códigos con app de autenticación
- Uso de código de backup en simulación

## 🔍 Puntos de análisis crítico

### Analiza y documenta:

1. **Usabilidad vs. Seguridad:**
   - ¿Cuál es el balance ideal?
   - ¿Algún servicio lo hace mejor que otros?

2. **Métodos MFA más seguros:**
   - SMS vs. App vs. Hardware keys
   - ¿Cuándo usar cada uno?

3. **Puntos de fallo:**
   - ¿Qué pasa si falla el método principal?
   - ¿Los métodos de recovery son seguros?

4. **Experiencia de usuario:**
   - ¿Cuál servicio tiene mejor UX?
   - ¿Dónde mejorarías la experiencia?

5. **Adoption barriers:**
   - ¿Por qué la gente no usa MFA?
   - ¿Cómo se podría mejorar la adopción?

## ✅ Criterios de evaluación

### Excelente (90-100%)
- Configuración exitosa en 4+ servicios
- Análisis comparativo detallado y crítico
- Documentación completa con screenshots
- Guía de mejores prácticas innovadora
- Plan de contingencia bien pensado
- Identificación de problemas y soluciones

### Bueno (80-89%)
- Configuración exitosa en 3 servicios
- Análisis comparativo básico pero correcto
- Documentación adecuada
- Guía de mejores prácticas estándar
- Plan de contingencia funcional

### Satisfactorio (70-79%)
- Configuración exitosa en 2 servicios
- Comparación superficial
- Documentación mínima requerida
- Cumplimiento de requisitos básicos

## 💡 Tips adicionales

### Para configuración exitosa:
- **Lee todas las opciones** antes de seleccionar
- **Siempre configura método de backup** antes de finalizar
- **Guarda códigos de recovery** inmediatamente
- **Prueba el funcionamiento** antes de continuar

### Para análisis efectivo:
- **Considera diferentes tipos de usuarios** (técnicos vs. no técnicos)
- **Piensa en escenarios reales** de uso
- **Evalúa el impacto en productividad**
- **Considera costos** (tiempo, dinero, complejidad)

### Seguridad personal:
- **Usa cuentas de prueba** para esta actividad
- **No compartas códigos reales** en la documentación
- **Guarda información sensible** de manera segura
- **Desactiva MFA de prueba** si no planeas mantenerla
