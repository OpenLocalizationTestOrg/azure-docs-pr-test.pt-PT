---
title: "aaaAzure caso prático de SQL da base de dados do Azure - Daxko/CSI | Microsoft Docs"
description: "Saiba mais sobre como Daxko/CSI utiliza a base de dados SQL tooaccelerate respetivo ciclo de desenvolvimento e tooenhance respetivos serviços de cliente e o desempenho"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI utilizado tooaccelerate do Azure, o ciclo de desenvolvimento e tooenhance respetivos serviços de cliente e o desempenho
![Logótipo de Daxko/CSI](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Software Daxko/CSI deparam um desafio: base dos centros de adequação a e a recriação do cliente foi crescer rapidamente, obrigado toohello sucesso da sua solução de software de empresarial abrangente, mas mantendo cópias de segurança com Olá infraestrutura de TI precisa para que a crescer base do cliente foi teste da empresa Olá equipa de TI. empresa Olá foi cada vez mais restrita por crescente overhead de operações, especialmente para gerir as suas bases de dados crescentes. Worse, esse overhead de operações foi cortando para recursos de desenvolvimento para o novo iniciativas, como novas funcionalidades de mobilidade para software da empresa Olá.

De acordo com tooDavid Molina, Director de produto de desenvolvimento em Daxko/CSI, Azure Software CSI fornecido com modelo de (PaaS) de plataforma-como-um-serviço Olá for necessário toosimplify gestão de base de dados, aumentar a escalabilidade e libertar recursos toofocus no software em vez do OPS Manager. "Base de dados SQL do azure foi uma excelente opção para-nos. Não ter tooworry sobre a manutenção de um servidor de SQL, um cluster de ativação pós-falha e Olá todas as outras necessidades de infraestrutura foi ideal para-nos."

Uma vez que a migrar tooAzure, CSI Software necessita de uma equipa de operações de toomanage apenas dois através de 600 bases de dados do cliente. empresa Olá utiliza conjuntos elásticos de base de dados do Azure SQL toomove cliente as bases de dados com base no tamanho e precisam.

Molina continua, "os nossos clientes felt Olá alterar imediatamente. Antes de conjuntos elásticos, ocasionalmente tinham tempos limite e outros problemas durante períodos de rajada. Com o Azure conjuntos elásticos, podem impulsar conforme necessário e utilize o software de Olá sem problemas."

Além disso tooimproving desempenho para os clientes, do Azure conjuntos elásticos libertado recursos de CSI Software toofocus no desenvolvimento de novos serviços e funcionalidades, em vez de terem de lidar com operações e gestão. Software CSI melhorar o respetivo software de enterprise oferta, SpectrumNG, toohelp ajudou a esses recursos de TI interagir com os membros de gym, melhorar a eficiência de equipa e conceder equipa e membros acesso móvel para tarefas interativas e notificações em tempo real.

Azure ajudou também CSI Software acelerar e melhorar o desenvolvimento de Olá e do ciclo de garantia de qualidade (pergunta e resposta), Ativando as opções de automatização. Com a implementação do Azure da empresa Olá, gestores de compilação podem empacotar os componentes com Olá clique do botão para um. Conforme Molina, "como parte do ciclo de lançamento de Olá, pergunta e resposta é agora toodeploy capaz de ambiente de teste de tooa no Azure, o que estritamente mimics nosso pilha de produção. Pode implementar compilações imediatamente toovet de ambiente de desenvolvimento tooour é alterado. É uma grande win para us, porque não foram cumpridos paridade para fins de teste antes dessa."

## <a name="offloading-toohello-cloud"></a>Descarregar toohello na nuvem
Antes de mover toohello cloud, CSI Software tinha construídos com êxito a própria infraestrutura multi-inquilino no Centro de dados local no Houston. Empresa Olá expandido, se deparam crescente pains crescentes de compra, aprovisionamento e manter todas hardware Olá e o software necessário toosupport que os seus clientes. Operações de toohandle staffing TI ficaram estrangulamento outro que conduziram tooa slowdown no aprovisionamento novos recursos e disponibilizando novo toocustomers de serviços.

CSI Software de analisar as opções de nuvem para eliminando esse sobrecarga, para que foi focar-se no respetivo código e, em vez das suas operações. empresa Olá detetados muitos dos fornecedores de nuvem superior Olá apenas oferecem soluções do infraestrutura-como-um-serviço (IaaS) que ainda requerem uma grande IT pessoal toomanage Olá IaaS pilha. No final de Olá, CSI Software determinar que solução de Azure PaaS Olá foi Olá melhor para as respetivas necessidades. Explica Molina, "O Azure obtém software de hardware e sistema de Olá fora de forma Olá, pelo que iremos poder concentrar na nossa ofertas de software, reduzindo o nosso custos gerais de TI."

## <a name="making-hello-transition-tooazure"></a>Efetuar Olá transição tooAzure
Depois de selecionar do Azure para a sua solução de PaaS, CSI Software começou a cloud de toohello de bases de dados e de infraestrutura de back-end a migrar. TooAzure anterior, os clientes de SpectrumNG necessário tooinstall uma aplicação cliente que comunicou com um serviço Windows Communication Foundation (WCF) no back-end Olá. TooMolina, de acordo com "Embora alguns clientes alojada tudo nos respetivos centros de dados, criámos saída multi-inquilino toobe de produto de Olá. Iremos alojado tudo num centro de dados no Houston, utilizar o SQL Server como Olá arquivo de dados.

"A nossa oferta produto também incluir um orientado para o membro portal web (escrito no ASP.net), que era presença na web do cliente de toobe concebida, com a etiqueta de branco toomatch Olá e uma API de SOAP toosupport Olá online as páginas e qualquer integração de terceiros."

nuvem de toohello de migração de Olá não entrem longa para a arquitetura de Olá. De acordo com tooMolina, "maioria de Olá de esforço Olá resolvida modificar a forma de Olá que iremos ler informações de ficheiro de configuração, modificação uma cadeia de ligação centralizada, e automatizar Olá empacotamento, carregamento e a implementação das nossas versões."

Olá toodevelop criar uma automatização, engenheiros CSI Software utilizado o Azure PowerShell e REST APIs toocreate pacotes e carregá-los de ambiente de teste tooa versão todas as noites.
Olá geral transição tooan implementação baseado na nuvem do Azure correu rápida e facilmente para a equipa de TI de Software CSI Olá. Explica Molina, "todas, iremos teve um ambiente de beta na nuvem de Olá dentro de três semanas toofour de colocar no projeto Olá. Que era uma win surprising para-nos."

Depois de configurar e testar hello ambiente, o CSI Software começou a migração de clientes. Para os clientes já a utilizar o CSI Software de alojamento, a transição de Olá foi quase totalmente integrada. Para os clientes a migrar de uma implementação no local, na nuvem de toohello de migração de Olá demorou algum tempo adicional, mas foi ainda principalmente tensão livre para os clientes e CSI Software.

Para clientes novos, CSI Software equipa de TI utiliza Olá seguintes processo tooon-quadro-los tooAzure:

1. Scripts do PowerShell do Azure são utilizada toospin configurar uma nova base de dados de cliente de Olá; todos os clientes começam num tooensure de escalão premium suficiente débito inicial para transição Olá.
2. Sempre que possível, o Software de CSI utiliza Olá Assistente de migração de SQL do Azure toomove dados tooan SQL Database do Azure instância existente.
3. Por fim, o Microsoft SQL Server Integration Services (SSIS) são utilizado tooreconcile quaisquer discrepâncias em dados de Olá ou tooperform qualquer limpeza de dados como necessário.

Hoje em dia, cerca de 99 por cento dos clientes de CSI Software estão alojados no Azure, entre quatro regionais dos centros de dados (Norte Central, Sul Central, leste e oeste). Por meio de centros de dados na região geográfica de cada cliente, o latência é mantida tooa mínimo.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Azure conjuntos elásticos liberte recursos de TI
Várias funcionalidades do Azure tem ajudou CSI Software shift deixou de ser a funcionalidade de toobeing direcionadas para a infraestrutura e operações e desenvolvimento concentra-se. Talvez benefício maior Olá foi de conjuntos elásticos.

CSI Software fornece atualmente 550 sobre bases de dados para os clientes. Antes de conjuntos elásticos, era difícil toomanage que muitas bases de dados dentro de uma estrutura de camada. Gestores de OPS tinham tooassign escalões de desempenho com base nas necessidades de rajada Olá de clientes, que obrigatório significativa IT-recurso dos custos gerais. Com conjuntos elásticos, gestores podem atribuir inquilinos um premium ou um conjunto padrão, conforme adequado e, em seguida, mova os clientes com base no tamanho e precisam. Os clientes felt Olá os efeitos da conjuntos elásticos Olá quase imediatamente; antes de conjuntos elásticos, os clientes tinham tempos limite e outros problemas durante períodos de utilização de rajada, mas com conjuntos elásticos, os clientes podem sentir atividade bursts conforme necessário e podem continuar toouse SpectrumNG sem problemas.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>Azure Active Directory georreplicação acelera Reporting Services
Alguns clientes de CSI Software também são tirar partido do Azure Active Directory georreplicação. Com replicação geográfica activa, cópia de segurança toofour bases de dados secundárias legíveis podem ser configuradas Olá regiões diferentes ou mesmo centro de dados. CSI Software utilizam georreplicação ativa de duas formas: primeiro, estão disponíveis no Olá maiúsculas e minúsculas de um centro de dados falha ou Olá incapacidade tooconnect toohello principal da base de dados; as bases de dados secundária Olá e o segundo, bases de dados secundária Olá são legíveis e podem ser utilizado toooffload cargas de trabalho só de leitura como tarefas de relatório. Alguns clientes CSI Software utilizam esta tooaccelerate benefício fluxos de trabalho de relatórios.

## <a name="csi-software-application-logic-and-architecture"></a>Lógica da aplicação de CSI Software e arquitetura
SpectrumNG utiliza funções da web. Uma vez aplicação Olá é multi-inquilino, um serviço WCF é utilizado toohandle Olá inicial o pedido de ligação de clientes. Como Molina informa "o pedido de Olá identifica cada cliente, que, em seguida, permite-na criar uma cadeia de ligação enviados tootheir toodo de bases de dados é necessário toodo."

Para a camada web de Olá do seu serviço, CSI Software tira partido do dimensionamento automático do Azure, com base no dia e hora. Recursos disponíveis são uma utilização superior tooaccommodate aumento automaticamente durante o horário comercial, toohello fuso horário de cada datacenter regional de acordo com. Recursos estão igualmente configurados tooscale para baixo no fim de semana, quando as necessidades do cliente são inferiores.

![Arquitetura de Daxko/CSI](./media/sql-database-implementation-daxko/figure1.png)

Figura 1. Uma função de trabalho de serviços em nuvem desenha dados estruturados da SQL Database do Azure e semiestruturados dados a partir do armazenamento de tabelas. Utilizadores de SpectrumNG interagem com que dados através de uma nuvem de serviços de função da web.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Utilizar as aplicações web e uma camada web plano para aplicações móveis
Utilizar base de dados do SQL Azure libertado recursos para o Software de CSI tooenable iniciativas novo, incluindo uma plataforma móvel completa com base numa API personalizada alojada em aplicações web do Azure. plataforma de Olá permite aos membros de gym e agendas de toocheck de dispositivos móveis de toouse pessoal, livro classes e receber mensagens.

Olá plataforma utiliza arquitetura orientada para serviços (SOA) tootake um único componente — como um sistema de ponto de venda (POS) ou um sistema de venda — movê-la no plano de web de momento tooanother Olá e, em seguida, rotação toosupport um serviço de cópia de segurança desse componente, mantendo tudo o resto em plano de original de Olá web. Esta capacidade proporciona flexibilidade imenso CSI Software e ajuda a mantenha os custos reduzidos.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure permite CSI Software aos programadores focarem-se no aplicações e serviços
Base de dados SQL do Azure não é apenas um boon tooSpectrumNG os clientes que desfrutar serviço rápida e fiável de Olá, também é uma grande win para Software de CSI equipa de TI e programadores. Ao descarregar ops tooAzure na nuvem de Olá, CSI Software reduzido a sobrecarga de infraestrutura e de recursos, acelerados significativamente os ciclos de desenvolvimento e já não necessita de desempenho de toooptimize toomicromanage bases de dados para os seus inquilinos.

## <a name="more-information"></a>Mais informações
* toolearn mais informações sobre conjuntos elásticos do Azure, consulte [conjuntos elásticos](sql-database-elastic-pool.md).
* toolearn mais informações sobre as ferramentas de base de dados e o dimensionamento elástico, consulte [ferramentas de base de dados elástica e dimensionamento elástico](sql-database-elastic-scale-get-started.md).
* Consulte toolearn mais informações sobre migrar uma base de dados do SQL Server, consulte [migrar um tooAzure de base de dados do SQL Server](sql-database-cloud-migrate.md).
* toolearn mais informações sobre a replicação geográfica activa, consulte [georreplicação ativa](sql-database-geo-replication-overview.md).
* toolearn mais informações sobre funções da Web e funções de trabalho, consulte [as funções de trabalho](../fundamentals-introduction-to-azure.md#compute).    
* toolearn mais informações sobre o Service Bus do Azure, consulte [Service Bus do Azure](https://azure.microsoft.com/services/service-bus/).
* toolearn mais informações sobre o dimensionamento automático, consulte [dimensionamento serviços em nuvem](../cloud-services/cloud-services-how-to-scale.md).

