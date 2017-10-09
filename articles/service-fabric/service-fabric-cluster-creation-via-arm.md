---
title: aaaCreate um Azure Service Fabric cluster a partir de um modelo | Microsoft Docs
description: "Este artigo descreve como tooset se um recurso de infraestrutura seguros do serviço de cluster no Azure utilizando o Azure Resource Manager, o Cofre de chaves do Azure e o Azure Active Directory (Azure AD) para autenticação de cliente."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Criar um cluster do Service Fabric com o Azure Resource Manager
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Portal do Azure](service-fabric-cluster-creation-via-portal.md)
>
>

Este guia passo a passo explica como configurar um cluster do Azure Service Fabric seguro no Azure utilizando o Gestor de recursos do Azure. Iremos reconhecer que esse artigo Olá é longo. Contudo, a menos que já estejam exaustivamente familiarizado com o conteúdo de Olá, ser toofollow se cada passo cuidadosamente.

Guia de Olá abrange Olá os seguintes procedimentos:

* Como configurar certificados de tooupload um cofre de chaves do Azure para a segurança do cluster e da aplicação
* Criar um cluster protegido no Azure utilizando o Gestor de recursos do Azure
* Autenticação de utilizadores utilizando o Azure Active Directory (Azure AD) para gestão de clusters

Um cluster seguro é um cluster que impede a operações de toomanagement de acesso não autorizado. Isto inclui a implementar, atualizar e aplicações a eliminar, serviços e dados de Olá contêm. Um cluster não seguro é um cluster que qualquer pessoa pode ligar tooat qualquer altura e efetuar operações de gestão. Embora seja possível toocreate um cluster não seguro, recomendamos vivamente que cria um cluster seguro de proposto Olá. Devido um cluster não seguro não pode ser protegido mais tarde, tem de ser criado um novo cluster.

conceito de Olá de criação de clusters seguros é hello iguais, quer sejam clusters do Linux ou do Windows. Para mais informações e do programa auxiliar de scripts para criar clusters Linux seguros consulte [criação de clusters seguros no Linux](#secure-linux-clusters).

## <a name="sign-in-tooyour-azure-account"></a>Inicie sessão no tooyour a conta do Azure
Este guia utiliza [Azure PowerShell][azure-powershell]. Quando inicia uma nova sessão do PowerShell, inicie sessão tooyour conta do Azure e selecionar a sua subscrição antes de executar os comandos do Azure.

A iniciar sessão tooyour conta do Azure:

```powershell
Login-AzureRmAccount
```

Selecione a sua subscrição:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Configurar um cofre de chaves
Esta secção explica como criar um cofre de chaves para um cluster do Service Fabric no Azure e para aplicações de Service Fabric. Para obter um guia completo tooAzure Cofre de chaves, consulte toohello [Cofre de chaves guia de introdução][key-vault-get-started].

Service Fabric utiliza toosecure de certificados x. 509 um cluster e fornece funcionalidades de segurança da aplicação. Utilize certificados de toomanage do Cofre de chaves para clusters de Service Fabric no Azure. Quando um cluster é implementado no Azure, o fornecedor de recursos do Azure de Olá que é responsável pela criação de clusters de Service Fabric obtém certificados a partir do Cofre de chaves e instala-los num cluster de Olá VMs.

Olá diagrama seguinte ilustra Olá relação entre o Cofre de chaves do Azure, um cluster do Service Fabric e fornecedor de recursos do Azure de Olá que utiliza certificados armazenados no Cofre de chaves quando cria um cluster:

![Diagrama de instalação do certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Criar um grupo de recursos
Step-by-Olá primeiro passo é toocreate um grupo de recursos especificamente para o seu Cofre de chaves. Recomendamos que colocar o Cofre de chaves Olá no seu próprio grupo de recursos. Esta ação permite-lhe remover Olá computação e armazenamento grupos de recursos, incluindo o grupo de recursos de Olá que contém o cluster do Service Fabric, sem perder as chaves e segredos. grupo de recursos de Olá que contém o seu Cofre de chaves _tem de ser Olá mesma região_ como cluster Olá que está a utilizar.

Se planear toodeploy clusters em várias regiões, sugerimos que, de nome de grupo de recursos de Olá e Cofre de chaves Olá de uma forma que indica a que região pertence.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
saída de Olá deve ter o seguinte aspeto:

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Criar um cofre de chaves no novo grupo de recursos Olá
cofre da chave Olá _tem de estar ativado para a implementação_ tooallow Olá certificados da tooget de fornecedor de recursos de computação do mesmo e instalá-lo em instâncias de máquina virtual:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

saída de Olá deve ter o seguinte aspeto:

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>Utilize um cofre de chaves

toouse um cofre de chaves, _necessário ativá-la para implementação_ tooallow Olá certificados da tooget de fornecedor de recursos de computação do mesmo e instalá-lo em nós de cluster:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>Adicionar o Cofre de chaves de tooyour de certificados

Os certificados são utilizados no Service Fabric tooprovide autenticação e encriptação toosecure diferentes aspetos de um cluster e respetivas aplicações. Para obter mais informações sobre como os certificados são utilizados no Service Fabric, consulte [cenários de segurança de cluster do Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Cluster e servidor de certificado (obrigatório)
Este certificado é necessário toosecure um cluster e impedir o acesso não autorizado tooit. Fornece segurança de cluster de duas formas:

* Autenticação do cluster: autentica o nó de nó de comunicação para a Federação de cluster. Apenas nós que podem provar a sua identidade com este certificado podem associar cluster Olá.
* Autenticação de servidor: autentica Olá cluster pontos finais tooa gestão cliente de gestão, para hello cliente de gestão sabe que está a falar com toohello real cluster. Este certificado fornece também um SSL para Olá API de gestão HTTPS e para o Service Fabric Explorer através de HTTPS.

tooserve estes fins, certificado Olá têm de cumprir os requisitos de Olá:

* certificado de Olá tem de conter uma chave privada.
* certificado de Olá tem de ser criado para a troca de chaves, que é exportável tooa ficheiro Personal Information Exchange (. pfx).
* nome do requerente do certificado Olá tem de corresponder ao domínio Olá que utilize o cluster do Service Fabric tooaccess Olá. Esta correspondência é necessário tooprovide um SSL para pontos finais de gestão do cluster Olá HTTPS e o Service Fabric Explorer. Não é possível obter um certificado SSL a partir de uma autoridade de certificação (AC) para Olá. cloudapp.azure.com domínio. Tem de obter um nome de domínio personalizado para o cluster. Quando solicitar um certificado a partir de uma AC, hello nome do requerente do certificado tem de corresponder ao nome de domínio personalizado de Olá que utilizar para o cluster.

### <a name="application-certificates-optional"></a>Certificados de aplicação (opcionais)
Qualquer número de certificados adicionais pode ser instalado num cluster por motivos de segurança da aplicação. Antes de criar o cluster, considere os cenários de segurança de aplicação Olá que requerem toobe um certificado instalado em nós de Olá, tal como:

* A encriptação e desencriptação de valores de configuração de aplicação.
* Encriptação dos dados em nós durante a replicação.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formatação certificados para utilização do fornecedor de recursos do Azure
Pode adicionar e utilizar privados ficheiros de chave (. pfx) diretamente através do seu Cofre de chaves. No entanto, o fornecedor de recursos de computação do Azure Olá requer toobe chaves armazenada num formato especial JavaScript Object Notation (JSON). formato de Olá inclui Olá arquivo. pfx como uma cadeia com codificação 64 base e Olá chave palavra-passe privada. tooaccommodate estes requisitos, Olá chaves tem de ser colocadas numa cadeia JSON e, em seguida, armazenadas como "segredos" na chave de Olá cofre.

toomake este processo mais fácil, uma [módulo do PowerShell está disponível no GitHub][service-fabric-rp-helpers]. módulo de Olá toouse, Olá a seguir:

1. Transferir o conteúdo completo de Olá do repositório de Olá para um diretório local.
2. Aceda toohello de diretório local.
2. Importe o módulo de ServiceFabricRPHelpers Olá na janela do PowerShell:

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

Olá `Invoke-AddCertToKeyVault` comando neste módulo PowerShell automaticamente formatos uma chave privada do certificado numa cadeia JSON e carrega-toohello Cofre de chaves. Utilize o certificado de cluster do Olá comando tooadd Olá e qualquer Cofre de chaves de toohello de certificados adicionais de aplicações. Repita este passo para todos os certificados adicionais que pretende tooinstall no seu cluster.

#### <a name="uploading-an-existing-certificate"></a>Carregar um certificado existente

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

Se obtiver um erro, como Olá mostrado aqui, normalmente, significa que tem um conflito de URL de recurso. conflito de Olá tooresolve, nome do Cofre de chaves de Olá de alteração.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Depois de resolver o conflito de Olá, saída Olá deve ter o seguinte aspeto:

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>É necessário Olá três anterior cadeias, CertificateThumbprint, SourceVault e CertificateURL, tooset segurança de um cluster do Service Fabric segura e tooobtain quaisquer certificados de aplicação que possam estar a utilizar para a segurança da aplicação. Se não guarde cadeias Olá, pode ser difícil tooretrieve-los através da consulta chave Olá cofre mais tarde.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>Criar um certificado autoassinado e carregá-lo toohello Cofre de chaves

Se já tiver carregado o seu Cofre de chaves de toohello de certificados, ignore este passo. Este passo é para gerar um novo certificado autoassinado e carregá-lo tooyour Cofre de chaves. Depois de alterar parâmetros Olá Olá script a seguir e, em seguida, executá-lo, deve ser pedido para uma palavra-passe do certificado.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

Se obtiver um erro, como Olá mostrado aqui, normalmente, significa que tem um conflito de URL de recurso. conflito de Olá tooresolve, nome do Cofre de chaves de alteração Olá, nome RG e assim sucessivamente.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Depois de resolver o conflito de Olá, saída Olá deve ter o seguinte aspeto:

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>É necessário Olá três anterior cadeias, CertificateThumbprint, SourceVault e CertificateURL, tooset segurança de um cluster do Service Fabric segura e tooobtain quaisquer certificados de aplicação que possam estar a utilizar para a segurança da aplicação. Se não guarde cadeias Olá, pode ser difícil tooretrieve-los através da consulta chave Olá cofre mais tarde.

 Nesta fase, deve ter Olá seguintes elementos no local:

* grupo de recursos do Olá Cofre de chaves.
* Olá Cofre de chaves e o respetivo URL (denominado SourceVault no Olá anterior a saída do PowerShell).
* certificado de autenticação de servidor de cluster Olá e o respetivo URL no Cofre de chaves Olá.
* os URLs no Cofre de chaves Olá e certificados de aplicação Olá.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>Configurar o Azure Active Directory para autenticação de cliente

Azure AD permite tooapplications de acesso de utilizador de toomanage organizações (conhecido como inquilinos). As aplicações são divididas aqueles com uma conta baseada na web IU de início de sessão e as pessoas com uma experiência de cliente nativo. Neste artigo, partimos do pressuposto que já criou um inquilino. Se não tiver, comece por ler [como tooget um Azure Active Directory inquilino][active-directory-howto-tenant].

Um cluster do Service Fabric oferece tooits de pontos de entrada várias funcionalidades de gestão, incluindo Olá baseada na web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] e [Visual Studio] [service-fabric-manage-application-in-visual-studio]. Como resultado, crie duas do Azure AD aplicações toocontrol acesso toohello cluster, uma aplicação web e uma aplicação nativa.

toosimplify alguns dos passos de Olá envolvidos na configuração do Azure AD com um cluster do Service Fabric, foi criado um conjunto de scripts do Windows PowerShell.

> [!NOTE]
> Tem de concluir Olá antes de criar o cluster de Olá os seguintes passos. Uma vez que scripts Olá esperam os nomes de clusters e os pontos finais, valores Olá deve ser planeadas e não os valores que já criou.

1. [Transfira scripts Olá] [ sf-aad-ps-script-download] tooyour computador.
2. Contexto Olá ficheiro zip, selecione **propriedades**, selecione Olá **desbloqueio** caixa de verificação e, em seguida, clique em **aplicar**.
3. Extraia o ficheiro zip Olá.
4. Executar `SetupApplications.ps1`e forneça Olá TenantId, ClusterName e WebApplicationReplyUrl como parâmetros. Por exemplo:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Pode encontrar o TenantId executando o comando do PowerShell Olá `Get-AzureSubscription`. Executar este comando apresenta Olá TenantId para cada subscrição.

    ClusterName é tooprefix utilizadas aplicações de Olá do Azure AD que são criadas pelo script de Olá. Não necessita de nome de cluster real toomatch Olá exatamente. É toomake apenas pretendido-lo mais fácil toomap do Azure AD artefactos toohello cluster do Service Fabric que está a ser utilizados com.

    WebApplicationReplyUrl é o ponto final da predefinição de Olá do Azure AD devolve tooyour utilizadores depois de concluir a iniciar sessão. Defina este ponto final como ponto final do Service Fabric Explorer Olá para o cluster, o que, por predefinição, está:

    https://&lt;cluster_domain&gt;: 19080/Explorer

    São toosign pedido na conta tooan que tenha privilégios administrativos para o inquilino Olá do Azure AD. Depois de iniciar sessão, o script de Olá cria Olá web e de aplicações nativas toorepresent o cluster do Service Fabric. Se observar a aplicações do inquilino Olá Olá [portal clássico do Azure][azure-classic-portal], deverá ver duas novas entradas:

   * *ClusterName*\_Cluster
   * *ClusterName*\_cliente

   script de Olá imprime Olá JSON é necessário pelo modelo do Azure Resource Manager Olá quando criar o cluster de Olá na secção seguinte, Olá, pelo que é uma janela do PowerShell boa ideia tookeep Olá abrir.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>Criar um modelo de Gestor de recursos de cluster do Service Fabric
Nesta secção, Olá produz de Olá anterior comandos do PowerShell são utilizados num modelo de Gestor de recursos de cluster do Service Fabric.

Modelos de Gestor de recursos de exemplo estão disponíveis no Olá [Galeria de modelo de início rápido do Azure no GitHub][azure-quickstart-templates]. Estes modelos, podem ser utilizados como um ponto de partida para o modelo de cluster.

### <a name="create-hello-resource-manager-template"></a>Criar modelo do Resource Manager Olá
Este guia utiliza Olá [5-nó cluster segura] [ service-fabric-secure-cluster-5-node-1-nodetype] modelo de exemplo e os parâmetros do modelo. Transferir `azuredeploy.json` e `azuredeploy.parameters.json` tooyour computador e abra ambos os ficheiros no seu editor de texto favorito.

### <a name="add-certificates"></a>Adicione certificados
Adicionar modelo de Gestor de recursos de cluster de tooa certificados consultando o Cofre de chaves Olá contém Olá chaves de certificado. Recomendamos que coloque os valores do Cofre de chaves de Olá num ficheiro de parâmetros de modelo do Resource Manager. Se o fizer, mantém Olá Gestor de recursos do ficheiro de modelo reutilizáveis e gratuita da implementação de tooa específico de valores.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>Adicionar o que conjunto de dimensionamento de máquina virtual de toohello do todos os certificados de osProfile
Cada certificado que está instalado num cluster de Olá tem de ser configurado na secção de osProfile Olá do recurso de conjunto de dimensionamento de Olá (Microsoft.Compute/virtualMachineScaleSets). Esta ação dá instruções ao certificado Olá tooinstall de fornecedor de recursos de Olá no Olá VMs. Esta instalação inclui o certificado de cluster Olá e quaisquer certificados de segurança de aplicações que planeia toouse para as suas aplicações:

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Configurar o certificado de cluster do Service Fabric Olá
certificado de autenticação do cluster Olá tem de ser configurado em ambos os recursos de cluster de Service Fabric Olá (Microsoft.ServiceFabric/clusters) e define Olá extensão do Service Fabric de dimensionamento da máquina virtual no recurso de conjunto de dimensionamento de máquina virtual de Olá. Esta disposição permite tooconfigure de fornecedor de recursos de Service Fabric Olá-lo para ser utilizado para autenticação de cluster e autenticação de servidor para pontos finais de gestão.

##### <a name="virtual-machine-scale-set-resource"></a>Recurso de conjunto de dimensionamento de máquina virtual:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>Recurso de infraestrutura de serviço:
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Inserir a configuração do Azure AD
configuração de Olá do Azure AD que criou anteriormente pode ser inserida diretamente no seu modelo do Resource Manager. No entanto, recomendamos que primeiro extrair os valores de Olá para um parâmetros ficheiro tookeep Olá Resource Manager modelo reutilizáveis e gratuita da implementação de tooa específico de valores.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### < um "Configurar-braço" ></a>parâmetros de modelo do Resource Manager configurar
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
Por fim, utilize os valores de saída de Olá do Cofre de chaves de Olá e o ficheiro de parâmetros do Azure AD PowerShell comandos toopopulate Olá:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
Nesta fase, deve ter Olá seguintes elementos no local:

* Grupo de recursos do Cofre de chaves
  * Key Vault
  * Certificado de autenticação de servidor de cluster
  * Certificado de encriptação de dados
* Inquilino do Azure Active Directory
  * Aplicação Azure AD para a gestão baseada na web e o Service Fabric Explorer
  * Aplicação Azure AD para a gestão de cliente nativo
  * Os utilizadores e as respetivas funções atribuídas
* Modelo de Gestor de recursos de cluster do Service Fabric
  * Certificados configurados por meio do Cofre de chaves
  * Azure Active Directory configurado

Olá seguinte diagrama ilustra onde ajustam o seu Cofre de chaves e a configuração do AD do Azure ao seu modelo do Resource Manager.

![Mapa de dependência do Gestor de recursos][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Criar cluster Olá
Agora, está pronto toocreate cluster de Olá utilizando [implementação do modelo de recursos do Azure][resource-group-template-deploy].

#### <a name="test-it"></a>Testá-lo
Utilize o modelo do Resource Manager com um ficheiro de parâmetros a Olá seguir tootest de comando do PowerShell:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>Implementá-la
Se passar de teste de modelo do Resource Manager Olá, utilize Olá seguir toodeploy de comando do PowerShell do modelo do Resource Manager com um ficheiro de parâmetros:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>Atribuir utilizadores tooroles
Depois de criar Olá aplicações toorepresent o cluster, atribuir os seus utilizadores funções toohello suportadas pelo Service Fabric: só de leitura e administrador. Pode atribuir funções de Olá utilizando Olá [portal clássico do Azure][azure-classic-portal].

1. No portal do Azure Olá, aceda tooyour inquilino e, em seguida, selecione **aplicações**.
2. Selecione a aplicação web Olá, que tem um nome como `myTestCluster_Cluster`.
3. Clique em Olá **utilizadores** separador.
4. Selecione um tooassign de utilizador e, em seguida, clique em Olá **atribuir** botão na Olá parte inferior do ecrã de Olá.

    ![Atribuir botão tooroles de utilizadores][assign-users-to-roles-button]
5. Selecione Olá função tooassign toohello utilizador.

    ![Caixa de diálogo "Atribuir utilizadores"][assign-users-to-roles-dialog]

> [!NOTE]
> Para obter mais informações sobre as funções no Service Fabric, consulte [controlo de acesso baseado em funções para clientes de Service Fabric](service-fabric-cluster-security-roles.md).
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Criar clusters seguros no Linux
processo de Olá toomake mais fácil, fornecemos uma [script de programa auxiliar](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux). Antes de utilizar este script de programa auxiliar, certifique-se de que já tem interface de linha de comandos do Azure (CLI) instalado e é no seu caminho. Certifique-se de que o script de Olá tem permissões tooexecute executando `chmod +x cert_helper.py` após transferindo-a. Step-by-Olá primeiro passo é toosign no tooyour conta do Azure ao utilizar a CLI com Olá `azure login` comando. Depois de iniciarem sessão tooyour conta do Azure, o script de programa auxiliar de Olá utilização com a sua AC assinado certificado, como Olá comando mostra os seguintes:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

parâmetro de - ifile Olá pode demorar um ficheiro. pfx ou um ficheiro. pem como entrada, com o tipo de certificado Olá (pfx ou pem ou ss se se tratar de um certificado autoassinado).
Olá parâmetro -h imprime o texto de ajuda de Olá.


Este comando devolve Olá seguintes três cadeias como saída Olá:

* SourceVaultID, que é o ID de Olá para Olá novo ResourceGroup de KeyVault-criado para si
* CertificateUrl para aceder ao certificado Olá
* CertificateThumbprint, que é utilizado para autenticação

Olá seguinte exemplo mostra como toouse Olá, comando:

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
Executar Olá precedente fornecem comando Olá três cadeias da seguinte forma:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

nome do requerente do certificado Olá tem de corresponder ao domínio Olá que utilize o cluster do Service Fabric tooaccess Olá. Esta correspondência é necessário tooprovide um SSL para pontos finais de gestão do cluster Olá HTTPS e o Service Fabric Explorer. Não é possível obter um certificado SSL a partir de uma AC para Olá `.cloudapp.azure.com` domínio. Tem de obter um nome de domínio personalizado para o cluster. Quando solicitar um certificado a partir de uma AC, hello nome do requerente do certificado tem de corresponder ao nome de domínio personalizado de Olá que utilizar para o cluster.

Estes nomes de requerente são entradas Olá terá toocreate um cluster do Service Fabric seguro (do Azure AD), conforme descrito em [parâmetros de modelo do Resource Manager configurar](#configure-arm). Pode ligar cluster segura toohello seguindo as instruções de Olá para [autenticar o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md). Clusters de pré-visualização do Linux não suportam a autenticação do Azure AD. Pode atribuir funções de administrador e cliente conforme descrito em Olá [atribuir funções toousers](#assign-roles) secção. Quando especificar as funções de administrador e o cliente para um cluster de pré-visualização do Linux, tem tooprovide thumbprints de certificado para autenticação. (Não fornecer nome de requerente Olá, porque não está a ser efetuada nenhuma validação da cadeia ou revogação nesta versão de pré-visualização.)

Se quiser toouse um certificado autoassinado para fins de teste, pode utilizar Olá mesmo toogenerate script uma. Em seguida, pode carregar o Cofre de chaves Olá certificado tooyour fornecendo o sinalizador de Olá `ss` em vez de fornecer o nome de caminho e o certificado do certificado de Olá. Por exemplo, consulte Olá seguinte comando para criar e carregar um certificado autoassinado:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
Este comando devolve Olá mesmas três cadeias: SourceVault, CertificateUrl e CertificateThumbprint. Em seguida, pode utilizar Olá cadeias toocreate um cluster com Linux seguro e uma localização onde o certificado autoassinado Olá está colocado. Terá de cluster do Olá certificado autoassinado tooconnect toohello. Pode ligar cluster segura toohello seguindo as instruções de Olá para [autenticar o cluster de tooa de acesso de cliente](service-fabric-connect-to-secure-cluster.md).

nome do requerente do certificado Olá tem de corresponder ao domínio Olá que utilize o cluster do Service Fabric tooaccess Olá. Esta correspondência é necessário tooprovide um SSL para pontos finais de gestão do cluster Olá HTTPS e o Service Fabric Explorer. Não é possível obter um certificado SSL a partir de uma AC para Olá `.cloudapp.azure.com` domínio. Tem de obter um nome de domínio personalizado para o cluster. Quando solicitar um certificado a partir de uma AC, hello nome do requerente do certificado tem de corresponder ao nome de domínio personalizado de Olá que utilizar para o cluster.

Pode preencher os parâmetros de Olá do script de programa auxiliar de Olá no Olá portal do Azure, conforme descrito em Olá [cria um cluster no portal do Azure de Olá](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) secção.

## <a name="next-steps"></a>Passos seguintes
Neste momento, tiver um cluster seguro com fornecer autenticação de gestão do Azure Active Directory. Em seguida, [ligar tooyour cluster](service-fabric-connect-to-secure-cluster.md) e saber como demasiado[gerir segredos de aplicação](service-fabric-application-secret-management.md).

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>Resolver problemas de definição de cópia de segurança do Azure Active Directory para autenticação de cliente
Caso se depare com um problema enquanto estiver a configurar do Azure AD para autenticação de cliente, consulte possíveis soluções de Olá nesta secção.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>Service Fabric Explorer pede-lhe tooselect um certificado
#### <a name="problem"></a>Problema
Depois de iniciar sessão com êxito a tooAzure AD no Service Fabric Explorer, browser Olá devolve home page do toohello, mas uma mensagem pede-lhe tooselect um certificado.

![Caixa de diálogo do SFX selecione o certificado][sfx-select-certificate-dialog]

#### <a name="reason"></a>Razão
utilizador Olá não está atribuído uma função no Olá aplicação de cluster do Azure AD. Assim, a autenticação do Azure AD falha no cluster do Service Fabric. Service Fabric Explorer retrocede toocertificate autenticação.

#### <a name="solution"></a>Solução
Siga as instruções de Olá para configurar o Azure AD e atribuir funções de utilizador. Além disso, recomendamos que ative "Aplicação utilizador atribuição tooaccess necessária," como `SetupApplications.ps1` does.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>Falha da ligação com o PowerShell com um erro: "Olá especificado credenciais são inválidas"
#### <a name="problem"></a>Problema
Quando utilizar o PowerShell tooconnect toohello cluster utilizando o modo de segurança "AzureActiveDirectory", depois de iniciar sessão com êxito tooAzure AD, falha na ligação de Olá com um erro: "Olá especificado que credenciais são inválidas."

#### <a name="solution"></a>Solução
Esta solução é Olá que igual Olá anterior a um.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>Service Fabric Explorer devolve uma falha ao iniciar sessão: "AADSTS50011"
#### <a name="problem"></a>Problema
Quando tenta toosign no tooAzure AD no Service Fabric Explorer, a página Olá devolve uma falha: "AADSTS50011: Olá endereço de resposta &lt;url&gt; não correspondem aos endereços de resposta de Olá configurados para a aplicação Olá: &lt;guid&gt;."

![Não corresponde ao endereço de resposta SFX][sfx-reply-address-not-match]

#### <a name="reason"></a>Razão
aplicação de cluster (web) de Olá que representa o Service Fabric Explorer tenta tooauthenticate no Azure AD e como parte do pedido de Olá fornece URL de retorno de redirecionamento de Olá. Mas Olá URL não está listado na aplicação Olá do Azure AD **URL de resposta** lista.

#### <a name="solution"></a>Solução
No Olá **configurar** separador de Olá aplicação (web) do cluster, adicione Olá URL do Service Fabric Explorer toohello **URL de resposta** lista ou substituir um dos itens de Olá na lista de Olá. Quando tiver terminado, guarde as alterações.

![Url de resposta de aplicação Web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>Ligue o cluster de Olá, utilizando a autenticação do Azure AD através do PowerShell
Olá tooconnect cluster do Service Fabric, utilize Olá seguinte o exemplo de comando do PowerShell:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn sobre Olá Connect-ServiceFabricCluster cmdlet, consulte [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>Pode reutilizar inquilino Olá mesmo Azure AD em vários clusters?
Sim. Mas, lembre-se a aplicação do tooadd Olá URL do Service Fabric Explorer tooyour cluster (web). Caso contrário, o Service Fabric Explorer não funciona.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Por que motivo é ainda necessário um certificado de servidor ao Azure AD está ativado?
FabricClient e FabricGateway executará uma autenticação mútua. Durante a autenticação do Azure AD, a integração do Azure AD fornece um cliente servidor toohello de identidade e o certificado de servidor Olá é identidade do servidor utilizado tooverify Olá. Para obter mais informações sobre certificados de Service Fabric, consulte [certificados x. 509 e o Service Fabric][x509-certificates-and-service-fabric].

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

