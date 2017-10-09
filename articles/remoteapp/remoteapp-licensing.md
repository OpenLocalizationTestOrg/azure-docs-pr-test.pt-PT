---
title: licenciamento do RemoteApp de aaaAzure | Microsoft Docs
description: Saiba como funciona o licenciamento no Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Como funciona o licenciamento no Azure RemoteApp?
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Portanto, configurou o serviço do Azure RemoteApp, criado os modelos e são aplicações de toopublish pronto tooyour utilizadores. Contudo, ainda existe uma toofigure coisa último out: licenciamento. Como funciona apenas trabalho licenciamento do RemoteApp e para aplicações de Olá que partilha através do RemoteApp?

O RemoteApp não requer quaisquer licenças do Windows ou CALs de Ambiente de Trabalho Remoto. Encarrega-se a sua subscrição de Olá do lado do RemoteApp próprio. (Consulte os detalhes de Olá de Olá [planos de preços](https://azure.microsoft.com/pricing/details/remoteapp).)

Se utilizar uma das imagens de Olá que está incluído na sua subscrição, pode partilhar qualquer uma das aplicações de Olá instaladas nessa imagem sem ser necessária uma licença separada. Por exemplo, se utilizar toobuild de imagem de modelo de Windows Server 2012 R2 Olá a coleção, pode partilhar o System Center Endpoint Protection com os seus utilizadores. Olá regra de toothis apenas exceções são Office 365 ProPlus, que necessita de uma subscrição separada, e o Office 2013, que não pode ser partilhado numa coleção de produção.

Se pretender que a imagem de modelo do toouse Olá do Office 365 incluída no RemoteApp, tem de ter um *existente* plano do Office 365 ProPlus. Olá que mesmo se aplica a qualquer aplicação do Office 365, que pode publicar utilizando um modelo personalizado. É necessário tooactivate Olá aplicações com a sua própria subscrição. Tal aplica-se a subscrições pagas e de avaliação. Se quiser imagem de modelo toouse Olá do Office 365 durante a avaliação de Olá, *e ainda não tiver uma subscrição*, visite a página de toohello do Office 365 demasiado[inscrever](https://go.microsoft.com/fwlink/p/?LinkID=403802) para uma subscrição de avaliação. Consulte [Como o RemoteApp e o Office funcionam em conjunto?](remoteapp-o365.md) para obter mais informações.

Se, durante o período de avaliação Olá, que não pretende subscrição de avaliação tooget um Office 365, utilize a imagem de modelo do Olá Office 2013 Professional Plus incluída no RemoteApp. Esta imagem de modelo apenas pode ser utilizada durante 30 dias e não pode ser convertida numa coleção paga.

Para outras aplicações, terá de toomake se de que tem Olá licença tooshare Olá aplicação.

Faz sentido, certo? Pode publicar qualquer aplicação que legalmente direito tooshare. E tem de se é realmente toomake designada por tooshare os programas.

Tenha em atenção que não pode utilizar uma CAL ou um contrato de Licenciamento em Volume numa coleção na nuvem. *Pode* utilizam um aplicações de tooactivate de contrato de licenciamento em Volume na sua coleção híbrida (exceto o Office). Basta tooinstall-los no seu modelo de imagem de Olá suporte de dados de licenciamento em Volume. Siga as informações de Olá do Olá aplicação fornecedor tooinstall as licenças no ambiente de trabalho remoto.

