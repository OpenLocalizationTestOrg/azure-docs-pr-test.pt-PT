---
title: "aaaUse dados e de pesquisa as tabelas de referência no Stream Analytics | Microsoft Docs"
description: "Utilizar dados de referência numa consulta do Stream Analytics"
keywords: "tabela de referência, os dados de referência"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Utilizar as tabelas de dados ou de pesquisa de referência num fluxo de entrada do Stream Analytics
Dados de referência (também conhecido como uma tabela de pesquisa) são um conjunto de dados finito que é estático ou abrandamento alterar natureza utilizar tooperform uma pesquisa ou toocorrelate com o fluxo de dados. utilização de toomake de dados de referência na sua tarefa do Azure Stream Analytics, normalmente, utilizará um [associação de dados de referência](https://msdn.microsoft.com/library/azure/dn949258.aspx) na sua consulta. Do Stream Analytics utiliza o Blob storage do Azure como camada de armazenamento Olá para dados de referência e com a referência do Azure Data Factory com os dados podem ser transformados e/ou copiados tooAzure armazenamento de BLOBs, para utilização como dados de referência de [qualquer número de baseado na nuvem e arquivos de dados no local](../data-factory/data-factory-data-movement-activities.md). Dados de referência são modelados como uma sequência de blobs (definido na configuração de entrada Olá) por ordem de Olá data/hora especificada no nome do blob Olá ascendente. - **Apenas** suporta a adição de toohello fim da sequência de Olá através da utilização de uma data/hora **maior** que Olá um especificada pelo blob último Olá na sequência de Olá.

Do Stream Analytics tem uma **limite de 100 MB por blob** mas tarefas podem processar vários blobs de referência utilizando Olá **padrão do caminho** propriedade.


## <a name="configuring-reference-data"></a>Configurar dados de referência
tooconfigure os dados de referência, terá primeiro toocreate uma entrada que é do tipo **dados de referência**. tabela de Olá abaixo explica cada propriedade que será necessário tooprovide ao criar a entrada de dados de referência de Olá com a respetiva descrição:


<table>
<tbody>
<tr>
<td>Nome da propriedade</td>
<td>Descrição</td>
</tr>
<tr>
<td>Alias de entrada</td>
<td>Um nome amigável que será utilizado no Olá tarefa consulta tooreference esta entrada.</td>
</tr>
<tr>
<td>Conta de Armazenamento</td>
<td>nome de Olá Olá da conta de armazenamento onde estão localizados os blobs. Se estiver a ser Olá mesma subscrição que a tarefa do Stream Analytics, pode selecioná-lo Olá lista pendente.</td>
</tr>
<tr>
<td>Chave de conta de armazenamento</td>
<td>chave secreta Olá associada à conta de armazenamento Olá. Este obtém preenchido automaticamente se a conta de armazenamento Olá está em Olá mesma subscrição que a tarefa de Stream Analytics.</td>
</tr>
<tr>
<td>Contentor de armazenamento</td>
<td>Contentores fornecem um agrupamento lógico blobs armazenados no Olá serviço Blob do Microsoft Azure. Ao carregar um blob de toohello serviço Blob, tem de especificar um contentor para esse blob.</td>
</tr>
<tr>
<td>Padrão de caminho</td>
<td>caminho de Olá utilizado toolocate os blobs no contentor especificado Olá. No caminho de Olá, pode optar por toospecify uma ou mais instâncias de Olá 2 variáveis os seguintes:<BR>{date}, {time}<BR>Exemplo 1: products/{date}/{time}/product-list.csv<BR>Exemplo 2: products/{date}/product-list.csv
</tr>
<tr>
<td>Formato de data [opcional]</td>
<td>Se tiver utilizado {date} dentro Olá padrão do caminho que especificou, pode selecionar o formato de data Olá em que os blobs são organizados de pendente Olá dos formatos suportados.<BR>Exemplo: DD/MM/DD, MM/DD/AAAA, etc.</td>
</tr>
<tr>
<td>Formato de hora [opcional]</td>
<td>Em seguida, se tiver utilizado {time} dentro Olá padrão do caminho que especificou, pode selecionar um formato de hora Olá no qual estão organizados os blobs dos pendente Olá dos formatos suportados.<BR>Exemplo: HH, HH/mm ou dd HH</td>
</tr>
<tr>
<td>Formato de serialização de eventos</td>
<td>se que as suas consultas funcionam de forma Olá esperado, o Stream Analytics toomake tem tooknow qual o formato de serialização está a utilizar para fluxos de dados recebidos. Para dados de referência, os formatos de Olá suportado são CSV e JSON.</td>
</tr>
<tr>
<td>Encoding</td>
<td>UTF-8 é Olá apenas formato de codificação suportado neste momento</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Gerar dados de referência com base numa agenda
Se os dados de referência for um conjunto de dados de alteração lentamente, suporte para atualizar os dados de referência está ativado, especificando um padrão de caminho na configuração de entrada de Olá utilizando Olá {date} e tokens de substituição de {time}. Do Stream Analytics escolherá definições de dados de referência de Olá atualizada com base num padrão caminho. Por exemplo, um padrão de `sample/{date}/{time}/products.csv` com um formato de data do **"Aaaa-MM-DD"** e um formato de hora do **"Dd HH"** dá instruções ao Stream Analytics toopick segurança blob Olá atualizado `sample/2015-04-16/17-30/products.csv` em 5:30 PM Abril 16th, 2015 fuso horário UTC.

> [!NOTE]
> Atualmente tarefas do Stream Analytics procure atualização de blob Olá apenas quando o tempo de máquina Olá avança tempo toohello codificado no nome do blob Olá. Por exemplo, a tarefa de Olá irá procurar `sample/2015-04-16/17-30/products.csv` logo que possível, mas não anteriormente que 5:30 PM 16th de Abril de 2015 UTC tempo zona. Este irá *nunca* procure um blob com um período de tempo codificado anteriormente que Olá um último que é detetado.
> 
> Por exemplo, Assim que a tarefa de Olá localiza blob Olá `sample/2015-04-16/17-30/products.csv` ignorará quaisquer ficheiros com uma data codificado anteriores ao 5:30 da Tarde 16th de Abril de 2015, pelo que, se um enlace tardio chegar `sample/2015-04-16/17-25/products.csv` blob é criado no Olá mesma tarefa do contentor Olá não utilizá-lo.
> 
> Da mesma forma se `sample/2015-04-16/17-30/products.csv` apenas é produzido nas 22:03:00 16th de Abril de 2015, mas não existem BLOBs com uma data anterior está presente no contentor de Olá, tarefa Olá irá utilizar este ficheiro começando as 22:03:00 16th de Abril de 2015 e utilizar dados de referência anterior Olá até.
> 
> Toothis uma exceção é quando a tarefa de Olá necessita de dados de processo toore para trás no tempo ou quando a tarefa de Olá é iniciado pela primeira vez. No início tarefa de Olá tempo está à procura de blob mais recente Olá produzido antes de iniciar a tarefa de Olá período de tempo especificado. Isto é feito tooensure que não existe um **vazios** referenciar o conjunto de dados quando inicia a tarefa de Olá. Se não for encontrado, a tarefa de Olá apresenta Olá seguir diagnóstico: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[O Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) pode ser utilizado tooorchestrate Olá tarefa de criação de definições de dados de referência do Stream Analytics tooupdate de blobs de Olá atualizado. Data Factory é um serviço de integração de dados baseado na nuvem que orquestra e automatiza o movimento de Olá e a transformação de dados. Fábrica de dados suporta [ligar tooa grande número de baseada na nuvem e arquivos de dados no local](../data-factory/data-factory-data-movement-activities.md) e mover dados facilmente regularmente que especificar. Para obter mais informações e orientações passo a passo sobre como tooset uma fábrica de dados de cópia de segurança pipeline de dados de referência toogenerate para Stream Analytics que é atualizada com base num agendamento predefinido, veja isto [GitHub exemplo](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Sugestões sobre como atualizar os dados de referência
1. Substituir blobs de dados de referência não irá causar Stream Analytics tooreload Olá blob e, em alguns casos pode causar Olá tarefa toofail. Olá recomendado dados de referência de toochange de forma é tooadd um novo blob utilizando Olá mesmo padrão de contentor e o caminho definido na entrada de tarefa Olá e utilizam uma data/hora **maior** que Olá um especificada pelo blob último Olá na sequência de Olá.
2. Os blobs de dados de referência são **não** ordenada por hora do blob Olá da "Última modificação", mas apenas por hora de Olá e a data especificada no nome do blob Olá utilizando Olá {date} e substituições {time}.
3. Em ocasiões, alguns, uma tarefa tem de voltar atrás no tempo, por conseguinte blobs de dados de referência não tem de ser alterados ou eliminados.

## <a name="get-help"></a>Obter ajuda
Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passos seguintes
Tiver sido introduzida tooStream Analytics, um serviço gerido para transmissão em fluxo a análise dos dados de Olá Internet das coisas. toolearn mais informações sobre este serviço, consulte:

* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
