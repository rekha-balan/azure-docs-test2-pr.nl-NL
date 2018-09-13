---
title: Use Azure Functions to perform a scheduled clean-up task | Microsoft Docs
description: Use Azure Functions create a C# function that runs based on an event timer.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: ''
tags: ''
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/26/2016
ms.author: glenga
ms.openlocfilehash: b22dc1b870e2b452f8e3bdfe9139b7bf4aee6bd5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549541"
---
# <a name="use-azure-functions-to-perform-a-scheduled-clean-up-task"></a><span data-ttu-id="fa08d-103">Use Azure Functions to perform a scheduled clean-up task</span><span class="sxs-lookup"><span data-stu-id="fa08d-103">Use Azure Functions to perform a scheduled clean-up task</span></span>
<span data-ttu-id="fa08d-104">This topic shows you how to use Azure Functions to create a new function in C# that runs based on an event timer to clean-up rows in a database table.</span><span class="sxs-lookup"><span data-stu-id="fa08d-104">This topic shows you how to use Azure Functions to create a new function in C# that runs based on an event timer to clean-up rows in a database table.</span></span> <span data-ttu-id="fa08d-105">The new function is created based on a pre-defined template in the Azure Functions portal.</span><span class="sxs-lookup"><span data-stu-id="fa08d-105">The new function is created based on a pre-defined template in the Azure Functions portal.</span></span> <span data-ttu-id="fa08d-106">To support this scenario, you must also set a database connection string as an App Service setting in the function app.</span><span class="sxs-lookup"><span data-stu-id="fa08d-106">To support this scenario, you must also set a database connection string as an App Service setting in the function app.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fa08d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fa08d-107">Prerequisites</span></span>
<span data-ttu-id="fa08d-108">Before you can create a function, you need to have an active Azure account.</span><span class="sxs-lookup"><span data-stu-id="fa08d-108">Before you can create a function, you need to have an active Azure account.</span></span> <span data-ttu-id="fa08d-109">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fa08d-109">If you don't already have an Azure account, [free accounts are available](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="fa08d-110">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in table named *TodoItems* in a SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fa08d-110">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in table named *TodoItems* in a SQL Database.</span></span> <span data-ttu-id="fa08d-111">This same TodoItems table is created when you complete the [Azure App Service Mobile Apps quickstart tutorial](../app-service-mobile/app-service-mobile-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa08d-111">This same TodoItems table is created when you complete the [Azure App Service Mobile Apps quickstart tutorial](../app-service-mobile/app-service-mobile-ios-get-started.md).</span></span> <span data-ttu-id="fa08d-112">You can also use a sample database  If you choose to use a different table, you will need to modify the command.</span><span class="sxs-lookup"><span data-stu-id="fa08d-112">You can also use a sample database  If you choose to use a different table, you will need to modify the command.</span></span>

<span data-ttu-id="fa08d-113">You can get the connection string used by a Mobile App backend in the portal under **All settings** > **Application settings** > **Connection strings** > **Show connection string values** > **MS_TableConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="fa08d-113">You can get the connection string used by a Mobile App backend in the portal under **All settings** > **Application settings** > **Connection strings** > **Show connection string values** > **MS_TableConnectionString**.</span></span> <span data-ttu-id="fa08d-114">You can also get the connection string direct from a SQL Database in the portal under **All settings** > **Properties** > **Show database connection strings** > **ADO.NET (SQL authentication)**.</span><span class="sxs-lookup"><span data-stu-id="fa08d-114">You can also get the connection string direct from a SQL Database in the portal under **All settings** > **Properties** > **Show database connection strings** > **ADO.NET (SQL authentication)**.</span></span>

<span data-ttu-id="fa08d-115">This scenario uses a bulk operation against the database.</span><span class="sxs-lookup"><span data-stu-id="fa08d-115">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="fa08d-116">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use Mobile Table binding.</span><span class="sxs-lookup"><span data-stu-id="fa08d-116">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use Mobile Table binding.</span></span>

## <a name="set-a-sql-database-connection-string-in-the-function-app"></a><span data-ttu-id="fa08d-117">Set a SQL Database connection string in the function app</span><span class="sxs-lookup"><span data-stu-id="fa08d-117">Set a SQL Database connection string in the function app</span></span>
<span data-ttu-id="fa08d-118">A function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="fa08d-118">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="fa08d-119">It is a best practice to store connection strings and other secrets in your function app settings.</span><span class="sxs-lookup"><span data-stu-id="fa08d-119">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="fa08d-120">This prevents accidental disclosure when your function code ends-up in a repo somewhere.</span><span class="sxs-lookup"><span data-stu-id="fa08d-120">This prevents accidental disclosure when your function code ends-up in a repo somewhere.</span></span> 

1. <span data-ttu-id="fa08d-121">Go to the [Azure Functions portal](https://functions.azure.com/signin) and sign-in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="fa08d-121">Go to the [Azure Functions portal](https://functions.azure.com/signin) and sign-in with your Azure account.</span></span>
2. <span data-ttu-id="fa08d-122">If you have an existing function app to use, select it from **Your function apps** then click **Open**.</span><span class="sxs-lookup"><span data-stu-id="fa08d-122">If you have an existing function app to use, select it from **Your function apps** then click **Open**.</span></span> <span data-ttu-id="fa08d-123">To create a new function app, type a unique **Name** for your new function app or accept the generated one, select your preferred **Region**, then click **Create + get started**.</span><span class="sxs-lookup"><span data-stu-id="fa08d-123">To create a new function app, type a unique **Name** for your new function app or accept the generated one, select your preferred **Region**, then click **Create + get started**.</span></span> 
3. <span data-ttu-id="fa08d-124">In your function app, click **Function app settings** > **Go to App Service settings**.</span><span class="sxs-lookup"><span data-stu-id="fa08d-124">In your function app, click **Function app settings** > **Go to App Service settings**.</span></span> 
   
    ![Function app settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-event-processing-function/functions-app-service-settings.png)
4. <span data-ttu-id="fa08d-126">In your function app, click **All settings**, scroll down to **Application settings**, then under **Connection strings** type `sqldb_connection` for **Name**, paste the connection string into **Value**, click **Save**, then close the function app blade to return to the Functions portal.</span><span class="sxs-lookup"><span data-stu-id="fa08d-126">In your function app, click **All settings**, scroll down to **Application settings**, then under **Connection strings** type `sqldb_connection` for **Name**, paste the connection string into **Value**, click **Save**, then close the function app blade to return to the Functions portal.</span></span>
   
    ![App Service setting connection string](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-event-processing-function/functions-app-service-settings-connection-strings.png)

<span data-ttu-id="fa08d-128">Now, you can add the C# function code that connects to your SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fa08d-128">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="create-a-timer-triggered-function-from-the-template"></a><span data-ttu-id="fa08d-129">Create a timer-triggered function from the template</span><span class="sxs-lookup"><span data-stu-id="fa08d-129">Create a timer-triggered function from the template</span></span>
1. <span data-ttu-id="fa08d-130">In your function app, click **+ New Function** > **TimerTrigger - C#** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="fa08d-130">In your function app, click **+ New Function** > **TimerTrigger - C#** > **Create**.</span></span> <span data-ttu-id="fa08d-131">This creates a function with a default name that is run on the default schedule of once every minute.</span><span class="sxs-lookup"><span data-stu-id="fa08d-131">This creates a function with a default name that is run on the default schedule of once every minute.</span></span> 
   
    ![Create a new timer-triggered function](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-create-an-event-processing-function/functions-create-new-timer-trigger.png)
2. <span data-ttu-id="fa08d-133">In the **Code** pane in the **Develop** tab, add the following assembly references at the top of the existing function code:</span><span class="sxs-lookup"><span data-stu-id="fa08d-133">In the **Code** pane in the **Develop** tab, add the following assembly references at the top of the existing function code:</span></span>
    ```cs
        #r "System.Configuration"
        #r "System.Data"
    ```

3. <span data-ttu-id="fa08d-134">Add the following `using` statements to the function:</span><span class="sxs-lookup"><span data-stu-id="fa08d-134">Add the following `using` statements to the function:</span></span>
    ```cs
        using System.Configuration;
        using System.Data.SqlClient;
        using System.Threading.Tasks;
    ```

4. <span data-ttu-id="fa08d-135">Replace the existing **Run** function with the following code:</span><span class="sxs-lookup"><span data-stu-id="fa08d-135">Replace the existing **Run** function with the following code:</span></span>
    ```cs
        public static async Task Run(TimerInfo myTimer, TraceWriter log)
        {
            var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
            using (SqlConnection conn = new SqlConnection(str))
            {
                conn.Open();
                var text = "DELETE from dbo.TodoItems WHERE Complete='True'";
                using (SqlCommand cmd = new SqlCommand(text, conn))
                {
                    // Execute the command and log the # rows deleted.
                    var rows = await cmd.ExecuteNonQueryAsync();
                    log.Info($"{rows} rows were deleted");
                }
            }
        }
    ```

5. <span data-ttu-id="fa08d-136">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows deleted from the TodoItems table.</span><span class="sxs-lookup"><span data-stu-id="fa08d-136">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows deleted from the TodoItems table.</span></span>
6. <span data-ttu-id="fa08d-137">(Optional) Using the [Mobile Apps quickstart app](../app-service-mobile/app-service-mobile-ios-get-started.md), mark additional items as "completed" then return to the **Logs** window and watch the same number of rows get deleted by the function during the next execution.</span><span class="sxs-lookup"><span data-stu-id="fa08d-137">(Optional) Using the [Mobile Apps quickstart app](../app-service-mobile/app-service-mobile-ios-get-started.md), mark additional items as "completed" then return to the **Logs** window and watch the same number of rows get deleted by the function during the next execution.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fa08d-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa08d-138">Next steps</span></span>
<span data-ttu-id="fa08d-139">See these topics for more information about Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fa08d-139">See these topics for more information about Azure Functions.</span></span>

* [<span data-ttu-id="fa08d-140">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="fa08d-140">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="fa08d-141">Programmer reference for coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="fa08d-141">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="fa08d-142">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fa08d-142">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="fa08d-143">Describes various tools and techniques for testing your functions.</span><span class="sxs-lookup"><span data-stu-id="fa08d-143">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="fa08d-144">How to scale Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fa08d-144">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="fa08d-145">Discusses service plans available with Azure Functions, including the Consumption plan, and how to choose the right plan.</span><span class="sxs-lookup"><span data-stu-id="fa08d-145">Discusses service plans available with Azure Functions, including the Consumption plan, and how to choose the right plan.</span></span>  

[!INCLUDE [Getting Started Note](../../includes/functions-get-help.md)]




