---
title: "práticas recomendadas de segurança de máquina virtual aaaAzure | Microsoft Docs"
description: "Este artigo fornece uma variedade de segurança melhores práticas toobe utilizada nas máquinas virtuais localizadas no Azure."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Melhores práticas de segurança de VM do Azure

Na maioria dos infraestrutura como cenários de serviço (IaaS), [máquinas de virtuais (VMs) do Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/) é informática de carga de trabalho principal do Olá para as organizações que utilizam a nuvem. Este facto é especialmente evidente em [cenários híbridos](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) em que as organizações pretender tooslowly migrar nuvem toohello de cargas de trabalho. Tais cenários, siga Olá [considerações de segurança geral para o IaaS](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)e aplicar segurança melhores práticas tooall as suas VMs.

Este artigo explica vários VM melhores práticas de segurança, cada derivado os nossos clientes e o nossas própria experiências diretas com as VMs.

melhores práticas de Olá baseiam-se num consenso da opinião e funcionam com capacidades de plataforma do Azure atual e conjuntos de funcionalidade. Porque opinions e tecnologias podem alterar ao longo do tempo, planeamos tooupdate este artigo regularmente tooreflect essas alterações.

Para cada melhor prática, artigo Olá explica:

* Que Olá melhor prática é.
* É uma boa ideia tooenable-lo.
* Como pode saber tooenable-lo.
* O que pode acontecer se falhar tooenable-lo.
* Possíveis alternativas toohello melhor prática.

artigo de Olá examina Olá seguintes práticas recomendadas de segurança VM:

* VM autenticação e controlo de acesso
* Acesso de disponibilidade e rede VM
* Proteger os dados Inativos no VMs através da imposição de encriptação
* Gerir as atualizações VM
* Gerir a sua postura de segurança VM
* Monitorizar o desempenho de VM

## <a name="vm-authentication-and-access-control"></a>VM autenticação e controlo de acesso

Olá primeiro passo para proteger a VM está tooensure apenas que os utilizadores autorizados são tooset capaz de segurança de VMs de novo. Pode utilizar [políticas do Azure Resource Manager](../azure-resource-manager/resource-manager-policy.md) tooestablish convenções de recursos na sua organização, criar políticas personalizadas e aplicar tooresources estas políticas, tais como [grupos de recursos](../azure-resource-manager/resource-group-overview.md).

As VMs que pertencem os grupo de recursos de tooa naturalmente herdam as respetivas políticas. Embora seja recomendável esta abordagem toomanaging VMs, pode também políticas de controlo de acesso tooindividual VM utilizando [controlo de acesso baseado em funções (RBAC)](../active-directory/role-based-access-control-configure.md).

Quando ativar políticas de Gestor de recursos e acesso VM de toocontrol RBAC, ajudar a melhorar a segurança VM geral. Recomendamos que consolidar as VMs com Olá ciclo de vida do mesma para Olá mesmo grupo de recursos. Ao utilizar grupos de recursos, pode implementar, monitorizar e os custos para os seus recursos de faturação de agregação. tooenable utilizadores tooaccess e o conjunto de segurança das VMs, utilize um [abordagem do menor privilégio](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). E quando atribui toousers de privilégios, planeie Olá toouse seguintes funções do Azure incorporadas:

- [Contribuinte de máquina virtual](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): pode gerir VMs, mas não Olá virtual toowhich de conta armazenamento ou de rede estão ligados.
- [Clássico contribuinte de Máquina Virtual](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): pode gerir VMs criadas utilizando o modelo de implementação clássica Olá, mas não Olá virtual rede ou armazenamento conta toowhich Olá as VMs estão ligadas.
- [Gestor de segurança](../active-directory/role-based-access-built-in-roles.md#security-manager): pode gerir os componentes de segurança, as políticas de segurança e as VMs.
- [DevTest Labs utilizador](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): pode ver tudo ligar, iniciar, reiniciar e encerrar VMs.

Não partilhe as contas e palavras-passe entre administradores e não reutilize palavras-passe em várias contas de utilizador ou serviços, especialmente palavras-passe de redes sociais ou outras atividades não administrativas. Idealmente, deve utilizar [do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modelos tooset as VMS em segurança. Ao utilizar esta abordagem, pode reforçar as opções de implementação e impor as definições de segurança em toda a implementação de Olá.

As organizações que não a impor controlo de acesso a dados, tirando partido de capacidades, tal como o RBAC podem ser conceder os seus utilizadores mais privilégios que necessário. Dados do utilizador inadequadas acesso toocertain diretamente podem comprometer a esses dados.

## <a name="vm-availability-and-network-access"></a>Acesso de disponibilidade e rede VM

Se a VM executa aplicações críticas que necessitam de toohave elevada disponibilidade, recomendamos vivamente a utilização de várias VMs. Para uma melhor disponibilidade, criar, pelo menos, duas VMs no Olá [conjunto de disponibilidade](../virtual-machines/windows/tutorial-availability-sets.md).

[Azure Load Balancer](../load-balancer/load-balancer-overview.md) também requer que as VMs com balanceamento de carga pertencem toohello mesmo conjunto de disponibilidade. Se estas VMs tem de ser acedidos a partir Olá Internet, tem de configurar um [Balanceador de carga para a Internet](../load-balancer/load-balancer-internet-overview.md).

Quando as VMs são toohello exposto à Internet, é importante que [controlar o fluxo de tráfego de rede com grupos de segurança de rede (NSGs)](../virtual-network/virtual-networks-nsg.md). Porque os NSGs podem ser aplicados toosubnets, pode minimizar o número de Olá de NSGs agrupando os recursos por sub-rede e, em seguida, aplicar NSGs toohello sub-redes. Olá intenção é que toocreate uma camada de isolamento de rede, pode fazê-lo ao configurar corretamente Olá [segurança de rede](../best-practices-network-security.md) capacidades no Azure.

Também pode utilizar Olá just-in-time (JIT) VM-funcionalidade de acesso do Centro de segurança do Azure toocontrol que tenha acesso remoto tooa VM específica e para o período de tempo.

As organizações que não a impor restrições de acesso de rede com acesso à tooInternet VMs são expostos toosecurity riscos, tais como um ataque de força bruta de protocolo RDP (Remote Desktop Protocol).

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Proteger dados Inativos nas suas VMs através da imposição de encriptação

[Encriptação de dados Inativos](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) é um passo obrigatório na direção soberania dos dados, privacidade e conformidade de dados. [Azure Disk Encryption](../security/azure-security-disk-encryption.md) permite que os administradores IT tooencrypt Windows e os discos de VM do IaaS Linux. Encriptação de disco combina a funcionalidade de BitLocker do Windows hello norma da indústria e Olá Linux dm-crypt funcionalidade tooprovide encriptação de volume para Olá SO e discos de dados de Olá.

Pode aplicar encriptação de disco toohelp salvaguardar o dados toomeet os requisitos de segurança e conformidade organizacionais. Organização deve considerar a utilização de encriptação toohelp mitigar os riscos relacionados toounauthorized acesso a dados. Recomendamos também que encriptar as suas unidades antes de escrever toothem dados confidenciais.

Ser tooencrypt se sua tooprotect de volumes de dados VM-las em rest na sua conta do storage do Azure. Proteger chaves de encriptação de Olá e o segredo utilizando [Cofre de chaves do Azure](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

As organizações que não impor a encriptação de dados são problemas de integridade toodata mais expostos. Por exemplo, os utilizadores não autorizados ou não autorizados poderão roubo de dados em contas comprometidas ou obter toodata de acesso não autorizado codificada no ClearFormat. Para além de colocar nessas riscos, toocomply com regulamentos da indústria, as empresas tem de provar que estes são exercising diligence e segurança correta a utilizar controla tooenhance a segurança de dados.

toolearn mais informações sobre a encriptação de disco, consulte [encriptação de disco do Azure para Windows e as VMs de IaaS Linux](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>Gerir as atualizações VM

Uma vez que as VMs do Azure, como todos os locais VMs, são toobe pretendido gerida pelo utilizador, Azure não push toothem de atualizações do Windows. É, no entanto, encouraged tooleave Olá Windows Update definição automática ativada. Outra opção consiste toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) ou outro produto de gestão de atualizações adequado no outro VM ou no local. O WSUS e o Windows Update manter VMs atual. Também recomendamos que utilize uma análise tooverify de produto que todas as suas VMs de IaaS estão operacionais toodate.

As cotações imagens fornecidas pelo Azure são Olá tooinclude regularmente atualizada mais recente arredondar de atualizações do Windows. No entanto, não há nenhuma garantia que as imagens de Olá será atuais no momento da implementação. Um atraso ligeiras (de mais do que algumas semanas) seguintes versões públicas pode ser possível. A verificar e instalar todas as atualizações do Windows devem ser Olá primeiro passo cada implementação. Esta medida é tooapply especialmente importante ao implementar imagens do ou as suas próprias bibliotecas. As imagens que são fornecidas como parte da Olá Azure Marketplace são atualizadas automaticamente por predefinição.

As organizações que não impõem políticas de atualização de software são mais toothreats expostas que explora vulnerabilidades conhecidas, anteriormente fixas. Para além de risking estas ameaças, toocomply com normas da indústria, as empresas tem de provar que estes são exercising diligence e toohelp de controlos de segurança correta a utilizar segurança Olá da respetiva carga de trabalho localizada na nuvem de Olá.

É importante tooemphasize que melhores práticas para centros de dados tradicionais de atualização de software e IaaS do Azure têm diversas semelhanças. Por conseguinte, recomendamos avaliar o seu tooinclude de políticas de atualização de software atual VMs.

## <a name="manage-your-vm-security-posture"></a>Gerir a sua postura de segurança VM

Estão a evolução das ameaças informático e proteger as suas VMs requer uma capacidade de monitorização de avançada que pode rapidamente detetar ameaças, impedir que os recursos de tooyour de acesso não autorizado, acionar alertas e reduzir os falsos positivos. postura de segurança de Olá para uma carga de trabalho é composto por todos os aspetos de segurança de Olá VM, de acesso de rede de toosecure de gestão de atualização.

postura de segurança de Olá toomonitor do seu [Windows](../security-center/security-center-virtual-machine.md) e [VMs com Linux](../security-center/security-center-linux-virtual-machine.md), utilize [Centro de segurança do Azure](../security-center/security-center-intro.md). No Centro de segurança do Azure, Salvaguarde as suas VMs, tirando partido de Olá seguintes capacidades:

* Aplicar definições de segurança de SO com regras de configuração recomendada
* Identificar e transferir atualizações críticas que podem estar em falta e de segurança do sistema
* Implementar recomendações de proteção antimalware de ponto final
* Validar a encriptação de disco
* Avaliar e remediar as vulnerabilidades
* Detetar ameaças

Centro de segurança pode monitorizar ativamente para as ameaças e potenciais ameaças são expostas em **alertas de segurança**. Ameaças correlacionadas são agregadas de uma única vista chamada **incidente de segurança**.

toounderstand como o Centro de segurança pode ajudar a identificar potenciais ameaças nas suas VMs localizados no Azure, veja Olá seguir as vídeo:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

As organizações que não impõem uma postura de segurança forte para as respetivas VMs permanecem não tem conhecimento de tentativas de potenciais por controlos de segurança de toocircumvent estabelecida de utilizadores não autorizados.

## <a name="monitor-vm-performance"></a>Monitorizar o desempenho de VM

Abuso de recurso pode ser um problema ao VM processos consumam mais recursos que deveriam. Problemas de desempenho com uma VM podem levar tooservice interrupção, que viola o princípio de segurança de Olá de disponibilidade. Por este motivo, é imperativo toomonitor acesso VM não só reativamente, enquanto está a ocorrer um problema, mas também proativamente, contra o desempenho da linha de base medida durante o funcionamento normal.

Analisando [ficheiros de registo de diagnóstico do Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), pode monitorizar os recursos da VM e identificar potenciais problemas que possam comprometer o desempenho e disponibilidade. Olá extensão de diagnóstico do Azure fornece capacidades de monitorização e diagnóstico em VMs baseadas no Windows. Pode ativar estas funcionalidades, incluindo a extensão de Olá como parte da Olá [modelo Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md).

Também pode utilizar [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-metrics.md) toogain visibilidade para o estado de funcionamento do recurso.

As organizações que não a monitorizar o desempenho da VM são toodetermine não é possível se determinadas alterações nos padrões de desempenho são normal ou anormal. Se Olá VM está a consumir mais recursos que o habitual, essas uma anomalias pode indicar um ataque potencial de um recurso externo ou um processo comprometido em execução no Olá VM.
