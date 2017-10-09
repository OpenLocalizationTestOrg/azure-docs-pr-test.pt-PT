---
title: "aaaReplicate uma aplicação do SharePoint de várias camadas utilizando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooreplicate uma aplicação do SharePoint de várias camadas utilizando as capacidades do Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Replicar uma aplicação do SharePoint de várias camadas para a recuperação de desastre utilizando o Azure Site Recovery

Este artigo descreve em detalhe como tooprotect um através da aplicação SharePoint [do Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Descrição geral

Microsoft SharePoint é uma aplicação de elevado desempenho que pode ajudar a um grupo ou o departamento de organizar, colaborar e partilhar informações. SharePoint pode fornecer portais de intranet, gestão de ficheiros e documentos, colaboração, redes sociais, extranets, Web sites, pesquisa de enterprise e business intelligence. Tem também a integração de sistema, integração de processo e capacidades de automatização do fluxo de trabalho. Normalmente, as organizações consideram como uma nível 1 aplicações confidencial toodowntime perda de dados e.

Hoje em dia, Microsoft SharePoint não fornece quaisquer funcionalidades de recuperação de desastre out of box. Independentemente do tipo de Olá e dimensionamento de um desastre, recuperação envolve a utilização de Olá de um centro de dados espera que pode recuperar farm Olá para. Os centros de dados em modo de espera são necessários para cenários em que sistemas redundantes locais e as cópias de segurança não é possível recuperar da falha de Olá no Centro de dados principal Olá.

Uma solução de recuperação após desastre boa deve permitir a modelação de planos de recuperação em torno de arquiteturas de aplicações complexas de Olá como o SharePoint. Também deve ter Olá capacidade tooadd personalizado passos toohandle aplicação mapeamentos entre várias camadas e, por conseguinte, fornecendo uma ativação pós-falha de clique único com um RTO inferior no evento Olá de um desastre.

Este artigo descreve em detalhe como tooprotect um através da aplicação SharePoint [do Azure Site Recovery](site-recovery-overview.md). Este artigo abordará as melhores práticas para replicar uma tooAzure de aplicações do SharePoint de três camadas, como pode fazer um exercício de recuperação após desastre e como pode tooAzure de aplicação Olá de ativação pós-falha.

Pode ver Olá vídeo sobre como recuperar uma tooAzure de aplicação de camada de várias abaixo.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que compreende seguinte Olá:

1. [Replicar tooAzure uma máquina virtual](site-recovery-vmware-to-azure.md)
2. Como demasiado[estruturar uma rede de recuperação](site-recovery-network-design.md)
3. [Fazer uma tooAzure de ativação pós-falha de teste](site-recovery-test-failover-to-azure.md)
4. [Fazer uma tooAzure de ativação pós-falha](site-recovery-failover.md)
5. Como demasiado[replicar um controlador de domínio](site-recovery-active-directory.md)
6. Como demasiado[replicar do SQL Server](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>Arquitetura do SharePoint

SharePoint pode ser implementado num ou mais servidores utilizando topologias em camadas e funções de servidor tooimplement uma estrutura de farm que satisfaz os objetivos e objetivos específicos. Um típico grande, a pedido alta server farm do SharePoint que suporta um número elevado de utilizadores em simultâneo e um grande número de itens de conteúdo utilizar agrupamento do serviço como parte da sua estratégia de escalabilidade. Esta abordagem envolve a executar os serviços em servidores dedicados, agrupamento estes serviços em conjunto e, em seguida, aumentar horizontalmente servidores Olá como um grupo. Olá seguinte topologia ilustra serviço Olá e o servidor de agrupamento para uma camada de três farm de servidores do SharePoint. . Consulte a documentação de tooSharePoint e arquiteturas de linha de produto para obter orientações detalhadas sobre diferentes topologias do SharePoint. Pode encontrar mais detalhes sobre a implementação do SharePoint 2013 no [neste documento](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Implementação padrão 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Suporte de recuperação de site

Para criar este artigo, máquinas virtuais VMware com o Windows Server 2012 R2 Enterprise foram utilizadas. SharePoint 2013 Enterprise edition e a edição Enterprise do SQL server 2014 foram utilizados. Como a replicação do Site Recovery desconhece de aplicação, recomendações Olá fornecidas aqui destinam-se toohold esperado nos seguintes cenários, bem como.

### <a name="source-and-target"></a>A origem e destino

**Cenário** | **site secundário tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sim | Sim
**VMware** | Sim | Sim
**Servidor físico** | Sim | Sim

### <a name="sharepoint-versions"></a>Versões do SharePoint
Olá seguintes versões do SharePoint server é suportada.

* Servidor do SharePoint 2013 padrão
* SharePoint server 2013 Enterprise
* Servidor do SharePoint 2016 padrão
* SharePoint server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Coisas tookeep em mente

Se estiver a utilizar um cluster partilhado com base em disco como qualquer camada na sua aplicação, em seguida, não poderá ser toouse capaz de recuperação de Site replicação tooreplicate dessas máquinas virtuais. Pode utilizar replicação nativa fornecida pela aplicação Olá e, em seguida, utilizar um [plano de recuperação](site-recovery-create-recovery-plans.md) toofailover todas as camadas.

## <a name="replicating-virtual-machines"></a>Replicar máquinas virtuais

Siga [esta orientação](site-recovery-vmware-to-azure.md) toostart Olá tooAzure de máquina virtual a replicar.

* Após a conclusão da replicação de Olá, certifique-se de que aceda a máquina virtual de tooeach de cada camada e selecione o mesma conjunto de disponibilidade no ' item replicados > Definições > propriedades > computação e rede '. Por exemplo, se a camada web tiver 3 VMs, certifique-se de Olá todos os 3 VMs são configuradas toobe parte do mesma conjunto de disponibilidade no Azure.

    ![Conjunto de disponibilidade de conjunto](./media/site-recovery-sharepoint/select-av-set.png)

* Para obter orientações sobre a proteger o Active Directory e DNS, consulte demasiado[proteger o Active Directory e DNS](site-recovery-active-directory.md) documento.

* Para obter orientações sobre a proteção de camada de base de dados em execução no SQL server, consulte demasiado[proteger o SQL Server](site-recovery-active-directory.md) documento.

## <a name="networking-configuration"></a>Configuração de redes

### <a name="network-properties"></a>Propriedades da rede

* Para Olá aplicação e a camada Web VMs, configure definições de rede no portal do Azure para que as VMs de Olá toohello anexado à direita DR rede após a ativação pós-falha.

    ![Selecione a rede](./media/site-recovery-sharepoint/select-network.png)


* Se estiver a utilizar um IP estático, em seguida, especifique Olá IP que pretende que sejam Olá tootake de máquina virtual no Olá **IP de destino** campo

    ![Definir o IP estático](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>DNS e o encaminhamento de tráfego

Para a internet com sites, [criar um perfil do Traffic Manager do tipo 'Priority'](../traffic-manager/traffic-manager-create-profile.md) no Olá subscrição do Azure. E, em seguida, configure o seu perfil do Traffic Manager e o DNS no Olá seguinte forma.


| **Onde** | **Origem** | **Destino**|
| --- | --- | --- |
| DNS público | DNS público para sites do SharePoint <br/><br/> Ex: sharepoint.contoso.com | Gestor de Tráfego <br/><br/> contososharepoint.trafficmanager.NET |
| DNS no local | sharepointonprem.contoso.com | IP público no farm do Olá no local |


No perfil do Gestor de tráfego, de Olá [criar Olá pontos finais primário e de recuperação](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Utilize o ponto final externo de Olá para o ponto final no local e o IP público para o ponto final do Azure. Certifique-se de que Olá prioridade é definida de ponto final de tooon local superior.

Uma página de teste numa porta específica (por exemplo, 800) na camada de web SharePoint Olá por ordem para tooautomatically do Gestor de tráfego de anfitrião detetar a ativação pós-falha de post de disponibilidade. Esta é uma solução no caso de não é possível ativar a autenticação anónima em qualquer um dos seus sites do SharePoint.

[Configurar o perfil do Traffic Manager Olá](../traffic-manager/traffic-manager-configure-priority-routing-method.md) com Olá abaixo as definições.

* Método de encaminhamento - 'Priority'
* DNS tempo toolive (TTL) - ' 30 segundos'
* Definições de monitorização do ponto final - se de que pode ativar a autenticação anónima, pode dar um ponto final do Web site específico. Em alternativa, pode utilizar uma página de teste numa porta específica (por exemplo, 800).

## <a name="creating-a-recovery-plan"></a>Criar um plano de recuperação

Um plano de recuperação permite a ativação pós-falha de Olá de várias camadas numa aplicação de várias camada, por conseguinte, manter a consistência da aplicação da sequência. Siga Olá passos abaixo ao criar um plano de recuperação para uma aplicação web de várias camadas. [Saiba mais sobre como criar um plano de recuperação](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>Adicionar grupos de toofailover de máquinas virtuais

1. Crie um plano de recuperação por Olá Adicionar aplicação e a camada Web VMs.
2. Clique em 'Personalizar' toogroup Olá VMs. Por predefinição, todas as VMs fazem parte do 'Grupo 1'.

    ![Personalizar RP](./media/site-recovery-sharepoint/rp-groups.png)

3. Criar outro grupo (grupo 2) e mover camada Web de Olá VMs para o novo grupo de Olá. O escalão de aplicação VMs deve fazer parte do 'Grupo 1' e a camada Web VMs deve fazer parte do 'Grupo 2'. Este é tooensure Olá camada VMs efetuar o arranque primeiro seguido de VMs de camada Web de aplicação.


### <a name="adding-scripts-toohello-recovery-plan"></a>Adicionar scripts toohello plano de recuperação

Pode implementar scripts de Azure Site Recovery Olá normalmente utilizada na sua conta de automatização clicar Olá 'Implementar tooAzure' no botão abaixo. Quando estiver a utilizar qualquer script publicado, certifique-se de que segue orientações Olá no script de Olá.

[![Implementar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Adicione um script de pré-ação too'Group 1' toofailover grupo de disponibilidade SQL. Utilize script de 'ASR-SQL-FailoverAG' Olá publicada nos scripts de exemplo de Olá. Certifique-se de que siga as orientações Olá no script de Olá e Olá necessárias alterações no script de Olá adequadamente.

    ![Adicionar-AG-Script-passo-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Adicionar-AG-Script-passo-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Adicione um script de ação post tooattach um balanceador de carga no Olá efetuado a ativação pós-falha de máquinas virtuais da camada Web (grupo 2). Utilize script de 'ASR AddSingleLoadBalancer' Olá publicada nos scripts de exemplo de Olá. Certifique-se de que siga as orientações Olá no script de Olá e Olá necessárias alterações no script de Olá adequadamente.

    ![Adicionar-LB-Script-passo-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Adicionar-LB-Script-passo-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Adicione um passo manual tooupdate Olá DNS registos toopoint toohello novo farm no Azure.

    * Para a internet com sites, não existem atualizações DNS são ativação pós-falha de post necessária. Siga os passos de Olá descritos nos Olá 'Redes orientações' secção tooconfigure Gestor de tráfego. Se tiver sido configurada Olá perfil do Traffic Manager, tal como descrito na secção anterior Olá, adicione uma porta de fictício de tooopen do script (800 no exemplo de Olá) no Olá VM do Azure.

    * Para os sites com acesso internos, adicione um passo manual tooupdate Olá DNS toopoint registos toohello novo Web camada da carga balanceador IP da VM.

4. Adicionar uma aplicação de pesquisa de toorestore passo manual de uma cópia de segurança ou iniciar um novo serviço de pesquisa.

5. Para restaurar a aplicação de serviço de pesquisa de uma cópia de segurança, siga os passos abaixo.

    * Este método assume que foi efetuada uma cópia de segurança da aplicação de serviço de pesquisa de Olá antes de evento catastrófica Olá e essa cópia de segurança Olá está disponível no site de Olá DR.
    * Isto pode facilmente alcançado Agendar cópia de segurança de Olá (por exemplo, uma vez diariamente) e utilizando uma cópia procedimento tooplace Olá de segurança em site Olá DR. Procedimentos de cópia pode incluir programas de script como AzCopy (cópia do Azure) ou como configurar o DFSR (Serviços de replicação de ficheiros distribuído).
    * Agora que Olá SharePoint de farm está em execução, navegue Olá Administração Central, 'Cópia de segurança e restaurar' e selecione o restauro. Olá restauro interrogates localização de cópia de segurança Olá especificada (poderá ter de valor de Olá tooupdate). Selecione as cópias de segurança de aplicação de serviço de pesquisa do Olá gostaria toorestore.
    * Pesquisa é restaurada. Tenha em atenção que Olá restauro espera toofind Olá mesmo topologia (mesmo número de servidores) e as mesmas rígido letras de unidade atribuídas toothose servidores. Para obter mais informações, consulte ['Aplicação de serviço de pesquisa de restauro no SharePoint 2013'](https://technet.microsoft.com/library/ee748654.aspx) documento.


6. Para começar com uma nova aplicação de serviço de pesquisa, siga os passos abaixo.

    * Este método parte do princípio de que está disponível uma cópia de segurança da base de dados do Olá "Administração de pesquisa" no site de Olá DR.
    * Uma vez que hello outras bases de dados de aplicação de serviço de pesquisa não são replicadas, precisam de toobe recriado. por isso, toodo navegue tooCentral administração e eliminar Olá aplicação de serviço de pesquisa. Em todos os servidores que Olá anfitrião índice de pesquisa, eliminar ficheiros de índice de Olá.
    * Voltar a criar Olá aplicação de serviço de pesquisa e este recria Olá as bases de dados. Recomenda-se toohave um script preparado que recria esta aplicação de service, uma vez que não é possível tooperform todas as ações através de Olá GUI. Por exemplo, definir localização de unidade de índice de Olá e configurar a topologia de pesquisa de Olá são possíveis apenas utilizando cmdlets do PowerShell do SharePoint. Utilizar o cmdlet do Windows PowerShell de Olá SPEnterpriseSearchServiceApplication de restauro e especifique Olá encontram enviadas para registo e base de dados de administração de pesquisa, Search_Service__DB foram replicadas. Este cmdlet fornece configuração de pesquisa de Olá, esquema, propriedades geridas, as regras e origens e cria um conjunto predefinido de Olá outros componentes.
    * Depois de Olá que aplicação de serviço de pesquisa tem de ser recriadas, tem de iniciar uma pesquisa completa para cada Olá toorestore de origem de conteúdo o serviço de pesquisa. Perder algumas informações de análise do farm no local de Olá, tais como recomendações de pesquisa.

7. Depois de concluídos todos os passos de Olá, guardar o plano de recuperação Olá e plano de recuperação final Olá terá um aspeto semelhante.

    ![RP guardado](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Efetuar uma ativação pós-falha de teste
Siga [esta orientação](site-recovery-test-failover-to-azure.md) toodo uma ativação pós-falha de teste.

1.  Aceda tooAzure portal e selecione o Cofre de serviço de recuperação.
2.  Clique no plano de recuperação de Olá criado da aplicação SharePoint.
3.  Clique em "Ativação pós-falha de teste".
4.  Selecione o ponto de recuperação e o processo de ativação pós-falha de teste de Olá toostart rede virtual do Azure.
5.  Assim que estiver ambiente secundário Olá cópias de segurança, pode realizar as validações.
6.  Depois de validações Olá estiverem concluídas, pode clicar em 'Limpeza ativação pós-falha de teste"no plano de recuperação Olá e ambiente de ativação pós-falha de teste de Olá limpos.

Para obter orientações sobre a fazer a ativação pós-falha de teste do AD e DNS, consulte demasiado[considerações de ativação pós-falha do AD e DNS](site-recovery-active-directory.md#test-failover-considerations) documento.

Para obter orientações sobre a efetuar ativação pós-falha de teste para o SQL Server sempre em grupos de disponibilidade, consulte demasiado[fazer testar a ativação pós-falha para o SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) documento.

## <a name="doing-a-failover"></a>Efetuar uma ativação pós-falha
Siga [esta orientação](site-recovery-failover.md) para efetuar uma ativação pós-falha.

1.  Aceda tooAzure portal e selecione o Cofre dos serviços de recuperação.
2.  Clique no plano de recuperação de Olá criado da aplicação SharePoint.
3.  Clique em 'Failover'.
4.  Selecione o processo de ativação pós-falha de Olá de toostart de ponto de recuperação.

## <a name="next-steps"></a>Passos seguintes
Pode saber mais sobre [replicar outras aplicações](site-recovery-workload.md) utilizando a recuperação de sites.
