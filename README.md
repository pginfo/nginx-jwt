# Validar token JWT usando Nginx

Para validar um token JWT fornecido na URL no parâmetro "ktoken" de uma requisição HTTP GET usando o próprio Nginx, você pode seguir este exemplo de configuração:

```nginx
http {
    # Configuração do módulo jwt
    jwt_key "example_key" "path/to/public/key.pem";

    server {
        listen 80;
        server_name example.com;

        location /api {
            # Habilita a autenticação JWT
            auth_jwt "Restricted Zone";
            auth_jwt_key_file "example_key";

            # Define o token a ser validado
            set $jwt_token $arg_ktoken;

            # Opções adicionais de validação podem ser especificadas, como expiração do token

            # Ação em caso de token inválido
            auth_jwt_errors off;

            # Configurações adicionais para tratamento de erro e regras de acesso
        }
    }
}
```

**Explicação**:

- `jwt_key`: Define uma chave JWT para uso nas configurações de validação. Você precisa fornecer o nome da chave e o caminho para a chave pública.
- `auth_jwt`: Ativa a validação JWT para a localização especificada.
- `auth_jwt_key_file`: Especifica a chave JWT a ser usada para verificar a assinatura do token.
- `set $jwt_token $arg_ktoken`: Define a variável `$jwt_token` para conter o valor do parâmetro "ktoken" na URL da requisição HTTP GET.
- `auth_jwt_errors`: Especifica o comportamento em caso de erro na validação JWT. Neste exemplo, estamos desativando a geração de respostas de erro JWT.
- Dentro da localização /api, você pode adicionar outras configurações, como regras de acesso e manipulação de erros, conforme necessário.

Certifique-se de substituir os valores de exemplo pelos valores reais relevantes para o seu sistema, como nomes de chaves e caminhos de arquivos.
