---
title: "Introdução ao AAA da automatização do Azure | Microsoft Docs"
description: "Este artigo fornece uma descrição geral do serviço de automatização do Azure, revendo os detalhes de design e implementação Olá no Olá tooonboard de preparação de oferta do Azure Marketplace."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 434e8ea28c55ff9bda1d2e46a7a6b8378a3baa0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation"></a>Introdução à Automatização do Azure

Este guia de introdução apresenta principais conceitos toohello relacionados implementação da automatização do Azure. Se estiver tooAutomation novo no Azure ou ter experiência com o software de fluxo de trabalho de automatização como o System Center Orchestrator, este guia ajuda-o a compreender como tooprepare e automatização carregar.  Em seguida, irá ser preparado toobegin runbooks para suportar as suas necessidades de automatização de processos de desenvolvimento. 


## <a name="automation-architecture-overview"></a>Descrição geral da arquitetura de automatização

![Descrição geral da Automatização do Azure](media/automation-offering-get-started/automation-infradiagram-networkcomms.png)

A automatização do Azure é um software como uma aplicação de serviço (SaaS) que fornece um escalável e fiável, multi-inquilino ambiente tooautomate processos com runbooks e gerir tooWindows de alterações de configuração e sistemas Linux através da configuração de estado pretendido (DSC) nos serviços em nuvem do Azure, ou no local. As entidades contidas na sua conta de Automatização, como os runbooks, os ativos, as contas Run são isolados de outras contas de Automatização na subscrição e outras subscrições.  

Os runbooks que executa no Azure são executados em sandboxes de Automatização, que são alojados na plataforma do Azure como máquinas virtuais como um serviço (PaaS).  As sandboxes de Automatização fornecem isolamento de inquilino para todos os aspetos da execução do runbook – módulos, armazenamento, memória, comunicação de rede, fluxos de trabalho, etc. Esta função é gerida pelo serviço de Olá e não está acessível a partir da sua conta do Azure ou a automatização do Azure para lhe toocontrol.         

implementação de Olá tooautomate e gestão de recursos no seu centro de dados local ou outros serviços em nuvem, depois de criar uma conta de automatização, pode designar um ou mais Olá de toorun máquinas [trabalho de Runbook híbrida (HRW)](automation-hybrid-runbook-worker.md) função.  Cada HRW requer Olá agente de gestão da Microsoft com uma área de trabalho de análise de registos de tooa ligação e uma conta de automatização.  Análise de registos é utilizado toobootstrap Olá instalação, a manter Olá agente de gestão da Microsoft e a monitorizar a funcionalidade de Olá de Olá HRW.  Olá fornecimento de runbooks e Olá toorun instrução-los são executadas pela automatização do Azure.

Pode implementar vários HRW tooprovide elevada disponibilidade para os runbooks, tarefas de runbook de balanceamento de carga e, em alguns casos dedicá-los para cargas de trabalho específicas ou ambientes.  Olá Microsoft Monitoring Agent no Olá HRW inicia a comunicação com o serviço de automatização de Olá através da porta TCP 443 e existem não requisitos de firewall de entrada.  Assim que tiver runbook em execução num HRW num ambiente de Olá e pretender Olá runbook tooperform as tarefas de gestão contra outras máquinas ou serviços nesse ambiente, pode haver ser outras portas que Olá runbook precisa de aceder.  Se as políticas de segurança de TI não permitir que os computadores no seu toohello tooconnect de rede à Internet, consulte o artigo de Olá [OMS Gateway](../log-analytics/log-analytics-oms-gateway.md)que atos como um proxy para Olá HRW toocollect estado da tarefa e receber informações de configuração a conta de automatização.

Os Runbooks em execução num HRW ser executado em contexto de Olá de Olá conta do sistema local no computador de Olá, que é Olá recomendado contexto de segurança quando efetuar ações administrativas no computador do Windows local Olá. Se pretender que as tarefas de toorun de runbook Olá relativamente aos recursos fora do computador local Olá, poderá ser necessário ativos de credenciais seguras do toodefine no Olá conta de automatização que pode aceder a partir do runbook Olá e utilizar tooauthenticate com um recurso externo Olá. Pode utilizar [credencial](automation-credentials.md), [certificado](automation-certificates.md), e [ligação](automation-connections.md) ativos no runbook com os cmdlets que lhe permitem toospecify credenciais, para poder ser autenticado.

Configurações de DSC armazenadas na automatização do Azure podem ser máquinas de virtuais tooAzure diretamente aplicado. Outras máquinas virtuais e físicas pode solicitar as configurações do servidor de solicitação do Automation DSC do Azure Olá.  Para gerir configurações do seu local físicos ou virtuais sistemas Windows e Linux, não precisa de toodeploy qualquer infraestrutura toosupport Olá Automation DSC servidor de solicitação apenas saído acesso à Internet a partir de cada toobe sistema gerido pelo DSC de automatização , comunicar através de serviço do TCP porta 443 toohello OMS.   

## <a name="prerequisites"></a>Pré-requisitos

### <a name="automation-dsc"></a>Automation DSC
Automation DSC do Azure pode ser utilizado toomanage várias máquinas:

* Máquinas virtuais do Azure (clássicas) com o Windows ou Linux
* Máquinas virtuais do Azure com o Windows ou Linux
* Máquinas virtuais dos Serviços Web Amazon (AWS) com o Windows ou Linux
* Computadores Windows físicos/virtuais no local ou numa cloud diferente do Azure ou AWS
* Computadores Linux físicos/virtuais no local ou numa cloud diferente do Azure ou AWS

versão mais recente do Olá do WMF 5 tem de estar instalado para o agente do PowerShell DSC Olá para Windows toobe toocommunicate possível com a automatização do Azure. versão mais recente do Olá do Olá [agente DSC do PowerShell para Linux](https://www.microsoft.com/en-us/download/details.aspx?id=49150) tem de estar instalado para Linux toobe toocommunicate possível com a automatização do Azure.

### <a name="hybrid-runbook-worker"></a>Função de Trabalho de Runbook Híbrida  
Ao designar um runbook do computador toorun híbrida tarefas, este computador tem de ter Olá seguinte:

* Windows Server 2012 ou posterior
* Windows PowerShell 4.0 ou posterior.  Recomendamos que instale o Windows PowerShell 5.0 no computador de Olá para uma maior fiabilidade. Pode transferir a versão nova Olá de Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=50395)
* Mínimo de dois núcleos
* Mínimo de 4 GB de RAM

### <a name="permissions-required-toocreate-automation-account"></a>Permissões necessária toocreate conta de automatização
toocreate ou atualizar uma conta de automatização, tem de ter Olá seguintes privilégios específicos e as permissões necessárias toocomplete neste tópico.   
 
* Na ordem toocreate uma conta de automatização, a conta de utilizador do AD tem de toobe tooa adicionado função com a função de proprietário toohello equivalente de permissões para recursos do Microsoft conforme descrito no artigo [controlo de acesso baseado em funções na automatização do Azure ](automation-role-based-access-control.md).  
* Se os registos de aplicação Olá definição estiver definido demasiado**Sim**, os utilizadores de não administrador no inquilino do Azure AD podem [registar aplicações AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions).  Se os registos de aplicação Olá definição estiver definido demasiado**não**, utilizador de Olá efetuar esta ação tem de ser um administrador global no Azure AD. 

Se não for um membro de instância do Active Directory da subscrição Olá antes de é adicionado toohello global administrador/co-administrator função da subscrição Olá, são adicionados tooActive diretório como convidado. Nesta situação, receberá um "não tem permissões toocreate..." aviso no Olá **adicionar conta de automatização** painel. Os utilizadores que foram adicionados toohello global administrador/co-administrator função pode ser removida da instância de diretório Active Directory da subscrição Olá e adicionado novamente toomake-los um utilizador completo no Active Directory. tooverify nesta situação, de Olá **do Azure Active Directory** painel no portal do Azure, selecione de Olá **utilizadores e grupos**, selecione **todos os utilizadores** e, depois de selecionar Olá utilizador específico, selecione **perfil**. Olá, valor de Olá **tipo de utilizador** não deve ser igual a atributo no perfil de utilizadores Olá **convidado**.

## <a name="authentication-planning"></a>Planeamento da autenticação
A automatização do Azure permite-lhe tooautomate tarefas relativamente aos recursos no Azure, no local e outros fornecedores de serviços em nuvem.  Para que um runbook tooperform as ações necessárias, tem de ter permissões toosecurely aceder Olá a recursos com direitos mínimos de Olá necessários numa subscrição Olá.  

### <a name="what-is-an-automation-account"></a>O que é uma conta de Automatização 
Todas as tarefas de automatização de Olá que executa relativamente aos recursos através de Olá cmdlets do Azure na automatização do Azure autenticar tooAzure utilizando a autenticação de com base em credenciais de identidade organizacional do Azure Active Directory.  Uma conta de automatização é diferente da conta de Olá utilize toosign toohello portal tooconfigure e utilizar os recursos do Azure.  Incluído com uma conta de recursos de automatização são seguinte Olá:

* **Certificados** - contém um certificado utilizado para autenticação a partir de um runbook ou configuração DSC.
* **Ligações** -contém a autenticação e a configuração informações necessárias tooconnect tooan externo serviço ou aplicação a partir de um runbook ou a configuração de DSC.
* **Credenciais** -é um objeto PSCredential que contém as credenciais de segurança, tais como um nome de utilizador e palavra-passe necessária tooauthenticate a partir de um runbook ou a configuração de DSC.
* **Módulos de integração** -são módulos do PowerShell incluídos com uma utilização de toomake de conta de automatização do Azure de cmdlets nos runbooks e configurações de DSC.
* **Agendas** - contém agendas que iniciam ou interrompem um runbook numa hora especificada, incluindo frequências recorrentes.
* **Variáveis** - contêm valores disponíveis a partir de um runbook ou configuração DSC.
* **Configurações de DSC** -são scripts do PowerShell que descreve como tooconfigure uma funcionalidade do sistema operativo ou definição ou instalar uma aplicação num computador Windows ou Linux.  
* **Runbooks** -são um conjunto de tarefas que efetuam algum processo automatizado na automatização do Azure, com base no Windows PowerShell.    

recursos de automatização de Olá para cada conta de automatização estão associados uma única região do Azure, mas as contas de automatização podem gerir todos os recursos de Olá na sua subscrição. Se tiver políticas que necessitam de dados e recursos toobe tooa isolado específica a região, crie as contas de automatização em diferentes regiões.

> [!NOTE]
> As contas de automatização e os recursos de Olá que contêm que são criados no Olá portal do Azure, não pode ser acedido em Olá portal clássico do Azure. Se quiser toomanage estas contas ou os respetivos recursos com o Windows PowerShell, tem de utilizar módulos do Azure Resource Manager Olá.
> 

Quando cria uma conta de automatização no portal do Azure de Olá, criar automaticamente duas entidades de autenticação:

* Uma conta Run As. Esta conta cria um principal de serviço no Azure Active Directory (Azure AD) e um certificado. Também atribui Olá contribuinte baseada em funções controlo de acesso (RBAC), que gere os recursos do Resource Manager utilizando runbooks.
* Uma conta Run As Clássica. Esta conta carrega um certificado de gestão, que é recursos clássicos toomanage utilizados utilizando runbooks.

Controlo de acesso baseado em funções está disponível com toogrant do Azure Resource Manager permitido conta de utilizador do ações tooan do Azure AD e conta Run As e autenticar esse principal de serviço.  Leitura [controlo de acesso baseado em funções no artigo de automatização do Azure](automation-role-based-access-control.md) para obter mais informações toohelp desenvolver o seu modelo para a gestão de permissões de automatização.  

#### <a name="authentication-methods"></a>Métodos de autenticação
Olá tabela seguinte resume os métodos de autenticação diferentes Olá para cada ambiente suportado pela automatização do Azure.

| Método | Ambiente 
| --- | --- | 
| Conta Run As e Run As Clássica |Implementação clássica do Azure e Azure Resource Manager |  
| Conta de Utilizador do Azure AD |Implementação clássica do Azure e Azure Resource Manager |  
| Autenticação do Windows |Centro de dados local ou de outro fornecedor de nuvem utilizando Olá Runbook Worker híbrido |  
| Credenciais AWS |Amazon Web Services |  

Em Olá **como to\Authentication e segurança** secção, são suporte artigos fornecendo passos de descrição geral e implementação tooconfigure autenticação para os ambientes, com um existente ou nova conta, dedique nesse ambiente.  Para Olá Run As do Azure e a conta Run As clássica, Olá tópico [atualização automatização conta Run As](automation-create-runas-account.md) descreve como tooupdate a conta de automatização existente com Olá Run As contas do portal de Olá ou através do PowerShell se não estava configurada inicialmente com uma conta Run As ou Run As clássica. Se pretender toocreate uma Run As e uma conta Run As clássica com um certificado emitido pela sua autoridade de certificação empresarial (AC), reveja toolearn este artigo como toocreate Olá contas utilizando esta configuração.     
 
## <a name="network-planning"></a>Planeamento da rede
Para registar de tooand de tooconnect do Runbook Worker híbrido com o Microsoft Operations Management Suite (OMS) Olá, tem de ter acesso toohello número da porta e Olá URLs descritos abaixo.  Além disso é toohello [Olá, portas e URLs necessários para o Microsoft Monitoring Agent](../log-analytics/log-analytics-windows-agents.md#network) tooconnect tooOMS. Se utilizar um servidor proxy para comunicação entre o agente de Olá e o serviço OMS Olá, terá de tooensure que recursos adequados Olá estão acessíveis. Se utilizar um toohello de acesso de toorestrict firewall Internet, terá de tooconfigure o acesso de toopermit de firewall.

informações de Olá abaixo URLs que são necessários para Olá Runbook Worker híbrido toocommunicate com a automatização e de porta de Olá da lista.

* Porta: apenas a TCP 443 é necessária para acesso de saída à Internet
* URL global:  *.azure-automation.net

Se tiver uma conta de automatização definida para uma região específica e comunicação toorestrict com esse centro de dados regionais, hello tabela seguinte fornece o registo de DNS Olá para cada região.

| **Região** | **Registo DNS** |
| --- | --- |
| EUA Centro-Sul |scus-jobruntimedata-prod-su1.azure-automation.net |
| EUA Leste 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| EUA Centro-Oeste | wcus-jobruntimedata-prod-su1.azure-automation.net |
| Europa Ocidental |we-jobruntimedata-prod-su1.azure-automation.net |
| Europa do Norte |ne-jobruntimedata-prod-su1.azure-automation.net |
| Canadá Central |cc-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste Asiático |sea-jobruntimedata-prod-su1.azure-automation.net |
| Índia Central |cid-jobruntimedata-prod-su1.azure-automation.net |
| Leste do Japão |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste da Austrália |ase-jobruntimedata-prod-su1.azure-automation.net |
| Reino Unido Sul | uks-jobruntimedata-prod-su1.azure-automation.net |
| Gov (US) - Virginia | usge-jobruntimedata-prod-su1.azure-automation.us |

Para obter uma lista de endereços IP em vez de nomes, transferir e reveja Olá [endereço IP de Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653) ficheiro xml de Olá Microsoft Download Center. 

> [!NOTE]
> Este ficheiro contém Olá intervalos de endereços IP (incluindo intervalos de computação, armazenamento e SQL) utilizados no Olá centros de dados do Microsoft Azure. Um ficheiro atualizado é publicado semanalmente que reflete Olá atualmente implementado intervalos e todas as alterações futuras toohello IP. Intervalos de novo no ficheiro de Olá não serão utilizados nos centros de dados de Olá para, pelo menos, uma semana. . A transferência Olá novo xml todas as semanas de ficheiros e efetuar as alterações necessárias Olá no seu site toocorrectly identificar os serviços em execução no Azure. Utilizadores de rota rápidos poderão tenha em atenção que este ficheiro utilizado tooupdate Olá anúncio BGP de espaço do Azure em Olá primeira semana de cada mês. 
> 

## <a name="creating-an-automation-account"></a>Criar uma conta de Automatização

Existem várias formas, que pode criar uma conta de automatização em Olá portal do Azure.  Olá, a tabela seguinte apresenta cada tipo de experiência de implementação e as diferenças entre ambos.  

|Método | Descrição |
|-------|-------------|
| Selecione a automatização e controlo de Olá Marketplace | Uma oferta, que cria uma conta de automatização e a área de trabalho OMS ligado tooone outro nas Olá mesmo grupo de recursos e região.  Integração com o OMS também inclui a vantagem de Olá de utilizar a análise de registos toomonitor e analisar fluxos de trabalho e o estado de tarefa de runbook ao longo do tempo e utilizar as funcionalidades avançadas tooescalate ou investigar problemas. Olá oferta também implementa Olá controlo de alterações e gestão de atualizações de soluções, que estão ativadas por predefinição. |
| Selecione a automatização de Olá Marketplace | Cria uma conta de automatização num grupo de recursos novo ou existente que não está ligado tooan área de trabalho do OMS e não inclui qualquer soluções disponíveis da oferta de automatização e controlo de Olá. Esta é uma configuração básica que apresente tooAutomation e pode ajudar a saber como toowrite runbooks, as configurações de DSC e utilização das capacidades do serviço de Olá Olá. |
| Soluções de Gestão Selecionadas | Se selecionar uma solução –  **[gestão de atualizações](../operations-management-suite/oms-solution-update-management.md)**,  **[VMs de início/paragem durante as horas de inatividade](automation-solution-vm-management.md)**, ou  **[ Registo de alterações](../log-analytics/log-analytics-change-tracking.md)**  solicitar-lhe tooselect uma automatização existente e área de trabalho OMS ou oferecem Olá toocreate opção ambos como necessários para Olá solução toobe implementado na sua subscrição. |

Este tópico explica como criar uma conta de automatização e a área de trabalho OMS por oferta de automatização e controlo de Olá de integração.  toocreate autónoma conta de automatização para o serviço de Olá toopreview ou testes, Olá revisão seguinte artigo [criar conta de automatização autónomo](automation-create-standalone-account.md).  

### <a name="create-automation-account-integrated-with-oms"></a>Criar conta de Automatização integrada no OMS
Olá recomendado tooonboard método que automatização é selecionando a oferta de automatização e controlo de Olá partir Olá Marketplace.  Esta ação cria uma conta de automatização e estabelece a integração de Olá com uma área de trabalho do OMS, incluindo Olá opção tooinstall Olá soluções de gestão que estão disponíveis com oferta de Olá.  

1. Inicie sessão no toohello portal do Azure com uma conta que seja um membro da função de administradores da subscrição Olá e o coadministrador da subscrição Olá.

2. Clique em **Novo**.<br><br> ![Selecione a Nova opção no portal do Azure](media/automation-offering-get-started/automation-portal-martketplacestart.png)<br>  

3. Procurar **automatização** e, em seguida, no Olá resultados de pesquisa selecione **automatização e controlo***.<br><br> ![Procure e selecione Automatização & Controlo a partir do Mercado](media/automation-offering-get-started/automation-portal-martketplace-select-automationandcontrol.png).<br>   

4. Depois de ler a descrição de Olá oferta Olá, clique em **criar**.  

5. No Olá **automatização e controlo** painel Definições, selecione **área de trabalho OMS**.  No Olá **áreas de trabalho do OMS** painel, selecione um toohello de área de trabalho ligada OMS Olá conta de automatização mesma subscrição do Azure está a ser ou crie uma área de trabalho do OMS.  Se não tiver uma área de trabalho do OMS, selecione **criar nova área de trabalho** e no Olá **área de trabalho OMS** painel efetuar o seguinte Olá: 
   - Especifique um nome para o novo Olá **área de trabalho OMS**.
   - Selecione um **subscrição** toolink tooby selecionando Olá na lista pendente se predefinido Olá selecionado não é adequado.
   - Em **Grupo de Recursos**, pode criar um grupo de recursos ou selecionar um já existente.  
   - Selecione uma **Localização**.  Atualmente Olá únicas localizações disponíveis são **Sudeste da Austrália**, **EUA Leste**, **Sudeste asiático**, **Central EUA oeste**e  **Europa Ocidental**.
   - Selecione um **Escalão de preço**.  solução Olá é oferecida na duas camadas: livre e camada por nó (OMS).  escalão gratuito Olá tem um limite na quantidade de Olá dos dados recolhidos por dia, o período de retenção e minutos de tempo de execução de tarefa de runbook.  Olá por nó (OMS) camada não tem um limite na quantidade de Olá dos dados recolhidos diariamente.  
   - Selecione **Conta de Automatização**.  Se estiver a criar uma nova área de trabalho do OMS, é necessário tooalso criar uma conta de automatização que está associada a Olá nova área de trabalho OMS especificada anteriormente, incluindo a sua subscrição do Azure, o grupo de recursos e a região.  Pode selecionar **criar uma conta de automatização** e no Olá **conta de automatização** painel, fornece Olá seguinte: 
  - No Olá **nome** campo, introduza o nome de Olá de Olá conta de automatização.

    Todas as outras opções são preenchidas automaticamente com base na área de trabalho do OMS Olá selecionada e estas opções não podem ser modificadas.  Uma conta Run As do Azure é o método de autenticação predefinido Olá oferta Olá.  Assim que clicar em **OK**, opções de configuração de Olá são validadas e Olá conta de automatização é criada.  Pode controlar o progresso em **notificações** menu Olá. 

    Caso contrário, selecione uma conta Run As de Automatização existente.  conta de Olá que selecionar já não pode ser ligado tooanother área de trabalho do OMS, caso contrário, uma mensagem de notificação é apresentada no painel de Olá.  Se já estiver ligado, é necessário tooselect uma conta Run As de automatização diferente ou criar um.

    Depois de concluir as informações de Olá necessárias, clique em **criar**.  informações de Olá são verificadas e as contas Run As e conta de automatização de Olá são criadas.  São devolvidos toohello **área de trabalho OMS** painel automaticamente.  

6. Depois de fornecer informações de Olá necessário no Olá **área de trabalho OMS** painel, clique em **criar**.  Enquanto as informações de Olá são verificadas e área de trabalho Olá é criada, pode controlar o progresso em **notificações** menu Olá.  São devolvidos toohello **Adicionar solução** painel.  

7. No Olá **automatização e controlo** painel Definições, confirme que pretende tooinstall Olá recomendado pré-seleccionado soluções. Se desmarcar qualquer uma, pode instalá-las individualmente mais tarde.  

8. Clique em **criar** tooproceed com a integração da automatização e uma área de trabalho do OMS. Todas as definições são validadas e, em seguida, tenta Olá toodeploy oferta na sua subscrição.  Este processo pode demorar vários segundos toocomplete e pode controlar o progresso em **notificações** menu Olá. 

Após a conclusão da oferta de Olá integradas, pode começar a criar soluções de gestão tiver ativado a runbooks, funcionam com Olá, implementar um [Runbook worker híbrido](automation-hybrid-runbook-worker.md) função ou começar a trabalhar com [Log Analytics](https://docs.microsoft.com/azure/log-analytics) dados de toocollect gerados pelos recursos no seu ambiente na nuvem ou no local.   

## <a name="next-steps"></a>Passos seguintes
* Pode confirmar que a sua nova conta de Automatização pode autenticar em relação a recursos do Azure, através da consulta de [test Azure Automation Run As account authentication (testar a autenticação da conta Run As de Automatização do Azure)](automation-verify-runas-authentication.md).
* tooget iniciado com a criação de runbooks, reveja primeiro Olá [tipos de runbook de automatização](automation-runbook-types.md) suportado e relacionadas com considerações antes de iniciar a criação.


