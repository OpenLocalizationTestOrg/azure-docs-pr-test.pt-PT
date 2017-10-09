---
title: aaaOptions para migrar no Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre as opções de Olá para migrar no Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="86786-103">Opções de migração no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="86786-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="86786-104">O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="86786-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="86786-105">Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="86786-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="86786-106">Se tiver parado a utilizar o Azure RemoteApp devido a Olá [anúncio de extinção](https://go.microsoft.com/fwlink/?linkid=821148) ou uma vez que terminar a avaliação, tem de toomigrate termina sessão do serviço de aplicações do Azure RemoteApp tooanother.</span><span class="sxs-lookup"><span data-stu-id="86786-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="86786-107">Existem duas abordagens diferentes para a migração: um autogerida (frequentemente designado por infraestrutura como serviço [IaaS]) implementação ou uma plataforma completamente gerida (frequentemente denominada como um serviço) ou de Software como serviço [PaaS/SaaS] oferta.</span><span class="sxs-lookup"><span data-stu-id="86786-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="86786-108">Self-service IaaS é uma implementação do-it-yourself que é gerida, operada e detida por si, diretamente implementados em máquinas virtuais (VMs) ou de sistemas físicos.</span><span class="sxs-lookup"><span data-stu-id="86786-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="86786-109">Em Olá outro terminar uma PaaS/SaaS completamente gerido oferta é mais como o Azure RemoteApp – um parceiro fornece uma camada de serviço por cima de uma solução de gestão remota que processa operacional e de manutenção, enquanto, como cliente Olá, fazer alguma gestão de aplicações e de imagem.</span><span class="sxs-lookup"><span data-stu-id="86786-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="86786-110">[Ver Olá Azure RemoteApp webinars nas opções de migração](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), ou continue a ler para obter mais informações, (incluindo exemplos de Olá diferente opções de alojamento).</span><span class="sxs-lookup"><span data-stu-id="86786-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="86786-111">Autogerida soluções de (IaaS)</span><span class="sxs-lookup"><span data-stu-id="86786-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="86786-112">**RDS no IaaS**</span><span class="sxs-lookup"><span data-stu-id="86786-112">**RDS on IaaS**</span></span>
<span data-ttu-id="86786-113">Pode implementar uma nativa baseado em sessões dos serviços de ambiente de trabalho remoto (no Windows Server) implementação utilizando o RemoteApp ou ambientes de trabalho no local ou num ambiente alojado (por exemplo, em VMs do Azure).</span><span class="sxs-lookup"><span data-stu-id="86786-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="86786-114">RDS em implementações IaaS são melhores para os clientes já familiarizados com e que tenham conhecimentos técnicos existente com as implementações de RDS.</span><span class="sxs-lookup"><span data-stu-id="86786-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="86786-115">É necessário com o Software Assurance (SA) de licenciamento em Volume para toouse de licenças de acesso de cliente RDS esta opção de implementação.</span><span class="sxs-lookup"><span data-stu-id="86786-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="86786-116">Implementação de RDS em VMs do Azure é mais fácil do que nunca quando utiliza a implementação e modelos de aplicação de patches (ler um [descrição geral](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) e, em seguida, [aceder-lhes obter](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="86786-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="86786-117">Pode obter Olá mesmas capacidades de dimensionamento elásticas com recursos de modelo de implementação clássico do Azure (não a recursos de modelo de recursos do Azure) no Azure RemoteApp utilizando Olá [automática dimensionamento script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), apesar de existirem mais configurações e personalizações.</span><span class="sxs-lookup"><span data-stu-id="86786-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="86786-118">Quando implementa o RDS em VMs do Azure, o suporte é fornecido através de [Azure suporta](https://azure.microsoft.com/support/plans/), Olá mesmo profissionais de suporte que suportados com o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="86786-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="86786-119">Pode obter custo estimativas com base na sua utilização existente contactando [suporte do Azure](https://azure.microsoft.com/support/plans/), ou pode efetuar cálculos por si através de um em breve toobe lançadas Calculadora de custo.</span><span class="sxs-lookup"><span data-stu-id="86786-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="86786-120">Além disso, com as VMs de série N (atualmente em pré-visualização privada) pode adicionar vGPU - saber mais sobre como adicionar vGPU e sobre como demasiado[escudo melhoramentos de RDS no Windows Server 2016](https://myignite.microsoft.com/videos/2794) na nossa sessão de Ignite.</span><span class="sxs-lookup"><span data-stu-id="86786-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="86786-121">Temos de guias de implementação passo a passo para [Windows Server 2012 R2](http://aka.ms/rdsonazure) e [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist com a sua implementação.</span><span class="sxs-lookup"><span data-stu-id="86786-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="86786-122">Veja Olá [blogue de ambiente de trabalho remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) para Olá mais recentes notícias de última hora.</span><span class="sxs-lookup"><span data-stu-id="86786-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="86786-123">**Citrix no IaaS**</span><span class="sxs-lookup"><span data-stu-id="86786-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="86786-124">Um Citrix nativo implementação baseados em sessão XenApp ou XenDesktop pode ser implementado no local ou num ambiente alojado (tal como em VMs do Azure).</span><span class="sxs-lookup"><span data-stu-id="86786-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="86786-125">Veja o guia de implementação passo a passo Olá, [Citrix XA 7.6 no Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="86786-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="86786-126">Leia mais sobre [Citrix no Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), incluindo uma calculadora de preços.</span><span class="sxs-lookup"><span data-stu-id="86786-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="86786-127">Também pode encontrar um [Citrix contacte](http://citrix.com/English/contact/index.asp) toodiscuss as opções de com.</span><span class="sxs-lookup"><span data-stu-id="86786-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="86786-128">Ofertas de (PaaS/SaaS) completamente geridas</span><span class="sxs-lookup"><span data-stu-id="86786-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="86786-129">Citrix XenApp Essentials (lançadas Abril de 2017)</span><span class="sxs-lookup"><span data-stu-id="86786-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="86786-130">Agora disponível no Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials é Olá novo serviço de Virtualização de aplicações, energia Olá de combinar e flexibilidade de Olá plataforma de nuvem Citrix com Olá simples, prescritiva, e de consumir a visão do Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="86786-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="86786-131">Clientes existentes do Azure RemoteApp podem [registar-se numa avaliação gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="86786-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="86786-132">Nota: Só encargos de serviço de utilizador Citrix é gratuito, aplicam-se de custos de armazenamento e computação do Azure</span><span class="sxs-lookup"><span data-stu-id="86786-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="86786-133">Saiba mais:</span><span class="sxs-lookup"><span data-stu-id="86786-133">Learn More:</span></span>
- [<span data-ttu-id="86786-134">Migrar a partir do Azure RemoteApp tooCitrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="86786-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="86786-135">Citrix e da Microsoft</span><span class="sxs-lookup"><span data-stu-id="86786-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="86786-136">[Apresentação do Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span><span class="sxs-lookup"><span data-stu-id="86786-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="86786-137">Citrix nuvem XenApp e XenDesktop serviço</span><span class="sxs-lookup"><span data-stu-id="86786-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="86786-138">[Citrix nuvem XenApp e XenDesktop serviço](https://www.citrix.com/products/citrix-cloud/services.html) é Olá melhor solução para a entrega de Olá de aplicações e ambientes de trabalho, mais avançada de gestão e capacidades de monitorização.</span><span class="sxs-lookup"><span data-stu-id="86786-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="86786-139">Conexlink (nome de plataforma: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="86786-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="86786-140">[MyCloudIT](https://mycloudit.com) é uma plataforma de automatização para toosimplify de empresas IT, otimizar e dimensionar migração Olá e Olá, entrega de ambientes de trabalho remotos, aplicações remotas e infraestrutura de nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="86786-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="86786-141">plataforma de MyCloudIT Olá reduz o tempo de implementação ao 95%, Azure custo por 30% e move-a infraestrutura de TI toda do seu cliente numa nuvem Olá num fim de alguns traços chaves.</span><span class="sxs-lookup"><span data-stu-id="86786-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="86786-142">Parceiros agora podem gerir clientes a partir de um dashboard global, os utilizadores finais de serviço à volta de Olá mundo como nunca antes e aumentar as receitas sem adicionar overhead adicional ou um vasto conjunto formação do Azure.</span><span class="sxs-lookup"><span data-stu-id="86786-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="86786-143">Localização principal: Dallas, TX, EUA</span><span class="sxs-lookup"><span data-stu-id="86786-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="86786-144">Região da operação: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="86786-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="86786-145">Estado de parceiros: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="86786-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="86786-146">Fornecedor de serviços de nuvem da Microsoft: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="86786-147">Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos</span><span class="sxs-lookup"><span data-stu-id="86786-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="86786-148">Soluções de migração do Azure RemoteApp: Sim, [Saiba mais](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="86786-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="86786-149">Brian Garoutte, VP de desenvolvimento de negócio</span><span class="sxs-lookup"><span data-stu-id="86786-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="86786-150">Telefone: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="86786-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="86786-151">E-mail:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="86786-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="86786-152">Moldura</span><span class="sxs-lookup"><span data-stu-id="86786-152">Frame</span></span>

<span data-ttu-id="86786-153">As organizações de TI na empresa e government, fornecedores de serviço geridas e os principais fornecedores de software escolha moldura toocreate e gerir as respetivas áreas de trabalho seguras e definidas por software na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="86786-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="86786-154">De toolarge pequenas organizações, moldura torna toolet incredibly fácil os utilizadores aceder às aplicações do Windows em qualquer browser a partir de qualquer dispositivo.</span><span class="sxs-lookup"><span data-stu-id="86786-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="86786-155">Olá plataforma de moldura inclui tudo um administrador necessidades toodeploy aplicações da nuvem Olá, incluindo Olá infraestrutura do Azure e licenças RDS (colocar a sua própria conta do Azure e licenças é opcional).</span><span class="sxs-lookup"><span data-stu-id="86786-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="86786-156">Saiba mais sobre [Frame no Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="86786-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="86786-157">Localização principal: San Mateo, AC, EUA</span><span class="sxs-lookup"><span data-stu-id="86786-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="86786-158">Região da operação: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="86786-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="86786-159">Parceiro da Microsoft: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="86786-160">Telefone: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="86786-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="86786-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="86786-161">Awingu</span></span>
<span data-ttu-id="86786-162">Awingu oferece uma solução de área de trabalho online simples com aplicações legadas, SaaS e os documentos a partir de um browser html5.</span><span class="sxs-lookup"><span data-stu-id="86786-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="86786-163">Como tal, disponibilizar quaisquer aplicações de forma segura em qualquer tipo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="86786-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="86786-164">Para os serviços SaaS, está disponível uma vasta gama op Single-Sign-On opções.</span><span class="sxs-lookup"><span data-stu-id="86786-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="86786-165">Também sistemas de ficheiros de diversos (nuvem) podem ser integrados profundamente na sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="86786-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="86786-166">Mobilidade de toofull seguinte, avançada online área de trabalho do Awingu de irá conceder-segurança ideal com controlos granulares (por exemplo, transferir/carregar), completo utilização auditoria, a multi-factor Authentication (por exemplo, o Azure MFA), a gravação da sessão e muito mais.</span><span class="sxs-lookup"><span data-stu-id="86786-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="86786-167">Out-of-a-box, Awingu ativa e aplicação de partilha sessão para colaboração otimizada e segura de documentos.</span><span class="sxs-lookup"><span data-stu-id="86786-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="86786-168">Solução do Awingu é API multi-inquilino, AD multi e aberto.</span><span class="sxs-lookup"><span data-stu-id="86786-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="86786-169">É utilizado pelo pequenas e grandes empresas, os fornecedores de serviços de nuvem e [ISVs](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="86786-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="86786-170">Estes clientes especialmente Agradecemos olá fáceis de utilizar, TCO facilidade para instalação e baixa.</span><span class="sxs-lookup"><span data-stu-id="86786-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="86786-171">Awingu tudo-em-é [disponíveis no Azure Marketplace de Olá](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) com 2 utilizadores em simultâneo incorporados.</span><span class="sxs-lookup"><span data-stu-id="86786-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="86786-172">Licenças adicionais estão disponíveis através de um [vasta gama de distribuidores e revendedores](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="86786-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="86786-173">Saiba mais sobre [Awingu no como tooAzure alternativo RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="86786-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="86786-174">Localização principal: Belgium</span><span class="sxs-lookup"><span data-stu-id="86786-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="86786-175">Regiões a funcionar: EMEA, América do Norte e Brasil</span><span class="sxs-lookup"><span data-stu-id="86786-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="86786-176">Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos</span><span class="sxs-lookup"><span data-stu-id="86786-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="86786-177">**Global**:</span><span class="sxs-lookup"><span data-stu-id="86786-177">**Global**:</span></span>
> 
> <span data-ttu-id="86786-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="86786-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="86786-179">E-mail:[arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="86786-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="86786-180">Telefone: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="86786-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="86786-181">**Belgium HQ**:</span><span class="sxs-lookup"><span data-stu-id="86786-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="86786-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="86786-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="86786-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="86786-183">9000 Gent</span></span>
> 
> <span data-ttu-id="86786-184">E-mail:[info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="86786-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="86786-185">Telefone: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="86786-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="86786-186">**EUA**:</span><span class="sxs-lookup"><span data-stu-id="86786-186">**USA**:</span></span>
> 
> <span data-ttu-id="86786-187">piso 7, 1177 Ave de Olá Americas,</span><span class="sxs-lookup"><span data-stu-id="86786-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="86786-188">Nova Iorque, NY 10036</span><span class="sxs-lookup"><span data-stu-id="86786-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="86786-189">E-mail:[info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="86786-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="86786-190">Microsoft Hospedava o fornecedor de serviço</span><span class="sxs-lookup"><span data-stu-id="86786-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="86786-191">Parceiros de alojamento oferecem, normalmente, um completamente gerido de ambiente de trabalho do Windows alojados e Olá de serviço de aplicações, que pode incluir a gestão de recursos do Azure, sistemas operativos, aplicações e suporte técnico com o parceiro de Olá do contratos de licenciamento em com a Microsoft e outros fornecedores de software, juntamente com a ser um contrato de licença de fornecedor de serviços tooallow reselling de licença de acesso de subscritor (SAL).</span><span class="sxs-lookup"><span data-stu-id="86786-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="86786-192">Olá informações seguintes fornecem detalhes e informações de contacto para algumas das Olá de que os fornecedores que especialização em clientes com a respetiva migração do Azure RemoteApp a prestar assistência.</span><span class="sxs-lookup"><span data-stu-id="86786-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="86786-193">Veja [lista atual de Olá de fornecedores de serviços alojados](http://aka.ms/rdsonazurecertified) que concluiu Olá RDS no IaaS learning caminho e avaliação.</span><span class="sxs-lookup"><span data-stu-id="86786-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="86786-194">Programa de fornecedor de serviço do Citrix</span><span class="sxs-lookup"><span data-stu-id="86786-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="86786-195">Olá programa de fornecedor de serviço do Citrix torna mais fácil de simplicidade Olá de toodeliver de fornecedores do serviço de nuvem virtual informática tooSMBs, oferece os serviços de Olá pretendem um modelo de fácil, pay as you go.</span><span class="sxs-lookup"><span data-stu-id="86786-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="86786-196">Fornecedores de serviços do Citrix aumentar as respetivas empresas da Microsoft SPLA e expandir os seus investimentos de plataforma RDS com qualquer dispositivo, acesso em qualquer local, hello mais amplas suporte da aplicação, uma experiência otimizada, maior segurança e maior escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="86786-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="86786-197">Por sua vez, os fornecedores de serviços de Citrix, attract subscritores mais aumentar satisfação do cliente e reduzir os custos operacionais.</span><span class="sxs-lookup"><span data-stu-id="86786-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="86786-198">[Saiba mais](http://www.citrix.com/products/service-providers.html) ou [localizar um parceiro](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="86786-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="86786-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="86786-199">Acuutech</span></span>
<span data-ttu-id="86786-200">[Acuutech](http://www.acuutech.com) specializes no fornecimento de soluções de ambiente de trabalho alojadas, entrega de ambiente de trabalho completo e aplicações de ISV experiências criadas no Microsoft tecnologia tooa global cliente base a partir do Azure e os respetivos centros de dados.</span><span class="sxs-lookup"><span data-stu-id="86786-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="86786-201">Localização principal: Londres, RU; Singapura; Houston, TX</span><span class="sxs-lookup"><span data-stu-id="86786-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="86786-202">Região da operação: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="86786-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="86786-203">Estado de parceiros: Gold</span><span class="sxs-lookup"><span data-stu-id="86786-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="86786-204">Fornecedor de serviços de nuvem da Microsoft: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="86786-205">Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos</span><span class="sxs-lookup"><span data-stu-id="86786-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="86786-206">Soluções de migração do Azure RemoteApp: Sim, [Saiba mais](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="86786-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="86786-207">**Reino Unido**:</span><span class="sxs-lookup"><span data-stu-id="86786-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="86786-208">5/6 Iorque próxima, Langston viagem,</span><span class="sxs-lookup"><span data-stu-id="86786-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="86786-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="86786-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="86786-210">Telefone: + 44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="86786-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="86786-211">**Singapura**:</span><span class="sxs-lookup"><span data-stu-id="86786-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="86786-212">Rua 100 Cecil, #09-02</span><span class="sxs-lookup"><span data-stu-id="86786-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="86786-213">Olá globo, Singapura 069532</span><span class="sxs-lookup"><span data-stu-id="86786-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="86786-214">Telefone: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="86786-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="86786-215">**América do Norte**:</span><span class="sxs-lookup"><span data-stu-id="86786-215">**North America**:</span></span>
>   
> <span data-ttu-id="86786-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="86786-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="86786-217">200 Suite, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="86786-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="86786-218">Telefone: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="86786-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="86786-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="86786-219">ASPEX</span></span>
<span data-ttu-id="86786-220">[ASPEX](http://www.aspex.be/en) specializes no ISVs transição toohello na nuvem e de ISV' procura toooptimize os respetivos atual setups de nuvem.</span><span class="sxs-lookup"><span data-stu-id="86786-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="86786-221">ASPEX oferece um vasto leque de serviços geridos, devops e serviços de consultoria.</span><span class="sxs-lookup"><span data-stu-id="86786-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="86786-222">Localização principal: Antwerp, Belgium</span><span class="sxs-lookup"><span data-stu-id="86786-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="86786-223">Região da operação: na Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="86786-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="86786-224">Estado de parceiros: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="86786-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="86786-225">Fornecedor de serviços de nuvem da Microsoft: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="86786-226">Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos</span><span class="sxs-lookup"><span data-stu-id="86786-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="86786-227">Soluções de migração do Azure RemoteApp: Sim, [Saiba mais](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="86786-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="86786-228">Telefone: +3232202198</span><span class="sxs-lookup"><span data-stu-id="86786-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="86786-229">Correio:[info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="86786-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="86786-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="86786-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="86786-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="86786-231">Caase.com</span></span>
<span data-ttu-id="86786-232">[Caase.com](http://www.caase.com/) ajuda empresas, governments locais, não governamental corpos e instituições cuidados de saúde com os respetivos journey para uma forma mais inteligente do trabalho em Olá Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="86786-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="86786-233">A ser produtivos e segura em qualquer local, com qualquer dispositivo e em custos com TI baixo.</span><span class="sxs-lookup"><span data-stu-id="86786-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="86786-234">Caase.com é uma especialista em verdadeira para Microsoft Office365, o Azure, o Enterprise Mobility, segurança e Windows.</span><span class="sxs-lookup"><span data-stu-id="86786-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="86786-235">Com o nosso consultancy, serviços de migração, os programas de adoção, formação, gestão e suporte Caase.com cria uma plataforma otimizada e segura para colaboração para clientes que os funcionários, parceiros e fornecedores.</span><span class="sxs-lookup"><span data-stu-id="86786-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="86786-236">Caase.com é mastermind Olá de Olá área de trabalho remoto do Azure (área de trabalho móvel) e Olá Digital à área de trabalho (sociais Intranet).</span><span class="sxs-lookup"><span data-stu-id="86786-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="86786-237">Ambas as soluções – conseguidas com a adoção – são foundation Olá que assegura que os utilizadores de Olá destas soluções têm Olá mais pleasant, com êxito e eficaz a experiência no respetivo toohello rota Microsoft Cloud.</span><span class="sxs-lookup"><span data-stu-id="86786-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="86786-238">Neerlandês tradução ánd um filme suporte através de aqui: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="86786-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="86786-239">Região da operação: com base neerlandês, alcance global</span><span class="sxs-lookup"><span data-stu-id="86786-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="86786-240">Estado de parceiros: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="86786-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="86786-241">Fornecedor de serviços de nuvem da Microsoft: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="86786-242">Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos</span><span class="sxs-lookup"><span data-stu-id="86786-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="86786-243">Soluções de migração do Azure RemoteApp: Sim, [mais](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="86786-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="86786-244">Países Baixos:</span><span class="sxs-lookup"><span data-stu-id="86786-244">Netherlands:</span></span>
> 
> <span data-ttu-id="86786-245">Rigtersbleek-Zandvoort 10 (Alemanha Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="86786-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="86786-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="86786-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="86786-247">Telefone: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="86786-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="86786-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="86786-248">Nerdio</span></span>
<span data-ttu-id="86786-249">[Nerdio para o Azure](http://getnerdio.com/nfa/) é uma plataforma de automatização de IT que fornece seja extremamente simples de aprovisionamento, gestão e a otimização de ambientes de TI completas no Olá nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86786-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="86786-250">Configurar ambientes de trabalho virtuais, aplicações remotas e os servidores a funcionar nas duas horas.</span><span class="sxs-lookup"><span data-stu-id="86786-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="86786-251">Administrar o ambiente de Olá no três cliques ou menos com o Portal de administração de Nerdio.</span><span class="sxs-lookup"><span data-stu-id="86786-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="86786-252">Utilize inteligente dimensionamento automático e guardar 40 too60% em recursos IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="86786-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="86786-253">Localização principal: região de operação de Chicago, IL: Estado de parceiro em todo o mundo: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) fornecedor de serviços do Microsoft Cloud: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="86786-254">Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos</span><span class="sxs-lookup"><span data-stu-id="86786-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="86786-255">Soluções de migração do Azure RemoteApp: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="86786-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="86786-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="86786-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="86786-257">Suite 212</span></span>
> 
> <span data-ttu-id="86786-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="86786-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="86786-259">EUA</span><span class="sxs-lookup"><span data-stu-id="86786-259">USA</span></span>
> 
> <span data-ttu-id="86786-260">Ext. 4NERDIO (844) 6</span><span class="sxs-lookup"><span data-stu-id="86786-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="86786-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="86786-261">**SaaSplaza**</span></span>
<span data-ttu-id="86786-262">[SaaSplaza](http://www.saasplaza.com/) oferece completa Microsoft Dynamics portefólio (NAV AX, GP, SL, CRM) pública e privada de nuvem (Azure).</span><span class="sxs-lookup"><span data-stu-id="86786-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="86786-263">Localização principal: Países Baixos</span><span class="sxs-lookup"><span data-stu-id="86786-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="86786-264">Operação região: em todo o mundo</span><span class="sxs-lookup"><span data-stu-id="86786-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="86786-265">Estado de parceiros: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="86786-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="86786-266">Fornecedor de serviços de nuvem da Microsoft: Sim</span><span class="sxs-lookup"><span data-stu-id="86786-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="86786-267">Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos</span><span class="sxs-lookup"><span data-stu-id="86786-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="86786-268">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="86786-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="86786-269">Prins Mauritslaan 29 35</span><span class="sxs-lookup"><span data-stu-id="86786-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="86786-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="86786-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="86786-271">Olá Países Baixos</span><span class="sxs-lookup"><span data-stu-id="86786-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="86786-272">Telefone: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="86786-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="86786-273">**Americas**:</span><span class="sxs-lookup"><span data-stu-id="86786-273">**Americas**:</span></span>
> 
> <span data-ttu-id="86786-274">171 Saxony viagem, Suite 105</span><span class="sxs-lookup"><span data-stu-id="86786-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="86786-275">Encinitas, AC 92024</span><span class="sxs-lookup"><span data-stu-id="86786-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="86786-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="86786-276">San Diego</span></span>
> 
> <span data-ttu-id="86786-277">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="86786-277">United States</span></span>
> 
> <span data-ttu-id="86786-278">Telefone: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="86786-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="86786-279">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="86786-279">**APAC**:</span></span>
> 
> <span data-ttu-id="86786-280">105 Cecil Rua</span><span class="sxs-lookup"><span data-stu-id="86786-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="86786-281">\#11-08, Olá Octagon</span><span class="sxs-lookup"><span data-stu-id="86786-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="86786-282">Singapura 069534</span><span class="sxs-lookup"><span data-stu-id="86786-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="86786-283">Singapura</span><span class="sxs-lookup"><span data-stu-id="86786-283">Singapore</span></span>
>   
> <span data-ttu-id="86786-284">Phone - Singapura: +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="86786-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="86786-285">Phone - Austrália: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="86786-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="86786-286">Phone - Nova Zelândia: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="86786-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="86786-287">Precisa de mais ajuda?</span><span class="sxs-lookup"><span data-stu-id="86786-287">Need more help?</span></span>
<span data-ttu-id="86786-288">Ainda precisa de ajudar a escolher ou tem mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="86786-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="86786-289">Utilize um dos Olá métodos tooget ajuda a seguir.</span><span class="sxs-lookup"><span data-stu-id="86786-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="86786-290">Enviar-nos por e-mail [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="86786-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="86786-291">Contacte [suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="86786-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="86786-292">Iniciar, abrindo um [caso de suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="86786-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="86786-293">Chamada-nos.</span><span class="sxs-lookup"><span data-stu-id="86786-293">Call us.</span></span> <span data-ttu-id="86786-294">[Localizar um número de venda local](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="86786-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

