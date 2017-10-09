---
title: "aaaHow tooconfigure o registo automático de dispositivos associados a um domínio do Windows com o Azure Active Directory | Microsoft Docs"
description: "Configure o tooregister de dispositivos Windows associados a um domínio automática e silenciosa com o Azure Active Directory."
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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="93d09-103">Como tooconfigure o registo automático do Windows associados a um domínio dispositivos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93d09-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="93d09-104">toouse [acesso condicional de baseado nos dispositivos do Azure Active Directory](active-directory-conditional-access-azure-portal.md), os computadores têm de estar registados no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93d09-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="93d09-105">Pode obter uma lista de dispositivos registados na sua organização utilizando Olá [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet no Olá [módulo Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="93d09-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="93d09-106">Este artigo fornece os passos de Olá para configurar o registo automático Olá de dispositivos associados a um domínio do Windows com o Azure AD na sua organização.</span><span class="sxs-lookup"><span data-stu-id="93d09-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="93d09-107">Para obter mais informações sobre:</span><span class="sxs-lookup"><span data-stu-id="93d09-107">For more information about:</span></span>

- <span data-ttu-id="93d09-108">Acesso condicional, consulte [acesso condicional de baseado nos dispositivos do Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="93d09-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="93d09-109">Dispositivos Windows 10 na área de trabalho Olá e experiências Olá melhorada quando registado com o Azure AD, consulte [Windows 10 para empresa Olá: utilizar dispositivos de trabalho](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93d09-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="93d09-110">Windows 10 Enterprise E3 no CSP, consulte Olá [Windows 10 Enterprise E3 na descrição geral de CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="93d09-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="93d09-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="93d09-111">Before you begin</span></span>

<span data-ttu-id="93d09-112">Antes de começar a configurar o registo automático Olá de dispositivos associados a um domínio do Windows no seu ambiente, deve familiarizá-lo com restrições de Olá e cenários de Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="93d09-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="93d09-113">tooimprove Olá facilitar a leitura de descrições de Olá, este tópico utiliza Olá termo os seguintes:</span><span class="sxs-lookup"><span data-stu-id="93d09-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="93d09-114">**Dispositivos atuais do Windows** -este prazo refere-se associados a um toodomain dispositivos com Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="93d09-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="93d09-115">**Dispositivos de nível inferior do Windows** -este prazo refere-se tooall **suportado** dispositivos Windows associados a um domínio, que estão em execução Windows 10 nem do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="93d09-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="93d09-116">Dispositivos atuais do Windows</span><span class="sxs-lookup"><span data-stu-id="93d09-116">Windows current devices</span></span>

- <span data-ttu-id="93d09-117">Para dispositivos com o sistema operativo da ambiente de trabalho de Windows hello, recomendamos que utilize o Windows 10 aniversário da atualização (versão 1607) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="93d09-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="93d09-118">Olá, registo de dispositivos atuais do Windows **é** suportada em ambientes não federada, tais como configurações de sincronização de hash de palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="93d09-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="93d09-119">Dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="93d09-119">Windows down-level devices</span></span>

- <span data-ttu-id="93d09-120">Olá seguintes dispositivos de nível inferior do Windows é suportada:</span><span class="sxs-lookup"><span data-stu-id="93d09-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="93d09-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="93d09-121">Windows 8.1</span></span>
    - <span data-ttu-id="93d09-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="93d09-122">Windows 7</span></span>
    - <span data-ttu-id="93d09-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="93d09-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="93d09-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="93d09-124">Windows Server 2012</span></span>
    - <span data-ttu-id="93d09-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="93d09-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="93d09-126">Olá, registo de dispositivos de nível inferior do Windows **é** suportada em ambientes não federada através de totalmente integrada de sessão único [do Azure Active Directory totalmente integrada Single Sign-On](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="93d09-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="93d09-127">Olá, registo de dispositivos de nível inferior do Windows **não é** suportados para dispositivos com perfis itinerantes.</span><span class="sxs-lookup"><span data-stu-id="93d09-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="93d09-128">Se estiver a depender de perfis ou definições de roaming, utilize o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="93d09-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="93d09-129">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="93d09-129">Prerequisites</span></span>

<span data-ttu-id="93d09-130">Antes de iniciar a ativação Olá-registo automático de dispositivos associados a um domínio na sua organização, terá de toomake certificar-se de que está a executar uma versão atualizada do Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="93d09-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="93d09-131">Do Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="93d09-131">Azure AD Connect:</span></span>

- <span data-ttu-id="93d09-132">Mantém a associação de Olá entre a conta de computador Olá no objeto de dispositivo Olá no Azure AD e no local do Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="93d09-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="93d09-133">Permite que outros dispositivos relacionados com funcionalidades como o Windows Hello para empresas.</span><span class="sxs-lookup"><span data-stu-id="93d09-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="93d09-134">Passos de configuração</span><span class="sxs-lookup"><span data-stu-id="93d09-134">Configuration steps</span></span>

<span data-ttu-id="93d09-135">Este tópico inclui os passos de Olá necessário para todos os cenários de configuração típica.</span><span class="sxs-lookup"><span data-stu-id="93d09-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="93d09-136">Utilize Olá tabela tooget uma descrição geral dos passos de Olá que são necessários para o seu cenário a seguir:</span><span class="sxs-lookup"><span data-stu-id="93d09-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="93d09-137">Passos</span><span class="sxs-lookup"><span data-stu-id="93d09-137">Steps</span></span>                                      | <span data-ttu-id="93d09-138">Sincronização de hash de atual e a palavra-passe do Windows</span><span class="sxs-lookup"><span data-stu-id="93d09-138">Windows current and password hash sync</span></span> | <span data-ttu-id="93d09-139">Atual do Windows e a Federação</span><span class="sxs-lookup"><span data-stu-id="93d09-139">Windows current and federation</span></span> | <span data-ttu-id="93d09-140">Windows de nível inferior</span><span class="sxs-lookup"><span data-stu-id="93d09-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="93d09-141">Passo 1: Configurar o ponto de ligação de serviço</span><span class="sxs-lookup"><span data-stu-id="93d09-141">Step 1: Configure service connection point</span></span> | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |
| <span data-ttu-id="93d09-145">Passo 2: Configurar a emissão de afirmações</span><span class="sxs-lookup"><span data-stu-id="93d09-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Marcar][1]                    | ![Marcar][1]        |
| <span data-ttu-id="93d09-148">Passo 3: Ativar dispositivos não Windows 10</span><span class="sxs-lookup"><span data-stu-id="93d09-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Marcar][1]        |
| <span data-ttu-id="93d09-150">Passo 4: Implementação de controlo e implementação</span><span class="sxs-lookup"><span data-stu-id="93d09-150">Step 4: Control deployment and rollout</span></span>     | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |
| <span data-ttu-id="93d09-154">Passo 5: Verificar se a dispositivos registados</span><span class="sxs-lookup"><span data-stu-id="93d09-154">Step 5: Verify registered devices</span></span>          | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="93d09-158">Passo 1: Configurar o ponto de ligação de serviço</span><span class="sxs-lookup"><span data-stu-id="93d09-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="93d09-159">objeto de (SCP) do ponto de ligação de serviço Olá é utilizado pelos seus dispositivos durante Olá registo toodiscover informações de inquilino do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93d09-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="93d09-160">No local no Active Directory (AD), objeto de SCP Olá para Olá-registo automático de dispositivos associados a um domínio tem de existir na partição de contexto de nomenclatura de configuração do Olá da floresta do computador Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="93d09-161">Não há apenas um contexto de nomenclatura de configuração por floresta.</span><span class="sxs-lookup"><span data-stu-id="93d09-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="93d09-162">Numa configuração várias floresta do Active Directory, tem de existir ponto de ligação de serviço Olá em todas as florestas que contêm os computadores associados a um domínio.</span><span class="sxs-lookup"><span data-stu-id="93d09-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="93d09-163">Pode utilizar Olá [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Olá contexto nomenclatura de configuração da sua floresta.</span><span class="sxs-lookup"><span data-stu-id="93d09-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="93d09-164">Para uma floresta com o nome de domínio do Active Directory Olá *fabrikam.com*, contexto de nomenclatura de configuração de Olá é:</span><span class="sxs-lookup"><span data-stu-id="93d09-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="93d09-165">Na sua floresta, o objeto de Olá SCP para Olá-registo automático de dispositivos associados a um domínio está localizado em:</span><span class="sxs-lookup"><span data-stu-id="93d09-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="93d09-166">Dependendo de como tiver implementado o Azure AD Connect, objeto de SCP Olá poderá já tiverem sido configurado.</span><span class="sxs-lookup"><span data-stu-id="93d09-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="93d09-167">Pode verificar a existência de Olá do objeto de Olá e obter valores de deteção de Olá utilizando Olá seguinte script do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="93d09-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="93d09-168">Olá **$scp. As palavras-chave** saída mostra informações de inquilino do Azure AD de Olá, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="93d09-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="93d09-169">Se o ponto de ligação de serviço Olá não existir, pode criá-la executando Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet no seu servidor do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="93d09-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="93d09-170">Credencial de administrador de empresa é necessário toorun este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="93d09-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="93d09-171">Olá cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93d09-171">hello cmdlet:</span></span>

- <span data-ttu-id="93d09-172">Cria o ponto de ligação de serviço Olá na floresta do Active Directory Olá do Azure AD Connect está ligado.</span><span class="sxs-lookup"><span data-stu-id="93d09-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="93d09-173">Requer que toospecify Olá `AdConnectorAccount` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="93d09-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="93d09-174">Esta é a conta de Olá que está configurada como o Active Directory a conta do conector no Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="93d09-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="93d09-175">Olá script seguinte mostra um exemplo de utilização do cmdlet Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="93d09-176">Este script, `$aadAdminCred = Get-Credential` requer tootype um nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="93d09-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="93d09-177">Terá de nome de utilizador de Olá tooprovide no formato de nome principal (UPN) do utilizador Olá (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="93d09-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="93d09-178">Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="93d09-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="93d09-179">Utiliza o módulo PowerShell do Active Directory de Olá, que depende de serviços da Web do Active Directory em execução num controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="93d09-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="93d09-180">Serviços da Web do Active Directory é suportada em controladores de domínio com o Windows Server 2008 R2 e posterior.</span><span class="sxs-lookup"><span data-stu-id="93d09-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="93d09-181">Só é suportado pelo Olá **MSOnline PowerShell versão do módulo 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="93d09-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="93d09-182">toodownload este módulo, utilize esta opção [ligação](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="93d09-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="93d09-183">Para controladores de domínio a executar o Windows Server 2008 ou de versões anteriores, utilize o script de Olá abaixo o ponto de ligação de serviço toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="93d09-184">Numa configuração de várias floresta, deve utilizar Olá seguir o ponto de ligação do serviço do script toocreate Olá em cada floresta onde existem computadores:</span><span class="sxs-lookup"><span data-stu-id="93d09-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="93d09-185">Passo 2: Configurar a emissão de afirmações</span><span class="sxs-lookup"><span data-stu-id="93d09-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="93d09-186">No Azure federado configuração do AD, dispositivos dependem de serviços de Federação do Active Directory (AD FS) ou um terceiros 3rd no local tooAzure de tooauthenticate de serviço de Federação AD.</span><span class="sxs-lookup"><span data-stu-id="93d09-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="93d09-187">Dispositivos autenticar tooget um tooregister de token de acesso contra Olá Service do Azure Active Directory dispositivo registo (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="93d09-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="93d09-188">Windows dispositivos atuais autenticam utilizando a autenticação integrada do Windows tooan WS-Trust ponto final ativo (versões 1.3 ou 2005) alojado pelo serviço de Federação Olá no local.</span><span class="sxs-lookup"><span data-stu-id="93d09-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="93d09-189">Quando utilizar o AD FS, quer **adfs/services/confiança/13/windowstransport** ou **adfs/services/confiança/2005/windowstransport** tem de estar ativada.</span><span class="sxs-lookup"><span data-stu-id="93d09-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="93d09-190">Se estiver a utilizar Olá Proxy de autenticação da Web, certifique-se também que este ponto final está publicado através do proxy de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="93d09-191">Pode ver que os parâmetros são ativados através da consola de gestão de Olá do AD FS em **serviço > pontos finais**.</span><span class="sxs-lookup"><span data-stu-id="93d09-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="93d09-192">Se não tiver o AD FS como o serviço de Federação no local, siga instruções de Olá do seu toomake fornecedor se suportam 1.3 de WS-Trust ou pontos finais de 2005 e estes são publicadas através de Olá ficheiro de troca de metadados (MEX).</span><span class="sxs-lookup"><span data-stu-id="93d09-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="93d09-193">Olá seguintes afirmações têm de existir no token de Olá recebido pelo Azure DRS para toocomplete de registo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="93d09-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="93d09-194">Azure DRS irá criar um objeto de dispositivo no Azure AD com algumas destas informações que, em seguida, são utilizadas pelo objeto de dispositivo do Azure AD Connect tooassociate Olá recém-criado com Olá computador conta no local.</span><span class="sxs-lookup"><span data-stu-id="93d09-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="93d09-195">Se tiver mais do que um nome de domínio verificado, terá de Olá tooprovide afirmação para computadores a seguir:</span><span class="sxs-lookup"><span data-stu-id="93d09-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="93d09-196">Se já estiver a emitir uma afirmação de ImmutableID (por exemplo, o ID de início de sessão alternativo) terá tooprovide uma afirmação correspondente para computadores:</span><span class="sxs-lookup"><span data-stu-id="93d09-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="93d09-197">Olá secções a seguir, encontrará informações sobre:</span><span class="sxs-lookup"><span data-stu-id="93d09-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="93d09-198">valores de Olá cada afirmação deve ter</span><span class="sxs-lookup"><span data-stu-id="93d09-198">hello values each claim should have</span></span>
- <span data-ttu-id="93d09-199">Como uma definição deverá ter o seguinte aspeto no AD FS</span><span class="sxs-lookup"><span data-stu-id="93d09-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="93d09-200">definição de Olá ajuda-o a tooverify se valores Olá estão presentes ou se terá toocreate-los.</span><span class="sxs-lookup"><span data-stu-id="93d09-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="93d09-201">Se não utilizar o AD FS para o servidor de Federação no local, siga estas afirmações tooissue do seu fornecedor instruções toocreate Olá configuração apropriada.</span><span class="sxs-lookup"><span data-stu-id="93d09-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="93d09-202">Afirmações de tipo de conta do problema</span><span class="sxs-lookup"><span data-stu-id="93d09-202">Issue account type claim</span></span>

<span data-ttu-id="93d09-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Esta afirmação tem de conter um valor de **DJ**, que identifica o dispositivo de Olá como um computador associado ao domínio.</span><span class="sxs-lookup"><span data-stu-id="93d09-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="93d09-204">No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:</span><span class="sxs-lookup"><span data-stu-id="93d09-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="93d09-205">Emitir objectGUID de Olá computador conta no local</span><span class="sxs-lookup"><span data-stu-id="93d09-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="93d09-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Esta afirmação tem de conter Olá **objectGUID** valor Olá no local a conta de computador.</span><span class="sxs-lookup"><span data-stu-id="93d09-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="93d09-207">No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:</span><span class="sxs-lookup"><span data-stu-id="93d09-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="93d09-208">Emitir Sidobjeto de Olá computador conta no local</span><span class="sxs-lookup"><span data-stu-id="93d09-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="93d09-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Esta afirmação tem de conter Olá Olá **Sidobjeto** valor Olá no local a conta de computador.</span><span class="sxs-lookup"><span data-stu-id="93d09-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="93d09-210">No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:</span><span class="sxs-lookup"><span data-stu-id="93d09-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="93d09-211">Emitir issuerID para computador quando múltiplos verificar nomes de domínio no Azure AD</span><span class="sxs-lookup"><span data-stu-id="93d09-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="93d09-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Esta afirmação tem de conter Olá identificador de recurso uniforme (URI) de qualquer um dos Olá verificar nomes de domínio que se ligam com Olá no local token de Olá de emissora de serviço (AD FS ou terceiros 3rd) de Federação.</span><span class="sxs-lookup"><span data-stu-id="93d09-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="93d09-213">No AD FS, pode adicionar regras de transformação de emissão que parece ser Olá aqueles abaixo nessa ordem específica após Olá aqueles acima.</span><span class="sxs-lookup"><span data-stu-id="93d09-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="93d09-214">Tenha em atenção que um tooexplicitly problema Olá regra para os utilizadores é necessário.</span><span class="sxs-lookup"><span data-stu-id="93d09-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="93d09-215">Em regras de Olá abaixo, é adicionada uma regra primeiro identificar utilizador vs. a autenticação de computador.</span><span class="sxs-lookup"><span data-stu-id="93d09-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

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


<span data-ttu-id="93d09-216">Na afirmação Olá acima,</span><span class="sxs-lookup"><span data-stu-id="93d09-216">In hello claim above,</span></span>

- <span data-ttu-id="93d09-217">`$<domain>`é o URL do serviço Olá AD FS</span><span class="sxs-lookup"><span data-stu-id="93d09-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="93d09-218">`<verified-domain-name>`é um marcador de posição terá tooreplace com um dos seus nomes de domínio verificado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="93d09-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="93d09-219">Para obter mais detalhes sobre os nomes de domínio verificado, consulte [adicionar um tooAzure de nome de domínio personalizado do Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="93d09-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="93d09-220">tooget uma lista dos seus domínios verificados da empresa, pode utilizar Olá [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="93d09-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="93d09-222">Emitir ImmutableID para computador quando existe uma para os utilizadores (por exemplo, início de sessão alternativo ID está definido)</span><span class="sxs-lookup"><span data-stu-id="93d09-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="93d09-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Esta afirmação tem de conter um valor válido para computadores.</span><span class="sxs-lookup"><span data-stu-id="93d09-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="93d09-224">No AD FS, pode criar uma regra de transformação de emissão da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="93d09-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="93d09-225">Programa auxiliar script toocreate Olá AD FS transformação regras de emissão</span><span class="sxs-lookup"><span data-stu-id="93d09-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="93d09-226">Olá seguinte script ajuda-o com a criação de emissão de Olá Olá descritas acima de regras de transformação.</span><span class="sxs-lookup"><span data-stu-id="93d09-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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

### <a name="remarks"></a><span data-ttu-id="93d09-227">Observações</span><span class="sxs-lookup"><span data-stu-id="93d09-227">Remarks</span></span> 

- <span data-ttu-id="93d09-228">Este script acrescenta regras existentes do Olá regras toohello.</span><span class="sxs-lookup"><span data-stu-id="93d09-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="93d09-229">Não execute scripts de Olá duas vezes porque Olá conjunto de regras seriam adicionado duas vezes.</span><span class="sxs-lookup"><span data-stu-id="93d09-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="93d09-230">Certifique-se de que nenhum correspondentes existem regras para estas afirmações (em condições de correspondente Olá) antes de executar o script de Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="93d09-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="93d09-231">Se tiver vários verificado nomes de domínio (conforme ilustrado no portal do Azure AD de Olá ou através do cmdlet Olá Get MsolDomains), defina o valor de Olá de **$multipleVerifiedDomainNames** no Olá script demasiado**$true**.</span><span class="sxs-lookup"><span data-stu-id="93d09-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="93d09-232">Certifique-se também que remova qualquer afirmação issuerid existente que poderá ter sido criada pelo Azure AD Connect ou através de outros meios.</span><span class="sxs-lookup"><span data-stu-id="93d09-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="93d09-233">Eis um exemplo para esta regra:</span><span class="sxs-lookup"><span data-stu-id="93d09-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="93d09-234">Se já ter emitido uma **ImmutableID** de afirmação para contas de utilizador, defina o valor de Olá de **$immutableIDAlreadyIssuedforUsers** no Olá script demasiado**$true**.</span><span class="sxs-lookup"><span data-stu-id="93d09-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="93d09-235">Passo 3: Ativar os dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="93d09-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="93d09-236">Se alguns dos seus dispositivos associados a um domínio Windows nível dispositivos, tem de:</span><span class="sxs-lookup"><span data-stu-id="93d09-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="93d09-237">Defina uma política no Azure AD tooenable dispositivos tooregister de utilizadores.</span><span class="sxs-lookup"><span data-stu-id="93d09-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="93d09-238">Configurar o seu local Federação serviço tooissue afirmações toosupport **autenticação integrada de Windows (IWA)** para registo de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="93d09-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="93d09-239">Adicione Olá do Azure AD dispositivos autenticação ponto final toohello Intranet zonas locais tooavoid certificado solicita ao autenticar o dispositivo de Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="93d09-240">Definir a política no Azure AD tooenable dispositivos tooregister de utilizadores</span><span class="sxs-lookup"><span data-stu-id="93d09-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="93d09-241">dispositivos de nível inferior do tooregister Windows, terá de toomake se esse Olá definição tooallow utilizadores tooregister dispositivos no Azure AD está definido.</span><span class="sxs-lookup"><span data-stu-id="93d09-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="93d09-242">No portal do Azure Olá, pode encontrar esta definição em:</span><span class="sxs-lookup"><span data-stu-id="93d09-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="93d09-243">Olá política seguinte tem de ser definida demasiado**todos os**: **os utilizadores podem registar os seus dispositivos com o Azure AD**</span><span class="sxs-lookup"><span data-stu-id="93d09-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Registar dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="93d09-245">Configurar o serviço de Federação no local</span><span class="sxs-lookup"><span data-stu-id="93d09-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="93d09-246">O serviço de Federação no local tem de suportar Olá emissora **authenticationmehod** e **wiaormultiauthn** afirmações ao receber uma autenticação pedem toohello do Azure AD da entidade confiadora, que contém um resouce_params parâmetro com um valor de codificação como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="93d09-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="93d09-247">Quando é fornecido este pedido, serviço de Federação no local Olá utilizador Olá utilizando a autenticação integrada do Windows tem de ser autenticado e após com êxito, este tem de emitir Olá seguintes duas afirmações:</span><span class="sxs-lookup"><span data-stu-id="93d09-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="93d09-248">No AD FS, tem de adicionar uma regra de transformação de emissão que método de autenticação através de transmite Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="93d09-249">**tooadd esta regra:**</span><span class="sxs-lookup"><span data-stu-id="93d09-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="93d09-250">Na consola de gestão do Olá AD FS, aceda demasiado`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="93d09-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="93d09-251">Objetos de confiança das entidades confiadoras do Olá plataforma de identidade do Microsoft Office 365 com o botão direito e, em seguida, selecione **editar regras de afirmação**.</span><span class="sxs-lookup"><span data-stu-id="93d09-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="93d09-252">No Olá **regras de transformação de emissão** separador, selecione **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="93d09-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="93d09-253">No Olá **regra de afirmação** lista de modelo, selecione **enviar afirmações utilizando uma regra personalizada**.</span><span class="sxs-lookup"><span data-stu-id="93d09-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="93d09-254">Selecione **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="93d09-254">Select **Next**.</span></span>
6. <span data-ttu-id="93d09-255">No Olá **nome da regra de afirmação** caixa, escreva **regra de afirmação de método de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="93d09-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="93d09-256">No Olá **regra de afirmação** caixa, Olá tipo seguinte regra:</span><span class="sxs-lookup"><span data-stu-id="93d09-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="93d09-257">No servidor de Federação, escreva o comando do PowerShell Olá abaixo depois de substituir  **\<RPObjectName\>**  com Olá entidade confiadora terceiros nome do objeto para os objetos de confiança das entidades confiadoras do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93d09-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="93d09-258">Este objeto é normalmente denominado **plataforma de identidade do Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="93d09-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="93d09-259">Adicionar zonas de Local Intranet de toohello de ponto final autenticação dispositivo Olá do Azure AD</span><span class="sxs-lookup"><span data-stu-id="93d09-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="93d09-260">certificado tooavoid pede-lhe quando os utilizadores no registo de dispositivos autenticam tooAzure AD, pode emitir um Olá tooadd do política tooyour dispositivos associados a domínios seguir zona de Local Intranet toohello URL no Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="93d09-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="93d09-261">Passo 4: Implementação de controlo e implementação</span><span class="sxs-lookup"><span data-stu-id="93d09-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="93d09-262">Quando tiver concluído os passos de Olá necessário, dispositivos associados a domínios são tooautomatically pronto registar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93d09-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="93d09-263">Dispositivos de todos os associados a um domínio que executam o Windows 10 aniversário da atualização e o Windows Server 2016 automaticamente registar com o Azure AD no dispositivo reinicie ou sessão do utilizador.</span><span class="sxs-lookup"><span data-stu-id="93d09-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="93d09-264">Novos dispositivos registar com o Azure AD quando o dispositivo de Olá for reiniciado depois de concluída a operação de associação de domínio Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="93d09-265">Dispositivos que foram anteriormente associado à área de trabalho tooAzure AD (por exemplo para o Intune) transição demasiado"*associados a um domínio, registado no AAD*"; no entanto demora algum tempo para que este processo toocomplete em todos os dispositivos que devem estar toohello normal fluxo de atividade de utilizador e domínio.</span><span class="sxs-lookup"><span data-stu-id="93d09-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="93d09-266">Observações</span><span class="sxs-lookup"><span data-stu-id="93d09-266">Remarks</span></span>

- <span data-ttu-id="93d09-267">Pode utilizar uma implementação de política de grupo do Olá ao toocontrol objeto de registo automática do Windows 10 e computadores associados a domínios do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="93d09-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="93d09-268">Windows 10 de Novembro de 2015 atualizar automaticamente regista com o Azure AD **apenas** se o objeto de política de grupo de implementação de Olá está definido.</span><span class="sxs-lookup"><span data-stu-id="93d09-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="93d09-269">toorollout Olá o registo automático de computadores de nível inferior do Windows, pode implementar um [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que selecionar.</span><span class="sxs-lookup"><span data-stu-id="93d09-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="93d09-270">Se push dispositivos de associados a um domínio de tooWindows 8.1 objeto de política de grupo do Olá, será tentado a registo; No entanto, é recomendado que utilize Olá [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) tooregister todos os dispositivos de nível inferior do Windows.</span><span class="sxs-lookup"><span data-stu-id="93d09-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="93d09-271">Criar um objeto de política de grupo</span><span class="sxs-lookup"><span data-stu-id="93d09-271">Create a Group Policy object</span></span> 

<span data-ttu-id="93d09-272">implementação de Olá toocontrol de registo automática de computadores atuais do Windows, deve implementar Olá **registar computadores associados a um domínio como dispositivos** dispositivos toohello objeto de política de grupo que pretende tooregister.</span><span class="sxs-lookup"><span data-stu-id="93d09-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="93d09-273">Por exemplo, pode implementar o grupo de segurança de tooa ou unidade organizacional do Olá política tooan.</span><span class="sxs-lookup"><span data-stu-id="93d09-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="93d09-274">**política de Olá tooset:**</span><span class="sxs-lookup"><span data-stu-id="93d09-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="93d09-275">Abra **Gestor de servidor**e, em seguida, aceda demasiado`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="93d09-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="93d09-276">Visite o nó de domínio toohello que corresponde ao domínio toohello onde pretende que o registo automático tooactivate de computadores atuais do Windows.</span><span class="sxs-lookup"><span data-stu-id="93d09-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="93d09-277">Clique com botão direito **objetos de política de grupo**e, em seguida, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="93d09-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="93d09-278">Escreva um nome para o objeto de política de grupo.</span><span class="sxs-lookup"><span data-stu-id="93d09-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="93d09-279">Por exemplo, *o registo automático tooAzure AD*.</span><span class="sxs-lookup"><span data-stu-id="93d09-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="93d09-280">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="93d09-280">Select **OK**.</span></span>
5. <span data-ttu-id="93d09-281">Clique com o botão direito do novo objeto de política de grupo e, em seguida, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="93d09-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="93d09-282">Aceda demasiado**configuração do computador** > **políticas** > **modelos administrativos** > **Windows Componentes** > **registo de dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="93d09-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="93d09-283">Clique com botão direito **registar computadores associados a um domínio como dispositivos**e, em seguida, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="93d09-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="93d09-284">Este modelo de política de grupo foi alterado de versões anteriores da consola de gestão de políticas de grupo Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="93d09-285">Se estiver a utilizar uma versão anterior da consola de Olá, aceda demasiado`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="93d09-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="93d09-286">Selecione **ativado**e, em seguida, selecione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="93d09-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="93d09-287">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="93d09-287">Select **OK**.</span></span>
9. <span data-ttu-id="93d09-288">Olá ligação localização tooa de objeto de política de grupo à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="93d09-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="93d09-289">Por exemplo, pode ligar-tooa específico, unidade organizacional.</span><span class="sxs-lookup"><span data-stu-id="93d09-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="93d09-290">Também foi ligue-o grupo de segurança específicos tooa de computadores que registar automaticamente com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93d09-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="93d09-291">tooset esta política para todos os computadores associados a domínios Windows 10 e Windows Server 2016 na sua organização, o domínio de toohello do objeto de política de grupo do ligação Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="93d09-292">Pacotes do Windows Installer para computadores não - Windows 10</span><span class="sxs-lookup"><span data-stu-id="93d09-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="93d09-293">computadores de nível inferior tooregister associados a um domínio Windows num ambiente federado, pode transferir e instalar estas pacote do Windows Installer (. msi) do Centro de transferências em Olá [Microsoft Workplace Join para computadores Windows de 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554) página.</span><span class="sxs-lookup"><span data-stu-id="93d09-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="93d09-294">Pode implementar o pacote de Olá através da utilização de um sistema de distribuição de software, como o System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="93d09-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="93d09-295">Olá pacote suporta opções de instalação silenciosa padrão Olá com Olá *silenciosos* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="93d09-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="93d09-296">System Center Configuration Manager Current Branch oferece vantagens adicionais de versões anteriores, como Olá capacidade tootrack concluída registos.</span><span class="sxs-lookup"><span data-stu-id="93d09-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="93d09-297">Para obter mais informações, consulte [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="93d09-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="93d09-298">Instalador de Olá cria uma tarefa agendada no sistema de Olá que é executado no contexto do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="93d09-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="93d09-299">tarefa de Olá é acionada quando o utilizador Olá inicia sessão tooWindows.</span><span class="sxs-lookup"><span data-stu-id="93d09-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="93d09-300">tarefa de Olá regista automaticamente o dispositivo de Olá com o Azure AD com as credenciais de utilizador Olá após a autenticação utilizando a autenticação integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="93d09-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="93d09-301">toosee Olá agendada a tarefa, de dispositivo Olá, aceda demasiado**Microsoft** > **Workplace Join**, e, em seguida, aceda a biblioteca do Programador de tarefas de toohello.</span><span class="sxs-lookup"><span data-stu-id="93d09-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="93d09-302">Passo 5: Verificar se a dispositivos registados</span><span class="sxs-lookup"><span data-stu-id="93d09-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="93d09-303">Pode verificar a dispositivos registados com êxito na sua organização utilizando Olá [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet no Olá [módulo Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="93d09-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="93d09-304">saída de Olá deste cmdlet mostra dispositivos registados no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93d09-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="93d09-305">tooget todos os dispositivos, utilize Olá **-todos os** parâmetro e, em seguida, filtro-los utilizando Olá **deviceTrustType** propriedade.</span><span class="sxs-lookup"><span data-stu-id="93d09-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="93d09-306">Associado a um domínio dispositivos têm um valor de **associados a um domínio**.</span><span class="sxs-lookup"><span data-stu-id="93d09-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93d09-307">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="93d09-307">Next steps</span></span>

* [<span data-ttu-id="93d09-308">Registo de dispositivos automático FAQ</span><span class="sxs-lookup"><span data-stu-id="93d09-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="93d09-309">Resolução de problemas de registo automático de domínio associados a computadores tooAzure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="93d09-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="93d09-310">Resolução de problemas de registo automático de domínio associados a computadores tooAzure AD – não do Windows 10</span><span class="sxs-lookup"><span data-stu-id="93d09-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="93d09-311">Acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93d09-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
