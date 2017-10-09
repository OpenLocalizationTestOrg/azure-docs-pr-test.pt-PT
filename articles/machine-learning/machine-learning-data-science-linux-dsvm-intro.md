---
title: "Olá aaaProvision máquinas de virtuais de ciência de dados de Linux | Microsoft Docs"
description: "Configurar e criar uma Máquina Virtual de ciência de dados de Linux no Azure toodo análise e machine learning."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 81dfa90f6cd4b4f33535a20fb97442bf9152d829
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-linux-data-science-virtual-machine"></a>Aprovisionar Olá máquinas de virtuais de ciência de dados de Linux
Olá máquinas de virtuais de ciência de dados de Linux é uma baseado em CentOS máquina virtual do Azure que vem com uma coleção de ferramentas pré-instaladas. Estas ferramentas são frequentemente utilizadas para fazer a análise de dados e machine learning. componentes de software chave Olá incluídos são:

* Sistema operativo: Distribuição Linux CentOS.
* Edição de programador do Microsoft R
* Distribuição do Python anaconda (versões 2.7 e 3.5), incluindo bibliotecas de análise de dados mais populares
* JuliaPro - uma distribuição organizada de idioma de Leonor com bibliotecas de análise de dados e científicos populares
* Instância de Spark autónomo e de nó único Hadoop (HDFS, Yarn)
* JupyterHub - um servidor de bloco de notas Jupyter multiuser R, Python, PySpark, kernels Leonor de suporte
* Explorador do Storage do Azure
* Interface de linha de comandos do Azure (CLI) para gerir recursos do Azure
* PostgresSQL base de dados
* Ferramentas do Machine learning
  * [Toolkit de rede computacional (CNTK)](https://github.com/Microsoft/CNTK): uma profunda learning toolkit de software da Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): um rápido de machine learning técnicas, como online, hash, allreduce, reductions, learning2search, Active Directory, de suporte do sistema e a configuração interativa.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): uma ferramenta fornecer implementação de árvore rápido e preciso elevada.
  * [Rattle](http://rattle.togaware.com/) (Olá ferramenta analíticos R tooLearn facilmente): uma ferramenta que torna a introdução à análise de dados e a máquina no R fácil, com a exploração de dados baseadas em GUI e modelação com a geração de código de R automática.
* SDK do Azure em Java, Python, node.js, Ruby, PHP
* Bibliotecas na R e Python para utilizam no Azure Machine Learning e outros serviços do Azure
* Ferramentas de desenvolvimento e editores (RStudio PyCharm, IntelliJ, Emacs, gedit, vi)


Se o fizer ciência de dados envolve iterating numa sequência de tarefas:

1. Localizar, carregar e processar previamente os dados
2. Criar e testar modelos
3. Implementação de modelos de Olá para consumo em aplicações inteligentes

Cientistas de dados utilizam várias ferramentas toocomplete estas tarefas. Pode ser bastante demorada toofind Olá adequado as versões do software de Olá, e, em seguida, toodownload, compilar e instalar estas versões.

Olá máquinas de virtuais de ciência de dados de Linux poderá facilitar este fardo substancialmente. Utilizá-lo toojump iniciar o projeto de análise. Permite-lhe toowork nas tarefas em vários idiomas, incluindo R, Python, SQL Server, Java e C++. Eclipse fornece um toodevelop IDE e testar o seu código que seja fácil toouse. Olá incluído no Olá VM do Azure SDK permite-lhe toobuild as suas aplicações através da utilização de vários serviços no Linux para a plataforma de nuvem do Microsoft hello. Além disso, terá acesso tooother idiomas como Ruby, Perl, PHP e node.js que também são instalados previamente.

Não existem sem custos de software para esta imagem VM de ciência de dados. Paga apenas Olá taxas que são analisadas com base no tamanho de Olá da máquina virtual Olá que for aprovisionado com a imagem de VM Olá de utilização de hardware do Azure. Obter mais detalhes sobre Olá computação taxas podem ser encontradas no Olá [página de listagem de VM no Azure Marketplace de Olá ](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Outras versões de Olá máquinas de virtuais de ciência de dados
Um [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) imagem também está disponível, com muitas das Olá mesmo ferramentas como Olá imagem CentOS plus estruturas de aprendizagem profunda. A [Windows](machine-learning-data-science-provision-vm.md) imagem está também disponível.

## <a name="prerequisites"></a>Pré-requisitos
Antes de poder criar uma Máquina Virtual de ciência de dados de Linux, tem de ter o seguinte Olá:

* **Uma subscrição do Azure**: um, ver tooobtain [avaliação gratuita do Azure obter](https://azure.microsoft.com/free/).
* **Uma conta de armazenamento do Azure**: um, ver toocreate [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). Em alternativa, a conta de armazenamento Olá pode ser criada como parte do processo de Olá de criação de Olá VM, se não pretender toouse uma conta existente.

## <a name="create-your-linux-data-science-virtual-machine"></a>Criar a máquina de Virtual de ciência de dados do Linux
Seguem-se Olá passos toocreate uma instância de Olá máquinas de virtuais de ciência de dados de Linux:

1. Navegue até a máquina virtual de toohello listagem no Olá [portal do Azure](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vmlinuxdsvm).
2. Clique em **criar** (na parte inferior do Olá) toobring segurança assistente Olá.![ configurar dados-ciência-vm](./media/machine-learning-data-science-linux-dsvm-intro/configure-linux-data-science-virtual-machine.png)
3. Olá seguintes secções fornece entradas Olá para cada um dos passos de Olá no Assistente de Olá (enumerado na Olá à direita dos Olá precedente figura) utilizado toocreate Olá máquinas de virtuais de ciência de dados de Microsoft. Seguem-se Olá entradas necessárias tooconfigure cada estes passos:
   
   a. **Noções básicas**:
   
   * **Nome**: nome do seu servidor de ciência de dados que está a criar.
   * **Nome de utilizador**: primeira conta de início de sessão ID.
   * **Palavra-passe**: primeira conta palavra-passe (pode utilizar a chave pública SSH em vez da palavra-passe).
   * **Subscrição**: Se tiver mais do que uma subscrição, selecione Olá uma no qual Olá máquina é toobe criado e cobrados. Tem de ter privilégios de criação de recursos para esta subscrição.
   * **Grupo de recursos**: pode criar uma nova ou utilize um grupo existente.
   * **Localização**: Centro de dados de Olá selecione que for mais apropriado. Normalmente, é Centro de dados de Olá que tem a maioria dos seus dados, ou está mais próximo tooyour de localização física para acesso de rede mais rápido.
   
   b. **Tamanho**:
   
   * Selecione um dos tipos de servidor Olá que cumpra os requisitos funcionais e restrições de custo. Selecione **ver tudo** toosee mais opções de tamanhos de VM.
   
   c. **Definições**:
   
   * **Tipo de disco**: escolha **Premium** se preferir uma unidade de estado sólido (SSD). Caso contrário, escolha **padrão**.
   * **Conta de armazenamento**: pode criar uma nova conta de armazenamento do Azure na sua subscrição ou utilize uma já existente no Olá mesma localização que escolheu no Olá **Noções básicas** passo do Assistente de Olá.
   * **Outros parâmetros**: na maioria dos casos, utilize apenas os valores predefinidos de Olá. os valores não predefinidos de tooconsider, paire sobre a ligação de informativa Olá para ajudá-lo em campos específicos Olá.
   
   d. **Resumo**:
   
   * Certifique-se de que todas as informações que introduziu estão corretas.
   
   e. **Comprar**:
   
   * toostart Olá aprovisionamento, clique em **comprar**. Termos de toohello de transação de Olá é fornecida uma ligação. Olá VM não tem quaisquer taxas adicionais para além de computação de Olá para o tamanho de servidor Olá escolheu no Olá **tamanho** passo.

Aprovisionamento de Olá deve demorar cerca de 10 a 20 minutos. Estado de Olá de aprovisionamento de Olá é apresentado no Olá portal do Azure.

## <a name="how-tooaccess-hello-linux-data-science-virtual-machine"></a>Como tooaccess Olá máquinas de virtuais de ciência de dados de Linux
Depois de Olá que é criada a VM, pode iniciar sessão tooit utilizando SSH. Utilizar as credenciais da conta de Olá que criou no Olá **Noções básicas** secção do passo 3 para a interface de shell Olá texto. No Windows, pode transferir uma ferramenta de cliente SSH como [Putty](http://www.putty.org). Se preferir um ambiente de trabalho gráfico (X Windows sistema), pode utilizar o Putty de reencaminhamento de X11 ou instalar Olá X2Go cliente.

> [!NOTE]
> cliente de Olá X2Go efetuada significativamente melhor do que nos testes de reencaminhamento de X11. Recomendamos que utilize o cliente de X2Go Olá para uma interface gráfica do ambiente de trabalho.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Instalar e configurar o cliente X2Go
Olá VM com Linux já está aprovisionado com o servidor de X2Go e ligações de cliente tooaccept pronto. tooconnect toohello ambiente de trabalho gráfico de VM com Linux, Olá seguintes no cliente:

1. Transferir e instalar o cliente de Olá X2Go para a sua plataforma de cliente de [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Execute cliente Olá X2Go e selecione **nova sessão**. É aberta uma janela de configuração com vários separadores. Introduza Olá seguir os parâmetros de configuração:
   * **Separador sessões**:
     * **Anfitrião**: nome de anfitrião de Olá ou endereço IP da sua VM de ciência de dados do Linux.
     * **Início de sessão**: nome de utilizador no Olá VM com Linux.
     * **Porta SSH**: deixe-22, valor de predefinido Olá.
     * **Tipo de sessão**: alteração Olá valor tooXFCE. Atualmente Olá VM com Linux só suporta o ambiente de trabalho XFCE.
   * **Separador de suporte de dados**: pode desativar o suporte de som e cliente impressão se não precisa de toouse-los.
   * **Pastas partilhadas**: Se pretender que diretórios das suas máquinas de cliente montadas em Olá VM com Linux, adicione os diretórios de máquina Olá cliente que pretende que o tooshare com Olá VM neste separador.

Depois de iniciar sessão toohello VM ao utilizar o cliente SSH Olá ou o ambiente de trabalho gráfico XFCE através do cliente de X2Go Olá, está pronto toostart utilizando Olá ferramentas que estão instaladas e configuradas no Olá VM. No XFCE, pode ver os atalhos de menu de aplicações e ícones do ambiente de trabalho para muitas das ferramentas de Olá.

## <a name="tools-installed-on-hello-linux-data-science-virtual-machine"></a>Ferramentas instaladas no Olá máquinas de virtuais de ciência de dados de Linux
### <a name="microsoft-r-server"></a>Servidor Microsoft R
R é um dos idiomas mais populares do Olá para análise de dados e de aprendizagem. Se quiser toouse R para a sua análise, Olá VM tem Microsoft R Server (MRS) com Olá Microsoft R abrir (MRO) e a biblioteca de Kernel de bibliotecas (MKL). Olá MKL otimiza operações bibliotecas comuns no algoritmos analíticos. MRO é 100 por cento compatível com CRAN R e qualquer uma das bibliotecas de Olá R publicadas no CRAN podem ser instaladas em Olá MRO. MRS dá-lhe dimensionar e operationalization dos modelos de R para os serviços web. Pode editar os programas de R dos editores de predefinição Olá, como RStudio, vi, Emacs ou gedit. Se estiver a utilizar o editor de Emacs Olá, tenha em atenção esse pacote de Emacs Olá RIMIR (Emacs Speaks as estatísticas), que simplifica a trabalhar com ficheiros de R dentro do editor de Emacs Olá, tenha sido previamente instalado.

consola toolaunch R, basta escrever **R** na shell de Olá. Isto leva-o ambiente interativa tooan. toodevelop seu programa de R, normalmente, utilize um editor como Emacs ou vi ou gedit e, em seguida, executar scripts de Olá dentro do R. Com RStudio, tiver um ambiente toodevelop completa gráfica do IDE do programa de R.

Há também um script do R para tooinstall Olá [pacotes primeiros 20 R](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) se pretender. Este script pode ser executado após estiver na interface interativa de Olá R, o que pode ser introduzida (tal como mencionado) escrevendo **R** na shell de Olá.  

### <a name="python"></a>Python
Para o desenvolvimento com o Python, distribuição Anaconda Python 2.7 e 3.5 foi instalada. Esta distribuição contém Olá base Python juntamente com cerca de 300 Olá mais populares dados, engenharia e bibliotecas de análise pacotes. Pode utilizar editores de texto Olá predefinido. Além disso, pode utilizar Spyder, um IDE do Python que está incluído com as distribuições de Anaconda Python. Spyder necessita de um ambiente de trabalho gráfico ou X11 reencaminhamento. É fornecido um tooSpyder atalho no ambiente de trabalho gráfico Olá.

Uma vez que temos o Python 2.7 e 3.5, terá de toospecifically ativar versão Python Olá pretendida (conda ambiente) que pretende toowork no Olá sessão atual. processo de ativação de Olá define a versão pretendida do toohello variável de caminho de Olá do Python.

tooactivate Olá Python 2.7 conda ambiente, execute o seguinte de Olá a partir da shell de Olá:

    source /anaconda/bin/activate root

Python 2.7 está instalado no */anaconda/bin*.

tooactivate Olá Python 3.5 conda ambiente, execute o seguinte de Olá a partir da shell de Olá:

    source /anaconda/bin/activate py35


Python 3.5 está instalado no */anaconda/envs/py35/bin*.

tooinvoke uma sessão interativa de Python, basta escrevê **python** na shell de Olá. Se estiver numa interface gráfica ou ter o conjunto de cópias de segurança de reencaminhamento de X11, pode escrever **pycharm** toolaunch Olá PyCharm IDE do Python.

bibliotecas de Python adicionais tooinstall, terá de toorun ```conda``` ou ````pip```` comandos em sudo e forneça o caminho completo do Gestor de pacotes de Python Olá (conda ou pip) tooinstall toohello correto ambiente Python. Por exemplo:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Bloco de notas do Jupyter
Olá distribuição Anaconda também inclui um bloco de notas do Jupyter, um código de tooshare de ambiente e a análise. notas do Jupyter Olá é acedida através do JupyterHub. Inicie sessão com o nome de utilizador de Linux local e a palavra-passe.

servidor de bloco de notas do Jupyter Olá foi previamente configurado com o Python 2, Python 3 e R kernels. Não há um ícone de ambiente de trabalho com o nome do servidor de bloco de notas ao hello do tooaccess de browser "Notas do Jupyter" toolaunch Olá. Se tiver Olá VM através do cliente SSH ou X2Go, também pode visitar [https://localhost:8000 /](https://localhost:8000/) tooaccess Olá servidor de bloco de notas do Jupyter.

> [!NOTE]
> Continue se obter quaisquer avisos de certificado.
> 
> 

Pode aceder ao servidor de bloco de notas do Jupyter Olá de qualquer anfitrião. Basta escrevê *https://\<nome DNS de VM ou o endereço IP\>: 8000 /*

> [!NOTE]
> Porta 8000 está aberta na firewall de Olá por predefinição quando Olá VM está aprovisionado.
> 
> 

Podemos ter empacotada exemplo blocos de notas – Python num e um em R. Pode ver exemplos de toohello Olá ligação na home page do bloco de notas Olá depois de se autenticar notas do Jupyter toohello utilizando o seu nome de utilizador de Linux local e a palavra-passe. Pode criar um novo bloco de notas, selecionando **novo**e, em seguida, kernel do Olá idioma apropriado. Se não vir Olá **novo** botão, clique em Olá **Jupyter** ícone na Olá superior toogo esquerdo toohello home page do servidor de bloco de notas Olá.

### <a name="apache-spark-standalone"></a>Apache Spark autónomo 
Uma instância autónoma do Apache Spark está pré-instalado Olá toohelp Linux DSVM desenvolver aplicações do Spark localmente primeiro antes de testar e implementar em grandes clusters. Pode executar programas PySpark através de kernel de Jupyter Olá. Quando abrir o Jupyter e clique no botão "Novo" de Olá deverá ver uma lista de kernels disponíveis. Olá "Spark - Python" é o kernel do PySpark Olá que lhe permite criar Spark aplicações utilizando a linguagem de Python. Também pode utilizar um IDE do Python como PyCharm ou Spyder toobuild que Spark programa. Desde, esta é uma instância autónoma, a pilha de Spark Olá é executado dentro de Olá chamar o programa de cliente. Isto torna mais rápido e mais fácil tootroubleshoot problemas com toodeveloping num cluster do Spark. 

Um bloco de notas do PySpark de exemplo é fornecido no Jupyter que pode encontrar no diretório de "SparkML" Olá sob o diretório de raiz de Olá de Jupyter ($HOME/blocos de notas/SparkML/pySpark). 

Se estiver de programação R para Spark, pode utilizar o Microsoft R Server, SparkR ou sparklyr. 

Antes de executar no contexto do Spark no Microsoft R Server, terá de toodo uma instância de Yarn e um tempo configuração passo tooenable um único nó Hadoop HDFS local. Por predefinição, os serviços do Hadoop são instalados mas desativados no Olá DSVM. Ordem tooenable, é necessário Olá toorun os seguintes comandos como Olá raiz pela primeira vez:

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

Pode parar Olá Hadoop relacionados com serviços quando não precisar deles executando ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` uma amostra que demonstra como MRS toodevelop e teste no contexto de Spark remoto (que é a instância de Spark Olá autónoma no Olá DSVM) é fornecido e está disponível no Olá `/dsvm/samples/MRS` diretório. 

### <a name="ides-and-editors"></a>IDEs e editores
Tem de escolher entre vários editores de código. Isto inclui vi/VIM, Emacs, gEdit, PyCharm, RStudio, Eclipse e IntelliJ. gEdit, Eclipse, IntelliJ, RStudio e PyCharm são editores gráficas e tem de toobe com sessão iniciada toouse de ambiente de trabalho gráfico tooa-los. Estes editores tem o ambiente de trabalho e aplicações menu Atalhos toolaunch-los.

**VIM** e **Emacs** são editores baseados em texto. Em Emacs, iremos tenha instalado um pacote de suplemento chamado Emacs Speaks estatísticas (RIMIR) que facilita a trabalhar com R dentro do editor de Emacs Olá. Podem encontrar mais informações em [RIMIR](http://ess.r-project.org/).

**Eclipse** é uma abertura de origem, IDE extensível que suporta vários idiomas. edição de programadores do Java Olá é uma instância Olá instalada Olá VM. Existem plug-ins disponíveis para vários idiomas populares que podem ser o ambiente de Olá tooextend instalado. Além disso, temos um plug-in instalado no Eclipse chamado **Toolkit do Azure para o Eclipse**. Permite-lhe toocreate, desenvolver, testar e implementar aplicações do Azure utilizando o ambiente de desenvolvimento de Eclipse Olá suporta idiomas como Java. Há também um **Azure SDK para Java** que permite acesso toodifferent serviços do Azure a partir de um ambiente de Java. Mais informações sobre o toolkit do Azure para o Eclipse podem ser encontradas em [Toolkit do Azure para o Eclipse](../azure-toolkit-for-eclipse.md).

**LaTex** está instalada através do pacote de texlive Olá juntamente com um suplemento Emacs [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) pacote, o que simplifica a criação os documentos LaTex dentro Emacs.  

### <a name="databases"></a>Bases de Dados
#### <a name="postgres"></a>Postgres
base de dados de origem aberta de Olá **Postgres** está disponível no Olá VM, com os serviços de Olá em execução e initdb já foi concluída. Ainda precisa de toocreate bases de dados e utilizadores. Para obter mais informações, consulte Olá [Postgres documentação](https://www.postgresql.org/docs/).  

#### <a name="graphical-sql-client"></a>Cliente gráfica do SQL Server
**SQuirrel SQL**, foi fornecido um gráfico cliente SQL, bases de dados do tooconnect toodifferent (como o Microsoft SQL Server, Postgres e MySQL) e as consultas SQL toorun. Pode executar este partir de uma sessão de ambiente de trabalho gráfica (utilizando o cliente de X2Go Olá, por exemplo). tooinvoke SQuirrel SQL, pode iniciar a partir do ícone de Olá no ambiente de trabalho Olá ou executar o seguinte comando na shell de Olá de Olá.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Antes de Olá utilizar em primeiro lugar, configure os controladores e os aliases de base de dados. controladores JDBC Olá estão localizados em:

*/usr/share/Java/jdbcdrivers*

Para obter mais informações, consulte [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Ferramentas de linha de comandos para aceder ao Microsoft SQL Server
pacote de controladores ODBC Olá para o SQL Server também inclui duas ferramentas da linha de comandos:

**BCP**: em massa do utilitário de bcp Olá copia dados entre uma instância do Microsoft SQL Server e um ficheiro de dados num formato especificado por um utilizador. o utilitário bcp de Olá pode ser utilizados tooimport grande número de novas linhas em tabelas do SQL Server ou tooexport dados fora de tabelas para ficheiros de dados. tooimport dados numa tabela, tem de utilizar um ficheiro de formato criado para essa tabela, ou compreender a estrutura de Olá da tabela de Olá e tipos de Olá de dados que são válidos para as colunas.

Para obter mais informações, consulte [estabelecer ligação com o bcp](https://msdn.microsoft.com/library/hh568446.aspx).

**SQLCMD**: pode introduzir instruções Transact-SQL com o utilitário sqlcmd de Olá, bem como os procedimentos de sistema e ficheiros Olá linha de comandos do script. Este utilitário utiliza lotes de tooexecute Transact-SQL de ODBC.

Para obter mais informações, consulte [ligar com sqlcmd](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> Existem algumas diferenças neste utilitário entre plataformas Linux e Windows. Consulte a documentação de Olá para obter mais detalhes.
> 
> 

#### <a name="database-access-libraries"></a>Bibliotecas de acesso de base de dados
Bibliotecas estão disponíveis nas bases de dados de tooaccess do R e Python.

* No R, Olá **RODBC** pacote ou **dplyr** pacote permite-lhe tooquery ou executar instruções SQL no servidor de base de dados de Olá.
* No Python, Olá **pyodbc** biblioteca fornece acesso a base de dados com ODBC como Olá camada subjacente.  

tooaccess **Postgres**:

* De r: Utilize Olá o pacote **RPostgreSQL**.
* Olá de utilização do Python: **psycopg2** biblioteca.

### <a name="azure-tools"></a>Ferramentas do Azure
Olá seguintes ferramentas do Azure está instalado no Olá VM:

* **Interface de linha de comandos do Azure**: Olá CLI do Azure permite-lhe toocreate e gerir recursos do Azure através de comandos da shell. tooinvoke Olá ferramentas do Azure, basta escrevê **do azure ajuda**. Para obter mais informações, consulte Olá [página de documentação do CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Explorador de armazenamento do Microsoft Azure**: Explorador de armazenamento do Microsoft Azure é uma ferramenta gráfica que é utilizado toobrowse através de objetos de Olá que tem de ser armazenados na sua conta do storage do Azure e tooupload e transferência tooand de dados de blobs do Azure. Pode aceder a Explorador de armazenamento do ícone de atalho do ambiente de trabalho de Olá. Pode invocar a partir de uma linha de shell, escrevendo **StorageExplorer**. Tem sessão iniciada a partir de um cliente X2Go de toobe ou ter o conjunto de cópias de segurança de reencaminhamento de X11.
* **Bibliotecas do Azure**: Olá seguem-se algumas das bibliotecas de Olá pré-instaladas.
  
  * **Python**: Olá relacionadas com o Azure, as bibliotecas no Python que está instalados estão **azure**, **azureml**, **pydocumentdb**, e **pyodbc** . Com Olá três primeiros bibliotecas, pode aceder a serviços de armazenamento do Azure, Azure Machine Learning e base de dados do Azure Cosmos (uma base de dados NoSQL no Azure). biblioteca de quarta Olá, pyodbc (juntamente com Olá Microsoft ODBC driver para SQL Server), permite acesso tooSQL Server, SQL Database do Azure e Azure SQL Data Warehouse do Python através de uma interface ODBC. Introduza **lista pip** toosee todas Olá listados bibliotecas. Ser toorun se este comando em ambos os Olá Python 2.7 e 3.5 ambientes.
  * **R**: Olá relacionadas com o Azure, as bibliotecas no R instalados estão **AzureML** e **RODBC**.
  * **Java**: lista de Olá das bibliotecas de Java do Azure pode ser encontrada no diretório de Olá **/dsvm/sdk/AzureSDKJava** no Olá VM. bibliotecas de chave Olá são Azure armazenamento e gestão de APIs, base de dados do Azure Cosmos e JDBC controladores para o SQL Server.  

Pode aceder ao hello [portal do Azure](https://portal.azure.com) do browser de Firefox pré-instaladas Olá. Olá portal do Azure, pode criar, gerir e monitorizar os recursos do Azure.

### <a name="azure-machine-learning"></a>Azure Machine Learning
O Azure Machine Learning é um serviço em nuvem completamente gerido que lhe permite toobuild, implementar e partilhar as soluções de Análise Preditiva. Criar os modelos e experimentações do Azure Machine Learning Studio. Pode ser acedido a partir de um browser web na máquina de virtual de ciência de dados de Olá, visitando [Microsoft Azure Machine Learning](https://studio.azureml.net).

Depois de iniciar sessão tooAzure Machine Learning Studio, terá acesso tooan experimentação tela onde pode criar um fluxo lógico Olá algoritmos do machine learning. Também tem de notas do Jupyter acesso tooa alojada no Azure Machine Learning e pode trabalhar de forma totalmente integrada com experimentações Olá no Machine Learning Studio. Operacionalize Olá modelos de machine learning que criou envolvendo-los numa interface de serviço web. Isto permite aos clientes escritos em qualquer predições tooinvoke de idioma de Olá modelos de machine learning. Para obter mais informações, consulte Olá [documentação de Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

Pode também criar os seus modelos no R ou Python no Olá VM e, em seguida, implementá-la na produção no Azure Machine Learning. Iremos instalou bibliotecas R (**AzureML**) e Python (**azureml**) tooenable esta funcionalidade.

Para obter informações sobre como toodeploy modelos no R e Python no Azure Machine Learning, consulte [dez coisas que pode fazer no Olá ciência de dados de Máquina Virtual](machine-learning-data-science-vm-do-ten-things.md) (em particular, Olá secção "Criar modelos de utilizar o R ou Python e Operacionalizá-las utilizar o Azure Machine Learning").

> [!NOTE]
> Estas instruções destinam-se a versão do Windows hello do Olá VM de ciência de dados. Mas as informações de Olá fornecidas não existe na implementação de modelos tooAzure Machine Learning são aplicável toohello VM com Linux.
> 
> 

### <a name="machine-learning-tools"></a>Ferramentas do Machine learning
Olá VM inclui alguns do machine learning ferramentas e algoritmos que tenham sido pré-compilado e previamente instalados localmente. Estas incluem:

* **CNTK** (computacional Toolkit de rede da Microsoft Research): uma profunda toolkit de aprendizagem.
* **Vowpal Wabbit**: um algoritmo de aprendizagem rápido online.
* **xgboost**: uma ferramenta que proporciona algoritmos da árvore otimizada, elevada.
* **Python**: Anaconda Python vem agrupada com algoritmos do machine learning com bibliotecas como saber de Scikit. Pode instalar outras bibliotecas utilizando Olá `pip install` comando.
* **R**: uma biblioteca completa de funções do machine learning está disponível para R. Algumas das bibliotecas de Olá que estão instaladas previamente são lm, glm, randomForest, rpart. Outras bibliotecas de podem ser instaladas através da execução:
  
        install.packages(<lib name>)

Eis algumas informações adicionais sobre Olá primeiro três ferramentas de aprendizagem máquina na lista de Olá.

#### <a name="cntk"></a>CNTK
Este é um código aberto, profunda toolkit de aprendizagem. É uma ferramenta da linha de comandos (cntk) e já está a ser Olá caminho.

toorun um exemplo básico, execute Olá os seguintes comandos na shell de Olá:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Para obter mais informações, consulte Olá secção CNTK [GitHub](https://github.com/Microsoft/CNTK)e Olá [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit é uma sistema operativo que utiliza técnicas, como online, hash, allreduce, reductions, learning2search, Active Directory, de aprendizagem e a configuração interativa.

ferramenta de Olá toorun em obter um exemplo muito básica, Olá seguintes:

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Existem outras, maior demonstrações nesse diretório. Para obter mais informações sobre VW, consulte [nesta secção do GitHub](https://github.com/JohnLangford/vowpal_wabbit)e Olá [Vowpal Wabbit wiki](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>xgboost
Esta é uma biblioteca que está concebida e otimizada para algoritmos (árvore elevada). objetivo Olá desta biblioteca é limites de cálculo de Olá toopush do extremes de toohello máquinas necessário tooprovide o árvore em grande escala os aumentos que seja escalável, portáteis e precisos.

É fornecido como uma linha de comandos, bem como uma biblioteca de R.

toouse nesta biblioteca no R, pode iniciar uma sessão interativa de R (apenas escrevendo **R** na shell de Olá) e o carregamento da biblioteca Olá.

Eis um exemplo simples, que pode executar numa linha de comandos do R:

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

linha de comandos do toorun Olá xgboost, seguem-se Olá comandos tooexecute na shell de Olá:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


Um ficheiro de .model é escrito toohello diretório especificado. Pode encontrar informações sobre este exemplo de demonstração [no GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Para obter mais informações sobre xgboost, consulte Olá [página de documentação xgboost](https://xgboost.readthedocs.org/en/latest/)e a respetiva [repositório do GitHub](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Rattle
Rattle (Olá **R** **A**nalytical **T**ool **T**Nã **L**mais significativos beneficiar **i** asily) utiliza a exploração de dados baseadas em GUI e modelação. Apresenta estatísticas e resumos visual de dados, os dados de transformações que podem ser prontamente modelados, cria supervisionados e supervisionados os modelos de dados de Olá, apresenta Olá desempenho dos modelos graficamente e define dados pontuações de novo. Também gera código do R, replicar Olá as operações no Olá IU que podem ser executadas diretamente no R ou utilizadas como um ponto de partida para análise adicional.

toorun Rattle, terá de toobe numa gráfica ambiente de trabalho início de sessão. No terminal Olá, escreva ```R``` tooenter ambiente de Olá R. Na linha de Olá R, introduza Olá os seguintes comandos:

    library(rattle)
    rattle()

Agora uma interface gráfica abre-se com um conjunto de separadores. Seguem-se Olá início rápido os passos em toouse Rattle necessário um conjunto de dados de Meteorologia de exemplo e criar um modelo. Em alguns dos passos de Olá abaixo, são tooautomatically pedido instalar e carregar alguns pacotes necessários do R que ainda não no sistema de Olá.

> [!NOTE]
> Se não tiver o pacote do acesso tooinstall Olá no diretório do sistema Olá (predefinição Olá), pode ver uma mensagem na sua R consola janela tooinstall pacotes tooyour biblioteca pessoal. Resposta *y* se vir estes pedidos.
> 
> 

1. Clique em **Executar**.
2. Uma caixa de diálogo aparece, pedimos-lhe se como o conjunto de dados de Meteorologia de exemplo Olá toouse. Clique em **Sim** exemplo de Olá tooload.
3. Clique em Olá **modelo** separador.
4. Clique em **executar** toobuild uma árvore de decisões.
5. Clique em **desenhar** da árvore de decisões de Olá toodisplay.
6. Clique em Olá **floresta** botão de opção e clique em **executar** toobuild uma floresta aleatória.
7. Clique em Olá **Evaluate** separador.
8. Clique em Olá **risco** botão de opção e clique em **executar** rastreia de desempenho do toodisplay dois risco (Cumulative).
9. Clique em Olá **registo** Olá do separador tooshow gerar código de R para Olá precedente operações.
   (Devido a erros de tooa na versão atual do Olá do Rattle, terá de tooinsert um  *#*  caráter à frente do *exportar este registo...*  no texto Olá do registo de Olá.)
10. Clique em Olá **exportar** botão toosave Olá R ficheiro do script com o nome *weather_script. R* toohello de pasta raiz.

Pode sair Rattle e R. Agora pode modificar o script do R Olá gerado ou utilizá-la conforme for toorun-la em qualquer altura toorepeat tudo o que foi concluído dentro do Olá Rattle IU. Especialmente para principiantes em R, esta é uma forma fácil tooquickly fazer Analysis Services e machine learning numa interface gráfica simple, ao gerar automaticamente o código no R toomodify e/ou saber mais.

## <a name="next-steps"></a>Passos seguintes
Eis como pode continuar a exploração e de aprendizagem automática:

* Olá [ciência de dados no Olá máquinas de virtuais de ciência de dados de Linux](machine-learning-data-science-linux-dsvm-walkthrough.md) instruções mostram-lhe como tooperform várias ciência de dados comuns de tarefas com Olá VM de ciência de dados de Linux aprovisionados aqui. 
* Explore Olá várias ferramentas de ciência de dados no Olá ciência de dados VM tentando saída ferramentas Olá descritas neste artigo. Também pode executar *dsvm-mais-info* na shell de Olá dentro da máquina virtual de Olá para um básico introdução e ponteiros toomore informações sobre as ferramentas de Olá instaladas na VM de Olá.  
* Saiba como soluções de analíticos toobuild ponto-a-ponto utilizando sistematicamente Olá [o processo de ciência de dados de equipa](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Visite Olá [galeria do Cortana análise](http://gallery.cortanaanalytics.com) para análise de dados e de aprendizagem máquina amostras Olá que utilize Cortana Analytics Suite.

