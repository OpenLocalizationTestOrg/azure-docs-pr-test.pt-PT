Data factory é um serviço de multi-inquilino tem Olá seguintes limites de predefinição na toomake local se subscrições de cliente estão protegidas de cargas de trabalho entre si. Muitos dos limites de Olá podem ser facilmente gerados para a sua subscrição de cópia de segurança limite máximo de toohello contactando o suporte.

| **Recurso** | **Limite Predefinido** | **Limite Máximo** |
| --- | --- | --- |
| fábricas de dados numa subscrição do Azure |50 |[Contactar o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| pipelines dentro de uma fábrica de dados |2500 |[Contactar o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| conjuntos de dados dentro de uma fábrica de dados |5000 |[Contactar o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| setores em simultâneo por conjunto de dados |10 |10 |
| bytes por objeto para objetos de pipeline <sup>1</sup> |200 KB |200 KB |
| bytes por objeto para o conjunto de dados e objetos do serviço ligado <sup>1</sup> |100 KB |2000 KB |
| Núcleos a pedido no cluster de HDInsight numa subscrição <sup>2</sup> |60 |[Contactar o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Unidade de movimento de dados de nuvem <sup>3</sup> |32 |[Contactar o suporte](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) |
| Repetir contagem pipeline para execuções de atividade |1000 |MaxInt (32 bits) |

<sup>1</sup> pipeline, conjunto de dados e objetos do serviço ligado de representar um agrupamento lógico da carga de trabalho. Os limites para estes objetos não estão relacionadas com tooamount dos dados pode mover e processar com o serviço de Azure Data Factory Olá. Fábrica de dados é concebida tooscale toohandle petabytes de dados.

<sup>2</sup> HDInsight a pedido núcleos alocados fora de subscrição de Olá que contém a fábrica de dados de Olá. Como resultado, Olá acima do limite é Olá fábrica de dados imposta limite núcleos núcleos de HDInsight a pedido e é diferente do limite de núcleos de Olá associado à subscrição do Azure.

<sup>3</sup> unidade de movimento de dados de nuvem (DMU) está a ser utilizada numa operação de cópia da nuvem para a nuvem. É uma medida que representa a potência de Olá (uma combinação de CPU, memória e alocação de recursos de rede) de uma única unidade na fábrica de dados. Pode obter um maior débito de cópia ao tirar partido mais DMUs para alguns cenários. Consulte demasiado[unidades de movimento de dados de nuvem](../articles/data-factory/data-factory-copy-activity-performance.md#cloud-data-movement-units) secção em detalhes.

| **Recurso** | **Predefinição de limite inferior** | **Limite mínimo** |
| --- | --- | --- |
| Intervalo de agendamento |15 minutos |15 minutos |
| Intervalo entre tentativas de repetição |1 segundo |1 segundo |
| Repita o valor de tempo limite |1 segundo |1 segundo |

### <a name="web-service-call-limits"></a>Limites de chamada de serviço Web
O Azure Resource Manager tem os limites de chamadas à API. Pode efetuar chamadas à API uma taxa dentro Olá [limita a API do Azure Resource Manager](../articles/azure-subscription-service-limits.md#resource-group-limits).
