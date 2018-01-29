---
title: Ligar a pilha do Azure com a CLI | Microsoft Docs
description: Saiba como utilizar a interface de linha de comandos (CLI) de plataforma para gerir e implementar os recursos na pilha do Azure
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/04/2017
ms.author: mabrigg
ms.openlocfilehash: 3ca71abb1b84f619cfafbf4c25b0c0cb95430858
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="install-and-configure-cli-for-use-with-azure-stack"></a>Instalar e configurar a CLI para utilização com a pilha do Azure

Neste artigo, vamos ajudá-lo durante o processo de utilizar a interface de linha de comandos do Azure (CLI) para gerir os recursos do Azure pilha Development Kit do Linux e plataformas de cliente Mac. 

## <a name="install-cli"></a>Instalar CLI

Em seguida, inicie sessão na estação de trabalho de desenvolvimento e instalar a CLI. Pilha do Azure requer a versão 2.0 do CLI do Azure. Pode instalar que utilizando os passos descritos no [instalar o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) artigo. Para verificar se a instalação foi concluída com êxito, abra um terminal ou uma janela de linha de comandos e execute o seguinte comando:

```azurecli
az --version
```

Deverá ver a versão da CLI do Azure e outras bibliotecas dependentes que estão instaladas no seu computador.

## <a name="trust-the-azure-stack-ca-root-certificate"></a>Confiar no certificado de raiz de AC de pilha do Azure

Obter o certificado de raiz da AC de pilha do Azure do operador de pilha do Azure e confiar nele. Para confiar no certificado de raiz de AC de pilha do Azure, anexe o certificado existente do Python. Se estiver a executar o CLI de uma máquina de Linux que é criada no ambiente de pilha do Azure, execute o seguinte comando bash:

```bash
sudo cat /var/lib/waagent/Certificates.pem >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

Se estiver a executar o CLI de uma máquina fora do ambiente do Azure Sack, tem primeiro de configurar [conectividade VPN do Azure pilha](azure-stack-connect-azure-stack.md). Agora copie o certificado PEM que exportou anteriormente para a estação de trabalho de desenvolvimento e execute os comandos seguintes, dependendo do SO do seu desenvolvimento estação de trabalho.

### <a name="linux"></a>Linux

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="macos"></a>macOS

```bash
sudo cat PATH_TO_PEM_FILE >> ~/lib/azure-cli/lib/python2.7/site-packages/certifi/cacert.pem
```

### <a name="windows"></a>Windows

```powershell
$pemFile = "<Fully qualified path to the PEM certificate Ex: C:\Users\user1\Downloads\root.pem>"

$root = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
$root.Import($pemFile)

Write-Host "Extracting needed information from the cert file"
$md5Hash    = (Get-FileHash -Path $pemFile -Algorithm MD5).Hash.ToLower()
$sha1Hash   = (Get-FileHash -Path $pemFile -Algorithm SHA1).Hash.ToLower()
$sha256Hash = (Get-FileHash -Path $pemFile -Algorithm SHA256).Hash.ToLower()

$issuerEntry  = [string]::Format("# Issuer: {0}", $root.Issuer)
$subjectEntry = [string]::Format("# Subject: {0}", $root.Subject)
$labelEntry   = [string]::Format("# Label: {0}", $root.Subject.Split('=')[-1])
$serialEntry  = [string]::Format("# Serial: {0}", $root.GetSerialNumberString().ToLower())
$md5Entry     = [string]::Format("# MD5 Fingerprint: {0}", $md5Hash)
$sha1Entry    = [string]::Format("# SHA1 Finterprint: {0}", $sha1Hash)
$sha256Entry  = [string]::Format("# SHA256 Fingerprint: {0}", $sha256Hash)
$certText = (Get-Content -Path $pemFile -Raw).ToString().Replace("`r`n","`n")

$rootCertEntry = "`n" + $issuerEntry + "`n" + $subjectEntry + "`n" + $labelEntry + "`n" + `
$serialEntry + "`n" + $md5Entry + "`n" + $sha1Entry + "`n" + $sha256Entry + "`n" + $certText

Write-Host "Adding the certificate content to Python Cert store"
Add-Content "${env:ProgramFiles(x86)}\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem" $rootCertEntry

Write-Host "Python Cert store was updated for allowing the azure stack CA root certificate"
```

## <a name="get-the-virtual-machine-aliases-endpoint"></a>Obter o ponto final aliases de máquina virtual

Antes dos utilizadores podem criar máquinas virtuais ao utilizar a CLI, tem de contactar o operador de pilha do Azure e obter o URI do ponto de final aliases de máquina virtual. Por exemplo, o Azure utiliza o URI seguinte: https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json. O administrador da nuvem deve configurar um ponto final semelhante para pilha do Azure com as imagens que estão disponíveis no mercado pilha do Azure. Os utilizadores tem de passar o URI do ponto final para o `endpoint-vm-image-alias-doc` parâmetro para o `az cloud register` comando conforme mostrado na secção seguinte. 
   

## <a name="connect-to-azure-stack"></a>Ligar ao Azure Stack

Utilize os seguintes passos para ligar a pilha do Azure:

1. Registar o seu ambiente de pilha do Azure executando o `az cloud register` comando.
   
   a. Para registar o *nuvem administrativa* ambiente, utilize:

      ```azurecli
      az cloud register \ 
        -n AzureStackAdmin \ 
        --endpoint-resource-manager "https://adminmanagement.local.azurestack.external" \ 
        --suffix-storage-endpoint "local.azurestack.external" \ 
        --suffix-keyvault-dns ".adminvault.local.azurestack.external" \ 
        --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
        --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
      ```

   b. Para registar o *utilizador* ambiente, utilize:

      ```azurecli
      az cloud register \ 
        -n AzureStackUser \ 
        --endpoint-resource-manager "https://management.local.azurestack.external" \ 
        --suffix-storage-endpoint "local.azurestack.external" \ 
        --suffix-keyvault-dns ".vault.local.azurestack.external" \ 
        --endpoint-active-directory-graph-resource-id "https://graph.windows.net/" \
        --endpoint-vm-image-alias-doc <URI of the document which contains virtual machine image aliases>
      ```

2. Defina o ambiente do Active Directory utilizando os seguintes comandos.

   a. Para o *nuvem administrativa* ambiente, utilize:

      ```azurecli
      az cloud set \
        -n AzureStackAdmin
      ```

   b. Para o *utilizador* ambiente, utilize:

      ```azurecli
      az cloud set \
        -n AzureStackUser
      ```

3. Atualize a configuração do ambiente para utilizar o perfil de versão de API específico da pilha do Azure. Para atualizar a configuração, execute o seguinte comando:

   ```azurecli
   az cloud update \
     --profile 2017-03-09-profile
   ```

4. Inicie sessão no seu ambiente de pilha do Azure utilizando o `az login` comando. Pode iniciar sessão para o ambiente de pilha do Azure como um utilizador ou como um [principal de serviço](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects). 

   * Inicie sessão como um *utilizador*: pode especificar o nome de utilizador e palavra-passe diretamente dentro do `az login` comando ou autenticar utilizando um browser. Tem de fazer a última opção se a sua conta tem de multi-factor authentication ativada.

      ```azurecli
      az login \
        -u <Active directory global administrator or user account. For example: username@<aadtenant>.onmicrosoft.com> \
        --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com>
      ```

      > [!NOTE]
      > Se a sua conta de utilizador tiver a autenticação multifator ativada, pode utilizar o `az login command` sem fornecer o `-u` parâmetro. Executar o comando dá-lhe um URL e um código que tem de utilizar a autenticação.
   
   * Inicie sessão como um *principal de serviço*: antes de iniciar sessão, [criar um principal de serviço através do portal do Azure](azure-stack-create-service-principals.md) ou a CLI e atribua-lhe uma função. Agora, inicie sessão com o seguinte comando:

      ```azurecli
      az login \
        --tenant <Azure Active Directory Tenant name. For example: myazurestack.onmicrosoft.com> \
        --service-principal \
        -u <Application Id of the Service Principal> \
        -p <Key generated for the Service Principal>
      ```

## <a name="test-the-connectivity"></a>Testar a conectividade

Agora que já obtivemos tudo o programa de configuração, vamos utilizar a CLI para criar recursos na pilha do Azure. Por exemplo, pode criar um grupo de recursos para uma aplicação e adicionar uma máquina virtual. Utilize o seguinte comando para criar um grupo de recursos com o nome "MyResourceGroup":

```azurecli
az group create \
  -n MyResourceGroup -l local
```

Se o grupo de recursos é criado com êxito, o comando anterior produz as seguintes propriedades do recurso recentemente criado:

![Saída de criar grupo de recursos](media/azure-stack-connect-cli/image1.png)

## <a name="known-issues"></a>Problemas conhecidos
Existem alguns problemas conhecidos que deve ter em mente quando utilizar a CLI na pilha do Azure:

* Revertidos de modo interativo CLI o `az interactive` comando ainda não é suportado na pilha do Azure.
* Para obter a lista de imagens da máquina virtual disponíveis na pilha do Azure, utilize o `az vm images list --all` comando, em vez do `az vm image list` comando. Especificar o `--all` opção certifica-se de que a resposta devolve apenas as imagens que estão disponíveis no seu ambiente de pilha do Azure. 
* Aliases de imagem de máquina virtual que estão disponíveis no Azure podem não ser aplicáveis a pilha do Azure. Quando utilizar imagens da máquina virtual, tem de utilizar o parâmetro URN completo (Canonical: UbuntuServer:14.04.3-LTS:1.0.0) em vez do alias de imagem. Este URN deve corresponder às especificações de imagem derivado o `az vm images list` comando.
* Por predefinição, o CLI 2.0 utiliza "Standard_DS1_v2" como o tamanho predefinido da imagem de máquina virtual. No entanto, este tamanho não está ainda disponível na pilha do Azure, por isso, tem de especificar o `--size` parâmetro explicitamente quando criar uma máquina virtual. Pode obter a lista de tamanhos de máquinas virtuais que estão disponíveis na pilha do Azure utilizando o `az vm list-sizes --location <locationName>` comando.


## <a name="next-steps"></a>Passos Seguintes

[Implementar modelos com a CLI do Azure](azure-stack-deploy-template-command-line.md)

[Gerir permissões de utilizador](azure-stack-manage-permissions.md)
