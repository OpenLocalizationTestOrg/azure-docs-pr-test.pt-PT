---
title: aaaManage Azure Analysis Services | Microsoft Docs
description: Saiba como toomanage um Analysis Services server no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Gerir do Analysis Services
Depois de criar um servidor de Analysis Services no Azure, poderão existir algumas tarefas de administração e gestão terá tooperform de imediato ou algum tempo baixo Olá viagem. Por exemplo, execute o processamento de dados de atualização de toohello, controlar quem pode aceder à modelos Olá no seu servidor, ou monitorizar estado de funcionamento do seu servidor. Algumas tarefas de gestão só podem ser efetuadas no portal do Azure, outros no SQL Server Management Studio (SSMS), e algumas tarefas podem ser efetuadas no.

## <a name="azure-portal"></a>Portal do Azure
[Portal do Azure](http://portal.azure.com/) é onde pode criar e eliminar servidores, monitorizar os recursos do servidor, altere o tamanho e gerir quem tem acesso tooyour servidores.  Se estiver a ter alguns problemas, também pode submeter um pedido de suporte.

![Obter o nome do servidor no Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Ligar o servidor tooyour no Azure é semelhante à ligação tooa instância de servidor na sua própria organização. Do SSMS, pode efetuar muitas das Olá mesmo tarefas como processamento de dados ou criar um script de processamento, gerir funções e utilizar o PowerShell.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Transfira e instale o SSMS
tooget Olá todas as funcionalidades mais recentes e experiência smoothest Olá ao ligar o servidor de Analysis Services do Azure tooyour, certifique-se de que está a utilizar a versão mais recente do Olá do SSMS. 

[Transferir o SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect com SSMS
 Quando com o SSMS, antes de hello do servidor tooyour ao ligar pela primeira vez, certifique-se de que o seu nome de utilizador está incluído no grupo de administradores de serviços de análise Olá. toolearn mais, consulte [os administradores de servidores](#server-administrators) posteriormente neste artigo.

1. Antes de ligar, precisa de nome do servidor tooget Olá. No **portal do Azure** > servidor > **descrição geral** > **nome do servidor**, nome do servidor de Olá de cópia.
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. No SSMS > **Object Explorer**, clique em **Connect** > **Analysis Services**.
3. No Olá **ligar tooServer** caixa de diálogo, colar no nome do servidor de Olá, em seguida, em **autenticação**, escolha um dos seguintes tipos de autenticação de Olá:
   
    **Autenticação do Windows** toouse as credenciais de domínio ome de utilizador e palavra-passe do Windows.

    **Autenticação de palavra-passe do Active Directory** toouse uma conta organizacional. Por exemplo, quando ligar a partir de um domínio associado a um computador.

    **Autenticação de Universal do Active Directory** toouse [autenticação não interativa ou multifator](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Se ligar no SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Os administradores de servidores e os utilizadores de base de dados
No Azure Analysis Services, existem dois tipos de utilizadores, os administradores de servidores e os utilizadores de base de dados. Ambos os tipos de utilizadores tem de estar no seu Azure Active Directory e tem de ser especificados por endereço de e-mail empresarial ou UPN. toolearn mais, consulte [permissões de autenticação e utilizador](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Resolução de problemas de ligação
Ao estabelecer ligação com o SSMS, caso se depare com problemas, poderá ter de cache de início de sessão de Olá tooclear. Nada é toodisc em cache. tooclear Olá cache, feche e reinicie Olá ligar o processo. 

## <a name="next-steps"></a>Passos seguintes
Se já não tiver implementado um modelo em tabela tooyour novo servidor, agora é uma boa altura. toolearn mais, consulte [implementar tooAzure Analysis Services](analysis-services-deploy.md).

Se tiver implementado um servidor de tooyour modelo, está tooit tooconnect pronto a utilizar um cliente ou browser. toolearn mais, consulte [obter dados a partir do servidor de Analysis Services do Azure](analysis-services-connect.md).

