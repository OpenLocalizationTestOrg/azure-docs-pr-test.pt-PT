---
title: "ligações de aaaITSM no conector de gestão do serviço de TI do OMS | Microsoft Docs"
description: "Ligar os seus produtos/serviços ITSM com o conector de gestão do serviço de TI no OMS toocentrally monitor e gerir itens de trabalho ITSM Olá."
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
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>Ligar ITSM produtos/serviços com o conector de gestão de serviços de TI (pré-visualização)
Este artigo fornece informações sobre como tooconnect sua tooIT de produtos/serviços ITSM conector do serviço de gestão no OMS e centralmente gerir itens de trabalho. Obter mais informações sobre o conector de gestão de serviços de TI, consulte [descrição geral](log-analytics-itsmc-overview.md).

Olá produtos/serviços a seguir é suportada:

- [O System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>Ligar o System Center Service Manager tooIT conector de gestão de serviço no OMS

Olá secções seguintes fornecem detalhes sobre como tooconnect toohello de produto do System Center Service Manager conector de gestão de serviços de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que tem Olá pré-requisitos cumpridos os seguintes:

- Conector de gestão do serviço IT instalado.
Obter mais informações: [configuração](log-analytics-itsmc-overview.md#configuration).
- Olá aplicação Web do Service Manager (aplicação Web) é implementado e configurado. Informações sobre a aplicação Web são [aqui](#create-and-deploy-service-manager-web-app-service).
- Ligação híbrida criada e configurada. Obter mais informações: [híbrida de Olá configurar ligação](#configure-the-hybrid-connection).
- As versões do Service Manager: 2012 R2 ou 2016.
- A função de utilizador: [operador avançado](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Procedimento de ligação

Utilize Olá tooconnect procedimento a seguir a toohello de instância do System Center Service Manager conector de gestão de serviços de TI:

1. Aceda demasiado**OMS** >**definições** > **origens ligadas**.
2. Selecione **ITSM conector,** clique **Adicionar nova ligação**.

    ![Do Service manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Fornecer informações de Olá, conforme descrito em Olá a tabela seguinte e clique em **guardar** ligação de Olá toocreate:

> [!NOTE]
> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Escreva um nome para a instância do System Center Service Manager Olá que pretende que o tooconnect com Olá conector de gestão de serviços de TI.  Utilize este nome mais tarde quando configurar os itens de trabalho nesta instância / ver a análise de registos detalhados. |
| **Selecione o tipo de ligação**   | Selecione **do System Center Service Manager**. |
| **URL do servidor**   | Introduza o URL de Olá do Olá aplicação Web do Service Manager. Obter mais informações sobre a aplicação Web do Service Manager são [aqui](#create-and-deploy-service-manager-web-app-service).
| **ID de cliente**   | Escreva o ID de cliente de Olá que gerado (utilizando o script automático Olá) para autenticar a aplicação Web de Olá. Mais informações sobre o script de Olá automatizada [aqui.](log-analytics-itsmc-service-manager-script.md)|
| **Segredo do cliente**   | Segredo do cliente do tipo Olá, gerado para este ID.   |
| **Âmbito de sincronização de dados**   | Selecione itens de trabalho do Service Manager Olá que pretende que o toosync através de Olá conector de gestão de serviços de TI.  Estes itens são importados para análise de registos de trabalho. **Opções:** incidentes, pedidos de alteração.|
| **Dados de sincronização** | Escreva o número de Olá dos últimos dias que pretende que os dados de Olá do. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender que os itens de configuração de Olá toocreate no produto ITSM Olá. Quando selecionada, o OMS cria Olá afetado CIs como itens de configuração (em caso de não existente CIs) no Olá suportados sistema ITSM. **Predefinição**: desativado. |

Quando ligado com êxito e sincronizada com êxito:

- Itens de trabalho selecionado do Service Manager são importados para o OMS **análise de registos.** Pode ver o resumo de Olá destes itens de trabalho no mosaico de conector de gestão de serviços de TI Olá.

- Da OMS, pode criar incidentes a partir dos alertas do OMS ou de pesquisa de registo, nesta instância do Service Manager.

Obter mais informações: [itens de trabalho de criar ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [itens de trabalho de criar ITSM do OMS registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Criar e implementar o serviço de aplicações web do Service Manager

tooconnect Olá Gestor do serviço no local com Olá conector de gestão de serviços de TI na OMS, a Microsoft criou uma aplicação Web do Service Manager no Olá GitHub.

tooset cópia de segurança Olá ITSM Web aplicação para o Gestor do serviço, Olá seguintes:

- **Aplicação de Web de Olá implementar** – implementar a aplicação Web de Olá, definir propriedades de Olá e autenticar com o Azure AD. Pode implementar a aplicação web de Olá utilizando Olá [automatizada script](log-analytics-itsmc-service-manager-script.md) que Microsoft tem lhe forneceu.
- **Configurar a ligação híbrida de Olá** - [configurar esta ligação](#configure-the-hybrid-connection), manualmente.

#### <a name="deploy-hello-web-app"></a>Implementar a aplicação web de Olá
Olá utilize automatizada [script](log-analytics-itsmc-service-manager-script.md) toodeploy Olá aplicação Web, definir propriedades de Olá e autenticar com o Azure AD.

Execute o script de Olá fornecendo Olá os detalhes necessários:

- Detalhes da subscrição do Azure
- Nome do grupo de recursos
- Localização
- Detalhes do servidor do Service Manager (nome do servidor, domínio, nome de utilizador e palavra-passe)
- Prefixo de nome de site para a sua aplicação Web
- Espaço de nomes de barramento de serviço.

Olá script cria Olá Web app através da nome Olá que especificou (juntamente com alguns cadeias adicionais toomake-exclusivo). Gera Olá **URL da aplicação Web**, **ID de cliente** e **segredo do cliente**.

Guardar valores Olá, poderá utilizá-los quando criar uma ligação com o conector de gestão do serviço de TI.

**Verifique a instalação da aplicação Olá Web**

1. Aceda demasiado**portal do Azure** > **recursos**.
2. Selecione a aplicação Web de Olá, clique em **definições** > **definições da aplicação**.
3. Confirme as informações de Olá sobre a instância do Service Manager Olá fornecida no momento de Olá da implementação de aplicação Olá através de script de Olá.

### <a name="configure-hello-hybrid-connection"></a>Configurar a ligação híbrida de Olá

Utilize Olá seguir o procedimento tooconfigure Olá da ligação híbrida que se liga a instância do Service Manager Olá com Olá conector de gestão de serviços de TI no OMS.

1. Localizar Olá aplicação Web do Service Manager, em **recursos Azure**.
2. Clique em **definições** > **redes**.
3. Em **ligações híbridas**, clique em **configurar pontos finais da sua ligação híbrida**.

    ![Rede de ligação híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. No Olá **ligações híbridas** painel, clique em **adicionar ligação híbrida**.

    ![Adicionar ligação híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. No Olá **as ligações híbridas de adicionar** painel, clique em **híbrida de criar nova ligação**.

    ![Nova ligação híbrida](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Escreva Olá os seguintes valores:

    - **Nome do ponto final**: Especifique um nome da ligação híbrida nova do Olá.
    -  **Anfitrião de ponto final**: FQDN do servidor de gestão do Service Manager Olá.
    - **Porta do ponto final**: escreva 5724
    - **Espaço de nomes de barramento de serviço**: Utilize um espaço de nomes de barramento de serviço existente ou crie um novo.
    - **Localização**: selecione a localização de Olá.
    -  **Nome**: especificar um barramento de serviço do nome toohello se estiver a criar.

    ![Valores de ligação híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Clique em **OK** tooclose Olá **criar a ligação híbrida** painel e iniciar a criação da ligação híbrida Olá.

    Depois da ligação híbrida Olá é criada, será apresentado no painel de Olá.

7. Após a criação da ligação híbrida Olá, selecione a ligação de Olá e clique em **adicionar selecionada da ligação híbrida**.

    ![Nova ligação híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Configurar a configuração do serviço de escuta Olá

Utilize Olá seguir o procedimento tooconfigure Olá escuta a configuração da ligação híbrida de Olá.

1. No Olá **ligações híbridas** painel, clique em **transferência Olá Gestor de ligações** e instalá-lo na máquina de olá onde a instância do System Center Service Manager está em execução.

    Depois de concluída, a instalação de Olá **IU do Gestor de ligações híbridas** opção está disponível em **iniciar** menu.

2. Clique em **IU do Gestor de ligações híbridas** , será solicitado para as suas credenciais do Azure.

3. Início de sessão com as suas credenciais do Azure e selecionar a sua subscrição onde foi criado Olá da ligação híbrida.

4. Clique em **Guardar**.

A ligação híbrida foi ligada com êxito.

![ligação híbrida com êxito](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Após a criação da ligação híbrida Olá, verificar e testar a ligação de Olá, visitando Olá implementar a aplicação de Web do Service Manager. Certifique-se de que a ligação de Olá é efetuada com êxito antes de tentar tooconnect toohello conector de gestão de serviços de TI no OMS.

Olá imagem seguinte mostra os detalhes de Olá de uma ligação com êxito:

![Teste de ligação híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>Ligar o ServiceNow tooIT conector de gestão de serviço no OMS

Olá secções seguintes fornecem detalhes sobre como tooconnect toohello de produto do ServiceNow conector de gestão de serviços de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que tem Olá pré-requisitos cumpridos os seguintes:

- Conector de gestão do serviço IT instalado. Obter mais informações: [configuração.](log-analytics-itsmc-overview.md#configuration)
- ServiceNow suportadas versões – Fuji, Geneva, Helsinki.

Administradores do ServiceNow tem de fazer Olá seguir na sua instância do ServiceNow:
- Geram o ID de cliente e o segredo de cliente para o produto de ServiceNow Olá. Para obter informações sobre como ver toogenerate ID de cliente e o segredo, [configuração de OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Instale Olá aplicações de utilizador para a integração da Microsoft OMS (ServiceNow aplicação). [Saiba mais](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- Crie função de utilizador de integração para a aplicação de utilizador de Olá instalada. Informações sobre como é a função de utilizador de integração de Olá toocreate [aqui](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Procedimento de ligação**

Utilize Olá procedimento toocreate uma ligação de ServiceNow os seguintes:

1. Aceda demasiado**OMS** > **definições** > **origens ligadas**.
2. Selecione **ITSM conector,** clique **Adicionar nova ligação**.

    ![Ligação de ServiceNow](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Fornecer informações de Olá, conforme descrito em Olá a tabela seguinte e clique em **guardar** ligação de Olá toocreate:

> [!NOTE]
> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Escreva um nome para a instância do ServiceNow Olá que pretende que o tooconnect com Olá conector de gestão de serviços de TI.  Utilize este nome mais tarde no OMS quando configurar os itens de trabalho neste ITSM / ver a análise de registos detalhados. |
| **Selecione o tipo de ligação**   | Selecione **ServiceNow**. |
| **Nome de Utilizador**   | Escreva o nome de utilizador de integração Olá que criou no Olá ServiceNow aplicação toosupport Olá ligação toohello conector de gestão de serviços de TI. Obter mais informações: [ServiceNow criar função de utilizador de aplicação](#create-integration-user-role-in-servicenow-app).|
| **Palavra-passe**   | Escreva a palavra-passe de Olá associada este nome de utilizador. **Tenha em atenção**: nome de utilizador e palavra-passe são utilizados para gerar tokens de autenticação apenas e não são armazenadas em qualquer lugar no serviço do Olá OMS.  |
| **URL do servidor**   | Escreva o URL de Olá de instância do ServiceNow Olá que pretende que o tooconnect tooIT conector do serviço de gestão. |
| **ID de cliente**   | Escreva o ID de cliente de Olá que pretende toouse para autenticação de OAuth2, o que é gerado anteriormente.  Obter mais informações sobre a geração de ID de cliente e o segredo: [configuração de OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **Segredo do cliente**   | Segredo do cliente do tipo Olá, gerado para este ID.   |
| **Âmbito de sincronização de dados**   | Selecione itens de trabalho de ServiceNow Olá que pretende que o tooOMS toosync, através de Olá conector de gestão de serviços de TI.  valores de Olá selecionado são importados para análise de registos.   **Opções:** incidentes e pedidos de alteração.|
| **Dados de sincronização** | Escreva o número de Olá dos últimos dias que pretende que os dados de Olá do. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender que os itens de configuração de Olá toocreate no produto ITSM Olá. Quando selecionada, o OMS cria Olá afetado CIs como itens de configuração (em caso de não existente CIs) no Olá suportados sistema ITSM. **Predefinição**: desativado. |


Quando ligado com êxito e sincronizada com êxito:

- Selecionar itens da ligação do ServiceNow são importados para análise de registos do OMS de trabalho.  Pode ver o resumo de Olá destes itens de trabalho no mosaico de conector de gestão de serviços de TI Olá.
- Pode criar incidentes, alertas e eventos de pesquisa de alertas do OMS ou de registo nesta instância do ServiceNow.  


Obter mais informações: [itens de trabalho de criar ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [itens de trabalho de criar ITSM do OMS registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-integration-user-role-in-servicenow-app"></a>Criar função de utilizador de integração na aplicação do ServiceNow

Olá de utilizador seguinte procedimento:

1.  Visite Olá [ServiceNow arquivo](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) e instalar Olá **aplicação de utilizador para ServiceNow e a integração do Microsoft OMS** na sua instância do ServiceNow.
2.  Após a instalação, visite Olá deixado barra de navegação da instância do ServiceNow Olá, procurar e selecione integrador de Microsoft OMS.  
3.  Clique em **lista de verificação de instalação**.

    Estado de Olá é apresentado como **não concluir** se é a função de utilizador Olá ainda toobe criado.

4.  No texto Olá caixas, em seguida demasiado**criar o utilizador de integração**, introduza Olá o nome de utilizador para o utilizador Olá que possam ligar toohello conector de gestão de serviços de TI no OMS.
5.  Introduza a palavra-passe de Olá para este utilizador e clique em **OK**.  

>[!NOTE]

> Utilize o ligação do ServiceNow toomake Olá estas credenciais no OMS.

Olá utilizador recentemente criado será apresentada com as funções predefinidas do Olá atribuídas.

Funções predefinidas:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.User
-   ITIL
-   template_editor
-   view_changer

Depois do utilizador Olá foi criado com êxito, Olá estado **Verifique a lista de verificação de instalação** move tooCompleted, listagem detalhes Olá Olá da função de utilizador criados para a aplicação Olá.

> [!NOTE]

> tooallow toocreate um utilizador **alertas** e **eventos** no ServiceNow da OMS:

> - Certifique-se de que ter o módulo de gestão de eventos de Olá instalada na sua instância do ServiceNow.

> - Adicione Olá utilizador de integração de toohello funções os seguintes:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Ligar Provance tooIT conector de gestão de serviço no OMS

Olá secções seguintes fornecem detalhes sobre como tooconnect toohello de produto do Provance conector de gestão de serviços de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que tem Olá pré-requisitos cumpridos os seguintes:

- Conector de gestão do serviço IT instalado. Obter mais informações: [configuração](log-analytics-itsmc-overview.md#configuration).
- Aplicação de provance deve ser registada com o Azure AD - e ID de cliente é disponibilizado. Para obter informações detalhadas, consulte [como autenticação do Active Directory de tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- A função de utilizador: administrador.

### <a name="connection-procedure"></a>Procedimento de ligação

Utilize Olá procedimento toocreate uma ligação de Provance os seguintes:

1. Aceda demasiado**OMS** > **definições** > **origens ligadas**.
2. Selecione **ITSM conector,** clique **Adicionar nova ligação**.  

    ![Ligação provance](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Fornecer informações de Olá, conforme descrito em Olá a tabela seguinte e clique em **guardar** ligação de Olá toocreate.

> [!NOTE]
> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Escreva um nome para a instância de Provance Olá que pretende que o tooconnect com Olá conector de gestão de serviços de TI.  Utilize este nome mais tarde no OMS quando configurar os itens de trabalho neste ITSM / ver a análise de registos detalhados. |
| **Selecione o tipo de ligação**   | Selecione **Provance**. |
| **Nome de Utilizador**   | Escreva o nome de utilizador de Olá que possam ligar toohello conector de gestão de serviços de TI.    |
| **Palavra-passe**   | Escreva a palavra-passe de Olá associada este nome de utilizador. **Nota:** nome de utilizador e palavra-passe são utilizados para gerar tokens de autenticação apenas e não são armazenadas em qualquer lugar no serviço do Olá OMS. _|
| **URL do servidor**   | Escreva o URL de Olá da sua instância Provance que pretende que o tooconnect tooIT conector do serviço de gestão. |
| **ID de cliente**   | Escreva o ID de cliente de Olá para autenticar esta ligação, que gerou na sua instância Provance.  Obter mais informações sobre o ID de cliente, consulte [como autenticação do Active Directory de tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Âmbito de sincronização de dados**   | Selecione itens de trabalho Olá Provance que pretende que o tooOMS toosync, através de Olá conector de gestão de serviços de TI.  Estes itens são importados para análise de registos de trabalho.   **Opções:** incidentes, pedidos de alteração.|
| **Dados de sincronização** | Escreva o número de Olá dos últimos dias que pretende que os dados de Olá do. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender que os itens de configuração de Olá toocreate no produto ITSM Olá. Quando selecionada, o OMS cria Olá afetado CIs como itens de configuração (em caso de não existente CIs) no Olá suportados sistema ITSM. **Predefinição**: desativado.|

Quando ligado com êxito e sincronizada com êxito:

- Itens de trabalho selecionados da ligação de Provance são importados para o OMS **análise de registos.**  Pode ver o resumo de Olá destes itens de trabalho no mosaico de conector de gestão de serviços de TI Olá.
- Pode criar incidentes e eventos de alertas do OMS ou de pesquisa de registo nesta instância Provance.

Obter mais informações: [itens de trabalho de criar ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [itens de trabalho de criar ITSM do OMS registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Ligar Cherwell tooIT conector de gestão de serviço no OMS

Olá secções seguintes fornecem detalhes sobre como tooconnect toohello de produto do Cherwell conector de gestão de serviços de TI no OMS.

### <a name="prerequisites"></a>Pré-requisitos

Certifique-se de que tem Olá pré-requisitos cumpridos os seguintes:

- Conector de gestão do serviço IT instalado. Obter mais informações: [configuração](log-analytics-itsmc-overview.md#configuration).
- ID de cliente gerado. Obter mais informações: [geram o ID de cliente para Cherwell](#generate-client-id-for-cherwell).
- A função de utilizador: administrador.

### <a name="connection-procedure"></a>Procedimento de ligação

Utilize Olá procedimento toocreate uma ligação de Cherwell os seguintes:

1. Aceda demasiado**OMS** >  **definições** > **origens ligadas**.
2. Selecione **ITSM conector** clique **Adicionar nova ligação**.  

    ![Id de utilizador Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Fornecer informações de Olá, conforme descrito em Olá a tabela seguinte e clique em **guardar** ligação de Olá toocreate.

> [!NOTE]
> Todos os parâmetros são obrigatórios.

| **Campo** | **Descrição** |
| --- | --- |
| **Nome**   | Escreva um nome para a instância de Cherwell Olá que pretende que o tooconnect toohello conector de gestão de serviços de TI.  Utilize este nome mais tarde no OMS quando configurar os itens de trabalho neste ITSM / ver a análise de registos detalhados. |
| **Selecione o tipo de ligação**   | Selecione **Cherwell.** |
| **Nome de Utilizador**   | Escreva o nome de utilizador de Cherwell Olá que possam ligar toohello conector de gestão de serviços de TI. |
| **Palavra-passe**   | Escreva a palavra-passe de Olá associada este nome de utilizador. **Nota:** nome de utilizador e palavra-passe são utilizados para gerar tokens de autenticação apenas e não são armazenadas em qualquer lugar no serviço do Olá OMS.|
| **URL do servidor**   | Escreva o URL de Olá da sua instância Cherwell que pretende que o tooconnect tooIT conector do serviço de gestão. |
| **ID de cliente**   | Escreva o ID de cliente de Olá para autenticar esta ligação, que gerou na sua instância Cherwell.   |
| **Âmbito de sincronização de dados**   | Selecione itens de trabalho Olá Cherwell que pretende que o toosync através de Olá conector de gestão de serviços de TI.  Estes itens são importados para análise de registos de trabalho.   **Opções:** incidentes, pedidos de alteração. |
| **Dados de sincronização** | Escreva o número de Olá dos últimos dias que pretende que os dados de Olá do. **Limite máximo**: 120 dias. |
| **Criar um novo item de configuração na solução ITSM** | Selecione esta opção se pretender que os itens de configuração de Olá toocreate no produto ITSM Olá. Quando selecionada, o OMS cria Olá afetado CIs como itens de configuração (em caso de não existente CIs) no Olá suportados sistema ITSM. **Predefinição**: desativado. |

Quando ligado com êxito e sincronizada com êxito:

- Selecionar itens a partir desta ligação Cherwell são importados para análise de registos do OMS de trabalho. Pode ver o resumo de Olá destes itens de trabalho no mosaico de conector de gestão de serviços de TI Olá.
- Pode criar incidentes e eventos nesta instância Cherwell da OMS. Obter mais informações: criar itens de trabalho ITSM para alertas do OMS e criar ITSM de trabalho itens de registos do OMS.

Obter mais informações: [itens de trabalho de criar ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) e [itens de trabalho de criar ITSM do OMS registos](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="generate-client-id-for-cherwell"></a>Geram o ID de cliente para Cherwell

toogenerate hello/chave de ID de cliente para Cherwell, utilize Olá seguinte procedimento:

1. Inicie sessão no tooyour Cherwell instância como administrador.
2. Clique em **segurança** > **as definições de cliente de API de REST editar**.
3. Selecione **criar novo cliente** > **segredo do cliente**.

    ![Id de utilizador Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Passos seguintes
 - [Criar itens de trabalho ITSM para alertas do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [Criar itens de trabalho ITSM a partir de registos do OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [Análise de registos de vista da ligação](log-analytics-itsmc-overview.md#using-the-solution)
