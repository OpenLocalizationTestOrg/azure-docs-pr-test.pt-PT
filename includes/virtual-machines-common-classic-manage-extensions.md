


## <a name="using-vm-extensions"></a>Utilizar extensões VM
Extensões de VM do Azure implementa comportamentos ou funcionalidades que ajudam a outros programas de trabalho em VMs do Azure (por exemplo, Olá **WebDeployForVSDevTest** extensão permite tooWeb do Visual Studio soluções de implementar na sua VM do Azure) ou indique Olá capacidade para toointeract com Olá VM toosupport alguns outro comportamento (por exemplo, pode utilizar extensões de acesso de VM de Olá do PowerShell, Olá CLI do Azure e REST clientes tooreset ou modificar os valores de acesso remoto na sua VM do Azure).

> [!IMPORTANT]
> Para obter uma lista completa das extensões as funcionalidades de Olá suportam, consulte [extensões de VM do Azure e funcionalidades](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Porque cada extensão VM suporta uma funcionalidade específica, exatamente o que pode e não pode fazer com uma extensão depende da extensão de Olá. Por conseguinte, antes de modificar a sua VM, certifique-se de que leu documentação Olá Olá pretende toouse extensão da VM. A remoção algumas extensões de VM não é suportada; outras pessoas têm propriedades que podem ser definidas e alterar o comportamento VM forma radicalmente.
> 
> 

tarefas mais comuns Olá são:

1. Localizar as extensões disponíveis
2. Atualizar extensões carregadas
3. Adicionar extensões
4. Remoção de extensões

## <a name="find-available-extensions"></a>Localizar as extensões disponíveis
Pode localizar a extensão e a utilização de informações expandidas:

* PowerShell
* Interface de linha de comandos de plataforma do Azure (CLI do Azure)
* API REST da Gestão de Serviços

### <a name="azure-powershell"></a>Azure PowerShell
Algumas extensões têm de cmdlets do PowerShell que são toothem específico, o que poderá facilitar a configuração a partir do PowerShell; mas hello seguintes cmdlets funciona para todas as extensões VM.

Pode utilizar Olá cmdlets tooobtain informações sobre as extensões disponíveis os seguintes:

* Para as instâncias de funções da web ou funções de trabalho, pode utilizar Olá [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.
* Para as instâncias de máquinas virtuais, pode utilizar Olá [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.
  
   Por exemplo, Olá seguinte como exemplo de código mostra toolist as informações de Olá **IaaSDiagnostics** extensão com o PowerShell.
  
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

### <a name="azure-command-line-interface-azure-cli"></a>Interface de linha de comandos do Azure (CLI do Azure)
Algumas extensões têm de comandos da CLI do Azure que são específica toothem (Olá Docker extensão da VM é um exemplo), que poderá facilitar a respetiva configuração; mas seguinte Olá comandos trabalho para todas as extensões VM.

Pode utilizar Olá **lista de extensão de vm do azure** tooobtain informações sobre as extensões disponíveis de comandos e utilize Olá **–-json** opção toodisplay todas as informações disponíveis sobre uma ou mais extensões. Se utilizar um nome de extensão, o comando de Olá devolve uma descrição JSON de todas as extensões disponíveis.

Por exemplo, Olá seguinte exemplo de código mostra como toolist Olá informações para Olá **IaaSDiagnostics** extensão com Olá CLI do Azure **lista de extensão de vm do azure** comando e utiliza Olá **–-json** opção tooreturn informações.

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



### <a name="service-management-rest-apis"></a>APIs REST de Gestão de Serviço
Pode utilizar Olá REST APIs tooobtain sobre as extensões disponíveis os seguintes:

* Para as instâncias de funções da web ou funções de trabalho, pode utilizar Olá [extensões disponíveis lista](https://msdn.microsoft.com/library/dn169559.aspx) operação. versões de Olá toolist das extensões disponíveis, pode utilizar [lista as versões de extensão](https://msdn.microsoft.com/library/dn495437.aspx).
* Para as instâncias de máquinas virtuais, pode utilizar Olá [extensões de recursos de lista](https://msdn.microsoft.com/library/dn495441.aspx) operação. versões de Olá toolist das extensões disponíveis, pode utilizar [versões de extensão de recursos de lista](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Adicionar, atualizar, ou desativar extensões
As extensões podem ser adicionadas quando é criada uma instância ou podem ser adicionados tooa executar instância. As extensões podem ser atualizadas, desativadas ou removidas. Pode efetuar estas ações utilizando cmdlets do PowerShell do Azure ou através da utilização de operações de API de REST de gestão do serviço de Olá. Os parâmetros são tooinstall necessária e algumas extensões de multimédia. Parâmetros públicos e privados são suportados para as extensões.

### <a name="azure-powershell"></a>Azure PowerShell
Utilizando cmdlets do PowerShell do Azure é Olá mais fácil forma tooadd e Atualize as extensões. Quando utilizar os cmdlets de extensão de Olá, a maior parte da configuração de Olá da extensão de Olá é feito por si. Por vezes, poderá ser necessário tooprogrammatically adicionar uma extensão. Quando precisar de toodo isto, tem de fornecer configuração Olá da extensão de Olá.

Pode utilizar os seguintes cmdlets tooknow se uma extensão requer uma configuração de parâmetros públicas e privadas de Olá:

* Para as instâncias de funções da web ou funções de trabalho, pode utilizar Olá **Get-AzureServiceAvailableExtension** cmdlet.
* Para as instâncias de máquinas virtuais, pode utilizar Olá **Get-AzureVMAvailableExtension** cmdlet.

### <a name="service-management-rest-apis"></a>APIs REST de Gestão de Serviço
Ao obter uma listagem das extensões disponíveis utilizando Olá REST APIs, recebe informações sobre como a extensão de Olá toobe configurado. informações de Olá que são devolvidas poderão mostrar informações de parâmetro representadas por um esquema pública e privada esquema. Os valores de parâmetros público são devolvidos nas consultas sobre instâncias Olá. Os valores de parâmetros privada não são devolvidos.

Pode utilizar Olá seguir tooknow de REST APIs, se uma extensão requer uma configuração de parâmetros públicas e privadas:

* Para instâncias de funções da web ou funções de trabalho, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de Olá na resposta de Olá do Olá [lista As extensões disponíveis](https://msdn.microsoft.com/library/dn169559.aspx) operação.
* Para instâncias de máquinas virtuais, Olá **PublicConfigurationSchema** e **PrivateConfigurationSchema** elementos contêm informações de Olá na resposta de Olá do Olá [lista Extensões de recursos](https://msdn.microsoft.com/library/dn495441.aspx) operação.

> [!NOTE]
> Extensões também podem utilizar as configurações que estão definidas com JSON. Quando estes tipos de extensões são utilizados, apenas Olá **SampleConfig** elemento é utilizado.
> 
> 

