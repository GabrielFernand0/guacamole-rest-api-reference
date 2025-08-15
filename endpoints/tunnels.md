# Túneis

O Apache Guacamole permite gerenciar túneis para conexões, facilitando o acesso remoto seguro.

---

## Listar Túneis

**Endpoint:**  
```
GET /api/session/data/{dataSource}/tunnels
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/tunnels?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/tunnels"
params = {"token": "SEU_TOKEN"}

response = requests.get(url, params=params)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
[
  {
    "identifier": "tunnel1",
    "protocol": "rdp",
    "parameters": {
      "hostname": "192.168.1.100",
      "port": 3389
    }
  },
  {
    "identifier": "tunnel2",
    "protocol": "vnc",
    "parameters": {
      "hostname": "192.168.1.101",
      "port": 5900
    }
  }
]
```

---

## Criar um Novo Túnel

**Endpoint:**  
```
POST /api/session/data/{dataSource}/tunnels
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| token      | string | ✅           | Token de autenticação              |

**Corpo da Requisição:**
```json
{
  "identifier": "tunnel3",
  "protocol": "rdp",
  "parameters": {
    "hostname": "192.168.1.102",
    "port": 3389
  }
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/tunnels" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "identifier": "tunnel3",
    "protocol": "rdp",
    "parameters": {
      "hostname": "192.168.1.102",
      "port": 3389
    }
  }'
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/tunnels"
headers = {"Guacamole-Token": "SEU_TOKEN"}
data = {
  "identifier": "tunnel3",
  "protocol": "rdp",
  "parameters": {
    "hostname": "192.168.1.102",
    "port": 3389
  }
}

response = requests.post(url, headers=headers, json=data)
print(response.json())
```

**Resposta esperada (201 Created):**
```json
{
  "status": "success",
  "identifier": "tunnel3"
}
```

---

## Excluir um Túnel

**Endpoint:**  
```
DELETE /api/session/data/{dataSource}/tunnels/{tunnelId}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| tunnelId   | string | ✅           | ID do túnel a ser excluído         |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/tunnels/tunnel3?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/tunnels/tunnel3"
params = {"token": "SEU_TOKEN"}

response = requests.delete(url, params=params)
print(response.json())
```

**Resposta esperada (204 No Content):**
```json
{}
