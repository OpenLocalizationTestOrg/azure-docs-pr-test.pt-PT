# <a name="azure-managed-disks-overview"></a>Descrição geral de discos gerida do Azure

Discos gerida do Azure simplifica a gestão de discos para VMs IaaS do Azure ao gerir Olá [contas do storage](../articles/storage/common/storage-introduction.md) associadas aos discos VM Olá. Tem o tipo de Olá toospecify apenas ([Premium](../articles/storage/common/storage-premium-storage.md) ou [padrão](../articles/storage/common/storage-standard-storage.md)) e Olá tamanho do disco tem e o Azure cria e gere o disco de Olá por si.

## <a name="benefits-of-managed-disks"></a>Benefícios dos discos geridos

Vamos ver alguns dos benefícios de Olá obtém ao utilizar discos geridos, começando neste vídeo no Channel 9, [melhor resiliência de VM do Azure com discos geridos](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency).
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>Implementação da VM Simple e dimensionável

Gerida armazenamento de identificadores de discos em segundo plano de Olá. Anteriormente, era necessário toocreate contas toohold Olá discos do armazenamento do (ficheiros. VHD) para as suas VMs do Azure. Quando como aumentar verticalmente, tinha toomake se criada mais contas do storage, pelo que não tenha a exceder o limite IOPS de Olá para armazenamento com qualquer um dos seus discos. Com os discos geridos processamento de armazenamento, já não são limitados por Olá limites de conta de armazenamento (por exemplo, o 20.000 IOPS / conta). Também já não tiver toocopy as contas do storage toomultiple imagens personalizadas (ficheiros. VHD). Pode geri-los numa localização central – uma conta do storage por região do Azure – e utilizá-los toocreate centenas de VMs numa subscrição.

Discos geridos permitirá toocreate segurança too10, 000 VM **discos** numa subscrição, que permitirá toocreate milhares de **VMs** numa única subscrição. Esta funcionalidade também aumenta a escalabilidade de Olá de [conjuntos de dimensionamento da Máquina Virtual (VMSS)](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) , permitindo-lhe toocreate tooa milhares VMS num VMSS utilizando uma imagem do Marketplace.

### <a name="better-reliability-for-availability-sets"></a>Melhor fiabilidade para conjuntos de disponibilidade

Discos geridos fornece melhor fiabilidade para conjuntos de disponibilidade, garantindo que Olá discos [VMs num conjunto de disponibilidade](../articles/virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) são suficientemente isolado de si tooavoid pontos únicos de falha. Este é automaticamente colocando discos Olá em unidades de escala de armazenamento diferente (carimbos de data /). Se um carimbo falhar devido a falha de toohardware ou de software, apenas instâncias de VM Olá com discos os carimbos de data / falharem. Por exemplo, vamos supor que tem uma aplicação em execução em cinco VMs e Olá VMs estão num conjunto de disponibilidade. Olá discos para essas VMs não todas ser armazenados no Olá mesmo carimbo, pelo que o se um carimbo ficar inativo, hello outras instâncias da aplicação Olá continuam toorun.

### <a name="highly-durable-and-available"></a>Elevada disponibilidade e durabilidade

Os Discos do Azure foram concebidos para garantir uma disponibilidade de 99,999%. REST mais fácil sabendo que tem três réplicas dos dados que permite elevada durabilidade. Se uma ou até duas réplicas problemas, o réplicas restantes Olá ajudam a garantir a persistência dos seus dados e a elevada tolerância contra falhas. Esta arquitetura tem ajudado o Azure a garantir de forma consistente uma durabilidade de nível empresarial para discos IaaS, com uma Taxa de Falhas Anual de ZERO% líder da indústria. 

### <a name="granular-access-control"></a>Controlo de acesso granulares

Pode utilizar [controlo de acesso em funções do Azure (RBAC)](../articles/active-directory/role-based-access-control-what-is.md) tooassign permissões específicas para um disco gerido tooone ou mais utilizadores. Gerido discos expõe uma variedade de operações, incluindo de leitura, escrita (criar/atualizar), eliminar e obter um [assinatura de acesso partilhado (SAS) URI](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md) para disco Olá. Pode conceder acesso tooonly Olá operações que necessita de uma pessoa tooperform a tarefa. Por exemplo, se não quiser toocopy uma pessoa uma conta de armazenamento do disco gerido tooa, pode escolher não toogrant acesso toohello exportação ação para esse disco gerido. Da mesma forma, se não quiser toouse uma pessoa toocopy um URI de SAS um disco gerido, pode escolher não toogrant toohello essa permissão disco gerido.

### <a name="azure-backup-service-support"></a>Suporte do serviço de cópia de segurança do Azure
Utilize o serviço de cópia de segurança do Azure com discos geridos toocreate uma tarefa de cópia de segurança com políticas de retenção de cópias de segurança, fácil restauro de VM e cópias de segurança baseados no tempo. Discos geridos só suportam localmente redundante armazenamento (LRS) como opção de replicação de Olá; Isto significa que mantém três cópias dos dados de Olá numa única região. Recuperação de desastres regionais, deve efetuar cópias de segurança aos discos VM numa região diferente através de [serviço cópia de segurança do Azure](../articles/backup/backup-introduction-to-azure-backup.md) e uma conta de armazenamento GRS como o Cofre de cópia de segurança. Cópia de segurança do Azure suporta atualmente os tamanhos de disco de dados se too1TB para cópia de segurança. Saiba mais sobre no [serviço utilizando a cópia de segurança do Azure para as VMs com discos geridos](../articles/backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="pricing-and-billing"></a>Preços e Faturação

Ao utilizar discos geridos, aplique Olá seguintes considerações de faturação:
* Tipo de armazenamento

* Tamanho do Disco

* Número de transações

* Transferências de dados de saída

* Gerido instantâneos de discos (cópia de disco completo)

Vamos um olhar estes.

**Tipo de armazenamento:** discos geridos oferece 2 escalões de desempenho: [Premium](../articles/storage/common/storage-premium-storage.md) (baseadas em SSD) e [padrão](../articles/storage/common/storage-standard-storage.md) (baseado em HDD). Faturação Olá de um disco gerido depende de qual o tipo de armazenamento que selecionou para o disco de Olá.


**Tamanho do disco**: faturação para discos geridos depende Olá aprovisionado do tamanho do disco de Olá. Azure maps Olá toohello aprovisionado tamanho (arredondar por excesso) mais próximo da opção de discos geridos conforme especificado nas tabelas de Olá abaixo. Cada tooone de mapas de disco gerido de Olá suportado tamanhos aprovisionados e é faturada em conformidade. Por exemplo, se criar um disco gerido standard e especificar um tamanho de aprovisionamento de 200 GB, é-lhe cobrada de acordo com Olá preços de Olá tipo de disco S20.

Seguem-se disponível para um disco gerido premium tamanhos de disco Olá:

| **Premium gerido <br>tipo de disco** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| Tamanho do Disco        | 32 GB   | 64 GB   | 128 GB  | 512 GB  | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


Seguem-se disponível para um disco gerido standard tamanhos de disco Olá:

| **Standard gerido <br>tipo de disco** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| Tamanho do Disco        | 32 GB   | 64 GB   | 128 GB | 512 GB | 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 


**Número de transações**: É Faturado por número de Olá de transações que efetuar um disco gerido standard. Não há sem qualquer custo para transações para um disco gerido premium.

**Transferências de dados de saída**: [transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/) (dados ficar fora de centros de dados do Azure) cobrança para utilização de largura de banda.

Para obter informações detalhadas sobre os preços para discos geridos, consulte [geridos discos preços](https://azure.microsoft.com/pricing/details/managed-disks).


## <a name="managed-disk-snapshots"></a>Disco gerido instantâneos

Um instantâneo gerido é uma cópia completa de só de leitura de um disco gerida que é armazenado como um disco gerido standard por predefinição. Com instantâneos, pode criar cópias de segurança aos discos geridos em qualquer ponto no tempo. Estes instantâneos existem independentes do disco de origem Olá e podem ser utilizado toocreate novos discos geridos. Estes são cobrados com base no tamanho Olá utilizado. Por exemplo, se criar um instantâneo de um disco gerido com capacidade de aprovisionamento de 64 GB e o tamanho de dados utilizados real de 10 GB, instantâneo será faturado apenas para Olá utilizado o tamanho de dados de 10 GB.  

[Instantâneos incrementais](../articles/virtual-machines/windows/incremental-snapshots.md) não são atualmente suportadas para discos geridos, mas será suportada em Olá futura.

toolearn mais sobre como instantâneos de toocreate com discos geridos, consulte estes recursos:

* [Criar uma cópia de um VHD armazenado como Disco Gerido com os Instantâneos no Windows](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Criar uma cópia de um VHD armazenado como Disco Gerido com os Instantâneos no Linux](../articles/virtual-machines/windows/snapshot-copy-managed-disk.md)


## <a name="images"></a>Imagens

Discos geridos também suportam a criação de uma imagem personalizada gerida. Pode criar uma imagem do seu VHD personalizado em contas de armazenamento ou diretamente a partir de uma VM (sys prepped) generalizada. Isto captura numa única imagem gerido todos os discos associados uma VM, incluindo Olá SO e discos de dados. Este permite criar centenas de VMs com a sua imagem personalizada sem Olá precisa toocopy ou gerir as contas de armazenamento.

Para obter informações sobre a criação de imagens, consulte Olá seguintes artigos:
* [Como toocapture uma imagem gerida de uma VM generalizada no Azure](../articles/virtual-machines/windows/capture-image-resource.md)
* [Como toogeneralize e capturar uma máquina virtual do Linux utilizando Olá Azure CLI 2.0](../articles/virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>Imagens versus instantâneos

Muitas vezes, verá word Olá "imagem" utilizada com as VMs e agora ver "instantâneos" bem. É importante toounderstand diferença de Olá entre estes. Com os discos geridos, pode demorar uma imagem de uma VM generalizada que tenha sido anulada. Esta imagem irá incluir todos os discos ligados de Olá toohello VM. Pode utilizar esta imagem toocreate uma nova VM e incluirá todos os discos de Olá.

Um instantâneo é uma cópia de um disco em Olá ponto no tempo que é executada. Só se aplica tooone disco. Se tiver uma VM que tem apenas um disco (Olá SO), pode tirar um instantâneo ou uma imagem do mesmo e criar uma VM a partir do instantâneo Olá ou imagem Olá.

E se uma VM tem cinco discos e estão repartidas? Poderá tirar um instantâneo de cada um dos discos de Olá, mas não existe nenhum deteção dentro Olá VM do Estado de Olá dos discos de Olá – instantâneos Olá conhecer apenas se um disco. Neste caso, os instantâneos de Olá teria toobe coordenado entre si e que não é atualmente suportado.

## <a name="managed-disks-and-encryption"></a>Discos geridos e encriptação

Existem dois tipos de encriptação toodiscuss toomanaged dos discos de referência. Olá primeiro um é armazenamento serviço encriptação (SSE), que é efetuada pelo serviço de armazenamento Olá. Olá segundo é Azure Disk Encryption, que pode ativar no Olá SO e discos de dados para as suas VMs.

### <a name="storage-service-encryption-sse"></a>Encriptação do serviço de armazenamento (SSE)

[Encriptação do serviço de armazenamento do Azure](../articles/storage/common/storage-service-encryption.md) fornece encriptação em rest e salvaguardar o dados toomeet os compromissos de segurança e conformidade organizacionais. SSE está ativada por predefinição para todos os discos geridos, instantâneos e imagens em todas as regiões de olá onde discos geridos está disponível. A partir de 10 de Junho de 2017, todos os novos geridos instantâneos/discos/imagens e novos dados escritos tooexisting gerido discos são automaticamente encriptados-em-rest com chaves geridas pela Microsoft.  Visite Olá [página de FAQ de discos geridos](../articles/virtual-machines/windows/faq-for-disks.md#managed-disks-and-storage-service-encryption) para obter mais detalhes.


### <a name="azure-disk-encryption-ade"></a>Encriptação de disco do Azure (ADE)

Encriptação de disco do Azure permite-lhe tooencrypt Olá SO e discos de dados utilizados pela máquina Virtual IaaS. A lista inclui discos geridos. Para o Windows, Olá unidades são encriptadas utilizando a tecnologia de encriptação do BitLocker de norma da indústria. Para Linux, discos Olá são encriptados utilizando a tecnologia de Olá DM-Crypt. Este é integrado com o Cofre de chaves do Azure tooallow toocontrol e gerir chaves de encriptação de disco Olá. Para obter mais informações, consulte [encriptação de disco do Azure para Windows e as VMs de IaaS Linux](../articles/security/azure-security-disk-encryption.md).

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre discos geridos, consulte toohello seguintes artigos.

### <a name="get-started-with-managed-disks"></a>Introdução aos Discos Geridos

* [Criar uma VM com o Resource Manager e o PowerShell](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm.md)

* [Criar uma VM com Linux utilizando Olá Azure CLI 2.0](../articles/virtual-machines/linux/quick-create-cli.md)

* [Anexar um tooa de disco de dados geridos VM do Windows com o PowerShell](../articles/virtual-machines/windows/attach-disk-ps.md)

* [Adicionar um disco gerido de tooa VM com Linux](../articles/virtual-machines/linux/add-disk.md)

* [Gerido Scripts de exemplo do PowerShell de discos](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Utilizar discos geridos na modelos Azure Resource Manager](../articles/virtual-machines/windows/using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Comparar as opções de armazenamento de discos geridos

* [Armazenamento Premium e discos](../articles/storage/common/storage-premium-storage.md)

* [Armazenamento padrão e discos](../articles/storage/common/storage-standard-storage.md)

### <a name="operational-guidance"></a>Orientação operacional

* [Migrar a partir do AWS e outras plataformas tooManaged discos no Azure](../articles/virtual-machines/windows/on-prem-to-azure.md)

* [Converta os discos de toomanaged VMs do Azure no Azure](../articles/virtual-machines/windows/migrate-to-managed-disks.md)
