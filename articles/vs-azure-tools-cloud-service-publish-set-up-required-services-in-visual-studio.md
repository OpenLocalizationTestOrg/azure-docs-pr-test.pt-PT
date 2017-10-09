---
title: "aaaPrepare toopublish ou implementar uma aplicação do Azure a partir do Visual Studio | Microsoft Docs"
description: "Saiba mais Olá tooset de procedimentos dos serviços de conta de nuvem e de armazenamento e configurar a sua aplicação do Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>Preparar tooPublish ou implementar uma aplicação do Azure a partir do Visual Studio
## <a name="overview"></a>Descrição geral
Antes de poder publicar um projeto de serviço em nuvem, tem de configurar Olá os seguintes serviços:

* A **serviço em nuvem** toorun as funções no Olá ambiente do Azure
* A **conta de armazenamento** que fornece acesso toohello os serviços tabela, fila e Blob.

Utilize Olá seguir procedimentos tooset configurar estes serviços e configurar a sua aplicação

## <a name="create-a-cloud-service"></a>Criar um serviço cloud
toopublish um tooAzure do serviço de nuvem, tem primeiro de criar um serviço em nuvem, que executa as funções no Olá ambiente do Azure. Pode criar um serviço em nuvem no Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885), conforme descrito na secção de Olá **toocreate um serviço em nuvem utilizando o portal clássico do Azure de Olá**, mais adiante neste tópico. Também pode criar um serviço em nuvem no Visual Studio, utilizando o Assistente para publicar Olá.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate um serviço em nuvem utilizando o Visual Studio
1. Abra o menu de atalho Olá para Olá projeto do Azure e escolha **publicar**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Se não tiver iniciado sessão, iniciar sessão com o nome de utilizador e palavra-passe para a conta do Microsoft hello ou uma conta organizacional associado à sua subscrição do Azure.
3. Escolha Olá **seguinte** botão tooadvance toohello **definições** página.

    ![Definições comuns do Assistente de publicação](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. No Olá **serviços em nuvem** lista, escolha **criar novo**. Olá **criar serviços do Azure** é apresentada a caixa de diálogo.
5. Introduza o nome de Olá do seu serviço em nuvem. o nome de Olá faz parte do URL de Olá para o seu serviço e, por conseguinte, tem de ser globalmente exclusivo. nome de Olá não é sensível.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate um serviço em nuvem utilizando Olá portal clássico do Azure
1. Inicie sessão no toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkId=253103) no Web site da Microsoft hello.
2. toodisplay (opcional) uma lista de serviços em nuvem que já criou, escolha a ligação de serviços em nuvem Olá no lado esquerdo do Olá da página Olá.
3. Escolha Olá  **+**  ícone na Olá inferior esquerda canto e, em seguida, escolha **serviço em nuvem** no menu de Olá que aparece. Ecrã outra com duas opções, **criação rápida** e **criação personalizada**, é apresentada. Se optar por **criação rápida**, pode criar um serviço em nuvem especificando o URL e Olá a região em que esta será fisicamente alojada. Se optar por **criação personalizada**, pode publicar imediatamente um serviço em nuvem, especificando um pacote (ficheiro. cspkg), um ficheiro de configuração (. cscfg) e um certificado. Criação personalizada não é necessária se tenciona toopublish seu serviço em nuvem utilizando Olá **publicar** comando num projeto do Azure. Olá **publicar** comando está disponível no menu de atalho Olá para um projeto do Azure.
4. Escolha **criação rápida** toolater publicar o serviço de nuvem utilizando o Visual Studio.
5. Especifique um nome do serviço em nuvem. URL de conclusão de Olá é apresentada a seguinte toohello nome.
6. Na lista de Olá, escolha a região olá onde está localizadas a maior parte dos utilizadores.
7. Em Olá parte inferior da janela de Olá, escolha Olá **criar serviço de nuvem** ligação.

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
Uma conta do storage fornece acesso toohello os serviços tabela, fila e Blob. Pode criar uma conta de armazenamento utilizando o Visual Studio ou Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate uma conta de armazenamento utilizando o Visual Studio
1. No **Explorador de soluções**, abra menu de atalho Olá para Olá **armazenamento** nó e, em seguida, escolha **criar conta de armazenamento**.

    ![Criar uma nova conta de armazenamento do Azure](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Selecione ou introduza Olá seguintes informações para Olá nova conta do storage no Olá **criar conta de armazenamento** caixa de diálogo.

   * Olá toowhich de subscrição do Azure que pretende que a conta de armazenamento de Olá tooadd.
   * nome de Olá pretende toouse Olá nova conta de armazenamento.
   * região Olá ou grupo de afinidade, (por exemplo, EUA Oeste ou Ásia Oriental).
   * Olá, tipo de replicação que pretende toouse Olá conta de armazenamento, tal como com redundância geográfica.
3. Quando tiver terminado, escolha **criar**.hello nova conta de armazenamento é apresentado no Olá **armazenamento** lista **Explorador de servidores**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate uma conta de armazenamento utilizando Olá portal clássico do Azure
1. Inicie sessão no toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkId=253103) no Web site da Microsoft hello.
2. (Opcional) tooview as contas do storage, escolha Olá **armazenamento** ligação no painel de Olá do Olá à esquerda do lado da página Olá.
3. No canto inferior esquerdo de Olá da página Olá, escolha Olá  **+**  ícone.
4. No menu de Olá que surgir, selecione **armazenamento**e, em seguida, escolha **criação rápida**.
5. Dê um nome que irá resultar num url exclusivo de conta de armazenamento Olá.
6. Dê um nome de serviço de nuvem. URL de conclusão de Olá é apresentada a seguinte toohello nome.
7. Na lista de Olá das regiões, escolha uma região onde está localizadas a maior parte dos utilizadores.
8. Especifique se pretende tooenable georreplicação. Se ativar a georreplicação, os dados serão guardados em várias localizações físicas tooreduce Olá hipótese de perda. Esta funcionalidade torna o armazenamento mais dispendioso, mas pode reduzir o custo de Olá Ativando geolocalização quando cria a conta de armazenamento Olá em vez de adicionar a funcionalidade de Olá mais tarde. Para obter mais informações, consulte [georreplicação](http://go.microsoft.com/fwlink/?LinkId=253108).
9. Em Olá parte inferior da janela de Olá, escolha Olá **criar conta de armazenamento** ligação.

Depois de criar a sua conta do storage, verá Olá URLs que pode utilizar os recursos de tooaccess em cada um dos serviços de armazenamento do Azure Olá e também Olá chaves de acesso primária e secundária para a sua conta. Utilizar estas chaves pedidos tooauthenticate realizados em serviços de armazenamento Olá.

> [!NOTE]
> chave de acesso secundária de Olá fornece Olá mesmo aceder à conta de armazenamento tooyour como chave de acesso primária de Olá e é gerado uma cópia de segurança a chave de acesso primária comprometida. Além disso, é recomendado que voltar a gerar as chaves de acesso regularmente. Pode modificar uma ligação cadeia definição toouse Olá chave secundária ao regenerar a chave primária Olá, em seguida, pode modificar chave primária do toouse Olá regenerada ao regenerar a chave secundária Olá.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Configurar os serviços de toouse aplicação fornecidos pela conta de armazenamento Olá
Tem de configurar qualquer função que acede ao armazenamento serviços toouse Olá serviços storage do Azure que criou. toodo, pode utilizar várias configurações de serviço para o projeto do Azure. Por predefinição, dois são criadas no seu projeto do Azure. Ao utilizar várias configurações de serviço, pode utilizar Olá mesma ligação da cadeia no seu código, mas tem um valor diferente para uma cadeia de ligação na configuração de cada serviço. Por exemplo, pode utilizar um toorun de configuração de serviço e depurar a aplicação localmente, utilizando o emulador de armazenamento do Azure de Olá e um toopublish de configuração de serviço diferente tooAzure sua aplicação. Para obter mais informações sobre configurações de serviço, consulte [configurar o Azure projeto através de várias configurações de serviço](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>Fornece os serviços de toouse de aplicação Olá conta de armazenamento de tooconfigure
1. No Visual Studio, abra a solução do Azure. No Explorador de soluções, abra o menu de atalho Olá para cada função no projeto do Azure que acede ao serviços de armazenamento Olá e escolha **propriedades**. É apresentada uma página com o nome de Olá da função de Olá no editor do Visual Studio Olá. página Olá apresenta Olá os campos para Olá **configuração** separador.
2. Nas páginas de propriedade de Olá para a função de Olá, escolha **definições**.
3. No Olá **a configuração do serviço** lista, escolha o nome de Olá Olá da configuração do serviço que quiser tooedit. Se pretender que as alterações de toomake tooall das configurações de serviço Olá para esta função, pode escolher **todas as configurações**.  Para obter mais informações sobre como tooupdate service configurações, consulte a secção de Olá **gerir cadeias de ligação de contas do Storage** tópico Olá [configurar funções de Olá para um serviço em nuvem do Azure com o Visual Studio ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify quaisquer definições de cadeia de ligação, escolha Olá **...** botão de seguinte toohello definição. Olá **criar cadeia de ligação de armazenamento** é apresentada a caixa de diálogo.
5. Em **estabelecer ligação utilizando**, escolha Olá **sua subscrição** opção.
6. No Olá **subscrição** lista, escolha a sua subscrição. Se a lista Olá de subscrições não incluem Olá aquele que pretende, escolha Olá **transferir definições de publicação** ligação.
7. No Olá **nome da conta** lista, escolha o nome da sua conta de armazenamento. Ferramentas do Azure obtém automaticamente as credenciais da conta de armazenamento utilizando o ficheiro. publishsettings de Olá. toospecify credenciais manualmente, a sua conta do storage escolha Olá **introduzir manualmente as credenciais** opção e, em seguida, continuar com este procedimento. Pode obter o nome da conta de armazenamento e a chave primária de Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885). Se não quiser toospecify definições da conta de armazenamento manualmente, escolha Olá **OK** caixa de diálogo do botão tooclose Olá.
8. Escolha Olá **introduza a conta de armazenamento** ligação de credenciais.
9. No Olá **nome da conta** box, introduza o nome de Olá da sua conta de armazenamento.

   > [!NOTE]
   > Iniciar sessão Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885)e, em seguida, escolha Olá **armazenamento** botão. portal de Olá mostra uma lista de contas de armazenamento. Se escolher uma conta, é aberta uma página para o mesmo. Pode copiar nome Olá Olá da conta de armazenamento a partir desta página. Se estiver a utilizar uma versão anterior do portal clássico Olá, nome de Olá da sua conta de armazenamento é apresentado na Olá **contas do Storage** vista. toocopy este nome destacá-la no Olá **propriedades** janela deste ver e, em seguida, escolha as chaves de Olá Ctrl-C. nome de Olá toopaste no Visual Studio, escolha Olá **nome da conta** texto caixa e, em seguida, escolha as chaves de Ctrl + V Olá.
   >
   >
10. No Olá **chave da conta** caixa, introduza a chave primária, ou copie e cole-o de Olá [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
     toocopy neste chave:

    1. Em Olá parte inferior da página Olá para a conta de armazenamento adequado Olá, escolha Olá **gerir chaves** botão.
    2. No Olá **gerir chaves de acesso** página, selecione o texto de Olá da chave de acesso primária de Olá e, em seguida, escolha as chaves de Ctrl + C Olá.
    3. Nas ferramentas do Azure, cole a chave de Olá Olá **chave da conta** caixa.
    4. Tem de selecionar uma das Olá toodetermine opções a seguir como serviço Olá acedem à conta de armazenamento Olá:

       * **Utilizar HTTP**. Esta é a opção de padrão de Olá. Por exemplo, `http://<account name>.blob.core.windows.net`.
       * **Utilizar o HTTPS** para uma ligação segura. Por exemplo, `https://<accountname>.blob.core.windows.net`.
       * **Especifique os pontos finais personalizados** para cada um dos Olá três serviços. Em seguida, pode escrever estes pontos finais no campo Olá para serviço específico Olá.

         > [!NOTE]
         > Se criar os pontos finais personalizados, pode criar uma cadeia de ligação mais complexa. Quando utilizar este formato de cadeia, pode especificar pontos finais de serviço de armazenamento que incluem um nome de domínio personalizado que registou para a sua conta de armazenamento com Olá serviço Blob. Também pode conceder acesso apenas tooblob recursos num contentor único através de uma assinatura de acesso partilhado. Para obter mais informações sobre como toocreate pontos finais personalizados, consulte [configurar cadeias de ligação de armazenamento do Azure](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave estas alterações de cadeia de ligação, escolha Olá **OK** botão e, em seguida, escolha Olá **guardar** botão na barra de ferramentas Olá. Depois de guardar estas alterações, pode obter valor Olá esta cadeia de ligação no código utilizando [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Quando publicar a aplicação tooAzure, escolha a configuração do serviço Olá que contenha Olá conta de armazenamento do Azure para a cadeia de ligação de Olá. Depois da aplicação for publicada, certifique-se de que a aplicação Olá funciona conforme esperado nos serviços de armazenamento do Azure Olá

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a publicação de aplicações tooAzure do Visual Studio, consulte [publicação de um serviço em nuvem com as ferramentas do Azure de Olá](vs-azure-tools-publishing-a-cloud-service.md).
