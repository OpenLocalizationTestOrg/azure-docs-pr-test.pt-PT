---
title: "dispositivos associados ao aaaHow tooconfigure híbrida do Azure Active Directory | Microsoft Docs"
description: "Saiba como dispositivos associados ao tooconfigure híbrida do Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: f97ea436eca2833d8a9843acd19e5c633bc0fc07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a><span data-ttu-id="d360b-103">Como dispositivos associados ao tooconfigure híbrida do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d360b-103">How tooconfigure hybrid Azure Active Directory joined devices</span></span>

<span data-ttu-id="d360b-104">Gestão de dispositivos no Azure Active Directory (Azure AD), pode certificar-se de que os utilizadores acedem aos seus recursos dos dispositivos que cumprem as normas de segurança e conformidade.</span><span class="sxs-lookup"><span data-stu-id="d360b-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="d360b-105">Para obter mais detalhes, consulte [gestão toodevice de introdução no Azure Active Directory](device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d360b-105">For more details, see [Introduction toodevice management in Azure Active Directory](device-management-introduction.md).</span></span>

<span data-ttu-id="d360b-106">Se tiver um ambiente do Active Directory no local e quiser toojoin tooAzure a dispositivos associados a um domínio AD, pode realizar esta através da configuração híbrida do Azure AD associado dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d360b-106">If you have an on-premises Active Directory environment and you want toojoin your domain-joined devices tooAzure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="d360b-107">tópico de Olá disponibiliza Olá relacionados com os passos.</span><span class="sxs-lookup"><span data-stu-id="d360b-107">hello topic provides you with hello related steps.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="d360b-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d360b-108">Before you begin</span></span>

<span data-ttu-id="d360b-109">Antes de iniciar a configuração híbrida do Azure AD dispositivos associados a um no seu ambiente, deverá familiarizar-se com restrições de Olá e cenários de Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="d360b-109">Before you start configuring hybrid Azure AD joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="d360b-110">tooimprove Olá facilitar a leitura de descrições de Olá, este tópico utiliza Olá termo os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d360b-110">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="d360b-111">**Dispositivos atuais do Windows** -este prazo refere-se associados a um toodomain dispositivos com Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d360b-111">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="d360b-112">**Dispositivos de nível inferior do Windows** -este prazo refere-se tooall **suportado** dispositivos Windows associados a um domínio, que estão em execução Windows 10 nem do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d360b-112">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="d360b-113">Dispositivos atuais do Windows</span><span class="sxs-lookup"><span data-stu-id="d360b-113">Windows current devices</span></span>

- <span data-ttu-id="d360b-114">Para dispositivos com o sistema operativo da ambiente de trabalho de Windows hello, recomendamos que utilize o Windows 10 aniversário da atualização (versão 1607) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d360b-114">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="d360b-115">Olá, registo de dispositivos atuais do Windows **é** suportada em ambientes não federada, tais como configurações de sincronização de hash de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="d360b-115">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="d360b-116">Dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="d360b-116">Windows down-level devices</span></span>

- <span data-ttu-id="d360b-117">Olá seguintes dispositivos de nível inferior do Windows é suportada:</span><span class="sxs-lookup"><span data-stu-id="d360b-117">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="d360b-118">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d360b-118">Windows 8.1</span></span>
    - <span data-ttu-id="d360b-119">Windows 7</span><span class="sxs-lookup"><span data-stu-id="d360b-119">Windows 7</span></span>
    - <span data-ttu-id="d360b-120">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d360b-120">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="d360b-121">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d360b-121">Windows Server 2012</span></span>
    - <span data-ttu-id="d360b-122">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d360b-122">Windows Server 2008 R2</span></span>
- <span data-ttu-id="d360b-123">Olá, registo de dispositivos de nível inferior do Windows **é** suportada em ambientes não federada através de totalmente integrada de sessão único [do Azure Active Directory totalmente integrada Single Sign-On](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="d360b-123">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="d360b-124">Olá, registo de dispositivos de nível inferior do Windows **não é** suportados para dispositivos com perfis itinerantes.</span><span class="sxs-lookup"><span data-stu-id="d360b-124">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="d360b-125">Se estiver a depender de perfis ou definições de roaming, utilize o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d360b-125">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="d360b-126">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d360b-126">Prerequisites</span></span>

<span data-ttu-id="d360b-127">Antes de iniciar a ativação híbrida do Azure AD associado dispositivos na sua organização, terá de toomake certificar-se de que está a executar uma versão atualizada do Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="d360b-127">Before you start enabling hybrid Azure AD joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="d360b-128">Do Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="d360b-128">Azure AD Connect:</span></span>

- <span data-ttu-id="d360b-129">Mantém a associação de Olá entre a conta de computador Olá no objeto de dispositivo Olá no Azure AD e no local do Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="d360b-129">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="d360b-130">Permite que outros dispositivos relacionados com funcionalidades como o Windows Hello para empresas.</span><span class="sxs-lookup"><span data-stu-id="d360b-130">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="d360b-131">Passos de configuração</span><span class="sxs-lookup"><span data-stu-id="d360b-131">Configuration steps</span></span>

<span data-ttu-id="d360b-132">Pode configurar híbrida do Azure AD associado dispositivos para vários tipos de plataformas de dispositivos do Windows.</span><span class="sxs-lookup"><span data-stu-id="d360b-132">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="d360b-133">Este tópico inclui os passos de Olá necessário para todos os cenários de configuração típica.</span><span class="sxs-lookup"><span data-stu-id="d360b-133">This topic includes hello required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="d360b-134">Utilize Olá tabela tooget uma descrição geral dos passos de Olá que são necessários para o seu cenário a seguir:</span><span class="sxs-lookup"><span data-stu-id="d360b-134">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="d360b-135">Passos</span><span class="sxs-lookup"><span data-stu-id="d360b-135">Steps</span></span>                                      | <span data-ttu-id="d360b-136">Sincronização de hash de atual e a palavra-passe do Windows</span><span class="sxs-lookup"><span data-stu-id="d360b-136">Windows current and password hash sync</span></span> | <span data-ttu-id="d360b-137">Atual do Windows e a Federação</span><span class="sxs-lookup"><span data-stu-id="d360b-137">Windows current and federation</span></span> | <span data-ttu-id="d360b-138">Windows de nível inferior</span><span class="sxs-lookup"><span data-stu-id="d360b-138">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="d360b-139">Passo 1: Configurar o ponto de ligação de serviço</span><span class="sxs-lookup"><span data-stu-id="d360b-139">Step 1: Configure service connection point</span></span> | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |
| <span data-ttu-id="d360b-143">Passo 2: Configurar a emissão de afirmações</span><span class="sxs-lookup"><span data-stu-id="d360b-143">Step 2: Setup issuance of claims</span></span>           |                                        | ![Marcar][1]                    | ![Marcar][1]        |
| <span data-ttu-id="d360b-146">Passo 3: Ativar dispositivos não Windows 10</span><span class="sxs-lookup"><span data-stu-id="d360b-146">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Marcar][1]        |
| <span data-ttu-id="d360b-148">Passo 4: Implementação de controlo e implementação</span><span class="sxs-lookup"><span data-stu-id="d360b-148">Step 4: Control deployment and rollout</span></span>     | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |
| <span data-ttu-id="d360b-152">Passo 5: Verificar se a dispositivos associados</span><span class="sxs-lookup"><span data-stu-id="d360b-152">Step 5: Verify joined devices</span></span>          | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="d360b-156">Passo 1: Configurar o ponto de ligação de serviço</span><span class="sxs-lookup"><span data-stu-id="d360b-156">Step 1: Configure service connection point</span></span>

<span data-ttu-id="d360b-157">objeto de (SCP) do ponto de ligação de serviço Olá é utilizado pelos seus dispositivos durante Olá registo toodiscover informações de inquilino do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360b-157">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="d360b-158">No local no Active Directory (AD), objeto Olá SCP para Olá híbrida do Azure AD associados a um dispositivos tem de existir na partição de contexto de nomenclatura de configuração do Olá da floresta do computador Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-158">In your on-premises Active Directory (AD), hello SCP object for hello hybrid Azure AD joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="d360b-159">Não há apenas um contexto de nomenclatura de configuração por floresta.</span><span class="sxs-lookup"><span data-stu-id="d360b-159">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="d360b-160">Numa configuração várias floresta do Active Directory, tem de existir ponto de ligação de serviço Olá em todas as florestas que contêm os computadores associados a um domínio.</span><span class="sxs-lookup"><span data-stu-id="d360b-160">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="d360b-161">Pode utilizar Olá [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Olá contexto nomenclatura de configuração da sua floresta.</span><span class="sxs-lookup"><span data-stu-id="d360b-161">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="d360b-162">Para uma floresta com o nome de domínio do Active Directory Olá *fabrikam.com*, contexto de nomenclatura de configuração de Olá é:</span><span class="sxs-lookup"><span data-stu-id="d360b-162">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="d360b-163">Na sua floresta, o objeto de Olá SCP para Olá-registo automático de dispositivos associados a um domínio está localizado em:</span><span class="sxs-lookup"><span data-stu-id="d360b-163">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="d360b-164">Dependendo de como tiver implementado o Azure AD Connect, objeto de SCP Olá poderá já tiverem sido configurado.</span><span class="sxs-lookup"><span data-stu-id="d360b-164">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="d360b-165">Pode verificar a existência de Olá do objeto de Olá e obter valores de deteção de Olá utilizando Olá seguinte script do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d360b-165">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="d360b-166">Olá **$scp. As palavras-chave** saída mostra informações de inquilino do Azure AD de Olá, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d360b-166">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="d360b-167">Se o ponto de ligação de serviço Olá não existir, pode criá-la executando Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet no seu servidor do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d360b-167">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="d360b-168">Credencial de administrador de empresa é necessário toorun este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d360b-168">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="d360b-169">Olá cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d360b-169">hello cmdlet:</span></span>

- <span data-ttu-id="d360b-170">Cria o ponto de ligação de serviço Olá na floresta do Active Directory Olá do Azure AD Connect está ligado.</span><span class="sxs-lookup"><span data-stu-id="d360b-170">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="d360b-171">Requer que toospecify Olá `AdConnectorAccount` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d360b-171">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="d360b-172">Esta é a conta de Olá que está configurada como o Active Directory a conta do conector no Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="d360b-172">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="d360b-173">Olá script seguinte mostra um exemplo de utilização do cmdlet Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-173">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="d360b-174">Este script, `$aadAdminCred = Get-Credential` requer tootype um nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="d360b-174">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="d360b-175">Terá de nome de utilizador de Olá tooprovide no formato de nome principal (UPN) do utilizador Olá (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="d360b-175">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="d360b-176">Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d360b-176">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="d360b-177">Utiliza o módulo PowerShell do Active Directory de Olá, que depende de serviços da Web do Active Directory em execução num controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="d360b-177">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="d360b-178">Serviços da Web do Active Directory é suportada em controladores de domínio com o Windows Server 2008 R2 e posterior.</span><span class="sxs-lookup"><span data-stu-id="d360b-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="d360b-179">Só é suportado pelo Olá **MSOnline PowerShell versão do módulo 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="d360b-179">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="d360b-180">toodownload este módulo, utilize esta opção [ligação](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="d360b-180">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="d360b-181">Para controladores de domínio a executar o Windows Server 2008 ou de versões anteriores, utilize o script de Olá abaixo o ponto de ligação de serviço toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-181">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="d360b-182">Numa configuração de várias floresta, deve utilizar Olá seguir o ponto de ligação do serviço do script toocreate Olá em cada floresta onde existem computadores:</span><span class="sxs-lookup"><span data-stu-id="d360b-182">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="d360b-183">Passo 2: Configurar a emissão de afirmações</span><span class="sxs-lookup"><span data-stu-id="d360b-183">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="d360b-184">No Azure federado configuração do AD, dispositivos dependem de serviços de Federação do Active Directory (AD FS) ou um terceiros 3rd no local tooAzure de tooauthenticate de serviço de Federação AD.</span><span class="sxs-lookup"><span data-stu-id="d360b-184">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="d360b-185">Dispositivos autenticar tooget um tooregister de token de acesso contra Olá Service do Azure Active Directory dispositivo registo (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="d360b-185">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="d360b-186">Windows dispositivos atuais autenticam utilizando a autenticação integrada do Windows tooan WS-Trust ponto final ativo (versões 1.3 ou 2005) alojado pelo serviço de Federação Olá no local.</span><span class="sxs-lookup"><span data-stu-id="d360b-186">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="d360b-187">Quando utilizar o AD FS, quer **adfs/services/confiança/13/windowstransport** ou **adfs/services/confiança/2005/windowstransport** tem de estar ativada.</span><span class="sxs-lookup"><span data-stu-id="d360b-187">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="d360b-188">Se estiver a utilizar Olá Proxy de autenticação da Web, certifique-se também que este ponto final está publicado através do proxy de Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-188">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="d360b-189">Pode ver que os parâmetros são ativados através da consola de gestão de Olá do AD FS em **serviço > pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="d360b-189">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="d360b-190">Se não tiver o AD FS como o serviço de Federação no local, siga instruções de Olá do seu toomake fornecedor se suportam 1.3 de WS-Trust ou pontos finais de 2005 e estes são publicadas através de Olá ficheiro de troca de metadados (MEX).</span><span class="sxs-lookup"><span data-stu-id="d360b-190">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="d360b-191">Olá seguintes afirmações têm de existir no token de Olá recebido pelo Azure DRS para toocomplete de registo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d360b-191">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="d360b-192">Azure DRS irá criar um objeto de dispositivo no Azure AD com algumas destas informações que, em seguida, são utilizadas pelo objeto de dispositivo do Azure AD Connect tooassociate Olá recém-criado com Olá computador conta no local.</span><span class="sxs-lookup"><span data-stu-id="d360b-192">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="d360b-193">Se tiver mais do que um nome de domínio verificado, terá de Olá tooprovide afirmação para computadores a seguir:</span><span class="sxs-lookup"><span data-stu-id="d360b-193">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="d360b-194">Se já estiver a emitir uma afirmação de ImmutableID (por exemplo, o ID de início de sessão alternativo) terá tooprovide uma afirmação correspondente para computadores:</span><span class="sxs-lookup"><span data-stu-id="d360b-194">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="d360b-195">Olá secções a seguir, encontrará informações sobre:</span><span class="sxs-lookup"><span data-stu-id="d360b-195">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="d360b-196">valores de Olá cada afirmação deve ter</span><span class="sxs-lookup"><span data-stu-id="d360b-196">hello values each claim should have</span></span>
- <span data-ttu-id="d360b-197">Como uma definição deverá ter o seguinte aspeto no AD FS</span><span class="sxs-lookup"><span data-stu-id="d360b-197">How a definition would look like in AD FS</span></span>

<span data-ttu-id="d360b-198">definição de Olá ajuda-o a tooverify se valores Olá estão presentes ou se terá toocreate-los.</span><span class="sxs-lookup"><span data-stu-id="d360b-198">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="d360b-199">Se não utilizar o AD FS para o servidor de Federação no local, siga estas afirmações tooissue do seu fornecedor instruções toocreate Olá configuração apropriada.</span><span class="sxs-lookup"><span data-stu-id="d360b-199">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="d360b-200">Afirmações de tipo de conta do problema</span><span class="sxs-lookup"><span data-stu-id="d360b-200">Issue account type claim</span></span>

<span data-ttu-id="d360b-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Esta afirmação tem de conter um valor de **DJ**, que identifica o dispositivo de Olá como um computador associado ao domínio.</span><span class="sxs-lookup"><span data-stu-id="d360b-201">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="d360b-202">No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:</span><span class="sxs-lookup"><span data-stu-id="d360b-202">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="d360b-203">Emitir objectGUID de Olá computador conta no local</span><span class="sxs-lookup"><span data-stu-id="d360b-203">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="d360b-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Esta afirmação tem de conter Olá **objectGUID** valor Olá no local a conta de computador.</span><span class="sxs-lookup"><span data-stu-id="d360b-204">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="d360b-205">No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:</span><span class="sxs-lookup"><span data-stu-id="d360b-205">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="d360b-206">Emitir Sidobjeto de Olá computador conta no local</span><span class="sxs-lookup"><span data-stu-id="d360b-206">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="d360b-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Esta afirmação tem de conter Olá Olá **Sidobjeto** valor Olá no local a conta de computador.</span><span class="sxs-lookup"><span data-stu-id="d360b-207">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="d360b-208">No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:</span><span class="sxs-lookup"><span data-stu-id="d360b-208">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="d360b-209">Emitir issuerID para computador quando múltiplos verificar nomes de domínio no Azure AD</span><span class="sxs-lookup"><span data-stu-id="d360b-209">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="d360b-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Esta afirmação tem de conter Olá identificador de recurso uniforme (URI) de qualquer um dos Olá verificar nomes de domínio que se ligam com Olá no local token de Olá de emissora de serviço (AD FS ou terceiros 3rd) de Federação.</span><span class="sxs-lookup"><span data-stu-id="d360b-210">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="d360b-211">No AD FS, pode adicionar regras de transformação de emissão que parece ser Olá aqueles abaixo nessa ordem específica após Olá aqueles acima.</span><span class="sxs-lookup"><span data-stu-id="d360b-211">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="d360b-212">Tenha em atenção que um tooexplicitly problema Olá regra para os utilizadores é necessário.</span><span class="sxs-lookup"><span data-stu-id="d360b-212">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="d360b-213">Em regras de Olá abaixo, é adicionada uma regra primeiro identificar utilizador vs. a autenticação de computador.</span><span class="sxs-lookup"><span data-stu-id="d360b-213">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="d360b-214">Na afirmação Olá acima,</span><span class="sxs-lookup"><span data-stu-id="d360b-214">In hello claim above,</span></span>

- <span data-ttu-id="d360b-215">`$<domain>`é o URL do serviço Olá AD FS</span><span class="sxs-lookup"><span data-stu-id="d360b-215">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="d360b-216">`<verified-domain-name>`é um marcador de posição terá tooreplace com um dos seus nomes de domínio verificado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="d360b-216">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="d360b-217">Para obter mais detalhes sobre os nomes de domínio verificado, consulte [adicionar um tooAzure de nome de domínio personalizado do Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d360b-217">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="d360b-218">tooget uma lista dos seus domínios verificados da empresa, pode utilizar Olá [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d360b-218">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="d360b-220">Emitir ImmutableID para computador quando existe uma para os utilizadores (por exemplo, início de sessão alternativo ID está definido)</span><span class="sxs-lookup"><span data-stu-id="d360b-220">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="d360b-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Esta afirmação tem de conter um valor válido para computadores.</span><span class="sxs-lookup"><span data-stu-id="d360b-221">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="d360b-222">No AD FS, pode criar uma regra de transformação de emissão da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d360b-222">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="d360b-223">Programa auxiliar script toocreate Olá AD FS transformação regras de emissão</span><span class="sxs-lookup"><span data-stu-id="d360b-223">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="d360b-224">Olá seguinte script ajuda-o com a criação de emissão de Olá Olá descritas acima de regras de transformação.</span><span class="sxs-lookup"><span data-stu-id="d360b-224">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="d360b-225">Observações</span><span class="sxs-lookup"><span data-stu-id="d360b-225">Remarks</span></span> 

- <span data-ttu-id="d360b-226">Este script acrescenta regras existentes do Olá regras toohello.</span><span class="sxs-lookup"><span data-stu-id="d360b-226">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="d360b-227">Não execute scripts de Olá duas vezes porque Olá conjunto de regras seriam adicionado duas vezes.</span><span class="sxs-lookup"><span data-stu-id="d360b-227">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="d360b-228">Certifique-se de que nenhum correspondentes existem regras para estas afirmações (em condições de correspondente Olá) antes de executar o script de Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="d360b-228">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="d360b-229">Se tiver vários verificado nomes de domínio (conforme ilustrado no portal do Azure AD de Olá ou através do cmdlet Olá Get MsolDomains), defina o valor de Olá de **$multipleVerifiedDomainNames** no Olá script demasiado**$true**.</span><span class="sxs-lookup"><span data-stu-id="d360b-229">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="d360b-230">Certifique-se também que remova qualquer afirmação issuerid existente que poderá ter sido criada pelo Azure AD Connect ou através de outros meios.</span><span class="sxs-lookup"><span data-stu-id="d360b-230">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="d360b-231">Eis um exemplo para esta regra:</span><span class="sxs-lookup"><span data-stu-id="d360b-231">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="d360b-232">Se já ter emitido uma **ImmutableID** de afirmação para contas de utilizador, defina o valor de Olá de **$immutableIDAlreadyIssuedforUsers** no Olá script demasiado**$true**.</span><span class="sxs-lookup"><span data-stu-id="d360b-232">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="d360b-233">Passo 3: Ativar os dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="d360b-233">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="d360b-234">Se alguns dos seus dispositivos associados a um domínio Windows nível dispositivos, tem de:</span><span class="sxs-lookup"><span data-stu-id="d360b-234">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="d360b-235">Defina uma política no Azure AD tooenable dispositivos tooregister de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="d360b-235">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="d360b-236">Configurar o seu local Federação serviço tooissue afirmações toosupport **autenticação integrada de Windows (IWA)** para registo de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d360b-236">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="d360b-237">Adicione Olá do Azure AD dispositivos autenticação ponto final toohello Intranet zonas locais tooavoid certificado solicita ao autenticar o dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-237">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="d360b-238">Definir a política no Azure AD tooenable dispositivos tooregister de utilizadores</span><span class="sxs-lookup"><span data-stu-id="d360b-238">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="d360b-239">dispositivos de nível inferior do tooregister Windows, terá de toomake se esse Olá definição tooallow utilizadores tooregister dispositivos no Azure AD está definido.</span><span class="sxs-lookup"><span data-stu-id="d360b-239">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="d360b-240">No portal do Azure Olá, pode encontrar esta definição em:</span><span class="sxs-lookup"><span data-stu-id="d360b-240">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="d360b-241">Olá política seguinte tem de ser definida demasiado**todos os**: **os utilizadores podem registar os seus dispositivos com o Azure AD**</span><span class="sxs-lookup"><span data-stu-id="d360b-241">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Registar dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="d360b-243">Configurar o serviço de Federação no local</span><span class="sxs-lookup"><span data-stu-id="d360b-243">Configure on-premises federation service</span></span> 

<span data-ttu-id="d360b-244">O serviço de Federação no local tem de suportar Olá emissora **authenticationmehod** e **wiaormultiauthn** afirmações ao receber uma autenticação pedem toohello do Azure AD da entidade confiadora, que contém um resouce_params parâmetro com um valor de codificação como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="d360b-244">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="d360b-245">Quando é fornecido este pedido, serviço de Federação no local Olá utilizador Olá utilizando a autenticação integrada do Windows tem de ser autenticado e após com êxito, este tem de emitir Olá seguintes duas afirmações:</span><span class="sxs-lookup"><span data-stu-id="d360b-245">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="d360b-246">No AD FS, tem de adicionar uma regra de transformação de emissão que método de autenticação através de transmite Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-246">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="d360b-247">**tooadd esta regra:**</span><span class="sxs-lookup"><span data-stu-id="d360b-247">**tooadd this rule:**</span></span>

1. <span data-ttu-id="d360b-248">Na consola de gestão do Olá AD FS, aceda demasiado`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="d360b-248">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="d360b-249">Objetos de confiança das entidades confiadoras do Olá plataforma de identidade do Microsoft Office 365 com o botão direito e, em seguida, selecione **editar regras de afirmação**.</span><span class="sxs-lookup"><span data-stu-id="d360b-249">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="d360b-250">No Olá **regras de transformação de emissão** separador, selecione **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="d360b-250">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="d360b-251">No Olá **regra de afirmação** lista de modelo, selecione **enviar afirmações utilizando uma regra personalizada**.</span><span class="sxs-lookup"><span data-stu-id="d360b-251">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="d360b-252">Selecione **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="d360b-252">Select **Next**.</span></span>
6. <span data-ttu-id="d360b-253">No Olá **nome da regra de afirmação** caixa, escreva **regra de afirmação de método de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="d360b-253">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="d360b-254">No Olá **regra de afirmação** caixa, Olá tipo seguinte regra:</span><span class="sxs-lookup"><span data-stu-id="d360b-254">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="d360b-255">No servidor de Federação, escreva o comando do PowerShell Olá abaixo depois de substituir  **\<RPObjectName\>**  com Olá entidade confiadora terceiros nome do objeto para os objetos de confiança das entidades confiadoras do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360b-255">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="d360b-256">Este objeto é normalmente denominado **plataforma de identidade do Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="d360b-256">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="d360b-257">Adicionar zonas de Local Intranet de toohello de ponto final autenticação dispositivo Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d360b-257">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="d360b-258">certificado tooavoid pede-lhe quando os utilizadores no registo de dispositivos autenticam tooAzure AD, pode emitir um Olá tooadd do política tooyour dispositivos associados a domínios seguir zona de Local Intranet toohello URL no Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="d360b-258">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="d360b-259">Passo 4: Implementação de controlo e implementação</span><span class="sxs-lookup"><span data-stu-id="d360b-259">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="d360b-260">Quando tiver concluído os passos de Olá necessário, dispositivos associados a domínios são tooautomatically pronto a associação do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="d360b-260">When you have completed hello required steps, domain-joined devices are ready tooautomatically join Azure AD:</span></span>

- <span data-ttu-id="d360b-261">Dispositivos de todos os associados a um domínio que executam o Windows 10 aniversário da atualização e o Windows Server 2016 automaticamente registar com o Azure AD no dispositivo reinicie ou sessão do utilizador.</span><span class="sxs-lookup"><span data-stu-id="d360b-261">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> 

- <span data-ttu-id="d360b-262">Novos dispositivos registar com o Azure AD quando o dispositivo de Olá for reiniciado depois de concluída a operação de associação de domínio Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-262">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

- <span data-ttu-id="d360b-263">Dispositivos que foram anteriormente do Azure AD registado (por exemplo, para o Intune) transição demasiado "*associados a um domínio, registado no AAD*"; no entanto demora algum tempo para que este processo toocomplete em todos os dispositivos que devem estar toohello fluxo normal de atividade de utilizador e domínio.</span><span class="sxs-lookup"><span data-stu-id="d360b-263">Devices that were previously Azure AD registered (for example, for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="d360b-264">Observações</span><span class="sxs-lookup"><span data-stu-id="d360b-264">Remarks</span></span>

- <span data-ttu-id="d360b-265">Pode utilizar uma implementação de política de grupo do Olá ao toocontrol objeto de registo automática do Windows 10 e computadores associados a domínios do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d360b-265">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="d360b-266">Windows 10 de Novembro de 2015 Update automaticamente associa com o Azure AD **apenas** se o objeto de política de grupo de implementação de Olá está definido.</span><span class="sxs-lookup"><span data-stu-id="d360b-266">Windows 10 November 2015 Update automatically joins with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="d360b-267">toorollout de computadores de nível inferior do Windows, pode implementar um [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que selecionar.</span><span class="sxs-lookup"><span data-stu-id="d360b-267">toorollout of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="d360b-268">Se push dispositivos de associados a um domínio de tooWindows 8.1 objeto de política de grupo do Olá, é tentada uma associação; No entanto, é recomendado que utilize Olá [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toojoin todos os dispositivos de nível inferior do Windows.</span><span class="sxs-lookup"><span data-stu-id="d360b-268">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, a join is attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toojoin all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="d360b-269">Criar um objeto de política de grupo</span><span class="sxs-lookup"><span data-stu-id="d360b-269">Create a Group Policy object</span></span> 

<span data-ttu-id="d360b-270">implementação de Olá toocontrol de computadores atuais do Windows, deve implementar Olá **registar computadores associados a um domínio como dispositivos** dispositivos toohello objeto de política de grupo que pretende tooregister.</span><span class="sxs-lookup"><span data-stu-id="d360b-270">toocontrol hello rollout of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="d360b-271">Por exemplo, pode implementar o grupo de segurança de tooa ou unidade organizacional do Olá política tooan.</span><span class="sxs-lookup"><span data-stu-id="d360b-271">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="d360b-272">**política de Olá tooset:**</span><span class="sxs-lookup"><span data-stu-id="d360b-272">**tooset hello policy:**</span></span>

1. <span data-ttu-id="d360b-273">Abra **Gestor de servidor**e, em seguida, aceda demasiado`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="d360b-273">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="d360b-274">Visite o nó de domínio toohello que corresponde ao domínio toohello onde pretende que o registo automático tooactivate de computadores atuais do Windows.</span><span class="sxs-lookup"><span data-stu-id="d360b-274">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="d360b-275">Clique com botão direito **objetos de política de grupo**e, em seguida, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="d360b-275">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="d360b-276">Escreva um nome para o objeto de política de grupo.</span><span class="sxs-lookup"><span data-stu-id="d360b-276">Type a name for your Group Policy object.</span></span> <span data-ttu-id="d360b-277">Por exemplo, * associação do Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="d360b-277">For example, *Hybrid Azure AD join.</span></span> 
5. <span data-ttu-id="d360b-278">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d360b-278">Click **OK**.</span></span>
6. <span data-ttu-id="d360b-279">Clique com o botão direito do novo objeto de política de grupo e, em seguida, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="d360b-279">Right-click your new Group Policy object, and then select **Edit**.</span></span>
7. <span data-ttu-id="d360b-280">Aceda demasiado**configuração do computador** > **políticas** > **modelos administrativos** > **Windows Componentes** > **registo de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="d360b-280">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> 
8. <span data-ttu-id="d360b-281">Clique com botão direito **registar computadores associados a um domínio como dispositivos**e, em seguida, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="d360b-281">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d360b-282">Este modelo de política de grupo foi alterado de versões anteriores da consola de gestão de políticas de grupo Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-282">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="d360b-283">Se estiver a utilizar uma versão anterior da consola de Olá, aceda demasiado`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="d360b-283">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="d360b-284">Selecione **ativado**e, em seguida, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="d360b-284">Select **Enabled**, and then click **Apply**.</span></span>
8. <span data-ttu-id="d360b-285">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d360b-285">Click **OK**.</span></span>
9. <span data-ttu-id="d360b-286">Olá ligação localização tooa de objeto de política de grupo à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="d360b-286">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="d360b-287">Por exemplo, pode ligar-tooa específico, unidade organizacional.</span><span class="sxs-lookup"><span data-stu-id="d360b-287">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="d360b-288">Também foi ligue-o grupo de segurança específicos tooa de computadores que associar automaticamente com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360b-288">You also could link it tooa specific security group of computers that automatically join with Azure AD.</span></span> <span data-ttu-id="d360b-289">tooset esta política para todos os computadores associados a domínios Windows 10 e Windows Server 2016 na sua organização, o domínio de toohello do objeto de política de grupo do ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-289">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="d360b-290">Pacotes do Windows Installer para computadores não - Windows 10</span><span class="sxs-lookup"><span data-stu-id="d360b-290">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="d360b-291">computadores de nível inferior toojoin associados a um domínio Windows num ambiente federado, pode transferir e instalar estas pacote do Windows Installer (. msi) do Centro de transferências em Olá [Microsoft Workplace Join para computadores Windows de 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)página.</span><span class="sxs-lookup"><span data-stu-id="d360b-291">toojoin domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="d360b-292">Pode implementar o pacote de Olá através da utilização de um sistema de distribuição de software, como o System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="d360b-292">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="d360b-293">Olá pacote suporta opções de instalação silenciosa padrão Olá com Olá *silenciosos* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d360b-293">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="d360b-294">System Center Configuration Manager Current Branch oferece vantagens adicionais de versões anteriores, como Olá capacidade tootrack concluída registos.</span><span class="sxs-lookup"><span data-stu-id="d360b-294">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="d360b-295">Para obter mais informações, consulte [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="d360b-295">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="d360b-296">Instalador de Olá cria uma tarefa agendada no sistema de Olá que é executado no contexto do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="d360b-296">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="d360b-297">tarefa de Olá é acionada quando o utilizador Olá inicia sessão tooWindows.</span><span class="sxs-lookup"><span data-stu-id="d360b-297">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="d360b-298">tarefas de Olá associa automaticamente dispositivos Olá com o Azure AD com as credenciais de utilizador Olá após a autenticação utilizando a autenticação integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="d360b-298">hello task silently joins hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="d360b-299">toosee Olá agendada a tarefa, de dispositivo Olá, aceda demasiado**Microsoft** > **Workplace Join**, e, em seguida, aceda a biblioteca do Programador de tarefas de toohello.</span><span class="sxs-lookup"><span data-stu-id="d360b-299">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-joined-devices"></a><span data-ttu-id="d360b-300">Passo 5: Verificar se a dispositivos associados</span><span class="sxs-lookup"><span data-stu-id="d360b-300">Step 5: Verify joined devices</span></span>

<span data-ttu-id="d360b-301">Pode verificar os dispositivos associados com êxito na sua organização utilizando Olá [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet no Olá [módulo Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="d360b-301">You can check successful joined devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="d360b-302">resultado Olá deste cmdlet mostra os dispositivos que são registados e associados com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d360b-302">hello output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="d360b-303">tooget todos os dispositivos, utilize Olá **-todos os** parâmetro e, em seguida, filtro-los utilizando Olá **deviceTrustType** propriedade.</span><span class="sxs-lookup"><span data-stu-id="d360b-303">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="d360b-304">Associado a um domínio dispositivos têm um valor de **associados a um domínio**.</span><span class="sxs-lookup"><span data-stu-id="d360b-304">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d360b-305">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d360b-305">Next steps</span></span>

* [<span data-ttu-id="d360b-306">Gestão de toodevice de introdução no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d360b-306">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
