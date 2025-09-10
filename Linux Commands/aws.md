#linux/command/cloud

Instalar AWS CLI
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install
```

Se tendran que configurar las credenciales para un usuario:

```bash
aws configure
```

Te pedirá:
- **AWS Access Key ID** → (lo obtienes en IAM → Usuario → Credenciales de seguridad).
- **AWS Secret Access Key** → (clave secreta asociada).
- **Default region name** → ej. `us-east-1` o `eu-west-1`.
- **Default output format** → `json`, `table` o `text` (recomiendo `json`).

Esto genera el archivo de configuración en:

```bash
~/.aws/credentials
~/.aws/config
```

*Si haces un cat , nano o vim podras ver y editar las credenciales configuradas*

---
# IMPORTANTE
Nunca publiques ni subas tus **Access Key** y **Secret Key**. Si es para usar con **certbot + Route53**, lo más seguro es crear un usuario IAM con permisos limitados solo a `route53:ChangeResourceRecordSets` y `route53:ListHostedZones`.

En el caso de Driving01 se ha creado un usuario en AWS específicamente para solo hacer el creado y renovación de certificados. Este usuario solo tiene acceso a la `route53` y es el configurado en los servidores.