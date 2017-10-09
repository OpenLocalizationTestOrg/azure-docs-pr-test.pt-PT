---
title: aaaLoad equilibrar Kubernetes contentores no Azure | Microsoft Docs
description: "Ligue externamente e o balanceamento de carga entre vários contentores num cluster Kubernetes no serviço de contentor do Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contentores, microserviços, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Contentores de balanceamento de carga num cluster Kubernetes no serviço de contentor do Azure 
Este artigo apresenta balanceamento de carga no cluster Kubernetes no serviço de contentor do Azure. Balanceamento de carga fornece um endereço IP externamente acessível para o serviço de Olá e distribui o tráfego de rede entre pods Olá em execução em VMs do agente.

Pode configurar um toouse de serviço Kubernetes [Balanceador de carga do Azure](../../load-balancer/load-balancer-overview.md) toomanage externo tráfego de rede (TCP). Sem configuração adicional, a carga de balanceamento e o encaminhamento de tráfego HTTP ou HTTPS ou cenários mais avançados é possível.

## <a name="prerequisites"></a>Pré-requisitos
* [Implementar um cluster de Kubernetes](container-service-kubernetes-walkthrough.md) no serviço de contentor do Azure
* [Ligar o seu cliente](../container-service-connect.md) tooyour cluster

## <a name="azure-load-balancer"></a>Balanceador de carga do Azure

Por predefinição, um cluster de Kubernetes implementado no serviço de contentor do Azure inclui um balanceador de carga do Azure para a Internet para o agente de Olá VMs. (Um recurso de Balanceador de carga individual está configurado para mestre Olá VMs.) Balanceador de carga do Azure é um balanceador de carga de camada 4. Atualmente, o Balanceador de carga Olá suporta apenas a tráfego TCP no Kubernetes.

Ao criar um serviço Kubernetes, podem configurar automaticamente o serviço de toohello de acesso de tooallow Balanceador de carga do Azure Olá. Balanceador de carga de Olá tooconfigure, conjunto Olá serviço `type` demasiado`LoadBalancer`. Balanceador de carga Olá cria uma regra toomap um endereço IP público e número de porta de receber tráfego toohello privados IP endereços de serviço e números de porta de pods de Olá no agente VMs (e vice-versa para o tráfego de resposta). 

 Seguem-se dois exemplos que mostra como tooset Olá Kubernetes serviço `type` demasiado`LoadBalancer`. (Depois tentar exemplos de Olá, eliminar as implementações de Olá se já não precisar delas.)

### <a name="example-use-hello-kubectl-expose-command"></a>Exemplo: Olá de utilização `kubectl expose` comando 
Olá [Kubernetes instruções](container-service-kubernetes-walkthrough.md) inclui um exemplo de como tooexpose um serviço com Olá `kubectl expose` comando e a respetiva `--type=LoadBalancer` sinalizador. Eis os passos de Olá:

1. Inicie uma nova implementação do contentor. Por exemplo, Olá seguir inicia comando chamada de uma nova implementação `mynginx`. implementação de Olá consiste em três contentores com base na imagem de Docker Olá para o servidor de web Olá Nginx.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Certifique-se de que os contentores de Olá estão em execução. Por exemplo, se consultar para contentores de Olá com `kubectl get pods`, consulte o seguinte de toohello semelhante de saída:

    ![Obter contentores Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure Olá carga balanceador tooaccept tráfego externo toohello implementação, execute `kubectl expose` com `--type=LoadBalancer`. Olá seguinte comando expõe servidor de Nginx Olá na porta 80:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Tipo `kubectl get svc` estado de Olá toosee dos serviços de Olá num cluster de Olá. Enquanto o Balanceador de carga Olá configura a regra de Olá, Olá `EXTERNAL-IP` de Olá serviço aparece como `<pending>`. Após alguns minutos, é configurado o endereço IP externo de Olá: 

    ![Configurar o Balanceador de carga do Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Certifique-se de que pode aceder ao serviço de Olá no endereço IP externo de Olá. Por exemplo, abra um endereço IP do web browser toohello mostrado. browser de Olá mostra Olá Nginx web servidor a executar dos contentores Olá. Em alternativa, execute Olá `curl` ou `wget` comando. Por exemplo:

    ```
    curl 13.82.93.130
    ```

    Deverá ver uma saída semelhante a:

    ![Acesso Nginx com curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. configuração de Olá toosee Olá do Azure de Balanceador de carga, aceda toohello [portal do Azure](https://portal.azure.com).

7. Navegue para o grupo de recursos de Olá para o cluster do serviço de contentor e selecione o Balanceador de carga Olá para o agente de Olá VMs. O nome deve ser Olá, mesmo que o serviço de contentor Olá. (Não escolha Balanceador de carga Olá para nós principais Olá, Olá um cujo nome inclui **master-lb**.) 

    ![Balanceador de carga no grupo de recursos](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. detalhes de Olá toosee da configuração de Balanceador de carga Olá, clique em **as regras de balanceamento de carga** e o nome de Olá Olá de regra de que foi configurada.

    ![Regras de Balanceador de carga](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Exemplo: Especificar `type: LoadBalancer` no ficheiro de configuração do serviço de Olá

Se implementar uma aplicação de contentor Kubernetes de JSON ou YAML [ficheiro de configuração do serviço](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), especifique um balanceador de carga externo, adicionando Olá especificação de serviço linha toohello os seguintes:

```YAML
 "type": "LoadBalancer"
``` 



Olá passos seguintes utilizam Olá Kubernetes [Guestbook exemplo](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). Neste exemplo é uma aplicação web de várias camadas com base nas imagens de Redis e PHP Docker. Pode especificar no ficheiro de configuração do serviço de Olá que Olá front-end PHP o servidor utiliza o Balanceador de carga do Azure de Olá.

1. Transferir o ficheiro de Olá `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Procurar Olá `spec` para Olá `frontend` serviço.
3. Anule os comentários linha Olá `type: LoadBalancer`.

    ![Balanceador de carga na configuração do serviço](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Guarde o ficheiro de Olá e implementar a aplicação Olá executando Olá os seguintes comandos:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Tipo `kubectl get svc` estado de Olá toosee dos serviços de Olá num cluster de Olá. Enquanto o Balanceador de carga Olá configura a regra de Olá, Olá `EXTERNAL-IP` de Olá `frontend` serviço aparece como `<pending>`. Após alguns minutos, é configurado o endereço IP externo de Olá: 

    ![Configurar o Balanceador de carga do Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Certifique-se de que pode aceder ao serviço de Olá no endereço IP externo de Olá. Por exemplo, pode abrir um web browser toohello endereço IP externo do serviço de Olá.

    ![Acesso guestbook externamente](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Pode adicionar guestbook entradas.

7. configuração de Olá toosee Olá do Azure de Balanceador de carga, navegue para o recurso de Balanceador de carga Olá para cluster Olá Olá [portal do Azure](https://portal.azure.com). Consulte os passos Olá no exemplo anterior Olá.

### <a name="considerations"></a>Considerações

* A criação de regra de Balanceador de carga Olá acontece de forma assíncrona e informações sobre o Balanceador de Olá aprovisionado são publicadas no serviço de Olá `status.loadBalancer` campo.
* Cada serviço é atribuído automaticamente o seu próprio endereço IP virtual no balanceador de carga Olá.
* Se quiser Balanceador de carga de Olá tooreach por um nome DNS, trabalhar com o seu toocreate de fornecedor de serviço de domínio um nome DNS para endereço IP da regra de Olá.

## <a name="http-or-https-traffic"></a>Tráfego HTTP ou HTTPS

Saldo de tooload HTTP ou HTTPS tráfego toocontainer aplicações web e gerir certificados de segurança de camada de transporte (TLS), pode utilizar Olá Kubernetes [entrada](https://kubernetes.io/docs/user-guide/ingress/) recursos. Uma entrada é uma coleção de regras que permitem ligações de entrada serviços de cluster de Olá tooreach. Para um toowork de recurso de entrada, cluster de Kubernetes Olá tem de ter um [controlador entrada](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) em execução.

Serviço de contentor do Azure não implementa um controlador de entrada Kubernetes automaticamente. Estão disponíveis várias implementações de controlador. Atualmente, Olá [controlador Nginx entrada](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) recomenda tooconfigure regras de entrada e de balanceamento de carga de tráfego HTTP e HTTPS. 

Para obter mais informações, consulte Olá [documentação do controlador de entrada Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Quando utilizar Olá controlador Nginx entrada no serviço de contentor do Azure, tem de expor como um serviço com a implementação do controlador de Olá `type: LoadBalancer`. Esta ação configura o controlador de toohello de tráfego de tooroute Balanceador de carga do Azure Olá. Para obter mais informações, consulte a secção anterior Olá.


## <a name="next-steps"></a>Passos seguintes

* Consulte Olá [Kubernetes LoadBalancer documentação](https://kubernetes.io/docs/user-guide/load-balancer/)
* Saiba mais sobre [controladores Kubernetes entrada e de entrada](https://kubernetes.io/docs/user-guide/ingress/)
* Consulte [Kubernetes exemplos](https://github.com/kubernetes/kubernetes/tree/master/examples)

