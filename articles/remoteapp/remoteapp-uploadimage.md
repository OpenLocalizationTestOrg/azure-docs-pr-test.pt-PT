---
title: aaaUpload uma imagem personalizada para o Azure RemoteApp | Microsoft Docs
description: Saiba como tooupload personalizadas de imagem para o Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Carregar uma imagem personalizada para o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Agora que criou a imagem de modelo personalizado ou Atualizou com as alterações, terá de tooupload biblioteca de imagens essa imagem tooyour Azure RemoteApp. Utilize estes passos.

## <a name="before-you-start"></a>Antes de começar
1. Verificar a sua imagem personalizada cumpre Olá [requisitos de imagem](remoteapp-imagereqs.md) e [os requisitos da aplicação](remoteapp-appreqs.md).
2. Instalar Olá [módulo Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Passo a passo sobre como imagem personalizada tooupload
1. Abra o Portal de gestão do Azure e navegue toohello RemoteApp página.
2. No Olá **imagens de modelo** separador, clique em **carregar** em Olá parte inferior da página Olá.
3. Introduza um nome amigável para a imagem e especifique a localização de conta de armazenamento Olá. Certifique-se de localização de Olá Olá mesma localização que a coleção do RemoteApp ou para uma localização onde pretende toocreate um.
4. Quando lhe for pedido, transferir Olá script tooyour local PC.
5. Copie os parâmetros de comando de Olá na área de transferência do Olá texto caixa tooyour.
6. Abra uma janela elevada do Windows PowerShell.
7. De Olá elevados janela do Windows PowerShell, navegue até toohello mesmo diretório onde transferiu o script de Olá.
8. Olá colar copiados comandos e prima **Enter**.
   
   processo de carregamento de Olá começará e duração pode depender de vários fatores, incluindo a velocidade da rede e o tamanho da imagem de Olá
9. Se o seu carregamento falhar devido a interrupção de rede ou coisas como ou, pode sempre retomar o processo de carregamento de Olá que começou. tooresume um carregamento, executar script de Olá novamente utilizando Olá a mesma linha de comandos.

> [!WARNING]
> Nunca modificar o script de carregamento de Olá. Verificações específicos tem sido implementado tooensure que Olá imagem cumpre os requisitos de imagem Olá e os requisitos da aplicação.
> 
> 

## <a name="common-problems"></a>Problemas comuns
* Certifique-se de que utilizar o Windows PowerShell, não o Azure PowerShell. Terá de módulo de Azure PowerShell tooinstall Olá porque determinados módulos são necessários durante o processo de carregamento de Olá.
* Nunca alter script Olá, validações existem para sua comodidade.
* Se o ficheiro de vhd Olá obtém bloqueado durante o carregamento, copie o ficheiro de Olá ou movê-la tooa nova localização e a tentativa de carregamento novamente. Poderão existir alguns processo do Windows que está a impedir o carregamento.  

