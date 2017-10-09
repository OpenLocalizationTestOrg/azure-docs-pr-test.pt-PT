---
title: "aaaUpgrading toohello API de REST do serviço do Azure Search versão 2016-09-01 | Microsoft Docs"
description: "Atualizar toohello API de REST do serviço do Azure Search versão 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Atualizar toohello API de REST do serviço do Azure Search versão 2016-09-01
Se estiver a utilizar a versão 2015-02-28 ou de pré-visualização 2015-02-28-de Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), este artigo irá ajudar a atualizar a sua aplicação toouse Olá seguinte geralmente disponível versão da API, 2016-09-01.

Versão 2016-09-01 das Olá REST API contém algumas alterações de versões anteriores. Estes são principalmente retrocompatível, para que alterar o seu código deverá ser preciso apenas esforço, consoante a versão que estava a utilizar antes. Consulte [passos tooupgrade](#UpgradeSteps) para obter instruções sobre como toochange código toouse Olá nova versão da sua API.

> [!NOTE]
> A instância de serviço de pesquisa do Azure suporta várias versões de REST API, incluindo Olá mais recente. Pode continuar toouse uma versão quando já não é hello mais recente, mas recomendamos que migrar a versão mais recente do código toouse Olá.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Novidades na versão 2016-09-01
Versão 2016-09-01 é versão geralmente disponível segundo Olá de Olá API de REST do serviço de pesquisa do Azure. Novas funcionalidades nesta versão de API incluem:

* [Analisadores personalizados](https://aka.ms/customanalyzers), que permitem tootake controlo sobre o processo de Olá de conversão de texto em tokens indexable e pesquisáveis.
* [Armazenamento de Blobs do Azure](search-howto-indexing-azure-blob-storage.md) e [Table Storage do Azure](search-howto-indexing-azure-tables.md) indexadores, que lhe permitem tooeasily importar dados de armazenamento do Azure na Azure Search num agendamento ou a pedido.
* [Campo mapeamentos](search-indexer-field-mappings.md), que permitem toocustomize como indexadores importar dados na Azure Search.
* Etags são, que permite que as definições de Olá tooupdate de índices, indexadores e origens de dados de forma segura de concorrência. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Passos tooupgrade
Se estiver a atualizar a partir da versão 2015-02-28, provavelmente, não terá toomake qualquer código tooyour alterações, que não seja o número de versão de Olá toochange. situações apenas Olá na qual poderá ser necessário toochange código são quando:

* O código de falha quando uma resposta de API, são devolvidas propriedades não reconhecidas. Por predefinição, a aplicação deve ignorar propriedades que não compreender.
* O código de persistir pedidos de API e tenta tooresend-los toohello nova versão de API. Por exemplo, isto pode acontecer se a aplicação persistir tokens de continuação devolvidos de Olá API de pesquisa (para obter mais informações, procure `@search.nextPageParameters` no Olá [referência da API de pesquisa](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Se qualquer uma destas situações aplicar tooyou, em seguida, poderá ter toochange código em conformidade. Caso contrário, não existem alterações devem ser necessárias a menos que queira toostart utilizando Olá [novas funcionalidades](#WhatsNew) da versão 2016-09-01.

Se estiver a atualizar a partir da versão 2015-02-28-pré-visualização, também se aplica a Olá acima, mas deve também estar ciente de que algumas funcionalidades de pré-visualização não estão disponíveis na versão 2016-09-01:

* Suporte do indexador de armazenamento de Blobs do Azure para blobs que contém matrizes JSON e de ficheiros CSV.
* Sinónimos
* Consultas de "Mais como"

Se o seu código utiliza estas funcionalidades, não será capaz de tooupgrade too2016-09-01, sem remover a sua utilização dos mesmos.

> [!IMPORTANT]
> . Lembre-se, pré-visualizar APIs foram concebidas para avaliação e de teste e não deve ser utilizadas em ambientes de produção.
> 
> 

## <a name="conclusion"></a>Conclusão
Se precisar de mais detalhes sobre como utilizar Olá API de REST do serviço de pesquisa do Azure, consulte Olá recentemente atualizado [referência da API](https://msdn.microsoft.com/library/azure/dn798935.aspx) no MSDN.

Apreciamos os seus comentários na Azure Search. Se tiver problemas, sentir tooask livre-nos para obter ajuda na Olá [fórum MSDN de pesquisa do Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou [StackOverflow](http://stackoverflow.com/). Se está a solicitar uma pergunta sobre a Azure procura StackOverflow, tootag se marca-a com `azure-search`.

Obrigado por utilizar a pesquisa do Azure!

