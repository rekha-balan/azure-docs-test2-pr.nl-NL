---
title: Debug a Java Web App on Azure in Eclipse | Microsoft Docs
description: This tutorial shows you how to use the Azure Toolkit for Eclipse to debug a Java Web App running on Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: ''
ms.assetid: 321d2d19-9ce0-4165-8555-b6b15e671393
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: asirveda;robmcm
ms.openlocfilehash: 093449af56eb24dece404904ac7e677e232edabe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553422"
---
# <a name="debug-a-java-web-app-on-azure-in-eclipse"></a><span data-ttu-id="3c36a-103">Debug a Java Web App on Azure in Eclipse</span><span class="sxs-lookup"><span data-stu-id="3c36a-103">Debug a Java Web App on Azure in Eclipse</span></span>
<span data-ttu-id="3c36a-104">This tutorial shows how to debug a Java Web App running on Azure by using the [Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3c36a-104">This tutorial shows how to debug a Java Web App running on Azure by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="3c36a-105">For the sake of simplicity, you will use a basic Java Server Page (JSP) example for this tutorial, but the steps would be similar for a Java servlet when you are debugging on Azure.</span><span class="sxs-lookup"><span data-stu-id="3c36a-105">For the sake of simplicity, you will use a basic Java Server Page (JSP) example for this tutorial, but the steps would be similar for a Java servlet when you are debugging on Azure.</span></span>

<span data-ttu-id="3c36a-106">When you have completed this tutorial, your application will look similar to the following illustration when you are debugging it in Eclipse:</span><span class="sxs-lookup"><span data-stu-id="3c36a-106">When you have completed this tutorial, your application will look similar to the following illustration when you are debugging it in Eclipse:</span></span>

![][01]

## <a name="prerequisites"></a><span data-ttu-id="3c36a-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3c36a-107">Prerequisites</span></span>
* <span data-ttu-id="3c36a-108">A Java Developer Kit (JDK), v 1.8 or later.</span><span class="sxs-lookup"><span data-stu-id="3c36a-108">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="3c36a-109">Eclipse IDE for Java EE Developers, Indigo or later.</span><span class="sxs-lookup"><span data-stu-id="3c36a-109">Eclipse IDE for Java EE Developers, Indigo or later.</span></span> <span data-ttu-id="3c36a-110">This can be downloaded from <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="3c36a-110">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="3c36a-111">A distribution of a Java-based web server or application server, such as Apache Tomcat or Jetty.</span><span class="sxs-lookup"><span data-stu-id="3c36a-111">A distribution of a Java-based web server or application server, such as Apache Tomcat or Jetty.</span></span>
* <span data-ttu-id="3c36a-112">An Azure subscription, which can be acquired from <https://azure.microsoft.com/en-us/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="3c36a-112">An Azure subscription, which can be acquired from <https://azure.microsoft.com/en-us/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="3c36a-113">The Azure Toolkit for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3c36a-113">The Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="3c36a-114">For more information, see [Installing the Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3c36a-114">For more information, see [Installing the Azure Toolkit for Eclipse].</span></span>
* <span data-ttu-id="3c36a-115">A Dynamic Web Project created and deployed to Azure App Service; for example see [Create a Hello World Web App for Azure in Eclipse].</span><span class="sxs-lookup"><span data-stu-id="3c36a-115">A Dynamic Web Project created and deployed to Azure App Service; for example see [Create a Hello World Web App for Azure in Eclipse].</span></span>

## <a name="to-debug-a-java-web-app-on-azure"></a><span data-ttu-id="3c36a-116">To Debug a Java Web App on Azure</span><span class="sxs-lookup"><span data-stu-id="3c36a-116">To Debug a Java Web App on Azure</span></span>
<span data-ttu-id="3c36a-117">To complete these steps in this section, you can use an existing Dynamic Web Project which you have already deployed as a Java Web App on Azure, you download a [Sample Dynamic Web Project] and follow steps in [Create a Hello World Web App for Azure in Eclipse] to deploy it on Azure.</span><span class="sxs-lookup"><span data-stu-id="3c36a-117">To complete these steps in this section, you can use an existing Dynamic Web Project which you have already deployed as a Java Web App on Azure, you download a [Sample Dynamic Web Project] and follow steps in [Create a Hello World Web App for Azure in Eclipse] to deploy it on Azure.</span></span> 

1. <span data-ttu-id="3c36a-118">Open Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3c36a-118">Open Eclipse.</span></span>
2. <span data-ttu-id="3c36a-119">Configure time-outs for remote debugging:</span><span class="sxs-lookup"><span data-stu-id="3c36a-119">Configure time-outs for remote debugging:</span></span>
   
   1. <span data-ttu-id="3c36a-120">Click the **Windows** menu in Eclipse, and then click **Preferences**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-120">Click the **Windows** menu in Eclipse, and then click **Preferences**.</span></span>
   2. <span data-ttu-id="3c36a-121">Expand the **Java** node, then select **Debug**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-121">Expand the **Java** node, then select **Debug**.</span></span>
   3. <span data-ttu-id="3c36a-122">Configure both the **Debugger timeout (ms)** and **Launch timeout (ms)** settings to `120000`.</span><span class="sxs-lookup"><span data-stu-id="3c36a-122">Configure both the **Debugger timeout (ms)** and **Launch timeout (ms)** settings to `120000`.</span></span>
      
       ![][02]
   4. <span data-ttu-id="3c36a-123">Click **OK** to close the **Preferences** dialog.</span><span class="sxs-lookup"><span data-stu-id="3c36a-123">Click **OK** to close the **Preferences** dialog.</span></span>
3. <span data-ttu-id="3c36a-124">In  Eclipse's Project Explorer view, right click the Dynamic Web Project which you have deployed to Azure.</span><span class="sxs-lookup"><span data-stu-id="3c36a-124">In  Eclipse's Project Explorer view, right click the Dynamic Web Project which you have deployed to Azure.</span></span> <span data-ttu-id="3c36a-125">When the context menu appears, select **Debug As**, and then click **Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-125">When the context menu appears, select **Debug As**, and then click **Azure Web App**.</span></span>
   
    ![][03]
4. <span data-ttu-id="3c36a-126">If this is the first time you are debugging your Dynamic Web Project, the **Debug Configurations** dialog will open; you can accept the default values which are specified by the Toolkit on the **Connect** tab. On the **Source** tab, click **Add**, then **Java project**, select **Dynamic Web Project**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-126">If this is the first time you are debugging your Dynamic Web Project, the **Debug Configurations** dialog will open; you can accept the default values which are specified by the Toolkit on the **Connect** tab. On the **Source** tab, click **Add**, then **Java project**, select **Dynamic Web Project**, and then click **OK**.</span></span> <span data-ttu-id="3c36a-127">Once you have completed these steps, click **Debug**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-127">Once you have completed these steps, click **Debug**.</span></span>
   
    ![][04]
5. <span data-ttu-id="3c36a-128">When prompted to **Enable remote debugging in the remote Web App now?**, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-128">When prompted to **Enable remote debugging in the remote Web App now?**, click **OK**.</span></span>
6. <span data-ttu-id="3c36a-129">When prompted that **Your web app is now ready for remote debugging**, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-129">When prompted that **Your web app is now ready for remote debugging**, click **OK**.</span></span>
   
    ![][05]
7. <span data-ttu-id="3c36a-130">When the **Debug Configurations** dialog reappears, click **Debug**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-130">When the **Debug Configurations** dialog reappears, click **Debug**.</span></span>
8. <span data-ttu-id="3c36a-131">A Windows command prompt or Unix shell will open and prepare necessary connection for debugging; you need to wait until the connection to your remote Java Web app is successful before you continue.</span><span class="sxs-lookup"><span data-stu-id="3c36a-131">A Windows command prompt or Unix shell will open and prepare necessary connection for debugging; you need to wait until the connection to your remote Java Web app is successful before you continue.</span></span> <span data-ttu-id="3c36a-132">If you are using Windows, it will look like the following illustration.</span><span class="sxs-lookup"><span data-stu-id="3c36a-132">If you are using Windows, it will look like the following illustration.</span></span>
   
    ![][06]
9. <span data-ttu-id="3c36a-133">Insert a break point in your JSP page, then open the URL for your Java Web App in a browser:</span><span class="sxs-lookup"><span data-stu-id="3c36a-133">Insert a break point in your JSP page, then open the URL for your Java Web App in a browser:</span></span>
   
   1. <span data-ttu-id="3c36a-134">Open up **Azure Explorer** in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="3c36a-134">Open up **Azure Explorer** in Eclipse.</span></span>
   2. <span data-ttu-id="3c36a-135">Navigate to **Web Apps** and the Java Web App you want to debug.</span><span class="sxs-lookup"><span data-stu-id="3c36a-135">Navigate to **Web Apps** and the Java Web App you want to debug.</span></span>
   3. <span data-ttu-id="3c36a-136">Right click on the Web App, and click **Open in Browser**.</span><span class="sxs-lookup"><span data-stu-id="3c36a-136">Right click on the Web App, and click **Open in Browser**.</span></span>
   4. <span data-ttu-id="3c36a-137">Eclipse will now enter into debug mode.</span><span class="sxs-lookup"><span data-stu-id="3c36a-137">Eclipse will now enter into debug mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c36a-138">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3c36a-138">Next Steps</span></span>
<span data-ttu-id="3c36a-139">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3c36a-139">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="3c36a-140">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span><span class="sxs-lookup"><span data-stu-id="3c36a-140">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Sample Dynamic Web Project]: http://go.microsoft.com/fwlink/?LinkId=817337

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Web Apps Overview]: ./app-service-web-overview.md

<!-- IMG List -->

[01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-eclipse/01-debug-java-web-app-in-eclipse.png
[02]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-eclipse/02-configure-eclipse-remote-debug.png
[03]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-eclipse/03-debug-as.png
[04]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-eclipse/04-debug-configurations.png
[05]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-eclipse/05-ready-for-remote-debugging.png
[06]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-eclipse/06-windows-command-prompt-connection-successful-to-remote.png






