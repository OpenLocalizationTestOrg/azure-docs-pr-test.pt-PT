---
title: "aaaProtecting as suas aplicações no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento trata as recomendações no Centro de segurança do Azure que o ajudam a proteger as suas aplicações do Azure e manter em conformidade com as políticas de segurança."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Proteger as suas aplicações no Centro de segurança do Azure
Centro de segurança do Azure analisa o estado de segurança de Olá dos seus recursos Azure. Quando o Centro de segurança identificar potenciais vulnerabilidades de segurança, cria recomendações ajudá-lo durante o processo de Olá de configurar os controlos de Olá necessário.  Tipos de recursos de tooAzure aplicam-se recomendações: máquinas virtuais (VMs), redes, SQL e aplicações.

Este artigo aborda as recomendações que se aplicam tooapplications.  Centro de recomendações de aplicação em torno da implementação de uma firewall de aplicação web.  Tabela de Olá de utilização abaixo como uma referência toohelp compreender recomendações de aplicação disponível Olá e que cada um faz se aplicá-lo.

## <a name="available-application-recommendations"></a>Recomendações de aplicação disponíveis
| Recomendação | Descrição |
| --- | --- |
| [Adicionar uma firewall de aplicação Web](security-center-add-web-application-firewall.md) |Recomenda-se de que irá implementar uma firewall de aplicação web (WAF) para pontos finais do web. É apresentada uma recomendação WAF para qualquer destinado ao IP público (IP de nível de instância ou IP com balanceamento de carga) que tenha um grupo de segurança de rede associada com portas web de entrada aberta (80,443).</br></br>Centro de segurança recomenda que aprovisionar um toohelp WAF se Defender contra ataques direcionada para as aplicações web em máquinas virtuais e no ambiente de serviço de aplicações. Aplicação serviço de ambiente (ASE) é um [Premium](https://azure.microsoft.com/pricing/details/app-service/) service opção plano do App Service do Azure fornece um ambiente completamente isolado e dedicado para execução segura de aplicações do App Service do Azure. toolearn mais informações sobre ASE, consulte Olá [a documentação de ambiente de serviço de aplicação](../app-service/app-service-app-service-environments-readme.md).</br></br>Pode proteger várias aplicações web no Centro de segurança ao adicionar estas aplicações tooyour WAF as implementações existentes. |
| [Finalizar a proteção das aplicações](security-center-add-web-application-firewall.md#finalize-application-protection) |configuração de Olá de toocomplete de uma WAF, o tráfego deve ser reencaminhado toohello WAF aplicação. Seguir esta recomendação conclui as alterações de configuração necessários de Olá. |

## <a name="see-also"></a>Consultar também
toolearn mais informações sobre as recomendações que se aplicam tooother tipos de recursos do Azure, consulte o artigo seguinte Olá:

* [Proteger as máquinas virtuais no Centro de segurança do Azure](security-center-virtual-machine-recommendations.md)
* [Proteger a sua rede no Centro de segurança do Azure](security-center-network-recommendations.md)
* [Proteger o seu serviço do SQL do Azure no Centro de segurança do Azure](security-center-sql-service-recommendations.md)

toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
