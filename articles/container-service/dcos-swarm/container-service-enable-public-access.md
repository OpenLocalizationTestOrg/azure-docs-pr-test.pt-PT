---
title: "aplicação de contentor do DC/OS do aaaEnable acesso tooAzure | Microsoft Docs"
description: "Como público tooenable acedam a contentores de SO/tooDC no serviço de contentor do Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contentores, Microserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Ativar a aplicação de serviço de contentor do Azure de tooan acesso público
Qualquer contentor de DC/OS em Olá ACS [agrupamento de agentes públicos](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) é toohello automaticamente exposto à internet. Por predefinição, as portas **80**, **443**, **8080** estão abertas e qualquer contentor (público) está a escutar as portas estão acessíveis. Este artigo mostra como tooopen mais portas para as suas aplicações no serviço de contentor do Azure.

## <a name="open-a-port-portal"></a>Abrir uma porta (portal)
Em primeiro lugar, temos de porta de Olá tooopen que queremos.

1. Inicie sessão no portal de toohello.
2. Grupo de recursos de Olá localizar que implementou Olá serviço de contentor do Azure para.
3. Selecione o Balanceador de carga do agente de Olá (que é denominado semelhante demasiado**XXXX-agente-lb-XXXX**).
   
    ![Balanceador de carga do serviço de contentor do Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Clique em **sondas** e, em seguida, **adicionar**.
   
    ![Pesquisas de Balanceador de carga do serviço de contentor do Azure](./media/container-service-enable-public-access/add-probe.png)
5. Preencha o formulário de pesquisa de Olá e clique em **OK**.
   
   | Campo | Descrição |
   | --- | --- |
   | Nome |Um nome descritivo da sonda Olá. |
   | Porta |porta de Olá de Olá tootest de contentor. |
   | Caminho |(Quando no modo HTTP) Olá tooprobe de caminho relativo Web site. HTTPS não suportado. |
   | intervalo |Olá período de tempo entre sonda tenta, em segundos. |
   | Limiar de mau estado de funcionamento |Número de sonda consecutivas tentativas antes de considerar o contentor de Olá mau estado de funcionamento. |
6. Novamente na propriedades Olá Olá agente de Balanceador de carga, clique em **as regras de balanceamento de carga** e, em seguida, **adicionar**.
   
    ![Regras de Balanceador de carga de serviço de contentor do Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Preencha o formulário de Balanceador de carga Olá e clique em **OK**.
   
   | Campo | Descrição |
   | --- | --- |
   | Nome |Um nome descritivo Olá de Balanceador de carga. |
   | Porta |porta de entrada pública de Olá. |
   | Porta de back-end |Olá interno público a porta da Olá contentor tooroute tráfego. |
   | Conjunto back-end |contentores Olá neste conjunto estará destino Olá para este Balanceador de carga. |
   | Sonda |Olá toodetermine sonda utilizada se um destino na Olá **conjunto back-end** está em bom estado. |
   | Persistência da sessão |Determina como o tráfego de um cliente deve ser processado Olá enquanto estiver em curso sessão Olá.<br><br>**Nenhum**: os pedidos sucessivos de Olá mesmo cliente pode ser processado por qualquer contentor.<br>**Cliente IP**: Olá, os pedidos sucessivos de Olá mesmo IP de cliente são processadas pelo mesmo contentor.<br>**Cliente IP e protocolo**: Olá, os pedidos sucessivos de Olá mesma combinação de IP e protocolo de cliente são processadas pelo mesmo contentor. |
   | Tempo limite de inatividade |(Apenas TCP) Em minutos, Olá tookeep de tempo que um cliente TCP/HTTP abrir sem depender *ligação keep-alive* mensagens. |

## <a name="add-a-security-rule-portal"></a>Adicionar uma regra de segurança (portal)
Em seguida, temos tooadd uma regra de segurança que encaminha o tráfego da nossa porta aberta através da firewall Olá.

1. Inicie sessão no portal de toohello.
2. Grupo de recursos de Olá localizar que implementou Olá serviço de contentor do Azure para.
3. Selecione Olá **pública** grupo de segurança de rede do agente (que é denominado semelhante demasiado**XXXX-agente-público-nsg-XXXX**).
   
    ![Grupo de segurança de rede de serviço de contentor do Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. Selecione **regras de segurança de entrada** e, em seguida, **adicionar**.
   
    ![Regras de grupo de segurança de rede de serviço de contentor do Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Preencha tooallow de regra de firewall de Olá a porta pública e clique em **OK**.
   
   | Campo | Descrição |
   | --- | --- |
   | Nome |Um nome descritivo Olá da regra da firewall. |
   | Prioridade |Classificação de prioridade da regra de Olá. Olá Olá número Olá superior Olá prioridade inferior. |
   | Origem |Restringir Olá entrada IP endereço intervalo toobe permitido ou negado por esta regra. Utilize **qualquer** toonot especificar uma restrição. |
   | Serviço |Selecione um conjunto de serviços predefinidos que destina-se a esta regra de segurança. Caso contrário, utilize **personalizada** toocreate os seus próprios. |
   | Protocolo |Restringir o tráfego com base no **TCP** ou **UDP**. Utilize **qualquer** toonot especificar uma restrição. |
   | Intervalo de portas |Quando **serviço** é **personalizada**, especifica Olá intervalo de portas que esta regra afeta. Pode utilizar uma porta única, tal como **80**, ou como um intervalo **1024-1500**. |
   | Ação |Permitir ou negar o tráfego que cumpra os critérios de Olá. |

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre a diferença de Olá entre [públicos e privados agentes DC/OS](container-service-dcos-agents.md).

Leia mais informações sobre [gerir os contentores de DC/SO](container-service-mesos-marathon-ui.md).

