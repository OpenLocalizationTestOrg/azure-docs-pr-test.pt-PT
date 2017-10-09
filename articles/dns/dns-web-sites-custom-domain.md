---
title: "registos DNS personalizados aaaCreate para uma aplicação web | Microsoft Docs"
description: "Como o DNS de domínio personalizado de toocreate regista da aplicação web utilizando o DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Criar registos DNS para uma aplicação web num domínio personalizado

Pode utilizar o DNS do Azure toohost um domínio personalizado para as suas aplicações web. Por exemplo, estiver a criar uma aplicação web do Azure e pretender que o seu tooaccess utilizadores-lo ao utilizar contoso.com ou www.contoso.com como um FQDN.

toodo, tiver dois registos toocreate:

* Um toocontoso.com de apontador de registo raiz "A"
* Um "CNAME" de registo para o nome de www Olá que aponta toohello um registo

Tenha em atenção que, se criar um registo a para uma aplicação web no Azure, Olá que um registo tem de ser atualizado manualmente se Olá subjacente endereço IP para alterações de aplicações web Olá.

## <a name="before-you-begin"></a>Antes de começar

Antes de começar, tem primeiro de criar uma zona DNS no DNS do Azure e delegar a zona de Olá no seu tooAzure de entidade de registo DNS.

1. toocreate uma zona DNS, siga os passos Olá [criar uma zona DNS](dns-getstarted-create-dnszone.md).
2. toodelegate tooAzure seu DNS DNS, siga Olá passos [delegação de domínio DNS](dns-domain-delegation.md).

Depois de criar uma zona e delegar-tooAzure DNS, em seguida, pode criar registos para o seu domínio personalizado.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Criar um registo a para o domínio personalizado

Um registo é toomap utilizado um endereço IP do nome tooits. No seguinte exemplo de Olá iremos atribuirá como um tooan de registo de um endereço IPv4:

### <a name="step-1"></a>Passo 1

Criar um registo a e atribuir tooa $rs variável

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Passo 2

Adicionar o conjunto de registos Olá IPv4 valor toohello criado anteriormente "@" utilizando a variável de Olá $rs atribuído. Olá IPv4 valor atribuído será o endereço IP Olá para a sua aplicação web.

endereço IP Olá toofind para uma aplicação web, siga os passos Olá [configurar um nome de domínio personalizado no App Service do Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Passo 3

Consolide o conjunto de registos do toohello Olá alterações. Utilize `Set-AzureRMDnsRecordSet` Olá tooupload alterações toohello tooAzure de conjunto de registos DNS:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Criar um registo CNAME para o domínio personalizado

Se o seu domínio já está a ser gerido pelo DNS do Azure (consulte [delegação de domínio DNS](dns-domain-delegation.md), pode utilizar Olá toocreate de exemplo de Olá um registo CNAME para contoso.azurewebsites.net a seguir.

### <a name="step-1"></a>Passo 1

Abra o PowerShell e crie um novo conjunto de registos CNAME e atribua tooa $rs variável. Neste exemplo, irá criar um tipo de conjunto de registos CNAME com uma "Hora toolive" de 600 segundos na zona DNS com o nome "contoso.com".

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

Olá seguinte o exemplo é resposta Olá.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Passo 2

Assim que for criado Olá conjunto de registos CNAME, terá de toocreate um valor de alias que irá apontar toohello web app.

Pode utilizar Olá atribuídos anteriormente a variável "$rs" para utilizar o comando do PowerShell Olá abaixo alias de Olá toocreate para contoso.azurewebsites.net de aplicação web de Olá.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

Olá seguinte o exemplo é resposta Olá.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Passo 3

Confirmar alterações Olá utilizando Olá `Set-AzureRMDnsRecordSet` cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

Pode validar o registo de Olá foi criado corretamente consultando Olá "www.contoso.com" com nslookup, conforme mostrado abaixo:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Crie um registo de "awverify" para as aplicações web

Se decidir toouse um registo para a sua aplicação web, tem de ir através de um tooensure do processo de verificação, domínio personalizado Olá próprio. Este passo de verificação é feito através da criação de um registo CNAME especial com o nome "awverify". Esta secção aplica-se apenas a registos tooA.

### <a name="step-1"></a>Passo 1

Crie Olá "awverify" registo. Exemplo de Olá abaixo, iremos criar registo de "aweverify" Olá contoso.com tooverify propriedade para o domínio personalizado Olá.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

Olá seguinte o exemplo é resposta Olá.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Passo 2

Após criar o conjunto de registos de Olá "awverify", atribua Olá Registro CNAME definir alias. Exemplo de Olá abaixo, iremos atribuirá Olá CNAMe conjunto de registos alias tooawverify.contoso.azurewebsites.net.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

Olá seguinte o exemplo é resposta Olá.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Passo 3

Confirmar alterações Olá utilizando Olá `Set-AzureRMDnsRecordSet cmdlet`, conforme mostrado no comando Olá abaixo.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Passos seguintes

Siga os passos Olá [configurar um nome de domínio personalizado para o App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure sua toouse de aplicação web um domínio personalizado.
