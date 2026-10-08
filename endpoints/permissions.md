# Permissões

Permissões são consultadas e alteradas no subrecurso `permissions` de um usuário ou grupo de usuários. Alterações usam PATCH com uma lista de operações JSON Patch; não são feitas com POST ou DELETE nesse endpoint.

## Consultar permissões de um usuário

```http
GET /api/session/data/{dataSource}/users/{username}/permissions
Guacamole-Token: <TOKEN>
```

As permissões efetivas de um usuário também podem ser consultadas em `/users/{username}/effectivePermissions`.

## Conceder permissão de sistema

```http
PATCH /api/session/data/{dataSource}/users/{username}/permissions
Content-Type: application/json
Guacamole-Token: <TOKEN>
```

Corpo para conceder permissão de leitura do sistema:

```json
[
  {
    "op": "add",
    "path": "/systemPermissions",
    "value": "READ"
  }
]
```

## Remover permissão

Use a mesma rota e altere `op` para `remove`:

```json
[
  {
    "op": "remove",
    "path": "/systemPermissions",
    "value": "READ"
  }
]
```

## Permissões sobre objetos

O caminho do patch identifica o tipo de permissão e o objeto. Por exemplo, permissões de conexão usam `/connectionPermissions/{identifier}`; permissões de grupo de conexões usam `/connectionGroupPermissions/{identifier}`. Valores válidos dependem do tipo de objeto e incluem permissões como `READ`, `UPDATE`, `DELETE` e `ADMINISTER`.

Os mesmos recursos de permissões estão disponíveis para grupos de usuários em `/userGroups/{identifier}/permissions`. O provedor de autenticação precisa permitir a operação.
