---
title: aaaDesign sua primeira base de dados SQL do Azure | Microsoft Docs
description: Saiba toodesign a sua primeira base de dados SQL do Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a>Conceber a sua primeira base de dados SQL do Azure

Base de dados SQL do Azure é um relacional da base de dados como um serviço (DBaaS) no Olá Microsoft Cloud ("Azure"). Neste tutorial, saiba como toouse Olá portal do Azure e [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) para: 

> [!div class="checklist"]
> * Criar uma base de dados no Olá portal do Azure
> * Configurar uma regra de firewall ao nível do servidor no Olá portal do Azure
> * Ligar a base de dados toohello com SSMS
> * Criar tabelas com o SSMS
> * Carregamento em massa com o BCP
> * Consultar os dados com o SSMS
> * Restaurar Olá tooa de base de dados anterior [ponto no restauro de tempo](sql-database-recovery-using-backups.md#point-in-time-restore) no Olá portal do Azure

Se não tiver uma subscrição do Azure, [criar uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete disponibilizar este tutorial, se tiver instalado:
- versão mais recente do Olá do [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).
- versão mais recente do Olá do [BCP e SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).

## <a name="log-in-toohello-azure-portal"></a>Início de sessão toohello portal do Azure

Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database"></a>Criar uma base de dados do SQL Server em branco

É criada uma base de dados SQL do Azure com um conjunto definido de [recursos de armazenamento e computação](sql-database-service-tiers.md). base de dados de Olá criada dentro de um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md) e num [servidor lógico da SQL Database do Azure](sql-database-features.md). 

Siga estes passos toocreate uma base de dados do SQL Server em branco. 

1. Clique em Olá **novo** botão encontrado no canto esquerda superior Olá de Olá portal do Azure.

2. Selecione **bases de dados** de Olá **novo** página e selecione **base de dados SQL** de Olá **bases de dados** página. 

   ![Criar base de dados vazio](./media/sql-database-design-first-database/create-empty-database.png)

3. Preencha formulário de base de dados SQL Olá com Olá seguintes informações, conforme mostrado no Olá anterior a imagem:   

   | Definição       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome da base de dados** | mySampleDatabase | Para nomes de bases de dados válidos, veja [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificadores de Bases de Dados). | 
   | **Subscrição** | A sua subscrição  | Para obter detalhes sobre as suas subscrições, veja [Subscriptions](https://account.windowsazure.com/Subscriptions) (Subscrições). |
   | **Grupo de recursos** | myResourceGroup | Para nomes de grupo de recursos válidos, veja [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Atribuição de nomes de regras e restrições). |
   | **Selecione a origem** | Base de dados em branco | Especifica que deve ser criada uma base de dados em branco. |

4. Clique em **servidor** toocreate e configurar um novo servidor para a sua nova base de dados. Preencha Olá **novo formulário de servidor** com Olá seguintes informações: 

   | Definição       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nome do servidor** | Qualquer nome globalmente exclusivo | Para nomes de servidores válidos, veja [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Atribuição de nomes de regras e restrições). | 
   | **Início de sessão de administrador do servidor** | Qualquer nome válido | Para nomes de início de sessão válidos, veja [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificadores de Bases de Dados).|
   | **Palavra-passe** | Qualquer palavra-passe válida | A palavra-passe tem de ter, pelo menos, 8 carateres e tem de conter carateres de três das seguintes categorias de Olá: carateres maiúsculos, carateres minúsculos, números e carateres não alfanuméricos. |
   | **Localização** | Nenhuma localização válida | Para obter mais informações sobre regiões, veja [Azure Regions](https://azure.microsoft.com/regions/) (Regiões do Azure). |

   ![criar servidor de base de dados](./media//sql-database-design-first-database/create-database-server.png)

5. Clique em **Selecionar**.

6. Clique em **escalão de preço** toospecify Olá camada e o desempenho do nível de serviço para a sua nova base de dados. Para este tutorial, selecione **20 DTUs** e **250** GB de armazenamento.

   ![criar base de dados-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Clique em **Aplicar**.  

8. Selecione um **agrupamento** para Olá em branco da base de dados (para este tutorial, utilize Olá predefinição). Para obter mais informações sobre agrupamentos, consulte [agrupamentos](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Clique em **criar** base de dados do tooprovision Olá. Aprovisionamento demora sobre toocomplete um minuto e um meio. 

10. Na barra de ferramentas Olá, clique em **notificações** processo de implementação de Olá toomonitor.

   ![notificação](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a>Criar uma regra de firewall ao nível do servidor

Olá serviço base de dados do SQL Server cria uma firewall no Olá ao nível do servidor que impede o ligar toohello servidor ou bases de dados no servidor de Olá, a menos que é criada uma regra de firewall firewall de Olá tooopen para endereços IP específicos de ferramentas e aplicações externas. Siga estes passos toocreate um [regra de firewall ao nível do servidor de base de dados SQL](sql-database-firewall-configure.md) para endereços IP do cliente e ativar a conectividade externa através de firewall de base de dados SQL Olá para apenas o seu endereço IP. 

> [!NOTE]
> A Base de Dados SQL comunica através da porta 1433. Se estiver a tentar tooconnect a partir de uma rede empresarial, o tráfego de saída através da porta 1433 não poderá permitido pela firewall da sua rede. Se assim for, não é possível ligar o servidor de base de dados do Azure SQL tooyour, a menos que o departamento de TI abre-se a porta 1433.
>

1. Depois de concluída a implementação de Olá, clique em **bases de dados SQL** do menu da esquerda Olá e, em seguida, clique em **mySampleDatabase** no Olá **bases de dados SQL** página. Olá página de descrição geral para abre a base de dados, que mostra Olá completamente qualificado nome do servidor (tais como **mynewserver20170313.database.windows.net**) e fornece opções para continuar a configuração. Copie este nome de servidor totalmente qualificado para utilizar mais tarde.

   > [!IMPORTANT]
   > Terá deste servidor de tooyour de tooconnect de nome de servidor completamente qualificado e as respetivas bases de dados subsequentes inícios rápidos.
   > 

   ![nome do servidor](./media/sql-database-connect-query-dotnet/server-name.png) 

2. Clique em **definir a firewall do servidor** na barra de ferramentas de Olá conforme mostrado na imagem anterior Olá. Olá **definições de Firewall** abre a página do servidor de base de dados SQL Olá. 

   ![regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Clique em **Adicionar IP do cliente** no Olá barra de ferramentas tooadd tooa nova regra de firewall de endereços de IP sua atual. Uma regra de firewall consegue abrir a porta 1433 para um único endereço IP ou para um intervalo de endereços IP.

4. Clique em **Guardar**. É criada uma regra de firewall ao nível do servidor para o endereço IP atual ao abrir a porta 1433 no servidor lógico de Olá.

   ![configurar regra de firewall do servidor](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Clique em **OK** e, em seguida, feche Olá **definições de Firewall** página.

Agora pode ligar o servidor de base de dados SQL toohello e respetivas bases de dados utilizando o SQL Server Management Studio ou outra ferramenta à sua escolha deste endereço IP utilizando a conta de administrador de servidor de Olá criada anteriormente.

> [!IMPORTANT]
> Por predefinição, o acesso através de firewall de base de dados SQL Olá está ativado para todos os serviços do Azure. Clique em **OFF** no toodisable página para todos os serviços do Azure.

## <a name="sql-server-connection-information"></a>Informações de ligação do servidor SQL

Obter o nome de servidor completamente qualificado de Olá para o servidor da SQL Database do Azure no Olá portal do Azure. Utilize Olá servidor completamente qualificado tooconnect tooyour ao servidor de nomes utilizando o SQL Server Management Studio.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Selecione **bases de dados SQL** no menu da esquerda do Olá e clique em sua base de dados no Olá **bases de dados SQL** página. 
3. No Olá **Essentials** painel Olá página do portal do Azure para a base de dados, localize e, em seguida, copie Olá **nome do servidor**.

   ![informações da ligação](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a>Ligar a base de dados toohello com SSMS

Utilize [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish um servidor de SQL Database do Azure de tooyour de ligação.

1. Abra o SQL Server Management Studio.

2. No Olá **ligar tooServer** caixa de diálogo, introduza Olá seguintes informações:

   | Definição       | Valor sugerido | Descrição | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | Tipo de servidor | Motor de base de dados | Este valor é necessário |
   | Nome do servidor | nome de servidor completamente qualificado Olá | Olá nome deve ser algo semelhante ao seguinte: **mynewserver20170313.database.windows.net**. |
   | Autenticação | Autenticação do SQL Server | Autenticação de SQL é o tipo de autenticação apenas de Olá que configurámos neste tutorial. |
   | Iniciar sessão | conta de administrador do servidor de Olá | Esta é a conta de Olá que especificou quando criou o servidor de Olá. |
   | Palavra-passe | Olá palavra-passe da sua conta de administrador do servidor | Esta é a palavra-passe de Olá que especificou quando criou o servidor de Olá. |

   ![ligar tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. Clique em **opções** no Olá **ligar tooserver** caixa de diálogo. No Olá **ligar toodatabase** secção, introduza **mySampleDatabase** base de dados do tooconnect toothis.

   ![ligar toodb no servidor](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. Clique em **Ligar**. é aberta a janela do Explorador de objetos de Olá no SSMS. 

5. No Object Explorer, expanda **bases de dados** e, em seguida, expanda **mySampleDatabase** objetos de Olá tooview na base de dados de exemplo de Olá.

   ![Objetos de base de dados](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a>Criar tabelas na base de dados de Olá 

Criar um esquema de base de dados com quatro tabelas que um sistema de gestão do estudante para universities utilizando o modelo [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):

- Pessoa
- Decorrer
- Estudante
- Esse modelo um sistema de gestão do estudante para universities de crédito

Olá diagrama seguinte mostra como estas tabelas estão relacionado tooeach outro. Alguns destas tabelas referenciam colunas nas outras tabelas. Por exemplo, a tabela de estudante Olá referencia Olá **PersonId** coluna Olá **pessoa** tabela. Prático Olá diagrama toounderstand como Olá tabelas neste tutorial são tooone relacionado outro. Para uma visão detalhada das como tabelas de base de dados Efetivo toocreate, consulte [criar tabelas de base de dados Efetivo](https://msdn.microsoft.com/library/cc505842.aspx). Para obter informações sobre como escolher tipos de dados, consulte [tipos de dados](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).

> [!NOTE]
> Também pode utilizar Olá [designer de tabela no SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate e as tabelas de design. 

![Relações de tabela](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. No Object Explorer, clique com o botão direito do rato em **mySampleDatabase** e, em seguida, clique em **Nova Consulta**. Uma janela de consulta em branco abre-se que está ligado tooyour base de dados.

2. Na janela de consulta Olá, execute Olá seguintes quatro tabelas da consulta toocreate na base de dados: 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Criar tabelas](./media/sql-database-design-first-database/create-tables.png)

3. Expanda o nó de 'tabelas' de Olá no Olá objeto do SQL Server Management Studio explorer toosee Olá tabelas criadas por si.

   ![Criar em tabelas do ssms](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a>Carregar dados para tabelas de Olá

1. Crie uma pasta denominada **SampleTableData** nos seus dados de exemplo do transferências pasta toostore da base de dados. 

2. Liga a seguir de Olá de contexto e guardá-las em Olá **SampleTableData** pasta. 

   - [SampleCourseData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [SamplePersonData](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [SampleStudentData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [SampleCreditData](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. Abra uma janela de linha de comandos e navegue toohello SampleTableData pasta.

4. Executar Olá os seguintes dados de exemplo de tooinsert comandos em tabelas de Olá, substituindo os valores de Olá para **ServerName**, **DatabaseName**, **UserName**e **Palavra-passe** com valores de Olá para o seu ambiente.
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

Agora tem carregados dados de exemplo para tabelas de Olá que criou anteriormente.

## <a name="query-data"></a>Consultar dados

Execute Olá seguintes informações de tooretrieve consultas de tabelas de base de dados de Olá. Consulte [escrever consultas de SQL](https://technet.microsoft.com/library/bb264565.aspx) toolearn mais sobre como escrever consultas SQL. consulta primeiro Olá junta toofind quatro tabelas todos os todos os Olá os estudantes que estejam taught por ' Dominick Pope' que tem um nível superior a % de 75 na sua classe. consulta segundo Olá associa as quatro tabelas e localiza todos os courses na qual tenha alguma vez inscrito 'Noe Coleman'.

1. Numa janela de consulta do SQL Server Management Studio, execute Olá seguinte consulta:

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. Numa janela de consulta do SQL Server Management Studio, execute os seguintes consultas:

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Restaurar um ponto anterior de tooa de base de dados no tempo

Imagine que tenha eliminado acidentalmente uma tabela. Este é algo que facilmente não consegue recuperar. Base de dados SQL do Azure permite-lhe toogo back tooany ponto no tempo no Olá última cópia de segurança too35 dias e restaurar este ponto no tempo tooa novos da base de dados. Pode toorecover esta base de dados os dados eliminados. Olá passos seguintes restaurar ponto de tooa de base de dados de exemplo de Olá antes de tabelas de Olá foram adicionadas.

1. Na página de base de dados SQL Olá da base de dados, clique em **restaurar** na barra de ferramentas Olá. Olá **restaurar** é aberta a página.

   ![Restauro](./media/sql-database-design-first-database/restore.png)

2. Preencha Olá **restaurar** formulário com informações de Olá necessário:
    * Nome da base de dados: forneça um nome de base de dados 
    * No momento: Olá selecione **no momento** separador no formulário de restauro Olá 
    * Ponto de restauro: selecione uma hora que ocorre antes de base de dados de Olá foi alterada
    * Servidor de destino: não é possível alterar este valor ao restaurar uma base de dados 
    * Agrupamento elástico de bases de dados: selecione **None**  
    * Escalão de preço: selecione **20 DTUs** e **250 GB** de armazenamento.

   ![ponto de restauro](./media/sql-database-design-first-database/restore-point.png)

3. Clique em **OK** toorestore Olá da base de dados demasiado[restaurar tooa ponto no tempo](sql-database-recovery-using-backups.md#point-in-time-restore) antes de tabelas de Olá foram adicionadas. Restaurar um ponto de diferentes de tooa de base de dados em tempo cria uma base de dados duplicado no Olá mesmo servidor como Olá original da base de dados a partir do ponto de Olá no tempo especificado, desde que está dentro do período de retenção de Olá para sua [camada de serviço](sql-database-service-tiers.md).

## <a name="next-steps"></a>Passos Seguintes 
Neste tutorial, aprendeu a tarefas de base de dados básicas, tais como criar uma base de dados e tabelas, carregar e consultar dados e restaurar Olá da base de dados tooa anterior no tempo. Aprendeu a:
> [!div class="checklist"]
> * Criar uma base de dados
> * Configurar uma regra de firewall
> * Ligar a base de dados de toohello com [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)
> * Criar tabelas
> * Carregamento em massa
> * Consultar os dados
> * Restaurar Olá da base de dados tooa anterior no tempo com a base de dados SQL [ponto no restauro de tempo](sql-database-recovery-using-backups.md#point-in-time-restore) capacidades

Produzir toohello seguinte toolearn tutorial sobre como criar uma base de dados utilizando o Visual Studio e c#.

> [!div class="nextstepaction"]
>[Estruturar uma base de dados SQL do Azure e estabelecer ligação com c# e ADO.NET](sql-database-design-first-database-csharp.md)
