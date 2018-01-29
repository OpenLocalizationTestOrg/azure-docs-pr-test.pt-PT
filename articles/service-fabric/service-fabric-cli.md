---
title: "Introdução à CLI do Azure Service Fabric"
description: "Saiba como utilizar a CLI do Azure Service Fabric. Saiba como ligar a um cluster e como gerir aplicações."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 10/20/2017
ms.author: edwardsa
ms.openlocfilehash: d24c7618c5d53cfe2871d596bfc0fe2cadd5940a
ms.sourcegitcommit: cf4c0ad6a628dfcbf5b841896ab3c78b97d4eafd
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/21/2017
---
# <a name="azure-service-fabric-cli"></a>CLI do Azure Service Fabric

A interface de linha de comandos (CLI) do Azure Service Fabric é um utilitário de linha de comandos para interagir e gerir entidades do Service Fabric. A CLI do Service Fabric pode ser utilizada com clusters do Windows ou do Linux. A CLI do Service Fabric é executada em qualquer plataforma onde o Python seja suportado.

[!INCLUDE [links to azure cli and service fabric cli](../../includes/service-fabric-sfctl.md)]

## <a name="prerequisites"></a>Pré-requisitos

Antes da instalação, certifique-se de que o seu ambiente tem o Python e o pip instalados. Para obter mais informações, veja a [documentação de início rápido do pip](https://pip.pypa.io/en/latest/quickstart/)e a [documentação de instalação do Python](https://wiki.python.org/moin/BeginnersGuide/Download) oficial.

A CLI suporta as versões 2.7, 3.5 e 3.6 do Python. O Python 3.6 é a versão recomendada, uma vez que o Python 2.7 atingirá brevemente o fim do suporte.

### <a name="service-fabric-target-runtime"></a>Runtime de destino do Service Fabric

A CLI do Service Fabric destina-se a suportar a versão de runtime mais recente do Service Fabric SDK. Utilize a tabela seguinte para determinar qual a versão da CLI a instalar:

| Versão da CLI   | Versão de runtime suportada |
|---------------|---------------------------|
| Mais recente (~=3)  | Mais recente (~=6.0)            |
| 1.1.0         | 5.6, 5.7                  |

Opcionalmente, pode especificar uma versão de destino da CLI a instalar ao colocar no comando `pip install` o sufixo `==<version>`. Por exemplo, para a versão 1.1.0, a sintaxe seria:

```
pip install -I sfctl==1.1.0
```

Substitua o comando `pip install` seguinte pelo comando mencionado anteriormente, quando necessário.

Para obter mais informações sobre versões da CLI do Service Fabric, veja a [Documentação do GitHub](https://github.com/Azure/service-fabric-cli/releases).

## <a name="install-pip-python-and-the-service-fabric-cli"></a>Instalar o pip, o Python e a CLI do Service Fabric

Existem muitas formas de instalar o pip e o Python na sua plataforma. Seguem-se alguns passos para configurar rapidamente os principais sistemas operativos com o Python 3 e o pip.

### <a name="windows"></a>Windows

Para Windows 10, Windows Server 2016 e Windows Server 2012 R2, utilize as instruções de instalação oficiais padrão. O instalador do Python também instala o pip por predefinição.

1. Aceda à [página de transferências do Python](https://www.python.org/downloads/) oficial e transfira a versão mais recente do Python 3.6

2. Inicie o instalador.

3. Na parte inferior da linha de comandos, selecione **Adicionar Python 3.6 a PATH**.

4. Selecione **Instalar Agora** e conclua a instalação.

Agora, pode abrir uma janela de comandos nova e obter a versão, quer do Python, quer do pip.

```bat
python --version
pip --version
```

Em seguida, execute o comando seguinte para instalar a CLI do Service Fabric:

```bat
pip install sfctl
sfctl -h
```

### <a name="ubuntu-and-windows-subsystem-for-linux"></a>Ubuntu e subsistema Windows para Linux

Para instalar a CLI do Service Fabric, execute os seguintes comandos:

```bash
sudo apt-get install python3
sudo apt-get install python3-pip
pip3 install sfctl
```

Em seguida, pode testar a instalação com:

```bash
sfctl -h
```

Se receber um erro de comando não encontrado, como:

`sfctl: command not found`

Certifique-se de que `~/.local/bin` está acessível a partir de `$PATH`:

```bash
export PATH=$PATH:~/.local/bin
echo "export PATH=$PATH:~/.local/bin" >> .bashrc
```

Se a instalação no subsistema Windows para Linux falhar com permissões de pasta incorretas, pode ser necessário tentar novamente com permissões elevadas:

```bash
sudo pip3 install sfctl
```

<a name = "cli-mac"></a>
### <a name="macos"></a>MacOS

Para MacOS, recomendamos utilizar o [Gestor de pacotes HomeBrew](https://brew.sh). Se o HomeBrew ainda não estiver instalado, execute o comando seguinte para o instalar:

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Em seguida, no terminal, instale o Python 3.6, o pip e a CLI do Service Fabric através dos comandos seguintes:

```bash
brew install python3
pip3 install sfctl
sfctl -h
```

## <a name="cli-syntax"></a>Sintaxe da CLI

Aos comandos é sempre adicionado o prefixo `sfctl`. Para obter informações gerais sobre todos os comandos que pode utilizar, utilize `sfctl -h`. Para obter ajuda com comandos individuais, utilize `sfctl <command> -h`.

Os comandos seguem uma estrutura repetível, com o destino do comando antes do verbo ou da ação.

```azurecli
sfctl <object> <action>
```

Neste exemplo, `<object>` é o destino de `<action>`.

## <a name="select-a-cluster"></a>Selecionar um cluster

Antes de executar qualquer operação, tem de selecionar um cluster ao qual se deve ligar. Por exemplo, para selecionar e ligar ao cluster com o nome `testcluster.com`, execute o comando seguinte:

> [!WARNING]
> Não utilize clusters do Service Fabric não seguros em ambientes de produção.

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

O ponto final do cluster tem de ter o prefixo `http` ou `https`. Tem de incluir a porta para o gateway HTTP. A porta e o endereço são os mesmos que o URL do Service Fabric Explorer.

Para os clusters que estão protegidos por um certificado, pode especificar um certificado PEM codificado. O certificado pode ser especificado como um ficheiro individual ou como um certificado e par de chaves. Se for um certificado autoassinado que não esteja assinado por uma AC, pode transmitir a opção `--no-verify` para ignorar a verificação de AC.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Para obter mais informações, veja [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md) (Ligar a um cluster do Azure Service Fabric seguro).

## <a name="basic-operations"></a>Operações básicas

As informações de ligação do cluster estão presentes em diferentes sessões da CLI do Service Fabric. Depois de selecionar um cluster do Service Fabric, pode executar qualquer comando do Service Fabric no mesmo.

Por exemplo, para obter o estado de funcionamento do cluster do Service Fabric, utilize o comando seguinte:

```azurecli
sfctl cluster health
```

O comando resulta na seguinte saída:

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a>Sugestões e resolução de problemas

Seguem-se algumas sugestões e dicas para resolver problemas comuns.

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a>Converter um certificado no formato PFX em PEM

A CLI do Service Fabric suporta ficheiros de certificados de cliente como PEM (extensão .pem). Se utilizar ficheiros PFX do Windows, tem de converter esses certificados no formato PEM. Para converter um ficheiro PFX para ficheiro PEM, utilize o comando seguinte:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Da mesma forma, para converter um ficheiro PEM num ficheiro PFX, pode utilizar o seguinte comando (não é fornecida qualquer palavra-passe aqui):

```bash
openssl  pkcs12 -export -out Certificates.pfx -inkey Certificates.pem -in Certificates.pem -passout pass:'' 
```

Para obter mais informações, veja a [documentação de OpenSSL](https://www.openssl.org/docs/).

### <a name="connection-problems"></a>Problemas de ligação

Algumas operações poderão gerar a mensagem seguinte:

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

Verifique se o ponto final do cluster especificado está disponível e à escuta. Confirme, também, se a IU do Service Fabric Explorer está disponível no anfitrião e na porta. Para atualizar o ponto final, utilize `sfctl cluster select`.

### <a name="detailed-logs"></a>Registos detalhados

Muitas vezes, os registos detalhados são úteis para depurar ou comunicar problemas. Existe um sinalizador `--debug` global que aumenta a verbosidade dos ficheiros de registo.

### <a name="command-help-and-syntax"></a>Ajuda de comandos e sintaxe

Para obter ajuda com um comando específico ou um grupo de comandos, utilize o sinalizador `-h`.

```azurecli
sfctl application -h
```

Segue-se outro exemplo:

```azurecli
sfctl application create -h
```

## <a name="updating-the-service-fabric-cli"></a>Atualizar a CLI do Service Fabric 

Para atualizar a CLI do Service Fabric, execute os seguintes comandos (substitua `pip` por `pip3` consoante o que tiver escolhido durante a instalação original):

```bash
pip uninstall sfctl
pip install sfctl
```

## <a name="next-steps"></a>Passos seguintes

* [Implementar uma aplicação com a CLI do Azure Service Fabric](service-fabric-application-lifecycle-sfctl.md)
* [Introdução ao Service Fabric no Linux](service-fabric-get-started-linux.md)
