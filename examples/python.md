# Exemplos com Python

Requer Python 3 e o pacote `requests`. O exemplo pede a senha sem exibi-la, autentica usando campos de formulário, lista conexões e encerra a sessão.

```python
import getpass
import os

import requests

base_url = os.environ["GUACAMOLE_URL"].rstrip("/")
username = input("Usuário Guacamole: ")
password = getpass.getpass("Senha Guacamole: ")

with requests.Session() as session:
    auth_response = session.post(
        f"{base_url}/api/tokens",
        data={"username": username, "password": password},
        timeout=20,
    )
    auth_response.raise_for_status()
    auth = auth_response.json()

    token = auth["authToken"]
    data_source = auth["dataSource"]
    session.headers["Guacamole-Token"] = token

    try:
        response = session.get(
            f"{base_url}/api/session/data/{data_source}/connections",
            timeout=20,
        )
        response.raise_for_status()

        # A coleção é um objeto indexado pelo identificador da conexão.
        for identifier, connection in response.json().items():
            print(identifier, connection.get("name"), connection.get("protocol"))
    finally:
        session.delete(f"{base_url}/api/tokens/{token}", timeout=20).raise_for_status()
```

Defina `GUACAMOLE_URL` com a raiz da aplicação, incluindo seu caminho de contexto, por exemplo `https://guac.example.com/guacamole`. Não imprima nem registre o token. Para ambientes remotos, use HTTPS.
