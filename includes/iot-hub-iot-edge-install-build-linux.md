## <a name="install-hello-prerequisites"></a>Instalar pré-requisitos de Olá

Olá passos deste tutorial partem do princípio de que está a executar Ubuntu Linux.

Abra uma shell e execute Olá os seguintes pacotes de comandos tooinstall Olá pré-requisitos:

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

Na shell de Olá, execute Olá os seguintes comandos tooclone Olá Azure IoT Edge GitHub repositório tooyour computador local:

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a>Como toobuild Olá exemplo

Agora pode compilar Olá IoT Edge e exemplos de tempo de execução no seu computador local:

1. Abra uma shell.

1. Navegue toohello pasta de raiz na sua cópia local do Olá **iot edge** repositório.

1. Execute o script de compilação da seguinte forma:

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

Este script utiliza o **cmake** toocreate utilitário uma pasta denominada **criar** na pasta raiz de Olá da sua cópia local a **iot edge** repositório e gerar um makefile. script de Olá, em seguida, cria solução Olá, ignorar a unidade de testes e testes de tooend de fim. Se pretender toobuild e executar testes de unidade de Olá, adicione Olá `--run-unittests` parâmetro. Se pretender toobuild e executar testes de tooend Olá fim, adicione Olá `--run-e2e-tests`.

> [!NOTE]
> Sempre que executar Olá **build.sh** script, este elimina e, em seguida, recria Olá **criar** pasta na pasta raiz de Olá da sua cópia local Olá **iot edge** repositório.
