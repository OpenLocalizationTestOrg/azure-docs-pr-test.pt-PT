---
title: "aaaConfigure um nome de domínio personalizado para uma aplicação web no App Service do Azure utiliza o Gestor de tráfego para balanceamento de carga."
description: "Utilize um nome de domínio personalizado para um uma aplicação web no App Service do Azure inclui o Gestor de tráfego para o balanceamento de carga."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="e69c8-103">Configurar um nome de domínio personalizado para uma aplicação web no serviço de aplicações do Azure utilizando o Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="e69c8-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="e69c8-104">Este artigo fornece instruções genéricas para utilizar um nome de domínio personalizado com o App Service do Azure que utilizam o Gestor de tráfego para balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="e69c8-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="e69c8-105">Compreender os registos DNS</span><span class="sxs-lookup"><span data-stu-id="e69c8-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="e69c8-106">Configurar as suas aplicações web para o modo padrão</span><span class="sxs-lookup"><span data-stu-id="e69c8-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="e69c8-107">Adicionar um registo DNS para o domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="e69c8-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="e69c8-108">Se tiver adquirido domínio através da Web Apps do Azure App Service, em seguida, ignorar os passos seguintes e consulte toohello passo final da [comprar o domínio para aplicações Web](custom-dns-web-site-buydomains-web-app.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="e69c8-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="e69c8-109">tooassociate o domínio personalizado com uma aplicação web no App Service do Azure, tem de adicionar uma nova entrada na tabela DNS Olá para o domínio personalizado ao utilizar ferramentas fornecidas pelo Olá de domínios que comprou o nome de domínio do.</span><span class="sxs-lookup"><span data-stu-id="e69c8-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="e69c8-110">Utilize Olá toolocate passos a seguir e utilize as ferramentas DNS Olá.</span><span class="sxs-lookup"><span data-stu-id="e69c8-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="e69c8-111">Inicie sessão na conta tooyour na sua entidade de registo do domínio e procure uma página para gerir registos DNS.</span><span class="sxs-lookup"><span data-stu-id="e69c8-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="e69c8-112">Procure ligações ou áreas do site de Olá identificados como **nome de domínio**, **DNS**, ou **nome do servidor de gestão**.</span><span class="sxs-lookup"><span data-stu-id="e69c8-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="e69c8-113">Muitas vezes, uma ligação toothis página pode ser encontrada ser visualização de informações da sua conta e, em seguida, tais como a procura para uma ligação **meu domínios**.</span><span class="sxs-lookup"><span data-stu-id="e69c8-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="e69c8-114">Depois de encontrar página de gestão de Olá para o nome de domínio, procure uma ligação que lhe permite registos DNS de Olá tooedit.</span><span class="sxs-lookup"><span data-stu-id="e69c8-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="e69c8-115">Isto poderá estar listado como um **ficheiro de zona**, **registos DNS**, ou como um **avançadas** a ligação de configuração.</span><span class="sxs-lookup"><span data-stu-id="e69c8-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="e69c8-116">página Olá terá, provavelmente, alguns registos já criados, tais como uma associação de entrada '**@**'ou'\*' com uma página de 'parking domínio'.</span><span class="sxs-lookup"><span data-stu-id="e69c8-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="e69c8-117">Também poderá conter registos de subdomínios comuns, tais como **www**.</span><span class="sxs-lookup"><span data-stu-id="e69c8-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="e69c8-118">página Olá será mencionar **registos CNAME**, ou forneça um tooselect pendente um tipo de registo.</span><span class="sxs-lookup"><span data-stu-id="e69c8-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="e69c8-119">-Pode mencionar também outros registos como **registos** e **registos MX**.</span><span class="sxs-lookup"><span data-stu-id="e69c8-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="e69c8-120">Em alguns casos, registos CNAME serão chamados por outros nomes, tal como um **registo Alias**.</span><span class="sxs-lookup"><span data-stu-id="e69c8-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="e69c8-121">página Olá também irá ter campos que lhe permitem demasiado**mapa** de um **nome de anfitrião** ou **nome de domínio** tooanother nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="e69c8-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="e69c8-122">Enquanto variam especificações Olá cada entidade de registo, no geral mapear *de* o nome de domínio personalizado (tais como **contoso.com**,) *para* nome de domínio do Traffic Manager Olá (**contoso.trafficmanager.net**) que é utilizado para a sua aplicação web.</span><span class="sxs-lookup"><span data-stu-id="e69c8-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e69c8-123">Em alternativa, se um registo já está em utilização e precisar de toopreemptively vincular o tooit de aplicações, pode criar um registo CNAME adicional.</span><span class="sxs-lookup"><span data-stu-id="e69c8-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="e69c8-124">Por exemplo, toopreemptively enlace **www.contoso.com** tooyour web app, crie um registo CNAME de **awverify.www** demasiado**contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="e69c8-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="e69c8-125">Em seguida, pode adicionar tooyour "www.contoso.com" aplicação Web sem alterar o registo CNAME Olá "www".</span><span class="sxs-lookup"><span data-stu-id="e69c8-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="e69c8-126">Para obter mais informações, consulte [registos DNS criar para uma aplicação web no domínio personalizado de][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="e69c8-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="e69c8-127">Quando terminar de adicionar ou modificar registos DNS na sua entidade de registo, guarde as alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="e69c8-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="e69c8-128">Ativar o Gestor de tráfego</span><span class="sxs-lookup"><span data-stu-id="e69c8-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="e69c8-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e69c8-129">Next steps</span></span>
<span data-ttu-id="e69c8-130">Para obter mais informações, consulte Olá [Centro para programadores do Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="e69c8-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
