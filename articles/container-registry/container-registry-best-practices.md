---
title: "Melhores práticas no Azure Container Registry"
description: "Saiba como utilizar o registo de contentor do Azure de forma eficiente, ao seguir estas melhores práticas."
services: container-registry
author: mmacy
manager: timlt
ms.service: container-registry
ms.topic: quickstart
ms.date: 12/20/2017
ms.author: marsma
ms.openlocfilehash: d94c6801f96ce684ebb912667dc4aa381c171216
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/18/2017
---
# <a name="best-practices-for-azure-container-registry"></a>Melhores práticas do Azure Container Registry

Ao seguir estas melhores práticas, pode ajudar a maximizar o desempenho e a utilização rentável do seu registo privado do Docker no Azure.

## <a name="network-close-deployment"></a>Implementação sem rede

Crie o registo de contentor na mesma região do Azure em que implementa contentores. Colocar o seu registo numa região sem rede para os anfitriões do seu contentor pode ajudar a reduzir a latência e o custo.

A implementação sem rede é uma das principais razões para utilizar um registo de contentor privado. As imagens do Docker têm uma [construção em camadas](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/) eficiente que permite implementações incrementais. No entanto, os novos nós têm de solicitar todas as camadas necessárias para uma determinada imagem. Este `docker pull` inicial pode adicionar rapidamente até vários gigabytes. Ter um registo privado próximo à sua implementação minimiza a latência de rede.
Além disso, todas as clouds públicas, o Azure incluído, implementam as taxas de saída da rede. Extrair imagens de um datacenter para outro, adiciona taxas de saída da rede além da latência.

## <a name="geo-replicate-multi-region-deployments"></a>Georreplicar implementações em várias regiões

Utilize a funcionalidade de [georreplicação](container-registry-geo-replication.md) do Azure Container Registry, se estiver a implementar contentores em várias regiões. Se estiver a servir clientes globais de datacenters locais ou a sua equipa de desenvolvimento estiver em diferentes localizações, pode simplificar a gestão dos registos e minimizar a latência através da georreplicação do seu registo. Atualmente em pré-visualização, esta funcionalidade está disponível nos registos [Premium](container-registry-skus.md).

Para saber como utilizar a georreplicação, veja o tutorial de três partes [Geo-replication in Azure Container Registry (Georreplicação no Azure Container Registry)](container-registry-tutorial-prepare-registry.md).

## <a name="repository-namespaces"></a>Espaços de nomes do repositório

Ao tirar partido dos espaços de nomes do repositório, pode permitir a partilha de um único registo em vários grupos na sua organização. Os registos podem ser partilhados em implementações e equipas. O Azure Container Registry suporta espaços de nomes aninhados, ao ativar o isolamento de grupo.

Por exemplo, considere as seguintes etiquetas da imagem de contentor. As imagens que são utilizadas a nível empresarial, como `aspnetcore`, são colocadas no espaço de nomes de raiz, enquanto as imagens de contentor pertencentes a grupos de Produção e Marketing utilizam os seus próprios espaços de nomes.

```
contoso.azurecr.io/aspnetcore:2.0
contoso.azurecr.io/products/widget/web:1
contoso.azurecr.io/products/bettermousetrap/refundapi:12.3
contoso.azurecr.io/marketing/2017-fall/concertpromotions/campaign:218.42
```

## <a name="dedicated-resource-group"></a>Grupo de recursos dedicado

Dado que os registos do contentor são recursos que são utilizados em vários anfitriões do contentor, um registo deve residir o seu próprio grupo de recursos.

Embora possa experimentar um tipo de anfitrião específico, como o Azure Container Instances, irá provavelmente eliminar a instância do contentor quando tiver terminado. No entanto, também pode manter a coleção de imagens enviadas para o Azure Container Registry. Ao colocar o seu registo no seu próprio grupo de recursos, está a minimizar o risco de eliminar acidentalmente a coleção de imagens no registo, ao eliminar o grupo de recursos de instância do contentor.

## <a name="authentication"></a>Autenticação

Ao autenticar com um registo de contentor do Azure, existem dois cenários principais: autenticação individual e autenticação de serviço (ou "sem interface"). A tabela seguinte apresenta uma breve descrição geral destes cenários e o método de autenticação recomendado para cada um.

| Tipo | Cenário de exemplo | Método recomendado |
|---|---|---|
| Identidade individual | Um programador a extrair imagens ou enviar imagens a partir da respetiva máquina de desenvolvimento. | [az acr login](/cli/azure/acr?view=azure-cli-latest#az_acr_login) |
| Identidade de serviço/sem interface | Compile e implemente pipelines onde o utilizador não esteja diretamente envolvido. | [Principal de serviço](container-registry-authentication.md#service-principal) |

Para obter informações aprofundadas sobre a autenticação do Azure Container Registry, veja [Authenticate with an Azure container registry (Autenticar com um registo de contentor do Azure)](container-registry-authentication.md).

## <a name="manage-registry-size"></a>Gerir o tamanho do registo

As restrições de armazenamento de cada [registo de contentor SKU] [ container-registry-skus] são destinadas para alinhar com um cenário típico: **Básico** para começar a trabalhar, **Standard**, para a maioria das aplicações de produção, e **Premium**, para desempenho de hiper escala e [georreplicação][container-registry-geo-replication]. Ao longo da vida do registo, deve gerir o tamanho eliminando periodicamente o conteúdo não utilizado.

Pode encontrar a utilização atual de um registo de contentor na **Descrição Geral** registo do contentor no portal do Azure:

![Informações de utilização do registo no portal do Azure][registry-overview-quotas]

Pode gerir o tamanho do registo utilizando o [CLI do Azure] [ azure-cli] ou o [portal do Azure][azure-portal]. Apenas os SKUs geridos (Básico, Standard, Premium) suportam a eliminação de repositório e imagem--não é possível eliminar repositórios, imagens ou etiquetas num registo Clássico.

### <a name="delete-in-azure-cli"></a>Eliminação na CLI do Azure

Utilize o comando [az acr repository delete][az-acr-repository-delete] para eliminar um repositório ou dentro conteúdo de um repositório.

Para eliminar um repositório, incluindo todas as etiquetas e dados de camada de imagem dentro do repositório, especifique apenas o nome do repositório ao executar [az acr repository delete][az-acr-repository-delete]. No exemplo seguinte, elimine o repositório *myapplication* e todas as etiquetas e dados de camada de imagem no repositório:

```azurecli
az acr repository delete --name myregistry --repository myapplication
```

Também pode eliminar dados de imagem de um repositório utilizando os argumentos `--tag` e `--manifest`. Para obter detalhes sobre estes argumentos, veja [referência do comando de eliminação de repositório az acr][az-acr-repository-delete].

### <a name="delete-in-azure-portal"></a>Eliminar no portal do Azure

Para eliminar um repositório de um registo no portal do Azure, primeiro navegue até ao registo de contentor. Em seguida, em **SERVIÇOS**, selecione **Repositórios** e clique com o botão direito do rato no repositório de que pretende eliminar. Selecione **Eliminar** para eliminar o repositório e as imagens Docker que este contém.

![Eliminar um novo repositório no portal do Azure][delete-repository-portal]

De forma similar, também pode eliminar etiquetas a partir de um repositório. Navegue para o repositório, clique com o botão direito do rato na etiqueta que pretende eliminar em **ETIQUETAS** e selecione **Eliminar**.

## <a name="next-steps"></a>Passos seguintes

O Azure Container Registry está disponível em vários escalões, denominadas SKUs, e cada uma dispõe de funcionalidades diferentes. Para obter detalhes sobre as SKUs disponíveis, veja [Azure Container Registry SKUs (SKUs do Azure Container Registry)](container-registry-skus.md).

<!-- IMAGES -->
[delete-repository-portal]: ./media/container-registry-best-practices/delete-repository-portal.png
[registry-overview-quotas]: ./media/container-registry-best-practices/registry-overview-quotas.png

<!-- LINKS - Internal -->
[az-acr-repository-delete]: /cli/azure/acr/repository#az_acr_repository_delete
[azure-cli]: /cli/azure/overview
[azure-portal]: https://portal.azure.com
[container-registry-geo-replication]: container-registry-geo-replication.md
[container-registry-skus]: container-registry-skus.md
