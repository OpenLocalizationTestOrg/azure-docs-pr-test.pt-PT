---
title: "método de encaminhamento utilizando o Gestor de tráfego do Azure de tráfego de prioridade aaaConfigure | Microsoft Docs"
description: "Este artigo explica como o método de encaminhamento no Gestor de tráfego de tráfego de prioridade de Olá tooconfigure"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Configurar o método de encaminhamento de tráfego de prioridade no Gestor de tráfego

Independentemente do modo de Web site Olá, Web sites do Azure já fornece a funcionalidade de ativação pós-falha para os Web sites num centro de dados (também conhecido como região). Gestor de tráfego fornece ativação pós-falha para Web sites em datacenters diferentes.

Um padrão comum para ativação pós-falha do serviço é toosend tráfego tooa primário serviço e forneça um conjunto de serviços de cópia de segurança idênticos para ativação pós-falha. Olá passos seguintes explicam como tooconfigure isto definida ativação pós-falha com Web sites e serviços em nuvem do Azure:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>método encaminhamento de tráfego prioridade de Olá tooconfigure

1. Num browser, inicie sessão no toohello [portal do Azure](http://portal.azure.com). Se ainda não tiver uma conta, pode inscrever-se para obter uma [avaliação gratuita durante um mês](https://azure.microsoft.com/free/). 
2. Na barra de pesquisa do portal de Olá, procure Olá **perfis do Traffic Manager** e, em seguida, clique em nome do perfil Olá que pretende que o método de encaminhamento Olá tooconfigure para.
3. No Olá **perfil do Traffic Manager** painel, certifique-se de que ambos Olá serviços em nuvem e Web sites que pretende que tooinclude na configuração estão presentes.
4. No Olá **definições** secção, clique em **configuração**e em Olá **configuração** painel, concluída, da seguinte forma:
    1. Para **definições do método de encaminhamento de tráfego**, certifique-se de que o método de encaminhamento de tráfego do Olá **prioridade**. Se não for, clique em **prioridade** na lista pendente de Olá.
    2. Conjunto Olá **definições de Endpoint Protection do monitor** idêntica para todas as cada ponto final dentro deste perfil da seguinte forma:
        1. Selecione Olá adequado **protocolo**e especifique Olá **porta** número. 
        2. Para **caminho** escreva uma barra  */* . pontos finais de toomonitor, tem de especificar um caminho e nome de ficheiro. A barra de reencaminhar "/" é uma entrada válida para o caminho relativo Olá e implica que o ficheiro Olá está no diretório de raiz Olá (predefinição).
        3. Na Olá parte superior da página Olá, clique em **guardar**.
5. No Olá **definições** secção, clique em **pontos finais**.
6. No Olá **pontos finais** painel, reveja Olá ordem de prioridade para os pontos finais. Quando seleciona Olá **prioridade** ordem Olá de pontos finais de Olá selecionado de método de encaminhamento de tráfego, é importante. Certifique-se a ordem de prioridade de Olá dos pontos finais.  Olá primário o ponto final está na parte superior. Verificar na ordem de Olá que apresentá-la. todos os pedidos serão encaminhadas toohello primeiro ponto final e se o Gestor de tráfego detetar-ser mau estado de funcionamento, o tráfego de Olá automaticamente a ativação pós-falha toohello próximo ponto final. 
7. toochange Olá ordem de prioridade de ponto final, clique em ponto final de Olá e em Olá **Endpoint** painel que é apresentado, clique em **editar** e alterar Olá **prioridade** valor conforme necessário . 
8. Clique em **guardar** toosave alterar as definições de ponto final de Olá.
9. Depois de concluir as alterações de configuração, clique em **guardar** em Olá parte inferior da página Olá.
10. Teste alterações Olá na configuração da seguinte forma:
    1.  Na barra de pesquisa do portal de Olá, procure o nome de perfil do Traffic Manager Olá e clique em perfil do Traffic Manager Olá nos resultados de Olá esse Olá apresentado.
    2.  No Olá **Gestor de tráfego** painel do perfil, clique em **descrição geral**.
    3.  Olá **perfil do Traffic Manager** painel apresenta o nome DNS de Olá do perfil do Traffic Manager recentemente criado. Isto pode ser utilizado por quaisquer clientes (por exemplo, ao navegar tooit utilizando um browser) tooget encaminhado toohello direita ponto final conforme determinado pela tipo Olá de encaminhamento. Neste caso, todos os pedidos são encaminhadas toohello primeiro ponto final e se o Gestor de tráfego detetar-ser mau estado de funcionamento, o tráfego de Olá automaticamente a ativação pós-falha toohello próximo ponto final.
11. Assim que o perfil do Traffic Manager está a funcionar, edite registo de DNS de Olá no seu toopoint de servidor DNS autoritativo a sua empresa toohello Gestor de tráfego domínio nome do domínio.

![Configurar o método de encaminhamento de tráfego de prioridade utilizando o Gestor de tráfego][1]

## <a name="next-steps"></a>Passos seguintes


- Saiba mais sobre [ponderado método de encaminhamento de tráfego](traffic-manager-configure-weighted-routing-method.md).
- Saiba mais sobre [método de encaminhamento de desempenho](traffic-manager-configure-performance-routing-method.md).
- Saiba mais sobre [método de encaminhamento geográfico](traffic-manager-configure-geographic-routing-method.md).
- Saiba como demasiado[testar as definições do Gestor de tráfego](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png