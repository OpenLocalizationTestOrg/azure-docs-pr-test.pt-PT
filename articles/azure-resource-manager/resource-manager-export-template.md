---
title: modelo do Azure Resource Manager aaaExport | Microsoft Docs
description: Utilize o Azure Resource Manager tooexport um modelo a partir de um grupo de recursos existente.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>Exportar um modelo do Azure Resource Manager a partir de recursos existentes
Neste artigo, saiba como tooexport um modelo do Resource Manager a partir dos recursos existentes na sua subscrição. Pode utilizar esse modelo gerado de toogain uma melhor compreensão da sintaxe do modelo.

Existem duas formas tooexport um modelo:

* Pode exportar Olá **modelo utilizado para a implementação**. modelo exportado Olá inclui todos os parâmetros de Olá e variáveis exatamente como estes apareceu no modelo original Olá. Esta abordagem é útil quando tiver implementado recursos através do portal de Olá e pretende toosee Olá modelo toocreate esses recursos. Este modelo pode ser utilizado imediatamente. 
* Pode exportar um **gerou modelo que representa o estado atual do Olá Olá do grupo de recursos**. modelo exportado Olá não é baseado em qualquer modelo que utilizou para a implementação. Em vez disso, cria um modelo que é um instantâneo Olá do grupo de recursos. modelo exportado Olá tem muitos valores codificados e provavelmente não tantos parâmetros como normalmente seriam definidos. Esta abordagem é útil quando modificar grupo de recursos de Olá após a implementação. Normalmente, este modelo requer modificações antes de poder ser utilizado.

Este tópico mostra ambas as abordagens através do portal Olá.

## <a name="deploy-resources"></a>Implementar recursos
Vamos começar por implementar tooAzure de recursos que pode utilizar para exportar como um modelo. Se já tiver um grupo de recursos na sua subscrição que pretende que o modelo de tooa tooexport, pode ignorar esta secção. resto Olá deste artigo parte do princípio de que implementou Olá web app e a solução de base de dados do SQL Server apresentados nesta secção. Se utilizar uma solução diferente, a sua experiência poderá ser ligeiramente diferente, mas passos Olá tooexport um modelo são Olá mesmo. 

1. No Olá [portal do Azure](https://portal.azure.com), selecione **novo**.
   
      ![selecionar novo](./media/resource-manager-export-template/new.png)
2. Procurar **aplicação web + SQL** e selecione-a partir das opções disponíveis Olá.
   
      ![procurar aplicação Web e SQL](./media/resource-manager-export-template/webapp-sql.png)

3. Selecione **Criar**.

      ![selecione criar](./media/resource-manager-export-template/create.png)

4. Fornece valores de Olá necessário para Olá web app e a base de dados SQL. Selecione **Criar**.

      ![forneça o valor da aplicação Web e do SQL](./media/resource-manager-export-template/provide-web-values.png)

a implementação de Olá pode demorar um minuto. Após a conclusão da implementação de Olá, a sua subscrição contém a solução de Olá.

## <a name="view-template-from-deployment-history"></a>Ver o modelo no histórico de implementações
1. Aceda toohello painel do grupo de recursos para o novo grupo de recursos. Tenha em atenção que painel Olá mostra o resultado de Olá da última implementação de Olá. Selecione essa ligação.
   
      ![painel do grupo de recursos](./media/resource-manager-export-template/select-deployment.png)
2. Pode ver um histórico de implementações de grupo Olá. No seu caso, o painel de Olá provavelmente lista apenas uma implementação. Selecione essa implementação.
   
     ![última implementação](./media/resource-manager-export-template/select-history.png)
3. Painel Olá mostra um resumo da implementação de Olá. Olá resumo inclui o estado de Olá da implementação de Olá e respetivas operações e a valores de Olá que fornecido para os parâmetros. modelo de Olá toosee que utilizou para a implementação de Olá, selecione **ver modelo**.
   
     ![ver resumo da implementação](./media/resource-manager-export-template/view-template.png)
4. O Resource Manager obtém Olá sete ficheiros para os seguintes:
   
   1. **Modelo** -modelo Olá que define a infraestrutura de Olá para a sua solução. Quando criou a conta de armazenamento Olá através do portal Olá, o Gestor de recursos utilizados toodeploy um modelo e guardou esse modelo para consulta futura.
   2. **Os parâmetros** -um ficheiro de parâmetros que pode utilizar toopass valores durante a implementação. Contém Olá valores que indicou durante a primeira implementação de Olá. Pode alterar qualquer um destes valores quando implementar novamente o modelo de Olá.
   3. **CLI** -Azure uma interface de linha comandos (CLI) ficheiro do script que pode utilizar o modelo de Olá toodeploy.
   3. **CLI 2.0** -Azure uma interface de linha comandos (CLI) ficheiro do script que pode utilizar o modelo de Olá toodeploy.
   4. **PowerShell** -ficheiro de script de um Azure PowerShell que pode utilizar o modelo de Olá toodeploy.
   5. **.NET** -uma classe .NET que pode utilizar o modelo de Olá toodeploy.
   6. **Ruby** -classe A Ruby que pode utilizar o modelo de Olá toodeploy.
      
      ficheiros de Olá estão disponíveis através de ligações no painel de Olá. Por predefinição, o painel de Olá apresenta modelo Olá.
      
       ![ver modelo](./media/resource-manager-export-template/see-template.png)
      
Este modelo é utilizar o modelo real Olá toocreate a aplicação web e a base de dados SQL. Tenha em atenção que contém os parâmetros que lhe permitem valores diferentes de tooprovide durante a implementação. toolearn mais informações sobre a estrutura de Olá de um modelo, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).

## <a name="export-hello-template-from-resource-group"></a>Exportar o modelo de Olá do grupo de recursos
Se tiver alterado os recursos ou adicionou recursos nas implementações de vários manualmente, a obtenção de um modelo do histórico de implementação de Olá não reflete o estado atual do Olá Olá do grupo de recursos. Esta secção mostra como tooexport um modelo que reflete Olá estado atual do grupo de recursos de Olá. 

> [!NOTE]
> Não pode exportar um modelo para um grupo de recursos que tenha mais de 200 recursos.
> 
> 

1. modelo de Olá tooview para um grupo de recursos, selecione **scripts de automatização**.
   
      ![exportar grupo de recursos](./media/resource-manager-export-template/select-automation.png)
   
     Gestor de recursos avalia Olá recursos no grupo de recursos de Olá e gera um modelo para esses recursos. Nem todos os tipos de recursos suportam a função de modelo de exportação de Olá. Poderá ver um erro a indicar que existe um problema com a exportação de Olá. Saiba a forma como a toohandle os problemas na Olá [corrigir problemas de exportação](#fix-export-issues) secção.
2. Verá novamente os ficheiros de seis Olá que pode utilizar a solução de Olá tooredeploy. No entanto, este modelo de Olá tempo é ligeiramente diferente. Tenha em atenção que Olá modelo gerado contém parâmetros menos do que o modelo de Olá na secção anterior. Além disso, muitos dos valores de Olá (como a localização e valores SKU) estão hard-coded neste modelo, em vez de aceitar um valor de parâmetro. Antes de a reutilizar este modelo, pode querer tooedit Olá modelo toomake melhor utilização de parâmetros. 
   
3. Tem duas opções para continuar a toowork com este modelo. Pode transferir o modelo de Olá e trabalhar no mesmo localmente com um editor de JSON. Em alternativa, pode guardar a biblioteca de tooyour Olá modelos e trabalhar no mesmo através do portal Olá.
   
     Se estiver familiarizado com um editor de JSON como [VS Code](https://code.visualstudio.com/) ou [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), poderá preferir transferir modelo de Olá localmente e utilizar essa editor. toowork localmente, selecione **transferir**.
   
      ![transferir modelo](./media/resource-manager-export-template/download-template.png)
   
     Se não estiverem definidas cópias de segurança com um editor de JSON, poderá preferir editar Olá modelo através do portal Olá. resto Olá deste tópico parte do princípio de que foi guardado com biblioteca de tooyour Olá modelos no portal de Olá. No entanto, se a mesma Olá sintaxe alterações toohello modelo se trabalhar localmente com um editor de JSON ou através do portal Olá. Selecione toowork através do portal Olá, **adicionar toolibrary**.
   
      ![Adicionar toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     Ao adicionar uma biblioteca de modelos de toohello, dê o modelo de Olá um nome e descrição. Em seguida, selecione **Guardar**.
   
     ![definir os valores do modelo](./media/resource-manager-export-template/save-library-template.png)
4. tooview um modelo guardado na biblioteca, selecione **mais serviços**, tipo **modelos** toofilter resultados, selecionados **modelos**.
   
      ![localizar modelos](./media/resource-manager-export-template/find-templates.png)
5. Selecione o modelo de Olá com o nome de Olá guardou.
   
      ![selecionar modelo](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Personalizar o modelo de Olá
Olá exportada modelo funciona bem que se quiser toocreate Olá mesmo web app e a base de dados SQL para todas as implementações. No entanto, o Resource Manager fornece opções para que possa implementar modelos com uma flexibilidade muito maior. Este artigo mostra como parâmetros de tooadd para Olá da base de dados nome administrador e a palavra-passe. Pode utilizar este mesmo tooadd de abordagem mais flexibilidade para outros valores no modelo de Olá.

1. modelo do toocustomize Olá, selecione **editar**.
   
     ![mostrar modelo](./media/resource-manager-export-template/select-edit.png)
2. Selecione o modelo de Olá.
   
     ![editar modelo](./media/resource-manager-export-template/select-added-template.png)
3. valores de Olá toopass capaz de toobe que poderá ser útil toospecify durante a implementação, adicionar Olá seguir dois parâmetros toohello **parâmetros** secção no modelo de Olá:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse Olá novos parâmetros, substitua a definição do servidor SQL Olá no Olá **recursos** secção. Repare que **administratorLogin** e **administratorLoginPassword** utilizam agora os valores dos parâmetros.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. Selecione **OK** quando tiver concluído a edição de modelo de Olá.
7. Selecione **guardar** modelo de toohello toosave Olá alterações.
   
     ![guardar modelo](./media/resource-manager-export-template/save-template.png)
8. modelo de Olá atualizado tooredeploy, selecione **implementar**.
   
     ![implementar modelo](./media/resource-manager-export-template/redeploy-template.png)
9. Fornecer valores de parâmetros e selecione um recurso grupo toodeploy Olá recursos.


## <a name="fix-export-issues"></a>Corrigir problemas de exportação
Nem todos os tipos de recursos suportam a função de modelo de exportação de Olá. tooresolve este problema, manualmente adicionar recursos em falta Olá no seu modelo. mensagem de erro de saudação inclui tipos de recursos de Olá que não não possível exportar. Localize o tipo de recurso na [Referência a modelos](/azure/templates/). Por exemplo, toomanually adicionar um gateway de rede virtual, consulte [referência ao modelo Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).

> [!NOTE]
> Só encontra problemas de exportação se exportar a partir de um grupo de recursos em vez do seu histórico de implementação. Se a última implementação representar com precisão o estado atual do Olá Olá do grupo de recursos, deve exportar modelo Olá do histórico de implementação de Olá, em vez do grupo de recursos de Olá. Só deve exporte de um grupo de recursos quando efetuou um grupo de recursos de toohello alterações que não estão definidas num único modelo.
> 
> 

## <a name="next-steps"></a>Passos seguintes
Aprendeu como tooexport um modelo a partir dos recursos que criou no portal de Olá.

* Pode implementar um modelo através do [PowerShell](resource-group-template-deploy.md), do [CLI do Azure](resource-group-template-deploy-cli.md) ou da [API REST](resource-group-template-deploy-rest.md).
* toosee como tooexport um modelo através do PowerShell, consulte [utilizar o Azure PowerShell com o Azure Resource Manager](powershell-azure-resource-manager.md).
* toosee como tooexport um modelo através da CLI do Azure, consulte [Olá utilize CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).

