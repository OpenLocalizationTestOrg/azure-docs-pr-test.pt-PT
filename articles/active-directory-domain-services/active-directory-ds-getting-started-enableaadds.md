---
title: 'Azure Active Directory Domain Services: Ativar o Azure Active Directory Domain Services | Microsoft Docs'
description: "Ativar o Azure Active Directory Domain Services utilizando Olá portal clássico do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="7e956-103">Ativar o Azure Active Directory Domain Services utilizando Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7e956-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="7e956-104">Tarefa 3: ativar o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="7e956-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="7e956-105">Nesta tarefa, ativar do Azure Active Directory Domain Services (Azure AD DS) para o seu diretório efetuando Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7e956-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="7e956-106">Aceda toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="7e956-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="7e956-107">No painel esquerdo Olá, selecione Olá **do Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="7e956-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="7e956-108">Selecione o inquilino do Azure Active Directory (Azure AD) Olá (diretório) para o qual pretende tooenable do Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="7e956-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Selecionar o Azure AD Directory](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="7e956-110">No Olá **diretório de pré-visualização** página, clique em Olá **configurar** separador.</span><span class="sxs-lookup"><span data-stu-id="7e956-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Separador Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="7e956-112">Em **dos serviços de domínio**, alterar Olá **ativar os serviços de domínio para este diretório** opção demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="7e956-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="7e956-113">Opções adicionais de configuração do Azure Active Directory Domain Services apresentados na página de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e956-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Ativar os Serviços de Domínio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="7e956-115">Quando ativar o Azure Active Directory Domain Services para o seu inquilino, o Azure AD gera e armazena Olá Kerberos e NTLM hashes de credencial necessários para autenticar utilizadores.</span><span class="sxs-lookup"><span data-stu-id="7e956-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="7e956-116">Especifique Olá **nome de domínio DNS dos serviços de domínio**.</span><span class="sxs-lookup"><span data-stu-id="7e956-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="7e956-117">nome de domínio predefinido Olá do diretório de Olá (com um **. onmicrosoft.com** sufixo) está selecionado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="7e956-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="7e956-118">Olá lista contém todos os domínios que tenham sido configurados para o diretório do Azure AD, incluindo ambos verificados e não verificado os domínios que configura num Olá **domínios** separador.</span><span class="sxs-lookup"><span data-stu-id="7e956-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="7e956-119">Também pode introduzir um nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="7e956-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="7e956-120">Neste exemplo, é o nome de domínio personalizado de Olá *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="7e956-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="7e956-121">prefixo de Olá do seu nome de domínio especificado (por exemplo, *contoso100* no Olá *contoso100.com* nome de domínio) tem de conter 15 ou menos carateres.</span><span class="sxs-lookup"><span data-stu-id="7e956-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="7e956-122">Não pode criar um domínio do Azure Active Directory Domain Services com um prefixo que contenha mais do que 15 carateres.</span><span class="sxs-lookup"><span data-stu-id="7e956-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="7e956-123">Certifique-se de que nome de domínio DNS Olá que escolheu para Olá gerido domínio ainda não existir na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="7e956-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="7e956-124">Especificamente, verifique se o toosee:</span><span class="sxs-lookup"><span data-stu-id="7e956-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="7e956-125">Já tiver um domínio com Olá mesmo nome de domínio DNS na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="7e956-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="7e956-126">Olá que selecionou a rede virtual tem uma ligação VPN à sua rede no local e, se tiver um domínio com Olá mesmo nome de domínio DNS na sua rede no local.</span><span class="sxs-lookup"><span data-stu-id="7e956-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="7e956-127">Tem um serviço em nuvem existente com esse nome na rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="7e956-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="7e956-128">Selecione uma rede virtual no qual pretende que o Azure Active Directory Domain Services toobe disponível.</span><span class="sxs-lookup"><span data-stu-id="7e956-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="7e956-129">Selecione a rede virtual Olá e sub-rede dedicada que criou no Olá **toothis de rede virtual de serviços de domínio do Connect** na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="7e956-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="7e956-130">Considere também a seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="7e956-130">Also consider hello following:</span></span>

   * <span data-ttu-id="7e956-131">Certifique-se a rede virtual Olá que especificou pertence tooan região do Azure que é suportado pelo Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="7e956-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="7e956-132">tooascertain Olá regiões do Azure onde os serviços de domínio do Active Directory do Azure está disponível, consulte [serviços do Azure por região](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="7e956-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="7e956-133">Redes virtuais que pertencem a região tooa onde o Azure Active Directory Domain Services não é suportado não aparecer na Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="7e956-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="7e956-134">Utilize uma sub-rede numa rede virtual Olá dedicada para o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="7e956-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="7e956-135">Efetue *não* selecione Olá sub-rede do gateway.</span><span class="sxs-lookup"><span data-stu-id="7e956-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="7e956-136">Veja [considerações de redes](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="7e956-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="7e956-137">Da mesma forma, redes virtuais que foram criadas utilizando o Gestor de recursos do Azure não aparecem na Olá na lista pendente.</span><span class="sxs-lookup"><span data-stu-id="7e956-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="7e956-138">O Azure Active Directory Domain Services não suporta redes virtuais baseadas no ARM atualmente.</span><span class="sxs-lookup"><span data-stu-id="7e956-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="7e956-139">Clique em tooenable do Azure Active Directory Domain Services, no painel de tarefas de Olá na Olá parte inferior da página Olá, **guardar**.</span><span class="sxs-lookup"><span data-stu-id="7e956-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="7e956-140">Enquanto o Azure Active Directory Domain Services está a ser ativado para o seu diretório, a página Olá apresenta um Estado de *pendente*.</span><span class="sxs-lookup"><span data-stu-id="7e956-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Ativar a janela dos Serviços de Domínio](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="7e956-142">O Azure Active Directory Domain Services fornece elevada disponibilidade para o seu domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="7e956-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="7e956-143">Depois de ativar o Azure Active Directory Domain Services, endereços IP Olá no qual o domínio serviços estão disponíveis na rede virtual Olá são apresentado um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="7e956-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="7e956-144">endereço IP segundo Olá é apresentado em breve após Olá em primeiro lugar, como logo que o serviço de Olá permite elevada disponibilidade para o seu domínio.</span><span class="sxs-lookup"><span data-stu-id="7e956-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="7e956-145">Quando a elevada disponibilidade está configurada e Active Directory para o seu domínio, deverá ver dois endereços IP na Olá **dos serviços de domínio** secção Olá **configurar** separador.</span><span class="sxs-lookup"><span data-stu-id="7e956-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="7e956-146">Depois de cerca de 20 too30 minutos, Olá primeiro endereço IP no qual o domínio serviços estão disponíveis na sua rede virtual no Olá **endereço IP** campo no Olá **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="7e956-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Janela dos Serviços de Domínio apresenta primeiro IP aprovisionado](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="7e956-148">Quando a elevada disponibilidade está operacional para o seu domínio, dois endereços IP são apresentados na página Olá.</span><span class="sxs-lookup"><span data-stu-id="7e956-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="7e956-149">O domínio gerido está disponível na rede virtual selecionada nestes dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="7e956-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="7e956-150">Tenha em atenção dois endereços IP Olá, de modo a que possa atualizar as definições de DNS Olá na sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="7e956-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="7e956-151">Se o fizer, permite que as máquinas virtuais no domínio toohello de tooconnect de rede virtual do Olá para operações como associação a um domínio.</span><span class="sxs-lookup"><span data-stu-id="7e956-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Janela dos Serviços de Domínio apresenta ambos os IPs aprovisionados](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="7e956-153">Dependendo do tamanho de Olá do inquilino do Azure AD (por exemplo, número de Olá de utilizadores ou grupos), o domínio gerido de tooyour de sincronização demora algum tempo.</span><span class="sxs-lookup"><span data-stu-id="7e956-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="7e956-154">Este processo de sincronização ocorre em segundo plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e956-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="7e956-155">Para inquilinos grandes, com dezenas de milhares de objetos, poderá demorar um dia ou dois para todos os utilizadores, as associações de grupo e toobe credenciais sincronizados.</span><span class="sxs-lookup"><span data-stu-id="7e956-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="7e956-156">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="7e956-156">Next step</span></span>
[<span data-ttu-id="7e956-157">Tarefa 4: atualizar as definições de DNS de Olá de Olá rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="7e956-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
