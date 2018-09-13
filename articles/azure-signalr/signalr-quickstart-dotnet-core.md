---
title: Quickstart to learn how to use Azure SignalR Service | Microsoft Docs
description: A quickstart for using Azure SignalR Service to create a chat room with ASP.NET Core MVC apps.
services: signalr
documentationcenter: ''
author: sffamily
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: signalr
ms.devlang: dotnet
ms.topic: quickstart
ms.tgt_pltfrm: ASP.NET
ms.workload: tbd
ms.date: 06/13/2018
ms.author: zhshang
ms.openlocfilehash: 398ba001bfe9c8b2dd77b66535f5cb4aaf5f6270
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868301"
---
# <a name="quickstart-create-a-chat-room-with-signalr-service"></a><span data-ttu-id="66b7f-103">Quickstart: Create a chat room with SignalR Service</span><span class="sxs-lookup"><span data-stu-id="66b7f-103">Quickstart: Create a chat room with SignalR Service</span></span>

<span data-ttu-id="66b7f-104">Microsoft Azure SignalR Service is currently in [Public Preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="66b7f-104">Microsoft Azure SignalR Service is currently in [Public Preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>

<span data-ttu-id="66b7f-105">Azure SignalR Service is an Azure service that helps developers easily build web applications with real-time features.</span><span class="sxs-lookup"><span data-stu-id="66b7f-105">Azure SignalR Service is an Azure service that helps developers easily build web applications with real-time features.</span></span> <span data-ttu-id="66b7f-106">This service is based on [SignalR for ASP.NET Core 2.0](https://docs.microsoft.com/aspnet/core/signalr/introduction).</span><span class="sxs-lookup"><span data-stu-id="66b7f-106">This service is based on [SignalR for ASP.NET Core 2.0](https://docs.microsoft.com/aspnet/core/signalr/introduction).</span></span>

<span data-ttu-id="66b7f-107">This article shows you how to get started with the Azure SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="66b7f-107">This article shows you how to get started with the Azure SignalR Service.</span></span> <span data-ttu-id="66b7f-108">In this quickstart, you will create a chat application using an ASP.NET Core MVC Web App web app.</span><span class="sxs-lookup"><span data-stu-id="66b7f-108">In this quickstart, you will create a chat application using an ASP.NET Core MVC Web App web app.</span></span> <span data-ttu-id="66b7f-109">This app will make a connection with your Azure SignalR Service resource to enable real-time content updates.</span><span class="sxs-lookup"><span data-stu-id="66b7f-109">This app will make a connection with your Azure SignalR Service resource to enable real-time content updates.</span></span> <span data-ttu-id="66b7f-110">You will host the web application locally and connect with multiple browser clients.</span><span class="sxs-lookup"><span data-stu-id="66b7f-110">You will host the web application locally and connect with multiple browser clients.</span></span> <span data-ttu-id="66b7f-111">Each client will be able to push content updates to all other clients.</span><span class="sxs-lookup"><span data-stu-id="66b7f-111">Each client will be able to push content updates to all other clients.</span></span> 


<span data-ttu-id="66b7f-112">You can use any code editor to complete the steps in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="66b7f-112">You can use any code editor to complete the steps in this quickstart.</span></span> <span data-ttu-id="66b7f-113">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="66b7f-113">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span></span>

<span data-ttu-id="66b7f-114">The code for this tutorial is available for download in the [AzureSignalR-samples GitHub repository](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/ChatRoom).</span><span class="sxs-lookup"><span data-stu-id="66b7f-114">The code for this tutorial is available for download in the [AzureSignalR-samples GitHub repository](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/ChatRoom).</span></span>  <span data-ttu-id="66b7f-115">Also, the creation of the Azure resources used in this quickstart can be accomplished with the [Create a SignalR Service script](scripts/signalr-cli-create-service.md).</span><span class="sxs-lookup"><span data-stu-id="66b7f-115">Also, the creation of the Azure resources used in this quickstart can be accomplished with the [Create a SignalR Service script](scripts/signalr-cli-create-service.md).</span></span>

![Quickstart Complete local](media/signalr-quickstart-dotnet-core/signalr-quickstart-complete-local.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]


## <a name="prerequisites"></a><span data-ttu-id="66b7f-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="66b7f-117">Prerequisites</span></span>

* <span data-ttu-id="66b7f-118">Install the [.NET Core SDK](https://www.microsoft.com/net/download/windows)</span><span class="sxs-lookup"><span data-stu-id="66b7f-118">Install the [.NET Core SDK](https://www.microsoft.com/net/download/windows)</span></span>
* <span data-ttu-id="66b7f-119">Download or clone the [AzureSignalR-sample](https://github.com/aspnet/AzureSignalR-samples) github repository.</span><span class="sxs-lookup"><span data-stu-id="66b7f-119">Download or clone the [AzureSignalR-sample](https://github.com/aspnet/AzureSignalR-samples) github repository.</span></span> 

## <a name="create-an-azure-signalr-resource"></a><span data-ttu-id="66b7f-120">Create an Azure SignalR resource</span><span class="sxs-lookup"><span data-stu-id="66b7f-120">Create an Azure SignalR resource</span></span>

[!INCLUDE [azure-signalr-create](../../includes/signalr-create.md)]

## <a name="create-an-aspnet-core-web-app"></a><span data-ttu-id="66b7f-121">Create an ASP.NET Core web app</span><span class="sxs-lookup"><span data-stu-id="66b7f-121">Create an ASP.NET Core web app</span></span>

<span data-ttu-id="66b7f-122">In this section, you use the [.NET Core command-line interface (CLI)](https://docs.microsoft.com/dotnet/core/tools/) to create a new ASP.NET Core MVC Web App project.</span><span class="sxs-lookup"><span data-stu-id="66b7f-122">In this section, you use the [.NET Core command-line interface (CLI)](https://docs.microsoft.com/dotnet/core/tools/) to create a new ASP.NET Core MVC Web App project.</span></span> <span data-ttu-id="66b7f-123">The advantage of using the .NET Core CLI over Visual Studio is that it is available across the Windows, macOS, and Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="66b7f-123">The advantage of using the .NET Core CLI over Visual Studio is that it is available across the Windows, macOS, and Linux platforms.</span></span> 

1. <span data-ttu-id="66b7f-124">Create a new folder for your project.</span><span class="sxs-lookup"><span data-stu-id="66b7f-124">Create a new folder for your project.</span></span> <span data-ttu-id="66b7f-125">In this quickstart, the *E:\Testing\chattest* folder is used.</span><span class="sxs-lookup"><span data-stu-id="66b7f-125">In this quickstart, the *E:\Testing\chattest* folder is used.</span></span>

2. <span data-ttu-id="66b7f-126">In the new folder, execute the following command to create a new ASP.NET Core MVC Web App project:</span><span class="sxs-lookup"><span data-stu-id="66b7f-126">In the new folder, execute the following command to create a new ASP.NET Core MVC Web App project:</span></span>

        dotnet new mvc


## <a name="add-secret-manager-to-the-project"></a><span data-ttu-id="66b7f-127">Add Secret Manager to the project</span><span class="sxs-lookup"><span data-stu-id="66b7f-127">Add Secret Manager to the project</span></span>

<span data-ttu-id="66b7f-128">In this section, you will add the [Secret Manager tool](https://docs.microsoft.com/aspnet/core/security/app-secrets) to your project.</span><span class="sxs-lookup"><span data-stu-id="66b7f-128">In this section, you will add the [Secret Manager tool](https://docs.microsoft.com/aspnet/core/security/app-secrets) to your project.</span></span> <span data-ttu-id="66b7f-129">The Secret Manager tool stores sensitive data for development work outside of your project tree.</span><span class="sxs-lookup"><span data-stu-id="66b7f-129">The Secret Manager tool stores sensitive data for development work outside of your project tree.</span></span> <span data-ttu-id="66b7f-130">This approach helps prevent the accidental sharing of app secrets within source code.</span><span class="sxs-lookup"><span data-stu-id="66b7f-130">This approach helps prevent the accidental sharing of app secrets within source code.</span></span>

1. <span data-ttu-id="66b7f-131">Open your *.csproj* file.</span><span class="sxs-lookup"><span data-stu-id="66b7f-131">Open your *.csproj* file.</span></span> <span data-ttu-id="66b7f-132">Add a `DotNetCliToolReference` element to include *Microsoft.Extensions.SecretManager.Tools*.</span><span class="sxs-lookup"><span data-stu-id="66b7f-132">Add a `DotNetCliToolReference` element to include *Microsoft.Extensions.SecretManager.Tools*.</span></span> <span data-ttu-id="66b7f-133">Also add a `UserSecretsId` element as shown below, and save the file.</span><span class="sxs-lookup"><span data-stu-id="66b7f-133">Also add a `UserSecretsId` element as shown below, and save the file.</span></span>

    <span data-ttu-id="66b7f-134">*chattest.csproj:*</span><span class="sxs-lookup"><span data-stu-id="66b7f-134">*chattest.csproj:*</span></span>

    ```xml
    <Project Sdk="Microsoft.NET.Sdk.Web">
    <PropertyGroup>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <UserSecretsId>SignalRChatRoomEx</UserSecretsId>
    </PropertyGroup>
    <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore.All" Version="2.0.0" />
    </ItemGroup>
    <ItemGroup>
        <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
        <DotNetCliToolReference Include="Microsoft.Extensions.SecretManager.Tools" Version="2.0.0" />
    </ItemGroup>
    </Project>    
    ```

## <a name="add-azure-signalr-to-the-web-app"></a><span data-ttu-id="66b7f-135">Add Azure SignalR to the web app</span><span class="sxs-lookup"><span data-stu-id="66b7f-135">Add Azure SignalR to the web app</span></span>

1. <span data-ttu-id="66b7f-136">Add a reference to the `Microsoft.Azure.SignalR` NuGet package by executing the following command:</span><span class="sxs-lookup"><span data-stu-id="66b7f-136">Add a reference to the `Microsoft.Azure.SignalR` NuGet package by executing the following command:</span></span>

        dotnet add package Microsoft.Azure.SignalR -v 1.0.0-*

2. <span data-ttu-id="66b7f-137">Execute the following command to restore packages for your project.</span><span class="sxs-lookup"><span data-stu-id="66b7f-137">Execute the following command to restore packages for your project.</span></span>

        dotnet restore

3. <span data-ttu-id="66b7f-138">Add a secret named *Azure:SignalR:ConnectionString* to Secret Manager.</span><span class="sxs-lookup"><span data-stu-id="66b7f-138">Add a secret named *Azure:SignalR:ConnectionString* to Secret Manager.</span></span> 

    <span data-ttu-id="66b7f-139">This secret will contain the connection string to access your SignalR Service resource.</span><span class="sxs-lookup"><span data-stu-id="66b7f-139">This secret will contain the connection string to access your SignalR Service resource.</span></span> <span data-ttu-id="66b7f-140">*Azure:SignalR:ConnectionString* is the default configuration key that SignalR looks for in order to establish a connection.</span><span class="sxs-lookup"><span data-stu-id="66b7f-140">*Azure:SignalR:ConnectionString* is the default configuration key that SignalR looks for in order to establish a connection.</span></span> <span data-ttu-id="66b7f-141">Replace the value in the command below with the connection string for your SignalR Service resource.</span><span class="sxs-lookup"><span data-stu-id="66b7f-141">Replace the value in the command below with the connection string for your SignalR Service resource.</span></span>

    <span data-ttu-id="66b7f-142">This command must be executed in the same directory as the *.csproj* file.</span><span class="sxs-lookup"><span data-stu-id="66b7f-142">This command must be executed in the same directory as the *.csproj* file.</span></span>

    ```
    dotnet user-secrets set Azure:SignalR:ConnectionString "Endpoint=<Your endpoint>;AccessKey=<Your access key>;"    
    ```

    <span data-ttu-id="66b7f-143">Secret Manager will only be used for testing the web app while it is hosted locally.</span><span class="sxs-lookup"><span data-stu-id="66b7f-143">Secret Manager will only be used for testing the web app while it is hosted locally.</span></span> <span data-ttu-id="66b7f-144">In a later tutorial, you will deploy the chat web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="66b7f-144">In a later tutorial, you will deploy the chat web app to Azure.</span></span> <span data-ttu-id="66b7f-145">Once the web app is deployed to Azure, you will use an application setting instead of storing the connection string with Secret Manager.</span><span class="sxs-lookup"><span data-stu-id="66b7f-145">Once the web app is deployed to Azure, you will use an application setting instead of storing the connection string with Secret Manager.</span></span>

    <span data-ttu-id="66b7f-146">This secret is a accessed with the configuration API.</span><span class="sxs-lookup"><span data-stu-id="66b7f-146">This secret is a accessed with the configuration API.</span></span> <span data-ttu-id="66b7f-147">A colon (:) works in the configuration name with the configuration API on all supported platforms, see [Configuration by environment](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/index?tabs=basicconfiguration&view=aspnetcore-2.0#configuration-by-environment).</span><span class="sxs-lookup"><span data-stu-id="66b7f-147">A colon (:) works in the configuration name with the configuration API on all supported platforms, see [Configuration by environment](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/index?tabs=basicconfiguration&view=aspnetcore-2.0#configuration-by-environment).</span></span> 


4. <span data-ttu-id="66b7f-148">Open *Startup.cs* and update the `ConfigureServices` method to use Azure SignalR Service by calling the `services.AddSignalR().AddAzureSignalR()` method:</span><span class="sxs-lookup"><span data-stu-id="66b7f-148">Open *Startup.cs* and update the `ConfigureServices` method to use Azure SignalR Service by calling the `services.AddSignalR().AddAzureSignalR()` method:</span></span>

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
        services.AddSignalR().AddAzureSignalR();
    }
    ```

    <span data-ttu-id="66b7f-149">By not passing a parameter to `AddAzureSignalR()`, this code uses the default configuration key, *Azure:SignalR:ConnectionString*, for the SignalR Service resource connection string.</span><span class="sxs-lookup"><span data-stu-id="66b7f-149">By not passing a parameter to `AddAzureSignalR()`, this code uses the default configuration key, *Azure:SignalR:ConnectionString*, for the SignalR Service resource connection string.</span></span>

5. <span data-ttu-id="66b7f-150">Also in *Startup.cs*, update the `Configure` method by replacing the call to `app.UseStaticFiles()` with the following code and save the file.</span><span class="sxs-lookup"><span data-stu-id="66b7f-150">Also in *Startup.cs*, update the `Configure` method by replacing the call to `app.UseStaticFiles()` with the following code and save the file.</span></span>

    ```csharp
    app.UseFileServer();
    app.UseAzureSignalR(routes =>
    {
        routes.MapHub<Chat>("/chat");
    });
    ```            

### <a name="add-a-hub-class"></a><span data-ttu-id="66b7f-151">Add a hub class</span><span class="sxs-lookup"><span data-stu-id="66b7f-151">Add a hub class</span></span>

<span data-ttu-id="66b7f-152">In SignalR, a hub is a core component that exposes a set of methods that can be called from client.</span><span class="sxs-lookup"><span data-stu-id="66b7f-152">In SignalR, a hub is a core component that exposes a set of methods that can be called from client.</span></span> <span data-ttu-id="66b7f-153">In this section, you define a hub class with two methods:</span><span class="sxs-lookup"><span data-stu-id="66b7f-153">In this section, you define a hub class with two methods:</span></span> 

* <span data-ttu-id="66b7f-154">`Broadcast`: This method broadcasts a message to all clients.</span><span class="sxs-lookup"><span data-stu-id="66b7f-154">`Broadcast`: This method broadcasts a message to all clients.</span></span>
* <span data-ttu-id="66b7f-155">`Echo`: This method sends a message back to the caller.</span><span class="sxs-lookup"><span data-stu-id="66b7f-155">`Echo`: This method sends a message back to the caller.</span></span>

<span data-ttu-id="66b7f-156">Both methods use the `Clients` interface provided by the ASP.NET Core SignalR SDK.</span><span class="sxs-lookup"><span data-stu-id="66b7f-156">Both methods use the `Clients` interface provided by the ASP.NET Core SignalR SDK.</span></span> <span data-ttu-id="66b7f-157">This interface gives you access to all connected clients enabling you to push content to your clients.</span><span class="sxs-lookup"><span data-stu-id="66b7f-157">This interface gives you access to all connected clients enabling you to push content to your clients.</span></span>

1. <span data-ttu-id="66b7f-158">In your project directory, add a new folder named *Hub*.</span><span class="sxs-lookup"><span data-stu-id="66b7f-158">In your project directory, add a new folder named *Hub*.</span></span> <span data-ttu-id="66b7f-159">Add a new hub code file named *Chat.cs* to the new folder.</span><span class="sxs-lookup"><span data-stu-id="66b7f-159">Add a new hub code file named *Chat.cs* to the new folder.</span></span>

2. <span data-ttu-id="66b7f-160">Add the following code to *Chat.cs* to define you hub class and save the file.</span><span class="sxs-lookup"><span data-stu-id="66b7f-160">Add the following code to *Chat.cs* to define you hub class and save the file.</span></span> 

    <span data-ttu-id="66b7f-161">Update the namespace for this class if you used a project name that differs from *chattest*.</span><span class="sxs-lookup"><span data-stu-id="66b7f-161">Update the namespace for this class if you used a project name that differs from *chattest*.</span></span>

    ```csharp
    using Microsoft.AspNetCore.SignalR;

    namespace chattest
    {

        public class Chat : Hub
        {
            public void BroadcastMessage(string name, string message)
            {
                Clients.All.SendAsync("broadcastMessage", name, message);
            }

            public void Echo(string name, string message)
            {
                Clients.Client(Context.ConnectionId).SendAsync("echo", name, message + " (echo from server)");
            }
        }
    }
    ```

### <a name="add-the-web-app-client-interface"></a><span data-ttu-id="66b7f-162">Add the web app client interface</span><span class="sxs-lookup"><span data-stu-id="66b7f-162">Add the web app client interface</span></span>

<span data-ttu-id="66b7f-163">The client user interface for this chat room app will be composed of HTML and JavaScript in a file named *index.html* in the *wwwroot* directory.</span><span class="sxs-lookup"><span data-stu-id="66b7f-163">The client user interface for this chat room app will be composed of HTML and JavaScript in a file named *index.html* in the *wwwroot* directory.</span></span>

<span data-ttu-id="66b7f-164">Copy the *index.html* file, and the *css*, and *scripts* folders from the *wwwroot* folder of the [samples repository](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/ChatRoom/wwwroot) into your project's *wwwroot* folder.</span><span class="sxs-lookup"><span data-stu-id="66b7f-164">Copy the *index.html* file, and the *css*, and *scripts* folders from the *wwwroot* folder of the [samples repository](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/ChatRoom/wwwroot) into your project's *wwwroot* folder.</span></span>

<span data-ttu-id="66b7f-165">The main code of *index.html*:</span><span class="sxs-lookup"><span data-stu-id="66b7f-165">The main code of *index.html*:</span></span> 

```javascript
var connection = new signalR.HubConnectionBuilder()
                            .withUrl('/chat')
                            .build();
bindConnectionMessage(connection);
connection.start()
    .then(function () {
        onConnected(connection);
    })
    .catch(function (error) {
        console.error(error.message);
    });
```    

<span data-ttu-id="66b7f-166">The code in *index.html*, calls `HubConnectionBuilder.build()` to make an HTTP connection to the Azure SignalR resource.</span><span class="sxs-lookup"><span data-stu-id="66b7f-166">The code in *index.html*, calls `HubConnectionBuilder.build()` to make an HTTP connection to the Azure SignalR resource.</span></span>

<span data-ttu-id="66b7f-167">If the connection is successful, that connection is passed to `bindConnectionMessage`, which adds event handlers for incoming content pushes to the client.</span><span class="sxs-lookup"><span data-stu-id="66b7f-167">If the connection is successful, that connection is passed to `bindConnectionMessage`, which adds event handlers for incoming content pushes to the client.</span></span> 

<span data-ttu-id="66b7f-168">`HubConnection.start()` starts communication with the hub.</span><span class="sxs-lookup"><span data-stu-id="66b7f-168">`HubConnection.start()` starts communication with the hub.</span></span> <span data-ttu-id="66b7f-169">Once communication is started, `onConnected()` adds the button event handlers.</span><span class="sxs-lookup"><span data-stu-id="66b7f-169">Once communication is started, `onConnected()` adds the button event handlers.</span></span> <span data-ttu-id="66b7f-170">These handlers use the connection to allow this client to push content updates to all connected clients.</span><span class="sxs-lookup"><span data-stu-id="66b7f-170">These handlers use the connection to allow this client to push content updates to all connected clients.</span></span>

## <a name="add-a-development-runtime-profile"></a><span data-ttu-id="66b7f-171">Add a development runtime profile</span><span class="sxs-lookup"><span data-stu-id="66b7f-171">Add a development runtime profile</span></span>

<span data-ttu-id="66b7f-172">In this section, you will add a development runtime environment for ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="66b7f-172">In this section, you will add a development runtime environment for ASP.NET Core.</span></span> <span data-ttu-id="66b7f-173">For more information on runtime environment for ASP.NET Core, see [Work with multiple environments in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="66b7f-173">For more information on runtime environment for ASP.NET Core, see [Work with multiple environments in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/environments).</span></span>

1. <span data-ttu-id="66b7f-174">Create a new folder in your project named *Properties*.</span><span class="sxs-lookup"><span data-stu-id="66b7f-174">Create a new folder in your project named *Properties*.</span></span>

2. <span data-ttu-id="66b7f-175">Add a new file named *launchSettings.json* to the folder, with the following content and save the file.</span><span class="sxs-lookup"><span data-stu-id="66b7f-175">Add a new file named *launchSettings.json* to the folder, with the following content and save the file.</span></span>

    ```json
    {
        "profiles" : 
        {
            "ChatRoom": 
            {
                "commandName": "Project",
                "launchBrowser": true,
                "environmentVariables": 
                {
                    "ASPNETCORE_ENVIRONMENT": "Development"
                },
                "applicationUrl": "http://localhost:5000/"
            }
        }
    }
    ```


## <a name="build-and-run-the-app-locally"></a><span data-ttu-id="66b7f-176">Build and Run the app locally</span><span class="sxs-lookup"><span data-stu-id="66b7f-176">Build and Run the app locally</span></span>

1. <span data-ttu-id="66b7f-177">To build the app using the .NET Core CLI, execute the following command in the command shell:</span><span class="sxs-lookup"><span data-stu-id="66b7f-177">To build the app using the .NET Core CLI, execute the following command in the command shell:</span></span>

        dotnet build

2. <span data-ttu-id="66b7f-178">Once the build successfully completes, execute the following command to run the web app locally:</span><span class="sxs-lookup"><span data-stu-id="66b7f-178">Once the build successfully completes, execute the following command to run the web app locally:</span></span>

        dotnet run

    <span data-ttu-id="66b7f-179">The app will be hosted locally on port 5000 as configured in our development runtime profile:</span><span class="sxs-lookup"><span data-stu-id="66b7f-179">The app will be hosted locally on port 5000 as configured in our development runtime profile:</span></span>

        E:\Testing\chattest>dotnet run
        Hosting environment: Development
        Content root path: E:\Testing\chattest
        Now listening on: http://localhost:5000
        Application started. Press Ctrl+C to shut down.    

3. <span data-ttu-id="66b7f-180">Launch two browser windows and navigate each browser to `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="66b7f-180">Launch two browser windows and navigate each browser to `http://localhost:5000`.</span></span> <span data-ttu-id="66b7f-181">You will be prompted to enter your name.</span><span class="sxs-lookup"><span data-stu-id="66b7f-181">You will be prompted to enter your name.</span></span> <span data-ttu-id="66b7f-182">Enter a client name for both clients and test pushing message content between both clients using the **Send** button.</span><span class="sxs-lookup"><span data-stu-id="66b7f-182">Enter a client name for both clients and test pushing message content between both clients using the **Send** button.</span></span>

    ![Quickstart Complete local](media/signalr-quickstart-dotnet-core/signalr-quickstart-complete-local.png)



## <a name="clean-up-resources"></a><span data-ttu-id="66b7f-184">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="66b7f-184">Clean up resources</span></span>

<span data-ttu-id="66b7f-185">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them with the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="66b7f-185">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them with the next tutorial.</span></span>

<span data-ttu-id="66b7f-186">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="66b7f-186">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="66b7f-187">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="66b7f-187">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="66b7f-188">Make sure that you do not accidentally delete the wrong resource group or resources.</span><span class="sxs-lookup"><span data-stu-id="66b7f-188">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="66b7f-189">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="66b7f-189">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span></span>
> 
> 

<span data-ttu-id="66b7f-190">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="66b7f-190">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>

<span data-ttu-id="66b7f-191">In the **Filter by name...** textbox, type the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="66b7f-191">In the **Filter by name...** textbox, type the name of your resource group.</span></span> <span data-ttu-id="66b7f-192">The instructions for this quickstart used a resource group named *SignalRTestResources*.</span><span class="sxs-lookup"><span data-stu-id="66b7f-192">The instructions for this quickstart used a resource group named *SignalRTestResources*.</span></span> <span data-ttu-id="66b7f-193">On your resource group in the result list, click **...** then **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="66b7f-193">On your resource group in the result list, click **...** then **Delete resource group**.</span></span>

   
![Delete](./media/signalr-quickstart-dotnet-core/signalr-delete-resource-group.png)


<span data-ttu-id="66b7f-195">You will be asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="66b7f-195">You will be asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="66b7f-196">Type the name of your resource group to confirm, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="66b7f-196">Type the name of your resource group to confirm, and click **Delete**.</span></span>
   
<span data-ttu-id="66b7f-197">After a few moments, the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="66b7f-197">After a few moments, the resource group and all of its contained resources are deleted.</span></span>



## <a name="next-steps"></a><span data-ttu-id="66b7f-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="66b7f-198">Next steps</span></span>

<span data-ttu-id="66b7f-199">In this quickstart, you've created a new Azure SignalR Service resource and used it with an ASP.NET Core Web app to push content updates in real time to multiple connected clients.</span><span class="sxs-lookup"><span data-stu-id="66b7f-199">In this quickstart, you've created a new Azure SignalR Service resource and used it with an ASP.NET Core Web app to push content updates in real time to multiple connected clients.</span></span> <span data-ttu-id="66b7f-200">To learn more about using Azure SignalR Service, continue to the next tutorial that demonstrates authentication.</span><span class="sxs-lookup"><span data-stu-id="66b7f-200">To learn more about using Azure SignalR Service, continue to the next tutorial that demonstrates authentication.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66b7f-201">Azure SignalR Service authentication</span><span class="sxs-lookup"><span data-stu-id="66b7f-201">Azure SignalR Service authentication</span></span>](./signalr-authenticate-oauth.md)


