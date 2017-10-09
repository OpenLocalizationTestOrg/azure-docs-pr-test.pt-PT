---
title: "aaaCreate um PHP web de aplicação no Azure | Microsoft Docs"
description: "Implemente em minutos a sua primeira aplicação PHP Hello World nas aplicações Web do serviço de aplicações do Azure."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a>Criar uma aplicação Web PHP no Azure

[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática.  Este tutorial de início rápido mostra como toodeploy um tooAzure de aplicações do PHP Web Apps. Criar Olá web app através da Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) na Shell de nuvem e utilizar toodeploy Git exemplo PHP código toohello da aplicação web.

![Aplicação de exemplo em execução no Azure]] (media/app-service-web-get-started-php/hello-world-in-browser.png)

Pode seguir os passos seguintes Olá utilizando um computador Mac, Windows ou Linux. Depois de Olá pré-requisitos se encontrem instalados, demora cerca de cinco minutos toocomplete passos Olá.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de introdução:

* [Instale o Git](https://git-scm.com/).
* [Instalar o PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>Transferir o exemplo de Olá localmente

Na janela de terminal, execute Olá os seguintes comandos. Isto será clonar a máquina local de tooyour aplicação de exemplo Olá e navegue até o código de exemplo de Olá contentor do toohello diretório.

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>Executar localmente a aplicação Olá

Executar a aplicação Olá localmente ao abrir uma janela de terminal e utilizar Olá `php` comando toolaunch Olá incorporada PHP servidor web.

```bash
php -S localhost:8080
```

Abra um browser e navegue até a aplicação de exemplo toohello no http://localhost:8080.

Consulte Olá **Olá, mundo!** mensagem da aplicação de exemplo de Olá apresentada na página Olá.

![Aplicação de exemplo em execução localmente](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

Na janela do terminal, prima **Ctrl + C** servidor de web de Olá tooexit.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Página da aplicação Web vazia](media/app-service-web-get-started-php/app-service-web-service-created.png)

Acabou de criar uma nova aplicação Web vazia no Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a>Procurar toohello aplicação localmente

Procure a aplicação de toohello implementado utilizando o seu browser.

```bash
http://<app_name>.azurewebsites.net
```

Olá, código de exemplo do PHP está em execução numa aplicação web App Service do Azure.

![Aplicação de exemplo em execução no Azure](media/app-service-web-get-started-php/hello-world-in-browser.png)

**Parabéns!** Transferiu o seu primeiro tooApp de aplicações do PHP serviço.

## <a name="update-locally-and-redeploy-hello-code"></a>Atualizar localmente e volte a implementar o código de Olá

Com um editor de texto local, abra Olá `index.php` ficheiro dentro da aplicação PHP Olá e faça um texto de toohello pequenas alterações na cadeia de Olá junto demasiado`echo`:

```php
echo "Hello Azure!";
```

Consolidar as alterações no Git e, em seguida, emitir tooAzure de alterações de código Olá.

```bash
git commit -am "updated output"
git push azure master
```

Depois de concluída a implementação, mudar a janela do browser back toohello que aberto no Olá **procurar toohello aplicação** passo e página Olá de atualização.

![Aplicação de exemplo atualizada em execução no Azure](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>Gerir a sua nova aplicação Web do Azure

Aceda toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicação que criou.

No menu à esquerda Olá, clique em **serviços aplicacionais**e, em seguida, clique em nome de Olá da sua aplicação web do Azure.

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

É apresentada a página de descrição geral da sua aplicação Web. Aqui, pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar.

![Painel Serviço de Aplicações no portal do Azure](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

menu à esquerda Olá fornece páginas diferentes para configurar a sua aplicação. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [PHP com MySQL](app-service-web-tutorial-php-mysql.md)
