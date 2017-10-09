---
title: "aaaGet à Azure Search no Node.js | Microsoft Docs"
description: "Instruções sobre a compilação de uma aplicação de pesquisa num serviço de pesquisa na cloud alojado no Azure utilizando Node.js como linguagem de programação."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Introdução à Azure Search no Node.js
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Saiba como toobuild um Node.js personalizado procure a aplicação que utiliza a Azure Search pela sua experiência de pesquisa. Este tutorial utiliza Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Olá objetos e as operações utilizados neste exercício.

Utilizámos [Node.js](https://Nodejs.org) e NPM, [Sublime Text 3](http://www.sublimetext.com/3)e o Windows PowerShell no Windows 8.1 toodevelop e testar este código.

toorun neste exemplo, tem de ter um serviço de pesquisa do Azure, pode inscrever-se no Olá [portal do Azure](https://portal.azure.com). Consulte [criar um serviço da Azure Search no portal de Olá](search-create-service-portal.md) para obter instruções passo a passo.

## <a name="about-hello-data"></a>Sobre os dados de Olá
Esta aplicação de exemplo utiliza dados dos Olá [serviços geológicos dos Estados Unidos (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)filtrados no tamanho de conjunto de dados do Olá estado da Rhode Island tooreduce Olá. Utilizaremos esta toobuild dados de uma aplicação de pesquisa que devolve edifícios históricos, tais como hospitais e escolas, assim como características funcionalidades, como rios, lagos e cumes.

Nesta aplicação, Olá **DataIndexer** programa compila e carrega Olá índice utilizando uma [indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construção, obter Olá filtrado de dados USGS de uma base de dados de SQL pública do Azure. As credenciais e ligação de origem de dados online toohello informações é fornecida no código do programa de Olá. Não é necessária qualquer configuração adicional.

> [!NOTE]
> Aplicamos um filtro toostay este conjunto de dados no limite de 10 000 documentos Olá de Olá escalão de preço gratuito. Se utilizar o escalão standard Olá, este limite não é aplicável. Para obter detalhes sobre a capacidade para cada escalão de preço, consulte [limites do Serviço de Pesquisa](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Localizar o nome do serviço Olá e chave de api do serviço da Azure Search
Depois de criar serviço Olá, devolver toohello portal tooget Olá URL ou `api-key`. Ligações tooyour serviço Search requerem que tenha o URL Olá e um `api-key` chamada de Olá tooauthenticate.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Na barra de índice de Olá, clique em **serviço de pesquisa** toolist todos os serviços da Azure Search aprovisionados para a sua subscrição.
3. Selecione Olá serviço toouse.
4. No dashboard do serviço de Olá, verá os mosaicos com informações essenciais, tais como o ícone da chave Olá para aceder às chaves de administração de Olá.
5. Copie o URL do serviço Olá, uma chave de administração e uma chave de consulta. Precisa de três mais tarde quando os adicionar ficheiro de config.js toohello.

## <a name="download-hello-sample-files"></a>Transferir ficheiros de exemplo de Olá
Utilize uma das Olá seguinte exemplo de Olá toodownload de abordagens.

1. Aceda demasiado[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Clique em **transferir ZIP**, guarde o ficheiro. zip de Olá e, em seguida, extraia todos os ficheiros de Olá nele contidos.

Todas as modificações do ficheiro e instruções de execução subsequentes são realizadas em ficheiros nesta pasta.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Atualize Olá config.js. com o seu URL do serviço Search e a chave de API
Utilizar Olá URL e a chave de api que copiou anteriormente, especifique o URL de Olá, chave de administrador e a chave de consulta no ficheiro de configuração.

As chaves de administração concedem um controlo total sobre as operações de serviço, incluindo criar ou eliminar um índice e carregar documentos. Em contrapartida, as chaves de consulta são para operações só de leitura, normalmente utilizadas por aplicações cliente que se ligam tooAzure pesquisa.

Neste exemplo, incluímos consulta Olá toohelp chave impor Olá melhor prática em utilizar a chave de consulta de Olá em aplicações cliente.

Olá seguinte captura de ecrã mostra **config.js** aberto num editor de texto, com Olá entradas relevantes demarcadas para que possa ver onde o ficheiro de Olá tooupdate com Olá valores que do são válidas para o serviço de pesquisa.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Alojar um ambiente de tempo de execução para o exemplo de Olá
exemplo de Olá requer um servidor HTTP, o que pode instalar globalmente utilizando npm.

Utilize uma janela do PowerShell para Olá os seguintes comandos.

1. Navegue toohello pasta que contém Olá **Package. JSON** ficheiro.
2. Digite `npm install`.
3. Digite `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Criar o índice de Olá e executar a aplicação Olá
1. Digite `npm run indexDocuments`.
2. Digite `npm run build`.
3. Digite `npm run start_server`.
4. Direcione o seu browser para `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Pesquisar nos dados USGS
conjunto de dados do Olá USGS inclui registos que são relevante toohello estado da Rhode Island. Se clicar em **pesquisa** numa caixa de pesquisa em branco, a obter entradas de principais 50 de Olá, Olá predefinido.

Introduzir um termo de pesquisa dá-motor de busca Olá algo toogo no. Tente introduzir um nome regional. "Roger Williams" foi o primeiro Governador de Olá de Rhode Island. Existem vários parques, edifícios e escolas com o seu nome.

![][9]

Também pode tentar qualquer um destes termos:

* Pawtucket
* Pembroke
* ganso +cabo

## <a name="next-steps"></a>Passos seguintes
Este é Olá primeiro tutorial da Azure Search com base no Node.js e Olá dados USGS. Ao longo do tempo, iremos irá expandir este tutorial toodemonstrate funcionalidades adicionais de pesquisa é aconselhável toouse nas suas soluções personalizadas.

Se já tiver algum conhecimento sobre a Azure Search, pode utilizar este exemplo como ponto de partida para tentar sugestores (escrita antecipada ou consultas de conclusão automática), filtros e navegação por facetas. Também pode melhorar Olá página de resultados de pesquisa ao adicionar contagens e criação de batches de documentos para que os utilizadores possam percorrer os resultados de Olá.

TooAzure nova pesquisa? Recomendamos que tentar toodevelop outros tutoriais compreender de que pode criar. Visite a nossa [página de documentação](https://azure.microsoft.com/documentation/services/search/) toofind mais recursos. Também pode ver as ligações de Olá no nosso [lista de vídeos e tutoriais](search-video-demo-tutorial-list.md) tooaccess obter mais informações.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
