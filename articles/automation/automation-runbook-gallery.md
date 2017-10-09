---
title: "galleries aaaRunbook e o módulo de automatização do Azure | Microsoft Docs"
description: "Os Runbooks e módulos da Comunidade da Microsoft e Olá estão disponíveis para tooinstall e utilizam no seu ambiente de automatização do Azure.  Este artigo descreve como pode aceder a estes recursos e toocontribute sua galeria de toohello runbooks."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d3fee7b4-630a-4c10-8425-9bf51d7c9e58
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 10b634460edf66dd7548017e3a2f7111b7125f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-and-module-galleries-for-azure-automation"></a>Galleries módulos e Runbooks de automatização do Azure
Em vez de criar os seus próprios runbooks e módulos na automatização do Azure, pode aceder a uma variedade de cenários que já foi criada pela Microsoft e Olá Comunidade.  Pode utilizar estes cenários sem modificações ou pode utilizá-los como um ponto de partida e editá-los para os seus requisitos específicos.

Pode obter runbooks a partir Olá [Galeria de Runbooks](#runbooks-in-runbook-gallery) e módulos de Olá [galeria do PowerShell](#modules-in-powerShell-gallery).  Também pode contribuir toohello Comunidade através da partilha de cenários que desenvolver.

## <a name="runbooks-in-runbook-gallery"></a>Runbooks na Galeria de Runbooks
Olá [Galeria de Runbooks](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=RootCategory&f\[0\].Value=WindowsAzure&f\[1\].Type=SubCategory&f\[1\].Value=WindowsAzure_automation&f\[1\].Text=Automation) proporciona uma variedade de runbooks da Microsoft e Olá Comunidade que pode importar para a automatização do Azure. Pode transferir ou um runbook da Galeria de Olá que está alojada no Olá [Centro de scripts do TechNet](https://gallery.technet.microsoft.com/scriptcenter/site/upload), ou pode importar runbooks diretamente na Galeria de Olá do Olá portal clássico do Azure ou do portal do Azure.

Só é possível importar diretamente a partir da Galeria de Runbooks Olá utilizando Olá portal clássico do Azure ou o portal do Azure. Não é possível executar esta função com o Windows PowerShell.

> [!NOTE]
> Deve validar conteúdo Olá de todos os runbooks que aproveitar Olá Galeria de Runbooks e tenha muito cuidado na instalação e executá-los num ambiente de produção. |
> 
> 

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-classic-portal"></a>tooimport um runbook a partir de Olá Galeria de Runbooks com Olá portal clássico do Azure
1. No Olá Portal do Azure, clique em, **novo**, **serviços aplicacionais**, **automatização**, **Runbook**, **da galeria**.
2. Selecione uma categoria tooview relacionadas com runbooks e selecione um runbook tooview os respetivos detalhes. Quando seleciona runbook Olá que pretende, clique no botão de seta para a direita Olá.
   
    ![Galeria de runbooks](media/automation-runbook-gallery/runbook-gallery.png)
3. Reveja o conteúdo de Olá do runbook Olá e tenha em atenção quaisquer requisitos na descrição Olá. Quando tiver terminado, clique no botão de seta para a direita Olá.
4. Introduza os detalhes do runbook Olá e, em seguida, clique no botão de marca de verificação Olá. nome do runbook Olá já irá ser preenchido.
5. o runbook de Olá aparecerá no Olá **Runbooks** separador para Olá conta de automatização.

### <a name="tooimport-a-runbook-from-hello-runbook-gallery-with-hello-azure-portal"></a>tooimport um runbook a partir de Olá Galeria de Runbooks com Olá portal do Azure
1. No Portal do Azure Olá, abra a sua conta de automatização.
2. Clique em Olá **Runbooks** mosaico tooopen Olá lista de runbooks.
3. Clique em **procurar galeria** botão.
   
    ![Galeria botão Procurar](media/automation-runbook-gallery/browse-gallery-button.png)
4. Localizar o item da Galeria de Olá que pretende e selecione-tooview os respetivos detalhes.
   
    ![Procurar da Galeria](media/automation-runbook-gallery/browse-gallery.png)
5. Clique em **projeto de fonte de vista** tooview item Olá Olá [Centro de scripts do TechNet](http://gallery.technet.microsoft.com/).
6. tooimport um item, clique na mesma tooview os respectivos detalhes e, em seguida, clique em Olá **importação** botão.
   
    ![Botão Importar](media/automation-runbook-gallery/gallery-item-detail.png)
7. Opcionalmente, altere o Olá de Olá runbook e, em seguida, clique em **OK** tooimport Olá runbook.
8. o runbook de Olá aparecerá no Olá **Runbooks** separador para Olá conta de automatização.

### <a name="adding-a-runbook-toohello-runbook-gallery"></a>A adição de uma galeria de runbook do runbook toohello
Microsoft encoraja tooadd runbooks toohello Galeria de Runbooks que pensa que seria útil tooother clientes.  Pode adicionar um runbook pelo [carregá-lo toohello Centro de scripts](http://gallery.technet.microsoft.com/site/upload) tendo em Olá conta os detalhes.

* Tem de especificar *do Windows Azure* para Olá **categoria** e *automatização* para Olá **subcategoria** para Olá runbook toobe apresentada no Assistente de Olá.  
* carregamento de Olá tem de ser um único ficheiro. ps1 ou. graphrunbook.  Se Olá runbook necessita de qualquer módulos, os runbooks subordinados ou ativos, em seguida, deve listar os na descrição Olá de submissão de Olá e na secção de comentários de Olá do runbook Olá.  Se tiver um cenário que necessitam de vários runbooks, em seguida, carregue cada separadamente e nomes de Olá de lista dos Olá relacionados com os runbooks em cada um das respetivas descrições. Certifique-se de que utiliza Olá mesmo etiquetas para que irá aparecer na Olá mesma categoria. Um utilizador terá tooread Olá descrição tooknow que outros runbooks são necessárias Olá cenário toowork.
* Adicione a etiqueta de Olá "GraphicalPS", se estiverem a publicar um **runbook gráfico** (não um fluxo de trabalho gráfico). 
* Inserir uma PowerShell ou o fluxo de trabalho do PowerShell fragmento de código na Olá descrição utilizando **inserir a secção de código** ícone.
* Olá resumo para carregamento Olá será apresentado no Olá que Galeria de Runbooks resulta pelo que deve fornecer informações detalhadas que o irão ajudar um utilizador identificar funcionalidade Olá de Olá runbook.
* Deve atribuir um toothree de Olá seguir o carregamento de toohello etiquetas.  Olá runbook será apresentado no Assistente de Olá em categorias de Olá que corresponde ao respetivas etiquetas.  As etiquetas não nesta lista serão ignoradas pelo Assistente de Olá. Se não especificar as etiquetas correspondentes, o runbook Olá serão listados na Olá outra categoria.
  
  * Cópia de segurança
  * Gestão de Capacidade
  * Controlo de alterações
  * Conformidade
  * Dev / teste ambientes
  * Recuperação Após Desastre
  * Monitorização
  * Aplicação de patches
  * Aprovisionamento
  * Remediação
  * Gestão de ciclo de vida VM
* Automatização de atualizações de galeria Olá uma vez uma hora, pelo que não verão as suas contribuições imediatamente.

## <a name="modules-in-powershell-gallery"></a>Módulos na galeria do PowerShell
Módulos do PowerShell contêm cmdlets que pode utilizar nos runbooks e módulos existentes que pode instalar na automatização do Azure estão disponíveis no Olá [galeria do PowerShell](http://www.powershellgallery.com).  Pode iniciar esta galeria a partir do portal do Azure de Olá e instalá-los diretamente na automatização do Azure ou pode transferi-las e instalá-los manualmente.  Não é possível instalar os módulos de Olá diretamente a partir de Olá portal clássico do Azure, mas pode transferi-los instalá-los tal como faria com qualquer outro módulo.

### <a name="tooimport-a-module-from-hello-automation-module-gallery-with-hello-azure-portal"></a>tooimport um módulo a partir da galeria do módulo de automatização de Olá com Olá portal do Azure
1. No Portal do Azure Olá, abra a sua conta de automatização.
2. Clique em Olá **ativos** mosaico tooopen Olá lista de recursos.
3. Clique em Olá **módulos** mosaico tooopen Olá lista de módulos.
4. Clique em Olá **procurar galeria** botão e Olá painel de navegação da galeria é iniciada.
   
    ![Galeria de módulo](media/automation-runbook-gallery/modules-blade.png) <br>
5. Depois de ter iniciado o painel de navegação da Galeria Olá, pode procurar por Olá seguintes campos:
   
   * Nome do módulo
   * Etiquetas
   * Autor
   * Nome do cmdlet/DSC de recursos
6. Localizar um módulo que está interessado em e selecione-tooview os respetivos detalhes.  
   Quando Pormenorize um módulo específico, pode ver mais informações sobre o módulo Olá, incluindo um toohello de back-ligação galeria do PowerShell, todas as dependências necessárias e todos os cmdlets de Olá e/ou recursos de DSC Olá módulo contém.
   
    ![Detalhes de módulos do PowerShell](media/automation-runbook-gallery/gallery-item-details-blade.png) <br>
7. módulo de Olá tooinstall diretamente na automatização do Azure, clique em Olá **importação** botão.
   
    ![Botão de módulo de importar](media/automation-runbook-gallery/module-import-button.png)
8. Ao clicar no botão de importação de Olá, verá o nome do módulo Olá que está prestes a tooimport. Se estiverem instaladas todas as dependências de Olá, Olá **OK** botão estará ativo. Se tiver dependências em falta, terá de tooimport os antes de importar este módulo.
9. Clique em **OK** tooimport Olá módulo e painel de módulo Olá serão iniciadas. Quando a automatização do Azure importa uma conta de tooyour do módulo, extrai metadados sobre o módulo Olá e Olá cmdlets.
   
    ![Painel do módulo de importação](media/automation-runbook-gallery/module-import-blade.png)
   
    Esta operação pode demorar alguns minutos, uma vez que cada atividade tem toobe extraído.
10. Receberá uma notificação esse módulo Olá está a ser implementado e uma notificação quando foi concluída.
11. Após a importação do módulo Olá, verá atividades disponíveis Olá e pode utilizar os respetivos recursos nos seus runbooks e a configuração de estado pretendido.

## <a name="requesting-a-runbook-or-module"></a>Pedir um runbook ou o módulo
Pode enviar pedidos demasiado[voz do utilizador](https://feedback.azure.com/forums/246290-azure-automation/).  Se precisar de ajudar a escrever um runbook ou tem alguma pergunta sobre o PowerShell, publique uma pergunta tooour [fórum](http://social.msdn.microsoft.com/Forums/windowsazure/en-US/home?forum=azureautomation&filter=alltypes&sort=lastpostdesc).

## <a name="next-steps"></a>Passos Seguintes
* tooget começar a utilizar runbooks, consulte [criar ou importar um runbook na automatização do Azure](automation-creating-importing-runbook.md)
* toounderstand Olá diferenças do PowerShell e o fluxo de trabalho do PowerShell com runbooks, consulte [fluxo de trabalho do PowerShell de aprendizagem](automation-powershell-workflow.md)

