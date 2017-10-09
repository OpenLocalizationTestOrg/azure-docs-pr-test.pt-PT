---
title: "máquinas virtuais do Azure de aaaConnect tooLog Analytics | Microsoft Docs"
description: "Para o Windows e Linux máquinas virtuais em execução no Azure, Olá recomendado forma de registos recolhidos e métricas é através da instalação da extensão de VM do Azure de análise de registo Olá. Pode utilizar Olá portal do Azure ou do PowerShell tooinstall Olá extensão da máquina virtual de análise de registos em VMs do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Ligar máquinas virtuais do Azure tooLog análise com um agente de análise de registos

Para computadores Windows e Linux, Olá recomendado método para recolher registos e as métricas é pela instalação do agente de análise de registos de Olá.

Olá mais fácil forma tooinstall Olá análise de registos do agente máquinas virtuais do Azure é através de Olá extensão de VM de análise do registo.  Utilizando a extensão de Olá simplifica o processo de instalação de Olá e configura automaticamente Olá agente toosend dados toohello Log Analytics área de trabalho que especificar. agente de Olá também atualizada automaticamente, assegurando que tem Step-by-Olá mais recentes funcionalidades e correções.

Para máquinas virtuais do Windows, ativar Olá *Microsoft Monitoring Agent* extensão da máquina virtual.
Para máquinas virtuais do Linux, ativar Olá *OMS agente para Linux* extensão da máquina virtual.

Saiba mais sobre [extensões de máquina virtual do Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e Olá [agente Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Quando utilizar coleção baseada no agente para dados de registo, tem de configurar [origens de dados de análise de registos](log-analytics-data-sources.md) toospecify Olá registos e as métricas que pretende que o toocollect.

> [!IMPORTANT]
> Se configurar dados de registo do Log Analytics tooindex utilizando [diagnóstico do Azure](log-analytics-azure-storage.md), e configurar Olá toocollect agente de Olá mesmo inicia sessão, em seguida, Olá registos são recolhidos duas vezes. São-lhe cobrados para ambas as origens de dados. Se tiver o agente de Olá instalado, recolher dados de registo utilizando o agente de Olá só - não configurar dados de registo de toocollect de análise de registos de diagnóstico do Azure.
>
>

Existem três formas de fácil extensão da máquina virtual tooenable Olá análise de registos:

* Ao utilizar Olá portal do Azure
* Ao utilizar o Azure PowerShell
* Ao utilizar um modelo Azure Resource Manager

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Ativar a extensão VM Olá na Olá portal do Azure
Pode instalar o agente de Olá para análise de registos e ligar Olá máquina virtual do Azure, que é executada no utilizando Olá [portal do Azure](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall Olá agente da análise de registos e ligue-se a área de trabalho do Log Analytics do Olá máquina virtual tooa
1. Inicie sessão em Olá [portal do Azure](http://portal.azure.com).
2. Selecione **procurar** no Olá à esquerda do lado do Olá portal e, em seguida, aceda demasiado**análise de registos (OMS)** e selecioná-lo.
3. Na lista de áreas de trabalho de análise de registos, selecione Olá uma que pretenda toouse com Olá VM do Azure.  
   ![Áreas de trabalho do OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. Em **gestão de análise de registo**, selecione **máquinas virtuais**.  
   ![Máquinas virtuais](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. Na lista de Olá de **máquinas virtuais**, selecione Olá máquina virtual no qual pretende que o agente de Olá tooinstall. Olá **estado de ligação do OMS** para Olá VM indica que é **não ligado**.  
   ![VM não ligado](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. Nos detalhes de Olá para a máquina virtual, selecione **Connect**. agente de Olá é automaticamente instalado e configurado para a área de trabalho de análise de registos. Este processo demora alguns minutos, durante o período de tempo é Olá estado da ligação do OMS *ligar...*  
   ![Ligar a VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Depois de instalar e ligar o agente de Olá, Olá **ligação OMS** estado será atualizado tooshow **esta área de trabalho**.  
   ![Ligado](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Ativar a extensão VM de Olá através do PowerShell
Quando configurar a máquina virtual utilizando o PowerShell, terá de tooprovide Olá **workspaceId** e **workspaceKey**. os nomes de propriedade de Olá na sua configuração de json são **maiúsculas e minúsculas**.

Pode encontrar Olá Id e a chave no Olá **definições** página do portal do OMS hello, ou do PowerShell conforme mostrado no Olá anterior exemplo.

![ID da área de trabalho e a chave primária](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Existem diferentes comandos para máquinas virtuais clássicas do Azure e as máquinas virtuais do Gestor de recursos. Seguem-se exemplos de clássica e Resource Manager máquinas virtuais.

Para as máquinas virtuais clássicas, utilize Olá seguinte o exemplo do PowerShell:

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

Para VMs do Gestor de recursos com Linux utilizando Olá seguir CLI
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Para máquinas de virtuais do Gestor de recursos, utilize Olá seguinte o exemplo do PowerShell:

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a>Implementar a extensão da VM Olá através de um modelo
Ao utilizar o Azure Resource Manager, pode criar um modelo (no formato JSON) que define a implementação de Olá e configuração da sua aplicação. Este modelo é conhecido como um modelo do Resource Manager e fornece uma implementação de toodefine de forma declarativa. Ao utilizar um modelo, que pode implementar a aplicação durante todo o ciclo de vida Olá repetidamente e ter a confiança de que os recursos estão a ser implementados num estado consistente.

Ao incluir o agente de análise de registos de Olá como parte do seu modelo do Resource Manager, pode certificar-se de que cada máquina virtual é a área de trabalho de análise de registos de tooyour de tooreport previamente configurada.

Para mais informações sobre modelos do Resource Manager, consulte [modelos Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Segue-se um exemplo de um modelo do Resource Manager que é utilizado para implementar uma máquina virtual que está a executar o Windows com Olá extensão do Microsoft Monitoring Agent instalada. Este é um modelo de máquinas típicos, com Olá seguintes adições:

* parâmetros workspaceId e workspaceName
* Secção de extensão do recurso Microsoft.EnterpriseCloud.Monitoring
* Saídas toolook Olá workspaceId e workspaceSharedKey

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

Pode implementar um modelo através da utilização de Olá seguinte comando do PowerShell:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Extensão de VM de análise do registo de Olá de resolução de problemas
Normalmente, receberá uma mensagem quando coisas não funcionam, do portal do Azure ou o Azure powershell.

1. Inicie sessão em Olá [portal do Azure](http://portal.azure.com).
2. Localize Olá VM e abra os detalhes VM.
3. Clique em **extensões** toocheck se a extensão do OMS está ativada ou não.

   ![Vista de extensão de VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Clique em Olá *MicrosoftMonitoringAgent*(Windows) ou *OmsAgentForLinux*(Linux) extensão e vista de detalhes. 

   ![Detalhes da extensão de VM](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Resolução de problemas de máquinas virtuais do Windows
Se hello *Microsoft Monitoring Agent* extensão de agente da VM não está a instalar ou relatórios, pode realizar Olá problema de Olá tootroubleshoot de passos a seguir.

1. Verifique se o agente de VM do Azure de Olá está instalado e a funcionar corretamente utilizando Olá os passos em [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).
   * Também pode rever o ficheiro de registo do agente VM Olá`C:\WindowsAzure\logs\WaAppAgent.log`
   * Se o registo de Olá não existir, o agente da VM Olá não está instalado.
     * [Instalar Olá agente da VM do Azure em VMs clássicas](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Confirme Olá Microsoft Monitoring Agent está a executar tarefas de heartbeat de extensão utilizando Olá os seguintes passos:
   * Inicie sessão na máquina virtual de toohello
   * Abra o Programador de tarefas e determinar Olá `update_azureoperationalinsight_agent_heartbeat` tarefas
   * Certifique-se tarefas de Olá está ativada e está em execução a cada minuto
   * Verifique o ficheiro de registo de heartbeat de Olá na`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Consulte Olá ficheiros de registo de extensão VM de agente de monitorização da Microsoft no`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Certifique-se a máquina virtual de Olá pode executar scripts do PowerShell
5. Certifique-se de que as permissões num C:\Windows\temp ainda não foram alteradas
6. Ver o estado de Olá de Olá Microsoft Monitoring Agent escrevendo Olá os seguintes comandos numa janela elevada do PowerShell na máquina virtual de Olá`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Consulte Olá ficheiros de registo do programa de configuração de Microsoft Monitoring Agent no`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Para obter mais informações, consulte [resolução de problemas de extensões do Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Resolução de problemas de máquinas virtuais do Linux
Se hello *agente do OMS para Linux* extensão de agente da VM não está a instalar ou relatórios, pode realizar Olá problema de Olá tootroubleshoot de passos a seguir.

1. Se o estado da extensão Olá é *desconhecido* verificar se o agente da VM do Azure de Olá está instalado e a funcionar corretamente, revendo o ficheiro de registo do agente VM Olá`/var/log/waagent.log`
   * Se o registo de Olá não existir, o agente da VM Olá não está instalado.
   * [Instalar o agente da VM do Azure de Olá em VMs do Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Para outros Estados mau estado de funcionamento, reveja Olá agente do OMS para a extensão de VM com Linux ficheiros de registo `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` e`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Se o estado da extensão Olá está em bom estado, mas não estão a ser carregados dados reveja Olá agente do OMS para ficheiros de registo de Linux`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Passos seguintes
* Configurar [origens de dados de análise de registos](log-analytics-data-sources.md) toospecify Olá toocollect métricas e registos.
* toogather dados provenientes de máquinas virtuais [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).
* [Recolher dados, utilizando o Azure Diagnostics](log-analytics-azure-storage.md) para outros recursos que estão em execução no Azure.

Para computadores que não estão no Azure, pode instalar o agente de análise de registos de Olá utilizando métodos de Olá descritas Olá seguintes artigos:

* [Ligar tooLog de computadores Windows análise](log-analytics-windows-agents.md)
* [Ligar tooLog de computadores Linux análise](log-analytics-linux-agents.md)
