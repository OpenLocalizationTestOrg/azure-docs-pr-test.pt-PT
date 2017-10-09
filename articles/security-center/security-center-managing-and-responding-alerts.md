---
title: "aaaManage alertas de segurança no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda-o a toouse Centro de segurança do Azure capacidades toomanage e responder a alertas de toosecurity."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>Gerir e responder a alertas de toosecurity no Centro de segurança do Azure
Este documento ajuda-o a utilizar o Centro de segurança do Azure toomanage e responder a alertas de toosecurity.

> [!NOTE]
> deteções tooenable avançada, atualização tooAzure padrão de centro de segurança. Está disponível uma avaliação gratuita de 60 dias. tooupgrade, selecione escalão de preço no Olá [política de segurança](security-center-policies.md). Consulte [preços do Centro de segurança do Azure](security-center-pricing.md) toolearn mais.
>
>

## <a name="what-are-security-alerts"></a>O que são alertas de segurança?
Centro de segurança automaticamente recolhe, analisa e integra-se os dados de registo dos seus recursos do Azure, rede Olá, ligado soluções de parceiros, como soluções de proteção ponto final e firewall, toodetect de ameaças reais e reduzir os falsos positivos. Uma lista de alertas de segurança prioritários é apresentada no Centro de segurança juntamente com Olá informações necessárias tooquickly investigar o problema de Olá e recomendações sobre como tooremediate um ataque.


> [!NOTE]
> Para obter mais informações sobre como funcionam as capacidades de deteção do Centro de Segurança, leia [Capacidades de Deteção do Centro de Segurança do Azure](security-center-detection-capabilities.md).
>
>

## <a name="managing-security-alerts"></a>Gerir alertas de segurança
Pode rever os alertas atuais ao observar Olá **alertas de segurança** mosaico. Abra o Portal do Azure e siga os passos de Olá abaixo toosee mais detalhes sobre cada alerta:

1. No dashboard do Centro de segurança de Olá, verá Olá **alertas de segurança** mosaico.

    ![Mosaico Alertas de segurança no Centro de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Clique em Olá do Olá mosaico tooopen **alertas de segurança** painel que contém mais detalhes sobre Olá alertas como é mostrado abaixo.

   ![Painel de alertas de segurança de Olá no Centro de segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

Na parte inferior Olá deste painel encontram Olá os detalhes para cada alerta. toosort, clique em coluna Olá que pretende que sejam toosort pelo. definição de Olá para cada coluna é indicada abaixo:

* **Descrição**: uma explicação breve do alerta Olá.
* **Contagem**: uma lista de todos os alertas deste tipo específico que foram detetados num dia específico.
* **Detetado por**: Olá serviço que foi responsável por ter acionado o alerta de Olá.
* **Data**: Olá data esse evento Olá ocorreu.
* **Estado**: Olá estado atual para esse alerta. Existem dois tipos de estados:
  * **Active Directory**: Olá alerta de segurança foi detetado.
* **Gravidade**: nível de gravidade Olá, que pode ser alta, média ou baixa.

### <a name="filtering-alerts"></a>Filtragem de alertas
Pode filtrar os alertas com base na data, no estado e na gravidade. Filtragem de alertas pode ser útil para cenários onde necessita de âmbito de Olá toonarrow de mostrar alertas de segurança. Por exemplo, pode pretender tooaddress alertas de segurança ocorridas no Olá últimas 24 horas porque está a investigar uma potencial violação no sistema de Olá.

1. Clique em **filtro** no Olá **alertas de segurança** painel. Olá **filtro** abre painel e selecionar valores de data, estado e gravidade de Olá desejar toosee.

    ![Filtragem de alertas no Centro de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Responder a alertas de toosecurity
Selecione um toolearn de alerta de segurança mais informações sobre eventos de Olá que acionou o alerta Olá e o que, se aplicável, os passos precisam de tootake tooremediate um ataque. Os alertas de segurança estão agrupados por tipo e data. Ao clicar num alerta de segurança irá abrir um painel que contém uma lista de alertas de Olá agrupado.

![Responder a alertas de toosecurity no Centro de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

Neste caso, os alertas de Olá que foram acionados referem-se toosuspicious atividade do protocolo RDP (Remote Desktop Protocol). Step-by-Olá primeira coluna mostra quais os recursos que foram atacados; Olá segundo mostra o número de vezes recursos Olá foi atacado; Olá terceira mostra o tempo de Olá de ataque de Olá; Olá fourth mostra o estado de alerta de Olá; e Olá fifth mostra a gravidade Olá de ataque de Olá. Depois de rever estas informações, clique em recursos de Olá que foi atacado e será aberto um novo painel.

![Sugestões para alertas que toodo sobre a segurança no Centro de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

No Olá **Descrição** campo deste painel irá encontrar mais detalhes sobre este evento. Estes detalhes adicionais facultam informações aprofundadas que Olá accionadas segurança alerta, Olá recurso de destino, quando aplicável Olá origem endereço IP e as recomendações sobre como tooremediate.  Em alguns casos, endereço IP de origem Olá estará vazio (não disponível) porque nem todos os registos de eventos de segurança do Windows incluem o endereço IP Olá.

remediação de Olá sugerida pelo centro de segurança irá variar de acordo com toohello alerta de segurança. Em alguns casos, poderá ter toouse tooimplement outras capacidades do Azure Olá recomendado remediação. Por exemplo, Olá remediação para este ataque é o endereço IP de Olá tooblacklist que está a gerar este ataque ao utilizar um [ACL de rede](../virtual-network/virtual-networks-acl.md) ou um [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) regra.

> [!NOTE]
> Para obter mais informações sobre os diferentes tipos Olá de alertas, leia o artigo [alertas de segurança por tipo no Centro de segurança do Azure](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Consultar também
Neste documento, aprendeu como tooconfigure políticas de segurança no Centro de segurança. toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Lidar com Incidentes de Segurança no Centro de Segurança do Azure](security-center-incident.md)
* [Capacidades de Deteção do Centro de Segurança do Azure](security-center-detection-capabilities.md)
* [Guia de Operações e Planeamento do Centro de Segurança do Azure](security-center-planning-and-operations-guide.md)
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – Encontre mensagens do blogue acerca da segurança e conformidade do Azure.
