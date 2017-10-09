---
title: "Implementação de aplicação com extensões de Máquina Virtual de aaaAutomating | Microsoft Docs"
description: "Tutorial do DotNet núcleos de Máquina Virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>Implementação de aplicação com modelos Azure Resource Manager para VMs do Windows

Depois de tem identificados e convertidos de um modelo de implementação de todos os requisitos de infraestrutura do Azure, implementação de aplicação real Olá tem toobe resolvido. Implementação de aplicação aqui faz referência binários da aplicação real Olá tooinstalling para recursos do Azure. Para o exemplo de arquivo de música Olá, .net Core e o IIS necessita toobe instalado e configurado em cada máquina virtual. Olá loja de música binários necessário toobe instalado na máquina virtual de Olá e Olá base de dados do arquivo de música previamente criada.

Este documento fornece detalhes sobre como extensões de Máquina Virtual podem automatizar a aplicação de implementação e configuração tooAzure máquinas virtuais. Todas as dependências e configurações exclusivas são realçadas. Para uma experiência otimizada Olá, pré-implemente uma instância de trabalho, juntamente com o modelo do Azure Resource Manager Olá e Olá solução tooyour subscrição do Azure. modelo completo Olá pode ser encontrado aqui – [implementação de arquivo de música em Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="configuration-script"></a>Script de configuração
Extensões de máquina virtual são programas especializados que executar em relação a automatização de configuração de tooprovide de máquinas virtuais. As extensões estão disponíveis para vários fins específicos, tais como o software antivírus, a configuração de registo e a configuração de Docker. Olá a extensão de Script personalizado pode ser utilizado toorun qualquer script em relação a uma máquina virtual. Exemplo do arquivo de música Olá, está a funcionar toohello script personalizado extensão tooconfigure Olá máquinas virtuais do Windows e instalar a aplicação da loja de música Olá.

Antes de com detalhes sobre como as extensões de máquina virtual são declaradas num modelo Azure Resource Manager, examine o script de Olá que está a ser executado. Este script configura Olá Windows máquina virtual toohost hello aplicação da loja de música. Quando executada, o script de Olá instala software todos os necessário, instalar aplicação da loja de música Olá do controlo de origem e preparar Olá base de dados. 

> Este exemplo está para efeitos de demonstração.

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a>Extensão de Script VM
Extensões de VM podem ser executadas em relação a uma máquina virtual no momento da compilação, incluindo o recurso de extensão de Olá num modelo do Azure Resource Manager Olá. extensão de Olá pode ser adicionado com o Assistente de Visual Studio adicionar recursos Olá ou por inserir o modelo de Olá JSON válido. Olá recursos de extensão de Script é aninhada Olá recurso de Máquina Virtual Isto pode ser visto no seguinte exemplo de Olá.

Siga esta ligação toosee Olá JSON amostra modelo do Resource Manager Olá – [extensão de Script de VM](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339). 

Observe que, Olá abaixo JSON Olá script é armazenado no GitHub. Este script também pode ser armazenado no Blob storage do Azure. Além disso, os modelos Azure Resource Manager permitem Olá script execução cadeia toobe construída de forma a que os valores de parâmetros de modelo podem ser utilizados como parâmetros para a execução do script. Neste caso, os dados são fornecidos quando implementar modelos de Olá e estes valores podem ser utilizados ao executar o script de Olá.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

Conforme mencionado, é também possível toostore sua personalizado de scripts no Blob storage do Azure. Existem duas opções para armazenar recursos de script de Olá no armazenamento de BLOBs torne Olá público de contentor/script e siga Olá mesmo abordar conforme apresentado acima, ou também podem ser mantido no armazenamento de BLOBs privada que requeiram tooprovide Olá storageAccountName e storageAccountKey toohello CustomScriptExtension definição do recurso.

No exemplo Olá abaixo podemos ter decorrido um passo adicional. Embora seja nome de conta de armazenamento de Olá tooprovide possíveis e a chave como um parâmetro ou variável durante a implementação, os modelos do Resource Manager fornecem Olá `listKeys` função que pode obter a conta de armazenamento Olá chave através de programação e insira-o no toohello modelo para si no momento da implementação.

Exemplo de Olá CustomScriptExtension definição do recurso abaixo, nosso script personalizado já foi carregado tooan denominada conta do storage do Azure `mystorageaccount9999` qual existe noutro grupo de recursos chamado `mysa999rgname`. Quando é implementar um modelo que contém este recurso, Olá `listKeys` função através de programação obtém a chave de conta do storage Olá Olá conta de armazenamento `mystorageaccount9999` no grupo de recursos de Olá `mysa999rgname` e insere-o no modelo de toohello para-nos.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

benefício de principais de Olá desta abordagem é que não requer toochange o modelo ou parâmetros de implementação no evento Olá de Olá armazenamento o alterar chave da conta.

Para obter mais informações sobre como utilizar a extensão de script personalizado Olá, consulte [extensões de script personalizado com modelos do Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-step"></a>Passo seguinte
<hr>

[Explorar os modelos do Gestor de recursos do Azure mais](https://github.com/Azure/azure-quickstart-templates)

