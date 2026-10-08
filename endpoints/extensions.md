# Recursos de extensões

O núcleo do Guacamole não oferece uma API genérica para listar, ativar ou desativar qualquer extensão instalada. A instalação e configuração de extensões são administradas no servidor, conforme o manual da extensão.

Uma extensão de autenticação pode expor recursos REST próprios. O Guacamole encaminha essas rotas para o provedor correspondente:

```text
/api/ext/{identifier}
/api/session/{authToken}/ext/{dataSource}
```

A forma dos caminhos abaixo dessas rotas e seus métodos HTTP depende da extensão. Consulte a documentação do módulo que fornece o recurso; não presuma que uma rota existe em todas as instalações.

Referências: [manual oficial](https://guacamole.apache.org/doc/gug/) e [código-fonte oficial das extensões](https://github.com/apache/guacamole-client).
