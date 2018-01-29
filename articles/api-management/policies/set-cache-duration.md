---
title: "Exemplo de política de gestão de Azure API - definir a duração da cache de resposta | Microsoft Docs"
description: "Exemplo de política de gestão de Azure API - demonstra como definir a duração da cache de resposta utilizando o valor de maxAge no cabeçalho de Cache-Control enviado pelo back-end..."
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 8471b51999159c8f6233abbbce998b122163efd8
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/04/2017
---
# <a name="set-response-cache-duration"></a>Definir a duração da cache de resposta

Este artigo mostra um exemplo de política de gestão de API do Azure que demonstra como definir a duração da cache de resposta utilizando o valor de maxAge no cabeçalho de Cache-Control enviado pelo back-end. Para definir ou editar um código de política, siga os passos descritos no [conjunto ou editar uma política](../set-edit-policies.md). Para ver outros exemplos, consulte [amostras de política](../policy-samples.md).

## <a name="policy"></a>Política

Cole o código para o **entrada** bloco.

[!code-xml[Main](../../../api-management-policy-samples/Snippets/Set cache duration using response cache control header.policy.xml)]

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre as políticas de APIM:

+ [Políticas de transformação](../api-management-transformation-policies.md)
+ [Exemplos de política](../policy-samples.md)

