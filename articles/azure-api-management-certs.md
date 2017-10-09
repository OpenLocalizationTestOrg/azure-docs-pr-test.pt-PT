---
title: "aaaUpload um certificado de API de gestão do Azure | Microsoft Docs"
description: "Saiba como tooupload athe API da gestão de certificados para Olá Portal clássico do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Carregar um certificado de gestão de API de gestão do Azure
Certificados de gestão permitem tooauthenticate com o modelo de implementação clássica Olá fornecido pelo Azure. Muitos programas e ferramentas (tais como o Visual Studio ou Olá SDK do Azure) utilizam estes configuração tooautomate de certificados e a implementação de vários serviços do Azure. 

> [!WARNING]
> Tenha cuidado! Estes tipos de certificados de permitir que qualquer pessoa que efetua a autenticação com os mesmos subscrição de Olá toomanage estão associados.
>
>

Se quiser obter mais informações sobre os certificados do Azure (incluindo a criar um certificado autoassinado), consulte o artigo [descrição geral de certificados para serviços de nuvem do Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Também pode utilizar [do Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-código de cliente para fins de automatização.

## <a name="upload-a-management-certificate"></a>Carregar um certificado de gestão
Depois de ter um certificado de gestão criado, (ficheiro. cer com apenas Olá chave pública) pode carregá-lo no portal de Olá. Quando estiver disponível no portal de Olá certificado de Olá, qualquer pessoa com um certificado correspondente (chave privada) pode ligar através de recursos de Olá de API de gestão e acesso Olá da Olá associado à subscrição.

1. Inicie sessão no toohello [portal do Azure](http://portal.azure.com).
2. Clique em **mais serviços** na lista de serviço do Azure do Olá na parte inferior, em seguida, selecione **subscrições** no Olá _geral_ grupo de serviço.

    ![Menu de subscrição](./media/azure-api-management-certs/subscriptions_menu.png)

3. Certifique-se tooselect Olá correta subscrição que pretende que o tooassociate com certificado Olá.     
4. Depois de selecionar a subscrição correta Olá, prima **certificados de gestão** no Olá _definições_ grupo.

    ![Definições](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Olá prima **carregar** botão.

    ![Carregar a página de certificados](./media/azure-api-management-certs/certificates_page.png)
6. Preencha as informações de caixa de diálogo Olá e prima **carregar**.

    ![Definições](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Passos seguintes
Agora que tem um certificado de gestão associado a uma subscrição, pode (após a instalação Olá correspondente ao certificado localmente) através de programação ligar toohello [REST API do modelo de implementação clássica](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizar Olá vários recursos do Azure que também estão associados essa subscrição.
