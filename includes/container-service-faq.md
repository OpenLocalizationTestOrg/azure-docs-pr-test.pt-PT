# <a name="container-service-frequently-asked-questions"></a>Perguntas mais frequentes sobre o Container Service

## <a name="orchestrators"></a>Orquestradores

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Que orquestradores de contentor suporta no Azure Container Service? 

Existe suporte para DC/SO de código aberto, Docker Swarm e Kubernetes. Para obter mais informações, consulte Olá [descrição geral](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Suporta o modo Docker Swarm? 

Não é atualmente suportado modo Swarm, mas é no plano de serviço Olá. 

### <a name="does-azure-container-service-support-windows-containers"></a>O Azure Container Service suporta contentores do Windows?  

Atualmente são suportados contentores de Linux com todos os orquestradores. O suporte para contentores do Windows com Kubernetes está em pré-visualização.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Recomenda um orquestrador específico no Azure Container Service? 
Geralmente não recomendamos um orquestrador específico. Se tiver experiência com um dos orchestrators Olá suportada, pode aplicar essa experiência no serviço de contentor do Azure. As tendências de dados sugerem, no entanto, que o DC/SO seja comprovado pela produção de Macrodados e as cargas de trabalho de IoT, o Kubernetes é adequado para cargas de trabalho de cloud nativa e o Docker Swarm é conhecido pela integração com ferramentas de Docker e uma fácil uma curva de aprendizagem.

Dependendo do seu cenário, também pode criar e gerir soluções de contentor personalizadas com outros serviços do Azure. Estes serviços incluem [Máquinas Virtuais](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Aplicações Web](../articles/app-service-web/app-service-web-overview.md) e [Batch](../articles/batch/batch-technical-overview.md).  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>O que é a diferença de Olá entre o serviço de contentor do Azure e de motor de ACS? 
Serviço de contentor do Azure é um serviço Azure SLA de segurança com funcionalidades no Olá portal do Azure, as ferramentas da linha de comandos do Azure e APIs do Azure. serviço de Olá permite tooquickly implementar e gerir clusters que executem ferramentas de orquestração do contentor standard com um número relativamente pequeno de opções de configuração. 

[Motor de ACS](http://github.com/Azure/acs-engine) for um projeto de open source que permite a configuração de cluster do power utilizadores toocustomize Olá em cada nível. Esta configuração de Olá tooalter de capacidade de infraestrutura e software significa que não oferecemos de nenhum SLA para o motor de ACS. Suporte é processado através do projeto de fonte aberta Olá no GitHub, em vez de através dos canais de Microsoft oficiais. 

## <a name="cluster-management"></a>Gestão de clusters

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Como criar chaves SSH para o meu cluster?

Pode utilizar ferramentas padrão no seu sistema operativo de toocreate um par de chaves público e privado SSH RSA para autenticação nas máquinas virtuais Linux Olá para o cluster. Para obter os passos, consulte Olá [OS X e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) orientações. 

Se utilizar [comandos de Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy um contentor do serviço cluster, SSH chaves podem ser geradas automaticamente para o cluster.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Como posso criar um serviço principal para o meu cluster de Kubernetes?

Um ID de principal de serviço do Azure Active Directory e a palavra-passe também são necessário toocreate um cluster de Kubernetes no serviço de contentor do Azure. Para obter mais informações, consulte [sobre principal de serviço Olá para um cluster de Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Se utilizar [comandos de Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy um Kubernetes cluster, o serviço principais credenciais podem ser geradas automaticamente para o cluster.

### <a name="how-large-a-cluster-can-i-create"></a>Que tamanho de cluster posso criar?
Pode criar clusters com um, três ou cinco nós principais. Pode escolher se too100 nós de agente.

> [!IMPORTANT]
> Para clusters maiores e consoante Olá que escolher para os nós de tamanho VM, poderá ter de quota de núcleos de Olá tooincrease na sua subscrição. toorequest um aumento de quota, abra uma [pedido de suporte ao cliente online](../articles/azure-supportability/how-to-create-azure-support-request.md) , sem encargos. Se estiver a utilizar uma [conta gratuita do Azure](https://azure.microsoft.com/free/), pode utilizar apenas um número limitado de núcleos de computação do Azure.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Como aumentar o número de Olá de estrutura mestres depois de criar um cluster? 
Assim que a criação do cluster de Olá, número de Olá de estrutura mestres é fixo e não pode ser alterado. Durante a criação de Olá do cluster de Olá, idealmente, deve selecionar vários modelos de estrutura mestres para elevada disponibilidade.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Como aumentar o número de Olá de agentes depois de criar um cluster? 
Pode dimensionar o número de Olá de agentes no cluster de Olá utilizando Olá portal do Azure ou ferramentas de linha de comandos. Consulte [Dimensionar um cluster do Azure Container Service](../articles/container-service/kubernetes/container-service-scale.md).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Quais são os URLs de Olá dos meus modelos de estrutura mestres e agentes? 
Olá URLs do cluster de recursos no serviço de contentor do Azure se baseiam em Olá de nomes DNS prefixo forneça e Olá nome Olá região do Azure que escolheu para a implementação. Por exemplo, o nome de domínio completamente qualificado (FQDN) Olá do nó principal Olá é deste formulário:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Pode encontrar URLs frequentemente utilizados para o seu cluster no Olá portal do Azure, Olá Explorador de recursos do Azure ou outras ferramentas do Azure.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Como posso saber qual a versão do orquestrador em execução no meu cluster?

* DC/SO: Consulte Olá [documentação do Mesosphere](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: executar `docker version`
* Kubernetes: executar `kubectl version`

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Como atualizar o orchestrator Olá após a implementação?

Atualmente, o serviço de contentor do Azure não indique ferramentas tooupgrade Olá versão orchestrator Olá implementada no seu cluster. Se o Container Service suportar uma versão posterior, pode implementar um novo cluster. Outra opção é ferramentas do orchestrator específicas de toouse se estiverem disponível tooupgrade um cluster no local. Por exemplo, veja [Atualizar DC/OS](https://dcos.io/docs/1.8/administration/upgrading/).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Onde posso encontrar o cluster de toomy de cadeia de ligação SSH Olá?

Pode encontrar a cadeia de ligação de Olá no Olá portal do Azure ou através de ferramentas da linha de comandos do Azure. 

1. No portal de Olá, navegue até toohello o grupo de recursos para a implementação de cluster Olá.  

2. Clique em **descrição geral** e clique em ligação Olá para **implementações** em **Essentials**. 

3. No Olá **histórico de implementação** painel, clique em implementação Olá que tem um nome que começa com **microsoft acs** seguido de uma data de implementação. Exemplo: microsoft-acs-201701310000.  

4. No Olá **resumo** página **saídas**, são fornecidas várias hiperligações de cluster. **SSHMaster0** fornece um SSH ligação cadeia toohello primeiro mestre do cluster do serviço de contentor. 

Como apontou anteriormente, também pode utilizar as ferramentas do Azure toofind Olá FQDN do mestre de Olá. Efetuar uma ligação SSH mestre toohello Olá FQDN do mestre de Olá e o nome de utilizador de Olá especificado ao criar o cluster de Olá a utilizar. Por exemplo:

```bash
ssh userName@masterFQDN –A –p 22 
```

Para obter mais informações, consulte [cluster do serviço de contentor do Azure de tooan de ligar](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Passos seguintes

* [Saiba mais](../articles/container-service/kubernetes/container-service-intro-kubernetes.md) sobre o Azure Container Service.
* Implementar um cluster do serviço de contentor utilizando Olá [portal](../articles/container-service/dcos-swarm/container-service-deployment.md) ou [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
