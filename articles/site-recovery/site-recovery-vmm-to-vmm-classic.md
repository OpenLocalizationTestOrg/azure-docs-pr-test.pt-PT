---
title: "aaaReplicate VMs de Hyper-V no site secundário do VMM tooa (clássica do Azure) | Microsoft Docs"
description: "Este artigo descreve como tooreplicate VMs de Hyper-V no VMM nuvens tooa site VMM secundário com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replicar máquinas virtuais de Hyper-V no VMM nuvens tooa site secundário do VMM
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clássico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Olá serviço Azure Site Recovery contribui tooyour continuidade do negócio e a estratégia de recuperação (BCDR) desastre através da orquestração de replicação, ativação pós-falha e recuperação de máquinas virtuais e servidores físicos. As máquinas podem ser replicada tooAzure ou centro de dados do tooa secundário no local. Para uma descrição geral, leia [O que é o Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Descrição geral
Este artigo descreve como tooreplicate Hyper-V máquinas virtuais no Hyper-V anfitrião servidores que são geridos no VMM nuvens toosecondary site do VMM utilizando o Azure Site Recovery.

artigo de Olá inclui pré-requisitos, mostra como instalar tooset configurar um cofre de recuperação de sites, Olá fornecedor do Azure Site Recovery na origem e servidores do VMM de destino, registar os servidores de Olá no Cofre de Olá, configurar definições de proteção de nuvens VMM e, em seguida, ativar proteção para VMs de Hyper-V. Concluir a cópia de segurança por teste toomake de ativação pós-falha de Olá se que tudo está a funcionar conforme esperado.

Publique comentários ou perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Arquitetura
imagem de Olá abaixo mostra os canais de comunicação diferente de Olá e portas utilizadas pelo Azure Site Recovery para replicação e de orquestração

![Topologia de E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Antes de começar
Certifique-se de que tem os pré-requisitos:

| **Pré-requisitos** | **Detalhes** |
| --- | --- |
| **Azure** |Necessita de uma conta do [Microsoft Azure](https://azure.microsoft.com/). Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Sites. |
| **VMM** |Precisa de, pelo menos, um servidor VMM.<br/><br/>servidor do VMM Olá deve estar a executar, pelo menos, System Center 2012 SP1 com Olá mais recentes atualizações cumulativas.<br/><br/>Se quiser tooset configurar a proteção com um único servidor do VMM, precisa de, pelo menos, dois nuvens configuradas no servidor de Olá.<br/><br/>Se pretender que a proteção de toodeploy com dois servidores do VMM, cada servidor tem de ter, pelo menos, uma nuvem configurada no servidor VMM principal Olá pretender tooprotect e uma nuvem configurada no servidor do VMM secundário Olá pretende toouse para proteção e recuperação<br/><br/>Todas as nuvens do VMM devem ter o conjunto de perfis de capacidade de Hyper-V de Olá.<br/><br/>nuvem de origem Olá que pretende que o tooprotect tem de conter um ou mais grupos de anfitriões do VMM. |
| **Hyper-V** |Precisa de um ou mais servidores de anfitrião de Hyper-V no Olá primários e secundários grupos de anfitriões VMM e um ou mais máquinas virtuais em cada servidor de anfitrião do Hyper-V.<br/><br/>Olá servidores de Hyper-V anfitrião e de destino tem de estar em execução, pelo menos, Windows Server 2012 com a função de Olá Hyper-V e ter Olá atualizações mais recentes instaladas.<br/><br/>Qualquer servidor de Hyper-V que contenha VMs que pretende tooprotect tem de estar localizado numa nuvem VMM.<br/><br/>Se estiver a executar o Hyper-V num cluster, tenha em atenção que Mediador de clusters não é criado automaticamente se tiver um cluster de baseadas no endereço IP estático. Terá de Mediador de clusters de Olá tooconfigure manualmente. [Saiba mais](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) na entrada de blogue de Aidan Finn. |
| **Mapeamento da rede** |Pode configurar toomake de mapeamento de rede se de que máquinas virtuais replicadas ideal são colocadas em servidores de anfitrião de Hyper-V secundários após a ativação pós-falha, e que possam estabelecer a ligação tooappropriate redes VM. Se não configurar o mapeamento da rede, as VMs de réplica será ligada tooany rede após a ativação pós-falha.<br/><br/>tooset segurança mapeamento da rede durante a implementação, certifique-se que Olá máquinas de virtuais no servidor de anfitrião do Hyper-V de origem Olá tooa ligado rede VM do VMM. Essa rede deve ser ligado tooa rede lógica que está associado a nuvem de Olá. < br /<br/>nuvem de destino Olá Olá VMM do servidor secundário que utilizar para recuperação deve ter uma rede VM correspondente configurada e, por sua vez deve ser ligado tooa correspondente a rede lógica que está associado a nuvem de destino Olá. |
| **Mapeamento de armazenamento** |Por predefinição quando replicar uma máquina virtual num Hyper-V anfitrião servidor tooa destino Hyper-V anfitrião servidor de origem, dados replicados são guardados na localização predefinida Olá indicado para o anfitrião de Hyper-V de destino Olá no Gestor de Hyper-V. Para obter mais controlo sobre onde os dados replicados são guardados, pode configurar o mapeamento de armazenamento<br/><br/> armazenamento de tooconfigure mapeamento, terá tooset segurança classificações de armazenamento na origem de Olá e servidores do VMM de destino antes de começar a implementação. |

## <a name="step-1-create-a-site-recovery-vault"></a>Passo 1: Criar um cofre de Recuperação de Sites
1. Inicie sessão no toohello [Portal de gestão](https://portal.azure.com) hello do servidor do VMM pretende tooregister.
2. Expanda **serviços de dados** > **dos serviços de recuperação** e clique em **Cofre de recuperação de Site**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. No **nome**, introduza um cofre de Olá tooidentify nome amigável.
5. No **região** selecione Olá região geográfica do Cofre de Olá. regiões toocheck suportada veja disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Clique em **Criar cofre**.

    ![Criar Cofre](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Verificação do Estado de Olá barra que cofre Olá foi criada. Olá cofre será listado como **Active Directory** na página do Olá principal dos serviços de recuperação.

## <a name="step-2-generate-a-vault-registration-key"></a>Passo 2: Gerar uma chave de registo do cofre
Gere uma chave de registo no Cofre de Olá. Depois de transferir Olá fornecedor do Azure Site Recovery e instalá-lo no servidor do VMM Olá, irá utilizar este servidor do VMM Olá tooregister chave no Cofre de Olá.

1. No Olá **dos serviços de recuperação** página, clique na página de início rápido Olá cofre tooopen Olá. Início rápido também pode ser aberto em qualquer altura utilizando o ícone de Olá.

    ![Ícone de Início Rápido](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. Na lista pendente de Olá, selecione **entre dois sites VMM no local**.
3. No **preparar servidores VMM**, clique em **gerar ficheiro de chave de registo**. ficheiro de chave Olá é gerado automaticamente e é válido durante 5 dias após ser gerado. Se não estiver a aceder a Olá portal do Azure hello do servidor do VMM terá toocopy este servidor de ficheiros de toohello.

    ![Chave de registo](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Passo 3: Instalar Olá Azure Site Recovery Provider
1. No Olá **início rápido** na página **preparar servidores VMM**, clique em **transferir o Microsoft Azure Site Recovery Provider para instalar nos servidores VMM** tooobtain Olá mais recente versão do ficheiro de instalação do fornecedor de Olá.
2. Execute este ficheiro no servidor de origem Olá do VMM.

   > [!NOTE]
   > Se o VMM for implementado num cluster e estiver a instalar Olá fornecedor para Olá pela primeira vez instalá-la a um nó ativo e concluir o servidor do Olá instalação tooregister Olá VMM no Cofre de Olá. Em seguida, instale Olá fornecedor no Olá outros nós. Tenha em atenção que, se estiver a atualizar Olá fornecedor terá tooupgrade em todos os nós porque deveriam todos estar em execução Olá mesma versão do fornecedor.
   >
   >
3. Olá instalador algumas **verificação de pré-requisitos** e pedidos Olá de toostop permissão VMM toobegin a configuração do fornecedor de serviço. Olá serviço VMM será reiniciado automaticamente após a conclusão do programa de configuração. Se estiver a instalar num VMM cluster que será solicitado função de Cluster toostop Olá.
4. Em **Microsoft Update** pode optar por atualizações. Com esta definição ativadas as atualizações do fornecedor serão instaladas tooyour política do Microsoft Update de acordo com.

    ![Atualizações da Microsoft](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. localização de instalação de Olá estiver definida demasiado**<SystemDrive>\Programas\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Clique em Olá instalação botão toostart instalar Olá fornecedor.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Depois de Olá fornecedor está instalado, clique em **registar** tooregister servidor Olá cofre Olá.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. No **nome do cofre**, verifique o nome de Olá do Cofre de Olá no qual Olá servidor será registado. Clique em *Seguinte*.

    ![Registo do servidor](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. No **ligação à Internet** especificar como Olá fornecedor em execução no Olá VMM server liga toohello Internet. Selecione **ligar com definições de proxy existentes** toouse Olá Internet ligação predefinições configuradas no servidor de Olá.

    ![Definições da Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Se quiser toouse um proxy personalizado, deve configurá-lo antes de instalar Olá fornecedor. Será executado um teste de ligação de proxy do toocheck Olá, quando configurar as definições de proxy personalizado.
   * Se utilizar um proxy personalizado ou o proxy predefinido exigir autenticação terá tooenter Olá os detalhes do proxy, incluindo endereço de proxy de Olá e a porta.
   * Os seguintes urls devem ser acessíveis a partir do Olá servidor VMM e anfitriões de Hyper-v Olá
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Permitir que os endereços IP Olá descritos em [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e o protocolo HTTPS (443). Terá de intervalos de IP da lista de toowhite da Olá região do Azure que planeia toouse e de EUA oeste.
   * Se utilizar um proxy personalizado uma conta RunAs do VMM (DRAProxyAccount) será automaticamente criada utilizando Olá especificada credenciais de proxy. Configure o servidor de proxy de Olá, para que esta conta pode autenticar com êxito. as definições da conta RunAs do VMM Olá podem ser modificadas na consola do VMM Olá. toodo, abra Olá **definições** área de trabalho, expanda **segurança**, clique em **contas Run as**e, em seguida, modifique a palavra-passe de Olá para DRAProxyAccount. Terá de serviço do VMM toorestart Olá para que esta definição surta efeito.
9. No **chave de registo**, selecione chave Olá que transferido a partir do Azure Site Recovery e copiou toohello o servidor do VMM.
10. definição de encriptação de Olá só é utilizada quando replicar VMs Hyper-V no tooAzure de nuvens do VMM. Se estiver a replicar tooa site secundário não é utilizado.
11. No **nome do servidor**, especifique o servidor de nome amigável tooidentify Olá VMM no Cofre de Olá. Numa configuração de cluster especifique o nome de função de cluster do Olá VMM.
12. No **sincronizar metadados da nuvem** Selecione se pretende toosynchronize metadados para todas as nuvens no servidor do VMM Olá Vault Olá. Esta ação só deverá toohappen uma vez em cada servidor. Se não quiser toosynchronize todas as nuvens, pode deixar esta definição desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem de Olá na consola do VMM Olá.
13. Clique em **seguinte** processo de Olá toocomplete. Após o registo, os metadados hello do servidor do VMM são obtidos pelo Azure Site Recovery. Olá servidor é apresentado na **servidores VMM** > **servidores** no Cofre de Olá.

    ![Servidores](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Instalação com linha de comandos
Também pode ser instalado Olá Azure Site Recovery Provider Olá linha de comandos. Este método pode ser utilizado tooinstall fornecedor Olá um Server CORE do Windows Server 2012 R2.

1. Transferir Olá fornecedor e o registo do ficheiro de chave tooa pasta de instalação. Por exemplo: C:\ASR.
2. Parar Olá serviço do System Center Virtual Machine Manager
3. Extraia o instalador de fornecedor Olá executando estes comandos numa linha de comandos com **administrador** privilégios:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instale o fornecedor de Olá executando:

        C:\ASR> setupdr.exe /i
5. Registe o fornecedor de Olá em execução:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Onde estão os parâmetros de Olá:

* **/Credentials**: o parâmetro obrigatório que especifica a localização de Olá no qual Olá se encontra o ficheiro de chave de registo  
* **/ FriendlyName**: o parâmetro obrigatório para o nome de Olá Olá Hyper-V do servidor de anfitrião que é apresentado no portal do Azure Site Recovery Olá.
* **/ EncryptionEnabled**: o parâmetro opcional que terá de toouse apenas em Olá VMM tooAzure cenário se precisar de encriptação das máquinas virtuais Inativos no Azure. Certifique-se que o nome do ficheiro de Olá Olá fornecer tem um **. pfx** extensão.
* **/proxyAddress**: o parâmetro opcional que especifica o endereço de hello do servidor de proxy de Olá.
* **/proxyaddress**: o parâmetro opcional que especifica a porta de hello do servidor de proxy de Olá.
* **/proxyUsername**: o parâmetro opcional que especifica o nome de utilizador de Proxy Olá (caso o proxy precise de autenticação).
* **/proxyPassword**: o parâmetro opcional que especifica Olá palavra-passe para autenticar com o servidor de proxy de Olá (se o proxy precise de autenticação).  

## <a name="step-4-configure-cloud-protection-settings"></a>Passo 4: Configurar a nuvem as definições de proteção
Depois de estarem registados servidores do VMM, pode configurar as definições de proteção de nuvem. Se ativou a opção de Olá **sincronizar dados de nuvem com o Cofre de Olá** quando instalou Olá fornecedor para todas as nuvens no servidor do VMM Olá irão aparecer na Olá **itens protegidos** separador no Cofre de Olá. Se não lhe foi pode sincronizar uma nuvem específica com o Azure Site Recovery na Olá **geral** separador da página de propriedades de nuvem Olá na consola do VMM Olá.

![Nuvem Publicada](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. Na página de início rápido de Olá, clique em **configurar a proteção de nuvens VMM**.
2. No Olá **nuvens VMM** separador, selecione a nuvem de Olá que pretende tooconfigure e aceda toohello **configuração** separador.
3. No **destino**, selecione **VMM**.
4. No **localização de destino**, selecione Olá servidor VMM no local que gere nuvem Olá pretende toouse para recuperação.
5. No **nuvem de destino**, selecione a nuvem de destino Olá pretende toouse para ativação pós-falha de máquinas virtuais da nuvem de origem Olá. Tenha em atenção que:

   * Recomendamos que selecione uma nuvem de destino cumpre os requisitos de recuperação para as máquinas virtuais de Olá que vai proteger.
   * Uma nuvem só pode pertencer tooa par de nuvem única — como um site primário ou de uma nuvem de destino.
6. No **copiar frequência**, especifique a frequência devem ser sincronizados dados entre localizações de origem e destino 5he. Tenha em atenção que esta definição só é relevante quando o anfitrião de Hyper-V Olá está a executar o Windows Server 2012 R2. Para outros servidores, é utilizada uma predefinição de cinco minutos.
7. No **pontos de recuperação adicionais**, especifique se pretende pontos adicionais de toocreate. valor de predefinição zero Olá indica que apenas Olá mais recente ponto de recuperação para uma máquina virtual primária é armazenado num servidor de anfitrião de réplica. Tenha em atenção que ativar vários pontos de recuperação requer armazenamento adicional para instantâneos Olá que estão armazenados em cada ponto de recuperação. Por predefinição, os pontos de recuperação são criados a cada hora, para que cada ponto de recuperação contém visão de uma hora de dados. valor de ponto de recuperação Olá atribuir para a máquina virtual de Olá na consola do VMM Olá não deve ser inferior ao valor de Olá que atribuir na consola do Azure Site Recovery Olá.
8. No **frequência de instantâneos consistentes com aplicações**, especifique a frequência toocreate de instantâneos consistentes com aplicações. Hyper-V utiliza dois tipos de instantâneos – um instantâneo padrão que fornece um instantâneo incremental de toda a máquina virtual Olá e um instantâneo consistente com aplicações, que tira um instantâneo de ponto no tempo dos dados de aplicação Olá no interior da máquina virtual de Olá. Instantâneos consistentes com aplicações utilizam tooensure do serviço de cópia de sombra de Volume (VSS) que aplicações estão num estado consistente quando se obtém o instantâneo de Olá. Tenha em atenção que se ativar instantâneos consistentes com aplicações, irá afetar desempenho Olá das aplicações em execução em máquinas virtuais de origem. Certifique-se de que valor Olá definido é inferior ao número de Olá de pontos de recuperação adicionais que configura.

    ![Configurar definições de proteção](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. No **compressão de transferência de dados**, especifique se os dados replicados que são transferidos devem ser comprimidos.
10. No **autenticação**, especifique a forma como o tráfego for autenticado entre Olá principal e servidores de anfitrião do Hyper-V de recuperação. Selecione HTTPS, salvo se tiver um ambiente de Kerberos configurado de trabalho. O Azure Site Recovery irá configurar automaticamente certificados para autenticação HTTPS. Não é necessária nenhuma configuração manual. Se selecionar Kerberos, uma permissão Kerberos será utilizada para autenticação mútua de servidores de anfitrião Olá. Por predefinição, a porta 8083 e 8084 (para certificados) será aberta em Olá Firewall do Windows nos servidores de anfitrião do Hyper-V Olá. Tenha em atenção que esta definição só é relevante para servidores de anfitrião de Hyper-V em execução no Windows Server 2012 R2.
11. No **porta**, modificar o número da porta na qual origem Olá Olá e escuta de computadores anfitrião para o tráfego de replicação de destino. Por exemplo, poderá modificar Olá definição se pretender que a limitação para o tráfego de replicação tooapply largura de banda de rede de Quality of Service (QoS). Certifique-se de que a porta de Olá não é utilizada por qualquer outra aplicação e que se encontra aberto as definições da firewall Olá.
12. No **método de replicação**, especifique a forma como a replicação dos dados a partir de localizações de tootarget de origem inicial Olá será tratada, antes de começa a replicação normal:

    * **Rede**— cópia dos dados através de rede de Olá pode ser morosa e consome. Recomendamos que utilize esta opção se a nuvem de Olá contém máquinas virtuais com os discos rígidos virtuais relativamente pequenos, e se o site primário Olá é o site secundário toohello ligado através de uma ligação com largura de banda wide. Pode especificar cópia Olá deve iniciar de imediato ou selecione uma hora. Se utilizar a replicação de rede, recomendamos que agendá-la durante as horas de ponta.
    * **Offline**— este método Especifica que a replicação inicial Olá irá ser efetuada utilizando suportes de dados externas. Isto é útil se pretender tooavoid degradação do desempenho de rede ou em localizações geograficamente remoto. toouse este método, especifique a localização de exportação de Olá na nuvem de origem Olá e a localização de importação de Olá na nuvem de destino Olá. Quando ativar a proteção para uma máquina virtual, Olá disco de rígido virtual é copiada toohello especificado localização de exportação. Envie-o site de destino toohello e copie-a localização de importação de toohello. Olá sistema cópias Olá importado informações toohello máquinas de virtuais de réplica.
13. Selecione **eliminar a Máquina Virtual de réplica** toospecify Olá máquina virtual de réplica deve ser eliminado se deixa de proteger a máquina virtual de Olá selecionando Olá **elimine a proteção da máquina virtual de Olá**  opção no separador de máquinas virtuais de Olá das propriedades de nuvem Olá. Com esta definição ativada, quando desativar proteção Olá máquina é removida do Azure Site Recovery, as definições de recuperação de sites de Olá para a máquina virtual de Olá são removidas na consola do VMM Olá e réplica Olá é eliminada.

    ![Configurar definições de proteção](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Depois de guardar as definições de Olá uma tarefa será criada e pode ser monitorizada no Olá **tarefas** separador. Todos os servidores de anfitrião de Hyper-V no Olá nuvem de origem do VMM serão configurados para replicação. Definições de nuvem podem ser modificadas no Olá **configurar** separador. Se pretender que localização de destino de Olá toomodify ou a nuvem de destino tem de remover configuração da nuvem Olá e, em seguida, reconfigurar a nuvem de Olá.

### <a name="prepare-for-offline-initial-replication"></a>Preparar a replicação inicial offline
Terá de Olá toodo seguir tooprepare ações para a replicação inicial offline:

* No servidor de origem Olá, terá de especificar uma localização de caminho do qual Olá será realizada a exportação de dados. Atribua o controlo total para as permissões de NTFS e partilha toohello serviço do VMM no caminho de exportação de Olá. No servidor de destino Olá, vai especificar uma localização de caminho de importação de dados de Olá partir do qual irá ocorrer. Atribua Olá mesmas permissões neste caminho de importação.
* Se hello importar ou exportar caminho for partilhado, atribuir a associação de grupo de administrador, utilizador avançado, operador de impressão ou o operador de servidor para a conta de serviço do VMM Olá no computador remoto Olá que Olá partilhado está localizada.
* Se estiver a utilizar quaisquer anfitriões de tooadd Run As contas, no Olá importar e exportar caminhos, atribua a leitura e permissões de escrita toohello contas Run as no VMM.
* Olá, importar e Exportar partilhas não deve estar localizada em qualquer computador utilizado como um servidor de anfitrião do Hyper-V, porque a configuração de loopback não é suportada pelo Hyper-V.
* No Active Directory, em cada servidor de anfitrião do Hyper-V que contém máquinas virtuais que pretende tooprotect, ativar e configurar a delegação restrita tootrust Olá computadores remotos em que a importação de Olá e exportação caminhos estão localizados, da seguinte forma:
  1. No controlador de domínio Olá, abra **computadores e utilizadores do Active Directory**.
  2. Na árvore da consola de Olá clique **DomainName** > **computadores**.
  3. O nome do servidor de anfitrião de Hyper-V de Olá contexto > **propriedades**.
  4. No Olá **delegação** separador clique T**rust neste computador para os serviços de toospecified de delegação apenas**.
  5. Clique em **utilizar qualquer protocolo de autenticação**.
  6. Clique em **adicionar** > **utilizadores e computadores**.
  7. Nome do tipo Olá do computador de Olá que aloja o caminho de exportação de Olá > **OK**. Na lista de Olá de serviços disponíveis, mantenha premida a tecla CTRL de Olá e clique em **cifs** > **OK**. Repita para nome de Olá do computador de Olá nesse caminho de importação de Olá de anfitriões. Repita conforme necessário para servidores de anfitrião de Hyper-V adicionais.

## <a name="step-5-configure-network-mapping"></a>Passo 5: Configurar o mapeamento da rede
1. Na página de início rápido de Olá, clique em **mapear redes**.
2. Selecione o servidor VMM de origem Olá partir do qual pretende toomap redes e, em seguida, Olá destino VMM toowhich hello do servidor serão mapeadas redes. lista de Olá de redes de origem e as respetivas redes de destino associada são apresentadas. É apresentado um valor em branco para as redes que atualmente não estão mapeadas.
3. Selecione uma rede no **rede na origem** > **mapa**. serviço de Olá Deteta redes VM Olá no servidor de destino Olá e apresenta-os. Clique em Olá informações ícone seguintes toohello origem e destino nomes tooview Olá sub-redes da rede para cada rede.

    ![Configurar o mapeamento da rede](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. Na caixa de diálogo Olá Selecione uma das redes VM Olá Olá VMM do servidor de destino.

    ![Selecione uma rede de destino](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Quando seleciona uma rede de destino, hello nuvens protegidas que utilizam a rede de origem Olá são apresentadas. Redes de destino disponíveis que estão associados às nuvens Olá utilizadas para proteção são também apresentados. Recomendamos que selecione uma rede de destino que esteja disponível tooall nuvens de Olá que estiver a utilizar para proteção. Ou, também pode ir toohello servidor VMM e modificar Olá nuvem propriedades tooadd Olá rede lógica correspondente toohello rede de vm que pretende que o toochoose.
6. Clique em processo de mapeamento do Olá marca de verificação toocomplete Olá. Progresso do mapeamento tootrack Olá é iniciada uma tarefa. Pode vê-la no Olá **tarefas** separador.

## <a name="step-6-configure-storage-mapping"></a>Passo 6: Configurar o mapeamento de armazenamento
Por predefinição quando replicar uma máquina virtual num Hyper-V anfitrião servidor tooa destino Hyper-V anfitrião servidor de origem, dados replicados são guardados na localização predefinida Olá indicado para o anfitrião de Hyper-V de destino Olá no Gestor de Hyper-V. Para obter mais controlo sobre onde os dados replicados são guardados, pode configurar os mapeamentos de armazenamento da seguinte forma:

1. Definir as classificações de armazenamento em ambos os origem Olá e servidores do VMM de destino. [Saiba mais](https://technet.microsoft.com/library/gg610685.aspx). Classificações tem de ser toohello disponíveis servidores de anfitrião de Hyper-V em nuvens de origem e de destino. Não precisam de classificações toohave Olá mesmo tipo de armazenamento. Por exemplo, pode mapear uma classificação de origem que contém a classificação destino de tooa de partilhas SMB que contém CSV.
2. Depois de classificações estão em vigor pode criar mapeamentos. toodo isto, na Olá **início rápido** página > **mapear armazenamento**.
3. Clique em Olá **armazenamento** separador > **mapeie as classificações de armazenamento**.
4. No Olá **mapeie as classificações de armazenamento** separador, selecione de classificações na origem de Olá e servidores do VMM de destino. Guarde as suas definições.

    ![Selecione uma rede de destino](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Passo 7: Ativar a proteção da máquina virtual
Depois de servidores, nuvens e redes estão configuradas corretamente, pode ativar a proteção para máquinas virtuais na nuvem de Olá.

1. No Olá **máquinas virtuais** separador na nuvem de Olá no qual Olá está localizada a máquina virtual, clique em **ativar a proteção** > **Adicionar máquinas virtuais**.
2. Na lista de Olá de máquinas virtuais na nuvem de Olá, selecione Olá um pretende tooprotect.

    ![Ativar a proteção da máquina virtual](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Controlar o progresso de Olá ação ativar proteção em Olá **tarefas** separador, incluindo a replicação inicial Olá. Após a tarefa finalizar proteção de Olá executa Olá máquina está preparada para ativação pós-falha. Depois de ativar a proteção e máquinas virtuais são replicadas, será capaz de tooview-las no Azure.

    ![Tarefa de proteção da máquina virtual](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> Também pode ativar a proteção para máquinas virtuais na consola do VMM Olá. Clique em **ativar proteção** na barra de ferramentas de Olá no Olá **do Azure Site Recovery** separador Propriedades da máquina virtual Olá.
>
>

### <a name="on-board-existing-virtual-machines"></a>Uma máquinas virtuais existentes
Se tiver máquinas virtuais existentes no VMM que estiver a replicar com a réplica do Hyper-V terá tooonboard-las para proteção do Azure Site Recovery da seguinte forma:

1. Certifique-se de que tem nuvens primárias e secundárias. Certifique-se de que o servidor Olá Hyper-V que aloja a máquina virtual existente e Olá está localizado na nuvem principal Olá e esse servidor de Hyper-V Olá Olá máquina virtual de réplica de alojamento está localizado na nuvem secundário Olá. Certifique-se de que configurou as definições de proteção de nuvens Olá. definições de Olá devem corresponder ao que os atualmente configurado para réplica do Hyper-V. Caso contrário, replicação da máquina virtual poderá não funcionar conforme esperado.
2. Em seguida, ative a proteção para a máquina virtual primária de Olá. Azure Site Recovery e o VMM irão garantir que hello mesmo anfitrião de réplica e a máquina virtual é detetada e do Azure Site Recovery irá reutilizar e restabelecer a replicação utilizando as definições de Olá configuradas durante a configuração da nuvem.

## <a name="test-your-deployment"></a>Testar a implementação
Planear a sua implementação, pode executar uma ativação pós-falha de teste para uma única máquina virtual ou criar um plano de recuperação consiste em várias máquinas virtuais e executar uma ativação pós-falha de teste para Olá tootest.  A ativação pós-falha de teste simula o mecanismo de ativação pós-falha e recuperação numa rede isolada.

### <a name="create-a-recovery-plan"></a>Criar um plano de recuperação
1. No Olá **planos de recuperação** separador, clique em **criar plano de recuperação**.
2. Especifique um nome para o plano de recuperação Olá e servidores do VMM de origem e de destino. servidor de origem Olá tem de ter as máquinas virtuais que estão ativadas para ativação pós-falha e recuperação. Selecione **Hyper-V** tooview apenas nuvens configuradas para a replicação de Hyper-V.

    ![Criar plano de recuperação](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. No **selecionar a Máquina Virtual**, selecione os grupos de replicação. Todas as máquinas virtuais associadas ao grupo de replicação de Olá com serão selecionadas e adicionados toohello plano de recuperação. Estas máquinas virtuais são adicionadas toohello grupo de predefinido do plano de recuperação – grupo 1. Pode adicionar mais grupos, se necessário. Tenha em atenção que, depois de máquinas virtuais de replicação, irá iniciar a cópia de segurança em conformidade com a ordem de Olá dos grupos de plano de recuperação Olá.

    ![Adicionar máquinas virtuais](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Depois de um plano de recuperação foi criado, aparece na lista de Olá no Olá **planos de recuperação** separador.

### <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste
1. No Olá **planos de recuperação** separador, selecione o plano de Olá e clique em **ativação pós-falha de teste**.
2. No Olá **confirmar ativação pós-falha de teste** página, selecione **nenhum**. Tenha em atenção que, com esta opção Olá ativado pós-falha de máquinas virtuais de réplica será ligada tooany rede. Isto irá testar que Olá falha de máquina virtual mais conforme esperado, mas não testar o seu ambiente de rede de replicação. Observe como demasiado[executar uma ativação pós-falha de teste](site-recovery-failover.md) para obter mais detalhes sobre como as opções de redes diferentes toouse.
3. será criada no mesmo anfitrião como anfitrião Olá existe da máquina virtual de réplica no qual Olá de Olá Olá máquina virtual de teste. É adicionado toohello mesma nuvem em que Olá máquina virtual de réplica se encontra.

### <a name="run-a-recovery-plan"></a>Executar um plano de recuperação
Depois de máquina de virtual de réplica de Olá de replicação pode não ter um endereço IP que é Olá igual ao endereço IP Olá Olá máquina virtual primária. Máquinas virtuais irá atualizar o servidor DNS de Olá que estão a utilizar após são iniciados. Também pode adicionar um script tooupdate Olá servidor DNS tooensure uma atualização atempadamente.

#### <a name="script-tooretrieve-hello-ip-address"></a>Endereço IP do script tooretrieve Olá
Execute este endereço IP Olá de tooretrieve de script de exemplo.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Script tooupdate DNS
Execute este tooupdate de script de exemplo DNS, especificar o endereço IP Olá obtido com script de exemplo Olá anterior.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Informações de privacidade para a recuperação de sites
Esta secção fornece informações sobre a privacidade adicionais Olá serviço Microsoft Azure Site Recovery ("serviço"). declaração de privacidade de Olá tooview para serviços do Microsoft Azure, consulte o [declaração de privacidade do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=324899)

**Funcionalidade: registo**

* **O que faz**: regista o servidor com o serviço de modo a que podem ser protegidas máquinas virtuais
* **As informações recolhidas**: depois de registar Olá serviço recolhe, processa e transmite informações de certificado de gestão hello do servidor do VMM que designou tooprovide recuperação de desastre com o nome do serviço hello do servidor do VMM Olá, e o nome de Olá das nuvens de máquina virtual no servidor do VMM.
* **Utilização de informações**:

  * Certificado de gestão — isto é utilizado toohelp identificar e autenticar o servidor do VMM Olá registado para acesso toohello serviço. Olá serviço utiliza Olá pública parte da chave Olá certificado toosecure registado um token que apenas Olá servidor do VMM pode ter acesso a. servidor de Olá tem toouse esta funcionalidades do serviço de token toogain acesso toohello.
  * Nome do servidor do VMM Olá – nome do servidor VMM Olá é necessário tooidentify e comunicar com o servidor VMM adequado Olá em que Olá nuvens estão localizadas.
  * Nomes hello do servidor do VMM de nuvem – nome da nuvem Olá é necessário quando utilizar a nuvem de serviço Olá funcionalidade emparelhamento/desemparelhamento descrita abaixo. Quando decidir toopair sua nuvem de centro de dados primária com outra nuvem no Centro de dados de recuperação Olá, Olá os nomes de todas as nuvens de Olá do Centro de dados de recuperação Olá são apresentados.
* **Escolha**: estas informações são uma parte essencial dos Olá processo de registo do serviço porque ajuda a e Olá serviço tooidentify Olá servidor do VMM para o qual pretende proteção do Azure Site Recovery tooprovide, bem como tooidentify Olá servidor VMM registado correto. Se não quiser toosend este toohello informações Service, não utilize este serviço. Se registar o servidor e, em seguida, posteriormente, pretender toounregister, pode fazê-ao eliminar informações de servidor do VMM Olá Olá portal do serviço (o que é Olá portal do Azure).

**Funcionalidade: Ativar a proteção do Azure Site Recovery**

* **O que faz**: Olá fornecedor do Azure Site Recovery instalado no servidor do VMM Olá é conduit Olá para comunicar com Olá serviço. Olá fornecedor é uma biblioteca de ligação dinâmica (DLL) alojada no processo VMM Olá. Após Olá que fornecedor está instalado, a funcionalidade de "Recuperação de centros de dados" Olá obtém ativada na consola de administrador do VMM Olá. Quaisquer máquinas virtuais novas ou existentes numa nuvem pode ativar uma propriedade denominada "Recuperação de centros de dados" toohelp proteger a máquina virtual de Olá. Assim que esta propriedade for definida, Olá fornecedor envia o nome de Olá e o ID de máquina virtual de Olá toohello serviço. proteção virtual Olá está ativada por tecnologia de replicação do Windows Server 2012 ou Windows Server 2012 R2 Hyper-V. dados da máquina virtual Olá obtém replicados a partir de um tooanother de anfitrião de Hyper-V (normalmente localizado no Centro de dados diferentes "recuperação de").
* **As informações recolhidas**: Olá serviço recolhe, processa e transmite os metadados para a máquina virtual Olá, que inclui o nome de Olá, ID, rede virtual e Olá nome da nuvem Olá a que pertence.
* **Utilização de informações**: Olá serviço utiliza Olá acima informações da máquina virtual informações toopopulate Olá no seu portal de serviço.
* **Escolha**: Esta é uma parte essencial do serviço de Olá e não pode ser desativada. Se não pretender que estas informações enviadas toohello Service, não conseguir ative a proteção do Azure Site Recovery para quaisquer máquinas virtuais. Tenha em atenção de que todos os dados enviados por Olá fornecedor toohello serviço são enviadas através de HTTPS.

**Funcionalidade: Plano de recuperação**

* **O que faz**: esta funcionalidade ajuda-o a toobuild um plano de orquestração de centro de dados de "recuperação de" Olá. Pode definir a ordem de Olá no qual Olá deverão ser iniciado no site de recuperação Olá máquinas virtuais ou um grupo de máquinas virtuais. Também pode especificar qualquer toobe scripts automatizados, executar ou toobe qualquer ação manual captado, de momento Olá de recuperação para cada máquina virtual. Ativação pós-falha (abrangido na secção seguinte, Olá), normalmente, é acionada no Olá ao nível do plano de recuperação para a recuperação coordenada.
* **As informações recolhidas**: Olá serviço recolhe, processa e transmite os metadados para o plano de recuperação Olá, incluindo os metadados da máquina virtual e metadados de quaisquer scripts de automatização e notas da ação manual.
* **Utilização de informações**: metadados Olá descrito acima são o plano de recuperação de Olá toobuild utilizadas no portal do serviço.
* **Escolha**: Esta é uma parte essencial do serviço de Olá e não pode ser desativada. Se não pretender que estas informações enviadas toohello Service, não crie planos de recuperação neste serviço.

**Funcionalidade: Mapeamento da rede**

* **O que faz**: esta funcionalidade permite-lhe toomap informações de rede do Centro de dados de recuperação center toohello Olá dados primários. Quando as máquinas virtuais de Olá são recuperadas no site de recuperação Olá, desta mapeamento ajuda a estabelecer conectividade de rede para os mesmos.
* **As informações recolhidas**: como parte da funcionalidade de mapeamento de rede de Olá, Olá serviço recolhe, processa e transmite Olá metadados de redes lógicas do Olá para cada site (primário e datacenter).
* **Utilização de informações**: Olá serviço utiliza Olá metadados toopopulate seu portal de serviço onde pode mapear informações da rede Olá.
* **Escolha**: Esta é uma parte essencial dos Olá serviço e não pode ser desativada. Se não pretender que estas informações enviadas toohello Service, não utilize a funcionalidade de mapeamento de rede Olá.

**Funcionalidade: A ativação pós-falha - teste planeada, não planeada**

* **O que faz**: esta funcionalidade ajuda a ativação pós-falha de uma máquina virtual de um centro de dados de gerida do VMM do tooanother de centro de dados geridos pelo VMM. ação de ativação pós-falha de Olá é acionada por utilizador Olá no seu portal de serviço. Razões possíveis para uma ativação pós-falha incluem um evento não planeado (por exemplo, no caso de Olá de um disaster0 natural; um evento planeado (por exemplo Centro de dados de balanceamento de carga); uma ativação pós-falha de teste (por exemplo um rehearsal de plano de recuperação).

Olá fornecedor no servidor do VMM Olá obtém notificado de evento Olá Olá serviço e executa uma ação de ativação pós-falha no anfitrião de Hyper-V Olá através de interfaces VMM. Ativação pós-falha real de Olá excluir máquina virtual de um tooanother de anfitrião de Hyper-V (normalmente em execução num centro de dados diferentes "recuperação de") é processada pelo tecnologia de replicação do Windows Server 2012 ou Windows Server 2012 R2 Hyper-V Olá. Após a conclusão da ativação pós-falha de Olá, Olá fornecedor instalada no servidor do VMM Olá do Centro de dados de "recuperação de" Olá envia Olá êxito informações toohello serviço.

* **As informações recolhidas**: Olá serviço utiliza Olá acima informações toopopulate Olá Estado informações de ação de ativação pós-falha de Olá no seu portal de serviço.
* **Utilização de informações**: Olá serviço utiliza Olá acima informações da seguinte forma:

  * Certificado de gestão — isto é utilizado toohelp identificar e autenticar o servidor do VMM Olá registado para acesso toohello serviço. Olá serviço utiliza Olá pública parte da chave Olá certificado toosecure registado um token que apenas Olá servidor do VMM pode ter acesso a. servidor de Olá tem toouse esta funcionalidades do serviço de token toogain acesso toohello.
  * Nome do servidor do VMM Olá – nome do servidor VMM Olá é necessário tooidentify e comunicar com o servidor VMM adequado Olá em que Olá nuvens estão localizadas.
  * Nomes hello do servidor do VMM de nuvem – nome da nuvem Olá é necessário quando utilizar a nuvem de serviço Olá funcionalidade emparelhamento/desemparelhamento descrita abaixo. Quando decidir toopair sua nuvem de centro de dados primária com outra nuvem no Centro de dados de recuperação Olá, Olá os nomes de todas as nuvens de Olá do Centro de dados de recuperação Olá são apresentados.
* **Escolha**: Esta é uma parte essencial do serviço de Olá e não pode ser desativada. Se não pretender que estas informações enviadas toohello Service, não utilize este serviço.

## <a name="next-steps"></a>Passos seguintes
Após executar um toocheck de ativação pós-falha de teste ambiente está a funcionar conforme esperado, [Saiba mais sobre](site-recovery-failover.md) diferentes tipos de ativações pós-falha.
