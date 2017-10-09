---
title: "aaaConfigure um nome de domínio personalizado nos serviços em nuvem | Microsoft Docs"
description: "Saiba como tooexpose a aplicação do Azure ou dados de um domínio personalizado ao configurar as definições de DNS."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="ecf27-103">Configurar um nome de domínio personalizado para um serviço em nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="ecf27-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ecf27-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ecf27-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="ecf27-105">Portal Clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="ecf27-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="ecf27-106">Quando cria um serviço em nuvem, o Azure atribui-subdomínio tooa cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="ecf27-106">When you create a Cloud Service, Azure assigns it tooa subdomain of cloudapp.net.</span></span> <span data-ttu-id="ecf27-107">Por exemplo, se o seu serviço em nuvem com o nome "contoso", os utilizadores irão ser capaz de tooaccess a aplicação num URL como http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="ecf27-107">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="ecf27-108">Azure também atribui um endereço IP virtual.</span><span class="sxs-lookup"><span data-stu-id="ecf27-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="ecf27-109">No entanto, também pode expor a aplicação no seu próprio nome de domínio, tal como contoso.com. Este artigo explica como tooreserve ou configurar um nome de domínio personalizado para funções da web de serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ecf27-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="ecf27-110">Já compreender quais são CNAME e registos?</span><span class="sxs-lookup"><span data-stu-id="ecf27-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="ecf27-111">[Ir passado Olá explicação](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="ecf27-111">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="ecf27-112">Obter vai mais rapidamente!</span><span class="sxs-lookup"><span data-stu-id="ecf27-112">Get going faster!</span></span> <span data-ttu-id="ecf27-113">Olá de utilização do Azure [orientado instruções](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="ecf27-113">Use hello Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="ecf27-114">Faz a associação de um nome de domínio personalizado e proteger a comunicação (SSL) com Cloud Services do Azure ou Web sites do Azure com um snap.</span><span class="sxs-lookup"><span data-stu-id="ecf27-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="ecf27-115">procedimentos de Olá nesta tarefa aplicam-se os serviços de Cloud tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ecf27-115">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="ecf27-116">Para os serviços de aplicação, consulte [isto](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="ecf27-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="ecf27-117">Para contas do storage, consulte [isto](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="ecf27-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="ecf27-118">Compreender os registos CNAME e A</span><span class="sxs-lookup"><span data-stu-id="ecf27-118">Understand CNAME and A records</span></span>
<span data-ttu-id="ecf27-119">CNAME (ou os registos de alias) e registos ambos permitem-lhe tooassociate um nome de domínio com um servidor específico (ou serviço neste caso,) no entanto, funcionam de forma diferente.</span><span class="sxs-lookup"><span data-stu-id="ecf27-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="ecf27-120">Também existem algumas considerações específicas ao utilizar registos com os serviços de nuvem do Azure que deve considerar antes de decidir qual toouse.</span><span class="sxs-lookup"><span data-stu-id="ecf27-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="ecf27-121">Registo CNAME ou Alias</span><span class="sxs-lookup"><span data-stu-id="ecf27-121">CNAME or Alias record</span></span>
<span data-ttu-id="ecf27-122">Um registo CNAME mapeia um *específico* domínio, como **contoso.com** ou **www.contoso.com**, nome de domínio canónico tooa.</span><span class="sxs-lookup"><span data-stu-id="ecf27-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="ecf27-123">Neste caso, o nome de domínio canónico Olá é Olá **[myapp] .cloudapp .net** nome de domínio do seu Azure alojada a aplicação.</span><span class="sxs-lookup"><span data-stu-id="ecf27-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="ecf27-124">Depois de criado, Olá CNAME cria um alias para Olá **[myapp] .cloudapp .net**.</span><span class="sxs-lookup"><span data-stu-id="ecf27-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="ecf27-125">Olá entrada CNAME irá resolver o endereço IP toohello do seu **[myapp] .cloudapp .net** service automaticamente, se alterar o endereço IP Olá do serviço de nuvem Olá, não terá tootake qualquer ação.</span><span class="sxs-lookup"><span data-stu-id="ecf27-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="ecf27-126">Alguns registrars de domínio apenas lhe permitam toomap subdomínios quando utilizar um registo CNAME, como www.contoso.com e não os nomes de raiz, tal como contoso.com. Para obter mais informações sobre registos CNAME, consulte a documentação de Olá fornecida pela sua entidade de registo, [Olá Wikipedia entrada no registo CNAME](http://en.wikipedia.org/wiki/CNAME_record), ou Olá [IETF os nomes de domínio - implementação e a especificação de](http://tools.ietf.org/html/rfc1035) documento.</span><span class="sxs-lookup"><span data-stu-id="ecf27-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="ecf27-127">Um registo</span><span class="sxs-lookup"><span data-stu-id="ecf27-127">A record</span></span>
<span data-ttu-id="ecf27-128">Um registo mapeia um domínio, tal como **contoso.com** ou **www.contoso.com**, *ou de um domínio de caráter universal* como  **\*. contoso.com**, tooan endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ecf27-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="ecf27-129">No caso de Olá de um serviço em nuvem do Azure, Olá IP virtual do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecf27-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="ecf27-130">Por isso vantagem principal de Olá de um registo através de um registo CNAME é que pode fazer com que uma entrada que utiliza um caráter universal, tais como \* **. contoso.com**, que seria processar pedidos de subdomínios vários como  **Mail.contoso.com**, **login.contoso.com**, ou **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="ecf27-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="ecf27-131">Uma vez que está mapeado um registo tooa o endereço IP estático, não é possível resolver automaticamente alterações toohello endereço IP do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ecf27-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="ecf27-132">Olá atribuir endereço IP utilizado pelo seu serviço em nuvem é Olá pela primeira vez que implementar tooan ranhura vazia (produção ou transição.) Se eliminar a implementação de Olá para a ranhura de Olá, endereço IP de Olá é libertado pelo Azure e qualquer bloco de toohello implementações futuras pode ser atribuído um novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ecf27-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="ecf27-133">Comodamente, endereço IP Olá de uma ranhura de implementação fornecido (produção ou transição) é mantido ao trocar entre testes e implementações de produção ou efetuar uma atualização direta de uma implementação existente.</span><span class="sxs-lookup"><span data-stu-id="ecf27-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="ecf27-134">Para obter mais informações sobre estas ações a efetuar, consulte [como serviços em nuvem toomanage](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="ecf27-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="ecf27-135">Adicionar um registo CNAME para o domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ecf27-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="ecf27-136">toocreate um registo CNAME, tem de adicionar uma nova entrada na tabela DNS Olá para o seu domínio personalizado utilizando ferramentas de Olá fornecidas pelo sua entidade de registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="ecf27-137">Cada entidade de registo tem um método semelhante, mas ligeiramente diferente de especificação de um registo CNAME, mas Olá conceitos Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="ecf27-138">Utilize um dos Olá de toofind métodos **. cloudapp.net** atribuído tooyour o serviço em nuvem do nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="ecf27-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="ecf27-139">Início de sessão toohello [portal clássico do Azure], selecione o seu serviço em nuvem, selecione **Dashboard**e, em seguida, determinar Olá **URL do Site** entrada no Olá **leitura rápida**  secção.</span><span class="sxs-lookup"><span data-stu-id="ecf27-139">Login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Site URL** entry in hello **quick glance** section.</span></span>
     
       ![secção de leitura rápida, que mostra o URL do site Olá][csurl]
     
       <span data-ttu-id="ecf27-141">**OU**</span><span class="sxs-lookup"><span data-stu-id="ecf27-141">**OR**</span></span>  
   * <span data-ttu-id="ecf27-142">Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, utilize Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ecf27-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="ecf27-143">Guarde o nome de domínio de Olá utilizado no URL Olá devolvido por qualquer um dos métodos, como precisará ao criar um registo CNAME.</span><span class="sxs-lookup"><span data-stu-id="ecf27-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="ecf27-144">Inicie sessão no Web site de tooyour DNS da entidade de registo e aceda toohello página para gerir o DNS.</span><span class="sxs-lookup"><span data-stu-id="ecf27-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="ecf27-145">Procure ligações ou áreas do site de Olá identificados como **nome de domínio**, **DNS**, ou **nome do servidor de gestão**.</span><span class="sxs-lookup"><span data-stu-id="ecf27-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="ecf27-146">Localize agora onde pode selecionar ou introduzir do CNAME.</span><span class="sxs-lookup"><span data-stu-id="ecf27-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="ecf27-147">Pode ter o registo de Olá tooselect tipo de uma lista pendente, ou vá tooan avançadas a página de definições.</span><span class="sxs-lookup"><span data-stu-id="ecf27-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="ecf27-148">Deve procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.</span><span class="sxs-lookup"><span data-stu-id="ecf27-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="ecf27-149">Tem também de fornecer domínio Olá ou subdomínio alias para Olá CNAME, tais como **www** se quiser toocreate um alias para **www.customdomain.com**. Se quiser toocreate um alias para o domínio de raiz de Olá, podem ser apresentado como Olá '**@**' símbolo nas ferramentas DNS da sua entidade de registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="ecf27-150">Em seguida, tem de fornecer um nome de anfitrião canónico, que é a sua aplicação **cloudapp.net** domínio neste caso.</span><span class="sxs-lookup"><span data-stu-id="ecf27-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="ecf27-151">Por exemplo, Olá seguir registo CNAME reencaminha todo o tráfego de **www.contoso.com** demasiado**contoso.cloudapp.net**, nome de domínio personalizado de Olá da sua aplicação implementada:</span><span class="sxs-lookup"><span data-stu-id="ecf27-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="ecf27-152">Nome de alias/anfitrião/subdomínio</span><span class="sxs-lookup"><span data-stu-id="ecf27-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="ecf27-153">Domínio canónico</span><span class="sxs-lookup"><span data-stu-id="ecf27-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="ecf27-154">www</span><span class="sxs-lookup"><span data-stu-id="ecf27-154">www</span></span> |<span data-ttu-id="ecf27-155">contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="ecf27-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="ecf27-156">Visitantes de **www.contoso.com** nunca irá ver o anfitrião de verdadeiro Olá (contoso.cloudapp.net) pelo processo de reencaminhamento de Olá é toothe invisível final utilizador.</span><span class="sxs-lookup"><span data-stu-id="ecf27-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>

> [!NOTE]
> <span data-ttu-id="ecf27-157">Olá exemplo acima só se aplica tootraffic em Olá **www** subdomínio.</span><span class="sxs-lookup"><span data-stu-id="ecf27-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="ecf27-158">Uma vez que não é possível utilizar carateres universais com registos CNAME, tem de criar um CNAME para cada domínio/subdomínio.</span><span class="sxs-lookup"><span data-stu-id="ecf27-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="ecf27-159">Se pretender que o tráfego de toodirect de subdomínios, tais como \*. contoso.com, tooyour cloudapp.net endereço, pode configurar um **URL de redirecionamento** ou **URL reencaminhar** entrada nas suas definições de DNS, ou Crie um registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-159">If you want toodirect  traffic from subdomains, such as \*.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="ecf27-160">Adicionar um registo a para o domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ecf27-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="ecf27-161">toocreate um um registo, tem primeiro de encontrar Olá um endereço IP virtual do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ecf27-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="ecf27-162">Em seguida, adicione uma nova entrada na tabela DNS Olá para o seu domínio personalizado utilizando ferramentas de Olá fornecidas pelo sua entidade de registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="ecf27-163">Cada entidade de registo tem um método semelhante, mas ligeiramente diferente de especificação de um registo, mas Olá conceitos Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="ecf27-164">Utilize um dos Olá seguinte endereço IP do métodos tooget Olá do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ecf27-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="ecf27-165">início de sessão toohello [portal clássico do Azure], selecione o seu serviço em nuvem, selecione **Dashboard**e, em seguida, determinar Olá **endereço IP Virtual público (VIP)** entrada no Olá **leitura rápida** secção.</span><span class="sxs-lookup"><span data-stu-id="ecf27-165">login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Public Virtual IP (VIP) address** entry in hello **quick glance** section.</span></span>
     
       ![secção de leitura rápida Mostrar Olá VIP][vip]
     
       <span data-ttu-id="ecf27-167">**OU**</span><span class="sxs-lookup"><span data-stu-id="ecf27-167">**OR**</span></span>  
   * <span data-ttu-id="ecf27-168">Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, utilize Olá seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ecf27-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="ecf27-169">Se tiver vários pontos finais associados com o serviço de nuvem, receberá várias linhas que contém o endereço IP Olá, mas todas as devem apresentar Olá mesmo endereço.</span><span class="sxs-lookup"><span data-stu-id="ecf27-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing hello IP address, but all should display hello same address.</span></span>
     
     <span data-ttu-id="ecf27-170">Guarde o endereço IP Olá, pois irá precisar ao criar um registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-170">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="ecf27-171">Inicie sessão no Web site de tooyour DNS da entidade de registo e aceda toohello página para gerir o DNS.</span><span class="sxs-lookup"><span data-stu-id="ecf27-171">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="ecf27-172">Procure ligações ou áreas do site de Olá identificados como **nome de domínio**, **DNS**, ou **nome do servidor de gestão**.</span><span class="sxs-lookup"><span data-stu-id="ecf27-172">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="ecf27-173">Localize agora onde pode selecionar ou introduzir um registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="ecf27-174">Pode ter o registo de Olá tooselect tipo de uma lista pendente, ou vá tooan avançadas a página de definições.</span><span class="sxs-lookup"><span data-stu-id="ecf27-174">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="ecf27-175">Selecione ou introduza o domínio de Olá ou subdomínio que irá utilizar este registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-175">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="ecf27-176">Por exemplo, seleccione **www** se quiser toocreate um alias para **www.customdomain.com**. Se pretender toocreate uma entrada de caráter universal para todos os subdomínios, introduza '__*__'.</span><span class="sxs-lookup"><span data-stu-id="ecf27-176">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="ecf27-177">Este irá cobrir todos os subdomínios como **mail.customdomain.com**, **login.customdomain.com**, e **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="ecf27-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="ecf27-178">Se quiser toocreate um um registo para o domínio de raiz de Olá, podem ser apresentado como Olá '**@**' símbolo nas ferramentas DNS da sua entidade de registo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-178">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="ecf27-179">Introduza o endereço IP de Olá do seu serviço em nuvem no Olá fornecido campo.</span><span class="sxs-lookup"><span data-stu-id="ecf27-179">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="ecf27-180">Isto associa a entrada de domínio de Olá utilizada no Olá um registo com o endereço IP Olá da sua implementação do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ecf27-180">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="ecf27-181">Por exemplo, Olá seguir um registo reencaminha todo o tráfego de **contoso.com** demasiado**137.135.70.239**, Olá endereço IP da sua aplicação implementada:</span><span class="sxs-lookup"><span data-stu-id="ecf27-181">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="ecf27-182">Nome do anfitrião/subdomínio</span><span class="sxs-lookup"><span data-stu-id="ecf27-182">Host name/Subdomain</span></span> | <span data-ttu-id="ecf27-183">Endereço IP</span><span class="sxs-lookup"><span data-stu-id="ecf27-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="ecf27-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="ecf27-184">137.135.70.239</span></span> |

<span data-ttu-id="ecf27-185">O exemplo mostra como criar um registo para o domínio de raiz de Olá.</span><span class="sxs-lookup"><span data-stu-id="ecf27-185">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="ecf27-186">Se desejar toocreate um toocover de entrada universal todos os subdomínios, introduziria '__*__' como subdomínio Olá.</span><span class="sxs-lookup"><span data-stu-id="ecf27-186">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '__*__' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="ecf27-187">Endereços IP no Azure são dinâmicos por predefinição.</span><span class="sxs-lookup"><span data-stu-id="ecf27-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="ecf27-188">Provavelmente pretenderá toouse um [reservado de endereços IP](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure não alterar o seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ecf27-188">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ecf27-189">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ecf27-189">Next steps</span></span>
* [<span data-ttu-id="ecf27-190">Como tooManage Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ecf27-190">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="ecf27-191">Como tooMap conteúdo do CDN tooa domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="ecf27-191">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="ecf27-192">[Configuração geral do seu serviço de nuvem](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ecf27-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="ecf27-193">Saiba como demasiado[implementar um serviço em nuvem](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ecf27-193">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="ecf27-194">Configurar [certificados ssl](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="ecf27-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portal clássico do Azure]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
