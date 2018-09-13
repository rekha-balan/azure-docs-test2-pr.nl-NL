---
title: Azure Service Fabric plug-in for Eclipse | Microsoft Docs
description: Get started with the Service Fabric plug-in for Eclipse.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: ''
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/06/2017
ms.author: saysa
ms.openlocfilehash: 65826ede7d96d5b2c247474a95b53e79155581f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552525"
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="8882d-103">Service Fabric plug-in for Eclipse Java application development</span><span class="sxs-lookup"><span data-stu-id="8882d-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="8882d-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span><span class="sxs-lookup"><span data-stu-id="8882d-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="8882d-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8882d-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="8882d-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="8882d-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="8882d-107">Install or update the Service Fabric plug-in in Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="8882d-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="8882d-108">You can install a Service Fabric plug-in in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8882d-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="8882d-109">The plug-in can help simplify the process of building and deploying Java services.</span><span class="sxs-lookup"><span data-stu-id="8882d-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="8882d-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span><span class="sxs-lookup"><span data-stu-id="8882d-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="8882d-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span><span class="sxs-lookup"><span data-stu-id="8882d-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="8882d-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="8882d-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="8882d-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span><span class="sxs-lookup"><span data-stu-id="8882d-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="8882d-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span><span class="sxs-lookup"><span data-stu-id="8882d-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="8882d-115">In the **Work with** box, enter **http://dl.windowsazure.com/eclipse/servicefabric**.</span><span class="sxs-lookup"><span data-stu-id="8882d-115">In the **Work with** box, enter **http://dl.windowsazure.com/eclipse/servicefabric**.</span></span>
  2.    <span data-ttu-id="8882d-116">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8882d-116">Click **Add**.</span></span>
    <span data-ttu-id="8882d-117">![Service Fabric plug-in for Eclipse Neon][sf-eclipse-plugin-install]</span><span class="sxs-lookup"><span data-stu-id="8882d-117">![Service Fabric plug-in for Eclipse Neon][sf-eclipse-plugin-install]</span></span>
  3.    <span data-ttu-id="8882d-118">Select the Service Fabric plug-in, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8882d-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="8882d-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span><span class="sxs-lookup"><span data-stu-id="8882d-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="8882d-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span><span class="sxs-lookup"><span data-stu-id="8882d-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="8882d-121">To check for available updates, go to **Help** > **Installation Details**.</span><span class="sxs-lookup"><span data-stu-id="8882d-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="8882d-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="8882d-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="8882d-123">Available updates will be installed.</span><span class="sxs-lookup"><span data-stu-id="8882d-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="8882d-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span><span class="sxs-lookup"><span data-stu-id="8882d-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="8882d-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span><span class="sxs-lookup"><span data-stu-id="8882d-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="8882d-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span><span class="sxs-lookup"><span data-stu-id="8882d-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="8882d-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.windowsazure.com/eclipse/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="8882d-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.windowsazure.com/eclipse/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="8882d-128">Create a Service Fabric application in Eclipse</span><span class="sxs-lookup"><span data-stu-id="8882d-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="8882d-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span><span class="sxs-lookup"><span data-stu-id="8882d-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="8882d-130">Select  **Service Fabric Project**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8882d-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Service Fabric New Project page 1][create-application/p1]

2.  <span data-ttu-id="8882d-132">Enter a name for your project, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8882d-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Service Fabric New Project page 2][create-application/p2]

3.  <span data-ttu-id="8882d-134">In the list of templates, select **Service Template**.</span><span class="sxs-lookup"><span data-stu-id="8882d-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="8882d-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8882d-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Service Fabric New Project page 3][create-application/p3]

4.  <span data-ttu-id="8882d-137">Enter the service name and service details, and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="8882d-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Service Fabric New Project page 4][create-application/p4]

5. <span data-ttu-id="8882d-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="8882d-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Service Fabric New Project page 5][create-application/p5]

6.  <span data-ttu-id="8882d-141">Your new project looks like this:</span><span class="sxs-lookup"><span data-stu-id="8882d-141">Your new project looks like this:</span></span>

    ![Service Fabric New Project page 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="8882d-143">Build and deploy a Service Fabric application in Eclipse</span><span class="sxs-lookup"><span data-stu-id="8882d-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="8882d-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="8882d-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Service Fabric right-click menu][publish/RightClick]

2. <span data-ttu-id="8882d-146">In the submenu, select the option you want:</span><span class="sxs-lookup"><span data-stu-id="8882d-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="8882d-147">To build the application without cleaning, click **Build Application**.</span><span class="sxs-lookup"><span data-stu-id="8882d-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="8882d-148">To do a clean build of the application, click **Rebuild Application**.</span><span class="sxs-lookup"><span data-stu-id="8882d-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="8882d-149">To clean the application of built artifacts, click **Clean Application**.</span><span class="sxs-lookup"><span data-stu-id="8882d-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="8882d-150">From this menu, you also can deploy, undeploy, and publish your application:</span><span class="sxs-lookup"><span data-stu-id="8882d-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="8882d-151">To deploy to your local cluster, click **Deploy Application**.</span><span class="sxs-lookup"><span data-stu-id="8882d-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="8882d-152">In the **Publish Application** dialog box, select a publish profile:</span><span class="sxs-lookup"><span data-stu-id="8882d-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="8882d-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="8882d-153">**Local.json**</span></span>
        -  <span data-ttu-id="8882d-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="8882d-154">**Cloud.json**</span></span>

     <span data-ttu-id="8882d-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span><span class="sxs-lookup"><span data-stu-id="8882d-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Service Fabric Publish menu][publish/Publish]

<span data-ttu-id="8882d-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span><span class="sxs-lookup"><span data-stu-id="8882d-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="8882d-158">Go to **Run** > **Run Configurations**.</span><span class="sxs-lookup"><span data-stu-id="8882d-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="8882d-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span><span class="sxs-lookup"><span data-stu-id="8882d-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="8882d-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span><span class="sxs-lookup"><span data-stu-id="8882d-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="8882d-161">The default is **local**.</span><span class="sxs-lookup"><span data-stu-id="8882d-161">The default is **local**.</span></span> <span data-ttu-id="8882d-162">To deploy to a remote or cloud cluster, select **cloud**.</span><span class="sxs-lookup"><span data-stu-id="8882d-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="8882d-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span><span class="sxs-lookup"><span data-stu-id="8882d-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="8882d-164">You can add or update endpoint details and security credentials.</span><span class="sxs-lookup"><span data-stu-id="8882d-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="8882d-165">Ensure that **Working Directory** points to the application you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="8882d-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="8882d-166">To change the application, click the **Workspace** button, and then select the application you want.</span><span class="sxs-lookup"><span data-stu-id="8882d-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="8882d-167">Click **Apply**, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="8882d-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="8882d-168">Your application builds and deploys within a few moments.</span><span class="sxs-lookup"><span data-stu-id="8882d-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="8882d-169">You can monitor the deployment status in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="8882d-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="8882d-170">Add a Service Fabric service to your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="8882d-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="8882d-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="8882d-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="8882d-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="8882d-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Service Fabric Add Service page 1][add-service/p1]

2.  <span data-ttu-id="8882d-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span><span class="sxs-lookup"><span data-stu-id="8882d-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="8882d-175">Select the service template you want to add to your project, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8882d-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Service Fabric Add Service page 2][add-service/p2]

4.  <span data-ttu-id="8882d-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span><span class="sxs-lookup"><span data-stu-id="8882d-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Service Fabric Add Service page 3][add-service/p3]

5.  <span data-ttu-id="8882d-179">After the service is added, your overall project structure looks similar to the following project:</span><span class="sxs-lookup"><span data-stu-id="8882d-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Service Fabric Add Service page 4][add-service/p4]

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="8882d-181">Upgrade your Service Fabric Java application</span><span class="sxs-lookup"><span data-stu-id="8882d-181">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="8882d-182">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="8882d-182">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="8882d-183">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span><span class="sxs-lookup"><span data-stu-id="8882d-183">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="8882d-184">The application type is **App1AppicationType**, and the application version is 1.0.</span><span class="sxs-lookup"><span data-stu-id="8882d-184">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="8882d-185">Now, you want to upgrade your application without interrupting availability.</span><span class="sxs-lookup"><span data-stu-id="8882d-185">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="8882d-186">First, make any changes to your application, and then rebuild the modified service.</span><span class="sxs-lookup"><span data-stu-id="8882d-186">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="8882d-187">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span><span class="sxs-lookup"><span data-stu-id="8882d-187">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="8882d-188">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span><span class="sxs-lookup"><span data-stu-id="8882d-188">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="8882d-189">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span><span class="sxs-lookup"><span data-stu-id="8882d-189">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="8882d-190">Then, use it to upgrade your application as needed.</span><span class="sxs-lookup"><span data-stu-id="8882d-190">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="8882d-191">Go to **Run** > **Run Configurations**.</span><span class="sxs-lookup"><span data-stu-id="8882d-191">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="8882d-192">In the left pane, click the small arrow to the left of **Gradle Project**.</span><span class="sxs-lookup"><span data-stu-id="8882d-192">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="8882d-193">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span><span class="sxs-lookup"><span data-stu-id="8882d-193">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="8882d-194">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="8882d-194">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="8882d-195">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8882d-195">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="8882d-196">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span><span class="sxs-lookup"><span data-stu-id="8882d-196">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="8882d-197">It also gets the latest updated application type version from the application manifest file.</span><span class="sxs-lookup"><span data-stu-id="8882d-197">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="8882d-198">The application upgrade takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="8882d-198">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="8882d-199">You can monitor the application upgrade in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="8882d-199">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png

[create-application/p1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship













