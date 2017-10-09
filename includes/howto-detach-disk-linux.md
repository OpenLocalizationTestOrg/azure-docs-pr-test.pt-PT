Quando já não necessita de um disco de dados que esteja anexado tooa máquina de virtual (VM), pode facilmente desanexá-lo. Quando lhe desligar um disco de Olá VM, disco de Olá não é removido do armazenamento. Se pretende que os toouse Olá existente dados no disco Olá novamente, pode reattach-toohello VM mesmo ou outro.  

> [!NOTE]
> Uma VM no Azure utiliza diferentes tipos de discos - um disco de sistema operativo, um disco local temporário e discos de dados opcionais. Para obter detalhes, veja [Acerca dos Discos e VHDs para Máquinas Virtuais](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Não é possível desanexar um disco de sistema operativo, a menos que também eliminar Olá VM.

## <a name="find-hello-disk"></a>Localizar o disco de Olá
Antes de pode desanexar um disco de uma VM tem toofind saída Olá número LUN, que é um identificador para Olá disco toobe desligado. toodo que, siga estes passos:

1. Abra a CLI do Azure e [ligar tooyour subscrição do Azure](../articles/xplat-cli-connect.md). Confirme que está no modo Gestão de Serviço do Azure (`azure config mode asm`).
2. Determinar que discos estão anexado tooyour VM. Olá exemplo seguinte apresenta uma lista de discos para a VM com o nome de Olá `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Olá de saída é semelhante toohello seguinte exemplo:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Tenha em atenção Olá LUN ou Olá **número de unidade lógica** para disco Olá que pretende que o toodetach.

## <a name="remove-operating-system-references-toohello-disk"></a>Remover disco do sistema operativo referências toohello
Antes de desanexar o disco de Olá de convidado de Linux Olá, certifique-se de que todas as partições de disco Olá não estão em utilização. Certifique-se de que esse sistema de operativo Olá não tenta tooremount-las após um reinício. Estes passos de configuração de Olá provavelmente criado quando anular [anexar](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco Olá.

1. Olá utilize `lsscsi` identificador do comando toodiscover Olá disco. `lsscsi` pode ser instalado através de `yum install lsscsi` (em distribuições baseadas no Red Hat) ou de `apt-get install lsscsi` (em distribuições baseadas no Debian). Pode encontrar o identificador de disco Olá que estiver à procura de utilizando o número LUN Olá. número da última Olá na cadeia de identificação de Olá em cada linha é Olá LUN. No Olá seguinte o exemplo de `lsscsi`, LUN 0 mapeia demasiado  */dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Utilize `fdisk -l <disk>` partições de Olá toodiscover associadas Olá disco toobe desligado. Olá exemplo seguinte mostra o resultado Olá para `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Desmonte cada partição listada para o disco de Olá. Olá exemplo seguinte unmounts `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Olá utilize `blkid` Olá de toodiscovery UUIDs não comandos para todas as partições. Olá de saída é semelhante toohello seguinte exemplo:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Remova as entradas no Olá **etc/fstab** ficheiro associado caminhos de dispositivo Olá ou UUIDs não para todas as partições de Olá disco toobe desligado.  As entradas para este exemplo poderão ser:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    ou
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Exposição do disco de Olá
Depois de encontrar o número LUN de Olá de disco Olá e referências de sistema operativo Olá removido, está pronto toodetach-lo:

1. Exposição do disco selecionado do Olá da máquina virtual de Olá executando o comando de Olá `azure vm disk detach
   <virtual-machine-name> <LUN>`. Olá exemplo seguinte Desanexa LUN `0` da VM com o nome de Olá `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. Pode verificar se o disco Olá obteve desligado executando `azure vm disk list` novamente. Olá seguintes verificações de exemplo Olá VM com o nome `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Olá de saída é semelhante toohello seguinte o exemplo, que mostra o disco de dados de Olá já não está ligado:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

disco Olá desligado permanece no armazenamento, mas já não máquina virtual de tooa anexado.

