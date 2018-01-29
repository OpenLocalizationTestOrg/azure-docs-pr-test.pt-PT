---
title: "Utilizar rascunho com o serviço de contentor do Azure e Azure registo de contentor"
description: "Crie um cluster do Kubernetes no ACS e um Azure Container Registry para criar a sua primeira aplicação no Azure com o Draft."
services: container-service
author: squillace
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 09/14/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: 9cf5b1227e69ada46bc0b1e5ff01cc12e73598f7
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a>Utilizar o Draft com o Azure Container Service e o Azure Container Registry para criar e implementar uma aplicação no Kubernetes

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

O [Draft](https://aka.ms/draft) é uma nova ferramenta de código aberto que permite programar facilmente aplicações baseadas em contentores e implementá-las em clusters do Kubernetes sem que sejam precisos grandes conhecimentos de Docker e Kubernetes -- ou inclusivamente instalá-las. A utilização de ferramentas como o Draft permite-lhe a si e às suas equipas concentrarem-se na criação da aplicação com o Kubernetes em vez de dedicarem tanta atenção à infraestrutura.

Pode utilizar o Draft com qualquer registo de imagens do Docker e com qualquer cluster do Kubernetes, incluindo no local. Este tutorial mostra como utilizar ACS com Kubernetes e ACR para criar um pipeline do programador em direto, mas seguro Kubernetes utilizando rascunho e como utilizar o DNS do Azure para expor nesse pipeline de programador para outras pessoas ver a um domínio.


## <a name="create-an-azure-container-registry"></a>Criar um Azure Container Registry
Pode [criar um Azure Container Registry ](../../container-registry/container-registry-get-started-azure-cli.md) facilmente, mas os passos são os seguintes:

1. Crie um grupo de recursos do Azure para gerir o registo do ACR e o cluster do Kubernetes no ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Criar uma imagem ACR registo utilizando [az acr criar](/cli/azure/acr#create) e certifique-se de que o `--admin-enabled` opção estiver definida como `true`.
      ```azurecli
      az acr create --resource-group draft --name draftacs --sku Basic
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Criar um Azure Container Service com o Kubernetes

Agora, está pronto para utilizar [az acs create](/cli/azure/acs#create) para criar um cluster do ACS tendo o Kubernetes como o valor de `--orchestrator-type`.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes --generate-ssh-keys
```

> [!NOTE]
> Uma vez que o Kubernetes não é o tipo de orquestrador predefinido, confirme que utiliza o comutador `--orchestrator-type kubernetes`.

Quando bem-sucedida, a saída é semelhante ao seguinte.

```json
waiting for AAD role to propagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Uma vez que já tem um cluster, pode utilizar o comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) para importar as credenciais. Agora, tem um ficheiro de configuração local para o seu cluster, de que o Helm e o Draft precisam para fazer o seu trabalho.

## <a name="install-and-configure-draft"></a>Instalar e configurar o Draft


1. Rascunho para o seu ambiente no https://github.com/Azure/draft/releases de transferir e instalar no seu caminho, para que possa ser utilizado o comando.
2. Transferir helm para o seu ambiente no https://github.com/kubernetes/helm/releases e [instalá-lo no seu caminho, para que possa ser utilizado o comando](https://github.com/kubernetes/helm/blob/master/docs/install.md#installing-the-helm-client).
3. Configure o Draft para utilizar o seu registo e criar subdomínios para cada gráfico do Helm que crie. Para configurar o Draft, precisa:
  - Do nome do Azure Container Registry (neste exemplo, `draftacsdemo`)
  - Da chave de registo, ou palavra-passe, de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`

  Chamar `draft init` e o processo de configuração solicita-lhe os valores acima; tenha em atenção que o URL de formato para o URL de registo é o nome do registo (neste exemplo, `draftacsdemo`) plus `.azurecr.io`. O nome de utilizador é o nome do registo no seu próprio. Da primeira vez que o executa, o processo é parecido com o seguinte.
 ```bash
    $ draft init
    Creating /home/ralph/.draft 
    Creating /home/ralph/.draft/plugins 
    Creating /home/ralph/.draft/packs 
    Creating pack go...
    Creating pack python...
    Creating pack ruby...
    Creating pack javascript...
    Creating pack gradle...
    Creating pack java...
    Creating pack php...
    Creating pack csharp...
    $DRAFT_HOME has been configured at /home/ralph/.draft.

    In order to configure Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io/myuser, quay.io/myuser, myregistry.azurecr.io): draftacsdemo.azurecr.io
    2. Enter your username: draftacsdemo
    3. Enter your password: 
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
```

Está agora pronto para implementar uma aplicação.


## <a name="build-and-deploy-an-application"></a>Criar e implementar uma aplicação

O repositório do Draft inclui [seis aplicações de exemplo simples](https://github.com/Azure/draft/tree/master/examples). Clone o repositório e vamos utilizar o [exemplo de Java](https://github.com/Azure/draft/tree/master/examples/java). Mude para o diretório de exemplos/java e o tipo `draft create` para criar a aplicação. Deve ser semelhante ao exemplo seguinte.
```bash
$ draft create
--> Draft detected the primary language as Java with 91.228814% certainty.
--> Ready to sail
```

A saída inclui um Dockerfile e um gráfico do Helm. Para criar e implementar, basta escrever `draft up`. O resultado é um vasto conjunto, mas deve ser semelhante ao seguinte exemplo.
```bash
$ draft up
Draft Up Started: 'handy-labradoodle'
handy-labradoodle: Building Docker Image: SUCCESS ⚓  (35.0232s)
handy-labradoodle: Pushing Docker Image: SUCCESS ⚓  (17.0062s)
handy-labradoodle: Releasing Application: SUCCESS ⚓  (3.8903s)
handy-labradoodle: Build ID: 01BT0ZJ87NWCD7BBPK4Y3BTTPB
```

## <a name="securely-view-your-application"></a>Ver com segurança a sua aplicação

O contentor está agora em execução em ACS. Para ver, utilize o `draft connect` comando, que cria uma ligação segura ao IP do cluster com uma porta específica para a sua aplicação para que possa visualizar localmente. Se tiver êxito, procure o URL ligar à sua aplicação na primeira linha depois do **êxito** indicador.

> [!NOTE]
> Se receber uma mensagem a indicar que não existem pods foram prontos, aguarde um momento e tente novamente ou, pode ver os pods fique pronto com `kubectl get pods -w` e tente novamente quando fazem.

```bash
draft connect
Connecting to your app...SUCCESS...Connect to your app on localhost:46143
Starting log streaming...
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
== Spark has ignited ...
>> Listening on 0.0.0.0:4567
```

No exemplo anterior, poderá escrever `curl -s http://localhost:46143` para receber a resposta `Hello World, I'm Java!`. Quando lhe CTRL + ou CMD + C (dependendo do ambiente do SO), o túnel seguro é desligado e é possível continuar a iterating.

## <a name="sharing-your-application-by-configuring-a-deployment-domain-with-azure-dns"></a>Partilhar a sua aplicação através da configuração de um domínio de implementação com o DNS do Azure

Já efetuou o ciclo de iteração de programador rascunho cria os passos anteriores. No entanto, pode partilhar a aplicação através da internet por:
1. Instalar uma entrada no seu cluster de ACS (para fornecer um endereço IP público no qual pretende apresentar a aplicação)
2. Delegar o domínio personalizado ao DNS do Azure e o domínio de mapeamento para o IP endereço ACS atribui ao seu controlador de entrada

### <a name="use-helm-to-install-the-ingress-controller"></a>Utilize helm para instalar o controlador de entrada.
Utilize **helm** para procurar e instalar `stable/traefik`, um controlador de entrada, para permitir pedidos de entrada para a sua compilações.
```bash
$ helm search traefik
NAME            VERSION DESCRIPTION
stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

$ helm install stable/traefik --name ingress
```
Agora, defina um observador no controlador `ingress` para capturar o valor do IP externo quando for implementado. Este endereço IP é o endereço que vai ser [mapeado para o seu domínio de implementação](#wire-up-deployment-domain) na secção seguinte.

```bash
$ kubectl get svc -w
NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
kubernetes                    10.0.0.1       <none>          443/TCP                      7h
```

Neste caso, o IP externo do domínio de implementação é `13.64.108.240`. Já pode mapear o seu domínio para este IP.

### <a name="map-the-ingress-ip-to-a-custom-subdomain"></a>Mapear o IP de entrada para um subdomínio personalizado

O Draft cria uma versão para cada gráfico do Helm que cria -- cada aplicação em que está a trabalhar. Cada um deles obtém um nome gerado que é utilizado pelo **rascunho** como um _subdomínio_ por cima de raiz _domínio implementação_ controlado por si. (Neste exemplo, utilizamos `squillace.io` como o domínio de implementação.) Para ativar o comportamento deste subdomínio, tem de criar um registo A para `'*.draft'` nas entradas de DNS do seu domínio de implementação, de modo a que cada subdomínio gerado seja encaminhado para o controlador de entradas do cluster do Kubernetes. 

O seu fornecedor de domínio tem a sua própria forma de atribuir servidores DNS; para [delegar os seus servidores de nomes para o DNS do Azure](../../dns/dns-delegate-domain-azure-dns.md), tem de seguir os passos abaixo:

1. Crie um grupo de recursos para a sua zona.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Crie uma zona DNS para o seu domínio.
Utilize o comando [az network dns zone create](/cli/azure/network/dns/zone#create) para obter os servidores de nomes e delegar o controlo de DNS para o DNS do Azure no seu domínio.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. Adicione os servidores DNS que lhe forem dados ao fornecedor do seu domínio de implementação, o que lhe vai permitir utilizar o DNS do Azure para reencaminhar o seu domínio como quiser. Varia de acordo com a forma de fazê-lo por domínio fornecer; [delegar nameservers o domínio ao DNS do Azure](../../dns/dns-delegate-domain-azure-dns.md) contém alguns dos detalhes que deve conhecer. 
4. Assim que o seu domínio tem sido delegado ao DNS do Azure, criar uma entrada de conjunto de registos da para o mapeamento de domínio de implementação para o `ingress` IP a partir do passo 2 da secção anterior.
  ```azurecli
  az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*.draft' -g squillace.io -z squillace.io
  ```
A saída é semelhante ao seguinte.
  ```json
  {
    "arecords": [
      {
        "ipv4Address": "13.64.108.240"
      }
    ],
    "etag": "<guid>",
    "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
    "metadata": null,
    "name": "*.draft",
    "resourceGroup": "squillace.io",
    "ttl": 3600,
    "type": "Microsoft.Network/dnszones/A"
  }
  ```
5. Reinstalar **rascunho**

   1. Remover **draftd** do cluster, escrevendo `helm delete --purge draft`. 
   2. Reinstalar **rascunho** utilizando o mesmo `draft-init` comando, mas com o `--ingress-enabled` opção:
    ```bash
    draft init --ingress-enabled
    ```
   Responda aos pedidos, tal como fez na primeira vez, acima. No entanto, tem uma pergunta mais para responder a, utilizando o caminho completo do domínio que configurou com o DNS do Azure.

6. Introduza o seu domínio de nível superior de entrada (por exemplo, draft.example.com): draft.squillace.io
7. Quando chamar `draft up` nesta altura, será capaz de ver a sua aplicação (ou `curl` -lo) no URL do formulário `<appname>.draft.<domain>.<top-level-domain>`. No caso deste exemplo, `http://handy-labradoodle.draft.squillace.io`. 
```bash
curl -s http://handy-labradoodle.draft.squillace.io
Hello World, I'm Java!
```


## <a name="next-steps"></a>Passos seguintes

Agora que já tem um cluster do Kubernetes no ACS, pode investigar com o [Azure Container Registry](../../container-registry/container-registry-intro.md) para criar mais e diferentes implementações deste cenário. Por exemplo, pode criar um conjunto de registos DNS de domínio draft._basedomain.toplevel_ que controle aspetos de subdomínios mais profundos para implementações do ACS específicas.






