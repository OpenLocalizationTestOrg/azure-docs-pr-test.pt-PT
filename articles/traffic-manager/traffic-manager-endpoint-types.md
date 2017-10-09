---
title: Tipos de ponto final do Gestor de aaaTraffic | Microsoft Docs
description: "Este artigo explica os diferentes tipos de pontos finais que podem ser utilizados com o Gestor de tráfego do Azure"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Pontos finais do Gestor de tráfego
Microsoft Traffic Manager do Azure permite-lhe toocontrol como tráfego de rede é distribuída implementações tooapplication em execução nos centros de dados diferentes. Configure cada implementação de aplicação como um ponto 'final' no Traffic Manager. Quando o Gestor de tráfego recebe um pedido DNS, escolhe um tooreturn de ponto final disponível no Olá resposta DNS. Gestor de tráfego bases de escolha de Olá no estado de ponto final atual Olá e método de encaminhamento de tráfego de Olá. Para obter mais informações, consulte [como Gestor de tráfego funciona](traffic-manager-how-traffic-manager-works.md).

Existem três tipos de ponto final suportada pelo Gestor de tráfego:
* **Pontos finais Azure** são utilizadas para serviços alojados no Azure.
* **Pontos finais externos** são utilizadas para serviços alojados fora do Azure, no local ou com um fornecedor de alojamento diferente.
* **Pontos finais de aninhada** é toocreate de perfis do Traffic Manager toocombine utilizados mais flexíveis encaminhamento de tráfego esquemas toosupport Olá necessidades de implementações maiores, mais complexas.

Não há nenhuma restrição para como pontos finais de diferentes tipos são combinados num único perfil do Traffic Manager. Cada perfil pode conter qualquer combinação de tipos de ponto final.

Olá secções a seguir descreve cada tipo de ponto final mais detalhadamente.

## <a name="azure-endpoints"></a>Pontos finais Azure

Pontos finais do Azure são utilizados para serviços baseados no Azure no Traffic Manager. Olá, os seguintes tipos de recursos do Azure é suportado:

* 'Clássico' VMs de IaaS e PaaS serviços em nuvem.
* Aplicações Web
* Recursos de PublicIPAddress (que podem ser ligado tooVMs diretamente ou através de um balanceador de carga do Azure). Olá publicIpAddress tem de ter um nome DNS atribuído toobe utilizado num perfil do Traffic Manager.

Recursos PublicIPAddress são recursos do Azure Resource Manager. Não existem no modelo de implementação clássica Olá. Deste modo, são apenas suportados no Gestor de tráfego do Azure Resource Manager experiências. Olá outros tipos de ponto final são suportados através do Gestor de recursos e Olá modelo de implementação clássica.

Quando utilizar pontos finais do Azure, o Gestor de tráfego Deteta quando uma VM do IaaS 'Clássico', o serviço em nuvem ou uma aplicação Web está parada e iniciada. Este estado é apresentado no estado de ponto final de Olá. Consulte [monitorização de pontos finais do Gestor de tráfego](traffic-manager-monitoring.md#endpoint-and-profile-status) para obter mais detalhes. Quando Olá subjacente serviço estiver parado, o Gestor de tráfego não efetua verificações de estado de funcionamento do ponto final ou o ponto final de toohello tráfego direta. Nenhum Gestor de tráfego ocorrem eventos de faturação para Olá parou a instância. Quando Olá forem reiniciados, retoma de faturação e ponto final de Olá tráfego tooreceive elegível. Esta deteção não se aplica a pontos finais de tooPublicIpAddress.

## <a name="external-endpoints"></a>Pontos finais externos

Pontos finais externos são utilizados para serviços fora do Azure. Por exemplo, um serviço alojado no local ou com um fornecedor diferente. Pontos finais externos podem ser utilizados individualmente ou combinados com pontos finais do Azure no Olá mesmo perfil do Traffic Manager. Combinar pontos finais do Azure com pontos finais externos permite vários cenários:

* Um modelo de ativação pós-falha ativo-ativo ou ativo-passivo, utilize Azure tooprovide aumentada a redundância para uma aplicação no local existente.
* Latência de aplicação tooreduce para os utilizadores em todo o mundo Olá, expandir um existente no local aplicação tooadditional localizações geográficas no Azure. Para obter mais informações, consulte [Gestor de tráfego 'Desempenho' Encaminhamento de tráfego](traffic-manager-routing-methods.md#performance).
* Utilize o Azure tooprovide capacidade adicional de uma aplicação no local existente, continuamente ou como um toomeet 'rajada para a nuvem' solução um pico de pedidos de pedido.

Em certos casos, é útil toouse pontos finais externos tooreference Azure serviços (para obter exemplos, consulte Olá [FAQ](traffic-manager-faqs.md#traffic-manager-endpoints)). Neste caso, as verificações de estado de funcionamento são faturadas a taxa de pontos finais Azure Olá, taxa de pontos finais externos não Olá. No entanto, ao contrário dos pontos finais do Azure, se parar ou eliminar Olá subjacente do serviço, estado de funcionamento verifique faturação continua até desativar ou eliminar o ponto final de Olá no Traffic Manager.

## <a name="nested-endpoints"></a>Pontos finais aninhados

Pontos finais aninhados combinam várias Gestor de tráfego perfis toocreate flexível encaminhamento de tráfego esquemas e suportem necessidades Olá implementações maiores, complexas. Com pontos finais de aninhados, é adicionado um perfil de 'child' como um perfil do ponto final tooa 'parent'. Ambos os perfis de principais e subordinados Olá podem conter outros pontos finais de qualquer tipo, incluindo outros perfis aninhados. Para obter mais informações, consulte [aninhada perfis do Traffic Manager](traffic-manager-nested-profiles.md).

## <a name="web-apps-as-endpoints"></a>Web Apps como pontos finais

São aplicáveis algumas considerações adicionais quando configurar as aplicações Web, como pontos finais no Traffic Manager:

1. Apenas as aplicações Web de Olá SKU "Padrão" ou superior são elegíveis para utilização com o Gestor de tráfego. Tenta tooadd uma aplicação Web de uma falha SKU inferior. Desatualização de Olá SKU de uma aplicação Web existente resulta no Gestor de tráfego já não está a enviar tráfego toothat aplicação Web.
2. Quando um ponto final recebe um pedido de HTTP, utiliza Olá 'alojar' cabeçalho Olá pedido toodetermine a aplicação Web deve pedir Olá de serviço. cabeçalho de anfitrião Olá contém Olá DNS nome utilizado tooinitiate Olá pedido, por exemplo 'contosoapp.azurewebsites.net'. toouse um nome DNS diferente com a sua aplicação Web, o nome DNS Olá tem de ser registado como um nome de domínio personalizado para Olá aplicação. Ao adicionar um ponto final da aplicação Web como um ponto final do Azure, o nome DNS de perfil de Gestor de tráfego de Olá é automaticamente registado para Olá aplicação. Este registo é removido automaticamente quando o ponto final de Olá foi eliminado.
3. Cada perfil de Gestor de tráfego pode ter no máximo uma aplicação Web ponto final de cada região do Azure. toowork em torno para esta restrição, pode configurar uma aplicação Web como um ponto final externo. Para obter mais informações, consulte Olá [FAQ](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Ativar e desativar pontos finais

Desativar um ponto final no Traffic Manager pode ser útil tootemporarily remover tráfego a partir de um ponto final que esteja no modo de manutenção ou que vai ser implementado. Assim que o ponto final de Olá for executada novamente, pode ser ativada novamente.

Pontos finais podem ser ativados e desativados através do portal do Gestor de tráfego de Olá, o PowerShell, a CLI ou a API REST, todos os que são suportados no Resource Manager e o modelo de implementação clássica Olá.

> [!NOTE]
> Desativar um ponto final do Azure tem nada toodo com o estado de implementação no Azure. Um Azure service (tais como uma VM ou aplicação Web permanece em execução e consegue tooreceive o tráfego, mesmo quando desativado no Traffic Manager. Tráfego pode ser resolvido diretamente toohello instância de serviço em vez de através do Gestor de tráfego de Olá perfil nome DNS. Para obter mais informações, consulte [como funciona o Gestor de tráfego](traffic-manager-how-traffic-manager-works.md).

elegibilidade atual do Olá de tráfego de tooreceive cada ponto final depende Olá seguintes fatores:

* Estado do perfil Olá (ativado/desativado)
* Estado de ponto final de Olá (ativado/desativado)
* resultados de Olá das verificações de estado de funcionamento de Olá para esse ponto final

Para obter mais informações, consulte [monitorização de pontos finais do Gestor de tráfego](traffic-manager-monitoring.md#endpoint-and-profile-status).

> [!NOTE]
> Uma vez que o Gestor de tráfego funciona ao hello do nível DNS, é tooinfluence não é possível existente ligações tooany ponto final de. Quando um ponto final não estiver disponível, o Gestor de tráfego direciona novas ligações tooanother ponto final disponível. No entanto, o anfitrião Olá atrás Olá desativado ou mau estado de funcionamento ponto final pode continuar tooreceive tráfego através de ligações existentes até que essas sessões estão terminadas. As aplicações devem limitar Olá sessão duração tooallow tráfego toodrain de ligações existentes.

Se todos os pontos finais num perfil estiverem desativados ou se o próprio perfil de Olá estiver desativado, o Gestor de tráfego envia uma consulta DNS novo do 'NXDOMAIN' resposta tooa.


## <a name="next-steps"></a>Passos seguintes

* Saiba [como funciona o Gestor de tráfego](traffic-manager-how-traffic-manager-works.md).
* Saiba mais sobre o Gestor de tráfego [ativação pós-falha automática e monitorização do ponto final](traffic-manager-monitoring.md).
* Saiba mais sobre o Gestor de tráfego [métodos de encaminhamento de tráfego](traffic-manager-routing-methods.md).
