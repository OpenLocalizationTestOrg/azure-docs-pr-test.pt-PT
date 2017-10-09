<span data-ttu-id="d9a4b-101">Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="d9a4b-102">modelo de Olá inclui uma secção denominada parâmetros que contém todos os valores de parâmetro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="d9a4b-103">Deve definir um parâmetro para esses valores que irão variar com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="d9a4b-104">Não defina parâmetros para valores que sempre permanecerão Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="d9a4b-105">Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="d9a4b-106">Quando definir parâmetros, utilize Olá **allowedValues** toospecify campo que os valores de um utilizador pode fornecer durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="d9a4b-107">Olá utilize **defaultValue** campo tooassign toohello parâmetro de valor, se não for fornecido nenhum valor durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="d9a4b-108">Iremos descrevem cada um dos parâmetros do modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="d9a4b-109">SiteName</span><span class="sxs-lookup"><span data-stu-id="d9a4b-109">siteName</span></span>
<span data-ttu-id="d9a4b-110">nome de Olá da aplicação web de Olá pretende toocreate.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="d9a4b-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="d9a4b-111">hostingPlanName</span></span>
<span data-ttu-id="d9a4b-112">nome de Olá de Olá do serviço de aplicações planear toouse para alojar a aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="d9a4b-113">SKU</span><span class="sxs-lookup"><span data-stu-id="d9a4b-113">sku</span></span>
<span data-ttu-id="d9a4b-114">Olá escalão de preço para Olá plano de alojamento.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="d9a4b-115">modelo de Olá define valores Olá que são permitidos para este parâmetro e atribui um valor predefinido (S1), se for especificado nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="d9a4b-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="d9a4b-116">workerSize</span></span>
<span data-ttu-id="d9a4b-117">Olá tamanho da instância Olá (pequeno, médio ou grande) de plano de alojamento.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="d9a4b-118">modelo de Olá define valores Olá que são permitidos para este parâmetro (0, 1 ou 2) e atribui um valor predefinido (0) se for especificado nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="d9a4b-119">valores de Olá correspondem toosmall, média e grande.</span><span class="sxs-lookup"><span data-stu-id="d9a4b-119">hello values correspond toosmall, medium and large.</span></span>

