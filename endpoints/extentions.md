# Extensões

## Introdução
O Apache Guacamole permite extensões que adicionam funcionalidades ao sistema, como autenticação adicional, novos protocolos ou integração com serviços externos.  
A API REST fornece endpoints para listar, habilitar, desabilitar ou obter informações detalhadas sobre as extensões instaladas.

---

## Listar Extensões

**Endpoint:**  
```
GET /api/session/data/{dataSource}/extensions
```

**Parâmetros:**

| Campo       | Tipo   | Obrigatório | Descrição                        |
|------------|--------|-------------|---------------------------------|
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`) |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/extensions" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Exemplo de requisição (Python):**
```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/extensions"
headers = {"Guacamole-Token": "SEU_TOKEN"}

response = requests.get(url, headers=headers)
print(response.json())
```

**Resposta esperada (200 OK):**
```json
[
  {
    "identifier": "mysql-auth",
    "name": "MySQL Authentication",
    "version": "1.0.0",
    "enabled": true,
    "provides": ["authentication"]
  },
  {
    "identifier": "ldap-auth",
    "name": "LDAP Authentication",
    "version": "1.2.1",
    "enabled": false,
    "provides": ["authentication"]
  }
]
```

---

## Ativar Extensão

**Endpoint:**  
```
POST /api/session/data/{dataSource}/extensions/{identifier}/enable
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição          |
|-----------|--------|-------------|------------------|
| identifier | string | ✅           | ID da extensão a ativar |

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/extensions/mysql-auth/enable" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Resposta esperada (200 OK):**
```json
{
  "identifier": "mysql-auth",
  "enabled": true
}
```

---

## Desativar Extensão

**Endpoint:**  
```
POST /api/session/data/{dataSource}/extensions/{identifier}/disable
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição          |
|-----------|--------|-------------|------------------|
| identifier | string | ✅           | ID da extensão a desativar |

**Exemplo de requisição (cURL):**
```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/extensions/mysql-auth/disable" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Resposta esperada (200 OK):**
```json
{
  "identifier": "mysql-auth",
  "enabled": false
}
```

---

## Obter Detalhes de uma Extensão

**Endpoint:**  
```
GET /api/session/data/{dataSource}/extensions/{identifier}
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição          |
|-----------|--------|-------------|------------------|
| identifier | string | ✅           | ID da extensão |

**Exemplo de requisição (cURL):**
```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/extensions/mysql-auth" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Resposta esperada (200 OK):**
```json
{
  "identifier": "mysql-auth",
  "name": "MySQL Authentication",
  "version": "1.0.0",
  "enabled": true,
  "provides": ["authentication"]
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
