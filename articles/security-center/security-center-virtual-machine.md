---
title: "aaaAzure Centro de segurança e Virtual Machines do Azure | Microsoft Docs"
description: "Este documento ajuda-o a toounderstand como o Centro de segurança do Azure pode salvaguardar a máquinas virtuais do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Centro de Segurança do Azure e Máquinas Virtuais do Azure
[Centro de segurança do Azure](https://azure.microsoft.com/services/security-center/) ajuda-o a evitar, detetar e responder toothreats. Fornece gestão de políticas e monitorização de segurança integrada nas suas subscrições do Azure, ajuda a detetar ameaças que caso contrário podem passar despercebidas e funciona com um ecossistema abrangente de soluções de segurança.

Este artigo mostra como o Centro de Segurança o pode ajudar a proteger as suas Máquinas Virtuais do Azure (VM).

## <a name="why-use-security-center"></a>Porquê utilizar o Centro de Segurança?
O Centro de Segurança ajuda-o a salvaguardar os dados da máquina virtual no Azure, oferecendo visibilidade sobre as definições de segurança da sua máquina virtual. Quando o Centro de segurança salvaguarda as suas VMs, Olá seguintes funcionalidades estarão disponível:

* As definições de segurança do sistema operativo (SO) com Olá recomendada as regras de configuração
* Segurança do sistema e atualizações críticas em falta
* Recomendações do Endpoint protection
* Validação de encriptação do disco
* Avaliação e remediação de vulnerabilidades
* Deteção de ameaças

Além disso toohelping proteger as suas VMs do Azure, o Centro de segurança também fornece monitorização de segurança e gestão de serviços em nuvem, serviços de aplicações, redes virtuais e muito mais. 

> [!NOTE]
> Consulte [tooAzure de introdução do Centro de segurança](security-center-intro.md) toolearn mais acerca do Centro de segurança do Azure.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
tooget começar a utilizar o Centro de segurança do Azure, irá precisar de tooknow e considere Olá seguinte:

* Tem de ter um tooMicrosoft de subscrição do Azure. Consulte [Security Center Pricing (Preços do Centro de Segurança)](https://azure.microsoft.com/pricing/details/security-center/), para obter mais informações sobre as camadas gratuitas e standard do Centro de Segurança.
* Planear a adoção do Centro de segurança, consulte [guia de operações e planeamento do Centro de segurança do Azure](security-center-planning-and-operations-guide.md) toolearn mais sobre as considerações de operações e planeamento.
* Para informações sobre a suportabilidade do sistema operativo, consulte [Azure Security Center frequently asked questions (FAQ) (Perguntas mais frequentes do Centro de Segurança do Azure (FAQ))](security-center-faq.md). 

## <a name="set-security-policy"></a>Definir política de segurança
Toobe necessidades recolha de dados ativada para que o Centro de segurança do Azure pode recolher informações de Olá tem tooprovide recomendações e alertas que são gerados com base na política de segurança de Olá que configura. A figura Olá abaixo, pode ver que **recolha de dados** foi ativado **no**.

Uma política de segurança define o conjunto de Olá de controlos que são recomendados para recursos dentro Olá especificado subscrição ou grupo de recursos. Antes de ativar a política de segurança, tem de ter ativada a recolha de dados, o Centro de segurança recolhe dados das suas máquinas virtuais na ordem tooassess respetivo estado de segurança, fornecer recomendações de segurança e alertá-lo toothreats. No Centro de segurança, é possível definir políticas para as suas subscrições do Azure ou os grupos de recursos de acordo com as necessidades de segurança tooyour da empresa e do tipo de Olá de aplicações ou sensibilidade dos dados de Olá em cada subscrição. 

![Política de segurança](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> mais informações sobre cada toolearn **política de prevenção** disponível, consulte [definir políticas de segurança](security-center-policies.md) artigo.
> 
> 

## <a name="manage-security-recommendations"></a>Gerir recomendações de segurança
Centro de segurança analisa o estado de segurança de Olá dos seus recursos Azure. Quando o Centro de Segurança identifica potenciais vulnerabilidades de segurança, cria recomendações. recomendações de Olá ajudá-lo através do processo de Olá de configurar os controlos de Olá necessário.

Depois de definir uma política de segurança, o Centro de segurança analisa o estado de segurança de Olá dos seus recursos tooidentify potenciais vulnerabilidades. recomendações de Olá são apresentadas num formato de tabela em que cada linha representa uma recomendação específica. tabela de Olá abaixo fornece alguns exemplos das recomendações para as VMs do Azure e o que cada um irá fazer se aplicá-lo. Quando seleciona uma recomendação, receberá informações que mostra como tooimplement Olá recomendação no Centro de segurança.

| Recomendação | Descrição |
| --- | --- |
| [Ativar a recolha de dados para subscrições](security-center-enable-data-collection.md) |Recomenda-se que ative a recolha de dados na política de segurança de Olá para cada uma das suas subscrições e todas as máquinas virtuais (VMs) nas suas subscrições. |
| [Remediar vulnerabilidades do SO](security-center-remediate-os-vulnerabilities.md) |Recomenda que alinhar as configurações de SO com Olá recomendada as regras de configuração, por exemplo, não permitem toobe de palavras-passe guardada. |
| [Aplicar atualizações do sistema](security-center-apply-system-updates.md) |Recomenda-se de que implemente tooVMs atualizações críticas e de segurança de sistema em falta. |
| [Reiniciar após atualizações do sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomenda-se de que reiniciar um processo de Olá toocomplete VM de aplicar atualizações do sistema. |
| [Instalar o Endpoint Protection](security-center-install-endpoint-protection.md) |Recomenda-se de que aprovisionar tooVMs de programas antimalware (apenas para VMs do Windows). |
| [Resolver alertas de estado de funcionamento do Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomenda-se que resolva falhas de proteção do ponto final. |
| [Ativar o Agente de VM](security-center-enable-vm-agent.md) |Permite toosee que necessite de VMs Olá agente da VM. Olá agente da VM tem de ser instalado em VMs no patch de tooprovision ordem análise, a linha de base de análise e programas antimalware. Olá agente VM está instalado por predefinição para as VMs que são implementadas a partir de Olá Azure Marketplace. artigo de Olá [extensões – parte 2 e o agente da VM](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fornece informações sobre como tooinstall Olá agente da VM. |
| [Aplicar encriptação de discos](security-center-apply-disk-encryption.md) |Recomenda-se que encripte os discos da VM com o Azure Disk Encryption (VMs Windows e Linux). Encriptação é recomendada para Olá SO e volumes de dados na VM. |
| [Avaliação de vulnerabilidades não instalada](security-center-vulnerability-assessment-recommendations.md) |Recomenda-se de que instala uma solução de avaliação de vulnerabilidades na sua VM. |
| [Remediar vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Permite-lhe a vulnerabilidades de sistema e de aplicações do toosee detetadas pela solução de avaliação de vulnerabilidade de Olá instalada na VM. |

> [!NOTE]
> toolearn mais informações sobre as recomendações, consulte [gerir recomendações de segurança](security-center-recommendations.md) artigo.
> 
> 

## <a name="monitor-security-health"></a>Monitorizar o estado de funcionamento da segurança
Depois de ativar [políticas de segurança](security-center-policies.md) para recursos de uma subscrição, o Centro de segurança irá analisar a segurança de Olá dos seus recursos tooidentify potenciais vulnerabilidades.  Pode ver o estado de segurança de Olá dos seus recursos, juntamente com quaisquer problemas na Olá **estado de funcionamento de segurança de recursos** painel. Ao clicar em **máquinas virtuais** no Olá **segurança de recursos** mosaico estado de funcionamento, Olá **máquinas virtuais** painel será aberto com recomendações para as suas VMs. 

![Estado de funcionamento da segurança](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Gerir e responder a alertas de toosecurity
Centro de segurança automaticamente recolhe, analisa e integra-se os dados de registo de recursos do Azure, rede Olá e soluções de parceiros ligadas (por exemplo, o ponto final e firewall soluções de proteção), toodetect de ameaças reais e reduzir os falsos positivos. Ao tirar partido de uma agregação diversificada de [as capacidades de deteção](security-center-detection-capabilities.md), o Centro de segurança é capaz de toogenerate definida segurança alertas toohelp investigar o problema de Olá rapidamente e fornecer recomendações como tooremediate ataques possíveis.

![Alertas de segurança](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Selecione um toolearn de alerta de segurança mais informações sobre eventos de Olá que acionou o alerta Olá e o que, se aplicável, os passos precisam de tootake tooremediate um ataque. Os alertas de segurança estão agrupados por [tipo](security-center-alerts-type.md) e data.

## <a name="see-also"></a>Consultar também
toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e respondeu.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.

