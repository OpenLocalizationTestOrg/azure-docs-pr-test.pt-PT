---
title: "definições do grupo aaaConfigure utilizando cmdlets do Azure Active Directory | Microsoft Docs"
description: "Como gerir as definições de Olá de grupos utilizando cmdlets do Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="f2563-103">Cmdlets do Azure Active Directory para configurar definições de grupo</span><span class="sxs-lookup"><span data-stu-id="f2563-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2563-104">Este conteúdo aplica-se apenas tooOffice 365 grupos.</span><span class="sxs-lookup"><span data-stu-id="f2563-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="f2563-105">Para obter mais informações sobre como definir grupos de segurança do tooallow utilizadores toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` conforme descrito em [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="f2563-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="f2563-106">Definições de grupos do Office 365 são configuradas utilizando um objeto de definições e um objeto de SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="f2563-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="f2563-107">Inicialmente, não vir quaisquer objetos de definições no seu diretório, porque o diretório está configurado com predefinições Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="f2563-108">as definições predefinidas do toochange Olá, tem de criar um novo objeto de definições através de um modelo de definições.</span><span class="sxs-lookup"><span data-stu-id="f2563-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="f2563-109">Modelos de definições são definidos pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f2563-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="f2563-110">Existem vários modelos diferentes definições.</span><span class="sxs-lookup"><span data-stu-id="f2563-110">There are several different settings templates.</span></span> <span data-ttu-id="f2563-111">definições do grupo tooconfigure do Office 365 para o seu diretório, utilizar o modelo de Olá com o nome "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="f2563-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="f2563-112">definições do grupo tooconfigure do Office 365 num único grupo, utilize o modelo de Olá com o nome "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="f2563-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="f2563-113">Este modelo é o grupo de tooan do Office 365 de acesso de convidado de toomanage utilizados.</span><span class="sxs-lookup"><span data-stu-id="f2563-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="f2563-114">cmdlets de Olá fazem parte do módulo Olá do Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="f2563-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="f2563-115">Para obter instruções sobre como toodownload e módulo Olá de instalação no seu computador, consulte o artigo de Olá [do Azure Active Directory PowerShell versão 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="f2563-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="f2563-116">Pode instalar Olá versão 2 versão do módulo Olá de [galeria do PowerShell Olá](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="f2563-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="f2563-117">Obter um valor de definições específicas</span><span class="sxs-lookup"><span data-stu-id="f2563-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="f2563-118">Se souber o nome de Olá de Olá definição queira tooretrieve, pode utilizar Olá abaixo do valor de definições cmdlet tooretrieve Olá atual.</span><span class="sxs-lookup"><span data-stu-id="f2563-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="f2563-119">Neste exemplo, estamos a obter o valor de Olá para uma definição com o nome "UsageGuidelinesUrl."</span><span class="sxs-lookup"><span data-stu-id="f2563-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="f2563-120">Pode ler que mais sobre as definições do diretório e os respetivos nomes mais baixo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f2563-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="f2563-121">Criar as definições ao nível do diretório de Olá</span><span class="sxs-lookup"><span data-stu-id="f2563-121">Create settings at hello directory level</span></span>
<span data-ttu-id="f2563-122">Estes passos criar definições ao nível do diretório, que se aplicam a grupos do Office 365 tooall (Unified grupos) no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="f2563-123">Olá DirectorySettings cmdlets, tem de especificar ID Olá Olá SettingsTemplate pretende toouse.</span><span class="sxs-lookup"><span data-stu-id="f2563-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="f2563-124">Se não souber este ID, este cmdlet devolve a lista de Olá de todos os modelos de definições:</span><span class="sxs-lookup"><span data-stu-id="f2563-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="f2563-125">Esta chamada de cmdlet devolve todos os modelos que estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="f2563-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="f2563-126">tooadd um URL de orientação de utilização, primeiro tem de tooget Olá SettingsTemplate objeto que define o valor de URL de orientação de utilização de Olá; ou seja, Olá Group.Unified modelo:</span><span class="sxs-lookup"><span data-stu-id="f2563-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="f2563-127">Em seguida, crie um novo objeto de definições com base em que o modelo:</span><span class="sxs-lookup"><span data-stu-id="f2563-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="f2563-128">Em seguida, atualize o valor de orientação de utilização de Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="f2563-129">Por fim, aplicar definições de Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="f2563-130">Após a conclusão com êxito, o cmdlet Olá devolve Olá ID de objeto de definições novo Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="f2563-131">Seguem-se as definições de Olá definidas no Olá Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="f2563-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="f2563-132">**Definição**</span><span class="sxs-lookup"><span data-stu-id="f2563-132">**Setting**</span></span> | <span data-ttu-id="f2563-133">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f2563-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="f2563-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="f2563-134">EnableGroupCreation</span></span><li><span data-ttu-id="f2563-135">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="f2563-135">Type: Boolean</span></span><li><span data-ttu-id="f2563-136">Predefinição: VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="f2563-136">Default: True</span></span> |<span data-ttu-id="f2563-137">Sinalizador de Olá que indica se é permitida a criação do grupo unificado no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="f2563-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="f2563-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="f2563-139">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="f2563-139">Type: String</span></span><li><span data-ttu-id="f2563-140">Predefinição: ""</span><span class="sxs-lookup"><span data-stu-id="f2563-140">Default: “”</span></span> |<span data-ttu-id="f2563-141">GUID Olá do grupo de segurança para que Olá membros são permitidos toocreate Unified grupos mesmo quando EnableGroupCreation = = false.</span><span class="sxs-lookup"><span data-stu-id="f2563-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="f2563-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="f2563-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="f2563-143">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="f2563-143">Type: String</span></span><li><span data-ttu-id="f2563-144">Predefinição: ""</span><span class="sxs-lookup"><span data-stu-id="f2563-144">Default: “”</span></span> |<span data-ttu-id="f2563-145">Uma ligação toohello diretrizes de utilização do grupo.</span><span class="sxs-lookup"><span data-stu-id="f2563-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="f2563-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="f2563-146">ClassificationDescriptions</span></span><li><span data-ttu-id="f2563-147">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="f2563-147">Type: String</span></span><li><span data-ttu-id="f2563-148">Predefinição: ""</span><span class="sxs-lookup"><span data-stu-id="f2563-148">Default: “”</span></span> | <span data-ttu-id="f2563-149">Uma lista delimitada por vírgulas de descrições de classificação.</span><span class="sxs-lookup"><span data-stu-id="f2563-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="f2563-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="f2563-150">DefaultClassification</span></span><li><span data-ttu-id="f2563-151">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="f2563-151">Type: String</span></span><li><span data-ttu-id="f2563-152">Predefinição: ""</span><span class="sxs-lookup"><span data-stu-id="f2563-152">Default: “”</span></span> | <span data-ttu-id="f2563-153">classificação de Olá é toobe utilizado como classificação predefinida de Olá para um grupo, se foi especificado nenhum.</span><span class="sxs-lookup"><span data-stu-id="f2563-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="f2563-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="f2563-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="f2563-155">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="f2563-155">Type: String</span></span><li><span data-ttu-id="f2563-156">Predefinição: ""</span><span class="sxs-lookup"><span data-stu-id="f2563-156">Default: “”</span></span> |<span data-ttu-id="f2563-157">Ainda não implementada</span><span class="sxs-lookup"><span data-stu-id="f2563-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="f2563-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="f2563-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="f2563-159">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="f2563-159">Type: Boolean</span></span><li><span data-ttu-id="f2563-160">Predefinição: False</span><span class="sxs-lookup"><span data-stu-id="f2563-160">Default: False</span></span> | <span data-ttu-id="f2563-161">Valor boleano que indica se é ou não um utilizador convidado pode ser um proprietário de grupos.</span><span class="sxs-lookup"><span data-stu-id="f2563-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="f2563-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="f2563-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="f2563-163">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="f2563-163">Type: Boolean</span></span><li><span data-ttu-id="f2563-164">Predefinição: VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="f2563-164">Default: True</span></span> | <span data-ttu-id="f2563-165">Valor boleano que indica se é ou não um utilizador convidado pode ter conteúdo dos grupos de acesso tooUnified.</span><span class="sxs-lookup"><span data-stu-id="f2563-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="f2563-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="f2563-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="f2563-167">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="f2563-167">Type: String</span></span><li><span data-ttu-id="f2563-168">Predefinição: ""</span><span class="sxs-lookup"><span data-stu-id="f2563-168">Default: “”</span></span> | <span data-ttu-id="f2563-169">Olá url de um diretrizes de utilização de convidado de toohello de ligação.</span><span class="sxs-lookup"><span data-stu-id="f2563-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="f2563-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="f2563-170">AllowToAddGuests</span></span><li><span data-ttu-id="f2563-171">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="f2563-171">Type: Boolean</span></span><li><span data-ttu-id="f2563-172">Predefinição: VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="f2563-172">Default: True</span></span> | <span data-ttu-id="f2563-173">Um booleano que indica se é ou não é permitido tooadd convidados toothis diretório.</span><span class="sxs-lookup"><span data-stu-id="f2563-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="f2563-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="f2563-174">ClassificationList</span></span><li><span data-ttu-id="f2563-175">Tipo: Cadeia</span><span class="sxs-lookup"><span data-stu-id="f2563-175">Type: String</span></span><li><span data-ttu-id="f2563-176">Predefinição: ""</span><span class="sxs-lookup"><span data-stu-id="f2563-176">Default: “”</span></span> |<span data-ttu-id="f2563-177">Uma lista delimitada por vírgulas dos valores de classificação válido que podem ser aplicados tooUnified grupos.</span><span class="sxs-lookup"><span data-stu-id="f2563-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="f2563-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="f2563-178">EnableGroupCreation</span></span><li><span data-ttu-id="f2563-179">Tipo: booleano</span><span class="sxs-lookup"><span data-stu-id="f2563-179">Type: Boolean</span></span><li><span data-ttu-id="f2563-180">Predefinição: VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="f2563-180">Default: True</span></span> | <span data-ttu-id="f2563-181">Um valor boleano que indica se os utilizadores que não podem criar novos grupos de unificada.</span><span class="sxs-lookup"><span data-stu-id="f2563-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="f2563-182">Ler definições ao nível do diretório de Olá</span><span class="sxs-lookup"><span data-stu-id="f2563-182">Read settings at hello directory level</span></span>
<span data-ttu-id="f2563-183">Estes passos ler definições ao nível do diretório, que se aplicam a grupos do Office tooall no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="f2563-184">Ler todas as definições de diretório existente:</span><span class="sxs-lookup"><span data-stu-id="f2563-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="f2563-185">Este cmdlet devolve uma lista de todas as definições de diretório:</span><span class="sxs-lookup"><span data-stu-id="f2563-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="f2563-186">Ler todas as definições para um grupo específico:</span><span class="sxs-lookup"><span data-stu-id="f2563-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="f2563-187">Ler todos os valores de definições de diretório de um objeto de definições de diretório específico, utilizando o GUID de Id de definições:</span><span class="sxs-lookup"><span data-stu-id="f2563-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="f2563-188">Este cmdlet devolve valores e nomes de Olá este objeto de definições para este grupo específico:</span><span class="sxs-lookup"><span data-stu-id="f2563-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="f2563-189">Atualizar as definições de um grupo específico</span><span class="sxs-lookup"><span data-stu-id="f2563-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="f2563-190">Procurar o modelo de definições de Olá com o nome "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="f2563-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. <span data-ttu-id="f2563-191">Obter o objeto de modelo de Olá para o modelo de Groups.Unified.Guest Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="f2563-192">Crie um novo objeto de definições do modelo de Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="f2563-193">Defina Olá definição toohello necessário valor:</span><span class="sxs-lookup"><span data-stu-id="f2563-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="f2563-194">Crie nova definição de Olá para grupo necessário Olá no diretório de Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="f2563-195">Atualizar as definições ao nível do diretório de Olá</span><span class="sxs-lookup"><span data-stu-id="f2563-195">Update settings at hello directory level</span></span>

<span data-ttu-id="f2563-196">Estes passos atualizar as definições ao nível do diretório, que são aplicadas tooall Unified grupos no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="f2563-197">Estes exemplos assumem que já há um objeto de definições no seu diretório.</span><span class="sxs-lookup"><span data-stu-id="f2563-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="f2563-198">Encontrar o objeto de definições existente Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="f2563-199">Atualize o valor de Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="f2563-200">Atualize a definição de Olá:</span><span class="sxs-lookup"><span data-stu-id="f2563-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="f2563-201">Remova as definições ao nível do diretório de Olá</span><span class="sxs-lookup"><span data-stu-id="f2563-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="f2563-202">Este passo remove as definições ao nível do diretório, que se aplicam a grupos do Office tooall no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="f2563-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="f2563-203">Referência de sintaxe de cmdlet</span><span class="sxs-lookup"><span data-stu-id="f2563-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="f2563-204">Pode encontrar mais documentação do Azure Active Directory PowerShell em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="f2563-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="f2563-205">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="f2563-205">Additional reading</span></span>

* [<span data-ttu-id="f2563-206">Gerir o acesso tooresources com grupos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2563-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="f2563-207">Integrar as identidades no local ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2563-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
