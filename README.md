# Envio de Email com PHP :email:

[![GitHub repo size](https://img.shields.io/github/repo-size/stackforgecode/SendMail-PHP)](https://github.com/stackforgecode/SendMail-PHP)
[![GitHub license](https://img.shields.io/github/license/stackforgecode/SendMail-PHP?style=flat)](https://github.com/stackforgecode/SendMail-PHP/blob/main/LICENSE)

Este projeto é um exemplo simples de como enviar e-mails utilizando PHP. Ele utiliza a biblioteca PHPMailer para realizar o envio de forma fácil e segura.

## Tecnologias :rocket:

- PHP 8.1 ou superior
- PHPMailer
- Composer

## Instruções de inicialização e instalação :computer:

1. Clone este repositório:

```bash
git clone https://github.com/stackforgecode/SendMail-PHP.git
```

2. Acesse o diretório do projeto:

```bash
cd SendMail-PHP
```

3. Instale as dependências usando o Composer:

```bash
composer install
```

4. Crie um arquivo `.env` na raiz do projeto e adicione as seguintes configurações:

```plaintext
SMTP_HOST=sandbox.smtp.mailtrap.io
SMTP_PORT=587
SMTP_USERNAME=8c1e417a7cc8a6
SMTP_PASSWORD=ba2121b44d8737
```

Certifique-se de substituir as configurações do servidor SMTP pelas suas configurações fornecidas pelo Mailtrap.

5. Inicie o servidor web embutido do PHP:

```bash
php -S localhost:8000 -t public
```

6. Acesse o formulário de contato no seu navegador em [http://localhost:8000/contatos.php](http://localhost:8000/contatos.php).

## Versões das bibliotecas :bookmark_tabs:

- PHPMailer: ^6.5
- vlucas/phpdotenv: ^5.4

## Contribuição :sparkles:

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues e enviar pull requests.

## Autor :bust_in_silhouette:

- Empresa: StackForge
- Usuário: @stackforgecode
- Autor: @rubenslyra

## Assista ao vídeo :movie_camera:

Confira nosso tutorial em vídeo sobre como enviar e-mails com PHP no YouTube: [StackForge - Envio de Email com PHP](https://youtube.com/stackforge)

Agradecemos por usar nosso exemplo de envio de e-mails com PHP! :heart: Esperamos que seja útil para você!

---
