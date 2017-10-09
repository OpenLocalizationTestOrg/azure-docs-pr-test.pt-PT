---
title: certificados de aaaUsing com Enterprise Integration Pack | Microsoft Docs
description: "Saiba como toouse certificados com Olá Enterprise Integration Pack | Aplicações lógicas do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>Mais informações sobre certificados e o Enterprise Integration Pack
## <a name="overview"></a>Descrição geral
Integração empresarial com utiliza comunicações de B2B toosecure de certificados. Pode utilizar dois tipos de certificados nas suas aplicações de integração do enterprise:

* Certificados públicos, tem de ser adquiridos de uma autoridade de certificação (AC).
* Certificados privados, pode emitir por si. Estes certificados são, por vezes, os certificados autoassinados tooas referenciado.

## <a name="what-are-certificates"></a>Quais são os certificados?
Os certificados são digitais documentos que verifique se a identidade Olá participantes Olá eletrónicas comunicações e que também protege as comunicações eletrónicas.

## <a name="why-use-certificates"></a>Porquê utilizar certificados?
Por vezes, comunicações B2B têm de ser mantidas confidenciais. Integração empresarial com utiliza certificados toosecure estas comunicações de duas formas:

* Ao encriptar o conteúdo de Olá de mensagens em fila
* Ao assinar digitalmente mensagens  

## <a name="upload-a-public-certificate"></a>Carregar um certificado público

toouse um *certificado público* nas suas logic apps com capacidades de B2B, primeiro tem de certificado de Olá tooupload na sua conta de integração.  

Depois de carregar um certificado, estão disponível toohelp proteger as mensagens B2B quando definir as respetivas propriedades no Olá [contratos](logic-apps-enterprise-integration-agreements.md) que criar.  

Seguem-se Olá os passos detalhados para carregar os certificados públicos na sua conta de integração, depois de se inscrever no toohello portal do Azure:

1. Selecione **mais serviços** e introduza **integração** na caixa de pesquisa de filtro de Olá. Selecione **contas de automatização** da lista de resultados de Olá     
![Selecione procurar](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Selecione Olá integração conta toowhich pretende que o certificado de Olá tooadd.  
![Selecione Olá integração conta toowhich pretende que o certificado de Olá tooadd](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Selecione Olá **certificados** mosaico.  
![Mosaico de Olá selecione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. No Olá **certificados** painel que abre, selecione de Olá **adicionar** botão.   
![Selecione o botão de adição de Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Introduza um **nome** de certificado e Olá, em seguida, selecione o tipo de certificado como **pública** de Olá pendente.  
6. Ícone de pasta Olá selecione no lado direito de Olá de Olá **certificado** caixa de texto. Quando abre o seleccionador de ficheiros de Olá, localize e selecione o ficheiro de certificado Olá que pretende que a conta de integração de tooyour tooupload.
7. Selecione o certificado de Olá e, em seguida, selecione **OK** no seleccionador de ficheiros de Olá. Isto valida e carrega a conta de integração do Olá certificados tooyour.
8. Por fim, fazer uma cópia no Olá **adicionar certificado** painel, selecione de Olá **OK** botão.  
![Selecione o botão OK Olá](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Selecione Olá **certificados** mosaico. Deverá ver Olá recentemente adicionado o certificado.  
![Ver o novo certificado de Olá](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Carregar um certificado privado

toouse um *certificado privado* nas suas logic apps com B2B capacidades, pode carregar uma conta de integração do certificado privado tooyour ao hello efetuando os passos seguintes

1. [Carregar o seu Cofre de tooKey chave privada](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de chaves") e fornecer um **nome da chave** 
   
   > [!TIP]
   > Tem de autorizar operações de tooperform Logic Apps no Cofre de chaves. Pode conceder principal de serviço do acesso toohello Logic Apps utilizando Olá seguinte comando do PowerShell:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Depois de ter sido passo anterior Olá, adicione uma conta de toointegration certificado privado.

Seguintes são Olá os passos detalhados para carregar os certificados privados na sua conta de integração, depois de se inscrever no toohello portal do Azure:  
 
1. Selecione a conta de integração do Olá toowhich que pretende o certificado de Olá tooadd e selecione Olá **certificados** mosaico.  
![Mosaico de Olá selecione certificados](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. No Olá **certificados** painel que abre, selecione de Olá **adicionar** botão.   
![Selecione o botão de adição de Olá](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Introduza um **nome** de certificado e Olá selecione o tipo de certificado como **privada** de Olá pendente.   
4. Selecione o ícone de pasta Olá no lado direito de Olá de Olá **certificado** caixa de texto. Quando abre o seleccionador de ficheiros de Olá, localize Olá de certificado pública correspondente que pretende que a conta de integração de tooyour tooupload.   
   
   > [!Note]
   > Ao adicionar um certificado privado é importante tooadd correspondente pública do certificado tooshow no [contratos AS2](logic-apps-enterprise-integration-as2.md) receber e enviar as definições de assinatura e encriptação de mensagens hello.
   > 
   >   

5. Selecione Olá **grupo de recursos**, **Cofre de chaves**, **nome da chave** e selecione Olá **OK** botão.  
![Adicionar certificado](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Selecione Olá **certificados** mosaico. Deverá ver Olá recentemente adicionado o certificado.
![Ver o novo certificado de Olá](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Criar um contrato de B2B](logic-apps-enterprise-integration-agreements.md)  
* [Saiba mais sobre o Cofre de chaves](../key-vault/key-vault-get-started.md "Saiba mais sobre o Cofre de chaves")  

