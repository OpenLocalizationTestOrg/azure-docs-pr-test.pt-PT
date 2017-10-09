Armazenamento é restrita por espaço em disco ou por um limite rígido Olá *número máximo* de índices ou documentos, o que ocorrer primeiro.

| Recurso | Gratuito | Básica | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contrato de Nível de Serviço (SLA) |N.º <sup>1</sup> |Sim |Sim |Sim |Sim |Sim |
| Armazenamento por partição |50 MB |2GB |25 GB |100 GB |200 GB |200 GB |
| Partições por serviço |N/D |1 |12 |12 |12 |3 <sup>2</sup> |
| Tamanho da partição |N/D |2GB |25 GB |100 GB |200 GB |200 GB |
| Réplicas |N/D |3 |12 |12 |12 |12 |
| Índices máximos |3 |5 |50 |200 |200 |1000 por partição ou 3000 por serviço |
| Indexadores máximos |3 |5 |50 |200 |200 |Sem suporte de indexador |
| Origens de dados máximas |3 |5 |50 |200 |200 |Sem suporte de indexador |
| Documentos máximos |10,000 |1 milhão |15 milhões por partição ou 180 milhões por serviço |60 milhões por partição ou 720 milhões por serviço |120 milhões por partição ou 1,4 biliões por serviço |1 milhão por índice ou 200 milhões por partição |
| Consultas estimadas por segundo (QPS) |N/D |~3 por réplica |~15 por réplica |~60 por réplica |~60 por réplica |>60 por réplica |

<sup>1</sup> funcionalidades de pré-visualização e o escalão gratuito não são fornecidos com os contratos de nível de serviço (SLAs). Para todos os escalões faturáveis, SLAs entram em vigor quando aprovisionar redundância suficiente para o seu serviço. Dois ou mais réplicas são necessárias para o SLA de consulta (leitura). Três ou mais réplicas são necessárias para consulta e indexação SLA (leitura / escrita). número de Olá de partições não é uma consideração de SLA. 

<sup>2</sup> S3 HD tem um limite rígido de 3 partições, que é inferior ao limite de partição Olá S3. limite de partição inferior Olá é imposta porque a contagem de índice de Olá para S3 HD é substancialmente superior. Dado que existem limites de serviço para ambos os recursos informáticos (processamento e armazenamento) e o conteúdo (índices e documentos), Olá conteúdo é atingido pela primeira vez.
