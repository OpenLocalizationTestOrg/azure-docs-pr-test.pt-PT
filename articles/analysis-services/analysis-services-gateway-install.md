---
title: gateway de dados no local aaaInstall | Microsoft Docs
description: Saiba como tooinstall e configure um gateway de dados no local.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Instalar e configurar um gateway de dados no local
É necessário um gateway de dados no local quando um ou mais servidores do Azure Analysis Services no Olá mesma região ligar a origens de dados de tooon local. toolearn mais sobre o gateway de Olá, consulte [gateway de dados no local](analysis-services-gateway.md).

## <a name="prerequisites"></a>Pré-requisitos
**Requisitos mínimos:**

* 4.5 do .NET framework
* versão de 64 bits do Windows 7 / Windows Server 2008 R2 (ou posterior)

**Recomendado:**

* CPU de 8 núcleos
* 8 GB de memória
* versão de 64 bits do Windows 2012 R2 (ou posterior)

**Considerações importantes sobre:**

* Durante a configuração, quando registar o gateway com o Azure, a região predefinida de Olá para a sua subscrição está selecionada. Pode escolher uma região diferente. Se tiver servidores na região mais do que um, tem de instalar um gateway para cada região. 
* gateway de Olá não pode ser instalado num controlador de domínio.
* Apenas um gateway pode ser instalado num único computador.
* Instale o gateway de Olá num computador que permanece no e não passa toosleep.
* Não instale o gateway de Olá numa rede de computador tooyour wirelessly ligado. Desempenho pode ser o seu.


## <a name="download"></a>Transferir
 [Transfira o gateway de Olá](https://aka.ms/azureasgateway)

## <a name="install"></a>Instalar

1. Execute a configuração.

2. Selecione uma localização, aceite os termos de Olá e, em seguida, clique em **instalar**.

   ![Instalar os termos de localização e a licença](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Selecione **gateway de dados no local (recomendado)**. Azure Analysis Services não suporta o modo pessoal.

   ![Escolha o tipo de gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Introduza uma conta toosign tooAzure. Olá conta tem de ser do Azure Active Directory seu inquilino. Esta conta é utilizada para o administrador do gateway Olá. 

   ![Introduza uma conta toosign tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Se iniciar sessão com uma conta de domínio, será mapeada conta institucional tooyour no Azure AD. A conta institucional será utilizada como administrador do gateway Olá Olá.

## <a name="register"></a>Registar
Na ordem toocreate um recurso de gateway no Azure, tem de registar a instância local Olá instalado com Olá serviço em nuvem Gateway. 

1.  Selecione **registar um novo gateway neste computador**.

    ![Registar](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Escreva uma chave de recuperação e o nome do seu gateway. Por predefinição, o gateway de Olá utiliza região de predefinida da sua subscrição. Se precisar de tooselect região diferente, selecione **alteração região**.

   ![Registar](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Crie um recurso de gateway do Azure
Depois de ter instalado e registado o gateway, terá de toocreate um recurso de gateway na sua subscrição do Azure. A iniciar sessão tooAzure com Olá mesma conta que utilizou quando registar o gateway de Olá.

1. No portal do Azure, clique em **criar um novo serviço** > **integração empresarial com** > **gateway de dados no local**  >   **Criar**.

   ![Crie um recurso de gateway](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. No **criar gateway de ligação**, introduza estas definições:

    * **Nome**: introduza um nome para o recurso do gateway. 

    * **Subscrição**: selecione Olá tooassociate de subscrição do Azure com o recurso do gateway. 
    Esta subscrição deve ser Olá mesma subscrição, os servidores fizerem no.
   
      subscrição de predefinição Olá baseia Olá conta do Azure que utilizou toosign no.

    * **Grupo de recursos**: crie um grupo de recursos ou selecione um existente.

    * **Localização**: região Olá selecione registado o seu gateway.

    * **Nome de instalação**: se a instalação do gateway não estiver selecionada, o gateway de Olá selecione registado. 

    Quando tiver terminado, clique em **criar**.

## <a name="connect-servers"></a>Ligue o recurso de gateway toohello de servidores

1. Na descrição geral da sua do Azure Analysis Services server, clique em **Gateway de dados no local**.

   ![Ligar o servidor toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. No **escolher um Gateway de dados do On-Premises tooconnect**, selecione o recurso do gateway e, em seguida, clique em **gateway selecionado Connect**.

   ![Ligar recursos do servidor de toogateway](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Se o gateway não aparecer na lista de Olá, o servidor não se encontra provável num Olá mesma região que região Olá que especificou quando registar o gateway de Olá. 

E já está. Se precisar de portas de tooopen ou efetuar a qualquer resolução de problemas, ser toocheck se out [gateway de dados no local](analysis-services-gateway.md).

## <a name="next-steps"></a>Passos seguintes
* [Gerir do Analysis Services](analysis-services-manage.md)   
* [Obter dados a partir do Azure Analysis Services](analysis-services-connect.md)
