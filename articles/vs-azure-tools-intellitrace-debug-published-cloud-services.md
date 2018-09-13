---
title: Debugging a published an Azure cloud service with Visual Studio and IntelliTrace | Microsoft Docs
description: Learn how to debug a cloud service with Visual Studio and IntelliTrace
services: visual-studio-online
documentationcenter: n/a
author: TomArcher
manager: douge
editor: ''
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 893b59fadc27a1505438f8e04e1e040a8339d49e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555566"
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="1e8a7-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="1e8a7-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="1e8a7-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="1e8a7-105">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-105">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="1e8a7-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay the recorded data from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay the recorded data from Visual Studio.</span></span> 

<span data-ttu-id="1e8a7-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="1e8a7-108">IntelliTrace collects information for your Azure roles.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="1e8a7-109">The virtual machines for these roles always run 64-bit operating systems.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-109">The virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="1e8a7-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) to attach directly to a cloud service that's running in Azure.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) to attach directly to a cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e8a7-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="1e8a7-112">Configure an Azure application for IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="1e8a7-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="1e8a7-113">To enable IntelliTrace for an Azure application, you must create and publish the application from a Visual Studio Azure project.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-113">To enable IntelliTrace for an Azure application, you must create and publish the application from a Visual Studio Azure project.</span></span> <span data-ttu-id="1e8a7-114">You must configure IntelliTrace for your Azure application before you publish it to Azure.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-114">You must configure IntelliTrace for your Azure application before you publish it to Azure.</span></span> <span data-ttu-id="1e8a7-115">If you publish your application without configuring IntelliTrace, you need to republish the project.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-115">If you publish your application without configuring IntelliTrace, you need to republish the project.</span></span> <span data-ttu-id="1e8a7-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="1e8a7-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="1e8a7-117">When you are ready to deploy your Azure application, verify that your project build targets are set to **Debug**.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-117">When you are ready to deploy your Azure application, verify that your project build targets are set to **Debug**.</span></span>

1. <span data-ttu-id="1e8a7-118">In **Solution Explorer**, right-click project, and, from the context menu, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-118">In **Solution Explorer**, right-click project, and, from the context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="1e8a7-119">In the **Publish Azure Application** dialog, select the Azure subscription, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-119">In the **Publish Azure Application** dialog, select the Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="1e8a7-120">In the **Settings** page, select the **Advanced Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-120">In the **Settings** page, select the **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="1e8a7-121">Turn on the **Enable IntelliTrace** option to collect IntelliTrace logs for your application when it is published in the cloud.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-121">Turn on the **Enable IntelliTrace** option to collect IntelliTrace logs for your application when it is published in the cloud.</span></span>
   
1. <span data-ttu-id="1e8a7-122">To customize the basic IntelliTrace configuration, select **Settings** next to **Enable IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-122">To customize the basic IntelliTrace configuration, select **Settings** next to **Enable IntelliTrace**.</span></span>

    ![IntelliTrace settings link](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="1e8a7-124">In the **IntelliTrace Settings** dialog, you can specify which events to log, whether to collect call information, which modules and processes to collect logs for, and how much space to allocate to the recording.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-124">In the **IntelliTrace Settings** dialog, you can specify which events to log, whether to collect call information, which modules and processes to collect logs for, and how much space to allocate to the recording.</span></span> <span data-ttu-id="1e8a7-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="1e8a7-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![IntelliTrace settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="1e8a7-127">The IntelliTrace log is a circular log file of the maximum size specified in the IntelliTrace settings (the default size is 250 MB).</span><span class="sxs-lookup"><span data-stu-id="1e8a7-127">The IntelliTrace log is a circular log file of the maximum size specified in the IntelliTrace settings (the default size is 250 MB).</span></span> <span data-ttu-id="1e8a7-128">IntelliTrace logs are collected to a file in the file system of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-128">IntelliTrace logs are collected to a file in the file system of the virtual machine.</span></span> <span data-ttu-id="1e8a7-129">When you request the logs, a snapshot is taken at that point in time and downloaded to your local computer.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-129">When you request the logs, a snapshot is taken at that point in time and downloaded to your local computer.</span></span>

<span data-ttu-id="1e8a7-130">After the Azure cloud service has been published to Azure, you can determine if IntelliTrace has been enabled from the Azure node in **Server Explorer**, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="1e8a7-130">After the Azure cloud service has been published to Azure, you can determine if IntelliTrace has been enabled from the Azure node in **Server Explorer**, as shown in the following image:</span></span>

![Server Explorer - IntelliTrace enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="1e8a7-132">Download IntelliTrace logs for a role instance</span><span class="sxs-lookup"><span data-stu-id="1e8a7-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="1e8a7-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span><span class="sxs-lookup"><span data-stu-id="1e8a7-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="1e8a7-134">In **Server Explorer**, expand the **Cloud Services** node, and locate role instance whose logs you wish to download.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-134">In **Server Explorer**, expand the **Cloud Services** node, and locate role instance whose logs you wish to download.</span></span> 

1. <span data-ttu-id="1e8a7-135">Right-click the role instance, and from the s context menu, select **View IntelliTrace Logs**.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-135">Right-click the role instance, and from the s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![View IntelliTrace logs menu option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="1e8a7-137">The IntelliTrace logs are downloaded to a file in a directory on your local computer.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-137">The IntelliTrace logs are downloaded to a file in a directory on your local computer.</span></span> <span data-ttu-id="1e8a7-138">Each time that you request the IntelliTrace logs, a new snapshot is created.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-138">Each time that you request the IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="1e8a7-139">While the logs are being downloaded, Visual Studio displays the progress of the operation in the **Azure Activity Log** window.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-139">While the logs are being downloaded, Visual Studio displays the progress of the operation in the **Azure Activity Log** window.</span></span> <span data-ttu-id="1e8a7-140">As shown in the following figure, you can expand the line item for the operation to see more detail.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-140">As shown in the following figure, you can expand the line item for the operation to see more detail.</span></span>

![VST_IntelliTraceDownloadProgress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="1e8a7-142">You can continue to work in Visual Studio while the IntelliTrace logs are downloading.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-142">You can continue to work in Visual Studio while the IntelliTrace logs are downloading.</span></span> <span data-ttu-id="1e8a7-143">When the log has finished downloading, it opens in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-143">When the log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="1e8a7-144">The IntelliTrace logs might contain exceptions that the framework generates and handles afterwards.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-144">The IntelliTrace logs might contain exceptions that the framework generates and handles afterwards.</span></span> <span data-ttu-id="1e8a7-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span><span class="sxs-lookup"><span data-stu-id="1e8a7-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1e8a7-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="1e8a7-146">Next steps</span></span>
- [<span data-ttu-id="1e8a7-147">Options for debugging Azure cloud services</span><span class="sxs-lookup"><span data-stu-id="1e8a7-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="1e8a7-148">Publishing an Azure cloud service using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e8a7-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)




