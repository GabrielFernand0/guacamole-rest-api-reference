# Conexões

Uma conexão representa um destino remoto e seu protocolo, como SSH, RDP ou VNC. Os dados retornados e as operações permitidas dependem do provedor de autenticação e das permissões do usuário.

## Listar conexões

```http
GET /api/session/data/{dataSource}/connections
Guacamole-Token: <TOKEN>
```

A resposta é um objeto JSON indexado pelo identificador da conexão, não uma lista JSON. Exemplo reduzido:

```json
{
  "1": {
    "identifier": "1",
    "name": "Servidor SSH",
    "parentIdentifier": "ROOT",
    "protocol": "ssh",
    "parameters": {
      "hostname": "host.example",
      "port": "22",
      "username": "usuario"
    }
  }
}
```

## Consultar uma conexão

```http
GET /api/session/data/{dataSource}/connections/{identifier}
Guacamole-Token: <TOKEN>
```

## Criar uma conexão

```http
POST /api/session/data/{dataSource}/connections
Content-Type: application/json
Guacamole-Token: <TOKEN>
```

Exemplo de corpo para uma conexão SSH:

```json
{
  "name": "Servidor SSH",
  "parentIdentifier": "ROOT",
  "protocol": "ssh",
  "parameters": {
    "hostname": "host.example",
    "port": "22",
    "username": "usuario"
  },
  "attributes": {}
}
```

`ROOT` identifica o grupo de conexões raiz. Para outro grupo, use seu identificador. Os parâmetros de conexão variam por protocolo; consulte o schema e os parâmetros suportados pela sua instalação. A criação bem-sucedida devolve o objeto criado, incluindo o identificador atribuído pelo provedor.

## Atualizar uma conexão

```http
PUT /api/session/data/{dataSource}/connections/{identifier}
Content-Type: application/json
Guacamole-Token: <TOKEN>
```

Envie a representação atualizada da conexão aceita pelo seu provedor. Uma atualização bem-sucedida não precisa retornar um corpo.

## Excluir uma conexão

```http
DELETE /api/session/data/{dataSource}/connections/{identifier}
Guacamole-Token: <TOKEN>
```

Uma resposta bem-sucedida não tem corpo (HTTP 204). Confirme o identificador e as permissões antes de excluir.

## Observações

- `{dataSource}` é um identificador retornado pela autenticação, como `postgresql`; não é o nome do protocolo.
- Coleções de recursos do Guacamole são normalmente objetos JSON indexados por identificador.
- Os campos disponíveis podem variar de acordo com o protocolo e o provedor.
