---
title: Connect to FTP server - Azure Logic Apps | Microsoft Docs
description: Create, monitor, and manage files on an FTP server with Azure Logic Apps
author: ecfan
manager: jeconnoc
ms.author: estfan
ms.date: 07/22/2016
ms.topic: article
ms.service: logic-apps
services: logic-apps
ms.reviewer: klam, LADocs
ms.suite: integration
tags: connectors
ms.openlocfilehash: 4355a767d2ecd500662cdf4522e8a7e12de86b80
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804874"
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="ca0e6-103">Get started with the FTP connector</span><span class="sxs-lookup"><span data-stu-id="ca0e6-103">Get started with the FTP connector</span></span>
<span data-ttu-id="ca0e6-104">Use the FTP connector to monitor, manage and create files on an  FTP server.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-104">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="ca0e6-105">To use [any connector](apis-list.md), you first need to create a logic app.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="ca0e6-106">You can get started by [creating a logic app now](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="ca0e6-106">You can get started by [creating a logic app now](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="ca0e6-107">Connect to FTP</span><span class="sxs-lookup"><span data-stu-id="ca0e6-107">Connect to FTP</span></span>
<span data-ttu-id="ca0e6-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="ca0e6-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="ca0e6-110">Create a connection to FTP</span><span class="sxs-lookup"><span data-stu-id="ca0e6-110">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="ca0e6-111">Use a FTP trigger</span><span class="sxs-lookup"><span data-stu-id="ca0e6-111">Use a FTP trigger</span></span>
<span data-ttu-id="ca0e6-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="ca0e6-113">[Learn more about triggers](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca0e6-113">[Learn more about triggers](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ca0e6-114">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-114">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="ca0e6-115">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-115">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="ca0e6-116">The FTP connector only supports explicit FTPS (FTP over SSL).</span><span class="sxs-lookup"><span data-stu-id="ca0e6-116">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="ca0e6-117">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-117">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="ca0e6-118">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-118">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="ca0e6-119">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-119">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="ca0e6-120">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span><span class="sxs-lookup"><span data-stu-id="ca0e6-120">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="ca0e6-121">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-121">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="ca0e6-122">The **When a file is added or modified** control opens up</span><span class="sxs-lookup"><span data-stu-id="ca0e6-122">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="ca0e6-123">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-123">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="ca0e6-124">Select the **...** located on the right side of the control.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-124">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="ca0e6-125">This opens the folder picker control</span><span class="sxs-lookup"><span data-stu-id="ca0e6-125">This opens the folder picker control</span></span>  
   <span data-ttu-id="ca0e6-126">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-126">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="ca0e6-127">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-127">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="ca0e6-128">Select the folder and notice the folder is now displayed in the **Folder** control.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-128">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="ca0e6-129">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-129">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="ca0e6-130">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-130">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="ca0e6-131">For a logic app to be functional, it must contain at least one trigger and one action.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-131">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="ca0e6-132">Follow the steps in the next section to add an action.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-132">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="ca0e6-133">Use a FTP action</span><span class="sxs-lookup"><span data-stu-id="ca0e6-133">Use a FTP action</span></span>
<span data-ttu-id="ca0e6-134">An action is an operation carried out by the workflow defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-134">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="ca0e6-135">[Learn more about actions](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="ca0e6-135">[Learn more about actions](../logic-apps/logic-apps-overview.md#logic-app-concepts).</span></span>  

<span data-ttu-id="ca0e6-136">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-136">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="ca0e6-137">Select **+ New step** to add the action to get the contents of the file on the FTP server</span><span class="sxs-lookup"><span data-stu-id="ca0e6-137">Select **+ New step** to add the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="ca0e6-138">Select the **Add an action** link.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-138">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="ca0e6-139">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-139">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="ca0e6-140">Enter *FTP* to search for all actions related to FTP.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-140">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="ca0e6-141">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-141">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="ca0e6-142">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-142">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="ca0e6-143">The **Get file content** control opens.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-143">The **Get file content** control opens.</span></span> <span data-ttu-id="ca0e6-144">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-144">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="ca0e6-145">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-145">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="ca0e6-146">Select the **File** control (the white space located below \*\*FILE\*\*\*).</span><span class="sxs-lookup"><span data-stu-id="ca0e6-146">Select the **File** control (the white space located below \*\*FILE\*\*\*).</span></span> <span data-ttu-id="ca0e6-147">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-147">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="ca0e6-148">Select the **File content** option.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-148">Select the **File content** option.</span></span>  
   <span data-ttu-id="ca0e6-149">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-149">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="ca0e6-150">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-150">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="ca0e6-151">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="ca0e6-151">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="ca0e6-152">Save your work then add a file to the FTP folder to test your workflow.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-152">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="ca0e6-153">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-153">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="ca0e6-154">The logic app also has been configured with an action to get the contents of the new or modified file.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-154">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="ca0e6-155">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span><span class="sxs-lookup"><span data-stu-id="ca0e6-155">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="ca0e6-156">Connector-specific details</span><span class="sxs-lookup"><span data-stu-id="ca0e6-156">Connector-specific details</span></span>

<span data-ttu-id="ca0e6-157">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="ca0e6-157">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ca0e6-158">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ca0e6-158">Next Steps</span></span>
[<span data-ttu-id="ca0e6-159">Create a logic app</span><span class="sxs-lookup"><span data-stu-id="ca0e6-159">Create a logic app</span></span>](../logic-apps/quickstart-create-first-logic-app-workflow.md)

