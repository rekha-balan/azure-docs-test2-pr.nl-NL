---
title: Connect to on-premises file systems from Azure Logic Apps | Microsoft Docs
description: Connect to on-premises file systems from your logic app workflow through the on-premises data gateway and File System connector
keywords: file systems
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: ''
ms.assetid: ''
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: deli; LADocs
ms.openlocfilehash: dd43c1e1657a066e7df552e5b4ac94f42edaebc0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555183"
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="1f233-104">Connect to on-premises file systems from logic apps with the File System connector</span><span class="sxs-lookup"><span data-stu-id="1f233-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="1f233-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span><span class="sxs-lookup"><span data-stu-id="1f233-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="1f233-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span><span class="sxs-lookup"><span data-stu-id="1f233-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f233-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f233-107">Prerequisites</span></span>

- <span data-ttu-id="1f233-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="1f233-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="1f233-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span><span class="sxs-lookup"><span data-stu-id="1f233-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="1f233-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span><span class="sxs-lookup"><span data-stu-id="1f233-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="1f233-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span><span class="sxs-lookup"><span data-stu-id="1f233-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="1f233-112">Add trigger and actions for connecting to your file system</span><span class="sxs-lookup"><span data-stu-id="1f233-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="1f233-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span><span class="sxs-lookup"><span data-stu-id="1f233-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="1f233-114">Under the trigger, choose **Next Step** > **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="1f233-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="1f233-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span><span class="sxs-lookup"><span data-stu-id="1f233-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![Search for file connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="1f233-117">Choose the **Create file** action, and create a connection to your file system.</span><span class="sxs-lookup"><span data-stu-id="1f233-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="1f233-118">If you don't have an existing connection, you are prompted to create one.</span><span class="sxs-lookup"><span data-stu-id="1f233-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="1f233-119">Choose **Connect via on-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="1f233-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="1f233-120">More properties appear.</span><span class="sxs-lookup"><span data-stu-id="1f233-120">More properties appear.</span></span>
   2. <span data-ttu-id="1f233-121">Select your root folder for your file system.</span><span class="sxs-lookup"><span data-stu-id="1f233-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="1f233-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span><span class="sxs-lookup"><span data-stu-id="1f233-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="1f233-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span><span class="sxs-lookup"><span data-stu-id="1f233-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="1f233-124">Enter the username and password for the gateway.</span><span class="sxs-lookup"><span data-stu-id="1f233-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="1f233-125">Select the gateway that you previously installed.</span><span class="sxs-lookup"><span data-stu-id="1f233-125">Select the gateway that you previously installed.</span></span>

       ![Configure connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="1f233-127">After you provide all the details, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f233-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="1f233-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span><span class="sxs-lookup"><span data-stu-id="1f233-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="1f233-129">If the connection is set up correctly, you see options for the action that you previously selected.</span><span class="sxs-lookup"><span data-stu-id="1f233-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="1f233-130">The file system connector is now ready for use.</span><span class="sxs-lookup"><span data-stu-id="1f233-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="1f233-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span><span class="sxs-lookup"><span data-stu-id="1f233-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![Create file action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="1f233-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span><span class="sxs-lookup"><span data-stu-id="1f233-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="1f233-134">Enter the recipients, title, and body of the email.</span><span class="sxs-lookup"><span data-stu-id="1f233-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="1f233-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span><span class="sxs-lookup"><span data-stu-id="1f233-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![Send email action](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="1f233-137">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="1f233-137">Save your logic app.</span></span> <span data-ttu-id="1f233-138">Test your app by uploading a file to Dropbox.</span><span class="sxs-lookup"><span data-stu-id="1f233-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="1f233-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span><span class="sxs-lookup"><span data-stu-id="1f233-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="1f233-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="1f233-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="1f233-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span><span class="sxs-lookup"><span data-stu-id="1f233-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="1f233-142">Try exploring other functionalities that the connector offers, for example:</span><span class="sxs-lookup"><span data-stu-id="1f233-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="1f233-143">Create file</span><span class="sxs-lookup"><span data-stu-id="1f233-143">Create file</span></span>
- <span data-ttu-id="1f233-144">List files in folder</span><span class="sxs-lookup"><span data-stu-id="1f233-144">List files in folder</span></span>
- <span data-ttu-id="1f233-145">Append file</span><span class="sxs-lookup"><span data-stu-id="1f233-145">Append file</span></span>
- <span data-ttu-id="1f233-146">Delete file</span><span class="sxs-lookup"><span data-stu-id="1f233-146">Delete file</span></span>
- <span data-ttu-id="1f233-147">Get file content</span><span class="sxs-lookup"><span data-stu-id="1f233-147">Get file content</span></span>
- <span data-ttu-id="1f233-148">Get file content using path</span><span class="sxs-lookup"><span data-stu-id="1f233-148">Get file content using path</span></span>
- <span data-ttu-id="1f233-149">Get file metadata</span><span class="sxs-lookup"><span data-stu-id="1f233-149">Get file metadata</span></span>
- <span data-ttu-id="1f233-150">Get file metadata using path</span><span class="sxs-lookup"><span data-stu-id="1f233-150">Get file metadata using path</span></span>
- <span data-ttu-id="1f233-151">List files in root folder</span><span class="sxs-lookup"><span data-stu-id="1f233-151">List files in root folder</span></span>
- <span data-ttu-id="1f233-152">Update file</span><span class="sxs-lookup"><span data-stu-id="1f233-152">Update file</span></span>

## <a name="get-help"></a><span data-ttu-id="1f233-153">Get help</span><span class="sxs-lookup"><span data-stu-id="1f233-153">Get help</span></span>

<span data-ttu-id="1f233-154">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="1f233-154">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="1f233-155">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="1f233-155">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f233-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f233-156">Next steps</span></span>

- <span data-ttu-id="1f233-157">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span><span class="sxs-lookup"><span data-stu-id="1f233-157">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="1f233-158">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="1f233-158">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>




