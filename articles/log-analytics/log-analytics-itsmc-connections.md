---
title: "Suportado ligações com o conector de gestão do serviço de TI no Log Analytics do Azure | Microsoft Docs"
description: "Este artigo fornece informações sobre como ligar os produtos/serviços ITSM conector de gestão de serviço com TI (ITSMC) na análise de registos do OMS para monitorizar e gerir itens de trabalho ITSM centralmente."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2018
ms.author: v-jysur
ms.openlocfilehash: a51ba4b45b7f6c72037d5c562a4ccd59e601cee4
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/24/2018
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector"></a>Ligar ITSM produtos/serviços com o conector de gestão do serviço de TI
Este artigo fornece informações sobre como configurar a ligação entre o ITSM produtos/serviços e o conector de gestão do serviço de TI (ITSMC) no Log Analytics para gerir centralmente os itens de trabalho. Para obter mais informações sobre ITSMC, consulte [descrição geral](log-analytics-itsmc-overview.md).

São suportados os seguintes ITSM produtos/serviços. Selecione o produto para ver informações detalhadas sobre como ligar o produto ao ITSMC.

- [O System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-azure)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-azure)
- [Provance](#connect-provance-to-it-service-management-connector-in-azure)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-azure)

> [!NOTE]

> Conector ITSM só podem ligar a instâncias de ServiceNow baseado na nuvem. Instâncias de ServiceNow no local não são atualmente suportadas.

## <a name="connect-system-center-service-manager-to-it-service-management-connector-in-azure"></a>Ligar o System Center Service Manager para o serviço de TI conector de gestão no Azure

As secções seguintes fornecem detalhes sobre como ligar o seu produto do System Center Service Manager para ITSMC no Azure.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que são cumpridos os seguintes pré-requisitos:

- ITSMC instalado. Obter mais informações: [adicionar a solução de conector de gestão de serviço de TI](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).
- A aplicação Web do Service Manager (aplicação Web) é implementada e configurada. Informações sobre a aplicação Web são [aqui](#create-and-deploy-service-manager-web-app-service).
- Ligação híbrida criada e configurada. Obter mais informações: [configurar a ligação de híbrida](#configure-the-hybrid-connection).
- As versões do Service Manager: 2012 R2 ou 2016.
- A função de utilizador: [operador avançado](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Procedimento de ligação

Utilize o procedimento seguinte para ligar a instância do System Center Service Manager para ITSMC:

1. No portal do Azure, aceda a **todos os recursos** e procure **ServiceDesk(YourWorkspaceName)**

2.  Em **ORIGENS de dados da área de trabalho** clique **ITSM ligações**.

    ![Nova ligação](./media/log-analytics-itsmc/add-new-itsm-connection.png)

3. Na parte superior do painel da direita, clique em **adicionar**.

4. Forneça as informações, tal como descrito na seguinte tabela e clique em **OK** para criar a ligação.

> [!NOTE]

> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome da Ligação**   | Escreva um nome para a instância do System Center Service Manager que pretende estabelecer ligação com ITSMC.  Utilize este nome mais tarde quando configurar os itens de trabalho nesta instância / ver a análise de registos detalhados. |
| **Tipo de parceiro**   | Selecione **do System Center Service Manager**. |
| **URL do servidor**   | Escreva o URL da aplicação Web do Service Manager. Obter mais informações sobre a aplicação Web do Service Manager são [aqui](#create-and-deploy-service-manager-web-app-service).
| **ID de cliente**   | Escreva o ID de cliente que gerou (utilizando o script automático) para autenticar a aplicação Web. Mais informações sobre o script automatizado [aqui.](log-analytics-itsmc-service-manager-script.md)|
| **Segredo do cliente**   | Escreva o segredo de cliente gerado para este ID.   |
| **Âmbito de sincronização de dados**   | Selecione os itens de trabalho do Service Manager que pretende sincronizar através de ITSMC.  Estes itens são importados para análise de registos de trabalho. **Opções:** incidentes, pedidos de alteração.|
| **Dados de sincronização** | Escreva o número de últimos dias que pretende que os dados da. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender criar itens de configuração no produto ITSM. Quando selecionada, o OMS cria o IC afectado como itens de configuração (em caso de não existente CIs) no sistema ITSM suportado. **Predefinição**: desativado. |

![Ligação do Service manager](./media/log-analytics-itsmc/service-manager-connection.png)

**Quando ligado com êxito e sincronizadas**:

- Itens de trabalho selecionado do Service Manager são importados para o Azure **análise de registos.** Pode ver o resumo dos seguintes itens de trabalho no mosaico do conector de gestão de serviços de TI.

- Pode criar incidentes a partir dos alertas de análise de registos ou registos ou a partir dos alertas do Azure nesta instância do Service Manager.


Saiba mais: [itens de trabalho de criar ITSM para alertas de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-alerts), [itens de trabalho de criar ITSM de registos de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-log-records) e [itens de trabalho de criar ITSM de alertas do Azure](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Criar e implementar o serviço de aplicações web do Service Manager

Para ligar o Gestor de serviços no local com ITSMC no Azure, Microsoft criou uma aplicação Web do Service Manager no GitHub.

Para configurar a aplicação ITSM Web para o Gestor do serviço, efetue o seguinte:

- **Implementar a aplicação Web** – implemente a aplicação Web, definir as propriedades e autenticar com o Azure AD. Pode implementar a aplicação web utilizando o [automatizada script](log-analytics-itsmc-service-manager-script.md) que Microsoft tem lhe forneceu.
- **Configurar a ligação híbrida** - [configurar esta ligação](#configure-the-hybrid-connection), manualmente.

#### <a name="deploy-the-web-app"></a>Implementar a aplicação web
Utilize o automatizada [script](log-analytics-itsmc-service-manager-script.md) para implementar a aplicação Web, definir as propriedades e autenticar com o Azure AD.

Execute o script, fornecendo os seguintes detalhes necessários:

- Detalhes da subscrição do Azure
- Nome do grupo de recursos
- Localização
- Detalhes do servidor do Service Manager (nome do servidor, domínio, nome de utilizador e palavra-passe)
- Prefixo de nome de site para a sua aplicação Web
- Espaço de nomes de barramento de serviço.

O script cria a aplicação Web utilizando o nome que especificou (juntamente com alguns cadeias adicionais para o tornar único). Gera o **URL da aplicação Web**, **ID de cliente** e **segredo do cliente**.

Guarde os valores, poderá utilizá-los quando criar uma ligação com ITSMC.

**Verifique a instalação da aplicação Web**

1. Aceda a **portal do Azure** > **recursos**.
2. Selecione a aplicação Web, clique em **definições** > **definições da aplicação**.
3. Confirme as informações sobre a instância do Service Manager que forneceu no momento da implementação de aplicação através do script.

### <a name="configure-the-hybrid-connection"></a>Configurar a ligação híbrida

Utilize o procedimento seguinte para configurar a ligação híbrida que se liga a instância do Service Manager com ITSMC no Azure.

1. Localizar a aplicação Web do Service Manager, em **recursos do Azure**.
2. Clique em **definições** > **redes**.
3. Em **ligações híbridas**, clique em **configurar pontos finais da sua ligação híbrida**.

    ![Rede de ligação híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. No **ligações híbridas** painel, clique em **adicionar ligação híbrida**.

    ![Adicionar ligação híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. No **as ligações híbridas de adicionar** painel, clique em **híbrida de criar nova ligação**.

    ![Nova ligação híbrida](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Escreva os seguintes valores:

    - **Nome do ponto final**: Especifique um nome para a nova ligação híbrida.
    -  **Anfitrião de ponto final**: FQDN do servidor de gestão do Service Manager.
    - **Porta do ponto final**: escreva 5724
    - **Espaço de nomes de barramento de serviço**: Utilize um espaço de nomes de barramento de serviço existente ou crie um novo.
    - **Localização**: selecione a localização.
    -  **Nome**: Especifique um nome para o barramento de serviço, se estiver a criar.

    ![Valores de ligação híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Clique em **OK** para fechar o **criar a ligação híbrida** painel e começar a criar a ligação híbrida.

    Depois de criar a ligação híbrida, é apresentado sob o painel.

7. Depois de criar a ligação híbrida, selecione a ligação e clique em **adicionar selecionada da ligação híbrida**.

    ![Nova ligação híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-the-listener-setup"></a>Configurar o programa de configuração do serviço de escuta

Utilize o procedimento seguinte para configurar o programa de configuração do serviço de escuta para a ligação híbrida.

1. No **ligações híbridas** painel, clique em **transferir o Gestor de ligações** e instalá-lo no computador onde a instância do System Center Service Manager está em execução.

    Assim que a instalação estiver concluída, **IU do Gestor de ligações híbridas** opção está disponível em **iniciar** menu.

2. Clique em **IU do Gestor de ligações híbridas** , será solicitado para as suas credenciais do Azure.

3. Início de sessão com as suas credenciais do Azure e selecionar a sua subscrição onde foi criada a ligação híbrida.

4. Clique em **Guardar**.

A ligação híbrida foi ligada com êxito.

![ligação híbrida com êxito](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Depois da híbrida ligação é criada, certifique-se e testar a ligação, visitando a aplicação Web do Service Manager implementada. Certifique-se de que a ligação é efetuada com êxito antes de tentar ligar ao ITSMC no Azure.

A imagem de exemplo seguinte mostra os detalhes de uma ligação com êxito:

![Teste de ligação híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-to-it-service-management-connector-in-azure"></a>Ligar o ServiceNow ao serviço de TI conector de gestão no Azure

As secções seguintes fornecem detalhes sobre como ligar o ServiceNow produto ITSMC no Azure.

### <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que são cumpridos os seguintes pré-requisitos:
- ITSMC instalado. Obter mais informações: [adicionar a solução de conector de gestão de serviço de TI](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).
- Versões suportadas do ServiceNow: Jakarta, Istanbul, Helsinki, Geneva

**Administradores do ServiceNow tem de fazer o seguinte na sua instância do ServiceNow**:
- Geram o ID de cliente e o segredo do cliente para o produto de ServiceNow. Para obter informações sobre como gerar ID de cliente e o segredo, consulte as seguintes informações conforme necessário:

    - [Configurar a OAuth para Jakarta](https://docs.servicenow.com/bundle/jakarta-platform-administration/page/administer/security/task/t_SettingUpOAuth.html)
    - [Configurar a OAuth para Istanbul](https://docs.servicenow.com/bundle/istanbul-platform-administration/page/administer/security/task/t_SettingUpOAuth.html)
    - [Configurar a OAuth para Helsinki](https://docs.servicenow.com/bundle/helsinki-platform-administration/page/administer/security/task/t_SettingUpOAuth.html)
    - [Configurar a OAuth para Geneva](https://docs.servicenow.com/bundle/geneva-servicenow-platform/page/administer/security/task/t_SettingUpOAuth.html)


- Instale a aplicação de utilizador para a integração da Microsoft OMS (ServiceNow aplicação). [Saiba mais](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.1 ).
- Crie função de utilizador de integração para a aplicação de utilizador instalada. Informações sobre como criar a função de utilizador de integração são [aqui](#create-integration-user-role-in-servicenow-app).

### <a name="connection-procedure"></a>**Procedimento de ligação**
Utilize o procedimento seguinte para criar uma ligação de ServiceNow:


1. No portal do Azure, aceda a **todos os recursos** e procure **ServiceDesk(YourWorkspaceName)**

2.  Em **ORIGENS de dados da área de trabalho** clique **ITSM ligações**.
    ![Nova ligação](./media/log-analytics-itsmc/add-new-itsm-connection.png)

3. Na parte superior do painel da direita, clique em **adicionar**.

4. Forneça as informações, tal como descrito na seguinte tabela e clique em **OK** para criar a ligação.


> [!NOTE]
> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome da Ligação**   | Escreva um nome para a instância do ServiceNow que pretende estabelecer ligação com ITSMC.  Utilize este nome mais tarde no OMS quando configurar os itens de trabalho neste ITSM / ver a análise de registos detalhados. |
| **Tipo de parceiro**   | Selecione **ServiceNow**. |
| **Nome de Utilizador**   | Escreva o nome de utilizador de integração que criou na aplicação para suportar a ligação ao ITSMC ServiceNow. Obter mais informações: [ServiceNow criar função de utilizador de aplicação](#create-integration-user-role-in-servicenow-app).|
| **Palavra-passe**   | Escreva a palavra-passe associada este nome de utilizador. **Tenha em atenção**: nome de utilizador e palavra-passe são utilizados para gerar tokens de autenticação apenas e não são armazenadas em qualquer lugar no âmbito do serviço ITSMC.  |
| **URL do servidor**   | Escreva o URL da instância do ServiceNow que pretende ligar à ITSMC. |
| **ID de cliente**   | Escreva o ID de cliente que pretende utilizar para autenticação de OAuth2, o que é gerado anteriormente.  Obter mais informações sobre a geração de ID de cliente e o segredo: [configuração de OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **Segredo do cliente**   | Escreva o segredo de cliente gerado para este ID.   |
| **Âmbito de sincronização de dados**   | Selecione os itens de trabalho do ServiceNow que quer sincronizar a análise de registos do Azure, através de ITSMC.  Os valores selecionados são importados para análise de registos.   **Opções:** incidentes e pedidos de alteração.|
| **Dados de sincronização** | Escreva o número de últimos dias que pretende que os dados da. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender criar itens de configuração no produto ITSM. Quando selecionada, ITSMC cria o IC afectado como itens de configuração (em caso de não existente CIs) no sistema ITSM suportado. **Predefinição**: desativado. |

![Ligação de ServiceNow](./media/log-analytics-itsmc/itsm-connection-servicenow-connection-latest.png)

**Quando ligado com êxito e sincronizadas**:

- Itens de trabalho selecionados da instância do ServiceNow são importados para o Azure **análise de registos.** Pode ver o resumo dos seguintes itens de trabalho no mosaico do conector de gestão de serviços de TI.

- Pode criar incidentes a partir dos alertas de análise de registos ou registos ou a partir dos alertas do Azure nesta instância do ServiceNow.

Saiba mais: [itens de trabalho de criar ITSM para alertas de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-alerts), [itens de trabalho de criar ITSM de registos de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-log-records) e [itens de trabalho de criar ITSM de alertas do Azure](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).

### <a name="create-integration-user-role-in-servicenow-app"></a>Criar função de utilizador de integração na aplicação do ServiceNow

Utilizador o seguinte procedimento:

1.  Visite o [ServiceNow arquivo](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.1) e instalar o **aplicação de utilizador para ServiceNow e a integração do Microsoft OMS** na sua instância do ServiceNow.
2.  Após a instalação, visite a barra de navegação esquerdo da instância do ServiceNow, pesquisa e selecione integrador de Microsoft OMS.  
3.  Clique em **lista de verificação de instalação**.

    O estado é apresentado como **não concluir** se a função de utilizador ainda está a ser criado.

4.  Nas caixas de texto, junto a **criar o utilizador de integração**, introduza o nome de utilizador para o utilizador que possam ligar à ITSMC no Azure.
5.  Introduza a palavra-passe para este utilizador e clique em **OK**.  

>[!NOTE]

> Utilizar estas credenciais para efetuar a ligação do ServiceNow no Azure.

O utilizador recentemente criado será apresentado com as funções predefinidas atribuídas.

**Predefinição funções**:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   ITIL
-   template_editor
-   view_changer

Depois do utilizador foi criado com êxito, o estado de **Verifique a lista de verificação de instalação** move como concluído, listar os detalhes da função de utilizador criados para a aplicação.

> [!NOTE]

> Para permitir que um utilizador crie **alertas** e **eventos** no ServiceNow a partir do Azure:

> - Certifique-se de que tem o módulo de gestão de eventos instalada na sua instância do ServiceNow.

> - Adicione as seguintes funções para o utilizador de integração:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-to-it-service-management-connector-in-azure"></a>Ligar Provance ao serviço de TI conector de gestão no Azure

As secções seguintes fornecem detalhes sobre como ligar o seu produto Provance ITSMC no Azure.


### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que são cumpridos os seguintes pré-requisitos:


- ITSMC instalado. Obter mais informações: [adicionar a solução de conector de gestão de serviço de TI](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).
- Aplicação de provance deve ser registada com o Azure AD - e ID de cliente é disponibilizado. Para obter informações detalhadas, consulte [como configurar a autenticação do Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

- A função de utilizador: administrador.

### <a name="connection-procedure"></a>Procedimento de ligação

Utilize o procedimento seguinte para criar uma ligação de Provance:

1. No portal do Azure, aceda a **todos os recursos** e procure **ServiceDesk(YourWorkspaceName)**

2.  Em **ORIGENS de dados da área de trabalho** clique **ITSM ligações**.
    ![Nova ligação](./media/log-analytics-itsmc/add-new-itsm-connection.png)

3. Na parte superior do painel da direita, clique em **adicionar**.

4. Forneça as informações, tal como descrito na seguinte tabela e clique em **OK** para criar a ligação.

> [!NOTE]

> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome da Ligação**   | Escreva um nome para a instância de Provance que pretende estabelecer ligação com ITSMC.  Utilize este nome mais tarde quando configurar os itens de trabalho neste ITSM / ver a análise de registos detalhados. |
| **Tipo de parceiro**   | Selecione **Provance**. |
| **Nome de Utilizador**   | Escreva o nome de utilizador que possam ligar à ITSMC.    |
| **Palavra-passe**   | Escreva a palavra-passe associada este nome de utilizador. **Nota:** nome de utilizador e palavra-passe são utilizados para gerar tokens de autenticação apenas e não são armazenadas em qualquer lugar no âmbito do serviço ITSMC. _|
| **URL do servidor**   | Escreva o URL da sua instância Provance que pretende ligar à ITSMC. |
| **ID de cliente**   | Escreva o ID de cliente para autenticar esta ligação, que gerou na sua instância Provance.  Obter mais informações sobre o ID de cliente, consulte [como configurar a autenticação do Active Directory](../app-service/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Âmbito de sincronização de dados**   | Selecione os itens de trabalho Provance que quer sincronizar a análise de registos do Azure, através de ITSMC.  Estes itens são importados para análise de registos de trabalho.   **Opções:** incidentes, pedidos de alteração.|
| **Dados de sincronização** | Escreva o número de últimos dias que pretende que os dados da. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender criar itens de configuração no produto ITSM. Quando selecionada, ITSMC cria o IC afectado como itens de configuração (em caso de não existente CIs) no sistema ITSM suportado. **Predefinição**: desativado.|

![Ligação provance](./media/log-analytics-itsmc/itsm-connections-provance-latest.png)

**Quando ligado com êxito e sincronizadas**:

- Itens de trabalho selecionado desta instância Provance são importados para o Azure **análise de registos.** Pode ver o resumo dos seguintes itens de trabalho no mosaico do conector de gestão de serviços de TI.

- Pode criar incidentes a partir dos alertas de análise de registos ou registos ou a partir dos alertas do Azure nesta instância Provance.

Saiba mais: [itens de trabalho de criar ITSM para alertas de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-alerts), [itens de trabalho de criar ITSM de registos de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-log-records) e [itens de trabalho de criar ITSM de alertas do Azure](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).

## <a name="connect-cherwell-to-it-service-management-connector-in-azure"></a>Ligar Cherwell ao serviço de TI conector de gestão no Azure

As secções seguintes fornecem detalhes sobre como ligar o seu produto Cherwell ITSMC no Azure.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que são cumpridos os seguintes pré-requisitos:

- ITSMC instalado. Obter mais informações: [adicionar a solução de conector de gestão de serviço de TI](log-analytics-itsmc-overview.md#adding-the-it-service-management-connector-solution).
- ID de cliente gerado. Obter mais informações: [geram o ID de cliente para Cherwell](#generate-client-id-for-cherwell).
- A função de utilizador: administrador.

### <a name="connection-procedure"></a>Procedimento de ligação

Utilize o procedimento seguinte para criar uma ligação de Provance:

1. No portal do Azure, aceda a **todos os recursos** e procure **ServiceDesk(YourWorkspaceName)**

2.  Em **ORIGENS de dados da área de trabalho** clique **ITSM ligações**.
    ![Nova ligação](./media/log-analytics-itsmc/add-new-itsm-connection.png)

3. Na parte superior do painel da direita, clique em **adicionar**.

4. Forneça as informações, tal como descrito na seguinte tabela e clique em **OK** para criar a ligação.

> [!NOTE]

> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome da Ligação**   | Escreva um nome para a instância de Cherwell que pretende ligar à ITSMC.  Utilize este nome mais tarde quando configurar os itens de trabalho neste ITSM / ver a análise de registos detalhados. |
| **Tipo de parceiro**   | Selecione **Cherwell.** |
| **Nome de Utilizador**   | Escreva o nome de utilizador Cherwell que possam ligar à ITSMC. |
| **Palavra-passe**   | Escreva a palavra-passe associada este nome de utilizador. **Nota:** nome de utilizador e palavra-passe são utilizados para gerar tokens de autenticação apenas e não são armazenadas em qualquer lugar no âmbito do serviço ITSMC.|
| **URL do servidor**   | Escreva o URL da sua instância Cherwell que pretende ligar à ITSMC. |
| **ID de cliente**   | Escreva o ID de cliente para autenticar esta ligação, que gerou na sua instância Cherwell.   |
| **Âmbito de sincronização de dados**   | Selecione os itens de trabalho Cherwell que pretende sincronizar através de ITSMC.  Estes itens são importados para análise de registos de trabalho.   **Opções:** incidentes, pedidos de alteração. |
| **Dados de sincronização** | Escreva o número de últimos dias que pretende que os dados da. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender criar itens de configuração no produto ITSM. Quando selecionada, ITSMC cria o IC afectado como itens de configuração (em caso de não existente CIs) no sistema ITSM suportado. **Predefinição**: desativado. |


![Ligação provance](./media/log-analytics-itsmc/itsm-connections-cherwell-latest.png)

**Quando ligado com êxito e sincronizadas**:

- Itens de trabalho selecionado desta instância Cherwell são importados para o Azure **análise de registos.** Pode ver o resumo dos seguintes itens de trabalho no mosaico do conector de gestão de serviços de TI.

- Pode criar incidentes a partir dos alertas de análise de registos ou registos ou a partir dos alertas do Azure nesta instância Cherwell.

Saiba mais: [itens de trabalho de criar ITSM para alertas de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-alerts), [itens de trabalho de criar ITSM de registos de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-log-records) e [itens de trabalho de criar ITSM de alertas do Azure](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts).

### <a name="generate-client-id-for-cherwell"></a>Geram o ID de cliente para Cherwell

Para gerar o chave/ID de cliente para Cherwell, utilize o seguinte procedimento:

1. Inicie sessão na sua instância Cherwell como administrador.
2. Clique em **segurança** > **as definições de cliente de API de REST editar**.
3. Selecione **criar novo cliente** > **segredo do cliente**.

    ![Id de utilizador Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Passos Seguintes
 - [Criar itens de trabalho ITSM para alertas de análise de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-alerts)
 - [Criar itens de trabalho ITSM do registo de análise de registos de registos de registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-log-analytics-log-records)
 - [Criar itens de trabalho ITSM a partir dos alertas do Azure](log-analytics-itsmc-overview.md#create-itsm-work-items-from-azure-alerts)
