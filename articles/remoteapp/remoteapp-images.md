---
title: "aaaWhat existe nas imagens de modelo do Azure RemoteApp Olá? | Microsoft Docs"
description: "Saiba mais sobre as imagens de modelo de Olá incluídas com o Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Novidades nas imagens de modelo do Azure RemoteApp Olá?
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

A sua subscrição do Azure RemoteApp inclui três imagens de modelo:

* Windows Server 2012
* Microsoft Office 365 ProPlus (é necessária uma subscrição do Office 365)
* Microsoft Office 2013 Professional Plus (versão de avaliação apenas)

> [!IMPORTANT]
> A sua subscrição do Azure RemoteApp concede que acesso toohello software nas imagens de Olá, com exceção de Olá do Office 365 ProPlus, que necessita de uma subscrição separada, e o Office 2013, que não pode ser utilizado em produção. Isto significa que pode partilhar os programas de Olá ou as aplicações nas imagens de modelo Olá com os seus utilizadores. Por exemplo, se criar uma coleção que utiliza a imagem do Windows Server 2012 R2 Olá, pode publicar o System Center Endpoint Protection para os utilizadores tooaccess através do RemoteApp.
> 
> Veja Olá [detalhes de licenciamento do RemoteApp](remoteapp-licensing.md) para obter mais informações. E [utilizar o Office com o Azure RemoteApp](remoteapp-o365.md) para Olá informações de licenciamento do Office.
> 
> 

Continue a ler para obter detalhes sobre o conteúdo de cada imagem.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 ("Olá imagem clássica")
Esta imagem baseia-se no sistema de operativo Microsoft Windows Server 2012 R2 Datacenter e tem hello seguintes funções e funcionalidades instaladas requisitos de Olá toomeet para imagens de modelo do Azure RemoteApp:

* .NET Framework 4.5, 3.5.1, 3.5
* Experiência de Utilização do Computador
* Serviços de Tinta Digital e Escrita Manual
* Media Foundation
* Anfitrião de Sessões de Ambiente de Trabalho Remoto
* Windows PowerShell 4.0
* ISE do Windows PowerShell
* Suporte WoW64

Esta imagem tem também Olá seguintes aplicações instaladas:

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (é necessária uma subscrição)
Office 365 é hello mais aplicação pedida, pelo que criámos uma imagem "personalizada" para si toowork com.

Esta imagem é uma extensão da imagem clássica Olá e tem hello seguintes componentes do Microsoft Office 365 ProPlus instalados além disso componentes de toohello descritos na imagem do Windows Server 2012 R2 Olá:

* Access
* Excel
* Lync
* OneNote
* OneDrive para empresas (tenha em atenção que o agente sincronização Olá não é suportado para utilização com o Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Ferramentas de Verificação do Microsoft Office

imagem de Olá também inclui o Visio Pro e o Project Pro.

E Olá aplicações, bem como os seguintes:

* SQL Native Client
* Controlador ODBC
* SQL Server Data Mining cliente
* MasterDataServices cliente
* Microsoft Publisher
* PowerQuery
* Power Map

A funcionalidade completa das aplicações do Office 365 ProPlus está apenas disponível para utilizadores com um plano do Office 365 ProPlus. Para obter mais detalhes sobre a subscrição do Office 365 de Olá planos consulte [planos de serviço do Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). Ainda tem perguntas? Veja Olá [do Office 365 + RemoteApp](remoteapp-o365.md) informações. Consulte também Olá novo artigo [como toouse subscrição do Office 365 com o Azure RemoteApp](remoteapp-officesubscription.md).

Tenha em atenção que necessário separadamente - toolicense do Office 365 ProPlus, Visio Pro e o Project Pro, cada têm a sua própria licença.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office 2013 Professional Plus (versão de avaliação apenas)
Durante o período de avaliação gratuita de Olá, pode testar o serviço de Olá com imagem Olá Office 2013.

Esta imagem é uma extensão da imagem clássica Olá e tem hello seguintes componentes do Microsoft Office 2013 Professional Plus instalados além componentes de toohello descritos na imagem do Windows Server 2012 R2 Olá:

* Access
* Excel
* Lync
* OneNote
* OneDrive para empresas (tenha em atenção que o agente sincronização Olá não é suportado para utilização com o Azure RemoteApp)
* Outlook
* PowerPoint
* Project
* Visio
* Word
* Ferramentas de Verificação do Microsoft Office

> [!IMPORTANT]
> **Informação legal:** esta imagem não inclui uma licença do Microsoft Office e *não pode ser utilizada para produção*. imagem do Office 2013 Professional Plus Olá destina-se apenas a utilização de avaliação. Se pretender que as aplicações do Office toouse no Azure RemoteApp para produção, terá de imagem do Office 365 ProPlus do toouse Olá. Para obter mais detalhes sobre o licenciamento do Office, consulte [Utilizar o Office 365 com o Azure RemoteApp](remoteapp-o365.md)
> 
> 

