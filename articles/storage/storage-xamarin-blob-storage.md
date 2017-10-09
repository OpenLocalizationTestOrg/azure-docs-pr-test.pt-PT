---
title: aaaHow toouse Blob Storage do Xamarin | Microsoft Docs
description: "Olá biblioteca de clientes do Storage do Azure para Xamarin permite aos programadores toocreate iOS, Android e Windows aplicações da loja com as suas interfaces de utilizador nativo. Este tutorial mostra como toouse Xamarin toocreate uma aplicação que utiliza o Blob storage do Azure."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>Como toouse Blob Storage do Xamarin
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Descrição geral
Xamarin permite aos programadores toouse um partilhado c# código base toocreate iOS, Android e Windows aplicações da loja com as suas interfaces de utilizador nativo. Este tutorial mostra como toouse Blob storage do Azure com uma aplicação Xamarin. Se quiser toolearn mais sobre o Storage do Azure, antes de explorar o código de Olá, consulte o artigo [introdução tooMicrosoft Storage do Azure](storage-introduction.md).

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Criar uma nova aplicação Xamarin
Para este tutorial, iremos irá criar uma aplicação que tenha como destino Android, iOS e Windows. Esta aplicação será simplesmente criar um contentor e carregar um blob para este contentor. Iremos utilizar Visual Studio no Windows, mas Olá learnings mesmos podem ser aplicadas ao criar uma aplicação utilizando o Xamarin Studio no macOS.

Siga estes passos toocreate a aplicação:

1. Se ainda não o fez, transfira e instale [Xamarin para Visual Studio](https://www.xamarin.com/download).
2. Abra o Visual Studio e crie uma aplicação em branco (nativo portáteis): **ficheiro > novo > projeto > plataforma > App(Native Portable) em branco**.
3. A solução no painel do Explorador de soluções de Olá com o botão direito e selecione **gerir pacotes NuGet para solução**. Procurar **Windowsazure** e instalar projetos do Olá mais recentes versão estável tooall na sua solução.
4. Compilar e executar o projeto.

Agora, deve ter uma aplicação que lhe permite tooclick um botão que incrementa um contador.

## <a name="create-container-and-upload-blob"></a>Criar o contentor e carregar blob
Em seguida, em seu `(Portable)` projeto, irá adicionar algum código demasiado`MyClass.cs`. Este código cria um contentor e carrega um blob para este contentor. `MyClass.cs`deve ter o seguinte aspeto Olá seguinte:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

Certifique-se de que tooreplace "your_account_name_here" e "your_account_key_here" com o nome da conta real e a chave de conta. 

O iOS, Android e Windows Phone todos os projetos tem referências tooyour portátil projeto - que significa que pode escrever todos os do seu código partilhado num coloque e utilização-lo em todos os seus projetos. Agora pode adicionar Olá de linha de partido de colocar de toostart tooeach projeto de código a seguir:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > mainactivity. CS

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > viewcontroller. CS

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a>Executar a aplicação Olá
Pode agora executar esta aplicação no emulador do Android ou Windows Phone. Também pode executar esta aplicação no emulador do iOS, mas esta opção requer um MAC. Para obter instruções específicas sobre como toodo, leia a documentação de Olá para [ligar o Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Depois de executar a aplicação, vai criar o contentor de Olá `mycontainer` na sua conta de armazenamento. Deve conter blob Olá, `myblob`, que tem texto Olá, `Hello, world!`. Pode verificar isto utilizando Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/).

## <a name="next-steps"></a>Passos seguintes
Neste tutorial, aprendeu como toocreate uma aplicação de plataformas cruzadas Xamarin que utiliza o armazenamento do Azure, especificamente concentrar-se num cenário no Blob Storage. No entanto, pode fazer muito mais com armazenamento de BLOBs não só, mas também com a tabela, ficheiros e armazenamento de filas. Consulte Olá artigos toolearn mais os seguintes:

* [Introdução ao armazenamento de Blobs do Azure através do .NET](storage-dotnet-how-to-use-blobs.md)
* [Introdução ao armazenamento de Tabelas do Azure através do .NET](storage-dotnet-how-to-use-tables.md)
* [Introdução ao Armazenamento de filas do Azure através do .NET](storage-dotnet-how-to-use-queues.md)
* [Introdução ao Armazenamento de Ficheiros do Azure no Windows](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

