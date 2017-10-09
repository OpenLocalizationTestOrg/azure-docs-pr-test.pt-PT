## <a name="azure-dns"></a><span data-ttu-id="b0d6c-101">DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="b0d6c-101">Azure DNS</span></span>
<span data-ttu-id="b0d6c-102">O DNS do Azure é um serviço de alojamento de domínios DNS, fornecer a resolução do nome utilizando a infraestrutura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="b0d6c-103">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b0d6c-103">Property</span></span> | <span data-ttu-id="b0d6c-104">Descrição</span><span class="sxs-lookup"><span data-stu-id="b0d6c-104">Description</span></span> | <span data-ttu-id="b0d6c-105">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="b0d6c-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b0d6c-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="b0d6c-106">**DNSzones**</span></span> |<span data-ttu-id="b0d6c-107">Registos DNS toohost de informações de zona de domínio de um determinado domínio</span><span class="sxs-lookup"><span data-stu-id="b0d6c-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="b0d6c-108">/ subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com "</span><span class="sxs-lookup"><span data-stu-id="b0d6c-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="b0d6c-109">Conjuntos de registos de DNS</span><span class="sxs-lookup"><span data-stu-id="b0d6c-109">DNS record sets</span></span>
<span data-ttu-id="b0d6c-110">Zonas DNS tem um objeto subordinado com o nome do conjunto de registos.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="b0d6c-111">Os conjuntos de registos são uma coleção de registos de anfitrião por tipo para uma zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="b0d6c-112">Tipos de registos são A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="b0d6c-113">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b0d6c-113">Property</span></span> | <span data-ttu-id="b0d6c-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="b0d6c-114">Description</span></span> | <span data-ttu-id="b0d6c-115">Valor da amostra</span><span class="sxs-lookup"><span data-stu-id="b0d6c-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b0d6c-116">A</span><span class="sxs-lookup"><span data-stu-id="b0d6c-116">A</span></span> |<span data-ttu-id="b0d6c-117">Tipo de registo de IPv4</span><span class="sxs-lookup"><span data-stu-id="b0d6c-117">IPv4 record type</span></span> |<span data-ttu-id="b0d6c-118">/subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="b0d6c-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="b0d6c-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="b0d6c-119">AAAA</span></span> |<span data-ttu-id="b0d6c-120">Tipo de registo de IPv6</span><span class="sxs-lookup"><span data-stu-id="b0d6c-120">IPv6 record type</span></span> |<span data-ttu-id="b0d6c-121">/subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/aaaa/hostrecord</span><span class="sxs-lookup"><span data-stu-id="b0d6c-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="b0d6c-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="b0d6c-122">CNAME</span></span> |<span data-ttu-id="b0d6c-123">tipo de registo de nome canónico <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="b0d6c-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="b0d6c-124">/subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="b0d6c-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="b0d6c-125">MX</span><span class="sxs-lookup"><span data-stu-id="b0d6c-125">MX</span></span> |<span data-ttu-id="b0d6c-126">tipo de registo do correio</span><span class="sxs-lookup"><span data-stu-id="b0d6c-126">mail record type</span></span> |<span data-ttu-id="b0d6c-127">/subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/MX/Mail</span><span class="sxs-lookup"><span data-stu-id="b0d6c-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="b0d6c-128">NS</span><span class="sxs-lookup"><span data-stu-id="b0d6c-128">NS</span></span> |<span data-ttu-id="b0d6c-129">tipo de registo do servidor de nome</span><span class="sxs-lookup"><span data-stu-id="b0d6c-129">name server record type</span></span> |<span data-ttu-id="b0d6c-130">/subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="b0d6c-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="b0d6c-131">SOA</span><span class="sxs-lookup"><span data-stu-id="b0d6c-131">SOA</span></span> |<span data-ttu-id="b0d6c-132">Início do tipo de registo de autoridade <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="b0d6c-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="b0d6c-133">/subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="b0d6c-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="b0d6c-134">SRV</span><span class="sxs-lookup"><span data-stu-id="b0d6c-134">SRV</span></span> |<span data-ttu-id="b0d6c-135">tipo de registo do serviço</span><span class="sxs-lookup"><span data-stu-id="b0d6c-135">service record type</span></span> |<span data-ttu-id="b0d6c-136">/subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="b0d6c-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="b0d6c-137"><sup>1</sup> só permite um valor por conjunto de registos.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="b0d6c-138"><sup>2</sup> só permite um tipo de registo SOA por zona DNS.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="b0d6c-139">Exemplo de zona DNS no formato Json:</span><span class="sxs-lookup"><span data-stu-id="b0d6c-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="b0d6c-140">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b0d6c-140">Additional resources</span></span>
<span data-ttu-id="b0d6c-141">Olá leitura [documentação da REST API para zonas DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="b0d6c-142">Olá leitura [documentação da REST API para conjuntos de registos DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="b0d6c-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

