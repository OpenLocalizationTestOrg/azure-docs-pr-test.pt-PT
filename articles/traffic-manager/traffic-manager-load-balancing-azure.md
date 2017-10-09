---
title: "balanceamento de carga aaaUsing serviços no Azure | Microsoft Docs"
description: "Este tutorial mostra como toocreate um cenário utilizando Olá portefólio de balanceamento de carga do Azure: Gestor de tráfego, o Gateway de aplicação e o Balanceador de carga."
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Utilizando os serviços de balanceamento de carga no Azure

## <a name="introduction"></a>Introdução

O Microsoft Azure oferece vários serviços para gerir a forma como o tráfego de rede é distribuído e balanceamento de carga. Pode utilizar estes serviços individualmente ou combinar os respetivos métodos, consoante as suas necessidades, a solução ideal de Olá toobuild.

Neste tutorial, vamos primeiro definir um caso de utilização do cliente e ver como este pode ser efetuada mais robusto e performant utilizando Olá seguir portefólio de balanceamento de carga do Azure: Gestor de tráfego, o Gateway de aplicação e o Balanceador de carga. Em seguida, podemos fornecer instruções passo a passo para criar uma implementação que georredundante, distribui o tráfego tooVMs e ajuda-o a gerir diferentes tipos de pedidos.

Um nível conceptual, cada um destes serviços desempenha um papel distinto na hierarquia de balanceamento de carga Olá.

* **Gestor de tráfego** fornece balanceamento de carga de global DNS. -Analisa os pedidos recebidos de DNS e responde com um ponto final em bom estado, de acordo com Olá encaminhamento cliente de Olá de política foi selecionada. Opções para métodos de encaminhamento são:
  * Desempenho encaminhamento toosend Olá requerente toohello mais próximo ponto final em termos de latência.
  * Prioridade encaminhamento toodirect todos os tráfego tooan ponto final, com outros pontos finais como cópia de segurança.
  * Ponderado round robin encaminhamento, que distribui o tráfego com base no peso Olá atribuído tooeach endpoint.

  Olá cliente liga-se diretamente toothat endpoint. Traffic Manager do Azure Deteta quando um ponto final está danificado e, em seguida, redireciona Olá instância de bom estado de funcionamento de tooanother de clientes. Consulte demasiado[documentação do Traffic Manager do Azure](traffic-manager-overview.md) toolearn mais sobre o serviço de Olá.
* **Gateway de aplicação** fornece o controlador de entrega de aplicações (ADC) como um oferta de serviço, vários grupos de capacidades de balanceamento de carga de 7 camadas para a sua aplicação. Permite que os clientes produtividade do toooptimize web farm ao descarregar o gateway de aplicação de toohello de terminação de SSL intensivas em CPU. Outras funcionalidades de encaminhamento de 7 camadas incluem a distribuição de round robin de tráfego de entrada, afinidade com base no cookie de sessão, URL com base no caminho de encaminhamento e Olá capacidade toohost vários sites por trás de um gateway de aplicação único. Gateway de aplicação pode ser configurado como um gateway de acesso à Internet, um gateway meramente internos ou uma combinação de ambos. Gateway de aplicação é Azure totalmente gerido, escalável e altamente disponível. Proporciona um conjunto avançado de capacidades de registo e diagnóstico, para uma melhor capacidade de gestão.
* **O Balanceador de carga** é uma parte integral da pilha de Azure SDN Olá, que fornece elevado desempenho, baixa latência camada 4 balanceamento de carga serviços protocolos de todos os UDP e TCP. Gere ligações de entrada e saídas. Pode configurar públicos e internos com balanceamento de carga pontos finais e definem regras toomap destinos de conjunto de tooback-end de ligações de entrada através de TCP e HTTP pesquisa de estado de funcionamento opções toomanage disponibilidade do serviço.

## <a name="scenario"></a>Cenário

Neste cenário de exemplo, vamos utilizar um site simples, que serve os dois tipos de conteúdo: imagens e páginas Web composto dinamicamente. Web site de Olá tem de ser georredundante e deverá servir os utilizadores de Olá mais próxima (mais baixa latência) toothem de localização. Olá programador da aplicação decidiu que Olá qualquer URLs que corresponde ao padrão/imagens / * são servido a partir de um conjunto de VMs diferentes de rest de Olá de web farm do Olá dedicado.

Além disso, o conjunto VM Olá predefinido que serve o conteúdo dinâmico Olá é tootalk tooa back-end da base de dados que está alojado num cluster de elevada disponibilidade. implementação de todo Olá é configurada através do Azure Resource Manager.

Utilizar o Gestor de tráfego, o Gateway de aplicação e o Balanceador de carga permite que este Web site tooachieve estes objetivos de design:

* **Redundância geográfica várias**: se uma região ficar inativo, o Gestor de tráfego de rotas totalmente integrada tráfego toohello região mais próxima sem qualquer intervenção do proprietário da aplicação Olá.
* **Latência reduzida**: porque o Gestor de tráfego direciona automaticamente a região mais próxima do Olá cliente toohello, cliente Olá ocorre com a menor latência quando pedir conteúdo de página Web Olá.
* **Escalabilidade independente**: porque a carga de trabalho de aplicação de web de Olá é separada por tipo de conteúdo, o proprietário da aplicação Olá pode dimensionar Olá pedido cargas de trabalho independentes entre si. Gateway de aplicação assegura que o tráfego de Olá agrupamentos direita toohello encaminhado com base no Olá especificado regras e Olá estado de funcionamento da aplicação Olá.
* **Balanceamento de carga interna**: porque o Balanceador de carga é à frente do cluster de elevada disponibilidade Olá, só ponto final do Active Directory e bom Olá para uma base de dados é exposto toohello aplicação. Além disso, um administrador da base de dados pode otimizar a carga de trabalho Olá por distribuição réplicas ativas e passivas cluster Olá independente da aplicação Olá de front-end. Balanceador de carga fornece o cluster de elevada disponibilidade toohello ligações e assegura que apenas as bases de dados bom recebem pedidos de ligação.

Olá diagrama seguinte mostra a arquitetura de Olá deste cenário:

![Diagrama de balanceamento de carga arquitetura](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> Neste exemplo é apenas uma das muitas configurações possíveis Olá balanceamento de carga dos serviços de que o Azure oferece. Gestor de tráfego, o Gateway de aplicação e o Balanceador de carga podem ser misto e toobest correspondente conforme as suas necessidades de balanceamento de carga. Por exemplo, se a descarga de SSL ou processamento de 7 camadas não é necessário, Balanceador de carga pode ser utilizado em vez de Gateway de aplicação.

## <a name="setting-up-hello-load-balancing-stack"></a>Configurar a pilha de balanceamento de carga Olá

### <a name="step-1-create-a-traffic-manager-profile"></a>Passo 1: Criar um perfil do Traffic Manager

1. No portal do Azure Olá, clique em **novo**e, em seguida, marketplace de Olá pesquisa para "Perfil do Traffic Manager."
2. No Olá **perfil do Gestor de tráfego criar** painel, introduza as seguintes informações básicas de Olá:

  * **Nome**: forneça um DNS do perfil do Traffic Manager prefixo de nome.
  * **Método de encaminhamento**: selecione Olá política do método de encaminhamento de tráfego. Para obter mais informações sobre métodos de Olá, consulte [sobre o tráfego do traffic Manager métodos de encaminhamento](traffic-manager-routing-methods.md).
  * **Subscrição**: selecione a subscrição de Olá que contém Olá perfil.
  * **Grupo de recursos**: grupo de recursos de Olá Select que contém Olá perfil. Pode ser um grupo de recursos novo ou existente.
  * **Localização do grupo de recursos**: serviço Gestor de tráfego é a localização de tooa global e não está vinculado. No entanto, tem de especificar uma região para o grupo de olá onde residem a metadados de Olá associados ao perfil do Gestor de tráfego de Olá. Esta localização não tem impacto na disponibilidade de tempo de execução de Olá do perfil de Olá.

3. Clique em **criar** toogenerate Olá perfil do Traffic Manager.

  ![Painel "Criar Gestor de tráfego"](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>Passo 2: Criar Olá gateways de aplicação

1. No Olá portal do Azure, no painel esquerdo Olá, clique em **novo** > **redes** > **Gateway de aplicação**.
2. Introduza Olá informações básicas sobre o gateway de aplicação Olá os seguintes:

  * **Nome**: nome de Olá Olá do gateway de aplicação.
  * **Tamanho do SKU**: Olá tamanho Olá do gateway de aplicação, disponível como pequeno, médio ou grande.
  * **Contagem de instância**: o número de instâncias Olá, um valor de 2 a 10.
  * **Grupo de recursos**: grupo de recursos de Olá que detém o gateway de aplicação Olá. Pode ser um grupo de recursos existente ou um novo.
  * **Localização**: região Olá Olá gateway de aplicação, que é Olá mesma localização do grupo de recursos de Olá. a localização de Olá é importante, porque a rede virtual Olá e um IP público tem de constar Olá mesma localização do gateway de Olá.
3. Clique em **OK**.
4. Defina a rede virtual Olá, sub-rede, IP de front-end e configurações de serviço de escuta para o gateway de aplicação Olá. Neste cenário, o endereço IP Front-end Olá é **pública**, que permite toobe adicionado como um ponto final toohello perfil do Traffic Manager mais tarde.
5. Configure o serviço de escuta de Olá com uma das seguintes opções de Olá:
    * Se utilizar HTTP, não há nada tooconfigure. Clique em **OK**.
    * Se utilizar o HTTPS, ainda é necessária configuração. Consulte demasiado[criar um gateway de aplicação](../application-gateway/application-gateway-create-gateway-portal.md), começando no passo 9. Quando tiver concluído a configuração de Olá, clique em **OK**.

#### <a name="configure-url-routing-for-application-gateways"></a>Configurar o encaminhamento de URL para gateways de aplicação

Quando seleciona um conjunto de back-end, um gateway de aplicação que está configurado com uma regra com base no caminho aceita um padrão do caminho do URL de pedido de Olá distribuição tooround-round robin de adição. Neste cenário, que estamos a adicionar uma regra com base no caminho toodirect qualquer URL com "/images/\*" toohello agrupamento de servidores de imagem. Para obter mais informações sobre como configurar o URL com base no caminho de encaminhamento para um gateway de aplicação, consulte demasiado[criar uma regra com base no caminho para um gateway de aplicação](../application-gateway/application-gateway-create-url-route-portal.md).

![Diagrama de camada web de Gateway de aplicação](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. Do seu grupo de recursos, aceda a instância de toohello Olá do gateway de aplicação que criou no Olá anterior a secção.
2. Em **definições**, selecione **conjuntos back-end**e, em seguida, selecione **adicionar** tooadd Olá VMs que pretende que o tooassociate com conjuntos de back-end Olá camada web.
3. No Olá **adicionar conjunto back-end** painel, introduza o nome de Olá do conjunto de back-end Olá e todos os endereços IP de Olá das máquinas de Olá que residem no conjunto de Olá. Neste cenário, estamos a estabelecer ligação dois conjuntos de servidores de back-end de máquinas virtuais.

  ![Painel de "Adicionar conjunto back-end" de Gateway de aplicação](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. Em **definições** Olá do gateway de aplicação, selecione **regras**e, em seguida, clique em Olá **caminho com base** botão tooadd uma regra.

  ![Botão de "Caminho com base" regras do Gateway de aplicação](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. No Olá **Adicionar regra de caminho com base em** painel, configurar a regra de Olá fornecendo Olá informações a seguir.

   Definições básicas:

   + **Nome**: nome amigável do Olá Olá de regra de que está acessível no portal de Olá.
   + **Serviço de escuta**: serviço de escuta de Olá que é utilizado para a regra de Olá.
   + **Predefinição conjunto back-end**: Olá toobe de conjunto back-end utilizado com a regra predefinida de Olá.
   + **Predefinições de HTTP**: Olá HTTP definições toobe utilizado com a regra predefinida de Olá.

   Regras com base no caminho:

   + **Nome**: nome amigável do Olá da regra com base no caminho de Olá.
   + **Caminhos**: regra de caminho Olá, que é utilizada para o tráfego de reencaminhamento.
   + **Conjunto back-end**: Olá toobe de conjunto back-end utilizado com esta regra.
   + **Definição de HTTP**: Olá HTTP definições toobe utilizado com esta regra.

   > [!IMPORTANT]
   > Caminhos: Caminhos válidos tem de começar com "/". Olá caráter universal "\*" é permitido apenas no final de Olá. Exemplos válidos são /xyz, /xyz\*, ou /xyz/\*.

   ![Painel de "Adicionar regra com base no caminho" do Gateway de aplicação](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>Passo 3: Adicionar pontos finais da aplicação gateways toohello Gestor de tráfego

Neste cenário, o Gestor de tráfego é gateways tooapplication ligado (conforme configurado na Olá precedente passos) que residem em regiões diferentes. Agora que os gateways de aplicação Olá estiverem configurados, o passo seguinte Olá é tooconnect-los tooyour perfil do Traffic Manager.

1. Abra o perfil do Traffic Manager. toodo por isso, procure no seu grupo de recursos ou procure o nome de Olá do perfil do Traffic Manager Olá de **todos os recursos**.
2. No painel esquerdo Olá, selecione **pontos finais**e, em seguida, clique em **adicionar** tooadd um ponto final.

  ![Botão de Gestor de tráfego pontos finais "Adicionar"](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. No Olá **adicionar ponto final** painel, crie um ponto final introduzindo Olá seguintes informações:

  * **Tipo**: selecionar tipo de Olá de ponto final tooload balancear. Neste cenário, selecione **ponto final do Azure** porque estamos a estabelecer ligação, instâncias de gateway de aplicação toohello que foram anteriormente configuradas.
  * **Nome**: introduza o nome Olá do ponto final de Olá.
  * **Tipo de recurso de destino**: selecione **endereço IP público** e, em **recurso de destino**, selecione o IP público do Olá Olá do gateway de aplicação que foi configurada anteriormente.

   ![Painel "Adicionar ponto final" do Gestor de tráfego](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Agora pode testar a configuração a aceder ao mesmo com Olá DNS do seu perfil do Gestor de tráfego (neste exemplo: TrafficManagerScenario.trafficmanager.net). Pode reenviar pedidos, trazer ou colocar baixo VMs e servidores web que foram criados em regiões diferentes e alterar tootest de definições de perfil de Gestor de tráfego de Olá a configuração.

### <a name="step-4-create-a-load-balancer"></a>Passo 4: Criar um balanceador de carga

Neste cenário, o Balanceador de carga distribui ligações a partir de Olá web camada toohello bases de dados dentro de um cluster de elevada disponibilidade.

Se o cluster de elevada disponibilidade da base de dados está a utilizar o SQL Server AlwaysOn, consulte demasiado[configurar um ou mais sempre na disponibilidade grupo de serviços de escuta](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) para obter instruções passo a passo.

Para obter mais informações sobre como configurar um balanceador de carga interno, consulte [criar um balanceador de carga interno no portal do Azure de Olá](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. No Olá portal do Azure, no painel esquerdo Olá, clique em **novo** > **redes** > **Balanceador de carga**.
2. No Olá **criar Balanceador de carga** painel, escolha um nome para o Balanceador de carga.
3. Conjunto Olá **tipo** demasiado**interno**e escolha a rede virtual adequado de Olá e a sub-rede para Olá tooreside de Balanceador de carga no.
4. Em **atribuição de endereços IP**, selecione **dinâmica** ou **estático**.
5. Em **grupo de recursos**, escolha o grupo de recursos de Olá Olá Balanceador de carga.
6. Em **localização**, escolha Olá região adequado Olá Balanceador de carga.
7. Clique em **criar** Balanceador de carga de Olá toogenerate.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Ligar um balanceador de carga de toohello de camada de base de dados de back-end

1. O grupo de recursos, localize o Balanceador de carga de Olá que foi criada nos passos anteriores Olá.
2. Em **definições**, clique em **conjuntos back-end**e, em seguida, clique em **adicionar** tooadd um conjunto de back-end.

  ![Painel "Adicionar conjunto back-end" do Balanceador de carga](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. No Olá **adicionar conjunto back-end** painel, introduza o nome Olá do conjunto de back-end Olá.
4. Adicione máquinas individuais ou um conjunto de back-end de toohello de conjunto de disponibilidade.

#### <a name="configure-a-probe"></a>Configurar uma sonda

1. No seu Balanceador de carga em **definições**, selecione **sondas**e, em seguida, clique em **adicionar** tooadd uma sonda.

 ![Painel "Adicionar sonda" de Balanceador de carga](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. No Olá **adicionar sonda** painel, introduza o nome Olá para a sonda de Olá.
3. Selecione Olá **protocolo** para a sonda de Olá. Para uma base de dados, pode querer uma sonda TCP, em vez de uma pesquisa HTTP. toolearn mais informações sobre pesquisas de Balanceador de carga, consulte demasiado[sondas de Balanceador de carga de compreender](../load-balancer/load-balancer-custom-probe-overview.md).
4. Introduza Olá **porta** do seu toobe de base de dados utilizada para aceder a sonda de Olá.
5. Em **intervalo**, especifique a frequência tooprobe Olá a aplicação.
6. Em **limiar de mau estado de funcionamento**, especifique o número de Olá de falhas de sonda contínua, que deve ocorrer para Olá back-end VM toobe considerado em mau estado de funcionamento.
7. Clique em **OK** sonda de Olá toocreate.

#### <a name="configure-hello-load-balancing-rules"></a>Configurar regras de balanceamento de carga Olá

1. Em **definições** do seu Balanceador de carga, selecione **as regras de balanceamento de carga**e, em seguida, clique em **adicionar** toocreate uma regra.
2. No Olá **regra de balanceamento de carga de adicionar** painel, introduza Olá **nome** para a regra de balanceamento de carga Olá.
3. Escolha Olá **endereço de IP de front-end** de Olá o Balanceador de carga, **protocolo**, e **porta**.
4. Em **porta back-end**, especifique Olá toobe de porta utilizada no conjunto de back-end Olá.
5. Selecione Olá **conjunto back-end** e Olá **sonda** que foram criados no Olá anterior passos tooapply Olá regra.
6. Em **persistência da sessão**, escolha como pretende que Olá sessões toopersist.
7. Em **tempos limite de inatividade**, especifique o número de Olá de minutos antes de um tempo limite de inatividade.
8. Em **IP flutuante**, selecione **desativado** ou **ativado**.
9. Clique em **OK** regra de Olá toocreate.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>Passo 5: Ligar o Balanceador de carga do camada web VMs toohello

Agora, iremos configurar Olá porta IP de Balanceador de carga e endereço front-end em aplicações de Olá que estão em execução em VMs a camada web para todas as ligações de base de dados. Esta configuração é aplicações toohello específicas que são executados nestas VMS. o endereço IP de destino tooconfigure Olá e a porta, consulte a documentação da aplicação de toohello. endereço IP Olá toofind de Olá front-end, no portal do Azure, de Olá avance conjunto IP Front-end toohello Olá **definições do Balanceador de carga** painel.

![Painel de navegação de "Conjunto de IP de front-end" de Balanceador de carga](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Passos seguintes

* [Descrição geral do Gestor de tráfego](traffic-manager-overview.md)
* [Descrição geral do Gateway de aplicação](../application-gateway/application-gateway-introduction.md)
* [Descrição Geral do Balanceador de Carga do Azure (Azure Load Balancer overview)](../load-balancer/load-balancer-overview.md)
