
### <a name="cacheskuname"></a>cacheSKUName
escalão de preço de Olá do Olá da Cache de Redis do Azure de novo.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

modelo de Olá define valores Olá que são permitidos para este parâmetro (básico ou Standard) e atribui um valor predefinido (básico), se for especificado nenhum valor. Basic fornece um único nó com vários tamanhos disponíveis segurança too53 GB.
Norma fornece dois nós primário/réplica com vários tamanhos disponíveis too53 GB e 99,9% SLA de cópias de segurança.

### <a name="cacheskufamily"></a>cacheSKUFamily
família de Olá para Olá sku.

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
tamanho de Olá de nova instância de Cache de Redis do Azure Olá. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


modelo de Olá define valores Olá que são permitidos para este parâmetro (0, 1, 2, 3, 4, 5 ou 6) e atribui um valor predefinido (1) se for especificado nenhum valor. Os números correspondem toofollowing tamanhos de cache: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB

