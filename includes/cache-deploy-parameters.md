
### <a name="cacheskuname"></a><span data-ttu-id="24604-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="24604-101">cacheSKUName</span></span>
<span data-ttu-id="24604-102">escalão de preço de Olá do Olá da Cache de Redis do Azure de novo.</span><span class="sxs-lookup"><span data-stu-id="24604-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

<span data-ttu-id="24604-103">modelo de Olá define valores Olá que são permitidos para este parâmetro (básico ou Standard) e atribui um valor predefinido (básico), se for especificado nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="24604-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="24604-104">Basic fornece um único nó com vários tamanhos disponíveis segurança too53 GB.</span><span class="sxs-lookup"><span data-stu-id="24604-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="24604-105">Norma fornece dois nós primário/réplica com vários tamanhos disponíveis too53 GB e 99,9% SLA de cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="24604-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="24604-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="24604-106">cacheSKUFamily</span></span>
<span data-ttu-id="24604-107">família de Olá para Olá sku.</span><span class="sxs-lookup"><span data-stu-id="24604-107">hello family for hello sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="24604-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="24604-108">cacheSKUCapacity</span></span>
<span data-ttu-id="24604-109">tamanho de Olá de nova instância de Cache de Redis do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="24604-109">hello size of hello new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="24604-110">modelo de Olá define valores Olá que são permitidos para este parâmetro (0, 1, 2, 3, 4, 5 ou 6) e atribui um valor predefinido (1) se for especificado nenhum valor.</span><span class="sxs-lookup"><span data-stu-id="24604-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="24604-111">Os números correspondem toofollowing tamanhos de cache: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="24604-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

