---
title: "aaaMonitoring recursos no Operations Management Suite segurança e a solução de auditoria | Microsoft Docs"
description: "Este documento ajuda-o toouse segurança do OMS e toomonitor de capacidades de auditoria os recursos e identificar problemas de segurança."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Monitorizar os recursos no Operations Management Suite segurança e a solução de auditoria
Este documento ajuda-o a utilizar a segurança do OMS e toomonitor de capacidades de auditoria os recursos e identificar problemas de segurança.

## <a name="what-is-oms"></a>O que é o OMS?
Microsoft Operations Management Suite (OMS) é a solução de gestão de IT que ajuda a gerir e proteger no local e a infraestrutura de nuvem de baseada na nuvem da Microsoft. Para obter mais informações sobre o OMS, leia o artigo de Olá [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>Monitorização de recursos
Sempre que possível, deverá incidentes de segurança tooprevent aconteça assegurados primeiro Olá. No entanto, é impossível tooprevent todos os incidentes de segurança. Quando um incidente de segurança ocorrem, terá de tooensure que o seu impacto é minimizado.  Existem três recomendações críticas que podem ser utilizado toominimize Olá número e Olá impacto de incidentes de segurança:

* Avalie regularmente vulnerabilidades no seu ambiente.
* Verificar regularmente a todos os sistemas informáticos e tooensure de dispositivos de rede que têm todas as correções mais recentes Olá instaladas.
* Verificar regularmente a todos os registos e mecanismos de registo, incluindo os registos de eventos do sistema operativo, registos específicos da aplicação e os registos de sistema de deteção de intrusões.

Permite que solução de auditoria e segurança do OMS IT tooactively monitorizar todos os recursos, o que podem ajudar a minimiza o impacto de Olá de incidentes de segurança. Auditoria e segurança do OMS tem domínios de segurança que podem ser utilizados para monitorizar os recursos. domínios de segurança de Olá fornece acesso rápido tooa opções, para Olá de monitorização de segurança seguintes domínios vai ser abordados mais detalhes:

* Avaliação de malware
* Avaliação de atualização
* Identidade e Acesso

> [!NOTE]
> Para obter uma descrição geral de todas estas opções, leia o artigo [introdução ao Operations Management Suite segurança e a solução de auditoria](oms-security-getting-started.md).
> 
> 

### <a name="monitoring-system-protection"></a>Proteção do sistema de monitorização
Uma defesa numa abordagem de profundidade, cada camada de proteção é importante para Olá estado geral de segurança do seu elemento. Computadores com detetadas ameaças e computadores com proteção insuficiente são mostrados em Olá mosaico de avaliação de Malware em domínios de segurança. Utilizando informações Olá no Olá avaliação de Malware, pode identificar um plano tooapply proteção toohello os servidores que precisem dele. tooaccess que Olá de siga esta opção, os passos abaixo:

1. No Olá **Microsoft Operations Management Suite** dashboard principal, clique em **auditoria e segurança** mosaico.
   
    ![Auditoria e segurança](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. No Olá **auditoria e segurança** dashboard, clique em **Antimalware avaliação** em **segurança domínios**. Olá **Antimalware avaliação** dashboard aparece conforme mostrado abaixo:

![Avaliação de malware](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

Pode utilizar Olá **avaliação de Malware** Olá do dashboard tooidentify os seguintes problemas de segurança:

* **Ameaças ativas**: computadores comprometidas e que tenham ameaças ativas no sistema de Olá.
* **Remediado ameaças**: computadores comprometidas mas ameaças Olá foram remediadas.
* **Assinatura desatualizada**: computadores que têm a proteção de software maligno ativada, mas a assinatura de Olá está desatualizada.
* **Sem proteção em tempo real**: computadores que não tenham antimalware instalado.

### <a name="monitoring-updates"></a>monitorização de atualizações
Aplicar atualizações de segurança mais recentes Olá é a melhor prática de segurança e deve ser incorporado na sua estratégia de gestão de atualização. Serviço Microsoft Monitoring Agent (HealthService.exe) lê as informações de atualização de computadores monitorizados e, em seguida, envia este serviço OMS toohello informações atualizadas na nuvem de Olá para processamento. Olá serviço Microsoft Monitoring Agent está configurado como um serviço automático e que deve ser sempre em execução no computador de destino Olá.

![monitorização de atualizações](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Lógica é toohello aplicados dados de atualização e o serviço em nuvem Olá regista dados de Olá. Se forem encontradas atualizações em falta, são apresentadas no Olá **atualizações** dashboard. Pode utilizar Olá **atualizações** toowork dashboard com em falta atualizações e desenvolver um plano tooapply-os servidores de toohello que precisam delas. Siga os passos de Olá abaixo tooaccess Olá **atualizações** dashboard:

1. No Olá **Microsoft Operations Management Suite** dashboard principal, clique em **auditoria e segurança** mosaico.
2. No Olá **auditoria e segurança** dashboard, clique em **avaliação de atualização** em **segurança domínios**. dashboard de atualização de Olá aparece conforme mostrado abaixo:

![avaliação de atualização](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

Neste dashboard pode efetuar um atualização avaliação toounderstand Olá estado atual dos seus computadores e ameaças mais críticas de Olá de endereço. Ao utilizar Olá **críticas ou de atualizações de segurança** mosaico, os administradores de TI será capaz de tooaccess informações detalhadas sobre as atualizações de Olá que estão em falta conforme mostrado abaixo:

![resultado da pesquisa](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

Este relatório incluem informações críticas que podem ser utilizado o tipo de Olá tooidentify de ameaça este sistema é vulnerável a, que inclui os artigos da Microsoft KB de Olá associados a atualização de segurança de Olá e Olá Bulletin MS que tenha mais detalhes sobre Olá vulnerabilidade.

### <a name="monitoring-identity-and-access"></a>Identidade e acesso de monitorização
Com os utilizadores trabalharem a partir de qualquer lugar, utilizando vários dispositivos e aceder a uma grande quantidade de aplicações na nuvem e no local, é imperativo que as credenciais estão protegidas. Ataques de roubo de credenciais são aquelas em que um atacante inicialmente obtiver tooaccess de credenciais de acesso tooa regular do utilizador um sistema na rede de Olá. Muitas vezes, este ataque inicial é apenas uma rede toohello acesso de forma tooget, objetivo ultimate Olá toodiscover contas de privilégio. 

Os atacantes e irão permanecer na rede de Olá, utilizando as ferramentas tooextract credenciais de sessões de Olá de outras contas de início de sessão iniciada livremente disponíveis. Dependendo da configuração do sistema de Olá, estas credenciais podem ser extraídas no formato Olá hashes, permissões ou palavras-passe de texto simples mesmo.  

> [!NOTE]
> as máquinas que são diretamente expostos toohello que Internet verá muitos falha tenta toologin que tente utilizar todos os tipos de conhecidos nomes de utilizador (por exemplo, administrador). Na maioria dos casos trata OK se não forem utilizados Olá conhecidos nomes de utilizador e se a palavra-passe de Olá é suficientemente segura.
> 
> 

-É possível tooidentify estes intrusos antes de poderem comprometer uma conta de privilégios. Pode tirar partido **solução de auditoria e de segurança do OMS** toomonitor identidades e acessos. Siga os passos de Olá abaixo tooaccess Olá **identidades e acessos** dashboard:

1. No Olá **Microsoft Operations Management Suite** clique em dashboard principal de segurança e auditoria mosaico.
2. No Olá **auditoria e segurança** dashboard, clique em **identidades e acessos** em **segurança domínios**. Olá **identidades e acessos** dashboard aparece conforme mostrado abaixo:

![identidade e acesso](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

Como parte da sua estratégia de monitorização regular, tem de incluir a monitorização de identidade. Administrador de TI deve ter um aspeto se existir um nome de utilizador válido específico que tenha várias tentativas. Isto poderá indicar um atacante que obteve o nome de utilizador reais Olá e tente toobrute force ou uma ferramenta automática que utiliza hard-coded palavra-passe expirou.

Ativar este dashboard IT tooquickly identificar recursos do potenciais ameaças relacionados tooidentity e acesso toocompany. É determinado importante tooalso identificar tendências potenciais, por exemplo na peça de mosaico do Olá inícios de sessão ao longo do tempo, pode ver ao longo do período de tempo quantas vezes foi efetuada uma tentativa de início de sessão falhadas. Neste caso Olá computador **servidor de ficheiros** recebido 35 tentativas de início de sessão. Pode explorar mais detalhes sobre este computador ao clicar no mesmo. 

![obter mais detalhes](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

relatório de Olá gerado para este computador proporciona detalhes importantes sobre este padrão. Reparado que Olá **conta** fornecem coluna Olá conta de utilizador que foi utilizado tootry tooaccess Olá, sistema, hello **TIMEGENERATED** fornecem coluna Olá o intervalo de tempo no qual Olá foi efetuada a tentativa e Olá **LOGONTYPENAME** fornecem coluna Olá localização onde foi efetuada esta tentativa. Se estes tentativas foram executadas localmente no sistema de Olá por um programa, Olá **processo** coluna seria que mostra o nome do processo de Olá. Em cenários em que a tentativa de início de sessão de Olá for proveniente de um programa, já tem o nome do processo Olá disponível e agora pode efetuar mais investigação no sistema de destino Olá.

## <a name="see-also"></a>Consultar também
Neste documento, aprendeu como toomonitor de solução de auditoria e segurança do OMS toouse os recursos. toolearn mais informações sobre a segurança do OMS, consulte Olá seguintes artigos:

* [Descrição geral do Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Introdução ao Operations Management Suite segurança e a solução de auditoria](oms-security-getting-started.md)
* [Monitorização e responder tooSecurity alertas no Operations Management Suite segurança e a solução de auditoria](oms-security-responding-alerts.md)

