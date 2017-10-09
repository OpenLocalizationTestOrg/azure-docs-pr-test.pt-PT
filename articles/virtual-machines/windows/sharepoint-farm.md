---
title: farms de servidores do SharePoint aaaCreate no Azure | Microsoft Docs
description: "Crie rapidamente um novo farm do SharePoint 2013 ou SharePoint 2016 no Azure utilizando o Olá marketplace portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Criar farms de servidores do SharePoint utilizando Olá marketplace portal do Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Farms do SharePoint 2013
Olá Microsoft Azure portal do Marketplace, pode criar rapidamente previamente configuradas farms do SharePoint Server 2013. Este modo, pode poupar muito tempo quando precisar de um farm do SharePoint básico ou de elevada disponibilidade para um ambiente de desenvolvimento/teste, ou se estiver a avaliar o SharePoint Server 2013 como uma solução de colaboração para a sua organização.

> [!NOTE]
> Olá **Farm do SharePoint Server** foi removido um item na Olá Azure Marketplace de Olá portal do Azure. Foi substituído com Olá **não - HA Farm do SharePoint 2013** e **Farm do SharePoint 2013 HA** itens.
>
>

farm do SharePoint básico Olá é constituído por três máquinas virtuais nesta configuração.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

Pode utilizar esta configuração de farm para uma configuração para o desenvolvimento de aplicações do SharePoint simplificada ou avaliação de tempo do primeiro do SharePoint 2013.

toocreate Olá básica () SharePoint farm de três servidores:

1. Clique em [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Clique em **implementar**.
3. No Olá **não - HA Farm do SharePoint 2013** painel, clique em **criar**.
4. Especificar definições nos passos Olá Olá **criar não - HA Farm do SharePoint 2013** painel e, em seguida, clique em **criar**.

farm do SharePoint de elevada disponibilidade de Olá consiste em máquinas virtuais nove nesta configuração.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Pode utilizar este farm configuração tootest superiores cliente cargas, a elevada disponibilidade Olá externo de site do SharePoint e grupos de Disponibilidade AlwaysOn do SQL Server para um farm do SharePoint. Também pode utilizar esta configuração para o desenvolvimento de aplicações do SharePoint num ambiente de elevada disponibilidade.

farm de SharePoint do toocreate Olá elevada disponibilidade (nove servidor):

1. Clique em [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Clique em **implementar**.
3. No Olá **Farm do SharePoint 2013 HA** painel, clique em **criar**.
4. Especificar definições nos passos Olá sete Olá **criar 2013 HA Farm do SharePoint** painel e, em seguida, clique em **criar**.

> [!NOTE]
> Não é possível criar Olá **não - HA Farm do SharePoint 2013** ou **Farm do SharePoint 2013 HA** com uma versão de avaliação gratuita do Azure.
>
>

Olá portal do Azure cria ambos estes farms numa rede virtual apenas na nuvem com uma presença na web para a Internet. Não há nenhum site para site VPN ou ExpressRoute ligação tooyour back-rede da organização.

> [!NOTE]
> Quando criar Olá básico ou farms do SharePoint de elevada disponibilidade utilizando Olá portal do Azure, não é possível especificar um grupo de recursos existente. toowork em torno esta limitação, crie estas farms com o Azure PowerShell. Para obter mais informações, consulte [farms do SharePoint 2013 criar dev/teste com o Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Farms do SharePoint 2016
Consulte [neste artigo](https://technet.microsoft.com/library/mt723354.aspx) para Olá toobuild instruções de Olá seguinte servidor único SharePoint Server 2016 do farm.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Gestão de farms do SharePoint Olá
Pode administrar servidores Olá destas farms através de ligações de ambiente de trabalho remoto. Para obter mais informações, consulte [iniciar sessão na máquina virtual de toohello](quick-create-portal.md#connect-to-virtual-machine).

Site do SharePoint de Administração Central Olá, pode configurar os meus sites, aplicações do SharePoint e outras funcionalidades. Para obter mais informações, consulte [configurar SharePoint](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Passos seguintes
* Detetar adicionais [SharePoint configurações](https://technet.microsoft.com/library/dn635309.aspx) nos serviços de infraestrutura do Azure.
