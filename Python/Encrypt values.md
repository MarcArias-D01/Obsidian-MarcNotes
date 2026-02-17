---
tags:
  - python
  - encrypt
---
Para encriptar valores:
```python 
def xor_bytes(data: bytes, key: bytes) -> bytes:
    return bytes(b ^ key[i % len(key)] for i, b in enumerate(data))

  
secret = b"VALOR_PARA_ENCRIPTAR"

key = b"PALABRA_VALOR_MAGICO"

obfuscated = xor_bytes(secret, key)

print(obfuscated.hex())
```

Para desencriptar los valores:
```python
import os

def xor_bytes(data: bytes, key: bytes) -> bytes:
    return bytes(b ^ key[i % len(key)] for i, b in enumerate(data))

  

def get_client_secret():
    obf = bytes.fromhex("VALOR_ENCRIPTADO")
    key = "PALABRA_VALOR_MAGICO".encode()
    return xor_bytes(obf, key).decode("utf-8")

  
get_client_secret()
```