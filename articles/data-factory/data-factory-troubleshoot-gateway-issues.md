---
title: problemas de Data Management Gateway aaaTroubleshoot | Microsoft Docs
description: "Fornece sugestões tootroubleshoot problemas relacionados tooData Management Gateway."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="0baf6-103">Utilizar o Data Management Gateway para resolver problemas</span><span class="sxs-lookup"><span data-stu-id="0baf6-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="0baf6-104">Este artigo fornece informações sobre como resolver problemas com a utilização do Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="0baf6-105">Consulte Olá [Data Management Gateway](data-factory-data-management-gateway.md) artigo para obter informações detalhadas sobre o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="0baf6-106">Consulte Olá [mover dados entre no local e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções de mover dados de um tooMicrosoft de base de dados do SQL Server no local Blob storage do Azure utilizando o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="0baf6-107">Gateway de tooinstall ou registar com falhas</span><span class="sxs-lookup"><span data-stu-id="0baf6-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="0baf6-108">1. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-108">1. Problem</span></span>
<span data-ttu-id="0baf6-109">Pode ver esta mensagem de erro quando instalar e registar um gateway, especificamente, ao transferir o ficheiro de instalação do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="0baf6-110">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-110">Cause</span></span>
<span data-ttu-id="0baf6-111">Olá da máquina em que está a tentar o gateway de Olá tooinstall falhou toodownload Olá mais recente gateway ficheiro de instalação do Centro de transferências Olá devido tooa problema de rede.</span><span class="sxs-lookup"><span data-stu-id="0baf6-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-112">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-112">Resolution</span></span>
<span data-ttu-id="0baf6-113">Verifique a sua toosee de definições de servidor de proxy de firewall se as definições de Olá bloqueiam a ligação de rede Olá do Olá computador toohello [Centro de transferências](https://download.microsoft.com/)e atualizar as definições de Olá em conformidade.</span><span class="sxs-lookup"><span data-stu-id="0baf6-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="0baf6-114">Em alternativa, pode transferir o ficheiro de instalação Olá gateway mais recente Olá da Olá [Centro de transferências](https://www.microsoft.com/download/details.aspx?id=39717) nas outras máquinas que podem aceder ao centro de transferências Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="0baf6-115">Pode, em seguida, o gateway de toohello do ficheiro de instalador do cópia Olá computador anfitrião e executá-la manualmente tooinstall e a atualização de gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="0baf6-116">2. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-116">2. Problem</span></span>
<span data-ttu-id="0baf6-117">Este erro ocorrer quando está a tentar tooinstall um gateway clicando **instalar diretamente neste computador** no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0baf6-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="0baf6-118">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-118">Cause</span></span>
<span data-ttu-id="0baf6-119">Já existe um gateway instalado na máquina de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-120">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-120">Resolution</span></span>
<span data-ttu-id="0baf6-121">Desinstalar o gateway existente do Olá na máquina de Olá e clique em Olá **instalar diretamente neste computador** ligar novamente.</span><span class="sxs-lookup"><span data-stu-id="0baf6-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="0baf6-122">3. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-122">3. Problem</span></span>
<span data-ttu-id="0baf6-123">Poderá ver este erro ao registar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="0baf6-124">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-124">Cause</span></span>
<span data-ttu-id="0baf6-125">Poderá ver esta mensagem para uma das Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="0baf6-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="0baf6-126">formato de Olá da chave de gateway Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="0baf6-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="0baf6-127">chave do gateway Olá foi invalidado.</span><span class="sxs-lookup"><span data-stu-id="0baf6-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="0baf6-128">a chave de gateway Olá tem foi regenerada do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="0baf6-129">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-129">Resolution</span></span>
<span data-ttu-id="0baf6-130">Certifique-se de que o se estiver a utilizar a chave de gateway correto de Olá partir Olá do portal.</span><span class="sxs-lookup"><span data-stu-id="0baf6-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="0baf6-131">Se for necessário, voltar a gerar uma chave e utilizar Olá tooregister chave Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="0baf6-132">4. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-132">4. Problem</span></span>
<span data-ttu-id="0baf6-133">Poderá ver Olá seguir a mensagem de erro quando está a registar um gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Conteúdo ou formato de chave é inválido](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="0baf6-135">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-135">Cause</span></span>
<span data-ttu-id="0baf6-136">Olá conteúdo ou formato de chave do gateway de entrada de Olá está incorreto.</span><span class="sxs-lookup"><span data-stu-id="0baf6-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="0baf6-137">Uma das razões Olá pode ser que copiou apenas uma parte da chave de Olá do portal de Olá ou estiver a utilizar uma chave inválida.</span><span class="sxs-lookup"><span data-stu-id="0baf6-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-138">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-138">Resolution</span></span>
<span data-ttu-id="0baf6-139">Gerar uma chave de gateway no portal de Olá e utilize Olá cópia botão toocopy Olá todo chave.</span><span class="sxs-lookup"><span data-stu-id="0baf6-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="0baf6-140">Em seguida, cole-o no gateway de Olá de tooregister janela.</span><span class="sxs-lookup"><span data-stu-id="0baf6-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="0baf6-141">5. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-141">5. Problem</span></span>
<span data-ttu-id="0baf6-142">Poderá ver Olá seguir a mensagem de erro quando está a registar um gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Chave do gateway é inválido ou está vazio](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="0baf6-144">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-144">Cause</span></span>
<span data-ttu-id="0baf6-145">chave do gateway Olá foi regenerada ou gateway Olá foi eliminada no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0baf6-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="0baf6-146">Também pode acontecer se a configuração do Data Management Gateway Olá não é mais recente.</span><span class="sxs-lookup"><span data-stu-id="0baf6-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-147">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-147">Resolution</span></span>
<span data-ttu-id="0baf6-148">Verifique se a configuração do Data Management Gateway Olá é uma versão mais recente Olá, pode encontrar a versão mais recente do Olá no Olá Microsoft [Centro de transferências](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="0baf6-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="0baf6-149">Se a configuração atual / mais recente e gateway ainda existe no Portal, regenerar a chave de gateway Olá no Olá portal do Azure e utilizar Olá cópia botão toocopy Olá todo chave e, em seguida, cole-o no gateway de Olá de tooregister janela.</span><span class="sxs-lookup"><span data-stu-id="0baf6-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="0baf6-150">Caso contrário, recriar o gateway de Olá e comece de novo.</span><span class="sxs-lookup"><span data-stu-id="0baf6-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="0baf6-151">6. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-151">6. Problem</span></span>
<span data-ttu-id="0baf6-152">Poderá ver Olá seguir a mensagem de erro quando está a registar um gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Chave do gateway é inválido ou está vazio](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="0baf6-154">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-154">Cause</span></span>
<span data-ttu-id="0baf6-155">Este erro pode ter acontecido porque o gateway Olá foi eliminado ou chave de gateway associado Olá foi regenerada.</span><span class="sxs-lookup"><span data-stu-id="0baf6-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-156">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-156">Resolution</span></span>
<span data-ttu-id="0baf6-157">Se tiverem sido eliminado gateway Olá, voltar a criar gateway de Olá a partir do portal de Olá, clique em **registar**, copie a chave de Olá portal Olá, cole-o e tente o gateway de Olá tooregister.</span><span class="sxs-lookup"><span data-stu-id="0baf6-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="0baf6-158">Se o gateway de Olá ainda existe mas a chave foi regenerada, utilize Olá novo tooregister chave Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="0baf6-159">Se não tiver chave Olá, regenere a chave de Olá novamente a partir do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="0baf6-160">7. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-160">7. Problem</span></span>
<span data-ttu-id="0baf6-161">Quando estiver a registar um gateway, poderá ser necessário tooenter caminho e a palavra-passe de um certificado.</span><span class="sxs-lookup"><span data-stu-id="0baf6-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Especifique o certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="0baf6-163">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-163">Cause</span></span>
<span data-ttu-id="0baf6-164">gateway de Olá foi registado em outras máquinas antes.</span><span class="sxs-lookup"><span data-stu-id="0baf6-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="0baf6-165">Durante o registo do Olá inicial de um gateway, um certificado de encriptação foi associado ao gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="0baf6-166">certificado Olá pode ser personalizada gerado pelo gateway de Olá ou fornecido pelo utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="0baf6-167">Este certificado é utilizado tooencrypt credenciais Olá do arquivo de dados (serviço ligado).</span><span class="sxs-lookup"><span data-stu-id="0baf6-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Exportar certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="0baf6-169">Quando restaurar gateway Olá no outro computador anfitrião, o Assistente de registo de Olá pede-lhe para toodecrypt este certificado de credenciais anteriormente encriptados com este certificado.</span><span class="sxs-lookup"><span data-stu-id="0baf6-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="0baf6-170">Sem este certificado não não possível desencriptar as credenciais de Olá ao novo gateway de Olá e execuções de atividade de cópia subsequentes associadas a este novo gateway falhará.</span><span class="sxs-lookup"><span data-stu-id="0baf6-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="0baf6-171">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-171">Resolution</span></span>
<span data-ttu-id="0baf6-172">Se exportou certificado da credencial Olá da máquina de gateway original Olá utilizando Olá **exportar** botão Olá **definições** separador no Data Management Gateway do Configuration Manager, utilize Olá certificado aqui.</span><span class="sxs-lookup"><span data-stu-id="0baf6-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="0baf6-173">Não é possível ignorar esta fase ao recuperar um gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="0baf6-174">Se o certificado de Olá está em falta, precisa de gateway de Olá toodelete do portal de Olá e voltar a criar um novo gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="0baf6-175">Além disso, atualize todos os serviços ligados que estão relacionados toohello gateway por reentering as respetivas credenciais.</span><span class="sxs-lookup"><span data-stu-id="0baf6-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="0baf6-176">8. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-176">8. Problem</span></span>
<span data-ttu-id="0baf6-177">Poderá ver Olá seguir a mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="0baf6-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="0baf6-178">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-178">Cause</span></span>
<span data-ttu-id="0baf6-179">Este erro ocorre quando o gateway está num ambiente que requer um tooaccess de proxy HTTP recursos da Internet, ou palavra-passe de autenticação do proxy é alterado, mas não é atualizado em conformidade no seu gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-180">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-180">Resolution</span></span>
<span data-ttu-id="0baf6-181">Siga as instruções de Olá Olá [considerações de servidor Proxy](#proxy-server-considerations) secção deste artigo e configurar as definições de proxy com o Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="0baf6-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="0baf6-182">Gateway está online com funcionalidade limitada</span><span class="sxs-lookup"><span data-stu-id="0baf6-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="0baf6-183">1. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-183">1. Problem</span></span>
<span data-ttu-id="0baf6-184">Ver o estado de Olá do gateway de Olá como online com funcionalidade limitada.</span><span class="sxs-lookup"><span data-stu-id="0baf6-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="0baf6-185">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-185">Cause</span></span>
<span data-ttu-id="0baf6-186">Ver estado Olá do gateway de Olá como online com funcionalidade limitada para uma das Olá seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="0baf6-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="0baf6-187">Gateway não é possível ligar o serviço de toocloud através do Service Bus do Azure.</span><span class="sxs-lookup"><span data-stu-id="0baf6-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="0baf6-188">Serviço em nuvem não é possível ligar toogateway através do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0baf6-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="0baf6-189">Quando o gateway de Olá está online com funcionalidade limitada, poderá não ser pipelines de dados do toocreate do toouse capaz de Olá Assistente de cópia do Data Factory para copiar dados tooor de arquivos de dados no local.</span><span class="sxs-lookup"><span data-stu-id="0baf6-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="0baf6-190">Como solução, pode utilizar o Editor do Data Factory no portal de Olá, Visual Studio ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0baf6-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-191">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-191">Resolution</span></span>
<span data-ttu-id="0baf6-192">Resolução para este problema (online com funcionalidade limitada) baseia-se no se o gateway de Olá não é possível ligar o serviço em nuvem toohello ou Olá outra forma.</span><span class="sxs-lookup"><span data-stu-id="0baf6-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="0baf6-193">Olá seguintes secções fornece estas resoluções.</span><span class="sxs-lookup"><span data-stu-id="0baf6-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="0baf6-194">2. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-194">2. Problem</span></span>
<span data-ttu-id="0baf6-195">Consulte Olá seguir o erro.</span><span class="sxs-lookup"><span data-stu-id="0baf6-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Gateway não é possível ligar o serviço de toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="0baf6-197">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-197">Cause</span></span>
<span data-ttu-id="0baf6-198">Gateway não é possível ligar o serviço em nuvem toohello através do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0baf6-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-199">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-199">Resolution</span></span>
<span data-ttu-id="0baf6-200">Siga estes gateway de Olá de tooget de passos online:</span><span class="sxs-lookup"><span data-stu-id="0baf6-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="0baf6-201">Permitir o endereço IP no computador do gateway de Olá e de firewall da empresa Olá as regras de saída.</span><span class="sxs-lookup"><span data-stu-id="0baf6-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="0baf6-202">Pode localizar endereços IP de Olá registo de eventos do Windows (ID = = 401): uma tentativa de foi efetuada tooaccess um socket de forma proibida pelo respetivos permissões de acesso XX. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="0baf6-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="0baf6-203">Configure definições de proxy no gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="0baf6-204">Consulte Olá [considerações de servidor Proxy](#proxy-server-considerations) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="0baf6-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="0baf6-205">Ative portas de saída 5671 e 9350-9354 em ambos os Olá Firewall do Windows no computador do gateway de Olá e firewall Olá da empresa.</span><span class="sxs-lookup"><span data-stu-id="0baf6-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="0baf6-206">Consulte Olá [portas e firewall](#ports-and-firewall) secção para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="0baf6-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="0baf6-207">Este passo é opcional, mas recomendamos por razões de desempenho de.</span><span class="sxs-lookup"><span data-stu-id="0baf6-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="0baf6-208">3. Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-208">3. Problem</span></span>
<span data-ttu-id="0baf6-209">Consulte Olá seguir o erro.</span><span class="sxs-lookup"><span data-stu-id="0baf6-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="0baf6-210">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-210">Cause</span></span>
<span data-ttu-id="0baf6-211">Um erro transitório na conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="0baf6-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-212">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-212">Resolution</span></span>
<span data-ttu-id="0baf6-213">Siga estes gateway de Olá de tooget de passos online:</span><span class="sxs-lookup"><span data-stu-id="0baf6-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="0baf6-214">Aguarde alguns minutos, conectividade Olá irá ser recuperada automaticamente quando o erro de Olá é removido.</span><span class="sxs-lookup"><span data-stu-id="0baf6-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="0baf6-215">Se Olá erro persistir, reinicie o serviço de gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="0baf6-216">Serviço de falha tooauthor ligado</span><span class="sxs-lookup"><span data-stu-id="0baf6-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="0baf6-217">Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-217">Problem</span></span>
<span data-ttu-id="0baf6-218">Poderá ver este erro quando tentar toouse Gestor de credenciais em credenciais de portal tooinput Olá para um novo serviço ligado ou atualizar as credenciais de um serviço ligado existente.</span><span class="sxs-lookup"><span data-stu-id="0baf6-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="0baf6-219">Quando vir este erro, página de definições de Olá do Data Management Gateway Configuration Manager aspeto que poderá ter Olá seguinte captura de ecrã.</span><span class="sxs-lookup"><span data-stu-id="0baf6-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Não é possível contactar a base de dados](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="0baf6-221">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-221">Cause</span></span>
<span data-ttu-id="0baf6-222">certificado SSL Olá pode ter sido perdido no computador do gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="0baf6-223">computador do gateway Olá não é possível carregar Olá certificado atualmente que é utilizado para encriptação SSL.</span><span class="sxs-lookup"><span data-stu-id="0baf6-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="0baf6-224">Também poderá ver uma mensagem de erro no registo de eventos de Olá que é semelhante toohello seguir a mensagem.</span><span class="sxs-lookup"><span data-stu-id="0baf6-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="0baf6-225">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-225">Resolution</span></span>
<span data-ttu-id="0baf6-226">Siga o problema de Olá de toosolve estes passos:</span><span class="sxs-lookup"><span data-stu-id="0baf6-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="0baf6-227">Inicie o Gestor de configuração do Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="0baf6-228">Comutador toohello **definições** separador.</span><span class="sxs-lookup"><span data-stu-id="0baf6-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="0baf6-229">Clique em Olá **alteração** certificado SSL do botão toochange Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![Botão de certificado de alteração](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="0baf6-231">Selecione um novo certificado como certificado SSL Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="0baf6-232">Pode utilizar qualquer certificado SSL que é gerado por si ou qualquer organização.</span><span class="sxs-lookup"><span data-stu-id="0baf6-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Especifique o certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="0baf6-234">Falha da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0baf6-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="0baf6-235">Problema</span><span class="sxs-lookup"><span data-stu-id="0baf6-235">Problem</span></span>
<span data-ttu-id="0baf6-236">É possível que repare Olá seguintes "UserErrorFailedToConnectToSqlserver" falha depois de configurar um pipeline no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="0baf6-237">Causa</span><span class="sxs-lookup"><span data-stu-id="0baf6-237">Cause</span></span>
<span data-ttu-id="0baf6-238">Isto pode acontecer por diferentes motivos e atenuação varia em conformidade.</span><span class="sxs-lookup"><span data-stu-id="0baf6-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0baf6-239">Resolução</span><span class="sxs-lookup"><span data-stu-id="0baf6-239">Resolution</span></span>
<span data-ttu-id="0baf6-240">Permita ligações de TCP de saída através da porta TCP/1433 no Olá do lado do cliente do Data Management Gateway antes de ligar tooan SQL da base de dados.</span><span class="sxs-lookup"><span data-stu-id="0baf6-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="0baf6-241">Se a base de dados de destino de Olá é uma base de dados SQL do Azure, verifique o SQL Server as definições da firewall para o Azure também.</span><span class="sxs-lookup"><span data-stu-id="0baf6-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="0baf6-242">Consulte Olá seguinte secção tootest Olá ligação toohello no local dados arquivo.</span><span class="sxs-lookup"><span data-stu-id="0baf6-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="0baf6-243">Ligação de arquivo de dados ou erros relacionados com o controlador</span><span class="sxs-lookup"><span data-stu-id="0baf6-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="0baf6-244">Se vir armazenar erros relacionados com o controlador ou de ligação de dados, conclua Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0baf6-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="0baf6-245">Inicie o Gestor de configuração do Data Management Gateway no computador do gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="0baf6-246">Comutador toohello **diagnóstico** separador.</span><span class="sxs-lookup"><span data-stu-id="0baf6-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="0baf6-247">No **Testar ligação**, adicione os valores de grupo do Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="0baf6-248">Clique em **teste** toosee se pode ligar toohello no local origem de dados do computador do gateway de Olá utilizando as informações da ligação Olá e as credenciais.</span><span class="sxs-lookup"><span data-stu-id="0baf6-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="0baf6-249">Se continuar a ligação de teste de Olá falhar depois de instalar um controlador, reinício Olá gateway para o mesmo toopick segurança alteração mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Ligação de teste no separador de diagnóstico](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="0baf6-251">Registos do gateway</span><span class="sxs-lookup"><span data-stu-id="0baf6-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="0baf6-252">Enviar tooMicrosoft de registos do gateway</span><span class="sxs-lookup"><span data-stu-id="0baf6-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="0baf6-253">Quando contactar a ajuda de tooget Support da Microsoft com a resolução de problemas de gateway, poderá ser-lhe pedido tooshare os registos do gateway.</span><span class="sxs-lookup"><span data-stu-id="0baf6-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="0baf6-254">Com a versão de Olá do gateway de Olá, pode partilhar os registos de gateway necessária com dois cliques de botão no Data Management Gateway do Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="0baf6-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="0baf6-255">Comutador toohello **diagnóstico** separador no Data Management Gateway do Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="0baf6-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Separador de diagnóstico do Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="0baf6-257">Clique em **enviar registos de** Olá toosee seguintes da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0baf6-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Registos de envio de Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="0baf6-259">(Opcional) Clique em **ver registos** tooreview registos no Visualizador de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="0baf6-260">(Opcional) Clique em **privacidade** tooreview web da Microsoft dos serviços de declaração de privacidade.</span><span class="sxs-lookup"><span data-stu-id="0baf6-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="0baf6-261">Quando estiver satisfeito com o que está prestes a tooupload, clique em **enviar registos de** tooactually enviar registos de Olá dos últimos sete dias tooMicrosoft Olá para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="0baf6-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="0baf6-262">Deverá ver o estado Olá da operação de envio registos Olá conforme mostrado na seguinte captura de ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Data Management Gateway enviar registos de estado](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="0baf6-264">Depois de concluída a operação de Olá, verá uma caixa de diálogo conforme mostrado na seguinte captura de ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Data Management Gateway enviar registos de estado](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="0baf6-266">Guardar Olá **relatório ID** e partilhá-las com Support da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0baf6-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="0baf6-267">Olá relatório ID é utilizado toolocate Olá gateway os registos que carregou para resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="0baf6-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="0baf6-268">ID de relatório Olá também é guardada no Visualizador de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="0baf6-269">Pode encontrá-lo ao observar o ID de evento "25" Olá e verifique Olá data e hora.</span><span class="sxs-lookup"><span data-stu-id="0baf6-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Data Management Gateway enviar registos de ID de relatório](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="0baf6-271">Gateway de arquivo os registos de computador do anfitrião de gateway</span><span class="sxs-lookup"><span data-stu-id="0baf6-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="0baf6-272">Existem alguns cenários em que tiver problemas de gateway e não pode partilhar os registos do gateway diretamente:</span><span class="sxs-lookup"><span data-stu-id="0baf6-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="0baf6-273">Se instalar manualmente o gateway de Olá e registar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="0baf6-274">Repita o gateway de Olá tooregister com uma chave gerada novamente no Data Management Gateway do Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="0baf6-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="0baf6-275">Tente toosend registos e não é possível ligar o serviço de anfitrião de gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="0baf6-276">Nestes cenários, pode guardar registos de gateway como um ficheiro zip e partilhá-las quando contactar o suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0baf6-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="0baf6-277">Por exemplo, se receber um erro ao registar o gateway de Olá como mostrado na seguinte captura de ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Erro de registo de Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="0baf6-279">Clique em Olá **arquivar registos do gateway** associar tooarchive e guarde os registos e, em seguida, partilhar o ficheiro zip Olá com suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0baf6-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Registos de arquivo de Gateway de gestão de dados](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="0baf6-281">Localize os registos do gateway</span><span class="sxs-lookup"><span data-stu-id="0baf6-281">Locate gateway logs</span></span>
<span data-ttu-id="0baf6-282">Pode encontrar informações de registo de gateway detalhadas nos registos de eventos do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0baf6-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="0baf6-283">Iniciar o Windows **Visualizador de eventos**.</span><span class="sxs-lookup"><span data-stu-id="0baf6-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="0baf6-284">Localize os registos no Olá **registos de serviços e aplicações** > **Data Management Gateway** pasta.</span><span class="sxs-lookup"><span data-stu-id="0baf6-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="0baf6-285">Quando estiver a resolver problemas relacionados com o gateway, procure eventos ao nível de erro no Visualizador de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="0baf6-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![O Data Management Gateway se regista no Visualizador de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
