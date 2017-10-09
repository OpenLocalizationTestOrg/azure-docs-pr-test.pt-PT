<span data-ttu-id="10e5e-101">Alguns pacotes podem não ser instalados através do pip quando são executados no Azure.</span><span class="sxs-lookup"><span data-stu-id="10e5e-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="10e5e-102">Pode simplesmente ser que esse pacote Olá não está disponível no Olá índice de pacote do Python.</span><span class="sxs-lookup"><span data-stu-id="10e5e-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="10e5e-103">É possível que é necessário um compilador (um compilador não está disponível no Olá máquina Olá aplicação web em execução no App Service do Azure).</span><span class="sxs-lookup"><span data-stu-id="10e5e-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="10e5e-104">Nesta secção, vamos abordar formas toodeal com este problema.</span><span class="sxs-lookup"><span data-stu-id="10e5e-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="10e5e-105">Solicitar rodas</span><span class="sxs-lookup"><span data-stu-id="10e5e-105">Request wheels</span></span>
<span data-ttu-id="10e5e-106">Se a instalação do pacote Olá exigir um compilador, deve tentar contactar Olá pacote proprietário toorequest que as rodas sejam disponibilizadas para o pacote de Olá.</span><span class="sxs-lookup"><span data-stu-id="10e5e-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="10e5e-107">Com Olá recente disponibilidade [Microsoft Visual C++ Compiler para o Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], agora é mais fácil pacotes toobuild com código nativo para o Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="10e5e-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="10e5e-108">Criar rodas (requer o Windows)</span><span class="sxs-lookup"><span data-stu-id="10e5e-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="10e5e-109">Nota: Ao utilizar esta opção, certifique-se pacote de Olá toocompile através de um ambiente Python que corresponde à Olá plataforma/arquitetura/versão que é utilizada na aplicação de web de Olá no App Service do Azure (Windows/32-bit/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="10e5e-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="10e5e-110">Se não instalar o pacote Olá porque requer um compilador, pode instalar o compilador de Olá no seu computador local e criar uma roda para o pacote de Olá, que, em seguida, irá incluir no seu repositório.</span><span class="sxs-lookup"><span data-stu-id="10e5e-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="10e5e-111">Utilizadores Mac/Linux: Se não tiver máquina do acesso tooa Windows, consulte o artigo [criar uma Máquina Virtual com o Windows] [ Create a Virtual Machine Running Windows] como toocreate uma VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="10e5e-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="10e5e-112">Pode utilizá-lo toobuild rodas de Olá, adicioná-los toohello repositório e eliminar Olá VM se assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="10e5e-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="10e5e-113">Para Python 2.7, pode instalar [Microsoft Visual C++ Compiler para o Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="10e5e-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="10e5e-114">Para Python 3.4, pode instalar [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="10e5e-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="10e5e-115">toobuild rodas, precisa de pacote de rodas Olá:</span><span class="sxs-lookup"><span data-stu-id="10e5e-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="10e5e-116">Irá utilizar `pip wheel` toocompile uma dependência:</span><span class="sxs-lookup"><span data-stu-id="10e5e-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="10e5e-117">Esta ação cria um ficheiro de whl na pasta \wheelhouse de Olá.</span><span class="sxs-lookup"><span data-stu-id="10e5e-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="10e5e-118">Adicione pasta \wheelhouse de Olá e repositório de tooyour de ficheiros de rodas.</span><span class="sxs-lookup"><span data-stu-id="10e5e-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="10e5e-119">Editar o Olá de tooadd requirements.txt `--find-links` opção na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="10e5e-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="10e5e-120">Isto indica pip toolook para obter uma correspondência exata na pasta local do Olá antes do índice de pacote toohello python.</span><span class="sxs-lookup"><span data-stu-id="10e5e-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="10e5e-121">Se quiser tooinclude todas as suas dependências Olá \wheelhouse pasta e não utilize Olá pacote do python do índice de todo, pode forçar o índice de pacote do pip tooignore Olá adicionando `--no-index` toohello superior do requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="10e5e-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="10e5e-122">Personalizar a instalação</span><span class="sxs-lookup"><span data-stu-id="10e5e-122">Customize installation</span></span>
<span data-ttu-id="10e5e-123">Pode personalizar tooinstall de script de implementação de Olá um pacote no ambiente virtual Olá a utilizar um instalador alternativo, tal como fácil\_instalar.</span><span class="sxs-lookup"><span data-stu-id="10e5e-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="10e5e-124">Veja o deploy.cmd para obter um exemplo comentado.  Certifique-se de que esses pacotes não estão listados no requirements.txt, tooprevent pip de instalá-los.</span><span class="sxs-lookup"><span data-stu-id="10e5e-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="10e5e-125">Adicione este script de implementação toohello:</span><span class="sxs-lookup"><span data-stu-id="10e5e-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="10e5e-126">Também pode ser capaz de toouse fácil\_instale tooinstall a partir de um instalador. exe (alguns são zip compatível, por isso, fácil\_instalar suporte).</span><span class="sxs-lookup"><span data-stu-id="10e5e-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="10e5e-127">Adicione Olá instalador tooyour repositório e invoque fácil\_instalar transferindo Olá toohello de caminho executável.</span><span class="sxs-lookup"><span data-stu-id="10e5e-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="10e5e-128">Adicione este script de implementação toohello:</span><span class="sxs-lookup"><span data-stu-id="10e5e-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="10e5e-129">Incluir o ambiente virtual Olá no repositório de Olá (requer o Windows)</span><span class="sxs-lookup"><span data-stu-id="10e5e-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="10e5e-130">Nota: Ao utilizar esta opção, certifique-se de que toouse um ambiente virtual que corresponde à Olá plataforma/arquitetura/versão que é utilizada na aplicação de web de Olá no App Service do Azure (Windows/32-bit/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="10e5e-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="10e5e-131">Se incluir o ambiente virtual Olá no repositório de Olá, pode impedir o script de implementação de Olá de fazer a gestão do ambiente virtual no Azure através da criação de um ficheiro vazio:</span><span class="sxs-lookup"><span data-stu-id="10e5e-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="10e5e-132">Recomendamos que elimine o ambiente virtual existente na aplicação Olá, tooprevent representada ficheiros Olá quando o ambiente virtual Olá foi gerida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10e5e-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
