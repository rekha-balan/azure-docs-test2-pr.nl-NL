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
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Service Fabric plug-in for Eclipse Java application development
Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers. In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric. Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a>Install or update the Service Fabric plug-in in Eclipse Neon
You can install a Service Fabric plug-in in Eclipse. The plug-in can help simplify the process of building and deploying Java services.

1.  Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:
    -   To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.
    -   To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].
    -   To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.

2.  To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.
  1.    In the **Work with** box, enter **http://dl.windowsazure.com/eclipse/servicefabric**.
  2.    Click **Add**.
    ![Service Fabric plug-in for Eclipse Neon][sf-eclipse-plugin-install]
  3.    Select the Service Fabric plug-in, and then click **Next**.
  4.    Complete the installation steps, and then accept the Microsoft Software License Terms.

If you already have the Service Fabric plug-in installed, make sure that you have the latest version. To check for available updates, go to **Help** > **Installation Details**. In the list of installed plug-ins, select Service Fabric, and then click **Update**. Available updates will be installed.

> [!NOTE]
> If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting. Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance. To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**. Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.windowsazure.com/eclipse/servicefabric).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Create a Service Fabric application in Eclipse

1.  In Eclipse Neon, go to **File** > **New** > **Other**. Select  **Service Fabric Project**, and then click **Next**.

    ![Service Fabric New Project page 1][create-application/p1]

2.  Enter a name for your project, and then click **Next**.

    ![Service Fabric New Project page 2][create-application/p2]

3.  In the list of templates, select **Service Template**. Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.

    ![Service Fabric New Project page 3][create-application/p3]

4.  Enter the service name and service details, and then click **Finish**.

    ![Service Fabric New Project page 4][create-application/p4]

5. When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.

    ![Service Fabric New Project page 5][create-application/p5]

6.  Your new project looks like this:

    ![Service Fabric New Project page 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Build and deploy a Service Fabric application in Eclipse

1.  Right-click your new Service Fabric application, and then select **Service Fabric**.

    ![Service Fabric right-click menu][publish/RightClick]

2. In the submenu, select the option you want:
    -   To build the application without cleaning, click **Build Application**.
    -   To do a clean build of the application, click **Rebuild Application**.
    -   To clean the application of built artifacts, click **Clean Application**.

3.  From this menu, you also can deploy, undeploy, and publish your application:
    -   To deploy to your local cluster, click **Deploy Application**.
    -   In the **Publish Application** dialog box, select a publish profile:
        -  **Local.json**
        -  **Cloud.json**

     These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.

  ![Service Fabric Publish menu][publish/Publish]

An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.

  1.    Go to **Run** > **Run Configurations**.
  2.    Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.
  3.    In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.  The default is **local**. To deploy to a remote or cloud cluster, select **cloud**.
  4.    To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed. You can add or update endpoint details and security credentials.
  5.    Ensure that **Working Directory** points to the application you want to deploy. To change the application, click the **Workspace** button, and then select the application you want.
  6.    Click **Apply**, and then click **Run**.

Your application builds and deploys within a few moments. You can monitor the deployment status in Service Fabric Explorer.  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a>Add a Service Fabric service to your Service Fabric application

To add a Service Fabric service to an existing Service Fabric application, do the following steps:

1.  Right-click the project you want to add a service to, and then click **Service Fabric**.

    ![Service Fabric Add Service page 1][add-service/p1]

2.  Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.
3.  Select the service template you want to add to your project, and then click **Next**.

    ![Service Fabric Add Service page 2][add-service/p2]

4.  Enter the service name (and other details, as needed), and then click the **Add Service** button.  

    ![Service Fabric Add Service page 3][add-service/p3]

5.  After the service is added, your overall project structure looks similar to the following project:

    ![Service Fabric Add Service page 4][add-service/p4]

## <a name="upgrade-your-service-fabric-java-application"></a>Upgrade your Service Fabric Java application

For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse. You deployed it by using the plug-in to create an application named **fabric:/App1Application**. The application type is **App1AppicationType**, and the application version is 1.0. Now, you want to upgrade your application without interrupting availability.

First, make any changes to your application, and then rebuild the modified service. Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant). Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.  

To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile. Then, use it to upgrade your application as needed.

1.  Go to **Run** > **Run Configurations**. In the left pane, click the small arrow to the left of **Gradle Project**.
2.  Right-click **ServiceFabricDeployer**, and then select **Duplicate**. Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.
3.  In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.

This process creates and saves a run configuration profile you can use at any time to upgrade your application. It also gets the latest updated application type version from the application manifest file.

The application upgrade takes a few minutes. You can monitor the application upgrade in Service Fabric Explorer.

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













