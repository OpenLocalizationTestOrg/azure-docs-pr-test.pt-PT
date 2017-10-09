---
title: aaaUsing Office com o Azure RemoteApp | Microsoft Docs
description: Saiba como o Office e o Azure RemoteApp funcionam em conjunto
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Utilizar o Office com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Tem duas opções para alojar aplicações do Office no Azure RemoteApp: Office 365 ProPlus ou a versão de avaliação do Office 2013 Professional Plus.

**Hei, responsável pelo Sabia que temos uma nova, uma melhor artigo logo que irá substituir isto? Veja [como toouse subscrição do Office 365 com o Azure RemoteApp](remoteapp-officesubscription.md). Abrange todas as informações de Olá que precisa para utilizar o Office 365 + RemoteApp do Azure.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
Pode criar uma coleção do RemoteApp utilizando a imagem de modelo do Office 365 ProPlus Olá. Esta opção permite-lhe tooextend tooRemoteApp de serviço do Office 365. Tem de ter um plano de subscrição existente e os utilizadores têm de estar licenciados para Olá serviço do Office 365 ProPlus, de forma autónoma ou através de planos de serviço Olá do Office 365.

RemoteApp suporta a ativação de computador partilhado do Office 365. Quando ativar a ativação de computador partilhado e utilizar Olá [ferramenta de implementação do Office](http://www.microsoft.com/download/details.aspx?id=36778) para instalação, Office 365 ProPlus instala sem ser activado. Quando um utilizador iniciar sessão para uma coleção que contém o Office 365, Office verifica toosee se o utilizador Olá tiver sido aprovisionada para Office 365 ProPlus. Se Sim, Office temporariamente ativa do Office 365 ProPlus - esta ativação mantém até esse sinais de utilizadores fora de serviço Olá.

toouse a ativação de computador partilhado do Office 365, terá de toocreate um [modelo personalizado](remoteapp-create-custom-image.md) e instalação do Office 365 ProPlus, seguindo [estas indicações](https://technet.microsoft.com/library/dn782858.aspx).

Pode gerir licenças do Office 365 dos seus utilizadores em Olá [Portal de administração do Office 365](https://portal.office365.com/). Leia mais informações sobre [planos de serviço do Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).  

## <a name="office-2013-professional-plus-trial"></a>Versão de avaliação do Office 2013 Professional Plus
Durante a avaliação de 30 dias do RemoteApp, pode utilizar o toocreate de imagem de modelo do Olá Office 2013 Professional Plus (versão de avaliação) uma coleção do RemoteApp. Pode atribuir utilizadores toothis avaliação coleção a utilizar as respetivas contas de trabalho do Azure Active Directory ou contas Microsoft. Não é necessária nenhuma subscrição adicional.

Esta é lo de Olá uma excelente opção tookick e obter um bom feeling para o Office no RemoteApp. No entanto, esta opção é pretendido para avaliação e teste apenas. Coleções do RemoteApp criadas utilizando a imagem de modelo do Office 2013 Professional Plus (versão de avaliação) Olá não podem ser transitado tooproduction modo e serão desativadas no fim de Olá do período de avaliação de Olá.

## <a name="switching-from-trial-tooproduction"></a>Mudar de avaliação tooproduction
Quando iniciar a avaliação gratuita de 30 dias, nota no Olá RemoteApp secção portal Olá informará quanto ter deixou na versão de avaliação de Olá antes que seja necessário tooa tootransition paga conta. Pode ativar o modo de tooproduction conta e o comutador utilizando a hiperligação de Olá desta nota.

Quando ativa a sua conta, este irá afetar todas as coleções do RemoteApp Olá na sua conta.

* Coleções que estejam a executar com Olá Windows Server 2012 R2 ou imagens de modelo do Office 365 ProPlus Olá irão transitar tooproduction de forma totalmente integrada. Todos os dados de utilizador e as definições, incluindo sessões em curso, permanecem intactas.
* Se tiver carregado imagens de modelo personalizada, coleções utilizando essas imagens também irão transitar totalmente integrada.
* imagem de modelo do Office 2013 Professional Plus (versão de avaliação) Olá destina-se apenas de avaliação. Coleções com esta imagem de modelo não podem ser transitado tooproduction. Serão colocados no estado "desactivado".

Se não transitar tooproduction modo por expiração Olá da sua versão de avaliação, as coleções do RemoteApp serão desativadas. Não se preocupe, as definições e dados dos utilizadores são guardados para outra 90 dias, pelo que, ainda pode ativar o modo de tooproduction de serviço e o comutador sem perda de dados.

