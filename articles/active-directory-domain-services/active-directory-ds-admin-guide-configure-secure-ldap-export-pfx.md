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
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurar segura LDAP (LDAPS) para um domínio gerido dos serviços de domínio do Azure AD

## <a name="before-you-begin"></a>Antes de começar
Certifique-se de que concluiu [tarefa 1 - obter um certificado para o LDAP seguro](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Tarefa 2 - exportar Olá segura LDAP certificado tooa. Ficheiro PFX
Antes de começar esta tarefa, certifique-se de que adquiriu o certificado LDAP seguro Olá de uma autoridade de certificação pública ou tiver criado um certificado autoassinado.

Efetuar Olá os seguintes passos, tooexport Olá LDAPS tooa de certificado. Ficheiro PFX.

1. Olá prima **iniciar** botão e tipo **R**. No Olá **executar** caixa de diálogo, escreva **mmc** e clique em **OK**.

    ![Iniciar a consola do MMC Olá](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. No Olá **controlo de conta de utilizador** linha de comandos, clique em **Sim** toolaunch MMC (Consola de gestão da Microsoft) como administrador.
3. De Olá **ficheiro** menu, clique em **Adicionar/Remover Snap-in...** .

    ![Adicionar a consola do snap-in tooMMC](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. No Olá **adicionar ou Remover Snap-ins** caixa de diálogo, selecione de Olá **certificados** snap-in e clique em Olá **adicionar >** botão.

    ![Adicionar a consola do snap-in tooMMC de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. No Olá **snap-in de certificados** assistente, selecione **conta de computador** e clique em **seguinte**.

    ![Adicionar snap-in de certificados para conta de computador](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. No Olá **selecionar computador** página, selecione **computador Local: (Olá computador em que esta consola está a ser executada)** e clique em **concluir**.

    ![Adicionar snap-in Certificados - computador Selecione](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. No Olá **adicionar ou Remover Snap-ins** caixa de diálogo, clique em **OK** tooadd Olá certificados snap-in tooMMC.

    ![Adicione certificados snap-in tooMMC - concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. Na janela MMC Olá, clique em tooexpand **raiz da consola**. Deverá ver Olá snap-in de certificados carregados. Clique em **certificados (computador Local)** tooexpand. Clique em tooexpand Olá **pessoais** nó, seguido de Olá **certificados** nós.

    ![Arquivo de certificados pessoais aberta](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Deverá ver o certificado autoassinado Olá que foi criada. Pode examinar propriedades de Olá de Olá certificado tooensure Olá thumbprint correspondências que comunicaram no windows PowerShell de Olá quando criou o certificado de Olá.
10. Selecione Olá certificado autoassinado e **certo**. No menu de contexto de Olá, selecione **todas as tarefas** e selecione **exportar...** .

    ![Exportar certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. No Olá **Assistente para exportar certificados**, clique em **seguinte**.

    ![Assistente de exportação de certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. No Olá **exportar chave privada** página, selecione **Sim, exportar a chave privada Olá**e clique em **seguinte**.

    ![Exportar chave privada do certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > TEM de exportar chave privada do Olá, juntamente com o certificado de Olá. Se fornecer um PFX que contém Olá chave privada do certificado de Olá, ativar LDAP seguro para o seu domínio gerido irá falhar.
    >
    >
13. No Olá **exportar formato de ficheiro** página, selecione **Personal Information Exchange - PKCS #12 (. PFX)** como formato de ficheiro Olá para Olá o certificado exportado.

    ![Exportar formato de ficheiro de certificado](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Apenas Olá. Formato de ficheiro PFX é suportado. Não exporta Olá toohello de certificado. Formato de ficheiro CER.
    >
    >
14. No Olá **segurança** página, selecione de Olá **palavra-passe** opção e escreva um Olá tooprotect de palavra-passe. Ficheiro PFX. Uma vez que é necessária na próxima tarefa de Olá, lembre-se desta palavra-passe. Clique em **seguinte** tooproceed.

    ![Palavra-passe para exportar certificados ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Tome nota desta palavra-passe. Precisa ao ativar o LDAP seguro para este domínio gerido no [tarefa 3 - ativar LDAP seguro para domínio Olá de gerido](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. No Olá **ficheiro tooExport** página, especifique o nome de ficheiro Olá e a localização onde pretende que o certificado de Olá tooexport.

    ![Caminho para exportar certificados](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. Olá seguir página, clique em **concluir** ficheiro do tooexport Olá certificado tooa PFX. Deverá ver a caixa de diálogo de confirmação quando o certificado de Olá foi exportado.

    ![Exportar certificado concluído](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Passo seguinte
[Tarefa 3 - ativar LDAP seguro para domínio Olá de gerido](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
