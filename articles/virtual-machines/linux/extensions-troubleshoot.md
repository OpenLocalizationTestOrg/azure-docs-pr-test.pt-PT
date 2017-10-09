---
title: "aaaTroubleshooting VM com Linux falhas de extensão | Microsoft Docs"
description: "Saiba mais sobre a resolução de falhas de extensão de VM do Linux do Azure"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="06737-103">Resolução de falhas de extensão de VM do Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="06737-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="06737-104">Visualizar o estado de extensão</span><span class="sxs-lookup"><span data-stu-id="06737-104">Viewing extension status</span></span>
<span data-ttu-id="06737-105">Modelos Azure Resource Manager podem ser executados a partir Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="06737-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="06737-106">Assim que o modelo de Olá é executado, pode ser visualizado estado da extensão Olá Explorador de recursos do Azure ou Olá ferramentas de linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="06737-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="06737-107">Segue-se um exemplo:</span><span class="sxs-lookup"><span data-stu-id="06737-107">Here is an example:</span></span>

<span data-ttu-id="06737-108">CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="06737-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="06737-109">O resultado de exemplo de Olá é:</span><span class="sxs-lookup"><span data-stu-id="06737-109">Here is hello sample output:</span></span>

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  <span data-ttu-id="06737-110">]</span><span class="sxs-lookup"><span data-stu-id="06737-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="06737-111">Resolução de falhas de Extenson:</span><span class="sxs-lookup"><span data-stu-id="06737-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="06737-112">Executar novamente a extensão de Olá no Olá VM</span><span class="sxs-lookup"><span data-stu-id="06737-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="06737-113">Se estiver a executar scripts num Olá VM utilizando a extensão de Script personalizado, por vezes, é possível executar um erro em que a VM foi criada com êxito mas Olá script falhou.</span><span class="sxs-lookup"><span data-stu-id="06737-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="06737-114">Nestes conditons Olá recomendado toorecover de forma do erro tooremove Olá extensão e novamente o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="06737-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="06737-115">Nota: No futuro, esta funcionalidade seria tooremove avançada Olá necessidade para desinstalar a extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="06737-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="06737-116">Remover extensão de Olá da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="06737-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="06737-117">Onde "publsher-name" corresponde ao tipo de extensão de toohello da saída de Olá de "get-instância-vista da vm do azure" e o nome é Olá nome do recurso de extensão de Olá a partir do modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="06737-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="06737-118">Assim que tiver sido removido extensão Olá, o modelo de Olá pode ser novamente executado toorun Olá scripts no Olá VM.</span><span class="sxs-lookup"><span data-stu-id="06737-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

