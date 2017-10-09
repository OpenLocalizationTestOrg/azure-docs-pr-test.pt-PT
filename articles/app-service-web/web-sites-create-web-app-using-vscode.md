---
title: "aaaCreate uma aplicação web de ASP.NET Core no Visual Studio Code"
description: "Este tutorial ilustra como toocreate um núcleo de ASP.NET web app através do Visual Studio Code."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a>Criar uma aplicação de web de ASP.NET Core no Visual Studio Code
## <a name="overview"></a>Descrição geral
Este tutorial mostra como toocreate um núcleo de ASP.NET web app utilizando [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) e implementá-la demasiado[App Service do Azure](../app-service/app-service-value-prop-what-is.md). 

> [!NOTE]
> Embora este artigo se refira a aplicações tooweb, também se aplica tooAPI aplicações e aplicações móveis. 
> 
> 

ASP.NET Core é uma recriar significativa do ASP.NET. ASP.NET Core é uma nova arquitetura de open source e plataforma para a criação de aplicações web baseados na nuvem modernas utilizando o .NET. Para obter mais informações, consulte [introdução tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html). Para obter informações sobre as aplicações web do App Service do Azure, consulte [descrição geral de aplicações Web](app-service-web-overview.md).

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a>Pré-requisitos
* Instalar [o VS Code](http://code.visualstudio.com/Docs/setup).
* Instalar o Git - pode instalá-lo a partir de qualquer um destas localizações: [Chocolatey](https://chocolatey.org/packages/git) ou [git scm.com](http://git-scm.com/downloads). Se for novo tooGit, escolha [git scm.com](http://git-scm.com/downloads) e selecione a opção de Olá demasiado**Git de utilização do Olá linha de comandos do Windows**. Depois de instalar o Git, também terá de nome de utilizador do tooset Olá Git e e-mail conforme for necessário mais tarde no tutorial Olá (quando efetuar uma consolidação a partir do código de VS).  

## <a name="install-aspnet-core"></a>Instalar o ASP.NET Core
ASP.NET Core é uma pilha de .NET lean para criação de nuvem moderna e aplicações web que são executados nos X, Linux e Windows. Se foram criada de Olá fundo segurança tooprovide uma arquitetura de programação otimizado para aplicações que estão a nuvem toohello implementado ou executado no local. É composto por componentes modulares com overhead mínimo para manter flexibilidade ao construir as suas soluções.

Este tutorial é concebida tooget começou a criar aplicações com Olá mais recentes desenvolvimento as versões do ASP.NET Core. Olá seguir instruções é específicas tooWindows. Para obter instruções de instalação nos X, Linux e Windows, consulte [introdução ao ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started). 


> [!NOTE]
> Para obter mais instruções de instalação para OS X, Linux e Windows, consulte [instalar o ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx). 
> 
> 

## <a name="create-hello-web-app"></a>Criar aplicação web de Olá
Esta secção mostra como tooscaffold uma nova aplicação ASP.NET web app através da ferramenta de .NET CLI Olá. 

1. Introduza o seguinte de Olá na Olá linha de comandos toocreate Olá projeto pasta e andaime Olá aplicação.
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![DotNet CLI - gerador de ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. toorestore Olá necessários pacotes NuGet e execute o Olá os seguintes comandos:
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a>Executar localmente a aplicação web de Olá
Agora que criou a aplicação web de Olá e obter todos os pacotes de NuGet Olá da aplicação Olá, pode executar Olá web aplicação localmente.

1. Executar a aplicação Olá (Olá `dotnet run` comando irá criar a aplicação Olá quando está desatualizada):
    ```terminal
    dotnet run
    ```
2. Abra um browser e navegue toohello seguinte URL.
   
    **http://localhost:5000**
   
    será apresentada a página predefinida de Olá da aplicação web de Olá da seguinte forma.
   
    ![Aplicação local web num browser](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. Feche o browser. No Olá **janela de comando**, prima **Ctrl + C** tooshut baixo aplicação Olá e fechar Olá **janela de comando**. 

## <a name="create-a-web-app-in-hello-azure-portal"></a>Criar uma aplicação web no Olá Portal do Azure
Olá passos seguintes irão guiá-lo a criar uma aplicação web no Olá Portal do Azure.

1. Inicie sessão no toohello [Portal do Azure](https://portal.azure.com).
2. Clique em **novo** em Olá parte superior esquerda do Olá Portal.
3. Clique em **aplicações Web > aplicação Web**.
   
    ![Nova aplicação de web do Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. Introduza um valor para **nome**, tais como **SampleWebAppDemo**. Tenha em atenção que este nome tem de toobe exclusivo e portal Olá irá impor que quando a tentativa de nome de Olá tooenter. Por conseguinte, se selecionar uma introduza um valor diferente, terá de toosubstitute valor para cada ocorrência dos **SampleWebAppDemo** que visualiza neste tutorial. 
5. Selecione um existente **plano do App Service** ou crie um novo. Se criar um novo plano, selecione Olá outras opções, localização e escalão de preço. Para obter mais informações sobre os planos do App Service, consulte o artigo de Olá, [descrição geral dos planos do App Service do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
   
    ![Azure novo painel de aplicação web](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. Clique em **Criar**.
   
    ![Painel aplicação Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a>Ativar a publicação de Git para a nova aplicação de web Olá
Git é um sistema de controlo de versão distribuída que é possível utilizar toodeploy a aplicação web do App Service do Azure. Irá armazenar o código de Olá escrita para a sua aplicação web num repositório de Git local e implementar o código tooAzure ao enviar o repositório remoto tooa.   

1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com).
2. Clique em **Browse** (Procurar).
3. Clique em **Web Apps** tooview uma lista de aplicações web de Olá associados à subscrição do Azure.
4. Selecione a aplicação de web de Olá que criou neste tutorial.
5. No painel de aplicação web de Olá, clique em **definições** > **a implementação contínua**. 
   
    ![Anfitrião de aplicação web do Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. Clique em **Escolher origem > repositório de Git Local**.
7. Clique em **OK**.
   
    ![Respository de Git Local do Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. Se não anteriormente configurou as credenciais de implementação para publicar uma aplicação web ou outra aplicação de serviço de aplicações, configure-os agora:
   
   * Clique em **definições** > **as credenciais de implementação**. Olá **definir credenciais de implementação** é apresentado o painel.
   * Crie um nome de utilizador e uma palavra-passe.  Irá precisar desta palavra-passe mais tarde, quando configurar o Git.
   * Clique em **Guardar**.
9. No painel da sua aplicação web, clique em **definições > propriedades**. URL de Olá de Olá repositório de Git remoto que vai implementar toois apresentado em **URL do GIT**.
10. Olá cópia **URL do GIT** valor para utilização posterior tutorial Olá.
    
    ![URL do Git do Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a>Publicar a sua tooAzure de aplicação web do serviço de aplicações
Nesta secção, irá criar um repositório de Git local e emitir a partir desse toodeploy tooAzure do repositório a tooAzure de aplicação web.

1. No VS Code, selecione Olá **Git** opção na barra de navegação esquerdo Olá.
   
    ![Ícone de Git no VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. Selecione **repositório de git inicializar** toomake se a sua área de trabalho está sob o controlo de origem do git. 
   
    ![Inicializar o Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. Abrir Olá janela de comandos e altere o diretório de toohello de diretórios da sua aplicação web. Em seguida, introduza Olá os seguintes comandos:
   
        git config core.autocrlf false
   
    Este comando impede que um problema sobre texto onde CRLF endings e LF endings estiverem envolvidos.
4. No VS Code, adicione uma mensagem de consolidação e clique em Olá **todos os consolidação** ícone de verificação.
   
    ![Consolidação de Git todos](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. Depois de Git terminou de processar, verá que existem não existem ficheiros listados na janela do Git Olá na **alterações**. 
   
    ![Git sem alterações](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. Altere o fundo toohello janela de comando em que linha de comandos Olá pontos toohello diretório onde está localizada a sua aplicação web.
7. Crie uma referência remota para enviar atualizações tooyour web app através da utilização de Olá URL do Git (terminar em ".git") que copiou anteriormente.
   
        git remote add azure [URL for remote repository]
8. Configure o Git toosave as suas credenciais localmente para que estarão disponíveis os comandos de push tooyour anexado automaticamente gerados a partir do código de VS.
   
        git config credential.helper store
9. Emitir o tooAzure alterações introduzindo Olá os seguintes comandos. Após este tooAzure push inicial, será capaz de toodo push de Olá todos os comandos a partir do código de VS. 
   
        git push -u azure master
   
    É-lhe pedido para a palavra-passe de Olá que criou anteriormente no Azure. **Nota: A palavra-passe não serão visível.**
   
    saída de Olá de Olá acima comando termina com uma mensagem que a implementação é efetuada com êxito.
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> Se efetuar alterações tooyour aplicação, pode voltar a publicar diretamente no VS Code utilizando a funcionalidade de Git incorporada Olá selecionando Olá **consolidar todas as** opção seguido Olá **Push** opção. Encontrará Olá **Push** opção disponível no Olá menu pendente seguinte toohello **consolidar todas as** e **atualizar** botões.
> 
> 

Se precisar de toocollaborate num projeto, deve considerar a enviar tooGitHub entre enviar tooAzure.

## <a name="run-hello-app-in-azure"></a>Executar a aplicação Olá no Azure
Agora que implementou a aplicação web, vamos executar a aplicação de Olá enquanto alojado no Azure. 

Pode fazê-lo de duas formas:

* Abra um browser e introduza o nome de Olá da sua aplicação web da seguinte forma.   
  
        http://SampleWebAppDemo.azurewebsites.net
* No Olá Portal do Azure, localize o painel de aplicação web Olá para a sua aplicação web e clique em **procurar** tooview a aplicação 
* no seu browser predefinido.

![Aplicação web do Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a>Resumo
Neste tutorial, aprendeu como toocreate uma aplicação web no VS Code e implementá-la tooAzure. Para mais informações sobre o VS Code, consulte o artigo de Olá, [por que motivo Visual Studio Code?](https://code.visualstudio.com/Docs/) Para obter informações sobre as web apps do App Service, consulte [descrição geral de aplicações Web](app-service-web-overview.md). 

