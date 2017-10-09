---
title: origens de dados de tooannotate aaaHow | Microsoft Docs
description: "Realce como tooarticle como recursos de dados de tooannotate no catálogo de dados do Azure, incluindo nomes amigáveis, etiquetas, descrições e especialistas."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5a7e6bb2-863c-4eca-b614-1c814920d9ed
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 1d1ef34e3f1ef73cdc65129209d938abe1e36c01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooannotate-data-sources"></a>Como tooannotate origens de dados
## <a name="introduction"></a>Introdução
**Catálogo de dados do Microsoft Azure** é um serviço em nuvem completamente gerido que funciona como um sistema de registo e de deteção de origens de dados empresariais. Por outras palavras, o catálogo de dados é tudo sobre ajudando as pessoas detetar, compreender e utilizar origens de dados e ajudar as organizações tooget valor mais partir dos respetivos dados existentes. Quando uma origem de dados é registada no catálogo de dados, os metadados é copiado e indexado pelo serviço de Olá, mas história Olá não termina não existe. Catálogo de dados permite que os utilizadores tooprovide os seus próprios Olá de toosupplement metadados descritivos – por exemplo, as etiquetas e descrições – metadados extraídos da origem de dados de Olá e mais compreensível toomore pessoas da origem de dados de Olá toomake.

## <a name="annotation-and-crowdsourcing"></a>Anotação e crowdsourcing
Todos têm um opinião. E é uma boa coisa.
Catálogo de dados reconhece que os utilizadores diferentes têm diferentes perspetivas em origens de dados empresariais e cada um destes perspetivas que pode ser útil. Considere Olá seguinte cenário:

* administrador de sistema Olá sabe o contrato de nível de serviço de Olá para servidores de Olá ou serviços essa origem de dados de Olá do anfitrião.
* administrador de bases de dados de Olá sabe cópia de segurança de Olá agendar para cada base de dados e Olá windows de processamento de ETL permitido.
* proprietário do sistema de Olá sabe o processo de Olá utilizadores toorequest acesso toohello origem de dados.
* steward de dados de Olá sabe como ativos de Olá e atributos na origem de dados de Olá mapeiam toohello modelo de dados de empresa.
* analista de Olá sabe como dados de Olá são utilizados no contexto de Olá dos processos de negócio Olá que suporta a ele.

Cada um destes perspetivas é útil e o catálogo de dados utiliza um toometadata de abordagem de crowdsourcing que permite que cada um toobe capturadas e utilizado tooprovide uma visão geral de origens de dados registados. Utilizar o portal do catálogo de dados de Olá, cada utilizador pode adicionar e editar as suas própria anotações, enquanto que está a ser anotações tooview capaz de fornecidos por outros utilizadores.

## <a name="different-types-of-annotations"></a>Diferentes tipos de anotações
Olá de suporta do catálogo de dados seguintes tipos de anotações:

| Anotação | Notas |
| --- | --- |
| Nome amigável |Nomes amigáveis podem ser fornecidos ao nível do elemento de dados de Olá, recursos de dados de Olá toomake compreendido mais facilmente. Nomes amigáveis são mais úteis quando o nome do objeto subjacente Olá toousers crípticas, abreviado ou caso contrário, não é significativo. |
| Descrição |Descrições podem ser fornecidas no recurso de dados de Olá e atributo / níveis de coluna. Descrições são anotações de texto abreviado de forma gratuita que descrevem a perspetiva do utilizador Olá no recurso de dados de Olá ou a sua utilização. |
| Etiquetas (etiquetas de utilizador) |As etiquetas podem ser fornecidas no recurso de dados de Olá e atributo / níveis de coluna. Etiquetas de utilizador são definidos pelo utilizador etiquetas que podem ser utilizados toocategorize recursos de dados ou atributos. |
| Etiquetas (etiquetas de glossário) |As etiquetas podem ser fornecidas no recurso de dados de Olá e atributo / níveis de coluna. Etiquetas de glossário são os termos do glossário definidas centralmente que podem ser utilizados toocategorize recursos de dados ou atributos utilizando uma taxonomia comercial comuns. Para obter mais informações consulte [como tooset segurança Olá glossário comercial para etiquetagem regida](data-catalog-how-to-business-glossary.md) |
| Especialistas |Especialistas podem ser fornecidas ao nível de recurso de dados de Olá. Especialistas identificam utilizadores ou grupos com perspetivas especialistas na dados Olá e podem servir como pontos de contacto para os utilizadores que detetar Olá origens de dados registadas e tem questões que não são respondidos pelo anotações existentes Olá. |
| Pedir acesso |Informações de pedidos de acesso podem ser fornecidas ao nível de recurso de dados de Olá. Esta informação é para os utilizadores que detetar uma origem de dados que não têm ainda tooaccess de permissões. Os utilizadores podem introduzir o endereço de correio eletrónico Olá de utilizador de Olá ou grupo que concede acesso, Olá URL do processo de Olá ferramenta que toogain necessidade dos utilizadores o acesso ou pode introduzir o próprio processo de Olá como texto. |
| Documentação |Documentação pode ser fornecida ao nível de recurso de dados de Olá. Documentação do recurso é informações de texto formatado, que podem incluir ligações e imagens e que pode fornecer as informações que não é transmitidas através de etiquetas e descrições. |

## <a name="annotating-multiple-assets"></a>Anotar vários recursos
Ao selecionar vários recursos de dados no portal do catálogo de dados de Olá, os utilizadores podem anotar todos os recursos selecionados numa única operação. Anotações irão aplicar ativos tooall selecionado, tornando mais fácil tooselect e fornecer uma descrição consistente e conjuntos de etiquetas e especialistas para recursos de dados relacionados.

> [!NOTE]
> As etiquetas e especialistas também podem ser fornecidas quando registar recursos de dados com dados de catálogo de dados de Olá ferramenta de registo de origem.
>
>

Quando selecionar várias tabelas e vistas, as colunas que todos os dados ativos têm em comum de selecionado será apresentado no portal do catálogo de dados de Olá. Isto permite que as etiquetas de tooprovide de utilizadores e descrições para todas as colunas com o mesmo nome de Olá para recursos de todos os selecionados.

## <a name="annotations-and-discovery"></a>Deteção e anotações
Tal como Olá metadados extraídos da origem de dados de Olá durante o registo é adicionado o índice de pesquisa do catálogo de dados toohello, fornecido pelo utilizador metadados também são indexados. Isto significa que não só fazem anotações tornar mais fácil para os utilizadores toounderstand Olá os dados que estes detetar, anotações também o tornam mais fácil para os utilizadores toodiscover Olá anotado recursos de dados ao pesquisar a utilizar os termos de Olá que fazer sentido toothem.

## <a name="summary"></a>Resumo
Registar uma origem de dados com o catálogo de dados faz com que os dados detetável por copiar os metadados estruturais e descritivo da origem de dados de Olá para Olá serviço de catálogo. Depois de uma origem de dados foi registada, os utilizadores podem fornecer anotações toomake mais fácil toodiscover e compreender a partir de dentro do portal do catálogo de dados Olá.

## <a name="see-also"></a>Consultar também
* [Introdução ao catálogo de dados do Azure](data-catalog-get-started.md) tutorial para obter detalhes passo a passo sobre como tooannotate origens de dados.
