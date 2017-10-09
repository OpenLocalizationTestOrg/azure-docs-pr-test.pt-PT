## <a name="install-hello-prerequisites"></a>Instalar pré-requisitos de Olá

1. Instalar [Visual Studio 2015 ou 2017](https://www.visualstudio.com). Pode utilizar Olá livre edição Community caso cumpra os requisitos de licenciamento Olá. Ser tooinclude se Visual C++ e Gestor de pacotes NuGet.

1. Instalar [git](http://www.git-scm.com) e certifique-se de que pode executar git.exe Olá linha de comandos.

1. Instalar [CMake](https://cmake.org/download/) e certifique-se de que pode executar cmake.exe Olá linha de comandos. CMake versão 3.7.2 ou posterior é recomendada. Olá **. msi** installer é a opção mais fácil de Olá no Windows. Adicionar o CMake toohello caminho para, pelo menos, Olá utilizador atual quando o instalador Olá pede-lhe.

1. Instalar [Python 2.7](https://www.python.org/downloads/release/python-27). Certifique-se de adicionar o Python tooyour `PATH` variável de ambiente no **painel de controlo -> sistema -> Avançadas definições do sistema -> variáveis de ambiente**.

1. Numa linha de comandos, execute Olá os seguintes comandos tooclone Olá Azure IoT Edge GitHub repositório tooyour computador local:

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a>Como toobuild Olá exemplo

Agora pode compilar Olá IoT Edge e exemplos de tempo de execução no seu computador local:

1. Abra um **linha de comandos do programador para VS 2015** ou **linha de comandos do programador para VS 2017** linha de comandos.

1. Navegue toohello pasta de raiz na sua cópia local do Olá **iot edge** repositório.

1. Execute o script de compilação da seguinte forma:

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

Este script cria um ficheiro de solução do Visual Studio e baseia-se a solução de Olá. Pode encontrar solução do Visual Studio Olá Olá **criar** pasta na sua cópia local do Olá **iot edge** repositório. Se pretender toobuild e executar testes de unidade de Olá, adicione Olá `--run-unittests` parâmetro. Se pretender toobuild e executar testes de tooend Olá fim, adicione Olá `--run-e2e-tests`.

> [!NOTE]
> Sempre que executar Olá **build.cmd** script, este elimina e, em seguida, recria Olá **criar** pasta na pasta raiz de Olá da sua cópia local Olá **iot edge** repositório.
