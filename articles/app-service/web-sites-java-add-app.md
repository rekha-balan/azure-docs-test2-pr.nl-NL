---
title: Add a Java application to Azure App Service Web Apps
description: This tutorial shows you how to add a page or application to your instance of Azure App Service Web Apps that is already configured to use Java.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/11/2018
ms.author: robmcm
ms.openlocfilehash: 71009370282fcfbd71c00b30d4ea22802035714d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865096"
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="fbd3e-103">Add a Java application to Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="fbd3e-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="fbd3e-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](app-service-web-get-started-java.md), you can upload your application by placing your WAR in the **webapps** folder.</span><span class="sxs-lookup"><span data-stu-id="fbd3e-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](app-service-web-get-started-java.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="fbd3e-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span><span class="sxs-lookup"><span data-stu-id="fbd3e-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="fbd3e-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span><span class="sxs-lookup"><span data-stu-id="fbd3e-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="fbd3e-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="fbd3e-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="fbd3e-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="fbd3e-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="fbd3e-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app using FTP](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="fbd3e-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app using FTP](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="fbd3e-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span><span class="sxs-lookup"><span data-stu-id="fbd3e-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="fbd3e-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span><span class="sxs-lookup"><span data-stu-id="fbd3e-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="fbd3e-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span><span class="sxs-lookup"><span data-stu-id="fbd3e-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="fbd3e-113">See Also</span><span class="sxs-lookup"><span data-stu-id="fbd3e-113">See Also</span></span>
<span data-ttu-id="fbd3e-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="fbd3e-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="fbd3e-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="fbd3e-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
