# Usuários

As operações de usuário dependem do provedor de autenticação. Um provedor pode não permitir criar, editar ou excluir usuários por meio da API.

## Listar usuários

```http
GET /api/session/data/{dataSource}/users
Guacamole-Token: <TOKEN>
```

A resposta é um objeto JSON indexado pelo nome de usuário:

```json
{
  "usuario1": {
    "username": "usuario1",
    "attributes": {
      "fullname": "Usuário de exemplo",
      "email": "usuario@example.com"
    }
  }
}
```

## Consultar, criar, atualizar ou excluir

```http
GET    /api/session/data/{dataSource}/users/{username}
POST   /api/session/data/{dataSource}/users
PUT    /api/session/data/{dataSource}/users/{username}
DELETE /api/session/data/{dataSource}/users/{username}
```

As operações de criação e atualização recebem JSON conforme o schema de usuário exposto pelo provedor. Não presuma que todos os provedores aceitam os mesmos campos.

A senha é atualizada em um recurso próprio:

```http
PUT /api/session/data/{dataSource}/users/{username}/password
Content-Type: application/json
Guacamole-Token: <TOKEN>
```

Consulte o schema da sua instalação para saber quais campos de senha são exigidos.

## Permissões e associações

Recursos relacionados a um usuário incluem `permissions`, `effectivePermissions`, `userGroups`, `connections` e `connectionGroups`. Para adicionar ou remover permissões, veja [Permissões](permissions.md). Associações usam operações PATCH no recurso correspondente e o formato JSON Patch do Guacamole.
