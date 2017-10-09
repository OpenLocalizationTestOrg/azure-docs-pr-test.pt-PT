---
title: "aaaHow toouse Olá SDK de aplicações móveis do Azure para Android | Microsoft Docs"
description: "Como toouse Olá SDK de aplicações móveis do Azure para Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Como toouse Olá SDK de aplicações móveis do Azure para Android

Este guia mostra como toouse Olá Android SDK de cliente para cenários comuns de tooimplement Mobile Apps, tais como:

* Consultar dados (inserir, atualizar e eliminar).
* Autenticação.
* Processamento de erros.
* Personalizar cliente Olá.

Este guia está centrado nas Olá do lado do cliente Android SDK.  toolearn mais informações sobre como Olá SDKs do lado do servidor para Mobile Apps, consulte [trabalhar com o back-end de .NET SDK] [ 10] ou [como toouse Olá back-end Node.js SDK] [ 11].

## <a name="reference-documentation"></a>Documentação de referência

Pode encontrar Olá [referência da API de Javadocs] [ 12] da biblioteca de cliente do Android Olá no GitHub.

## <a name="supported-platforms"></a>Plataformas suportadas

Olá SDK de aplicações móveis do Azure para Android suporta níveis de API 19 através de 24 (KitKat através de Nougat) para o telefone e tablet fatores de formulários.  A autenticação, em particular, utiliza uma comuns web framework abordagem toogather as credenciais.  Autenticação de servidor fluxo não funciona com dispositivos de fator de formulário pequeno como observa.

## <a name="setup-and-prerequisites"></a>A configuração e pré-requisitos

Olá concluída [início rápido de aplicações móveis](app-service-mobile-android-get-started.md) tutorial.  Esta tarefa garante que todos os pré-requisitos para o desenvolvimento de aplicações móveis do Azure foram cumpridos.  Olá início rápido também o ajuda a configurar a sua conta e criar a sua primeira back-end da aplicação móvel.

Se decidir não toocomplete tutorial de início rápido de Olá, conclua Olá seguintes tarefas:

* [criar um back-end de aplicação móvel] [ 13] toouse com a sua aplicação Android.
* No Android Studio, [atualização Olá Gradle compilar ficheiros](#gradle-build).
* [Ativar a permissão de internet](#enable-internet).

### <a name="gradle-build"></a>Olá Gradle criar ficheiro de atualização

Alterar ambas **gradle** ficheiros:

1. Adicione este código toohello *projeto* nível **gradle** ficheiro dentro Olá *buildscript* etiqueta:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Adicione este código toohello *módulo aplicação* nível **gradle** ficheiro dentro Olá *dependências* etiqueta:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    Versão mais recente Olá está atualmente 3.3.0. versões de Olá suportado estão listadas [na gaveta][14].

### <a name="enable-internet"></a>Ativar a permissão de internet

tooaccess do Azure, a aplicação tem de ter permissão de INTERNET Olá ativada. Se ainda não estiver ativada, adicionar Olá seguinte linha de código tooyour **AndroidManifest.xml** ficheiro:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Criar uma ligação de cliente

Mobile Apps do Azure fornece quatro funções tooyour de aplicações móveis:

* Acesso a dados e a Sincronização Offline com um serviço de aplicações móveis do Azure.
* Chame APIs personalizadas escritas com Olá SDK do servidor de aplicações do Azure Mobile.
* Autenticação com o App Service do Azure autenticação e autorização.
* Registo da notificação com os Hubs de notificação push.

Cada uma destas funções primeiro exige que crie um `MobileServiceClient` objeto.  Apenas um `MobileServiceClient` objecto deve ser criado dentro do seu cliente móvel (ou seja, deve ser um padrão de Singleton).  toocreate um `MobileServiceClient` objeto:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Olá `<MobileAppUrl>` é uma cadeia ou um objeto de URL que aponta tooyour back-end móvel.  Se estiver a utilizar o back-end móvel toohost do App Service do Azure, em seguida, certifique-se de utilizar Olá segura `https://` versão do URL de Olá.

Olá cliente também requer acesso toohello atividade ou contexto - hello `this` parâmetro no exemplo de Olá.  Olá MobileServiceClient construção deverá ocorrer dentro de Olá `onCreate()` método de Olá atividade referenciada na Olá `AndroidManifest.xml` ficheiro.

Como melhor prática, deve de separar as comunicações de servidor na sua própria classe (padrão de singleton).  Neste caso, deverá passar Olá atividade dentro de Olá construtor tooappropriately configurar serviço de Olá.  Por exemplo:

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

Agora pode chamar `AzureServiceAdapter.Initialize(this);` no Olá `onCreate()` método da sua atividade principal.  Utilizam outros métodos de que necessitam do cliente do acesso toohello `AzureServiceAdapter.getInstance();` tooobtain um adaptador de serviço de toohello de referência.

## <a name="data-operations"></a>Operações de dados

núcleo de Olá de Olá SDK de aplicações móveis do Azure é tooprovide acesso toodata armazenado no SQL Azure no back-end de aplicação móvel de Olá.  Pode aceder a estes dados a utilizar classes com tipo seguro (preferidas) ou sem tipos consultas (não recomendadas).  em massa de Olá desta secção lida com a utilizar classes com tipo seguro.

### <a name="define-client-data-classes"></a>Definir as classes de dados de cliente

dados de tooaccess das tabelas de SQL Azure, definir classes de dados de cliente que correspondem a tabelas toohello Olá back-end da aplicação móvel. Os exemplos neste tópico partem do princípio de uma tabela com o nome **MyDataTable**, que tem Olá seguintes colunas:

* ID
* Texto
* Concluir

Olá correspondente objeto escrito do lado do cliente reside num ficheiro denominado **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Adicione métodos getter e setter para cada campo que adicionar.  Se a tabela de SQL Azure contiver mais colunas, seria adicionar classe de toothis de campos Olá correspondente.  Por exemplo, se hello DTO (objeto de transferência de dados) tinha uma coluna de prioridade de número inteiro, em seguida, poderá adicionar este campo, juntamente com os seus métodos getter e setter:

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

toolearn como toocreate tabelas adicionais no seu back-end do Mobile Apps, consulte [como: definir um controlador de tabela] [ 15] (back-end do .NET) ou [definir tabelas utilizando um esquema dinâmica] [ 16] (Back-end do Node.js).

Uma tabela de back-end do Mobile Apps do Azure define cinco campos especiais, quatro que são tooclients disponíveis:

* `String id`: Olá ID globalmente exclusivo para o registo de Olá.  Como melhor prática, certifique-Olá id Olá representação de um [UUID] [ 17] objeto.
* `DateTimeOffset updatedAt`: Olá data/hora da última atualização da Olá.  campo de updatedAt Olá é definido pelo servidor Olá e nunca deve ser definido pelo seu código de cliente.
* `DateTimeOffset createdAt`: Olá data/hora esse objeto Olá foi criado.  campo de createdAt Olá é definido pelo servidor Olá e nunca deve ser definido pelo seu código de cliente.
* `byte[] version`: Normalmente representado como uma cadeia, a versão de Olá seja também definido pelo servidor Olá.
* `boolean deleted`: Indica que o registo de Olá foram eliminado mas não removido ainda.  Não utilize `deleted` como uma propriedade de classe.

Olá `id` campo é obrigatório.  Olá `updatedAt` campo e `version` campo são utilizados para sincronização offline (para a resolução de sincronização e conflito incremental respetivamente).  Olá `createdAt` é um campo de referência de campo e não é utilizado pelo cliente de Olá.  os nomes de Olá são "entre a transmissão" nomes de propriedades de Olá e não são ajustável.  No entanto, pode criar um mapeamento entre o objeto e Olá nomes de "entre a transmissão" utilizando Olá [gson] [ 3] biblioteca.  Por exemplo:

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a>Criar uma referência de tabela

tooaccess uma tabela, primeiro crie um [MobileServiceTable] [ 8] objeto ao chamar Olá **getTable** método no Olá [MobileServiceClient][9].  Este método tem dois sobrecargas:

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

No Olá seguinte código, **mClient** é um objeto de MobileServiceClient tooyour referência.  sobrecarga primeiro Olá é utilizada em que nome de classe de Olá e nome da tabela Olá são Olá mesmo e é hello um utilizado no Olá início rápido:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Olá sobrecarga segundo é utilizada quando o nome da tabela Olá é diferente do nome de classe de Olá: primeiro parâmetro de Olá é o nome de tabela Olá.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Consulta uma tabela de back-end

Em primeiro lugar, obtenha uma referência de tabela.  Em seguida, execute uma consulta numa referência de tabela Olá.  Uma consulta é qualquer combinação de:

* A `.where()` [cláusula de filtro](#filtering).
* Um `.orderBy()` [ordenação cláusula](#sorting).
* A `.select()` [cláusula de seleção de campo](#selection).
* A `.skip()` e `.top()` para [resultados do bloco paginado](#paging).

cláusulas Olá tem de ser apresentadas no Olá anterior a ordem.

### <a name="filter"></a>Filtrar resultados

formulário de geral Olá de uma consulta é:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Olá anterior exemplo devolve todos os resultados (se o tamanho máximo de página toohello definido pelo servidor Olá).  Olá `.execute()` método executa a consulta de Olá no back-end de Olá.  Olá consulta é convertida tooan [OData v3] [ 19] consulta antes da transmissão toohello Mobile Apps back-end.  Na receção, back-end das Mobile Apps do Olá converte consulta Olá uma instrução de SQL Server antes de executar a instância de SQL Azure Olá.  Uma vez que a atividade de rede demora algum tempo, Olá `.execute()` método devolve um [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Filtrar os dados devolvidos

Olá após a execução da consulta devolve todos os itens de Olá **ToDoItem** tabela onde **concluída** é igual a **falso**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** Olá referência toohello serviço móvel tabela que criámos anteriormente.

Define um filtro com Olá **onde** chamada do método na referência de tabela Olá. Olá **onde** método é seguido um **campo** método seguido de um método que especifica o predicado de lógica de Olá. Métodos de predicado possíveis incluem **eq** (igual a), **ne** (não igual a), **gt** (superior), **ge** (maior ou igual a), **lt** (inferior), **le** (menor ou igual a). Estes métodos permitem-lhe comparar o número e toospecific valores de campos de cadeia.

Pode filtrar as datas. Olá métodos seguintes permitem-lhe comparar o campo de data completo de Olá ou partes da data de Olá: **ano**, **mês**, **dia**, **hora**, **minuto**, e **segundo**. Olá exemplo seguinte adiciona um filtro para itens cujo *data devida* é igual a 2013.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Olá seguintes métodos de suportam filtros complexos em campos de cadeia: **startsWith**, **endsWith**, **concat**, **subcadeia**, **indexOf**, **substituir**, **toLower**, **toUpper**, **compactar**, e  **comprimento**. Olá filtros de exemplo a seguir para a tabela de linhas em que hello *texto* coluna começa com "PRI0."

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

os seguintes métodos de operador de Olá é suportada em campos de números: **adicionar**, **sub**, **mul**, **div**, **mod**, **piso**, **limite**, e **arredondar**. Olá filtros de exemplo a seguir para a tabela de linhas em que hello **duração** é um número par.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

Pode combinar os predicados com estes métodos lógicos: **e**, **ou** e **não**. Olá seguinte o exemplo combina duas Olá precedente exemplos.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Agrupar e aninhar operadores lógicos:

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

Para obter mais debate e exemplos de filtragem, consulte [explorar richness Olá do modelo de consulta do cliente do Android Olá][20].

### <a name="sorting"></a>Ordenação devolvida dados

Olá seguinte código devolve todos os itens de uma tabela com **ToDoItems** ordenados ascendente por Olá *texto* campo. *mToDoTable* Olá referência toohello back-end tabela que criou anteriormente:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

Olá primeiro parâmetro de Olá **orderBy** método é um nome de toohello igual de cadeia do campo de Olá no qual toosort. segundo parâmetro de Olá utiliza Olá **QueryOrder** toospecify de enumeração se toosort ascendente ou descendente.  Se está a filtrar utilizando Olá ***onde*** método, Olá ***onde*** método tem de ser invocado antes Olá ***orderBy*** método.

### <a name="selection"></a>Selecionar colunas específicas

Olá seguinte código ilustra como tooreturn todos os itens de uma tabela com **ToDoItems**, mas apenas apresenta Olá **concluída** e **texto** campos. **mToDoTable** Olá referência toohello back-end tabela que criámos anteriormente.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

a função Olá parâmetros toohello selecione são os nomes de cadeia de Olá das colunas da tabela de Olá que pretende que o tooreturn.  Olá **selecione** método tem métodos toofollow como **onde** e **orderBy**. Pode ser seguido de métodos de paginação, como **ignorar** e **superior**.

### <a name="paging"></a>Devolver dados nas páginas

Os dados são **sempre** devolvido nas páginas.  número máximo de Olá de registos devolvidos é definido pelo servidor Olá.  Se os pedidos de cliente de Olá mais registos, o servidor de Olá devolve número máximo de Olá de registos.  Por predefinição, o tamanho máximo de página de Olá no servidor de Olá é 50 registos.

primeiro exemplo de Olá mostra como tooselect Olá cinco itens superiores de uma tabela. consulta de Olá devolve itens Olá de uma tabela com **ToDoItems**. **mToDoTable** Olá referência toohello back-end tabela que criou anteriormente:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Segue-se uma consulta que ignora Olá primeiro cinco itens e, em seguida, devolve Olá cinco seguinte:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Se quiser tooget todos os registos numa tabela, implemente código tooiterate através de todas as páginas:

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

Um pedido para todos os registos ao utilizar este método cria um mínimo de dois pedidos toohello Mobile Apps back-end.

> [!TIP]
> Escolher entre Olá para o tamanho de página direita é um equilíbrio entre a utilização da memória enquanto o pedido de Olá está a acontecer, a utilização de largura de banda e a atraso na receção de dados de Olá completamente.  a predefinição de Olá (50 registos) é adequada para todos os dispositivos.  Se utilizar exclusivamente nos dispositivos de memória superiores, aumente a segurança too500.  Ter encontrámos esse tamanho de página Olá crescente para além de 500 regista resultados em atrasos inaceitável e problemas de memória grande.

### <a name="chaining"></a>Como: concatenar métodos de consulta

os métodos de Olá no consultar tabelas de back-end podem concatenar. Encadeamento métodos permite-lhe tooselect colunas específicas de filtrado linhas são ordenadas e bloco paginadas de consulta. Pode criar filtros lógicos complexos.  Cada método de consulta devolve um objeto da consulta. série de Olá tooend de métodos e consulta de Olá, na verdade, de execução, chamada Olá **executar** método. Por exemplo:

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

Olá encadeados consulta métodos tem de ser ordenados como segue:

1. Filtragem (**onde**) métodos.
2. A ordenação (**orderBy**) métodos.
3. Seleção (**selecione**) métodos.
4. paginação (**ignorar** e **superior**) métodos.

## <a name="binding"></a>Vincular a interface de utilizador de toohello de dados

O enlace de dados envolve três componentes:

* origem de dados de Olá
* esquema do ecrã Olá
* adaptador de Olá que ties Olá, dois em conjunto.

No nosso código de exemplo, iremos devolver dados de Olá da tabela de Mobile Apps SQL Azure Olá **ToDoItem** para uma matriz. Esta atividade é um padrão comum para aplicações de dados.  Consultas de base de dados, muitas vezes, devolvem uma coleção de linhas que Olá cliente obtém uma lista ou a matriz. Neste exemplo, a matriz de Olá é origem de dados de Olá.  código de Olá Especifica um esquema de ecrã que define a vista de Olá Olá de dados de que é apresentado no dispositivo Olá.  Olá dois estão vinculados juntamente com um adaptador, o qual este código é uma extensão de Olá **ArrayAdapter&lt;ToDoItem&gt;**  classe.

#### <a name="layout"></a>Definir Olá esquema

esquema de Olá é definida por alguns fragmentos de código XML. Tendo em conta um esquema existente, Olá seguinte código representa Olá **ListView** queremos toopopulate com os nossos dados do servidor.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

No Olá precedente código, Olá *listitem* atributo especifica o id de Olá do esquema de Olá para uma linha individuais na lista de Olá. Este código especifica uma caixa de verificação e do respetivo texto associado e obtém instanciado uma vez para cada item na lista de Olá. Este esquema não apresenta Olá **id** campo e um esquema mais complexo de especificar os campos adicionais na apresentação de Olá. Este código está a ser Olá **row_list_to_do.xml** ficheiro.

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a>Definir o adaptador de Olá
Uma vez que a origem de dados de Olá da nossa vista é uma matriz de **ToDoItem**, iremos subclasse nosso adaptador de um **ArrayAdapter&lt;ToDoItem&gt;**  classe. Este subclasse produz uma vista para cada **ToDoItem** utilizando Olá **row_list_to_do** esquema.  No nosso código, iremos definir Olá seguir uma classe que seja uma extensão de Olá **ArrayAdapter&lt;i&gt;**  classe:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Substituir adaptadores Olá **getView** método. Por exemplo:

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

Estamos a criar uma instância desta classe no nosso atividade da seguinte forma:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Olá segundo parâmetro toohello ToDoItemAdapter construtor é um esquema de toohello de referência. Iremos agora pode instanciar Olá **ListView** e atribuir Olá adaptador toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Utilizar Olá adaptador tooBind toohello da IU

Agora, está pronto toouse o enlace de dados. Olá código seguinte mostra como tooget itens na tabela de Olá e preenche Olá adaptador local com Olá devolvido itens.

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

Chamar adaptador Olá sempre modificar Olá **ToDoItem** tabela. Uma vez que as modificações são efetuadas numa base de registo por registo, para processar uma única linha, em vez de uma coleção. Inserir um item, chamar Olá **adicionar** método no Olá adaptador; a eliminar, chamar Olá **remover** método.

Pode encontrar um exemplo completo em Olá [Android projeto de início rápido][21].

## <a name="inserting"></a>Inserir dados de back-end de Olá

Instanciar uma instância de Olá *ToDoItem* classe e definir as respetivas propriedades.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Em seguida, utilize **INSERT ()** tooinsert um objeto:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Olá dados devolvidos pela entidade correspondências Olá inseridos na tabela de back-end Olá, ID de Olá incluídos e quaisquer outros valores (como Olá `createdAt`, `updatedAt`, e `version` campos) definida no back-end de Olá.

As tabelas de Mobile Apps requerem uma coluna de chave primária com o nome **id**. Esta coluna tem de ser uma cadeia. valor predefinido de Olá da coluna de ID de Olá é um GUID.  Pode fornecer outros valores exclusivos, como endereços de e-mail ou nomes de utilizador. Quando um valor de ID de cadeia não é fornecido para um registo inserido, o back-end de Olá gera um novo GUID.

Valores de ID de cadeia fornecem Olá seguintes vantagens:

* Os iDs podem ser gerados sem o tornar uma base de dados de toohello de ida e volta.
* Os registos são toomerge mais fácil de tabelas diferentes ou bases de dados.
* Valores de ID melhor integram com a lógica de uma aplicação.

Os valores de ID de cadeia são **REQUIRED** para suporte de sincronização offline.  Não é possível alterar um Id assim que esta está armazenada na base de dados de back-end de Olá.

## <a name="updating"></a>Atualize dados numa aplicação móvel

dados de tooupdate numa tabela, transmitir Olá novo objeto toohello **Update ()** método.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

Neste exemplo, *item* é uma linha de referência tooa no Olá *ToDoItem* tabela, o que tenha tido tooit algumas alterações.  Olá linha com Olá mesmo **id** é atualizado.

## <a name="deleting"></a>Eliminar dados de uma aplicação móvel

Olá código a seguir mostra como toodelete dados de uma tabela, especificando Olá objeto de dados.

```java
mToDoTable
    .delete(item);
```

Também pode eliminar um item, especificando Olá **id** campo Olá toodelete de linha.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Procurar um item específico por Id

Procurar um item com específico **id** campo com Olá **lookUp()** método:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Como: trabalhar com dados sem tipo

o modelo de programação sem tipo Olá dá-lhe controlo exato através de serialização JSON.  Existem alguns cenários comuns em que pode ser útil toouse um modelo de programação sem tipo. Por exemplo, se a tabela de back-end contém demasiadas colunas e só precisa de tooreference um subconjunto de colunas de Olá.  modelo escrito Olá requer toodefine todas as colunas de Olá definidas no back-end das Mobile Apps de Olá na sua classe de dados.  Na maioria das chamadas à API para aceder aos dados de Olá é semelhante toohello escreveu chamadas de programação. Olá principal diferença é que no modelo sem tipo Olá invocar métodos em Olá **MobileServiceJsonTable** objeto, em vez de Olá **MobileServiceTable** objeto.

### <a name="json_instance"></a>Criar uma instância de uma tabela sem tipo

Toohello semelhante escreveu modelo, pode começa por colocar uma referência de tabela, mas neste caso é um **MobileServicesJsonTable** objeto. Obter referência Olá ao chamar Olá **getTable** método numa instância do cliente de Olá:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Assim que tiver criado uma instância de Olá **MobileServiceJsonTable**, tem Olá virtualmente API mesmo disponível como com o modelo de programação escrito Olá. Em alguns casos, os métodos de Olá assumem um parâmetro sem tipo em vez de um parâmetro com tipo.

### <a name="json_insert"></a>Inserir uma tabela sem tipo
Olá a seguir mostra código como toodo insert. Olá primeiro passo é toocreate um [JsonObject][1], que faz parte de Olá [gson] [ 3] biblioteca.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Em seguida, utilize **INSERT ()** tooinsert objeto sem tipo de Olá na tabela de Olá.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Se precisar de tooget Olá ID de objeto de Olá inserir, utilize Olá **getAsJsonPrimitive()** método.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Eliminar uma tabela sem tipo
Olá código seguinte mostra como toodelete uma instância, Olá neste caso, a mesma instância de um **JsonObject** que foi criado no antes de Olá *inserir* exemplo. código de Olá é Olá mesmo tal como acontece com Olá escreveu maiúsculas e minúsculas, mas o método de Olá tem uma assinatura diferente, porque referencia uma **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

Também pode eliminar uma instância diretamente, utilizando o respetivo ID:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Devolver todas as linhas a partir de uma tabela sem tipo
Olá a seguir mostra código como tooretrieve uma tabela inteira. Uma vez que estiver a utilizar uma tabela em JSON, pode obter apenas algumas das colunas da tabela de Olá seletivamente.

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

Olá mesmo conjunto de filtragem, filtragem e paginação métodos disponíveis para o modelo com tipo Olá estão disponíveis para o modelo sem tipo Olá.

## <a name="offline-sync"></a>Implementar a Sincronização Offline

Olá cliente SDK do Azure Mobile Apps também implementa sincronização offline dos dados utilizando um toostore de base de dados do SQLite uma cópia dos dados do servidor de Olá localmente.  Operações executadas numa tabela offline não necessitam de conectividade móveis toowork.  Ajudas de sincronização offline no resiliência e desempenho em despesa Olá de lógica mais complexa para resolução de conflitos.  Olá cliente SDK do Azure Mobile Apps implementa Olá seguintes funcionalidades:

* Sincronização incremental: Registos nova e atualizados apenas são transferidos, guardar o consumo de memória e largura de banda.
* Simultaneidade otimista: Operações são consideradas toosucceed.  Resolução de conflitos é deferida até que as atualizações são executadas no servidor de Olá.
* Resolução de conflitos: Olá que SDK Deteta quando uma alteração em conflito foram efetuada no servidor de Olá e fornece hooks utilizador de Olá tooalert.
* Eliminação de forma recuperável: Registos eliminados são marcados eliminados, permitindo que os outro dispositivos tooupdate respetiva cache offline.

### <a name="initialize-offline-sync"></a>Iniciar Sincronização Offline

Cada tabela offline tem de ser definida na cache de offline Olá antes de utilização.  Normalmente, a definição da tabela é feita imediatamente após a criação de hello do cliente de Olá:

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Obter uma referência toohello Offline tabela de Cache

Para uma tabela online, utilize `.getTable()`.  Para uma tabela offline, utilize `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Olá todos os métodos que estão disponíveis em tabelas online (incluindo filtragem, ordenação, paginação, inserir dados, atualizar dados e a eliminação de dados) funcionam igualmente bem em tabelas online e offline.

### <a name="synchronize-hello-local-offline-cache"></a>Sincronizar Olá Local Offline Cache

A sincronização é controlo Olá da sua aplicação.  Segue-se um método de sincronização de exemplo:

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

Se for fornecido um nome de consulta toohello `.pull(query, queryname)` método, em seguida, sincronização incremental é registos apenas tooreturn utilizado e que foram criados ou alterados desde a solicitação de Olá pela última vez foi concluída com êxito.

### <a name="handle-conflicts-during-offline-synchronization"></a>Identificador de conflitos durante a Sincronização Offline

Se acontecer um conflito durante um `.push()` operação, uma `MobileServiceConflictException` é emitida.   item de servidor emitido Olá está incorporado na exceção de Olá e podem ser obtida pelos `.getItem()` na exceção de Olá.  Ajuste push Olá ao chamar Olá seguintes itens no objeto de MobileServiceSyncContext Olá:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Depois de todos os conflitos são marcados como quiser, chamar `.push()` novamente tooresolve Olá todos os conflitos.

## <a name="custom-api"></a>Chamar uma API personalizada

Uma API personalizada permite-lhe toodefine pontos finais personalizados que expõem funcionalidades do servidor que não mapear tooan inserir, atualizar, eliminar ou operação de leitura. Ao utilizar uma API personalizada, pode ter mais controlo sobre mensagens, incluindo o ler, definir cabeçalhos de mensagens HTTP e definir um formato de corpo de mensagem que não sejam JSON.

A partir de um cliente do Android, tem de chamar Olá **invokeApi** método toocall Olá personalizado ponto final de API. Olá exemplo seguinte mostra como toocall um ponto final de API com o nome **completeAll**, que devolve uma classe de coleção com o nome **MarkAllResult**.

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

Olá **invokeApi** método é denominado no cliente Olá, o que envia uma mensagem de pedido toohello nova API personalizada. resultado de Olá devolvido por API personalizada Olá apresentado numa caixa de diálogo mensagem, tal como quaisquer erros. Outras versões **invokeApi** permitem-lhe enviar um objeto no corpo do pedido de Olá opcionalmente, especifique o método de Olá HTTP e enviar parâmetros de consulta com o pedido de Olá. Sem tipos versões do **invokeApi** são fornecidos bem.

## <a name="authentication"></a>Adicionar autenticação tooyour aplicação

Tutoriais já descrevem em detalhe como tooadd estas funcionalidades.

Serviço de aplicações suporta [autenticar utilizadores de aplicação](app-service-mobile-android-get-started-users.md) através de vários fornecedores de identidade externas: Facebook, Google, Account Microsoft, Twitter e o Azure Active Directory. Pode definir permissões de acesso de toorestrict tabelas para operações específicas tooonly autenticada utilizadores. Também pode utilizar a identidade de Olá utilizadores autenticados tooimplement das regras de autorização no seu back-end.

São suportados dois fluxos de autenticação: um **servidor** fluxo e um **cliente** fluxo. fluxo de servidor Olá fornece a experiência de autenticação mais simples de Olá, como baseia-se na interface de web de fornecedores de identidade Olá.  Não existem SDKs adicionais são tooimplement necessária autenticação de fluxo do servidor. Autenticação de fluxo de servidor não fornece uma integração profunda em dispositivos móveis Olá e só é recomendada para uma prova de cenários de conceito.

fluxo de cliente Olá permite a integração mais profunda com as capacidades específicas do dispositivo, como o início de sessão único como depende SDKs fornecidas pelo fornecedor de identidade Olá.  Por exemplo, pode integrar Olá Facebook SDK na sua aplicação móvel.  cliente para dispositivos móveis Olá trocas na aplicação do Facebook Olá e confirma o início de sessão antes de troca de aplicação móvel de back-tooyour.

Quatro passos são necessários tooenable autenticação na sua aplicação:

* Registe a aplicação para autenticação com um fornecedor de identidade.
* Configure o back-end do serviço de aplicações.
* Restringir os utilizadores de tooauthenticated de permissões tabela apenas em Olá back-end do serviço de aplicações.
* Adicione a aplicação de tooyour de código de autenticação.

Pode definir permissões de acesso de toorestrict tabelas para operações específicas tooonly autenticada utilizadores. Também pode utilizar Olá SID de um utilizador autenticado toomodify pedidos.  Para obter mais informações, consulte [introdução à autenticação] e Olá documentação HOWTO de SDK do servidor.

### <a name="caching"></a>Autenticação: Fluxo de servidor

Olá código seguinte inicia um processo de início de sessão de fluxo de servidor utilizando o fornecedor de Google Olá.  É necessária configuração adicional devido aos requisitos de segurança de Olá para o fornecedor de Google Olá:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Além disso, adicione Olá classe de atividade principal do método toohello os seguintes:

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

Olá `GOOGLE_LOGIN_REQUEST_CODE` definido no seu main atividade é utilizada para Olá `login()` método e dentro de Olá `onActivityResult()` método.  Pode escolher qualquer número exclusivo, desde que hello mesmo número é utilizado no Olá `login()` método e Olá `onActivityResult()` método.  Se separar o código de cliente Olá para um adaptador de serviço (conforme mostrado anteriormente), deve chamar os métodos de adequada de Olá no adaptador de serviço Olá.

Também precisa de projeto de Olá tooconfigure para customtabs.  Primeiro, especifique um URL de redirecionamento.  Adicionar Olá seguinte fragmento demasiado`AndroidManifest.xml`:

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

Adicionar Olá **redirectUriScheme** toohello `build.gradle` ficheiro para a sua aplicação:

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

Por fim, adicione `com.android.support:customtabs:23.0.1` toohello a lista de dependências em Olá `build.gradle` ficheiro:

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

Obter ID de Olá de Olá utilizador com sessão iniciada de um **MobileServiceUser** utilizando Olá **getUserId** método. Para obter um exemplo de como toouse Futures toocall Olá assíncrono início de sessão APIs, consulte [introdução à autenticação].

> [!WARNING]
> Olá esquema de URL mencionado diferencia maiúsculas de minúsculas.  Certifique-se de que todas as ocorrências de `{url_scheme_of_you_app}` corresponder a maiúsculas e minúsculas.

### <a name="caching"></a>Tokens de autenticação de cache

Colocação em cache os tokens de autenticação requer toostore Olá ID de utilizador e o token de autenticação localmente no dispositivo de Olá. Olá próxima vez que inicia a aplicação Olá, seleciona cache Olá, e se estes valores não estiverem presentes, pode ignorar registo de Olá no procedimento rehydrate cliente Olá com estes dados. No entanto estes dados são sensíveis e devem ser armazenado encriptados para segurança no caso de telefone Olá obtém roubado.  Pode ver um exemplo completo de como autenticação toocache tokens no [secção de tokens de autenticação da Cache][7].

Quando tenta toouse um token expirado, receberá um *401 não autorizado* resposta. Pode processar erros de autenticação utilizando filtros.  Filtros interceptar pedidos toohello back-end do serviço de aplicações. o código de filtro de Olá testa a resposta de Olá para um 401, aciona o processo de início de sessão Olá e, em seguida, retoma pedido Olá que gerou Olá 401.

### <a name="refresh"></a>Utilize Tokens de atualização

token de Olá devolvido por autorização e autenticação do serviço de aplicações do Azure tem um tempo de vida definido de uma hora.  Após este período, tem de voltar utilizador Olá.  Se for um token de longa duração que receberam através da autenticação de fluxo de cliente, em seguida, pode voltar a utilizar com autenticação do serviço de aplicações do Azure e a utilização de autorização Olá mesmo token.  Outro token do App Service do Azure é gerado com uma duração de novo.

Também pode registar Olá fornecedor toouse Tokens de atualização.  Um Token de atualização não está sempre disponível.  É necessária configuração adicional:

* Para **do Azure Active Directory**, configurar um segredo de cliente para Olá aplicação do Active Directory do Azure.  Especifique o segredo do cliente Olá no Olá App Service do Azure quando configurar a autenticação do Active Directory do Azure.  Quando chamar `.login()`, transmitir `response_type=code id_token` como um parâmetro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Para **Google**, transmitir Olá `access_type=offline` como um parâmetro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Para **Account Microsoft**, selecione Olá `wl.offline_access` âmbito.

chamar toorefresh um token, `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Como melhor prática, crie um filtro que Deteta uma resposta 401 do servidor de Olá e tenta token de utilizador de Olá toorefresh.

## <a name="log-in-with-client-flow-authentication"></a>Iniciar sessão com a autenticação de cliente-fluxo

processo geral de Olá para iniciar sessão com a autenticação de fluxo de cliente é o seguinte:

* Configure a autorização e autenticação do serviço de aplicações do Azure tal como faria com autenticação de servidor fluxo.
* Integre o SDK de fornecedor de autenticação Olá para autenticação tooproduce um token de acesso.
* Chamar Olá `.login()` método da seguinte forma:

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

Substitua Olá `onSuccess()` método com independentemente código que queira toouse num início de sessão com êxito.  Olá `{provider}` cadeia é um fornecedor de válido: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, ou **twitter**.  Se tiver implementado a autenticação personalizada, em seguida, também pode utilizar etiquetas de fornecedor de autenticação personalizado de Olá.

### <a name="adal"></a>Autenticar os utilizadores com Olá Active Directory Authentication Library (ADAL)

Pode utilizar os utilizadores de toosign do Active Directory Authentication Library (ADAL) Olá na sua aplicação com o Azure Active Directory. A utilização de um início de sessão do fluxo de cliente, muitas vezes, é preferível toousing Olá `loginAsync()` métodos que fornece uma funcionalidade do UX mais nativa e permite a personalização adicional.

1. Configurar o back-end da aplicação móvel para o início de sessão do AAD ao seguinte Olá [como tooconfigure App Service para início de sessão do Active Directory] [ 22] tutorial. Certifique-se de que toocomplete Olá passo opcional de registar uma aplicação cliente nativa.
2. Instale ADAL modificando o Olá tooinclude do gradle ficheiros seguintes definições:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. Adicione Olá aplicação tooyour de código a seguir, tornando Olá substituições os seguintes:

* Substitua **aqui de autoridade de inserção** com o nome de Olá do inquilino Olá no qual que aprovisionou a sua aplicação. formato de Olá deve ser https://login.microsoftonline.com/contoso.onmicrosoft.com.
* Substitua **INSERT-RESOURCE-ID-aqui** com o ID de cliente Olá do back-end da aplicação móvel. Pode obter ID de cliente Olá de Olá **avançadas** separador em **definições do Azure Active Directory** no portal de Olá.
* Substitua **INSERT-cliente ID aqui** com o ID de cliente Olá copiados da aplicação de cliente nativo Olá.
* Substitua **INSERT-REDIRECIONAMENTO-URI-aqui** com o seu site */.auth/login/done* ponto final, utilizando o esquema HTTPS de Olá. Este valor deve ser semelhante demasiado*https://contoso.azurewebsites.net/.auth/login/done*.

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a>Ajustar Olá comunicação cliente-servidor

Olá ligação de cliente é normalmente uma ligação de HTTP básica Olá subjacente biblioteca HTTP fornecida com Olá Android SDK a utilizar.  Existem várias razões, razão pela qual pretenda toochange que:

* Pretende toouse um tempos de limite de tooadjust de biblioteca HTTP alternativo.
* Pretende tooprovide uma barra de progresso.
* Pretende tooadd uma funcionalidade de gestão de toosupport API de cabeçalho personalizado.
* Pretende toointercept uma resposta de falha para que pode implementar a reautenticação rápida.
* Pretende que o serviço de análise do tooan de pedidos do toolog back-end.

### <a name="using-an-alternate-http-library"></a>Utilizar uma biblioteca de HTTP alternativo

Chamar Olá `.setAndroidHttpClientFactory()` método imediatamente depois de criar uma referência de cliente.  Por exemplo, tooset Olá ligação too60 segundos de tempo limite (em vez da predefinição de Olá 10 segundos):

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a>Implementar um filtro de progresso

Pode implementar um intercept de cada pedido, implementando um `ServiceFilter`.  Por exemplo, o seguinte Olá atualiza uma barra de progresso previamente criada:

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

Pode ligar a este cliente de toohello de filtro da seguinte forma:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Personalizar a cabeçalhos de pedido

Utilize o seguinte Olá `ServiceFilter` e anexe o filtro de Olá em Olá mesma forma que Olá `ProgressFilter`:

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a>Configurar serialização automática

Pode especificar uma estratégia de conversão aplica-se a coluna de tooevery utilizando Olá [gson] [ 3] API. biblioteca de cliente do Android Olá utiliza [gson] [ 3] em segundo plano de Olá tooserialize Java objetos tooJSON dados antes do envio de dados de Olá tooAzure do serviço de aplicações.  Olá código seguinte utiliza Olá **setFieldNamingStrategy()** estratégia de Olá tooset de método. Neste exemplo eliminará Olá inicial caráter (um "m") e caráter seguinte, em seguida, minúsculos Olá, para cada nome de campo. Por exemplo, este seria ativar "mId" em "id".  Implementar um Olá de tooreduce de estratégia de conversão necessita para `SerializedName()` anotações na maioria dos campos.

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

Este código tem de ser executado antes de criar uma referência de cliente para dispositivos móveis utilizando Olá **MobileServiceClient**.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[introdução à autenticação]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
