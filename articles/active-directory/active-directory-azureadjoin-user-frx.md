---
title: "aaaSet configurar um novo dispositivo com o Azure AD durante a configuração | Microsoft Docs"
description: "Um tópico que explica como os utilizadores podem configurar a associação do Azure AD durante a sua experiência de primeira execução."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Configurar um novo dispositivo com o Azure AD durante a configuração
No Windows 10, os utilizadores podem associar tooAzure os respetivos dispositivos do Active Directory (Azure AD), a experiência de primeira execução Olá (FRX). Isto permite que os funcionários do organizações toodistribute dispositivos shrink-wrapped tootheir ou estudantes ou deixe-escolher os seus próprios dispositivos (CYOD).
Se as edições Windows 10 Professional ou Windows 10 Enterprise estiver instalado num dispositivo, Olá experiência do processo de configuração de toohello as predefinições para os dispositivos pertencentes à empresa.

## <a name="toojoin-a-device-tooazure-ad"></a>toojoin tooAzure um dispositivo AD
1. Quando ativar no seu dispositivo novo e iniciar o processo de configuração de Olá, deverá ver Olá **obter pronto** mensagem. Siga Olá tooset de pedidos de cópia de segurança do dispositivo.
2. Comece por personalizar o seu idioma e região. Em seguida, aceite termos de licenciamento de Software do Olá Microsoft.
   ![Personalizar a sua região](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Selecione a rede de Olá pretende toouse para ligar toohello Internet.
4. Selecione se estiver a utilizar um dispositivo pessoal ou de um dispositivo da empresa. Se for pertencentes à empresa, clique em **este dispositivo pertence toomy organização**. Esta ação inicia a experiência de associação do Azure AD Olá. Segue-se um ecrã que verá se estiver a utilizar o Windows 10 Professional.
   <center>
   ![Quem é o proprietário este ecrã de PC](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Introduza as credenciais de Olá que foram fornecidas tooyou pela sua organização.
   <center>
   ![Ecrã de início de sessão](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Depois de introduzir o nome de utilizador, um inquilino correspondente está localizado no Azure AD. Se estiver num domínio federado, será o servidor de Secure Token serviço (STS) no local de tooyour redirecionada – por exemplo, serviços do Active Directory Federação (AD FS).
7. Se for um utilizador num domínio não federada, introduza as credenciais diretamente no Olá página do Azure AD alojadas. Se tiver sido configurada imagem corporativa da empresa, verá também logótipo da sua organização e suporta texto.
8. Lhe for pedida para um desafio de autenticação multifator. Este desafio pode ser configurado por um administrador de TI.
9. Azure AD verifica se este utilizador/dispositivo requer inscrição na gestão de dispositivos móveis.
10. Windows regista o dispositivo de Olá no diretório da organização Olá no Azure AD e inscreve-lo na gestão de dispositivos móveis, se apropriado.
11. Se for um utilizador gerido, o Windows executa toohello ambiente de trabalho através de Olá processo automático de início de sessão.
12. Se um utilizador federado, o utilizador é direcionado toohello Windows início de sessão ecrã tooenter as suas credenciais.

> [!NOTE]
> Associar um domínio do Windows Server Active Directory no local do hello Windows experiência de out-of-box não é suportada. Por conseguinte, se planear toojoin um domínio de tooa do computador, deve selecionar ligação Olá **configurar o Windows com uma conta local** em vez disso. Em seguida, pode associar domínio de Olá das definições de Olá no seu computador, tal como fez antes.
> 
> 

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para empresa Olá: dispositivos de toouse formas de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Expandir nuvem dispositivos de tooWindows 10 capacidades através da associação do Azure Active Directory](active-directory-azureadjoin-user-upgrade.md)
* [Autenticar identidades sem palavras-passe através do Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Saiba mais sobre os cenários de utilização da Associação do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Ligar a dispositivos associados a domínios tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Associação do Azure AD](active-directory-azureadjoin-setup.md)

