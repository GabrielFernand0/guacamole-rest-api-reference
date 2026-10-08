# Grupos de conexões

Grupos organizam conexões e outros grupos em uma árvore. O grupo raiz usa o identificador `ROOT`.

## Consultar a árvore de grupos

```http
GET /api/session/data/{dataSource}/connectionGroups/{identifier}/tree
Guacamole-Token: <TOKEN>
```

Use `ROOT` para consultar a árvore a partir da raiz. A resposta é um objeto de grupo com seus descendentes, sujeito às permissões do usuário.

## Listar grupos

```http
GET /api/session/data/{dataSource}/connectionGroups
Guacamole-Token: <TOKEN>
```

A resposta é um objeto JSON indexado pelos identificadores dos grupos.

## Criar um grupo

```http
POST /api/session/data/{dataSource}/connectionGroups
Content-Type: application/json
Guacamole-Token: <TOKEN>
```

Exemplo de corpo:

```json
{
  "name": "Operações",
  "type": "ORGANIZATIONAL",
  "parentIdentifier": "ROOT",
  "attributes": {}
}
```

Os tipos de grupo incluem `ORGANIZATIONAL` e `BALANCING`. Campos e validações podem depender do provedor de autenticação.

## Atualizar ou excluir

```http
PUT /api/session/data/{dataSource}/connectionGroups/{identifier}
DELETE /api/session/data/{dataSource}/connectionGroups/{identifier}
Guacamole-Token: <TOKEN>
```

Envie o objeto atualizado no corpo do `PUT`. Uma atualização ou exclusão bem-sucedida pode retornar sem corpo (HTTP 204).

## Observações

- `{dataSource}` deve ser o identificador retornado pelo endpoint de autenticação.
- O endpoint `/tree` retorna a estrutura hierárquica; ele não se chama `/children`.
- Não use `0` como identificador do grupo raiz: use `ROOT`.
