
## <a name="about-vhds"></a>Sobre VHDs

Olá VHDs utilizados no Azure são ficheiros. vhd armazenados como blobs de páginas numa conta do storage standard ou premium no Azure. Para obter detalhes sobre blobs de páginas, consulte [Understanding block blobs and page blobs (Noções sobre blobs de blocos e blobs de páginas)](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/). Para obter detalhes sobre o armazenamento premium, consulte [High-performance premium storage and Azure VMs (VMs do Azure e armazenamento premium de elevado desempenho)](../articles/storage/common/storage-premium-storage.md).

Azure suporta Olá fixo formato VHD do disco. Define de formato Olá fixo Olá disco lógico horizontalmente de forma linear dentro do ficheiro de Olá, pelo que esse X do deslocamento de disco é armazenado no desvio de blob X. Um rodapé pequeno no fim de Olá do blob Olá Descreve propriedades de Olá de Olá VHD. Muitas vezes, o formato fixo Olá gasta espaço porque a maioria dos discos tem grandes intervalos não utilizados nos mesmos. No entanto, Azure armazena os ficheiros. VHD num formato disperso, para receber os benefícios de Olá de ambos os Olá fixo e dinâmico discos em Olá mesmo tempo. Para obter mais detalhes, consulte [Getting started with virtual hard disks (Introdução aos discos rígidos virtuais)](https://technet.microsoft.com/library/dd979539.aspx).

Todos os ficheiros. vhd no Azure que pretende toouse como discos de toocreate uma origem ou imagens são só de leitura. Quando cria um disco ou a imagem, o Azure faz cópias de Olá ficheiros. vhd. Estas cópias podem ser só de leitura ou de leitura e-escrita, dependendo de como utilizar Olá VHD.

Quando criar uma máquina virtual a partir de uma imagem, o Azure cria um disco para a máquina virtual Olá que é uma cópia do ficheiro. VHD de origem Olá. tooprotect eliminações acidentais, Azure coloca uma concessão em qualquer ficheiro de VHD de origem que tenha utilizado toocreate uma imagem, um disco de sistema operativo ou um disco de dados.

Antes de poder eliminar um ficheiro. VHD de origem, terá de concessão de Olá tooremove ao eliminar disco Olá ou image. toodelete um ficheiro. vhd que está a ser utilizado por uma máquina virtual como um disco de sistema operativo, pode eliminar a máquina de virtual Olá, disco de sistema operativo Olá e ficheiro. VHD de origem Olá, uma vez por eliminar a máquina virtual de Olá e eliminar todos os discos associados. No entanto, a eliminação de um ficheiro .vhd que é uma origem para um disco exige vários passos numa determinada ordem. Em primeiro lugar desanexar o disco de Olá da máquina virtual de Olá, em seguida, eliminar Olá disco e, em seguida, elimine o ficheiro. vhd Olá.

> [!WARNING]
> Se eliminar um ficheiro .vhd de origem do armazenamento ou eliminar a sua conta de armazenamento, a Microsoft não pode recuperar os dados por si.
> 

## <a name="types-of-disks"></a>Tipos de discos 

Os Discos do Azure foram concebidos para garantir uma disponibilidade de 99,999%. Discos do Azure tem consistentemente entregar durabilidade de nível empresarial, com um líder da indústria ZERO % Annualized taxa de falhas.

Existem dois escalões de desempenho para o armazenamento que pode escolher ao criar os discos - Armazenamento Standard e Premium. Além disso, existem dois tipos de discos - geridos e não geridos - que podem residir em qualquer escalão de desempenho.


### <a name="standard-storage"></a>Armazenamento Standard 

O Armazenamento Standard está protegido por HDDs e fornece armazenamento económico, mantendo o desempenho. O Armazenamento Standard pode ser replicado localmente num datacenter, ou ser georredundante com datacenters primários e secundários. Para mais informações sobre a replicação de armazenamento, consulte [Azure Storage replication (Replicação de Armazenamento do Azure)](../articles/storage/common/storage-redundancy.md). 

Para mais informações sobre a utilização do Armazenamento Standard com discos da VM, consulte [Standard Storage and Disks (Armazenamento Standard e Discos)](../articles/storage/common/storage-standard-storage.md).

### <a name="premium-storage"></a>Armazenamento Premium 

O Armazenamento Premium é apoiado por SSDs e fornece suporte para discos de elevado desempenho e de baixa latência para VMs com cargas de trabalho E/S intensivas. Pode utilizar o armazenamento Premium com DS, série DSv2, GS, Ls ou FS série Azure VMs. Para mais informações, consulte [Premium Storage (Armazenamento Premium)](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Discos não geridos

Discos não geridos são tipo tradicionais de Olá de discos que foram utilizados por VMs. Com estas, criar a sua própria conta de armazenamento e especifique que conta de armazenamento ao criar o disco de Olá. Tiver toomake se não colocar demasiados discos em Olá a mesma conta de armazenamento, porque foi excedido Olá [metas de escalabilidade](../articles/storage/common/storage-scalability-targets.md) Olá conta de armazenamento (20.000 IOPS, por exemplo), resultando em Olá VMs a ser limitadas. Com os discos não geridos, tem de toofigure enviados como toomaximize Olá a utilização de um ou mais contas tooget Olá melhor desempenho do armazenamento fora as suas VMs.

### <a name="managed-disks"></a>Managed disks 

Gerido identificadores de discos armazenamento Olá conta criação/gestão em segundo plano de Olá e assegura que não têm tooworry sobre limites de escalabilidade Olá Olá da conta de armazenamento. Basta especificar o tamanho do disco Olá e a camada de desempenho de Olá (padrão/Premium) e o Azure cria e gere o disco de Olá por si. Mesmo que adicione discos ou aumentar vertical ou Olá VM, não tem tooworry sobre armazenamento de Olá que está a ser utilizado. 

Também pode gerir imagens personalizadas numa conta do storage por região do Azure e utilizá-los toocreate centenas de VMs no Olá mesma subscrição. Para obter mais informações sobre discos geridos, consulte Olá [descrição geral de discos geridos](../articles/virtual-machines/windows/managed-disks-overview.md).

Recomendamos que utilize discos gerida do Azure para novas VMs e que converter os discos de toomanaged discos não gerido anterior, partido tootake Olá muitas funcionalidades disponíveis em discos geridos.

### <a name="disk-comparison"></a>Comparação de discos

Olá, a tabela seguinte fornece uma comparação de Premium vs padrão para ambos geridos e geridos toohelp discos decidir que toouse.

|    | Disco Premium do Azure | Disco Standard do Azure |
|--- | ------------------ | ------------------- |
| Tipo de Disco | Unidades de Estado Sólido (SSD) | Unidades de Disco Rígido (HDD)  |
| Descrição geral  | Suporte de disco de baixa latência, alto desempenho baseado em SSD para VMs com cargas de trabalho intensivas em E/S ou ambiente de produção crítico de missão de alojamento | Suporte de disco económico baseado em HDD para cenários de VM de Programação/Teste |
| Cenário  | Cargas de trabalho confidenciais de produção e de desempenho | Programação/Teste, não crítico, <br>Acesso pouco frequente |
| Tamanho do Disco | P4: 32 GB (apenas discos geridos)<br>P6: 64 GB (apenas discos geridos)<br>P10: 128 GB<br>P20: 512 GB<br>P30: 1024 GB<br>P40: GB 2048<br>P50: GB 4095 | Discos não geridos: 1 GB – 4 TB (GB 4095) <br><br>Managed Disks:<br> S4: 32 GB <br>S6: 64 GB <br>S10: 128 GB <br>S20: 512 GB <br>S30: 1024 GB <br>S40: GB 2048<br>S50: GB 4095| 
| Débito Máx por Disco | 250 MB/s | 60 MB/s | 
| IOPs Máx por disco | 7500 IOPS | 500 IOPS | 

