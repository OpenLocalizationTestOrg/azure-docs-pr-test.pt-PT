---
title: Criar e gerir regras de firewall de MySQL na base de dados do Azure para MySQL | Microsoft Docs
description: Criar e gerir a base de dados do Azure MySQL das regras de firewall com o portal do Azure
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 01/20/2018
ms.openlocfilehash: 3ab65ad99b3219060bb044b0e6b84edf3f1737e0
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/22/2018
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-by-using-the-azure-portal"></a>Criar e gerir o Azure base de dados MySQL das regras de firewall com o portal do Azure
Regras de firewall ao nível do servidor permitem que os administradores aceder a uma base de dados do Azure para o servidor de MySQL de um endereço IP especificado ou um intervalo de endereços IP. 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a>Criar uma regra de firewall ao nível do servidor no portal do Azure

1. Na página de servidor MySQL, em definições, clique em **ligação segurança** para abrir a página de segurança de ligação da base de dados do Azure para MySQL.

   ![Portal do Azure – clique em segurança de ligação](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Clique em **Adicionar IP do meu** na barra de ferramentas. Isto cria automaticamente uma regra de firewall com o endereço IP público do seu computador, como percetível pelo sistema do Azure.

   ![Portal do Azure – clique em Adicionar meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. Verifique o seu endereço IP antes de guardar a configuração. Em algumas situações, o endereço IP observado pelo portal do Azure é diferente do endereço IP utilizado ao aceder à internet e os servidores do Azure. Por conseguinte, terá de alterar o IP inicial e o IP final para se a função de regra, conforme esperado.

   Utilize um motor de busca ou outra ferramenta online para verificar o seu próprio endereço IP. Por exemplo, pesquise "qual é o meu endereço IP". 

   ![Bing para saber o que é o meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. Adicione intervalos de endereços adicionais. Nas regras da firewall para a base de dados do Azure para MySQL, pode especificar um único endereço IP ou um intervalo de endereços. Se pretender limitar a regra para um único endereço IP, escreva o mesmo endereço nos campos de IP inicial e final IP. Abrir a firewall permite que os administradores, utilizadores e aplicações para aceder a qualquer base de dados no servidor de MySQL a que tenham credenciais válidas.

   ![Portal do Azure – regras de firewall ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. Clique em **guardar** na barra de ferramentas para guardar esta regra de firewall ao nível do servidor. Aguarde a confirmação de que a atualização para as regras de firewall é efetuada com êxito.

   ![Portal do Azure – clique em Guardar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)

## <a name="connecting-from-azure"></a>Ligar a partir do Azure
Para permitir que as aplicações do Azure ligar à base de dados do Azure para o servidor de MySQL, as ligações do Azure tem de estar ativadas. Por exemplo, para alojar uma aplicação de Web Apps do Azure ou uma aplicação que é executado numa VM do Azure ou para ligar a partir de um gateway de gestão de dados do Azure Data Factory. Os recursos não precisam de estar na mesma rede Virtual (VNET) ou grupo de recursos para a regra de firewall para permitir essas ligações. Quando uma aplicação do Azure tenta ligar ao servidor de base de dados, a firewall verifica se as ligações do Azure são permitidas. Existem dois métodos para ativar estes tipos de ligações. Uma definição de firewall com o endereço de início e de fim igual a 0.0.0.0 indica que estas ligações são permitidas. Em alternativa, pode definir o **permitir o acesso aos serviços do Azure** opção para **ON** no portal do **segurança de ligação** painel e prima **guardar**. Se a tentativa de ligação não for permitida, o pedido não atingir o MySQL servidor da base de dados do Azure.

> [!IMPORTANT]
> Esta opção configura a firewall para permitir todas as ligações a partir do Azure, incluindo ligações de subscrições de outros clientes. Quando seleciona esta opção, certifique-se de que as permissões de início de sessão e de utilizador limitam o acesso a utilizadores autorizados apenas.
> 

## <a name="manage-existing-server-level-firewall-rules-by-using-the-azure-portal"></a>Gerir regras de firewall ao nível do servidor existente utilizando o portal do Azure
Repita os passos para gerir as regras de firewall.
* Para adicionar o computador atual, clique em **+ adicionar My IP**. Clique em **Guardar** para guardar as alterações.
* Para adicionar endereços IP adicionais, escreva o **nome da regra**, **IP inicial**, e **IP final**. Clique em **Guardar** para guardar as alterações.
* Para modificar uma regra existente, clique em qualquer um dos campos existentes na regra e, em seguida, modifique. Clique em **Guardar** para guardar as alterações.
* Para eliminar uma regra existente, clique no botão de reticências [...] e, em seguida, clique em **eliminar**. Clique em **Guardar** para guardar as alterações.


## <a name="next-steps"></a>Passos Seguintes
- Da mesma forma, pode aplicar o script para [criar e gerir a base de dados do Azure para as regras de firewall de MySQL utilizando a CLI do Azure](howto-manage-firewall-using-cli.md).
- Para obter ajuda na ligação para uma base de dados do Azure para o servidor de MySQL, consulte [bibliotecas de ligação para base de dados do Azure para MySQL](./concepts-connection-libraries.md)
