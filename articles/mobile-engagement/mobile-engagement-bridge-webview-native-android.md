---
title: aaaBridge WebView Android com nativo Mobile Engagement SDK Android
description: "Descreve como toocreate uma ponte entre WebView em execução de Javascript e Olá nativo Mobile Engagement SDK Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: cf272f3f-2b09-41b1-b190-944cdca8bba2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a7a09bcc156490fe69ad29a67809745dcfc22da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="bridge-android-webview-with-native-mobile-engagement-android-sdk"></a>Bridge WebView Android com nativo Mobile Engagement SDK Android
> [!div class="op_single_selector"]
> * [Bridge de Android](mobile-engagement-bridge-webview-native-android.md)
> * [Bridge de iOS](mobile-engagement-bridge-webview-native-ios.md)
> 
> 

Algumas aplicações móveis são concebidas como uma aplicação híbrida onde Olá aplicação for desenvolvida utilizando a desenvolvimento do Android nativo, mas alguns ou mesmo todos os ecrãs Olá são compostos dentro de um WebView Android. Ainda pode consumir SDK Android do Mobile Engagement essas aplicações e este tutorial descreve como toogo sobre como fazê-lo. código de exemplo de Olá abaixo baseia-se no Olá documentação Android [aqui](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript). Descreve como esta abordagem documentada poderia ser utilizada tooimplement Olá mesmo para Android SDK do Mobile Engagement métodos de forma a que um Webview a partir de uma aplicação híbrida também pode iniciar pedidos tootrack eventos, tarefas, erros, as informações da aplicação ao encaminhando-los através do nosso SDK Android. 

1. Tem primeiro de tudo, tooensure que tenham passado por nossa [tutorial de introdução](mobile-engagement-android-get-started.md) toointegrate Olá SDK Android do Mobile Engagement na sua aplicação híbrida. Depois, fazê-lo, o `OnCreate` método terá um aspeto semelhante Olá seguinte.  
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("<Mobile Engagement Conn String>");
            EngagementAgent.getInstance(this).init(engagementConfiguration);
        }
2. Agora Certifique-se de que a aplicação híbrida tem um ecrã com um WebView. Olá código para a mesma será semelhante toohello seguinte onde iremos são carregar um ficheiro HTML local **Sample.html** no Olá Webview no Olá `onCreate` método do ecrã. 
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
        }
   
        protected void onCreate(Bundle savedInstanceState) {
            ...
            ...
            SetWebView();
        }
3. Agora crie um ficheiro de bridge chamado **WebAppInterface** que cria um wrapper através de alguns normalmente utilizadas métodos de SDK Android do Mobile Engagement com Olá `@JavascriptInterface` abordagem descrita no Olá [documentação Android ](https://developer.android.com/guide/webapps/webview.html#BindingJavaScript):
   
        import android.content.Context;
        import android.os.Bundle;
        import android.util.Log;
        import android.webkit.JavascriptInterface;
   
        import com.microsoft.azure.engagement.EngagementAgent;
   
        import org.json.JSONArray;
        import org.json.JSONObject;
   
        public class WebAppInterface {
            Context mContext;
   
            /** Instantiate hello interface and set hello context */
            WebAppInterface(Context c) {
                mContext = c;
            }
   
            @JavascriptInterface
            public void sendEngagementEvent(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendEvent(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void startEngagementJob(String name, String extras ){
                EngagementAgent.getInstance(mContext).startJob(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void endEngagementJob(String name){
                EngagementAgent.getInstance(mContext).endJob(name);
            }
   
            @JavascriptInterface
            public void sendEngagementError(String name, String extras ){
                EngagementAgent.getInstance(mContext).sendError(name, ParseExtras(extras));
            }
   
            @JavascriptInterface
            public void sendEngagementAppInfo(String appInfo){
                EngagementAgent.getInstance(mContext).sendAppInfo(ParseExtras(appInfo));
            }
   
            public Bundle ParseExtras(String input) {
                Bundle extras = new Bundle();
   
                try {
                    JSONObject jObject = new JSONObject(input);
                    extras.putString(jObject.names().getString(0),
                            jObject.get(jObject.names().getString(0)).toString());
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return extras;
            }
        }  
4. Assim que tiver criado Olá acima ficheiro bridge, precisamos tooensure que está associada a nossa Webview. Para este toohappen, terá de tooedit sua `SetWebview` método, para que as TI aspeto Olá seguinte:
   
        private void SetWebView() {
            WebView myWebView = (WebView) findViewById(R.id.webview);
            myWebView.loadUrl("file:///android_asset/Sample.html");
            WebSettings webSettings = myWebView.getSettings();
            webSettings.setJavaScriptEnabled(true);
            myWebView.addJavascriptInterface(new WebAppInterface(this), "EngagementJs");
        }
5. Olá acima fragmento, telefonámos `addJavascriptInterface` tooassociate nosso bridge de classe com o nosso Webview e também criou um identificador chamado **EngagementJs** métodos de Olá toocall do ficheiro de bridge de Olá. 
6. Agora criar Olá seguintes ficheiro chamado **Sample.html** no seu projeto numa pasta denominada **ativos** que é carregado na Olá Webview e onde que iremos chamar os métodos de Olá do ficheiro de bridge de Olá.
   
        <!doctype html>
        <html>
            <head>
                <style type='text/css'>
                    html { font-family:Helvetica; color:#222; }
                    h1 { color:steelblue; font-size:22px; margin-top:16px; }
                    h2 { color:grey; font-size:14px; margin-top:18px; margin-bottom:0px; }
                </style>
   
                <script type="text/javascript">
   
                    window.onerror = function(err)
                    {
                      log('window.onerror: ' + err);
                    }
   
                    send = function(inputId)
                    {
                        var input = document.getElementById(inputId);
                        if(input)
                        {
                            var value = input.value;
                            // Example of how extras info can be passed with hello Engagement logs
                            var extras = '{"CustomerId":"MS290011"}';
   
                            if(value && value.length > 0)
                            {
                                switch(inputId)
                                {
                                    case "event":
                                    EngagementJs.sendEngagementEvent(value, extras);
                                    break;
   
                                    case "job":
                                    EngagementJs.startEngagementJob(value, extras);
                                    window.setTimeout( function()
                                    {
                                      EngagementJs.endEngagementJob(value);
                                    }, 10000 );
                                    break;
   
                                    case "error":
                                    EngagementJs.sendEngagementError(value, extras);
                                    break;
   
                                    case "appInfo":
                                    EngagementJs.sendEngagementAppInfo({"customer_name":value});
                                    break;
                                }
                            }
                        }
                    }
                </script>
            </head>
            <body>
                <h1>Bridge Tester</h1>
                <div id='engagement'>
                    <h2>Event</h2>
                    <input type="text" id="event" size="35">
                    <button onclick="send('event')">Send</button>
   
                    <h2>Job</h2>
                    <input type="text" id="job" size="35">
                    <button onclick="send('job')">Send</button>
   
                    <h2>Error</h2>
                    <input type="text" id="error" size="35">
                    <button onclick="send('error')">Send</button>
   
                    <h2>AppInfo</h2>
                    <input type="text" id="appInfo" size="35">
                    <button onclick="send('appInfo')">Send</button>
                </div>
            </body>
        </html>
7. Pontos de seguinte de Olá nota sobre o ficheiro HTML Olá acima:
   
   * Contém um conjunto de caixas de entrada onde pode fornecer toobe de dados utilizada como nomes para o evento, a tarefa, o erro, a AppInfo. Ao clicar no Olá no botão seguinte tooit, é efetuada uma chamada toohello Javascript que acaba por métodos de chamadas Olá de Olá bridge ficheiro toopass toohello esta chamada de SDK Android do Mobile Engagement. 
   * Iremos são etiquetagem em alguns eventos de toohello estático informações adicionais, tarefas e até mesmo erros toodemonstrate como este pode ser efetuada. Estas informações adicionais são enviadas como um JSON de cadeia que, se procurar na Olá `WebAppInterface` de ficheiros, que é analisada e colocar um Android `Bundle` e é transmitido juntamente com o envio de eventos, tarefas, erros. 
   * Uma tarefa do Mobile Engagement é arrancou com o nome de Olá especificou na caixa de entrada Olá, executar para 10 segundos e encerrar. 
   * Uma etiqueta ou appinfo de Mobile Engagement é transmitida como chave estático Olá e o valor de Olá que introduziu na entrada de Olá como valor de Olá para tag Olá com 'customer_name'. 
8. Aplicação Olá execução e irá ver seguinte Olá. Agora, fornecer algum nome para um evento de teste como Olá seguintes e clique **enviar** abaixo do mesmo. 
   
    ![][1]
9. Agora que se vá toohello **Monitor** separador da sua aplicação e procure em **eventos-detalhes >**, irá ver este evento aparecer juntamente com Olá estático-as informações da aplicação que estamos a enviar. 
   
   ![][2]

<!-- Images. -->
[1]: ./media/mobile-engagement-bridge-webview-native-android/sending-event.png
[2]: ./media/mobile-engagement-bridge-webview-native-android/event-output.png
