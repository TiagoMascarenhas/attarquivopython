
## Código completo

```python
# Definir o nome do arquivo
import_file = "allow_list.txt"

# Lista de IPs a serem removidos
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# Abrir e ler o arquivo
with open(import_file, "r") as file:
    ip_addresses = file.read()

# Converter string em lista
ip_addresses = ip_addresses.split()

# Iterar pela lista de remoção e remover IPs
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)

# Converter lista de volta para string
ip_addresses = "\n".join(ip_addresses)

# Atualizar o arquivo com a nova lista
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

