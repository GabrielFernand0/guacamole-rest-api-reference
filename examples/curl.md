# Exemplos com cURL

Estes exemplos usam Bash, cURL e `jq`. Defina a URL raiz da aplicação Guacamole (incluindo o caminho de contexto, se houver). Use HTTPS fora de um ambiente local de teste.

```bash
export GUACAMOLE_URL="https://guac.example.com/guacamole"
read -r -p "Usuário Guacamole: " GUAC_USERNAME
read -r -s -p "Senha Guacamole: " GUAC_PASSWORD
printf '\n'

AUTH_JSON=$(curl --fail-with-body --silent --show-error \
  --data-urlencode "username=$GUAC_USERNAME" \
  --data-urlencode "password=$GUAC_PASSWORD" \
  "$GUACAMOLE_URL/api/tokens")
unset GUAC_PASSWORD

TOKEN=$(printf '%s' "$AUTH_JSON" | jq -er '.authToken')
DATA_SOURCE=$(printf '%s' "$AUTH_JSON" | jq -er '.dataSource')
```

## Listar conexões

Envie o token no cabeçalho `Guacamole-Token`. A coleção de conexões é um objeto JSON indexado pelos identificadores:

```bash
curl --fail-with-body --silent --show-error \
  -H "Guacamole-Token: $TOKEN" \
  "$GUACAMOLE_URL/api/session/data/$DATA_SOURCE/connections" | jq
```

## Encerrar a sessão

```bash
curl --fail-with-body --silent --show-error \
  -X DELETE "$GUACAMOLE_URL/api/tokens/$TOKEN"
unset TOKEN AUTH_JSON GUAC_USERNAME DATA_SOURCE
```

Não cole tokens ou senhas em scripts versionados, comandos salvos no histórico, tickets ou logs.
