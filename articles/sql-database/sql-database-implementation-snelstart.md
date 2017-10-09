---
title: "aaaAzure caso prático de SQL da base de dados do Azure - Snelstart | Microsoft Docs"
description: "Saiba mais sobre como SnelStart utiliza base de dados SQL toorapidly expandir os serviços empresariais uma taxa de 1.000 novo Azure bases de dados SQL por mês"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Com o Azure, SnelStart expandiu rapidamente os serviços empresariais uma taxa de 1.000 novo Azure bases de dados SQL por mês
![SnelStartLogo](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart torna software popular financeiros-empresarial-gestão e para empresas pequena e média (PMEs) no países baixos de Olá. Que os seus 55,000 clientes são servidos por uma equipa de pessoal de 110 funcionários, incluindo uma equipa de TI de 35. Ao mover da oferta de software-como-um-serviço (SaaS) tooa do ambiente de trabalho de software criada no Azure, SnelStart efetuadas hello mais de serviços incorporados, automatizar a gestão através do ambiente familiar em c# e otimizar o desempenho e escalabilidade por nem over - ou aprovisionamento em que as empresas utilizam conjuntos elásticos. Utilizar o Azure fornece fluidity de Olá SnelStart de mover os clientes no local e Olá na nuvem.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>Por que motivo SnelStart expandido serviços da nuvem de ambiente de trabalho toohello Olá
> "A trabalhar com o Azure significa que pode fornecer software mais rápida, rapidamente reagir toocustomer exigências e dimensionar soluções quando exigências aumentam."
> 
> — Henry foi, Arquitetos de Software
> 
> 

SnelStart foi executada uma empresa de software com êxito durante anos, com um modelo de programação tradicionais: code, o pacote, são enviados e repita. Ao longo do tempo, Olá esteja a par da alteração queria mais rápido e mais rapidamente. Normas são alterados frequentemente e os clientes necessários mais fácil formas tooprocess financeiros os registos e colaboram com os respetivos accountants e government tookeep cópias de segurança com essas alterações.

"Envio toocustomers de software foi dispendiosa e restritiva," tooHenry de acordo com foi, arquitetos de software. "Produção, empacotamento e os custos de envio limitada frequência foi Lançamos software. Tivemos toopackage atualizações para shipments periódicas, mas que efetuadas toomeet rígido os nossos clientes alterar necessidades. Iremos foi nunca ter a certeza de que os nossos clientes atualizado toohello a versão mais recente do produto Olá. Por conseguinte, tivemos toosupport várias versões, tornando Olá suporta toodo muito difícil tarefa bem."

Foi adiciona, "queremos uma forma tooprogram e versão atualizações num na melhoria ritmo, pelo que iremos foi inovar mais rapidamente e criar novos serviços para os nossos clientes. Também Queremos que tooautomate uma forma mais processa na ordem toosimplify necessidades de negócio administração os nossos clientes."

Para SnelStart, Olá solução foi tooextend os respetivos serviços, se tornar um fornecedor de SaaS baseado na nuvem. plataforma de base de dados do Azure SQL Olá ajudou SnelStart chegar lá sem incorrer em Olá principais custos gerais de TI que necessitaria uma solução de infraestrutura-como-um-serviço (IaaS).

modelo de nuvem Olá também permite SnelStart toofix erros e fornecer novas funcionalidades rapidamente, sem que os clientes que necessitam toodownload e atualização de software. De acordo com tooBeen, "Using cloud services do Azure permite-nos tooquickly act após a alteração de requisitos de terceiros. Em vez de ter tooship um novo toothousands de versão dos clientes, iremos pode adaptar informações enviadas a partir dos formatos de toonew nossa aplicação de ambiente de trabalho de terceiros."

## <a name="a-modern-company-with-traditional-roots"></a>Uma empresa moderna com raízes tradicionais
SnelStart é uma empresa moderna, seja ágil, alta raízes humble dating too1964, quando founders Olá iniciado empresa Olá como um fabricante de peças instrumento musical. heart Olá de Olá SnelStart empresas de software iniciado realmente beating no Olá 1980s, durante a proliferação de Olá de computador do Olá pessoal. empresa Olá necessárias um software de gestão de contas de toohello alternativo melhor disponível no momento de Olá pelo demorou é importante as suas próprias mãos. Em 1982, a empresa Olá criados foundation Olá do que seria deixar de software de gestão de contas SnelStart. Início de Olá, software Olá foi admired para sua simplicidade e velocidade —, tanto que, para que Olá eventualmente alteradas foco e empresa reinvented próprio para uma empresa de software.

Em 1995, SnelStart lançadas a sua primeira aplicação de bookkeeping para Windows. aplicação Olá, incorporada no Microsoft Visual Basic 1.0 e do Microsoft Access bases de dados ajudou a crescer Olá toomore base do cliente de 5000 utilizadores.

Hoje, SnelStart é um fornecedor de principais de uma linha de negócio (LOB) e a aplicação de negócio administração direcionada para PMEs neerlandês e entrepreneurs self employed. Como Carlo Kuip, arquiteto IT, diz: "o nosso objetivo é tooprovide automatização de 100-por cento dos serviços de administração de negócio para os nossos clientes."

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>Otimizar o desempenho e o custo com conjuntos elásticos
SnelStart era um adopter antecipado em grande escala de conjuntos elásticos. Conjuntos elásticos ajudam os custos de limite do Olá da empresa e gerir requisitos de desempenho de forma mais eficiente. De acordo com tooBeen, "ao utilizar conjuntos elásticos, mas pode otimizar o desempenho com base nas necessidades de Olá dos nossos clientes, sem sobre-aprovisionar. Se tivemos tooprovision com base no pico de carga, seria possível bastante dispendiosa. Em vez disso, Olá recursos de tooshare opção entre várias bases de dados de utilização baixo nos permite toocreate uma solução que efetua bem e também é rentável. "

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Bases de dados SQL do Azure ajuda containerize dados para segurança e isolamento
Base de dados SQL do Azure permite SnelStart tooeasily e mover com transparência tooAzure de dados de negócio administração dos clientes no local. Olá SQL Database do Azure é um contentor conveniente que fornece o isolamento, um limite para autenticação, autorização e fácil capacidades de cópia de segurança e restauro. Bases de dados fornecem um modelo conceptual adequado para a administração de negócio. De acordo com tooCarlo Kuip, arquiteto IT, "itens este limite do contentor contêm dados confidenciais que são fundamental tooa negócio e armazenar esses itens no mantém base de dados isolado-los bem protegidas. Iremos pode gerir autorização ao nível da base de dados de Olá e mesmo a automatizar a gestão de Olá e escalável destas bases de dados sem necessidade dos administradores de base de dados (DBAs) em equipa."

O Azure SQL Data Warehouse também desempenha um papel na história de segurança e gestão da SnelStart Olá, ajudando empresa Olá recolher dados de telemetria, tais como a deteção de intrusões, o registo de atividade do utilizador e a conectividade.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure remove sobrecarga para que os programadores podem demora mais tempo a entrega de valor
modelo de plataforma do Azure Olá removido custos de infraestrutura e ativada SnelStart tooautomate implementações utilizando bibliotecas de gestão do c#. Como Kuip Estados, "foi possível toogrow nosso atuais operações com uma equipa de pessoal muito pequena durante a recuperação após desastre, escalabilidade e velocidade em simultâneo crescente opções para os nossos clientes. desenvolvimento do Olá shift tooservices libertado recursos toofocus nos novos serviços e funcionalidades, em vez de apenas atualizar tookeep de código existente cópias de segurança com novos códigos de regulamentos ou fiscais." Adiciona, "Ao automatizar a gestão e utilizar a oferta de SaaS Olá, mas é capaz de toodeliver mais valor para os nossos clientes, sem ter investimentos grande toomake na equipa operacional." Por exemplo, ao utilizar conjuntos do Azure e elásticos, SnelStart foi tooadd capaz de uma variedade de novas funcionalidades, incluindo a integração de dados de cliente mais robusta com bancos, de faturação novos serviços, verificações pequenas empresas e serviços de e-mail.

> "Olá apenas primeiro alguns meses de 2016, vamos expandido implementações nossa base de dados do Azure SQL toomore 5.500 prestes a 12 000 e estamos a adicionar atualmente 1000 bases de dados por mês."
> 
> — Henry foi, Arquitetos de Software
> 
> 

Gestão de base de dados é ainda mais automatizado utilizando a funcionalidade das tarefas elásticas Olá. Como Kuip Estados, "altamente Agradecemos a deteção automática de Olá das bases de dados numa instância de base de dados SQL [server]." Isto permite SnelStart tooexecute operações de gestão em todos os respetivos clientes dinamicamente crescente base sem custos adicionais.

SnelStart também está a desenvolver uma API que age como um mediador entre os dados de cliente e as aplicações criadas pelo parceiros de software de terceiros. Como Kuip Estados, "Esta API irá ativar outro fornecedores tooadd funcionalidade tooour de software, por exemplo, eliminando a entrada de dados de faturas e outros documentos." Os clientes já não terá toomanually faturas de tipo para o seu software de gestão de contas de pequenas empresas; Olá SnelStart software será trocar informações necessárias Olá diretamente. Isto permite aos clientes toojoin as respetivas empresas-administração tarefas com o ecossistema de Olá de informações é emergentes de transformação digital no setor Olá.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>A forma como os serviços do Azure ativar SaaS para SnelStart
Ao utilizar o Azure, SnelStart pode servir os clientes e os respetivos accountants mais totalmente integrada na nuvem de Olá. Por exemplo, os clientes e accountants pode partilhar informações ao aceder diretamente a API de cliente do SnelStart, alojado no Azure. Kuip Estados "estes serviços reutilizáveis são tooour disponíveis direcionadas para o cliente web apps e fornecem infraestrutura e funções comuns tooallow administração de toobusiness de acesso para clientes e o software de terceiros toothird utilizados pelos nossos clientes. Os exemplos incluem fornecer capacidades de configuração do produto, a gestão de regras de firewall e gerir os processos de execução longa, como as cópias de segurança."

> O nosso objetivo é tooprovide automatização de 100-por cento dos serviços de administração de negócio para os nossos clientes." 
> 
> — Carlo Kuip, Arquiteto IT
> 
> 

Além disso, os serviços web SnelStart permitir que os clientes e accountants tooeasily aceder a dados em conjuntos elásticos SQL Database do Azure. Este modelo de SaaS, conjugado com a elasticidade da base de dados e o Azure Resource Manager, fornece SnelStart com funcionalidades de escalabilidade complementam todas as implementações do Azure. implementação de Olá é totalmente automatizada utilizando bibliotecas de gestão do c#.

![Arquitetura de SnelStart](./media/sql-database-implementation-snelstart/figure1.png)

Figura 1. A partir de Junho de 2016, SnelStart tem mais de 50 conjuntos elásticos e bases de dados mais do que 11,000

## <a name="simplicity-from-hello-cloud"></a>Simplicidade da nuvem Olá
Desde a mover tooan solução baseada na nuvem do Azure, SnelStart foi toosupport capaz de crescimento de cliente rápido ao oferta de serviços e funcionalidades inovadoras. TooBeen, de acordo com "com o Azure, pode fornecer quase contínua atualizações para os nossos clientes, sem a expandir o nosso pessoal de operações. E obtemos Olá todas as outras funcionalidades do Azure grande — como a recuperação após desastre e escalabilidade — incluídas na. "

> "Quando foi realmente através em Redmond... Recebi uma chamada de um programador regresso países baixos de Olá, phoning-me sobre um problema específico. Iremos foram tooget capaz de Microsoft toodeliver uma alteração no respetivo ambiente de produção dentro de 48 horas toosolve nosso problema. "
> 
> — Henry foi, Arquitetos de Software
> 
> 

SnelStart também appreciates parceria forte Olá que tem desenvolvidas com a equipa do Olá BD SQL do Microsoft Azure. Como Estados Kuip, "temos discussões sobre funcionalidades e como a tecnologia de toouse, que é algo appreciated em ambos os lados."
objetivo imediata de Olá para SnelStart é tookeep crescer respetivo cliente satisfeito base. Como foi Estados, "Sem Olá técnica e limitações de recursos que tivemos como um ISV, há toohow sem limite até que ponto que cresça."

## <a name="more-information"></a>Mais informações
* toolearn mais informações sobre conjuntos elásticos do Azure, consulte [conjuntos elásticos](sql-database-elastic-pool.md).
* toolearn mais informações sobre funções da Web e funções de trabalho, consulte [as funções de trabalho](../fundamentals-introduction-to-azure.md#compute).    
* toolearn mais informações sobre o Azure SQL Data Warehouse, consulte [SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn mais informações sobre SnelStart, consulte [SnelStart](http://www.snelstart.nl).

