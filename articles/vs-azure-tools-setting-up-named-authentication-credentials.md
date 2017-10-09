---
title: "aaaSetting cópias de segurança denominado as credenciais de autenticação | Microsoft Docs"
description: "Saiba como o serviço em nuvem credenciais tootooprovide que o Visual Studio podem utilizar tooauthenticate pedidos tooAzure toopublish tooAzure uma aplicação do Visual Studio ou toomonitor existente... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Configurar as credenciais de autenticação com o nome
toopublish tooAzure uma aplicação do Visual Studio ou toomonitor um serviço em nuvem existente, tem de fornecer credenciais que o Visual Studio podem utilizar tooauthenticate pedidos tooAzure. Existem vários locais no Visual Studio, onde pode iniciar sessão tooprovide estas credenciais. Por exemplo, de Olá Explorador de servidores, pode abrir o menu de atalho Olá para Olá **Azure** nós e escolher **ligar tooMicrosoft subscrição do Azure...** . Quando iniciar sessão, as informações de subscrição de Olá associadas à conta do Azure estão disponíveis no Visual Studio e tiver toodo mais nada.

Ferramentas do Azure também suporta uma forma mais antiga de fornecer credenciais, utilizando o ficheiro de subscrição de Olá (ficheiro. publishsettings). Este tópico descreve este método, que ainda é suportado no Azure SDK 2.2.

Olá seguintes itens é necessário para autenticação tooAzure:

* O ID de subscrição
* Um certificado válido de x. 509v3

> [!NOTE]
> o comprimento de chave do certificado x. 509 v3 de Olá Olá tem de ser, pelo menos, 2048 bits. Azure irá rejeitar qualquer certificado que não cumpram este requisito ou que não é válido.
>
>

Visual Studio utiliza o ID de subscrição, juntamente com dados de certificado Olá como credenciais. as credenciais adequadas Olá são referenciadas no ficheiro de subscrição de Olá (ficheiro. publishsettings), que contém uma chave pública do certificado de Olá. ficheiro de subscrição de Olá pode conter as credenciais para a mais do que uma subscrição.

Pode editar as informações de subscrição de Olá de Olá **New/editar subscrição** caixa de diálogo, conforme explicado posteriormente neste tópico.

Se quiser toocreate um certificado por si, pode consultar toohello instruções [criar e carregar um certificado de gestão para o Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e, em seguida, carregar manualmente Olá certificado toohello [portal clássico do Azure ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Estas credenciais que o Visual Studio requer toomanage que seus serviços em nuvem não são Olá mesmas credenciais que são necessária tooauthenticate um pedido de serviços do storage do Azure Olá.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>Importar, definir ou editar credenciais de autenticação no Visual Studio
Pode importar, definir ou modificar as credenciais de autenticação no Olá **nova subscrição** caixa de diálogo, que é apresentada se efetuar Olá seguinte ação:

* No **Explorador de servidores**, abra menu de atalho Olá para Olá **Azure** nós, escolha **gerir e subscrições de filtro...** , escolha Olá **certificados** separador e efetue um dos seguintes Olá:

    * Escolha **importar** onde pode transferir ficheiros de subscrições Olá para Olá atualmente tooopen caixa de diálogo de importar as subscrições do Microsoft Azure de Olá carregar a subscrição, procurar tooits localização da transferência e, em seguida, importá-lo para utilização no autenticação.
    * Escolha **novo** onde pode configurar uma nova subscrição para utilização na autenticação tooopen caixa de diálogo de nova subscrição de Olá.
    * Escolha **editar** (depois de escolher a sua subscrição do Active Directory) onde pode editar uma subscrição existente para utilizar na autenticação tooopen caixa de diálogo de editar subscrição de Olá. 

Olá procedimento assume que Olá **nova subscrição** caixa de diálogo está aberta.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>tooset das credenciais de autenticação no Visual Studio
1. No Olá **selecionar um certificado existente** para lista de autenticação, selecione um certificado.
2. Escolha Olá **caminho completo do cópia Olá** ligação. caminho de Olá certificado Olá (ficheiro. cer) é copiado toohello da área de transferência.

   > [!IMPORTANT]
   > toopublish a aplicação do Azure a partir do Visual Studio, tem de carregar este certificado toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. tooupload Olá certificado toohello portal do Azure:

   1. Abra Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. Se lhe for solicitado, inicie sessão no portal de toohello e, em seguida, navegue até demasiado**definições**, **certificados de gestão**.
   3. No painel de certificados de gestão de Olá, escolha **carregar**.
   4. Selecione a sua subscrição do Azure, cole o caminho completo do Olá do ficheiro. cer Olá que acabou de criar e escolha **carregar**.
