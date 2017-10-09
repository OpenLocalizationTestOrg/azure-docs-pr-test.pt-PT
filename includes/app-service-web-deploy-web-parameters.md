Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado. modelo de Olá inclui uma secção denominada parâmetros que contém todos os valores de parâmetro de Olá.
Deve definir um parâmetro para esses valores que irão variar com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar. Não defina parâmetros para valores que sempre permanecerão Olá mesmo. Cada valor do parâmetro é utilizado em Olá toodefine Olá recursos do modelo que são implementados. 

Quando definir parâmetros, utilize Olá **allowedValues** toospecify campo que os valores de um utilizador pode fornecer durante a implementação. Olá utilize **defaultValue** campo tooassign toohello parâmetro de valor, se não for fornecido nenhum valor durante a implementação.

Iremos descrevem cada um dos parâmetros do modelo de Olá.

### <a name="sitename"></a>SiteName
nome de Olá da aplicação web de Olá pretende toocreate.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
nome de Olá de Olá do serviço de aplicações planear toouse para alojar a aplicação web de Olá.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>SKU
Olá escalão de preço para Olá plano de alojamento.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

modelo de Olá define valores Olá que são permitidos para este parâmetro e atribui um valor predefinido (S1), se for especificado nenhum valor.

### <a name="workersize"></a>workerSize
Olá tamanho da instância Olá (pequeno, médio ou grande) de plano de alojamento.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

modelo de Olá define valores Olá que são permitidos para este parâmetro (0, 1 ou 2) e atribui um valor predefinido (0) se for especificado nenhum valor. valores de Olá correspondem toosmall, média e grande.

