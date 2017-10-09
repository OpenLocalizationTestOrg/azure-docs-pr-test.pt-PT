---
title: aaaUse um servidor de SQL no local no Azure Machine Learning | Microsoft Docs
description: "Utilize dados a partir de uma análise de tooperform avançada no local do SQL Server da base de dados com o Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>Fazer análises avançadas com o Azure Machine Learning ao utilizar dados de uma base de dados do SQL Server no local

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Muitas vezes, as empresas que funcionam com dados no local pretende tootake vantagem da escala de Olá e da agilidade dessas soluções de nuvem de Olá para as respetivas cargas de trabalho de aprendizagem. Mas que não pretendem toodisrupt os seus processos de negócio atual e os fluxos de trabalho, movendo os respetivos no local dados toohello na nuvem. O Azure Machine Learning suporta agora ao ler os dados a partir de uma base de dados do SQL Server no local e, em seguida, formação e classificação de um modelo com estes dados. Já não tiver dados de Olá de copiar e sincronização toomanually entre a nuvem de Olá e o servidor no local. Em vez disso, Olá **importar dados** módulo no Azure Machine Learning Studio agora pode ler diretamente a partir da sua base de dados do SQL Server no local para fins de formação e classificação de tarefas.

Este artigo fornece uma descrição geral de como tooingress no local dados do SQL Server no Azure Machine Learning. Pressupõe que está familiarizado com conceitos de Azure Machine Learning áreas de trabalho, módulos, conjuntos de dados, as experimentações *etc.*.

> [!NOTE]
> Esta funcionalidade não está disponível para áreas de trabalho gratuitas. Para obter mais informações sobre preços do Machine Learning e camadas, consulte [preços do Azure Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Instalar Olá Microsoft Data Management Gateway
tooaccess uma base de dados do SQL Server no local no Azure Machine Learning, terá de toodownload e instalar Olá Microsoft Data Management Gateway. Quando configurar a ligação de gateway Olá no Machine Learning Studio, terá oportunidade de Olá para transferir e instalar gateway Olá utilizando Olá **transferência e gateway de dados de registo** diálogo descritas abaixo.

Também pode instalar Olá Data Management Gateway antecedência ao descarregar e executar o pacote de configuração do MSI Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).
Escolha a versão mais recente Olá, a seleção de 32 bits ou 64 bits conforme apropriado para o seu computador. Olá MSI, também pode ser utilizado tooupgrade uma Data Management Gateway toohello mais recente versão existente, com todas as definições preservados.

gateway de Olá tem Olá os seguintes pré-requisitos:

* versões de sistema operativo do Windows Hello suportado são o Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* Olá recomendada a configuração da máquina do gateway de Olá é, pelo menos, 2 GHz, 4 núcleos, 8GB de RAM e o disco de 80GB.
* Se o computador do anfitrião de Olá hibernates, gateway Olá não responde a pedidos toodata. Por conseguinte, configure uma esquema de energia adequado Olá computador antes de instalar o gateway de Olá. Se a máquina de Olá toohibernate configurada, a instalação do gateway Olá apresenta uma mensagem.
* Porque a atividade de cópia ocorre uma frequência específico, Olá utilização de recursos (CPU, memória) na máquina de Olá segue também Olá mesmo padrão das horas de ponta e tempos de inatividade. Utilização de recursos também depende descontos elevados Olá quantidade de dados a ser movidos. Quando várias tarefas de cópia estão em curso, irá reparar a utilização de recursos, aceda a cópia de segurança durante as horas de pico. Embora seja tecnicamente suficientes Olá mínimos de configuração indicados acima, poderá pretender que toohave uma configuração com mais recursos à configuração mínima de Olá consoante a carga específica para o movimento de dados.

Considere Olá seguinte quando configurar e utilizar um Data Management Gateway:

* Pode instalar apenas uma instância do Data Management Gateway num único computador.
* Pode utilizar um único gateway para várias origens de dados no local.
* Pode ligar vários gateways em computadores diferentes toohello mesma origem de dados no local.
* Configurar um gateway para a área de trabalho apenas um de cada vez. Atualmente, os gateways não podem ser partilhados em áreas de trabalho.
* Pode configurar vários gateways para uma única área de trabalho. Por exemplo, poderá pretender toouse um gateway que está ligado tooyour origens de dados de teste durante o desenvolvimento e um gateway de produção quando estiver pronto toooperationalize.
* gateway de Olá não precisa de toobe no mesmo computador como origem de dados de Olá de Olá. Mas, permanecendo toohello próximo origem de dados reduz o tempo de Olá Olá gateway tooconnect toohello origem de dados. Recomendamos que instale o gateway de Olá num computador que é diferente do Olá uma origem de dados que anfitriões Olá no local para que hello origem de dados e de gateway não competem para ter recursos.
* Se já tiver um gateway instalado no seu computador, que serve o Power BI ou do Azure Data Factory cenários, instale um gateway separado para o Azure Machine Learning noutro computador.

  > [!NOTE]
  > Não é possível executar o Data Management Gateway e o Gateway do Power BI no Olá mesmo computador.
  >
  >
* Tem de toouse Olá Data Management Gateway para o Azure Machine Learning, mesmo se estiver a utilizar o Azure ExpressRoute para outros dados. Deve tratar a origem de dados como uma origem de dados no local (que é protegido por uma firewall), mesmo quando a utiliza o ExpressRoute. Utilize a conectividade de tooestablish Olá Data Management Gateway entre Machine Learning e origem de dados de Olá.

Pode encontrar informações detalhadas sobre os pré-requisitos da instalação, os passos de instalação e sugestões de resolução de problemas no artigo Olá [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md).

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>Dados de entrada da sua base de dados do SQL Server no local para o Azure Machine Learning
Esta explicação passo a passo, irá configurar um Data Management Gateway numa área de trabalho do Azure Machine Learning, configurá-lo e, em seguida, ler dados a partir de uma base de dados do SQL Server no local.

> [!TIP]
> Antes de começar, desativar o Bloqueador de janelas de pop-up do browser para `studio.azureml.net`. Se estiver a utilizar Olá browser Google Chrome, transfira e instale uma das Olá vários plug-ins disponíveis no Google Chrome WebStore [clique uma vez extensão de aplicação](https://chrome.google.com/webstore/search/clickonce?_category=extensions).
>
>

### <a name="step-1-create-a-gateway"></a>Passo 1: Criar um gateway
primeiro passo de Olá é toocreate e configurar Olá gateway tooaccess a base de dados do SQL Server no local.

1. Inicie sessão no demasiado[Azure Machine Learning Studio](https://studio.azureml.net/Home/) e selecione Olá área de trabalho que pretende toowork no.
2. Clique em Olá **definições** painel Olá à esquerda e, em seguida, clique em Olá **GATEWAYS dados** separador na parte superior do Olá.
3. Clique em **novo GATEWAY de dados** em Olá parte inferior do ecrã de Olá.

    ![Novo Gateway de dados](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. No Olá **novo gateway de dados** caixa de diálogo, introduza Olá **nome do Gateway** e, opcionalmente, adicione um **Descrição**. Clique em seta de Olá na Olá inferior canto direito toogo toohello próximo passo da configuração de Olá.

    ![Introduzir descrição e nome de gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. Olá transferir e registar o diálogo de gateway de dados, área de transferência do cópia Olá chave de registo de GATEWAY toohello.

    ![Transferir e registar o gateway de dados](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>Se ainda não tiver transferido e instalado Olá Microsoft Data Management Gateway, em seguida, clique em **transferências o data management gateway**. Este guia toothe Microsoft Download Center onde pode selecionar a versão do gateway Olá, tem de, transferir e instalá-lo. Pode encontrar informações detalhadas sobre os pré-requisitos da instalação, os passos de instalação e sugestões de resolução de problemas nas secções de início de Olá artigo Olá [mover dados entre origens no local e nuvem com o Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Após a instalação do gateway de Olá, Olá Gestor de configuração do Data Management Gateway irá abrir e Olá **registar gateway** é apresentada a caixa de diálogo. Olá colar **chave de registo de Gateway** que copiou toohello área de transferência e clique em **registar**.
8. Se já tiver um gateway instalado, execute Olá Gestor de configuração do Data Management Gateway. Clique em **alterar chave**, cole o **chave de registo de Gateway** que copiou toohello área de transferência no passo anterior Olá e clique em **OK**.
9. Quando Olá instalação estiver concluída, Olá **registar gateway** é apresentada a caixa de diálogo para o Microsoft Data Management Gateway Configuration Manager. Cole Olá chave de registo de GATEWAY que copiou para a área de transferência Olá num passo anterior e clique em **registar**.

    ![Registar o gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. Olá configuração do gateway está concluída quando Olá os seguintes valores está definida no Olá **home page** separador no Microsoft Data Management Gateway do Configuration Manager:

    * **O nome do gateway** e **nome da instância** estão definidas toohello nome do gateway de Olá.
    * **Registo** estiver definido demasiado**registada**.
    * **Estado** estiver definido demasiado**iniciado**.
    * barra de estado de Olá na Olá inferior apresenta **ligado tooData o serviço de nuvem do Gateway de gestão** juntamente com uma marca de verificação verde.

      ![Gestor de Gateway de gestão de dados](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      Azure Machine Learning Studio também obtém atualizado quando o registo de Olá é efetuada com êxito.

    ![Registo de gateway com êxito](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. No Olá **transferir e registar o gateway de dados** caixa de diálogo, clique em configuração de Olá de toocomplete marca de verificação. Olá **definições** página apresenta o estado do gateway como "Online". No painel direito de Olá, encontrará estado e outras informações úteis.

    ![Definições do gateway](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. No Gestor de configuração do Microsoft Data Management Gateway de Olá comutador toohello **certificado** certificado de Olá do separador. especificado neste separador é utilizado tooencrypt/desencriptação credenciais para o arquivo de dados no local do Olá que especificar no portal de Olá. Este certificado é Olá predefinido certificado. A Microsoft recomenda alterar este certificado próprio tooyour que efetue cópias de segurança no seu sistema de gestão de certificados. Clique em **alteração** toouse seu próprio certificado em vez disso.

    ![Certificado de gateway de alteração](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (opcional) Se quiser tooenable o registo verboso para resolver problemas com o gateway de Olá, no Gestor de configuração do Microsoft Data Management Gateway de Olá comutador toothe **diagnóstico** separador e verifique Olá **ativar o registo para fins de resolução de problemas verboso** opção. Olá informações de registo podem ser encontradas na Olá Visualizador de eventos do Windows em Olá **registos de serviços e aplicações**  - &gt; **Data Management Gateway** nós. Também pode utilizar Olá **diagnóstico** separador tootest Olá ligação tooan no local origem de dados utilizando Olá gateway.

    ![Ativar o registo verboso](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Este passo conclui o processo de configuração do gateway Olá no Azure Machine Learning.
Está agora pronto toouse os dados no local.

Pode criar e configurar vários gateways no Studio para cada área de trabalho. Por exemplo, pode ter um gateway que pretende que origens de dados de teste de tooyour tooconnect durante o desenvolvimento e um gateway diferentes para as origens de dados de produção. O Azure Machine Learning dá-lhe o tooset flexibilidade dos vários gateways consoante o seu ambiente empresarial. Atualmente, não é possível partilhar um gateway entre as áreas de trabalho e apenas um gateway pode ser instalado num único computador. Para obter mais informações, consulte [mover dados entre origens no local e nuvem com o Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>Passo 2: Utilizar Olá gateway tooread dados de uma origem de dados no local
Depois de configurar o gateway de Olá, pode adicionar um **importar dados** módulo para uma experimentação que entradas Olá da base de dados Olá no local do SQL Server.

1. No Machine Learning Studio, selecione Olá **EXPERIMENTAÇÕES** separador, clique em **+ novo** no Olá canto inferior esquerdo e selecione **experimentação em branco** (ou selecione uma das várias de exemplo experimentações disponíveis).
2. Localize e arraste Olá **importar dados** módulo toohello tela de experimentação.
3. Clique em **guardar como** abaixo tela Olá. Introduza "Azure local no SQL Server Tutorial do Machine Learning" para o nome da experimentação Olá, selecione a área de trabalho e clique em Olá **OK** marca de verificação.

   ![Guardar experimentação com um novo nome](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Clique em Olá **importar dados** tooselect de módulo, em seguida, no **propriedades** toohello painel à direita da tela Olá, selecione "Base de dados do SQL Server no local" Olá **origem de dados** na lista pendente.
5. Selecione Olá **gateway de dados** instalado e registado. Pode configurar o outro gateway ao selecionar "(adicionar novo Gateway de dados...)".

   ![Selecione o gateway de dados para o módulo de importar dados](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Introduza Olá SQL **nome do servidor de base de dados** e **nome de base de dados**, juntamente com Olá SQL **consulta de base de dados** pretende tooexecute.
7. Clique em **introduza valores** em **nome de utilizador e palavra-passe** e introduza as credenciais da sua base de dados. Pode utilizar a autenticação integrada do Windows ou a autenticação de servidor de SQL consoante o modo como o SQL Server no local está configurado.

   ![Introduza as credenciais da base de dados](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   mensagem de saudação alterações "valores necessários" demasiado "valores conjunto" com uma marca de verificação verde. Só precisa de credenciais de Olá tooenter uma vez, a menos que as informações de base de dados de Olá ou palavra-passe é alterada. O Azure Machine Learning utiliza o certificado de Olá que forneceu quando instalou as credenciais do Olá gateway tooencrypt Olá na nuvem de Olá. Azure nunca armazena as credenciais no local sem encriptação.

   ![Importar as propriedades do módulo de dados](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. Clique em **executar** experimentação de Olá toorun.

Depois Olá da experimentação ser concluída em execução, pode visualizar dados Olá importados da base de dados de Olá clicando Olá porta de saída de Olá **importar dados** módulo e selecionando **visualizar**.

Depois de concluir a desenvolver a sua experimentação, pode implementar e operacionalizar o seu modelo. Olá, utilizando o serviço de execução do Batch, dados de Olá no local do SQL Server da base de dados configurada no Olá **importar dados** módulo será ler e utilizado para classificação. Apesar de poder utilizar Olá pedido de serviço de resposta para a classificação de dados no local, a Microsoft recomenda a utilização de [suplemento do Excel](machine-learning-excel-add-in-for-web-services.md) em vez disso. Atualmente, escrever tooan no local da base de dados do SQL Server através de **exportar dados** não é suportado nas suas experimentações ou publicado web serviços.
