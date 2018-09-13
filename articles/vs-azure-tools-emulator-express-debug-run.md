---
title: Using Emulator Express to run and debug an Azure cloud service on a local machine | Microsoft Docs
description: Using Emulator Express to run and debug a cloud service on a local machine
services: visual-studio-online
documentationcenter: n/a
author: TomArcher
manager: douge
editor: ''
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: tarcher
ms.openlocfilehash: 99af4a0ce0b93bcb7c3967431ac7029e2a425f94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552785"
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a><span data-ttu-id="4d182-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span><span class="sxs-lookup"><span data-stu-id="4d182-103">Using Emulator Express to run and debug an Azure cloud service on a local machine</span></span>
<span data-ttu-id="4d182-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span><span class="sxs-lookup"><span data-stu-id="4d182-104">By using Emulator Express, you can test and debug a cloud service without running Visual Studio as an administrator.</span></span> <span data-ttu-id="4d182-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span><span class="sxs-lookup"><span data-stu-id="4d182-105">You can set your project settings to use either Emulator Express or the full emulator, depending on the requirements of your cloud service.</span></span> <span data-ttu-id="4d182-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="4d182-106">For more information about the full emulator, see [Run an Azure Application in the Compute Emulator](storage/storage-use-emulator.md).</span></span>

## <a name="using-emulator-express-in-visual-studio"></a><span data-ttu-id="4d182-107">Using Emulator Express in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d182-107">Using Emulator Express in Visual Studio</span></span>
<span data-ttu-id="4d182-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span><span class="sxs-lookup"><span data-stu-id="4d182-108">When you create an Azure project in Azure SDK 2.3 or later, Emulator Express is automatically used.</span></span> <span data-ttu-id="4d182-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="4d182-109">For existing projects that were created with an earlier version of the Azure SDK, use the following steps to select Emulator Express:</span></span>

1. <span data-ttu-id="4d182-110">Create or open an Azure cloud service project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d182-110">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="4d182-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4d182-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>

1. <span data-ttu-id="4d182-112">In the projects properties pages, select the **Web** tab.</span><span class="sxs-lookup"><span data-stu-id="4d182-112">In the projects properties pages, select the **Web** tab.</span></span>

    ![Properties for an Azure cloud service project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. <span data-ttu-id="4d182-114">Under **Local Development Server**, select **Use IIS Express option**.</span><span class="sxs-lookup"><span data-stu-id="4d182-114">Under **Local Development Server**, select **Use IIS Express option**.</span></span>

1. <span data-ttu-id="4d182-115">Under **Emulator**, select **Use Emulator Express**.</span><span class="sxs-lookup"><span data-stu-id="4d182-115">Under **Emulator**, select **Use Emulator Express**.</span></span>
   
1. <span data-ttu-id="4d182-116">To launch the Emulator Express, run the following command at a command prompt:</span><span class="sxs-lookup"><span data-stu-id="4d182-116">To launch the Emulator Express, run the following command at a command prompt:</span></span> 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a><span data-ttu-id="4d182-117">Emulator Express limitations</span><span class="sxs-lookup"><span data-stu-id="4d182-117">Emulator Express limitations</span></span>
<span data-ttu-id="4d182-118">The following issues are known limitations of Emulator Express:</span><span class="sxs-lookup"><span data-stu-id="4d182-118">The following issues are known limitations of Emulator Express:</span></span> 

- <span data-ttu-id="4d182-119">Emulator Express is not compatible with IIS Web Server.</span><span class="sxs-lookup"><span data-stu-id="4d182-119">Emulator Express is not compatible with IIS Web Server.</span></span>
- <span data-ttu-id="4d182-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span><span class="sxs-lookup"><span data-stu-id="4d182-120">Your cloud service can contain multiple roles, but each role is limited to one instance.</span></span>
- <span data-ttu-id="4d182-121">You can't access port numbers below 1000.</span><span class="sxs-lookup"><span data-stu-id="4d182-121">You can't access port numbers below 1000.</span></span> <span data-ttu-id="4d182-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span><span class="sxs-lookup"><span data-stu-id="4d182-122">If you use an authentication provider that normally uses a port below 1000, you might need to change this value to a port number that's above 1000.</span></span>
- <span data-ttu-id="4d182-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span><span class="sxs-lookup"><span data-stu-id="4d182-123">Any limitations that apply to the Azure Compute Emulator also apply to Emulator Express.</span></span> <span data-ttu-id="4d182-124">For example, you can't have more than 50 role instances per deployment.</span><span class="sxs-lookup"><span data-stu-id="4d182-124">For example, you can't have more than 50 role instances per deployment.</span></span> <span data-ttu-id="4d182-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span><span class="sxs-lookup"><span data-stu-id="4d182-125">For more information about the Azure Compute Emulator, see [Run an Azure Application in the Compute Emulator](http://go.microsoft.com/fwlink/p/?LinkId=623050).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d182-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d182-126">Next steps</span></span>
[<span data-ttu-id="4d182-127">Debugging Azure cloud services</span><span class="sxs-lookup"><span data-stu-id="4d182-127">Debugging Azure cloud services</span></span>](https://msdn.microsoft.com/library/azure/ee405479.aspx)

