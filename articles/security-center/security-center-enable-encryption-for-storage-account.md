---
title: "encriptação de aaaEnable para a conta de armazenamento no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá as recomendações do Centro de segurança do Azure * * ativar a encriptação para o Azure armazenamento conta *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="1105e-103">Ativar a encriptação para a conta de armazenamento do Azure no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="1105e-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="1105e-104">Centro de segurança do Azure poderá recomendar que ativar a encriptação do serviço de armazenamento do Azure para dados inativos.</span><span class="sxs-lookup"><span data-stu-id="1105e-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="1105e-105">Encriptação de serviço de armazenamento (SSE) funciona através da encriptação de dados de Olá quando é escrito tooAzure armazenamento e a desencriptação de dados de Olá antes da obtenção.</span><span class="sxs-lookup"><span data-stu-id="1105e-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="1105e-106">SSE atualmente só está disponível para Olá serviço Blob do Azure e pode ser utilizado para blobs de blocos, blobs de páginas e blobs de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="1105e-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="1105e-107">toolearn mais, consulte [encriptação do serviço de armazenamento para dados Inativos](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="1105e-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="1105e-108">Depois de ativar a encriptação, apenas novos dados são encriptados.</span><span class="sxs-lookup"><span data-stu-id="1105e-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="1105e-109">Os blobs existentes na sua conta de armazenamento de permanecer desencriptados.</span><span class="sxs-lookup"><span data-stu-id="1105e-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="1105e-110">os blobs existentes tooencrypt, consulte Olá [FAQ de encriptação do serviço de armazenamento](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="1105e-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="1105e-111">Encriptação do serviço de armazenamento só é suportada em contas de armazenamento do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1105e-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="1105e-112">Contas de armazenamento clássicas não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="1105e-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="1105e-113">Olá toounderstand clássico e modelos de implementação do Resource Manager, consulte [modelos de implementação do Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="1105e-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1105e-114">Este documento apresenta serviço Olá utilizando um exemplo de implementação.</span><span class="sxs-lookup"><span data-stu-id="1105e-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="1105e-115">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="1105e-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="1105e-116">Implementar a recomendação de Olá</span><span class="sxs-lookup"><span data-stu-id="1105e-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="1105e-117">No Olá **recomendações** painel, selecione **ativar a encriptação da conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="1105e-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="1105e-118">![Ativar a encriptação da conta de armazenamento][1]</span><span class="sxs-lookup"><span data-stu-id="1105e-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="1105e-119">Olá **ativar a encriptação de armazenamento** abre o painel.</span><span class="sxs-lookup"><span data-stu-id="1105e-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="1105e-120">Este painel apresenta uma lista de contas de armazenamento do Azure olá onde a encriptação de armazenamento está desativada.</span><span class="sxs-lookup"><span data-stu-id="1105e-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="1105e-121">Neste exemplo, vamos selecione **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="1105e-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="1105e-122">![Ativar a encriptação de armazenamento][2]</span><span class="sxs-lookup"><span data-stu-id="1105e-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="1105e-123">Olá **encriptação** painel **storageacct1** abre.</span><span class="sxs-lookup"><span data-stu-id="1105e-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="1105e-124">Selecione **ativada**.</span><span class="sxs-lookup"><span data-stu-id="1105e-124">Select **Enabled**.</span></span>
   <span data-ttu-id="1105e-125">![Painel de encriptação][3]</span><span class="sxs-lookup"><span data-stu-id="1105e-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="1105e-126">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1105e-126">Select **Save**.</span></span>

<span data-ttu-id="1105e-127">Agora que tiver ativado a encriptação de armazenamento para **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="1105e-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="1105e-128">Consultar também</span><span class="sxs-lookup"><span data-stu-id="1105e-128">See also</span></span>
<span data-ttu-id="1105e-129">Este documento mostrou como tooimplement Olá Centro de segurança recomendação "ativar encriptação para a conta de armazenamento do Azure."</span><span class="sxs-lookup"><span data-stu-id="1105e-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="1105e-130">toolearn mais informações sobre a encriptação do serviço de armazenamento do Azure, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="1105e-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="1105e-131">Encriptação do serviço de armazenamento do Azure para dados Inativos</span><span class="sxs-lookup"><span data-stu-id="1105e-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="1105e-132">toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="1105e-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="1105e-133">[Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) -Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="1105e-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="1105e-134">[Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) -Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.</span><span class="sxs-lookup"><span data-stu-id="1105e-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="1105e-135">[Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e respondeu.</span><span class="sxs-lookup"><span data-stu-id="1105e-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="1105e-136">[Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) -Saiba como recomendações ajudam a proteger os seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1105e-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1105e-137">[FAQ do Centro de segurança do Azure](security-center-faq.md) -encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="1105e-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="1105e-138">[Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) -encontre mensagens do Blogue acerca da segurança do Azure e conformidade.</span><span class="sxs-lookup"><span data-stu-id="1105e-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
