---
title: "aaaBuild e implementar uma aplicação Java API no App Service do Azure"
description: "Saiba como toocreate uma aplicação Java API do pacote e implementá-la tooAzure do serviço de aplicações."
services: app-service\api
documentationcenter: java
author: rmcmurray
manager: erikre
editor: tdykstra
ms.assetid: 8d21ba5f-fc57-4269-bc8f-2fcab936ec22
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: get-started-article
ms.date: 04/25/2017
ms.author: rachelap;robmcm
ms.openlocfilehash: a4056fec870b1c4bed8ee14bb0e748b3ee89b9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a>Criar e implementar uma aplicação API Java no App Service do Azure
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Este tutorial mostra como toocreate uma aplicação Java e implementá-la tooAzure API Apps do App Service utilizando [Git]. Olá instruções deste tutorial podem ser seguidas em qualquer sistema operativo que seja capaz de executar Java. código de Olá neste tutorial é compilado com [Maven]. [Utilizando o JAX RS] é utilizado toocreate Olá serviço RESTful e é gerada com base no Olá [Swagger] especificação de metadados utilizando Olá [Swagger Editor].

## <a name="prerequisites"></a>Pré-requisitos
1. [Kit de Programação Java 8] \(ou posterior)
2. [Maven] instalado no seu computador de desenvolvimento
3. [Git] instalado no seu computador de desenvolvimento
4. Um paga ou [avaliação gratuita] subscrição demasiado[Microsoft Azure]
5. Um aplicação de teste HTTP como o [Postman]

## <a name="scaffold-hello-api-using-swaggerio"></a>Andaime Olá API utilizando o Swagger.IO
Utilizar o editor online do Olá swagger.io, pode introduzir código Swagger JSON ou YAML que representa a estrutura de Olá da sua API. Assim que tiver a área de superfície de API de Olá concebida, pode exportar código para uma variedade de plataformas e estruturas. Na secção seguinte, Olá, código de Olá estruturado será modificado tooinclude a funcionalidade mock. 

Esta demonstração irá começar com um corpo Swagger JSON irá colar no editor swagger.io de Olá, que será, em seguida, ser utilizados toogenerate código efetuar JAX RS tooaccess utiliza um ponto final de REST API. Em seguida, irá editar Olá estruturado código tooreturn dados mock, simulando uma API REST incorporada visível um mecanismo de persistência de dados.  

1. Copie Olá área de transferência de tooyour de código de Swagger JSON a seguir:
   
        {
            "swagger": "2.0",
            "info": {
                "version": "v1",
                "title": "Contact List",
                "description": "A Contact list API based on Swagger and built using Java"
            },
            "host": "localhost",
            "schemes": [
                "http",
                "https"
            ],
            "basePath": "/api",
            "paths": {
                "/contacts": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_get",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                },
                "/contacts/{id}": {
                    "get": {
                        "tags": [
                            "Contact"
                        ],
                        "operationId": "contacts_getById",
                        "consumes": [],
                        "produces": [
                            "application/json",
                            "text/json"
                        ],
                        "parameters": [
                            {
                                "name": "id",
                                "in": "path",
                                "required": true,
                                "type": "integer",
                                "format": "int32"
                            }
                        ],
                        "responses": {
                            "200": {
                                "description": "OK",
                                "schema": {
                                    "type": "array",
                                    "items": {
                                        "$ref": "#/definitions/Contact"
                                    }
                                }
                            }
                        },
                        "deprecated": false
                    }
                }
            },
            "definitions": {
                "Contact": {
                    "type": "object",
                    "properties": {
                        "Id": {
                            "format": "int32",
                            "type": "integer"
                        },
                        "Name": {
                            "type": "string"
                        },
                        "EmailAddress": {
                            "type": "string"
                        }
                    }
                }
            }
        }
2. Navegue toohello [Online Swagger Editor]. Uma vez, clique Olá **ficheiro -> colar JSON** item de menu.
   
    ![Colar item do menu JSON][paste-json]
3. Cole no Olá contactos lista Swagger JSON da API que copiou anteriormente. 
   
    ![Colar o código JSON no Swagger][pasted-swagger]
4. Ver resumo de API apresentados no editor de Olá e páginas de documentação de Olá. 
   
    ![Ver Documentos Gerados no Swagger][view-swagger-generated-docs]
5. Selecione Olá **gerar servidor -> JAX RS** as código de lado do servidor tooscaffold de opção do menu Olá irá editar posterior tooadd a implementação de mock. 
   
    ![Item do Menu Gerar Código][generate-code-menu-item]
   
    Depois do código de Olá é gerado, receberá um toodownload de ficheiro ZIP. Este ficheiro contém o código de Olá estruturado pelo gerador de código de Swagger Olá e todos os associados criar scripts. Deszipe o diretório de tooa de biblioteca na totalidade Olá na sua estação de trabalho de desenvolvimento. 

## <a name="edit-hello-code-tooadd-api-implementation"></a>Editar Olá código tooadd implementação de API
Nesta secção, irá substituir a implementação do Olá gerado pelo Swagger pelo código lado do servidor com o código personalizado. Step-by-Olá novo código irá devolver um cliente de chamada de toohello de entidades ArrayList de contacto. 

1. Abra Olá *Contact.java* ficheiro de modelo, que está localizado em Olá *src/gen/java/e/s/swagger/modelo* pasta, utilizando [Visual Studio Code] ou no seu editor de texto favorito. 
   
    ![Abrir Ficheiro de Modelo de Contacto][open-contact-model-file]
2. Adicionar Olá seguinte construtor dentro Olá **contacte** classe. 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. Abra Olá *ContactsApiServiceImpl.java* ficheiro de implementação de serviço, que está localizado em Olá *src/main/java/e/s/swagger/api/impl* pasta, utilizando [Visual Studio Code]ou no seu editor de texto favorito.
   
    ![Abrir Ficheiro de Código do Serviço de Contacto][open-contact-service-code-file]
4. Substitua o código de Olá no ficheiro de Olá com este novo tooadd de código um código do serviço toohello a implementação de mock. 
   
        package io.swagger.api.impl;
   
        import io.swagger.api.*;
        
        import io.swagger.model.Contact;
        import java.util.*;
        import io.swagger.api.NotFoundException;
               
        import javax.ws.rs.core.Response;
        import javax.ws.rs.core.SecurityContext;
   
        @javax.annotation.Generated(value = "class io.swagger.codegen.languages.JaxRSServerCodegen", date = "2015-11-24T21:54:11.648Z")
        public class ContactsApiServiceImpl extends ContactsApiService {
   
            private ArrayList<Contact> loadContacts()
            {
                ArrayList<Contact> list = new ArrayList<Contact>();
                list.add(new Contact(1, "Barney Poland", "barney@contoso.com"));
                list.add(new Contact(2, "Lacy Barrera", "lacy@contoso.com"));
                list.add(new Contact(3, "Lora Riggs", "lora@contoso.com"));
                return list;
            }
   
            @Override
            public Response contactsGet(SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                return Response.ok().entity(list).build();
                }
   
            @Override
            public Response contactsGetById(Integer id, SecurityContext securityContext)
            throws NotFoundException {
                ArrayList<Contact> list = loadContacts();
                Contact ret = null;
   
                for(int i=0; i<list.size(); i++)
                {
                    if(list.get(i).getId() == id)
                        {
                            ret = list.get(i);
                        }
                }
                return Response.ok().entity(ret).build();
            }
        }
5. Abra uma linha de comandos e altere o diretório toohello na pasta raiz da sua aplicação.
6. Executar Olá seguinte código do Maven comando toobuild Olá e executá-la utilizando Olá servidor da aplicação Jetty localmente. 
   
        mvn package jetty:run
7. Deverá ver a janela de comandos de Olá refletir que a aplicação Jetty iniciou o código na porta 8080. 
   
    ![Abrir Ficheiro de Código do Serviço de Contacto][run-jetty-war]
8. Utilize [Postman] toomake uma API "obter todos os contactos" do pedido toohello método em http://localhost:8080/api/contactos.
   
    ![Olá chamada API contactos][calling-contacts-api]
9. Utilize [Postman] toomake uma API "obter contacto específico" do pedido toohello método localizado em http://localhost:8080/api/contacts/2.
   
    ![Olá chamada API contactos][calling-specific-contact-api]
10. Por fim, crie o ficheiro de Java WAR (arquivo Web) Olá executando Olá seguinte comando Maven na sua consola. 
    
         mvn package war:war
11. Uma vez que é criado o ficheiro WAR de Olá, será colocado em Olá **destino** pasta. Navegue até à Olá **destino** pasta e mude o nome Olá ficheiro WAR demasiado**ROOT.war**. (Certifique-se de que corresponde a capitalização Olá este formato).
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. Por fim, execute Olá os seguintes comandos a partir da pasta de raiz de Olá do seu toocreate aplicação um **implementar** Olá de toodeploy pasta toouse WAR tooAzure de ficheiros. 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a>Publicar Olá tooAzure de saída do serviço de aplicações
Nesta secção, que irá aprender como toocreate uma nova aplicação API utilizando Olá Portal do Azure, preparar essa aplicação API para alojar aplicações Java e implementar Olá recentemente criado WAR ficheiro tooAzure toorun do serviço de aplicações, a nova aplicação API. 

1. Criar uma nova aplicação API no Olá [portal do Azure], clicando Olá **novo -> Web + Mobile -> aplicação API** item de menu, introduzindo os detalhes da aplicação e, em seguida, clicar em **criar**.
   
    ![Criar uma nova Aplicação API][create-api-app]
2. Quando tiver sido criada a sua aplicação API, abra a aplicação **definições** painel e, em seguida, clique em Olá **definições da aplicação** item de menu. Selecione Olá versões mais recentes do Java de opções disponíveis Olá, em seguida, selecione Olá Tomcat mais recente a partir de Olá **contentor Web** e, em seguida, clique em **guardar**.
   
    ![Configurar o Java no Olá painel aplicação API][set-up-java]
3. Clique em Olá **as credenciais de implementação** menu Definições do item e forneça um nome de utilizador e palavra-passe desejar toouse para publicar ficheiros tooyour aplicação API. 
   
    ![Definir credenciais de implementação][deployment-credentials]
4. Clique em Olá **origem de implementação** item de menu de definições. Uma vez, clique Olá **Escolher origem** botão, selecione de Olá **repositório de Git Local** opção e, em seguida, clique em **OK**. Esta ação cria um repositório de Git em execução no Azure, que tem uma associação à sua Aplicação API. Sempre que consolidar o código toohello *mestre* ramo do repositório de Git, o código será publicado na sua instância de aplicação API em execução em direto. 
   
    ![Configurar um novo repositório de Git no local][select-git-repo]
5. Copie a área de transferência do Olá novo repositório de Git URL tooyour. Guarde-o pois vai ser importante num determinado momento. 
   
    ![Configurar um novo repositório de Git para a sua aplicação][copy-git-repo-url]
6. Push Olá WAR ficheiro toohello online repositório de Git. toodo, navegue até à Olá **implementar** pasta que criou anteriormente para que possa facilmente consolidar o código de Olá segurança repositório de toohello em execução no seu serviço de aplicações. Uma vez que está na janela de consola Olá e navegar para a pasta de olá onde está localizada, a pasta de webapps Olá emitir Olá seguindo Git comandos toolaunch Olá processo e desativar uma implementação. 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    Assim que emite Olá **push** pedido, poderá ser-á pedido para palavra-passe de Olá que criou anteriormente para a credencial da implementação Olá. Depois de introduzir as suas credenciais, deverá ver o seu ecrã de portal Olá atualização foi implementada.
7. Se utilizar novamente o Postman toohit Olá recentemente implementada aplicação API em execução no App Service do Azure, verá que o comportamento de Olá é consistente e de que agora está a devolver dados de contacto conforme esperado e utilizar as alterações de código simples toohello Swagger.io código Java estruturado. 
   
    ![Utilizar a API REST dos Contactos do Java em direto no Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a>Passos seguintes
Neste artigo, só era possível toostart com um ficheiro Swagger JSON e algum código Java estruturado obtido a partir do editor Swagger.io de Olá. A partir daí, as suas alterações simples e um processo de implementação de Git resultou numa aplicação API funcional escrita em Java. tutorial de Olá seguinte mostra como demasiado[consumir API apps a partir de clientes JavaScript, utilizando a CORS][App Service API CORS]. Olá de tutoriais posteriores na série mostram como tooimplement autenticação e autorização.

toobuild esta amostra, pode saber mais sobre Olá [SDK de armazenamento para Java] blobs do toopersist Olá JSON. Em alternativa, pode utilizar Olá [Document DB Java SDK] toosave sua tooAzure de dados de contacto Document DB. 

<a name="see-also"></a>

## <a name="see-also"></a>Veja Também
Para obter mais informações sobre como utilizar o Azure com o Java, visite [Azure para programadores Java](/java/azure).

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[portal do Azure]: https://portal.azure.com/
[Document DB Java SDK]: ../documentdb/documentdb-java-application.md
[avaliação gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Kit de Programação Java 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Utilizando o JAX RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Online Swagger Editor]: http://editor2.swagger.io/
[Postman]: https://www.getpostman.com/
[SDK de armazenamento para Java]:../storage/blobs/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger Editor]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: ./media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: ./media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: ./media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: ./media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: ./media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: ./media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: ./media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: ./media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: ./media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: ./media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: ./media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: ./media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: ./media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: ./media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: ./media/app-service-api-java-api-app/postman-calling-azure-contacts.png
