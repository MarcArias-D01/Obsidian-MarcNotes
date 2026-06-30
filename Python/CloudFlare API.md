---
tags:
  - python
  - cloudflare
  - requests
date: 2026-06-30
---
# CLoudFlare API /scrape

url: https://api.cloudflare.com/client/v4/accounts/<accountId>/browser-rendering/scrape

Doc: https://developers.cloudflare.com/browser-run/quick-actions/scrape-endpoint/

Endpoint para pdoer scrapear paginas web facilemente. Actualemente tiene un suo gratuirto de 10 minutos por día.
- Lo que se tarda en hacer la request se sumo al tiempo total.
- El API_TOKEN solo necesita permisos de edición en browser run

Ejemplo de uso:

```python
import requests

token = "asdasdasdasd"
account_id = "asdasdasd"
url = f"https://api.cloudflare.com/client/v4/accounts/{account_id}/browser-rendering/scrape"

headers = {"Authorization": f"Bearer {token}", "Content-Type": "application/json"} 

payload = {
    "url": "https://www.pieces-yam.com/",
    "elements": [{"selector": "div"}, {"selector": "a"}, {"selector": "h4"}],
}

resp = requests.post(url=url, headers=headers, json=payload)
```