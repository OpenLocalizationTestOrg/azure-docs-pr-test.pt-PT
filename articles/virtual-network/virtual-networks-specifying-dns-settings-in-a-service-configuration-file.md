---
title: "as definições de DNS num ficheiro de configuração do serviço de aaaSpecifying | Microsoft Docs"
description: "especificar definições de DNS personalizadas com o ficheiro de configuração do serviço de rede virtual"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="abad6-103">Especificar as definições de DNS no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="abad6-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="abad6-104">Elementos DNS</span><span class="sxs-lookup"><span data-stu-id="abad6-104">DNS elements</span></span>
<span data-ttu-id="abad6-105">Um ficheiro de configuração de serviço pode conter um elemento de DnsServers com uma lista de endereços IPv4 para servidores de sistema de nomes de domínio (DNS) de Olá Olá serviço irá utilizar.</span><span class="sxs-lookup"><span data-stu-id="abad6-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="abad6-106">As definições no ficheiro de configuração do serviço de Olá têm precedência sobre as definições no ficheiro de configuração de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="abad6-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="abad6-107">Para obter mais informações, consulte [esquema de configuração de serviço do Azure (. cscfg ficheiro)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="abad6-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="abad6-108">**Elemento NetworkConfiguration**</span><span class="sxs-lookup"><span data-stu-id="abad6-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="abad6-109">Olá **nome** atributo na Olá **DnsServer** elemento é utilizado apenas como um nome de referência.</span><span class="sxs-lookup"><span data-stu-id="abad6-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="abad6-110">Que não representa o nome de anfitrião Olá para o servidor DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="abad6-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="abad6-111">Cada **DnsServer** valor do atributo tem de ser exclusivo em toda a subscrição Microsoft Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="abad6-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="abad6-112">Veja Também</span><span class="sxs-lookup"><span data-stu-id="abad6-112">See Also</span></span>
[<span data-ttu-id="abad6-113">Esquema de configuração do serviço do Azure (. cscfg)</span><span class="sxs-lookup"><span data-stu-id="abad6-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="abad6-114">Esquema de configuração de rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="abad6-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="abad6-115">Configurar uma rede Virtual com ficheiros de configuração de rede</span><span class="sxs-lookup"><span data-stu-id="abad6-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="abad6-116">Sobre as definições de rede Virtual no Portal de gestão de Olá</span><span class="sxs-lookup"><span data-stu-id="abad6-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

