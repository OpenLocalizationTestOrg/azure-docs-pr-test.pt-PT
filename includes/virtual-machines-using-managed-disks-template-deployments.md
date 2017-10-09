# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Através de gerido discos de modelos Azure Resource Manager

Este documento explica Olá as diferenças entre discos geridos e quando utilizar máquinas virtuais do Azure Resource Manager modelos tooprovision. Isto irá ajudá-lo tooupdate modelos existentes que estão a utilizar discos de toomanaged discos não geridos. Para referência, estamos a utilizar Olá [101 vm-simples windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modelo como guia. Pode ver o modelo de Olá utilizando ambos [discos geridos pelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) e uma versão anterior utilizando [não gerido discos](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) se gostaria toodirectly compará-los.

## <a name="unmanaged-disks-template-formatting"></a>Modelo de discos não gerido formatação

toobegin, iremos veja são implementadas em discos como não geridos. Quando criar discos não geridos, tem um armazenamento conta toohold Olá de ficheiros VHD. Pode criar uma nova conta de armazenamento ou utilizar uma que já existe. Este artigo irá mostrar como toocreate uma nova conta de armazenamento. tooaccomplish, precisa de um recurso de conta de armazenamento no bloco de recursos de Olá conforme mostrado abaixo.

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

Dentro do objeto de máquina virtual de Olá, temos uma dependência no tooensure de conta de armazenamento Olá ter criado antes de máquina virtual de Olá. Dentro do Olá `storageProfile` secção, vamos, em seguida, especifique Olá URI completo de Olá localização do VHD, o que faz referência a conta de armazenamento Olá e é necessário para o disco de Olá SO e discos de dados. 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a>Gerido a formatação do modelo de discos

Com os discos gerida do Azure, o disco de Olá torna-se de um recurso de nível superior e já não necessita de um toobe de conta de armazenamento criado por utilizador Olá. Discos geridos pela primeira vez foram expostos no Olá `2016-04-30-preview` versão de API, estão disponíveis em todas as versões de API subsequentes e estão agora o tipo de disco Olá predefinido. Olá secções seguintes guiá-lo através de predefinições de Olá e como toofurther personalizar os discos de detalhe.

> [!NOTE]
> Recomenda-se toouse uma API versão posterior à `2016-04-30-preview` como ocorreram alterações entre `2016-04-30-preview` e `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Disco gerido predefinições

toocreate uma VM com discos geridos, que já não necessita de recurso de conta de armazenamento de Olá toocreate e pode atualizar o recurso de máquina virtual da seguinte forma. Especificamente, tenha em atenção que Olá `apiVersion` reflete `2017-03-30` e Olá `osDisk` e `dataDisks` já não consulte tooa URI específico para Olá VHD. Quando implementar sem especificar propriedades adicionais, utilizará o disco de Olá [armazenamento LRS padrão](../articles/storage/common/storage-redundancy.md). Não se for especificado nenhum nome, assume o formato Olá `<VMName>_OsDisk_1_<randomstring>` para o disco de SO de Olá e `<VMName>_disk<#>_<randomstring>` para cada disco de dados. Por predefinição, a encriptação de disco do Azure está desativada; a colocação em cache é leitura/escrita para o disco de SO de Olá e nenhum dos discos de dados. Poderá reparar no exemplo Olá abaixo que há uma dependência de conta de armazenamento, embora isto é apenas para armazenamento de diagnóstico e não é necessária para armazenamento em disco.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a>Utilizar um recurso de nível superior de disco gerido

Como uma alternativa toospecifying Olá configuração do disco no objeto de máquina virtual de Olá, pode criar um recurso de disco de nível superior e ligá-lo como parte da criação da máquina virtual de Olá. Por exemplo, podemos criar um recurso de disco, da seguinte forma toouse como um disco de dados.

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

Dentro do objeto da VM Olá, em seguida, iremos pode referenciar esta toobe de objeto disco ligado. Especificar ID de recurso Olá de Olá geridos no disco que criou no Olá `managedDisk` propriedade permite anexo Olá do disco de Olá como Olá é criada a VM. Tenha em atenção que Olá `apiVersion` Olá recurso VM está definida demasiado`2017-03-30`. Note também que criámos uma dependência no tooensure de recurso de disco de Olá que é criado com êxito antes da criação da VM. 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Criar conjuntos de disponibilidade geridos com VMs com discos geridos

toocreate geridos disponibilidade conjuntos com VMs com discos geridos, adicionar Olá `sku` disponibilidade do objeto toohello definir recurso e Olá `name` propriedade demasiado`Aligned`. Isto garante que os discos de Olá para cada VM são suficientemente isolados de si tooavoid pontos únicos de falha. Tenha também em atenção que Olá `apiVersion` para recursos de conjunto de disponibilidade de Olá estiver definido demasiado`2017-03-30`.

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a>Cenários adicionais e personalizações

toofind completo sobre as especificações de REST API de Olá, reveja Olá [criar um disco gerido documentação da REST API](/rest/api/manageddisks/disks/disks-create-or-update). Encontrará noutros cenários, bem como predefinição e os valores aceitáveis que podem ser submetidos toohello API através de implementações do modelo. 

## <a name="next-steps"></a>Passos seguintes

* Para modelos completos que utilizem discos geridos visite Olá seguintes hiperligações do repositório de início rápido do Azure.
    * [VM do Windows com o disco gerido](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [VM com Linux com o disco gerido](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Obter uma lista completa dos modelos de disco gerido](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Visite Olá [descrição geral do discos geridos Azure](../articles/virtual-machines/windows/managed-disks-overview.md) discos geridos pelo documento toolearn mais informações sobre como.
* Consultar a documentação de referência de modelo Olá para recursos da máquina virtual, visitando Olá [referência ao modelo Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.
* Consultar a documentação de referência de modelo Olá para recursos de disco, visitando Olá [referência ao modelo Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.
 
