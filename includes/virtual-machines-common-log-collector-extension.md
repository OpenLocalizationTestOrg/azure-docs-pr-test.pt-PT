
Diagnosticar problemas com um serviço em nuvem do Microsoft Azure necessita de recolher ficheiros de registo do serviço de Olá em máquinas virtuais como ocorrer problemas de Olá. Pode utilizar a coleção de uma única tooperfom Olá AzureLogCollector extensão a pedido dos registos de um ou mais VMs de serviço de nuvem (a partir de funções da web e funções de trabalho) e transferência Olá recolhido ficheiros tooan conta do storage do Azure – tudo sem remotamente início de sessão tooany de Olá VMs.

> [!NOTE]
> Descrições para a maioria das informações de Olá registada podem ser encontradas em http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.
> 
> 

Existem dois modos de coleção depende de tipos de Olá de toobe ficheiros recolhidos.

* Convidado do Azure agente registos apenas (GA). Este modo da coleção inclui todos os agentes de convidado do Olá registos tooAzure relacionados e outros componentes do Azure.
* Todos os registos (completa). Este modo da coleção recolherá todos os ficheiros no modo de GA mais:
  
  * registos de eventos do sistema e de aplicações
  * Registos de erros HTTP
  * Registos de IIS
  * Registos de configuração
  * outros registos de sistema

Em ambos os modos de coleção, as pastas de recolha de dados adicionais podem ser especificadas através da utilização de uma coleção de Olá seguir a estrutura:

* **Nome**: nome de Olá da coleção de Olá, que será utilizada como nome de Olá da subpasta dentro Olá zip ficheiro toobe recolhidos.
* **Localização**: Olá caminho toohello pasta na máquina virtual de olá onde serão recolhidos os ficheiros.
* **SearchPattern**: padrão de Olá Olá de nomes de toobe ficheiros recolhidos. Predefinição é "*"
* **Recursiva**: se os ficheiros de Olá serão recolhido recursivamente na pasta Olá.

## <a name="prerequisites"></a>Pré-requisitos
* É necessário toohave uma conta de armazenamento para ficheiros de zip toosave gerado de extensão.
* Tem de se certificar de que está a utilizar o Azure PowerShell Cmdlets V0.8.0 ou superior. Para obter mais informações, consulte [Azure transfere](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Adicionar extensão de Olá
Pode utilizar [do Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets ou [APIs REST do serviço de gestão](https://msdn.microsoft.com/library/ee460799.aspx) tooadd Olá AzureLogCollector extensão.

Para serviços em nuvem, Olá cmdlet do Powershell do Azure existente, **conjunto AzureServiceExtension**, podem ser utilizados tooenable Olá extensão instâncias de função de serviço em nuvem. Sempre que esta extensão é ativada através deste cmdlet, a recolha de registos é acionada Olá selecionado instâncias de função dos direitos selecionados.

Para máquinas virtuais, Olá cmdlet do Powershell do Azure existente, **conjunto AzureVMExtension**, podem ser utilizados tooenable Olá extensão em máquinas virtuais. Sempre que esta extensão é ativada através de cmdlets do Olá, recolha de registos é acionada em cada instância.

Internamente, esta extensão utiliza Olá PublicConfiguration baseados em JSON e PrivateConfiguration. Olá que se segue esquema Olá de uma amostra JSON para a configuração pública e privada.

### <a name="publicconfiguration"></a>PublicConfiguration
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

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> Esta extensão não necessita de **privateConfiguration**. Apenas pode fornecer uma estrutura vazia para Olá **– PrivateConfiguration** argumento.
> 
> 

Pode seguir um Olá dois os seguintes passos tooadd Olá AzureLogCollector tooone ou mais instâncias de um serviço em nuvem ou Máquina Virtual dos direitos selecionados, os acionadores Olá coleções em cada VM toorun e enviam ficheiros Olá recolhido tooAzure conta especificado.

## <a name="adding-as-a-service-extension"></a>Adicionar como uma extensão de serviço
1. Siga a subscrição de tooyour Olá instruções tooconnect Azure PowerShell.
2. Especifique o nome do serviço Olá, ranhura, funções e toowhich de instâncias de função que pretende tooadd e ativar a extensão de AzureLogCollector Olá.
   
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
3. Especificar a pasta de dados adicionais de Olá para os quais serão recolhidos os ficheiros (este passo é opcional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > Pode utilizar o token `%roleroot%` unidade de raiz de função do toospecify Olá, uma vez que não utiliza uma unidade fixa.
   > 
   > 
4. Forneça o nome da conta de armazenamento do Azure Olá e ficheiros de chave toowhich recolhido serão carregados.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Chamada Olá SetAzureServiceLogCollector.ps1 (incluído no fim de Olá do artigo Olá) como extensão do modo tooenable Olá AzureLogCollector para um serviço em nuvem. Depois de concluída a execução de Olá, pode encontrar o ficheiro Olá carregado em`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

Olá segue-se a definição de Olá dos parâmetros de Olá transmitido toohello script. (Isto é copiado abaixo, bem como.)

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

* *ServiceName*: O nome do serviço em nuvem.
* *Funções*: uma lista de funções, tais como "WebRole1" ou "WorkerRole1".
* *Instâncias*: uma lista de nomes de Olá de instâncias de função separados por vírgulas – utilizar a cadeia de carateres universais Olá ("*") para todas as instâncias de função.
* *Ranhura*: nome da ranhura. "Production" ou "Transição".
* *Modo*: modo da coleção. "Completo" ou "GA".
* *StorageAccountName*: recolhidos de conta de armazenamento do nome do Azure para armazenar dados.
* *StorageAccountKey*: a chave de conta de armazenamento de nome do Azure.
* *AdditionalDataLocationList*: uma lista de Olá seguir a estrutura:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Adicionar como uma extensão VM
Siga a subscrição de tooyour Olá instruções tooconnect Azure PowerShell.

1. Especifique o nome do serviço Olá, VM e modo da coleção Olá.
   
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
2. Forneça o nome da conta de armazenamento do Azure Olá e ficheiros de chave toowhich recolhido serão carregados.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Chamada Olá SetAzureVMLogCollector.ps1 (incluído no fim de Olá do artigo Olá) como extensão do modo tooenable Olá AzureLogCollector para um serviço em nuvem. Depois de concluída a execução de Olá, pode encontrar o ficheiro Olá carregado em https://YouareStorageAccountName.blob.core.windows.net/vmlogs

Olá segue-se a definição de Olá dos parâmetros de Olá transmitido toohello script. (Isto é copiado abaixo, bem como.)

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

* ServiceName: O nome do serviço cloud.
* VMName Olá nome Olá VM.
* Modo: Modo de coleção. "Completo" ou "GA".
* StorageAccountName: O nome da conta de armazenamento do Azure para armazenar os dados recolhidos.
* StorageAccountKey: Nome da chave de conta de armazenamento do Azure.
* AdditionalDataLocationList: Uma lista de Olá seguir a estrutura:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>Ficheiros de Script do PowerShell de extensão
SetAzureServiceLogCollector.ps1

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


SetAzureVMLogCollector.ps1

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

## <a name="next-steps"></a>Passos Seguintes
Agora pode examinar ou copiar os registos de uma localização muito simple.

