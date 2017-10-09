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
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="a6f9c-103">Mover grupo de recursos de toonew de recursos ou subscrição</span><span class="sxs-lookup"><span data-stu-id="a6f9c-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="a6f9c-104">Este tópico mostra como toomove recursos tooeither uma nova subscrição ou um novo recurso do grupo no Olá mesma subscrição.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="a6f9c-105">Pode utilizar o portal de Olá, do PowerShell, CLI do Azure ou Olá recursos toomove de REST API.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="a6f9c-106">as operações de movimentação de Olá neste tópico são tooyou disponível sem qualquer assistência a partir do suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="a6f9c-107">Quando move recursos, o grupo de Olá de origem e o grupo de destino Olá estão bloqueados durante a operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="a6f9c-108">Escrever e operações de eliminação são bloqueados Olá dos grupos de recursos, até concluir a movimentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="a6f9c-109">Este bloqueio significa não é possível adicionar, atualizar ou eliminar recursos em grupos de recursos de Olá, mas não significa recursos Olá são interrompidos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="a6f9c-110">Por exemplo, se mover um SQL Server e a respetivo base de dados tooa novo grupo de recursos, uma aplicação que utiliza a base de dados de Olá não ocorre nenhum período de indisponibilidade.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="a6f9c-111">Pode ainda ler e escrever toohello base de dados.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="a6f9c-112">Não é possível alterar a localização de Olá de recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="a6f9c-113">Mover um recurso só move-tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="a6f9c-114">novo grupo de recursos Olá pode ter uma localização diferente, mas que não alterar a localização de Olá do recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="a6f9c-115">Este artigo descreve como conta offering toomove recursos dentro de um Azure existente.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="a6f9c-116">Se quiser toochange, na verdade, a conta do Azure offering (como atualizar do pagamento de toopre pay as you go) ao continuar toowork com os seus recursos existentes, consulte [mudar a sua oferta tooanother de subscrição do Azure](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="a6f9c-117">Lista de verificação antes de mover os recursos</span><span class="sxs-lookup"><span data-stu-id="a6f9c-117">Checklist before moving resources</span></span>
<span data-ttu-id="a6f9c-118">Existem algumas tooperform as etapas importantes antes de mover um recurso.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="a6f9c-119">Ao confirmar estas condições, pode evitar erros.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="a6f9c-120">Olá subscrições de origem e de destino tem de existir na Olá mesmo [inquilino do Azure Active Directory](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="a6f9c-121">toocheck que ambas as subscrições têm Olá mesmo ID de inquilino, utilize o Azure PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="a6f9c-122">Para o Azure PowerShell, utilize:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="a6f9c-123">Para o Azure CLI 2.0, utilize:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="a6f9c-124">Se Olá inquilino IDs para subscrições de origem e destino Olá não são Olá mesmo, a tentativa de diretório de Olá toochange para subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="a6f9c-125">No entanto, esta opção está apenas disponível tooService administradores que estão assinados com uma conta Microsoft (não uma conta institucional).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="a6f9c-126">tooattempt alterar o diretório de Olá, inicie sessão toohello [portal clássico](https://manage.windowsazure.com/)e selecione **definições**e selecionar a subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="a6f9c-127">Se hello **Editar diretório** ícone está disponível, selecione-toochange Olá associados do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![Editar diretório](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="a6f9c-129">Ícone de que não esteja disponível, tem de contactar o suporte toomove Olá recursos tooa novo inquilino.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="a6f9c-130">serviço de Olá tem de ativar a recursos de toomove Olá capacidade.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="a6f9c-131">Este tópico lista os serviços de ativar a mover recursos e os serviços não ative a mover recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="a6f9c-132">subscrição de destino Olá tem de estar registada para o fornecedor de recursos de Olá do recurso de Olá a ser movido.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="a6f9c-133">Se não, receberá um erro a indicar que Olá **subscrição não está registada para um tipo de recurso**.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="a6f9c-134">Poderá encontrar este problema ao mover uma recurso tooa nova subscrição, mas essa subscrição nunca foi utilizada com esse tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="a6f9c-135">toolearn como toocheck Olá estado do registo e registar fornecedores de recursos, consulte [fornecedores de recursos e tipos](resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="a6f9c-136">Quando toocall suportar</span><span class="sxs-lookup"><span data-stu-id="a6f9c-136">When toocall support</span></span>
<span data-ttu-id="a6f9c-137">Pode mover a maioria dos recursos através de operações de self-service de Olá apresentadas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="a6f9c-138">Utilize Olá self-service operações:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="a6f9c-139">Mover recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="a6f9c-140">Mover recursos clássicos toohello de acordo com [limitações de implementação clássica](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="a6f9c-141">Contacte o suporte quando é necessário:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-141">Call support when you need to:</span></span>

* <span data-ttu-id="a6f9c-142">Mova os recursos tooa nova conta e do Azure (inquilino do Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="a6f9c-143">Mover recursos clássicos mas estão a ter problemas com as limitações de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="a6f9c-144">Serviços que permitem mover</span><span class="sxs-lookup"><span data-stu-id="a6f9c-144">Services that enable move</span></span>
<span data-ttu-id="a6f9c-145">Por agora, os serviços de Olá que permitem mover tooboth um novo grupo de recursos e subscrição são:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="a6f9c-146">Gestão de API</span><span class="sxs-lookup"><span data-stu-id="a6f9c-146">API Management</span></span>
* <span data-ttu-id="a6f9c-147">Aplicações de serviço de aplicações (aplicações web) - consulte [limitações do serviço de aplicações](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="a6f9c-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="a6f9c-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6f9c-148">Application Insights</span></span>
* <span data-ttu-id="a6f9c-149">Automatização</span><span class="sxs-lookup"><span data-stu-id="a6f9c-149">Automation</span></span>
* <span data-ttu-id="a6f9c-150">Batch</span><span class="sxs-lookup"><span data-stu-id="a6f9c-150">Batch</span></span>
* <span data-ttu-id="a6f9c-151">Bing Maps</span><span class="sxs-lookup"><span data-stu-id="a6f9c-151">Bing Maps</span></span>
* <span data-ttu-id="a6f9c-152">CDN</span><span class="sxs-lookup"><span data-stu-id="a6f9c-152">CDN</span></span>
* <span data-ttu-id="a6f9c-153">Serviços em nuvem - consulte [limitações de implementação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="a6f9c-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="a6f9c-154">Serviços Cognitivos</span><span class="sxs-lookup"><span data-stu-id="a6f9c-154">Cognitive Services</span></span>
* <span data-ttu-id="a6f9c-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="a6f9c-155">Content Moderator</span></span>
* <span data-ttu-id="a6f9c-156">Catálogo de Dados</span><span class="sxs-lookup"><span data-stu-id="a6f9c-156">Data Catalog</span></span>
* <span data-ttu-id="a6f9c-157">Data Factory</span><span class="sxs-lookup"><span data-stu-id="a6f9c-157">Data Factory</span></span>
* <span data-ttu-id="a6f9c-158">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a6f9c-158">Data Lake Analytics</span></span>
* <span data-ttu-id="a6f9c-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a6f9c-159">Data Lake Store</span></span>
* <span data-ttu-id="a6f9c-160">DNS</span><span class="sxs-lookup"><span data-stu-id="a6f9c-160">DNS</span></span>
* <span data-ttu-id="a6f9c-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a6f9c-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="a6f9c-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a6f9c-162">Event Hubs</span></span>
* <span data-ttu-id="a6f9c-163">Clusters do HDInsight - consulte [limitações do HDInsight](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="a6f9c-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="a6f9c-164">Hubs IoT</span><span class="sxs-lookup"><span data-stu-id="a6f9c-164">IoT Hubs</span></span>
* <span data-ttu-id="a6f9c-165">Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="a6f9c-165">Key Vault</span></span>
* <span data-ttu-id="a6f9c-166">Balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="a6f9c-166">Load Balancers</span></span>
* <span data-ttu-id="a6f9c-167">Aplicações Lógicas</span><span class="sxs-lookup"><span data-stu-id="a6f9c-167">Logic Apps</span></span>
* <span data-ttu-id="a6f9c-168">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a6f9c-168">Machine Learning</span></span>
* <span data-ttu-id="a6f9c-169">Serviços de Multimédia</span><span class="sxs-lookup"><span data-stu-id="a6f9c-169">Media Services</span></span>
* <span data-ttu-id="a6f9c-170">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a6f9c-170">Mobile Engagement</span></span>
* <span data-ttu-id="a6f9c-171">Hubs de Notificação</span><span class="sxs-lookup"><span data-stu-id="a6f9c-171">Notification Hubs</span></span>
* <span data-ttu-id="a6f9c-172">Informações Operacionais</span><span class="sxs-lookup"><span data-stu-id="a6f9c-172">Operational Insights</span></span>
* <span data-ttu-id="a6f9c-173">Gestão de Operações</span><span class="sxs-lookup"><span data-stu-id="a6f9c-173">Operations Management</span></span>
* <span data-ttu-id="a6f9c-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="a6f9c-174">Power BI</span></span>
* <span data-ttu-id="a6f9c-175">Cache de Redis</span><span class="sxs-lookup"><span data-stu-id="a6f9c-175">Redis Cache</span></span>
* <span data-ttu-id="a6f9c-176">Scheduler</span><span class="sxs-lookup"><span data-stu-id="a6f9c-176">Scheduler</span></span>
* <span data-ttu-id="a6f9c-177">Pesquisa</span><span class="sxs-lookup"><span data-stu-id="a6f9c-177">Search</span></span>
* <span data-ttu-id="a6f9c-178">Gestão de Servidores</span><span class="sxs-lookup"><span data-stu-id="a6f9c-178">Server Management</span></span>
* <span data-ttu-id="a6f9c-179">Service Bus</span><span class="sxs-lookup"><span data-stu-id="a6f9c-179">Service Bus</span></span>
* <span data-ttu-id="a6f9c-180">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a6f9c-180">Service Fabric</span></span>
* <span data-ttu-id="a6f9c-181">Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a6f9c-181">Storage</span></span>
* <span data-ttu-id="a6f9c-182">Armazenamento (clássica) - consulte [limitações de implementação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="a6f9c-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="a6f9c-183">Estado do Stream Analytics - Stream Analytics não não possível mover as tarefas em execução.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="a6f9c-184">Servidor de base de dados do SQL Server - hello base de dados e servidor têm de residir no Olá mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="a6f9c-185">Quando move um SQL server, todas as suas bases de dados também são movidas.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="a6f9c-186">Gestor de Tráfego</span><span class="sxs-lookup"><span data-stu-id="a6f9c-186">Traffic Manager</span></span>
* <span data-ttu-id="a6f9c-187">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="a6f9c-187">Virtual Machines</span></span>
* <span data-ttu-id="a6f9c-188">Máquinas virtuais com certificado armazenado no Cofre de chaves - mover grupo de recursos de toonew na mesma subscrição está ativada, mas mover subscrição cruzada não está ativada.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="a6f9c-189">Máquinas virtuais (clássicas) - consulte [limitações de implementação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="a6f9c-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="a6f9c-190">Conjuntos de Dimensionamento de Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="a6f9c-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="a6f9c-191">Não é possível mover o redes virtuais - atualmente, uma rede Virtual em modo de peering, até que o VNet peering foi desativado.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="a6f9c-192">Depois de desativar, Olá rede Virtual pode ser movida com êxito e Olá o VNet peering pode ser ativado.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="a6f9c-193">Além disso, uma rede Virtual não pode ser movida tooa uma subscrição diferente se Olá rede Virtual contém nenhuma sub-rede com ligações de navegação de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="a6f9c-194">Por exemplo, uma sub-rede de rede Virtual tem uma ligação de navegação de recursos quando um recurso de redis Microsoft.Cache é implementado para esta sub-rede.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="a6f9c-195">Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="a6f9c-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="a6f9c-196">Serviços que não ative a mover</span><span class="sxs-lookup"><span data-stu-id="a6f9c-196">Services that do not enable move</span></span>
<span data-ttu-id="a6f9c-197">Serviços de Olá que atualmente não permitem mover um recurso são:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="a6f9c-198">Serviços de domínio do AD</span><span class="sxs-lookup"><span data-stu-id="a6f9c-198">AD Domain Services</span></span>
* <span data-ttu-id="a6f9c-199">Serviço de estado de funcionamento de AD híbrido</span><span class="sxs-lookup"><span data-stu-id="a6f9c-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="a6f9c-200">Gateway de Aplicação</span><span class="sxs-lookup"><span data-stu-id="a6f9c-200">Application Gateway</span></span>
* <span data-ttu-id="a6f9c-201">Conjuntos de disponibilidade com máquinas virtuais com discos geridos</span><span class="sxs-lookup"><span data-stu-id="a6f9c-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="a6f9c-202">Serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="a6f9c-202">BizTalk Services</span></span>
* <span data-ttu-id="a6f9c-203">Serviço de Contentor</span><span class="sxs-lookup"><span data-stu-id="a6f9c-203">Container Service</span></span>
* <span data-ttu-id="a6f9c-204">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a6f9c-204">Express Route</span></span>
* <span data-ttu-id="a6f9c-205">DevTest Labs - mover grupo de recursos de toonew na mesma subscrição está ativado, mas cruzada movimentação da subscrição não está ativado.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="a6f9c-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="a6f9c-206">Dynamics LCS</span></span>
* <span data-ttu-id="a6f9c-207">Imagens de criada a partir de discos geridos</span><span class="sxs-lookup"><span data-stu-id="a6f9c-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="a6f9c-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="a6f9c-208">Managed Disks</span></span>
* <span data-ttu-id="a6f9c-209">Aplicações geridas</span><span class="sxs-lookup"><span data-stu-id="a6f9c-209">Managed Applications</span></span>
* <span data-ttu-id="a6f9c-210">Cofre dos serviços de recuperação - também não move Olá computação, rede e armazenamento recursos associados Olá a serviços de recuperação cofre, consulte [limitações de serviços de recuperação](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="a6f9c-211">Segurança</span><span class="sxs-lookup"><span data-stu-id="a6f9c-211">Security</span></span>
* <span data-ttu-id="a6f9c-212">Instantâneos criados a partir de discos geridos</span><span class="sxs-lookup"><span data-stu-id="a6f9c-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="a6f9c-213">Gestor de dispositivos do StorSimple</span><span class="sxs-lookup"><span data-stu-id="a6f9c-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="a6f9c-214">Máquinas virtuais com discos geridos</span><span class="sxs-lookup"><span data-stu-id="a6f9c-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="a6f9c-215">Redes virtuais (clássicas) - consulte [limitações de implementação clássica](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="a6f9c-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="a6f9c-216">Máquinas virtuais criadas a partir dos recursos de mercado - não é possível mover entre subscrições.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="a6f9c-217">Tem de recurso toobe desaprovisionada na subscrição atual Olá e implementado novamente numa nova subscrição de Olá</span><span class="sxs-lookup"><span data-stu-id="a6f9c-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="a6f9c-218">Limitações do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="a6f9c-218">App Service limitations</span></span>
<span data-ttu-id="a6f9c-219">Ao trabalhar com aplicações do App Service, não é possível mover um plano de serviço aplicacional.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="a6f9c-220">aplicações do App Service toomove, as opções são:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="a6f9c-221">Mova Olá plano do App Service e todos os outros recursos do serviço de aplicações que recursos grupo tooa novo grupo de recursos que ainda não tenham recursos do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="a6f9c-222">Este requisito significa que tem de mover mesmo Olá recursos do serviço de aplicações que não estão associados com Olá plano do App Service.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="a6f9c-223">Mover Olá aplicações tooa noutro grupo de recursos, mas manter todos os planos de serviço de aplicações no grupo de recursos Olá original.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="a6f9c-224">Hello do serviço de aplicações plano não precisa de tooreside no Olá mesmo grupo de recursos como aplicação Olá para Olá aplicação toofunction corretamente.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="a6f9c-225">Por exemplo, se o grupo de recursos contém:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="a6f9c-226">**Web-a** que se encontra associado **plano-a**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="a6f9c-227">**Web-b** que se encontra associado **plano-b**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="a6f9c-228">As opções são:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-228">Your options are:</span></span>

* <span data-ttu-id="a6f9c-229">Mover **web-a**, **um plano**, **web-b**, e **plano-b**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="a6f9c-230">Mover **web-a** e **web-b**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="a6f9c-231">Mover **web-a**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-231">Move **web-a**</span></span>
* <span data-ttu-id="a6f9c-232">Mover **web-b**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-232">Move **web-b**</span></span>

<span data-ttu-id="a6f9c-233">Todas as outras combinações de envolvem deixando de um tipo de recurso que não pode ser deixado atrás, ao mover um plano de serviço de aplicações (qualquer tipo de recurso de serviço de aplicações).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="a6f9c-234">Se a aplicação web reside num grupo de recursos diferente que o plano de serviço de aplicações, mas quiser toomove ambas tooa novo grupo de recursos, tem de efetuar Olá move em dois passos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="a6f9c-235">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-235">For example:</span></span>

* <span data-ttu-id="a6f9c-236">**Web-a** reside no **web-grupo**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="a6f9c-237">**um plano** reside no **plano-grupo**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="a6f9c-238">Pretende **web-a** e **um plano** tooreside no **grupo combinados**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="a6f9c-239">tooaccomplish isto mover, efetuar duas operações de movimentação separado no Olá seguinte sequência:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="a6f9c-240">Mover Olá **web-a** demasiado**plano-grupo**</span><span class="sxs-lookup"><span data-stu-id="a6f9c-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="a6f9c-241">Mover **web-a** e **um plano** demasiado**grupo combinado**.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="a6f9c-242">Pode mover um certificado de serviço de aplicação tooa novo grupo de recursos ou subscrição sem quaisquer problemas.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="a6f9c-243">No entanto, se a sua aplicação web inclui um certificado SSL que comprou externamente e carregado toohello aplicação, tem de eliminar o certificado de Olá antes de aplicação de web de Olá mover.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="a6f9c-244">Por exemplo, pode efetuar Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="a6f9c-245">Eliminar o certificado de Olá carregado de aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="a6f9c-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="a6f9c-246">Mover Olá web app</span><span class="sxs-lookup"><span data-stu-id="a6f9c-246">Move hello web app</span></span>
3. <span data-ttu-id="a6f9c-247">Carregar a aplicação web do Olá certificado toohello</span><span class="sxs-lookup"><span data-stu-id="a6f9c-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="a6f9c-248">Limitações de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="a6f9c-248">Recovery Services limitations</span></span>
<span data-ttu-id="a6f9c-249">Mover não está ativada para armazenamento, rede, ou recursos de computação utilizada tooset segurança de recuperação após desastre com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="a6f9c-250">Por exemplo, suponha que configurou a replicação da sua conta de armazenamento de tooa de máquinas no local (Storage1) e pretende Olá protegido máquina toocome cópias de segurança após a ativação pós-falha tooAzure como uma máquina virtual (VM1) ligado tooa de rede virtual (Network1).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="a6f9c-251">Não é possível mover qualquer um destes recursos do Azure - Storage1, VM1, e Network1 - em recursos agrupa dentro Olá mesma subscrição ou nas subscrições.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="a6f9c-252">Limitações do HDInsight</span><span class="sxs-lookup"><span data-stu-id="a6f9c-252">HDInsight limitations</span></span>

<span data-ttu-id="a6f9c-253">Pode mover tooa de clusters do HDInsight-nova subscrição ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="a6f9c-254">No entanto, não é possível mover entre Olá subscrições redes de cluster do HDInsight toohello ligado recursos (por exemplo, a rede virtual Olá, NIC ou Balanceador de carga).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="a6f9c-255">Além disso, não é possível mover tooa novo grupo de recursos uma NIC que está a máquina virtual de tooa ligado para o cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="a6f9c-256">Quando move uma HDInsight cluster tooa nova subscrição, mova primeiro outros recursos (como a conta de armazenamento Olá).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="a6f9c-257">Em seguida, mova o cluster do HDInsight Olá por si só.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="a6f9c-258">Limitações de implementação clássica</span><span class="sxs-lookup"><span data-stu-id="a6f9c-258">Classic deployment limitations</span></span>
<span data-ttu-id="a6f9c-259">Olá opções para mover recursos implementados através do modelo clássico Olá divergir com base em se estiver a mover recursos Olá dentro de uma subscrição ou tooa nova subscrição.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="a6f9c-260">Mesma subscrição</span><span class="sxs-lookup"><span data-stu-id="a6f9c-260">Same subscription</span></span>
<span data-ttu-id="a6f9c-261">Quando move os recursos do grupo de recursos do recurso de um grupo tooanother dentro da mesma subscrição, Olá seguintes restrições aplicam-se de Olá:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="a6f9c-262">Não não possível mover a redes virtuais (clássica).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="a6f9c-263">Máquinas virtuais (clássicas) têm de ser movidas com o serviço de nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="a6f9c-264">Só é possível mover o serviço em nuvem quando mover Olá inclui todas as respetivas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="a6f9c-265">Serviço de uma nuvem apenas pode ser movido de cada vez.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="a6f9c-266">Apenas uma conta de armazenamento (clássica) pode ser movida de cada vez.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="a6f9c-267">Não é possível mover a conta de armazenamento (clássica) na Olá mesma operação com uma máquina virtual ou um serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="a6f9c-268">toomove recursos clássicos tooa novo grupo de recursos dentro Olá mesma subscrição, utilize operações de movimentação padrão Olá através de Olá [portal](#use-portal), [Azure PowerShell](#use-powershell), [CLI do Azure](#use-azure-cli), ou [REST API](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="a6f9c-269">Utilizar Olá mesmas operações como a utilizar para mover recursos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="a6f9c-270">Nova subscrição</span><span class="sxs-lookup"><span data-stu-id="a6f9c-270">New subscription</span></span>
<span data-ttu-id="a6f9c-271">Ao mover a nova subscrição tooa de recursos, aplicam-se Olá seguintes restrições:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="a6f9c-272">Todos os recursos clássicos na subscrição Olá têm de ser movidos Olá mesma operação.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="a6f9c-273">subscrição de destino Olá não pode conter quaisquer outros recursos clássicos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="a6f9c-274">Mover Olá só pode ser pedido através de uma API de REST separado para move clássico.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="a6f9c-275">comandos de movimentação de Gestor de recursos Olá padrão não funcionam quando mover a nova subscrição tooa de recursos clássicos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="a6f9c-276">toomove recursos clássicos tooa nova subscrição, utilize Olá as operações REST que são recursos tooclassic específico.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="a6f9c-277">toouse REST, execute Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="a6f9c-278">Verifique se a subscrição de origem Olá pode participar numa subscrição cruzada mover.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="a6f9c-279">Utilize Olá seguinte operação:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="a6f9c-280">No corpo do pedido de Olá, incluem:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="a6f9c-281">resposta de Olá para a operação de validação de Olá está a ser Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="a6f9c-282">Verifique se a subscrição de destino Olá pode participar numa subscrição cruzada mover.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="a6f9c-283">Utilize Olá seguinte operação:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="a6f9c-284">No corpo do pedido de Olá, incluem:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="a6f9c-285">resposta Olá está a ser Olá mesmo formato como validação de subscrição de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="a6f9c-286">Se ambas as subscrições de passar pela validação, mova todos os recursos clássicos da subscrição de tooanother de uma subscrição com Olá seguinte operação:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="a6f9c-287">No corpo do pedido de Olá, incluem:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="a6f9c-288">operação de Olá pode ser executada durante vários minutos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="a6f9c-289">Utilizar o portal</span><span class="sxs-lookup"><span data-stu-id="a6f9c-289">Use portal</span></span>
<span data-ttu-id="a6f9c-290">toomove recursos, selecione o grupo de recursos de Olá que contenha esses recursos e, em seguida, selecione Olá **mover** botão.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![Mover recursos](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="a6f9c-292">Selecione se estiver a mover Olá recursos tooa novo grupo de recursos ou uma nova subscrição.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="a6f9c-293">Selecione Olá recursos toomove e grupo de recursos de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="a6f9c-294">Confirmar que tem de tooupdate scripts para estes recursos e selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="a6f9c-295">Se tiver selecionado o ícone de subscrição de editar Olá no passo anterior Olá, também tem de selecionar a subscrição de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![Selecione um destino](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="a6f9c-297">No **notificações**, verá que Olá mover a operação está em execução.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-297">In **Notifications**, you see that hello move operation is running.</span></span>

![Mostrar o estado de movimentação](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="a6f9c-299">Quando tiver concluído, será notificado do resultado de Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-299">When it has completed, you are notified of hello result.</span></span>

![Mostrar resultado de movimentação](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="a6f9c-301">Utilizar o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6f9c-301">Use PowerShell</span></span>
<span data-ttu-id="a6f9c-302">toomove existente grupo de recursos de tooanother de recursos ou subscrição, utilize Olá `Move-AzureRmResource` comando.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="a6f9c-303">Olá primeiro exemplo mostra como toomove um recurso tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="a6f9c-304">Olá segundo exemplo mostra como toomove vários recursos tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="a6f9c-305">toomove tooa nova subscrição, incluir um valor para Olá `DestinationSubscriptionId` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="a6f9c-306">É-lhe perguntado tooconfirm que pretende que o toomove Olá especificado recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="a6f9c-307">Utilizar a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a6f9c-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="a6f9c-308">toomove existente grupo de recursos de tooanother de recursos ou subscrição, utilize Olá `az resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="a6f9c-309">Fornece recursos Olá IDs de Olá toomove de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="a6f9c-310">Pode obter IDs de recurso com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="a6f9c-311">Olá seguinte exemplo mostra como toomove um armazenamento conta tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="a6f9c-312">No Olá `--ids` parâmetro, forneça uma lista de valores separados por espaço de mensagens em fila de toomove de IDs de recurso Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="a6f9c-313">toomove tooa nova subscrição, fornecer Olá `--destination-subscription-id` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="a6f9c-314">Utilizar a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="a6f9c-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="a6f9c-315">toomove existente grupo de recursos de tooanother de recursos ou subscrição, utilize Olá `azure resource move` comando.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="a6f9c-316">Fornece recursos Olá IDs de Olá toomove de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="a6f9c-317">Pode obter IDs de recurso com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="a6f9c-318">Que devolve Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-318">Which returns hello following format:</span></span>

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

<span data-ttu-id="a6f9c-319">Olá seguinte exemplo mostra como toomove um armazenamento conta tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="a6f9c-320">No Olá `-i` parâmetro, forneça uma lista separada por vírgulas de toomove de IDs de recurso Olá.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="a6f9c-321">É-lhe perguntado tooconfirm que pretende que o toomove Olá recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="a6f9c-322">Utilizar API REST</span><span class="sxs-lookup"><span data-stu-id="a6f9c-322">Use REST API</span></span>
<span data-ttu-id="a6f9c-323">grupo de recursos de tooanother toomove existente recursos ou subscrição, execute:</span><span class="sxs-lookup"><span data-stu-id="a6f9c-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="a6f9c-324">No corpo do pedido de Olá, especifique o grupo de recursos de destino de Olá e Olá toomove de recursos.</span><span class="sxs-lookup"><span data-stu-id="a6f9c-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="a6f9c-325">Para obter mais informações sobre a operação de REST de movimentação Olá, consulte [mover recursos](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6f9c-326">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a6f9c-326">Next steps</span></span>
* <span data-ttu-id="a6f9c-327">toolearn sobre cmdlets do PowerShell para gerir a sua subscrição, consulte [utilizar o Azure PowerShell com o Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="a6f9c-328">toolearn sobre os comandos da CLI do Azure para gerir a sua subscrição, consulte [Olá de utilizar a CLI do Azure com o Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="a6f9c-329">toolearn sobre funcionalidades portais para gerir a sua subscrição, consulte [utilizar Olá toomanage portal do Azure recursos](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="a6f9c-330">toolearn sobre a aplicação de recursos de tooyour a lógica da organização, consulte [utilizar etiquetas tooorganize os recursos](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="a6f9c-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
