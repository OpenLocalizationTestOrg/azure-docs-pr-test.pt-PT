O Azure determinará se a aplicação utiliza o Python **se ambas estas condições forem verdadeiras**:

* ficheiro Requirements.txt na pasta raiz de Olá
* qualquer ficheiro. PY na pasta raiz de Olá ou de um ficheiro Runtime.txt a especificar python

Quando for esse caso de Olá, irá utilizar um script de implementação específico do Python, que executa a sincronização padrão de Olá de ficheiros, bem como operações adicionais do Python, tais como:

* Gestão automática do ambiente virtual
* Instalação de pacotes listados no ficheiro requirements.txt com pip
* A criação de Olá config adequado com base no Olá selecionado versão Python.
* Recolha de ficheiros estáticos para aplicações Django

Pode controlar determinados aspetos dos passos de implementação predefinidos Olá sem ter de script de Olá toocustomize.

Se quiser tooskip todos os passos de implementação específico do Python, pode criar este ficheiro vazio:

    \.skipPythonDeployment

Para obter mais controlo sobre a implementação, pode substituir o script de implementação do Olá predefinido criando Olá os seguintes ficheiros:

    \.deployment
    \deploy.cmd

Pode utilizar Olá [interface de linha de comandos do Azure] [ Azure command-line interface] ficheiros de Olá toocreate.  Utilize este comando na pasta do projeto:

    azure site deploymentscript --python

Se estes ficheiros não existirem, o Azure cria um script de implementação temporário e executa-o.  É idêntico toohello aquele que criar com o comando de Olá acima.

[Azure command-line interface]: http://azure.microsoft.com/downloads/
