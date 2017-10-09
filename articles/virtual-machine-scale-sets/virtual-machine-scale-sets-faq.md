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
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Perguntas mais frequentes de conjuntos de dimensionamento de máquina virtual do Azure

Obtenha respostas define toofrequently mais frequentes sobre o sobre o dimensionamento da máquina virtual no Azure.

## <a name="autoscale"></a>Dimensionamento Automático

### <a name="what-are-best-practices-for-azure-autoscale"></a>Quais são as melhores práticas para o dimensionamento automático do Azure?

Para melhores práticas para o dimensionamento automático, consulte [melhores práticas para máquinas virtuais de dimensionamento automático](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Onde posso encontrar os nomes de métricos de dimensionamento automático que utiliza a métrica do anfitrião?

Para nomes de métricos de dimensionamento automático que utiliza a métrica baseada no anfitrião, consulte [suportado métricas com a monitorização do Azure](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Existem os exemplos de dimensionamento automático com base num comprimento de fila e o tópico do Service Bus do Azure?

Sim. Para obter exemplos de dimensionamento automático com base num comprimento de fila e o tópico do Service Bus do Azure, consulte [métricas comuns de dimensionamento automático de Monitor de Azure](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Para uma fila de barramento de serviço, utilize Olá JSON a seguir:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Para uma fila de armazenamento, utilize Olá JSON a seguir:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Substitua os valores de exemplo pelo seu recurso Uniform Resource Identifiers (URIs).


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Deve posso dimensionamento automático utilizando as métricas baseada no anfitrião ou uma extensão de diagnóstico?

Pode criar uma definição de dimensionamento automático num métricas de nível do anfitrião VM toouse ou métricas de com base no SO convidado.

Para obter uma lista das métricas suportadas, consulte [métricas comuns de dimensionamento automático de Monitor de Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Para obter um exemplo completo para conjuntos de dimensionamento de máquina virtual, consulte [configuração avançada de dimensionamento automático através de modelos do Resource Manager para conjuntos de dimensionamento de máquina virtual](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

exemplo de Olá utiliza a métrica de CPU Olá ao nível do anfitrião e uma métrica de contagem de mensagens.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Como definir a regras de alertas sobre um conjunto de dimensionamento de máquina virtual

Pode criar alertas nas métricas para conjuntos de dimensionamento de máquina virtual através do PowerShell ou a CLI do Azure. Para obter mais informações, consulte [Azure Monitor PowerShell rápido iniciar amostras](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) e [CLI de várias plataformas de Monitor de Azure rápido iniciar amostras](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Olá TargetResourceId do conjunto de dimensionamento de máquina virtual de Olá tem o seguinte aspeto: 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/Providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

Pode escolher qualquer contador de desempenho da VM como tooset métrica Olá um alerta para. Para obter mais informações, consulte [métricas de SO convidado para VMs do Windows baseados no Resource Manager](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) e [métricas de SO convidado para VMs com Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) no Olá [métricas comuns de dimensionamento automático Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)artigo.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>Como configurar Dimensionar automaticamente conforme um conjunto utilizando o PowerShell de dimensionamento de máquina virtual?

tooset cópias de segurança de dimensionamento automático numa escala de máquina virtual definido através do PowerShell, consulte a mensagem de blogue de Olá [como conjunto de dimensionamento automático de tooadd tooan dimensionamento de máquina virtual do Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Certificados

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Como posso enviar em segurança toohello um certificado VM? Como aprovisionar um toorun de conjunto de dimensionamento de máquina virtual um Web site onde hello SSL para o Web site Olá vem incluído em segurança de uma configuração de certificado? (Olá comuns rotação a operação de certificado deverá ser quase Olá mesmo que uma operação de atualização da configuração.) Tem um exemplo de como toodo Isto? 

toosecurely são enviados toohello um certificado VM, pode instalar um certificado de cliente diretamente para um arquivo de certificados do Windows do Cofre de chaves do cliente Olá.

Utilize Olá JSON a seguir:

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

código de Olá suporta o Windows e Linux.

Para obter mais informações, consulte [criar ou atualizar um dimensionamento da máquina virtual definir](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Exemplo de certificado autoassinado

1.  Crie um certificado autoassinado no Cofre de chaves.

    Utilize Olá os seguintes comandos do PowerShell:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Este oferece comando Olá entrada de modelo do Azure Resource Manager Olá.

    Para obter um exemplo de como toocreate um certificado autoassinado no Cofre de chaves, consulte o artigo [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Alterar o modelo do Resource Manager Olá.

    Adicionar esta propriedade demasiado**virtualMachineProfile**, como parte da Olá recursos de conjunto de dimensionamento de máquina virtual:

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
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Pode especificar um toouse do par de chaves SSH para a autenticação SSH com uma escala de máquina virtual Linux definido a partir de um modelo do Resource Manager?  

Sim. Olá REST API para **osProfile** é semelhante API REST de VM padrão toohello. 

Incluir **osProfile** no seu modelo:

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
 
Este bloco JSON é utilizado na [modelo de início rápido do Olá 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Olá perfil de SO também é utilizado em [Olá grelayhost.json GitHub rápido iniciar modelo](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Para obter mais informações, consulte [criar ou atualizar um dimensionamento da máquina virtual definir](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Como posso remover certificados preteridos? 

tooremove preterido certificados, remover certificado antigo de Olá Olá cofre certificados na lista. Deixe todos os certificados de Olá que pretende que tooremain no seu computador na lista de Olá. Isto não remove o certificado de Olá de todas as suas VMs. Também não adiciona Olá certificado toonew VMs que são criadas no conjunto de dimensionamento de máquina virtual de Olá. 

certificado Olá tooremove VMs existentes, escrever um script personalizado certificados de Olá extensão toomanually remover do seu arquivo de certificados.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Como posso inserir uma chave pública SSH na camada SSH do conjunto de dimensionamento do Olá máquina virtual durante o aprovisionamento Pretende toostore Olá SSH públicos valores de chave no Cofre de chaves do Azure e, em seguida, utilizá-los no meu modelo do Resource Manager.

Se está a fornecer Olá VMs apenas com uma chave SSH pública, não precisa de tooput Olá as chaves públicas no Cofre de chaves. As chaves públicas não são secretas.
 
Pode fornecer as chaves públicas SSH em texto simples quando criar uma VM com Linux:

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
 
nome do elemento linuxConfiguration | Necessário | Tipo | Descrição
--- | --- | --- | --- |  ---
SSH | Não | Coleção | Especifica a configuração da chave SSH Olá para um SO Linux
Caminho | Sim | Cadeia | Especifica o caminho do ficheiro Olá Linux em que as chaves SSH Olá ou o certificado deve estar localizado
keyData | Sim | Cadeia | Especifica uma chave pública de SSH com codificação base64

Por exemplo, consulte [modelo de início rápido do Olá 101-vm-sshkey GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>Quando executar `Update-AzureRmVmss` após a adição de mais de um certificado de Olá mesma chave de cofre, vejo Olá seguintes mensagens:
 
>Update-AzureRmVmss: Segredo de lista contém instâncias repetidas de /subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname} < minha subscrição-id > / resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, que não é permitida.
 
Isto pode acontecer se tentar toore-adicionar Olá mesmo cofre em vez de utilizar um novo certificado de cofre para o Cofre de origem existente Olá. Olá `Add-AzureRmVmssSecret` comando não funcionar corretamente, se estiver a adicionar segredos adicionais.
 
tooadd mais segredos de Olá mesmo Cofre de chaves, atualização Olá $vmss.properties.osProfile.secrets[0].vaultCertificates lista.
 
Para obter Olá esperado estrutura de entrada, consulte [criar ou atualizar uma máquina virtual definir](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Encontrar o segredo de Olá no objeto conjunto de dimensionamento de máquina virtual de Olá que se encontra no Cofre de chaves Olá. Em seguida, adicionar a sua lista de toohello de referência (Olá URL e nome de arquivo secreta Olá) de certificado associada Olá cofre.

> [!NOTE] 
> Atualmente, não é possível remover certificados dos VMs utilizando a API de conjunto de dimensionamento de máquina virtual de Olá.
>

Novas VMs não terão o certificado antigo Olá. No entanto, as VMs que têm o certificado de Olá e que já são implementadas terão o certificado antigo Olá.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>Pode emitir conjunto sem fornecer a palavra-passe de Olá, quando o certificado de Olá está no arquivo secreta Olá de dimensionamento de máquina virtual de toohello de certificados?

Não é necessário toohard código palavras-passe em scripts. Pode obter dinamicamente as palavras-passe com permissões de Olá utilizar script de implementação de Olá toorun. Se tiver um script que se move um certificado a partir do Cofre de chaves de arquivo secreta Olá, Olá arquivo secreto `get certificate` comando também produz Olá palavra-passe do ficheiro. pfx Olá.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Como Olá segredos virtualMachineProfile.osProfile para um dimensionamento da máquina virtual definir a propriedade de trabalho? Por que motivo precisa valor de sourceVault Olá quando tenho toospecify Olá URI absoluto de um certificado utilizando Olá certificateUrl propriedade? 

Uma referência de certificado de gestão remota do Windows (WinRM) deve estar presente no Olá propriedade segredos Olá perfil do SO. 

objetivo Olá que indica que o Cofre de origem Olá é políticas (ACL) de lista de controlo de acesso de tooenforce que existem no modelo de serviço de nuvem do Azure de um utilizador. Se o Cofre de origem Olá não está especificado, os utilizadores que não dispõe de permissões toodeploy ou acesso segredos tooa Cofre de chaves será toothrough capaz de um fornecedor de recursos de computação (CRP). As ACLs existem mesmo para recursos que não existem.

Se fornecer um ID de Cofre de origem incorreto, mas um URL do Cofre de chaves válida, é comunicado um erro ao consultar operação Olá.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Se adicionar tooan segredos existente conjunto de dimensionamento da máquina virtual, são segredos Olá injetados para VMs existentes, ou apenas para novos? 

Certificados são adicionados tooall as suas VMs, mesmo pré-existentes aqueles. Se o dimensionamento da máquina virtual definir a propriedade de upgradePolicy estiver definido demasiado**manual**, Olá é adicionar certificado toohello VM quando efetuar uma atualização manual Olá VM.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Onde colocar o certificados para VMs com Linux?

toolearn como toodeploy certificados para VMs com Linux, consulte [implementar tooVMs de certificados de um cofre de chaves gerida pelo cliente](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Como adicionar um novo cofre certificado tooa novo objeto certificado?

tooadd um cofre certificado tooan segredo existente, consulte Olá seguinte o exemplo do PowerShell. Utilize apenas um objeto secreto.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>O que acontece toocertificates recriar uma VM?

Se criar nova imagem de uma VM, os certificados são eliminados. Disco do SO todo Olá eliminações de reprocessamento de imagem. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>O que acontece se eliminar um certificado a partir do Cofre de chaves Olá?

Se segredo Olá é eliminado do Cofre de chaves Olá e, em seguida, execute `stop deallocate` para todas as suas VMs e, em seguida, iniciá-los novamente, irá ocorrer uma falha. Falha de Olá ocorre porque Olá CRP necessita segredos de Olá tooretrieve do Cofre de chaves Olá, mas não pode ser. Neste cenário, pode eliminar certificados Olá do modelo de conjunto de dimensionamento de máquina virtual de Olá. 

componente de CRP de Olá não persiste segredos do cliente. Se executar `stop deallocate` para todas as VMs no conjunto de dimensionamento de máquina virtual de Olá, cache Olá é eliminado. Neste cenário, segredos são obtidos a partir do Cofre de chaves Olá.

Não ocorrer este problema durante a ampliação porque não existe uma cópia em cache do segredo Olá no Service Fabric do Azure (no modelo de recursos de infraestrutura único inquilino Olá).
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Por que razão tem a localização exata de Olá toospecify para o URL de certificado Olá (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), conforme indicado na [cenários de segurança de cluster do Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Olá documentação do Cofre de chaves do Azure indica que Olá que obter API de REST do segredo deverá devolver a versão mais recente do Olá do segredo Olá se versão Olá não for especificado.
 
Método | URL
--- | ---
INTRODUÇÃO | https://mykeyvault.Vault.Azure.NET/Secrets/ {nome-segredo} / {segredo-version}? api-version = {api-version}

Substitua {*segredo-name*} com o nome de Olá e substitua {*segredo versão*} com a versão de Olá do segredo Olá pretende tooretrieve. versão secreta Olá poderão ser excluído. Nesse caso, a versão atual do Olá é obtido.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Por que razão tem versão de certificado de Olá toospecify quando utilizar o Cofre de chaves?

objetivo Olá versão de certificado de Olá requisito toospecify Olá Cofre de chaves é toomake-limpar toohello utilizador o certificado for implementado nas respetivas VMs.

Se criar uma VM e, em seguida, atualize o seu segredo no Cofre de chaves Olá, certificado novo Olá não é transferido tooyour VMs. Mas as suas VMs aparecem tooreference e novas VMs obtêm segredo Olá de novo. tooavoid, são necessário tooreference uma versão secreta.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>A minha equipa funciona com vários certificados que são distribuídos toous como chaves públicas. cer. O que é Olá abordagem para implementar o conjunto de dimensionamento da máquina virtual estes certificados tooa recomendada?

toodeploy. cer as chaves públicas tooa escala conjunto da máquina virtual, pode gerar um ficheiro. pfx que contém apenas os ficheiros. cer. toodo, utilize `X509ContentType = Pfx`. Por exemplo, carregue o ficheiro. cer de Olá como um objeto de x509Certificate2 em c# ou PowerShell e, em seguida, chame o método de Olá. 

Para obter mais informações, consulte [X509Certificate.Export método (X509ContentType, cadeia)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Não vejo uma opção para os utilizadores toopass em certificados como cadeias de base64. A maioria dos fornecedores de recursos tem esta opção.

tooemulate transmitir num certificado como uma cadeia base64, pode extrair Olá mais recente com versão do URL num modelo do Resource Manager. Inclua Olá propriedade JSON no seu modelo do Resource Manager a seguir:

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>Alguns têm certificados de toowrap em objetos JSON no cofres de chaves?

Em conjuntos de dimensionamento de máquina virtual e VMs, certificados tem de ser moldados numa objetos JSON. 

Também é suportada a Olá o tipo de conteúdo application/x-pkcs12. Para obter instruções sobre como utilizar o application/x-pkcs12, consulte [os certificados PFX no Cofre de chaves do Azure](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
Atualmente não suportamos. cer ficheiros. ficheiros. cer toouse, exportá-las em contentores. pfx.



## <a name="compliance"></a>Conformidade

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Estão em conformidade de PCI define o dimensionamento da máquina virtual?

Conjuntos de dimensionamento de máquina virtual são uma camada de API dinâmico sobreposta Olá CRP. Ambos os componentes fazem parte da plataforma de computação de Olá no Olá árvore de serviço do Azure.

Numa perspetiva de conformidade, conjuntos de dimensionamento de máquina virtual são uma parte fundamental da plataforma de computação do Azure Olá. Estes partilham uma equipa, ferramentas, processos, a metodologia de implementação, controlos de segurança, just-in-time (JIT) compilação, monitorização, alertas e assim sucessivamente, com CRP Olá próprio. Conjuntos de dimensionamento de máquina virtual são da indústria de cartão de pagamento (PCI)-conformidade porque Olá CRP faz parte de atestado de PCI dados segurança Standard (DSS) atual Olá.

Para obter mais informações, consulte [Olá Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>Extensões

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Como posso eliminar uma extensão de conjunto de dimensionamento de máquina virtual?

toodelete um dimensionamento da máquina virtual Definir extensão, Olá utilize seguinte o exemplo do PowerShell:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
Pode encontrar o valor extensionName Olá `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Existe que um dimensionamento da máquina virtual definir exemplo de modelo que se integra com o Operations Management Suite?

Para um dimensionamento da máquina virtual definido exemplo de modelo que se integra com o Operations Management Suite, consulte o segundo exemplo de Olá na [implementar um cluster do Service Fabric do Azure e ative a monitorização utilizando a análise de registos](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Extensões parecem toorun em paralelo em conjuntos de dimensionamento de máquina virtual. Isto faz com que a minha toofail de extensão de script personalizado. O que posso fazer toofix Isto?

toolearn sobre a sequenciação de extensão em conjuntos de dimensionamento de máquina virtual, consulte [sequenciação extensão em conjuntos de dimensionamento de máquina virtual do Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Como redefinir as palavras-passe de Olá para VMs no meu conjunto de dimensionamento de máquina virtual?

tooreset Olá palavra-passe para as VMs no seu dimensionamento de máquina virtual definido, utilização de extensões de acesso VM. 

Utilize Olá seguinte o exemplo do PowerShell:

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
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>Como adicionar uma extensão tooall VMs a minha conjunto de dimensionamento de máquina virtual?

Se a política de atualização estiver definida demasiado**automática**, voltar a implementar o modelo de Olá com novas propriedades de extensão Olá atualiza todas as VMs.

Se a política de atualização estiver definida demasiado**manual**, primeiro atualizar extensão Olá e, em seguida, atualizar manualmente todas as instâncias nas suas VMs.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Se forem atualizadas extensões Olá associadas um conjunto de dimensionamento de máquina virtual existente, existentes VMs afetadas? (Ou seja, será Olá VMs *não* modelo de conjunto de dimensionamento de máquina virtual Olá correspondência?) Ou são ignorados? Quando um computador existente é healed de serviço ou recriado, são Olá scripts que estão atualmente configuradas no conjunto de dimensionamento de máquina virtual de Olá executado ou são scripts de Olá que foram configuradas quando Olá que VM foi criada pela primeira vez utilizado?

Se definir a definição da extensão Olá no dimensionamento de máquina virtual de Olá é atualizar o modelo e Olá upgradePolicy for definida demasiado**automática**, atualiza Olá VMs. Se Olá upgradePolicy for definida demasiado**manual**, extensões sinalizadas como não corresponde ao modelo de Olá. 

Se uma VM existente healed de serviço, é apresentada como um reinício e extensões de Olá não são novamente executadas. Se é recriada, é como substituir unidade Olá SO com a imagem de origem Olá. Qualquer especialização modelo mais recente Olá, tais como as extensões, são executados.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Como aderir a um domínio de tooan do Azure AD de conjunto de dimensionamento de máquina virtual?

toojoin um domínio de Azure Active Directory (Azure AD) tooan de conjunto de dimensionamento de máquina virtual, pode definir uma extensão. 

toodefine uma extensão, utilize a propriedade de JsonADDomainExtension Olá:

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
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>A minha extensão de conjunto de dimensionamento da máquina virtual está a tentar tooinstall algo que requer uma reinicialização. Por exemplo, "commandToExecute": "powershell.exe - ExecutionPolicy irrestrito Install-WindowsFeature-nome FS-Resource-Manager – IncludeManagementTools"

Se a extensão de conjunto de dimensionamento da máquina virtual está a tentar tooinstall algo que requer um reinício, pode utilizar a extensão do Azure Automation configuração de estado pretendido (DSC de automatização) Olá. Se o sistema de operativo Olá for Windows Server 2012 R2, o Azure obtém na configuração de Windows Management Framework (WMF) 5.0 Olá, reinícios e, em seguida, continua com a configuração de Olá. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>Como posso ativar de antimalware no meu conjunto de dimensionamento de máquina virtual?

tooturn no antimalware no seu dimensionamento da máquina virtual definir, utilize Olá seguinte o exemplo do PowerShell:

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

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Preciso de tooexecute um script personalizado que está alojado numa conta do storage privada. script de Olá é executado com êxito ao armazenamento de Olá é público, mas quando tento toouse uma assinatura de acesso partilhado (SAS), falhar. Esta mensagem é apresentada: "Em falta os parâmetros obrigatórios para a assinatura de acesso partilhado válida". Ligação + SAS funciona bem a partir do meu local do browser.

tooexecute um script personalizado que está alojado numa conta do storage privada, configurar definições protegidas com a chave de conta do storage Olá e nome. Para obter mais informações, consulte [extensão de Script personalizado para Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Redes
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>É possível tooassign do conjunto de dimensionamento de tooa um grupo de segurança de rede (NSG), para que será aplicada tooall Olá NICs de VM no conjunto de Olá?

Sim. Podem ser aplicado um grupo de segurança de rede diretamente o conjunto de dimensionamento de tooa por que o referenciam na secção de networkInterfaceConfigurations Olá do perfil de rede Olá. Exemplo:

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

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>Como posso fazer uma alternância de VIP para conjuntos de dimensionamento de máquina virtual no Olá mesma subscrição e região mesmo?

Se tiver dois virtual conjuntos de dimensionamento de máquina com frente-ends de Balanceador de carga do Azure e, se encontram num Olá mesma subscrição e região, foi possível anular a atribuição de endereços IP públicos Olá de cada um deles e atribuir toohello outro. Consulte [alternância de VIP: implementação de Blue verde no Gestor de recursos do Azure](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) por exemplo. Isto implica um atraso como Olá recursos sejam desalocada/atribuído ao nível de rede Olá. Uma opção mais rápida é toouse Gateway de aplicação do Azure com dois conjuntos de back-end e uma regra de encaminhamento. Em alternativa, pode alojar a aplicação com [App service do Azure](https://azure.microsoft.com/en-us/services/app-service/) que fornece suporte para a mudança rápida de entre as ranhuras de teste e produção.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Como posso especificar um intervalo de privada toouse de endereços IP para a atribuição de endereço IP privada estática?

Endereços IP são selecionados de sub-rede que especificar. 

método de alocação de Olá de endereços IP de conjunto de dimensionamento de máquina virtual está sempre "dinâmico", mas que não significa que podem alterar estes endereços IP. Neste caso, "dinâmica" apenas significa que não especifique o endereço IP Olá num pedido PUT. Especifique Olá estático definida através de sub-rede Olá. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Como posso implementar uma máquina virtual escala conjunto tooan existente rede virtual do Azure? 

toodeploy um dimensionamento da máquina virtual definir tooan de rede virtual do Azure existente, consulte [implementar uma máquina virtual escala conjunto tooan rede virtual existente](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Como adicionar o endereço IP Olá conjunto de Olá toohello saída de um modelo da VM primeiro num dimensionamento de máquina virtual?

endereço IP Olá tooadd de Olá primeira VM na saída de toohello do conjunto de dimensionamento máquina virtual de um modelo, consulte [ARM: IPs privados obter VMSS](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>Pode utilizar conjuntos de dimensionamento com acelerados da rede?

Sim. toouse acelerado funcionamento em rede, configurar enableAcceleratedNetworking tootrue no seu dimensionamento as definições de networkInterfaceConfigurations do conjunto. Por exemplo,
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

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Como pode configurar os servidores DNS Olá utilizados por um conjunto de dimensionamento?

toocreate do conjunto de dimensionamento uma VM com uma configuração de DNS personalizada, adicione que uma escala de toohello do pacote JSON dnsSettings definir networkInterfaceConfigurations secção. Exemplo:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Como configurar a um tooassign de conjunto de dimensionamento um tooeach de endereço IP público VM?

toocreate conjunto de um dimensionamento VM que atribui uma tooeach de endereço IP público VM, certifique-se versão Olá API de Olá Microsoft.Compute/virtualMAchineScaleSets recursos 2017-03-30 e adicionar um _publicipaddressconfiguration_ pacote JSON conjunto de dimensionamento de toohello ipConfigurations secção. Exemplo:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>Pode configurar um toowork de conjunto de dimensionamento com vários Gateways de aplicação?

Sim. Pode adicionar Olá id de recurso para vários toohello de conjuntos de endereços do Gateway de aplicação back-end _applicationGatewayBackendAddressPools_ lista no Olá _ipConfigurations_ secção do seu conjunto de dimensionamento perfil de rede.

## <a name="scale"></a>Escala

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>No caso de que iria criar um conjunto com menos de duas VMs de dimensionamento de máquina virtual?

Uma razão toocreate um máquina virtual conjunto de dimensionamento com menos de duas VMs seriam definidas toouse Olá elástico as propriedades de um dimensionamento da máquina virtual. Por exemplo, pode implementar um conjunto de dimensionamento de máquina virtual com zero VMs toodefine a infraestrutura sem pagar VM a executar os custos. Em seguida, quando estiver pronto toodeploy VMs, aumente Olá "capacidade" de dimensionamento de máquina virtual de Olá conjunto contagem de instâncias de produção de toohello.

Outro motivo, que poderá criar um conjunto com menos de duas VMs de dimensionamento de máquina virtual é se está preocupados com menos com disponibilidade de sessão através de um conjunto de disponibilidade com VMs discretas. Conjuntos de dimensionamento de máquina virtual dão-lhe um toowork de forma com unidades de computação undifferentiated são fungible. Este uniformidade da é um principal diferenciador para conjuntos de dimensionamento de máquina virtual em comparação com conjuntos de disponibilidade. Muitas cargas de trabalho sem monitorização de estado não controlam unidades individuais. Se ignora a carga de trabalho Olá, pode reduzir verticalmente a unidade de computação tooone e, em seguida, aumentar verticalmente toomany quando aumenta a carga de trabalho Olá.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Como alterar o número de Olá de VMs num conjunto de dimensionamento de máquina virtual?

número de Olá toochange de VMs no conjunto de dimensionamento de máquina virtual, consulte [alterar a contagem de instâncias de Olá de um conjunto de dimensionamento de máquina virtual](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Como posso definir alertas personalizados para quando determinados limiares são atingidos?

Tem alguma flexibilidade na forma como lidar com alertas de limiares especificados. Por exemplo, pode definir webhooks personalizado. Olá seguinte o exemplo de webhook é a partir de um modelo do Resource Manager:

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

Neste exemplo, um alerta passa tooPagerduty.com quando for atingido um limiar.



## <a name="patching-and-operations"></a>Aplicação de patches e operações

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Como posso criar uma escala definida num grupo de recursos existente?

Criar conjuntos de dimensionamento num recurso existente grupo ainda não é possível a partir do portal do Azure de Olá, mas pode especificar um grupo de recursos existente quando implementar uma escala definido a partir de um modelo Azure Resource Manager. Também pode especificar um grupo de recursos existente ao criar um conjunto utilizando o Azure PowerShell ou a CLI de dimensionamento.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>Mover que grupo de recursos de tooanother do conjunto de um dimensionamento?

Sim, pode mover o dimensionamento conjunto recursos tooa nova subscrição ou grupo de recursos.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>Como atualizar tooI a minha máquina virtual conjunto de dimensionamento de tooa nova imagem? Como gerir a aplicação de patches?

tooupdate o dimensionamento da máquina virtual definir tooa nova imagem e a aplicação de patches toomanage, consulte [Atualize um conjunto de dimensionamento de máquina virtual](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Pode utilizar tooreset de operação de recriação de imagem de Olá uma VM sem alterar a imagem de Olá? (Ou seja, posso pretender repor uma VM toofactory definições em vez de tooa nova imagem.)

Sim, pode utilizar tooreset de operação de recriação de imagem de Olá uma VM, sem alterar a imagem de Olá. No entanto, se o conjunto de dimensionamento da máquina virtual faz referência a uma imagem de plataforma com `version = latest`, a VM pode atualizar tooa imagem de SO posterior ao chamar `reimage`.

Para obter mais informações, consulte [gerir todas as VMs num conjunto de dimensionamento de máquina virtual](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Resolução de problemas

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Como ativar diagnósticos de arranque?

tooturn diagnósticos de arranque, em primeiro lugar, crie uma conta de armazenamento. Em seguida, colocar este bloco JSON no seu conjunto de dimensionamento de máquina virtual **virtualMachineProfile**e atualizar o conjunto de dimensionamento de máquina virtual de Olá:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

Quando é criada uma nova VM, Olá propriedade InstanceView Olá VM mostra detalhes de Olá para captura de ecrã Olá e assim sucessivamente. Eis um exemplo:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Propriedades da máquina virtual

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Como posso obter informações sobre propriedades para cada VM sem fazer chamadas de várias? Por exemplo, como seria posso obter o domínio de falhas de Olá para cada um dos Olá 100 VMs no meu conjunto de dimensionamento de máquina virtual?

informações de propriedade tooget para cada VM sem fazer chamadas de várias, pode chamar `ListVMInstanceViews` efetuando uma API REST `GET` no Olá seguir o URI do recurso:

/subscriptions/{targetsubscriptionid}/resourcegroups/{targetresourcegroupname} < subscription_id > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtualMachines? $expand = instanceView & $select = instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>Pode posso passar os argumentos de outra extensão toodifferent VMs num conjunto de dimensionamento de máquina virtual?

Não, não poder passar os argumentos de outra extensão toodifferent VMs num conjunto de dimensionamento de máquina virtual. No entanto, as extensões podem agir com base nas propriedades de exclusivo Olá de Olá VM que estão em execução no, tal como no nome da máquina de Olá. Extensões também podem consultar os metadados de instância no http://169.254.169.254 tooget mais informações sobre Olá VM.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Por que motivo existem intervalos entre a minha nomes de máquina VM de conjunto de dimensionamento de máquina virtual e os IDs de VM? Por exemplo: 0, 1, 3...

Existem intervalos entre os nomes de máquina VM de conjunto de dimensionamento de máquina virtual e os IDs de VM, porque o conjunto de dimensionamento da máquina virtual **bandeira** propriedade está definida valor predefinido toohello **verdadeiro**. Se provocam um aprovisionamento estiver definido demasiado**verdadeiro**, mais VMs que pediu são criados. VMs Extras, em seguida, são eliminadas. Neste caso, obtenha a implementação de uma maior fiabilidade, mas a despesa Olá de atribuição de nomes contíguo e contíguo tradução de endereços de rede (NAT) regras. 

Pode definir esta propriedade demasiado**falso**. Para conjuntos de dimensionamento pequeno máquina virtual, isto não afeta significativamente fiabilidade de implementação.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Qual é Olá diferença entre a eliminação de uma VM com um conjunto de dimensionamento de máquina virtual e Desalocação Olá VM? Quando devo escolher um através de outro Olá?

Olá principal diferença entre a eliminação de uma VM com um conjunto de dimensionamento de máquina virtual e Desalocação Olá VM é que `deallocate` não elimina Olá de discos rígidos virtuais (VHDs). Existem custos de armazenamento associados a execução `stop deallocate`. Pode utilizar um ou Olá outra para uma das Olá seguintes motivos:

- Pretende toostop pagar os custos de computação, mas pretende que o estado do disco Olá tookeep de Olá VMs.
- Pretende que um conjunto de VMs de toostart mais rapidamente do que foi ampliar um conjunto de dimensionamento de máquina virtual.
  - Cenário de toothis relacionados, pode ter criado o seu motor de dimensionamento automático e pretender uma escala de ponto a ponto mais rápida.
- Tem um conjunto de dimensionamento de máquina virtual é unevenly distribuído por domínios de falhas ou domínios de atualização. Isto poderá ser porque tem VMs eliminado seletivamente ou porque as VMs foram eliminadas após provocam um aprovisionamento. Executar `stop deallocate` seguido `start` na máquina virtual de Olá uniformemente conjunto de dimensionamento distribui Olá VMs domínios de falhas ou domínios de atualização.

