<span data-ttu-id="01d8f-101">O Azure determinará se a aplicação utiliza o Python **se ambas estas condições forem verdadeiras**:</span><span class="sxs-lookup"><span data-stu-id="01d8f-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="01d8f-102">ficheiro Requirements.txt na pasta raiz de Olá</span><span class="sxs-lookup"><span data-stu-id="01d8f-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="01d8f-103">qualquer ficheiro. PY na pasta raiz de Olá ou de um ficheiro Runtime.txt a especificar python</span><span class="sxs-lookup"><span data-stu-id="01d8f-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="01d8f-104">Quando for esse caso de Olá, irá utilizar um script de implementação específico do Python, que executa a sincronização padrão de Olá de ficheiros, bem como operações adicionais do Python, tais como:</span><span class="sxs-lookup"><span data-stu-id="01d8f-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="01d8f-105">Gestão automática do ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="01d8f-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="01d8f-106">Instalação de pacotes listados no ficheiro requirements.txt com pip</span><span class="sxs-lookup"><span data-stu-id="01d8f-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="01d8f-107">A criação de Olá config adequado com base no Olá selecionado versão Python.</span><span class="sxs-lookup"><span data-stu-id="01d8f-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="01d8f-108">Recolha de ficheiros estáticos para aplicações Django</span><span class="sxs-lookup"><span data-stu-id="01d8f-108">Collect static files for Django applications</span></span>

<span data-ttu-id="01d8f-109">Pode controlar determinados aspetos dos passos de implementação predefinidos Olá sem ter de script de Olá toocustomize.</span><span class="sxs-lookup"><span data-stu-id="01d8f-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="01d8f-110">Se quiser tooskip todos os passos de implementação específico do Python, pode criar este ficheiro vazio:</span><span class="sxs-lookup"><span data-stu-id="01d8f-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="01d8f-111">Se quiser tooskip recolha de ficheiros estáticos para a sua aplicação Django:</span><span class="sxs-lookup"><span data-stu-id="01d8f-111">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="01d8f-112">Para obter mais controlo sobre a implementação, pode substituir o script de implementação do Olá predefinido criando Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="01d8f-112">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="01d8f-113">Pode utilizar Olá [interface de linha de comandos do Azure] [ Azure command-line interface] ficheiros de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="01d8f-113">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="01d8f-114">Utilize este comando na pasta do projeto:</span><span class="sxs-lookup"><span data-stu-id="01d8f-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="01d8f-115">Se estes ficheiros não existirem, o Azure cria um script de implementação temporário e executa-o.</span><span class="sxs-lookup"><span data-stu-id="01d8f-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="01d8f-116">É idêntico toohello aquele que criar com o comando de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="01d8f-116">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
