---
title: "Análise de Data Lake Store saída de aaaStream | Microsoft Docs"
description: "Configuração de autenticação e autorização de um Azure Data Lake Store numa tarefa do Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>Saída de Stream Analytics Data Lake Store
Tarefas do Stream Analytics suportam vários métodos de saída, a ser um um [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). O Azure Data Lake Store é um repositório de hiper escala a nível da empresa para cargas de trabalho de análise de macrodados. Arquivo data Lake permite-lhe toostore dados de qualquer tamanho, tipo e velocidade de ingestão para análises exploratórias e operacionais.

## <a name="authorize-a-data-lake-store-account"></a>Autorizar a conta do Data Lake Store
1. Quando a Data Lake Store é selecionada como uma saída no Olá portal do Azure, terá de aceder a utilização de tooauthorize do Data Lake Store existente ou toorequest toohello Data Lake Store através do Portal clássico do Olá.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Se já tiver acesso tooData Lake Store, clique em "Autorizar agora" e por um breve período de tempo a página irá aparecer que indica "Redirecting tooauthorization". página Olá automaticamente será fechada e será apresentada com a página Olá que permitiria tooconfigure Olá Data Lake Store saída.

Se não tiver assinado cópias de segurança para o Data Lake Store, pode seguir Olá "Inscrever-me agora" ligação tooinitiate Olá pedido ou, siga Olá [obter instruções de introdução](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Configurar propriedades de saída do Data Lake Store Olá
Assim que tiver a conta de Data Lake Store Olá autenticada, pode configurar propriedades de Olá para a saída do Data Lake Store. tabela de Olá abaixo é Olá obter lista de nomes de propriedade e os respetivos tooconfigure de descrição de saída do Data Lake Store.

<table>
<tbody>
<tr>
<td><B>NOME DA PROPRIEDADE</B></td>
<td><B>DESCRIÇÃO</B></td>
</tr>
<tr>
<td>Alias de saída</td>
<td>Este é um nome amigável utilizado em consultas toodirect Olá consulta saída toothis Data Lake Store.</td>
</tr>
<tr>
<td>Conta do Data Lake Store</td>
<td>nome de Olá Olá da conta de armazenamento onde está a enviar o resultado. Será apresentada uma lista de contas do Data Lake Store Olá a sessão de utilizador tem acesso ao.</td>
</tr>
<tr>
<td>Caminho do prefixo padrão [<I>opcional</I>]</td>
<td>Olá ficheiro caminho utilizado toowrite os ficheiros dentro do Olá especificado conta do Data Lake Store. <BR>{date}, {time}<BR>Exemplo 1: pasta1/logs / {date} / {time}<BR>Exemplo 2: pasta1/logs / {date}</td>
</tr>
<tr>
<td>Formato de data [<I>opcional</I>]</td>
<td>Se o token de data de Olá é utilizado no caminho de prefixo Olá, pode selecionar o formato de data Olá na qual os ficheiros estão organizados. Exemplo: DD/MM/DD</td>
</tr>
<tr>
<td>Formato de hora [<I>opcional</I>]</td>
<td>Se o token de tempo de Olá é utilizado no caminho de prefixo Olá, especifique o formato de hora Olá na qual os ficheiros estão organizados. Valor de Olá só suportada está atualmente HH.</td>
</tr>
<tr>
<td>Formato de serialização de eventos</td>
<td>Formato de serialização para dados de saída. JSON, CSV e Avro são suportados.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Se o formato CSV ou JSON, uma codificação tem de ser especificada. UTF-8 é Olá apenas formato de codificação suportado neste momento.</td>
</tr>
<tr>
<td>Delimitador</td>
<td>Só é aplicável a serialização de CSV. Stream Analytics suporta um número de delimitadores comuns para serializar os dados CSV. Os valores suportados são vírgula, ponto e vírgula, espaço, separador e barra vertical.</td>
</tr>
<tr>
<td>formato</td>
<td>Só é aplicável a serialização do JSON. Separadas por linhas Especifica que Olá saída será formatada, fazendo com que cada objeto JSON separado por uma nova linha. A matriz Especifica que Olá saída será formatada como uma matriz de objetos JSON.</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>Renovar autorização do arquivo Data Lake
Atualmente, não há uma limitação em que o token de autenticação de Olá tem toobe atualizado manualmente todos os 90 dias para todas as tarefas com a saída do Data Lake Store. Também terá de toore-autenticar a sua conta do Data Lake Store, se tiver alterado a palavra-passe, uma vez que a tarefa foi criada ou pela última vez autenticada. Um sintoma de que este problema é um erro nos registos de operação de Olá com a indicação de necessidade de nova autorização e nenhum resultado da tarefa.

tooresolve este problema, parar a tarefa em execução e aceda a saída tooyour Data Lake Store. Clique em ligação de "Autorização de renovação" Olá e por um breve período de tempo a página irá aparecer que indica "Redirecting tooauthorization …". página Olá irá fechar automaticamente e se tiver êxito, irá indicar "Autorização tem foi renovada com êxito". Que, em seguida, precisa tooclick "Guardar" em Olá parte inferior da página Olá e pode avançar ao reiniciar a tarefa de Olá perda de dados de tooavoid de hora da última paragem.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

