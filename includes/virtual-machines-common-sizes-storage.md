
Olá Ls série está otimizado para cargas de trabalho que necessitam de armazenamento temporário de latência baixa, como bases de dados NoSQL, incluindo Cassandra, MongoDB, Cloudera, Redis. Olá Ls série oferece segurança vCPUs too32, utilizando Olá [processador Intel Xeon de®® E5 v3 família](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). obtém Olá Ls série Olá mesmo desempenho de CPU como Olá GS/G-série e inclui GiB 8 de memória por vCPU.  

## <a name="ls-series"></a>Série Ls

ACU: 180-240
 
| Tamanho          | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Discos de dados máximos | Débito máximo do armazenamento temporário e em cache: IOPS/MBps (tamanho da cache em GiB) | Débito máximo do disco não colocado em cache: IOPS/MBps | NICs. Máx. / Desempenho de rede esperado (Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s  | 4    | 32   | 678   | 8              | ND / ND (0)          | 5,000 / 125                               | 2 / 4000       | 
| Standard_L8s  | 8    | 64   | 1,388 | 16             | ND / ND (0)          | 10,000 / 250                              | 4 / 8000  | 
| Standard_L16s | 16   | 128  | 2,807 | 32             | ND / ND (0)          | 20,000 / 500                              | 8 / 6000 - 16000 &#8224; | 
| Standard_L32s* | 32 | 256  | 5,630 | 64             | ND / ND (0)          | 40,000 / 1,000                            | 8 / 20000 | 
 

débito de disco máximo Olá possível com as VMs de série Ls poderá ser limitado pelo número de Olá, tamanho e striping de quaisquer discos ligados. Para obter mais detalhes, veja [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md). 

* Instância é toohardware isolado tooa dedicado único cliente.

