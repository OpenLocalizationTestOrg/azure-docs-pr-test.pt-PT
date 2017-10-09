---
title: aaaView e gerir alertas do Microsoft Azure StorSimple Virtual matriz | Microsoft Docs
description: "Descreve as condições de alerta de matriz Virtual StorSimple e gravidade, e como toouse Olá StorSimple Manager service toomanage alertas."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 97ee25a1-0ec3-4883-9a0a-54b722598462
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0fb5b1b9064f33df1d8fa7ace45f0d72b0a1622
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-alerts-for-hello-storsimple-virtual-array"></a>Utilize o Gestor de dispositivos StorSimple toomanage alertas para Olá matriz Virtual StorSimple

## <a name="overview"></a>Descrição geral

funcionalidade de alertas de Olá no Olá serviço Gestor de dispositivos do StorSimple é uma forma para tooreview e desmarque alertas relacionados tooStorSimple Virtual matrizes de forma em tempo real. Pode utilizar alertas Olá no Olá **resumo serviço** painel toocentrally monitorizar problemas de estado de funcionamento de Olá das suas matrizes de Virtual StorSimple e Olá solução global do Microsoft Azure StorSimple.

Este tutorial descreve como tooconfigure as notificações de alerta, condições comuns de alerta, níveis de gravidade do alerta e como tooview e controlar alertas. Além disso, inclui referência rápida alerta tabelas, que permitem tooquickly localizar um alerta específico e respondem corretamente.

![Página de alertas](./media/storsimple-virtual-array-manage-alerts/alerts1.png)

## <a name="configure-alert-settings"></a>Configurar definições de alerta

Pode escolher se pretende toobe notificado por correio eletrónico de condições de alerta de Olá para cada uma das suas matrizes de Virtual StorSimple. Além disso, pode identificar outros destinatários de notificação de alertas, introduzindo os respetivos endereços de e-mail no Olá **destinatários de e-mail adicionais** caixa, separada por ponto e vírgula.

> [!NOTE]
> Pode introduzir um máximo de 20 endereços de e-mail por matriz virtual.


Depois de ativar a notificação por e-mail para uma matriz de virtual, os membros da lista de notificação de Olá irão receber uma mensagem de e-mail, ocorre um alerta crítico de cada vez. mensagens Hello serão enviadas  *storsimple-alerts-noreply@mail.windowsazure.com*  e irá descrever a condição de alerta de Olá. Podem clicar destinatários **Unsubscribe** tooremove próprios da lista de notificação de correio eletrónico Olá.

#### <a name="tooenable-email-notification-for-alerts"></a>tooenable notificação de correio eletrónico para alertas

1. Aceda tooyour Gestor de dispositivos do StorSimple, serviço e no Olá **gestão** secção, selecione e clique em **dispositivos**. Na lista de Olá dos dispositivos apresentada, selecione e clique em seu dispositivo.
   
    ![definições de alerta](./media/storsimple-virtual-array-manage-alerts/alerts2.png)
2. Esta ação abre segurança Olá **definições** painel. No Olá **definições do dispositivo** secção, selecione **geral**. Esta ação abre segurança Olá **definições gerais** painel.
   
    ![Configuração de notificação de alertas](./media/storsimple-virtual-array-manage-alerts/alerts4.png)
3. No Olá **definições gerais** painel, vá demasiado**as definições de alertas** secção e definir Olá seguinte:
   
   1. No Olá **ativar notificação de correio eletrónico** campo, selecione **Sim**.
   2. No Olá **administradores de serviço de E-Mail** campo, selecione **Sim** se pretende que o administrador de serviços de Olá toohave e todos os coadministradores recebem notificações de alerta de Olá.
   3. No Olá **destinatários de e-mail adicionais** campo, introduza os endereços de e-mail Olá todos os outros destinatários que devem receber notificações de alerta de Olá. Introduza os nomes no formato de Olá  *someone@somewhere.com* . Utilize endereços de correio eletrónico de Olá de tooseparate ponto e vírgula. Pode configurar um máximo de 20 endereços de e-mail por dispositivo virtual.
      
       ![Configuração de notificação de alertas](./media/storsimple-virtual-array-manage-alerts/alerts6.png)
   4. toosend uma notificação de correio eletrónico de teste, clique em **enviar e-mail de teste**. Olá serviço StorSimple Manager de dispositivos irá apresentar mensagens de estado, que reencaminha a notificação de teste de Olá.
      
       ![Alertas de e-mail de notificação enviado de teste](./media/storsimple-virtual-array-manage-alerts/alerts7.png)
      
      > [!NOTE]
      > Se testar Olá não é possível enviar mensagem de notificação, serviço de Gestor de dispositivos do StorSimple Olá apresentará uma mensagem adequada. Clique em **OK**, aguarde alguns minutos e, em seguida, repita toosend a mensagem de notificação de teste.
      > 
      > 
   5. Na Olá parte inferior da página Olá, clique em **guardar** toosave a configuração. Quando lhe for pedida a confirmação, clique em **Sim**.
      
      ![Alertas de e-mail de notificação enviado de teste](./media/storsimple-virtual-array-manage-alerts/alerts10.png)

## <a name="common-alert-conditions"></a>Condições de alerta comuns

A matriz de Virtual StorSimple gera alertas resposta tooa diversas condições. Olá, são tipos de condições alertas mais comuns Olá:

* **Problemas de conectividade** – estes alertas ocorrem quando não existe qualquer dificuldade na transferência de dados. Podem ocorrer problemas de comunicação durante a transferência de dados tooand da conta de armazenamento do Azure Olá ou atraso toolack da conetividade entre dispositivos virtuais Olá e o serviço do Gestor de dispositivos do StorSimple de Olá. Problemas de comunicação estão alguns dos toofix hardest Olá porque existem muitos pontos de falha. Deve sempre primeiro certifique-se de que as acesso à Internet e conectividade de rede estão disponíveis antes de continuar em toomore avançadas de resolução de problemas. Para informações sobre as portas e as definições da firewall, aceda demasiado[requisitos de sistema de matriz Virtual StorSimple](storsimple-ova-system-requirements.md). Para obter ajuda na resolução de problemas, visite demasiado[resolver problemas com o cmdlet Olá Test-Connection](storsimple-troubleshoot-deployment.md).
* **Problemas de desempenho** – estes alertas são causados quando o sistema não se encontra satisfatória, tal como quando está sob uma carga elevada.

Além disso, poderá ver toosecurity relacionados alertas, atualizações ou falhas de tarefas.

## <a name="alert-severity-levels"></a>Níveis de gravidade do alerta

Os alertas têm níveis de gravidade de diferente, consoante o impacto de Olá que Olá situação alerta irá ter e Olá necessidade de um alerta de toohello de resposta. níveis de gravidade Olá são:

* **Crítico** – este alerta está numa condição de tooa de resposta que está a afetar o desempenho de êxito de Olá do seu sistema. A ação é necessária tooensure que o serviço do StorSimple Olá não é interrompido.
* **Aviso** – esta condição pode ficar crítica, se não resolvido. Deve investigar a situação Olá e tomar qualquer problema de Olá tooclear ação necessária.
* **Informações** – este alerta contém informações que podem ser úteis para controlar e gerir o sistema.

## <a name="view-and-track-alerts"></a>Ver e monitorizar alertas

painel Resumo de serviço do Gestor de dispositivos do StorSimple de Olá fornece-lhe uma leitura rápida no número de Olá de alertas nos seus dispositivos virtuais, dispostas por nível de gravidade.

![Dashboard de alertas](./media/storsimple-virtual-array-manage-alerts/alerts14.png)

Clique em Olá de tooopen nível de gravidade Olá **alertas** painel. resultados de Olá incluem apenas os alertas de Olá que correspondem a esse nível de gravidade.

![Tipo de tooalert de âmbito do relatório de alertas](./media/storsimple-virtual-array-manage-alerts/alerts15.png)

Clique num alerta Olá lista tooget adicionais os detalhes do alerta Olá, incluindo Olá hora da última foi comunicada um alerta de Olá, número de Olá de ocorrências de alerta de Olá no dispositivo Olá e Olá alerta de Olá tooresolve de ação recomendada.

![Lista de alertas e os detalhes](./media/storsimple-virtual-array-manage-alerts/alerts16.png)

Pode copiar o ficheiro de texto do Olá detalhes do alerta tooa se precisar de toosend Olá informações tooMicrosoft suporte. Depois de ter seguido recomendação Olá e resolvido Olá condição de alerta no local, deve limpar o alerta de Olá da lista de Olá. Selecione o alerta de Olá Olá lista e, em seguida, clique em **limpar**. tooclear vários alertas, selecionadas de cada alerta, clique em qualquer coluna exceto Olá **alerta** coluna e, em seguida, clique em **limpar** depois de selecionar todos os Olá toobe alertas desmarcada.

Ao clicar em **limpar**, terá de comentários do Olá oportunidade tooprovide sobre alerta Olá e passos de Olá, que demorou tooresolve Olá problema. 

![comentários do alerta](./media/storsimple-virtual-array-manage-alerts/alerts17.png)

Alguns eventos serão limpo pelo sistema Olá se outro evento é acionado com novas informações. 

## <a name="sort-and-review-alerts"></a>A ordenação e rever alertas

Olá **alertas** painel pode apresentar too250 alertas de cópias de segurança. Se ter excedido esse número de alertas, nem todos os alertas serão apresentados na vista de predefinição Olá. Pode combinar Olá toocustomize campos os alertas são apresentados a seguir:

* **Estado** – pode apresentar um **Active Directory** ou **Cleared** alertas. Alertas ativos ainda estão a ser acionados no seu sistema, enquanto a alertas desmarcadas foram ou eliminadas manualmente por um administrador ou de forma programática porque o sistema de Olá atualizado a condição de alerta de Olá com novas informações.
* **Gravidade** – pode apresentar os alertas de todos os níveis de gravidade (crítico, aviso, informações) ou apenas uma determinada gravidade, tais como alertas críticos apenas.
* **Origem** – pode apresentar os alertas de todas as origens ou limitar Olá toothose de alertas do serviço de Olá ou um ou Olá todos os dispositivos virtuais.
* **Intervalo de tempo** – especificando Olá **de** e **para** as datas e carimbos de data / hora, pode ver alertas durante Olá período de tempo que está interessado em.

## <a name="alerts-quick-reference"></a>Referência rápida de alertas

Olá tabelas a seguir lista alguns dos alertas do Olá StorSimple que poderá encontrar, bem como informações adicionais e as recomendações, quando disponíveis. Alertas de matriz Virtual StorSimple enquadram-se um dos Olá seguintes categorias:

* [Alertas de conectividade de nuvem](#cloud-connectivity-alerts)
* [Alertas de configuração](#configuration-alerts)
* [Alertas de falha da tarefa](#job-failure-alerts)
* [Alertas de desempenho](#performance-alerts)
* [Alertas de segurança](#security-alerts)
* [Atualizar alertas](#update-alerts)

### <a name="cloud-connectivity-alerts"></a>Alertas de conectividade de nuvem

| Texto de alerta | Evento | Obter mais informações / as ações recomendadas |
|:--- |:--- |:--- |
| Dispositivo  *<device name>*  é não ligado toohello nuvem. |Olá com o nome de dispositivo não é possível ligar toohello nuvem. |Não foi possível ligar o toohello nuvem. Isto pode dever-se devido tooone seguinte Olá:<ul><li>Pode existir um problema com as definições de rede de Olá no seu dispositivo.</li><li>Pode existir um problema com as credenciais de conta de armazenamento Olá.</li></ul>Para mais informações sobre como resolver problemas de conectividade, visite toohello [IU da web do local](storsimple-ova-web-ui-admin.md) do dispositivo Olá. |

### <a name="configuration-alerts"></a>Alertas de configuração

| Texto de alerta | Evento | Obter mais informações / as ações recomendadas |
|:--- |:--- |:--- |
| Configuração do dispositivo virtual no local não suportada. |Desempenho lento. |configuração atual Olá poderão resultar numa degradação do desempenho. Certifique-se de que o servidor satisfaz os requisitos mínimos de configuração de Olá. Para mais informações, visite demasiado[StorSimple Virtual matriz requisitos](storsimple-ova-system-requirements.md). |
| Estiver a ficar sem espaço em disco aprovisionado <*nome de dispositivo*>. |Aviso de espaço em disco. |Tiver pouco espaço em disco aprovisionado. toofree segurança espaço, considere mover as cargas de trabalho tooanother volume ou partilha ou eliminação de dados. |

### <a name="job-failure-alerts"></a>Alertas de falha da tarefa

| Texto de alerta | Evento | Obter mais informações / as ações recomendadas |
|:--- |:--- |:--- |
| Cópia de segurança de <*nome de dispositivo*> não foi possível concluir. |Falha da tarefa de cópia de segurança. |Não foi possível criar uma cópia de segurança. Considere um dos seguintes Olá:<ul><li>Problemas de conectividade podem estar a impedir operação de cópia de segurança de Olá a conclusão com êxito. Certifique-se de que existem não existem problemas de conectividade. Para mais informações sobre como resolver problemas de conectividade, visite toohello [IU da web do local](storsimple-ova-web-ui-admin.md) para o dispositivo virtual.</li><li>Atingiu o limite de armazenamento disponível Olá. toofree segurança espaço, considere eliminar quaisquer cópias de segurança que já não são necessárias.</li></ul> Resolver problemas de Olá, limpar o alerta de Olá e repita a operação de Olá. |
| Clonar de <*nome de dispositivo*> não foi possível concluir. |Falha da tarefa de clone. |Não foi possível criar um clone. Considere um dos seguintes Olá:<ul><li>A lista de cópia de segurança pode não ser válida. Atualize Olá lista tooverify ainda é válida.</li><li>Problemas de conectividade podem estar a impedir Olá clone conclusão da operação com êxito. Certifique-se de que existem não existem problemas de conectividade.</li><li>Atingiu o limite de armazenamento disponível Olá. toofree segurança espaço, considere eliminar quaisquer cópias de segurança que já não são necessárias.</li></ul>Resolver problemas de Olá, limpar o alerta de Olá e repita a operação de Olá. |

### <a name="performance-alerts"></a>Alertas de desempenho

| Texto de alerta | Evento | Obter mais informações / as ações recomendadas |
|:--- |:--- |:--- |
| Sofram atrasos inesperados na transferência de dados. |Transferência de dados lenta. |Limitação erros ocorrem quando exceder os objetivos de escalabilidade Olá de um serviço de armazenamento. serviço de armazenamento Olá não esta tooensure que nenhum cliente único ou inquilino pode utilizar o serviço de Olá em despesa Olá de terceiros. Para mais informações sobre como resolver problemas da sua conta do storage do Azure, visite demasiado[monitorizar, diagnosticar e resolver problemas de armazenamento do Microsoft Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md). |
| Está a executar a baixa no local de reserva de espaço em disco no <*nome de dispositivo*>. |Tempo de resposta lento. |total de 10% do Olá tamanho aprovisionado para <*nome de dispositivo*> está reservado Olá dispositivo local e é agora pouco em Olá reservado espaço. carga de trabalho Olá no <*nome de dispositivo*> está a gerar uma maior taxa de volume de alterações ou pode ter migrada recentemente uma grande quantidade de dados. Isto pode resultar num desempenho reduzido. Considere uma das Olá seguintes ações tooresolve isto:<ul><li>Aumente Olá nuvem largura de banda toothis o dispositivo.</li><li>Reduzir ou move cargas de trabalho tooanother volume ou partilha.</li></ul> |

### <a name="security-alerts"></a>Alertas de segurança

| Texto de alerta | Evento | Obter mais informações / as ações recomendadas |
|:--- |:--- |:--- |
| Palavra-passe para <*nome de dispositivo*> irá expirar dentro de <*número*> dias. |Aviso de palavra-passe. |A palavra-passe expira em < número < dias. Considere alterar a palavra-passe. Para mais informações, visite demasiado[alterar Olá matriz Virtual StorSimple dispositivo administrador palavra-passe](storsimple-virtual-array-change-device-admin-password.md). |

### <a name="update-alerts"></a>Atualizar alertas

| Texto de alerta | Evento | Obter mais informações / as ações recomendadas |
|:--- |:--- |:--- |
| Novas atualizações estão disponíveis para o seu dispositivo. |Estão disponíveis atualizações toohello matriz Virtual StorSimple. |Poderá instalar novas atualizações a partir de Olá **manutenção** página. |
| Não foi possível verificar novas atualizações em <*nome de dispositivo*>. |Falha de atualização. |Ocorreu um erro ao instalar novas atualizações. Pode instalar manualmente Olá atualizações. Se Olá problema persistir, contacte [Microsoft Support](storsimple-contact-microsoft-support.md). |

## <a name="next-steps"></a>Passos seguintes

* [Saiba mais sobre Olá matriz Virtual StorSimple](storsimple-ova-overview.md).

