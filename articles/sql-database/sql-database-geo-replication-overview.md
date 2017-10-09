---
title: "aaaFailover grupos e a georreplicação ativa - SQL Database do Azure | Microsoft Docs"
description: "Grupos de ativação de pós-falha automática com georreplicação ativa permite-lhe toosetup 4 réplicas de base de dados em qualquer um dos Olá centros de dados do Azure e a ativação pós-falha de autoomatically no evento Olá de indisponibilidade."
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>Descrição geral: Grupos de ativação pós-falha e a georreplicação ativa
Replicação geográfica activa permite-lhe tooconfigure segurança toofour legível secundário bases de dados no Olá localizações (regiões) do Centro de dados idêntica ou diferentes. Bases de dados secundárias estão disponíveis para consulta e de ativação pós-falha no caso de Olá de uma data center Olá ou falha incapacidade tooconnect toohello base de dados primária. ativação pós-falha de Olá tem de ser iniciada manualmente por aplicação Olá do utilizador Olá. Após a ativação pós-falha, a nova principal de Olá tem um ponto final de ligação diferente. 

> [!NOTE]
> Replicação geográfica activa está disponível para todas as bases de dados em todos os escalões de serviço em todas as regiões.
>  

Grupos de auto-ativação pós-falha de base de dados SQL do Azure (na pré-visualização) é um tooautomatically de funcionalidade foi concebida de base de dados SQL gerir relação de replicação geográfica, conectividade e ativação pós-falha à escala. Com a mesma, Olá clientes ganhos Olá capacidade tooautomatically recuperar várias bases de dados relacionados na região secundária Olá após falhas regionais catastrófica ou outros eventos de não planeados resultam na perda total ou parcial de Olá do serviço de base de dados SQL disponibilidade na região primária Olá. Além disso, podem utilizar Olá bases de dados secundária legível toooffload só de leitura cargas de trabalho.  Porque os grupos de ativação de pós-falha automática envolvem várias bases de dados que têm de ser configuradas no servidor primário Olá. Servidores primários e secundários têm de estar no Olá mesma subscrição. Grupos de auto-ativação pós-falha suportam a replicação de todas as bases de dados no Olá grupo tooonly um servidor secundário numa região diferente. Replicação geográfica activa, sem grupos de ativação de pós-falha automática, permite que cópias de segurança secundárias too4 em qualquer região.

Se estiver a utilizar a georreplicação ativa e para qualquer motivo, que a base de dados primária falha ou simplesmente a necessidades toobe colocado offline, pode iniciar tooany de ativação pós-falha das bases de dados secundárias. Quando a ativação pós-falha é tooone ativada das bases de dados secundária Olá, todas as outras bases de dados secundárias são automaticamente ligado toohello nova principal. Se estiver a utilizar ativação de pós-falha automática e grupos de recuperação de base de dados (em pré-visualização) toomanage qualquer falha que afeta uma ou várias das bases de dados de Olá nos resultados de grupo Olá na ativação pós-falha automática. Pode configurar uma política de ativação de pós-falha automática Olá que melhor se adeque às necessidades da sua aplicação, ou pode ativamente por não participar e utilizar a ativação manual. Além disso, os grupos de auto-ativação pós-falha (em pré-visualização) fornecem leitura / escrita e pontos finais de escuta de só de leitura que permanecem inalterados durante as ativações pós-falha. Se utilizar a ativação de ativação pós-falha manual ou automática, ativação pós-falha comutadores todas as bases de dados secundárias no Olá tooprimary de grupo. Após a conclusão da ativação pós-falha de base de dados de Olá, registo DNS Olá é a região de toohello de pontos finais Olá do tooredirect automaticamente atualizado novo.

Pode gerir a replicação e ativação pós-falha de uma base de dados individual ou um conjunto de bases de dados num servidor ou num agrupamento elástico com georreplicação ativa. Pode fazê-lo nesse utilizando Olá [portal do Azure](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [Transact-SQL](sql-database-geo-replication-transact-sql.md), ou Olá [REST API](https://msdn.microsoft.com/library/azure/mt163685.aspx). Após a ativação pós-falha, certifique-se requisitos de autenticação de Olá para o servidor e base de dados estão configurados no principal Olá de novo. Para obter mais informações, consulte [segurança da base de dados do SQL Server após a recuperação de desastre](sql-database-geo-replication-security-config.md). Isto aplica-se ambos os grupos de replicação geográfica e ativação de pós-falha automática tooactive (em pré-visualização).

Olá tira partido de replicação geográfica activa [Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) tecnologia do SQL Server tooasynchronously replicar as transações consolidadas no Olá base de dados primária tooa secundária da base de dados utiliza o isolamento de instantâneo consolidada leitura (RCSI). Os grupos de auto-ativação pós-falha fornecem a semântica de grupo Olá por cima georreplicação ativa mas Olá é utilizado o mesmo mecanismo de replicação assíncrona. Enquanto em qualquer momento de determinado, base de dados secundária Olá poderão ser ligeiramente atrás de base de dados primária Olá, são garantidos dados secundário Olá toonever ter transações parciais. Redundância por várias regiões permite que aplicações tooquickly recuperar de uma perda permanente de todo o datacenter ou partes de um datacenter causado por perante desastres naturais, erros humanos catastrófica ou atos maliciosos. dados específicos do RPO Olá podem ser encontrados em [descrição geral da continuidade do negócio](sql-database-business-continuity.md).

Olá figura seguinte mostra um exemplo de replicação geográfica activa configurado com um site primário na região do Olá Norte Central-nos e secundários na região do Olá Sul Central-nos.

![relação de replicação geográfica](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Uma vez que as bases de dados secundária Olá são legíveis, podem ser utilizados toooffload só de leitura cargas de trabalho como tarefas de relatório. Se estiver a utilizar replicação geográfica activa, é a base de dados secundária toocreate possíveis Olá no Olá mesma região com Olá primário, mas não aumenta resiliência toocatastrophic de falhas da aplicação Olá. Se estiver a utilizar grupos de auto-ativação pós-falha (em pré-visualização), a base de dados secundária é sempre criado numa região diferente.

Além disso, toodisaster recuperação replicação geográfica activa pode ser utilizada em Olá os seguintes cenários:

* **Base de dados de migração**: pode utilizar a georreplicação ativa toomigrate bases de dados de um servidor tooanother online com o período de indisponibilidade mínimo.
* **As atualizações de aplicações**: pode criar um secundário adicional como uma cópia de back-falhar durante as atualizações de aplicações.

continuidade do negócio real de tooachieve, adicionar redundância da base de dados entre centros de dados é apenas uma parte da solução de Olá. Recuperar uma aplicação (serviço) ponto-a-ponto após uma falha catastrófica necessita de recuperação de todos os componentes que constituem o serviço de Olá e quaisquer serviços dependentes. Exemplos destes componentes incluem software de cliente Olá (por exemplo, um browser com uma JavaScript personalizado), extremidades web de front-, armazenamento e DNS. É fundamental que todos os componentes são resiliente toohello mesmas falhas e ficam disponíveis dentro do Olá tempo objetivo de recuperação (RTO) da sua aplicação. Por conseguinte, tem de tooidentify todos os serviços dependentes e compreender garantias de Olá e capacidades que fornecem. Em seguida, tem de colocar tooensure passos adequados que as suas funções serviço durante Olá ativação pós-falha dos serviços de Olá do qual depende. Para obter mais informações sobre soluções de conceção para recuperação após desastre, consulte [conceber soluções de nuvem de recuperação de desastre utilizando replicação geográfica activa](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-capabilities"></a>Capacidades de replicação geográfica activa
a funcionalidade de replicação geográfica activa Olá fornece Olá seguir as capacidades essenciais:
* **Replicação assíncrona automática**: só pode criar uma base de dados secundária adicionando tooan base de dados existente. Olá secundária pode ser criado em qualquer servidor da SQL Database do Azure. Depois de criado, a base de dados secundária Olá é preenchido com dados de Olá copiados a partir da base de dados primária Olá. Este processo é conhecido como o seeding. Depois de base de dados secundária foi criado e pré-propagadas, atualizações toohello base de dados primária estiver no modo assíncrono replicadas da base de dados secundária toohello automaticamente. Replicação assíncrona significa que as transações são consolidadas na base de dados primária Olá antes de serem replicadas toohello base de dados secundária. 
* **Bases de dados secundárias legíveis**: uma aplicação pode aceder a uma base de dados secundária para operações só de leitura utilizando Olá mesmo ou de principais de segurança diferentes utilizado para aceder à base de dados primária Olá. Olá bases de dados secundárias operam em isolamento do instantâneo modo tooensure a replicação das atualizações de Olá de Olá primário (reprodução de registo) não está atrasada por consultas executadas no Olá secundário.

   > [!NOTE]
   > repetição de registo Olá está atrasada na base de dados secundária Olá se existem atualizações do esquema que está a receber de Olá principal que necessitam de um bloqueio de esquema de base de dados secundária Olá. 
   > 

* **Várias bases de dados secundárias legíveis**: dois ou mais bases de dados secundárias aumentam a redundância e nível de proteção para a base de dados primária Olá e da aplicação. Se existirem várias bases de dados secundárias, a aplicação Olá permanece protegida mesmo se uma das bases de dados secundária Olá falhar. Se existir apenas uma base de dados secundária, e este falhar, a aplicação Olá está exposta toohigher risco até que seja criada uma nova base de dados secundária.

   > [!NOTE]
   > Se estiver a utilizar a georreplicação ativa toobuild uma aplicação distribuída global e tem de aceder a tooprovide só de leitura toodata em mais de 4 regiões, pode criar secundária de uma secundária (um processo conhecido como encadeamento). Desta forma pode alcançar praticamente ilimitada escala de replicação de base de dados. Além disso, encadeamento reduz a sobrecarga de Olá da replicação de base de dados primária Olá. compromisso de Olá é Olá aumento desfasamento nas bases de dados secundária Olá mais folha. . 
   >

* **Suporte de bases de dados do conjunto elástico**: georreplicação ativa pode ser configurada para uma base de dados em qualquer conjunto elástico. base de dados secundária Olá pode ser noutro conjunto elástico. Para bases de dados normais, Olá secundário pode ser um conjunto elástico e vice-versa desde que estejam escalões de serviço Olá Olá mesmo. 
* **Nível de desempenho configurável da base de dados secundária Olá**: uma base de dados secundária pode ser criado com o nível de desempenho inferior ao hello primário. Bases de dados primários e secundários são necessários toohave Olá mesma camada de serviço. Esta opção não é recomendada para aplicações com a atividade de escrita da base de dados elevada porque o desfasamento aumento Olá aumenta o risco de Olá de perda de dados substanciais após uma ativação pós-falha. Além disso, depois de desempenho da aplicação Olá ativação pós-falha é afetado até Olá novo primário é atualizado tooa um desempenho superior ao nível. Olá gráfico de percentagem de e/s de registo no portal do Azure fornece uma boa forma tooestimate Olá nível de desempenho mínima de Olá secundário que é necessário toosustain Olá replicação carga. Por exemplo, se a base de dados primária é P6 (1000 DTU) e o respetivo registo de percentagem de e/s é 50% Olá secundário necessita toobe com pelo menos P4 (500 DTU). Também pode obter utilizando dados de e/s de registo do Olá [resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) ou [sys.dm db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) vistas da base de dados.  Para obter mais informações sobre níveis de desempenho de base de dados SQL Olá, consulte [opções de base de dados SQL e desempenho](sql-database-service-tiers.md). 
* **Ativação pós-falha controlado de utilizador e a reativação pós-falha**: uma base de dados secundária explicitamente pode ser desativados toohello função primária em qualquer altura através da aplicação Olá ou utilizador de Olá. Durante uma Olá de indisponibilidade real deve ser utilizada a opção "", que imediatamente promove um site primário Olá toobe secundário. Quando principal falha Olá recupera e está disponível novamente, sistema Olá automaticamente Olá marcas recuperado primário como uma secundária e colocá-lo com o novo site primário Olá. Devido a natureza assíncrona toohello da replicação, uma pequena quantidade de dados pode ser perdida durante as ativações pós-falha não planeadas se falhar de um site primário antes de ser replicado Olá mais recente alterações toohello secundário. Quando um site primário com várias bases de dados secundárias a ativação pós-falha, sistema Olá reconfigura automaticamente relações de replicação de Olá e Olá ligações restantes secundárias toohello recentemente promovido primário sem exigir qualquer intervenção do utilizador. Após a falha de Olá que causou a ativação pós-falha de Olá é atenuada, poderá ser região primária do tooreturn desejável Olá aplicação toohello. toodo, o comando de ativação pós-falha de Olá deve ser invocado com Olá "planeada" opção. 
* **Manter sincronizadas as credenciais e regras de firewall**: Recomendamos que utilize [regras de firewall de base de dados](sql-database-firewall-configure.md) para bases de dados de georreplicação para estas regras podem ser replicadas com tooensure de base de dados de Olá todas as bases de dados secundárias tem Olá mesmas regras de firewall como Olá primário. Esta abordagem elimina a necessidade de Olá para os clientes toomanually configurar e manter as regras de firewall nos servidores que alojam as bases de dados de Olá, primária e secundária. Da mesma forma, [continha os utilizadores de base de dados](sql-database-manage-logins.md) para dados de acesso garante bases de dados principais e secundários têm sempre Olá mesmo utilizador as credenciais, por isso durante uma ativação pós-falha, existe sem interrupções toomismatches devida com inícios de sessão e palavras-passe. Com a adição de Olá de [do Azure Active Directory](../active-directory/active-directory-whatis.md), os clientes podem gerir o acesso tooboth primária e secundária bases de dados e eliminando Olá necessitam para a gestão de credenciais em bases de dados completamente.

## <a name="auto-failover-group-capabilities"></a>Capacidades do grupo de ativação de pós-falha automática

Funcionalidade de grupos de ativação de pós-falha automática fornece uma abstração de elevado desempenho de replicação geográfica activa por suportar a replicação de nível de grupo e a ativação pós-falha automática. Além disso, remove cadeia de ligação de SQL toochange Olá Olá necessária após a ativação pós-falha, fornecendo os parâmetros de serviço de escuta adicionais Olá. 

* **Grupo de ativação pós-falha**: um ou vários grupos de ativação pós-falha podem ser criados entre dois servidores em regiões diferentes (servidores primários e secundários). Cada grupo pode incluir uma ou várias bases de dados que são recuperados como uma unidade no caso de todos os ou algumas bases de dados primárias ficam indisponíveis devido a indisponibilidade de tooan na região primária Olá.  
* **Servidor primário**: um servidor que aloja as bases de dados primária Olá no grupo de ativação pós-falha de Olá.
* **Servidor secundário**: um servidor que aloja as bases de dados secundária Olá no grupo de ativação pós-falha de Olá. servidor secundário Olá não pode estar em Olá mesma região que o servidor primário Olá.
* **Adicionar grupo de toofailover de bases de dados**: pode colocar várias bases de dados dentro de um servidor ou dentro de um elástico agrupamento para Olá mesmo grupo de ativação pós-falha. Se adicionar um grupo de toohello de base de dados autónomo, este cria automaticamente uma base de dados secundária utilizando Olá mesmo nível de desempenho e de edição. Se a base de dados primária Olá está num conjunto elástico, Olá secundário é criado automaticamente no agrupamento elástico Olá com Olá mesmo nome. Se adicionar uma base de dados que já tem uma base de dados secundária no servidor secundário Olá, esse georreplicação é herdada por grupo de Olá.

   > [!NOTE]
   > Ao adicionar uma base de dados que já tem uma base de dados secundária no servidor que não faz parte do grupo de ativação pós-falha de Olá, é criado um novo secundário no servidor secundário Olá. 
   >

* **Escuta de leitura e escrita do grupo de ativação pós-falha**: registo CNAME no DNS A formados como  **&lt;nome do grupo de ativação pós-falha&gt;. database.windows.net** que aponte toohello o URL do servidor primário atual. Permite que Olá aplicações do SQL de leitura e escrita tootransparently restabelecer a ligação da base de dados primária toohello quando Olá primário alterado após a ativação pós-falha. 
* **Escuta de só de leitura do grupo de ativação pós-falha**: registo CNAME no DNS A formados como  **&lt;nome do grupo de ativação pós-falha&gt;. secondary.database.windows.net** que aponte o URL do servidor secundário toohello. Permite que Olá só de leitura aplicações SQL tootransparently ligar toohello base de dados secundária utilizando Olá especificado regras de balanceamento de carga. Opcionalmente, pode especificar se pretende Olá só de leitura tráfego toobe automaticamente redirecionada servidor primário toohello quando o servidor secundário Olá não está disponível.
* **Política de ativação pós-falha automática**: por predefinição, o grupo de ativação pós-falha de Olá está configurado com uma política de ativação pós-falha automática. sistema Olá aciona uma ativação pós-falha, assim que for detetada Olá falha. Se pretender que o fluxo de trabalho do toocontrol Olá ativação pós-falha da aplicação Olá, pode desativar a ativação pós-falha automática. 
* **Ativação pós-falha manual**: podem iniciar manualmente ativação pós-falha em qualquer altura, independentemente da configuração de ativação pós-falha automática Olá. Se a política de ativação pós-falha automática não é a ativação pós-falha manual configurada é toorecover necessários bases de dados no grupo de ativação pós-falha de Olá. Pode iniciar a ativação pós-falha forçada ou amigável (com a sincronização de dados completa). Olá última pode ser região primária de toohello servidor ativo de Olá toorelocate utilizados. Quando concluir a ativação pós-falha os registos DNS de Olá são servidor correto do toohello de conectividade tooensure automaticamente atualizadas.
* **Período de tolerância a perdas de dados**: porque bases de dados de Olá, primária e secundária são sincronizados utilizando a ativação pós-falha de Olá replicação assíncrona pode resultar na perda de dados. Pode personalizar tooreflect de política de ativação pós-falha automática Olá perda de toodata de tolerância da sua aplicação. Ao configurar **GracePeriodWithDataLossHours**, pode controlar quanto sistema Olá aguarda antes de iniciar a ativação pós-falha de Olá, que é provavelmente tooresult perda de dados. 

   > [!NOTE]
   > Quando o sistema Deteta que bases de dados de Olá num grupo de Olá ainda estão online (por exemplo, falha de Olá apenas afetado plane de controlo de serviço Olá), ativa imediatamente a ativação pós-falha de Olá com sincronização de dados completa (amigável ativação pós-falha), independentemente do valor de Olá definido pelo **GracePeriodWithDataLossHours**. Este comportamento garante que não há nenhuma perda de dados durante a recuperação de Olá. período de tolerância Olá entra em vigor apenas quando uma ativação pós-falha amigável não é possível. Se a falha de Olá mitigada antes de expirar o período de tolerância Olá, ativação pós-falha de Olá não se encontra ativada.
   >

* **Vários grupos de ativação pós-falha**: pode configurar vários grupos de ativação pós-falha para Olá mesmo par de escala de Olá de toocontrol de servidores de ativações pós-falha. Cada grupo de ativação pós-falha independentemente. Se a aplicação multi-inquilino utiliza conjuntos elásticos, pode utilizar esta capacidade toomix primária e secundária bases de dados em cada agrupamento. Desta forma que pode reduzir o Olá impacto de uma interrupção tooonly metade dos inquilinos Olá.

## <a name="best-practices-of-building-highly-available-service"></a>Melhores práticas de criação do serviço de elevada disponibilidade

toobuild um serviço de elevada disponibilidade que utiliza os clientes de Olá de base de dados SQL do Azure deve seguir estas diretrizes:
- **Grupo de ativação pós-falha de utilização**: um ou vários grupos de ativação pós-falha podem ser criados entre dois servidores em regiões diferentes (servidores primários e secundários). Cada grupo pode incluir uma ou várias bases de dados que são recuperados como uma unidade no caso de todos os ou algumas bases de dados primárias ficam indisponíveis devido a indisponibilidade de tooan na região primária Olá. grupo de ativação pós-falha de Olá cria a base de dados de georreplicação secundária com Olá mesmo objetivo como Olá principal de serviço. Se adicionar que um existente georreplicação relação toohello ativação pós-falha grupo disponibilizar se Olá georreplicação-secundário está configurado com Olá mesmo como objetivo de nível de serviço Olá primário.
- **Utilizar o serviço de escuta de leitura e escrita para a carga de trabalho OLTP**: quando efetuar a utilização de operações do OLTP  **&lt;nome do grupo de ativação pós-falha&gt;. database.windows.net** como o URL do servidor Olá e ligações de Olá serão toohello automaticamente direcionados principal. Este URL não será alterado após a ativação pós-falha de Olá.  
Ativação pós-falha de Olá nota implica a atualização de Olá registo DNS para que ligações de cliente Olá será redirecionado toohello novo primário apenas após o cliente de Olá DNS cache é atualizada.
- **Utilize o serviço de escuta de só de leitura para a carga de trabalho só de leitura**: Se tiver uma logicamente isolada só de leitura carga de trabalho que está vinculada toocertain tolerância a falhas de dados, pode utilizar base de dados secundária Olá na aplicação Olá. Para utilizam sessões só de leitura  **&lt;nome do grupo de ativação pós-falha&gt;. secondary.database.windows.net** como o URL do servidor Olá e ligação Olá serão automaticamente direcionado toohello secundário. Também é recomendável que indicar na cadeia de ligação ler intenção utilizando **ApplicationIntent ReadOnly de =**. 
- **Preparado para degradação do desempenho**: decisão de ativação pós-falha do SQL Server é independente de rest de Olá da aplicação Olá ou outros serviços utilizado. aplicação Olá pode ser "misto" com alguns componentes numa região e alguns noutra. tooavoid degradação de Olá, certifique-se a implementação de aplicação redundante Olá na região de Olá DR e siga as diretrizes de Olá neste artigo.  
Tenha em atenção Olá aplicação na região de DR Olá não tem toouse uma cadeia de ligação diferente.  
- **Preparar para a perda de dados**: se for detetada uma falha, o SQL Server aciona automaticamente ativação pós-falha de leitura e escrita se houver zero toohello de perda de dados melhor dos nossos dados de conhecimento. Caso contrário, aguarda para período Olá especificado pelo **GracePeriodWithDataLossHours**. Se tiver especificado **GracePeriodWithDataLossHours**, estar preparadas para a perda de dados. Em geral, durante a falhas, Azure favorece a disponibilidade. Se não é possível suportar a perda de dados, certifique-se de que tooset **GracePeriodWithDataLossHours** tooa suficientemente grande número, por exemplo, 24 horas. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>Atualizar ou desatualização de uma base de dados primária
Pode atualizar ou mudar um nível de desempenho diferentes de tooa de base de dados primária (Olá dentro da mesma camada de serviço) sem desligar quaisquer bases de dados secundárias. Ao atualizar, recomendamos que primeiro a atualizar a base de dados secundária Olá e, em seguida, atualizar Olá principal. Quando desatualização, inverter a ordem de Olá: mudar Olá principal primeiro e, em seguida, mudar Olá secundário. Quando atualiza ou mudar o escalão de serviço diferente de tooa de base de dados de Olá esta recomendação é imposta. 

> [!NOTE]
> Se tiver criado a base de dados secundária como parte da configuração do grupo de ativação pós-falha de Olá não é base de dados secundária toodowngrade recomendada Olá. Este é tooensure a camada de dados tem suficiente capacidade tooprocess a carga de trabalho regular após a ativação pós-falha está ativada. 
>

## <a name="preventing-hello-loss-of-critical-data"></a>Impedir que Olá perda de dados críticos
Devido a latência elevada toohello das redes de área alargada, a cópia contínua utiliza um mecanismo de replicação assíncrona. Replicação assíncrona faz com que alguma perda de dados obrigatório se ocorrer uma falha. No entanto, algumas aplicações podem exigir sem perda de dados. tooprotect estas atualizações críticas, um programador de aplicações podem chamar Olá [sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) procedimento sistema imediatamente após a consolidar transação Olá. Chamar **sp_wait_for_database_copy_sync** Olá blocos chamar thread até ser transações consolidadas de último Olá transmitidos toohello base de dados secundária. No entanto, este não aguardar Olá transmitido transações toobe reproduzido e dedicada a Olá secundário. **sp_wait_for_database_copy_sync** é confinada tooa a cópia contínua específico ligação. Qualquer utilizador com Olá ligação direitos toohello principal da base de dados pode chamar este procedimento.

> [!NOTE]
> **sp_wait_for_database_copy_sync** irá impedir a perda de dados após a ativação pós-falha, mas será garante a sincronização completa para acesso de leitura. Olá atraso causado por um **sp_wait_for_database_copy_sync** chamada de procedimento pode ser significativa e depende do tamanho Olá do registo de transações Olá momento Olá da chamada de Olá. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>Através de programação gerir grupos de ativação pós-falha e a georreplicação ativa
Tal como abordado anteriormente, grupos de auto-ativação pós-falha (em pré-visualização) e o Active Directory georreplicação também pode ser gerida através de programação com o Azure PowerShell e Olá REST API. Olá tabelas a seguir descreve o conjunto de Olá de comandos disponíveis.

**API de Gestor de recursos do Azure e a segurança baseada em funções**: georreplicação ativa inclui um conjunto de APIs do Azure Resource Manager para a gestão, incluindo Olá [API de REST de base de dados do Azure SQL](https://docs.microsoft.com/rest/api/sql/) e [Azure Cmdlets do PowerShell](https://docs.microsoft.com/powershell/azure/overview). Estas APIs requerem Olá utilização de grupos de recursos e suportam a segurança baseada em funções (RBAC). Para obter mais informações sobre como tooimplement aceder às funções, consulte [controlo de acesso em funções do Azure](../active-directory/role-based-access-control-what-is.md).

> [!NOTE]
> Muitas funcionalidades novas da replicação geográfica activa só são suportadas com [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) com base [API de REST do Azure SQL](https://msdn.microsoft.com/library/azure/mt163571.aspx) e [cmdlets do PowerShell de base de dados do SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx). Olá [API de REST (clássica)](https://msdn.microsoft.com/library/azure/dn505719.aspx) e [cmdlets da SQL Database do Azure (clássica)](https://msdn.microsoft.com/library/azure/dn546723.aspx) são suportados para compatibilidade com versões anteriores ao utilizar Olá APIs do Azure Resource Manager são recomendadas. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>Gerir SQL da base de dados ativação pós-falha utilizando com Transact-SQL

| Comando | Descrição |
| --- | --- |
| [Falha de ALTER DATABASE (base de dados SQL do Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Utilizar o servidor para adicionar SECUNDÁRIO no argumento toocreate uma base de dados secundária para uma base de dados existente e começa a replicação de dados |
| [Falha de ALTER DATABASE (base de dados SQL do Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Utilize a ativação pós-falha ou FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch uma ativação pós-falha primário tooinitiate de toobe de base de dados secundária |
| [Falha de ALTER DATABASE (base de dados SQL do Azure)](https://msdn.microsoft.com/library/mt574871.aspx) |Utilize a remover o servidor SECUNDÁRIO do ON tooterminate uma replicação de dados entre uma base de dados SQL e Olá especificado base de dados secundária. |
| [sys.geo_replication_links (SQL Database do Azure)](https://msdn.microsoft.com/library/mt575501.aspx) |Devolve informações sobre todas as ligações de replicação existente para cada base de dados no servidor lógico da SQL Database do Azure de Olá. |
| [sys.dm_geo_replication_link_status (SQL Database do Azure)](https://msdn.microsoft.com/library/mt575504.aspx) |Obtém Olá a última replicação, desfasamento de último e outras informações sobre a ligação de replicação de Olá para uma determinada base de dados do SQL. |
| [operation_status (SQL Database do Azure)](https://msdn.microsoft.com/library/dn270022.aspx) |Mostra o estado de Olá para todas as operações de base de dados, incluindo o estado de Olá Olá das ligações de replicação. |
| [sp_wait_for_database_copy_sync (SQL Database do Azure)](https://msdn.microsoft.com/library/dn467644.aspx) |faz com que Olá aplicação toowait até que todas as transações consolidadas são replicadas e confirmadas pela Olá Active Directory base de dados secundária. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>Gerir SQL da base de dados ativação pós-falha utilizando o com o PowerShell

| Cmdlet | Descrição |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Obtém um ou mais bases de dados. |
| [Novo AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Cria uma base de dados secundária para uma base de dados existente e começa a replicação de dados. |
| [Conjunto AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Comutadores uma ativação pós-falha primário tooinitiate de toobe de base de dados secundária. |
| [Remover AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Termina a replicação de dados entre uma base de dados SQL e Olá especificado base de dados secundária. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Obtém as ligações de georreplicação Olá entre uma base de dados do SQL do Azure e um grupo de recursos ou do SQL Server. |
| [Novo AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Este comando cria um grupo de ativação pós-falha e regista-o nos servidores primários e secundários|
| [Remover AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Remove o grupo de ativação pós-falha de hello do servidor de Olá e elimina o grupo de Olá todas as bases de dados secundária incluídos |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | Obtém a configuração do grupo de ativação pós-falha de Olá |
| [Conjunto AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Modifica a configuração de Olá do grupo de ativação pós-falha de Olá |
| [Comutador AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | Ativação pós-falha de acionadores de servidor secundário de toohello grupo de ativação pós-falha Olá |
|  | |

> [!IMPORTANT]
> Para scripts de exemplo, consulte [configurar e ativação pós-falha de uma base de dados utilizando a replicação geográfica activa](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [configurar e utilizar a georreplicação ativa agrupado da base de dados de ativação pós-falha](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md), e [configurar e ativação pós-falha de um grupo de ativação pós-falha para uma base de dados (pré-visualização)] (scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md.
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>Gerir a ativação pós-falha de base de dados do SQL Server utilizando Olá REST API
| API | Descrição |
| --- | --- |
| [Criar ou atualização de base de dados (createMode = restaurar)](/rest/api/sql/Databases/CreateOrUpdate) |Cria, atualiza ou restaura um site primário ou de uma base de dados secundária. |
| [Obter criar ou atualizar o estado da base de dados](/rest/api/sql/Databases/CreateOrUpdate) |Devolve o estado de Olá durante uma operação de criação. |
| [Definir a base de dados secundária como principal (a ativação pós-falha planeada)](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Conjuntos de base de dados réplica é primária por falhar ao longo da base de dados Olá atual réplica primária. |
| [Definir a base de dados secundária como principal (ativação pós-falha não planeada)](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Conjuntos de base de dados réplica é primária por falhar ao longo da base de dados Olá atual réplica primária. Esta operação poderá resultar na perda de dados. |
| [Obter ligação de replicação](/rest/api/sql/replicationlinks/get) |Obtém uma ligação de replicação específicos para uma determinada base de dados do SQL numa parceria de georreplicação. Obtém informações Olá visíveis na vista de catálogo Olá sys.geo_replication_links. |
| [Ligações de replicação - lista pela base de dados](/rest/api/sql/replicationlinks/listbydatabase) | Obtém todas as ligações de replicação para uma determinada base de dados do SQL numa parceria de georreplicação. Obtém informações Olá visíveis na vista de catálogo Olá sys.geo_replication_links. |
| [Eliminar ligação de replicação](/rest/api/sql/databases/delete) | Elimina uma ligação de replicação de base de dados. Não é possível efetuar durante a ativação pós-falha. |
| [Criar ou grupo de ativação pós-falha de atualização] / rest/api/sql/failovergroups/createorupdate) | Cria ou atualiza um grupo de ativação pós-falha |
| [Eliminar grupo de ativação pós-falha](/rest/api/sql/failovergroups/delete) | Remove o grupo de ativação pós-falha de hello do servidor de Olá |
| [Ativação pós-falha (planeada)](/rest/api/sql/failovergroups/failover) | A ativação pós-falha do servidor de toothis do Olá atual servidor principal. |
| [Permitir a ativação pós-falha forçada perda de dados](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |ails através do servidor de toothis do Olá atual servidor principal. Esta operação poderá resultar na perda de dados. |
| [Obter grupo de ativação pós-falha](/rest/api/sql/failovergroups/get) | Obtém um grupo de ativação pós-falha. |
| [Liste os grupos de ativação pós-falha pelo servidor](/rest/api/sql/failovergroups/listbyserver) | Apresenta uma lista de grupos de ativação pós-falha de Olá num servidor. |
| [Grupo de atualização de ativação pós-falha](/rest/api/sql/failovergroups/update) | Atualiza um grupo de ativação pós-falha. |
|  | |

## <a name="next-steps"></a>Passos seguintes
* Para scripts de exemplo, consulte:
   - [Configurar e utilizar a georreplicação ativa única da base de dados de ativação pós-falha](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [Configurar e utilizar a georreplicação ativa agrupado da base de dados de ativação pós-falha](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [Configurar e ativação pós-falha a ativação pós-falha de grupo para uma base de dados (pré-visualização)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* Para cenários e uma descrição geral de continuidade de negócio, consulte [descrição geral da continuidade de negócio](sql-database-business-continuity.md)
* toolearn sobre cópias de segurança automatizada de SQL Database do Azure, consulte [cópias de segurança automatizadas de base de dados SQL](sql-database-automated-backups.md).
* toolearn sobre a utilização de cópias de segurança automatizadas para recuperação, consulte [restaurar uma base de dados de cópias de segurança de iniciou o serviço Olá](sql-database-recovery-using-backups.md).
* toolearn sobre requisitos de autenticação para um novo servidor primário e a base de dados, consulte [segurança da base de dados do SQL Server após a recuperação de desastre](sql-database-geo-replication-security-config.md).

