---
title: aaaHow tooconnect toodata origens | Microsoft Docs
description: "Realce a forma como tooconnect toodata origens detetaram com o catálogo de dados do Azure tooarticle como."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Como tooconnect toodata origens
## <a name="introduction"></a>Introdução
**Catálogo de dados do Microsoft Azure** é um serviço em nuvem completamente gerido que funciona como um sistema de registo e de deteção de origens de dados empresariais. Por outras palavras, **catálogo de dados do Azure** está tudo sobre Ajuda pessoas detetar, compreender e utilizar origens de dados e ajudar as organizações tooget mais valor a partir da respetiva dados existentes. Um aspeto chave deste cenário é utilizar Olá origem de dados – depois de um utilizador Deteta uma data e compreende o objetivo, Olá passo seguinte consiste em tooconnect toohello da origem de dados tooput toouse respetivos dados.

## <a name="data-source-locations"></a>Localizações de origem de dados
Durante o registo da origem de dados, **catálogo de dados do Azure** recebe os metadados sobre a origem de dados de Olá. Estes metadados incluem detalhes de Olá da localização da origem de dados Olá. detalhes de Olá da localização de Olá irão variar origem toodata da origem de dados, mas sempre conterá Olá tooconnect de informações necessárias. Por exemplo, localização Olá para uma tabela do SQL Server inclui o nome de servidor Olá, nome de base de dados, nome de esquema e nome da tabela, enquanto a localização de Olá para um relatório do SQL Server Reporting Services inclui o nome do servidor de Olá e relatório de toohello Olá caminho. Outros tipos de origens de dados terão localizações refletem estrutura Olá e capacidades do sistema de origem Olá.

## <a name="integrated-client-tools"></a>Ferramentas de cliente integrada
Olá mais simples forma tooconnect tooa origem de dados é toouse Olá "Abrir em..." menu no Olá **catálogo de dados do Azure** portal. Este menu apresenta uma lista de opções para ligar a recursos de dados selecionados toohello.
Quando utilizar a vista em mosaico predefinido Olá, este menu está disponível no Olá cada mosaico.

 ![Abrir uma tabela do SQL Server no Excel a partir do mosaico de recurso de dados de Olá](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Quando utilizar a vista de lista de Olá, menu Olá está disponível na barra de pesquisa de Olá na Olá parte superior da janela de portal Olá.

 ![Abrir um relatório do SQL Server Reporting Services no Gestor de relatórios a partir da barra de pesquisa de Olá](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Aplicações de cliente suportados
Quando utilizar Olá "Abrir em..." origens de menu para os dados no portal do catálogo de dados do Azure de Olá, Olá correta de cliente aplicação tem de estar instalada no computador de cliente Olá.

| Abrir numa aplicação | Extensão de ficheiro / protocolo | Versões de aplicações suportados |
| --- | --- | --- |
| Excel |. odc |Excel 2010 ou posterior |
| Excel (primeiros 1000) |. odc |Excel 2010 ou posterior |
| Power Query |ou |Excel 2016 ou o Excel 2010 ou o Excel 2013 com Olá Power Query para o suplemento do Excel instalado |
| Ambiente de trabalho do Power BI |. pbix |Power BI Desktop Julho de 2016 ou posterior |
| SQL Server Data Tools |vsweb: / / |Visual Studio 2013 atualização 4 ou posterior com ferramentas do SQL Server instalada |
| Gestor de relatórios |http:// |Consulte [requisitos de browser do SQL Server Reporting Services](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Os dados, as ferramentas
Opções de Olá disponíveis no menu de Olá dependerá do tipo Olá do recurso de dados selecionado no momento. Obviamente, nem todas as ferramentas de possíveis serão incluídas Olá "Abrir em..." menu, mas é ainda fácil tooconnect origem de dados de toohello utilizando qualquer ferramenta de cliente. Quando um recurso de dados está selecionado na Olá **catálogo de dados do Azure** portal, localização concluída Olá é apresentada no painel de propriedades de Olá.

 ![Informações de ligação para uma tabela do SQL Server](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

informações de ligação de Olá detalhes serão diferentes do tipo de origem de toodata de tipo de origem de dados, mas as informações de Olá incluídas no portal de Olá irão dar-lhe tudo o que precisa de origem de dados de toohello tooconnect de qualquer ferramenta de cliente. Os utilizadores podem copiar detalhes da ligação Olá Olá origens de dados que são detetados utilizando **catálogo de dados do Azure**, ativá-las toowork com dados Olá na ferramenta de sua escolha.

## <a name="connecting-and-data-source-permissions"></a>Permissões de origem de dados e de ligação
Embora **catálogo de dados do Azure** faz com que as origens de dados detetável, acesso toohello dados propriamente ditos permanecem sob o controlo de Olá de proprietário de origem de dados de Olá ou administrador. Deteção de uma origem de dados de **catálogo de dados do Azure** não atribua um utilizador qualquer origem de dados de Olá de tooaccess de permissões em si.

toomake-lo mais fácil para os utilizadores que detetar um dados de origem, mas não dispõe de permissões tooaccess respetivos dados, os utilizadores podem fornecer informações na Olá propriedade pedir acesso ao anotar uma origem de dados. As informações fornecidas aqui – incluindo o processo de toohello ligações ou ponto de contacto para obter acesso à origem de dados – são apresentadas juntamente com informações da localização de origem de dados de Olá no portal de Olá.

 ![Informações de ligação com instruções de acesso de pedido fornecidas](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Resumo
Registar uma origem de dados com **catálogo de dados do Azure** faz com que os dados detetável por copiar os metadados estruturais e descritivo da origem de dados de Olá para Olá serviço de catálogo. Depois de uma origem de dados tiver sido registada e detetada, os utilizadores podem ligar toohello origem de dados de Olá **catálogo de dados do Azure** portal "Abrir em..." " menu ou utilizar as ferramentas de dados escolhidas.

## <a name="see-also"></a>Consultar também
* [Introdução ao catálogo de dados do Azure](data-catalog-get-started.md) tutorial para obter detalhes passo a passo sobre como tooconnect toodata origens.
