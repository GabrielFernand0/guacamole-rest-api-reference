# Grupos de Conexões

## Introdução

Grupos de conexões permitem organizar múltiplas conexões dentro do Apache Guacamole.
Eles ajudam a estruturar o acesso a diferentes servidores e serviços de forma hierárquica e controlada.

---

## Listar Grupos de Conexões

**Endpoint:**

```
GET /api/session/data/{dataSource}/connectionGroups/{id}/children
```

**Parâmetros:**

| Campo      | Tipo   | Obrigatório | Descrição                             |
| ---------- | ------ | ----------- | ------------------------------------- |
| dataSource | string | ✅           | Fonte de dados (ex: `postgresql`)     |
| id         | string | ✅           | ID do grupo de conexões (0 para root) |

**Exemplo de requisição (cURL):**

```bash
curl -X GET "http://SEU_GUACAMOLE/api/session/data/postgresql/connectionGroups/0/children" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Exemplo de requisição (Python):**

```python
import requests

url = "http://SEU_GUACAMOLE/api/session/data/postgresql/connectionGroups/0/children"
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
    "type": "ORGANIZATIONAL",
    "childConnections": [],
    "childConnectionGroups": []
  }
]
```

---

## Criar Grupo de Conexões

**Endpoint:**

```
POST /api/session/data/{dataSource}/connectionGroups
```

**Parâmetros (JSON):**

| Campo            | Tipo   | Obrigatório | Descrição                             |
| ---------------- | ------ | ----------- | ------------------------------------- |
| name             | string | ✅           | Nome do grupo de conexões             |
| type             | string | ✅           | Tipo: `ORGANIZATIONAL` ou `BALANCING` |
| parentIdentifier | string | ✅           | ID do grupo pai (0 para root)         |

**Exemplo de requisição (cURL):**

```bash
curl -X POST "http://SEU_GUACAMOLE/api/session/data/postgresql/connectionGroups" \
  -H "Content-Type: application/json" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{"name":"Novo Grupo","type":"ORGANIZATIONAL","parentIdentifier":"0"}'
```

**Resposta esperada (201 Created):**

```json
{
  "identifier": "2",
  "name": "Novo Grupo",
  "type": "ORGANIZATIONAL",
  "childConnections": [],
  "childConnectionGroups": []
}
```

---

## Atualizar Grupo de Conexões

**Endpoint:**

```
PUT /api/session/data/{dataSource}/connectionGroups/{id}
```

**Parâmetros (JSON):**

| Campo | Tipo   | Obrigatório | Descrição          |
| ----- | ------ | ----------- | ------------------ |
| name  | string | ✅           | Novo nome do grupo |
| type  | string | ✅           | Tipo do grupo      |

**Exemplo de requisição (cURL):**

```bash
curl -X PUT "http://SEU_GUACAMOLE/api/session/data/postgresql/connectionGroups/2" \
  -H "Content-Type: application/json" \
  -H "Guacamole-Token: SEU_TOKEN" \
  -d '{"name":"Grupo Atualizado","type":"ORGANIZATIONAL"}'
```

**Resposta esperada (200 OK):**

```json
{
  "identifier": "2",
  "name": "Grupo Atualizado",
  "type": "ORGANIZATIONAL"
}
```

---

## Deletar Grupo de Conexões

**Endpoint:**

```
DELETE /api/session/data/{dataSource}/connectionGroups/{id}
```

**Parâmetros:**

| Campo | Tipo   | Obrigatório | Descrição             |
| ----- | ------ | ----------- | --------------------- |
| id    | string | ✅           | ID do grupo a deletar |

**Exemplo de requisição (cURL):**

```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/session/data/postgresql/connectionGroups/2" \
  -H "Guacamole-Token: SEU_TOKEN"
```

**Resposta esperada:**

* `204 No Content` – Grupo deletado com sucesso.

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

* Evitar deletar grupos que ainda possuem conexões ou subgrupos ativos.
* Utilizar IDs corretos do `dataSource` e do grupo pai.
* Manter nomes de grupos claros e organizados para facilitar administração.
