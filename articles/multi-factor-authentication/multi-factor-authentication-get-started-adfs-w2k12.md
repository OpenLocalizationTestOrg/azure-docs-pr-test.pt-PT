---
title: aaaMFA servidor com o AD FS no Windows Server | Microsoft Docs
description: "Este artigo descreve como tooget começar a utilizar multi-factor Authentication do Azure e o AD FS no Windows Server 2012 R2 e 2016."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Configurar o servidor do Azure multi-factor Authentication toowork com o AD FS no Windows Server
Se utilizar os serviços de Federação do Active Directory (AD FS) e pretende toosecure recursos de nuvem ou no local, pode configurar toowork do servidor do Azure multi-factor Authentication com o AD FS. Esta configuração aciona a verificação de dois passos para pontos finais de alto valor.

Neste artigo, discutimos a utilização do Servidor Multi-Factor Authentication do Azure com o AD FS no Windows Server 2012 R2 ou no Windows Server 2016. Para obter mais informações, leia o artigo sobre como demasiado[proteger recursos na nuvem e no local utilizando o servidor do Azure multi-factor Authentication com o AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Proteger o Windows Server AD FS com o Servidor Multi-Factor Authentication do Azure
Quando instalar o servidor do Azure multi-factor Authentication, tem Olá seguintes opções:

* Instalar o servidor de autenticação do multi-factor do Azure localmente no Olá mesmo servidor do AD FS
* Instalar o adaptador do multi-factor Authentication do Azure de Olá localmente no Olá servidor AD FS e, em seguida, instale o servidor multi-factor Authentication num computador diferente

Antes de começar, tenha em atenção Olá seguintes informações:

* Não é necessário tooinstall servidor do Azure multi-factor Authentication no seu servidor AD FS. No entanto, tem de instalar adaptador do multi-factor Authentication de Olá para o AD FS num Windows Server 2012 R2 ou Windows Server 2016, que está a executar o AD FS. Pode instalar o servidor de Olá num computador diferente se for uma versão suportada e instalar Olá adaptador AD FS separadamente no seu servidor de Federação do AD FS. Consulte Olá os seguintes procedimentos toolearn como tooinstall Olá adaptador separadamente.
* Se a sua organização utilizar métodos de verificação de aplicação móvel ou mensagem de texto, cadeias de Olá definidas nas definições da empresa contêm um marcador de posição <$*application_name*$>. No servidor do MFA v7.1, pode fornecer um nome de aplicação que substitui este marcador de posição. V 7.0 ou anterior, este marcador de posição não é substituído automaticamente quando utiliza o adaptador do Olá AD FS. Para essas versões mais antigas, remova marcador de posição de Olá cadeias adequadas Olá quando proteger o AD FS.
* conta de Olá que utilizar toosign no tem de ter grupos de segurança de toocreate de direitos de utilizador no seu serviço do Active Directory.
* o Assistente de instalação do adaptador Olá multi-factor Authentication. o AD FS cria um grupo de segurança chamado PhoneFactor Admins na sua instância do Active Directory. -Lo, em seguida, adiciona a conta de serviço de Olá do AD FS do seu grupo de toothis do serviço de Federação. Certifique-se no seu controlador de domínio que Olá grupo PhoneFactor Admins é efetivamente criado e que a conta de serviço Olá AD FS é um membro deste grupo. Se necessário, adicione manualmente toohello de conta de serviço do AD FS de Olá grupo PhoneFactor Admins no seu controlador de domínio.
* Para obter informações sobre a instalação Olá SDK do serviço Web com o portal de utilizador de Olá, leia sobre [implementar o portal de utilizador de Olá multi-factor Authentication do servidor do Azure.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Instalar o servidor de autenticação do multi-factor do Azure localmente no servidor de Olá do AD FS
1. Transfira e instale o Servidor Multi-Factor Authentication do Azure no seu servidor AD FS. Para obter informações de instalação, consulte a [introdução ao Servidor Multi-Factor Authentication do Azure](multi-factor-authentication-get-started-server.md).
2. Na consola de gestão de servidor do Azure multi-factor Authentication Olá, clique em Olá **do AD FS** ícone. Selecione as opções de Olá **permitir inscrição de utilizador** e **permitir que os utilizadores tooselect método**.
3. Selecione quaisquer opções adicionais que gostaria de toospecify para a sua organização.
4. Clique em **Instalar Adaptador AD FS**.
   
   <center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Se for apresentada a janela de Active Directory Olá, isto significa que duas coisas. O computador está tooa associados a um domínio e Olá configuração do Active Directory para proteger a comunicação entre o adaptador do Olá AD FS e o serviço de multi-factor Authentication Olá estiver incompleta. Clique em **seguinte** tooautomatically concluir esta configuração, ou selecione Olá **ignorar configuração automática do Active Directory e configurar as definições manualmente** caixa de verificação. Clique em **Seguinte**.
6. Se for apresentado o windows de Grupo Local de Olá, isto significa que duas coisas. O computador não está tooa associados a um domínio e configuração do grupo local de Olá para proteger a comunicação entre o adaptador do Olá AD FS e o serviço de multi-factor Authentication Olá está incompleta. Clique em **seguinte** tooautomatically concluir esta configuração, ou selecione Olá **ignorar configuração automática do Grupo Local e configurar as definições manualmente** caixa de verificação. Clique em **Seguinte**.
7. No Assistente de instalação de Olá, clique em **seguinte**. Servidor de autenticação multi-factor do Azure cria Olá grupo PhoneFactor Admins e adiciona toohello de conta de serviço do AD FS de Olá grupo PhoneFactor Admins.
   <center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. No Olá **iniciar o instalador** página, clique em **seguinte**.
9. No instalador do adaptador Olá multi-factor Authentication. o AD FS, clique em **seguinte**.
10. Clique em **fechar** quando Olá instalação estiver terminada.
11. Quando Olá adaptador foi instalado, tem de registá-lo com o AD FS. Abra o Windows PowerShell e execute Olá os seguintes comandos:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse o adaptador recém-registado, Editar política de autenticação global Olá no AD FS. Na consola de gestão do Olá AD FS, aceda toohello **políticas de autenticação** nós. No Olá **multi-factor Authentication** secção, clique em Olá **editar** ligação seguinte toohello **definições globais** secção. No Olá **Editar política de autenticação Global** janela, selecione **multi-factor Authentication** como método de autenticação adicional e, em seguida, clique em **OK**. adaptador de Olá está registado como WindowsAzureMultiFactorAuthentication. Reinicie Olá AD FS serviço para o efeito de tootake Olá registo.

<center>![Nuvem](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

Neste momento, servidor multi-factor Authentication está definida toobe um toouse do fornecedor de autenticação adicional com o AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Instalar uma instância autónoma do adaptador de Olá do AD FS utilizando Olá SDK do serviço Web
1. Instale Olá SDK do serviço Web no servidor de Olá que está a executar o servidor multi-factor Authentication.
2. Seguinte Olá de copiar ficheiros a partir de \Program Olá-servidor-factor Authentication diretório toohello no qual planeia adaptador do tooinstall Olá AD FS:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Execute o ficheiro de instalação MultiFactorAuthenticationAdfsAdapterSetup64.msi Olá.
4. No instalador do adaptador Olá multi-factor Authentication. o AD FS, clique em **seguinte** instalação de Olá toostart.
5. Clique em **fechar** quando Olá instalação estiver terminada.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Editar o ficheiro multifactorauthenticationadfsadapter. config de Olá
Siga o ficheiro do multifactorauthenticationadfsadapter. config tooedit Olá estes passos:

1. Conjunto Olá **usewebservicesdk como** nó demasiado**verdadeiro**.  
2. Definir o valor de Olá para **WebServiceSdkUrl** toohello URL de Olá Web Service SDK do multi-factor Authentication. Por exemplo: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, onde *certificatename* é Olá nome do seu certificado.  
3. Edite o script de Olá register-multifactorauthenticationadfsadapter.ps1 adicionando *- ConfigurationFilePath &lt;caminho&gt;*  final toohello Olá `Register-AdfsAuthenticationProvider` comando, onde  *&lt;caminho&gt;*  é o ficheiro multifactorauthenticationadfsadapter. config do Olá caminho completo toohello.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Configurar Olá SDK do serviço Web com um nome de utilizador e palavra-passe
Existem duas opções para configurar Olá Web Service SDK. Olá pela primeira vez com um nome de utilizador e palavra-passe, Olá segundo está com um certificado de cliente. Siga estes passos para a opção de primeiro Olá ou avançar diretamente para Olá segundo.  

1. Definir o valor de Olá para **WebServiceSdkUsername** tooan conta que seja membro do grupo de segurança PhoneFactor Admins de Olá. Olá utilize &lt;domínio&gt;&#92;&lt; nome de utilizador&gt; formato.  
2. Definir o valor de Olá para **WebServiceSdkPassword** toohello palavra-passe de conta apropriada.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Configurar Olá SDK do serviço Web com um certificado de cliente
Se não quiser toouse um nome de utilizador e palavra-passe, siga estes passos de Olá tooconfigure SDK do serviço Web com um certificado de cliente.

1. Obtenha um certificado de cliente de uma autoridade de certificação para o servidor de Olá que está a executar Olá Web Service SDK. Saiba como demasiado[obter certificados de cliente](https://technet.microsoft.com/library/cc770328.aspx).  
2. Importar Olá cliente certificado toohello computador local arquivo de certificados pessoais no servidor de Olá que está a executar Olá Web Service SDK. Certifique-se o que certificado público da autoridade de certificação que Olá está no arquivo de certificados de certificados de raiz fidedigna.  
3. Exporte chaves públicas e privadas Olá de Olá cliente certificado tooa. pfx.  
4. Exporte a chave pública do Olá Base64 tooa. cer no ficheiro em formato.  
5. No Gestor de servidores, certifique-se a funcionalidade de autenticação de mapeamento de certificados de cliente de \Web Server\Security\IIS que Olá servidor Web (IIS) está instalada. Se não estiver instalado, selecione **para adicionar funções e funcionalidades** tooadd esta funcionalidade.  
6. No Gestor de IIS, faça duplo clique em **Editor de configuração** num Web site Olá que contém o diretório virtual do SDK do serviço Web Olá. É importante tooselect Olá Web site, não Olá diretório virtual.  
7. Aceda toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** secção.  
8. Conjunto ativado demasiado**verdadeiro**.  
9. Defina oneToOneCertificateMappingsEnabled demasiado**verdadeiro**.  
10. Clique em Olá **...**  botão toooneToOneMappings seguinte e, em seguida, clique em Olá **adicionar** ligação.  
11. Abra o ficheiro. cer de Base64 Olá que exportou anteriormente. Remova *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* e quaisquer quebras de linha. Copie a cadeia resultante Olá.  
12. Conjunto de certificado toohello cadeia copiada no Olá precedente passo.  
13. Conjunto ativado demasiado**verdadeiro**.  
14. Definir o nome de utilizador tooan conta que seja membro do grupo de segurança PhoneFactor Admins de Olá. Olá utilize &lt;domínio&gt;&#92;&lt; nome de utilizador&gt; formato.  
15. Definir a palavra-passe de conta adequada de toohello de palavra-passe Olá e, em seguida, feche o Editor de configuração.  
16. Clique em Olá **aplicar** ligação.  
17. No diretório virtual do SDK do serviço Web de Olá, faça duplo clique em **autenticação**.  
18. Certifique-se de que representação do ASP.NET e a autenticação básica estão definidas demasiado**ativado**, e que todos os outros itens estão definidos demasiado**desativado**.  
19. No diretório virtual do SDK do serviço Web de Olá, faça duplo clique em **as definições de SSL**.  
20. Definir certificados de cliente demasiado**aceitar**e, em seguida, clique em **aplicar**.  
21. Copie Olá. pfx que exportou anteriormente servidor toohello que está a executar Olá adaptador AD FS.  
22. Importe o arquivo de certificados pessoais do computador local do Olá. pfx ficheiro toohello.  
23. Clique com botão direito e selecione **gerir chaves privadas**e, em seguida, conceder acesso de leitura toohello conta que utilizou toosign no serviço do toohello AD FS.  
24. Abrir Olá cliente certificado e copie Olá thumbprint a partir do Olá **detalhes** separador.  
25. No ficheiro multifactorauthenticationadfsadapter. config de Olá, defina **WebServiceSdkCertificateThumbprint** toohello cadeia copiada no passo anterior Olá.  

Por fim, tooregister Olá adaptador, execute Olá \Program-script fator files\multi-factor Authentication Server\register-multifactorauthenticationadfsadapter.ps1 no PowerShell. adaptador de Olá está registado como WindowsAzureMultiFactorAuthentication. Reinicie Olá AD FS serviço para o efeito de tootake Olá registo.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Proteger recursos do Azure AD com o AD FS
toosecure o recurso da nuvem, configure uma regra de afirmações para que os serviços de Federação do Active Directory emite Olá multipleauthn afirmação quando um utilizador efetua a verificação com êxito. Esta afirmação é transmitida tooAzure AD. Siga este toowalk procedimento passos Olá:

1. Abra a Gestão do AD FS.
2. Olá esquerda, selecione **confianças da entidade Confiadora**.
3. Clique com o botão direito do rato na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Afirmação...**

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Em Regras de Transformação da Emissão, clique em **Adicionar Regra.**

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. No Olá Adicionar Assistente de regra de afirmação de transformação, selecione **passar ou filtrar uma afirmação de entrada** de Olá pendente e clique em **seguinte**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Dê um nome à sua regra.
7. Selecione **referências dos métodos de autenticação** como Olá entrada de tipo de afirmação.
8. Selecione **Passar todos os valores de afirmação**.
    ![Assistente para Adicionar Regra de Afirmação de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Clique em **Concluir**. Feche a consola de gestão FS Olá AD.

## <a name="related-topics"></a>Tópicos relacionados
Para obter ajuda de resolução de problemas, consulte Olá [perguntas mais frequentes do Azure multi-factor Authentication](multi-factor-authentication-faq.md)
