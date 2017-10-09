---
title: "aaaGetting iniciado com segurança do Operations Management Suite e uma solução de auditoria | Microsoft Docs"
description: "Isto ajuda a documento tooget começar a utilizar auditoria e segurança do Operations Management Suite toomonitor de capacidades de solução da nuvem híbrida."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>Introdução à Solução de Segurança e Auditoria do Operations Management Suite
Este documento ajuda-o a começar rapidamente com as funções da solução de Segurança e Auditoria do Operations Management Suite (OMS) guiando-o ao longo de cada opção.

## <a name="what-is-oms"></a>O que é o OMS?
O Microsoft Operations Management Suite (OMS) é a solução de gestão de TI baseada na nuvem da Microsoft que o ajuda a gerir e a proteger a sua infraestrutura no local e na nuvem. Para obter mais informações sobre o OMS, leia o artigo de Olá [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="oms-security-and-audit-dashboard"></a>Dashboard de Segurança e Auditoria do OMS
Olá auditoria e segurança do OMS solução fornece uma vista abrangente da sua organização postura de segurança IT com consultas de pesquisa incorporadas para problemas relevantes que necessitam da sua atenção. Olá **auditoria e segurança** dashboard é ecrã principal de Olá para tudo toosecurity no OMS. Fornece informações de alto nível sobre estado de segurança de Olá dos seus computadores. Também inclui Olá capacidade tooview todos os eventos de Olá passado 24 horas, 7 dias, ou qualquer outro período de tempo personalizado. Olá tooaccess **auditoria e segurança** dashboard, siga estes passos:

1. No Olá **Microsoft Operations Management Suite** dashboard principal, clique em **definições** mosaico no Olá esquerdo.
2. No Olá **definições** painel, em **soluções** clique **auditoria e segurança** opção.
3. Olá **auditoria e segurança** dashboard é apresentado:
   
    ![Dashboard de Segurança e Auditoria do OMS](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

Se que está a aceder a este dashboard para Olá pela primeira vez e não tiver dispositivos monitorizados pelo OMS, Olá mosaicos não serão preenchidos com os dados obtidos a partir do agente de Olá. Depois de instalar o agente de Olá, pode demorar algum tempo toopopulate, por conseguinte, o que veem inicialmente poderá estar em falta alguns dados como ainda estiver a carregar toohello nuvem.  Neste caso, é normal toosee algumas os mosaicos sem informações tangible. Leitura [computadores Windows ligar diretamente tooOMS](https://technet.microsoft.com/library/mt484108.aspx) para obter mais informações sobre como agente do OMS tooinstall num sistema Windows e [Linux ligar computadores tooOMS](https://technet.microsoft.com/library/mt622052.aspx) para obter mais informações sobre como tooperform esta tarefa num sistema Linux.

> [!NOTE]
> agente de Olá recolhe informações de Olá com base em Olá atual eventos que estão ativados, por exemplo, nome do computador, nome de utilizador e de endereço IP. No entanto, nenhum documento/ficheiros, nome de base de dados ou dados privados são recolhidos.   
> 
> 

As soluções são uma coleção de regras de aquisição de dados, de lógica e de visualização para lidar com dificuldades principais do cliente. A Segurança e Auditoria é uma solução, outras podem ser adicionadas separadamente. Artigo de Olá leitura [adicionar soluções](https://technet.microsoft.com/library/mt674635.aspx) para obter mais informações sobre como tooadd uma nova solução.

dashboard de auditoria e segurança do OMS Olá está organizado em quatro categorias principais:

* **Domínios de segurança**: nesta área será capaz de toofurther explorar os registos de segurança ao longo do tempo, aceder a avaliação de malware, atualizar a avaliação, segurança de rede, informações de identidade e acesso, os computadores com eventos de segurança e tivessem dashboard do Centro de segurança de acesso tooAzure.
* **Problemas relevantes**: esta opção permitirá tooquickly identificar o número de Olá de problemas de Active Directory e Olá gravidade estes problemas.
* **As deteções (pré-visualização)**: permite-lhe padrões de ataque tooidentify por visualizar alertas de segurança que possam ocorrer relativamente aos seus recursos.
* **Ameaça Intelligence**: permite-lhe tooidentify padrões de ataque ao visualizar o número total de Olá de servidores com tráfego IP malicioso de saída, tipo de ameaça malicioso Olá e um mapa que mostra onde são feitos destes IPs. 
* **Consultas de segurança comuns**: esta opção fornece a uma lista de segurança mais comuns Olá consultas que pode ser utilizado toomonitor seu ambiente. Ao clicar destas consultas, é aberto Olá **pesquisa** painel com resultados de Olá para essa consulta.

> [!NOTE]
> para obter mais informações sobre como o OMS mantém os dados seguros, leia Como o OMS protege os dados.
> 
> 

## <a name="security-domains"></a>Domínios de segurança
Quando a monitorização de recursos, é importante toobe tooquickly capaz de acesso Olá estado atual do seu ambiente. No entanto, também é importante toobe tootrack capaz de eventos de back-ocorridas nos Olá anterior que pode conduzir tooa uma melhor compreensão sobre o que acontece no seu ambiente em determinado ponto no tempo. 

> [!NOTE]
> retenção de dados está de acordo com o plano de preços do toohello OMS. Para obter mais informações, visite Olá [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx) página de preços.
> 
> 

Cenários de investigação de resposta e forense incidentes diretamente beneficiarão de resultados de Olá disponíveis no Olá **registos de segurança ao longo do tempo** mosaico.

![Registos de segurança ao longo do tempo](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

Quando clica neste mosaico, Olá **pesquisa** painel será aberto, que mostra um resultado de consulta para **eventos de segurança** (tipo = SecurityEvents) com dados baseados no Olá últimos sete dias, como mostrado abaixo:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Registos de segurança ao longo do tempo](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

resultado da pesquisa Olá está dividido em dois painéis: painel esquerdo Olá dá-lhe uma análise detalhada do número de Olá dos eventos de segurança que foram encontrados computadores Olá em que foram encontradas estes eventos, número de Olá de contas que foram detetados nestes computadores e tipos de Olá de Atividades. painel direito Olá fornece resultados total Olá e uma vista cronológica Olá de eventos de segurança com a atividade do computador Olá de nome e o evento. Também pode clicar em **mostrar mais** tooview mais detalhes sobre este evento, tais como dados de eventos de Olá, ID de evento Olá e origem de evento Olá.

> [!NOTE]
> Para obter mais informações sobre a consulta de pesquisa do OMS, leia [Referência de pesquisa do OMS](https://technet.microsoft.com/library/mt450427.aspx).
> 
> 

### <a name="antimalware-assessment"></a>Avaliação de antimalware
Este ativa a opção tooquickly identificam os computadores com proteção insuficiente e computadores que sejam comprometidos por um software maligno. Avaliação de malware Estado ameaças detetadas em servidores de Olá monitorizado são lidas e, em seguida, Olá dados é enviada o serviço OMS toohello na nuvem de Olá para processamento. Servidores com ameaças detetadas e os servidores com proteção insuficiente são apresentadas no dashboard de avaliação do Olá software maligno, que é acessível depois de clicar em Olá **Antimalware avaliação** mosaico. 

![avaliação de software maligno](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

Tal como quaisquer outro mosaico em direto disponível no Dashboard do OMS, ao clicar nela, Olá **pesquisa** painel será aberto com o resultado da consulta Olá. Para esta opção, se clicar no Olá **não Reporting** opção em **estado de proteção**, terá de resultado da consulta Olá que mostra esta entrada único que contém o nome do computador Olá e respetiva classificação, como mostrado abaixo:

![resultado da pesquisa](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *classificação* é um nível dá ao estado de Olá tooreflect de proteção de Olá (, desativar, atualizar, etc.) e ameaças que sejam encontradas. Com que o como um número toomake agregações da ajuda.
> 
> 

Se clicar no nome do computador Olá, terá de vista de cronológica Olá do Estado de proteção Olá neste computador. Isto é muito útil para cenários nos quais tem de toounderstand se Olá antimalware foi instalado e em algum momento foi removido.   

### <a name="update-assessment"></a>Avaliação de atualização
Ativa esta opção determinar tooquickly Olá problemas de segurança de toopotential exposição geral e se ou crítica estas atualizações são para o seu ambiente. Solução de auditoria e de segurança do OMS fornecem apenas visualização Olá destas atualizações, dados reais Olá vêm [soluções de gestão de atualização](oms-solution-update-management.md), que é um módulo diferente dentro do OMS. Um exemplo de Olá atualizações aqui:

![atualizações do sistema](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> Para obter mais informações sobre a solução de Gestão de Atualizações, leia [Update Management solution in OMS (Solução de Gestão de Atualizações no OMS)](oms-solution-update-management.md).
> 
> 

### <a name="identity-and-access"></a>Identidade e Acesso
Identidade deve ser um controlo de Olá plane para a sua empresa, a proteger a sua identidade deve ser a sua prioridade superior. Enquanto no Olá anterior foram perimeters em torno organizações e essas perimeters foram um dos limites de defesas primário Olá, nowadays com mais dados e aplicações mais mover toohello nuvem identidade Olá torna-se perímetro Olá de novo. 

> [!NOTE]
> atualmente dados Olá baseia-se apenas nos dados de início de sessão de eventos de segurança (evento ID 4624) de inícios de sessão Olá futuros Office 365 e dados do Azure AD também serão incluídos.
> 
> 

Através da monitorização de atividades a identidade será capaz de tootake pró-ativas antes de um incidente local ou ações reativa toostop uma tentativa de ataque. Olá **identidades e acessos** dashboard fornece uma descrição geral do seu estado de identidade, incluindo Olá número de tentativas falhadas toolog, Olá conta do utilizador em que foram utilizados durante essas tentativas, as contas que foram bloqueadas, contas com alteraram ou repor a palavra-passe e, atualmente, número de contas que são registados no. 

Quando clica no Olá **identidades e acessos** mosaico verá Olá dashboard os seguintes:

![identidade e acesso](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

informações de Olá disponíveis neste dashboard imediatamente podem ajudar tooidentify uma atividade suspeita potencial. Por exemplo, não existem 338 tentativas toolog no como **administrador** e 100% destes tentativas falhou. Isto pode ser causado por um ataque de força bruta contra esta conta. Se clicar nesta conta irá obter mais informações que podem ajudá-lo recurso de destino Olá toodetermine para este ataque potencial:

![resultados de pesquisa](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

Olá relatório detalhado fornece informações importantes sobre este evento, incluindo: computador de destino Olá, tipo de Olá de início de sessão (neste cenário início de sessão de rede), a atividade de Olá (neste evento maiúsculas 4625) e uma linha cronológica abrangente de cada tentativa. 

### <a name="computers"></a>Computadores
Este mosaico podem ser utilizados tooaccess todos os computadores que tenham ativamente eventos de segurança. Quando clica neste mosaico irão ver a lista de Olá de computadores com eventos de segurança e o número de Olá de eventos em cada computador:

![Computadores](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

Pode continuar a investigação, clicando em cada computador e rever eventos de segurança de Olá que foram sinalizados.

### <a name="threat-intelligence"></a>Informações sobre Ameaças

Ao utilizar a opção de ameaças de Olá disponível na auditoria e segurança do OMS, os administradores de TI pode identificar ameaças de segurança no ambiente de Olá, por exemplo, identificar se um determinado computador faz parte de um botnet dedicado. Computadores podem tornar-se nós de um botnet quando os atacantes ilicitamente instalar software maligno que liga secretly este comando de toohello do computador e o controlo. Também poderá identificar potenciais ameaças provenientes de canais de comunicação underground, como o darknet. Obter mais informações sobre ameaças o lendo [toosecurity de monitorização e de que responde alertas no Operations Management Suite segurança e a solução de auditoria](oms-security-responding-alerts.md) artigo.

Em alguns cenários, pode observar um IP potencialmente mal-intencionado que foi acedido a partir de um computador monitorizado:

![mapa de informações sobre ameaças](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

Este alerta e outras pessoas dentro Olá mesma categoria, são gerados através de segurança do OMS através do aproveitamento [ameaças da Microsoft](https://youtu.be/O4WtxgUrDc8). Olá dados de ameaças é recolhida pela Microsoft, bem como comprado junto de fornecedores de intelligence ameaça à esquerda. Estes dados são atualizados frequentemente e adaptada descritos mover de toofast ameaças. Devido a natureza tooits, devem ser combinada com outras fontes de informação de segurança ao [investigar](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) um alerta de segurança. 

### <a name="baseline-assessment"></a>Avaliação da Linha de Base

A Microsoft, juntamente com o setor e as organizações governamentais em todo o mundo, define uma configuração do Windows que representa implementações de servidor altamente seguras. Esta configuração é um conjunto de chaves de registo, definições de política de auditoria e definições de política de segurança juntamente com os valores recomendados da Microsoft para estas definições. Este conjunto de regras é conhecido como linha de base de Segurança. Leia [Avaliação da Linha de Base em Solução de Segurança e Auditoria do Operations Management Suite](oms-security-baseline.md) para obter mais informações sobre esta opção.

### <a name="azure-security-center"></a>Centro de Segurança do Azure
Este mosaico é basicamente um dashboard do atalho tooaccess Centro de segurança do Azure. Leia [Introdução ao Centro de Segurança do Azure](../security-center/security-center-get-started.md) para obter mais informações sobre esta solução.

## <a name="notable-issues"></a>Problemas relevantes
Olá objetivo principal deste grupo de opções é tooprovide uma vista rápida dos problemas de Olá que tem no seu ambiente, por categorizá-los no crítico, aviso e informativo. Olá mosaico de tipo de problema do Active Directory é uma visualização estes problemas, mas não permite tooexplore mais detalhes sobre os mesmos, para que precisa de toouse parte inferior do Olá deste mosaico com nome Olá problema de Olá (nome), como muitos objetos tinha isto acontecer (número) e como é crítica (GRAVIDADE).

![Problemas relevantes](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

Pode ver que estes problemas já foram abordados em diferentes áreas de Olá **segurança domínios** grupo, que reinforces intenção Olá esta vista: visualizar Olá mais importantes no seu ambiente de um único local.

## <a name="detections-preview"></a>Deteções (Pré-visualização)
Olá principal objetivo esta opção é tooallow IT tooquickly identificar potenciais ambiente de tootheir ameaças através de e gravidade Olá esta ameaça.

![Informações sobre Ameaças](./media/oms-security-getting-started/oms-getting-started-fig12.png)

Esta opção também pode ser utilizada durante uma [investigação de resposta a incidentes](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) tooperform Olá assessment e obter mais informações sobre o ataque Olá.

> [!NOTE]
> Para obter mais informações sobre como toouse OMS para resposta a incidentes, veja este vídeo: [como tooLeverage Olá Centro de segurança do Azure e do Microsoft Operations Management Suite para uma resposta a incidentes](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703).
> 
> 

## <a name="threat-intelligence"></a>Informações sobre Ameaças
Olá ameaça nova secção intelligence da solução de auditoria e segurança Olá visualiza padrões de ataque possíveis Olá de várias maneiras: Olá número total de servidores com tráfego IP malicioso de saída, Olá tipo ameaça malicioso e um mapa que mostra onde estes IPs são provenientes da. Pode interagir com o mapa de Olá e clique em Olá IPs para obter mais informações.

Pushpins amarelo no mapa de Olá indicar que o tráfego de entrada de IPs maliciosos. Não é invulgar para servidores que estão expostas toohello internet toosee malicioso tráfego de entrada, mas recomendamos que reveja estes toomake tentativas se de que nenhum do foi concluída com êxito. Estes indicadores baseiam-se nos registos do IIS, no WireData e nos registos de Firewall do Windows.  

![Informações sobre Ameaças](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>Consultas de segurança comuns
lista de Olá de consultas de segurança comuns disponíveis pode ser útil para obter informações de toorapidly acesso do recurso e personalizá-lo com base nas necessidades do seu ambiente. Estas consultas comuns são:

* todas as Atividades de Segurança
* Atividades de segurança no Olá computador \ "computador01.contoso.com \" (substituir pelo nome do seu computador)
* Atividades de segurança no Olá computador \ "computador01.contoso.com \" para a conta "Administrador" (substituir com os seus próprios nomes de computador e da conta)
* atividade de Início de Sessão por Computador
* contas que terminaram o antimalware da Microsoft em qualquer computador
* Computadores nos quais foi terminado Olá processo de antimalware da Microsoft
* computadores nos quais foi executado o "hash.exe" (substitua com um nome de processo diferente)
* todos os nomes de Processo que foram executados
* atividade de Início de Sessão por Conta
* Contas que iniciaram sessão remotamente em Olá computador \ "computador01.contoso.com \" (substituir pelo nome do seu computador)

## <a name="see-also"></a>Consultar também
Neste documento, foram introduzidas tooOMS solução de auditoria e segurança. toolearn mais informações sobre a segurança do OMS, consulte Olá seguintes artigos:

* [Descrição geral do Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorização e responder tooSecurity alertas no Operations Management Suite segurança e a solução de auditoria](oms-security-responding-alerts.md)
* [Recursos de Monitorização na Solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

