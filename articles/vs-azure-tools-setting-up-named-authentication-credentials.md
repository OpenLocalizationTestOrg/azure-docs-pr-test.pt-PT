---
title: "aaaSetting cópias de segurança denominado as credenciais de autenticação | Microsoft Docs"
description: "Saiba como o serviço em nuvem credenciais tootooprovide que o Visual Studio podem utilizar tooauthenticate pedidos tooAzure toopublish tooAzure uma aplicação do Visual Studio ou toomonitor existente... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="bae10-103">Configurar as credenciais de autenticação com o nome</span><span class="sxs-lookup"><span data-stu-id="bae10-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="bae10-104">toopublish tooAzure uma aplicação do Visual Studio ou toomonitor um serviço em nuvem existente, tem de fornecer credenciais que o Visual Studio podem utilizar tooauthenticate pedidos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bae10-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="bae10-105">Existem vários locais no Visual Studio, onde pode iniciar sessão tooprovide estas credenciais.</span><span class="sxs-lookup"><span data-stu-id="bae10-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="bae10-106">Por exemplo, de Olá Explorador de servidores, pode abrir o menu de atalho Olá para Olá **Azure** nós e escolher **ligar tooMicrosoft subscrição do Azure...** . Quando iniciar sessão, as informações de subscrição de Olá associadas à conta do Azure estão disponíveis no Visual Studio e tiver toodo mais nada.</span><span class="sxs-lookup"><span data-stu-id="bae10-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="bae10-107">Ferramentas do Azure também suporta uma forma mais antiga de fornecer credenciais, utilizando o ficheiro de subscrição de Olá (ficheiro. publishsettings).</span><span class="sxs-lookup"><span data-stu-id="bae10-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="bae10-108">Este tópico descreve este método, que ainda é suportado no Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="bae10-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="bae10-109">Olá seguintes itens é necessário para autenticação tooAzure:</span><span class="sxs-lookup"><span data-stu-id="bae10-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="bae10-110">O ID de subscrição</span><span class="sxs-lookup"><span data-stu-id="bae10-110">Your subscription ID</span></span>
* <span data-ttu-id="bae10-111">Um certificado válido de x. 509v3</span><span class="sxs-lookup"><span data-stu-id="bae10-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="bae10-112">o comprimento de chave do certificado x. 509 v3 de Olá Olá tem de ser, pelo menos, 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="bae10-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="bae10-113">Azure irá rejeitar qualquer certificado que não cumpram este requisito ou que não é válido.</span><span class="sxs-lookup"><span data-stu-id="bae10-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="bae10-114">Visual Studio utiliza o ID de subscrição, juntamente com dados de certificado Olá como credenciais.</span><span class="sxs-lookup"><span data-stu-id="bae10-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="bae10-115">as credenciais adequadas Olá são referenciadas no ficheiro de subscrição de Olá (ficheiro. publishsettings), que contém uma chave pública do certificado de Olá.</span><span class="sxs-lookup"><span data-stu-id="bae10-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="bae10-116">ficheiro de subscrição de Olá pode conter as credenciais para a mais do que uma subscrição.</span><span class="sxs-lookup"><span data-stu-id="bae10-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="bae10-117">Pode editar as informações de subscrição de Olá de Olá **New/editar subscrição** caixa de diálogo, conforme explicado posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="bae10-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="bae10-118">Se quiser toocreate um certificado por si, pode consultar toohello instruções [criar e carregar um certificado de gestão para o Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e, em seguida, carregar manualmente Olá certificado toohello [portal clássico do Azure ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="bae10-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="bae10-119">Estas credenciais que o Visual Studio requer toomanage que seus serviços em nuvem não são Olá mesmas credenciais que são necessária tooauthenticate um pedido de serviços do storage do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="bae10-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="bae10-120">Importar, definir ou editar credenciais de autenticação no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bae10-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="bae10-121">Pode importar, definir ou modificar as credenciais de autenticação no Olá **nova subscrição** caixa de diálogo, que é apresentada se efetuar Olá seguinte ação:</span><span class="sxs-lookup"><span data-stu-id="bae10-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="bae10-122">No **Explorador de servidores**, abra menu de atalho Olá para Olá **Azure** nós, escolha **gerir e subscrições de filtro...** , escolha Olá **certificados** separador e efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="bae10-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="bae10-123">Escolha **importar** onde pode transferir ficheiros de subscrições Olá para Olá atualmente tooopen caixa de diálogo de importar as subscrições do Microsoft Azure de Olá carregar a subscrição, procurar tooits localização da transferência e, em seguida, importá-lo para utilização no autenticação.</span><span class="sxs-lookup"><span data-stu-id="bae10-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="bae10-124">Escolha **novo** onde pode configurar uma nova subscrição para utilização na autenticação tooopen caixa de diálogo de nova subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="bae10-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="bae10-125">Escolha **editar** (depois de escolher a sua subscrição do Active Directory) onde pode editar uma subscrição existente para utilizar na autenticação tooopen caixa de diálogo de editar subscrição de Olá.</span><span class="sxs-lookup"><span data-stu-id="bae10-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="bae10-126">Olá procedimento assume que Olá **nova subscrição** caixa de diálogo está aberta.</span><span class="sxs-lookup"><span data-stu-id="bae10-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="bae10-127">tooset das credenciais de autenticação no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bae10-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="bae10-128">No Olá **selecionar um certificado existente** para lista de autenticação, selecione um certificado.</span><span class="sxs-lookup"><span data-stu-id="bae10-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="bae10-129">Escolha Olá **caminho completo do cópia Olá** ligação.</span><span class="sxs-lookup"><span data-stu-id="bae10-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="bae10-130">caminho de Olá certificado Olá (ficheiro. cer) é copiado toohello da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="bae10-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="bae10-131">toopublish a aplicação do Azure a partir do Visual Studio, tem de carregar este certificado toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bae10-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="bae10-132">tooupload Olá certificado toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="bae10-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="bae10-133">Abra Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="bae10-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="bae10-134">Se lhe for solicitado, inicie sessão no portal de toohello e, em seguida, navegue até demasiado**definições**, **certificados de gestão**.</span><span class="sxs-lookup"><span data-stu-id="bae10-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="bae10-135">No painel de certificados de gestão de Olá, escolha **carregar**.</span><span class="sxs-lookup"><span data-stu-id="bae10-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="bae10-136">Selecione a sua subscrição do Azure, cole o caminho completo do Olá do ficheiro. cer Olá que acabou de criar e escolha **carregar**.</span><span class="sxs-lookup"><span data-stu-id="bae10-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
