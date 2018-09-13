---
title: Use Azure Functions to perform a database clean up task | Microsoft Docs
description: Use Azure Functions to schedule a task that connects to Azure SQL Database to periodically clean up rows.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: a257948c97437d6045f705acb02054928d22ff89
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821189"
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="6d497-103">Use Azure Functions to connect to an Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6d497-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="6d497-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6d497-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="6d497-105">The new C# script function is created based on a pre-defined timer trigger template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6d497-105">The new C# script function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="6d497-106">To support this scenario, you must also set a database connection string as an app setting in the function app.</span><span class="sxs-lookup"><span data-stu-id="6d497-106">To support this scenario, you must also set a database connection string as an app setting in the function app.</span></span> <span data-ttu-id="6d497-107">This scenario uses a bulk operation against the database.</span><span class="sxs-lookup"><span data-stu-id="6d497-107">This scenario uses a bulk operation against the database.</span></span> 

<span data-ttu-id="6d497-108">To have your function process individual create, read, update, and delete (CRUD) operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="6d497-108">To have your function process individual create, read, update, and delete (CRUD) operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d497-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6d497-109">Prerequisites</span></span>

+ <span data-ttu-id="6d497-110">This topic uses a timer triggered function.</span><span class="sxs-lookup"><span data-stu-id="6d497-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="6d497-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span><span class="sxs-lookup"><span data-stu-id="6d497-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="6d497-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span><span class="sxs-lookup"><span data-stu-id="6d497-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="6d497-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6d497-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="6d497-114">Get connection information</span><span class="sxs-lookup"><span data-stu-id="6d497-114">Get connection information</span></span>

<span data-ttu-id="6d497-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6d497-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="6d497-116">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6d497-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="6d497-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span><span class="sxs-lookup"><span data-stu-id="6d497-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="6d497-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span><span class="sxs-lookup"><span data-stu-id="6d497-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span> 

    ![Copy the ADO.NET connection string.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="6d497-120">Set the connection string</span><span class="sxs-lookup"><span data-stu-id="6d497-120">Set the connection string</span></span> 

<span data-ttu-id="6d497-121">A function app hosts the execution of your functions in Azure.</span><span class="sxs-lookup"><span data-stu-id="6d497-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="6d497-122">It is a best practice to store connection strings and other secrets in your function app settings.</span><span class="sxs-lookup"><span data-stu-id="6d497-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="6d497-123">Using application settings prevents accidental disclosure of the connection string with your code.</span><span class="sxs-lookup"><span data-stu-id="6d497-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="6d497-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="6d497-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="6d497-125">Select **Platform features** > **Application settings**.</span><span class="sxs-lookup"><span data-stu-id="6d497-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Application settings for the function app.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="6d497-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span><span class="sxs-lookup"><span data-stu-id="6d497-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Add a connection string to the function app settings.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="6d497-129">Setting</span><span class="sxs-lookup"><span data-stu-id="6d497-129">Setting</span></span>       | <span data-ttu-id="6d497-130">Suggested value</span><span class="sxs-lookup"><span data-stu-id="6d497-130">Suggested value</span></span> | <span data-ttu-id="6d497-131">Description</span><span class="sxs-lookup"><span data-stu-id="6d497-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="6d497-132">**Name**</span><span class="sxs-lookup"><span data-stu-id="6d497-132">**Name**</span></span>  |  <span data-ttu-id="6d497-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="6d497-133">sqldb_connection</span></span>  | <span data-ttu-id="6d497-134">Used to access the stored connection string in your function code.</span><span class="sxs-lookup"><span data-stu-id="6d497-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="6d497-135">**Value**</span><span class="sxs-lookup"><span data-stu-id="6d497-135">**Value**</span></span> | <span data-ttu-id="6d497-136">Copied string</span><span class="sxs-lookup"><span data-stu-id="6d497-136">Copied string</span></span>  | <span data-ttu-id="6d497-137">Paste the connection string you copied in the previous section and replace `{your_username}` and `{your_password}` placeholders with real values.</span><span class="sxs-lookup"><span data-stu-id="6d497-137">Paste the connection string you copied in the previous section and replace `{your_username}` and `{your_password}` placeholders with real values.</span></span> |
    | <span data-ttu-id="6d497-138">**Type**</span><span class="sxs-lookup"><span data-stu-id="6d497-138">**Type**</span></span> | <span data-ttu-id="6d497-139">SQL Database</span><span class="sxs-lookup"><span data-stu-id="6d497-139">SQL Database</span></span> | <span data-ttu-id="6d497-140">Use the default SQL Database connection.</span><span class="sxs-lookup"><span data-stu-id="6d497-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="6d497-141">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6d497-141">Click **Save**.</span></span>

<span data-ttu-id="6d497-142">Now, you can add the C# function code that connects to your SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6d497-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="6d497-143">Update your function code</span><span class="sxs-lookup"><span data-stu-id="6d497-143">Update your function code</span></span>

1. <span data-ttu-id="6d497-144">In your function app in the portal, select the timer-triggered function.</span><span class="sxs-lookup"><span data-stu-id="6d497-144">In your function app in the portal, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="6d497-145">Add the following assembly references at the top of the existing C# script function code:</span><span class="sxs-lookup"><span data-stu-id="6d497-145">Add the following assembly references at the top of the existing C# script function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```
    >[!NOTE]
    ><span data-ttu-id="6d497-146">The code in these examples are C# script from the portal.</span><span class="sxs-lookup"><span data-stu-id="6d497-146">The code in these examples are C# script from the portal.</span></span> <span data-ttu-id="6d497-147">When you are developing a precompiled C# function locally, you must instead add references to these assembles in your local project.</span><span class="sxs-lookup"><span data-stu-id="6d497-147">When you are developing a precompiled C# function locally, you must instead add references to these assembles in your local project.</span></span>  

3. <span data-ttu-id="6d497-148">Add the following `using` statements to the function:</span><span class="sxs-lookup"><span data-stu-id="6d497-148">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="6d497-149">Replace the existing `Run` function with the following code:</span><span class="sxs-lookup"><span data-stu-id="6d497-149">Replace the existing `Run` function with the following code:</span></span>
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="6d497-150">This sample command updates the `Status` column based on the ship date.</span><span class="sxs-lookup"><span data-stu-id="6d497-150">This sample command updates the `Status` column based on the ship date.</span></span> <span data-ttu-id="6d497-151">It should update 32 rows of data.</span><span class="sxs-lookup"><span data-stu-id="6d497-151">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="6d497-152">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span><span class="sxs-lookup"><span data-stu-id="6d497-152">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![View the function logs.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="6d497-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d497-154">Next steps</span></span>

<span data-ttu-id="6d497-155">Next, learn how to use Functions with Logic Apps to integrate with other services.</span><span class="sxs-lookup"><span data-stu-id="6d497-155">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="6d497-156">Create a function that integrates with Logic Apps</span><span class="sxs-lookup"><span data-stu-id="6d497-156">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="6d497-157">For more information about Functions, see the following topics:</span><span class="sxs-lookup"><span data-stu-id="6d497-157">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="6d497-158">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="6d497-158">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="6d497-159">Programmer reference for coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="6d497-159">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="6d497-160">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="6d497-160">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="6d497-161">Describes various tools and techniques for testing your functions.</span><span class="sxs-lookup"><span data-stu-id="6d497-161">Describes various tools and techniques for testing your functions.</span></span>  
