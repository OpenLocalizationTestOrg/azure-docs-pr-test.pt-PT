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
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="1a4f8-103">Guia de resolução de problemas de Explorador de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="1a4f8-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="1a4f8-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="1a4f8-104">Introduction</span></span>

<span data-ttu-id="1a4f8-105">Explorador de armazenamento do Microsoft Azure (pré-visualização) é uma aplicação autónoma que lhe permite tooeasily trabalho com dados de armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="1a4f8-106">aplicação Olá pode ligar a contas toStorage alojadas no Azure, Sovereign nuvens e pilha do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="1a4f8-107">Este guia resume soluções para problemas comuns vistos no Explorador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="1a4f8-108">Inicie sessão no problemas</span><span class="sxs-lookup"><span data-stu-id="1a4f8-108">Sign in issues</span></span>

<span data-ttu-id="1a4f8-109">Antes de continuar, tente reiniciar a aplicação e ver se os problemas de Olá possam ser corrigidos.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-109">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="1a4f8-110">Erro: O certificado Autoassinado na cadeia de certificados</span><span class="sxs-lookup"><span data-stu-id="1a4f8-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="1a4f8-111">Existem vários motivos por que razão poderá encontrar este erro, e Olá mais dois os motivos mais comuns são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-111">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="1a4f8-112">aplicação Olá está ligada através de "proxy transparente", que significa um servidor (por exemplo, o servidor da empresa) é a intercetar tráfego HTTPS, desencriptação-lo e, em seguida, encriptá-la através de um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-112">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="1a4f8-113">Está a executar uma aplicação, tal como software antivírus, que é inserirem-se um certificado SSL autoassinado para mensagens hello do HTTPS recebidos.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="1a4f8-114">Quando o Explorador de armazenamento encontra um dos problemas de Olá, pode já não sabe se a mensagem de HTTPS de saudação recebida é adulterada.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-114">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="1a4f8-115">Se tiver uma cópia do certificado autoassinado Olá, pode deixar o Explorador de armazenamento confiar nele.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-115">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="1a4f8-116">Se não souber de que é inserirem certificado Olá, siga estes passos toofind-lo:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-116">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="1a4f8-117">Instalar SSL aberta</span><span class="sxs-lookup"><span data-stu-id="1a4f8-117">Install Open SSL</span></span>

    - <span data-ttu-id="1a4f8-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (qualquer uma das versões leve Olá deve ser suficiente)</span><span class="sxs-lookup"><span data-stu-id="1a4f8-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="1a4f8-119">Mac e Linux: devem ser incluídos com o sistema operativo</span><span class="sxs-lookup"><span data-stu-id="1a4f8-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="1a4f8-120">Executar SSL aberta</span><span class="sxs-lookup"><span data-stu-id="1a4f8-120">Run Open SSL</span></span>

    - <span data-ttu-id="1a4f8-121">Windows: Abra o diretório de instalação de Olá, clique em **/bin/**e, em seguida, faça duplo clique **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-121">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="1a4f8-122">Mac e Linux: executar **openssl** de um terminal.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="1a4f8-123">Executar s_client - showcerts-ligar microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="1a4f8-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="1a4f8-124">Procure certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-124">Look for self-signed certificates.</span></span> <span data-ttu-id="1a4f8-125">Se não souber qual são autoassinados, procure em qualquer lugar requerente Olá ("s:") e o emissor ("i:") são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-125">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="1a4f8-126">Quando encontrar quaisquer certificados autoassinados, para cada um, copie e cole tudo a partir e incluindo **---BEGIN CERTIFICATE---** demasiado**---fim certificado---** tooa novo ficheiro de. cer.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="1a4f8-127">Abra o Explorador de armazenamento, clique em **editar** > **certificados SSL** > **importar certificados**e, em seguida, utilize Olá ficheiro selecionador toofind, selecione, e abrir Olá. cer ficheiros que criou.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="1a4f8-128">Se não encontrar quaisquer certificados autoassinados com Olá os passos acima, contacte-nos através da ferramenta de comentários de Olá para obter mais ajuda.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-128">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="1a4f8-129">Não é possível tooretrieve subscrições</span><span class="sxs-lookup"><span data-stu-id="1a4f8-129">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="1a4f8-130">Se forem tooretrieve não é possível que as suas subscrições depois de iniciar sessão com êxito no, siga estes passos tootroubleshoot este problema:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-130">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="1a4f8-131">Certifique-se de que a conta tem acesso toohello subscrições ao iniciar sessão Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-131">Verify that your account has access toohello subscriptions by signing into hello Azure Portal.</span></span>

- <span data-ttu-id="1a4f8-132">Certifique-se de que se inscreveu no utilizando Olá ambiente correto (do Azure, Azure China, Datacenters do Azure, Azure US Government ou pilha de ambiente/Azure personalizado).</span><span class="sxs-lookup"><span data-stu-id="1a4f8-132">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="1a4f8-133">Se estiver atrás de um proxy, certifique-se de que configurou proxy do Explorador de armazenamento de Olá corretamente.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-133">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="1a4f8-134">Tente remover e readding conta Olá.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-134">Try removing and readding hello account.</span></span>

- <span data-ttu-id="1a4f8-135">Tente eliminar Olá os seguintes ficheiros do diretório de raiz (ou seja, C:\Users\ContosoUser) e, em seguida, voltar a adicionar conta de Olá:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-135">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="1a4f8-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="1a4f8-136">.adalcache</span></span>

    - <span data-ttu-id="1a4f8-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="1a4f8-137">.devaccounts</span></span>

    - <span data-ttu-id="1a4f8-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="1a4f8-138">.extaccounts</span></span>

- <span data-ttu-id="1a4f8-139">Consola de ferramentas do veja Olá programador (premindo F12) quando iniciar sessão para as mensagens de erro:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-139">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Ferramentas de programador](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="1a4f8-141">Página de autenticação não é possível toosee Olá</span><span class="sxs-lookup"><span data-stu-id="1a4f8-141">Unable toosee hello authentication page</span></span>

<span data-ttu-id="1a4f8-142">Se estiver a página de autenticação não é possível toosee Olá, siga estes passos tootroubleshoot este problema:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-142">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="1a4f8-143">Consoante a velocidade de Olá da sua ligação, poderá demorar algum tempo para tooload da página de início de sessão de Olá, aguarde, pelo menos, um minuto antes de fechar a caixa de diálogo de autenticação de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-143">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="1a4f8-144">Se estiver atrás de um proxy, certifique-se de que configurou proxy do Explorador de armazenamento de Olá corretamente.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-144">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="1a4f8-145">Consola de programador do Olá vista ao premir a tecla F12 de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-145">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="1a4f8-146">Ver respostas hello da consola de programador Olá e veja se pode encontrar qualquer clue porquê autenticação não está a funcionar.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-146">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="1a4f8-147">Não é possível remover a conta</span><span class="sxs-lookup"><span data-stu-id="1a4f8-147">Cannot remove account</span></span>

<span data-ttu-id="1a4f8-148">Se forem tooremove não é possível uma conta, ou se Olá reautenticação ligação fazer nada, siga estes passos tootroubleshoot este problema:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-148">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="1a4f8-149">Tente eliminar Olá os seguintes ficheiros do diretório de raiz e, em seguida, readding conta Olá:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-149">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="1a4f8-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="1a4f8-150">.adalcache</span></span>

    - <span data-ttu-id="1a4f8-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="1a4f8-151">.devaccounts</span></span>

    - <span data-ttu-id="1a4f8-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="1a4f8-152">.extaccounts</span></span>

- <span data-ttu-id="1a4f8-153">Se quiser tooremove SAS ligado recursos de armazenamento, elimine Olá os seguintes ficheiros:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-153">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="1a4f8-154">Pasta de %AppData%/StorageExplorer para Windows</span><span class="sxs-lookup"><span data-stu-id="1a4f8-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="1a4f8-155">/Users/ < your_name >/biblioteca/Applicaiton suporte/StorageExplorer para Mac</span><span class="sxs-lookup"><span data-stu-id="1a4f8-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="1a4f8-156">~/.config/StorageExplorer para Linux</span><span class="sxs-lookup"><span data-stu-id="1a4f8-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="1a4f8-157">Terá tooreenter todas as suas credenciais se eliminar estes ficheiros.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-157">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="1a4f8-158">Problemas de proxy</span><span class="sxs-lookup"><span data-stu-id="1a4f8-158">Proxy issues</span></span>

<span data-ttu-id="1a4f8-159">Em primeiro lugar, certifique-se de que Olá seguindo as informações que introduziu estão corretos:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-159">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="1a4f8-160">Olá URL de proxy e a porta número</span><span class="sxs-lookup"><span data-stu-id="1a4f8-160">hello proxy URL and port number</span></span>

- <span data-ttu-id="1a4f8-161">Nome de utilizador e palavra-passe se for necessário por proxy Olá</span><span class="sxs-lookup"><span data-stu-id="1a4f8-161">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="1a4f8-162">Soluções comuns</span><span class="sxs-lookup"><span data-stu-id="1a4f8-162">Common solutions</span></span>

<span data-ttu-id="1a4f8-163">Se ainda ocorrerem problemas, siga estes passos tootroubleshoot-los:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-163">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="1a4f8-164">Se pode ligar toohello Internet sem utilizar o proxy, certifique-se de que o Explorador de armazenamento funciona sem as definições de proxy ativadas.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-164">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="1a4f8-165">Se for este caso de Olá, poderá existir um problema com as definições de proxy.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-165">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="1a4f8-166">Trabalhar com os problemas de Olá tooidentify do proxy administrador.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-166">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="1a4f8-167">Certifique-se de que as outras aplicações utilizando o servidor de proxy de Olá funcionam conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-167">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="1a4f8-168">Verifique se pode ligar o portal do Microsoft Azure toohello utilizando o seu browser</span><span class="sxs-lookup"><span data-stu-id="1a4f8-168">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="1a4f8-169">Certifique-se de que pode receber respostas do seu pontos finais de serviço.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="1a4f8-170">Introduza um URL de ponto final no seu browser.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="1a4f8-171">Se pode ligar, deverá receber um InvalidQueryParameterValue ou semelhante resposta XML.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="1a4f8-172">Se também que mais alguém está a utilizar o Explorador de armazenamento com o seu servidor proxy, certifique-se de que possam estabelecer a ligação.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="1a4f8-173">Se pode ligar-se, se possuir toocontact o administrador do servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-173">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="1a4f8-174">Ferramentas para diagnosticar problemas</span><span class="sxs-lookup"><span data-stu-id="1a4f8-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="1a4f8-175">Se tiver de ferramentas de rede, como o Fiddler para Windows, podem ser capaz de toodiagnose problemas de Olá da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-175">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="1a4f8-176">Se tiver toowork através do proxy, poderá ter tooconfigure sua tooconnect ferramenta rede através do proxy de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-176">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="1a4f8-177">Verifique o número de porta de Olá utilizado pela ferramenta de sua rede.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-177">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="1a4f8-178">Introduza o URL de anfitrião local Olá e Olá número da porta da ferramenta de rede, como definições de proxy no Explorador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-178">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="1a4f8-179">Se esta isdone corretamente, a ferramenta de rede começa registo de pedidos de rede efetuados por pontos finais de serviço e toomanagement do Explorador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="1a4f8-180">Por exemplo, introduza https://cawablobgrs.blob.core.windows.net/ para o ponto final do blob num browser, e irá receber uma resposta é semelhante Olá seguinte, o que sugere Olá recurso existe, apesar de não é possível aceder-lhe.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![exemplo de código](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="1a4f8-182">Contacte o administrador do servidor proxy</span><span class="sxs-lookup"><span data-stu-id="1a4f8-182">Contact proxy server admin</span></span>

<span data-ttu-id="1a4f8-183">Se as definições de proxy estão corretas, poderá ter toocontact seu administrador de servidor proxy, e</span><span class="sxs-lookup"><span data-stu-id="1a4f8-183">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="1a4f8-184">Certifique-se de que o proxy não bloqueia o tráfego tooAzure gestão ou recurso pontos finais.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-184">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="1a4f8-185">Verifique se o protocolo de autenticação de Olá utilizado pelo seu servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-185">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="1a4f8-186">Explorador de armazenamento não suporta atualmente os proxies NTLM.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="1a4f8-187">Mensagem de erro "Não é possível tooRetrieve subordinados"</span><span class="sxs-lookup"><span data-stu-id="1a4f8-187">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="1a4f8-188">Se estiver ligado tooAzure através de um proxy, certifique-se de que as definições de proxy estão corretas.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-188">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="1a4f8-189">Se foi concedido acesso tooa recurso do proprietário Olá de subscrição de Olá ou conta, certifique-se de que leu ou lista de permissões para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-189">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="1a4f8-190">Problemas com o SAS URL</span><span class="sxs-lookup"><span data-stu-id="1a4f8-190">Issues with SAS URL</span></span>
<span data-ttu-id="1a4f8-191">Se estiver a ligar o serviço de tooa utilizando um URL SAS e estão a ocorrer este erro:</span><span class="sxs-lookup"><span data-stu-id="1a4f8-191">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="1a4f8-192">Certifique-se de que o URL de Olá fornece as permissões necessárias Olá tooread ou lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-192">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="1a4f8-193">Certifique-se de que Olá que URL não expirou.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-193">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="1a4f8-194">Se Olá SAS URL baseiam-se uma política de acesso, certifique-se de que política de acesso de Olá não foi revogada.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-194">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a4f8-195">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1a4f8-195">Next steps</span></span>

<span data-ttu-id="1a4f8-196">Se nenhuma das soluções de Olá resolver o problema, submeter o seu problema através da ferramenta de comentários de Olá com o seu e-mail e tantos detalhes sobre o problema de Olá incluídas como podem, para que podemos contactá-lo para corrigir o problema de Olá.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-196">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="1a4f8-197">toodo, clique em **ajudar** e, em seguida, clique em **enviar comentários**.</span><span class="sxs-lookup"><span data-stu-id="1a4f8-197">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Comentários](./media/storage-explorer-troubleshooting/4022503_en_1.png)
