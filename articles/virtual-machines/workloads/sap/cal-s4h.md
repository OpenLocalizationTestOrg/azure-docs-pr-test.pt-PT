---
title: aaaDeploy SAP S/4HANA ou BW/4HANA numa VM do Azure | Microsoft Docs
description: Implementar SAP S/4HANA ou BW/4HANA numa VM do Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Implementar SAP S/4HANA ou BW/4HANA no Azure
Este artigo descreve como toodeploy S/4HANA no Azure utilizando Olá biblioteca de aplicação de nuvem do SAP (SAP CAL) 3.0. toodeploy outras soluções baseadas em SAP HANA, tais como BW/4HANA, siga Olá mesmos passos.

> [!NOTE]
Para mais informações sobre Olá SAP CAL, visite toohello [biblioteca de aplicação de nuvem do SAP](https://cal.sap.com/) Web site. SAP também tem um blogue sobre Olá [SAP nuvem aplicação biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Além disso como de 29 de Maio de 2017, pode utilizar o modelo de implementação Azure Resource Manager Olá toohello preferencial menos implementação clássica modelo toodeploy Olá SAP CAL. Recomendamos que utilize o modelo de implementação Resource Manager novo Olá e ignorar o modelo de implementação clássica Olá.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Solução do passo a passo do processo toodeploy Olá

Olá sequência das capturas de ecrã a seguir mostra como toodeploy S/4HANA no Azure utilizando Olá SAP CAL. processo de Olá funciona Olá mesma forma para outras soluções, tais como BW/4HANA.

Olá **soluções** página mostra algumas das Olá soluções baseadas em CAL de SAP HANA disponíveis no Azure. **SAP S/4HANA 1610 FPS01, Fully-Activated aplicação** na linha de média de Olá:

![Soluções de CAL SAP](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Criar uma conta no Olá SAP CAL
1. toosign no toohello SAP CAL para Olá pela primeira vez, utilize o SAP-utilizador ou outro utilizador registado com o SAP. Em seguida, defina uma conta do SAP CAL que é utilizada por aplicações de toodeploy SAP CAL Olá no Azure. Na definição da conta de Olá, tem de:

    a. Selecione o modelo de implementação de Olá no Azure (Gestor de recursos ou clássico).

    b. Introduza a sua subscrição do Azure. Uma conta do SAP CAL pode ser atribuída a subscrição de tooone apenas. Se precisar de mais do que uma subscrição, terá de toocreate outra conta do SAP CAL.

    c. Dê Olá SAP CAL permissão toodeploy na sua subscrição do Azure.

    > [!NOTE]
    Olá passos seguintes mostram como uma conta de toocreate uma CAL SAP para implementações do Resource Manager. Se já tiver uma conta do SAP CAL que é o modelo de implementação clássica toohello ligado, *necessário* toofollow toocreate estes passos uma nova conta do SAP CAL. nova conta do SAP CAL Olá tem toodeploy no modelo do Resource Manager Olá.

2. Crie uma nova conta do SAP CAL. Olá **contas** página mostra três opções para o Azure: 

    a. **Microsoft Azure (clássica)** é o modelo de implementação clássica Olá e já não é preferencial.

    b. **Microsoft Azure** é Olá novo modelo de implementação de Gestor de recursos.

    c. **O Microsoft Azure operado pela 21Vianet** é uma opção na China que utiliza o modelo de implementação clássica Olá.

    Selecione toodeploy no modelo do Resource Manager Olá, **Microsoft Azure**.

    ![Detalhes de conta do CAL SAP](./media/cal-s4h/s4h-pic-2a.png)

3. Introduza Olá Azure **ID de subscrição** que pode ser encontrado no Olá portal do Azure.

   ![Contas de CAL SAP](./media/cal-s4h/s4h-pic3c.png)

4. tooauthorize Olá SAP CAL toodeploy para Olá subscrição do Azure definidos, clique em **autorizar**. Olá seguir página é apresentada no separador do browser Olá:

   ![Início de sessão dos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. Se mais do que um utilizador estiver listado, escolha Olá conta Microsoft à qual está ligado toobe Olá coadministrador do Olá subscrição do Azure que selecionou. Olá seguir página é apresentada no separador do browser Olá:

   ![Confirmação de serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. Clique em **aceitar**. Se a autorização de Olá for bem-sucedida, Olá definição de conta do SAP CAL apresenta novamente. Após um curto período de tempo, uma mensagem confirma que o processo de autorização de Olá foi concluída com êxito.

7. Olá tooassign recém-criado SAP CAL conta de utilizador do tooyour, introduza o **ID de utilizador** no Olá caixa de texto Olá direito e clique em **adicionar**.

   ![Associação de conta toouser](./media/cal-s4h/s4h-pic8a.png)

8. Clique em sua conta com o utilizador Olá que utilize toosign toohello SAP CAL, de tooassociate **revisão**. 
 
9. associação de Olá toocreate entre o utilizador e a conta do SAP CAL Olá recentemente criado, clique em **criar**.

   ![Associação de conta do utilizador tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

Criou com êxito uma conta do SAP CAL que é capaz de:

- Utilize o modelo de implementação do Resource Manager Olá.
- Implemente sistemas SAP na sua subscrição do Azure.

Agora pode começar a toodeploy S/4HANA na sua subscrição de utilizador no Azure.

> [!NOTE]
Antes de continuar, determine se tem de quotas de núcleo do Azure para as VMs do Azure série H. Momento Olá, Olá SAP CAL utiliza H série VMs do Azure toodeploy algumas das soluções de SAP HANA baseado Olá. A subscrição do Azure poderá não ter quaisquer quotas de núcleos de série de H para série H. Se assim for, poderá ser necessário toocontact suporte do Azure tooget uma quota de núcleos de série de H, pelo menos, 16.

> [!NOTE]
Ao implementar uma solução no Azure em Olá SAP CAL, poderá achar que pode escolher apenas uma região do Azure. toodeploy em regiões do Azure que não sejam Olá um sugerida pelo Olá SAP CAL, precisa de toopurchase uma subscrição de CAL do SAP. Também poderá ter tooopen uma mensagem com o SAP toohave sua toodeliver de conta ativada de CAL para regiões do Azure que não sejam Olá aqueles inicialmente sugeridos.

### <a name="deploy-a-solution"></a>Implementar uma solução

Eis como implementar uma solução de Olá **soluções** página do Olá SAP CAL. Olá SAP CAL tem duas sequências toodeploy:

- Uma sequência básica que utiliza uma página toodefine Olá sistema toobe implementado
- Uma sequência avançada que dá-lhe algumas opções em tamanhos de VM 

Iremos demonstrar Olá toodeployment de caminho básico aqui.

1. No Olá **detalhes da conta** página, tem de:

    a. Selecione uma conta do SAP CAL. (Utilizar uma conta que seja toodeploy associado com o modelo de implementação do Resource Manager Olá.)

    b. Introduza uma instância **nome**.

    c. Selecione um Azure **região**. Olá SAP CAL sugere uma região. Se precisar de outra região do Azure e não tiver uma subscrição de SAP CAL, precisa de subscrição de tooorder um CAL com SAP.

    d. Introduza um mestre **palavra-passe** para a solução de Olá de nove ou oito carateres. palavra-passe de Olá é utilizada para os administradores de Olá dos componentes diferentes Olá.

   ![Modo de CAL Basic SAP: Criar uma instância](./media/cal-s4h/s4h-pic10a.png)

2. Clique em **criar**e na caixa de mensagem de Olá que aparece, clique em **OK**.

   ![CAL de SAP suportado tamanhos de VM](./media/cal-s4h/s4h-pic10b.png)

3. No Olá **chave privada** caixa de diálogo, clique em **arquivo** toostore chave privada de Olá no Olá SAP CAL. proteção de palavra-passe toouse para a chave privada de Olá, clique em **transferir**. 

   ![Chave privada de CAL SAP](./media/cal-s4h/s4h-pic10c.png)

4. Olá leitura SAP CAL **aviso** de mensagens e clique em **OK**.

   ![Aviso de CAL SAP](./media/cal-s4h/s4h-pic10d.png)

    Agora a implementação de Olá ocorre. Após algum tempo, dependendo da complexidade da solução de Olá (Olá SAP CAL fornece uma estimativa) e o tamanho Olá Olá estado é mostrado como Active Directory e pronto a utilizar.

5. as máquinas virtuais de Olá toofind recolhidas com Olá outros recursos associados num grupo de recursos, visite toohello portal do Azure: 

   ![Objetos de SAP CAL implementados no portal novo Olá](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. No portal de SAP CAL Olá, é apresentado o estado de Olá como **Active Directory**. tooconnect toohello solução, clique em **Connect**. Os diferentes componentes do diferentes opções tooconnect toohello são implementados dentro desta solução.

   ![Instâncias de CAL SAP](./media/cal-s4h/active_solution.png)

7. Antes de poder utilizar um dos Olá opções tooconnect toohello implementado sistemas, clique em **guia de introdução**. 

   ![Ligar toohello instância](./media/cal-s4h/connect_to_solution.png)

    os nomes de documentação Olá hello utilizadores para cada um dos métodos de conectividade Olá. Olá palavras-passe para esses utilizadores são definidas toohello mestre palavra-passe que definiu no início de Olá do processo de implementação de Olá. Na documentação de Olá, outros mais funcionais utilizadores são listados com as palavras-passe, que pode utilizar toosign no toohello implementado o sistema. 

    Por exemplo, se utilizar Olá SAP GUI que está pré-instalado na máquina de ambiente de trabalho remoto do Windows hello, Olá sistema S/4 poderá ter o seguinte aspeto:

   ![SM50 no Olá pré-instalado SAP GUI](./media/cal-s4h/gui_sm50.png)

    Ou, se utilizar Olá DBACockpit, instância de Olá poderá ter o seguinte aspeto:

   ![SM50 no Olá DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

Dentro de algumas horas, um dispositivo de SAP S/4 bom estado de funcionamento é implementado no Azure.

Se comprou a uma subscrição de SAP CAL, SAP suporta totalmente implementações através de Olá SAP CAL no Azure. fila de suporte de Olá é BC-VCM-CAL.







