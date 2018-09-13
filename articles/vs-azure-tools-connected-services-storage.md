---
title: Add Azure Storage by using Connected Services in Visual Studio | Microsoft Docs
description: Add Azure Storage to your app by using the Visual Studio Add Connected Services dialog box
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: tarcher
ms.openlocfilehash: fefa36cbeb8a15e0c6787622c6f11e9098d01b20
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671053"
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="d3c3a-103">Adding Azure storage by using Visual Studio Connected Services</span><span class="sxs-lookup"><span data-stu-id="d3c3a-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="d3c3a-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span><span class="sxs-lookup"><span data-stu-id="d3c3a-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="d3c3a-105">C# cloud service</span><span class="sxs-lookup"><span data-stu-id="d3c3a-105">C# cloud service</span></span>
- <span data-ttu-id="d3c3a-106">.NET backend mobile service</span><span class="sxs-lookup"><span data-stu-id="d3c3a-106">.NET backend mobile service</span></span>
- <span data-ttu-id="d3c3a-107">ASP.NET website or service</span><span class="sxs-lookup"><span data-stu-id="d3c3a-107">ASP.NET website or service</span></span>
- <span data-ttu-id="d3c3a-108">ASP.NET Core service</span><span class="sxs-lookup"><span data-stu-id="d3c3a-108">ASP.NET Core service</span></span>
- <span data-ttu-id="d3c3a-109">Azure WebJob service</span><span class="sxs-lookup"><span data-stu-id="d3c3a-109">Azure WebJob service</span></span> 

<span data-ttu-id="d3c3a-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="d3c3a-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="d3c3a-112">Connect to Azure Storage using the Connected Services dialog</span><span class="sxs-lookup"><span data-stu-id="d3c3a-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="d3c3a-113">Open your project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d3c3a-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="d3c3a-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Add Azure connected service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="d3c3a-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Add Azure Storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="d3c3a-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="d3c3a-119">If you need to create a storage account, go to the next step.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="d3c3a-120">Otherwise, skip to step 6.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-120">Otherwise, skip to step 6.</span></span>
    
    ![Add existing storage account to project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="d3c3a-122">To create a storage account:</span><span class="sxs-lookup"><span data-stu-id="d3c3a-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="d3c3a-123">Select **Create a New Storage Account** at the bottom of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="d3c3a-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![New Azure storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="d3c3a-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="d3c3a-127">Select the new storage account in the list, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="d3c3a-128">The storage connected service appears under the **Service References** node of your project.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="d3c3a-129">How your project is modified</span><span class="sxs-lookup"><span data-stu-id="d3c3a-129">How your project is modified</span></span>
<span data-ttu-id="d3c3a-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span><span class="sxs-lookup"><span data-stu-id="d3c3a-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="d3c3a-131">The specific changes depend on the project type:</span><span class="sxs-lookup"><span data-stu-id="d3c3a-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="d3c3a-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="d3c3a-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="d3c3a-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="d3c3a-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="d3c3a-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="d3c3a-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="d3c3a-135">WebJob project - [What happened - WebJob projects](storage/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="d3c3a-135">WebJob project - [What happened - WebJob projects](storage/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3c3a-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3c3a-136">Next steps</span></span>
- [<span data-ttu-id="d3c3a-137">MSDN Forum: Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d3c3a-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="d3c3a-138">Microsoft Azure Storage Team Blog</span><span class="sxs-lookup"><span data-stu-id="d3c3a-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="d3c3a-139">Azure Storage documentation</span><span class="sxs-lookup"><span data-stu-id="d3c3a-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)




