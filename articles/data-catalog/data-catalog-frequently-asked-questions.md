---
title: "aaaAzure catálogo de dados perguntas mais frequentes | Microsoft Docs"
description: "Perguntas mais frequentes sobre o catálogo de dados do Azure, incluindo as capacidades de deteção de origem de dados, anotação e gestão."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Perguntas mais frequentes sobre o catálogo de dados do Azure
Este artigo fornece respostas toofrequently pedido perguntas relacionadas com o serviço de catálogo de dados do Azure toohello.

## <a name="what-is-azure-data-catalog"></a>O que é o Catálogo de Dados do Azure?
Catálogo de dados é um serviço completamente gerido, alojado no Microsoft Azure, o que funciona como um sistema de registo e a deteção de origens de dados empresariais. Catálogo de dados, qualquer utilizador, de cientistas de toodata analistas e os programadores, pode registar, detetar, compreender e consumir origens de dados.

## <a name="what-customer-challenges-does-it-solve"></a>O cliente desafia o does resolver?
Endereços do catálogo de dados Olá desafios de deteção de origem de dados e de "dados escuros", para que os utilizadores podem detetar e compreender origens de dados empresariais.

## <a name="what-are-its-target-audiences"></a>Quais são o público-alvo?
Catálogo de dados foi concebido para utilizadores técnicos e não técnicos, incluindo:

* Os programadores de dados e profissionais de BI e a análise: pessoas que são responsáveis pela produzir dados e análise de conteúdo para outros tooconsume.
* Stewards de dados: pessoas que têm conhecimento de Olá sobre Olá dados, o que significa e como é toobe pretendido utilizado.
* Os consumidores de dados: as pessoas que precisa de tooeasily capaz de toobe detetar, compreender e ligar dados toohello precisam toodo o trabalho e utilizando a ferramenta Olá à escolha.
* Central IT: as pessoas que precisam de toomake centenas de origens de dados detetável por utilizadores de empresas e que precisam de supervisão toomaintain como dados está a ser utilizados e por quem.

## <a name="what-is-its-availability-by-region"></a>O que é a disponibilidade do mesmo por região?
Serviços de catálogo de dados estão atualmente disponíveis no Olá seguintes centros de dados:

* EUA Oeste
* EUA Leste
* Europa Ocidental
* Europa do Norte
* Leste da Austrália
* Sudeste Asiático

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>Quais são os limites no número de Olá de recursos de dados?
Olá livre Edition do catálogo de dados é limitado too5, recursos de dados registados 000.

Olá Standard Edition do catálogo de dados suporta segurança too100, 000 registar recursos de dados.

## <a name="what-are-its-supported-data-source-and-asset-types"></a>Quais são os respetivos tipos de recursos e de origem de dados suportados?
Para obter uma lista de origens de dados atualmente suportados, consulte [DSR do catálogo de dados](data-catalog-dsr.md).

## <a name="how-do-i-request-support-for-another-data-source"></a>O pedido de suporte para outra origem de dados?
toosubmit funcionalidade pedidos e outros comentários, aceda toohello [fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-do-i-get-started-with-data-catalog"></a>Como começar a utilizar com o catálogo de dados?
Olá melhor forma tooget iniciado é acedendo demasiado[introdução ao catálogo de dados](data-catalog-get-started.md). Este artigo é uma descrição geral ponto-a-ponto capacidades Olá no serviço de Olá.

## <a name="how-do-i-register-my-data"></a>Como registar a meus dados?
tooregister os dados no catálogo de dados:
1. No portal do catálogo de dados do Azure Olá, no Olá **publicar** área, a ferramenta de registo do início Olá catálogo de dados do Azure. 
2. No catálogo de dados de Olá publicação da aplicação, inicie sessão com Olá mesmas credenciais que utilizam tooaccess Olá portal do catálogo de dados.
3. Selecione a origem de dados de Olá e ativos específicos Olá que pretende que o tooregister.

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>As propriedades que se extrair para recursos de dados que estão registados?
propriedades específicas Olá diferem origem toodata da origem de dados, mas, em geral, Olá serviço de publicação do catálogo de dados extrai Olá seguintes informações:

* Nome do recurso
* Tipo de recurso
* Descrição de recurso
* Nomes de atributo/coluna
* Tipos de dados de atributo/coluna
* Descrição de atributo/coluna

> [!IMPORTANT]
> Registar recursos de dados com o catálogo de dados não mover ou copiar o dados toohello na nuvem. Registar recursos de uma origem de dados cópias Olá tooAzure de metadados dos recursos, mas dados Olá permanecem na localização de origem de dados existente Olá. regra de toothis Olá exceção é se escolher um perfil de dados ou registos de pré-visualização tooupload ao registar recursos de Olá. Ao incluir uma pré-visualização, cópia de segurança too20 registos são copiados de cada recurso e armazenados como instantâneo no catálogo de dados. Ao incluir um perfil de dados, agregam informações são calculadas e incluídas nos metadados de Olá armazenados no catálogo de Olá. Agregam informações pode incluir o tamanho de Olá das tabelas, Olá percentagem de valores nulos por coluna ou Olá mínima, máximo e médio valores em colunas. 
>
>

> [!NOTE]
> Para origens de dados, tais como o SQL Server Analysis Services que tenha uma primeira classe **Descrição** propriedade, Olá catálogo de dados de publicação aplicação extrai esse valor de propriedade. Para bases de dados relacionais de SQL Server, que não dispõem de uma primeira classe **Descrição** propriedade, Olá aplicação publicação do catálogo de dados extrai o valor de Olá de Olá **ms_description** propriedade expandida para objetos e colunas. Para obter mais informações, consulte [utilizando propriedades expandidas em objetos de base de dados](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx).
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>Quanto deve necessário para tooappear de recursos recentemente registados no catálogo de Olá?
Depois de registar recursos de catálogo de dados, poderão ocorrer durante um período de 5 segundos de too10 antes de serem apresentados no portal do catálogo de dados de Olá.

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>Como anotar e enriqueça Olá metadados para os meus recursos de dados registados?
Olá mais simples forma tooprovide metadados para recursos registados é tooselect Olá recurso no portal do catálogo de dados de Olá e, em seguida, introduza valores Olá no painel de propriedades de Olá ou no painel de esquema para o objeto selecionado Olá.

Também pode fornecer alguns metadados, como especialistas e etiquetas, durante o processo de registo de Olá. os valores de Olá que fornecem no serviço de publicação do catálogo de dados de Olá aplicam ativos tooall a ser registados nessa altura. Olá tooview recentemente registou objetos no portal de Olá anotação adicionais, selecione de Olá **ver Portal** botão no ecrã final de Olá de Olá aplicação publicação do catálogo de dados.

## <a name="how-do-i-delete-my-registered-data-objects"></a>Como eliminar o meu objetos de dados registados
Pode eliminar um objeto do catálogo de dados selecionando o objeto de Olá no portal de Olá e, em seguida, clicando em Olá **eliminar** botão. Remover objetos de Olá remove os seus metadados do catálogo de dados, mas não afetam a origem de dados subjacente Olá.

## <a name="what-is-an-expert"></a>O que é um especialista?
Um especialista é uma pessoa que tenha uma perspetiva-se informado sobre um objeto de dados. Um objeto pode ter vários especialistas. Um especialista não precisa de toobe Olá "proprietário" de um objeto, mas é simplesmente a alguém que sabe como dados de Olá podem e deve ser utilizado.

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>Como posso partilharem informações com a equipa do catálogo de dados de Olá se posso encontrar problemas?
tooreport devido a problemas, partilham informações e fazer perguntas, aceda toohello [fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>Olá catálogo funciona com outra origem de dados que estou interessado em?
Ativamente estamos a trabalhar adicionar mais tooData de origens de dados catálogo. Se quiser toosee suportada uma origem de dados específica, sugerimos (ou o suporte de voz, se já tiver sido sugerido) por vai toohello [fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>Como é o catálogo de dados do Azure relacionados com toohello catálogo de dados no Power BI para Office 365?
Pode considerar do catálogo de dados do Azure como uma evolução do Olá catálogo de dados no Power BI. A partir de mola 2017, o catálogo de dados do Azure é utilizado tooenable Olá partilha e a deteção de consultas no Excel 2016 e o Power Query para Excel. Capacidades do catálogo de dados no Excel estão disponíveis toousers com licenças Power BI Pro.

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>O que fazem permissões necessário tooregister ativos com o catálogo de dados?
ferramenta de registo do toorun Olá catálogo de dados, necessita de permissões na origem de dados de Olá permite-lhe tooread Olá metadados a partir da origem de Olá. tooalso incluir uma pré-visualização, tem de ter as permissões que permitem-lhe tooread nos dados de Olá objetos Olá a ser registado.

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>Será catálogo de dados seja disponibilizado para, bem como a implementação no local?
Catálogo de dados é um serviço em nuvem que pode trabalhar com toodeliver de origens de dados na nuvem e no local uma solução de deteção de origem de dados híbrida. Não existem atualmente não planos para uma versão de Olá serviço de catálogo de dados que é executado no local.

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>Pode extrair metadados mais ou rico de origens de dados de Olá que o registo?
Estamos a ativamente capacidades de Olá tooexpand do catálogo de dados. Se pretender que os metadados de adicionais toohave extraídos da origem de dados de Olá durante o registo, sugerimos (ou votos para o mesmo, se já tiver sido sugerido) no Olá [fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). No futuro, Olá, permitiremos partes terceiros tooadd nova origem tipos de dados através de uma API de extensibilidade.

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>Como restringir visibilidade de Olá dos recursos de dados registados, para que apenas determinadas pessoas podem detetá-los?
Selecione recursos de dados de Olá na Olá catálogo de dados e, em seguida, clique em Olá **obter propriedade** botão. Os proprietários de recursos de dados no catálogo de dados podem alterar a visibilidade de Olá definições tooeither permitir Olá toodiscover todos os utilizadores, recursos de empresa ou restringir os utilizadores de toospecific visibilidade.

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>Como atualizar o registo de Olá para um recurso de dados para que as alterações da origem de dados de Olá são refletidas no catálogo de Olá?
metadados de Olá tooupdate para recursos de dados que já estão registados no catálogo de Olá, basta volte a registar origem de dados de Olá que contenha recursos Olá. As alterações da origem de dados de Olá, tais como colunas a ser adicionadas ou removidas de tabelas ou vistas, são atualizadas no catálogo de Olá, mas qualquer anotações fornecidas pelos utilizadores são retidas.

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>A minha pergunta não é atendida aqui. Onde ir para respostas
Aceda toohello [fórum do catálogo de dados do Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). Perguntas mais frequentes existe irão orientar os respetivos aqui.
