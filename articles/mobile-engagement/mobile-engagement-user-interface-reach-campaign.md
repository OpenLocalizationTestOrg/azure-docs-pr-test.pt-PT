---
title: aaaAzure Interface de utilizador do Mobile Engagement - campanhas de alcance
description: "Laern como toocreate e gerir campanhas de notificações push utilizando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="93c0f-103">Como toocreate e gerir campanhas de notificações push</span><span class="sxs-lookup"><span data-stu-id="93c0f-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="93c0f-104">Pode utilizar Olá secção alcance Olá IU toocreate uma nova campanha Push com uma fórmula complexa, fornecendo todas as informações de Olá terá toosend uma notificação push.</span><span class="sxs-lookup"><span data-stu-id="93c0f-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="93c0f-105">Olá opções de uma campanha Push variam ligeiramente consoante os tipos de campanha Olá quatro: anúncios, inquéritos, Pushes de dados e os mosaicos (apenas Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="93c0f-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="93c0f-106">Opção aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="93c0f-106">Option Applies to:</span></span>
* <span data-ttu-id="93c0f-107">Idiomas: Todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="93c0f-108">Campanha: Todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="93c0f-109">Notificação: Anúncios, inquéritos</span><span class="sxs-lookup"><span data-stu-id="93c0f-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="93c0f-110">Conteúdo: Exclusivo para cada tipo de campanha</span><span class="sxs-lookup"><span data-stu-id="93c0f-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="93c0f-111">Audiência: Todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="93c0f-112">Período de tempo: mosaicos de anúncios, inquéritos,</span><span class="sxs-lookup"><span data-stu-id="93c0f-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="93c0f-113">Teste: Todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Campaign1 alcance][20]

## <a name="languages"></a><span data-ttu-id="93c0f-115">Linguagens</span><span class="sxs-lookup"><span data-stu-id="93c0f-115">Languages</span></span>
<span data-ttu-id="93c0f-116">Pode utilizar o menu de Olá pendente idiomas toosend uma versão diferente do seu toodevices de Push que são definidas toouse vários idiomas.</span><span class="sxs-lookup"><span data-stu-id="93c0f-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="93c0f-117">Por predefinição, todos os dispositivos irão receber Olá mesmo Push, independentemente da que idioma definidos toouse.</span><span class="sxs-lookup"><span data-stu-id="93c0f-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="93c0f-118">Os utilizadores com o idioma diferente do dispositivo conjunto tooa irão receber a versão de idioma predefinido de Olá de Olá Push.</span><span class="sxs-lookup"><span data-stu-id="93c0f-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="93c0f-119">Muitas das opções de campanha de push Olá permitem-lhe toospecify de conteúdo alternativo para cada um dos idiomas adicionais Olá que selecionar.</span><span class="sxs-lookup"><span data-stu-id="93c0f-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Campaign2 alcance][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="93c0f-121">Diferenças de idioma aplicam-se a:</span><span class="sxs-lookup"><span data-stu-id="93c0f-121">Language differences apply to:</span></span>
* <span data-ttu-id="93c0f-122">Idiomas: É possível selecionar idiomas exclusivos no idioma do adição toohello predefinido</span><span class="sxs-lookup"><span data-stu-id="93c0f-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="93c0f-123">Campanha: Mesmos para todos os idiomas</span><span class="sxs-lookup"><span data-stu-id="93c0f-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="93c0f-124">Notificação: Exclusivo para cada idioma Ademais toohello predefinido idioma</span><span class="sxs-lookup"><span data-stu-id="93c0f-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="93c0f-125">Conteúdo: Exclusivo para cada idioma Ademais toohello predefinido idioma</span><span class="sxs-lookup"><span data-stu-id="93c0f-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="93c0f-126">Audiência: Podem ser filtrados por um critério de idioma individual</span><span class="sxs-lookup"><span data-stu-id="93c0f-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="93c0f-127">Período de tempo: mesmo para todos os idiomas</span><span class="sxs-lookup"><span data-stu-id="93c0f-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="93c0f-128">Teste: Podem ser enviados tooeach idioma num momento</span><span class="sxs-lookup"><span data-stu-id="93c0f-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="93c0f-129">Idiomas suportados:</span><span class="sxs-lookup"><span data-stu-id="93c0f-129">Supported Languages:</span></span>
* <span data-ttu-id="93c0f-130">Árabe (ar)</span><span class="sxs-lookup"><span data-stu-id="93c0f-130">Arabic (ar)</span></span> 
* <span data-ttu-id="93c0f-131">Búlgaro (bg)</span><span class="sxs-lookup"><span data-stu-id="93c0f-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="93c0f-132">Catalan (AC)</span><span class="sxs-lookup"><span data-stu-id="93c0f-132">Catalan (ca)</span></span> 
* <span data-ttu-id="93c0f-133">Chinês (zh)</span><span class="sxs-lookup"><span data-stu-id="93c0f-133">Chinese (zh)</span></span> 
* <span data-ttu-id="93c0f-134">Croata (RH)</span><span class="sxs-lookup"><span data-stu-id="93c0f-134">Croatian (hr)</span></span> 
* <span data-ttu-id="93c0f-135">Czech (CS)</span><span class="sxs-lookup"><span data-stu-id="93c0f-135">Czech (cs)</span></span> 
* <span data-ttu-id="93c0f-136">Dinamarquês (da)</span><span class="sxs-lookup"><span data-stu-id="93c0f-136">Danish (da)</span></span> 
* <span data-ttu-id="93c0f-137">Neerlandês (nl)</span><span class="sxs-lookup"><span data-stu-id="93c0f-137">Dutch (nl)</span></span> 
* <span data-ttu-id="93c0f-138">Inglês (en)</span><span class="sxs-lookup"><span data-stu-id="93c0f-138">English (en)</span></span> 
* <span data-ttu-id="93c0f-139">Finlandês (fi)</span><span class="sxs-lookup"><span data-stu-id="93c0f-139">Finnish (fi)</span></span> 
* <span data-ttu-id="93c0f-140">Francês (fr)</span><span class="sxs-lookup"><span data-stu-id="93c0f-140">French (fr)</span></span> 
* <span data-ttu-id="93c0f-141">Alemão (de)</span><span class="sxs-lookup"><span data-stu-id="93c0f-141">German (de)</span></span> 
* <span data-ttu-id="93c0f-142">Grego (el)</span><span class="sxs-lookup"><span data-stu-id="93c0f-142">Greek (el)</span></span> 
* <span data-ttu-id="93c0f-143">Hebraico (ele)</span><span class="sxs-lookup"><span data-stu-id="93c0f-143">Hebrew (he)</span></span> 
* <span data-ttu-id="93c0f-144">Hindi (Olá)</span><span class="sxs-lookup"><span data-stu-id="93c0f-144">Hindi (hi)</span></span> 
* <span data-ttu-id="93c0f-145">Húngaro (hu)</span><span class="sxs-lookup"><span data-stu-id="93c0f-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="93c0f-146">Indonesian (id)</span><span class="sxs-lookup"><span data-stu-id="93c0f-146">Indonesian (id)</span></span> 
* <span data-ttu-id="93c0f-147">Italiano ()</span><span class="sxs-lookup"><span data-stu-id="93c0f-147">Italian (it)</span></span> 
* <span data-ttu-id="93c0f-148">Japonês (ja)</span><span class="sxs-lookup"><span data-stu-id="93c0f-148">Japanese (ja)</span></span> 
* <span data-ttu-id="93c0f-149">Coreano (ko)</span><span class="sxs-lookup"><span data-stu-id="93c0f-149">Korean (ko)</span></span> 
* <span data-ttu-id="93c0f-150">Letão (lv)</span><span class="sxs-lookup"><span data-stu-id="93c0f-150">Latvian (lv)</span></span> 
* <span data-ttu-id="93c0f-151">Lituano (lt)</span><span class="sxs-lookup"><span data-stu-id="93c0f-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="93c0f-152">Malaio (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="93c0f-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="93c0f-153">Norueguês Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="93c0f-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="93c0f-154">Polaco (LP)</span><span class="sxs-lookup"><span data-stu-id="93c0f-154">Polish (pl)</span></span> 
* <span data-ttu-id="93c0f-155">Português (pt)</span><span class="sxs-lookup"><span data-stu-id="93c0f-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="93c0f-156">Romeno (ro)</span><span class="sxs-lookup"><span data-stu-id="93c0f-156">Romanian (ro)</span></span> 
* <span data-ttu-id="93c0f-157">Russo (ru)</span><span class="sxs-lookup"><span data-stu-id="93c0f-157">Russian (ru)</span></span> 
* <span data-ttu-id="93c0f-158">Sérvio (sr)</span><span class="sxs-lookup"><span data-stu-id="93c0f-158">Serbian (sr)</span></span> 
* <span data-ttu-id="93c0f-159">Eslovaco (sk)</span><span class="sxs-lookup"><span data-stu-id="93c0f-159">Slovak (sk)</span></span> 
* <span data-ttu-id="93c0f-160">Esloveno (sl)</span><span class="sxs-lookup"><span data-stu-id="93c0f-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="93c0f-161">Espanhol (es)</span><span class="sxs-lookup"><span data-stu-id="93c0f-161">Spanish (es)</span></span> 
* <span data-ttu-id="93c0f-162">Sueco (sv)</span><span class="sxs-lookup"><span data-stu-id="93c0f-162">Swedish (sv)</span></span> 
* <span data-ttu-id="93c0f-163">Tagalog (tl)</span><span class="sxs-lookup"><span data-stu-id="93c0f-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="93c0f-164">Tailandês (ésimo)</span><span class="sxs-lookup"><span data-stu-id="93c0f-164">Thai (th)</span></span> 
* <span data-ttu-id="93c0f-165">Turco (seg)</span><span class="sxs-lookup"><span data-stu-id="93c0f-165">Turkish (tr)</span></span> 
* <span data-ttu-id="93c0f-166">Ucraniano (RU)</span><span class="sxs-lookup"><span data-stu-id="93c0f-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="93c0f-167">Vietnamita (vi)</span><span class="sxs-lookup"><span data-stu-id="93c0f-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="93c0f-168">Campanha</span><span class="sxs-lookup"><span data-stu-id="93c0f-168">Campaign</span></span>
<span data-ttu-id="93c0f-169">Pode utilizar o nome do Olá campanha secção tooset Olá e categoria da sua campanha, bem como se planear tooignore Olá público-alvo secção uma campanha de emissão e enviar esta campanha através de Olá API de alcance (e alguns elementos com o nível baixo de Olá Push API) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="93c0f-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="93c0f-170">Categorias podem ser utilizadas com uma notificação personalizada modelo toocontrol nas notificações na aplicação com base nas definições predefinidas.</span><span class="sxs-lookup"><span data-stu-id="93c0f-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="93c0f-171">Pode obter uma lista das suas existentes "categorias" através de Olá API de alcance.</span><span class="sxs-lookup"><span data-stu-id="93c0f-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="93c0f-172">Se utilizar a opção de "Ignorar audiência; push será enviado toousers através de Olá API" Olá na secção "Campanha" Olá uma campanha de alcance campanha Olá não enviará automaticamente, terá de toosend-lo manualmente através de Olá API de alcance.</span><span class="sxs-lookup"><span data-stu-id="93c0f-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Campaign3 alcance][22]

### <a name="option-applies-to"></a><span data-ttu-id="93c0f-174">Opção aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="93c0f-174">Option Applies to:</span></span>
* <span data-ttu-id="93c0f-175">Nome: todos os</span><span class="sxs-lookup"><span data-stu-id="93c0f-175">Name:    All</span></span>
* <span data-ttu-id="93c0f-176">Categoria: Anúncios, inquéritos</span><span class="sxs-lookup"><span data-stu-id="93c0f-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="93c0f-177">Ignorar audiência; push será enviado toousers através de Olá API: todos os</span><span class="sxs-lookup"><span data-stu-id="93c0f-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="93c0f-178">Notificação</span><span class="sxs-lookup"><span data-stu-id="93c0f-178">Notification</span></span>
<span data-ttu-id="93c0f-179">Pode utilizar Olá secção tooset básicas as definições de notificação para o push, incluindo: Olá título do Olá Push, mensagem de saudação, uma imagem de na aplicação, ou se for dispensáveis.</span><span class="sxs-lookup"><span data-stu-id="93c0f-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="93c0f-180">Muitas definições de notificação são toohello específicas de plataforma do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="93c0f-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="93c0f-181">Pode selecionar se o push será enviado "na aplicação" ou "fora da aplicação" ou ambos.</span><span class="sxs-lookup"><span data-stu-id="93c0f-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="93c0f-182">(Lembre-se de que os utilizadores podem "optar ativamente por participar" ou "ativamente" de "fora de aplicação" Pushes no sistema operativo de Olá nível nos respetivos dispositivos e Azure Mobile Engagement será não ser capaz de toooverride esta definição.</span><span class="sxs-lookup"><span data-stu-id="93c0f-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="93c0f-183">Lembre-se também de que processa a API de alcance Olá "na aplicação" e "fora da aplicação" Pushes.</span><span class="sxs-lookup"><span data-stu-id="93c0f-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="93c0f-184">Olá Push API pode ser utilizado toohandle "fora da aplicação" pushes demasiado.) Pushes podem ser personalizadas com imagens ou conteúdo HTML, incluindo ligações avançadas para ligar fora da sua aplicação ou tooanother na localização na sua aplicação (Android SDK 2.1.0 ou posteriores categorias intenção necessárias).</span><span class="sxs-lookup"><span data-stu-id="93c0f-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="93c0f-185">Pode alterar destaque de ícone ou iOS Olá e enviar o conteúdo web ou de texto (um pop-up com html, URL ligação tooanother localização de conteúdo dentro ou fora da aplicação Olá).</span><span class="sxs-lookup"><span data-stu-id="93c0f-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="93c0f-186">Também pode fazer com que os dispositivos Android toque ou Vibre com Olá Push.</span><span class="sxs-lookup"><span data-stu-id="93c0f-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="93c0f-187">(Lembre-se de que, será necessário Olá correto SDK as permissões no Android tooring do ficheiro de manifesto ou Vibre um dispositivo.) Não é atualmente nenhum setor padrão para tamanhos de Android "panorama geral", uma vez que os tamanhos de ecrã são diferentes em todos os dispositivos, mas as imagens de 400 x 100 funcionam em praticamente qualquer tamanho do ecrã.</span><span class="sxs-lookup"><span data-stu-id="93c0f-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="93c0f-188">Tipos de entrega:</span><span class="sxs-lookup"><span data-stu-id="93c0f-188">Delivery Types:</span></span>
* <span data-ttu-id="93c0f-189">Apenas fora da aplicação: notificação de Olá irá ser entregue ao utilizador Olá não utiliza a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="93c0f-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="93c0f-190">Olá fora de notificação de aplicação apenas requer um certificado da Apple ou da Google (certificado APNS ou GCM).</span><span class="sxs-lookup"><span data-stu-id="93c0f-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="93c0f-191">Na aplicação apenas: notificação de Olá é apresentada apenas quando a aplicação de Olá está em execução.</span><span class="sxs-lookup"><span data-stu-id="93c0f-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="93c0f-192">notificação de Olá utiliza utilizador do Olá Capptain entrega sistema tooreach Olá.</span><span class="sxs-lookup"><span data-stu-id="93c0f-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="93c0f-193">Pode personalizar totalmente esquema/apresentação visual para Olá do seu push.</span><span class="sxs-lookup"><span data-stu-id="93c0f-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="93c0f-194">Sempre: Esta opção assegura que, enviar uma notificação de que aplicação Olá está em execução ou não.</span><span class="sxs-lookup"><span data-stu-id="93c0f-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Campaign4 alcance][23]

### <a name="option-applies-to"></a><span data-ttu-id="93c0f-196">Opção aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="93c0f-196">Option Applies to:</span></span>
* <span data-ttu-id="93c0f-197">Notificação: Anúncios, inquéritos</span><span class="sxs-lookup"><span data-stu-id="93c0f-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="93c0f-198">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="93c0f-198">Content</span></span>
<span data-ttu-id="93c0f-199">Pode utilizar Olá secção de conteúdo toomodify Olá conteúdo os anúncios, inquéritos, Pushes de dados e os mosaicos (apenas Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="93c0f-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="93c0f-200">definição do conteúdo Olá das campanhas de Push é o tipo de toohello específico da campanha.</span><span class="sxs-lookup"><span data-stu-id="93c0f-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="93c0f-201">Consultar também</span><span class="sxs-lookup"><span data-stu-id="93c0f-201">See also</span></span>
* <span data-ttu-id="93c0f-202">[Documentação de IU - chegar - Push o conteúdo][Link 29]</span><span class="sxs-lookup"><span data-stu-id="93c0f-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Campaign5 alcance][24]

## <a name="audience"></a><span data-ttu-id="93c0f-204">Audiência</span><span class="sxs-lookup"><span data-stu-id="93c0f-204">Audience</span></span>
<span data-ttu-id="93c0f-205">Pode utilizar Olá público-alvo secção toodefine uma lista de itens toolimit padrão sua campanha ou os limites a sua campanha com base nos critérios personalizados.</span><span class="sxs-lookup"><span data-stu-id="93c0f-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="93c0f-206">conjunto de opções tooLimit padrão Olá seu público-alvo permite-lhe toopush tooeither novo ou antigo utilizadores ou apenas utilizadores de push nativo.</span><span class="sxs-lookup"><span data-stu-id="93c0f-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="93c0f-207">Também pode definir uma quota toolimit Olá diversas os utilizadores que recebem push Olá.</span><span class="sxs-lookup"><span data-stu-id="93c0f-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="93c0f-208">Pode editar manualmente expressão Olá como a sua campanha é filtrada tooinclude um ou mais utilizadores de tootarget critério.</span><span class="sxs-lookup"><span data-stu-id="93c0f-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="93c0f-209">Pode escrever manualmente uma expressão de audiência.</span><span class="sxs-lookup"><span data-stu-id="93c0f-209">You can manually type an audience expression.</span></span> <span data-ttu-id="93c0f-210">Uma expressão deste tipo tem de definir explicitamente relação Olá entre critérios.</span><span class="sxs-lookup"><span data-stu-id="93c0f-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="93c0f-211">Um critério é descrito por um identificador que tem de começar com uma letra em maiúsculas e não pode conter espaços.</span><span class="sxs-lookup"><span data-stu-id="93c0f-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="93c0f-212">relação de Olá entre os critérios de Olá pode ser descrita através de 'e', 'ou', 'not' operadores, bem como '(',')'.</span><span class="sxs-lookup"><span data-stu-id="93c0f-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="93c0f-213">Exemplo: "Criterion1 ou (Criterion1 e não Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="93c0f-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="93c0f-214">Com um grande público-alvo incluído no campanhas, lado do servidor de Olá filtragem análise pode ser lento, especialmente se tentar toostart Olá várias campanhas no mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="93c0f-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="93c0f-215">Se for possível, inicie uma campanha cada vez.</span><span class="sxs-lookup"><span data-stu-id="93c0f-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="93c0f-216">Ao hello mais, apenas início quatro campanhas de cada vez.</span><span class="sxs-lookup"><span data-stu-id="93c0f-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="93c0f-217">Push apenas tooyour utilizadores ativos (caixa de verificação "interagir apenas com utilizadores que podem ser contactados através de Push nativo" e "Interagir com apenas os utilizadores ativos") para que apenas os seus utilizadores que ainda tenham Olá aplicação instalada e utilização-lo terão toobe analisado.</span><span class="sxs-lookup"><span data-stu-id="93c0f-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="93c0f-218">Assim que o seu público-alvo estiver definida, pode utilizar Olá simular botão toofind saída quantos utilizadores irão receber este Push.</span><span class="sxs-lookup"><span data-stu-id="93c0f-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="93c0f-219">Isto irá de cálculo do número de Olá de utilizadores conhecidos potencialmente segmentados desta audiência (trata de uma estimativa baseada numa amostra aleatória de utilizadores).</span><span class="sxs-lookup"><span data-stu-id="93c0f-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="93c0f-220">Lembre-se de que os utilizadores que desinstalaram a aplicação Olá também fazem parte desta audiência, mas não não possível aceder.</span><span class="sxs-lookup"><span data-stu-id="93c0f-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="93c0f-221">Consultar também</span><span class="sxs-lookup"><span data-stu-id="93c0f-221">See also</span></span>
* <span data-ttu-id="93c0f-222">[IU documentação - alcance - novo critério de Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="93c0f-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Campaign6 alcance][25]

### <a name="edit-expression"></a><span data-ttu-id="93c0f-224">Editar expressão</span><span class="sxs-lookup"><span data-stu-id="93c0f-224">Edit expression</span></span>
![Campaign7 alcance][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="93c0f-226">Limite que a opção de audiência aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="93c0f-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="93c0f-227">Interagir apenas com um subconjunto de utilizadores: todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="93c0f-228">Interagir apenas com antigos utilizadores: todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="93c0f-229">Interagir apenas com novos utilizadores: todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="93c0f-230">Interagir apenas com Inativos utilizadores: os mosaicos de anúncios, inquéritos,</span><span class="sxs-lookup"><span data-stu-id="93c0f-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="93c0f-231">Interagir apenas com Active Directory utilizadores: todos os (anúncios, inquéritos, Pushes de dados, mosaicos)</span><span class="sxs-lookup"><span data-stu-id="93c0f-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="93c0f-232">Interagir apenas com utilizadores que possam ser contactados através de Push nativo: anúncios, inquéritos</span><span class="sxs-lookup"><span data-stu-id="93c0f-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="93c0f-233">Período de tempo</span><span class="sxs-lookup"><span data-stu-id="93c0f-233">Time Frame</span></span>
<span data-ttu-id="93c0f-234">Pode utilizar Olá período de tempo secção tooset quando Olá push será enviado ou pode deixar campanha de Olá Olá período de tempo em branco toostart imediatamente.</span><span class="sxs-lookup"><span data-stu-id="93c0f-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="93c0f-235">Lembre-se de que utilizar fuso horário Olá dos utilizadores finais pode começar campanha Olá por dia anterior de espera para os utilizadores finais na Ásia e enviar pequenos lotes de pushes cada vez até que todos os fusos horários diferentes no período de tempo do Olá mundo correspondência Olá definido para a sua campanha.</span><span class="sxs-lookup"><span data-stu-id="93c0f-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="93c0f-236">Utilizar fuso horário dos utilizadores finais Olá pode também provocar atrasos em campanhas porque tem toorequest Olá hora phone Olá antes de iniciar o push de Olá.</span><span class="sxs-lookup"><span data-stu-id="93c0f-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="93c0f-237">As campanhas sem uma data de fim pode colocar em cache pushes localmente e ainda as pode apresentar depois de concluir manualmente campanhas.</span><span class="sxs-lookup"><span data-stu-id="93c0f-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="93c0f-238">tooavoid este comportamento, específicos de uma hora de fim de campanhas.</span><span class="sxs-lookup"><span data-stu-id="93c0f-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="93c0f-239">Consultar também</span><span class="sxs-lookup"><span data-stu-id="93c0f-239">See also</span></span>
* <span data-ttu-id="93c0f-240">[Alcançar - como Tos – agendamento][Link 3]</span><span class="sxs-lookup"><span data-stu-id="93c0f-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Campaign8 alcance][27]

### <a name="settings-apply-to"></a><span data-ttu-id="93c0f-242">Aplicam as definições para:</span><span class="sxs-lookup"><span data-stu-id="93c0f-242">Settings Apply to:</span></span>
* <span data-ttu-id="93c0f-243">Período de tempo: mosaicos de anúncios, inquéritos,</span><span class="sxs-lookup"><span data-stu-id="93c0f-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="93c0f-244">Teste</span><span class="sxs-lookup"><span data-stu-id="93c0f-244">Test</span></span>
<span data-ttu-id="93c0f-245">Pode utilizar Olá teste secção toosend este dispositivo de teste própria tooyour push antes de guardar a campanha Olá.</span><span class="sxs-lookup"><span data-stu-id="93c0f-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="93c0f-246">Se tiver configurado qualquer idiomas personalizados para esta campanha, pode testar Olá push em cada idioma.</span><span class="sxs-lookup"><span data-stu-id="93c0f-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="93c0f-247">Pode configurar um dispositivo de teste de "A minha conta".</span><span class="sxs-lookup"><span data-stu-id="93c0f-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="93c0f-248">Pushes não do lado do servidor, os dados são registados quando utiliza o botão de Olá demasiado "teste", os dados são registados apenas para as campanhas real push.</span><span class="sxs-lookup"><span data-stu-id="93c0f-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="93c0f-249">Consultar também</span><span class="sxs-lookup"><span data-stu-id="93c0f-249">See also</span></span>
* <span data-ttu-id="93c0f-250">[Documentação de IU - minha conta][Link 14]</span><span class="sxs-lookup"><span data-stu-id="93c0f-250">[UI Documentation - My Account][Link 14]</span></span>

![Campaign9 alcance][28]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

