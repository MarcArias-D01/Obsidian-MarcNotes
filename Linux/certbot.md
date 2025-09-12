#linux/command/cerbot #linux/software/certbot #SSL 

Certbot es una herramienta de **Let's Encrypt** que automatiza la obtención y renovación de certificados SSL/TLS gratuitos.  
Se integra fácilmente con servidores web como **Nginx o Apache** para habilitar HTTPS.  
Su objetivo es simplificar la gestión de certificados y mejorar la seguridad en sitios web. ✅

En el caso de Driving01 se utiliza el certbot para AWS `route53` #linux/software/certbot/install  

```bash
sudo apt install python3-certbot-dns-route53 -y

sudo apt install certbot python3-certbot-nginx -y   # si usas Nginx
sudo apt install certbot python3-certbot-apache -y  # si usas Apache
```

Una vez instalado, Certbot se encarga de:
- Pedir certificados a Let’s Encrypt
- Guardarlos en `/etc/letsencrypt/`
- Renovarlos automáticamente con `certbot renew`

**ES IMPORTATNE SI SE HACE DESDE AWS TENER AWS INSTALADO EN EL SERVIDOR Y CONFIGURADO CON UN USUARIO QUE PUEDA ACCEDER A ROUTE53** [[aws]]

En Driving01 utilizamos el siguiente comando si hemos de crear el certificado por primera vez:

```bash
certbot certonly --dns-route53 -d <your_doman> --non-interactive --agree-tos
```

Una vez creado el certificado podemos renovarlos fácilmente con el siguiente script:
```bash
#!/bin/bash

CERT_NAMES=(
    "your_domain"
    "your_domain"
    "your_domain"
)

DAYS_RENEW=30

echo "Stopping Nginx"
systemctl stop nginx

# Recorre cada certificado
for CERT_NAME in "${CERT_NAMES[@]}"; do
    CERT_PATH="/etc/letsencrypt/live/$CERT_NAME/fullchain.pem"
    if [ -f "$CERT_PATH" ]; then
        EXPIRATION_DATE=$(sudo openssl x509 -enddate -noout -in "$CERT_PATH" | awk -F'=' '{print $2}')
        EXPIRATION_TIMESTAMP=$(date -d "$EXPIRATION_DATE" +%s 2>/dev/null)
        if [ -z "$EXPIRATION_TIMESTAMP" ]; then
            echo "❌ ERROR: Cannot get expiration date from $CERT_PATH"
            continue
        fi

        CURRENT_TIMESTAMP=$(date +%s)
        DAYS_LEFT=$(( (EXPIRATION_TIMESTAMP - CURRENT_TIMESTAMP) / 86400 ))
        if [ "$DAYS_LEFT" -le "$DAYS_RENEW" ]; then
            echo "⚠️ Renewing cert $CERT_PATH as it expires in $DAYS_LEFT days."
            sudo certbot certonly --dns-route53 -d $CERT_NAME --non-interactive --agree-tos
        else
            echo "Cert $CERT_PATH expires in $DAYS_LEFT days. Not renewing atm"
        fi

    else
        echo "❌ ERROR: Cannot find $CERT_PATH"
        logger -t CertCheck "❌ ERROR: No se encontró el certificado en $CERT_PATH"
    fi

done

echo "Starting Nginx..."

systemctl start nginx
```

---

# IMPORTANTE
Nunca publiques ni subas tus **Access Key** y **Secret Key**. Si es para usar con **certbot + Route53**, lo más seguro es crear un usuario IAM con permisos limitados solo a `route53:ChangeResourceRecordSets` y `route53:ListHostedZones`.