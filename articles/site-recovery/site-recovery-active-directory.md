---
title: aaaProtect Active Directory e DNS com o Azure Site Recovery | Microsoft Docs
description: "Este artigo descreve como tooimplement uma solução de recuperação após desastre para o Active Directory utilizando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: af1d9b26-1956-46ef-bd05-c545980b72dc
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 7/20/2017
ms.author: pratshar
ms.openlocfilehash: 49903e54f6d6e1839b0571b7a852c6d7517f0aa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="protect-active-directory-and-dns-with-azure-site-recovery"></a>Proteger o Active Directory e DNS com o Azure Site Recovery
As aplicações empresariais, tais como o SharePoint, Dynamics AX e SAP dependem do Active Directory e um toofunction de infraestrutura DNS corretamente. Quando cria uma solução de recuperação após desastre para aplicações, é importante tooremember que precisa de tooprotect e recuperar o Active Directory e DNS antes de Olá outros componentes da aplicação, tooensure coisas funcionarem corretamente quando ocorrer um desastre.

Recuperação de sites é um serviço Azure que permite a recuperação de desastre através da orquestração da replicação, ativação pós-falha e recuperação de máquinas virtuais. Recuperação de sites suporta um número de cenários de replicação tooconsistently proteger e totalmente integrada a ativação pós-falha máquinas virtuais e aplicações tooprivate, public ou fornecedor de alojamento nuvens.

Utilizar a recuperação de sites, pode criar um plano de recuperação após desastre automatizado completa para o Active Directory. Quando ocorrem interrupções, pode iniciar uma ativação pós-falha em segundos a partir de qualquer lugar e obter do Active Directory em execução dentro de alguns minutos. Se tiver implementado o Active Directory para várias aplicações, tais como o SharePoint e SAP no seu site primário e pretende toofail através de completa do local Olá, pode efetuar a ativação pós-falha do Active Directory a utilizar primeiro a recuperação de sites e, em seguida, ativação pós-falha Olá outras aplicações utilizar planos de recuperação específico da aplicação.

Este artigo explica como toocreate uma solução de recuperação após desastre para o Active Directory, como tooperform ativação pós-falha planeada, não planeada e as ativações pós-falha de teste utilizando um plano de recuperação de um clique, Olá pré-requisitos e configurações suportadas.  Deve estar familiarizado com o Active Directory e o Azure Site Recovery antes de começar.

## <a name="replicating-domain-controller"></a>Replicar o controlador de domínio

Terá de toosetup [replicação do Site Recovery](#enable-protection-using-site-recovery) , pelo menos, uma máquina virtual que aloja o controlador de domínio e DNS. Se tiver [vários controladores de domínio](#environment-with-multiple-domain-controllers) no seu ambiente, além disso tooreplicating Olá máquina virtual de controlador de domínio com a recuperação de Site, segurança, também deverá dispor de tooset um [docontroladordedomínioadicional](#protect-active-directory-with-active-directory-replication) no site de destino Olá (Azure ou num datacenter secundário no local). 

### <a name="single-domain-controller-environment"></a>Ambiente de controlador de domínio único
Se tiver algumas aplicações e apenas um único controlador de domínio e pretende toofail ao longo de todo o site Olá em conjunto, em seguida, é recomendável utilizar o controlador de domínio do Site Recovery tooreplicate Olá toohello site secundário (se estiver a efetuar ativação pós-falha tooAzure ou site secundário tooa). Olá mesmo replicado domínio máquina virtual de controlador/DNS pode ser utilizada para [ativação pós-falha de teste](#test-failover-considerations) bem.

### <a name="environment-with-multiple-domain-controllers"></a>Ambiente com vários controladores de domínio
Se tem muitas aplicações e existir mais do que um controlador de domínio no ambiente de Olá, ou se planear toofail ao longo de algumas aplicações simultaneamente, recomendamos que que além controlador de domínio de Olá tooreplicating virtual máquina com a recuperação de Site é também configurar um [controlador de domínio adicional](#protect-active-directory-with-active-directory-replication) no site de destino Olá (Azure ou num datacenter secundário no local). Para [ativação pós-falha de teste](#test-failover-considerations), utilize o controlador de domínio replicado pela recuperação de sites e para ativação pós-falha, Olá o controlador de domínio adicional no site de destino Olá. 


Olá secções seguintes explicam como tooenable proteção para um controlador de domínio no Site Recovery e como tooset se um controlador de domínio no Azure.

## <a name="prerequisites"></a>Pré-requisitos
* Uma implementação no local do servidor do Active Directory e DNS.
* Um cofre dos serviços de recuperação de Site do Azure de uma subscrição do Microsoft Azure.
* Se estiver a replicar tooAzure, execute a ferramenta de avaliação de preparação de Máquina Virtual do Azure de Olá no VMs tooensure está compatíveis com as VMs do Azure e do Azure Site Recovery Services.

## <a name="enable-protection-using-site-recovery"></a>Ativar a proteção com a recuperação de Site
### <a name="protect-hello-virtual-machine"></a>Proteger a máquina virtual de Olá
Ative a proteção da máquina virtual de controlador/DNS de domínio do Olá no Site Recovery. Configure definições de recuperação de Site com base no tipo de máquina virtual de Olá (Hyper-V ou VMware). controlador de domínio de Olá replicado com a recuperação de sites é utilizada para [ativação pós-falha de teste](#test-failover-considerations). Certifique-se de que cumpre os requisitos de Olá:

1. controlador de domínio Olá é um servidor de catálogo global
2. controlador de domínio Olá deve ser o proprietário da função FSMO Olá para as funções que será necessário durante uma ativação pós-falha de teste (caso contrário, estas funções terá toobe [seized](http://aka.ms/ad_seize_fsmo) após a ativação pós-falha de Olá)

### <a name="configure-virtual-machine-network-settings"></a>Configurar as definições de rede de máquina virtual
Para a máquina de virtual controlador/DNS do domínio Olá, configure definições de rede na recuperação de Site para que máquina virtual de Olá será toohello anexado de rede à direita após a ativação pós-falha. 

![Definições de rede VM](./media/site-recovery-active-directory/DNS-Target-IP.png)

## <a name="protect-active-directory-with-active-directory-replication"></a>Proteger o Active Directory com a replicação do Active Directory
### <a name="site-to-site-protection"></a>Proteção de site a site
Crie um controlador de domínio no site secundário Olá. Quando promover a função de controlador de domínio de tooa servidor Olá, especifique o nome de Olá do Olá mesmo domínio que está a ser utilizado no site primário Olá. Pode utilizar Olá **serviços e locais do Active Directory** snap-in tooconfigure definições de ligação de site Olá objeto sites de Olá toowhich são adicionados. Ao configurar as definições de uma ligação de site, pode controlar quando a replicação ocorre entre dois ou mais sites,. e frequên. Para obter mais informações, consulte [agendar a replicação entre Sites](https://technet.microsoft.com/library/cc731862.aspx).

### <a name="site-to-azure-protection"></a>Proteção de site para o Azure
Siga as instruções de Olá demasiado[criar um controlador de domínio numa Azure virtual network](../active-directory/active-directory-install-replica-active-directory-domain-controller.md). Quando promover a função de controlador de domínio de tooa servidor Olá, especificar Olá mesmo nome de domínio que é utilizado no site primário Olá.

Em seguida, [reconfigurar o servidor DNS Olá para a rede virtual Olá](../active-directory/active-directory-install-replica-active-directory-domain-controller.md#reconfigure-dns-server-for-the-virtual-network), servidor DNS de Olá toouse no Azure.

![Rede do Azure](./media/site-recovery-active-directory/azure-network.png)

**DNS na rede de produção do Azure**

## <a name="test-failover-considerations"></a>Considerações de ativação pós-falha de teste
Ativação pós-falha de teste ocorre numa rede que está isolada da rede de produção para que não há nenhum impacto nas cargas de trabalho de produção.

A maioria das aplicações também requerem presença Olá um controlador de domínio e um toofunction de servidor DNS. Por conseguinte, antes de aplicação Olá é a ativação pós-falha, um controlador de domínio tem de toobe criado no Olá isolada rede toobe utilizado para ativação pós-falha de teste. Olá toodo de forma mais fácil é tooreplicate uma máquina virtual de controlador/DNS de domínio com a recuperação de Site. Em seguida, execute uma ativação pós-falha de teste da máquina de virtual de controlador de domínio Olá antes de executar uma ativação pós-falha de teste Olá do plano de recuperação para a aplicação Olá. Eis como pode fazê-lo:

1. [Replicar](site-recovery-replicate-vmware-to-azure.md) Olá máquinas de virtuais do controlador/DNS do domínio utilizando a recuperação de sites.
1. Crie uma rede isolada. Qualquer rede virtual criada no Azure, por predefinição está isolada de outras redes. Recomendamos que o intervalo de endereços IP Olá para esta rede é igual da sua rede de produção. Não conseguir ative a conetividade site a site nesta rede.
1. Forneça um endereço IP de DNS na rede de Olá criada, como endereço IP Olá que espera tooget de máquina virtual Olá DNS. Se estiver a replicar tooAzure, em seguida, forneça endereços IP Olá para Olá VM que é utilizada na ativação pós-falha no **IP de destino** definição **computação e rede** definições. 

    ![IP de destino](./media/site-recovery-active-directory/DNS-Target-IP.png) **IP de destino**

    ![Rede de teste do Azure](./media/site-recovery-active-directory/azure-test-network.png)

    **DNS na rede de teste do Azure**

> [!TIP]
> Máquinas virtuais de teste de toocreate numa sub-rede do mesmo nome de tentativas de recuperação de site e utilizar Olá IP mesmo que foi fornecido no **computação e rede** as definições da máquina virtual de Olá. Se a sub-rede do mesmo nome não está disponível no Olá rede virtual do Azure fornecida para ativação pós-falha de teste, em seguida, a máquina virtual de teste é criada na primeira sub-rede da Olá por ordem alfabética. Se o IP de destino Olá fizer parte de Olá escolhido sub-rede, recuperação de Site tenta toocreate Olá ativação pós-falha máquina virtual de teste utilizando Olá IP de destino. Se Olá IP de destino não faz parte de Olá escolhido sub-rede, em seguida, máquina de virtual de ativação pós-falha de teste obtém criada utilizando qualquer IP disponível no Olá escolhido sub-rede. 
>
>


1. Se estiver a replicar site no local de tooanother e estiver a utilizar DHCP, siga as instruções de Olá demasiado[configurar o DNS e DHCP para ativação pós-falha de teste](site-recovery-test-failover-vmm-to-vmm.md#prepare-dhcp)
1. Efetue uma ativação pós-falha de teste da máquina virtual Olá domínio controlador execute numa rede isolada Olá. Utilize mais recente disponível **aplicação consistente** ponto de recuperação da Olá domínio controlador máquina virtual toodo Olá ativação pós-falha de teste. 
1. Execute uma ativação pós-falha de teste para o plano de recuperação de Olá contém máquinas virtuais da aplicação Olá. 
1. Depois do teste concluído, **ativação pós-falha de teste de limpeza** na máquina de virtual de controlador de domínio Olá. Este passo elimina Olá controlador de domínio que foi criada para ativação pós-falha de teste.


### <a name="removing-reference-tooother-domain-controllers"></a>Remover os controladores de domínio de tooother de referência
Quando estão a fazer uma ativação pós-falha de teste, não coloque todos os controladores de domínio de Olá na rede de teste de Olá. referência de Olá tooremove dos outros controladores de domínio existentes no seu ambiente de produção, poderá ter demasiado[obter funções de FSMO Active Directory](http://aka.ms/ad_seize_fsmo) e [limpeza de metadados](https://technet.microsoft.com/library/cc816907.aspx) para o domínio em falta controladores. 



> [!IMPORTANT]
> Algumas das configurações de Olá descritas na seguinte secção de Olá não são configurações de controlador de domínio do Olá padrão/predefinidas. Se não quiser toomake estes controlador de domínio de produção de tooa de alterações, em seguida, que pode criar um toobe dedicado de controlador de domínio utilizado para ativação pós-falha de teste de recuperação de Site e efetuar estas alterações toothat.  
>
>

### <a name="issues-because-of-virtualization-safeguards"></a>Problemas devido a proteções de Virtualização 

Começando com o Windows Server 2012, [incorporadas proteções adicionais para os serviços de domínio do Active Directory](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100). Estas salvaguardas de ajudam a proteger os controladores de domínio virtualizados contra o USN reverte, desde que a plataforma de hipervisor subjacente Olá suporta VM-GenerationID. Azure suporta VM-GenerationID, o que significa que os controladores de domínio que executam o Windows Server 2012 ou posterior no Azure máquinas virtuais têm proteções adicionais Olá. 


Quando Olá VM-Generation ID é reposta, o invocationID de Olá da base de dados do Olá AD DS também é reposto, rejeitado Olá conjunto de RID e SYSVOL está marcado como não autoritativo. Para obter mais informações, consulte [introdução tooActive Virtualização de serviços de domínio do](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/introduction-to-active-directory-domain-services-ad-ds-virtualization-level-100) e [virtualizar o DFSR com segurança](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)

Falha ao longo do tooAzure pode fazer com que a reposição do VM-GenerationID e que inicia no proteções adicionais Olá quando inicia a máquina de virtual de controlador de domínio Olá no Azure. Isto poderá resultar num **atraso significativo** a máquina de virtual de controlador de domínio toohello toologin capaz de utilizador. Uma vez que este controlador de domínio apenas seria possível utilizar uma ativação pós-falha de teste, as proteções de Virtualização não são necessárias. tooensure não altera VM-GenerationID da máquina de virtual de controlador de domínio Olá, em seguida, pode alterar o valor Olá seguintes too4 DWORD no controlador de domínio do Olá no local.

        
        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\gencounter\Start
 

#### <a name="symptoms-of-virtualization-safeguards"></a>Sintomas das proteções de Virtualização
 
Se as proteções de Virtualização tem kicked após uma ativação pós-falha de teste, poderá ver um ou mais dos seguintes sintomas:  

Alteração do ID de geração

![Alteração do ID de geração](./media/site-recovery-active-directory/Event2170.png)

Alteração do ID de invocação

![Alteração do ID de invocação](./media/site-recovery-active-directory/Event1109.png)

Partilhas de SYSVOL e Netlogon não estão disponíveis

![Partilha SYSVOL](./media/site-recovery-active-directory/sysvolshare.png)

![NTFRS Sysvol](./media/site-recovery-active-directory/Event13565.png)

São eliminados quaisquer bases de dados DFSR

![Eliminar da base de dados de DFSR](./media/site-recovery-active-directory/Event2208.png)


> [!IMPORTANT]
> Algumas das configurações de Olá descritas na seguinte secção de Olá não são configurações de controlador de domínio do Olá padrão/predefinidas. Se não quiser toomake estes controlador de domínio de produção de tooa de alterações, em seguida, que pode criar um toobe dedicado de controlador de domínio utilizado para ativação pós-falha de teste de recuperação de Site e efetuar estas alterações toothat.  
>
>


### <a name="troubleshooting-domain-controller-issues-during-test-failover"></a>Resolução de problemas problemas de controlador de domínio durante a ativação pós-falha de teste


Na linha de comandos, execute Olá os seguintes comandos toocheck se pastas SYSVOL e NETLOGON são partilhadas:

    NET SHARE

Na linha de comandos Olá, execute Olá os seguintes comandos tooensure Olá controlador de domínio está a funcionar corretamente.

    dcdiag /v > dcdiag.txt

No registo de saída Olá, procure o seguinte tooconfirm de texto Olá controlador de domínio está a funcionar corretamente. 

* "test transmitido conectividade"
* "transmitido teste publicidade"
* "test transmitido MachineAccount"

Se hello anteriores condições forem satisfeitas, é provável que controlador de domínio Olá está a funcionar corretamente. Caso contrário, tente os passos seguintes.


* Efetue um restauro autoritativa de controlador de domínio Olá.
    * Embora seja [não recomendado toouse FRS replicação](https://blogs.technet.microsoft.com/filecab/2014/06/25/the-end-is-nigh-for-frs/), mas se ainda estiver a utilizar, em seguida, siga os passos de Olá fornecidos [aqui](https://support.microsoft.com/kb/290762) toodo um restauro autoritativa. Pode ler mais sobre Burflags abordou na ligação anterior Olá [aqui](https://blogs.technet.microsoft.com/janelewis/2006/09/18/d2-and-d4-what-is-it-for/).
    * Se estiver a utilizar replicação de DFSR, em seguida, siga os passos de Olá disponíveis [aqui](https://support.microsoft.com/kb/2218556) toodo um restauro autoritativa. Também pode utilizar o Powershell funções disponíveis neste [ligação](https://blogs.technet.microsoft.com/thbouche/2013/08/28/dfsr-sysvol-authoritative-non-authoritative-restore-powershell-functions/) para esta finalidade. 
    
* Ignorar os requisitos de sincronização inicial, definindo a seguir too0 chave do registo no controlador de domínio do Olá no local. Se esta DWORD não existir, em seguida, pode criá-la sob o nó 'Parameters'. Pode ler mais sobre o assunto [aqui](https://support.microsoft.com/kb/2001093)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Repl Perform Initial Synchronizations

* Desative o requisito de Olá que um servidor de catálogo global é toovalidate disponíveis início de sessão do utilizador através da definição a seguir too1 chave do registo no controlador de domínio do Olá no local. Se esta DWORD não existir, pode criá-la sob o nó 'Lsa'. Pode ler mais sobre o assunto [aqui](http://support.microsoft.com/kb/241789)

        HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\IgnoreGCFailures



### <a name="dns-and-domain-controller-on-different-machines"></a>DNS e controlador de domínio em computadores diferentes
Se o DNS não está no Olá mesma máquina virtual como controlador de domínio Olá, terá de toocreate uma VM de DNS Olá ativação pós-falha de teste. Se não estiverem na mesma VM de Olá, pode ignorar esta secção.

Pode utilizar um servidor DNS de raiz e criar todas as zonas de Olá necessário. Por exemplo, se o domínio do Active Directory for contoso.com, pode criar uma zona DNS com o nome de Olá contoso.com. entradas de Olá correspondente tooActive diretório tem de ser atualizadas no DNS, da seguinte forma:

1. Certifique-se de que estas definições estão em vigor antes de qualquer outra máquina virtual no plano de recuperação Olá é apresentada:
   
   * zona de Olá deve ter o nome depois de nome de raiz de floresta Olá.
   * zona de Olá tem de ser de segurança de ficheiros.
   * zona de Olá deve estar ativada para atualizações seguras e não segura.
   * resolução de Olá da máquina de virtual de controlador de domínio Olá deve ponto toohello endereço IP da máquina de virtual Olá DNS.
2. Execute o seguinte comando na máquina de virtual do controlador de domínio de Olá:
   
    `nltest /dsregdns`
3. Adicionar uma zona no servidor DNS Olá, permita que as atualizações não segura e adicione uma entrada para o mesmo tooDNS:
   
        dnscmd /zoneadd contoso.com  /Primary
        dnscmd /recordadd contoso.com  contoso.com. SOA %computername%.contoso.com. hostmaster. 1 15 10 1 1
        dnscmd /recordadd contoso.com %computername%  A <IP_OF_DNS_VM>
        dnscmd /config contoso.com /allowupdate 1

## <a name="next-steps"></a>Passos seguintes
Leitura [que cargas de trabalho posso proteger?](site-recovery-workload.md) toolearn mais sobre como proteger cargas de trabalho empresariais com o Azure Site Recovery.

