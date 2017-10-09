---
title: "aaaIntegrate da automatização do Azure com o controlo de origem do Visual Stuido Team Services | Microsoft Docs"
description: "Cenário explica como configurar a integração com uma conta de automatização do Azure e o controlo de origem do Visual Stuido Team Services."
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "o Azure powershell, VSTS, controlo de código fonte, automatização"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Cenário de automatização do Azure – integração de controlo de origem de automatização com o Visual Studio Team Services

Neste cenário, tem um projeto do Visual Studio Team Services que está a utilizar runbooks de automatização do Azure toomanage ou configurações de DSC sob o controlo de origem.
Este artigo descreve como toointegrate VSTS com o seu ambiente de automatização do Azure para essa integração contínua acontece para cada verificação.

## <a name="getting-hello-scenario"></a>Ao obter cenário de Olá

Este cenário é composta por dois runbooks do PowerShell que pode importar diretamente a partir de Olá [Galeria de Runbooks](automation-runbook-gallery.md) no Olá portal do Azure ou transferir a partir de Olá [galeria do PowerShell](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Descrição| 
--------|------------|
VSTS de sincronização | Importar runbooks ou configurações de controlo de origem VSTS quando é efetuado um verificação-in. Se executar manualmente, irá importar e publicar todos os runbooks ou configurações para Olá conta de automatização.| 
Sincronização VSTSGit | Importar runbooks ou configurações de VSTS sob o controlo de origem do Git quando é efetuado um verificação-in. Se executar manualmente, irá importar e publicar todos os runbooks ou configurações para Olá conta de automatização.|

### <a name="variables"></a>Variáveis

Variável | Descrição|
-----------|------------|
VSToken | Recurso de variável seguro criará que contém o token de acesso pessoal VSTS Olá. Pode saber como toocreate aceder um pessoal VSTS token no Olá [página de autenticação VSTS](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Instalar e configurar este cenário

Criar um [token de acesso pessoal](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) no VSTS que irá utilizar toosync Olá runbooks ou configurações na sua conta de automatização.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Criar um [variável segura](automation-variables.md) no seu Olá de toohold de conta de automatização de acesso pessoal token para que o runbook Olá pode autenticar runbooks de Olá tooVSTS e sync ou configurações para Olá conta de automatização. Pode atribuir o nome deste VSToken. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Importe runbook Olá que irá sincronizar os runbooks ou configurações para a conta de automatização Olá. Pode utilizar Olá [runbook de exemplo VSTS](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) ou Olá [VSTS com o runbook de exemplo do Git] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) de Olá PowerShellGallery.com dependendo se utilizar VSTS origem de controlo ou VSTS com o Git e implemente tooyour conta de automatização.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

Agora, pode [publicar](automation-creating-importing-runbook.md#publishing-a-runbook) este runbook para que possa criar um webhook. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Criar um [webhook](automation-webhooks.md) para este runbook VSTS de sincronização e preencha os parâmetros Olá, conforme mostrado abaixo. Certifique-se que copiar o url do webhook Olá pois terá para um hook de serviço no VSTS. Olá VSAccessTokenVariableName é o nome de Olá (VSToken) da variável segura Olá que criou o token de acesso pessoal de Olá toohold anterior. 

Integração com VSTS (sincronização-VSTS.ps1) irá demorar Olá seguir os parâmetros.
### <a name="sync-vsts-parameters"></a>Parâmetros de sincronização VSTS

Parâmetro | Descrição| 
--------|------------|
WebhookData | Isto contêm Olá checkin informações enviadas pelo Olá VSTS serviço hook. Deve deixar este parâmetro em branco.| 
ResourceGroup | Este é o nome de Olá Olá do grupo de recursos que a conta de automatização Olá.|
AutomationAccountName | nome da conta de automatização de Olá que serão sincronizados com VSTS Olá.|
VSFolder | O nome da pasta de Olá no VSTS onde existem Olá runbooks e configurações.|
VSAccount | nome de Olá do Olá conta Visual Studio Team Services.| 
VSAccessTokenVariableName | nome de Olá de Olá segura variável (VSToken) que contém o token de acesso pessoal VSTS Olá.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Se estiver a utilizar VSTS com o GIT (sincronização-VSTSGit.ps1) irá demorar Olá seguir os parâmetros.

Parâmetro | Descrição|
--------|------------|
WebhookData | Isto contêm Olá checkin informações enviadas pelo Olá VSTS serviço hook. Deve deixar este parâmetro em branco.| ResourceGroup | Este nome de Olá Olá do grupo de recursos que a conta de automatização Olá.|
AutomationAccountName | nome da conta de automatização de Olá que serão sincronizados com VSTS Olá.|
VSAccount | nome de Olá do Olá conta Visual Studio Team Services.|
VSProject | nome de Olá do projeto de Olá no VSTS onde existem Olá runbooks e configurações.|
GitRepo | nome do repositório de Git Olá Olá.|
GitBranch | nome de Olá do ramo de Olá no repositório de VSTS Git.|
Pasta | nome de Olá da pasta de Olá no VSTS Git ramo.|
VSAccessTokenVariableName | nome de Olá de Olá segura variável (VSToken) que contém o token de acesso pessoal VSTS Olá.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Crie um hook de serviço no VSTS para a pasta de toohello de verificação-ins que aciona o webhook na entrada código. Selecione Web Hooks como Olá serviço toointegrate com quando cria uma nova subscrição. Pode saber mais sobre o serviço hooks na [documentação VSTS serviço Hooks](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

Deve agora ser capaz de toodo todos os inícios verificação dos seus runbooks e configurações no VSTS e ter estes automaticamente sincronizar tinha na sua conta de automatização.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Se executar este runbook manualmente sem a ser acionado por VSTS, pode deixar parâmetro de webhookdata Olá vazio e executará uma sincronização completa da pasta VSTS Olá especificada.

Se desejar toouninstall cenário de Olá, remover um hook de serviço Olá VSTS, eliminar Olá runbook e Olá VSToken variável.
