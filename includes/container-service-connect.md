# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Se um cluster tooa ligação remota Kubernetes, DC/OS ou Docker Swarm
Depois de criar um cluster do serviço de contentor do Azure, é necessário tooconnect toohello cluster toodeploy e gerir as cargas de trabalho. Este artigo descreve como tooconnect toohello mestre VM de Olá cluster a partir de um computador remoto. 

clusters de Olá Kubernetes, DC/OS e Docker Swarm fornecem pontos finais de HTTP localmente. Para Kubernetes, este ponto final de forma segura está exposta no Olá internet e pode aceder ao mesmo executando Olá `kubectl` ferramenta da linha de comandos a partir de qualquer computador ligado à internet. 

Para DC/OS e Docker Swarm, recomendamos que crie um túnel secure shell (SSH) do seu sistema de gestão de cluster do computador local toohello. Uma vez estabelecido túnel Olá, pode executar os comandos que utilizam pontos finais HTTP Olá e interface web da vista Olá do orchestrator (se disponível) do sistema local. 

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster do Kubernetes, DC/OS, Docker ou Swarm [implementado no Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).
* SSH RSA ficheiro de chave privada, correspondente toohello toohello adicionado de chave pública cluster durante a implementação. Estes comandos pressupõem que está a essa chave SSH privada Olá ser `$HOME/.ssh/id_rsa` no seu computador. Veja estas instruções para [macOS e Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md), para obter mais informações. Se Olá ligação SSH não está a funcionar, poderá ser necessário demasiado [repor as chaves SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Ligue tooa Kubernetes cluster

Siga estes passos tooinstall e configurar `kubectl` no seu computador.

> [!NOTE] 
> No Linux ou macOS, poderá ser necessário comandos Olá toorun esta secção utilizando `sudo`.
> 

### <a name="install-kubectl"></a>Instalar o kubectl
Uma forma tooinstall esta ferramenta é toouse Olá `az acs kubernetes install-cli` comandos de Azure CLI 2.0. toorun este comando, certifique-se de que a [instalado](/cli/azure/install-az-cli2) Olá 2.0 de CLI do Azure mais recente e registado no tooan conta do Azure (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

Em alternativa, pode transferir os mais recentes Olá `kubectl` cliente diretamente a partir de Olá [Kubernetes versões página](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Para obter mais informações, consulte [Installing and Setting up kubectl (Instalar e Configurar o kubectl)](https://kubernetes.io/docs/tasks/kubectl/install/).

### <a name="download-cluster-credentials"></a>Transferir as credenciais do cluster
Assim que tiver `kubectl` instalado, terá de máquina de tooyour do toocopy Olá cluster credenciais. As credenciais do toodo unidirecional get Olá é com Olá `az acs kubernetes get-credentials` comando. Transmita o nome de Olá Olá do grupo de recursos e o nome de Olá do recurso de serviço de contentor Olá:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Este comando transfere as credenciais de cluster Olá demasiado`$HOME/.kube/config`, onde `kubectl` espera que toobe localizado.

Em alternativa, pode utilizar `scp` toosecurely copiar o ficheiro da Olá de `$HOME/.kube/config` no Olá mestre VM tooyour computador local. Por exemplo:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Se estiver no Windows, pode utilizar Bash no Ubuntu no Windows, o cliente de cópia de ficheiros segura PuTTy Olá ou uma ferramenta semelhante.

### <a name="use-kubectl"></a>Utilizar o kubectl

Assim que tiver `kubectl` configurado, testar a ligação de Olá enumerando nós Olá do cluster:

```bash
kubectl get nodes
```

Pode experimentar outros comandos do `kubectl`. Por exemplo, pode ver Olá Kubernetes Dashboard. Primeiro, execute um proxy de servidor de Kubernetes API toohello:

```bash
kubectl proxy
```

Olá Kubernetes IU está agora disponível em: `http://localhost:8001/ui`.

Para obter mais informações, consulte Olá [início rápido Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Ligue o cluster de DC/OS ou Swarm tooa

Olá toouse DC/OS e Docker Swarm clusters implementados pelo serviço de contentor do Azure, siga estas instruções toocreate um túnel SSH do sistema local do Linux, macOS ou do Windows. 

> [!NOTE]
> Estas instruções centram-se no encapsulamento do tráfego TCP através de SSH. Também pode iniciar uma sessão interativa de SSH com um dos sistemas de gestão de cluster interno Olá, mas não é recomendável. Trabalhar diretamente num sistema interno acarreta riscos de fazer alterações à configuração inadvertidamente.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Criar um túnel SSH no Linux ou macOS
Olá primeira coisa que que fazer quando criar um túnel SSH no Linux ou macOS é toolocate Olá pública nome DNS Olá com balanceamento de carga modelos de estrutura mestres. Siga estes passos.


1. No Olá [portal do Azure](https://portal.azure.com), procure o grupo de recursos de toohello que contém o cluster do serviço de contentor. Expanda o grupo de recursos de Olá, para que cada recurso é apresentado. 

2. Clique em Olá **serviço de contentor** recursos e clique em **descrição geral**. Olá **mestre FQDN** de Olá cluster aparecerá em **Essentials**. Guarde este nome para utilização posterior. 

    ![Nome DNS público](./media/container-service-connect/pubdns.png)

    Em alternativa, execute Olá `az acs show` comando no seu serviço de contentor. Procure Olá **mestre de perfil: fqdn** propriedade no resultado do comando de Olá.

3. Agora, abra uma shell e execute Olá `ssh` comando, especificando Olá os seguintes valores: 

    **LOCAL_PORT** é a porta TCP Olá no lado do serviço de Olá da Olá túnel tooconnect para. Para o Swarm, defina este too2375. Para DC/OS, defina este too80. 
    **REMOTE_PORT** Olá é a porta do ponto final de Olá que pretende que o tooexpose. Para Swarm, utilize a porta 2375. Para o DC/OS, utilize a porta 80.  
    **Nome de utilizador** é o nome de utilizador de Olá fornecido quando implementou o cluster de Olá.  
    **DNSPREFIX** é Olá prefixo DNS que forneceu quando implementou o cluster de Olá.  
    **REGIÃO** região Olá em que o grupo de recursos está localizado.  
    **PATH_TO_PRIVATE_KEY** [opcional] é Olá caminho toohello chave privada que corresponde ao toohello chave pública que forneceu quando criou o cluster de Olá. Utilize esta opção com Olá `-i` sinalizador.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Olá porta de ligação SSH é 2200 e não Olá porta padrão 22. Num cluster com mais do que uma VM principal, este é Olá ligação porta toohello primeiro mestre de VM.
  > 

  comando de Olá devolve sem saída.

Veja exemplos de Olá para DC/OS e Swarm no Olá seguintes secções:    

### <a name="dcos-tunnel"></a>Túnel do DC/OS
tooopen um túnel para pontos finais de DC/OS, execute um comando semelhante Olá seguinte:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> Certifique-se de que não tem outro processo local que vincule a porta 80. Se necessário, pode especificar uma porta local diferente da 80, como a 8080. Contudo, se utilizar esta porta, alguns links da IU da Web poderão não funcionar.
>

Agora pode aceder aos pontos finais de DC/SO Olá do sistema local através de Olá os seguintes URLs (assumindo que local porta 80):

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

Da mesma forma, pode atingir resto Olá das APIs para cada aplicação através deste túnel.

### <a name="swarm-tunnel"></a>Túnel do Swarm
tooopen um túnel toohello ponto final Swarm, execute um comando semelhante Olá seguinte:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> Certifique-se de que não tem outro processo local que vincule a porta 2375. Por exemplo, se estiver a executar o daemon de Docker Olá localmente, é definido pela porta de toouse predefinida 2375. Se necessário, pode especificar uma porta local diferente da 2375.
>

Agora pode aceder na cluster Docker Swarm Olá utilizando a interface de linha de comandos (CLI do Docker) do Olá Docker no sistema local. Para instruções de instalação, veja [Instalar Docker](https://docs.docker.com/engine/installation/).

Defina o toohello de variável de ambiente de DOCKER_HOST porta local configurado para túnel Olá. 

```bash
export DOCKER_HOST=:2375
```

Execute os comandos de Docker esse toohello túnel do cluster Docker Swarm. Por exemplo:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Criar um túnel SSH no Windows
Existem várias opções para criar túneis SSH no Windows. Se estiver a executar Bash no Ubuntu no Windows ou uma ferramenta semelhante, pode seguir as instruções de túnel de SSH de Olá mostradas anteriormente neste artigo para macOS e Linux. Como alternativa no Windows, esta secção descreve como túnel de Olá toouse PuTTY toocreate.

1. [Transfira o PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour sistema Windows.

2. Execute a aplicação Olá.

3. Introduza um nome de anfitrião que é composta por nome de utilizador de administrador de cluster Olá e o nome DNS público Olá Olá primeiro do mestre de no cluster de Olá. Olá **nome de anfitrião** semelhante demasiado`azureuser@PublicDNSName`. Introduza 2200 para Olá **porta**.

    ![Configuração do puTTY 1](./media/container-service-connect/putty1.png)

4. Selecione **SSH > Auth**. Adicione um caminho tooyour ficheiro de chave privada (*.ppk formato) para autenticação. Pode utilizar uma ferramenta como [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate este ficheiro de Olá cluster de Olá toocreate utilizadas chaves de SSH.

    ![Configuração do puTTY 2](./media/container-service-connect/putty2.png)

5. Selecione **SSH > túneis** e configure Olá seguintes portas reencaminhadas:

    * **Porta de Origem:** utilize a porta 80 para DC/OS ou a 2375 para Swarm.
    * **Destino:** utilize localhost:80 para DC/OS ou localhost:2375 para Swarm.

    Olá seguinte o exemplo está configurado para DC/OS, mas será semelhante para Docker Swarm.

    > [!NOTE]
    > A porta 80 não deve ser utilizada quando cria este túnel.
    > 

    ![Configuração do puTTY 3](./media/container-service-connect/putty3.png)

6. Quando tiver terminado, clique em **sessão > guardar** configuração da ligação toosave Olá.

7. tooconnect toohello sessão do PuTTY, clique em **abra**. Quando se liga, pode ver a configuração da porta no registo de eventos do PuTTY Olá Olá.

    ![Registo de eventos do puTTY](./media/container-service-connect/putty4.png)

Depois de ter configurado o túnel de Olá para DC/OS, pode aceder Olá relacionadas com pontos finais em:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Depois de ter configurado o túnel de Olá para Docker Swarm, abra o tooconfigure de definições do Windows uma variável de ambiente de sistema com o nome `DOCKER_HOST` com um valor de `:2375`. Em seguida, podem aceder cluster Swarm de Olá através de Olá CLI do Docker.

## <a name="next-steps"></a>Passos seguintes
Implementar e gerir contentores no seu cluster:

* [Trabalhar com o Azure Container Service e o Kubernetes](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Trabalhar com o Azure Container Service e o DC/OS](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Trabalhar com Olá serviço de contentor do Azure e Docker Swarm](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

