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
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="d1373-103">Criar e implementar uma aplicação API Java no App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="d1373-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="d1373-104">Este tutorial mostra como toocreate uma aplicação Java e implementá-la tooAzure API Apps do App Service utilizando [Git].</span><span class="sxs-lookup"><span data-stu-id="d1373-104">This tutorial shows how toocreate a Java application and deploy it tooAzure App Service API Apps using [Git].</span></span> <span data-ttu-id="d1373-105">Olá instruções deste tutorial podem ser seguidas em qualquer sistema operativo que seja capaz de executar Java.</span><span class="sxs-lookup"><span data-stu-id="d1373-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="d1373-106">código de Olá neste tutorial é compilado com [Maven].</span><span class="sxs-lookup"><span data-stu-id="d1373-106">hello code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="d1373-107">[Utilizando o JAX RS] é utilizado toocreate Olá serviço RESTful e é gerada com base no Olá [Swagger] especificação de metadados utilizando Olá [Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="d1373-107">[Jax-RS] is used toocreate hello RESTful Service, and is generated based on hello [Swagger] metadata specification using hello [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1373-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d1373-108">Prerequisites</span></span>
1. <span data-ttu-id="d1373-109">[Kit de Programação Java 8] \(ou posterior)</span><span class="sxs-lookup"><span data-stu-id="d1373-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="d1373-110">[Maven] instalado no seu computador de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d1373-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="d1373-111">[Git] instalado no seu computador de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="d1373-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="d1373-112">Um paga ou [avaliação gratuita] subscrição demasiado[Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="d1373-112">A paid or [free trial] subscription too[Microsoft Azure]</span></span>
5. <span data-ttu-id="d1373-113">Um aplicação de teste HTTP como o [Postman]</span><span class="sxs-lookup"><span data-stu-id="d1373-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-hello-api-using-swaggerio"></a><span data-ttu-id="d1373-114">Andaime Olá API utilizando o Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="d1373-114">Scaffold hello API using Swagger.IO</span></span>
<span data-ttu-id="d1373-115">Utilizar o editor online do Olá swagger.io, pode introduzir código Swagger JSON ou YAML que representa a estrutura de Olá da sua API.</span><span class="sxs-lookup"><span data-stu-id="d1373-115">Using hello swagger.io online editor, you can enter Swagger JSON or YAML code representing hello structure of your API.</span></span> <span data-ttu-id="d1373-116">Assim que tiver a área de superfície de API de Olá concebida, pode exportar código para uma variedade de plataformas e estruturas.</span><span class="sxs-lookup"><span data-stu-id="d1373-116">Once you have hello API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="d1373-117">Na secção seguinte, Olá, código de Olá estruturado será modificado tooinclude a funcionalidade mock.</span><span class="sxs-lookup"><span data-stu-id="d1373-117">In hello next section, hello scaffolded code will be modified tooinclude mock functionality.</span></span> 

<span data-ttu-id="d1373-118">Esta demonstração irá começar com um corpo Swagger JSON irá colar no editor swagger.io de Olá, que será, em seguida, ser utilizados toogenerate código efetuar JAX RS tooaccess utiliza um ponto final de REST API.</span><span class="sxs-lookup"><span data-stu-id="d1373-118">This demonstration will begin with a Swagger JSON body that you will paste into hello swagger.io editor, which will then be used toogenerate code making use of JAX-RS tooaccess a REST API endpoint.</span></span> <span data-ttu-id="d1373-119">Em seguida, irá editar Olá estruturado código tooreturn dados mock, simulando uma API REST incorporada visível um mecanismo de persistência de dados.</span><span class="sxs-lookup"><span data-stu-id="d1373-119">Then, you'll edit hello scaffolded code tooreturn mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="d1373-120">Copie Olá área de transferência de tooyour de código de Swagger JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1373-120">Copy hello following Swagger JSON code tooyour clipboard:</span></span>
   
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
2. <span data-ttu-id="d1373-121">Navegue toohello [Online Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="d1373-121">Navigate toohello [Online Swagger Editor].</span></span> <span data-ttu-id="d1373-122">Uma vez, clique Olá **ficheiro -> colar JSON** item de menu.</span><span class="sxs-lookup"><span data-stu-id="d1373-122">Once there, click hello **File -> Paste JSON** menu item.</span></span>
   
    ![Colar item do menu JSON][paste-json]
3. <span data-ttu-id="d1373-124">Cole no Olá contactos lista Swagger JSON da API que copiou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d1373-124">Paste in hello Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Colar o código JSON no Swagger][pasted-swagger]
4. <span data-ttu-id="d1373-126">Ver resumo de API apresentados no editor de Olá e páginas de documentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1373-126">View hello documentation pages and API summary rendered in hello editor.</span></span> 
   
    ![Ver Documentos Gerados no Swagger][view-swagger-generated-docs]
5. <span data-ttu-id="d1373-128">Selecione Olá **gerar servidor -> JAX RS** as código de lado do servidor tooscaffold de opção do menu Olá irá editar posterior tooadd a implementação de mock.</span><span class="sxs-lookup"><span data-stu-id="d1373-128">Select hello **Generate Server -> JAX-RS** menu option tooscaffold hello server-side code you'll edit later tooadd mock implementation.</span></span> 
   
    ![Item do Menu Gerar Código][generate-code-menu-item]
   
    <span data-ttu-id="d1373-130">Depois do código de Olá é gerado, receberá um toodownload de ficheiro ZIP.</span><span class="sxs-lookup"><span data-stu-id="d1373-130">Once hello code is generated, you'll be provided a ZIP file toodownload.</span></span> <span data-ttu-id="d1373-131">Este ficheiro contém o código de Olá estruturado pelo gerador de código de Swagger Olá e todos os associados criar scripts.</span><span class="sxs-lookup"><span data-stu-id="d1373-131">This file contains hello code scaffolded by hello Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="d1373-132">Deszipe o diretório de tooa de biblioteca na totalidade Olá na sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d1373-132">Unzip hello entire library tooa directory on your development workstation.</span></span> 

## <a name="edit-hello-code-tooadd-api-implementation"></a><span data-ttu-id="d1373-133">Editar Olá código tooadd implementação de API</span><span class="sxs-lookup"><span data-stu-id="d1373-133">Edit hello Code tooadd API Implementation</span></span>
<span data-ttu-id="d1373-134">Nesta secção, irá substituir a implementação do Olá gerado pelo Swagger pelo código lado do servidor com o código personalizado.</span><span class="sxs-lookup"><span data-stu-id="d1373-134">In this section, you'll replace hello Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="d1373-135">Step-by-Olá novo código irá devolver um cliente de chamada de toohello de entidades ArrayList de contacto.</span><span class="sxs-lookup"><span data-stu-id="d1373-135">hello new code will return an ArrayList of Contact entities toohello calling client.</span></span> 

1. <span data-ttu-id="d1373-136">Abra Olá *Contact.java* ficheiro de modelo, que está localizado em Olá *src/gen/java/e/s/swagger/modelo* pasta, utilizando [Visual Studio Code] ou no seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="d1373-136">Open hello *Contact.java* model file, which is located in hello *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Abrir Ficheiro de Modelo de Contacto][open-contact-model-file]
2. <span data-ttu-id="d1373-138">Adicionar Olá seguinte construtor dentro Olá **contacte** classe.</span><span class="sxs-lookup"><span data-stu-id="d1373-138">Add hello following constructor within hello **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="d1373-139">Abra Olá *ContactsApiServiceImpl.java* ficheiro de implementação de serviço, que está localizado em Olá *src/main/java/e/s/swagger/api/impl* pasta, utilizando [Visual Studio Code]ou no seu editor de texto favorito.</span><span class="sxs-lookup"><span data-stu-id="d1373-139">Open hello *ContactsApiServiceImpl.java* service implementation file, which is located in hello *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Abrir Ficheiro de Código do Serviço de Contacto][open-contact-service-code-file]
4. <span data-ttu-id="d1373-141">Substitua o código de Olá no ficheiro de Olá com este novo tooadd de código um código do serviço toohello a implementação de mock.</span><span class="sxs-lookup"><span data-stu-id="d1373-141">Overwrite hello code in hello file with this new code tooadd a mock implementation toohello service code.</span></span> 
   
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
5. <span data-ttu-id="d1373-142">Abra uma linha de comandos e altere o diretório toohello na pasta raiz da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="d1373-142">Open a command prompt and change directory toohello root folder of your application.</span></span>
6. <span data-ttu-id="d1373-143">Executar Olá seguinte código do Maven comando toobuild Olá e executá-la utilizando Olá servidor da aplicação Jetty localmente.</span><span class="sxs-lookup"><span data-stu-id="d1373-143">Execute hello following Maven command toobuild hello code and run it using hello Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="d1373-144">Deverá ver a janela de comandos de Olá refletir que a aplicação Jetty iniciou o código na porta 8080.</span><span class="sxs-lookup"><span data-stu-id="d1373-144">You should see hello command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Abrir Ficheiro de Código do Serviço de Contacto][run-jetty-war]
8. <span data-ttu-id="d1373-146">Utilize [Postman] toomake uma API "obter todos os contactos" do pedido toohello método em http://localhost:8080/api/contactos.</span><span class="sxs-lookup"><span data-stu-id="d1373-146">Use [Postman] toomake a request toohello "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Olá chamada API contactos][calling-contacts-api]
9. <span data-ttu-id="d1373-148">Utilize [Postman] toomake uma API "obter contacto específico" do pedido toohello método localizado em http://localhost:8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="d1373-148">Use [Postman] toomake a request toohello "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Olá chamada API contactos][calling-specific-contact-api]
10. <span data-ttu-id="d1373-150">Por fim, crie o ficheiro de Java WAR (arquivo Web) Olá executando Olá seguinte comando Maven na sua consola.</span><span class="sxs-lookup"><span data-stu-id="d1373-150">Finally, build hello Java WAR (Web ARchive) file by executing hello following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="d1373-151">Uma vez que é criado o ficheiro WAR de Olá, será colocado em Olá **destino** pasta.</span><span class="sxs-lookup"><span data-stu-id="d1373-151">Once hello WAR file is built, it will be placed into hello **target** folder.</span></span> <span data-ttu-id="d1373-152">Navegue até à Olá **destino** pasta e mude o nome Olá ficheiro WAR demasiado**ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="d1373-152">Navigate into hello **target** folder and rename hello WAR file too**ROOT.war**.</span></span> <span data-ttu-id="d1373-153">(Certifique-se de que corresponde a capitalização Olá este formato).</span><span class="sxs-lookup"><span data-stu-id="d1373-153">(Make sure hello capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="d1373-154">Por fim, execute Olá os seguintes comandos a partir da pasta de raiz de Olá do seu toocreate aplicação um **implementar** Olá de toodeploy pasta toouse WAR tooAzure de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="d1373-154">Finally, execute hello following commands from hello root folder of your application toocreate a **deploy** folder toouse toodeploy hello WAR file tooAzure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-hello-output-tooazure-app-service"></a><span data-ttu-id="d1373-155">Publicar Olá tooAzure de saída do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="d1373-155">Publish hello output tooAzure App Service</span></span>
<span data-ttu-id="d1373-156">Nesta secção, que irá aprender como toocreate uma nova aplicação API utilizando Olá Portal do Azure, preparar essa aplicação API para alojar aplicações Java e implementar Olá recentemente criado WAR ficheiro tooAzure toorun do serviço de aplicações, a nova aplicação API.</span><span class="sxs-lookup"><span data-stu-id="d1373-156">In this section you'll learn how toocreate a new API App using hello Azure Portal, prepare that API App for hosting Java applications, and deploy hello newly-created WAR file tooAzure App Service toorun your new API App.</span></span> 

1. <span data-ttu-id="d1373-157">Criar uma nova aplicação API no Olá [portal do Azure], clicando Olá **novo -> Web + Mobile -> aplicação API** item de menu, introduzindo os detalhes da aplicação e, em seguida, clicar em **criar**.</span><span class="sxs-lookup"><span data-stu-id="d1373-157">Create a new API app in hello [Azure portal], by clicking hello **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Criar uma nova Aplicação API][create-api-app]
2. <span data-ttu-id="d1373-159">Quando tiver sido criada a sua aplicação API, abra a aplicação **definições** painel e, em seguida, clique em Olá **definições da aplicação** item de menu.</span><span class="sxs-lookup"><span data-stu-id="d1373-159">Once your API app has been created, open your app's **Settings** blade, and then click hello **Application settings** menu item.</span></span> <span data-ttu-id="d1373-160">Selecione Olá versões mais recentes do Java de opções disponíveis Olá, em seguida, selecione Olá Tomcat mais recente a partir de Olá **contentor Web** e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d1373-160">Select hello latest Java versions from hello available options, then select hello latest Tomcat from hello **Web container** menu, and then click **Save**.</span></span>
   
    ![Configurar o Java no Olá painel aplicação API][set-up-java]
3. <span data-ttu-id="d1373-162">Clique em Olá **as credenciais de implementação** menu Definições do item e forneça um nome de utilizador e palavra-passe desejar toouse para publicar ficheiros tooyour aplicação API.</span><span class="sxs-lookup"><span data-stu-id="d1373-162">Click hello **Deployment credentials** settings menu item, and provide a username and password you wish toouse for publishing files tooyour API App.</span></span> 
   
    ![Definir credenciais de implementação][deployment-credentials]
4. <span data-ttu-id="d1373-164">Clique em Olá **origem de implementação** item de menu de definições.</span><span class="sxs-lookup"><span data-stu-id="d1373-164">Click hello **Deployment source** settings menu item.</span></span> <span data-ttu-id="d1373-165">Uma vez, clique Olá **Escolher origem** botão, selecione de Olá **repositório de Git Local** opção e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1373-165">Once there, click hello **Choose source** button, select hello **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="d1373-166">Esta ação cria um repositório de Git em execução no Azure, que tem uma associação à sua Aplicação API.</span><span class="sxs-lookup"><span data-stu-id="d1373-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="d1373-167">Sempre que consolidar o código toohello *mestre* ramo do repositório de Git, o código será publicado na sua instância de aplicação API em execução em direto.</span><span class="sxs-lookup"><span data-stu-id="d1373-167">Each time you commit code toohello *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Configurar um novo repositório de Git no local][select-git-repo]
5. <span data-ttu-id="d1373-169">Copie a área de transferência do Olá novo repositório de Git URL tooyour.</span><span class="sxs-lookup"><span data-stu-id="d1373-169">Copy hello new Git repository's URL tooyour clipboard.</span></span> <span data-ttu-id="d1373-170">Guarde-o pois vai ser importante num determinado momento.</span><span class="sxs-lookup"><span data-stu-id="d1373-170">Save this as it will be important in a moment.</span></span> 
   
    ![Configurar um novo repositório de Git para a sua aplicação][copy-git-repo-url]
6. <span data-ttu-id="d1373-172">Push Olá WAR ficheiro toohello online repositório de Git.</span><span class="sxs-lookup"><span data-stu-id="d1373-172">Git push hello WAR file toohello online repository.</span></span> <span data-ttu-id="d1373-173">toodo, navegue até à Olá **implementar** pasta que criou anteriormente para que possa facilmente consolidar o código de Olá segurança repositório de toohello em execução no seu serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="d1373-173">toodo this, navigate into hello **deploy** folder you created earlier so that you can easily commit hello code up toohello repository running in your App Service.</span></span> <span data-ttu-id="d1373-174">Uma vez que está na janela de consola Olá e navegar para a pasta de olá onde está localizada, a pasta de webapps Olá emitir Olá seguindo Git comandos toolaunch Olá processo e desativar uma implementação.</span><span class="sxs-lookup"><span data-stu-id="d1373-174">Once you're in hello console window and navigated into hello folder where hello webapps folder is located, issue hello following Git commands toolaunch hello process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="d1373-175">Assim que emite Olá **push** pedido, poderá ser-á pedido para palavra-passe de Olá que criou anteriormente para a credencial da implementação Olá.</span><span class="sxs-lookup"><span data-stu-id="d1373-175">Once you issue hello **push** request, you'll be asked for hello password you created for hello deployment credential earlier.</span></span> <span data-ttu-id="d1373-176">Depois de introduzir as suas credenciais, deverá ver o seu ecrã de portal Olá atualização foi implementada.</span><span class="sxs-lookup"><span data-stu-id="d1373-176">After you enter your credentials, you should see your portal display that hello update was deployed.</span></span>
7. <span data-ttu-id="d1373-177">Se utilizar novamente o Postman toohit Olá recentemente implementada aplicação API em execução no App Service do Azure, verá que o comportamento de Olá é consistente e de que agora está a devolver dados de contacto conforme esperado e utilizar as alterações de código simples toohello Swagger.io código Java estruturado.</span><span class="sxs-lookup"><span data-stu-id="d1373-177">If you once again use Postman toohit hello newly-deployed API App running in Azure App Service, you'll see that hello behavior is consistent and that now it is returning contact data as expected, and using simple code changes toohello Swagger.io scaffolded Java code.</span></span> 
   
    ![Utilizar a API REST dos Contactos do Java em direto no Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="d1373-179">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d1373-179">Next steps</span></span>
<span data-ttu-id="d1373-180">Neste artigo, só era possível toostart com um ficheiro Swagger JSON e algum código Java estruturado obtido a partir do editor Swagger.io de Olá.</span><span class="sxs-lookup"><span data-stu-id="d1373-180">In this article, you were able toostart with a Swagger JSON file and some scaffolded Java code obtained from hello Swagger.io editor.</span></span> <span data-ttu-id="d1373-181">A partir daí, as suas alterações simples e um processo de implementação de Git resultou numa aplicação API funcional escrita em Java.</span><span class="sxs-lookup"><span data-stu-id="d1373-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="d1373-182">tutorial de Olá seguinte mostra como demasiado[consumir API apps a partir de clientes JavaScript, utilizando a CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="d1373-182">hello next tutorial shows how too[consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="d1373-183">Olá de tutoriais posteriores na série mostram como tooimplement autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="d1373-183">Later tutorials in hello series show how tooimplement authentication and authorization.</span></span>

<span data-ttu-id="d1373-184">toobuild esta amostra, pode saber mais sobre Olá [SDK de armazenamento para Java] blobs do toopersist Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="d1373-184">toobuild on this sample, you can learn more about hello [Storage SDK for Java] toopersist hello JSON blobs.</span></span> <span data-ttu-id="d1373-185">Em alternativa, pode utilizar Olá [Document DB Java SDK] toosave sua tooAzure de dados de contacto Document DB.</span><span class="sxs-lookup"><span data-stu-id="d1373-185">Or, you could use hello [Document DB Java SDK] toosave your Contact data tooAzure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="d1373-186">Veja Também</span><span class="sxs-lookup"><span data-stu-id="d1373-186">See Also</span></span>
<span data-ttu-id="d1373-187">Para obter mais informações sobre como utilizar o Azure com o Java, visite [Azure para programadores Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="d1373-187">For more information about using Azure with Java, visit [Azure for Java developers](/java/azure).</span></span>

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
