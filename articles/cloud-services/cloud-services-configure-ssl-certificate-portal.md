---
title: "aaaConfigure SSL para um serviço em nuvem | Microsoft Docs"
description: "Saiba como toospecify um ponto final de HTTPS para uma função da web e como tooupload um SSL certificados toosecure a aplicação. Estes exemplos utilizam Olá portal do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="c914a-104">Configurar o SSL para uma aplicação no Azure</span><span class="sxs-lookup"><span data-stu-id="c914a-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c914a-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c914a-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="c914a-106">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="c914a-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="c914a-107">Encriptação do Secure Socket Layer (SSL) é o método de Olá normalmente utilizada de proteger os dados enviados entre Olá internet.</span><span class="sxs-lookup"><span data-stu-id="c914a-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="c914a-108">Esta tarefa comuns aborda como toospecify um ponto final de HTTPS para uma função da web e como tooupload um SSL certificados toosecure a aplicação.</span><span class="sxs-lookup"><span data-stu-id="c914a-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="c914a-109">procedimentos de Olá nesta tarefa aplicam-se os serviços de nuvem tooAzure; para os serviços de aplicação, consulte [isto](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="c914a-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="c914a-110">Esta tarefa utiliza uma implementação de produção.</span><span class="sxs-lookup"><span data-stu-id="c914a-110">This task uses a production deployment.</span></span> <span data-ttu-id="c914a-111">Informações sobre como utilizar uma implementação de teste são fornecidas no fim de Olá deste tópico.</span><span class="sxs-lookup"><span data-stu-id="c914a-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="c914a-112">Leitura [isto](cloud-services-how-to-create-deploy-portal.md) primeiro se ainda não tiver criado um serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="c914a-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="c914a-113">Passo 1: Obter um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="c914a-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="c914a-114">tooconfigure SSL para uma aplicação, terá primeiro tooget um certificado SSL assinado por uma autoridade de certificação (CA), uma terceiros fidedigna, que emite certificados para esta finalidade.</span><span class="sxs-lookup"><span data-stu-id="c914a-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="c914a-115">Se já tiver uma, terá de tooobtain um de uma empresa que sells certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="c914a-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="c914a-116">certificado Olá tem de cumprir os requisitos para certificados SSL no Azure de Olá:</span><span class="sxs-lookup"><span data-stu-id="c914a-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="c914a-117">certificado de Olá tem de conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="c914a-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="c914a-118">certificado de Olá tem de ser criado para a troca de chaves, tooa exportável ficheiro Personal Information Exchange (. pfx).</span><span class="sxs-lookup"><span data-stu-id="c914a-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="c914a-119">Olá nome do requerente do certificado deve corresponder ao serviço de nuvem do Olá domínio utilizado tooaccess Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="c914a-120">Não é possível obter um certificado SSL a partir de uma autoridade de certificação (AC) para o domínio de cloudapp.net Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="c914a-121">Tem de adquirir uma toouse de nome de domínio personalizado ao seu serviço de acesso.</span><span class="sxs-lookup"><span data-stu-id="c914a-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="c914a-122">Quando solicitar um certificado a partir de uma AC, nome do requerente do certificado Olá tem de corresponder ao hello domínio personalizado nome utilizado tooaccess a aplicação.</span><span class="sxs-lookup"><span data-stu-id="c914a-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="c914a-123">Por exemplo, se o nome de domínio personalizado for **contoso.com** seria pedir um certificado da AC para ***. contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c914a-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="c914a-124">certificado de Olá tem de utilizar um mínimo de encriptação de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="c914a-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="c914a-125">Para fins de teste, pode [criar](cloud-services-certs-create.md) e utilizar um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="c914a-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="c914a-126">Um certificado autoassinado não é autenticado através de uma AC e pode utilizar o domínio de cloudapp.net Olá como Olá URL do site.</span><span class="sxs-lookup"><span data-stu-id="c914a-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="c914a-127">Por exemplo, hello tarefa seguinte utiliza um certificado autoassinado que Olá nome comum (CN) utilizado no certificado Olá é **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="c914a-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="c914a-128">Em seguida, tem de incluir informações sobre o certificado de Olá na sua definição de serviço e os ficheiros de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="c914a-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="c914a-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="c914a-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="c914a-130">Passo 2: Modificar Olá de ficheiros de configuração e definição de serviço</span><span class="sxs-lookup"><span data-stu-id="c914a-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="c914a-131">A aplicação tem de ser configurado toouse certificado de Olá e um ponto final de HTTPS tem de ser adicionado.</span><span class="sxs-lookup"><span data-stu-id="c914a-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="c914a-132">Como resultado, hello definição de serviço e os ficheiros de configuração de serviço necessário toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="c914a-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="c914a-133">No seu ambiente de desenvolvimento, abra o ficheiro de definição de serviço Olá (. CSDEF), adicione um **certificados** secção dentro Olá **WebRole** secção e incluir Olá seguintes informações o certificado (e certificados intermediários):</span><span class="sxs-lookup"><span data-stu-id="c914a-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="c914a-134">Olá **certificados** secção define o nome de Olá do nosso certificado, a localização e o nome de Olá do arquivo de olá onde está localizado.</span><span class="sxs-lookup"><span data-stu-id="c914a-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="c914a-135">As permissões (`permisionLevel` atributo) pode ser tooone de conjunto de Olá os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="c914a-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="c914a-136">Valor de permissão</span><span class="sxs-lookup"><span data-stu-id="c914a-136">Permission Value</span></span> | <span data-ttu-id="c914a-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="c914a-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="c914a-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="c914a-138">limitedOrElevated</span></span> |<span data-ttu-id="c914a-139">**(Predefinição)**  Todos os processos de função podem aceder à chave privada Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="c914a-140">elevada</span><span class="sxs-lookup"><span data-stu-id="c914a-140">elevated</span></span> |<span data-ttu-id="c914a-141">Apenas os processos elevados podem aceder à chave privada Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="c914a-142">No seu ficheiro de definição de serviço, adicione um **InputEndpoint** elemento Olá **pontos finais** secção tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="c914a-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="c914a-143">No seu ficheiro de definição de serviço, adicione um **enlace** elemento Olá **Sites** secção.</span><span class="sxs-lookup"><span data-stu-id="c914a-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="c914a-144">Este elemento adiciona um toomap de enlace de HTTPS do site do ponto final tooyour:</span><span class="sxs-lookup"><span data-stu-id="c914a-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="c914a-145">Todos os Olá as alterações necessárias toohello ficheiro de definição serviço foram concluídas; No entanto, ainda precisa de informações do certificado de Olá tooadd para o ficheiro de configuração do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="c914a-146">No seu ficheiro de configuração serviço (CSCFG), Serviceconfiguration, adicione um **certificados** valor com que o certificado.</span><span class="sxs-lookup"><span data-stu-id="c914a-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="c914a-147">Olá exemplo de código seguinte fornece detalhes de Olá **certificados** secção, exceto o valor do thumbprint Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="c914a-148">(Este exemplo utiliza **sha1** para o algoritmo de thumbprint Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="c914a-149">Especificar valor adequado de Olá para o algoritmo de thumbprint do certificado.)</span><span class="sxs-lookup"><span data-stu-id="c914a-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="c914a-150">Agora que foram atualizados Olá serviço definição e o serviço de ficheiros de configuração, a implementação do carregamento tooAzure do pacote.</span><span class="sxs-lookup"><span data-stu-id="c914a-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="c914a-151">Se estiver a utilizar **cspack**, não utilize o **/generateConfigurationFile** sinalizador, como o que irá substituir as informações do certificado que acabou de inserir.</span><span class="sxs-lookup"><span data-stu-id="c914a-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="c914a-152">Passo 3: Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="c914a-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="c914a-153">Ligar toohello portal do Azure e...</span><span class="sxs-lookup"><span data-stu-id="c914a-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="c914a-154">No Olá **todos os recursos** secção Olá Portal, selecione o seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c914a-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Publicar o seu serviço em nuvem](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="c914a-156">Clique em **certificados**.</span><span class="sxs-lookup"><span data-stu-id="c914a-156">Click **Certificates**.</span></span>

    ![Clique Olá certificados ícone](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="c914a-158">Clique em **carregar** em Olá parte superior da área de certificados de Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Clique em item de menu de carregamento de Olá](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="c914a-160">Fornecer Olá **ficheiro**, **palavra-passe**, em seguida, clique em **carregar** na parte inferior de Olá da área de entrada de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="c914a-161">Passo 4: Ligar a instância de função toohello através de HTTPS</span><span class="sxs-lookup"><span data-stu-id="c914a-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="c914a-162">Agora que a implementação está a funcionar no Azure, pode ligar tooit através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c914a-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="c914a-163">Clique em Olá **URL do Site** tooopen segurança browser da web Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Clique em Olá URL do Site](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="c914a-165">No seu browser, modificar Olá ligação toouse **https** em vez de **http**e, em seguida, visitar a página Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c914a-166">Se estiver a utilizar um certificado autoassinado, ao procurar o ponto final de HTTPS de tooan associado ao certificado autoassinado Olá vir um erro de certificado no browser Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="c914a-167">Utilizar um certificado assinado por uma autoridade de certificação fidedignas elimina este problema; no Olá entretanto, pode ignorar o erro de Olá.</span><span class="sxs-lookup"><span data-stu-id="c914a-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="c914a-168">(Outra opção é o arquivo de certificados de autoridade de certificação fidedigna tooadd Olá certificado autoassinado toohello do utilizador.)</span><span class="sxs-lookup"><span data-stu-id="c914a-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Pré-visualização do site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="c914a-170">Se quiser toouse SSL para uma implementação de teste em vez de uma implementação de produção, terá primeiro de toodetermine Olá URL utilizado para Olá implementação de teste.</span><span class="sxs-lookup"><span data-stu-id="c914a-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="c914a-171">Depois de ter sido implementado o seu serviço em nuvem, Olá URL toohello ambiente de teste é determinado pelo Olá **ID de implementação** GUID neste formato:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="c914a-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="c914a-172">Criar um certificado com Olá comum nome (CN) toohello igual baseado no GUID URL (por exemplo, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="c914a-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="c914a-173">Utilize Olá portal tooadd Olá certificado tooyour testado serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="c914a-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="c914a-174">Em seguida, adicionar Olá informações tooyour CSDEF e CSCFG ficheiros de certificado, Empacote novamente esta aplicação e atualizar a sua implementação faseada toouse Olá novo pacote.</span><span class="sxs-lookup"><span data-stu-id="c914a-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="c914a-175">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c914a-175">Next steps</span></span>
* <span data-ttu-id="c914a-176">[Configuração geral do seu serviço de nuvem](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c914a-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="c914a-177">Saiba como demasiado[implementar um serviço em nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c914a-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="c914a-178">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c914a-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="c914a-179">[Gerir o serviço de nuvem](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c914a-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
