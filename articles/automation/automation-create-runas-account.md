---
title: "Criar contas Run As de Automatização do Azure | Microsoft Docs"
description: "Este artigo descreve como atualizar a sua conta de Automatização e criar contas Run As com o PowerShell ou a partir do portal."
services: automation
documentationcenter: 
author: georgewallace
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2017
ms.author: magoedte
ms.openlocfilehash: 74d363be48972b40ba6a50b845acea78e1b5cc20
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/10/2018
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a>Atualizar a autenticação da conta de Automatização com contas Run As 
Pode atualizar a sua conta de Automatização existente a partir do portal do Azure ou utilizar o PowerShell, se:

* Criar uma conta de Automatização, mas rejeitar criar a conta Run As.
* Já tiver uma conta de Automatização para gerir os recursos do Resource Manager e quer atualizá-la para incluir a conta Run As para autenticação de runbooks.
* Já tiver uma conta de automatização para gerir os recursos clássicos e quer atualizá-la para utilizar a Run As Clássica em vez de criar uma nova conta e migrar os runbooks e recursos para a mesma.   

O processo cria os seguintes itens na sua conta de Automatização.

**Para contas Run as:**

* Cria uma aplicação do Azure AD com um certificado autoassinado, cria uma conta de principal de serviço para a aplicação no Azure AD e atribui a função Contribuidor à conta na sua subscrição atual. Pode alterar esta definição para Proprietário ou qualquer outra função. Para obter mais informações, veja [Controlo de acesso baseado em funções na Automatização do Azure](automation-role-based-access-control.md).
* Cria um recurso de certificado da Automatização com o nome *AzureRunAsCertificate* na conta de Automatização especificada. O recurso do certificado contém a chave privada do certificado que a aplicação do Azure AD utiliza.
* Cria um recurso de ligação da Automatização com o nome *AzureRunAsConnection* na conta de Automatização especificada. O recurso de ligação contém o applicationId, o tenantId, o subscriptionId e o thumbprint do certificado.

**Para contas Run As Clássica:**

* Cria um recurso de certificado da Automatização com o nome *AzureClassicRunAsCertificate* na conta de Automatização especificada. O recurso do certificado contém a chave privada do certificado que o certificado de gestão utiliza.
* Cria um recurso de ligação da Automatização com o nome *AzureClassicRunAsConnection* na conta de Automatização especificada. O recurso de ligação contém o nome da subscrição, o subscriptionid e o nome de recurso do certificado.

## <a name="prerequisites"></a>Pré-requisitos
Se optar por [utilizar o PowerShell para criar as contas Run As](#create-run-as-account-using-powershell), este processo requer:

* O Windows 10 e Windows Server 2016 com os módulos do Azure Resource Manager 3.4.1 e posterior. O script do PowerShell não suporta versões anteriores do Windows.
* Azure PowerShell 1.0 e posterior. Para obter mais informações sobre a versão do PowerShell 1.0, veja [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Como instalar e configurar o Azure PowerShell).
* Uma conta de Automatização, que é referenciada como o valor para os parâmetros *–AutomationAccountName* e *-ApplicationDisplayName*.

Para obter os valores para *SubscriptionID*, *ResourceGroup* e *AutomationAccountName*, que são parâmetros necessários para o script, faça o seguinte:

1. No portal do Azure, clique em **Mais serviços**, que se encontra no canto inferior esquerdo. Na lista de recursos, escreva **Automatização**. À medida que começa a escrever, a lista filtra com base na sua entrada. Selecione **Contas de Automatização**.
2. Na página da conta de Automatização, selecione a sua conta de Automatização e, em **Definições da Conta** selecione **Propriedades**.  
3. Repare nos valores na página **Propriedades**.<br><br> ![O painel “Propriedades” da conta de Automatização](media/automation-create-runas-account/automation-account-properties.png)  

### <a name="required-permissions-to-update-your-automation-account"></a>Permissões necessárias para atualizar a conta de Automatização
Para atualizar uma conta de Automatização, tem de ter os seguintes privilégios específicos e as permissões necessárias para concluir este tópico.   
 
* A sua conta de utilizador do AD tem de ser adicionada a uma função com permissões equivalentes à função de Contribuidor para recursos Microsoft.Automation, conforme descrito no artigo [Controlo de acesso baseado em funções na Automatização do Azure](automation-role-based-access-control.md#contributor-role-permissions).  
* Os utilizadores não administradores no seu inquilino do Azure AD podem [registar aplicações AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) se a opção **Os utilizadores podem registar aplicações** do inquilino do Azure AD na página **Definições de utilizadores** está definida como **Sim**. Se a definição dos registos da aplicação for **Não**, o utilizador que executa esta ação tem de ser um administrador global no Azure AD.

Se não for membro da instância do Active Directory da subscrição antes de ser adicionado à função de administrador global/coadministrador da mesma, é adicionado ao Active Directory como convidado. Nesta situação, recebe o aviso "Não tem permissões para criar..." no painel **Adicionar Conta de Automatização**. Os utilizadores que foram adicionados primeiro à função de administrador global/coadministrador podem ser removidos da instância do Active Directory da subscrição e adicionados novamente, para que se tornem em Utilizadores completos no Active Directory. Para verificar esta situação, no painel **Azure Active Directory**, no portal do Azure, selecione **Utilizadores e grupos**, **Todos os utilizadores** e, depois de selecionar o utilizador específico, selecione **Perfil**. O valor do atributo **Tipo de utilizador** sob o perfil de utilizadores não deve ser igual a **Convidado**.

## <a name="create-run-as-account-from-the-portal"></a>Criar conta Run As no portal
Nesta secção, execute os seguintes passos para atualizar a sua conta de Automatização do Azure no portal do Azure.  Crie as contas Run As e Classic Run As individualmente. Se não precisar de gerir os recursos clássicos, pode simplesmente criar a conta Run As do Azure.  

1. Inicie sessão no portal do Azure com uma conta que seja membro da função Administradores da Subscrição e coadministrador da subscrição.
2. No portal do Azure, clique em **Mais serviços**, que se encontra no canto inferior esquerdo. Na lista de recursos, escreva **Automatização**. À medida que começa a escrever, a lista filtra com base na sua entrada. Selecione **Contas de Automatização**.
3. Na página **Contas de Automatização**, selecione a sua conta de Automatização a partir da lista de contas de Automatização.
4. No painel da esquerda, selecione **Contas Run As** na secção **Definições da Conta**.  
5. Consoante a conta que precisar, selecione **Conta Run As do Azure** ou **Conta Run As Clássica do Azure**.  Depois de selecionar **Adicionar Conta Run As do Azure** ou **Adicionar Conta Run As Clássica do Azure**, é apresentado o painel e, depois de rever as informações de descrição geral, clique em **Criar** para prosseguir com a criação da conta Run As.  
6. Enquanto o Azure cria a conta Run As, pode acompanhar o progresso em **Notificações** a partir do menu.  Também é apresentada uma faixa a indicar que a conta está a ser criada.  Este processo pode demorar alguns minutos a concluir.  

## <a name="create-run-as-account-using-powershell-script"></a>Criar conta Run As com o script do PowerShell
Este script do PowerShell inclui suporte para as seguintes configurações:

* Utilizar um certificado autoassinado para criar uma conta Run As.
* Utilizar um certificado autoassinado para criar uma conta Run As e uma conta Run As Clássica.
* Criar uma conta Run As e uma conta Run As Clássica mediante a utilização de um certificado emitido pela sua autoridade de certificação empresarial (AC).
* Utilizar um certificado autoassinado na cloud do Azure Government para criar uma conta Run As e uma conta Run As Clássica.

>[!NOTE]
> Se selecionar uma destas opções para criar uma conta Run As Clássica, após o script ser executado, carregue o certificado público (extensão de nome de ficheiro .cer) para o arquivo de gestão da subscrição na qual a conta de Automatização foi criada.
> 

1. Guarde o seguinte script no seu computador. Neste exemplo, guarde-o com o nome de ficheiro *New-RunAsAccount.ps1*.

         #Requires -RunAsAdministrator
         Param (
         [Parameter(Mandatory=$true)]
         [String] $ResourceGroup,

         [Parameter(Mandatory=$true)]
         [String] $AutomationAccountName,

         [Parameter(Mandatory=$true)]
         [String] $ApplicationDisplayName,

         [Parameter(Mandatory=$true)]
         [String] $SubscriptionId,

         [Parameter(Mandatory=$true)]
         [Boolean] $CreateClassicRunAsAccount,

         [Parameter(Mandatory=$true)]
         [String] $SelfSignedCertPlainPassword,

         [Parameter(Mandatory=$false)]
         [String] $EnterpriseCertPathForRunAsAccount,

         [Parameter(Mandatory=$false)]
         [String] $EnterpriseCertPlainPasswordForRunAsAccount,

         [Parameter(Mandatory=$false)]
         [String] $EnterpriseCertPathForClassicRunAsAccount,

         [Parameter(Mandatory=$false)]
         [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

         [Parameter(Mandatory=$false)]
         [ValidateSet("AzureCloud","AzureUSGovernment")]
         [string]$EnvironmentName="AzureCloud",

         [Parameter(Mandatory=$false)]
         [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
         )

         function CreateSelfSignedCertificate([string] $certificateName, [string] $selfSignedCertPlainPassword,
                                        [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
         $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
             -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
             -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired) -HashAlgorithm SHA256

         $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
         Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
         Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
         }

         function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
         $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
         $keyId = (New-Guid).Guid

         $startDate = Get-Date
         $endDate = (Get-Date $PfxCert.GetExpirationDateString()).AddDays(-1)
         
         #Create an Azure AD application, AD App Credential, AD ServicePrincipal
         $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $keyId) 
         $ApplicationCredential = New-AzureRmADAppCredential -ApplicationId $Application.ApplicationId -CertValue $keyValue -StartDate $startDate -EndDate $endDate 
         $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId 
         $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

         # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
         Sleep -s 15
         $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
         $Retries = 0;
         While ($NewRole -eq $null -and $Retries -le 6)
         {
             Sleep -s 10
             New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
             $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
             $Retries++;
         }
             return $Application.ApplicationId.ToString();
         }

         function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
         $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
         Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
         New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
         }

         function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
         Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
         New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
         }

         Import-Module AzureRM.Profile
         Import-Module AzureRM.Resources

         $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
         if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 4) -or ($AzureRMProfileVersion.Major -gt 3)))
         {
             Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
             return
         }

         Login-AzureRmAccount -Environment $EnvironmentName 
         $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

         # Create a Run As account by using a service principal
         $CertifcateAssetName = "AzureRunAsCertificate"
         $ConnectionAssetName = "AzureRunAsConnection"
         $ConnectionTypeName = "AzureServicePrincipal"

         if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
         $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
         $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
         } else {
            $CertificateName = $AutomationAccountName+$CertifcateAssetName
            $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
            $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
            $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
            CreateSelfSignedCertificate $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
         }

         # Create a service principal
         $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
         $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

         # Create the Automation certificate asset
         CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

         # Populate the ConnectionFieldValues
         $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
         $TenantID = $SubscriptionInfo | Select TenantId -First 1
         $Thumbprint = $PfxCert.Thumbprint
         $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

         # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
         CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

         if ($CreateClassicRunAsAccount) {
              # Create a Run As account by using a service principal
              $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
              $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
              $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
              $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                      "Log in to the Microsoft Azure portal (https://portal.azure.com) and select Subscriptions -> Management Certificates." + [Environment]::NewLine +
                      "Then click Upload and upload the .cer format of #CERT#"

               if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
               $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
               $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
               $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
         } else {
               $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
               $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
               $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
               $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
               $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
               CreateSelfSignedCertificate $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
         }

         # Create the Automation certificate asset
         CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

         # Populate the ConnectionFieldValues
         $SubscriptionName = $subscription.Subscription.Name
         $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

         # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
         CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

         Write-Host -ForegroundColor red $UploadMessage
         }

2. No seu computador, inicie o **Windows PowerShell** a partir do ecrã **Iniciar** ecrã com direitos de utilizador elevados.
3. A partir da shell da linha de comandos elevada, aceda à pasta que contém o script que criou no passo 1.  
4. Execute o script, utilizando os valores de parâmetros da configuração de que precisa.

    **Utilizar um certificado autoassinado para criar uma conta Run As**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Utilizar um certificado autoassinado para criar uma conta Run As e uma conta Run As Clássica**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Utilizar um certificado empresarial para criar uma conta Run As e uma conta Run As Clássica**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Utilizar um certificado autoassinado na cloud do Azure Government para criar uma conta Run As e uma conta Run As Clássica**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Após o script ser executado, ser-lhe-á pedido para autenticar com o Azure. Inicie sessão com uma conta que seja membro da função de administradores da subscrição e coadministrador da subscrição.
    >
    >

Depois de o script ser executado com êxito, tenha em conta o seguinte:
* Se tiver criado uma conta Run As Clássica com um certificado público autoassinado (ficheiro .cer), o script cria-o e guarda-o na pasta de ficheiros temporários no seu computador, no perfil de utilizador *%USERPROFILE%\AppData\Local\Temp* que utilizou para executar a sessão do PowerShell.
* Se tiver criado uma conta Run As Clássica com um certificado público empresarial (ficheiro .cer), utilize esse certificado. Siga as instruções para [carregar um certificado da API de gestão para o portal do Azure](../azure-api-management-certs.md)e, em seguida, validar a configuração das credenciais com recursos de implementação clássica, utilizando o [código para autenticação de exemplo com os recursos de implementação clássico do Azure](automation-verify-runas-authentication.md#classic-run-as-authentication). 
* Se *não* tiver criado uma conta Run As Clássica, autentique com recursos do Resource Manager e utilize o [código de exemplo para autenticar com recursos da Gestão do Serviço](automation-verify-runas-authentication.md#automation-run-as-authentication) para validar a configuração da credencial.

## <a name="next-steps"></a>Passos Seguintes
* Para mais informações sobre Principais de Serviço, consulte a [Objetos da Aplicação e Objetos de Principais de Serviço](../active-directory/active-directory-application-objects.md).
* Para obter mais informações sobre certificados e serviços do Azure, consulte [Certificates overview for Azure Cloud Services (Descrição geral de certificados para Serviços Cloud do Azure)](../cloud-services/cloud-services-certs-create.md).
