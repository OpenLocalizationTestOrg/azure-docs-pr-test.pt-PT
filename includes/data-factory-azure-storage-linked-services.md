### <a name="azure-storage-linked-service"></a>Serviço Ligado do Storage do Azure
Olá **serviço ligado do Storage do Azure** permite-lhe toolink uma fábrica de dados do Azure de tooan de conta de armazenamento do Azure utilizando Olá **chave da conta**, que fornece a fábrica de dados de Olá com toohello de acesso global do Azure Armazenamento. Olá, a tabela seguinte fornece uma descrição para JSON elementos específico tooAzure serviço ligado de armazenamento.

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| tipo |a propriedade de tipo Olá tem de ser definida: **AzureStorage** |Sim |
| connectionString |Especifique informações necessárias tooconnect tooAzure armazenamento para a propriedade connectionString de Olá. |Sim |

Consulte Olá seguinte artigo para a chave de conta de Olá de tooview/copiar de passos para um Storage do Azure: [ver, copiar e armazenamento voltar a gerar chaves de acesso](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Exemplo:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Serviço ligado do Storage do Azure Sas
Uma assinatura de acesso partilhado (SAS) fornece acesso delegado tooresources na sua conta de armazenamento. Permite toogrant um cliente limitada tooobjects de permissões na sua conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter tooshare as chaves de acesso da conta. Olá SAS é um URI que abrange nos respetivos parâmetros de consulta todos os Olá as informações necessárias para o recurso de armazenamento de tooa acesso autenticado. recursos de armazenamento tooaccess com Olá SAS, o cliente de Olá apenas precisa toopass no Olá SAS toohello adequado construtor ou método. Para obter informações detalhadas sobre SAS, consulte [assinaturas de acesso partilhado: Olá compreender o modelo SAS](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure Data Factory agora só suporta **serviço SAS** , mas não a conta SAS. Consulte [tipos de assinaturas de acesso partilhado](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) para obter detalhes sobre estes dois tipos e como tooconstruct. Tenha em atenção Olá URL SAS generable a partir do portal do Azure ou o Explorador de armazenamento é um SAS de conta, que não é suportado.
> 

Olá SAS de armazenamento do Azure ligado serviço permite-lhe toolink uma fábrica de dados do Azure de tooan de conta de armazenamento do Azure, utilizando uma assinatura de acesso partilhado (SAS). Fornece fábrica de dados de Olá com acesso restrito/vínculo de tempo específico/tooall recursos (/ contentor do blob) no armazenamento de Olá. Olá, a tabela seguinte fornece uma descrição para JSON elementos específico tooAzure serviço SAS de armazenamento ligado. 

| Propriedade | Descrição | Necessário |
|:--- |:--- |:--- |
| tipo |a propriedade de tipo Olá tem de ser definida: **AzureStorageSas** |Sim |
| sasUri |Especifique os recursos de armazenamento do Azure do URI de assinatura de acesso partilhado toohello como BLOBs, contentor ou tabela.  |Sim |

**Exemplo:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Ao criar um **URI de SAS**, considerar o seguinte Olá:  

* Conjunto adequada de leitura/escrita **permissões** em objetos com base na forma Olá ligado serviço (leitura, escrita, leitura/escrita) é utilizado na fábrica de dados.
* Definir **hora de expiração** adequadamente. Certifique-se de que os objetos de armazenamento do Olá acesso tooAzure não expirar dentro do período ativo de Olá de pipeline de Olá.
* URI deve estar criado no contentor Olá direito/blob ou nível de tabela com base no Olá precisa. Tooan um Uri de SAS BLOBs do Azure permite tooaccess de serviço do Data Factory Olá esse blob específico. Um contentor de Blobs do Azure do Uri de SAS tooan permite Olá tooiterate de serviço Data Factory através de blobs no contentor. Se precisa de acesso de tooprovide mais/menos objetos mais tarde, ou atualização Olá SAS URI, lembre-se de serviço de Olá ligado tooupdate com Olá novo URI.   

