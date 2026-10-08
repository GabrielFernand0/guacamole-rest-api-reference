# Grupos de usuários

Grupos de usuários permitem associar pessoas e outros grupos. O suporte e os campos disponíveis dependem do provedor de autenticação.

## Listar grupos

```http
GET /api/session/data/{dataSource}/userGroups
Guacamole-Token: <TOKEN>
```

A resposta é um objeto JSON indexado pelo identificador do grupo.

## Consultar, criar, atualizar ou excluir

```http
GET    /api/session/data/{dataSource}/userGroups/{identifier}
POST   /api/session/data/{dataSource}/userGroups
PUT    /api/session/data/{dataSource}/userGroups/{identifier}
DELETE /api/session/data/{dataSource}/userGroups/{identifier}
```

Use o schema de grupo disponibilizado pela sua instalação para preparar os corpos JSON de criação e atualização.

## Associar membros

Os membros e grupos relacionados são recursos separados. Para alterar o conjunto de usuários de um grupo, use PATCH em `memberUsers`:

```http
PATCH /api/session/data/{dataSource}/userGroups/{identifier}/memberUsers
Content-Type: application/json
Guacamole-Token: <TOKEN>
```

O corpo é uma lista de operações JSON Patch:

```json
[
  { "op": "add", "path": "/", "value": "usuario1" },
  { "op": "remove", "path": "/", "value": "usuario2" }
]
```

Para associar grupos, os recursos são `memberUserGroups` e `userGroups` na rota do grupo. Use o mesmo formato PATCH, com o identificador do objeto em `value`.

Cada operação de PATCH é aplicada ao conjunto de associações; a permissão e o suporte dependem do provedor.
