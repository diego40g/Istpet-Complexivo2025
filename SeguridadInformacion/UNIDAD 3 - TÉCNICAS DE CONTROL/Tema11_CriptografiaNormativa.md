# Tema 11: Criptografía y Normativa

## Índice de Contenidos
1. [Criptografía Avanzada](#criptografía-avanzada)
2. [Implementación de Criptografía](#implementación-de-criptografía)
3. [Criptoanálisis](#criptoanálisis)
4. [Aplicaciones Criptográficas](#aplicaciones-criptográficas)
5. [Normativa para la Protección de Datos](#normativa-para-la-protección-de-datos)
6. [RGPD (Reglamento General de Protección de Datos)](#rgpd-reglamento-general-de-protección-de-datos)
7. [Otras Regulaciones Importantes](#otras-regulaciones-importantes)
8. [Implementación de Compliance](#implementación-de-compliance)
9. [Auditoría y Certificación](#auditoría-y-certificación)

---

## Criptografía Avanzada

### Algoritmos Criptográficos Modernos

#### Criptografía Simétrica Avanzada
La **criptografía simétrica** utiliza la misma clave para cifrar y descifrar datos. Los algoritmos modernos proporcionan alta velocidad y eficiencia computacional.

**Algoritmos de Cifrado en Bloque:**
```
Advanced Encryption Standard (AES):
├── AES-128 (clave de 128 bits)
├── AES-192 (clave de 192 bits)
└── AES-256 (clave de 256 bits)

Modos de Operación:
├── CBC (Cipher Block Chaining)
├── CTR (Counter Mode)
├── GCM (Galois/Counter Mode)
├── XTS (XEX-based Tweaked CodeBook)
└── OCB (Offset CodeBook Mode)
```

**Características de AES:**
- Algoritmo estándar FIPS-197
- Resistente a ataques conocidos
- Implementación eficiente en hardware/software
- Amplia adopción industrial

#### Criptografía Asimétrica Moderna
**RSA (Rivest-Shamir-Adleman):**
```
RSA Key Sizes:
├── 1024 bits (Deprecated - Insecure)
├── 2048 bits (Current minimum standard)
├── 3072 bits (Recommended for long-term)
└── 4096 bits (High security applications)

RSA Applications:
├── Digital signatures
├── Key exchange
├── Certificate authorities
└── Secure communications
```

**Elliptic Curve Cryptography (ECC):**
```
ECC Advantages:
├── Smaller key sizes for equivalent security
├── Faster computations
├── Lower power consumption
├── Reduced storage requirements
└── Mobile-friendly implementations

Popular Curves:
├── P-256 (secp256r1) - NIST standard
├── P-384 (secp384r1) - Higher security
├── Curve25519 - High-speed applications
└── Ed25519 - Digital signatures
```

### Funciones Hash Criptográficas

#### SHA (Secure Hash Algorithm) Family
```
SHA Family Evolution:
├── SHA-1 (160-bit) - DEPRECATED
│   ├── Collision vulnerabilities discovered
│   ├── No longer suitable for security
│   └── Replaced by SHA-2/SHA-3
├── SHA-2 Family
│   ├── SHA-224 (224-bit digest)
│   ├── SHA-256 (256-bit digest)
│   ├── SHA-384 (384-bit digest)
│   └── SHA-512 (512-bit digest)
└── SHA-3 Family (Keccak)
    ├── SHA3-224, SHA3-256, SHA3-384, SHA3-512
    ├── SHAKE128, SHAKE256 (Extendable output)
    └── Different internal structure from SHA-2
```

#### Aplicaciones de Hash Functions
**Integridad de Datos:**
```bash
# Verificación de integridad con SHA-256
sha256sum archivo.txt > archivo.txt.sha256
sha256sum -c archivo.txt.sha256

# Hash de contraseñas con salt
echo -n "password123salt456" | sha256sum
```

**Proof of Work (Blockchain):**
- Minería de criptomonedas
- Consenso distribuido
- Prevención de spam
- Rate limiting mechanisms

### Criptografía Cuántica

#### Fundamentos de Computación Cuántica
**Conceptos Básicos:**
```
Quantum Computing Principles:
├── Qubits (Quantum bits)
│   ├── Superposition states
│   ├── Entanglement phenomena
│   └── Quantum interference
├── Quantum Gates
│   ├── Hadamard gates
│   ├── Pauli gates (X, Y, Z)
│   └── CNOT gates
└── Quantum Algorithms
    ├── Shor's algorithm (factoring)
    ├── Grover's algorithm (search)
    └── Simon's algorithm (periodicity)
```

#### Amenaza Cuántica a la Criptografía Actual
**Algoritmos Vulnerables:**
```
Quantum Threat Assessment:
├── RSA Encryption
│   ├── Shor's algorithm breaks RSA
│   ├── Timeline: 10-30 years
│   └── Key sizes irrelevant
├── Elliptic Curve Cryptography
│   ├── Also vulnerable to Shor's algorithm
│   ├── Faster break than RSA
│   └── No classical defense
├── Discrete Logarithm Problems
│   ├── Diffie-Hellman key exchange
│   ├── ElGamal encryption
│   └── DSA signatures
└── Symmetric Cryptography
    ├── Grover's algorithm halves key strength
    ├── AES-128 → effectively 64-bit security
    └── AES-256 → effectively 128-bit security
```

#### Post-Quantum Cryptography
**NIST Post-Quantum Standards:**
```
PQC Algorithm Categories:
├── Lattice-based Cryptography
│   ├── CRYSTALS-Kyber (Key encapsulation)
│   ├── CRYSTALS-Dilithium (Digital signatures)
│   └── NTRU (Key exchange)
├── Code-based Cryptography
│   ├── Classic McEliece
│   └── BIKE (QC-LDPC)
├── Multivariate Cryptography
│   ├── Rainbow (Digital signatures)
│   └── GeMSS
└── Isogeny-based Cryptography
    ├── SIKE (Supersingular isogeny)
    └── CSIDH (Commutative SIDH)
```

### Protocolos Criptográficos

#### Perfect Forward Secrecy (PFS)
**Implementación de PFS:**
- Diffie-Hellman ephemeral (DHE)
- Elliptic Curve Diffie-Hellman ephemeral (ECDHE)
- Generación de nuevas claves por sesión
- Protección contra compromiso de claves privadas a largo plazo

#### Zero-Knowledge Proofs
**Tipos de Zero-Knowledge:**
```
ZK Proof Systems:
├── Interactive Proofs
│   ├── Prover-Verifier interaction
│   ├── Multiple rounds of communication
│   └── Fiat-Shamir heuristic
├── Non-Interactive Proofs (NIZK)
│   ├── Single message proof
│   ├── Common reference string
│   └── Practical implementations
└── Succinct Proofs (zk-SNARKs)
    ├── Constant-size proofs
    ├── Blockchain applications
    └── Privacy-preserving protocols
```

---

## Implementación de Criptografía

### Bibliotecas Criptográficas

#### OpenSSL
**Características Principales:**
```
OpenSSL Capabilities:
├── Symmetric Encryption (AES, DES, 3DES, ChaCha20)
├── Asymmetric Encryption (RSA, ECC, DSA)
├── Hash Functions (SHA-1, SHA-2, SHA-3, MD5)
├── Message Authentication (HMAC, CMAC)
├── Key Derivation (PBKDF2, scrypt, Argon2)
├── Random Number Generation (CSPRNG)
├── Certificate Management (X.509)
└── Protocol Support (TLS, DTLS)
```

**Ejemplos de Uso:**
```bash
# Generar clave RSA
openssl genrsa -out private_key.pem 2048
openssl rsa -in private_key.pem -pubout -out public_key.pem

# Cifrado/descifrado simétrico
openssl enc -aes-256-cbc -salt -in archivo.txt -out archivo.enc -k password
openssl enc -aes-256-cbc -d -in archivo.enc -out archivo_dec.txt -k password

# Firma digital
openssl dgst -sha256 -sign private_key.pem -out signature.bin archivo.txt
openssl dgst -sha256 -verify public_key.pem -signature signature.bin archivo.txt

# Generar certificado autofirmado
openssl req -x509 -new -key private_key.pem -out certificate.crt -days 365
```

#### Libsodium
**Ventajas de Libsodium:**
- API simple y segura por defecto
- Resistente a timing attacks
- Implementaciones auditadas
- Soporte multiplataforma

```c
// Ejemplo en C con libsodium
#include <sodium.h>

// Cifrado autenticado
int encrypt_message(const char *message, unsigned char *ciphertext) {
    unsigned char key[crypto_secretbox_KEYBYTES];
    unsigned char nonce[crypto_secretbox_NONCEBYTES];
    
    crypto_secretbox_keygen(key);
    randombytes_buf(nonce, sizeof nonce);
    
    return crypto_secretbox_easy(ciphertext, 
                                (unsigned char *)message, 
                                strlen(message), 
                                nonce, key);
}
```

### API de Cifrado

#### Java Cryptography Architecture (JCA)
```java
// Cifrado AES en Java
import javax.crypto.*;
import javax.crypto.spec.*;

public class AESExample {
    public static byte[] encrypt(String plainText, SecretKey key) 
            throws Exception {
        Cipher cipher = Cipher.getInstance("AES/GCM/NoPadding");
        cipher.init(Cipher.ENCRYPT_MODE, key);
        
        return cipher.doFinal(plainText.getBytes());
    }
    
    public static String decrypt(byte[] cipherText, SecretKey key) 
            throws Exception {
        Cipher cipher = Cipher.getInstance("AES/GCM/NoPadding");
        cipher.init(Cipher.DECRYPT_MODE, key);
        
        byte[] plainText = cipher.doFinal(cipherText);
        return new String(plainText);
    }
}
```

#### .NET Cryptography Services
```csharp
// Cifrado RSA en C#
using System.Security.Cryptography;

public class RSAExample {
    public static byte[] EncryptRSA(string data, RSAParameters publicKey) {
        using (RSA rsa = RSA.Create()) {
            rsa.ImportParameters(publicKey);
            return rsa.Encrypt(Encoding.UTF8.GetBytes(data), 
                              RSAEncryptionPadding.OaepSHA256);
        }
    }
    
    public static string DecryptRSA(byte[] encryptedData, 
                                   RSAParameters privateKey) {
        using (RSA rsa = RSA.Create()) {
            rsa.ImportParameters(privateKey);
            byte[] decryptedData = rsa.Decrypt(encryptedData, 
                                              RSAEncryptionPadding.OaepSHA256);
            return Encoding.UTF8.GetString(decryptedData);
        }
    }
}
```

### Gestión de Claves Criptográficas

#### Key Management Lifecycle
```
Key Management Phases:
├── Generation
│   ├── Cryptographically secure random generation
│   ├── Sufficient entropy sources
│   ├── Hardware security modules (HSM)
│   └── Key strength requirements
├── Distribution
│   ├── Secure key exchange protocols
│   ├── Public key infrastructure (PKI)
│   ├── Key escrow considerations
│   └── Multi-party key agreement
├── Storage
│   ├── Hardware security modules
│   ├── Key wrapping techniques
│   ├── Secure enclaves
│   └── Access control mechanisms
├── Usage
│   ├── Key rotation policies
│   ├── Usage limitations
│   ├── Audit logging
│   └── Non-repudiation
├── Archival
│   ├── Long-term storage requirements
│   ├── Legal compliance needs
│   ├── Key recovery procedures
│   └── Backward compatibility
└── Destruction
    ├── Secure deletion methods
    ├── Cryptographic erasure
    ├── Hardware destruction
    └── Audit trails
```

#### Hardware Security Modules (HSM)
**Características de HSMs:**
```
HSM Capabilities:
├── Tamper-resistant hardware
├── FIPS 140-2 Level 3/4 certification
├── Hardware random number generation
├── Secure key storage and processing
├── High-performance cryptographic operations
├── Network-attached or PCIe card form factors
├── Role-based authentication
└── Audit logging and monitoring

Popular HSM Solutions:
├── Thales Luna Network HSMs
├── Entrust nShield HSMs
├── Utimaco CryptoServer
├── AWS CloudHSM
├── Azure Dedicated HSM
└── Google Cloud HSM
```

### Performance y Optimización

#### Optimización de Algoritmos
**Técnicas de Optimización:**
```
Cryptographic Optimization:
├── Hardware Acceleration
│   ├── AES-NI instructions (Intel)
│   ├── ARM cryptographic extensions
│   ├── GPU-based cryptography
│   └── Dedicated crypto processors
├── Software Optimizations
│   ├── Assembly language implementations
│   ├── Vectorized operations (SIMD)
│   ├── Cache-friendly algorithms
│   └── Parallel processing
├── Protocol Optimizations
│   ├── Session reuse (TLS)
│   ├── Bulk cipher preference
│   ├── Elliptic curves over RSA
│   └── Perfect forward secrecy balance
└── Implementation Considerations
    ├── Side-channel resistance
    ├── Constant-time operations
    ├── Memory-hard functions
    └── Timing attack mitigation
```

#### Benchmarking Criptográfico
```bash
# OpenSSL speed tests
openssl speed aes-256-cbc
openssl speed rsa2048
openssl speed ecdsa

# Resultados típicos en hardware moderno:
# AES-256-CBC: ~1-2 GB/s
# RSA-2048 sign: ~2000-5000 ops/sec
# ECDSA-256 sign: ~20000-50000 ops/sec
```

---

## Criptoanálisis

### Tipos de Ataques Criptográficos

#### Clasificación de Ataques
```
Cryptanalytic Attack Classification:
├── By Information Available
│   ├── Ciphertext-only attack
│   ├── Known-plaintext attack
│   ├── Chosen-plaintext attack
│   ├── Chosen-ciphertext attack
│   └── Adaptive chosen-ciphertext attack
├── By Attack Method
│   ├── Brute force (exhaustive key search)
│   ├── Dictionary attacks
│   ├── Frequency analysis
│   ├── Differential cryptanalysis
│   ├── Linear cryptanalysis
│   └── Algebraic attacks
├── By Computational Resources
│   ├── Classical attacks
│   ├── Quantum attacks
│   ├── Side-channel attacks
│   └── Social engineering attacks
└── By Attack Goals
    ├── Key recovery
    ├── Message recovery
    ├── Forgery attacks
    └── Distinguishing attacks
```

#### Ataques Específicos a Algoritmos
**Ataques a RSA:**
```
RSA Attack Vectors:
├── Mathematical Attacks
│   ├── Integer factorization (GNFS)
│   ├── Pollard's p-1 method
│   ├── Quadratic sieve
│   └── Elliptic curve factorization
├── Implementation Attacks
│   ├── Timing attacks
│   ├── Power analysis attacks
│   ├── Electromagnetic attacks
│   └── Acoustic cryptanalysis
├── Protocol Attacks
│   ├── Padding oracle attacks (PKCS#1)
│   ├── Bleichenbacher attacks
│   ├── ROBOT attacks
│   └── Common modulus attacks
└── Weak Key Attacks
    ├── Small exponent attacks
    ├── Related key attacks
    ├── Partial key exposure
    └── Fault injection attacks
```

**Ataques a AES:**
```
AES Attack Research:
├── Theoretical Attacks
│   ├── Square attack (reduced rounds)
│   ├── Boomerang attacks
│   ├── Impossible differential
│   └── Integral cryptanalysis
├── Side-channel Attacks
│   ├── Cache-timing attacks
│   ├── Power analysis (DPA/SPA)
│   ├── Electromagnetic emanations
│   └── Acoustic attacks
├── Implementation Vulnerabilities
│   ├── Key schedule weaknesses
│   ├── S-box implementation flaws
│   ├── Round function attacks
│   └── White-box cryptography breaks
└── Related-key Attacks
    ├── Biclique attacks
    ├── Key schedule cryptanalysis
    ├── Weak key classes
    └── Slide attacks
```

### Side-Channel Attacks

#### Tipos de Side-Channel Attacks
```
Side-Channel Attack Types:
├── Timing Attacks
│   ├── Measure execution time variations
│   ├── Exploit algorithmic branches
│   ├── Network timing analysis
│   └── Remote timing attacks
├── Power Analysis Attacks
│   ├── Simple Power Analysis (SPA)
│   ├── Differential Power Analysis (DPA)
│   ├── Correlation Power Analysis (CPA)
│   └── Template attacks
├── Electromagnetic Attacks
│   ├── EM emanation analysis
│   ├── Near-field probes
│   ├── Far-field analysis
│   └── Tempest attacks
├── Acoustic Attacks
│   ├── CPU acoustic emanations
│   ├── Keyboard acoustic analysis
│   ├── Printer acoustic reconstruction
│   └── Hard drive acoustic patterns
└── Fault Injection Attacks
    ├── Clock glitching
    ├── Voltage manipulation
    ├── Optical fault injection
    └── Body bias injection
```

#### Contramedidas Side-Channel
**Técnicas de Protección:**
```
Side-Channel Countermeasures:
├── Algorithmic Countermeasures
│   ├── Constant-time algorithms
│   ├── Blinding techniques
│   ├── Masking schemes
│   └── Dummy operations
├── Hardware Countermeasures
│   ├── Power line filtering
│   ├── Clock randomization
│   ├── Electromagnetic shielding
│   └── Secure hardware design
├── Software Countermeasures
│   ├── Address space randomization
│   ├── Instruction shuffling
│   ├── Noise injection
│   └── Redundant computations
└── Protocol-level Protection
    ├── Message blinding
    ├── Key refreshing
    ├── Randomized padding
    └── Secure multi-party computation
```

### Criptomalware

#### Tipos de Criptomalware
```
Cryptomalware Classification:
├── Ransomware
│   ├── File encryption ransomware
│   ├── Master boot record encryption
│   ├── Database-targeting ransomware
│   └── Cloud storage encryption
├── Cryptojacking
│   ├── Browser-based mining
│   ├── Fileless cryptomining
│   ├── Mobile cryptojacking
│   └── IoT device exploitation
├── Cryptographic Trojans
│   ├── Certificate theft
│   ├── Key logging
│   ├── SSL/TLS manipulation
│   └── Cryptographic library replacement
└── Advanced Persistent Threats (APT)
    ├── Custom encryption schemes
    ├── Steganographic communication
    ├── Certificate authority compromise
    └── Long-term key exfiltration
```

#### Análisis de Ransomware
**Técnicas de Análisis:**
```bash
# Análisis estático de malware
strings malware_sample.exe | grep -i crypt
objdump -d malware_sample.exe | grep -A5 -B5 "crypto\|aes\|rsa"

# Detección de patrones de cifrado
volatility -f memory.raw imageinfo
volatility -f memory.raw -P Win7SP1x64 malfind

# Análisis de tráfico de red
tcpdump -i eth0 -w ransomware_traffic.pcap
wireshark ransomware_traffic.pcap
```

**Indicadores de Compromiso (IoCs):**
- Modificación masiva de extensiones de archivos
- Comunicación con dominios de comando y control
- Creación de notas de rescate
- Eliminación de copias de seguridad (shadow copies)
- Actividad de red sospechosa en puertos no estándar

---

## Aplicaciones Criptográficas

### Blockchain y Criptomonedas

#### Fundamentos de Blockchain
**Componentes Criptográficos:**
```
Blockchain Cryptographic Components:
├── Hash Functions
│   ├── SHA-256 (Bitcoin)
│   ├── Keccak-256 (Ethereum)
│   ├── BLAKE2 (various altcoins)
│   └── Merkle tree construction
├── Digital Signatures
│   ├── ECDSA (secp256k1)
│   ├── EdDSA (Ed25519)
│   ├── Schnorr signatures
│   └── Multi-signature schemes
├── Consensus Mechanisms
│   ├── Proof of Work (PoW)
│   ├── Proof of Stake (PoS)
│   ├── Delegated Proof of Stake (DPoS)
│   └── Practical Byzantine Fault Tolerance
└── Privacy Technologies
    ├── Ring signatures (Monero)
    ├── Zero-knowledge proofs (Zcash)
    ├── Confidential transactions
    └── CoinJoin mixing
```

#### Implementación de Blockchain
```python
# Ejemplo básico de bloque en Python
import hashlib
import json
from time import time

class Block:
    def __init__(self, index, transactions, timestamp, previous_hash, nonce=0):
        self.index = index
        self.transactions = transactions
        self.timestamp = timestamp
        self.previous_hash = previous_hash
        self.nonce = nonce
    
    def compute_hash(self):
        block_string = json.dumps(self.__dict__, sort_keys=True)
        return hashlib.sha256(block_string.encode()).hexdigest()

class Blockchain:
    difficulty = 4  # Dificultad del proof of work
    
    def __init__(self):
        self.chain = []
        self.create_genesis_block()
    
    def create_genesis_block(self):
        genesis_block = Block(0, [], time(), "0")
        genesis_block.hash = genesis_block.compute_hash()
        self.chain.append(genesis_block)
    
    def proof_of_work(self, block):
        block.nonce = 0
        computed_hash = block.compute_hash()
        
        while not computed_hash.startswith('0' * Blockchain.difficulty):
            block.nonce += 1
            computed_hash = block.compute_hash()
        
        return computed_hash
```

### Protocolos de Comunicación Segura

#### Transport Layer Security (TLS)
**TLS 1.3 Mejoras:**
```
TLS 1.3 Enhancements:
├── Simplified Handshake
│   ├── 1-RTT connection establishment
│   ├── 0-RTT resumption support
│   ├── Simplified cipher suite negotiation
│   └── Forward secrecy by default
├── Cryptographic Improvements
│   ├── Removal of insecure algorithms (RC4, MD5, SHA-1)
│   ├── AEAD-only encryption modes
│   ├── Modern key exchange (ECDHE, DHE, PSK)
│   └── Post-quantum cryptography readiness
├── Security Enhancements
│   ├── Encrypted handshake messages
│   ├── Certificate transparency integration
│   ├── Downgrade attack protection
│   └── Key separation for different purposes
└── Performance Benefits
    ├── Reduced computational overhead
    ├── Faster connection establishment
    ├── Better mobile device performance
    └── Reduced bandwidth usage
```

#### Signal Protocol
**Double Ratchet Algorithm:**
```
Signal Protocol Components:
├── Initial Key Exchange
│   ├── X3DH (Extended Triple Diffie-Hellman)
│   ├── Identity keys (long-term)
│   ├── Signed prekeys (medium-term)
│   └── One-time prekeys (ephemeral)
├── Double Ratchet
│   ├── Diffie-Hellman ratchet (forward secrecy)
│   ├── Symmetric key ratchet (immediate forward secrecy)
│   ├── Message keys derivation
│   └── Out-of-order message handling
├── Encryption
│   ├── AES-256 in CBC mode
│   ├── HMAC-SHA256 authentication
│   ├── Key derivation (HKDF)
│   └── Secure random number generation
└── Additional Features
    ├── Future secrecy (break-in recovery)
    ├── Deniable authentication
    ├── Asynchronous communication
    └── Group messaging support
```

### E-commerce y Transacciones Digitales

#### Payment Card Industry (PCI) Cryptography
**PCI DSS Cryptographic Requirements:**
```
PCI DSS Cryptographic Standards:
├── Encryption Requirements
│   ├── Strong cryptography (AES minimum)
│   ├── Key length minimum 128-bit (256-bit recommended)
│   ├── Encryption of cardholder data at rest
│   └── Encryption of cardholder data in transit
├── Key Management (Requirement 3)
│   ├── Key generation and distribution
│   ├── Secure key storage
│   ├── Key rotation and retirement
│   └── Access control to cryptographic keys
├── Transmission Security (Requirement 4)
│   ├── Strong cryptography for open networks
│   ├── Never send unencrypted PANs by email
│   ├── Secure messaging technologies
│   └── Certificate and trust chain validation
└── Testing Requirements
    ├── Regular vulnerability scanning
    ├── Penetration testing
    ├── File integrity monitoring
    └── Security assessment procedures
```

#### Digital Payment Protocols
**EMV Chip Technology:**
- Application cryptograms for transaction authentication
- Dynamic data authentication (DDA)
- Static data authentication (SDA)
- Combined data authentication (CDA)
- PIN verification and management

### Voto Electrónico

#### Requisitos Criptográficos
```
E-voting Cryptographic Requirements:
├── Privacy Properties
│   ├── Vote secrecy (ballot privacy)
│   ├── Receipt-freeness
│   ├── Coercion resistance
│   └── Anonymous voting
├── Integrity Properties
│   ├── Vote accuracy
│   ├── Completeness (all votes counted)
│   ├── Soundness (only valid votes)
│   └── Robustness against failures
├── Verifiability Properties
│   ├── Individual verifiability
│   ├── Universal verifiability
│   ├── End-to-end verifiability
│   └── Dispute resolution
└── Availability Properties
    ├── System availability during voting
    ├── Scalability for large elections
    ├── Performance under load
    └── Disaster recovery capabilities
```

#### Tecnologías de Voto Electrónico
**Homomorphic Encryption Voting:**
- Permite sumar votos cifrados sin descifrar
- Preserva la privacidad individual
- Permite verificación pública del resultado
- Basado en ElGamal o Paillier cryptosystems

**Blind Signature Voting:**
- Votante obtiene firma ciega de autoridad
- Voto es unlinkable a la identidad del votante
- Previene double voting
- Permite verificación individual

---

## Normativa para la Protección de Datos

### Marco Legal Internacional

#### Evolución de la Privacidad Digital
**Hitos Históricos:**
```
Privacy Legislation Timeline:
├── 1970s - Fair Information Practice Principles (FIPP)
├── 1980 - OECD Privacy Guidelines
├── 1981 - Council of Europe Convention 108
├── 1995 - EU Data Protection Directive 95/46/EC
├── 2001 - US PATRIOT Act
├── 2016 - EU-US Privacy Shield Framework
├── 2018 - EU General Data Protection Regulation (GDPR)
├── 2018 - California Consumer Privacy Act (CCPA)
├── 2020 - Brazil General Data Protection Law (LGPD)
└── 2021 - China Personal Information Protection Law (PIPL)
```

#### Principios Fundamentales de Protección de Datos
**Principios GDPR:**
```
GDPR Core Principles (Article 5):
├── Lawfulness, fairness and transparency
├── Purpose limitation
├── Data minimisation
├── Accuracy
├── Storage limitation
├── Integrity and confidentiality (security)
└── Accountability
```

### Jurisdicciones y Alcance Global

#### Comparación Internacional
```
Global Privacy Regulation Comparison:
┌─────────────┬─────────────┬─────────────┬─────────────┐
│ Jurisdiction│ Regulation  │ Scope       │ Penalties   │
├─────────────┼─────────────┼─────────────┼─────────────┤
│ EU          │ GDPR        │ Global      │ 4% revenue  │
│ California  │ CCPA/CPRA   │ CA consumers│ $7,500/rec  │
│ Brazil      │ LGPD        │ Brazil data │ 2% revenue  │
│ China       │ PIPL        │ China data  │ 5% revenue  │
│ Canada      │ PIPEDA      │ Commercial  │ Variable    │
│ Japan       │ APPI        │ Personal    │ Criminal    │
└─────────────┴─────────────┴─────────────┴─────────────┘
```

---

## RGPD (Reglamento General de Protección de Datos)

### Principios Fundamentales

#### Bases Legales para el Tratamiento (Artículo 6)
```
GDPR Legal Bases:
├── Consent (Art. 6.1.a)
│   ├── Freely given
│   ├── Specific
│   ├── Informed
│   └── Unambiguous
├── Contract (Art. 6.1.b)
│   ├── Performance of contract
│   └── Pre-contractual measures
├── Legal Obligation (Art. 6.1.c)
│   ├── EU law obligations
│   └── Member state law obligations
├── Vital Interests (Art. 6.1.d)
│   ├── Life-threatening situations
│   └── Physical integrity protection
├── Public Task (Art. 6.1.e)
│   ├── Public interest
│   └── Official authority exercise
└── Legitimate Interests (Art. 6.1.f)
    ├── Balancing test required
    ├── Data subject interests priority
    └── Fundamental rights consideration
```

### Derechos de los Interesados

#### Derechos Individuales (Capítulo III)
```
Data Subject Rights:
├── Right of Access (Art. 15)
│   ├── Confirmation of processing
│   ├── Copy of personal data
│   ├── Processing information
│   └── Free of charge (with exceptions)
├── Right to Rectification (Art. 16)
│   ├── Inaccurate data correction
│   ├── Incomplete data completion
│   └── Third party notification
├── Right to Erasure (Art. 17) - "Right to be forgotten"
│   ├── No longer necessary for purposes
│   ├── Consent withdrawal
│   ├── Unlawful processing
│   └── Technical measures for erasure
├── Right to Restrict Processing (Art. 18)
│   ├── Accuracy contested
│   ├── Processing unlawful
│   ├── Controller no longer needs data
│   └── Objection pending
├── Right to Data Portability (Art. 20)
│   ├── Structured, commonly used format
│   ├── Machine-readable format
│   ├── Direct transmission to another controller
│   └── Only for automated processing
├── Right to Object (Art. 21)
│   ├── Processing for public task/legitimate interests
│   ├── Direct marketing (absolute right)
│   ├── Profiling for direct marketing
│   └── Scientific/historical research
└── Rights Related to Automated Decision-Making (Art. 22)
    ├── Not subject to solely automated decisions
    ├── Significant effects on individual
    ├── Human intervention right
    └── Contest decision right
```

### Obligaciones del Responsable del Tratamiento

#### Responsabilidades Principales
```
Controller Obligations:
├── Data Protection by Design and by Default (Art. 25)
│   ├── Technical measures integration
│   ├── Organisational measures integration
│   ├── Pseudonymisation implementation
│   └── Data minimisation by default
├── Joint Controllers (Art. 26)
│   ├── Arrangement determination
│   ├── Respective responsibilities
│   ├── Contact point designation
│   └── Transparent information provision
├── Records of Processing Activities (Art. 30)
│   ├── Controller identification
│   ├── Processing purposes
│   ├── Data subject categories
│   ├── Personal data categories
│   ├── Recipients categories
│   ├── Third country transfers
│   ├── Retention periods
│   └── Security measures description
├── Data Protection Impact Assessment (Art. 35)
│   ├── High risk processing identification
│   ├── Systematic assessment
│   ├── Risks to rights and freedoms
│   └── Mitigation measures
└── Data Breach Notification (Art. 33-34)
    ├── 72-hour notification to authority
    ├── Individual notification if high risk
    ├── Documentation requirements
    └── Communication content requirements
```

### Sanciones y Multas

#### Régimen Sancionador (Artículo 83)
```
GDPR Penalty Framework:
├── Administrative Fines Tier 1 (Up to €10M or 2% global turnover)
│   ├── Controller/processor obligations (Art. 8, 11, 25-39)
│   ├── Certification body obligations (Art. 42, 43)
│   └── Monitoring body obligations (Art. 41, 43)
├── Administrative Fines Tier 2 (Up to €20M or 4% global turnover)
│   ├── Basic principles violation (Art. 5, 6, 7, 9)
│   ├── Data subjects' rights violation (Art. 12-22)
│   ├── Transfer provisions violation (Art. 44-49)
│   └── Non-compliance with authority orders
├── Additional Penalties
│   ├── Processing bans
│   ├── Data flow suspension
│   ├── Certification withdrawal
│   └── Temporary/definitive limitation
└── Factors for Penalty Calculation
    ├── Nature, gravity, and duration
    ├── Intentional or negligent character
    ├── Technical and organisational measures
    ├── Cooperation with supervisory authority
    ├── Previous infringements
    ├── Financial benefits gained
    └── Other aggravating/mitigating factors
```

### Implementación Práctica

#### Programa de Compliance GDPR
```
GDPR Compliance Program:
├── Phase 1: Assessment and Gap Analysis
│   ├── Data mapping and inventory
│   ├── Processing activity documentation
│   ├── Legal basis identification
│   ├── Risk assessment
│   └── Gap analysis against GDPR requirements
├── Phase 2: Policy and Procedure Development
│   ├── Privacy policy updates
│   ├── Data retention policies
│   ├── Consent management procedures
│   ├── Data subject request procedures
│   └── Breach response procedures
├── Phase 3: Technical Implementation
│   ├── Privacy by design implementation
│   ├── Data security measures
│   ├── Consent management systems
│   ├── Data portability tools
│   └── Anonymisation/pseudonymisation techniques
├── Phase 4: Organisational Measures
│   ├── Data Protection Officer appointment
│   ├── Staff training and awareness
│   ├── Vendor management program
│   ├── Data processing agreements
│   └── Accountability documentation
└── Phase 5: Monitoring and Maintenance
    ├── Regular compliance audits
    ├── Privacy impact assessments
    ├── Incident response testing
    ├── Policy updates and reviews
    └── Continuous improvement process
```

---

## Otras Regulaciones Importantes

### HIPAA (Health Insurance Portability and Accountability Act)

#### HIPAA Security Rule
```
HIPAA Security Safeguards:
├── Administrative Safeguards
│   ├── Security Officer designation
│   ├── Workforce training and access management
│   ├── Information access management
│   ├── Security awareness and training
│   ├── Security incident procedures
│   ├── Contingency planning
│   ├── Evaluation procedures
│   └── Business associate contracts
├── Physical Safeguards
│   ├── Facility access controls
│   ├── Workstation use restrictions
│   ├── Device and media controls
│   └── Environmental protections
├── Technical Safeguards
│   ├── Access control (unique user identification)
│   ├── Audit controls and logging
│   ├── Integrity controls
│   ├── Person or entity authentication
│   └── Transmission security
└── Implementation Specifications
    ├── Required implementations
    ├── Addressable implementations
    ├── Risk assessment based decisions
    └── Documentation requirements
```

### PCI DSS (Payment Card Industry Data Security Standard)

#### PCI DSS Requirements
```
PCI DSS 12 Requirements:
├── Build and Maintain Secure Networks
│   ├── Req 1: Install/maintain firewall configuration
│   └── Req 2: Don't use vendor-supplied defaults
├── Protect Cardholder Data
│   ├── Req 3: Protect stored cardholder data
│   └── Req 4: Encrypt transmission over open networks
├── Maintain Vulnerability Management Program
│   ├── Req 5: Protect against malware
│   └── Req 6: Develop/maintain secure systems
├── Implement Strong Access Control
│   ├── Req 7: Restrict access by business need-to-know
│   ├── Req 8: Identify/authenticate access to systems
│   └── Req 9: Restrict physical access to cardholder data
├── Regularly Monitor and Test Networks
│   ├── Req 10: Track/monitor all access to network
│   └── Req 11: Regularly test security systems
└── Maintain Information Security Policy
    └── Req 12: Maintain policy addressing security
```

### SOX (Sarbanes-Oxley Act)

#### SOX IT Controls
```
SOX IT Control Framework:
├── Section 302: Corporate Responsibility
│   ├── CEO/CFO certification of financial reports
│   ├── Internal control assessment
│   ├── Material weakness disclosure
│   └── Control deficiency reporting
├── Section 404: Management Assessment
│   ├── Internal control framework establishment
│   ├── Control effectiveness assessment
│   ├── External auditor attestation
│   └── Material weakness identification
├── IT General Controls (ITGC)
│   ├── Access controls and security
│   ├── Program change controls
│   ├── Program development controls
│   ├── Computer operations controls
│   └── System software controls
└── Application Controls
    ├── Input controls
    ├── Processing controls
    ├── Output controls
    └── Interface controls
```

### ISO 27001

#### Information Security Management System (ISMS)
```
ISO 27001 Structure:
├── Context of the Organization (Clause 4)
│   ├── Understanding organization and context
│   ├── Understanding needs of interested parties
│   ├── Determining ISMS scope
│   └── Information security management system
├── Leadership (Clause 5)
│   ├── Leadership and commitment
│   ├── Information security policy
│   └── Organizational roles and responsibilities
├── Planning (Clause 6)
│   ├── Actions to address risks and opportunities
│   ├── Information security objectives
│   └── Planning to achieve objectives
├── Support (Clause 7)
│   ├── Resources
│   ├── Competence
│   ├── Awareness
│   ├── Communication
│   └── Documented information
├── Operation (Clause 8)
│   ├── Operational planning and control
│   └── Information security risk assessment
├── Performance Evaluation (Clause 9)
│   ├── Monitoring, measurement, analysis
│   ├── Internal audit
│   └── Management review
└── Improvement (Clause 10)
    ├── Nonconformity and corrective action
    └── Continual improvement
```

---

## Implementación de Compliance

### Evaluación de Riesgos de Privacidad

#### Metodología de Privacy Risk Assessment
```
Privacy Risk Assessment Process:
├── Step 1: Data Flow Mapping
│   ├── Data collection identification
│   ├── Processing activities mapping
│   ├── Data sharing and transfers
│   └── Retention and deletion practices
├── Step 2: Risk Identification
│   ├── Privacy risks to individuals
│   ├── Compliance risks to organization
│   ├── Reputation and business risks
│   └── Technical and security risks
├── Step 3: Risk Analysis
│   ├── Likelihood assessment
│   ├── Impact evaluation
│   ├── Risk rating calculation
│   └── Risk tolerance comparison
├── Step 4: Risk Treatment
│   ├── Risk mitigation measures
│   ├── Risk acceptance decisions
│   ├── Risk transfer options
│   └── Risk avoidance strategies
└── Step 5: Monitoring and Review
    ├── Risk monitoring procedures
    ├── Regular reassessment schedule
    ├── Incident tracking and analysis
    └── Continuous improvement process
```

### Privacy by Design

#### Privacy by Design Principles
```
Privacy by Design Implementation:
├── Proactive not Reactive
│   ├── Anticipate privacy issues
│   ├── Prevent privacy breaches
│   ├── Design-stage integration
│   └── Early risk mitigation
├── Privacy as the Default
│   ├── Maximum privacy protection default
│   ├── No action required from individual
│   ├── Automatic privacy protection
│   └── Opt-in rather than opt-out
├── Full Functionality
│   ├── All legitimate interests accommodated
│   ├── Zero-sum approach avoided
│   ├── Win-win solutions sought
│   └── Positive-sum approach
├── End-to-End Security
│   ├── Secure data lifecycle management
│   ├── Encryption and access controls
│   ├── Secure destruction procedures
│   └── Continuous monitoring
├── Visibility and Transparency
│   ├── Clear privacy notices
│   ├── Open communication
│   ├── Accountability demonstration
│   └── Regular reporting
├── Respect for User Privacy
│   ├── User-centric design
│   ├── Strong privacy defaults
│   ├── User control mechanisms
│   └── Individual empowerment
└── Implementation Strategies
    ├── Technical privacy controls
    ├── Organizational privacy measures
    ├── Process privacy integration
    └── Cultural privacy awareness
```

### Data Protection Impact Assessment (DPIA)

#### DPIA Process
```
DPIA Methodology:
├── DPIA Threshold Assessment
│   ├── High risk processing identification
│   ├── GDPR Article 35(3) criteria check
│   ├── Supervisory authority guidance review
│   └── Professional judgment application
├── DPIA Execution
│   ├── Processing description
│   ├── Necessity and proportionality assessment
│   ├── Risk identification and analysis
│   ├── Mitigation measures identification
│   ├── Stakeholder consultation
│   └── DPO consultation (if applicable)
├── DPIA Documentation
│   ├── Executive summary
│   ├── Detailed assessment results
│   ├── Risk register and treatment plan
│   ├── Implementation roadmap
│   └── Monitoring and review schedule
├── DPIA Review and Approval
│   ├── Internal stakeholder review
│   ├── Legal and compliance review
│   ├── Management approval
│   └── Implementation authorization
└── DPIA Monitoring and Updates
    ├── Regular reassessment schedule
    ├── Change management integration
    ├── Incident tracking and analysis
    └── Lesson learned documentation
```

---

## Auditoría y Certificación

### Procesos de Auditoría

#### Auditoría de Seguridad de la Información
```
Information Security Audit Process:
├── Pre-audit Planning
│   ├── Audit scope definition
│   ├── Risk-based audit approach
│   ├── Resource allocation
│   ├── Stakeholder communication
│   └── Audit timeline establishment
├── Audit Execution
│   ├── Documentation review
│   ├── Control testing procedures
│   ├── Interview conduction
│   ├── Technical assessment
│   ├── Gap analysis performance
│   └── Evidence collection
├── Audit Reporting
│   ├── Finding classification
│   ├── Risk rating assignment
│   ├── Recommendation development
│   ├── Management letter preparation
│   └── Executive summary creation
├── Follow-up Activities
│   ├── Management response review
│   ├── Remediation plan assessment
│   ├── Implementation verification
│   └── Residual risk evaluation
└── Continuous Monitoring
    ├── Control effectiveness monitoring
    ├── Risk landscape changes
    ├── Regulatory updates tracking
    └── Best practice evolution
```

### Certificaciones de Seguridad

#### Principales Certificaciones
```
Security Certification Landscape:
├── ISO/IEC 27001 Certification
│   ├── ISMS implementation
│   ├── Third-party assessment
│   ├── Annual surveillance audits
│   └── 3-year recertification cycle
├── SOC (Service Organization Control) Reports
│   ├── SOC 1 (financial reporting controls)
│   ├── SOC 2 (security, availability, confidentiality)
│   ├── SOC 3 (general use reports)
│   └── Annual or periodic assessments
├── Industry-Specific Certifications
│   ├── PCI DSS compliance validation
│   ├── HIPAA compliance assessment
│   ├── FedRAMP authorization (US government)
│   └── IRAP assessment (Australian government)
├── Cloud Security Certifications
│   ├── CSA STAR certification
│   ├── Cloud security alliance standards
│   ├── Multi-cloud compliance programs
│   └── Continuous monitoring requirements
└── Privacy Certifications
    ├── Privacy shield certification (historical)
    ├── GDPR certification schemes
    ├── Privacy by design certifications
    └── Cross-border transfer mechanisms
```

### Mejora Continua

#### Continuous Improvement Framework
```
Security Improvement Lifecycle:
├── Performance Monitoring
│   ├── Key Performance Indicators (KPIs)
│   ├── Security metrics collection
│   ├── Compliance dashboard maintenance
│   └── Stakeholder reporting
├── Gap Assessment
│   ├── Current state evaluation
│   ├── Desired state definition
│   ├── Gap identification and prioritization
│   └── Resource requirement analysis
├── Improvement Planning
│   ├── Initiative prioritization
│   ├── Resource allocation
│   ├── Timeline development
│   └── Success criteria definition
├── Implementation and Execution
│   ├── Project management methodology
│   ├── Change management process
│   ├── Training and awareness programs
│   └── Communication and engagement
└── Review and Optimization
    ├── Post-implementation review
    ├── Lesson learned documentation
    ├── Process optimization
    └── Next cycle planning
```

## Objetivos de Aprendizaje
- [ ] Dominar algoritmos criptográficos modernos (AES, RSA, ECC)
- [ ] Comprender criptografía post-cuántica y sus implicaciones
- [ ] Implementar soluciones criptográficas seguras usando bibliotecas estándar
- [ ] Realizar análisis de vulnerabilidades criptográficas y side-channel attacks
- [ ] Evaluar aplicaciones criptográficas en blockchain y comunicaciones seguras
- [ ] Comprender el marco regulatorio internacional de protección de datos
- [ ] Implementar compliance GDPR completo en organizaciones
- [ ] Desarrollar programas de evaluación de riesgos de privacidad
- [ ] Realizar auditorías de protección de datos y certificaciones de seguridad
- [ ] Establecer programas de mejora continua en privacidad y seguridad

## Recursos Adicionales

### Textos Legales y Normativas
- [Reglamento General de Protección de Datos (GDPR)](https://gdpr-info.eu/) - Texto completo oficial
- [NIST Cryptographic Standards](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines) - Estándares criptográficos
- [ISO/IEC 27001:2013](https://www.iso.org/standard/54534.html) - Sistema de gestión de seguridad
- [PCI Security Standards Council](https://www.pcisecuritystandards.org/) - Estándares PCI DSS

### Herramientas de Compliance y Criptografía
- [OpenSSL](https://www.openssl.org/) - Biblioteca criptográfica completa
- [Libsodium](https://libsodium.gitbook.io/doc/) - Biblioteca criptográfica moderna
- [OneTrust](https://www.onetrust.com/) - Plataforma de gestión de privacidad
- [TrustArc](https://trustarc.com/) - Soluciones de compliance de privacidad

### Organizaciones y Recursos Profesionales
- [International Association of Privacy Professionals (IAPP)](https://iapp.org/) - Asociación profesional de privacidad
- [Cloud Security Alliance (CSA)](https://cloudsecurityalliance.org/) - Seguridad en la nube
- [European Data Protection Board (EDPB)](https://edpb.europa.eu/) - Autoridades europeas de protección de datos
- [Cryptography Research](https://www.cryptography.com/) - Investigación en criptografía aplicada

### Cursos y Certificaciones
- **CIPP/E** (Certified Information Privacy Professional/Europe) - IAPP
- **CIPM** (Certified Information Privacy Manager) - IAPP
- **CISSP** (Certified Information Systems Security Professional) - (ISC)²
- **CISA** (Certified Information Systems Auditor) - ISACA

## Actividades Prácticas

### Laboratorio 1: Implementación Criptográfica
**Objetivo:** Implementar y comparar algoritmos criptográficos modernos
**Actividades:**
- Implementar cifrado AES en diferentes modos de operación
- Generar y gestionar claves RSA y ECC
- Comparar rendimiento de algoritmos simétricos y asimétricos
- Implementar funciones hash y verificar integridad
- Desarrollar aplicación de firma digital completa

### Laboratorio 2: Análisis de Side-Channel Attacks
**Objetivo:** Comprender y detectar vulnerabilidades de canal lateral
**Actividades:**
- Analizar timing attacks en implementaciones criptográficas
- Simular power analysis attacks básicos
- Implementar contramedidas de protección
- Evaluar efectividad de medidas de mitigación
- Documentar hallazgos y recomendaciones

### Laboratorio 3: Desarrollo de Blockchain
**Objetivo:** Implementar blockchain básico con elementos criptográficos
**Actividades:**
- Crear estructura de bloques con hash functions
- Implementar proof-of-work consensus mechanism
- Desarrollar sistema de transacciones con firmas digitales
- Crear wallet básico para gestión de claves
- Probar resistencia a ataques comunes

### Laboratorio 4: Evaluación GDPR Compliance
**Objetivo:** Realizar assessment completo de compliance GDPR
**Actividades:**
- Mapear flujos de datos personales en organización simulada
- Identificar bases legales para procesamiento
- Evaluar derechos de los interesados implementados
- Realizar Data Protection Impact Assessment (DPIA)
- Desarrollar plan de remediación de gaps identificados

### Laboratorio 5: Auditoría de Privacidad y Seguridad
**Objetivo:** Ejecutar auditoría completa de programa de privacidad
**Actividades:**
- Revisar políticas y procedimientos de privacidad
- Evaluar controles técnicos y organizacionales
- Probar procedimientos de respuesta a incidentes
- Verificar programa de capacitación y concientización
- Generar reporte de auditoría con recomendaciones

### Proyecto Integrador: Programa de Compliance Integral
**Objetivo:** Diseñar e implementar programa completo de compliance
**Componentes:**
1. **Assessment Inicial**: Evaluación de estado actual
2. **Framework Selection**: Selección de marcos regulatorios aplicables
3. **Gap Analysis**: Identificación de brechas de compliance
4. **Implementation Plan**: Plan detallado de implementación
5. **Technical Controls**: Implementación de controles técnicos
6. **Organizational Controls**: Desarrollo de controles organizacionales
7. **Training Program**: Programa de capacitación y concientización
8. **Monitoring System**: Sistema de monitoreo continuo
9. **Incident Response**: Procedimientos de respuesta a incidentes
10. **Audit and Review**: Programa de auditoría y revisión continua

**Entregables:**
- Documento de estrategia de compliance
- Políticas y procedimientos desarrollados
- Implementaciones técnicas funcionales
- Programa de capacitación completo
- Sistema de monitoreo y reportes
- Plan de auditoría y mejora continua
