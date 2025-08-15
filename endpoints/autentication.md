# Autenticação

## Introdução

A API do Apache Guacamole utiliza autenticação baseada em **token**.
Para acessar endpoints protegidos, é necessário primeiro obter um token de sessão válido.

---

## Obter Token

**Endpoint:**

```
POST /api/tokens
```

**Parâmetros (JSON):**

| Campo    | Tipo   | Obrigatório | Descrição            |
| -------- | ------ | ----------- | -------------------- |
| username | string | ✅         | Usuário do Guacamole |
| password | string | ✅         | Senha do usuário     |

**Exemplo de requisição (cURL):**

```bash
curl -X POST "http://SEU_GUACAMOLE/api/tokens" \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"admin"}'
```

**Exemplo de requisição (Python):**

```python
import requests

url = "http://SEU_GUACAMOLE/api/tokens"
data = {"username": "admin", "password": "admin"}

response = requests.post(url, json=data)
print(response.json())
```

**Resposta esperada (200 OK):**

```json
{
  "authToken": "cddf7e9b-1c0e-4f9e-99bb-3dcf5b8fbc41",
  "username": "admin",
  "dataSource": "postgresql"
}
```

**Observações:**

* O token expira após um período de inatividade.
* Requisições subsequentes devem incluir o token no **query param** `token` ou no header `Guacamole-Token`.
* Em caso de logout, utilize o endpoint `/api/tokens/{token}` com método `DELETE`.

---

## Logout

**Endpoint:**

```
DELETE /api/tokens/{token}
```

**Parâmetros:**

| Campo | Tipo   | Obrigatório | Descrição                |
| ----- | ------ | ----------- | ------------------------ |
| token | string | ✅           | Token retornado no login |

**Exemplo de requisição (cURL):**

```bash
curl -X DELETE "http://SEU_GUACAMOLE/api/tokens/cddf7e9b-1c0e-4f9e-99bb-3dcf5b8fbc41"
```

**Resposta esperada:**

* `204 No Content` – Logout realizado com sucesso.

---

## Códigos de Resposta Comuns

| Código | Significado             |
| ------ | ----------------------- |
| 200    | Requisição bem-sucedida |
| 204    | Sem conteúdo            |
| 400    | Requisição inválida     |
| 401    | Não autorizado          |
| 404    | Não encontrado          |

---

## Boas Práticas

* Reautenticar antes que o token expire.
* Evitar armazenar tokens em locais inseguros.
* Tratar corretamente os códigos de erro (`401 Unauthorized`, `400 Bad Request`, etc.).
* Utilizar tokens apenas em conexões seguras (HTTPS).
