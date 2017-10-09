---
title: "aaaSpecifying as definições de DNS num ficheiro de configuração de rede virtual | Microsoft Docs"
description: "Como ficheiro de definições do servidor DNS toochange numa rede virtual com uma configuração de rede virtual no modelo de implementação clássica Olá"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="3c6dd-103">Especificar as definições de DNS num ficheiro de configuração de rede virtual</span><span class="sxs-lookup"><span data-stu-id="3c6dd-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="3c6dd-104">Um ficheiro de configuração de rede tem dois elementos que pode utilizar as definições de sistema de nomes de domínio (DNS) toospecify: **DnsServers** e **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="3c6dd-105">Pode adicionar uma lista de servidores DNS especificando os respetivos endereços IP e nomes toohello de referência **DnsServers** elemento.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="3c6dd-106">Em seguida, pode utilizar um **DnsServerRef** toospecify de elemento que as entradas de servidor DNS do elemento de DnsServers hello são utilizadas para os sites de rede diferente dentro da sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3c6dd-107">Este artigo abrange o modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="3c6dd-108">ficheiro de configuração de rede Olá pode conter Olá seguintes elementos.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="3c6dd-109">título de Olá de cada elemento é a página de tooa ligado que fornece informações adicionais sobre o elemento de Olá definições do valor.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c6dd-110">Para obter informações sobre como tooconfigure Olá o ficheiro de configuração de rede, consulte [configurar uma rede Virtual utilizar um ficheiro de configuração de rede](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="3c6dd-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="3c6dd-111">Para obter informações sobre cada elemento contido no ficheiro de configuração de rede Olá, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c6dd-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="3c6dd-112">Elemento de DNS</span><span class="sxs-lookup"><span data-stu-id="3c6dd-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="3c6dd-113">Olá **nome** atributo na Olá **DnsServer** elemento é utilizado apenas como uma referência para Olá **DnsServerRef** elemento.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="3c6dd-114">Que não representa o nome de anfitrião Olá para o servidor DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="3c6dd-115">Cada **DnsServer** valor do atributo tem de ser exclusivo em toda a subscrição Microsoft Azure Olá</span><span class="sxs-lookup"><span data-stu-id="3c6dd-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="3c6dd-116">Elemento de Sites de rede virtual</span><span class="sxs-lookup"><span data-stu-id="3c6dd-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="3c6dd-117">Na ordem toospecify esta definição para o elemento de Sites de rede virtuais Olá, deve ser anteriormente definido no elemento DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="3c6dd-118">Olá DnsServerRef *nome* no Olá Sites de rede virtuais elemento deve referir-se valor de nome de tooa especificado no elemento DNS Olá para DnsServer *nome*.</span><span class="sxs-lookup"><span data-stu-id="3c6dd-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3c6dd-119">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3c6dd-119">Next steps</span></span>
* <span data-ttu-id="3c6dd-120">Compreender Olá [esquema de configuração de rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="3c6dd-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="3c6dd-121">Compreender Olá [esquema de configuração do serviço de Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="3c6dd-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="3c6dd-122">[Configurar uma rede virtual com ficheiros de configuração de rede](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="3c6dd-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

