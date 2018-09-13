---
title: Validate Azure registration for Azure Stack | Microsoft Docs
description: Use the Azure Stack Readiness Checker to validate Azure registration.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/08/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 57869de8a99c65810da0c75f81c75d93eac88412
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856950"
---
# <a name="validate-azure-registration"></a><span data-ttu-id="99f56-103">Validate Azure registration</span><span class="sxs-lookup"><span data-stu-id="99f56-103">Validate Azure registration</span></span> 
<span data-ttu-id="99f56-104">Use the Azure Stack Readiness Checker tool (AzsReadinessChecker) to validate that your Azure subscription is ready to use with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="99f56-104">Use the Azure Stack Readiness Checker tool (AzsReadinessChecker) to validate that your Azure subscription is ready to use with Azure Stack.</span></span> <span data-ttu-id="99f56-105">Validate registration before you begin an Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="99f56-105">Validate registration before you begin an Azure Stack deployment.</span></span> <span data-ttu-id="99f56-106">The readiness checker validates:</span><span class="sxs-lookup"><span data-stu-id="99f56-106">The readiness checker validates:</span></span>
- <span data-ttu-id="99f56-107">The Azure subscription you use is a supported type.</span><span class="sxs-lookup"><span data-stu-id="99f56-107">The Azure subscription you use is a supported type.</span></span> <span data-ttu-id="99f56-108">Subscriptions must be a Cloud Service Provider (CSP) or Enterprise Agreement (EA).</span><span class="sxs-lookup"><span data-stu-id="99f56-108">Subscriptions must be a Cloud Service Provider (CSP) or Enterprise Agreement (EA).</span></span> 
- <span data-ttu-id="99f56-109">The account you use to register your subscription with Azure can sign in to Azure and is a subscription owner.</span><span class="sxs-lookup"><span data-stu-id="99f56-109">The account you use to register your subscription with Azure can sign in to Azure and is a subscription owner.</span></span> 

<span data-ttu-id="99f56-110">For more information about Azure Stack registration, see [Register Azure Stack with Azure](azure-stack-registration.md).</span><span class="sxs-lookup"><span data-stu-id="99f56-110">For more information about Azure Stack registration, see [Register Azure Stack with Azure](azure-stack-registration.md).</span></span> 

## <a name="get-the-readiness-checker-tool"></a><span data-ttu-id="99f56-111">Get the readiness checker tool</span><span class="sxs-lookup"><span data-stu-id="99f56-111">Get the readiness checker tool</span></span>
<span data-ttu-id="99f56-112">Download the latest version of the Azure Stack Readiness Checker tool (AzsReadinessChecker) is available on [PSGallery](https://aka.ms/AzsReadinessChecker).</span><span class="sxs-lookup"><span data-stu-id="99f56-112">Download the latest version of the Azure Stack Readiness Checker tool (AzsReadinessChecker) is available on [PSGallery](https://aka.ms/AzsReadinessChecker).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="99f56-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99f56-113">Prerequisites</span></span>
<span data-ttu-id="99f56-114">The following prerequisites must be in place.</span><span class="sxs-lookup"><span data-stu-id="99f56-114">The following prerequisites must be in place.</span></span>

<span data-ttu-id="99f56-115">**The computer where the tool runs:**</span><span class="sxs-lookup"><span data-stu-id="99f56-115">**The computer where the tool runs:**</span></span>
 - <span data-ttu-id="99f56-116">Windows 10 or Windows Server 2016, with internet connectivity.</span><span class="sxs-lookup"><span data-stu-id="99f56-116">Windows 10 or Windows Server 2016, with internet connectivity.</span></span>
 - <span data-ttu-id="99f56-117">PowerShell 5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="99f56-117">PowerShell 5.1 or later.</span></span> <span data-ttu-id="99f56-118">To check your version, run the following PowerShell cmd and then review the *Major* version and *Minor* versions:</span><span class="sxs-lookup"><span data-stu-id="99f56-118">To check your version, run the following PowerShell cmd and then review the *Major* version and *Minor* versions:</span></span>  

    >`$PSVersionTable.PSVersion` 
 - <span data-ttu-id="99f56-119">Configure [PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="99f56-119">Configure [PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
 - <span data-ttu-id="99f56-120">Download the latest version of [Microsoft Azure Stack Readiness Checker](https://aka.ms/AzsReadinessChecker) tool.</span><span class="sxs-lookup"><span data-stu-id="99f56-120">Download the latest version of [Microsoft Azure Stack Readiness Checker](https://aka.ms/AzsReadinessChecker) tool.</span></span>  

<span data-ttu-id="99f56-121">**Azure Active Directory environment:**</span><span class="sxs-lookup"><span data-stu-id="99f56-121">**Azure Active Directory environment:**</span></span>
 - <span data-ttu-id="99f56-122">Identify the username and password for an account that is an owner for the Azure subscription you will use with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="99f56-122">Identify the username and password for an account that is an owner for the Azure subscription you will use with Azure Stack.</span></span>  
 - <span data-ttu-id="99f56-123">Identify the subscription ID for the Azure subscription you will use.</span><span class="sxs-lookup"><span data-stu-id="99f56-123">Identify the subscription ID for the Azure subscription you will use.</span></span> 
 - <span data-ttu-id="99f56-124">Identify the AzureEnvironment you will use: *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span><span class="sxs-lookup"><span data-stu-id="99f56-124">Identify the AzureEnvironment you will use: *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span></span>

## <a name="validate-azure-registration"></a><span data-ttu-id="99f56-125">Validate Azure registration</span><span class="sxs-lookup"><span data-stu-id="99f56-125">Validate Azure registration</span></span>
1. <span data-ttu-id="99f56-126">On a computer that meets the prerequisites, open an administrative PowerShell prompt and then run the following command to install the AzsReadinessChecker.</span><span class="sxs-lookup"><span data-stu-id="99f56-126">On a computer that meets the prerequisites, open an administrative PowerShell prompt and then run the following command to install the AzsReadinessChecker.</span></span>
    > `Install-Module Microsoft.AzureStack.ReadinessChecker -Force`

2. <span data-ttu-id="99f56-127">From the PowerShell prompt, run the following to set *$registrationCredential* as the account that is the subscription owner.</span><span class="sxs-lookup"><span data-stu-id="99f56-127">From the PowerShell prompt, run the following to set *$registrationCredential* as the account that is the subscription owner.</span></span>   <span data-ttu-id="99f56-128">Replace *subscriptionowner@contoso.onmicrosoft.com* with your account and tenant.</span><span class="sxs-lookup"><span data-stu-id="99f56-128">Replace *subscriptionowner@contoso.onmicrosoft.com* with your account and tenant.</span></span> 
    > `$registrationCredential = Get-Credential subscriptionowner@contoso.onmicrosoft.com -Message "Enter Credentials for Subscription Owner"`

3. <span data-ttu-id="99f56-129">From the PowerShell prompt, run the following to set *$subscriptionID* as the Azure subscription you will use.</span><span class="sxs-lookup"><span data-stu-id="99f56-129">From the PowerShell prompt, run the following to set *$subscriptionID* as the Azure subscription you will use.</span></span> <span data-ttu-id="99f56-130">Replace *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx* with your own subscription ID.</span><span class="sxs-lookup"><span data-stu-id="99f56-130">Replace *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx* with your own subscription ID.</span></span>  
     > `$subscriptionID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"` 

4. <span data-ttu-id="99f56-131">From the PowerShell prompt, run the following to start validation of your subscription</span><span class="sxs-lookup"><span data-stu-id="99f56-131">From the PowerShell prompt, run the following to start validation of your subscription</span></span> 
   - <span data-ttu-id="99f56-132">Specify the value for AzureEnvironment as *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span><span class="sxs-lookup"><span data-stu-id="99f56-132">Specify the value for AzureEnvironment as *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span></span>  
   - <span data-ttu-id="99f56-133">Provide your Azure Active Directory administrator and your Azure Active Directory Tenant name.</span><span class="sxs-lookup"><span data-stu-id="99f56-133">Provide your Azure Active Directory administrator and your Azure Active Directory Tenant name.</span></span> 

   > `Start-AzsReadinessChecker -RegistrationAccount $registrationCredential -AzureEnvironment AzureCloud -RegistrationSubscriptionID $subscriptionID`

5. <span data-ttu-id="99f56-134">After the tool runs, review the output.</span><span class="sxs-lookup"><span data-stu-id="99f56-134">After the tool runs, review the output.</span></span> <span data-ttu-id="99f56-135">Confirm the status is OK for both logon and the registration requirements.</span><span class="sxs-lookup"><span data-stu-id="99f56-135">Confirm the status is OK for both logon and the registration requirements.</span></span> <span data-ttu-id="99f56-136">A successful validation appears like the following image:</span><span class="sxs-lookup"><span data-stu-id="99f56-136">A successful validation appears like the following image:</span></span>  
![run-validation](./media/azure-stack-validate-registration/registration-validation.png)


## <a name="report-and-log-file"></a><span data-ttu-id="99f56-138">Report and log file</span><span class="sxs-lookup"><span data-stu-id="99f56-138">Report and log file</span></span>
<span data-ttu-id="99f56-139">Each time validation runs, it logs results to **AzsReadinessChecker.log** and **AzsReadinessCheckerReport.json**.</span><span class="sxs-lookup"><span data-stu-id="99f56-139">Each time validation runs, it logs results to **AzsReadinessChecker.log** and **AzsReadinessCheckerReport.json**.</span></span> <span data-ttu-id="99f56-140">The location of these files displays with the validation results in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99f56-140">The location of these files displays with the validation results in PowerShell.</span></span> 

<span data-ttu-id="99f56-141">These files can help you share validation status before you deploy Azure Stack or investigate validation problems.</span><span class="sxs-lookup"><span data-stu-id="99f56-141">These files can help you share validation status before you deploy Azure Stack or investigate validation problems.</span></span> <span data-ttu-id="99f56-142">Both files persist the results of each subsequent validation check.</span><span class="sxs-lookup"><span data-stu-id="99f56-142">Both files persist the results of each subsequent validation check.</span></span> <span data-ttu-id="99f56-143">The report provides your deployment team confirmation of the identity configuration.</span><span class="sxs-lookup"><span data-stu-id="99f56-143">The report provides your deployment team confirmation of the identity configuration.</span></span> <span data-ttu-id="99f56-144">The log file can help your deployment or support team investigate validation issues.</span><span class="sxs-lookup"><span data-stu-id="99f56-144">The log file can help your deployment or support team investigate validation issues.</span></span> 

<span data-ttu-id="99f56-145">By default, both files are written to *C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json*.</span><span class="sxs-lookup"><span data-stu-id="99f56-145">By default, both files are written to *C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json*.</span></span>  
 - <span data-ttu-id="99f56-146">Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.</span><span class="sxs-lookup"><span data-stu-id="99f56-146">Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.</span></span>   
 - <span data-ttu-id="99f56-147">Use the **-CleanReport** parameter at the end of the run command to clear information from *AzsReadinessCheckerReport.json*.</span><span class="sxs-lookup"><span data-stu-id="99f56-147">Use the **-CleanReport** parameter at the end of the run command to clear information from *AzsReadinessCheckerReport.json*.</span></span>  <span data-ttu-id="99f56-148">about previous runs of the tool.</span><span class="sxs-lookup"><span data-stu-id="99f56-148">about previous runs of the tool.</span></span> <span data-ttu-id="99f56-149">For more information, [Azure Stack validation report](azure-stack-validation-report.md).</span><span class="sxs-lookup"><span data-stu-id="99f56-149">For more information, [Azure Stack validation report](azure-stack-validation-report.md).</span></span>

## <a name="validation-failures"></a><span data-ttu-id="99f56-150">Validation failures</span><span class="sxs-lookup"><span data-stu-id="99f56-150">Validation failures</span></span>
<span data-ttu-id="99f56-151">If a validation check fails, details about the failure display in the PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="99f56-151">If a validation check fails, details about the failure display in the PowerShell window.</span></span> <span data-ttu-id="99f56-152">The tool also logs information to the AzsReadinessChecker.log.</span><span class="sxs-lookup"><span data-stu-id="99f56-152">The tool also logs information to the AzsReadinessChecker.log.</span></span>

<span data-ttu-id="99f56-153">The following examples provide guidance on common validation failures.</span><span class="sxs-lookup"><span data-stu-id="99f56-153">The following examples provide guidance on common validation failures.</span></span>

### <a name="user-must-be-an-owner-of-the-subscription"></a><span data-ttu-id="99f56-154">User must be an owner of the subscription</span><span class="sxs-lookup"><span data-stu-id="99f56-154">User must be an owner of the subscription</span></span>   
<span data-ttu-id="99f56-155">![subscription-owner](./media/azure-stack-validate-registration/subscription-owner.png)
**Cause** - The account is not an administrator of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="99f56-155">![subscription-owner](./media/azure-stack-validate-registration/subscription-owner.png)
**Cause** - The account is not an administrator of the Azure subscription.</span></span>   

<span data-ttu-id="99f56-156">**Resolution** - Use an account that is an administrator of the Azure subscription that will be billed for usage from the Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="99f56-156">**Resolution** - Use an account that is an administrator of the Azure subscription that will be billed for usage from the Azure Stack deployment.</span></span>


### <a name="expired-or-temporary-password"></a><span data-ttu-id="99f56-157">Expired or temporary password</span><span class="sxs-lookup"><span data-stu-id="99f56-157">Expired or temporary password</span></span> 
<span data-ttu-id="99f56-158">![expired-password](./media/azure-stack-validate-registration/expired-password.png)
**Cause** - The account can’t log on because the password is either expired or is temporary.</span><span class="sxs-lookup"><span data-stu-id="99f56-158">![expired-password](./media/azure-stack-validate-registration/expired-password.png)
**Cause** - The account can’t log on because the password is either expired or is temporary.</span></span>     

<span data-ttu-id="99f56-159">**Resolution** - In PowerShell run and follow the prompts to reset the password.</span><span class="sxs-lookup"><span data-stu-id="99f56-159">**Resolution** - In PowerShell run and follow the prompts to reset the password.</span></span> 
  > `Login-AzureRMAccount` 

<span data-ttu-id="99f56-160">Alternatively, login into https://portal.azure.com as the account and the user will be forced to change the password.</span><span class="sxs-lookup"><span data-stu-id="99f56-160">Alternatively, login into https://portal.azure.com as the account and the user will be forced to change the password.</span></span>


### <a name="microsoft-accounts-are-not-supported-for-registration"></a><span data-ttu-id="99f56-161">Microsoft accounts are not supported for registration</span><span class="sxs-lookup"><span data-stu-id="99f56-161">Microsoft accounts are not supported for registration</span></span>  
<span data-ttu-id="99f56-162">![unsupported-account](./media/azure-stack-validate-registration/unsupported-account.png)
**Cause** - A Microsoft account (like Outlook.com or Hotmail.com) was specified.</span><span class="sxs-lookup"><span data-stu-id="99f56-162">![unsupported-account](./media/azure-stack-validate-registration/unsupported-account.png)
**Cause** - A Microsoft account (like Outlook.com or Hotmail.com) was specified.</span></span>  <span data-ttu-id="99f56-163">These accounts are not supported.</span><span class="sxs-lookup"><span data-stu-id="99f56-163">These accounts are not supported.</span></span>

<span data-ttu-id="99f56-164">**Resolution** - Use an account and subscription from a Cloud Service Provider (CSP) or Enterprise Agreement (EA).</span><span class="sxs-lookup"><span data-stu-id="99f56-164">**Resolution** - Use an account and subscription from a Cloud Service Provider (CSP) or Enterprise Agreement (EA).</span></span> 


### <a name="unknown-user-type"></a><span data-ttu-id="99f56-165">Unknown user type</span><span class="sxs-lookup"><span data-stu-id="99f56-165">Unknown user type</span></span>  
<span data-ttu-id="99f56-166">![unknown-user](./media/azure-stack-validate-registration/unknown-user.png)
**Cause** - The account can’t log on to the specified Azure Active Directory environment.</span><span class="sxs-lookup"><span data-stu-id="99f56-166">![unknown-user](./media/azure-stack-validate-registration/unknown-user.png)
**Cause** - The account can’t log on to the specified Azure Active Directory environment.</span></span> <span data-ttu-id="99f56-167">In this example, *AzureChinaCloud* is specified as the *AzureEnvironment*.</span><span class="sxs-lookup"><span data-stu-id="99f56-167">In this example, *AzureChinaCloud* is specified as the *AzureEnvironment*.</span></span>  

<span data-ttu-id="99f56-168">**Resolution** - Confirm that the account is valid for the specified Azure Environment.</span><span class="sxs-lookup"><span data-stu-id="99f56-168">**Resolution** - Confirm that the account is valid for the specified Azure Environment.</span></span> <span data-ttu-id="99f56-169">In PowerShell, run the following to verify the account is valid for a specific environment.</span><span class="sxs-lookup"><span data-stu-id="99f56-169">In PowerShell, run the following to verify the account is valid for a specific environment.</span></span>     
  > `Login-AzureRmAccount -EnvironmentName AzureChinaCloud`


## <a name="next-steps"></a><span data-ttu-id="99f56-170">Next Steps</span><span class="sxs-lookup"><span data-stu-id="99f56-170">Next Steps</span></span>
<span data-ttu-id="99f56-171">[Validate Azure identity](azure-stack-validate-identity.md)
[View the readiness report](azure-stack-validation-report.md)
[General Azure Stack integration considerations](azure-stack-datacenter-integration.md)</span><span class="sxs-lookup"><span data-stu-id="99f56-171">[Validate Azure identity](azure-stack-validate-identity.md)
[View the readiness report](azure-stack-validation-report.md)
[General Azure Stack integration considerations](azure-stack-datacenter-integration.md)</span></span>

