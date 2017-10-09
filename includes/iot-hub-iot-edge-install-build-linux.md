## <a name="install-hello-prerequisites"></a><span data-ttu-id="41afd-101">Instalar pré-requisitos de Olá</span><span class="sxs-lookup"><span data-stu-id="41afd-101">Install hello prerequisites</span></span>

<span data-ttu-id="41afd-102">Olá passos deste tutorial partem do princípio de que está a executar Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="41afd-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="41afd-103">Abra uma shell e execute Olá os seguintes pacotes de comandos tooinstall Olá pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="41afd-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="41afd-104">Na shell de Olá, execute Olá os seguintes comandos tooclone Olá Azure IoT Edge GitHub repositório tooyour computador local:</span><span class="sxs-lookup"><span data-stu-id="41afd-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="41afd-105">Como toobuild Olá exemplo</span><span class="sxs-lookup"><span data-stu-id="41afd-105">How toobuild hello sample</span></span>

<span data-ttu-id="41afd-106">Agora pode compilar Olá IoT Edge e exemplos de tempo de execução no seu computador local:</span><span class="sxs-lookup"><span data-stu-id="41afd-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="41afd-107">Abra uma shell.</span><span class="sxs-lookup"><span data-stu-id="41afd-107">Open a shell.</span></span>

1. <span data-ttu-id="41afd-108">Navegue toohello pasta de raiz na sua cópia local do Olá **iot edge** repositório.</span><span class="sxs-lookup"><span data-stu-id="41afd-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="41afd-109">Execute o script de compilação da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="41afd-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="41afd-110">Este script utiliza o **cmake** toocreate utilitário uma pasta denominada **criar** na pasta raiz de Olá da sua cópia local a **iot edge** repositório e gerar um makefile.</span><span class="sxs-lookup"><span data-stu-id="41afd-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="41afd-111">script de Olá, em seguida, cria solução Olá, ignorar a unidade de testes e testes de tooend de fim.</span><span class="sxs-lookup"><span data-stu-id="41afd-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="41afd-112">Se pretender toobuild e executar testes de unidade de Olá, adicione Olá `--run-unittests` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="41afd-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="41afd-113">Se pretender toobuild e executar testes de tooend Olá fim, adicione Olá `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="41afd-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="41afd-114">Sempre que executar Olá **build.sh** script, este elimina e, em seguida, recria Olá **criar** pasta na pasta raiz de Olá da sua cópia local Olá **iot edge** repositório.</span><span class="sxs-lookup"><span data-stu-id="41afd-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
