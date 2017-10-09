# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="af29c-101">Através de gerido discos de modelos Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="af29c-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="af29c-102">Este documento explica Olá as diferenças entre discos geridos e quando utilizar máquinas virtuais do Azure Resource Manager modelos tooprovision.</span><span class="sxs-lookup"><span data-stu-id="af29c-102">This document walks through hello differences between managed and unmanaged disks when using Azure Resource Manager templates tooprovision virtual machines.</span></span> <span data-ttu-id="af29c-103">Isto irá ajudá-lo tooupdate modelos existentes que estão a utilizar discos de toomanaged discos não geridos.</span><span class="sxs-lookup"><span data-stu-id="af29c-103">This will help you tooupdate existing templates that are using unmanaged Disks toomanaged disks.</span></span> <span data-ttu-id="af29c-104">Para referência, estamos a utilizar Olá [101 vm-simples windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modelo como guia.</span><span class="sxs-lookup"><span data-stu-id="af29c-104">For reference, we are using hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="af29c-105">Pode ver o modelo de Olá utilizando ambos [discos geridos pelo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) e uma versão anterior utilizando [não gerido discos](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) se gostaria toodirectly compará-los.</span><span class="sxs-lookup"><span data-stu-id="af29c-105">You can see hello template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like toodirectly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="af29c-106">Modelo de discos não gerido formatação</span><span class="sxs-lookup"><span data-stu-id="af29c-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="af29c-107">toobegin, iremos veja são implementadas em discos como não geridos.</span><span class="sxs-lookup"><span data-stu-id="af29c-107">toobegin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="af29c-108">Quando criar discos não geridos, tem um armazenamento conta toohold Olá de ficheiros VHD.</span><span class="sxs-lookup"><span data-stu-id="af29c-108">When creating unmanaged disks, you need a storage account toohold hello VHD files.</span></span> <span data-ttu-id="af29c-109">Pode criar uma nova conta de armazenamento ou utilizar uma que já existe.</span><span class="sxs-lookup"><span data-stu-id="af29c-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="af29c-110">Este artigo irá mostrar como toocreate uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="af29c-110">This article will show you how toocreate a new storage account.</span></span> <span data-ttu-id="af29c-111">tooaccomplish, precisa de um recurso de conta de armazenamento no bloco de recursos de Olá conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="af29c-111">tooaccomplish this, you need a storage account resource in hello resources block as shown below.</span></span>

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

<span data-ttu-id="af29c-112">Dentro do objeto de máquina virtual de Olá, temos uma dependência no tooensure de conta de armazenamento Olá ter criado antes de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="af29c-112">Within hello virtual machine object, we need a dependency on hello storage account tooensure that it's created before hello virtual machine.</span></span> <span data-ttu-id="af29c-113">Dentro do Olá `storageProfile` secção, vamos, em seguida, especifique Olá URI completo de Olá localização do VHD, o que faz referência a conta de armazenamento Olá e é necessário para o disco de Olá SO e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="af29c-113">Within hello `storageProfile` section, we then specify hello full URI of hello VHD location, which references hello storage account and is needed for hello OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="af29c-114">Gerido a formatação do modelo de discos</span><span class="sxs-lookup"><span data-stu-id="af29c-114">Managed disks template formatting</span></span>

<span data-ttu-id="af29c-115">Com os discos gerida do Azure, o disco de Olá torna-se de um recurso de nível superior e já não necessita de um toobe de conta de armazenamento criado por utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="af29c-115">With Azure Managed Disks, hello disk becomes a top-level resource and no longer requires a storage account toobe created by hello user.</span></span> <span data-ttu-id="af29c-116">Discos geridos pela primeira vez foram expostos no Olá `2016-04-30-preview` versão de API, estão disponíveis em todas as versões de API subsequentes e estão agora o tipo de disco Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="af29c-116">Managed disks were first exposed in hello `2016-04-30-preview` API version, they are available in all subsequent API versions and are now hello default disk type.</span></span> <span data-ttu-id="af29c-117">Olá secções seguintes guiá-lo através de predefinições de Olá e como toofurther personalizar os discos de detalhe.</span><span class="sxs-lookup"><span data-stu-id="af29c-117">hello following sections walk through hello default settings and detail how toofurther customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="af29c-118">Recomenda-se toouse uma API versão posterior à `2016-04-30-preview` como ocorreram alterações entre `2016-04-30-preview` e `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="af29c-118">It is recommended toouse an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="af29c-119">Disco gerido predefinições</span><span class="sxs-lookup"><span data-stu-id="af29c-119">Default managed disk settings</span></span>

<span data-ttu-id="af29c-120">toocreate uma VM com discos geridos, que já não necessita de recurso de conta de armazenamento de Olá toocreate e pode atualizar o recurso de máquina virtual da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="af29c-120">toocreate a VM with managed disks, you no longer need toocreate hello storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="af29c-121">Especificamente, tenha em atenção que Olá `apiVersion` reflete `2017-03-30` e Olá `osDisk` e `dataDisks` já não consulte tooa URI específico para Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="af29c-121">Specifically note that hello `apiVersion` reflects `2017-03-30` and hello `osDisk` and `dataDisks` no longer refer tooa specific URI for hello VHD.</span></span> <span data-ttu-id="af29c-122">Quando implementar sem especificar propriedades adicionais, utilizará o disco de Olá [armazenamento LRS padrão](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="af29c-122">When deploying without specifying additional properties, hello disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="af29c-123">Não se for especificado nenhum nome, assume o formato Olá `<VMName>_OsDisk_1_<randomstring>` para o disco de SO de Olá e `<VMName>_disk<#>_<randomstring>` para cada disco de dados.</span><span class="sxs-lookup"><span data-stu-id="af29c-123">If no name is specified, it takes hello format of `<VMName>_OsDisk_1_<randomstring>` for hello OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="af29c-124">Por predefinição, a encriptação de disco do Azure está desativada; a colocação em cache é leitura/escrita para o disco de SO de Olá e nenhum dos discos de dados.</span><span class="sxs-lookup"><span data-stu-id="af29c-124">By default, Azure disk encryption is disabled; caching is Read/Write for hello OS disk and None for data disks.</span></span> <span data-ttu-id="af29c-125">Poderá reparar no exemplo Olá abaixo que há uma dependência de conta de armazenamento, embora isto é apenas para armazenamento de diagnóstico e não é necessária para armazenamento em disco.</span><span class="sxs-lookup"><span data-stu-id="af29c-125">You may notice in hello example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="af29c-126">Utilizar um recurso de nível superior de disco gerido</span><span class="sxs-lookup"><span data-stu-id="af29c-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="af29c-127">Como uma alternativa toospecifying Olá configuração do disco no objeto de máquina virtual de Olá, pode criar um recurso de disco de nível superior e ligá-lo como parte da criação da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="af29c-127">As an alternative toospecifying hello disk configuration in hello virtual machine object, you can create a top-level disk resource and attach it as part of hello virtual machine creation.</span></span> <span data-ttu-id="af29c-128">Por exemplo, podemos criar um recurso de disco, da seguinte forma toouse como um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="af29c-128">For example, we can create a disk resource as follows toouse as a data disk.</span></span>

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

<span data-ttu-id="af29c-129">Dentro do objeto da VM Olá, em seguida, iremos pode referenciar esta toobe de objeto disco ligado.</span><span class="sxs-lookup"><span data-stu-id="af29c-129">Within hello VM object, we can then reference this disk object toobe attached.</span></span> <span data-ttu-id="af29c-130">Especificar ID de recurso Olá de Olá geridos no disco que criou no Olá `managedDisk` propriedade permite anexo Olá do disco de Olá como Olá é criada a VM.</span><span class="sxs-lookup"><span data-stu-id="af29c-130">Specifying hello resource ID of hello managed disk we created in hello `managedDisk` property allows hello attachment of hello disk as hello VM is created.</span></span> <span data-ttu-id="af29c-131">Tenha em atenção que Olá `apiVersion` Olá recurso VM está definida demasiado`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="af29c-131">Note that hello `apiVersion` for hello VM resource is set too`2017-03-30`.</span></span> <span data-ttu-id="af29c-132">Note também que criámos uma dependência no tooensure de recurso de disco de Olá que é criado com êxito antes da criação da VM.</span><span class="sxs-lookup"><span data-stu-id="af29c-132">Also note that we've created a dependency on hello disk resource tooensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="af29c-133">Criar conjuntos de disponibilidade geridos com VMs com discos geridos</span><span class="sxs-lookup"><span data-stu-id="af29c-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="af29c-134">toocreate geridos disponibilidade conjuntos com VMs com discos geridos, adicionar Olá `sku` disponibilidade do objeto toohello definir recurso e Olá `name` propriedade demasiado`Aligned`.</span><span class="sxs-lookup"><span data-stu-id="af29c-134">toocreate managed availability sets with VMs using managed disks, add hello `sku` object toohello availability set resource and set hello `name` property too`Aligned`.</span></span> <span data-ttu-id="af29c-135">Isto garante que os discos de Olá para cada VM são suficientemente isolados de si tooavoid pontos únicos de falha.</span><span class="sxs-lookup"><span data-stu-id="af29c-135">This ensures that hello disks for each VM are sufficiently isolated from each other tooavoid single points of failure.</span></span> <span data-ttu-id="af29c-136">Tenha também em atenção que Olá `apiVersion` para recursos de conjunto de disponibilidade de Olá estiver definido demasiado`2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="af29c-136">Also note that hello `apiVersion` for hello availability set resource is set too`2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="af29c-137">Cenários adicionais e personalizações</span><span class="sxs-lookup"><span data-stu-id="af29c-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="af29c-138">toofind completo sobre as especificações de REST API de Olá, reveja Olá [criar um disco gerido documentação da REST API](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="af29c-138">toofind full information on hello REST API specifications, please review hello [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="af29c-139">Encontrará noutros cenários, bem como predefinição e os valores aceitáveis que podem ser submetidos toohello API através de implementações do modelo.</span><span class="sxs-lookup"><span data-stu-id="af29c-139">You will find additional scenarios, as well as default and acceptable values that can be submitted toohello API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="af29c-140">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="af29c-140">Next steps</span></span>

* <span data-ttu-id="af29c-141">Para modelos completos que utilizem discos geridos visite Olá seguintes hiperligações do repositório de início rápido do Azure.</span><span class="sxs-lookup"><span data-stu-id="af29c-141">For full templates that use managed disks visit hello following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="af29c-142">VM do Windows com o disco gerido</span><span class="sxs-lookup"><span data-stu-id="af29c-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="af29c-143">VM com Linux com o disco gerido</span><span class="sxs-lookup"><span data-stu-id="af29c-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="af29c-144">Obter uma lista completa dos modelos de disco gerido</span><span class="sxs-lookup"><span data-stu-id="af29c-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="af29c-145">Visite Olá [descrição geral do discos geridos Azure](../articles/virtual-machines/windows/managed-disks-overview.md) discos geridos pelo documento toolearn mais informações sobre como.</span><span class="sxs-lookup"><span data-stu-id="af29c-145">Visit hello [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document toolearn more about managed disks.</span></span>
* <span data-ttu-id="af29c-146">Consultar a documentação de referência de modelo Olá para recursos da máquina virtual, visitando Olá [referência ao modelo Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) documento.</span><span class="sxs-lookup"><span data-stu-id="af29c-146">Review hello template reference documentation for virtual machine resources by visiting hello [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="af29c-147">Consultar a documentação de referência de modelo Olá para recursos de disco, visitando Olá [referência ao modelo Microsoft.Compute/disks](/templates/microsoft.compute/disks) documento.</span><span class="sxs-lookup"><span data-stu-id="af29c-147">Review hello template reference documentation for disk resources by visiting hello [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
