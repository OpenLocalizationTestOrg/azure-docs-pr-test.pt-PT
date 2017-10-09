---
title: aaaReplicate VMs de Hyper-V no VMM com o SAN utilizando o Azure Site Recovery | Microsoft Docs
description: "Este artigo descreve como máquinas de virtuais tooreplicate Hyper-V entre dois sites com o Azure Site Recovery utilizando a replicação SAN."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>Replicar VMs de Hyper-V no site secundário do VMM nuvens tooa com o Azure Site Recovery utilizando SAN


Utilize este artigo se quiser toodeploy [do Azure Site Recovery](site-recovery-overview.md) toomanage replicação de VMs de Hyper-V (geridas em nuvens do System Center Virtual Machine Manager) tooa site secundário do VMM, utilizando o Azure Site Recovery no portal clássico Olá. Este cenário não está disponível no novo portal do Azure Olá.



Publique quaisquer comentários no fim de Olá deste artigo. Obtenha respostas a perguntas de tootechnical no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>Por que razão a replicar com SAN e a recuperação de sites?

* SAN fornece uma solução de replicação de nível empresarial, dimensionável para que um site primário que contém o Hyper-V com SAN pode replicar LUNs tooa site secundário com SAN. Armazenamento é gerido pelo VMM e a replicação e ativação pós-falha é orquestradas com a recuperação de Site.
* Recuperação de site trabalhou com vários [parceiros de armazenamento de SAN](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) tooprovide replicação entre o armazenamento de canal de fibra e o iSCSI.  
* Utilize SAN infraestrutura tooprotect fundamentais às aplicações existentes implementadas em clusters de Hyper-V. As VMs podem ser replicadas como um grupo para que as aplicações de N camadas podem ser a ativação pós-falha consistentemente.
* Replicação SAN garante a consistência da replicação em toda a diferentes camadas de uma aplicação com a replicação sincronizada para baixa RTO e RPO e asynchronized replicação flexibilidade elevada (consoante as suas capacidades da matriz de armazenamento).  
* Pode gerir o armazenamento de SAN no Olá recursos de infraestrutura do VMM e utilizar SMI-S no armazenamento existente do VMM toodiscover.  

Tenha em atenção que:
- Replicação de site a site com SAN não está disponível no Olá portal do Azure. Só está disponível no portal clássico Olá. Não não possível criar novos cofres no portal clássico Olá. Podem ser mantidas cofres existentes.
- Replicação de SAN tooAzure não é suportada.
- Não é possível replicar VHDXs partilhados ou unidades lógicas (LUN) que estão diretamente ligados tooVMs através de iSCSI ou canal de fibra. Clusters convidados podem ser replicadas.


## <a name="architecture"></a>Arquitetura

![Arquitetura de SAN](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: configurar um cofre de recuperação de sites no Olá portal do Azure.
- **Armazenamento SAN**: armazenamento de SAN é gerido no Olá recursos de infraestrutura do VMM. Adicione o fornecedor de armazenamento Olá, criar classificações de armazenamento e configurar agrupamentos de armazenamento.
- **O VMM e o Hyper-V**: recomenda-se um servidor do VMM em cada site. Configurar nuvens privadas do VMM e coloque clusters Hyper-V nessas nuvens. Durante a implementação, Olá fornecedor do Azure Site Recovery está instalado em cada servidor VMM e o servidor de Olá está registado no Cofre de Olá. Olá fornecedor comunica com a replicação de toomanage de serviço de recuperação de Site Olá, a ativação pós-falha e a reativação pós-falha.
- **Replicação**: depois de configurar o armazenamento no VMM e configurar a replicação na recuperação de Site, ocorre a replicação entre o armazenamento de SAN de Olá primário e secundário. Não existem dados de replicação são enviados tooSite recuperação.
- **Ativação pós-falha**: Ativar a ativação pós-falha no portal de recuperação de Site Olá. Não há perda de dados durante a ativação pós-falha porque a replicação está síncrona.
- **Reativação pós-falha**: toofail back, ativar a replicação inversa tootransfer delta alterações relativamente ao site primário do Olá site secundário toohello. Depois de concluída a replicação inversa, execute uma ativação pós-falha planeada do tooprimary secundário. Esta ativação pós-falha planeada para réplica Olá VMs no site secundário Olá e inicia-los no site primário Olá.


## <a name="before-you-start"></a>Antes de começar


**Pré-requisitos** | **Detalhes**
--- | ---
**Azure** |Necessita de uma conta do [Microsoft Azure](https://azure.microsoft.com/). Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Sites. Crie um tooconfigure de cofre do Azure Site Recovery e gerir a replicação e ativação pós-falha.
**VMM** | Pode utilizar um único servidor do VMM e replicar entre nuvens diferentes, mas recomendamos um VMM no site primário Olá e um no site secundário Olá. Um VMM pode ser implementado como um servidor autónomo físico ou virtual ou como um cluster. <br/><br/>servidor do VMM Olá deve ser executar o System Center 2012 R2 ou posterior com Olá mais recentes atualizações cumulativas.<br/><br/> Precisa de, pelo menos, uma nuvem configurada no servidor VMM principal Olá pretender tooprotect e uma nuvem configurada no servidor do VMM secundário Olá pretende toouse para ativação pós-falha.<br/><br/> nuvem de origem Olá tem de conter um ou mais grupos de anfitriões do VMM.<br/><br/> Todas as nuvens do VMM devem ter o conjunto de perfis de capacidade Hyper-V Olá.<br/><br/> Para obter mais informações sobre como configurar as nuvens do VMM, consulte [implementam uma nuvem privada da VM](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Hyper-V** | Precisa de um ou mais clusters Hyper-V em nuvens VMM primárias e secundárias.<br/><br/> cluster de Hyper-V de origem Olá tem de conter uma ou mais VMs.<br/><br/> grupos de anfitriões VMM Olá em sites primários e secundários do Olá tem de conter, pelo menos, um Olá clusters de Hyper-V.<br/><br/>servidores de Hyper-V do anfitrião e o destino Olá devem executar o Windows Server 2012 ou posterior com Hyper-V de Olá função e Olá mais recentes atualizações instaladas.<br/><br/> Se estiver a executar o Hyper-V num cluster e tem um cluster de baseadas no endereço IP estático, o Mediador de clusters não é criado automaticamente. Deve configurá-la manualmente. Para obter mais informações, consulte [preparar clusters de anfitriões para réplica do Hyper-V](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters).
**Armazenamento SAN** | Pode replicar máquinas de virtuais em cluster convidado com armazenamento de iSCSI ou canal ou ao utilizar discos rígidos virtuais (vhdx) partilhados.<br/><br/> Tem duas matrizes SAN: um no site primário Olá e o site secundário Olá num.<br/><br/> Uma infraestrutura de rede deve ser configurada entre as matrizes de Olá. Replicação e de peering devem ser configurados. Licenças de replicação devem ser configuradas em conformidade com os requisitos de matriz de armazenamento Olá.<br/><br/>Configure a rede entre servidores de anfitrião Olá Hyper-V e a matriz de armazenamento de Olá, para que os anfitriões podem comunicar com o LUN de armazenamento, utilizando Isci ou canal de fibra.<br/><br/> Verifique [matrizes de armazenamento suportadas](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> Fornecedores de SMI-S fabricantes de matriz de armazenamento devem ser instalados e matrizes SAN de Olá devem ser geridas pelo fornecedor de Olá. Configure Olá fornecedor de acordo com toomanufacturer as instruções.<br/><br/>Certifique-se de fornecedor de SMI-S da matriz que Olá num servidor que Olá VMM server possa aceder através de rede de Olá com um endereço IP ou FQDN.<br/><br/> Cada matriz SAN deve ter um ou mais agrupamentos de armazenamento disponível.<br/><br/> servidor VMM principal do Olá deve gerir matriz primário Olá e servidor do VMM secundário Olá deve gerir matriz secundário Olá.
**Mapeamento da rede** | Configure o mapeamento da rede para que as máquinas virtuais replicadas ideal são colocadas em servidores de anfitrião de Hyper-V secundários após a ativação pós-falha e para que o se estiver a redes VM tooappropriate ligado. Se não configurar o mapeamento da rede, as VMs de réplica será ligada tooany rede após a ativação pós-falha.<br/><br/> Certifique-se de que redes do VMM estão configuradas corretamente para que pode configurar o mapeamento da rede durante a implementação da recuperação de Site. No VMM, Olá VMs no anfitrião de Hyper-V de origem Olá deve ser ligado tooa rede VM do VMM. Essa rede deve ser ligado tooa rede lógica que esteja associado Olá nuvem.<br/><br/> nuvem de destino Olá deve ter uma rede VM correspondente e, por sua vez deve ser ligado tooa correspondente rede lógica que está associado a nuvem de destino Olá.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>Passo 1: Preparar a infraestrutura do VMM de Olá
tooprepare da infraestrutura do VMM, tem de:

1. Certifique-se as nuvens do VMM.
2. Integrar e classificar o armazenamento de SAN no VMM.
3. Crie LUNs e atribuir armazenamento.
4. Crie grupos de replicação.
5. Configure as redes VM.

### <a name="verify-vmm-clouds"></a>Certifique-se de nuvens do VMM

Certifique-se que a nuvens do VMM estão configuradas corretamente antes de começar a implementação da recuperação de Site.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Integrar e classificar o armazenamento de SAN no Olá recursos de infraestrutura do VMM

1. Na consola do VMM Olá, vá demasiado**recursos de infraestrutura** > **armazenamento** > **adicionar recursos** > **dedispositivosdearmazenamento**.
2. No Olá **adicionar dispositivos de armazenamento** assistente, selecione **selecione um tipo de fornecedor de armazenamento** e selecione **SAN e dispositivos NAS detetados e geridos por um fornecedor SMI-S**.

    ![Tipo de fornecedor](./media/site-recovery-vmm-san/provider-type.png)

3. No Olá **especificar protocolo e o endereço do fornecedor de SMI-S de armazenamento de Olá** página, selecione **SMI-S CIMXML** e especifique as definições de Olá para ligação toohello fornecedor.
4. No **ou FQDN do endereço IP de fornecedor** e **porta TCP/IP**, especifique as definições de Olá para ligação toohello fornecedor. Pode utilizar uma ligação SSL apenas para CIMXML SMI-S.

    ![Fornecedor de ligar](./media/site-recovery-vmm-san/connect-settings.png)
5. No **conta Run as**, especifique uma conta Run As do VMM que pode aceder ao fornecedor de Olá ou criar uma conta.
6. No Olá **recolher informações** página, o VMM tenta automaticamente toodiscover e importar informações de dispositivo de armazenamento Olá. Deteção de tooretry, clique em **pesquisar fornecedor**. Se o processo de deteção de Olá for bem sucedida, Olá detetados matrizes de armazenamento, agrupamentos de armazenamento, fabricante, modelo e capacidade são listadas na página Olá.

    ![Detetar o armazenamento](./media/site-recovery-vmm-san/discover.png)
7. No **selecione tooplace de agrupamentos de armazenamento sob gestão e atribuir uma classificação**, selecione Olá agrupamentos de armazenamento que o VMM irá gerir e atribuir-lhes uma classificação. As informações de LUN é importadas dos agrupamentos de armazenamento Olá. Crie LUNs com base nas aplicações Olá precisa tooprotect, os respetivos requisitos de capacidade e os requisitos para que precisa de tooreplicate em conjunto.

    ![Classificar o armazenamento](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>Criar LUN e atribuir armazenamento

Crie LUNs com base nas aplicações Olá precisa tooprotect, os requisitos de capacidade e os requisitos para que precisa de tooreplicate em conjunto.

1. Depois do armazenamento de Olá aparece no Olá recursos de infraestrutura do VMM, pode [aprovisionar LUNs](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > Não adicione VHDs para Olá VM que estão ativadas para replicação tooLUNs. Se esses LUNs não estão num grupo de replicação de recuperação de sites, não será possível detetar pela recuperação de sites.
     >

2. Atribua o cluster de anfitriões de Hyper-V de toohello de capacidade de armazenamento para que o VMM pode implementar o armazenamento da máquina virtual dados toohello aprovisionado:

   * Antes da cluster toohello de armazenamento, terá de tooallocate este grupo de anfitriões VMM toohello no qual Olá cluster reside. Para obter mais informações, consulte [como o grupo no VMM de anfitriões de tooa de unidades lógicas de armazenamento tooallocate](https://technet.microsoft.com/library/gg610686.aspx) e [como o grupo de anfitriões tooa no VMM de agrupamentos de armazenamento de tooallocate](https://technet.microsoft.com/library/gg610635.aspx).
   * Alocar o cluster de toohello de capacidade de armazenamento conforme descrito em [como cluster de armazenamento tooconfigure num anfitrião Hyper-V no VMM](https://technet.microsoft.com/library/gg610692.aspx).

    ![Tipo de fornecedor](./media/site-recovery-vmm-san/provider-type.png)
3. No **especificar protocolo e o endereço do fornecedor de SMI-S de armazenamento de Olá**, selecione **SMI-S CIMXML**. Especificar definições de Olá para estabelecer a ligação de fornecedor toohello. Pode utilizar uma ligação SSL apenas para CIMXML SMI-S.

    ![Fornecedor de ligar](./media/site-recovery-vmm-san/connect-settings.png)
4. No **conta Run as**, especifique uma conta Run As do VMM que pode aceder ao fornecedor de Olá ou criar uma conta.
5. No **recolher informações**, o VMM tenta automaticamente toodiscover e importar informações de dispositivo de armazenamento Olá. Se precisar de tooretry, clique em **pesquisar fornecedor**. Quando o processo de deteção de Olá for bem sucedida, matrizes de armazenamento Olá, agrupamentos de armazenamento, o fabricante, o modelo e capacidade são listadas na página Olá.

    ![Detetar o armazenamento](./media/site-recovery-vmm-san/discover.png)
7. No **selecione tooplace de agrupamentos de armazenamento sob gestão e atribuir uma classificação**, selecione os agrupamentos de armazenamento de Olá VMM irá gerir e atribuir-lhes uma classificação. As informações de LUN é importadas dos agrupamentos de armazenamento Olá.

    ![Classificar o armazenamento](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Criar grupos de replicação

Crie um grupo de replicação que inclui todos os LUNs de Olá terão tooreplicate em conjunto.

1. Na consola do VMM de Olá, abra Olá **grupos de replicação** separador de propriedades de matriz de armazenamento Olá e, em seguida, clique em **novo**.
2. Crie grupo de replicação de Olá.

    ![Grupo de replicação SAN](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Configure as redes

Se pretender que o mapeamento da rede tooconfigure, Olá a seguir:

1. Consulte o mapeamento da rede de recuperação de sites.
2. Prepare as redes VM no VMM:

   * [Configure as redes lógicas](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [Configure as redes VM](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>Passo 2: Criar um cofre

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) hello do servidor do VMM pretende tooregister no Cofre de Olá.
2. Expanda **serviços de dados** > **dos serviços de recuperação**e, em seguida, clique em **Cofre de recuperação de Site**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. No **nome**, introduza um cofre de Olá tooidentify nome amigável.
5. No **região**, selecione Olá região geográfica do Cofre de Olá. regiões toocheck suportado, consulte [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Clique em **Criar cofre**.

    ![Novo Cofre](./media/site-recovery-vmm-san/create-vault.png)

Verifique tooconfirm de barra de estado de Olá Olá cofre foi criado com êxito. Olá cofre será listado como **Active Directory** no Olá principal **dos serviços de recuperação** página.

### <a name="register-hello-vmm-servers"></a>Registar os servidores do VMM de Olá

1. Abra Olá **início rápido** página de Olá **dos serviços de recuperação** página. Início rápido também pode ser aberto em qualquer altura, selecionando o ícone de Olá.

    ![Ícone de Início Rápido](./media/site-recovery-vmm-san/quick-start-icon.png)
2. Na caixa de lista pendente de Olá, selecione **entre Hyper-V no local utilizando a replicação de matriz de site**.

    ![Chave de registo](./media/site-recovery-vmm-san/select-san.png)
3. No **preparar servidores VMM**, transferir Olá a versão mais recente do ficheiro de instalação do fornecedor do Azure Site Recovery Olá.
4. Execute este ficheiro no servidor de origem Olá do VMM. Se o VMM for implementado num cluster e estiver a instalar Olá fornecedor para Olá pela primeira vez, instale Olá fornecedor num nó ativo e concluir o servidor do Olá instalação tooregister Olá VMM no Cofre de Olá. Em seguida, instale Olá fornecedor no Olá outros nós. Se estiver a atualizar Olá fornecedor, terá de tooupgrade em todos os nós, para que possam ter Olá a mesma versão do fornecedor.
5. Instalador de Olá verifica os requisitos e pedidos permissão toostop Olá a configuração do fornecedor de toobegin de serviço do VMM. serviço de Olá será reiniciado automaticamente após a conclusão do programa de configuração. Num VMM cluster, irá ser função de Cluster de Olá toostop pedido.
6. No **Microsoft Update**, pode optar pelas atualizações e as atualizações do fornecedor serão instaladas de acordo com política do Microsoft Update tooyour.

    ![Atualizações da Microsoft](./media/site-recovery-vmm-san/ms-update.png)

7. Por predefinição, é a localização de instalação de Olá para Olá fornecedor <SystemDrive>\Programas\Microsoft System Center 2012 R2\Virtual Machine Manager\bin. Clique em **instalar** toobegin.

    ![Localização de instalação](./media/site-recovery-vmm-san/install-location.png)

8. Depois de Olá fornecedor está instalado, clique em **registar** tooregister Olá servidor do VMM no Cofre de Olá.

    ![Instalação completa](./media/site-recovery-vmm-san/install-complete.png)

9. No **ligação à Internet**, especifique como Olá fornecedor se liga toohello Internet. Selecione **utilizar definições de proxy do sistema predefinidas** se quiser toouse Olá Internet predefinições de ligação no servidor de Olá.

    ![Definições da Internet](./media/site-recovery-vmm-san/proxy-details.png)

   * Se quiser toouse um proxy personalizado, configurá-lo antes de instalar Olá fornecedor. Quando configurar as definições de proxy personalizado, um teste é executado a ligação de proxy de Olá toocheck.
   * Se utilizar um proxy personalizado, ou se o proxy predefinido exigir autenticação, deverá introduzir os detalhes do proxy Olá, incluindo endereço de Olá e a porta.
   * Olá necessários que URLs devem estar acessíveis hello do servidor do VMM.
   * Se utilizar um proxy personalizado, uma conta Run As do VMM (DRAProxyAccount) é criada automaticamente utilizando Olá especificada credenciais de proxy. Configure o servidor de proxy de Olá, para que esta conta pode autenticar. Pode modificar Olá Run as definições da conta na consola do VMM Olá (**definições** > **segurança** > **contas Run as**  >  **DRAProxyAccount**). Tem de reiniciar o serviço do VMM Olá para Olá alteração tootake produza efeitos.
10. No **chave de registo**, selecione chave Olá que transferiu Olá toohello portal e copiado do servidor do VMM.
11. No **nome do cofre**, verifique o nome de Olá do Cofre de Olá no qual Olá servidor será registado.

    ![Registo do servidor](./media/site-recovery-vmm-san/vault-creds.png)
12. definição de encriptação de Olá só é utilizada para replicação de tooAzure do VMM. Pode ignorá-lo.

    ![Registo do servidor](./media/site-recovery-vmm-san/encrypt.png)
13. No **nome do servidor**, especifique o servidor de nome amigável tooidentify Olá VMM no Cofre de Olá. Numa configuração de cluster, especifique o nome de função de cluster do Olá VMM.
14. No **sincronização de metadados de nuvem inicial**, selecione se pretende toosynchronize metadados para todas as nuvens no servidor do VMM Olá. Esta ação só deverá toohappen uma vez em cada servidor. Se não quiser toosynchronize todas as nuvens, pode deixar esta definição desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem de Olá na consola do VMM Olá.

    ![Registo do servidor](./media/site-recovery-vmm-san/friendly-name.png)

15. Clique em **seguinte** processo de Olá toocomplete. Após o registo, os metadados hello do servidor do VMM são obtidos pelo Azure Site Recovery. Olá servidor é apresentado na **servidores** > **servidores VMM** no Cofre de Olá.

### <a name="command-line-installation"></a>Instalação da linha de comandos

Olá fornecedor do Azure Site Recovery também pode ser instalado utilizando Olá seguinte linha de comandos. Este método pode ser fornecedor de Olá tooinstall utilizados no Server Core do Windows Server 2012 R2.

1. Transferir Olá fornecedor e o registo do ficheiro de chave tooa pasta de instalação. Por exemplo: C:\ASR.
2. Pare o serviço do VMM Olá.
3. Extraia o instalador de fornecedor Olá. Execute estes comandos como administrador:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instale Olá fornecedor:

        C:\ASR> setupdr.exe /i
5. Registe Olá fornecedor:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parâmetros:

* **/Credentials**: parâmetro necessário para a localização de Olá no qual Olá se encontra o ficheiro de chave de registo.  
* **/ FriendlyName**: parâmetro necessário para o nome de Olá Olá Hyper-V do servidor de anfitrião que é apresentado no portal do Azure Site Recovery Olá.
* **/ EncryptionEnabled**: o parâmetro opcional apenas utilizado quando replicar do tooAzure do VMM.
* **/proxyAddress**: o parâmetro opcional que especifica o endereço de hello do servidor de proxy de Olá.
* **/proxyaddress**: o parâmetro opcional que especifica a porta de hello do servidor de proxy de Olá.
* **/proxyUsername**: o parâmetro opcional que especifica o nome de utilizador de proxy Olá (caso o proxy de Olá requer autenticação).
* **/proxyPassword**: o parâmetro opcional que especifica Olá palavra-passe para autenticar com o servidor de proxy de Olá (se o proxy de Olá requer autenticação).

## <a name="step-3-map-storage-arrays-and-pools"></a>Passo 3: Mapear matrizes de armazenamento e agrupamentos

Mapear toospecify matrizes primárias e secundárias que conjunto de armazenamento secundário recebe dados de replicação agrupamento principal Olá. Mapear armazenamento antes de configurar a replicação, porque as informações de mapeamento de Olá são utilizadas quando ativar a proteção dos grupos de replicação.

Antes de começar, certifique-se de que são apresentadas as nuvens do VMM no Cofre de Olá. As nuvens são detetadas quando sincronizar todas as nuvens durante a instalação do fornecedor ou quando sincronizar uma nuvem específica na consola do VMM Olá.

1. Clique em **recursos** > **armazenamento de servidor** > **matrizes de destino e origem de mapa**.
    ![Registo do servidor](./media/site-recovery-vmm-san/storage-map.png)

2. Selecione matrizes de armazenamento Olá no site primário Olá e mapeá-los toostorage matrizes no site secundário Olá. No **agrupamentos de armazenamento**, selecione uma origem e destino toomap de agrupamento de armazenamento.

    ![Registo do servidor](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>Passo 4: Configurar as definições de replicação

Depois de estarem registados servidores do VMM, configure as definições de proteção de nuvem.

1. No Olá **início rápido** página, clique em **configurar a proteção de nuvens VMM**.
2. No Olá **itens protegidos** separador, selecione a nuvem de Olá **configuração**.
3. No **destino**, selecione **VMM**.
4. No **localização de destino**, selecione servidor do VMM Olá que gere nuvem Olá pretende toouse para recuperação.
5. No **nuvem de destino**, selecione a nuvem de destino Olá pretende toouse para ativação pós-falha da VM.
   * Recomendamos que selecione uma nuvem de destino cumpre os requisitos de recuperação para as máquinas virtuais de Olá que proteger.
   * Nuvem apenas pode pertencer a par de nuvem única tooa – como um site primário ou de uma nuvem de destino.
6. Recuperação de sites verifica se as nuvens têm acesso tooSAN armazenamento e que Olá matrizes são mapeadas.
7. Se a verificação for bem sucedida, no **tipo de replicação**, selecione **SAN**.

Depois de guardar as definições de Olá, é criada uma tarefa que pode ser monitorizada no Olá **tarefas** separador. As definições podem ser modificadas no Olá **configurar** separador. Se quiser localização de destino de Olá toomodify ou a nuvem de destino, tem de remover a configuração da nuvem Olá e, em seguida, reconfigurar a nuvem de Olá.

## <a name="step-5-enable-network-mapping"></a>Passo 5: Ativar o mapeamento da rede

1. No Olá **início rápido** página, clique em **mapear redes**.
2. Selecione o servidor do VMM de origem de Olá e, em seguida, selecione as hello de toowhich VMM de destino do Olá servidor redes serão mapeadas. lista de Olá de redes de origem e as respetivas redes de destino associada são apresentadas. É apresentado um valor em branco para as redes que não são mapeados. Clique em Olá informações ícone seguintes toohello origem e destino nomes tooview Olá sub-redes da rede para cada rede.
3. Selecione uma rede no **rede na origem**e, em seguida, clique em **mapa**. serviço de Olá Deteta redes VM Olá no servidor de destino Olá e apresenta-os.

    ![Arquitetura de SAN](./media/site-recovery-vmm-san/network-map1.png)
4. Selecione uma das redes VM Olá Olá VMM do servidor de destino.

    ![Arquitetura de SAN](./media/site-recovery-vmm-san/network-map2.png)

5. Quando seleciona uma rede de destino, hello nuvens protegidas que utilizam a rede de origem Olá são apresentadas. Redes de destino disponíveis também são apresentados. Recomendamos que selecione uma rede de destino que esteja disponível tooall nuvens de Olá que estiver a utilizar para replicação.
6. Clique em processo de mapeamento do Olá marca de verificação toocomplete Olá. É iniciada uma tarefa que controla o progresso. Pode vê-la no Olá **tarefas** separador.

## <a name="step-6-enable-replication-for-replication-groups"></a>Passo 6: Ativar a replicação dos grupos de replicação

Antes de poder ativar a proteção para máquinas virtuais, terá de replicação de tooenable para grupos de replicação de armazenamento.

1. No Olá **propriedades** página da nuvem principal do Olá no portal de recuperação de Site Olá, abra Olá **máquinas virtuais** separador e clique em **adicionar grupo de replicação**.
2. Selecionados um ou mais VMM grupos de replicação que estão associados a nuvem de Olá, certifique-se de matrizes de origem e destino Olá e especifique a frequência de replicação de Olá.

Recuperação de sites, VMM e fornecedores de SMI-S de Olá aprovisionar LUN de armazenamento de site de destino do Olá e ativar a replicação de armazenamento. Se o grupo de replicação de Olá já está a ser replicado, a recuperação de sites reutiliza a relação de replicação existente Olá e atualizações Olá informações.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Passo 7: Ativar a proteção para máquinas virtuais


Quando um grupo de armazenamento está a replicar, ative a proteção para VMs na consola do VMM Olá com um dos seguintes métodos de Olá:

* **Nova máquina virtual**: ao criar uma VM, ativar a replicação e associe o grupo de replicação de Olá Olá VM.
  Com esta opção, o VMM utiliza o armazenamento VM do posicionamento inteligente toooptimally local Olá nos LUNs Olá Olá do grupo de replicação. Recuperação de site orquestra a criação de uma VM no site secundário Olá de sombra Olá e atribui a capacidade para que as VMs da réplica podem ser iniciadas após a ativação pós-falha.
* **Máquina virtual existente**: se uma máquina virtual já está implementada no VMM, pode ativar a replicação e efetuar um grupo de replicação de tooa de migração de armazenamento. Após a conclusão, VMM e a recuperação de Site detetar Olá nova VM e começar a geri-la no Site Recovery. Uma sombra é criada a VM no site secundário Olá, e a capacidade é atribuída para que essa VM de réplica Olá possa ser iniciada após a ativação pós-falha.

![Ativar a proteção](./media/site-recovery-vmm-san/enable-protect.png)

Depois das VMs estão ativadas para replicação, estas aparecem na consola da recuperação de Site Olá. Pode ver as propriedades VM, controlar o estado e controlar os grupos de replicação de ativação pós-falha que contêm várias VMs. Na replicação de SAN, todas as VMs associadas um grupo de replicação devem efetuar a ativação pós-falha em conjunto. Isto acontece porque a ativação pós-falha ocorre na camada de armazenamento Olá primeiro. É importante toogroup a replicação de grupos corretamente e coloque apenas as VMs associadas em conjunto.

> [!NOTE]
> Depois de ativar a replicação para uma VM, não adicione o tooLUNs VHDs, a menos que estão localizados num grupo de replicação do Site Recovery. Os VHDs só serão detetados pela recuperação de sites se estão localizados num grupo de replicação do Site Recovery.
>
>

Pode controlar o progresso, incluindo a replicação inicial Olá, no Olá **tarefas** separador. Após a execução da tarefa de finalizar proteção Olá, Olá máquina está preparada para ativação pós-falha.

![Tarefa de proteção da máquina virtual](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>Passo 8: Testar a implementação de Olá

Teste a sua toomake de implementação, certificar-se de que as VMs falharem mais conforme esperado. toodo isto, crie um plano de recuperação e executar uma ativação pós-falha de teste.

1. No Olá **planos de recuperação** separador, clique em **criar plano de recuperação**.
2. Especifique um nome para o plano de recuperação Olá e selecione os servidores do VMM de origem e de destino. servidor de origem Olá tem de ter as VMs que estão ativadas para ativação pós-falha e recuperação. Selecione **SAN** tooview apenas nuvens configuradas para replicação SAN.

    ![Criar plano de recuperação](./media/site-recovery-vmm-san/r-plan.png)

3. No **selecionar Virtual Machines**, selecione os grupos de replicação. Todas as VMs associadas ao grupo de Olá com são adicionadas toohello plano de recuperação. Estas VMs são adicionadas toohello grupo de predefinido do plano de recuperação (grupo 1). Pode adicionar mais grupos, se necessário. Após a replicação, as VMs estão numeradas toohello ordem dos grupos de plano de recuperação Olá de acordo com.

    ![Selecione as máquinas virtuais](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Depois de criado o plano de recuperação Olá, é apresentado na lista de Olá no Olá **planos de recuperação** separador. Selecione o plano de Olá e escolha **ativação pós-falha de teste**.
5. No Olá **confirmar ativação pós-falha de teste** página, selecione **nenhum**. Com esta opção ativada, Olá pós-falha nas VMs de réplica será ligada tooany rede. Esta ação testa esse Olá VMs efetuar a ativação pós-falha conforme esperado, mas não testar o ambiente de rede Olá. Para mais informações sobre outras opções de rede, consulte [ativação pós-falha do Site Recovery](site-recovery-failover.md).

    ![Rede de teste selecione](./media/site-recovery-vmm-san/test-fail1.png)

6. VM de teste de Olá é criada no Olá mesmo anfitrião como anfitrião Olá na réplica que Olá VM existe. Esta não está adicionada nuvem toohello no qual Olá VM de réplica está localizado.
2. Após a replicação, a VM de réplica Olá terá um endereço IP diferente a máquina virtual primária de Olá. Se emitir endereços de DHCP, serão atualizado automaticamente. Se não estiver a utilizar o DHCP e quiser Olá mesmo endereços, terá de toorun alguns scripts.
3. Execute este endereço IP do script tooretrieve Olá:

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. Execute este tooupdate de script de exemplo DNS. Especifique o endereço IP Olá obtidos.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Passos seguintes

Após executar um toocheck de ativação pós-falha de teste que o seu ambiente está a funcionar conforme esperado, consulte [ativação pós-falha do Site Recovery](site-recovery-failover.md) toolearn sobre os diferentes tipos de ativações pós-falha.
