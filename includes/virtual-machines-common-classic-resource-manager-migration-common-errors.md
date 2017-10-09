# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Erros comuns durante clássico tooAzure migração do Gestor de recursos
Este catálogos de artigo hello mais comuns e mitigações de erros durante a migração de Olá dos recursos IaaS da pilha de Gestor de recursos do Azure de toohello de modelo de implementação clássico do Azure.

## <a name="list-of-errors"></a>Lista de erros
| Cadeia do erro | Mitigação |
| --- | --- |
| Erro de servidor interno |Em alguns casos, este é um erro transitório que desaparece com uma nova tentativa. Se as prossegue toopersist, [contacte o suporte do Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) como necessita de investigação de registos de plataforma. <br><br> **Nota:** depois de incidente Olá é controlada pela equipa de suporte de Olá, não tente qualquer mitigação automática, esta poderá ter consequências inesperadas no seu ambiente. |
| A migração não é suporta na Implementação {deployment-name} em HostedService {hosted-service-name}, porque é uma implementação de PaaS (função da Web/Trabalho). |Isto acontece quando uma implementação contém uma função da Web/trabalho. Uma vez que a migração só é suportada para máquinas virtuais, remova a função de web/trabalho Olá da implementação de Olá e repita a migração. |
| Falha na implementação de modelo {template-name}. CorrelationId={guid} |Backend Olá do serviço de migração, utilizamos recursos do Azure Resource Manager modelos toocreate na pilha do Olá do Azure Resource Manager. Uma vez que os modelos são idempotent, normalmente, pode em segurança repetir Olá tooget de operação de migração anteriores este erro. Se este erro persistir toopersist, [contacte o suporte do Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) e conceder-lhes Olá CorrelationId. <br><br> **Nota:** depois de incidente Olá é controlada pela equipa de suporte de Olá, não tente qualquer mitigação automática, esta poderá ter consequências inesperadas no seu ambiente. |
| rede virtual de Olá {--nome de rede virtual} não existe. |Isto pode acontecer se tiver criado Olá rede Virtual no novo portal do Azure Olá. nome de rede Virtual real Olá segue o padrão de Olá "grupo * <VNET name>" |
| A VM {vm-name} em HostedService {hosted-service-name} contém a Extensão {extension-name}, que o Azure Resource Manager não suporta. Recomenda-se toouninstall a Olá VM antes de continuar com a migração. |O Azure Resource Manager suporta extensões XML, como BGInfo 1.*. Por conseguinte, estas extensões não podem ser migradas. Se estas extensões estão esquerdo Olá instalado na máquina, são automaticamente desinstaladas antes de concluir a migração de Olá. |
| A VM {vm-name} em HostedService {hosted-service-name} contém a Extensão VMSnapshot/VMSnapshotLinux, que não é suportada, atualmente, para Migração. Desinstale-a da VM de Olá e adicioná-la novamente utilizando o Azure Resource Manager depois Olá migração está concluída |Este é o cenário de olá onde a máquina virtual de Olá está configurada para cópia de segurança do Azure. Uma vez que esta é atualmente um cenário não suportado, siga solução Olá em https://aka.ms/vmbackupmigration |
| VM {nome da vm} em HostedService {alojado--nome do serviço} contém a extensão {nome da extensão} cujo estado não está a ser reportado de Olá VM. Por este motivo, esta VM não pode ser migrada. Certifique-se de que Olá estado da extensão está a ser reportado ou desinstalar a extensão de Olá Olá VM e repita a migração. <br><br> A VM {vm-name} em HostedService {hosted-service-name} contém a Extensão {extension-name}, que reporta o Estado do Processador: {handler-status}. Por conseguinte, não pode ser migrada Olá VM. Certifique-se de que o estado de processador de extensão de Olá reportado é {processador-status} ou desinstale-a da Olá VM e repita a migração. <br><br> Relatório de agente da VM para VM {nome da vm} em HostedService {alojado--nome do serviço} Olá estado geral de agente como não preparada. Por conseguinte, Olá VM poderá não ser migrado, se tiver uma extensão pode ser migrada. Certifique-se de que Olá agente da VM está a comunicar o estado geral de agente como pronta. Consulte toohttps://aka.ms/classiciaasmigrationfaqs. |O agente convidado do Azure & extensões de VM necessário toopopulate de conta de armazenamento VM à internet acesso toohello saída respetivo estado. As causas comuns das falhas de estado incluem <li> um grupo de segurança de rede que bloqueia o acesso de saída toohello internet <li> Se Olá VNET tiver servidores DNS no local e a conectividade DNS está perdido <br><br> Se continuar toosee um Estado não suportado, pode desinstalar Olá extensões tooskip esta verificação e avançar com a migração. |
| A migração não é suporta na Implementação {deployment-name} em HostedService {hosted-service-name}, porque tem vários Conjuntos de Disponibilidade. |Atualmente, só podem ser migrados serviços alojados que tenham um ou menos Conjuntos de Disponibilidade. toowork em torno este problema, mova Olá adicional conjuntos de disponibilidade e o serviço alojado de máquinas virtuais nesses tooa de conjuntos de disponibilidade diferente. |
| Migração não é suportada para a implementação {nome da implementação} em HostedService {alojado--nome do serviço porque tem VMs que não fazem parte do conjunto de disponibilidade de Olá, apesar de Olá HostedService contém uma. |solução de Olá para este cenário é tooeither mover todas as máquinas de virtuais Olá para um único disponibilidade definir ou remover todas as máquinas virtuais Olá que conjunto de disponibilidade no serviço de Olá alojado. |
| Conta de armazenamento/HostedService/Virtual rede {--nome de rede virtual} está em curso Olá de ser migrada e, por conseguinte, não pode ser alterada |Este erro ocorre quando Olá "Preparar" operação de migração foi concluída no recurso de Olá e uma operação que iria tornar um recurso de toohello de alteração é acionada. Devido a bloqueio Olá plane de gestão de Olá após a operação de "Preparar", a qualquer recurso de toohello de alterações estão bloqueadas. plane de gestão do toounlock Olá, pode executar Olá "Consolidar" migração operação toocomplete migração ou a operação "Preparar" Olá, Olá "Abortar" migração operação tooroll novamente. |
| A migração não é permitida em HostedService {hosted-service-name}, porque a VM {vm-name} do mesmo tem o Estado: RoleStateUnknown. A migração é permitida apenas quando Olá VM se encontra dos seguintes Olá Estados - em execução, parada, parado Desalocada. |Olá VM poderá estar sob através de uma transição de estado, o que normalmente acontece quando durante uma operação de atualização no Olá HostedService como um reinício, instalação da extensão etc. É recomendado para Olá toocomplete de operação de atualização no Olá HostedService antes de tentar a migração. |
| Implementação {nome da implementação} em HostedService {alojado--nome do serviço} contém uma VM {nome da vm} com o disco de dados {nome de disco de dados} cujos tamanho {size-of-the-vhd-blob-backing-the-data-disk} em bytes blob físico não corresponde ao {de tamanho lógico de disco de dados de VM Olá total de bytes size-of-the-data-Disk-specified-in-the-VM-API}. Migração irá continuar sem especificar um tamanho de disco de dados de Olá para Olá VM do Azure Resource Manager. | Este erro ocorre se tiver redimensionado blob VHD Olá sem atualizar o tamanho de Olá no modelo de VM API Olá. Os passos de mitigação detalhados estão descritos [abaixo](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|
| Ocorreu uma exceção de armazenamento ao validar o disco de dados {data disk name} com a ligação de multimédia {data disk Uri} para a VM {VM name} no Serviço Cloud {Cloud Service name}. Certifique-se que dessa ligação de suporte de dados VHD Olá está acessível para esta máquina virtual | Este erro pode acontecer se discos Olá Olá VM ter sido eliminada ou não está acessível já. Certifique-se Olá discos para Olá VM existe.|
| A VM {vm-name} em HostedService {cloud-service-name} contém o Disco com a Ligação de Multimédia {vhd-uri}, que tem o nome de blob {vhd-blob-name}, o qual não é suportado no Azure Resource Manager. | Este erro ocorre quando o nome de Olá do blob Olá tem um "/" no mesmo que não é suportada no fornecedor de recursos de computação atualmente. |
| Migração não é permitida para a implementação {nome da implementação} em HostedService {nome de serviço de nuvem}, porque não se encontra no âmbito regional Olá. Consulte toohttp://aka.ms/regionalscope para mover este âmbito de tooregional de implementação. | Em 2014, o Azure anunciou a que os recursos de rede irão mover de um âmbito de tooregional de nível de âmbito do cluster. Veja [http://aka.ms/regionalscope] para obter mais detalhes (http://aka.ms/regionalscope). Este erro ocorre quando a implementação de Olá a ser migrada não tenha tido uma operação de atualização, move-automaticamente o âmbito regional tooa. Melhor solução é tooeither adicionar um ponto final tooa VM ou dados de um disco toohello VM e, em seguida, repita a migração. <br> Consulte [como tooset dos pontos finais na máquina virtual clássico do Windows no Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) ou [anexar dados disco tooa máquina virtual do Windows criada com o modelo de implementação clássica Olá](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Mitigações detalhadas

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>VM com o disco de dados cujo físico blob tamanho em bytes não corresponde ao hello disco de dados de VM lógica tamanho em bytes.

Isto acontece quando hello tamanho lógico de disco de dados pode obter sincronizado com o tamanho do blob de VHD Olá real. Isto pode ser facilmente verificado através de Olá os seguintes comandos:

#### <a name="verifying-hello-issue"></a>Verificar o problema de Olá

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Problema de Olá mitigar

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Mover VM tooa outra subscrição depois de concluir a migração

Depois de concluir o processo de migração de Olá, poderá pretender subscrição de tooanother toomove Olá VM. No entanto, se tiver um segredo/certificado Olá VM que faça referência a um recurso do Cofre de chaves, hello mover não é atualmente suportada. Olá abaixo instruções permitirá problema de Olá tooworkaround. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>CLI 2.0 do Azure

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
