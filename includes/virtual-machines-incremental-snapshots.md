# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Criar cópias de segurança do Azure discos VM não geridos com instantâneos incrementais
## <a name="overview"></a>Descrição geral
Armazenamento do Azure fornece a capacidade de Olá tootake instantâneos de blobs. Instantâneos capturam o estado de blob Olá neste ponto no tempo. Neste artigo, vamos descrever um cenário em que pode manter cópias de segurança dos discos da máquina virtual através de instantâneos. Pode utilizar este metodologia quando optar por não toouse cópia de segurança do Azure e o serviço de recuperação e desejar toocreate uma estratégia de cópia de segurança personalizada para os discos da máquina virtual.

Discos de máquina virtual do Azure são armazenados como blobs de páginas no armazenamento do Azure. Uma vez que vamos são que descrevem uma estratégia de cópia de segurança para os discos da máquina virtual neste artigo, vamos Consulte toosnapshots no contexto de Olá de blobs de páginas. toolearn mais informações sobre instantâneos, consulte demasiado[criar um instantâneo de um Blob](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

## <a name="what-is-a-snapshot"></a>O que é um instantâneo?
Um instantâneo do blob é uma versão só de leitura de um blob que é capturada num ponto no tempo. Assim que tiver sido criado um instantâneo,-lo pode ser ler, copiar, ou eliminada, mas não modificado. Os instantâneos proporcionar uma tooback de forma a segurança de um blob como é apresentado um momento. Até REST versão 2015-04-05, era necessário instantâneos do Olá capacidade toocopy completa. Com Olá REST versão 2015-07-08 e superior, também pode copiar instantâneos incrementais.

## <a name="full-snapshot-copy"></a>Cópia de instantâneo completo
Instantâneos podem ser copiados tooanother conta de armazenamento como um cópias de segurança do blob tookeep do blob base Olá. Também pode copiar um instantâneo ao longo do respetivo blob base, o que é como restaurar Olá blob tooan versão anterior. Quando um instantâneo é copiado a partir de um tooanother de conta de armazenamento, ocupar Olá mesmo espaço como blob de página base Olá. Por conseguinte, copiar todo instantâneos de um tooanother de conta de armazenamento está lento e consome espaço na conta de armazenamento de destino Olá.

> [!NOTE]
> Se copiar o destino de tooanother de base blob Olá, Olá os instantâneos de blob Olá não são copiados, juntamente com o mesmo. Da mesma forma, se substituir um blob base com uma cópia, instantâneos associados blob base Olá não são afetados e permanecem intactos sob o nome do base blob Olá.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Criar cópias de segurança utilizando instantâneos de discos
Como uma estratégia de cópia de segurança para os discos da máquina virtual, pode criar periódicos instantâneos do blob de página ou disco Olá e copiá-los utilizando ferramentas como conta de armazenamento de tooanother [copiar Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) operação ou [AzCopy](../articles/storage/common/storage-use-azcopy.md). Pode copiar um blob de página de destino do instantâneo tooa com um nome diferente. blob de página de destino Olá resultante é um blob de página gravável e não um instantâneo. Neste artigo, vamos descrever cópias de segurança do passos tootake dos discos da máquina virtual através de instantâneos.

### <a name="restore-disks-using-snapshots"></a>Restaurar utilizando instantâneos de discos
Quando for toorestore tempo tooa seu disco estável versão que foram capturado anteriormente dos instantâneos de cópia de segurança de Olá, pode copiar um instantâneo através de blob de página base Olá. Após o instantâneo de Olá toohello promovida blob de página base, Olá instantâneo permanece, mas a origem é substituída por uma cópia que pode ser de leitura e escrita. Neste artigo, vamos descrevem passos toorestore uma versão anterior do disco do respetivo instantâneo.

### <a name="implementing-full-snapshot-copy"></a>Implementar a cópia de instantâneo completo
Pode implementar uma cópia completa de instantâneo efetuando o seguinte Olá,

* Em primeiro lugar, tire um instantâneo do blob base Olá utilizando Olá [instantâneo Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) operação.
* Em seguida, copiar Olá instantâneo tooa destino armazenamento conta utilizando [copiar Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob).
* Repita este processo toomaintain cópia de segurança cópias o blob de base.

## <a name="incremental-snapshot-copy"></a>Cópia de instantâneo incremental
funcionalidade nova do Olá do Olá [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) API fornece um muito tooback forma uma melhor segurança instantâneos Olá dos seus blobs de páginas ou discos. Olá API devolve Olá lista de alterações entre blob base Olá e instantâneos de Olá, que reduz a quantidade de Olá de espaço de armazenamento numa conta Olá de cópia de segurança. Olá API suporta blobs de páginas no armazenamento Premium, bem como o armazenamento Standard. Utilizar esta API, pode criar soluções de cópia de segurança mais rápidas e eficientes para VMs do Azure. Esta API será disponíveis Olá REST versão 2015-07-08 e planos superiores.

Cópia de instantâneo incremental permite-lhe toocopy de um armazenamento conta tooanother Olá diferença entre,

* Base blob e o respetivo instantâneo ou um
* Todos os instantâneos do blob base Olá dois

Olá fornecido seguintes condições são cumpridos,

* blob Olá foi criado no Jan-1-2016 ou posterior.
* blob Olá não foi substituído pela [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) ou [copiar Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) entre duas instantâneos.

**Tenha em atenção**: esta funcionalidade está disponível para Blobs de página do Azure Standard e Premium.

Quando tiver uma estratégia de cópia de segurança personalizada através de instantâneos, copiar instantâneos Olá um tooanother de conta de armazenamento pode ser lenta e pode consumir muito espaço de armazenamento. Em vez de copiar conta de armazenamento de cópia de segurança de tooa de instantâneo completo de Olá, pode escrever diferença Olá entre BLOBs de páginas de cópia de segurança de tooa de instantâneos consecutivos. Desta forma, Olá tempo toocopy Olá espaço toostore cópias de segurança e é reduzido.

### <a name="implementing-incremental-snapshot-copy"></a>Implementar a cópia de instantâneo Incremental
Pode implementar a cópia de instantâneo incremental efetuando o seguinte Olá,

* Tirar um instantâneo da utilização de base blob Olá [instantâneo Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob).
* Cópia Olá instantâneo toohello destino armazenamento de cópia de segurança conta utilizando [copiar Blob](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob). Este é o blob de páginas de cópia de segurança de Olá. Tirar um instantâneo de BLOBs de páginas de cópia de segurança de Olá e armazene-o numa conta Olá de cópia de segurança.
* Crie outro instantâneo de blob base Olá utilizando o Blob de instantâneo.
* Obter a diferença de Olá entre os instantâneos de primeiro e segundo Olá de utilizar o base blob Olá [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges). Utilize o parâmetro novo Olá **prevsnapshot**, toospecify Olá de instantâneo Olá pretende diferença de Olá tooget com o valor DateTime. Quando este parâmetro estiver presente, Olá resposta REST inclui apenas Olá as páginas que foram alteradas entre os instantâneos de destino e instantâneo anterior, incluindo páginas encriptadas.
* Utilize [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) tooapply blob de página de cópia de segurança de toohello estas alterações.
* Por fim, tire um instantâneo de BLOBs de páginas de cópia de segurança de Olá e armazene-o numa conta de armazenamento de cópia de segurança de Olá.

Na secção seguinte, Olá, iremos descrevem com maior detalhe como pode manter as cópias de segurança de discos utilizando a cópia de instantâneo Incremental

## <a name="scenario"></a>Cenário
Nesta secção, iremos descrevem um cenário que envolva uma estratégia de cópia de segurança personalizada para os discos da máquina virtual através de instantâneos.

Considere uma VM do Azure-série DS com o premium storage P30 disco ligado. disco Olá P30 chamado *mypremiumdisk* são armazenados numa conta de armazenamento premium chamada *mypremiumaccount*. Uma conta de armazenamento standard denominada *mybackupstdaccount* é utilizado para armazenar a cópia de segurança de Olá de *mypremiumdisk*. Gostaríamos tookeep um instantâneo de *mypremiumdisk* cada 12 horas.

toolearn sobre a criação de conta de armazenamento e discos, consulte demasiado[contas do storage do Azure sobre](../articles/storage/storage-create-storage-account.md).

toolearn sobre a cópia de segurança de VMs do Azure, consulte demasiado[cópias de segurança de VM do Azure planear](../articles/backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Cópias de segurança do passos toomaintain de um disco através de instantâneos de incrementais
Olá passos seguintes descrevem como instantâneos de tootake de *mypremiumdisk* e manter cópias de segurança de Olá no *mybackupstdaccount*. Olá cópia de segurança é um blob de página padrão chamado *mybackupstdpageblob*. Olá BLOBs de páginas de cópia de segurança sempre refletem Olá mesmo estado como Olá último instantâneo *mypremiumdisk*.

1. Criar um instantâneo de BLOBs de páginas de cópia de segurança de Olá para o disco de armazenamento premium, *mypremiumdisk* chamado *mypremiumdisk_ss1*.
2. Copie esta toomybackupstdaccount de instantâneo como um blob de página chamado *mybackupstdpageblob*.
3. Tirar um instantâneo *mybackupstdpageblob* chamado *mybackupstdpageblob_ss1*com [instantâneo Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) e armazená-la no *mybackupstdaccount*.
4. Durante a janela de cópia de segurança Olá, crie outro instantâneo de *mypremiumdisk*, diga *mypremiumdisk_ss2*e armazená-la no *mypremiumaccount*.
5. Obter as alterações incrementais Olá entre instantâneos Olá dois, *mypremiumdisk_ss2* e *mypremiumdisk_ss1*com [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) no  *mypremiumdisk_ss2* com Olá **prevsnapshot** toohello timestamp do conjunto de parâmetros *mypremiumdisk_ss1*. Escrita de BLOBs de página de cópia de segurança de toohello estas alterações incrementais *mybackupstdpageblob* no *mybackupstdaccount*. Se existirem intervalos eliminados alterações incrementais Olá, tem de ser limpo a partir do blob de página de cópia de segurança de Olá. Utilize [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) blob de página de cópia de segurança de toohello do toowrite alterações incrementais.
6. Tirar um instantâneo de BLOBs de páginas de cópia de segurança de Olá *mybackupstdpageblob*, chamado *mybackupstdpageblob_ss2*. Eliminar instantâneo anterior Olá *mypremiumdisk_ss1* da conta de armazenamento premium.
7. Repita os passos 4 a 6 cada janela de cópia de segurança. Desta forma, pode manter as cópias de segurança de *mypremiumdisk* numa conta do standard storage.

![Cópia de segurança disco utilizando instantâneos de incrementais](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Passos toorestore um disco de instantâneos
Olá, os seguintes passos, que descrevem como toorestore Olá disco premium, *mypremiumdisk* tooan anteriormente instantâneo da conta de armazenamento de cópia de segurança de Olá *mybackupstdaccount*.

1. Identifique Olá ponto no tempo que pretende toorestore Olá premium disco. Digamos que é instantâneo *mybackupstdpageblob_ss2*, que é armazenado na conta de armazenamento de cópia de segurança de Olá *mybackupstdaccount*.
2. No mybackupstdaccount, promover o instantâneo de Olá *mybackupstdpageblob_ss2* como blob de página base cópia de segurança nova Olá *mybackupstdpageblobrestored*.
3. Tirar um instantâneo este BLOBs de páginas de cópia de segurança restaurada, denominado *mybackupstdpageblobrestored_ss1*.
4. Blob de páginas de Olá restaurada cópia *mybackupstdpageblobrestored* de *mybackupstdaccount* demasiado*mypremiumaccount* como disco de premium novo Olá  *mypremiumdiskrestored*.
5. Tirar um instantâneo *mypremiumdiskrestored*, chamado *mypremiumdiskrestored_ss1* para efetuar cópias de segurança incrementais futuras.
6. Ponto de série de Olá DS toohello restaurada disco da VM *mypremiumdiskrestored* e desanexar Olá antigo *mypremiumdisk* de Olá VM.
7. Iniciar o processo de cópia de segurança de Olá descrito na secção anterior para o disco de Olá restaurada *mypremiumdiskrestored*, utilizando Olá *mybackupstdpageblobrestored* como BLOBs de páginas de cópia de segurança de Olá.

![Restaurar o disco de instantâneos](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Passos Seguintes
Seguinte de Olá utilize liga toolearn mais informações sobre a criação de instantâneos de um blob e planeamento da sua infraestrutura de cópia de segurança de VM.

* [Criar um instantâneo de um Blob](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)
* [Planear a infraestrutura de cópia de segurança de VM](../articles/backup/backup-azure-vms-introduction.md)

