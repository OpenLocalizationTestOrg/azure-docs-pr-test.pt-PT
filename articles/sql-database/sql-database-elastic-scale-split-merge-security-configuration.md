---
title: "configuração de segurança de intercalação aaaSplit | Microsoft Docs"
description: "Configurar x409 certificados de encriptação"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="27cae-103">Configuração de segurança de divisão de intercalação</span><span class="sxs-lookup"><span data-stu-id="27cae-103">Split-merge security configuration</span></span>
<span data-ttu-id="27cae-104">serviço de divisão/intercalação do toouse Olá, deve configurar corretamente segurança.</span><span class="sxs-lookup"><span data-stu-id="27cae-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="27cae-105">serviço de Olá faz parte da funcionalidade do dimensionamento elástico Olá da base de dados do Microsoft Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="27cae-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="27cae-106">Para obter mais informações, consulte [divisão de dimensionamento elástico e o Tutorial do serviço de intercalação](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="27cae-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="27cae-107">Configurar certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-107">Configuring certificates</span></span>
<span data-ttu-id="27cae-108">Certificados são configurados de duas formas.</span><span class="sxs-lookup"><span data-stu-id="27cae-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="27cae-109">Olá tooConfigure certificado SSL</span><span class="sxs-lookup"><span data-stu-id="27cae-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="27cae-110">tooConfigure certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="27cae-111">tooobtain certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-111">tooobtain certificates</span></span>
<span data-ttu-id="27cae-112">Certificados podem ser obtidos a partir de autoridades de certificação (AC) pública ou de Olá [serviço de certificados do Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="27cae-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="27cae-113">Estes são Olá preferido métodos tooobtain certificados.</span><span class="sxs-lookup"><span data-stu-id="27cae-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="27cae-114">Se essas opções não estiverem disponíveis, pode gerar **certificados autoassinados**.</span><span class="sxs-lookup"><span data-stu-id="27cae-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="27cae-115">Certificados de toogenerate de ferramentas</span><span class="sxs-lookup"><span data-stu-id="27cae-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="27cae-116">MakeCert.exe</span><span class="sxs-lookup"><span data-stu-id="27cae-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="27cae-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="27cae-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="27cae-118">ferramentas de Olá toorun</span><span class="sxs-lookup"><span data-stu-id="27cae-118">toorun hello tools</span></span>
* <span data-ttu-id="27cae-119">De um programador linha de comandos para estúdios Visual, consulte [linha de comandos do Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="27cae-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="27cae-120">Se instalada, aceda a:</span><span class="sxs-lookup"><span data-stu-id="27cae-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="27cae-121">Obter Olá WDK de [Windows 8.1: Transferir kits e ferramentas](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="27cae-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="27cae-122">certificado SSL de Olá tooconfigure</span><span class="sxs-lookup"><span data-stu-id="27cae-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="27cae-123">Um certificado SSL é necessário tooencrypt Olá comunicação e autenticar Olá servidor.</span><span class="sxs-lookup"><span data-stu-id="27cae-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="27cae-124">Escolha Olá mais aplicável dos Olá três cenários abaixo e executar todos os passos:</span><span class="sxs-lookup"><span data-stu-id="27cae-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="27cae-125">Criar um novo certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="27cae-126">Criar um certificado Autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="27cae-127">Criar o ficheiro PFX de certificado de SSL autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="27cae-128">Carregar o certificado SSL tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="27cae-129">Atualizar o certificado SSL no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="27cae-130">Importar a autoridade de certificação de SSL</span><span class="sxs-lookup"><span data-stu-id="27cae-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="27cae-131">arquivo de um certificado existente de certificado Olá toouse</span><span class="sxs-lookup"><span data-stu-id="27cae-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="27cae-132">Exportar o certificado SSL do arquivo de certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="27cae-133">Carregar o certificado SSL tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="27cae-134">Atualizar o certificado SSL no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="27cae-135">toouse um certificado existente num ficheiro PFX</span><span class="sxs-lookup"><span data-stu-id="27cae-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="27cae-136">Carregar o certificado SSL tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="27cae-137">Atualizar o certificado SSL no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="27cae-138">certificados de cliente tooconfigure</span><span class="sxs-lookup"><span data-stu-id="27cae-138">tooconfigure client certificates</span></span>
<span data-ttu-id="27cae-139">Certificados de cliente são necessários na ordem tooauthenticate pedidos toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="27cae-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="27cae-140">Escolha Olá mais aplicável dos Olá três cenários abaixo e executar todos os passos:</span><span class="sxs-lookup"><span data-stu-id="27cae-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="27cae-141">Desativar a certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="27cae-142">Desativar a autenticação baseada em certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="27cae-143">Emitir novos certificados de cliente autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="27cae-144">Criar uma autoridade de certificação Autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="27cae-145">Carregar o certificado de AC tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="27cae-146">Atualizar o certificado de AC no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="27cae-147">Emitir certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="27cae-148">Criar ficheiros PFX para certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="27cae-149">Importar o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="27cae-150">Copie os Thumbprints de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="27cae-151">Configurar clientes permitido no Olá ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="27cae-152">Utilizar certificados de cliente existente</span><span class="sxs-lookup"><span data-stu-id="27cae-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="27cae-153">Localizar a chave pública de AC</span><span class="sxs-lookup"><span data-stu-id="27cae-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="27cae-154">Carregar o certificado de AC tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="27cae-155">Atualizar o certificado de AC no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="27cae-156">Copie os Thumbprints de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="27cae-157">Configurar clientes permitido no Olá ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="27cae-158">Configurar a verificação de revogação de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="27cae-159">Endereços IP permitidos</span><span class="sxs-lookup"><span data-stu-id="27cae-159">Allowed IP addresses</span></span>
<span data-ttu-id="27cae-160">Pontos finais de serviço do acesso toohello podem ser restringida toospecific intervalos de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="27cae-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="27cae-161">encriptação de tooconfigure para arquivo Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="27cae-162">É de um certificado de credenciais de Olá tooencrypt necessárias que são armazenadas no arquivo de metadados de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="27cae-163">Escolha Olá mais aplicável dos Olá três cenários abaixo e executar todos os passos:</span><span class="sxs-lookup"><span data-stu-id="27cae-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="27cae-164">Utilizar um novo certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="27cae-165">Criar um certificado Autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="27cae-166">Criar o ficheiro PFX de certificado de encriptação autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="27cae-167">Carregar o certificado de encriptação tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="27cae-168">Atualizar o certificado de encriptação no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="27cae-169">Utilizar um certificado existente Olá do arquivo de certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="27cae-170">Exportar o certificado de encriptação do arquivo de certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="27cae-171">Carregar o certificado de encriptação tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="27cae-172">Atualizar o certificado de encriptação no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="27cae-173">Utilizar um certificado existente num ficheiro PFX</span><span class="sxs-lookup"><span data-stu-id="27cae-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="27cae-174">Carregar o certificado de encriptação tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="27cae-175">Atualizar o certificado de encriptação no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="27cae-176">configuração predefinida de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-176">hello default configuration</span></span>
<span data-ttu-id="27cae-177">configuração predefinida de Olá nega todos os acesso toohello ponto final de HTTP.</span><span class="sxs-lookup"><span data-stu-id="27cae-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="27cae-178">Este é Olá recomendado definição, uma vez que os pontos finais do Olá pedidos toothese podem transportar as informações confidenciais, como as credenciais da base de dados.</span><span class="sxs-lookup"><span data-stu-id="27cae-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="27cae-179">configuração predefinida de Olá permite que todos os acesso toohello ponto final de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="27cae-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="27cae-180">Esta definição pode ser restringida adicional.</span><span class="sxs-lookup"><span data-stu-id="27cae-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="27cae-181">Alterar Olá configuração</span><span class="sxs-lookup"><span data-stu-id="27cae-181">Changing hello Configuration</span></span>
<span data-ttu-id="27cae-182">Olá grupo de regras de controlo de acesso que se aplicam tooand endpoint estão configuradas no Olá  **<EndpointAcls>**  secção Olá **ficheiro de configuração do serviço**.</span><span class="sxs-lookup"><span data-stu-id="27cae-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="27cae-183">regras de Olá num grupo de controlo de acesso estão configuradas num <AccessControl name=""> secção do ficheiro de configuração do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="27cae-184">formato de Olá é explicado na documentação de listas de controlo de acesso de rede.</span><span class="sxs-lookup"><span data-stu-id="27cae-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="27cae-185">Por exemplo, tooallow IPs apenas na Olá intervalo 100.100.0.0 too100.100.255.255 tooaccess Olá ponto final de HTTPS, regras de Olá deverá ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="27cae-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="27cae-186">Negação de prevenção de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-186">Denial of service prevention</span></span>
<span data-ttu-id="27cae-187">Existem dois mecanismos diferentes suportado toodetect e impedem ataques Denial of Service:</span><span class="sxs-lookup"><span data-stu-id="27cae-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="27cae-188">Restringir o número de pedidos em simultâneo por anfitrião remoto (desativado por predefinição)</span><span class="sxs-lookup"><span data-stu-id="27cae-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="27cae-189">Restringir a taxa de acesso por anfitrião remoto (por predefinição)</span><span class="sxs-lookup"><span data-stu-id="27cae-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="27cae-190">Estas baseiam-se nas funcionalidades Olá mais documentadas em segurança IP dinâmica no IIS.</span><span class="sxs-lookup"><span data-stu-id="27cae-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="27cae-191">Quando alterar esta configuração cuidado com de Olá seguintes fatores:</span><span class="sxs-lookup"><span data-stu-id="27cae-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="27cae-192">comportamento de Olá de proxies e os dispositivos de tradução de endereços de rede através de informações do anfitrião remoto de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="27cae-193">Cada recurso de tooany pedido na função da web Olá é considerado (por exemplo, carregar scripts, imagens, etc.)</span><span class="sxs-lookup"><span data-stu-id="27cae-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="27cae-194">Restringir o número de acessos simultâneos</span><span class="sxs-lookup"><span data-stu-id="27cae-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="27cae-195">definições de Olá que configurar este comportamento são:</span><span class="sxs-lookup"><span data-stu-id="27cae-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="27cae-196">Altere DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable esta proteção.</span><span class="sxs-lookup"><span data-stu-id="27cae-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="27cae-197">Restringir a taxa de acesso</span><span class="sxs-lookup"><span data-stu-id="27cae-197">Restricting rate of access</span></span>
<span data-ttu-id="27cae-198">definições de Olá que configurar este comportamento são:</span><span class="sxs-lookup"><span data-stu-id="27cae-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="27cae-199">Configurar Olá resposta tooa negou o pedido</span><span class="sxs-lookup"><span data-stu-id="27cae-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="27cae-200">Olá seguinte definição configura Olá resposta tooa negada o pedido:</span><span class="sxs-lookup"><span data-stu-id="27cae-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="27cae-201">Consulte a documentação do toohello para segurança IP dinâmica no IIS para outros valores suportados.</span><span class="sxs-lookup"><span data-stu-id="27cae-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="27cae-202">Operações para configurar certificados de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="27cae-203">Este tópico é apenas de referência.</span><span class="sxs-lookup"><span data-stu-id="27cae-203">This topic is for reference only.</span></span> <span data-ttu-id="27cae-204">Siga os passos de configuração de Olá descritos em:</span><span class="sxs-lookup"><span data-stu-id="27cae-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="27cae-205">Configurar um certificado SSL Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="27cae-206">Configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="27cae-207">Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-207">Create a self-signed certificate</span></span>
<span data-ttu-id="27cae-208">Execute:</span><span class="sxs-lookup"><span data-stu-id="27cae-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="27cae-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="27cae-209">toocustomize:</span></span>

* <span data-ttu-id="27cae-210">-n com Olá URL de serviço.</span><span class="sxs-lookup"><span data-stu-id="27cae-210">-n with hello service URL.</span></span> <span data-ttu-id="27cae-211">Carateres universais ("CN = * .cloudapp .net") e os nomes alternativos ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") são suportados.</span><span class="sxs-lookup"><span data-stu-id="27cae-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="27cae-212">-i com data de expiração do certificado Olá criar uma palavra-passe segura e especifique-quando lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="27cae-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="27cae-213">Criar o ficheiro PFX de certificado SSL autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="27cae-214">Execute:</span><span class="sxs-lookup"><span data-stu-id="27cae-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="27cae-215">Introduza a palavra-passe e, em seguida, exportar o certificado com estas opções:</span><span class="sxs-lookup"><span data-stu-id="27cae-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="27cae-216">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-216">Yes, export hello private key</span></span>
* <span data-ttu-id="27cae-217">Exportar todas as propriedades expandidas</span><span class="sxs-lookup"><span data-stu-id="27cae-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="27cae-218">Exportar o certificado SSL do arquivo de certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="27cae-219">Localizar o certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-219">Find certificate</span></span>
* <span data-ttu-id="27cae-220">Clique em ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="27cae-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="27cae-221">Exportar o certificado para um. Ficheiro PFX com estas opções:</span><span class="sxs-lookup"><span data-stu-id="27cae-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="27cae-222">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="27cae-223">Incluir todos os certificados no caminho de certificação de Olá se for possível * exportar propriedades expandidas tudo</span><span class="sxs-lookup"><span data-stu-id="27cae-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="27cae-224">Carregar o serviço de toocloud do certificado SSL</span><span class="sxs-lookup"><span data-stu-id="27cae-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="27cae-225">Carregue o certificado com Olá existente ou gerado. Ficheiro PFX com Olá par de chaves de SSL:</span><span class="sxs-lookup"><span data-stu-id="27cae-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="27cae-226">Introduza a palavra-passe Olá a proteger as informações de chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="27cae-227">Atualizar o certificado SSL no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="27cae-228">Atualize o valor do thumbprint de Olá de Olá definição no ficheiro de configuração do serviço de Olá com o thumbprint Olá do serviço em nuvem do Olá certificado carregado toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="27cae-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="27cae-229">Importar a autoridade de certificação de SSL</span><span class="sxs-lookup"><span data-stu-id="27cae-229">Import SSL certification authority</span></span>
<span data-ttu-id="27cae-230">Siga estes passos em todos os conta/máquina que irão comunicar com o serviço de Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="27cae-231">Faça duplo clique Olá. Ficheiro CER no Explorador do Windows</span><span class="sxs-lookup"><span data-stu-id="27cae-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="27cae-232">Na caixa de diálogo de certificado Olá, clique em instalar certificado...</span><span class="sxs-lookup"><span data-stu-id="27cae-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="27cae-233">Importar o certificado para Olá que arquivo de autoridades de certificação de raiz fidedigna</span><span class="sxs-lookup"><span data-stu-id="27cae-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="27cae-234">Desativar a autenticação baseada em certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="27cae-235">Apenas a autenticação de baseada em certificado cliente é suportada e a sua desativação permitirá para acesso público toohello pontos finais do serviço, a menos que outros mecanismos estão no local (por exemplo, Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="27cae-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="27cae-236">Altere toofalse estas definições na funcionalidade do Olá serviço de configuração ficheiro tooturn Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="27cae-237">Em seguida, copie Olá mesmo thumbprint como Olá SSL de certificado na definição de certificado Olá AC:</span><span class="sxs-lookup"><span data-stu-id="27cae-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="27cae-238">Criar uma autoridade de certificação autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="27cae-239">Execute os seguintes passos toocreate tooact um certificado autoassinado como uma autoridade de certificação de Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="27cae-240">toocustomize-la</span><span class="sxs-lookup"><span data-stu-id="27cae-240">toocustomize it</span></span>

* <span data-ttu-id="27cae-241">-i com data de expiração de certificação Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="27cae-242">Localizar a chave pública de AC</span><span class="sxs-lookup"><span data-stu-id="27cae-242">Find CA public key</span></span>
<span data-ttu-id="27cae-243">Todos os certificados de cliente tem de ter foi emitidos por uma autoridade de certificação fidedigna pelo serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="27cae-244">Localize toohello de chave pública de Olá autoridade de certificação que emitiu os certificados de cliente Olá que vão toobe utilizado para autenticação no tooupload ordem-toohello o serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="27cae-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="27cae-245">Se o ficheiro de Olá com a chave pública Olá não estiver disponível, exportá-lo a partir do arquivo de certificados de Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="27cae-246">Localizar o certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-246">Find certificate</span></span>
  * <span data-ttu-id="27cae-247">Olá, procure um certificado de cliente emitido pela mesma autoridade de certificação</span><span class="sxs-lookup"><span data-stu-id="27cae-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="27cae-248">Faça duplo clique em certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="27cae-249">Selecione o separador de caminho de certificação de Olá na caixa de diálogo do Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="27cae-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="27cae-250">Faça duplo clique entrada de AC Olá no caminho de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="27cae-251">Toma nota de propriedades do certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="27cae-252">Fechar Olá **certificado** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27cae-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="27cae-253">Localizar o certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-253">Find certificate</span></span>
  * <span data-ttu-id="27cae-254">Procure Olá AC referido acima.</span><span class="sxs-lookup"><span data-stu-id="27cae-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="27cae-255">Clique em ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="27cae-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="27cae-256">Exportar o certificado para um. CER com estas opções:</span><span class="sxs-lookup"><span data-stu-id="27cae-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="27cae-257">**Não, não exportar chave privada Olá**</span><span class="sxs-lookup"><span data-stu-id="27cae-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="27cae-258">Inclua todos os certificados no caminho de certificação de Olá se possível.</span><span class="sxs-lookup"><span data-stu-id="27cae-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="27cae-259">Exporte todas as propriedades expandidas.</span><span class="sxs-lookup"><span data-stu-id="27cae-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="27cae-260">Carregar o serviço de toocloud de certificado de AC</span><span class="sxs-lookup"><span data-stu-id="27cae-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="27cae-261">Carregue o certificado com Olá existente ou gerado. Ficheiro CER com a chave pública Olá AC.</span><span class="sxs-lookup"><span data-stu-id="27cae-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="27cae-262">Certificado da AC de atualização no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="27cae-263">Atualize o valor do thumbprint de Olá de Olá definição no ficheiro de configuração do serviço de Olá com o thumbprint Olá do serviço em nuvem do Olá certificado carregado toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="27cae-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="27cae-264">Atualizar o valor Olá Olá seguinte definição com Olá mesmo thumbprint:</span><span class="sxs-lookup"><span data-stu-id="27cae-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="27cae-265">Emitir certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-265">Issue client certificates</span></span>
<span data-ttu-id="27cae-266">Cada serviço de Olá individuais tooaccess autorizados deve ter um certificado de cliente emitido para his/hers exclusivo utilizar e deve escolher que HIS/hers proprietário tooprotect de palavra-passe segura respetiva chave privada.</span><span class="sxs-lookup"><span data-stu-id="27cae-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="27cae-267">Olá, seguindo os passos tem de ser executado na mesma máquina onde Olá AC um certificado autoassinado foi gerada e armazenada de Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="27cae-268">Personalizar:</span><span class="sxs-lookup"><span data-stu-id="27cae-268">Customizing:</span></span>

* <span data-ttu-id="27cae-269">-n com um ID de cliente de toohello que será autenticada com este certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="27cae-270">-i com data de expiração do certificado Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="27cae-271">MyID.pvk e MyID.cer com os nomes de ficheiro exclusivo para este certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="27cae-272">Este comando irá solicitar uma toobe de palavra-passe criada e, em seguida, utilizado uma vez.</span><span class="sxs-lookup"><span data-stu-id="27cae-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="27cae-273">Utilize uma palavra-passe segura.</span><span class="sxs-lookup"><span data-stu-id="27cae-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="27cae-274">Criar ficheiros PFX para o cliente certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="27cae-275">Para cada certificado de cliente gerado, execute:</span><span class="sxs-lookup"><span data-stu-id="27cae-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="27cae-276">Personalizar:</span><span class="sxs-lookup"><span data-stu-id="27cae-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="27cae-277">Introduza a palavra-passe e, em seguida, exportar o certificado com estas opções:</span><span class="sxs-lookup"><span data-stu-id="27cae-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="27cae-278">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-278">Yes, export hello private key</span></span>
* <span data-ttu-id="27cae-279">Exportar todas as propriedades expandidas</span><span class="sxs-lookup"><span data-stu-id="27cae-279">Export all extended properties</span></span>
* <span data-ttu-id="27cae-280">Olá toowhom individuais, que este certificado emitido deve escolher a palavra-passe de exportação de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="27cae-281">Importar o certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-281">Import client certificate</span></span>
<span data-ttu-id="27cae-282">Cada indivíduo para o qual foi emitido um certificado de cliente deve importar par de chaves Olá máquinas Olá he/she utilizará toocommunicate com o serviço de Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="27cae-283">Faça duplo clique Olá. Ficheiro PFX no Explorador do Windows</span><span class="sxs-lookup"><span data-stu-id="27cae-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="27cae-284">Importar o certificado para Olá pessoal armazenar com, pelo menos, esta opção:</span><span class="sxs-lookup"><span data-stu-id="27cae-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="27cae-285">Incluir todas as propriedades expandidas marcadas</span><span class="sxs-lookup"><span data-stu-id="27cae-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="27cae-286">Copie os thumbprints de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="27cae-287">Cada indivíduo para o qual foi emitido um certificado de cliente tem de seguir estes passos na ordem tooobtain Olá thumbprint his/hers certificado que será adicionado toohello ficheiro de configuração de serviço:</span><span class="sxs-lookup"><span data-stu-id="27cae-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="27cae-288">Executar certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="27cae-288">Run certmgr.exe</span></span>
* <span data-ttu-id="27cae-289">Selecione o separador Personal Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-289">Select hello Personal tab</span></span>
* <span data-ttu-id="27cae-290">Faça duplo clique em certificado de cliente de Olá toobe utilizado para autenticação</span><span class="sxs-lookup"><span data-stu-id="27cae-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="27cae-291">Olá certificado caixa de diálogo que se abre, selecione o separador de detalhes de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="27cae-292">Certifique-se que apresenta Mostrar tudo</span><span class="sxs-lookup"><span data-stu-id="27cae-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="27cae-293">Campo de Olá selecione denominado Thumbprint na lista de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="27cae-294">Copiar Olá valor do thumbprint Olá * * eliminar carateres Unicode não visível à frente dígito primeiro Olá * * eliminar todos os espaços</span><span class="sxs-lookup"><span data-stu-id="27cae-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="27cae-295">Configurar clientes permitido no ficheiro de configuração do serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="27cae-296">Atualize o valor de Olá de Olá definição no ficheiro de configuração do serviço de Olá com uma lista separada por vírgulas de thumbprints Olá Olá certificados de cliente permitidas acesso toohello serviço os seguintes:</span><span class="sxs-lookup"><span data-stu-id="27cae-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="27cae-297">Configurar a verificação de revogação de certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="27cae-298">não verifica a predefinição de Olá com Olá autoridade de certificação para o estado de revogação de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="27cae-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="27cae-299">verificações de tooturn no Olá, se Olá autoridade de certificação que emitiu certificados de cliente Olá suportar estas verificações, alterar Olá seguinte definição com um dos valores de Olá definidos no Olá X509RevocationMode enumeração:</span><span class="sxs-lookup"><span data-stu-id="27cae-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="27cae-300">Criar o ficheiro PFX para certificados de encriptação autoassinado</span><span class="sxs-lookup"><span data-stu-id="27cae-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="27cae-301">Para um certificado de encriptação, execute:</span><span class="sxs-lookup"><span data-stu-id="27cae-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="27cae-302">Personalizar:</span><span class="sxs-lookup"><span data-stu-id="27cae-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="27cae-303">Introduza a palavra-passe e, em seguida, exportar o certificado com estas opções:</span><span class="sxs-lookup"><span data-stu-id="27cae-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="27cae-304">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-304">Yes, export hello private key</span></span>
* <span data-ttu-id="27cae-305">Exportar todas as propriedades expandidas</span><span class="sxs-lookup"><span data-stu-id="27cae-305">Export all extended properties</span></span>
* <span data-ttu-id="27cae-306">Precisa de palavra-passe de Olá ao carregar o serviço em nuvem do Olá certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="27cae-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="27cae-307">Exportar o certificado de encriptação do arquivo de certificados</span><span class="sxs-lookup"><span data-stu-id="27cae-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="27cae-308">Localizar o certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-308">Find certificate</span></span>
* <span data-ttu-id="27cae-309">Clique em ações -> todas as tarefas -> Exportar...</span><span class="sxs-lookup"><span data-stu-id="27cae-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="27cae-310">Exportar o certificado para um. Ficheiro PFX com estas opções:</span><span class="sxs-lookup"><span data-stu-id="27cae-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="27cae-311">Sim, exportar a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="27cae-312">Incluir todos os certificados no caminho de certificação de Olá se possível</span><span class="sxs-lookup"><span data-stu-id="27cae-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="27cae-313">Exportar todas as propriedades expandidas</span><span class="sxs-lookup"><span data-stu-id="27cae-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="27cae-314">Carregar o serviço de toocloud de certificado de encriptação</span><span class="sxs-lookup"><span data-stu-id="27cae-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="27cae-315">Carregue o certificado com Olá existente ou gerado. Ficheiro PFX com o par de chaves de encriptação de Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="27cae-316">Introduza a palavra-passe Olá a proteger as informações de chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="27cae-317">Atualizar o certificado de encriptação no ficheiro de configuração de serviço</span><span class="sxs-lookup"><span data-stu-id="27cae-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="27cae-318">Atualize o valor do thumbprint de Olá de Olá definições no ficheiro de configuração do serviço de Olá com o thumbprint Olá do serviço em nuvem do Olá certificado carregado toohello os seguintes:</span><span class="sxs-lookup"><span data-stu-id="27cae-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="27cae-319">Operações comuns do certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-319">Common certificate operations</span></span>
* <span data-ttu-id="27cae-320">Configurar um certificado SSL Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="27cae-321">Configurar certificados de cliente</span><span class="sxs-lookup"><span data-stu-id="27cae-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="27cae-322">Localizar o certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-322">Find certificate</span></span>
<span data-ttu-id="27cae-323">Siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="27cae-323">Follow these steps:</span></span>

1. <span data-ttu-id="27cae-324">Execute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="27cae-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="27cae-325">Ficheiro -> Adicionar/Remover Snap-in...</span><span class="sxs-lookup"><span data-stu-id="27cae-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="27cae-326">Selecione **certificados**.</span><span class="sxs-lookup"><span data-stu-id="27cae-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="27cae-327">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="27cae-327">Click **Add**.</span></span>
5. <span data-ttu-id="27cae-328">Escolha a localização do arquivo de certificados de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="27cae-329">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="27cae-329">Click **Finish**.</span></span>
7. <span data-ttu-id="27cae-330">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27cae-330">Click **OK**.</span></span>
8. <span data-ttu-id="27cae-331">Expanda **certificados**.</span><span class="sxs-lookup"><span data-stu-id="27cae-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="27cae-332">Expanda o nó de arquivo de certificados de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="27cae-333">Expanda o nó secundário do Olá certificado.</span><span class="sxs-lookup"><span data-stu-id="27cae-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="27cae-334">Selecione um certificado na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="27cae-335">Exportar certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-335">Export certificate</span></span>
<span data-ttu-id="27cae-336">No Olá **Assistente para exportar certificados**:</span><span class="sxs-lookup"><span data-stu-id="27cae-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="27cae-337">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="27cae-337">Click **Next**.</span></span>
2. <span data-ttu-id="27cae-338">Selecione **Sim**, em seguida, **chave privada do exportação Olá**.</span><span class="sxs-lookup"><span data-stu-id="27cae-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="27cae-339">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="27cae-339">Click **Next**.</span></span>
4. <span data-ttu-id="27cae-340">Selecione o formato de ficheiro de saída pretendidas Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="27cae-341">Verifique as opções de Olá assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="27cae-341">Check hello desired options.</span></span>
6. <span data-ttu-id="27cae-342">Verifique **palavra-passe**.</span><span class="sxs-lookup"><span data-stu-id="27cae-342">Check **Password**.</span></span>
7. <span data-ttu-id="27cae-343">Introduza uma palavra-passe segura e confirmá-la.</span><span class="sxs-lookup"><span data-stu-id="27cae-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="27cae-344">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="27cae-344">Click **Next**.</span></span>
9. <span data-ttu-id="27cae-345">Escreva ou procure um nome de ficheiro onde toostore Olá certificado (utilizar um. Extensão PFX).</span><span class="sxs-lookup"><span data-stu-id="27cae-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="27cae-346">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="27cae-346">Click **Next**.</span></span>
11. <span data-ttu-id="27cae-347">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="27cae-347">Click **Finish**.</span></span>
12. <span data-ttu-id="27cae-348">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27cae-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="27cae-349">Importar certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-349">Import certificate</span></span>
<span data-ttu-id="27cae-350">No Assistente para importar certificados Olá:</span><span class="sxs-lookup"><span data-stu-id="27cae-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="27cae-351">Selecione a localização do arquivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="27cae-352">Selecione **utilizador atual** se apenas a processos em execução em utilizador atual serão aceder ao serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="27cae-353">Selecione **máquina Local** se outros processos neste computador forem aceder ao serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="27cae-354">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="27cae-354">Click **Next**.</span></span>
3. <span data-ttu-id="27cae-355">Se importar de um ficheiro, confirme o caminho do ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="27cae-356">Se importar um. Ficheiro PFX:</span><span class="sxs-lookup"><span data-stu-id="27cae-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="27cae-357">Introduza a palavra-passe Olá a proteger a chave privada Olá</span><span class="sxs-lookup"><span data-stu-id="27cae-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="27cae-358">Selecione as opções de importação</span><span class="sxs-lookup"><span data-stu-id="27cae-358">Select import options</span></span>
5. <span data-ttu-id="27cae-359">Selecionar certificados de "Local" em Olá seguir arquivo</span><span class="sxs-lookup"><span data-stu-id="27cae-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="27cae-360">Clique em **Browse** (Procurar).</span><span class="sxs-lookup"><span data-stu-id="27cae-360">Click **Browse**.</span></span>
7. <span data-ttu-id="27cae-361">Selecione arquivo de Olá pretendido.</span><span class="sxs-lookup"><span data-stu-id="27cae-361">Select hello desired store.</span></span>
8. <span data-ttu-id="27cae-362">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="27cae-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="27cae-363">Se for escolhido o arquivo de autoridade de certificação de raiz fidedigna Olá, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="27cae-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="27cae-364">Clique em **OK** em todas as janelas de caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="27cae-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="27cae-365">Carregar certificado</span><span class="sxs-lookup"><span data-stu-id="27cae-365">Upload certificate</span></span>
<span data-ttu-id="27cae-366">No Olá [Portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="27cae-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="27cae-367">Selecione **serviços em nuvem**.</span><span class="sxs-lookup"><span data-stu-id="27cae-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="27cae-368">Selecione o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="27cae-369">No menu superior Olá, clique em **certificados**.</span><span class="sxs-lookup"><span data-stu-id="27cae-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="27cae-370">Na barra inferior de Olá, clique em **carregar**.</span><span class="sxs-lookup"><span data-stu-id="27cae-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="27cae-371">Selecione o ficheiro de certificado Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="27cae-372">Se é um. PFX ficheiro, introduza a palavra-passe de Olá para a chave privada Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="27cae-373">Depois de concluída, copie o thumbprint do certificado Olá da nova entrada de Olá na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="27cae-374">Outras considerações de segurança</span><span class="sxs-lookup"><span data-stu-id="27cae-374">Other security considerations</span></span>
<span data-ttu-id="27cae-375">as definições de SSL de Olá descritas neste documento encriptam a comunicação entre o serviço de Olá e respetivos clientes quando o ponto final de HTTPS de Olá é utilizado.</span><span class="sxs-lookup"><span data-stu-id="27cae-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="27cae-376">Isto é importante porque as credenciais de acesso de base de dados e possivelmente outras informações confidenciais contidas na comunicação de Olá.</span><span class="sxs-lookup"><span data-stu-id="27cae-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="27cae-377">Tenha em atenção, no entanto, de que o serviço de Olá persistir estado interno, incluindo credenciais, no respetivas internas tabelas na base de dados do Microsoft Azure SQL Olá que forneceu para o armazenamento de metadados na sua subscrição do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="27cae-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="27cae-378">A base de dados foi definido como parte da Olá seguinte definição no ficheiro de configuração de serviço (. Ficheiro CSCFG):</span><span class="sxs-lookup"><span data-stu-id="27cae-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="27cae-379">As credenciais armazenadas nesta base de dados são encriptadas.</span><span class="sxs-lookup"><span data-stu-id="27cae-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="27cae-380">No entanto, como melhor prática, certifique-se de que são mantidas funções web e de trabalho das implementações serviço cópia de segurança toodate e segura à medida que têm acesso toohello metadados da base de dados e Olá certificado utilizado para encriptação e desencriptação de credenciais armazenadas.</span><span class="sxs-lookup"><span data-stu-id="27cae-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

