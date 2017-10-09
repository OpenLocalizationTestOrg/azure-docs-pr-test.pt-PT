---
title: "Perguntas mais frequentes de conjuntos de dimensionamento de máquina virtual aaaAzure | Microsoft Docs"
description: "Obter toofrequently respostas mais frequentes sobre o sobre conjuntos de dimensionamento de máquina virtual."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="7c179-103">Perguntas mais frequentes de conjuntos de dimensionamento de máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="7c179-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="7c179-104">Obtenha respostas define toofrequently mais frequentes sobre o sobre o dimensionamento da máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="7c179-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="7c179-105">Dimensionamento Automático</span><span class="sxs-lookup"><span data-stu-id="7c179-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="7c179-106">Quais são as melhores práticas para o dimensionamento automático do Azure?</span><span class="sxs-lookup"><span data-stu-id="7c179-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="7c179-107">Para melhores práticas para o dimensionamento automático, consulte [melhores práticas para máquinas virtuais de dimensionamento automático](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="7c179-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="7c179-108">Onde posso encontrar os nomes de métricos de dimensionamento automático que utiliza a métrica do anfitrião?</span><span class="sxs-lookup"><span data-stu-id="7c179-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="7c179-109">Para nomes de métricos de dimensionamento automático que utiliza a métrica baseada no anfitrião, consulte [suportado métricas com a monitorização do Azure](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="7c179-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="7c179-110">Existem os exemplos de dimensionamento automático com base num comprimento de fila e o tópico do Service Bus do Azure?</span><span class="sxs-lookup"><span data-stu-id="7c179-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="7c179-111">Sim.</span><span class="sxs-lookup"><span data-stu-id="7c179-111">Yes.</span></span> <span data-ttu-id="7c179-112">Para obter exemplos de dimensionamento automático com base num comprimento de fila e o tópico do Service Bus do Azure, consulte [métricas comuns de dimensionamento automático de Monitor de Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="7c179-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="7c179-113">Para uma fila de barramento de serviço, utilize Olá JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c179-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="7c179-114">Para uma fila de armazenamento, utilize Olá JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c179-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="7c179-115">Substitua os valores de exemplo pelo seu recurso Uniform Resource Identifiers (URIs).</span><span class="sxs-lookup"><span data-stu-id="7c179-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="7c179-116">Deve posso dimensionamento automático utilizando as métricas baseada no anfitrião ou uma extensão de diagnóstico?</span><span class="sxs-lookup"><span data-stu-id="7c179-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="7c179-117">Pode criar uma definição de dimensionamento automático num métricas de nível do anfitrião VM toouse ou métricas de com base no SO convidado.</span><span class="sxs-lookup"><span data-stu-id="7c179-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="7c179-118">Para obter uma lista das métricas suportadas, consulte [métricas comuns de dimensionamento automático de Monitor de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="7c179-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="7c179-119">Para obter um exemplo completo para conjuntos de dimensionamento de máquina virtual, consulte [configuração avançada de dimensionamento automático através de modelos do Resource Manager para conjuntos de dimensionamento de máquina virtual](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="7c179-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="7c179-120">exemplo de Olá utiliza a métrica de CPU Olá ao nível do anfitrião e uma métrica de contagem de mensagens.</span><span class="sxs-lookup"><span data-stu-id="7c179-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="7c179-121">Como definir a regras de alertas sobre um conjunto de dimensionamento de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7c179-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="7c179-122">Pode criar alertas nas métricas para conjuntos de dimensionamento de máquina virtual através do PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c179-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="7c179-123">Para obter mais informações, consulte [Azure Monitor PowerShell rápido iniciar amostras](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) e [CLI de várias plataformas de Monitor de Azure rápido iniciar amostras](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="7c179-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="7c179-124">Olá TargetResourceId do conjunto de dimensionamento de máquina virtual de Olá tem o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="7c179-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="7c179-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/Providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="7c179-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="7c179-126">Pode escolher qualquer contador de desempenho da VM como tooset métrica Olá um alerta para.</span><span class="sxs-lookup"><span data-stu-id="7c179-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="7c179-127">Para obter mais informações, consulte [métricas de SO convidado para VMs do Windows baseados no Resource Manager](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) e [métricas de SO convidado para VMs com Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) no Olá [métricas comuns de dimensionamento automático Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artigo.</span><span class="sxs-lookup"><span data-stu-id="7c179-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="7c179-128">Como configurar Dimensionar automaticamente conforme um conjunto utilizando o PowerShell de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="7c179-129">tooset cópias de segurança de dimensionamento automático numa escala de máquina virtual definido através do PowerShell, consulte a mensagem de blogue de Olá [como conjunto de dimensionamento automático de tooadd tooan dimensionamento de máquina virtual do Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="7c179-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="7c179-130">Certificados</span><span class="sxs-lookup"><span data-stu-id="7c179-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="7c179-131">Como posso enviar em segurança toohello um certificado VM?</span><span class="sxs-lookup"><span data-stu-id="7c179-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="7c179-132">Como aprovisionar um toorun de conjunto de dimensionamento de máquina virtual um Web site onde hello SSL para o Web site Olá vem incluído em segurança de uma configuração de certificado?</span><span class="sxs-lookup"><span data-stu-id="7c179-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="7c179-133">(Olá comuns rotação a operação de certificado deverá ser quase Olá mesmo que uma operação de atualização da configuração.) Tem um exemplo de como toodo Isto?</span><span class="sxs-lookup"><span data-stu-id="7c179-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="7c179-134">toosecurely são enviados toohello um certificado VM, pode instalar um certificado de cliente diretamente para um arquivo de certificados do Windows do Cofre de chaves do cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="7c179-135">Utilize Olá JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c179-135">Use hello following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="7c179-136">código de Olá suporta o Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="7c179-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="7c179-137">Para obter mais informações, consulte [criar ou atualizar um dimensionamento da máquina virtual definir](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c179-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="7c179-138">Exemplo de certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="7c179-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="7c179-139">Crie um certificado autoassinado no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="7c179-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="7c179-140">Utilize Olá os seguintes comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7c179-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="7c179-141">Este oferece comando Olá entrada de modelo do Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="7c179-142">Para obter um exemplo de como toocreate um certificado autoassinado no Cofre de chaves, consulte o artigo [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="7c179-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="7c179-143">Alterar o modelo do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="7c179-144">Adicionar esta propriedade demasiado**virtualMachineProfile**, como parte da Olá recursos de conjunto de dimensionamento de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="7c179-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="7c179-145">Pode especificar um toouse do par de chaves SSH para a autenticação SSH com uma escala de máquina virtual Linux definido a partir de um modelo do Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="7c179-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="7c179-146">Sim.</span><span class="sxs-lookup"><span data-stu-id="7c179-146">Yes.</span></span> <span data-ttu-id="7c179-147">Olá REST API para **osProfile** é semelhante API REST de VM padrão toohello.</span><span class="sxs-lookup"><span data-stu-id="7c179-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="7c179-148">Incluir **osProfile** no seu modelo:</span><span class="sxs-lookup"><span data-stu-id="7c179-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="7c179-149">Este bloco JSON é utilizado na [modelo de início rápido do Olá 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7c179-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="7c179-150">Olá perfil de SO também é utilizado em [Olá grelayhost.json GitHub rápido iniciar modelo](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="7c179-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="7c179-151">Para obter mais informações, consulte [criar ou atualizar um dimensionamento da máquina virtual definir](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="7c179-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="7c179-152">Como posso remover certificados preteridos?</span><span class="sxs-lookup"><span data-stu-id="7c179-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="7c179-153">tooremove preterido certificados, remover certificado antigo de Olá Olá cofre certificados na lista.</span><span class="sxs-lookup"><span data-stu-id="7c179-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="7c179-154">Deixe todos os certificados de Olá que pretende que tooremain no seu computador na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="7c179-155">Isto não remove o certificado de Olá de todas as suas VMs.</span><span class="sxs-lookup"><span data-stu-id="7c179-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="7c179-156">Também não adiciona Olá certificado toonew VMs que são criadas no conjunto de dimensionamento de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="7c179-157">certificado Olá tooremove VMs existentes, escrever um script personalizado certificados de Olá extensão toomanually remover do seu arquivo de certificados.</span><span class="sxs-lookup"><span data-stu-id="7c179-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="7c179-158">Como posso inserir uma chave pública SSH na camada SSH do conjunto de dimensionamento do Olá máquina virtual durante o aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="7c179-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="7c179-159">Pretende toostore Olá SSH públicos valores de chave no Cofre de chaves do Azure e, em seguida, utilizá-los no meu modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c179-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="7c179-160">Se está a fornecer Olá VMs apenas com uma chave SSH pública, não precisa de tooput Olá as chaves públicas no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="7c179-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="7c179-161">As chaves públicas não são secretas.</span><span class="sxs-lookup"><span data-stu-id="7c179-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="7c179-162">Pode fornecer as chaves públicas SSH em texto simples quando criar uma VM com Linux:</span><span class="sxs-lookup"><span data-stu-id="7c179-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="7c179-163">nome do elemento linuxConfiguration</span><span class="sxs-lookup"><span data-stu-id="7c179-163">linuxConfiguration element name</span></span> | <span data-ttu-id="7c179-164">Necessário</span><span class="sxs-lookup"><span data-stu-id="7c179-164">Required</span></span> | <span data-ttu-id="7c179-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="7c179-165">Type</span></span> | <span data-ttu-id="7c179-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="7c179-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="7c179-167">SSH</span><span class="sxs-lookup"><span data-stu-id="7c179-167">ssh</span></span> | <span data-ttu-id="7c179-168">Não</span><span class="sxs-lookup"><span data-stu-id="7c179-168">No</span></span> | <span data-ttu-id="7c179-169">Coleção</span><span class="sxs-lookup"><span data-stu-id="7c179-169">Collection</span></span> | <span data-ttu-id="7c179-170">Especifica a configuração da chave SSH Olá para um SO Linux</span><span class="sxs-lookup"><span data-stu-id="7c179-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="7c179-171">Caminho</span><span class="sxs-lookup"><span data-stu-id="7c179-171">path</span></span> | <span data-ttu-id="7c179-172">Sim</span><span class="sxs-lookup"><span data-stu-id="7c179-172">Yes</span></span> | <span data-ttu-id="7c179-173">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7c179-173">String</span></span> | <span data-ttu-id="7c179-174">Especifica o caminho do ficheiro Olá Linux em que as chaves SSH Olá ou o certificado deve estar localizado</span><span class="sxs-lookup"><span data-stu-id="7c179-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="7c179-175">keyData</span><span class="sxs-lookup"><span data-stu-id="7c179-175">keyData</span></span> | <span data-ttu-id="7c179-176">Sim</span><span class="sxs-lookup"><span data-stu-id="7c179-176">Yes</span></span> | <span data-ttu-id="7c179-177">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7c179-177">String</span></span> | <span data-ttu-id="7c179-178">Especifica uma chave pública de SSH com codificação base64</span><span class="sxs-lookup"><span data-stu-id="7c179-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="7c179-179">Por exemplo, consulte [modelo de início rápido do Olá 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7c179-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="7c179-180">Quando executar `Update-AzureRmVmss` após a adição de mais de um certificado de Olá mesma chave de cofre, vejo Olá seguintes mensagens:</span><span class="sxs-lookup"><span data-stu-id="7c179-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="7c179-181">Update-AzureRmVmss: Segredo de lista contém instâncias repetidas de /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname} < minha subscrição-id > / resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, que não é permitida.</span><span class="sxs-lookup"><span data-stu-id="7c179-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="7c179-182">Isto pode acontecer se tentar toore-adicionar Olá mesmo cofre em vez de utilizar um novo certificado de cofre para o Cofre de origem existente Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="7c179-183">Olá `Add-AzureRmVmssSecret` comando não funcionar corretamente, se estiver a adicionar segredos adicionais.</span><span class="sxs-lookup"><span data-stu-id="7c179-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="7c179-184">tooadd mais segredos de Olá mesmo Cofre de chaves, atualização Olá $vmss.properties.osProfile.secrets[0].vaultCertificates lista.</span><span class="sxs-lookup"><span data-stu-id="7c179-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="7c179-185">Para obter Olá esperado estrutura de entrada, consulte [criar ou atualizar uma máquina virtual definir](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c179-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="7c179-186">Encontrar o segredo de Olá no objeto conjunto de dimensionamento de máquina virtual de Olá que se encontra no Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="7c179-187">Em seguida, adicionar a sua lista de toohello de referência (Olá URL e nome de arquivo secreta Olá) de certificado associada Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="7c179-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="7c179-188">Atualmente, não é possível remover certificados dos VMs utilizando a API de conjunto de dimensionamento de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="7c179-189">Novas VMs não terão o certificado antigo Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="7c179-190">No entanto, as VMs que têm o certificado de Olá e que já são implementadas terão o certificado antigo Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="7c179-191">Pode emitir conjunto sem fornecer a palavra-passe de Olá, quando o certificado de Olá está no arquivo secreta Olá de dimensionamento de máquina virtual de toohello de certificados?</span><span class="sxs-lookup"><span data-stu-id="7c179-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="7c179-192">Não é necessário toohard código palavras-passe em scripts.</span><span class="sxs-lookup"><span data-stu-id="7c179-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="7c179-193">Pode obter dinamicamente as palavras-passe com permissões de Olá utilizar script de implementação de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="7c179-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="7c179-194">Se tiver um script que se move um certificado a partir do Cofre de chaves de arquivo secreta Olá, Olá arquivo secreto `get certificate` comando também produz Olá palavra-passe do ficheiro. pfx Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="7c179-195">Como Olá segredos virtualMachineProfile.osProfile para um dimensionamento da máquina virtual definir a propriedade de trabalho?</span><span class="sxs-lookup"><span data-stu-id="7c179-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="7c179-196">Por que motivo precisa valor de sourceVault Olá quando tenho toospecify Olá URI absoluto de um certificado utilizando Olá certificateUrl propriedade?</span><span class="sxs-lookup"><span data-stu-id="7c179-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="7c179-197">Uma referência de certificado de gestão remota do Windows (WinRM) deve estar presente no Olá propriedade segredos Olá perfil do SO.</span><span class="sxs-lookup"><span data-stu-id="7c179-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="7c179-198">objetivo Olá que indica que o Cofre de origem Olá é políticas (ACL) de lista de controlo de acesso de tooenforce que existem no modelo de serviço de nuvem do Azure de um utilizador.</span><span class="sxs-lookup"><span data-stu-id="7c179-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="7c179-199">Se o Cofre de origem Olá não está especificado, os utilizadores que não dispõe de permissões toodeploy ou acesso segredos tooa Cofre de chaves será toothrough capaz de um fornecedor de recursos de computação (CRP).</span><span class="sxs-lookup"><span data-stu-id="7c179-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="7c179-200">As ACLs existem mesmo para recursos que não existem.</span><span class="sxs-lookup"><span data-stu-id="7c179-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="7c179-201">Se fornecer um ID de Cofre de origem incorreto, mas um URL do Cofre de chaves válida, é comunicado um erro ao consultar operação Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="7c179-202">Se adicionar tooan segredos existente conjunto de dimensionamento da máquina virtual, são segredos Olá injetados para VMs existentes, ou apenas para novos?</span><span class="sxs-lookup"><span data-stu-id="7c179-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="7c179-203">Certificados são adicionados tooall as suas VMs, mesmo pré-existentes aqueles.</span><span class="sxs-lookup"><span data-stu-id="7c179-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="7c179-204">Se o dimensionamento da máquina virtual definir a propriedade de upgradePolicy estiver definido demasiado**manual**, Olá é adicionar certificado toohello VM quando efetuar uma atualização manual Olá VM.</span><span class="sxs-lookup"><span data-stu-id="7c179-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="7c179-205">Onde colocar o certificados para VMs com Linux?</span><span class="sxs-lookup"><span data-stu-id="7c179-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="7c179-206">toolearn como toodeploy certificados para VMs com Linux, consulte [implementar tooVMs de certificados de um cofre de chaves gerida pelo cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="7c179-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="7c179-207">Como adicionar um novo cofre certificado tooa novo objeto certificado?</span><span class="sxs-lookup"><span data-stu-id="7c179-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="7c179-208">tooadd um cofre certificado tooan segredo existente, consulte Olá seguinte o exemplo do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c179-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="7c179-209">Utilize apenas um objeto secreto.</span><span class="sxs-lookup"><span data-stu-id="7c179-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="7c179-210">O que acontece toocertificates recriar uma VM?</span><span class="sxs-lookup"><span data-stu-id="7c179-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="7c179-211">Se criar nova imagem de uma VM, os certificados são eliminados.</span><span class="sxs-lookup"><span data-stu-id="7c179-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="7c179-212">Disco do SO todo Olá eliminações de reprocessamento de imagem.</span><span class="sxs-lookup"><span data-stu-id="7c179-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="7c179-213">O que acontece se eliminar um certificado a partir do Cofre de chaves Olá?</span><span class="sxs-lookup"><span data-stu-id="7c179-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="7c179-214">Se segredo Olá é eliminado do Cofre de chaves Olá e, em seguida, execute `stop deallocate` para todas as suas VMs e, em seguida, iniciá-los novamente, irá ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="7c179-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="7c179-215">Falha de Olá ocorre porque Olá CRP necessita segredos de Olá tooretrieve do Cofre de chaves Olá, mas não pode ser.</span><span class="sxs-lookup"><span data-stu-id="7c179-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="7c179-216">Neste cenário, pode eliminar certificados Olá do modelo de conjunto de dimensionamento de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="7c179-217">componente de CRP de Olá não persiste segredos do cliente.</span><span class="sxs-lookup"><span data-stu-id="7c179-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="7c179-218">Se executar `stop deallocate` para todas as VMs no conjunto de dimensionamento de máquina virtual de Olá, cache Olá é eliminado.</span><span class="sxs-lookup"><span data-stu-id="7c179-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="7c179-219">Neste cenário, segredos são obtidos a partir do Cofre de chaves Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="7c179-220">Não ocorrer este problema durante a ampliação porque não existe uma cópia em cache do segredo Olá no Service Fabric do Azure (no modelo de recursos de infraestrutura único inquilino Olá).</span><span class="sxs-lookup"><span data-stu-id="7c179-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="7c179-221">Por que razão tem a localização exata de Olá toospecify para o URL de certificado Olá (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), conforme indicado na [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="7c179-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="7c179-222">Olá documentação do Cofre de chaves do Azure indica que Olá que obter API de REST do segredo deverá devolver a versão mais recente do Olá do segredo Olá se versão Olá não for especificado.</span><span class="sxs-lookup"><span data-stu-id="7c179-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="7c179-223">Método</span><span class="sxs-lookup"><span data-stu-id="7c179-223">Method</span></span> | <span data-ttu-id="7c179-224">URL</span><span class="sxs-lookup"><span data-stu-id="7c179-224">URL</span></span>
--- | ---
<span data-ttu-id="7c179-225">INTRODUÇÃO</span><span class="sxs-lookup"><span data-stu-id="7c179-225">GET</span></span> | <span data-ttu-id="7c179-226">https://mykeyvault.Vault.Azure.NET/Secrets/ {nome-segredo} / {segredo-version}? api-version = {api-version}</span><span class="sxs-lookup"><span data-stu-id="7c179-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="7c179-227">Substitua {*segredo-name*} com o nome de Olá e substitua {*segredo versão*} com a versão de Olá do segredo Olá pretende tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="7c179-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="7c179-228">versão secreta Olá poderão ser excluído.</span><span class="sxs-lookup"><span data-stu-id="7c179-228">hello secret version might be excluded.</span></span> <span data-ttu-id="7c179-229">Nesse caso, a versão atual do Olá é obtido.</span><span class="sxs-lookup"><span data-stu-id="7c179-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="7c179-230">Por que razão tem versão de certificado de Olá toospecify quando utilizar o Cofre de chaves?</span><span class="sxs-lookup"><span data-stu-id="7c179-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="7c179-231">objetivo Olá versão de certificado de Olá requisito toospecify Olá Cofre de chaves é toomake-limpar toohello utilizador o certificado for implementado nas respetivas VMs.</span><span class="sxs-lookup"><span data-stu-id="7c179-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="7c179-232">Se criar uma VM e, em seguida, atualize o seu segredo no Cofre de chaves Olá, certificado novo Olá não é transferido tooyour VMs.</span><span class="sxs-lookup"><span data-stu-id="7c179-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="7c179-233">Mas as suas VMs aparecem tooreference e novas VMs obtêm segredo Olá de novo.</span><span class="sxs-lookup"><span data-stu-id="7c179-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="7c179-234">tooavoid, são necessário tooreference uma versão secreta.</span><span class="sxs-lookup"><span data-stu-id="7c179-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="7c179-235">A minha equipa funciona com vários certificados que são distribuídos toous como chaves públicas. cer.</span><span class="sxs-lookup"><span data-stu-id="7c179-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="7c179-236">O que é Olá abordagem para implementar o conjunto de dimensionamento da máquina virtual estes certificados tooa recomendada?</span><span class="sxs-lookup"><span data-stu-id="7c179-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="7c179-237">toodeploy. cer as chaves públicas tooa escala conjunto da máquina virtual, pode gerar um ficheiro. pfx que contém apenas os ficheiros. cer.</span><span class="sxs-lookup"><span data-stu-id="7c179-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="7c179-238">toodo, utilize `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="7c179-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="7c179-239">Por exemplo, carregue o ficheiro. cer de Olá como um objeto de x509Certificate2 em c# ou PowerShell e, em seguida, chame o método de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="7c179-240">Para obter mais informações, consulte [X509Certificate.Export método (X509ContentType, cadeia)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="7c179-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="7c179-241">Não vejo uma opção para os utilizadores toopass em certificados como cadeias de base64.</span><span class="sxs-lookup"><span data-stu-id="7c179-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="7c179-242">A maioria dos fornecedores de recursos tem esta opção.</span><span class="sxs-lookup"><span data-stu-id="7c179-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="7c179-243">tooemulate transmitir num certificado como uma cadeia base64, pode extrair Olá mais recente com versão do URL num modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c179-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="7c179-244">Inclua Olá propriedade JSON no seu modelo do Resource Manager a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c179-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="7c179-245">Alguns têm certificados de toowrap em objetos JSON no cofres de chaves?</span><span class="sxs-lookup"><span data-stu-id="7c179-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="7c179-246">Em conjuntos de dimensionamento de máquina virtual e VMs, certificados tem de ser moldados numa objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="7c179-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="7c179-247">Também é suportada a Olá o tipo de conteúdo application/x-pkcs12.</span><span class="sxs-lookup"><span data-stu-id="7c179-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="7c179-248">Para obter instruções sobre como utilizar o application/x-pkcs12, consulte [os certificados PFX no Cofre de chaves do Azure](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="7c179-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="7c179-249">Atualmente não suportamos. cer ficheiros.</span><span class="sxs-lookup"><span data-stu-id="7c179-249">We currently do not support .cer files.</span></span> <span data-ttu-id="7c179-250">ficheiros. cer toouse, exportá-las em contentores. pfx.</span><span class="sxs-lookup"><span data-stu-id="7c179-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="7c179-251">Conformidade</span><span class="sxs-lookup"><span data-stu-id="7c179-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="7c179-252">Estão em conformidade de PCI define o dimensionamento da máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="7c179-253">Conjuntos de dimensionamento de máquina virtual são uma camada de API dinâmico sobreposta Olá CRP.</span><span class="sxs-lookup"><span data-stu-id="7c179-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="7c179-254">Ambos os componentes fazem parte da plataforma de computação de Olá no Olá árvore de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c179-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="7c179-255">Numa perspetiva de conformidade, conjuntos de dimensionamento de máquina virtual são uma parte fundamental da plataforma de computação do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="7c179-256">Estes partilham uma equipa, ferramentas, processos, a metodologia de implementação, controlos de segurança, just-in-time (JIT) compilação, monitorização, alertas e assim sucessivamente, com CRP Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="7c179-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="7c179-257">Conjuntos de dimensionamento de máquina virtual são da indústria de cartão de pagamento (PCI)-conformidade porque Olá CRP faz parte de atestado de PCI dados segurança Standard (DSS) atual Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="7c179-258">Para obter mais informações, consulte [Olá Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="7c179-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="7c179-259">Extensões</span><span class="sxs-lookup"><span data-stu-id="7c179-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="7c179-260">Como posso eliminar uma extensão de conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="7c179-261">toodelete um dimensionamento da máquina virtual Definir extensão, Olá utilize seguinte o exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7c179-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="7c179-262">Pode encontrar o valor extensionName Olá `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="7c179-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="7c179-263">Existe que um dimensionamento da máquina virtual definir exemplo de modelo que se integra com o Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="7c179-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="7c179-264">Para um dimensionamento da máquina virtual definido exemplo de modelo que se integra com o Operations Management Suite, consulte o segundo exemplo de Olá na [implementar um cluster do Service Fabric do Azure e ative a monitorização utilizando a análise de registos](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="7c179-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="7c179-265">Extensões parecem toorun em paralelo em conjuntos de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c179-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="7c179-266">Isto faz com que a minha toofail de extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="7c179-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="7c179-267">O que posso fazer toofix Isto?</span><span class="sxs-lookup"><span data-stu-id="7c179-267">What can I do toofix this?</span></span>

<span data-ttu-id="7c179-268">toolearn sobre a sequenciação de extensão em conjuntos de dimensionamento de máquina virtual, consulte [sequenciação extensão em conjuntos de dimensionamento de máquina virtual do Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="7c179-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="7c179-269">Como redefinir as palavras-passe de Olá para VMs no meu conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="7c179-270">tooreset Olá palavra-passe para as VMs no seu dimensionamento de máquina virtual definido, utilização de extensões de acesso VM.</span><span class="sxs-lookup"><span data-stu-id="7c179-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="7c179-271">Utilize Olá seguinte o exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7c179-271">Use hello following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="7c179-272">Como adicionar uma extensão tooall VMs a minha conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="7c179-273">Se a política de atualização estiver definida demasiado**automática**, voltar a implementar o modelo de Olá com novas propriedades de extensão Olá atualiza todas as VMs.</span><span class="sxs-lookup"><span data-stu-id="7c179-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="7c179-274">Se a política de atualização estiver definida demasiado**manual**, primeiro atualizar extensão Olá e, em seguida, atualizar manualmente todas as instâncias nas suas VMs.</span><span class="sxs-lookup"><span data-stu-id="7c179-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="7c179-275">Se forem atualizadas extensões Olá associadas um conjunto de dimensionamento de máquina virtual existente, existentes VMs afetadas?</span><span class="sxs-lookup"><span data-stu-id="7c179-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="7c179-276">(Ou seja, será Olá VMs *não* modelo de conjunto de dimensionamento de máquina virtual Olá correspondência?) Ou são ignorados?</span><span class="sxs-lookup"><span data-stu-id="7c179-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="7c179-277">Quando um computador existente é healed de serviço ou recriado, são Olá scripts que estão atualmente configuradas no conjunto de dimensionamento de máquina virtual de Olá executado ou são scripts de Olá que foram configuradas quando Olá que VM foi criada pela primeira vez utilizado?</span><span class="sxs-lookup"><span data-stu-id="7c179-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="7c179-278">Se definir a definição da extensão Olá no dimensionamento de máquina virtual de Olá é atualizar o modelo e Olá upgradePolicy for definida demasiado**automática**, atualiza Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="7c179-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="7c179-279">Se Olá upgradePolicy for definida demasiado**manual**, extensões sinalizadas como não corresponde ao modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="7c179-280">Se uma VM existente healed de serviço, é apresentada como um reinício e extensões de Olá não são novamente executadas.</span><span class="sxs-lookup"><span data-stu-id="7c179-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="7c179-281">Se é recriada, é como substituir unidade Olá SO com a imagem de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="7c179-282">Qualquer especialização modelo mais recente Olá, tais como as extensões, são executados.</span><span class="sxs-lookup"><span data-stu-id="7c179-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="7c179-283">Como aderir a um domínio de tooan do Azure AD de conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="7c179-284">toojoin um domínio de Azure Active Directory (Azure AD) tooan de conjunto de dimensionamento de máquina virtual, pode definir uma extensão.</span><span class="sxs-lookup"><span data-stu-id="7c179-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="7c179-285">toodefine uma extensão, utilize a propriedade de JsonADDomainExtension Olá:</span><span class="sxs-lookup"><span data-stu-id="7c179-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="7c179-286">A minha extensão de conjunto de dimensionamento da máquina virtual está a tentar tooinstall algo que requer uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="7c179-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="7c179-287">Por exemplo, "commandToExecute": "powershell.exe - ExecutionPolicy irrestrito Install-WindowsFeature-nome FS-Resource-Manager – IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="7c179-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="7c179-288">Se a extensão de conjunto de dimensionamento da máquina virtual está a tentar tooinstall algo que requer um reinício, pode utilizar a extensão do Azure Automation configuração de estado pretendido (DSC de automatização) Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="7c179-289">Se o sistema de operativo Olá for Windows Server 2012 R2, o Azure obtém na configuração de Windows Management Framework (WMF) 5.0 Olá, reinícios e, em seguida, continua com a configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="7c179-290">Como posso ativar de antimalware no meu conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="7c179-291">tooturn no antimalware no seu dimensionamento da máquina virtual definir, utilize Olá seguinte o exemplo do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7c179-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="7c179-292">Preciso de tooexecute um script personalizado que está alojado numa conta do storage privada.</span><span class="sxs-lookup"><span data-stu-id="7c179-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="7c179-293">script de Olá é executado com êxito ao armazenamento de Olá é público, mas quando tento toouse uma assinatura de acesso partilhado (SAS), falhar.</span><span class="sxs-lookup"><span data-stu-id="7c179-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="7c179-294">Esta mensagem é apresentada: "Em falta os parâmetros obrigatórios para a assinatura de acesso partilhado válida".</span><span class="sxs-lookup"><span data-stu-id="7c179-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="7c179-295">Ligação + SAS funciona bem a partir do meu local do browser.</span><span class="sxs-lookup"><span data-stu-id="7c179-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="7c179-296">tooexecute um script personalizado que está alojado numa conta do storage privada, configurar definições protegidas com a chave de conta do storage Olá e nome.</span><span class="sxs-lookup"><span data-stu-id="7c179-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="7c179-297">Para obter mais informações, consulte [extensão de Script personalizado para Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="7c179-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="7c179-298">Redes</span><span class="sxs-lookup"><span data-stu-id="7c179-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="7c179-299">É possível tooassign do conjunto de dimensionamento de tooa um grupo de segurança de rede (NSG), para que será aplicada tooall Olá NICs de VM no conjunto de Olá?</span><span class="sxs-lookup"><span data-stu-id="7c179-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="7c179-300">Sim.</span><span class="sxs-lookup"><span data-stu-id="7c179-300">Yes.</span></span> <span data-ttu-id="7c179-301">Podem ser aplicado um grupo de segurança de rede diretamente o conjunto de dimensionamento de tooa por que o referenciam na secção de networkInterfaceConfigurations Olá do perfil de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="7c179-302">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7c179-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="7c179-303">Como posso fazer uma alternância de VIP para conjuntos de dimensionamento de máquina virtual no Olá mesma subscrição e região mesmo?</span><span class="sxs-lookup"><span data-stu-id="7c179-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="7c179-304">Se tiver dois virtual conjuntos de dimensionamento de máquina com frente-ends de Balanceador de carga do Azure e, se encontram num Olá mesma subscrição e região, foi possível anular a atribuição de endereços IP públicos Olá de cada um deles e atribuir toohello outro.</span><span class="sxs-lookup"><span data-stu-id="7c179-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="7c179-305">Consulte [alternância de VIP: implementação de Blue verde no Gestor de recursos do Azure](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) por exemplo.</span><span class="sxs-lookup"><span data-stu-id="7c179-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="7c179-306">Isto implica um atraso como Olá recursos sejam desalocada/atribuído ao nível de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="7c179-307">Uma opção mais rápida é toouse Gateway de aplicação do Azure com dois conjuntos de back-end e uma regra de encaminhamento.</span><span class="sxs-lookup"><span data-stu-id="7c179-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="7c179-308">Em alternativa, pode alojar a aplicação com [App service do Azure](https://azure.microsoft.com/en-us/services/app-service/) que fornece suporte para a mudança rápida de entre as ranhuras de teste e produção.</span><span class="sxs-lookup"><span data-stu-id="7c179-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="7c179-309">Como posso especificar um intervalo de privada toouse de endereços IP para a atribuição de endereço IP privada estática?</span><span class="sxs-lookup"><span data-stu-id="7c179-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="7c179-310">Endereços IP são selecionados de sub-rede que especificar.</span><span class="sxs-lookup"><span data-stu-id="7c179-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="7c179-311">método de alocação de Olá de endereços IP de conjunto de dimensionamento de máquina virtual está sempre "dinâmico", mas que não significa que podem alterar estes endereços IP.</span><span class="sxs-lookup"><span data-stu-id="7c179-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="7c179-312">Neste caso, "dinâmica" apenas significa que não especifique o endereço IP Olá num pedido PUT.</span><span class="sxs-lookup"><span data-stu-id="7c179-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="7c179-313">Especifique Olá estático definida através de sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="7c179-314">Como posso implementar uma máquina virtual escala conjunto tooan existente rede virtual do Azure?</span><span class="sxs-lookup"><span data-stu-id="7c179-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="7c179-315">toodeploy um dimensionamento da máquina virtual definir tooan de rede virtual do Azure existente, consulte [implementar uma máquina virtual escala conjunto tooan rede virtual existente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="7c179-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="7c179-316">Como adicionar o endereço IP Olá conjunto de Olá toohello saída de um modelo da VM primeiro num dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="7c179-317">endereço IP Olá tooadd de Olá primeira VM na saída de toohello do conjunto de dimensionamento máquina virtual de um modelo, consulte [ARM: IPs privados obter VMSS](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="7c179-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="7c179-318">Pode utilizar conjuntos de dimensionamento com acelerados da rede?</span><span class="sxs-lookup"><span data-stu-id="7c179-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="7c179-319">Sim.</span><span class="sxs-lookup"><span data-stu-id="7c179-319">Yes.</span></span> <span data-ttu-id="7c179-320">toouse acelerado funcionamento em rede, configurar enableAcceleratedNetworking tootrue no seu dimensionamento as definições de networkInterfaceConfigurations do conjunto.</span><span class="sxs-lookup"><span data-stu-id="7c179-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="7c179-321">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="7c179-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="7c179-322">Como pode configurar os servidores DNS Olá utilizados por um conjunto de dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="7c179-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="7c179-323">toocreate do conjunto de dimensionamento uma VM com uma configuração de DNS personalizada, adicione que uma escala de toohello do pacote JSON dnsSettings definir networkInterfaceConfigurations secção.</span><span class="sxs-lookup"><span data-stu-id="7c179-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="7c179-324">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7c179-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="7c179-325">Como configurar a um tooassign de conjunto de dimensionamento um tooeach de endereço IP público VM?</span><span class="sxs-lookup"><span data-stu-id="7c179-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="7c179-326">toocreate conjunto de um dimensionamento VM que atribui uma tooeach de endereço IP público VM, certifique-se versão Olá API de Olá Microsoft.Compute/virtualMAchineScaleSets recursos 2017-03-30 e adicionar um _publicipaddressconfiguration_ pacote JSON conjunto de dimensionamento de toohello ipConfigurations secção.</span><span class="sxs-lookup"><span data-stu-id="7c179-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="7c179-327">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7c179-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="7c179-328">Pode configurar um toowork de conjunto de dimensionamento com vários Gateways de aplicação?</span><span class="sxs-lookup"><span data-stu-id="7c179-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="7c179-329">Sim.</span><span class="sxs-lookup"><span data-stu-id="7c179-329">Yes.</span></span> <span data-ttu-id="7c179-330">Pode adicionar Olá id de recurso para vários toohello de conjuntos de endereços do Gateway de aplicação back-end _applicationGatewayBackendAddressPools_ lista no Olá _ipConfigurations_ secção do seu conjunto de dimensionamento perfil de rede.</span><span class="sxs-lookup"><span data-stu-id="7c179-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="7c179-331">Escala</span><span class="sxs-lookup"><span data-stu-id="7c179-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="7c179-332">No caso de que iria criar um conjunto com menos de duas VMs de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="7c179-333">Uma razão toocreate um máquina virtual conjunto de dimensionamento com menos de duas VMs seriam definidas toouse Olá elástico as propriedades de um dimensionamento da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c179-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="7c179-334">Por exemplo, pode implementar um conjunto de dimensionamento de máquina virtual com zero VMs toodefine a infraestrutura sem pagar VM a executar os custos.</span><span class="sxs-lookup"><span data-stu-id="7c179-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="7c179-335">Em seguida, quando estiver pronto toodeploy VMs, aumente Olá "capacidade" de dimensionamento de máquina virtual de Olá conjunto contagem de instâncias de produção de toohello.</span><span class="sxs-lookup"><span data-stu-id="7c179-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="7c179-336">Outro motivo, que poderá criar um conjunto com menos de duas VMs de dimensionamento de máquina virtual é se está preocupados com menos com disponibilidade de sessão através de um conjunto de disponibilidade com VMs discretas.</span><span class="sxs-lookup"><span data-stu-id="7c179-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="7c179-337">Conjuntos de dimensionamento de máquina virtual dão-lhe um toowork de forma com unidades de computação undifferentiated são fungible.</span><span class="sxs-lookup"><span data-stu-id="7c179-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="7c179-338">Este uniformidade da é um principal diferenciador para conjuntos de dimensionamento de máquina virtual em comparação com conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="7c179-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="7c179-339">Muitas cargas de trabalho sem monitorização de estado não controlam unidades individuais.</span><span class="sxs-lookup"><span data-stu-id="7c179-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="7c179-340">Se ignora a carga de trabalho Olá, pode reduzir verticalmente a unidade de computação tooone e, em seguida, aumentar verticalmente toomany quando aumenta a carga de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="7c179-341">Como alterar o número de Olá de VMs num conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="7c179-342">número de Olá toochange de VMs no conjunto de dimensionamento de máquina virtual, consulte [alterar a contagem de instâncias de Olá de um conjunto de dimensionamento de máquina virtual](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="7c179-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="7c179-343">Como posso definir alertas personalizados para quando determinados limiares são atingidos?</span><span class="sxs-lookup"><span data-stu-id="7c179-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="7c179-344">Tem alguma flexibilidade na forma como lidar com alertas de limiares especificados.</span><span class="sxs-lookup"><span data-stu-id="7c179-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="7c179-345">Por exemplo, pode definir webhooks personalizado.</span><span class="sxs-lookup"><span data-stu-id="7c179-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="7c179-346">Olá seguinte o exemplo de webhook é a partir de um modelo do Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="7c179-346">hello following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="7c179-347">Neste exemplo, um alerta passa tooPagerduty.com quando for atingido um limiar.</span><span class="sxs-lookup"><span data-stu-id="7c179-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="7c179-348">Aplicação de patches e operações</span><span class="sxs-lookup"><span data-stu-id="7c179-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="7c179-349">Como posso criar uma escala definida num grupo de recursos existente?</span><span class="sxs-lookup"><span data-stu-id="7c179-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="7c179-350">Criar conjuntos de dimensionamento num recurso existente grupo ainda não é possível a partir do portal do Azure de Olá, mas pode especificar um grupo de recursos existente quando implementar uma escala definido a partir de um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c179-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="7c179-351">Também pode especificar um grupo de recursos existente ao criar um conjunto utilizando o Azure PowerShell ou a CLI de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="7c179-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="7c179-352">Mover que grupo de recursos de tooanother do conjunto de um dimensionamento?</span><span class="sxs-lookup"><span data-stu-id="7c179-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="7c179-353">Sim, pode mover o dimensionamento conjunto recursos tooa nova subscrição ou grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7c179-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="7c179-354">Como atualizar tooI a minha máquina virtual conjunto de dimensionamento de tooa nova imagem?</span><span class="sxs-lookup"><span data-stu-id="7c179-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="7c179-355">Como gerir a aplicação de patches?</span><span class="sxs-lookup"><span data-stu-id="7c179-355">How do I manage patching?</span></span>

<span data-ttu-id="7c179-356">tooupdate o dimensionamento da máquina virtual definir tooa nova imagem e a aplicação de patches toomanage, consulte [Atualize um conjunto de dimensionamento de máquina virtual](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="7c179-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="7c179-357">Pode utilizar tooreset de operação de recriação de imagem de Olá uma VM sem alterar a imagem de Olá?</span><span class="sxs-lookup"><span data-stu-id="7c179-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="7c179-358">(Ou seja, posso pretender repor uma VM toofactory definições em vez de tooa nova imagem.)</span><span class="sxs-lookup"><span data-stu-id="7c179-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="7c179-359">Sim, pode utilizar tooreset de operação de recriação de imagem de Olá uma VM, sem alterar a imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="7c179-360">No entanto, se o conjunto de dimensionamento da máquina virtual faz referência a uma imagem de plataforma com `version = latest`, a VM pode atualizar tooa imagem de SO posterior ao chamar `reimage`.</span><span class="sxs-lookup"><span data-stu-id="7c179-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="7c179-361">Para obter mais informações, consulte [gerir todas as VMs num conjunto de dimensionamento de máquina virtual](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="7c179-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="7c179-362">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="7c179-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="7c179-363">Como ativar diagnósticos de arranque?</span><span class="sxs-lookup"><span data-stu-id="7c179-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="7c179-364">tooturn diagnósticos de arranque, em primeiro lugar, crie uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7c179-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="7c179-365">Em seguida, colocar este bloco JSON no seu conjunto de dimensionamento de máquina virtual **virtualMachineProfile**e atualizar o conjunto de dimensionamento de máquina virtual de Olá:</span><span class="sxs-lookup"><span data-stu-id="7c179-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="7c179-366">Quando é criada uma nova VM, Olá propriedade InstanceView Olá VM mostra detalhes de Olá para captura de ecrã Olá e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="7c179-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="7c179-367">Eis um exemplo:</span><span class="sxs-lookup"><span data-stu-id="7c179-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="7c179-368">Propriedades da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7c179-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="7c179-369">Como posso obter informações sobre propriedades para cada VM sem fazer chamadas de várias?</span><span class="sxs-lookup"><span data-stu-id="7c179-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="7c179-370">Por exemplo, como seria posso obter o domínio de falhas de Olá para cada um dos Olá 100 VMs no meu conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="7c179-371">informações de propriedade tooget para cada VM sem fazer chamadas de várias, pode chamar `ListVMInstanceViews` efetuando uma API REST `GET` no Olá seguir o URI do recurso:</span><span class="sxs-lookup"><span data-stu-id="7c179-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="7c179-372">/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname} < subscription_id > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtualMachines? $expand = instanceView & $select = instanceView</span><span class="sxs-lookup"><span data-stu-id="7c179-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="7c179-373">Pode posso passar os argumentos de outra extensão toodifferent VMs num conjunto de dimensionamento de máquina virtual?</span><span class="sxs-lookup"><span data-stu-id="7c179-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="7c179-374">Não, não poder passar os argumentos de outra extensão toodifferent VMs num conjunto de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c179-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="7c179-375">No entanto, as extensões podem agir com base nas propriedades de exclusivo Olá de Olá VM que estão em execução no, tal como no nome da máquina de Olá.</span><span class="sxs-lookup"><span data-stu-id="7c179-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="7c179-376">Extensões também podem consultar os metadados de instância no http://169.254.169.254 tooget mais informações sobre Olá VM.</span><span class="sxs-lookup"><span data-stu-id="7c179-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="7c179-377">Por que motivo existem intervalos entre a minha nomes de máquina VM de conjunto de dimensionamento de máquina virtual e os IDs de VM?</span><span class="sxs-lookup"><span data-stu-id="7c179-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="7c179-378">Por exemplo: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="7c179-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="7c179-379">Existem intervalos entre os nomes de máquina VM de conjunto de dimensionamento de máquina virtual e os IDs de VM, porque o conjunto de dimensionamento da máquina virtual **bandeira** propriedade está definida valor predefinido toohello **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="7c179-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="7c179-380">Se provocam um aprovisionamento estiver definido demasiado**verdadeiro**, mais VMs que pediu são criados.</span><span class="sxs-lookup"><span data-stu-id="7c179-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="7c179-381">VMs Extras, em seguida, são eliminadas.</span><span class="sxs-lookup"><span data-stu-id="7c179-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="7c179-382">Neste caso, obtenha a implementação de uma maior fiabilidade, mas a despesa Olá de atribuição de nomes contíguo e contíguo tradução de endereços de rede (NAT) regras.</span><span class="sxs-lookup"><span data-stu-id="7c179-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="7c179-383">Pode definir esta propriedade demasiado**falso**.</span><span class="sxs-lookup"><span data-stu-id="7c179-383">You can set this property too**false**.</span></span> <span data-ttu-id="7c179-384">Para conjuntos de dimensionamento pequeno máquina virtual, isto não afeta significativamente fiabilidade de implementação.</span><span class="sxs-lookup"><span data-stu-id="7c179-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="7c179-385">Qual é Olá diferença entre a eliminação de uma VM com um conjunto de dimensionamento de máquina virtual e Desalocação Olá VM?</span><span class="sxs-lookup"><span data-stu-id="7c179-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="7c179-386">Quando devo escolher um através de outro Olá?</span><span class="sxs-lookup"><span data-stu-id="7c179-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="7c179-387">Olá principal diferença entre a eliminação de uma VM com um conjunto de dimensionamento de máquina virtual e Desalocação Olá VM é que `deallocate` não elimina Olá de discos rígidos virtuais (VHDs).</span><span class="sxs-lookup"><span data-stu-id="7c179-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="7c179-388">Existem custos de armazenamento associados a execução `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="7c179-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="7c179-389">Pode utilizar um ou Olá outra para uma das Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="7c179-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="7c179-390">Pretende toostop pagar os custos de computação, mas pretende que o estado do disco Olá tookeep de Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="7c179-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="7c179-391">Pretende que um conjunto de VMs de toostart mais rapidamente do que foi ampliar um conjunto de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c179-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="7c179-392">Cenário de toothis relacionados, pode ter criado o seu motor de dimensionamento automático e pretender uma escala de ponto a ponto mais rápida.</span><span class="sxs-lookup"><span data-stu-id="7c179-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="7c179-393">Tem um conjunto de dimensionamento de máquina virtual é unevenly distribuído por domínios de falhas ou domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="7c179-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="7c179-394">Isto poderá ser porque tem VMs eliminado seletivamente ou porque as VMs foram eliminadas após provocam um aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="7c179-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="7c179-395">Executar `stop deallocate` seguido `start` na máquina virtual de Olá uniformemente conjunto de dimensionamento distribui Olá VMs domínios de falhas ou domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="7c179-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

