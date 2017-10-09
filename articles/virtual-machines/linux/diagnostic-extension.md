---
title: "Computação aaaAzure - extensão de diagnóstico do Linux | Microsoft Docs"
description: "Como tooconfigure Olá métricas de toocollect de extensão de diagnóstico Linux do Azure (LAD) e eventos de registo de VMs do Linux em execução no Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="025e2-103">Utilize registos e as métricas de toomonitor de extensão de diagnóstico do Linux</span><span class="sxs-lookup"><span data-stu-id="025e2-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="025e2-104">Este documento descreve a versão 3.0 e mais recente de Olá extensão de diagnóstico do Linux.</span><span class="sxs-lookup"><span data-stu-id="025e2-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="025e2-105">Para obter informações sobre a versão mais antiga e 2.3, consulte [neste documento](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="025e2-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="025e2-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="025e2-106">Introduction</span></span>

<span data-ttu-id="025e2-107">Olá extensão de diagnóstico do Linux ajuda a um utilizador monitor Olá estado de funcionamento de uma VM com Linux em execução no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="025e2-108">Tem Olá seguintes capacidades:</span><span class="sxs-lookup"><span data-stu-id="025e2-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="025e2-109">Recolhe métricas de desempenho do sistema de Olá VM e armazena-os numa tabela específica numa conta do storage designada.</span><span class="sxs-lookup"><span data-stu-id="025e2-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="025e2-110">Obtém o registo de eventos do syslog e armazena-os numa tabela específica no Olá designada de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="025e2-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="025e2-111">Permite que os utilizadores toocustomize Olá dados as métricas que são recolhidas e a ser carregadas.</span><span class="sxs-lookup"><span data-stu-id="025e2-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="025e2-112">Permite a instalações de syslog do utilizadores toocustomize Olá e níveis de gravidade dos eventos que são recolhidos e a ser carregados.</span><span class="sxs-lookup"><span data-stu-id="025e2-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="025e2-113">Permite que os utilizadores tooupload especificado ficheiros tooa armazenamento designado tabela de registo de.</span><span class="sxs-lookup"><span data-stu-id="025e2-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="025e2-114">Suporta o envio de métricas e registo de eventos tooarbitrary EventHub pontos finais e a formatados em JSON blobs no Olá designada de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="025e2-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="025e2-115">Esta extensão funciona com ambos os modelos de implementação do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="025e2-116">Instalação da extensão Olá em VM</span><span class="sxs-lookup"><span data-stu-id="025e2-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="025e2-117">Pode ativar esta extensão utilizando cmdlets do Azure PowerShell Olá, scripts da CLI do Azure ou modelos de implementação do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="025e2-118">Para obter mais informações, consulte [extensões funcionalidades](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="025e2-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="025e2-119">Olá portal do Azure não pode ser utilizado tooenable ou configurar LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="025e2-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="025e2-120">Em vez disso, instala e configura versão 2.3.</span><span class="sxs-lookup"><span data-stu-id="025e2-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="025e2-121">Gráficos de portais do Azure e alertas de trabalham com dados de ambas as versões da extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="025e2-122">Estas instruções de instalação e um [configuração de exemplo transferível](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurar LAD 3.0 para:</span><span class="sxs-lookup"><span data-stu-id="025e2-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="025e2-123">captura e arquivo Olá mesmas métricas que foram fornecidas pelo LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="025e2-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="025e2-124">captura de um conjunto de métricas de sistema de ficheiros, novo tooLAD 3.0; útil</span><span class="sxs-lookup"><span data-stu-id="025e2-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="025e2-125">captura de coleção de syslog Olá predefinida ativada por LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="025e2-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="025e2-126">Ative Olá experiência do portal do Azure para charting e alertas nas métricas VM.</span><span class="sxs-lookup"><span data-stu-id="025e2-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="025e2-127">configuração transferível Olá é apenas um exemplo; Modifique-toosuit as suas próprias necessidades.</span><span class="sxs-lookup"><span data-stu-id="025e2-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="025e2-128">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="025e2-128">Prerequisites</span></span>

* <span data-ttu-id="025e2-129">**Agente Linux do Azure versão 2.2.0 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="025e2-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="025e2-130">A maioria das imagens de galeria do Azure VM Linux incluem versão 2.2.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="025e2-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="025e2-131">Executar `/usr/sbin/waagent -version` versão de Olá tooconfirm instalado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="025e2-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="025e2-132">Se Olá VM estiver a executar uma versão mais antiga do agente do convidado Olá, siga [estas instruções](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate-lo.</span><span class="sxs-lookup"><span data-stu-id="025e2-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="025e2-133">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="025e2-133">**Azure CLI**.</span></span> <span data-ttu-id="025e2-134">[Configurar Olá Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) ambiente no seu computador.</span><span class="sxs-lookup"><span data-stu-id="025e2-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="025e2-135">Olá wget comando, se ainda não tiver: executar `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="025e2-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="025e2-136">Uma subscrição do Azure existente e um armazenamento existente contas dentro da mesma dados de Olá toostore.</span><span class="sxs-lookup"><span data-stu-id="025e2-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="025e2-137">Instalação de exemplo</span><span class="sxs-lookup"><span data-stu-id="025e2-137">Sample installation</span></span>

<span data-ttu-id="025e2-138">Preencha os parâmetros corretos Olá no Olá primeiro três linhas, em seguida, execute este script como raiz:</span><span class="sxs-lookup"><span data-stu-id="025e2-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="025e2-139">URL de Olá para configuração de exemplo de Olá e o respetivo conteúdo, é toochange do requerente.</span><span class="sxs-lookup"><span data-stu-id="025e2-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="025e2-140">Transfira uma cópia do ficheiro JSON Olá definições do portal e personalizá-lo para as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="025e2-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="025e2-141">Qualquer modelos ou automatização que constrói, deve utilizar a sua cópia, em vez de a transferir esse URL cada vez.</span><span class="sxs-lookup"><span data-stu-id="025e2-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="025e2-142">A atualizar as definições de extensão de Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-142">Updating hello extension settings</span></span>

<span data-ttu-id="025e2-143">Depois de alterou a sua protegido ou definições público, implementá-las toohello VM executando Olá mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="025e2-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="025e2-144">Se nada alterado nas definições de Olá, definições de Olá atualizado são enviadas toohello extensão.</span><span class="sxs-lookup"><span data-stu-id="025e2-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="025e2-145">LAD reloads configuração Olá e reinicia si próprio.</span><span class="sxs-lookup"><span data-stu-id="025e2-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="025e2-146">Migração a partir de versões anteriores da extensão de Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="025e2-147">Olá a versão mais recente da extensão de Olá **3.0**.</span><span class="sxs-lookup"><span data-stu-id="025e2-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="025e2-148">**Todas as versões antigas (2) foram preteridas e pode ser anuladas nesta ou após 31 de Julho de 2018**.</span><span class="sxs-lookup"><span data-stu-id="025e2-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="025e2-149">Esta extensão apresenta a configuração de toohello de alterações de quebra de extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="025e2-150">Um essa alteração foi efetuada a segurança de Olá tooimprove da extensão de Olá; como resultado, efeitos compatibilidade com 2 não foi possível manter.</span><span class="sxs-lookup"><span data-stu-id="025e2-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="025e2-151">Além disso, Olá publicador de extensão para esta extensão é diferente do publicador Olá para as versões do Olá 2. x.</span><span class="sxs-lookup"><span data-stu-id="025e2-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="025e2-152">toomigrate de 2. x toothis nova versão da extensão de Olá, tem de desinstalar extensão antigo do Olá (em nome do publicador antigo Olá), em seguida, instalar versão 3 Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="025e2-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="025e2-153">Recomendações:</span><span class="sxs-lookup"><span data-stu-id="025e2-153">Recommendations:</span></span>

* <span data-ttu-id="025e2-154">Instale a extensão de Olá com a atualização de versões de secundárias automática ativada.</span><span class="sxs-lookup"><span data-stu-id="025e2-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="025e2-155">No modelo de implementação clássica VMs, especifique '3.*' como versão de Olá se estiver a instalar extensão Olá através da CLI XPLAT do Azure ou do Powershell.</span><span class="sxs-lookup"><span data-stu-id="025e2-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="025e2-156">Na implementação do Azure Resource Manager modelo VMs, incluir ' "autoUpgradeMinorVersion": true' no modelo de implementação de VM Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="025e2-157">Utilize uma conta de armazenamento nova/diferente para LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="025e2-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="025e2-158">Existem várias incompatibilidades pequenas entre LAD 2.3 e LAD 3.0 que tornam uma conta troublesome de partilha:</span><span class="sxs-lookup"><span data-stu-id="025e2-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="025e2-159">LAD 3.0 armazena eventos syslog numa tabela com um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="025e2-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="025e2-160">counterSpecifier Olá cadeias para `builtin` métricas diferem no LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="025e2-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="025e2-161">Definições protegidas</span><span class="sxs-lookup"><span data-stu-id="025e2-161">Protected settings</span></span>

<span data-ttu-id="025e2-162">Este conjunto de informações de configuração contém informações confidenciais que devem ser protegidas a partir da vista pública, por exemplo, as credenciais do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="025e2-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="025e2-163">Estas definições são transmitido tooand armazenada pela extensão de Olá em formato encriptado.</span><span class="sxs-lookup"><span data-stu-id="025e2-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="025e2-164">Nome</span><span class="sxs-lookup"><span data-stu-id="025e2-164">Name</span></span> | <span data-ttu-id="025e2-165">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-165">Value</span></span>
---- | -----
<span data-ttu-id="025e2-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="025e2-166">storageAccountName</span></span> | <span data-ttu-id="025e2-167">nome de Olá Olá da conta de armazenamento na qual os dados são escritos pela extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="025e2-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="025e2-168">storageAccountEndPoint</span></span> | <span data-ttu-id="025e2-169">ponto final de Olá (opcional) identificar nuvem Olá no qual Olá conta de armazenamento existe.</span><span class="sxs-lookup"><span data-stu-id="025e2-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="025e2-170">Se esta definição estiver ausente, LAD predefinições toohello nuvem pública do Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="025e2-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="025e2-171">toouse uma conta de armazenamento em Datacenters do Azure, Azure Government ou Azure China, definir este valor em conformidade.</span><span class="sxs-lookup"><span data-stu-id="025e2-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="025e2-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="025e2-172">storageAccountSasToken</span></span> | <span data-ttu-id="025e2-173">Um [token SAS de conta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para serviços Blob e a tabela (`ss='bt'`), toocontainers aplicáveis e objetos (`srt='co'`), que concede adiciona, criar, listar, atualizar e permissões de escrita (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="025e2-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="025e2-174">Efetue *não* incluem Olá leading pergunta-interrogação (?).</span><span class="sxs-lookup"><span data-stu-id="025e2-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="025e2-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="025e2-175">mdsdHttpProxy</span></span> | <span data-ttu-id="025e2-176">(opcional) HTTP proxy informações necessárias tooenable Olá extensão tooconnect toohello especificar conta de armazenamento e de ponto final.</span><span class="sxs-lookup"><span data-stu-id="025e2-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="025e2-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="025e2-177">sinksConfig</span></span> | <span data-ttu-id="025e2-178">(opcional) Detalhes de destinos alternativos toowhich métricas e eventos podem ser fornecidos.</span><span class="sxs-lookup"><span data-stu-id="025e2-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="025e2-179">detalhes específicos do Olá de cada sink de dados suportados pela extensão de Olá são abordados nas secções de Olá que se seguem.</span><span class="sxs-lookup"><span data-stu-id="025e2-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="025e2-180">Pode criar facilmente Olá necessário token SAS através de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="025e2-181">Selecione toowhich de conta de armazenamento para fins gerais de Olá pretende Olá extensão toowrite</span><span class="sxs-lookup"><span data-stu-id="025e2-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="025e2-182">Selecione "Assinatura de acesso partilhado" de Olá definições parte menu à esquerda Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="025e2-183">Certifique-secções apropriadas Olá conforme descritos anteriormente</span><span class="sxs-lookup"><span data-stu-id="025e2-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="025e2-184">Clique no botão de "SAS gerar" Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-184">Click hello "Generate SAS" button.</span></span>

![Imagem](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="025e2-186">Olá cópia gerado SAS no campo de storageAccountSasToken Olá; Remova a marca de pergunta leading Olá ("?").</span><span class="sxs-lookup"><span data-stu-id="025e2-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="025e2-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="025e2-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="025e2-188">Esta secção opcional define adicionais destinos de extensão de Olá toowhich envia informações de Olá recolhe.</span><span class="sxs-lookup"><span data-stu-id="025e2-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="025e2-189">matriz de "sink" Olá contém um objeto para cada sink de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="025e2-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="025e2-190">Olá determina o atributo "tipo" Olá outros atributos no objeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="025e2-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-191">Element</span></span> | <span data-ttu-id="025e2-192">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-192">Value</span></span>
------- | -----
<span data-ttu-id="025e2-193">nome</span><span class="sxs-lookup"><span data-stu-id="025e2-193">name</span></span> | <span data-ttu-id="025e2-194">Uma cadeia utilizada toorefer toothis sink noutro local na configuração da extensão Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="025e2-195">tipo</span><span class="sxs-lookup"><span data-stu-id="025e2-195">type</span></span> | <span data-ttu-id="025e2-196">tipo de Olá do sink que está a ser definido.</span><span class="sxs-lookup"><span data-stu-id="025e2-196">hello type of sink being defined.</span></span> <span data-ttu-id="025e2-197">Determina a Olá outros valores (se aplicável) em instâncias deste tipo.</span><span class="sxs-lookup"><span data-stu-id="025e2-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="025e2-198">Versão 3.0 do Olá extensão de diagnóstico do Linux suporta dois tipos de receptores: EventHub e JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="025e2-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="025e2-199">receptor de EventHub Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-199">hello EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="025e2-200">entrada de "sasURL" Olá contém Olá URL completo, incluindo o token SAS, para Olá dados do Hub de eventos toowhich deve ser publicado.</span><span class="sxs-lookup"><span data-stu-id="025e2-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="025e2-201">LAD requer uma SAS nomenclatura uma política que ativa Olá enviar afirmações.</span><span class="sxs-lookup"><span data-stu-id="025e2-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="025e2-202">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="025e2-202">An example:</span></span>

* <span data-ttu-id="025e2-203">Criar um espaço de nomes de Event Hubs chamado`contosohub`</span><span class="sxs-lookup"><span data-stu-id="025e2-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="025e2-204">Criar um Hub de eventos no espaço de nomes de Olá chamado`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="025e2-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="025e2-205">Criar uma política de acesso partilhado no Olá com o nome de Hub de eventos `writer` que permite Olá afirmações de envio</span><span class="sxs-lookup"><span data-stu-id="025e2-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="025e2-206">Se tiver criado uma SAS boa até à meia-noite UTC em 1 de Janeiro de 2018, o valor de sasURL Olá pode ser:</span><span class="sxs-lookup"><span data-stu-id="025e2-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="025e2-207">Para obter mais informações sobre a criação de tokens SAS para os Event Hubs, consulte [esta página web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="025e2-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="025e2-208">receptor de JsonBlob Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="025e2-209">Dados direcionado tooa JsonBlob sink é armazenado em blobs no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="025e2-210">Cada instância de LAD cria um blob a cada hora para cada nome de sink.</span><span class="sxs-lookup"><span data-stu-id="025e2-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="025e2-211">Cada blob contém sempre uma matriz JSON é sintaticamente válida do objeto.</span><span class="sxs-lookup"><span data-stu-id="025e2-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="025e2-212">Novas entradas atomically são adicionadas toohello matriz.</span><span class="sxs-lookup"><span data-stu-id="025e2-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="025e2-213">Os BLOBs são armazenados num contentor com o mesmo nome como sink Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="025e2-214">Olá regras de armazenamento do Azure para os nomes de contentor do blob aplicam toohello nomes de JsonBlob sinks: entre 3 e 63 carateres ASCII alfanuméricos minúsculos ou travessões.</span><span class="sxs-lookup"><span data-stu-id="025e2-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="025e2-215">Definições de público</span><span class="sxs-lookup"><span data-stu-id="025e2-215">Public settings</span></span>

<span data-ttu-id="025e2-216">Esta estrutura contém vários blocos de definições que controlam as informações de Olá recolhidas pela extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="025e2-217">Cada definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="025e2-217">Each setting is optional.</span></span> <span data-ttu-id="025e2-218">Se especificar `ladCfg`, também tem de especificar `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="025e2-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="025e2-219">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-219">Element</span></span> | <span data-ttu-id="025e2-220">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-220">Value</span></span>
------- | -----
<span data-ttu-id="025e2-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="025e2-221">StorageAccount</span></span> | <span data-ttu-id="025e2-222">nome de Olá Olá da conta de armazenamento na qual os dados são escritos pela extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="025e2-223">Tem de ser Olá mesmo nome como está especificado no Olá [protegidos definições](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="025e2-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="025e2-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="025e2-224">mdsdHttpProxy</span></span> | <span data-ttu-id="025e2-225">(opcional) Mesmo do Olá [protegidos definições](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="025e2-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="025e2-226">valor pública Olá é substituída pelo valor de privada Olá, se definir.</span><span class="sxs-lookup"><span data-stu-id="025e2-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="025e2-227">Colocar as definições de proxy que contêm um segredo, tais como uma palavra-passe no Olá [protegidos definições](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="025e2-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="025e2-228">elementos de restantes Olá são descritos em detalhe no Olá secções a seguir.</span><span class="sxs-lookup"><span data-stu-id="025e2-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="025e2-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="025e2-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="025e2-230">Esta recolha de Olá de controlos de estrutura opcional de métricas e registos para entrega toohello dados de serviço e tooother de métricas de Azure sinks.</span><span class="sxs-lookup"><span data-stu-id="025e2-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="025e2-231">Tem de especificar um `performanceCounters` ou `syslogEvents` ou ambos.</span><span class="sxs-lookup"><span data-stu-id="025e2-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="025e2-232">Tem de especificar Olá `metrics` estrutura.</span><span class="sxs-lookup"><span data-stu-id="025e2-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="025e2-233">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-233">Element</span></span> | <span data-ttu-id="025e2-234">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-234">Value</span></span>
------- | -----
<span data-ttu-id="025e2-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="025e2-235">eventVolume</span></span> | <span data-ttu-id="025e2-236">(opcional) Controlos Olá número de partições criadas numa tabela de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="025e2-237">Tem de ser um dos `"Large"`, `"Medium"`, ou `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="025e2-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="025e2-238">Se não for especificado, o valor predefinido de Olá é `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="025e2-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="025e2-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="025e2-239">sampleRateInSeconds</span></span> | <span data-ttu-id="025e2-240">intervalo predefinido de Olá (opcional) entre a coleção de métricas (unaggregated) não processadas.</span><span class="sxs-lookup"><span data-stu-id="025e2-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="025e2-241">frequência de amostragem Olá mais pequena suportada é 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="025e2-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="025e2-242">Se não for especificado, o valor predefinido de Olá é `15`.</span><span class="sxs-lookup"><span data-stu-id="025e2-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="025e2-243">metrics</span><span class="sxs-lookup"><span data-stu-id="025e2-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="025e2-244">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-244">Element</span></span> | <span data-ttu-id="025e2-245">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-245">Value</span></span>
------- | -----
<span data-ttu-id="025e2-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="025e2-246">resourceId</span></span> | <span data-ttu-id="025e2-247">ID de recurso do Azure Resource Manager Olá do Olá VM ou de dimensionamento da máquina virtual Olá definir Olá toowhich que VM pertence.</span><span class="sxs-lookup"><span data-stu-id="025e2-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="025e2-248">Esta definição tem de ser também especificado se qualquer sink JsonBlob é utilizado numa configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="025e2-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="025e2-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="025e2-250">frequência de Olá que métricas agregadas são toobe calculado e transferidos tooAzure métricas, expressado como um intervalo de tempo é 8601.</span><span class="sxs-lookup"><span data-stu-id="025e2-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="025e2-251">período de transferência mais pequeno Olá é 60 segundos, ou seja, PT1M.</span><span class="sxs-lookup"><span data-stu-id="025e2-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="025e2-252">Tem de especificar pelo menos um scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="025e2-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="025e2-253">Exemplos de Olá métricas especificadas na secção de performanceCounters Olá são recolhidas a cada 15 segundos ou a taxa de exemplo de Olá explicitamente definida para o contador de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="025e2-254">Se forem apresentados vários scheduledTransferPeriod frequências (tal como no exemplo de Olá), cada agregação é calculada independentemente.</span><span class="sxs-lookup"><span data-stu-id="025e2-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="025e2-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="025e2-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="025e2-256">Esta secção opcional controla coleção Olá de métricas.</span><span class="sxs-lookup"><span data-stu-id="025e2-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="025e2-257">Exemplos não processados são agregados para cada [scheduledTransferPeriod](#metrics) tooproduce estes valores:</span><span class="sxs-lookup"><span data-stu-id="025e2-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="025e2-258">média</span><span class="sxs-lookup"><span data-stu-id="025e2-258">mean</span></span>
* <span data-ttu-id="025e2-259">mínimo</span><span class="sxs-lookup"><span data-stu-id="025e2-259">minimum</span></span>
* <span data-ttu-id="025e2-260">Máximo</span><span class="sxs-lookup"><span data-stu-id="025e2-260">maximum</span></span>
* <span data-ttu-id="025e2-261">recolhido o último valor</span><span class="sxs-lookup"><span data-stu-id="025e2-261">last-collected value</span></span>
* <span data-ttu-id="025e2-262">Contagem de amostras em bruto utilizado agregado de Olá toocompute</span><span class="sxs-lookup"><span data-stu-id="025e2-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="025e2-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-263">Element</span></span> | <span data-ttu-id="025e2-264">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-264">Value</span></span>
------- | -----
<span data-ttu-id="025e2-265">sinks</span><span class="sxs-lookup"><span data-stu-id="025e2-265">sinks</span></span> | <span data-ttu-id="025e2-266">(opcional) Uma lista separada por vírgulas dos nomes do sinks toowhich que LAD envia resultados métricos agregados.</span><span class="sxs-lookup"><span data-stu-id="025e2-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="025e2-267">Todas as métricas agregadas são publicados tooeach listado sink.</span><span class="sxs-lookup"><span data-stu-id="025e2-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="025e2-268">Consulte [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="025e2-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="025e2-269">Exemplo: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="025e2-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="025e2-270">tipo</span><span class="sxs-lookup"><span data-stu-id="025e2-270">type</span></span> | <span data-ttu-id="025e2-271">Identifica o fornecedor de real Olá de métrica de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="025e2-272">Classe</span><span class="sxs-lookup"><span data-stu-id="025e2-272">class</span></span> | <span data-ttu-id="025e2-273">Em conjunto com ". o contador" identifica métrica específica do Olá no espaço de nomes do fornecedor de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="025e2-274">Contador</span><span class="sxs-lookup"><span data-stu-id="025e2-274">counter</span></span> | <span data-ttu-id="025e2-275">Em conjunto com "class", identifica métrica específica do Olá no espaço de nomes do fornecedor de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="025e2-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="025e2-276">counterSpecifier</span></span> | <span data-ttu-id="025e2-277">Identifica a métrica específica do Olá no espaço de nomes do Olá métricas do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="025e2-278">Condição</span><span class="sxs-lookup"><span data-stu-id="025e2-278">condition</span></span> | <span data-ttu-id="025e2-279">(opcional) Aplica-se de uma instância específica de métrica de Olá Olá objeto toowhich de seleciona ou seleciona Olá agregação em todas as instâncias desse objeto.</span><span class="sxs-lookup"><span data-stu-id="025e2-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="025e2-280">Para obter mais informações, consulte Olá [ `builtin` as definições de métrica](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="025e2-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="025e2-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="025e2-281">sampleRate</span></span> | <span data-ttu-id="025e2-282">É o intervalo de 8601 que define a taxa de Olá que são recolhidos exemplos não processados para esta métrica.</span><span class="sxs-lookup"><span data-stu-id="025e2-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="025e2-283">Se não definir o intervalo de coleção de Olá é definido por valor Olá [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="025e2-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="025e2-284">frequência de amostragem suportados mais curta do Olá é 15 segundos (PT15S).</span><span class="sxs-lookup"><span data-stu-id="025e2-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="025e2-285">unidade</span><span class="sxs-lookup"><span data-stu-id="025e2-285">unit</span></span> | <span data-ttu-id="025e2-286">Deve ser um estas cadeias: "Count", "Bytes", "Segundos", "Percentagem", "CountPerSecond", "BytesPerSecond", "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="025e2-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="025e2-287">Define a unidade de Olá para a métrica de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="025e2-288">Os consumidores de dados de Olá recolhido esperam Olá recolhidos dados valores toomatch esta unidade.</span><span class="sxs-lookup"><span data-stu-id="025e2-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="025e2-289">LAD ignora este campo.</span><span class="sxs-lookup"><span data-stu-id="025e2-289">LAD ignores this field.</span></span>
<span data-ttu-id="025e2-290">displayName</span><span class="sxs-lookup"><span data-stu-id="025e2-290">displayName</span></span> | <span data-ttu-id="025e2-291">Olá etiqueta (no idioma de Olá especificado por região associada Olá definição) toobe ligado toothis dados no Azure métricas.</span><span class="sxs-lookup"><span data-stu-id="025e2-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="025e2-292">LAD ignora este campo.</span><span class="sxs-lookup"><span data-stu-id="025e2-292">LAD ignores this field.</span></span>

<span data-ttu-id="025e2-293">counterSpecifier Olá é um identificador arbitrário.</span><span class="sxs-lookup"><span data-stu-id="025e2-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="025e2-294">Os consumidores de métricas, como Olá charting portal do Azure e os alertas funcionalidade, utilizam counterSpecifier como Olá "chave", que identifica uma métrica ou uma instância de uma métrica.</span><span class="sxs-lookup"><span data-stu-id="025e2-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="025e2-295">Para `builtin` métricas, recomendamos que utilize valores counterSpecifier que começam com `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="025e2-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="025e2-296">Se está a recolher uma instância específica de uma métrica, recomendamos que ligue o identificador de Olá do valor de counterSpecifier Olá instância toohello.</span><span class="sxs-lookup"><span data-stu-id="025e2-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="025e2-297">Alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="025e2-297">Some examples:</span></span>

* <span data-ttu-id="025e2-298">`/builtin/Processor/PercentIdleTime`-Tempo inativo, Considerando todos os núcleos</span><span class="sxs-lookup"><span data-stu-id="025e2-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="025e2-299">`/builtin/Disk/FreeSpace(/mnt)`-Espaço para o sistema de ficheiros do Olá /mnt</span><span class="sxs-lookup"><span data-stu-id="025e2-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="025e2-300">`/builtin/Disk/FreeSpace`-Espaço Considerando todos os sistemas de ficheiros instalados montados</span><span class="sxs-lookup"><span data-stu-id="025e2-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="025e2-301">Nem LAD nem Olá portal do Azure espera Olá counterSpecifier valor toomatch qualquer padrão.</span><span class="sxs-lookup"><span data-stu-id="025e2-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="025e2-302">Ser consistente na forma como pode construir valores de counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="025e2-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="025e2-303">Quando especificar `performanceCounters`, LAD escreve sempre tabela tooa de dados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="025e2-304">Pode ter Olá mesmo dados escritos tooJSON blobs e/ou os Event Hubs, mas não é possível desativar a tabela de tooa armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="025e2-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="025e2-305">Todas as instâncias de Olá extensão de diagnóstico configurada toouse Olá a mesma conta de armazenamento, nome e o ponto final de adicionam os seus toohello métricas e registos mesma tabela.</span><span class="sxs-lookup"><span data-stu-id="025e2-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="025e2-306">Se estiver a escrever VMs demasiados toohello pode limitar a mesma partição de tabela, Azure escreve toothat partição.</span><span class="sxs-lookup"><span data-stu-id="025e2-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="025e2-307">eventVolume Olá definição faz com que as entradas toobe distribuídos por 1 (breve), 10 (mediano) ou 100 partições de diferentes (grande).</span><span class="sxs-lookup"><span data-stu-id="025e2-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="025e2-308">Normalmente, "Médio" é suficiente tooensure tráfego não é limitado.</span><span class="sxs-lookup"><span data-stu-id="025e2-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="025e2-309">funcionalidade de métricas de Azure Olá de Olá portal do Azure utiliza dados Olá nesta gráficos de tooproduce de tabela ou tootrigger alertas.</span><span class="sxs-lookup"><span data-stu-id="025e2-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="025e2-310">nome da tabela Olá é concatenação Olá estas cadeias de:</span><span class="sxs-lookup"><span data-stu-id="025e2-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="025e2-311">Olá "scheduledTransferPeriod" para Olá agregado valores armazenados na tabela de Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="025e2-312">Uma data, no formato de Olá "AAAAMMDD", que altera a cada 10 dias</span><span class="sxs-lookup"><span data-stu-id="025e2-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="025e2-313">Os exemplos incluem `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="025e2-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="025e2-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="025e2-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="025e2-315">Esta secção opcional controla coleção Olá de eventos de registo de syslog.</span><span class="sxs-lookup"><span data-stu-id="025e2-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="025e2-316">Se for omitida secção Olá, eventos syslog não são capturados de todo.</span><span class="sxs-lookup"><span data-stu-id="025e2-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="025e2-317">a coleção de syslogEventConfiguration Olá tem uma entrada para cada função do syslog de interesse.</span><span class="sxs-lookup"><span data-stu-id="025e2-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="025e2-318">Se minSeverity "NONE" para uma determinada instalação ou se essa função não aparece no elemento de Olá de todo, não há eventos de instalação de que são capturados.</span><span class="sxs-lookup"><span data-stu-id="025e2-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="025e2-319">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-319">Element</span></span> | <span data-ttu-id="025e2-320">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-320">Value</span></span>
------- | -----
<span data-ttu-id="025e2-321">sinks</span><span class="sxs-lookup"><span data-stu-id="025e2-321">sinks</span></span> | <span data-ttu-id="025e2-322">Uma lista separada por vírgulas dos nomes do sinks registo individuais toowhich eventos são publicados.</span><span class="sxs-lookup"><span data-stu-id="025e2-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="025e2-323">Todos os eventos de registo correspondentes restrições de Olá no syslogEventConfiguration são publicados tooeach listado sink.</span><span class="sxs-lookup"><span data-stu-id="025e2-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="025e2-324">Exemplo: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="025e2-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="025e2-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="025e2-325">facilityName</span></span> | <span data-ttu-id="025e2-326">Um nome de função do syslog (tal como "registo\_utilizador" ou "registo\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="025e2-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="025e2-327">Consulte a secção "instalações" Olá Olá [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obter uma lista completa Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="025e2-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="025e2-328">minSeverity</span></span> | <span data-ttu-id="025e2-329">Um nível de gravidade syslog (tal como "registo\_ERR" ou "registo\_informações").</span><span class="sxs-lookup"><span data-stu-id="025e2-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="025e2-330">Consulte a secção "nível de" Olá Olá [página de man syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obter uma lista completa Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="025e2-331">extensão de Olá captura eventos enviados toohello instalações em especificados, ou acima Olá nível.</span><span class="sxs-lookup"><span data-stu-id="025e2-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="025e2-332">Quando especificar `syslogEvents`, LAD escreve sempre tabela tooa de dados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="025e2-333">Pode ter Olá mesmo dados escritos tooJSON blobs e/ou os Event Hubs, mas não é possível desativar a tabela de tooa armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="025e2-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="025e2-334">Olá comportamento para esta tabela de criação de partições é Olá igual à descrita para `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="025e2-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="025e2-335">nome da tabela Olá é concatenação Olá estas cadeias de:</span><span class="sxs-lookup"><span data-stu-id="025e2-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="025e2-336">Uma data, no formato de Olá "AAAAMMDD", que altera a cada 10 dias</span><span class="sxs-lookup"><span data-stu-id="025e2-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="025e2-337">Os exemplos incluem `LinuxSyslog20170410` e `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="025e2-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="025e2-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="025e2-338">perfCfg</span></span>

<span data-ttu-id="025e2-339">Esta secção opcional controla a execução de arbitrários [OMI](https://github.com/Microsoft/omi) consultas.</span><span class="sxs-lookup"><span data-stu-id="025e2-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="025e2-340">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-340">Element</span></span> | <span data-ttu-id="025e2-341">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-341">Value</span></span>
------- | -----
<span data-ttu-id="025e2-342">Espaço de nomes</span><span class="sxs-lookup"><span data-stu-id="025e2-342">namespace</span></span> | <span data-ttu-id="025e2-343">(opcional) Olá OMI espaço de nomes no qual Olá consulta deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="025e2-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="025e2-344">Se não for indicado, o valor predefinido de Olá é "raiz/scx", implementado por Olá [fornecedores de plataforma do System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="025e2-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="025e2-345">consulta</span><span class="sxs-lookup"><span data-stu-id="025e2-345">query</span></span> | <span data-ttu-id="025e2-346">Olá toobe consulta OMI foi executado.</span><span class="sxs-lookup"><span data-stu-id="025e2-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="025e2-347">Tabela</span><span class="sxs-lookup"><span data-stu-id="025e2-347">table</span></span> | <span data-ttu-id="025e2-348">tabela de armazenamento do Azure Olá (opcional), no Olá designada de conta de armazenamento (consulte [protegidos definições](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="025e2-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="025e2-349">frequência</span><span class="sxs-lookup"><span data-stu-id="025e2-349">frequency</span></span> | <span data-ttu-id="025e2-350">número de Olá (opcional) de segundos entre a execução da consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="025e2-351">Valor predefinido é de 300 (5 minutos) valor mínimo é de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="025e2-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="025e2-352">sinks</span><span class="sxs-lookup"><span data-stu-id="025e2-352">sinks</span></span> | <span data-ttu-id="025e2-353">(opcional) Uma lista separada por vírgulas dos nomes dos resultados métrica não processados exemplo toowhich sinks adicionais deve ser publicada.</span><span class="sxs-lookup"><span data-stu-id="025e2-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="025e2-354">Nenhuma agregação destes exemplos em bruto é calculada por extensão Olá ou por métricas do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="025e2-355">O "tabela" ou "sinks" ou ambos, tem de ser especificados.</span><span class="sxs-lookup"><span data-stu-id="025e2-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="025e2-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="025e2-356">fileLogs</span></span>

<span data-ttu-id="025e2-357">Capturar Olá de controlos de ficheiros de registo.</span><span class="sxs-lookup"><span data-stu-id="025e2-357">Controls hello capture of log files.</span></span> <span data-ttu-id="025e2-358">LAD captura novas linhas de texto que estes são escritos no ficheiro toohello e escreve-as linhas tootable e/ou qualquer sinks especificados (JsonBlob ou EventHub).</span><span class="sxs-lookup"><span data-stu-id="025e2-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="025e2-359">Elemento</span><span class="sxs-lookup"><span data-stu-id="025e2-359">Element</span></span> | <span data-ttu-id="025e2-360">Valor</span><span class="sxs-lookup"><span data-stu-id="025e2-360">Value</span></span>
------- | -----
<span data-ttu-id="025e2-361">ficheiro</span><span class="sxs-lookup"><span data-stu-id="025e2-361">file</span></span> | <span data-ttu-id="025e2-362">nome do caminho completo Olá da toobe de ficheiro de registo Olá observada e capturadas.</span><span class="sxs-lookup"><span data-stu-id="025e2-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="025e2-363">Olá pathname tem o nome num único ficheiro; -Não é um diretório de nomes ou conter carateres universais.</span><span class="sxs-lookup"><span data-stu-id="025e2-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="025e2-364">Tabela</span><span class="sxs-lookup"><span data-stu-id="025e2-364">table</span></span> | <span data-ttu-id="025e2-365">tabela de armazenamento do Azure Olá (opcional), no armazenamento de Olá designada de conta (conforme especificado na configuração de Olá protegido), em que novas linhas de Olá "seguimento" do ficheiro de Olá é escritos.</span><span class="sxs-lookup"><span data-stu-id="025e2-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="025e2-366">sinks</span><span class="sxs-lookup"><span data-stu-id="025e2-366">sinks</span></span> | <span data-ttu-id="025e2-367">(opcional) Enviar uma lista separada por vírgulas dos nomes das linhas de registo de toowhich sinks adicionais.</span><span class="sxs-lookup"><span data-stu-id="025e2-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="025e2-368">O "tabela" ou "sinks" ou ambos, tem de ser especificados.</span><span class="sxs-lookup"><span data-stu-id="025e2-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="025e2-369">Métricas suportadas pelo fornecedor de builtin Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="025e2-370">fornecedor de métrica de builtin Olá é uma origem de métricas mais interessante tooa conjunto amplo de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="025e2-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="025e2-371">Estas métricas enquadram-se a cinco classes abrangentes:</span><span class="sxs-lookup"><span data-stu-id="025e2-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="025e2-372">Processador</span><span class="sxs-lookup"><span data-stu-id="025e2-372">Processor</span></span>
* <span data-ttu-id="025e2-373">Memória</span><span class="sxs-lookup"><span data-stu-id="025e2-373">Memory</span></span>
* <span data-ttu-id="025e2-374">Rede</span><span class="sxs-lookup"><span data-stu-id="025e2-374">Network</span></span>
* <span data-ttu-id="025e2-375">Sistema de ficheiros</span><span class="sxs-lookup"><span data-stu-id="025e2-375">Filesystem</span></span>
* <span data-ttu-id="025e2-376">Disco</span><span class="sxs-lookup"><span data-stu-id="025e2-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="025e2-377">métricas de Builtin para Olá classe de processador</span><span class="sxs-lookup"><span data-stu-id="025e2-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="025e2-378">classe de processador de métricas de Olá fornece informações sobre a utilização do processador no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="025e2-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="025e2-379">Ao agregar percentagens, o resultado Olá é média Olá em todas as CPUs.</span><span class="sxs-lookup"><span data-stu-id="025e2-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="025e2-380">No core dois VM, se um núcleo 100% ocupado e Olá outro era 100% inativo, Olá comunicadas que percentidletime seria 50.</span><span class="sxs-lookup"><span data-stu-id="025e2-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="025e2-381">Se cada principal era 50% ocupado para Olá mesmo período, Olá comunicadas resultado também seria 50.</span><span class="sxs-lookup"><span data-stu-id="025e2-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="025e2-382">Numa quatro core VM, com um núcleo 100% ocupado e Olá outros inativo, Olá comunicadas que percentidletime seria 75.</span><span class="sxs-lookup"><span data-stu-id="025e2-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="025e2-383">Contador</span><span class="sxs-lookup"><span data-stu-id="025e2-383">counter</span></span> | <span data-ttu-id="025e2-384">Significado</span><span class="sxs-lookup"><span data-stu-id="025e2-384">Meaning</span></span>
------- | -------
<span data-ttu-id="025e2-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="025e2-385">PercentIdleTime</span></span> | <span data-ttu-id="025e2-386">Percentagem de tempo durante a janela de agregação de Olá que processadores foram ao executar o ciclo de inatividade de kernel Olá</span><span class="sxs-lookup"><span data-stu-id="025e2-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="025e2-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="025e2-387">PercentProcessorTime</span></span> | <span data-ttu-id="025e2-388">Percentagem de tempo de execução de um thread não inativo</span><span class="sxs-lookup"><span data-stu-id="025e2-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="025e2-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="025e2-389">PercentIOWaitTime</span></span> | <span data-ttu-id="025e2-390">Percentagem de tempo à espera de e/s operações toocomplete</span><span class="sxs-lookup"><span data-stu-id="025e2-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="025e2-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="025e2-391">PercentInterruptTime</span></span> | <span data-ttu-id="025e2-392">Percentagem de tempo de execução de hardware/software interrupções e DPCs (chamadas de procedimento diferidas)</span><span class="sxs-lookup"><span data-stu-id="025e2-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="025e2-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="025e2-393">PercentUserTime</span></span> | <span data-ttu-id="025e2-394">De tempo não inativo durante a janela de agregação de Olá, percentagem de Olá de tempo despendido num utilizador mais com prioridade normal</span><span class="sxs-lookup"><span data-stu-id="025e2-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="025e2-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="025e2-395">PercentNiceTime</span></span> | <span data-ttu-id="025e2-396">De tempo não inativo, Olá percentagem gasta em lowered prioridade (nice)</span><span class="sxs-lookup"><span data-stu-id="025e2-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="025e2-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="025e2-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="025e2-398">De tempo não inativo, Olá percentagem gasta no modo privilegiado (kernel)</span><span class="sxs-lookup"><span data-stu-id="025e2-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="025e2-399">Olá primeiro quatro contadores devem soma too100%.</span><span class="sxs-lookup"><span data-stu-id="025e2-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="025e2-400">Olá últimos três contadores também soma too100%; Estes subdividir Olá soma de PercentProcessorTime, PercentIOWaitTime e PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="025e2-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="025e2-401">Definir tooobtain uma métrica único agregada para todos os processadores, `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="025e2-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="025e2-402">tooobtain uma métrica para um processador específico, tal como o segundo processador lógico Olá de um quatro principais VM, defina `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="025e2-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="025e2-403">Os números de processador lógico estão no intervalo de Olá `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="025e2-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="025e2-404">métricas de Builtin para Olá classe de memória</span><span class="sxs-lookup"><span data-stu-id="025e2-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="025e2-405">classe de memória de métricas de Olá fornece informações sobre a utilização da memória, paginação e trocar.</span><span class="sxs-lookup"><span data-stu-id="025e2-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="025e2-406">Contador</span><span class="sxs-lookup"><span data-stu-id="025e2-406">counter</span></span> | <span data-ttu-id="025e2-407">Significado</span><span class="sxs-lookup"><span data-stu-id="025e2-407">Meaning</span></span>
------- | -------
<span data-ttu-id="025e2-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="025e2-408">AvailableMemory</span></span> | <span data-ttu-id="025e2-409">Memória física disponível no MiB</span><span class="sxs-lookup"><span data-stu-id="025e2-409">Available physical memory in MiB</span></span>
<span data-ttu-id="025e2-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="025e2-410">PercentAvailableMemory</span></span> | <span data-ttu-id="025e2-411">Memória física disponível como uma percentagem do total de memória</span><span class="sxs-lookup"><span data-stu-id="025e2-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="025e2-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="025e2-412">UsedMemory</span></span> | <span data-ttu-id="025e2-413">Na utilização memória física (MiB)</span><span class="sxs-lookup"><span data-stu-id="025e2-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="025e2-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="025e2-414">PercentUsedMemory</span></span> | <span data-ttu-id="025e2-415">Em utilização memória física como percentagem do total de memória</span><span class="sxs-lookup"><span data-stu-id="025e2-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="025e2-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="025e2-416">PagesPerSec</span></span> | <span data-ttu-id="025e2-417">Paginação total (leitura/escrita)</span><span class="sxs-lookup"><span data-stu-id="025e2-417">Total paging (read/write)</span></span>
<span data-ttu-id="025e2-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="025e2-418">PagesReadPerSec</span></span> | <span data-ttu-id="025e2-419">Páginas de ler a partir da cópia de arquivo (ficheiro de troca, os ficheiros de programa, ficheiro mapeado, etc.)</span><span class="sxs-lookup"><span data-stu-id="025e2-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="025e2-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="025e2-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="025e2-421">Páginas escritas toobacking armazenam (ficheiro de comutação, ficheiro mapeado, etc.)</span><span class="sxs-lookup"><span data-stu-id="025e2-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="025e2-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="025e2-422">AvailableSwap</span></span> | <span data-ttu-id="025e2-423">Espaço de comutação utilizado (MiB)</span><span class="sxs-lookup"><span data-stu-id="025e2-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="025e2-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="025e2-424">PercentAvailableSwap</span></span> | <span data-ttu-id="025e2-425">Espaço de comutação utilizado como uma percentagem de comutação total</span><span class="sxs-lookup"><span data-stu-id="025e2-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="025e2-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="025e2-426">UsedSwap</span></span> | <span data-ttu-id="025e2-427">Na utilização de espaço de comutação (MiB)</span><span class="sxs-lookup"><span data-stu-id="025e2-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="025e2-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="025e2-428">PercentUsedSwap</span></span> | <span data-ttu-id="025e2-429">Em utilização de espaço de comutação como uma percentagem de comutação total</span><span class="sxs-lookup"><span data-stu-id="025e2-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="025e2-430">Esta classe de métricas tem apenas uma única instância.</span><span class="sxs-lookup"><span data-stu-id="025e2-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="025e2-431">atributo de "condição" Olá sem outras definições útil e deve ser omitido.</span><span class="sxs-lookup"><span data-stu-id="025e2-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="025e2-432">métricas de Builtin para Olá classe de rede</span><span class="sxs-lookup"><span data-stu-id="025e2-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="025e2-433">classe de rede de métricas de Olá fornece informações sobre a atividade de rede em interfaces de rede individuais desde o arranque.</span><span class="sxs-lookup"><span data-stu-id="025e2-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="025e2-434">LAD não expõe as métricas de largura de banda, que podem ser obtidas a partir de métricas de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="025e2-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="025e2-435">Contador</span><span class="sxs-lookup"><span data-stu-id="025e2-435">counter</span></span> | <span data-ttu-id="025e2-436">Significado</span><span class="sxs-lookup"><span data-stu-id="025e2-436">Meaning</span></span>
------- | -------
<span data-ttu-id="025e2-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="025e2-437">BytesTransmitted</span></span> | <span data-ttu-id="025e2-438">Total de bytes enviados desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-438">Total bytes sent since boot</span></span>
<span data-ttu-id="025e2-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="025e2-439">BytesReceived</span></span> | <span data-ttu-id="025e2-440">Total de bytes recebidos desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-440">Total bytes received since boot</span></span>
<span data-ttu-id="025e2-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="025e2-441">BytesTotal</span></span> | <span data-ttu-id="025e2-442">Total de bytes enviadas ou recebidas desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="025e2-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="025e2-443">PacketsTransmitted</span></span> | <span data-ttu-id="025e2-444">Total de pacotes enviados desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-444">Total packets sent since boot</span></span>
<span data-ttu-id="025e2-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="025e2-445">PacketsReceived</span></span> | <span data-ttu-id="025e2-446">Total de pacotes recebidos desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-446">Total packets received since boot</span></span>
<span data-ttu-id="025e2-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="025e2-447">TotalRxErrors</span></span> | <span data-ttu-id="025e2-448">Número de recebe erros desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-448">Number of receive errors since boot</span></span>
<span data-ttu-id="025e2-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="025e2-449">TotalTxErrors</span></span> | <span data-ttu-id="025e2-450">Número de erros de transmitir desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="025e2-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="025e2-451">TotalCollisions</span></span> | <span data-ttu-id="025e2-452">Número de colisões é comunicado pelo portas de rede Olá desde o arranque</span><span class="sxs-lookup"><span data-stu-id="025e2-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="025e2-453">Embora esta classe é instanced, LAD não suporta a captura as métricas da rede agregadas em todos os dispositivos de rede.</span><span class="sxs-lookup"><span data-stu-id="025e2-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="025e2-454">métricas de Olá tooobtain para uma interface específica, tal como eth0, defina `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="025e2-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="025e2-455">métricas de Builtin para Olá classe do sistema de ficheiros</span><span class="sxs-lookup"><span data-stu-id="025e2-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="025e2-456">classe de sistema de ficheiros de métricas de Olá fornece informações sobre a utilização do sistema de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="025e2-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="025e2-457">Valores absoluto e percentagem são comunicados como seriam tooan apresentadas comum utilizador (não raiz).</span><span class="sxs-lookup"><span data-stu-id="025e2-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="025e2-458">Contador</span><span class="sxs-lookup"><span data-stu-id="025e2-458">counter</span></span> | <span data-ttu-id="025e2-459">Significado</span><span class="sxs-lookup"><span data-stu-id="025e2-459">Meaning</span></span>
------- | -------
<span data-ttu-id="025e2-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="025e2-460">FreeSpace</span></span> | <span data-ttu-id="025e2-461">Espaço em disco disponível em bytes</span><span class="sxs-lookup"><span data-stu-id="025e2-461">Available disk space in bytes</span></span>
<span data-ttu-id="025e2-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="025e2-462">UsedSpace</span></span> | <span data-ttu-id="025e2-463">Espaço em disco em bytes utilizado</span><span class="sxs-lookup"><span data-stu-id="025e2-463">Used disk space in bytes</span></span>
<span data-ttu-id="025e2-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="025e2-464">PercentFreeSpace</span></span> | <span data-ttu-id="025e2-465">Percentagem de espaço livre</span><span class="sxs-lookup"><span data-stu-id="025e2-465">Percentage free space</span></span>
<span data-ttu-id="025e2-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="025e2-466">PercentUsedSpace</span></span> | <span data-ttu-id="025e2-467">Percentagem de espaço utilizado</span><span class="sxs-lookup"><span data-stu-id="025e2-467">Percentage used space</span></span>
<span data-ttu-id="025e2-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="025e2-468">PercentFreeInodes</span></span> | <span data-ttu-id="025e2-469">Percentagem de inodes não utilizadas</span><span class="sxs-lookup"><span data-stu-id="025e2-469">Percentage of unused inodes</span></span>
<span data-ttu-id="025e2-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="025e2-470">PercentUsedInodes</span></span> | <span data-ttu-id="025e2-471">Percentagem de inodes alocado (em utilização) somadas em todos os sistemas de ficheiros instalados</span><span class="sxs-lookup"><span data-stu-id="025e2-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="025e2-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-472">BytesReadPerSecond</span></span> | <span data-ttu-id="025e2-473">Bytes lidos por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-473">Bytes read per second</span></span>
<span data-ttu-id="025e2-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="025e2-475">Bytes escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-475">Bytes written per second</span></span>
<span data-ttu-id="025e2-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-476">BytesPerSecond</span></span> | <span data-ttu-id="025e2-477">Bytes lidos ou escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-477">Bytes read or written per second</span></span>
<span data-ttu-id="025e2-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-478">ReadsPerSecond</span></span> | <span data-ttu-id="025e2-479">Operações de leitura por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-479">Read operations per second</span></span>
<span data-ttu-id="025e2-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-480">WritesPerSecond</span></span> | <span data-ttu-id="025e2-481">Operações por segundo de escrita</span><span class="sxs-lookup"><span data-stu-id="025e2-481">Write operations per second</span></span>
<span data-ttu-id="025e2-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-482">TransfersPerSecond</span></span> | <span data-ttu-id="025e2-483">Operações de leitura ou escrita por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-483">Read or write operations per second</span></span>

<span data-ttu-id="025e2-484">Valores agregados em todos os sistemas de ficheiros podem ser obtidos através da definição `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="025e2-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="025e2-485">Os valores de um sistema de ficheiros montado específico, tal como "/ mnt", pode ser obtido através da definição `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="025e2-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="025e2-486">métricas de Builtin para Olá classe do disco</span><span class="sxs-lookup"><span data-stu-id="025e2-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="025e2-487">classe de disco de métricas de Olá fornece informações sobre a utilização do dispositivo de disco.</span><span class="sxs-lookup"><span data-stu-id="025e2-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="025e2-488">Estas estatísticas aplicam toohello toda a unidade.</span><span class="sxs-lookup"><span data-stu-id="025e2-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="025e2-489">Se existirem vários sistemas de ficheiros num dispositivo, os contadores de Olá desse dispositivo são, efetivamente, agregados em todos eles.</span><span class="sxs-lookup"><span data-stu-id="025e2-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="025e2-490">Contador</span><span class="sxs-lookup"><span data-stu-id="025e2-490">counter</span></span> | <span data-ttu-id="025e2-491">Significado</span><span class="sxs-lookup"><span data-stu-id="025e2-491">Meaning</span></span>
------- | -------
<span data-ttu-id="025e2-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-492">ReadsPerSecond</span></span> | <span data-ttu-id="025e2-493">Operações de leitura por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-493">Read operations per second</span></span>
<span data-ttu-id="025e2-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-494">WritesPerSecond</span></span> | <span data-ttu-id="025e2-495">Operações por segundo de escrita</span><span class="sxs-lookup"><span data-stu-id="025e2-495">Write operations per second</span></span>
<span data-ttu-id="025e2-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-496">TransfersPerSecond</span></span> | <span data-ttu-id="025e2-497">Totais operações por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-497">Total operations per second</span></span>
<span data-ttu-id="025e2-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="025e2-498">AverageReadTime</span></span> | <span data-ttu-id="025e2-499">Segundos média por operação de leitura</span><span class="sxs-lookup"><span data-stu-id="025e2-499">Average seconds per read operation</span></span>
<span data-ttu-id="025e2-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="025e2-500">AverageWriteTime</span></span> | <span data-ttu-id="025e2-501">Segundos média por operação de escrita</span><span class="sxs-lookup"><span data-stu-id="025e2-501">Average seconds per write operation</span></span>
<span data-ttu-id="025e2-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="025e2-502">AverageTransferTime</span></span> | <span data-ttu-id="025e2-503">Segundos média por operação</span><span class="sxs-lookup"><span data-stu-id="025e2-503">Average seconds per operation</span></span>
<span data-ttu-id="025e2-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="025e2-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="025e2-505">Número médio de operações de disco em fila</span><span class="sxs-lookup"><span data-stu-id="025e2-505">Average number of queued disk operations</span></span>
<span data-ttu-id="025e2-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="025e2-507">Número de bytes lidos por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-507">Number of bytes read per second</span></span>
<span data-ttu-id="025e2-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="025e2-509">Número de bytes escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-509">Number of bytes written per second</span></span>
<span data-ttu-id="025e2-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="025e2-510">BytesPerSecond</span></span> | <span data-ttu-id="025e2-511">Número de bytes lidos ou escritos por segundo</span><span class="sxs-lookup"><span data-stu-id="025e2-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="025e2-512">Valores agregados em todos os discos podem ser obtidos através da definição `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="025e2-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="025e2-513">informações de tooget para um dispositivo específico (por exemplo, dev/sdf1), definir `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="025e2-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="025e2-514">Instalar e configurar LAD 3.0 através da CLI</span><span class="sxs-lookup"><span data-stu-id="025e2-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="025e2-515">Pressupondo que as definições de protegidos estão no ficheiro de Olá PrivateConfig.json e as informações de configuração pública estão a ser PublicConfig.json, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="025e2-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="025e2-516">comando Olá parte do princípio de que está a utilizar o modo de gestão de recursos do Azure (arm) Olá de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="025e2-517">tooconfigure LAD para implementação clássica VMs (ASM) do modelo, mude demasiado "asm" modo (`azure config mode asm`) e omitir o nome do grupo de recursos Olá no comando Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="025e2-518">Para obter mais informações, consulte Olá [documentação da CLI de plataforma](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="025e2-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="025e2-519">Uma configuração de exemplo LAD 3.0</span><span class="sxs-lookup"><span data-stu-id="025e2-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="025e2-520">Com base no Olá anterior a uma configuração de extensão de LAD 3.0 de exemplo com alguma explicação sobre as definições, aqui.</span><span class="sxs-lookup"><span data-stu-id="025e2-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="025e2-521">tooapply caso tooyour deste exemplo, deve utilizar o seu próprio nome de conta de armazenamento, SAS token de conta e tokens EventHubs SAS.</span><span class="sxs-lookup"><span data-stu-id="025e2-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="025e2-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="025e2-522">PrivateConfig.json</span></span>

<span data-ttu-id="025e2-523">Configuram estas definições privadas:</span><span class="sxs-lookup"><span data-stu-id="025e2-523">These private settings configure:</span></span>

* <span data-ttu-id="025e2-524">uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="025e2-524">a storage account</span></span>
* <span data-ttu-id="025e2-525">um token SAS conta correspondente</span><span class="sxs-lookup"><span data-stu-id="025e2-525">a matching account SAS token</span></span>
* <span data-ttu-id="025e2-526">vários sinks (JsonBlob ou EventHubs com SAS tokens)</span><span class="sxs-lookup"><span data-stu-id="025e2-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="025e2-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="025e2-527">PublicConfig.json</span></span>

<span data-ttu-id="025e2-528">Estas definições públicas causam LAD para:</span><span class="sxs-lookup"><span data-stu-id="025e2-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="025e2-529">Carregue as métricas de tempo de processador de percentagem e utilizado--espaço em disco toohello `WADMetrics*` tabela</span><span class="sxs-lookup"><span data-stu-id="025e2-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="025e2-530">Carregar mensagens do syslog instalações "utilizador" e a gravidade "informações" toohello `LinuxSyslog*` tabela</span><span class="sxs-lookup"><span data-stu-id="025e2-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="025e2-531">Carregar em bruto OMI consulta resultados (PercentProcessorTime e PercentIdleTime) toohello denominado `LinuxCPU` tabela</span><span class="sxs-lookup"><span data-stu-id="025e2-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="025e2-532">Carregar anexadas linhas no ficheiro `/var/log/myladtestlog` toohello `MyLadTestLog` tabela</span><span class="sxs-lookup"><span data-stu-id="025e2-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="025e2-533">Em cada caso, os dados também são carregados para:</span><span class="sxs-lookup"><span data-stu-id="025e2-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="025e2-534">Armazenamento de Blobs do Azure (nome do contentor é definido no sink de JsonBlob Olá)</span><span class="sxs-lookup"><span data-stu-id="025e2-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="025e2-535">Ponto final de EventHubs (conforme especificado no receptor de EventHubs Olá)</span><span class="sxs-lookup"><span data-stu-id="025e2-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="025e2-536">Olá `resourceId` no Olá configuração tem de corresponder ao que de dimensionamento de máquina virtual VM ou Olá Olá definida.</span><span class="sxs-lookup"><span data-stu-id="025e2-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="025e2-537">Métricas de plataforma do Azure charting e alertas sabe Olá resourceId de Olá VM que está a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="025e2-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="025e2-538">Dados de Olá toofind-espera para a VM utilizando a chave de pesquisa do Olá resourceId Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="025e2-539">Se utilizar o dimensionamento automático do Azure, Olá resourceId na configuração de dimensionamento automático de Olá tem de corresponder ao resourceId Olá utilizado pelo LAD.</span><span class="sxs-lookup"><span data-stu-id="025e2-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="025e2-540">Olá resourceId está incorporado no Olá os nomes de JsonBlobs escritas pelo LAD.</span><span class="sxs-lookup"><span data-stu-id="025e2-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="025e2-541">Ver os seus dados</span><span class="sxs-lookup"><span data-stu-id="025e2-541">View your data</span></span>

<span data-ttu-id="025e2-542">Utilizar dados de desempenho do Olá tooview portal do Azure ou definir alertas:</span><span class="sxs-lookup"><span data-stu-id="025e2-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![Imagem](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="025e2-544">Olá `performanceCounters` sempre os dados são armazenados uma tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="025e2-545">APIs de armazenamento do Azure estão disponíveis para vários idiomas e plataformas.</span><span class="sxs-lookup"><span data-stu-id="025e2-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="025e2-546">Os dados enviados tooJsonBlob sinks são armazenados em blobs na conta do storage Olá com o nome no Olá [protegidos definições](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="025e2-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="025e2-547">Pode consumir dados de BLOBs de Olá utilizando as APIs de armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="025e2-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="025e2-548">Além disso, pode utilizar estes dados de Olá de tooaccess de ferramentas da IU no armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="025e2-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="025e2-549">Explorador de servidores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="025e2-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="025e2-550">[Explorador de armazenamento do Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Explorador de armazenamento do Azure").</span><span class="sxs-lookup"><span data-stu-id="025e2-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="025e2-551">Este instantâneo de uma sessão do Explorador de armazenamento do Microsoft Azure mostra Olá gerado tabelas de armazenamento do Azure e contentores de uma extensão de LAD 3.0 configurada corretamente na VM de teste.</span><span class="sxs-lookup"><span data-stu-id="025e2-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="025e2-552">imagem de Olá não corresponde exatamente ao hello [exemplo de configuração LAD 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="025e2-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![Imagem](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="025e2-554">Consulte Olá relevante [EventHubs documentação](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn como tooconsume mensagens publicadas tooan EventHubs endpoint.</span><span class="sxs-lookup"><span data-stu-id="025e2-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="025e2-555">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="025e2-555">Next steps</span></span>

* <span data-ttu-id="025e2-556">Criar métricas alertas no [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) recolher com base nas métricas Olá.</span><span class="sxs-lookup"><span data-stu-id="025e2-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="025e2-557">Criar [monitorização gráficos](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para as métricas.</span><span class="sxs-lookup"><span data-stu-id="025e2-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="025e2-558">Saiba como demasiado[criar um conjunto de dimensionamento de máquina virtual](/azure/virtual-machines/linux/tutorial-create-vmss) utilizando o dimensionamento automático toocontrol de métricas.</span><span class="sxs-lookup"><span data-stu-id="025e2-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
