---
title: "aaaConnect análise do Configuration Manager tooLog | Microsoft Docs"
description: "Este artigo mostra Olá passos tooconnect do Configuration Manager tooLog analisar dados de início e de análise."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Ligar a análise de tooLog do Configuration Manager
Pode ligar-se a análise do System Center Configuration Manager tooLog nos dados de coleção de dispositivos de toosync OMS. Isto disponibiliza dados da sua hierarquia do Configuration Manager na OMS.

## <a name="prerequisites"></a>Pré-requisitos

Análise de registos suporta ramo atual do System Center Configuration Manager, versão 1606 e planos superior.  

## <a name="configuration-overview"></a>Descrição geral de configuração
Olá passos a seguir resume Olá processo tooconnect análise tooLog do Configuration Manager.  

1. No Portal de gestão do Azure Olá, registe o Configuration Manager como uma aplicação de aplicação Web e/ou Web API e certifique-se de que tem Olá ID e o cliente chave secreta do cliente do registo de Olá do Azure Active Directory. Consulte [utilizar a aplicação do portal toocreate do Active Directory e um principal de serviço que pode aceder aos recursos](../azure-resource-manager/resource-group-create-service-principal-portal.md) para obter informações detalhadas sobre como efetuar este passo.
2. No Portal de gestão do Azure, de Olá [fornecer o Configuration Manager (aplicação de web registado Olá) com permissão tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).
3. No Configuration Manager, [adicionar uma ligação utilizando Olá Adicionar Assistente de ligação de OMS](#add-an-oms-connection-to-configuration-manager).
4. No Configuration Manager, [atualizar propriedades da ligação Olá](#update-oms-connection-properties) se a chave secreta Olá palavra-passe ou o cliente nunca expira ou se tenha perdida.
5. Com as informações do portal do OMS Olá, [transfira e instale o Microsoft Monitoring Agent de Olá](#download-and-install-the-agent) num computador de Olá com ligação de serviço do Configuration Manager Olá função do sistema de sites do ponto. agente de Olá envia tooOMS de dados do Configuration Manager.
6. Na análise de registos, [importar coleções do Configuration Manager](#import-collections) como grupos de computadores.
7. Na análise de registos, ver dados do Configuration Manager como [grupos de computadores](log-analytics-computer-groups.md).

Pode ler mais sobre a ligação do Configuration Manager tooOMS em [sincronizar os dados do Configuration Manager toohello Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Indique do Configuration Manager com permissões tooOMS
Olá procedimento seguinte fornece Olá Portal de gestão do Azure com permissões tooaccess OMS. Especificamente, tem de conceder Olá *função de contribuinte* toousers no grupo de recursos de Olá na ordem tooallow Olá Azure Management Portal tooconnect tooOMS do Configuration Manager.

> [!NOTE]
> Tem de especificar permissões no OMS para o Configuration Manager. Caso contrário, receberá uma mensagem de erro quando utilizar o Assistente de configuração de Olá no Configuration Manager.
>
>

1. Abra Olá [portal do Azure](https://portal.azure.com/) e clique em **procurar** > **análise de registos (OMS)** painel do tooopen Olá análise de registos (OMS).  
2. No Olá **análise de registos (OMS)** painel, clique em **adicionar** tooopen Olá **área de trabalho OMS** painel.  
   ![Painel do OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. No Olá **área de trabalho OMS** painel, forneça Olá seguintes informações e, em seguida, clique em **OK**.

   * **Área de trabalho do OMS**
   * **Subscrição**
   * **Grupo de recursos**
   * **Localização**
   * **Escalão de preço**  
     ![Painel do OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > exemplo de Olá acima cria um novo grupo de recursos. grupo de recursos de Olá é apenas utilizado tooprovide do Configuration Manager com área de trabalho do permissões toohello OMS neste exemplo.
     >
     >
4. Clique em **procurar** > **grupos de recursos** tooopen Olá **grupos de recursos** painel.
5. No Olá **grupos de recursos** painel, clique em grupo de recursos de Olá que criou acima tooopen Olá &lt;nome do grupo de recursos&gt; painel Definições.  
   ![Painel de definições do grupo de recursos](./media/log-analytics-sccm/sccm-azure03.png)
6. No Olá &lt;nome do grupo de recursos&gt; painel Definições, clique em Olá de tooopen (IAM) do controlo de acesso &lt;nome do grupo de recursos&gt; painel de utilizadores.  
   ![Painel de utilizadores do grupo de recursos](./media/log-analytics-sccm/sccm-azure04.png)  
7. No Olá &lt;nome do grupo de recursos&gt; painel de utilizadores, clique em **adicionar** tooopen Olá **adicionar acesso** painel.
8. No Olá **adicionar acesso** painel, clique em **selecionar uma função**e, em seguida, selecione Olá **contribuinte** função.  
   ![Selecione uma função](./media/log-analytics-sccm/sccm-azure05.png)  
9. Clique em **adicionar utilizadores**, selecione o utilizador do Gestor de configuração Olá, clique em **selecione**e, em seguida, clique em **OK**.  
   ![Adicionar utilizadores](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Adicionar um tooConfiguration de ligação do OMS Manager
Ordem tooadd uma ligação do OMS, ambiente do Configuration Manager tem de ter um [ponto de ligação de serviço](https://technet.microsoft.com/library/mt627781.aspx) configurados para o modo online.

1. No Olá **administração** área de trabalho do Configuration Manager, selecione **OMS conector**. Esta ação abre Olá **Adicionar Assistente de ligação do OMS**. Selecione **seguinte**.
2. No Olá **geral** ecrã, confirme que efetuou Olá ações a seguir e que que tenha os detalhes para cada item, em seguida, selecione **seguinte**.

   1. Olá, no Portal de gestão do Azure, tiver registado do Configuration Manager como uma aplicação de aplicação Web e/ou Web API e de que tem Olá [ID de cliente do registo de Olá](../active-directory/active-directory-integrating-applications.md).
   2. Olá Portal de gestão do Azure, criou uma chave de segredo da aplicação Olá aplicação registada no Azure Active Directory.  
   3. Olá Portal de gestão do Azure, forneceu Olá web registado aplicação com permissão tooaccess OMS.  
      ![Página de assistente geral de tooOMS de ligação](./media/log-analytics-sccm/sccm-console-general01.png)
3. No Olá **do Azure Active Directory** ecrã, configure o seu tooOMS de definições de ligação, fornecendo o **inquilino** , **ID de cliente** , e **chave de segredo do cliente**  , em seguida, selecione **seguinte**.  
   ![Página de assistente do Azure Active Directory tooOMS de ligação](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Se tiver efetuado Olá todos os outros procedimentos com êxito, em seguida, Olá informações sobre Olá **configuração da ligação OMS** ecrã serão apresentadas automaticamente nesta página. As informações de definições de ligação de Olá deverão ser apresentados para sua **subscrição do Azure** , **grupo de recursos do Azure** , e **área de trabalho do Operations Management Suite**.  
   ![Página de ligação do assistente OMS tooOMS de ligação](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Assistente de Olá liga toohello OMS serviço, utilizando as informações de Olá que tiver de entrada. Selecione as coleções de dispositivos de Olá que pretende toosync com o OMS e, em seguida, clique em **adicionar**.  
   ![Selecione as coleções](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Verifique as definições de ligação no Olá **resumo** ecrã, em seguida, selecione **seguinte**. Olá **progresso** ecrã mostra o estado da ligação Olá, em seguida, deve **concluída**.

> [!NOTE]
> Tem de ligar o site de nível superior do OMS toohello na sua hierarquia. Se ligar OMS tooa um site primário autónomo e, em seguida, adicionar um ambiente de tooyour do site de administração central, irá ter toodelete e recrie Olá OMS ligação na hierarquia Olá de novo.
>
>

Depois de ter ligado tooOMS do Configuration Manager, pode adicionar ou remover coleções e ver propriedades de Olá de Olá ligação OMS.

## <a name="update-oms-connection-properties"></a>Atualizar propriedades de ligação do OMS
Se uma chave secreta de cliente ou a palavra-passe nunca expira ou se tenha perdida, terá de propriedades de ligação do toomanually atualização Olá OMS.

1. No Configuration Manager, navegue até demasiado**serviços em nuvem** , em seguida, selecione **OMS conector** tooopen Olá **propriedades de ligação do OMS** página.
2. Nesta página, clique em Olá **do Azure Active Directory** separador tooview sua **inquilino**, **ID de cliente**, **expiração chave secreta de cliente**. **Certifique-se** sua **chave secreta do cliente** se tiver expirado.

## <a name="download-and-install-hello-agent"></a>Transfira e instale o agente de Olá
1. No portal do OMS Olá, [transferir ficheiro de configuração do agente de Olá da OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Utilize um dos Olá seguintes métodos tooinstall e configurar o agente de Olá no computador de Olá com a função de sistema ao site do ponto de ligação Olá do Configuration Manager service:
   * [Instalar o agente de Olá utilizando o programa de configuração](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Instalar o agente de Olá utilizando a linha de comandos Olá](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Instalar o agente de Olá utilizando DSC na automatização do Azure](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Importar coleções
Depois de ter adicionado um tooConfiguration de ligação do OMS Manager e Olá agente foi instalado no computador de Olá com ligação de serviço do Configuration Manager Olá função de sistema de sites do ponto, Olá passo seguinte consiste em tooimport coleções do Configuration Manager na OMS como grupos de computadores.

Após a importação estiver ativada, as informações de associação de coleção de Olá são obtidas todos os 3 horas tookeep Olá coleção associações atuais. Pode escolher toodisable importação em qualquer altura.

1. No portal do OMS Olá, clique em **definições**.
2. Clique em Olá **grupos de computadores** separador e, em seguida, clique em Olá **SCCM** separador.
3. Selecione **associações de coleção do Gestor de configuração da importação** e, em seguida, clique em **guardar**.  
   ![Grupos de computadores - separador SCCM](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Ver dados do Configuration Manager
Depois de ter adicionado um tooConfiguration de ligação do OMS Manager e Olá agente foi instalado no computador de Olá com a função de sistema ao site do ponto de ligação Olá do Configuration Manager service, tooOMS são enviados dados de agente Olá. Na OMS, as coleções do Configuration Manager aparecem como [grupos de computadores](log-analytics-computer-groups.md). Pode ver grupos Olá Olá **do Configuration Manager** página em **grupos de computadores** no **definições**.

Após Olá coleções são importadas, pode ver que foram detetados como quantos computadores com associações de coleção. Também pode ver o número de Olá de coleções que tenham sido importados.

![Grupos de computadores - separador SCCM](./media/log-analytics-sccm/sccm-computer-groups02.png)

Ao clicar em qualquer um, abre-se de pesquisa, apresentar o todas Olá importado grupos ou todos os computadores que pertencem tooeach grupo. Utilizar [pesquisa registo](log-analytics-log-searches.md), pode iniciar uma análise aprofundada de dados do Configuration Manager.

## <a name="next-steps"></a>Passos seguintes
* Utilize [pesquisa registo](log-analytics-log-searches.md) tooview informações detalhadas sobre os dados do Configuration Manager.
