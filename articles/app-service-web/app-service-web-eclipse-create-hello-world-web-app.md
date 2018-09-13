---
title: Create a basic Azure web app using Eclipse | Microsoft Docs
description: This tutorial shows you how to use the Azure Toolkit for Eclipse to create a Hello World Web App for Azure.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm;asirveda
ms.openlocfilehash: a8e99f54d22a6dc0dd56aebf71ce37cea0fd14da
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550792"
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="1b23a-103">Create a basic Azure web app using Eclipse</span><span class="sxs-lookup"><span data-stu-id="1b23a-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="1b23a-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="1b23a-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="1b23a-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span><span class="sxs-lookup"><span data-stu-id="1b23a-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="1b23a-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span><span class="sxs-lookup"><span data-stu-id="1b23a-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Preview of Hello World app][01]

## <a name="prerequisites"></a><span data-ttu-id="1b23a-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b23a-108">Prerequisites</span></span>
* <span data-ttu-id="1b23a-109">A Java Developer Kit (JDK), v 1.8 or later.</span><span class="sxs-lookup"><span data-stu-id="1b23a-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="1b23a-110">Eclipse IDE for Java EE Developers, Luna or later.</span><span class="sxs-lookup"><span data-stu-id="1b23a-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="1b23a-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="1b23a-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="1b23a-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span><span class="sxs-lookup"><span data-stu-id="1b23a-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="1b23a-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="1b23a-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="1b23a-114">The [Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="1b23a-114">The [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="1b23a-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="1b23a-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for Eclipse].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="1b23a-116">To create a Hello World application</span><span class="sxs-lookup"><span data-stu-id="1b23a-116">To create a Hello World application</span></span>
<span data-ttu-id="1b23a-117">First, we'll start off with creating a Java project.</span><span class="sxs-lookup"><span data-stu-id="1b23a-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="1b23a-118">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-118">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="1b23a-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span><span class="sxs-lookup"><span data-stu-id="1b23a-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="1b23a-120">For purposes of this tutorial, name the project **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-120">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="1b23a-121">Your screen will appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="1b23a-121">Your screen will appear similar to the following:</span></span>
   
    ![Creating a new Dynamic Web Project][02]
3. <span data-ttu-id="1b23a-123">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-123">Click **Finish**.</span></span>
4. <span data-ttu-id="1b23a-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="1b23a-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="1b23a-126">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-126">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="1b23a-127">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-127">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="1b23a-128">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="1b23a-128">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="1b23a-129">within the existing `<body>` element.</span><span class="sxs-lookup"><span data-stu-id="1b23a-129">within the existing `<body>` element.</span></span> <span data-ttu-id="1b23a-130">Your updated `<body>` content should resemble the following example:</span><span class="sxs-lookup"><span data-stu-id="1b23a-130">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="1b23a-131">Save index.jsp.</span><span class="sxs-lookup"><span data-stu-id="1b23a-131">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="1b23a-132">To deploy your application to an Azure Web App Container</span><span class="sxs-lookup"><span data-stu-id="1b23a-132">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="1b23a-133">There are several ways by which you can deploy a Java web application to Azure.</span><span class="sxs-lookup"><span data-stu-id="1b23a-133">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="1b23a-134">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span><span class="sxs-lookup"><span data-stu-id="1b23a-134">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="1b23a-135">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span><span class="sxs-lookup"><span data-stu-id="1b23a-135">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="1b23a-136">As a result, the publishing process for your application will take seconds, not minutes.</span><span class="sxs-lookup"><span data-stu-id="1b23a-136">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="1b23a-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="1b23a-138">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span><span class="sxs-lookup"><span data-stu-id="1b23a-138">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Publish as Azure Web App][03]
   
    <span data-ttu-id="1b23a-140">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span><span class="sxs-lookup"><span data-stu-id="1b23a-140">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Publish as Azure Web App][14]
3. <span data-ttu-id="1b23a-142">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span><span class="sxs-lookup"><span data-stu-id="1b23a-142">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
    ![Azure Sign In dialog box][04]
   
    <span data-ttu-id="1b23a-144">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span><span class="sxs-lookup"><span data-stu-id="1b23a-144">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="1b23a-145">When this happens, continue following the sign in instructions.</span><span class="sxs-lookup"><span data-stu-id="1b23a-145">When this happens, continue following the sign in instructions.</span></span>
4. <span data-ttu-id="1b23a-146">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span><span class="sxs-lookup"><span data-stu-id="1b23a-146">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="1b23a-147">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span><span class="sxs-lookup"><span data-stu-id="1b23a-147">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="1b23a-148">When you have selected your subscriptions, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Manage Subscriptions dialog box][05]
5. <span data-ttu-id="1b23a-150">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span><span class="sxs-lookup"><span data-stu-id="1b23a-150">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Deploy to Azure Web App Container dialog box][06]
6. <span data-ttu-id="1b23a-152">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span><span class="sxs-lookup"><span data-stu-id="1b23a-152">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="1b23a-153">Otherwise, select an existing Web App Container and skip to step 7 below.</span><span class="sxs-lookup"><span data-stu-id="1b23a-153">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   1. <span data-ttu-id="1b23a-154">Click **New...**</span><span class="sxs-lookup"><span data-stu-id="1b23a-154">Click **New...**</span></span>
      
       ![Deploy to Azure Web App Container dialog box][15]
   2. <span data-ttu-id="1b23a-156">The **New Web App Container** dialog box will be displayed:</span><span class="sxs-lookup"><span data-stu-id="1b23a-156">The **New Web App Container** dialog box will be displayed:</span></span>
      
       ![New Web App Container dialog box][07a]
   3. <span data-ttu-id="1b23a-158">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b23a-158">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="1b23a-159">(Note that the name must be available and conform to Azure Web App naming requirements.)</span><span class="sxs-lookup"><span data-stu-id="1b23a-159">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="1b23a-160">In the **Web Container** drop-down menu, select the appropriate software for your application.</span><span class="sxs-lookup"><span data-stu-id="1b23a-160">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="1b23a-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="1b23a-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="1b23a-162">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span><span class="sxs-lookup"><span data-stu-id="1b23a-162">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="1b23a-163">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span><span class="sxs-lookup"><span data-stu-id="1b23a-163">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="1b23a-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span><span class="sxs-lookup"><span data-stu-id="1b23a-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="1b23a-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span><span class="sxs-lookup"><span data-stu-id="1b23a-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="1b23a-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span><span class="sxs-lookup"><span data-stu-id="1b23a-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="1b23a-167">Click **New...**</span><span class="sxs-lookup"><span data-stu-id="1b23a-167">Click **New...**</span></span>
      * <span data-ttu-id="1b23a-168">The **New Resource Group** dialog box will be displayed:</span><span class="sxs-lookup"><span data-stu-id="1b23a-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![New Resource Group dialog box][08]
      * <span data-ttu-id="1b23a-170">In the the **Name** textbox, specify a name for your new Resource Group.</span><span class="sxs-lookup"><span data-stu-id="1b23a-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="1b23a-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span><span class="sxs-lookup"><span data-stu-id="1b23a-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="1b23a-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span><span class="sxs-lookup"><span data-stu-id="1b23a-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="1b23a-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span><span class="sxs-lookup"><span data-stu-id="1b23a-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="1b23a-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span><span class="sxs-lookup"><span data-stu-id="1b23a-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
        
        * <span data-ttu-id="1b23a-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span><span class="sxs-lookup"><span data-stu-id="1b23a-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="1b23a-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1b23a-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="1b23a-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span><span class="sxs-lookup"><span data-stu-id="1b23a-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![New Web App Container dialog box][07b]
   7. <span data-ttu-id="1b23a-179">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-179">Click **OK**.</span></span>
   8. <span data-ttu-id="1b23a-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span><span class="sxs-lookup"><span data-stu-id="1b23a-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="1b23a-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span><span class="sxs-lookup"><span data-stu-id="1b23a-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="1b23a-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span><span class="sxs-lookup"><span data-stu-id="1b23a-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="1b23a-183">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:</span><span class="sxs-lookup"><span data-stu-id="1b23a-183">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="1b23a-184">Click **New...**</span><span class="sxs-lookup"><span data-stu-id="1b23a-184">Click **New...**</span></span>
      * <span data-ttu-id="1b23a-185">The **New App Service Plan** dialog box will be displayed:</span><span class="sxs-lookup"><span data-stu-id="1b23a-185">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![New App Service Plan dialog box][09]
      * <span data-ttu-id="1b23a-187">In the the **Name** textbox, specify a name for your new App Service Plan.</span><span class="sxs-lookup"><span data-stu-id="1b23a-187">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="1b23a-188">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span><span class="sxs-lookup"><span data-stu-id="1b23a-188">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="1b23a-189">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span><span class="sxs-lookup"><span data-stu-id="1b23a-189">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="1b23a-190">For testing purposes you can choose **Free**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="1b23a-191">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span><span class="sxs-lookup"><span data-stu-id="1b23a-191">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="1b23a-192">For testing purposes you can choose **Small**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="1b23a-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span><span class="sxs-lookup"><span data-stu-id="1b23a-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![New Web App Container dialog box][10]
   10. <span data-ttu-id="1b23a-195">Click **OK** to complete the creation of your new Web App container.</span><span class="sxs-lookup"><span data-stu-id="1b23a-195">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="1b23a-196">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span><span class="sxs-lookup"><span data-stu-id="1b23a-196">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
7. <span data-ttu-id="1b23a-197">You are now ready to complete the initial deployment of your Web App to Azure:</span><span class="sxs-lookup"><span data-stu-id="1b23a-197">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
    ![Deploy to Azure Web App Container dialog box][11]
   
    <span data-ttu-id="1b23a-199">Click **OK** to deploy your Java application to the selected Web App container.</span><span class="sxs-lookup"><span data-stu-id="1b23a-199">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
    <span data-ttu-id="1b23a-200">By default, your application will be deployed as a subdirectory of the application server.</span><span class="sxs-lookup"><span data-stu-id="1b23a-200">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="1b23a-201">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-201">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="1b23a-202">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span><span class="sxs-lookup"><span data-stu-id="1b23a-202">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Azure Activity Log][12]
   
    <span data-ttu-id="1b23a-204">The process of deploying your Web App to Azure should take only a few seconds to complete.</span><span class="sxs-lookup"><span data-stu-id="1b23a-204">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="1b23a-205">When your application ready, you will see a link named **Published** in the **Status** column.</span><span class="sxs-lookup"><span data-stu-id="1b23a-205">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="1b23a-206">When you click the link, it will take you to your deployed Web App's home page.</span><span class="sxs-lookup"><span data-stu-id="1b23a-206">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="1b23a-207">Updating your web app</span><span class="sxs-lookup"><span data-stu-id="1b23a-207">Updating your web app</span></span>
<span data-ttu-id="1b23a-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span><span class="sxs-lookup"><span data-stu-id="1b23a-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="1b23a-209">You can update the deployment of an existing Java Web App.</span><span class="sxs-lookup"><span data-stu-id="1b23a-209">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="1b23a-210">You can publish an additional Java application to the same Web App Container.</span><span class="sxs-lookup"><span data-stu-id="1b23a-210">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="1b23a-211">In either case, the process is identical and takes only a few seconds:</span><span class="sxs-lookup"><span data-stu-id="1b23a-211">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="1b23a-212">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span><span class="sxs-lookup"><span data-stu-id="1b23a-212">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="1b23a-213">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span><span class="sxs-lookup"><span data-stu-id="1b23a-213">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="1b23a-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span><span class="sxs-lookup"><span data-stu-id="1b23a-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="1b23a-215">Select the one you want to publish or re-publish your Java application to and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-215">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="1b23a-216">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span><span class="sxs-lookup"><span data-stu-id="1b23a-216">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="1b23a-217">Starting, stopping, or restarting an existing web app</span><span class="sxs-lookup"><span data-stu-id="1b23a-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="1b23a-218">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span><span class="sxs-lookup"><span data-stu-id="1b23a-218">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="1b23a-219">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-219">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="1b23a-220">If you have not previously logged in, it will prompt you to do so.</span><span class="sxs-lookup"><span data-stu-id="1b23a-220">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="1b23a-221">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span><span class="sxs-lookup"><span data-stu-id="1b23a-221">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="1b23a-222">Expand the **Azure** node.</span><span class="sxs-lookup"><span data-stu-id="1b23a-222">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="1b23a-223">Expand the **Web Apps** node.</span><span class="sxs-lookup"><span data-stu-id="1b23a-223">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="1b23a-224">Right-click the desired Web App.</span><span class="sxs-lookup"><span data-stu-id="1b23a-224">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="1b23a-225">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span><span class="sxs-lookup"><span data-stu-id="1b23a-225">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="1b23a-226">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span><span class="sxs-lookup"><span data-stu-id="1b23a-226">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Stopping an Existing Web App][13]

## <a name="next-steps"></a><span data-ttu-id="1b23a-228">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1b23a-228">Next Steps</span></span>
<span data-ttu-id="1b23a-229">For more information about the Azure Toolkits for Java IDEs, see the following links:</span><span class="sxs-lookup"><span data-stu-id="1b23a-229">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="1b23a-230">[Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b23a-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1b23a-231">[Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b23a-231">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="1b23a-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span><span class="sxs-lookup"><span data-stu-id="1b23a-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="1b23a-233">[What's New in the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="1b23a-233">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="1b23a-234">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b23a-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1b23a-235">[Installing the Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b23a-235">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="1b23a-236">[Create a Hello World Web App for Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b23a-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="1b23a-237">[What's New in the Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="1b23a-237">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="1b23a-238">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="1b23a-238">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="1b23a-239">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span><span class="sxs-lookup"><span data-stu-id="1b23a-239">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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

[01]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
















