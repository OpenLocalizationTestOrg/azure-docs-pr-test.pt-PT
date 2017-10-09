---
title: requisitos de aaaApp para o Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre os requisitos de Olá para aplicações que pretende que o toouse no Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>Requisitos de aplicações
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

O Azure RemoteApp suporta transmissão em fluxo 32 bits ou 64 bits baseados em Windows aplicações a partir de uma imagem do Windows Server 2012 R2. A maioria das existente 32 bits ou 64 bits baseados em Windows as aplicações são executadas "tal como está" no Azure RemoteApp (Serviços de ambiente de trabalho remoto ou anteriormente conhecido como os serviços de Terminal) ambiente. No entanto, há uma diferença entre a execução e também - algumas aplicações funcionarem corretamente e execute, enquanto outros não. Olá informações a seguir fornece orientações para desenvolver aplicações num ambiente de serviços de ambiente de trabalho remoto e testar tooensure compatibilidade.

Sugestão: Estamos a trabalhar criar alguns exemplos de trabalho de aplicações para si. Verá o novo tópicos que abordam através do Microsoft Access, QuickBooks e App-V no RemoteApp.

## <a name="requirements"></a>Requisitos
Estes três requisitos, se seguidos, ajudam a sua aplicação executada corretamente no RemoteApp:

1. As aplicações que cumpre todos os [requisitos de certificação para aplicações de ambiente de trabalho do Windows](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx) e respeitar demasiado[diretrizes de programação dos serviços de ambiente de trabalho remoto](https://msdn.microsoft.com/library/aa383490.aspx) terão concluída compatibilidade com o RemoteApp.
2. As aplicações devem nunca armazenar dados localmente na imagem de Olá ou instâncias do RemoteApp que podem ser perdidas.  Depois de criar uma coleção do RemoteApp, instâncias de Olá são Clonadas são sem monitorização de estado e só devem conter as aplicações. Armazenar dados de uma origem externa ou no perfil do utilizador Olá.
3. Imagens personalizadas nunca devem conter dados que podem ser perdidos.  

## <a name="testing-your-apps"></a>Testar as suas aplicações
Utilize estas aplicações de tootesting passos:

1. Instalar o Windows Server 2012 R2 e a sua aplicação
2. Ativar o Ambiente de Trabalho Remoto
3. Crie duas contas de utilizador, UserA e UserB, adicionar o grupo de segurança do utilizador contas toohello ambiente de trabalho remoto.
4. Verificar a compatibilidade da sessão multi através do estabelecimento de dois em simultâneo RDS sessões toohello PC ao iniciar a aplicação Olá.
5. Validar o comportamento da aplicação

## <a name="application-development-guidelines"></a>Orientações de desenvolvimento de aplicações
Utilize Olá seguir as diretrizes para desenvolver aplicações do RemoteApp.

### <a name="multiple-users"></a>Vários utilizadores
* Instalar um [aplicação para um único utilizador ](https://msdn.microsoft.com/library/aa380661.aspx)podem criar problemas num ambiente multiuser.
* As aplicações devem [armazenar informações específicas do utilizador](https://msdn.microsoft.com/library/aa383452.aspx) em localizações específicas do utilizador, em separado de informações globais que se aplica tooall utilizadores.
* RemoteApp utiliza vários [espaços de nomes de objetos de kernel](https://msdn.microsoft.com/library/aa382954.aspx); um espaço de nomes global é utilizado principalmente pelo services em aplicações de cliente/servidor.
* Não é seguro tooassume que Olá nome do computador ou Olá [endereço IP](https://msdn.microsoft.com/library/aa382942.aspx) toohello atribuído computador estão associados um único utilizador porque vários utilizadores podem ter sessão iniciados em simultâneo tooa anfitrião de sessões de ambiente de trabalho remoto (RD sessão Servidor de anfitrião).

### <a name="performance"></a>Desempenho
* Desativar [efeitos gráfico](https://msdn.microsoft.com/library/aa380822.aspx) antes de adicionar o seu tooRemoteApp de aplicação.
* disponibilidade de toomaximize da CPU para todos os utilizadores, quer desativar [em segundo plano tarefas ](https://msdn.microsoft.com/library/aa380665.aspx) ou criar tarefas de segundo plano eficiente que não são intensivas em recursos.
* Deve otimizar e equilibrar aplicação [thread utilização](https://msdn.microsoft.com/library/aa383520.aspx) para um ambiente multiuser, multiprocessador.
* desempenho de toooptimize, é boa prática para aplicações demasiado[detetar](https://msdn.microsoft.com/library/aa380798.aspx) se estiverem a executar uma sessão de cliente.

