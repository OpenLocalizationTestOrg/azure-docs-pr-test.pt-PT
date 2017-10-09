---
title: aaaBuild e implementar um modelo de machine learning utilizar o SQL Server numa VM do Azure | Microsoft Docs
description: "Processo de análise avançada e tecnologia em ação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Olá o processo de ciência de dados de equipa em ação: utilizar o SQL Server
Neste tutorial, a guiá-lo através do processo de Olá de criar e implementar um modelo de machine learning com o SQL Server e um conjunto de dados publicamente disponível – hello [NYC Taxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados. procedimento Olá segue um fluxo de trabalho de ciências de dados padrão: inserção e explorar dados Olá, criar learning de toofacilitate de funcionalidades, em seguida, criar e implementar um modelo.

## <a name="dataset"></a>NYC Taxi viagens descrição do conjunto de dados
Olá dados NYC Taxi viagem cerca de 20GB de ficheiros CSV comprimidos (GB de ~ 48 descomprimido), que inclui mais de milhões de 173 viagens individuais e Olá fares paga para cada viagem. Cada registo viagem inclui a localização de recolha e drop-off Olá e a hora, acesso anónimos (controlador) número de licença e número de medallion (id exclusivo do taxi). dados Olá abrange todos os viagens no ano de Olá 2013 e são fornecidos na Olá seguir dois conjuntos de dados de cada mês:

1. Olá 'trip_data' CSV contém detalhes viagem, tais como o número de passageiros, recolha e dropoff pontos, duração de viagem e comprimento viagem. Seguem-se alguns registos de exemplo:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Olá 'trip_fare' CSV contém detalhes de fare Olá paga para cada viagem, tais como o tipo de pagamento, a quantidade de fare, surcharge e taxas, sugestões e tolls e quantidade total de Olá paga. Seguem-se alguns registos de exemplo:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

viagem de toojoin de chave exclusivo Olá\_dados e viagem\_fare é composto por campos Olá: medallion, acesso\_licenciamento e a recolha\_datetime.

## <a name="mltasks"></a>Exemplos de predição de tarefas
Iremos irá formular três problemas de predição com base no Olá *sugestão\_quantidade*, nomeadamente:

1. Classificação do binária: prever ou não uma sugestão foi paga para uma viagem, ou seja, um *sugestão\_quantidade* que é superior ao $0 é um exemplo positivo, enquanto um *sugestão\_quantidade* $ 0 é um exemplo negativo.
2. Classificação de várias classes: intervalo de Olá toopredict de sugestão paga para viagem Olá. Iremos dividir Olá *sugestão\_quantidade* em cinco intervalos binários ou classes:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Tarefa de regressão: quantidade de Olá toopredict de sugestão paga para uma viagem.  

## <a name="setup"></a>Configurar a definição Olá dados do Azure ciência ambiente para análise avançada
Como pode ver partir Olá [planear o ambiente](machine-learning-data-science-plan-your-environment.md) guia, existem várias opções toowork com Olá NYC Taxi viagens conjunto de dados do Azure:

* Trabalhar com dados Olá em blobs do Azure e o modelo no Azure Machine Learning
* Carregar dados de Olá para uma base de dados do SQL Server e o modelo no Azure Machine Learning

Neste tutorial, iremos demonstrar importação de paralelo em massa de Olá tooa de dados do SQL Server, exploração de dados, a funcionalidade de engenharia e para baixo amostragem utilizando o SQL Server Management Studio, bem como utilizar IPython bloco de notas. [Scripts de exemplo](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) e [IPython blocos de notas](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) são partilhados no GitHub. Um toowork de bloco de notas do exemplo IPython com dados Olá em blobs do Azure também está disponível no Olá mesma localização.

tooset configurar o ambiente de ciência de dados do Azure:

1. [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md)
2. [Criar uma área de trabalho do Azure Machine Learning](machine-learning-create-workspace.md)
3. [Aprovisionar uma máquina de Virtual de ciência de dados](machine-learning-data-science-setup-sql-server-virtual-machine.md), que fornece um SQL Server e um servidor de IPython bloco de notas.
   
   > [!NOTE]
   > scripts de exemplo de Olá e IPython blocos de notas serão transferidos tooyour máquinas de ciência de dados durante o processo de configuração de Olá. Quando tiver concluído a Olá script de pós-instalação de VM, exemplos de Olá estarão disponíveis na biblioteca de documentos da VM:  
   > 
   > * Scripts de exemplo:`C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Blocos de notas do exemplo IPython:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   onde `<user_name>` é o nome de início de sessão do Windows da VM. Iremos dar toohello pastas de exemplo como **Scripts de exemplo** e **blocos de notas do exemplo IPython**.
   > 
   > 

Com base no tamanho do conjunto de dados de Olá, localização da origem de dados e ambiente de destino do Azure selecionada Olá, este cenário é semelhante demasiado[cenário \#5: SQL Server numa VM do Azure de destino do conjunto de dados grande nos ficheiros de locais,](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Obter Olá dados a partir da origem público
Olá tooget [NYC Taxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados da sua localização pública, poderá utilizar qualquer um dos métodos de Olá descritos na [tooand mover dados do Blob Storage do Azure](machine-learning-data-science-move-azure-blob.md) toocopy Olá dados tooyour nova a máquina virtual.

dados de Olá toocopy utilizando o AzCopy:

1. Inicie sessão na máquina de virtual tooyour (VM)
2. Criar um novo diretório num disco de dados da VM Olá (Nota: não utilize Olá disco temporário vem com Olá VM como um disco de dados).
3. Na janela de linha de comandos, execute Olá seguinte linha de comandos do Azcopy, substituindo < path_to_data_folder > com a sua pasta de dados que criou no (2):
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Quando tiver concluído a Olá AzCopy, um total de 24 zipado ficheiros CSV (12 para viagem\_dados e 12 para viagem\_fare) deve estar na pasta de dados de Olá.
4. Descomprimir ficheiros de Olá transferido. Tenha em atenção a pasta de olá onde residem os ficheiros de Olá descomprimido. Esta pasta irá ser referido tooas Olá < caminho\_para\_dados\_ficheiros\>.

## <a name="dbload"></a>Dados de importação em massa na base de dados do SQL Server
Olá desempenho de carregamento/transferência de grandes quantidades de dados tooan SQL da base de dados e consultas subsequentes pode ser melhorado utilizando *particionada tabelas e vistas*. Nesta secção, iremos segui instruções Olá descritas em [paralelo em massa importar utilizando o SQL Server partição tabelas de dados](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate um nova base de dados e carregar Olá dados em tabelas particionadas em paralelo.

1. Enquanto tem sessão iniciada no tooyour VM, iniciar **SQL Server Management Studio**.
2. Estabelecer ligação utilizando a autenticação do Windows.
   
    ![Ligação SSMS][12]
3. Se ainda não tiver alterado o modo de autenticação do SQL Server Olá e criado um novo utilizador de início de sessão do SQL Server, abra o ficheiro de script de Olá denominado **alterar\_auth.sql** no Olá **Scripts de exemplo** pasta. Alterar o nome de utilizador predefinido Olá e a palavra-passe. Clique em **! Executar** no script de Olá toorun do Olá barra de ferramentas.
   
    ![Executar o Script][13]
4. Certifique-se de e/ou alterar Olá predefinido da base de dados e registo pastas tooensure que recém-criado bases de dados será armazenado no disco de dados do SQL Server. imagem de VM do SQL Server de Olá está otimizada para cargas de datawarehousing está pré-configurada com discos de dados e de registo. Se a VM não inclui um disco de dados e adicionar novos discos rígidos virtuais durante o processo de configuração VM de Olá, altere pastas predefinidas de Olá da seguinte forma:
   
   * Nome do SQL Server de Olá de contexto no Olá à esquerda painel e clique em **propriedades**.
     
       ![Propriedades do SQL Server][14]
   * Selecione **definições de base de dados** de Olá **selecionar uma página** lista toohello esquerda.
   * Certifique-se de e/ou alterar Olá **localizações predefinidas de base de dados** toohello **disco de dados** localizações à sua escolha. Este é onde novas bases de dados residem se criada com as definições de localização do Olá predefinidas.
     
       ![Predefinições de base de dados do SQL Server][15]  
5. toocreate uma nova base de dados e um conjunto de grupos de ficheiros toohold Olá tabelas particionadas, abra o script de exemplo de Olá **criar\_db\_default.sql**. script de Olá irá criar uma nova base de dados com o nome **TaxiNYC** e 12 grupos de ficheiros na localização de dados do Olá predefinida. Cada grupo de ficheiros irá conter um mês de viagem\_dados e viagem\_fare dados. Modificar o nome da base de dados de Olá, se assim o desejar. Clique em **! Executar** script de Olá toorun.
6. Em seguida, crie duas tabelas de partição, um para viagem Olá\_dados e outra para viagem Olá\_fare. Abra o script de exemplo de Olá **criar\_particionada\_table.sql**, que irá:
   
   * Crie uma partição função toosplit Olá de dados por mês.
   * Crie um toomap de esquema de partição de dados tooa outro grupo de ficheiros cada mês.
   * Criar dois esquema de partição de tabelas particionadas toohello mapeada: **nyctaxi\_viagem** vai conter viagem Olá\_dados e **nyctaxi\_fare** vai conter viagem Olá \_fare dados.
     
     Clique em **! Executar** toorun Olá script e criar tabelas de Olá particionada.
7. No Olá **Scripts de exemplo** pasta, existem dois scripts do PowerShell de exemplo fornecidos toodemonstrate importações de paralelo em massa tooSQL servidor de tabelas de dados.
   
   * **BCP\_paralelas\_generic.ps1** é um script genérico tooparallel em massa importar dados para uma tabela. Modificar este script tooset Olá entrada e de destino variáveis conforme indicado nas linhas de comentários de Olá no script de Olá.
   * **BCP\_paralelas\_nyctaxi.ps1** é uma versão de pré-configurada do script genérico Olá e pode ser utilizado tootooload ambas as tabelas de dados de NYC Taxi viagens Olá.  
8. Contexto Olá **bcp\_paralelas\_nyctaxi.ps1** nome do script e clique em **editar** tooopen-lo no PowerShell. Olá revisão variáveis da configuração predefinida e modificar de acordo com nome de base de dados selecionada tooyour, pasta de dados de entrada, pasta de registo de destino e ficheiros de formato de exemplo do caminhos toohello **nyctaxi_trip.xml** e **nyctaxi\_ fare.XML** (fornecidas Olá **Scripts de exemplo** pasta).
   
    ![Dados de importação em volume][16]
   
    Também pode selecionar o modo de autenticação de Olá, a predefinição é a autenticação do Windows. Clique em seta verde Olá no Olá toorun de barra de ferramentas. script de Olá iniciará 24 operações de importação de em massa em paralelo, 12 para cada tabela particionada. Pode monitorizar o progresso de importação de dados de Olá, abrindo a pasta de dados predefinida do Olá do SQL Server como conjunto acima.
9. relatórios de script do PowerShell Olá Olá inicial e final vezes. Quando todos os em massa importações concluída, é comunicado Olá hora de fim. Verificação Olá destino registo pasta tooverify que Olá em massa importações teve êxito, ou seja, sem erros reportados na pasta de registo de destino Olá.
10. A base de dados está agora pronto para exploração, engenharia da funcionalidade e outras operações conforme pretendido. Uma vez que as tabelas de Olá são particionadas toohello de acordo com **recolha\_datetime** campo, consultas, que incluem **recolha\_datetime** condições em Olá  **ONDE** cláusula será vantajoso contar com o esquema de partição Olá.
11. No **SQL Server Management Studio**, explore o script de exemplo de Olá fornecido **exemplo\_queries.sql**. toorun qualquer uma das consultas de exemplo de Olá, realce Olá linhas de consulta, em seguida, clique em **! Executar** na barra de ferramentas Olá.
12. Olá dados NYC Taxi viagens será carregado no duas tabelas separadas. operações de associação de tooimprove, recomenda-se vivamente tabelas de Olá tooindex. script de exemplo de Olá **criar\_particionada\_index.sql** cria índices particionados na chave de associação composto Olá **medallion, acesso\_licença e recolha\_datetime**.

## <a name="dbexplore"></a>Exploração de dados e de engenharia da funcionalidade no SQL Server
Nesta secção, iremos efetuar geração de exploração e funcionalidade de dados através da execução de consultas SQL diretamente no Olá **SQL Server Management Studio** utilizar Olá do SQL Server da base de dados criada anteriormente. Um script de exemplo com o nome **exemplo\_queries.sql** é fornecido na Olá **Scripts de exemplo** pasta. Modificar o nome de base de dados do Olá script toochange Olá, se for diferente do predefinido Olá: **TaxiNYC**.

Neste exercício, iremos:

* Ligar demasiado**SQL Server Management Studio** utilizando a autenticação do Windows ou utilizando a autenticação do SQL Server e Olá nome de início de sessão do SQL Server e a palavra-passe.
* Explore as distribuições de dados de alguns campos no variando intervalos de tempo.
* Investigue a qualidade dos dados de campos de latitude e longitude de Olá.
* Gerar etiquetas de classificação de várias classes e binária com base no Olá **sugestão\_quantidade**.
* Gerar funcionalidades e computação/comparar as distâncias de viagem.
* Associar tabelas Olá dois e extrair amostra aleatória que será utilizado toobuild modelos.

Quando estiver pronto tooproceed tooAzure Machine Learning, o utilizador pode optar por:  

1. Guardar Olá final SQL tooextract e exemplo Olá dados e copiar-colar Olá consulta diretamente para um [importar dados] [ import-data] módulo no Azure Machine Learning, ou
2. Manter Olá amostragem e foi desenvolvidos dados planear toouse para criação de uma nova base de dados do modelo de tabela e utilizam nova tabela de Olá Olá [importar dados] [ import-data] módulo no Azure Machine Learning.

Nesta secção, irá guardar Olá consulta final tooextract e exemplo Olá os dados. segundo método de Olá é demonstrado nos Olá [exploração de dados e funcionalidade de engenharia no bloco de notas do IPython](#ipnb) secção.

Para uma verificação rápida do número de Olá de linhas e colunas no Olá tabelas preenchido anteriormente utilizando a importação de paralelo em massa,

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Exploração: Distribuição de viagem por medallion
Neste exemplo identifica medallion Olá (taxi números) com mais do que 100 viagens dentro de um determinado período de tempo. consulta de Olá seria beneficiar de acesso de tabela Olá particionada desde que está a ter pelo esquema de partição Olá da **recolha\_datetime**. Consultar o conjunto de dados completo Olá também faz com que a utilização de tabela particionada Olá e/ou a análise de índice.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploração: Distribuição de viagem medallion e hack_license
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Avaliação de qualidade de dados: Verificar os registos com incorreto longitude e/ou latitude
Neste exemplo investiga se qualquer um dos campos de longitude e/ou latitude Olá ou contém um valor inválido (radian graus devem ser entre -90 e 90), ou ter (0, 0) coordenadas.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Exploração: Vs Tipped. Distribuição de Tipped viagens não
Neste exemplo localiza o número de Olá de viagens foram tipped vs tipped não num determinado momento período (ou em Olá conjunto de dados completo se que abrangem ano completa Olá). Esta distribuição reflete Olá etiqueta binário distribuição toobe posteriormente utilizado para a modelação de classificação binária.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Exploração: Distribuição de classe/intervalo de sugestão
Neste exemplo calcula a distribuição de Olá de intervalos de sugestão num determinado momento período (ou em Olá conjunto de dados completo se que abrangem ano completa Olá). Esta é a distribuição de Olá das classes de etiqueta Olá que serão utilizados mais tarde para a modelação de classificação de várias classes.

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a>Exploração: Computação e comparar distância viagem
Neste exemplo converte longitude de recolha e drop-off Olá e pontos de geografia de tooSQL latitude, calcula distância de viagem Olá utilizando a diferença de pontos de geografia SQL e devolve uma amostra aleatória de resultados de Olá para comparação. exemplo de Olá limita os resultados de Olá toovalid coordena a utilizar apenas Olá qualidade assessment a consulta de dados abrangida anteriormente.

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a>Engenharia da funcionalidade em consultas SQL
Olá etiqueta geração geografia conversão exploração consultas e também podem ser utilizado toogenerate etiquetas/funcionalidades removendo Olá contando parte. Exemplos SQL de engenharia funcionalidades adicionais são fornecidos na Olá [exploração de dados e funcionalidade de engenharia no bloco de notas do IPython](#ipnb) secção. É mais eficientes toorun Olá funcionalidade geração consultas no conjunto de dados completo Olá ou um subconjunto do mesmo através de consultas SQL que executam diretamente na instância de base de dados do SQL Server de Olá grande. consultas de Olá podem ser executadas na **SQL Server Management Studio**, IPython bloco de notas ou qualquer ferramenta/ambiente de desenvolvimento que pode aceder ao hello da base de dados localmente ou remotamente.

#### <a name="preparing-data-for-model-building"></a>A preparar os dados para a criação de modelo
Olá associações de consulta seguinte Olá **nyctaxi\_viagem** e **nyctaxi\_fare** tabelas, gera uma etiqueta de classificação binária **tipped**, um etiqueta de classificação de classe Multi **sugestão\_classe**e extrai uma amostra aleatória de 1% do Olá conjunto de dados completa associados. Esta consulta pode ser copiada e colada diretamente no Olá [Azure Machine Learning Studio](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta da base de dados do Olá do SQL Server instância no Azure. consulta de Olá exclui registos com incorreto (0, 0) coordenadas.

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <a name="ipnb"></a>Exploração de dados e de engenharia da funcionalidade no bloco de notas do IPython
Nesta secção, iremos efetuar exploração de dados e a geração de funcionalidade através de consultas de Python e SQL na base de dados do SQL Server Olá criada anteriormente. Um exemplo IPython bloco de notas com o nome **machine-Learning-data-science-process-sql-story.ipynb** é fornecido na Olá **blocos de notas do exemplo IPython** pasta. Este bloco de notas também está disponível no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Olá recomendado sequência quando trabalhar com macrodados é seguinte Olá:

* Ler um exemplo de dados de Olá pequeno para um intervalo de dados em memória.
* Efetuar algumas visualizações e explorations utilizando Olá amostras de dados.
* Experimentar a engenharia da funcionalidade utilizando dados Olá amostragem.
* Para maior exploração de dados, a manipulação de dados e de engenharia da funcionalidade, utilize as consultas de SQL do Python tooissue diretamente na base de dados do SQL Server Olá Olá VM do Azure.
* Decida toouse de tamanho de exemplo de Olá para criação de modelo do Azure Machine Learning.

Quando está preparado tooproceed tooAzure Machine Learning, o utilizador pode optar por:  

1. Guardar Olá final SQL tooextract e exemplo Olá dados e copiar-colar Olá consulta diretamente para um [importar dados] [ import-data] módulo no Azure Machine Learning. Este método é demonstrado nos Olá [edifício modelos no Azure Machine Learning](#mlmodel) secção.    
2. Manter Olá amostragem e os dados foi desenvolvidos planear toouse para criação de uma nova tabela de base de dados do modelo, em seguida, utilizar a nova tabela de Olá no Olá [importar dados] [ import-data] módulo.

Olá seguem-se alguns exploração de dados, visualização de dados e funcionalidade exemplos de engenharia. Para obter mais exemplos, consulte o bloco de notas do Olá exemplo IPython de SQL no Olá **blocos de notas do exemplo IPython** pasta.

#### <a name="initialize-database-credentials"></a>Inicializar as credenciais da base de dados
Inicializar as definições de ligação de base de dados no Olá seguintes variáveis:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Criar a ligação de base de dados
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Número de relatório de linhas e colunas na tabela nyctaxi_trip
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* Número total de linhas = 173179759  
* Número total de colunas = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Leia-in de uma amostra de dados de pequena de Olá base de dados do SQL Server
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

Tabela de exemplo do tempo tooread Olá é 6.492000 segundos  
Número de linhas e colunas obter = (84952, 21)

#### <a name="descriptive-statistics"></a>Estatísticas descritivas
Agora está pronto tooexplore dados de Olá amostragem. Iremos começar a utilizar ao procurar estatísticas descritivas para Olá **viagem\_distância** (ou qualquer outro) campo (s):

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Visualização: Exemplo de desenho de caixa
Em seguida, observe o desenho de caixa de Olá para Olá viagem distância toovisualize Olá quantiles

    df1.boxplot(column='trip_distance',return_type='dict')

![Desenhar #1][1]

#### <a name="visualization-distribution-plot-example"></a>Visualização: Exemplo de desenho de distribuição
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Desenhar #2][2]

#### <a name="visualization-bar-and-line-plots"></a>Visualização: Barra e Plots de linha
Neste exemplo, vamos bin distância de viagem Olá em cinco intervalos binários e visualizar Olá discretização resultados.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Iremos pode desenhar Olá acima distribuição bin na barra de uma ou linha desenho tal como indicado abaixo

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Desenhar #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Desenhar #4][4]

#### <a name="visualization-scatterplot-example"></a>Visualização: Exemplo de Scatterplot
Vamos mostrar o desenho de gráfico de dispersão entre **viagem\_tempo\_no\_seg** e **viagem\_distância** toosee se não houver qualquer correlação

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Desenhar #6][6]

Da mesma forma, pode verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Desenhar #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Olá amostragem secundárias dados no SQL Server
Quando preparar dados para o modelo de criação num [Azure Machine Learning Studio](https://studio.azureml.net), ou pode optar Olá **toouse de consulta SQL diretamente no módulo de importar dados de Olá** ou manter Olá foi desenvolvido e amostragem dados numa tabela nova, que pode utilizar num Olá [importar dados] [ import-data] módulo com um simples **SELECIONAR * FROM < sua\_novo\_tabela\_nome >**.

Nesta secção, que iremos criar uma nova toohold Olá da tabela amostragem e foi desenvolvido dados. Um exemplo de uma consulta SQL direta para a criação de modelo é fornecido na Olá [exploração de dados e funcionalidade de engenharia no SQL Server](#dbexplore) secção.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Crie uma tabela de exemplo e Populate com % 1 de Olá associado tabelas. Remova a primeira tabela se existir.
Nesta secção, vamos associar tabelas Olá **nyctaxi\_viagem** e **nyctaxi\_fare**, a extrair uma amostra aleatória de 1% e manter dados Olá amostragem um novo nome de tabela  **nyctaxi\_um\_por cento**:

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Exploração de dados através de consultas de SQL no bloco de notas do IPython
Nesta secção, vamos explorar as distribuições de dados utilizando os dados de 1% amostragem Olá, que são mantidos numa tabela nova Olá que criámos acima. Tenha em atenção que podem ser executadas explorations semelhantes utilizando tabelas original Olá, utilizando opcionalmente **TABLESAMPLE** toolimit exploração de Olá exemplo ou ao limitar Olá resulta tooa dado período de tempo utilizando Olá **recolha \_datetime** partições, conforme ilustrado nas Olá [exploração de dados e funcionalidade de engenharia no SQL Server](#dbexplore) secção.

#### <a name="exploration-daily-distribution-of-trips"></a>Exploração: Distribuição diária viagens
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Exploração: Viagem distribuição por medallion
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Geração de funcionalidade através de consultas SQL no bloco de notas do IPython
Nesta secção, irá gerar novas etiquetas e funcionalidades, utilizando diretamente as consultas SQL, operar na tabela de 1% exemplo Olá criámos na secção anterior Olá.

#### <a name="label-generation-generate-class-labels"></a>Geração de etiqueta: Gerar etiquetas de classe
No seguinte exemplo de Olá, iremos gerar dois conjuntos de toouse etiquetas para a modelação:

1. Binário de classe de etiquetas **tipped** (prever se uma sugestão terá)
2. Etiquetas de várias classes **sugestão\_classe** (prever bin de sugestão de Olá ou intervalo)
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Engenharia da funcionalidade: Funcionalidades de contagem para colunas Categórico
Neste exemplo transforma um campo categórico num campo numérico ao substituir cada categoria com contagem de Olá dos respetivos ocorrências nos dados de Olá.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Engenharia da funcionalidade: Funcionalidades de reciclagem para colunas numérico
Neste exemplo transforma um campo numérico contínuo em intervalos de categoria predefinidas, ou seja, transformação campo numérico para um campo categórico.

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Engenharia da funcionalidade: Extrair as funcionalidades de localização de Decimal Latitude/Longitude
Neste exemplo divide representação decimal de Olá de um campo de latitude e/ou longitude em vários campos de região de granularidade diferente, tais como país, cidade, town, blocos, etc. Tenha em atenção que Olá novos georreplicação-campos não são mapeados tooactual localizações. Para obter informações sobre localizações de geocode de mapeamento, consulte [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Verificar o formulário de final Olá da tabela de featurized Olá
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Iremos agora está pronto tooproceed toomodel criação e implementação de modelo no [Azure Machine Learning](https://studio.azureml.net). dados de Olá estão prontos para qualquer um dos problemas de predição de Olá identificados anteriormente, nomeadamente:

1. Classificação do binária: toopredict ou não uma sugestão foi paga para uma viagem.
2. Classificação de várias classes: intervalo de Olá toopredict de sugestão paga, de acordo com toohello classes definidas anteriormente.
3. Tarefa de regressão: quantidade de Olá toopredict de sugestão paga para uma viagem.  

## <a name="mlmodel"></a>Criar modelos no Azure Machine Learning
exercício de modelação de Olá toobegin, registo, na área de trabalho do tooyour Azure Machine Learning. Se ainda não tiver criado uma área de trabalho de aprendizagem, consulte o artigo [criar uma área de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).

1. tooget iniciado com o Azure Machine Learning, consulte [que é o Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Inicie sessão no demasiado[Azure Machine Learning Studio](https://studio.azureml.net).
3. página de Studio Home Olá fornece uma variedade de informações, vídeos, tutoriais, ligações toohello referência de módulos e outros recursos. Fore mais informações sobre o Azure Machine Learning, consulte Olá [Centro de documentação do Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

Uma experimentação de preparação típico é composta pelos seguintes Olá:

1. Criar um **+ novo** experimentação.
2. Obter dados de Olá tooAzure Machine Learning.
3. Pré-processar, transformar e manipular dados de Olá conforme necessário.
4. Gere funcionalidades conforme necessário.
5. Dividir os dados de Olá em conjuntos de dados de formação / / testes validação (ou tem conjuntos de dados separados para cada).
6. Selecione um ou mais algoritmos do machine learning consoante Olá toosolve de problema de aprendizagem. Por exemplo, classificação binária, classificação de várias classes, regressão.
7. Preparar um ou mais modelos utilizando o conjunto de dados de formação de Olá.
8. Conjunto de dados de validação Olá utilizando model(s) treinado Olá de pontuação.
9. Avalie Olá model(s) toocompute Olá relevantes métricas para Olá problema de aprendizagem.
10. Ajustar Olá model(s) e selecione Olá melhor toodeploy de modelo.

Neste exercício, vamos já explorou e foi desenvolvido dados Olá no SQL Server e decidir tooingest de tamanho de exemplo de Olá no Azure Machine Learning. toobuild um ou mais dos modelos de predição de Olá decidimos:

1. Obter dados de Olá tooAzure Machine Learning utilizando Olá [importar dados] [ import-data] módulo, disponível no Olá **dados de entrada e saída** secção. Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência do módulo.
   
    ![Importar dados de aprendizagem do Azure][17]
2. Selecione **SQL Database do Azure** como Olá **origem de dados** no Olá **propriedades** painel.
3. Introduza o nome DNS de base de dados de Olá no Olá **nome do servidor de base de dados** campo. Formato:`tcp:<your_virtual_machine_DNS_name>,1433`
4. Introduza Olá **nome de base de dados** no campo correspondente Olá.
5. Introduza Olá **nome de utilizador do SQL Server** no Olá * * nome do servidor utilizador aqccount e Olá palavra-passe no Olá **palavra-passe de conta de utilizador do**.
6. Verifique **aceita qualquer certificado de servidor** opção.
7. No Olá **consulta de base de dados** editar a área de texto, cole a consulta de Olá que extrai Olá necessário campos (incluindo quaisquer campos calculados como etiquetas Olá) da base de dados e pendente amostras de tamanho da amostra Olá dados toohello assim o desejar.

É um exemplo de uma experimentação de classificação binária ler os dados diretamente a partir da base de dados do SQL Server Olá na figura Olá abaixo. Podem ser construídas experimentações semelhantes para classificação de várias classes e problemas de regressão.

![Azure Machine Learning formação][10]

> [!IMPORTANT]
> No Olá modelação de extração de dados e fazendo a amostragem exemplos de consultas fornecidos nas secções anteriores, **todas as etiquetas para exercícios de modelação Olá três estão incluídas na consulta de Olá**. Um passo importante (obrigatório) em cada um dos Olá modelação exercícios é demasiado**excluir** Olá desnecessárias etiquetas para Olá outros dois problemas e quaisquer outros **fugas de destino**. Para por exemplo, quando utilizar a classificação do binária, utilize etiqueta Olá **tipped** e excluir os campos de Olá **sugestão\_classe**, **sugestão\_quantidade**, e **total\_quantidade**. Olá última são fugas de destino, desde que o implica sugestão Olá paga.
> 
> colunas desnecessárias tooexclude e/ou fugas de destino, pode utilizar Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo ou Olá [Editar metadados] [ edit-metadata]. Para obter mais informações, consulte [selecionar colunas no conjunto de dados] [ select-columns] e [Editar metadados] [ edit-metadata] páginas de referência.
> 
> 

## <a name="mldeploy"></a>Modelos de implementação no Azure Machine Learning
Quando o modelo estiver pronto, pode facilmente implementá-lo como um serviço web diretamente a partir da experimentação Olá. Para obter mais informações sobre a implementação de serviços web do Azure Machine Learning, consulte [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy um novo serviço web, tem de:

1. Crie uma experimentação de classificação.
2. Implemente o serviço web de Olá.

toocreate uma classificação de experimentação de um **concluído** experimentação de preparação, clique em **criar classificação experimentação** na barra de ação inferior Olá.

![A classificação do Azure][18]

O Azure Machine Learning tentará toocreate uma experimentação de classificação com base nos componentes de Olá do experimentação de preparação de Olá. Em particular, irá:

1. Guarde o modelo treinado Olá e remover módulos de formação do modelo de Olá.
2. Identificar uma lógica **porta de entrada** toorepresent Olá esperado esquema de dados de entrada.
3. Identificar uma lógica **porta de saída** esquema de saída do serviço do toorepresent Olá web esperado.

Quando é criado Olá experimentação de classificação, reveja-lo e ajustar conforme necessário. Um ajuste típico é conjunto de dados entrada tooreplace Olá e/ou a consulta com um que exclui os campos de etiqueta, como estes não estarão disponíveis quando o serviço de Olá é chamado. Também é que um boa prática tooreduce Olá o tamanho de Olá entrada tooa de consulta e/ou conjunto de dados poucos registos, apenas suficiente esquema da entrada Olá tooindicate. Para a porta de saída Olá, é comum tooexclude campos de entrada de todos os e incluir apenas Olá **etiquetas classificadas** e **probabilidades classificadas** no Olá saída utilizando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.

É um classificação experimentação de exemplo na figura Olá abaixo. Quando está preparado toodeploy, clique em Olá **publicar o serviço de WEB** botão na barra de ação inferior Olá.

![Publicar de aprendizagem do Azure][11]

toorecap, neste tutorial explicação passo a passo, criou um ambiente de ciência de dados do Azure, trabalhado com um conjunto de dados grande público todas as forma de Olá de toomodel de aquisição de dados de preparação e implementação de um serviço web Azure Machine Learning.

### <a name="license-information"></a>Informações de licença
Estas instruções de exemplo e o respetivo que acompanha scripts e IPython notebook(s) são partilhadas pela Microsoft em licença MIT de Olá. Verifique o ficheiro de LICENSE.txt Olá no diretório de Olá do código de exemplo de Olá no GitHub para obter mais detalhes.

### <a name="references"></a>Referências
• [Andrés Monroy NYC Taxi viagens página de transferência](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC Taxi viagem dados por Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [NYC Taxi e Limousine Commission investigação e estatísticas](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
