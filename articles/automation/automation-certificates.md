---
title: "aaaCertificate ativos na automatização do Azure | Microsoft Docs"
description: "Certificados podem ser armazenados em segurança na automatização do Azure para que possam ser acedidos por runbooks ou configurações de DSC tooauthenticate contra do Azure e recursos de terceiros.  Este artigo explica os detalhes de Olá de certificados e como toowork com os mesmos no texto e gráficos de criação."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="b85dc-104">Ativos de certificado na automatização do Azure</span><span class="sxs-lookup"><span data-stu-id="b85dc-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="b85dc-105">Certificados podem ser armazenados em segurança na automatização do Azure para que possam ser acedidos por runbooks ou configurações de DSC utilizando Olá **Get-AzureRmAutomationRmCertificate** atividade para recursos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b85dc-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="b85dc-106">Isto permite-lhe toocreate runbooks e configurações de DSC que utilizam certificados para autenticação ou adiciona-os recursos tooAzure ou de terceiros.</span><span class="sxs-lookup"><span data-stu-id="b85dc-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="b85dc-107">Proteger recursos na automatização do Azure incluem as credenciais, certificados, ligações e as variáveis encriptadas.</span><span class="sxs-lookup"><span data-stu-id="b85dc-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="b85dc-108">Estes elementos são encriptados e armazenados em Olá da automatização do Azure com uma chave exclusiva que é gerada para cada conta de automatização.</span><span class="sxs-lookup"><span data-stu-id="b85dc-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="b85dc-109">Esta chave é encriptada por um certificado principal e armazenada na automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="b85dc-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="b85dc-110">Antes de o armazenamento de um recurso seguro, chave de Olá da conta de automatização de Olá é desencriptada utilizando o certificado principal Olá e, em seguida, utilizado asset de Olá tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="b85dc-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="b85dc-111">Cmdlets do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b85dc-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="b85dc-112">cmdlets de Olá no Olá a tabela seguinte são utilizado toocreate e gerir recursos de certificado de automatização com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b85dc-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="b85dc-113">Estes são enviados como parte da Olá [módulo Azure PowerShell](../powershell-install-configure.md) que está disponível para utilização nos runbooks de automatização e configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="b85dc-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="b85dc-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="b85dc-114">Cmdlets</span></span>|<span data-ttu-id="b85dc-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="b85dc-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="b85dc-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b85dc-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="b85dc-117">Obtém informações sobre toouse um certificado de um runbook ou a configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="b85dc-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="b85dc-118">Apenas pode obter o certificado de Olá propriamente dito da atividade de Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="b85dc-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="b85dc-119">Novo AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b85dc-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="b85dc-120">Cria um novo certificado para a automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="b85dc-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="b85dc-121">Remover AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b85dc-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="b85dc-122">Remove um certificado da automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="b85dc-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="b85dc-123">Cria um novo certificado para a automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="b85dc-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="b85dc-124">Conjunto AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="b85dc-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="b85dc-125">Define as propriedades de Olá para um certificado existente, incluindo carregar o ficheiro de certificado Olá e a palavra-passe Olá de definição para um ficheiro. pfx.</span><span class="sxs-lookup"><span data-stu-id="b85dc-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="b85dc-126">AzureCertificate adicionar</span><span class="sxs-lookup"><span data-stu-id="b85dc-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="b85dc-127">Carrega um serviço de certificado para Olá especificado serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="b85dc-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="b85dc-128">Criar um novo certificado</span><span class="sxs-lookup"><span data-stu-id="b85dc-128">Creating a new certificate</span></span>

<span data-ttu-id="b85dc-129">Quando cria um novo certificado, carregue uma tooAzure de ficheiro. cer ou. pfx automatização.</span><span class="sxs-lookup"><span data-stu-id="b85dc-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="b85dc-130">Se marcar o certificado de Olá como exportável, pode transferi-la fora do arquivo de certificados do Olá da automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="b85dc-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="b85dc-131">Se não é exportável, em seguida, pode apenas ser utilizado para a assinatura no runbook Olá ou a configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="b85dc-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="b85dc-132">toocreate um novo certificado com Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b85dc-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="b85dc-133">Da sua conta de automatização, clique em Olá **ativos** mosaico tooopen Olá **ativos** painel.</span><span class="sxs-lookup"><span data-stu-id="b85dc-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="b85dc-134">Clique em Olá **certificados** mosaico tooopen Olá **certificados** painel.</span><span class="sxs-lookup"><span data-stu-id="b85dc-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="b85dc-135">Clique em **adicionar um certificado** , Olá parte superior do painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="b85dc-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="b85dc-136">Escreva um nome para o certificado de Olá Olá **nome** caixa.</span><span class="sxs-lookup"><span data-stu-id="b85dc-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="b85dc-137">Clique em **selecione um ficheiro** em **carregar um ficheiro de certificado** toobrowse para um ficheiro. cer ou. pfx.</span><span class="sxs-lookup"><span data-stu-id="b85dc-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="b85dc-138">Se selecionar um ficheiro. pfx, especifique uma palavra-passe e se deve ter permissão toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="b85dc-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="b85dc-139">Clique em **criar** toosave Olá novo certificado elemento.</span><span class="sxs-lookup"><span data-stu-id="b85dc-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="b85dc-140">toocreate um novo certificado com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b85dc-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="b85dc-141">Olá exemplo seguinte demonstra como toocreate uma automatização novo certificado e marcá-la exportável.</span><span class="sxs-lookup"><span data-stu-id="b85dc-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="b85dc-142">Esta ação importa um ficheiro. pfx existente.</span><span class="sxs-lookup"><span data-stu-id="b85dc-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="b85dc-143">Utilizar um certificado</span><span class="sxs-lookup"><span data-stu-id="b85dc-143">Using a certificate</span></span>

<span data-ttu-id="b85dc-144">Tem de utilizar Olá **Get-AutomationCertificate** atividade toouse um certificado.</span><span class="sxs-lookup"><span data-stu-id="b85dc-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="b85dc-145">Não é possível utilizar Olá [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet, uma vez que devolve informações sobre o recurso de certificado Olá, mas não o certificado de Olá propriamente dito.</span><span class="sxs-lookup"><span data-stu-id="b85dc-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="b85dc-146">Exemplo de textual runbook</span><span class="sxs-lookup"><span data-stu-id="b85dc-146">Textual runbook sample</span></span>

<span data-ttu-id="b85dc-147">Olá, código de exemplo a seguir mostra como serviço num runbook em nuvem tooadd tooa um certificado.</span><span class="sxs-lookup"><span data-stu-id="b85dc-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="b85dc-148">Neste exemplo, palavra-passe de Olá é obtido a partir de uma variável de automatização encriptados.</span><span class="sxs-lookup"><span data-stu-id="b85dc-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="b85dc-149">Exemplo de um runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="b85dc-149">Graphical runbook sample</span></span>

<span data-ttu-id="b85dc-150">Adicionar um **Get-AutomationCertificate** tooa runbook gráfico clicando no certificado de Olá no painel de biblioteca de Olá do editor gráfico Olá e selecionando **adicionar toocanvas**.</span><span class="sxs-lookup"><span data-stu-id="b85dc-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Adicionar tela toohello de certificado](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="b85dc-152">Olá imagem seguinte mostra um exemplo de utilização de um certificado de um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="b85dc-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="b85dc-153">Este é Olá mesmo exemplo mostrado acima para adicionar um serviço de nuvem de tooa de certificado a partir de um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="b85dc-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="b85dc-154">Criação de gráficos de exemplo</span><span class="sxs-lookup"><span data-stu-id="b85dc-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="b85dc-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b85dc-155">Next steps</span></span>

- <span data-ttu-id="b85dc-156">toolearn mais informações sobre como trabalhar com fluxo lógico de ligações toocontrol Olá de atividades do runbook é concebido tooperform, consulte [nas hiperligações na criação de gráficos](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="b85dc-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
