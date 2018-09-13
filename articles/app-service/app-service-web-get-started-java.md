---
title: Create your first Java web app in Azure
description: Learn how to run web apps in App Service by deploying a basic Java app.
services: app-service\web
documentationcenter: ''
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 03/26/2018
ms.author: cephalin;robmcm
ms.custom: mvc, devcenter
ms.openlocfilehash: 854ae54992a1389ec7c7f7892c738d070421264d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867451"
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="e45a3-103">Create your first Java web app in Azure</span><span class="sxs-lookup"><span data-stu-id="e45a3-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="e45a3-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="e45a3-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e45a3-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="e45a3-105">This quickstart shows how to deploy a Java web app to App Service by using the [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

> [!NOTE]
>
> <span data-ttu-id="e45a3-106">The steps in this quickstart show how to use the Eclipse IDE to publish a Java web app to App Service, but you can use the IntelliJ IDEA Ultimate Edition or Community Edition.</span><span class="sxs-lookup"><span data-stu-id="e45a3-106">The steps in this quickstart show how to use the Eclipse IDE to publish a Java web app to App Service, but you can use the IntelliJ IDEA Ultimate Edition or Community Edition.</span></span> <span data-ttu-id="e45a3-107">For more information, see [Create a Hello World web app for Azure using IntelliJ](/java/azure/intellij/azure-toolkit-for-intellij-create-hello-world-web-app).</span><span class="sxs-lookup"><span data-stu-id="e45a3-107">For more information, see [Create a Hello World web app for Azure using IntelliJ](/java/azure/intellij/azure-toolkit-for-intellij-create-hello-world-web-app).</span></span>
>

<span data-ttu-id="e45a3-108">When you have completed this quickstart, your application will look similar to the following illustration when you view it in a web browser:</span><span class="sxs-lookup"><span data-stu-id="e45a3-108">When you have completed this quickstart, your application will look similar to the following illustration when you view it in a web browser:</span></span>

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="e45a3-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e45a3-111">Prerequisites</span></span>

<span data-ttu-id="e45a3-112">To complete this quickstart, install:</span><span class="sxs-lookup"><span data-stu-id="e45a3-112">To complete this quickstart, install:</span></span>

* <span data-ttu-id="e45a3-113">The free <a href="http://www.eclipse.org/downloads/" target="_blank">Eclipse IDE for Java EE Developers</a>.</span><span class="sxs-lookup"><span data-stu-id="e45a3-113">The free <a href="http://www.eclipse.org/downloads/" target="_blank">Eclipse IDE for Java EE Developers</a>.</span></span> <span data-ttu-id="e45a3-114">This quickstart uses Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="e45a3-114">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="e45a3-115">The <a href="/java/azure/eclipse/azure-toolkit-for-eclipse-installation" target="_blank">Azure Toolkit for Eclipse</a>.</span><span class="sxs-lookup"><span data-stu-id="e45a3-115">The <a href="/java/azure/eclipse/azure-toolkit-for-eclipse-installation" target="_blank">Azure Toolkit for Eclipse</a>.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e45a3-116">You will need to sign into your Azure account using the Azure Toolkit for Eclipse to complete the steps in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="e45a3-116">You will need to sign into your Azure account using the Azure Toolkit for Eclipse to complete the steps in this quickstart.</span></span> <span data-ttu-id="e45a3-117">To do so, see [Azure Sign In Instructions for the Azure Toolkit for Eclipse](/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="e45a3-117">To do so, see [Azure Sign In Instructions for the Azure Toolkit for Eclipse](/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>
>

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="e45a3-118">Create a dynamic web project in Eclipse</span><span class="sxs-lookup"><span data-stu-id="e45a3-118">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="e45a3-119">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-119">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="e45a3-120">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-120">In the **New Dynamic Web Project** dialog box, name the project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![New Dynamic Web Project dialog box](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="e45a3-122">Add a JSP page</span><span class="sxs-lookup"><span data-stu-id="e45a3-122">Add a JSP page</span></span>

<span data-ttu-id="e45a3-123">If Project Explorer is not displayed, restore it.</span><span class="sxs-lookup"><span data-stu-id="e45a3-123">If Project Explorer is not displayed, restore it.</span></span>

![Java EE workspace for Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="e45a3-125">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span><span class="sxs-lookup"><span data-stu-id="e45a3-125">In Project Explorer, expand the **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="e45a3-126">Right-click **WebContent**, and then select **New** > **JSP File**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-126">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu for a new JSP file in Project Explorer](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="e45a3-128">In the **New JSP File** dialog box:</span><span class="sxs-lookup"><span data-stu-id="e45a3-128">In the **New JSP File** dialog box:</span></span>

* <span data-ttu-id="e45a3-129">Name the file **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-129">Name the file **index.jsp**.</span></span>
* <span data-ttu-id="e45a3-130">Select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-130">Select **Finish**.</span></span>

  ![New JSP File dialog box](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="e45a3-132">In the index.jsp file, replace the `<body></body>` element with the following markup:</span><span class="sxs-lookup"><span data-stu-id="e45a3-132">In the index.jsp file, replace the `<body></body>` element with the following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="e45a3-133">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="e45a3-133">Save the changes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e45a3-134">If you see an error on line 1 that refers to a missing Java Servlet class, you can ignore it.</span><span class="sxs-lookup"><span data-stu-id="e45a3-134">If you see an error on line 1 that refers to a missing Java Servlet class, you can ignore it.</span></span>
> 
> ![Benign Java servlet error](./media/app-service-web-get-started-java/java-servlet-benign-error.png)
>

## <a name="publish-the-web-app-to-azure"></a><span data-ttu-id="e45a3-136">Publish the web app to Azure</span><span class="sxs-lookup"><span data-stu-id="e45a3-136">Publish the web app to Azure</span></span>

<span data-ttu-id="e45a3-137">In Project Explorer, right-click your project, and then select **Azure** > **Publish as Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-137">In Project Explorer, right-click your project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Publish as Azure Web App context menu](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="e45a3-139">If you are prompted with the **Azure Sign In** dialog box, you will need to follow the steps in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse](/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) article to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="e45a3-139">If you are prompted with the **Azure Sign In** dialog box, you will need to follow the steps in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse](/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) article to enter your credentials.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="e45a3-140">Deploy Web App dialog box</span><span class="sxs-lookup"><span data-stu-id="e45a3-140">Deploy Web App dialog box</span></span>

<span data-ttu-id="e45a3-141">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="e45a3-141">After you have signed in to your Azure account, the **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="e45a3-142">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-142">Select **Create**.</span></span>

![Deploy Web App dialog box](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="e45a3-144">Create App Service dialog box</span><span class="sxs-lookup"><span data-stu-id="e45a3-144">Create App Service dialog box</span></span>

<span data-ttu-id="e45a3-145">The **Create App Service** dialog box appears with default values.</span><span class="sxs-lookup"><span data-stu-id="e45a3-145">The **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="e45a3-146">The number **170602185241** shown in the following image is different in your dialog box.</span><span class="sxs-lookup"><span data-stu-id="e45a3-146">The number **170602185241** shown in the following image is different in your dialog box.</span></span>

![Create App Service dialog box](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="e45a3-148">In the **Create App Service** dialog box:</span><span class="sxs-lookup"><span data-stu-id="e45a3-148">In the **Create App Service** dialog box:</span></span>

* <span data-ttu-id="e45a3-149">Enter a unique name for your web app, or keep the generated name.</span><span class="sxs-lookup"><span data-stu-id="e45a3-149">Enter a unique name for your web app, or keep the generated name.</span></span> <span data-ttu-id="e45a3-150">This name must be unique across Azure.</span><span class="sxs-lookup"><span data-stu-id="e45a3-150">This name must be unique across Azure.</span></span> <span data-ttu-id="e45a3-151">The name is part of the URL address for the web app.</span><span class="sxs-lookup"><span data-stu-id="e45a3-151">The name is part of the URL address for the web app.</span></span> <span data-ttu-id="e45a3-152">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="e45a3-152">For example: if the web app name is **MyJavaWebApp**, the URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="e45a3-153">For this quickstart, keep the default web container.</span><span class="sxs-lookup"><span data-stu-id="e45a3-153">For this quickstart, keep the default web container.</span></span>
* <span data-ttu-id="e45a3-154">Select an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e45a3-154">Select an Azure subscription.</span></span>
* <span data-ttu-id="e45a3-155">On the **App service plan** tab:</span><span class="sxs-lookup"><span data-stu-id="e45a3-155">On the **App service plan** tab:</span></span>

  * <span data-ttu-id="e45a3-156">**Create new**: Keep the default, which is the name of the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="e45a3-156">**Create new**: Keep the default, which is the name of the App Service plan.</span></span>
  * <span data-ttu-id="e45a3-157">**Location**: Select **West Europe** or a location near you.</span><span class="sxs-lookup"><span data-stu-id="e45a3-157">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="e45a3-158">**Pricing tier**: Select the free option.</span><span class="sxs-lookup"><span data-stu-id="e45a3-158">**Pricing tier**: Select the free option.</span></span> <span data-ttu-id="e45a3-159">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span><span class="sxs-lookup"><span data-stu-id="e45a3-159">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span></span>

   ![Create App Service dialog box](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="e45a3-161">Resource group tab</span><span class="sxs-lookup"><span data-stu-id="e45a3-161">Resource group tab</span></span>

<span data-ttu-id="e45a3-162">Select the **Resource group** tab. Keep the default generated value for the resource group.</span><span class="sxs-lookup"><span data-stu-id="e45a3-162">Select the **Resource group** tab. Keep the default generated value for the resource group.</span></span>

![Resource group tab](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="e45a3-164">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-164">Select **Create**.</span></span>

<!--
### The JDK tab

Select the **JDK** tab. Keep the default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="e45a3-165">The Azure Toolkit creates the web app and displays a progress dialog box.</span><span class="sxs-lookup"><span data-stu-id="e45a3-165">The Azure Toolkit creates the web app and displays a progress dialog box.</span></span>

![Create App Service Progress dialog box](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="e45a3-167">Deploy Web App dialog box</span><span class="sxs-lookup"><span data-stu-id="e45a3-167">Deploy Web App dialog box</span></span>

<span data-ttu-id="e45a3-168">In the **Deploy Web App** dialog box, select **Deploy to root**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-168">In the **Deploy Web App** dialog box, select **Deploy to root**.</span></span> <span data-ttu-id="e45a3-169">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="e45a3-169">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy to the root, the web app named **MyFirstJavaOnAzureWebApp** is deployed to *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Deploy Web App dialog box](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="e45a3-171">The dialog box shows the Azure, JDK, and web container selections.</span><span class="sxs-lookup"><span data-stu-id="e45a3-171">The dialog box shows the Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="e45a3-172">Select **Deploy** to publish the web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="e45a3-172">Select **Deploy** to publish the web app to Azure.</span></span>

<span data-ttu-id="e45a3-173">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span><span class="sxs-lookup"><span data-stu-id="e45a3-173">When the publishing finishes, select the **Published** link in the **Azure Activity Log** dialog box.</span></span>

![Azure Activity Log dialog box](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="e45a3-175">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="e45a3-175">Congratulations!</span></span> <span data-ttu-id="e45a3-176">You have successfully deployed your web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="e45a3-176">You have successfully deployed your web app to Azure.</span></span> 

!["Hello Azure!"](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-the-web-app"></a><span data-ttu-id="e45a3-179">Update the web app</span><span class="sxs-lookup"><span data-stu-id="e45a3-179">Update the web app</span></span>

<span data-ttu-id="e45a3-180">Change the sample JSP code to a different message.</span><span class="sxs-lookup"><span data-stu-id="e45a3-180">Change the sample JSP code to a different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="e45a3-181">Save the changes.</span><span class="sxs-lookup"><span data-stu-id="e45a3-181">Save the changes.</span></span>

<span data-ttu-id="e45a3-182">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-182">In Project Explorer, right-click the project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="e45a3-183">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span><span class="sxs-lookup"><span data-stu-id="e45a3-183">The **Deploy Web App** dialog box appears and shows the app service that you previously created.</span></span> 

> [!NOTE] 
> <span data-ttu-id="e45a3-184">Select **Deploy to root** each time you publish.</span><span class="sxs-lookup"><span data-stu-id="e45a3-184">Select **Deploy to root** each time you publish.</span></span> 
> 

<span data-ttu-id="e45a3-185">Select the web app and select **Deploy**, which publishes the changes.</span><span class="sxs-lookup"><span data-stu-id="e45a3-185">Select the web app and select **Deploy**, which publishes the changes.</span></span>

<span data-ttu-id="e45a3-186">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span><span class="sxs-lookup"><span data-stu-id="e45a3-186">When the **Publishing** link appears, select it to browse to the web app and see the changes.</span></span>

## <a name="manage-the-web-app"></a><span data-ttu-id="e45a3-187">Manage the web app</span><span class="sxs-lookup"><span data-stu-id="e45a3-187">Manage the web app</span></span>

<span data-ttu-id="e45a3-188">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span><span class="sxs-lookup"><span data-stu-id="e45a3-188">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to see the web app that you created.</span></span>

<span data-ttu-id="e45a3-189">From the left menu, select **Resource Groups**.</span><span class="sxs-lookup"><span data-stu-id="e45a3-189">From the left menu, select **Resource Groups**.</span></span>

![Portal navigation to resource groups](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="e45a3-191">Select the resource group.</span><span class="sxs-lookup"><span data-stu-id="e45a3-191">Select the resource group.</span></span> <span data-ttu-id="e45a3-192">The page shows the resources that you created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="e45a3-192">The page shows the resources that you created in this quickstart.</span></span>

![Resource group](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="e45a3-194">Select the web app (**webapp-170602193915** in the preceding image).</span><span class="sxs-lookup"><span data-stu-id="e45a3-194">Select the web app (**webapp-170602193915** in the preceding image).</span></span>

<span data-ttu-id="e45a3-195">The **Overview** page appears.</span><span class="sxs-lookup"><span data-stu-id="e45a3-195">The **Overview** page appears.</span></span> <span data-ttu-id="e45a3-196">This page gives you a view of how the app is doing.</span><span class="sxs-lookup"><span data-stu-id="e45a3-196">This page gives you a view of how the app is doing.</span></span> <span data-ttu-id="e45a3-197">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="e45a3-197">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="e45a3-198">The tabs on the left side of the page show the different configurations that you can open.</span><span class="sxs-lookup"><span data-stu-id="e45a3-198">The tabs on the left side of the page show the different configurations that you can open.</span></span> 

![App Service page in Azure portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="e45a3-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="e45a3-200">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e45a3-201">Map custom domain</span><span class="sxs-lookup"><span data-stu-id="e45a3-201">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
