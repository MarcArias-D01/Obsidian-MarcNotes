---
tags:
  - python
  - requests
  - ip
---
Para obtener fácilmente tu ip.

```python
import requests

response = requests.get('https://api.ipify.org/')

return response.text # 79.152.102.101
```
