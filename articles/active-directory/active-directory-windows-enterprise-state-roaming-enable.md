---
title: aaaEnable Roaming de estado empresarial no Azure Active Directory | Microsoft Docs
description: "Perguntas mais frequentes sobre as definições de Roaming de estado empresarial em dispositivos Windows. Roaming de estado empresarial fornece aos utilizadores uma experiência unificada entre os respetivos dispositivos Windows e reduz o tempo de Olá necessário para configurar um novo dispositivo."
services: active-directory
keywords: roaming, nuvem do windows, como de estado empresarial roaming de estado do tooenable empresarial
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Ativar o Roaming de Estado Empresarial no Azure Active Directory
Roaming de estado empresarial é tooany disponíveis organização com uma subscrição Premium do Azure Active Directory (Azure AD). Para obter mais detalhes sobre como tooget uma subscrição do Azure AD, consulte Olá [página de produto do Azure AD](https://azure.microsoft.com/services/active-directory).

Quando ativar Roaming de estado empresarial, a organização será automaticamente concedida licenças para uma subscrição gratuita de utilização limitada de tooAzure Rights Management. Esta subscrição gratuita é limitado tooencrypting e desencriptação de definições da empresa e dados da aplicação sincronizados por Olá Roaming de estado empresarial serviço; tem de ter uma subscrição paga toouse Olá funcionalidades completas do Azure Rights Management.

Depois de obter uma subscrição Premium do Azure AD, siga estas tooenable passos Roaming de estado empresarial:

1. Início de sessão toohello portal clássico do Azure.
2. Olá esquerda, selecione **do Active Directory**e, em seguida, selecione o diretório de Olá para o qual pretende tooenable Roaming de estado empresarial.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Aceda toohello **configurar** separador no topo de Olá.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Desloque para baixo a página Olá e selecione **os utilizadores poderão SINCRONIZAR as definições e dados da aplicação empresarial**e, em seguida, clique em **guardar**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Para definições de tooroam de dispositivos Windows 10 com Olá serviço Roaming de estado empresarial, Olá tem de ser autenticado através de uma identidade do Azure AD. Para dispositivos que estão associados a um tooAzure AD, o início de sessão primário do utilizador Olá é identidade Olá do Azure AD, pelo que é necessária nenhuma configuração adicional. Para dispositivos que utilizam um tradicional no Active Directory local, Olá administrador de TI tem [ligar Olá dispositivos associados a domínios tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Armazenamento de dados de sincronização
Roaming de estado empresarial dados estão alojados numa ou várias [regiões do Azure](https://azure.microsoft.com/regions/) que melhor está alinhada com o valor de país/região de Olá definido na instância do Azure Active Directory de Olá. Dados de Roaming de estado empresarial estão particionados com base nas três regiões geográficas principais: América do Norte, EMEA e APAC. Dados de Roaming de estado empresarial para o inquilino Olá encontra localmente com a região geográfica Olá e não são replicados em regiões.  Por exemplo, os clientes que têm as respetivas tooone de conjunto de valor de país/região de países EMEA como "França" ou "Zambia" terá os seus dados de uma ou alojados de Olá regiões do Azure na Europa.  Os clientes que definir o respetivo valor de país/região no Azure AD tooone da América do Norte países como "Dos Estados Unidos" ou "Canadá" terá os seus dados alojada num ou mais das Olá Olá E.U.A. regiões do Azure.  Os clientes que definir o respetivo valor de país/região no Azure AD tooone de países APAC como "Austrália" ou "Nova Zelândia" terá os seus dados alojada num ou mais das Olá regiões do Azure na Ásia.  -Sul American países e os dados de Antarctica serão alojados num ou mais regiões do Azure dentro Olá E.U.A..  valor de país/região Olá está definido como parte do processo de criação do diretório do Azure AD de Olá e não pode ser modificada posteriormente. 

Se precisar de mais detalhes sobre localização de armazenamento de dados,. um ticket [suporte do Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Gerir o Roaming de estado empresarial
Administradores globais do Azure AD podem ativar e desativar o Roaming de estado empresarial no Olá portal clássico do Azure.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Os administradores globais podem limitar a sincronização de definições toospecific grupos de segurança.

Administradores globais também podem ver um relatório de estado de sincronização de dispositivos por utilizador, selecionando um utilizador específico na instância do Active Directory de Olá **utilizadores** lista e clicando na **dispositivos** separador e selecionar vista **Dispositivos a sincronizar as definições e dados da aplicação empresarial**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Retenção de dados
Os dados sincronizados tooAzure através de Roaming de estado empresarial será mantida indefinidamente, a menos que é executada uma operação de eliminação manual ou dados Olá em questão são determinado toobe obsoletos. 

**Eliminação explícita:** dados Olá são eliminados quando um administrador do Azure elimina um utilizador ou um diretório ou um administrador explicitamente pedidos que os dados são toobe eliminado.

* **A eliminação do utilizador**: quando um utilizador for eliminado no Azure AD, a conta de utilizador de Olá roaming de dados será marcada para eliminação e será eliminada entre 90 dias too180. 
* **Eliminação de diretório**: eliminar um diretório todo no Azure AD é uma operação de imediato. Todos os dados de definições de Olá associados com que o diretório será marcado para eliminação e será eliminado entre 90 dias too180. 
* **Na eliminação do pedido**: se Olá do Azure AD admin pretende toomanually eliminar dados ou dados de definições de um utilizador específico, Olá, admin pode um ticket [suporte do Azure](https://azure.microsoft.com/support/). 

**Eliminação de dados de obsoleta**: dados que não tiverem sido acedidos de um ano ("período de retenção Olá") será tratado como obsoleto e podem ser eliminado do Azure. período de retenção de Olá é toochange do requerente, mas não poderá ser inferior a 90 dias. dados obsoletos Olá podem ser um conjunto específico de definições de aplicação do Windows ou todas as definições para um utilizador. Por exemplo:

* Se não há dispositivos que aceder a uma coleção de definições (por exemplo, uma aplicação é removida do dispositivo hello, ou um grupo de definições, tais como "Tema" está desativado para todos os dispositivos de um utilizador), essa coleção será ficou obsoleta após o período de retenção de Olá e pode ser eliminar. 
* Se um utilizador tiver desativado a sincronização de definições em todos os dispositivos sua, em seguida, nenhum dos dados de definições de Olá serão acedidas as aplicações e todos os dados de definições de Olá desse utilizador serão ficou obsoletos e podem ser eliminados após o período de retenção de Olá. 
* Se Olá, admin do Azure AD directory desligar Roaming de estado empresarial para o diretório de todo Olá, em seguida, todos os utilizadores desse diretório irá parar a sincronização de definições e todos os dados de definições para todos os utilizadores serão ficou obsoletos e podem ser eliminados após o período de retenção de Olá. 

**Eliminar a recuperação de dados**: política de retenção de dados de Olá não é configurável. Depois dos dados de Olá foi eliminados permanentemente, não serão recuperável. No entanto, é importante toonote Olá dados das definições só será eliminado a partir do Azure, não o dispositivo de utilizador final Olá. Se qualquer dispositivo mais tarde volta toohello Roaming de estado empresarial serviço, definições de Olá novamente serão sincronizadas com êxito e armazenadas no Azure.

## <a name="related-topics"></a>Tópicos relacionados
* [Descrição geral do Roaming de estado empresarial](active-directory-windows-enterprise-state-roaming-overview.md)
* [As definições e roaming FAQ de dados](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Definições de política e o MDM para sincronização de definições de grupo](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Referência de definições de roaming Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Resolução de problemas](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
