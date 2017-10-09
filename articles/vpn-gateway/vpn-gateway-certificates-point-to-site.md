---
title: 'Gerar e exportar certificados para ponto a Site: PowerShell: Azure | Microsoft Docs'
description: "Este artigo contém passos toocreate um certificado de raiz autoassinado, exportar a chave pública Olá e gerar os certificados de cliente através do PowerShell no Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="2600e-103">Gerar e exportar certificados para ligações ponto a Site através do PowerShell no Windows 10</span><span class="sxs-lookup"><span data-stu-id="2600e-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="2600e-104">Ligações de ponto a Site utilizam certificados tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="2600e-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="2600e-105">Este artigo mostra-lhe como toocreate autoassinado a raiz do certificado e gerar os certificados de cliente através do PowerShell no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2600e-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="2600e-106">Se está a procurar passos de configuração de ponto a Site, tais como como certificados de raiz tooupload, selecione um dos artigos Olá ' Configurar ponto a Site' de Olá seguinte listam:</span><span class="sxs-lookup"><span data-stu-id="2600e-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2600e-107">Criar certificados autoassinados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2600e-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="2600e-108">Criar certificados autoassinados - MakeCert</span><span class="sxs-lookup"><span data-stu-id="2600e-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="2600e-109">Configurar o ponto a Site - Resource Manager - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2600e-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="2600e-110">Configurar o ponto a Site - Gestor de recursos - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2600e-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="2600e-111">Configurar o ponto a Site - Classic - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2600e-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="2600e-112">Tem de efetuar os passos de Olá neste artigo num computador com o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="2600e-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="2600e-113">cmdlets do PowerShell Olá que utilize certificados toogenerate fazem parte do sistema de operativo Olá Windows 10 e não funcionam nas outras versões do Windows.</span><span class="sxs-lookup"><span data-stu-id="2600e-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="2600e-114">computador Olá Windows 10 é apenas necessário toogenerate Olá certificados.</span><span class="sxs-lookup"><span data-stu-id="2600e-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="2600e-115">Assim que são gerados certificados Olá, pode carregá-los ou instalá-los em qualquer sistema operativo de cliente suportada.</span><span class="sxs-lookup"><span data-stu-id="2600e-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="2600e-116">Se não tiver o computador do acesso tooa Windows 10, pode utilizar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificados.</span><span class="sxs-lookup"><span data-stu-id="2600e-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="2600e-117">Olá certificados que geram o utilizando um dos métodos podem ser instalados em qualquer [suportado](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) sistema operativo do cliente.</span><span class="sxs-lookup"><span data-stu-id="2600e-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="2600e-118"><a name="rootcert"></a>Criar um certificado de raiz autoassinado</span><span class="sxs-lookup"><span data-stu-id="2600e-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="2600e-119">Utilize Olá SelfSignedCertificate novo cmdlet toocreate um certificado de raiz autoassinado.</span><span class="sxs-lookup"><span data-stu-id="2600e-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="2600e-120">Para informações de parâmetros adicionais, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="2600e-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="2600e-121">A partir de um computador com o Windows 10, abra uma consola do Windows PowerShell com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="2600e-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="2600e-122">Utilize Olá certificado de raiz autoassinado de Olá de toocreate de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="2600e-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="2600e-123">Olá exemplo seguinte cria um certificado de raiz autoassinado com o nome 'P2SRootCert', que é instalado automaticamente em 'Certificados atual User\Personal\Certificates'.</span><span class="sxs-lookup"><span data-stu-id="2600e-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="2600e-124">Pode ver o certificado de Olá abrindo *certmgr.msc*, ou *gerir certificados de utilizador*.</span><span class="sxs-lookup"><span data-stu-id="2600e-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="2600e-125"><a name="cer"></a>Exportar a chave pública de Olá (. cer)</span><span class="sxs-lookup"><span data-stu-id="2600e-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="2600e-126">Olá exported.cer ficheiro tem de ser tooAzure carregado.</span><span class="sxs-lookup"><span data-stu-id="2600e-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="2600e-127">Para obter instruções, consulte [configurar uma ligação ponto a Site](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="2600e-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="2600e-128">tooadd um certificado de raiz fidedigna adicionais, [nesta secção](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="2600e-129">Exportar o certificado de raiz autoassinado Olá e toostore de chave pública-(opcional)</span><span class="sxs-lookup"><span data-stu-id="2600e-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="2600e-130">Poderá ser útil tooexport Olá um certificado de raiz autoassinado e armazena de forma segura.</span><span class="sxs-lookup"><span data-stu-id="2600e-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="2600e-131">Se necessário, mais tarde pode instalá-lo noutro computador e gerar mais certificados de cliente ou exportar outro ficheiro. cer.</span><span class="sxs-lookup"><span data-stu-id="2600e-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="2600e-132">Olá tooexport raiz um certificado autoassinado como uma. pfx, certificado de raiz de Olá selecione e utilize Olá mesmos passos conforme descrito em [exportar um certificado de cliente](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="2600e-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="2600e-133"><a name="clientcert"></a>Gerar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="2600e-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="2600e-134">Cada computador cliente que liga tooa a VNet com ponto a Site tem de ter um certificado de cliente instalado.</span><span class="sxs-lookup"><span data-stu-id="2600e-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="2600e-135">Gerar um certificado de cliente a partir do certificado de raiz autoassinado Olá e, em seguida, exportar e instalar o certificado de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="2600e-136">Se o certificado de cliente Olá não estiver instalado, a autenticação falha.</span><span class="sxs-lookup"><span data-stu-id="2600e-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="2600e-137">Olá seguintes passos guiá-lo a gerar um certificado de cliente de um certificado de raiz autoassinado.</span><span class="sxs-lookup"><span data-stu-id="2600e-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="2600e-138">Pode gerar vários certificados de cliente a partir de Olá mesmo certificado de raiz.</span><span class="sxs-lookup"><span data-stu-id="2600e-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="2600e-139">Ao gerar os certificados de cliente utilizando Olá passos abaixo, o certificado de cliente Olá é automaticamente instalado no computador de Olá que utilizou o certificado de Olá toogenerate.</span><span class="sxs-lookup"><span data-stu-id="2600e-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="2600e-140">Se quiser tooinstall um certificado de cliente no outro computador cliente, pode exportar o certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="2600e-141">Exemplos de Olá utilizam Olá SelfSignedCertificate novo cmdlet toogenerate um certificado de cliente que expira dentro de um ano.</span><span class="sxs-lookup"><span data-stu-id="2600e-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="2600e-142">Para informações de parâmetros adicionais, como a definição de um valor diferente de expiração do certificado de cliente Olá, consulte [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="2600e-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="2600e-143">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="2600e-143">Example 1</span></span>

<span data-ttu-id="2600e-144">Este exemplo utiliza Olá declarado '$cert' variável da secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="2600e-145">Se fechar a consola do PowerShell Olá depois de criar Olá certificado de raiz autoassinado ou estiver a criar adicionais de cliente certificados numa nova sessão de consola do PowerShell, utilize os passos de Olá em [exemplo 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="2600e-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="2600e-146">Modificar e execute toogenerate de exemplo de Olá um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="2600e-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="2600e-147">Se executar Olá seguinte o exemplo sem modificá-lo, o resultado de Olá é um certificado de cliente com o nome 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="2600e-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="2600e-148">Se pretender que os certificados de subordinados de Olá tooname algo pessoa, modifique o valor CN Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="2600e-149">Não altere Olá TextExtension quando executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="2600e-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="2600e-150">certificado de cliente de Olá gerar é instalado automaticamente nos 'Certificados - User\Personal\Certificates atual' no seu computador.</span><span class="sxs-lookup"><span data-stu-id="2600e-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="2600e-151"><a name="ex2"></a>Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="2600e-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="2600e-152">Se estiver a criar adicionais de cliente certificados ou são não utilizar Olá mesmo sessão do PowerShell que utilizou toocreate seu certificado de raiz autoassinado, Olá utilize os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="2600e-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="2600e-153">Identifica o certificado de raiz autoassinado Olá que está instalado no computador de Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="2600e-154">Este cmdlet devolve uma lista de certificados que estão instalados no seu computador.</span><span class="sxs-lookup"><span data-stu-id="2600e-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="2600e-155">Localize o nome de requerente Olá de Olá devolvida a lista, em seguida, impressão digital de Olá de cópia é localizado seguinte tooit tooa texto ficheiro.</span><span class="sxs-lookup"><span data-stu-id="2600e-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="2600e-156">No seguinte exemplo de Olá, existem dois certificados.</span><span class="sxs-lookup"><span data-stu-id="2600e-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="2600e-157">Olá CN é Olá nome do certificado de raiz autoassinado Olá partir das quais pretende toogenerate um certificado de subordinados.</span><span class="sxs-lookup"><span data-stu-id="2600e-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="2600e-158">Neste caso, 'P2SRootCert'.</span><span class="sxs-lookup"><span data-stu-id="2600e-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="2600e-159">Declare uma variável para o certificado de raiz de Olá utilizando thumbprint Olá do passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="2600e-160">Substitua o THUMBPRINT com Olá impressão digital do certificado de raiz de Olá partir do qual pretende toogenerate um certificado de subordinados.</span><span class="sxs-lookup"><span data-stu-id="2600e-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="2600e-161">Por exemplo, a utilizar o thumbprint Olá para P2SRootCert no passo anterior Olá, variável Olá este aspeto:</span><span class="sxs-lookup"><span data-stu-id="2600e-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="2600e-162">Modificar e execute toogenerate de exemplo de Olá um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="2600e-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="2600e-163">Se executar Olá seguinte o exemplo sem modificá-lo, o resultado de Olá é um certificado de cliente com o nome 'P2SChildCert'.</span><span class="sxs-lookup"><span data-stu-id="2600e-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="2600e-164">Se pretender que os certificados de subordinados de Olá tooname algo pessoa, modifique o valor CN Olá.</span><span class="sxs-lookup"><span data-stu-id="2600e-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="2600e-165">Não altere Olá TextExtension quando executar este exemplo.</span><span class="sxs-lookup"><span data-stu-id="2600e-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="2600e-166">certificado de cliente de Olá gerar é instalado automaticamente nos 'Certificados - User\Personal\Certificates atual' no seu computador.</span><span class="sxs-lookup"><span data-stu-id="2600e-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="2600e-167"><a name="clientexport"></a>Exportar um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="2600e-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="2600e-168"><a name="install"></a>Instalar um certificado de cliente exportado</span><span class="sxs-lookup"><span data-stu-id="2600e-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2600e-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2600e-169">Next steps</span></span>

<span data-ttu-id="2600e-170">Continue com a sua configuração de ponto a Site.</span><span class="sxs-lookup"><span data-stu-id="2600e-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="2600e-171">Para **Resource Manager** passos de modelo de implementação, consulte [configurar um tooa de ligação de ponto a Site VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2600e-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="2600e-172">Para **clássico** passos de modelo de implementação, consulte [configurar um tooa de ligação VPN ponto a Site VNet (clássica)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2600e-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
