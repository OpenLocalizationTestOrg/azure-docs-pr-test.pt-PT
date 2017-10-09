---
title: "aaaRestrict acesso através de pontos finais de acesso à Internet no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação do Centro de segurança do Azure * * restringir o acesso através da Internet com o ponto final * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a>Restringir o acesso através de pontos finais de acesso à Internet no Centro de segurança do Azure
Centro de segurança do Azure recomendará que restringir o acesso através de pontos finais de acesso à Internet se qualquer um dos seus grupos de segurança de rede (NSGs) tem uma ou mais regras de entrada que permite o acesso de "qualquer" endereço IP de origem. A abertura de acesso demasiado "nenhum" pode ativar os atacantes tooaccess os recursos. Centro de segurança irá recomendar que edite estes endereços IP do regras de entrada toorestrict acesso toosource que, na verdade, precisam de acesso.

Esta recomendação é gerada para qualquer porta de web não tem "qualquer" como origem.

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação. Não se trata de um guia passo-a-passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de Olá
1. No Olá **painel recomendações**, selecione **restringir o acesso através da Internet com o ponto final**.

   ![Restringir o acesso através de um ponto final com acesso à Internet][1]
2. Esta ação abre o painel de Olá **restringir o acesso através da Internet com o ponto final**. Este painel lista Olá máquinas de virtuais (VMs) com as regras de entrada que criam um potencial problema de segurança. Selecione uma VM.

   ![Selecione uma VM][2]
3. Olá **NSG** painel mostra informações de grupo de segurança de rede, as regras de entrada relacionadas, e Olá associado à VM. Selecione **editar regras de entrada** tooproceed com uma regra de entrada de edição.

   ![Painel do grupo de segurança de rede][3]
4. No Olá **regras de segurança de entrada** painel selecione Olá tooedit de regra de entrada. Neste exemplo, vamos selecione **AllowWeb**.

   ![Regras de segurança de entrada][4]

   Tenha em atenção, também pode selecionar **predefinido regras** conjunto de Olá toosee de regras de predefinidas contido por todos os NSGs. regras de predefinidas Olá não podem ser eliminadas, mas como lhes é atribuída uma prioridade mais baixa, podem ser substituídas pelas regras de Olá que criar. Saiba mais sobre [predefinido regras](../virtual-network/virtual-networks-nsg.md#default-rules).

   ![Regras predefinidas][5]
5. No Olá **AllowWeb** painel, editar Olá propriedades da regra de entrada Olá, de modo que Olá **origem** é um endereço IP ou o bloco de endereços IP. toolearn mais informações sobre Olá as propriedades da regra de entrada Olá, consulte [regras do NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).

   ![Editar regra de entrada][6]

## <a name="see-also"></a>Consultar também
Este artigo mostrou como tooimplement Olá Centro de segurança recomendação "restringir o acesso através da Internet com o ponto final." toolearn mais informações sobre a ativação NSGs e regras, consulte o artigo seguinte Olá:

* [O que é um Grupo de Segurança de Rede (NSG)? (What is a Network Security Group (NSG)?)](../virtual-network/virtual-networks-nsg.md)
* [Como os NSGs toomanage utilizando Olá portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md)– Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gerir recomendações de segurança no Centro de Segurança do Azure](security-center-recommendations.md) – Saiba como as recomendações o ajudam a proteger os seus recursos do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [FAQ do Centro de segurança do Azure](security-center-faq.md)– encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)-obter Olá mais recentes notícias de segurança do Azure e informações.

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
