---
title: Creating an Azure cloud service project with Visual Studio | Microsoft Docs
description: Learn now to create an Azure cloud service project with Visual Studio
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: c697e66547dc64dec834617b60613c2728bb1155
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553370"
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Creating an Azure cloud service project with Visual Studio
The Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service. Once the project has been created, Visual Studio enables you to configure, debug, and deploy the cloud service to Azure.

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a>Steps to create an Azure cloud service project in Visual Studio
This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.  

1. Start Visual Studio as an administrator.

1. On the main menu, select **File** > **New** > **Project**.

1. Select **Cloud** from the Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from the list of templates.

    ![New Azure cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Specify which version of the .NET Framework you want to use to develop your project.

1. Enter a name and location for your project and a name for the solution. 

1. Select **OK**.

1. In the **New Microsoft Azure Cloud Service** dialog, select the roles that you want to add, and choose the right arrow button to add them to your solution.

    ![Select new Azure cloud service roles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. To rename a role that you've added, hover on the role in the **New Microsoft Azure Cloud Service** dialog, and, from the context menu, select **Rename**. You can also rename a role within your solution (in the **Solution Explorer**) after it has been added.

    ![Rename Azure cloud service role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

The Visual Studio Azure project has associations to the role projects in the solution. The project also includes the *service definition file* and *service configuration file*:

- **Service definition file** - Defines the runtime settings for your application, including what roles are required, endpoints, and virtual machine size. 
- **Service configuration file** - Configures how many instances of a role are run and the values of the settings defined for a role. 

For more information about these files, see [Configure the Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Next steps
- [Managing roles in Azure cloud service projects with Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)



