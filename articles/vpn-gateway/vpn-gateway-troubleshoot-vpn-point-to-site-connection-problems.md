---
title: "problemas de ligação de aaaTroubleshoot Azure ponto a site | Microsoft Docs"
description: "Saiba como tootroubleshoot problemas de ligação de ponto a site."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="0ef76-103">Resolução de problemas: Problemas de ligação de ponto a site do Azure</span><span class="sxs-lookup"><span data-stu-id="0ef76-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="0ef76-104">Este artigo apresenta uma lista de problemas de ligação de ponto a site comuns que podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="0ef76-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="0ef76-105">Também descreve possíveis causas e soluções para esses problemas.</span><span class="sxs-lookup"><span data-stu-id="0ef76-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="0ef76-106">Erro de cliente VPN: não foi possível encontrar um certificado</span><span class="sxs-lookup"><span data-stu-id="0ef76-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-107">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-107">Symptom</span></span>

<span data-ttu-id="0ef76-108">Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="0ef76-109">**Não foi possível encontrar um certificado que pode ser utilizado com este protocolo de autenticação extensível. (Erro 798)**</span><span class="sxs-lookup"><span data-stu-id="0ef76-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-110">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-110">Cause</span></span>

<span data-ttu-id="0ef76-111">Este problema ocorre se o certificado de cliente Olá Faltam **certificados - User\Personal\Certificates atual**.</span><span class="sxs-lookup"><span data-stu-id="0ef76-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-112">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-112">Solution</span></span>

<span data-ttu-id="0ef76-113">Certifique-se de que certificado de cliente Olá está instalado no Olá seguinte localização do arquivo de certificados de Olá (Certmgr.msc):</span><span class="sxs-lookup"><span data-stu-id="0ef76-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="0ef76-114">**Certificados - User\Personal\Certificates atual**</span><span class="sxs-lookup"><span data-stu-id="0ef76-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="0ef76-115">Para obter mais informações sobre como tooinstall Olá certificado de cliente, consulte [gerar e exportar certificados para ligações ponto a site](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="0ef76-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0ef76-116">Ao importar o certificado de cliente Olá, não selecione Olá **ativar a proteção forte por chave privada** opção.</span><span class="sxs-lookup"><span data-stu-id="0ef76-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="0ef76-117">Erro de cliente VPN: mensagem de saudação recebida era inesperada ou formatado incorretamente</span><span class="sxs-lookup"><span data-stu-id="0ef76-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-118">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-118">Symptom</span></span>

<span data-ttu-id="0ef76-119">Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="0ef76-120">**foi recebida uma mensagem Olá era inesperada ou incorretamente formatado. (Erro 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="0ef76-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-121">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-121">Cause</span></span>

<span data-ttu-id="0ef76-122">Este problema ocorre se a chave pública do certificado de raiz Olá não é carregado para o gateway de VPN do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="0ef76-123">Também pode ocorrer se a chave de Olá está danificada ou expirada.</span><span class="sxs-lookup"><span data-stu-id="0ef76-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-124">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-124">Solution</span></span>

<span data-ttu-id="0ef76-125">tooresolve este problema, verifique o estado de Olá de raiz de Olá de certificado no Olá toosee portal do Azure se foi revogado.</span><span class="sxs-lookup"><span data-stu-id="0ef76-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="0ef76-126">Se não for revogado, experimente o certificado de raiz de Olá toodelete e reupload.</span><span class="sxs-lookup"><span data-stu-id="0ef76-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="0ef76-127">Para obter mais informações, consulte [criar certificados](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="0ef76-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="0ef76-128">Erro de cliente VPN: uma cadeia de certificados processada, mas foi terminado</span><span class="sxs-lookup"><span data-stu-id="0ef76-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="0ef76-129">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-129">Symptom</span></span> 

<span data-ttu-id="0ef76-130">Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="0ef76-131">**Uma cadeia de certificados processados mas terminada num certificado de raiz que não é considerado fidedigno pelo fornecedor de confiança Olá.**</span><span class="sxs-lookup"><span data-stu-id="0ef76-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-132">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-132">Solution</span></span>

1. <span data-ttu-id="0ef76-133">Certifique-se de que Olá seguintes certificados na localização correta Olá:</span><span class="sxs-lookup"><span data-stu-id="0ef76-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="0ef76-134">Certificado</span><span class="sxs-lookup"><span data-stu-id="0ef76-134">Certificate</span></span> | <span data-ttu-id="0ef76-135">Localização</span><span class="sxs-lookup"><span data-stu-id="0ef76-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="0ef76-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="0ef76-136">AzureClient.pfx</span></span>  | <span data-ttu-id="0ef76-137">User\Personal\Certificates atual</span><span class="sxs-lookup"><span data-stu-id="0ef76-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="0ef76-138">Azuregateway -*GUID*. cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="0ef76-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="0ef76-139">Autoridades de certificação de raiz User\Trusted atual</span><span class="sxs-lookup"><span data-stu-id="0ef76-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="0ef76-140">AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="0ef76-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="0ef76-141">Autoridades de certificação de raiz local Computer\Trusted</span><span class="sxs-lookup"><span data-stu-id="0ef76-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="0ef76-142">Se os certificados de Olá já estão na localização de Olá, tente certificados de Olá toodelete e reinstalá-los.</span><span class="sxs-lookup"><span data-stu-id="0ef76-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="0ef76-143">Olá  **azuregateway -*GUID*. cloudapp.net** certificado está no pacote configuração de cliente VPN de Olá que transferiu a partir do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef76-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="0ef76-144">Pode utilizar o ficheiro archivers tooextract Olá os ficheiros do pacote de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="0ef76-145">Erro de transferência de ficheiro: o URI de destino não for especificado.</span><span class="sxs-lookup"><span data-stu-id="0ef76-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-146">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-146">Symptom</span></span>

<span data-ttu-id="0ef76-147">Receber Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-147">You receive hello following error message:</span></span>

<span data-ttu-id="0ef76-148">**Erro de transferência do ficheiro. URI de destino não está especificado.**</span><span class="sxs-lookup"><span data-stu-id="0ef76-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-149">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-149">Cause</span></span> 

<span data-ttu-id="0ef76-150">Este problema ocorre devido a um tipo de gateway incorreto.</span><span class="sxs-lookup"><span data-stu-id="0ef76-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="0ef76-151">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-151">Solution</span></span>

<span data-ttu-id="0ef76-152">Olá, tipo de gateway VPN tem de ser **VPN**, e Olá tipo de VPN tem de ser **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="0ef76-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="0ef76-153">Erro de cliente VPN: falha no script personalizado VPN do Azure</span><span class="sxs-lookup"><span data-stu-id="0ef76-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="0ef76-154">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-154">Symptom</span></span>

<span data-ttu-id="0ef76-155">Quando tenta tooconnect tooan rede virtual do Azure utilizando o cliente VPN Olá, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="0ef76-156">**Script personalizado (tooupdate o encaminhamento de tabela) falha. (Erro 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="0ef76-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-157">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-157">Cause</span></span>

<span data-ttu-id="0ef76-158">Este problema pode ocorrer se estiver a tentar ligação de VPN do tooopen Olá ponto a site utilizando um atalho.</span><span class="sxs-lookup"><span data-stu-id="0ef76-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-159">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-159">Solution</span></span> 

<span data-ttu-id="0ef76-160">Abra o pacote de VPN Olá diretamente em vez de abri-lo a partir do atalho Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="0ef76-161">Não é possível instalar o cliente VPN Olá</span><span class="sxs-lookup"><span data-stu-id="0ef76-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-162">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-162">Cause</span></span> 

<span data-ttu-id="0ef76-163">Um certificado adicional é gateway de VPN de Olá tootrust necessária para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0ef76-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="0ef76-164">certificado de Olá está incluído no pacote configuração de cliente VPN de Olá que é gerado a partir de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef76-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-165">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-165">Solution</span></span>

<span data-ttu-id="0ef76-166">Extraia o pacote de configuração de cliente VPN Olá e localizar o ficheiro. cer de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="0ef76-167">Olá tooinstall de certificado, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="0ef76-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="0ef76-168">Abra mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="0ef76-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="0ef76-169">Adicionar Olá **certificados** snap-in.</span><span class="sxs-lookup"><span data-stu-id="0ef76-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="0ef76-170">Selecione Olá **computador** conta do computador local Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="0ef76-171">Contexto Olá **autoridades de certificação de raiz fidedigna** nós.</span><span class="sxs-lookup"><span data-stu-id="0ef76-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="0ef76-172">Clique em **todas as tarefas** > **importação**e o ficheiro. cer toohello de procurar extraiu de pacote de configuração de cliente VPN Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="0ef76-173">Reinicie o computador de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="0ef76-174">Tente cliente VPN de Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="0ef76-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="0ef76-175">Erro de portal do Azure: Falha ao gateway de VPN do toosave Olá, e os dados de Olá inválidos</span><span class="sxs-lookup"><span data-stu-id="0ef76-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-176">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-176">Symptom</span></span>

<span data-ttu-id="0ef76-177">Quando tenta alterações de Olá toosave para gateway de VPN Olá no Olá portal do Azure, receber Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="0ef76-178">**Gateway de rede virtual falha toosave &lt;* nome do gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="0ef76-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="0ef76-179">Dados do certificado &lt; *ID de certificado* &gt; é invalid.* *</span><span class="sxs-lookup"><span data-stu-id="0ef76-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-180">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-180">Cause</span></span> 

<span data-ttu-id="0ef76-181">Este problema pode ocorrer se Olá raiz certificado chave pública que carregou contém um caráter inválido, por exemplo, um espaço.</span><span class="sxs-lookup"><span data-stu-id="0ef76-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-182">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-182">Solution</span></span>

<span data-ttu-id="0ef76-183">Certifique-se de que os dados de Olá no certificado de Olá não contém carateres inválidos, tais como as quebras de linha (mudanças).</span><span class="sxs-lookup"><span data-stu-id="0ef76-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="0ef76-184">valor inteiro Olá deve ser uma linha de tempo.</span><span class="sxs-lookup"><span data-stu-id="0ef76-184">hello entire value should be one long line.</span></span> <span data-ttu-id="0ef76-185">Olá seguir o texto é uma amostra de certificado Olá:</span><span class="sxs-lookup"><span data-stu-id="0ef76-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="0ef76-186">Erro de portal do Azure: Falha ao gateway de VPN de Olá toosave e Olá o nome do recurso é inválido</span><span class="sxs-lookup"><span data-stu-id="0ef76-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-187">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-187">Symptom</span></span>

<span data-ttu-id="0ef76-188">Quando tenta alterações de Olá toosave para gateway de VPN Olá no Olá portal do Azure, receber Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="0ef76-189">**Gateway de rede virtual falha toosave &lt;* nome do gateway*&gt;.</span><span class="sxs-lookup"><span data-stu-id="0ef76-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="0ef76-190">Nome do recurso &lt; *nome do certificado tente tooupload* &gt; é inválido. o * *.</span><span class="sxs-lookup"><span data-stu-id="0ef76-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-191">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-191">Cause</span></span>

<span data-ttu-id="0ef76-192">Este problema ocorre porque o nome de Olá do certificado de Olá contém um caráter inválido, tais como um espaço.</span><span class="sxs-lookup"><span data-stu-id="0ef76-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="0ef76-193">Erro de portal do Azure: erro de transferência de ficheiro de pacote VPN 503</span><span class="sxs-lookup"><span data-stu-id="0ef76-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-194">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-194">Symptom</span></span>

<span data-ttu-id="0ef76-195">Quando tenta pacote de configuração do cliente VPN do toodownload Olá, receberá Olá seguir a mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="0ef76-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="0ef76-196">**Falha ao ficheiro de Olá toodownload. Detalhes do erro: erro 503. servidor de Olá está ocupado.**</span><span class="sxs-lookup"><span data-stu-id="0ef76-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="0ef76-197">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-197">Solution</span></span>

<span data-ttu-id="0ef76-198">Este erro pode ser causado por um problema temporário de rede.</span><span class="sxs-lookup"><span data-stu-id="0ef76-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="0ef76-199">Repita o pacote de VPN de Olá toodownload depois de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0ef76-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="0ef76-200">A atualização de Gateway de VPN do Azure: P2S todos os clientes são tooconnect não é possível</span><span class="sxs-lookup"><span data-stu-id="0ef76-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-201">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-201">Cause</span></span>

<span data-ttu-id="0ef76-202">Se o certificado de Olá é mais de 50 por cento através da respetiva duração, certificado Olá é distribuído.</span><span class="sxs-lookup"><span data-stu-id="0ef76-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-203">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-203">Solution</span></span>

<span data-ttu-id="0ef76-204">tooresolve este problema, crie e redistribuir novos certificados toohello os clientes VPN.</span><span class="sxs-lookup"><span data-stu-id="0ef76-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="0ef76-205">Demasiados clientes VPN ligados em simultâneo</span><span class="sxs-lookup"><span data-stu-id="0ef76-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="0ef76-206">Para cada gateway de VPN, Olá o número máximo de ligações permitidos é 128.</span><span class="sxs-lookup"><span data-stu-id="0ef76-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="0ef76-207">Pode ver o número total de Olá de clientes ligados no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef76-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="0ef76-208">VPN ponto a site incorretamente adiciona uma rota 10.0.0.0/8 toohello tabela de rotas</span><span class="sxs-lookup"><span data-stu-id="0ef76-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-209">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-209">Symptom</span></span>

<span data-ttu-id="0ef76-210">Ao marcar Olá ligação VPN no cliente de ponto a site Olá, o cliente VPN Olá deve adicionar uma rota para Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef76-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="0ef76-211">serviço de programa auxiliar IP Olá deve adicionar uma rota de sub-rede de Olá de clientes VPN de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="0ef76-212">Olá intervalo de cliente VPN pertence tooa sub-rede mais pequeno de 10.0.0.0/8, tais como 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="0ef76-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="0ef76-213">Em vez de uma rota para 10.0.12.0/24, uma rota para 10.0.0.0/8 é adicionada que tenha a prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="0ef76-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="0ef76-214">Esta rota incorreta de quebras de conectividade com outras redes de no local que têm de pertencer tooanother sub-rede dentro do intervalo de 10.0.0.0/8 Olá, tais como 10.50.0.0/24, que não tenham uma rota específica definida.</span><span class="sxs-lookup"><span data-stu-id="0ef76-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="0ef76-215">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-215">Cause</span></span>

<span data-ttu-id="0ef76-216">Este comportamento é por predefinição para clientes Windows.</span><span class="sxs-lookup"><span data-stu-id="0ef76-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="0ef76-217">Quando o cliente de Olá utiliza o protocolo PPP IPCP de Olá, obtém o endereço IP Olá para a interface de túnel hello do servidor de Olá (gateway VPN Olá neste caso).</span><span class="sxs-lookup"><span data-stu-id="0ef76-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="0ef76-218">No entanto, devido a uma limitação no protocolo Olá, o cliente Olá tem máscara de sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="0ef76-219">Porque não há nenhum tooget de forma, o cliente de Olá tentará máscara de sub-rede tooguess Olá com base na classe de Olá do endereço IP de interface de túnel Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="0ef76-220">Por conseguinte, uma rota foi adicionada com base no Olá mapeamento estático os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0ef76-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="0ef76-221">Se o endereço pertence tooclass A--> aplicar /8</span><span class="sxs-lookup"><span data-stu-id="0ef76-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="0ef76-222">Se o endereço pertence tooclass B--> aplicar /16</span><span class="sxs-lookup"><span data-stu-id="0ef76-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="0ef76-223">Se o endereço pertence tooclass C--> aplicar /24</span><span class="sxs-lookup"><span data-stu-id="0ef76-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="0ef76-224">Cliente VPN não é possível aceder a partilhas de ficheiros de rede</span><span class="sxs-lookup"><span data-stu-id="0ef76-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-225">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-225">Symptom</span></span>

<span data-ttu-id="0ef76-226">cliente VPN Olá estabeleceu ligação toohello rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef76-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="0ef76-227">No entanto, o cliente Olá não é possível aceder às partilhas de rede.</span><span class="sxs-lookup"><span data-stu-id="0ef76-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="0ef76-228">Causa</span><span class="sxs-lookup"><span data-stu-id="0ef76-228">Cause</span></span>

<span data-ttu-id="0ef76-229">Olá protocolo SMB é utilizado para acesso de partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="0ef76-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="0ef76-230">Quando é iniciada a ligação de Olá, cliente VPN Olá adiciona as credenciais de sessão Olá e Olá a falha ocorre.</span><span class="sxs-lookup"><span data-stu-id="0ef76-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="0ef76-231">Uma vez estabelecido ligação Olá, o cliente Olá é forçado toouse Olá cache as credenciais a autenticação Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0ef76-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="0ef76-232">Este processo inicia consultas toohello Centro de distribuição de chaves (um controlador de domínio) tooget um token.</span><span class="sxs-lookup"><span data-stu-id="0ef76-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="0ef76-233">Porque Olá cliente liga-se de Olá Internet, poderá não ser capaz de tooreach controlador de domínio de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="0ef76-234">Por conseguinte, cliente Olá não é possível efetuar a ativação pós-falha do tooNTLM de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0ef76-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="0ef76-235">Olá apenas tempo que o cliente Olá é pedido uma credencial é quando tem um certificado válido (com SAN = UPN) emitido por Olá toowhich de domínio está associado.</span><span class="sxs-lookup"><span data-stu-id="0ef76-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="0ef76-236">cliente de Olá também tem de ser fisicamente ligada toohello rede de domínio.</span><span class="sxs-lookup"><span data-stu-id="0ef76-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="0ef76-237">Neste caso, o cliente de Olá tenta certificado de Olá toouse e acede toohello controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="0ef76-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="0ef76-238">Em seguida, Olá Centro de distribuição de chaves devolve um erro de "KDC_ERR_C_PRINCIPAL_UNKNOWN".</span><span class="sxs-lookup"><span data-stu-id="0ef76-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="0ef76-239">cliente de Olá é forçada toofail tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="0ef76-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="0ef76-240">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-240">Solution</span></span>

<span data-ttu-id="0ef76-241">toowork em torno do problema Olá, desativar Olá colocação em cache de credenciais de domínio de Olá seguinte subchave de registo:</span><span class="sxs-lookup"><span data-stu-id="0ef76-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="0ef76-242">Não é possível localizar a ligação de VPN de ponto a site Olá no Windows após a reinstalação do cliente VPN Olá</span><span class="sxs-lookup"><span data-stu-id="0ef76-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="0ef76-243">Sintoma</span><span class="sxs-lookup"><span data-stu-id="0ef76-243">Symptom</span></span>

<span data-ttu-id="0ef76-244">Remover a ligação de VPN de ponto a site Olá e, em seguida, reinstalar o cliente VPN Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="0ef76-245">Nesta situação, Olá ligação VPN não está configurado com êxito.</span><span class="sxs-lookup"><span data-stu-id="0ef76-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="0ef76-246">Não vir a ligação de VPN de Olá na Olá **ligações de rede** definições do Windows.</span><span class="sxs-lookup"><span data-stu-id="0ef76-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="0ef76-247">Solução</span><span class="sxs-lookup"><span data-stu-id="0ef76-247">Solution</span></span>

<span data-ttu-id="0ef76-248">problema de Olá tooresolve, eliminar Olá antigos VPN cliente ficheiros de configuração da **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, e, em seguida, execute novamente o programa de instalação de cliente VPN de Olá.</span><span class="sxs-lookup"><span data-stu-id="0ef76-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
