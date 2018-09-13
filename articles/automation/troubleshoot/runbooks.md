---
title: Troubleshoot errors with Azure Automation Runbooks
description: Learn how to troubleshoot issues with Azure Automation runbooks
services: automation
author: georgewallace
ms.author: gwallace
ms.date: 07/13/2018
ms.topic: conceptual
ms.service: automation
manager: carmonm
ms.openlocfilehash: 78f9ba817008a28e63ec167c4e2ccc7f3859be16
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856508"
---
# <a name="troubleshoot-errors-with-runbooks"></a><span data-ttu-id="103e5-103">Troubleshoot errors with runbooks</span><span class="sxs-lookup"><span data-stu-id="103e5-103">Troubleshoot errors with runbooks</span></span>

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a><span data-ttu-id="103e5-104">Authentication errors when working with Azure Automation runbooks</span><span class="sxs-lookup"><span data-stu-id="103e5-104">Authentication errors when working with Azure Automation runbooks</span></span>

### <a name="sign-in-failed"></a><span data-ttu-id="103e5-105">Scenario: Sign in to Azure Account failed</span><span class="sxs-lookup"><span data-stu-id="103e5-105">Scenario: Sign in to Azure Account failed</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-106">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-106">Issue</span></span>

<span data-ttu-id="103e5-107">You receive the following error when working with the `Add-AzureAccount` or `Connect-AzureRmAccount` cmdlets.</span><span class="sxs-lookup"><span data-stu-id="103e5-107">You receive the following error when working with the `Add-AzureAccount` or `Connect-AzureRmAccount` cmdlets.</span></span>
<span data-ttu-id="103e5-108">:</span><span class="sxs-lookup"><span data-stu-id="103e5-108">:</span></span>

```
Unknown_user_type: Unknown User Type
```

#### <a name="cause"></a><span data-ttu-id="103e5-109">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-109">Cause</span></span>

<span data-ttu-id="103e5-110">This error occurs if the credential asset name is not valid or if the username and password that you used to set up the Automation credential asset are not valid.</span><span class="sxs-lookup"><span data-stu-id="103e5-110">This error occurs if the credential asset name is not valid or if the username and password that you used to set up the Automation credential asset are not valid.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-111">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-111">Resolution</span></span>

<span data-ttu-id="103e5-112">In order to determine what's wrong, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="103e5-112">In order to determine what's wrong, take the following steps:</span></span>  

1. <span data-ttu-id="103e5-113">Make sure that you don’t have any special characters, including the **@** character in the Automation credential asset name that you are using to connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="103e5-113">Make sure that you don’t have any special characters, including the **@** character in the Automation credential asset name that you are using to connect to Azure.</span></span>  
2. <span data-ttu-id="103e5-114">Check that you can use the username and password that are stored in the Azure Automation credential in your local PowerShell ISE editor.</span><span class="sxs-lookup"><span data-stu-id="103e5-114">Check that you can use the username and password that are stored in the Azure Automation credential in your local PowerShell ISE editor.</span></span> <span data-ttu-id="103e5-115">You can do this by running the following cmdlets in the PowerShell ISE:</span><span class="sxs-lookup"><span data-stu-id="103e5-115">You can do this by running the following cmdlets in the PowerShell ISE:</span></span>  

   ```powershell
   $Cred = Get-Credential  
   #Using Azure Service Management
   Add-AzureAccount –Credential $Cred  
   #Using Azure Resource Manager  
   Connect-AzureRmAccount –Credential $Cred
   ```

3. <span data-ttu-id="103e5-116">If your authentication fails locally, this means that you haven’t set up your Azure Active Directory credentials properly.</span><span class="sxs-lookup"><span data-stu-id="103e5-116">If your authentication fails locally, this means that you haven’t set up your Azure Active Directory credentials properly.</span></span> <span data-ttu-id="103e5-117">Refer to [Authenticating to Azure using Azure Active Directory](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) blog post to get the Azure Active Directory account set up correctly.</span><span class="sxs-lookup"><span data-stu-id="103e5-117">Refer to [Authenticating to Azure using Azure Active Directory](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) blog post to get the Azure Active Directory account set up correctly.</span></span>  

4. <span data-ttu-id="103e5-118">If it appears to be a transient error, try adding retry logic to your authentication routine to make authenticating more robust.</span><span class="sxs-lookup"><span data-stu-id="103e5-118">If it appears to be a transient error, try adding retry logic to your authentication routine to make authenticating more robust.</span></span>

   ```powershell
   # Get the connection "AzureRunAsConnection"
   $connectionName = "AzureRunAsConnection"
   $servicePrincipalConnection = Get-AutomationConnection -Name $connectionName

   $logonAttempt = 0
   $logonResult = $False

   while(!($connectionResult) -And ($logonAttempt -le 10))
   {
   $LogonAttempt++
   # Logging in to Azure...
   $connectionResult = Connect-AzureRmAccount `
      -ServicePrincipal `
      -TenantId $servicePrincipalConnection.TenantId `
      -ApplicationId $servicePrincipalConnection.ApplicationId `
      -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint

   Start-Sleep -Seconds 30
   }
   ```

### <a name="unable-to-find-subscription"></a><span data-ttu-id="103e5-119">Scenario: Unable to find the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="103e5-119">Scenario: Unable to find the Azure subscription</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-120">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-120">Issue</span></span>

<span data-ttu-id="103e5-121">You receive the following error when working with the `Select-AzureSubscription` or `Select-AzureRmSubscription` cmdlets.:</span><span class="sxs-lookup"><span data-stu-id="103e5-121">You receive the following error when working with the `Select-AzureSubscription` or `Select-AzureRmSubscription` cmdlets.:</span></span>

```
The subscription named <subscription name> cannot be found.
```

#### <a name="error"></a><span data-ttu-id="103e5-122">Error</span><span class="sxs-lookup"><span data-stu-id="103e5-122">Error</span></span>

<span data-ttu-id="103e5-123">This error occurs if the subscription name is not valid or if the Azure Active Directory user who is trying to get the subscription details is not configured as an admin of the subscription.</span><span class="sxs-lookup"><span data-stu-id="103e5-123">This error occurs if the subscription name is not valid or if the Azure Active Directory user who is trying to get the subscription details is not configured as an admin of the subscription.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-124">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-124">Resolution</span></span>

<span data-ttu-id="103e5-125">In order to determine if you have properly authenticated to Azure and have access to the subscription you are trying to select, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="103e5-125">In order to determine if you have properly authenticated to Azure and have access to the subscription you are trying to select, take the following steps:</span></span>  

1. <span data-ttu-id="103e5-126">Make sure that you run the **Add-AzureAccount** before running the **Select-AzureSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="103e5-126">Make sure that you run the **Add-AzureAccount** before running the **Select-AzureSubscription** cmdlet.</span></span>  
2. <span data-ttu-id="103e5-127">If you still see this error message, modify your code by adding the **Get-AzureSubscription** cmdlet following the **Add-AzureAccount** cmdlet and then execute the code.</span><span class="sxs-lookup"><span data-stu-id="103e5-127">If you still see this error message, modify your code by adding the **Get-AzureSubscription** cmdlet following the **Add-AzureAccount** cmdlet and then execute the code.</span></span> <span data-ttu-id="103e5-128">Now verify if the output of Get-AzureSubscription contains your subscription details.</span><span class="sxs-lookup"><span data-stu-id="103e5-128">Now verify if the output of Get-AzureSubscription contains your subscription details.</span></span>  

   * <span data-ttu-id="103e5-129">If you don't see any subscription details in the output, this means that the subscription isn’t initialized yet.</span><span class="sxs-lookup"><span data-stu-id="103e5-129">If you don't see any subscription details in the output, this means that the subscription isn’t initialized yet.</span></span>  
   * <span data-ttu-id="103e5-130">If you do see the subscription details in the output, confirm that you are using the correct subscription name or ID with the **Select-AzureSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="103e5-130">If you do see the subscription details in the output, confirm that you are using the correct subscription name or ID with the **Select-AzureSubscription** cmdlet.</span></span>

### <a name="auth-failed-mfa"></a><span data-ttu-id="103e5-131">Scenario: Authentication to Azure failed because multi-factor authentication is enabled</span><span class="sxs-lookup"><span data-stu-id="103e5-131">Scenario: Authentication to Azure failed because multi-factor authentication is enabled</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-132">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-132">Issue</span></span>

<span data-ttu-id="103e5-133">You receive the following error when authenticating to Azure with your Azure username and password:</span><span class="sxs-lookup"><span data-stu-id="103e5-133">You receive the following error when authenticating to Azure with your Azure username and password:</span></span>

```
Add-AzureAccount: AADSTS50079: Strong authentication enrollment (proof-up) is required
```

#### <a name="cause"></a><span data-ttu-id="103e5-134">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-134">Cause</span></span>

<span data-ttu-id="103e5-135">If you have multi-factor authentication on your Azure account, you can't use an Azure Active Directory user to authenticate to Azure.</span><span class="sxs-lookup"><span data-stu-id="103e5-135">If you have multi-factor authentication on your Azure account, you can't use an Azure Active Directory user to authenticate to Azure.</span></span> <span data-ttu-id="103e5-136">Instead, you need to use a certificate or a service principal to authenticate to Azure.</span><span class="sxs-lookup"><span data-stu-id="103e5-136">Instead, you need to use a certificate or a service principal to authenticate to Azure.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-137">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-137">Resolution</span></span>

<span data-ttu-id="103e5-138">To use a certificate with the Azure classic deployment model cmdlets, refer to [creating and adding a certificate to manage Azure services.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx)</span><span class="sxs-lookup"><span data-stu-id="103e5-138">To use a certificate with the Azure classic deployment model cmdlets, refer to [creating and adding a certificate to manage Azure services.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx)</span></span> <span data-ttu-id="103e5-139">To use a service principal with Azure Resource Manager cmdlets, refer to [creating service principal using Azure portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md) and [authenticating a service principal with Azure Resource Manager.](../../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="103e5-139">To use a service principal with Azure Resource Manager cmdlets, refer to [creating service principal using Azure portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md) and [authenticating a service principal with Azure Resource Manager.](../../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>

## <a name="common-errors-when-working-with-runbooks"></a><span data-ttu-id="103e5-140">Common errors when working with runbooks</span><span class="sxs-lookup"><span data-stu-id="103e5-140">Common errors when working with runbooks</span></span>

### <a name="task-was-cancelled"></a><span data-ttu-id="103e5-141">Scenario: The runbook fails with the error: A task was canceled</span><span class="sxs-lookup"><span data-stu-id="103e5-141">Scenario: The runbook fails with the error: A task was canceled</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-142">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-142">Issue</span></span>

<span data-ttu-id="103e5-143">Your runbook fails with an error similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="103e5-143">Your runbook fails with an error similar to the following example:</span></span>

```
Exception: A task was canceled.
```

#### <a name="cause"></a><span data-ttu-id="103e5-144">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-144">Cause</span></span>

<span data-ttu-id="103e5-145">This error can be caused by using outdated Azure modules.</span><span class="sxs-lookup"><span data-stu-id="103e5-145">This error can be caused by using outdated Azure modules.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-146">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-146">Resolution</span></span>

<span data-ttu-id="103e5-147">This error can be resolved by updating your Azure modules to the latest version.</span><span class="sxs-lookup"><span data-stu-id="103e5-147">This error can be resolved by updating your Azure modules to the latest version.</span></span>

<span data-ttu-id="103e5-148">In your Automation Account, click **Modules**, and click **Update Azure modules**.</span><span class="sxs-lookup"><span data-stu-id="103e5-148">In your Automation Account, click **Modules**, and click **Update Azure modules**.</span></span> <span data-ttu-id="103e5-149">The update takes roughly 15 minutes, once complete re-run the runbook that was failing.</span><span class="sxs-lookup"><span data-stu-id="103e5-149">The update takes roughly 15 minutes, once complete re-run the runbook that was failing.</span></span> <span data-ttu-id="103e5-150">To learn more about updating your modules, see [Update Azure modules in Azure Automation](../automation-update-azure-modules.md).</span><span class="sxs-lookup"><span data-stu-id="103e5-150">To learn more about updating your modules, see [Update Azure modules in Azure Automation](../automation-update-azure-modules.md).</span></span>

### <a name="child-runbook-auth-failure"></a><span data-ttu-id="103e5-151">Scenario: Child runbook fails when dealing with multiple subscriptions</span><span class="sxs-lookup"><span data-stu-id="103e5-151">Scenario: Child runbook fails when dealing with multiple subscriptions</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-152">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-152">Issue</span></span>

<span data-ttu-id="103e5-153">When executing child runbooks with `Start-AzureRmRunbook`, the child runbook fails to manage Azure resources.</span><span class="sxs-lookup"><span data-stu-id="103e5-153">When executing child runbooks with `Start-AzureRmRunbook`, the child runbook fails to manage Azure resources.</span></span>

#### <a name="cause"></a><span data-ttu-id="103e5-154">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-154">Cause</span></span>

<span data-ttu-id="103e5-155">The child runbook is not using the correct context when running.</span><span class="sxs-lookup"><span data-stu-id="103e5-155">The child runbook is not using the correct context when running.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-156">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-156">Resolution</span></span>

<span data-ttu-id="103e5-157">When working with multiple subscriptions the subscription context might be lost when invoking child runbooks.</span><span class="sxs-lookup"><span data-stu-id="103e5-157">When working with multiple subscriptions the subscription context might be lost when invoking child runbooks.</span></span> <span data-ttu-id="103e5-158">To ensure that the subscription context is passed to the child runbooks, add the `DefaultProfile` parameter to the cmdlet and pass the context to it.</span><span class="sxs-lookup"><span data-stu-id="103e5-158">To ensure that the subscription context is passed to the child runbooks, add the `DefaultProfile` parameter to the cmdlet and pass the context to it.</span></span>

```azurepowershell-interactive
# Connect to Azure with RunAs account
$ServicePrincipalConnection = Get-AutomationConnection -Name 'AzureRunAsConnection'

Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint

$AzureContext = Select-AzureRmSubscription -SubscriptionId $ServicePrincipalConnection.SubscriptionID

$params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true}

Start-AzureRmAutomationRunbook `
    –AutomationAccountName 'MyAutomationAccount' `
    –Name 'Test-ChildRunbook' `
    -ResourceGroupName 'LabRG' `
    -DefaultProfile $AzureContext `
    –Parameters $params –wait
```

### <a name="not-recognized-as-cmdlet"></a><span data-ttu-id="103e5-159">Scenario: The runbook fails because of a missing cmdlet</span><span class="sxs-lookup"><span data-stu-id="103e5-159">Scenario: The runbook fails because of a missing cmdlet</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-160">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-160">Issue</span></span>

<span data-ttu-id="103e5-161">Your runbook fails with an error similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="103e5-161">Your runbook fails with an error similar to the following example:</span></span>

```
The term 'Connect-AzureRmAccount' is not recognized as the name of a cmdlet, function, script file, or operable program.  Check the spelling of the name, or if the path was included verify that the path is correct and try again.
```

#### <a name="cause"></a><span data-ttu-id="103e5-162">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-162">Cause</span></span>

<span data-ttu-id="103e5-163">This error can be caused by the following reasons:</span><span class="sxs-lookup"><span data-stu-id="103e5-163">This error can be caused by the following reasons:</span></span>

1. <span data-ttu-id="103e5-164">The module containing the cmdlet is not imported into the automation account</span><span class="sxs-lookup"><span data-stu-id="103e5-164">The module containing the cmdlet is not imported into the automation account</span></span>
2. <span data-ttu-id="103e5-165">The module containg the cmdlet is imported but is out of date</span><span class="sxs-lookup"><span data-stu-id="103e5-165">The module containg the cmdlet is imported but is out of date</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-166">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-166">Resolution</span></span>

<span data-ttu-id="103e5-167">This error can be resolved by completing one of the following tasks:</span><span class="sxs-lookup"><span data-stu-id="103e5-167">This error can be resolved by completing one of the following tasks:</span></span>

<span data-ttu-id="103e5-168">If the module is an Azure module, see [How to update Azure PowerShell modules in Azure Automation](../automation-update-azure-modules.md) to learn how to update your modules in your automation account.</span><span class="sxs-lookup"><span data-stu-id="103e5-168">If the module is an Azure module, see [How to update Azure PowerShell modules in Azure Automation](../automation-update-azure-modules.md) to learn how to update your modules in your automation account.</span></span>

<span data-ttu-id="103e5-169">If it is a seperate module, ensure the module in imported in your Automation Account.</span><span class="sxs-lookup"><span data-stu-id="103e5-169">If it is a seperate module, ensure the module in imported in your Automation Account.</span></span>

### <a name="job-attempted-3-times"></a><span data-ttu-id="103e5-170">Scenario: The runbook job start was attempted three times, but it failed to start each time</span><span class="sxs-lookup"><span data-stu-id="103e5-170">Scenario: The runbook job start was attempted three times, but it failed to start each time</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-171">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-171">Issue</span></span>

<span data-ttu-id="103e5-172">Your runbook fails with the error:</span><span class="sxs-lookup"><span data-stu-id="103e5-172">Your runbook fails with the error:</span></span>

```
The job was tried three times but it failed
```

#### <a name="cause"></a><span data-ttu-id="103e5-173">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-173">Cause</span></span>

<span data-ttu-id="103e5-174">This error can be caused by the following reasons:</span><span class="sxs-lookup"><span data-stu-id="103e5-174">This error can be caused by the following reasons:</span></span>

1. <span data-ttu-id="103e5-175">Memory Limit.</span><span class="sxs-lookup"><span data-stu-id="103e5-175">Memory Limit.</span></span> <span data-ttu-id="103e5-176">There are documented limits on how much memory allocated to a Sandbox  [Automation service limits](../../azure-subscription-service-limits.md#automation-limits) so a job may fail it if it is using more than 400 MB of memory.</span><span class="sxs-lookup"><span data-stu-id="103e5-176">There are documented limits on how much memory allocated to a Sandbox  [Automation service limits](../../azure-subscription-service-limits.md#automation-limits) so a job may fail it if it is using more than 400 MB of memory.</span></span>

2. <span data-ttu-id="103e5-177">Module Incompatible.</span><span class="sxs-lookup"><span data-stu-id="103e5-177">Module Incompatible.</span></span> <span data-ttu-id="103e5-178">This can occur if module dependencies are not correct and if they are not, your runbook typically returns a "Command not found" or "Cannot bind parameter" message.</span><span class="sxs-lookup"><span data-stu-id="103e5-178">This can occur if module dependencies are not correct and if they are not, your runbook typically returns a "Command not found" or "Cannot bind parameter" message.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-179">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-179">Resolution</span></span>

<span data-ttu-id="103e5-180">Any of the following solutions fix the problem:</span><span class="sxs-lookup"><span data-stu-id="103e5-180">Any of the following solutions fix the problem:</span></span>

* <span data-ttu-id="103e5-181">Suggested methods to work within the memory limit are to split the workload between multiple runbooks, not process as much data in memory, not to write unnecessary output from your runbooks, or consider how many checkpoints you write into your PowerShell workflow runbooks.</span><span class="sxs-lookup"><span data-stu-id="103e5-181">Suggested methods to work within the memory limit are to split the workload between multiple runbooks, not process as much data in memory, not to write unnecessary output from your runbooks, or consider how many checkpoints you write into your PowerShell workflow runbooks.</span></span>  

* <span data-ttu-id="103e5-182">Update your Azure modules by following the steps [How to update Azure PowerShell modules in Azure Automation](../automation-update-azure-modules.md).</span><span class="sxs-lookup"><span data-stu-id="103e5-182">Update your Azure modules by following the steps [How to update Azure PowerShell modules in Azure Automation](../automation-update-azure-modules.md).</span></span>  

* <span data-ttu-id="103e5-183">Another solution is to run the runbook on a [Hybrid Runbook Worker](../automation-hrw-run-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="103e5-183">Another solution is to run the runbook on a [Hybrid Runbook Worker](../automation-hrw-run-runbooks.md).</span></span> <span data-ttu-id="103e5-184">Hybrid Workers are not limited by the [fair share](../automation-runbook-execution.md#fair-share) limits that Azure sandboxes are.</span><span class="sxs-lookup"><span data-stu-id="103e5-184">Hybrid Workers are not limited by the [fair share](../automation-runbook-execution.md#fair-share) limits that Azure sandboxes are.</span></span>

### <a name="fails-deserialized-object"></a><span data-ttu-id="103e5-185">Scenario: Runbook fails because of deserialized object</span><span class="sxs-lookup"><span data-stu-id="103e5-185">Scenario: Runbook fails because of deserialized object</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-186">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-186">Issue</span></span>

<span data-ttu-id="103e5-187">Your runbook fails with the error:</span><span class="sxs-lookup"><span data-stu-id="103e5-187">Your runbook fails with the error:</span></span>

```
Cannot bind parameter <ParameterName>.

Cannot convert the <ParameterType> value of type Deserialized <ParameterType> to type <ParameterType>.
```

#### <a name="cause"></a><span data-ttu-id="103e5-188">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-188">Cause</span></span>

<span data-ttu-id="103e5-189">If your runbook is a PowerShell Workflow, it stores complex objects in a deserialized format in order to persist your runbook state if the workflow is suspended.</span><span class="sxs-lookup"><span data-stu-id="103e5-189">If your runbook is a PowerShell Workflow, it stores complex objects in a deserialized format in order to persist your runbook state if the workflow is suspended.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-190">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-190">Resolution</span></span>

<span data-ttu-id="103e5-191">Any of the following three solutions fix this problem:</span><span class="sxs-lookup"><span data-stu-id="103e5-191">Any of the following three solutions fix this problem:</span></span>

1. <span data-ttu-id="103e5-192">If you are piping complex objects from one cmdlet to another, wrap these cmdlets in an InlineScript.</span><span class="sxs-lookup"><span data-stu-id="103e5-192">If you are piping complex objects from one cmdlet to another, wrap these cmdlets in an InlineScript.</span></span>
2. <span data-ttu-id="103e5-193">Pass the name or value that you need from the complex object instead of passing the entire object.</span><span class="sxs-lookup"><span data-stu-id="103e5-193">Pass the name or value that you need from the complex object instead of passing the entire object.</span></span>
3. <span data-ttu-id="103e5-194">Use a PowerShell runbook instead of a PowerShell Workflow runbook.</span><span class="sxs-lookup"><span data-stu-id="103e5-194">Use a PowerShell runbook instead of a PowerShell Workflow runbook.</span></span>

### <a name="quota-exceeded"></a><span data-ttu-id="103e5-195">Scenario: Runbook job failed because the allocated quota exceeded</span><span class="sxs-lookup"><span data-stu-id="103e5-195">Scenario: Runbook job failed because the allocated quota exceeded</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-196">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-196">Issue</span></span>

<span data-ttu-id="103e5-197">Your runbook job fails with the error:</span><span class="sxs-lookup"><span data-stu-id="103e5-197">Your runbook job fails with the error:</span></span>

```
The quota for the monthly total job run time has been reached for this subscription
```

#### <a name="cause"></a><span data-ttu-id="103e5-198">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-198">Cause</span></span>

<span data-ttu-id="103e5-199">This error occurs when the job execution exceeds the 500-minute free quota for your account.</span><span class="sxs-lookup"><span data-stu-id="103e5-199">This error occurs when the job execution exceeds the 500-minute free quota for your account.</span></span> <span data-ttu-id="103e5-200">This quota applies to all types of job execution tasks such as testing a job, starting a job from the portal, executing a job by using webhooks and scheduling a job to execute by using either the Azure portal or in your datacenter.</span><span class="sxs-lookup"><span data-stu-id="103e5-200">This quota applies to all types of job execution tasks such as testing a job, starting a job from the portal, executing a job by using webhooks and scheduling a job to execute by using either the Azure portal or in your datacenter.</span></span> <span data-ttu-id="103e5-201">To learn more about pricing for Automation, see [Automation pricing](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="103e5-201">To learn more about pricing for Automation, see [Automation pricing](https://azure.microsoft.com/pricing/details/automation/).</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-202">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-202">Resolution</span></span>

<span data-ttu-id="103e5-203">If you want to use more than 500 minutes of processing per month, you need to change your subscription from the Free tier to the Basic tier.</span><span class="sxs-lookup"><span data-stu-id="103e5-203">If you want to use more than 500 minutes of processing per month, you need to change your subscription from the Free tier to the Basic tier.</span></span> <span data-ttu-id="103e5-204">You can upgrade to the Basic tier by taking the following steps:</span><span class="sxs-lookup"><span data-stu-id="103e5-204">You can upgrade to the Basic tier by taking the following steps:</span></span>  

1. <span data-ttu-id="103e5-205">Sign in to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="103e5-205">Sign in to your Azure subscription</span></span>  
2. <span data-ttu-id="103e5-206">Select the Automation account you wish to upgrade</span><span class="sxs-lookup"><span data-stu-id="103e5-206">Select the Automation account you wish to upgrade</span></span>  
3. <span data-ttu-id="103e5-207">Click on **Settings** > **Pricing**.</span><span class="sxs-lookup"><span data-stu-id="103e5-207">Click on **Settings** > **Pricing**.</span></span>
4. <span data-ttu-id="103e5-208">Click **Enable** on page bottom to upgrade your account to the **Basic** tier.</span><span class="sxs-lookup"><span data-stu-id="103e5-208">Click **Enable** on page bottom to upgrade your account to the **Basic** tier.</span></span>

### <a name="cmdlet-not-recognized"></a><span data-ttu-id="103e5-209">Scenario: Cmdlet not recognized when executing a runbook</span><span class="sxs-lookup"><span data-stu-id="103e5-209">Scenario: Cmdlet not recognized when executing a runbook</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-210">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-210">Issue</span></span>

<span data-ttu-id="103e5-211">Your runbook job fails with the error:</span><span class="sxs-lookup"><span data-stu-id="103e5-211">Your runbook job fails with the error:</span></span>

```
<cmdlet name>: The term <cmdlet name> is not recognized as the name of a cmdlet, function, script file, or operable program.
```

#### <a name="cause"></a><span data-ttu-id="103e5-212">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-212">Cause</span></span>

<span data-ttu-id="103e5-213">This error is caused when the PowerShell engine cannot find the cmdlet you are using in your runbook.</span><span class="sxs-lookup"><span data-stu-id="103e5-213">This error is caused when the PowerShell engine cannot find the cmdlet you are using in your runbook.</span></span> <span data-ttu-id="103e5-214">This could be because the module containing the cmdlet is missing from the account, there is a name conflict with a runbook name, or the cmdlet also exists in another module and Automation cannot resolve the name.</span><span class="sxs-lookup"><span data-stu-id="103e5-214">This could be because the module containing the cmdlet is missing from the account, there is a name conflict with a runbook name, or the cmdlet also exists in another module and Automation cannot resolve the name.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-215">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-215">Resolution</span></span>

<span data-ttu-id="103e5-216">Any of the following solutions fix the problem:</span><span class="sxs-lookup"><span data-stu-id="103e5-216">Any of the following solutions fix the problem:</span></span>  

* <span data-ttu-id="103e5-217">Check that you have entered the cmdlet name correctly.</span><span class="sxs-lookup"><span data-stu-id="103e5-217">Check that you have entered the cmdlet name correctly.</span></span>  
* <span data-ttu-id="103e5-218">Make sure the cmdlet exists in your Automation account and that there are no conflicts.</span><span class="sxs-lookup"><span data-stu-id="103e5-218">Make sure the cmdlet exists in your Automation account and that there are no conflicts.</span></span> <span data-ttu-id="103e5-219">To verify if the cmdlet is present, open a runbook in edit mode and search for the cmdlet you want to find in the library or run `Get-Command <CommandName>`.</span><span class="sxs-lookup"><span data-stu-id="103e5-219">To verify if the cmdlet is present, open a runbook in edit mode and search for the cmdlet you want to find in the library or run `Get-Command <CommandName>`.</span></span> <span data-ttu-id="103e5-220">Once you have validated that the cmdlet is available to the account, and that there are no name conflicts with other cmdlets or runbooks, add it to the canvas and ensure that you are using a valid parameter set in your runbook.</span><span class="sxs-lookup"><span data-stu-id="103e5-220">Once you have validated that the cmdlet is available to the account, and that there are no name conflicts with other cmdlets or runbooks, add it to the canvas and ensure that you are using a valid parameter set in your runbook.</span></span>  
* <span data-ttu-id="103e5-221">If you do have a name conflict and the cmdlet is available in two different modules, you can resolve this by using the fully qualified name for the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="103e5-221">If you do have a name conflict and the cmdlet is available in two different modules, you can resolve this by using the fully qualified name for the cmdlet.</span></span> <span data-ttu-id="103e5-222">For example, you can use **ModuleName\CmdletName**.</span><span class="sxs-lookup"><span data-stu-id="103e5-222">For example, you can use **ModuleName\CmdletName**.</span></span>  
* <span data-ttu-id="103e5-223">If you are executing the runbook on-premises in a hybrid worker group, then make sure that the module/cmdlet is installed on the machine that hosts the hybrid worker.</span><span class="sxs-lookup"><span data-stu-id="103e5-223">If you are executing the runbook on-premises in a hybrid worker group, then make sure that the module/cmdlet is installed on the machine that hosts the hybrid worker.</span></span>

### <a name="evicted-from-checkpoint"></a><span data-ttu-id="103e5-224">Scenario: A long running runbook consistently fails with the exception: "The job cannot continue running because it was repeatedly evicted from the same checkpoint"</span><span class="sxs-lookup"><span data-stu-id="103e5-224">Scenario: A long running runbook consistently fails with the exception: "The job cannot continue running because it was repeatedly evicted from the same checkpoint"</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-225">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-225">Issue</span></span>

<span data-ttu-id="103e5-226">This behavior is by design due to the "Fair Share" monitoring of processes within Azure Automation, which automatically suspends a runbook if it executes longer than three hours.</span><span class="sxs-lookup"><span data-stu-id="103e5-226">This behavior is by design due to the "Fair Share" monitoring of processes within Azure Automation, which automatically suspends a runbook if it executes longer than three hours.</span></span> <span data-ttu-id="103e5-227">However, the error message returned does not provide "what next" options.</span><span class="sxs-lookup"><span data-stu-id="103e5-227">However, the error message returned does not provide "what next" options.</span></span>

#### <a name="cause"></a><span data-ttu-id="103e5-228">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-228">Cause</span></span>

<span data-ttu-id="103e5-229">A runbook can be suspended for a number of reasons.</span><span class="sxs-lookup"><span data-stu-id="103e5-229">A runbook can be suspended for a number of reasons.</span></span> <span data-ttu-id="103e5-230">Suspends happen mostly due to errors.</span><span class="sxs-lookup"><span data-stu-id="103e5-230">Suspends happen mostly due to errors.</span></span> <span data-ttu-id="103e5-231">For example, an uncaught exception in a runbook, a network failure, or a crash on the Runbook Worker running the runbook, all cause the runbook to be suspended and start from its last checkpoint when resumed.</span><span class="sxs-lookup"><span data-stu-id="103e5-231">For example, an uncaught exception in a runbook, a network failure, or a crash on the Runbook Worker running the runbook, all cause the runbook to be suspended and start from its last checkpoint when resumed.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-232">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-232">Resolution</span></span>

<span data-ttu-id="103e5-233">The documented solution to avoid this issue is to use Checkpoints in a workflow.</span><span class="sxs-lookup"><span data-stu-id="103e5-233">The documented solution to avoid this issue is to use Checkpoints in a workflow.</span></span> <span data-ttu-id="103e5-234">To learn more, refer to [Learning PowerShell Workflows](../automation-powershell-workflow.md#checkpoints).</span><span class="sxs-lookup"><span data-stu-id="103e5-234">To learn more, refer to [Learning PowerShell Workflows](../automation-powershell-workflow.md#checkpoints).</span></span> <span data-ttu-id="103e5-235">A more thorough explanation of "Fair Share" and Checkpoint can be found in this blog article [Using Checkpoints in Runbooks](https://azure.microsoft.com/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).</span><span class="sxs-lookup"><span data-stu-id="103e5-235">A more thorough explanation of "Fair Share" and Checkpoint can be found in this blog article [Using Checkpoints in Runbooks](https://azure.microsoft.com/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).</span></span>

### <a name="long-running-runbook"></a><span data-ttu-id="103e5-236">Scenario: A long running runbook fails to complete</span><span class="sxs-lookup"><span data-stu-id="103e5-236">Scenario: A long running runbook fails to complete</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-237">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-237">Issue</span></span>

<span data-ttu-id="103e5-238">This behavior is by design in Azure sandboxes due to the "Fair Share" monitoring of processes within Azure Automation, which automatically suspends a runbook if it executes longer than three hours.</span><span class="sxs-lookup"><span data-stu-id="103e5-238">This behavior is by design in Azure sandboxes due to the "Fair Share" monitoring of processes within Azure Automation, which automatically suspends a runbook if it executes longer than three hours.</span></span>

#### <a name="cause"></a><span data-ttu-id="103e5-239">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-239">Cause</span></span>

<span data-ttu-id="103e5-240">The runbook ran over the 3 hour limit allowed by fair share in an Azure Sandbox</span><span class="sxs-lookup"><span data-stu-id="103e5-240">The runbook ran over the 3 hour limit allowed by fair share in an Azure Sandbox</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-241">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-241">Resolution</span></span>

<span data-ttu-id="103e5-242">The recommended solution is to run the runbook on a [Hybrid Runbook Worker](../automation-hrw-run-runbooks.md).</span><span class="sxs-lookup"><span data-stu-id="103e5-242">The recommended solution is to run the runbook on a [Hybrid Runbook Worker](../automation-hrw-run-runbooks.md).</span></span> <span data-ttu-id="103e5-243">Hybrid Workers are not limited by the [fair share](../automation-runbook-execution.md#fair-share) 3 hour runbook limit that Azure sandboxes are.</span><span class="sxs-lookup"><span data-stu-id="103e5-243">Hybrid Workers are not limited by the [fair share](../automation-runbook-execution.md#fair-share) 3 hour runbook limit that Azure sandboxes are.</span></span>

## <a name="common-errors-when-importing-modules"></a><span data-ttu-id="103e5-244">Common errors when importing modules</span><span class="sxs-lookup"><span data-stu-id="103e5-244">Common errors when importing modules</span></span>

### <a name="module-fails-to-import"></a><span data-ttu-id="103e5-245">Scenario: Module fails to import or cmdlets can't be executed after importing</span><span class="sxs-lookup"><span data-stu-id="103e5-245">Scenario: Module fails to import or cmdlets can't be executed after importing</span></span>

#### <a name="issue"></a><span data-ttu-id="103e5-246">Issue</span><span class="sxs-lookup"><span data-stu-id="103e5-246">Issue</span></span>

<span data-ttu-id="103e5-247">A module fails to import or imports successfully, but no cmdlets are extracted.</span><span class="sxs-lookup"><span data-stu-id="103e5-247">A module fails to import or imports successfully, but no cmdlets are extracted.</span></span>

#### <a name="cause"></a><span data-ttu-id="103e5-248">Cause</span><span class="sxs-lookup"><span data-stu-id="103e5-248">Cause</span></span>

<span data-ttu-id="103e5-249">Some common reasons that a module might not successfully import to Azure Automation are:</span><span class="sxs-lookup"><span data-stu-id="103e5-249">Some common reasons that a module might not successfully import to Azure Automation are:</span></span>

* <span data-ttu-id="103e5-250">The structure does not match the structure that Automation needs it to be in.</span><span class="sxs-lookup"><span data-stu-id="103e5-250">The structure does not match the structure that Automation needs it to be in.</span></span>
* <span data-ttu-id="103e5-251">The module is dependent on another module that has not been deployed to your Automation account.</span><span class="sxs-lookup"><span data-stu-id="103e5-251">The module is dependent on another module that has not been deployed to your Automation account.</span></span>
* <span data-ttu-id="103e5-252">The module is missing its dependencies in the folder.</span><span class="sxs-lookup"><span data-stu-id="103e5-252">The module is missing its dependencies in the folder.</span></span>
* <span data-ttu-id="103e5-253">The `New-AzureRmAutomationModule` cmdlet is being used to upload the module, and you have not given the full storage path or have not loaded the module by using a publicly accessible URL.</span><span class="sxs-lookup"><span data-stu-id="103e5-253">The `New-AzureRmAutomationModule` cmdlet is being used to upload the module, and you have not given the full storage path or have not loaded the module by using a publicly accessible URL.</span></span>

#### <a name="resolution"></a><span data-ttu-id="103e5-254">Resolution</span><span class="sxs-lookup"><span data-stu-id="103e5-254">Resolution</span></span>

<span data-ttu-id="103e5-255">Any of the following solutions fix the problem:</span><span class="sxs-lookup"><span data-stu-id="103e5-255">Any of the following solutions fix the problem:</span></span>

* <span data-ttu-id="103e5-256">Make sure that the module follows the following format: ModuleName.Zip **->** ModuleName or Version Number **->** (ModuleName.psm1, ModuleName.psd1)</span><span class="sxs-lookup"><span data-stu-id="103e5-256">Make sure that the module follows the following format: ModuleName.Zip **->** ModuleName or Version Number **->** (ModuleName.psm1, ModuleName.psd1)</span></span>
* <span data-ttu-id="103e5-257">Open the .psd1 file and see if the module has any dependencies.</span><span class="sxs-lookup"><span data-stu-id="103e5-257">Open the .psd1 file and see if the module has any dependencies.</span></span> <span data-ttu-id="103e5-258">If it does, upload these modules to the Automation account.</span><span class="sxs-lookup"><span data-stu-id="103e5-258">If it does, upload these modules to the Automation account.</span></span>
* <span data-ttu-id="103e5-259">Make sure that any referenced .dlls are present in the module folder.</span><span class="sxs-lookup"><span data-stu-id="103e5-259">Make sure that any referenced .dlls are present in the module folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="103e5-260">Next steps</span><span class="sxs-lookup"><span data-stu-id="103e5-260">Next steps</span></span>

<span data-ttu-id="103e5-261">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span><span class="sxs-lookup"><span data-stu-id="103e5-261">If you did not see your problem or are unable to solve your issue, visit one of the following channels for more support:</span></span>

* <span data-ttu-id="103e5-262">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span><span class="sxs-lookup"><span data-stu-id="103e5-262">Get answers from Azure experts through [Azure Forums](https://azure.microsoft.com/support/forums/)</span></span>
* <span data-ttu-id="103e5-263">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span><span class="sxs-lookup"><span data-stu-id="103e5-263">Connect with [@AzureSupport](https://twitter.com/azuresupport) – the official Microsoft Azure account for improving customer experience by connecting the Azure community to the right resources: answers, support, and experts.</span></span>
* <span data-ttu-id="103e5-264">If you need more help, you can file an Azure support incident.</span><span class="sxs-lookup"><span data-stu-id="103e5-264">If you need more help, you can file an Azure support incident.</span></span> <span data-ttu-id="103e5-265">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="103e5-265">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>