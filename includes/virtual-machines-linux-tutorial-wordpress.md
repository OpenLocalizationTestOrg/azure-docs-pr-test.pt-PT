## <a name="install-wordpress"></a><span data-ttu-id="203c7-101">Instalar o WordPress</span><span class="sxs-lookup"><span data-stu-id="203c7-101">Install WordPress</span></span>

<span data-ttu-id="203c7-102">Se quiser tootry da pilha, instale uma aplicação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="203c7-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="203c7-103">Por exemplo, os seguintes passos de Olá instalar open source para Olá [WordPress](https://wordpress.org/) plataforma toocreate sites e blogues.</span><span class="sxs-lookup"><span data-stu-id="203c7-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="203c7-104">Tootry outras cargas de trabalho incluem [Drupal](http://www.drupal.org) e [Moodle](https://moodle.org/).</span><span class="sxs-lookup"><span data-stu-id="203c7-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="203c7-105">Este programa de configuração do WordPress destina-se a prova de conceito.</span><span class="sxs-lookup"><span data-stu-id="203c7-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="203c7-106">Para obter mais informações e as definições de instalação de produção, consulte Olá [WordPress documentação](https://codex.wordpress.org/Main_Page).</span><span class="sxs-lookup"><span data-stu-id="203c7-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="203c7-107">Instalar o pacote do Olá WordPress</span><span class="sxs-lookup"><span data-stu-id="203c7-107">Install hello WordPress package</span></span>

<span data-ttu-id="203c7-108">Execute Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="203c7-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="203c7-109">Configurar WordPress</span><span class="sxs-lookup"><span data-stu-id="203c7-109">Configure WordPress</span></span>

<span data-ttu-id="203c7-110">Configure WordPress toouse MySQL e o PHP.</span><span class="sxs-lookup"><span data-stu-id="203c7-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="203c7-111">Executar Olá tooopen de comando a seguir um editor de texto à sua escolha e criar o ficheiro de Olá `/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="203c7-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="203c7-112">Olá cópia seguintes linhas toohello ficheiro, substituindo a palavra-passe de base de dados para *yourPassword* (mantenha outros valores inalterados).</span><span class="sxs-lookup"><span data-stu-id="203c7-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="203c7-113">Em seguida, guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="203c7-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="203c7-114">No diretório de trabalho, crie um ficheiro de texto `wordpress.sql` base de dados do tooconfigure Olá WordPress:</span><span class="sxs-lookup"><span data-stu-id="203c7-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="203c7-115">Adicionar Olá comandos a seguir, substituindo a palavra-passe de base de dados para *yourPassword* (mantenha outros valores inalterados).</span><span class="sxs-lookup"><span data-stu-id="203c7-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="203c7-116">Em seguida, guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="203c7-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="203c7-117">Execute Olá os seguintes comandos toocreate Olá da base de dados:</span><span class="sxs-lookup"><span data-stu-id="203c7-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="203c7-118">Após a conclusão do comando de Olá, elimine o ficheiro de Olá `wordpress.sql`.</span><span class="sxs-lookup"><span data-stu-id="203c7-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="203c7-119">Mova a raiz de documento ao servidor do web de toohello Olá WordPress instalação:</span><span class="sxs-lookup"><span data-stu-id="203c7-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="203c7-120">Agora pode concluir a configuração do WordPress Olá e publicar na plataforma de Olá.</span><span class="sxs-lookup"><span data-stu-id="203c7-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="203c7-121">Abra um browser e aceda demasiado`http://yourPublicIPAddress/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="203c7-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="203c7-122">Substitua o endereço IP público Olá da sua VM.</span><span class="sxs-lookup"><span data-stu-id="203c7-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="203c7-123">Deve ser semelhante toothis imagem.</span><span class="sxs-lookup"><span data-stu-id="203c7-123">It should look similar toothis image.</span></span>

![Página de instalação do WordPress](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)