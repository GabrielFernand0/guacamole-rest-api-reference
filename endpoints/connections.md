# Conexões

## Introdução

Conexões no Apache Guacamole representam acessos a servidores ou serviços remotos, como RDP, VNC ou SSH.
A API permite criar, atualizar, listar e deletar conexões, bem como associá-las a grupos e usuários.

---

## Listar Conexões

**Endpoint:**

```
GET /api/session/data/{dataSource}/connections
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                         |
| ---------- | ------ | ----------- | --------------------------------- |
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`) |

**Exemplo de requisição (cURL):**

```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/connections" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Exemplo de requisição (Python):**

```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/connections"
headers = {"Guacamole-Token": "SEU_TOKEN"}

response = requests.get(url, headers=headers)
print(response.json())
```

**Resposta esperada (200 OK):**

```json
[
  {
    "identifier": "1",
    "name": "Servidor Web",
    "protocol": "ssh",
    "parameters": {
        "hostname": "192.168.1.10",
        "port": "22",
        "username": "usuario"
    }
  }
]
```

---

## Criar Conexão

**Endpoint:**

```
POST /api/session/data/{dataSource}/connections
```

**Parâmetros (JSON):**

| Campo            | Tipo   | Obrigatório | Descrição                            |
| ---------------- | ------ | ----------- | ------------------------------------ |
| name             | string | ✅           | Nome da conexão                      |
| parentIdentifier | string | ✅           | ID do grupo de conexões              |
| protocol         | string | ✅           | Protocolo: `ssh`, `rdp`, `vnc`, etc. |
| parameters       | object | ✅           | Parâmetros específicos do protocolo  |

**Exemplo de requisição (cURL):**

```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/connections" \
  -H "Content-Type: application/json" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
        "name":"Conexão SSH",
        "parentIdentifier":"1",
        "protocol":"ssh",
        "parameters":{
            "hostname":"192.168.1.10",
            "port":"22",
            "username":"usuario"
        }
      }'
```

**Resposta esperada (201 Created):**

```json
{
  "identifier": "2",
  "name": "Conexão SSH",
  "protocol": "ssh",
  "parameters": {
      "hostname": "192.168.1.10",
      "port": "22",
      "username": "usuario"
  }
}
```

---

## Atualizar Conexão

**Endpoint:**

```
PUT /api/session/data/{dataSource}/connections/{id}
```

**Parâmetros (JSON):**

| Campo      | Tipo   | Obrigatório | Descrição               |
| ---------- | ------ | ----------- | ----------------------- |
| name       | string | ✅           | Novo nome da conexão    |
| protocol   | string | ✅           | Protocolo da conexão    |
| parameters | object | ✅           | Parâmetros do protocolo |

**Exemplo de requisição (cURL):**

```bash
curl -X PUT "http://SEU_GUACAMOLE/api/session/data/postgresql/connections/2" \
  -H "Content-Type: application/json" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
        "name":"Conexão SSH Atualizada",
        "protocol":"ssh",
        "parameters":{
            "hostname":"192.168.1.11",
            "port":"22",
            "username":"novo_usuario"
        }
      }'
```

**Resposta esperada (200 OK):**

```json
{
  "identifier": "2",
  "name": "Conexão SSH Atualizada",
  "protocol": "ssh",
  "parameters": {
      "hostname": "192.168.1.11",
      "port": "22",
      "username": "novo_usuario"
  }
}
```

---

## Deletar Conexão

**Endpoint:**

```
DELETE /api/session/data/{dataSource}/connections/{id}
```

**Parâmetros:**

| Campo | Tipo   | Obrigatório | Descrição               |
| ----- | ------ | ----------- | ----------------------- |
| id    | string | ✅           | ID da conexão a deletar |

**Exemplo de requisição (cURL):**

```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/connections/2" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Resposta esperada:**

* `204 No Content` – Conexão deletada com sucesso.

---

## Códigos de Resposta Comuns

| Código | Significado             |
| ------ | ----------------------- |
| 200    | Requisição bem-sucedida |
| 201    | Criado com sucesso      |
| 204    | Sem conteúdo            |
| 400    | Requisição inválida     |
| 401    | Não autorizado          |
| 404    | Não encontrado          |

---

## Boas Práticas

* Sempre verificar o grupo pai (`parentIdentifier`) antes de criar conexões.
* Manter os parâmetros do protocolo corretos para evitar falhas de autenticação.
* Nomear conexões de forma clara para facilitar a administração.





-----------------------------------------------------------------



# Conexões

## Introdução

Conexões no Apache Guacamole representam acessos a servidores ou serviços remotos, como RDP, VNC ou SSH.
A API permite criar, atualizar, listar e deletar conexões, bem como associá-las a grupos e usuários.

---

## Listar Conexões

**Endpoint:**

```
GET /api/session/data/{dataSource}/connections
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                         |
| ---------- | ------ | ----------- | --------------------------------- |
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`) |

**Exemplo de requisição (cURL):**

```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/connections" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Exemplo de requisição (Python):**

```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/connections"
headers = {"Guacamole-Token": "SEU_TOKEN"}

response = requests.get(url, headers=headers)
print(response.json())
```

**Resposta esperada (200 OK):**

```json
[
  {
    "identifier": "1",
    "name": "Servidor Web",
    "protocol": "ssh",
    "parameters": {
        "hostname": "192.168.1.10",
        "port": "22",
        "username": "usuario"
    }
  }
]
```

---

## Criar Conexão

**Endpoint:**

```
POST /api/session/data/{dataSource}/connections
```

**Parâmetros (JSON):**

| Campo             | Tipo   | Obrigatório | Descrição                                             |
| ----------------- | ------ | ----------- | ----------------------------------------------------- |
| name              | string | ✅           | Nome da conexão                                       |
| parentIdentifier  | string | ✅           | ID do grupo de conexões                               |
| protocol          | string | ✅           | Protocolo: `ssh`, `rdp`, `vnc`, etc.                  |
| parameters        | object | ✅           | Parâmetros específicos do protocolo                   |
| attributes        | object | ❌           | Atributos opcionais, como `max-connections`, `weight` |
| tags              | array  | ❌           | Lista de tags para organização                        |
| activeConnections | int    | ❌           | Número máximo de conexões simultâneas                 |
| readOnly          | bool   | ❌           | Indica se a conexão é somente leitura                 |

**Exemplo de requisição (cURL):**

```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/connections" \
  -H "Content-Type: application/json" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
        "name":"Conexão SSH",
        "parentIdentifier":"1",
        "protocol":"ssh",
        "parameters":{
            "hostname":"192.168.1.10",
            "port":"22",
            "username":"usuario"
        },
        "attributes":{
            "max-connections":5,
            "weight":10
        },
        "tags":["dev","ssh"],
        "activeConnections":1,
        "readOnly":false
      }'
```

**Resposta esperada (201 Created):**

```json
{
  "identifier": "2",
  "name": "Conexão SSH",
  "protocol": "ssh",
  "parameters": {
      "hostname": "192.168.1.10",
      "port": "22",
      "username": "usuario"
  },
  "attributes":{
      "max-connections":5,
      "weight":10
  },
  "tags":["dev","ssh"],
  "activeConnections":1,
  "readOnly":false
}
```

---

## Atualizar Conexão

**Endpoint:**

```
PUT /api/session/data/{dataSource}/connections/{id}
```

**Parâmetros (JSON):**

| Campo             | Tipo   | Obrigatório | Descrição                             |
| ----------------- | ------ | ----------- | ------------------------------------- |
| name              | string | ✅           | Novo nome da conexão                  |
| protocol          | string | ✅           | Protocolo da conexão                  |
| parameters        | object | ✅           | Parâmetros do protocolo               |
| attributes        | object | ❌           | Atributos opcionais                   |
| tags              | array  | ❌           | Lista de tags                         |
| activeConnections | int    | ❌           | Número máximo de conexões simultâneas |
| readOnly          | bool   | ❌           | Indica se a conexão é somente leitura |

**Exemplo de requisição (cURL):**

```bash
curl -X PUT "http://SEU_GUACAMOLE/api/session/data/postgresql/connections/2" \
  -H "Content-Type: application/json" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{
        "name":"Conexão SSH Atualizada",
        "protocol":"ssh",
        "parameters":{
            "hostname":"192.168.1.11",
            "port":"22",
            "username":"novo_usuario"
        },
        "attributes":{
            "max-connections":10,
            "weight":20
        },
        "tags":["prod","ssh"],
        "activeConnections":2,
        "readOnly":true
      }'
```

**Resposta esperada (200 OK):**

```json
{
  "identifier": "2",
  "name": "Conexão SSH Atualizada",
  "protocol": "ssh",
  "parameters": {
      "hostname": "192.168.1.11",
      "port": "22",
      "username": "novo_usuario"
  },
  "attributes":{
      "max-connections":10,
      "weight":20
  },
  "tags":["prod","ssh"],
  "activeConnections":2,
  "readOnly":true
}
```

---

## Deletar Conexão

**Endpoint:**

```
DELETE /api/session/data/{dataSource}/connections/{id}
```

**Parâmetros:**

| Campo | Tipo   | Obrigatório | Descrição               |
| ----- | ------ | ----------- | ----------------------- |
| id    | string | ✅           | ID da conexão a deletar |

**Exemplo de requisição (cURL):**

```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/connections/2" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Resposta esperada:**

* `204 No Content` – Conexão deletada com sucesso.

---

## Códigos de Resposta Comuns

| Código | Significado             |
| ------ | ----------------------- |
| 200    | Requisição bem-sucedida |
| 201    | Criado com sucesso      |
| 204    | Sem conteúdo            |
| 400    | Requisição inválida     |
| 401    | Não autorizado          |
| 404    | Não encontrado          |

---

## Boas Práticas

* Sempre verificar o grupo pai (`parentIdentifier`) antes de criar conexões.
* Manter os parâmetros do protocolo corretos para evitar falhas de autenticação.
* Nomear conexões de forma clara para facilitar a administração.
