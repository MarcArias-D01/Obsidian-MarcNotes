---
tags:
  - linux
  - linux/ubuntu
  - linux/arch
  - linux/disk-usage
---

# `du` = *disk usage*

Útil para saber el espacio en tu linux

```bash
sudo du -ah --max-depth=1 . | sort -rh | head -n 20  
```