# Autenticação

O endpoint de tokens autentica um usuário e devolve um token de sessão do Guacamole.

## Criar um token

```http
POST /api/tokens
Content-Type: application/x-www-form-urlencoded
```

Envie `username` e `password` como campos de formulário. A resposta inclui o token, a fonte de dados selecionada e as fontes disponíveis para esse usuário.

Exemplo de resposta:

```json
{
  "authToken": "<TOKEN>",
  "username": "admin",
  "dataSource": "postgresql",
  "availableDataSources": ["postgresql"]
}
```

Use o valor retornado em `dataSource` nas rotas que contêm `{dataSource}`. Não presuma que toda instalação usa `postgresql`.

Nas chamadas protegidas, o token pode ser enviado pelo cabeçalho `Guacamole-Token`. O parâmetro de consulta `token` também é aceito por compatibilidade, mas URLs podem ser gravadas em logs e histórico do navegador; prefira o cabeçalho.

## Encerrar a sessão

```http
DELETE /api/tokens/{authToken}
```

Uma resposta bem-sucedida não tem corpo (HTTP 204). Trate o token como uma credencial e não o imprima nem o registre em logs.

## Expiração

Tokens de sessão expiram após um período sem atividade. O tempo é controlado pela configuração `API_SESSION_TIMEOUT`; o padrão documentado é 60 minutos de inatividade. Veja a [configuração oficial do Guacamole](https://guacamole.apache.org/doc/gug/configuring-guacamole.html).

## Segurança

- Use HTTPS.
- Não use credenciais padrão em produção.
- Use uma conta de automação com permissões mínimas.
- Não publique tokens, senhas ou respostas contendo dados de clientes.
- Guarde segredos em variáveis de ambiente ou em um gerenciador de segredos.
