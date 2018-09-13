---
title: 'Azure DocumentDB portal tool: Script Explorer | Microsoft Docs'
description: Learn about the DocumentDB Script Explorer, an Azure Portal tool to manage DocumentDB server-side programming artifacts including JavaScript stored procedures, triggers, and user-defined functions.
keywords: javascript editor
services: documentdb
author: kirillg
manager: jhubbard
editor: monicar
documentationcenter: ''
ms.assetid: 9d0620da-2449-4c17-82a4-24aaa46e9b3e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: kirillg
ms.openlocfilehash: c4cd32708dfb4f882e0a7d4107720625ddf973ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554061"
---
# <a name="create-and-run-stored-procedures-triggers-and-user-defined-functions-using-the-documentdb-script-explorer"></a><span data-ttu-id="6d6b8-104">Create and run stored procedures, triggers, and user-defined functions using the DocumentDB Script Explorer</span><span class="sxs-lookup"><span data-stu-id="6d6b8-104">Create and run stored procedures, triggers, and user-defined functions using the DocumentDB Script Explorer</span></span>
<span data-ttu-id="6d6b8-105">This article provides an overview of the [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) Script Explorer, which is a JavaScript editor in the Azure portal that enables you to view and execute DocumentDB server-side programming artifacts including stored procedures, triggers, and user-defined functions.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-105">This article provides an overview of the [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) Script Explorer, which is a JavaScript editor in the Azure portal that enables you to view and execute DocumentDB server-side programming artifacts including stored procedures, triggers, and user-defined functions.</span></span> <span data-ttu-id="6d6b8-106">Read more about DocumentDB server-side programming in the [Stored procedures, database triggers, and UDFs](documentdb-programming.md) article.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-106">Read more about DocumentDB server-side programming in the [Stored procedures, database triggers, and UDFs](documentdb-programming.md) article.</span></span>

## <a name="launch-script-explorer"></a><span data-ttu-id="6d6b8-107">Launch Script Explorer</span><span class="sxs-lookup"><span data-stu-id="6d6b8-107">Launch Script Explorer</span></span>
1. <span data-ttu-id="6d6b8-108">In the [Azure portal](https://portal.azure.com), on the left navigation, click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-108">In the [Azure portal](https://portal.azure.com), on the left navigation, click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span></span> 

    <span data-ttu-id="6d6b8-109">If **NoSQL (DocumentDB)** is not visible, click **More Services** at the bottom, and then click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-109">If **NoSQL (DocumentDB)** is not visible, click **More Services** at the bottom, and then click ![Azure DocumentDB icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-query-collections-query-explorer/nosql-documentdb-portal-icon.png) **NoSQL (DocumentDB)**.</span></span>
2. <span data-ttu-id="6d6b8-110">In the resources menu, click **Script Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-110">In the resources menu, click **Script Explorer**.</span></span>
   
    ![Screenshot of the Script Explorer command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorercommand.png)
   
    <span data-ttu-id="6d6b8-112">The **Database** and **Collection** drop-down list boxes are pre-populated depending on the context in which you launch Script Explorer.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-112">The **Database** and **Collection** drop-down list boxes are pre-populated depending on the context in which you launch Script Explorer.</span></span>  <span data-ttu-id="6d6b8-113">For example, if you launch from a database blade, then the current database is pre-populated.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-113">For example, if you launch from a database blade, then the current database is pre-populated.</span></span>  <span data-ttu-id="6d6b8-114">If you launch from a collection blade, then the current collection is pre-populated.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-114">If you launch from a collection blade, then the current collection is pre-populated.</span></span>
3. <span data-ttu-id="6d6b8-115">Use the **Database** and **Collection** drop-down list boxes to easily change the collection from which scripts are currently being viewed without having to close and re-launch Script Explorer.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-115">Use the **Database** and **Collection** drop-down list boxes to easily change the collection from which scripts are currently being viewed without having to close and re-launch Script Explorer.</span></span>  
4. <span data-ttu-id="6d6b8-116">Script Explorer also supports filtering the currently loaded set of scripts by their id property.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-116">Script Explorer also supports filtering the currently loaded set of scripts by their id property.</span></span>  <span data-ttu-id="6d6b8-117">Simply type in the filter box and the results in the Script Explorer list are filtered based on your supplied criteria.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-117">Simply type in the filter box and the results in the Script Explorer list are filtered based on your supplied criteria.</span></span>
   
    ![Screenshot of Script Explorer with filtered results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorerfilterresults.png)

    > [!IMPORTANT] 
    > <span data-ttu-id="6d6b8-119">The Script Explorer filter functionality only filters from the ***currently*** loaded set of scripts and does not automatically refresh the currently selected collection.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-119">The Script Explorer filter functionality only filters from the ***currently*** loaded set of scripts and does not automatically refresh the currently selected collection.</span></span>

1. <span data-ttu-id="6d6b8-120">To refresh the list of scripts loaded by Script Explorer, simply click the **Refresh** command at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-120">To refresh the list of scripts loaded by Script Explorer, simply click the **Refresh** command at the top of the blade.</span></span>
   
    ![Screenshot of Script Explorer refresh command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorerrefresh.png)

## <a name="create-view-and-edit-stored-procedures-triggers-and-user-defined-functions"></a><span data-ttu-id="6d6b8-122">Create, view, and edit stored procedures, triggers, and user-defined functions</span><span class="sxs-lookup"><span data-stu-id="6d6b8-122">Create, view, and edit stored procedures, triggers, and user-defined functions</span></span>
<span data-ttu-id="6d6b8-123">Script Explorer allows you to easily perform CRUD operations on DocumentDB server-side programming artifacts.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-123">Script Explorer allows you to easily perform CRUD operations on DocumentDB server-side programming artifacts.</span></span>  

* <span data-ttu-id="6d6b8-124">To create a script, simply click on the applicable create command within script explorer, provide an id, enter the contents of the script, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-124">To create a script, simply click on the applicable create command within script explorer, provide an id, enter the contents of the script, and click **Save**.</span></span>
  
    ![Screenshot of Script Explorer create option, showing the JavaScript editor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorercreatecommand.png)
* <span data-ttu-id="6d6b8-126">When creating a trigger, you must also specify the trigger type and trigger operation</span><span class="sxs-lookup"><span data-stu-id="6d6b8-126">When creating a trigger, you must also specify the trigger type and trigger operation</span></span>
  
    ![Screenshot of Script Explorer create trigger option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorercreatetrigger.png)
* <span data-ttu-id="6d6b8-128">To view a script, simply click the script in which you're interested.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-128">To view a script, simply click the script in which you're interested.</span></span>
  
    ![Screenshot of Script Explorer view script experience](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorerviewscript.png)
* <span data-ttu-id="6d6b8-130">To edit a script, simply make the desired changes in the JavaScript editor and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-130">To edit a script, simply make the desired changes in the JavaScript editor and click **Save**.</span></span>
  
    ![Screenshot of Script Explorer view script experience](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorereditscript.png)
* <span data-ttu-id="6d6b8-132">To discard any pending changes to a script, simply click the **Discard** command.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-132">To discard any pending changes to a script, simply click the **Discard** command.</span></span>
  
    ![Screenshot of Script Explorer discard changes experience](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorerdiscardchanges.png)
* <span data-ttu-id="6d6b8-134">Script Explorer also allows you to easily view the system properties of the currently loaded script by clicking the **Properties** command.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-134">Script Explorer also allows you to easily view the system properties of the currently loaded script by clicking the **Properties** command.</span></span>
  
    ![Screenshot of Script Explorer script properties view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptproperties.png)
  
  > [!NOTE]
  > <span data-ttu-id="6d6b8-136">The timestamp (_ts) property is internally represented as epoch time, but Script Explorer displays the value in a human readable GMT format.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-136">The timestamp (_ts) property is internally represented as epoch time, but Script Explorer displays the value in a human readable GMT format.</span></span>
  > 
  > 
* <span data-ttu-id="6d6b8-137">To delete a script, select it in Script Explorer and click the **Delete** command.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-137">To delete a script, select it in Script Explorer and click the **Delete** command.</span></span>
  
    ![Screenshot of Script Explorer delete command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorerdeletescript1.png)
* <span data-ttu-id="6d6b8-139">Confirm the delete action by clicking **Yes** or cancel the delete action by clicking **No**.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-139">Confirm the delete action by clicking **Yes** or cancel the delete action by clicking **No**.</span></span>
  
    ![Screenshot of Script Explorer delete command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/scriptexplorerdeletescript2.png)

## <a name="execute-a-stored-procedure"></a><span data-ttu-id="6d6b8-141">Execute a stored procedure</span><span class="sxs-lookup"><span data-stu-id="6d6b8-141">Execute a stored procedure</span></span>
> [!WARNING]
> <span data-ttu-id="6d6b8-142">Executing stored procedures in Script Explorer is not yet supported for server side partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-142">Executing stored procedures in Script Explorer is not yet supported for server side partitioned collections.</span></span> <span data-ttu-id="6d6b8-143">For more information, visit [Partitioning and Scaling in DocumentDB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6d6b8-143">For more information, visit [Partitioning and Scaling in DocumentDB](documentdb-partition-data.md).</span></span>
> 
> 

<span data-ttu-id="6d6b8-144">Script Explorer allows you to execute server-side stored procedures from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-144">Script Explorer allows you to execute server-side stored procedures from the Azure portal.</span></span>

* <span data-ttu-id="6d6b8-145">When opening a new create stored procedure blade, a default script (*prefix*) will already be provided.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-145">When opening a new create stored procedure blade, a default script (*prefix*) will already be provided.</span></span> <span data-ttu-id="6d6b8-146">In order to run the *prefix* script or your own script, add an *id* and *inputs*.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-146">In order to run the *prefix* script or your own script, add an *id* and *inputs*.</span></span> <span data-ttu-id="6d6b8-147">For stored procedures that accept multiple parameters, all inputs must be within an array (e.g. *["foo", "bar"]*).</span><span class="sxs-lookup"><span data-stu-id="6d6b8-147">For stored procedures that accept multiple parameters, all inputs must be within an array (e.g. *["foo", "bar"]*).</span></span>
  
    ![Screenshot of Script Explorer Stored Procedures blade to add input and execute a stored procedure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/documentdb-execute-a-stored-procedure-input.png)
* <span data-ttu-id="6d6b8-149">To execute a stored procedure, simply click on the **Save & Execute** command within script editor pane.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-149">To execute a stored procedure, simply click on the **Save & Execute** command within script editor pane.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6d6b8-150">The **Save & Execute** command will save your stored procedure before executing, which means it will overwrite the previously saved version of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-150">The **Save & Execute** command will save your stored procedure before executing, which means it will overwrite the previously saved version of the stored procedure.</span></span>
  > 
  > 
* <span data-ttu-id="6d6b8-151">Successful stored procedure executions will have a *Successfully saved and executed the stored procedure* status and the returned results will be populated in the *Results* pane.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-151">Successful stored procedure executions will have a *Successfully saved and executed the stored procedure* status and the returned results will be populated in the *Results* pane.</span></span>
  
    ![Screenshot of Script Explorer Stored Procedures blade, to execute a stored procedure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/documentdb-execute-a-stored-procedure.png)
* <span data-ttu-id="6d6b8-153">If the execution encounters an error, the error will be populated in the *Results* pane.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-153">If the execution encounters an error, the error will be populated in the *Results* pane.</span></span>
  
    ![Screenshot of Script Explorer script properties view.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-view-scripts/documentdb-execute-a-stored-procedure-error.png)

## <a name="work-with-scripts-outside-the-portal"></a><span data-ttu-id="6d6b8-156">Work with scripts outside the portal</span><span class="sxs-lookup"><span data-stu-id="6d6b8-156">Work with scripts outside the portal</span></span>
<span data-ttu-id="6d6b8-157">The Script Explorer in the Azure portal is just one way to work with stored procedures, triggers, and user-defined functions in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-157">The Script Explorer in the Azure portal is just one way to work with stored procedures, triggers, and user-defined functions in DocumentDB.</span></span> <span data-ttu-id="6d6b8-158">You can also work with scripts using the the REST API and the [client SDKs](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6d6b8-158">You can also work with scripts using the the REST API and the [client SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="6d6b8-159">The REST API documentation includes samples for working with [stored procedures using REST](https://msdn.microsoft.com/library/azure/mt489092.aspx), [user defined functions using REST](https://msdn.microsoft.com/library/azure/dn781481.aspx), and [triggers using REST](https://msdn.microsoft.com/library/azure/mt489116.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d6b8-159">The REST API documentation includes samples for working with [stored procedures using REST](https://msdn.microsoft.com/library/azure/mt489092.aspx), [user defined functions using REST](https://msdn.microsoft.com/library/azure/dn781481.aspx), and [triggers using REST](https://msdn.microsoft.com/library/azure/mt489116.aspx).</span></span> <span data-ttu-id="6d6b8-160">Samples are also available showing how to [work with scripts using C#](documentdb-dotnet-samples.md#server-side-programming-examples) and [work with scripts using Node.js](documentdb-nodejs-samples.md#server-side-programming-examples).</span><span class="sxs-lookup"><span data-stu-id="6d6b8-160">Samples are also available showing how to [work with scripts using C#](documentdb-dotnet-samples.md#server-side-programming-examples) and [work with scripts using Node.js](documentdb-nodejs-samples.md#server-side-programming-examples).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d6b8-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d6b8-161">Next steps</span></span>
<span data-ttu-id="6d6b8-162">Learn more about DocumentDB server-side programming in the [Stored procedures, database triggers, and UDFs](documentdb-programming.md) article.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-162">Learn more about DocumentDB server-side programming in the [Stored procedures, database triggers, and UDFs](documentdb-programming.md) article.</span></span>

<span data-ttu-id="6d6b8-163">The [Learning path](https://azure.microsoft.com/documentation/learning-paths/documentdb/) is also a useful resource to guide you as you learn more about DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6d6b8-163">The [Learning path](https://azure.microsoft.com/documentation/learning-paths/documentdb/) is also a useful resource to guide you as you learn more about DocumentDB.</span></span>  

















