#python/json/text

Recomendado para guardar / compartir datos
```python
diccionario = {'test':'doc1' , 'test_test':'esto es un ejemplo'}

texto_json = json.dumps(diccionario, ensure_ascii=False, indent=4)
```

#python/json/create 

```python
import json

diccionario = {'test':'doc1' , 'test_test':'esto es un ejemplo'}

diccionario = dict(test = 'doc1', test_test = 'esto es un ejemplo')
```

#python/json/open

```python
import json

with open("mi_diccionario.json", "r", encoding="utf-8") as f:
    d = json.load(f)
```

#python/json/edit 

```python 
import json

persona = {
    "nombre": "Ana",
    "edad": 30,
    "ciudad": "Madrid"
}

# Editar 1 valor
if 'edad' in persona:
	persona["edad"] = 31

# Agregar una clave
persona["profesion"] = "Ingeniera"

del persona["ciudad"]   # borra la clave "ciudad"

valor = persona.pop("profesion")  # elimina y devuelve el valor

# Update de varios valores a la vez
persona.update({"nombre": "Ana María", "edad": 32})

# editar por condiciones
for clave, valor in persona.items():
    if clave == "edad":
        persona[k] = v + 1 

```

#python/json/save 

```python
import json

with open("mi_diccionario.json", "w", encoding="utf-8") as f:
    json.dump(diccionario, f, ensure_ascii=False, indent=4)
    
```