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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="7fbf0-103">Utilizar eficazmente os ambientes de DevOps para as suas aplicações web</span><span class="sxs-lookup"><span data-stu-id="7fbf0-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="7fbf0-104">Este artigo mostra como tooset configurar e gerir as implementações de aplicações web, quando várias versões da aplicação são em vários ambientes, como o desenvolvimento, teste, garantia de qualidade (pergunta e resposta) e produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="7fbf0-105">Cada versão da aplicação pode ser considerado como ambiente de desenvolvimento para fim específico de Olá do processo de implementação.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="7fbf0-106">Por exemplo, os programadores podem utilizar Olá pergunta e resposta ambiente tootest Olá da qualidade da aplicação Olá antes de poderem push Olá tooproduction de alterações.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="7fbf0-107">Vários ambientes de desenvolvimento podem ser um desafio porque necessita de código tootrack, gerir os recursos (cálculo, aplicação web, base de dados, cache, etc.) e implementar código entre ambientes.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="7fbf0-108">Configurar um ambiente de não produção (fase, desenvolvimento, pergunta e resposta)</span><span class="sxs-lookup"><span data-stu-id="7fbf0-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="7fbf0-109">Depois de uma aplicação web de produção se encontra em execução, o passo seguinte Olá é toocreate um ambiente de não produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="7fbf0-110">toouse ranhuras de implementação, certifique-se de que está a executar no modo de plano de Olá Standard ou Premium do serviço de aplicações do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="7fbf0-111">As ranhuras de implementação são aplicações web em direto com os seus próprios nomes de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="7fbf0-112">Elementos de conteúdo e a configuração da aplicação Web podem ser trocados entre duas ranhuras de implementação, incluindo a ranhura de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="7fbf0-113">Quando implementa o bloco de implementação de tooa de aplicação, obter Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="7fbf0-114">Pode validar a aplicação de web de tooa alterações numa ranhura de implementação de teste antes de comutação aplicação Olá ranhura de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="7fbf0-115">Quando implementar uma ranhura de tooa de aplicação web pela primeira vez e trocar-o em produção, todas as instâncias de ranhura Olá são preparadas antes de a ser alternados em produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="7fbf0-116">Este processo elimina o período de indisponibilidade quando implementar a aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="7fbf0-117">redirecionamento de tráfego de Olá é totalmente integrado e não existem pedidos são ignorados devido a operações de tooswap.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="7fbf0-118">tooautomate este fluxo de trabalho completo, configurar [automática comutação](web-sites-staged-publishing.md#configure-auto-swap) quando a validação de pré-troca de não é necessária.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="7fbf0-119">Após uma troca a ranhura Olá que tem agora a aplicação web de Olá anteriormente testado tem Olá anterior aplicação de web de produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="7fbf0-120">Se as alterações de Olá alternadas na ranhura de produção Olá não tem o aspeto esperado, pode realizar Olá mesmo comutação imediatamente tooget sua "boa conhecida da última" back de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="7fbf0-121">tooset se uma transição ranhura de implementação, consulte [configurar ambientes para web apps no App Service do Azure de teste](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="7fbf0-122">Cada ambiente deve incluir o seu próprio conjunto de recursos.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="7fbf0-123">Por exemplo, se a sua aplicação web utiliza uma base de dados, em seguida, produção e aplicações web de teste devem utilizar bases de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="7fbf0-124">Adicione transição recursos de ambiente de desenvolvimento, tais como a base de dados, de armazenamento ou cache tooset o ambiente de desenvolvimento de teste.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="7fbf0-125">Exemplos de como utilizar vários ambientes de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="7fbf0-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="7fbf0-126">Qualquer projeto deve seguir a gestão de código de origem com, pelo menos, dois ambientes: programação e produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="7fbf0-127">Se utilizar sistemas de gestão de conteúdo (CMSs), estruturas de aplicações, etc., aplicação Olá pode não suportar este cenário sem personalização.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="7fbf0-128">Este eventuality é verdadeiro para algumas das arquiteturas populares Olá e que são debatidas Olá secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="7fbf0-129">Muitas das perguntas vêm toomind quando trabalha com CMS/estruturas, tais como:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="7fbf0-130">Como interromper conteúdo Olá em ambientes diferentes?</span><span class="sxs-lookup"><span data-stu-id="7fbf0-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="7fbf0-131">Que ficheiros pode alterar sem afetar as atualizações de versão do framework?</span><span class="sxs-lookup"><span data-stu-id="7fbf0-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="7fbf0-132">Como gerir configurações por ambiente?</span><span class="sxs-lookup"><span data-stu-id="7fbf0-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="7fbf0-133">Como gerir atualizações de versões de módulos, plug-ins e arquitetura de central Olá?</span><span class="sxs-lookup"><span data-stu-id="7fbf0-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="7fbf0-134">Existem muitas formas tooset segurança vários ambientes para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="7fbf0-135">Olá exemplos seguintes mostram um método para cada aplicação correspondentes.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="7fbf0-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="7fbf0-136">WordPress</span></span>
<span data-ttu-id="7fbf0-137">Nesta secção, ficará a saber como tooset configurar um fluxo de trabalho de implementação utilizando ranhuras para WordPress.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="7fbf0-138">WordPress, como a maioria das soluções CMS, não suporta vários ambientes de desenvolvimento sem personalização.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="7fbf0-139">funcionalidade de aplicações Web Olá do App Service do Azure tem algumas funcionalidades que tornam mais fácil toostore definições de configuração fora do seu código.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="7fbf0-140">Antes de criar um bloco de transição, configure o toosupport de código da aplicação vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="7fbf0-141">toosupport vários ambientes WordPress, terá de tooedit `wp-config.php` no seu desenvolvimento local aplicação web e adicionar Olá seguinte código no início de Olá do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="7fbf0-142">Este processo irá ativar a sua aplicação toopick Olá configuração correto com base no ambiente selecionado Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="7fbf0-143">Crie uma pasta na raiz da aplicação de web chamado `config`e adicione Olá `wp-config.azure.php` e `wp-config.local.php` ficheiros, que representam o seu ambiente do Azure e o ambiente local, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="7fbf0-144">Copie o seguinte Olá no `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="7fbf0-145">Definir as chaves de segurança de Olá, conforme ilustrado no código anterior Olá pode ajudar tooprevent a sua aplicação web de que está a ser vítima de acesso ilícito, por isso, utilize valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="7fbf0-146">Se precisar de cadeia de Olá toogenerate para chaves de segurança mencionadas no código Olá, pode [gerador automática toohello aceda](https://api.wordpress.org/secret-key/1.1/salt) toocreate nova chave/valor pares.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="7fbf0-147">Cópia Olá seguinte código no `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="7fbf0-148">Utilizar caminhos relativos</span><span class="sxs-lookup"><span data-stu-id="7fbf0-148">Use relative paths</span></span>
<span data-ttu-id="7fbf0-149">Um tooconfigure coisa último na aplicação do WordPress Olá é caminhos relativos.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="7fbf0-150">WordPress armazena informações de URL na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="7fbf0-151">Este tipo de armazenamento permite mover conteúdo a partir de um ambiente tooanother mais difícil.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="7fbf0-152">Terá tooupdate Olá da base de dados de cada vez move de local toostage ou ambientes de tooproduction fase.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="7fbf0-153">risco de Olá tooreduce dos problemas que pode dever-se com a implementação de uma base de dados sempre que implementar a partir de um ambiente tooanother, utilize Olá [relativo raiz liga Plug-in](https://wordpress.org/plugins/root-relative-urls/), que pode instalar utilizando o administrador do WordPress Olá dashboard.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="7fbf0-154">Adicionar Olá seguir entradas tooyour `wp-config.php` ficheiro antes de Olá `That's all, stop editing!` comentário:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="7fbf0-155">Ativar o plug-in de Olá através de Olá `Plugins` menu no dashboard do WordPress administrador.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="7fbf0-156">Guarde as definições de permalink para aplicação WordPress.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="7fbf0-157">Olá final `wp-config.php` ficheiro</span><span class="sxs-lookup"><span data-stu-id="7fbf0-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="7fbf0-158">As atualizações de núcleo do WordPress não irão afetar o `wp-config.php`, `wp-config.azure.php`, e `wp-config.local.php` ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="7fbf0-159">Eis uma versão final do Olá `wp-config.php` ficheiro:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="7fbf0-160">Configurar um ambiente de teste</span><span class="sxs-lookup"><span data-stu-id="7fbf0-160">Set up a staging environment</span></span>
1. <span data-ttu-id="7fbf0-161">Se já tiver uma aplicação web do WordPress em execução na sua subscrição do Azure, inicie sessão no toohello [portal do Azure](http://portal.azure.com), e, em seguida, aceda a aplicação de web do WordPress tooyour.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="7fbf0-162">Se não tiver uma aplicação web WordPress, pode criar um Olá Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="7fbf0-163">toolearn mais, consulte [criar uma aplicação web WordPress no App Service do Azure](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="7fbf0-164">Clique em **definições** > **ranhuras de implementação** > **adicionar** toocreate uma ranhura de implementação com o nome de Olá *fase*.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="7fbf0-165">Um bloco de implementação é outra aplicação web que partilhas Olá mesmos recursos que a aplicação de web primário Olá que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Criar a ranhura de implementação de fase](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="7fbf0-167">Adicionar outra base de dados MySQL, diga `wordpress-stage-db`, grupo de recursos de tooyour `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![Adicionar grupo de tooresource de base de dados MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="7fbf0-169">Atualizar as cadeias de ligação de Olá da fase implementação ranhura toopoint toohello nova base de dados, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="7fbf0-170">A aplicação web de produção, `wordpressprodapp`e a aplicação web, de transição `wordpressprodapp-stage`, bases de dados do tem toodifferent ponto.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="7fbf0-171">Configurar as definições de aplicação específico do ambiente</span><span class="sxs-lookup"><span data-stu-id="7fbf0-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="7fbf0-172">Os programadores podem armazenar pares de cadeia de chave/valor no Azure como parte das informações de configuração de Olá, denominadas **as definições de aplicação**, que está associada a uma aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="7fbf0-173">Em runtime, as aplicações web automaticamente obtêm estes valores e torná-los toocode disponível que está a ser executado na sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="7fbf0-174">Numa perspetiva de segurança, que é uma vantagem lado nice porque informações confidenciais, tais como cadeias de ligação de base de dados que incluem palavras-passe, nunca apresentados como texto não encriptado num ficheiro, tal como `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="7fbf0-175">Este processo, o que é explicado na Olá parágrafos a seguir, é útil porque inclui as alterações ao ficheiro e as alterações de base de dados para a aplicação de WordPress Olá:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="7fbf0-176">Atualização de versão do WordPress</span><span class="sxs-lookup"><span data-stu-id="7fbf0-176">WordPress version upgrade</span></span>
* <span data-ttu-id="7fbf0-177">Adicionar novos, editar ou atualizar o plug-ins</span><span class="sxs-lookup"><span data-stu-id="7fbf0-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="7fbf0-178">Adicionar novos, editar ou atualizar temas</span><span class="sxs-lookup"><span data-stu-id="7fbf0-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="7fbf0-179">Configure definições de aplicação para:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-179">Configure app settings for:</span></span>

* <span data-ttu-id="7fbf0-180">Informações de base de dados</span><span class="sxs-lookup"><span data-stu-id="7fbf0-180">Database information</span></span>
* <span data-ttu-id="7fbf0-181">Ativar/desativar o registo do WordPress</span><span class="sxs-lookup"><span data-stu-id="7fbf0-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="7fbf0-182">Definições de segurança do WordPress</span><span class="sxs-lookup"><span data-stu-id="7fbf0-182">WordPress security settings</span></span>

![Definições de aplicação para a aplicação web do Wordpress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="7fbf0-184">Certifique-se de que adiciona Olá seguintes definições de aplicação para a ranhura de aplicação e fase da web de produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="7fbf0-185">Tenha em atenção que Olá produção web app e o teste de web de aplicação utilizam bases de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="7fbf0-186">Limpar Olá **ranhura definição** caixa de verificação para todos os parâmetros de definições de Olá, exceto WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="7fbf0-187">Este processo irá comutação configuração Olá para a sua aplicação web, o conteúdo do ficheiro e a base de dados.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="7fbf0-188">Se **ranhura definição** é a opção estiver marcada, as definições de aplicação e a configuração da cadeia de ligação da aplicação web Olá serão *não* mover entre ambientes ao efetuar uma **comutação** operação.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="7fbf0-189">Quaisquer alterações de base de dados que estão presentes não irão interromper a sua aplicação web de produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="7fbf0-190">Implemente Olá desenvolvimento local ambiente web app toohello fase aplicação web e a base de dados ao utilizar o WebMatrix ou ferramentas da sua escolha, por exemplo, FTP, Git ou PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Web Matrix publicar caixa de diálogo de aplicação web do WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="7fbf0-192">Procurar e testar a aplicação de web de transição.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-192">Browse and test your staging web app.</span></span> <span data-ttu-id="7fbf0-193">Tendo em consideração um cenário em que o tema Olá da aplicação web de Olá é toobe atualizada, eis Olá aplicação web de transição.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Procure a aplicação web antes de troca de ranhuras de teste](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="7fbf0-195">Se todos os procura boa, clique em Olá **comutação** botão no seu toomove de aplicação web transição ambiente de produção toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="7fbf0-196">Neste caso, trocar o Olá web app e a base de dados de Olá em ambientes durante cada **troca** operação.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Pré-visualizar alterações de comutação para WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="7fbf0-198">Se o seu cenário necessitar de ficheiros de push tooonly (sem as atualizações da base de dados), em seguida, verifique **ranhura definição** para todos os Olá relacionadas com a base de dados *as definições de aplicação* e *cadeias de ligação definições*no Olá **definições da aplicação Web** painel dentro Olá portal do Azure antes de efetuar Olá **comutação**.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="7fbf0-199">Neste caso, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER e predefinições da cadeia de ligação devem aparecer na pré-visualizar alterações quando o fizer uma **comutação**.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="7fbf0-200">Neste momento, quando concluir Olá **comutação** operação, Olá aplicação web do WordPress que irá ter Olá atualiza apenas ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="7fbf0-201">Antes de fazer um **comutação**, segue-se a aplicação de web do WordPress Olá produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="7fbf0-202">![Aplicação web de produção antes de troca de ranhuras](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="7fbf0-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="7fbf0-203">Depois de Olá **comutação** operação, tema Olá tiver sido atualizada na sua aplicação web de produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Aplicação web de produção após a troca de ranhuras](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="7fbf0-205">Quando precisar de tooroll anterior, pode aceder web de produção toohello **as definições de aplicação**e clique em Olá **comutação** botão tooswap Olá web app e a base de dados a partir da ranhura de toostaging de produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="7fbf0-206">Lembre-se de que se as alterações de base de dados estão incluídas com um **comutação** operação, em seguida, Olá próxima vez que implementar tooyour teste a aplicação web, terá de toodeploy Olá alterações toohello atual base de dados para a sua aplicação de web de transição.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="7fbf0-207">base de dados atual Olá poderão Olá anterior produção ou Olá fase base de dados.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="7fbf0-208">Resumo</span><span class="sxs-lookup"><span data-stu-id="7fbf0-208">Summary</span></span>
<span data-ttu-id="7fbf0-209">Segue-se um processo generalizado para qualquer aplicação que tenha uma base de dados:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="7fbf0-210">Instale aplicação Olá no ambiente local.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="7fbf0-211">Inclua específico do ambiente configurações (local e do Azure as Web Apps).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="7fbf0-212">Configure os seus ambientes de teste e produção para aplicações Web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="7fbf0-213">Se tiver uma aplicação de produção já em execução no Azure, sincronizar o seu conteúdos (ficheiros/código e base de dados) toolocal e transição ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="7fbf0-214">Desenvolva a sua aplicação no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="7fbf0-215">Colocar a sua aplicação web de produção em manutenção ou modo bloqueado e sincronizar o conteúdo da base de dados de ambientes de produção toostaging e desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="7fbf0-216">Implemente toohello teste e de ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="7fbf0-217">Implemente tooproduction ambiente.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="7fbf0-218">Repita os passos 4 a 6.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="7fbf0-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="7fbf0-219">Umbraco</span></span>
<span data-ttu-id="7fbf0-220">Nesta secção, ficará a saber como Olá Umbraco CMS utiliza um módulo personalizado toodeploy pelos vários ambientes de DevOps.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="7fbf0-221">Neste exemplo fornece uma abordagem diferente toomanaging vários ambientes de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="7fbf0-222">[Umbraco CMS](http://umbraco.com/) é uma solução de .NET CMS popular, que é utilizada pelos programadores muitos.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="7fbf0-223">Fornece Olá [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy do módulo de ambientes de tooproduction toostaging de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="7fbf0-224">Pode facilmente criar um ambiente de desenvolvimento local para uma aplicação de web Umbraco CMS utilizando o Visual Studio ou o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="7fbf0-225">Criar uma aplicação de web Umbraco com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7fbf0-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="7fbf0-226">Criar uma aplicação de web Umbraco com o WebMatrix</span><span class="sxs-lookup"><span data-stu-id="7fbf0-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="7fbf0-227">Memorizar sempre tooremove Olá `install` pasta na sua aplicação e carregá-la nunca toostage ou de produção as web apps.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="7fbf0-228">Este tutorial utiliza o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="7fbf0-229">Configurar um ambiente de teste</span><span class="sxs-lookup"><span data-stu-id="7fbf0-229">Set up a staging environment</span></span>
1. <span data-ttu-id="7fbf0-230">Crie uma ranhura de implementação, tal como mencionado anteriormente para Olá Umbraco CMS web app, partindo do princípio que já tem uma aplicação de web Umbraco CMS cópias de segurança e em execução.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="7fbf0-231">Se não o fizer, pode criar um Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="7fbf0-232">Atualizar a cadeia de ligação de Olá para a fase implementação ranhura toopoint toohello novo **umbraco-fase-db** base de dados.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="7fbf0-233">A aplicação de web de produção (umbraositecms-1) e o teste web app (umbracositecms-1-fase) *tem* toodifferent de ponto de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Atualizar a cadeia de ligação para a aplicação web com a nova base de dados de teste de teste](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="7fbf0-235">Clique em **definições de publicação obter** para a ranhura de implementação de Olá **fase**.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="7fbf0-236">Este processo irá transferir um ficheiro de definições de publicação que armazena todas as informações de Olá que Visual Studio ou o WebMatrix requer toopublish a aplicação da aplicação web do Azure de toohello aplicação Olá desenvolvimento local web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Obter publicar a definição de aplicação web de transição de Olá](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="7fbf0-238">Abra a aplicação web de desenvolvimento local no WebMatrix ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="7fbf0-239">Este tutorial utiliza o WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="7fbf0-240">Em primeiro lugar, precisa de tooimport Olá publicar o ficheiro de definições para a sua aplicação de web de transição.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Importar definições de publicação para Umbraco utilizando a Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="7fbf0-242">Rever as alterações na caixa de diálogo Olá e implementar a sua aplicação web do Azure tooyour aplicação de local web, *umbracositecms-1-fase*.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="7fbf0-243">Ao implementar os ficheiros diretamente a aplicação web de transição de tooyour, omite ficheiros Olá `~/app_data/TEMP/` pasta porque estes ficheiros serão gerados novamente quando a aplicação de web de fase de Olá é o primeira foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="7fbf0-244">Também deve omitir Olá `~/app_data/umbraco.config` ficheiro, que também será regenerado.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Reveja a publicar alterações na matriz da web](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="7fbf0-246">Depois de publicar Olá Umbraco local aplicação toohello teste web aplicação web com êxito, procure a aplicação de web de transição tooyour e execute alguns testes toorule eventuais problemas.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="7fbf0-247">Configurar o módulo de implementação de Courier2 Olá</span><span class="sxs-lookup"><span data-stu-id="7fbf0-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="7fbf0-248">Com Olá [Courier2](http://umbraco.com/products/more-add-ons/courier-2) módulo, pode simplesmente com o botão direito toopush conteúdo, folhas de estilo e módulos de desenvolvimento de um teste web app tooa produção aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="7fbf0-249">Este processo reduz o risco de Olá de interrompendo a sua aplicação web de produção quando implementar uma atualização.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="7fbf0-250">Adquirir uma licença do Courier2 para Olá `*.azurewebsites.net` domínio e o domínio personalizado (diga http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="7fbf0-251">Depois de comprar licenças de Olá, local Olá transferido licença (. Ficheiro LIC) no Olá `bin` pasta.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Remova o ficheiro de licença na pasta bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="7fbf0-253">[Transferir o pacote de Olá Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="7fbf0-254">Inicie sessão na aplicação de web de fase tooyour, diga http://umbracocms-site-stage.azurewebsites.net/umbraco, clique em Olá **programador** e, em seguida, clique em **pacotes** > **instalar pacote local**.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Instalador do pacote de Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="7fbf0-256">Carregar o pacote de Olá Courier2 utilizando o instalador Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Carregar o pacote para o módulo de courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="7fbf0-258">pacote de Olá tooconfigure, é necessário que o ficheiro de courier.config de Olá tooupdate em Olá **configuração** pasta da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="7fbf0-259">Em `<repositories>`, introduza Olá produção URL e o utilizador as informações de site.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="7fbf0-260">Se estiver a utilizar o fornecedor de membros Umbraco Olá predefinido, em seguida, adicione Olá ID de utilizador de administração de Olá no Olá &lt;utilizador&gt; secção.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="7fbf0-261">Se estiver a utilizar um fornecedor de associação Umbraco personalizado, utilize `<login>`,`<password>` no site de produção do Olá Courier2 módulo tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="7fbf0-262">Para obter mais detalhes, [consultar a documentação de Olá para o módulo Olá Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="7fbf0-263">Da mesma forma, instale o módulo de Courier2 Olá no seu site de produção e configure-a aplicação web do toopoint toohello fase no respetivo ficheiro courier.config respetivos conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="7fbf0-264">Clique em Olá **Courier2** separador Olá dashboard de aplicações web Umbraco CMS e, em seguida, clique em **localizações**.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="7fbf0-265">Deverá ver o nome do repositório Olá tal como mencionado na `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="7fbf0-266">Efetue este processo nas suas produção e o teste web apps.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-266">Do this process on both your production and staging web apps.</span></span>

    ![Repositório de aplicação de web de destino de vista](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="7fbf0-268">toodeploy conteúdo do site de produção toohello de site, de transição de Olá aceda demasiado**conteúdo**e selecione uma página existente ou crie uma nova página.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="7fbf0-269">Posso irá selecionar uma página existente da minha aplicação web em que é o título de Olá da página Olá **introdução – novo**e, em seguida, clique em **guardar e publicar**.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Alterar o título da página e publicar](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="7fbf0-271">Contexto Olá modificado página tooview todas as opções de Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="7fbf0-272">Clique em **Courier** tooopen Olá **implementação** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="7fbf0-273">Clique em **implementar** tooinitiate implementação.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Caixa de diálogo de implementação de módulo de Courier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="7fbf0-275">Rever as alterações de Olá e, em seguida, clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-275">Review hello changes, and then click **Continue**.</span></span>

    ![Alterações de revisão de caixa de diálogo de implementação de módulo de Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="7fbf0-277">registo da implementação Olá mostra se a implementação de Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Ver registos de implementação do módulo de Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="7fbf0-279">Procure o toosee de aplicação de web de produção se as alterações de Olá são refletidas.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Procure a aplicação web de produção](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="7fbf0-281">toolearn mais informações sobre como toouse Courier, reveja Olá documentação.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="7fbf0-282">Como tooupgrade Olá versão Umbraco CMS</span><span class="sxs-lookup"><span data-stu-id="7fbf0-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="7fbf0-283">Irá Courier não atualizar de uma versão do Umbraco CMS tooanother de ajuda.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="7fbf0-284">Ao atualizar uma versão de Umbraco CMS, tem de verificar a existência de incompatibilidades com os módulos personalizados ou os módulos de parceiros e Olá bibliotecas Umbraco principais.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="7fbf0-285">Seguem-se as melhores práticas:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-285">Here are best practices:</span></span>

* <span data-ttu-id="7fbf0-286">Sempre efetuar uma cópia de segurança de aplicação web e a base de dados antes de atualizar.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="7fbf0-287">Nas aplicações web no Azure, pode configurar cópias de segurança automáticas para os Web sites utilizando a funcionalidade de cópia de segurança de Olá e restaurar o seu site se for necessário, utilizando a funcionalidade de restauro Olá.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="7fbf0-288">Para obter mais detalhes, consulte [como tooback verticalmente a sua aplicação web](web-sites-backup.md) e [como toorestore a aplicação web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="7fbf0-289">Verifique se os pacotes de parceiros estão compatíveis com a versão de Olá que estiver a atualizar a.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="7fbf0-290">Página de transferência no pacote de Olá, reveja Olá projeto de compatibilidade com a versão de Umbraco CMS.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="7fbf0-291">Para obter mais detalhes sobre como tooupgrade a aplicação web localmente, [Consulte Olá geral atualização orientação](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="7fbf0-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="7fbf0-292">Depois de atualizar o seu site de desenvolvimento local, publica Olá alterações toohello aplicação web de transição.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="7fbf0-293">Teste a aplicação.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-293">Test your application.</span></span> <span data-ttu-id="7fbf0-294">Se todos os procura boa, utilize Olá **comutação** botão tooswap a aplicação de web de produção de toohello do teste site.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="7fbf0-295">Quando utiliza Olá **comutação** operação, pode ver as alterações de Olá que vai ser afetadas na configuração da sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="7fbf0-296">Isto **comutação** operação trocas Olá web apps e bases de dados.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="7fbf0-297">Depois de Olá **comutação**, Olá produção web aplicação será ponto toohello umbraco-fase-db da base de dados e Olá base de dados do teste web aplicação será ponto tooumbraco-prod-db.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Pré-visualização de comutação para implementar Umbraco CMS](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="7fbf0-299">Seguem-se as vantagens de troca de aplicação web de Olá e base de dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="7fbf0-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="7fbf0-300">Pode reverter toohello versão anterior da aplicação web com outra **comutação** se houver algum problema de aplicação.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="7fbf0-301">Para uma atualização, terá de toodeploy ficheiros e de bases de dados de aplicação de web de produção de toohello aplicação web de transição de Olá e de base de dados.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="7fbf0-302">Inúmeros aspetos podem correrem mal quando implementar os ficheiros e as bases de dados.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="7fbf0-303">Ao utilizar Olá **comutação** funcionalidade de ranhuras, iremos pode reduzir o período de indisponibilidade durante a atualização e reduzir o risco de Olá de falhas que podem ocorrer ao implementar alterações.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="7fbf0-304">Pode fazê-lo **um teste a / B** utilizando Olá [teste em produção](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="7fbf0-305">Este exemplo mostra Olá flexibilidade de plataforma olá onde pode criar módulos personalizados semelhante implementação de toomanage do módulo Courier tooUmbraco entre ambientes.</span><span class="sxs-lookup"><span data-stu-id="7fbf0-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="7fbf0-306">Referências</span><span class="sxs-lookup"><span data-stu-id="7fbf0-306">References</span></span>
[<span data-ttu-id="7fbf0-307">Desenvolvimento de software seja ágil App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="7fbf0-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="7fbf0-308">Configurar ambientes para web apps no App Service do Azure de teste</span><span class="sxs-lookup"><span data-stu-id="7fbf0-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="7fbf0-309">Como tooblock web aceder às ranhuras de implementação de produção toonon</span><span class="sxs-lookup"><span data-stu-id="7fbf0-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
