---
title: Build and deploy a Java API app in Azure App Service
description: Learn how to create a Java API app package and deploy it to Azure App Service.
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
ms.date: 12/22/2016
ms.author: rachelap;robmcm
ms.openlocfilehash: 2f039d74f0c250fb3f200304d4c9ce76b16a1d78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661266"
---
# <a name="build-and-deploy-a-java-api-app-in-azure-app-service"></a><span data-ttu-id="a65a5-103">Build and deploy a Java API app in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a65a5-103">Build and deploy a Java API app in Azure App Service</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="a65a5-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span><span class="sxs-lookup"><span data-stu-id="a65a5-104">This tutorial shows how to create a Java application and deploy it to Azure App Service API Apps using [Git].</span></span> <span data-ttu-id="a65a5-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span><span class="sxs-lookup"><span data-stu-id="a65a5-105">The instructions in this tutorial can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="a65a5-106">The code in this tutorial is built using [Maven].</span><span class="sxs-lookup"><span data-stu-id="a65a5-106">The code in this tutorial is built using [Maven].</span></span> <span data-ttu-id="a65a5-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="a65a5-107">[Jax-RS] is used to create the RESTful Service, and is generated based on the [Swagger] metadata specification using the [Swagger Editor].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a65a5-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a65a5-108">Prerequisites</span></span>
1. <span data-ttu-id="a65a5-109">[Java Developer's Kit 8] \(or later)</span><span class="sxs-lookup"><span data-stu-id="a65a5-109">[Java Developer's Kit 8] \(or later)</span></span>
2. <span data-ttu-id="a65a5-110">[Maven] installed on your development machine</span><span class="sxs-lookup"><span data-stu-id="a65a5-110">[Maven] installed on your development machine</span></span>
3. <span data-ttu-id="a65a5-111">[Git] installed on your development machine</span><span class="sxs-lookup"><span data-stu-id="a65a5-111">[Git] installed on your development machine</span></span>
4. <span data-ttu-id="a65a5-112">A paid or [free trial] subscription to [Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="a65a5-112">A paid or [free trial] subscription to [Microsoft Azure]</span></span>
5. <span data-ttu-id="a65a5-113">An HTTP test application like [Postman]</span><span class="sxs-lookup"><span data-stu-id="a65a5-113">An HTTP test application like [Postman]</span></span>

## <a name="scaffold-the-api-using-swaggerio"></a><span data-ttu-id="a65a5-114">Scaffold the API using Swagger.IO</span><span class="sxs-lookup"><span data-stu-id="a65a5-114">Scaffold the API using Swagger.IO</span></span>
<span data-ttu-id="a65a5-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span><span class="sxs-lookup"><span data-stu-id="a65a5-115">Using the swagger.io online editor, you can enter Swagger JSON or YAML code representing the structure of your API.</span></span> <span data-ttu-id="a65a5-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span><span class="sxs-lookup"><span data-stu-id="a65a5-116">Once you have the API surface area designed, you can export code for a variety of platforms and frameworks.</span></span> <span data-ttu-id="a65a5-117">In the next section, the scaffolded code will be modified to include mock functionality.</span><span class="sxs-lookup"><span data-stu-id="a65a5-117">In the next section, the scaffolded code will be modified to include mock functionality.</span></span> 

<span data-ttu-id="a65a5-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span><span class="sxs-lookup"><span data-stu-id="a65a5-118">This demonstration will begin with a Swagger JSON body that you will paste into the swagger.io editor, which will then be used to generate code making use of JAX-RS to access a REST API endpoint.</span></span> <span data-ttu-id="a65a5-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span><span class="sxs-lookup"><span data-stu-id="a65a5-119">Then, you'll edit the scaffolded code to return mock data, simulating a REST API built atop a data persistence mechanism.</span></span>  

1. <span data-ttu-id="a65a5-120">Copy the following Swagger JSON code to your clipboard:</span><span class="sxs-lookup"><span data-stu-id="a65a5-120">Copy the following Swagger JSON code to your clipboard:</span></span>
   
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
2. <span data-ttu-id="a65a5-121">Navigate to the [Online Swagger Editor].</span><span class="sxs-lookup"><span data-stu-id="a65a5-121">Navigate to the [Online Swagger Editor].</span></span> <span data-ttu-id="a65a5-122">Once there, click the **File -> Paste JSON** menu item.</span><span class="sxs-lookup"><span data-stu-id="a65a5-122">Once there, click the **File -> Paste JSON** menu item.</span></span>
   
    ![Paste JSON menu item][paste-json]
3. <span data-ttu-id="a65a5-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="a65a5-124">Paste in the Contacts List API Swagger JSON you copied earlier.</span></span> 
   
    ![Pasting JSON code into Swagger][pasted-swagger]
4. <span data-ttu-id="a65a5-126">View the documentation pages and API summary rendered in the editor.</span><span class="sxs-lookup"><span data-stu-id="a65a5-126">View the documentation pages and API summary rendered in the editor.</span></span> 
   
    ![View Swagger Generated Docs][view-swagger-generated-docs]
5. <span data-ttu-id="a65a5-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span><span class="sxs-lookup"><span data-stu-id="a65a5-128">Select the **Generate Server -> JAX-RS** menu option to scaffold the server-side code you'll edit later to add mock implementation.</span></span> 
   
    ![Generate Code Menu Item][generate-code-menu-item]
   
    <span data-ttu-id="a65a5-130">Once the code is generated, you'll be provided a ZIP file to download.</span><span class="sxs-lookup"><span data-stu-id="a65a5-130">Once the code is generated, you'll be provided a ZIP file to download.</span></span> <span data-ttu-id="a65a5-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span><span class="sxs-lookup"><span data-stu-id="a65a5-131">This file contains the code scaffolded by the Swagger code generator and all associated build scripts.</span></span> <span data-ttu-id="a65a5-132">Unzip the entire library to a directory on your development workstation.</span><span class="sxs-lookup"><span data-stu-id="a65a5-132">Unzip the entire library to a directory on your development workstation.</span></span> 

## <a name="edit-the-code-to-add-api-implementation"></a><span data-ttu-id="a65a5-133">Edit the Code to add API Implementation</span><span class="sxs-lookup"><span data-stu-id="a65a5-133">Edit the Code to add API Implementation</span></span>
<span data-ttu-id="a65a5-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span><span class="sxs-lookup"><span data-stu-id="a65a5-134">In this section, you'll replace the Swagger-generated code's server-side implementation with your custom code.</span></span> <span data-ttu-id="a65a5-135">The new code will return an ArrayList of Contact entities to the calling client.</span><span class="sxs-lookup"><span data-stu-id="a65a5-135">The new code will return an ArrayList of Contact entities to the calling client.</span></span> 

1. <span data-ttu-id="a65a5-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="a65a5-136">Open the *Contact.java* model file, which is located in the *src/gen/java/io/swagger/model* folder, using [Visual Studio Code] or your favorite text editor.</span></span> 
   
    ![Open Contact Model File][open-contact-model-file]
2. <span data-ttu-id="a65a5-138">Add the following constructor to the **Contact** class.</span><span class="sxs-lookup"><span data-stu-id="a65a5-138">Add the following constructor to the **Contact** class.</span></span> 
   
        public Contact(Integer id, String name, String email) 
        {
            this.id = id;
            this.name = name;
            this.emailAddress = email;
        }
3. <span data-ttu-id="a65a5-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="a65a5-139">Open the *ContactsApiServiceImpl.java* service implementation file, which is located in the *src/main/java/io/swagger/api/impl* folder, using [Visual Studio Code] or your favorite text editor.</span></span>
   
    ![Open Contact Service Code File][open-contact-service-code-file]
4. <span data-ttu-id="a65a5-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span><span class="sxs-lookup"><span data-stu-id="a65a5-141">Overwrite the code in the file with this new code to add a mock implementation to the service code.</span></span> 
   
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
5. <span data-ttu-id="a65a5-142">Open a command prompt and change directory to the root folder of your application.</span><span class="sxs-lookup"><span data-stu-id="a65a5-142">Open a command prompt and change directory to the root folder of your application.</span></span>
6. <span data-ttu-id="a65a5-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span><span class="sxs-lookup"><span data-stu-id="a65a5-143">Execute the following Maven command to build the code and run it using the Jetty app server locally.</span></span> 
   
        mvn package jetty:run
7. <span data-ttu-id="a65a5-144">You should see the command window reflect that Jetty has started your code on port 8080.</span><span class="sxs-lookup"><span data-stu-id="a65a5-144">You should see the command window reflect that Jetty has started your code on port 8080.</span></span> 
   
    ![Open Contact Service Code File][run-jetty-war]
8. <span data-ttu-id="a65a5-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="a65a5-146">Use [Postman] to make a request to the "get all contacts" API method at http://localhost:8080/api/contacts.</span></span>
   
    ![Call the Contacts API][calling-contacts-api]
9. <span data-ttu-id="a65a5-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span><span class="sxs-lookup"><span data-stu-id="a65a5-148">Use [Postman] to make a request to the "get specific contact" API method located at http://localhost:8080/api/contacts/2.</span></span>
   
    ![Call the Contacts API][calling-specific-contact-api]
10. <span data-ttu-id="a65a5-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span><span class="sxs-lookup"><span data-stu-id="a65a5-150">Finally, build the Java WAR (Web ARchive) file by executing the following Maven command in your console.</span></span> 
    
         mvn package war:war
11. <span data-ttu-id="a65a5-151">Once the WAR file is built, it will be placed into the **target** folder.</span><span class="sxs-lookup"><span data-stu-id="a65a5-151">Once the WAR file is built, it will be placed into the **target** folder.</span></span> <span data-ttu-id="a65a5-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span><span class="sxs-lookup"><span data-stu-id="a65a5-152">Navigate into the **target** folder and rename the WAR file to **ROOT.war**.</span></span> <span data-ttu-id="a65a5-153">(Make sure the capitalization matches this format).</span><span class="sxs-lookup"><span data-stu-id="a65a5-153">(Make sure the capitalization matches this format).</span></span>
    
          rename swagger-jaxrs-server-1.0.0.war ROOT.war
12. <span data-ttu-id="a65a5-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span><span class="sxs-lookup"><span data-stu-id="a65a5-154">Finally, execute the following commands from the root folder of your application to create a **deploy** folder to use to deploy the WAR file to Azure.</span></span> 
    
          mkdir deploy
          mkdir deploy\webapps
          copy target\ROOT.war deploy\webapps
          cd deploy

## <a name="publish-the-output-to-azure-app-service"></a><span data-ttu-id="a65a5-155">Publish the output to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a65a5-155">Publish the output to Azure App Service</span></span>
<span data-ttu-id="a65a5-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span><span class="sxs-lookup"><span data-stu-id="a65a5-156">In this section you'll learn how to create a new API App using the Azure Portal, prepare that API App for hosting Java applications, and deploy the newly-created WAR file to Azure App Service to run your new API App.</span></span> 

1. <span data-ttu-id="a65a5-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span><span class="sxs-lookup"><span data-stu-id="a65a5-157">Create a new API app in the [Azure portal], by clicking the **New -> Web + Mobile -> API app** menu item, entering your app details, and then clicking **Create**.</span></span>
   
    ![Create a new API App][create-api-app]
2. <span data-ttu-id="a65a5-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span><span class="sxs-lookup"><span data-stu-id="a65a5-159">Once your API app has been created, open your app's **Settings** blade, and then click the **Application settings** menu item.</span></span> <span data-ttu-id="a65a5-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a65a5-160">Select the latest Java versions from the available options, then select the latest Tomcat from the **Web container** menu, and then click **Save**.</span></span>
   
    ![Set up Java in the API App blade][set-up-java]
3. <span data-ttu-id="a65a5-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span><span class="sxs-lookup"><span data-stu-id="a65a5-162">Click the **Deployment credentials** settings menu item, and provide a username and password you wish to use for publishing files to your API App.</span></span> 
   
    ![Set deployment credentials][deployment-credentials]
4. <span data-ttu-id="a65a5-164">Click the **Deployment source** settings menu item.</span><span class="sxs-lookup"><span data-stu-id="a65a5-164">Click the **Deployment source** settings menu item.</span></span> <span data-ttu-id="a65a5-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a65a5-165">Once there, click the **Choose source** button, select the **Local Git Repository** option, and then click **OK**.</span></span> <span data-ttu-id="a65a5-166">This will create a Git repository running in Azure, that has an association with your API App.</span><span class="sxs-lookup"><span data-stu-id="a65a5-166">This will create a Git repository running in Azure, that has an association with your API App.</span></span> <span data-ttu-id="a65a5-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span><span class="sxs-lookup"><span data-stu-id="a65a5-167">Each time you commit code to the *master* branch of your Git repository, your code will be published into your live running API App instance.</span></span> 
   
    ![Set up a new local Git repository][select-git-repo]
5. <span data-ttu-id="a65a5-169">Copy the new Git repository's URL to your clipboard.</span><span class="sxs-lookup"><span data-stu-id="a65a5-169">Copy the new Git repository's URL to your clipboard.</span></span> <span data-ttu-id="a65a5-170">Save this as it will be important in a moment.</span><span class="sxs-lookup"><span data-stu-id="a65a5-170">Save this as it will be important in a moment.</span></span> 
   
    ![Set up a new Git repository for your app][copy-git-repo-url]
6. <span data-ttu-id="a65a5-172">Git push the WAR file to the online repository.</span><span class="sxs-lookup"><span data-stu-id="a65a5-172">Git push the WAR file to the online repository.</span></span> <span data-ttu-id="a65a5-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span><span class="sxs-lookup"><span data-stu-id="a65a5-173">To do this, navigate into the **deploy** folder you created earlier so that you can easily commit the code up to the repository running in your App Service.</span></span> <span data-ttu-id="a65a5-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span><span class="sxs-lookup"><span data-stu-id="a65a5-174">Once you're in the console window and navigated into the folder where the webapps folder is located, issue the following Git commands to launch the process and fire off a deployment.</span></span> 
   
         git init
         git add .
         git commit -m "initial commit"
         git remote add azure [YOUR GIT URL]
         git push azure master
   
    <span data-ttu-id="a65a5-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span><span class="sxs-lookup"><span data-stu-id="a65a5-175">Once you issue the **push** request, you'll be asked for the password you created for the deployment credential earlier.</span></span> <span data-ttu-id="a65a5-176">After you enter your credentials, you should see your portal display that the update was deployed.</span><span class="sxs-lookup"><span data-stu-id="a65a5-176">After you enter your credentials, you should see your portal display that the update was deployed.</span></span>
7. <span data-ttu-id="a65a5-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span><span class="sxs-lookup"><span data-stu-id="a65a5-177">If you once again use Postman to hit the newly-deployed API App running in Azure App Service, you'll see that the behavior is consistent and that now it is returning contact data as expected, and using simple code changes to the Swagger.io scaffolded Java code.</span></span> 
   
    ![Using your Java Contacts REST API live in Azure][postman-calling-azure-contacts]

## <a name="next-steps"></a><span data-ttu-id="a65a5-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="a65a5-179">Next steps</span></span>
<span data-ttu-id="a65a5-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span><span class="sxs-lookup"><span data-stu-id="a65a5-180">In this article, you were able to start with a Swagger JSON file and some scaffolded Java code obtained from the Swagger.io editor.</span></span> <span data-ttu-id="a65a5-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span><span class="sxs-lookup"><span data-stu-id="a65a5-181">From there, your simple changes and a Git deploy process resulted in having a functional API app written in Java.</span></span> <span data-ttu-id="a65a5-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span><span class="sxs-lookup"><span data-stu-id="a65a5-182">The next tutorial shows how to [consume API apps from JavaScript clients, using CORS][App Service API CORS].</span></span> <span data-ttu-id="a65a5-183">Later tutorials in the series show how to implement authentication and authorization.</span><span class="sxs-lookup"><span data-stu-id="a65a5-183">Later tutorials in the series show how to implement authentication and authorization.</span></span>

<span data-ttu-id="a65a5-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span><span class="sxs-lookup"><span data-stu-id="a65a5-184">To build on this sample, you can learn more about the [Storage SDK for Java] to persist the JSON blobs.</span></span> <span data-ttu-id="a65a5-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span><span class="sxs-lookup"><span data-stu-id="a65a5-185">Or, you could use the [Document DB Java SDK] to save your Contact data to Azure Document DB.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="a65a5-186">See Also</span><span class="sxs-lookup"><span data-stu-id="a65a5-186">See Also</span></span>
<span data-ttu-id="a65a5-187">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="a65a5-187">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

[App Service API CORS]: app-service-api-cors-consume-javascript.md
[Azure portal]: https://portal.azure.com/
[Document DB Java SDK]: ../documentdb/documentdb-java-application.md
[free trial]: https://azure.microsoft.com/pricing/free-trial/
[Git]: http://www.git-scm.com/
[Azure Java Developer Center]: /develop/java/
[Java Developer's Kit 8]: http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
[Jax-RS]: https://jax-rs-spec.java.net/
[Maven]: https://maven.apache.org/
[Microsoft Azure]: https://azure.microsoft.com/
[Online Swagger Editor]: http://editor.swagger.io/
[Postman]: https://www.getpostman.com/
[Storage SDK for Java]: ../storage/storage-java-how-to-use-blob-storage.md
[Swagger]: http://swagger.io/
[Swagger Editor]: http://editor.swagger.io/
[Visual Studio Code]: https://code.visualstudio.com

<!-- IMG List -->

[paste-json]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/paste-json.png
[pasted-swagger]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/pasted-swagger.png
[view-swagger-generated-docs]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/view-swagger-generated-docs.png
[generate-code-menu-item]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/generate-code-menu-item.png
[open-contact-model-file]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/open-contact-model-file.png
[open-contact-service-code-file]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/open-contact-service-code-file.png
[run-jetty-war]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/run-jetty-war.png
[calling-contacts-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/calling-contacts-api.png
[calling-specific-contact-api]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/calling-specific-contact-api.png
[create-api-app]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/create-api-app.png
[set-up-java]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/set-up-java.png
[deployment-credentials]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/deployment-credentials.png
[select-git-repo]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/select-git-repo.png
[copy-git-repo-url]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/copy-git-repo-url.png
[postman-calling-azure-contacts]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-java-api-app/postman-calling-azure-contacts.png















