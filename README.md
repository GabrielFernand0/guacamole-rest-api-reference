# Apache Guacamole REST API - Documentação não oficial

Documentação **não oficial** da API REST do Apache Guacamole, criada com base em:
- Testes práticos
- Uso real em produção
- Referências da comunidade

---

## Objetivo
- Fornecer uma referência rápida e clara para desenvolvedores e administradores.
- Facilitar a integração e automação do Guacamole via API.
- Centralizar exemplos e explicações úteis.

---

## Versões testadas
Esta documentação foi construída a partir de uso e validação real da API nas seguintes versões do Apache Guacamole:
- **1.5.4**
- **1.5.5**
- **1.6.0**

Embora outros releases possam funcionar de forma semelhante, todos os exemplos e endpoints descritos aqui foram confirmados como funcionais nessas versões.  
Para versões futuras, alguns detalhes podem mudar, e a contribuição da comunidade será bem-vinda para manter esta documentação atualizada.

---

## Aviso
> ⚠️ Esta documentação **não é oficial** e não é mantida pelo projeto Apache Guacamole.  
> Créditos à [documentação de referência](https://github.com/ridvanaltun/guacamole-rest-api-documentation).

---

## Common Responses
Esta seção descreve os códigos de resposta mais comuns retornados pela API:
 _______________________________
| Código | Significado          |
|--------|----------------------|
| 200    | A request succeeded  |
| 204    | No content           |
| 400    | Bad request          |
| 401    | Unauthorized         |
| 404    | Not found            |
|________|______________________|

---

## Estrutura dos Endpoints
Cada arquivo contém a descrição detalhada dos métodos, parâmetros, exemplos de requisição e resposta para cada recurso da API:

- **[Autenticação](endpoints/autentication.md)**
- **[Conexões](endpoints/connections.md)**
- **[Grupos de Conexões](endpoints/connections-groups.md)**
- **[Usuários](endpoints/users.md)**
- **[Grupos de Usuários](endpoints/user-groups.md)**
- **[Permissões](endpoints/permissions.md)**
- **[Histórico](endpoints/history.md)**
- **[Túneis](endpoints/tunnels.md)**

---

## Exemplos de Uso
Para facilitar a implementação, há exemplos práticos de chamadas à API em diferentes formatos:

- **[Exemplos com cURL](examples/curl.md)**
- **[Exemplos com Python](examples/python.md)**
