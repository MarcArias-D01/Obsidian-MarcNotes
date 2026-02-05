---
tags:
  - python
  - mail
---

Función para enviar mail des de outlook cuenta empresa.
Primero tendrás que crear una aplicación y darle al GRAPH permisos de aplicación de mail.send. 
Importante, crear un secret en la aplicación.

```python
def send_mail_outlook(
    sender: str,
    receptor: str,
    subject: str,
    body: str,
) -> bool:
    """
    Envía un email vía SMTP de Outlook/Office365.
  
    Args:
        sender: Tu email @outlook.com o @office365
        app_key: Contraseña de aplicación (no la normal)
        receptor: Email del receptor
        subject: Título del email
        body: Contenido del mensaje
        copy: Lista opcional de copias

    Returns:
        True si se envió correctamente
    """
    def __xor_bytes(data: bytes, key: bytes) -> bytes:
        return bytes(b ^ key[i % len(key)] for i, b in enumerate(data))

    def __get_secret(env_name: str):
        obf = bytes.fromhex(os.getenv(env_name))
        key = os.getenv("KEY").encode()
        return __xor_bytes(obf, key).decode("utf-8")

    tenant_id = __get_secret("AZURE_TENANT_ID")
    client_id = __get_secret("AZURE_CLIENT_ID")
    client_secret = __get_secret("AZURE_CLIENT_SECRET")
  
    # 1) Get token
    token_url = f"https://login.microsoftonline.com/{tenant_id}/oauth2/v2.0/token"

    data = {
        "client_id": client_id,
        "client_secret": client_secret,
        "scope": "https://graph.microsoft.com/.default",
        "grant_type": "client_credentials",
    }

    token_res = requests.post(token_url, data=data)
    token_res.raise_for_status()
    access_token = token_res.json()["access_token"]

    # 2) Build email payload
    endpoint = f"https://graph.microsoft.com/v1.0/users/{sender}/sendMail"

    email_msg = {
        "message": {
            "subject": f"{subject}",
            "body": {
                "contentType": "Text",
                "content": f"{body}",
            },
            "toRecipients": [{"emailAddress": {"address": receptor}}],
        },
        "saveToSentItems": "true",
    }

    # 3) Send mail
    r = requests.post(
        endpoint,
        headers={"Authorization": f"Bearer {access_token}"},
        json=email_msg,
    ) 

    return r
```