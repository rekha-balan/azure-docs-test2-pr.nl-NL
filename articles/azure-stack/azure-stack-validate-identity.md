---
title: Validate Azure Identity for Azure Stack | Microsoft Docs
description: Use the Azure Stack Readiness Checker to validate Azure identity.
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
ms.date: 05/08/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: fe5e7281cbe01ad11f667729df344f91ef1327d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864432"
---
# <a name="validate-azure-identity"></a><span data-ttu-id="c933a-103">Validate Azure identity</span><span class="sxs-lookup"><span data-stu-id="c933a-103">Validate Azure identity</span></span> 
<span data-ttu-id="c933a-104">Use the Azure Stack Readiness Checker tool (AzsReadinessChecker) to validate that your Azure Active Directory (Azure AD) is ready to use with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c933a-104">Use the Azure Stack Readiness Checker tool (AzsReadinessChecker) to validate that your Azure Active Directory (Azure AD) is ready to use with Azure Stack.</span></span> <span data-ttu-id="c933a-105">Validate your Azure identity solution before you begin an Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="c933a-105">Validate your Azure identity solution before you begin an Azure Stack deployment.</span></span>  

<span data-ttu-id="c933a-106">The readiness checker validates:</span><span class="sxs-lookup"><span data-stu-id="c933a-106">The readiness checker validates:</span></span>
 - <span data-ttu-id="c933a-107">Azure Active Directory (Azure AD) as an identity provider for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="c933a-107">Azure Active Directory (Azure AD) as an identity provider for Azure Stack.</span></span>
 - <span data-ttu-id="c933a-108">The Azure AD account that you plan to use can log on as a global administrator of your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c933a-108">The Azure AD account that you plan to use can log on as a global administrator of your Azure Active Directory.</span></span> 

<span data-ttu-id="c933a-109">Validation ensures your environment is ready for Azure Stack to store information about users, applications, groups, and service principals from Azure Stack in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c933a-109">Validation ensures your environment is ready for Azure Stack to store information about users, applications, groups, and service principals from Azure Stack in your Azure AD.</span></span>

## <a name="get-the-readiness-checker-tool"></a><span data-ttu-id="c933a-110">Get the readiness checker tool</span><span class="sxs-lookup"><span data-stu-id="c933a-110">Get the readiness checker tool</span></span>
<span data-ttu-id="c933a-111">Download the latest version of the Azure Stack Readiness Checker tool (AzsReadinessChecker) from the [PSGallery](https://aka.ms/AzsReadinessChecker).</span><span class="sxs-lookup"><span data-stu-id="c933a-111">Download the latest version of the Azure Stack Readiness Checker tool (AzsReadinessChecker) from the [PSGallery](https://aka.ms/AzsReadinessChecker).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="c933a-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c933a-112">Prerequisites</span></span>
<span data-ttu-id="c933a-113">The following prerequisites must be in place.</span><span class="sxs-lookup"><span data-stu-id="c933a-113">The following prerequisites must be in place.</span></span>

<span data-ttu-id="c933a-114">**The computer where the tool runs:**</span><span class="sxs-lookup"><span data-stu-id="c933a-114">**The computer where the tool runs:**</span></span>
 - <span data-ttu-id="c933a-115">Windows 10 or Windows Server 2016, with internet connectivity.</span><span class="sxs-lookup"><span data-stu-id="c933a-115">Windows 10 or Windows Server 2016, with internet connectivity.</span></span>
 - <span data-ttu-id="c933a-116">PowerShell 5.1 or later.</span><span class="sxs-lookup"><span data-stu-id="c933a-116">PowerShell 5.1 or later.</span></span> <span data-ttu-id="c933a-117">To check your version, run the following PowerShell cmd and then review the *Major* version and *Minor* versions:</span><span class="sxs-lookup"><span data-stu-id="c933a-117">To check your version, run the following PowerShell cmd and then review the *Major* version and *Minor* versions:</span></span>  

   > `$PSVersionTable.PSVersion`
 - <span data-ttu-id="c933a-118">Configure [PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="c933a-118">Configure [PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
 - <span data-ttu-id="c933a-119">The latest version of [Microsoft Azure Stack Readiness Checker](https://aka.ms/AzsReadinessChecker) tool.</span><span class="sxs-lookup"><span data-stu-id="c933a-119">The latest version of [Microsoft Azure Stack Readiness Checker](https://aka.ms/AzsReadinessChecker) tool.</span></span>

<span data-ttu-id="c933a-120">**Azure Active Directory environment:**</span><span class="sxs-lookup"><span data-stu-id="c933a-120">**Azure Active Directory environment:**</span></span>
 - <span data-ttu-id="c933a-121">Identify the Azure AD account you will use for Azure Stack and ensure it is an Azure Active Directory Global administrator.</span><span class="sxs-lookup"><span data-stu-id="c933a-121">Identify the Azure AD account you will use for Azure Stack and ensure it is an Azure Active Directory Global administrator.</span></span>
 - <span data-ttu-id="c933a-122">Identify your Azure AD Tenant Name.</span><span class="sxs-lookup"><span data-stu-id="c933a-122">Identify your Azure AD Tenant Name.</span></span> <span data-ttu-id="c933a-123">The tenant name must be the *primary* domain name for your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c933a-123">The tenant name must be the *primary* domain name for your Azure Active Directory.</span></span> <span data-ttu-id="c933a-124">For example, *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="c933a-124">For example, *contoso.onmicrosoft.com*.</span></span> 
 - <span data-ttu-id="c933a-125">Identify the AzureEnvironement you will use: *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span><span class="sxs-lookup"><span data-stu-id="c933a-125">Identify the AzureEnvironement you will use: *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span></span>

## <a name="validate-azure-identity"></a><span data-ttu-id="c933a-126">Validate Azure identity</span><span class="sxs-lookup"><span data-stu-id="c933a-126">Validate Azure identity</span></span> 
1. <span data-ttu-id="c933a-127">On a computer that meets the prerequisites, open an administrative PowerShell prompt and then run the following command to install the AzsReadinessChecker:</span><span class="sxs-lookup"><span data-stu-id="c933a-127">On a computer that meets the prerequisites, open an administrative PowerShell prompt and then run the following command to install the AzsReadinessChecker:</span></span>  

   > `Install-Module Microsoft.AzureStack.ReadinessChecker -Force`

2. <span data-ttu-id="c933a-128">From the PowerShell prompt, run the following to set *$serviceAdminCredential* as the Service Administrator for your Azure AD Tenant.</span><span class="sxs-lookup"><span data-stu-id="c933a-128">From the PowerShell prompt, run the following to set *$serviceAdminCredential* as the Service Administrator for your Azure AD Tenant.</span></span>  <span data-ttu-id="c933a-129">Replace *serviceadmin@contoso.onmicrosoft.com* with your account and tenant.</span><span class="sxs-lookup"><span data-stu-id="c933a-129">Replace *serviceadmin@contoso.onmicrosoft.com* with your account and tenant.</span></span> 
   > `$serviceAdminCredential = Get-Credential serviceadmin@contoso.onmicrosoft.com -Message "Enter Credentials for Service Administrator of Azure Active Directory Tenant"` 

3. <span data-ttu-id="c933a-130">From the PowerShell prompt, run the following to start validation of your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c933a-130">From the PowerShell prompt, run the following to start validation of your Azure AD.</span></span> 
   - <span data-ttu-id="c933a-131">Specify the value for AzureEnvironment as *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span><span class="sxs-lookup"><span data-stu-id="c933a-131">Specify the value for AzureEnvironment as *AzureCloud*, *AzureGermanCloud*, or *AzureChinaCloud*.</span></span>  
   - <span data-ttu-id="c933a-132">Specify your Azure Active Directory Tenant Name to replace *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="c933a-132">Specify your Azure Active Directory Tenant Name to replace *contoso.onmicrosoft.com*.</span></span> 

   > `Start-AzsReadinessChecker -AADServiceAdministrator $serviceAdminCredential -AzureEnvironment AzureCloud -AADDirectoryTenantName contoso.onmicrosoft.com`
4. <span data-ttu-id="c933a-133">After the tool runs, review the output.</span><span class="sxs-lookup"><span data-stu-id="c933a-133">After the tool runs, review the output.</span></span> <span data-ttu-id="c933a-134">Confirm the status is **OK** for both logon and the installation requirements.</span><span class="sxs-lookup"><span data-stu-id="c933a-134">Confirm the status is **OK** for both logon and the installation requirements.</span></span> <span data-ttu-id="c933a-135">A successful validation appears like the following image:</span><span class="sxs-lookup"><span data-stu-id="c933a-135">A successful validation appears like the following image:</span></span> 
 
![run-validation](./media/azure-stack-validate-identity/validation.png)


## <a name="report-and-log-file"></a><span data-ttu-id="c933a-137">Report and log file</span><span class="sxs-lookup"><span data-stu-id="c933a-137">Report and log file</span></span>
<span data-ttu-id="c933a-138">Each time validation runs, it logs results to **AzsReadinessChecker.log** and **AzsReadinessCheckerReport.json**.</span><span class="sxs-lookup"><span data-stu-id="c933a-138">Each time validation runs, it logs results to **AzsReadinessChecker.log** and **AzsReadinessCheckerReport.json**.</span></span> <span data-ttu-id="c933a-139">The location of these files displays with the validation results in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c933a-139">The location of these files displays with the validation results in PowerShell.</span></span>

<span data-ttu-id="c933a-140">These files can help you share validation status before you deploy Azure Stack or investigate validation problems.</span><span class="sxs-lookup"><span data-stu-id="c933a-140">These files can help you share validation status before you deploy Azure Stack or investigate validation problems.</span></span>  <span data-ttu-id="c933a-141">Both files persist the results of each subsequent validation check.</span><span class="sxs-lookup"><span data-stu-id="c933a-141">Both files persist the results of each subsequent validation check.</span></span> <span data-ttu-id="c933a-142">The report provides your deployment team confirmation of the identity configuration.</span><span class="sxs-lookup"><span data-stu-id="c933a-142">The report provides your deployment team confirmation of the identity configuration.</span></span> <span data-ttu-id="c933a-143">The log file can help your deployment or support team investigate validation issues.</span><span class="sxs-lookup"><span data-stu-id="c933a-143">The log file can help your deployment or support team investigate validation issues.</span></span> 

<span data-ttu-id="c933a-144">By default, both files are written to *C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json*.</span><span class="sxs-lookup"><span data-stu-id="c933a-144">By default, both files are written to *C:\Users\<username>\AppData\Local\Temp\AzsReadinessChecker\AzsReadinessCheckerReport.json*.</span></span>  
 - <span data-ttu-id="c933a-145">Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.</span><span class="sxs-lookup"><span data-stu-id="c933a-145">Use the **-OutputPath** ***&lt;path&gt;*** parameter at the end of the run command line to specify a different report location.</span></span>   
 - <span data-ttu-id="c933a-146">Use the **-CleanReport** parameter at the end of the run command to clear information from *AzsReadinessCheckerReport.json*.</span><span class="sxs-lookup"><span data-stu-id="c933a-146">Use the **-CleanReport** parameter at the end of the run command to clear information from *AzsReadinessCheckerReport.json*.</span></span>  <span data-ttu-id="c933a-147">about previous runs of the tool.</span><span class="sxs-lookup"><span data-stu-id="c933a-147">about previous runs of the tool.</span></span> 

<span data-ttu-id="c933a-148">For more information, [Azure Stack validation report](azure-stack-validation-report.md).</span><span class="sxs-lookup"><span data-stu-id="c933a-148">For more information, [Azure Stack validation report](azure-stack-validation-report.md).</span></span>

## <a name="validation-failures"></a><span data-ttu-id="c933a-149">Validation failures</span><span class="sxs-lookup"><span data-stu-id="c933a-149">Validation failures</span></span>
<span data-ttu-id="c933a-150">If a validation check fails, details about the failure display in the PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="c933a-150">If a validation check fails, details about the failure display in the PowerShell window.</span></span> <span data-ttu-id="c933a-151">The tool also logs information to the AzsReadinessChecker.log.</span><span class="sxs-lookup"><span data-stu-id="c933a-151">The tool also logs information to the AzsReadinessChecker.log.</span></span>

<span data-ttu-id="c933a-152">The following examples provide guidance on common validation failures.</span><span class="sxs-lookup"><span data-stu-id="c933a-152">The following examples provide guidance on common validation failures.</span></span>

### <a name="expired-or-temporary-password"></a><span data-ttu-id="c933a-153">Expired or temporary password</span><span class="sxs-lookup"><span data-stu-id="c933a-153">Expired or temporary password</span></span> 
 
<span data-ttu-id="c933a-154">![expired password](./media/azure-stack-validate-identity/expired-password.png)
**Cause** - The account can’t log on because the password is either expired or is temporary.</span><span class="sxs-lookup"><span data-stu-id="c933a-154">![expired password](./media/azure-stack-validate-identity/expired-password.png)
**Cause** - The account can’t log on because the password is either expired or is temporary.</span></span>     

<span data-ttu-id="c933a-155">**Resolution** - In PowerShell run the following, and then follow the prompts to reset the password.</span><span class="sxs-lookup"><span data-stu-id="c933a-155">**Resolution** - In PowerShell run the following, and then follow the prompts to reset the password.</span></span>  
> `Login-AzureRMAccount`

<span data-ttu-id="c933a-156">Alternatively, login into https://portal.azure.com as the account and the user will be forced to change the password.</span><span class="sxs-lookup"><span data-stu-id="c933a-156">Alternatively, login into https://portal.azure.com as the account and the user will be forced to change the password.</span></span>
### <a name="unknown-user-type"></a><span data-ttu-id="c933a-157">Unknown user type</span><span class="sxs-lookup"><span data-stu-id="c933a-157">Unknown user type</span></span> 
 
<span data-ttu-id="c933a-158">![unknown user](./media/azure-stack-validate-identity/unknown-user.png)
**Cause** - The account can’t log on to the specified Azure Active Directory (AADDirectoryTenantName).</span><span class="sxs-lookup"><span data-stu-id="c933a-158">![unknown user](./media/azure-stack-validate-identity/unknown-user.png)
**Cause** - The account can’t log on to the specified Azure Active Directory (AADDirectoryTenantName).</span></span> <span data-ttu-id="c933a-159">In this example, *AzureChinaCloud* is specified as the *AzureEnvironment*.</span><span class="sxs-lookup"><span data-stu-id="c933a-159">In this example, *AzureChinaCloud* is specified as the *AzureEnvironment*.</span></span>

<span data-ttu-id="c933a-160">**Resolution** - Confirm that the account is valid for the specified Azure Environment.</span><span class="sxs-lookup"><span data-stu-id="c933a-160">**Resolution** - Confirm that the account is valid for the specified Azure Environment.</span></span> <span data-ttu-id="c933a-161">In PowerShell, run the following to verify the account is valid for a specific environment:   Login-AzureRmAccount – EnvironmentName AzureChinaCloud</span><span class="sxs-lookup"><span data-stu-id="c933a-161">In PowerShell, run the following to verify the account is valid for a specific environment:   Login-AzureRmAccount – EnvironmentName AzureChinaCloud</span></span> 
### <a name="account-is-not-an-administrator"></a><span data-ttu-id="c933a-162">Account is not an administrator</span><span class="sxs-lookup"><span data-stu-id="c933a-162">Account is not an administrator</span></span> 
 
![not administrator](./media/azure-stack-validate-identity/not-admin.png)

<span data-ttu-id="c933a-164">**Cause** -  Although the account can successfully log on, the account is not an admin of the Azure Active Directory (AADDirectoryTenantName).</span><span class="sxs-lookup"><span data-stu-id="c933a-164">**Cause** -  Although the account can successfully log on, the account is not an admin of the Azure Active Directory (AADDirectoryTenantName).</span></span>  

<span data-ttu-id="c933a-165">**Resolution** - Login into https://portal.azure.com as the account, go to **Azure Active Directory** > **Users** > *Select the User* > **Directory Role**, and then ensure the user is a **Global administrator**.</span><span class="sxs-lookup"><span data-stu-id="c933a-165">**Resolution** - Login into https://portal.azure.com as the account, go to **Azure Active Directory** > **Users** > *Select the User* > **Directory Role**, and then ensure the user is a **Global administrator**.</span></span>  <span data-ttu-id="c933a-166">If the account is a User, go to **Azure Active Directory** > **Custom domain** names, and confirm that the name you supplied for *AADDirectoryTenantName* is marked as the primary domain name for this directory.</span><span class="sxs-lookup"><span data-stu-id="c933a-166">If the account is a User, go to **Azure Active Directory** > **Custom domain** names, and confirm that the name you supplied for *AADDirectoryTenantName* is marked as the primary domain name for this directory.</span></span>  <span data-ttu-id="c933a-167">In this example, that is *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="c933a-167">In this example, that is *contoso.onmicrosoft.com*.</span></span> 

<span data-ttu-id="c933a-168">Azure Stack requires that the domain name is the primary domain name.</span><span class="sxs-lookup"><span data-stu-id="c933a-168">Azure Stack requires that the domain name is the primary domain name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c933a-169">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c933a-169">Next Steps</span></span>
[<span data-ttu-id="c933a-170">Validate Azure registration</span><span class="sxs-lookup"><span data-stu-id="c933a-170">Validate Azure registration</span></span>](azure-stack-validate-registration.md)  
[<span data-ttu-id="c933a-171">View the readiness report</span><span class="sxs-lookup"><span data-stu-id="c933a-171">View the readiness report</span></span>](azure-stack-validation-report.md)  
[<span data-ttu-id="c933a-172">General Azure Stack integration considerations</span><span class="sxs-lookup"><span data-stu-id="c933a-172">General Azure Stack integration considerations</span></span>](azure-stack-datacenter-integration.md)  

