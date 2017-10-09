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
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="c3bc3-103">Resolução de problemas de registo automático de domínio associado computadores tooAzure AD para clientes de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="c3bc3-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="c3bc3-104">Este tópico é aplicável toohello apenas os seguintes clientes:</span><span class="sxs-lookup"><span data-stu-id="c3bc3-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="c3bc3-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c3bc3-105">Windows 7</span></span> 
- <span data-ttu-id="c3bc3-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c3bc3-106">Windows 8.1</span></span> 
- <span data-ttu-id="c3bc3-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c3bc3-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="c3bc3-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c3bc3-108">Windows Server 2012</span></span> 
- <span data-ttu-id="c3bc3-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c3bc3-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="c3bc3-110">Para Windows 10 ou Windows Server 2016, consulte [registo automático de domínio de resolução de problemas associados a computadores tooAzure AD – Windows 10 e Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c3bc3-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="c3bc3-111">Este tópico parte do princípio de que configurou registo automático de dispositivos associados a um domínio delineados na como descrito em [como tooconfigure o registo automático do Windows associados a um domínio dispositivos com o Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3bc3-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="c3bc3-112">Este tópico fornece orientações sobre como tooresolve potenciais problemas de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="c3bc3-113">Toonote algumas coisas para resultados com êxito:</span><span class="sxs-lookup"><span data-stu-id="c3bc3-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="c3bc3-114">O registo destes clientes sobre o Azure AD é por utilizador/dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="c3bc3-115">Por exemplo: se jdoe e jharnett iniciar sessão no dispositivo toothis, um registo separados (DeviceID) é criado para cada um destes utilizadores no separador de informações de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="c3bc3-116">O registo de um destes clientes Box Olá está configurado tootry no início de sessão ou bloquear/desbloquear e pode haver atraso de 5 minutos que isto é acionado através de uma tarefa de Programador de tarefas.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="c3bc3-117">Um novamente instalar o sistema de operativo Olá ou um manual anular o registo e volte a registar pode criar um novo registo no Azure AD e irá resultar no várias entradas no separador de informações de utilizador Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="c3bc3-118">Passo 1: Obter o estado de registo de Olá</span><span class="sxs-lookup"><span data-stu-id="c3bc3-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="c3bc3-119">**Estado do registo de Olá tooverify:**</span><span class="sxs-lookup"><span data-stu-id="c3bc3-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="c3bc3-120">Olá abra a linha de comandos como administrador</span><span class="sxs-lookup"><span data-stu-id="c3bc3-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="c3bc3-121">Tipo`"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="c3bc3-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="c3bc3-122">Este comando apresenta uma caixa de diálogo que fornece mais detalhes sobre o estado de associação de Olá.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="c3bc3-124">Passo 2: Avaliar o estado do registo Olá</span><span class="sxs-lookup"><span data-stu-id="c3bc3-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="c3bc3-125">Se a associação Olá não foi bem sucedida, caixa de diálogo Olá fornece-lhe obter detalhes sobre o problema de Olá que ocorreu.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="c3bc3-126">**problemas mais comuns Olá são:**</span><span class="sxs-lookup"><span data-stu-id="c3bc3-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="c3bc3-127">Uma configuração incorreta do AD FS ou o Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3bc3-127">A misconfigured AD FS or Azure AD</span></span>

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="c3bc3-129">Não tem sessão iniciada como um utilizador de domínio</span><span class="sxs-lookup"><span data-stu-id="c3bc3-129">You are not signed on as a domain user</span></span>

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="c3bc3-131">Foi atingida a quota de uma</span><span class="sxs-lookup"><span data-stu-id="c3bc3-131">A quota has been reached</span></span>

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="c3bc3-133">serviço de Olá não está a responder</span><span class="sxs-lookup"><span data-stu-id="c3bc3-133">hello service is not responding</span></span> 

    ![Associação à área de trabalho para Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="c3bc3-135">Também pode encontrar informações de estado de Olá no registo de eventos de Olá em **aplicações e serviços Log\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="c3bc3-136">**Olá causas mais comuns para um registo com falhas são:**</span><span class="sxs-lookup"><span data-stu-id="c3bc3-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="c3bc3-137">O computador não está no rede interna da organização Olá ou uma VPN sem ligação tooan no local controlador de domínio do AD.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="c3bc3-138">São registados no computador de tooyour com uma conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="c3bc3-139">Problemas de configuração do serviço:</span><span class="sxs-lookup"><span data-stu-id="c3bc3-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="c3bc3-140">Olá servidor de Federação foi configurado toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="c3bc3-141">Não há nenhum objeto de ponto de ligação de serviço que aponta tooyour nome de domínio verificado no Azure AD numa floresta Olá AD em que o computador de Olá pertence.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="c3bc3-142">Um utilizador atingiu o limite de Olá dos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="c3bc3-143">Consulte Introdução ao registo de dispositivos do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3bc3-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3bc3-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c3bc3-144">Next steps</span></span>

<span data-ttu-id="c3bc3-145">Para obter mais informações, consulte Olá [registo automático de dispositivos FAQ](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c3bc3-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
