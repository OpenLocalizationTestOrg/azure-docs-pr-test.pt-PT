---
title: "aaaUsing emulador Express toorun e depuração do Azure num computador local, o serviço em nuvem | Microsoft Docs"
description: "Utilizar o emulador Express toorun e depuração um serviço em nuvem num computador local"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Utilizar o emulador Express toorun e depuração um Azure serviço em nuvem num computador local
Ao utilizar o emulador Express, pode testar e depurar um serviço em nuvem sem executar o Visual Studio como administrador. Pode definir o seu toouse de definições do projeto ou emulador Express ou Olá emulador completo, dependendo dos requisitos de Olá do seu serviço de nuvem. Para obter mais informações sobre o emulador completo Olá, consulte [executa uma aplicação do Azure no emulador de computação de Olá](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Utilizando o emulador rápida no Visual Studio
Quando cria um projeto do Azure no Azure SDK 2.3 ou posterior, emulador Express é automaticamente utilizado. Para os projetos existentes que foram criados com uma versão anterior do Olá SDK do Azure, utilize Olá tooselect passos emulador Express os seguintes:

1. Criar ou abrir um projeto de serviço em nuvem do Azure no Visual Studio.

1. No **Explorador de soluções**, clique no projeto Olá e, no menu de contexto de Olá, selecione **propriedades**.

1. Nas páginas de propriedades de projetos de Olá, selecione Olá **Web** separador.

    ![Propriedades de um projeto de serviço em nuvem do Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Em **servidor de desenvolvimento Local**, selecione **utilize IIS Express opção**.

1. Em **emulador**, selecione **utilizar emulador Express**.
   
1. toolaunch Olá emulador Express, execute Olá os seguintes comandos numa linha de comandos: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Limitações do emulador rápida
os seguintes problemas de Olá é conhecido limitações do emulador Express: 

- Emulador Express não é compatível com o servidor Web do IIS.
- O serviço em nuvem pode conter várias funções, mas cada função é limitado tooone instância.
- Não é possível aceder a números de porta abaixo 1000. Se utilizar um fornecedor de autenticação que normalmente utiliza uma porta abaixo 1000, poderá ser necessário toochange este número de porta de tooa valor é superior a 1000.
- Quaisquer limitações que se aplicam toohello emulador de computação do Azure também se aplicam tooEmulator rápida. Por exemplo, não pode ter mais de 50 instâncias de função por implementação. Para obter mais informações sobre Olá emulador de computação do Azure, consulte [executa uma aplicação do Azure no emulador de computação de Olá](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Passos seguintes
[Depuração cloud services do Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
