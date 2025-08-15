# Grupos de Usuários

O Apache Guacamole permite gerenciar grupos de usuários, facilitando a organização e atribuição de permissões de acesso.

## Listar Grupos de Usuários

**Endpoint:**  
```
GET /api/session/data/{dataSource}/userGroups
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups"
params = {"token": "SEU_TOKEN"}

response = requests.get(url, params=params)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
[
  {
    "identifier": "group1",
    "name": "Grupo 1",
    "description": "Descrição do Grupo 1"
  },
  {
    "identifier": "group2",
    "name": "Grupo 2",
    "description": "Descrição do Grupo 2"
  }
]
```

---

## Criar um Novo Grupo de Usuários

**Endpoint:**  
```
POST /api/session/data/{dataSource}/userGroups
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| token      | string | ✅           | Token de autenticação              |

**Corpo da Requisição:**
```json
{
  "identifier": "group3",
  "name": "Grupo 3",
  "description": "Descrição do Grupo 3"
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "identifier": "group3",
    "name": "Grupo 3",
    "description": "Descrição do Grupo 3"
  }'
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups"
headers = {"Guacamole-Token": "SEU_TOKEN"}
data = {
  "identifier": "group3",
  "name": "Grupo 3",
  "description": "Descrição do Grupo 3"
}

response = requests.post(url, headers=headers, json=data)
print(response.json())
```

**Resposta esperada (201 Created):**
```json
{
  "status": "success",
  "identifier": "group3"
}
```

---

## Detalhes de um Grupo de Usuários

**Endpoint:**  
```
GET /api/session/data/{dataSource}/userGroups/{groupId}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| groupId    | string | ✅           | ID do grupo de usuários            |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3"
params = {"token": "SEU_TOKEN"}

response = requests.get(url, params=params)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
{
  "identifier": "group3",
  "name": "Grupo 3",
  "description": "Descrição do Grupo 3"
}
```

---

## Adicionar Membros a um Grupo de Usuários

**Endpoint:**  
```
POST /api/session/data/{dataSource}/userGroups/{groupId}/members
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| groupId    | string | ✅           | ID do grupo de usuários            |
| token      | string | ✅           | Token de autenticação              |

**Corpo da Requisição:**
```json
{
  "members": ["user1", "user2"]
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3/members" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "members": ["user1", "user2"]
  }'
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3/members"
headers = {"Guacamole-Token": "SEU_TOKEN"}
data = {
  "members": ["user1", "user2"]
}

response = requests.post(url, headers=headers, json=data)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
{
  "status": "success"
}
```

---

## Remover Membros de um Grupo de Usuários

**Endpoint:**  
```
DELETE /api/session/data/{dataSource}/userGroups/{groupId}/members
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| groupId    | string | ✅           | ID do grupo de usuários            |
| token      | string | ✅           | Token de autenticação              |

**Corpo da Requisição:**
```json
{
  "members": ["user1", "user2"]
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3/members" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "members": ["user1", "user2"]
  }'
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3/members"
headers = {"Guacamole-Token": "SEU_TOKEN"}
data = {
  "members": ["user1", "user2"]
}

response = requests.delete(url, headers=headers, json=data)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
{
  "status": "success"
}
```

---

## Excluir um Grupo de Usuários

**Endpoint:**  
```
DELETE /api/session/data/{dataSource}/userGroups/{groupId}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                          |
|------------|--------|-------------|------------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| groupId    | string | ✅           | ID do grupo de usuários            |
| token      | string | ✅           | Token de autenticação              |

**Exemplo de requisição (cURL):**
```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3?token=SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/userGroups/group3"
params = {"token": "SEU_TOKEN"}

response = requests.delete(url, params=params)
print(response.json())
```

**Resposta esperada (204 No Content):**
```json
{}
```
