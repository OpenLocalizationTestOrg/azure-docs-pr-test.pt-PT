---
title: "implementação do aaaHigh disponibilidade entre geográfica AD FS no Azure com o Gestor de tráfego do Azure | Microsoft Docs"
description: "Este documento ficará a saber como toodeploy do AD FS no Azure para disponibilidade elevada."
keywords: "AD fs com o Gestor de tráfego do Azure, o AD FS com o Traffic Manager do Azure, geográfica, múltiplos centros de dados, geográficos dos centros de dados, várias geográfica dos centros de dados, implementar o AD FS no azure, implementar adfs do azure, adfs do azure, azure ad fs, implementar o AD FS, implementar o AD FS no azure, do ad fs implementar o AD FS no azure, implementar o AD FS no azure, azure AD FS, introdução tooAD FS, do Azure, o AD FS no Azure, iaas, AD FS, move tooazure de adfs"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Implementação de AD FS geográficos cruzados de elevada disponibilidade no Azure com o Gestor de Tráfego do Azure
[Implementação do AD FS no Azure](active-directory-aadconnect-azure-adfs.md) fornece orientação passo a passo como toohow pode implementar uma infraestrutura do AD FS simple para a sua organização no Azure. Este artigo fornece os passos seguintes Olá toocreate um entre geográfica implementação do AD FS no Azure com [Traffic Manager do Azure](../traffic-manager/traffic-manager-overview.md). Traffic Manager do Azure ajuda a criar um geograficamente propagação elevada disponibilidade e a infraestrutura do AD FS de elevado desempenho para a sua organização, tornando a utilização de intervalo de métodos de encaminhamento disponível toosuit diferentes necessita da infraestrutura de Olá.

Permite uma infraestrutura do AD FS geográfica cruzada de elevada disponibilidade:

* **Eliminação de um ponto único de falha:** com capacidades de ativação pós-falha do Gestor de tráfego do Azure, pode conseguir uma infraestrutura do AD FS altamente disponível, mesmo quando um dos centros de dados de Olá na parte globo Olá fica inativo
* **Desempenho melhorado:** pode utilizar Olá de sugestões de implementação no tooprovide artigo uma infraestrutura de AD FS de elevado desempenho que pode ajudar os utilizadores a autenticar mais rapidamente. 

## <a name="design-principles"></a>Princípios de conceção
![Estrutura global](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

princípios de design básico Olá será mesmos conforme indicado em princípios de Design artigo Olá implementação do AD FS no Azure. Diagrama de Olá acima mostra uma extensão de região geográfica do Olá implementação básica tooanother simple. Seguem-se algumas tooconsider pontos quando expandir a sua região geográfica do toonew de implementação

* **Rede virtual:** deve criar uma nova rede virtual numa região geográfica Olá pretende que a infraestrutura do toodeploy adicional AD FS. Diagrama de Olá acima para ver Geo1 VNET e Geo2 VNET como Olá duas redes virtuais em cada região geográfica.
* **Controladores de domínio e servidores do AD FS na nova VNET geográfica:** recomenda-se os controladores de domínio toodeploy na região geográfica novo de Olá para que os servidores de Olá do AD FS na região novo Olá tenham toocontact um controlador de domínio na outra extremidade rede Away toocomplete uma autenticação e o desempenho de Olá assim melhorar.
* **Contas de armazenamento:** contas de armazenamento associados uma região. Uma vez que for implementar máquinas numa região geográfica novo, terá toocreate novas contas do storage toobe utilizado na região de Olá.  
* **Grupos de segurança de rede:** como contas de armazenamento, os Grupos de Segurança de Rede criados numa região não podem ser utilizados noutra região geográfica. Por conseguinte, terá toocreate nova rede segurança grupos semelhantes toothose na região geográfica primeiro de Olá de sub-rede INT e rede de Perímetro na região geográfica novo de Olá.
* **As etiquetas de DNS para endereços IP públicos:** Traffic Manager do Azure podem referir-se tooendpoints apenas através de etiquetas DNS. Por conseguinte, é necessário toocreate etiquetas DNS para os endereços IP públicos dos Olá externo balanceadores de carga.
* **Traffic Manager do Azure:** Gestor de tráfego do Microsoft Azure permite-lhe toocontrol distribuição Olá utilizador tráfego tooyour pontos finais do serviço em execução em datacenters diferentes em torno Olá mundo. Traffic Manager do Azure funciona em Olá nível DNS. Utiliza DNS respostas toodirect pelo utilizador final tráfego distribuída tooglobally pontos finais. Os clientes ligam, em seguida, pontos finais de toothose diretamente. Com diferentes opções de encaminhamento de desempenho, Weighted e prioridade, pode facilmente optar opção de encaminhamento Olá mais adequada para as necessidades da sua organização. 
* **V net tooV net conectividade entre duas regiões:** não precisa de toohave conectividade entre redes virtuais Olá próprio. Uma vez que cada rede virtual tem acesso toodomain controladores e tem o servidor do AD FS e WAP própria, pode funcionam sem qualquer conectividade entre redes virtuais do Olá em regiões diferentes. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Passos toointegrate Traffic Manager do Azure
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Implementar o AD FS na região geográfica novo de Olá
Siga os passos de Olá e as diretrizes no [implementação do AD FS no Azure](active-directory-aadconnect-azure-adfs.md) toodeploy Olá topologia mesma região geográfica novo de Olá.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Etiquetas de DNS para os endereços IP públicos de Olá com acesso à Internet (público) balanceadores de carga
Tal como mencionado acima, Olá Traffic Manager do Azure só pode referenciar tooDNS etiquetas como pontos finais e, por conseguinte, é importante toocreate etiquetas DNS para os endereços IP públicos dos Olá externo balanceadores de carga. Abaixo captura de ecrã mostra como pode configurar a etiqueta de DNS para endereço IP público Olá. 

![Etiqueta de DNS](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Implementar o Gestor de Tráfego do Azure
Siga os passos de Olá abaixo toocreate um perfil do Gestor de tráfego. Para obter mais informações, também pode consultar demasiado[gerir um perfil do Traffic Manager do Azure](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Criar um perfil do Gestor de Tráfego:** atribua um nome exclusivo ao seu perfil do Gestor de Tráfego. Este nome de perfil de Olá faz parte do nome DNS Olá e age como um prefixo de etiqueta Olá do nome de domínio do Traffic Manager. nome de Olá / prefixo é adicionado too.trafficmanager.net toocreate uma etiqueta de DNS para o Gestor de tráfego. Olá captura de ecrã abaixo mostra o Gestor de tráfego de Olá prefixo DNS que está a ser definido como mysts e a etiqueta DNS resultante será mysts.trafficmanager.net. 
   
    ![Criar um perfil do Gestor de Tráfego](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Método de encaminhamento de tráfego:** existem três opções de encaminhamento disponíveis no Gestor de Tráfego:
   
   * Prioridade 
   * Desempenho
   * Ponderada
     
     **Desempenho** Olá recomenda infraestrutura do opção tooachieve extremamente reativo AD FS. No entanto, pode escolher o método de encaminhamento mais adequado para as suas necessidades de implementação. funcionalidade do Olá AD FS não é afetada pela opção de encaminhamento Olá selecionada. Veja o artigo [Métodos de encaminhamento de tráfego do Gestor de Tráfego](../traffic-manager/traffic-manager-routing-methods.md) para obter mais informações. Olá captura de ecrã de exemplo acima, pode ver Olá **desempenho** método selecionado.
3. **Configurar pontos finais:** na página do Gestor de tráfego de Olá, clique em pontos finais e selecione Adicionar. Esta ação irá abrir uma adicionar ponto final página semelhante toohello captura de ecrã abaixo
   
   ![Configurar pontos finais](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Entradas de diferentes Olá, siga orientação Olá abaixo:
   
   **Tipo:** selecione o ponto final do Azure como podemos apontar tooan endereço IP público do Azure.
   
   **Nome:** criar um nome que pretende que o tooassociate com o ponto final de Olá. Isto não é o nome DNS Olá e não tem efeito em registos de DNS.
   
   **Tipo de recurso de destino:** endereço IP público Selecione como propriedade de toothis Olá value. 
   
   **Recurso de destino:** Isto irá dar-lhe uma opção toochoose das etiquetas DNS diferentes Olá que tem disponíveis na sua subscrição. Escolha Olá que etiqueta de DNS correspondente toohello ponto final que está a configurar.
   
   Adicione o ponto final para cada região geográfica que pretende Olá Traffic Manager do Azure tooroute o tráfego.
   Para obter mais informações e os passos detalhados sobre como tooadd / configurar pontos finais no Gestor de tráfego, consulte demasiado[adicionar, desativar, ativar ou eliminar pontos finais](../traffic-manager/traffic-manager-endpoints.md)
4. **Configurar a sonda:** na página do Gestor de tráfego de Olá, clique em configuração. Na página de configuração de Olá, é necessário toochange Olá monitor definições tooprobe na porta 80 do HTTP e o caminho relativo /adfs/probe
   
    ![Configurar a sonda](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Certifique-se de que estado Olá de pontos finais de Olá ONLINE após a conclusão da configuração de Olá**. Se todos os pontos finais no estado 'degradado', o Gestor de tráfego do Azure executará um melhor tráfego de Olá de tooroute tentativa partindo do princípio de que o diagnóstico Olá está incorreto e todos os pontos finais estão acessíveis.
   > 
   > 
5. **A modificar registos DNS para o Gestor de tráfego do Azure:** o serviço de Federação deve ser um nome de DNS do Gestor de tráfego do Azure de toohello CNAME. Crie um CNAME no Olá registos DNS públicos para que, na verdade, quem está a tentar o serviço de Federação tooreach Olá atinge Olá Traffic Manager do Azure.
   
    Por exemplo, serviço de Federação do toopoint Olá fs.fabidentity.com toohello Gestor de tráfego, terá de tooupdate sua toobe registos de recursos DNS Olá seguintes:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Testar Olá encaminhamento e inicie sessão do AD FS
### <a name="routing-test"></a>Teste de encaminhamento
Um teste muito básico para o encaminhamento de Olá seria tootry ping Olá Federação serviço nome DNS de uma máquina em cada região geográfica. Consoante o método de encaminhamento Olá escolhido, ponto final de Olá, na verdade, ping sobre será refletido na apresentação de ping de Olá. Por exemplo, se tiver selecionado o desempenho de Olá encaminhamento, em seguida, o ponto final de Olá mais próximo toohello região do cliente de Olá irá ser atingido. Segue-se instantâneo Olá dois pings a partir de dois computadores de cliente de região diferente, um EastAsia região e o outro nos EUA oeste. 

![Teste de encaminhamento](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Teste de início de sessão do AD FS
Olá tootest da forma mais fácil do AD FS é utilizar a página IdpInitiatedSignon.aspx de Olá. Na ordem toobe toodo capaz de que, é necessário tooenable Olá IdpInitiatedSignOn nas propriedades de Olá do AD FS. Siga os passos de Olá abaixo tooverify a configuração do AD FS

1. Executar Olá cmdlet abaixo no servidor do Olá AD FS, com o PowerShell, tooset-tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Em qualquer máquina externa, aceda a https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Deverá ver a página Olá do AD FS, conforme mostrado abaixo:
   
    ![Teste de ADFS - desafio de autenticação](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    e após o início de sessão com êxito, é-lhe apresentada uma mensagem de êxito, conforme mostrado abaixo:
   
    ![Teste de ADFS - autenticação bem sucedida](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Ligações relacionadas
* [Implementação básica do AD FS no Azure](active-directory-aadconnect-azure-adfs.md)
* [Gestor de Tráfego do Microsoft Azure](../traffic-manager/traffic-manager-overview.md)
* [Métodos de encaminhamento de tráfego do Gestor de Tráfego](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Passos seguintes
* [Gerir um perfil no Traffic Manager do Azure](../traffic-manager/traffic-manager-manage-profiles.md)
* [Adicionar, desativar, ativar ou eliminar pontos finais](../traffic-manager/traffic-manager-endpoints.md) 

