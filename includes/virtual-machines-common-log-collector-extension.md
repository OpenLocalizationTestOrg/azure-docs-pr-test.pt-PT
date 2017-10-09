
<span data-ttu-id="e044e-101">Diagnosticar problemas com um serviço em nuvem do Microsoft Azure necessita de recolher ficheiros de registo do serviço de Olá em máquinas virtuais como ocorrer problemas de Olá.</span><span class="sxs-lookup"><span data-stu-id="e044e-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="e044e-102">Pode utilizar a coleção de uma única tooperfom Olá AzureLogCollector extensão a pedido dos registos de um ou mais VMs de serviço de nuvem (a partir de funções da web e funções de trabalho) e transferência Olá recolhido ficheiros tooan conta do storage do Azure – tudo sem remotamente início de sessão tooany de Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="e044e-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="e044e-103">Descrições para a maioria das informações de Olá registada podem ser encontradas em http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="e044e-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="e044e-104">Existem dois modos de coleção depende de tipos de Olá de toobe ficheiros recolhidos.</span><span class="sxs-lookup"><span data-stu-id="e044e-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="e044e-105">Convidado do Azure agente registos apenas (GA).</span><span class="sxs-lookup"><span data-stu-id="e044e-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="e044e-106">Este modo da coleção inclui todos os agentes de convidado do Olá registos tooAzure relacionados e outros componentes do Azure.</span><span class="sxs-lookup"><span data-stu-id="e044e-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="e044e-107">Todos os registos (completa).</span><span class="sxs-lookup"><span data-stu-id="e044e-107">All Logs (Full).</span></span> <span data-ttu-id="e044e-108">Este modo da coleção recolherá todos os ficheiros no modo de GA mais:</span><span class="sxs-lookup"><span data-stu-id="e044e-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="e044e-109">registos de eventos do sistema e de aplicações</span><span class="sxs-lookup"><span data-stu-id="e044e-109">system and application event logs</span></span>
  * <span data-ttu-id="e044e-110">Registos de erros HTTP</span><span class="sxs-lookup"><span data-stu-id="e044e-110">HTTP error logs</span></span>
  * <span data-ttu-id="e044e-111">Registos de IIS</span><span class="sxs-lookup"><span data-stu-id="e044e-111">IIS Logs</span></span>
  * <span data-ttu-id="e044e-112">Registos de configuração</span><span class="sxs-lookup"><span data-stu-id="e044e-112">Setup logs</span></span>
  * <span data-ttu-id="e044e-113">outros registos de sistema</span><span class="sxs-lookup"><span data-stu-id="e044e-113">other system logs</span></span>

<span data-ttu-id="e044e-114">Em ambos os modos de coleção, as pastas de recolha de dados adicionais podem ser especificadas através da utilização de uma coleção de Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="e044e-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="e044e-115">**Nome**: nome de Olá da coleção de Olá, que será utilizada como nome de Olá da subpasta dentro Olá zip ficheiro toobe recolhidos.</span><span class="sxs-lookup"><span data-stu-id="e044e-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="e044e-116">**Localização**: Olá caminho toohello pasta na máquina virtual de olá onde serão recolhidos os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="e044e-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="e044e-117">**SearchPattern**: padrão de Olá Olá de nomes de toobe ficheiros recolhidos.</span><span class="sxs-lookup"><span data-stu-id="e044e-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="e044e-118">Predefinição é "*"</span><span class="sxs-lookup"><span data-stu-id="e044e-118">Default is “*”</span></span>
* <span data-ttu-id="e044e-119">**Recursiva**: se os ficheiros de Olá serão recolhido recursivamente na pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="e044e-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e044e-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e044e-120">Prerequisites</span></span>
* <span data-ttu-id="e044e-121">É necessário toohave uma conta de armazenamento para ficheiros de zip toosave gerado de extensão.</span><span class="sxs-lookup"><span data-stu-id="e044e-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="e044e-122">Tem de se certificar de que está a utilizar o Azure PowerShell Cmdlets V0.8.0 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e044e-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="e044e-123">Para obter mais informações, consulte [Azure transfere](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e044e-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="e044e-124">Adicionar extensão de Olá</span><span class="sxs-lookup"><span data-stu-id="e044e-124">Add hello extension</span></span>
<span data-ttu-id="e044e-125">Pode utilizar [do Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets ou [APIs REST do serviço de gestão](https://msdn.microsoft.com/library/ee460799.aspx) tooadd Olá AzureLogCollector extensão.</span><span class="sxs-lookup"><span data-stu-id="e044e-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="e044e-126">Para serviços em nuvem, Olá cmdlet do Powershell do Azure existente, **conjunto AzureServiceExtension**, podem ser utilizados tooenable Olá extensão instâncias de função de serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e044e-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="e044e-127">Sempre que esta extensão é ativada através deste cmdlet, a recolha de registos é acionada Olá selecionado instâncias de função dos direitos selecionados.</span><span class="sxs-lookup"><span data-stu-id="e044e-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="e044e-128">Para máquinas virtuais, Olá cmdlet do Powershell do Azure existente, **conjunto AzureVMExtension**, podem ser utilizados tooenable Olá extensão em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="e044e-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="e044e-129">Sempre que esta extensão é ativada através de cmdlets do Olá, recolha de registos é acionada em cada instância.</span><span class="sxs-lookup"><span data-stu-id="e044e-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="e044e-130">Internamente, esta extensão utiliza Olá PublicConfiguration baseados em JSON e PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="e044e-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="e044e-131">Olá que se segue esquema Olá de uma amostra JSON para a configuração pública e privada.</span><span class="sxs-lookup"><span data-stu-id="e044e-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="e044e-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="e044e-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="e044e-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="e044e-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="e044e-134">Esta extensão não necessita de **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="e044e-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="e044e-135">Apenas pode fornecer uma estrutura vazia para Olá **– PrivateConfiguration** argumento.</span><span class="sxs-lookup"><span data-stu-id="e044e-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="e044e-136">Pode seguir um Olá dois os seguintes passos tooadd Olá AzureLogCollector tooone ou mais instâncias de um serviço em nuvem ou Máquina Virtual dos direitos selecionados, os acionadores Olá coleções em cada VM toorun e enviam ficheiros Olá recolhido tooAzure conta especificado.</span><span class="sxs-lookup"><span data-stu-id="e044e-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="e044e-137">Adicionar como uma extensão de serviço</span><span class="sxs-lookup"><span data-stu-id="e044e-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="e044e-138">Siga a subscrição de tooyour Olá instruções tooconnect Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e044e-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="e044e-139">Especifique o nome do serviço Olá, ranhura, funções e toowhich de instâncias de função que pretende tooadd e ativar a extensão de AzureLogCollector Olá.</span><span class="sxs-lookup"><span data-stu-id="e044e-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="e044e-140">Especificar a pasta de dados adicionais de Olá para os quais serão recolhidos os ficheiros (este passo é opcional).</span><span class="sxs-lookup"><span data-stu-id="e044e-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="e044e-141">Pode utilizar o token `%roleroot%` unidade de raiz de função do toospecify Olá, uma vez que não utiliza uma unidade fixa.</span><span class="sxs-lookup"><span data-stu-id="e044e-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="e044e-142">Forneça o nome da conta de armazenamento do Azure Olá e ficheiros de chave toowhich recolhido serão carregados.</span><span class="sxs-lookup"><span data-stu-id="e044e-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="e044e-143">Chamada Olá SetAzureServiceLogCollector.ps1 (incluído no fim de Olá do artigo Olá) como extensão do modo tooenable Olá AzureLogCollector para um serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e044e-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="e044e-144">Depois de concluída a execução de Olá, pode encontrar o ficheiro Olá carregado em`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="e044e-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="e044e-145">Olá segue-se a definição de Olá dos parâmetros de Olá transmitido toohello script.</span><span class="sxs-lookup"><span data-stu-id="e044e-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="e044e-146">(Isto é copiado abaixo, bem como.)</span><span class="sxs-lookup"><span data-stu-id="e044e-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="e044e-147">*ServiceName*: O nome do serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e044e-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="e044e-148">*Funções*: uma lista de funções, tais como "WebRole1" ou "WorkerRole1".</span><span class="sxs-lookup"><span data-stu-id="e044e-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="e044e-149">*Instâncias*: uma lista de nomes de Olá de instâncias de função separados por vírgulas – utilizar a cadeia de carateres universais Olá ("*") para todas as instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="e044e-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="e044e-150">*Ranhura*: nome da ranhura.</span><span class="sxs-lookup"><span data-stu-id="e044e-150">*Slot*: Slot name.</span></span> <span data-ttu-id="e044e-151">"Production" ou "Transição".</span><span class="sxs-lookup"><span data-stu-id="e044e-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="e044e-152">*Modo*: modo da coleção.</span><span class="sxs-lookup"><span data-stu-id="e044e-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="e044e-153">"Completo" ou "GA".</span><span class="sxs-lookup"><span data-stu-id="e044e-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="e044e-154">*StorageAccountName*: recolhidos de conta de armazenamento do nome do Azure para armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="e044e-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="e044e-155">*StorageAccountKey*: a chave de conta de armazenamento de nome do Azure.</span><span class="sxs-lookup"><span data-stu-id="e044e-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="e044e-156">*AdditionalDataLocationList*: uma lista de Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="e044e-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="e044e-157">Adicionar como uma extensão VM</span><span class="sxs-lookup"><span data-stu-id="e044e-157">Adding as a VM Extension</span></span>
<span data-ttu-id="e044e-158">Siga a subscrição de tooyour Olá instruções tooconnect Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e044e-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="e044e-159">Especifique o nome do serviço Olá, VM e modo da coleção Olá.</span><span class="sxs-lookup"><span data-stu-id="e044e-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="e044e-160">Forneça o nome da conta de armazenamento do Azure Olá e ficheiros de chave toowhich recolhido serão carregados.</span><span class="sxs-lookup"><span data-stu-id="e044e-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="e044e-161">Chamada Olá SetAzureVMLogCollector.ps1 (incluído no fim de Olá do artigo Olá) como extensão do modo tooenable Olá AzureLogCollector para um serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="e044e-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="e044e-162">Depois de concluída a execução de Olá, pode encontrar o ficheiro Olá carregado em https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span><span class="sxs-lookup"><span data-stu-id="e044e-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="e044e-163">Olá segue-se a definição de Olá dos parâmetros de Olá transmitido toohello script.</span><span class="sxs-lookup"><span data-stu-id="e044e-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="e044e-164">(Isto é copiado abaixo, bem como.)</span><span class="sxs-lookup"><span data-stu-id="e044e-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="e044e-165">ServiceName: O nome do serviço cloud.</span><span class="sxs-lookup"><span data-stu-id="e044e-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="e044e-166">VMName Olá nome Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e044e-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="e044e-167">Modo: Modo de coleção.</span><span class="sxs-lookup"><span data-stu-id="e044e-167">Mode: Collection mode.</span></span> <span data-ttu-id="e044e-168">"Completo" ou "GA".</span><span class="sxs-lookup"><span data-stu-id="e044e-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="e044e-169">StorageAccountName: O nome da conta de armazenamento do Azure para armazenar os dados recolhidos.</span><span class="sxs-lookup"><span data-stu-id="e044e-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="e044e-170">StorageAccountKey: Nome da chave de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e044e-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="e044e-171">AdditionalDataLocationList: Uma lista de Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="e044e-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="e044e-172">Ficheiros de Script do PowerShell de extensão</span><span class="sxs-lookup"><span data-stu-id="e044e-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="e044e-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="e044e-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="e044e-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="e044e-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="e044e-175">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="e044e-175">Next Steps</span></span>
<span data-ttu-id="e044e-176">Agora pode examinar ou copiar os registos de uma localização muito simple.</span><span class="sxs-lookup"><span data-stu-id="e044e-176">Now you can examine or copy your logs from one very simple location.</span></span>

