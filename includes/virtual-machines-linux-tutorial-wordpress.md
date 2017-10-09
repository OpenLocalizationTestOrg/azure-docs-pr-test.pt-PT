## <a name="install-wordpress"></a>Instalar o WordPress

Se quiser tootry da pilha, instale uma aplicação de exemplo. Por exemplo, os seguintes passos de Olá instalar open source para Olá [WordPress](https://wordpress.org/) plataforma toocreate sites e blogues. Tootry outras cargas de trabalho incluem [Drupal](http://www.drupal.org) e [Moodle](https://moodle.org/). 

Este programa de configuração do WordPress destina-se a prova de conceito. Para obter mais informações e as definições de instalação de produção, consulte Olá [WordPress documentação](https://codex.wordpress.org/Main_Page). 



### <a name="install-hello-wordpress-package"></a>Instalar o pacote do Olá WordPress

Execute Olá os seguintes comandos:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>Configurar WordPress

Configure WordPress toouse MySQL e o PHP. Executar Olá tooopen de comando a seguir um editor de texto à sua escolha e criar o ficheiro de Olá `/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
Olá cópia seguintes linhas toohello ficheiro, substituindo a palavra-passe de base de dados para *yourPassword* (mantenha outros valores inalterados). Em seguida, guarde o ficheiro de Olá.

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

No diretório de trabalho, crie um ficheiro de texto `wordpress.sql` base de dados do tooconfigure Olá WordPress: 

```bash
sudo sensible-editor wordpress.sql
```

Adicionar Olá comandos a seguir, substituindo a palavra-passe de base de dados para *yourPassword* (mantenha outros valores inalterados). Em seguida, guarde o ficheiro de Olá.

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


Execute Olá os seguintes comandos toocreate Olá da base de dados:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Após a conclusão do comando de Olá, elimine o ficheiro de Olá `wordpress.sql`.

Mova a raiz de documento ao servidor do web de toohello Olá WordPress instalação:

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

Agora pode concluir a configuração do WordPress Olá e publicar na plataforma de Olá. Abra um browser e aceda demasiado`http://yourPublicIPAddress/wordpress`. Substitua o endereço IP público Olá da sua VM. Deve ser semelhante toothis imagem.

![Página de instalação do WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)