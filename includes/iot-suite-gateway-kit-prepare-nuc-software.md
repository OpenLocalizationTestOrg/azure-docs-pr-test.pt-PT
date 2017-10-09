## <a name="build-iot-edge"></a>Criar IoT Edge

Este tutorial utiliza personalizado toocommunicate de módulos de limite de IoT com Olá solução pré-configurada de monitorização remota. Por conseguinte, terá de módulos de limite de IoT Olá toobuild a partir do código de origem personalizada. Olá seguintes secções descreve como tooinstall IoT Edge e compilação Olá módulo personalizado do limite de IoT.

### <a name="install-iot-edge"></a>Instalar o limite de IoT

Olá passos seguintes descrevem como tooinstall Olá pré-compilado software IoT Edge Olá Intel NUC:

1. Configure repositórios de pacote inteligente Olá necessário executando os seguintes comandos no Olá Intel NUC de Olá:

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    Introduza `y` quando comando Olá pede-lhe demasiado**incluir este canal?**.

1. Atualize Gestor de pacotes inteligente de Olá executando Olá os seguintes comandos:

    ```bash
    smart update
    ```

1. Instale o pacote de limite de IoT do Azure de Olá executando Olá os seguintes comandos:

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. Verifique a instalação de Olá ao exemplo de "Olá mundo" Olá em execução. Este exemplo escreve um ficheiro de log.txT toohello do Olá mundo mensagem a cada cinco segundos. Olá seguintes comandos executam Olá "Olá mundo" exemplo:

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    Ignorar todas **argumento inválido** mensagens quando deixa de exemplo de Olá.

    Utilize Olá comando tooview Olá do conteúdo do ficheiro de registo Olá os seguintes:

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a>Resolução de problemas

Se receber o erro de Olá "nenhum pacote fornece util-linux-dev", tente reiniciando Olá Intel NUC.
