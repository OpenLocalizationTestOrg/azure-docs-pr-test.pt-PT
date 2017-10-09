---
title: "aaaDesired configuração de estado para descrição geral do Azure | Microsoft Docs"
description: "Descrição geral para a utilização de processador de extensão do Microsoft Azure Olá para configuração de estado pretendido do PowerShell. Incluindo a pré-requisitos, arquitetura, os cmdlets..."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="d75ff-104">Processador de extensão de configuração de estado pretendido do Azure introdução toohello</span><span class="sxs-lookup"><span data-stu-id="d75ff-104">Introduction toohello Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d75ff-105">Olá agente da VM do Azure e as extensões associadas fazem parte do Olá dos serviços de infraestrutura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-105">hello Azure VM Agent and associated Extensions are part of hello Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="d75ff-106">Extensões de VM são os componentes de software que expandem a funcionalidade de VM Olá e simplificam a várias operações de gestão de VM.</span><span class="sxs-lookup"><span data-stu-id="d75ff-106">VM Extensions are software components that extend hello VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="d75ff-107">Por exemplo, Olá extensão VMAccess pode ser utilizado tooreset palavra-passe de um administrador ou Olá Script personalizado extensão pode ser utilizado tooexecute um script no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d75ff-107">For example, hello VMAccess extension can be used tooreset an administrator's password, or hello Custom Script extension can be used tooexecute a script on hello VM.</span></span>

<span data-ttu-id="d75ff-108">Este artigo apresenta Olá extensão pretendido Estado Configuration (DSC) do PowerShell para as VMs do Azure como parte da Olá SDK do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d75ff-108">This article introduces hello PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="d75ff-109">Pode utilizar os novos cmdlets tooupload e aplicar uma configuração de DSC do PowerShell numa VM do Azure ativada com Olá extensão de DSC do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d75ff-109">You can use new cmdlets tooupload and apply a PowerShell DSC configuration on an Azure VM enabled with hello PowerShell DSC extension.</span></span> <span data-ttu-id="d75ff-110">Olá chamadas de extensão de DSC do PowerShell para Olá do PowerShell DSC tooenact receberam a configuração de DSC na Olá VM.</span><span class="sxs-lookup"><span data-stu-id="d75ff-110">hello PowerShell DSC extension calls into PowerShell DSC tooenact hello received DSC configuration on hello VM.</span></span> <span data-ttu-id="d75ff-111">Esta funcionalidade está também disponível através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-111">This functionality is also available through hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d75ff-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d75ff-112">Prerequisites</span></span>
<span data-ttu-id="d75ff-113">**Máquina local** toointeract com Olá extensão da VM do Azure, tem de toouse ou Olá portal do Azure ou Olá, Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="d75ff-113">**Local machine** toointeract with hello Azure VM extension, you need toouse either hello Azure portal or hello Azure PowerShell SDK.</span></span> 

<span data-ttu-id="d75ff-114">**O agente convidado** Olá VM do Azure que está configurado por configuração Olá DSC tem toobe um sistema operativo que suporta o Windows Management Framework (WMF) 4.0 ou 5.0.</span><span class="sxs-lookup"><span data-stu-id="d75ff-114">**Guest Agent** hello Azure VM that is configured by hello DSC configuration needs toobe an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="d75ff-115">obter uma lista completa Olá de versões de SO suportadas pode ser encontrada em Olá [histórico de versões de extensão de DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="d75ff-115">hello full list of supported OS versions can be found at hello [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="d75ff-116">Conceitos e termos de licenciamento</span><span class="sxs-lookup"><span data-stu-id="d75ff-116">Terms and concepts</span></span>
<span data-ttu-id="d75ff-117">Este guia presumes familiaridade com Olá seguintes conceitos:</span><span class="sxs-lookup"><span data-stu-id="d75ff-117">This guide presumes familiarity with hello following concepts:</span></span>

<span data-ttu-id="d75ff-118">Configuração - um documento de configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="d75ff-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="d75ff-119">Nó - um destino para uma configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="d75ff-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="d75ff-120">Neste documento, "nó" sempre refere-se tooan VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-120">In this document, "node" always refers tooan Azure VM.</span></span>

<span data-ttu-id="d75ff-121">Dados de configuração - um. psd1 ficheiros que contêm dados ambientais para uma configuração</span><span class="sxs-lookup"><span data-stu-id="d75ff-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="d75ff-122">Descrição geral da arquitetura</span><span class="sxs-lookup"><span data-stu-id="d75ff-122">Architectural overview</span></span>
<span data-ttu-id="d75ff-123">Olá extensão de DSC do Azure utiliza Olá agente da VM do Azure framework toodeliver, enact e elaborar relatórios sobre configurações de DSC em execução em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-123">hello Azure DSC extension uses hello Azure VM Agent framework toodeliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="d75ff-124">Olá extensão de DSC espera um ficheiro. zip que contém, pelo menos, um documento de configuração e um conjunto de parâmetros fornecidos através de Olá SDK do Azure PowerShell ou de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-124">hello DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through hello Azure PowerShell SDK or through hello Azure portal.</span></span>

<span data-ttu-id="d75ff-125">Quando a extensão de Olá é chamado para Olá pela primeira vez, é executado um processo de instalação.</span><span class="sxs-lookup"><span data-stu-id="d75ff-125">When hello extension is called for hello first time, it runs an installation process.</span></span> <span data-ttu-id="d75ff-126">Este processo é instalado uma versão de Olá Windows Management Framework (WMF) utilizando Olá lógica os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d75ff-126">This process installs a version of hello Windows Management Framework (WMF) using hello following logic:</span></span>

1. <span data-ttu-id="d75ff-127">Se Olá SO de VM do Azure for Windows Server 2016, não é necessária nenhuma ação.</span><span class="sxs-lookup"><span data-stu-id="d75ff-127">If hello Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="d75ff-128">Windows Server 2016 já tem uma versão mais recente Olá do PowerShell instalada.</span><span class="sxs-lookup"><span data-stu-id="d75ff-128">Windows Server 2016 already has hello latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="d75ff-129">Se hello `wmfVersion` é especificada a propriedade e que versão do Olá WMF está instalada, a menos que é incompatível com a SO da VM Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-129">If hello `wmfVersion` property is specified, that version of hello WMF is installed unless it is incompatible with hello VM's OS.</span></span>
3. <span data-ttu-id="d75ff-130">Se não `wmfVersion` é especificada a propriedade, Olá mais recente versão aplicável do Olá WMF está instalado.</span><span class="sxs-lookup"><span data-stu-id="d75ff-130">If no `wmfVersion` property is specified, hello latest applicable version of hello WMF is installed.</span></span>

<span data-ttu-id="d75ff-131">Instalação de Olá WMF requer um reinício.</span><span class="sxs-lookup"><span data-stu-id="d75ff-131">Installation of hello WMF requires a reboot.</span></span> <span data-ttu-id="d75ff-132">Após o reinício, extensão Olá transfere o ficheiro. zip de Olá especificado no Olá `modulesUrl` propriedade.</span><span class="sxs-lookup"><span data-stu-id="d75ff-132">After reboot, hello extension downloads hello .zip file specified in hello `modulesUrl` property.</span></span> <span data-ttu-id="d75ff-133">Se esta localização no armazenamento de Blobs do Azure, pode ser especificado um token SAS Olá `sasToken` propriedade tooaccess Olá ficheiro.</span><span class="sxs-lookup"><span data-stu-id="d75ff-133">If this location is in Azure blob storage, a SAS token can be specified in hello `sasToken` property tooaccess hello file.</span></span> <span data-ttu-id="d75ff-134">Depois de Olá zip é transferido e descompactado, Olá função de configuração definida no `configurationFunction` está a executar o ficheiro MOF a toogenerate Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-134">After hello .zip is downloaded and unpacked, hello configuration function defined in `configurationFunction` is run toogenerate hello MOF file.</span></span> <span data-ttu-id="d75ff-135">extensão de Olá, em seguida, executa `Start-DscConfiguration -Force` no ficheiro MOF Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="d75ff-135">hello extension then runs `Start-DscConfiguration -Force` on hello generated MOF file.</span></span> <span data-ttu-id="d75ff-136">a extensão de Olá capturas de saída e escreve-a novamente saída toohello canal de estado do Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-136">hello extension captures output and writes it back out toohello Azure Status Channel.</span></span> <span data-ttu-id="d75ff-137">A partir deste ponto no Olá o MMC de DSC processa a monitorização e a correção como habitualmente.</span><span class="sxs-lookup"><span data-stu-id="d75ff-137">From this point on, hello DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="d75ff-138">Cmdlets do PowerShell</span><span class="sxs-lookup"><span data-stu-id="d75ff-138">PowerShell cmdlets</span></span>
<span data-ttu-id="d75ff-139">Cmdlets do PowerShell podem ser utilizados com o Azure Resource Manager ou Olá toopackage de modelo de implementação clássica, publicar e monitorizar as implementações de extensão de DSC.</span><span class="sxs-lookup"><span data-stu-id="d75ff-139">PowerShell cmdlets can be used with Azure Resource Manager or hello classic deployment model toopackage, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="d75ff-140">Olá seguintes cmdlets listados são módulos de implementação clássica Olá, mas pode ser substituída "Azure" com o modelo do "AzureRm" toouse Olá Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d75ff-140">hello following cmdlets listed are hello classic deployment modules, but "Azure" can be replaced with "AzureRm" toouse hello Azure Resource Manager model.</span></span> <span data-ttu-id="d75ff-141">Por exemplo, `Publish-AzureVMDscConfiguration` utiliza Olá modelo de implementação clássica, onde `Publish-AzureRmVMDscConfiguration` utiliza o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d75ff-141">For example,  `Publish-AzureVMDscConfiguration` uses hello classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="d75ff-142">`Publish-AzureVMDscConfiguration`aceita um ficheiro de configuração, analisa-lo para recursos de DSC dependentes e cria um ficheiro. zip que contém a configuração de Olá e configuração do DSC recursos necessários tooenact Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing hello configuration and DSC resources needed tooenact hello configuration.</span></span> <span data-ttu-id="d75ff-143">Também pode criar pacote Olá localmente utilizando Olá `-ConfigurationArchivePath` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d75ff-143">It can also create hello package locally using hello `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="d75ff-144">Caso contrário, publica o armazenamento de BLOBs de tooAzure de ficheiro. zip Olá e protege-lo com um token SAS.</span><span class="sxs-lookup"><span data-stu-id="d75ff-144">Otherwise, it publishes hello .zip file tooAzure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="d75ff-145">ficheiro. zip de Olá criado por este cmdlet tem script de configuração. ps1 Olá na raiz de Olá da pasta de arquivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-145">hello .zip file created by this cmdlet has hello .ps1 configuration script at hello root of hello archive folder.</span></span> <span data-ttu-id="d75ff-146">Pasta do módulo Olá colocada na pasta de arquivo de Olá os recursos ter.</span><span class="sxs-lookup"><span data-stu-id="d75ff-146">Resources have hello module folder placed in hello archive folder.</span></span> 

<span data-ttu-id="d75ff-147">`Set-AzureVMDscExtension`injects Olá as definições de Olá extensão de DSC do PowerShell para um objeto de configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="d75ff-147">`Set-AzureVMDscExtension` injects hello settings needed by hello PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="d75ff-148">No modelo de implementação clássica Olá, alterações VM Olá tem de ser aplicado tooan VM do Azure com `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="d75ff-148">In hello classic deployment model, hello VM changes must be applied tooan Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="d75ff-149">`Get-AzureVMDscExtension`obtém o estado da extensão DSC Olá de uma VM específica.</span><span class="sxs-lookup"><span data-stu-id="d75ff-149">`Get-AzureVMDscExtension` retrieves hello DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="d75ff-150">`Get-AzureVMDscExtensionStatus`obtém o estado de Olá da configuração de DSC Olá enacted pelo processador de extensão de DSC Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-150">`Get-AzureVMDscExtensionStatus` retrieves hello status of hello DSC configuration enacted by hello DSC extension handler.</span></span> <span data-ttu-id="d75ff-151">Esta ação pode ser efetuada num única VM, ou grupo de VMs.</span><span class="sxs-lookup"><span data-stu-id="d75ff-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="d75ff-152">`Remove-AzureVMDscExtension`Remove o processador de extensão de Olá de uma máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="d75ff-152">`Remove-AzureVMDscExtension` removes hello extension handler from a given virtual machine.</span></span> <span data-ttu-id="d75ff-153">Este cmdlet **não** remover a configuração de Olá, desinstalar Olá WMF ou alterar as definições de Olá aplicado na máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-153">This cmdlet does **not** remove hello configuration, uninstall hello WMF, or change hello applied settings on hello virtual machine.</span></span> <span data-ttu-id="d75ff-154">Remove apenas o processador de extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-154">It only removes hello extension handler.</span></span> 

<span data-ttu-id="d75ff-155">**Principais diferenças nos cmdlets ASM e o Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="d75ff-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="d75ff-156">Cmdlets do Gestor de recursos do Azure são síncronos.</span><span class="sxs-lookup"><span data-stu-id="d75ff-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="d75ff-157">Cmdlets ASM são assíncronos.</span><span class="sxs-lookup"><span data-stu-id="d75ff-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="d75ff-158">ResourceGroupName, VMName, ArchiveStorageAccountName, versão e a localização estão todos os parâmetros necessários no Gestor de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="d75ff-159">ArchiveResourceGroupName é um novo parâmetro opcional para o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d75ff-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="d75ff-160">Pode especificar este parâmetro, quando a conta de armazenamento pertence tooa noutro grupo de recursos que Olá um onde a máquina virtual de Olá é criada.</span><span class="sxs-lookup"><span data-stu-id="d75ff-160">You can specify this parameter when your storage account belongs tooa different resource group than hello one where hello virtual machine is created.</span></span>
* <span data-ttu-id="d75ff-161">ConfigurationArchive denomina ArchiveBlobName no Gestor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d75ff-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="d75ff-162">ContainerName denomina ArchiveContainerName no Gestor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d75ff-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="d75ff-163">StorageEndpointSuffix denomina ArchiveStorageEndpointSuffix no Gestor de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d75ff-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="d75ff-164">foi adicionada comutador de AutoUpdate Olá tooAzure tooenable do Gestor de recursos automático de atualização de Olá processador toohello mais recente versão da extensão como e quando estiver disponível.</span><span class="sxs-lookup"><span data-stu-id="d75ff-164">hello AutoUpdate switch has been added tooAzure Resource Manager tooenable automatic updating of hello extension handler toohello latest version as and when it is available.</span></span> <span data-ttu-id="d75ff-165">Tenha em atenção de que este parâmetro tem toocause reinícios de potenciais Olá no Olá VM quando uma nova versão do Olá que WMF é libertado.</span><span class="sxs-lookup"><span data-stu-id="d75ff-165">Note this parameter has hello potential toocause reboots on hello VM when a new version of hello WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="d75ff-166">Funcionalidade de portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d75ff-166">Azure portal functionality</span></span>
<span data-ttu-id="d75ff-167">Procure tooa VM.</span><span class="sxs-lookup"><span data-stu-id="d75ff-167">Browse tooa VM.</span></span> <span data-ttu-id="d75ff-168">Em Definições -> geral clique em "As extensões."</span><span class="sxs-lookup"><span data-stu-id="d75ff-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="d75ff-169">É criado um novo painel.</span><span class="sxs-lookup"><span data-stu-id="d75ff-169">A new pane is created.</span></span> <span data-ttu-id="d75ff-170">Clique em "Adicionar" e selecione o PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="d75ff-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="d75ff-171">portal de Olá tem de entrada.</span><span class="sxs-lookup"><span data-stu-id="d75ff-171">hello portal needs input.</span></span>
<span data-ttu-id="d75ff-172">**Módulos de configuração ou Script**: Este campo é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d75ff-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="d75ff-173">Necessita de um ficheiro. ps1, que contém um script de configuração ou um ficheiro. zip com um script de configuração. ps1 na raiz de Olá e todos os recursos dependentes, nas pastas de módulo no Olá zip.</span><span class="sxs-lookup"><span data-stu-id="d75ff-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at hello root, and all dependent resources in module folders within hello .zip.</span></span> <span data-ttu-id="d75ff-174">Podem ser criada com Olá `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet incluído no Olá SDK do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d75ff-174">It can be created with hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in hello Azure PowerShell SDK.</span></span> <span data-ttu-id="d75ff-175">ficheiro. zip de Olá é carregado para o armazenamento de BLOBs de utilizador protegido por um token SAS.</span><span class="sxs-lookup"><span data-stu-id="d75ff-175">hello .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="d75ff-176">**Ficheiro de configuração de dados PSD1**: Este campo é opcional.</span><span class="sxs-lookup"><span data-stu-id="d75ff-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="d75ff-177">Se a configuração necessita de um ficheiro de dados de configuração. psd1, utilize este campo tooselect-lo e carregue-o armazenamento de BLOBs de utilizador tooyour, onde é protegida por um token SAS.</span><span class="sxs-lookup"><span data-stu-id="d75ff-177">If your configuration requires a configuration data file in .psd1, use this field tooselect it and upload it tooyour user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="d75ff-178">**Nome qualificado do módulo de configuração**:. ps1 ficheiros podem ter várias funções de configuração.</span><span class="sxs-lookup"><span data-stu-id="d75ff-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="d75ff-179">Introduza o nome de Olá do script. ps1 de configuração de Olá seguido por um '\' e Olá nome da função de configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="d75ff-179">Enter hello name of hello configuration .ps1 script followed by a  '\' and hello name of hello configuration function.</span></span> <span data-ttu-id="d75ff-180">Por exemplo, se o script. ps1 tem Olá. o nome "configuration.ps1", não sendo configuração Olá "IisInstall", deve introduzir:`configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="d75ff-180">For example, if your .ps1 script has hello name "configuration.ps1", and hello configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="d75ff-181">**Configuração argumentos**: se a função de configuração de Olá aceita argumentos, introduzi-las a sessão aqui no formato de Olá `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="d75ff-181">**Configuration Arguments**: If hello configuration function takes arguments, enter them in here in hello format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="d75ff-182">Tenha em atenção de que este formato é um formato diferente que como argumentos de configuração são aceites através de cmdlets do PowerShell ou modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d75ff-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="d75ff-183">Introdução</span><span class="sxs-lookup"><span data-stu-id="d75ff-183">Getting started</span></span>
<span data-ttu-id="d75ff-184">Olá extensão de DSC do Azure aceita documentos de configuração de DSC e enacts-los em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d75ff-184">hello Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="d75ff-185">Segue-se um exemplo simple de uma configuração.</span><span class="sxs-lookup"><span data-stu-id="d75ff-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="d75ff-186">Guarde-o localmente como "IisInstall.ps1":</span><span class="sxs-lookup"><span data-stu-id="d75ff-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="d75ff-187">Olá seguindo os passos local Olá IisInstall.ps1 script do Olá especificado VM, executar a configuração de Olá e devolver relatórios sobre o estado.</span><span class="sxs-lookup"><span data-stu-id="d75ff-187">hello following steps place hello IisInstall.ps1 script on hello specified VM, execute hello configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="d75ff-188">Modelo clássico</span><span class="sxs-lookup"><span data-stu-id="d75ff-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="d75ff-189">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d75ff-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="d75ff-190">Registo</span><span class="sxs-lookup"><span data-stu-id="d75ff-190">Logging</span></span>
<span data-ttu-id="d75ff-191">Os registos são colocados em:</span><span class="sxs-lookup"><span data-stu-id="d75ff-191">Logs are placed in:</span></span>

<span data-ttu-id="d75ff-192">C:\WindowsAzure\Logs\Plugins\Microsoft.PowerShell.DSC\[número de versão]</span><span class="sxs-lookup"><span data-stu-id="d75ff-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="d75ff-193">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d75ff-193">Next steps</span></span>
<span data-ttu-id="d75ff-194">Para obter mais informações sobre o PowerShell DSC, [visitar o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="d75ff-194">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="d75ff-195">Examine Olá [modelo Azure Resource Manager para a extensão de Olá DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d75ff-195">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="d75ff-196">toofind funcionalidades adicionais, pode gerir com o PowerShell DSC, [procurar galeria do PowerShell Olá](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) mais recursos de DSC.</span><span class="sxs-lookup"><span data-stu-id="d75ff-196">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="d75ff-197">Para obter detalhes sobre a transmitir parâmetros confidenciais para as configurações, consulte [gerir credenciais de forma segura com o processador de extensão de Olá DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d75ff-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with hello DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

