---
title: gateway de dados no local aaaInstall | Microsoft Docs
description: Saiba como tooinstall e configure um gateway de dados no local.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="69af3-103">Instalar e configurar um gateway de dados no local</span><span class="sxs-lookup"><span data-stu-id="69af3-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="69af3-104">É necessário um gateway de dados no local quando um ou mais servidores do Azure Analysis Services no Olá mesma região ligar a origens de dados de tooon local.</span><span class="sxs-lookup"><span data-stu-id="69af3-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="69af3-105">toolearn mais sobre o gateway de Olá, consulte [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="69af3-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69af3-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="69af3-106">Prerequisites</span></span>
<span data-ttu-id="69af3-107">**Requisitos mínimos:**</span><span class="sxs-lookup"><span data-stu-id="69af3-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="69af3-108">4.5 do .NET framework</span><span class="sxs-lookup"><span data-stu-id="69af3-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="69af3-109">versão de 64 bits do Windows 7 / Windows Server 2008 R2 (ou posterior)</span><span class="sxs-lookup"><span data-stu-id="69af3-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="69af3-110">**Recomendado:**</span><span class="sxs-lookup"><span data-stu-id="69af3-110">**Recommended:**</span></span>

* <span data-ttu-id="69af3-111">CPU de 8 núcleos</span><span class="sxs-lookup"><span data-stu-id="69af3-111">8 Core CPU</span></span>
* <span data-ttu-id="69af3-112">8 GB de memória</span><span class="sxs-lookup"><span data-stu-id="69af3-112">8 GB Memory</span></span>
* <span data-ttu-id="69af3-113">versão de 64 bits do Windows 2012 R2 (ou posterior)</span><span class="sxs-lookup"><span data-stu-id="69af3-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="69af3-114">**Considerações importantes sobre:**</span><span class="sxs-lookup"><span data-stu-id="69af3-114">**Important considerations:**</span></span>

* <span data-ttu-id="69af3-115">Durante a configuração, quando registar o gateway com o Azure, a região predefinida de Olá para a sua subscrição está selecionada.</span><span class="sxs-lookup"><span data-stu-id="69af3-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="69af3-116">Pode escolher uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="69af3-116">You can choose a different region.</span></span> <span data-ttu-id="69af3-117">Se tiver servidores na região mais do que um, tem de instalar um gateway para cada região.</span><span class="sxs-lookup"><span data-stu-id="69af3-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="69af3-118">gateway de Olá não pode ser instalado num controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="69af3-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="69af3-119">Apenas um gateway pode ser instalado num único computador.</span><span class="sxs-lookup"><span data-stu-id="69af3-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="69af3-120">Instale o gateway de Olá num computador que permanece no e não passa toosleep.</span><span class="sxs-lookup"><span data-stu-id="69af3-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="69af3-121">Não instale o gateway de Olá numa rede de computador tooyour wirelessly ligado.</span><span class="sxs-lookup"><span data-stu-id="69af3-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="69af3-122">Desempenho pode ser o seu.</span><span class="sxs-lookup"><span data-stu-id="69af3-122">Performance can be diminished.</span></span>


## <span data-ttu-id="69af3-123"><a name="download"></a>Transferir</span><span class="sxs-lookup"><span data-stu-id="69af3-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="69af3-124">Transfira o gateway de Olá</span><span class="sxs-lookup"><span data-stu-id="69af3-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="69af3-125"><a name="install"></a>Instalar</span><span class="sxs-lookup"><span data-stu-id="69af3-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="69af3-126">Execute a configuração.</span><span class="sxs-lookup"><span data-stu-id="69af3-126">Run setup.</span></span>

2. <span data-ttu-id="69af3-127">Selecione uma localização, aceite os termos de Olá e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="69af3-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Instalar os termos de localização e a licença](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="69af3-129">Selecione **gateway de dados no local (recomendado)**.</span><span class="sxs-lookup"><span data-stu-id="69af3-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="69af3-130">Azure Analysis Services não suporta o modo pessoal.</span><span class="sxs-lookup"><span data-stu-id="69af3-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Escolha o tipo de gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="69af3-132">Introduza uma conta toosign tooAzure.</span><span class="sxs-lookup"><span data-stu-id="69af3-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="69af3-133">Olá conta tem de ser do Azure Active Directory seu inquilino.</span><span class="sxs-lookup"><span data-stu-id="69af3-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="69af3-134">Esta conta é utilizada para o administrador do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="69af3-134">This account is used for hello gateway administrator.</span></span> 

   ![Introduza uma conta toosign tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="69af3-136">Se iniciar sessão com uma conta de domínio, será mapeada conta institucional tooyour no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69af3-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="69af3-137">A conta institucional será utilizada como administrador do gateway Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="69af3-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="69af3-138"><a name="register"></a>Registar</span><span class="sxs-lookup"><span data-stu-id="69af3-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="69af3-139">Na ordem toocreate um recurso de gateway no Azure, tem de registar a instância local Olá instalado com Olá serviço em nuvem Gateway.</span><span class="sxs-lookup"><span data-stu-id="69af3-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="69af3-140">Selecione **registar um novo gateway neste computador**.</span><span class="sxs-lookup"><span data-stu-id="69af3-140">Select **Register a new gateway on this computer**.</span></span>

    ![Registar](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="69af3-142">Escreva uma chave de recuperação e o nome do seu gateway.</span><span class="sxs-lookup"><span data-stu-id="69af3-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="69af3-143">Por predefinição, o gateway de Olá utiliza região de predefinida da sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="69af3-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="69af3-144">Se precisar de tooselect região diferente, selecione **alteração região**.</span><span class="sxs-lookup"><span data-stu-id="69af3-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![Registar](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="69af3-146"><a name="create-resource"></a>Crie um recurso de gateway do Azure</span><span class="sxs-lookup"><span data-stu-id="69af3-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="69af3-147">Depois de ter instalado e registado o gateway, terá de toocreate um recurso de gateway na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="69af3-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="69af3-148">A iniciar sessão tooAzure com Olá mesma conta que utilizou quando registar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="69af3-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="69af3-149">No portal do Azure, clique em **criar um novo serviço** > **integração empresarial com** > **gateway de dados no local**  >   **Criar**.</span><span class="sxs-lookup"><span data-stu-id="69af3-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Crie um recurso de gateway](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="69af3-151">No **criar gateway de ligação**, introduza estas definições:</span><span class="sxs-lookup"><span data-stu-id="69af3-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="69af3-152">**Nome**: introduza um nome para o recurso do gateway.</span><span class="sxs-lookup"><span data-stu-id="69af3-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="69af3-153">**Subscrição**: selecione Olá tooassociate de subscrição do Azure com o recurso do gateway.</span><span class="sxs-lookup"><span data-stu-id="69af3-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="69af3-154">Esta subscrição deve ser Olá mesma subscrição, os servidores fizerem no.</span><span class="sxs-lookup"><span data-stu-id="69af3-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="69af3-155">subscrição de predefinição Olá baseia Olá conta do Azure que utilizou toosign no.</span><span class="sxs-lookup"><span data-stu-id="69af3-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="69af3-156">**Grupo de recursos**: crie um grupo de recursos ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="69af3-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="69af3-157">**Localização**: região Olá selecione registado o seu gateway.</span><span class="sxs-lookup"><span data-stu-id="69af3-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="69af3-158">**Nome de instalação**: se a instalação do gateway não estiver selecionada, o gateway de Olá selecione registado.</span><span class="sxs-lookup"><span data-stu-id="69af3-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="69af3-159">Quando tiver terminado, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="69af3-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="69af3-160"><a name="connect-servers"></a>Ligue o recurso de gateway toohello de servidores</span><span class="sxs-lookup"><span data-stu-id="69af3-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="69af3-161">Na descrição geral da sua do Azure Analysis Services server, clique em **Gateway de dados no local**.</span><span class="sxs-lookup"><span data-stu-id="69af3-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Ligar o servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="69af3-163">No **escolher um Gateway de dados do On-Premises tooconnect**, selecione o recurso do gateway e, em seguida, clique em **gateway selecionado Connect**.</span><span class="sxs-lookup"><span data-stu-id="69af3-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Ligar recursos do servidor de toogateway](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="69af3-165">Se o gateway não aparecer na lista de Olá, o servidor não se encontra provável num Olá mesma região que região Olá que especificou quando registar o gateway de Olá.</span><span class="sxs-lookup"><span data-stu-id="69af3-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="69af3-166">E já está.</span><span class="sxs-lookup"><span data-stu-id="69af3-166">That's it.</span></span> <span data-ttu-id="69af3-167">Se precisar de portas de tooopen ou efetuar a qualquer resolução de problemas, ser toocheck se out [gateway de dados no local](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="69af3-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69af3-168">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="69af3-168">Next steps</span></span>
* [<span data-ttu-id="69af3-169">Gerir do Analysis Services</span><span class="sxs-lookup"><span data-stu-id="69af3-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="69af3-170">Obter dados a partir do Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="69af3-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
