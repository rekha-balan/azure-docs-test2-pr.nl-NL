---
title: Configure an Azure cloud service project with Visual Studio | Microsoft Docs
description: Learn how to configure an Azure cloud service project in Visual Studio, depending on your requirements for that project.
services: visual-studio-online
author: ghogen
manager: douge
assetId: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/06/2017
ms.author: ghogen
ms.openlocfilehash: 0e2e03f7a492f5018b99145a63bb1b7432d3e0b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825708"
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="3efd1-103">Configure an Azure cloud service project with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3efd1-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="3efd1-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span><span class="sxs-lookup"><span data-stu-id="3efd1-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="3efd1-105">You can set properties for the project for the following categories:</span><span class="sxs-lookup"><span data-stu-id="3efd1-105">You can set properties for the project for the following categories:</span></span>

- <span data-ttu-id="3efd1-106">**Publish a cloud service to Azure** - You can set a property to make sure that an existing cloud service deployed to Azure is not accidentally deleted.</span><span class="sxs-lookup"><span data-stu-id="3efd1-106">**Publish a cloud service to Azure** - You can set a property to make sure that an existing cloud service deployed to Azure is not accidentally deleted.</span></span>
- <span data-ttu-id="3efd1-107">**Run or debug a cloud service on the local computer** - You can select a service configuration to use and indicate whether you want to start the Azure storage emulator.</span><span class="sxs-lookup"><span data-stu-id="3efd1-107">**Run or debug a cloud service on the local computer** - You can select a service configuration to use and indicate whether you want to start the Azure storage emulator.</span></span>
- <span data-ttu-id="3efd1-108">**Validate a cloud service package when it is created** - You can decide to treat any warnings as errors so that you can ensure that the cloud service package deploys without any issues.</span><span class="sxs-lookup"><span data-stu-id="3efd1-108">**Validate a cloud service package when it is created** - You can decide to treat any warnings as errors so that you can ensure that the cloud service package deploys without any issues.</span></span> 

## <a name="steps-to-configure-an-azure-cloud-service-project"></a><span data-ttu-id="3efd1-109">Steps to configure an Azure cloud service project</span><span class="sxs-lookup"><span data-stu-id="3efd1-109">Steps to configure an Azure cloud service project</span></span>
1. <span data-ttu-id="3efd1-110">Open or create a cloud service project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3efd1-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="3efd1-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="3efd1-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="3efd1-112">In the project's properties page, select the **Development** tab.</span><span class="sxs-lookup"><span data-stu-id="3efd1-112">In the project's properties page, select the **Development** tab.</span></span>

    ![Project properties menu](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="3efd1-114">Set **Prompt before deleting an existing deployment** to **True**.</span><span class="sxs-lookup"><span data-stu-id="3efd1-114">Set **Prompt before deleting an existing deployment** to **True**.</span></span> <span data-ttu-id="3efd1-115">This setting helps to ensure you don't accidentally delete an existing deployment in Azure</span><span class="sxs-lookup"><span data-stu-id="3efd1-115">This setting helps to ensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="3efd1-116">Select the desired **Service configuration** to indicate which service configuration you want to use when you run or debug your cloud service locally.</span><span class="sxs-lookup"><span data-stu-id="3efd1-116">Select the desired **Service configuration** to indicate which service configuration you want to use when you run or debug your cloud service locally.</span></span> <span data-ttu-id="3efd1-117">For more information on how to modify a service configuration for a role, see [How to configure the roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="3efd1-117">For more information on how to modify a service configuration for a role, see [How to configure the roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="3efd1-118">Set **Start Azure storage emulator** to **True** to start the Azure storage emulator when you run or debug your cloud service locally.</span><span class="sxs-lookup"><span data-stu-id="3efd1-118">Set **Start Azure storage emulator** to **True** to start the Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="3efd1-119">Set **Treat warnings as errors** to **True** to make sure you cannot publish if there are package validation errors.</span><span class="sxs-lookup"><span data-stu-id="3efd1-119">Set **Treat warnings as errors** to **True** to make sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="3efd1-120">Set **Use web project ports** to **True** to make sure that your web role uses the same port each time it starts locally in IIS Express.</span><span class="sxs-lookup"><span data-stu-id="3efd1-120">Set **Use web project ports** to **True** to make sure that your web role uses the same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="3efd1-121">From the Visual Studio toolbar, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="3efd1-121">From the Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3efd1-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="3efd1-122">Next steps</span></span>
- [<span data-ttu-id="3efd1-123">Configure an Azure project using multiple service configurations</span><span class="sxs-lookup"><span data-stu-id="3efd1-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

