---
title: "aaaSet políticas de segurança no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda-o a tooconfigure políticas de segurança no Centro de segurança do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Definir políticas de segurança no Centro de Segurança do Azure
Este documento ajuda-o a tooconfigure políticas de segurança no Centro de segurança, ao servir pelos, através de Olá passos necessários tooperform esta tarefa.

>[!NOTE] 
>A partir da precoce de Junho de 2017, o Centro de segurança utiliza Olá Microsoft Monitoring Agent toocollect e arquivo de dados. Consulte [migração de plataforma de centro de segurança do Azure](security-center-platform-migration.md) toolearn mais. informações de Olá neste artigo representam a funcionalidade do Centro de segurança após a transição toohello Microsoft Monitoring Agent.
>

## <a name="what-are-security-policies"></a>O que são políticas de segurança?
Uma política de segurança define o conjunto de Olá de controlos, que são recomendados para recursos dentro Olá especificado subscrição. No Centro de segurança, é possível definir políticas para as suas subscrições do Azure, de acordo com as necessidades de segurança da empresa tooyour e tipo de Olá de aplicações ou sensibilidade dos dados de Olá em cada subscrição.

Por exemplo, os recursos que são utilizados para programação ou testes podem ter requisitos de segurança diferentes dos que são utilizados para aplicações de produção. Da mesma forma, as aplicações que utilizam dados regulados como informação identificativa podem exigir um nível mais elevado de segurança. Políticas de segurança estão ativadas em recomendações de segurança de unidade de centro de segurança do Azure e monitorização toohelp identificar potenciais vulnerabilidades e a mitigar ameaças. Leitura [guia de operações e planeamento do Centro de segurança do Azure](security-center-planning-and-operations-guide.md) para obter mais informações sobre como toodetermine Olá opção que são adequadas para si.

## <a name="set-security-policies"></a>Definir políticas de segurança
Pode configurar políticas de segurança para cada subscrição. toomodify uma política de segurança, tem de ser um proprietário ou contribuinte dessa subscrição. Inicie sessão toohello portal do Azure e siga Olá ter êxito políticas de segurança de tooconfigure no Centro de segurança de passos:

1. Clique em Olá **política** mosaico no dashboard do Centro de segurança de Olá.
2. No painel de política de segurança de Olá que se abre, selecione a subscrição de Olá no qual pretende que a política de segurança de Olá tooenable.

    ![Definir política](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Olá **política de segurança** abre painel para a subscrição de Olá selecionado com um conjunto de opções. Olá opções disponíveis neste painel são:

   * **Política de prevenção**: Utilize esta opção tooconfigure diferentes políticas por subscrição.  
   * **Notificação por e-mail**: Utilize esta opção tooconfigure uma notificação de correio eletrónico que é enviada no Olá primeiro diária ocorrência de um alerta e para os alertas de elevada gravidade. As preferências de e-mail só podem ser configuradas para as políticas de subscrição. Leitura [fornecer detalhes de contacto de segurança no Centro de segurança do Azure](security-center-provide-security-contact-details.md) para obter mais informações sobre como tooconfigure uma notificação por e-mail.
   * **Escalão de preço**: Utilize esta Olá de tooupgrade opção seleção do escalão de preço. Consulte [preços do Centro de segurança](security-center-pricing.md) toolearn mais sobre os preços de opções.
4. Certifique-se de que a opção **Recolher dados de máquinas virtuais** está **Ativada**. Esta opção permite a recolha de automática de registos de recursos existentes e novas utilizando Olá Microsoft Monitoring Agent – isto é Olá mesmo agente utilizado pelo serviço de Olá Operations Management Suite e análise de registos. Dados recolhidos a partir deste agente são armazenados um existente workspace(s) de análise de registos associados à subscrição do Azure ou um workspace(s) nova, tendo em conta Olá de geografia de Olá VM.

5. No Olá **política de segurança** painel, clique em **política de prevenção** toosee Olá opções disponíveis. Clique em **no** recomendações de segurança de Olá tooenable que são relevantes para esta subscrição.

    ![Selecionar as políticas de segurança de Olá](./media/security-center-policies/security-center-policies-fig7.png)

Utilize Olá como uma referência toounderstand a tabela seguinte cada opção:

| Política | Quando o estado está ativado |
| --- | --- |
| Atualizações do sistema |Obtém uma lista diária de atualizações críticas e de segurança disponíveis a partir do Windows Update ou o Windows Server Update Services. lista de obtidas Olá depende do serviço de Olá que esteja configurado para que a máquina virtual e recomenda que as atualizações em falta Olá sejam aplicadas. Para sistemas Linux, a política de Olá utiliza Olá pacote fornecidos pela distro gestão sistema toodetermine os pacotes com atualizações disponíveis. Também verifica se existem atualizações críticas e de segurança de máquinas virtuais dos [Serviços em Nuvem do Azure](../cloud-services/cloud-services-how-to-configure.md). |
| Vulnerabilidades do SO |Analisa o sistema operativo configurações diária toodetermine problemas que possam tornar Olá máquina virtual vulnerável tooattack. política de Olá recomenda também tooaddress de alterações de configuração, estas vulnerabilidades. Consulte Olá [lista de linhas de base recomendadas](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) para obter mais informações sobre as configurações específicas Olá que estão a ser monitorizados. (Neste momento, o Windows Server 2016 não é totalmente suportado.) |
| Endpoint protection |Recomenda endpoint protection toobe aprovisionada para todas as máquinas virtuais de Windows toohelp identificar e remover vírus, spyware e outro software malicioso. |
| Encriptação de disco |Recomenda a ativação da encriptação de disco em todas as máquinas virtuais de proteção de dados de tooenhance inativos. |
| Grupos de segurança de rede |Recomenda que [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md) ser toocontrol configurado entrada e saída de tráfego tooVMs com pontos finais públicos. Os grupos de segurança de rede configurados para uma sub-rede são herdados por todas as interfaces de rede de máquina virtual, exceto se for especificado em contrário. Além disso toochecking que foi configurado um grupo de segurança de rede, esta política avalia tooidentify de regras de regras de segurança de entrada que permitam o tráfego de entrada. |
| Firewall de aplicação Web |Recomenda-se de que uma firewall de aplicação web seja aprovisionada em máquinas de virtuais quando Olá seguinte é verdadeiro: </br></br>[IP público de nível de instância](../virtual-network/virtual-networks-instance-level-public-ip.md) (ILPIP) é utilizado e hello regras de segurança de entrada para o grupo de segurança de rede associado à Olá são configuradas tooallow acesso tooport 80/443.</br></br>É utilizado o IP com balanceamento de carga e Olá associado balanceamento de carga e regras de tradução (NAT) de endereços de rede de entrada estão configuradas tooallow acesso tooport 80/443. (Para obter mais informações, veja [Suporte do Azure Resource Manager para o Load Balancer](../load-balancer/load-balancer-arm.md). |
| Firewall da próxima geração |Expande as proteções de rede para além dos grupos de segurança de rede, que estão incorporados no Azure. Centro de segurança irá detetar as implementações para os quais uma firewall da próxima geração recomenda-se e ativar tooprovision uma aplicação virtual. |
| Auditoria do SQL e Deteção de Ameaças |Recomenda que a auditoria de acesso tooAzure da base de dados ativada para compatibilidade e também avançada a deteção de ameaças, para efeitos de investigação. |
| Encriptação SQL |Recomenda que a encriptação inativa seja ativada para a suas bases de dados SQL do Azure, cópias de segurança associadas e ficheiros de registo de transação. Mesmo se existir uma falha dos seus dados, esta poderá não ser legível. |
| Avaliação de vulnerabilidades |Recomenda-se de que instala uma solução de avaliação de vulnerabilidades na sua VM. |
| Encriptação de Armazenamento |Atualmente esta funcionalidade está disponível para Blobs do Azure e Ficheiros. Depois de ativar a Encriptação do Serviço de Armazenamento, apenas os novos dados serão encriptados e quaisquer ficheiros existentes nesta conta de armazenamento irão permanecer desencriptados. |
| Acesso de Rede JIT |Quando apenas na hora estiver ativada, o Centro de segurança bloqueia baixo tráfego de entrada tooyour VMs do Azure através da criação de uma regra NSG. Selecione as portas de Olá no Olá VM toowhich deve ser bloqueado tráfego de entrada. Para obter mais informações, veja [Manage virtual machine access using just in time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) (Gerir o acesso da máquina virtual através do just in time). |

Depois de configurar todas as opções, clique em **OK** no Olá **política de segurança** painel que tem as recomendações de Olá e, em seguida, clique em **guardar** no Olá **segurança Política** painel que tem definições iniciais Olá.

> [!NOTE]
> Se ainda aplica ao nível do grupo de recursos Olá Olá escalão de preço. Para obter mais informações visitando Olá [preços](https://azure.microsoft.com/pricing/details/security-center/) página.
>
>

## <a name="see-also"></a>Consultar também
Neste documento, aprendeu como tooconfigure políticas de segurança no Centro de segurança do Azure. toolearn mais acerca do Centro de segurança do Azure, consulte o artigo seguinte Olá:

* [Guia de operações e planeamento do Centro de Segurança do Azure](security-center-planning-and-operations-guide.md). Saiba como tooplan e compreender o Centro de segurança do Azure do Olá estrutura considerações tooadopt.
* [Monitorização de estado de funcionamento de segurança no Centro de Segurança do Azure](security-center-monitoring.md). Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md). Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de Segurança do Azure](security-center-partner-solutions.md). Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
* [Centro de Segurança do Azure FAQ (FAQ do Centro de Segurança do Azure)](security-center-faq.md). Localize perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/). Encontre mensagens do blogue acerca da segurança e conformidade do Azure.
