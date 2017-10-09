---
title: origens de dados de perfil de tooData aaaHow
description: "Realce como dados de nível de tabela e coluna tooinclude perfis quando registar origens de dados no catálogo de dados do Azure e como os dados toouse perfis de origens de dados de toounderstand tooarticle como."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a>Origens de dados de perfis de dados
## <a name="introduction"></a>Introdução
**Catálogo de dados do Microsoft Azure** é um serviço em nuvem completamente gerido que funciona como um sistema de registo e de deteção de origens de dados empresariais. Por outras palavras, **catálogo de dados do Azure** está tudo sobre Ajuda pessoas detetar, compreender e utilizar origens de dados e ajudar as organizações tooget mais valor a partir da respetiva dados existentes. Quando uma origem de dados é registada com **catálogo de dados do Azure**, os metadados é copiado e indexado pelo serviço de Olá, mas o bloco de Olá não termina não existe.

Olá **a criação de perfis de dados** funcionalidade do **catálogo de dados do Azure** analisa os dados de Olá de origens de dados suportados no seu catálogo e recolhe estatísticas e as informações sobre os dados. É fácil tooinclude um perfil dos seus recursos de dados. Ao registar um recurso de dados, escolha **incluir perfil de dados** na ferramenta de registo da origem de dados de Olá.

## <a name="what-is-data-profiling"></a>O que é a criação de perfis de dados
A criação de perfis de dados examina dados Olá na origem de dados de Olá a ser registado e recolhe estatísticas e as informações sobre os dados. Durante a deteção de origem de dados, estas estatísticas podem ajudar a determinar adequabilidade Olá de Olá dados toosolve seu problema empresarial.

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

Olá seguintes origens de dados suportam a criação de perfis de dados:

* SQL Server (incluindo BD SQL do Azure e Azure SQL Data Warehouse) tabelas e vistas
* Oracle tabelas e vistas
* Teradata tabelas e vistas
* Tabelas do Hive

Perfis de dados, incluindo quando registar recursos de dados ajuda os utilizadores a responder às perguntas sobre origens de dados, incluindo:

* Este pode ser utilizado toosolve meu problema empresarial?
* Dados Olá está em conformidade com as normas de tooparticular ou padrões?
* Quais são alguns dos anomalias Olá Olá da origem de dados?
* O que são possíveis desafios de integrar estes dados na minha aplicação?

> [!NOTE]
> Também pode adicionar documentação tooan asset toodescribe como dados podem ser integrados numa aplicação. Consulte [como origens de dados de toodocument](data-catalog-how-to-documentation.md).
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a>Como tooinclude dados de perfil ao registar uma origem de dados
É fácil tooinclude um perfil da sua origem de dados. Quando registar uma origem de dados no Olá **toobe objetos registado** painel do registo da origem de dados Olá ferramenta, escolha **incluir perfil de dados**.

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

mais informações sobre como toolearn como tooregister origens de dados, consulte [como origens de dados de tooregister](data-catalog-how-to-register.md) e [introdução ao catálogo de dados do Azure](data-catalog-get-started.md).

## <a name="filtering-on-data-assets-that-include-data-profiles"></a>Filtragem de recursos de dados que incluem perfis de dados
recursos de dados de toodiscover que incluem um perfil de dados, pode incluir `has:tableDataProfiles` ou `has:columnsDataProfiles` como um dos seus termos de pesquisa.

> [!NOTE]
> Selecionar **incluir perfil de dados** nos dados de Olá ferramenta de registo de origem inclui a tabela e as informações do perfil de nível de coluna. No entanto, hello API do catálogo de dados permite toobe de recursos de dados registados com apenas um conjunto de informações de perfil incluídas.
>
>

## <a name="viewing-data-profile-information"></a>Ver as informações de perfil de dados
Depois de encontrar uma origem de dados adequado com um perfil, pode ver detalhes do perfil de dados de Olá. dados de Olá tooview perfil, selecione um recurso de dados e escolha **dados perfil** na janela portal do catálogo de dados Olá.

![](media/data-catalog-data-profile/data-catalog-view.png)

Um perfil de dados no **catálogo de dados do Azure** mostra tabela e informações de perfil de coluna, incluindo:

### <a name="object-data-profile"></a>Perfil de dados de objeto
* Número de linhas
* Tamanho da tabela
* Quando o objeto de Olá última atualização

### <a name="column-data-profile"></a>Perfil de dados da coluna
* Tipo de dados da coluna
* Número de valores distintos
* Número de linhas com valores nulos
* Mínimo, máximo, média e desvio padrão para valores da coluna

## <a name="summary"></a>Resumo
A criação de perfis de dados fornece estatísticas e informações sobre como registar dados ativos toohelp determinar adequabilidade Olá de Olá dados toosolve alguns dos problemas empresariais. Juntamente com anotar e documentar origens de dados, perfis de dados podem dar aos utilizadores uma compreensão mais aprofundada dos seus dados.

## <a name="see-also"></a>Veja Também
* [Como tooregister origens de dados](data-catalog-how-to-register.md)
* [Introdução ao Catálogo de Dados do Azure](data-catalog-get-started.md)
