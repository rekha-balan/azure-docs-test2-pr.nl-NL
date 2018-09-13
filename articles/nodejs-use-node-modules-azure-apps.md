---
title: Working with Node.js Modules
description: Learn how to work with Node.js modules when using Azure App Service or Cloud Services.
services: ''
documentationcenter: nodejs
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 4ef028e7dbacc126a94b383d0fb13e255bcedcaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563711"
---
# <a name="using-nodejs-modules-with-azure-applications"></a>Using Node.js Modules with Azure applications
This document provides guidance on using Node.js modules with applications hosted on Azure. It provides guidance on ensuring that your application uses a specific version of module as well as using native modules with Azure.

If you are already familiar with using Node.js modules, **package.json** and **npm-shrinkwrap.json** files, the following is a quick summary of what is discussed in this article:

* Azure App Service understands **package.json** and **npm-shrinkwrap.json** files and can install modules based on entries in these files.
* Azure Cloud Services expect all modules to be installed on the development environment, and the **node\_modules** directory to be included as part of the deployment package. It is possible to enable support for installing modules using **package.json** or **npm-shrinkwrap.json** files on Cloud Services, however this requires customization of the default scripts used by Cloud Service projects. For an example of how to accomplish this, see [Azure Startup task to run npm install to avoid deploying node modules](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> Azure Virtual Machines are not discussed in this article, as the deployment experience in a VM will be dependent on the operating system hosted by the Virtual Machine.
> 
> 

## <a name="nodejs-modules"></a>Node.js Modules
Modules are loadable JavaScript packages that provide specific functionality for your application. A module is usually installed using the **npm** command-line tool, however some (such as the http module) are provided as part of the core Node.js package.

When modules are installed, they are stored in the **node\_modules** directory at the root of your application directory structure. Each module within the **node\_modules** directory maintains its own **node\_modules** directory that contains any modules that it depends on, and this repeats again for every module all the way down the dependency chain. This allows each module installed to have its own version requirements for the modules it depends on, however it can result in quite a large directory structure.

When deploying the **node\_modules** directory as part of your application, it will increase the size of the deployment compared to using a **package.json** or **npm-shrinkwrap.json** file; however, it does guarantee that the version of the modules used in production are the same as those used in development.

### <a name="native-modules"></a>Native Modules
While most modules are simply plain-text JavaScript files, some modules are platform-specific binary images. These modules are compiled at install time, usually by using Python and node-gyp. Since Azure Cloud Services rely on the **node\_modules** folder being deployed as part of the application, any native module included as part of the installed modules should work in a cloud service as long as it was installed and compiled on a Windows development system.

Azure App Service does not support all native modules and might fail at compiling those with very specific prerequisites. While some popular modules like MongoDB have optional native dependencies and work just fine without them, two workarounds proved successful with almost all native modules available today:

* Run **npm install** on a Windows machine that has all the native module's prerequisites installed. Then, deploy the created **node\_modules** folder as part of the application to Azure App Service.
  * Before compiling, check that your local Node.js installation has matching architecture and the version is as close as possible to the one used in Azure (the current values can be checked on runtime from properties **process.arch** and **process.version**).
* Azure App Service can be configured to execute custom bash or shell scripts during deployment, giving you the opportunity to execute custom commands and precisely configure the way **npm install** is being run. For a video showing how to do this, see [Custom Website Deployment Scripts with Kudu].

### <a name="using-a-packagejson-file"></a>Using a package.json file
The **package.json** file is a way to specify the top level dependencies your application requires so that the hosting platform can install the dependencies, rather than requiring you to include the **node\_packages** folder as part of the deployment. After the application has been deployed, the **npm install** command is used to parse the **package.json** file and install all the dependencies listed.

During development, you can use the **--save**, **--save-dev**, or **--save-optional** parameters when installing modules to add an entry for the module to your **package.json** file automatically. For more information, see [npm-install](https://docs.npmjs.com/cli/install).

One potential problem with the **package.json** file is that it only specifies the version for top level dependencies. Each module installed may or may not specify the version of the modules it depends on, and so it is possible that you may end up with a different dependency chain than the one used in development.

> [!NOTE]
> When deploying to Azure App Service, if your <b>package.json</b> file references a native module you will see an error similar to the following when publishing the application using Git:
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>Using a npm-shrinkwrap.json file
The **npm-shrinkwrap.json** file is an attempt to address the module versioning limitations of the **package.json** file. While the **package.json** file only includes versions for the top level modules, the **npm-shrinkwrap.json** file contains the version requirements for the full module dependency chain.

When your application is ready for production, you can lock-down version requirements and create an **npm-shrinkwrap.json** file by using the **npm shrinkwrap** command. This will use the versions currently installed in the **node\_modules** folder, and record these to the **npm-shrinkwrap.json** file. After the application has been deployed to the hosting environment, the **npm install** command is used to parse the **npm-shrinkwrap.json** file and install all the dependencies listed. For more information, see [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap).

> [!NOTE]
> When deploying to Azure App Service, if your <b>npm-shrinkwrap.json</b> file references a native module you will see an error similar to the following when publishing the application using Git:
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

## <a name="next-steps"></a>Next Steps
Now that you understand how to use Node.js modules with Azure, learn how to [specify the Node.js version], [build and deploy a Node.js web app](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Interface for Mac and Linux].

For more information, see the [Node.js Developer Center](/develop/nodejs/).

[specify the Node.js version]: nodejs-specify-node-version-azure-apps.md
[How to use the Azure Command-Line Interface for Mac and Linux]:cli-install-nodejs.md
[Custom Website Deployment Scripts with Kudu]: /documentation/videos/custom-web-site-deployment-scripts-with-kudu/