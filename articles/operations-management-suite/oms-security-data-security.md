---
title: "aaaOperations Management Suite segurança e de segurança de dados de solução de auditoria | Microsoft Docs"
description: "Este documento explica como os dados são geridos e guardados de forma segura no Operations Management Suite Security e na Solução de Segurança e Auditoria."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Segurança de dados da solução de Segurança e Auditoria do Operations Management Suite
os clientes de toohelp evitar, detetar e responder toothreats, [segurança Operations Management Suite (OMS) e a solução de auditoria](operations-management-suite-overview.md) recolhe e processa dados sobre os recursos, que inclui:

* Registo de eventos de segurança
* Eventos de Rastreio de Eventos para o Windows (ETW)
* Eventos de auditoria do AppLocker
* Registo de Firewall do Windows
* Eventos de Análise de Ameaças Avançada
* Resultados da avaliação de linha de base
* Resultados da avaliação de antimalware
* Resultados da avaliação de atualização/correção
* Fluxos de auditáveis explicitamente estão ativados no agente Olá

Iremos tornar-se ao privacidade de Olá compromissos forte tooprotect e segurança destes dados. Microsoft respeita diretrizes de conformidade e segurança toostrict — desde a codificação toooperating um serviço.
Este artigo explica como os dados são geridos e guardados de forma segura na Solução de Segurança e Auditoria do OMS.

## <a name="data-sources"></a>Origens de dados
Solução de auditoria e de segurança do OMS analisam dados de máquinas virtuais e físicos computadores onde está instalado Olá agente do OMS. A Solução de Segurança e Auditoria do OMS pode recolher informações de configuração sobre eventos de segurança, tais como eventos do Windows, registos de auditoria, registos do IIS e mensagens syslog. Os exemplos destes dados incluem: tipo e versão do sistema operativo, processos em execução, nome da máquina, endereços IP, utilizador com sessão iniciada e ID do inquilino.  

## <a name="data-protection"></a>Proteção de dados
**A segregação de dados**: dados são mantidos separados de forma lógica em cada componente em todo o serviço de Olá. Todos os dados são etiquetados por organização. Este tipo de etiquetagem persiste por todo o ciclo de vida do Olá dados e é imposto em cada camada de serviço Olá. 

**Acesso a dados**: tooprovide recomendações de segurança e investigar potenciais ameaças de segurança, a equipa da Microsoft pode aceder a informações recolhidas ou analisadas pelos serviços. Respeitamos toohello [termos de licenciamento Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e [declaração de privacidade](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), quais estipulam que Microsoft não irá utilizar dados de cliente ou derivará informações dos mesmos para qualquer publicidade ou semelhantes fins comerciais. recomendações de segurança tooprovide e investigar potenciais ameaças de segurança, a equipa da Microsoft pode aceder a informações recolhidas ou analisadas pelos serviços. Apenas utilizamos os dados de cliente como tooprovide necessário, com o Azure serviços, incluindo fins compatíveis com o fornecimento desses serviços. Manter todos os dados própria de tooyour direitos.

**Utilização de dados**: a Microsoft utiliza os padrões e ameaças vistas através dos vários inquilinos tooenhance nossas capacidades de prevenção e deteção; podemos fazê-lo de acordo com os compromissos de privacidade de Olá descritos na nossa [privacidade Instrução](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Localização de dados é configurada ao nível da área de trabalho OMS Olá, durante a criação de área de trabalho Olá, o que faz parte do Olá inicial auditoria e segurança do OMS o processo de configuração.
> 
> 

## <a name="see-also"></a>Consultar também
Através deste documento aprendeu como os dados são geridos e salvaguardados no OMS. toolearn mais informações sobre a segurança do OMS e a solução de auditoria, consulte:

* [Descrição geral do Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorização e responder tooSecurity alertas no Operations Management Suite segurança e a solução de auditoria](oms-security-responding-alerts.md)
* [Recursos de Monitorização na Solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

