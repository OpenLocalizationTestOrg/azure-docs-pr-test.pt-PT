
1. Inicie sessão no tooyour a subscrição do Azure com os passos de Olá apresentados na [ligar tooAzure de Olá CLI do Azure 1.0](../articles/xplat-cli-connect.md).

2. Certifique-se de que está no modo de implementação clássico Olá da seguinte forma:

    ```azurecli
    azure config mode asm
    ```

3. Localize da imagem Olá Linux que pretende que tooload de imagens disponíveis Olá da seguinte forma:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    Numa janela da linha de comandos do Windows, utilize **find** em vez de grep.
   
4. Utilize `azure vm create` toocreate uma VM com a imagem de Linux Olá na lista anterior Olá. Este passo cria um serviço cloud e uma conta de armazenamento. Também pode ligar esta VM tooan serviço em nuvem existente com uma `-c` opção. Criar um toolog de ponto final SSH na máquina virtual do Linux toohello com Olá `-e` opção. Olá exemplo seguinte cria uma VM chamada `myVM` utilizando Olá `Ubuntu-14_04_4-LTS` imagem no Olá `West US` localização e adiciona um nome de utilizador `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Olá de saída é semelhante toohello seguinte exemplo:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Para uma máquina virtual do Linux, tem de fornecer Olá `-e` opção `vm create`. Não é possível tooenable SSH depois de máquina virtual de Olá foi criada. Para obter mais detalhes sobre o SSH, leia o artigo [como tooUse SSH com o Linux no Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. Pode verificar os atributos de Olá de Olá VM utilizando Olá `azure vm show` comando. Olá exemplo a seguir lista as informações para a VM com o nome de Olá `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Iniciar a VM com Olá `azure vm start` comando da seguinte forma:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Passos seguintes
Para obter detalhes sobre todos os comandos de máquina virtual estes 1.0 de CLI do Azure, leia o artigo Olá [Using Olá 1.0 de CLI do Azure com a implementação de clássico Olá API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

