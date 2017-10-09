---
title: aaaAccess origens de dados no local para Azure Logic Apps | Microsoft Docs
description: "Configurar o gateway de dados no local Olá para que possa aceder a origens de dados no local a partir das logic apps"
keywords: "aceder a dados no local, a transferência de dados, a encriptação e origens de dados"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Origens de dados de acesso no local a partir das logic apps com o gateway de dados do Olá no local

tooaccess origens de dados no local das logic apps, configurar um gateway de dados no local que podem utilizar aplicações lógicas com conectores suportados. gateway de Olá atua como uma ponte que fornece a transferência de dados rápida e encriptação entre origens de dados no local e as logic apps. gateway de Olá transmite dados a partir de origens do local em canais encriptados através de Olá Service Bus do Azure. Todo o tráfego origina como tráfego de saída seguro de agente de gateway Olá. Saiba mais sobre [como funciona o gateway de dados de Olá](logic-apps-gateway-install.md#gateway-cloud-service). 

gateway de Olá suporta origens de dados de toothese ligações no local:

*   BizTalk Server 2016
*   DB2  
*   Sistema de Ficheiros
*   Informix
*   MQ
*   MySQL
*   Base de dados Oracle
*   PostgreSQL
*   Servidor de aplicações SAP 
*   Servidor de mensagens SAP
*   SharePoint
*   SQL Server
*   Teradata

Estes passos mostram como tooset segurança Olá no local toowork de gateway de dados com as logic apps. Para obter mais informações sobre conectores suportados, consulte [conectores para o Azure Logic Apps](../connectors/apis-list.md). 

Para obter informações sobre como toouse Olá gateway com outros serviços, consulte estes artigos:

*   [Gateway de dados do Microsoft Power BI no local](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Gateway de dados no local do Analysis Services do Azure](../analysis-services/analysis-services-gateway.md)
*   [Gateway de dados do Microsoft Flow no local](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Gateway de dados do Microsoft PowerApps no local](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Requisitos

* Tem de ter já [instalado o gateway de dados de Olá num computador local](logic-apps-gateway-install.md).

* Quando inicia sessão no portal do Azure de toohello, tiver toouse Olá a mesma conta escolar ou profissional que foi utilizada demasiado[instalar o gateway de dados no local de Olá](logic-apps-gateway-install.md#requirements). A conta de início de sessão também tem de ter uma subscrição do Azure toouse quando cria um recurso de gateway no Olá portal do Azure para a sua instalação do gateway.

* A instalação do gateway já não pode ser reclamada por um recurso de gateway do Azure. Pode associar o seu gateway instalação tooonly um gateway do Azure recurso. Afirmação acontece quando criar o recurso do gateway de Olá, para que a instalação de Olá não está disponível para outros recursos.

## <a name="set-up-hello-data-gateway-connection"></a>Configurar a ligação de gateway de dados de Olá

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Instalar o gateway de dados do Olá no local

Se ainda não o fez, siga Olá [gateway de dados no local do passos tooinstall Olá](logic-apps-gateway-install.md). Antes de continuar com Olá outros passos, certifique-se de que instalou o gateway de dados de Olá num computador local.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Criar um recurso do Azure para o gateway de dados do Olá no local

Depois de instalar o gateway de Olá num computador local, tem de criar o gateway de dados como um recurso no Azure. Este passo também associa o seu recurso de gateway com a sua subscrição do Azure.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure"). Certifique-se toouse Olá mesmo trabalho do Azure ou o endereço de e-mail profissional utilizado o gateway de Olá tooinstall.

2. No menu à esquerda de Olá no Azure, escolha **novo** > **integração empresarial com** > **gateway de dados no local** conforme mostrado aqui:

   ![Localizar "gateway de dados no local"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. No Olá **criar gateway de ligação** painel, forneça estes detalhes toocreate o recurso do gateway de dados:

    * **Nome**: introduza um nome para o recurso do gateway. 

    * **Subscrição**: selecione Olá tooassociate de subscrição do Azure com o recurso do gateway. 
    Esta subscrição deve ser Olá mesma subscrição que a sua aplicação lógica.
   
      subscrição de predefinição Olá baseia Olá conta do Azure que utilizou toosign no.

    * **Grupo de recursos**: criar um grupo de recursos ou selecione um grupo de recursos existente para implementar o recurso do gateway. 
    Grupos de recursos ajudam a gerir recursos do Azure relacionados como uma coleção.

    * **Localização**: Azure restringe esta localização toohello mesma região que foi selecionado para o serviço de nuvem do gateway Olá durante [instalação do gateway](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Certifique-se de que a localização do recurso de gateway de Olá corresponde à localização do serviço de nuvem do Olá gateway. Caso contrário, a instalação do gateway pode não aparecer na lista de gateways Olá instalado para lhe tooselect passo seguinte Olá.
      > 
      > Pode utilizar regiões diferentes para o seu recurso de gateway e para a sua aplicação lógica.

    * **Nome de instalação**: se a instalação do gateway não estiver selecionada, selecione o gateway de Olá que instalou anteriormente. 

    Escolha tooadd Olá gateway recursos tooyour dashboard do Azure, **Pin toodashboard**. 
    Quando tiver terminado, escolha **criar**.

    Por exemplo:

    ![Forneça detalhes toocreate o gateway de dados no local](./media/logic-apps-gateway-connection/createblade.png)

    toofind ou ver o seu gateway de dados em qualquer altura, menu Olá principal do Azure à esquerda, aceda demasiado **mais serviços** > **integração empresarial com** > **dados no local Gateways**.

    ![Aceda demasiado "Mais serviços", "Integração empresarial com o", "Gateways de dados no local"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Ligar o gateway de dados no local de toohello de aplicação de lógica

Agora que já criou o seu recurso de gateway de dados e associado à sua subscrição do Azure com esse recurso, crie uma ligação entre o gateway de dados de aplicação e Olá lógica.

> [!NOTE]
> A localização de ligação do gateway tem de existir na Olá mesma região que a sua aplicação lógica, mas pode utilizar um gateway de dados existe numa região diferente.

1. No portal do Azure Olá, criar ou abrir a sua aplicação lógica no Designer de aplicação lógica.

2. Adicione um conector que suporte ligações no local, como o SQL Server.

3. A seguir a ordem de Olá apresentada, selecione **ligar através do gateway de dados no local**, forneça um nome de ligação exclusiva Olá informações necessárias e selecione o recurso de gateway de dados de Olá que pretende que o toouse. Quando tiver terminado, escolha **criar**.

   > [!TIP]
   > Um nome de ligação exclusiva ajuda-o a identificar facilmente essa ligação mais tarde, especialmente quando cria várias ligações. Se aplicável, também inclua o domínio de qualificado Olá para o seu nome de utilizador. 

   ![Criar ligação entre o gateway de dados e aplicação lógica](./media/logic-apps-gateway-connection/blankconnection.png)

Parabéns, a ligação de gateway está agora preparada para sua toouse de aplicação lógica.

## <a name="edit-your-gateway-connection-settings"></a>Editar as definições de ligação de gateway

Depois de criar uma ligação de gateway para a sua aplicação lógica, pode querer toolater Olá Update para essa ligação específica.

1. ligação de gateway do toofind Olá:

   * No painel de aplicação de lógica de Olá, sob **ferramentas de desenvolvimento**, selecione **API ligações**. 
   
     Olá **API ligações** painel mostra todas as ligações de API associadas com a sua aplicação lógica, incluindo ligações de gateway.

     ![Aceda a aplicação de lógica de tooyour, selecione "API ligações"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Ou, no menu Olá principal do Azure à esquerda, vá demasiado **mais serviços** > **Web & Mobile Services** > **API ligações** para todas as ligações de API incluindo ligações do gateway, que estão associadas a sua subscrição do Azure. 

   * Ou, no Olá principal do Azure menu à esquerda, aceda demasiado**todos os recursos** para todas as ligações de API, incluindo ligações de gateway, que estão associadas a sua subscrição do Azure.

2. Selecione a ligação de gateway Olá que pretender tooview ou a editar e escolha **ligação editar API**.

   > [!TIP]
   > Se as atualizações não entre em vigor, tente [parando e reiniciando o serviço de gateway do Windows hello](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Comutador ou eliminar o recurso de gateway de dados no local

toocreate um recurso de gateway diferentes, o gateway de associar a um recurso diferente ou remova o recurso do gateway Olá, pode eliminar o recurso do gateway Olá sem afetar a instalação do gateway Olá. 

1. Menu Olá principal do Azure à esquerda, aceda demasiado**todos os recursos**. 
2. Localize e selecione o recurso de gateway de dados.
3. Escolha **Gateway de dados no local**e na barra de ferramentas de recurso Olá, escolha **eliminar**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Perguntas mais frequentes

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Passos seguintes

* [Proteger as suas aplicações lógicas](./logic-apps-securing-a-logic-app.md)
* [Exemplos e cenários para aplicações lógicas comuns](./logic-apps-examples-and-scenarios.md)
