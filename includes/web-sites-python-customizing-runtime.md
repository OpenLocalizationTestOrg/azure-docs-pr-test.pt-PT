Azure irá determinar a versão de Olá do Python toouse para o ambiente virtual com Olá seguinte prioridade:

1. versão especificada no runtime.txt na pasta raiz de Olá
2. versão especificada pela definição Python na configuração da aplicação web Olá (Olá **definições** > **definições da aplicação** painel para a sua aplicação web no Olá Portal do Azure)
3. é Python-2.7 predefinido Olá se Olá acima são especificados

Valores válidos para o conteúdo de Olá do 

    \runtime.txt

são:

* python-2.7
* python-3.4

Se versão micro Olá (terceiro dígito) estiver especificada, será ignorada.

