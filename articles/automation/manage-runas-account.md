---
title: Manage Azure Automation Run As accounts
description: This article describes how to manage your Run As accounts with PowerShell, or from the portal.
services: automation
ms.service: automation
ms.component: shared-capabilities
author: georgewallace
ms.author: gwallace
ms.date: 08/16/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 2d6b58c95b918d820e207e801e62e7897c2ee366
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870282"
---
# <a name="manage-azure-automation-run-as-accounts"></a><span data-ttu-id="08975-103">Manage Azure Automation Run As accounts</span><span class="sxs-lookup"><span data-stu-id="08975-103">Manage Azure Automation Run As accounts</span></span>

<span data-ttu-id="08975-104">Run As accounts in Azure Automation are used to provide authentication for managing resources in Azure with the Azure cmdlets.</span><span class="sxs-lookup"><span data-stu-id="08975-104">Run As accounts in Azure Automation are used to provide authentication for managing resources in Azure with the Azure cmdlets.</span></span>

<span data-ttu-id="08975-105">When you create a Run As account, it creates a new service principal user in Azure Active Directory and assigns the Contributor role to this user at the subscription level.</span><span class="sxs-lookup"><span data-stu-id="08975-105">When you create a Run As account, it creates a new service principal user in Azure Active Directory and assigns the Contributor role to this user at the subscription level.</span></span>

<span data-ttu-id="08975-106">There are two types of Run As Accounts:</span><span class="sxs-lookup"><span data-stu-id="08975-106">There are two types of Run As Accounts:</span></span>

* <span data-ttu-id="08975-107">**Azure Run As Account** - This account is used to manage Resource Manager deployment model resources.</span><span class="sxs-lookup"><span data-stu-id="08975-107">**Azure Run As Account** - This account is used to manage Resource Manager deployment model resources.</span></span>
  * <span data-ttu-id="08975-108">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span><span class="sxs-lookup"><span data-stu-id="08975-108">Creates an Azure AD application with a self-signed certificate, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="08975-109">You can change this setting to Owner or any other role.</span><span class="sxs-lookup"><span data-stu-id="08975-109">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="08975-110">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="08975-110">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
  * <span data-ttu-id="08975-111">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="08975-111">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="08975-112">The certificate asset holds the certificate private key that's used by the Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="08975-112">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
  * <span data-ttu-id="08975-113">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="08975-113">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="08975-114">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span><span class="sxs-lookup"><span data-stu-id="08975-114">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

* <span data-ttu-id="08975-115">**Azure Classic Run As Account** - This account is used to manage Classic deployment model resources.</span><span class="sxs-lookup"><span data-stu-id="08975-115">**Azure Classic Run As Account** - This account is used to manage Classic deployment model resources.</span></span>
  * <span data-ttu-id="08975-116">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="08975-116">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="08975-117">The certificate asset holds the certificate private key used by the management certificate.</span><span class="sxs-lookup"><span data-stu-id="08975-117">The certificate asset holds the certificate private key used by the management certificate.</span></span>
  * <span data-ttu-id="08975-118">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="08975-118">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="08975-119">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span><span class="sxs-lookup"><span data-stu-id="08975-119">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

## <a name="permissions"></a><span data-ttu-id="08975-120">Permissions to configure Run As accounts</span><span class="sxs-lookup"><span data-stu-id="08975-120">Permissions to configure Run As accounts</span></span>

<span data-ttu-id="08975-121">To create or update a Run As account, you must have specific privileges and permissions.</span><span class="sxs-lookup"><span data-stu-id="08975-121">To create or update a Run As account, you must have specific privileges and permissions.</span></span> <span data-ttu-id="08975-122">A Global Administrator/Co-Administrator can complete all the tasks.</span><span class="sxs-lookup"><span data-stu-id="08975-122">A Global Administrator/Co-Administrator can complete all the tasks.</span></span> <span data-ttu-id="08975-123">In a situation where you have seperation of duties, the following table shows a listing of the tasks, the equivalent cmdlet and permissions needed:</span><span class="sxs-lookup"><span data-stu-id="08975-123">In a situation where you have seperation of duties, the following table shows a listing of the tasks, the equivalent cmdlet and permissions needed:</span></span>

|<span data-ttu-id="08975-124">Task</span><span class="sxs-lookup"><span data-stu-id="08975-124">Task</span></span>|<span data-ttu-id="08975-125">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="08975-125">Cmdlet</span></span>  |<span data-ttu-id="08975-126">Minimum Permissions</span><span class="sxs-lookup"><span data-stu-id="08975-126">Minimum Permissions</span></span>  |
|---|---------|---------|
|<span data-ttu-id="08975-127">Create Azure AD Application</span><span class="sxs-lookup"><span data-stu-id="08975-127">Create Azure AD Application</span></span>|[<span data-ttu-id="08975-128">New-AzureRmADApplication</span><span class="sxs-lookup"><span data-stu-id="08975-128">New-AzureRmADApplication</span></span>](/powershell/module/azurerm.resources/new-azurermadapplication)     | <span data-ttu-id="08975-129">Application Developer Role</span><span class="sxs-lookup"><span data-stu-id="08975-129">Application Developer Role</span></span>        |
|<span data-ttu-id="08975-130">Add a credential to the application.</span><span class="sxs-lookup"><span data-stu-id="08975-130">Add a credential to the application.</span></span>|[<span data-ttu-id="08975-131">New-AzureRmADAppCredential</span><span class="sxs-lookup"><span data-stu-id="08975-131">New-AzureRmADAppCredential</span></span>](/powershell/module/AzureRM.Resources/New-AzureRmADAppCredential)     | <span data-ttu-id="08975-132">Application administrator or GLOBAL ADMIN</span><span class="sxs-lookup"><span data-stu-id="08975-132">Application administrator or GLOBAL ADMIN</span></span>         |
|<span data-ttu-id="08975-133">Create and Get an Azure AD service principal</span><span class="sxs-lookup"><span data-stu-id="08975-133">Create and Get an Azure AD service principal</span></span>|[<span data-ttu-id="08975-134">New-AzureRMADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="08975-134">New-AzureRMADServicePrincipal</span></span>](/powershell/module/AzureRM.Resources/New-AzureRmADServicePrincipal)</br>[<span data-ttu-id="08975-135">Get-AzureRmADServicePrincipal</span><span class="sxs-lookup"><span data-stu-id="08975-135">Get-AzureRmADServicePrincipal</span></span>](/powershell/module/AzureRM.Resources/Get-AzureRmADServicePrincipal)     | <span data-ttu-id="08975-136">Application administrator or GLOBAL ADMIN</span><span class="sxs-lookup"><span data-stu-id="08975-136">Application administrator or GLOBAL ADMIN</span></span>        |
|<span data-ttu-id="08975-137">Assign or get the RBAC role for the specified principal</span><span class="sxs-lookup"><span data-stu-id="08975-137">Assign or get the RBAC role for the specified principal</span></span>|[<span data-ttu-id="08975-138">New-AzureRMRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="08975-138">New-AzureRMRoleAssignment</span></span>](/powershell/module/AzureRM.Resources/New-AzureRmRoleAssignment)</br>[<span data-ttu-id="08975-139">Get-AzureRMRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="08975-139">Get-AzureRMRoleAssignment</span></span>](/powershell/module/AzureRM.Resources/Get-AzureRmRoleAssignment)      | <span data-ttu-id="08975-140">User Access Administrator or Owner</span><span class="sxs-lookup"><span data-stu-id="08975-140">User Access Administrator or Owner</span></span>        |
|<span data-ttu-id="08975-141">Create or remove an Automation certificate</span><span class="sxs-lookup"><span data-stu-id="08975-141">Create or remove an Automation certificate</span></span>|[<span data-ttu-id="08975-142">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="08975-142">New-AzureRmAutomationCertificate</span></span>](/powershell/module/AzureRM.Automation/New-AzureRmAutomationCertificate)</br>[<span data-ttu-id="08975-143">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="08975-143">Remove-AzureRmAutomationCertificate</span></span>](/powershell/module/AzureRM.Automation/Remove-AzureRmAutomationCertificate)     | <span data-ttu-id="08975-144">Contributor on Resource Group</span><span class="sxs-lookup"><span data-stu-id="08975-144">Contributor on Resource Group</span></span>         |
|<span data-ttu-id="08975-145">Create or remove an Automation connection</span><span class="sxs-lookup"><span data-stu-id="08975-145">Create or remove an Automation connection</span></span>|[<span data-ttu-id="08975-146">New-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="08975-146">New-AzureRmAutomationConnection</span></span>](/powershell/module/AzureRM.Automation/New-AzureRmAutomationConnection)</br>[<span data-ttu-id="08975-147">Remove-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="08975-147">Remove-AzureRmAutomationConnection</span></span>](/powershell/module/AzureRM.Automation/Remove-AzureRmAutomationConnection)|<span data-ttu-id="08975-148">Contributor on Resource Group</span><span class="sxs-lookup"><span data-stu-id="08975-148">Contributor on Resource Group</span></span> |

* <span data-ttu-id="08975-149">An AD user account with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor).</span><span class="sxs-lookup"><span data-stu-id="08975-149">An AD user account with permissions equivalent to the Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor).</span></span>  
* <span data-ttu-id="08975-150">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the Azure AD tenant's **Users can register applications** option in **User settings** page is set to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="08975-150">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if the Azure AD tenant's **Users can register applications** option in **User settings** page is set to **Yes**.</span></span> <span data-ttu-id="08975-151">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08975-151">If the app registrations setting is set to **No**, the user performing this action must be a global administrator in Azure AD.</span></span>

<span data-ttu-id="08975-152">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span><span class="sxs-lookup"><span data-stu-id="08975-152">If you are not a member of the subscription’s Active Directory instance before you are added to the global administrator/co-administrator role of the subscription, you are added to Active Directory as a guest.</span></span> <span data-ttu-id="08975-153">In this situation, you receive a `You do not have permissions to create…` warning on the **Add Automation Account** page.</span><span class="sxs-lookup"><span data-stu-id="08975-153">In this situation, you receive a `You do not have permissions to create…` warning on the **Add Automation Account** page.</span></span> <span data-ttu-id="08975-154">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and readded to make them a full User in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="08975-154">Users who were added to the global administrator/co-administrator role first can be removed from the subscription's Active Directory instance and readded to make them a full User in Active Directory.</span></span> <span data-ttu-id="08975-155">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span><span class="sxs-lookup"><span data-stu-id="08975-155">To verify this situation, from the **Azure Active Directory** pane in the Azure portal, select **Users and groups**, select **All users** and, after you select the specific user, select **Profile**.</span></span> <span data-ttu-id="08975-156">The value of the **User type** attribute under the users profile should not equal **Guest**.</span><span class="sxs-lookup"><span data-stu-id="08975-156">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>

## <a name="create-a-run-as-account-in-the-portal"></a><span data-ttu-id="08975-157">Create a Run As account in the Portal</span><span class="sxs-lookup"><span data-stu-id="08975-157">Create a Run As account in the Portal</span></span>

<span data-ttu-id="08975-158">In this section, perform the following steps to update your Azure Automation account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="08975-158">In this section, perform the following steps to update your Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="08975-159">You create the Run As and Classic Run As accounts individually.</span><span class="sxs-lookup"><span data-stu-id="08975-159">You create the Run As and Classic Run As accounts individually.</span></span> <span data-ttu-id="08975-160">If you don't need to manage classic resources, you can just create the Azure Run As account.</span><span class="sxs-lookup"><span data-stu-id="08975-160">If you don't need to manage classic resources, you can just create the Azure Run As account.</span></span>  

1. <span data-ttu-id="08975-161">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span><span class="sxs-lookup"><span data-stu-id="08975-161">Sign in to the Azure portal with an account that is a member of the Subscription Admins role and co-administrator of the subscription.</span></span>
1. <span data-ttu-id="08975-162">In the Azure portal, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="08975-162">In the Azure portal, click **All services**.</span></span> <span data-ttu-id="08975-163">In the list of resources, type **Automation**.</span><span class="sxs-lookup"><span data-stu-id="08975-163">In the list of resources, type **Automation**.</span></span> <span data-ttu-id="08975-164">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="08975-164">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="08975-165">Select **Automation Accounts**.</span><span class="sxs-lookup"><span data-stu-id="08975-165">Select **Automation Accounts**.</span></span>
1. <span data-ttu-id="08975-166">On the **Automation Accounts** page, select your Automation account from the list of Automation accounts.</span><span class="sxs-lookup"><span data-stu-id="08975-166">On the **Automation Accounts** page, select your Automation account from the list of Automation accounts.</span></span>
1. <span data-ttu-id="08975-167">In the left-hand pane, select **Run As Accounts** under the section **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="08975-167">In the left-hand pane, select **Run As Accounts** under the section **Account Settings**.</span></span>  
1. <span data-ttu-id="08975-168">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span><span class="sxs-lookup"><span data-stu-id="08975-168">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span> <span data-ttu-id="08975-169">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** pane appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span><span class="sxs-lookup"><span data-stu-id="08975-169">After selecting either the **Add Azure Run As** or **Add Azure Classic Run As Account** pane appears and after reviewing the overview information, click **Create** to proceed with Run As account creation.</span></span>  
1. <span data-ttu-id="08975-170">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="08975-170">While Azure creates the Run As account, you can track the progress under **Notifications** from the menu.</span></span> <span data-ttu-id="08975-171">A banner is also displayed stating the account is being created.</span><span class="sxs-lookup"><span data-stu-id="08975-171">A banner is also displayed stating the account is being created.</span></span> <span data-ttu-id="08975-172">This process can take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="08975-172">This process can take a few minutes to complete.</span></span>  

## <a name="create-run-as-account-using-powershell"></a><span data-ttu-id="08975-173">Create Run As account using PowerShell</span><span class="sxs-lookup"><span data-stu-id="08975-173">Create Run As account using PowerShell</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08975-174">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="08975-174">Prerequisites</span></span>

<span data-ttu-id="08975-175">The following list provides the requirements to create a Run As account in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="08975-175">The following list provides the requirements to create a Run As account in PowerShell:</span></span>

* <span data-ttu-id="08975-176">Windows 10 or Windows Server 2016 with Azure Resource Manager modules 3.4.1 and later.</span><span class="sxs-lookup"><span data-stu-id="08975-176">Windows 10 or Windows Server 2016 with Azure Resource Manager modules 3.4.1 and later.</span></span> <span data-ttu-id="08975-177">The PowerShell script does not support earlier versions of Windows.</span><span class="sxs-lookup"><span data-stu-id="08975-177">The PowerShell script does not support earlier versions of Windows.</span></span>
* <span data-ttu-id="08975-178">Azure PowerShell 1.0 and later.</span><span class="sxs-lookup"><span data-stu-id="08975-178">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="08975-179">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="08975-179">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="08975-180">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters.</span><span class="sxs-lookup"><span data-stu-id="08975-180">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters.</span></span>
* <span data-ttu-id="08975-181">Permissions equivalent to what is listed in [Required permissions to configure Run As accounts](#permissions)</span><span class="sxs-lookup"><span data-stu-id="08975-181">Permissions equivalent to what is listed in [Required permissions to configure Run As accounts](#permissions)</span></span>

<span data-ttu-id="08975-182">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span><span class="sxs-lookup"><span data-stu-id="08975-182">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the script, do the following:</span></span>

1. <span data-ttu-id="08975-183">In the Azure portal, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="08975-183">In the Azure portal, click **All services**.</span></span> <span data-ttu-id="08975-184">In the list of resources, type **Automation**.</span><span class="sxs-lookup"><span data-stu-id="08975-184">In the list of resources, type **Automation**.</span></span> <span data-ttu-id="08975-185">As you begin typing, the list filters based on your input.</span><span class="sxs-lookup"><span data-stu-id="08975-185">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="08975-186">Select **Automation Accounts**.</span><span class="sxs-lookup"><span data-stu-id="08975-186">Select **Automation Accounts**.</span></span>
1. <span data-ttu-id="08975-187">On the Automation account page, select your Automation account, and then under **Account Settings** select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="08975-187">On the Automation account page, select your Automation account, and then under **Account Settings** select **Properties**.</span></span>  
1. <span data-ttu-id="08975-188">Note the **Subscription ID**, **Name**, and **Resource Group** values on the **Properties** page.</span><span class="sxs-lookup"><span data-stu-id="08975-188">Note the **Subscription ID**, **Name**, and **Resource Group** values on the **Properties** page.</span></span>

   ![The Automation account "Properties" page](media/manage-runas-account/automation-account-properties.png)

<span data-ttu-id="08975-190">This PowerShell script includes support for the following configurations:</span><span class="sxs-lookup"><span data-stu-id="08975-190">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="08975-191">Create a Run As account by using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="08975-191">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="08975-192">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="08975-192">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="08975-193">Create a Run As account and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span><span class="sxs-lookup"><span data-stu-id="08975-193">Create a Run As account and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>
* <span data-ttu-id="08975-194">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span><span class="sxs-lookup"><span data-stu-id="08975-194">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

>[!NOTE]
> <span data-ttu-id="08975-195">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span><span class="sxs-lookup"><span data-stu-id="08975-195">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>

1. <span data-ttu-id="08975-196">Save the following script on your computer.</span><span class="sxs-lookup"><span data-stu-id="08975-196">Save the following script on your computer.</span></span> <span data-ttu-id="08975-197">In this example, save it with the filename *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="08975-197">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

   <span data-ttu-id="08975-198">The script uses multiple Azure Resource Manager cmdlets to create resources.</span><span class="sxs-lookup"><span data-stu-id="08975-198">The script uses multiple Azure Resource Manager cmdlets to create resources.</span></span> <span data-ttu-id="08975-199">The following table shows the cmdlets and their permissions needed.</span><span class="sxs-lookup"><span data-stu-id="08975-199">The following table shows the cmdlets and their permissions needed.</span></span>

    ```powershell
    #Requires -RunAsAdministrator
    Param (
        [Parameter(Mandatory = $true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory = $true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory = $true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory = $true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory = $true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory = $true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory = $false)]
        [string] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory = $false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory = $false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory = $false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory = $false)]
        [ValidateSet("AzureCloud", "AzureUSGovernment")]
        [string]$EnvironmentName = "AzureCloud",

        [Parameter(Mandatory = $false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
    )

    function CreateSelfSignedCertificate([string] $certificateName, [string] $selfSignedCertPlainPassword,
        [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired) -HashAlgorithm SHA256

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
    }

    function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $keyId = (New-Guid).Guid

        # Create an Azure AD application, AD App Credential, AD ServicePrincipal

        # Requires Application Developer Role, but works with Application administrator or GLOBAL ADMIN
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $keyId) 
        # Requires Application administrator or GLOBAL ADMIN
        $ApplicationCredential = New-AzureRmADAppCredential -ApplicationId $Application.ApplicationId -CertValue $keyValue -StartDate $PfxCert.NotBefore -EndDate $PfxCert.NotAfter
        # Requires Application administrator or GLOBAL ADMIN
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId 
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
        Sleep -s 15
        # Requires User Access Administrator or Owner.
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6) {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
        return $Application.ApplicationId.ToString();
    }

    function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName, [string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
    }

    function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
    }

    Import-Module AzureRM.Profile
    Import-Module AzureRM.Resources

    $AzureRMProfileVersion = (Get-Module AzureRM.Profile).Version
    if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 4) -or ($AzureRMProfileVersion.Major -gt 3))) {
        Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
        return
    }

    Connect-AzureRmAccount -Environment $EnvironmentName 
    $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

    # Create a Run As account by using a service principal
    $CertifcateAssetName = "AzureRunAsCertificate"
    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionTypeName = "AzureServicePrincipal"

    if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
    }
    else {
        $CertificateName = $AutomationAccountName + $CertifcateAssetName
        $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
        $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
        $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
        CreateSelfSignedCertificate $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
    }

    # Create a service principal
    $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
    $ApplicationId = CreateServicePrincipal $PfxCert $ApplicationDisplayName

    # Create the Automation certificate asset
    CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

    # Populate the ConnectionFieldValues
    $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
    $TenantID = $SubscriptionInfo | Select TenantId -First 1
    $Thumbprint = $PfxCert.Thumbprint
    $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

    # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
    CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

    if ($CreateClassicRunAsAccount) {
        # Create a Run As account by using a service principal
        $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
        $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
        $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
        $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
        "Log in to the Microsoft Azure portal (https://portal.azure.com) and select Subscriptions -> Management Certificates." + [Environment]::NewLine +
        "Then click Upload and upload the .cer format of #CERT#"

        if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
            $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
            $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
            $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        }
        else {
            $ClassicRunAsAccountCertificateName = $AutomationAccountName + $ClassicRunAsAccountCertifcateAssetName
            $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
            $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
            $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
            $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
            CreateSelfSignedCertificate $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName   $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red       $UploadMessage
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="08975-200">**Add-AzureRmAccount** is now an alias for **Connect-AzureRMAccount**.</span><span class="sxs-lookup"><span data-stu-id="08975-200">**Add-AzureRmAccount** is now an alias for **Connect-AzureRMAccount**.</span></span> <span data-ttu-id="08975-201">When searching your library items, if you do not see **Connect-AzureRMAccount**, you can use **Add-AzureRmAccount**, or you can [update your modules](automation-update-azure-modules.md) in your Automation Account.</span><span class="sxs-lookup"><span data-stu-id="08975-201">When searching your library items, if you do not see **Connect-AzureRMAccount**, you can use **Add-AzureRmAccount**, or you can [update your modules](automation-update-azure-modules.md) in your Automation Account.</span></span>

1. <span data-ttu-id="08975-202">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span><span class="sxs-lookup"><span data-stu-id="08975-202">On your computer, start **Windows PowerShell** from the **Start** screen with elevated user rights.</span></span>
1. <span data-ttu-id="08975-203">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span><span class="sxs-lookup"><span data-stu-id="08975-203">From the elevated command-line shell, go to the folder that contains the script you created in step 1.</span></span>  
1. <span data-ttu-id="08975-204">Execute the script by using the parameter values for the configuration you require.</span><span class="sxs-lookup"><span data-stu-id="08975-204">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="08975-205">**Create a Run As account by using a self-signed certificate**</span><span class="sxs-lookup"><span data-stu-id="08975-205">**Create a Run As account by using a self-signed certificate**</span></span>  

    ```powershell
    .\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false
    ```

    <span data-ttu-id="08975-206">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span><span class="sxs-lookup"><span data-stu-id="08975-206">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  

    ```powershell
    .\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true
    ```

    <span data-ttu-id="08975-207">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span><span class="sxs-lookup"><span data-stu-id="08975-207">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  

    ```powershell
    .\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>
    ```

    <span data-ttu-id="08975-208">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span><span class="sxs-lookup"><span data-stu-id="08975-208">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>
  
    ```powershell
    .\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment
    ```

    > [!NOTE]
    > <span data-ttu-id="08975-209">After the script has executed, you will be prompted to authenticate with Azure.</span><span class="sxs-lookup"><span data-stu-id="08975-209">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="08975-210">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span><span class="sxs-lookup"><span data-stu-id="08975-210">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

<span data-ttu-id="08975-211">After the script has executed successfully, note the following:</span><span class="sxs-lookup"><span data-stu-id="08975-211">After the script has executed successfully, note the following:</span></span>

* <span data-ttu-id="08975-212">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="08975-212">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>

* <span data-ttu-id="08975-213">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span><span class="sxs-lookup"><span data-stu-id="08975-213">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="08975-214">Follow the instructions for [uploading a management API certificate to the Azure portal](../azure-api-management-certs.md).(automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="08975-214">Follow the instructions for [uploading a management API certificate to the Azure portal](../azure-api-management-certs.md).(automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="08975-215">Delete a Run As or Classic Run As account</span><span class="sxs-lookup"><span data-stu-id="08975-215">Delete a Run As or Classic Run As account</span></span>

<span data-ttu-id="08975-216">This section describes how to delete and re-create a Run As or Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="08975-216">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="08975-217">When you perform this action, the Automation account is retained.</span><span class="sxs-lookup"><span data-stu-id="08975-217">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="08975-218">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="08975-218">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="08975-219">In the Azure portal, open the Automation account.</span><span class="sxs-lookup"><span data-stu-id="08975-219">In the Azure portal, open the Automation account.</span></span>

1. <span data-ttu-id="08975-220">On the **Automation account** page, select **Run As Accounts**.</span><span class="sxs-lookup"><span data-stu-id="08975-220">On the **Automation account** page, select **Run As Accounts**.</span></span>

1. <span data-ttu-id="08975-221">On the **Run As Accounts** properties page, select either the Run As account or Classic Run As account that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="08975-221">On the **Run As Accounts** properties page, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="08975-222">Then, on the **Properties** pane for the selected account, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="08975-222">Then, on the **Properties** pane for the selected account, click **Delete**.</span></span>

 ![Delete Run As account](media/manage-runas-account/automation-account-delete-runas.png)

1. <span data-ttu-id="08975-224">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="08975-224">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

1. <span data-ttu-id="08975-225">After the account has been deleted, you can re-create it on the **Run As Accounts** properties page by selecting the create option **Azure Run As Account**.</span><span class="sxs-lookup"><span data-stu-id="08975-225">After the account has been deleted, you can re-create it on the **Run As Accounts** properties page by selecting the create option **Azure Run As Account**.</span></span>

 ![Re-create the Automation Run As account](media/manage-runas-account/automation-account-create-runas.png)

## <a name="cert-renewal"></a><span data-ttu-id="08975-227">Self-signed certificate renewal</span><span class="sxs-lookup"><span data-stu-id="08975-227">Self-signed certificate renewal</span></span>

<span data-ttu-id="08975-228">At some point before your Run As account expires, you need to renew the certificate.</span><span class="sxs-lookup"><span data-stu-id="08975-228">At some point before your Run As account expires, you need to renew the certificate.</span></span> <span data-ttu-id="08975-229">If you believe that the Run As account has been compromised, you can delete and re-create it.</span><span class="sxs-lookup"><span data-stu-id="08975-229">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="08975-230">This section discusses how to perform these operations.</span><span class="sxs-lookup"><span data-stu-id="08975-230">This section discusses how to perform these operations.</span></span>

<span data-ttu-id="08975-231">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span><span class="sxs-lookup"><span data-stu-id="08975-231">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="08975-232">You can renew it at any time before it expires.</span><span class="sxs-lookup"><span data-stu-id="08975-232">You can renew it at any time before it expires.</span></span> <span data-ttu-id="08975-233">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span><span class="sxs-lookup"><span data-stu-id="08975-233">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="08975-234">The certificate remains valid until its expiration date.</span><span class="sxs-lookup"><span data-stu-id="08975-234">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="08975-235">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate is replaced by a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="08975-235">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate is replaced by a self-signed certificate.</span></span>

<span data-ttu-id="08975-236">To renew the certificate, do the following:</span><span class="sxs-lookup"><span data-stu-id="08975-236">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="08975-237">In the Azure portal, open the Automation account.</span><span class="sxs-lookup"><span data-stu-id="08975-237">In the Azure portal, open the Automation account.</span></span>

1. <span data-ttu-id="08975-238">Select **Run As Accounts** under **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="08975-238">Select **Run As Accounts** under **Account Settings**.</span></span>

    ![Automation account properties pane](media/manage-runas-account/automation-account-properties-pane.png)

1. <span data-ttu-id="08975-240">On the **Run As Accounts** properties page, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span><span class="sxs-lookup"><span data-stu-id="08975-240">On the **Run As Accounts** properties page, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

1. <span data-ttu-id="08975-241">On the **Properties** pane for the selected account, click **Renew certificate**.</span><span class="sxs-lookup"><span data-stu-id="08975-241">On the **Properties** pane for the selected account, click **Renew certificate**.</span></span>

    ![Renew certificate for Run As account](media/manage-runas-account/automation-account-renew-runas-certificate.png)

1. <span data-ttu-id="08975-243">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="08975-243">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

<span data-ttu-id="08975-244">If you are un-able to renew the Run As certificate</span><span class="sxs-lookup"><span data-stu-id="08975-244">If you are un-able to renew the Run As certificate</span></span>
## <a name="limiting-run-as-account-permissions"></a><span data-ttu-id="08975-245">Limiting Run As account permissions</span><span class="sxs-lookup"><span data-stu-id="08975-245">Limiting Run As account permissions</span></span>

<span data-ttu-id="08975-246">To control targeting of automation against resources in Azure Automation, the Run As account by default is granted contributor rights in the subscription.</span><span class="sxs-lookup"><span data-stu-id="08975-246">To control targeting of automation against resources in Azure Automation, the Run As account by default is granted contributor rights in the subscription.</span></span> <span data-ttu-id="08975-247">If you need to restrict what the RunAs service principal can do, you can remove the account from the contributor role to the subscription and add it as a contributor to the resource groups you want to specify.</span><span class="sxs-lookup"><span data-stu-id="08975-247">If you need to restrict what the RunAs service principal can do, you can remove the account from the contributor role to the subscription and add it as a contributor to the resource groups you want to specify.</span></span>

<span data-ttu-id="08975-248">In the Azure portal, select **Subscriptions** and choose the subscription of your Automation Account.</span><span class="sxs-lookup"><span data-stu-id="08975-248">In the Azure portal, select **Subscriptions** and choose the subscription of your Automation Account.</span></span> <span data-ttu-id="08975-249">Select **Access control (IAM)** and search for the service principal for your Automation Account (it looks like \<AutomationAccountName\>_unique identifier).</span><span class="sxs-lookup"><span data-stu-id="08975-249">Select **Access control (IAM)** and search for the service principal for your Automation Account (it looks like \<AutomationAccountName\>_unique identifier).</span></span> <span data-ttu-id="08975-250">Select the account and click **Remove** to remove it from the subscription.</span><span class="sxs-lookup"><span data-stu-id="08975-250">Select the account and click **Remove** to remove it from the subscription.</span></span>

![Subscription contributors](media/manage-runas-account/automation-account-remove-subscription.png)

<span data-ttu-id="08975-252">To add the service principal to a resource group, select the resource group in the Azure portal and select **Access control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="08975-252">To add the service principal to a resource group, select the resource group in the Azure portal and select **Access control (IAM)**.</span></span> <span data-ttu-id="08975-253">Select **Add**, this opens the **Add permissions** page.</span><span class="sxs-lookup"><span data-stu-id="08975-253">Select **Add**, this opens the **Add permissions** page.</span></span> <span data-ttu-id="08975-254">For **Role**, select **Contributor**.</span><span class="sxs-lookup"><span data-stu-id="08975-254">For **Role**, select **Contributor**.</span></span> <span data-ttu-id="08975-255">In the **Select** text box type in the name of the service principal for your Run As account, and select it from the list.</span><span class="sxs-lookup"><span data-stu-id="08975-255">In the **Select** text box type in the name of the service principal for your Run As account, and select it from the list.</span></span> <span data-ttu-id="08975-256">Click **Save** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="08975-256">Click **Save** to save the changes.</span></span> <span data-ttu-id="08975-257">Do this for the resources groups you want to give your Azure Automation Run As service principal access to.</span><span class="sxs-lookup"><span data-stu-id="08975-257">Do this for the resources groups you want to give your Azure Automation Run As service principal access to.</span></span>

## <a name="misconfiguration"></a><span data-ttu-id="08975-258">Misconfiguration</span><span class="sxs-lookup"><span data-stu-id="08975-258">Misconfiguration</span></span>

<span data-ttu-id="08975-259">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span><span class="sxs-lookup"><span data-stu-id="08975-259">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="08975-260">The items include:</span><span class="sxs-lookup"><span data-stu-id="08975-260">The items include:</span></span>

* <span data-ttu-id="08975-261">Certificate asset</span><span class="sxs-lookup"><span data-stu-id="08975-261">Certificate asset</span></span>
* <span data-ttu-id="08975-262">Connection asset</span><span class="sxs-lookup"><span data-stu-id="08975-262">Connection asset</span></span>
* <span data-ttu-id="08975-263">Run As account has been removed from the contributor role</span><span class="sxs-lookup"><span data-stu-id="08975-263">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="08975-264">Service principal or application in Azure AD</span><span class="sxs-lookup"><span data-stu-id="08975-264">Service principal or application in Azure AD</span></span>

<span data-ttu-id="08975-265">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties pane for the account.</span><span class="sxs-lookup"><span data-stu-id="08975-265">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties pane for the account.</span></span>

![Incomplete Run As account configuration status](media/manage-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="08975-267">When you select the Run As account, the account **Properties** pane displays the following error message:</span><span class="sxs-lookup"><span data-stu-id="08975-267">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

```text
The Run As account is incomplete. Either one of these was deleted or not created - Azure Active Directory Application, Service Principal, Role, Automation Certificate asset, Automation Connect asset - or the Thumbprint is not identical between Certificate and Connection. Please delete and then re-create the Run As Account.
```

<span data-ttu-id="08975-268">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span><span class="sxs-lookup"><span data-stu-id="08975-268">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08975-269">Next steps</span><span class="sxs-lookup"><span data-stu-id="08975-269">Next steps</span></span>

* <span data-ttu-id="08975-270">For more information about Service Principals, see [Application Objects and Service Principal Objects](../active-directory/develop/app-objects-and-service-principals.md).</span><span class="sxs-lookup"><span data-stu-id="08975-270">For more information about Service Principals, see [Application Objects and Service Principal Objects](../active-directory/develop/app-objects-and-service-principals.md).</span></span>
* <span data-ttu-id="08975-271">For more information about certificates and Azure services, see [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="08975-271">For more information about certificates and Azure services, see [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
