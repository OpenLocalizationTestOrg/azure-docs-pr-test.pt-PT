---
title: "aaaHow toouse Olá do Azure Active Directory Power BI pacote de conteúdos | Microsoft Docs"
description: "Saiba como toouse hello do Azure Active Directory Power BI pacote de conteúdos"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>Como toouse hello do Azure Active Directory Power BI pacote de conteúdos

Para os administradores de TI, é fundamental compreender como é que os utilizadores adotam e utilizam as funcionalidades do Azure Active Directory. Permite-lhe tooplan a utilização de tooincrease de infraestrutura e de comunicação de IT e tooget hello mais fora de funcionalidades do AAD. Pacote de conteúdo do Power BI para o Azure Active Directory oferece Olá capacidade toofurther analisar o toounderstand de dados como pode utilizar este dados toogather mais rico aprofundadas que se passa no seu Azure Active Directory para Olá diversas capacidades de está bastante dependem.  Com a integração de Olá das APIs do Azure Active Directory para o Power BI, pode facilmente transferir pacotes de conteúdos pré-criadas Olá e obter informações acerca da atividades de Olá tooall dentro do seu Azure Active Directory utilizando a experiência de visualização avançado que oferece do Power BI. Pode criar o seu próprio dashboard e partilhá-lo facilmente com qualquer pessoa da sua organização. 

Este tópico fornece-lhe instruções passo a passo sobre como tooinstall e utilize Olá conteúdo do pacote no seu ambiente.

## <a name="installation"></a>Instalação  

**Olá tooinstall o pacote de conteúdos do Power BI:**

1. Inicie sessão no [Power BI](https://app.powerbi.com/groups/me/getdata/services) com a sua conta do Power BI (isto é Olá mesma conta que o Office 365 ou a conta do Azure AD).

2. Na Olá parte inferior do painel de navegação esquerdo Olá, selecione **obter dados**.

    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. No Olá **serviços** , clique em **obter**.
   
    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Procure **Azure Active Directory**.

    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  Quando lhe for pedido, escreva o seu ID de Inquilino do Azure AD e clique em **Seguinte**.

    > [!TIP] 
    > Olá de tooget uma forma rápida Id do inquilino para o seu inquilino do Office 365 / do Azure AD é toologin toohello Portal do Azure AD, desagregar toohello diretório e copie o ID de Olá da Olá seguinte URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension/diretório/<tenantid>/directoryQuickStart

    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Clique em **entrar**. 
 
    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Introduza o nome de utilizador e a palavra-passe e clique em **Iniciar sessão**.
 
    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  Caixa de diálogo de consentimento de aplicação Olá, clique em **aceitar**.
 
9.  Quando o seu dashboard de registos de Atividades do Azure Active Directory estiver criado, clique no mesmo.
 
    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>O que posso fazer com este pacote de conteúdos?

Antes de iremos avançar para o que pode fazer com este pacote de conteúdos, rápida pré-visualização Eis de Olá vários relatórios no conteúdo de Olá do pacote. Relatório de dados anterior entra toohello **últimos 30 dias**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Relatórios incluídos nesta versão do Pacote de Conteúdos de registos do Azure Active Directory

**Relatório de utilização da aplicação e tendência**: obter conhecimentos aprofundados em aplicações de Olá utilizados na sua organização e aqueles que estão a ser utilizados mais Olá e quando. Pode utilizar este relatório toogather aprofundadas como uma aplicação que recentemente implementado na sua organização está a ser utilizada ou saber que aplicações são populares. Ao fazê-lo, pode melhorar a utilização se vir que o se a aplicação Olá não está a ser utilizada.

**Inícios de sessão por localização e os utilizadores**: obter conhecimentos aprofundados em todos os Olá inícios de sessão efetuados utilizando a identidade do Azure e fornecem informações sobre a identidade de Olá de utilizadores de Olá. Com estas informações, pode analisar mais aprofundadamente inícios de sessão individuais e responder a perguntas como:

- De onde é que este utilizador iniciou sessão?
- O utilizador tem Olá maioria dos inícios de sessão e onde estes início de sessão do? 
- Foi Olá início de sessão com êxito?  
 
Pode clicar numa data ou localização específica para ver informações mais detalhadas.

**Utilizadores exclusivos por aplicação**: veja todos os utilizadores exclusivos que estão a utilizar uma determinada aplicação. Inclui apenas os utilizadores que iniciaram sessão “*com êxito*” numa aplicação.

**Inícios de sessão de dispositivo**: obter uma vista do tipo de Olá do SO e os browsers que estão a ser utilizados por utilizadores na sua organização com informações detalhadas sobre os utilizadores Olá, incluindo:

- Nome de Utilizador
- Endereço IP
- Localização 
- Estado de início de sessão 

Com este relatório, pode perceber Olá vários perfis de dispositivo utilizadas dentro da sua organização e determinam as políticas de dispositivos com base no que é utilizado

**Funil de SSPR**: saiba como é que as reposições de palavras-passe são feitas na sua organização. Obter um peek na palavra-passe quantos reposições foram tentadas através da ferramenta SSPR Olá e quantos deles teve êxito. Aprofundar falhas de reposições de palavra-passe de Olá utilizando funil SSPR Olá e compreender por que motivo determinadas falhas ocorreram. Este relatório fornece uma compreensão mais aprofundada de como ferramenta SSPR Olá é utilizada na sua organização para que possa tomar decisões corretas Olá.

## <a name="customizing-azure-ad-activity-content-pack"></a>Personalizar o Pacote de Conteúdos de Atividades do Azure AD

**Alterar a visualização**: pode alterar uma visualização de relatório clicando **Editar relatório** e selecione a visualização de Olá pretende.
 
![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Incluir campos adicionais**: pode adicionar um relatório de toohello de campo ou removê-lo ao selecionar toowhich visual Olá pretende que o campo de Olá tooadd/remover. Exemplo de Olá abaixo, posso estou a adicionar "início de sessão no estado" campo toohello vista em tabela. 
 
![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Dashboard do PIN visualizações tooyour**: personalizar o dashboard e incluir os seus próprios relatórios de toohello visualizações e afixá-lo toohello dashboard. Exemplo de Olá abaixo, posso adicionado um novo filtro chamado "início de sessão no estado" em incluídos-Olá relatório. Posso também mudou visualização Olá de gráfico de linhas do gráfico de barras tooa e pode afixar este dashboard visual toohello novo.

![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**O dashboard de partilha**: assim que tiver criado o conteúdo de Olá quiser, pode partilhar o dashboard de Olá com utilizadores Olá na sua organização. Não se esqueça de que depois de partilhar o relatório de Olá, podem ver os campos de Olá que selecionou no relatório de Olá.
 
![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Agendar uma atualização diária do seu relatório do Power BI

tooschedule uma atualização diária do seu relatório do Power BI, aceda demasiado**conjuntos de dados > Definições > Agendar Atualização** e defina-o conforme mostrado abaixo.
 
![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>Atualizar a versão de toonewer do pacote de conteúdos

Se quiser tooupdate o conteúdo do pacote de tooget uma versão mais recente:

- Transfira o pacote de conteúdos novos Olá e configurá-lo de acordo com as instruções apresentadas neste artigo.

- Assim que tiver configurado-lo, aceda demasiado**origem de dados > Definições > credenciais da origem de dados** e volte a introduzir as suas credenciais, conforme mostrado abaixo

    ![Pacote de Conteúdos do Power BI para o Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Assim que a versão nova do Olá do pacote de conteúdos Olá está a funcionar, pode remover a versão antiga do Olá se for necessário, eliminando relatórios subjacente Olá e conjuntos de dados associados a esse pacote de conteúdos.

## <a name="still-having-issues"></a>Ainda está com problemas? 

Veja o nosso [guia de resolução de problemas](active-directory-reporting-troubleshoot-content-pack.md). Para obter ajuda geral com o Power BI, veja estes [artigos de ajuda](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Passos seguintes

Para obter uma descrição geral de criação de relatórios, consulte Olá [relatórios do Azure Active Directory](active-directory-reporting-azure-portal.md).
