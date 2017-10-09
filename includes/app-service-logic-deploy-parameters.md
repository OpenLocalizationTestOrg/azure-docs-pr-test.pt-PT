Com o Azure Resource Manager, define os parâmetros para os valores que pretende toospecify quando o modelo de Olá é implementado. modelo de Olá inclui uma secção denominada parâmetros que contém todos os valores de parâmetro de Olá.
Deve definir um parâmetro para esses valores que irão variar com base no projeto Olá que estiver a implementar ou com base no ambiente de Olá que estiver a implementar. Não defina parâmetros para valores que sempre permanecerão Olá mesmo. Cada valor do parâmetro é utilizado em Olá toodefine modelo de Olá recursos que são implementar. 

Quando definir parâmetros, utilize Olá **allowedValues** toospecify campo que os valores de um utilizador pode fornecer durante a implementação. Olá utilize **defaultValue** campo tooassign toohello parâmetro de valor, se não for fornecido nenhum valor durante a implementação.

Iremos descrevem cada um dos parâmetros do modelo de Olá.

### <a name="logicappname"></a>logicAppName
nome de Olá do toocreate de aplicação de lógica de Olá.

    "logicAppName": {
        "type": "string"
    }