---
title: Debug a Java Web App on Azure in IntelliJ | Microsoft Docs
description: This tutorial shows you how to use the Azure Toolkit for IntelliJ to debug a Java Web App running on Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: ''
ms.assetid: 78148648-5a89-4b7d-98f1-9cf8f38dfe8d
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: asirveda;robmcm
ms.openlocfilehash: 41516749b6b5527f5a35cc6503f6a26ecadecb44
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556699"
---
# <a name="debug-a-java-web-app-on-azure-in-intellij"></a><span data-ttu-id="7475d-103">Debug a Java Web App on Azure in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="7475d-103">Debug a Java Web App on Azure in IntelliJ</span></span>
<span data-ttu-id="7475d-104">This tutorial shows how to debug a Java Web App running on Azure by using the [Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="7475d-104">This tutorial shows how to debug a Java Web App running on Azure by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="7475d-105">For the sake of simplicity, you will use a basic Java Server Page (JSP) example for this tutorial, but the steps would be similar for a Java servlet when you are debugging on Azure.</span><span class="sxs-lookup"><span data-stu-id="7475d-105">For the sake of simplicity, you will use a basic Java Server Page (JSP) example for this tutorial, but the steps would be similar for a Java servlet when you are debugging on Azure.</span></span>

<span data-ttu-id="7475d-106">When you have completed this tutorial, your application will look similar to the following illustration when you are debugging it in IntelliJ:</span><span class="sxs-lookup"><span data-stu-id="7475d-106">When you have completed this tutorial, your application will look similar to the following illustration when you are debugging it in IntelliJ:</span></span>

![][01]

## <a name="prerequisites"></a><span data-ttu-id="7475d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7475d-107">Prerequisites</span></span>
* <span data-ttu-id="7475d-108">A Java Developer Kit (JDK), v 1.8 or later.</span><span class="sxs-lookup"><span data-stu-id="7475d-108">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="7475d-109">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="7475d-109">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="7475d-110">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="7475d-110">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="7475d-111">A distribution of a Java-based web server or application server, such as Apache Tomcat or Jetty.</span><span class="sxs-lookup"><span data-stu-id="7475d-111">A distribution of a Java-based web server or application server, such as Apache Tomcat or Jetty.</span></span>
* <span data-ttu-id="7475d-112">An Azure subscription, which can be acquired from <https://azure.microsoft.com/en-us/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="7475d-112">An Azure subscription, which can be acquired from <https://azure.microsoft.com/en-us/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="7475d-113">The Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7475d-113">The Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="7475d-114">For more information, see [Installing the Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="7475d-114">For more information, see [Installing the Azure Toolkit for IntelliJ].</span></span>
* <span data-ttu-id="7475d-115">A Dynamic Web Project created and deployed to Azure App Service; for example see [Create a Hello World Web App for Azure in IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="7475d-115">A Dynamic Web Project created and deployed to Azure App Service; for example see [Create a Hello World Web App for Azure in IntelliJ].</span></span>

## <a name="to-debug-a-java-web-app-on-azure"></a><span data-ttu-id="7475d-116">To Debug a Java Web App on Azure</span><span class="sxs-lookup"><span data-stu-id="7475d-116">To Debug a Java Web App on Azure</span></span>
<span data-ttu-id="7475d-117">To complete these steps in this section, you can use an existing Dynamic Web Project which you have already deployed as a Java Web App on Azure, you download a [Sample Dynamic Web Project] and follow steps in [Create a Hello World Web App for Azure in IntelliJ] to deploy it on Azure.</span><span class="sxs-lookup"><span data-stu-id="7475d-117">To complete these steps in this section, you can use an existing Dynamic Web Project which you have already deployed as a Java Web App on Azure, you download a [Sample Dynamic Web Project] and follow steps in [Create a Hello World Web App for Azure in IntelliJ] to deploy it on Azure.</span></span> 

1. <span data-ttu-id="7475d-118">Open the Java Web App project which you deployed to Azure in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7475d-118">Open the Java Web App project which you deployed to Azure in IntelliJ.</span></span>
2. <span data-ttu-id="7475d-119">Click the **Run** menu, and then click **Edit Configurations...**.</span><span class="sxs-lookup"><span data-stu-id="7475d-119">Click the **Run** menu, and then click **Edit Configurations...**.</span></span>
   
    ![][02]
3. <span data-ttu-id="7475d-120">When the **Run/Debug Configurations** dialog box opens:</span><span class="sxs-lookup"><span data-stu-id="7475d-120">When the **Run/Debug Configurations** dialog box opens:</span></span> 
   
   1. <span data-ttu-id="7475d-121">Select **Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="7475d-121">Select **Azure Web App**.</span></span>
   2. <span data-ttu-id="7475d-122">Click on **+** to add a new configuration.</span><span class="sxs-lookup"><span data-stu-id="7475d-122">Click on **+** to add a new configuration.</span></span>
   3. <span data-ttu-id="7475d-123">Provide a **Name** for the configuration.</span><span class="sxs-lookup"><span data-stu-id="7475d-123">Provide a **Name** for the configuration.</span></span>
   4. <span data-ttu-id="7475d-124">Accept the remaining default values which are suggested by the Azure Toolkit, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7475d-124">Accept the remaining default values which are suggested by the Azure Toolkit, and then click **OK**.</span></span>
      
       ![][03]
4. <span data-ttu-id="7475d-125">Select the Azure Web App debug configuration that you just created on the right top of the menu and click on **Debug**</span><span class="sxs-lookup"><span data-stu-id="7475d-125">Select the Azure Web App debug configuration that you just created on the right top of the menu and click on **Debug**</span></span>
   
    ![][04]
5. <span data-ttu-id="7475d-126">When prompted to **Enable remote debugging in the remote Web App now?**, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7475d-126">When prompted to **Enable remote debugging in the remote Web App now?**, click **OK**.</span></span>
6. <span data-ttu-id="7475d-127">When prompted that **Your web app is now ready for remote debugging**, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7475d-127">When prompted that **Your web app is now ready for remote debugging**, click **OK**.</span></span>
   
    ![][05]
7. <span data-ttu-id="7475d-128">Select the Azure Web App debug configuration that you just created on the right top of the menu, and then click on **Debug**.</span><span class="sxs-lookup"><span data-stu-id="7475d-128">Select the Azure Web App debug configuration that you just created on the right top of the menu, and then click on **Debug**.</span></span>
8. <span data-ttu-id="7475d-129">A Windows command prompt or Unix shell will open and prepare necessary connection for debugging; you need to wait until the connection to your remote Java Web app is successful before you continue.</span><span class="sxs-lookup"><span data-stu-id="7475d-129">A Windows command prompt or Unix shell will open and prepare necessary connection for debugging; you need to wait until the connection to your remote Java Web app is successful before you continue.</span></span> <span data-ttu-id="7475d-130">If you are using Windows, it will look like the following illustration:</span><span class="sxs-lookup"><span data-stu-id="7475d-130">If you are using Windows, it will look like the following illustration:</span></span>
   
    ![][06]
9. <span data-ttu-id="7475d-131">Insert a break point in your JSP page, then open the URL for your Java Web App in a browser:</span><span class="sxs-lookup"><span data-stu-id="7475d-131">Insert a break point in your JSP page, then open the URL for your Java Web App in a browser:</span></span>
   
   1. <span data-ttu-id="7475d-132">Open up **Azure Explorer** in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="7475d-132">Open up **Azure Explorer** in IntelliJ.</span></span>
   2. <span data-ttu-id="7475d-133">Navigate to **Web Apps** and the Java Web App you want to debug.</span><span class="sxs-lookup"><span data-stu-id="7475d-133">Navigate to **Web Apps** and the Java Web App you want to debug.</span></span>
   3. <span data-ttu-id="7475d-134">Right click on the Web App, and click **Open in Browser**.</span><span class="sxs-lookup"><span data-stu-id="7475d-134">Right click on the Web App, and click **Open in Browser**.</span></span>
   4. <span data-ttu-id="7475d-135">IntelliJ will now enter into debug mode.</span><span class="sxs-lookup"><span data-stu-id="7475d-135">IntelliJ will now enter into debug mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7475d-136">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7475d-136">Next Steps</span></span>
<span data-ttu-id="7475d-137">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="7475d-137">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="7475d-138">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span><span class="sxs-lookup"><span data-stu-id="7475d-138">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Installing the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Sample Dynamic Web Project]: http://go.microsoft.com/fwlink/?LinkId=817337

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Web Apps Overview]: ./app-service-web-overview.md

<!-- IMG List -->

[01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-intellij/01-debug-java-web-app-in-intellij.png
[02]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-intellij/02-configure-intellij-remote-debug.png
[03]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-intellij/03-debug-configuration.png
[04]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-intellij/04-select-debug.png
[05]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-intellij/05-ready-for-remote-debugging.png
[06]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-debug-java-web-app-in-intellij/06-windows-command-prompt-connection-successful-to-remote.png






