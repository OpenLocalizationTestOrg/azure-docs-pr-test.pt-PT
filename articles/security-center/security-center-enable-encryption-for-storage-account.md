---
title: "encriptação de aaaEnable para a conta de armazenamento no Centro de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá as recomendações do Centro de segurança do Azure * * ativar a encriptação para o Azure armazenamento conta *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Ativar a encriptação para a conta de armazenamento do Azure no Centro de segurança do Azure
Centro de segurança do Azure poderá recomendar que ativar a encriptação do serviço de armazenamento do Azure para dados inativos.

Encriptação de serviço de armazenamento (SSE) funciona através da encriptação de dados de Olá quando é escrito tooAzure armazenamento e a desencriptação de dados de Olá antes da obtenção.  SSE atualmente só está disponível para Olá serviço Blob do Azure e pode ser utilizado para blobs de blocos, blobs de páginas e blobs de acréscimo.  toolearn mais, consulte [encriptação do serviço de armazenamento para dados Inativos](../storage/common/storage-service-encryption.md).


> [!Note]
> Depois de ativar a encriptação, apenas novos dados são encriptados. Os blobs existentes na sua conta de armazenamento de permanecer desencriptados. os blobs existentes tooencrypt, consulte Olá [FAQ de encriptação do serviço de armazenamento](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

Encriptação do serviço de armazenamento só é suportada em contas de armazenamento do Resource Manager. Contas de armazenamento clássicas não são atualmente suportadas. Olá toounderstand clássico e modelos de implementação do Resource Manager, consulte [modelos de implementação do Azure](../azure-classic-rm.md).

> [!NOTE]
> Este documento apresenta serviço Olá utilizando um exemplo de implementação.  Este documento não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de Olá
1. No Olá **recomendações** painel, selecione **ativar a encriptação da conta de armazenamento do Azure**.
   ![Ativar a encriptação da conta de armazenamento][1]
2. Olá **ativar a encriptação de armazenamento** abre o painel. Este painel apresenta uma lista de contas de armazenamento do Azure olá onde a encriptação de armazenamento está desativada. Neste exemplo, vamos selecione **storageacct1**.
   ![Ativar a encriptação de armazenamento][2]
3. Olá **encriptação** painel **storageacct1** abre. Selecione **ativada**.
   ![Painel de encriptação][3]
4. Selecione **Guardar**.

Agora que tiver ativado a encriptação de armazenamento para **storageacct1**.


## <a name="see-also"></a>Consultar também
Este documento mostrou como tooimplement Olá Centro de segurança recomendação "ativar encriptação para a conta de armazenamento do Azure." toolearn mais informações sobre a encriptação do serviço de armazenamento do Azure, consulte o artigo seguinte Olá:

* [Encriptação do serviço de armazenamento do Azure para dados Inativos](../storage/common/storage-service-encryption.md)

toolearn mais acerca do Centro de segurança, consulte o artigo seguinte Olá:

* [Definir políticas de segurança no Centro de segurança do Azure](security-center-policies.md) -Saiba como as políticas de segurança de tooconfigure às suas subscrições do Azure e os grupos de recursos.
* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) -Saiba como toomonitor Olá estado de funcionamento dos seus recursos Azure.
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e respondeu.
* [Gerir recomendações de segurança no Centro de segurança do Azure](security-center-recommendations.md) -Saiba como recomendações ajudam a proteger os seus recursos do Azure.
* [FAQ do Centro de segurança do Azure](security-center-faq.md) -encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Blogue de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) -encontre mensagens do Blogue acerca da segurança do Azure e conformidade.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
