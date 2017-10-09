---
title: "segurança de dados de análise de aaaLog | Microsoft Docs"
description: "Saiba mais sobre como a análise de registos protege a sua privacidade e protege os seus dados."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Registo de segurança de dados de análise
Microsoft está empenhada tooprotecting sua privacidade e proteger os dados, enquanto fornece software e serviços que ajudam a gerir Olá infraestrutura de TI da sua organização. Reconhecemos que, quando entrust tooothers os dados, essa confiança requer a segurança rigorosas. Microsoft respeita diretrizes de conformidade e segurança toostrict — desde a codificação toooperating um serviço.

Proteger e a proteção de dados é uma prioridade superior na Microsoft. Contacte-nos com quaisquer perguntas, sugestões ou problemas sobre quaisquer Olá seguintes informações, incluindo as nossas políticas de segurança ao [as opções de suporte do Azure](http://azure.microsoft.com/support/options/).

Este artigo explica como os dados são recolhidos, processados e protegidos pela análise de registos Olá Operations Management Suite (OMS). Pode utilizar o serviço web do agentes tooconnect toohello, utilize dados operacionais do System Center Operations Manager toocollect ou obter dados de diagnóstico do Azure para utilização por análise de registos. Olá dados recolhidos são enviados através de Olá Internet utilizando a autenticação baseada em certificado de & SSL 3 toohello serviço análise de registos, que está alojado no Microsoft Azure. Dados são comprimidos pelo agente Olá antes de ser enviada.

Olá serviço análise de registos gere em segurança os dados baseados na nuvem utilizando Olá seguintes métodos:

* segregação de dados
* retenção de dados
* segurança física
* Gestão de incidentes
* Conformidade
* certificações de normas de segurança

## <a name="data-segregation"></a>segregação de dados
Dados de cliente são mantidos separados de forma lógica em cada componente em todo o Olá serviço OMS. Todos os dados são etiquetados por organização. Este tipo de etiquetagem persiste por todo o ciclo de vida do Olá dados e é imposto em cada camada de serviço Olá. Cada cliente tem um blob do Azure dedicado que aloja os dados a longo prazo Olá

## <a name="data-retention"></a>Retenção de dados
Dados de registo de pesquisa indexada são armazenados e mantidos de acordo com tooyour plano de preços. Para obter mais informações, consulte [preços de análise do registo](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft elimina dados de cliente de 30 dias após a área de trabalho do Olá OMS está fechada. Microsoft elimina também Olá conta do Storage do Azure onde os dados de Olá residem. Quando os dados de cliente for removidos, serão destruídas não unidades físicas.

Olá, a tabela seguinte lista algumas das soluções de disponíveis Olá no OMS e exemplos Olá tipos de dados que recolher.

| **Solução** | **Tipos de dados** |
| --- | --- |
| Avaliação da Configuração |Dados de configuração, metadados e dados de estado |
| Planeamento da Capacidade |Dados de desempenho e metadados |
| Antimalware |Dados de configuração e metadados |
| Avaliação de Atualizações do Sistema |Dados de metadados e o Estado |
| Gestão de Registos |Definido pelo utilizador registos de eventos, os registos de eventos do Windows e/ou os registos de IIS |
| Monitorização de Alterações |Inventário de software e os metadados do serviço do Windows |
| SQL Server e de avaliação do Active Directory |Dados WMI, dados de registo, dados de desempenho e gestão dinâmica do SQL Server ver resultados |

Olá, a tabela seguinte mostra exemplos dos tipos de dados:

| **Tipo de dados** | **Campos** |
| --- | --- |
| Alerta |Alerta de nome, descrição do alerta, Timemodified, ID do problema, IsMonitorAlert, RuleId, estado de resolução do, prioridade, gravidade, categoria, proprietário, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| Configuração |CustomerID AgentID, EntityID, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Evento |EventId EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, número, categoria, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Nota:** quando escreve eventos com campos personalizados no registo de eventos do Windows toohello, OMS recolhe-los. |
| Metadados |Timemodified, ObjectStatus, OrganizationalUnit, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IPAddress, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, endereço IP, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| Desempenho |ObjectName, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| Estado |StateChangeEventId StateId, NewHealthState, OldHealthState, contexto, TimeGenerated, TimeAdded, StateId2, Timemodified, MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>segurança física
Análise de registos de Olá no serviço do OMS é manned pela equipa da Microsoft e todas as atividades são registadas e podem ser auditadas. serviço de Olá executa completamente no Azure e está em conformidade com Olá Azure critérios comuns de engenharia. Pode ver detalhes sobre a segurança física de Olá de recursos do Azure na página 18 de Olá [descrição geral de segurança do Microsoft Azure](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Áreas de toosecure de direitos de acesso físico são alteradas dentro de um dia útil para qualquer pessoa que já não tem a responsabilidade de serviço do OMS Olá, incluindo a transferência e terminação. Pode ler sobre as infraestrutura física global dos Olá utilizamos em [Microsoft Datacenters](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Gestão de incidentes
OMS tem um processo de gestão de incidentes que cumprem todos os serviços Microsoft. toosummarize, iremos:

* Utilize um modelo de responsabilidade partilhado onde uma parte de responsabilidade de segurança pertence tooMicrosoft e uma parte pertence toohello cliente
* Gerir incidentes de segurança do Azure
  * Iniciar uma investigação mediante a deteção de um incidente
  * Avalie o impacto de Olá e a gravidade de um incidente por um membro da equipa de resposta a incidentes na chamada. Com base na provas, avaliação de Olá pode ou não pode resultar em mais Escalamento toohello resposta equipa de segurança.
  * Diagnosticar um incidente por segurança resposta especialistas tooconduct Olá forenses ou de investigação, identifique as estratégias de contenção, mitigação e solução. Se a equipa de segurança de Olá Deteta que os dados de cliente podem ter ficado tooan exposta ilícita ou não autorizada execução individuais, paralela de Olá processo de notificação do cliente incidente começa em paralelo.  
  * Stabilize e recuperar a partir de incidente Olá. equipa de resposta a incidentes de Olá cria um problema de Olá de toomitigate de plano de recuperação. Passos de contenção crisis como quarentena sistemas afetados podem ocorrer imediatamente e em paralelo com diagnósticos adicionais. Poderão ser planeadas mais mitigações de termo que ocorrer após ter passado o risco de imediato Olá.  
  * Fechar o incidente Olá e realize um mortem post. equipa de resposta a incidentes de Olá cria um mortem post que descreve Olá os detalhes do Olá incidente, com as políticas de toorevise de intenção de Olá, procedimentos e processos tooprevent uma periodicidade do evento de Olá.
* Notificar os clientes de incidentes de segurança
  * Determinar o âmbito de Olá de clientes afetados e tooprovide qualquer pessoa que é afetado como detalhadas um aviso quanto possível
  * Crie um aviso tooprovide clientes com informações detalhadas suficiente para que estes possam efetuar uma investigação no respetivo fim e cumprir os compromissos que estas efetuou os utilizadores finais de tootheir ao não unduly atrasando o processo de notificação de Olá.
  * Confirmar e declarar incidente Olá, conforme necessário.
  * Notificar os clientes com uma notificação de incidente sem unreasonable atraso e em conformidade com qualquer legal ou contractual compromisso. Notificações de incidentes de segurança são entregues tooone ou mais dos administradores de um cliente por qualquer meio seleciona da Microsoft, incluindo através de e-mail.
* Realizar a preparação de equipa e formação
  * Equipa da Microsoft é necessárias toocomplete segurança e formação de deteção, o que ajuda os tooidentify e relatório suspeito problemas de segurança.  
  * Os operadores a trabalhar num serviço Microsoft Azure de Olá têm obrigações de formação de adição envolvente os respetivos sistemas de toosensitive de acesso que alojam dados de cliente.
  * Técnico de resposta de segurança do Microsoft recebe formação especializada para as respetivas funções

Se ocorrer a perda de quaisquer dados de cliente, iremos notificá-lo cada cliente dentro de um dia. No entanto, a perda de dados de cliente nunca foi excedido com o OMS. Além disso, vamos manter cópias dos dados que foi criados e é distribuída geograficamente.

Para obter mais informações sobre como o Microsoft responde toosecurity incidentes, consulte [Microsoft Azure Security Response no Olá nuvem](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Conformidade
Olá, segurança de informações do OMS software desenvolvimento e o serviço da equipa e o programa de governação suporta os requisitos de negócio e respeite toolaws e regulamentos, conforme descrito em [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) e [Compatibilidade de centro de confiança do Microsoft](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). Como OMS estabelece requisitos de segurança, identifica os controlos de segurança, gere, monitores e riscos também estão descritas não existe. Anual, vamos rever as políticas, normas, diretrizes e procedimentos.

Cada membro de equipa de desenvolvimento do OMS recebe formação de segurança da aplicação formal. Internamente, iremos utilizar um sistema de controlo de versão para o desenvolvimento de software. Cada projeto de software está protegido pelo sistema de controlo de versão Olá.

A Microsoft tem uma equipa de segurança e conformidade supervisiona e avalia todos os serviços Microsoft. Officers de segurança de informações constituem equipa Olá e não estão associados com Olá departamentos que desenvolver OMS de engenharia. officers de segurança de Olá têm as seus próprios cadeia de gestão e realize avaliações independentes dos produtos e segurança dos serviços de tooensure e conformidade.

Placa da Microsoft do directors é notificada através de um relatório sobre todos os programas de segurança de informações na Microsoft anual.

Olá OMS software desenvolvimento e serviço equipa está ativamente trabalhar com equipas de Olá Legal Microsoft e de conformidade e outro tooacquire de parceiros da indústria certificações vários.

## <a name="certifications-and-attestations"></a>Certificações e attestations
Análise de registos do OMS cumpre os requisitos de Olá:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [NORMA ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Pagamento da indústria do cartão (PCI compatíveis) dados (PCI DSS Security Standard)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) por Olá PCI segurança normas Council.
* [O tipo de serviço organização controlos (SOC) 1 1 e certificados SOC 2 tipo 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2) em conformidade
* [HIPAA e HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) para empresas que têm um contrato de associar de negócio para HIPAA
* Critérios de engenharia comuns do Windows
* Informática Fidedigna da Microsoft
* Como um serviço do Azure, os componentes de Olá que utiliza o OMS respeitar tooAzure requisitos de conformidade. Pode ler mais em [compatibilidade de centro de fidedignidade da Microsoft](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx).

> [!NOTE]
> Em alguns certificações/attestations, análise de registos está listado em seu nome anteriores do *das informações operacionais*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Fluxo de dados de segurança a informática em nuvem
Olá diagrama seguinte mostra uma arquitetura de segurança na nuvem como fluxo Olá de informações da sua empresa e como são protegido como é move o serviço de análise de registos de toohello, em última análise visto por si no portal do OMS Olá. Mais informações sobre cada passo segue diagrama Olá.

![Imagem de recolha de dados do OMS e segurança](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Inscreva-se e recolher dados de análise de registo
Para toosend dados tooLog análise sua organização, configure os de agentes do Windows, os agentes em execução em máquinas virtuais do Azure ou agentes OMS para Linux. Se utilizar o agentes do Operations Manager, em seguida, utilizar um Assistente de configuração no tooconfigure de consola de operações de Olá-los. Utilizadores (que podem ser, outros utilizadores individuais ou um grupo de pessoas) crie uma ou mais contas OMS (áreas de trabalho do OMS) e registar agentes utilizando um dos seguintes contas de Olá:

* [ID organizacional](../active-directory/sign-up-organization.md)
* [Conta Microsoft - Outlook, Office em direto, MSN](http://www.microsoft.com/account/default.aspx)

Uma área de trabalho do OMS é onde dados recolhidos, agregados, analisados e apresentados. Uma área de trabalho é principalmente utilizada como um meio de toopartition de dados e cada área de trabalho é exclusiva. Por exemplo, poderá pretender toohave geridos os dados de produção com uma área de trabalho OMS e os dados de teste geridos com outra área de trabalho. Áreas de trabalho também ajudam a um administrador controlo utilizador acesso toohello de dados. Cada área de trabalho pode ter várias contas de utilizador associadas à mesma e, cada conta de utilizador pode aceder a várias áreas de trabalho do OMS. Criar com base na região de centro de dados de áreas de trabalho. Cada área de trabalho é replicada tooother centros de dados numa região de Olá, principalmente para disponibilidade de serviço do OMS.

Para o Operations Manager, quando tiver concluído o Assistente de configuração de Olá, cada grupo de gestão do Operations Manager estabelece uma ligação com Olá serviço análise de registos. Em seguida, utilize Olá Assistente para adicionar computadores toochoose quais os computadores no grupo de gestão de Olá são permitidos toosend serviço toohello a dados. Para outros tipos de agente, cada estabelece ligação com segurança toohello serviço OMS.

Todas as comunicações entre sistemas ligados e Olá serviço análise de registos são encriptadas.  Olá TLS protocolo (HTTPS) é utilizado para encriptação.  Olá processo do Microsoft SDL é seguido tooensure análise de registos está atualizada com avanços mais recentes do Olá nas protocolos criptográficos.

Cada tipo de agente recolhe dados para análise de registos. tipo de Olá de dados que são recolhidos é depende de tipos de Olá de soluções utilizadas. Pode ver um resumo de recolha de dados em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md). Além disso, as informações mais detalhadas de recolha estão disponíveis para a maioria das soluções. Uma solução é um pacote de vistas predefinidas, consultas de pesquisa de registo, as regras de recolha de dados e a lógica de processamento. Apenas os administradores podem utilizar a análise de registos tooimport uma solução. Após a importação solução Olá, é movido toohello servidores de gestão de Operations Manager (se utilizado) e, em seguida, tooany agentes que selecionou. Posteriormente, os agentes de Olá recolhem dados de Olá.

## <a name="2-send-data-from-agents"></a>2. Enviar dados de agentes
Registar todos os tipos de agente com uma chave de registo e é estabelecida uma ligação segura entre o agente de Olá e o serviço de análise de registos de Olá utilizando a autenticação baseada em certificado e SSL com a porta 443. OMS utiliza um arquivo secreta toogenerate e manter as chaves. As chaves privadas rodam todos os 90 dias e são armazenadas no Azure e são geridas pelo Olá Azure operações que siga strict práticas de regulamentação e conformidade.

Com o Operations Manager, registe uma área de trabalho com o serviço de análise de registos de Olá e é estabelecida uma ligação HTTPS segura entre o servidor de gestão do Operations Manager Olá.

Para agentes do Windows em execução em máquinas virtuais do Azure, uma chave de armazenamento só de leitura é eventos de diagnóstico tooread utilizados nas tabelas do Azure.

Se qualquer agente não é possível toocommunicate toohello serviço por qualquer motivo, hello dados recolhidos são armazenados localmente na cache de temporária e servidor de gestão de Olá tenta dados de Olá tooresend a cada oito minutos durante duas horas. dados em cache do agente de Olá estão protegidos pelo arquivo de credenciais do sistema de operativo Olá. Se o serviço de Olá não é possível processar os dados de Olá passadas duas horas, agentes Olá ficarão em fila os dados de Olá. Se a fila Olá ficar cheia, o OMS começa a remover tipos de dados, começando com dados de desempenho. o limite de fila do agente Olá é uma chave de registo, pelo que pode modificá-la, se necessário. Os dados recolhidos são comprimidos e enviados serviço toohello, ignorando as bases de dados no local, pelo que não adiciona quaisquer toothem de carga. Depois de as recolher Olá são enviados dados, este é removido da cache de Olá.

Como descrito acima, dados de agentes são enviados através de SSL tooMicrosoft centros de dados do Azure. Opcionalmente, pode utilizar segurança adicional do ExpressRoute tooprovide para dados de Olá. O ExpressRoute é uma forma toodirectly ligar tooAzure da sua rede WAN existente, tal como um protocolo multi etiqueta mudança VPN (MPLS) fornecida por um fornecedor de serviço de rede. Para obter mais informações, consulte [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. Olá serviço análise de registos recebe e processa dados
serviço de análise de registos de Olá assegura que recebidos dados de uma origem fidedigna validando certificados e integridade dos dados de Olá com a autenticação do Azure. Olá não processados dados não processados são, em seguida, armazenados como um blob na [armazenamento do Microsoft Azure](../storage/common/storage-introduction.md) e não está encriptada. No entanto, cada blob storage do Azure tem um conjunto de conjunto exclusivo de chaves, que é acessível toothat apenas de utilizador. tipo de Olá dos dados armazenados depende tipos Olá das soluções que foram importadas e utilizadas toocollect dados. Em seguida, Olá serviço análise de registos processa dados não processados Olá do blob storage do Azure de Olá.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Análise de registos tooaccess Olá dados
Pode iniciar sessão tooLog análise no portal do OMS Olá utilizando a conta institucional Olá ou conta Microsoft que configurou anteriormente. Todo o tráfego entre o portal do OMS Olá e análise de registos na OMS é enviado através de um canal HTTPS seguro. Ao utilizar o portal do OMS Olá, é gerado um ID de sessão no cliente de utilizador Olá (web browser) e os dados são armazenados numa cache local até Olá de sessão é terminada. Quando terminar, cache Olá é eliminada. Os cookies do lado do cliente, que não contêm informações de identificação pessoal, não são automaticamente removidos. Cookies de sessão estão marcados HTTPOnly e estão protegidos. Após um período de inatividade previamente determinado, sessão portal do OMS Olá é terminado.

Utilizar o portal do OMS Olá, pode exportar dados tooa CSV ficheiro e podem aceder a dados através de APIs de pesquisa. Exportação CSV é limitado too50, 000 linhas por exportar e dados de API too5 restrito, 000 linhas por pesquisa.

## <a name="next-steps"></a>Passos seguintes
* [Introdução à análise de registos](log-analytics-get-started.md) toolearn mais informações sobre a análise de registos e get e funcional, em minutos.
