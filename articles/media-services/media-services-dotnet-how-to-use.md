---
title: "aaaHow tooSet computador cópias de segurança para o desenvolvimento de serviços de suporte de dados com o .NET"
description: "Saiba mais sobre Olá pré-requisitos para os Media Services utilizando Olá SDK de Media Services para .NET. Também saber como toocreate uma aplicação do Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>Desenvolvimento de Media Services com .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Este tópico descreve como serviços de multimédia de desenvolvimento de toostart aplicações através do .NET.

Olá **SDK .NET do Azure Media Services** biblioteca permite-lhe tooprogram nos serviços de suporte de dados através do .NET. toomake-mesmo toodevelop mais fácil com o .NET, hello **extensões do SDK .NET do Azure suporte de dados de serviços** biblioteca é fornecida. Esta biblioteca contém um conjunto de métodos de extensão e funções de programa auxiliar que simplificam o código de .NET. Ambas as bibliotecas estão disponíveis através de **NuGet** e **GitHub**.

## <a name="prerequisites"></a>Pré-requisitos
* Uma conta dos Media Services numa subscrição Azure nova ou existente. Consulte o tópico Olá [como tooCreate uma conta de Media Services](media-services-portal-create-account.md).
* Sistemas operativos: Windows 10, Windows 7, Windows 2008 R2 ou Windows 8.
* .NET framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Criar e configurar um projeto de Visual Studio
Esta secção mostra-lhe como toocreate um projeto no Visual Studio e defina-o para o desenvolvimento de Media Services.  Neste caso, projeto Olá é uma aplicação de consola c# Windows, mas hello mesmos passos de configuração mostrados aqui aplicam tooother tipos de projetos, que pode criar para aplicações de serviços de suporte de dados (por exemplo, uma aplicação do Windows Forms ou uma aplicação Web de ASP.NET).

Esta secção mostra como toouse **NuGet** tooadd SDK .NET dos Media Services extensões e outras bibliotecas dependentes.

Em alternativa, pode obter bits SDK .NET dos Media Services mais recentes do Olá a partir do GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) ou [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), construir solução Olá e adicionar as referências de Olá toohello projeto de cliente. Todas as dependências necessárias de Olá obterem transferiu e extraiu automaticamente.

1. Crie uma nova Aplicação de Consola C# no Visual Studio. Introduza Olá **nome**, **localização**, e **nome da solução**e, em seguida, clique em OK.
2. Compilar a solução de Olá.
3. Utilize **NuGet** tooinstall e adicione **extensões do SDK .NET do Azure suporte de dados de serviços** (**windowsazure.mediaservices.extensions**). Ao instalar este pacote, também é instalado o **SDK do .NET dos Media Services** e são adicionadas todas as outras dependências necessárias.
   
    Certifique-se de que tem a versão mais recente do Olá do NuGet instalado. Para obter mais instruções de instalação e informações, consulte [NuGet](http://nuget.codeplex.com/).
4. No Explorador de soluções, clique no nome de Olá do projeto de Olá e escolha pacotes NuGet gerir.
   
    é apresentada a caixa de diálogo Olá gerir pacotes NuGet.
5. Na Galeria de Olá Online, procure as extensões de MediaServices do Azure, escolha extensões do SDK .NET do Azure suporte de dados de serviços e, em seguida, clique no botão de instalação de Olá.
   
    projeto de Olá é modificado e referencia toohello extensões do SDK do .NET dos serviços de suporte de dados, SDK .NET dos Media Services, e são adicionadas outras assemblagens dependentes.
6. toopromote limpeza ambiente de desenvolvimento, considere ativar restauro do pacote NuGet. Para obter mais informações, consulte [restauro do pacote NuGet "](http://docs.nuget.org/consume/package-restore).
7. Adicione uma referência demasiado**System** assemblagem. Esta assemblagem contém Olá System. **ConfigurationManager** classe, ou seja, ficheiros de configuração tooaccess utilizados (por exemplo, App. config).
   
    referências de tooadd utilizando Olá a caixa de diálogo de referências de gerir, clique no nome do projeto Olá no Olá Explorador de soluções. Em seguida, selecione Adicionar e referências.
   
    é apresentada a caixa de diálogo do Olá referências de gerir.
8. Em assemblagens do .NET framework, localize e selecione a assemblagem de System Olá e prima OK.
9. Abra o ficheiro de App. config Olá e adicione um *appSettings* ficheiro toohello de secção.     
   
    Definir valores de Olá que são necessários tooconnect toohello API dos serviços de suporte de dados. Para obter mais informações, consulte [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

    Se estiver a utilizar [autenticação de utilizador](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) o ficheiro de configuração irá provavelmente têm valores para o seu domínio de inquilino do Azure AD e Olá ponto final de API de REST de AMS.
    
    >[!Important]
    >A maioria dos exemplos de código no Olá documentação de Media Services do Azure definir, utilize um tipo (interativo) de utilizador da autenticação tooconnect toohello API de AMS. Este método de autenticação irá funcionar bem para gestão ou de monitorização de aplicações nativas: as aplicações móveis, as aplicações do Windows e aplicações de consola. Este método de autenticação não é adequado para o servidor, serviços web, tipo APIs de aplicações.  Para obter mais informações, consulte [Olá de acesso AMS API com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Substituir a existente Olá **utilizando** instruções início Olá Olá Program.cs do ficheiro de com Olá seguinte código.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

Neste momento, está pronto toostart desenvolver uma aplicação dos Media Services.    

## <a name="example"></a>Exemplo

Eis um exemplo de pequeno que se liga toohello AMS API e apresenta uma lista de todos os processadores de suporte de dados disponíveis.
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>Passos seguintes

Agora [pode ligar toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) e iniciar [desenvolver](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

