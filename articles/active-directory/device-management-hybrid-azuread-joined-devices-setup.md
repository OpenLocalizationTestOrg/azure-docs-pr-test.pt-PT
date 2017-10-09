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
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a>Como dispositivos associados ao tooconfigure híbrida do Azure Active Directory

Gestão de dispositivos no Azure Active Directory (Azure AD), pode certificar-se de que os utilizadores acedem aos seus recursos dos dispositivos que cumprem as normas de segurança e conformidade. Para obter mais detalhes, consulte [gestão toodevice de introdução no Azure Active Directory](device-management-introduction.md).

Se tiver um ambiente do Active Directory no local e quiser toojoin tooAzure a dispositivos associados a um domínio AD, pode realizar esta através da configuração híbrida do Azure AD associado dispositivos. tópico de Olá disponibiliza Olá relacionados com os passos. 


## <a name="before-you-begin"></a>Antes de começar

Antes de iniciar a configuração híbrida do Azure AD dispositivos associados a um no seu ambiente, deverá familiarizar-se com restrições de Olá e cenários de Olá suportado.  

tooimprove Olá facilitar a leitura de descrições de Olá, este tópico utiliza Olá termo os seguintes: 

- **Dispositivos atuais do Windows** -este prazo refere-se associados a um toodomain dispositivos com Windows 10 ou Windows Server 2016.
- **Dispositivos de nível inferior do Windows** -este prazo refere-se tooall **suportado** dispositivos Windows associados a um domínio, que estão em execução Windows 10 nem do Windows Server 2016.  


### <a name="windows-current-devices"></a>Dispositivos atuais do Windows

- Para dispositivos com o sistema operativo da ambiente de trabalho de Windows hello, recomendamos que utilize o Windows 10 aniversário da atualização (versão 1607) ou posterior. 
- Olá, registo de dispositivos atuais do Windows **é** suportada em ambientes não federada, tais como configurações de sincronização de hash de palavra-passe.  


### <a name="windows-down-level-devices"></a>Dispositivos de nível inferior do Windows

- Olá seguintes dispositivos de nível inferior do Windows é suportada:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- Olá, registo de dispositivos de nível inferior do Windows **é** suportada em ambientes não federada através de totalmente integrada de sessão único [do Azure Active Directory totalmente integrada Single Sign-On](https://aka.ms/hybrid/sso).
- Olá, registo de dispositivos de nível inferior do Windows **não é** suportados para dispositivos com perfis itinerantes. Se estiver a depender de perfis ou definições de roaming, utilize o Windows 10.



## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar a ativação híbrida do Azure AD associado dispositivos na sua organização, terá de toomake certificar-se de que está a executar uma versão atualizada do Azure AD connect.

Do Azure AD Connect:

- Mantém a associação de Olá entre a conta de computador Olá no objeto de dispositivo Olá no Azure AD e no local do Active Directory (AD). 
- Permite que outros dispositivos relacionados com funcionalidades como o Windows Hello para empresas.



## <a name="configuration-steps"></a>Passos de configuração

Pode configurar híbrida do Azure AD associado dispositivos para vários tipos de plataformas de dispositivos do Windows. Este tópico inclui os passos de Olá necessário para todos os cenários de configuração típica.  

Utilize Olá tabela tooget uma descrição geral dos passos de Olá que são necessários para o seu cenário a seguir:  



| Passos                                      | Sincronização de hash de atual e a palavra-passe do Windows | Atual do Windows e a Federação | Windows de nível inferior |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Passo 1: Configurar o ponto de ligação de serviço | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |
| Passo 2: Configurar a emissão de afirmações           |                                        | ![Marcar][1]                    | ![Marcar][1]        |
| Passo 3: Ativar dispositivos não Windows 10      |                                        |                                | ![Marcar][1]        |
| Passo 4: Implementação de controlo e implementação     | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |
| Passo 5: Verificar se a dispositivos associados          | ![Marcar][1]                            | ![Marcar][1]                    | ![Marcar][1]        |



## <a name="step-1-configure-service-connection-point"></a>Passo 1: Configurar o ponto de ligação de serviço

objeto de (SCP) do ponto de ligação de serviço Olá é utilizado pelos seus dispositivos durante Olá registo toodiscover informações de inquilino do Azure AD. No local no Active Directory (AD), objeto Olá SCP para Olá híbrida do Azure AD associados a um dispositivos tem de existir na partição de contexto de nomenclatura de configuração do Olá da floresta do computador Olá. Não há apenas um contexto de nomenclatura de configuração por floresta. Numa configuração várias floresta do Active Directory, tem de existir ponto de ligação de serviço Olá em todas as florestas que contêm os computadores associados a um domínio.

Pode utilizar Olá [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Olá contexto nomenclatura de configuração da sua floresta.  

Para uma floresta com o nome de domínio do Active Directory Olá *fabrikam.com*, contexto de nomenclatura de configuração de Olá é:

`CN=Configuration,DC=fabrikam,DC=com`

Na sua floresta, o objeto de Olá SCP para Olá-registo automático de dispositivos associados a um domínio está localizado em:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

Dependendo de como tiver implementado o Azure AD Connect, objeto de SCP Olá poderá já tiverem sido configurado.
Pode verificar a existência de Olá do objeto de Olá e obter valores de deteção de Olá utilizando Olá seguinte script do Windows PowerShell: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Olá **$scp. As palavras-chave** saída mostra informações de inquilino do Azure AD de Olá, por exemplo:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Se o ponto de ligação de serviço Olá não existir, pode criá-la executando Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet no seu servidor do Azure AD Connect. Credencial de administrador de empresa é necessário toorun este cmdlet.  
Olá cmdlet:

- Cria o ponto de ligação de serviço Olá na floresta do Active Directory Olá do Azure AD Connect está ligado. 
- Requer que toospecify Olá `AdConnectorAccount` parâmetro. Esta é a conta de Olá que está configurada como o Active Directory a conta do conector no Azure AD connect. 


Olá script seguinte mostra um exemplo de utilização do cmdlet Olá. Este script, `$aadAdminCred = Get-Credential` requer tootype um nome de utilizador. Terá de nome de utilizador de Olá tooprovide no formato de nome principal (UPN) do utilizador Olá (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- Utiliza o módulo PowerShell do Active Directory de Olá, que depende de serviços da Web do Active Directory em execução num controlador de domínio. Serviços da Web do Active Directory é suportada em controladores de domínio com o Windows Server 2008 R2 e posterior.
- Só é suportado pelo Olá **MSOnline PowerShell versão do módulo 1.1.166.0**. toodownload este módulo, utilize esta opção [ligação](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Para controladores de domínio a executar o Windows Server 2008 ou de versões anteriores, utilize o script de Olá abaixo o ponto de ligação de serviço toocreate Olá.

Numa configuração de várias floresta, deve utilizar Olá seguir o ponto de ligação do serviço do script toocreate Olá em cada floresta onde existem computadores:
 
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


## <a name="step-2-setup-issuance-of-claims"></a>Passo 2: Configurar a emissão de afirmações

No Azure federado configuração do AD, dispositivos dependem de serviços de Federação do Active Directory (AD FS) ou um terceiros 3rd no local tooAzure de tooauthenticate de serviço de Federação AD. Dispositivos autenticar tooget um tooregister de token de acesso contra Olá Service do Azure Active Directory dispositivo registo (Azure DRS).

Windows dispositivos atuais autenticam utilizando a autenticação integrada do Windows tooan WS-Trust ponto final ativo (versões 1.3 ou 2005) alojado pelo serviço de Federação Olá no local.

> [!NOTE]
> Quando utilizar o AD FS, quer **adfs/services/confiança/13/windowstransport** ou **adfs/services/confiança/2005/windowstransport** tem de estar ativada. Se estiver a utilizar Olá Proxy de autenticação da Web, certifique-se também que este ponto final está publicado através do proxy de Olá. Pode ver que os parâmetros são ativados através da consola de gestão de Olá do AD FS em **serviço > pontos finais**.
>
>Se não tiver o AD FS como o serviço de Federação no local, siga instruções de Olá do seu toomake fornecedor se suportam 1.3 de WS-Trust ou pontos finais de 2005 e estes são publicadas através de Olá ficheiro de troca de metadados (MEX).

Olá seguintes afirmações têm de existir no token de Olá recebido pelo Azure DRS para toocomplete de registo do dispositivo. Azure DRS irá criar um objeto de dispositivo no Azure AD com algumas destas informações que, em seguida, são utilizadas pelo objeto de dispositivo do Azure AD Connect tooassociate Olá recém-criado com Olá computador conta no local.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Se tiver mais do que um nome de domínio verificado, terá de Olá tooprovide afirmação para computadores a seguir:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Se já estiver a emitir uma afirmação de ImmutableID (por exemplo, o ID de início de sessão alternativo) terá tooprovide uma afirmação correspondente para computadores:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

Olá secções a seguir, encontrará informações sobre:
 
- valores de Olá cada afirmação deve ter
- Como uma definição deverá ter o seguinte aspeto no AD FS

definição de Olá ajuda-o a tooverify se valores Olá estão presentes ou se terá toocreate-los.

> [!NOTE]
> Se não utilizar o AD FS para o servidor de Federação no local, siga estas afirmações tooissue do seu fornecedor instruções toocreate Olá configuração apropriada.

### <a name="issue-account-type-claim"></a>Afirmações de tipo de conta do problema

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Esta afirmação tem de conter um valor de **DJ**, que identifica o dispositivo de Olá como um computador associado ao domínio. No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Emitir objectGUID de Olá computador conta no local

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Esta afirmação tem de conter Olá **objectGUID** valor Olá no local a conta de computador. No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Emitir Sidobjeto de Olá computador conta no local

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Esta afirmação tem de conter Olá Olá **Sidobjeto** valor Olá no local a conta de computador. No AD FS, pode adicionar uma regra de transformação de emissão que tem este aspeto:

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Emitir issuerID para computador quando múltiplos verificar nomes de domínio no Azure AD

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Esta afirmação tem de conter Olá identificador de recurso uniforme (URI) de qualquer um dos Olá verificar nomes de domínio que se ligam com Olá no local token de Olá de emissora de serviço (AD FS ou terceiros 3rd) de Federação. No AD FS, pode adicionar regras de transformação de emissão que parece ser Olá aqueles abaixo nessa ordem específica após Olá aqueles acima. Tenha em atenção que um tooexplicitly problema Olá regra para os utilizadores é necessário. Em regras de Olá abaixo, é adicionada uma regra primeiro identificar utilizador vs. a autenticação de computador.

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


Na afirmação Olá acima,

- `$<domain>`é o URL do serviço Olá AD FS
- `<verified-domain-name>`é um marcador de posição terá tooreplace com um dos seus nomes de domínio verificado no Azure AD



Para obter mais detalhes sobre os nomes de domínio verificado, consulte [adicionar um tooAzure de nome de domínio personalizado do Active Directory](active-directory-add-domain.md).  
tooget uma lista dos seus domínios verificados da empresa, pode utilizar Olá [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Emitir ImmutableID para computador quando existe uma para os utilizadores (por exemplo, início de sessão alternativo ID está definido)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**-Esta afirmação tem de conter um valor válido para computadores. No AD FS, pode criar uma regra de transformação de emissão da seguinte forma:

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Programa auxiliar script toocreate Olá AD FS transformação regras de emissão

Olá seguinte script ajuda-o com a criação de emissão de Olá Olá descritas acima de regras de transformação.

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

### <a name="remarks"></a>Observações 

- Este script acrescenta regras existentes do Olá regras toohello. Não execute scripts de Olá duas vezes porque Olá conjunto de regras seriam adicionado duas vezes. Certifique-se de que nenhum correspondentes existem regras para estas afirmações (em condições de correspondente Olá) antes de executar o script de Olá novamente.

- Se tiver vários verificado nomes de domínio (conforme ilustrado no portal do Azure AD de Olá ou através do cmdlet Olá Get MsolDomains), defina o valor de Olá de **$multipleVerifiedDomainNames** no Olá script demasiado**$true**. Certifique-se também que remova qualquer afirmação issuerid existente que poderá ter sido criada pelo Azure AD Connect ou através de outros meios. Eis um exemplo para esta regra:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Se já ter emitido uma **ImmutableID** de afirmação para contas de utilizador, defina o valor de Olá de **$immutableIDAlreadyIssuedforUsers** no Olá script demasiado**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Passo 3: Ativar os dispositivos de nível inferior do Windows

Se alguns dos seus dispositivos associados a um domínio Windows nível dispositivos, tem de:

- Defina uma política no Azure AD tooenable dispositivos tooregister de utilizadores.
 
- Configurar o seu local Federação serviço tooissue afirmações toosupport **autenticação integrada de Windows (IWA)** para registo de dispositivos.
 
- Adicione Olá do Azure AD dispositivos autenticação ponto final toohello Intranet zonas locais tooavoid certificado solicita ao autenticar o dispositivo de Olá.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Definir a política no Azure AD tooenable dispositivos tooregister de utilizadores

dispositivos de nível inferior do tooregister Windows, terá de toomake se esse Olá definição tooallow utilizadores tooregister dispositivos no Azure AD está definido. No portal do Azure Olá, pode encontrar esta definição em:

`Azure Active Directory > Users and groups > Device settings`
    
Olá política seguinte tem de ser definida demasiado**todos os**: **os utilizadores podem registar os seus dispositivos com o Azure AD**

![Registar dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Configurar o serviço de Federação no local 

O serviço de Federação no local tem de suportar Olá emissora **authenticationmehod** e **wiaormultiauthn** afirmações ao receber uma autenticação pedem toohello do Azure AD da entidade confiadora, que contém um resouce_params parâmetro com um valor de codificação como mostrado abaixo:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Quando é fornecido este pedido, serviço de Federação no local Olá utilizador Olá utilizando a autenticação integrada do Windows tem de ser autenticado e após com êxito, este tem de emitir Olá seguintes duas afirmações:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

No AD FS, tem de adicionar uma regra de transformação de emissão que método de autenticação através de transmite Olá.  

**tooadd esta regra:**

1. Na consola de gestão do Olá AD FS, aceda demasiado`AD FS > Trust Relationships > Relying Party Trusts`.
2. Objetos de confiança das entidades confiadoras do Olá plataforma de identidade do Microsoft Office 365 com o botão direito e, em seguida, selecione **editar regras de afirmação**.
3. No Olá **regras de transformação de emissão** separador, selecione **Adicionar regra**.
4. No Olá **regra de afirmação** lista de modelo, selecione **enviar afirmações utilizando uma regra personalizada**.
5. Selecione **seguinte**.
6. No Olá **nome da regra de afirmação** caixa, escreva **regra de afirmação de método de autenticação**.
7. No Olá **regra de afirmação** caixa, Olá tipo seguinte regra:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. No servidor de Federação, escreva o comando do PowerShell Olá abaixo depois de substituir  **\<RPObjectName\>**  com Olá entidade confiadora terceiros nome do objeto para os objetos de confiança das entidades confiadoras do Azure AD. Este objeto é normalmente denominado **plataforma de identidade do Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Adicionar zonas de Local Intranet de toohello de ponto final autenticação dispositivo Olá do Azure AD

certificado tooavoid pede-lhe quando os utilizadores no registo de dispositivos autenticam tooAzure AD, pode emitir um Olá tooadd do política tooyour dispositivos associados a domínios seguir zona de Local Intranet toohello URL no Internet Explorer:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Passo 4: Implementação de controlo e implementação

Quando tiver concluído os passos de Olá necessário, dispositivos associados a domínios são tooautomatically pronto a associação do Azure AD:

- Dispositivos de todos os associados a um domínio que executam o Windows 10 aniversário da atualização e o Windows Server 2016 automaticamente registar com o Azure AD no dispositivo reinicie ou sessão do utilizador. 

- Novos dispositivos registar com o Azure AD quando o dispositivo de Olá for reiniciado depois de concluída a operação de associação de domínio Olá.

- Dispositivos que foram anteriormente do Azure AD registado (por exemplo, para o Intune) transição demasiado "*associados a um domínio, registado no AAD*"; no entanto demora algum tempo para que este processo toocomplete em todos os dispositivos que devem estar toohello fluxo normal de atividade de utilizador e domínio.

### <a name="remarks"></a>Observações

- Pode utilizar uma implementação de política de grupo do Olá ao toocontrol objeto de registo automática do Windows 10 e computadores associados a domínios do Windows Server 2016.

- Windows 10 de Novembro de 2015 Update automaticamente associa com o Azure AD **apenas** se o objeto de política de grupo de implementação de Olá está definido.

- toorollout de computadores de nível inferior do Windows, pode implementar um [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que selecionar.

- Se push dispositivos de associados a um domínio de tooWindows 8.1 objeto de política de grupo do Olá, é tentada uma associação; No entanto, é recomendado que utilize Olá [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toojoin todos os dispositivos de nível inferior do Windows. 

### <a name="create-a-group-policy-object"></a>Criar um objeto de política de grupo 

implementação de Olá toocontrol de computadores atuais do Windows, deve implementar Olá **registar computadores associados a um domínio como dispositivos** dispositivos toohello objeto de política de grupo que pretende tooregister. Por exemplo, pode implementar o grupo de segurança de tooa ou unidade organizacional do Olá política tooan.

**política de Olá tooset:**

1. Abra **Gestor de servidor**e, em seguida, aceda demasiado`Tools > Group Policy Management`.
2. Visite o nó de domínio toohello que corresponde ao domínio toohello onde pretende que o registo automático tooactivate de computadores atuais do Windows.
3. Clique com botão direito **objetos de política de grupo**e, em seguida, selecione **novo**.
4. Escreva um nome para o objeto de política de grupo. Por exemplo, * associação do Azure AD híbrido. 
5. Clique em **OK**.
6. Clique com o botão direito do novo objeto de política de grupo e, em seguida, selecione **editar**.
7. Aceda demasiado**configuração do computador** > **políticas** > **modelos administrativos** > **Windows Componentes** > **registo de dispositivos**. 
8. Clique com botão direito **registar computadores associados a um domínio como dispositivos**e, em seguida, selecione **editar**.
   
   > [!NOTE]
   > Este modelo de política de grupo foi alterado de versões anteriores da consola de gestão de políticas de grupo Olá. Se estiver a utilizar uma versão anterior da consola de Olá, aceda demasiado`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Selecione **ativado**e, em seguida, clique em **aplicar**.
8. Clique em **OK**.
9. Olá ligação localização tooa de objeto de política de grupo à sua escolha. Por exemplo, pode ligar-tooa específico, unidade organizacional. Também foi ligue-o grupo de segurança específicos tooa de computadores que associar automaticamente com o Azure AD. tooset esta política para todos os computadores associados a domínios Windows 10 e Windows Server 2016 na sua organização, o domínio de toohello do objeto de política de grupo do ligação Olá.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Pacotes do Windows Installer para computadores não - Windows 10

computadores de nível inferior toojoin associados a um domínio Windows num ambiente federado, pode transferir e instalar estas pacote do Windows Installer (. msi) do Centro de transferências em Olá [Microsoft Workplace Join para computadores Windows de 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)página.

Pode implementar o pacote de Olá através da utilização de um sistema de distribuição de software, como o System Center Configuration Manager. Olá pacote suporta opções de instalação silenciosa padrão Olá com Olá *silenciosos* parâmetro. System Center Configuration Manager Current Branch oferece vantagens adicionais de versões anteriores, como Olá capacidade tootrack concluída registos. Para obter mais informações, consulte [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

Instalador de Olá cria uma tarefa agendada no sistema de Olá que é executado no contexto do utilizador Olá. tarefa de Olá é acionada quando o utilizador Olá inicia sessão tooWindows. tarefas de Olá associa automaticamente dispositivos Olá com o Azure AD com as credenciais de utilizador Olá após a autenticação utilizando a autenticação integrada do Windows. toosee Olá agendada a tarefa, de dispositivo Olá, aceda demasiado**Microsoft** > **Workplace Join**, e, em seguida, aceda a biblioteca do Programador de tarefas de toohello.

## <a name="step-5-verify-joined-devices"></a>Passo 5: Verificar se a dispositivos associados

Pode verificar os dispositivos associados com êxito na sua organização utilizando Olá [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet no Olá [módulo Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

resultado Olá deste cmdlet mostra os dispositivos que são registados e associados com o Azure AD. tooget todos os dispositivos, utilize Olá **-todos os** parâmetro e, em seguida, filtro-los utilizando Olá **deviceTrustType** propriedade. Associado a um domínio dispositivos têm um valor de **associados a um domínio**.

## <a name="next-steps"></a>Passos seguintes

* [Gestão de toodevice de introdução no Azure Active Directory](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
