---
title: Configure an Azure Run As Account | Microsoft Docs
description: This tutorial walks you through the creation, testing, and example use of security-principal authentication in Azure Automation.
services: automation
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
keywords: service principal name, setspn, azure authentication
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ms.openlocfilehash: 86b127245c494f491fdc948f22f473081f460623
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549422"
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="ff894-104">Authenticate runbooks with an Azure Run As account</span><span class="sxs-lookup"><span data-stu-id="ff894-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="ff894-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff894-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="ff894-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="ff894-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="ff894-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span><span class="sxs-lookup"><span data-stu-id="ff894-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="ff894-108">A Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-108">A Run As account.</span></span> <span data-ttu-id="ff894-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="ff894-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="ff894-111">A Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-111">A Classic Run As account.</span></span> <span data-ttu-id="ff894-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="ff894-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span><span class="sxs-lookup"><span data-stu-id="ff894-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="ff894-114">With Run As and Classic Run As accounts, you can:</span><span class="sxs-lookup"><span data-stu-id="ff894-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="ff894-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff894-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="ff894-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="ff894-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="ff894-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="ff894-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="ff894-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="ff894-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span><span class="sxs-lookup"><span data-stu-id="ff894-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="ff894-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="ff894-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="ff894-122">The process works only for Automation accounts that you create in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff894-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="ff894-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span><span class="sxs-lookup"><span data-stu-id="ff894-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="ff894-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span><span class="sxs-lookup"><span data-stu-id="ff894-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="ff894-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span><span class="sxs-lookup"><span data-stu-id="ff894-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="ff894-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span><span class="sxs-lookup"><span data-stu-id="ff894-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="ff894-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="ff894-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="ff894-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span><span class="sxs-lookup"><span data-stu-id="ff894-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="ff894-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="ff894-130">Create an Automation account from the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ff894-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="ff894-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="ff894-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span><span class="sxs-lookup"><span data-stu-id="ff894-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="ff894-133">You must also be added as a user to that subscription's default Active Directory instance.</span><span class="sxs-lookup"><span data-stu-id="ff894-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="ff894-134">The account does not need to be assigned a privileged role.</span><span class="sxs-lookup"><span data-stu-id="ff894-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="ff894-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span><span class="sxs-lookup"><span data-stu-id="ff894-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="ff894-136">In this instance, you will receive a “You do not have permissions to create…”</span><span class="sxs-lookup"><span data-stu-id="ff894-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="ff894-137">warning on the **Add Automation Account** blade.</span><span class="sxs-lookup"><span data-stu-id="ff894-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="ff894-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ff894-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="ff894-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span><span class="sxs-lookup"><span data-stu-id="ff894-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="ff894-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span><span class="sxs-lookup"><span data-stu-id="ff894-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="ff894-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span><span class="sxs-lookup"><span data-stu-id="ff894-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="ff894-142">Select **Automation Accounts**.</span><span class="sxs-lookup"><span data-stu-id="ff894-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="ff894-143">On the **Automation Accounts** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ff894-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="ff894-144">The **Add Automation Account** blade opens.</span><span class="sxs-lookup"><span data-stu-id="ff894-144">The **Add Automation Account** blade opens.</span></span>

 ![The "Add Automation Account" blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="ff894-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span><span class="sxs-lookup"><span data-stu-id="ff894-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![Add Automation Account Warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="ff894-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="ff894-149">If you have more than one subscription, do the following:</span><span class="sxs-lookup"><span data-stu-id="ff894-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="ff894-150">a.</span><span class="sxs-lookup"><span data-stu-id="ff894-150">a.</span></span> <span data-ttu-id="ff894-151">Under **Subscription**, specify one for the new account.</span><span class="sxs-lookup"><span data-stu-id="ff894-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="ff894-152">b.</span><span class="sxs-lookup"><span data-stu-id="ff894-152">b.</span></span> <span data-ttu-id="ff894-153">Under **Resource Group**, click **Create new** or **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="ff894-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="ff894-154">c.</span><span class="sxs-lookup"><span data-stu-id="ff894-154">c.</span></span> <span data-ttu-id="ff894-155">Under **Location**, specify an Azure datacenter.</span><span class="sxs-lookup"><span data-stu-id="ff894-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="ff894-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff894-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ff894-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span><span class="sxs-lookup"><span data-stu-id="ff894-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="ff894-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span><span class="sxs-lookup"><span data-stu-id="ff894-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="ff894-159">Consequently, the account has no access to resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="ff894-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="ff894-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span><span class="sxs-lookup"><span data-stu-id="ff894-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Warning message on the "Add Automation Account" blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="ff894-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span><span class="sxs-lookup"><span data-stu-id="ff894-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="ff894-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="ff894-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="ff894-164">Resources</span><span class="sxs-lookup"><span data-stu-id="ff894-164">Resources</span></span>
<span data-ttu-id="ff894-165">When the Automation account is successfully created, several resources are automatically created for you.</span><span class="sxs-lookup"><span data-stu-id="ff894-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="ff894-166">The resources are summarized in the following two tables:</span><span class="sxs-lookup"><span data-stu-id="ff894-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="ff894-167">Run As account resources</span><span class="sxs-lookup"><span data-stu-id="ff894-167">Run As account resources</span></span>

| <span data-ttu-id="ff894-168">Resource</span><span class="sxs-lookup"><span data-stu-id="ff894-168">Resource</span></span> | <span data-ttu-id="ff894-169">Description</span><span class="sxs-lookup"><span data-stu-id="ff894-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff894-170">AzureAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="ff894-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="ff894-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="ff894-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="ff894-172">AzureAutomationTutorialScript Runbook</span><span class="sxs-lookup"><span data-stu-id="ff894-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="ff894-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="ff894-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="ff894-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="ff894-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="ff894-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span><span class="sxs-lookup"><span data-stu-id="ff894-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="ff894-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="ff894-177">The certificate has a one-year lifespan.</span><span class="sxs-lookup"><span data-stu-id="ff894-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="ff894-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="ff894-178">AzureRunAsConnection</span></span> | <span data-ttu-id="ff894-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span><span class="sxs-lookup"><span data-stu-id="ff894-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="ff894-180">Classic Run As account resources</span><span class="sxs-lookup"><span data-stu-id="ff894-180">Classic Run As account resources</span></span>

| <span data-ttu-id="ff894-181">Resource</span><span class="sxs-lookup"><span data-stu-id="ff894-181">Resource</span></span> | <span data-ttu-id="ff894-182">Description</span><span class="sxs-lookup"><span data-stu-id="ff894-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ff894-183">AzureClassicAutomationTutorial Runbook</span><span class="sxs-lookup"><span data-stu-id="ff894-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="ff894-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span><span class="sxs-lookup"><span data-stu-id="ff894-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="ff894-185">AzureClassicAutomationTutorial Script Runbook</span><span class="sxs-lookup"><span data-stu-id="ff894-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="ff894-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span><span class="sxs-lookup"><span data-stu-id="ff894-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="ff894-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="ff894-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="ff894-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="ff894-189">The certificate has a one-year lifespan.</span><span class="sxs-lookup"><span data-stu-id="ff894-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="ff894-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="ff894-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="ff894-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="ff894-192">Verify Run As authentication</span><span class="sxs-lookup"><span data-stu-id="ff894-192">Verify Run As authentication</span></span>
<span data-ttu-id="ff894-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="ff894-194">In the Azure portal, open the Automation account that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ff894-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="ff894-195">Click the **Runbooks** tile to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="ff894-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span><span class="sxs-lookup"><span data-stu-id="ff894-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="ff894-197">The following events occur:</span><span class="sxs-lookup"><span data-stu-id="ff894-197">The following events occur:</span></span>
 * <span data-ttu-id="ff894-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span><span class="sxs-lookup"><span data-stu-id="ff894-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="ff894-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span><span class="sxs-lookup"><span data-stu-id="ff894-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="ff894-200">The status becomes **Starting** when a worker claims the job.</span><span class="sxs-lookup"><span data-stu-id="ff894-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="ff894-201">The status becomes **Running** when the runbook starts running.</span><span class="sxs-lookup"><span data-stu-id="ff894-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="ff894-202">When the runbook job has finished running, you should see a status of **Completed**.</span><span class="sxs-lookup"><span data-stu-id="ff894-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="ff894-203">To see the detailed results of the runbook, click the **Output** tile.</span><span class="sxs-lookup"><span data-stu-id="ff894-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="ff894-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span><span class="sxs-lookup"><span data-stu-id="ff894-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="ff894-205">Close the **Output** blade to return to the **Job Summary** blade.</span><span class="sxs-lookup"><span data-stu-id="ff894-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="ff894-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span><span class="sxs-lookup"><span data-stu-id="ff894-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="ff894-207">Verify Classic Run As authentication</span><span class="sxs-lookup"><span data-stu-id="ff894-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="ff894-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="ff894-209">In the Azure portal, open the Automation account that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="ff894-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="ff894-210">Click the **Runbooks** tile to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="ff894-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span><span class="sxs-lookup"><span data-stu-id="ff894-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="ff894-212">The following events occur:</span><span class="sxs-lookup"><span data-stu-id="ff894-212">The following events occur:</span></span>

 * <span data-ttu-id="ff894-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span><span class="sxs-lookup"><span data-stu-id="ff894-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="ff894-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span><span class="sxs-lookup"><span data-stu-id="ff894-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="ff894-215">The status becomes **Starting** when a worker claims the job.</span><span class="sxs-lookup"><span data-stu-id="ff894-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="ff894-216">The status becomes **Running** when the runbook starts running.</span><span class="sxs-lookup"><span data-stu-id="ff894-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="ff894-217">When the runbook job has finished running, you should see a status of **Completed**.</span><span class="sxs-lookup"><span data-stu-id="ff894-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Security Principal Runbook Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="ff894-219">To see the detailed results of the runbook, click the **Output** tile.</span><span class="sxs-lookup"><span data-stu-id="ff894-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="ff894-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span><span class="sxs-lookup"><span data-stu-id="ff894-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="ff894-221">Close the **Output** blade to return to the **Job Summary** blade.</span><span class="sxs-lookup"><span data-stu-id="ff894-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="ff894-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span><span class="sxs-lookup"><span data-stu-id="ff894-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="ff894-223">Managing your Run As account</span><span class="sxs-lookup"><span data-stu-id="ff894-223">Managing your Run As account</span></span>
<span data-ttu-id="ff894-224">At some point before your Automation account expires, you will need to renew the certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="ff894-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span><span class="sxs-lookup"><span data-stu-id="ff894-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="ff894-226">This section discusses how to perform these operations.</span><span class="sxs-lookup"><span data-stu-id="ff894-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="ff894-227">Self-signed certificate renewal</span><span class="sxs-lookup"><span data-stu-id="ff894-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="ff894-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span><span class="sxs-lookup"><span data-stu-id="ff894-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="ff894-229">You can renew it at any time before it expires.</span><span class="sxs-lookup"><span data-stu-id="ff894-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="ff894-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span><span class="sxs-lookup"><span data-stu-id="ff894-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="ff894-231">The certificate remains valid until its expiration date.</span><span class="sxs-lookup"><span data-stu-id="ff894-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="ff894-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="ff894-233">To renew the certificate, do the following:</span><span class="sxs-lookup"><span data-stu-id="ff894-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="ff894-234">In the Azure portal, open the Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="ff894-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span><span class="sxs-lookup"><span data-stu-id="ff894-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Automation account properties pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="ff894-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span><span class="sxs-lookup"><span data-stu-id="ff894-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="ff894-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span><span class="sxs-lookup"><span data-stu-id="ff894-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Renew certificate for Run As account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="ff894-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="ff894-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="ff894-241">Delete a Run As or Classic Run As account</span><span class="sxs-lookup"><span data-stu-id="ff894-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="ff894-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="ff894-243">When you perform this action, the Automation account is retained.</span><span class="sxs-lookup"><span data-stu-id="ff894-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="ff894-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ff894-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="ff894-245">In the Azure portal, open the Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="ff894-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span><span class="sxs-lookup"><span data-stu-id="ff894-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="ff894-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="ff894-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="ff894-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ff894-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Delete Run As account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="ff894-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span><span class="sxs-lookup"><span data-stu-id="ff894-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="ff894-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span><span class="sxs-lookup"><span data-stu-id="ff894-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Re-create the Automation Run As account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="ff894-253">Misconfiguration</span><span class="sxs-lookup"><span data-stu-id="ff894-253">Misconfiguration</span></span>
<span data-ttu-id="ff894-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span><span class="sxs-lookup"><span data-stu-id="ff894-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="ff894-255">The items include:</span><span class="sxs-lookup"><span data-stu-id="ff894-255">The items include:</span></span>

* <span data-ttu-id="ff894-256">Certificate asset</span><span class="sxs-lookup"><span data-stu-id="ff894-256">Certificate asset</span></span>
* <span data-ttu-id="ff894-257">Connection asset</span><span class="sxs-lookup"><span data-stu-id="ff894-257">Connection asset</span></span>
* <span data-ttu-id="ff894-258">Run As account has been removed from the contributor role</span><span class="sxs-lookup"><span data-stu-id="ff894-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="ff894-259">Service principal or application in Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff894-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="ff894-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span><span class="sxs-lookup"><span data-stu-id="ff894-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Incomplete Run As account configuration status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="ff894-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span><span class="sxs-lookup"><span data-stu-id="ff894-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Incomplete Run As configuration warning message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="ff894-264">.</span><span class="sxs-lookup"><span data-stu-id="ff894-264">.</span></span>

<span data-ttu-id="ff894-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span><span class="sxs-lookup"><span data-stu-id="ff894-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="ff894-266">Update your Automation account by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff894-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="ff894-267">You can use PowerShell to update your existing Automation account if:</span><span class="sxs-lookup"><span data-stu-id="ff894-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="ff894-268">You create an Automation account but decline to create the Run As account.</span><span class="sxs-lookup"><span data-stu-id="ff894-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="ff894-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span><span class="sxs-lookup"><span data-stu-id="ff894-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="ff894-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span><span class="sxs-lookup"><span data-stu-id="ff894-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="ff894-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span><span class="sxs-lookup"><span data-stu-id="ff894-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="ff894-272">The script has the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="ff894-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="ff894-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span><span class="sxs-lookup"><span data-stu-id="ff894-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="ff894-274">It is not supported on earlier versions of Windows.</span><span class="sxs-lookup"><span data-stu-id="ff894-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="ff894-275">Azure PowerShell 1.0 and later.</span><span class="sxs-lookup"><span data-stu-id="ff894-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="ff894-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="ff894-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="ff894-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="ff894-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="ff894-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span><span class="sxs-lookup"><span data-stu-id="ff894-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="ff894-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span><span class="sxs-lookup"><span data-stu-id="ff894-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="ff894-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ff894-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="ff894-281">Note the values on the **Properties** blade.</span><span class="sxs-lookup"><span data-stu-id="ff894-281">Note the values on the **Properties** blade.</span></span>

![The Automation account "Properties" blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="ff894-283">Create a Run As account PowerShell script</span><span class="sxs-lookup"><span data-stu-id="ff894-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="ff894-284">This PowerShell script includes support for the following configurations:</span><span class="sxs-lookup"><span data-stu-id="ff894-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="ff894-285">Create a Run As account by using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ff894-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="ff894-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="ff894-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span><span class="sxs-lookup"><span data-stu-id="ff894-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="ff894-289">Depending on the configuration option you select, the script creates the following items.</span><span class="sxs-lookup"><span data-stu-id="ff894-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="ff894-290">**For Run As accounts:**</span><span class="sxs-lookup"><span data-stu-id="ff894-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="ff894-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span><span class="sxs-lookup"><span data-stu-id="ff894-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="ff894-292">You can change this setting to Owner or any other role.</span><span class="sxs-lookup"><span data-stu-id="ff894-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="ff894-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="ff894-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="ff894-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="ff894-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="ff894-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="ff894-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="ff894-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span><span class="sxs-lookup"><span data-stu-id="ff894-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="ff894-298">**For Classic Run As accounts:**</span><span class="sxs-lookup"><span data-stu-id="ff894-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="ff894-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="ff894-300">The certificate asset holds the certificate private key used by the management certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="ff894-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span><span class="sxs-lookup"><span data-stu-id="ff894-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="ff894-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span><span class="sxs-lookup"><span data-stu-id="ff894-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="ff894-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span><span class="sxs-lookup"><span data-stu-id="ff894-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="ff894-304">To execute the script and upload the certificate, do the following:</span><span class="sxs-lookup"><span data-stu-id="ff894-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="ff894-305">Save the following script on your computer.</span><span class="sxs-lookup"><span data-stu-id="ff894-305">Save the following script on your computer.</span></span> <span data-ttu-id="ff894-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="ff894-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
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

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

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
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="ff894-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span><span class="sxs-lookup"><span data-stu-id="ff894-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="ff894-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span><span class="sxs-lookup"><span data-stu-id="ff894-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="ff894-309">Execute the script by using the parameter values for the configuration you require.</span><span class="sxs-lookup"><span data-stu-id="ff894-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="ff894-310">**Create a Run As account by using a self-signed certificate**</span><span class="sxs-lookup"><span data-stu-id="ff894-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="ff894-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span><span class="sxs-lookup"><span data-stu-id="ff894-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="ff894-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span><span class="sxs-lookup"><span data-stu-id="ff894-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="ff894-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span><span class="sxs-lookup"><span data-stu-id="ff894-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="ff894-314">After the script has executed, you will be prompted to authenticate with Azure.</span><span class="sxs-lookup"><span data-stu-id="ff894-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="ff894-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span><span class="sxs-lookup"><span data-stu-id="ff894-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="ff894-316">After the script has executed successfully, note the following:</span><span class="sxs-lookup"><span data-stu-id="ff894-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="ff894-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="ff894-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="ff894-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span><span class="sxs-lookup"><span data-stu-id="ff894-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="ff894-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="ff894-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="ff894-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="ff894-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="ff894-321">Sample code to authenticate with Resource Manager resources</span><span class="sxs-lookup"><span data-stu-id="ff894-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="ff894-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="ff894-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span><span class="sxs-lookup"><span data-stu-id="ff894-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="ff894-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span><span class="sxs-lookup"><span data-stu-id="ff894-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="ff894-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](https://msdn.microsoft.com/library/mt619263.aspx) cmdlet is stated with the parameter set *-SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="ff894-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](https://msdn.microsoft.com/library/mt619263.aspx) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="ff894-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span><span class="sxs-lookup"><span data-stu-id="ff894-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="ff894-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span><span class="sxs-lookup"><span data-stu-id="ff894-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="ff894-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span><span class="sxs-lookup"><span data-stu-id="ff894-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="ff894-329">It authenticates by using the service principal certificate, not the user credentials.</span><span class="sxs-lookup"><span data-stu-id="ff894-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="ff894-330">Sample code to authenticate with Service Management resources</span><span class="sxs-lookup"><span data-stu-id="ff894-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="ff894-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span><span class="sxs-lookup"><span data-stu-id="ff894-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="ff894-332">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff894-332">Next steps</span></span>
* [<span data-ttu-id="ff894-333">Application and service principal objects in Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff894-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="ff894-334">Role-based access control in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="ff894-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="ff894-335">Certificates overview for Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ff894-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)












