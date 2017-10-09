---
title: aaaInstall MongoDB numa VM do Windows no Azure | Microsoft Docs
description: "Saiba como tooinstall MongoDB numa VM do Azure com o Windows Server 2012 R2 criados com o modelo de implementação do Resource Manager Olá."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Instalar e configurar o MongoDB uma VM do Windows no Azure
[MongoDB](http://www.mongodb.org) é um popular open source e de elevado desempenho base de dados NoSQL. Este artigo irá orientá-lo a instalar e configurar o MongoDB numa máquina virtual (VM) do Windows Server 2012 R2 no Azure. Também pode [instalar MongoDB numa VM com Linux no Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Pré-requisitos
Antes de instalar e configurar o MongoDB, necessário toocreate uma VM e, idealmente, adicione um tooit de disco de dados. Consulte os seguintes artigos toocreate uma VM de Olá e adicione um disco de dados:

* Criar uma VM do Windows Server utilizando [Olá portal do Azure](quick-create-portal.md) ou [Azure PowerShell](quick-create-powershell.md).
* Anexar um dados disco tooa VM do Windows Server utilizando [Olá portal do Azure](attach-managed-disk-portal.md) ou [Azure PowerShell](attach-disk-ps.md).

toobegin instalar e configurar o MongoDB, [iniciar sessão tooyour VM do Windows Server](connect-logon.md) utilizando o ambiente de trabalho remoto.

## <a name="install-mongodb"></a>Instalar MongoDB
> [!IMPORTANT]
> Funcionalidades de segurança do MongoDB, como a autenticação e o enlace de endereço IP, não estão ativadas por predefinição. Funcionalidades de segurança devem ser ativadas antes de implementar o ambiente de produção do MongoDB tooa. Para obter mais informações, consulte [autenticação e de segurança do MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).


1. Depois de se ligar tooyour VM utilizando o ambiente de trabalho remoto, abra o Internet Explorer de Olá **iniciar** menu Olá VM.
2. Selecione **utilizar definições de segurança, privacidade e compatibilidade recomendadas** quando o Internet Explorer primeiro abre e clique em **OK**.
3. Configuração de segurança avançada do Internet Explorer está ativada por predefinição. Adicione a lista de toohello do Olá MongoDB Web site de sites autorizados:
   
   * Selecione Olá **ferramentas** ícone no canto superior direito de Olá.
   * No **opções da Internet**, selecione Olá **segurança** separador e, em seguida, selecione Olá **Sites fidedignos** ícone.
   * Clique em Olá **Sites** botão. Adicionar *https://\*. mongodb.org* toohello lista de sites fidedignos e a caixa de diálogo Olá, em seguida, feche.
     
     ![Configurar definições de segurança do Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. Procurar toohello [MongoDB - transfere](http://www.mongodb.org/downloads) página (http://www.mongodb.org/downloads).
5. Se necessário, selecione Olá **Comunidade servidor** edition e, em seguida, selecione de Olá mais recente estável versão atual para o Windows Server 2008 R2 de 64 bits e posterior. toodownload Olá instalador, clique em **transferências (msi)**.
   
    ![Transferir o instalador do MongoDB](./media/install-mongodb/download-mongodb.png)
   
    Execute o instalador do Olá depois de concluída a transferência de Olá.
6. Ler e aceitar o contrato de licença de Olá. Quando lhe for pedido, selecione **concluída** instalar.
7. No ecrã final Olá, clique em **instalar**.

## <a name="configure-hello-vm-and-mongodb"></a>Configurar Olá VM e MongoDB
1. as variáveis de caminho Olá não são atualizadas pelo programa de instalação do Olá MongoDB. Sem Olá MongoDB `bin` localização na sua variável de caminho, terá de caminho completo do toospecify Olá sempre que utilizar um executável do MongoDB. variável de caminho do tooadd Olá localização tooyour:
   
   * Contexto Olá **iniciar** menu e selecione **sistema**.
   * Clique em **definições de sistema avançadas**e, em seguida, clique em **variáveis de ambiente**.
   * Em **variáveis do sistema**, selecione **caminho**e, em seguida, clique em **editar**.
     
     ![Configurar variáveis de caminho](./media/install-mongodb/configure-path-variables.png)
     
     Adicionar Olá caminho tooyour MongoDB `bin` pasta. MongoDB é normalmente instalado na *c:\Programas\Microsoft Files\MongoDB*. Verifique o caminho de instalação de Olá no VM. Olá exemplo seguinte adiciona toohello de localização de instalação do Olá predefinido MongoDB `PATH` variável:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Ser se tooadd Olá à esquerda ponto e vírgula (`;`) tooindicate que estiver a adicionar um tooyour localização `PATH` variável.

2. Crie diretórios de dados e de registo do MongoDB no seu disco de dados. De Olá **iniciar** menu, selecione **linha de comandos**. os seguintes exemplos de Olá criar diretórios Olá no disco f:
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Iniciar uma instância do MongoDB com Olá comando a seguir, ajuste os dados de tooyour Olá caminho e inicie diretórios em conformidade:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Pode demorar alguns minutos para MongoDB tooallocate ficheiros do diário Olá e começar a escutar ligações. Todas as mensagens de registo são direcionado toohello *F:\MongoLogs\mongolog.log* ficheiro como `mongod.exe` servidor é iniciado e atribui ficheiros do diário.
   
   > [!NOTE]
   > linha de comandos Olá permanece direcionada para esta tarefa enquanto a instância do MongoDB está em execução. Deixe Olá linha de comandos janela abra toocontinue com MongoDB. Em alternativa, instale o MongoDB como serviço, conforme detalhado no passo seguinte Olá.

4. Para uma experiência mais robusta do MongoDB, instalar Olá `mongod.exe` como um serviço. Criação de um serviço significa que não precisa de tooleave numa linha de comandos executar sempre que quiser toouse MongoDB. Crie serviço Olá forma, ajustar Olá caminho tooyour dados e registo de diretórios em conformidade:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Olá comando anterior cria um serviço com o nome MongoDB, com uma descrição do "BD de Mongo". também está especificado Olá os seguintes parâmetros:
   
   * Olá `--dbpath` opção especifica a localização de Olá do diretório de dados de Olá.
   * Olá `--logpath` opção tem de ser toospecify utilizado um ficheiro de registo, porque o serviço em execução Olá não tem uma saída de toodisplay de janela de comando.
   * Olá `--logappend` opção especifica que um reinício do serviço de Olá provoca o ficheiro de registo saída tooappend toohello existente.
   
   toostart Olá MongoDB serviço, executar Olá os seguintes comandos:
   
    ```
    net start MongoDB
    ```
   
    Para obter mais informações sobre como criar o serviço de MongoDB Olá, consulte [configurar um serviço do Windows para o MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Instância do MongoDB de Olá de teste
Com o MongoDB em execução como uma única instância ou instalado como um serviço, pode agora começar a criar e utilizar as bases de dados. Olá toostart shell administrativa do MongoDB, abrir outra janela de linha de comandos de Olá **iniciar** menu e introduza Olá os seguintes comandos:

```
mongo  
```

Pode listar as bases de dados de Olá com Olá `db` comando. Insira alguns dados da seguinte forma:

```
db.foo.insert( { a : 1 } )
```

Procure dados da seguinte forma:

```
db.foo.find()
```

Olá de saída é semelhante toohello seguinte exemplo:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Olá saída `mongo` consola da seguinte forma:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Configurar regras de grupo de segurança de rede e de firewall
Agora que MongoDB está instalado e em execução, abra uma porta na Firewall do Windows, pelo que pode ligar remotamente tooMongoDB. toocreate uma nova regra de entrada tooallow a porta TCP 27017, abra uma linha de comandos administrativa do PowerShell e introduza Olá os seguintes comandos:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

Também pode criar regra de Olá utilizando Olá **Firewall do Windows com segurança avançada** ferramenta de gestão gráficas. Crie uma nova regra de entrada tooallow a porta TCP 27017.

Se necessário, crie um grupo de segurança de rede regra tooallow acesso tooMongoDB de fora da sub-rede de rede virtual do Azure existente Olá. Olá pode criar regras do grupo de segurança de rede utilizando Olá [portal do Azure](nsg-quickstart-portal.md) ou [Azure PowerShell](nsg-quickstart-powershell.md). Tal como acontece com as regras de Firewall do Windows hello, permita a interface de rede virtual do TCP porta 27017 toohello da sua VM do MongoDB.

> [!NOTE]
> A porta TCP 27017 é Olá predefinido porta é utilizada por MongoDB. Pode alterar esta porta utilizando Olá `--port` parâmetro ao iniciar `mongod.exe` manualmente ou a partir de um serviço. Se alterar a porta de Olá, certifique-se tooupdate Olá Firewall do Windows e o grupo de segurança de rede regras no Olá precedente passos.


## <a name="next-steps"></a>Passos seguintes
Neste tutorial, aprendeu como tooinstall e configurar o MongoDB na sua VM do Windows. Pode agora aceder MongoDB na sua VM do Windows, por seguir Olá avançadas tópicos Olá [documentação do MongoDB](https://docs.mongodb.com/manual/).

