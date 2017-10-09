---
title: "aaaTesting o serviço de dados oferecem para Olá Marketplace | Microsoft Docs"
description: "Compreenda como tootest o serviço de dados oferecem para Olá Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Testar a sua oferta de serviço de dados no modo de transição
> [!IMPORTANT]
> **Neste momento, estamos já não integração qualquer nova editores de serviço de dados. Novo dataservices não irá obter aprovada para listagem.** Se tiver uma aplicação de negócio de SaaS que gostaria de toopublish pode encontrar mais informações no AppSource [aqui](https://appsource.microsoft.com/partners). Se tiver um aplicações IaaS ou para programadores de serviço teria como toopublish no Azure Marketplace pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Depois de concluir os primeiros dois passos, Olá de [criar a sua conta Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) e [criar a sua oferta de serviço de dados de mensagens em fila no Portal de publicação](marketplace-publishing-data-service-creation.md) está pronto para disponibilizar a oferta Olá Azure Marketplace. Este tópico irá guiá-lo Olá pela primeira vez, intermediária, passo chamada "transição"

Significa que implementar a sua oferta no privado "sandbox", onde pode testar e verificar a respetiva funcionalidade antes de enviar-tooproduction de teste. oferta de Olá será apresentado tal como qualquer cliente de tooa que implementou, de transição.

## <a name="step-1-pushing-your-offer-toostaging"></a>Passo 1. Enviar a sua oferta toostaging
Enviar a sua oferta toostaging permite-lhe oferta de Olá tootest antes de ficar disponíveis toofuture subscritores.  Pode ver como oferta irá aparecer e funcionar os subscrever tooyour dados.  

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. Início de sessão para Olá [Portal de publicação](https://publish.windowsazure.com)
2. Selecione **serviços de dados** na janela de navegação esquerdo Olá
3. Selecione a sua oferta pretende toopush toostaging. Verá Olá acima ecrã.
4. Clique em **Push tooStaging** botão.  
5. Se existirem problemas com Olá oferta necessário toobe concluída toostaging toopushing anterior, verá uma lista apresentada.  Corrija estes itens clicando em cada item na lista de Olá. Quando todas as correções efetuadas, clique em **Push tooStaging** botão novamente.

Se existirem sem problemas com a sua oferta verá a janela de pop-up de Olá abaixo.  

Se não tiver planeamento/não aprovado toosurface oferta no Portal do Azure (atualmente limitou capacidade), em seguida, janela de pop-up Olá apenas fechar.

tootest os dados de serviço no Portal do Azure (no portal do adição toohello DataMarket), terá de tootest um ID de subscrição do Azure com.  Este ID de subscrição irá identificar a conta de Olá que será permitido tootest oferta.  

Cortar e colar o ID de subscrição e clique em Olá toocontinue de marca de verificação.

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Estes IDs de subscrições do Azure só são necessárias para teste e transição em Olá [Azure Management Portal](https://manage.windowsazure.com). Não são necessária tootest no Azure Marketplace.
> 
> 

Olá aparecimento do ecrã que aparece mostra que a publicação está a decorrer, apresentando Olá "em curso" ícone realçado amarelo abaixo. Enviar toostaging demora entre 10 too15 minutos.  Se demora mais, atualize primeiro o seu browser (prima F5 no IE).  Em casos raros olá onde a oferta é ainda enviar toostaging depois de uma hora, clique em contactar Olá nos toolet-na saber que existe um problema de ligação.

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Quando terminar de Olá Push tooStaging Olá "em curso" ícone deixa de mover e Olá será possível atualizar o estado demasiado "teste".  Está agora pronto tootest oferta.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>Passo 2. Testar a sua oferta faseada DataMarket
Clique em seguinte texto Olá de ligação de Olá **"consulte o seu serviço oferecem em..."** ecrã de Olá toodisplay que Olá subscritor verá quando a sua oferta fica tooproduction e aparecerá na DataMarket.

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Testar ou certifique-se de que cada um dos itens de 12 Olá marcada acima tooensure todos os logótipos os preços/transações, texto, imagens, documentação e as ligações estão corretos e a funcionar corretamente.  Este é um tooensure boa altura quaisquer valores de teste que introduziu ao criar a sua oferta foram substituídos por valores reais.

1. Logótipo da oferta
2. Nome da oferta
3. Web site da empresa de publicador, nome/link tooyour
4. Categorias de pesquisa para a sua oferta
5. Subscritores de tooassist de ligação de suporte da oferta
6. Contextual descrição para a sua oferta
7. Plano de oferta que mostram os detalhes de faturação
8. Ligação tooimplementation código
9. Imagens de exemplo que ilustram a utilização de dados da oferta
10. Metadados de entrada/saída para cada serviço dentro de oferta de Olá
11. Termos do oferta de utilização
12. Pré-visualização de dados da oferta de Olá

Por fim, verifique o serviço de Olá funcionará através de Olá Datamarket clicando Olá hiperligação "EXPLORAR este conjunto de dados".  Irá abrir uma nova janela na ferramenta de Olá chamamos "Explorador de serviço", de modo pode pré-visualizar resultados Olá de uma consulta relativamente ao seu serviço.  Nesta janela, pode introduzir Olá parâmetros necessitam e ver resultados de Olá apresentados por uma consulta relativamente ao seu serviço.   Além disso, apresentado é o URL de Olá na sua consulta.  

> [!NOTE]
> Ser se tooreview Olá descrição textual do serviço de Olá apresentada na parte superior do Olá.  E se a oferta é composta por mais do que um serviço chamar, clique em Olá nos separadores na Olá inferior tooswitch toohello seguinte serviço tooreview e testar.
> 
> 

## <a name="next-step"></a>Passo seguinte
Se estiver a ter problemas e precisar de ajuda para resolvê-los contacte [suporte do Editor de Azure](http://go.microsoft.com/fwlink/?LinkId=272975).

Se estiver satisfeito e toopublish pronto a oferta leia Olá [aprovação do pedido tooPush tooProduction](marketplace-publishing-push-to-production.md) documentação.

## <a name="see-also"></a>Veja Também
* [Introdução: Como toopublish toohello uma oferta Azure Marketplace](marketplace-publishing-getting-started.md)

