---
title: "Implementar os serviços de aplicação: A pilha do Azure | Microsoft Docs"
description: "Orientação detalhada para implementar o serviço de aplicações na pilha do Azure"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2017
ms.author: anwestg
ms.openlocfilehash: 522e5a334b5165344b66524d03f0d85468b81332
ms.sourcegitcommit: be0d1aaed5c0bbd9224e2011165c5515bfa8306c
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/01/2017
---
# <a name="add-an-app-service-resource-provider-to-azure-stack"></a>Adicionar um fornecedor de recursos do serviço de aplicações a pilha do Azure

Como um operador de nuvem de pilha do Azure, pode conceder aos seus utilizadores a capacidade de criar aplicações API e web. Para tal, terá de adicionar primeiro o [fornecedor de recursos do serviço de aplicações](azure-stack-app-service-overview.md) para a implementação da pilha de Azure conforme descrito neste artigo. Depois de ter instalado o fornecedor de recursos do serviço de aplicações, pode incluí-la nas suas ofertas e planos. Os utilizadores, em seguida, podem subscrever para obter o serviço e começar a criar aplicações.

> [!IMPORTANT]
> Antes de executar o programa de instalação, certifique-se de que seguiu as orientações no [antes de começar](azure-stack-app-service-before-you-get-started.md).
> 
>



## <a name="run-the-app-service-resource-provider-installer"></a>Execute o instalador de fornecedor de recursos do serviço de aplicações

Instalar o fornecedor de recursos do serviço de aplicações para o seu ambiente de pilha do Azure pode demorar até uma hora. Durante este processo, o instalador irá:

* Crie um contentor de BLOBs na conta do storage do Azure pilha especificada.
* Crie uma zona DNS e entradas para o serviço de aplicações.
* Registe o fornecedor de recursos do serviço de aplicações.
* Registe os itens de galeria do serviço de aplicações.

Para implementar o fornecedor de recursos do serviço de aplicações, siga estes passos:

1. Execute appservice.exe como um administrador (azurestack\CloudAdmin).

2. Clique em **implementar o serviço de aplicações na nuvem do Azure pilha**.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image01.png)

3. Reveja e aceite os termos de licenciamento de Software Microsoft e, em seguida, clique em **seguinte**.

4. Reveja e aceite os termos de licença de terceiros e, em seguida, clique em **seguinte**.

5. Certifique-se de que as informações de configuração do serviço de aplicações em nuvem estão corretas. Se utilizou as predefinições durante a implementação do Kit de desenvolvimento de pilha do Azure, pode aceitar os valores predefinidos aqui. No entanto, se as opções personalizado quando implementou a pilha do Azure, tem de editar os valores nesta janela para refletir que. Por exemplo, se utilizar o mycloud.com de sufixo de domínio, o ponto final tem de alterar a management.mycloud.com. Depois de confirmar as suas informações, clique em **seguinte**.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image02.png)

6. Na página seguinte:
    1. Clique em de **Connect** junto ao **subscrições de pilha do Azure** caixa.
        - Se estiver a utilizar o Azure Active Directory (Azure AD), introduza a conta de administrador do Azure AD e a palavra-passe que forneceu quando implementou a pilha do Azure. Clique em **sessão**.
        - Se estiver a utilizar serviços de Federação do Active Directory (AD FS), forneça a sua conta de administrador. Por exemplo, cloudadmin@azurestack.local. Introduza a palavra-passe e clique em **sessão**.
    2. No **subscrições de pilha do Azure** caixa, selecione a sua subscrição.
    3. No **localizações de pilha do Azure** caixa, selecione a localização que corresponde à região estiver a implementar. Por exemplo, seleccione **local** se a implementar o Kit de desenvolvimento de pilha do Azure.
    4. Introduza um **nome do grupo de recursos** para a sua implementação do serviço de aplicações. Por predefinição, está definido como **APPSERVICE\<região\>**.
    5. Introduza o **nome da conta de armazenamento** que pretende que o serviço de aplicações para criar como parte da instalação. Por predefinição, está definido como **appsvclocalstor**.
    6. Clique em **Seguinte**.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image03.png)

7. Introduza as informações para a partilha de ficheiros e, em seguida, clique em **seguinte**. O endereço da partilha de ficheiros tem de utilizar o nome de domínio completamente qualificado do servidor de ficheiros, por exemplo \\\appservicefileserver.local.cloudapp.azurestack.external\websites ou o endereço IP, por exemplo \\\10.0.0.1\websites.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image04.png)

8. Na página seguinte:
    1. No **ID da aplicação de identidade** box, introduza o GUID para a aplicação estiver a utilizar para a identidade (a partir do Azure AD).
    2. No **ficheiro de certificado de identidade aplicação** caixa, introduza (ou navegue até à) a localização do ficheiro de certificado.
    3. No **palavra-passe de certificado de identidade aplicação** caixa, introduza a palavra-passe do certificado. Esta palavra-passe é aquele que anotou quando utilizou o script para criar os certificados.
    4. No **ficheiro de certificado de raiz do Azure Resource Manager** caixa, introduza (ou navegue até à) a localização do ficheiro de certificado.
    5. Clique em **Seguinte**.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image05.png)

9. Para cada uma a três caixas de ficheiro de certificado, clique em **procurar** e navegue para o ficheiro de certificado adequado. Tem de fornecer a palavra-passe para cada certificado. Estes certificados são aqueles que criou no [passo de certificados necessários criar](azure-stack-app-service-deploy.md#create-the-required-certificates). Clique em **seguinte** após introduzir todas as informações.

    | Box | Exemplo de nome de ficheiro de certificado |
    | --- | --- |
    | **Ficheiro de certificado SSL do serviço de aplicações predefinido** | \_. appservice.local.AzureStack.external.pfx |
    | **Ficheiro de certificado SSL de API do serviço de aplicações** | api.appservice.local.AzureStack.external.pfx |
    | **Ficheiro de certificado de SSL de publicador do serviço de aplicações** | ftp.appservice.local.AzureStack.external.pfx |

    Se utilizou um sufixo de domínio diferente ao criar os certificados, não utilizem os nomes de ficheiro de certificado *local. AzureStack.external*. Em alternativa, utilize as informações de domínio personalizado.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image06.png)    

10. Introduza os detalhes do SQL Server para a instância de servidor utilizada para alojar as bases de dados do fornecedor de recursos do serviço de aplicações e, em seguida, clique em **seguinte**. O instalador valida as propriedades de ligação do SQL Server.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image07.png)    

11. Reveja as opções de SKU e a instância de função. As predefinições são preenchidas com o número mínimo de instância e o SKU mínimo para cada função numa implementação ASDK. É fornecido um resumo dos requisitos vCPU e memória para o ajudar a planear a implementação. Depois de efetuar as seleções, clique em **seguinte**.

    > [!NOTE]
    > Para implementações de produção, seguir as orientações no [planeamento de capacidade de funções de servidor do App Service do Azure na pilha de Azure](azure-stack-app-service-capacity-planning.md).
    > 
    >

    | Função | Instâncias mínimas | SKU mínima | Notas |
    | --- | --- | --- | --- |
    | Controlador | 1 | Standard_A1 - (1 vCPU, 1792 MB) | Gere e mantém o estado de funcionamento da nuvem do serviço de aplicações. |
    | Gestão | 1 | Standard_A2 - (vCPUs 2, 3584 MB) | Gere os pontos finais App Service do Azure Resource Manager e API, extensões portais (administrador inquilino, portal das funções) e o serviço de dados. Para suportar a ativação pós-falha, aumentar as instâncias recomendadas para 2. |
    | Publicador | 1 | Standard_A1 - (1 vCPU, 1792 MB) | Publica conteúdo através da implementação web e FTP. |
    | FrontEnd | 1 | Standard_A1 - (1 vCPU, 1792 MB) | Encaminha os pedidos a aplicações de serviço de aplicações. |
    | Trabalho partilhado | 1 | Standard_A1 - (1 vCPU, 1792 MB) | Anfitriões ou aplicações API aplicações web e funções do Azure. Pode querer adicionar mais instâncias. Como um operador, pode definir a sua oferta e escolha qualquer camada SKU. As camadas tem de ter um mínimo de um vCPU. |

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image08.png)    

    > [!NOTE]
    > **Windows Server 2016 Core não é uma imagem de plataforma suportada para utilização com o Azure App Service na pilha de Azure**.

12. No **selecione a imagem de plataforma** caixa, selecione a imagem de máquina virtual de implementação do Windows Server 2016 das disponíveis no fornecedor de recursos de computação para a nuvem de serviço de aplicações. Clique em **Seguinte**.

13. Na página seguinte:
     1. Introduza o nome de utilizador de administrador de máquina virtual de função de trabalho e a palavra-passe.
     2. Introduza o nome de utilizador de administrador de máquina virtual de outras funções e a palavra-passe.
     3. Clique em **Seguinte**.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image09.png)    

14. Na página de resumo:
    1. Certifique-se seleções que fez. Para efetuar alterações, utilize o **anterior** botões para visitar às páginas anteriores.
    2. Se as configurações estão corretas, selecione a caixa de verificação.
    3. Para iniciar a implementação, clique em **seguinte**.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image10.png)    

15. Na página seguinte:
    1. Controle o progresso da instalação. Serviço de aplicações na pilha de Azure demora cerca de 60 minutos para implementar com base nas seleções predefinido.
    2. Depois do programa de instalação for concluída com êxito, clique em **saída**.

    ![Instalador do serviço de aplicações](media/azure-stack-app-service-deploy/image11.png)    


## <a name="validate-the-app-service-on-azure-stack-installation"></a>Validar o serviço de aplicações numa instalação de pilha do Azure

1. No portal de administração de pilha do Azure, aceda a **administração - App Service**.

2. Na descrição geral em estado, certifique-se que o **estado** mostra **todas as funções, estará pronto**.

    ![Gestão de serviço de aplicações](media/azure-stack-app-service-deploy/image12.png)    

## <a name="test-drive-app-service-on-azure-stack"></a>Testar o serviço de aplicações na pilha do Azure

Depois de implementar e registar o fornecedor de recursos do serviço de aplicações, testá-lo para se certificar de que os utilizadores podem implementar web e API apps.

> [!NOTE]
> Terá de criar uma oferta que tenha o espaço de nomes Microsoft. Web dentro do plano. Em seguida, terá de ter uma subscrição de inquilino subscreve esta oferta. Para obter mais informações, consulte [criar oferta](azure-stack-create-offer.md) e [criar plano](azure-stack-create-plan.md).
>
*Tem* ter uma subscrição de inquilino para criar aplicações que utilizam o serviço de aplicações na pilha do Azure. As capacidades de apenas um administrador de serviço pode ser no portal de administração estão relacionadas com a administração de fornecedor de recursos do App Service. Estas capacidades incluem adicionar capacidade, configurar origens de implementação e adicionar camadas de trabalho e SKUs.
>
Criar web, a API e o Azure funciona aplicações, tem de utilizar o portal de inquilinos e ter uma subscrição de inquilino.

1. No portal de inquilinos pilha do Azure, clique em **novo** > **Web + móvel** > **aplicação Web**.

2. No **aplicação Web** painel, escreva um nome no **aplicação Web** caixa.

3. Em **grupo de recursos**, clique em **novo**. Escreva um nome no **grupo de recursos** caixa.

4. Clique em **plano do Serviço de Aplicações/Localização** > **Criar Novo**.

5. No **plano do App Service** painel, escreva um nome no **plano do App Service** caixa.

6. Clique em **escalão de preço** > **livres partilhados** ou **partilhados partilhados** > **selecione**  >   **OK** > **criar**.

7. Na sob um minuto, um mosaico para a nova aplicação web aparece no dashboard. Clique no mosaico.

8. No **aplicação Web** painel, clique em **procurar** para ver o Web site predefinido para esta aplicação.

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a>Implementar um site WordPress, DNN ou Django (opcional)

1. No portal de inquilinos pilha do Azure, clique em  **+** , vá para o Azure Marketplace, implementar um site do Django e aguarde pela conclusão com êxito. A plataforma de web Django utiliza um ficheiro com base no sistema base de dados do. Não requer quaisquer fornecedores de recursos adicionais, tais como SQL Server ou MySQL.

2. Se implementou também um fornecedor de recursos do MySQL, pode implementar um site WordPress no Marketplace. Quando lhe for pedida para parâmetros de base de dados, introduza o nome de utilizador como  *User1@Server1* , com o nome de utilizador e o nome do servidor da sua preferência.

3. Se implementou também um fornecedor de recursos do SQL Server, pode implementar um site DNN do Marketplace. Quando lhe for pedida para parâmetros de base de dados, escolha uma base de dados no computador que executa o SQL Server que está ligada ao seu fornecedor de recursos.

## <a name="next-steps"></a>Passos seguintes

Também pode experimentar o outro [plataforma como dos serviços de serviço (PaaS)](azure-stack-tools-paas-services.md).

- [Fornecedor de recursos do SQL Server](azure-stack-sql-resource-provider-deploy.md)
- [Fornecedor de recursos de MySQL](azure-stack-mysql-resource-provider-deploy.md)

<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
