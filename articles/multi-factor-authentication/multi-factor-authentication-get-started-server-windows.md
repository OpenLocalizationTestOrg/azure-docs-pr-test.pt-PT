---
title: "Autenticação do Windows e Servidor de MFA do Azure | Microsoft Docs"
description: "Esta é a página do Multi-Factor Authentication do Azure que irá ajudar a implementar a Autenticação do Windows e o Servidor Multi-Factor Authentication do Azure."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.openlocfilehash: ae4503425d139c31d810f4bcf940b03357ed933a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Autenticação do Windows e Servidor Multi-Factor Authentication do Azure
Utilize a secção Autenticação do Windows do Servidor Multi-Factor Authentication do Azure para ativar e configurar a autenticação do Windows para aplicações. Antes de configurar a Autenticação do Windows, mantenha a lista seguinte em mente:

* Após a configuração, reinicie o Multi-Factor Authentication para os Serviços de Terminal entrarem em vigor.
* Se "Exigir correspondência de utilizador do Multi-Factor Authentication do Azure" estiver selecionado e não estiver na lista de utilizadores, não conseguirá iniciar sessão no computador depois de reiniciar.
* Os IPs Fidedignos dependem do facto de a aplicação poder fornecer o IP do cliente na autenticação. Atualmente, apenas os Serviços de Terminal são suportados.  

> [!NOTE]
> Esta funcionalidade não é suportada para proteger os Serviços de Terminal no Windows Server 2012 R2.

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a>Para proteger uma aplicação com a Autenticação do Windows, utilize o procedimento seguinte.
1. No Servidor Multi-Factor Authentication do Azure, clique no ícone Autenticação do Windows.
   ![Autenticação do Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Selecione a caixa de verificação **Ativar Autenticação do Windows**. Por predefinição, esta caixa está desmarcada.
3. O separador Aplicações permite ao administrador configurar uma ou mais aplicações para a Autenticação do Windows.
4. Selecione um servidor ou uma aplicação e especifique se o servidor/aplicação está ativado. Clique em **OK**.
5. Clique em **Adicionar...**
6. O separador IPs Fidedignos permite ignorar sessões o Multi-Factor Authentication do Azure para as sessões do Windows com origem em IPs específicos. Por exemplo, se os empregados utilizarem a aplicação a partir do escritório e de casa, pode decidir que não pretende que os respetivos telefones toquem para o Multi-Factor Authentication do Azure enquanto estiverem no escritório. Para tal, especifique a sub-rede do escritório como uma entrada de IPs Fidedignos.
7. Clique em **Adicionar...**
8. Selecione **IP Único** se gostaria de ignorar um único endereço IP.
9. Selecione **Intervalo de IP** se gostaria de ignorar um intervalo de IP completo. Por exemplo, 10.63.193.1-10.63.193.100.
10. Selecione **Sub-rede** se pretende especificar um intervalo de IPs utilizando a notação de sub-rede. Introduza o IP inicial da sub-rede e escolha a máscara de rede adequada na lista pendente.
11. Clique em **OK**.

## <a name="next-steps"></a>Passos seguintes

- [Configurar aplicações de VPN de terceiros para o Servidor de MFA do Azure](multi-factor-authentication-advanced-vpn-configurations.md)

- [Aumente a infraestrutura de autenticação existente com a extensão NPS para a MFA do Azure](multi-factor-authentication-nps-extension.md)
