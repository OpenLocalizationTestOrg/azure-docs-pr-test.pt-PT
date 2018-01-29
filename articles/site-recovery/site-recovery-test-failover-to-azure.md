---
title: "Testar a ativação pós-falha para o Azure Site Recovery | Microsoft Docs"
description: "Saiba mais sobre como executar uma ativação pós-falha de teste no local para o Azure"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 10/16/2017
ms.author: pratshar
ms.openlocfilehash: a4555b1cc758e2d4bdd11a16776dc3bb209adee8
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/23/2018
---
# <a name="test--failover-to-azure-in-site-recovery"></a>Ativação pós-falha de teste para o Azure no Site Recovery



Este artigo descreve como executar um exercício de recuperação após desastre para o Azure, utilizando uma ativação pós-falha de teste de recuperação de sites.  

Execute uma ativação pós-falha de teste para validar a replicação e a estratégia de recuperação após desastre sem qualquer perda de dados ou o período de indisponibilidade. Uma ativação pós-falha de teste não tem impacto replicação em curso ou o seu ambiente de produção. Pode executar uma ativação pós-falha de teste a uma máquina virtual específica (VM) ou com um [plano de recuperação](site-recovery-create-recovery-plans.md) que contém várias VMs. 


## <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste
Este procedimento descreve como executar uma ativação pós-falha de teste para um plano de recuperação. 

![Ativação pós-falha de teste](./media/site-recovery-test-failover-to-azure/TestFailover.png)


1. No Site Recovery no portal do Azure, clique em **planos de recuperação** > *recoveryplan_name* > **ativação pós-falha de teste**.
2. Selecione um **ponto de recuperação** ao qual pretende efetuar a ativação pós-falha. Pode utilizar uma das seguintes opções:
    - **Mais recentes processados**: esta opção a ativação pós-falha todas as VMs no plano do ponto de recuperação mais recente, processados pelo Site Recovery. Para ver a para uma VM específica de pontos de recuperação mais recente, consulte **pontos de recuperação mais recente** nas definições de VM. Esta opção fornece um RTO baixa (objetivo de tempo de recuperação), porque nenhum tempo é gasto a processar dados não processados.
    - **Mais recente consistentes da aplicação**: esta opção a ativação pós-falha todas as VMs no plano para o ponto mais recente recuperação consistentes com aplicações processado pela recuperação de sites. Para ver a para uma VM específica de pontos de recuperação mais recente, consulte **pontos de recuperação mais recente** nas definições de VM. 
    - **Mais recente**: esta opção primeiro processa todos os dados que foi enviados para o serviço de recuperação de sites, criar um ponto de recuperação para cada VM antes de falhar ao longo ao mesmo. Esta opção fornece o RPO mais baixo (objetivo de ponto de recuperação), uma vez que a VM criadas após ativação pós-falha terá de todos os dados replicados no Site Recovery quando a ativação pós-falha foi acionada.
    - **Mais recente várias VMS processados**: esta opção está disponível para planos de recuperação com uma ou mais VMs que têm a consistência multi VM ativada. As VMs com a definição ativada com a ativação pós-falha do ponto de recuperação consistente de várias VMS mais recente. Outras VMs com a ativação pós-falha do ponto de recuperação de processamento mais recente.  
    - **Mais recente várias VMS consistentes da aplicação**: esta opção está disponível para planos de recuperação com uma ou mais VMs que têm a consistência multi VM ativada. As VMs que fazem parte de um grupo de replicação de ativação pós-falha para o ponto de recuperação consistentes com aplicações de várias VMS mais recente. Outras VMs com a ativação pós-falha para o respetivo ponto de recuperação consistentes com aplicações mais recente. 
    - **Personalizada**: Utilize esta opção para efetuar a ativação pós-falha de uma VM específica para um ponto de recuperação específico.
3. Selecione uma Azure virtual network na qual será criado as VMs de teste.

    - Tentativas de recuperação de site para criar teste VMs numa sub-rede com o mesmo nome e o mesmo endereço IP que foi fornecido no **computação e rede** definições da VM.
    - Se uma sub-rede com o mesmo nome não está disponível na rede virtual do Azure utilizada para a ativação pós-falha de teste, em seguida, o teste de VM é criada na primeira sub-rede por ordem alfabética.
    - Se o mesmo endereço IP não está disponível na sub-rede, VM recebe outro endereço IP disponível na sub-rede. [Saiba mais](#creating-a-network-for-test-failover).
4. Se estiver a efetuar a ativação pós-falha para o Azure e a encriptação de dados estiver ativada, no **chave de encriptação**, selecione o certificado que foi emitido quando ativada, encriptação durante a instalação do fornecedor. Pode ignorar este passo de encriptação não está ativada.
5. Controlar o progresso de ativação pós-falha no **tarefas** separador. Deve conseguir ver a máquina de réplica de teste no portal do Azure.
6. Para iniciar uma ligação de RDP para a VM do Azure, terá de [adicionar um endereço IP público](site-recovery-monitoring-and-troubleshooting.md) na interface de rede de ativação pós-falha VM. 
7. Quando tudo está a funcionar conforme esperado, clique em **ativação pós-falha de teste de limpeza**. Isto elimina as VMs que foram criadas durante a ativação pós-falha de teste.
8. No **notas**, registar e guardar todas as observações associadas à ativação pós-falha de teste. 


![Ativação pós-falha de teste](./media/site-recovery-test-failover-to-azure/TestFailoverJob.png)

Quando é acionada uma ativação pós-falha de teste, ocorre o seguinte:

1. **Pré-requisitos**: verificação de um pré-requisitos é executado para se certificar de que todas as condições necessárias para a ativação pós-falha são cumpridas.
2. **Ativação pós-falha**: A ativação pós-falha processa e preparar os dados, para que uma VM do Azure podem ser criada a partir do mesmo.
3. **Mais recente**: Se tiver escolhido o último ponto de recuperação, é criado um ponto de recuperação de dados foi enviada para o serviço.
4. **Iniciar**: este passo cria uma máquina virtual do Azure com os dados processados no passo anterior.

### <a name="failover-timing"></a>Temporização da ativação pós-falha

Nos seguintes cenários, ativação pós-falha requer um passo intermédio extra que normalmente demora cerca de 8 a 10 minutos a concluir:

* Executar uma versão do serviço de mobilidade anterior 9.8 de VMs de VMware
* Servidores físicos
* VMware Linux VMs
* VM do Hyper-V protegida como servidores físicos
* VM de VMware, onde os seguintes controladores não são controladores de arranque:
    * storvsc
    * VMBus
    * storflt
    * intelide
    * ATAPI
* VM do VMware que não tenham DHCP activado, rrespective de se estão a utilizar DHCP ou endereços IP estáticos.

Em todos os outros casos, não é necessário nenhum passo intermédio e ativação pós-falha demora significativamente menos tempo.


## <a name="create-a-network-for-test-failover"></a>Criar uma rede para a ativação pós-falha de teste

Recomendamos que ativação pós-falha de teste, escolha uma rede que está isolada da rede do site de recuperação de produção específica no **computação e rede** definições para cada VM. Por predefinição, quando criar uma Azure virtual network, está isolada de outras redes. A rede de teste deve imitar a sua rede de produção:

- A rede de teste deve ter o mesmo número de sub-redes que a sua rede de produção. Sub-redes devem ter os mesmos nomes.
- A rede de teste deve utilizar o mesmo rangek de endereço IP.
- Atualizar o DNS da rede de teste com o endereço IP especificado para a VM com DNS **computação e rede** definições. Leitura [considerações de ativação pós-falha do Active Directory](site-recovery-active-directory.md#test-failover-considerations) para obter mais detalhes.


## <a name="test-failover-to-a-production-network-in-the-recovery-site"></a>Ativação pós-falha de teste para uma rede de produção no site de recuperação

Embora, recomendamos que utilize uma rede de teste separada da sua rede de produção, se pretender testar um exercício de recuperação após desastre na sua rede de produção, tenha em atenção o seguinte: 

- Certifique-se de que a VM principal é encerrada ao executar a ativação pós-falha de teste. Não existe Otherewise será duas VMs com a mesma identidade, em execução na mesma rede, ao mesmo tempo. Isto pode levar a consequências inesperadas.
- As alterações às VMs criadas para ativação pós-falha de teste serão perdidas quando limpar a ativação pós-falha. Estas alterações não são replicadas para a VM principal.
- Teste no seu ambiente de produção leva a um tempo de inatividade da sua aplicação de produção. Os utilizadores não devem utilizar as aplicações em execução em VMs quando a ativação pós-falha de teste está em curso.  



## <a name="prepare-active-directory-and-dns"></a>Preparar o Active Directory e DNS

Para executar uma ativação pós-falha de teste para a aplicação de teste, terá de uma cópia do seu ambiente do Active Directory de produção no seu ambiente de teste. Leitura [considerações de ativação pós-falha do Active Directory](site-recovery-active-directory.md#test-failover-considerations) para obter mais informações.

## <a name="prepare-to-connect-to-azure-vms-after-failover"></a>Preparar a ligação para VMs do Azure após a ativação pós-falha

Se pretende ligar as VMs do Azure com RDP após a ativação pós-falha, siga os requisitos resumidos na tabela.

**Ativação pós-falha** | **Localização** | **Ações**
--- | --- | ---
**VM do Azure com o Windows** | Máquina no local antes da ativação pós-falha | Para aceder à VM do Azure através da internet, ative o RDP e certifique-se de que as regras TCP e UDP estão adicionadas para **pública**, e que o RDP é permitido para todos os perfis de **Firewall do Windows**  >  **Aplicações permitidas**.<br/><br/> Para aceder à VM do Azure através de uma ligação site a site, ative o RDP na máquina e certifique-se de que o RDP é permitido no **Firewall do Windows** -> **aplicações e funcionalidades permitidas**, para **Domínio e privada** redes.<br/><br/>  Certifique-se de que o sistema operativo de política de SAN está definido como **OnlineAll**. [Saiba mais](https://support.microsoft.com/kb/3031135).<br/><br/> Certifique-se de que existem não existem atualizações pendentes do Windows na VM quando acione uma ativação pós-falha. Poderá iniciar a atualização do Windows quando efetuar a ativação pós-falha e não poderá iniciar sessão no VM até a conclusão da atualização. 
**VM do Azure com o Windows** | VM do Azure após a ativação pós-falha |  [Adicionar um endereço IP público](site-recovery-monitoring-and-troubleshooting.md) para a VM.<br/><br/> As regras de grupo de segurança de rede em ativação pós-falha VM (e na sub-rede Azure à qual está ligado) necessário permitir ligações de entrada à porta RDP.<br/><br/> Verifique **diagnóstico de arranque** para verificar uma captura de ecrã da VM.<br/><br/> Se não conseguir ligar, verifique que a VM está em execução e reveja estes [sugestões de resolução de problemas](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).
**VM do Azure a executar Linux** | Máquina no local antes da ativação pós-falha | Certifique-se de que o serviço de Secure Shell na VM está definido para iniciar automaticamente no arranque do sistema.<br/><br/> Verifique se as regras de firewall permitem uma ligação SSH ao mesmo.
**VM do Azure a executar Linux** | VM do Azure após a ativação pós-falha | As regras de grupo de segurança de rede em ativação pós-falha VM (e na sub-rede Azure à qual está ligado) necessário permitir ligações de entrada na porta SSH.<br/><br/> [Adicionar um endereço IP público](site-recovery-monitoring-and-troubleshooting.md) para a VM.<br/><br/> Verifique **diagnóstico de arranque** para uma captura de ecrã da VM.<br/><br/>



## <a name="next-steps"></a>Passos Seguintes
Depois de concluir um exercício de recuperação após desastre, saiba mais sobre outros tipos de [ativação pós-falha](site-recovery-failover.md).
