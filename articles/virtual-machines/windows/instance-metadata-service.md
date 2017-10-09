---
title: "aaaAzure metadados de instância de serviço para Windows | Microsoft Docs"
description: "RESTful interface tooget sobre computação, rede e eventos de manutenções da VM do Windows."
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a>Serviço de metadados de instância do Azure para as VMs do Windows


Olá Service de metadados de instância do Azure fornece informações sobre as instâncias de máquina virtual que podem ser utilizado toomanage e configurar as máquinas virtuais em execução.
Isto inclui informações como SKU, a configuração de rede e os eventos de manutenção futura. Para obter mais informações sobre o tipo de informações é disponível, consulte [categorias de metadados](#instance-metadata-data-categories).

Serviço de metadados de instância do Azure é um ponto final de REST tooall acessível VMs de IaaS criado através de Olá [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). ponto final de Olá está disponível um endereço de IP bem conhecidos não encaminháveis internos (`169.254.169.254`) que podem ser acedidos apenas a partir de dentro de Olá VM.



> [!IMPORTANT]
> Este serviço é **geralmente disponível** em regiões globais do Azure. Trata-se em pré-visualização pública para Government, China e na nuvem do Azure de alemão. Regularmente recebe atualizações tooexpose novas informações sobre instâncias de máquina virtual. Esta página reflete Olá atualizado [categorias de dados](#instance-metadata-data-categories) disponíveis.



## <a name="service-availability"></a>Disponibilidade do serviço
serviço de Olá está disponível em todas as regiões do Global Azure geralmente disponíveis. serviço de Olá está em pré-visualização pública em regiões de Olá Government, China ou na Alemanha.

Regiões                                        | Disponibilidade?
-----------------------------------------------|-----------------------------------------------
[Todas as regiões do Azure Global geralmente disponíveis](https://azure.microsoft.com/regions/)     | Geralmente disponível 
[Azure Government](https://azure.microsoft.com/overview/clouds/government/)              | Pré-visualização 
[Azure China](https://www.azure.cn/)                                                           | Pré-visualização
[Datacenters do Azure](https://azure.microsoft.com/overview/clouds/germany/)                    | Pré-visualização

Esta tabela é atualizada quando o serviço de Olá e fica disponível outras nuvens do Azure.

tootry saída Olá serviço de metadados de instância, crie uma VM de [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) ou Olá [portal do Azure](http://portal.azure.com) no Olá acima regiões e siga Olá exemplos abaixo.

## <a name="usage"></a>Utilização

### <a name="versioning"></a>Controlo de versões
Olá instância metadados do serviço é com a versão. As versões são obrigatórias e a versão atual do Olá `2017-04-02`.

> [!NOTE] 
> Pré-visualização as versões anteriores dos eventos agendadas suportados {mais recente} como Olá api-version. Este formato já não é suportado e será preterido no Olá futura.

À medida que adiciona as versões mais recentes, as versões mais antigas podem ainda ser acedidas para compatibilidade, se os scripts terem dependências de formatos de dados específicos. No entanto, tenha em atenção que version(2017-03-01) de pré-visualização atual Olá poderão não estar disponíveis assim que o serviço de Olá estiver geralmente disponível.

### <a name="using-headers"></a>Utilizar cabeçalhos
Quando consultar Olá instância metadados do serviço, tem de fornecer o cabeçalho de Olá `Metadata: true` tooensure Olá pedido não foi inadvertidamente redirecionado o pedido.

### <a name="retrieving-metadata"></a>Obtenção de metadados

Metadados da instância estão disponível para executar as VMs criado/geridos através de [do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/). Aceder a todas as categorias de dados para uma instância de máquina virtual utilizando Olá pedido os seguintes:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> Todas as consultas de metadados de instância diferenciam maiúsculas de minúsculas.

### <a name="data-output"></a>Saída de dados
Por predefinição, Olá instância metadados serviço devolve dados no formato JSON (`Content-Type: application/json`). No entanto, APIs diferentes pode devolver dados em diferentes formatos, se for pedida.
Olá tabela que se segue é uma referência de APIs podem suportar outros formatos de dados.

API | Formato de dados predefinido | Outros formatos
--------|---------------------|--------------
/instance | JSON | Texto
/scheduledevents | JSON | Nenhum

tooaccess um formato de resposta não predefinido, especifique o formato de pedido de Olá como um parâmetro de cadeia de consulta no pedido de Olá. Por exemplo:

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a>Segurança
ponto final de serviço de metadados de instância de Olá é acessível apenas a partir de dentro de Olá executar a instância de máquina virtual num endereço IP não encaminháveis internos. Além disso, qualquer pedido com um `X-Forwarded-For` cabeçalho é rejeitado pelo serviço de Olá.
É também necessário pedidos toocontain um `Metadata: true` tooensure de cabeçalho que Olá pedido real foi diretamente pretendida e não uma parte de redirecionamento não intencional. 

### <a name="error"></a>Erro
Se existir um elemento de dados não encontrado ou um pedido com formato incorreto, Olá instância metadados serviço devolve erros de HTTP padrão. Por exemplo:

Código de estado de HTTP | Razão
----------------|-------
200 OK |
Pedido de 400 incorreta | Falta `Metadata: true` cabeçalho
404 Não Encontrado | Olá does't elemento pedido existe 
405 Método não permitido | Apenas `GET` e `POST` os pedidos são suportados
429 demasiados pedidos | Olá API atualmente suporta um máximo de 5 consultas por segundo
Erro no serviço 500     | Tente novamente após algum tempo

### <a name="examples"></a>Exemplos

> [!NOTE] 
> Todas as respostas de API são cadeias JSON. Todas as respostas de exemplo seguintes são impressas pretty para legibilidade.

#### <a name="retrieving-network-information"></a>A obtenção de informações de rede

**Pedido**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

**Resposta**

> [!NOTE] 
> resposta Olá é uma cadeia JSON. Olá seguinte exemplo de resposta é impresso pretty para legibilidade.

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a>Obter o endereço IP público

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a>Obter todos os metadados para uma instância

**Pedido**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

**Resposta**

> [!NOTE] 
> resposta Olá é uma cadeia JSON. Olá seguinte exemplo de resposta é impresso pretty para legibilidade.

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a>Obtenção de metadados na máquina virtual do Windows

**Pedido**

Metadados de instância podem ser obtido no Windows através do utilitário do PowerShell de Olá `curl`: 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

Ou através de Olá `Invoke-RestMethod` cmdlet:
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

**Resposta**

> [!NOTE] 
> resposta Olá é uma cadeia JSON. Olá seguinte exemplo de resposta é impresso pretty para legibilidade.

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a>Categorias de dados de metadados de instância
Olá seguintes categorias de dados está disponível através de Olá metadados do serviço da instância:

Dados | Descrição
-----|------------
localização | Olá de região do Azure VM está em execução
nome | Nome do Olá VM 
oferta | Disponibilizam informações para a imagem VM Olá. Este valor só está presente para imagens implementadas a partir da Galeria de imagem do Azure.
Fabricante | Publicador de imagem de VM Olá
SKU | SKU específico para a imagem VM Olá  
Versão | Versão da imagem VM Olá 
osType | Linux ou do Windows 
platformUpdateDomain |  [Domínio de atualização](manage-availability.md) Olá VM está em execução no
platformFaultDomain | [Domínio de falhas](manage-availability.md) Olá VM está em execução no
vmId | [Identificador exclusivo](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) para Olá VM
vmSize | [Tamanho da VM](sizes.md)
IPv4/privateIpAddress | Endereço IPv4 local de Olá VM 
IPv4/publicIpAddress | Endereço IPv4 público de Olá VM
endereço de sub-rede / | Endereço de sub-rede de Olá VM
prefixo de sub-rede / | Prefixo de sub-rede, 24 de exemplo
IPv6/ipAddress | Endereço IPv6 local de Olá VM
MacAddress | Endereço mac VM 
scheduledevents | Está a ser atualmente consulte de pré-visualização pública [scheduledevents](scheduled-events.md)

## <a name="example-scenarios-for-usage"></a>Exemplos de cenários de utilização  

### <a name="tracking-vm-running-on-azure"></a>Controlo de VM em execução no Azure

Como um fornecedor de serviços, poderá ser necessário tootrack Olá número as VMs com o seu software ou agentes que necessitam de exclusividade tootrack de Olá VM. toobe tooget capaz de um ID exclusivo para uma VM, utilize Olá `vmId` campo do serviço de metadados de instância.

**Pedido**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

**Resposta**

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a>Colocação de contentores, partições de dados com base em domínio de falhas/atualização 

Alguns cenários, colocação das réplicas de dados diferentes é prime importância. Por exemplo, [colocação de réplica do HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) ou colocação contentor através de um [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) poderá necessitar tooknow Olá `platformFaultDomain` e `platformUpdateDomain` Olá VM está em execução no.
Pode consultar estes dados diretamente através do Olá instância metadados do serviço.

**Pedido**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

**Resposta**

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a>Obter mais informações sobre Olá VM durante caso de suporte 

Como um fornecedor de serviços, poderá receber uma chamada de suporte onde pretende que tooknow mais informações sobre Olá VM. Pedir Olá cliente tooshare Olá computação metadados podem fornecer informações básicas para Olá suporte profissional tooknow sobre o tipo de Olá da VM no Azure. 

**Pedido**

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

**Resposta**

> [!NOTE] 
> resposta Olá é uma cadeia JSON. Olá seguinte exemplo de resposta é impresso pretty para legibilidade.

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a>Exemplos de chamar o serviço de metadados utilizando idiomas diferentes dentro Olá VM 

Idioma | Exemplo 
---------|----------------
Ruby     | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.RB
Aceda a Lan   | https://github.com/Microsoft/azureimds/blob/Master/imdssample.go            
python   | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.PY
C++      | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample-Windows.cpp
C#       | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.CS
Javascript | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.js
PowerShell | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.ps1
Bash       | https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.SH
    

## <a name="faq"></a>FAQ
1. Estou a obter erros de Olá `400 Bad Request, Required metadata header not specified`. O que significa?
   * Olá serviço de metadados de instância requer cabeçalho Olá `Metadata: true` toobe transmitido no pedido de Olá. Transmitir este cabeçalho numa chamada REST de Olá permite acesso toohello instância metadados do serviço. 
2. Por que razão estou posso obter não informações de computação para a minha VM?
   * Olá instância de serviço de metadados apenas suporta atualmente instâncias criadas com o Azure Resource Manager. Olá futura, pode adicionar suporte para as VMs de serviço de nuvem.
3. Criar um algum volta a minha máquina Virtual através do Azure Resource Manager. Por que razão estou posso não ver as informações de metadados de computação?
   * Para quaisquer VMs criadas após Sep 2016, adicione um [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart ver metadados de computação. Para VMs anteriores (criadas antes de Sep 2016), adicionar/remover as extensões ou dados de metadados de toorefresh discos toohello VM.
4. Por que razão estou obter Erro Olá `500 Internal Server Error`?
   * Repita o pedido com base no back exponencial fora do sistema. Se o problema de Olá persistir, contacte o suporte do Azure.
5. Onde posso partilham perguntas/comentários adicionais?
   * Envie os seus comentários sobre http://feedback.azure.com.
7. Isto seria funcionar para a instância de conjunto de dimensionamento de Máquina Virtual?
   * Sim metadados serviço está disponível para instâncias de conjunto de dimensionamento. 
6. Como posso obter suporte para o serviço de Olá?
   * tooget suporte para o serviço de Olá, criar um problema de suporte no portal do Azure para Olá VM onde não é capaz de tooget metadados resposta após várias tentativas de longas 

   ![Suporte de metadados de instância](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre Olá [agendada eventos](scheduled-events.md) API **em pré-visualização pública** fornecida pelo Olá metadados de instância de serviço.
