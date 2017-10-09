---
title: "aaaGet dados utilizando Olá API do Azure AD Reporting com certificados | Microsoft Docs"
description: "Explica como toouse Olá API do Azure AD Reporting com dados tooget de credenciais de certificado de diretórios sem intervenção do utilizador."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Obter dados utilizando a API de relatórios do Azure AD Olá com certificados
Este artigo aborda como toouse Olá API do Azure AD Reporting com dados tooget de credenciais de certificado de diretórios sem intervenção do utilizador. 

## <a name="use-hello-azure-ad-reporting-api"></a>Olá, utilize a API de relatórios de AD do Azure 
A API de relatórios de AD do Azure requer que conclua Olá os seguintes passos:
 *  Pré-requisitos da instalação
 *  Defina o certificado de Olá na sua aplicação
 *  Obter um token de acesso
 *  Utilizar Olá de token toocall de acesso de Olá Graph API

Para obter informações sobre o código de origem, veja [Leverage Report API Module (Tirar Partido do Módulo da API de Relatório)](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils). 

### <a name="install-prerequisites"></a>Pré-requisitos da instalação
Precisa de toohave Azure AD PowerShell V2 e AzureADUtils module instalada.

1. Transfira e instale o Azure AD Powershell V2, seguir instruções Olá em [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Transferir o módulo do Azure AD Utils Olá da [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Este módulo disponibiliza vários cmdlets de utilitário, incluindo:
   * versão mais recente do Olá da ADAL com Nuget
   * Tokens de acesso de utilizador, chaves de aplicação e certificados, através da ADAL
   * Graph API que processa resultados paginados

**módulo do Azure AD Utils de Olá tooinstall:**

1. Criar um diretório toosave Olá utilitários módulo (por exemplo, c:\azureAD) e transferir o módulo Olá a partir do GitHub.
2. Abra uma sessão do PowerShell e aceda diretório toohello que acabou de criar. 
3. Importar o módulo Olá e instalá-la no caminho de módulo Olá PowerShell utilizando o cmdlet Olá AzureADUtilsModule de instalação. 

sessão de Olá deve ter um aspeto semelhante toothis ecrã:

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Defina o certificado de Olá na sua aplicação
1. Se já tiver uma aplicação, obter o ID de objeto de Olá Portal do Azure. 

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Abra uma sessão do PowerShell e ligue tooAzure AD utilizando o cmdlet Olá Connect-AzureAD.

  ![Portal do Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Utilize o cmdlet New-AzureADApplicationCertificateCredential de Olá de AzureADUtils tooadd tooit de credencial um certificado. 

>[!Note]
>Precisa de aplicação de Olá tooprovide ID de objeto capturadas anteriormente, bem como Olá objeto certificado (obter esta utilizando Olá Cert: unidade).
>


  ![Portal do Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Obter um token de acesso

tooget um token de acesso, utilize o cmdlet de Get-AzureADGraphAPIAccessTokenFromCert Olá de AzureADUtils. 

>[!NOTE]
>É necessário toouse Olá ID da aplicação em vez de Olá ID de objeto que utilizou na secção último Olá.
>

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Utilizar Olá de token toocall de acesso de Olá Graph API

Agora, pode criar script de Olá. Abaixo está um exemplo utilizando o cmdlet Invoke-AzureADGraphAPIQuery de Olá de Olá AzureADUtils. Este cmdlet processa resultados paginados múltiplos e, em seguida, envia do pipeline de PowerShell esses resultados toohello. 

 ![Portal do Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

Agora está pronto tooexport tooa CSV e guardar o sistema do tooa SIEM. Pode também moldar o script no tooget tarefa agendada dados do Azure AD do seu inquilino periodicamente sem ter de chaves de aplicação toostore no código de origem Olá. 

## <a name="next-steps"></a>Passos seguintes
[Olá Noções básicas de gestão de identidades do Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



