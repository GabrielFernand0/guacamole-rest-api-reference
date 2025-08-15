# Permissões

O Apache Guacamole permite atribuir e revogar permissões de acesso a conexões e grupos de conexões para usuários e grupos.

---

## Atribuir Permissões de Sistema a um Usuário

**Endpoint:**  
```
POST /api/session/data/{dataSource}/users/{username}/permissions
```

**Parâmetros:**

| Campo       | Tipo   | Obrigatório | Descrição                          |
|-------------|--------|-------------|------------------------------------|
| dataSource  | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| username    | string | ✅           | Nome de usuário                    |

**Corpo da Requisição:**
```json
{
  "permissions": [
    {
      "type": "SYSTEM",
      "permission": "READ"
    }
  ]
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/users/usuario1/permissions" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "permissions": [
      {
        "type": "SYSTEM",
        "permission": "READ"
      }
    ]
  }'
```

**Resposta esperada (200 OK):**
```json
{
  "status": "success"
}
```

---

## Revogar Permissões de Sistema de um Usuário

**Endpoint:**  
```
DELETE /api/session/data/{dataSource}/users/{username}/permissions
```

**Parâmetros:**

| Campo       | Tipo   | Obrigatório | Descrição                          |
|-------------|--------|-------------|------------------------------------|
| dataSource  | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| username    | string | ✅           | Nome de usuário                    |

**Corpo da Requisição:**
```json
{
  "permissions": [
    {
      "type": "SYSTEM",
      "permission": "READ"
    }
  ]
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/users/usuario1/permissions" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "permissions": [
      {
        "type": "SYSTEM",
        "permission": "READ"
      }
    ]
  }'
```

**Resposta esperada (200 OK):**
```json
{
  "status": "success"
}
```

---

## Atribuir Grupos de Conexões a um Usuário

**Endpoint:**  
```
POST /api/session/data/{dataSource}/users/{username}/connectionGroups
```

**Parâmetros:**

| Campo       | Tipo   | Obrigatório | Descrição                          |
|-------------|--------|-------------|------------------------------------|
| dataSource  | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| username    | string | ✅           | Nome de usuário                    |

**Corpo da Requisição:**
```json
{
  "connectionGroups": [
    {
      "identifier": "group1",
      "permissions": ["READ"]
    }
  ]
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/users/usuario1/connectionGroups" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "connectionGroups": [
      {
        "identifier": "group1",
        "permissions": ["READ"]
      }
    ]
  }'
```

**Resposta esperada (200 OK):**
```json
{
  "status": "success"
}
```

---

## Revogar Grupos de Conexões de um Usuário

**Endpoint:**  
```
DELETE /api/session/data/{dataSource}/users/{username}/connectionGroups
```

**Parâmetros:**

| Campo       | Tipo   | Obrigatório | Descrição                          |
|-------------|--------|-------------|------------------------------------|
| dataSource  | string | ✅           | Fonte de dados (ex: `postgresql`)  |
| username    | string | ✅           | Nome de usuário                    |

**Corpo da Requisição:**
```json
{
  "connectionGroups": [
    {
      "identifier": "group1",
      "permissions": ["READ"]
    }
  ]
}
```

**Exemplo de requisição (cURL):**
```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/users/usuario1/connectionGroups" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
    "connectionGroups": [
      {
        "identifier": "group1",
        "permissions": ["READ"]
      }
    ]
  }'
```

**Resposta esperada (200 OK):**
```json
{
  "status": "success"
}
