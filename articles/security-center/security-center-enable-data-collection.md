---
title: "recolha de dados de aaaEnable no Centro de segurança do Azure | Microsoft Docs"
description: " Saiba como tooenable recolha de dados no Centro de segurança do Azure. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Ativar a recolha de dados no Centro de segurança do Azure

> [!NOTE]
> A partir da precoce de Junho de 2017, o Centro de segurança irá utilizar Olá Microsoft Monitoring Agent toocollect e armazenar dados. toolearn mais, consulte [migração de plataforma de centro de segurança do Azure](security-center-platform-migration.md). informações de Olá neste artigo representam a funcionalidade do Centro de segurança após a transição toohello Microsoft Monitoring Agent.
>
>

Centro de segurança recolhe dados do seu tooassess de máquinas virtuais (VMs) respetivo estado de segurança, fornecer recomendações de segurança e alertá-lo toothreats. Quando aceder primeiro ao centro de segurança, tem Olá opção tooenable a recolha de dados para todas as VMs na sua subscrição. Se a recolha de dados não estiver ativada, o Centro de segurança recomenda que ative a recolha de dados na política de segurança de Olá dessa subscrição.

Quando a recolha de dados estiver ativada, o Centro de segurança Aprovisiona Olá Microsoft Monitoring Agent em todos os existentes suportadas máquinas virtuais do Azure e quaisquer novos que são criados. Olá Microsoft Monitoring Agent verifica a existência de várias configurações relacionadas com segurança. Além disso, o sistema de operativo Olá desencadeia eventos de registo de eventos. Os exemplos destes dados incluem: tipo e versão do sistema operativo, registos de sistema operativo (registos de eventos do Windows), processos em execução, nome da máquina, endereços IP, utilizador com sessão iniciada e ID do inquilino. Olá Microsoft Monitoring Agent lê entradas de registo de eventos e configurações e copia a área de trabalho do Olá dados tooyour para análise. Olá Microsoft Monitoring Agent também copia a área de tooyour de ficheiros de informação de falha.

Se estiver a utilizar o escalão gratuito do Olá do Centro de segurança, pode desativar a recolha de dados provenientes de máquinas virtuais por desativar a recolha de dados na política de segurança de Olá. Desativar a recolha de dados limita as avaliações de segurança para as suas VMs. toolearn mais, consulte [desativar a recolha de dados](#disabling-data-collection). Coleção de artefacto e instantâneos de discos VM estão ativadas, mesmo que a recolha de dados foi desativada. Recolha de dados é necessária para subscrições no escalão Standard do Olá do Centro de segurança.

> [!NOTE]
> Saiba mais sobre gratuito e Standard do Centro de segurança [escalões de preço](security-center-pricing.md).
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de Olá

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação. Este documento não é um guia passo a passo.
>
>

1. No Olá **recomendações** painel, selecione **ativar a recolha de dados para subscrições**.  Esta ação abre Olá **ativar recolha de dados** painel.
   ![Painel recomendações][2]
2. No Olá **ativar recolha de dados** painel, selecione a sua subscrição. Olá **política de segurança** painel para essa subscrição abre-se.
3. No Olá **política de segurança** painel, selecione **no** em **recolha de dados** tooautomatically recolher registos. Ativar Olá Aprovisiona recolha de dados monitorização extensão em todos os atuais e novas suportadas VMs na subscrição Olá.
4. Selecione **Guardar**.
5. Selecione **OK**.

## <a name="disabling-data-collection"></a>Desativar a recolha de dados
Se estiver a utilizar o escalão gratuito do Olá do Centro de segurança, pode desativar a recolha de dados provenientes de máquinas virtuais em qualquer altura ao desativar a recolha de dados na política de segurança de Olá. Recolha de dados é necessária para subscrições no escalão Standard do Olá do Centro de segurança.

1. Devolver toohello **Centro de segurança** painel e selecione Olá **política** mosaico. Esta ação abre Olá **segurança política-definir política por subscrição** painel.
   ![Selecione o mosaico de política de Olá][5]
2. No Olá **segurança política-definir política por subscrição** painel, subscrição Olá Selecione se pretende toodisable recolha de dados.
3. Olá **política de segurança** painel para essa subscrição abre-se.  Selecione **desativar** na recolha de dados.
4. Selecione **guardar** no Friso superior Olá.

## <a name="next-steps"></a>Passos seguintes
Este artigo mostrou como tooimplement Olá Centro de segurança recomendação "ativar recolha de dados." toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) – Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) – Saiba como recomendações ajudam a proteger os seus recursos do Azure.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e respondeu.
* [Monitorizar soluções de parceiros com o Centro de segurança do Azure](security-center-partner-solutions.md) – Saiba como toomonitor Olá estado de funcionamento das suas soluções de parceiros.
- [Segurança de dados do Centro de segurança do Azure](security-center-data-security.md) -Saiba como os dados são geridos e salvaguardados no Centro de segurança.
* [FAQ do Centro de segurança do Azure](security-center-faq.md)– encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)-obter Olá mais recentes notícias de segurança do Azure e informações.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
