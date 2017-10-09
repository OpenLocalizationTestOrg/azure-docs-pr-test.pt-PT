---
title: "faturação de Olá aaaChange para o Azure RemoteApp | Microsoft Docs"
description: Saiba como toostop a ser cobrados para o Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Migrar a partir do Azure RemoteApp tooMyCloudIT 

**Atualmente utilizar Microsoft Azure RemoteApp?** : MyCloudIT incorporada toomigrate uma ferramenta automatizada sua plataforma de gestão do Azure RemoteApp (ARA) collection(s) toohello MyCloudIT ao continuar toorun no Microsoft Azure.

**Tirar partido do portal do Azure Resource Manager de Olá**: permite a migração foi concluída na plataforma de MyCloudIT Olá novo portal de Azure Resource Manager do acesso instantâneas tooAzure. Este portal contém todas as novas capacidades de Olá e inovações oferecidas pelo Microsoft Azure, incluindo acesso tooVirtual máquina tamanhos tooensure a implementação é criada necessidades de Olá toosupport da sua empresa.

**Testar a solução certa de Olá tooensure paralelas para as suas necessidades**: é criada a ferramenta de migração de MyCloudIT Olá processo de migração de Olá tooinitiate e teste no tempo paralelo os seus utilizadores ARA atuais continuar toouse ARA.  Os seus utilizadores irão permanecer no ARA até a migração e testes são concluídos.  ferramenta de migração de Olá é criada a coleção de ARA típica do toohandle Olá.  Se sentir que tem um cenário exclusivo e não padrão, contacte-nos [ sales@conexlink.com ](mailto:sales@conexlink.com) para podermos fornecer um plano personalizáveis tooassist com a sua migração.

**Capacidades de ambiente de trabalho-como-um-serviço**: tenha em atenção que MyCloudIT não só proporciona capacidades de RemoteApp Olá está habituado a, mas que também oferecemos completo ambiente de trabalho-como-um-serviço capacidades para Olá mesmo custo por mês, sem qualquer utilizador mínima requisitos.

## <a name="what-we-will-do-for-you"></a>O que será efetuado por si

MyCloudIT automatiza a migração de Olá do seu modelo do Azure RemoteApp no portal clássico do Azure de Olá do seu toohello de subscrição do Azure Resource Manager Portal da sua subscrição com o nosso ferramenta de migração automatizada.  

> [!NOTE]
> Olá, Olá Azure RemoteApp modelo têm de permanecer na mesma região do Azure, como a implementação do Azure RemoteApp original.  Se precisar de toochange Azure regiões ou subscrições do Azure durante a migração de Olá, contacte-nos para orientações adicionais em [ sales@conexlink.com ](mailto:sales@conexlink.com).

Leitura abaixo para informações detalhadas sobre Olá automatizar o processo de migração com a ferramenta de migração de MyCloudIT Olá:

1. ferramenta de migração de Olá analisa as subscrições atuais para todas as implementações de ARA existentes.  
2. Selecione um ARA coleção toomigrate cada vez.  Se tiver várias coleções, execute a nossa ferramenta várias vezes.
3. Ter Olá opção toocopy Olá discos de perfil de utilizador (UDP) tooyour nova implementação, de modo a pode obter dados legados, ou manualmente mapear alojam UPDs toohello nova implementação. Se optar por toocopy sua alojam UPDs, iremos guardar alojam UPDs de Olá e incluir um ficheiro de texto que mapeia o nome de Olá UPD nome tooeach dos utilizadores.  Olá alojam UPDs será copiado tooa partilha no servidor RDSMGMT Olá `F:\Shares\LegacyUPD` e irá ser exposta através de partilha de Olá `\\RDSmgmt\LegacyUPD`. 
4. A migração irá exigir sem períodos de indisponibilidade para a sua implementação ARA atual.  No entanto, se as alterações serem efetuadas toohello alojam UPDs (a partir de ARA) após a cópia de Olá, estas alterações não serão refletidas na alojam UPDs Olá armazenados no portal do Azure Resource Manager de Olá. 
5. Se tiver VMs adicionais, como controladores de domínio e servidores de ficheiros na sua rede Virtual do Azure clássico irão estabelecer VNet peering entre existente clássico Virtual Network do Azure e hello nova rede Virtual criar para si, no Olá novo recurso do Azure Portal de gestor.
6. A nossa solução automatizada só irá estabelecer VNet peering entre existente clássico Virtual Network do Azure e Olá nova rede Virtual, se a implementação de ARA existente é uma implementação híbrida; ou seja, está a autenticar com um controlador de domínio de diretório Active Directory do Windows Server no Olá existentes de rede Virtual clássica. Se não podemos estabelecer VNet peering para a coleção, mas precisa de VNet peering, contacte-nos como [ sales@conexlink.com ](mailto:sales@conexlink.com) e vai ser satisfeito tooconfigure VNet peering sem custos adicionais.
7. A nossa solução automatizada irá garantir a configuração de DNS do Azure é atualizada com Olá novo tooensure de definições de rede Virtual, a nova implementação pode ligar tooyour existentes controlador de domínio no Olá VNet clássica.
8. A nossa solução automatizada será Certifique-se de que existem não existem conflitos de endereços IP como estamos a criar esta nova rede Virtual e estabelecer Olá VNet peering para implementações que tenham um Windows Server Active Directory do servidor existente.
9. Se estiver a utilizar apenas do Azure AD para autenticação, MyCloudIT irá criar um novo Windows do domínio do Active Directory e utilizar o Azure AD Connect toosynchronize utilizadores entre instância do Olá existente do Azure AD e Olá criado de novo Windows do domínio do Active Directory por MyCloudIT.
10. Se estiver a utilizar um utilizadores do Windows Server Active Directory Domain tooauthenticate ARA, nossa solução automatizada irá ligar a sua nova tooyour de implementação de MyCloudIT existentes do controlador de domínio do Active Directory do Windows Server através de VNet peering.
11. Se estiver a utilizar o Azure Active Directory Domain Services para a autenticação, iremos pode migrar a, mas contacte-nos para que possa criar um plano de migração personalizado para si.  Envie um e-mail demasiado[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Depois de Olá coleção toobe migrado é confirmado, manter-se novamente e reduzir enquanto a nossa solução automatizada migra a coleção de ARA e os discos do perfil de utilizador (opcional) toohello nova aplicações remotas MyCloudIT orientadas por solução.
13. Após a conclusão da implementação de Olá, vamos voltar publicar Olá mesmas aplicações que foram publicadas no ARA e após a implementação será capaz de toopublish outras aplicações.

## <a name="post-migration-benefits"></a>Publique as vantagens de migração

1. Podemos fornecer a consola de gestão de Olá que permite-lhe toomanage Olá ciclo de vida completo da sua implementação de aplicações remotas.
2. Será capaz de toomanage máquinas a virtuais a partir do nosso portal.  Iniciar / parar e redimensionar VMs individuais, se necessário.
3. consola de gestão de Olá fornece Olá toocreate de capacidade e a gerir utilizadores / grupos a partir do nosso portal de gestão.
4. consola de gestão de Olá disponibiliza Olá capacidade toosynchronize aos utilizadores do Office 365 toocreate uma experiência de início de sessão na mesma.
5. Olá consola de gestão fornece Olá capacidade toocreate adicionais Remote App e coleções de ambiente de trabalho sem custos de utilizador duplicado ou requisitos de utilizador mínima. 
6. consola de gestão de Olá fornece a capacidade de Olá toopublish novas aplicações de aplicações remotas.
7. consola de gestão de Olá fornece o arranque do Olá capacidade tooschedule Olá e encerramento da sua implementação de aplicações remotas se só precisa da solução durante horas específicas.
8. consola de gestão de Olá fornece a capacidade de Olá tooautomate instalação de Olá e a configuração do agente de cópia de segurança do Azure Olá que fornece um histórico de retenção do documento para os seus dados de cliente.
9. consola de gestão de Olá fornece acesso tooperformance métricas da sua implementação.  Este oferece Olá capacidade tooidentify quaisquer potenciais congestionamentos de desempenho sem instalar ferramentas de gestão de desempenho adicionais.
10. Se tiver vários anfitriões de sessão, será automaticamente tooenable capaz de dimensionamento da sessão de Olá, por isso, apenas anfitriões que tenham toobe em execução estão em execução.
11. MyCloudIT fornece o servidor de gateway do acesso toohello RDWeb através de um nome de domínio MyCloudIT.  Fornecemos também Olá capacidade toore mapa Olá URL tooa URL personalizado para o utilizador final, imagem corporativa.

## <a name="prerequisites-for-migration"></a>Pré-requisitos para migração

1. Tem de ter acesso toohello subscrição do Azure que aloja a atual solução de Azure RemoteApp.
2. Tem de conceder permissões nosso portais dentro da sua subscrição toomigrate seu modelo e toocreate / modificar a sua nova implementação de MyCloudIT.
3. Tenha em atenção que devido a limitação de tooa no Azure Remote App, cada coleção só pode ser migrada três vezes.  Se precisar de uma coleção de toomigrate mais do que três vezes, pode emitir um tooincrease de tooAzure permissão a contagem de exportação, ou contacte-nos e iremos irá ajudar a contagem de exportação de Olá pedido tooincrease Olá ARA.

## <a name="mycloudit-billing"></a>MyCloudIT faturação

Consulte [MyCloudIT preços do RemoteApp soluções](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) para obter informações sobre como toopredict e gerir os custos gerais do Azure.

Se ainda tiver questões, contacte-nos [ sales@conexlink.com ](mailto:sales@conexlink.com) ou veja o vídeo de demonstração completo de Olá [ferramenta de migração do Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

