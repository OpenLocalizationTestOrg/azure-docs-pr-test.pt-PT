---
title: "aaaOMS extensão da máquina virtual do Azure para Linux | Microsoft Docs"
description: "Implemente o agente do OMS Olá na máquina de virtual com Linux utilizando uma extensão da máquina virtual."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Extensão da máquina virtual OMS para Linux

## <a name="overview"></a>Descrição geral

Operations Management Suite (OMS) fornece capacidades de remediação de monitorização, alertas e alertas na nuvem e no local ativos. Olá extensão da máquina virtual de agente do OMS para Linux é publicado e suportado pela Microsoft. a extensão de Olá instala o agente do OMS Olá em máquinas virtuais do Azure e inscreve máquinas virtuais para uma área de trabalho existente do OMS. Olá de detalhes deste documento suportado plataformas, as configurações e opções de implementação para Olá extensão da máquina virtual OMS para Linux.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="operating-system"></a>Sistema operativo

Olá extensão de agente do OMS pode ser executada relativamente a estes distribuições do Linux.

| Distribuição | Versão |
|---|---|
| CentOS Linux | 5, 6 e 7 |
| Oracle Linux | 5, 6 e 7 |
| Red Hat Enterprise Linux Server | 5, 6 e 7 |
| Debian GNU/Linux | 6, 7 e 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| Servidor Linux Empresarial SUSE | 11 e 12 |

### <a name="internet-connectivity"></a>Conectividade Internet

Olá Linux na extensão do agente do OMS requer a máquina virtual de destino que Olá é toohello ligado à internet. 

## <a name="extension-schema"></a>Esquema de extensão

Olá seguinte JSON mostra esquema Olá para Olá extensão de agente do OMS. extensão de Olá requer Olá área de trabalho ID e a área de trabalho chave a partir da área de trabalho do OMS do destino de Olá; Estes valores podem ser encontrados no portal do OMS Olá. Porque a chave da área de trabalho de Olá deve ser tratado como dados confidenciais, devem ser armazenado numa configuração de definição protegido. Dados de definição de extensão protegido de VM do Azure é encriptados e desencriptados apenas na máquina de virtual de destino Olá. Tenha em atenção que **workspaceId** e **workspaceKey** diferenciam maiúsculas de minúsculas.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Valores de propriedade

| Nome | Valor / exemplo |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| Fabricante | Microsoft.EnterpriseCloud.Monitoring |
| tipo | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (por exemplo) | 6f680a37-00c6-41C7-a93f-1437e3462574 |
| workspaceKey (por exemplo) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI + rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ = = |


## <a name="template-deployment"></a>Implementação de modelos

Extensões VM do Azure podem ser implementadas com modelos Azure Resource Manager. Os modelos são ideais quando implementar um ou mais máquinas virtuais que necessitam de configuração de implementação de post, tais como tooOMS de integração. Um modelo de Gestor de recursos de exemplo que inclui a extensão da VM de agente do OMS Olá pode ser encontrado no Olá [Galeria de início rápido de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

configuração de JSON Olá para uma extensão de máquina virtual pode ser aninhada Olá recurso de máquina virtual ou colocada na raiz de Olá ou de nível superior de um modelo do Resource Manager JSON. a colocação da configuração de JSON Olá Olá afeta valor Olá Olá recursos nome e tipo. Para obter mais informações, consulte [definir nome e tipo para recursos subordinados](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Olá exemplo que se segue parte do princípio de extensão do OMS Olá é aninhada Olá recurso de máquina virtual. Quando o aninhamento de recursos de extensão de Olá, Olá JSON é colocada na Olá `"resources": []` objeto de máquina virtual de Olá.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Quando colocar extensão Olá JSON na raiz de Olá de modelo de Olá, nome do recurso Olá inclui uma máquina virtual do referência toohello principal e tipo de Olá reflete configuração aninhada Olá.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Implementação da CLI do Azure

Olá CLI do Azure pode ser utilizado toodeploy Olá VM de agente do OMS extensão tooan máquina virtual existente. Substitua a chave OMS de Olá e o ID do OMS com os da sua área de trabalho do OMS. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Resolver problemas e suporte

### <a name="troubleshoot"></a>Resolução de problemas

Dados sobre o estado de Olá das implementações de extensão de podem ser obtidos a partir da Olá portal do Azure e utilizando Olá CLI do Azure. Estado de implementação de Olá toosee das extensões para uma determinada VM, execute Olá utilizando o comando a seguir Olá CLI do Azure.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Execução de extensão de saída é toohello registado os seguintes ficheiros:

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Códigos de erro e os respetivos significados

| Código de erro | Significado | Ação possíveis |
| :---: | --- | --- |
| 10 | VM já se encontra ligado tooan área de trabalho do OMS | tooconnect Olá VM toohello área de trabalho especificada no esquema de extensão de Olá, defina stopOnMultipleConnections toofalse nas definições de públicas ou remova esta propriedade. Esta VM obtém cobrada depois de cada área de trabalho está ligado a um. |
| 11 | Configuração inválida fornecida toohello extensão | Siga Olá precedente exemplos tooset todos os valores de propriedade necessários para a implementação. |
| 12 | Gestor de pacotes de dpkg Olá está bloqueado | Certifique-se de que todos os dpkg operações de atualização na máquina de Olá tiver concluído e tente novamente. |
| 20 | Ativar chamado prematuramente | [Olá atualização agente Linux do Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello versão mais recente disponível. |
| 51 | Esta extensão não é suportada no sistema de operativo Olá da VM | |
| 55 | Não é possível ligar o serviço do Microsoft Operations Management Suite toohello | Verifique se Olá sistema tem acesso à Internet ou que foi fornecido um proxy HTTP válido. Além disso, verifique a correção de Olá do ID da área de trabalho Olá. |

Informações adicionais de resolução de problemas podem ser encontradas no Olá [guia de resolução de problemas do OMS agente para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Suporte

Se precisar de mais ajuda, a qualquer altura neste artigo, pode contactar Olá especialistas do Azure no Olá [fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/en-us/support/forums/). Em alternativa, pode ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/en-us/support/options/) e selecione o suporte de Get. Para obter informações sobre como utilizar o suporte do Azure, leia o artigo Olá [suporte do Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
