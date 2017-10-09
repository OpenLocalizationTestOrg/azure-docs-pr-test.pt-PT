
Para obter mais informações sobre discos, veja [About Disks and VHDs for Virtual Machines (Acerca de Discos e VHDs para Máquinas Virtuais)](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Anexar um disco vazio
1. Abra a CLI do Azure 1.0 e [ligar tooyour subscrição do Azure](../articles/xplat-cli-connect.md). Confirme que está no modo Gestão de Serviço do Azure (`azure config mode asm`).
2. Introduza `azure vm disk attach-new` toocreate e anexe um novo disco, conforme mostrado no seguinte exemplo de Olá. Substitua *myVM* com o nome de Olá da Máquina Virtual com Linux e especifique o tamanho do disco de Olá Olá em GB, o que é *100GB* neste exemplo:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Depois de disco de dados de Olá é criado e ligado, está listado no resultado Olá `azure vm disk list <virtual-machine-name>` conforme mostrado no seguinte exemplo de Olá:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Olá de saída é semelhante toohello seguinte exemplo:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Anexar um disco existente
Para anexar um disco existente, tem de ter um .vhd disponível numa conta de armazenamento.

1. Abra a CLI do Azure 1.0 e [ligar tooyour subscrição do Azure](../articles/xplat-cli-connect.md). Confirme que está no modo Gestão de Serviço do Azure (`azure config mode asm`).
2. Verifique se Olá VHD que pretende tooattach já está carregado tooyour subscrição do Azure:
   
    ```azurecli
    azure vm disk list
    ```

    Olá de saída é semelhante toohello seguinte exemplo:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Se não encontrar o disco de Olá que quiser toouse, pode carregar uma subscrição de tooyour VHD local utilizando `azure vm disk create` ou `azure vm disk upload`. Um exemplo de `disk create` seria como no seguinte exemplo de Olá:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Olá de saída é semelhante toohello seguinte exemplo:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   Também pode utilizar `azure vm disk upload` tooupload uma conta de armazenamento específicas de tooa do VHD. Ler mais sobre Olá comandos toomanage os discos de dados de máquina virtual do Azure [através de aqui](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Agora pode anexa Olá pretendido VHD tooyour máquina:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Certifique-se de que tooreplace *myVM* com o nome de Olá da sua máquina virtual, e *myVHD* com o VHD pretendido.

5. Pode verificar o disco de Olá é anexado toohello máquina de virtual com `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Olá de saída é semelhante toohello seguinte exemplo:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Depois de adicionar um disco de dados, irá precisar de toolog na máquina virtual de toohello e inicializar disco Olá, para que a máquina virtual de Olá pode utilizar o disco de Olá para armazenamento (veja Olá os seguintes passos para obter mais informações sobre como toodo Inicializar disco Olá).
> 
> 

