---
title: aaaCreate um pipeline de desenvolvimento no Azure com Jenkins | Microsoft Docs
description: "Saiba como toocreate um Jenkins virtual máquina no Azure que obtém a partir do GitHub em cada código consolidar e cria um novo Docker toorun de contentor, a aplicação"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a>Como toocreate uma infraestrutura de desenvolvimento de uma VM com Linux no Azure com Jenkins, GitHub e Docker
tooautomate Olá compilação e testar a fase de desenvolvimento de aplicações, pode utilizar uma integração contínua e o pipeline de implementação (CI/CD). Neste tutorial, vai criar um pipeline de CI/CD numa VM do Azure incluindo como:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Instalar e configurar Jenkins
> * Criar o webhook integração entre o GitHub e Jenkins
> * Criar e consolida acionador que jenkins criar tarefas a partir do GitHub
> * Criar uma imagem de Docker para a sua aplicação
> * Certifique-se de consolidações de GitHub criem nova imagem do Docker e executar a aplicação de atualizações


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-jenkins-instance"></a>Criar uma instância de Jenkins
Um tutorial anterior em [como toocustomize uma máquina virtual do Linux no primeiro arranque](tutorial-automate-vm-deployment.md), que aprendeu como tooautomate personalização de VM com init de nuvem. Este tutorial utiliza um ficheiro de nuvem init tooinstall Jenkins e Docker numa VM. 

Na sua shell atual, crie um ficheiro denominado *nuvem init.txt* e colar Olá seguindo a configuração. Por exemplo, crie o ficheiro de Olá no Olá Shell na nuvem não no seu computador local. Introduza `sensible-editor cloud-init-jenkins.txt` toocreate Olá ficheiro e ver uma lista de editores disponíveis. Certifique-se de que o ficheiro init de nuvem todo Olá foi corretamente copiado, Olá especialmente a primeira linha:

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

Antes de poder criar uma VM, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create). Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupJenkins* no Olá *eastus* localização:

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

Agora criar uma VM com [az vm criar](/cli/azure/vm#create). Olá utilize `--custom-data` toopass de parâmetro no seu ficheiro de configuração de nuvem init. Forneça o caminho completo do Olá demasiado*nuvem-init-jenkins.txt* se tiver guardado o ficheiro de Olá fora do diretório de trabalho presente.

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

Demora alguns minutos para Olá VM toobe criada e configurada.

tooallow web tráfego tooreach a VM, utilize [az vm open-porta](/cli/azure/vm#open-port) tooopen porta *8080* Jenkins para tráfego de e porta *1337* para aplicação Node.js Olá que é utilizado toorun uma aplicação de exemplo:

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a>Configurar Jenkins
tooaccess sua Jenkins instância, obtenha o endereço IP público Olá da sua VM:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Por motivos de segurança, terá de tooenter Olá administrador inicial palavra-passe que é armazenado num ficheiro de texto no seu Olá de toostart VM que jenkins instalar. Utilize o endereço IP público Olá obtido no Olá anterior passo tooSSH tooyour VM:

```bash
ssh azureuser@<publicIps>
```

Olá vista `initialAdminPassword` para sua Jenkins instalar e copie-o:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Se o ficheiro de Olá ainda não está disponível, aguarde alguns minutos para a nuvem init toocomplete Olá Jenkins e instalação de Docker.

Agora abra um browser e aceda demasiado`http://<publicIps>:8080`. Conclua a configuração Jenkins Olá inicial da seguinte forma:

- Introduza Olá *initialAdminPassword* obtida Olá VM no passo anterior Olá.
- Clique em **selecione tooinstall de plug-ins**
- Procurar *GitHub* na caixa de texto de Olá na parte superior do Olá, selecione Olá *Plug-in do GitHub*, em seguida, clique em **instalar**
- toocreate uma conta de utilizador Jenkins, preencha o formulário de Olá conforme pretendido. Numa perspetiva de segurança, deve criar este primeiro utilizador Jenkins em vez de os continuar como conta de administrador predefinida Olá.
- Quando terminar, clique em **começar a utilizar Jenkins**


## <a name="create-github-webhook"></a>Criar o GitHub webhook
integração de Olá tooconfigure com o GitHub, abra Olá [aplicação de exemplo de Olá, mundo Node.js](https://github.com/Azure-Samples/nodejs-docs-hello-world) do repositório do Olá exemplos do Azure. toofork Olá repositório tooyour ser proprietário da conta do GitHub, clique em Olá **bifurcação** botão no canto superior direito Olá.

Crie um webhook no interior de bifurcação de Olá que criou:

- Clique em **definições**, em seguida, selecione **integrações & serviços** no lado esquerdo Olá.
- Clique em **Adicionar serviço**, em seguida, introduza *Jenkins* na caixa Filtro.
- Selecione *Jenkins (GitHub Plug-in)*
- Para Olá **Jenkins ligue URL**, introduza `http://<publicIps>:8080/github-webhook/`. Certifique-se de que incluem Olá à direita /
- Clique em **Adicionar serviço**

![Adicione o repositório do GitHub webhook tooyour escolhido](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a>Criar tarefa de Jenkins
toohave Jenkins respondeu tooan eventos no GitHub, tais como consolidar o código, criar uma tarefa de Jenkins. 

No seu Web site Jenkins, clique em **criar novas tarefas** da home page do Olá:

- Introduza *Olámundo* como o nome da tarefa. Escolha **projeto Freestyle**, em seguida, selecione **OK**.
- Em Olá **geral** secção, selecione **GitHub** projeto e introduza o URL do repositório escolhido, tais como *https://github.com/iainfoulds/nodejs-docs-hello-world*
- Em Olá **gestão de código de origem** secção, selecione **Git**, introduza o seu repositório forked *.git* URL, tais como *https://github.com/iainfoulds/nodejs-docs-hello-world.git*
- Em Olá **criar Acionadores** secção, selecione **acionador de rotina do GitHub para consulta GITscm**.
- Em Olá **criar** secção, escolha **Adicionar passo de compilação**. Selecione **executar shell**, em seguida, introduza `echo "Testing"` na janela toocommand.
- Clique em **guardar** em Olá parte inferior da janela de tarefas Olá.


## <a name="test-github-integration"></a>Integração do GitHub de teste
Olá tootest integração do GitHub com Jenkins, consolidar uma alteração na sua bifurcação. 

No GitHub da IU da web, selecione o seu repositório forked e, em seguida, clique em Olá **index.js** ficheiro. Clique em tooedit de ícone de lápis Olá este ficheiro para a linha 6 lê:

```nodejs
response.end("Hello World!");
```

toocommit as suas alterações, clique em Olá **consolidar alterações** botão na parte inferior de Olá.

No Jenkins, uma nova compilação é iniciado em Olá **criar histórico** secção do canto de esquerdo Olá inferior da sua página de tarefa. Clique em ligação de número de compilação de Olá e selecione **consola saída** no tamanho da esquerda Olá. Pode ver os passos de Olá Jenkins demora como o seu código é retirado da GitHub e Olá mensagem de saudação do saídas ação de compilação `Testing` toohello consola. Sempre que uma consolidação é efetuada no GitHub webhook Olá acede tooJenkins e acionar uma nova compilação desta forma.


## <a name="define-docker-build-image"></a>Definir imagem de compilação do Docker
toosee Olá Node.js aplicação em execução com base no seu consolidações do GitHub, permite criar um Docker imagem toorun Olá aplicação. imagem de Olá é criada a partir de um Dockerfile que define a forma como tooconfigure Olá contentor que executa a aplicação Olá. 

Olá SSH ligação tooyour VM, altere o diretório de área de trabalho de Jenkins de toohello chamado após a tarefa de Olá que criou no passo anterior. No nosso exemplo, que foi atribuído o nome *Olámundo*.

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

Criar um ficheiro com neste diretório de área de trabalho com `sudo sensible-editor Dockerfile` e colar Olá seguir o conteúdo. Certifique-se de que Olá que dockerfile todo é copiados corretamente, especialmente Olá primeira linha:

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

Este Dockerfile utiliza Olá imagem base do Node.js com Linux Extreme, porta expõe 1337 Olá mundo Olá aplicação é executado em, em seguida, copia os ficheiros de aplicação Olá e inicializa-lo.


## <a name="create-jenkins-build-rules"></a>Criar regras de compilação Jenkins
No passo anterior, criou uma regra de compilação Jenkins básica que uma consola de toohello de mensagem de saída. Permite criar Olá compilação passo toouse nosso Dockerfile e executar a aplicação de Olá.

Novamente na instância Jenkins, selecione a tarefa de Olá que criou no passo anterior. Clique em **configurar** no lado esquerdo Olá e desloque para baixo toohello **criar** secção:

- Remover existentes `echo "Test"` passo de compilação. Clique em Olá vermelho cruzada na Olá canto superior direito da caixa de passo de compilação Olá existente.
- Clique em **Adicionar passo de compilação**, em seguida, selecione **executar shell**
- No Olá **comando** caixa, introduza Olá os seguintes comandos do Docker, em seguida, selecione **guardar**:

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

passos de compilação do Docker Olá criar uma imagem e a etiqueta com Olá Jenkins número de compilação para pode manter um histórico de imagens. Quaisquer contentores existentes a executar a aplicação Olá são parados e, em seguida, são removidas. Um novo contentor é iniciado utilizando a imagem de Olá e executa a aplicação Node.js com base no consolidações mais recentes do Olá no GitHub.


## <a name="test-your-pipeline"></a>Testar o pipeline
pipeline de todo Olá toosee em ação, editar Olá *index.js* ficheiros no seu repositório do GitHub forked novamente e clique em **Confirmar alteração**. Inicia uma nova tarefa em Jenkins com base nos Olá webhook GitHub. Este demora alguns segundos a imagem de Docker toocreate Olá e iniciar a sua aplicação num contentor de novo.

Se for necessário, obter novamente o endereço IP público Olá da sua VM:

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

Abra um browser e introduza `http://<publicIps>:1337`. A aplicação Node.js é apresentada e reflete consolidações mais recentes do Olá no seu bifurcação de GitHub da seguinte forma:

![Aplicação Node.js em execução](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

Agora a efetuar outra edição toohello *index.js* ficheiro no GitHub e Confirmar alteração Olá. Aguarde alguns segundos para Olá tarefa toocomplete no Jenkins, em seguida, atualize a sua versão do web browser toosee Olá atualizada da sua aplicação em execução num novo contentor da seguinte forma:

![Aplicação Node.js em execução depois de outra consolidação do GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a>Passos seguintes
Neste tutorial, configurou GitHub toorun uma tarefa de compilação Jenkins em cada consolidação de código e, em seguida, implementar a aplicação de um tootest de contentor do Docker. Aprendeu a:

> [!div class="checklist"]
> * Criar uma VM Jenkins
> * Instalar e configurar Jenkins
> * Criar o webhook integração entre o GitHub e Jenkins
> * Criar e consolida acionador que jenkins criar tarefas a partir do GitHub
> * Criar uma imagem de Docker para a sua aplicação
> * Certifique-se de consolidações de GitHub criem nova imagem do Docker e executar a aplicação de atualizações

Avançar toolearn tutorial seguinte de toohello mais informações sobre como toointegrate Jenkins com o Visual Studio Team Services.

> [!div class="nextstepaction"]
> [Implementar aplicações com Jenkins e serviços da equipa](tutorial-build-deploy-jenkins.md)