---
title: "aaaHow toouse Olá multisservidor Azure Plug-in com a integração contínua Hudson | Microsoft Docs"
description: "Descreve como toouse Olá Azure multisservidor Plug-in com a integração contínua Hudson."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>Como toouse Olá Azure multisservidor Plug-in com a integração contínua Hudson
Olá, Azure multisservidor Plug-in para Hudson permite-lhe nós de multisservidor tooprovision no Azure quando em execução distribuída baseia-se.

## <a name="install-hello-azure-slave-plug-in"></a>Instalar Olá Azure multisservidor Plug-in
1. No dashboard de Hudson Olá, clique em **gerir Hudson**.
2. No Olá **gerir Hudson** página, clique em **gerir plug-ins**.
3. Clique em Olá **disponível** separador.
4. Clique em **pesquisa** e tipo **Azure** toolimit Olá lista toorelevant plug-ins.
   
    Se optar por tooscroll através da lista de Olá de plug-ins disponíveis, encontrará Olá multisservidor Azure Plug-in em Olá **distribuídas compilar e gestão de clusters** secção Olá **outros** separador.
5. Selecione a caixa de verificação Olá para **Plug-in do Azure multisservidor**.
6. Clique em **Instalar**.
7. Reinicie Hudson.

Agora que Olá Plug-in estiver instalado, passos Olá seria tooconfigure Olá Plug-in com o perfil de subscrição do Azure e toocreate um modelo que será utilizado na criação de Olá VM para o nó de multisservidor Olá.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>Configurar Olá Azure multisservidor Plug-in com o seu perfil de subscrição
Um perfil de subscrição, também referidos tooas definições de publicação, é um ficheiro XML que contém as credenciais seguras e algumas informações adicionais, terá de toowork com o Azure no seu ambiente de desenvolvimento. Olá tooconfigure multisservidor Azure Plug-in, tem de:

* O id de subscrição
* Um certificado de gestão para a sua subscrição

Pode encontrá-las no seu [perfil subscrição]. Segue-se um exemplo de um perfil de subscrição.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

Assim que tiver o seu perfil de subscrição, siga estas Olá tooconfigure de passos do Azure multisservidor Plug-in.

1. No dashboard de Hudson Olá, clique em **gerir Hudson**.
2. Clique em **Configurar sistema**.
3. Desloque para baixo Olá de toofind de página Olá **nuvem** secção.
4. Clique em **Adicionar nova nuvem > Microsoft Azure**.
   
    ![Adicionar nova na nuvem][add new cloud]
   
    Isto irá mostrar campos olá onde terá tooenter detalhes da sua subscrição.
   
    ![configurar o perfil][configure profile]
5. Copie o certificado de gestão e o id de subscrição de Olá do seu perfil de subscrição e cole-os em campos apropriados Olá.
   
    Quando copiar Olá id e a gestão de certificado de subscrição, **não** incluir as aspas Olá que coloque os valores de Olá.
6. Clique em **verifique configuração**.
7. Quando a configuração de Olá é verificada com êxito, clique em **guardar**.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>Configurar o plug-in modelo de máquina virtual para Olá multisservidor do Azure
Um modelo de máquina virtual define os parâmetros de Olá Olá Plug-in utilizará toocreate um nó subordinado no Azure. No Olá os passos seguintes, irá ser criar modelo para uma VM com Ubuntu.

1. No dashboard de Hudson Olá, clique em **gerir Hudson**.
2. Clique em **Configurar sistema**.
3. Desloque para baixo Olá de toofind de página Olá **nuvem** secção.
4. Dentro do Olá **nuvem** secção, localizar **adicionar modelo de Máquina Virtual do Azure** e clique em Olá **adicionar** botão.
   
    ![Adicionar modelo de vm][add vm template]
5. Especifique um nome de serviço em nuvem no Olá **nome** campo. Se o nome de Olá especificado refere-se tooan existente serviço em nuvem, será aprovisionado Olá VM em que o serviço. Caso contrário, o Azure irá criar um novo.
6. No Olá **Descrição** campo, introduza o texto que descreve o modelo de Olá estiver a criar. Estas informações são apenas para fins de documentary e não são utilizadas no aprovisionamento de uma VM.
7. No Olá **etiquetas** campo, introduza **linux**. Esta etiqueta tooidentify utilizados Olá modelo que está a criar e é o modelo de Olá tooreference posteriormente utilizado ao criar uma tarefa de Hudson.
8. Selecione uma região onde será criada Olá VM.
9. Selecione o tamanho da VM Olá adequado.
10. Especifique uma conta de armazenamento onde Olá VM será criada. Certifique-se de que está a ser Olá mesma região que o serviço de nuvem Olá que irá utilizar. Se pretender que o novo armazenamento toobe, criado, pode deixar este campo em branco.
11. Período de retenção Especifica o número de Olá de minutos antes de Hudson elimina um subordinado de inatividade. Deixe este valor predefinido Olá 60.
12. No **utilização**, selecione Olá condição apropriada quando este nó subordinado será utilizado. Por agora, selecione **utilizar este nó quanto possível**.
    
     Neste momento, o formulário seria ter um aspeto toothis um pouco semelhante:
    
     ![configuração de modelo][template config]
13. No **família de imagem ou Id** tiver toospecify que imagem do sistema será instalada na VM. Pode selecionar numa lista de famílias de imagem ou especificar uma imagem personalizada.
    
     Se quiser tooselect de uma lista de famílias de imagem, introduza Olá primeiro caráter (maiúsculas e minúsculas) do nome de família Olá imagem. Por exemplo, escrevendo **U** será apresentada uma lista de famílias de Ubuntu Server. Depois de selecionar a partir da lista de Olá, Jenkins irá utilizar Olá versão mais recente dessa imagem de sistema de que família quando aprovisionar a VM.
    
     ![Lista de família do SO][OS family list]
    
     Se tiver uma imagem personalizada que pretende que toouse em vez disso, introduza o nome de Olá dessa imagem personalizada. Os nomes de imagens personalizadas não são apresentados numa lista, para que tenha tooensure Olá nome é introduzido corretamente.    
    
     Para este tutorial, escreva **U** toobring uma lista de imagens Ubuntu e selecione **Ubuntu Server 14.04 LTS**.
14. Para **iniciar método**, selecione **SSH**.
15. Script de Olá abaixo de copiar e colar Olá **Init script** campo.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     Olá **Init script** será executado após Olá é criada a VM. Neste exemplo, o script de Olá instala Java, o git e ant.
16. No Olá **Username** e **palavra-passe** campos, introduza os valores preferidos para a conta de administrador de Olá que será criada na sua VM.
17. Clique em **verificar modelo** toocheck se Olá que foram especificados parâmetros são válidos.
18. Clique em **Guardar**.

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Criar uma tarefa de Hudson que é executada num nó subordinado no Azure
Nesta secção, irá criar uma tarefa de Hudson que será executada num nó subordinado no Azure.

1. No dashboard de Hudson Olá, clique em **nova tarefa**.
2. Introduza um nome para a tarefa de Olá que estiver a criar.
3. Para o tipo de tarefa Olá, selecione **criar uma tarefa de estilo livre software**.
4. Clique em **OK**.
5. Na página de configuração da tarefa de Olá, selecione **restringir onde é possível executar este projeto**.
6. Selecione **menu nó e a etiqueta** e selecione **linux** (especificamos esta etiqueta ao criar o modelo de máquina virtual de Olá na secção anterior Olá).
7. No Olá **criar** secção, clique em **Adicionar passo de compilação** e selecione **executar shell**.
8. Editar Olá script a seguir, substituindo **{github nome da sua conta}**, **{no nome do projeto}**, e **{diretório do seu projeto}** com adequado valores e cole Olá Editar o script na área de texto de Olá que aparece.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. Clique em **Guardar**.
10. No Hudson dashboard de Olá, localize a tarefa de Olá que acabou de criar e clique em Olá **agendar uma compilação** ícone.

Hudson, em seguida, irá criar um nó subordinado com o modelo de Olá que criou na secção anterior Olá e executar o script de Olá que especificou no passo de compilação de Olá para esta tarefa.

## <a name="next-steps"></a>Passos Seguintes
Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure].

<!-- URL List -->

[Centro de programadores Java do Azure]: https://azure.microsoft.com/develop/java/
[perfil subscrição]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

