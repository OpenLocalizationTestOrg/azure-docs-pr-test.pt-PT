## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="a1410-101">Implementações de incrementais e completas</span><span class="sxs-lookup"><span data-stu-id="a1410-101">Incremental and complete deployments</span></span>
<span data-ttu-id="a1410-102">Quando implementar os recursos, especifica que a implementação de Olá é uma atualização incremental ou uma atualização completa.</span><span class="sxs-lookup"><span data-stu-id="a1410-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="a1410-103">Olá a principal diferença entre estes dois modos é o como o Gestor de recursos processa os recursos existentes no grupo de recursos de Olá que não estejam no modelo de Olá:</span><span class="sxs-lookup"><span data-stu-id="a1410-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="a1410-104">No modo de conclusão, o Gestor de recursos **elimina** recursos que existem num grupo de recursos de Olá, mas não estão especificados no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="a1410-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="a1410-105">No modo de incremental, o Gestor de recursos **deixa inalterados** recursos que existem num grupo de recursos de Olá, mas não estão especificados no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="a1410-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="a1410-106">Para ambos os modos, o Resource Manager tenta tooprovision todos os recursos especificados no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="a1410-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="a1410-107">Se o recurso de Olá já existe no grupo de recursos de Olá e as respetivas definições são iguais, operação Olá resulta em nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="a1410-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="a1410-108">Se alterar as definições de Olá para um recurso, recursos de Olá é aprovisionado com as novas definições.</span><span class="sxs-lookup"><span data-stu-id="a1410-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="a1410-109">Se tentar localização de Olá tooupdate ou tipo de um recurso existente, implementação de Olá falha com um erro.</span><span class="sxs-lookup"><span data-stu-id="a1410-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="a1410-110">Em vez disso, implemente um novo recurso com a localização de Olá ou escreva o que precisa.</span><span class="sxs-lookup"><span data-stu-id="a1410-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="a1410-111">Por predefinição, o Gestor de recursos utiliza modo incremental Olá.</span><span class="sxs-lookup"><span data-stu-id="a1410-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="a1410-112">diferença de Olá tooillustrate entre modos completas e incrementais, considere Olá cenário a seguir.</span><span class="sxs-lookup"><span data-stu-id="a1410-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="a1410-113">**Grupo de recursos existente** contém:</span><span class="sxs-lookup"><span data-stu-id="a1410-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="a1410-114">Recurso A</span><span class="sxs-lookup"><span data-stu-id="a1410-114">Resource A</span></span>
* <span data-ttu-id="a1410-115">Recurso B</span><span class="sxs-lookup"><span data-stu-id="a1410-115">Resource B</span></span>
* <span data-ttu-id="a1410-116">Recurso C</span><span class="sxs-lookup"><span data-stu-id="a1410-116">Resource C</span></span>

<span data-ttu-id="a1410-117">**Modelo** define:</span><span class="sxs-lookup"><span data-stu-id="a1410-117">**Template** defines:</span></span>

* <span data-ttu-id="a1410-118">Recurso A</span><span class="sxs-lookup"><span data-stu-id="a1410-118">Resource A</span></span>
* <span data-ttu-id="a1410-119">Recurso B</span><span class="sxs-lookup"><span data-stu-id="a1410-119">Resource B</span></span>
* <span data-ttu-id="a1410-120">Recurso D</span><span class="sxs-lookup"><span data-stu-id="a1410-120">Resource D</span></span>

<span data-ttu-id="a1410-121">Quando implementada no **incremental** modo, o grupo de recursos de Olá contém:</span><span class="sxs-lookup"><span data-stu-id="a1410-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="a1410-122">Recurso A</span><span class="sxs-lookup"><span data-stu-id="a1410-122">Resource A</span></span>
* <span data-ttu-id="a1410-123">Recurso B</span><span class="sxs-lookup"><span data-stu-id="a1410-123">Resource B</span></span>
* <span data-ttu-id="a1410-124">Recurso C</span><span class="sxs-lookup"><span data-stu-id="a1410-124">Resource C</span></span>
* <span data-ttu-id="a1410-125">Recurso D</span><span class="sxs-lookup"><span data-stu-id="a1410-125">Resource D</span></span>

<span data-ttu-id="a1410-126">Quando implementada no **concluída** modo, C recurso é eliminado.</span><span class="sxs-lookup"><span data-stu-id="a1410-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="a1410-127">grupo de recursos de Olá contém:</span><span class="sxs-lookup"><span data-stu-id="a1410-127">hello resource group contains:</span></span>

* <span data-ttu-id="a1410-128">Recurso A</span><span class="sxs-lookup"><span data-stu-id="a1410-128">Resource A</span></span>
* <span data-ttu-id="a1410-129">Recurso B</span><span class="sxs-lookup"><span data-stu-id="a1410-129">Resource B</span></span>
* <span data-ttu-id="a1410-130">Recurso D</span><span class="sxs-lookup"><span data-stu-id="a1410-130">Resource D</span></span>
