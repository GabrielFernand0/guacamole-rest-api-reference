# Usuários

O Apache Guacamole permite gerenciar usuários, facilitando o controle de acesso e permissões.

## Listar Usuários

**Endpoint:**  
```
GET /api/session/data/{dataSource}/users
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/users?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/users"
params = {"token": "SEU_TOKEN"}

response = requests.get(url, params=params)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
[
  {
    "username": "user1",
    "enabled": true,
    "attributes": {
      "fullname": "User One",
      "email": "user1@example.com"
    }
  },
  {
    "username": "user2",
    "enabled": false,
    "attributes": {
      "fullname": "User Two",
      "email": "user2@example.com"
    }
  }
]
```

---

## Criar um Novo Usuário

**Endpoint:**  
```
POST /api/session/data/{dataSource}/users
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| token      | string | ✅           | Token de autenticação              |

**Corpo da Requisição:**
```json
{
  "username": "user3",
  "password": "senha123",
  "enabled": true,
  "attributes": {
    "fullname": "User Three",
    "email": "user3@example.com"
  }
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/users" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "username": "user3",
    "password": "senha123",
    "enabled": true,
    "attributes": {
      "fullname": "User Three",
      "email": "user3@example.com"
    }
  }'
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/users"
headers = {"Guacamole-Token": "SEU_TOKEN"}
data = {
  "username": "user3",
  "password": "senha123",
  "enabled": True,
  "attributes": {
    "fullname": "User Three",
    "email": "user3@example.com"
  }
}

response = requests.post(url, headers=headers, json=data)
print(response.json())
```

**Resposta esperada (201 Created):**
```json
{
  "status": "success",
  "username": "user3"
}
```

---

## Detalhes de um Usuário

**Endpoint:**  
```
GET /api/session/data/{dataSource}/users/{username}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| username   | string | ✅           | Nome de usuário                    |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/users/user3?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/users/user3"
params = {"token": "SEU_TOKEN"}

response = requests.get(url, params=params)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
{
  "username": "user3",
  "enabled": true,
  "attributes": {
    "fullname": "User Three",
    "email": "user3@example.com"
  }
}
```

---

## Atualizar um Usuário

**Endpoint:**  
```
PUT /api/session/data/{dataSource}/users/{username}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| username   | string | ✅           | Nome de usuário                    |
| token      | string | ✅           | Token de autenticação              |

**Corpo da Requisição:**
```json
{
  "password": "novaSenha123",
  "enabled": false,
  "attributes": {
    "fullname": "User Three Updated",
    "email": "user3updated@example.com"
  }
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X PUT "http://SEU_GUACAMOLE/api/session/data/postgresql/users/user3" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "password": "novaSenha123",
    "enabled": false,
    "attributes": {
      "fullname": "User Three Updated",
      "email": "user3updated@example.com"
    }
  }'
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/users/user3"
headers = {"Guacamole-Token": "SEU_TOKEN"}
data = {
  "password": "novaSenha123",
  "enabled": False,
  "attributes": {
    "fullname": "User Three Updated",
    "email": "user3updated@example.com"
  }
}

response = requests.put(url, headers=headers, json=data)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
{
  "status": "success"
}
```

---

## Excluir um Usuário

**Endpoint:**  
```
DELETE /api/session/data/{dataSource}/users/{username}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| username   | string | ✅           | Nome de usuário                    |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/users/user3?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/users/user3"
params = {"token": "SEU_TOKEN"}

response = requests.delete(url, params=params)
print(response.json())
```

**Resposta esperada (204 No Content):**
```json
{}
```
