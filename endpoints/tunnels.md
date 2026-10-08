# Túneis da sessão

Um túnel é parte de uma sessão ativa do Guacamole. A coleção de túneis pertence ao token de sessão; ela não é uma coleção de conexões configuradas e não oferece operações genéricas de criação de conexões.

## Listar túneis da sessão

```http
GET /api/session/{authToken}/tunnels
```

A resposta é uma coleção de identificadores de túneis associados à sessão.

## Consultar um túnel

```http
GET /api/session/{authToken}/tunnels/{tunnelId}/protocol
GET /api/session/{authToken}/tunnels/{tunnelId}/activeConnection
```

O primeiro recurso informa o protocolo associado ao túnel; o segundo expõe a conexão ativa associada, quando disponível.

O token aparece no caminho destas rotas. Trate a URL completa como sensível e evite registrá-la ou compartilhá-la. Para encerrar a sessão, use o endpoint de logout descrito em [Autenticação](authentication.md).
