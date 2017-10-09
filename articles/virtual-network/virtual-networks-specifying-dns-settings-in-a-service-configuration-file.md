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
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a>Especificar as definições de DNS no ficheiro de configuração de serviço
## <a name="dns-elements"></a>Elementos DNS
Um ficheiro de configuração de serviço pode conter um elemento de DnsServers com uma lista de endereços IPv4 para servidores de sistema de nomes de domínio (DNS) de Olá Olá serviço irá utilizar. As definições no ficheiro de configuração do serviço de Olá têm precedência sobre as definições no ficheiro de configuração de rede Olá. Para obter mais informações, consulte [esquema de configuração de serviço do Azure (. cscfg ficheiro)](https://msdn.microsoft.com/library/azure/ee758710.aspx).

**Elemento NetworkConfiguration**

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> Olá **nome** atributo na Olá **DnsServer** elemento é utilizado apenas como um nome de referência. Que não representa o nome de anfitrião Olá para o servidor DNS Olá. Cada **DnsServer** valor do atributo tem de ser exclusivo em toda a subscrição Microsoft Azure Olá.
> 
> 

## <a name="see-also"></a>Veja Também
[Esquema de configuração do serviço do Azure (. cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710)

[Esquema de configuração de rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Configurar uma rede Virtual com ficheiros de configuração de rede](http://go.microsoft.com/fwlink/?LinkId=248094)

[Sobre as definições de rede Virtual no Portal de gestão de Olá](http://go.microsoft.com/fwlink/?LinkId=248092)

