---
title: Create a basic Azure web app in IntelliJ | Microsoft Docs
description: This tutorial shows you how to use the Azure Toolkit for IntelliJ to create a Hello World Web App for Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm;asirveda
ms.openlocfilehash: e316ab902fa3319da6e417ff6bda813aba808cf1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552568"
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="f927e-103">Create a basic Azure web app in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="f927e-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="f927e-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="f927e-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="f927e-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span><span class="sxs-lookup"><span data-stu-id="f927e-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="f927e-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span><span class="sxs-lookup"><span data-stu-id="f927e-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Sample Web Page][01]

## <a name="prerequisites"></a><span data-ttu-id="f927e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f927e-108">Prerequisites</span></span>
* <span data-ttu-id="f927e-109">A Java Developer Kit (JDK), v 1.8 or later.</span><span class="sxs-lookup"><span data-stu-id="f927e-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="f927e-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="f927e-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="f927e-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="f927e-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="f927e-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span><span class="sxs-lookup"><span data-stu-id="f927e-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="f927e-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="f927e-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="f927e-114">The [Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="f927e-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="f927e-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="f927e-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="f927e-116">To create a Hello World application</span><span class="sxs-lookup"><span data-stu-id="f927e-116">To create a Hello World application</span></span>
<span data-ttu-id="f927e-117">First, we'll start off with creating a Java project.</span><span class="sxs-lookup"><span data-stu-id="f927e-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="f927e-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="f927e-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![File New Project][02]
2. <span data-ttu-id="f927e-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span><span class="sxs-lookup"><span data-stu-id="f927e-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![New Project Dialog][03a]
   
3. <span data-ttu-id="f927e-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f927e-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="f927e-123">Click **Next** in the New Project dialog box to continue.</span><span class="sxs-lookup"><span data-stu-id="f927e-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Specify JDK Home Directory][03b]
4. <span data-ttu-id="f927e-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f927e-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![New Project Dialog][04]
5. <span data-ttu-id="f927e-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="f927e-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Open Index Page][05c]
6. <span data-ttu-id="f927e-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="f927e-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="f927e-130">within the existing `<body>` element.</span><span class="sxs-lookup"><span data-stu-id="f927e-130">within the existing `<body>` element.</span></span> <span data-ttu-id="f927e-131">Your updated `<body>` content should resemble the following example:</span><span class="sxs-lookup"><span data-stu-id="f927e-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="f927e-132">Save index.jsp.</span><span class="sxs-lookup"><span data-stu-id="f927e-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="f927e-133">To deploy your application to an Azure Web App Container</span><span class="sxs-lookup"><span data-stu-id="f927e-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="f927e-134">There are several ways by which you can deploy a Java web application to Azure.</span><span class="sxs-lookup"><span data-stu-id="f927e-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="f927e-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span><span class="sxs-lookup"><span data-stu-id="f927e-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="f927e-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span><span class="sxs-lookup"><span data-stu-id="f927e-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="f927e-137">As a result, the publishing process for your application will take seconds, not minutes.</span><span class="sxs-lookup"><span data-stu-id="f927e-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="f927e-138">Before you publish your application, you first need to configure your module settings.</span><span class="sxs-lookup"><span data-stu-id="f927e-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="f927e-139">To do so, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="f927e-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="f927e-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span><span class="sxs-lookup"><span data-stu-id="f927e-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="f927e-141">When the context menu appears, click **Open Module Settings**.</span><span class="sxs-lookup"><span data-stu-id="f927e-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Open Module Settings][05a]
2. <span data-ttu-id="f927e-143">When the Project Structure dialog box appears:</span><span class="sxs-lookup"><span data-stu-id="f927e-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="f927e-144">a.</span><span class="sxs-lookup"><span data-stu-id="f927e-144">a.</span></span> <span data-ttu-id="f927e-145">Click **Artifacts** in the list of **Project Settings**.</span><span class="sxs-lookup"><span data-stu-id="f927e-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="f927e-146">b.</span><span class="sxs-lookup"><span data-stu-id="f927e-146">b.</span></span> <span data-ttu-id="f927e-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span><span class="sxs-lookup"><span data-stu-id="f927e-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="f927e-148">c.</span><span class="sxs-lookup"><span data-stu-id="f927e-148">c.</span></span> <span data-ttu-id="f927e-149">Change the **Type** to **Web Application: Archive**.</span><span class="sxs-lookup"><span data-stu-id="f927e-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="f927e-150">d.</span><span class="sxs-lookup"><span data-stu-id="f927e-150">d.</span></span> <span data-ttu-id="f927e-151">Click **OK** to close the Project Structure dialog box.</span><span class="sxs-lookup"><span data-stu-id="f927e-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Open Module Settings][05b]

<span data-ttu-id="f927e-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="f927e-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="f927e-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span><span class="sxs-lookup"><span data-stu-id="f927e-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="f927e-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span><span class="sxs-lookup"><span data-stu-id="f927e-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Azure Publish Context Menu][06]
2. <span data-ttu-id="f927e-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span><span class="sxs-lookup"><span data-stu-id="f927e-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="f927e-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span><span class="sxs-lookup"><span data-stu-id="f927e-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="f927e-159">When this happens, continue to follow the sign in instructions.)</span><span class="sxs-lookup"><span data-stu-id="f927e-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Azure Log In Dialog][07]
3. <span data-ttu-id="f927e-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="f927e-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="f927e-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="f927e-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Manage Subscriptions][08]
4. <span data-ttu-id="f927e-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span><span class="sxs-lookup"><span data-stu-id="f927e-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![App Containers][09]
5. <span data-ttu-id="f927e-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="f927e-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="f927e-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span><span class="sxs-lookup"><span data-stu-id="f927e-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="f927e-168">Click **+**</span><span class="sxs-lookup"><span data-stu-id="f927e-168">Click **+**</span></span>
      
       ![Add App Container][10]
   2. <span data-ttu-id="f927e-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span><span class="sxs-lookup"><span data-stu-id="f927e-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![New App Container][11a]
   3. <span data-ttu-id="f927e-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span><span class="sxs-lookup"><span data-stu-id="f927e-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="f927e-173">Note that the name must be available and conform to Azure Web App naming requirements.</span><span class="sxs-lookup"><span data-stu-id="f927e-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="f927e-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span><span class="sxs-lookup"><span data-stu-id="f927e-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="f927e-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="f927e-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="f927e-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span><span class="sxs-lookup"><span data-stu-id="f927e-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="f927e-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span><span class="sxs-lookup"><span data-stu-id="f927e-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="f927e-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span><span class="sxs-lookup"><span data-stu-id="f927e-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="f927e-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span><span class="sxs-lookup"><span data-stu-id="f927e-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="f927e-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span><span class="sxs-lookup"><span data-stu-id="f927e-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="f927e-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f927e-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="f927e-182">The **New Resource Group** dialog box will be displayed:</span><span class="sxs-lookup"><span data-stu-id="f927e-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![New Resource Group][12]
      * <span data-ttu-id="f927e-184">In the the **Name** textbox, specify a name for your new Resource Group.</span><span class="sxs-lookup"><span data-stu-id="f927e-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="f927e-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span><span class="sxs-lookup"><span data-stu-id="f927e-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="f927e-186">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f927e-186">Click **OK**.</span></span>
   7. <span data-ttu-id="f927e-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span><span class="sxs-lookup"><span data-stu-id="f927e-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="f927e-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span><span class="sxs-lookup"><span data-stu-id="f927e-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="f927e-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span><span class="sxs-lookup"><span data-stu-id="f927e-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="f927e-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span><span class="sxs-lookup"><span data-stu-id="f927e-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="f927e-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f927e-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="f927e-192">The **New App Service Plan** dialog box will be displayed:</span><span class="sxs-lookup"><span data-stu-id="f927e-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![New App Service Plan][13]
      * <span data-ttu-id="f927e-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span><span class="sxs-lookup"><span data-stu-id="f927e-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="f927e-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span><span class="sxs-lookup"><span data-stu-id="f927e-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="f927e-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span><span class="sxs-lookup"><span data-stu-id="f927e-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="f927e-197">For testing purposes you can choose **Free**.</span><span class="sxs-lookup"><span data-stu-id="f927e-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="f927e-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span><span class="sxs-lookup"><span data-stu-id="f927e-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="f927e-199">For testing purposes you can choose **Small**.</span><span class="sxs-lookup"><span data-stu-id="f927e-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="f927e-200">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f927e-200">Click **OK**.</span></span>
   8. <span data-ttu-id="f927e-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span><span class="sxs-lookup"><span data-stu-id="f927e-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="f927e-202">However, you can select a different version and distribution of the JVM.</span><span class="sxs-lookup"><span data-stu-id="f927e-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="f927e-203">To do so, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="f927e-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="f927e-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f927e-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="f927e-205">You can choose from one of the following options:</span><span class="sxs-lookup"><span data-stu-id="f927e-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="f927e-206">Deploy the default JDK which is offered by Azure</span><span class="sxs-lookup"><span data-stu-id="f927e-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="f927e-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span><span class="sxs-lookup"><span data-stu-id="f927e-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="f927e-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span><span class="sxs-lookup"><span data-stu-id="f927e-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![New App Container JDK Tab][11b]
   9. <span data-ttu-id="f927e-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span><span class="sxs-lookup"><span data-stu-id="f927e-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![New App Container][14]
   10. <span data-ttu-id="f927e-212">Click **OK** to complete the creation of your new Web App container.</span><span class="sxs-lookup"><span data-stu-id="f927e-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="f927e-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span><span class="sxs-lookup"><span data-stu-id="f927e-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="f927e-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span><span class="sxs-lookup"><span data-stu-id="f927e-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="f927e-215">By default, your application will be deployed as a subdirectory of the application server.</span><span class="sxs-lookup"><span data-stu-id="f927e-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="f927e-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span><span class="sxs-lookup"><span data-stu-id="f927e-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Deploy To Azure][15]
7. <span data-ttu-id="f927e-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span><span class="sxs-lookup"><span data-stu-id="f927e-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Progress Indicator][16]
   
    <span data-ttu-id="f927e-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span><span class="sxs-lookup"><span data-stu-id="f927e-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="f927e-221">When your application ready, you will see a link named **Published** in the **Status** column.</span><span class="sxs-lookup"><span data-stu-id="f927e-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="f927e-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span><span class="sxs-lookup"><span data-stu-id="f927e-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="f927e-223">Browsing to your Web App on Azure</span><span class="sxs-lookup"><span data-stu-id="f927e-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="f927e-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span><span class="sxs-lookup"><span data-stu-id="f927e-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="f927e-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f927e-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="f927e-226">If you have not previously logged in, it will prompt you to do so.</span><span class="sxs-lookup"><span data-stu-id="f927e-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="f927e-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span><span class="sxs-lookup"><span data-stu-id="f927e-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="f927e-228">Expand the **Azure** node.</span><span class="sxs-lookup"><span data-stu-id="f927e-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="f927e-229">Expand the **Web Apps** node.</span><span class="sxs-lookup"><span data-stu-id="f927e-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="f927e-230">Right-click the desired Web App.</span><span class="sxs-lookup"><span data-stu-id="f927e-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="f927e-231">When the context menu appears, click **Open in Browser**.</span><span class="sxs-lookup"><span data-stu-id="f927e-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Browse Web App][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="f927e-233">Updating your web app</span><span class="sxs-lookup"><span data-stu-id="f927e-233">Updating your web app</span></span>
<span data-ttu-id="f927e-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span><span class="sxs-lookup"><span data-stu-id="f927e-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="f927e-235">You can update the deployment of an existing Java Web App.</span><span class="sxs-lookup"><span data-stu-id="f927e-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="f927e-236">You can publish an additional Java application to the same Web App Container.</span><span class="sxs-lookup"><span data-stu-id="f927e-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="f927e-237">In either case, the process is identical and takes only a few seconds:</span><span class="sxs-lookup"><span data-stu-id="f927e-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="f927e-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span><span class="sxs-lookup"><span data-stu-id="f927e-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="f927e-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span><span class="sxs-lookup"><span data-stu-id="f927e-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="f927e-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span><span class="sxs-lookup"><span data-stu-id="f927e-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="f927e-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f927e-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="f927e-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span><span class="sxs-lookup"><span data-stu-id="f927e-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="f927e-243">Starting, stopping, or restarting an existing web app</span><span class="sxs-lookup"><span data-stu-id="f927e-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="f927e-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span><span class="sxs-lookup"><span data-stu-id="f927e-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="f927e-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f927e-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="f927e-246">If you have not previously logged in, it will prompt you to do so.</span><span class="sxs-lookup"><span data-stu-id="f927e-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="f927e-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span><span class="sxs-lookup"><span data-stu-id="f927e-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="f927e-248">Expand the **Azure** node.</span><span class="sxs-lookup"><span data-stu-id="f927e-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="f927e-249">Expand the **Web Apps** node.</span><span class="sxs-lookup"><span data-stu-id="f927e-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="f927e-250">Right-click the desired Web App.</span><span class="sxs-lookup"><span data-stu-id="f927e-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="f927e-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span><span class="sxs-lookup"><span data-stu-id="f927e-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="f927e-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span><span class="sxs-lookup"><span data-stu-id="f927e-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Stop Web App][18]

## <a name="next-steps"></a><span data-ttu-id="f927e-254">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f927e-254">Next Steps</span></span>
<span data-ttu-id="f927e-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span><span class="sxs-lookup"><span data-stu-id="f927e-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="f927e-256">[Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f927e-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f927e-257">[Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f927e-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="f927e-258">[Create a Hello World Web App for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f927e-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="f927e-259">[What's New in the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="f927e-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="f927e-260">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f927e-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f927e-261">[Installing the Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f927e-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="f927e-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span><span class="sxs-lookup"><span data-stu-id="f927e-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="f927e-263">[What's New in the Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="f927e-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="f927e-264">See Also</span><span class="sxs-lookup"><span data-stu-id="f927e-264">See Also</span></span>
<span data-ttu-id="f927e-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="f927e-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="f927e-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span><span class="sxs-lookup"><span data-stu-id="f927e-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Installing the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[What's New in the Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[What's New in the Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Web Apps Overview]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png






















