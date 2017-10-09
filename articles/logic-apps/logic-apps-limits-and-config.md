---
title: "aaaLogic aplicação limites e configuração | Microsoft Docs"
description: "Descrição geral de Olá limites de serviço e valores de configuração disponíveis para aplicações lógicas."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 739509afe5c9a7b7e946ba3571951264127e5297
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-app-limits-and-configuration"></a>Limites e configuração da Aplicação Lógica

Segue-se informações sobre limites de Olá atual e detalhes de configuração para o Azure Logic Apps.

## <a name="limits"></a>Limites

### <a name="http-request-limits"></a>Limites de pedidos HTTP

Seguem-se os limites de uma única chamada de pedido de e/ou o conector HTTP.

#### <a name="timeout"></a>Tempo limite

|Nome|Limite|Notas|
|----|----|----|
|Tempo limite do pedido|Por 120 segundos|Um [padrão assíncrono](../logic-apps/logic-apps-create-api-app.md) ou [até ciclo](logic-apps-loops-and-scopes.md) pode compensar conforme necessário|

#### <a name="message-size"></a>Tamanho da mensagem

|Nome|Limite|Notas|
|----|----|----|
|Tamanho da mensagem|100 MB|Algumas APIs e conectores podem não suportar 100 MB |
|Limite de avaliação da expressão|131,072 carateres|`@concat()`, `@base64()`, `string` não pode ser superior a este limite|

#### <a name="retry-policy"></a>Política de repetição

|Nome|Limite|Notas|
|----|----|----|
|Tentativas de repetição|10| Predefinição é 4. Pode configurar com Olá [Repita o parâmetro de política](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|Intervalo máximo de repetição|1 hora|Pode configurar com Olá [Repita o parâmetro de política](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|
|Mín. intervalo de repetição|seg 5|Pode configurar com Olá [Repita o parâmetro de política](https://msdn.microsoft.com/en-us/library/azure/mt643939.aspx)|

### <a name="run-duration-and-retention"></a>Duração de execução e retenção

Seguem-se Olá os limites de uma aplicação lógica única de executar.

|Nome|Limite|Notas|
|----|----|----|
|Duração de execução|90 dias||
|Retenção de armazenamento|90 dias|A partir de Olá hora de início de execução|
|Intervalo de periodicidade mín.|seg 1|| 15 segundos para aplicações lógicas com o plano do App Service
|Intervalo de periodicidade máximo|dias de 500||

Se esperar tooexceed executar duration ou armazenamento limites de retenção no fluxo de processamento normal, [contacte-nos](mailto://logicappsemail@microsoft.com) , de modo a que o possamos ajudar com as suas necessidades.


### <a name="looping-and-debatching-limits"></a>Criar ciclos e debatching limites

Seguem-se os limites de uma aplicação lógica única de executar.

|Nome|Limite|Notas|
|----|----|----|
|ForEach itens|100,000|Pode utilizar Olá [ação de consulta](../connectors/connectors-native-query.md) toofilter matrizes maior conforme necessário|
|Até iterações|5,000||
|Itens de SplitOn|100,000||
|ForEach paralelismo|50| Predefinição é 20. Pode definir foreach sequenciais tooa adicionando `"operationOptions": "Sequential"` toohello `foreach` ação ou nível específico de paralelismo a utilizar`runtimeConfiguration`|


### <a name="throughput-limits"></a>Limites de débito

Seguem-se os limites de uma instância da aplicação lógica única. 

|Nome|Limite|Notas|
|----|----|----|
|Execuções de ações por 5 minutos |100,000|Pode distribuir a carga de trabalho por várias aplicações conforme necessário|
|Chamadas de saída em simultâneo de ações |~2,500|Reduzir o número de pedidos simultâneos ou reduzir a duração de Olá conforme necessário|
|Tempo de execução endpoint recebidas de chamadas em simultâneo |~1,000|Reduzir o número de pedidos simultâneos ou reduzir a duração de Olá conforme necessário|
|Ponto final de tempo de execução de leitura de chamadas por 5 minutos |60,000|Pode distribuir a carga de trabalho por várias aplicações conforme necessário|
|Ponto final de tempo de execução invocar chamadas por 5 minutos |45,000|Pode distribuir a carga de trabalho por várias aplicações conforme necessário|

Se estiver tooexceed este limite em processamento normal ou de teste de carga de toorun desejar que pode exceder este limite para um período de tempo, [contacte-nos](mailto://logicappsemail@microsoft.com) , de modo a que o possamos ajudar com as suas necessidades.

### <a name="definition-limits"></a>Limites de definição

Seguem-se os limites de uma definição de aplicação lógica única.

|Nome|Limite|Notas|
|----|----|----|
|Ações por fluxo de trabalho|500|Pode adicionar fluxos de trabalho aninhados tooextend este limite conforme necessário|
|Profundidade de aninhamento de ação de permissão|8|Pode adicionar fluxos de trabalho aninhados tooextend este limite conforme necessário|
|Fluxos de trabalho por região por subscrição|1000||
|Acionadores por fluxo de trabalho|10||
|Limite de casos de âmbito do comutador|25||
|Número de variáveis por fluxo de trabalho|250||
|Carateres máx. por expressão|8,192||
|Máx. `trackedProperties` tamanho em carateres|16,000|
|`action`/`trigger`limite de nome|80||
|`description`limite de comprimento|256||
|`parameters`limite|50||
|`outputs`limite|10||

### <a name="integration-account-limits"></a>Limites de conta de integração

Seguem-se os limites para artefactos adicionadas toointegration conta

|Nome|Limite|Notas|
|----|----|----|
|Esquema|8 MB|Pode utilizar [URI de blob](logic-apps-enterprise-integration-schemas.md) tooupload ficheiros com mais de 2 MB |
|Mapa (ficheiro XSLT)|2 MB| |
|Ponto final de tempo de execução de leitura de chamadas por 5 minutos |60,000|Pode distribuir a carga de trabalho em várias contas conforme necessário|
|Ponto final de tempo de execução invocar chamadas por 5 minutos |45,000|Pode distribuir a carga de trabalho em várias contas conforme necessário|
|Ponto final de tempo de execução controlo chamadas por 5 minutos |45,000|Pode distribuir a carga de trabalho em várias contas conforme necessário|
|Ponto final de tempo de execução de chamadas em simultâneo de bloqueio |~1,000|Reduzir o número de pedidos simultâneos ou reduzir a duração de Olá conforme necessário|

### <a name="b2b-protocols-as2-x12-edifact-message-size"></a>Tamanho da mensagem de protocolos de B2B (AS2, X12, EDIFACT)

Seguem-se limites de Olá protocolos B2B

|Nome|Limite|Notas|
|----|----|----|
|AS2|50 MB|Toodecode aplicável e codificar|
|X12|50 MB|Toodecode aplicável e codificar|
|EDIFACT|50 MB|Toodecode aplicável e codificar|

## <a name="configuration"></a>Configuração

### <a name="ip-address"></a>Endereço IP

#### <a name="logic-app-service"></a>Serviço de aplicações lógicas

As chamadas efetuadas diretamente a partir de uma aplicação lógica (ou seja, através de [HTTP](../connectors/connectors-native-http.md) ou [HTTP + Swagger](../connectors/connectors-native-http-swagger.md)) ou outros pedidos HTTP provenientes Olá endereço IP especificado no Olá lista a seguir:

|Região de aplicação lógica|IP de saída|
|-----|----|
|Leste da Austrália|13.75.153.66, 104.210.89.222, 104.210.89.244, 13.75.149.4, 104.210.91.55, 104.210.90.241|
|Sudeste da Austrália|13.73.115.153, 40.115.78.70, 40.115.78.237, 13.73.114.207, 13.77.3.139, 13.70.159.205|
|Sul do Brasil|191.235.86.199, 191.235.95.229, 191.235.94.220, 191.235.82.221, 191.235.91.7, 191.234.182.26|
|Canadá Central|52.233.29.92, 52.228.39.241, 52.228.39.244|
|Leste do Canadá|52.232.128.155, 52.229.120.45, 52.229.126.25|
|Índia Central|52.172.157.194, 52.172.184.192, 52.172.191.194, 52.172.154.168, 52.172.186.159, 52.172.185.79|
|EUA Central|13.67.236.76, 40.77.111.254, 40.77.31.87, 13.67.236.125, 104.208.25.27, 40.122.170.198|
|Ásia Oriental|168.63.200.173, 13.75.89.159, 23.97.68.172, 13.75.94.173, 40.83.127.19, 52.175.33.254|
|EUA Leste|137.135.106.54, 40.117.99.79, 40.117.100.228, 13.92.98.111, 40.121.91.41, 40.114.82.191|
|EUA Leste 2|40.84.25.234, 40.79.44.7, 40.84.59.136, 40.84.30.147, 104.208.155.200, 104.208.158.174|
|Leste do Japão|13.71.146.140, 13.78.84.187, 13.78.62.130, 13.71.158.3, 13.73.4.207, 13.71.158.120|
|Oeste do Japão|40.74.140.173, 40.74.81.13, 40.74.85.215, 40.74.140.4, 104.214.137.243, 138.91.26.45|
|EUA Centro-Norte|168.62.249.81, 157.56.12.202, 65.52.211.164, 168.62.248.37, 157.55.210.61, 157.55.212.238|
|Europa do Norte|13.79.173.49, 52.169.218.253, 52.169.220.174, 40.113.12.95, 52.178.165.215, 52.178.166.21|
|EUA Centro-Sul|13.65.98.39, 13.84.41.46, 13.84.43.45, 104.210.144.48, 13.65.82.17, 13.66.52.232|
|Sudeste Asiático|52.163.93.214, 52.187.65.81, 52.187.65.155, 13.76.133.155, 52.163.228.93, 52.163.230.166|
|Sul da Índia|52.172.9.47, 52.172.49.43, 52.172.51.140, 52.172.50.24, 52.172.55.231, 52.172.52.0|
|Europa Ocidental|13.95.155.53, 52.174.54.218, 52.174.49.6, 40.68.222.65, 40.68.209.23, 13.95.147.65|
|Índia Ocidental|104.211.164.112, 104.211.165.81, 104.211.164.25, 104.211.164.80, 104.211.162.205, 104.211.164.136|
|EUA Oeste|52.160.90.237, 138.91.188.137, 13.91.252.184, 52.160.92.112, 40.118.244.241, 40.118.241.243|
|Reino Unido Sul|51.140.74.14, 51.140.73.85, 51.140.78.44|
|Reino Unido Oeste|51.141.54.185, 51.141.45.238, 51.141.47.136|

#### <a name="connectors"></a>Conectores

As chamadas efetuadas a partir de um [conector](../connectors/apis-list.md) provenientes Olá endereço IP especificado no Olá lista a seguir:

|Região de aplicação lógica|IP de saída|
|-----|----|
|Leste da Austrália|40.126.251.213|
|Sudeste da Austrália|40.127.80.34|
|Sul do Brasil|191.232.38.129|
|Canadá Central|52.233.31.197, 52.228.42.205, 52.228.33.76, 52.228.34.13|
|Leste do Canadá|52.229.123.98, 52.229.120.178, 52.229.126.202, 52.229.120.52|
|Índia Central|104.211.98.164|
|EUA Central|40.122.49.51|
|Ásia Oriental|23.99.116.181|
|EUA Leste|191.237.41.52|
|EUA Leste 2|104.208.233.100|
|Leste do Japão|40.115.186.96|
|Oeste do Japão|40.74.130.77|
|EUA Centro-Norte|65.52.218.230|
|Europa do Norte|104.45.93.9|
|EUA Centro-Sul|104.214.70.191|
|Sudeste Asiático|13.76.231.68|
|Sul da Índia|104.211.227.225|
|Europa Ocidental|40.115.50.13|
|Índia Ocidental|104.211.161.203|
|EUA Oeste|104.40.51.248|
|Reino Unido Sul|51.140.80.51|
|Reino Unido Oeste|51.141.47.105|


## <a name="next-steps"></a>Passos Seguintes  

- tooget à Logic Apps, siga Olá [criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md) tutorial.  
- [Ver exemplos e cenários comuns](../logic-apps/logic-apps-examples-and-scenarios.md)
- [Pode automatizar os processos de negócios com Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) 
- [Saiba como tooIntegrate seus sistemas com Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)
