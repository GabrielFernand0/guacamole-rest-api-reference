# Apache Guacamole REST API — referência comunitária

Referência **não oficial** para integrar aplicações e scripts ao Apache Guacamole pela API HTTP usada pelo cliente web. O conteúdo reúne rotas, exemplos e observações práticas; não substitui o manual oficial nem a validação na instância em uso.

## Compatibilidade

As versões registradas como testadas neste projeto são **1.5.4, 1.5.5 e 1.6.0**. O comportamento e os campos disponíveis podem variar conforme a versão e o provedor de autenticação (por exemplo, PostgreSQL, MySQL ou LDAP). O valor de `dataSource` deve vir de `availableDataSources` na resposta de autenticação.

Esta documentação é independente e **não é mantida nem endossada pelo projeto Apache Guacamole**. Para integrações específicas de extensões, consulte também a documentação da própria extensão.

## Comece por aqui

1. Obtenha um token usando [Autenticação](endpoints/authentication.md).
2. Use o token no cabeçalho `Guacamole-Token` nas chamadas de API.
3. Consulte os [exemplos com cURL](examples/curl.md) ou [Python](examples/python.md).
4. Escolha o recurso:

| Recurso | Referência |
| --- | --- |
| Conexões | [Conexões](endpoints/connections.md) |
| Grupos de conexões | [Grupos de conexões](endpoints/connections-groups.md) |
| Usuários | [Usuários](endpoints/users.md) |
| Grupos de usuários | [Grupos de usuários](endpoints/user-groups.md) |
| Permissões | [Permissões](endpoints/permissions.md) |
| Histórico | [Histórico](endpoints/history.md) |
| Túneis da sessão | [Túneis](endpoints/tunnels.md) |
| Recursos de extensões | [Extensões](endpoints/extensions.md) |

## URL base e autenticação

A URL base é a raiz da aplicação Guacamole, incluindo o caminho de contexto quando aplicável, por exemplo `https://guac.example.com/guacamole`. Assim, o endpoint de autenticação fica em `{URL_BASE}/api/tokens`.

Prefira HTTPS e envie o token no cabeçalho `Guacamole-Token`. Evite incluir credenciais ou tokens em exemplos versionados, logs, histórico do shell ou URLs compartilhadas. Use uma conta com somente as permissões necessárias.

## Contribuições

Correções e exemplos reproduzíveis são bem-vindos. Ao abrir uma issue ou pull request, informe:

- versão do Guacamole e provedor de autenticação usados;
- endpoint, método e objetivo da chamada;
- resposta sanitizada, sem tokens, senhas, endereços ou nomes reais de ambientes.

Quando possível, valide a alteração em uma instância de teste e indique a versão testada.

## Licença

A documentação original deste repositório está sob [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Os exemplos de código estão sob a licença [MIT](LICENSE-CODE). Veja [LICENSE](LICENSE) para o escopo e as ressalvas sobre materiais de terceiros.

## Referências oficiais

- [Manual do Apache Guacamole 1.6.0](https://guacamole.apache.org/doc/gug/)
- [Documentação das APIs oficiais do Guacamole](https://guacamole.apache.org/api-documentation/)
- [Código-fonte oficial do cliente e das extensões](https://github.com/apache/guacamole-client)
- [Autenticação por token no código-fonte](https://github.com/apache/guacamole-client/blob/1.6.0/guacamole/src/main/java/org/apache/guacamole/rest/auth/TokenRESTService.java)
