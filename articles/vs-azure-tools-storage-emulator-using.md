---
title: "aaaConfiguring e utilizar Olá emulador do Storage com o Visual Studio | Microsoft Docs"
description: "Configurar e utilizar Olá emulador do Storage com o Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Configurar e utilizar Olá emulador do Storage com o Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Descrição geral
ambiente de desenvolvimento de SDK do Azure Olá inclui Olá emulador do storage um utilitário que simula Olá tabela, fila e Blob dos serviços de armazenamento disponíveis no Azure no seu computador de desenvolvimento local. Se estiver a criar um serviço em nuvem que utiliza serviços de armazenamento do Azure Olá ou escrever qualquer aplicação externa que chamadas Olá dos serviços de armazenamento, pode testar código localmente no emulador do storage Olá. Ferramentas do Azure Olá para Microsoft Visual Studio integrar a gestão do emulador do storage Olá no Visual Studio. Ferramentas do Azure Olá inicializar Olá armazenamento emulador da base de dados na primeira utilização, inicia Olá serviço de emulador de armazenamento, quando executada ou depurar o seu código a partir do Visual Studio e fornece acesso só de leitura toohello emulador os dados de armazenamento através de Olá Explorador de armazenamento do Azure.

Para obter informações detalhadas no emulador do storage Olá, incluindo os requisitos de sistema e instruções de configuração personalizada, consulte [Olá utilizar emulador do Storage do Azure para desenvolvimento e teste](storage/common/storage-use-emulator.md).

> [!NOTE]
> Existem algumas diferenças de funcionalidade entre simulação de emulador de armazenamento Olá e serviços do storage do Azure Olá. Consulte [diferenças entre Olá emulador de armazenamento e serviços de armazenamento do Azure](storage/common/storage-use-emulator.md) no Olá documentação do Azure SDK para obter informações sobre as diferenças específicas de Olá.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Configurar uma cadeia de ligação para o emulador do storage Olá
tooaccess Olá emulador do storage a partir do código de uma função deverá tooconfigure uma ligação de cadeia que emulador do storage toohello pontos e que pode ser posteriormente alterada toopoint tooan conta do storage do Azure. Uma cadeia de ligação é uma definição de configuração que pode ler a função na conta de armazenamento do tempo de execução tooconnect tooa. Para obter mais informações sobre como ver cadeias de ligação de toocreate [Olá configurar aplicação Azure](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> Pode devolver uma conta de emulador de armazenamento de toohello referência a partir do código utilizando Olá **DevelopmentStorageAccount** propriedade. Esta abordagem funciona corretamente se quiser tooaccess Olá emulador do storage a partir do código, mas se planear toopublish tooAzure sua aplicação, será necessário toocreate um tooaccess de cadeia de ligação a sua conta do storage do Azure e modificar o seu código toouse que cadeia de ligação antes de o publicar. Se estiver oscila frequentemente entre a conta de emulador de armazenamento Olá e uma conta de armazenamento do Azure, uma cadeia de ligação irá simplificar este processo.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>A inicializar e executar o emulador do storage Olá
Pode especificar que quando executa ou depurar o seu serviço no Visual Studio, Visual Studio inicia automaticamente emulador do storage Olá. No Explorador de soluções, abra o menu de atalho Olá para sua **Azure** projeto e escolha **propriedades**. No Olá **desenvolvimento** separador, Olá **iniciar emulador do Storage de Azure** lista, escolha **verdadeiro** (se não estiver já definido toothat valor).

Olá pela primeira vez, executar ou depurar o seu serviço do Visual Studio, o emulador do storage Olá inicia um processo de inicialização. Este processo reserva portas locais para o emulador do storage Olá e cria a base de dados de emulador de armazenamento de Olá. Depois de concluído, este processo não precisa de toorun novamente, a menos que a base de dados de emulador de armazenamento de Olá é eliminada.

> [!NOTE]
> A partir da versão de Junho de 2012 Olá do Olá ferramentas do Azure, o emulador de armazenamento Olá é executado, por predefinição, no SQL Server Express LocalDB. Nas versões anteriores do Olá ferramentas do Azure, o emulador do storage Olá é executada relativamente a uma instância predefinida do SQL Express 2005 ou 2008, que é necessário instalar antes de pode instalar Olá SDK do Azure. Também pode executar o emulador do storage Olá em relação a uma instância nomeada do SQL Server Express ou com um nome ou a instância predefinida do Microsoft SQL Server. Se precisar de tooconfigure Olá armazenamento emulador toorun em relação a uma instância diferente de instância predefinida de Olá, consulte [Olá utilizar emulador do Storage do Azure para desenvolvimento e teste](storage/common/storage-use-emulator.md).
> 
> 

emulador do storage Olá fornece um utilizador interface tooview Olá dos serviços de armazenamento local Olá e toostart, pare e repô-las. Assim que o serviço de emulador de armazenamento Olá foi iniciado, pode apresentar a interface de utilizador Olá ou iniciar ou parar o serviço de Olá clicando com o ícone da área de notificação Olá para Olá emulador do Microsoft Azure, na barra de tarefas do Olá Windows.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Visualizar os dados de emulador de armazenamento no Explorador de servidores
nó de armazenamento do Azure Olá no Explorador de servidores permite-lhe as definições de dados e alteração tooview de blob e dados da tabela nas suas contas do storage, incluindo Olá emulador do storage. Consulte [recursos de gerir o armazenamento de Blobs do Azure com o Explorador de armazenamento (pré-visualização)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) para obter mais informações.

