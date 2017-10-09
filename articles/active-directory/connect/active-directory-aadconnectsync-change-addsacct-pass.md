---
title: "Sincronização do Azure AD Connect: a alteração Olá AD DS conta palavra-passe de | Microsoft Docs"
description: "Este documento de tópico descreve como tooupdate do Azure AD Connect após Olá palavra-passe da conta de Olá do AD DS é alterado."
services: active-directory
keywords: Conta do AD DS, a conta do Active Directory, a palavra-passe
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="57c27-104">A alteração de palavra-passe de conta do Olá AD DS</span><span class="sxs-lookup"><span data-stu-id="57c27-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="57c27-105">conta do Olá AD DS refere-se a conta de utilizador toohello utilizada pelo Azure AD Connect toocommunicate com o Active Directory no local.</span><span class="sxs-lookup"><span data-stu-id="57c27-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="57c27-106">Se alterar Olá palavra-passe da conta do AD DS de Olá, tem de atualizar o serviço de sincronização ligar do Azure AD com a nova palavra-passe Olá.</span><span class="sxs-lookup"><span data-stu-id="57c27-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="57c27-107">Caso contrário, Olá que sincronização já não pode sincronizar corretamente com Olá no local do Active Directory e irá encontrar Olá seguintes erros:</span><span class="sxs-lookup"><span data-stu-id="57c27-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="57c27-108">No Olá operação Synchronization Service Manager, qualquer importação ou exportação com no local irá falhar do AD com **credenciais de início não** erro.</span><span class="sxs-lookup"><span data-stu-id="57c27-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="57c27-109">No Visualizador de eventos do Windows, o registo de eventos de aplicações de Olá contém um erro com **6000 de ID de evento** e mensagem **'agente de gestão de Olá "contoso.com" Falha toorun porque as credenciais de Olá foram inválidas'** .</span><span class="sxs-lookup"><span data-stu-id="57c27-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="57c27-110">Como tooupdate Olá serviço de sincronização com a nova palavra-passe para a conta do AD DS</span><span class="sxs-lookup"><span data-stu-id="57c27-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="57c27-111">tooupdate Olá serviço de sincronização com a nova palavra-passe Olá:</span><span class="sxs-lookup"><span data-stu-id="57c27-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="57c27-112">Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).</span><span class="sxs-lookup"><span data-stu-id="57c27-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="57c27-113">![Gestor do serviço de sincronização](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="57c27-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="57c27-114">Aceda toohello **conectores** separador.</span><span class="sxs-lookup"><span data-stu-id="57c27-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="57c27-115">Selecione Olá **conector AD** que corresponde à conta do toohello AD DS para o qual a respetiva palavra-passe foi alterada.</span><span class="sxs-lookup"><span data-stu-id="57c27-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="57c27-116">Em **ações**, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="57c27-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="57c27-117">Na caixa de diálogo pop-up de Olá, selecione **ligar tooActive diretório floresta**:</span><span class="sxs-lookup"><span data-stu-id="57c27-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="57c27-118">Introduza Olá nova palavra-passe da conta de Olá do AD DS no Olá **palavra-passe** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="57c27-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="57c27-119">Clique em **OK** toosave Olá nova palavra-passe e a caixa de diálogo de pop-up Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="57c27-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="57c27-120">Reinício hello do Azure AD Connect serviço de sincronização em Gestor de controlo de serviço do Windows.</span><span class="sxs-lookup"><span data-stu-id="57c27-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="57c27-121">Este é tooensure que qualquer referência toohello palavra-passe antiga é removido da cache de memória de Olá.</span><span class="sxs-lookup"><span data-stu-id="57c27-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57c27-122">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="57c27-122">Next steps</span></span>
<span data-ttu-id="57c27-123">**Tópicos de descrição geral**</span><span class="sxs-lookup"><span data-stu-id="57c27-123">**Overview topics**</span></span>

* [<span data-ttu-id="57c27-124">Sincronização do Azure AD Connect: Noções e personalizar a sincronização</span><span class="sxs-lookup"><span data-stu-id="57c27-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="57c27-125">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57c27-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
