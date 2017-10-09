
>[!NOTE]
>O Log Analytics era anteriormente conhecido como Operational Insights.
>
>

Olá seguintes limites aplicam-se os recursos de análise tooLog por subscrição:

| Recurso | Limite Predefinido | Comentários
| --- | --- | --- |
| Número de áreas de trabalho gratuitas por subscrição | 10 | Não pode aumentar este limite. |
| Número de áreas de trabalho pagas por subscrição | N/D | Estão limitados pelo número de Olá dos recursos dentro de um grupo de recursos e número de grupos de recursos por subscrição | 


Olá limites a seguir aplicam-se a área de trabalho de análise de registos de tooeach:

|  | Gratuito | Standard | Premium | Autónomo | OMS |
| --- | --- | --- | --- | --- | --- |
| Volume de dados recolhido por dia |500 MB<sup>1</sup> |Nenhuma |Nenhuma | Nenhuma | Nenhuma
| Período de retenção de dados |7 dias |1 mês |12 meses | 1 mês<sup>2</sup> | 1 mês <sup>2</sup>|

<sup>1</sup> quando os clientes atingem o respetivo limite de transferência de dados diária da 500 MB, análise de dados para e retoma início Olá da Olá dia seguinte. Os dias são baseados no fuso horário UTC.

<sup>2</sup> período de retenção de dados de Olá para Olá autónoma e OMS planos de preços pode ser aumentada too730 dias.

| Categoria | Limites | Comentários
| --- | --- | --- |
| API do Recoletor de Dados | O tamanho máximo para um post individual é 30 MB<br>O tamanho máximo para os valores de campos é 32 KB | Dividir volumes maiores em vários posts<br>Os campos com mais de 32 KB são truncados. |
| API de Pesquisa | 5000 registos devolvidos para dados não agregados<br>500 000 registos para dados agregados | Dados agregados são uma pesquisa que inclui Olá `measure` comando
 
