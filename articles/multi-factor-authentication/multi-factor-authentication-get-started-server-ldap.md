---
title: "aaaLDAP autenticação e o servidor MFA do Azure | Microsoft Docs"
description: "Esta é Olá multi-factor authentication página que irá ajudar a implementar a autenticação LDAP e o servidor do Azure multi-factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>Autenticação LDAP e o servidor do Azure multi-factor Authentication
Por predefinição, hello do servidor do Azure multi-factor Authentication está configurado tooimport ou sincronizar utilizadores do Active Directory. No entanto, pode ser configurado toobind toodifferent de diretórios LDAP, tais como um diretório ADAM ou controlador de domínio do Active Directory específico. Quando o diretório de tooa ligado através de LDAP, hello do servidor multi-factor Authentication Azure pode atuar como um autenticações de tooperform do proxy LDAP. Também permite Olá utilização do enlace de LDAP como destino RADIUS, para pré-autenticação de utilizadores com a autenticação do IIS ou para autenticação primária no portal de utilizador do Olá MFA do Azure.

toouse Azure multi-factor Authentication como um proxy LDAP, inserir hello do servidor multi-factor Authentication Azure entre o cliente LDAP Olá (por exemplo, a aplicação VPN) e o servidor de diretório LDAP Olá. Olá servidor do Azure multi-factor Authentication tem de ser configurado toocommunicate com os servidores de cliente de Olá e o diretório LDAP Olá. Nesta configuração, hello do servidor multi-factor Authentication Azure aceita os pedidos LDAP dos servidores cliente e as aplicações e reencaminha-os toohello destino LDAP diretório toovalidate Olá primárias as credenciais do servidor. Se o diretório LDAP Olá valida as credenciais principais Olá, o multi-factor Authentication do Azure efetua uma verificação de identidade segundo e envia um cliente LDAP de back-toohello de resposta. autenticação completa Olá é concluída com êxito apenas se a autenticação de servidor LDAP Olá e verificação de segundo passo Olá concluída com êxito.

## <a name="configure-ldap-authentication"></a>Configurar a autenticação LDAP
autenticação no LDAP tooconfigure, Olá de instalação do servidor multi-factor Authentication Azure num servidor do Windows. Utilize Olá seguinte procedimento:

### <a name="add-an-ldap-client"></a>Adicionar um cliente LDAP

1. No servidor do Azure multi-factor Authentication Olá, selecione o ícone de autenticação LDAP Olá no menu à esquerda Olá.
2. Verifique Olá **ativar autenticação LDAP** caixa de verificação.

   ![Autenticação LDAP](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. No separador de clientes Olá, altere a porta TCP Olá e a porta SSL se Olá serviço Azure multi-factor Authentication LDAP vincular toonon padrão portas toolisten pedidos LDAP.
4. Se planear toouse LDAPS do Olá cliente toohello servidor do Azure multi-factor Authentication, um certificado SSL tem de estar instalado no Olá mesmo servidor que o servidor MFA. Clique em **procurar** toohello seguinte SSL certificado caixa e, selecione um certificado toouse para ligação segura Olá.
5. Clique em **Adicionar**.
6. Na caixa de diálogo Adicionar cliente LDAP de Olá, introduza o endereço IP de Olá da aplicação Olá, servidor ou aplicação que autentica toohello servidor e um nome de aplicação (opcional). nome da aplicação Olá aparece nos relatórios do Azure multi-factor Authentication e poderá ser apresentado nas mensagens de autenticação SMS ou da aplicação móvel.
7. Verifique Olá **correspondência de utilizador exigir autenticação multi-factor do Azure** caixa se todos os utilizadores tiverem sido ou importados para Olá servidor e a verificação de passo tootwo do requerente. Se um número significativo de utilizadores ainda não foram importado para Olá servidor e/ou excluídos da verificação de dois passos, deixe Olá caixa desmarcada. Consulte o ficheiro de ajuda do servidor MFA Olá para obter informações adicionais sobre esta funcionalidade.

Repita estes passos tooadd adicionais LDAP os clientes.

### <a name="configure-hello-ldap-directory-connection"></a>Configurar a ligação ao diretório LDAP Olá

Quando Olá Azure multi-factor Authentication está configurado tooreceive autenticações de LDAP, necessário utilizar o proxy nesses diretório LDAP toohello autenticações. Por conseguinte, o separador de destino Olá apresenta apenas um único, a cinzento opção toouse um destino LDAP.

1. Olá tooconfigure ligação do diretório LDAP, clique em Olá **integração de diretórios** ícone.
2. No separador de definições de Olá, selecione Olá **utilize a configuração de LDAP específica** botão de opção.
3. Selecione **Editar...**
4. Na caixa de diálogo Editar configuração de LDAP de Olá, preencha os campos de Olá com o diretório LDAP Olá informações necessárias tooconnect toohello. As descrições dos campos de Olá estão incluídas no ficheiro de ajuda do servidor do Azure multi-factor Authentication Olá.

    ![Integração de Diretórios](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Testar a ligação de LDAP Olá clicando Olá **teste** botão.
6. Se o teste de ligação LDAP Olá foi concluída com êxito, clique em Olá **OK** botão.
7. Clique em Olá **filtros** Olá do separador servidor está pré-configurada tooload contentores, grupos de segurança e utilizadores do Active Directory. Se vincular tooa outro diretório LDAP, provavelmente terá de filtros de Olá tooedit apresentados. Clique em Olá **ajudar** ligação para obter mais informações sobre filtros.
8. Clique em Olá **atributos** Olá do separador servidor está pré-configurada toomap atributos do Active Directory.
9. Se estiver a vincular tooa outros diretório ou toochange Olá previamente configurada mapeamentos de atributos LDAP, clique em **editar...**
10. Na caixa de diálogo Editar atributos de Olá, modifique os mapeamentos de atributos LDAP Olá para o seu diretório. Os nomes de atributos podem ser escritos no ou selecionados clicando Olá **...** campo tooeach seguinte do botão. Clique em Olá **ajudar** ligação para obter mais informações sobre os atributos.
11. Clique em Olá **OK** botão.
12. Clique em Olá **definições da empresa** ícone e selecione Olá **resolução de nome de utilizador** separador.
13. Se está a ligar tooActive diretório a partir de um servidor associado a um domínio, deixe Olá **utilizar segurança identificadores (SIDs) do Windows correspondentes** botão de opção seleccionado. Caso contrário, selecione Olá **o atributo de identificador exclusivo de LDAP de utilização para correspondentes** botão de opção. 

Quando Olá **o atributo de identificador exclusivo de LDAP de utilização para correspondentes** botão de opção está selecionado, hello do servidor multi-factor Authentication Azure tenta tooresolve tooa cada nome de utilizador, o identificador exclusivo no diretório LDAP Olá. É efetuada uma pesquisa LDAP no Olá Username atributos definidos no Olá integração de diretórios -> separador atributos. Quando um utilizador efetua a autenticação, o nome de utilizador Olá é toohello resolver o identificador exclusivo no diretório LDAP Olá. Identificador exclusivo Olá é utilizado para o utilizador Olá correspondente no ficheiro de dados do Azure multi-factor Authentication Olá. Isto permite efetuar comparações sensível e formatos de nome de utilizador extenso e abreviado.

Depois de concluir estes passos, Olá MFA Server escuta a portas Olá configurada para pedidos de acesso LDAP dos Olá configurada clientes e atos como um proxy para os pedidos toohello o diretório LDAP para autenticação.

## <a name="configure-ldap-client"></a>Configurar o cliente LDAP
Olá tooconfigure cliente LDAP, utilize as diretrizes de Olá:

* Configure a sua aplicação tooauthenticate através de LDAP toohello do servidor multi-factor Authentication Azure, aplicação ou servidor como se fosse o seu diretório LDAP. Utilize Olá mesmo definições que normalmente utilizaria tooconnect diretamente tooyour diretório LDAP, exceto o nome do servidor Olá ou endereço IP, que será que hello do servidor do Azure multi-factor Authentication.
* Configurar Olá LDAP tempo limite too30-60 em segundos, de modo que não haja credenciais do utilizador de tempo, toovalidate Olá com o diretório LDAP Olá, efetuar verificação de segundo passo Olá, receber a respetiva resposta e pedido de acesso LDAP toohello de responder.
* Se utilizar o LDAPS, hello aplicação ou o servidor efetuar consultas LDAP de Olá deve confiar Olá certificado SSL instalado no hello do servidor do Azure multi-factor Authentication.

