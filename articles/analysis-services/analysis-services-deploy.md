---
title: aaaDeploy tooAzure Analysis Services utilizando o SSDT | Microsoft Docs
description: Saiba como toodeploy tooan um modelo em tabela do Azure Analysis Services server utilizando o SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Implementar um modelo a partir de SSDT
Depois de criar um servidor na sua subscrição do Azure, está pronto toodeploy um tooit de base de dados do modelo de tabela. Pode utilizar o SQL Server Data Tools (SSDT) toobuild e implementar um projeto de modelo em tabela que está a trabalhar. 

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciada, é necessário:

* **Servidor Analysis Services** no Azure. toolearn mais, consulte [criar um servidor de Analysis Services do Azure](analysis-services-create-server.md).
* **Projeto de modelo em tabela** no SSDT ou um modelo em tabela existente em Olá 1200 ou superior ao nível de compatibilidade. Nunca criou um? Tente Olá [tutorial de vendas modelação de tabela do Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).
* **Gateway no local** -se uma ou mais origens de dados estão no local na rede da sua organização, terá de tooinstall um [gateway de dados no local](analysis-services-gateway.md). gateway de Olá é necessário para o servidor na nuvem de Olá ligar tooyour no local origens tooprocess e atualize dados no modelo de Olá.

> [!TIP]
> Antes de implementar, certifique-se de que pode processar os dados de Olá nas suas tabelas. No SSDT, clique em **Modelo** > **Processar** > **Processar tudo**. Se o processamento falhar, a implementação não é efetuada com êxito.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy um modelo em tabela do SSDT

1. Antes de implementar, terá de nome do servidor tooget Olá. No **portal do Azure** > servidor > **descrição geral** > **nome do servidor**, nome do servidor de Olá de cópia.
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. No SSDT > **Explorador de soluções**, projeto do contexto Olá > **propriedades**. Em seguida, no **implementação** > **servidor** cole o nome do servidor Olá.   
   
    ![Colar o nome do servidor na propriedade de implementação do servidor](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. Em **Explorador de Soluções**, clique com o botão direito do rato em **Propriedades** e, em seguida, clique em **Implementar**. Poderá ser pedido toosign no tooAzure.
   
    ![Implementar tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Estado de implementação é apresentado na janela saída Olá e em implementar.
   
    ![Estado da implementação](./media/analysis-services-deploy/aas-deploy-status.png)

É tudo há tooit!


## <a name="troubleshooting"></a>Resolução de problemas
Se a implementação falhar quando os metadados de implementação, é provável porque SSDT não foi possível ligar o servidor de tooyour. Certifique-se de que pode ligar o servidor de tooyour com o SSMS. Em seguida, certifique-se Olá propriedade do servidor de implementação para o projeto de Olá está correto.

Se a implementação falhar numa tabela, é provável porque o servidor não foi possível ligar a origem de dados de tooa. Se a origem de dados no local na rede da sua organização, ser tooinstall se um [gateway de dados no local](analysis-services-gateway.md).

## <a name="next-steps"></a>Passos seguintes
Agora que tem o seu servidor do modelo em tabela tooyour implementado, está pronto tooconnect tooit. Pode [ligar tooit com o SSMS](analysis-services-manage.md) toomanage-lo. E, pode [ligar tooit utilizando uma ferramenta de cliente](analysis-services-connect.md) como Power BI, o Power BI Desktop, ou o Excel e o início a criação de relatórios.

