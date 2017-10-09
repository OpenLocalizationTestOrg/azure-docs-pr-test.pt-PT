---
title: "acesso de aaaConditional no Olá portal clássico do Azure | Microsoft Docs"
description: "Utilize o controlo de acesso condicional Olá toocheck de portal clássico do Azure para condições específicas durante a autenticação para acesso tooapplications."
services: active-directory
keywords: "acesso condicional tooapps, acesso condicional com o Azure AD, proteger o acesso a recursos de toocompany, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Acesso condicional no Olá portal clássico do Azure

Este tópico é sobre o acesso condicional no Olá portal clássico do Azure. Para informações mais recentes de Olá sobre o acesso condicional no Olá do Azure Active Directory, consulte [acesso condicional no Azure Active Directory](active-directory-conditional-access-azure-portal.md).


capacidades de controlo de Olá no acesso condicional do Azure Active Directory (Azure AD) oferecem formas simples toohelp recursos segura na nuvem de Olá e no local. Políticas de acesso condicional, tal como a autenticação multifator pode ajudar a proteger contra o risco de Olá de roubo e phished credenciais. Outras políticas de acesso condicional podem ajudar a manter os dados da sua organização. Por exemplo, além disso toorequiring credenciais, poderá ter uma política que apenas os dispositivos que estão inscritos num sistema de gestão de dispositivos móveis, como o Microsoft Intune pode aceder a serviços confidenciais da sua organização.

## <a name="prerequisites"></a>Pré-requisitos
Acesso condicional do Azure AD é uma funcionalidade do [Azure Active Directory Premium](http://www.microsoft.com/identity). Cada utilizador que acede a uma aplicação que tem de aplicar políticas de acesso condicional tem de ter uma licença do Azure AD Premium. Pode saber mais sobre os requisitos de licença do [relatório sem licença de utilizador](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Como é que o controlo de acesso condicional é imposto?
Com o controlo de acesso condicional no local, do Azure AD verifica para condições específicas Olá definido para um utilizador tooaccess uma aplicação. Depois dos requisitos de acesso são cumpridos, o utilizador Olá é autenticado e pode aceder à aplicação Olá.  

![Descrição geral do acesso condicional](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Condições
Estes são condições que pode incluir numa política de acesso condicional:

* **Associação ao grupo**. Controle o acesso de um utilizador com base na associação num grupo.
* **Localização**. Utilizar a localização de Olá Olá tootrigger multifator da autenticação de utilizador e utilizar controlos de bloco quando um utilizador não se encontra numa rede fidedigna.
* **Plataforma de dispositivo**. Utilize a plataforma de dispositivo Olá, por exemplo, iOS, Android, Windows Mobile ou Windows, como uma condição para aplicar a política.
* **Dispositivo ativado**. Estado do dispositivo, se ativado ou desativado, é validado durante a avaliação da política de dispositivo. Se desativar um dispositivo perdido ou roubado no diretório de Olá, já não se pode satisfazer requisitos da política.
* **Risco de início de sessão e o utilizador**. Pode utilizar [do Azure AD Identity Protection](active-directory-identityprotection.md) para políticas de risco de acesso condicional. Políticas de risco de acesso condicional ajudam a dar a sua organização avançada com base em proteção em eventos de risco e as atividades de início de sessão invulgares.

## <a name="controls"></a>Controlos
Estes são controlos que pode utilizar tooenforce uma política de acesso condicional:

* **Autenticação multifator**. Pode exigir a autenticação forte através da autenticação multifator. Pode utilizar a autenticação multifator com o Azure multi-factor Authentication ou utilizando um fornecedor de autenticação multifator no local, juntamente com os serviços de Federação do Active Directory (AD FS). Utilizar multi-factor authentication ajuda a proteger os recursos de que está a ser acedida por um utilizador não autorizado que poderá ter obteve acesso toohello credenciais de um utilizador válido.
* **Bloco**. Pode aplicar condições como localização de utilizador tooblock acesso de utilizador. Por exemplo, pode bloquear o acesso quando um utilizador não se encontra numa rede fidedigna.
* **Os dispositivos conformes**. Pode definir políticas de acesso condicional ao nível do dispositivo Olá. Pode configurar uma política para que apenas os computadores que estão associados a um domínio ou os dispositivos móveis que estejam inscritos numa aplicação de gestão de dispositivos móveis, podem aceder aos recursos da sua organização. Por exemplo, pode utilizar a conformidade de dispositivo do Intune toocheck e, em seguida, comunicar-tooAzure AD para a imposição quando o utilizador Olá tenta tooaccess uma aplicação. Para obter orientações detalhadas sobre como toouse Intune tooprotect aplicações e dados, consulte [proteger aplicações e dados com o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Também pode utilizar proteção de dados de tooenforce do Intune para dispositivos perdidos ou roubados. Para obter mais informações, consulte [ajudar a proteger os seus dados com a eliminação completa ou seletiva através do Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Aplicações
Pode impor uma política de acesso condicional ao nível da aplicação Olá. Defina níveis de acesso para aplicações e serviços em nuvem Olá ou no local. política de Olá é aplicado diretamente toohello Web site ou serviço. Olá é imposta para acesso toohello browser e tooapplications Olá serviço de acesso.

## <a name="device-based-conditional-access"></a>Acesso condicional baseado no dispositivo
Pode restringir o acesso tooapplications dos dispositivos que são registados com o Azure AD e o que satisfaz os condições específicas. Acesso condicional baseado no dispositivo protege os recursos de uma organização de utilizadores que a tentativa de recursos de Olá tooaccess de:

* Dispositivos desconhecidos ou não geridos.
* Dispositivos que não cumprem as políticas de segurança de Olá a organização configurou.

Pode definir políticas com base nestes requisitos:

* **Dispositivos associados a domínios**. Defina uma política toorestrict acesso toodevices que são o domínio de Active Directory no local tooan associados e que também estão registados com o Azure AD. Esta política aplica-se tooWindows computadores de secretária, portáteis e enterprise tablets.
  Para obter mais informações sobre como tooset se o registo automático de dispositivos associados a um domínio com o Azure AD, consulte [configurar o registo automático de dispositivos associados a um domínio do Windows com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Os dispositivos conformes**. Definir um toodevices acesso toorestrict de política que estão marcados **compatíveis** no diretório do sistema de gestão de Olá. Esta política assegura que apenas os dispositivos que cumpram as políticas de segurança, tais como impor a encriptação de ficheiros num dispositivo são permissão de acesso. Pode utilizar este acesso toorestrict de política de Olá seguintes dispositivos:
  
  * **Os dispositivos associados a um domínio Windows**. Gerido pelo System Center Configuration Manager (no ramo atual do Olá) implementados numa configuração híbrida.
  * **Dispositivos pessoais ou de trabalho Windows 10 Mobile**. Gerido pelo Intune ou por um sistema de gestão de dispositivos móveis de terceiros suportadas.
  * **iOS e dispositivos Android**. Gerido pelo Intune.

Os utilizadores que acedem a aplicações que estão protegidas por um baseado nos dispositivos, política de autoridade de certificação tem aceder à aplicação Olá de um dispositivo que cumpra os requisitos desta política. O acesso é negado se tentada num dispositivo que não cumpre os requisitos de política.

Para obter informações sobre como tooconfigure um dispositivo baseada na política de autoridade de certificação no Azure AD, consulte [definir a política de acesso condicional baseado no dispositivo para aplicações do Azure Active Directory-ligado](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Recursos
Consulte Olá os seguintes recursos categorias e artigos toolearn mais sobre a definição de acesso condicional para a sua organização.

### <a name="multi-factor-authentication-and-location-policies"></a>Políticas de autenticação e a localização de multifator
* [Introdução ao acesso condicional tooAzure ligados AD aplicações com base nas políticas de autenticação multifator, localização e grupo](active-directory-conditional-access-azuread-connected-apps.md)
* [Aplicações e browsers suportados](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Acesso condicional baseado no dispositivo
* [Definir política de acesso condicional baseado no dispositivo para o acesso a aplicações de Active Directory-ligado tooAzure do controlo](active-directory-conditional-access-policy-connected-applications.md)
* [Configurar o registo automático do Windows dispositivos associados a um domínio com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Resolução de problemas para problemas de acesso do Azure Active Directory](active-directory-conditional-access-device-remediation.md)
* [Ajudar a proteger dados em dispositivos perdidos ou roubados ao utilizar o Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Proteger recursos com base em risco de início de sessão
* [Proteção de identidade do Azure AD](active-directory-identityprotection.md)

### <a name="next-steps"></a>Passos seguintes
* [Perguntas mais frequentes de acesso condicional](active-directory-conditional-faqs.md)
* [Referência técnica](active-directory-conditional-access-technical-reference.md)

