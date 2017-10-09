---
title: certificados de aaaUsing com Enterprise Integration Pack | Microsoft Docs
description: "Saiba como toouse certificados com Olá Enterprise Integration Pack | Aplicações lógicas do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="d133c-103">Mais informações sobre certificados e o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d133c-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="d133c-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="d133c-104">Overview</span></span>
<span data-ttu-id="d133c-105">Integração empresarial com utiliza comunicações de B2B toosecure de certificados.</span><span class="sxs-lookup"><span data-stu-id="d133c-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="d133c-106">Pode utilizar dois tipos de certificados nas suas aplicações de integração do enterprise:</span><span class="sxs-lookup"><span data-stu-id="d133c-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="d133c-107">Certificados públicos, tem de ser adquiridos de uma autoridade de certificação (AC).</span><span class="sxs-lookup"><span data-stu-id="d133c-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="d133c-108">Certificados privados, pode emitir por si.</span><span class="sxs-lookup"><span data-stu-id="d133c-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="d133c-109">Estes certificados são, por vezes, os certificados autoassinados tooas referenciado.</span><span class="sxs-lookup"><span data-stu-id="d133c-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="d133c-110">Quais são os certificados?</span><span class="sxs-lookup"><span data-stu-id="d133c-110">What are certificates?</span></span>
<span data-ttu-id="d133c-111">Os certificados são digitais documentos que verifique se a identidade Olá participantes Olá eletrónicas comunicações e que também protege as comunicações eletrónicas.</span><span class="sxs-lookup"><span data-stu-id="d133c-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="d133c-112">Porquê utilizar certificados?</span><span class="sxs-lookup"><span data-stu-id="d133c-112">Why use certificates?</span></span>
<span data-ttu-id="d133c-113">Por vezes, comunicações B2B têm de ser mantidas confidenciais.</span><span class="sxs-lookup"><span data-stu-id="d133c-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="d133c-114">Integração empresarial com utiliza certificados toosecure estas comunicações de duas formas:</span><span class="sxs-lookup"><span data-stu-id="d133c-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="d133c-115">Ao encriptar o conteúdo de Olá de mensagens em fila</span><span class="sxs-lookup"><span data-stu-id="d133c-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="d133c-116">Ao assinar digitalmente mensagens</span><span class="sxs-lookup"><span data-stu-id="d133c-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="d133c-117">Carregar um certificado público</span><span class="sxs-lookup"><span data-stu-id="d133c-117">Upload a public certificate</span></span>

<span data-ttu-id="d133c-118">toouse um *certificado público* nas suas logic apps com capacidades de B2B, primeiro tem de certificado de Olá tooupload na sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="d133c-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="d133c-119">Depois de carregar um certificado, estão disponível toohelp proteger as mensagens B2B quando definir as respetivas propriedades no Olá [contratos](logic-apps-enterprise-integration-agreements.md) que criar.</span><span class="sxs-lookup"><span data-stu-id="d133c-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="d133c-120">Seguem-se Olá os passos detalhados para carregar os certificados públicos na sua conta de integração, depois de se inscrever no toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="d133c-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="d133c-121">Selecione **mais serviços** e introduza **integração** na caixa de pesquisa de filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="d133c-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="d133c-122">Selecione **contas de automatização** da lista de resultados de Olá</span><span class="sxs-lookup"><span data-stu-id="d133c-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="d133c-123">![Selecione procurar](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="d133c-124">Selecione Olá integração conta toowhich pretende que o certificado de Olá tooadd.</span><span class="sxs-lookup"><span data-stu-id="d133c-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Selecione Olá integração conta toowhich pretende que o certificado de Olá tooadd](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="d133c-126">Selecione Olá **certificados** mosaico.</span><span class="sxs-lookup"><span data-stu-id="d133c-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="d133c-127">![Mosaico de Olá selecione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="d133c-128">No Olá **certificados** painel que abre, selecione de Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="d133c-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="d133c-129">![Selecione o botão de adição de Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="d133c-130">Introduza um **nome** de certificado e Olá, em seguida, selecione o tipo de certificado como **pública** de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="d133c-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="d133c-131">Ícone de pasta Olá selecione no lado direito de Olá de Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d133c-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="d133c-132">Quando abre o seleccionador de ficheiros de Olá, localize e selecione o ficheiro de certificado Olá que pretende que a conta de integração de tooyour tooupload.</span><span class="sxs-lookup"><span data-stu-id="d133c-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="d133c-133">Selecione o certificado de Olá e, em seguida, selecione **OK** no seleccionador de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="d133c-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="d133c-134">Isto valida e carrega a conta de integração do Olá certificados tooyour.</span><span class="sxs-lookup"><span data-stu-id="d133c-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="d133c-135">Por fim, fazer uma cópia no Olá **adicionar certificado** painel, selecione de Olá **OK** botão.</span><span class="sxs-lookup"><span data-stu-id="d133c-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="d133c-136">![Selecione o botão OK Olá](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="d133c-137">Selecione Olá **certificados** mosaico.</span><span class="sxs-lookup"><span data-stu-id="d133c-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="d133c-138">Deverá ver Olá recentemente adicionado o certificado.</span><span class="sxs-lookup"><span data-stu-id="d133c-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="d133c-139">![Ver o novo certificado de Olá](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="d133c-140">Carregar um certificado privado</span><span class="sxs-lookup"><span data-stu-id="d133c-140">Upload a private certificate</span></span>

<span data-ttu-id="d133c-141">toouse um *certificado privado* nas suas logic apps com B2B capacidades, pode carregar uma conta de integração do certificado privado tooyour ao hello efetuando os passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d133c-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="d133c-142">[Carregar o seu Cofre de tooKey chave privada](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de chaves") e fornecer um **nome da chave**</span><span class="sxs-lookup"><span data-stu-id="d133c-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="d133c-143">Tem de autorizar operações de tooperform Logic Apps no Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="d133c-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="d133c-144">Pode conceder principal de serviço do acesso toohello Logic Apps utilizando Olá seguinte comando do PowerShell:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="d133c-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="d133c-145">Depois de ter sido passo anterior Olá, adicione uma conta de toointegration certificado privado.</span><span class="sxs-lookup"><span data-stu-id="d133c-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="d133c-146">Seguintes são Olá os passos detalhados para carregar os certificados privados na sua conta de integração, depois de se inscrever no toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="d133c-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="d133c-147">Selecione a conta de integração do Olá toowhich que pretende o certificado de Olá tooadd e selecione Olá **certificados** mosaico.</span><span class="sxs-lookup"><span data-stu-id="d133c-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="d133c-148">![Mosaico de Olá selecione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="d133c-149">No Olá **certificados** painel que abre, selecione de Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="d133c-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="d133c-150">![Selecione o botão de adição de Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="d133c-151">Introduza um **nome** de certificado e Olá selecione o tipo de certificado como **privada** de Olá pendente.</span><span class="sxs-lookup"><span data-stu-id="d133c-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="d133c-152">Selecione o ícone de pasta Olá no lado direito de Olá de Olá **certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d133c-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="d133c-153">Quando abre o seleccionador de ficheiros de Olá, localize Olá de certificado pública correspondente que pretende que a conta de integração de tooyour tooupload.</span><span class="sxs-lookup"><span data-stu-id="d133c-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="d133c-154">Ao adicionar um certificado privado é importante tooadd correspondente pública do certificado tooshow no [contratos AS2](logic-apps-enterprise-integration-as2.md) receber e enviar as definições de assinatura e encriptação de mensagens hello.</span><span class="sxs-lookup"><span data-stu-id="d133c-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="d133c-155">Selecione Olá **grupo de recursos**, **Cofre de chaves**, **nome da chave** e selecione Olá **OK** botão.</span><span class="sxs-lookup"><span data-stu-id="d133c-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="d133c-156">![Adicionar certificado](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="d133c-157">Selecione Olá **certificados** mosaico.</span><span class="sxs-lookup"><span data-stu-id="d133c-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="d133c-158">Deverá ver Olá recentemente adicionado o certificado.</span><span class="sxs-lookup"><span data-stu-id="d133c-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="d133c-159">![Ver o novo certificado de Olá](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="d133c-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="d133c-160">Criar um contrato de B2B</span><span class="sxs-lookup"><span data-stu-id="d133c-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="d133c-161">Saiba mais sobre o Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="d133c-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de chaves")  

