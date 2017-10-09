---
title: recursos de nuvem aaaSecure MFA do Azure e do AD FS | Microsoft Docs
description: "Este é Olá multi-factor authentication página que descreve como tooget utilizar a MFA do Azure e o AD FS na nuvem de Olá."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Proteger recursos da nuvem com o Multi-Factor Authentication do Azure e o AD FS
Se a sua organização estiver federada com o Azure Active Directory, utilize o multi-factor Authentication do Azure ou recursos de toosecure de serviços de Federação do Active Directory (AD FS) que sejam acedidos pelo Azure AD. Utilize Olá os seguintes recursos do Azure Active Directory de toosecure de procedimentos com multi-factor Authentication do Azure ou serviços de Federação do Active Directory.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Proteger recursos do Azure AD com o AD FS
toosecure o recurso da nuvem, configure uma regra de afirmações para que os serviços de Federação do Active Directory emite Olá multipleauthn afirmação quando um utilizador efetua a verificação com êxito. Esta afirmação é transmitida tooAzure AD. Siga este toowalk procedimento passos Olá:


1. Abra a Gestão do AD FS.
2. Olá esquerda, selecione **confianças da entidade Confiadora**.
3. Clique com o botão direito do rato na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Afirmação**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Em Regras de Transformação da Emissão, clique em **Adicionar Regra**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. No Olá Adicionar Assistente de regra de afirmação de transformação, selecione **passar ou filtrar uma afirmação de entrada** de Olá pendente e clique em **seguinte**.

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Dê um nome à sua regra. 
7. Selecione **referências dos métodos de autenticação** como Olá entrada de tipo de afirmação.
8. Selecione **Passar todos os valores de afirmação**.
    ![Assistente para Adicionar Regra de Afirmação de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Clique em **Concluir**. Feche a consola de gestão FS Olá AD.

## <a name="trusted-ips-for-federated-users"></a>IPs Fidedignos para utilizadores federados
IPs fidedignos permitem aos administradores de verificação de dois passos tooby passagem para endereços IP específicos, ou para os utilizadores federados que tenham pedidos com origem na sua própria intranet. Olá secções seguintes descrevem como tooconfigure multi-factor Authentication do Azure fidedigna IPs com utilizadores federados e ignorar a verificação quando um pedido tem origem dentro de uma intranet de utilizadores federados. Isto é conseguido através da configuração do AD FS toouse um pass-through ou filtrar um modelo de afirmação de entrada com Olá tipo de afirmação dentro da rede empresarial.

Este exemplo utiliza o Office 365 para as Confianças de Entidades Confiadoras.

### <a name="configure-hello-ad-fs-claims-rules"></a>Configurar regras de afirmações Olá do AD FS
Olá primeira coisa toodo é tooconfigure Olá do AD FS afirmações. Criar duas regras de afirmações, uma para Olá dentro da rede empresarial de afirmações de tipo e uma adicional para manter os utilizadores com sessão iniciados.

1. Abra a Gestão do AD FS.
2. Olá esquerda, selecione **confianças da entidade Confiadora**.
3. Clique com o botão direito do rato na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Afirmação**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Em Regras de Transformação da Emissão, clique em **Adicionar Regra.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. No Olá Adicionar Assistente de regra de afirmação de transformação, selecione **passar ou filtrar uma afirmação de entrada** de Olá pendente e clique em **seguinte**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. No Olá caixa seguinte tooClaim nome da regra, atribua a regra, um nome. Por exemplo: InsideCorpNet.
7. Na lista pendente Olá, tooIncoming seguinte tipo de afirmação, selecione **dentro da rede empresarial**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Clique em **Concluir**.
9. Em Regras de Transformação da Emissão, clique em **Adicionar Regra**.
10. No Olá Adicionar Assistente de regra de afirmação de transformação, selecione **enviar afirmações utilizando uma regra personalizada** de Olá pendente e clique em **seguinte**.
11. Na caixa de Olá em nome da regra de afirmação: introduza *manter os utilizadores com sessão iniciada no*.
12. Na caixa de regra personalizada de Olá, introduza:

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Clique em **Concluir**.
14. Clique em **Aplicar**.
15. Clique em **OK**.
16. Feche a Gestão do AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Configurar IPs Fidedignos do Multi-Factor Authentication do Azure com Utilizadores Federados
Agora que Olá afirmações estão ativadas, podemos configurar IPs fidedignos.

1. Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Olá esquerda, clique em **do Active Directory**.
3. No diretório, selecione o diretório de olá onde pretende tooset configurar IPs fidedignos.
4. No diretório que selecionou Olá, clique em **configurar**.
5. Na secção de autenticação multifator Olá, clique em **gerir definições do serviço**.
6. Na página de definições do serviço de Olá, em IPs fidedignos, selecione **ignorar várias-factor-autenticação para pedidos de utilizadores federados na minha intranet**.  

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Clique em **Guardar**.
8. Depois de tem sido aplicadas Olá atualizações, clique em **fechar**.

Já está! Neste momento, os utilizadores federados do Office 365 só devem ter toouse MFA quando uma afirmação tiver origem a partir da intranet de empresa Olá fora.
