---
title: "aaaMove recursos do Azure toonew subscrição ou grupo de recursos | Microsoft Docs"
description: "Utilize o Azure Resource Manager toomove recursos tooa novo grupo de recursos ou subscrição."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Mover grupo de recursos de toonew de recursos ou subscrição
Este tópico mostra como toomove recursos tooeither uma nova subscrição ou um novo recurso do grupo no Olá mesma subscrição. Pode utilizar o portal de Olá, do PowerShell, CLI do Azure ou Olá recursos toomove de REST API. as operações de movimentação de Olá neste tópico são tooyou disponível sem qualquer assistência a partir do suporte do Azure.

Quando move recursos, o grupo de Olá de origem e o grupo de destino Olá estão bloqueados durante a operação de Olá. Escrever e operações de eliminação são bloqueados Olá dos grupos de recursos, até concluir a movimentação de Olá. Este bloqueio significa não é possível adicionar, atualizar ou eliminar recursos em grupos de recursos de Olá, mas não significa recursos Olá são interrompidos. Por exemplo, se mover um SQL Server e a respetivo base de dados tooa novo grupo de recursos, uma aplicação que utiliza a base de dados de Olá não ocorre nenhum período de indisponibilidade. Pode ainda ler e escrever toohello base de dados.

Não é possível alterar a localização de Olá de recurso de Olá. Mover um recurso só move-tooa novo grupo de recursos. novo grupo de recursos Olá pode ter uma localização diferente, mas que não alterar a localização de Olá do recurso de Olá.

> [!NOTE]
> Este artigo descreve como conta offering toomove recursos dentro de um Azure existente. Se quiser toochange, na verdade, a conta do Azure offering (como atualizar do pagamento de toopre pay as you go) ao continuar toowork com os seus recursos existentes, consulte [mudar a sua oferta tooanother de subscrição do Azure](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Lista de verificação antes de mover os recursos
Existem algumas tooperform as etapas importantes antes de mover um recurso. Ao confirmar estas condições, pode evitar erros.

1. Olá subscrições de origem e de destino tem de existir na Olá mesmo [inquilino do Azure Active Directory](../active-directory/active-directory-howto-tenant.md). toocheck que ambas as subscrições têm Olá mesmo ID de inquilino, utilize o Azure PowerShell ou a CLI do Azure.

  Para o Azure PowerShell, utilize:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Para o Azure CLI 2.0, utilize:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Se Olá inquilino IDs para subscrições de origem e destino Olá não são Olá mesmo, a tentativa de diretório de Olá toochange para subscrição Olá. No entanto, esta opção está apenas disponível tooService administradores que estão assinados com uma conta Microsoft (não uma conta institucional). tooattempt alterar o diretório de Olá, inicie sessão toohello [portal clássico](https://manage.windowsazure.com/)e selecione **definições**e selecionar a subscrição de Olá. Se hello **Editar diretório** ícone está disponível, selecione-toochange Olá associados do Azure Active Directory.

  ![Editar diretório](./media/resource-group-move-resources/edit-directory.png)

  Ícone de que não esteja disponível, tem de contactar o suporte toomove Olá recursos tooa novo inquilino.

2. serviço de Olá tem de ativar a recursos de toomove Olá capacidade. Este tópico lista os serviços de ativar a mover recursos e os serviços não ative a mover recursos.
3. subscrição de destino Olá tem de estar registada para o fornecedor de recursos de Olá do recurso de Olá a ser movido. Se não, receberá um erro a indicar que Olá **subscrição não está registada para um tipo de recurso**. Poderá encontrar este problema ao mover uma recurso tooa nova subscrição, mas essa subscrição nunca foi utilizada com esse tipo de recurso. toolearn como toocheck Olá estado do registo e registar fornecedores de recursos, consulte [fornecedores de recursos e tipos](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Quando toocall suportar
Pode mover a maioria dos recursos através de operações de self-service de Olá apresentadas neste tópico. Utilize Olá self-service operações:

* Mover recursos do Resource Manager.
* Mover recursos clássicos toohello de acordo com [limitações de implementação clássica](#classic-deployment-limitations).

Contacte o suporte quando é necessário:

* Mova os recursos tooa nova conta e do Azure (inquilino do Azure Active Directory).
* Mover recursos clássicos mas estão a ter problemas com as limitações de Olá.

## <a name="services-that-enable-move"></a>Serviços que permitem mover
Por agora, os serviços de Olá que permitem mover tooboth um novo grupo de recursos e subscrição são:

* Gestão de API
* Aplicações de serviço de aplicações (aplicações web) - consulte [limitações do serviço de aplicações](#app-service-limitations)
* Application Insights
* Automatização
* Batch
* Bing Maps
* CDN
* Serviços em nuvem - consulte [limitações de implementação clássica](#classic-deployment-limitations)
* Serviços Cognitivos
* Content Moderator
* Catálogo de Dados
* Data Factory
* Data Lake Analytics
* Data Lake Store
* DNS
* Azure Cosmos DB
* Event Hubs
* Clusters do HDInsight - consulte [limitações do HDInsight](#hdinsight-limitations)
* Hubs IoT
* Cofre de Chaves
* Balanceadores de carga
* Aplicações Lógicas
* Machine Learning
* Serviços de Multimédia
* Mobile Engagement
* Hubs de Notificação
* Informações Operacionais
* Gestão de Operações
* Power BI
* Cache de Redis
* Scheduler
* Pesquisa
* Gestão de Servidores
* Service Bus
* Service Fabric
* Armazenamento
* Armazenamento (clássica) - consulte [limitações de implementação clássica](#classic-deployment-limitations)
* Estado do Stream Analytics - Stream Analytics não não possível mover as tarefas em execução.
* Servidor de base de dados do SQL Server - hello base de dados e servidor têm de residir no Olá mesmo grupo de recursos. Quando move um SQL server, todas as suas bases de dados também são movidas.
* Gestor de Tráfego
* Virtual Machines
* Máquinas virtuais com certificado armazenado no Cofre de chaves - mover grupo de recursos de toonew na mesma subscrição está ativada, mas mover subscrição cruzada não está ativada.
* Máquinas virtuais (clássicas) - consulte [limitações de implementação clássica](#classic-deployment-limitations)
* Conjuntos de Dimensionamento de Máquinas Virtuais
* Não é possível mover o redes virtuais - atualmente, uma rede Virtual em modo de peering, até que o VNet peering foi desativado. Depois de desativar, Olá rede Virtual pode ser movida com êxito e Olá o VNet peering pode ser ativado. Além disso, uma rede Virtual não pode ser movida tooa uma subscrição diferente se Olá rede Virtual contém nenhuma sub-rede com ligações de navegação de recursos. Por exemplo, uma sub-rede de rede Virtual tem uma ligação de navegação de recursos quando um recurso de redis Microsoft.Cache é implementado para esta sub-rede.
* Gateway de VPN


## <a name="services-that-do-not-enable-move"></a>Serviços que não ative a mover
Serviços de Olá que atualmente não permitem mover um recurso são:

* Serviços de domínio do AD
* Serviço de estado de funcionamento de AD híbrido
* Gateway de Aplicação
* Conjuntos de disponibilidade com máquinas virtuais com discos geridos
* Serviços BizTalk
* Serviço de Contentor
* ExpressRoute
* DevTest Labs - mover grupo de recursos de toonew na mesma subscrição está ativado, mas cruzada movimentação da subscrição não está ativado.
* Dynamics LCS
* Imagens de criada a partir de discos geridos
* Managed Disks
* Aplicações geridas
* Cofre dos serviços de recuperação - também não move Olá computação, rede e armazenamento recursos associados Olá a serviços de recuperação cofre, consulte [limitações de serviços de recuperação](#recovery-services-limitations).
* Segurança
* Instantâneos criados a partir de discos geridos
* Gestor de dispositivos do StorSimple
* Máquinas virtuais com discos geridos
* Redes virtuais (clássicas) - consulte [limitações de implementação clássica](#classic-deployment-limitations)
* Máquinas virtuais criadas a partir dos recursos de mercado - não é possível mover entre subscrições. Tem de recurso toobe desaprovisionada na subscrição atual Olá e implementado novamente numa nova subscrição de Olá

## <a name="app-service-limitations"></a>Limitações do serviço de aplicações
Ao trabalhar com aplicações do App Service, não é possível mover um plano de serviço aplicacional. aplicações do App Service toomove, as opções são:

* Mova Olá plano do App Service e todos os outros recursos do serviço de aplicações que recursos grupo tooa novo grupo de recursos que ainda não tenham recursos do serviço de aplicações. Este requisito significa que tem de mover mesmo Olá recursos do serviço de aplicações que não estão associados com Olá plano do App Service.
* Mover Olá aplicações tooa noutro grupo de recursos, mas manter todos os planos de serviço de aplicações no grupo de recursos Olá original.

Hello do serviço de aplicações plano não precisa de tooreside no Olá mesmo grupo de recursos como aplicação Olá para Olá aplicação toofunction corretamente.

Por exemplo, se o grupo de recursos contém:

* **Web-a** que se encontra associado **plano-a**
* **Web-b** que se encontra associado **plano-b**

As opções são:

* Mover **web-a**, **um plano**, **web-b**, e **plano-b**
* Mover **web-a** e **web-b**
* Mover **web-a**
* Mover **web-b**

Todas as outras combinações de envolvem deixando de um tipo de recurso que não pode ser deixado atrás, ao mover um plano de serviço de aplicações (qualquer tipo de recurso de serviço de aplicações).

Se a aplicação web reside num grupo de recursos diferente que o plano de serviço de aplicações, mas quiser toomove ambas tooa novo grupo de recursos, tem de efetuar Olá move em dois passos. Por exemplo:

* **Web-a** reside no **web-grupo**
* **um plano** reside no **plano-grupo**
* Pretende **web-a** e **um plano** tooreside no **grupo combinados**

tooaccomplish isto mover, efetuar duas operações de movimentação separado no Olá seguinte sequência:

1. Mover Olá **web-a** demasiado**plano-grupo**
2. Mover **web-a** e **um plano** demasiado**grupo combinado**.

Pode mover um certificado de serviço de aplicação tooa novo grupo de recursos ou subscrição sem quaisquer problemas. No entanto, se a sua aplicação web inclui um certificado SSL que comprou externamente e carregado toohello aplicação, tem de eliminar o certificado de Olá antes de aplicação de web de Olá mover. Por exemplo, pode efetuar Olá os seguintes passos:

1. Eliminar o certificado de Olá carregado de aplicação web de Olá
2. Mover Olá web app
3. Carregar a aplicação web do Olá certificado toohello

## <a name="recovery-services-limitations"></a>Limitações de serviços de recuperação
Mover não está ativada para armazenamento, rede, ou recursos de computação utilizada tooset segurança de recuperação após desastre com o Azure Site Recovery.

Por exemplo, suponha que configurou a replicação da sua conta de armazenamento de tooa de máquinas no local (Storage1) e pretende Olá protegido máquina toocome cópias de segurança após a ativação pós-falha tooAzure como uma máquina virtual (VM1) ligado tooa de rede virtual (Network1). Não é possível mover qualquer um destes recursos do Azure - Storage1, VM1, e Network1 - em recursos agrupa dentro Olá mesma subscrição ou nas subscrições.

## <a name="hdinsight-limitations"></a>Limitações do HDInsight

Pode mover tooa de clusters do HDInsight-nova subscrição ou grupo de recursos. No entanto, não é possível mover entre Olá subscrições redes de cluster do HDInsight toohello ligado recursos (por exemplo, a rede virtual Olá, NIC ou Balanceador de carga). Além disso, não é possível mover tooa novo grupo de recursos uma NIC que está a máquina virtual de tooa ligado para o cluster de Olá.

Quando move uma HDInsight cluster tooa nova subscrição, mova primeiro outros recursos (como a conta de armazenamento Olá). Em seguida, mova o cluster do HDInsight Olá por si só.

## <a name="classic-deployment-limitations"></a>Limitações de implementação clássica
Olá opções para mover recursos implementados através do modelo clássico Olá divergir com base em se estiver a mover recursos Olá dentro de uma subscrição ou tooa nova subscrição.

### <a name="same-subscription"></a>Mesma subscrição
Quando move os recursos do grupo de recursos do recurso de um grupo tooanother dentro da mesma subscrição, Olá seguintes restrições aplicam-se de Olá:

* Não não possível mover a redes virtuais (clássica).
* Máquinas virtuais (clássicas) têm de ser movidas com o serviço de nuvem Olá.
* Só é possível mover o serviço em nuvem quando mover Olá inclui todas as respetivas máquinas virtuais.
* Serviço de uma nuvem apenas pode ser movido de cada vez.
* Apenas uma conta de armazenamento (clássica) pode ser movida de cada vez.
* Não é possível mover a conta de armazenamento (clássica) na Olá mesma operação com uma máquina virtual ou um serviço em nuvem.

toomove recursos clássicos tooa novo grupo de recursos dentro Olá mesma subscrição, utilize operações de movimentação padrão Olá através de Olá [portal](#use-portal), [Azure PowerShell](#use-powershell), [CLI do Azure](#use-azure-cli), ou [REST API](#use-rest-api). Utilizar Olá mesmas operações como a utilizar para mover recursos do Resource Manager.

### <a name="new-subscription"></a>Nova subscrição
Ao mover a nova subscrição tooa de recursos, aplicam-se Olá seguintes restrições:

* Todos os recursos clássicos na subscrição Olá têm de ser movidos Olá mesma operação.
* subscrição de destino Olá não pode conter quaisquer outros recursos clássicos.
* Mover Olá só pode ser pedido através de uma API de REST separado para move clássico. comandos de movimentação de Gestor de recursos Olá padrão não funcionam quando mover a nova subscrição tooa de recursos clássicos.

toomove recursos clássicos tooa nova subscrição, utilize Olá as operações REST que são recursos tooclassic específico. toouse REST, execute Olá os seguintes passos:

1. Verifique se a subscrição de origem Olá pode participar numa subscrição cruzada mover. Utilize Olá seguinte operação:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     No corpo do pedido de Olá, incluem:

  ```json
  {
    "role": "source"
  }
  ```

     resposta de Olá para a operação de validação de Olá está a ser Olá seguinte formato:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Verifique se a subscrição de destino Olá pode participar numa subscrição cruzada mover. Utilize Olá seguinte operação:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     No corpo do pedido de Olá, incluem:

  ```json
  {
    "role": "target"
  }
  ```

     resposta Olá está a ser Olá mesmo formato como validação de subscrição de origem Olá.
3. Se ambas as subscrições de passar pela validação, mova todos os recursos clássicos da subscrição de tooanother de uma subscrição com Olá seguinte operação:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    No corpo do pedido de Olá, incluem:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

operação de Olá pode ser executada durante vários minutos.

## <a name="use-portal"></a>Utilizar o portal
toomove recursos, selecione o grupo de recursos de Olá que contenha esses recursos e, em seguida, selecione Olá **mover** botão.

![Mover recursos](./media/resource-group-move-resources/select-move.png)

Selecione se estiver a mover Olá recursos tooa novo grupo de recursos ou uma nova subscrição.

Selecione Olá recursos toomove e grupo de recursos de destino Olá. Confirmar que tem de tooupdate scripts para estes recursos e selecione **OK**. Se tiver selecionado o ícone de subscrição de editar Olá no passo anterior Olá, também tem de selecionar a subscrição de destino Olá.

![Selecione um destino](./media/resource-group-move-resources/select-destination.png)

No **notificações**, verá que Olá mover a operação está em execução.

![Mostrar o estado de movimentação](./media/resource-group-move-resources/show-status.png)

Quando tiver concluído, será notificado do resultado de Olá.

![Mostrar resultado de movimentação](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>Utilizar o PowerShell
toomove existente grupo de recursos de tooanother de recursos ou subscrição, utilize Olá `Move-AzureRmResource` comando.

Olá primeiro exemplo mostra como toomove um recurso tooa novo grupo de recursos.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Olá segundo exemplo mostra como toomove vários recursos tooa novo grupo de recursos.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa nova subscrição, incluir um valor para Olá `DestinationSubscriptionId` parâmetro.

É-lhe perguntado tooconfirm que pretende que o toomove Olá especificado recursos.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Utilizar a CLI do Azure 2.0
toomove existente grupo de recursos de tooanother de recursos ou subscrição, utilize Olá `az resource move` comando. Fornece recursos Olá IDs de Olá toomove de recursos. Pode obter IDs de recurso com Olá os seguintes comandos:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Olá seguinte exemplo mostra como toomove um armazenamento conta tooa novo grupo de recursos. No Olá `--ids` parâmetro, forneça uma lista de valores separados por espaço de mensagens em fila de toomove de IDs de recurso Olá.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa nova subscrição, fornecer Olá `--destination-subscription-id` parâmetro.

## <a name="use-azure-cli-10"></a>Utilizar a CLI do Azure 1.0
toomove existente grupo de recursos de tooanother de recursos ou subscrição, utilize Olá `azure resource move` comando. Fornece recursos Olá IDs de Olá toomove de recursos. Pode obter IDs de recurso com Olá os seguintes comandos:

```azurecli
azure resource list -g sourceGroup --json
```

Que devolve Olá seguinte formato:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Olá seguinte exemplo mostra como toomove um armazenamento conta tooa novo grupo de recursos. No Olá `-i` parâmetro, forneça uma lista separada por vírgulas de toomove de IDs de recurso Olá.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

É-lhe perguntado tooconfirm que pretende que o toomove Olá recurso especificado.

## <a name="use-rest-api"></a>Utilizar API REST
grupo de recursos de tooanother toomove existente recursos ou subscrição, execute:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

No corpo do pedido de Olá, especifique o grupo de recursos de destino de Olá e Olá toomove de recursos. Para obter mais informações sobre a operação de REST de movimentação Olá, consulte [mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Passos seguintes
* toolearn sobre cmdlets do PowerShell para gerir a sua subscrição, consulte [utilizar o Azure PowerShell com o Resource Manager](powershell-azure-resource-manager.md).
* toolearn sobre os comandos da CLI do Azure para gerir a sua subscrição, consulte [Olá de utilizar a CLI do Azure com o Resource Manager](xplat-cli-azure-resource-manager.md).
* toolearn sobre funcionalidades portais para gerir a sua subscrição, consulte [utilizar Olá toomanage portal do Azure recursos](resource-group-portal.md).
* toolearn sobre a aplicação de recursos de tooyour a lógica da organização, consulte [utilizar etiquetas tooorganize os recursos](resource-group-using-tags.md).
