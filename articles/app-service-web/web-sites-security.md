---
title: "aaaSecure uma aplicação no App Service do Azure"
description: "Saiba como toosecure uma aplicação web, o back-end da aplicação móvel ou a aplicação API no App Service do Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Proteger uma aplicação Web Java no Serviço de Aplicações do Azure
Este artigo ajuda-o a começar em proteger a sua aplicação web, o back-end da aplicação móvel ou a aplicação API no App Service do Azure. 

A segurança no App Service do Azure tem dois níveis: 

* **Segurança de infraestrutura e plataforma** -tem de confiança do Azure toohave Olá serviços tooactually executar ações em segurança na nuvem de Olá.
* **Segurança da aplicação** -tem de forma segura toodesign Olá aplicação em si. Isto inclui como integrar com o Azure Active Directory, como gerir certificados e, como, certifique-se de que pode falar com segurança toodifferent serviços. 

#### <a name="infrastructure-and-platform-security"></a>Segurança de infraestrutura e plataforma
Porque o serviço de aplicações mantém Olá as VMs do Azure, armazenamento, ligações de rede, estruturas web, gestão e as funcionalidades de integração e muito mais, ativamente está protegida e protegido e passa através de conformidade vigorous e verifica se num toomake repetidamente que:

* As aplicações de serviço de aplicações estão isoladas de ambos os Olá Internet e da Olá recursos do Azure dos outros clientes.
* Comunicação de segredos (por exemplo, cadeias de ligação) entre a aplicação de serviço de aplicações e outros recursos do Azure (por exemplo, base de dados SQL) num grupo de recursos permanece no Azure e não cruzada quaisquer limites de rede. Os segredos são sempre encriptados.
* Todas as comunicações entre a aplicação de serviço de aplicações e recursos externos, como a gestão do PowerShell, a interface de linha de comandos, SDKs do Azure, REST APIs e as ligações híbridas, são encriptados corretamente.
* ameaças de 24 horas gestão protege os recursos do serviço de aplicações de software maligno, distribuída denial of service (DDoS) distribuídos, ataques man-in-the-middle (MITM) e outras ameaças. 

Para obter mais informações sobre a segurança da infraestrutura e plataforma no Azure, consulte [Centro de fidedignidade do Azure](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Segurança da aplicação
Enquanto é responsável por proteger a infraestrutura de Olá plataforma e que a aplicação for executada no Azure, é sua responsabilidade toosecure sua própria aplicação. Por outras palavras, terá de toodevelop, implementar e gerir o seu código da aplicação e o conteúdo de forma segura. Sem isto, o código da aplicação ou o conteúdo pode ainda ser toothreats vulnerável, tais como:

* Injeção de SQL
* Hijacking de sessão
* Em vários locais site scripting
* MITM ao nível da aplicação
* DDoS ao nível da aplicação

Ver um debate completo de considerações de segurança para aplicações baseadas na web ultrapassa o âmbito Olá deste documento. Como um ponto de partida para obter orientações sobre como proteger a sua aplicação, consulte Olá [aplicação do abra Web projeto segurança (OWASP)](https://www.owasp.org/index.php/Main_Page), especificamente Olá [10 principais projeto.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), que apresenta uma lista de Olá 10 superior atual web críticos aplicação falhas de segurança, conforme determinado pela membros OWASP.

## <a name="perform-penetration-testing-on-your-app"></a>Efetuar penetração teste na sua aplicação
Um dos Olá tooget de formas mais fácil começar a testar para vulnerabilidades na sua aplicação de serviço de aplicações é toouse Olá [integração com o Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) vulnerabilidade de um clique tooperform análise na sua aplicação. Pode ver os resultados do teste Olá num relatório fácil de compreender e saber como toofix cada vulnerabilidade com instruções passo a passo.

Se preferir tooperform a seus próprios penetração testes ou pretender toouse outro conjunto de scanner ou fornecedor, tem de seguir Olá [penetração do Azure, teste o processo de aprovação](https://security-forms.azure.com/penetration-testing/terms) e obter penetração de Olá pretendido tooperform de aprovação anterior os testes.

## <a name="https"></a>Proteger a comunicação com clientes
Se utilizar Olá  **\*. azurewebsites.net** nome de domínio criada para a sua aplicação de serviço de aplicações, pode utilizar imediatamente HTTPS, tal como é fornecido um certificado SSL para todos os  **\*. azurewebsites.net** nomes de domínio. Se o seu site utiliza um [nome de domínio personalizado](app-service-web-tutorial-custom-domain.md), pode carregar um certificado SSL demasiado[ativar HTTPS](app-service-web-tutorial-custom-ssl.md) para o domínio personalizado Olá.

Ativar [HTTPS](https://en.wikipedia.org/wiki/HTTPS) pode ajudar a proteger contra ataques MITM na comunicação de Olá entre a aplicação e os seus utilizadores.

## <a name="secure-data-tier"></a>Camada de dados seguros
Serviço de aplicações altamente integra-se a base de dados SQL, para que todas as cadeias de ligação de Olá são encriptadas em quadro Olá e só são desencriptadas no Olá VM essa aplicação Olá é executado no *e* apenas quando Olá execuções de aplicação. Além disso, SQL Database do Azure inclui muitas toohelp de funcionalidades de segurança a proteger os seus dados de aplicação de ameaças informático, incluindo [encriptação em rest](https://msdn.microsoft.com/library/dn948096.aspx), [sempre encriptados](https://msdn.microsoft.com/library/mt163865.aspx), [ Máscara de dados dinâmicos](../sql-database/sql-database-dynamic-data-masking-get-started.md), e [deteção de ameaças](../sql-database/sql-database-threat-detection.md). Se tiver dados confidenciais ou requisitos de conformidade, consulte o artigo [proteger a sua base de dados do SQL Server](../sql-database/sql-database-security-overview.md) para obter mais informações sobre como toosecure os dados.

Se utilizar um fornecedor de base de dados de terceiros, tais como ClearDB, deve consultar com a documentação do fornecedor de Olá diretamente no melhores práticas de segurança.  

## <a name="develop"></a>Proteger o desenvolvimento e implementação
### <a name="publishing-profiles-and-publish-settings"></a>Publicação de perfis e definições de publicação
Quando a desenvolver aplicações, executar tarefas de gestão ou automatização de tarefas, tais como a utilizar utilitários **Visual Studio**, **Web Matrix**, **Azure PowerShell** ou Olá **Interface de linha de comandos do azure (CLI do Azure)**, pode utilizar tanto um *definições de publicação* ficheiro ou uma *perfil de publicação*. Os tipos de ficheiro autenticar com o Azure e devem ser protegidos acesso tooprevent não autorizado.

* A **definições de publicação** ficheiro contém
  
  * O ID de subscrição do Azure
  * Um certificado de gestão que permite-lhe tooperform tarefas de gestão para a sua subscrição *sem ter tooprovide um nome de conta ou palavra-passe*.
* A **perfil de publicação** ficheiro contém
  
  * Informações de publicação de aplicação tooyour

Se utilizar um utilitário que utiliza um ficheiro de definições de publicação ou um ficheiro de perfil de publicação, importar ficheiro de Olá com definições de publicação Olá ou perfil no utilitário Olá e, em seguida, **eliminar** ficheiro Olá. Se é necessário manter o ficheiro de Olá, tooshare com outras pessoas a trabalhar num projeto Olá, por exemplo, armazene-o numa localização segura, tal como um *encriptados* diretório com permissões restritas.

Além disso, deve verificar se as credenciais de Olá importado são protegidas. Por exemplo, **Azure PowerShell** e Olá **Interface de linha de comandos do Azure (CLI do Azure)** ambos armazenam informação importada no seu **diretório raiz** ( *~*  nos sistemas Linux ou OS X e */utilizadores/yourusername* nos sistemas operativos Windows.) Para segurança adicional, pode ser útil demasiado**encriptar** estas localizações utilizando as ferramentas de encriptação disponíveis para o seu sistema operativo.

### <a name="configuration-settings-and-connection-strings"></a>Definições de configuração e as cadeias de ligação
É comum prática toostore as cadeias de ligação, credenciais de autenticação e outras informações confidenciais nos ficheiros de configuração. Infelizmente, estes ficheiros podem ser expostos no seu Web site ou selecionados para um repositório público, estas informações a exposição. Uma procura simple na [GitHub](https://github.com), por exemplo, pode descobrir countless ficheiros de configuração com segredos expostos no repositórios de Olá público.

Olá melhor prática é tookeep estas informações fora de ficheiros de configuração da sua aplicação. Serviço de aplicações permite-lhe armazenar informações de configuração como parte do ambiente de tempo de execução de Olá como **as definições de aplicação** e **cadeias de ligação**. os valores de Olá são expostos tooyour aplicação durante a execução através de *variáveis de ambiente* para a maioria das linguagens de programação. Para aplicações de .NET, estes valores são injetados a configuração do .NET no tempo de execução. Para além nestas situações, estas definições de configuração irão permanecem encriptadas, a menos que pode ver ou configura as propriedades utilizando Olá [Portal do Azure](https://portal.azure.com) ou utilitários, tais como o PowerShell ou Olá CLI do Azure. 

Armazenar as informações de configuração no App Service possibilita toolock de administrador da aplicação Olá baixo informações confidenciais para aplicações de produção Olá. Os programadores podem utilizar um conjunto separado de definições de configuração para o desenvolvimento de aplicações e definições de Olá podem ser automaticamente substituídas por definições de Olá configuradas no serviço de aplicações. Os programadores de Olá mesmo não tem de segredos de Olá tooknow configurados para a aplicação de produção Olá. Para obter mais informações sobre como configurar as definições de aplicação e cadeias de ligação no App Service, consulte [configurar aplicações web](web-sites-configure.md).

### <a name="ftps"></a>FTPS
App Service do Azure fornece seguro sistema de ficheiros do toohello de acesso FTP para a sua aplicação através de **FTPS**. Isto permite que toosecurely acesso Olá de código da aplicação Olá web app, bem como os diagnósticos registos. É recomendado que utilize sempre FTPS em vez de FTP. 

ligação FTPS Olá para a sua aplicação pode ser encontrada com Olá os seguintes passos:

1. Abra Olá [Portal do Azure](https://portal.azure.com).
2. Selecione **Procurar tudo**.
3. De Olá **procurar** painel, selecione **serviços aplicacionais**.
4. De Olá **serviços aplicacionais** painel, a aplicação pretendida Olá selecione.
5. No painel da aplicação Olá, selecione **todas as definições**.
6. De Olá **definições** painel, selecione **propriedades**.
7. Olá ligações de FTP/FTPS são fornecidas no Olá **definições** painel. 

Para obter mais informações sobre FTPS, consulte [protocolo de transferência de ficheiros](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Passos seguintes
Para mais informações sobre segurança Olá de Olá plataforma do Azure, informações sobre como reportar um **incidente de segurança ou abuso**, ou tooinform Microsoft que vão realizar **penetração testar** de sua site, consulte a secção de segurança de Olá de Olá [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Para mais informações sobre **Web. config** ou **applicationHost. config** ficheiros na aplicação do serviço de aplicações, consulte [opções de configuração foi desbloqueadas nas web apps do App Service do Azure](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Para obter informações sobre as informações de registo para aplicações de serviço de aplicações, que podem ser úteis na deteção de ataques, consulte [ativar o registo de diagnóstico](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

