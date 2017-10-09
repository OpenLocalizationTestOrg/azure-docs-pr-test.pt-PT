---
title: "ambientes de DevOps aaaUse eficazmente para a sua aplicação web | Microsoft Docs"
description: "Saiba como implementação toouse ranhuras tooset configurar e gerir vários ambientes de desenvolvimento para a sua aplicação"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Utilizar eficazmente os ambientes de DevOps para as suas aplicações web
Este artigo mostra como tooset configurar e gerir as implementações de aplicações web, quando várias versões da aplicação são em vários ambientes, como o desenvolvimento, teste, garantia de qualidade (pergunta e resposta) e produção. Cada versão da aplicação pode ser considerado como ambiente de desenvolvimento para fim específico de Olá do processo de implementação. Por exemplo, os programadores podem utilizar Olá pergunta e resposta ambiente tootest Olá da qualidade da aplicação Olá antes de poderem push Olá tooproduction de alterações.
Vários ambientes de desenvolvimento podem ser um desafio porque necessita de código tootrack, gerir os recursos (cálculo, aplicação web, base de dados, cache, etc.) e implementar código entre ambientes.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Configurar um ambiente de não produção (fase, desenvolvimento, pergunta e resposta)
Depois de uma aplicação web de produção se encontra em execução, o passo seguinte Olá é toocreate um ambiente de não produção. toouse ranhuras de implementação, certifique-se de que está a executar no modo de plano de Olá Standard ou Premium do serviço de aplicações do Azure. As ranhuras de implementação são aplicações web em direto com os seus próprios nomes de anfitrião. Elementos de conteúdo e a configuração da aplicação Web podem ser trocados entre duas ranhuras de implementação, incluindo a ranhura de produção Olá. Quando implementa o bloco de implementação de tooa de aplicação, obter Olá seguintes vantagens:

- Pode validar a aplicação de web de tooa alterações numa ranhura de implementação de teste antes de comutação aplicação Olá ranhura de produção Olá.
- Quando implementar uma ranhura de tooa de aplicação web pela primeira vez e trocar-o em produção, todas as instâncias de ranhura Olá são preparadas antes de a ser alternados em produção. Este processo elimina o período de indisponibilidade quando implementar a aplicação web. redirecionamento de tráfego de Olá é totalmente integrado e não existem pedidos são ignorados devido a operações de tooswap. tooautomate este fluxo de trabalho completo, configurar [automática comutação](web-sites-staged-publishing.md#configure-auto-swap) quando a validação de pré-troca de não é necessária.
- Após uma troca a ranhura Olá que tem agora a aplicação web de Olá anteriormente testado tem Olá anterior aplicação de web de produção. Se as alterações de Olá alternadas na ranhura de produção Olá não tem o aspeto esperado, pode realizar Olá mesmo comutação imediatamente tooget sua "boa conhecida da última" back de aplicação web.

tooset se uma transição ranhura de implementação, consulte [configurar ambientes para web apps no App Service do Azure de teste](web-sites-staged-publishing.md). Cada ambiente deve incluir o seu próprio conjunto de recursos. Por exemplo, se a sua aplicação web utiliza uma base de dados, em seguida, produção e aplicações web de teste devem utilizar bases de dados diferentes. Adicione transição recursos de ambiente de desenvolvimento, tais como a base de dados, de armazenamento ou cache tooset o ambiente de desenvolvimento de teste.

## <a name="examples-of-using-multiple-development-environments"></a>Exemplos de como utilizar vários ambientes de desenvolvimento
Qualquer projeto deve seguir a gestão de código de origem com, pelo menos, dois ambientes: programação e produção. Se utilizar sistemas de gestão de conteúdo (CMSs), estruturas de aplicações, etc., aplicação Olá pode não suportar este cenário sem personalização. Este eventuality é verdadeiro para algumas das arquiteturas populares Olá e que são debatidas Olá secções a seguir. Muitas das perguntas vêm toomind quando trabalha com CMS/estruturas, tais como:

- Como interromper conteúdo Olá em ambientes diferentes?
- Que ficheiros pode alterar sem afetar as atualizações de versão do framework?
- Como gerir configurações por ambiente?
- Como gerir atualizações de versões de módulos, plug-ins e arquitetura de central Olá?

Existem muitas formas tooset segurança vários ambientes para o seu projeto. Olá exemplos seguintes mostram um método para cada aplicação correspondentes.

### <a name="wordpress"></a>WordPress
Nesta secção, ficará a saber como tooset configurar um fluxo de trabalho de implementação utilizando ranhuras para WordPress. WordPress, como a maioria das soluções CMS, não suporta vários ambientes de desenvolvimento sem personalização. funcionalidade de aplicações Web Olá do App Service do Azure tem algumas funcionalidades que tornam mais fácil toostore definições de configuração fora do seu código.

1. Antes de criar um bloco de transição, configure o toosupport de código da aplicação vários ambientes. toosupport vários ambientes WordPress, terá de tooedit `wp-config.php` no seu desenvolvimento local aplicação web e adicionar Olá seguinte código no início de Olá do ficheiro de Olá. Este processo irá ativar a sua aplicação toopick Olá configuração correto com base no ambiente selecionado Olá.

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. Crie uma pasta na raiz da aplicação de web chamado `config`e adicione Olá `wp-config.azure.php` e `wp-config.local.php` ficheiros, que representam o seu ambiente do Azure e o ambiente local, respetivamente.

3. Copie o seguinte Olá no `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Definir as chaves de segurança de Olá, conforme ilustrado no código anterior Olá pode ajudar tooprevent a sua aplicação web de que está a ser vítima de acesso ilícito, por isso, utilize valores exclusivos. Se precisar de cadeia de Olá toogenerate para chaves de segurança mencionadas no código Olá, pode [gerador automática toohello aceda](https://api.wordpress.org/secret-key/1.1/salt) toocreate nova chave/valor pares.

4. Cópia Olá seguinte código no `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>Utilizar caminhos relativos
Um tooconfigure coisa último na aplicação do WordPress Olá é caminhos relativos. WordPress armazena informações de URL na base de dados de Olá. Este tipo de armazenamento permite mover conteúdo a partir de um ambiente tooanother mais difícil. Terá tooupdate Olá da base de dados de cada vez move de local toostage ou ambientes de tooproduction fase. risco de Olá tooreduce dos problemas que pode dever-se com a implementação de uma base de dados sempre que implementar a partir de um ambiente tooanother, utilize Olá [relativo raiz liga Plug-in](https://wordpress.org/plugins/root-relative-urls/), que pode instalar utilizando o administrador do WordPress Olá dashboard.

Adicionar Olá seguir entradas tooyour `wp-config.php` ficheiro antes de Olá `That's all, stop editing!` comentário:

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Ativar o plug-in de Olá através de Olá `Plugins` menu no dashboard do WordPress administrador. Guarde as definições de permalink para aplicação WordPress.

#### <a name="hello-final-wp-configphp-file"></a>Olá final `wp-config.php` ficheiro
As atualizações de núcleo do WordPress não irão afetar o `wp-config.php`, `wp-config.azure.php`, e `wp-config.local.php` ficheiros. Eis uma versão final do Olá `wp-config.php` ficheiro:

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Configurar um ambiente de teste
1. Se já tiver uma aplicação web do WordPress em execução na sua subscrição do Azure, inicie sessão no toohello [portal do Azure](http://portal.azure.com), e, em seguida, aceda a aplicação de web do WordPress tooyour. Se não tiver uma aplicação web WordPress, pode criar um Olá Azure Marketplace. toolearn mais, consulte [criar uma aplicação web WordPress no App Service do Azure](web-sites-php-web-site-gallery.md).
Clique em **definições** > **ranhuras de implementação** > **adicionar** toocreate uma ranhura de implementação com o nome de Olá *fase*. Um bloco de implementação é outra aplicação web que partilhas Olá mesmos recursos que a aplicação de web primário Olá que criou anteriormente.

    ![Criar a ranhura de implementação de fase](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Adicionar outra base de dados MySQL, diga `wordpress-stage-db`, grupo de recursos de tooyour `wordpressapp-group`.

    ![Adicionar grupo de tooresource de base de dados MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Atualizar as cadeias de ligação de Olá da fase implementação ranhura toopoint toohello nova base de dados, `wordpress-stage-db`. A aplicação web de produção, `wordpressprodapp`e a aplicação web, de transição `wordpressprodapp-stage`, bases de dados do tem toodifferent ponto.

#### <a name="configure-environment-specific-app-settings"></a>Configurar as definições de aplicação específico do ambiente
Os programadores podem armazenar pares de cadeia de chave/valor no Azure como parte das informações de configuração de Olá, denominadas **as definições de aplicação**, que está associada a uma aplicação web. Em runtime, as aplicações web automaticamente obtêm estes valores e torná-los toocode disponível que está a ser executado na sua aplicação web. Numa perspetiva de segurança, que é uma vantagem lado nice porque informações confidenciais, tais como cadeias de ligação de base de dados que incluem palavras-passe, nunca apresentados como texto não encriptado num ficheiro, tal como `wp-config.php`.

Este processo, o que é explicado na Olá parágrafos a seguir, é útil porque inclui as alterações ao ficheiro e as alterações de base de dados para a aplicação de WordPress Olá:

* Atualização de versão do WordPress
* Adicionar novos, editar ou atualizar o plug-ins
* Adicionar novos, editar ou atualizar temas

Configure definições de aplicação para:

* Informações de base de dados
* Ativar/desativar o registo do WordPress
* Definições de segurança do WordPress

![Definições de aplicação para a aplicação web do Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Certifique-se de que adiciona Olá seguintes definições de aplicação para a ranhura de aplicação e fase da web de produção. Tenha em atenção que Olá produção web app e o teste de web de aplicação utilizam bases de dados diferentes.

1. Limpar Olá **ranhura definição** caixa de verificação para todos os parâmetros de definições de Olá, exceto WP_ENV. Este processo irá comutação configuração Olá para a sua aplicação web, o conteúdo do ficheiro e a base de dados. Se **ranhura definição** é a opção estiver marcada, as definições de aplicação e a configuração da cadeia de ligação da aplicação web Olá serão *não* mover entre ambientes ao efetuar uma **comutação** operação. Quaisquer alterações de base de dados que estão presentes não irão interromper a sua aplicação web de produção.

2. Implemente Olá desenvolvimento local ambiente web app toohello fase aplicação web e a base de dados ao utilizar o WebMatrix ou ferramentas da sua escolha, por exemplo, FTP, Git ou PhpMyAdmin.

    ![Web Matrix publicar caixa de diálogo de aplicação web do WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Procurar e testar a aplicação de web de transição. Tendo em consideração um cenário em que o tema Olá da aplicação web de Olá é toobe atualizada, eis Olá aplicação web de transição.

    ![Procure a aplicação web antes de troca de ranhuras de teste](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Se todos os procura boa, clique em Olá **comutação** botão no seu toomove de aplicação web transição ambiente de produção toohello conteúdo. Neste caso, trocar o Olá web app e a base de dados de Olá em ambientes durante cada **troca** operação.

    ![Pré-visualizar alterações de comutação para WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Se o seu cenário necessitar de ficheiros de push tooonly (sem as atualizações da base de dados), em seguida, verifique **ranhura definição** para todos os Olá relacionadas com a base de dados *as definições de aplicação* e *cadeias de ligação definições*no Olá **definições da aplicação Web** painel dentro Olá portal do Azure antes de efetuar Olá **comutação**. Neste caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER e predefinições da cadeia de ligação devem aparecer na pré-visualizar alterações quando o fizer uma **comutação**. Neste momento, quando concluir Olá **comutação** operação, Olá aplicação web do WordPress que irá ter Olá atualiza apenas ficheiros.
    >
    >

    Antes de fazer um **comutação**, segue-se a aplicação de web do WordPress Olá produção.
    ![Aplicação web de produção antes de troca de ranhuras](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Depois de Olá **comutação** operação, tema Olá tiver sido atualizada na sua aplicação web de produção.

    ![Aplicação web de produção após a troca de ranhuras](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Quando precisar de tooroll anterior, pode aceder web de produção toohello **as definições de aplicação**e clique em Olá **comutação** botão tooswap Olá web app e a base de dados a partir da ranhura de toostaging de produção. Lembre-se de que se as alterações de base de dados estão incluídas com um **comutação** operação, em seguida, Olá próxima vez que implementar tooyour teste a aplicação web, terá de toodeploy Olá alterações toohello atual base de dados para a sua aplicação de web de transição. base de dados atual Olá poderão Olá anterior produção ou Olá fase base de dados.

#### <a name="summary"></a>Resumo
Segue-se um processo generalizado para qualquer aplicação que tenha uma base de dados:

1. Instale aplicação Olá no ambiente local.
2. Inclua específico do ambiente configurações (local e do Azure as Web Apps).
3. Configure os seus ambientes de teste e produção para aplicações Web.
4. Se tiver uma aplicação de produção já em execução no Azure, sincronizar o seu conteúdos (ficheiros/código e base de dados) toolocal e transição ambientes de produção.
5. Desenvolva a sua aplicação no seu ambiente local.
6. Colocar a sua aplicação web de produção em manutenção ou modo bloqueado e sincronizar o conteúdo da base de dados de ambientes de produção toostaging e desenvolvimento.
7. Implemente toohello teste e de ambiente de teste.
8. Implemente tooproduction ambiente.
9. Repita os passos 4 a 6.

### <a name="umbraco"></a>Umbraco
Nesta secção, ficará a saber como Olá Umbraco CMS utiliza um módulo personalizado toodeploy pelos vários ambientes de DevOps. Neste exemplo fornece uma abordagem diferente toomanaging vários ambientes de desenvolvimento.

[Umbraco CMS](http://umbraco.com/) é uma solução de .NET CMS popular, que é utilizada pelos programadores muitos. Fornece Olá [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy do módulo de ambientes de tooproduction toostaging de desenvolvimento. Pode facilmente criar um ambiente de desenvolvimento local para uma aplicação de web Umbraco CMS utilizando o Visual Studio ou o WebMatrix.

- [Criar uma aplicação de web Umbraco com o Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Criar uma aplicação de web Umbraco com o WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

Memorizar sempre tooremove Olá `install` pasta na sua aplicação e carregá-la nunca toostage ou de produção as web apps. Este tutorial utiliza o WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Configurar um ambiente de teste
1. Crie uma ranhura de implementação, tal como mencionado anteriormente para Olá Umbraco CMS web app, partindo do princípio que já tem uma aplicação de web Umbraco CMS cópias de segurança e em execução. Se não o fizer, pode criar um Olá Marketplace.
2. Atualizar a cadeia de ligação de Olá para a fase implementação ranhura toopoint toohello novo **umbraco-fase-db** base de dados. A aplicação de web de produção (umbraositecms-1) e o teste web app (umbracositecms-1-fase) *tem* toodifferent de ponto de bases de dados.

    ![Atualizar a cadeia de ligação para a aplicação web com a nova base de dados de teste de teste](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Clique em **definições de publicação obter** para a ranhura de implementação de Olá **fase**. Este processo irá transferir um ficheiro de definições de publicação que armazena todas as informações de Olá que Visual Studio ou o WebMatrix requer toopublish a aplicação da aplicação web do Azure de toohello aplicação Olá desenvolvimento local web.

    ![Obter publicar a definição de aplicação web de transição de Olá](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Abra a aplicação web de desenvolvimento local no WebMatrix ou Visual Studio. Este tutorial utiliza o WebMatrix. Em primeiro lugar, precisa de tooimport Olá publicar o ficheiro de definições para a sua aplicação de web de transição.

    ![Importar definições de publicação para Umbraco utilizando a Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Rever as alterações na caixa de diálogo Olá e implementar a sua aplicação web do Azure tooyour aplicação de local web, *umbracositecms-1-fase*. Ao implementar os ficheiros diretamente a aplicação web de transição de tooyour, omite ficheiros Olá `~/app_data/TEMP/` pasta porque estes ficheiros serão gerados novamente quando a aplicação de web de fase de Olá é o primeira foi iniciado. Também deve omitir Olá `~/app_data/umbraco.config` ficheiro, que também será regenerado.

    ![Reveja a publicar alterações na matriz da web](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Depois de publicar Olá Umbraco local aplicação toohello teste web aplicação web com êxito, procure a aplicação de web de transição tooyour e execute alguns testes toorule eventuais problemas.

#### <a name="set-up-hello-courier2-deployment-module"></a>Configurar o módulo de implementação de Courier2 Olá
Com Olá [Courier2](http://umbraco.com/products/more-add-ons/courier-2) módulo, pode simplesmente com o botão direito toopush conteúdo, folhas de estilo e módulos de desenvolvimento de um teste web app tooa produção aplicação web. Este processo reduz o risco de Olá de interrompendo a sua aplicação web de produção quando implementar uma atualização.
Adquirir uma licença do Courier2 para Olá `*.azurewebsites.net` domínio e o domínio personalizado (diga http://abc.com). Depois de comprar licenças de Olá, local Olá transferido licença (. Ficheiro LIC) no Olá `bin` pasta.

![Remova o ficheiro de licença na pasta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Transferir o pacote de Olá Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Inicie sessão na aplicação de web de fase tooyour, diga http://umbracocms-site-stage.azurewebsites.net/umbraco, clique em Olá **programador** e, em seguida, clique em **pacotes** > **instalar pacote local**.

    ![Instalador do pacote de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Carregar o pacote de Olá Courier2 utilizando o instalador Olá.

    ![Carregar o pacote para o módulo de courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. pacote de Olá tooconfigure, é necessário que o ficheiro de courier.config de Olá tooupdate em Olá **configuração** pasta da sua aplicação web.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. Em `<repositories>`, introduza Olá produção URL e o utilizador as informações de site.
    Se estiver a utilizar o fornecedor de membros Umbraco Olá predefinido, em seguida, adicione Olá ID de utilizador de administração de Olá no Olá &lt;utilizador&gt; secção.
    Se estiver a utilizar um fornecedor de associação Umbraco personalizado, utilize `<login>`,`<password>` no site de produção do Olá Courier2 módulo tooconnect toohello.
    Para obter mais detalhes, [consultar a documentação de Olá para o módulo Olá Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. Da mesma forma, instale o módulo de Courier2 Olá no seu site de produção e configure-a aplicação web do toopoint toohello fase no respetivo ficheiro courier.config respetivos conforme mostrado aqui.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Clique em Olá **Courier2** separador Olá dashboard de aplicações web Umbraco CMS e, em seguida, clique em **localizações**. Deverá ver o nome do repositório Olá tal como mencionado na `courier.config`. Efetue este processo nas suas produção e o teste web apps.

    ![Repositório de aplicação de web de destino de vista](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. toodeploy conteúdo do site de produção toohello de site, de transição de Olá aceda demasiado**conteúdo**e selecione uma página existente ou crie uma nova página. Posso irá selecionar uma página existente da minha aplicação web em que é o título de Olá da página Olá **introdução – novo**e, em seguida, clique em **guardar e publicar**.

    ![Alterar o título da página e publicar](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Contexto Olá modificado página tooview todas as opções de Olá. Clique em **Courier** tooopen Olá **implementação** caixa de diálogo. Clique em **implementar** tooinitiate implementação.

    ![Caixa de diálogo de implementação de módulo de Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Rever as alterações de Olá e, em seguida, clique em **continuar**.

    ![Alterações de revisão de caixa de diálogo de implementação de módulo de Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    registo da implementação Olá mostra se a implementação de Olá foi concluída com êxito.

     ![Ver registos de implementação do módulo de Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Procure o toosee de aplicação de web de produção se as alterações de Olá são refletidas.

     ![Procure a aplicação web de produção](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

toolearn mais informações sobre como toouse Courier, reveja Olá documentação.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Como tooupgrade Olá versão Umbraco CMS
Irá Courier não atualizar de uma versão do Umbraco CMS tooanother de ajuda. Ao atualizar uma versão de Umbraco CMS, tem de verificar a existência de incompatibilidades com os módulos personalizados ou os módulos de parceiros e Olá bibliotecas Umbraco principais. Seguem-se as melhores práticas:

* Sempre efetuar uma cópia de segurança de aplicação web e a base de dados antes de atualizar. Nas aplicações web no Azure, pode configurar cópias de segurança automáticas para os Web sites utilizando a funcionalidade de cópia de segurança de Olá e restaurar o seu site se for necessário, utilizando a funcionalidade de restauro Olá. Para obter mais detalhes, consulte [como tooback verticalmente a sua aplicação web](web-sites-backup.md) e [como toorestore a aplicação web](web-sites-restore.md).
* Verifique se os pacotes de parceiros estão compatíveis com a versão de Olá que estiver a atualizar a. Página de transferência no pacote de Olá, reveja Olá projeto de compatibilidade com a versão de Umbraco CMS.

Para obter mais detalhes sobre como tooupgrade a aplicação web localmente, [Consulte Olá geral atualização orientação](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Depois de atualizar o seu site de desenvolvimento local, publica Olá alterações toohello aplicação web de transição. Teste a aplicação. Se todos os procura boa, utilize Olá **comutação** botão tooswap a aplicação de web de produção de toohello do teste site. Quando utiliza Olá **comutação** operação, pode ver as alterações de Olá que vai ser afetadas na configuração da sua aplicação web. Isto **comutação** operação trocas Olá web apps e bases de dados. Depois de Olá **comutação**, Olá produção web aplicação será ponto toohello umbraco-fase-db da base de dados e Olá base de dados do teste web aplicação será ponto tooumbraco-prod-db.

![Pré-visualização de comutação para implementar Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Seguem-se as vantagens de troca de aplicação web de Olá e base de dados de Olá:

* Pode reverter toohello versão anterior da aplicação web com outra **comutação** se houver algum problema de aplicação.
* Para uma atualização, terá de toodeploy ficheiros e de bases de dados de aplicação de web de produção de toohello aplicação web de transição de Olá e de base de dados. Inúmeros aspetos podem correrem mal quando implementar os ficheiros e as bases de dados. Ao utilizar Olá **comutação** funcionalidade de ranhuras, iremos pode reduzir o período de indisponibilidade durante a atualização e reduzir o risco de Olá de falhas que podem ocorrer ao implementar alterações.
* Pode fazê-lo **um teste a / B** utilizando Olá [teste em produção](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funcionalidade.

Este exemplo mostra Olá flexibilidade de plataforma olá onde pode criar módulos personalizados semelhante implementação de toomanage do módulo Courier tooUmbraco entre ambientes.

## <a name="references"></a>Referências
[Desenvolvimento de software seja ágil App Service do Azure](app-service-agile-software-development.md)

[Configurar ambientes para web apps no App Service do Azure de teste](web-sites-staged-publishing.md)

[Como tooblock web aceder às ranhuras de implementação de produção toonon](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
