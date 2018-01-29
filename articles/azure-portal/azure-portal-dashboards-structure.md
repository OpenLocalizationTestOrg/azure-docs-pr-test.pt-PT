---
title: A estrutura dos Dashboards do Azure | Microsoft Docs
description: Este artigo explica a estrutura JSON de um Dashboard do Azure
services: azure-portal
documentationcenter: 
author: adamab
manager: timlt
editor: tysonn
ms.service: azure-portal
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/01/2017
ms.author: adamab
ms.openlocfilehash: f71ff9383f20a1a75fd2c1cf4dc3aaf049d970cf
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="the-structure-of-azure-dashboards"></a>A estrutura dos Dashboards do Azure
Este documento explica a estrutura de um dashboard do Azure, utilizando o dashboard seguinte como exemplo:

![dashboard de exemplo](./media/azure-portal-dashboards-structure/sample-dashboard.png)

Uma vez que partilhado [dashboards do Azure são recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), este dashboard pode ser representado como JSON.  O JSON seguinte representa o dashboard visualizado acima.

```json

{
    "properties": {
        "lenses": {
            "0": {
                "order": 0,
                "parts": {
                    "0": {
                        "position": {
                            "x": 0,
                            "y": 0,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "content": "## Azure Virtual Machines Overview\r\nNew team members should watch this video to get familiar with Azure Virtual Machines.",
                                        "title": "",
                                        "subtitle": ""
                                    }
                                }
                            }
                        }
                    },
                    "1": {
                        "position": {
                            "x": 3,
                            "y": 0,
                            "rowSpan": 4,
                            "colSpan": 8
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "content": "This is the team dashboard for the test VM we use on our team. Here are some useful links:\r\n\r\n1. [Getting started](https://www.contoso.com/tsgs)\r\n1. [Troubleshooting guide](https://www.contoso.com/tsgs)\r\n1. [Architecture docs](https://www.contoso.com/tsgs)",
                                        "title": "Test VM Dashboard",
                                        "subtitle": "Contoso"
                                    }
                                }
                            }
                        }
                    },
                    "2": {
                        "position": {
                            "x": 0,
                            "y": 2,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/VideoPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "title": "",
                                        "subtitle": "",
                                        "src": "https://www.youtube.com/watch?v=YcylDIiKaSU&list=PLLasX02E8BPCsnETz0XAMfpLR1LIBqpgs&index=4",
                                        "autoplay": false
                                    }
                                }
                            }
                        }
                    },
                    "3": {
                        "position": {
                            "x": 0,
                            "y": 4,
                            "rowSpan": 3,
                            "colSpan": 11
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Percentage CPU",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "4": {
                        "position": {
                            "x": 0,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Disk Read Operations/Sec",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Disk Write Operations/Sec",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "5": {
                        "position": {
                            "x": 3,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Disk Read Bytes",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Disk Write Bytes",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "6": {
                        "position": {
                            "x": 6,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Network In",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Network Out",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "7": {
                        "position": {
                            "x": 9,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 2
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "id",
                                    "value": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Compute/PartType/VirtualMachinePart",
                            "asset": {
                                "idInputName": "id",
                                "type": "VirtualMachine"
                            },
                            "defaultMenuItemId": "overview"
                        }
                    }
                }
            }
        },
        "metadata": {
            "model": {
                "timeRange": {
                    "value": {
                        "relative": {
                            "duration": 24,
                            "timeUnit": 1
                        }
                    },
                    "type": "MsPortalFx.Composition.Configuration.ValueTypes.TimeRange"
                }
            }
        }
    },
    "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/dashboards/providers/Microsoft.Portal/dashboards/aa9786ae-e159-483f-b05f-1f7f767741a9",
    "name": "aa9786ae-e159-483f-b05f-1f7f767741a9",
    "type": "Microsoft.Portal/dashboards",
    "location": "eastasia",
    "tags": {
        "hidden-title": "Created via API"
    }
}

```

## <a name="common-resource-properties"></a>Propriedades comuns de recursos

Vamos dividir as secções relevantes de JSON.  As propriedades de nível superior, __id__, __nome__, __tipo__, __localização__, e __etiquetas__ são propriedades partilhado entre todos os tipos de recursos do Azure. Ou seja, não têm muito com conteúdo do dashboard.

### <a name="the-id-property"></a>A propriedade de id

O id de recurso do Azure, requerente para o [convenções de recursos do Azure de nomenclatura](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). Quando o portal cria um dashboard escolhe geralmente um id sob a forma de um guid, mas é livres de utilizar um nome válido ao criá-los através de programação. 

### <a name="the-name-property"></a>A propriedade de nome
O nome é o segmento de recurso Id que não inclua a subscrição, tipo de recurso ou informações do grupo de recursos. Essencialmente, é o último segmento do id do recurso.

### <a name="the-type-property"></a>A propriedade de tipo
Todos os dashboards são do tipo __Microsoft.Portal/dashboards__.

### <a name="the-location-property"></a>A propriedade de localização
Ao contrário de outros recursos, dashboards não tem um componente de tempo de execução.  Para dashboards, a localização indica a localização geográfica primária que armazena a representação JSON do dashboard. O valor deve ser um dos códigos de localização que podem ser obtidos utilizando o [localizações API no recurso de subscrições](https://docs.microsoft.com/rest/api/resources/subscriptions).

### <a name="the-tags-property"></a>A propriedade de etiquetas
As etiquetas são uma funcionalidade comum de recursos do Azure que lhe permitem organizar os seus recursos por pares de valor de nome arbitrários. Para dashboards, há um tag especial chamado __título oculto__. Se o dashboard tem esta propriedade preenchida, em seguida, é utilizado como o nome a apresentar para o seu dashboard no portal. Não não possível mudar o nome de Ids de recurso do Azure, mas podem etiquetas. Esta etiqueta dá-lhe uma forma de ter um nome a apresentar renamable para o seu dashboard.

`"tags": { "hidden-title": "Created via API" }`

### <a name="the-properties-object"></a>O objeto de propriedades
O objeto de propriedades contém duas propriedades, __as lentes__ e __metadados__. O __as lentes__ propriedade contém informações sobre os mosaicos (a.k.a. partes) no dashboard.  O __metadados__ propriedade existe para potenciais funcionalidades futuras.

### <a name="the-lenses-property"></a>A propriedade as lentes
O __as lentes__ propriedade contém o dashboard. Tenha em atenção que o lentes objeto neste exemplo contém uma propriedade de único denominada "0". As lentes são um conceito de agrupamento que não está atualmente implementado nos dashboards. Por agora, todos os seus dashboards ter esta propriedade de único do objeto de lente, novamente, chamada "0".

### <a name="the-lens-object"></a>O objeto de lente
O objeto por baixo de "0" contém duas propriedades, __ordem__ e __partes__.  Na versão atual do dashboards, __ordem__ é sempre 0. O __partes__ propriedade contém um objeto que define os componentes individuais (a.k.a. os mosaicos) no dashboard.

O __partes__ objeto contém uma propriedade para cada parte, onde o nome da propriedade é um número. Este número não é significativo. 

### <a name="the-part-object"></a>O objeto de parte
Cada objeto de parte individuais tem um __posição__, e __metadados__.

### <a name="the-position-object"></a>O objeto de posição
O __posição__ propriedade contém as informações de tamanho e localização para a parte expresso como __x__, __y__, __rowSpan__e __colSpan__. Os valores estão em termos de unidades de grelha. Estas unidades de grelha estão visíveis ao dashboard está no modo de personalizar, conforme mostrado aqui. Se pretender que um mosaico para ter uma largura de duas unidades de grelha, uma altura da unidade de uma grelha e uma localização na parte superior esquerda canto do dashboard, em seguida, o obejct posição tem o seguinte aspeto:

`location: { x: 0, y: 0, rowSpan: 2, colSpan: 1 }`

![unidades de grelha](./media/azure-portal-dashboards-structure/grid-units.png)

### <a name="the-metadata-object"></a>O objeto de metadados
Cada parte tem uma propriedade de metadados, um objeto tem apenas uma propriedade necessária chamada __tipo__. Esta cadeia informa o portal que mosaico para mostrar. A nossa dashboard de exemplo utiliza estes tipos de mosaicos:


1. `Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart`– Utilizada para mostrar as métricas de monitorização
1. `Extension[azure]/HubsExtension/PartType/MarkdownPart`– Utilizada para mostrar com texto ou as imagens com formatação básico de listas, ligações, etc.
1. `Extension[azure]/HubsExtension/PartType/VideoPart`– Utilizada para mostrar os vídeos do YouTube, Channel9 e qualquer outro tipo de vídeo que funciona de uma tag de vídeo de html.
1. `Extension/Microsoft_Azure_Compute/PartType/VirtualMachinePart`– Utilizada para mostrar o nome e o estado de uma máquina virtual do Azure.

Cada tipo de parte tem a respetiva configuração. As propriedades de configuração possíveis são denominadas __entradas__, __definições__, e __asset__. 

### <a name="the-inputs-object"></a>O objeto de entradas
O objeto de entradas geralmente contém informações que está vinculado a um mosaico para uma instância de recurso.  A parte da máquina virtual no nosso dashboard de exemplo contém uma entrada único que utiliza o id de recurso do Azure para expressar o enlace.  Este formato de id de recurso é consistente em todos os recursos do Azure.

```json
"inputs":
[
    {
        "name": "id",
        "value": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
    }
]

```
A parte do gráfico de métricas tem uma entrada único que expresse precisa o recurso para criar o enlace, bem como informações sobre o metric(s) que está a ser apresentado. Segue-se a entrada para o mosaico que é que mostra as métricas de rede e rede saída.

```json
“inputs”:
[
    {
        "name": "queryInputs",
        "value": 
        {
            "timespan": 
            {
                "duration": "PT1H",
                "start": null,
                "end": null
           },
            "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
            "chartType": 0,
            "metrics": 
            [
                {
                    "name": "Network In",
                    "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                },
                {
                    "name": "Network Out",
                    "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                }
            ]
        }
    }
]

```

### <a name="the-settings-object"></a>O objeto de definições
O objeto de definições contém os elementos de uma parte configuráveis.  No nosso dashboard de exemplo, a parte de Markdown utiliza as definições para armazenar o conteúdo, bem como um título configurável e subtítulo de markdown personalizado.

```json
"settings": 
{
    "content": 
    {
        "settings": 
        {
            "content": "This is the team dashboard for the test VM we use on our team. Here are some useful links:\r\n\r\n1. [Getting started](https://www.contoso.com/tsgs)\r\n1. [Troubleshooting guide](https://www.contoso.com/tsgs)\r\n1. [Architecture docs](https://www.contoso.com/tsgs)",
            "title": "Test VM Dashboard",
            "subtitle": "Contoso"
        }
    }
}

```

Da mesma forma, o mosaico gráfica tem as suas próprias definições que contêm um ponteiro para o vídeo para reprodução, uma definição da reprodução automática ROM e informações de título opcional.

```json
"settings": 
{
   "content": 
    {
        "settings": 
        {
            "title": "",
            "subtitle": "",
            "src": "https://www.youtube.com/watch?v=YcylDIiKaSU&list=PLLasX02E8BPCsnETz0XAMfpLR1LIBqpgs&index=4",
            "autoplay": false
        }
    }
}

```

### <a name="the-asset-object"></a>O objeto elemento
Os mosaicos que estão vinculados aos objetos de portais primeiro class geríveis (denominados ativos) tem esta relação expressa através do objeto de elemento.  No nosso dashboard de exemplo, o mosaico de máquina virtual contém esta descrição de recurso.  O __idInputName__ propriedade indica ao portal do que o id de entrada contém o identificador exclusivo para o elemento, neste caso, o id de recurso. Tipos de recursos mais Azure tem ativos definidos no portal.

`"asset": {    "idInputName": "id",    "type": "VirtualMachine"    }`