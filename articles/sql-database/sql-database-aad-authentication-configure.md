---
title: "autenticação no Azure Active Directory aaaConfigure - SQL | Microsoft Docs"
description: "Saiba como tooconnect tooSQL base de dados e o SQL Data Warehouse, utilizando a autenticação do Active Directory do Azure."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Configurar e gerir a autenticação do Azure Active Directory com a base de dados SQL ou SQL Data Warehouse

Este artigo mostra como toocreate preencher do Azure AD e, em seguida, utilizar o Azure AD com o SQL Database do Azure e o SQL Data Warehouse. Para obter uma descrição geral, consulte [autenticação do Active Directory do Azure](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Ligar tooSQL servidor em execução numa VM do Azure não é suportado com uma conta do Azure Active Directory. Em alternativa, utilize um domínio de conta do Active Directory.

## <a name="create-and-populate-an-azure-ad"></a>Criar e preencher um Azure AD
Criar um Azure AD e preenchê-lo com os utilizadores e grupos. Azure AD pode ser Olá domínio inicial do Azure AD um domínio gerido. Azure AD também pode ser um local no Active Directory Domain Services que está federada com Olá do Azure AD.

Para obter mais informações, consulte [integrar as identidades no local ao Azure Active Directory](../active-directory/active-directory-aadconnect.md), [adicionar o seus próprios tooAzure de nome de domínio AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure suporta agora a Federação com o Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [administrar o seu diretório do Azure AD](https://msdn.microsoft.com/library/azure/hh967611.aspx), [gerir do Azure AD com o Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), e [identidade híbrida Portas e protocolos necessários](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Opcional: Associar ou alterar Olá active directory está atualmente associado a sua subscrição do Azure
tooassociate a base de dados com o diretório de Olá do Azure AD para a sua organização, certifique-diretório Olá um diretório fidedigno para Olá subscrição do Azure alojamento Olá da base de dados. Para obter mais informações, consulte [Como associar as subscrições do Azure ao Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Informações adicionais:** subscrição do Azure cada tem uma relação de confiança com uma instância do Azure AD. Isto significa que confia nesse diretório tooauthenticate utilizadores, serviços e dispositivos. Várias subscrições podem confiar Olá mesmo diretório, mas uma subscrição confianças apenas um diretório. Pode ver o diretório de confiança através da sua subscrição em Olá **definições** separador em [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Esta relação de confiança de uma subscrição com um diretório é ao contrário da relação de Olá que tem uma subscrição com todos os outros recursos no Azure (sites, bases de dados e assim sucessivamente), que são mais como recursos subordinados de uma subscrição. Se uma subscrição expirar, em seguida, aceder a outros recursos associados à subscrição Olá toothose também deixa de. Mas Olá diretório permanece no Azure, pode associar outra subscrição esse diretório e os utilizadores do diretório de Olá toomanage de continuar. Para obter mais informações sobre os recursos, consulte [compreender o acesso a recursos no Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Olá procedimentos seguintes mostram como toochange Olá associados diretório para uma determinada subscrição.
1. Ligar tooyour [Portal clássico do Azure](https://manage.windowsazure.com/) através da utilização de um administrador de subscrição do Azure.
2. Na faixa do Olá esquerdo, selecione **definições**.
3. As subscrições são apresentadas no ecrã de definições de Olá. Se assim pretender Olá a subscrição não aparecer, clique em **subscrições** pendente na parte superior do Olá, Olá **filtro por DIRETÓRIO** e selecione o diretório de Olá que contém as suas subscrições e, em seguida, clique em **Aplicar**.
   
    ![Selecione a subscrição][4]
4. No Olá **definições** área, clique a sua subscrição e, em seguida, clique em **editar DIRETÓRIO** em Olá parte inferior da página Olá.
   
    ![portal de definições do AD][5]
5. No Olá **editar DIRETÓRIO** caixa, selecione Olá do Azure Active Directory que estão associados com o SQL Server ou SQL Data Warehouse e, em seguida, clique em seta Olá seguinte.
   
    ![Selecione de diretório de edição][6]
6. No Olá **confirmar** diretório caixa de diálogo mapeamento, confirme que "**todos os coadministradores serão removidos.**"
   
    ![Editar diretório confirmar][7]
7. Clique em portal de Olá Olá verificação tooreload.

   > [!NOTE]
   > Quando alterar o diretório de Olá, os coadministradores de tooall acesso, utilizadores do Azure AD e grupos e os utilizadores dos recursos de diretório de segurança são removidos e já não ter acesso toothis subscrição ou os respetivos recursos. Apenas, como um administrador de serviço, pode configurar o acesso para principais, com base no diretório Olá de novo. Esta alteração poderá demorar uma quantidade substancial de recursos de tooall toopropagate de tempo. Alterar o diretório de Olá, também alterações hello administrador do Azure AD para a base de dados SQL e do armazém de dados do SQL Server e não permitir acesso de base de dados para os utilizadores do Azure AD existentes. admin Olá do Azure AD tem de ser reposição (conforme descrito abaixo) e Azure novo utilizadores do AD tem de ser criados.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Criar um administrador do Azure AD para o Azure SQL server
Cada servidor de SQL do Azure (que aloja uma base de dados SQL ou SQL Data Warehouse) começa com uma conta de administrador de servidor único que seja administrador de hello do servidor de SQL do Azure completo Olá. Um administrador do SQL Server segundo tem de ser criado, que é uma conta do Azure AD. Este principal é criado como um utilizador de base de dados contida na base de dados mestra Olá. Como os administradores, as contas de administrador do servidor Olá são membros de Olá **db_owner** função em todos os utilizadores da base de dados e introduza cada base de dados do utilizador como Olá **dbo** utilizador. Para mais informações sobre as contas de administrador do servidor Olá, consulte [gerir bases de dados e inícios de sessão na base de dados do Azure SQL](sql-database-manage-logins.md).

Ao utilizar o Azure Active Directory com georreplicação, o administrador do Azure Active Directory Olá tem de ser configurado para Olá principal e servidores secundários Olá. Se um servidor tiver um administrador do Azure Active Directory, em seguida, inícios de sessão do Azure Active Directory e os utilizadores recebem um erro de tooserver "Não é possível ligar".

> [!NOTE]
> Os utilizadores que não se baseiam numa conta do Azure AD (incluindo a conta de administrador de servidor de SQL do Azure Olá), não é possível criar utilizadores do Azure baseada no AD, porque não têm toovalidate permissões propostas utilizadores de base de dados com Olá do Azure AD.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Aprovisionar um administrador do Azure Active Directory para o servidor de SQL do Azure

Olá dois procedimentos a seguir mostra como tooprovision um administrador do Azure Active Directory para o servidor de SQL do Azure no portal do Azure de Olá e utilizando o PowerShell.

### <a name="azure-portal"></a>Portal do Azure
1. No Olá [portal do Azure](https://portal.azure.com/), no Olá canto superior direito, clique em seu toodrop de ligação para baixo de uma lista de diretórios de Active Directory possíveis. Escolha Olá corrigir do Active Directory como a predefinição de Olá do Azure AD. Este passo ligações Olá subscrição associação com o Active Directory com o servidor de SQL do Azure, certificando-se de que Olá mesma subscrição é utilizada para do Azure AD e o SQL Server. (servidor de SQL do Azure Olá pode alojar o SQL Database do Azure ou o Azure SQL Data Warehouse.)   
    ![ad escolha][8]   
    
2. No Olá deixado faixa selecione **servidores SQL**, selecione o **do SQL Server**e, em seguida, no Olá **do SQL Server** painel, clique em **administrador do Active Directory**.   
3. No Olá **administrador do Active Directory** painel, clique em **definir administrador**.   
    ![Selecione active directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. No Olá **Adicionar administrador** painel, procure um utilizador, o utilizador selecione Olá ou o grupo toobe um administrador e, em seguida, clique em **selecione**. (o painel de administração do Active Directory Olá mostra todos os membros e grupos do Active Directory. Não não possível selecionar utilizadores ou grupos que estão a cinzento porque não são suportados como administradores do Azure AD. (Consulte Olá lista de administradores suportados no Olá **funcionalidades do Azure AD e limitações** secção [utilizar Azure Active Directory Authentication para a autenticação com base de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication.md).) O controlo de acesso baseado em funções (RBAC) aplica-se apenas toohello portal e não é propagado tooSQL do servidor.   
    ![Selecionar admin](./media/sql-database-aad-authentication/select-admin.png)  
    
5. Na parte superior de Olá de Olá **administrador do Active Directory** painel, clique em **guardar**.   
    ![Guardar admin](./media/sql-database-aad-authentication/save-admin.png)   

processo de Olá da alteração administrador Olá pode demorar vários minutos. Em seguida, o administrador novo Olá aparece no Olá **administrador do Active Directory** caixa.

   > [!NOTE]
   > Quando configurar o Azure AD de Olá, admin, Olá novo administrador nome (utilizador ou grupo) não pode já estar presente no Olá virtual principal da base de dados como um utilizador de autenticação do SQL Server. Se estiver presente, a configuração de administração do Azure AD Olá falhará; a reverter a respetiva criação e que indica que este tipo de administrador (nome) já existe. Uma vez que tal um utilizador de autenticação do SQL Server não faz parte de Olá do Azure AD, falha a qualquer servidor de toohello esforço tooconnect através da autenticação do Azure AD.
   > 


toolater remover um administrador, na parte superior de Olá de Olá **administrador do Active Directory** painel, clique em **remover administrador**e, em seguida, clique em **guardar**.

### <a name="powershell"></a>PowerShell
toorun cmdlets do PowerShell, terá de toohave Azure PowerShell instalado e em execução. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

tooprovision de administrador do Azure AD, execute Olá os seguintes comandos do PowerShell do Azure:

* Add-AzureRmAccount
* SELECT-AzureRmSubscription

Os cmdlets utilizados tooprovision e gerir o administrador do Azure AD:

| Nome do cmdlet | Descrição |
| --- | --- |
| [Conjunto AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Aprovisiona um administrador do Azure Active Directory para o servidor SQL do Azure ou do Azure SQL Data Warehouse. (Tem de ser da subscrição atual Olá.) |
| [Remover AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Remove o administrador do Azure Active Directory para o servidor SQL do Azure ou do Azure SQL Data Warehouse. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Devolve informações sobre um administrador do Azure Active Directory atualmente configurada para o servidor de SQL do Azure Olá ou o Azure SQL Data Warehouse. |

Utilizar o comando get-help toosee mais os detalhes de cada um destes comandos, por exemplo do PowerShell ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Olá seguir Aprovisiona de script com o nome de um grupo de administrador do Azure AD **DBA_Group** (id de objeto `40b79501-b343-44ed-9ce7-da4c8cc7353f`) para Olá **demo_server** servidor num grupo de recursos com o nome **23 de grupo** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Olá **DisplayName** parâmetro de entrada aceita o nome a apresentar Olá do Azure AD ou Olá Nome Principal de utilizador. Por exemplo, ``DisplayName="John Smith"`` e ``DisplayName="johns@contoso.com"``. A Olá apenas de grupos do Azure AD do Azure AD, nome a apresentar é suportado.

> [!NOTE]
> Olá comando do PowerShell do Azure ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` não impedem que aprovisionamento admins do Azure AD para os utilizadores não suportados. Um utilizador não suportado pode ser aprovisionado, mas não é possível ligar a base de dados tooa. 
> 

Olá exemplo seguinte utiliza Olá opcional **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Olá, Azure AD **ObjectID** é necessária quando hello **DisplayName** não é exclusivo. Olá tooretrieve **ObjectID** e **DisplayName** valores, utilize a secção de Active Directory Olá do Portal clássico do Azure e ver Olá propriedades de um utilizador ou grupo.
> 

Olá seguinte o exemplo devolve informações sobre a administração de Olá atual do Azure AD para o Azure SQL server:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Olá seguinte o exemplo remove um administrador do Azure AD:

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

Também pode aprovisionar um administrador de diretório do Azure Active Directory utilizando Olá REST APIs. Para obter mais informações, consulte [referência de API de REST de gestão de serviço e operações para operações de bases de dados SQL do Azure para bases de dados do Azure SQL](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
Também pode aprovisionar um administrador do Azure AD por Olá chamar comandos da CLI os seguintes:
| Comando | Descrição |
| --- | --- |
|[Criar ad-administrador do servidor de sql AZ](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Aprovisiona um administrador do Azure Active Directory para o servidor SQL do Azure ou do Azure SQL Data Warehouse. (Tem de ser da subscrição atual Olá.) |
|[eliminação de administração do ad do AZ sql server](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Remove o administrador do Azure Active Directory para o servidor SQL do Azure ou do Azure SQL Data Warehouse. |
|[lista de administração de ad AZ sql server](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Devolve informações sobre um administrador do Azure Active Directory atualmente configurada para o servidor de SQL do Azure Olá ou o Azure SQL Data Warehouse. |
|[atualização de administração do ad do AZ SQL Server](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Atualiza o administrador do Active Directory Olá para um servidor SQL do Azure ou o Azure SQL Data Warehouse. |

Para mais informações sobre comandos da CLI, consulte [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>Configurar os computadores cliente
Em todas as máquinas de cliente, de que as aplicações ou utilizadores ligam tooAzure base de dados do SQL Server ou utilizar identidades do Azure AD, o Azure SQL Data Warehouse tem de instalar Olá seguinte software:

* .NET framework 4.6 ou posterior a partir do [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Biblioteca de autenticação do Azure Active Directory para o SQL Server (**ADALSQL. DLL**) está disponível em vários idiomas (tanto x86 como amd64) do Centro de transferências Olá em [Microsoft Active Directory Authentication Library para Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

Pode satisfazer estes requisitos por:

* Instalar o [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ou [SQL Server Data Tools para Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) Olá, cumpre os requisitos do .NET Framework 4.6.
* SSMS instala a versão de Olá x86 do **ADALSQL. DLL**.
* SSDT instala a versão de amd64 Olá do **ADALSQL. DLL**.
* Olá mais recente Visual Studio do [Visual Studio Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) cumpre o requisito de Olá .NET Framework 4.6, mas não instalar a versão de amd64 necessário Olá do **ADALSQL. DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Criar utilizadores de base de dados contida na sua base de dados mapeado tooAzure identidades do AD

Autenticação do Azure Active Directory requer toobe de utilizadores de base de dados criada como utilizadores de base de dados contida. Um utilizador de base de dados contida, com base na identidade do Azure AD, é um utilizador de base de dados que não tem um início de sessão na base de dados mestra Olá e Olá, que identity de tooan maps no diretório do Azure AD que está associado a base de dados de Olá. Olá identidade do Azure AD pode ser uma conta de utilizador individual ou um grupo. Para obter mais informações sobre os utilizadores de base de dados contida, consulte [efetuar contidos utilizadores de base de dados da base de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Não não possível criar utilizadores de base de dados (com exceção de Olá dos administradores) através do portal. Funções do RBAC não são propagada tooSQL servidor, base de dados SQL ou SQL Data Warehouse. Funções do RBAC do Azure são utilizadas para gerir recursos do Azure e não aplicam permissões toodatabase. Por exemplo, Olá **contribuinte de servidor de SQL** função não concede acesso tooconnect toohello base de dados SQL ou SQL Data Warehouse. deve ser concedida permissão de acesso de Olá diretamente na base de dados de Olá com instruções Transact-SQL.
>

toocreate do Azure baseada no AD contidos da base de dados utilizador (que não seja Olá administrador do servidor que é proprietário da base de dados de Olá), se ligar toohello base de dados com uma identidade do Azure AD, como um utilizador com, pelo menos, Olá **ALTER qualquer utilizador** permissão. Em seguida, utilize Olá seguindo a sintaxe Transact-SQL:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* pode ser Olá nome principal de utilizador do Azure AD utilizador ou Olá nome a apresentar para um grupo do Azure AD.

**Exemplos:** toocreate um utilizador de base de dados contida, que representa um Azure AD federados ou geridos utilizador de domínio:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate um utilizador de base de dados contida, que representa um Azure AD ou federadas o grupo de domínio, forneça o nome a apresentar Olá de um grupo de segurança:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate um utilizador de base de dados contida, que representa uma aplicação que estabelece ligação utilizar um token do Azure AD:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  Diretamente não é possível criar um utilizador a partir de um Azure Active Directory que não sejam Olá do Azure Active Directory que está associado a sua subscrição do Azure. No entanto, os membros de outros diretórios do Active Directory que são os utilizadores importados no Olá associados do Active Directory (conhecido como utilizadores externos) pode ser adicionado grupo do Active Directory tooan no inquilino Olá do Active Directory. Ao criar um utilizador de base de dados contida para esse grupo do AD, hello os utilizadores de Olá externo do Active Directory poderem obter acesso tooSQL da base de dados.   

Para obter mais informações sobre como criar contidos base de dados de utilizadores com base em identidades do Azure Active Directory, consulte [criar utilizador (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Remover administrador Olá do Azure Active Directory para o Azure SQL server impede que qualquer utilizador de autenticação do Azure AD ligar toohello servidor. Se necessário, inutilizável utilizadores do Azure AD podem ser removidos manualmente por um administrador da base de dados SQL.   

>  [!NOTE]
>  Se receber um **ligação o tempo limite expirou**, poderá ser necessário tooset Olá `TransparentNetworkIPResolution` parâmetro toofalse de cadeia de ligação de Olá. Para obter mais informações, consulte [problema de tempo limite de ligação com o .NET Framework 4.6.1 - TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).   

   
Quando criar um utilizador de base de dados, que o utilizador recebe Olá **CONNECT** permissão e pode ligar-se a base de dados toothat como membro do Olá **pública** função. Olá inicialmente apenas permissões de utilizador toohello disponíveis são as permissões concedidas toohello **pública** função ou as permissões concedidas tooany grupos do Windows que são membros do. Depois de aprovisionar um utilizador do Azure baseada no AD contidos da base de dados, pode conceder permissões adicionais do utilizador Olá, Olá igual a forma como pode conceder permissão tooany outro tipo de utilizador. Normalmente, conceder permissões toodatabase funções e adicionar utilizadores tooroles. Para obter mais informações, consulte [Noções básicas de permissão de motor de base de dados](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Para obter mais informações sobre as funções de base de dados SQL especiais, consulte [gerir bases de dados e inícios de sessão na base de dados do Azure SQL](sql-database-manage-logins.md).
Um utilizador de domínio federado, que é importado para um domínio de gerir, tem de utilizar identidade de domínio Olá gerido.

> [!NOTE]
> Os utilizadores do AD do Azure são marcados nos metadados da base de dados de Olá com o tipo E (EXTERNAL_USER) e para os grupos com tipo X (EXTERNAL_GROUPS). Para obter mais informações, consulte [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Ligar toohello de armazém de dados ou base de dados de utilizador com o SSMS ou o SSDT  
administrador de Olá do Azure AD tooconfirm está corretamente configurado, ligar toohello **mestre** base de dados utilizando a conta de administrador Olá do Azure AD.
tooprovision do Azure AD-utilizador com base no contidos da base de dados (que não seja Olá administrador do servidor que é proprietário da base de dados de Olá) ligar toohello base de dados com uma identidade do Azure AD que tenha a base de dados do access toohello.

> [!IMPORTANT]
> Suporte para a autenticação do Azure Active Directory está disponível com [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) no Visual Studio 2015. Olá versão de Agosto de 2016 do SSMS também inclui suporte para autenticação do Active Directory Universal, que permite aos administradores toorequire multi-factor Authentication com uma chamada telefónica, mensagem de texto, os smart cards pin ou a notificação da aplicação móvel.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>Utilizar um tooconnect de identidade do Azure AD com o SSMS ou o SSDT  

Olá procedimentos a seguir mostra como tooconnect tooa SQL da base de dados com uma identidade do Azure AD utilizando o SQL Server Management Studio ou ferramentas de base de dados do SQL Server.

### <a name="active-directory-integrated-authentication"></a>Autenticação integrada do Active Directory

Utilize este método se tiver iniciado a sessão tooWindows com as suas credenciais do Azure Active Directory de um domínio federado.

1. Iniciar o Management Studio ou as ferramentas do Data e em Olá **ligar tooServer** (ou **ligar tooDatabase motor**) Olá caixa de diálogo **autenticação** caixa, selecione **Integradas no Active Directory -**. Nenhuma palavra-passe é necessária ou pode ser introduzida porque as suas credenciais existentes serão apresentados para ligação Olá.   

    ![Selecionar a autenticação integrada do AD][11]
2. Clique em Olá **opções** botão e em Olá **propriedades de ligação** página, numa Olá **ligar toodatabase** caixa, o nome do tipo Olá da base de dados de utilizador de Olá pretende tooconnect a. (Olá **ID de nome ou o inquilino de domínio do AD**"opção só é suportada para **Universal com uma ligação de MFA** opções, caso contrário, se estiver a cinzento.)  

    ![Selecione o nome de base de dados de Olá][13]

## <a name="active-directory-password-authentication"></a>Autenticação de palavra-passe do Active Directory

Utilize este método quando a ligação com um nome do principal do Azure AD utilizando Olá do Azure AD gerido domínio. Também pode utilizá-lo para uma conta federada sem domínio toohello de acesso, por exemplo, quando trabalhar remotamente.

Utilize este método se tiver iniciado a sessão tooWindows utilizando as credenciais de um domínio que não está Federado com o Azure ou ao utilizar a autenticação do Azure AD através do Azure AD com base no Olá inicial ou Olá domínio cliente.

1. Iniciar o Management Studio ou as ferramentas do Data e em Olá **ligar tooServer** (ou **ligar tooDatabase motor**) Olá caixa de diálogo **autenticação** caixa, selecione **Do Active Directory - palavra-passe**.
2. No Olá **nome de utilizador** caixa, escreva o nome de utilizador do Azure Active Directory no formato de Olá  **username@domain.com** . Tem de ser uma conta de Olá do Azure Active Directory ou uma conta de domínio federar com Olá do Azure Active Directory.
3. No Olá **palavra-passe** caixa, escreva a palavra-passe de utilizador para a conta do Azure Active Directory de Olá ou federadas conta de domínio.

    ![Selecionar a autenticação de palavra-passe do AD][12]
4. Clique em Olá **opções** botão e em Olá **propriedades de ligação** página, numa Olá **ligar toodatabase** caixa, o nome do tipo Olá da base de dados de utilizador de Olá pretende tooconnect a. (Consulte gráfico Olá na opção anterior Olá).

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>Utilizar um tooconnect de identidade do Azure AD a partir de uma aplicação cliente

Olá procedimentos a seguir mostra como tooconnect tooa SQL da base de dados com uma identidade do Azure AD a partir de uma aplicação de cliente.

###  <a name="active-directory-integrated-authentication"></a>Autenticação integrada do Active Directory

toouse autenticação integrada do Windows, o Active Directory seu domínio tem de ser federada com o Azure Active Directory. A aplicação de cliente (ou um serviço) ligar toohello base de dados tem de executar num computador associado a um domínio sob credenciais de domínio de um utilizador.

utilizando a base de dados tooconnect tooa integrado autenticação e uma identidade do Azure AD, palavra-chave de autenticação de Olá na cadeia de ligação de base de dados de Olá tem de ser definida tooActive Directory Integrated. Olá seguinte c# código de exemplo utiliza o ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

palavra-chave da cadeia de ligação de Olá ``Integrated Security=True`` não é suportada para a ligação tooAzure base de dados SQL. Quando efetuar uma ligação de ODBC, será necessário tooremove espaços e definir too'ActiveDirectoryIntegrated de autenticação '.

### <a name="active-directory-password-authentication"></a>Autenticação de palavra-passe do Active Directory

utilizando a base de dados tooconnect tooa integrado autenticação e uma identidade do Azure AD, palavra-chave de autenticação de Olá tem de ser definida tooActive palavra-passe de diretório. tem de conter o ID de utilizador/UID e palavras-chave de palavra-passe/PWD e valores de cadeia de ligação de Olá. Olá seguinte c# código de exemplo utiliza o ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Saiba mais sobre os métodos de autenticação do Azure AD com exemplos de código de demonstração de Olá disponíveis em [demonstração de GitHub de autenticação do Azure AD](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Token do Azure AD
Este método de autenticação permite que os serviços de camada média tooconnect tooAzure base de dados do SQL Server ou o Azure SQL Data Warehouse por obter um token do Azure Active Directory (AAD). Permite cenários sofisticados, incluindo a autenticação baseada em certificado. Tem de concluir quatro passos básicos toouse do Azure AD autenticação com token:

1. Registar a sua aplicação no Azure Active Directory e obter id de cliente Olá para o seu código. 
2. Crie uma aplicação Olá da representing de utilizador da base de dados. (Concluir anteriormente no passo 6).
3. Crie um certificado no execuções de computador do cliente Olá aplicação Olá.
4. Adicione certificado Olá como uma chave para a sua aplicação.

Cadeia de ligação de exemplo:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Para obter mais informações, consulte [blogue de segurança do SQL Server](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Olá, seguindo as instruções, ligar a versão 13.1 sqlcmd, que está disponível no Olá [Centro de transferências](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Passos seguintes
- Para obter uma descrição geral do acesso e controlo na Base de Dados SQL, veja [Acesso e controlo da Base de Dados SQL](sql-database-control-access.md).
- Para obter uma descrição geral de inícios de sessão, utilizadores e funções de base de dados da Base de Dados SQL, veja [Inícios de sessão, utilizadores e funções de base de dados](sql-database-manage-logins.md).
- Para obter mais informações sobre os principais de bases de dados, veja [Principals (Principais)](https://msdn.microsoft.com/library/ms181127.aspx).
- Para obter mais informações sobre as funções de base de dados, veja [Database roles (Funções de base de dados)](https://msdn.microsoft.com/library/ms189121.aspx).
- Para obter mais informações sobre as regras de firewall na Base de Dados SQL, veja [Regras de firewall da Base de Dados SQL](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

