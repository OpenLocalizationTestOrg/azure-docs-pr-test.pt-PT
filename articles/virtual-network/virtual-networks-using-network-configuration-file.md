---
title: "aaaConfigure uma rede Virtual do Azure (clássica) - ficheiro de configuração de rede | Microsoft Docs"
description: "Saiba como toocreate e modificar redes virtuais (clássicas) através da exportação, alterar e importar um ficheiro de configuração de rede."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Configurar uma rede virtual (clássica) utilizando um ficheiro de configuração de rede
> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que implementações mais novas utilizem o modelo de implementação do Resource Manager Olá.

Pode criar e configurar uma rede virtual (clássica) com um ficheiro de configuração de rede através de Olá interface de linha de comandos do Azure (CLI) 1.0 ou do Azure PowerShell. Não é possível criar ou modificar uma rede virtual através do modelo de implementação Azure Resource Manager Olá utilizando um ficheiro de configuração de rede. Não é possível utilizar Olá toocreate portal do Azure ou modificar uma rede virtual (clássica) utilizando um ficheiro de configuração de rede, no entanto, pode utilizar Olá toocreate do portal do Azure, uma rede virtual (clássica), sem utilizar um ficheiro de configuração de rede.

Criar e configurar uma rede virtual (clássica) com um ficheiro de configuração de rede necessitam de exportação, alterar e importar o ficheiro de Olá.

## <a name="export"></a>Exportar um ficheiro de configuração de rede

Pode utilizar o PowerShell ou Olá CLI do Azure tooexport um ficheiro de configuração de rede. PowerShell exporta um ficheiro XML, enquanto Olá CLI do Azure exporta um ficheiro json.

### <a name="powershell"></a>PowerShell
 
1. [Instalar o Azure PowerShell e inicie sessão tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Altere o diretório de Olá (e certifique-se de que existe) e o nome do ficheiro no Olá os seguintes comandos como pretendido, em seguida, execute Olá comando tooexport Olá rede ficheiro de configuração:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>CLI do Azure 1.0

1. [Instalar Olá CLI do Azure 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Concluir Olá restantes passos de uma linha de comandos da CLI do Azure 1.0.
2. Inicie sessão no tooAzure introduzindo Olá `azure login` comando.
3. Certifique-se de que está no modo asm introduzindo Olá `azure config mode asm` comando.
4. Altere o diretório de Olá (e certifique-se de que existe) e o nome do ficheiro no Olá os seguintes comandos como pretendido, em seguida, execute Olá comando tooexport Olá rede ficheiro de configuração:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Criar ou modificar um ficheiro de configuração de rede

Um ficheiro de configuração de rede é um ficheiro XML (ao utilizar o PowerShell) ou um ficheiro json (ao utilizar Olá CLI do Azure). Pode editar o ficheiro de Olá em qualquer texto ou editor de XML/json. Olá [definições de esquema do ficheiro de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx) artigo inclui os detalhes de todas as definições. Para obter explicações adicionais das definições de Olá, consulte [ver redes virtuais e definições](virtual-network-manage-network.md#view-vnet). alterações de Olá efetuar toohello ficheiro:

- Deve estar em conformidade com o esquema de Olá de importação de Olá de rede, ou o ficheiro de configuração falhará.
- Substituir as definições de rede existente para a sua subscrição, por isso, tenha muito cuidado quando efetuar alterações. Por exemplo, referencie Olá exemplo rede ficheiros de configuração que se seguem. Indicar o ficheiro original Olá contidos dois **VirtualNetworkSite** instâncias e foi alterado, conforme ilustrado nos exemplos de Olá. Quando importar o ficheiro de Olá, Azure elimina a rede virtual do Olá para Olá **VirtualNetworkSite** instância removido no ficheiro de Olá. Este cenário simplificado assume que não existem recursos foram na rede virtual Olá, como se existirem, não foi possível eliminar a rede virtual Olá e importar Olá irão falhar.

> [!IMPORTANT]
> Azure considera uma sub-rede que tenha algo implementado tooit como **em utilização**. Quando uma sub-rede em utilização, não pode ser modificado. Antes de modificar as informações de sub-rede num ficheiro de configuração de rede, mova tudo o que implementou toohello sub-rede tooa outra sub-rede que não está a ser modificado. Consulte [mover um tooa outra sub-rede VM ou instância de função](virtual-networks-move-vm-role-to-subnet.md) para obter mais detalhes.

### <a name="example-xml-for-use-with-powershell"></a>Exemplo XML para utilização com o PowerShell

Olá ficheiro de configuração de rede de exemplo seguinte cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereços de *10.0.0.0/16* no Olá *EUA Leste* Azure região. rede virtual Olá contém uma sub-rede designada *mySubnet* com um prefixo de endereço de *10.0.0.0/24*.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

Se o ficheiro de configuração de rede de Olá exportou não contém nenhum conteúdo, pode copiar Olá XML no exemplo anterior Olá e cole-o um novo ficheiro.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>JSON de exemplo para utilização com Olá CLI do Azure 1.0

Olá ficheiro de configuração de rede de exemplo seguinte cria uma rede virtual denominada *myVirtualNetwork* com um espaço de endereços de *10.0.0.0/16* no Olá *EUA Leste* Azure região. rede virtual Olá contém uma sub-rede designada *mySubnet* com um prefixo de endereço de *10.0.0.0/24*.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

Se o ficheiro de configuração de rede de Olá exportou não contém nenhum conteúdo, pode copiar o json de Olá no exemplo anterior Olá e cole-o um novo ficheiro.

## <a name="import"></a>Importar um ficheiro de configuração de rede

Pode utilizar o PowerShell ou Olá CLI do Azure tooimport um ficheiro de configuração de rede. PowerShell importa um ficheiro XML, enquanto Olá CLI do Azure importa um ficheiro json. Se falhar a importação de Olá, confirme que o ficheiro Olá está em conformidade com Olá [esquema de configuração de rede](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Instalar o Azure PowerShell e inicie sessão tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Alterar o diretório de Olá e nome do ficheiro no Olá os seguintes comandos conforme necessário, em seguida, execute o ficheiro de configuração de rede tooimport Olá Olá comando:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>CLI do Azure 1.0

1. [Instalar Olá CLI do Azure 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Concluir Olá restantes passos de uma linha de comandos da CLI do Azure 1.0.
2. Inicie sessão no tooAzure introduzindo Olá `azure login` comando.
3. Certifique-se de que está no modo asm introduzindo Olá `azure config mode asm` comando.
4. Alterar o diretório de Olá e nome do ficheiro no Olá os seguintes comandos conforme necessário, em seguida, execute o ficheiro de configuração de rede tooimport Olá Olá comando:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
