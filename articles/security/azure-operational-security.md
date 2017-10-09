---
title: "aaaAzure segurança operacional | Microsoft Docs"
description: "Saiba mais sobre o Microsoft Operations Management Suite (OMS), os respetivos serviços e como funciona."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Segurança operacional do Azure
## <a name="introduction"></a>Introdução

### <a name="overview"></a>Descrição geral
Sabemos que a segurança está tarefa um na nuvem de Olá e como importante é que encontrará exatas e atempadas informações sobre a segurança do Azure. Uma das Olá melhor motivos toouse do Azure para as suas aplicações e serviços é tootake partido de grande Olá de ferramentas de segurança e funcionalidades disponíveis. Estas ferramentas e capacidades de ajudam a torná-lo toocreate possíveis soluções de segura na plataforma do Azure segura de Olá. O Microsoft Azure tem de fornecer confidencialidade, integridade e disponibilidade dos dados de cliente, permitindo também accountability transparente.

clientes toohelp compreender melhor a matriz de Olá de controlos de segurança implementado dentro do Microsoft Azure a partir de ambos os clientes de Olá e Microsoft operacionais das perspetivas, este documento técnico, "Azure operacional" segurança, é escrito que fornece um abrangente olhos segurança operacional Olá disponível com o Windows Azure.

### <a name="azure-platform"></a>Plataforma do Azure
Azure é uma plataforma de serviço de nuvem pública que suporta uma seleção abrangente dos sistemas operativos, programação idiomas, estruturas, ferramentas, bases de dados e dispositivos. Pode ser executado contentores de Linux com a integração do Docker; criar aplicações com JavaScript, Python, .NET, PHP, Java e Node.js; compilação back-ends para iOS, Android e Windows dispositivos. Serviço Cloud do Azure suporta Olá mesmas tecnologias milhões de programadores e profissionais de TI já dependem e de confiança.

Quando criar ou migrar os recursos IT à, um fornecedor de serviços de nuvem pública são depender tooprotect de capacidades da organização as suas aplicações e dados com os serviços de Olá e controlos de Olá fornecem toomanage Olá segurança da sua conta baseado na nuvem ativos.

Infraestrutura do Azure foi concebida de Olá instalações tooapplications para alojar milhões de clientes em simultâneo, e fornece uma base de confiança no qual as empresas podem cumprir os seus requisitos de segurança. Além disso, Azure disponibiliza uma vasta matriz de toocontrol de capacidade de segurança configuráveis opções e Olá-las de modo a que pode personalizar toomeet Olá exclusivo os requisitos de segurança de implementações da sua organização. Este documento será ajuda-o a compreender a segurança do Azure como capacidades podem ajudar a satisfazer estes requisitos.

### <a name="abstract"></a>Abstrato
Segurança operacionais do Azure refere-se os serviços de toohello, controlos e toousers disponíveis funcionalidades para proteger os seus dados, aplicações e outros recursos no Microsoft Azure. Segurança operacionais do Azure é construída numa estrutura que incorpora o conhecimento de Olá adquirido através de várias funcionalidades que são exclusivo tooMicrosoft, incluindo Olá Microsoft Security Development Lifecycle (SDL), Olá Microsoft Security Response Center programa e deteção profunda de Olá atuais das ameaças.

Este documento técnico descreve tooAzure de abordagem operacional de segurança da Microsoft na plataforma de nuvem do Microsoft Azure Olá e inclui os seguintes serviços:
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Centro de Segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Observador de rede do Azure](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Análise de armazenamento do Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) é Olá solução de gestão de IT para nuvem híbrida de Olá. Utilizado individualmente ou tooextend a implementação existente do System Center, OMS dá-lhe Olá flexibilidade máxima e controlo de gestão baseado na nuvem da sua infraestrutura.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

Com o OMS, pode gerir qualquer instância em nenhuma nuvem, incluindo no local, o Azure, AWS, Windows Server, o Linux, VMware e OpenStack, um custo mais baixo que soluções competitivos. Incorporado para Olá, mundo primeiro de nuvem, OMS oferece uma nova toomanaging de abordagem sua empresa que é Olá forma fácil e mais económica negócio novo toomeet desafia e acomodar novas cargas de trabalho, aplicações e ambientes de nuvem.

### <a name="oms-services"></a>Serviços do OMS

funcionalidade de principal de Olá do OMS é fornecida por um conjunto de serviços que são executados no Azure. Cada serviço fornece uma função de gestão específico e pode combinar os cenários de gestão diferentes tooachieve de serviços.

| Serviço  | Descrição|
| :------------- | :-------------|
| Log Analytics | Monitorizar e analisar a disponibilidade de Olá e o desempenho de recursos diferentes, incluindo físicos e máquinas virtuais. |
|Automatização | Automatizar processos manuais e impor configurações para computadores e máquinas virtuais. |
| Cópia de segurança | Cópia de segurança e restaurar dados críticos. |
| Site Recovery | Providenciar elevada disponibilidade para aplicações críticas. |

### <a name="log-analytics"></a>Log Analytics

O [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) oferece serviços de monitorização para o OMS, ao recolher dados de recursos geridos num repositório central. Estes dados podem incluir eventos, dados de desempenho ou dados personalizados fornecidos através de Olá API. Depois de recolhidos, dados de Olá estão disponíveis para alertas, análise e exportação.


Este método permite-lhe tooconsolidate dados de várias origens, pelo que pode combinar dados a partir do seu serviços do Azure com existentes no local ambiente. Também claramente separa coleção Olá dos dados de Olá da ação de Olá efetuada nos dados, para que todas as ações disponíveis tooall tipos de dados.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

Olá serviço análise de registos gere em segurança os dados baseados na nuvem utilizando Olá seguintes métodos:
-   segregação de dados
-   retenção de dados
-   segurança física
-   Gestão de incidentes
-   Conformidade
-   certificações de normas de segurança

### <a name="azure-backup"></a>Azure Backup

[Cópia de segurança do Azure](http://azure.microsoft.com/documentation/services/backup) fornece dados de cópia de segurança e restaurar os serviços e faz parte do conjunto OMS Olá dos produtos e serviços.
Protege os dados de aplicação e mantém-nos durante anos sem qualquer investimento de capital e com um mínimo de custos operacionais. -Pode cópias de segurança dos servidores de Windows físicas e virtuais além disso tooapplication cargas de trabalho, tais como o SQL Server e o SharePoint. Também pode ser utilizado por [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate protegidos tooAzure de dados para redundância e armazenamento de longa duração.


Os dados protegidos no Azure Backup são armazenados num cofre de cópias de segurança localizado numa região geográfica específica. Olá os dados são replicados no Olá mesma região e, dependendo do tipo de Olá de cofre, também pode ser replicada tooanother região para resiliência adicional.

### <a name="management-solutions"></a>Soluções de Gestão
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) é baseado na nuvem IT solução de gestão da Microsoft que o ajuda a gerir e proteger no local e a infraestrutura de nuvem.


[As soluções de gestão](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) prepackaged conjuntos de logics que implementam um cenário de gestão específico utilizando um ou mais serviços do OMS. Diferentes soluções estão disponíveis da Microsoft e de parceiros que pode adicionar facilmente tooyour subscrição do Azure tooincrease Olá valor seu investimento no OMS. Como parceiro, pode criar a suas próprias soluções toosupport as suas aplicações e serviços e forneça toousers através de Olá Azure Marketplace ou modelos de início rápido.


![Soluções de Gestão](./media/azure-operational-security/azure-operational-security-fig4.png)

Um bom exemplo de uma solução que utiliza várias funcionalidades adicionais de tooprovide serviços é Olá [solução de gestão de atualizações](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). Esta solução usa Olá [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) agente para o Windows e Linux toocollect informações sobre as atualizações necessárias em cada agente. Escreve este repositório de análise de registos de toohello dados onde pode analisá-lo com um dashboard incluído.

Quando cria uma implementação, os runbooks do [da automatização do Azure](https://docs.microsoft.com/azure/automation/automation-intro) tooinstall utilizados necessárias atualizações. Gerir este processo completo no portal de Olá e não precisa de tooworry sobre detalhes subjacente Olá.

## <a name="azure-security-center"></a>Centro de Segurança do Azure

Centro de segurança do Azure ajuda a proteger os seus recursos do Azure. Fornece gestão de políticas e monitorização de segurança integrada nas suas subscrições do Azure. No âmbito do serviço de Olá, conseguem toodefine políticas não apenas em relação a suas subscrições do Azure, mas também contra [grupos de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), pelo que pode ser mais granular.

### <a name="security-policies-and-recommendations"></a>Recomendações e políticas de segurança

Uma política de segurança define o conjunto de Olá de controlos, que são recomendados para recursos dentro Olá especificado subscrição ou grupo de recursos.

No Centro de segurança, é possível definir políticas de acordo com requisitos de segurança tooyour da empresa e do tipo de Olá de aplicações ou sensibilidade dos dados de Olá.

![Recomendações e políticas de segurança](./media/azure-operational-security/azure-operational-security-fig5.png)


As políticas que estão ativadas no nível de subscrição de Olá automaticamente propagadas tooall grupos de recursos dentro da subscrição Olá, conforme mostrado no diagrama de Olá no lado direito de Olá:


### <a name="data-collection"></a>Recolha de dados

Centro de segurança recolhe dados do seu tooassess de máquinas virtuais (VMs) respetivo estado de segurança, fornecer recomendações de segurança e alertá-lo toothreats. Quando o acesso do primeiro centro de segurança, a recolha de dados está ativado em todas as VMs na sua subscrição. Recomenda-se a recolha de dados, mas pode ativamente por desativar a recolha de dados no Olá política do Centro de segurança.

### <a name="data-sources"></a>Origens de dados

- Centro de segurança do Azure analisa os dados das Olá seguir visibilidade de tooprovide origens no seu estado de segurança, identificar vulnerabilidades Recomendamos mitigações e detetar ameaças Active Directory:

-   Serviços do Azure: Utiliza informações sobre a configuração de Olá dos serviços do Azure que implementou através da comunicação com o fornecedor de recursos desse serviço.

- Tráfego de Rede: utiliza metadados de tráfego de rede de amostragem da infraestrutura da Microsoft, tais como porta/IP de origem/destino, tamanho do pacote e protocolo de rede.

-   Soluções de Parceiros: utiliza alertas de segurança das soluções de parceiros integradas, tais como firewalls e soluções antimalware.

-   As suas Máquinas Virtuais: utiliza informações de configuração e informações sobre eventos de segurança, tais como eventos do Windows e registos de auditoria, registos do IIS, mensagens do syslog e ficheiros de informação de falha de sistema das suas máquinas virtuais.

### <a name="data-protection"></a>Proteção de dados

os clientes de toohelp evitar, detetarem e respondem toothreats, o Centro de segurança do Azure recolhe e processa dados relacionados com a segurança, incluindo informações de configuração, metadados, registos de eventos, ficheiros de informação de falha e muito mais. Microsoft respeita diretrizes de conformidade e segurança toostrict — desde a codificação toooperating um serviço.

-   **A segregação de dados**: dados são mantidos separados de forma lógica em cada componente em todo o serviço de Olá. Todos os dados são etiquetados por organização. Este tipo de etiquetagem persiste por todo o ciclo de vida do Olá dados e é imposto em cada camada de serviço Olá.

-   **Acesso a dados**: tooprovide recomendações de segurança e investigar potenciais ameaças de segurança, a equipa da Microsoft pode aceder às informações recolhidas ou analisados pelo serviços do Azure, incluindo ficheiros de informação de falha, a processar eventos de criação, disco VM instantâneos e artefactos, que podem incluir, involuntariamente, dados de cliente ou dados pessoais das suas máquinas virtuais. Respeitamos toohello [declaração de privacidade e termos de licenciamento Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), o estado de que a Microsoft não é utiliza dados de cliente ou derivará informações dos mesmos para quaisquer fins comerciais fim de publicidade ou semelhantes.

-   **Utilização de dados**: a Microsoft utiliza os padrões e ameaças vistas através dos vários inquilinos tooenhance nossas capacidades de prevenção e deteção; podemos fazê-lo de acordo com os compromissos de privacidade de Olá descritos na nossa [privacidade Instrução](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Localização dos dados

O Centro de Segurança do Azure recolhe cópias efémeras dos ficheiros de informação de falha de sistema e analisa-as para encontrar sinais de tentativas de exploração e casos em que a segurança tenha sido comprometida. Centro de segurança do Azure efetua esta análise na Olá mesma geografia como Olá área de trabalho e eliminações Olá cópias efémeras quando a análise estiver concluída. Artefactos de computador são armazenados centralmente na Olá mesma região, tal como Olá VM.

-   **As contas do Storage**: é especificada uma conta de armazenamento para cada região onde as máquinas virtuais estão em execução. Este permite toostore dados na mesma região que a máquina virtual de Olá do qual Olá os dados são recolhidos de Olá.

-   **Armazenamento do Centro de segurança do Azure**: informações sobre alertas de segurança, incluindo alertas de parceiro, recomendações e estado de funcionamento de segurança são armazenadas centralmente, atualmente na Olá dos Estados Unidos. Estas informações podem incluir informações de configuração relacionadas e eventos de segurança recolhidos das suas máquinas virtuais como tooprovide necessário com Olá segurança segurança, recomendação ou alerta de estado de funcionamento.


## <a name="azure-monitor"></a>Azure Monitor

Olá [segurança do OMS](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) e permite que solução de auditoria IT tooactively monitorizar todos os recursos, o que podem ajudar a minimiza o impacto de Olá de incidentes de segurança. Auditoria e segurança do OMS tem domínios de segurança que podem ser utilizados para monitorizar os recursos. domínio de segurança de Olá fornece acesso rápido toooptions, Olá de monitorização de segurança seguintes domínios são abordados em obter mais detalhes:

-   Avaliação de malware
-   Avaliação de atualização
-   Identidade e acesso.

Monitor do Azure fornece indicações tooinformation tipos específicos de recursos. Oferece visualização, consulta, encaminhamento, alertas, escala automática e automatização em dados de Olá infraestrutura do Azure (registo da atividade) e cada individuais (registos de diagnóstico) de recursos do Azure.

![Azure Monitor](./media/azure-operational-security/azure-operational-security-fig6.png)


Aplicações em nuvem são complexas com várias partes mover. A monitorização fornece tooensure de dados que a aplicação permanece cópias de segurança e em execução em bom estado. Também ajuda a toostave desativado potenciais problemas ou a resolução de problemas anteriores aqueles.

Além disso, pode utilizar a monitorização dados toogain conhecimentos aprofundados sobre a sua aplicação. Conhecimentos podem ajudá-lo tooimprove do desempenho de aplicações ou maintainability ou automatizar ações que caso contrário necessitem intervenção manual.

### <a name="azure-activity-log"></a>Registo de atividade do Azure


É um registo que fornece informações sobre as operações de Olá que foram efetuadas nos recursos na sua subscrição. Olá registo de atividade era anteriormente conhecida como "Registos de auditoria" ou "Registos operacionais", uma vez que os relatórios de eventos de controlo plane para as suas subscrições.

![Registo de atividade do Azure](./media/azure-operational-security/azure-operational-security-fig7.png)

Olá registo de atividade pode determinar Olá ' que, quem e quando ' para quaisquer operações (PUT, POST, DELETE) efetuadas nos recursos de Olá na sua subscrição de escrita. Também pode compreender o estado de Olá Olá da operação do e outras propriedades relevantes. Olá registo de atividade inclui leitura operações (GET) ou as operações para recursos que utilizam o modelo de clássico Olá.

### <a name="azure-diagnostic-logs"></a>Registos de diagnóstico do Azure

Estes registos são emitidos por um recurso e fornecerem dados avançados, frequentes sobre a operação de Olá desse recurso. conteúdo de Olá estes registos varia consoante o tipo de recurso.

Por exemplo, registos de sistema de eventos do Windows são uma categoria de registo de diagnóstico para VMs e blob, tabela e fila registos são categorias de registos de diagnóstico para contas de armazenamento.

Registos de diagnóstico é diferente do Olá [registo de atividade (anteriormente conhecido como registo de auditoria ou registo operacional)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). registo de atividade Olá fornece informações sobre as operações de Olá que foram efetuadas nos recursos na sua subscrição. Registos de diagnóstico fornecem informações aprofundadas operations que o seu recurso efetuadas em si.

### <a name="metrics"></a>Métricas

Monitor do Azure permite-lhe tooconsume telemetria toogain visibilidade desempenho Olá e estado de funcionamento das cargas de trabalho no Azure. Olá mais importantes dados de telemetria do Azure é métricas Olá (também denominadas de contadores de desempenho) emitidas pelo Azure mais recursos. Monitor do Azure fornece várias formas tooconfigure e consumir estes [métricas](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) para monitorização e resolução de problemas. As métricas são uma origem de telemetria importante e permitem-lhe Olá toodo seguintes tarefas:

-   **Monitorizar o desempenho de Olá** do seu recurso (por exemplo, uma aplicação VM, o Web site ou lógica) ao respetiva métricas num gráfico portal de desenho e afixação esse dashboard tooa do gráfico.

-   **Seja notificado de um problema** impactos Olá desempenho dos seus recursos, quando uma métrica atravesse um determinado limiar.

-   **Configurar as ações automatizadas**, tais como automática dimensionamento um recurso ou acionando um runbook quando uma métrica atravesse um determinado limiar.

-   **Efetuar análises avançadas** ou relatórios sobre tendências de desempenho ou a utilização do seu recurso.

-   **Arquivo** Olá histórico de desempenho ou o estado de funcionamento dos seus recursos para compatibilidade ou a fins de auditoria.

### <a name="azure-diagnostics"></a>Diagnóstico do Azure

É a capacidade de Olá no Azure que permite a recolha de Olá de dados de diagnóstico sobre uma aplicação implementada. Pode utilizar a extensão de diagnóstico de Olá de várias origens diferentes. São atualmente suportados [Web de serviço de nuvem do Azure e funções de trabalho](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [Virtual Machines do Azure](https://docs.microsoft.com/azure/virtual-machines/windows/overview) com o Microsoft Windows, e [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Outros serviços do Azure têm os seus próprios diagnóstico separado.

## <a name="azure-network-watcher"></a>Observador de rede do Azure

Auditoria de segurança de rede é vital para detetar vulnerabilidades de rede e garantir a conformidade com a segurança de TI e o modelo de regulamentação de governação. Vista de grupo de segurança, pode obter as regras do grupo de segurança de rede e segurança do Olá configurado e Olá regras de segurança eficaz. Com Olá obter lista de regras aplicadas, poderá determinar Olá as portas são abertas e avaliar a vulnerabilidade de rede.

[Observador de rede](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) é um serviço regional que permite-lhe toomonitor e diagnosticar condições a um nível de rede no, a e do Azure. Diagnóstico de rede e ferramentas de visualização disponíveis com o observador de rede ajudam-na compreender, diagnosticar e obter a rede de tooyour insights no Azure. Este serviço inclui a captura de pacotes, o salto seguinte, o fluxo IP verificar, a vista de grupo de segurança, os registos de fluxo NSG. A monitorização ao nível do cenário fornece uma vista de tooend final dos recursos de rede em contraste tooindividual recursos a monitorização da rede.

![Observador de rede do Azure](./media/azure-operational-security/azure-operational-security-fig8.png)

Observador de rede tem atualmente Olá seguintes capacidades:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Registos de auditoria</a>**-operações efetuadas como parte da configuração de Olá de redes são registados. Estes registos podem ser visualizados no Olá portal do Azure ou obtidos através de ferramentas da Microsoft, tais como o Power BI ou ferramentas de terceiros. Os registos de auditoria estão disponíveis através do portal de Olá, do PowerShell, CLI e Rest API. Para obter mais informações sobre os registos de auditoria, consulte operações de auditoria com o Resource Manager. Os registos de auditoria estão disponíveis para operações efetuadas em todos os recursos de rede.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">Fluxo IP verifica </a>**  -verifica se a um pacote é permitido ou negado com base nos parâmetros de pacotes de 5 cadeias de identificação do fluxo informações (IP de destino, IP de origem, porta de destino, porta de origem e protocolo). Se o pacote Olá é negado por um grupo de segurança de rede, é devolvido regra Olá e grupo de segurança de rede que negado pacotes hello.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Próximo salto</a>**  -determina o salto seguinte do Olá para pacotes a ser encaminhado no Olá infraestrutura de rede do Azure, permitindo-lhe rotas toodiagnose qualquer configurados incorretamente definida pelo utilizador.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Vista do grupo de segurança</a>**  -obtém as regras de segurança eficaz e aplicados Olá que são aplicadas numa VM.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">O registo de fluxo de NSG</a>**  -registos de fluxo para grupos de segurança de rede, permitem-lhe toocapture registos tootraffic relacionados que é permitido ou negado por regras de segurança de Olá no grupo de Olá. fluxo de Olá é definido por uma informação de 5 cadeias de identificação – IP de origem, IP de destino, porta de origem, porta de destino e protocolo.

## <a name="azure-storage-analytics"></a>Análise do Armazenamento do Azure

[Análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) pode armazenar métricas que incluem dados de capacidade e estatísticas agregadas de transações sobre o serviço de armazenamento de tooa de pedidos. As transações são reportadas ao nível da operação ambas Olá API e nível de serviço de armazenamento de Olá e capacidade é reportada ao nível de serviço de armazenamento Olá. Dados de métricas pode ser a utilização do serviço de armazenamento de tooanalyze utilizado, diagnosticar problemas com pedidos efetuados contra o serviço de armazenamento Olá e desempenho de Olá tooimprove das aplicações que utilizam um serviço.

[Análise de armazenamento do Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) efetua o registo e fornece dados de métricas para uma conta de armazenamento. Pode utilizar esta pedidos de tootrace de dados, analisar tendências de utilização e diagnosticar problemas com a sua conta de armazenamento. Registo de análise de armazenamento está disponível para Olá [serviços tabela, fila e Blob](https://docs.microsoft.com/azure/storage/storage-introduction). Análise de armazenamento regista informações detalhadas sobre o serviço de armazenamento de tooa pedidos com êxito ou falhada.

Estas informações podem ser utilizados toomonitor de pedidos individuais e toodiagnose problemas com um serviço de armazenamento. Pedidos são registados numa base de melhor esforço. Entradas de registo são criadas apenas se não existirem pedidos efetuados contra o ponto final de serviço Olá. Para o exemplo se uma conta de armazenamento tem de atividade no respetivo ponto final do Blob, mas não no respetivos pontos finais de tabelas ou filas, apenas os registos relativos toohello serviço Blob é criado.

Análise de armazenamento toouse, terá de a ativar individualmente para cada serviço pretende toomonitor. Pode ativá-la no Olá [portal do Azure](https://portal.azure.com/); para obter mais informações, consulte [monitorizar uma conta de armazenamento no portal do Azure de Olá](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). Também pode ativar a análise de armazenamento através de programação através de Olá REST API ou biblioteca de clientes Olá. Utilize Olá definir propriedades de serviço operação tooenable análise de armazenamento individualmente para cada serviço.

Olá agregados dados são armazenados num blob bem conhecido (para o registo) e em tabelas bem conhecidas (para métricas), que podem ser acedidas com o serviço de Blob Olá e APIs de serviço tabela.

Análise de armazenamento tem um limite de 20 TB quantidade Olá dos dados armazenados que seja independentes do limite total de Olá para a sua conta de armazenamento. Todos os registos são armazenados no [blobs de blocos](https://docs.microsoft.com/azure/storage/storage-analytics) num contentor com o nome $logs, que são criados automaticamente quando a análise de armazenamento está ativada para uma conta de armazenamento.

Olá seguintes ações executadas pela análise de armazenamento é sujeito a faturação:

-   Blobs toocreate de pedidos de registo
-   Pedidos toocreate as entidades da tabela de métricas.

> [!Note]
> Para obter mais informações sobre as políticas de retenção de dados e de faturação, consulte [faturação e de análise de armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing).
> Para um desempenho ideal, quer toolimit Olá diversas altamente sobreutilizados discos anexados toohello máquina virtual tooavoid possíveis de limitação. Se todos os discos não estão a ser altamente utilizados em Olá mesmo tempo, conta de armazenamento Olá pode suportar um maior disco número.

> [!Note]
> Para obter mais informações sobre limites de conta de armazenamento, consulte [metas de desempenho e escalabilidade do Storage do Azure](https://docs.microsoft.com/azure/storage/storage-scalability-targets).


Olá, os seguintes tipos de pedidos autenticados e anónimos é registado.

| Autenticado  | Anónimo|
| :------------- | :-------------|
| Pedidos com êxito | Pedidos com êxito |
|Falha de pedidos, incluindo o tempo limite, limitação, rede, autorização e outros erros | Pedidos utilizando um acesso assinatura partilhado (SAS), incluindo pedidos falhados e bem-sucedidas |
| Pedidos utilizando um acesso assinatura partilhado (SAS), incluindo pedidos falhados e bem-sucedidas |Erros de tempo limite para o cliente e servidor |
|   Dados de tooanalytics de pedidos |    Pedidos falhados de GET com o código de erro 304 (não modificados) |
| Pedidos efetuados pelo armazenamento Analytics ela própria, tal como criação de registo ou eliminação, não são registados. Uma lista completa dos dados de Olá registado está documentada na Olá [operações de registadas análise de armazenamento e as mensagens de estado](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato de registo de análise do armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) tópicos. | Todos os outros pedidos anónimos falhados não são registados. Uma lista completa dos dados de Olá registado está documentada na Olá [operações de registadas análise de armazenamento e as mensagens de estado](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato de registo de análise do armazenamento](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD também inclui um conjunto completo de capacidades de gestão de identidade, incluindo autenticação multifator, registo de dispositivos, gestão de palavra-passe self-service, gestão de grupos self-service, gestão de contas com privilégios, controlo de acesso baseado em funções, monitorização de utilização de aplicações, avançado auditoria e monitorização e alertas de segurança.

-   Melhore a segurança de aplicação com a autenticação multifator do Azure AD e o acesso condicional.

-   Monitorizar a utilização da aplicação e proteger a sua empresa contra ameaças avançadas com relatórios e monitorização de segurança.

O Azure Active Directory (Azure AD) inclui relatórios de segurança, atividade e auditoria para o diretório. [Olá relatório de auditoria do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) ajuda os clientes tooidentify privilegiado ações ocorridas no seu Azure Active Directory. Ações privilegiadas incluem alterações de elevação (por exemplo, a criação de função ou reposições de palavra-passe), alterar as configurações da política (por exemplo políticas de palavra-passe), ou a configuração de toodirectory alterações (por exemplo, alterações toodomain Federação definições).

os relatórios de Olá fornecem o registo de auditoria Olá para o nome do evento Olá, ator Olá que efetuou a ação de Olá, recurso de destino Olá afetado pela alteração Olá e de data de Olá e de tempo (em UTC). Os clientes são a lista de Olá tooretrieve capaz de eventos de auditoria para o seu Azure Active Directory através de Olá [portal do Azure](https://portal.azure.com/), conforme descrito nas [ver os registos de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Eis uma lista de relatórios de Olá incluídos:

| Relatórios de segurança  | Relatórios de atividade| Relatórios de auditoria |
| :------------- | :-------------| :-------------|
|Inícios de sessão de fontes desconhecidas | Utilização da aplicação: resumo | Relatório de auditoria de diretório |
|Inícios de sessão após várias falhas | Utilização da aplicação: detalhado |   |
|Inícios de sessão de várias localizações geográficas | Dashboard de aplicações |  |
|Inícios de sessão de endereços IP com atividade suspeita |Erros de aprovisionamento de contas |  |
|Atividades irregulares de início de sessão |Dispositivos de utilizadores individuais |  |
|Inícios de sessão de dispositivos possivelmente infetados |Atividade de utilizadores individuais |   |
|Utilizadores com atividade anómala de início de sessão |Relatório de atividade de grupos |   |
| |Relatório de atividade de registo de reposição de palavra-passe |   |
| |Atividade de reposição de palavra-passe |   | |



dados de Olá destes relatórios podem ser úteis tooyour aplicações, como sistemas SIEM, auditoria e ferramentas de business intelligence. relatórios de Olá do Azure AD [APIs](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) fornecer acesso programático toohello dados através de um conjunto de APIs baseado em REST. Pode chamar estas APIs a partir de vários idiomas e as ferramentas de programação.

Eventos na Olá relatório de auditoria do Azure AD são retidos durante 180 dias.

> [!Note]
> Para obter mais informações sobre a retenção em relatórios, consulte [políticas de retenção de relatório do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Para os clientes interessados em armazenar as respetivas [eventos de auditoria](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) para períodos de retenção mais longos, hello API de relatórios podem ser utilizados tooregularly solicitação eventos de auditoria para um arquivo de dados separada.

## <a name="summary"></a>Resumo

Este resumos de artigo proteger a sua privacidade e proteger os seus dados, durante a distribuição de software e serviços que o ajudam a gerir Olá infraestrutura de TI da sua organização. Microsoft reconhece que, quando estes entrust tooothers os seus dados, essa confiança requer a segurança rigorosas. Microsoft respeita diretrizes de conformidade e segurança toostrict — desde a codificação toooperating um serviço. Proteger e a proteção de dados é uma prioridade superior na Microsoft.

Este artigo explica

-   Como dados são recolhidos, processados e protegidos Olá Operations Management Suite (OMS).

-   Analise rapidamente eventos em várias origens de dados. Identificar riscos de segurança e compreender o âmbito de Olá e o impacto de ameaças e ataques de danos de Olá de toomitigate de uma violação de segurança.

-   Identifique padrões de ataque ao ver o tráfego IP malicioso de saída e os tipos de ameaças maliciosas. Compreenda a postura de segurança de Olá de todo o seu ambiente, independentemente da plataforma.

-   Capture todas as Olá registo e evento dados necessários para uma auditoria de segurança ou a conformidade. Recursos e tempo de Olá barra necessário toosupply com um completo, pesquisável e exportável registo e evento conjunto de dados de auditoria de segurança.

<ul>
<li>Recolha eventos relacionados com segurança, auditoria e análise de violação tookeep um fecho eye seus ativos:</li>
<ul>
<li>Postura de segurança</li>
<li>Problema relevantes</li>
<li>Ameaças resumos</li>
</ul>
</ul>

## <a name="next-steps"></a>Passos Seguintes

- [Conceção e segurança operacional](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft designs os respetivos serviços e software com a segurança em mente toohelp Certifique-se de que a respetiva infraestrutura de nuvem é resiliente e defended contra ataques.

- [Operations Management Suite | Segurança e conformidade](https://www.microsoft.com/cloud-platform/security-and-compliance)

Utilizar o Microsoft segurança dados e análise tooperform mais inteligente e eficaz deteção de ameaças.

- [Operações e planeamento do Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) um conjunto de passos e tarefas que pode seguir toooptimize a utilização do Centro de segurança com base nos requisitos de segurança da sua organização e o modelo de gestão de nuvem.

