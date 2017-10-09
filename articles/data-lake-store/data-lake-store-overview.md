---
title: aaaOverview do Azure Data Lake Store | Microsoft Docs
description: "Compreender o que é o valor do Azure Data Lake Store e Olá fornece através de outros arquivos de dados"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Descrição geral do Azure Data Lake Store
O Azure Data Lake Store é um repositório de hiper escala a nível da empresa para cargas de trabalho de análise de macrodados. Azure Data Lake permite-lhe toocapture dados de qualquer tamanho, tipo e velocidade de ingestão num único local para análises exploratórias e operacionais.

> [!TIP]
> Olá utilize [percurso de aprendizagem do Data Lake Store](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart explorar Olá serviço de Azure Data Lake Store.
> 
> 

O Azure Data Lake Store pode ser acedido a partir do Hadoop (disponíveis com o cluster do HDInsight) utilizando Olá APIs de REST compatível com WebHDFS. É especificamente concebida tooenable análise dos dados de Olá armazenado e está otimizado para desempenho para cenários de análise de dados. Box Olá, inclui todas as capacidades de nível empresarial Olá — segurança, capacidade de gestão, escalabilidade, fiabilidade e disponibilidade — essenciais para casos de utilização empresarial reais.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Algumas das principais capacidades de Olá de Olá do Azure Data Lake incluem o seguinte Olá.

### <a name="built-for-hadoop"></a>Incorporado para o Hadoop
arquivo de Azure Data Lake Olá é um sistema de ficheiros Apache Hadoop compatível com distribuído ficheiro sistema Hadoop (HDFS) e funciona com o ecossistema do Hadoop Olá.  As aplicações do HDInsight ou serviços que utilizam Olá WebHDFS API existente podem ser facilmente integrados com o Data Lake Store. O Data Lake Store também expõe uma interface REST compatível com WebHDFS para aplicações

Os dados armazenados no Data Lake Store podem ser facilmente analisados utilizando as estruturas de análise de Hadoop, tais como MapReduce ou Hive. Clusters do Microsoft Azure HDInsight podem ser aprovisionados e configurados toodirectly aceder a dados armazenados no Data Lake Store.

### <a name="unlimited-storage-petabyte-files"></a>Armazenamento ilimitado, ficheiros petabyte
O Azure Data Lake Store fornece armazenamento ilimitado e é adequado para armazenar diversos dados para análise. Não tem quaisquer limites de tamanhos de conta, tamanhos de ficheiro ou Olá quantidade de dados que podem ser armazenados no data lake. Ficheiros individuais podem variar entre kilobytes toopetabytes tamanho toostore uma escolha ideal qualquer tipo de dados. Os dados são armazenados de forma durável fazendo várias cópias e não existe nenhum limite duração Olá de tempo para que Olá dados podem ser armazenados no lake de dados de Olá.

### <a name="performance-tuned-for-big-data-analytics"></a>Desempenho otimizado para análise de macrodados
O Azure Data Lake Store foi concebido para executar análise sistemas que necessitam de débito intenso tooquery e analisam grandes quantidades de dados de grande escala. Olá data lake propaga partes de um ficheiro através de um número de servidores de armazenamento individuais. Isto melhora a Olá débito de leitura ao ler o ficheiro de Olá em paralelo para efetuar análise de dados.

### <a name="enterprise-ready-highly-available-and-secure"></a>Pronto para empresas: elevada disponibilidade e segurança
O Azure Data Lake Store fornece disponibilidade e fiabilidade de norma da indústria. Os recursos de dados são armazenados de maneira duradoura efetuando cópias redundantes tooguard contra quaisquer falhas inesperadas. As empresas podem utilizar o Azure Data Lake nas respetivas soluções como uma parte importante da respetiva plataforma de dados.

Data Lake Store também fornece segurança de nível empresarial para os dados de Olá armazenado. Para obter mais informações, consulte o artigo [Proteger dados no Azure Data Lake Store](#DataLakeStoreSecurity).

### <a name="all-data"></a>Todos os Dados
O Azure Data Lake Store pode armazenar quaisquer dados no formato nativo, tal como está, sem necessidade de qualquer transformações anteriores. Arquivo data Lake não requerem um toobe esquema definida antes do carregamento dos dados de Olá, mantendo-os dados de Olá toohello estrutura de análise individual toointerpret e definir um esquema momento Olá da análise de Olá. Ser capaz de toostore ficheiros de formatos e tamanhos arbitrários torna possível para o Data Lake Store toohandle estruturado, dados estruturados, semi-estruturados e não estruturados.

Os contentores do Azure Data Lake Store para dados são essencialmente pastas e ficheiros. Operar em dados de Olá armazenado utilizando SDKs, o Portal do Azure e o Azure Powershell. Desde que coloque os dados para o arquivo de Olá utilizando estas interfaces e utilizando os contentores adequados Olá, pode armazenar qualquer tipo de dados. Data Lake Store não efetua qualquer processamento especial de dados com base no tipo de Olá de dados que armazena.

## <a name="DataLakeStoreSecurity"></a>Proteger dados no Azure Data Lake Store
O Azure Data Lake Store utiliza o Azure Active Directory para autenticação e listas de controlo de acesso (ACLs) toomanage aceder a dados tooyour.

| Funcionalidade | Descrição |
| --- | --- |
| Autenticação |O Azure Data Lake Store integra-se com o Azure Active Directory (AAD) para a gestão de identidades e acesso a todos os Olá dados armazenados no Azure Data Lake Store. Como resultado de integração de Olá, beneficia de Azure Data Lake de todas as funcionalidades do AAD, incluindo autenticação multifator, acesso condicional, controlo de acesso baseado em funções, monitorização de utilização de aplicações, monitorização de segurança e alertas, etc. O Azure Data Lake Store suporta Olá protocolo OAuth 2.0 para a autenticação com na interface REST de Olá. |
| Controlo de acesso |Azure Data Lake Store fornece controlo de acesso ao suportar permissões do estilo POSIX expostas pelo protocolo WebHDFS de Olá. No Olá pré-visualização pública do Data Lake Store (versão atual do Olá), ACLs podem ser ativados na pasta raiz de Olá, subpastas e ficheiros individuais. Para obter mais informações sobre como as ACLs funcionam no contexto do Data Lake Store, veja [Controlo de acesso no Data Lake Store](data-lake-store-access-control.md). |
| Encriptação |Data Lake Store também proporciona a encriptação dos dados armazenados na conta de Olá. Especifique as definições de encriptação de Olá ao criar uma conta de Data Lake Store. Pode toohave escolha os dados encriptados ou optar por sem encriptação. Para obter mais informações sobre como tooprovide relacionados com a encriptação configuração, consulte [introdução ao Azure Data Lake Store utilizando o Portal do Azure de Olá](data-lake-store-get-started-portal.md). |

Pretende toolearn mais sobre como proteger dados no Data Lake Store. Siga as ligações de Olá abaixo.

* Para obter instruções sobre como toosecure dados no Data Lake Store, consulte [proteger dados no Azure Data Lake Store](data-lake-store-secure-data.md).
* Prefere vídeos? [Veja este vídeo](https://mix.office.com/watch/1q2mgzh9nn5lx) na forma como toosecure dados armazenados no Data Lake Store.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Aplicações compatíveis com o Azure Data Lake Store
O Azure Data Lake Store é compatível com a maioria dos componentes de origem do ecossistema do Hadoop de Olá do. Também é integrado corretamente com outros serviços do Azure. Isto faz com que o Data Lake Store seja a opção perfeita para as suas necessidades de armazenamento de dados. Siga as ligações de Olá abaixo toolearn mais sobre como o Data Lake Store pode ser utilizado tanto com componentes de código aberto, bem como outros serviços do Azure.

* Consulte o artigo [Aplicações e serviços compatíveis com o Azure Data Lake Store](data-lake-store-compatible-oss-other-applications.md) para obter uma lista de aplicações de código aberto interoperáveis com o Data Lake Store.
* Consulte [integração com outros serviços do Azure](data-lake-store-integrate-with-other-services.md) toounderstand como o Data Lake Store pode ser utilizado com outro Azure serviços tooenable uma vasta gama de cenários.
* Consulte [cenários para utilizar o Data Lake Store](data-lake-store-data-scenarios.md) toolearn como toouse Data Lake armazenar em cenários, como a ingestão de dados, processamento de dados, transferir dados e visualizar dados.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>O que é o sistema de ficheiros do Azure Data Lake Store (adl: / /)?
Data Lake Store pode ser acedido através do novo sistema de ficheiros Olá, Olá AzureDataLakeFilesystem (adl: / /), em ambientes do Hadoop (disponíveis com o cluster do HDInsight). Aplicações e serviços que utilizam adl: / / são capazes de tootake partido da Otimização do desempenho que não estão atualmente disponíveis no WebHDFS. Como resultado, oferece de Data Lake Store Olá flexibilidade tooeither beneficiar melhor desempenho possível Olá com Olá recomendado a opção de utilização adl: / / ou manter o código existente ao continuar toouse Olá WebHDFS API diretamente. O Azure HDInsight tira total partido Olá AzureDataLakeFilesystem tooprovide Olá melhor desempenho no Data Lake Store.

Pode aceder os dados Olá Data Lake Store utilizando `adl://<data_lake_store_name>.azuredatalakestore.net`. Para obter mais informações sobre como tooaccess Olá dados Olá Data Lake Store, consulte [ver propriedades de Olá armazenados dados](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>Como começo a utilizar o Azure Data Lake Store?
Consulte [introdução ao Data Lake Store utilizando Olá Portal do Azure](data-lake-store-get-started-portal.md), no como tooprovision um Data Lake Store utilizando Olá Portal do Azure. Depois de ter aprovisionado do Azure Data Lake, pode saber como toouse ofertas de macrodados, tais como o Azure Data Lake Analytics ou o Azure HDInsight com o Data Lake Store. Também pode criar um toocreate de aplicações de .NET uma conta do Azure Data Lake Store e efetuar operações como carregamento de dados, a transferência de dados, etc.

* [Introdução ao Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Use Azure HDInsight with Data Lake Store (Utilizar o Azure HDInsight com o Data Lake Store)](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Introdução ao Azure Data Lake Store com SDK .NET](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Vídeos do Data Lake Store
Se preferir assistir a vídeos toolearn, o Data Lake Store fornece vídeos através de funcionalidades.

* [Criar uma Conta do Azure Data Lake Store](https://mix.office.com/watch/1k1cycy4l4gen)
* [Utilize o Explorador de dados de Olá tooManage dados no Azure Data Lake Store](https://mix.office.com/watch/icletrxrh6pc)
* [Ligar o Azure Data Lake Analytics tooAzure Data Lake Store](https://mix.office.com/watch/qwji0dc9rx9k)
* [Aceder ao Azure Data Lake Store através do Data Lake Analytics](https://mix.office.com/watch/1n0s45up381a8)
* [Ligar o Azure HDInsight tooAzure Data Lake Store](https://mix.office.com/watch/l93xri2yhtp2)
* [Aceder ao Azure Data Lake Store através do Hive e do Pig](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Utilizar o DistCp (cópia distribuída do Hadoop) toocopy dados tooand a partir do Azure Data Lake Store](https://mix.office.com/watch/1liuojvdx6sie)
* [Utilizar o Apache Sqoop toomove dados entre origens relacionais e o Azure Data Lake Store](https://mix.office.com/watch/1butcdjxmu114)
* [Orquestração de Dados com o Azure Data Factory para o Azure Data Lake Store](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Proteger dados em Olá Azure Data Lake Store](https://mix.office.com/watch/1q2mgzh9nn5lx)

