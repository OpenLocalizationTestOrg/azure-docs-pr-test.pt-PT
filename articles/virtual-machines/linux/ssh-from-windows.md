---
title: as chaves de aaaUse SSH com o Windows para VMs com Linux | Microsoft Docs
description: "Saiba como chaves toogenerate e utilizar SSH no computador tooconnect tooa Linux máquina virtual do Windows no Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Como chaves de tooUse SSH com o Windows no Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Quando se liga tooLinux as máquinas virtuais (VMs) no Azure, deve utilizar [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide um toolog de forma mais segura no tooyour VM com Linux. Este processo envolve uma troca de chaves pública e privada através de Olá secure shell (SSH) comando tooauthenticate por si em vez de um nome de utilizador e palavra-passe. Palavras-passe são vulneráveis toobrute-force ataques, especialmente em VMs de acesso à Internet, tais como servidores web. Este artigo fornece uma descrição geral de chaves SSH e como toogenerate Olá chaves adequadas num computador Windows.

## <a name="overview-of-ssh-and-keys"></a>Descrição geral de SSH e chaves
Pode iniciar com segurança no tooyour VM com Linux através da utilização de chaves públicas e privadas:

* Olá **chave pública** é colocada na VM com Linux ou qualquer outro serviço que quiser toouse com a criptografia de chave pública.
* Olá **chave privada** é que tooyour presente VM com Linux quando iniciar sessão, tooverify sua identidade. Proteja esta chave privada. Não a partilhe.

Estas chaves públicas e privadas podem ser utilizados em várias VMs e serviços. Não é necessário um par de chaves para cada VM ou serviço pretende tooaccess. Para obter uma descrição mais detalhada, consulte [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography).

SSH é um protocolo de ligação encriptada que permite que os inícios de sessão seguros através de ligações não segura. É Olá predefinido protocolo para VMs com Linux alojados no Azure. Apesar de SSH próprio fornece uma ligação encriptada, ainda utilizar palavras-passe com ligações SSH deixa Olá VM vulnerável toobrute-force ataques ou deteção de palavras-passe. Um método mais seguro e preferencial de ligação tooa VM utilizando o SSH é utilizar estas chaves públicas e privadas, também conhecido como as chaves SSH.

Se não desejar toouse chaves SSH, pode ainda iniciar sessão no tooyour VMs com Linux utilizando uma palavra-passe. Se a VM não for toohello exposto à Internet, a utilização de palavras-passe pode ser suficiente. No entanto, é ainda necessário toomanage as palavras-passe para cada VM com Linux e manter políticas de palavra-passe bom estado de funcionamento e práticas, como o comprimento mínimo da palavra-passe e a atualizar regularmente-los. utilização de Olá de chaves SSH reduz o complexidade Olá da gestão de credenciais individuais através de várias VMs.

## <a name="windows-packages-and-ssh-clients"></a>Pacotes do Windows e clientes SSH
Ligar tooand gerir VMs com Linux no Azure com um **cliente SSH**. Computadores com o Windows não têm, normalmente, um cliente SSH instalado. Olá Windows 10 aniversário da atualização adicionados Bash para Windows e hello mais recente do Windows 10 criadores Update fornece atualizações adicionais. Este subsistema Windows para Linux permite-lhe utilitários toorun e o acesso, por exemplo, um cliente SSH nativamente dentro de uma shell de deteção. Pode seguir qualquer um dos documentos de Linux Olá, em seguida, como [como toogenerate SSH chave combinada para Linux](mac-create-ssh-keys.md). Bash para Windows está ainda em desenvolvimento e é considerado uma versão beta. Para mais informações sobre Bash para Windows, consulte [Bash no Ubuntu no Windows](https://msdn.microsoft.com/commandline/wsl/about).

Se desejar toouse algo que não sejam Bash para Windows, comuns SSH do Windows que pode instalar forem incluídos clientes em Olá os seguintes pacotes:

* [Git para Windows](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>Ficheiros de chave que necessita de toocreate?
O Azure requer, pelo menos, 2048 bits, **ssh-rsa** formatado chaves públicas e privadas. Se estiver a gerir os recursos do Azure utilizando o modelo de implementação clássica Olá, terá também de toogenerate um PEM (`.pem` ficheiro).

Seguem-se cenários de implementação de Olá e Olá tipos de ficheiros que utilizam em cada:

1. **SSH-rsa** chaves são necessárias para qualquer implementação utilizando Olá [portal do Azure](https://portal.azure.com)e implementações do Resource Manager utilizando Olá [CLI do Azure](../../cli-install-nodejs.md).
   * Estas chaves são normalmente, todos os maioria das pessoas ter.
2. A `.pem` ficheiro é VMs toocreate necessárias utilizando a implementação do Olá clássico. Estas chaves são suportadas em implementações clássicas quando Olá [portal do Azure](https://portal.azure.com) ou [CLI do Azure](../../cli-install-nodejs.md).
   * Basta toocreate estas chaves adicionais e certificados se estiver a gerir os recursos criados utilizando o modelo de implementação clássica Olá.

## <a name="install-git-for-windows"></a>Instalar o Git para Windows
Olá secção anterior vários pacotes listados que incluem Olá `openssl` ferramenta para o Windows. Esta ferramenta é chaves públicas e privadas de toocreate necessários. Olá, como os seguintes detalhes de exemplos tooinstall e utilizar **Git para Windows**, embora pode escolher qualquer pacote que preferir. **Git para Windows** dá-lhe acesso toosome o software open source adicional ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) ferramentas e utilitários que poderão ser útil à medida que trabalha com VMs com Linux.

1. Transfira e instale **Git para Windows** de Olá seguinte localização: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Aceitar o processo de instalação de opções predefinidas de Olá durante Olá não ser que necessite especificamente toochange-los.
3. Executar **Git Bash** de Olá **Menu Iniciar** > **Git** > **Git Bash**. consola de Olá procura toohello semelhante seguinte exemplo:

    ![Git para Windows Bash shell](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Criar uma chave privada
1. No seu **Git Bash** janela, utilize `openssl.exe` toocreate uma chave privada. Olá exemplo seguinte cria uma chave denominada `myPrivateKey` e o certificado com o nome `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    saída de Olá procura toohello semelhante seguinte exemplo:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Se bash reportar um erro, tente abrir um novo **Git Bash** janela com privilégios elevados. Em seguida, volte a executar Olá `openssl` comando.

2. Olá resposta solicita o nome do país, localização, nome da organização, etc.
3. A nova chave privada e certificado são criados no seu diretório de trabalho atual. Como medida de segurança, deve definir permissões de Olá na sua chave privada para que apenas tem acesso:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Olá [secção seguinte](#create-a-private-key-for-putty) detalhes utilizando PuTTYgen tooboth ver e utilizar a chave pública Olá e criar uma chave privada específico para utilizar o PuTTY tooSSH tooLinux VMs. Olá seguinte comando gera um ficheiro de chave pública nomeado `myPublicKey.key` que pode utilizar imediatamente:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Se precisar de recursos de clássico toomanage também, converter Olá `myCert.pem` demasiado`myCert.cer` (DER codificado X509 certificado). Execute este passo opcional apenas se precisar de toospecifically gerir recursos de clássico mais antigos.

    Converter o certificado de Olá utilizando Olá os seguintes comandos:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Criar uma chave privada para o PuTTY
PuTTY for um cliente SSH comuns para o Windows. É gratuita toouse qualquer cliente SSH que desejar. toouse PuTTY, terá de toocreate um tipo de chave - uma chave privada PuTTY (PPK) adicional. Se não desejar toouse PuTTY, ignore esta secção.

Olá exemplo seguinte cria esta chave privada adicional especificamente para PuTTY toouse:

1. Utilize **Git Bash** tooconvert privada da sua chave para uma chave privada RSA que possa compreender PuTTYgen. Olá exemplo seguinte cria uma chave denominada `myPrivateKey_rsa` da chave existente Olá denominado `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Como medida de segurança, deve definir permissões de Olá na sua chave privada para que apenas tem acesso:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Transferir e executar PuTTYgen de Olá seguinte localização: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Clique em menu Olá: **ficheiro** > **chave privada de carga**
4. Localize a chave privada (`myPrivateKey_rsa` no exemplo anterior Olá). diretório predefinido de Olá quando iniciar **Git Bash** é `C:\Users\%username%`. Alterar tooshow de filtro de ficheiro Olá **todos os ficheiros (\*.\*)** :

    ![Carregar a chave privada existente de Olá para PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. Clique em **abra**. Numa linha indica que essa chave Olá foi importado com êxito:

    ![Chave tooPuTTYgen foram importados com êxito](./media/ssh-from-windows/successfully-imported-key.png)
6. Clique em **OK** linha de comandos do tooclose Olá.
7. chave pública Olá é apresentada na parte superior Olá Olá **PuTTYgen** janela. Copie e cole esta chave pública Olá portal do Azure ou o modelo Azure Resource Manager ao criar uma VM com Linux. Também pode clicar em **Guardar chave pública** toosave um computador de tooyour cópia:

    ![Guarde o ficheiro de chave pública PuTTY](./media/ssh-from-windows/save-public-key.png)

    Olá exemplo seguinte mostra como poderia copiar e colar esta chave pública no Olá portal do Azure, quando criar uma VM com Linux. chave pública Olá, em seguida, é normalmente armazenado num `~/.ssh/authorized_keys` na sua nova VM.

    ![Utilize a chave pública, quando cria uma VM no Olá portal do Azure](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. Novamente no **PuTTYgen**, clique em **guardar a chave privada**:

    ![Guarde o ficheiro de chave privada do PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Uma linha de comandos pede-lhe se pretende toocontinue sem introduzir uma frase de acesso para a sua chave. Uma frase de acesso é como uma chave privada de tooyour anexado de palavra-passe. Mesmo se alguém foram tooobtain a chave privada, ainda não seria capaz de tooauthenticate utilizando apenas Olá chave. Deverá também precisam de Olá frase de acesso. Sem uma frase de acesso, se alguém obtém a chave privada, podem iniciar sessão tooany VM ou serviço que utiliza essa chave. Recomendamos que crie uma frase de acesso. No entanto, se se esquecer da frase de acesso de Olá, não há nenhuma forma toorecovê-lo.
   >
   >

    Se desejar tooenter uma frase de acesso, clique em **não**, introduza uma frase de acesso na janela principal do PuTTYgen Olá e, em seguida, clique em **Guardar chave privada** novamente. Caso contrário, clique em **Sim** toocontinue sem fornecer Olá frase de acesso opcional.
9. Introduza um nome e localização toosave o ficheiro PPK.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Utilizar o Putty tooSSH tooa máquina Linux
Novamente, PuTTY for um cliente SSH comuns para o Windows. É gratuita toouse qualquer cliente SSH que desejar. Olá, como os seguintes detalhes de passos toouse sua tooauthenticate chave privada com a VM do Azure através do SSH. passos de Olá serem semelhantes em outros clientes de chaves SSH em termos de necessitar tooload sua Olá tooauthenticate chave privada ligação SSH.

1. Olá, transferir e executar putty da seguinte localização: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Preencha o nome de anfitrião de Olá ou endereço IP da sua VM do Olá portal do Azure:

    ![Abrir nova ligação PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. Antes de selecionar **abra**, clique em **ligação** > **SSH** > **Auth** separador. Procurar tooand selecione a chave privada:

    ![Selecione a sua chave privada do PuTTY para autenticação](./media/ssh-from-windows/putty-auth-dialog.png)
4. Clique em **abra** tooconnect tooyour máquina

## <a name="next-steps"></a>Passos seguintes
Também pode gerar as chaves públicas e privadas do Olá [utilizando OS X e Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Para obter mais informações sobre Bash para Windows e os benefícios de Olá de ter as ferramentas de OSS prontamente disponíveis no seu computador Windows, consulte [Bash no Ubuntu no Windows](https://msdn.microsoft.com/commandline/wsl/about).

Se tiver problemas ao utilizar o SSH tooconnect tooyour VMs com Linux, consulte [resolver problemas de SSH ligações tooan VM do Linux do Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
