


## <a name="using-vm-extensions"></a><span data-ttu-id="46685-101">Utilizar extensões VM</span><span class="sxs-lookup"><span data-stu-id="46685-101">Using VM Extensions</span></span>
<span data-ttu-id="46685-102">Extensões de VM do Azure implementa comportamentos ou funcionalidades que ajudam a outros programas de trabalho em VMs do Azure (por exemplo, Olá **WebDeployForVSDevTest** extensão permite tooWeb do Visual Studio soluções de implementar na sua VM do Azure) ou indique Olá capacidade para toointeract com Olá VM toosupport alguns outro comportamento (por exemplo, pode utilizar extensões de acesso de VM de Olá do PowerShell, Olá CLI do Azure e REST clientes tooreset ou modificar os valores de acesso remoto na sua VM do Azure).</span><span class="sxs-lookup"><span data-stu-id="46685-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46685-103">Para obter uma lista completa das extensões as funcionalidades de Olá suportam, consulte [extensões de VM do Azure e funcionalidades](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="46685-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="46685-104">Porque cada extensão VM suporta uma funcionalidade específica, exatamente o que pode e não pode fazer com uma extensão depende da extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="46685-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="46685-105">Por conseguinte, antes de modificar a sua VM, certifique-se de que leu documentação Olá Olá pretende toouse extensão da VM.</span><span class="sxs-lookup"><span data-stu-id="46685-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="46685-106">A remoção algumas extensões de VM não é suportada; outras pessoas têm propriedades que podem ser definidas e alterar o comportamento VM forma radicalmente.</span><span class="sxs-lookup"><span data-stu-id="46685-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="46685-107">tarefas mais comuns Olá são:</span><span class="sxs-lookup"><span data-stu-id="46685-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="46685-108">Localizar as extensões disponíveis</span><span class="sxs-lookup"><span data-stu-id="46685-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="46685-109">Atualizar extensões carregadas</span><span class="sxs-lookup"><span data-stu-id="46685-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="46685-110">Adicionar extensões</span><span class="sxs-lookup"><span data-stu-id="46685-110">Adding Extensions</span></span>
4. <span data-ttu-id="46685-111">Remoção de extensões</span><span class="sxs-lookup"><span data-stu-id="46685-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="46685-112">Localizar as extensões disponíveis</span><span class="sxs-lookup"><span data-stu-id="46685-112">Find Available Extensions</span></span>
<span data-ttu-id="46685-113">Pode localizar a extensão e a utilização de informações expandidas:</span><span class="sxs-lookup"><span data-stu-id="46685-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="46685-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46685-114">PowerShell</span></span>
* <span data-ttu-id="46685-115">Interface de linha de comandos de plataforma do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="46685-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="46685-116">API REST da Gestão de Serviços</span><span class="sxs-lookup"><span data-stu-id="46685-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="46685-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46685-117">Azure PowerShell</span></span>
<span data-ttu-id="46685-118">Algumas extensões têm de cmdlets do PowerShell que são toothem específico, o que poderá facilitar a configuração a partir do PowerShell; mas hello seguintes cmdlets funciona para todas as extensões VM.</span><span class="sxs-lookup"><span data-stu-id="46685-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="46685-119">Pode utilizar Olá cmdlets tooobtain informações sobre as extensões disponíveis os seguintes:</span><span class="sxs-lookup"><span data-stu-id="46685-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="46685-120">Para as instâncias de funções da web ou funções de trabalho, pode utilizar Olá [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="46685-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="46685-121">Para as instâncias de máquinas virtuais, pode utilizar Olá [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="46685-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="46685-122">Por exemplo, Olá seguinte como exemplo de código mostra toolist as informações de Olá **IaaSDiagnostics** extensão com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="46685-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="46685-123">Interface de linha de comandos do Azure (CLI do Azure)</span><span class="sxs-lookup"><span data-stu-id="46685-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="46685-124">Algumas extensões têm de comandos da CLI do Azure que são específica toothem (Olá Docker extensão da VM é um exemplo), que poderá facilitar a respetiva configuração; mas seguinte Olá comandos trabalho para todas as extensões VM.</span><span class="sxs-lookup"><span data-stu-id="46685-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="46685-125">Pode utilizar Olá **lista de extensão de vm do azure** tooobtain informações sobre as extensões disponíveis de comandos e utilize Olá **–-json** opção toodisplay todas as informações disponíveis sobre uma ou mais extensões.</span><span class="sxs-lookup"><span data-stu-id="46685-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="46685-126">Se utilizar um nome de extensão, o comando de Olá devolve uma descrição JSON de todas as extensões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="46685-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="46685-127">Por exemplo, Olá seguinte exemplo de código mostra como toolist Olá informações para Olá **IaaSDiagnostics** extensão com Olá CLI do Azure **lista de extensão de vm do azure** comando e utiliza Olá **–-json** opção tooreturn informações.</span><span class="sxs-lookup"><span data-stu-id="46685-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="46685-128">APIs REST de Gestão de Serviço</span><span class="sxs-lookup"><span data-stu-id="46685-128">Service Management REST APIs</span></span>
<span data-ttu-id="46685-129">Pode utilizar Olá REST APIs tooobtain sobre as extensões disponíveis os seguintes:</span><span class="sxs-lookup"><span data-stu-id="46685-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="46685-130">Para as instâncias de funções da web ou funções de trabalho, pode utilizar Olá [extensões disponíveis lista](https://msdn.microsoft.com/library/dn169559.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="46685-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="46685-131">versões de Olá toolist das extensões disponíveis, pode utilizar [lista as versões de extensão](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="46685-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="46685-132">Para as instâncias de máquinas virtuais, pode utilizar Olá [extensões de recursos de lista](https://msdn.microsoft.com/library/dn495441.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="46685-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="46685-133">versões de Olá toolist das extensões disponíveis, pode utilizar [versões de extensão de recursos de lista](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="46685-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="46685-134">Adicionar, atualizar, ou desativar extensões</span><span class="sxs-lookup"><span data-stu-id="46685-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="46685-135">As extensões podem ser adicionadas quando é criada uma instância ou podem ser adicionados tooa executar instância.</span><span class="sxs-lookup"><span data-stu-id="46685-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="46685-136">As extensões podem ser atualizadas, desativadas ou removidas.</span><span class="sxs-lookup"><span data-stu-id="46685-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="46685-137">Pode efetuar estas ações utilizando cmdlets do PowerShell do Azure ou através da utilização de operações de API de REST de gestão do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="46685-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="46685-138">Os parâmetros são tooinstall necessária e algumas extensões de multimédia.</span><span class="sxs-lookup"><span data-stu-id="46685-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="46685-139">Parâmetros públicos e privados são suportados para as extensões.</span><span class="sxs-lookup"><span data-stu-id="46685-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="46685-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46685-140">Azure PowerShell</span></span>
<span data-ttu-id="46685-141">Utilizando cmdlets do PowerShell do Azure é Olá mais fácil forma tooadd e Atualize as extensões.</span><span class="sxs-lookup"><span data-stu-id="46685-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="46685-142">Quando utilizar os cmdlets de extensão de Olá, a maior parte da configuração de Olá da extensão de Olá é feito por si.</span><span class="sxs-lookup"><span data-stu-id="46685-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="46685-143">Por vezes, poderá ser necessário tooprogrammatically adicionar uma extensão.</span><span class="sxs-lookup"><span data-stu-id="46685-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="46685-144">Quando precisar de toodo isto, tem de fornecer configuração Olá da extensão de Olá.</span><span class="sxs-lookup"><span data-stu-id="46685-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="46685-145">Pode utilizar os seguintes cmdlets tooknow se uma extensão requer uma configuração de parâmetros públicas e privadas de Olá:</span><span class="sxs-lookup"><span data-stu-id="46685-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="46685-146">Para as instâncias de funções da web ou funções de trabalho, pode utilizar Olá **Get-AzureServiceAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="46685-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="46685-147">Para as instâncias de máquinas virtuais, pode utilizar Olá **Get-AzureVMAvailableExtension** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="46685-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="46685-148">APIs REST de Gestão de Serviço</span><span class="sxs-lookup"><span data-stu-id="46685-148">Service Management REST APIs</span></span>
<span data-ttu-id="46685-149">Ao obter uma listagem das extensões disponíveis utilizando Olá REST APIs, recebe informações sobre como a extensão de Olá toobe configurado.</span><span class="sxs-lookup"><span data-stu-id="46685-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="46685-150">informações de Olá que são devolvidas poderão mostrar informações de parâmetro representadas por um esquema pública e privada esquema.</span><span class="sxs-lookup"><span data-stu-id="46685-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="46685-151">Os valores de parâmetros público são devolvidos nas consultas sobre instâncias Olá.</span><span class="sxs-lookup"><span data-stu-id="46685-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="46685-152">Os valores de parâmetros privada não são devolvidos.</span><span class="sxs-lookup"><span data-stu-id="46685-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="46685-153">Pode utilizar Olá seguir tooknow de REST APIs, se uma extensão requer uma configuração de parâmetros públicas e privadas:</span><span class="sxs-lookup"><span data-stu-id="46685-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="46685-154">Para instâncias de funções da web ou funções de trabalho, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de Olá na resposta de Olá do Olá [lista As extensões disponíveis](https://msdn.microsoft.com/library/dn169559.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="46685-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="46685-155">Para instâncias de máquinas virtuais, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de Olá na resposta de Olá do Olá [lista Extensões de recursos](https://msdn.microsoft.com/library/dn495441.aspx) operação.</span><span class="sxs-lookup"><span data-stu-id="46685-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="46685-156">Extensões também podem utilizar as configurações que estão definidas com JSON.</span><span class="sxs-lookup"><span data-stu-id="46685-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="46685-157">Quando estes tipos de extensões são utilizados, apenas Olá **SampleConfig** elemento é utilizado.</span><span class="sxs-lookup"><span data-stu-id="46685-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

