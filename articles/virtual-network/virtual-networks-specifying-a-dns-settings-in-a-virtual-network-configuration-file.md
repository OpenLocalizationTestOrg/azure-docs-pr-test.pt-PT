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
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a>Especificar as definições de DNS num ficheiro de configuração de rede virtual
Um ficheiro de configuração de rede tem dois elementos que pode utilizar as definições de sistema de nomes de domínio (DNS) toospecify: **DnsServers** e **DnsServerRef**. Pode adicionar uma lista de servidores DNS especificando os respetivos endereços IP e nomes toohello de referência **DnsServers** elemento. Em seguida, pode utilizar um **DnsServerRef** toospecify de elemento que as entradas de servidor DNS do elemento de DnsServers hello são utilizadas para os sites de rede diferente dentro da sua rede virtual.

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo abrange o modelo de implementação clássica Olá.

ficheiro de configuração de rede Olá pode conter Olá seguintes elementos. título de Olá de cada elemento é a página de tooa ligado que fornece informações adicionais sobre o elemento de Olá definições do valor.

> [!IMPORTANT]
> Para obter informações sobre como tooconfigure Olá o ficheiro de configuração de rede, consulte [configurar uma rede Virtual utilizar um ficheiro de configuração de rede](virtual-networks-using-network-configuration-file.md). Para obter informações sobre cada elemento contido no ficheiro de configuração de rede Olá, consulte [esquema de configuração de rede Virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
> 
> 

[Elemento de DNS](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> Olá **nome** atributo na Olá **DnsServer** elemento é utilizado apenas como uma referência para Olá **DnsServerRef** elemento. Que não representa o nome de anfitrião Olá para o servidor DNS Olá. Cada **DnsServer** valor do atributo tem de ser exclusivo em toda a subscrição Microsoft Azure Olá
> 
> 

[Elemento de Sites de rede virtual](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> Na ordem toospecify esta definição para o elemento de Sites de rede virtuais Olá, deve ser anteriormente definido no elemento DNS Olá. Olá DnsServerRef *nome* no Olá Sites de rede virtuais elemento deve referir-se valor de nome de tooa especificado no elemento DNS Olá para DnsServer *nome*.
> 
> 

## <a name="next-steps"></a>Passos seguintes
* Compreender Olá [esquema de configuração de rede Virtual do Azure](http://go.microsoft.com/fwlink/?LinkId=248093).
* Compreender Olá [esquema de configuração do serviço de Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).
* [Configurar uma rede virtual com ficheiros de configuração de rede](virtual-networks-using-network-configuration-file.md).

