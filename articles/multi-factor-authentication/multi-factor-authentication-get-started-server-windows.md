---
title: "aaaWindows autenticação e o servidor MFA do Azure | Microsoft Docs"
description: "Esta é Olá multi-factor authentication página que irá ajudar a implementar a autenticação do Windows e o servidor do Azure multi-factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Autenticação do Windows e Servidor Multi-Factor Authentication do Azure
Utilize a secção autenticação do Windows hello hello do servidor multi-factor Authentication Azure tooenable e configurar a autenticação do Windows para aplicações. Antes de configurar a autenticação do Windows, mantenha Olá lista em consideração os seguintes:

* Após a configuração, reinicie Olá Azure multi-factor Authentication para o efeito de tootake de serviços de Terminal.
* Se estiver marcada "Correspondência de utilizador exigir autenticação multi-factor do Azure" e não estiver na lista de utilizadores Olá, não será capaz de toolog numa máquina Olá após o reinício.
* Fidedigno que IPs é depende se a aplicação Olá pode fornecer Olá IP do cliente com a autenticação de Olá. Atualmente, apenas os Serviços de Terminal são suportados.  

> [!NOTE]
> Esta funcionalidade não é suportado toosecure os serviços de Terminal no Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure uma aplicação com a autenticação do Windows, Olá utilize procedimento a seguir.
1. No hello do servidor multi-factor Authentication Azure clique Olá ícone autenticação do Windows.
   ![Autenticação do Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Verifique Olá **ativar a autenticação do Windows** caixa de verificação. Por predefinição, esta caixa está desmarcada.
3. separador de aplicações de Olá permite Olá administrador tooconfigure uma ou mais aplicações para autenticação do Windows.
4. Selecione um servidor ou a aplicação – especificar se a aplicação e do Olá está ativada. Clique em **OK**.
5. Clique em **Adicionar...**
6. separador IPs fidedignos de Olá permite-lhe tooskip sessões de Azure multi-factor Authentication do Windows provenientes de IPs específicos. Por exemplo, se os funcionários utilizarem a aplicação Olá Olá escritório e em casa, pode decidir que não pretende que os telefones toquem para o Azure multi-factor Authentication, office Olá. Para tal, tem de especificar a sub-rede do escritório Olá como entrada de IPs fidedignos.
7. Clique em **Adicionar...**
8. Selecione **IP único** se gostaria tooskip um único endereço IP.
9. Selecione **intervalo IP** se gostaria tooskip um intervalo IP completo. Por exemplo, 10.63.193.1-10.63.193.100.
10. Selecione **sub-rede** se gostaria toospecify um intervalo de IPs utilizando a notação de sub-rede. Introduza o IP inicial da sub-rede Olá e escolha Olá máscara de rede adequada Olá na lista pendente.
11. Clique em **OK**.

## <a name="next-steps"></a>Passos seguintes

- [Configurar aplicações de VPN de terceiros para o Servidor de MFA do Azure](multi-factor-authentication-advanced-vpn-configurations.md)

- [Aumentar a sua infraestrutura de autenticação existente com Olá extensão NPS para o Azure MFA](multi-factor-authentication-nps-extension.md)
