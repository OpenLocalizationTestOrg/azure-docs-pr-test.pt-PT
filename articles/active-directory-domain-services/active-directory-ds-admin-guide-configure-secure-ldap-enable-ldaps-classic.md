---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do Azure AD | Microsoft Docs"
description: "Configurar o LDAP seguro (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2abf0-103">Configurar segura LDAP (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2abf0-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2abf0-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2abf0-104">Before you begin</span></span>
<span data-ttu-id="2abf0-105">Certifique-se de que concluiu [tarefa 2 - exportação Olá segura LDAP certificado tooa. Ficheiro PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="2abf0-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="2abf0-106">Optar por toouse Olá pré-visualização experiência do portal do Azure ou Olá toocomplete de portal clássico do Azure esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="2abf0-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="2abf0-107">**Portal do Azure (pré-visualização)**: [Enable secure LDAP utilizando Olá portal do Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="2abf0-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="2abf0-108">**Portal clássico do Azure**: [Enable secure LDAP utilizando o portal clássico do Azure Olá](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="2abf0-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="2abf0-109">Tarefa 3 - ativar LDAP seguro para Olá domínio gerido utilizando o portal clássico do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="2abf0-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="2abf0-110">tooenable LDAP seguro, execute os seguintes passos de configuração de Olá:</span><span class="sxs-lookup"><span data-stu-id="2abf0-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="2abf0-111">Navegue toohello  **[portal clássico do Azure](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="2abf0-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="2abf0-112">Selecione Olá **do Active Directory** nós no painel esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="2abf0-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="2abf0-113">Selecione o diretório de Olá do Azure AD (também referida tooas "tenant"), para que tiver ativado os serviços de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2abf0-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Selecionar o Azure AD Directory](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="2abf0-115">Clique em Olá **configurar** separador.</span><span class="sxs-lookup"><span data-stu-id="2abf0-115">Click hello **Configure** tab.</span></span>

    ![Separador Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="2abf0-117">Desloque para baixo toohello secção intitulada **dos serviços de domínio**.</span><span class="sxs-lookup"><span data-stu-id="2abf0-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="2abf0-118">Deverá ver uma opção intitulada **LDAP seguro (LDAPS)** conforme mostrado na seguinte captura de ecrã de Olá:</span><span class="sxs-lookup"><span data-stu-id="2abf0-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Secção de configuração dos Serviços de Domínio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="2abf0-120">Clique em Olá **configurar certificado...**  botão toobring segurança Olá **configurar certificados para proteger o LDAP** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2abf0-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configurar o certificado para o LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="2abf0-122">Clique em seguinte de ícone de pasta Olá **ficheiro com um certificado PFX** toospecify Olá PFX ficheiro que contém o certificado Olá desejar toouse para toohello de acesso LDAP seguro geridos domínio.</span><span class="sxs-lookup"><span data-stu-id="2abf0-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="2abf0-123">Também introduza a palavra-passe de Olá que especificou ao exportar o ficheiro do Olá certificado toohello PFX.</span><span class="sxs-lookup"><span data-stu-id="2abf0-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="2abf0-124">Em seguida, clique em Olá feito botão na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="2abf0-124">Then, click hello done button on hello bottom.</span></span>

    ![Especifique o ficheiro de LDAP PFX seguro e a palavra-passe](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="2abf0-126">Olá **dos serviços de domínio** secção Olá **configurar** separador deve obter cinzento e está a ser Olá **pendentes...**  Estado alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2abf0-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="2abf0-127">Durante este período, certificado LDAPS Olá é verificado em termos de exatidão e segura LDAP estiver configurado para o seu domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="2abf0-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![Proteger o LDAP - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="2abf0-129">Demora cerca de 10 minutos de too15 tooenable proteger LDAP para o seu domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="2abf0-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="2abf0-130">Se Olá fornecido não corresponde ao certificado LDAP seguro Olá necessário critérios, LDAP seguro não está ativada para o seu diretório e verá uma falha.</span><span class="sxs-lookup"><span data-stu-id="2abf0-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="2abf0-131">Por exemplo, nome de domínio Olá está incorreto, certificado Olá já expirou ou expira em breve.</span><span class="sxs-lookup"><span data-stu-id="2abf0-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="2abf0-132">Quando o LDAP seguro está ativado com êxito para o seu domínio gerido, Olá **pendentes...**  deve desaparecer mensagem.</span><span class="sxs-lookup"><span data-stu-id="2abf0-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="2abf0-133">Deverá ver Olá impressão digital do certificado de Olá apresentado.</span><span class="sxs-lookup"><span data-stu-id="2abf0-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="2abf0-135">Tarefa 4 - ativar o acesso LDAP seguro através de Olá internet</span><span class="sxs-lookup"><span data-stu-id="2abf0-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="2abf0-136">**Tarefas opcionais** - se não planear tooaccess Olá domínio gerido utilizando LDAPS mais Olá internet, ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="2abf0-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="2abf0-137">Antes de começar esta tarefa, certifique-se de que concluiu os passos de Olá descritos em [tarefa 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="2abf0-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="2abf0-138">Deverá ver uma opção demasiado**ATIVAR SECURE LDAP acesso através de Olá INTERNET** no Olá **dos serviços de domínio** secção Olá **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="2abf0-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="2abf0-139">Esta opção estiver definida demasiado**não** por predefinição, uma vez que toohello de acesso à internet geridos domínio através de LDAP seguro está desativado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="2abf0-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="2abf0-141">Ativar/desativar **ATIVAR SECURE LDAP acesso através de Olá INTERNET** demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="2abf0-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="2abf0-142">Clique em Olá **guardar** botão no painel inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="2abf0-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="2abf0-143">![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="2abf0-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="2abf0-144">Olá **dos serviços de domínio** secção Olá **configurar** separador deve obter cinzento e está a ser Olá **pendentes...**  Estado alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2abf0-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="2abf0-145">Após algum tempo, internet acesso tooyour domínio gerido através de LDAP seguro está ativado.</span><span class="sxs-lookup"><span data-stu-id="2abf0-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![Proteger o LDAP - estado pendente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="2abf0-147">Demora cerca de 10 minutos tooenable acesso à internet através de LDAP seguro para o seu domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="2abf0-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="2abf0-148">Quando tooyour de acesso LDAP seguro efectuada domínio Olá internet é ativada com êxito, Olá **pendentes...**  deve desaparecer mensagem.</span><span class="sxs-lookup"><span data-stu-id="2abf0-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="2abf0-149">Deverá ver Olá IP externo de endereços que podem ser o diretório de tooaccess utilizados por LDAPS no campo Olá **IP endereço para LDAPS acesso externo**.</span><span class="sxs-lookup"><span data-stu-id="2abf0-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP seguro ativado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="2abf0-151">Tarefa 5 - configurar o DNS tooaccess Olá domínio gerido de Olá internet</span><span class="sxs-lookup"><span data-stu-id="2abf0-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="2abf0-152">**Tarefas opcionais** - se não planear tooaccess Olá domínio gerido utilizando LDAPS mais Olá internet, ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="2abf0-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="2abf0-153">Antes de começar esta tarefa, certifique-se de que concluiu os passos de Olá descritos em [Tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="2abf0-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="2abf0-154">Assim que tiver ativado o acesso LDAP seguro através de Olá internet para o seu domínio gerido, terá de tooupdate DNS para que os computadores cliente possam localizar este domínio gerido.</span><span class="sxs-lookup"><span data-stu-id="2abf0-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="2abf0-155">No final Olá Tarefa 4, um endereço IP externo é apresentado no Olá **configurar** separador **IP endereço para LDAPS acesso externo**.</span><span class="sxs-lookup"><span data-stu-id="2abf0-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="2abf0-156">Configure o seu fornecedor de DNS externo para que esse nome DNS Olá de Olá geridos endereço IP externo do domínio (por exemplo, ' ldaps.contoso100.com') toothis pontos.</span><span class="sxs-lookup"><span data-stu-id="2abf0-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="2abf0-157">No nosso exemplo, é preciso Olá toocreate seguir a entrada DNS:</span><span class="sxs-lookup"><span data-stu-id="2abf0-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="2abf0-158">Já está - está agora toohello tooconnect pronto gerido Olá de domínio utilizando o LDAP seguro através de internet.</span><span class="sxs-lookup"><span data-stu-id="2abf0-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="2abf0-159">Lembre-se de que os computadores cliente têm de confiar emissor Olá de Olá LDAPS certificado toobe capaz de tooconnect com êxito toohello gerido a utilizar o LDAPS do domínio.</span><span class="sxs-lookup"><span data-stu-id="2abf0-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="2abf0-160">Se estiver a utilizar uma autoridade de certificação empresarial ou uma autoridade de certificação publicamente fidedigna, não terá toodo nada, uma vez que os computadores cliente confiar estes emissores de certificados.</span><span class="sxs-lookup"><span data-stu-id="2abf0-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="2abf0-161">Se estiver a utilizar um certificado autoassinado, terá de tooinstall Olá pública faz parte do certificado autoassinado Olá no arquivo de certificados fidedignos Olá no computador de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="2abf0-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="2abf0-162">Bloqueio pendente LDAPS aceder domínio gerido tooyour através de Olá internet</span><span class="sxs-lookup"><span data-stu-id="2abf0-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="2abf0-163">**Tarefas opcionais** - se não tiver ativado o LDAPS domínio gerido do acesso toohello mais Olá internet, ignorar esta tarefa de configuração.</span><span class="sxs-lookup"><span data-stu-id="2abf0-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="2abf0-164">Antes de começar esta tarefa, certifique-se de que concluiu os passos de Olá descritos em [Tarefa 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="2abf0-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="2abf0-165">A exposição do seu domínio gerido para o acesso LDAPS através de Olá internet representa uma ameaça de segurança.</span><span class="sxs-lookup"><span data-stu-id="2abf0-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="2abf0-166">Olá domínio gerido está acessível a partir do Olá internet na porta de Olá utilizada para o LDAP seguro (ou seja, porta 636).</span><span class="sxs-lookup"><span data-stu-id="2abf0-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="2abf0-167">Por conseguinte, pode escolher toorestrict acesso toohello gerido domínio toospecific conhecido endereços IP.</span><span class="sxs-lookup"><span data-stu-id="2abf0-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="2abf0-168">Para segurança melhorada, crie um grupo de segurança de rede (NSG) e associá-la a sub-rede de olá onde tiver ativado os serviços de domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2abf0-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="2abf0-169">Olá tabela a seguir ilustra um exemplo NSG pode configurar, toolock para baixo de acesso LDAP seguro através de Olá internet.</span><span class="sxs-lookup"><span data-stu-id="2abf0-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="2abf0-170">Olá NSG contém um conjunto de regras que permitem acesso de entrada de LDAPS através da porta TCP 636 apenas a partir de um conjunto especificado de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="2abf0-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="2abf0-171">Olá predefinido 'DenyAll' regra aplica-se tooall outro tráfego de entrada de Olá internet.</span><span class="sxs-lookup"><span data-stu-id="2abf0-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="2abf0-172">Olá NSG regra tooallow LDAPS acesso através de Olá internet a partir de endereços IP especificados tem uma prioridade superior à Olá regra DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="2abf0-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Olá, acesso LDAPS do exemplo NSG toosecure pela internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="2abf0-174">**Obter mais informações** - [grupos de segurança de rede](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="2abf0-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="2abf0-175">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="2abf0-175">Related content</span></span>
* [<span data-ttu-id="2abf0-176">Serviços de domínio do Azure AD - guia de introdução</span><span class="sxs-lookup"><span data-stu-id="2abf0-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2abf0-177">Administrar um domínio gerido dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2abf0-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="2abf0-178">Administrar a política de grupo num domínio gerido dos serviços de domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2abf0-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="2abf0-179">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="2abf0-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2abf0-180">Criar um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="2abf0-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
