---
title: "Novamente executar Assistente de instalação de Olá do Azure AD Connect | Microsoft Docs"
description: "Explica como o Assistente de instalação de Olá funciona Olá segunda vez que executá-la."
keywords: "Assistente de instalação do Olá do Azure AD Connect permite-lhe configurar Olá de definições de manutenção segunda vez que executá-la"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="e1b6d-104">Sincronização do Azure AD Connect: executar o Assistente de instalação de Olá uma segunda vez</span><span class="sxs-lookup"><span data-stu-id="e1b6d-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="e1b6d-105">Olá pela primeira vez, execute o Assistente de instalação do Olá do Azure AD Connect, explica como tooconfigure a instalação.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="e1b6d-106">Se executar novamente o Assistente de instalação de Olá, oferece opções de manutenção.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="e1b6d-107">Pode encontrar o Assistente de instalação de Olá no menu de início de Olá denominado **do Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Menu Iniciar](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="e1b6d-109">Quando iniciar o Assistente de instalação de Olá, verá uma página com estas opções:</span><span class="sxs-lookup"><span data-stu-id="e1b6d-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Página com uma lista de tarefas adicionais](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="e1b6d-111">Se tiver instalado o AD FS com o Azure AD Connect, terá ainda mais opções.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="e1b6d-112">Olá opções adicionais tiver para AD FS estão documentados na [gestão ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="e1b6d-113">Selecione uma das tarefas de Olá e clique em **seguinte** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1b6d-114">Enquanto tiver o Assistente de instalação de Olá abrir, todas as operações no motor de sincronização de Olá são suspensas.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="e1b6d-115">Certifique-se que fechar o Assistente de instalação de Olá, assim que concluir as alterações de configuração.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="e1b6d-116">Ver a configuração atual</span><span class="sxs-lookup"><span data-stu-id="e1b6d-116">View current configuration</span></span>
<span data-ttu-id="e1b6d-117">Esta opção fornece-lhe uma vista rápida do que as suas opções atualmente configuradas.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-117">This option gives you a quick view of your currently configured options.</span></span>

![Página com uma lista de todas as opções e o respetivo estado](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="e1b6d-119">Clique em **anterior** toogo anterior.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="e1b6d-120">Se selecionar **saída**, feche o Assistente de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="e1b6d-121">Personalizar opções de sincronização</span><span class="sxs-lookup"><span data-stu-id="e1b6d-121">Customize synchronization options</span></span>
<span data-ttu-id="e1b6d-122">Esta opção é a configuração da sincronização toomake utilizados alterações toohello.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="e1b6d-123">Verá um subconjunto das opções a partir do caminho de instalação do Olá configuração personalizada.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="e1b6d-124">Ver esta opção, mesmo se tiver utilizado inicialmente instalação rápida.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="e1b6d-125">[Adicionar mais diretórios](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="e1b6d-126">Para remover um diretório, consulte [eliminar um conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="e1b6d-127">[Alterar o domínio e a UO filtragem](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="e1b6d-128">Remova a filtragem de grupos.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-128">Remove Group filtering.</span></span>
* <span data-ttu-id="e1b6d-129">[Alterar as funcionalidades opcionais](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="e1b6d-130">Olá outras opções de instalação inicial Olá não podem ser alteradas e não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="e1b6d-131">Estas opções são:</span><span class="sxs-lookup"><span data-stu-id="e1b6d-131">These options are:</span></span>

* <span data-ttu-id="e1b6d-132">Alterar o atributo de Olá toouse para userPrincipalName e sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="e1b6d-133">Alterar Olá associar método destinada a objetos da floresta diferente.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="e1b6d-134">Ative a filtragem baseada no grupo.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="e1b6d-135">Atualizar o esquema de diretório</span><span class="sxs-lookup"><span data-stu-id="e1b6d-135">Refresh directory schema</span></span>
<span data-ttu-id="e1b6d-136">Esta opção é utilizada se tiver alterado o esquema de Olá dos seus no local florestas do AD DS.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="e1b6d-137">Por exemplo, poderá ter instalado o Exchange ou atualizado o esquema de tooa Windows Server 2012 com objetos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="e1b6d-138">Neste caso, tem de esquema do tooinstruct do Azure AD Connect tooread Olá novamente do AD DS e atualizar a sua cache.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="e1b6d-139">Esta ação gera também de novo Olá regras de sincronização.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="e1b6d-140">Se adicionar o esquema do Exchange Olá, por exemplo, as regras de sincronização de Olá para o Exchange estão adicionadas toohello configuração.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="e1b6d-141">Quando seleciona esta opção, são listados todos os diretórios de Olá na configuração.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="e1b6d-142">Pode manter a predefinição de Olá e atualizar todas as florestas ou anule a seleção de algumas delas.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Página com uma lista de todos os diretórios no ambiente de Olá](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="e1b6d-144">Configurar o modo de teste</span><span class="sxs-lookup"><span data-stu-id="e1b6d-144">Configure staging mode</span></span>
<span data-ttu-id="e1b6d-145">Esta opção permite-lhe tooenable e desativar o modo de teste no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="e1b6d-146">Podem encontrar mais informações sobre testes de modo e como são utilizadas no [operações](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="e1b6d-147">opção de Olá mostra se o teste está atualmente ativada ou desativada:</span><span class="sxs-lookup"><span data-stu-id="e1b6d-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Opção que também está a mostrar o estado atual do Olá do modo de teste](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="e1b6d-149">toochange Olá Estado, selecione esta opção e selecione ou unselect Olá caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Opção que também está a mostrar o estado atual do Olá do modo de teste](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="e1b6d-151">Alterar a sessão do utilizador</span><span class="sxs-lookup"><span data-stu-id="e1b6d-151">Change user sign-in</span></span>
<span data-ttu-id="e1b6d-152">Esta opção permite-lhe toochange toofederation de sincronização de palavra-passe ou Olá inverso.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="e1b6d-153">Não é possível alterar demasiado**não configurar**.</span><span class="sxs-lookup"><span data-stu-id="e1b6d-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="e1b6d-154">Para obter mais informações sobre esta opção, consulte [sessão do utilizador](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1b6d-155">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e1b6d-155">Next steps</span></span>
* <span data-ttu-id="e1b6d-156">Saiba mais sobre o modelo de configuração de Olá utilizado por uma sincronização do Azure AD Connect no [compreender de aprovisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="e1b6d-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="e1b6d-157">**Tópicos de descrição geral**</span><span class="sxs-lookup"><span data-stu-id="e1b6d-157">**Overview topics**</span></span>

* [<span data-ttu-id="e1b6d-158">Sincronização do Azure AD Connect: Noções e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="e1b6d-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="e1b6d-159">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1b6d-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
