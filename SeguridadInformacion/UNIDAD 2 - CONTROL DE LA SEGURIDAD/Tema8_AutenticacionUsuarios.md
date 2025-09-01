# Tema 8: Autenticación de Usuarios

## Contenido

### La Autenticación de Usuario
- Concepto de autenticación
- Factores de autenticación
- Diferencia entre autenticación y autorización
- Importancia de la gestión de identidad

### Factores de Autenticación
- Algo que sabes (contraseñas)
- Algo que tienes (tokens, tarjetas)
- Algo que eres (biometría)
- Autenticación multifactor (MFA)

### Sistemas de Contraseñas
- Políticas de contraseñas seguras
- Almacenamiento seguro de contraseñas
- Técnicas de hash y salt
- Gestores de contraseñas

### Autenticación Biométrica
- Tipos de biometría (huella, iris, voz, facial)
- Ventajas y desventajas
- Implementación práctica
- Consideraciones de privacidad

### Tokens y Certificados
- Tokens físicos y software
- Certificados digitales
- PKI (Public Key Infrastructure)
- Smart cards

### Permisos y Control de Acceso
- Modelos de control de acceso (MAC, DAC, RBAC)
- Principio de menor privilegio
- Separación de funciones
- Gestión de permisos en sistemas

# Tema 8: Autenticación de Usuarios

## Índice de Contenidos
1. [Métodos de Autenticación](#métodos-de-autenticación)
2. [Tecnologías de Autenticación](#tecnologías-de-autenticación)
3. [Protocolos de Autenticación](#protocolos-de-autenticación)
4. [Sistemas de Single Sign-On (SSO)](#sistemas-de-single-sign-on-sso)
5. [Gestión de Identidades](#gestión-de-identidades)
6. [Ataques contra Autenticación](#ataques-contra-autenticación)
7. [Mejores Prácticas](#mejores-prácticas)
8. [Implementación Práctica](#implementación-práctica)

---

## Métodos de Autenticación

### Fundamentos de Autenticación

#### Los Tres Factores de Autenticación
La autenticación se basa en tres factores fundamentales que verifican la identidad de un usuario:

```
Authentication Factors:
┌─────────────────────────────────────────────────────────────┐
│ Factor 1: Something You Know (Knowledge Factor)            │
│ ├── Passwords                                              │
│ ├── PINs                                                   │
│ ├── Security questions                                     │
│ └── Passphrases                                           │
├─────────────────────────────────────────────────────────────┤
│ Factor 2: Something You Have (Possession Factor)           │
│ ├── Smart cards                                           │
│ ├── Hardware tokens                                       │
│ ├── Mobile devices (SMS, apps)                            │
│ └── USB security keys                                     │
├─────────────────────────────────────────────────────────────┤
│ Factor 3: Something You Are (Inherence Factor)             │
│ ├── Fingerprints                                          │
│ ├── Iris/retina scans                                     │
│ ├── Voice recognition                                      │
│ └── Facial recognition                                     │
└─────────────────────────────────────────────────────────────┘

Security Levels:
├── Single Factor Authentication (SFA) - 1 factor
├── Two-Factor Authentication (2FA) - 2 different factors
├── Multi-Factor Authentication (MFA) - 2+ factors
└── Adaptive Authentication - Context-aware verification
```

#### Autenticación de Un Factor (SFA)

**Características:**
- Utiliza solo un método de verificación
- Generalmente contraseñas
- Menor nivel de seguridad
- Fácil implementación y uso

```python
# Ejemplo básico de autenticación SFA
import hashlib
import getpass

class SimpleAuth:
    def __init__(self):
        # Base de datos simulada de usuarios
        self.users = {
            "admin": "240be518fabd2724ddb6f04eeb1da5967448d7e831c08c8fa822809f74c720a9",  # "admin123"
            "user1": "ef92b778bafe771e89245b89ecbc08a44a4e166c06659911881f383d4473e94f"   # "secret456"
        }
    
    def hash_password(self, password):
        """Crear hash SHA-256 de la contraseña"""
        return hashlib.sha256(password.encode()).hexdigest()
    
    def authenticate(self, username, password):
        """Verificar credenciales de usuario"""
        if username in self.users:
            password_hash = self.hash_password(password)
            if password_hash == self.users[username]:
                return True
        return False
    
    def login(self):
        """Proceso de inicio de sesión"""
        username = input("Username: ")
        password = getpass.getpass("Password: ")
        
        if self.authenticate(username, password):
            print("✓ Authentication successful!")
            return True
        else:
            print("✗ Invalid credentials!")
            return False

# Uso
auth = SimpleAuth()
auth.login()
```

#### Autenticación de Dos Factores (2FA)

**Implementación Típica:**
```
2FA Process Flow:
User ──1. Username/Password──→ System
User ←─2. Request 2nd Factor──── System
User ──3. SMS/Token/Biometric─→ System
User ←─4. Grant/Deny Access──── System

Common 2FA Methods:
├── SMS-based OTP
├── Email-based verification
├── TOTP (Time-based One-Time Password)
├── Push notifications
├── Hardware tokens (YubiKey)
└── Biometric verification
```

#### Ejemplo de Implementación 2FA con TOTP
```python
import pyotp
import qrcode
import io
import base64

class TOTP_2FA:
    def __init__(self):
        self.users = {}
    
    def register_user(self, username):
        """Registrar nuevo usuario con 2FA"""
        # Generar secret key única para el usuario
        secret = pyotp.random_base32()
        self.users[username] = {
            'secret': secret,
            'totp': pyotp.TOTP(secret)
        }
        
        # Generar URL para QR code
        totp_uri = pyotp.totp.TOTP(secret).provisioning_uri(
            username, issuer_name="SecureApp"
        )
        
        # Generar QR code
        qr = qrcode.QRCode(version=1, box_size=10, border=5)
        qr.add_data(totp_uri)
        qr.make(fit=True)
        
        print(f"User {username} registered.")
        print(f"Secret key: {secret}")
        print("Scan QR code with authenticator app:")
        qr.print_ascii()
        
        return secret
    
    def verify_totp(self, username, token):
        """Verificar token TOTP"""
        if username not in self.users:
            return False
        
        totp = self.users[username]['totp']
        return totp.verify(token, valid_window=1)
    
    def authenticate_2fa(self, username, password, token):
        """Autenticación completa 2FA"""
        # Paso 1: Verificar contraseña (simulado)
        if not self.verify_password(username, password):
            return False, "Invalid password"
        
        # Paso 2: Verificar TOTP
        if not self.verify_totp(username, token):
            return False, "Invalid TOTP token"
        
        return True, "Authentication successful"
    
    def verify_password(self, username, password):
        """Simulación de verificación de contraseña"""
        # En implementación real, verificar hash de contraseña
        return True  # Simplificado para ejemplo

---

## Sistemas de Single Sign-On (SSO)

### Conceptos Fundamentales de SSO

#### Beneficios del Single Sign-On
```
SSO Benefits Analysis:
├── User Experience
│   ├── One set of credentials for multiple systems
│   ├── Reduced password fatigue
│   ├── Faster access to resources
│   └── Improved productivity
├── Security Benefits
│   ├── Centralized authentication control
│   ├── Stronger password policies
│   ├── Reduced credential exposure
│   └── Better audit trails
├── Administrative Benefits
│   ├── Centralized user management
│   ├── Simplified provisioning/deprovisioning
│   ├── Reduced helpdesk calls
│   └── Lower administrative overhead
└── Business Benefits
    ├── Improved employee satisfaction
    ├── Faster onboarding processes
    ├── Better compliance reporting
    └── Reduced operational costs
```

#### Arquitectura SSO
```
SSO Architecture Components:
┌─────────────────────────────────────────────────────────────┐
│                    SSO Architecture                         │
│                                                             │
│ User ────1. Access Request────→ Service Provider (SP)      │
│   ↑                                        │                │
│   │                                        │                │
│   │         6. Access Granted              │2. Redirect     │
│   │                                        │   to IdP       │
│   │                                        ↓                │
│   │                             Identity Provider (IdP)     │
│   │                                        │                │
│   │                                        │3. Authentication│
│   │                                        │   Request      │
│   │                                        ↓                │
│   └─────4. Authenticate─────────────────── User Portal     │
│           5. Return SAML/JWT Token                          │
│                                                             │
│ Components:                                                 │
│ ├── Identity Provider (IdP): Authentication authority      │
│ ├── Service Provider (SP): Target application              │
│ ├── Security Token: SAML assertion, JWT, etc.             │
│ └── User Agent: Browser or application                     │
└─────────────────────────────────────────────────────────────┘
```

### SAML Implementation

#### SAML SSO Implementation
```python
import xml.etree.ElementTree as ET
import base64
import zlib
import urllib.parse
from datetime import datetime, timedelta
import uuid
from cryptography.hazmat.primitives import serialization, hashes
from cryptography.hazmat.primitives.asymmetric import rsa, padding

class SAMLProvider:
    def __init__(self, entity_id, sso_url, certificate_path=None):
        self.entity_id = entity_id
        self.sso_url = sso_url
        self.certificate_path = certificate_path
        
    def create_saml_request(self, sp_entity_id, acs_url):
        """Crear SAML Authentication Request"""
        request_id = f"_request_{uuid.uuid4().hex}"
        issue_instant = datetime.utcnow().strftime('%Y-%m-%dT%H:%M:%SZ')
        
        # Crear XML SAML Request
        saml_request = f"""<?xml version="1.0" encoding="UTF-8"?>
<samlp:AuthnRequest 
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
    xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
    ID="{request_id}"
    Version="2.0"
    IssueInstant="{issue_instant}"
    Destination="{self.sso_url}"
    AssertionConsumerServiceURL="{acs_url}"
    ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST">
    
    <saml:Issuer>{sp_entity_id}</saml:Issuer>
    
    <samlp:NameIDPolicy 
        Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
        AllowCreate="true"/>
        
    <samlp:RequestedAuthnContext Comparison="exact">
        <saml:AuthnContextClassRef>
            urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
        </saml:AuthnContextClassRef>
    </samlp:RequestedAuthnContext>
</samlp:AuthnRequest>"""
        
        return saml_request, request_id
    
    def encode_saml_request(self, saml_request):
        """Codificar SAML Request para HTTP Redirect"""
        # Deflate compression
        compressed = zlib.compress(saml_request.encode('utf-8'))
        
        # Base64 encoding
        encoded = base64.b64encode(compressed).decode('utf-8')
        
        # URL encoding
        return urllib.parse.quote_plus(encoded)
    
    def create_sso_redirect_url(self, saml_request, relay_state=None):
        """Crear URL de redirección para SSO"""
        encoded_request = self.encode_saml_request(saml_request)
        redirect_url = f"{self.sso_url}?SAMLRequest={encoded_request}"
        
        if relay_state:
            encoded_relay_state = urllib.parse.quote_plus(relay_state)
            redirect_url += f"&RelayState={encoded_relay_state}"
        
        return redirect_url
    
    def create_saml_response(self, user_attributes, request_id, sp_entity_id):
        """Crear SAML Response (Identity Provider)"""
        response_id = f"_response_{uuid.uuid4().hex}"
        assertion_id = f"_assertion_{uuid.uuid4().hex}"
        issue_instant = datetime.utcnow().strftime('%Y-%m-%dT%H:%M:%SZ')
        not_on_or_after = (datetime.utcnow() + timedelta(hours=1)).strftime('%Y-%m-%dT%H:%M:%SZ')
        
        # Crear assertion
        attributes_xml = ""
        for attr_name, attr_values in user_attributes.items():
            if not isinstance(attr_values, list):
                attr_values = [attr_values]
            
            attr_values_xml = ""
            for value in attr_values:
                attr_values_xml += f'<saml:AttributeValue xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">{value}</saml:AttributeValue>'
            
            attributes_xml += f"""
            <saml:Attribute Name="{attr_name}" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:uri">
                {attr_values_xml}
            </saml:Attribute>"""
        
        saml_response = f"""<?xml version="1.0" encoding="UTF-8"?>
<samlp:Response 
    xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol"
    xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion"
    ID="{response_id}"
    Version="2.0"
    IssueInstant="{issue_instant}"
    Destination="{sp_entity_id}"
    InResponseTo="{request_id}">
    
    <saml:Issuer>{self.entity_id}</saml:Issuer>
    
    <samlp:Status>
        <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    
    <saml:Assertion 
        ID="{assertion_id}"
        Version="2.0"
        IssueInstant="{issue_instant}">
        
        <saml:Issuer>{self.entity_id}</saml:Issuer>
        
        <saml:Subject>
            <saml:NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient">
                {user_attributes.get('username', 'unknown_user')}
            </saml:NameID>
            <saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
                <saml:SubjectConfirmationData 
                    NotOnOrAfter="{not_on_or_after}"
                    Recipient="{sp_entity_id}"
                    InResponseTo="{request_id}"/>
            </saml:SubjectConfirmation>
        </saml:Subject>
        
        <saml:Conditions 
            NotBefore="{issue_instant}"
            NotOnOrAfter="{not_on_or_after}">
            <saml:AudienceRestriction>
                <saml:Audience>{sp_entity_id}</saml:Audience>
            </saml:AudienceRestriction>
        </saml:Conditions>
        
        <saml:AuthnStatement AuthnInstant="{issue_instant}">
            <saml:AuthnContext>
                <saml:AuthnContextClassRef>
                    urn:oasis:names:tc:SAML:2.0:ac:classes:Password
                </saml:AuthnContextClassRef>
            </saml:AuthnContext>
        </saml:AuthnStatement>
        
        <saml:AttributeStatement>
            {attributes_xml}
        </saml:AttributeStatement>
    </saml:Assertion>
</samlp:Response>"""
        
        return saml_response
    
    def parse_saml_response(self, encoded_response):
        """Parsear SAML Response recibida"""
        try:
            # Decodificar Base64
            decoded = base64.b64decode(encoded_response)
            
            # Parsear XML
            root = ET.fromstring(decoded)
            
            # Extraer información básica
            response_info = {
                'response_id': root.get('ID'),
                'status': None,
                'attributes': {},
                'name_id': None
            }
            
            # Verificar status
            status_elem = root.find('.//{urn:oasis:names:tc:SAML:2.0:protocol}StatusCode')
            if status_elem is not None:
                response_info['status'] = status_elem.get('Value')
            
            # Extraer NameID
            nameid_elem = root.find('.//{urn:oasis:names:tc:SAML:2.0:assertion}NameID')
            if nameid_elem is not None:
                response_info['name_id'] = nameid_elem.text
            
            # Extraer atributos
            for attr_elem in root.findall('.//{urn:oasis:names:tc:SAML:2.0:assertion}Attribute'):
                attr_name = attr_elem.get('Name')
                attr_values = []
                
                for value_elem in attr_elem.findall('.//{urn:oasis:names:tc:SAML:2.0:assertion}AttributeValue'):
                    attr_values.append(value_elem.text)
                
                response_info['attributes'][attr_name] = attr_values
            
            return response_info
            
        except Exception as e:
            raise Exception(f"Error parsing SAML response: {str(e)}")

# Ejemplo de uso SAML SSO
class SAMLServiceProvider:
    def __init__(self, entity_id, acs_url, idp_sso_url):
        self.entity_id = entity_id
        self.acs_url = acs_url
        self.saml_provider = SAMLProvider("https://idp.example.com", idp_sso_url)
        self.pending_requests = {}
    
    def initiate_sso(self, target_url=None):
        """Iniciar proceso SSO"""
        # Crear SAML Request
        saml_request, request_id = self.saml_provider.create_saml_request(
            self.entity_id, self.acs_url
        )
        
        # Guardar request_id para validación posterior
        self.pending_requests[request_id] = {
            'timestamp': datetime.utcnow(),
            'target_url': target_url
        }
        
        # Crear URL de redirección
        redirect_url = self.saml_provider.create_sso_redirect_url(
            saml_request, relay_state=target_url
        )
        
        return redirect_url, request_id
    
    def handle_sso_response(self, saml_response, relay_state=None):
        """Procesar respuesta SSO"""
        try:
            response_info = self.saml_provider.parse_saml_response(saml_response)
            
            # Verificar status
            if response_info['status'] != 'urn:oasis:names:tc:SAML:2.0:status:Success':
                return False, "Authentication failed", None
            
            # Extraer información de usuario
            user_info = {
                'username': response_info['name_id'],
                'attributes': response_info['attributes']
            }
            
            return True, "Authentication successful", user_info
            
        except Exception as e:
            return False, f"Error processing SAML response: {str(e)}", None

# Ejemplo de integración
saml_sp = SAMLServiceProvider(
    entity_id="https://sp.example.com",
    acs_url="https://sp.example.com/saml/acs",
    idp_sso_url="https://idp.example.com/saml/sso"
)

# Iniciar SSO
sso_url, request_id = saml_sp.initiate_sso(target_url="/dashboard")
print(f"Redirect to: {sso_url}")
```

### OAuth 2.0 y OpenID Connect

#### Implementación OAuth 2.0
```python
import requests
import secrets
import hashlib
import base64
import json
import urllib.parse
from datetime import datetime, timedelta

class OAuth2Client:
    def __init__(self, client_id, client_secret, redirect_uri, auth_server_url):
        self.client_id = client_id
        self.client_secret = client_secret
        self.redirect_uri = redirect_uri
        self.auth_server_url = auth_server_url
        self.token_endpoint = f"{auth_server_url}/token"
        self.auth_endpoint = f"{auth_server_url}/authorize"
    
    def generate_pkce_challenge(self):
        """Generar PKCE challenge para OAuth 2.0 público"""
        # Generar code verifier
        code_verifier = base64.urlsafe_b64encode(secrets.token_bytes(32)).decode('utf-8').rstrip('=')
        
        # Generar code challenge
        challenge_bytes = hashlib.sha256(code_verifier.encode()).digest()
        code_challenge = base64.urlsafe_b64encode(challenge_bytes).decode('utf-8').rstrip('=')
        
        return code_verifier, code_challenge
    
    def get_authorization_url(self, scope="openid profile email", state=None, use_pkce=True):
        """Crear URL de autorización"""
        if state is None:
            state = secrets.token_urlsafe(32)
        
        params = {
            'response_type': 'code',
            'client_id': self.client_id,
            'redirect_uri': self.redirect_uri,
            'scope': scope,
            'state': state
        }
        
        code_verifier, code_challenge = None, None
        if use_pkce:
            code_verifier, code_challenge = self.generate_pkce_challenge()
            params.update({
                'code_challenge': code_challenge,
                'code_challenge_method': 'S256'
            })
        
        auth_url = f"{self.auth_endpoint}?{urllib.parse.urlencode(params)}"
        
        return auth_url, state, code_verifier
    
    def exchange_code_for_token(self, authorization_code, code_verifier=None):
        """Intercambiar código de autorización por token"""
        token_data = {
            'grant_type': 'authorization_code',
            'code': authorization_code,
            'redirect_uri': self.redirect_uri,
            'client_id': self.client_id,
        }
        
        # Añadir PKCE code verifier si está presente
        if code_verifier:
            token_data['code_verifier'] = code_verifier
        
        headers = {
            'Content-Type': 'application/x-www-form-urlencoded'
        }
        
        # Autenticación de cliente
        if self.client_secret:
            # Client credentials en header Authorization
            credentials = base64.b64encode(f"{self.client_id}:{self.client_secret}".encode()).decode()
            headers['Authorization'] = f"Basic {credentials}"
        else:
            # Client ID en body (para clientes públicos)
            token_data['client_id'] = self.client_id
        
        try:
            response = requests.post(
                self.token_endpoint,
                data=token_data,
                headers=headers,
                timeout=10
            )
            
            if response.status_code == 200:
                token_response = response.json()
                return True, token_response
            else:
                return False, f"Token exchange failed: {response.text}"
                
        except Exception as e:
            return False, f"Error exchanging token: {str(e)}"
    
    def refresh_access_token(self, refresh_token):
        """Renovar access token usando refresh token"""
        token_data = {
            'grant_type': 'refresh_token',
            'refresh_token': refresh_token
        }
        
        headers = {
            'Content-Type': 'application/x-www-form-urlencoded'
        }
        
        if self.client_secret:
            credentials = base64.b64encode(f"{self.client_id}:{self.client_secret}".encode()).decode()
            headers['Authorization'] = f"Basic {credentials}"
        else:
            token_data['client_id'] = self.client_id
        
        try:
            response = requests.post(
                self.token_endpoint,
                data=token_data,
                headers=headers,
                timeout=10
            )
            
            if response.status_code == 200:
                return True, response.json()
            else:
                return False, f"Token refresh failed: {response.text}"
                
        except Exception as e:
            return False, f"Error refreshing token: {str(e)}"
    
    def get_user_info(self, access_token):
        """Obtener información de usuario usando access token"""
        headers = {
            'Authorization': f'Bearer {access_token}'
        }
        
        userinfo_endpoint = f"{self.auth_server_url}/userinfo"
        
        try:
            response = requests.get(userinfo_endpoint, headers=headers, timeout=10)
            
            if response.status_code == 200:
                return True, response.json()
            else:
                return False, f"User info request failed: {response.text}"
                
        except Exception as e:
            return False, f"Error getting user info: {str(e)}"

# OpenID Connect implementation
class OpenIDConnectClient(OAuth2Client):
    def __init__(self, client_id, client_secret, redirect_uri, issuer_url):
        # Descubrir endpoints desde well-known configuration
        self.issuer_url = issuer_url
        self.discovery_url = f"{issuer_url}/.well-known/openid-configuration"
        
        # Cargar configuración
        discovery_config = self.load_discovery_document()
        
        super().__init__(
            client_id, client_secret, redirect_uri, 
            discovery_config.get('authorization_endpoint', '').replace('/authorize', '')
        )
        
        self.token_endpoint = discovery_config.get('token_endpoint')
        self.auth_endpoint = discovery_config.get('authorization_endpoint')
        self.userinfo_endpoint = discovery_config.get('userinfo_endpoint')
        self.jwks_uri = discovery_config.get('jwks_uri')
    
    def load_discovery_document(self):
        """Cargar documento de descubrimiento OpenID Connect"""
        try:
            response = requests.get(self.discovery_url, timeout=10)
            if response.status_code == 200:
                return response.json()
            else:
                raise Exception(f"Failed to load discovery document: {response.status_code}")
        except Exception as e:
            print(f"Error loading discovery document: {e}")
            # Configuración por defecto
            return {
                'authorization_endpoint': f"{self.issuer_url}/authorize",
                'token_endpoint': f"{self.issuer_url}/token",
                'userinfo_endpoint': f"{self.issuer_url}/userinfo",
                'jwks_uri': f"{self.issuer_url}/jwks"
            }
    
    def validate_id_token(self, id_token):
        """Validar ID Token JWT (implementación simplificada)"""
        try:
            # En implementación real, validar firma JWT con JWKS
            # Aquí solo decodificamos el payload
            header, payload, signature = id_token.split('.')
            
            # Añadir padding si es necesario
            payload += '=' * (-len(payload) % 4)
            
            decoded_payload = base64.urlsafe_b64decode(payload)
            claims = json.loads(decoded_payload)
            
            # Validaciones básicas
            now = datetime.utcnow().timestamp()
            
            if claims.get('exp', 0) < now:
                return False, "Token expired"
            
            if claims.get('iss') != self.issuer_url:
                return False, "Invalid issuer"
            
            if self.client_id not in claims.get('aud', []):
                return False, "Invalid audience"
            
            return True, claims
            
        except Exception as e:
            return False, f"ID token validation error: {str(e)}"
    
    def authenticate(self, authorization_code, code_verifier=None):
        """Proceso completo de autenticación OpenID Connect"""
        # Intercambiar código por tokens
        token_success, token_response = self.exchange_code_for_token(
            authorization_code, code_verifier
        )
        
        if not token_success:
            return False, token_response, None
        
        # Validar ID token
        id_token = token_response.get('id_token')
        if id_token:
            valid, claims_or_error = self.validate_id_token(id_token)
            if not valid:
                return False, f"ID token validation failed: {claims_or_error}", None
            
            user_claims = claims_or_error
        else:
            return False, "No ID token in response", None
        
        # Obtener información adicional de usuario si es necesario
        access_token = token_response.get('access_token')
        if access_token and self.userinfo_endpoint:
            userinfo_success, userinfo = self.get_user_info(access_token)
            if userinfo_success:
                # Combinar claims del ID token con userinfo
                user_claims.update(userinfo)
        
        return True, "Authentication successful", {
            'tokens': token_response,
            'user_claims': user_claims
        }

# Ejemplo de uso OAuth/OIDC
oidc_client = OpenIDConnectClient(
    client_id="my-app-client-id",
    client_secret="my-app-client-secret",
    redirect_uri="https://myapp.com/callback",
    issuer_url="https://auth.example.com"
)

# Iniciar flujo de autenticación
auth_url, state, code_verifier = oidc_client.get_authorization_url()
print(f"Redirect user to: {auth_url}")

# Después del callback (simulado)
# auth_success, message, result = oidc_client.authenticate(
#     authorization_code="received_auth_code",
#     code_verifier=code_verifier
# )
```

---

## Gestión de Identidades

### Identity and Access Management (IAM)

#### Arquitectura IAM Empresarial
```
Enterprise IAM Architecture:
┌─────────────────────────────────────────────────────────────┐
│                    IAM Components                           │
│                                                             │
│ ┌─────────────────┐  ┌─────────────────┐  ┌───────────────┐ │
│ │   Identity      │  │   Access        │  │  Governance   │ │
│ │   Management    │  │   Management    │  │  & Analytics  │ │
│ │                 │  │                 │  │               │ │
│ │ • User Stores   │  │ • Authorization │  │ • Compliance  │ │
│ │ • Directories   │  │ • RBAC/ABAC     │  │ • Auditing    │ │
│ │ • Provisioning  │  │ • Entitlements  │  │ • Reporting   │ │
│ └─────────────────┘  └─────────────────┘  └───────────────┘ │
│                                                             │
│ ┌─────────────────┐  ┌─────────────────┐  ┌───────────────┐ │
│ │  Authentication │  │   Federation    │  │  Application  │ │
│ │   Services      │  │   Services      │  │  Integration  │ │
│ │                 │  │                 │  │               │ │
│ │ • MFA           │  │ • SAML          │  │ • APIs        │ │
│ │ • SSO           │  │ • OAuth/OIDC    │  │ • Connectors  │ │
│ │ • Risk-based    │  │ • Trust         │  │ • Adapters    │ │
│ └─────────────────┘  └─────────────────┘  └───────────────┘ │
└─────────────────────────────────────────────────────────────┘

IAM Processes:
├── Identity Lifecycle Management
├── Access Request and Approval
├── Periodic Access Reviews
├── Segregation of Duties (SoD)
└── Compliance Reporting
```

#### Implementación Sistema IAM
```python
from datetime import datetime, timedelta
from enum import Enum
import json
import hashlib

class AccessStatus(Enum):
    ACTIVE = "active"
    SUSPENDED = "suspended"
    EXPIRED = "expired"
    PENDING = "pending"

class Role:
    def __init__(self, role_id, name, description, permissions=None):
        self.role_id = role_id
        self.name = name
        self.description = description
        self.permissions = permissions or []
        self.created_date = datetime.now()
    
    def add_permission(self, permission):
        if permission not in self.permissions:
            self.permissions.append(permission)
    
    def remove_permission(self, permission):
        if permission in self.permissions:
            self.permissions.remove(permission)

class User:
    def __init__(self, user_id, username, email, first_name, last_name):
        self.user_id = user_id
        self.username = username
        self.email = email
        self.first_name = first_name
        self.last_name = last_name
        self.roles = []
        self.status = AccessStatus.PENDING
        self.created_date = datetime.now()
        self.last_login = None
        self.failed_login_attempts = 0
        self.password_last_changed = None
        self.attributes = {}
    
    def assign_role(self, role, assigned_by, expiration_date=None):
        role_assignment = {
            'role': role,
            'assigned_date': datetime.now(),
            'assigned_by': assigned_by,
            'expiration_date': expiration_date,
            'status': AccessStatus.ACTIVE
        }
        self.roles.append(role_assignment)
    
    def get_effective_permissions(self):
        """Obtener permisos efectivos de todos los roles activos"""
        permissions = set()
        for role_assignment in self.roles:
            if role_assignment['status'] == AccessStatus.ACTIVE:
                # Verificar expiración
                if (role_assignment['expiration_date'] is None or 
                    role_assignment['expiration_date'] > datetime.now()):
                    permissions.update(role_assignment['role'].permissions)
        return list(permissions)
    
    def has_permission(self, permission):
        """Verificar si el usuario tiene un permiso específico"""
        return permission in self.get_effective_permissions()

class IAMSystem:
    def __init__(self):
        self.users = {}
        self.roles = {}
        self.access_requests = {}
        self.audit_log = []
        self.policies = {}
    
    def log_event(self, event_type, user_id, details):
        """Registrar evento en log de auditoría"""
        log_entry = {
            'timestamp': datetime.now(),
            'event_type': event_type,
            'user_id': user_id,
            'details': details
        }
        self.audit_log.append(log_entry)
    
    def create_user(self, username, email, first_name, last_name, created_by):
        """Crear nuevo usuario"""
        user_id = hashlib.md5(username.encode()).hexdigest()[:8]
        
        if user_id in self.users:
            return False, "User already exists"
        
        user = User(user_id, username, email, first_name, last_name)
        self.users[user_id] = user
        
        self.log_event("USER_CREATED", user_id, {
            'username': username,
            'created_by': created_by
        })
        
        return True, user
    
    def create_role(self, name, description, permissions):
        """Crear nuevo rol"""
        role_id = hashlib.md5(name.encode()).hexdigest()[:8]
        
        if role_id in self.roles:
            return False, "Role already exists"
        
        role = Role(role_id, name, description, permissions)
        self.roles[role_id] = role
        
        self.log_event("ROLE_CREATED", None, {
            'role_name': name,
            'permissions': permissions
        })
        
        return True, role
    
    def request_access(self, user_id, role_id, requester_id, justification, expiration_date=None):
        """Solicitar acceso a rol"""
        request_id = hashlib.md5(f"{user_id}{role_id}{datetime.now()}".encode()).hexdigest()[:8]
        
        access_request = {
            'request_id': request_id,
            'user_id': user_id,
            'role_id': role_id,
            'requester_id': requester_id,
            'justification': justification,
            'expiration_date': expiration_date,
            'status': 'PENDING',
            'request_date': datetime.now(),
            'approved_by': None,
            'approval_date': None
        }
        
        self.access_requests[request_id] = access_request
        
        self.log_event("ACCESS_REQUESTED", user_id, {
            'role_id': role_id,
            'requester_id': requester_id,
            'justification': justification
        })
        
        return True, request_id
    
    def approve_access_request(self, request_id, approver_id, comments=None):
        """Aprobar solicitud de acceso"""
        if request_id not in self.access_requests:
            return False, "Request not found"
        
        request = self.access_requests[request_id]
        
        if request['status'] != 'PENDING':
            return False, "Request already processed"
        
        # Verificar que el usuario y rol existen
        user_id = request['user_id']
        role_id = request['role_id']
        
        if user_id not in self.users or role_id not in self.roles:
            return False, "User or role not found"
        
        # Aprobar solicitud
        request['status'] = 'APPROVED'
        request['approved_by'] = approver_id
        request['approval_date'] = datetime.now()
        request['comments'] = comments
        
        # Asignar rol al usuario
        user = self.users[user_id]
        role = self.roles[role_id]
        user.assign_role(role, approver_id, request['expiration_date'])
        
        self.log_event("ACCESS_APPROVED", user_id, {
            'role_id': role_id,
            'approved_by': approver_id,
            'request_id': request_id
        })
        
        return True, "Access request approved"
    
    def revoke_access(self, user_id, role_id, revoked_by, reason):
        """Revocar acceso a rol"""
        if user_id not in self.users:
            return False, "User not found"
        
        user = self.users[user_id]
        
        # Buscar y revocar rol
        for role_assignment in user.roles:
            if (role_assignment['role'].role_id == role_id and 
                role_assignment['status'] == AccessStatus.ACTIVE):
                role_assignment['status'] = AccessStatus.SUSPENDED
                role_assignment['revoked_by'] = revoked_by
                role_assignment['revoked_date'] = datetime.now()
                role_assignment['revocation_reason'] = reason
                
                self.log_event("ACCESS_REVOKED", user_id, {
                    'role_id': role_id,
                    'revoked_by': revoked_by,
                    'reason': reason
                })
                
                return True, "Access revoked successfully"
        
        return False, "Role assignment not found or already inactive"
    
    def perform_access_review(self, reviewer_id):
        """Realizar revisión de accesos"""
        review_results = {
            'review_date': datetime.now(),
            'reviewer_id': reviewer_id,
            'users_reviewed': 0,
            'roles_reviewed': 0,
            'expired_access': [],
            'suspicious_access': [],
            'recommendations': []
        }
        
        for user_id, user in self.users.items():
            review_results['users_reviewed'] += 1
            
            # Verificar roles expirados
            for role_assignment in user.roles:
                if (role_assignment['expiration_date'] and 
                    role_assignment['expiration_date'] < datetime.now() and
                    role_assignment['status'] == AccessStatus.ACTIVE):
                    
                    review_results['expired_access'].append({
                        'user_id': user_id,
                        'username': user.username,
                        'role': role_assignment['role'].name,
                        'expiration_date': role_assignment['expiration_date']
                    })
            
            # Detectar acceso sospechoso (sin login por mucho tiempo)
            if (user.last_login and 
                (datetime.now() - user.last_login).days > 90):
                review_results['suspicious_access'].append({
                    'user_id': user_id,
                    'username': user.username,
                    'last_login': user.last_login,
                    'reason': 'No login for over 90 days'
                })
        
        # Generar recomendaciones
        if review_results['expired_access']:
            review_results['recommendations'].append(
                "Revoke expired role assignments"
            )
        
        if review_results['suspicious_access']:
            review_results['recommendations'].append(
                "Review accounts with no recent activity"
            )
        
        self.log_event("ACCESS_REVIEW", None, {
            'reviewer_id': reviewer_id,
            'results_summary': {
                'users_reviewed': review_results['users_reviewed'],
                'expired_count': len(review_results['expired_access']),
                'suspicious_count': len(review_results['suspicious_access'])
            }
        })
        
        return review_results
    
    def generate_compliance_report(self, report_type="full"):
        """Generar reporte de cumplimiento"""
        report = {
            'report_date': datetime.now(),
            'report_type': report_type,
            'user_statistics': {
                'total_users': len(self.users),
                'active_users': len([u for u in self.users.values() if u.status == AccessStatus.ACTIVE]),
                'suspended_users': len([u for u in self.users.values() if u.status == AccessStatus.SUSPENDED])
            },
            'role_statistics': {
                'total_roles': len(self.roles),
                'permissions_per_role': {r.name: len(r.permissions) for r in self.roles.values()}
            },
            'access_requests': {
                'total_requests': len(self.access_requests),
                'pending_requests': len([r for r in self.access_requests.values() if r['status'] == 'PENDING']),
                'approved_requests': len([r for r in self.access_requests.values() if r['status'] == 'APPROVED'])
            },
            'recent_activities': self.audit_log[-50:]  # Últimas 50 actividades
        }
        
        return report

# Ejemplo de uso del sistema IAM
iam = IAMSystem()

# Crear roles
iam.create_role("Admin", "System Administrator", ["read", "write", "delete", "admin"])
iam.create_role("User", "Standard User", ["read", "write"])
iam.create_role("ReadOnly", "Read Only Access", ["read"])

# Crear usuarios
iam.create_user("john.doe", "john@example.com", "John", "Doe", "system")
iam.create_user("jane.smith", "jane@example.com", "Jane", "Smith", "admin")

# Solicitar acceso
user_id = list(iam.users.keys())[0]  # John Doe
role_id = list(iam.roles.keys())[1]  # User role

success, request_id = iam.request_access(
    user_id, role_id, "admin", 
    "User needs access for daily operations",
    expiration_date=datetime.now() + timedelta(days=365)
)

if success:
    # Aprobar solicitud
    iam.approve_access_request(request_id, "admin", "Approved for business needs")

# Realizar revisión de accesos
review_results = iam.perform_access_review("security_officer")
print(f"Access review completed: {review_results['users_reviewed']} users reviewed")

# Generar reporte de cumplimiento
compliance_report = iam.generate_compliance_report()
print(f"Compliance report: {compliance_report['user_statistics']['total_users']} total users")
```

Este contenido completo del Tema 8 proporciona una cobertura exhaustiva de la autenticación de usuarios, desde métodos básicos hasta sistemas empresariales avanzados de gestión de identidades. Continuaré con el Tema 9 a continuación.

#### Estrategias MFA Avanzadas
```
Advanced MFA Strategies:
├── Risk-Based Authentication
│   ├── Device fingerprinting
│   ├── Geolocation analysis
│   ├── Behavioral patterns
│   └── Time-based restrictions
├── Adaptive Authentication
│   ├── Context-aware decisions
│   ├── Machine learning integration
│   ├── Continuous authentication
│   └── Step-up authentication
├── Passwordless Authentication
│   ├── FIDO2/WebAuthn
│   ├── Certificate-based
│   ├── Biometric-only
│   └── Magic links
└── Zero Trust Authentication
    ├── Never trust, always verify
    ├── Continuous verification
    ├── Micro-segmentation
    └── Least privilege access
```

#### Implementación de Autenticación Adaptativa
```python
import json
import requests
from datetime import datetime, timedelta
import geoip2.database

class AdaptiveAuth:
    def __init__(self):
        self.user_profiles = {}
        self.risk_threshold = 0.7
        self.geo_reader = geoip2.database.Reader('GeoLite2-City.mmdb')
    
    def calculate_risk_score(self, username, request_data):
        """Calcular puntuación de riesgo basada en contexto"""
        risk_score = 0.0
        
        # Factor 1: Ubicación geográfica
        try:
            response = self.geo_reader.city(request_data['ip_address'])
            current_country = response.country.iso_code
            
            if username in self.user_profiles:
                usual_countries = self.user_profiles[username].get('countries', [])
                if current_country not in usual_countries:
                    risk_score += 0.3
        except:
            risk_score += 0.2
        
        # Factor 2: Dispositivo desconocido
        device_fingerprint = request_data.get('device_fingerprint')
        if username in self.user_profiles:
            known_devices = self.user_profiles[username].get('devices', [])
            if device_fingerprint not in known_devices:
                risk_score += 0.4
        
        # Factor 3: Horario inusual
        current_hour = datetime.now().hour
        if username in self.user_profiles:
            usual_hours = self.user_profiles[username].get('login_hours', [])
            if current_hour not in usual_hours:
                risk_score += 0.2
        
        # Factor 4: Múltiples intentos fallidos recientes
        failed_attempts = request_data.get('recent_failures', 0)
        if failed_attempts > 3:
            risk_score += 0.3
        
        return min(risk_score, 1.0)
    
    def determine_auth_requirements(self, risk_score):
        """Determinar requisitos de autenticación basados en riesgo"""
        if risk_score < 0.3:
            return ["password"]
        elif risk_score < 0.6:
            return ["password", "sms_otp"]
        elif risk_score < 0.8:
            return ["password", "totp", "device_verification"]
        else:
            return ["password", "totp", "biometric", "admin_approval"]
    
    def authenticate_adaptive(self, username, provided_factors, request_context):
        """Proceso de autenticación adaptativa"""
        risk_score = self.calculate_risk_score(username, request_context)
        required_factors = self.determine_auth_requirements(risk_score)
        
        print(f"Risk Score: {risk_score:.2f}")
        print(f"Required Factors: {required_factors}")
        
        # Verificar que todos los factores requeridos estén presentes
        for factor in required_factors:
            if factor not in provided_factors:
                return False, f"Missing required factor: {factor}"
            
            # Verificar cada factor
            if not self.verify_factor(username, factor, provided_factors[factor]):
                return False, f"Invalid {factor}"
        
        # Actualizar perfil de usuario
        self.update_user_profile(username, request_context)
        
        return True, "Authentication successful"
    
    def verify_factor(self, username, factor_type, factor_value):
        """Verificar factor específico de autenticación"""
        # Implementación simplificada
        verification_methods = {
            'password': lambda u, v: True,  # Implementar hash verification
            'sms_otp': lambda u, v: len(v) == 6 and v.isdigit(),
            'totp': lambda u, v: len(v) == 6 and v.isdigit(),
            'biometric': lambda u, v: v.get('confidence', 0) > 0.8,
            'device_verification': lambda u, v: v.get('verified', False)
        }
        
        return verification_methods.get(factor_type, lambda u, v: False)(username, factor_value)
    
    def update_user_profile(self, username, context):
        """Actualizar perfil de comportamiento del usuario"""
        if username not in self.user_profiles:
            self.user_profiles[username] = {
                'countries': [],
                'devices': [],
                'login_hours': []
            }
        
        profile = self.user_profiles[username]
        
        # Actualizar países
        try:
            response = self.geo_reader.city(context['ip_address'])
            country = response.country.iso_code
            if country not in profile['countries']:
                profile['countries'].append(country)
        except:
            pass
        
        # Actualizar dispositivos
        device = context.get('device_fingerprint')
        if device and device not in profile['devices']:
            profile['devices'].append(device)
        
        # Actualizar horarios
        hour = datetime.now().hour
        if hour not in profile['login_hours']:
            profile['login_hours'].append(hour)

# Ejemplo de uso
adaptive_auth = AdaptiveAuth()

# Simular solicitud de autenticación
request_context = {
    'ip_address': '192.168.1.1',
    'device_fingerprint': 'chrome_windows_fp123',
    'recent_failures': 1
}

provided_factors = {
    'password': 'user_password',
    'sms_otp': '123456'
}

success, message = adaptive_auth.authenticate_adaptive(
    'john_doe', provided_factors, request_context
)
print(f"Result: {message}")
```

---

## Tecnologías de Autenticación

### Contraseñas Tradicionales

#### Gestión Segura de Contraseñas
```python
import hashlib
import secrets
import string
from argon2 import PasswordHasher
from argon2.exceptions import VerifyMismatchError

class SecurePasswordManager:
    def __init__(self):
        self.ph = PasswordHasher()
        self.password_history = {}  # Historial de contraseñas por usuario
        
    def generate_strong_password(self, length=16, include_symbols=True):
        """Generar contraseña segura aleatoria"""
        characters = string.ascii_letters + string.digits
        if include_symbols:
            characters += "!@#$%^&*"
        
        password = ''.join(secrets.choice(characters) for _ in range(length))
        return password
    
    def validate_password_strength(self, password):
        """Validar fortaleza de contraseña"""
        issues = []
        
        if len(password) < 12:
            issues.append("Password must be at least 12 characters long")
        
        if not any(c.islower() for c in password):
            issues.append("Password must contain lowercase letters")
        
        if not any(c.isupper() for c in password):
            issues.append("Password must contain uppercase letters")
        
        if not any(c.isdigit() for c in password):
            issues.append("Password must contain numbers")
        
        if not any(c in "!@#$%^&*()_+-=[]{}|;:,.<>?" for c in password):
            issues.append("Password must contain special characters")
        
        # Verificar patrones comunes
        common_patterns = ['123', 'abc', 'password', 'qwerty']
        if any(pattern in password.lower() for pattern in common_patterns):
            issues.append("Password contains common patterns")
        
        return len(issues) == 0, issues
    
    def hash_password(self, password):
        """Crear hash seguro usando Argon2"""
        return self.ph.hash(password)
    
    def verify_password(self, password, hash):
        """Verificar contraseña contra hash"""
        try:
            self.ph.verify(hash, password)
            return True
        except VerifyMismatchError:
            return False
    
    def check_password_reuse(self, username, new_password):
        """Verificar reutilización de contraseñas"""
        if username not in self.password_history:
            return True
        
        history = self.password_history[username]
        for old_hash in history:
            if self.verify_password(new_password, old_hash):
                return False
        return True
    
    def update_password(self, username, old_password, new_password):
        """Actualizar contraseña con validaciones"""
        # Validar fortaleza de nueva contraseña
        is_strong, issues = self.validate_password_strength(new_password)
        if not is_strong:
            return False, f"Password validation failed: {'; '.join(issues)}"
        
        # Verificar que no sea reutilizada
        if not self.check_password_reuse(username, new_password):
            return False, "Password has been used recently"
        
        # Hash de nueva contraseña
        new_hash = self.hash_password(new_password)
        
        # Actualizar historial
        if username not in self.password_history:
            self.password_history[username] = []
        
        self.password_history[username].append(new_hash)
        
        # Mantener solo últimas 12 contraseñas en historial
        if len(self.password_history[username]) > 12:
            self.password_history[username] = self.password_history[username][-12:]
        
        return True, "Password updated successfully"

# Ejemplo de uso
password_manager = SecurePasswordManager()

# Generar contraseña fuerte
strong_password = password_manager.generate_strong_password()
print(f"Generated password: {strong_password}")

# Validar contraseña
is_valid, issues = password_manager.validate_password_strength("weak")
print(f"Password validation: {is_valid}, Issues: {issues}")

# Hash y verificación
password_hash = password_manager.hash_password("MyStrongP@ssw0rd123")
is_valid = password_manager.verify_password("MyStrongP@ssw0rd123", password_hash)
print(f"Password verification: {is_valid}")
```

### Biometría

#### Implementación de Autenticación Biométrica
```python
import cv2
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity
import hashlib

class BiometricAuth:
    def __init__(self):
        self.face_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + 'haarcascade_frontalface_default.xml')
        self.registered_faces = {}
        self.threshold = 0.8
    
    def capture_face(self, user_id):
        """Capturar imagen facial para registro"""
        cap = cv2.VideoCapture(0)
        faces_captured = []
        
        print("Press SPACE to capture face, ESC to finish")
        
        while len(faces_captured) < 5:  # Capturar 5 muestras
            ret, frame = cap.read()
            if not ret:
                break
            
            gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
            faces = self.face_cascade.detectMultiScale(gray, 1.3, 5)
            
            for (x, y, w, h) in faces:
                cv2.rectangle(frame, (x, y), (x+w, y+h), (255, 0, 0), 2)
                face_roi = gray[y:y+h, x:x+w]
                
                # Mostrar frame
                cv2.imshow('Face Capture', frame)
                
                key = cv2.waitKey(1) & 0xFF
                if key == 32:  # SPACE key
                    if face_roi.size > 0:
                        face_resized = cv2.resize(face_roi, (100, 100))
                        faces_captured.append(face_resized.flatten())
                        print(f"Face {len(faces_captured)} captured")
                elif key == 27:  # ESC key
                    break
        
        cap.release()
        cv2.destroyAllWindows()
        
        if faces_captured:
            # Promedio de las muestras capturadas
            face_template = np.mean(faces_captured, axis=0)
            self.registered_faces[user_id] = face_template
            return True
        return False
    
    def authenticate_face(self, user_id):
        """Autenticar usuario por reconocimiento facial"""
        if user_id not in self.registered_faces:
            return False, "User not registered"
        
        cap = cv2.VideoCapture(0)
        authenticated = False
        attempts = 0
        max_attempts = 30  # 30 frames para autenticación
        
        while attempts < max_attempts and not authenticated:
            ret, frame = cap.read()
            if not ret:
                break
            
            gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
            faces = self.face_cascade.detectMultiScale(gray, 1.3, 5)
            
            for (x, y, w, h) in faces:
                cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
                face_roi = gray[y:y+h, x:x+w]
                
                if face_roi.size > 0:
                    face_resized = cv2.resize(face_roi, (100, 100))
                    face_vector = face_resized.flatten().reshape(1, -1)
                    template_vector = self.registered_faces[user_id].reshape(1, -1)
                    
                    # Calcular similaridad
                    similarity = cosine_similarity(face_vector, template_vector)[0][0]
                    
                    if similarity > self.threshold:
                        cv2.putText(frame, f"AUTH OK: {similarity:.2f}", (x, y-10), 
                                  cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 255, 0), 1)
                        authenticated = True
                    else:
                        cv2.putText(frame, f"AUTH FAIL: {similarity:.2f}", (x, y-10), 
                                  cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 255), 1)
            
            cv2.imshow('Face Authentication', frame)
            if cv2.waitKey(1) & 0xFF == 27:  # ESC to exit
                break
            
            attempts += 1
        
        cap.release()
        cv2.destroyAllWindows()
        
        return authenticated, "Authentication successful" if authenticated else "Authentication failed"

# Simulación de autenticación por huella dactilar
class FingerprintAuth:
    def __init__(self):
        self.enrolled_prints = {}
    
    def enroll_fingerprint(self, user_id, fingerprint_data):
        """Registrar huella dactilar (simulado)"""
        # En implementación real, usar sensor de huella
        minutiae = self.extract_minutiae(fingerprint_data)
        self.enrolled_prints[user_id] = minutiae
        return True
    
    def extract_minutiae(self, fingerprint_image):
        """Extraer características de minutiae (simulado)"""
        # En implementación real, usar algoritmos de extracción de minutiae
        # Simulamos con hash de la imagen
        return hashlib.sha256(fingerprint_image).hexdigest()
    
    def verify_fingerprint(self, user_id, fingerprint_data):
        """Verificar huella dactilar"""
        if user_id not in self.enrolled_prints:
            return False, "User not enrolled"
        
        minutiae = self.extract_minutiae(fingerprint_data)
        enrolled_minutiae = self.enrolled_prints[user_id]
        
        # En implementación real, comparar minutiae con tolerancia
        match = minutiae == enrolled_minutiae
        
        return match, "Fingerprint verified" if match else "Fingerprint mismatch"

# Ejemplo de uso combinado
class MultiBiometricAuth:
    def __init__(self):
        self.face_auth = BiometricAuth()
        self.fingerprint_auth = FingerprintAuth()
    
    def register_user(self, user_id):
        """Registro biométrico completo"""
        print(f"Registering biometric data for {user_id}")
        
        # Registro facial
        face_success = self.face_auth.capture_face(user_id)
        
        # Registro de huella (simulado)
        dummy_fingerprint = b"fingerprint_data_" + user_id.encode()
        fp_success = self.fingerprint_auth.enroll_fingerprint(user_id, dummy_fingerprint)
        
        return face_success and fp_success
    
    def authenticate_multibiometric(self, user_id):
        """Autenticación biométrica múltiple"""
        # Autenticación facial
        face_result, face_msg = self.face_auth.authenticate_face(user_id)
        
        # Autenticación por huella (simulado)
        dummy_fingerprint = b"fingerprint_data_" + user_id.encode()
        fp_result, fp_msg = self.fingerprint_auth.verify_fingerprint(user_id, dummy_fingerprint)
        
        # Requiere ambos métodos para autenticación completa
        success = face_result and fp_result
        message = f"Face: {face_msg}, Fingerprint: {fp_msg}"
        
        return success, message
```

### Tokens de Hardware

#### Implementación con YubiKey
```python
from yubico_client import Yubico
import binascii

class HardwareTokenAuth:
    def __init__(self, client_id, secret_key):
        self.yubico_client = Yubico(client_id, secret_key)
        self.registered_tokens = {}
    
    def register_yubikey(self, username, yubikey_otp):
        """Registrar YubiKey para usuario"""
        try:
            # Verificar OTP válido
            status = self.yubico_client.verify(yubikey_otp)
            if status:
                # Extraer public ID del token
                public_id = yubikey_otp[:12]
                self.registered_tokens[username] = public_id
                return True, f"YubiKey registered for {username}"
        except Exception as e:
            return False, f"Registration failed: {str(e)}"
        
        return False, "Invalid YubiKey OTP"
    
    def verify_yubikey(self, username, yubikey_otp):
        """Verificar YubiKey OTP"""
        if username not in self.registered_tokens:
            return False, "User not registered"
        
        try:
            # Verificar que el public ID coincida
            public_id = yubikey_otp[:12]
            if public_id != self.registered_tokens[username]:
                return False, "Wrong YubiKey for user"
            
            # Verificar OTP con servidor Yubico
            status = self.yubico_client.verify(yubikey_otp)
            return status, "YubiKey verified" if status else "Invalid OTP"
            
        except Exception as e:
            return False, f"Verification error: {str(e)}"

# Implementación de U2F/FIDO2
class FIDO2Auth:
    def __init__(self):
        self.registered_keys = {}
    
    def register_fido2_key(self, username, credential_data):
        """Registrar clave FIDO2"""
        # En implementación real, usar librerías FIDO2
        # Aquí simulamos el proceso
        
        credential_id = binascii.hexlify(credential_data.get('id', b'dummy')).decode()
        public_key = credential_data.get('public_key', b'dummy_key')
        
        if username not in self.registered_keys:
            self.registered_keys[username] = []
        
        self.registered_keys[username].append({
            'credential_id': credential_id,
            'public_key': public_key,
            'counter': 0
        })
        
        return True, f"FIDO2 key registered for {username}"
    
    def verify_fido2_assertion(self, username, assertion_data):
        """Verificar aserción FIDO2"""
        if username not in self.registered_keys:
            return False, "No keys registered for user"
        
        credential_id = assertion_data.get('credential_id')
        signature = assertion_data.get('signature')
        counter = assertion_data.get('counter', 0)
        
        # Buscar credencial registrada
        for key_data in self.registered_keys[username]:
            if key_data['credential_id'] == credential_id:
                # Verificar contador (protección contra replay)
                if counter <= key_data['counter']:
                    return False, "Invalid counter value"
                
                # En implementación real, verificar firma criptográfica
                # Aquí simulamos verificación exitosa
                key_data['counter'] = counter
                return True, "FIDO2 authentication successful"
        
        return False, "Credential not found"

# Ejemplo de uso integrado
class HybridTokenAuth:
    def __init__(self):
        self.yubikey_auth = HardwareTokenAuth("dummy_client", "dummy_secret")
        self.fido2_auth = FIDO2Auth()
    
    def register_user_tokens(self, username):
        """Registrar múltiples tokens para usuario"""
        print(f"Token registration for {username}")
        
        # Simular registro YubiKey
        yubikey_otp = input("Touch YubiKey: ")
        yubi_success, yubi_msg = self.yubikey_auth.register_yubikey(username, yubikey_otp)
        print(f"YubiKey: {yubi_msg}")
        
        # Simular registro FIDO2
        fido2_credential = {
            'id': b'credential_123',
            'public_key': b'public_key_data'
        }
        fido2_success, fido2_msg = self.fido2_auth.register_fido2_key(username, fido2_credential)
        print(f"FIDO2: {fido2_msg}")
        
        return yubi_success or fido2_success
    
    def authenticate_with_tokens(self, username):
        """Autenticación con tokens hardware"""
        print(f"Hardware token authentication for {username}")
        
        token_type = input("Token type (yubikey/fido2): ").lower()
        
        if token_type == "yubikey":
            yubikey_otp = input("Touch YubiKey: ")
            return self.yubikey_auth.verify_yubikey(username, yubikey_otp)
        elif token_type == "fido2":
            # Simular aserción FIDO2
            assertion = {
                'credential_id': 'credential_123',
                'signature': b'signature_data',
                'counter': 1
            }
            return self.fido2_auth.verify_fido2_assertion(username, assertion)
        else:
            return False, "Unknown token type"
```

---

## Protocolos de Autenticación

### Kerberos

#### Funcionamiento del Protocolo Kerberos
```
Kerberos Authentication Flow:
┌─────────────────────────────────────────────────────────────┐
│                 Kerberos V5 Protocol                       │
│                                                             │
│ 1. AS-REQ: Authentication Server Request                   │
│ Client ────────────────────────→ AS (KDC)                  │
│        Username + Timestamp                                 │
│                                                             │
│ 2. AS-REP: Authentication Server Reply                     │
│ Client ←───────────────────────── AS (KDC)                 │
│        TGT + Session Key                                    │
│                                                             │
│ 3. TGS-REQ: Ticket Granting Server Request                │
│ Client ────────────────────────→ TGS (KDC)                 │
│        TGT + Service Request                                │
│                                                             │
│ 4. TGS-REP: Ticket Granting Server Reply                  │
│ Client ←───────────────────────── TGS (KDC)                │
│        Service Ticket                                       │
│                                                             │
│ 5. AP-REQ: Application Request                             │
│ Client ────────────────────────→ Service Server            │
│        Service Ticket + Authenticator                      │
│                                                             │
│ 6. AP-REP: Application Reply (optional)                    │
│ Client ←───────────────────────── Service Server           │
│        Mutual Authentication                                │
└─────────────────────────────────────────────────────────────┘

Key Components:
├── KDC (Key Distribution Center)
│   ├── AS (Authentication Server)
│   └── TGS (Ticket Granting Server)
├── Principal (User or Service)
├── Realm (Authentication Domain)
├── TGT (Ticket Granting Ticket)
└── Service Ticket
```

#### Implementación Kerberos Client
```python
import socket
import struct
import hashlib
from datetime import datetime, timedelta
import base64

class KerberosClient:
    def __init__(self, realm, kdc_host, kdc_port=88):
        self.realm = realm
        self.kdc_host = kdc_host
        self.kdc_port = kdc_port
        self.tgt = None
        self.session_key = None
    
    def get_password_hash(self, password, salt):
        """Generar hash de contraseña para Kerberos"""
        # Simplificado - en implementación real usar PBKDF2
        return hashlib.pbkdf2_hmac('sha256', password.encode(), salt, 100000)
    
    def build_as_req(self, username, password):
        """Construir Authentication Server Request"""
        # Estructura simplificada de AS-REQ
        req_data = {
            'pvno': 5,  # Kerberos version
            'msg-type': 10,  # AS-REQ
            'req-body': {
                'kdc-options': 0x40000000,  # FORWARDABLE
                'cname': {
                    'name-type': 1,  # NT-PRINCIPAL
                    'name-string': [username]
                },
                'realm': self.realm,
                'sname': {
                    'name-type': 2,  # NT-SRV-INST
                    'name-string': ['krbtgt', self.realm]
                },
                'till': datetime.now() + timedelta(hours=8),
                'nonce': 12345,  # Random nonce
                'etype': [18]  # AES256-CTS-HMAC-SHA1-96
            }
        }
        
        # En implementación real, usar ASN.1 DER encoding
        return str(req_data).encode()
    
    def send_kdc_request(self, request_data):
        """Enviar solicitud a KDC"""
        try:
            sock = socket.socket(socket.AF_INET, socket.SOCK_UDP)
            sock.settimeout(10)
            
            # Enviar solicitud
            sock.sendto(request_data, (self.kdc_host, self.kdc_port))
            
            # Recibir respuesta
            response, addr = sock.recvfrom(4096)
            sock.close()
            
            return response
        except Exception as e:
            print(f"KDC communication error: {e}")
            return None
    
    def authenticate(self, username, password):
        """Proceso de autenticación completo"""
        print(f"Authenticating {username}@{self.realm}")
        
        # Paso 1: AS-REQ
        as_req = self.build_as_req(username, password)
        as_rep = self.send_kdc_request(as_req)
        
        if not as_rep:
            return False, "Failed to communicate with KDC"
        
        # Paso 2: Procesar AS-REP (simulado)
        if self.process_as_rep(as_rep, password):
            print("✓ TGT obtained successfully")
            return True, "Authentication successful"
        else:
            return False, "Authentication failed"
    
    def process_as_rep(self, as_rep, password):
        """Procesar Authentication Server Reply"""
        # En implementación real, decodificar ASN.1 y descifrar TGT
        # Aquí simulamos el proceso
        
        # Simular extracción de TGT y session key
        self.tgt = base64.b64encode(as_rep[:100]).decode()
        self.session_key = hashlib.sha256(password.encode()).digest()[:16]
        
        return True
    
    def get_service_ticket(self, service_name):
        """Obtener ticket para servicio específico"""
        if not self.tgt:
            return False, "No TGT available"
        
        print(f"Requesting service ticket for {service_name}")
        
        # Construir TGS-REQ
        tgs_req_data = {
            'pvno': 5,
            'msg-type': 12,  # TGS-REQ
            'tgt': self.tgt,
            'service': service_name
        }
        
        tgs_req = str(tgs_req_data).encode()
        tgs_rep = self.send_kdc_request(tgs_req)
        
        if tgs_rep:
            # Simular procesamiento de service ticket
            service_ticket = base64.b64encode(tgs_rep[:80]).decode()
            return True, service_ticket
        
        return False, "Failed to obtain service ticket"

# Ejemplo de uso
kerberos_client = KerberosClient(realm="EXAMPLE.COM", kdc_host="192.168.1.10")
success, message = kerberos_client.authenticate("john.doe", "password123")
print(f"Authentication result: {message}")

if success:
    ticket_success, service_ticket = kerberos_client.get_service_ticket("HTTP/webserver.example.com")
    if ticket_success:
        print(f"Service ticket obtained: {service_ticket[:50]}...")
```

### LDAP Authentication

#### Cliente LDAP para Autenticación
```python
import ldap3
from ldap3 import Server, Connection, ALL, NTLM, SIMPLE
import ssl

class LDAPAuth:
    def __init__(self, server_uri, base_dn, use_tls=True):
        self.server_uri = server_uri
        self.base_dn = base_dn
        self.use_tls = use_tls
        self.connection = None
    
    def connect_admin(self, admin_dn, admin_password):
        """Conectar con credenciales administrativas"""
        try:
            server = Server(self.server_uri, get_info=ALL, use_ssl=self.use_tls)
            self.connection = Connection(
                server, 
                user=admin_dn, 
                password=admin_password,
                authentication=SIMPLE,
                auto_bind=True
            )
            return True, "Admin connection successful"
        except Exception as e:
            return False, f"Admin connection failed: {str(e)}"
    
    def search_user(self, username):
        """Buscar usuario en directorio LDAP"""
        if not self.connection:
            return None, "No LDAP connection"
        
        search_filter = f"(|(uid={username})(sAMAccountName={username})(userPrincipalName={username}@*))"
        
        try:
            self.connection.search(
                search_base=self.base_dn,
                search_filter=search_filter,
                attributes=['dn', 'uid', 'cn', 'mail', 'memberOf', 'accountLocked']
            )
            
            if len(self.connection.entries) == 1:
                return self.connection.entries[0], "User found"
            elif len(self.connection.entries) == 0:
                return None, "User not found"
            else:
                return None, "Multiple users found"
        except Exception as e:
            return None, f"Search error: {str(e)}"
    
    def authenticate_user(self, username, password):
        """Autenticar usuario contra LDAP"""
        # Buscar usuario primero
        user_entry, search_msg = self.search_user(username)
        if not user_entry:
            return False, search_msg
        
        user_dn = str(user_entry.dn)
        
        # Verificar si la cuenta está bloqueada
        if hasattr(user_entry, 'accountLocked') and user_entry.accountLocked:
            return False, "Account is locked"
        
        try:
            # Intentar bind con credenciales de usuario
            server = Server(self.server_uri, get_info=ALL, use_ssl=self.use_tls)
            user_connection = Connection(
                server,
                user=user_dn,
                password=password,
                authentication=SIMPLE,
                auto_bind=True
            )
            
            # Si llegamos aquí, la autenticación fue exitosa
            user_connection.unbind()
            
            # Obtener información adicional del usuario
            user_info = {
                'dn': user_dn,
                'username': username,
                'cn': str(user_entry.cn) if hasattr(user_entry, 'cn') else '',
                'email': str(user_entry.mail) if hasattr(user_entry, 'mail') else '',
                'groups': [str(group) for group in user_entry.memberOf] if hasattr(user_entry, 'memberOf') else []
            }
            
            return True, user_info
            
        except Exception as e:
            return False, f"Authentication failed: {str(e)}"
    
    def get_user_groups(self, username):
        """Obtener grupos del usuario"""
        user_entry, search_msg = self.search_user(username)
        if not user_entry:
            return [], search_msg
        
        groups = []
        if hasattr(user_entry, 'memberOf'):
            for group_dn in user_entry.memberOf:
                # Extraer nombre del grupo del DN
                group_name = group_dn.split(',')[0].split('=')[1]
                groups.append(group_name)
        
        return groups, "Groups retrieved successfully"
    
    def change_user_password(self, username, old_password, new_password):
        """Cambiar contraseña de usuario"""
        user_entry, search_msg = self.search_user(username)
        if not user_entry:
            return False, search_msg
        
        user_dn = str(user_entry.dn)
        
        try:
            # Conectar con credenciales actuales
            server = Server(self.server_uri, get_info=ALL, use_ssl=self.use_tls)
            user_connection = Connection(
                server,
                user=user_dn,
                password=old_password,
                authentication=SIMPLE,
                auto_bind=True
            )
            
            # Cambiar contraseña
            result = user_connection.extend.microsoft.modify_password(user_dn, new_password, old_password)
            user_connection.unbind()
            
            if result:
                return True, "Password changed successfully"
            else:
                return False, "Password change failed"
                
        except Exception as e:
            return False, f"Password change error: {str(e)}"

# Ejemplo de uso
ldap_auth = LDAPAuth(
    server_uri="ldaps://dc.example.com:636",
    base_dn="dc=example,dc=com",
    use_tls=True
)

# Conectar como administrador
admin_success, admin_msg = ldap_auth.connect_admin(
    "cn=admin,dc=example,dc=com", 
    "admin_password"
)

if admin_success:
    # Autenticar usuario
    auth_success, auth_result = ldap_auth.authenticate_user("john.doe", "user_password")
    
    if auth_success:
        print(f"Authentication successful: {auth_result}")
        
        # Obtener grupos del usuario
        groups, group_msg = ldap_auth.get_user_groups("john.doe")
        print(f"User groups: {groups}")
    else:
        print(f"Authentication failed: {auth_result}")
```

### RADIUS Authentication

#### Servidor RADIUS Básico
```python
import socket
import struct
import hashlib
import secrets
from datetime import datetime

class RADIUSServer:
    def __init__(self, host='localhost', port=1812, secret='testing123'):
        self.host = host
        self.port = port
        self.secret = secret.encode()
        self.users = {
            'user1': 'password1',
            'user2': 'password2',
            'admin': 'admin123'
        }
        self.packet_types = {
            1: 'Access-Request',
            2: 'Access-Accept',
            3: 'Access-Reject',
            4: 'Accounting-Request',
            5: 'Accounting-Response'
        }
    
    def create_radius_packet(self, code, identifier, attributes=None):
        """Crear paquete RADIUS"""
        if attributes is None:
            attributes = b''
        
        # Generar authenticator aleatorio para Access-Accept/Reject
        if code in [2, 3]:
            authenticator = secrets.token_bytes(16)
        else:
            authenticator = b'\x00' * 16
        
        # Calcular longitud total
        length = 20 + len(attributes)
        
        # Construir paquete
        packet = struct.pack('!BBH16s', code, identifier, length, authenticator)
        packet += attributes
        
        return packet
    
    def parse_radius_packet(self, data):
        """Parsear paquete RADIUS recibido"""
        if len(data) < 20:
            return None
        
        # Extraer header
        code, identifier, length, authenticator = struct.unpack('!BBH16s', data[:20])
        
        # Extraer atributos
        attributes = {}
        offset = 20
        
        while offset < len(data):
            if offset + 2 > len(data):
                break
                
            attr_type, attr_length = struct.unpack('!BB', data[offset:offset+2])
            
            if attr_length < 2 or offset + attr_length > len(data):
                break
            
            attr_value = data[offset+2:offset+attr_length]
            attributes[attr_type] = attr_value
            offset += attr_length
        
        return {
            'code': code,
            'identifier': identifier,
            'length': length,
            'authenticator': authenticator,
            'attributes': attributes
        }
    
    def create_attribute(self, attr_type, value):
        """Crear atributo RADIUS"""
        if isinstance(value, str):
            value = value.encode()
        
        length = len(value) + 2
        return struct.pack('!BB', attr_type, length) + value
    
    def verify_request_authenticator(self, packet_data, received_auth):
        """Verificar Request Authenticator"""
        # Para Access-Request, verificar MD5 hash
        packet_without_auth = packet_data[:4] + b'\x00' * 16 + packet_data[20:]
        expected_auth = hashlib.md5(packet_without_auth + self.secret).digest()
        
        # En implementación real, el Request Authenticator es aleatorio
        # y se verifica diferente. Aquí simplificamos.
        return True
    
    def create_response_authenticator(self, response_packet, request_auth):
        """Crear Response Authenticator"""
        # Response Auth = MD5(Code + ID + Length + Request Auth + Response Attributes + Secret)
        temp_packet = response_packet[:4] + request_auth + response_packet[20:]
        return hashlib.md5(temp_packet + self.secret).digest()
    
    def authenticate_user(self, username, password):
        """Autenticar usuario"""
        if username in self.users:
            return self.users[username] == password
        return False
    
    def handle_access_request(self, packet):
        """Procesar Access-Request"""
        attributes = packet['attributes']
        
        # Extraer username y password
        username = attributes.get(1, b'').decode('utf-8', errors='ignore')
        password = attributes.get(2, b'').decode('utf-8', errors='ignore')
        
        print(f"Authentication attempt: {username}")
        
        if self.authenticate_user(username, password):
            # Access-Accept
            print(f"✓ Authentication successful for {username}")
            
            # Crear atributos de respuesta
            reply_attributes = b''
            reply_attributes += self.create_attribute(18, f"Welcome {username}!")  # Reply-Message
            reply_attributes += self.create_attribute(27, "3600")  # Session-Timeout
            
            response = self.create_radius_packet(2, packet['identifier'], reply_attributes)
            
            # Actualizar Response Authenticator
            response_auth = self.create_response_authenticator(response, packet['authenticator'])
            response = response[:4] + response_auth + response[20:]
            
            return response
        else:
            # Access-Reject
            print(f"✗ Authentication failed for {username}")
            
            reply_attributes = b''
            reply_attributes += self.create_attribute(18, "Invalid credentials")  # Reply-Message
            
            response = self.create_radius_packet(3, packet['identifier'], reply_attributes)
            
            # Actualizar Response Authenticator
            response_auth = self.create_response_authenticator(response, packet['authenticator'])
            response = response[:4] + response_auth + response[20:]
            
            return response
    
    def start_server(self):
        """Iniciar servidor RADIUS"""
        sock = socket.socket(socket.AF_INET, socket.SOCK_UDP)
        sock.bind((self.host, self.port))
        
        print(f"RADIUS Server started on {self.host}:{self.port}")
        
        while True:
            try:
                data, addr = sock.recvfrom(4096)
                print(f"Received packet from {addr}")
                
                packet = self.parse_radius_packet(data)
                if packet:
                    print(f"Packet type: {self.packet_types.get(packet['code'], 'Unknown')}")
                    
                    if packet['code'] == 1:  # Access-Request
                        response = self.handle_access_request(packet)
                        if response:
                            sock.sendto(response, addr)
                    else:
                        print(f"Unsupported packet type: {packet['code']}")
                else:
                    print("Invalid RADIUS packet received")
                    
            except Exception as e:
                print(f"Error processing packet: {e}")

# Cliente RADIUS para pruebas
class RADIUSClient:
    def __init__(self, server_host, server_port=1812, secret='testing123'):
        self.server_host = server_host
        self.server_port = server_port
        self.secret = secret.encode()
    
    def authenticate(self, username, password):
        """Enviar Access-Request"""
        sock = socket.socket(socket.AF_INET, socket.SOCK_UDP)
        sock.settimeout(5)
        
        try:
            # Crear atributos
            attributes = b''
            attributes += self.create_attribute(1, username)  # User-Name
            attributes += self.create_attribute(2, password)  # User-Password (should be encrypted)
            attributes += self.create_attribute(4, "192.168.1.100")  # NAS-IP-Address
            
            # Crear paquete Access-Request
            identifier = secrets.randbelow(256)
            packet = struct.pack('!BBH16s', 1, identifier, 20 + len(attributes), b'\x00' * 16)
            packet += attributes
            
            # Enviar solicitud
            sock.sendto(packet, (self.server_host, self.server_port))
            
            # Recibir respuesta
            response_data, addr = sock.recvfrom(4096)
            
            if len(response_data) >= 20:
                code = response_data[0]
                if code == 2:
                    return True, "Access-Accept"
                elif code == 3:
                    return False, "Access-Reject"
            
            return False, "Invalid response"
            
        except socket.timeout:
            return False, "Request timeout"
        except Exception as e:
            return False, f"Error: {str(e)}"
        finally:
            sock.close()
    
    def create_attribute(self, attr_type, value):
        """Crear atributo RADIUS"""
        if isinstance(value, str):
            value = value.encode()
        
        length = len(value) + 2
        return struct.pack('!BB', attr_type, length) + value

# Ejemplo de uso
if __name__ == "__main__":
    import threading
    
    # Iniciar servidor RADIUS en hilo separado
    server = RADIUSServer()
    server_thread = threading.Thread(target=server.start_server)
    server_thread.daemon = True
    server_thread.start()
    
    # Esperar un poco para que el servidor inicie
    import time
    time.sleep(1)
    
    # Probar cliente
    client = RADIUSClient('localhost')
    
    # Prueba de autenticación exitosa
    success, message = client.authenticate('user1', 'password1')
    print(f"Test 1: {success} - {message}")
    
    # Prueba de autenticación fallida
    success, message = client.authenticate('user1', 'wrong_password')
    print(f"Test 2: {success} - {message}")
```

Continuaré con el resto del contenido del Tema 8 en la siguiente respuesta...

### Gestión de Identidades
- Lifecycle de identidades
- Provisioning y deprovisioning
- Auditoría de accesos
- Compliance y regulaciones

## Objetivos de Aprendizaje
- [ ] Comprender los principios de autenticación
- [ ] Implementar políticas de contraseñas seguras
- [ ] Configurar autenticación multifactor
- [ ] Gestionar permisos efectivamente
- [ ] Evaluar sistemas de autenticación

## Recursos Adicionales
- Herramientas de gestión de identidad
- Estándares de autenticación
- Mejores prácticas de la industria

## Actividades
- Configuración de MFA
- Auditoría de permisos
- Implementación de políticas de contraseñas
- Evaluación de sistemas biométricos
