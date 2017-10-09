


<span data-ttu-id="10d0f-101">Este tópico descreve como:</span><span class="sxs-lookup"><span data-stu-id="10d0f-101">This topic describes how to:</span></span>

* <span data-ttu-id="10d0f-102">Inserir dados numa máquina virtual do Azure (VM) ao que está a ser aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="10d0f-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="10d0f-103">Obtê-lo para o Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="10d0f-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="10d0f-104">Utilizar ferramentas especiais disponíveis em algumas toodetect de sistemas e processar dados personalizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10d0f-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="10d0f-105">Este artigo descreve como personalizados dados podem ser injetadas através da utilização de uma VM criada com Olá API de gestão de serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="10d0f-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="10d0f-106">toosee como toouse Olá API de gestão de recursos do Azure, consulte [modelo de exemplo de Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="10d0f-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="10d0f-107">Dados personalizados inserirem-se para a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="10d0f-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="10d0f-108">Esta funcionalidade atualmente só é suportada em Olá [Interface de linha de comandos do Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="10d0f-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="10d0f-109">Aqui criamos uma `custom-data.txt` ficheiro que contém os nossos dados, em seguida, inserir que no toohello VM durante o aprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="10d0f-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="10d0f-110">Embora possa utilizar qualquer uma das opções de Olá para Olá `azure vm create` seguinte Olá demonstra uma abordagem muito básica, comando:</span><span class="sxs-lookup"><span data-stu-id="10d0f-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="10d0f-111">Dados personalizados a utilizar na máquina virtual de Olá</span><span class="sxs-lookup"><span data-stu-id="10d0f-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="10d0f-112">Se a VM do Azure é uma VM com base no Windows, em seguida, é guardado no ficheiro de dados personalizados Olá a demasiado`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="10d0f-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="10d0f-113">Embora foi com codificação base64 tootransfer de Olá computador local toohello nova VM, é automaticamente descodificar e pode ser aberta ou utilizadas imediatamente.</span><span class="sxs-lookup"><span data-stu-id="10d0f-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="10d0f-114">Se o ficheiro de Olá, será substituído.</span><span class="sxs-lookup"><span data-stu-id="10d0f-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="10d0f-115">segurança de Olá no diretório de Olá estiver definida demasiado**controlo de sistema: completo** e **administradores: completo controlo**.</span><span class="sxs-lookup"><span data-stu-id="10d0f-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="10d0f-116">Se a VM do Azure é uma VM baseado em Linux, em seguida, o ficheiro de dados personalizados Olá estarão localizado em um dos seguintes Olá coloca, dependendo do seu distro.</span><span class="sxs-lookup"><span data-stu-id="10d0f-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="10d0f-117">Olá poderão ser codificado por base64, pelo que poderá ter dados de Olá toodecode primeiro:</span><span class="sxs-lookup"><span data-stu-id="10d0f-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="10d0f-118">Init de nuvem no Azure</span><span class="sxs-lookup"><span data-stu-id="10d0f-118">Cloud-init on Azure</span></span>
<span data-ttu-id="10d0f-119">Se a VM do Azure é a partir de uma imagem Ubuntu ou CoreOS, em seguida, pode utilizar CustomData toosend uma configuração de nuvem toocloud-init.</span><span class="sxs-lookup"><span data-stu-id="10d0f-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="10d0f-120">Ou, se o ficheiro de dados personalizada é um script, em seguida, na nuvem init pode simplesmente executá-lo.</span><span class="sxs-lookup"><span data-stu-id="10d0f-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="10d0f-121">Ubuntu nuvem imagens</span><span class="sxs-lookup"><span data-stu-id="10d0f-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="10d0f-122">Na maioria das imagens de Linux do Azure, seria editar "/ etc/waagent.conf" tooconfigure Olá temporário disco e a comutação ficheiro de recursos.</span><span class="sxs-lookup"><span data-stu-id="10d0f-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="10d0f-123">Consulte [guia de utilizador do agente Linux do Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="10d0f-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="10d0f-124">No entanto, nas imagens de nuvem de Ubuntu Olá, tem de utilizar o disco de recursos de Olá do cloud init tooconfigure (ou seja, Olá "efémeras" disco) e a comutação partição.</span><span class="sxs-lookup"><span data-stu-id="10d0f-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="10d0f-125">Consulte Olá seguir a página Olá Ubuntu Wiki para obter mais detalhes: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="10d0f-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="10d0f-126">Próximas etapas: nuvem init a utilizar</span><span class="sxs-lookup"><span data-stu-id="10d0f-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="10d0f-127">Para obter mais informações, consulte Olá [documentação de nuvem init para Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="10d0f-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="10d0f-128">Adicionar referência de API de REST de gestão de serviço de função</span><span class="sxs-lookup"><span data-stu-id="10d0f-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="10d0f-129">Interface de linha de comandos do Azure</span><span class="sxs-lookup"><span data-stu-id="10d0f-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

