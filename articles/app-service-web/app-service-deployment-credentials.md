---
title: "aaaAzure as credenciais de implementação do serviço de aplicações | Microsoft Docs"
description: "Saiba como toouse Olá as credenciais de implementação do App Service do Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Configurar as credenciais de implementação para o App Service do Azure
[App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) suportam dois tipos de credenciais para [implementação de Git local](app-service-deploy-local-git.md) e [implementação de FTP/S](app-service-deploy-ftp.md). Estes são não Olá, mesmo que as suas credenciais do Azure Active Directory.

* **Credenciais de utilizador ao nível**: um conjunto de credenciais de conta do Azure completo de Olá. Pode ser utilizado toodeploy tooApp serviço para qualquer aplicação, em qualquer subscrição, o que Olá conta do Azure tem tooaccess de permissão. Estes são o conjunto de credenciais predefinido do Olá que configurar na **serviços aplicacionais** > **&lt;APP_NAME>.azurewebsites.NET >** > **ascredenciaisdeimplementação**. Isto também é Olá conjunto predefinido que é apresentado no portal de Olá GUI (por exemplo, Olá **descrição geral** e **propriedades** da sua aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Quando delegar tooAzure de aceder aos recursos através de controlo de acesso baseado em ' (RBAC) da função ou coadministrador de permissões, cada utilizador do Azure que recebe acesso tooan aplicação pode utilizar sua credenciais de nível de utilizador pessoais até que o acesso é revogado. Estas credenciais de implementação não devem ser partilhados com outros utilizadores do Azure.
    >
    >

* **Credenciais ao nível da aplicação**: um conjunto de credenciais para cada aplicação. Pode ser utilizado toodeploy aplicação de toothat apenas. credenciais de Olá para cada aplicação é gerada automaticamente durante a criação da aplicação e se encontra da aplicação Olá perfil de publicação. Não é possível configurar manualmente as credenciais de Olá, mas pode repô-los para uma aplicação em qualquer altura.

    > [!NOTE]
    > Na ordem toogive alguém aceder a credenciais toothese através de função de acesso baseado em controlo (RBAC), terá de toomake-los contribuinte ou superior no Olá aplicação Web. Os leitores não são permitidos toopublish e, por conseguinte, não é possível aceder essas credenciais.
    >
    >

## <a name="userscope"></a>Definir e repor as credenciais de nível de utilizador

Pode configurar as suas credenciais de nível de utilizador em qualquer aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources). Independentemente disso, a aplicação que pode configurar estas credenciais, aplica-se aplicações de tooall e para todas as subscrições no seu Azure da conta. 

tooconfigure as suas credenciais de nível de utilizador:

1. No Olá [portal do Azure](https://portal.azure.com), clique em do serviço de aplicações >  **&lt;any_app >** > **as credenciais de implementação**.

    > [!NOTE]
    > No portal de Olá, tem de ter pelo menos uma aplicação para que possam aceder ao painel de credenciais de implementação de Olá. No entanto, com Olá [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), pode configurar as credenciais de nível de utilizador sem uma aplicação existente.

2. Configurar o nome de utilizador Olá e a palavra-passe e, em seguida, clique em **guardar**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Assim que tiver configurado as suas credenciais de implementação, pode encontrar Olá *Git* nome de utilizador de implementação na sua aplicação **descrição geral**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

e e *FTP* nome de utilizador de implementação na sua aplicação **propriedades**.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure mostra a palavra-passe de implementação de nível de utilizador. Se se esquecer da palavra-passe de Olá, não é possível obtê-lo. No entanto, pode repor as suas credenciais, seguindo os passos de Olá nesta secção.
>
>  

## <a name="appscope"></a>Obter e repor as credenciais de nível de aplicação
Para cada aplicação no App Service, as suas credenciais ao nível da aplicação são armazenadas na Olá perfil de publicação de XML.

credenciais do tooget Olá ao nível da aplicação:

1. No Olá [portal do Azure](https://portal.azure.com), clique em do serviço de aplicações >  **&lt;any_app >** > **descrição geral**.

2. Clique em **... Mais** > **perfil de publicação de Get**, e inicia a transferência para um. Ficheiro PublishSettings.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Olá aberta. PublishSettings de ficheiros e determinar Olá `<publishProfile>` etiqueta com o atributo de Olá `publishMethod="FTP"`. Em seguida, obter o `userName` e `password` atributos.
Estas são as credenciais do Olá ao nível da aplicação.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Credenciais de utilizador ao nível do toohello semelhante, o nome de utilizador de implementação de Olá FTP está num formato de Olá de `<app_name>\<username>`, e nome de utilizador de implementação de Git de Olá é apenas `<username>` sem Olá anterior `<app_name>\`.

credenciais do tooreset Olá ao nível da aplicação:

1. No Olá [portal do Azure](https://portal.azure.com), clique em do serviço de aplicações >  **&lt;any_app >** > **descrição geral**.

2. Clique em **... Mais** > **perfil de publicação de reposição**. Clique em **Sim** tooconfirm Olá repor.

    a ação repor Olá invalida qualquer anteriormente transferidos. Ficheiros PublishSettings.

## <a name="next-steps"></a>Passos seguintes

Saiba como toouse toodeploy estas credenciais a aplicação da [local Git](app-service-deploy-local-git.md) ou utilizando [FTP/S](app-service-deploy-ftp.md).
