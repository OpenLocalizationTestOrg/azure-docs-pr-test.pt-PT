
1. <span data-ttu-id="e2b55-101">Inicie sessão no tooyour a subscrição do Azure com os passos de Olá apresentados na [ligar tooAzure de Olá CLI do Azure 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e2b55-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="e2b55-102">Certifique-se de que está no modo de implementação clássico Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e2b55-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="e2b55-103">Localize da imagem Olá Linux que pretende que tooload de imagens disponíveis Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e2b55-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="e2b55-104">Numa janela da linha de comandos do Windows, utilize **find** em vez de grep.</span><span class="sxs-lookup"><span data-stu-id="e2b55-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="e2b55-105">Utilize `azure vm create` toocreate uma VM com a imagem de Linux Olá na lista anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="e2b55-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="e2b55-106">Este passo cria um serviço cloud e uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e2b55-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="e2b55-107">Também pode ligar esta VM tooan serviço em nuvem existente com uma `-c` opção.</span><span class="sxs-lookup"><span data-stu-id="e2b55-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="e2b55-108">Criar um toolog de ponto final SSH na máquina virtual do Linux toohello com Olá `-e` opção.</span><span class="sxs-lookup"><span data-stu-id="e2b55-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="e2b55-109">Olá exemplo seguinte cria uma VM chamada `myVM` utilizando Olá `Ubuntu-14_04_4-LTS` imagem no Olá `West US` localização e adiciona um nome de utilizador `ops`:</span><span class="sxs-lookup"><span data-stu-id="e2b55-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="e2b55-110">Olá de saída é semelhante toohello seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="e2b55-110">hello output is similar toohello following example:</span></span>

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
   > <span data-ttu-id="e2b55-111">Para uma máquina virtual do Linux, tem de fornecer Olá `-e` opção `vm create`.</span><span class="sxs-lookup"><span data-stu-id="e2b55-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="e2b55-112">Não é possível tooenable SSH depois de máquina virtual de Olá foi criada.</span><span class="sxs-lookup"><span data-stu-id="e2b55-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="e2b55-113">Para obter mais detalhes sobre o SSH, leia o artigo [como tooUse SSH com o Linux no Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2b55-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="e2b55-114">Pode verificar os atributos de Olá de Olá VM utilizando Olá `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="e2b55-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="e2b55-115">Olá exemplo a seguir lista as informações para a VM com o nome de Olá `myVM`:</span><span class="sxs-lookup"><span data-stu-id="e2b55-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="e2b55-116">Iniciar a VM com Olá `azure vm start` comando da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="e2b55-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="e2b55-117">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e2b55-117">Next steps</span></span>
<span data-ttu-id="e2b55-118">Para obter detalhes sobre todos os comandos de máquina virtual estes 1.0 de CLI do Azure, leia o artigo Olá [Using Olá 1.0 de CLI do Azure com a implementação de clássico Olá API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e2b55-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

