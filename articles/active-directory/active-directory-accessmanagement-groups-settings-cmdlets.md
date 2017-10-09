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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Cmdlets do Azure Active Directory para configurar definições de grupo

> [!IMPORTANT]
> Este conteúdo aplica-se apenas tooOffice 365 grupos. Para obter mais informações sobre como definir grupos de segurança do tooallow utilizadores toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` conforme descrito em [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Definições de grupos do Office 365 são configuradas utilizando um objeto de definições e um objeto de SettingsTemplate. Inicialmente, não vir quaisquer objetos de definições no seu diretório, porque o diretório está configurado com predefinições Olá. as definições predefinidas do toochange Olá, tem de criar um novo objeto de definições através de um modelo de definições. Modelos de definições são definidos pela Microsoft. Existem vários modelos diferentes definições. definições do grupo tooconfigure do Office 365 para o seu diretório, utilizar o modelo de Olá com o nome "Group.Unified". definições do grupo tooconfigure do Office 365 num único grupo, utilize o modelo de Olá com o nome "Group.Unified.Guest". Este modelo é o grupo de tooan do Office 365 de acesso de convidado de toomanage utilizados. 

cmdlets de Olá fazem parte do módulo Olá do Azure Active Directory PowerShell V2. Para obter instruções sobre como toodownload e módulo Olá de instalação no seu computador, consulte o artigo de Olá [do Azure Active Directory PowerShell versão 2](https://docs.microsoft.com/powershell/azuread/). Pode instalar Olá versão 2 versão do módulo Olá de [galeria do PowerShell Olá](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Obter um valor de definições específicas
Se souber o nome de Olá de Olá definição queira tooretrieve, pode utilizar Olá abaixo do valor de definições cmdlet tooretrieve Olá atual. Neste exemplo, estamos a obter o valor de Olá para uma definição com o nome "UsageGuidelinesUrl." Pode ler que mais sobre as definições do diretório e os respetivos nomes mais baixo neste artigo.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Criar as definições ao nível do diretório de Olá
Estes passos criar definições ao nível do diretório, que se aplicam a grupos do Office 365 tooall (Unified grupos) no diretório de Olá.

1. Olá DirectorySettings cmdlets, tem de especificar ID Olá Olá SettingsTemplate pretende toouse. Se não souber este ID, este cmdlet devolve a lista de Olá de todos os modelos de definições:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  Esta chamada de cmdlet devolve todos os modelos que estão disponíveis:
  
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
2. tooadd um URL de orientação de utilização, primeiro tem de tooget Olá SettingsTemplate objeto que define o valor de URL de orientação de utilização de Olá; ou seja, Olá Group.Unified modelo:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Em seguida, crie um novo objeto de definições com base em que o modelo:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Em seguida, atualize o valor de orientação de utilização de Olá:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Por fim, aplicar definições de Olá:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

Após a conclusão com êxito, o cmdlet Olá devolve Olá ID de objeto de definições novo Olá:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Seguem-se as definições de Olá definidas no Olá Group.Unified SettingsTemplate.

| **Definição** | **Descrição** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Tipo: booleano<li>Predefinição: VERDADEIRO |Sinalizador de Olá que indica se é permitida a criação do grupo unificado no diretório de Olá. |
|  <ul><li>GroupCreationAllowedGroupId<li>Tipo: Cadeia<li>Predefinição: "" |GUID Olá do grupo de segurança para que Olá membros são permitidos toocreate Unified grupos mesmo quando EnableGroupCreation = = false. |
|  <ul><li>UsageGuidelinesUrl<li>Tipo: Cadeia<li>Predefinição: "" |Uma ligação toohello diretrizes de utilização do grupo. |
|  <ul><li>ClassificationDescriptions<li>Tipo: Cadeia<li>Predefinição: "" | Uma lista delimitada por vírgulas de descrições de classificação. |
|  <ul><li>DefaultClassification<li>Tipo: Cadeia<li>Predefinição: "" | classificação de Olá é toobe utilizado como classificação predefinida de Olá para um grupo, se foi especificado nenhum.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Tipo: Cadeia<li>Predefinição: "" |Ainda não implementada
|  <ul><li>AllowGuestsToBeGroupOwner<li>Tipo: booleano<li>Predefinição: False | Valor boleano que indica se é ou não um utilizador convidado pode ser um proprietário de grupos. |
|  <ul><li>AllowGuestsToAccessGroups<li>Tipo: booleano<li>Predefinição: VERDADEIRO | Valor boleano que indica se é ou não um utilizador convidado pode ter conteúdo dos grupos de acesso tooUnified. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Tipo: Cadeia<li>Predefinição: "" | Olá url de um diretrizes de utilização de convidado de toohello de ligação. |
|  <ul><li>AllowToAddGuests<li>Tipo: booleano<li>Predefinição: VERDADEIRO | Um booleano que indica se é ou não é permitido tooadd convidados toothis diretório.|
|  <ul><li>ClassificationList<li>Tipo: Cadeia<li>Predefinição: "" |Uma lista delimitada por vírgulas dos valores de classificação válido que podem ser aplicados tooUnified grupos. |
|  <ul><li>EnableGroupCreation<li>Tipo: booleano<li>Predefinição: VERDADEIRO | Um valor boleano que indica se os utilizadores que não podem criar novos grupos de unificada. |


## <a name="read-settings-at-hello-directory-level"></a>Ler definições ao nível do diretório de Olá
Estes passos ler definições ao nível do diretório, que se aplicam a grupos do Office tooall no diretório de Olá.

1. Ler todas as definições de diretório existente:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Este cmdlet devolve uma lista de todas as definições de diretório:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Ler todas as definições para um grupo específico:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Ler todos os valores de definições de diretório de um objeto de definições de diretório específico, utilizando o GUID de Id de definições:
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Este cmdlet devolve valores e nomes de Olá este objeto de definições para este grupo específico:
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

## <a name="update-settings-for-a-specific-group"></a>Atualizar as definições de um grupo específico

1. Procurar o modelo de definições de Olá com o nome "Groups.Unified.Guest"
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
2. Obter o objeto de modelo de Olá para o modelo de Groups.Unified.Guest Olá:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Crie um novo objeto de definições do modelo de Olá:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Defina Olá definição toohello necessário valor:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Crie nova definição de Olá para grupo necessário Olá no diretório de Olá:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Atualizar as definições ao nível do diretório de Olá

Estes passos atualizar as definições ao nível do diretório, que são aplicadas tooall Unified grupos no diretório de Olá. Estes exemplos assumem que já há um objeto de definições no seu diretório.

1. Encontrar o objeto de definições existente Olá:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Atualize o valor de Olá:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Atualize a definição de Olá:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Remova as definições ao nível do diretório de Olá
Este passo remove as definições ao nível do diretório, que se aplicam a grupos do Office tooall no diretório de Olá.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Referência de sintaxe de cmdlet
Pode encontrar mais documentação do Azure Active Directory PowerShell em [Cmdlets do Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Leitura adicional

* [Gerir o acesso tooresources com grupos do Azure Active Directory](active-directory-manage-groups.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)
