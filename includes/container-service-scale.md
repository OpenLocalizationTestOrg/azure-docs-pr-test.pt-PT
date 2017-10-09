# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Dimensionar nós de agente num cluster do Container Service
Depois de [implementar um cluster do serviço de contentor Azure](../articles/container-service/dcos-swarm/container-service-deployment.md), poderá ser necessário toochange Olá diversas nós de agente. Por exemplo, poderá precisar de mais agentes, de modo a poder executar mais aplicações de contentores ou instâncias. 

Pode alterar o número de Olá de nós de agente de um cluster DC/OS, Docker Swarm ou Kubernetes utilizando Olá portal do Azure ou Olá Azure CLI 2.0. 

## <a name="scale-with-hello-azure-portal"></a>Dimensionar com Olá portal do Azure

1. No Olá [portal do Azure](https://portal.azure.com), procure **serviços de contentor**e, em seguida, clique em serviço de contentor Olá que pretende que o toomodify.
2. No Olá **serviço de contentor** painel, clique em **agentes**.
3. No **contagem de VM**, introduza o número de Olá pretendido de nós de agentes.

    ![Um agrupamento no portal de Olá de escala](./media/container-service-scale/container-service-scale-portal.png)

4. configuração de Olá toosave, clique em **guardar**.

## <a name="scale-with-hello-azure-cli-20"></a>Dimensionar com Olá Azure CLI 2.0

Certifique-se de que a [instalado](/cli/azure/install-az-cli2) Olá 2.0 de CLI do Azure mais recente e registado no tooan conta do azure (`az login`).

### <a name="see-hello-current-agent-count"></a>Consulte a contagem de agentes Olá atual
número de Olá toosee de agentes atualmente num cluster de Olá, execute Olá `az acs show` comando. Isto mostra a configuração de cluster Olá. Por exemplo, Olá a seguir mostra Olá configuração do serviço de contentor Olá com o nome do comando `containerservice-myACSName` no grupo de recursos de Olá `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

comando Olá devolve o número de Olá de agentes no Olá `Count` valor em `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Utilize Olá az comando da escala de acs
número de Olá toochange de nós de agente, execute Olá `az acs scale` Olá de comando e de alimentação **grupo de recursos**, **nome do serviço de contentor**e Olá pretendido **nova contagem de agente**. Ao utilizar um número mais pequeno ou maior, pode reduzir ou aumentar de forma vertical, respetivamente.

Por exemplo, o número de Olá toochange de agentes Olá anterior too10 de cluster, escreva Olá os seguintes comandos:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Olá, Azure CLI 2.0 devolve uma cadeia JSON que representa a nova configuração de Olá do serviço de contentor Olá, incluindo a nova contagem de agente Olá.

Para obter mais opções de comandos, execute `az acs scale --help`.

## <a name="scaling-considerations"></a>Considerações sobre o dimensionamento

* número de Olá de nós de agente tem de ser entre 1 e 100, inclusive. 

* A quota de núcleos pode limitar o número de Olá de nós de agente num cluster.

* Operações de dimensionamento de nó de agente são aplicados tooan conjunto de dimensionamento da máquina virtual do Azure que contém o agrupamento de agentes Olá. Num cluster DC/OS, apenas nós de agente no conjunto de privada Olá são ampliados por operações Olá apresentadas neste artigo.

* Consoante o orchestrator de Olá que implementar no seu cluster, pode dimensionar separadamente número Olá de instâncias de um contentor em execução no cluster de Olá. Por exemplo, num cluster DC/OS, utilize Olá [IU do Marathon](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange Olá diversas instâncias de uma aplicação de contentor.

* Atualmente, o dimensionamento automático de nós de agentes em clusters de serviços de contentores não é suportado.

## <a name="next-steps"></a>Passos seguintes
* Veja [mais exemplos](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) da utilização de comandos da CLI 2.0 do Azure com o Azure Container Service.
* Saiba mais sobre os [conjuntos de agentes do DC/SO](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) no Azure Container Service.

