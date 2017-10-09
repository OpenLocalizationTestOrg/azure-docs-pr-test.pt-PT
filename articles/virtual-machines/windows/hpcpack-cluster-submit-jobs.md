---
title: cluster aaaSubmit tarefas tooan pacote HPC no Azure | Microsoft Docs
description: "Saiba como tooset um toosubmit de computador no local de cópia de segurança das tarefas de cluster HPC Pack de tooan no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Submeter tarefas HPC de um cluster HPC Pack do local no computador tooan implementado no Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Configurar um local no cliente computador toosubmit tarefas tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster no Azure. Este artigo mostra como tooset cópias de segurança num computador local com o cliente ferramentas toosubmit tarefa através de cluster toohello HTTPS no Azure. Desta forma, vários utilizadores do cluster podem submeter tarefas tooa baseado na nuvem HPC Pack cluster, mas sem ligar diretamente o nó principal do toohello VM ou aceder a uma subscrição do Azure.

![Submeter um cluster de tooa tarefa no Azure][jobsubmit]

## <a name="prerequisites"></a>Pré-requisitos
* **Nó principal HPC Pack implementado na VM do Azure** -é recomendável que utilize ferramentas automatizadas, tais como um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) ou um [script do PowerShell do Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) nó principal do toodeploy Olá e cluster. Precisará de nome DNS de Olá do nó principal Olá e Olá as credenciais de um administrador de cluster para concluir os passos de Olá neste artigo.
* **Computador cliente** -necessita de um computador cliente Windows ou Windows Server que pode executar utilitários de cliente de HPC Pack (consulte [requisitos de sistema](https://technet.microsoft.com/library/dn535781.aspx)). Se pretender que apenas portal web do toouse Olá HPC Pack ou as tarefas de toosubmit de REST API, pode utilizar qualquer computador cliente à sua escolha.
* **Suporte de instalação do HPC Pack** -tooinstall Olá utilitários de cliente de HPC Pack, o pacote de instalação livre de Olá para a versão mais recente do HPC Pack (pacote HPC 2012 R2) está disponível a partir do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Certifique-se de que transfira Olá mesma versão do pacote HPC que está instalado no nó principal do Olá VM.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Passo 1: Instalar e configurar componentes do web Olá no nó principal Olá
tooenable REST interface toosubmit tarefas toohello cluster através de HTTPS, certifique-se de que os componentes da web HPC Pack Olá são configurados no nó principal do Olá HPC Pack. Se ainda não estiverem instalados, primeiro de instalar os componentes web do Olá executando o ficheiro de instalação de HpcWebComponents.msi Olá. Em seguida, configure os componentes de Olá executando o script de HPC PowerShell Olá **conjunto HPCWebComponents.ps1**.

Para obter procedimentos detalhados, consulte [instalar Olá Microsoft HPC Pack Web componentes](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Determinados modelos de início rápido do Azure para HPC Pack instalar e configurar componentes do web Olá automaticamente. Se utilizar Olá [script de implementação de HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate cluster de Olá, opcionalmente, pode instalar e configurar componentes do web Olá como parte da implementação de Olá.
> 
> 

**componentes do tooinstall Olá web**

1. Liga o nó principal do toohello VM utilizando Olá credenciais de um administrador de cluster.
2. A partir da pasta de configuração de pacote HPC Olá, execute HpcWebComponents.msi no nó principal Olá.
3. Siga os passos de Olá Olá assistente tooinstall Olá hospeda componentes da web

**componentes do tooconfigure Olá web**

1. No nó principal Olá, inicie o HPC PowerShell como administrador.
2. localização de toohello do diretório toochange de script de configuração de Olá, Olá tipo os seguintes comandos:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure Olá REST interface e iniciar Olá serviço Web de HPC, Olá tipo os seguintes comandos:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Quando tooselect pedido um certificado, escolha o certificado de Olá que corresponde ao nome DNS público toohello de nó principal Olá. Por exemplo, se implementar nó principal Olá VM utilizando o modelo de implementação clássica Olá, nome do certificado Olá aspeto CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Se utilizar o modelo de implementação do Resource Manager Olá, o nome do certificado Olá aspeto CN =&lt;*HeadNodeDnsName*&gt;.&lt; *região*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Selecionar este certificado mais tarde ao submeter o nó principal do toohello de tarefas de um computador local. Não selecione ou configurar um certificado que corresponde ao nome do computador toohello do nó principal do Olá num domínio do Active Directory Olá (por exemplo, CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. portal de web de Olá tooconfigure para submissão da tarefa, Olá tipo os seguintes comandos:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Após a conclusão do script Olá, pare e reinicie Olá, o serviço de agendador de tarefas HPC, escrevendo Olá os seguintes comandos:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Passo 2: Instalar utilitários de cliente de HPC Pack Olá num computador local
Se quiser utilitários de cliente do tooinstall Olá HPC Pack no seu computador, transferir os ficheiros de configuração de HPC Pack (instalação completa) da Olá [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Quando iniciar a instalação de Olá, escolha a opção de configuração de Olá para Olá **utilitários de cliente de HPC Pack**.

nó principal do toosubmit tarefas toohello VM das ferramentas de cliente de HPC Pack toouse Olá, também tem de tooexport um certificado do nó principal Olá e instalá-lo no computador de cliente Olá. certificado de Olá tem de estar no. Formato CER.

**certificado de Olá tooexport do nó principal Olá**

1. No nó principal Olá, adicione Olá certificados snap-in tooa consola de gestão da Microsoft para Olá conta de computador Local. Para obter passos tooadd Olá snap-in, consulte [adicionar Olá Snap-in Certificados tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).
2. Na árvore da consola de Olá, expanda **certificados-Computador Local** > **pessoais**e, em seguida, clique em **certificados**.
3. Localizar certificados Olá que configurou para Olá HPC Pack web componentes [passo 1: instalar e configurar componentes do web Olá no nó principal Olá](#step-1:-install-and-configure-the-web-components-on-the-head-node) (por exemplo, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).
4. Faça duplo clique Olá certificado e clique em **todas as tarefas** > **exportar**.
5. No Assistente para exportar certificados Olá, clique em **seguinte**e certifique-se de que **não exportar chave privada Olá** está selecionada.
6. Olá siga restantes passos Olá assistente tooexport Olá do certificado de no DER x. 509 binário de codificado (. Formato CER).

**certificado de Olá tooimport no computador de cliente Olá**

1. Copie o certificado de Olá que exportou a partir da pasta de tooa Olá nó principal no computador de cliente Olá.
2. No computador de cliente Olá, execute certmgr.msc.
3. No Gestor de certificados, expanda **certificados-utilizador atual** > **autoridades de certificação de raiz fidedigna**, faça duplo clique **certificados**e, em seguida, Clique em **todas as tarefas** > **importação**.
4. No Assistente para importar certificados Olá, clique em **seguinte** e siga Olá passos tooimport Olá certificado que exportou do Olá nó principal toohello arquivo de autoridades de certificação de raiz fidedigna.

> [!TIP]
> Poderá ver um aviso de segurança, porque a autoridade de certificação de Olá no nó principal Olá não é reconhecida pelo computador de cliente Olá. Para fins de teste, pode ignorar esta importação de certificados de Olá aviso e concluída.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Passo 3: Executar tarefas de teste no cluster de Olá
tooverify a configuração, tente tarefas em execução no Olá cluster no Azure de Olá no local do computador. Por exemplo, pode utilizar ferramentas de HPC Pack GUI ou cluster de toohello comandos da linha de comandos toosubmit tarefas. Também pode utilizar um tarefas baseada na web toosubmit portal.

**comandos de submissão de tarefa toorun no computador de cliente Olá**

1. Num computador cliente onde estão instalados os utilitários de cliente de HPC Pack Olá, inicie uma linha de comandos.
2. Escreva um comando de exemplo. Por exemplo, toolist todas as tarefas no cluster de Olá, escreva um tooone semelhante do comando de Olá seguintes, dependendo do nome DNS completo Olá de nó principal Olá:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    ou
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Utilize Olá nome DNS completo de nó principal do Olá, não Olá endereço IP, no URL de programador Olá. Se especificar o endereço IP Olá, aparece um erro semelhante demasiado "necessita de certificado de servidor Olá tooeither tem uma cadeia válida de confiança ou toobe colocados no arquivo de raiz fidedigna Olá."
   > 
   > 
3. Quando lhe for pedido, escreva o nome de utilizador de Olá (formato Olá &lt;DomainName&gt;\\&lt;UserName&gt;) e palavra-passe de administrador de clusters HPC Olá ou outro utilizador de cluster que configurou. Pode escolher toostore credenciais Olá localmente para mais operações de tarefa.
   
    É apresentada uma lista de tarefas.

**toouse Gestor de tarefas HPC no computador de cliente Olá**

1. Se não armazenar as credenciais do domínio para um utilizador de cluster anteriormente quando submete uma tarefa, pode adicionar credenciais Olá no Gestor de credenciais.
   
    a. No painel de controlo do computador de cliente Olá, inicie o Gestor de credenciais.
   
    b. Clique em **credenciais do Windows** > **adicionar uma credencial genérica**.
   
    c. Especifique o endereço do Internet Olá (por exemplo, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler ou https://&lt;HeadNodeDnsName&gt;.&lt; região&gt;.cloudapp.azure.com/HpcScheduler) e o nome de utilizador Olá (&lt;DomainName&gt;\\&lt;UserName&gt;) e palavra-passe de administrador do cluster Olá ou outro utilizador de cluster que configurou.
2. No computador de cliente Olá, inicie o Gestor de tarefas HPC.
3. No Olá **selecionar nó Head** caixa de diálogo, tipo Olá URL toohello nó principal no Azure (por exemplo, https://&lt;HeadNodeDnsName&gt;. cloudapp.net ou https://&lt;HeadNodeDnsName&gt;. &lt;região&gt;. cloudapp.azure.com).
   
    Gestor de tarefas HPC abre-se e mostra uma lista de tarefas no nó principal Olá.

**portal de web toouse Olá em execução no nó principal Olá**

1. Iniciar um browser no computador de cliente Olá e introduza um dos Olá endereços, dependendo do nome DNS completo Olá de nó principal Olá os seguintes:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    ou
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. Na Olá segurança caixa de diálogo que aparece, escreva as credenciais do domínio Olá de administrador de clusters HPC Olá. (Também pode adicionar outros utilizadores de cluster em diferentes funções. Consulte [gestão de utilizadores de Cluster](https://technet.microsoft.com/library/ff919335.aspx).)
   
    portal de web de Olá abre toohello vista de lista de tarefas.
3. Clique em toosubmit uma tarefa de exemplo que devolve a cadeia de Olá "Olá mundo" do cluster de Olá, **nova tarefa** na navegação esquerda Olá.
4. No Olá **nova tarefa** página **de páginas de submissão**, clique em **Olámundo**. é apresentada a página de submissão de tarefa Olá.
5. Clique em **submeter**. Se lhe for solicitado, forneça as credenciais do domínio Olá de administrador de clusters HPC Olá. Olá trabalho é submetido e Olá ID da tarefa é apresentado no Olá **tarefas My** página.
6. resultados de Olá tooview da tarefa de Olá submetido, clique Olá ID da tarefa e, em seguida, clique em **tarefas vista** saída do comando de Olá tooview (em **saída**).

## <a name="next-steps"></a>Passos seguintes
* Também pode submeter tarefas toohello cluster do Azure com Olá [API de REST do HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Se pretender que as tarefas do cluster toosubmit de um cliente Linux, consulte Olá Python exemplo no Olá [SDK do HPC Pack 2012 R2 e o código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
