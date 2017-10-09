---
title: aaaDeploy WebJobs com o Visual Studio
description: "Saiba como toodeploy WebJobs do Azure tooAzure serviço Web Apps do App com o Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a>Implementar o WebJobs com o Visual Studio
## <a name="overview"></a>Descrição geral
Este tópico explica como toouse Visual Studio toodeploy uma aplicação de consola projeto aplicação web de tooa no [do serviço de aplicações](http://go.microsoft.com/fwlink/?LinkId=529714) como um [trabalho Web do Azure](http://go.microsoft.com/fwlink/?LinkId=390226). Para obter informações sobre como toodeploy WebJobs utilizando Olá [Portal do Azure](https://portal.azure.com), consulte [tarefas de execução em segundo plano com WebJobs](web-sites-create-web-jobs.md).

Quando o Visual Studio implementa um projeto de aplicação de consola com WebJobs, executa duas tarefas:

* Tempo de execução de cópias ficheiros toohello pasta adequada no Olá web app (*App_Data/tarefas/contínua* para WebJobs contínuos, *App_Data/tarefas/acionada* para WebJobs agendadas e a pedido).
* Configura [tarefas do agendador do Azure](#scheduler) para WebJobs são agendada toorun em alturas específicas. (Isto não é necessária para WebJobs contínuos.)

Um projeto preparados WebJobs tem Olá tooit adicionados itens a seguir:

* Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pacote NuGet.
* A [settings.json webjob publicar](#publishsettings) ficheiro que contém as definições de implementação e programador. 

![Diagrama que mostra o que é adicionado a implementação de tooenable tooa aplicação de consola como um trabalho Web](./media/websites-dotnet-deploy-webjobs/convert.png)

Pode adicionar estes tooan de itens existentes projeto de aplicação de consola ou utilizar um modelo toocreate um novo projeto de aplicação de consola com WebJobs. 

Pode implementar um projeto como um WebJob por si só ou ligue-o projeto web de tooa para que implementa automaticamente sempre que implementar o projeto web de Olá. toolink projetos, o Visual Studio inclui o nome de Olá do projeto de ativado o WebJobs Olá num [webjobs list.json](#webjobslist) ficheiros no projeto web de Olá.

![Diagrama que mostra o projeto de WebJob tooweb projeto de ligação](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a>Pré-requisitos
Funcionalidades de implementação de WebJobs estão disponíveis no Visual Studio quando instala Olá Azure SDK para .NET:

* [Azure SDK para .NET (Visual Studio)](https://azure.microsoft.com/downloads/).

## <a id="convert"></a>Ativar a implementação de WebJobs para um projeto de aplicação de consola existente
Tem duas opções:

* [Ativar a implementação automática com um projeto web](#convertlink).
  
    Configure um projeto de aplicação de consola existente para que o se implementa automaticamente como um WebJob quando implementar um projeto web. Utilize esta opção quando quiser toorun o trabalho Web em Olá mesma aplicação web na qual executar Olá relacionadas com a aplicação web.
* [Ativar a implementação sem um projeto web](#convertnolink).
  
    Configure um toodeploy de projeto de aplicação de consola existente como um WebJob por si só, com o projeto de web de tooa nenhuma ligação. Utilize esta opção quando quiser toorun um WebJob numa aplicação web por si só, com nenhuma aplicação web em execução na aplicação web de Olá. É aconselhável toodo isto na ordem tooscale capaz de toobe os recursos de trabalho Web independentemente os recursos de aplicação web.

### <a id="convertlink"></a>Ativar a implementação automática de WebJobs com um projeto web
1. Contexto Olá web projeto **Explorador de soluções**e, em seguida, clique em **adicionar** > **projeto existente como o trabalho Web do Azure**.
   
    ![Projeto existente como o trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    Olá [trabalho Web do Azure de adicionar](#configure) é apresentada a caixa de diálogo.
2. No Olá **nome do projeto** na lista pendente, selecione Olá tooadd de projeto de aplicação de consola como um WebJob.
   
    ![Selecionar o projeto na caixa de diálogo Adicionar WebJob do Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. Olá concluída [trabalho Web do Azure de adicionar](#configure) caixa de diálogo e, em seguida, clique em **OK**. 

### <a id="convertnolink"></a>Ativar a implementação de WebJobs sem um projeto web
1. Projeto de aplicação de consola do contexto Olá no **Explorador de soluções**e, em seguida, clique em **publicar como trabalho Web do Azure...** . 
   
    ![Publicar como trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    Olá [trabalho Web do Azure de adicionar](#configure) caixa de diálogo é apresentada, com o projeto de Olá selecionado na Olá **nome do projeto** caixa.
2. Olá concluída [trabalho Web do Azure de adicionar](#configure) caixa de diálogo e, em seguida, clique em **OK**.
   
   Olá **publicar Web** é apresentado o assistente.  Se não quiser toopublish imediatamente, feche o Assistente de Olá. definições de Olá que introduziu são guardadas para quando quiser demasiado[implementar o projeto de Olá](#deploy).

## <a id="create"></a>Criar um novo projeto WebJobs-ativado
toocreate um novo projeto WebJobs ativado, pode utilizar Olá aplicação de consola projeto modelo e ativar WebJobs implementação conforme explicado no [Olá secção anterior](#convert). Como alternativa, pode utilizar o modelo de novo projeto do Olá WebJobs:

* [Utilizar o modelo de novo projeto de WebJobs Olá para um WebJob independente](#createnolink)
  
    Criar um projeto e configurá-lo toodeploy autonomamente como um WebJob, com o projeto de web de tooa nenhuma ligação. Utilize esta opção quando quiser toorun um WebJob numa aplicação web por si só, com nenhuma aplicação web em execução na aplicação web de Olá. É aconselhável toodo isto na ordem tooscale capaz de toobe os recursos de trabalho Web independentemente os recursos de aplicação web.
* [Utilizar o modelo de novo projeto de WebJobs Olá para um projeto web do trabalho Web tooa ligado](#createlink)
  
    Crie um projeto que está configurado toodeploy automaticamente como um WebJob quando um projeto web na Olá mesma solução for implementada. Utilize esta opção quando quiser toorun o trabalho Web em Olá mesma aplicação web na qual executar Olá relacionadas com a aplicação web.

> [!NOTE]
> modelo de novo projeto de WebJobs Olá automaticamente instala os pacotes NuGet e inclui código *Program.cs* para Olá [SDK de WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs). Se não quiser toouse Olá SDK de WebJobs, remover ou alterar Olá `host.RunAndBlock` instrução no *Program.cs*.
> 
> 

### <a id="createnolink"></a>Utilizar o modelo de novo projeto de WebJobs Olá para um WebJob independente
1. Clique em **ficheiro** > **novo projeto**e, em seguida, no Olá **novo projeto** clique da caixa de diálogo **nuvem**  >   **Trabalho Web do Azure (.NET Framework)**.
   
    ![Caixa de diálogo do projeto nova que mostra o modelo do trabalho Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. Siga as instruções de Olá apresentadas anteriormente demasiado[tornar Olá projeto de aplicação de consola um projeto de WebJobs independente](#convertnolink).

### <a id="createlink"></a>Utilizar o modelo de novo projeto de WebJobs Olá para um projeto web do trabalho Web tooa ligado
1. Contexto Olá web projeto **Explorador de soluções**e, em seguida, clique em **adicionar** > **novo projeto do trabalho Web do Azure**.
   
    ![Nova entrada de menu do projeto de trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    Olá [trabalho Web do Azure de adicionar](#configure) é apresentada a caixa de diálogo.
2. Olá concluída [trabalho Web do Azure de adicionar](#configure) caixa de diálogo e, em seguida, clique em **OK**.

## <a id="configure"></a>caixa de diálogo do Olá adicionar WebJob do Azure
Olá **trabalho Web do Azure de adicionar** caixa de diálogo permite-lhe introduzir o nome do WebJob Olá e executar a definição do modo para o trabalho Web. 

![Adicionar caixa de diálogo do trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

campos de Olá nesta caixa de diálogo correspondem toofields no Olá **nova tarefa** caixa de diálogo de Olá Portal do Azure. Para obter mais informações, consulte [tarefas de execução em segundo plano com WebJobs](web-sites-create-web-jobs.md).

> [!NOTE]
> * Para obter informações sobre a implementação da linha de comandos, consulte [ativação da linha de comandos ou entrega de Azure WebJobs contínuos](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).
> * Se implementar um WebJob e, em seguida, decidir que pretende que o tipo de Olá toochange do trabalho Web e volte a implementar, terá de ficheiro do toodelete Olá settings.json webjobs publicar. Esta ação irá tornar o Visual Studio Mostrar Olá novamente, as opções de publicação para que possa alterar o tipo de Olá do trabalho Web.
> * Se implementar um WebJob e mais tarde mudar de Olá modo execução contínua de toonon contínua ou vice-versa, o Visual Studio cria um WebJob novo no Azure quando implementar novamente. Se alterar outras definições de agendamento, mas deixe executar modo Olá mesmo ou alternar entre agendada e a pedido, atualizações do Visual Studio Olá tarefa existente em vez de criar um novo.
> 
> 

## <a id="publishsettings"></a>settings.json webjob publicar
Quando configurar uma aplicação de consola para a implementação de WebJobs, o Visual Studio instala Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet pacote e armazena informações de agendamento um *settings.json webjob publicar*  ficheiros no projeto Olá *propriedades* pasta do projeto de WebJobs Olá. Eis um exemplo desse ficheiro:

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

Pode editar este ficheiro diretamente e o Visual Studio fornece IntelliSense. esquema do ficheiro de Olá é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) e podem ser visualizados não existe.  

## <a id="webjobslist"></a>webjobs list.json
Quando liga um projeto do projeto preparados WebJobs tooa web, Visual Studio armazena o nome de Olá do projeto de WebJobs Olá num *webjobs list.json* ficheiros do projeto web Olá *propriedades* pasta. lista de Olá pode conter vários projetos de WebJobs, conforme mostrado no seguinte exemplo de Olá:

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

Pode editar este ficheiro diretamente e o Visual Studio fornece IntelliSense. esquema do ficheiro de Olá é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) e podem ser visualizados não existe.

## <a id="deploy"></a>Implementar um projeto de WebJobs
Um projeto de WebJobs que tenha ligado projeto web de tooa implementa automaticamente com o projeto web de Olá. Para obter informações sobre a implementação do projeto web, consulte [como toodeploy tooWeb aplicações](web-sites-deploy.md).

toodeploy um projeto de WebJobs por si só, clique no projeto Olá no **Explorador de soluções** e clique em **publicar como trabalho Web do Azure...** . 

![Publicar como trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

Para um WebJob independente, Olá mesmo **publicar Web** assistente que é utilizado para projetos web é apresentada, mas com menos toochange disponíveis de definições.

## <a id="nextsteps"></a>Passos Seguintes
Este artigo tem explicado como toodeploy WebJobs utilizando o Visual Studio. Para obter mais informações sobre como toodeploy WebJobs do Azure, consulte o artigo [WebJobs do Azure - recomendado recursos - implementação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).

