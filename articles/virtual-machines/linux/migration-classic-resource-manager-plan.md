---
title: "aaaPlanning para a migração de recursos IaaS do clássico tooAzure Resource Manager | Microsoft Docs"
description: "Planeamento da migração de recursos IaaS do clássico tooAzure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 53c6f640425b69cae2ef10afb8c92b8ac4394267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Planeamento da migração de recursos IaaS do clássico tooAzure Resource Manager
Enquanto o Azure Resource Manager oferece muitas funcionalidades incrível, é fundamental tooplan saída toomake de journey sua migração sure coisas correm. A dedicar muito tempo sobre o planeamento irá garantir que não ocorrerem problemas ao executar atividades de migração. 

> [!NOTE] 
> Olá seguir orientações era a equipa de Consultadora de cliente do Azure de Olá de descontos elevados contribuíram tooby e arquitetos de soluções de nuvem a trabalhar com os clientes migrar enviornments grandes. Como tal, este documento continuará tooget atualizada como novos padrões de sucesso surgir, por isso, verifique novamente a partir do momento tootime toosee se existirem quaisquer novas recomendações.

Existem quatro fases geral do journey de migração de Olá:

![Fases de migração](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Planear

### <a name="technical-considerations-and-tradeoffs"></a>Considerações de técnicas e fala

Consoante o tamanho de requisitos técnicos, localizações geográficas e práticas operacionais, poderá querer tooconsider:

1. Por que motivo o Azure Resource Manager for pretendido para a sua organização?  Quais são as razões de negócio Olá para uma migração?
2. Quais são as razões de Olá técnica para o Azure Resource Manager?  O que (se aplicável) adicionais serviços do Azure seriam como tooleverage?
3. Que aplicações (ou conjuntos de máquinas virtuais) estão incluídos na migração Olá?
4. São suportados os cenários de migração Olá API?  Olá revisão [não suportado funcionalidades e configurações](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations).
5. As equipas operacionais agora suportar VMs/aplicações em clássica e do Azure Resource Manager?
6. Como (se todo) do Azure Resource Manager alterar a implementação de VM, gestão, monitorização e relatórios processos?  Os scripts de implementação precisa toobe atualizado?
7. O que é comunicações Olá planear tooalert intervenientes (os utilizadores finais, os proprietários da aplicação e proprietários de infraestrutura)?
8. Dependendo da complexidade Olá do ambiente de Olá, deve existir um período de manutenção onde Olá é tooend indisponível utilizadores e proprietários de tooapplication?  Se Sim, para o período de tempo?
9. O que é intervenientes de tooensure de plano de formação Olá é knowledgeable e proficient no Gestor de recursos do Azure?
10. O que é a gestão do programa de Olá ou plano de gestão do projeto para a migração de Olá?
11. Quais são as linhas cronológicas de Olá para migração do Olá do Azure Resource Manager e outros relacionadas com tecnologia da estrada maps?  São serem executadas de forma ideal alinhados?

### <a name="patterns-of-success"></a>Padrões de sucesso

Os clientes com êxito tem detalhadas planos onde o Olá acima perguntas são abordados, documentados e regida.  Certifique-se de que os planos de migração de Olá são comunicados amplamente toosponsors e intervenientes.  Equipar por si com conhecimentos sobre as opções de migração; é altamente recomendável ler através deste documento migração definido abaixo.

* [Descrição geral da migração de plataforma suportada dos recursos IaaS do clássico tooAzure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnica detalhada da plataforma suportada a migração do Gestor de recursos de tooAzure clássico](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planeamento da migração de recursos IaaS do clássico tooAzure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utilizar o PowerShell toomigrate IaaS recursos do Gestor de recursos de tooAzure clássico](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utilizar recursos de IaaS toomigrate CLI do clássico tooAzure Resource Manager](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ferramentas de Comunidade para prestar assistência com a migração de recursos IaaS do clássico tooAzure Resource Manager](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Consultar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Olá revisão mais perguntas mais frequentes sobre a migração de IaaS de recursos do Gestor de recursos de tooAzure clássico](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Pitfalls tooavoid

- Tooplan de falha.  passos de tecnologia de Olá desta migração são comprovados e resultado Olá é previsível.
- Pressuposto de que a API de migração de plataforma suportada Olá será conta para todos os cenários. Olá leitura [não suportado funcionalidades e configurações](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) toounderstand que cenários são suportados.
- Planear não potencial falha de aplicação para os utilizadores finais.  Planear a memória intermédia suficiente tooadequately avisar os utilizadores finais de tempo de aplicação potencialmente indisponível.


## <a name="lab-test"></a>Teste de laboratório 

**Replicar o seu ambiente e efetuar uma migração de teste**
  > [!NOTE]
  > É executada replicação exata do seu ambiente existente utilizando uma ferramenta contribuíram de Comunidade que não é oficialmente suportada pelo Support da Microsoft. Por conseguinte, é um **opcional** passo mas é melhor forma toofind Olá problemas sem afetar os ambientes de produção. Se utilizar uma ferramenta contribuíram de Comunidade não é uma opção, em seguida, leia sobre Olá preparar/validar/abortar Dry executar recomendação abaixo.
  >
  
  Realizar um laboratório de teste do seu cenário exato (computação, redes e armazenamento) é Olá melhor forma tooensure uma migração uniforme. Isto irá ajudar a garantir:

  - Um laboratório detida separado ou uma existente tootest de ambiente de não produção. Recomendamos um laboratório detida separado que pode ser migrado repetidamente e pode ser modificado destructively.  Scripts toocollect/hydrate metadados de subscrições real Olá estão listados abaixo.
  - É um laboratório de Olá toocreate boa ideia de uma subscrição separada. Olá razão é que laboratório Olá será desligado repetidamente e ter um separado, subscrição isolada irá reduzir hipótese de Olá algo reais que irá obter forma acidental eliminado.

  Isto pode ser conseguido utilizando Olá AsmMetadataParser ferramenta. [Leia mais sobre esta ferramenta aqui](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

### <a name="patterns-of-success"></a>Padrões de sucesso

seguinte Olá foram problemas detetados no muitas das migrações maior Olá. Não se trata de uma lista exaustiva e devem consultar toohello [não suportado funcionalidades e configurações](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) para obter mais detalhes. Pode ou não pode encontrar estes problemas técnicos, mas se o fizer a resolver estes antes de tentar efetuar a migração irá garantir uma experiência smoother.

- **Fazer uma execução de Dry preparar/validar/abortar** -talvez é Olá mais importante passo tooensure clássico tooAzure Resource Manager migração com êxito. migração de Olá API tem três passos principais: validar, preparar e a consolidação. Validar será leu o estado de Olá do seu ambiente clássico e devolver um resultado de todos os problemas. No entanto, porque alguns problemas poderão existir na pilha de Azure Resource Manager Olá, validar será interceta tudo. Olá próximo passo no processo de migração, preparar ajudará a expor esses problemas. Preparar irá mover Olá os metadados do clássico tooAzure Resource Manager, mas será não consolidação Olá mover e irá não remover ou alterar tudo na Olá lado clássico. Olá dry executar envolve a preparação da migração de Olá, em seguida, abortar (**não são consolidar**) preparar a migração de Olá. objetivo Olá validar/preparar/abortar dry executar é toosee todos os metadados de Olá na pilha do Azure Resource Manager Olá, examiná-lo (*programaticamente ou no Portal*), certifique-se de que tudo migra corretamente e de trabalho através de problemas técnicos.  Esta será também dão-lhe um sentido de duração de migração, para que possam planear em conformidade para período de indisponibilidade.  Um validar/preparar/abortar não irá causar qualquer período de inatividade do utilizador; Por conseguinte, é tooapplication não acontece utilização.
  - itens de Olá abaixo terá toobe resolvido antes de ser executada a dry Olá, mas um teste de execução dry também com segurança esvaziar saída estes passos de preparação se estes estão em falta. Durante a migração de enterprise, encontrámos Olá dry executar toobe preparação da migração tooensure uma forma segura e valiosas.
  - Quando preparar está em execução, controlo de Olá plane (operações de gestão do Azure) será bloqueada para a rede virtual todo de Olá, pelo que não podem ser feitas alterações tooVM metadados durante a validar/preparar/abortar.  Mas, caso contrário, qualquer função de aplicação (RD, VM utilização, etc.) será afetada.  Os utilizadores de VMs de Olá não saberá que está a ser executado com dry Olá.

- **Express circuitos Expressroute e a VPN**. Atualmente, Gateways de rota Express com ligações de autorização não podem ser migrados sem períodos de indisponibilidade. Para a solução de Olá, consulte [migrar ExpressRoute circuitos e associadas redes virtuais do modelo de implementação Resource Manager do Olá toohello clássico](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **Extensões de VM** -extensões de Máquina Virtual, potencialmente, são uma das Olá maior roadblocks toomigrating VMs em execução. Remediação de extensões de VM pode demorar upwards of 1-2 dias, por isso planeie em conformidade.  Um trabalho do agente do Azure é tooreport necessários estado de extensão da VM anterior de VMs em execução. Se o estado de Olá volta como incorreto para uma VM em execução, esta será parado a migração. agente de Olá próprio não tem toobe na ordem de trabalho tooenable migração, mas se existirem extensões Olá VM, ambos os um agente de trabalho e saído acesso à internet (com o DNS) serão necessários para reencaminhar toomove de migração.
  - Se o servidor DNS tooa conectividade se perder durante a migração, todas as extensões de VM, exceto BGInfo v1. \* necessário toofirst removidos cada VM antes de preparar a migração e posteriormente adicionado novamente toohello back VM após a migração do Gestor de recursos do Azure.  **Esta é apenas para as VMs que estejam a executar.**  Se Olá VMs está parado desalocada, extensões de VM não é necessário toobe removido. **Nota:** várias extensões, tal como será monitorização do Centro de segurança e diagnóstico do Azure reinstalar próprios após a migração, por isso, a remover não é um problema.
  - Além disso, certifique-se grupos de segurança de rede não são restringir o acesso de internet de saída. Isto pode acontecer com algumas configurações de grupos de segurança de rede. Acesso de internet de saída (e DNS) é necessário para extensões de VM toobe migrados tooAzure Resource Manager. 
  - Existem duas versões do Olá extensão BGInfo: v1 e v2.  Se Olá VM foi criada utilizando o portal clássico Olá ou PowerShell, Olá VM terá provavelmente extensão de v1 Olá no mesmo. Esta extensão não necessita de toobe removido e será ignorado (não migrados) pela migração Olá API. No entanto, se Olá VMS clássicas foi criada com o novo portal do Azure Olá, terá que é provável que versão de Olá v2 baseados em JSON do BGInfo, que pode ser migrada tooAzure Gestor de recursos fornecido agente Olá está a funcionar e se tem acesso de internet de saída (e DNS). 
  - **Opção de remediação 1**. Se souber que as suas VMs não terão saída acesso à internet, um serviço DNS de funcionar e, em seguida, os agentes do Azure a trabalhar em VMs Olá, desinstale todas as extensões VM como parte da migração de Olá antes de preparar, em seguida, reinstale Olá extensões de VM após a migração. 
  - **Opção de remediação 2**. Se forem demasiado grandes de um hurdle extensões VM, outra opção consiste tooshutdown/desalocar todas as VMs antes da migração. Migrar Olá desalocada VMs e reiniciá-las no Olá do lado do Azure Resource Manager. benefício de Olá aqui é que as extensões de VM irão migrar. Olá downside é que todos os público com acesso à IPs virtuais serão perdidas (pode ser um não-starter), e, obviamente Olá VMs será encerrado a causar um muito maior impacto nas aplicações de trabalho.

    > [!NOTE] 
    > Se estiver configurada uma política do Centro de segurança do Azure contra Olá executar as VMs que está a ser migradas, tem de política de segurança de Olá toobe parado antes de remover as extensões, caso contrário, a segurança Olá extensão monitorização será reinstalado automaticamente Olá VM após a removê-lo.

- **Conjuntos de disponibilidade** – para uma rede virtual (vNet) toobe migrados tooAzure Gestor de recursos, Olá VMs de implementação (ou seja, o serviço de nuvem) contida clássica têm de estar todos num conjunto de disponibilidade ou Olá VMs todos os não é necessário qualquer conjunto de disponibilidade. Ter mais do que um conjunto de disponibilidade no serviço de nuvem Olá não é compatível com o Azure Resource Manager e será parado a migração.  Além disso, não pode existir algumas VMs num conjunto de disponibilidade e algumas VMs não num conjunto de disponibilidade. tooresolve, será necessário tooremediate ou reshuffle o seu serviço em nuvem.  Planear em conformidade, como poderá ser demorada. 

- **Implementações de função da Web/trabalho** -serviços em nuvem que contém funções web e de trabalho não é possível migrar tooAzure Resource Manager. Olá web/funções de trabalho primeiro tem de ser removidas a partir da rede virtual Olá antes de iniciar a migração.  Uma solução típica é toojust mover web/trabalho função instâncias tooa separado rede virtual clássica que seja também circuito de ExpressRoute tooan ligado ou toomigrate Olá código toonewer serviços de aplicacionais PaaS (este debate ultrapassa o âmbito Olá deste documento). No anterior Olá Reimplementar caso, crie uma nova rede virtual clássica, mover/implementar Olá web/trabalho funções toothat nova rede virtual e eliminar as implementações de Olá a partir da rede virtual Olá a ser movido. Não existem alterações de código necessárias. Olá novo [Peering de rede Virtual](../../virtual-network/virtual-network-peering-overview.md) capacidade pode ser toopeer utilizado em conjunto Olá clássico rede virtual que contém Olá web/funções de trabalho e outras redes virtuais na mesma região do Azure, tais como a rede virtual ser Olá de Olá migrar (**depois de concluída a migração da rede virtual, redes virtuais em modo de peering não podem ser migradas**), por conseguinte, fornecer Olá mesmas capacidades sem perda de desempenho e não penalidades de latência/largura de banda. Dada a adição de Olá de [Peering de rede Virtual](../../virtual-network/virtual-network-peering-overview.md), implementações de função da web/trabalho facilmente agora podem ser mitigadas e bloquear não Olá migração tooAzure Resource Manager.

- **Quotas do Gestor de recursos do Azure** -regiões do Azure têm quotas/limites separados para clássica e do Azure Resource Manager. Apesar de um cenário de migração não está a ser consumido novo hardware *(está a troca de VMs existentes do clássico tooAzure Gestor de recursos)*, quotas do Azure Resource Manager continua a precisar toobe no local com capacidade suficiente antes Pode começar a migração. Abaixo encontram-se descritos Olá principais os limites que viu causam problemas.  Abra um Olá de tooraise de pedido de suporte de quota limita. 

    > [!NOTE]
    > Estes limites necessário toobe gerado em Olá mesma região como migrado do seu toobe ambiente atual.
    >

    - Interfaces de Rede
    - Balanceadores de carga
    - IPs públicos
    - IPs públicos estáticos
    - Núcleos
    - Grupos de Segurança de Rede
    - Tabelas de Rota

    Pode verificar a sua atual quotas do Azure Resource Manager utilizando Olá os seguintes comandos com a versão mais recente do Olá do Azure CLI 2.0.

    **Computação** *(núcleos, conjuntos de Avaiability)*

    ```bash
    az vm list-usage -l <azure-region> -o jsonc 
    ```

    **Rede** *(Interfaces, balanceadores de carga, as tabelas de rotas de rede de redes virtuais, os IPs públicos estáticos, os IPs públicos, grupos de segurança de rede)*
    
    ```bash
    az network list-usages -l <azure-region> -o jsonc
    ```

    **Armazenamento** *(conta de armazenamento)*
    
    ```bash
    az storage account show-usage
    ```

- **API de Gestor de recursos do Azure, os limites** – se tiver um ambiente grande o suficiente (ex. > 400 VMs numa VNET), pode clicar em Olá predefinido API os limites para escritas (atualmente **1200 escritas/hora**) no Gestor de recursos do Azure. Antes de iniciar a migração, deve de aumentar um tooincrease de pedido de suporte esse limite para a sua subscrição.

- **Excedeu o tempo limite estado de VM de aprovisionamento** - se qualquer VM tem o estado Olá **aprovisionamento excedeu o tempo**, este necessidades toobe resolvido pré-migração. Olá única forma toodo trata com período de indisponibilidade por desaprovisionamento/reprovisioning Olá VM (eliminar, mantenha disco Olá e recrie Olá VM). 

- **Estado da VM RoleStateUnknown** - se a migração forem devido tooa **estado de função desconhecido** erro da mensagem, Inspecione Olá VM através do portal Olá e certifique-se de que está a ser executado. Este erro normalmente desaparecerá respetivo proprietário (sem remediação necessária) após alguns minutos e é, muitas vezes, um tipo transitório frequentemente visto durante uma Máquina Virtual **iniciar**, **parar**, **reiniciar** operações. **Recomendado prática:** nova tentativa de migração novamente após alguns minutos. 

- **Cluster de recursos de infraestrutura não existe** – em alguns casos, determinados de VMs não podem ser migradas por vários motivos ímpares. Um nestes casos conhecidos é se Olá VM foi criada recentemente (num Olá última semana ou modo) ocorreu tooland um cluster do Azure que ainda não está equipado para cargas de trabalho do Azure Resource Manager.  Receberá um erro que indica que **fabric cluster não existe** e hello VM não pode ser migrada. A aguardar alguns dias, normalmente, irá resolver este problema específico como cluster Olá logo que irá obter ativado o Azure Resource Manager. No entanto, uma solução imediata é demasiado`stop-deallocate` Olá VM, reencaminhar continuar com a migração e iniciar Olá VM cópia de segurança no Azure Resource Manager depois de migrar.

### <a name="pitfalls-tooavoid"></a>Pitfalls tooavoid

- Não demorar atalhos e omitir a migrações de validar/preparar/abortar dry executar Olá.
- Mais, caso contrário, os problemas potenciais será superfície durante os passos de validar/preparar/abortar Olá.

## <a name="migration"></a>Migração

### <a name="technical-considerations-and-tradeoffs"></a>Considerações de técnicas e fala

Agora, está pronto porque já trabalhou através de Olá os problemas conhecidos com o seu ambiente.

Para as migrações real Olá, poderá querer tooconsider:

1. Planear e agendar a rede virtual Olá (unidade mais pequena de migração) com aumento de prioridade.  Olá simples redes virtuais pela primeira vez, e progresso com Olá mais complicados redes virtuais.
2. Maioria dos clientes terão de ambientes de não produção e de produção.  Agende produção pela última vez.
3. **(OPCIONAL)**  Agendar um período de indisponibilidade de manutenção com muitos da memória intermédia no caso de surgem problemas inesperados.
4. Comunicar com e alinhar com as equipas de suporte no caso de surgir um.

### <a name="patterns-of-success"></a>Padrões de sucesso

deve ser considerada e atenuados tooa anterior de migração real Olá técnica documentação de orientação de Olá secção laboratório teste acima.  Com testes adequados, a migração de Olá é, na verdade, um non-evento.  Para ambientes de produção, poderá ser útil toohave obter suporte adicional, tal como um parceiro da Microsoft fidedigno ou serviços do Microsoft Premier.

### <a name="pitfalls-tooavoid"></a>Pitfalls tooavoid

A testar não totalmente poderá causar problemas e atraso na migração Olá.  

## <a name="beyond-migration"></a>Para além da migração

### <a name="technical-considerations-and-tradeoffs"></a>Considerações de técnicas e fala

Agora que já está no Gestor de recursos do Azure, maximize a plataforma de Olá.  Olá leitura [descrição geral do Gestor de recursos do Azure](../../azure-resource-manager/resource-group-overview.md) toofind saída sobre outras vantagens.

Tooconsider coisas:

- Agrupamento Olá a migração com outras atividades.  Optar ativamente por participar a maioria dos clientes para uma janela de manutenção da aplicação.  Se Sim, é aconselhável toouse tooenable este período de indisponibilidade outras funcionalidades do Gestor de recursos do Azure como encriptação e migração tooManaged discos.
- Revê Olá técnico e as razões de negócio para o Azure Resource Manager; Ative Olá serviços adicionais disponíveis apenas no Azure Resource Manager que se aplicam tooyour ambiente.
- Modernize o seu ambiente com os serviços de PaaS.

### <a name="patterns-of-success"></a>Padrões de sucesso

Ser tem um fim específico no qual serviços agora pretende tooenable no Gestor de recursos do Azure.  Muitos clientes localizar Olá abaixo apelativa para os seus ambientes do Azure:

- [Controlo de acesso baseado em funções](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Modelos Azure Resource Manager para a implementação mais fácil e mais controlada](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Etiquetas](../../azure-resource-manager/resource-group-using-tags.md).
- [Controlo de atividade](../../azure-resource-manager/resource-group-audit.md)
- [Políticas de recursos](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Pitfalls tooavoid

Lembre-se de que o motivo pelo qual iniciou esta journey de migração do Gestor de recursos de tooAzure clássico.  Quais eram razões de negócio original Olá? Alcançar razão comercial de Olá?


## <a name="next-steps"></a>Passos seguintes

* [Descrição geral da migração de plataforma suportada dos recursos IaaS do clássico tooAzure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnica detalhada da plataforma suportada a migração do Gestor de recursos de tooAzure clássico](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planeamento da migração de recursos IaaS do clássico tooAzure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Utilizar o PowerShell toomigrate IaaS recursos do Gestor de recursos de tooAzure clássico](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Ferramentas de Comunidade para prestar assistência com a migração de recursos IaaS do clássico tooAzure Resource Manager](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Consultar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Olá revisão mais perguntas mais frequentes sobre a migração de IaaS de recursos do Gestor de recursos de tooAzure clássico](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
