---
title: aaaCreate artefactos personalizados para a VM do DevTest Labs | Microsoft Docs
description: Saiba como tooauthor seus artefactos para utilizam com o DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Criar artefactos personalizados para a VM do DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Descrição geral
**Artefactos** são utilizado toodeploy e configurar a sua aplicação depois de uma VM está aprovisionada. Um artefacto é composta por um ficheiro de definição de artefacto e outros ficheiros de script são armazenados numa pasta num repositório de git. Ficheiros de definição de artefacto consistem em JSON e expressões que pode utilizar toospecify que pretende tooinstall numa VM. Por exemplo, pode definir o nome de Olá dos parâmetros que são disponibilizados quando Olá comando é executado, toorun de comando e um artefacto. Pode consultar os ficheiros de script de tooother dentro do ficheiro de definição de artefacto Olá por nome.

## <a name="artifact-definition-file-format"></a>Formato de ficheiro de definição de artefactos
Olá exemplo seguinte mostra as secções de Olá que compõem a estrutura básica do Olá de um ficheiro de definição:

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| Nome do elemento | Necessário? | Descrição |
| --- | --- | --- |
| $schema |Não |Localização do ficheiro de esquema JSON Olá que ajuda a validade Olá Olá do ficheiro de definição de teste. |
| Título |Sim |Nome do artefacto de Olá apresentado no laboratório Olá. |
| descrição |Sim |Descrição do artefacto de Olá apresentado no laboratório Olá. |
| iconUri |Não |URI de ícone de Olá apresentado no laboratório Olá. |
| targetOsType |Sim |Sistema operativo de Olá VM onde os artefactos está instalado. As opções suportadas são: Windows e Linux. |
| parâmetros |Não |Valores que são fornecidos quando o comando de instalação do artefacto é executado numa máquina. Isto ajuda a personalizar o artefacto. |
| runCommand |Sim |Comando que é executado numa VM de instalação de artefactos. |

### <a name="artifact-parameters"></a>Parâmetros de artefactos
Na secção de parâmetros de Olá Olá do ficheiro de definição, especifique os valores de um utilizador pode introduzir ao instalar um artefacto. Pode consultar os valores de toothese no comando de instalação do artefacto Olá.

Definir os parâmetros com Olá seguir a estrutura:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Nome do elemento | Necessário? | Descrição |
| --- | --- | --- |
| tipo |Sim |Tipo de valor de parâmetro. Consulte Olá lista para Olá permitido tipos os seguintes: |
| displayName |Sim |Nome do parâmetro de Olá que é o utilizador tooa apresentadas no laboratório Olá. | |
| descrição |Sim |Descrição do parâmetro de Olá que é apresentado no laboratório Olá. |

Olá permitidos tipos são:

* cadeia – qualquer cadeia JSON válida
* Int – qualquer número inteiro JSON válido
* bool – qualquer booleano de JSON válido
* matriz – nenhuma matriz JSON válido

## <a name="artifact-expressions-and-functions"></a>Funções e expressões de artefactos
Pode utilizar expressão e o comando de instalação do artefacto de Olá tooconstruct de funções.
As expressões são colocadas entre parênteses Retos ([e]) e são avaliadas quando artefactos Olá está instalado. As expressões podem aparecer em qualquer local, um valor de cadeia JSON e sempre devolver um valor JSON diferente. Se precisar de toouse uma cadeia literal, que começa com um parêntese [, tem de utilizar dois parênteses Retos [[.
Normalmente, utilizar expressões com funções tooconstruct um valor. Tal como em JavaScript, chamadas de função estejam formatadas como functionName(arg1,arg2,arg3).

Olá lista seguinte mostra as funções comuns:

* Parameters(parameterName) - devolve um valor de parâmetro que é fornecido quando Olá artefactos comando é executado.
* concat (arg1 arg2, arg3,...) - combina vários valores de cadeia. Esta função pode efetuar qualquer número de argumentos.

Olá seguinte exemplo mostra como toouse expressão e funções tooconstruct um valor:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Criar um artefacto personalizado
Crie os seus artefactos personalizados, seguindo estes passos:

1. Instalar um editor de JSON - é necessário um toowork do editor de JSON com ficheiros de definição de artefactos. Recomendamos que utilize [Visual Studio Code](https://code.visualstudio.com/), que está disponível para Windows, Linux e OS X.
2. Obter um exemplo artifactfile.json - modificação artefactos Olá criado pela equipa do Azure DevTest Labs no nosso [repositório do GitHub](https://github.com/Azure/azure-devtestlab), em que foi criado uma biblioteca avançada de artefactos que o ajudam a criar os seus artefactos. Transferir um ficheiro de definição de artefacto e efetuar alterações tooit toocreate seus artefactos.
3. Se utilizar o IntelliSense - tire partido IntelliSense toosee elementos válidos que podem ser utilizado tooconstruct um ficheiro de definição de artefactos. Também pode ver Olá diferentes opções para os valores de um elemento. Por exemplo, o IntelliSense mostrar de Olá duas opções do Windows ou Linux ao editar Olá **targetOsType** elemento.
4. Artefactos de Olá de arquivo num [repositório de git](devtest-lab-add-artifact-repo.md).
   
   1. Crie um diretório separado para cada artefactos em que o nome de diretório Olá é Olá mesmo como nome de artefacto Olá.
   2. Armazenar o ficheiro de definição de artefacto Olá (artifactfile.json) no diretório de Olá que criou.
   3. Comando de instalação de scripts de Olá de arquivo que são referenciados do artefacto de Olá.
      
      Eis um exemplo de como pode ver uma pasta de artefacto:
      
      ![Exemplo de repositório de git de artefactos](./media/devtest-lab-artifact-author/git-repo.png)
5. Adicionar o laboratório de toohello de repositório de artefactos Olá - consulte o artigo toohello, [adicione um repositório de Git para artefactos e modelos](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Artigos relacionados
* [Como falhas de artefacto toodiagnose no DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Associar um domínio do AD utilizando um modelo do resource manager no Azure DevTest Labs de tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[adicionar um laboratório de tooa do repositório de artefactos Git](devtest-lab-add-artifact-repo.md).

