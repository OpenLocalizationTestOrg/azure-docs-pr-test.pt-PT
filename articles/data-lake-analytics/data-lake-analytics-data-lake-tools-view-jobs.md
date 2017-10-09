---
title: aaaUse Browser de tarefa e vista de tarefas para tarefas do Azure Data Lake Analytics | Microsoft Docs
description: 'Saiba como toouse Browser de tarefa e vista de tarefas para tarefas do Azure Data Lake Analytics. '
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bdf27b4d-6f58-4093-ab83-4fa3a99b5650
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: jgao
ms.openlocfilehash: c45e618426808349ca380b1bcfaefd4c947ce7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-job-browser-and-job-view-for-azure-data-lake-analytics-jobs"></a>Utilizar o Browser de tarefa e vista de tarefas para tarefas do Azure Data lake Analytics
Olá arquivos de serviço do Azure Data Lake Analytics submeter as tarefas num [arquivo de consultas](#query-store). Neste artigo, saiba como toouse Browser de tarefa e ver a tarefa no Azure Data Lake Tools para Olá toofind de Visual Studio histórico informações da tarefa. 

Por predefinição, o Olá serviço do Data Lake Analytics arquiva tarefas Olá durante 30 dias. período de expiração de Olá pode ser configurado Olá portal do Azure através da configuração de política de expiração de Olá personalizada. Não será capaz de tooaccess informações de tarefa de Olá após a expiração. 

## <a name="prerequisites"></a>Pré-requisitos
Consulte [ferramentas do Data Lake para pré-requisitos do Visual Studio](data-lake-analytics-data-lake-tools-get-started.md#prerequisites).

## <a name="open-hello-job-browser"></a>Abrir Olá Browser de tarefa
Acesso Olá Browser tarefa através de **Explorador de servidores > Azure > do Data Lake Analytics > tarefas** no Visual Studio.  Utilizar Olá tarefa Browser, pode aceder ao arquivo de consultas de Olá de uma conta de Data Lake Analytics. Tarefa Browser mostra o arquivo de consultas no Olá deixado, as informações da tarefa básico e vista de tarefa de apresentação correta Olá detalhadas as informações da tarefa.

## <a name="job-view"></a>Vista de tarefas
Vista de tarefas mostra Olá informações detalhadas de uma tarefa. tooopen uma tarefa, faça duplo clique uma tarefa em Olá tarefa Browser, ou abri-lo a partir do menu de Data Lake Olá, clicando em vista de tarefas. Deverá ver uma caixa de diálogo preenchida com Olá tarefa URL.

![Data Lake Tools Browser de tarefa do Visual Studio](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view.png)

Contém a vista de tarefas:

* Resumo da Tarefa
  
    Atualizar Olá ver tarefa toosee hello mais recentes informações de tarefas em execução.
  
  * Estado da tarefa (gráfico):
    
      Estado da tarefa destaca as fases de tarefa Olá:
    
      ![Estado de fases de tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-phases.png)
    
    * A preparar: Carregue o script toohello na nuvem, compilar e otimizar o script de Olá utilizando o serviço de compilação de Olá.
    * Colocados em fila: As tarefas são whey em fila estão a aguardar recursos suficientes ou as tarefas de Olá excedem o máximo tarefas simultâneas Olá por limitação de conta. definição de prioridade de Olá determina sequência Olá das tarefas em fila - Olá Olá número, maior prioridade de Olá Olá.
    * Em execução: a tarefa de Olá, na verdade, está em execução na sua conta do Data Lake Analytics.
    * A finalizar: tarefa Olá está a ser concluída (por exemplo, a finalizar o ficheiro de Olá).
      
      tarefa de Olá pode falhar em cada fase. Por exemplo, erros de compilação na fase de preparar Olá, erros de tempo limite na fase de em fila Olá e erros de execução na fase de execução de Olá, etc.
  * Informações básicas
    
      mostram informações de tarefa básico Olá na parte inferior do Olá do painel de resumo da tarefa de Olá.
    
      ![Estado de fases de tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-info.png)
    
    * Resultado da tarefa: Foi concluída com êxito ou falha. tarefa de Olá poderão falhar em cada fase.
    * Duração total: Padrão de fundo tempo de relógio (duração) entre a submeter o tempo e a hora de fim.
    * O tempo total de computação: soma Olá de cada tempo de execução de vértice, pode considerá-lo como Olá tempo essa tarefa Olá for executada no vértice apenas um. Consulte tooTotal vértices toofind mais informações sobre o vértice.
    * Hora de envio/início/fim: tempo Olá quando Olá serviço do Data Lake Analytics recebe Olá de toorun de submissão/iniciar tarefa tarefa/termina tarefa Olá com êxito ou não.
    * Em fila/compilação/execução: Tempo de relógio de lateral gasto durante a fase de preparar/em fila/em execução Olá.
    * : Olá Data Lake Analytics conta utilizada para executar a tarefa de Olá.
    * Autor: Olá utilizador submetido a tarefa de Olá, pode ser a conta de uma pessoa real ou uma conta de sistema.
    * Prioridade: prioridade de Olá tarefa Olá. Olá Olá número, maior prioridade de Olá Olá. Afeta apenas a sequência de Olá das tarefas de Olá na fila de Olá. Definir uma prioridade mais alta não alta impedem mais tarefas em execução.
    * Paralelismo: Olá pedida número máximo de simultâneas do Azure Data Lake Analytics unidades (ADLAUs), aka vértices. Atualmente, é de um vértice tooone igual a VM com dois núcleos virtual e seis GB de RAM, apesar de Isto pode ser atualizado no futuro do Data Lake Analytics atualizações.
    * Bytes restantes: Total de Bytes que necessitam de toobe processada até Olá tarefa é concluída.
    * Bytes escritos/leitura: Bytes que foram leitura/escrita desde a tarefa de Olá começou a ser executada.
    * Total de vértices: tarefa Olá é dividida cópias de segurança em trabalho de várias partes, cada trabalho de peça é chamado um vértice. Este valor descreve consiste em quantos tarefa de Olá peças de trabalho. Pode considerar um vértice como uma unidade de processo básico, também conhecido como Azure Data Lake Analytics unidade (ADLAU), e vértices podem ser executadas em paralelismo. 
    * Concluir/em execução/com falhas: Olá contagem de vértices concluída/em execução/falhou. Vértices podem falhar devido a falhas de código e de sistema de utilizador do tooboth, mas as repetições de sistema Olá falhou vértices automaticamente algumas vezes. Se vértice Olá ainda é falha depois de repetir, tarefa todo Olá irá falhar.
* Gráfico da tarefa
  
    Um script U-SQL representa lógica Olá de transformar dados de entrada toooutput dados. script de Olá é compilado e otimizada, o plano de execução físico tooa na fase de preparar Olá. Gráfico da tarefa é o plano de execução físico tooshow Olá.  Olá seguinte diagrama ilustra o processo de Olá:
  
    ![Estado de fases de tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-logical-to-physical-plan.png)
  
    Uma tarefa é dividida cópias de segurança em trabalho de várias partes. Cada trabalho de peça é chamado um vértice. vértices Olá são agrupados como Super vértice (aka fase) e visualizados como gráfico da tarefa. Olá fase verde placards no gráfico da tarefa Olá mostram fases Olá.
  
    Cada vértice numa fase está a fazer Olá mesmo tipos de trabalhar com diferentes partes de Olá mesmos dados. Por exemplo, se tiver um ficheiro com um de TB de dados, e não existirem centenas de vértices ao ler a partir dos mesmos, cada um deles está a ler um segmento. Esses vértices são agrupadas numa Olá mesmo fase e fazer mesmo funcionam em diferentes partes do mesmo ficheiro de entrada.
  
  * <a name="state-information"></a>Informações de fase
    
      Numa fase específica, são apresentados algumas números placard Olá.
    
      ![Fase de gráfico da tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage.png)
    
    * SV1 Extrair: nome de Olá uma fase, designado por um número e Olá operação um método.
    * 84 vértices: Olá contagem total de vértices nesta fase. a figura Olá indica quantos trabalho de peças está dividido nesta fase.
    * s/vértice 12.90: hello tempo de execução de vértice médio para esta fase. Desta figura é calculada pela soma (cada tempo de execução de vértice) / (contagem de vértice total). O que significa se foi possível atribuir todos os vértices Olá a executar a paralelismo, a fase de todo Olá estiverem concluída em 12.90 s. Isto também significa que se todos os Olá trabalho nesta fase é feita serialmente, custo Olá seria #vertices * Méd do tempo.
    * 850,895 linhas escritas: Total de contagem de linhas escrita nesta fase.
    * R/w quantidade de dados de leitura/Written nesta fase em bytes.
    * Cores: Cores são utilizadas no estado do Olá fase tooindicate vértice diferentes.
      
      * Verde indica vértice Olá é concluída com êxito.
      * Cor de laranja indica vértice Olá for repetida. vértice Olá repetida falhou, mas é automaticamente repetida e com êxito pelo sistema Olá e Olá geral fase é concluída com êxito. Se vértice Olá repetida, mas ainda não foi possível, cor Olá ativa a vermelho e Olá tarefa toda falhou.
      * Vermelho indica falha, que significa que um determinado vértice tinha foi repetida algumas vezes pelo sistema Olá, mas ainda não foi possível. Este cenário faz com que Olá tarefa todo toofail.
      * Azul significa que um determinado vértice está em execução.
      * Em branco indica Olá vértice está à espera. vértice Olá poderá toobe espera agendada depois de um ADLAU fica disponível, ou pode ser aguardar a intervenção, desde que os respetivos dados de entrada podem não estar preparados.
      
      Pode encontrar mais detalhes para a fase de Olá por posicionado o cursor do rato por um Estado:
      
      ![Detalhes de fase de gráfico da tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-stage-details.png)
  * Vértices: Descreve os detalhes de vértices Olá, por exemplo, quantas vértices no total, vértices quantas foram concluídas, são que falhou ou continua em execução/em espera, etc.
  * Dados lidos em vários locais/intra pod: ficheiros e os dados são armazenados em várias pods no sistema de ficheiros distribuído. valor de Olá aqui descreve a quantidade de dados tem sido lida Olá mesmo pod ou cruzada pod.
  * Total de tempo de computação: soma Olá de cada tempo de execução de vértice na fase de Olá, pode considerá-lo como o tempo de Olá demoraria se tudo funcionar na fase de Olá for executado no vértice apenas um.
  * Linhas de leitura/escrita e de dados: indica quanto dados linhas tem sido leitura/escrita ou necessário toobe ler.
  * Falhas de leitura de vértice: descreve vértices quantos são falhou ao dados de leitura.
  * Elimina o vértice duplicado: se um vértice executa demasiado lenta, sistema Olá pode agendar vértices vários toorun Olá trabalho do mesmo fragmento. Vértices reductant serão eliminadas depois de um dos vértices Olá concluída com êxito. Vértice duplicado elimina registos Olá diversas vértices são eliminadas como duplications na fase de Olá.
  * Revocations vértice: vértice Olá foi concluída com êxito, mas obter novamente mais tarde devido a razões toosome. Por exemplo, se a jusante vértice perder dados de entrada intermédios, irá perguntar Olá vértice montante toorerun.
  * Execuções de agenda de vértice: Olá total de tempo que vértices Olá tem sido agendadas.
  * Dados de média/mínimo/máximo vértice lidos: Olá mínimo/médio/máximo de cada vértice ler os dados.
  * Duração: Olá lateral relógio tempo que uma fase demora, terá de tooload perfil toosee este valor.
  * Reprodução de Tarefa
    
      O Data Lake Analytics executa tarefas e arquivos Olá vértices com informações de tarefas Olá, por exemplo, quando são iniciados vértices Olá, parar, falha e como são repetidas, etc. Todas as informações de Olá é automaticamente registado no arquivo de consultas Olá e armazenadas no seu perfil de tarefa. Pode transferir Olá perfil tarefa através de "Carregar perfil" na vista de tarefa e pode ver Olá reprodução de tarefa depois de transferir Olá perfil de tarefa.
    
      Reprodução de tarefa é uma visualização de epitome do que aconteceu num cluster de Olá. Ajuda a ver o progresso de execução da tarefa e detetar visualmente anomalias de desempenho e congestionamentos de muito curto período de tempo (menor que, normalmente, 30s).
  * Apresentação de mapa térmico de tarefa 
    
      Mapa térmico de tarefa pode ser selecionado através da lista pendente de apresentação de Olá no gráfico da tarefa. 
    
      ![Apresentação do mapa de área dinâmica para dados do gráfico de tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-display.png)
    
      Mostra Olá e/s, hora e débito térmico de uma tarefa, através do qual pode encontrar onde tarefa Olá despende a maior parte do tempo de Olá ou se a sua tarefa é uma tarefa de limites de e/s e assim sucessivamente.
    
      ![Exemplo do mapa de área dinâmica para dados do gráfico de tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-graph-heat-map-example.png)
    
    * Progresso: Olá progresso de execução da tarefa, consulte as informações no [testar informações](#stage-information).
    * Dados de leitura/escrita: mapa térmico de Olá de dados totais de leitura/escrita em cada fase.
    * Tempo de computação: mapa térmico de Olá de SUM (cada tempo de execução de vértice), pode considerar este como período de tempo que demoraria se todo o trabalho na fase de Olá for executado com apenas 1 vértice.
    * Tempo de execução média por nó: mapa térmico de Olá de SUM (cada tempo de execução de vértice) / (vértice número). O que significa se foi possível atribuir todos os vértices Olá a executar a paralelismo, fase todo Olá será efetuada neste período de tempo.
    * Débito de entrada/saída: mapa térmico de Olá de débito de entrada/saída de cada fase, pode confirmar se a tarefa é uma tarefa está vinculada e/s através deste.
* Operações de metadados
  
    Pode efetuar algumas operações de metadados no script U-SQL, tais como criar uma base de dados, remova uma tabela, etc. Estas operações são apresentadas na operação de metadados após a compilação. Pode encontrar asserções, criar entidades, largar entidades aqui.
  
    ![Operações de metadados de vista de tarefas de análise do Data Lake do Azure](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-metadata-operations.png)
* Histórico de estado
  
    Olá histórico de estado também é visualizado no resumo da tarefa, mas pode obter mais detalhes aqui. Pode encontrar Olá detalhada informações tais como quando a tarefa de Olá está preparada, colocados em fila, começou a ser executada, terminou. Também pode encontrar o número de vezes que foi compilada tarefa Olá (Olá CcsAttempts: 1), quando é, na verdade, o cluster de toohello emitidos de tarefa de Olá (Olá detalhe: tarefa toocluster de emissão), etc.
  
    ![Histórico de estado de vista de tarefas de análise do Data Lake do Azure](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-state-history.png)
* Diagnóstico
  
    ferramenta de Olá diagnoses automaticamente a execução da tarefa. Irá receber alertas quando existirem alguns erros ou problemas de desempenho nas suas tarefas. Tenha em atenção que tem de toodownload perfil tooget informações completas aqui. 
  
    ![Diagnóstico de vista de tarefas de análise do Data Lake do Azure](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-view-diagnostics.png)
  
  * Avisos: Um alerta aparece aqui com aviso do compilador. Pode clicar em "x comprovativos" ligação toohave mais detalhes assim que o alerta de Olá aparece.
  * Vértice executar demasiado longo: se qualquer vértice fica sem tempo (diga 5 horas), irão ser encontrados problemas aqui.
  * Utilização de recursos: Se já tiver alocado paralelismo mais ou insuficiente que necessita, irão ser encontrados problemas aqui. Também pode clique toosee de utilização de recursos mais detalhes e efetuar investiguem cenários toofind uma melhor alocação de recursos (para obter mais detalhes, consulte o artigo neste guia).
  * Verificação de memória: se qualquer vértice utiliza mais de 5 GB de memória, irão ser encontrados problemas aqui. Execução da tarefa pode obter terminada pelo sistema, se utiliza mais memória a limitação do sistema.

## <a name="job-detail"></a>Detalhes da tarefa
Detalhes da tarefa mostra Olá informações detalhadas do trabalho Olá, incluindo Script, recursos e vista de execução de vértice.

![Detalhes da tarefa do Azure Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-view-jobs/data-lake-tools-job-details.png)

* Script
  
    Olá script U-SQL da tarefa de Olá é armazenado no arquivo de consultas Olá. Pode ver o script de U-SQL original Olá e submeter novamente se for necessário.
* Recursos
  
    Pode encontrar saídas de compilação de tarefa de Olá armazenadas no arquivo de consultas Olá através dos recursos. Por exemplo, pode encontrar "algebra.xml", que é utilizado tooshow Olá gráfico da tarefa, as assemblagens Olá registou, etc. aqui.
* Vista de execução de vértice
  
    Mostra vértices detalhes de execução. Olá tarefa perfil arquiva cada registo de execução de vértice, tais como os dados totais leitura/escrita, tempo de execução, estado, etc. Através desta vista, pode obter mais detalhes sobre a forma como foi executada uma tarefa. Para obter mais informações, consulte [Olá utilize vista de execução de vértice nas ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).

## <a name="next-steps"></a>Passos Seguintes
* informações de diagnóstico toolog, consulte [aceder a registos de diagnóstico para o Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)
* toosee uma consulta mais complexa, consulte [analisar registos de site utilizando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* Vista de execução de vértice toouse, consulte [Olá utilize vista de execução de vértice nas ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md)

