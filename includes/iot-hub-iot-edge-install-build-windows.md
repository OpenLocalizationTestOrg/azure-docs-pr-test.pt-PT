## <a name="install-hello-prerequisites"></a><span data-ttu-id="7ea78-101">Instalar pré-requisitos de Olá</span><span class="sxs-lookup"><span data-stu-id="7ea78-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="7ea78-102">Instalar [Visual Studio 2015 ou 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="7ea78-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="7ea78-103">Pode utilizar Olá livre edição Community caso cumpra os requisitos de licenciamento Olá.</span><span class="sxs-lookup"><span data-stu-id="7ea78-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="7ea78-104">Ser tooinclude se Visual C++ e Gestor de pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ea78-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="7ea78-105">Instalar [git](http://www.git-scm.com) e certifique-se de que pode executar git.exe Olá linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="7ea78-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="7ea78-106">Instalar [CMake](https://cmake.org/download/) e certifique-se de que pode executar cmake.exe Olá linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="7ea78-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="7ea78-107">CMake versão 3.7.2 ou posterior é recomendada.</span><span class="sxs-lookup"><span data-stu-id="7ea78-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="7ea78-108">Olá **. msi** installer é a opção mais fácil de Olá no Windows.</span><span class="sxs-lookup"><span data-stu-id="7ea78-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="7ea78-109">Adicionar o CMake toohello caminho para, pelo menos, Olá utilizador atual quando o instalador Olá pede-lhe.</span><span class="sxs-lookup"><span data-stu-id="7ea78-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="7ea78-110">Instalar [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="7ea78-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="7ea78-111">Certifique-se de adicionar o Python tooyour `PATH` variável de ambiente no **painel de controlo -> sistema -> Avançadas definições do sistema -> variáveis de ambiente**.</span><span class="sxs-lookup"><span data-stu-id="7ea78-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="7ea78-112">Numa linha de comandos, execute Olá os seguintes comandos tooclone Olá Azure IoT Edge GitHub repositório tooyour computador local:</span><span class="sxs-lookup"><span data-stu-id="7ea78-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="7ea78-113">Como toobuild Olá exemplo</span><span class="sxs-lookup"><span data-stu-id="7ea78-113">How toobuild hello sample</span></span>

<span data-ttu-id="7ea78-114">Agora pode compilar Olá IoT Edge e exemplos de tempo de execução no seu computador local:</span><span class="sxs-lookup"><span data-stu-id="7ea78-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="7ea78-115">Abra um **linha de comandos do programador para VS 2015** ou **linha de comandos do programador para VS 2017** linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="7ea78-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="7ea78-116">Navegue toohello pasta de raiz na sua cópia local do Olá **iot edge** repositório.</span><span class="sxs-lookup"><span data-stu-id="7ea78-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="7ea78-117">Execute o script de compilação da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="7ea78-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="7ea78-118">Este script cria um ficheiro de solução do Visual Studio e baseia-se a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="7ea78-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="7ea78-119">Pode encontrar solução do Visual Studio Olá Olá **criar** pasta na sua cópia local do Olá **iot edge** repositório.</span><span class="sxs-lookup"><span data-stu-id="7ea78-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="7ea78-120">Se pretender toobuild e executar testes de unidade de Olá, adicione Olá `--run-unittests` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7ea78-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="7ea78-121">Se pretender toobuild e executar testes de tooend Olá fim, adicione Olá `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="7ea78-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="7ea78-122">Sempre que executar Olá **build.cmd** script, este elimina e, em seguida, recria Olá **criar** pasta na pasta raiz de Olá da sua cópia local Olá **iot edge** repositório.</span><span class="sxs-lookup"><span data-stu-id="7ea78-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
