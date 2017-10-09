---
title: "aaaCreate sua primeira aplicação de web de Java no Azure"
description: "Saiba como toorun web apps no App Service ao implementar uma aplicação básica de Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Criar a primeira aplicação Web Java no Azure

Olá [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) funcionalidade do [App Service do Azure](../app-service/app-service-value-prop-what-is.md) fornece uma serviço de alojamento na web altamente dimensionável e aplicação de patches personalizada. Este guia de introdução mostra como toodeploy um Java web tooApp do app Service utilizando Olá [IDE Eclipse para programadores de Java EE](http://www.eclipse.org/).

!["Olá, Azure!” aplicação Web de exemplo](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este guia de introdução, instale:

* Olá livre [IDE Eclipse para programadores de Java EE](http://www.eclipse.org/downloads/). Este guia de introdução utiliza o Eclipse Neon.
* Olá [Toolkit do Azure para o Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Criar um projeto Web dinâmico no Eclipse

No Eclipse, selecione **Ficheiro** > **Novo** > **Projeto Web Dinâmico**.

No Olá **novo Dynamic Web Project** caixa de diálogo, o projeto de Olá nome **MyFirstJavaOnAzureWebApp**e selecione **concluir**.
   
![Caixa de diálogo Novo Projeto Web Dinâmico](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Adicionar uma página JSP

Se o Explorador de Projeto não for apresentado, restaure-o.

![Área de trabalho Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

No Explorador de projeto, expanda Olá **MyFirstJavaOnAzureWebApp** projeto.
Clique com botão direito do rato em **WebContent**e, em seguida, selecione **Novo** > **Ficheiro JSP**.

![Menu de um novo ficheiro JSP no Explorador de Projeto](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

No Olá **novo ficheiro JSP** caixa de diálogo:

* Ficheiro de Olá nome **index.jsp**.
* Selecione **Concluir**.

  ![Caixa de diálogo Novo Ficheiro JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

No ficheiro de index.jsp Olá, substitua Olá `<body></body>` elemento com Olá markup os seguintes:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Guarde as alterações de Olá.

## <a name="publish-hello-web-app-tooazure"></a>Publicar Olá web app tooAzure

No Explorador de projeto, clique no projeto Olá e, em seguida, selecione **Azure** > **publicar como aplicação Web do Azure**.

![Menu de contexto Publicar como Aplicação Web do Azure](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

No Olá **Azure sessão** caixa de diálogo, mantenha Olá **interativo** opção e, em seguida, selecione **sessão**.

Siga as instruções de início de sessão Olá.

### <a name="deploy-web-app-dialog-box"></a>Caixa de diálogo Implementar Aplicação Web

Depois de ter a sessão tooyour conta do Azure, Olá **implementar Web App** é apresentada a caixa de diálogo.

Selecione **Criar**.

![Caixa de diálogo Implementar Aplicação Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Caixa de diálogo Criar Serviço de Aplicações

Olá **criar App Service** é apresentada a caixa de diálogo com os valores predefinidos. número de Olá **170602185241** mostrado na Olá seguinte imagem é diferente na sua caixa de diálogo.

![Caixa de diálogo Criar Serviço de Aplicações](./media/app-service-web-get-started-java/cas1.png)

No Olá **criar App Service** caixa de diálogo:

* Mantenha o nome de Olá gerado para a aplicação web de Olá. Este nome tem de ser exclusivo em todo o Azure. nome de Olá faz parte do endereço de URL Olá da aplicação web de Olá. Por exemplo: se for o nome da aplicação web Olá **MyJavaWebApp**, Olá URL é *myjavawebapp.azurewebsites.net*.
* Mantenha o contentor de web Olá predefinido.
* Selecione uma subscrição do Azure.
* No Olá **plano do App service** separador:

  * **Criar um novo**: mantenha Olá, predefinição que é o nome de Olá de Olá plano do App Service.
  * **Localização**: selecione **Europa Ocidental** ou um local perto de si.
  * **Escalão de preço**: selecione Olá opção gratuita. Para as funcionalidades, veja [Preços do Serviço de Aplicações](https://azure.microsoft.com/pricing/details/app-service/).

   ![Caixa de diálogo Criar Serviço de Aplicações](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Separador grupo de recursos

Selecione Olá **grupo de recursos** separador. Mantenha o valor de predefinido gerado de Olá Olá grupo de recursos.

![Separador grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Selecione **Criar**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Olá Toolkit do Azure cria a aplicação web de Olá e apresenta uma caixa de diálogo de progresso.

![Caixa de diálogo Progresso de Criar Serviço de Aplicações](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Caixa de diálogo Implementar Aplicação Web

No Olá **implementar Web App** caixa de diálogo, selecione **implementar tooroot**. Se tiver um serviço de aplicações em *wingtiptoys.azurewebsites.net* e não implementar toohello raiz, aplicação web de Olá designada **MyFirstJavaOnAzureWebApp** é implementado demasiado *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Caixa de diálogo Implementar Aplicação Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

mostra de caixa de diálogo Olá hello do Azure, JDK e seleções de contentor web.

Selecione **implementar** toopublish Olá web app tooAzure.

Quando concluir a publicação de Olá, selecione Olá **publicada** ligação no Olá **registo de atividade do Azure** caixa de diálogo.

![Caixa de diálogo de Registo de Atividade do Azure](./media/app-service-web-get-started-java/aal.png)

Parabéns! Implementados com êxito a sua tooAzure de aplicação web. 

!["Olá, Azure!” aplicação Web de exemplo](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Atualizar a aplicação web de Olá

Alterar exemplo JSP código tooa outra mensagem de saudação.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Guarde as alterações de Olá.

No Explorador de projeto, clique no projeto Olá e, em seguida, selecione **Azure** > **publicar como aplicação Web do Azure**.

Olá **implementar Web App** é apresentada a caixa de diálogo e mostra hello do serviço de aplicações que criou anteriormente. 

> [!NOTE]
> Selecione **implementar tooroot** sempre publicar.
>

Selecione a aplicação web de Olá e selecione **implementar**, que publica alterações Olá.

Quando Olá **publicação** ligação for apresentada, selecione-a aplicação de web de toohello toobrowse e ver Olá alterações.

## <a name="manage-hello-web-app"></a>Gerir a aplicação web de Olá

Aceda toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toosee Olá web aplicação que criou.

No menu à esquerda de Olá, selecione **grupos de recursos**.

![Grupos de tooresource de navegação do portal](media/app-service-web-get-started-java/rg.png)

Selecione o grupo de recursos de Olá. página Olá mostra recursos Olá que criou neste guia de introdução.

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

Selecione Olá web app (**webapp 170602193915** no Olá anterior a imagem).

Olá **descrição geral** é apresentada a página. Esta página dá-lhe uma vista de como aplicação Olá está a fazer. Aqui, pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar. separadores Olá no lado esquerdo do Olá da página Olá mostram Olá configurações diferentes em que pode abrir. 

![Página Serviço de Aplicações no portal do Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Passos seguintes

> [!div class="nextstepaction"]
> [Mapear domínio personalizado](app-service-web-tutorial-custom-domain.md)
