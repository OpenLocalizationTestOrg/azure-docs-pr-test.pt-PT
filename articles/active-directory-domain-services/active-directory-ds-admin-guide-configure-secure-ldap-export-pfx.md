---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do Azure AD | Microsoft Docs"
description: "Configurar o LDAP seguro (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="568eb-103">Configurar segura LDAP (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="568eb-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="568eb-104">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="568eb-104">Before you begin</span></span>
<span data-ttu-id="568eb-105">Certifique-se de que concluiu [tarefa 1 - obter um certificado para o LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="568eb-105">Ensure you've completed [Task 1 - obtain a certificate for secure LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).</span></span>


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a><span data-ttu-id="568eb-106">Tarefa 2 - exportar Olá segura LDAP certificado tooa. Ficheiro PFX</span><span class="sxs-lookup"><span data-stu-id="568eb-106">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>
<span data-ttu-id="568eb-107">Antes de começar esta tarefa, certifique-se de que adquiriu o certificado LDAP seguro Olá de uma autoridade de certificação pública ou tiver criado um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="568eb-107">Before you start this task, ensure that you have obtained hello secure LDAP certificate from a public certification authority or have created a self-signed certificate.</span></span>

<span data-ttu-id="568eb-108">Efetuar Olá os seguintes passos, tooexport Olá LDAPS tooa de certificado. Ficheiro PFX.</span><span class="sxs-lookup"><span data-stu-id="568eb-108">Perform hello following steps, tooexport hello LDAPS certificate tooa .PFX file.</span></span>

1. <span data-ttu-id="568eb-109">Olá prima **iniciar** botão e tipo **R**. No Olá **executar** caixa de diálogo, escreva **mmc** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="568eb-109">Press hello **Start** button and type **R**. In hello **Run** dialog, type **mmc** and click **OK**.</span></span>

    ![Iniciar a consola do MMC Olá](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. <span data-ttu-id="568eb-111">No Olá **controlo de conta de utilizador** linha de comandos, clique em **Sim** toolaunch MMC (Consola de gestão da Microsoft) como administrador.</span><span class="sxs-lookup"><span data-stu-id="568eb-111">On hello **User Account Control** prompt, click **YES** toolaunch MMC (Microsoft Management Console) as administrator.</span></span>
3. <span data-ttu-id="568eb-112">De Olá **ficheiro** menu, clique em **Adicionar/Remover Snap-in...** .</span><span class="sxs-lookup"><span data-stu-id="568eb-112">From hello **File** menu, click **Add/Remove Snap-in...**.</span></span>

    ![Adicionar a consola do snap-in tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. <span data-ttu-id="568eb-114">No Olá **adicionar ou Remover Snap-ins** caixa de diálogo, selecione de Olá **certificados** snap-in e clique em Olá **adicionar >** botão.</span><span class="sxs-lookup"><span data-stu-id="568eb-114">In hello **Add or Remove Snap-ins** dialog, select hello **Certificates** snap-in, and click hello **Add >** button.</span></span>

    ![Adicionar a consola do snap-in tooMMC de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. <span data-ttu-id="568eb-116">No Olá **snap-in de certificados** assistente, selecione **conta de computador** e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="568eb-116">In hello **Certificates snap-in** wizard, select **Computer account** and click **Next**.</span></span>

    ![Adicionar snap-in de certificados para conta de computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. <span data-ttu-id="568eb-118">No Olá **selecionar computador** página, selecione **computador Local: (Olá computador em que esta consola está a ser executada)** e clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="568eb-118">On hello **Select Computer** page, select **Local computer: (hello computer this console is running on)** and click **Finish**.</span></span>

    ![Adicionar snap-in Certificados - computador Selecione](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. <span data-ttu-id="568eb-120">No Olá **adicionar ou Remover Snap-ins** caixa de diálogo, clique em **OK** tooadd Olá certificados snap-in tooMMC.</span><span class="sxs-lookup"><span data-stu-id="568eb-120">In hello **Add or Remove Snap-ins** dialog, click **OK** tooadd hello certificates snap-in tooMMC.</span></span>

    ![Adicione certificados snap-in tooMMC - concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. <span data-ttu-id="568eb-122">Na janela MMC Olá, clique em tooexpand **raiz da consola**.</span><span class="sxs-lookup"><span data-stu-id="568eb-122">In hello MMC window, click tooexpand **Console Root**.</span></span> <span data-ttu-id="568eb-123">Deverá ver Olá snap-in de certificados carregados.</span><span class="sxs-lookup"><span data-stu-id="568eb-123">You should see hello Certificates snap-in loaded.</span></span> <span data-ttu-id="568eb-124">Clique em **certificados (computador Local)** tooexpand.</span><span class="sxs-lookup"><span data-stu-id="568eb-124">Click **Certificates (Local Computer)** tooexpand.</span></span> <span data-ttu-id="568eb-125">Clique em tooexpand Olá **pessoais** nó, seguido de Olá **certificados** nós.</span><span class="sxs-lookup"><span data-stu-id="568eb-125">Click tooexpand hello **Personal** node, followed by hello **Certificates** node.</span></span>

    ![Arquivo de certificados pessoais aberta](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. <span data-ttu-id="568eb-127">Deverá ver o certificado autoassinado Olá que foi criada.</span><span class="sxs-lookup"><span data-stu-id="568eb-127">You should see hello self-signed certificate we created.</span></span> <span data-ttu-id="568eb-128">Pode examinar propriedades de Olá de Olá certificado tooensure Olá thumbprint correspondências que comunicaram no windows PowerShell de Olá quando criou o certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="568eb-128">You can examine hello properties of hello certificate tooensure hello thumbprint matches that reported on hello PowerShell windows when you created hello certificate.</span></span>
10. <span data-ttu-id="568eb-129">Selecione Olá certificado autoassinado e **certo**.</span><span class="sxs-lookup"><span data-stu-id="568eb-129">Select hello self-signed certificate and **right click**.</span></span> <span data-ttu-id="568eb-130">No menu de contexto de Olá, selecione **todas as tarefas** e selecione **exportar...** .</span><span class="sxs-lookup"><span data-stu-id="568eb-130">From hello right-click menu, select **All Tasks** and select **Export...**.</span></span>

    ![Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. <span data-ttu-id="568eb-132">No Olá **Assistente para exportar certificados**, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="568eb-132">In hello **Certificate Export Wizard**, click **Next**.</span></span>

    ![Assistente de exportação de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. <span data-ttu-id="568eb-134">No Olá **exportar chave privada** página, selecione **Sim, exportar a chave privada Olá**e clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="568eb-134">On hello **Export Private Key** page, select **Yes, export hello private key**, and click **Next**.</span></span>

    ![Exportar chave privada do certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > <span data-ttu-id="568eb-136">TEM de exportar chave privada do Olá, juntamente com o certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="568eb-136">You MUST export hello private key along with hello certificate.</span></span> <span data-ttu-id="568eb-137">Se fornecer um PFX que contém Olá chave privada do certificado de Olá, ativar LDAP seguro para o seu domínio gerido irá falhar.</span><span class="sxs-lookup"><span data-stu-id="568eb-137">If you provide a PFX that does not contain hello private key for hello certificate, enabling secure LDAP for your managed domain fails.</span></span>
    >
    >
13. <span data-ttu-id="568eb-138">No Olá **exportar formato de ficheiro** página, selecione **Personal Information Exchange - PKCS #12 (. PFX)** como formato de ficheiro Olá para Olá o certificado exportado.</span><span class="sxs-lookup"><span data-stu-id="568eb-138">On hello **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)** as hello file format for hello exported certificate.</span></span>

    ![Exportar formato de ficheiro de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > <span data-ttu-id="568eb-140">Apenas Olá. Formato de ficheiro PFX é suportado.</span><span class="sxs-lookup"><span data-stu-id="568eb-140">Only hello .PFX file format is supported.</span></span> <span data-ttu-id="568eb-141">Não exporta Olá toohello de certificado. Formato de ficheiro CER.</span><span class="sxs-lookup"><span data-stu-id="568eb-141">Do not export hello certificate toohello .CER file format.</span></span>
    >
    >
14. <span data-ttu-id="568eb-142">No Olá **segurança** página, selecione de Olá **palavra-passe** opção e escreva um Olá tooprotect de palavra-passe. Ficheiro PFX.</span><span class="sxs-lookup"><span data-stu-id="568eb-142">On hello **Security** page, select hello **Password** option and type in a password tooprotect hello .PFX file.</span></span> <span data-ttu-id="568eb-143">Uma vez que é necessária na próxima tarefa de Olá, lembre-se desta palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="568eb-143">Remember this password since it will be needed in hello next task.</span></span> <span data-ttu-id="568eb-144">Clique em **seguinte** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="568eb-144">Click **Next** tooproceed.</span></span>

    ![<span data-ttu-id="568eb-145">Palavra-passe para exportar certificados</span><span class="sxs-lookup"><span data-stu-id="568eb-145">Password for certificate export</span></span> ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > <span data-ttu-id="568eb-146">Tome nota desta palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="568eb-146">Make a note of this password.</span></span> <span data-ttu-id="568eb-147">Precisa ao ativar o LDAP seguro para este domínio gerido no [tarefa 3 - ativar LDAP seguro para domínio Olá de gerido](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="568eb-147">You need it while enabling secure LDAP for this managed domain in [Task 3 - enable secure LDAP for hello managed domain](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
    >
    >
15. <span data-ttu-id="568eb-148">No Olá **ficheiro tooExport** página, especifique o nome de ficheiro Olá e a localização onde pretende que o certificado de Olá tooexport.</span><span class="sxs-lookup"><span data-stu-id="568eb-148">On hello **File tooExport** page, specify hello file name and location where you'd like tooexport hello certificate.</span></span>

    ![Caminho para exportar certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. <span data-ttu-id="568eb-150">Olá seguir página, clique em **concluir** ficheiro do tooexport Olá certificado tooa PFX.</span><span class="sxs-lookup"><span data-stu-id="568eb-150">On hello following page, click **Finish** tooexport hello certificate tooa PFX file.</span></span> <span data-ttu-id="568eb-151">Deverá ver a caixa de diálogo de confirmação quando o certificado de Olá foi exportado.</span><span class="sxs-lookup"><span data-stu-id="568eb-151">You should see confirmation dialog when hello certificate has been exported.</span></span>

    ![Exportar certificado concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a><span data-ttu-id="568eb-153">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="568eb-153">Next step</span></span>
[<span data-ttu-id="568eb-154">Tarefa 3 - ativar LDAP seguro para domínio Olá de gerido</span><span class="sxs-lookup"><span data-stu-id="568eb-154">Task 3 - enable secure LDAP for hello managed domain</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
