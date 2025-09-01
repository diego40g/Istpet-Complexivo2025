# Tema 9: Cifrado de Información

## Índice de Contenidos
1. [Fundamentos de Criptografía](#fundamentos-de-criptografía)
2. [Cifrado Simétrico](#cifrado-simétrico)
3. [Cifrado Asimétrico](#cifrado-asimétrico)
4. [Funciones Hash](#funciones-hash)
5. [Firma Digital](#firma-digital)
6. [Infraestructura de Clave Pública (PKI)](#infraestructura-de-clave-pública-pki)
7. [Implementación Práctica](#implementación-práctica)
8. [Casos de Uso y Aplicaciones](#casos-de-uso-y-aplicaciones)

---

## Fundamentos de Criptografía

### Historia y Evolución de la Criptografía

#### Línea Temporal Criptográfica
```
Evolution of Cryptography:
┌─────────────────────────────────────────────────────────────┐
│ Ancient Era (500 BC - 400 AD)                              │
│ ├── Caesar Cipher (substitution)                           │
│ ├── Scytale (transposition)                               │
│ └── Polybius Square                                        │
├─────────────────────────────────────────────────────────────┤
│ Medieval Period (400 - 1400)                               │
│ ├── Vigenère Cipher (polyalphabetic)                      │
│ ├── Book Ciphers                                           │
│ └── Frequency Analysis Development                          │
├─────────────────────────────────────────────────────────────┤
│ Renaissance & Early Modern (1400 - 1900)                   │
│ ├── Great Cipher (Louis XIV)                               │
│ ├── Jefferson Disk                                         │
│ └── Telegraph Ciphers                                      │
├─────────────────────────────────────────────────────────────┤
│ Modern Era (1900 - 1970)                                   │
│ ├── Enigma Machine (WWII)                                  │
│ ├── DES Development                                         │
│ └── Computer-based Cryptography                            │
├─────────────────────────────────────────────────────────────┤
│ Contemporary Era (1970 - Present)                          │
│ ├── Public Key Cryptography (1976)                         │
│ ├── AES Standard (2001)                                     │
│ ├── Quantum Cryptography                                   │
│ └── Post-Quantum Cryptography                              │
└─────────────────────────────────────────────────────────────┘
```

#### Principios Fundamentales
```python
# Implementación de César Cipher como introducción histórica
class CaesarCipher:
    def __init__(self, shift=3):
        self.shift = shift
        self.alphabet = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    
    def encrypt(self, plaintext):
        """Cifrar texto usando César Cipher"""
        ciphertext = ""
        for char in plaintext.upper():
            if char in self.alphabet:
                old_pos = self.alphabet.index(char)
                new_pos = (old_pos + self.shift) % 26
                ciphertext += self.alphabet[new_pos]
            else:
                ciphertext += char
        return ciphertext
    
    def decrypt(self, ciphertext):
        """Descifrar texto usando César Cipher"""
        plaintext = ""
        for char in ciphertext.upper():
            if char in self.alphabet:
                old_pos = self.alphabet.index(char)
                new_pos = (old_pos - self.shift) % 26
                plaintext += self.alphabet[new_pos]
            else:
                plaintext += char
        return plaintext
    
    def frequency_analysis(self, text):
        """Análisis de frecuencias para criptoanálisis"""
        frequency = {}
        total_letters = 0
        
        for char in text.upper():
            if char in self.alphabet:
                total_letters += 1
                frequency[char] = frequency.get(char, 0) + 1
        
        # Convertir a porcentajes
        for char in frequency:
            frequency[char] = (frequency[char] / total_letters) * 100
        
        return frequency

# Ejemplo de uso histórico
caesar = CaesarCipher(13)  # ROT13
plaintext = "HELLO WORLD"
ciphertext = caesar.encrypt(plaintext)
decrypted = caesar.decrypt(ciphertext)

print(f"Original: {plaintext}")
print(f"Encrypted: {ciphertext}")
print(f"Decrypted: {decrypted}")

# Análisis de frecuencias
freq_analysis = caesar.frequency_analysis("THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG")
print("Frequency Analysis:", freq_analysis)
```

### Conceptos Básicos de Criptografía Moderna

#### Taxonomía Criptográfica
```
Cryptographic Classification:
├── By Key Usage
│   ├── Symmetric (Same key for encryption/decryption)
│   │   ├── Stream Ciphers (RC4, ChaCha20)
│   │   └── Block Ciphers (AES, DES, 3DES)
│   └── Asymmetric (Different keys)
│       ├── Public Key Encryption (RSA, ECC)
│       └── Digital Signatures (DSA, ECDSA)
├── By Operation Type
│   ├── Substitution (Character replacement)
│   ├── Transposition (Position rearrangement)
│   ├── Product Ciphers (Combination of both)
│   └── Stream Operations (Bit-by-bit)
├── By Security Level
│   ├── Classical (Breakable with modern computers)
│   ├── Computationally Secure (Infeasible to break)
│   ├── Unconditionally Secure (Theoretically unbreakable)
│   └── Quantum Resistant (Post-quantum cryptography)
└── By Application
    ├── Data Encryption
    ├── Authentication
    ├── Non-repudiation
    └── Key Exchange
```

#### Principios de Seguridad Criptográfica (Kerchoff's Principle)
```python
class CryptographicPrinciples:
    """
    Implementación de principios criptográficos fundamentales
    """
    
    @staticmethod
    def kerchoff_principle():
        """
        Principio de Kerchoff: La seguridad debe residir en la clave,
        no en el secreto del algoritmo
        """
        return {
            "principle": "Security through key secrecy, not algorithm secrecy",
            "implications": [
                "Algorithm should be public and well-studied",
                "Security relies entirely on key secrecy",
                "Open algorithms can be peer-reviewed",
                "No security through obscurity"
            ],
            "examples": [
                "AES algorithm is public, keys are secret",
                "RSA algorithm is public, private keys are secret"
            ]
        }
    
    @staticmethod
    def perfect_secrecy():
        """
        Concepto de secreto perfecto (Shannon)
        """
        return {
            "definition": "Ciphertext provides no information about plaintext",
            "requirements": [
                "Key length >= Message length",
                "Key must be truly random",
                "Key must never be reused",
                "Key must be kept secret"
            ],
            "examples": ["One-Time Pad (OTP)"],
            "practical_limitations": [
                "Key distribution problem",
                "Key storage requirements",
                "Key generation challenges"
            ]
        }
    
    @staticmethod
    def computational_security():
        """
        Seguridad computacional práctica
        """
        return {
            "definition": "Infeasible to break with available computational resources",
            "factors": [
                "Time complexity",
                "Space complexity", 
                "Financial cost",
                "Technology limitations"
            ],
            "examples": [
                "AES-256: 2^256 possible keys",
                "RSA-2048: Factoring large numbers",
                "SHA-256: Finding collisions"
            ]
        }

# Implementación de One-Time Pad (secreto perfecto)
import secrets
import string

class OneTimePad:
    def __init__(self):
        self.alphabet = string.ascii_uppercase
    
    def generate_key(self, length):
        """Generar clave aleatoria del tamaño del mensaje"""
        return ''.join(secrets.choice(self.alphabet) for _ in range(length))
    
    def encrypt(self, plaintext, key):
        """Cifrar usando One-Time Pad"""
        if len(key) < len(plaintext):
            raise ValueError("Key must be at least as long as plaintext")
        
        ciphertext = ""
        for i, char in enumerate(plaintext.upper()):
            if char in self.alphabet:
                p_index = self.alphabet.index(char)
                k_index = self.alphabet.index(key[i])
                c_index = (p_index + k_index) % 26
                ciphertext += self.alphabet[c_index]
            else:
                ciphertext += char
        
        return ciphertext
    
    def decrypt(self, ciphertext, key):
        """Descifrar usando One-Time Pad"""
        plaintext = ""
        for i, char in enumerate(ciphertext.upper()):
            if char in self.alphabet:
                c_index = self.alphabet.index(char)
                k_index = self.alphabet.index(key[i])
                p_index = (c_index - k_index) % 26
                plaintext += self.alphabet[p_index]
            else:
                plaintext += char
        
        return plaintext

# Ejemplo de uso OTP
otp = OneTimePad()
message = "SECRETMESSAGE"
key = otp.generate_key(len(message))

encrypted = otp.encrypt(message, key)
decrypted = otp.decrypt(encrypted, key)

print(f"Message: {message}")
print(f"Key: {key}")
print(f"Encrypted: {encrypted}")
print(f"Decrypted: {decrypted}")
```

---

## Cifrado Simétrico

### Algoritmos de Cifrado por Bloques

#### Advanced Encryption Standard (AES)
```python
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
from cryptography.hazmat.primitives import padding, hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC
import os
import base64

class AESCipher:
    def __init__(self, key_size=256):
        self.key_size = key_size
        self.block_size = 128  # AES block size is always 128 bits
    
    def generate_key(self, password=None, salt=None):
        """Generar clave AES desde password o aleatoriamente"""
        if password:
            # Derivar clave desde password usando PBKDF2
            if salt is None:
                salt = os.urandom(16)
            
            kdf = PBKDF2HMAC(
                algorithm=hashes.SHA256(),
                length=self.key_size // 8,  # Convert bits to bytes
                salt=salt,
                iterations=100000,
            )
            key = kdf.derive(password.encode())
            return key, salt
        else:
            # Generar clave aleatoria
            return os.urandom(self.key_size // 8), None
    
    def encrypt_cbc(self, plaintext, key, iv=None):
        """Cifrar usando AES-CBC"""
        if iv is None:
            iv = os.urandom(16)  # 128-bit IV
        
        # Padding PKCS7
        padder = padding.PKCS7(128).padder()
        padded_data = padder.update(plaintext.encode())
        padded_data += padder.finalize()
        
        # Cifrado
        cipher = Cipher(algorithms.AES(key), modes.CBC(iv))
        encryptor = cipher.encryptor()
        ciphertext = encryptor.update(padded_data) + encryptor.finalize()
        
        return ciphertext, iv
    
    def decrypt_cbc(self, ciphertext, key, iv):
        """Descifrar usando AES-CBC"""
        cipher = Cipher(algorithms.AES(key), modes.CBC(iv))
        decryptor = cipher.decryptor()
        padded_plaintext = decryptor.update(ciphertext) + decryptor.finalize()
        
        # Remove padding
        unpadder = padding.PKCS7(128).unpadder()
        plaintext = unpadder.update(padded_plaintext) + unpadder.finalize()
        
        return plaintext.decode()
    
    def encrypt_gcm(self, plaintext, key, iv=None, associated_data=None):
        """Cifrar usando AES-GCM (Authenticated Encryption)"""
        if iv is None:
            iv = os.urandom(12)  # 96-bit IV for GCM
        
        cipher = Cipher(algorithms.AES(key), modes.GCM(iv))
        encryptor = cipher.encryptor()
        
        # Añadir datos asociados si existen
        if associated_data:
            encryptor.authenticate_additional_data(associated_data)
        
        ciphertext = encryptor.update(plaintext.encode()) + encryptor.finalize()
        
        return ciphertext, iv, encryptor.tag
    
    def decrypt_gcm(self, ciphertext, key, iv, tag, associated_data=None):
        """Descifrar usando AES-GCM"""
        cipher = Cipher(algorithms.AES(key), modes.GCM(iv, tag))
        decryptor = cipher.decryptor()
        
        # Añadir datos asociados si existen
        if associated_data:
            decryptor.authenticate_additional_data(associated_data)
        
        plaintext = decryptor.update(ciphertext) + decryptor.finalize()
        
        return plaintext.decode()
    
    def encrypt_file(self, file_path, output_path, key, mode='GCM'):
        """Cifrar archivo"""
        with open(file_path, 'rb') as infile:
            data = infile.read()
        
        if mode == 'GCM':
            ciphertext, iv, tag = self.encrypt_gcm(data.decode('utf-8', errors='ignore'), key)
            
            # Guardar IV + Tag + Ciphertext
            with open(output_path, 'wb') as outfile:
                outfile.write(iv)
                outfile.write(tag)
                outfile.write(ciphertext)
        
        elif mode == 'CBC':
            ciphertext, iv = self.encrypt_cbc(data.decode('utf-8', errors='ignore'), key)
            
            # Guardar IV + Ciphertext
            with open(output_path, 'wb') as outfile:
                outfile.write(iv)
                outfile.write(ciphertext)
    
    def decrypt_file(self, file_path, output_path, key, mode='GCM'):
        """Descifrar archivo"""
        with open(file_path, 'rb') as infile:
            if mode == 'GCM':
                iv = infile.read(12)  # 96-bit IV
                tag = infile.read(16)  # 128-bit tag
                ciphertext = infile.read()
                
                plaintext = self.decrypt_gcm(ciphertext, key, iv, tag)
            
            elif mode == 'CBC':
                iv = infile.read(16)  # 128-bit IV
                ciphertext = infile.read()
                
                plaintext = self.decrypt_cbc(ciphertext, key, iv)
        
        with open(output_path, 'w') as outfile:
            outfile.write(plaintext)

# Ejemplo de uso AES
aes = AESCipher(256)

# Generar clave desde password
key, salt = aes.generate_key("mi_password_secreto")
print(f"Derived key: {base64.b64encode(key).decode()}")
print(f"Salt: {base64.b64encode(salt).decode()}")

# Cifrado CBC
message = "Este es un mensaje secreto que necesita ser protegido"
ciphertext_cbc, iv_cbc = aes.encrypt_cbc(message, key)
decrypted_cbc = aes.decrypt_cbc(ciphertext_cbc, key, iv_cbc)

print(f"Original: {message}")
print(f"CBC Encrypted: {base64.b64encode(ciphertext_cbc).decode()}")
print(f"CBC Decrypted: {decrypted_cbc}")

# Cifrado GCM (con autenticación)
ciphertext_gcm, iv_gcm, tag_gcm = aes.encrypt_gcm(message, key)
decrypted_gcm = aes.decrypt_gcm(ciphertext_gcm, key, iv_gcm, tag_gcm)

print(f"GCM Encrypted: {base64.b64encode(ciphertext_gcm).decode()}")
print(f"GCM Tag: {base64.b64encode(tag_gcm).decode()}")
print(f"GCM Decrypted: {decrypted_gcm}")
```

#### Modos de Operación de Cifrado por Bloques
```python
class BlockCipherModes:
    """
    Implementación educativa de diferentes modos de operación
    """
    
    def __init__(self, block_cipher_func, block_size=16):
        self.cipher = block_cipher_func
        self.block_size = block_size
    
    def ecb_encrypt(self, plaintext, key):
        """Electronic Codebook (ECB) - NO RECOMENDADO"""
        # Advertencia: ECB no es seguro para datos reales
        blocks = self._pad_and_split(plaintext)
        ciphertext_blocks = []
        
        for block in blocks:
            encrypted_block = self.cipher(block, key, encrypt=True)
            ciphertext_blocks.append(encrypted_block)
        
        return b''.join(ciphertext_blocks)
    
    def cbc_encrypt(self, plaintext, key, iv):
        """Cipher Block Chaining (CBC)"""
        blocks = self._pad_and_split(plaintext)
        ciphertext_blocks = []
        previous_block = iv
        
        for block in blocks:
            # XOR con bloque anterior (o IV)
            xored_block = self._xor_blocks(block, previous_block)
            encrypted_block = self.cipher(xored_block, key, encrypt=True)
            ciphertext_blocks.append(encrypted_block)
            previous_block = encrypted_block
        
        return b''.join(ciphertext_blocks)
    
    def cfb_encrypt(self, plaintext, key, iv):
        """Cipher Feedback (CFB)"""
        blocks = self._split_no_padding(plaintext)
        ciphertext_blocks = []
        previous_block = iv
        
        for block in blocks:
            # Cifrar el bloque anterior
            encrypted_previous = self.cipher(previous_block, key, encrypt=True)
            # XOR con el plaintext
            ciphertext_block = self._xor_blocks(block, encrypted_previous[:len(block)])
            ciphertext_blocks.append(ciphertext_block)
            previous_block = ciphertext_block.ljust(self.block_size, b'\x00')
        
        return b''.join(ciphertext_blocks)
    
    def ofb_encrypt(self, plaintext, key, iv):
        """Output Feedback (OFB)"""
        blocks = self._split_no_padding(plaintext)
        ciphertext_blocks = []
        feedback = iv
        
        for block in blocks:
            # Generar keystream
            keystream = self.cipher(feedback, key, encrypt=True)
            # XOR con plaintext
            ciphertext_block = self._xor_blocks(block, keystream[:len(block)])
            ciphertext_blocks.append(ciphertext_block)
            feedback = keystream
        
        return b''.join(ciphertext_blocks)
    
    def ctr_encrypt(self, plaintext, key, nonce):
        """Counter (CTR)"""
        blocks = self._split_no_padding(plaintext)
        ciphertext_blocks = []
        counter = 0
        
        for block in blocks:
            # Crear contador
            counter_block = nonce + counter.to_bytes(8, 'big')
            # Generar keystream
            keystream = self.cipher(counter_block, key, encrypt=True)
            # XOR con plaintext
            ciphertext_block = self._xor_blocks(block, keystream[:len(block)])
            ciphertext_blocks.append(ciphertext_block)
            counter += 1
        
        return b''.join(ciphertext_blocks)
    
    def _pad_and_split(self, data):
        """Aplicar padding PKCS7 y dividir en bloques"""
        # PKCS7 padding
        if isinstance(data, str):
            data = data.encode()
        
        padding_length = self.block_size - (len(data) % self.block_size)
        padded_data = data + bytes([padding_length] * padding_length)
        
        # Dividir en bloques
        blocks = []
        for i in range(0, len(padded_data), self.block_size):
            blocks.append(padded_data[i:i + self.block_size])
        
        return blocks
    
    def _split_no_padding(self, data):
        """Dividir en bloques sin padding"""
        if isinstance(data, str):
            data = data.encode()
        
        blocks = []
        for i in range(0, len(data), self.block_size):
            blocks.append(data[i:i + self.block_size])
        
        return blocks
    
    def _xor_blocks(self, block1, block2):
        """XOR entre dos bloques"""
        return bytes(a ^ b for a, b in zip(block1, block2))

# Función simulada de cifrado por bloques (para demostración)
def dummy_block_cipher(block, key, encrypt=True):
    """Cifrado simulado para demostración de modos"""
    # En implementación real, aquí iría AES, DES, etc.
    result = bytearray(block)
    for i in range(len(result)):
        result[i] ^= key[i % len(key)]
    return bytes(result)

# Ejemplo de uso de modos
modes = BlockCipherModes(dummy_block_cipher, 16)
key = b"mi_clave_secreta"
iv = os.urandom(16)
nonce = os.urandom(8)
plaintext = "Este mensaje sera cifrado con diferentes modos"

print("=== Comparación de Modos de Cifrado ===")

# ECB (inseguro)
ecb_result = modes.ecb_encrypt(plaintext, key)
print(f"ECB: {base64.b64encode(ecb_result).decode()}")

# CBC
cbc_result = modes.cbc_encrypt(plaintext, key, iv)
print(f"CBC: {base64.b64encode(cbc_result).decode()}")

# CFB
cfb_result = modes.cfb_encrypt(plaintext, key, iv)
print(f"CFB: {base64.b64encode(cfb_result).decode()}")

# OFB
ofb_result = modes.ofb_encrypt(plaintext, key, iv)
print(f"OFB: {base64.b64encode(ofb_result).decode()}")

# CTR
ctr_result = modes.ctr_encrypt(plaintext, key, nonce)
print(f"CTR: {base64.b64encode(ctr_result).decode()}")
```

### Cifrado de Flujo

#### ChaCha20 Stream Cipher
```python
from cryptography.hazmat.primitives.ciphers import Cipher, algorithms, modes
import os

class ChaCha20Cipher:
    def __init__(self):
        self.key_size = 32  # 256 bits
        self.nonce_size = 12  # 96 bits
    
    def generate_key(self):
        """Generar clave aleatoria para ChaCha20"""
        return os.urandom(self.key_size)
    
    def encrypt(self, plaintext, key, nonce=None):
        """Cifrar con ChaCha20"""
        if nonce is None:
            nonce = os.urandom(self.nonce_size)
        
        cipher = Cipher(algorithms.ChaCha20(key, nonce), mode=None)
        encryptor = cipher.encryptor()
        
        if isinstance(plaintext, str):
            plaintext = plaintext.encode()
        
        ciphertext = encryptor.update(plaintext) + encryptor.finalize()
        return ciphertext, nonce
    
    def decrypt(self, ciphertext, key, nonce):
        """Descifrar con ChaCha20"""
        cipher = Cipher(algorithms.ChaCha20(key, nonce), mode=None)
        decryptor = cipher.decryptor()
        
        plaintext = decryptor.update(ciphertext) + decryptor.finalize()
        return plaintext.decode()

# Implementación educativa de RC4 (para comprensión histórica)
class RC4Cipher:
    """
    Implementación educativa de RC4 - NO USAR EN PRODUCCIÓN
    RC4 es inseguro y se incluye solo con fines educativos
    """
    
    def __init__(self):
        pass
    
    def ksa(self, key):
        """Key Scheduling Algorithm"""
        S = list(range(256))
        j = 0
        
        for i in range(256):
            j = (j + S[i] + key[i % len(key)]) % 256
            S[i], S[j] = S[j], S[i]
        
        return S
    
    def prga(self, S, length):
        """Pseudo-Random Generation Algorithm"""
        i = j = 0
        keystream = []
        
        for _ in range(length):
            i = (i + 1) % 256
            j = (j + S[i]) % 256
            S[i], S[j] = S[j], S[i]
            K = S[(S[i] + S[j]) % 256]
            keystream.append(K)
        
        return keystream
    
    def encrypt_decrypt(self, data, key):
        """Cifrar/Descifrar con RC4 (operación simétrica)"""
        if isinstance(key, str):
            key = [ord(c) for c in key]
        
        if isinstance(data, str):
            data = [ord(c) for c in data]
        
        S = self.ksa(key)
        keystream = self.prga(S, len(data))
        
        result = []
        for i in range(len(data)):
            result.append(data[i] ^ keystream[i])
        
        return result

# Ejemplo de uso de cifrado de flujo
print("=== Cifrado de Flujo ===")

# ChaCha20 (moderno y seguro)
chacha = ChaCha20Cipher()
key = chacha.generate_key()
message = "Mensaje para cifrado de flujo con ChaCha20"

encrypted, nonce = chacha.encrypt(message, key)
decrypted = chacha.decrypt(encrypted, key, nonce)

print(f"ChaCha20 Original: {message}")
print(f"ChaCha20 Encrypted: {base64.b64encode(encrypted).decode()}")
print(f"ChaCha20 Nonce: {base64.b64encode(nonce).decode()}")
print(f"ChaCha20 Decrypted: {decrypted}")

# RC4 (histórico, inseguro)
rc4 = RC4Cipher()
rc4_key = "clave_secreta"
rc4_message = "Mensaje RC4"

rc4_encrypted = rc4.encrypt_decrypt(rc4_message, rc4_key)
rc4_decrypted = rc4.encrypt_decrypt(rc4_encrypted, rc4_key)
rc4_decrypted_str = ''.join(chr(c) for c in rc4_decrypted)

print(f"\nRC4 Original: {rc4_message}")
print(f"RC4 Encrypted: {[hex(c) for c in rc4_encrypted]}")
print(f"RC4 Decrypted: {rc4_decrypted_str}")
```

---

## Cifrado Asimétrico

### RSA (Rivest-Shamir-Adleman)

#### Implementación Educativa RSA
```python
import random
import math
from cryptography.hazmat.primitives.asymmetric import rsa, padding
from cryptography.hazmat.primitives import serialization, hashes

class RSAEducational:
    """
    Implementación educativa de RSA para entender los conceptos
    NO usar en producción - usar bibliotecas criptográficas probadas
    """
    
    def __init__(self, key_size=512):  # Tamaño pequeño para demostración
        self.key_size = key_size
        self.public_key = None
        self.private_key = None
    
    def is_prime(self, n, k=5):
        """Test de primalidad Miller-Rabin"""
        if n < 2:
            return False
        if n in (2, 3):
            return True
        if n % 2 == 0:
            return False
        
        # Escribir n-1 como 2^r * d
        r = 0
        d = n - 1
        while d % 2 == 0:
            r += 1
            d //= 2
        
        # Test Miller-Rabin k veces
        for _ in range(k):
            a = random.randrange(2, n - 1)
            x = pow(a, d, n)
            
            if x == 1 or x == n - 1:
                continue
            
            for _ in range(r - 1):
                x = pow(x, 2, n)
                if x == n - 1:
                    break
            else:
                return False
        
        return True
    
    def generate_prime(self, bits):
        """Generar número primo de tamaño específico"""
        while True:
            n = random.getrandbits(bits)
            n |= (1 << bits - 1) | 1  # Asegurar que sea impar y del tamaño correcto
            if self.is_prime(n):
                return n
    
    def gcd(self, a, b):
        """Algoritmo de Euclides para MCD"""
        while b:
            a, b = b, a % b
        return a
    
    def extended_gcd(self, a, b):
        """Algoritmo extendido de Euclides"""
        if a == 0:
            return b, 0, 1
        gcd, x1, y1 = self.extended_gcd(b % a, a)
        x = y1 - (b // a) * x1
        y = x1
        return gcd, x, y
    
    def mod_inverse(self, e, phi):
        """Inverso modular usando algoritmo extendido de Euclides"""
        gcd, x, _ = self.extended_gcd(e, phi)
        if gcd != 1:
            raise ValueError("El inverso modular no existe")
        return (x % phi + phi) % phi
    
    def generate_keypair(self):
        """Generar par de claves RSA"""
        # Paso 1: Generar dos primos grandes p y q
        p = self.generate_prime(self.key_size // 2)
        q = self.generate_prime(self.key_size // 2)
        
        # Paso 2: Calcular n = p * q
        n = p * q
        
        # Paso 3: Calcular φ(n) = (p-1)(q-1)
        phi = (p - 1) * (q - 1)
        
        # Paso 4: Elegir e tal que 1 < e < φ(n) y gcd(e, φ(n)) = 1
        e = 65537  # Exponente público común
        if self.gcd(e, phi) != 1:
            # Si e no es coprimo con phi, buscar otro
            for e in range(3, phi, 2):
                if self.gcd(e, phi) == 1:
                    break
        
        # Paso 5: Calcular d tal que d*e ≡ 1 (mod φ(n))
        d = self.mod_inverse(e, phi)
        
        # Claves pública y privada
        self.public_key = (n, e)
        self.private_key = (n, d)
        
        return {
            'public': self.public_key,
            'private': self.private_key,
            'parameters': {'p': p, 'q': q, 'phi': phi}
        }
    
    def encrypt(self, message, public_key):
        """Cifrar mensaje con clave pública"""
        n, e = public_key
        
        if isinstance(message, str):
            # Convertir string a entero
            message_bytes = message.encode('utf-8')
            m = int.from_bytes(message_bytes, 'big')
        else:
            m = message
        
        if m >= n:
            raise ValueError("Mensaje demasiado grande para el tamaño de clave")
        
        # c = m^e mod n
        ciphertext = pow(m, e, n)
        return ciphertext
    
    def decrypt(self, ciphertext, private_key):
        """Descifrar con clave privada"""
        n, d = private_key
        
        # m = c^d mod n
        decrypted = pow(ciphertext, d, n)
        
        try:
            # Convertir entero a string
            message_bytes = decrypted.to_bytes((decrypted.bit_length() + 7) // 8, 'big')
            return message_bytes.decode('utf-8')
        except:
            return decrypted

# RSA con bibliotecas criptográficas profesionales
class RSAProduction:
    def __init__(self, key_size=2048):
        self.key_size = key_size
        self.private_key = None
        self.public_key = None
    
    def generate_keypair(self):
        """Generar par de claves RSA usando biblioteca segura"""
        self.private_key = rsa.generate_private_key(
            public_exponent=65537,
            key_size=self.key_size,
        )
        self.public_key = self.private_key.public_key()
        
        return self.private_key, self.public_key
    
    def encrypt(self, message, public_key):
        """Cifrar con padding OAEP (recomendado)"""
        if isinstance(message, str):
            message = message.encode('utf-8')
        
        ciphertext = public_key.encrypt(
            message,
            padding.OAEP(
                mgf=padding.MGF1(algorithm=hashes.SHA256()),
                algorithm=hashes.SHA256(),
                label=None
            )
        )
        return ciphertext
    
    def decrypt(self, ciphertext, private_key):
        """Descifrar con padding OAEP"""
        plaintext = private_key.decrypt(
            ciphertext,
            padding.OAEP(
                mgf=padding.MGF1(algorithm=hashes.SHA256()),
                algorithm=hashes.SHA256(),
                label=None
            )
        )
        return plaintext.decode('utf-8')
    
    def sign(self, message, private_key):
        """Crear firma digital"""
        if isinstance(message, str):
            message = message.encode('utf-8')
        
        signature = private_key.sign(
            message,
            padding.PSS(
                mgf=padding.MGF1(hashes.SHA256()),
                salt_length=padding.PSS.MAX_LENGTH
            ),
            hashes.SHA256()
        )
        return signature
    
    def verify_signature(self, message, signature, public_key):
        """Verificar firma digital"""
        if isinstance(message, str):
            message = message.encode('utf-8')
        
        try:
            public_key.verify(
                signature,
                message,
                padding.PSS(
                    mgf=padding.MGF1(hashes.SHA256()),
                    salt_length=padding.PSS.MAX_LENGTH
                ),
                hashes.SHA256()
            )
            return True
        except:
            return False
    
    def export_keys(self):
        """Exportar claves en formato PEM"""
        private_pem = self.private_key.private_bytes(
            encoding=serialization.Encoding.PEM,
            format=serialization.PrivateFormat.PKCS8,
            encryption_algorithm=serialization.NoEncryption()
        )
        
        public_pem = self.public_key.public_bytes(
            encoding=serialization.Encoding.PEM,
            format=serialization.PublicFormat.SubjectPublicKeyInfo
        )
        
        return private_pem, public_pem

# Ejemplo de uso RSA
print("=== RSA Cifrado Asimétrico ===")

# Implementación educativa (conceptos básicos)
rsa_edu = RSAEducational(512)  # Tamaño pequeño para demostración
keys = rsa_edu.generate_keypair()

print("Parámetros RSA educativo:")
print(f"p: {keys['parameters']['p']}")
print(f"q: {keys['parameters']['q']}")
print(f"n: {keys['public'][0]}")
print(f"e: {keys['public'][1]}")
print(f"d: {keys['private'][1]}")

# Cifrado/descifrado educativo
message = "Hola RSA!"
try:
    encrypted_edu = rsa_edu.encrypt(message, keys['public'])
    decrypted_edu = rsa_edu.decrypt(encrypted_edu, keys['private'])
    print(f"\nMensaje original: {message}")
    print(f"Cifrado educativo: {encrypted_edu}")
    print(f"Descifrado educativo: {decrypted_edu}")
except Exception as e:
    print(f"Error en RSA educativo: {e}")

# Implementación profesional
rsa_prod = RSAProduction(2048)
private_key, public_key = rsa_prod.generate_keypair()

# Cifrado seguro
message_prod = "Mensaje secreto con RSA profesional"
encrypted_prod = rsa_prod.encrypt(message_prod, public_key)
decrypted_prod = rsa_prod.decrypt(encrypted_prod, private_key)

print(f"\nRSA Producción:")
print(f"Mensaje: {message_prod}")
print(f"Cifrado: {base64.b64encode(encrypted_prod).decode()}")
print(f"Descifrado: {decrypted_prod}")

# Firma digital
signature = rsa_prod.sign(message_prod, private_key)
is_valid = rsa_prod.verify_signature(message_prod, signature, public_key)
print(f"Firma válida: {is_valid}")

# Exportar claves
private_pem, public_pem = rsa_prod.export_keys()
print(f"\nClave pública PEM:\n{public_pem.decode()}")
```

### Criptografía de Curvas Elípticas (ECC)

#### Implementación ECC
```python
from cryptography.hazmat.primitives.asymmetric import ec
from cryptography.hazmat.primitives import serialization, hashes

class ECCCryptography:
    def __init__(self, curve=ec.SECP256R1()):
        self.curve = curve
        self.private_key = None
        self.public_key = None
    
    def generate_keypair(self):
        """Generar par de claves ECC"""
        self.private_key = ec.generate_private_key(self.curve)
        self.public_key = self.private_key.public_key()
        return self.private_key, self.public_key
    
    def create_shared_key(self, private_key, peer_public_key):
        """Crear clave compartida usando ECDH"""
        shared_key = private_key.exchange(
            ec.ECDH(), peer_public_key
        )
        return shared_key
    
    def sign_message(self, message, private_key):
        """Firmar mensaje con ECDSA"""
        if isinstance(message, str):
            message = message.encode('utf-8')
        
        signature = private_key.sign(
            message,
            ec.ECDSA(hashes.SHA256())
        )
        return signature
    
    def verify_signature(self, message, signature, public_key):
        """Verificar firma ECDSA"""
        if isinstance(message, str):
            message = message.encode('utf-8')
        
        try:
            public_key.verify(
                signature,
                message,
                ec.ECDSA(hashes.SHA256())
            )
            return True
        except:
            return False
    
    def export_keys(self):
        """Exportar claves ECC"""
        private_pem = self.private_key.private_bytes(
            encoding=serialization.Encoding.PEM,
            format=serialization.PrivateFormat.PKCS8,
            encryption_algorithm=serialization.NoEncryption()
        )
        
        public_pem = self.public_key.public_bytes(
            encoding=serialization.Encoding.PEM,
            format=serialization.PublicFormat.SubjectPublicKeyInfo
        )
        
        return private_pem, public_pem
    
    def demonstrate_ecdh(self):
        """Demostrar intercambio de claves ECDH"""
        # Alice genera sus claves
        alice_private = ec.generate_private_key(self.curve)
        alice_public = alice_private.public_key()
        
        # Bob genera sus claves
        bob_private = ec.generate_private_key(self.curve)
        bob_public = bob_private.public_key()
        
        # Intercambio de claves
        alice_shared = alice_private.exchange(ec.ECDH(), bob_public)
        bob_shared = bob_private.exchange(ec.ECDH(), bob_public)
        
        return {
            'alice_shared': alice_shared,
            'bob_shared': bob_shared,
            'keys_match': alice_shared == bob_shared
        }

# Ejemplo de uso ECC
print("=== Criptografía de Curvas Elípticas (ECC) ===")

ecc = ECCCryptography()
private_key, public_key = ecc.generate_keypair()

# Firma digital con ECDSA
message = "Mensaje para firmar con ECDSA"
signature = ecc.sign_message(message, private_key)
is_valid = ecc.verify_signature(message, signature, public_key)

print(f"Mensaje: {message}")
print(f"Firma válida: {is_valid}")
print(f"Firma: {base64.b64encode(signature).decode()}")

# Demostrar ECDH
ecdh_demo = ecc.demonstrate_ecdh()
print(f"\nECDH Key Exchange:")
print(f"Alice shared key: {base64.b64encode(ecdh_demo['alice_shared']).decode()}")
print(f"Bob shared key: {base64.b64encode(ecdh_demo['bob_shared']).decode()}")
print(f"Keys match: {ecdh_demo['keys_match']}")

# Exportar claves
private_pem, public_pem = ecc.export_keys()
print(f"\nECC Public Key:\n{public_pem.decode()[:200]}...")
```

---

## Funciones Hash

### Propiedades de las Funciones Hash Criptográficas

#### Características Fundamentales
```
Hash Function Properties:
┌─────────────────────────────────────────────────────────────┐
│ 1. Deterministic                                           │
│    └── Same input always produces same output              │
│                                                             │
│ 2. Fixed Output Size                                        │
│    └── Output length is constant regardless of input size  │
│                                                             │
│ 3. Fast Computation                                         │
│    └── Efficient to compute hash for any input             │
│                                                             │
│ 4. Pre-image Resistance (One-way)                          │
│    └── Given h, infeasible to find x such that hash(x)=h   │
│                                                             │
│ 5. Second Pre-image Resistance                              │
│    └── Given x, infeasible to find y≠x with hash(x)=hash(y)│
│                                                             │
│ 6. Collision Resistance                                     │
│    └── Infeasible to find any x,y where hash(x)=hash(y)    │
│                                                             │
│ 7. Avalanche Effect                                         │
│    └── Small input change causes large output change       │
└─────────────────────────────────────────────────────────────┘
```

#### Implementación de Funciones Hash
```python
import hashlib
import hmac
import os
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC
from cryptography.hazmat.primitives.kdf.scrypt import Scrypt

class HashFunctions:
    def __init__(self):
        self.supported_algorithms = ['md5', 'sha1', 'sha256', 'sha384', 'sha512', 'sha3_256', 'sha3_512']
    
    def hash_message(self, message, algorithm='sha256'):
        """Calcular hash de un mensaje"""
        if isinstance(message, str):
            message = message.encode('utf-8')
        
        if algorithm not in self.supported_algorithms:
            raise ValueError(f"Algoritmo no soportado: {algorithm}")
        
        hash_func = getattr(hashlib, algorithm)()
        hash_func.update(message)
        
        return {
            'algorithm': algorithm,
            'input': message.decode('utf-8'),
            'hash_hex': hash_func.hexdigest(),
            'hash_bytes': hash_func.digest(),
            'hash_length': len(hash_func.digest())
        }
    
    def compare_algorithms(self, message):
        """Comparar diferentes algoritmos hash"""
        results = {}
        
        for algorithm in self.supported_algorithms:
            try:
                result = self.hash_message(message, algorithm)
                results[algorithm] = {
                    'hash': result['hash_hex'],
                    'length': result['hash_length']
                }
            except:
                results[algorithm] = {'error': 'Algorithm not available'}
        
        return results
    
    def demonstrate_avalanche_effect(self, message):
        """Demostrar efecto avalancha"""
        original_hash = self.hash_message(message, 'sha256')
        
        # Cambiar un solo carácter
        modified_message = message[:-1] + ('a' if message[-1] != 'a' else 'b')
        modified_hash = self.hash_message(modified_message, 'sha256')
        
        # Calcular diferencias de bits
        orig_bytes = bytes.fromhex(original_hash['hash_hex'])
        mod_bytes = bytes.fromhex(modified_hash['hash_hex'])
        
        different_bits = 0
        for i in range(len(orig_bytes)):
            xor_result = orig_bytes[i] ^ mod_bytes[i]
            different_bits += bin(xor_result).count('1')
        
        total_bits = len(orig_bytes) * 8
        change_percentage = (different_bits / total_bits) * 100
        
        return {
            'original_message': message,
            'modified_message': modified_message,
            'original_hash': original_hash['hash_hex'],
            'modified_hash': modified_hash['hash_hex'],
            'different_bits': different_bits,
            'total_bits': total_bits,
            'change_percentage': change_percentage
        }
    
    def hash_file(self, file_path, algorithm='sha256', chunk_size=8192):
        """Calcular hash de archivo grande"""
        hash_func = getattr(hashlib, algorithm)()
        
        try:
            with open(file_path, 'rb') as f:
                while chunk := f.read(chunk_size):
                    hash_func.update(chunk)
            
            return {
                'file': file_path,
                'algorithm': algorithm,
                'hash': hash_func.hexdigest()
            }
        except FileNotFoundError:
            return {'error': f'File not found: {file_path}'}
    
    def create_hmac(self, message, key, algorithm='sha256'):
        """Crear HMAC (Hash-based Message Authentication Code)"""
        if isinstance(message, str):
            message = message.encode('utf-8')
        if isinstance(key, str):
            key = key.encode('utf-8')
        
        hmac_result = hmac.new(key, message, getattr(hashlib, algorithm))
        
        return {
            'message': message.decode('utf-8'),
            'algorithm': f'HMAC-{algorithm.upper()}',
            'hmac_hex': hmac_result.hexdigest(),
            'hmac_bytes': hmac_result.digest()
        }
    
    def verify_hmac(self, message, key, expected_hmac, algorithm='sha256'):
        """Verificar HMAC"""
        computed_hmac = self.create_hmac(message, key, algorithm)
        
        # Comparación segura contra timing attacks
        try:
            return hmac.compare_digest(
                computed_hmac['hmac_hex'],
                expected_hmac
            )
        except:
            return False

# Funciones de derivación de claves seguras
class SecureKeyDerivation:
    def __init__(self):
        pass
    
    def pbkdf2_derive(self, password, salt=None, iterations=100000, key_length=32, algorithm='sha256'):
        """Derivar clave usando PBKDF2"""
        if isinstance(password, str):
            password = password.encode('utf-8')
        
        if salt is None:
            salt = os.urandom(16)
        
        hash_algorithm = getattr(hashes, algorithm.upper())()
        
        kdf = PBKDF2HMAC(
            algorithm=hash_algorithm,
            length=key_length,
            salt=salt,
            iterations=iterations,
        )
        
        derived_key = kdf.derive(password)
        
        return {
            'algorithm': f'PBKDF2-{algorithm.upper()}',
            'iterations': iterations,
            'salt': base64.b64encode(salt).decode(),
            'derived_key': base64.b64encode(derived_key).decode(),
            'key_length': key_length
        }
    
    def scrypt_derive(self, password, salt=None, n=16384, r=8, p=1, key_length=32):
        """Derivar clave usando scrypt"""
        if isinstance(password, str):
            password = password.encode('utf-8')
        
        if salt is None:
            salt = os.urandom(16)
        
        kdf = Scrypt(
            algorithm=hashes.SHA256(),
            length=key_length,
            salt=salt,
            n=n,
            r=r,
            p=p,
        )
        
        derived_key = kdf.derive(password)
        
        return {
            'algorithm': 'scrypt',
            'parameters': f'N={n}, r={r}, p={p}',
            'salt': base64.b64encode(salt).decode(),
            'derived_key': base64.b64encode(derived_key).decode(),
            'key_length': key_length
        }

# Ejemplos de uso
print("=== Funciones Hash Criptográficas ===")

hash_func = HashFunctions()

# Comparar algoritmos
message = "Este es un mensaje para hashear"
comparison = hash_func.compare_algorithms(message)

print("Comparación de algoritmos hash:")
for algo, result in comparison.items():
    if 'error' not in result:
        print(f"{algo.upper():>10}: {result['hash'][:64]}... ({result['length']} bytes)")

# Demostrar efecto avalancha
avalanche = hash_func.demonstrate_avalanche_effect("Hello World!")
print(f"\n=== Efecto Avalancha ===")
print(f"Mensaje original: '{avalanche['original_message']}'")
print(f"Mensaje modificado: '{avalanche['modified_message']}'")
print(f"Hash original:  {avalanche['original_hash']}")
print(f"Hash modificado: {avalanche['modified_hash']}")
print(f"Bits diferentes: {avalanche['different_bits']}/{avalanche['total_bits']} ({avalanche['change_percentage']:.1f}%)")

# HMAC
hmac_key = "mi_clave_secreta"
hmac_result = hash_func.create_hmac(message, hmac_key)
print(f"\n=== HMAC ===")
print(f"Mensaje: {hmac_result['message']}")
print(f"HMAC: {hmac_result['hmac_hex']}")

# Verificar HMAC
is_valid_hmac = hash_func.verify_hmac(message, hmac_key, hmac_result['hmac_hex'])
print(f"HMAC válido: {is_valid_hmac}")

# Derivación de claves
kdf = SecureKeyDerivation()

# PBKDF2
pbkdf2_result = kdf.pbkdf2_derive("mi_password_seguro", iterations=100000)
print(f"\n=== Derivación de Claves ===")
print(f"PBKDF2:")
print(f"  Algoritmo: {pbkdf2_result['algorithm']}")
print(f"  Iteraciones: {pbkdf2_result['iterations']}")
print(f"  Salt: {pbkdf2_result['salt']}")
print(f"  Clave derivada: {pbkdf2_result['derived_key'][:32]}...")

# scrypt
scrypt_result = kdf.scrypt_derive("mi_password_seguro")
print(f"\nscrypt:")
print(f"  Algoritmo: {scrypt_result['algorithm']}")
print(f"  Parámetros: {scrypt_result['parameters']}")
print(f"  Salt: {scrypt_result['salt']}")
print(f"  Clave derivada: {scrypt_result['derived_key'][:32]}...")
```

---

## Firma Digital

### Principios de la Firma Digital

#### Conceptos Fundamentales
```
Digital Signature Properties:
┌─────────────────────────────────────────────────────────────┐
│ Authentication                                              │
│ ├── Verifies sender identity                                │
│ └── Proves message origin                                   │
│                                                             │
│ Integrity                                                   │
│ ├── Detects message tampering                               │
│ └── Ensures data hasn't been altered                       │
│                                                             │
│ Non-repudiation                                             │
│ ├── Sender cannot deny signing                              │
│ └── Legal proof of authorship                               │
│                                                             │
│ Unforgeable                                                 │
│ ├── Only holder of private key can create                   │
│ └── Computationally infeasible to forge                     │
└─────────────────────────────────────────────────────────────┘

Signature Process:
1. Message → Hash Function → Message Digest
2. Message Digest → Private Key → Digital Signature
3. Send: Original Message + Digital Signature

Verification Process:
1. Received Message → Hash Function → Message Digest A
2. Digital Signature → Public Key → Message Digest B
3. Compare: Message Digest A == Message Digest B
```

#### Implementación de Firma Digital
```python
from datetime import datetime, timedelta
import json

class DigitalSignatureSystem:
    def __init__(self):
        self.rsa_system = RSAProduction(2048)
        self.ecc_system = ECCCryptography()
        self.signatures_log = []
    
    def create_document(self, content, author, document_type="text"):
        """Crear documento estructurado para firmar"""
        document = {
            'content': content,
            'author': author,
            'document_type': document_type,
            'created_at': datetime.now().isoformat(),
            'version': '1.0',
            'metadata': {
                'length': len(content),
                'hash_preview': hashlib.sha256(content.encode()).hexdigest()[:16]
            }
        }
        return document
    
    def sign_document_rsa(self, document, private_key, certificate_info=None):
        """Firmar documento usando RSA"""
        # Serializar documento a JSON
        document_json = json.dumps(document, sort_keys=True)
        
        # Crear hash del documento
        document_hash = hashlib.sha256(document_json.encode()).hexdigest()
        
        # Firmar el hash
        signature = self.rsa_system.sign(document_json, private_key)
        
        # Crear estructura de firma
        signature_data = {
            'document_hash': document_hash,
            'signature': base64.b64encode(signature).decode(),
            'algorithm': 'RSA-PSS-SHA256',
            'signed_at': datetime.now().isoformat(),
            'certificate_info': certificate_info,
            'signature_id': hashlib.md5(signature).hexdigest()[:16]
        }
        
        # Registrar en log
        self.signatures_log.append({
            'signature_id': signature_data['signature_id'],
            'document_hash': document_hash,
            'signed_at': signature_data['signed_at'],
            'algorithm': signature_data['algorithm']
        })
        
        return {
            'document': document,
            'signature': signature_data
        }
    
    def verify_document_rsa(self, signed_document, public_key):
        """Verificar firma RSA de documento"""
        document = signed_document['document']
        signature_data = signed_document['signature']
        
        try:
            # Recrear JSON del documento
            document_json = json.dumps(document, sort_keys=True)
            
            # Verificar hash
            current_hash = hashlib.sha256(document_json.encode()).hexdigest()
            if current_hash != signature_data['document_hash']:
                return {
                    'valid': False,
                    'reason': 'Document has been modified',
                    'current_hash': current_hash,
                    'original_hash': signature_data['document_hash']
                }
            
            # Verificar firma
            signature_bytes = base64.b64decode(signature_data['signature'])
            is_valid = self.rsa_system.verify_signature(
                document_json, signature_bytes, public_key
            )
            
            verification_result = {
                'valid': is_valid,
                'signature_id': signature_data['signature_id'],
                'algorithm': signature_data['algorithm'],
                'signed_at': signature_data['signed_at'],
                'verified_at': datetime.now().isoformat()
            }
            
            if not is_valid:
                verification_result['reason'] = 'Invalid signature'
            
            return verification_result
            
        except Exception as e:
            return {
                'valid': False,
                'reason': f'Verification error: {str(e)}'
            }
    
    def sign_document_ecc(self, document, private_key):
        """Firmar documento usando ECDSA"""
        document_json = json.dumps(document, sort_keys=True)
        signature = self.ecc_system.sign_message(document_json, private_key)
        
        signature_data = {
            'document_hash': hashlib.sha256(document_json.encode()).hexdigest(),
            'signature': base64.b64encode(signature).decode(),
            'algorithm': 'ECDSA-SHA256',
            'signed_at': datetime.now().isoformat(),
            'signature_id': hashlib.md5(signature).hexdigest()[:16]
        }
        
        return {
            'document': document,
            'signature': signature_data
        }
    
    def verify_document_ecc(self, signed_document, public_key):
        """Verificar firma ECDSA de documento"""
        document = signed_document['document']
        signature_data = signed_document['signature']
        
        try:
            document_json = json.dumps(document, sort_keys=True)
            
            # Verificar hash
            current_hash = hashlib.sha256(document_json.encode()).hexdigest()
            if current_hash != signature_data['document_hash']:
                return {'valid': False, 'reason': 'Document modified'}
            
            # Verificar firma
            signature_bytes = base64.b64decode(signature_data['signature'])
            is_valid = self.ecc_system.verify_signature(
                document_json, signature_bytes, public_key
            )
            
            return {
                'valid': is_valid,
                'signature_id': signature_data['signature_id'],
                'algorithm': signature_data['algorithm'],
                'verified_at': datetime.now().isoformat()
            }
            
        except Exception as e:
            return {'valid': False, 'reason': f'Error: {str(e)}'}
    
    def create_timestamp_signature(self, document, private_key, timestamp_authority="Internal TSA"):
        """Crear firma con timestamp"""
        signed_doc = self.sign_document_rsa(document, private_key)
        
        # Añadir timestamp
        timestamp_data = {
            'timestamp': datetime.now().isoformat(),
            'authority': timestamp_authority,
            'accuracy': '1 second',
            'tsa_signature': 'tsa_signature_placeholder'  # En implementación real
        }
        
        signed_doc['timestamp'] = timestamp_data
        return signed_doc
    
    def get_signatures_report(self):
        """Generar reporte de firmas"""
        return {
            'total_signatures': len(self.signatures_log),
            'signatures': self.signatures_log,
            'report_generated_at': datetime.now().isoformat()
        }

# Ejemplo de uso de firma digital
print("=== Sistema de Firma Digital ===")

# Inicializar sistema
sig_system = DigitalSignatureSystem()

# Generar claves RSA y ECC
rsa_private, rsa_public = sig_system.rsa_system.generate_keypair()
ecc_private, ecc_public = sig_system.ecc_system.generate_keypair()

# Crear documento
document = sig_system.create_document(
    content="Este es un contrato digital importante que debe ser firmado.",
    author="Juan Pérez",
    document_type="contract"
)

print("Documento original:")
print(json.dumps(document, indent=2))

# Firmar con RSA
certificate_info = {
    'subject': 'CN=Juan Pérez,O=Empresa XYZ',
    'issuer': 'CN=CA Authority',
    'serial_number': '12345',
    'valid_until': (datetime.now() + timedelta(days=365)).isoformat()
}

signed_rsa = sig_system.sign_document_rsa(
    document, rsa_private, certificate_info
)

print(f"\n=== Firma RSA ===")
print(f"Signature ID: {signed_rsa['signature']['signature_id']}")
print(f"Algorithm: {signed_rsa['signature']['algorithm']}")
print(f"Document Hash: {signed_rsa['signature']['document_hash']}")

# Verificar firma RSA
verification_rsa = sig_system.verify_document_rsa(signed_rsa, rsa_public)
print(f"RSA Verification: {verification_rsa}")

# Firmar con ECC
signed_ecc = sig_system.sign_document_ecc(document, ecc_private)
verification_ecc = sig_system.verify_document_ecc(signed_ecc, ecc_public)

print(f"\n=== Firma ECC ===")
print(f"ECC Verification: {verification_ecc}")

# Probar modificación de documento (debe fallar verificación)
tampered_document = signed_rsa.copy()
tampered_document['document']['content'] = "Documento modificado maliciosamente"

verification_tampered = sig_system.verify_document_rsa(tampered_document, rsa_public)
print(f"\n=== Documento Modificado ===")
print(f"Tampered Verification: {verification_tampered}")

# Reporte de firmas
report = sig_system.get_signatures_report()
print(f"\n=== Reporte de Firmas ===")
print(f"Total signatures: {report['total_signatures']}")
```

---

## Infraestructura de Clave Pública (PKI)

### Componentes de PKI

#### Arquitectura PKI
```
PKI Architecture:
┌─────────────────────────────────────────────────────────────┐
│                     Root CA                                 │
│              ┌─────────────────┐                            │
│              │   Root Certificate │                         │
│              │   Self-Signed      │                         │
│              │   Long-term validity│                        │
│              └─────────────────┘                            │
│                       │                                     │
│              ┌─────────┴─────────┐                          │
│              │                   │                          │
│         Intermediate CA     Intermediate CA                 │
│      ┌─────────────────┐   ┌─────────────────┐              │
│      │  Issued by Root │   │  Issued by Root │              │
│      │  Signs End-user │   │  Signs End-user │              │
│      │  Certificates   │   │  Certificates   │              │
│      └─────────────────┘   └─────────────────┘              │
│              │                       │                      │
│      ┌───────┴───────┐       ┌─────────┴─────────┐          │
│      │               │       │                   │          │
│  End-Entity     End-Entity  Server           Client         │
│ Certificates   Certificates Certificates   Certificates     │
│                                                             │
│ Supporting Components:                                      │
│ • Certificate Repository (LDAP/HTTP)                       │
│ • Certificate Revocation List (CRL)                        │
│ • Online Certificate Status Protocol (OCSP)               │
│ • Registration Authority (RA)                              │
│ • Time Stamping Authority (TSA)                            │
└─────────────────────────────────────────────────────────────┘
```

#### Implementación PKI Simulada
```python
import uuid
from datetime import datetime, timedelta
from enum import Enum
from cryptography.x509.oid import NameOID, ExtendedKeyUsageOID
from cryptography import x509
from cryptography.x509 import load_pem_x509_certificate
import ipaddress

class CertificateType(Enum):
    ROOT_CA = "root_ca"
    INTERMEDIATE_CA = "intermediate_ca"
    END_ENTITY = "end_entity"
    SERVER = "server"
    CLIENT = "client"
    CODE_SIGNING = "code_signing"

class PKIManager:
    def __init__(self):
        self.certificates = {}
        self.private_keys = {}
        self.revoked_certificates = []
        self.serial_number_counter = 1000000
    
    def generate_serial_number(self):
        """Generar número de serie único"""
        self.serial_number_counter += 1
        return self.serial_number_counter
    
    def create_certificate_name(self, common_name, organization=None, 
                               organizational_unit=None, country=None, 
                               state=None, city=None, email=None):
        """Crear nombre X.509 para certificado"""
        name_components = [x509.NameAttribute(NameOID.COMMON_NAME, common_name)]
        
        if organization:
            name_components.append(x509.NameAttribute(NameOID.ORGANIZATION_NAME, organization))
        if organizational_unit:
            name_components.append(x509.NameAttribute(NameOID.ORGANIZATIONAL_UNIT_NAME, organizational_unit))
        if country:
            name_components.append(x509.NameAttribute(NameOID.COUNTRY_NAME, country))
        if state:
            name_components.append(x509.NameAttribute(NameOID.STATE_OR_PROVINCE_NAME, state))
        if city:
            name_components.append(x509.NameAttribute(NameOID.LOCALITY_NAME, city))
        if email:
            name_components.append(x509.NameAttribute(NameOID.EMAIL_ADDRESS, email))
        
        return x509.Name(name_components)
    
    def create_root_ca_certificate(self, common_name="Root CA", 
                                  organization="Mi Organizacion", 
                                  validity_years=10):
        """Crear certificado raíz CA"""
        # Generar clave privada
        private_key = rsa.generate_private_key(
            public_exponent=65537,
            key_size=4096,
        )
        
        # Crear nombre del certificado
        subject = issuer = self.create_certificate_name(
            common_name=common_name,
            organization=organization,
            organizational_unit="Security Department",
            country="US",
            state="California",
            city="San Francisco"
        )
        
        # Configurar certificado
        builder = x509.CertificateBuilder()
        builder = builder.subject_name(subject)
        builder = builder.issuer_name(issuer)
        builder = builder.public_key(private_key.public_key())
        builder = builder.serial_number(self.generate_serial_number())
        builder = builder.not_valid_before(datetime.utcnow())
        builder = builder.not_valid_after(datetime.utcnow() + timedelta(days=validity_years*365))
        
        # Añadir extensiones para CA
        builder = builder.add_extension(
            x509.BasicConstraints(ca=True, path_length=None),
            critical=True
        )
        builder = builder.add_extension(
            x509.KeyUsage(
                key_cert_sign=True,
                crl_sign=True,
                key_encipherment=False,
                data_encipherment=False,
                key_agreement=False,
                content_commitment=False,
                digital_signature=True,
                encipher_only=False,
                decipher_only=False
            ),
            critical=True
        )
        builder = builder.add_extension(
            x509.SubjectKeyIdentifier.from_public_key(private_key.public_key()),
            critical=False
        )
        
        # Firmar certificado (auto-firmado para root CA)
        certificate = builder.sign(private_key, hashes.SHA256())
        
        # Almacenar
        cert_id = str(certificate.serial_number)
        self.certificates[cert_id] = {
            'certificate': certificate,
            'type': CertificateType.ROOT_CA,
            'created_at': datetime.now(),
            'issuer_id': cert_id,  # Auto-firmado
            'status': 'active'
        }
        self.private_keys[cert_id] = private_key
        
        return cert_id, certificate, private_key
    
    def create_intermediate_ca_certificate(self, root_ca_id, 
                                          common_name="Intermediate CA",
                                          organization="Mi Organizacion",
                                          validity_years=5):
        """Crear certificado CA intermedio"""
        if root_ca_id not in self.certificates:
            raise ValueError("Root CA not found")
        
        root_ca_cert = self.certificates[root_ca_id]['certificate']
        root_ca_key = self.private_keys[root_ca_id]
        
        # Generar nueva clave privada
        private_key = rsa.generate_private_key(
            public_exponent=65537,
            key_size=2048,
        )
        
        # Crear nombre del certificado
        subject = self.create_certificate_name(
            common_name=common_name,
            organization=organization,
            organizational_unit="Intermediate CA",
            country="US"
        )
        
        # Configurar certificado
        builder = x509.CertificateBuilder()
        builder = builder.subject_name(subject)
        builder = builder.issuer_name(root_ca_cert.subject)
        builder = builder.public_key(private_key.public_key())
        builder = builder.serial_number(self.generate_serial_number())
        builder = builder.not_valid_before(datetime.utcnow())
        builder = builder.not_valid_after(datetime.utcnow() + timedelta(days=validity_years*365))
        
        # Extensiones para CA intermedia
        builder = builder.add_extension(
            x509.BasicConstraints(ca=True, path_length=0),  # No puede crear más CAs
            critical=True
        )
        builder = builder.add_extension(
            x509.KeyUsage(
                key_cert_sign=True,
                crl_sign=True,
                digital_signature=True,
                key_encipherment=False,
                data_encipherment=False,
                key_agreement=False,
                content_commitment=False,
                encipher_only=False,
                decipher_only=False
            ),
            critical=True
        )
        builder = builder.add_extension(
            x509.SubjectKeyIdentifier.from_public_key(private_key.public_key()),
            critical=False
        )
        builder = builder.add_extension(
            x509.AuthorityKeyIdentifier.from_issuer_public_key(root_ca_cert.public_key()),
            critical=False
        )
        
        # Firmar con clave del root CA
        certificate = builder.sign(root_ca_key, hashes.SHA256())
        
        # Almacenar
        cert_id = str(certificate.serial_number)
        self.certificates[cert_id] = {
            'certificate': certificate,
            'type': CertificateType.INTERMEDIATE_CA,
            'created_at': datetime.now(),
            'issuer_id': root_ca_id,
            'status': 'active'
        }
        self.private_keys[cert_id] = private_key
        
        return cert_id, certificate, private_key
    
    def create_end_entity_certificate(self, ca_id, common_name, 
                                     certificate_type=CertificateType.END_ENTITY,
                                     organization=None, email=None,
                                     dns_names=None, ip_addresses=None,
                                     validity_days=365):
        """Crear certificado de entidad final"""
        if ca_id not in self.certificates:
            raise ValueError("CA certificate not found")
        
        ca_cert = self.certificates[ca_id]['certificate']
        ca_key = self.private_keys[ca_id]
        
        # Generar clave privada
        private_key = rsa.generate_private_key(
            public_exponent=65537,
            key_size=2048,
        )
        
        # Crear nombre del certificado
        subject = self.create_certificate_name(
            common_name=common_name,
            organization=organization,
            email=email
        )
        
        # Configurar certificado
        builder = x509.CertificateBuilder()
        builder = builder.subject_name(subject)
        builder = builder.issuer_name(ca_cert.subject)
        builder = builder.public_key(private_key.public_key())
        builder = builder.serial_number(self.generate_serial_number())
        builder = builder.not_valid_before(datetime.utcnow())
        builder = builder.not_valid_after(datetime.utcnow() + timedelta(days=validity_days))
        
        # Extensiones básicas
        builder = builder.add_extension(
            x509.BasicConstraints(ca=False, path_length=None),
            critical=True
        )
        
        # Configurar uso de clave según tipo
        if certificate_type == CertificateType.SERVER:
            key_usage = x509.KeyUsage(
                key_encipherment=True,
                digital_signature=True,
                key_agreement=False,
                key_cert_sign=False,
                crl_sign=False,
                content_commitment=False,
                data_encipherment=False,
                encipher_only=False,
                decipher_only=False
            )
            extended_key_usage = x509.ExtendedKeyUsage([
                ExtendedKeyUsageOID.SERVER_AUTH
            ])
        elif certificate_type == CertificateType.CLIENT:
            key_usage = x509.KeyUsage(
                digital_signature=True,
                key_encipherment=True,
                key_agreement=False,
                key_cert_sign=False,
                crl_sign=False,
                content_commitment=True,
                data_encipherment=False,
                encipher_only=False,
                decipher_only=False
            )
            extended_key_usage = x509.ExtendedKeyUsage([
                ExtendedKeyUsageOID.CLIENT_AUTH
            ])
        else:  # END_ENTITY genérico
            key_usage = x509.KeyUsage(
                digital_signature=True,
                key_encipherment=True,
                key_agreement=False,
                key_cert_sign=False,
                crl_sign=False,
                content_commitment=False,
                data_encipherment=False,
                encipher_only=False,
                decipher_only=False
            )
            extended_key_usage = x509.ExtendedKeyUsage([
                ExtendedKeyUsageOID.CLIENT_AUTH,
                ExtendedKeyUsageOID.SERVER_AUTH
            ])
        
        builder = builder.add_extension(key_usage, critical=True)
        builder = builder.add_extension(extended_key_usage, critical=True)
        
        # Subject Alternative Names (SAN) para certificados de servidor
        if dns_names or ip_addresses:
            san_list = []
            if dns_names:
                for dns_name in dns_names:
                    san_list.append(x509.DNSName(dns_name))
            if ip_addresses:
                for ip_addr in ip_addresses:
                    san_list.append(x509.IPAddress(ipaddress.ip_address(ip_addr)))
            
            builder = builder.add_extension(
                x509.SubjectAlternativeName(san_list),
                critical=False
            )
        
        # Identificadores de clave
        builder = builder.add_extension(
            x509.SubjectKeyIdentifier.from_public_key(private_key.public_key()),
            critical=False
        )
        builder = builder.add_extension(
            x509.AuthorityKeyIdentifier.from_issuer_public_key(ca_cert.public_key()),
            critical=False
        )
        
        # Firmar certificado
        certificate = builder.sign(ca_key, hashes.SHA256())
        
        # Almacenar
        cert_id = str(certificate.serial_number)
        self.certificates[cert_id] = {
            'certificate': certificate,
            'type': certificate_type,
            'created_at': datetime.now(),
            'issuer_id': ca_id,
            'status': 'active'
        }
        self.private_keys[cert_id] = private_key
        
        return cert_id, certificate, private_key
    
    def revoke_certificate(self, cert_id, reason="unspecified"):
        """Revocar certificado"""
        if cert_id not in self.certificates:
            raise ValueError("Certificate not found")
        
        revocation_info = {
            'certificate_id': cert_id,
            'serial_number': self.certificates[cert_id]['certificate'].serial_number,
            'revoked_at': datetime.now(),
            'reason': reason
        }
        
        self.revoked_certificates.append(revocation_info)
        self.certificates[cert_id]['status'] = 'revoked'
        
        return revocation_info
    
    def generate_crl(self, ca_id):
        """Generar Certificate Revocation List (CRL)"""
        if ca_id not in self.certificates:
            raise ValueError("CA certificate not found")
        
        ca_cert = self.certificates[ca_id]['certificate']
        ca_key = self.private_keys[ca_id]
        
        # Filtrar certificados revocados emitidos por esta CA
        ca_revoked_certs = [
            cert for cert in self.revoked_certificates
            if self.certificates[cert['certificate_id']]['issuer_id'] == ca_id
        ]
        
        # Crear lista de certificados revocados
        revoked_certs = []
        for revoked in ca_revoked_certs:
            revoked_cert_builder = x509.RevokedCertificateBuilder()
            revoked_cert_builder = revoked_cert_builder.serial_number(revoked['serial_number'])
            revoked_cert_builder = revoked_cert_builder.revocation_date(revoked['revoked_at'])
            
            # Añadir razón de revocación
            reason_code = x509.ReasonFlags.unspecified
            if revoked['reason'] == 'key_compromise':
                reason_code = x509.ReasonFlags.key_compromise
            elif revoked['reason'] == 'ca_compromise':
                reason_code = x509.ReasonFlags.ca_compromise
            elif revoked['reason'] == 'superseded':
                reason_code = x509.ReasonFlags.superseded
            
            revoked_cert_builder = revoked_cert_builder.add_extension(
                x509.CRLReason(reason_code),
                critical=False
            )
            
            revoked_certs.append(revoked_cert_builder.build())
        
        # Construir CRL
        crl_builder = x509.CertificateRevocationListBuilder()
        crl_builder = crl_builder.issuer_name(ca_cert.subject)
        crl_builder = crl_builder.last_update(datetime.utcnow())
        crl_builder = crl_builder.next_update(datetime.utcnow() + timedelta(days=7))
        
        for revoked_cert in revoked_certs:
            crl_builder = crl_builder.add_revoked_certificate(revoked_cert)
        
        # Añadir número de CRL
        crl_builder = crl_builder.add_extension(
            x509.CRLNumber(len(self.revoked_certificates)),
            critical=False
        )
        
        # Firmar CRL
        crl = crl_builder.sign(ca_key, hashes.SHA256())
        
        return crl
    
    def verify_certificate_chain(self, cert_id, trusted_ca_ids=None):
        """Verificar cadena de certificados"""
        if cert_id not in self.certificates:
            return {'valid': False, 'reason': 'Certificate not found'}
        
        cert_info = self.certificates[cert_id]
        certificate = cert_info['certificate']
        
        # Verificar estado de revocación
        if cert_info['status'] == 'revoked':
            return {'valid': False, 'reason': 'Certificate revoked'}
        
        # Verificar validez temporal
        now = datetime.utcnow()
        if now < certificate.not_valid_before:
            return {'valid': False, 'reason': 'Certificate not yet valid'}
        if now > certificate.not_valid_after:
            return {'valid': False, 'reason': 'Certificate expired'}
        
        # Construir cadena
        chain = [cert_id]
        current_id = cert_id
        
        while True:
            current_cert_info = self.certificates[current_id]
            issuer_id = current_cert_info['issuer_id']
            
            # Si es auto-firmado (root CA)
            if issuer_id == current_id:
                break
            
            if issuer_id not in self.certificates:
                return {'valid': False, 'reason': 'Issuer certificate not found'}
            
            chain.append(issuer_id)
            current_id = issuer_id
            
            # Evitar bucles infinitos
            if len(chain) > 10:
                return {'valid': False, 'reason': 'Chain too long'}
        
        # Verificar firmas en la cadena
        for i in range(len(chain) - 1):
            cert_to_verify = self.certificates[chain[i]]['certificate']
            issuer_cert = self.certificates[chain[i + 1]]['certificate']
            
            try:
                # Verificar que el certificado fue firmado por el emisor
                issuer_cert.public_key().verify(
                    cert_to_verify.signature,
                    cert_to_verify.tbs_certificate_bytes,
                    padding.PKCS1v15(),
                    cert_to_verify.signature_hash_algorithm,
                )
            except:
                return {'valid': False, 'reason': f'Invalid signature in chain at position {i}'}
        
        return {
            'valid': True,
            'chain': chain,
            'chain_length': len(chain),
            'root_ca': chain[-1]
        }
    
    def get_certificate_info(self, cert_id):
        """Obtener información detallada del certificado"""
        if cert_id not in self.certificates:
            return None
        
        cert_info = self.certificates[cert_id]
        certificate = cert_info['certificate']
        
        # Extraer información básica
        subject_info = {}
        for attribute in certificate.subject:
            subject_info[attribute.oid._name] = attribute.value
        
        issuer_info = {}
        for attribute in certificate.issuer:
            issuer_info[attribute.oid._name] = attribute.value
        
        # Extraer extensiones
        extensions = {}
        for ext in certificate.extensions:
            extensions[ext.oid._name] = {
                'critical': ext.critical,
                'value': str(ext.value)
            }
        
        return {
            'certificate_id': cert_id,
            'serial_number': str(certificate.serial_number),
            'subject': subject_info,
            'issuer': issuer_info,
            'valid_from': certificate.not_valid_before.isoformat(),
            'valid_until': certificate.not_valid_after.isoformat(),
            'signature_algorithm': certificate.signature_hash_algorithm.name,
            'public_key_algorithm': certificate.public_key().__class__.__name__,
            'extensions': extensions,
            'type': cert_info['type'].value,
            'status': cert_info['status'],
            'created_at': cert_info['created_at'].isoformat()
        }
    
    def export_certificate_pem(self, cert_id):
        """Exportar certificado en formato PEM"""
        if cert_id not in self.certificates:
            return None
        
        certificate = self.certificates[cert_id]['certificate']
        pem_data = certificate.public_bytes(serialization.Encoding.PEM)
        
        return pem_data.decode('utf-8')
    
    def generate_pki_report(self):
        """Generar reporte completo de PKI"""
        total_certs = len(self.certificates)
        active_certs = len([c for c in self.certificates.values() if c['status'] == 'active'])
        revoked_certs = len(self.revoked_certificates)
        
        cert_types = {}
        for cert_info in self.certificates.values():
            cert_type = cert_info['type'].value
            cert_types[cert_type] = cert_types.get(cert_type, 0) + 1
        
        return {
            'summary': {
                'total_certificates': total_certs,
                'active_certificates': active_certs,
                'revoked_certificates': revoked_certs,
                'certificate_types': cert_types
            },
            'certificates': [
                {
                    'id': cert_id,
                    'serial': str(info['certificate'].serial_number),
                    'subject': info['certificate'].subject.rfc4514_string(),
                    'type': info['type'].value,
                    'status': info['status'],
                    'expires': info['certificate'].not_valid_after.isoformat()
                }
                for cert_id, info in self.certificates.items()
            ],
            'revoked_list': self.revoked_certificates,
            'report_generated': datetime.now().isoformat()
        }

# Ejemplo de uso PKI completo
print("=== Infraestructura de Clave Pública (PKI) ===")

# Inicializar PKI
pki = PKIManager()

# 1. Crear Root CA
print("1. Creando Root CA...")
root_ca_id, root_cert, root_key = pki.create_root_ca_certificate(
    common_name="Mi Root CA",
    organization="Empresa Segura S.A.",
    validity_years=20
)
print(f"Root CA creado: {root_ca_id}")

# 2. Crear CA Intermedia
print("\n2. Creando Intermediate CA...")
intermediate_ca_id, intermediate_cert, intermediate_key = pki.create_intermediate_ca_certificate(
    root_ca_id=root_ca_id,
    common_name="Mi Intermediate CA",
    organization="Empresa Segura S.A.",
    validity_years=10
)
print(f"Intermediate CA creado: {intermediate_ca_id}")

# 3. Crear certificado de servidor
print("\n3. Creando certificado de servidor...")
server_cert_id, server_cert, server_key = pki.create_end_entity_certificate(
    ca_id=intermediate_ca_id,
    common_name="www.miempresa.com",
    certificate_type=CertificateType.SERVER,
    organization="Empresa Segura S.A.",
    dns_names=["www.miempresa.com", "miempresa.com", "api.miempresa.com"],
    ip_addresses=["192.168.1.100"],
    validity_days=365
)
print(f"Server certificate creado: {server_cert_id}")

# 4. Crear certificado de cliente
print("\n4. Creando certificado de cliente...")
client_cert_id, client_cert, client_key = pki.create_end_entity_certificate(
    ca_id=intermediate_ca_id,
    common_name="Juan Perez",
    certificate_type=CertificateType.CLIENT,
    organization="Empresa Segura S.A.",
    email="juan.perez@miempresa.com",
    validity_days=365
)
print(f"Client certificate creado: {client_cert_id}")

# 5. Verificar cadenas de certificados
print("\n5. Verificando cadenas de certificados...")
server_verification = pki.verify_certificate_chain(server_cert_id)
client_verification = pki.verify_certificate_chain(client_cert_id)

print(f"Server certificate chain: {server_verification}")
print(f"Client certificate chain: {client_verification}")

# 6. Mostrar información detallada
print("\n6. Información del certificado de servidor:")
server_info = pki.get_certificate_info(server_cert_id)
print(f"Subject: {server_info['subject']}")
print(f"Valid from: {server_info['valid_from']}")
print(f"Valid until: {server_info['valid_until']}")
print(f"Signature algorithm: {server_info['signature_algorithm']}")

# 7. Revocar un certificado
print("\n7. Revocando certificado de cliente...")
revocation = pki.revoke_certificate(client_cert_id, "key_compromise")
print(f"Certificate revoked: {revocation}")

# 8. Generar CRL
print("\n8. Generando Certificate Revocation List...")
crl = pki.generate_crl(intermediate_ca_id)
print(f"CRL generated with {len(crl)} revoked certificates")

# 9. Verificar certificado revocado
print("\n9. Verificando certificado revocado...")
revoked_verification = pki.verify_certificate_chain(client_cert_id)
print(f"Revoked certificate verification: {revoked_verification}")

# 10. Exportar certificados
print("\n10. Exportando certificados...")
server_pem = pki.export_certificate_pem(server_cert_id)
print(f"Server certificate PEM:\n{server_pem[:200]}...")

# 11. Reporte completo de PKI
print("\n11. Reporte PKI:")
pki_report = pki.generate_pki_report()
print(json.dumps(pki_report['summary'], indent=2))
```

### Casos de Uso y Aplicaciones

#### Implementación de SSL/TLS Server
```python
import socket
import ssl

class SecureServerExample:
    def __init__(self, pki_manager, server_cert_id):
        self.pki = pki_manager
        self.server_cert_id = server_cert_id
    
    def create_ssl_context(self):
        """Crear contexto SSL con certificados PKI"""
        # En implementación real, se cargarían desde archivos
        context = ssl.create_default_context(ssl.Purpose.CLIENT_AUTH)
        
        # Configurar certificado y clave privada
        # context.load_cert_chain(certfile, keyfile)
        
        # Configurar verificación de cliente (opcional)
        context.verify_mode = ssl.CERT_OPTIONAL
        # context.load_verify_locations(cafile)
        
        return context
    
    def demonstrate_handshake(self):
        """Simular handshake SSL/TLS"""
        print("SSL/TLS Handshake Process:")
        print("1. Client Hello - Client sends supported cipher suites")
        print("2. Server Hello - Server selects cipher suite")
        print("3. Server Certificate - Server sends certificate chain")
        print("4. Server Key Exchange (if needed)")
        print("5. Certificate Request (if client auth required)")
        print("6. Server Hello Done")
        print("7. Client Certificate (if requested)")
        print("8. Client Key Exchange")
        print("9. Certificate Verify (if client cert sent)")
        print("10. Change Cipher Spec (both sides)")
        print("11. Finished messages (both sides)")
        print("12. Application data transfer begins")

# Ejemplo de aplicación empresarial
class EnterpriseCASystem:
    def __init__(self):
        self.pki = PKIManager()
        self.employee_certificates = {}
        self.device_certificates = {}
        
    def setup_enterprise_pki(self):
        """Configurar PKI empresarial completa"""
        # Root CA corporativo
        root_id, _, _ = self.pki.create_root_ca_certificate(
            common_name="Corporate Root CA",
            organization="Mi Empresa Corp",
            validity_years=30
        )
        
        # CA para empleados
        employee_ca_id, _, _ = self.pki.create_intermediate_ca_certificate(
            root_ca_id=root_id,
            common_name="Employee Certificate Authority",
            organization="Mi Empresa Corp - HR Department"
        )
        
        # CA para dispositivos
        device_ca_id, _, _ = self.pki.create_intermediate_ca_certificate(
            root_ca_id=root_id,
            common_name="Device Certificate Authority",  
            organization="Mi Empresa Corp - IT Department"
        )
        
        # CA para servidores
        server_ca_id, _, _ = self.pki.create_intermediate_ca_certificate(
            root_ca_id=root_id,
            common_name="Server Certificate Authority",
            organization="Mi Empresa Corp - Infrastructure"
        )
        
        return {
            'root_ca': root_id,
            'employee_ca': employee_ca_id,
            'device_ca': device_ca_id,
            'server_ca': server_ca_id
        }
    
    def issue_employee_certificate(self, ca_id, employee_name, employee_email, department):
        """Emitir certificado para empleado"""
        cert_id, cert, key = self.pki.create_end_entity_certificate(
            ca_id=ca_id,
            common_name=employee_name,
            certificate_type=CertificateType.CLIENT,
            organization=f"Mi Empresa Corp - {department}",
            email=employee_email,
            validity_days=365
        )
        
        self.employee_certificates[employee_email] = {
            'certificate_id': cert_id,
            'employee_name': employee_name,
            'department': department,
            'issued_date': datetime.now()
        }
        
        return cert_id
    
    def issue_device_certificate(self, ca_id, device_name, device_type, location):
        """Emitir certificado para dispositivo"""
        cert_id, cert, key = self.pki.create_end_entity_certificate(
            ca_id=ca_id,
            common_name=device_name,
            certificate_type=CertificateType.END_ENTITY,
            organization=f"Mi Empresa Corp - {device_type}",
            validity_days=730  # 2 años para dispositivos
        )
        
        self.device_certificates[device_name] = {
            'certificate_id': cert_id,
            'device_type': device_type,
            'location': location,
            'issued_date': datetime.now()
        }
        
        return cert_id
    
    def generate_enterprise_report(self):
        """Generar reporte empresarial"""
        pki_report = self.pki.generate_pki_report()
        
        enterprise_report = {
            'pki_summary': pki_report['summary'],
            'employee_certificates': len(self.employee_certificates),
            'device_certificates': len(self.device_certificates),
            'employees': list(self.employee_certificates.keys()),
            'devices': list(self.device_certificates.keys()),
            'report_date': datetime.now().isoformat()
        }
        
        return enterprise_report

# Demostración de sistema empresarial
print("\n=== Sistema PKI Empresarial ===")

enterprise = EnterpriseCASystem()
ca_structure = enterprise.setup_enterprise_pki()

print("Estructura de CA creada:")
for ca_type, ca_id in ca_structure.items():
    print(f"  {ca_type}: {ca_id}")

# Emitir certificados para empleados
employees = [
    ("Alice Johnson", "alice@empresa.com", "IT"),
    ("Bob Smith", "bob@empresa.com", "Finance"),
    ("Carol Williams", "carol@empresa.com", "HR")
]

print("\nEmitiendo certificados de empleados:")
for name, email, dept in employees:
    cert_id = enterprise.issue_employee_certificate(
        ca_structure['employee_ca'], name, email, dept
    )
    print(f"  {name}: {cert_id}")

# Emitir certificados para dispositivos
devices = [
    ("PRINTER-01", "Network Printer", "Floor 1"),
    ("SERVER-WEB-01", "Web Server", "Data Center"),
    ("IOT-SENSOR-001", "Temperature Sensor", "Warehouse A")
]

print("\nEmitiendo certificados de dispositivos:")
for device_name, device_type, location in devices:
    cert_id = enterprise.issue_device_certificate(
        ca_structure['device_ca'], device_name, device_type, location
    )
    print(f"  {device_name}: {cert_id}")

# Generar reporte empresarial
enterprise_report = enterprise.generate_enterprise_report()
print(f"\nReporte Empresarial:")
print(f"Total de certificados: {enterprise_report['pki_summary']['total_certificates']}")
print(f"Certificados de empleados: {enterprise_report['employee_certificates']}")
print(f"Certificados de dispositivos: {enterprise_report['device_certificates']}")

print("\n=== Cifrado de Información - Tema Completo ===")
print("✓ Conceptos fundamentales de criptografía")
print("✓ Cifrado simétrico (AES, ChaCha20, modos de operación)")
print("✓ Cifrado asimétrico (RSA, ECC)")
print("✓ Funciones hash criptográficas")
print("✓ Firma digital y autenticación")
print("✓ Infraestructura de Clave Pública (PKI)")
print("✓ Aplicaciones empresariales y casos de uso")
```

---

## Conclusión

El **cifrado de información** es un pilar fundamental de la seguridad informática moderna. Hemos explorado:

### Puntos Clave
- **Criptografía simétrica**: Rápida y eficiente para grandes volúmenes de datos
- **Criptografía asimétrica**: Esencial para intercambio seguro de claves y autenticación
- **Funciones hash**: Fundamentales para integridad y autenticación
- **Firma digital**: Proporciona autenticación, integridad y no repudio
- **PKI**: Infraestructura crítica para gestión de certificados a gran escala

### Mejores Prácticas
1. Usar bibliotecas criptográficas probadas y actualizadas
2. Implementar múltiples capas de seguridad
3. Gestionar claves de forma segura
4. Mantener certificados actualizados
5. Auditar y monitorear sistemas criptográficos regularmente

La criptografía moderna permite construir sistemas seguros y confiables, fundamentales para la protección de datos en el mundo digital actual.
- Malware que usa cifrado (ransomware)
- Protección contra malware de cifrado

### Implementación Práctica
- Herramientas de cifrado (GPG, OpenSSL)
- Cifrado en aplicaciones web
- Cifrado en bases de datos
- Cifrado en comunicaciones

## Objetivos de Aprendizaje
- [ ] Implementar políticas de contraseñas efectivas
- [ ] Configurar sistemas de auditoría
- [ ] Comprender algoritmos de cifrado
- [ ] Implementar cifrado simétrico y asimétrico
- [ ] Gestionar infraestructuras PKI

## Recursos Adicionales
- Herramientas de cifrado open source
- Estándares criptográficos
- Guías de implementación

## Actividades
- Configuración de políticas de contraseñas
- Implementación de cifrado de archivos
- Creación de certificados digitales
- Análisis de malware criptográfico
