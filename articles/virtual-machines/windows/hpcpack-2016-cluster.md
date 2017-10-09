---
title: aaaHPC 2016 de pacote do cluster no Azure | Microsoft Docs
description: Saiba como toodeploy um 2016 de pacote HPC cluster no Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Implementar um cluster HPC Pack 2016 no Azure

Siga os passos de Olá toodeploy este artigo um [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster em máquinas virtuais do Azure. Pacote HPC é solução HPC gratuita da Microsoft incorporada no Microsoft Azure e o Windows Server tecnologias e suporta um cargas de trabalho de intervalo HPC wide.

Utilize um dos Olá [modelos Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de Olá HPC Pack 2016. Existem várias opções de topologia de cluster com números diferentes de nós principais do cluster e com o Linux ou nós de computação do Windows.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="pfx-certificate"></a>Certificado PFX

Um cluster do Microsoft HPC Pack 2016 requer uma comunicação do Personal Information (Exchange PFX) certificado toosecure Olá entre os nós HPC Olá. certificado Olá tem de cumprir os requisitos de Olá:

* Tem de ter uma chave privada com capacidade de troca de chaves
* A utilização de chaves inclui a assinatura Digital e cifragem
* Utilização de chave avançada incluem autenticação de cliente e a autenticação de servidor

Se ainda não tiver um certificado que cumpra estes requisitos, pode pedir o certificado de Olá de uma autoridade de certificação. Em alternativa, pode utilizar Olá os seguintes comandos toogenerate Olá certificado autoassinado com base no sistema de operativo Olá no qual executar o comando de Olá e exportar um certificado PFX formato Olá com chave privada.

* **Para Windows 10 ou Windows Server 2016**, execute Olá incorporada **New-SelfSignedCertificate** cmdlet do PowerShell da seguinte forma:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Para sistemas operativos anteriores ao Windows 10 ou Windows Server 2016**, transferir Olá [gerador do certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de Olá Microsoft Script Center. Extraia os conteúdos e execute Olá os seguintes comandos numa linha de PowerShell:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Carregar o certificado tooan Cofre de chaves do Azure

Antes de implementar o cluster HPC de Olá, carregar Olá certificado tooan [Cofre de chaves do Azure](../../key-vault/index.md) como um Olá secreta e registo seguintes informações para utilização durante a implementação de Olá: **nome do cofre**,  **Grupo de recursos do cofre**, **URL de certificado**, e **thumbprint do certificado**.

Um certificado de Olá tooupload de script de PowerShell de exemplo seguinte. Para obter mais informações sobre como carregar um certificado tooan Cofre de chaves do Azure, consulte [introdução ao Cofre de chaves do Azure](../../key-vault/key-vault-get-started.md).

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>Topologias suportadas

Escolha uma das Olá [modelos Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de Olá HPC Pack 2016. Seguem-se arquiteturas de alto nível das três topologias de cluster suportadas. Topologias de elevada disponibilidade incluem vários nós principais do cluster.

1. Cluster de elevada disponibilidade com o domínio do Active Directory

    ![Cluster do HA no domínio do AD](./media/hpcpack-2016-cluster/haad.png)



2. Cluster de elevada disponibilidade sem o domínio do Active Directory

    ![Cluster do HA sem domínio AD](./media/hpcpack-2016-cluster/hanoad.png)

3. Cluster com um único nó principal

   ![Cluster com o único nó principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Implementar um cluster

cluster de Olá toocreate, escolha um modelo e clique em **implementar tooAzure**. No Olá [portal do Azure](https://portal.azure.com), especifique os parâmetros para o modelo de Olá, conforme descrito em Olá os seguintes passos. Cada modelo cria todos os recursos do Azure necessários para a infraestrutura de cluster HPC Olá. Recursos incluem uma Azure virtual network, pública IP endereços, o Balanceador de carga (apenas para um cluster de elevada disponibilidade), interfaces de rede, conjuntos de disponibilidade, contas de armazenamento e máquinas virtuais.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Passo 1: Selecione a subscrição de Olá, localização e grupo de recursos

Olá **subscrição** e Olá **localização** tem de ser o mesmo que especificou quando carregou o certificado do PFX (consulte pré-requisitos). Recomendamos que crie um **grupo de recursos** para a implementação de Olá.

### <a name="step-2-specify-hello-parameter-settings"></a>Passo 2: Especificar as definições de parâmetro de Olá

Introduza ou altere os valores de parâmetros de modelo Olá. Clique em Olá ícone seguinte tooeach parâmetro informações de ajuda. Consulte também as orientações de Olá para [tamanhos VM disponíveis](sizes.md).

Especifique os valores de Olá que registou no Olá pré-requisitos para seguir os parâmetros de Olá: **nome do cofre**, **grupo de recursos do cofre**, **URL de certificado**e **Thumbprint do certificado**.

### <a name="step-3-review-legal-terms-and-create"></a>Passo 3. Reveja os termos legais e criar
Clique em **consultar termos legais** termos de Olá tooreview. Se concordar, clique em **Compra**e, em seguida, clique em **criar** implementação de Olá toostart.

## <a name="connect-toohello-cluster"></a>Ligue o cluster de toohello
1. Após a implementação de cluster HPC Pack de Olá, aceda toohello [portal do Azure](https://portal.azure.com). Clique em **grupos de recursos**e encontrar o grupo de recursos de Olá que Olá cluster foi implementado. Pode encontrar Olá máquinas de virtuais do nó principal.

    ![Nós principais do cluster no portal de Olá](./media/hpcpack-2016-cluster/clusterhns.png)

2. Clique num nó principal (num cluster de elevada disponibilidade, clique em qualquer um de nós principais Olá). No **Essentials**, pode encontrar o endereço IP público Olá ou nome DNS completo de cluster Olá.

    ![Definições de ligação de cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Clique em **Connect** toolog no tooany de nós principais Olá através de ambiente de trabalho remoto com o seu nome de utilizador de administrador especificadas. Se tiver cluster Olá implementou um domínio do Active Directory, o nome de utilizador de Olá tem o formato de Olá <privateDomainName> \<adminUsername > (por exemplo, hpc.local\hpcadmin).

## <a name="next-steps"></a>Passos seguintes
* Submeta cluster tooyour de tarefas. Consulte [submeter tarefas tooHPC um cluster HPC Pack no Azure](hpcpack-cluster-submit-jobs.md) e [gerir um cluster HPC Pack 2016 no Azure utilizando o Azure Active Directory](hpcpack-cluster-active-directory.md).

