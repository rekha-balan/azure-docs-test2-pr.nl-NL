---
title: Create a Node.js chat application with Socket.IO in Azure App Service
description: A tutorial that demonstrates using socket.io in a node.js web app hosted on Azure.
services: app-service\web
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 4f5c04525437aefeccbe58e06b084433d0413dc1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556564"
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Create a Node.js chat application with Socket.IO in Azure App Service
Socket.IO provides real-time communication between your node.js server and clients using WebSockets. It also supports fallback to other transports (such as long polling) that work with older browsers. This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache]. For more information on Socket.IO, see <http://socket.io/>.

> [!NOTE]
> The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].
> 
> 

## <a name="download-the-chat-example"></a>Download the chat example
For this project, we will use the chat example from the [Socket.IO GitHub repository]. Perform the following steps to download the example and add it to the project you previously created.

1. Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)
2. Extract the archive and copy the **examples\\chat** directory to a new location. For example, **\\node\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modify app.js and install modules
1. Rename the **index.js** file to **app.js**. This allows Azure to detect that this is a Node.js application.
2. Open the **app.js** file in a text editor. Change the line containing `var io = require('../..')(server);` as shown below:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:
   
        npm install
   
    This will install the modules into a subfolder named **node_modules**.

## <a name="create-an-azure-web-app"></a>Create an Azure Web App
Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.

> [!NOTE]
> To complete this tutorial, you need an Azure account. If you don't have an account, you can create a free trial account in just a couple of minutes. For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.
> 
> 

1. Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription. See [Install and Configure the Azure CLI](../cli-install-nodejs.md).
2. If this is your first time setting up a repository in Azure, you need to create login credentials. From the Azure CLI, enter the following command:
   
        azure site deployment user set [username] [password]
3. Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository. This command also creates a Git remote named 'azure'.
   
        azure site create mysitename --git
   
    You must replace 'mysitename' with a unique name for your web app.
4. Commit the existing files to the local repository by using the following commands:
   
        git add .
        git commit -m "Initial commit"
5. Push the files to the Azure Web Apps repository with the following command:
   
        git push azure master
   
    When prompted, enter your credentials from step 2. You will receive status messages as modules are imported on the server. Once this process has completed, the application will be hosted on your Azure web app.
   
   > [!NOTE]
   > During module installation, you may notice errors that 'The imported project ... was not found'. These can safely be ignored.
   > 
   > 
6. Socket.IO uses WebSockets, which are not enabled by default on Azure. To enable web sockets, use the following command:
   
        azure site set -w
   
    If prompted, enter the name of the web app.
   
   > [!NOTE]
   > The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface. You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).
   > 
   > To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**. Under **Web Sockets**, click **On**. Then click **Save**.
   > 
   > 
7. To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:
   
        azure site browse

Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.

## <a name="scale-out"></a>Scale out
Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances. While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.

> [!NOTE]
> An additional requirement for scaling out a Socket.IO solution is support for sticky sessions. Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing. For more information, see [Instance Affinity in Azure Web Sites].
> 
> 

### <a name="create-a-redis-cache"></a>Create a Redis cache
Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.

> [!NOTE]
> Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a>Add the redis and socket.io-redis modules
1. From a command-line, change to the **\\node\\chat** directory and use the following command.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > The versions specified in this command are the versions used when testing this article.
   > 
   > 
2. Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.
   
    This will create a publish and subscribe client to the Redis cache created previously. The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application
   
   > [!NOTE]
   > While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache. So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.
   > 
   > While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014. The above code uses the default, unsecure port of 6379.
   > 
   > 
3. Save the modified **app.js**

### <a name="commit-changes-and-redeploy"></a>Commit changes and redeploy
From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.

    azure site scale instances --instances #

Where **#** is the number of instances to create.

You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.

## <a name="troubleshooting"></a>Troubleshooting
### <a name="connection-limits"></a>Connection limits
Azure Web Apps is available in multiple SKUs, which determine the resources available to your site. This includes the number of allowed WebSocket connections. For more information, see the [Web Apps Pricing page].

### <a name="messages-arent-being-sent-using-websockets"></a>Messages aren't being sent using WebSockets
If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.

* **Try limiting the transport to just WebSockets**
  
    In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets. If one or the other does not, Socket.IO will negotiate another transport, such as long polling. The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`. You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.
  > 
  > 
* **Use SSL**
  
    WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header. Some intermediate network devices, such as web proxies, may remove these headers. To avoid this problem, you can establish the WebSocket connection over SSL.
  
    An easy way to accomplish this is to configure Socket.IO to `match origin protocol`. This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page. If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.
  
    To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Verify web.config settings**
  
    Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application. For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.
  
        <webSocket enabled="false"/>
  
    This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO. If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.
  
    Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed. Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file. You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link. The URLs are displayed in the **quick glance** section.
  
  > [!NOTE]
  > The **web.config** file is only generated by Azure Websites if your application does not provide one. If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.
  > 
  > 
  
    If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.  For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point. For example, replacing **app.js** with **server.js**.

> [!NOTE]
> If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service. No credit cards required; no commitments.
> 
> 

## <a name="next-steps"></a>Next steps
In this tutorial you learned how to create a chat application hosted in an Azure web app. You can also host this application as an Azure Cloud Service. For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].

For more information, see also the [Node.js Developer Center].

## <a name="whats-changed"></a>What's changed
* For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].

<!-- URL List -->

[Azure Redis Cache]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643
[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js Developer Center]: /develop/nodejs/
[Try App Service]: https://azure.microsoft.com/try/app-service/
[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io-redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub repository]: https://github.com/socketio/socket.io
[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
