# Instruções de Configuração e Uso do Projeto

📂 **Estrutura de Diretórios do Projeto**

```
meu-projeto/
├── composer.json
├── composer.lock
├── public/
│   ├── index.php
│   └── contatos.php
├── routes/
│   └── web.php
└── src/
    └── Mailer.php
```

📦 **Dependências**

- [phpmailer/phpmailer](https://packagist.org/packages/phpmailer/phpmailer): ^6.5
- [vlucas/phpdotenv](https://packagist.org/packages/vlucas/phpdotenv): ^5.4

🔧 **Configuração e Instalação**

1. Clone o repositório para o seu ambiente local:

```bash
git clone https://github.com/stackforgecode/SendMail-PHP.git
```

2. Navegue até o diretório do projeto:

```bash
cd SendMail-PHP
```

3. Instale as dependências do projeto usando o Composer:

```bash
composer install
```

4. Crie um arquivo `.env` no diretório raiz do projeto com as seguintes informações:

```
SMTP_HOST=sandbox.smtp.mailtrap.io
SMTP_PORT=587
SMTP_USERNAME=8c1e417a7cc8a6
SMTP_PASSWORD=ba2121b44d8737
DB_DATABASE=database.sqlite
```

5. Configure o seu servidor web para apontar para o diretório `public/` do projeto.

⚙️ **Uso**

- Acesse o formulário de contato em `http://localhost/contatos.php`.
- Preencha os campos do formulário com o nome, e-mail e mensagem desejados.
- Clique em "Enviar" para enviar o e-mail.

🗃️ **Banco de Dados**

- O projeto utiliza o banco de dados SQLite.
- O arquivo de banco de dados `database.sqlite` será criado automaticamente na raiz do projeto.

🔒 **Importante**

Certifique-se de substituir as configurações do servidor SMTP (`SMTP_HOST`, `SMTP_PORT`, `SMTP_USERNAME` e `SMTP_PASSWORD`) pelas suas próprias configurações fornecidas pelo Mailtrap.

⚡ **Tags**

#PHP #Composer #PHPMailer #Dotenv #Mailtrap #SMTP #SQLite #FormulárioDeContato

-----------------------------------------------------
----------- Inicializando ---------------------------
-----------------------------------------------------

## Estrutura de diretórios do projeto:

```
meu-projeto/
├── composer.json
├── composer.lock
├── public/
│   ├── index.php
│   └── contatos.php
├── routes/
│   └── web.php
├── src/
│   ├── Mailer.php
│   └── Utils.php
├── storage/
│   └── database.sqlite
├── .env
├── utils.md
└── README.md
```

## Arquivo `composer.json`:

```json
{
    "autoload": {
        "psr-4": {
            "App\\": "src/"
        }
    },
    "require": {
        "phpmailer/phpmailer": "^6.5",
        "vlucas/phpdotenv": "^5.4",
        "symfony/var-dumper": "^5.4",
        "illuminate/database": "^8.0",
        "illuminate/console": "^8.0",
        "doctrine/dbal": "^3.1",
        "nikic/php-parser": "^4.11"
    },
    "require-dev": {
        "psy/psysh": "^0.10.5"
    }
}
```

## Instale as dependências do projeto:

```bash
composer install
```

## Arquivo `.env`:

Crie um novo arquivo chamado `.env` no diretório raiz do projeto e adicione as seguintes linhas ao arquivo:

```plaintext
SMTP_HOST=sandbox.smtp.mailtrap.io
SMTP_PORT=587
SMTP_USERNAME=8c1e417a7cc8a6
SMTP_PASSWORD=ba2121b44d8737
DB_CONNECTION=sqlite
DB_DATABASE=/path/to/storage/database.sqlite
```

Certifique-se de substituir as configurações do servidor SMTP (`SMTP_HOST`, `SMTP_PORT`, `SMTP_USERNAME` e `SMTP_PASSWORD`) pelas suas configurações fornecidas pelo Mailtrap. Além disso, ajuste o caminho para o arquivo `database.sqlite` no parâmetro `DB_DATABASE`.

## Arquivo `index.php`:

```php
<?php
require_once '../vendor/autoload.php';
require_once '../routes/web.php';

use App\Mailer;
use Dotenv\Dotenv;
use Symfony\Component\VarDumper\VarDumper;

// Carrega as variáveis de ambiente
$dotenv = Dotenv::createImmutable(__DIR__ . '/..');
$dotenv->load();

// Verifica se o formulário foi submetido
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    // Obtenha os dados do formulário
    $name = $_POST['name'];
    $email = $_POST['email'];
    $message = $_POST['message'];

    // Validação dos dados (faça suas próprias validações de acordo com suas necessidades)

    // Instancie o objeto Mailer
    $mailer = new Mailer();

    // Envie o e-mail
    $result = $mailer->sendEmail($name, $email, $message);

    if ($result) {
        echo 'E-mail enviado com sucesso!';
    } else {
        echo 'Ocorreu um erro ao enviar o e-mail.';
    }
}

// Exemplo de uso do VarDumper
$data = ['key' => 'value'];
VarDumper::dump($data);
```

## Arquivo `contatos.php`:



```php
<!DOCTYPE html>
<html>
<head>
    <title>Contatos</title>
</head>
<body>
    <h1>Formulário de Contato</h1>
    <form method="POST" action="index.php">
        <label for="name">Nome:</label>
        <input type="text" name="name" id="name" required><br><br>

        <label for="email">E-mail:</label>
        <input type="email" name="email" id="email" required><br><br>

        <label for="message">Mensagem:</label><br>
        <textarea name="message" id="message" rows="5" required></textarea><br><br>

        <input type="submit" value="Enviar">
    </form>
</body>
</html>
```

## Arquivo `web.php`:

```php
<?php
// Defina suas rotas aqui
```

## Classe `Mailer` em `Mailer.php`:

```php
<?php
namespace App;

use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;
use Dotenv\Dotenv;

class Mailer
{
    public function sendEmail($name, $email, $message)
    {
        $dotenv = Dotenv::createImmutable(__DIR__ . '/..');
        $dotenv->load();

        $mail = new PHPMailer(true);

        try {
            // Configurações do servidor SMTP
            $mail->isSMTP();
            $mail->Host = $_ENV['SMTP_HOST'];
            $mail->SMTPAuth = true;
            $mail->Username = $_ENV['SMTP_USERNAME'];
            $mail->Password = $_ENV['SMTP_PASSWORD'];
            $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
            $mail->Port = $_ENV['SMTP_PORT'];

            // Remetente e destinatário
            $mail->setFrom('remetente@example.com', 'Nome do Remetente');
            $mail->addAddress('destinatario@example.com', 'Nome do Destinatário');

            // Conteúdo do e-mail
            $mail->isHTML(true);
            $mail->Subject = 'Assunto do e-mail';
            $mail->Body = "Nome: $name<br>Email: $email<br>Mensagem: $message";

            $mail->send();
            return true;
        } catch (Exception $e) {
            return false;
        }
    }
}
```

## Classe `Utils` em `Utils.php`:

```php
<?php
namespace App;

class Utils
{
    public static function setupDatabase()
    {
        $dbPath = $_ENV['DB_DATABASE'];

        if (!file_exists($dbPath)) {
            touch($dbPath);
        }
    }
}
```

## Arquivo `utils.md`:

### Utilizando o Tinker

O Tinker é uma ferramenta interativa para interagir com o Laravel através da linha de comando. Com ele, você pode executar código PHP, testar funcionalidades e explorar seu aplicativo.

Principais comandos do Tinker:

- `php artisan tinker`: Inicia o Tinker.
- `app()`: Retorna uma instância do aplicativo Laravel.
- `getRoutes()`: Retorna uma lista de rotas registradas.
- `route('nome_da_rota')`: Gera uma URL para a rota com o nome especificado.
- `DB::table('nome_da_tabela')->get()`: Retorna todos os registros de uma tabela do banco de dados.
- `Model::find($

id)`: Retorna um registro com base no ID usando um modelo.
- `factory(Model::class)->create()`: Cria uma instância do modelo e a salva no banco de dados.

### Utilizando o Git

O Git é um sistema de controle de versão distribuído amplamente utilizado para gerenciar projetos de software. Aqui estão alguns comandos úteis do Git:

- `git init`: Inicia um novo repositório Git.
- `git clone <URL>`: Clona um repositório remoto para o seu ambiente local.
- `git add <arquivo>`: Adiciona um arquivo específico para o próximo commit.
- `git commit -m "<mensagem>"`: Cria um novo commit com os arquivos adicionados e uma mensagem descritiva.
- `git push`: Envia os commits locais para um repositório remoto.
- `git pull`: Obtém as atualizações mais recentes de um repositório remoto e mescla com o ramo atual.
- `git branch`: Lista todos os ramos disponíveis no repositório.
- `git checkout <ramo>`: Alterna para um ramo específico.
- `git merge <ramo>`: Mescla um ramo específico com o ramo atual.
- `git log`: Mostra o histórico de commits.

### Criando alias usando gitconfig

Você pode criar alias personalizados no Git para simplificar comandos frequentemente usados. Para adicionar um alias, siga estes passos:

1. Abra o arquivo de configuração global do Git com o seguinte comando:

```bash
git config --global --edit
```

2. No arquivo aberto, adicione os aliases desejados. Por exemplo:

```
[alias]
    co = checkout
    ci = commit
    st = status
```

3. Salve e feche o arquivo.

Agora você pode usar esses aliases para executar comandos Git mais rapidamente. Por exemplo, em vez de digitar `git commit`, você pode usar `git ci`.
