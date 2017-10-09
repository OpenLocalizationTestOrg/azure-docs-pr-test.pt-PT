---
title: "aaaSet segurança ambientes para web apps no App Service do Azure de teste | Microsoft Docs"
description: "Saiba como toouse testado publicação para web apps no App Service do Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="96bb5-103">Configurar ambientes no App Service do Azure de teste</span><span class="sxs-lookup"><span data-stu-id="96bb5-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="96bb5-104">Ao implementar a aplicação web, a aplicação web no Linux, back-end móvel e API Apps demasiado[do serviço de aplicações](http://go.microsoft.com/fwlink/?LinkId=529714), pode implementar o bloco de implementação separado de tooa em vez de ranhura de produção Olá predefinido quando em execução no Olá **padrão**ou **Premium** modo de plano de serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="96bb5-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="96bb5-105">As ranhuras de implementação são aplicações realmente em direto com os seus próprios nomes de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="96bb5-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="96bb5-106">Elementos de conteúdo e as configurações de aplicação podem ser trocados entre duas ranhuras de implementação, incluindo a ranhura de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="96bb5-107">Implementar a ranhura de implementação da aplicação tooa tem Olá seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="96bb5-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="96bb5-108">Pode validar alterações de aplicações numa ranhura de implementação de teste antes de troca de ranhura de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="96bb5-109">Implementar uma tooa a ranhura de aplicação pela primeira vez e trocar-o em produção assegura que todas as instâncias de ranhura Olá são preparadas antes de a ser alternados em produção.</span><span class="sxs-lookup"><span data-stu-id="96bb5-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="96bb5-110">Isto elimina o período de indisponibilidade quando implementar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="96bb5-111">redirecionamento de tráfego de Olá é totalmente integrado e não existem pedidos são ignorados devido a operações de comutação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="96bb5-112">Este fluxo de trabalho completo pode ser automatizado configurando [automática comutação](#Auto-Swap) quando a validação de pré-troca de não é necessária.</span><span class="sxs-lookup"><span data-stu-id="96bb5-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="96bb5-113">Depois de uma troca ranhura Olá com a aplicação anteriormente faseada tem agora Olá anterior aplicação de produção.</span><span class="sxs-lookup"><span data-stu-id="96bb5-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="96bb5-114">Se as alterações de Olá alternadas na ranhura de produção Olá não tem o aspeto esperado, pode realizar Olá que mesmo comutação imediatamente fazer uma cópia de tooget do "última conhecido boa o site".</span><span class="sxs-lookup"><span data-stu-id="96bb5-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="96bb5-115">Cada modo de plano de serviço de aplicações suporta um número diferente de ranhuras de implementação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="96bb5-116">suporta o modo da sua aplicação toofind limite o número de Olá de ranhuras, consulte [preços do App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="96bb5-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="96bb5-117">Quando a aplicação tiver várias ranhuras, não é possível alterar o modo de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="96bb5-118">Dimensionamento não está disponível para ranhuras de não produção.</span><span class="sxs-lookup"><span data-stu-id="96bb5-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="96bb5-119">Gestão de recursos ligado não é suportada para as ranhuras de não produção.</span><span class="sxs-lookup"><span data-stu-id="96bb5-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="96bb5-120">No Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) apenas, pode evitar esta potencial impacto na ranhura de produção, movendo temporariamente Olá ranhura de produção não tooa diferente do serviço de aplicações plano modo.</span><span class="sxs-lookup"><span data-stu-id="96bb5-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="96bb5-121">Tenha em atenção que ranhura de produção não Olá novamente têm de partilhar Olá mesmo modo ranhura de produção Olá antes de pode trocar ranhuras de Olá dois.</span><span class="sxs-lookup"><span data-stu-id="96bb5-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="96bb5-122">Adicionar uma ranhura de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-122">Add a deployment slot</span></span>
<span data-ttu-id="96bb5-123">aplicação Olá deve estar em execução Olá **padrão** ou **Premium** modo na ordem para tooenable várias ranhuras de implementação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="96bb5-124">No Olá [Portal do Azure](https://portal.azure.com/), abra a aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="96bb5-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="96bb5-125">Escolha Olá **ranhuras de implementação** opção, em seguida, clique em **adicionar ranhura**.</span><span class="sxs-lookup"><span data-stu-id="96bb5-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Adicionar uma nova ranhura de implementação][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="96bb5-127">Se a aplicação Olá já está a não ser Olá **padrão** ou **Premium** modo, receberá uma mensagem a indicar os modos de Olá suportado para ativar a publicação de teste.</span><span class="sxs-lookup"><span data-stu-id="96bb5-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="96bb5-128">Neste momento, tiver Olá opção tooselect **atualizar** e navegue toohello **escala** separador da sua aplicação antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="96bb5-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="96bb5-129">No Olá **adicionar uma ranhura** painel, dê um nome de ranhura Olá e selecionar se tooclone configuração de aplicação a partir de outro bloco de implementação existente.</span><span class="sxs-lookup"><span data-stu-id="96bb5-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="96bb5-130">Clique em Olá toocontinue de marca de verificação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-130">Click hello check mark toocontinue.</span></span>
   
    ![Origem de configuração][ConfigurationSource1]
   
    <span data-ttu-id="96bb5-132">Olá pela primeira vez, adicionar uma ranhura, apenas terá duas opções: configuração de clone a partir da ranhura de predefinição Olá na produção ou não de todo.</span><span class="sxs-lookup"><span data-stu-id="96bb5-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="96bb5-133">Depois de criar várias ranhuras, será tooclone capaz de configuração a partir de uma ranhura diferente Olá um na produção:</span><span class="sxs-lookup"><span data-stu-id="96bb5-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Origens de configuração][MultipleConfigurationSources]
4. <span data-ttu-id="96bb5-135">No painel de recursos da sua aplicação, clique em **ranhuras de implementação**, em seguida, clique uma tooopen da ranhura de implementação do painel de recursos nesse bloco, com um conjunto de métricas e a configuração, tal como qualquer outra aplicação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="96bb5-136">Olá nome de ranhura Olá é mostrado na parte superior de Olá de Olá painel tooremind Olá que está a visualizar a ranhura de implementação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Título da ranhura de implementação][StagingTitle]
5. <span data-ttu-id="96bb5-138">Clique em URL da aplicação Olá no painel de ranhura Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="96bb5-139">Tenha em atenção a ranhura de implementação de Olá tem o seu próprio nome de anfitrião e também é uma aplicação em direto.</span><span class="sxs-lookup"><span data-stu-id="96bb5-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="96bb5-140">toolimit acesso público toohello ranhura de implementação, consulte [aplicação Web do App Service – ranhuras de implementação de produção toonon de acesso web bloco](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="96bb5-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="96bb5-141">Não há nenhum conteúdo após a criação da ranhura de implementação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="96bb5-142">Pode implementar toohello ranhura de um ramo do repositório diferente ou um repositório completamente diferente.</span><span class="sxs-lookup"><span data-stu-id="96bb5-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="96bb5-143">Também pode alterar a configuração da ranhura de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="96bb5-144">Olá utilize publicar ou implementação de perfil de credenciais associadas ao bloco de implementação de Olá para as atualizações de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="96bb5-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="96bb5-145">Por exemplo, pode [publicar toothis ranhura com o git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="96bb5-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="96bb5-146">Configuração para as ranhuras de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-146">Configuration for deployment slots</span></span>
<span data-ttu-id="96bb5-147">Ao clonar a configuração a partir de outro bloco de implementação, a configuração clonado Olá é editável.</span><span class="sxs-lookup"><span data-stu-id="96bb5-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="96bb5-148">Além disso, alguns elementos de configuração segue conteúdo Olá através de uma troca (não ranhura específica) enquanto outros elementos de configuração permanecerão no Olá mesmo espaço depois de uma troca (específica da ranhura).</span><span class="sxs-lookup"><span data-stu-id="96bb5-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="96bb5-149">Olá listas seguintes mostram configuração Olá que será alterado quando trocar ranhuras.</span><span class="sxs-lookup"><span data-stu-id="96bb5-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="96bb5-150">**As definições que são trocadas**:</span><span class="sxs-lookup"><span data-stu-id="96bb5-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="96bb5-151">Sockets de Web de definições gerais - por exemplo, a versão do framework, 32/64 bits,</span><span class="sxs-lookup"><span data-stu-id="96bb5-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="96bb5-152">Definições de aplicação (pode ser configurado toostick tooa ranhura)</span><span class="sxs-lookup"><span data-stu-id="96bb5-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="96bb5-153">Cadeias de ligação (pode ser configurado toostick tooa ranhura)</span><span class="sxs-lookup"><span data-stu-id="96bb5-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="96bb5-154">Mapeamentos do processador</span><span class="sxs-lookup"><span data-stu-id="96bb5-154">Handler mappings</span></span>
* <span data-ttu-id="96bb5-155">Definições de monitorização e diagnóstico</span><span class="sxs-lookup"><span data-stu-id="96bb5-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="96bb5-156">Conteúdo de WebJobs</span><span class="sxs-lookup"><span data-stu-id="96bb5-156">WebJobs content</span></span>

<span data-ttu-id="96bb5-157">**As definições que não estão a ser alternadas**:</span><span class="sxs-lookup"><span data-stu-id="96bb5-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="96bb5-158">Pontos finais de publicação</span><span class="sxs-lookup"><span data-stu-id="96bb5-158">Publishing endpoints</span></span>
* <span data-ttu-id="96bb5-159">Nomes de domínio personalizados</span><span class="sxs-lookup"><span data-stu-id="96bb5-159">Custom Domain Names</span></span>
* <span data-ttu-id="96bb5-160">Certificados SSL e os enlaces</span><span class="sxs-lookup"><span data-stu-id="96bb5-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="96bb5-161">Definições de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="96bb5-161">Scale settings</span></span>
* <span data-ttu-id="96bb5-162">Programadores de WebJobs</span><span class="sxs-lookup"><span data-stu-id="96bb5-162">WebJobs schedulers</span></span>

<span data-ttu-id="96bb5-163">tooconfigure uma definição ou ligação cadeia toostick tooa ranhura de aplicação (não alternada) Olá acesso **definições da aplicação** painel para uma ranhura específica, em seguida, selecione Olá **ranhura definição** caixa Olá elementos de configuração que devem stick ranhura Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="96bb5-164">Tenha em atenção que um elemento de configuração marcar como ranhura específica tem efeito Olá estabelecer que o elemento não swappable como em todas as ranhuras de implementação de Olá associadas Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Definições de ranhura][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="96bb5-166">Trocar ranhuras de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-166">Swap deployment slots</span></span> 
<span data-ttu-id="96bb5-167">Pode trocar ranhuras de implementação no Olá **descrição geral** ou **ranhuras de implementação** vista do painel de recursos da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96bb5-168">Antes de trocar uma aplicação de uma ranhura de implementação em produção, certifique-se de que todas as definições específicas do bloco não estão configuradas exatamente como pretende que toohave-lo na Olá troca de destino.</span><span class="sxs-lookup"><span data-stu-id="96bb5-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="96bb5-169">tooswap ranhuras de implementação, clique em Olá **comutação** botão na barra de comando Olá da aplicação Olá ou na barra de comando Olá de uma ranhura de implementação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Botão de comutação][SwapButtonBar]

2. <span data-ttu-id="96bb5-171">Certifique-se de que Olá troca troca de origem e o destino estão definidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="96bb5-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="96bb5-172">Normalmente, o destino de troca de Olá é ranhura de produção Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="96bb5-173">Clique em **OK** operação de Olá toocomplete.</span><span class="sxs-lookup"><span data-stu-id="96bb5-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="96bb5-174">Quando concluída a operação de Olá, ranhuras de implementação de Olá tem sido alternadas.</span><span class="sxs-lookup"><span data-stu-id="96bb5-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Concluir troca](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="96bb5-176">Para Olá **troca com pré-visualização** comutação tipo, consulte [troca com pré-visualização (fase multi swap)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="96bb5-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="96bb5-177">Troca com pré-visualização (fase multi swap)</span><span class="sxs-lookup"><span data-stu-id="96bb5-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="96bb5-178">Troca com pré-visualização ou fase multi troca, simplificar a validação de elementos de configuração específicos da ranhura, tais como cadeias de ligação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="96bb5-179">Para cargas de trabalho pesadas, pretende toovalidate Olá aplicação se comporta conforme esperado quando a configuração da ranhura de produção Olá é aplicada, e tem de executar essa validação *antes* aplicação Olá é alternada em produção.</span><span class="sxs-lookup"><span data-stu-id="96bb5-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="96bb5-180">Troca com pré-visualização é o que precisa.</span><span class="sxs-lookup"><span data-stu-id="96bb5-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="96bb5-181">Troca com pré-visualização não é suportada nas web apps no Linux.</span><span class="sxs-lookup"><span data-stu-id="96bb5-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="96bb5-182">Quando utiliza Olá **troca com pré-visualização** opção (consulte [trocar ranhuras de implementação](#Swap)), serviço de aplicações Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="96bb5-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="96bb5-183">Não é afetada mantém Olá destino ranhura inalterada existente, por isso, carga de trabalho em que ranhura (por exemplo, produção).</span><span class="sxs-lookup"><span data-stu-id="96bb5-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="96bb5-184">Aplica os elementos de configuração de Olá de Olá destino ranhura toohello ranhura de origem, incluindo cadeias de ligação de específicos da ranhura de Olá e as definições de aplicação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="96bb5-185">Reinicia os processos de trabalho de Olá na ranhura de origem Olá utilizando estes elementos de configuração acima mencionados.</span><span class="sxs-lookup"><span data-stu-id="96bb5-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="96bb5-186">Quando concluir troca Olá: move ranhura de origem de pré-warmed cópia de segurança Olá na ranhura de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="96bb5-187">ranhura de destino Olá é movida para a ranhura de origem Olá como uma troca manual.</span><span class="sxs-lookup"><span data-stu-id="96bb5-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="96bb5-188">Se cancelar a troca de Olá: volta elementos de configuração de Olá da ranhura de origem do Olá origem ranhura toohello.</span><span class="sxs-lookup"><span data-stu-id="96bb5-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="96bb5-189">Pode pré-visualizar exatamente como aplicação Olá irão comportar-se com a configuração da ranhura de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="96bb5-190">Depois de concluir a validação, concluir troca Olá num passo separado.</span><span class="sxs-lookup"><span data-stu-id="96bb5-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="96bb5-191">Este passo tem Olá adicionada vantagem de ranhura de origem de Olá já está preparada com configuração pretendida Olá e, os clientes não irão experimentar qualquer período de inatividade.</span><span class="sxs-lookup"><span data-stu-id="96bb5-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="96bb5-192">Exemplos de Olá cmdlets Azure PowerShell disponíveis para comutação fase multi estão incluídos no Olá cmdlets Azure PowerShell para a secção de ranhuras de implementação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="96bb5-193">Configurar a troca automática</span><span class="sxs-lookup"><span data-stu-id="96bb5-193">Configure Auto Swap</span></span>
<span data-ttu-id="96bb5-194">Simplifica a troca automática cenários de DevOps onde pretende toocontinuously implementa a sua aplicação com zero frio e períodos de indisponibilidade para os clientes de fim da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="96bb5-195">Quando uma ranhura de implementação está configurada para a troca automática em produção, sempre que enviar a ranhura de toothat de atualização de código, o serviço de aplicações será automaticamente a comutação aplicação Olá em produção, depois de já ter preparada na ranhura de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96bb5-196">Quando ativa a comutação automática para uma ranhura, certifique-se a configuração da ranhura Olá exatamente configuração de Olá que se destina a ranhura de destino Olá (normalmente, ranhura de produção Olá).</span><span class="sxs-lookup"><span data-stu-id="96bb5-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="96bb5-197">Troca automática não é suportada nas web apps no Linux.</span><span class="sxs-lookup"><span data-stu-id="96bb5-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="96bb5-198">É fácil a configuração automática de comutação para uma ranhura.</span><span class="sxs-lookup"><span data-stu-id="96bb5-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="96bb5-199">Siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="96bb5-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="96bb5-200">No **ranhuras de implementação**, selecione uma ranhura de não produção e escolha **definições da aplicação** no painel de recursos que ranhura.</span><span class="sxs-lookup"><span data-stu-id="96bb5-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="96bb5-201">Selecione **no** para **automática comutação**, selecione ranhura de destino pretendido de Olá no **automática trocar a ranhura**e clique em **guardar** na barra de comando Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="96bb5-202">Certifique-se a configuração para a ranhura de Olá exatamente configuração de Olá que se destina a ranhura de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="96bb5-203">Olá **notificações** separador irá flash um verde **êxito** após a conclusão da operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="96bb5-204">tootest comutação automática para a sua aplicação, primeiro pode selecionar uma ranhura de destino de não produção no **automática trocar a ranhura** toobecome familiarizado com a funcionalidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="96bb5-205">Execute uma ranhura de implementação de toothat de push de código.</span><span class="sxs-lookup"><span data-stu-id="96bb5-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="96bb5-206">Troca automática irá ocorrer após um curto período de tempo e atualização Olá será apresentada no URL da ranhura de destino.</span><span class="sxs-lookup"><span data-stu-id="96bb5-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="96bb5-207">toorollback uma aplicação de produção após a troca</span><span class="sxs-lookup"><span data-stu-id="96bb5-207">toorollback a production app after swap</span></span>
<span data-ttu-id="96bb5-208">Se os erros são identificados em produção após uma troca de ranhura, reversão ranhuras Olá tootheir back-Estados de pré-comutação de ao trocar ranhuras de Olá dois mesmo imediatamente.</span><span class="sxs-lookup"><span data-stu-id="96bb5-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="96bb5-209">Warm-up personalizado antes de comutação</span><span class="sxs-lookup"><span data-stu-id="96bb5-209">Custom warm-up before swap</span></span>
<span data-ttu-id="96bb5-210">Algumas aplicações podem exigir ações warm-up personalizado.</span><span class="sxs-lookup"><span data-stu-id="96bb5-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="96bb5-211">Olá `applicationInitialization` elemento de configuração em Web. config permite-lhe toospecify inicialização personalizada ações toobe efetuada antes de que é recebido um pedido.</span><span class="sxs-lookup"><span data-stu-id="96bb5-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="96bb5-212">operação de troca de Olá espera que este toocomplete warm-up personalizado.</span><span class="sxs-lookup"><span data-stu-id="96bb5-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="96bb5-213">Eis um fragmento de Web. config de exemplo.</span><span class="sxs-lookup"><span data-stu-id="96bb5-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="96bb5-214">toodelete uma ranhura de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-214">toodelete a deployment slot</span></span>
<span data-ttu-id="96bb5-215">No painel de Olá para uma ranhura de implementação, o painel da ranhura de implementação Olá aberto, clique em **descrição geral** (página predefinida de Olá) e clique em **eliminar** na barra de comando Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Eliminar uma ranhura de implementação][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="96bb5-217">Cmdlets do PowerShell do Azure para as ranhuras de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="96bb5-218">O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell, incluindo suporte para gerir as ranhuras de implementação no App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="96bb5-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="96bb5-219">Para obter informações sobre como instalar e configurar o Azure PowerShell e sobre a autenticação do Azure PowerShell com a sua subscrição do Azure, consulte [como tooinstall e configurar o Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96bb5-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="96bb5-220">Criar uma aplicação Web</span><span class="sxs-lookup"><span data-stu-id="96bb5-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="96bb5-221">Criar uma ranhura de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="96bb5-222">Inicie uma troca com a revisão (fase multi swap) e aplicar a ranhura de toosource da configuração de ranhura de destino</span><span class="sxs-lookup"><span data-stu-id="96bb5-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="96bb5-223">Cancelar uma troca pendente (troca com a revisão) e restaurar a configuração da ranhura de origem</span><span class="sxs-lookup"><span data-stu-id="96bb5-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="96bb5-224">Trocar ranhuras de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="96bb5-225">Elimine o bloco de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="96bb5-226">Comandos de Interface de linha de comandos (CLI do Azure) do Azure para as ranhuras de implementação</span><span class="sxs-lookup"><span data-stu-id="96bb5-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="96bb5-227">Olá CLI do Azure fornece comandos de várias plataformas para trabalhar com o Azure, incluindo suporte para gerir as ranhuras de implementação do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="96bb5-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="96bb5-228">Para obter instruções sobre como instalar e configurar hello CLI do Azure, incluindo informações sobre como tooconnect CLI do Azure tooyour subscrição do Azure, consulte [instalar e configurar a CLI do Azure de Olá](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="96bb5-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="96bb5-229">chamar toolist Olá os comandos disponíveis para o App Service do Azure no Olá CLI do Azure, `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="96bb5-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="96bb5-230">Para [Azure CLI 2.0](https://github.com/Azure/azure-cli) comandos para as ranhuras de implementação, consulte [ranhura de implementação do az appservice web](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="96bb5-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="96bb5-231">lista de sites do Azure</span><span class="sxs-lookup"><span data-stu-id="96bb5-231">azure site list</span></span>
<span data-ttu-id="96bb5-232">Para obter informações sobre as aplicações de Olá na subscrição atual Olá, chamar **a lista de sites do azure**, como no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="96bb5-233">criar o site do Azure</span><span class="sxs-lookup"><span data-stu-id="96bb5-233">azure site create</span></span>
<span data-ttu-id="96bb5-234">chamar toocreate uma ranhura de implementação, **do azure site criar** e especifique o nome de Olá de uma aplicação existente e nome de Olá da toocreate de ranhura Olá, como no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="96bb5-235">controlo de origem tooenable para Olá nova ranhura, utilize Olá **– git** opção, como no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="96bb5-236">troca de site do Azure</span><span class="sxs-lookup"><span data-stu-id="96bb5-236">azure site swap</span></span>
<span data-ttu-id="96bb5-237">toomake Olá ranhura de implementação atualizada Olá aplicação de produção, utilize Olá **troca de site do azure** comando tooperform uma operação de troca, como no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="96bb5-238">aplicação de produção Olá não irá ocorrer algum tempo, nem vai sofrer-uma arranque a frio.</span><span class="sxs-lookup"><span data-stu-id="96bb5-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="96bb5-239">eliminação de site do Azure</span><span class="sxs-lookup"><span data-stu-id="96bb5-239">azure site delete</span></span>
<span data-ttu-id="96bb5-240">toodelete uma ranhura de implementação que já não é necessário, utilize Olá **eliminação de site do azure** comando, como no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="96bb5-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="96bb5-241">Veja uma aplicação Web em ação.</span><span class="sxs-lookup"><span data-stu-id="96bb5-241">See a web app in action.</span></span> <span data-ttu-id="96bb5-242">[Experimentar o App Service](https://azure.microsoft.com/try/app-service/) imediatamente e crie uma aplicação de arranque de curta duração — sem cartões de crédito, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="96bb5-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="96bb5-243">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="96bb5-243">Next Steps</span></span>
<span data-ttu-id="96bb5-244">[Web do App Service do Azure aplicação – bloquear ranhuras de implementação de produção toonon de acesso web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[introdução tooApp serviço no Linux](./app-service-linux-intro.md)
[avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="96bb5-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

