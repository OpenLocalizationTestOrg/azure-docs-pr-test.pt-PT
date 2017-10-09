---
title: aaaImport tooAnalytics os dados no Azure Application Insights | Microsoft Docs
description: "Importar dados estáticos toojoin com a telemetria da aplicação ou importe um tooquery de fluxo de dados separada Analytics."
services: application-insights
keywords: "Abra o esquema, a importação de dados"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Importar dados para análise

Importar dados de tabela para [análise](app-insights-analytics.md), qualquer toojoin com [Application Insights](app-insights-overview.md) telemetria da sua aplicação, ou pode analisá-lo como uma sequência separada. A análise é fluxos de elevado volume timestamped uma consulta poderosa idioma tooanalyzing adequada de telemetria.

Pode importar dados para análise ao utilizar o seu próprio esquema. Não tem esquemas de Application Insights de padrão de Olá do toouse como pedido ou rastreio.

Pode importar JSON ou DSV (delimitador de valores separados por - ponto e vírgula, vírgula ou por separador) ficheiros.

Existem três situações em que a importação tooAnalytics é útil:

* **Associe-se com a telemetria da aplicação.** Por exemplo, pode importar uma tabela que mapeia os URLs de títulos de página legível de toomore o Web site. Análise, pode criar um relatório de gráfico do dashboard que mostra Olá dez páginas mais populares no seu Web site. Agora, pode mostrar Olá títulos de página em vez de Olá URLs.
* **Correlacionar a telemetria da sua aplicação** com outras origens, como o tráfego de rede, os dados do servidor ou CDN ficheiros de registo.
* **Aplica o fluxo de dados separada do tooa de análise.** Application Insights Analytics é uma ferramenta poderosa, o que funciona bem com dispersa, timestamped fluxos - muito melhores do que o SQL Server em muitos casos. Se tiver essa um fluxo de alguns outra origem, pode analisá-lo com a análise.

Enviar dados de origem de dados de tooyour é fácil. 

1. (Uma vez) Defina o esquema de Olá dos seus dados numa "origem de dados'.
2. (Periodicamente) Carregar o armazenamento de tooAzure de dados e chame Olá REST API toonotify-nos que novos dados está a aguardar ingestão. Dentro de alguns minutos, os dados de Olá estão disponíveis para consulta na análise.

Olá frequência de carregamento de Olá é definida por si e a rapidez pretende que o seu toobe dados disponível para consultas. É mais eficientes dados de tooupload segmentos maior, mas não superior a 1GB.

> [!NOTE]
> *Obteve muitos tooanalyze de origens de dados?* [*Considere a utilização de* logstash *tooship os dados no Application Insights.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Antes de começar

É necessário:

1. Um recurso do Application Insights no Microsoft Azure.

 * Se quiser tooanalyze os dados separadamente a partir de qualquer outra telemetria [criar um novo recurso do Application Insights](app-insights-create-new-resource.md).
 * Se estiver a adesão ou comparar os seus dados com a telemetria a partir de uma aplicação que já está definida com o Application Insights, em seguida, pode utilizar recursos Olá para essa aplicação.
 * Recurso de toothat de acesso contribuinte ou proprietário.
 
2. Armazenamento do Azure. Carregar tooAzure armazenamento e análise obtém os dados a partir daí. 

 * Recomendamos que crie uma conta de armazenamento dedicado para os blobs. Se os blobs são partilhados com outros processos, demora mais longo para o nosso tooread processos os blobs.


## <a name="define-your-schema"></a>Definir o esquema

Antes de importar dados, tem de definir um *origem de dados,* que especifica o esquema de Olá dos seus dados.
Pode ter segurança too50 origens de dados num único recurso do Application Insights

1. Inicie o Assistente de origem de dados de Olá. Utilize o botão "Adicionar nova origem de dados". Em alternativa - clique no botão de definições no canto superior direito e selecione "Origens de dados" no menu pendente.

    ![Adicionar nova origem de dados](./media/app-insights-analytics-import/add-new-data-source.png)

    Forneça um nome para a nova origem de dados.

2. Defina o formato de ficheiros de Olá que irá carregar.

    Pode definir o formato de Olá manualmente ou carregar um ficheiro de exemplo.

    Se os dados de Olá estão num formato CSV, Olá primeira linha exemplo Olá pode ser cabeçalhos de coluna. Pode alterar os nomes de campos de Olá no passo seguinte Olá.

    exemplo de Olá deve incluir pelo menos 10 linhas ou registos de dados.

    Os nomes de coluna ou o campo devem ter nomes alfanuméricos (sem espaços ou pontuação).

    ![Carregar um ficheiro de exemplo](./media/app-insights-analytics-import/sample-data-file.png)


3. Esquema de Olá de revisão que Olá assistente foi obtido. Se este inferir tipos de Olá a partir de uma amostra, poderá ter de tipos de Olá inferido tooadjust de colunas de Olá.

    ![Esquema de Olá inferido de revisão](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (Opcional.) Carregue uma definição de esquema. Consulte o formato de Olá abaixo.

 * Selecione um carimbo. Todos os dados na análise tem de ter um campo de carimbo. Tem de ter tipo `datetime`, mas não tem toobe com o nome 'timestamp'. Se os seus dados têm uma coluna que contém uma data e hora no formato ISO, escolha tal como coluna de carimbo de Olá. Caso contrário, escolha "como dados chegou" e o processo de importação de Olá irá adicionar um campo de carimbo.

5. Crie origem de dados de Olá.

### <a name="schema-definition-file-format"></a>Formato de ficheiro de definição de esquema

Em vez de editar o esquema de Olá na IU, pode carregar a definição de esquema de Olá de um ficheiro. formato de definição de esquema Olá é o seguinte: 

Formato delimitado 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

Formato JSON 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Cada coluna é identificada por nome e tipo de localização de Olá. 

* Localização – para o formato de ficheiro delimitado-lo é posição Olá do valor de Olá mapeado. Para o formato JSON, é Olá jpath da chave de Olá mapeado.
* Nome – Olá apresentado o nome da coluna de Olá.
* Tipo – Olá dados dessa coluna.
 
No caso de dados de exemplo foi utilizados e é delimitado formato de ficheiro, definição de esquema Olá tem de mapear todas as colunas e adicionar novas colunas no fim de Olá. 

JSON permite um mapeamento parcial de dados de Olá, portanto hello definição de esquema no formato JSON não tem toomap cada chave que não foi encontrado nos dados de exemplo. -Também é possível mapear colunas que não façam parte de dados de exemplo de Olá. 

## <a name="import-data"></a>Importar dados

dados tooimport, carregue-o armazenamento de tooAzure, criar uma chave de acesso para o mesmo e, em seguida, efetuar uma chamada de REST API.

![Adicionar nova origem de dados](./media/app-insights-analytics-import/analytics-upload-process.png)

Pode efetuar Olá seguindo o processo manualmente ou configurar um toodo automatizado do sistema-lo em intervalos regulares. Terá de toofollow estes passos para cada bloco de dados pretende tooimport.

1. Carregar dados de Olá demasiado[blob storage do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * Os BLOBs podem ser qualquer dimensão se too1GB descomprimidos. Os blobs grande de centenas de MB são ideais de uma perspetiva de desempenho.
 * Pode comprimi-los com o tempo de carregamento de tooimprove Gzip e latência para Olá dados toobe disponível para consulta. Olá utilize `.gz` extensão de nome de ficheiro.
 * É melhor toouse uma conta de armazenamento separada para esta finalidade, chamadas de tooavoid provenientes de diferentes serviços abrandamento desempenho.
 * Quando o envio de dados de alta frequência, cada alguns segundos, é recomendado toouse mais do que uma conta de armazenamento, por motivos de desempenho.

 
2. [Criar uma chave de assinatura de acesso partilhado de blob Olá](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). chave de Olá deve ter um período de expiração de um dia e fornecer acesso de leitura.
3. Efetuar uma toonotify de chamada REST Application Insights que está a aguardar a dados.

 * Ponto final:`https://dc.services.visualstudio.com/v2/track`
 * Método HTTP: POST
 * Payload:

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

marcadores de posição de Olá são:

* `Blob URI with Shared Access Key`: Pode obter esta do procedimento de Olá para criar uma chave. É blob toohello específico.
* `Schema ID`: Olá ID do esquema gerado para o esquema definido. dados Olá este blob devem estar em conformidade toohello esquema.
* `DateTime`: tempo de Olá no qual Olá pedido ser submetido, UTC. Podemos aceitar estes formatos: ISO8601 (como "2016-01-01 13:45:01"); Rfc822 ("Qua, 14 16 de Dec 14:57:01 + 0000"); RFC850 ("Quarta-feira, 14-Dec-16 UTC de 57:14:00"); RFC1123 ("Qua, 14 de Dec de 2016 57:14:00 + 0000").
* `Instrumentation key`de recurso do Application Insights.

dados de Olá estão disponíveis no Analytics após alguns minutos.

## <a name="error-responses"></a>Respostas de erro

* **pedido incorreto 400**: indica que o payload de pedido Olá é inválido. Verifique:
 * Chave de instrumentação correto.
 * Valor de hora válido. Deve ser tempo Olá agora em UTC.
 * Está em conformidade com o JSON do evento de Olá toohello esquema.
* **403 Proibido**: blob Olá que enviou não está acessível. Certifique-se de que essa chave de acesso partilhado Olá é válido e não expirou.
* **404 não encontrado**:
 * blob Olá não existe.
 * sourceId Olá está errada.

Estão disponíveis na mensagem de erro de resposta de Olá informações mais detalhadas.


## <a name="sample-code"></a>Código de exemplo

Este código utiliza Olá [newtonsoft](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) pacote NuGet.

### <a name="classes"></a>Classes

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Ingerir dados

Utilize este código para cada blob. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Passos seguintes

* [Apresentação de Olá idioma de consulta de análise de registos](app-insights-analytics-tour.md)
* [Utilize *Logstash* toosend dados tooApplication Insights](https://github.com/Microsoft/logstash-output-application-insights)
