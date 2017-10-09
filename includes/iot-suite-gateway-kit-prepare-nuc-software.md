## <a name="build-iot-edge"></a><span data-ttu-id="635d9-101">Criar IoT Edge</span><span class="sxs-lookup"><span data-stu-id="635d9-101">Build IoT Edge</span></span>

<span data-ttu-id="635d9-102">Este tutorial utiliza personalizado toocommunicate de módulos de limite de IoT com Olá solução pré-configurada de monitorização remota.</span><span class="sxs-lookup"><span data-stu-id="635d9-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="635d9-103">Por conseguinte, terá de módulos de limite de IoT Olá toobuild a partir do código de origem personalizada.</span><span class="sxs-lookup"><span data-stu-id="635d9-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="635d9-104">Olá seguintes secções descreve como tooinstall IoT Edge e compilação Olá módulo personalizado do limite de IoT.</span><span class="sxs-lookup"><span data-stu-id="635d9-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="635d9-105">Instalar o limite de IoT</span><span class="sxs-lookup"><span data-stu-id="635d9-105">Install IoT Edge</span></span>

<span data-ttu-id="635d9-106">Olá passos seguintes descrevem como tooinstall Olá pré-compilado software IoT Edge Olá Intel NUC:</span><span class="sxs-lookup"><span data-stu-id="635d9-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="635d9-107">Configure repositórios de pacote inteligente Olá necessário executando os seguintes comandos no Olá Intel NUC de Olá:</span><span class="sxs-lookup"><span data-stu-id="635d9-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="635d9-108">Introduza `y` quando comando Olá pede-lhe demasiado**incluir este canal?**.</span><span class="sxs-lookup"><span data-stu-id="635d9-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="635d9-109">Atualize Gestor de pacotes inteligente de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="635d9-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="635d9-110">Instale o pacote de limite de IoT do Azure de Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="635d9-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="635d9-111">Verifique a instalação de Olá ao exemplo de "Olá mundo" Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="635d9-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="635d9-112">Este exemplo escreve um ficheiro de log.txT toohello do Olá mundo mensagem a cada cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="635d9-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="635d9-113">Olá seguintes comandos executam Olá "Olá mundo" exemplo:</span><span class="sxs-lookup"><span data-stu-id="635d9-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="635d9-114">Ignorar todas **argumento inválido** mensagens quando deixa de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="635d9-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="635d9-115">Utilize Olá comando tooview Olá do conteúdo do ficheiro de registo Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="635d9-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="635d9-116">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="635d9-116">Troubleshooting</span></span>

<span data-ttu-id="635d9-117">Se receber o erro de Olá "nenhum pacote fornece util-linux-dev", tente reiniciando Olá Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="635d9-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
