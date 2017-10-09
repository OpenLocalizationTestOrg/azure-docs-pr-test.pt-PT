---
title: aaaUse toodeploy portal do Azure recursos do Azure | Microsoft Docs
description: Utilize o portal do Azure e o Azure Resource Manager toodeploy os recursos.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Implementar recursos com modelos do Resource Manager e do Portal do Azure
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [CLI do Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Este tópico mostra como toouse Olá [portal do Azure](https://portal.azure.com) com [do Azure Resource Manager](resource-group-overview.md) toodeploy os recursos do Azure. toolearn sobre como gerir os recursos, consulte [recursos do Azure de gerir através do portal](resource-group-portal.md).

Atualmente, nem todos os serviço suporta hello portal ou do Resource Manager. Para esses serviços, terá de toouse Olá [portal clássico](https://manage.windowsazure.com). Para o estado de Olá de cada serviço, consulte [gráfico de disponibilidade de portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Criar grupo de recursos
1. toocreate um grupo de recursos vazio, selecione **novo** > **gestão** > **grupo de recursos**.
   
    ![Criar grupo de recursos em branco](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Atribua um nome e localização e, se necessário, selecione uma subscrição. Precisa de tooprovide uma localização para o grupo de recursos de Olá porque o grupo de recursos de Olá armazena os metadados sobre recursos de Olá. Por motivos de conformidade, poderá ser útil toospecify armazenar esses metadados. Em geral, recomendamos que especifique uma localização onde a maioria dos seus recursos irá residir. Utilizar Olá mesma localização pode simplificar o seu modelo.
   
    ![conjunto de valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Implementar recursos do Marketplace
Depois de criar um grupo de recursos, pode implementar recursos tooit de Olá Marketplace. Olá Marketplace fornece soluções previamente definidas para cenários comuns.

1. toostart uma implementação, selecione **novo** e Olá tipo de recurso que gostaria de toodeploy. Em seguida, procure para versão específica do Olá de recursos de Olá gostaria toodeploy.
   
    ![implementar recursos](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Se não vir solução específica Olá gostaria toodeploy, pode procurar Olá Marketplace-lo.
   
    ![marketplace de pesquisa](./media/resource-group-template-deploy-portal/search-resource.png)
3. Dependendo do tipo de Olá de recursos selecionado, tem uma coleção de propriedades relevantes tooset antes da implementação. Essas opções não são mostradas aqui, como que variam com base no tipo de recurso. Para todos os tipos, tem de selecionar um grupo de recursos de destino. imagem de Olá seguinte mostra como toocreate uma aplicação web e implementá-la toohello grupo de recursos que criou.
   
    ![Criar grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Em alternativa, pode decidir toocreate um grupo de recursos quando implementar os recursos. Selecione **criar nova** e atribua um nome de grupo de recursos de Olá.
   
    ![Criar novo grupo de recursos](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Começa a sua implementação. implementação de Olá pode demorar alguns minutos. Quando tiver concluído a implementação de Olá, verá uma notificação.
   
    ![Vista de notificação](./media/resource-group-template-deploy-portal/view-notification.png)
5. Depois de implementar os recursos, pode adicionar o grupo de recursos de toohello recursos mais utilizando Olá **adicionar** comando no painel do grupo de recursos de Olá.
   
    ![adicionar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Implementar recursos do modelo personalizado
Se pretender tooexecute uma implementação, mas não utilizar qualquer um dos modelos de Olá no Olá Marketplace, pode criar um modelo personalizado que define a infraestrutura de Olá para a sua solução. toolearn sobre a criação de modelos, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).

1. Selecione toodeploy um modelo personalizado através do portal Olá, **novo**e iniciar a pesquisa para **modelo de implementação** até que o pode selecionar opções de Olá.
   
    ![implementação do modelo de pesquisa](./media/resource-group-template-deploy-portal/search-template.png)
2. Selecione **modelo de implementação** a partir dos recursos disponíveis Olá.
   
    ![Selecione a implementação do modelo](./media/resource-group-template-deploy-portal/select-template.png)
3. Depois de iniciar a implementação do modelo Olá, abra o modelo em branco Olá que está disponível para personalizar.
   
    ![Criar modelo](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    No editor de Olá, adicione a sintaxe do Olá JSON que define os recursos de Olá pretende toodeploy. Selecione **guardar** quando terminar. Para obter orientações sobre a sintaxe JSON Olá de escrita, consulte [instruções do modelo do Resource Manager](resource-manager-template-walkthrough.md).
   
    ![editar modelo](./media/resource-group-template-deploy-portal/edit-template.png)
4. Em alternativa, pode selecionar um modelo pré-existente de Olá [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/). Estes modelos são contribuídos por Comunidade Olá. Estes incluem muitos cenários comuns e alguém adicionou um modelo que é semelhante toowhat que está a tentar toodeploy. Pode procurar Olá modelos toofind algo que corresponda ao seu cenário.
   
    ![Selecione o modelo de início rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Pode ver o modelo selecionado Olá num editor de Olá.
5. Depois de fornecer Olá todos os outros valores, selecione **criar** modelo de Olá toodeploy. 
   
    ![implementar modelo](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Implementar recursos a partir de um modelo guardado tooyour conta
portal Olá permite toosave tooyour um modelo conta do Azure e volte a implementá-lo mais tarde. Para obter mais informações sobre como trabalhar com estes guardar modelos, [introdução ao modelos privados no portal do Azure de Olá](../marketplace-consumer/mytemplates-getstarted.md).

1. Selecione os modelos guardados de toofind **procurar** > **modelos**.
   
    ![Procurar modelos](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Na lista de Olá dos modelos guardado tooyour conta, selecione Olá um desejar toowork no.
   
    ![modelos guardados](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Selecione **implementar** tooredeploy guardar este modelo.
   
    ![implementar a modelo guardado](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Passos seguintes
* consulte os registos de auditoria tooview, [auditar operações com o Resource Manager](resource-group-audit.md).
* tootroubleshoot erros de implementação, consulte [ver as operações de implementação](resource-manager-deployment-operations.md).
* tooretrieve um modelo a partir de uma implementação ou o grupo de recursos, consulte [modelo de exportar o Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).
* Para obter orientações sobre como as empresas podem utilizar o Gestor de recursos tooeffectively gerir subscrições, consulte [andaime enterprise do Azure - governação de subscrição prescritiva](resource-manager-subscription-governance.md).

