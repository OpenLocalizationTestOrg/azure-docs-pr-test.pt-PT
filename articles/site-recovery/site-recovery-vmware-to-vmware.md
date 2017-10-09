---
title: "aaaReplicate VMs de VMware ou servidores físicos num tooanother site (portal clássico do Azure) | Microsoft Docs"
description: "Utilize este artigo tooreplicate VMs de VMware ou Windows/Linux servidores físicos tooa site secundário com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: jwhit
editor: 
ms.assetid: b2cba944-d3b4-473c-8d97-9945c7eabf63
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 5789ca07f0aa15cf194615fd33103dac930d7b7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-on-premises-vmware-virtual-machines-or-physical-servers-tooa-secondary-site-in-hello-classic-azure-portal"></a>Replicar máquinas virtuais VMware no local ou servidores físicos tooa num site secundário no portal clássico do Azure Olá

## <a name="overview"></a>Descrição geral
InMage Scout no Azure Site Recovery fornece em tempo real replicação entre sites do VMware no local. InMage Scout está incluído no subscrições de serviços do Azure Site Recovery. 

## <a name="prerequisites"></a>Pré-requisitos
**Conta do Azure**: irá precisar de um [Microsoft Azure](https://azure.microsoft.com/) conta. Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). [Saiba mais](https://azure.microsoft.com/pricing/details/site-recovery/) sobre os preços da Recuperação de Sites.

## <a name="step-1-create-a-vault"></a>Passo 1: Criar um cofre
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em Novo > gestão > cópia de segurança e recuperação de sites (OMS). Em alternativa, pode clicar em Procurar > cofre dos serviços de recuperação > Adicionar.
3. No **nome** especificar um cofre de Olá tooidentify nome amigável. Se tiver mais do que uma subscrição, selecione uma delas.
4. No **grupo de recursos** criar um novo grupo de recursos ou selecione um existente. Especifique os campos de toocomplete necessário uma região do Azure.
5. No **localização**, selecione Olá região geográfica do Cofre de Olá. regiões toocheck suportado, consulte [preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Se pretender que o tooquickly acesso Olá cofre a partir de Olá Dashboard clique toodashboard de Pin e, em seguida, clique em criar.
7. Step-by-Olá novo cofre é apresentado no Olá Dashboard > todos os recursos, e em Olá principal recuperação cofres dos serviços de painel.

## <a name="step-2-configure-hello-vault-and-download-inmage-scout-components"></a>Passo 2: Configurar o Cofre de Olá e transferir os componentes de InMage Scout
1. No painel de cofres dos serviços de recuperação de Olá seleciona o Cofre e clique em definições.
2. No **definições** > **introdução** clique **recuperação de Site** > Passo 1: **preparar infraestrutura**  >  **Objetivo de proteção**.
3. No **objetivo de proteção** selecione toorecovery site e selecionar Sim, com o VMware vSphere hipervisor. Em seguida, clique em OK.
4. No **configuração Scout**, clique em transferir de chave de software e o registo de toodownload InMage Scout 8.0.1 GA. ficheiros de configuração de Olá para todos os Olá necessários componentes estão no ficheiro. zip transferido de Olá.

## <a name="step-3-install-component-updates"></a>Passo 3: Instalar atualizações de componentes
Leia sobre Olá mais recente [atualizações](#updates). Irá instalar os ficheiros de atualização de Olá em servidores no Olá seguinte ordem:

1. Servidor RX se existir um
2. Servidores de configuração
3. Servidores de processos
4. Servidores de destino mestre
5. servidores de vContinuum
6. Servidor de origem (o Windows e o servidor Linux)

Instale atualizações de Olá da seguinte forma:

1. Transferir Olá [atualizar](https://aka.ms/asr-scout-update5) ficheiro. zip. Este ficheiro. zip contém Olá os seguintes ficheiros:

   * RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.GZ
   * CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe
   * UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe
   * UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
   * vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe
   * Bits de update4 UA para RHEL5, OL5, OL6, SUSE 10, SUSE 11: UA_<Linux OS>_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz
2. Extraia os ficheiros. zip de Olá.<br>
3. **Para o servidor de RX Olá**: cópia **RX_8.0.4.0_GA_Update_4_8725872_16Sep16.tar.gz** servidor de RX toohello e extraia. Olá extraiu pasta, execute **/instalar**.<br>
4. **Para o servidor de processo do servidor de configuração de Olá**: cópia **CX_Windows_8.0.4.0_GA_Update_4_8725865_14Sep16.exe** toohello servidor de configuração e o servidor de processos. Faça duplo clique em toorun-lo.<br>
5. **Para o servidor de destino principal do Windows hello**: Olá tooupdate unified agente, cópia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello servidor de destino mestre. Faça duplo clique toorun-lo. Tenha em atenção que Olá unificada agente também seja servidor de origem de toohello aplicável se a origem não for atualizada até Update4. Deve instalá-lo no servidor de origem Olá bem, tal como mencionado mais tarde nesta lista.<br>
6. **Para o servidor vContinuum de Olá**: cópia **vCon_Windows_8.0.5.0_GA_Update_5_11525767_20Apr17.exe** toohello vContinuum servidor.  Certifique-se de que tiver fechado o Assistente de vContinuum Olá. Faça duplo clique no Olá toorun de ficheiro.<br>
7. **Para o servidor de destino principal do Linux Olá**: Olá tooupdate unified agente, cópia **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello principal do servidor de destino e extraiu-lo. Olá extraiu pasta, execute **/instalar**.<br>
8. **Para o servidor de origem do Windows hello**: não é necessário tooinstall 5 de atualização de agente na origem se IDs já se encontra no update4. Se for inferior a update4, aplique o agente de atualização 5 Olá.
Olá tooupdate unified agente, cópia **UA_Windows_8.0.5.0_GA_Update_5_11525802_20Apr17.exe** toohello servidor de origem. Faça duplo clique toorun-lo. <br>
9. **Para o servidor de origem do Linux Olá**: tooupdate Olá unificada de agente, versão correspondente UA toohello Linux do servidor de ficheiros de copiar e extrai-lo. Olá extraiu pasta, execute **/instalar**.  Exemplo: Para o servidor do RHEL 6.7 64 bits, copie **UA_RHEL6 64_8.0.4.0_GA_Update_4_9035261_26Sep16.tar.gz** toohello servidor e extraia. Olá extraiu pasta, execute **/instalar**.

## <a name="step-4-set-up-replication"></a>Passo 4: Configurar a replicação
1. Configure a replicação entre a origem de Olá e de destino VMware sites.
2. Para obter orientações, utilize Olá documentação de InMage Scout que é transferida com o produto Olá. Em alternativa, pode aceder a Olá documentação da seguinte forma:

   * [Notas de versão](https://aka.ms/asr-scout-release-notes)
   * [Matriz de compatibilidade](https://aka.ms/asr-scout-cm)
   * [Guia do utilizador](https://aka.ms/asr-scout-user-guide)
   * [Guia do utilizador RX](https://aka.ms/asr-scout-rx-user-guide)
   * [Guia de instalação rápida](https://aka.ms/asr-scout-quick-install-guide)

## <a name="updates"></a>Atualizações
### <a name="azure-site-recovery-scout-801-update-5"></a>Do Azure Site Recovery Scout 8.0.1 atualização 5
Atualização Scout 5 é uma atualização cumulativa. Tem todos os Olá correções de atualização1 até update4 e seguir novo correções de erros e melhoramentos.
Correções que são adicionadas a partir de ASR Scout update4 tooupdate5 são componentes de destino e vContinuum tooMaster específico. Se todos os seus servidores de origem, destino principal, o servidor de configuração, o servidor de processos e o RX já estão no ASR Scout update4, em seguida, é necessário tooapply atualizar 5 apenas no servidor de destino mestre. 

**Novo suporte de plataforma**
* SUSE Linux Enterprise Server 11 4(SP4) do Service Pack

> [!NOTE]
> SLES 11 SP4 64 bits **InMage_UA_8.0.1.0_SLES11-SP4-64_GA_13Apr2017_release.tar.gz** é compactada com o pacote do base Scout GA **InMage_Scout_Standard_8.0.1 GA.zip**. Transferir o pacote de Scout GA do portal como mencionado em [passo 1](#step-1-create-a-vault).
>

**Correções de erros e melhoramentos**

* Aumentar a fiabilidade do suporte de Cluster do Windows
    * Sometime corrigidos alguns dos Olá P2V MSCS tornar-se de discos de cluster RAW após a recuperação
    * A recuperação de cluster do MSCS de P2V Fixed-falha devido a erro de correspondência de ordem de toodisk
    * Cluster do Fixed-MSCS adicionar discos operação falha com erro de correspondência de tamanho de disco
    * Cluster do MSCS de origem do Fixed-com verificação de disponibilidade de mapeamento de RDM LUNs falha na verificação de tamanho
    * Proteção de cluster de nó único Fixed-falha devido tooSCSI problema de incompatibilidade 
    * Voltar a fixed-proteger do Olá P2V Windows cluster server falha se existirem discos de cluster de destino. 
    
* Durante a proteção de reativação pós-falha, se MT selecionado não se encontra no Olá mesmo servidor ESXi como que Olá protegido máquina de origem (durante a proteção direta), então vContinuum escolherá MT errado Olá durante a recuperação de reativação pós-falha e, subsequentemente, operação de recuperação falhará.

> [!NOTE]
> 
> * Acima correções do cluster de P2V é, por exemplo, esses cluster do MSCS físicos que estão protegidos raiz com o ASR Scout update5 tooonly aplicável. tooavail Olá cluster correções no Olá já protegidos cluster do MSCS de P2V com as atualizações mais antigas, terá de toofollow Olá passos de atualização que são mencionados na secção de Olá 12, atualização protegidos tooScout de cluster do P2V MSCS Update5 de [ASR Scout versão Notas](https://aka.ms/asr-scout-release-notes).
> 
> * Voltar a proteger de cluster do MSCS físico pode reutilizar existente discos de destino apenas se momento Olá da reativação da proteção, Olá mesmo conjunto de discos estão ativas em cada cluster Olá nós, tal como estavam quando inicialmente protegidos. Se não, em seguida, existem passos manuais tal como mencionado na secção 12 [notas de versão ASR Scout](https://aka.ms/asr-scout-release-notes) demasiado mover Olá destino lado discos toohello arquivo de dados correto caminho toore-utilização-los durante a reativação da proteção. Se Proteja o cluster do MSCS Olá no modo de P2V sem os seguintes passos de atualização, irá criar o novo disco no servidor de ESXi do destino de Olá. Precisa de discos antigos do toomanually eliminar Olá de Olá arquivo de dados.
> 
> * Sempre que a origem SLES11 ou SLES11 com qualquer servidor de pacote de serviço é reiniciado corretamente, em seguida, um deve marcar manualmente Olá **raiz** pares de replicação para sincronizar novamente de disco não será notificado na placa CX IU. Se não o ' marca Olá raiz disco para ressincronização, poderá ver os problemas de integridade (DI) de dados.
> 

### <a name="azure-site-recovery-scout-801-update-4"></a>Do Azure Site Recovery Scout 8.0.1 atualização 4
Scout atualização 4 é uma atualização cumulativa. Tem todos os Olá correções de atualização1 até update3 e seguir novo correções de erros e melhoramentos.

**Novo suporte de plataforma**

* Foi adicionado suporte para o vCenter/vSphere 6.0, 6.1 e 6.2
* Foi adicionado suporte para os seguintes sistemas operativos Linux
  * Red Hat Enterprise Linux (RHEL) 7.0, 7.1 e 7.2
  * CentOS 7.0, 7.1 e 7.2
  * Red Hat Enterprise Linux (RHEL) 6.8
  * CentOS 6.8

> [!NOTE]
> RHEL/CentOS 7 64 bits **InMage_UA_8.0.1.0_RHEL7-64_GA_06Oct2016_release.tar.gz** é compactada com o pacote do base Scout GA **InMage_Scout_Standard_8.0.1 GA.zip**. Transferir o pacote de Scout GA do portal como mencionado em [passo 1](#step-1-create-a-vault).
>
>

**Correções de erros e melhoramentos**

* Encerramento melhorado processamento para seguintes sos de Linux e clones tooprevent problemas indesejáveis sincronizar novamente.
  * Red Hat Enterprise Linux (RHEL) 6. x
  * Oracle Linux (OL) 6. x
* Para Linux, acesso de pasta completos as permissões no diretório de instalação do agente unificada são agora restringido a apenas toohello utilizador local.
* No Windows exceder o tempo limite problema ao emitir marca de livro distribuída consistência comum nos descontos elevados carregar aplicações distribuídas, como clusters SQL e SharePoint.
* Registo adicionado relacionados com a correção no instalador base CX.
* Ligação de transferência do VMware vCLI 6.0 é adicionada tooWindows instalador de base de destino mestre.
* Adicionar mais verificações e os registos para alterações de configurações de rede durante a ativação pós-falha e aprofunda de DR.
* Informações de retenção sometime não são reportado toohello CX.  
* Para um cluster físico, volume tamanho novamente a operação através do Assistente de vContinuum está a falhar quando foi efetuada a operação de encolhimento de volume de origem.
* Cluster de proteção falhou com o erro "Falha toofind Olá disco a assinatura" quando o disco de cluster é disco PRDM.
* Falha do servidor de transporte cxps devido à exceção de fora do intervalo.
* Nome do servidor e colunas IP estão agora redimensionáveis na página de instalação push do Assistente de vContinuum.
* Melhoramentos de API RX
  * Fornece cinco mais recente disponível comuns consistência pontos (apenas garantida etiquetas).
  * Fornece detalhes de espaço livre e capacidade para todos os Olá dispositivos protegidos.
  * Fornece o estado do controlador de Scout no servidor de origem.

> [!NOTE]
> * **InMage_Scout_Standard_8.0.1_GA.zip** pacote base agora atualizou instalador base CX **InMage_CX_8.0.1.0_Windows_GA_26Feb2015_release.exe** e o programa de instalação base do destino principal de Windows **InMage_ Scout_vContinuum_MT_8.0.1.0_Windows_GA_26Feb2015_release.exe**. Para todos os nova instalação utilize o bits de GA CX e de destino principal do Windows novo.
> * Atualização 4 pode ser aplicada diretamente em 8.0.1 depois da disponibilidade geral
> * servidor de configuração de Olá e RX atualizações não é possível revertidas após a que está a ser aplicadas no sistema de Olá.
>
>

### <a name="azure-site-recovery-scout-801-update-3"></a>Do Azure Site Recovery Scout 8.0.1 Update 3
A atualização 3 inclui seguinte Olá correções de erros e melhoramentos:

* servidor de configuração de Olá e RX falhar o Cofre de recuperação de sites do tooregister toohello quando forem atrás proxy Olá.
* Olá número de horas que Olá objetivo de ponto de recuperação (RPO) não for cumprido não é obter atualizadas no relatório de estado de funcionamento de Olá.
* servidor de configuração de Olá não estiver a sincronizar com RX quando detalhes de hardware do ESX Olá ou detalhes da rede contém caracteres UTF-8.
* Os controladores de domínio do Windows Server 2008 R2 falharem tooboot após a recuperação.
* Sincronização offline não está a funcionar conforme esperado.
* Após a ativação pós-falha de máquina virtual (VM), a eliminação do par de replicação obtém bloqueada no Olá CX IU durante muito tempo e os utilizadores não é possível concluir a reativação pós-falha da Olá ou retomar a operação.
* Em geral as operações de instantâneo terminadas pela tarefa de consistência Olá foram otimizadas toohelp reduzir aplicação desliga como os clientes de SQL.
* desempenho de Olá da ferramenta de consistência Olá (VACP.exe) foi melhorado, reduzindo a utilização de memória de Olá que é necessária para a criação de instantâneos no Windows.
* a instalação de emissão de Olá falhas do serviço quando a palavra-passe de Olá é superior a 16 carateres.
* vContinuum não está a verificar e pedir para novas credenciais do vCenter quando as credenciais de Olá forem alteradas.
* No Linux, Gestor de cache de destino mestre Olá (cachemgr) não está a transferir ficheiros do servidor de processos Olá, o que resulta em limitação do par de replicação.
* Quando a ordem de disco de cluster (MSCS) de ativação pós-falha física Olá é não Olá igual em todos os nós de Olá, a replicação não está definida para algumas Olá volumes de cluster.
  <br/>Tenha em atenção de que esse cluster Olá tem toobe proteger tootake partido Esta correção.  
* Funcionalidade de SMTP não está a funcionar conforme esperado após RX é atualizado a partir do Scout 7.1 tooScout 8.0.1.
* Foram adicionadas estatísticas mais no registo de Olá por Olá reversão operação tootrack Olá período de tempo demorou toocomplete-lo.
* Foi adicionado suporte para sistemas de operativos Linux no servidor de origem Olá:
  * Atualização do Red Hat Enterprise Linux (RHEL) 6 7
  * 7 de atualização do centOS 6
* Olá CX e RX IU agora podem mostrar notificação Olá par Olá, que entra no modo de mapa de bits.
* Olá seguintes correções de segurança foram adicionadas no RX:

| **Descrição do problema** | **Procedimentos de implementação** |
| --- | --- |
| Ignorar a autorização através do parâmetro de adulteração |Utilizadores toonon aplicável acesso restrito. |
| Falsificação de pedidos entre sites |Conceito página token de Olá implementado, que gera aleatoriamente para todas as páginas. <br/>Com esta opção, verá: <li> É apenas uma único início de sessão instância para Olá mesmo utilizador.</li><li>Atualização de página não funciona – irá redirecionar toohello dashboard.</li> |
| Carregamento de ficheiros maliciosos |Extensões de toocertain ficheiros restrito. Permitidos extensões são: 7z, aiff, asf, avi, bmp, csv, documento, docx, fla, flv, gif, gz, gzip, jpeg, jpg, registo, mid mov, mp3, mp4, mpc, mpeg, mpg, ods, odt, pdf, png, ppt, pptx, pxd, qt, ram, rar, rm, rmi, rmvb, rtf, sdc, sitd, swf, sxc, sxw, tar , tgz, tif, tiff, txt, vsd, wav, wma, wmv, xls, xlsx, xml e zip. |
| Persistente de scripts entre sites |Adicionar validações de entrada. |

> [!NOTE]
> * Todas as atualizações de recuperação de Site são cumulativas. A atualização 3 tem todas as correções Olá de atualização 1 e 2 de atualização. A atualização 3 pode ser aplicada diretamente em 8.0.1 depois da disponibilidade geral
> * servidor de configuração de Olá e RX atualizações não é possível revertidas após a que está a ser aplicadas no sistema de Olá.
>
>

### <a name="azure-site-recovery-scout-801-update-2-update-03dec15"></a>Do Azure Site Recovery Scout 8.0.1 atualização 2 (atualização 03 15 de Dec)
Correções Update 2 incluem:

* **Servidor de configuração**: corrigir um problema que impediu o funcionalidade de medição Olá 31 dias gratuita funcionar conforme esperado ao hello o servidor de configuração foi registado no Site Recovery.
* **Agente unificada**: corrigir um problema no Update 1 que resultaram numa atualização Olá não a ser instalada no servidor de destino mestre Olá quando este tiver sido atualizado de too8.0.1 versão 8.0.

### <a name="azure-site-recovery-scout-801-update-1"></a>Do Azure Site Recovery Scout 8.0.1 atualização 1
A atualização 1 inclui seguinte Olá correções e novas funcionalidades:

* 31 dias de proteção livre por instância de servidor. Isto permite-lhe funcionalidades tootest ou configurar um prova de conceito.
  * Todas as operações no servidor de Olá, incluindo a ativação pós-falha e a reativação pós-falha, são gratuitas para Olá primeiro 31 dias, começando pelo tempo de Olá que um servidor primeiro está protegido com Scout de recuperação de Site.
  * De Olá 32nd dia em diante, cada servidor protegido será cobrado a taxa de instância padrão Olá para o site de propriedade de cliente do Azure Site Recovery proteção tooa.
  * Em qualquer altura, número de Olá dos servidores protegidos que estão atualmente a ser cobrados está disponível na página do Dashboard de Olá do cofre do Azure Site Recovery Olá.
* Adicionado suporte para vSphere Interface de linha de comandos (vCLI) 5.5 atualização 2.
* Adicionado suporte para sistemas de operativos Linux no servidor de origem Olá:
  * RHEL 6 Update 6
  * RHEL 5 atualizar 11
  * Atualização 6 do centOS 6
  * Atualização do centOS 5 11
* Correções de erros Olá de tooaddress os seguintes problemas:
  * Falha do registo do cofre para o servidor de configuração de Olá ou servidor RX.
  * Volumes de cluster não aparecem conforme esperado quando máquinas virtuais em cluster são proteger quando estes retomar.
  * Reativação pós-falha falha quando o servidor de destino mestre Olá é alojado num servidor diferente ESXi provenientes de máquinas de virtuais de produção do Olá no local.
  * Permissões de ficheiro de configuração são alteradas ao atualizar too8.0.1, que afeta a proteção e as operações.
  * limiar de ressincronização Olá não é imposta conforme esperado, que servem como tooinconsistent comportamento de replicação.
  * definições de RPO Olá não são apresentados corretamente no interface de servidor de configuração de Olá. o valor de dados de Olá descomprimido incorretamente, mostra o valor de Olá comprimido.
  * operação de remoção de Olá não elimina conforme esperado no Assistente de vContinuum Olá e replicação não é eliminada da interface de servidor de configuração de Olá.
  * No Assistente de vContinuum Olá, disco de Olá é automaticamente não seleccionado quando clicar em **detalhes** na vista de disco Olá durante a proteção de máquinas de virtuais MSCS.
  * Durante o cenário de (P2V) físico-virtual Olá, os serviços de HP necessários, como CIMnotify e CqMgHost, não são movida toomanual na recuperação da máquina virtual. Isto resulta num tempo de arranque adicionais.
  * Proteção de máquinas virtuais do Linux falha quando existirem mais de 26 discos no servidor de destino mestre Olá.

## <a name="next-steps"></a>Passos seguintes
Após alguma questão que tem na Olá [fórum do Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).
