---
title: "Glossário aaaAzure - dicionário do Azure | Microsoft Docs"
description: "Utilize terminologia de nuvem do Olá Glossário do Azure toounderstand Olá plataforma Azure. Este dicionário do Azure pequeno fornece definições comuns termos de nuvem do Azure."
keywords: "Dicionário do Azure, terminologia de nuvem, Glossário do Azure, definições terminológicas, os termos de nuvem"
services: na
documentationcenter: na
author: MonicaRush
manager: jhubbard
editor: 
ms.assetid: d7ac12f7-24b5-4bcd-9e4d-3d76fbd8d297
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: monicar
ms.openlocfilehash: 486bbbfc71a48a6ebc39b14f7ab71f8604b7a6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-glossary-a-dictionary-of-cloud-terminology-on-hello-azure-platform"></a>Glossário do Microsoft Azure: um dicionário de terminologia de nuvem no Olá plataforma do Azure

Glossário do Microsoft Azure de Olá é um dicionário abreviado do terminologia de nuvem do Olá plataforma Azure. Veja também:

* [Microsoft Azure e o Amazon Web Services](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/) -serviços de definições do Azure e os seus homólogos AWS.<!-- I propose toolink toohttps://azure.microsoft.com/en-us/services/ instead of this -->
* [Termos de computação da nuvem](https://azure.microsoft.com/overview/cloud-computing-dictionary/) -termos de nuvem da indústria geral.

## <a name="account"></a>Conta
Uma conta que tenha utilizado tooaccess e gerir uma subscrição do Azure. -Tem muitas vezes designado tooas um Azure conta embora uma conta pode ser qualquer um dos seguintes: um trabalho existente, escola, ou pessoais conta Microsoft, ou um nome de utilizador do Office 365 e palavra-passe. Também pode criar uma conta toomanage uma subscrição do Azure quando se inscreve para Olá [avaliação gratuita](https://azure.microsoft.com).  
Consulte [inscrever-se para uma subscrição do Azure com a sua conta Office 365](billing/billing-use-existing-office-365-account-azure-subscription.md) e [contas podem utilizar toosign no](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="api-app"></a>Aplicação API
Outro nome para [aplicação do app Service](#app-service-app).

## <a name="app-service-app"></a>Aplicação do app Service
Olá recursos de computação que [App Service do Azure](app-service/app-service-value-prop-what-is.md) fornece para alojar um [Web site ou aplicação web](app-service-web/app-service-web-overview.md), [web API](app-service-api/app-service-api-apps-why-best-platform.md), ou [back-end da aplicação móvel](app-service-mobile/app-service-mobile-value-prop.md). Aplicações do App Service também são referidos tooas *serviços aplicacionais*, *aplicações web*, *das API apps*, e *aplicações móveis*.

## <a name="availability-set"></a>conjunto de disponibilidade
Uma coleção de máquinas virtuais que são geridos em conjunto tooprovide redundância de aplicação e fiabilidade. utilização de Olá de um conjunto de disponibilidade assegura que, durante um evento de manutenção planeado ou não planeado, pelo menos uma máquina virtual está disponível.  
Consulte [gerir a disponibilidade de Olá das Windows virtual machines](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gerir a disponibilidade de Olá das máquinas virtuais do Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="classic-model"></a>Modelo de implementação clássica do Azure
Um dos dois [modelos de implementação](resource-manager-deployment-model.md) utilizado toodeploy recursos no Azure (o novo modelo de Olá é o Azure Resource Manager). Alguns serviços do Azure suportam apenas Olá modelo Implementação Resource Manager, algumas suportam apenas o modelo de implementação clássica Olá e algumas de suportar. documentação de Olá para cada serviço do Azure Especifica quais model(s) suportam.

## <a name="cli"></a>Interface de linha de comandos (CLI) do Azure
Uma interface de linha de comandos que podem ser utilizado toomanage Azure serviços a partir de Windows, macOS e Linux.  Alguns serviços ou funcionalidades de serviço podem ser geridas apenas através do PowerShell ou Olá CLI. Consulte [CLI do Azure 2.0](/cli/azure/overview)

## <a name="powershell"></a>O Azure PowerShell
Uma interface de linha de comandos toomanage Azure serviços através de uma linha de comandos a partir de Windows PCs. Alguns serviços ou funcionalidades de serviço podem ser geridas apenas através do PowerShell ou Olá CLI.
Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)

## <a name="arm-model"></a>Modelo de implementação do Azure Resource Manager
Um dos dois [modelos de implementação](resource-manager-deployment-model.md) utilizado toodeploy recursos no Microsoft Azure (Olá outro é o modelo de implementação clássica Olá). Alguns serviços do Azure suportam apenas Olá modelo Implementação Resource Manager, algumas suportam apenas o modelo de implementação clássica Olá e algumas de suportar. documentação de Olá para cada serviço do Azure Especifica quais model(s) suportam.

## <a name="fault-domain"></a>Domínio de falhas
Olá coleção de máquinas virtuais num conjunto de disponibilidade que pode possivelmente falhará em Olá mesmo tempo. Um exemplo é um grupo de computadores num bastidor que partilham um comutador de rede de origem e de energia comum. No Azure, as máquinas de virtuais Olá num conjunto de disponibilidade automaticamente estão separadas em vários domínios de falhas.  
Consulte [gerir a disponibilidade de Olá das Windows virtual machines](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [gerir a disponibilidade de Olá das máquinas virtuais do Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)  

## <a name="geo"></a>georreplicação
Um limite definido para residency de dados que contém, geralmente, dois ou mais regiões. limites de Olá podem estar dentro ou se para além dos limites national e são deve influenciados pelos Regulamento dedução dos impostos. Cada georreplicação tem, pelo menos, uma região. Exemplos de geos são Ásia-Pacífico e Japão. Também denominado *geografia*.  
Consulte [regiões do Azure](best-practices-availability-paired-regions.md)

## <a name="geo-replication"></a>replicação geográfica
processo de Olá de replicar automaticamente o conteúdo como blobs, tabelas e filas dentro de um par regional.  
Consulte [Georreplicação ativa para a base de dados SQL do Azure](sql-database/sql-database-geo-replication-overview.md)
<!-- hello meaning of "geo" in this term seems toobe different than hello meaning provided in hello "geo" entry -->

## <a name="image"></a>Imagem
Um ficheiro que contém o sistema de operativo Olá e configuração da aplicação que pode ser utilizado toocreate qualquer número de máquinas virtuais. No Azure, existem dois tipos de imagens: VM imagem e a imagem do SO. Uma imagem de VM inclui um sistema operativo e todos os discos anexados a máquina virtual de tooa quando é criada a imagem de Olá. Imagem do SO contém apenas um sistema operativo generalizado com não configurações de disco de dados.  
Consulte [navegar e selecionadas imagens da máquina virtual Windows no Azure com o PowerShell ou Olá CLI](virtual-machines/windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="limits"></a>Limites
número de Olá de recursos que podem ser criados ou Olá benchmark de desempenho que pode ser alcançado. Os limites associados normalmente subscrições, serviços e ofertas.  
Consulte [subscrição do Azure e limites de serviço, quotas e restrições](azure-subscription-service-limits.md)

## <a name="load-balancer"></a>O Balanceador de carga
Um recurso que distribui o tráfego de entrada entre os computadores numa rede. No Azure, um balanceador de carga distribui máquinas de toovirtual tráfego definidas um conjunto de Balanceador de carga. A [Balanceador de carga](load-balancer/load-balancer-overview.md) pode ser o acesso à internet ou pode ser interna.  

## <a name="mobile-app"></a>aplicação móvel
Outro nome para [aplicação do serviço de aplicações](#app-service-app).

## <a name="offer"></a>oferta
preços Olá, créditos e os termos relacionados a aplicável tooan subscrição do Azure.  
Consulte Olá [página de detalhes de oferta do Azure](https://azure.microsoft.com/support/legal/offer-details/)

## <a name="portal"></a>portal
portal de web seguro Olá utilizado toodeploy e gerir serviços do Azure.  Existem dois portais: Olá [portal do Azure](http://portal.azure.com/) e Olá [portal clássico](http://manage.windowsazure.com/). Alguns serviços estão disponíveis em ambos os portais, enquanto que outras pessoas só estão disponíveis num ou Olá outros. Olá [gráfico de disponibilidade de portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/) listas os serviços estão disponíveis no qual o portal.

## <a name="region"></a>Região
Uma área dentro de uma georreplicação limites não cross national e contém um ou mais dos centros de dados. Preços, os serviços regionais e tipos de oferta estão expostos ao nível da região de Olá. Uma região normalmente se encontra emparelhada com outro região, o que pode ser segurança tooseveral centenas quilómetros ausente. Pares regionais podem ser utilizados como um mecanismo para cenários de elevada disponibilidade e recuperação após desastre. Também referidos tooas *localização*.  
Consulte [regiões do Azure](best-practices-availability-paired-regions.md)

## <a name="resource"></a>Recursos
Um item que faz parte da sua solução do Azure. Cada serviço do Azure permite-lhe toodeploy diferentes tipos de recursos, tais como bases de dados ou de máquinas virtuais.   
Consulte [descrição geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="resource-group"></a>grupo de recursos
Um contentor no Gestor de recursos que retém recursos relacionados para uma aplicação. grupo de recursos de Olá pode incluir todos os recursos de Olá para uma aplicação ou apenas os recursos que estão logicamente agrupados. Pode decidir como pretende que os recursos de tooallocate tooresource grupos com base no que é adequado Olá mais para a sua organização.  
Consulte [descrição geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="arm-template"></a>Modelo do Resource Manager
Um ficheiro JSON que forma declarativa define um ou mais recursos do Azure e que define dependências entre Olá implementado recursos. modelo de Olá pode ser utilizados toodeploy Olá recursos forma consistente e repetida.  
Consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md)

## <a name="resource-provider"></a>Fornecedor de recursos
Um serviço que fornece recursos de Olá, pode implementar e gerir através do Resource Manager. Cada fornecedor de recursos oferece operações para trabalhar com recursos de Olá que estão implementados. Fornecedores de recursos podem ser acedidos através de Olá portal do Azure, Azure PowerShell e vários SDKs de programação.  
Consulte [descrição geral do Azure Resource Manager](azure-resource-manager/resource-group-overview.md)

## <a name="role"></a>Função
Um meio para controlar o acesso que pode ser atribuído toousers, grupos e serviços. As funções são tooperform capaz de ações, tais como criar, gerirem e ler nos recursos do Azure.  
Consulte [RBAC: funções incorporadas](active-directory/role-based-access-built-in-roles.md)

## <a name="sla"></a>contrato de nível de serviço (SLA)
contrato de Olá que descreve os compromissos da Microsoft para o tempo de atividade e conectividade. Cada serviço do Azure tem um SLA específico.  
Consulte [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/)

## <a name="sas"></a>assinatura de acesso partilhado (SAS)
Uma assinatura que permite recursos de tooa de acesso de toogrant limitada, sem a chave de conta a exposição. Por exemplo, [Storage do Azure utiliza SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) toogrant tooobjects de acesso de cliente, tais como os blobs. [IoT Hub utiliza SAS](iot-hub/iot-hub-devguide-security.md#security-tokens) telemetria de toosend toogrant dispositivos permissão.

## <a name="storage-account"></a>conta de armazenamento
Uma conta que dá-lhe aceder aos serviços de ficheiro, tabela, fila e Blob do Azure de toohello no armazenamento do Azure. o nome de conta do storage Olá define o espaço de nomes exclusivo Olá para objetos de dados do Storage do Azure.  
Consulte [contas do storage do Azure sobre](storage/common/storage-create-storage-account.md)

## <a name="subscription"></a>subscrição
Contrato de um cliente com a Microsoft permite-lhes tooobtain Azure serviços. preços de subscrição de Olá e os termos relacionados são regidos pelas oferta Olá escolhida para subscrição Olá.
Consulte [contrato de subscrição Online da Microsoft](https://azure.microsoft.com/support/legal/subscription-agreement/) e [subscrições do Azure como estão associadas ao Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md)

## <a name="tag"></a>Etiqueta
Um termo de indexação que permite recursos de toocategorize de acordo com requisitos de tooyour de gestão ou faturação. Quando tiver uma coleção complexa de recursos, pode utilizar toovisualize etiquetas esses elementos Olá forma Olá mais sentido. Por exemplo, pode Etiquetar recursos que desempenham uma função semelhante na sua organização ou pertencem toohello mesmo departamento.  
Consulte [utilizar etiquetas tooorganize os recursos do Azure](resource-group-using-tags.md)

## <a name="update-domain"></a>Domínio de atualização
Olá coleção de máquinas virtuais num conjunto de disponibilidade que são atualizadas em Olá mesmo tempo. Máquinas virtuais no Olá mesmo domínio de atualização são reiniciadas em conjunto durante a manutenção planeada. O Azure nunca reinicia mais de um domínio de atualização de cada vez. Também referido tooas um domínio de atualização.  
Consulte [gerir a disponibilidade de Olá das Windows virtual machines](virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [gerir a disponibilidade de Olá das máquinas virtuais do Linux](virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vm"></a>máquina virtual
Olá, implementação de software de um computador físico que executa um sistema operativo. Várias máquinas virtuais podem ser executados em simultâneo no Olá mesmo hardware. No Azure, estão disponíveis uma variedade de tamanhos de máquinas virtuais.  
Consulte [documentação de Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)

## <a name="vm-extension"></a>extensão da máquina virtual
Um recurso que implementa comportamentos ou funcionalidades que ajudam a outros programas de trabalho ou fornecem a capacidade de Olá para toointeract com um computador em execução. Por exemplo, pode utilizar tooreset de extensão de acesso de VM Olá ou modificar os valores de acesso remoto numa máquina virtual do Azure.
<!-- This definition seems obscure toome; maybe a list of examples would work better than a conceptual definition? -->
Consulte [sobre extensões de máquina virtual e funcionalidades (Windows)](virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [sobre extensões de máquina virtual e funcionalidades (Linux)](virtual-machines/linux/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="vnet"></a>rede virtual
Uma rede que fornece conectividade entre os recursos do Azure que seja isolado de todos os outros inquilinos do Azure. Um [Gateway de VPN do Azure](vpn-gateway/vpn-gateway-about-vpngateways.md) permite-lhe estabelecer ligações entre redes virtuais e [entre uma rede virtual e uma rede no local](vpn-gateway/vpn-gateway-plan-design.md). Pode controlar totalmente os blocos de endereços IP Olá, definições de DNS, as políticas de segurança e as tabelas de rotas dentro de uma rede virtual.  
Consulte [descrição geral da rede Virtual](virtual-network/virtual-networks-overview.md)  

## <a name="web-app"></a>Aplicação Web
Outro nome para [aplicação do serviço de aplicações](#app-service-app).

## <a name="see-also"></a>Consultar também

* [Introdução ao Azure](https://azure.microsoft.com/get-started/)
* [Centro de recursos de nuvem](https://azure.microsoft.com/resources/)  
* [Azure para a sua aplicação de negócio](https://azure.microsoft.com/overview/business-apps-on-azure/)
* [Azure no seu centro de dados](https://azure.microsoft.com/overview/business-apps-on-azure/)

