---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do Azure AD | Microsoft Docs"
description: "Configurar o LDAP seguro (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurar segura LDAP (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD
Este artigo mostra como pode permitir proteger Lightweight Directory acesso protocolo (LDAPS) para o seu domínio gerido dos serviços de domínio do Azure AD. LDAP seguro também é conhecido como "acesso protocolo LDAP (Lightweight Directory) através de Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.

## <a name="before-you-begin"></a>Antes de começar
tarefas de Olá tooperform apresentadas neste artigo, tem de:

1. Um **subscrição do Azure**.
2. Um **diretório do Azure AD** -está sincronizada com um diretório no local ou um diretório apenas na nuvem.
3. **Serviços de domínio do Azure AD** tem de estar ativada para o diretório de Olá do Azure AD. Se ainda não o feito, siga todas as tarefas de Olá descritas em Olá [guia de introdução](active-directory-ds-getting-started.md).
4. A **certificado toobe utilizado tooenable LDAP seguro**.

   * **Recomendado** -obter um certificado de uma autoridade de certificação pública fidedigna. Esta opção de configuração é mais segura.
   * Em alternativa, pode também optar por demasiado[criar um certificado autoassinado](#task-1---obtain-a-certificate-for-secure-ldap) conforme mostrado posteriormente neste artigo.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Requisitos do certificado LDAP seguro Olá
Adquirir um certificado válido por Olá seguir diretrizes, antes de ativar LDAP seguro. Ocorrerem falhas, se tentar tooenable LDAP seguro para o seu domínio gerido com um certificado inválido incorreto.

1. **Emissor fidedigno** -Olá certificado tem de ser emitido por uma autoridade fidedigna pelos computadores que ligam toohello domínio gerido utilizando LDAP seguro. Esta autoridade pode ser uma autoridade de certificação pública fidedigna por estes computadores.
2. **Duração** -Olá certificado tem de ser válido para, pelo menos, Olá próximos 3 a 6 meses. LDAP acesso tooyour gerido domínio seguro é interrompido quando Olá certificado expirar.
3. **Nome do requerente** -nome de requerente Olá no certificado Olá tem de ser um caráter universal para o seu domínio gerido. Por exemplo, se o seu domínio com o nome 'contoso100.com', nome do requerente do certificado Olá tem de ser ' *. contoso100.com'. Definir Olá DNS (nome alternativo do requerente) toothis universal nome.
4. **Utilização da chave** - certificado Olá tem de ser configurado para Olá seguinte utiliza - as assinaturas Digital e cifragem de chaves.
5. **Objetivo do certificado** -Olá certificado tem de ser válido para autenticação de servidor SSL.

> [!NOTE]
> **Autoridades de certificação empresarial:** dos serviços de domínio do Azure AD não suporta a utilização segurados LDAP certificados emitidos pela autoridade de certificação empresarial da sua organização. Esta restrição é porque o serviço de Olá não fidedigna a AC como uma autoridade de certificação de raiz empresarial. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Tarefa 1 - obter um certificado para o LDAP seguro
tarefa primeiro Olá envolve a obtenção de um certificado utilizado para proteger LDAP acesso toohello domínio gerido. Tem duas opções:

* Obtenha um certificado de uma autoridade de certificação. autoridade de Olá pode ser uma autoridade de certificação pública.
* Crie um certificado autoassinado.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Opção (recomendado) - obter um certificado LDAP seguro de uma autoridade de certificação
Se a sua organização obtém os certificados de autoridades de certificação pública, terá de tooobtain Olá seguro LDAP certificado nessa autoridade de certificação pública.

Quando solicitar um certificado, certifique-se de que satisfaçam todos os requisitos de Olá descritos na [requisitos para o certificado LDAP seguro Olá](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Computadores cliente que necessitam de tooconnect toohello domínio gerido utilizando LDAP seguro têm de confiar emissor Olá do certificado LDAP seguro Olá.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Opção B - criar um certificado autoassinado para o LDAP seguro
Se não conta toouse um certificado de uma autoridade de certificação pública, pode escolher um certificado autoassinado para o LDAP seguro para toocreate.

**Criar um certificado autoassinado com o PowerShell**

No seu computador Windows, abra uma nova janela do PowerShell como **administrador** e Olá tipo os seguintes comandos, toocreate um novo certificado autoassinado.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

No Olá anterior exemplo, substitua '*. contoso100.com' com o nome de domínio DNS Olá do seu domínio gerido. Por exemplo, se tiver criado um domínio gerido chamado 'contoso100.onmicrosoft.com', substitua '*. contoso100.com' no Olá acima script com ' *. contoso100.onmicrosoft.com').

![Selecionar o Azure AD Directory](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

certificado autoassinado Olá recém-criado é colocado no arquivo de certificados de Olá local da máquina.


## <a name="next-step"></a>Passo seguinte
[Tarefa 2 - exportar Olá segura LDAP certificado tooa. Ficheiro PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
