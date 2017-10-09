---
title: "Guia de resolução de problemas de Explorador de armazenamento aaaAzure | Microsoft Docs"
description: "Descrição geral da funcionalidade de depuração Olá duas do Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Guia de resolução de problemas de Explorador de armazenamento do Azure

## <a name="introduction"></a>Introdução

Explorador de armazenamento do Microsoft Azure (pré-visualização) é uma aplicação autónoma que lhe permite tooeasily trabalho com dados de armazenamento do Azure no Windows, macOS e Linux. aplicação Olá pode ligar a contas toStorage alojadas no Azure, Sovereign nuvens e pilha do Azure.

Este guia resume soluções para problemas comuns vistos no Explorador de armazenamento.

## <a name="sign-in-issues"></a>Inicie sessão no problemas

Antes de continuar, tente reiniciar a aplicação e ver se os problemas de Olá possam ser corrigidos.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Erro: O certificado Autoassinado na cadeia de certificados

Existem vários motivos por que razão poderá encontrar este erro, e Olá mais dois os motivos mais comuns são os seguintes:

1. aplicação Olá está ligada através de "proxy transparente", que significa um servidor (por exemplo, o servidor da empresa) é a intercetar tráfego HTTPS, desencriptação-lo e, em seguida, encriptá-la através de um certificado autoassinado.

2. Está a executar uma aplicação, tal como software antivírus, que é inserirem-se um certificado SSL autoassinado para mensagens hello do HTTPS recebidos.

Quando o Explorador de armazenamento encontra um dos problemas de Olá, pode já não sabe se a mensagem de HTTPS de saudação recebida é adulterada. Se tiver uma cópia do certificado autoassinado Olá, pode deixar o Explorador de armazenamento confiar nele. Se não souber de que é inserirem certificado Olá, siga estes passos toofind-lo:

1. Instalar SSL aberta

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (qualquer uma das versões leve Olá deve ser suficiente)

    - Mac e Linux: devem ser incluídos com o sistema operativo

2. Executar SSL aberta

    - Windows: Abra o diretório de instalação de Olá, clique em **/bin/**e, em seguida, faça duplo clique **openssl.exe**.
    - Mac e Linux: executar **openssl** de um terminal.

3. Executar s_client - showcerts-ligar microsoft.com:443

4. Procure certificados autoassinados. Se não souber qual são autoassinados, procure em qualquer lugar requerente Olá ("s:") e o emissor ("i:") são Olá mesmo.

5. Quando encontrar quaisquer certificados autoassinados, para cada um, copie e cole tudo a partir e incluindo **---BEGIN CERTIFICATE---** demasiado**---fim certificado---** tooa novo ficheiro de. cer.

6. Abra o Explorador de armazenamento, clique em **editar** > **certificados SSL** > **importar certificados**e, em seguida, utilize Olá ficheiro selecionador toofind, selecione, e abrir Olá. cer ficheiros que criou.

Se não encontrar quaisquer certificados autoassinados com Olá os passos acima, contacte-nos através da ferramenta de comentários de Olá para obter mais ajuda.

### <a name="unable-tooretrieve-subscriptions"></a>Não é possível tooretrieve subscrições

Se forem tooretrieve não é possível que as suas subscrições depois de iniciar sessão com êxito no, siga estes passos tootroubleshoot este problema:

- Certifique-se de que a conta tem acesso toohello subscrições ao iniciar sessão Olá Portal do Azure.

- Certifique-se de que se inscreveu no utilizando Olá ambiente correto (do Azure, Azure China, Datacenters do Azure, Azure US Government ou pilha de ambiente/Azure personalizado).

- Se estiver atrás de um proxy, certifique-se de que configurou proxy do Explorador de armazenamento de Olá corretamente.

- Tente remover e readding conta Olá.

- Tente eliminar Olá os seguintes ficheiros do diretório de raiz (ou seja, C:\Users\ContosoUser) e, em seguida, voltar a adicionar conta de Olá:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Consola de ferramentas do veja Olá programador (premindo F12) quando iniciar sessão para as mensagens de erro:

![Ferramentas de programador](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>Página de autenticação não é possível toosee Olá

Se estiver a página de autenticação não é possível toosee Olá, siga estes passos tootroubleshoot este problema:

- Consoante a velocidade de Olá da sua ligação, poderá demorar algum tempo para tooload da página de início de sessão de Olá, aguarde, pelo menos, um minuto antes de fechar a caixa de diálogo de autenticação de Olá.

- Se estiver atrás de um proxy, certifique-se de que configurou proxy do Explorador de armazenamento de Olá corretamente.

- Consola de programador do Olá vista ao premir a tecla F12 de Olá. Ver respostas hello da consola de programador Olá e veja se pode encontrar qualquer clue porquê autenticação não está a funcionar.

### <a name="cannot-remove-account"></a>Não é possível remover a conta

Se forem tooremove não é possível uma conta, ou se Olá reautenticação ligação fazer nada, siga estes passos tootroubleshoot este problema:

- Tente eliminar Olá os seguintes ficheiros do diretório de raiz e, em seguida, readding conta Olá:

    - .adalcache

    - .devaccounts

    - .extaccounts

- Se quiser tooremove SAS ligado recursos de armazenamento, elimine Olá os seguintes ficheiros:

    - Pasta de %AppData%/StorageExplorer para Windows

    - /Users/ < your_name >/biblioteca/Applicaiton suporte/StorageExplorer para Mac

    - ~/.config/StorageExplorer para Linux

> [!NOTE]
>  Terá tooreenter todas as suas credenciais se eliminar estes ficheiros.

## <a name="proxy-issues"></a>Problemas de proxy

Em primeiro lugar, certifique-se de que Olá seguindo as informações que introduziu estão corretos:

- Olá URL de proxy e a porta número

- Nome de utilizador e palavra-passe se for necessário por proxy Olá

### <a name="common-solutions"></a>Soluções comuns

Se ainda ocorrerem problemas, siga estes passos tootroubleshoot-los:

- Se pode ligar toohello Internet sem utilizar o proxy, certifique-se de que o Explorador de armazenamento funciona sem as definições de proxy ativadas. Se for este caso de Olá, poderá existir um problema com as definições de proxy. Trabalhar com os problemas de Olá tooidentify do proxy administrador.

- Certifique-se de que as outras aplicações utilizando o servidor de proxy de Olá funcionam conforme esperado.

- Verifique se pode ligar o portal do Microsoft Azure toohello utilizando o seu browser

- Certifique-se de que pode receber respostas do seu pontos finais de serviço. Introduza um URL de ponto final no seu browser. Se pode ligar, deverá receber um InvalidQueryParameterValue ou semelhante resposta XML.

- Se também que mais alguém está a utilizar o Explorador de armazenamento com o seu servidor proxy, certifique-se de que possam estabelecer a ligação. Se pode ligar-se, se possuir toocontact o administrador do servidor proxy.

### <a name="tools-for-diagnosing-issues"></a>Ferramentas para diagnosticar problemas

Se tiver de ferramentas de rede, como o Fiddler para Windows, podem ser capaz de toodiagnose problemas de Olá da seguinte forma:

- Se tiver toowork através do proxy, poderá ter tooconfigure sua tooconnect ferramenta rede através do proxy de Olá.

- Verifique o número de porta de Olá utilizado pela ferramenta de sua rede.

- Introduza o URL de anfitrião local Olá e Olá número da porta da ferramenta de rede, como definições de proxy no Explorador de armazenamento. Se esta isdone corretamente, a ferramenta de rede começa registo de pedidos de rede efetuados por pontos finais de serviço e toomanagement do Explorador de armazenamento. Por exemplo, introduza https://cawablobgrs.blob.core.windows.net/ para o ponto final do blob num browser, e irá receber uma resposta é semelhante Olá seguinte, o que sugere Olá recurso existe, apesar de não é possível aceder-lhe.

![exemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Contacte o administrador do servidor proxy

Se as definições de proxy estão corretas, poderá ter toocontact seu administrador de servidor proxy, e

- Certifique-se de que o proxy não bloqueia o tráfego tooAzure gestão ou recurso pontos finais.

- Verifique se o protocolo de autenticação de Olá utilizado pelo seu servidor proxy. Explorador de armazenamento não suporta atualmente os proxies NTLM.

## <a name="unable-tooretrieve-children-error-message"></a>Mensagem de erro "Não é possível tooRetrieve subordinados"

Se estiver ligado tooAzure através de um proxy, certifique-se de que as definições de proxy estão corretas. Se foi concedido acesso tooa recurso do proprietário Olá de subscrição de Olá ou conta, certifique-se de que leu ou lista de permissões para esse recurso.

### <a name="issues-with-sas-url"></a>Problemas com o SAS URL
Se estiver a ligar o serviço de tooa utilizando um URL SAS e estão a ocorrer este erro:

- Certifique-se de que o URL de Olá fornece as permissões necessárias Olá tooread ou lista de recursos.

- Certifique-se de que Olá que URL não expirou.

- Se Olá SAS URL baseiam-se uma política de acesso, certifique-se de que política de acesso de Olá não foi revogada.

## <a name="next-steps"></a>Passos seguintes

Se nenhuma das soluções de Olá resolver o problema, submeter o seu problema através da ferramenta de comentários de Olá com o seu e-mail e tantos detalhes sobre o problema de Olá incluídas como podem, para que podemos contactá-lo para corrigir o problema de Olá.

toodo, clique em **ajudar** e, em seguida, clique em **enviar comentários**.

![Comentários](./media/storage-explorer-troubleshooting/4022503_en_1.png)
