---
title: "aaaTroubleshooting Olá-registo automático de domínio do Azure AD computadores associados a um para clientes de nível inferior do Windows | Microsoft Docs"
description: "Registo automático Olá de domínio do Azure AD de resolução de problemas associados a computadores para os clientes de nível inferior do Windows."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Resolução de problemas de registo automático de domínio associado computadores tooAzure AD para clientes de nível inferior do Windows 

Este tópico é aplicável toohello apenas os seguintes clientes: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Para Windows 10 ou Windows Server 2016, consulte [registo automático de domínio de resolução de problemas associados a computadores tooAzure AD – Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

Este tópico parte do princípio de que configurou registo automático de dispositivos associados a um domínio delineados na como descrito em [como tooconfigure o registo automático do Windows associados a um domínio dispositivos com o Azure Active Directory](active-directory-device-registration-get-started.md).
 
Este tópico fornece orientações sobre como tooresolve potenciais problemas de resolução de problemas.  
Toonote algumas coisas para resultados com êxito: 

- O registo destes clientes sobre o Azure AD é por utilizador/dispositivo. Por exemplo: se jdoe e jharnett iniciar sessão no dispositivo toothis, um registo separados (DeviceID) é criado para cada um destes utilizadores no separador de informações de utilizador Olá.  

- O registo de um destes clientes Box Olá está configurado tootry no início de sessão ou bloquear/desbloquear e pode haver atraso de 5 minutos que isto é acionado através de uma tarefa de Programador de tarefas. 

- Um novamente instalar o sistema de operativo Olá ou um manual anular o registo e volte a registar pode criar um novo registo no Azure AD e irá resultar no várias entradas no separador de informações de utilizador Olá no Olá portal do Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Passo 1: Obter o estado de registo de Olá 

**Estado do registo de Olá tooverify:**  

1. Olá abra a linha de comandos como administrador 

2. Tipo`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

Este comando apresenta uma caixa de diálogo que fornece mais detalhes sobre o estado de associação de Olá.

![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Passo 2: Avaliar o estado do registo Olá 

Se a associação Olá não foi bem sucedida, caixa de diálogo Olá fornece-lhe obter detalhes sobre o problema de Olá que ocorreu.

**problemas mais comuns Olá são:**

- Uma configuração incorreta do AD FS ou o Azure AD

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Não tem sessão iniciada como um utilizador de domínio

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Foi atingida a quota de uma

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- serviço de Olá não está a responder 

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Também pode encontrar informações de estado de Olá no registo de eventos de Olá em **aplicações e serviços Log\Microsoft-Workplace Join**.
  
**Olá causas mais comuns para um registo com falhas são:** 

- O computador não está no rede interna da organização Olá ou uma VPN sem ligação tooan no local controlador de domínio do AD.

- São registados no computador de tooyour com uma conta de computador local. 

- Problemas de configuração do serviço: 

  - Olá servidor de Federação foi configurado toosupport **WIAORMULTIAUTHN**. 

  - Não há nenhum objeto de ponto de ligação de serviço que aponta tooyour nome de domínio verificado no Azure AD numa floresta Olá AD em que o computador de Olá pertence.

  - Um utilizador atingiu o limite de Olá dos dispositivos. Consulte Introdução ao registo de dispositivos do Azure Active Directory.

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações, consulte Olá [registo automático de dispositivos FAQ](active-directory-device-registration-faq.md) 
