---
title: Tutorial - Configure Azure Analysis Services server administrator and user roles tutorial lesson | Microsoft Docs
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: tutorial
ms.date: 07/09/2018
ms.author: owend
ms.reviewer: owend
ms.openlocfilehash: 1c1dd5316eead5e91dd77d3e6b21a7a14d39afeb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856065"
---
# <a name="tutorial-configure-server-administrator-and-user-roles"></a><span data-ttu-id="04ed1-102">Tutorial: Configure server administrator and user roles</span><span class="sxs-lookup"><span data-stu-id="04ed1-102">Tutorial: Configure server administrator and user roles</span></span>

 <span data-ttu-id="04ed1-103">In this tutorial, you use SQL Server Management Studio (SSMS) to connect to your server in Azure to configure server administrator and model database roles.</span><span class="sxs-lookup"><span data-stu-id="04ed1-103">In this tutorial, you use SQL Server Management Studio (SSMS) to connect to your server in Azure to configure server administrator and model database roles.</span></span> <span data-ttu-id="04ed1-104">You're also introduced  to [Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200).</span><span class="sxs-lookup"><span data-stu-id="04ed1-104">You're also introduced  to [Tabular Model Scripting Language (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200).</span></span> <span data-ttu-id="04ed1-105">TMSL is a JSON-based scripting language for tabular models at the 1200 and higher compatibility levels.</span><span class="sxs-lookup"><span data-stu-id="04ed1-105">TMSL is a JSON-based scripting language for tabular models at the 1200 and higher compatibility levels.</span></span> <span data-ttu-id="04ed1-106">It can be used to automate many tabular modeling tasks.</span><span class="sxs-lookup"><span data-stu-id="04ed1-106">It can be used to automate many tabular modeling tasks.</span></span> <span data-ttu-id="04ed1-107">TMSL is often used with PowerShell, but in this tutorial, you use the XMLA query editor in SSMS.</span><span class="sxs-lookup"><span data-stu-id="04ed1-107">TMSL is often used with PowerShell, but in this tutorial, you use the XMLA query editor in SSMS.</span></span> <span data-ttu-id="04ed1-108">With this tutorial, you complete these tasks:</span><span class="sxs-lookup"><span data-stu-id="04ed1-108">With this tutorial, you complete these tasks:</span></span> 
  
> [!div class="checklist"]
> * <span data-ttu-id="04ed1-109">Get your server name from the portal</span><span class="sxs-lookup"><span data-stu-id="04ed1-109">Get your server name from the portal</span></span>
> * <span data-ttu-id="04ed1-110">Connect to your server by using SSMS</span><span class="sxs-lookup"><span data-stu-id="04ed1-110">Connect to your server by using SSMS</span></span>
> * <span data-ttu-id="04ed1-111">Add a user or group to the server administrator role</span><span class="sxs-lookup"><span data-stu-id="04ed1-111">Add a user or group to the server administrator role</span></span> 
> * <span data-ttu-id="04ed1-112">Add a user or group to the model database administrator role</span><span class="sxs-lookup"><span data-stu-id="04ed1-112">Add a user or group to the model database administrator role</span></span>
> * <span data-ttu-id="04ed1-113">Add a new model database role and add a user or group</span><span class="sxs-lookup"><span data-stu-id="04ed1-113">Add a new model database role and add a user or group</span></span>

<span data-ttu-id="04ed1-114">To learn more about user security in Azure Analysis Services, see [Authentication and user permissions](../analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="04ed1-114">To learn more about user security in Azure Analysis Services, see [Authentication and user permissions](../analysis-services-manage-users.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="04ed1-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04ed1-115">Prerequisites</span></span>

- <span data-ttu-id="04ed1-116">An Azure Active Directory in your subscription.</span><span class="sxs-lookup"><span data-stu-id="04ed1-116">An Azure Active Directory in your subscription.</span></span>
- <span data-ttu-id="04ed1-117">Created an [Azure Analysis Services server](../analysis-services-create-server.md) in your subscription.</span><span class="sxs-lookup"><span data-stu-id="04ed1-117">Created an [Azure Analysis Services server](../analysis-services-create-server.md) in your subscription.</span></span>
- <span data-ttu-id="04ed1-118">Have [server administrator](../analysis-services-server-admins.md) permissions.</span><span class="sxs-lookup"><span data-stu-id="04ed1-118">Have [server administrator](../analysis-services-server-admins.md) permissions.</span></span>
- <span data-ttu-id="04ed1-119">[Add the adventureworks sample model](../analysis-services-create-sample-model.md) to your server.</span><span class="sxs-lookup"><span data-stu-id="04ed1-119">[Add the adventureworks sample model](../analysis-services-create-sample-model.md) to your server.</span></span>
- <span data-ttu-id="04ed1-120">[Install the latest version of SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="04ed1-120">[Install the latest version of SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="04ed1-121">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="04ed1-121">Log in to the Azure portal</span></span>

<span data-ttu-id="04ed1-122">Log in to the [portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="04ed1-122">Log in to the [portal](https://portal.azure.com/).</span></span>

## <a name="get-server-name"></a><span data-ttu-id="04ed1-123">Get server name</span><span class="sxs-lookup"><span data-stu-id="04ed1-123">Get server name</span></span>
<span data-ttu-id="04ed1-124">In order to connect to your server from SSMS, you first need the server name.</span><span class="sxs-lookup"><span data-stu-id="04ed1-124">In order to connect to your server from SSMS, you first need the server name.</span></span> <span data-ttu-id="04ed1-125">You can get the server name from the portal.</span><span class="sxs-lookup"><span data-stu-id="04ed1-125">You can get the server name from the portal.</span></span>

<span data-ttu-id="04ed1-126">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span><span class="sxs-lookup"><span data-stu-id="04ed1-126">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
   ![Get server name in Azure](./media/analysis-services-tutorial-roles/aas-copy-server-name.png)

## <a name="connect-in-ssms"></a><span data-ttu-id="04ed1-128">Connect in SSMS</span><span class="sxs-lookup"><span data-stu-id="04ed1-128">Connect in SSMS</span></span>

<span data-ttu-id="04ed1-129">For the remaining tasks, you use SSMS to connect to and manage your server.</span><span class="sxs-lookup"><span data-stu-id="04ed1-129">For the remaining tasks, you use SSMS to connect to and manage your server.</span></span>

1. <span data-ttu-id="04ed1-130">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-130">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>

    ![Connect](./media/analysis-services-tutorial-roles/aas-ssms-connect.png)

2. <span data-ttu-id="04ed1-132">In the **Connect to Server** dialog box, in **Server name**, paste in the server name you copied from the portal.</span><span class="sxs-lookup"><span data-stu-id="04ed1-132">In the **Connect to Server** dialog box, in **Server name**, paste in the server name you copied from the portal.</span></span> <span data-ttu-id="04ed1-133">In **Authentication**, choose **Active Directory Universal with MFA Support**, then enter your user account, and then press **Connect**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-133">In **Authentication**, choose **Active Directory Universal with MFA Support**, then enter your user account, and then press **Connect**.</span></span>
   
    ![Connect in SSMS](./media/analysis-services-tutorial-roles/aas-connect-ssms-auth.png)

    > [!TIP]
    > <span data-ttu-id="04ed1-135">Choosing Active Directory Universal with MFA Support is recommended.</span><span class="sxs-lookup"><span data-stu-id="04ed1-135">Choosing Active Directory Universal with MFA Support is recommended.</span></span> <span data-ttu-id="04ed1-136">This type of authentication type supports [non-interactive and multi-factor authentication](../../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="04ed1-136">This type of authentication type supports [non-interactive and multi-factor authentication](../../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 

3. <span data-ttu-id="04ed1-137">In **Object Explorer**, expand to see server objects.</span><span class="sxs-lookup"><span data-stu-id="04ed1-137">In **Object Explorer**, expand to see server objects.</span></span> <span data-ttu-id="04ed1-138">Right-click to see server properties.</span><span class="sxs-lookup"><span data-stu-id="04ed1-138">Right-click to see server properties.</span></span>
   
    ![Connect in SSMS](./media/analysis-services-tutorial-roles/aas-connect-ssms-objexp.png)

## <a name="add-a-user-account-to-the-server-administrator-role"></a><span data-ttu-id="04ed1-140">Add a user account to the server administrator role</span><span class="sxs-lookup"><span data-stu-id="04ed1-140">Add a user account to the server administrator role</span></span>

<span data-ttu-id="04ed1-141">In this task, you add a user or group account from your Azure AD to the server administrator role.</span><span class="sxs-lookup"><span data-stu-id="04ed1-141">In this task, you add a user or group account from your Azure AD to the server administrator role.</span></span> <span data-ttu-id="04ed1-142">If you're adding a security group, it must have the `MailEnabled` property set to `True`.</span><span class="sxs-lookup"><span data-stu-id="04ed1-142">If you're adding a security group, it must have the `MailEnabled` property set to `True`.</span></span>

1. <span data-ttu-id="04ed1-143">In **Object Explorer**, right-click your server name, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-143">In **Object Explorer**, right-click your server name, and then click **Properties**.</span></span> 
2. <span data-ttu-id="04ed1-144">In the **Analysis Server Properties** window, click **Security** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-144">In the **Analysis Server Properties** window, click **Security** > **Add**.</span></span>
3. <span data-ttu-id="04ed1-145">In the **Select a User or Group** window, enter a user or group account in your Azure AD, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-145">In the **Select a User or Group** window, enter a user or group account in your Azure AD, and then click **Add**.</span></span> 
   
     ![Add server admin](./media/analysis-services-tutorial-roles/aas-add-server-admin.png)

4. <span data-ttu-id="04ed1-147">Click **OK**, to close **Analysis Server Properties**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-147">Click **OK**, to close **Analysis Server Properties**.</span></span>

    > [!TIP]
    > <span data-ttu-id="04ed1-148">You can also add server administrators by using **Analysis Services Admins** in the portal.</span><span class="sxs-lookup"><span data-stu-id="04ed1-148">You can also add server administrators by using **Analysis Services Admins** in the portal.</span></span> 

## <a name="add-a-user-to-the-model-database-administrator-role"></a><span data-ttu-id="04ed1-149">Add a user to the model database administrator role</span><span class="sxs-lookup"><span data-stu-id="04ed1-149">Add a user to the model database administrator role</span></span>

<span data-ttu-id="04ed1-150">In this task, you add a user or group account to the Internet Sales Administrator role that already exists in the model.</span><span class="sxs-lookup"><span data-stu-id="04ed1-150">In this task, you add a user or group account to the Internet Sales Administrator role that already exists in the model.</span></span> <span data-ttu-id="04ed1-151">This role has Full control (Administrator) permissions for the adventureworks sample model database.</span><span class="sxs-lookup"><span data-stu-id="04ed1-151">This role has Full control (Administrator) permissions for the adventureworks sample model database.</span></span> <span data-ttu-id="04ed1-152">This task uses the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) TMSL command in a script created for you.</span><span class="sxs-lookup"><span data-stu-id="04ed1-152">This task uses the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) TMSL command in a script created for you.</span></span>

1. <span data-ttu-id="04ed1-153">In **Object Explorer**, expand **Databases** > **adventureworks** > **Roles**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-153">In **Object Explorer**, expand **Databases** > **adventureworks** > **Roles**.</span></span> 
2. <span data-ttu-id="04ed1-154">Right-click **Internet Sales Administrator**, then click **Script Role as** > **CREATE OR REPLACE To** > **New Query Editor Window**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-154">Right-click **Internet Sales Administrator**, then click **Script Role as** > **CREATE OR REPLACE To** > **New Query Editor Window**.</span></span>

    ![New Query Editor Window](./media/analysis-services-tutorial-roles/aas-add-db-admin.png)

3. <span data-ttu-id="04ed1-156">In the **XMLAQuery**, change the value for **"memberName":** to a user or group account in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04ed1-156">In the **XMLAQuery**, change the value for **"memberName":** to a user or group account in your Azure AD.</span></span> <span data-ttu-id="04ed1-157">By default, the account you're signed in with is included; however, you do not need to add your own account because you are already a server administrator.</span><span class="sxs-lookup"><span data-stu-id="04ed1-157">By default, the account you're signed in with is included; however, you do not need to add your own account because you are already a server administrator.</span></span>

    ![TMSL script in XMLA query](./media/analysis-services-tutorial-roles/aas-add-db-admin-script.png)

4. <span data-ttu-id="04ed1-159">Press **F5**, to execute the script.</span><span class="sxs-lookup"><span data-stu-id="04ed1-159">Press **F5**, to execute the script.</span></span>


## <a name="add-a-new-model-database-role-and-add-a-user-or-group"></a><span data-ttu-id="04ed1-160">Add a new model database role and add a user or group</span><span class="sxs-lookup"><span data-stu-id="04ed1-160">Add a new model database role and add a user or group</span></span>

<span data-ttu-id="04ed1-161">In this task, you use the [Create](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/create-command-tmsl?view=sql-analysis-services-2017) command in a TMSL script to create a new Internet Sales Global role, specify *read* permissions for the role, and add a user or group account from your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04ed1-161">In this task, you use the [Create](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/create-command-tmsl?view=sql-analysis-services-2017) command in a TMSL script to create a new Internet Sales Global role, specify *read* permissions for the role, and add a user or group account from your Azure AD.</span></span>

1. <span data-ttu-id="04ed1-162">In **Object Explorer**, right-click **adventureworks**, and then click **New Query** > **XMLA**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-162">In **Object Explorer**, right-click **adventureworks**, and then click **New Query** > **XMLA**.</span></span> 
2. <span data-ttu-id="04ed1-163">Copy and paste the following TMSL script into the query editor:</span><span class="sxs-lookup"><span data-stu-id="04ed1-163">Copy and paste the following TMSL script into the query editor:</span></span>

    ```JSON
    {
    "create": {
      "parentObject": {
        "database": "adventureworks",
       },
       "role": {
         "name": "Internet Sales Global",
         "description": "All users can query model data",
         "modelPermission": "read",
         "members": [
           {
             "memberName": "globalsales@adventureworks.com",
             "identityProvider": "AzureAD"
           }
         ]
       }
      }
    }
    ```

3. <span data-ttu-id="04ed1-164">Change `"memberName": "globalsales@adventureworks.com"` object value to a user or group account in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04ed1-164">Change `"memberName": "globalsales@adventureworks.com"` object value to a user or group account in your Azure AD.</span></span>
4. <span data-ttu-id="04ed1-165">Press **F5**, to execute the script.</span><span class="sxs-lookup"><span data-stu-id="04ed1-165">Press **F5**, to execute the script.</span></span>

## <a name="verify-your-changes"></a><span data-ttu-id="04ed1-166">Verify your changes</span><span class="sxs-lookup"><span data-stu-id="04ed1-166">Verify your changes</span></span>

1. <span data-ttu-id="04ed1-167">In **Object Explorer**, click your servername, and then click **Refresh** or press **F5**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-167">In **Object Explorer**, click your servername, and then click **Refresh** or press **F5**.</span></span>
2. <span data-ttu-id="04ed1-168">Expand **Databases** > **adventureworks** > **Roles**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-168">Expand **Databases** > **adventureworks** > **Roles**.</span></span> <span data-ttu-id="04ed1-169">Verify the user account and new role changes you added in the previous tasks appear.</span><span class="sxs-lookup"><span data-stu-id="04ed1-169">Verify the user account and new role changes you added in the previous tasks appear.</span></span>   

    ![Verify in Object Explorer](./media/analysis-services-tutorial-roles/aas-connect-ssms-verify.png)

## <a name="clean-up-resources"></a><span data-ttu-id="04ed1-171">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="04ed1-171">Clean up resources</span></span>

<span data-ttu-id="04ed1-172">When no longer needed, delete the user or group accounts and roles.</span><span class="sxs-lookup"><span data-stu-id="04ed1-172">When no longer needed, delete the user or group accounts and roles.</span></span> <span data-ttu-id="04ed1-173">To do so, use **Role Properties** > **Membership** to remove user accounts, or right-click a role and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="04ed1-173">To do so, use **Role Properties** > **Membership** to remove user accounts, or right-click a role and then click **Delete**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="04ed1-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="04ed1-174">Next steps</span></span>
<span data-ttu-id="04ed1-175">In this tutorial, you learned how to connect to your Azure AS server and explore the adventureworks sample model databases and properties in SSMS.</span><span class="sxs-lookup"><span data-stu-id="04ed1-175">In this tutorial, you learned how to connect to your Azure AS server and explore the adventureworks sample model databases and properties in SSMS.</span></span> <span data-ttu-id="04ed1-176">You also learned how to use SSMS and TMSL scripts to add users or groups to existing and new roles.</span><span class="sxs-lookup"><span data-stu-id="04ed1-176">You also learned how to use SSMS and TMSL scripts to add users or groups to existing and new roles.</span></span> <span data-ttu-id="04ed1-177">Now that you have user permissions configured for your server and sample model database, you and other users can connect to it by using client applications like Power BI.</span><span class="sxs-lookup"><span data-stu-id="04ed1-177">Now that you have user permissions configured for your server and sample model database, you and other users can connect to it by using client applications like Power BI.</span></span> <span data-ttu-id="04ed1-178">To learn more, continue to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="04ed1-178">To learn more, continue to the next tutorial.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="04ed1-179">Tutorial: Connect with Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="04ed1-179">Tutorial: Connect with Power BI Desktop</span></span>](analysis-services-tutorial-pbid.md)

