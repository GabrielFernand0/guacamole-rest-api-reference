# Histórico

O histórico fica disponível por fonte de dados e é dividido entre registros de conexão e de usuário. Os registros disponíveis dependem do provedor de autenticação e das extensões instaladas.

## Histórico de conexões

Listar registros:

```http
GET /api/session/data/{dataSource}/history/connections
Guacamole-Token: <TOKEN>
```

Consultar um registro pelo identificador:

```http
GET /api/session/data/{dataSource}/history/connections/{identifier}
Guacamole-Token: <TOKEN>
```

## Histórico de usuários

```http
GET /api/session/data/{dataSource}/history/users
GET /api/session/data/{dataSource}/history/users/{identifier}
Guacamole-Token: <TOKEN>
```

Os registros e os campos retornados variam entre provedores. Não trate o histórico como uma fonte de auditoria garantida sem confirmar retenção, configuração e suporte do provedor usado.
