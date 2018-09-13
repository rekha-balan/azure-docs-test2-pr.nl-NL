---
title: Using PM2 configuration for Node.js in Web Apps on Linux | Microsoft Docs
description: Using PM2 configuration for Node.js in Web Apps on Linux
keywords: azure app service, web app, nodejs, pm2, linux, oss
services: app-service
documentationcenter: ''
author: naziml
manager: erikre
editor: ''
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 3d90733adc10478521bbf6cac00dd9403aa128fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549517"
---
# <a name="use-pm2-configuration-for-nodejs-in-web-apps-on-linux"></a><span data-ttu-id="d502f-104">Use PM2 configuration for Node.js in Web Apps on Linux</span><span class="sxs-lookup"><span data-stu-id="d502f-104">Use PM2 configuration for Node.js in Web Apps on Linux</span></span>
<span data-ttu-id="d502f-105">If you set the application stack to Node.js for Web Apps on Linux, you get the option to set a Node.js startup file as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="d502f-105">If you set the application stack to Node.js for Web Apps on Linux, you get the option to set a Node.js startup file as shown in the following image:</span></span>

![Set a Node.js startup file][1]

<span data-ttu-id="d502f-107">You can use this option to do one of the following tasks:</span><span class="sxs-lookup"><span data-stu-id="d502f-107">You can use this option to do one of the following tasks:</span></span>

* <span data-ttu-id="d502f-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="d502f-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="d502f-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="d502f-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="d502f-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span><span class="sxs-lookup"><span data-stu-id="d502f-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span></span> <span data-ttu-id="d502f-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span><span class="sxs-lookup"><span data-stu-id="d502f-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="d502f-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span><span class="sxs-lookup"><span data-stu-id="d502f-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "/bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["/bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="d502f-113">Important things to note in this configuration are:</span><span class="sxs-lookup"><span data-stu-id="d502f-113">Important things to note in this configuration are:</span></span>

* <span data-ttu-id="d502f-114">The "script" property specifies your application's start script.</span><span class="sxs-lookup"><span data-stu-id="d502f-114">The "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="d502f-115">The "instances" property specifies how many instances of the node process to launch.</span><span class="sxs-lookup"><span data-stu-id="d502f-115">The "instances" property specifies how many instances of the node process to launch.</span></span> <span data-ttu-id="d502f-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span><span class="sxs-lookup"><span data-stu-id="d502f-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="d502f-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span><span class="sxs-lookup"><span data-stu-id="d502f-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span></span>
* <span data-ttu-id="d502f-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span><span class="sxs-lookup"><span data-stu-id="d502f-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d502f-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="d502f-119">Next steps</span></span>
* [<span data-ttu-id="d502f-120">What is App Service on Linux?</span><span class="sxs-lookup"><span data-stu-id="d502f-120">What is App Service on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="d502f-121">Azure App Service Web Apps on Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="d502f-121">Azure App Service Web Apps on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png

