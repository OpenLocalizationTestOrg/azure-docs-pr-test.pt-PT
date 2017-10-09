---
title: "aaaMicrosoft monitorização comparação de produto | Microsoft Docs"
description: "Microsoft Operations Management Suite (OMS) é a solução de gestão de IT que ajuda a gerir e proteger no local e a infraestrutura de nuvem de baseada na nuvem da Microsoft.  Este artigo identifica os serviços de diferentes Olá incluídos no OMS e fornece ligações tootheir detalhadas conteúdo."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Comparação de produto de monitorização Microsoft
Este artigo fornece uma comparação entre o System Center Operations Manager (SCOM) e análise de registos no Operations Management Suite (OMS) em termos da respetiva arquitetura, a lógica de Olá de como monitorizam estes recursos e como ele efetuar uma análise de dados de Olá recolha.  Este é toogive, uma compreensão dos seus diferenças e força da codificação relativa fundamental.  

## <a name="basic-architecture"></a>Arquitetura básica
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Todos os componentes SCOM estão instalados no seu centro de dados.  [Os agentes estiverem instalados](http://technet.microsoft.com/library/hh551142.aspx) nas máquinas do Windows e Linux geridos pelo SCOM.  Agentes ligar demasiado[servidores de gestão](https://technet.microsoft.com/library/hh301922.aspx) que comunicam com Olá SCOM da base de dados do armazém de dados.  Agentes baseiam-se em servidores de toomanagement de tooconnect de autenticação de domínio.  Aqueles fora de um domínio fidedigno podem efetuar a autenticação de certificado ou ligar tooa [servidor de Gateway](https://technet.microsoft.com/library/hh212823.aspx).

SCOM requer duas bases de dados do SQL Server, para dados operacionais e outra armazém toosupport dados de relatórios e análise de dados.  A [servidor de relatórios](https://technet.microsoft.com/library/hh298611.aspx) executa o SQL Server Reporting Services tooreport nos dados Olá armazém de dados. 

SCOM pode monitorizar os recursos de nuvem através de pacotes de gestão para os produtos, como [Azure](https://www.microsoft.com/download/details.aspx?id=38414), [do Office 365](https://www.microsoft.com/download/details.aspx?id=43708), e [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Estes pacotes de gestão, utilize um ou mais agentes locais como proxies para deteção na nuvem, recursos e toomeasure de fluxos de trabalho a executar o seu desempenho e disponibilidade.  Os agentes de proxy são também utilizados demasiado[monitorizar dispositivos de rede](https://technet.microsoft.com/library/hh212935.aspx) e outros recursos externos.

Olá consola de operações é uma aplicação do Windows que estabelece ligação tooone Olá de servidores de gestão e permite Olá administrador tooview e analisar os dados recolhidos e configurar o ambiente do Olá SCOM.  Uma consola baseada na web pode ser alojada em qualquer servidor IIS e fornece uma análise de dados através de um browser.

![Arquitetura do SCOM](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
A maioria dos componentes do OMS encontram-se em Olá em nuvem do Azure para que possa implementar e geri-lo com o mínimo custo e esforço administrativo.  Todos os dados recolhidos pela análise de registos são armazenados no repositório do Olá OMS.

Análise de registos pode recolher dados a partir de um dos três origens:

* Máquinas virtuais que executam o Windows e Olá e físicas [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx) ou Linux e Olá [agente do Operations Management Suite para Linux](https://technet.microsoft.com/library/mt622052.aspx).  Estas máquinas podem ser no local ou de máquinas virtuais no Azure ou noutra nuvem.
* Uma conta de armazenamento do Azure com [diagnósticos do Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) dados recolhidos por função de trabalho do Azure, a função da web ou a máquina virtual.
* [Grupo de gestão do SCOM ligação tooa](https://technet.microsoft.com/library/mt484104.aspx).  Nesta configuração, os agentes de Olá comunicam com servidores de gestão do SCOM que fornecem a base de dados do SCOM do Olá dados toohello onde, em seguida, é entregue arquivo de dados do toohello OMS.
  Os administradores de analisam os dados recolhidos e configure a análise de registos com o portal do OMS Olá que está alojado no Azure e pode ser acedido a partir de qualquer browser.  As aplicações móveis tooaccess estes dados estão disponíveis para plataformas padrão Olá.

![Arquitetura de análise do registo](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>Integrar o SCOM e análise de registos
Quando o SCOM é utilizado como uma origem de dados para análise de registos, pode tirar partido das funcionalidades de Olá de ambos os produtos numa híbrida com o ambiente de monitorização.  Pode configurar agentes SCOM existentes através de Olá consola de operações toobe geridos pelo OMS, além de pacotes de gestão de toorun toocontinuing do SCOM.  
Dados a partir de um grupo de gestão do SCOM ligado é entregue tooLog análise utilizando um dos quatro métodos:

* Eventos e os dados de desempenho são recolhidos pelo agente Olá e entregue tooSCOM.  Servidores de gestão no SCOM, em seguida, entregar Olá dados tooLog análise.
* Alguns eventos, tais como registos de IIS e eventos de segurança continuam toobe diretamente entregar tooLog análise do agente de Olá.
* Algumas soluções terá de fornecer o agente de toohello software adicional ou exigir que o software seja instalado toocollect de dados adicionais.  Estes dados serão normalmente enviados diretamente tooLog análise.
* Algumas soluções irão recolher dados diretamente a partir de servidores de gestão do SCOM provenientes de agente Olá.  Por exemplo, Olá [solução de gestão de alertas](https://technet.microsoft.com/library/mt484092.aspx) recolhe alertas do SCOM, depois de terem sido criadas.

## <a name="monitoring-logic"></a>Lógica de monitorização
SCOM e análise de registos trabalham com dados semelhantes recolhidos a partir de agentes mas tem diferenças fundamentais em como definir e implementar a respetiva lógica para recolha de dados e como analisam estes dados de Olá que possam recolher.

### <a name="operations-manager"></a>Operations Manager
Lógica de monitorização para o SCOM estiver implementado no [pacotes de gestão](https://technet.microsoft.com/library/hh457558.aspx) que contêm a lógica de deteção de componentes toomonitor, medir o estado de funcionamento de Olá esses componentes e para recolher dados tooanalyze.  Dados de monitorização pode ser tão simples como recolher um contador de desempenho ou eventos ou que poderia utilizar lógica complexa implementada num script.  Pacotes de gestão que incluem a monitorização completa estão disponíveis para uma variedade de [aplicações da Microsoft e de terceiros](http://go.microsoft.com/fwlink/?LinkId=82105) nos dispositivos de rede e toohardware de adição.  Pode [criar os seus próprios pacotes de gestão](http://aka.ms/mpauthor) para aplicações personalizadas.

Pacotes de gestão contém vários fluxos de trabalho que cada uma desempenha algumas função distinta monitorização, como um contador de desempenho de amostragem, a verificar o estado de Olá de um serviço ou executar um script.  Cada fluxo de trabalho é executado independentemente e define o seus próprio resultados, tais como a base de dados que irá escrever tooand se irá gerar um alerta. 

Pode substituir os detalhes do fluxo de trabalho, tais como a frequência de Olá executam, onde considerar que um erro de limiar de Olá e a gravidade de Olá de alerta de Olá que estas geram.  Também pode fornecer funcionalidades adicionais ao adicionar os seus fluxos de trabalho.

![Substituições](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Pacotes de gestão são instalados na base de dados do Olá do Operations Manager e distribuídos automaticamente por tooagents pelos servidores de gestão.  Cada agente irá transferir pacotes de gestão e carregar aplicações toohello relevantes de fluxos de trabalho que tenham instalado automaticamente.  Dados recolhidos pelo agente Olá é entregue toohello back-o servidor de gestão para inserção no Olá SCOM da base de dados do armazém de dados.  Olá consola de operações permite-lhe tooview e analisar estes dados através de vistas personalizadas, dashboards e relatórios incluídos no pacote de gestão de Olá.

distribuição de Olá dos pacotes de gestão é ilustrada no Olá diagrama a seguir.

![Fluxo do pacote de gestão](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Evento e recolha de desempenho
Análise de registos recolhe os eventos e contadores de desempenho de sistemas de agente utilizando origens, como o registo de eventos do Windows, registos de IIS e Syslog.  Pode definir critérios para os quais os dados são recolhidos através do portal da análise de registos de Olá e, em seguida, criar consultas de registo tooanalyze Olá recolhido dados.  Um conjunto de critérios padrão é definido quando criar a sua área de trabalho do OMS e pode definir dados adicionais para aplicações específicas. 

![Definir os registos de eventos no registo de análise](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

Enquanto SCOM tem muitos fluxos de trabalho detalhados que, normalmente, definem critérios específicos de dados e a ação de Olá que deve ser efetuada em resposta, a análise de registos tem critérios mais gerais para a recolha de dados.  Consultas de registo e soluções fornecem mais visados critérios para analisar e atuar sobre dados específicos na nuvem de Olá após o qual foi recolhido.

#### <a name="solutions"></a>Soluções
Soluções fornecem lógica adicional para recolha de dados e análise.  Pode selecionar a subscrição do soluções tooadd tooyour OMS partir Olá Galeria de solução.

![Galeria de soluções](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Soluções principalmente executam na nuvem de Olá fornecendo uma análise de eventos e contadores de desempenho recolhidos no repositório do Olá OMS.  Também pode definem toobe dados adicionais recolhida que pode ser analisado com consultas de registo ou pela interface de utilizador adicional fornecida pela solução de Olá no dashboard do Olá OMS. 

Por exemplo, Olá [solução de controlo de alterações](https://technet.microsoft.com/library/mt484099.aspx) Deteta a configuração é alterado em sistemas de agente e escreve eventos toohello OMS repositório que pode ser analisado com várias vistas gráficas resumem detetou alterações.  Pode explorar para baixo da vista de Olá resumido consultas de registo que Olá apresentar dados recolhidos pela solução de Olá de detalhado.

Enquanto pode selecionar que soluções adicionar subscrição tooyour, não tem atualmente Olá capacidade toocreate as suas próprias soluções.  Pode selecionar eventos Olá e toocollect de contadores de desempenho e criar vistas personalizadas com base nas suas próprias consultas de registo.

Olá lógica de monitorização para análise de registos está resumido na Olá diagrama a seguir.

![Fluxo de solução de análise do registo](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Monitorização do Estado de Funcionamento
### <a name="operations-manager"></a>Operations Manager
SCOM pode os diferentes componentes Olá de uma aplicação de modelo e forneça um Estado de funcionamento em tempo real para cada.  Isto permite-lhe toonot apenas vista detetou erros e de desempenho ao longo do tempo, mas também toovalidate Olá real estado de funcionamento do sistema ou uma aplicação e cada um dos respetivos componentes em qualquer momento.  Uma vez que compreende Olá períodos de tempo que uma aplicação está disponível, o motor de estado de funcionamento de Olá no SCOM também suporta nível de serviço contratos (SLA) que analisar e elaborar relatórios sobre a disponibilidade de Olá de uma aplicação ao longo do tempo.

Por exemplo, vista de Olá abaixo mostra o estado de funcionamento em tempo real do Olá de motores de base de dados do SQL Server monitorizados pelo SCOM.  Olá estado de funcionamento de cada um dos Olá bases de dados para um dos motores de base de dados de Olá é apresentado na parte inferior de Olá metade da vista de Olá.

![Vista de estado](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Olá Explorador de estado de funcionamento para um dos motores de base de dados de Olá é mostrado abaixo com monitores de Olá que são utilizado toodetermine o estado de funcionamento geral.  Estes monitores são definidos no Olá pacote de gestão do SQL Server e executar todos os motores de base de dados do SQL Server detetados pelo SCOM.

![Explorador de estado de funcionamento](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

Componentes em vários sistemas podem ser combinados toomeasure Olá estado de funcionamento uma aplicação distribuída.  Isto pode ser particularmente útil para a linha de aplicações empresariais que incluem vários componentes distribuídos.  Pode criar um modelo que mede o estado de funcionamento de Olá de cada componente dessa rollup para disponibilidade para a aplicação Olá.

Active Directory é um exemplo de um pacote de gestão que fornece um modelo tooanalyze os respetivos componentes distribuídos.  Diagrama de exemplo de Olá abaixo mostra Olá estado de funcionamento Olá ambiente geral e Olá relação entre florestas, domínios e os controladores de domínio.  Cada um destes componentes inclui subcomponentes e vários monitores semelhante exemplo SQL de toohello acima.

![Vista de diagrama do SCOM](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS não incluem um toomodel aplicações comuns do motor ou medir o respetivo estado de funcionamento em tempo real.  As soluções individuais podem avaliar Olá estado de funcionamento geral dos serviços de determinado com base nos dados recolhidos e poderá instalarem lógica personalizada na análise em tempo real do Olá agente tooperform.  Porque executam soluções na nuvem de Olá com o repositório do acesso toohello OMS, muitas vezes, podem fornecer mais profundo do Analysis Services que normalmente é efetuado por pacotes de gestão. 

Por exemplo, Olá [soluções AD avaliação e de avaliação do SQL Server](https://technet.microsoft.com/library/mt484102.aspx) analisar os dados recolhidos e fornecer uma classificação diferente para diferentes aspetos do ambiente de Olá.  Inclui recomendações para melhoramentos que podem ser efetuadas disponibilidade de Olá tooimprove e o desempenho do ambiente de Olá.

![Solução de avaliação do AD](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Análise de dados
SCOM e análise de registos fornecem funcionalidades diferentes tooanalyze recolhido dados.  SCOM tem vistas e Dashboards na consola de operações de Olá para analisar dados recentes numa variedade de formatos e relatórios para apresentar dados Olá armazém de dados em formato tabular.  Análise de registos fornece uma interface e o idioma de consulta de conclusão de registo para analisar os dados no repositório do Olá OMS.  Quando o SCOM é utilizado como uma origem de dados para análise de registos, o repositório de Olá inclui dados recolhidos pelo SCOM para que ferramentas de análise de registos de Olá podem ser utilizados tooanalyze dados de ambos os sistemas.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Vistas
As vistas na consola de operações de Olá permitem que tooview diferentes tipos de dados recolhidos pelo SCOM em diferentes formatos, normalmente, a tabela de eventos, alertas e dados de estado e gráficos de linha de dados de desempenho.  Vistas efetuar análise mínima ou consolidação de dados de Olá mas permitem-lhe toofilter tooparticular critérios de acordo com. 

![Vistas](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Pacotes de gestão, normalmente, irão fornecer várias vistas que suporte aplicação Olá ou sistema que monitoriza.  Isto pode incluir vistas de estado para objetos diferentes Olá que o pacote de gestão de Olá Deteta, vistas para problemas detetados e vistas de desempenho para contadores do alerta.

As vistas são particularmente adequadas para analisar o estado atual do Olá do ambiente de Olá, incluindo alertas abertos e estado de funcionamento de Olá de sistemas monitorizados e objetos.  Pode desagregar dados de evento ou desempenho de toodetailed suportar um alerta específico na ordem toodiagnose a causa raiz. Da mesma forma, pode ver o desempenho de Olá e estado de funcionamento de diferentes componentes de uma aplicação tooassess o estado de funcionamento atual.

#### <a name="dashboards"></a>Dashboards
Dashboards no Olá consola de operações principalmente trabalhar com Olá mesmos dados, vistas, mas são mais personalizáveis e podem incluir mais rica visualizações.  Um conjunto de dashboards padrão estão disponíveis que pode personalizar facilmente para os seus fins.  Também pode utilizar um widget de PowerShell que pode apresentar dados devolvidos por uma consulta do PowerShell.

![Dashboard](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Os programadores dispõem de Olá capacidade tooadd componentes personalizados toodashboards incluem nos respetivos pacotes de gestão.  Estes podem ser tooa altamente especializadas determinada aplicação, tais como o dashboard de Olá no Olá pacote de gestão de SQL abaixo.  Este dashboard também pode ser utilizado como um modelo para as versões personalizadas.

![Dashboard SQL](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Relatórios
Relatórios no SCOM analisam dados do armazém de dados de Olá em formato tabular.  Pode ser impresso e agendadas para entrega automatizada em formatos de ficheiro diferentes, incluindo PDF, o CSV e o Word.  Relatórios de trabalham com dados do armazém de dados de Olá para que estejam especialmente adequados para uma análise de tendências de longo prazo.

Pacotes de gestão, normalmente, irão fornecer relatórios personalizados para uma aplicação específica.  Também pode selecionar a partir de uma biblioteca genéricas de relatórios de que pode personalizar para as suas próprias aplicações ou para efetuar análise ad hoc.

Segue-se um relatório de desempenho de exemplo que mostra os dados recolhidos pelo Olá pacote de gestão do Active Directory.

![Relatório](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Análise de registos tem um [idioma de consulta](https://technet.microsoft.com/library/mt484120.aspx) que pode utilizar tooperform análise nos dados de várias aplicações sem Olá necessidade toocreate uma vista personalizada ou um relatório.  Uma vez OMS está implementado na nuvem de Olá, o desempenho das consultas e análise de dados não são as limitações de hardware do requerente tooany e rapidamente pode analisar incluindo milhões de registos de consultas. 

Consultas de análise de registos também são base Olá de outras funcionalidades.  Pode guardar uma consulta, exportar tooExcel respetivos resultados ou que o executar em intervalos regulares e gerar um alerta se os resultados correspondentes aos critérios de determinado automaticamente.  

![Fluxo de consulta de registo](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

Segue-se um exemplo de uma consulta de análise de registos.  Neste exemplo, todos os eventos com "Iniciar" no nome de Olá são devolvidos e agrupados pelo evento ID.  utilizador Olá fornece simplesmente consulta Olá e análise de registos gera dinamicamente a análise de Olá de tooperform de interface de utilizador de Olá.  Selecionar qualquer item na lista de Olá irá devolver Olá detalhadas dados de eventos.

![Consulta de registo](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

Além disso tooproviding ad hoc Analysis Services, consultas de análise de registos podem ser guardadas para utilização futura e também adicionado tooyour [OMS dashboard](http://technet.microsoft.com/library/mt484090.aspx) conforme mostrado no seguinte exemplo de Olá.

![Dashboard do OMS](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Passos Seguintes
* Implementar [do System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx).
* Inscrever-se [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics).  

