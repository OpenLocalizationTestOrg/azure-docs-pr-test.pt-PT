---
title: "Descrição geral do serviço de metadados de instância de aaaAzure | Microsoft Docs"
description: "RESTful interface tooget sobre computação, rede e eventos de manutenções da VM."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="069df-103">Serviço de metadados de instância do Azure</span><span class="sxs-lookup"><span data-stu-id="069df-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="069df-104">Olá Service de metadados de instância do Azure fornece informações sobre as instâncias de máquina virtual que podem ser utilizado toomanage e configurar as máquinas virtuais em execução.</span><span class="sxs-lookup"><span data-stu-id="069df-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="069df-105">Isto inclui informações como SKU, a configuração de rede e os eventos de manutenção futura.</span><span class="sxs-lookup"><span data-stu-id="069df-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="069df-106">Para obter mais informações sobre o tipo de informações é disponível, consulte [categorias de metadados](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="069df-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="069df-107">Serviço de metadados de instância do Azure é um ponto final de REST tooall acessível VMs de IaaS criado através de Olá [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="069df-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="069df-108">ponto final de Olá está disponível um endereço de IP bem conhecidos não encaminháveis internos (`169.254.169.254`) que podem ser acedidos apenas a partir de dentro de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="069df-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="069df-109">Informações importantes</span><span class="sxs-lookup"><span data-stu-id="069df-109">Important information</span></span>

<span data-ttu-id="069df-110">Este serviço é **geralmente disponível** em regiões globais do Azure.</span><span class="sxs-lookup"><span data-stu-id="069df-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="069df-111">Trata-se em pré-visualização pública para Government, China e na nuvem do Azure de alemão.</span><span class="sxs-lookup"><span data-stu-id="069df-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="069df-112">Regularmente recebe atualizações tooexpose novas informações sobre instâncias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="069df-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="069df-113">Esta página reflete Olá atualizado [categorias de dados](#instance-metadata-data-categories) disponíveis.</span><span class="sxs-lookup"><span data-stu-id="069df-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="069df-114">Disponibilidade do serviço</span><span class="sxs-lookup"><span data-stu-id="069df-114">Service Availability</span></span>
<span data-ttu-id="069df-115">serviço de Olá está disponível em todas as regiões do Global Azure geralmente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="069df-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="069df-116">serviço de Olá está em pré-visualização pública em regiões de Olá Government, China ou na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="069df-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="069df-117">Regiões</span><span class="sxs-lookup"><span data-stu-id="069df-117">Regions</span></span>                                        | <span data-ttu-id="069df-118">Disponibilidade?</span><span class="sxs-lookup"><span data-stu-id="069df-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="069df-119">Todas as regiões do Azure Global geralmente disponíveis</span><span class="sxs-lookup"><span data-stu-id="069df-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="069df-120">Geralmente disponível</span><span class="sxs-lookup"><span data-stu-id="069df-120">Generally Available</span></span> 
[<span data-ttu-id="069df-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="069df-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="069df-122">Pré-visualização</span><span class="sxs-lookup"><span data-stu-id="069df-122">In Preview</span></span> 
[<span data-ttu-id="069df-123">Azure China</span><span class="sxs-lookup"><span data-stu-id="069df-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="069df-124">Pré-visualização</span><span class="sxs-lookup"><span data-stu-id="069df-124">In Preview</span></span>
[<span data-ttu-id="069df-125">Datacenters do Azure</span><span class="sxs-lookup"><span data-stu-id="069df-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="069df-126">Pré-visualização</span><span class="sxs-lookup"><span data-stu-id="069df-126">In Preview</span></span>

<span data-ttu-id="069df-127">Esta tabela é atualizada quando o serviço de Olá e fica disponível outras nuvens do Azure.</span><span class="sxs-lookup"><span data-stu-id="069df-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="069df-128">tootry saída Olá serviço de metadados de instância, crie uma VM de [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou Olá [portal do Azure](http://portal.azure.com) no Olá acima regiões e siga Olá exemplos abaixo.</span><span class="sxs-lookup"><span data-stu-id="069df-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="069df-129">Utilização</span><span class="sxs-lookup"><span data-stu-id="069df-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="069df-130">Controlo de versões</span><span class="sxs-lookup"><span data-stu-id="069df-130">Versioning</span></span>
<span data-ttu-id="069df-131">Olá instância metadados do serviço é com a versão.</span><span class="sxs-lookup"><span data-stu-id="069df-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="069df-132">As versões são obrigatórias e a versão atual do Olá `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="069df-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="069df-133">Pré-visualização as versões anteriores dos eventos agendadas suportados {mais recente} como Olá api-version.</span><span class="sxs-lookup"><span data-stu-id="069df-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="069df-134">Este formato já não é suportado e será preterido no Olá futura.</span><span class="sxs-lookup"><span data-stu-id="069df-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="069df-135">À medida que adiciona as versões mais recentes, as versões mais antigas podem ainda ser acedidas para compatibilidade, se os scripts terem dependências de formatos de dados específicos.</span><span class="sxs-lookup"><span data-stu-id="069df-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="069df-136">No entanto, tenha em atenção que version(2017-03-01) de pré-visualização atual Olá poderão não estar disponíveis assim que o serviço de Olá estiver geralmente disponível.</span><span class="sxs-lookup"><span data-stu-id="069df-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="069df-137">Utilizar cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="069df-137">Using Headers</span></span>
<span data-ttu-id="069df-138">Quando consultar Olá instância metadados do serviço, tem de fornecer o cabeçalho de Olá `Metadata: true` tooensure Olá pedido não foi inadvertidamente redirecionado o pedido.</span><span class="sxs-lookup"><span data-stu-id="069df-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="069df-139">Obtenção de metadados</span><span class="sxs-lookup"><span data-stu-id="069df-139">Retrieving metadata</span></span>

<span data-ttu-id="069df-140">Metadados da instância estão disponível para executar as VMs criado/geridos através de [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="069df-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="069df-141">Aceder a todas as categorias de dados para uma instância de máquina virtual utilizando Olá pedido os seguintes:</span><span class="sxs-lookup"><span data-stu-id="069df-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="069df-142">Todas as consultas de metadados de instância diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="069df-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="069df-143">Saída de dados</span><span class="sxs-lookup"><span data-stu-id="069df-143">Data output</span></span>
<span data-ttu-id="069df-144">Por predefinição, Olá instância metadados serviço devolve dados no formato JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="069df-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="069df-145">No entanto, APIs diferentes pode devolver dados em diferentes formatos, se for pedida.</span><span class="sxs-lookup"><span data-stu-id="069df-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="069df-146">Olá tabela que se segue é uma referência de APIs podem suportar outros formatos de dados.</span><span class="sxs-lookup"><span data-stu-id="069df-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="069df-147">API</span><span class="sxs-lookup"><span data-stu-id="069df-147">API</span></span> | <span data-ttu-id="069df-148">Formato de dados predefinido</span><span class="sxs-lookup"><span data-stu-id="069df-148">Default Data Format</span></span> | <span data-ttu-id="069df-149">Outros formatos</span><span class="sxs-lookup"><span data-stu-id="069df-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="069df-150">/instance</span><span class="sxs-lookup"><span data-stu-id="069df-150">/instance</span></span> | <span data-ttu-id="069df-151">JSON</span><span class="sxs-lookup"><span data-stu-id="069df-151">json</span></span> | <span data-ttu-id="069df-152">Texto</span><span class="sxs-lookup"><span data-stu-id="069df-152">text</span></span>
<span data-ttu-id="069df-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="069df-153">/scheduledevents</span></span> | <span data-ttu-id="069df-154">JSON</span><span class="sxs-lookup"><span data-stu-id="069df-154">json</span></span> | <span data-ttu-id="069df-155">Nenhum</span><span class="sxs-lookup"><span data-stu-id="069df-155">none</span></span>

<span data-ttu-id="069df-156">tooaccess um formato de resposta não predefinido, especifique o formato de pedido de Olá como um parâmetro de cadeia de consulta no pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="069df-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="069df-157">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="069df-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="069df-158">Segurança</span><span class="sxs-lookup"><span data-stu-id="069df-158">Security</span></span>
<span data-ttu-id="069df-159">ponto final de serviço de metadados de instância de Olá é acessível apenas a partir de dentro de Olá executar a instância de máquina virtual num endereço IP não encaminháveis internos.</span><span class="sxs-lookup"><span data-stu-id="069df-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="069df-160">Além disso, qualquer pedido com um `X-Forwarded-For` cabeçalho é rejeitado pelo serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="069df-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="069df-161">É também necessário pedidos toocontain um `Metadata: true` tooensure de cabeçalho que Olá pedido real foi diretamente pretendida e não uma parte de redirecionamento não intencional.</span><span class="sxs-lookup"><span data-stu-id="069df-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="069df-162">Erro</span><span class="sxs-lookup"><span data-stu-id="069df-162">Error</span></span>
<span data-ttu-id="069df-163">Se existir um elemento de dados não encontrado ou um pedido com formato incorreto, Olá instância metadados serviço devolve erros de HTTP padrão.</span><span class="sxs-lookup"><span data-stu-id="069df-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="069df-164">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="069df-164">For example:</span></span>

<span data-ttu-id="069df-165">Código de estado de HTTP</span><span class="sxs-lookup"><span data-stu-id="069df-165">HTTP Status Code</span></span> | <span data-ttu-id="069df-166">Razão</span><span class="sxs-lookup"><span data-stu-id="069df-166">Reason</span></span>
----------------|-------
<span data-ttu-id="069df-167">200 OK</span><span class="sxs-lookup"><span data-stu-id="069df-167">200 OK</span></span> |
<span data-ttu-id="069df-168">Pedido de 400 incorreta</span><span class="sxs-lookup"><span data-stu-id="069df-168">400 Bad Request</span></span> | <span data-ttu-id="069df-169">Falta `Metadata: true` cabeçalho</span><span class="sxs-lookup"><span data-stu-id="069df-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="069df-170">404 Não Encontrado</span><span class="sxs-lookup"><span data-stu-id="069df-170">404 Not Found</span></span> | <span data-ttu-id="069df-171">Olá does't elemento pedido existe</span><span class="sxs-lookup"><span data-stu-id="069df-171">hello requested element does't exist</span></span> 
<span data-ttu-id="069df-172">405 Método não permitido</span><span class="sxs-lookup"><span data-stu-id="069df-172">405 Method Not Allowed</span></span> | <span data-ttu-id="069df-173">Apenas `GET` e `POST` os pedidos são suportados</span><span class="sxs-lookup"><span data-stu-id="069df-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="069df-174">429 demasiados pedidos</span><span class="sxs-lookup"><span data-stu-id="069df-174">429 Too Many Requests</span></span> | <span data-ttu-id="069df-175">Olá API atualmente suporta um máximo de 5 consultas por segundo</span><span class="sxs-lookup"><span data-stu-id="069df-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="069df-176">Erro no serviço 500</span><span class="sxs-lookup"><span data-stu-id="069df-176">500 Service Error</span></span>     | <span data-ttu-id="069df-177">Tente novamente após algum tempo</span><span class="sxs-lookup"><span data-stu-id="069df-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="069df-178">Exemplos</span><span class="sxs-lookup"><span data-stu-id="069df-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="069df-179">Todas as respostas de API são cadeias JSON.</span><span class="sxs-lookup"><span data-stu-id="069df-179">All API responses are JSON strings.</span></span> <span data-ttu-id="069df-180">Todas as respostas de exemplo seguintes são impressas pretty para legibilidade.</span><span class="sxs-lookup"><span data-stu-id="069df-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="069df-181">A obtenção de informações de rede</span><span class="sxs-lookup"><span data-stu-id="069df-181">Retrieving network information</span></span>

<span data-ttu-id="069df-182">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="069df-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="069df-183">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="069df-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="069df-184">resposta Olá é uma cadeia JSON.</span><span class="sxs-lookup"><span data-stu-id="069df-184">hello response is a JSON string.</span></span> <span data-ttu-id="069df-185">Olá seguinte exemplo de resposta é impresso pretty para legibilidade.</span><span class="sxs-lookup"><span data-stu-id="069df-185">hello following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="069df-186">Obter o endereço IP público</span><span class="sxs-lookup"><span data-stu-id="069df-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="069df-187">Obter todos os metadados para uma instância</span><span class="sxs-lookup"><span data-stu-id="069df-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="069df-188">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="069df-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="069df-189">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="069df-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="069df-190">resposta Olá é uma cadeia JSON.</span><span class="sxs-lookup"><span data-stu-id="069df-190">hello response is a JSON string.</span></span> <span data-ttu-id="069df-191">Olá seguinte exemplo de resposta é impresso pretty para legibilidade.</span><span class="sxs-lookup"><span data-stu-id="069df-191">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="069df-192">Obtenção de metadados na máquina Virtual do Windows</span><span class="sxs-lookup"><span data-stu-id="069df-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="069df-193">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="069df-193">**Request**</span></span>

<span data-ttu-id="069df-194">Metadados de instância podem ser obtido no Windows através do utilitário do PowerShell de Olá `curl`:</span><span class="sxs-lookup"><span data-stu-id="069df-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="069df-195">Ou através de Olá `Invoke-RestMethod` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="069df-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="069df-196">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="069df-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="069df-197">resposta Olá é uma cadeia JSON.</span><span class="sxs-lookup"><span data-stu-id="069df-197">hello response is a JSON string.</span></span> <span data-ttu-id="069df-198">Olá seguinte exemplo de resposta é impresso pretty para legibilidade.</span><span class="sxs-lookup"><span data-stu-id="069df-198">hello following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="069df-199">Categorias de dados de metadados de instância</span><span class="sxs-lookup"><span data-stu-id="069df-199">Instance metadata data categories</span></span>
<span data-ttu-id="069df-200">Olá seguintes categorias de dados está disponível através de Olá metadados do serviço da instância:</span><span class="sxs-lookup"><span data-stu-id="069df-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="069df-201">Dados</span><span class="sxs-lookup"><span data-stu-id="069df-201">Data</span></span> | <span data-ttu-id="069df-202">Descrição</span><span class="sxs-lookup"><span data-stu-id="069df-202">Description</span></span>
-----|------------
<span data-ttu-id="069df-203">localização</span><span class="sxs-lookup"><span data-stu-id="069df-203">location</span></span> | <span data-ttu-id="069df-204">Olá de região do Azure VM está em execução</span><span class="sxs-lookup"><span data-stu-id="069df-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="069df-205">nome</span><span class="sxs-lookup"><span data-stu-id="069df-205">name</span></span> | <span data-ttu-id="069df-206">Nome do Olá VM</span><span class="sxs-lookup"><span data-stu-id="069df-206">Name of hello VM</span></span> 
<span data-ttu-id="069df-207">oferta</span><span class="sxs-lookup"><span data-stu-id="069df-207">offer</span></span> | <span data-ttu-id="069df-208">Disponibilizam informações para a imagem VM Olá.</span><span class="sxs-lookup"><span data-stu-id="069df-208">Offer information for hello VM image.</span></span> <span data-ttu-id="069df-209">Este valor só está presente para imagens implementadas a partir da Galeria de imagem do Azure.</span><span class="sxs-lookup"><span data-stu-id="069df-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="069df-210">Fabricante</span><span class="sxs-lookup"><span data-stu-id="069df-210">publisher</span></span> | <span data-ttu-id="069df-211">Publicador de imagem de VM Olá</span><span class="sxs-lookup"><span data-stu-id="069df-211">Publisher of hello VM image</span></span>
<span data-ttu-id="069df-212">SKU</span><span class="sxs-lookup"><span data-stu-id="069df-212">sku</span></span> | <span data-ttu-id="069df-213">SKU específico para a imagem VM Olá</span><span class="sxs-lookup"><span data-stu-id="069df-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="069df-214">Versão</span><span class="sxs-lookup"><span data-stu-id="069df-214">version</span></span> | <span data-ttu-id="069df-215">Versão da imagem VM Olá</span><span class="sxs-lookup"><span data-stu-id="069df-215">Version of hello VM image</span></span> 
<span data-ttu-id="069df-216">osType</span><span class="sxs-lookup"><span data-stu-id="069df-216">osType</span></span> | <span data-ttu-id="069df-217">Linux ou do Windows</span><span class="sxs-lookup"><span data-stu-id="069df-217">Linux or Windows</span></span> 
<span data-ttu-id="069df-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="069df-218">platformUpdateDomain</span></span> |  <span data-ttu-id="069df-219">[Domínio de atualização](virtual-machines-windows-manage-availability.md) Olá VM está em execução no</span><span class="sxs-lookup"><span data-stu-id="069df-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="069df-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="069df-220">platformFaultDomain</span></span> | <span data-ttu-id="069df-221">[Domínio de falhas](virtual-machines-windows-manage-availability.md) Olá VM está em execução no</span><span class="sxs-lookup"><span data-stu-id="069df-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="069df-222">vmId</span><span class="sxs-lookup"><span data-stu-id="069df-222">vmId</span></span> | <span data-ttu-id="069df-223">[Identificador exclusivo](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para Olá VM</span><span class="sxs-lookup"><span data-stu-id="069df-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="069df-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="069df-224">vmSize</span></span> | [<span data-ttu-id="069df-225">Tamanho da VM</span><span class="sxs-lookup"><span data-stu-id="069df-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="069df-226">IPv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="069df-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="069df-227">Endereço IPv4 local de Olá VM</span><span class="sxs-lookup"><span data-stu-id="069df-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="069df-228">IPv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="069df-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="069df-229">Endereço IPv4 público de Olá VM</span><span class="sxs-lookup"><span data-stu-id="069df-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="069df-230">endereço de sub-rede /</span><span class="sxs-lookup"><span data-stu-id="069df-230">subnet/address</span></span> | <span data-ttu-id="069df-231">Endereço de sub-rede de Olá VM</span><span class="sxs-lookup"><span data-stu-id="069df-231">Subnet address of hello VM</span></span>
<span data-ttu-id="069df-232">prefixo de sub-rede /</span><span class="sxs-lookup"><span data-stu-id="069df-232">subnet/prefix</span></span> | <span data-ttu-id="069df-233">Prefixo de sub-rede, 24 de exemplo</span><span class="sxs-lookup"><span data-stu-id="069df-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="069df-234">IPv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="069df-234">ipv6/ipAddress</span></span> | <span data-ttu-id="069df-235">Endereço IPv6 local de Olá VM</span><span class="sxs-lookup"><span data-stu-id="069df-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="069df-236">MacAddress</span><span class="sxs-lookup"><span data-stu-id="069df-236">macAddress</span></span> | <span data-ttu-id="069df-237">Endereço mac VM</span><span class="sxs-lookup"><span data-stu-id="069df-237">VM mac address</span></span> 
<span data-ttu-id="069df-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="069df-238">scheduledevents</span></span> | <span data-ttu-id="069df-239">Está a ser atualmente consulte de pré-visualização pública [scheduledevents](virtual-machines-scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="069df-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="069df-240">Exemplos de cenários de utilização</span><span class="sxs-lookup"><span data-stu-id="069df-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="069df-241">Controlo de VM em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="069df-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="069df-242">Como um fornecedor de serviços, poderá ser necessário tootrack Olá número as VMs com o seu software ou agentes que necessitam de exclusividade tootrack de Olá VM.</span><span class="sxs-lookup"><span data-stu-id="069df-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="069df-243">toobe tooget capaz de um ID exclusivo para uma VM, utilize Olá `vmId` campo do serviço de metadados de instância.</span><span class="sxs-lookup"><span data-stu-id="069df-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="069df-244">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="069df-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="069df-245">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="069df-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="069df-246">Colocação de contentores, partições de dados com base em domínio de falhas/atualização</span><span class="sxs-lookup"><span data-stu-id="069df-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="069df-247">Alguns cenários, colocação das réplicas de dados diferentes é prime importância.</span><span class="sxs-lookup"><span data-stu-id="069df-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="069df-248">Por exemplo, [colocação de réplica do HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou colocação contentor através de um [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) poderá necessitar tooknow Olá `platformFaultDomain` e `platformUpdateDomain` Olá VM está em execução no.</span><span class="sxs-lookup"><span data-stu-id="069df-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="069df-249">Pode consultar estes dados diretamente através do Olá instância metadados do serviço.</span><span class="sxs-lookup"><span data-stu-id="069df-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="069df-250">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="069df-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="069df-251">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="069df-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="069df-252">Obter mais informações sobre Olá VM durante caso de suporte</span><span class="sxs-lookup"><span data-stu-id="069df-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="069df-253">Como um fornecedor de serviços, poderá receber uma chamada de suporte onde pretende que tooknow mais informações sobre Olá VM.</span><span class="sxs-lookup"><span data-stu-id="069df-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="069df-254">Pedir Olá cliente tooshare Olá computação metadados podem fornecer informações básicas para Olá suporte profissional tooknow sobre o tipo de Olá da VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="069df-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="069df-255">**Pedido**</span><span class="sxs-lookup"><span data-stu-id="069df-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="069df-256">**Resposta**</span><span class="sxs-lookup"><span data-stu-id="069df-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="069df-257">resposta Olá é uma cadeia JSON.</span><span class="sxs-lookup"><span data-stu-id="069df-257">hello response is a JSON string.</span></span> <span data-ttu-id="069df-258">Olá seguinte exemplo de resposta é impresso pretty para legibilidade.</span><span class="sxs-lookup"><span data-stu-id="069df-258">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="069df-259">Exemplos de chamar o serviço de metadados utilizando idiomas diferentes dentro Olá VM</span><span class="sxs-lookup"><span data-stu-id="069df-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="069df-260">Idioma</span><span class="sxs-lookup"><span data-stu-id="069df-260">Language</span></span> | <span data-ttu-id="069df-261">Exemplo</span><span class="sxs-lookup"><span data-stu-id="069df-261">Example</span></span> 
---------|----------------
<span data-ttu-id="069df-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="069df-262">Ruby</span></span>     | <span data-ttu-id="069df-263">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="069df-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="069df-264">Aceda a Lan</span><span class="sxs-lookup"><span data-stu-id="069df-264">Go Lan</span></span>   | <span data-ttu-id="069df-265">https://github.com/Microsoft/azureimds/blob/Master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="069df-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="069df-266">python</span><span class="sxs-lookup"><span data-stu-id="069df-266">python</span></span>   | <span data-ttu-id="069df-267">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="069df-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="069df-268">C++</span><span class="sxs-lookup"><span data-stu-id="069df-268">C++</span></span>      | <span data-ttu-id="069df-269">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="069df-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="069df-270">C#</span><span class="sxs-lookup"><span data-stu-id="069df-270">C#</span></span>       | <span data-ttu-id="069df-271">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.CS</span><span class="sxs-lookup"><span data-stu-id="069df-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="069df-272">Javascript</span><span class="sxs-lookup"><span data-stu-id="069df-272">Javascript</span></span> | <span data-ttu-id="069df-273">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="069df-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="069df-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="069df-274">Powershell</span></span> | <span data-ttu-id="069df-275">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="069df-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="069df-276">Bash</span><span class="sxs-lookup"><span data-stu-id="069df-276">Bash</span></span>       | <span data-ttu-id="069df-277">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.SH</span><span class="sxs-lookup"><span data-stu-id="069df-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="069df-278">FAQ</span><span class="sxs-lookup"><span data-stu-id="069df-278">FAQ</span></span>
1. <span data-ttu-id="069df-279">Estou a obter erros de Olá `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="069df-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="069df-280">O que significa?</span><span class="sxs-lookup"><span data-stu-id="069df-280">What does this mean?</span></span>
   * <span data-ttu-id="069df-281">Olá serviço de metadados de instância requer cabeçalho Olá `Metadata: true` toobe transmitido no pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="069df-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="069df-282">Transmitir este cabeçalho numa chamada REST de Olá permite acesso toohello instância metadados do serviço.</span><span class="sxs-lookup"><span data-stu-id="069df-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="069df-283">Por que razão estou posso obter não informações de computação para a minha VM?</span><span class="sxs-lookup"><span data-stu-id="069df-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="069df-284">Olá instância de serviço de metadados apenas suporta atualmente instâncias criadas com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="069df-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="069df-285">Olá futura, pode adicionar suporte para as VMs de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="069df-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="069df-286">Criar um algum volta a minha máquina Virtual através do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="069df-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="069df-287">Por que razão estou posso não ver as informações de metadados de computação?</span><span class="sxs-lookup"><span data-stu-id="069df-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="069df-288">Para quaisquer VMs criadas após Sep 2016, adicione um [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart ver metadados de computação.</span><span class="sxs-lookup"><span data-stu-id="069df-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="069df-289">Para VMs anteriores (criadas antes de Sep 2016), adicionar/remover as extensões ou dados de metadados de toorefresh discos toohello VM.</span><span class="sxs-lookup"><span data-stu-id="069df-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="069df-290">Por que razão estou obter Erro Olá `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="069df-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="069df-291">Repita o pedido com base no back exponencial fora do sistema.</span><span class="sxs-lookup"><span data-stu-id="069df-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="069df-292">Se o problema de Olá persistir, contacte o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="069df-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="069df-293">Onde posso partilham perguntas/comentários adicionais?</span><span class="sxs-lookup"><span data-stu-id="069df-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="069df-294">Envie os seus comentários sobre http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="069df-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="069df-295">Isto seria funcionar para a instância de conjunto de dimensionamento de Máquina Virtual?</span><span class="sxs-lookup"><span data-stu-id="069df-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="069df-296">Sim metadados serviço está disponível para instâncias de conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="069df-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="069df-297">Como posso obter suporte para o serviço de Olá?</span><span class="sxs-lookup"><span data-stu-id="069df-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="069df-298">tooget suporte para o serviço de Olá, criar um problema de suporte no portal do Azure para Olá VM onde não é capaz de tooget metadados resposta após várias tentativas de longas</span><span class="sxs-lookup"><span data-stu-id="069df-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Suporte de metadados de instância](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="069df-300">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="069df-300">Next Steps</span></span>

- <span data-ttu-id="069df-301">Saiba mais sobre Olá [scheduledevents](virtual-machines-scheduled-events.md) API **na pré-visualização pública** fornecida pelo Olá instância metadados do serviço.</span><span class="sxs-lookup"><span data-stu-id="069df-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
