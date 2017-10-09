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
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Processador de extensão de configuração de estado pretendido do Azure introdução toohello
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Olá agente da VM do Azure e as extensões associadas fazem parte do Olá dos serviços de infraestrutura do Microsoft Azure. Extensões de VM são os componentes de software que expandem a funcionalidade de VM Olá e simplificam a várias operações de gestão de VM. Por exemplo, Olá extensão VMAccess pode ser utilizado tooreset palavra-passe de um administrador ou Olá Script personalizado extensão pode ser utilizado tooexecute um script no Olá VM.

Este artigo apresenta Olá extensão pretendido Estado Configuration (DSC) do PowerShell para as VMs do Azure como parte da Olá SDK do Azure PowerShell. Pode utilizar os novos cmdlets tooupload e aplicar uma configuração de DSC do PowerShell numa VM do Azure ativada com Olá extensão de DSC do PowerShell. Olá chamadas de extensão de DSC do PowerShell para Olá do PowerShell DSC tooenact receberam a configuração de DSC na Olá VM. Esta funcionalidade está também disponível através de Olá portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
**Máquina local** toointeract com Olá extensão da VM do Azure, tem de toouse ou Olá portal do Azure ou Olá, Azure PowerShell SDK. 

**O agente convidado** Olá VM do Azure que está configurado por configuração Olá DSC tem toobe um sistema operativo que suporta o Windows Management Framework (WMF) 4.0 ou 5.0. obter uma lista completa Olá de versões de SO suportadas pode ser encontrada em Olá [histórico de versões de extensão de DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Conceitos e termos de licenciamento
Este guia presumes familiaridade com Olá seguintes conceitos:

Configuração - um documento de configuração de DSC. 

Nó - um destino para uma configuração de DSC. Neste documento, "nó" sempre refere-se tooan VM do Azure.

Dados de configuração - um. psd1 ficheiros que contêm dados ambientais para uma configuração

## <a name="architectural-overview"></a>Descrição geral da arquitetura
Olá extensão de DSC do Azure utiliza Olá agente da VM do Azure framework toodeliver, enact e elaborar relatórios sobre configurações de DSC em execução em VMs do Azure. Olá extensão de DSC espera um ficheiro. zip que contém, pelo menos, um documento de configuração e um conjunto de parâmetros fornecidos através de Olá SDK do Azure PowerShell ou de Olá portal do Azure.

Quando a extensão de Olá é chamado para Olá pela primeira vez, é executado um processo de instalação. Este processo é instalado uma versão de Olá Windows Management Framework (WMF) utilizando Olá lógica os seguintes:

1. Se Olá SO de VM do Azure for Windows Server 2016, não é necessária nenhuma ação. Windows Server 2016 já tem uma versão mais recente Olá do PowerShell instalada.
2. Se hello `wmfVersion` é especificada a propriedade e que versão do Olá WMF está instalada, a menos que é incompatível com a SO da VM Olá.
3. Se não `wmfVersion` é especificada a propriedade, Olá mais recente versão aplicável do Olá WMF está instalado.

Instalação de Olá WMF requer um reinício. Após o reinício, extensão Olá transfere o ficheiro. zip de Olá especificado no Olá `modulesUrl` propriedade. Se esta localização no armazenamento de Blobs do Azure, pode ser especificado um token SAS Olá `sasToken` propriedade tooaccess Olá ficheiro. Depois de Olá zip é transferido e descompactado, Olá função de configuração definida no `configurationFunction` está a executar o ficheiro MOF a toogenerate Olá. extensão de Olá, em seguida, executa `Start-DscConfiguration -Force` no ficheiro MOF Olá gerado. a extensão de Olá capturas de saída e escreve-a novamente saída toohello canal de estado do Azure. A partir deste ponto no Olá o MMC de DSC processa a monitorização e a correção como habitualmente. 

## <a name="powershell-cmdlets"></a>Cmdlets do PowerShell
Cmdlets do PowerShell podem ser utilizados com o Azure Resource Manager ou Olá toopackage de modelo de implementação clássica, publicar e monitorizar as implementações de extensão de DSC. Olá seguintes cmdlets listados são módulos de implementação clássica Olá, mas pode ser substituída "Azure" com o modelo do "AzureRm" toouse Olá Azure Resource Manager. Por exemplo, `Publish-AzureVMDscConfiguration` utiliza Olá modelo de implementação clássica, onde `Publish-AzureRmVMDscConfiguration` utiliza o Azure Resource Manager. 

`Publish-AzureVMDscConfiguration`aceita um ficheiro de configuração, analisa-lo para recursos de DSC dependentes e cria um ficheiro. zip que contém a configuração de Olá e configuração do DSC recursos necessários tooenact Olá. Também pode criar pacote Olá localmente utilizando Olá `-ConfigurationArchivePath` parâmetro. Caso contrário, publica o armazenamento de BLOBs de tooAzure de ficheiro. zip Olá e protege-lo com um token SAS.

ficheiro. zip de Olá criado por este cmdlet tem script de configuração. ps1 Olá na raiz de Olá da pasta de arquivo de Olá. Pasta do módulo Olá colocada na pasta de arquivo de Olá os recursos ter. 

`Set-AzureVMDscExtension`injects Olá as definições de Olá extensão de DSC do PowerShell para um objeto de configuração de VM. No modelo de implementação clássica Olá, alterações VM Olá tem de ser aplicado tooan VM do Azure com `Update-AzureVM`. 

`Get-AzureVMDscExtension`obtém o estado da extensão DSC Olá de uma VM específica. 

`Get-AzureVMDscExtensionStatus`obtém o estado de Olá da configuração de DSC Olá enacted pelo processador de extensão de DSC Olá. Esta ação pode ser efetuada num única VM, ou grupo de VMs.

`Remove-AzureVMDscExtension`Remove o processador de extensão de Olá de uma máquina virtual especificada. Este cmdlet **não** remover a configuração de Olá, desinstalar Olá WMF ou alterar as definições de Olá aplicado na máquina virtual de Olá. Remove apenas o processador de extensão de Olá. 

**Principais diferenças nos cmdlets ASM e o Azure Resource Manager**

* Cmdlets do Gestor de recursos do Azure são síncronos. Cmdlets ASM são assíncronos.
* ResourceGroupName, VMName, ArchiveStorageAccountName, versão e a localização estão todos os parâmetros necessários no Gestor de recursos do Azure.
* ArchiveResourceGroupName é um novo parâmetro opcional para o Azure Resource Manager. Pode especificar este parâmetro, quando a conta de armazenamento pertence tooa noutro grupo de recursos que Olá um onde a máquina virtual de Olá é criada.
* ConfigurationArchive denomina ArchiveBlobName no Gestor de recursos do Azure
* ContainerName denomina ArchiveContainerName no Gestor de recursos do Azure
* StorageEndpointSuffix denomina ArchiveStorageEndpointSuffix no Gestor de recursos do Azure
* foi adicionada comutador de AutoUpdate Olá tooAzure tooenable do Gestor de recursos automático de atualização de Olá processador toohello mais recente versão da extensão como e quando estiver disponível. Tenha em atenção de que este parâmetro tem toocause reinícios de potenciais Olá no Olá VM quando uma nova versão do Olá que WMF é libertado. 

## <a name="azure-portal-functionality"></a>Funcionalidade de portal do Azure
Procure tooa VM. Em Definições -> geral clique em "As extensões." É criado um novo painel. Clique em "Adicionar" e selecione o PowerShell DSC.

portal de Olá tem de entrada.
**Módulos de configuração ou Script**: Este campo é obrigatório. Necessita de um ficheiro. ps1, que contém um script de configuração ou um ficheiro. zip com um script de configuração. ps1 na raiz de Olá e todos os recursos dependentes, nas pastas de módulo no Olá zip. Podem ser criada com Olá `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet incluído no Olá SDK do Azure PowerShell. ficheiro. zip de Olá é carregado para o armazenamento de BLOBs de utilizador protegido por um token SAS. 

**Ficheiro de configuração de dados PSD1**: Este campo é opcional. Se a configuração necessita de um ficheiro de dados de configuração. psd1, utilize este campo tooselect-lo e carregue-o armazenamento de BLOBs de utilizador tooyour, onde é protegida por um token SAS. 

**Nome qualificado do módulo de configuração**:. ps1 ficheiros podem ter várias funções de configuração. Introduza o nome de Olá do script. ps1 de configuração de Olá seguido por um '\' e Olá nome da função de configuração de Olá. Por exemplo, se o script. ps1 tem Olá. o nome "configuration.ps1", não sendo configuração Olá "IisInstall", deve introduzir:`configuration.ps1\IisInstall`

**Configuração argumentos**: se a função de configuração de Olá aceita argumentos, introduzi-las a sessão aqui no formato de Olá `argumentName1=value1,argumentName2=value2`. Tenha em atenção de que este formato é um formato diferente que como argumentos de configuração são aceites através de cmdlets do PowerShell ou modelos do Resource Manager. 

## <a name="getting-started"></a>Introdução
Olá extensão de DSC do Azure aceita documentos de configuração de DSC e enacts-los em VMs do Azure. Segue-se um exemplo simple de uma configuração. Guarde-o localmente como "IisInstall.ps1":

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

Olá seguindo os passos local Olá IisInstall.ps1 script do Olá especificado VM, executar a configuração de Olá e devolver relatórios sobre o estado.
###<a name="classic-model"></a>Modelo clássico
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
###<a name="azure-resource-manager-model"></a>Modelo do Azure Resource Manager

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

## <a name="logging"></a>Registo
Os registos são colocados em:

C:\WindowsAzure\Logs\Plugins\Microsoft.PowerShell.DSC\[número de versão]

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre o PowerShell DSC, [visitar o Centro de documentação do PowerShell Olá](https://msdn.microsoft.com/powershell/dsc/overview). 

Examine Olá [modelo Azure Resource Manager para a extensão de Olá DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

toofind funcionalidades adicionais, pode gerir com o PowerShell DSC, [procurar galeria do PowerShell Olá](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) mais recursos de DSC.

Para obter detalhes sobre a transmitir parâmetros confidenciais para as configurações, consulte [gerir credenciais de forma segura com o processador de extensão de Olá DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

