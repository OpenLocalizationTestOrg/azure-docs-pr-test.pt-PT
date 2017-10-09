>[!NOTE]
>Para obter recursos que não sejam fixos, pode pedir Olá quotas toobe gerado, abrindo um pedido de suporte. Efetue **não** criar contas de Media Services do Azure adicionais numa tentativa de limites superiores tooobtain.

| Recurso | Limite Predefinido | 
| --- | --- | 
| Contas dos Serviços de Multimédia do Azure (AMS) numa subscrição individual | 25 (fixo) |
| Unidades Reservadas de Multimédia (RUs) por conta do AMS |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| Trabalhos por conta do AMS | 50,000<sup>(2)</sup> |
| Tarefas em cadeia por trabalho | 30 (fixo) |
| Elementos por conta do AMS | 1 000 000|
| Elementos por tarefa | 50 |
| Elementos por trabalho | 100 |
| Localizadores exclusivos associados a um elemento ao mesmo tempo | 5<sup>(4)</sup> |
| Canais em direto por conta do AMS |5|
| Programas no estado de paragem por canal |50|
| Programas no estado parado por canal |3|
| Pontos finais de transmissão em fluxo no estado em execução por conta do AMS|2|
| Unidades de transmissão em fluxo por ponto final de transmissão em fluxo |10 |
| Contas de armazenamento | 1000<sup>(5)</sup> (fixo) |
| Políticas | 1,000,000<sup>(6)</sup> |
| Tamanho dos ficheiros| Em alguns cenários não há um limite no tamanho máximo do ficheiro de Olá suportado para processamento nos Media Services. <sup>7</sup> |
  
<sup>1</sup> As RUs S3 não estão disponíveis na Índia Ocidental. os limites de RU máximas Olá obterem repor se cliente Olá alterações Olá tipo (por exemplo, a partir de S2 tooS1). 

<sup>2</sup> Este número inclui trabalhos em fila, concluídos, ativos e cancelados. Não inclui trabalhos eliminados. Pode eliminar tarefas antigo Olá utilizando **IJob.Delete** ou Olá **eliminar** pedido de HTTP.

A partir de 1 de Abril de 2017, qualquer registo de tarefas na sua conta mais antiga do que 90 dias serão automaticamente eliminado, juntamente com os respetivos registos de tarefa associados, mesmo que o número total de Olá de registos é inferior a quota máxima de Olá. Se precisar de informações de tarefa/tooarchive Olá, pode utilizar o código de Olá descrito [aqui](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> quando efetuar um pedido de entidades de tarefa toolist, será devolvido um máximo de 1000 por pedido. Se precisar de controlar tookeep de submetido todas as tarefas, pode utilizar parte superior/skip conforme descrito em [opções de consulta OData sistema](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> Os localizadores não foram concebidos para gerir o controlo de acesso por utilizador. utilizadores de tooindividual de direitos de acesso diferentes toogive, utilizar soluções de gestão de direitos digitais (DRM). Para obter mais informações, veja [esta](../articles/media-services/media-services-content-protection-overview.md) secção.

<sup>5</sup> contas do storage Olá tem de ser de Olá mesma subscrição do Azure.

<sup>6</sup> Existe um limite de um milhão de políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy). 

>[!NOTE]
> Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões de acesso / etc. Para obter informações e um exemplo, consulte [esta](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) secção.

<sup>7</sup>se estiver a carregar conteúdo tooan Asset no suporte de dados do Azure serviços com tooprocess intenção Olá-o com um dos processadores de multimédia de Olá no nosso serviço (ou seja, codificadores como motores codificador de multimédia Standard e o fluxo de trabalho do suporte de dados codificador Premium ou o Analysis Services em seguida, como enfrentam Detector), deve ter conhecimento da restrição de Olá no tamanho máximo de Olá. 

A partir do dia 15 de Maio de 2017, tamanho máximo de Olá suportado para um blob único 195 TB - com largers de ficheiro que este limite, a tarefa irá falhar. Estamos a trabalhar um tooaddress corrija este limite. Além disso, restrição Olá no tamanho máximo do Olá de Olá Asset é a seguinte.

| Tipo de Unidade Reservada de Multimédia | Tamanho máximo de entrada (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|
