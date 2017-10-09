---
title: aaaHost um Ruby no Web site Rails de uma VM com Linux | Microsoft Docs
description: "Configurar e alojar um Ruby no Web site baseado em Rails no Azure através de uma máquina virtual Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Aplicação Web Ruby on Rails numa VM do Azure
Este tutorial mostra como toohost um Ruby no Web site de Rails no Azure através de uma máquina virtual Linux.  

Este tutorial foi validado utilizando Ubuntu Server 14.04 LTS. Se utilizar uma distribuição diferente do Linux, poderá ser necessário toomodify Olá passos tooinstall Rails.

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com os recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.
>
>

## <a name="create-an-azure-vm"></a>Criar uma VM do Azure
Comece por criar uma VM do Azure com uma imagem de Linux.

toocreate Olá VM, pode utilizar Olá portal do Azure ou Olá Interface de linha de comandos do Azure (CLI).

### <a name="azure-portal"></a>Portal do Azure
1. Inicie sessão em Olá [portal do Azure](https://portal.azure.com)
2. Clique em **novo**, em seguida, escreva "Ubuntu Server 14.04" na caixa de pesquisa de Olá. Clique em entrada Olá devolvida pela pesquisa de Olá. Olá modelo de implementação, selecione **clássico**, em seguida, clique em "Criar".
3. No painel de noções básicas de Olá, fornecer valores para os campos de Olá necessário: nome (para Olá VM), nome de utilizador, tipo de autenticação e credenciais correspondentes Olá, subscrição do Azure, grupo de recursos e localização.

   ![Criar uma nova imagem de Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Depois de Olá VM é aprovisionado, clique no nome da VM Olá e, em **pontos finais** no Olá **definições** categoria. Localizar o ponto final SSH Olá, listado na **autónomo**.

   ![Ponto final predefinido](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>CLI do Azure
Siga os passos Olá [criar com uma Máquina Virtual a executar Linux][vm-instructions].

Depois de Olá VM é aprovisionado, pode obter o ponto final de SSH Olá executando Olá os seguintes comandos:

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>Instalar Ruby Rails
1. Utilize o SSH tooconnect toohello VM.
2. A partir da sessão SSH Olá, utilize Olá os seguintes comandos tooinstall Ruby no Olá VM:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    instalação de Olá pode demorar alguns minutos. Quando estiver concluída, utilize Olá tooverify de comando que é instalado Ruby os seguintes:

        ruby -v

3. Seguinte Olá de utilização de comandos tooinstall Rails:

        sudo gem install rails --no-rdoc --no-ri -V

    Utilize Olá – não rdoc e – tooskip sinalizadores ri não instalar documentação de Olá, que é mais rápido.
    Este comando, provavelmente, irá demorar muito tempo tooexecute, para adicionar Olá -V irá apresentar informações sobre o progresso da instalação Olá.

## <a name="create-and-run-an-app"></a>Criar e executar uma aplicação
Enquanto continuam a ser registados através de SSH, execute Olá os seguintes comandos:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Olá [novo](http://guides.rubyonrails.org/command_line.html#rails-new) comando cria uma nova aplicação Rails. Olá [servidor](http://guides.rubyonrails.org/command_line.html#rails-server) comando inicia Olá servidor web WEBrick que vem com Rails. (Para utilização em produção, seria provavelmente pretende toouse um servidor diferente, tal como Unicorn ou Passenger.)

Deverá ver o seguinte de toohello semelhante de saída.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Adicionar um ponto final
1. Aceda toohello [portal do Azure] [https://portal.azure.com] e selecione a VM.

2. Selecione **pontos finais** no Olá **definições** ao longo da página de Olá Olá limite esquerdo.

3. Clique em **adicionar** em Olá parte superior da página Olá.

4. No Olá **adicionar ponto final** diálogo página, introduza Olá seguintes informações:

   * **Nome**: HTTP
   * **Protocolo**: TCP
   * **Porta pública**: 80
   * **Porta privada**: 3000
   * **Endereço de instalador de plataforma de vírgula flutuante**: desativado
   * **Lista de controlo de acesso - ordem**: 1001 ou outro valor que define a prioridade Olá desta regra de acesso.
   * **Lista de controlo de acesso - nome**: allowHTTP
   * **Lista de controlo de acesso - ação**: permitir
   * **Lista de controlo de acesso - sub-rede remota**: 1.0.0.0/16

     Este ponto final possui uma porta pública 80 que irá encaminhar tráfego toohello porta privada de 3000, onde servidor de Rails Olá está a escutar. regra de lista de controlo de acesso de Olá permite tráfego público na porta 80.

     ![novo ponto final](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Clique em OK toosave Olá endpoint.

6. Deve apresentada uma mensagem que indica **guardar ponto final de máquina virtual**. Assim que esta mensagem desaparece, o ponto final de Olá está ativa. Pode agora testar a aplicação ao navegar toohello o nome DNS da sua máquina virtual. Web site de Olá deve aparecer semelhante toohello seguinte:

    ![página de rails predefinida][default-rails-cloud]

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, fez a maior parte dos passos de Olá manualmente. Num ambiente de produção, teria de escrever a sua aplicação no computador de desenvolvimento e implementá-la toohello VM do Azure. Além disso, a maioria dos ambientes de produção alojam a aplicação de Rails de Olá juntamente com outro processo do servidor, tais como o Apache ou NginX, os identificadores de pedem de encaminhamento toomultiple instâncias da aplicação de Rails Olá e que serve recursos estáticos. Para obter mais informações, consulte http://rubyonrails.org/deploy/.

toolearn mais informações sobre Ruby no Rails, visite Olá [Ruby no Rails guias][rails-guides].

toouse serviços do Azure da sua aplicação Ruby, consulte:

* [Armazenar dados não estruturados com blobs][blobs]
* [Pares chave/valor de arquivo com tabelas][tables]
* [Servir conteúdo de largura de banda alta com Olá rede de entrega de conteúdo][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
