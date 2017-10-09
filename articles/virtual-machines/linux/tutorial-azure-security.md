---
title: "aaaAzure Centro de segurança e Linux as máquinas virtuais no Azure | Microsoft Docs"
description: "Saiba mais sobre a segurança para a máquina virtual do Linux do Azure com o Centro de segurança do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Monitorizar a segurança da máquina virtual utilizando o Centro de segurança do Azure

Centro de segurança do Azure pode ajudar a obter visibilidade para o recurso do Azure práticas de segurança. Centro de segurança oferece monitorização de segurança integrada. -Pode detetar ameaças que caso contrário podem passar despercebidas. Neste tutorial, pode obter informações sobre o Centro de segurança do Azure e como:
 
> [!div class="checklist"]
> * Configurar a recolha de dados
> * Configurar políticas de segurança
> * Ver e corrigir problemas de estado de funcionamento de configuração
> * Reveja as ameaças detetadas  

## <a name="security-center-overview"></a>Descrição geral do Centro de segurança

Centro de segurança identifica potenciais problemas de configuração de máquina virtual (VM) e direcionados ameaças de segurança. Estes podem incluir as VMs que estão em falta grupos de segurança de rede, os discos não encriptados e ataques de protocolo RDP (Remote Desktop Protocol) de força bruta. informações de Olá são mostradas no dashboard do Centro de segurança de Olá em gráficos de fácil leitura.

tooaccess Olá dashboard do Centro de segurança, no portal do Azure, no menu de Olá, selecione de Olá **Centro de segurança**. No dashboard de Olá, pode ver o estado de funcionamento de segurança de Olá do seu ambiente do Azure, encontrar uma contagem de recomendações atuais e ver Olá estado atual de alertas de ameaça. Pode expandir cada toosee de alto nível gráfico mais detalhes.

![Dashboard do Centro de segurança](./media/tutorial-azure-security/asc-dash.png)

Centro de segurança vai mais além recomendações tooprovide de deteção de dados para problemas que Deteta. Por exemplo, se uma VM foi implementada sem um grupo de segurança de rede ligado, o Centro de segurança apresenta uma recomendação, com passos de remediação que pode efetuar. Obter a remediação automática sem sair contexto Olá do Centro de segurança.  

![Recomendações](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>Configurar a recolha de dados

Antes de poder obter visibilidade para configurações de segurança VM, terá de tooset configurar recolha de dados do Centro de segurança. Isto envolve a ativação da recolha de dados e criar toohold recolhido dados de conta de armazenamento do Azure. 

1. No dashboard do Centro de segurança de Olá, clique em **política de segurança**e, em seguida, selecione a sua subscrição. 
2. Para **recolha de dados**, selecione **no**.
3. Selecione uma conta de armazenamento, de toocreate **escolher uma conta de armazenamento**. Em seguida, selecione **OK**.
4. No Olá **política de segurança** painel, selecione **guardar**. 

agente de recolha de dados de centro de segurança de Olá é instalado em todas as VMs e começa a recolha de dados. 

## <a name="set-up-a-security-policy"></a>Configurar uma política de segurança

As políticas de segurança são itens de Olá toodefine utilizado para o qual o Centro de segurança recolhe dados e faz recomendações. Pode aplicar conjuntos toodifferent de políticas de segurança diferentes dos recursos do Azure. Embora por predefinição os recursos do Azure são avaliados em relação a todos os itens de política, pode desativar os itens de política individuais para todos os recursos do Azure ou para um grupo de recursos. Para obter informações aprofundadas sobre as políticas de segurança do Centro de segurança, consulte [definir políticas de segurança no Centro de segurança do Azure](../../security-center/security-center-policies.md). 

tooset configurar uma política de segurança para todos os recursos do Azure:

1. No dashboard do Centro de segurança de Olá, selecione **política de segurança**e, em seguida, selecione a sua subscrição.
2. Selecione **política de prevenção**.
3. Ativar ou desativar os itens de política que pretende que o tooapply tooall recursos do Azure.
4. Quando tiver terminado de selecionar as definições, selecione **OK**.
5. No Olá **política de segurança** painel, selecione **guardar**. 

tooset configurar uma política para um grupo de recursos específico:

1. No dashboard do Centro de segurança de Olá, selecione **política de segurança**e, em seguida, selecione um grupo de recursos.
2. Selecione **política de prevenção**.
3. Ativar ou desativar os itens de política que pretende que o grupo de recursos de toohello tooapply.
4. Em **HERANÇA**, selecione **Unique**.
5. Quando tiver terminado de selecionar as definições, selecione **OK**.
6. No Olá **política de segurança** painel, selecione **guardar**.  

Também pode desativar a recolha de dados para um grupo de recursos específico nesta página.

No seguinte exemplo de Olá, foi criada uma política exclusiva para um grupo de recursos denominado *myResoureGroup*. Nesta política, o disco de encriptação e web aplicação firewall recomendações estão desativadas.

![Exclusivo da política](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>Ver estado de funcionamento de configuração de VM

Depois de ter ativada a recolha de dados e definir uma política de segurança, o Centro de segurança começa tooprovide alertas e as recomendações. Como VMs implementadas, o agente de recolha de dados de Olá está instalado. Centro de segurança, em seguida, é preenchido com dados de Olá novas VMs. Para obter informações aprofundadas sobre o estado de funcionamento de configuração de VM, consulte [proteger as suas VMs no Centro de segurança](../../security-center/security-center-virtual-machine-recommendations.md). 

Como os dados são recolhidos, estado de funcionamento de recursos de Olá para cada VM e os recursos do Azure relacionados é agregado. informações de Olá são apresentadas um gráfico de fácil leitura. 

Estado de funcionamento de recursos tooview:

1.  No dashboard do Centro de segurança de Olá, sob **estado de funcionamento de segurança de recursos**, selecione **computação**. 
2.  No Olá **computação** painel, selecione **máquinas virtuais**. Esta vista fornece um resumo do Estado de configuração de Olá para todas as suas VMs.

![Estado de funcionamento de computação](./media/tutorial-azure-security/compute-health.png)

toosee todas as recomendações para uma VM, selecione Olá VM. Recomendações e remediação são abordadas mais detalhadamente na secção seguinte, Olá deste tutorial.

## <a name="remediate-configuration-issues"></a>Resolver problemas de configuração

Depois de centro de segurança começa toopopulate com dados de configuração, as recomendações são efetuadas com base na política de segurança de Olá que configurou. Por exemplo, se uma VM foi configurado sem um grupo de segurança de rede associados, uma recomendação é feita toocreate um. 

toosee uma lista de todas as recomendações: 

1. No dashboard do Centro de segurança de Olá, selecione **recomendações**.
2. Selecione uma recomendação específica. É apresentada uma lista de todos os recursos para o qual se aplica a recomendação de Olá.
3. tooapply uma recomendação, selecione um recurso específico. 
4. Siga as instruções de Olá para passos de remediação. 

Em muitos casos, o Centro de segurança fornece passos passíveis de ação pode demorar tooaddress uma recomendação sem sair do Centro de segurança. No seguinte exemplo de Olá, o Centro de segurança Deteta um grupo de segurança de rede que tenha uma regra de entrada sem restrições. Na página de recomendação Olá, pode selecionar Olá **editar regras de entrada** botão. Olá IU que é necessário toomodify Olá regra é apresentada. 

![Recomendações](./media/tutorial-azure-security/remediation.png)

Como são resolvidas as recomendações, são marcados como resolvido. 

## <a name="view-detected-threats"></a>Ver ameaças detetadas

Além disso tooresource recomendações de configuração, o Centro de segurança apresenta os alertas de deteção de ameaças. funcionalidade de alertas de segurança de Olá agrega os dados recolhidos a partir de cada VM, registos de rede do Azure e soluções de parceiros ligadas toodetect ameaças de segurança relativamente aos recursos do Azure. Para obter informações aprofundadas sobre as capacidades de deteção de ameaças do Centro de segurança, consulte [as capacidades de deteção do Centro de segurança do Azure](../../security-center/security-center-detection-capabilities.md).

funcionalidade de alertas de segurança de Olá requer o Centro de segurança de Olá preços toobe camada aumentada de *livres* demasiado*padrão*. 30 dias **avaliação gratuita** está disponível quando mover toothis escalão de preço superior. 

escalão de preço Olá toochange:  

1. No dashboard do Centro de segurança de Olá, clique em **política de segurança**e, em seguida, selecione a sua subscrição.
2. Selecione **escalão de preço**.
3. Selecione a camada novo Olá e, em seguida, selecione **selecione**.
4. No Olá **política de segurança** painel, selecione **guardar**. 

Depois de alterar o escalão de preço de Olá, o gráfico de alertas de segurança de Olá começa toopopulate como são detetadas ameaças de segurança.

![Alertas de segurança](./media/tutorial-azure-security/security-alerts.png)

Selecione uma alerta tooview informações. Por exemplo, pode ver uma descrição de ameaça Olá, hora da deteção Olá, todas as tentativas de ameaças e Olá remediação recomendada. No seguinte exemplo de Olá, foi detetado um ataque de força bruta RDP, com 294 tentativas falhadas de RDP. É fornecida uma resolução recomendada.

![Ataque RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, pode configurar o Centro de segurança do Azure e, em seguida, revisto VMs no Centro de segurança. Aprendeu a:

> [!div class="checklist"]
> * Configurar a recolha de dados
> * Configurar políticas de segurança
> * Ver e corrigir problemas de estado de funcionamento de configuração
> * Reveja as ameaças detetadas

Produzir toolearn tutorial seguinte de toohello mais informações sobre como criar um pipeline de CI/CD com Jenkins, GitHub e Docker.

> [!div class="nextstepaction"]
> [Criar a infraestrutura de CI/CD com Jenkins, GitHub e Docker](tutorial-jenkins-github-docker-cicd.md)

