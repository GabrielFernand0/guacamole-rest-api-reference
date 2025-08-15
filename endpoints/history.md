# Histórico de Conexões

O endpoint `/history` permite acessar informações sobre as conexões realizadas, incluindo dados como o usuário que iniciou a conexão, o tempo de duração e o status da conexão.

---

## Listar Histórico de Conexões

**Endpoint:**  
```
GET /api/session/data/{dataSource}/history
```

**Parâmetros:**

| Campo       | Tipo   | Obrigatório | Descrição                          |
|-------------|--------|-------------|------------------------------------|
| dataSource  | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| token       | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/history?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/history"
params = {"token": "SEU_TOKEN"}

response = requests.get(url, params=params)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
[
  {
    "start": "2025-08-15T14:30:00Z",
    "duration": 120,
    "username": "usuario1",
    "connection": "Conexao A",
    "status": "sucesso"
  },
  {
    "start": "2025-08-15T15:00:00Z",
    "duration": 90,
    "username": "usuario2",
    "connection": "Conexao B",
    "status": "falha"
  }
]
```

---

## Detalhes de uma Conexão

**Endpoint:**  
```
GET /api/session/data/{dataSource}/history/{historyId}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| historyId  | string | ✅           | ID do histórico da conexão         |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/history/12345?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/history/12345"
params = {"token": "SEU_TOKEN"}

response = requests.get(url, params=params)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
{
  "start": "2025-08-15T14:30:00Z",
  "duration": 120,
  "username": "usuario1",
  "connection": "Conexao A",
  "status": "sucesso",
  "details": {
    "ip": "192.168.1.100",
    "protocol": "RDP",
    "client": "Windows 10"
  }
}
```

---

## Códigos de Resposta Comuns

| Código | Significado             |
|--------|-----------------------|
| 200    | Requisição bem-sucedida|
| 400    | Requisição inválida    |
| 401    | Não autorizado         |
| 404    | Não encontrado         |
