---
title: "aaaRespond toosecurity incidentes com o Centro de segurança do Azure | Microsoft Docs"
description: "Este documento explica como toouse segurança do Azure do Centro de para um cenário de resposta a incidentes."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 8af12f1c-4dce-4212-8ac4-170d4313492d
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: aaf50c0c7e774d03d517c3fd11686dbae48dd29b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-security-center-for-an-incident-response"></a>Utilizar o Centro de Segurança do Azure para resposta a incidentes
Muitas organizações Saiba como toorespond toosecurity incidentes apenas após a sofrer um ataque. os custos de tooreduce e danos, é importante toohave uma resposta a incidentes planear no local antes de um ataque ocorre. Pode utilizar o Centro de segurança do Azure em várias fases de uma resposta a incidentes.

## <a name="incident-response-planning"></a>Planeamento de resposta a incidentes
Um plano eficaz depende de três funções essenciais: ser capaz de tooprotect, detetar e responder toothreats. Proteção está prestes a impedir a incidentes, a deteção é sobre como identificar ameaças numa fase inicial e resposta sobre expulsar atacante Olá e impactos de Olá toomitigate sistemas de uma violação de restauro.

Este artigo irá utilizar fases de resposta a incidentes de segurança de Olá de Olá [Microsoft Azure Security Response no Olá nuvem](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678) artigo, conforme mostrado no Olá diagrama a seguir:

![Ciclo de vida de resposta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig1.png)

Pode utilizar o Centro de segurança durante as fases de detetar, avaliação e diagnosticar Olá. Seguem-se exemplos de como o Centro de segurança podem ser úteis durante três fases de resposta a incidentes inicial Olá:

* **Detetar**: Reveja indicação primeiro Olá uma investigação de eventos.
  * Exemplo: Reveja Olá inicial verificação que um alerta de segurança de alta prioridade foi gerado no dashboard do Centro de segurança de Olá.
* **Avaliar**: efetuar Olá avaliação inicial tooobtain mais informações sobre a atividade suspeita Olá.
  * Exemplo: obter mais informações sobre o alerta de segurança de Olá.
* **Diagnosticar**: realize uma investigação técnica e identifique as estratégias de contenção, atenuação e solução.
  * Exemplo: Siga os passos de remediação de Olá descritos pelo centro de segurança nesse alerta específico de segurança.

cenário de Olá que se segue mostra como o Centro de segurança tooleverage durante Olá detetar, avaliação e diagnosticar/respondeu fases de um incidente de segurança. No Centro de Segurança, um [incidente de segurança](security-center-incident.md) é uma agregação de todos os alertas de um recurso que são alinhados com padrões de [cadeia de eliminação](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/). Os incidentes surgem no Olá [alertas de segurança](security-center-managing-and-responding-alerts.md) mosaico e o painel. Um incidente revela a lista de Olá de alertas relacionados, que permite-lhe tooobtain mais informações sobre cada ocorrência. Centro de segurança também apresenta autónomo alertas de segurança que também podem ser utilizado tootrack para baixo de uma atividade suspeita.

## <a name="scenario"></a>Cenário
Contoso migrada recentemente algumas das respetivos tooAzure de recursos no local, incluindo alguns baseado em máquina virtual cargas de trabalho de linha de negócio e bases de dados SQL. De momento, a CSIRT (Equipa de Resposta a Incidentes de Segurança Informática) da Contoso tem dificuldade em investigar problemas de segurança porque as informações de segurança não estão integradas com as respetivas ferramentas atuais de resposta a incidentes. Esta falta de integração apresenta um problema durante a fase de detetar (demasiados falsos positivos) de Olá, bem como durante Olá avaliação e diagnosticar fases. Como parte da migração, decidiu tooopt para o Centro de segurança toohelp-endereços este problema.

Olá primeira fase da migração concluída depois de serem integrado todos os recursos e resolvido todas as recomendações de segurança de Olá do Centro de segurança. Contoso CSIRT é Olá focal ponto para lidar com incidentes de segurança do computador. equipa de Olá é composta por um grupo de pessoas com responsabilidades para lidar com qualquer incidente de segurança. os membros da equipa Olá claramente definiu deveres tooensure que nenhum área da resposta for deixada detetados pelo.

Objetivo Olá neste cenário, vamos toofocus nas funções de Olá de Olá pessoas fictícias que fazem parte da Contoso CSIRT os seguintes:

![Ciclo de vida de resposta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig2.png)

A Constança está nas operações de segurança. As responsabilidades dela incluem:

* Monitorizar e responder a ameaças toosecurity em torno do relógio de Olá.
* Em constante crescendo toohello proprietário da carga de trabalho de nuvem ou analista de segurança conforme necessário.

Samuel é um analista de segurança e as suas responsabilidades incluem:

* Investigar ataques.
* Resolver alertas.
* Trabalhar com a carga de trabalho proprietários toodetermine e aplicar mitigações.

Como pode ver, Judy e Sam tenham responsabilidades de diferentes, e tem funcionam em conjunto tooshare informações de centro de segurança.

## <a name="recommended-solution"></a>Solução recomendada
Uma vez que Judy e Sam têm diferentes funções, podem utilizar diferentes áreas de informações relevantes do Centro de segurança tooobtain para as respetivas atividades diárias. A Constança vai utilizar **Alertas de segurança** como parte da respetiva monitorização diária.

![Alertas de segurança](./media/security-center-incident-response/security-center-incident-response-fig3.png)

Judy irá utilizar alertas de segurança durante Olá detetar e as fases de avaliação. Após a Judy avaliação inicial Olá, ela pode escalar Olá problema tooSam se for necessária a investigação adicional. Neste momento, Sam irá utilizar as informações de Olá fornecido pelo centro de segurança, por vezes, juntamente com outras origens de dados, toomove toohello Diagnostique fase.

## <a name="how-tooimplement-this-solution"></a>Como tooimplement esta solução
toosee como pretende utilizar o Centro de segurança do Azure num cenário de resposta a incidentes, vamos seguir os passos de Judy nas fases de detetar e avaliação Olá e, em seguida, ver o que faz Sam problema de Olá toodiagnose.

### <a name="detect-and-assess-incident-response-stages"></a>Diagnosticar e Avaliar fases de resposta a incidentes
Judy com sessão iniciada toohello portal do Azure e está a trabalhar na consola do Centro de segurança de Olá. Como parte do respetivo diariamente monitorização de atividades, ela iniciado rever segurança alta prioridade Olá de alertas, efetuando os seguintes passos:

1. Clique em Olá **alertas de segurança** Olá mosaico e acesso **alertas de segurança** painel.
    ![Painel Alerta de segurança](./media/security-center-incident-response/security-center-incident-response-fig4.png)

   > [!NOTE]
   > Objetivo Olá neste cenário, Judy é contínuo tooperform uma avaliação de alerta de atividade de SQL malicioso Olá, como mostrado na Olá precedente figura.
   >
   >
2. Clique em Olá **atividade maliciosa SQL** alertas e rever recursos Olá atacado Olá **atividade maliciosa SQL** painel: ![detalhes do incidente](./media/security-center-incident-response/security-center-incident-response-fig5.png)

    Neste painel, Judy pode anota sobre recursos de Olá atacado, como número de vezes que este ataque foi efetuada, e quando foi detetado.
3. Clique em Olá **atacados recursos** tooobtain mais informações sobre este ataque.

Depois de ler a descrição de Olá, Judy é convinced que não se trata de um falsos positivos e que ela deve escalar tooSam este cenário.

### <a name="diagnose-incident-response-stage"></a>Diagnosticar a fase de resposta a incidentes
SAM recebe caso Olá de Judy e começa a rever os passos de remediação de Olá sugerido do Centro de segurança.

![Ciclo de vida de resposta a incidentes](./media/security-center-incident-response/security-center-incident-response-fig6.png)

### <a name="additional-resources"></a>Recursos adicionais
equipa de resposta a incidentes de Olá também pode tirar partido de Olá [Power BI do Centro de segurança](security-center-powerbi.md) capacidade toosee os diferentes tipos de relatórios. Estes relatórios podem ajudá-los durante a toovisualize de investigação adicional, analisar e filtrar recomendações e alertas de segurança. Para as empresas que utilizam as suas informações de segurança e a solução de gestão (SIEM) de evento durante o processo de investigação Olá, estes também podem [integrar o Centro de segurança com a respetiva solução](security-center-integrating-alerts-with-log-integration.md). Também pode integrar os registos de auditoria do Azure e eventos de segurança de máquina virtual (VM) utilizando Olá [ferramenta de registo do Azure de integração](https://blogs.msdn.microsoft.com/azuresecurity/2016/07/21/microsoft-azure-log-integration-preview/). um ataque tooinvestigate, pode utilizar estas informações em conjunto com as informações de Olá que fornece o Centro de segurança.

## <a name="conclusion"></a>Conclusão
Reuni uma equipa antes de ocorre um incidente é muito importante tooyour organização e positivamente influenciarão a forma como os incidentes são processados. Olá ferramentas direita toomonitor recursos podem ajudar a tooremediate de passos exatos tootake esta equipa um incidente de segurança. Centro de segurança [as capacidades de deteção](security-center-detection-capabilities.md) pode ajudar a incidentes de toosecurity TI tooquickly responder e remediar problemas de segurança.
