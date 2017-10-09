---
title: "aaaOperations descrição geral da gestão Suite (OMS) | Microsoft Docs"
description: "O Microsoft Operations Management Suite (OMS) é a solução de gestão de TI baseada na nuvem da Microsoft que o ajuda a gerir e a proteger a sua infraestrutura no local e na nuvem.  Este artigo descreve o valor de Olá do OMS, identifica os diferentes serviços de Olá e ofertas incluídas no OMS e fornece ligações tootheir detalhadas conteúdo."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>O que é o Operations Management Suite (OMS)?
Este artigo fornece uma introdução tooOperations Management Suite (OMS), incluindo uma breve descrição geral de valor de negócio Olá fornece, soluções de serviços e a gestão de Olá inclui e ofertas de Olá pacote em conjunto diferentes serviços e soluções.  As ligações são incluídas toohello detalhadas documentação sobre como implementar e utilizar cada serviço e a solução.

## <a name="from-on-premises-toohello-cloud"></a>De nuvem de toohello no local
A Microsoft disponibiliza há muito tempo produtos para gerir ambientes empresariais.  Vários produtos foram consolidados num conjunto de produtos de gestão do System Center de Olá no 2007.  Isto incluído o Configuration Manager que fornece funcionalidades como a distribuição de software e inventário, Operations Manager, que fornece a monitorização proativa de aplicações e sistemas do Orchestrator que inclui processos manuais do tooautomate runbooks e Data Protection Manager para cópia de segurança e recuperação de dados críticos.

Com mais recursos informáticos mover toohello cloud, os produtos do System Center adquiridos mais funcionalidades de nuvem, tais como o Operations Manager e o Orchestrator gerir recursos no Azure.  Contudo, ainda eram essencialmente concebidos como soluções no local e exigiam um investimento significativo na implementação e manutenção do ambiente de gestão no local.  toocompletely tirar partido de nuvem Olá e suportar futuras aplicações, um novo toomanagement de abordagem foi necessária.

## <a name="introducing-operations-management-suite"></a>Introdução ao Operations Management Suite
Operations Management Suite (também conhecido como OMS) é uma coleção de serviços de gestão que foram concebidos na nuvem de Olá desde o início de Olá.  Em vez de implementar e gerir recursos no local, os componentes do OMS estão totalmente alojados no Azure.  A configuração é mínima e pode começar a utilizá-lo numa questão de minutos.  

- **Custo e complexidade da implementação mínimos.**  Porque todos os componentes de Olá e os dados para OMS são armazenados no Azure, pode ter a cópia de segurança e em execução num curto período de tempo sem Olá complexidade e o investimento no local componentes.
- **Níveis de toocloud de escala.**  Não tem tooworry sobre pagar com recursos de computação que não precisa de ou sobre a ficar sem espaço de armazenamento desde Olá nuvem permite-lhe toopay apenas para que, na verdade, utilizar e prontamente sejam dimensionadas de carga tooany que precisa.  Pode começar por gerir alguns recursos tooget, que foi iniciado e, em seguida, aumentar verticalmente tooyour todo o ambiente.
- **Tire partido das funcionalidades mais recentes Olá.**  São constantemente adicionadas e atualizadas as funcionalidades dos serviços do OMS.  Constantemente a ter acesso toohello funcionalidades mais recentes sem quaisquer atualizações de toodeploy requisito.
- **Serviços integrados.**  Enquanto cada um dos serviços OMS Olá fornecer valor significativo no seu próprio, estes podem trabalhar em conjunto toosolve cenários de gestão complexa.  Por exemplo, um runbook na automatização do Azure pode unidade um processo de ativação pós-falha com o Azure Site Recovery e, em seguida, inicie sessão informações tooLog análise toogenerate um alerta.
- **Conhecimento global.**  As soluções de gestão no OMS continuamente tem informações mais recentes do acesso toohello.  Olá solução de auditoria e segurança, por exemplo, pode executar uma análise de ameaças com ameaças mais recentes Olá sejam detetadas em torno Olá mundo.
- **Acesso em qualquer local.**  Aceda ao seu ambiente de gestão em qualquer local onde tenha um browser.  Instale aplicação da OMS de Olá no smartphone para dados de monitorização do acesso pronto tooyour.

### <a name="is-it-just-for-hello-cloud"></a>É apenas para a nuvem de Olá?
Apenas porque os serviços do OMS são executados nuvem de Olá não significa que eles não é possível gerir de forma eficaz o ambiente no local.  Colocar um agente em todas as janelas ou computador com Linux no seu centro de dados e enviará tooLog dados análise onde pode ser analisado juntamente com todos os outros dados recolhidos a partir de serviços em nuvem ou no local.  Utilize a cópia de segurança do Azure e o Azure Site Recovery cloud de Olá tooleverage para cópia de segurança e a elevada disponibilidade para recursos no local.  
Os Runbooks na nuvem de Olá normalmente não é possível aceder os recursos no local, mas pode instalar um agente num ou mais computadores demasiado que irá alojar os runbooks no seu centro de dados.  Quando inicia um runbook, basta especificar se quiser toorun na nuvem de Olá ou uma função de trabalho local.

## <a name="hybrid-management-with-system-center"></a>Gestão híbrida com o System Center
Se tiver uma instalação existente do System Center, pode integrar estes componentes OMS serviços tooprovide uma solução híbrida de ambos no local e na nuvem ambientes tirar partido specialties relativo de Olá de cada produto.  Ligar o seu existentes do Operations Manager grupo tooLog análise tooanalyze gerido agentes de gestão na nuvem de Olá.  Utilize o processo de cópia de segurança existente com o Data Protection Manager toobackup sua toohello de dados na nuvem.  


## <a name="oms-services"></a>Serviços do OMS
funcionalidade de principal de Olá do OMS é fornecida por um conjunto de serviços que são executados no Azure.  Cada serviço fornece uma função de gestão específico e pode combinar os cenários de gestão diferentes tooachieve de serviços.

|| Serviço | Descrição |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | Monitorizar e analisar a disponibilidade de Olá e o desempenho de recursos diferentes, incluindo físicos e máquinas virtuais. |
| ![Automatização do Azure](media/operations-management-suite-overview/icon-automation.png) | Automatização | Automatizar processos manuais e impor configurações para computadores e máquinas virtuais. |
| ![Azure Backup](media/operations-management-suite-overview/icon-backup.png) | Cópia de segurança | Criar cópias de segurança e restaurar dados críticos. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Site Recovery | Providenciar elevada disponibilidade para aplicações críticas. |

### <a name="log-analytics"></a>Log Analytics
O [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) oferece serviços de monitorização para o OMS, ao recolher dados de recursos geridos num repositório central.  Estes dados podem incluir eventos, dados de desempenho ou dados personalizados fornecidos através de Olá API. Depois de recolhidos, dados de Olá estão disponíveis para alertas, análise e exportação.  Este método permite-lhe uma variedade de origens de dados tooconsolidate modo pode combinar os dados dos seus serviços do Azure com o seu ambiente no local existente.  Também claramente separa coleção Olá dos dados de Olá da ação de Olá efetuada nos dados, para que todas as ações disponíveis tooall tipos de dados.  

![Descrição geral do Log Analytics](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>Recolher daos
Existem uma variedade de formas que pode obter dados para o repositório de Olá para tooanalyze de análise de registos.

- **Computadores Windows ou Linux e máquinas virtuais.**  Instalar Olá Microsoft Monitoring Agent no [Windows](../log-analytics/log-analytics-windows-agents.md) e [Linux](../log-analytics/log-analytics-linux-agents.md) computadores ou máquinas virtuais que pretende que os dados de toocollect do.  agente Olá irá transferir automaticamente a partir da configuração de análise de registos que define os eventos e toocollect de dados de desempenho.  Pode facilmente instalar o agente de Olá em máquinas virtuais em execução no Azure utilizando o Olá portal do Azure.  Se tiver um ambiente existente do Operations Manager, pode ligar tooLog de grupo de gestão de Olá análise e iniciar automaticamente a recolha de dados de todos os agentes existentes.
- **Serviços do Azure.**  Análise de registos recolhe a telemetria de [diagnósticos do Azure e a monitorização do Azure](../log-analytics/log-analytics-azure-storage.md) no repositório de Olá, de modo a que possa monitorizar recursos do Azure.
- **API do Recoletor de Dados.**  O Log Analytics tem uma [API REST para preencher dados de qualquer cliente](../log-analytics/log-analytics-data-collector-api.md).  Isto permite-lhe toocollect dados de aplicações de terceiros ou implementar cenários de gestão personalizado.  Um método comum é toouse um runbook nos dados de toocollect de automatização do Azure e, em seguida, utilizar Olá toowrite de API do Recoletor de dados-toohello repositório.

#### <a name="reporting-and-analyzing-data"></a>Analisar os dados e criar relatórios
Análise de registos inclui um consulta poderosa linguagem tooextract os dados armazenados no repositório de Olá.  Uma vez que os dados de todas as origens são armazenados como registos, pode analisar dados de várias origens numa única consulta.
  
Além disso, tooad hoc análise, análise de registos fornece várias formas tooreport e analisar dados de uma consulta.

- **Vistas e dashboards.**  [Vistas](../log-analytics/log-analytics-view-designer.md) e [dashboards](../log-analytics/log-analytics-dashboards.md) visualizar Olá resultados de uma consulta no portal de Olá.  Soluções de gestão serão incluem, geralmente, as vistas que analisam dados de Olá da solução de Olá.  Também pode criar as suas próprias vistas personalizadas tooanalyze dados e disponibilizá-lo prontamente no seu portal personalizado.
- **Exportar.**  Ter Olá opção tooexport Olá os resultados de qualquer consulta para que possa analisá-lo fora da análise de registos.  Ainda pode agendar uma exportação regular demasiado[Power BI](../log-analytics/log-analytics-powerbi.md) que fornece capacidades de visualização e análise significativas.
- **API de Pesquisa de Registos.**  O Log Analytics tem uma [API REST para recolher dados de qualquer cliente](../log-analytics/log-analytics-log-search-api.md).  Isto permite-lhe tooprogrammatically trabalho com dados recolhidos no repositório de Olá ou aceder a partir de outra ferramenta de monitorização.

#### <a name="alerting"></a>Alertas
O Log Analytics pode [alertar pró-ativamente](../log-analytics/log-analytics-alerts.md) os utilizadores ou tomar medidas corretivas quando deteta problemas.  Tal como todas as outras análises do Log Analytics, os alertas são feitos com pesquisas de registos.  Esta pesquisa é executada com base numa agenda regular, e é criado um alerta se os resultados de Olá corresponderem aos critérios de específicos.

![Alertas do Log Analytics](media/operations-management-suite-overview/overview-alerts.png)

Além disso toocreating um registo de alerta no repositório de análise de registos de Olá, alertas podem demorar Olá ações a seguir.

- **Enviar e-mail.**  Enviar um e-mail tooproactively notificá-lo de um problema detetado.
- **Runbook.**  Um alerta do Log Analytics pode iniciar um runbook na Automatização do Azure.  Normalmente, isto é feito problema do tooattempt toocorrect Olá detetado.  Olá runbook pode ser iniciado na nuvem de Olá no Olá maiúsculas e minúsculas de um problema no Azure ou outra nuvem ou foi iniciada num agente local para um problema num físico ou numa máquina virtual.
- **Webhook.**  Um alerta pode iniciar um webhook e transmita-dados de Olá os resultados da pesquisa de Olá de registo.  Isto permite a integração com os serviços externos, como um sistema de alerta alternativo ou, pode tentar uma ação corretiva tootake para um web site externo.

### <a name="azure-automation"></a>Automatização do Azure
[A automatização do Azure](http://azure.microsoft.com/documentation/services/automation) fornece tooOMS de gestão de configuração e de automatização do processo.  Este automatiza processos manuais e ajuda a configurações de tooenforce para computadores físicos e virtuais.  

#### <a name="process-automation"></a>Automatização de Processos
Para automatizar os processos manuais, a Automatização do Azure utiliza [runbooks](../automation/automation-runbook-types.md), que se baseiam em scripts do PowerShell ou no fluxo de trabalho do PowerShell.  Também inclui suporte runbooks, tais como as variáveis que podem ser partilhados entre vários runbooks e as credenciais e ligações que permitem-lhe as informações de toostore encriptado que poderão ser necessárias para um runbook para a autenticação de recursos.
Os Runbooks oferecem a automatização de processos para Olá outros serviços no suite Olá.  Dado que cada um dos Olá outros serviços podem ser acedidos com o PowerShell ou através de uma API REST, pode criar runbooks tooperform essas funções como recolher dados de gestão na análise de registos ou iniciar uma cópia de segurança com cópia de segurança do Azure.

##### <a name="accessing-resources"></a>Aceder aos recursos
Visto que os runbooks são baseados no PowerShell, podem gerir qualquer recurso que possa ser acedido com cmdlets do PowerShell.  Quando lhe [carregar um módulo](../automation/automation-integration-modules.md) na sua conta de automatização, torna-se disponíveis tooall runbooks nessa conta. 
 
Quando os runbooks são executados na nuvem de Olá, podem aceder a quaisquer recursos acessíveis a partir da nuvem Olá.  Estes podem ser recursos na sua subscrição do Azure, noutra cloud, como o Amazon Web Services (AWS) ou um serviço acessível através de uma API REST.  Os Runbooks na nuvem de Olá não executados sob as credenciais, mas pode tirar partido dos recursos de automatização como credenciais, ligações e certificados tooauthenticate tooresources que vão aceder.

Recursos no seu centro de dados muito provável que não podem ser acedidos a partir de um runbook em execução na nuvem de Olá.  Pode instalar um ou mais [os Runbook Workers híbridos](../automation/automation-hybrid-runbook-worker.md) nos seus dados do Centro de apesar toorun runbooks que necessitam de aceder a recursos toolocal.  Quando inicia um runbook, especifique se deve ser executada na nuvem de Olá ou uma função de trabalho específica.

![Runbooks da Automatização do Azure](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Iniciar um runbook
Os runbooks podem ser [iniciados de várias formas](../automation/automation-starting-a-runbook.md), para que possam ser incluídos em diversos cenários de gestão.  

- **Portal do Azure.**  Como outros serviços do Azure, da automatização do Azure podem ser gerida a partir Olá Portal do Azure.  Além disso toostarting runbooks, pode importá-los ou criar os seus próprios.
- **Agendados.**  Pode agendar toostart de runbooks em intervalos regulares.  Isto permite-lhe tooautomatically repetir um processo de gestão regular ou recolher dados tooLog análise.
- **PowerShell e API.**  Pode iniciar os runbooks e transmita-los necessário informações de parâmetro de um cmdlet do PowerShell ou Olá API de REST de automatização do Azure.  
- **Webhook.**  É possível criar um webhook para qualquer runbook que permite o toobe iniciada a partir de aplicações externas ou web sites.
- **Alerta do Log Analytics.**  Um alerta na análise de registos pode iniciar automaticamente um problema de toocorrect tooattempt do runbook Olá identificado por alerta Olá.

#### <a name="configuration-management"></a>Gestão da Configuração
[Configuração de estado pretendido ' (DSC) da PowerShell](../automation/automation-dsc-overview.md) é uma plataforma de gestão do Windows PowerShell que permite-lhe toodeploy e impor configuração Olá físicos e máquinas virtuais.  A automatização do Azure gere as configurações de DSC e fornece um servidor de solicitação na nuvem de Olá que os agentes podem aceder ao tooretrieve necessárias configurações.

![Azure Automation DSC](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Azure Backup e Azure Site Recovery
Cópia de segurança do Azure e de Azure Site Recovery contribuem toobusiness a recuperação de continuidade e desastre.  Cada têm funcionalidades que o ajudam a tooensure que as aplicações permanecem disponíveis quando ocorrem falhas e de devolvem toonormal operações quando sistemas fique novamente online.  Ambos os serviços contribuem toohello objetivos de ponto de recuperação (RPOs) e os objetivos de tempo de recuperação (RTOs) definidos para a sua organização. O RPO define o limite de aceitável Olá em que dados não estão disponíveis durante uma falha e Olá RTO limita Olá aceitável período de tempo em que um serviço ou aplicação não está disponível durante uma falha.

#### <a name="azure-backup"></a>Azure Backup
O [Azure Backup](http://azure.microsoft.com/documentation/services/backup) proporciona serviços de criação de cópias de segurança e de restauro de dados no OMS.  Protege os dados de aplicação e mantém-nos durante anos sem qualquer investimento de capital e com um mínimo de custos operacionais.  -Pode criar cópias de segurança dados a partir de servidores físicos e virtuais do Windows em cargas de trabalho de tooapplication de adição, tais como o SQL Server e o SharePoint.  Também pode ser utilizado por tooAzure de dados do System Center Data Protection Manager (DPM) tooreplicate protegido para redundância e armazenamento a longo prazo.

Os dados protegidos no Azure Backup são armazenados num cofre de cópias de segurança localizado numa região geográfica específica. Olá os dados são replicados no Olá mesma região e, dependendo do tipo de Olá de cofre, também pode ser replicada tooanother região para resiliência adicional.

A Cópia de Segurança do Azure tem três cenários fundamentais.

- **Computador Windows com agente do Azure Backup.** Cópia de segurança de ficheiros e pastas a partir de qualquer Windows server ou o cliente diretamente tooyour Cofre de cópia de segurança do Azure.<br><br>![Computador Windows com agente do Azure Backup](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) ou Microsoft Azure Backup Server.** Tirar partido dos ficheiros de toobackup do DPM ou o servidor de cópia de segurança do Microsoft Azure e as pastas em cargas de trabalho de tooapplication de adição, como o armazenamento de toolocal SQL e SharePoint e, em seguida, são replicadas tooyour Cofre de cópia de segurança do Azure. Suporta máquinas virtuais do Windows e do Linux no Hyper-V ou no VMware.<br><br>![System Center Data Protection Manager (DPM) ou Microsoft Azure Backup Server.](media/operations-management-suite-overview/overview-backup-02.png)
- **Extensões da Máquina Virtual do Azure.** Cópia de segurança Windows ou Linux virtual máquinas Azure tooyour Cofre de cópia de segurança do Azure.<br><br>![Extensões da Máquina Virtual do Azure](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[O Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) fornece continuidade do negócio através da orquestração da replicação dos locais virtuais e máquinas físicas tooAzure ou tooa site secundário. Se o site primário não estiver disponível, pode efetuar a ativação pós-falha localização secundária toohello para que os utilizadores podem manter o trabalho e falhar voltando sistemas devolvem tooworking ordem. 

O Azure Site Recovery proporciona elevada disponibilidade para aplicações e servidores.  Contribui tooyour continuidade de negócios e uma estratégia de recuperação (BCDR) desastre através da orquestração da replicação, ativação pós-falha e recuperação de máquinas de virtuais de Hyper-V no local, as máquinas virtuais VMware e servidores físicos Windows/Linux. Pode replicar máquinas tooa secundária de centro de dados ou expandir o seu centro de dados através da replicação-los tooAzure. O Site Recovery também fornece ativação pós-falha e recuperação simples para cargas de trabalho. Integra-se com mecanismos de recuperação após desastres, como o SQL Server AlwaysOn e fornece planos de recuperação para ativação pós-falha fácil de cargas de trabalho que estão em camadas em várias máquinas.

O Azure Site Recovery tem três cenários de replicação fundamentais.

- **Replicação de máquinas virtuais de Hyper-V.**  Se as máquinas virtuais de Hyper-V geridas em nuvens VMM, pode replicar tooa secundário center ou tooAzure o armazenamento de dados. Replicação tooAzure é através de uma ligação de internet segura. Centro de dados secundário replicação tooa é Olá LAN.  Se as máquinas virtuais de Hyper-V não são geridas pelo VMM, pode replicar tooAzure armazenamento apenas. Replicação tooAzure é através de uma ligação de internet segura.<br><br>![Replicação de máquinas virtuais de Hyper-V](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **Replicação de máquinas virtuais de VMWare.**  Pode replicar VMware máquinas virtuais tooa datacenter secundário com armazenamento de VMware ou tooAzure. Replicação tooAzure pode ocorrer ao longo de um site para site VPN ou Azure ExpressRoute ou através de uma ligação de Internet segura. Datacenter secundário de tooa de replicação ocorre através de Olá canal de dados do InMage Scout.<br><br>![Replicação de máquinas virtuais de VMWare](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Replicação de servidores Windows e Linux físicos**  Pode replicar servidores físicos tooa datacenter ou tooAzure armazenamento secundário. Replicação tooAzure pode ocorrer ao longo de um site para site VPN ou Azure ExpressRoute ou através de uma ligação de Internet segura. Datacenter secundário de tooa de replicação ocorre através de Olá canal de dados do InMage Scout. O Azure Site Recovery tem uma solução OMS apresenta algumas estatísticas, mas tem de utilizar Olá portal do Azure para quaisquer operações.<br><br>![Replicação de servidores físicos do Windows e Linux](media/operations-management-suite-overview/overview-siterecovery-physical.png)


O Site Recovery armazena metadados em cofres localizados numa região geográfica específica do Azure. Não existem dados replicados são guardados por Olá serviço de recuperação de Site.

## <a name="management-solutions"></a>Soluções de Gestão
As [Soluções de Gestão](operations-management-suite-solutions.md) são conjuntos pré-embalados de lógica que implementam um determinado cenário de gestão que tira partido de um ou mais serviços do OMS.  Diferentes soluções estão disponíveis da Microsoft e de parceiros que pode adicionar facilmente tooyour subscrição do Azure tooincrease Olá valor seu investimento no OMS.  Como parceiro pode criar a suas próprias soluções toosupport as suas aplicações e serviços e forneça toousers através de Olá Azure Marketplace ou modelos de início rápido.

Um bom exemplo de uma solução que tira partido das funcionalidades adicionais do vários serviços tooprovide é Olá [solução de gestão de atualizações](oms-solution-update-management.md).  Esta solução usa o agente de análise de registos de Olá para Windows e Linux toocollect informações sobre as atualizações necessárias em cada agente.  Escreve este repositório de análise de registos de toohello dados onde pode analisá-lo com um dashboard incluído.  Quando cria uma implementação, os runbooks na automatização do Azure são utilizados tooinstall necessárias atualizações.  Gerir este processo completo no portal de Olá e não precisa de tooworry sobre detalhes subjacente Olá.

![Solução](media/operations-management-suite-overview/overview-solution.png)

Pode efetuar a maioria das soluções de um ou mais dos Olá seguintes funções.

- Recolher informações adicionais.  O Log Analytics recolhe diversos dados a partir de clientes e serviços, incluindo dados de eventos e de desempenho.  Uma solução de gestão pode recolher informações adicionais que não estão disponíveis noutras origens de dados, utilizando, muitas vezes, runbooks da Automatização do Azure.
- Disponibilizar análises adicionais das informações recolhidas.  As soluções de gestão incluem dashboards e vistas que proporcionam análises e visualização dos dados.  Estas pesquisas de registo de back-toopredefined ligação permitem-lhe toodrill em Olá detalhadas dados.  Pode também desempenhadas Analysis Services em dados já foram recolhidas no repositório de Olá, por exemplo, procure em eventos de segurança para os padrões que indiquem uma ameaça.
- Acrescentar funcionalidade.  Algumas soluções fornecidas pela Microsoft podem tirar partido de capacidades de Olá das funcionalidades adicionais do Olá principais serviços tooprovide.  Por exemplo, o mapa de serviço fornece a suas próprias toodiscover de consola e mapas de servidor e processo de dependências em tempo real.
Soluções regularmente a serem adicionadas tooOMS pela Microsoft e parceiros, permitindo-lhe toocontinuously aumentam o valor de Olá do investimento.  Pode procurar e instalar soluções da Microsoft através de Olá soluções de catálogo no portal do OMS Olá ou procurar e instalar soluções de parceiros e a Microsoft através de Olá Azure Marketplace em Olá Portal do Azure.  

![Galeria de Soluções](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre o [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Saiba mais sobre o [Automatização do Azure](../automation/automation-intro.md).
* Saiba mais sobre o [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Saiba mais sobre o [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).
* Detetar Olá [soluções que estão disponíveis](../log-analytics/log-analytics-add-solutions.md) nas ofertas de OMS diferentes Olá. 

