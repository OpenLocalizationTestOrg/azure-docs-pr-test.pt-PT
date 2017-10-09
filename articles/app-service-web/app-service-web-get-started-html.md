---
title: "aplicação web de aaaCreate um HTML estático no Azure | Microsoft Docs"
description: "Saiba como aplicação de exemplo toorun as web apps no App Service do Azure ao implementar um HTML estático."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>Criar uma aplicação Web HTML estática no Azure

[As Aplicações Web do Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática.  Este guia de introdução mostra como toodeploy HTML + CSS básico site tooAzure Web Apps. Criar Olá web app através da Olá [CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), e utilizar a aplicação web de conteúdo toohello HTML Git toodeploy exemplo.

![Página inicial da aplicação de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

Pode seguir os passos seguintes Olá utilizando um computador Mac, Windows ou Linux. Depois de Olá pré-requisitos se encontrem instalados, demora cerca de cinco minutos toocomplete passos Olá.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de introdução:

- [Instale o Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="download-hello-sample"></a>Transferir o exemplo de Olá

Numa janela de terminal, execute Olá os seguintes comandos tooclone Olá exemplo aplicação repositório tooyour computador local.

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

Utilize toorun desta janela de terminal todos os comandos de Olá neste guia de introdução.

## <a name="view-hello-html"></a>Ver Olá HTML

Navegue toohello diretório que contém o exemplo de Olá HTML. Abra Olá *index.html* ficheiros no seu browser.

![Home page da aplicação de exemplo](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Página da aplicação Web vazia](media/app-service-web-get-started-html/app-service-web-service-created.png)

Acabou de criar uma nova aplicação Web vazia no Azure.

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>Procurar aplicações toohello

Num browser, aceda toohello URL da aplicação web do Azure:

```
http://<app_name>.azurewebsites.net
```

página Olá está em execução como uma aplicação web do App Service do Azure.

![Home page da aplicação de exemplo](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**Parabéns!** Transferiu o seu primeiro tooApp de aplicação HTML serviço.

## <a name="update-and-redeploy-hello-app"></a>Atualizar e volte a implementar a aplicação de Olá

Abra Olá *index.html* ficheiro num editor de texto e de marcação de toohello uma alteração. Por exemplo, altere o cabeçalho de Olá H1 de toojust "Azure App Service - exemplo estático HTML o Site" "do serviço de aplicações do Azure".

Consolidar as alterações no Git e, em seguida, emitir tooAzure de alterações de código Olá.

```bash
git commit -am "updated HTML"
git push azure master
```

Depois de concluída a implementação, Atualize as suas alterações do browser toosee Olá.

![Página inicial atualizada da aplicação de exemplo](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>Gerir a sua nova aplicação Web do Azure

Aceda toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toomanage Olá web aplicação que criou.

No menu à esquerda Olá, clique em **serviços aplicacionais**e, em seguida, clique em nome de Olá da sua aplicação web do Azure.

![Aplicação de web de tooAzure de navegação do portal](./media/app-service-web-get-started-html/portal1.png)

É apresentada a página de descrição geral da sua aplicação Web. Aqui, pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar. 

![Painel Serviço de Aplicações no portal do Azure](./media/app-service-web-get-started-html/portal2.png)

menu à esquerda Olá fornece páginas diferentes para configurar a sua aplicação. 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [Mapear domínio personalizado](app-service-web-tutorial-custom-domain.md)
