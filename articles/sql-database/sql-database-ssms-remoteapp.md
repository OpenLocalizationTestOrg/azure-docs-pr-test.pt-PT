---
title: aaaConnect tooSQL base de dados utilizando o SQL Server Management Studio no Azure RemoteApp | Microsoft Docs
description: "Utilize este tutorial toolearn como toouse SQL Server Management Studio no Azure RemoteApp para segurança e desempenho ao ligar tooSQL da base de dados"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Utilizar o SQL Server Management Studio no Azure RemoteApp tooconnect tooSQL da base de dados

> [!IMPORTANT]
> O Azure RemoteApp está a ser descontinuado. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
>

## <a name="introduction"></a>Introdução
Este tutorial mostra como toouse SQL Server Management Studio (SSMS) no Azure RemoteApp tooconnect tooSQL da base de dados. Orienta Olá processo de configuração de SQL Server Management Studio no Azure RemoteApp, explica as vantagens de Olá e mostra as funcionalidades de segurança que pode utilizar no Azure Active Directory.

**Estimado tempo toocomplete:** 45 minutos

## <a name="ssms-in-azure-remoteapp"></a>SSMS no Azure RemoteApp
O Azure RemoteApp é um serviço RDS no Azure que fornece as aplicações. Pode saber mais acerca do mesmo aqui: [que é o RemoteApp?](../remoteapp/remoteapp-whatis.md)

SSMS em execução no Azure RemoteApp fornecem Olá a mesma experiência como executar localmente o SSMS.

![Captura de ecrã com SSMS em execução no Azure RemoteApp][1]

## <a name="benefits"></a>Benefícios
Existem muitas vantagens toousing SSMS no Azure RemoteApp, incluindo:

* A porta 1433 no Azure SQL server não tem toobe exposto externamente (fora do Azure).
* Tookeep sem necessidade de adicionar e remover endereços IP na firewall do servidor de SQL do Azure de Olá.
* Todas as ligações do Azure RemoteApp ocorrem através de HTTPS utilizando a porta 443 encriptados protocolo de ambiente de trabalho remoto
* É multiutilizador e pode dimensionar.
* Há um ganhos de desempenho de ter o SSMS no Olá mesma região que Olá base de dados SQL.
* Pode auditar a utilização do Azure RemoteApp com a edição de Premium Olá do Azure Active Directory que tem os relatórios de atividade do utilizador.
* Pode ativar a autenticação multifator (MFA).
* O acesso SSMS em qualquer local quando utilizar qualquer um dos Olá suportado clientes do Azure RemoteApp que inclui o iOS, Android, Mac, Windows Phone e PCs Windows.

## <a name="create-hello-azure-remoteapp-collection"></a>Criar coleção do Olá do Azure RemoteApp
Seguem-se Olá passos toocreate a coleção do RemoteApp do Azure com o SSMS:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Criar uma nova VM do Windows da imagem
Utilize Olá "Windows Server remoto ambiente de trabalho sessão anfitrião Windows Server 2012 R2" de imagem de Olá Galeria toomake a nova VM.

### <a name="2-install-ssms-from-sql-express"></a>2. Instalar o SSMS do SQL Server Express
Vá para Olá nova VM e navegue até a página de transferência toothis: [rápida do Microsoft® SQL Server® 2014](https://www.microsoft.com/download/details.aspx?id=42299)

Há uma transferência de tooonly opção SSMS. Após a transferência, vá para o diretório de instalação de Olá e execute a configuração tooinstall SSMS.

Também precisa de tooinstall SQL Server 2014 Service Pack 1. Poderá transferi-lo aqui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 inclui uma funcionalidade essencial para trabalhar com a SQL Database do Azure.

### <a name="3-run-validate-script-and-sysprep"></a>3. Executar script de validar e Sysprep
No Olá ambiente de trabalho de Olá VM é um script de PowerShell chamado validar. Execute este fazendo duplo clique em. Irá verificar que esse Olá VM está pronto toobe utilizada para alojar remoto de aplicações. Quando a verificação estiver concluída, pedirá toorun sysprep - escolha toorun-lo.

Quando o sysprep estiver concluída, será encerrado Olá VM.

toolearn mais sobre a criação de uma imagem do Azure RemoteApp, consulte: [como toocreate um modelo do RemoteApp imagem no Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Captura de imagem
Quando Olá VM parou de funcionar, encontrá-lo no portal atual Olá e capturá-la.

toolearn mais informações sobre a capturar uma imagem do utilizador, consulte [capturar uma imagem de uma máquina virtual de Azure Windows criada com o modelo de implementação clássica Olá](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. Adicionar imagens de modelo do RemoteApp tooAzure
No Azure RemoteApp secção portal atual Olá Olá, aceda a toohello separador de imagens de modelo e clique em Adicionar. Na caixa de pop-up Olá, selecione "Importar uma imagem a partir da sua biblioteca de máquinas virtuais" e, em seguida, escolha Olá imagem que acabou de criar.

### <a name="6-create-cloud-collection"></a>6. Criar a coleção na nuvem
No portal atual Olá, crie uma nova coleção de nuvem do RemoteApp do Azure. Escolha Olá imagem de modelo que acabou de importar com o SSMS instalado no mesmo.

![Criar nova coleção na nuvem][2]

### <a name="7-publish-ssms"></a>7. Publicar SSMS
No Olá publicação separador da sua nova coleção de nuvem, selecione de publicar uma aplicação Olá Menu Iniciar e, em seguida, escolha SSMS Olá lista.

![Publicar aplicações][5]

### <a name="8-add-users"></a>8. Adicionar utilizadores
No separador de acesso de utilizador de Olá pode selecionar os utilizadores de Olá que terão acesso toothis Azure RemoteApp coleção que inclui apenas o SSMS.

![Adicionar Utilizador][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Instalar a aplicação de cliente do Azure RemoteApp Olá
Pode transferir e instalar um cliente do Azure RemoteApp aqui: [transferir | O Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Configurar o servidor SQL do Azure
Olá apenas configuração necessária é tooensure serviços do Azure está ativada para firewall de Olá. Se utilizar esta solução, em seguida, não terá tooadd qualquer IP endereços tooopen Olá firewall. tráfego de rede de Olá permitido toohello do SQL Server é a partir de outros serviços do Azure.

![Permitir do Azure][4]

## <a name="multi-factor-authentication-mfa"></a>Autenticação Multifator (MFA)
MFA pode ser ativado especificamente para esta aplicação. Aceda toohello separador de aplicações do Azure Active Directory. Irá encontrar uma entrada para o Microsoft Azure RemoteApp. Se clique essa aplicação e, em seguida, configurar, será apresentada a página de Olá abaixo onde pode ativar a MFA para esta aplicação.

![Ativar a MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Auditoria de atividade do utilizador com o Azure Active Directory Premium
Se não tiver do Azure AD Premium e, em seguida, tiver tooturn-lo na Olá secção de licenças do seu diretório. Com o Premium ativado, pode atribuir utilizadores ao nível do toohello Premium.

Quando acede tooa utilizador no Azure Active Directory, em seguida, pode aceder toohello atividade separador toosee início de sessão informações tooAzure RemoteApp.

## <a name="next-steps"></a>Passos seguintes
Depois de concluir todos os Olá os passos acima, que será capaz de toorun Olá Azure RemoteApp cliente e iniciar sessão com um utilizador atribuído. Será apresentada com o SSMS como uma das suas aplicações e pode executá-lo, tal como faria se foi instalado no seu computador com o SQL server tooAzure acesso.

Para obter mais informações sobre como toomake Olá tooSQL de ligação da base de dados, consulte [ligar tooSQL da base de dados com o SQL Server Management Studio e executar uma consulta de T-SQL de exemplo](sql-database-connect-query-ssms.md).

Tudo o que é por agora. Divirta-se!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png