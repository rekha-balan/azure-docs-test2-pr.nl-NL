---
title: 'Azure Active Directory Domain Services: Troubleshooting Service Principal configuration| Microsoft Docs'
description: Troubleshooting Service Principal configuration for Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: eringreenlee
manager: ''
editor: ''
ms.assetid: f168870c-b43a-4dd6-a13f-5cfadc5edf2c
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/12/2018
ms.author: ergreenl
ms.openlocfilehash: 5bc1212cc6e894cd82a60abb42f92893c0bb2d43
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966456"
---
# <a name="troubleshoot-invalid-service-principal-configuration-for-your-managed-domain"></a><span data-ttu-id="f2e3d-103">Troubleshoot invalid Service Principal configuration for your managed domain</span><span class="sxs-lookup"><span data-stu-id="f2e3d-103">Troubleshoot invalid Service Principal configuration for your managed domain</span></span>

<span data-ttu-id="f2e3d-104">This article helps you troubleshoot and resolve service principal-related configuration errors that result in the following alert message:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-104">This article helps you troubleshoot and resolve service principal-related configuration errors that result in the following alert message:</span></span>

## <a name="alert-aadds102-service-principal-not-found"></a><span data-ttu-id="f2e3d-105">Alert AADDS102: Service Principal not found</span><span class="sxs-lookup"><span data-stu-id="f2e3d-105">Alert AADDS102: Service Principal not found</span></span>

<span data-ttu-id="f2e3d-106">**Alert message:** *A Service Principal required for Azure AD Domain Services to function properly has been deleted from your Azure AD directory. This configuration impacts Microsoft's ability to monitor, manage, patch, and synchronize your managed domain.*</span><span class="sxs-lookup"><span data-stu-id="f2e3d-106">**Alert message:** *A Service Principal required for Azure AD Domain Services to function properly has been deleted from your Azure AD directory. This configuration impacts Microsoft's ability to monitor, manage, patch, and synchronize your managed domain.*</span></span>

<span data-ttu-id="f2e3d-107">[Service principals](../active-directory/develop/app-objects-and-service-principals.md) are applications that Microsoft uses to manage, update, and maintain your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-107">[Service principals](../active-directory/develop/app-objects-and-service-principals.md) are applications that Microsoft uses to manage, update, and maintain your managed domain.</span></span> <span data-ttu-id="f2e3d-108">If they are deleted, it breaks Microsoft's ability to service your domain.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-108">If they are deleted, it breaks Microsoft's ability to service your domain.</span></span>


## <a name="check-for-missing-service-principals"></a><span data-ttu-id="f2e3d-109">Check for missing service principals</span><span class="sxs-lookup"><span data-stu-id="f2e3d-109">Check for missing service principals</span></span>
<span data-ttu-id="f2e3d-110">Use the following steps to determine which service principals need to be recreated:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-110">Use the following steps to determine which service principals need to be recreated:</span></span>

1. <span data-ttu-id="f2e3d-111">Navigate to the [Enterprise Applications - All Applications](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps) page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-111">Navigate to the [Enterprise Applications - All Applications](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps) page in the Azure portal.</span></span>
2. <span data-ttu-id="f2e3d-112">In the **Show** dropdown, select **All Applications** and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-112">In the **Show** dropdown, select **All Applications** and click **Apply**.</span></span>
3. <span data-ttu-id="f2e3d-113">Using the following table, search for each application ID by pasting the ID into the search box and pressing enter.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-113">Using the following table, search for each application ID by pasting the ID into the search box and pressing enter.</span></span> <span data-ttu-id="f2e3d-114">If the search results are empty, you must recreate the service principal by following the steps in the "resolution" column.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-114">If the search results are empty, you must recreate the service principal by following the steps in the "resolution" column.</span></span>

| <span data-ttu-id="f2e3d-115">Application ID</span><span class="sxs-lookup"><span data-stu-id="f2e3d-115">Application ID</span></span> | <span data-ttu-id="f2e3d-116">Resolution</span><span class="sxs-lookup"><span data-stu-id="f2e3d-116">Resolution</span></span> |
| :--- | :--- | :--- |
| <span data-ttu-id="f2e3d-117">2565bd9d-da50-47d4-8b85-4c97f669dc36</span><span class="sxs-lookup"><span data-stu-id="f2e3d-117">2565bd9d-da50-47d4-8b85-4c97f669dc36</span></span> | [<span data-ttu-id="f2e3d-118">Recreate a missing service principal with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2e3d-118">Recreate a missing service principal with PowerShell</span></span>](#recreate-a-missing-service-principal-with-powershell) |
| <span data-ttu-id="f2e3d-119">443155a6-77f3-45e3-882b-22b3a8d431fb</span><span class="sxs-lookup"><span data-stu-id="f2e3d-119">443155a6-77f3-45e3-882b-22b3a8d431fb</span></span> | [<span data-ttu-id="f2e3d-120">Re-register to the Microsoft.AAD namespace</span><span class="sxs-lookup"><span data-stu-id="f2e3d-120">Re-register to the Microsoft.AAD namespace</span></span>](#re-register-to-the-microsoft-aad-namespace-using-the-azure-portal) |
| <span data-ttu-id="f2e3d-121">abba844e-bc0e-44b0-947a-dc74e5d09022</span><span class="sxs-lookup"><span data-stu-id="f2e3d-121">abba844e-bc0e-44b0-947a-dc74e5d09022</span></span>  | [<span data-ttu-id="f2e3d-122">Re-register to the Microsoft.AAD namespace</span><span class="sxs-lookup"><span data-stu-id="f2e3d-122">Re-register to the Microsoft.AAD namespace</span></span>](#re-register-to-the-microsoft-aad-namespace-using-the-azure-portal) |
| <span data-ttu-id="f2e3d-123">d87dcbc6-a371-462e-88e3-28ad15ec4e64</span><span class="sxs-lookup"><span data-stu-id="f2e3d-123">d87dcbc6-a371-462e-88e3-28ad15ec4e64</span></span> | [<span data-ttu-id="f2e3d-124">Service principals that self correct</span><span class="sxs-lookup"><span data-stu-id="f2e3d-124">Service principals that self correct</span></span>](#service-principals-that-self-correct) |

## <a name="recreate-a-missing-service-principal-with-powershell"></a><span data-ttu-id="f2e3d-125">Recreate a missing Service Principal with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2e3d-125">Recreate a missing Service Principal with PowerShell</span></span>
<span data-ttu-id="f2e3d-126">Follow these steps if a service principal with the ID ```2565bd9d-da50-47d4-8b85-4c97f669dc36``` is missing from your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-126">Follow these steps if a service principal with the ID ```2565bd9d-da50-47d4-8b85-4c97f669dc36``` is missing from your Azure AD directory.</span></span>

<span data-ttu-id="f2e3d-127">**Resolution:** You need Azure AD PowerShell to complete these steps.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-127">**Resolution:** You need Azure AD PowerShell to complete these steps.</span></span> <span data-ttu-id="f2e3d-128">For information on installing Azure AD PowerShell, see [this article](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0.).</span><span class="sxs-lookup"><span data-stu-id="f2e3d-128">For information on installing Azure AD PowerShell, see [this article](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0.).</span></span>

<span data-ttu-id="f2e3d-129">To address this issue, type the following commands in a PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-129">To address this issue, type the following commands in a PowerShell window:</span></span>
1. <span data-ttu-id="f2e3d-130">Install the Azure AD PowerShell module and import it.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-130">Install the Azure AD PowerShell module and import it.</span></span>

    ```powershell
    Install-Module AzureAD
    Import-Module AzureAD
    ```

2. <span data-ttu-id="f2e3d-131">Check whether the service principal required for Azure AD Domain Services is missing in your directory by executing the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-131">Check whether the service principal required for Azure AD Domain Services is missing in your directory by executing the following PowerShell command:</span></span>

    ```powershell
    Get-AzureAdServicePrincipal -filter "AppId eq '2565bd9d-da50-47d4-8b85-4c97f669dc36'"
    ```

3. <span data-ttu-id="f2e3d-132">Create the service principal by typing the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-132">Create the service principal by typing the following PowerShell command:</span></span>

    ```powershell
    New-AzureAdServicePrincipal -AppId "2565bd9d-da50-47d4-8b85-4c97f669dc36"
    ```

4. <span data-ttu-id="f2e3d-133">After you have created the missing service principal, wait two hours and check your managed domain's health.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-133">After you have created the missing service principal, wait two hours and check your managed domain's health.</span></span>


## <a name="re-register-to-the-microsoft-aad-namespace-using-the-azure-portal"></a><span data-ttu-id="f2e3d-134">Re-register to the Microsoft AAD namespace using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f2e3d-134">Re-register to the Microsoft AAD namespace using the Azure portal</span></span>
<span data-ttu-id="f2e3d-135">Follow these steps if a service principal with the ID ```443155a6-77f3-45e3-882b-22b3a8d431fb``` or ```abba844e-bc0e-44b0-947a-dc74e5d09022``` is missing from your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-135">Follow these steps if a service principal with the ID ```443155a6-77f3-45e3-882b-22b3a8d431fb``` or ```abba844e-bc0e-44b0-947a-dc74e5d09022``` is missing from your Azure AD directory.</span></span>

<span data-ttu-id="f2e3d-136">**Resolution:** Use the following steps to restore Domain Services on your directory:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-136">**Resolution:** Use the following steps to restore Domain Services on your directory:</span></span>

1. <span data-ttu-id="f2e3d-137">Navigate to the [Subscriptions](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) page in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-137">Navigate to the [Subscriptions](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) page in the Azure portal.</span></span>
2. <span data-ttu-id="f2e3d-138">Choose the subscription from the table that is associated with your managed domain</span><span class="sxs-lookup"><span data-stu-id="f2e3d-138">Choose the subscription from the table that is associated with your managed domain</span></span>
3. <span data-ttu-id="f2e3d-139">Using the left-hand navigation, choose **Resource Providers**</span><span class="sxs-lookup"><span data-stu-id="f2e3d-139">Using the left-hand navigation, choose **Resource Providers**</span></span>
4. <span data-ttu-id="f2e3d-140">Search for "Microsoft.AAD" in the table and click **Re-register**</span><span class="sxs-lookup"><span data-stu-id="f2e3d-140">Search for "Microsoft.AAD" in the table and click **Re-register**</span></span>
5. <span data-ttu-id="f2e3d-141">To ensure the alert is resolved, view the health page for your managed domain in two hours.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-141">To ensure the alert is resolved, view the health page for your managed domain in two hours.</span></span>


## <a name="service-principals-that-self-correct"></a><span data-ttu-id="f2e3d-142">Service Principals that self correct</span><span class="sxs-lookup"><span data-stu-id="f2e3d-142">Service Principals that self correct</span></span>
<span data-ttu-id="f2e3d-143">Follow these steps if a service principal with the ID ```d87dcbc6-a371-462e-88e3-28ad15ec4e64``` is missing from your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-143">Follow these steps if a service principal with the ID ```d87dcbc6-a371-462e-88e3-28ad15ec4e64``` is missing from your Azure AD directory.</span></span>

<span data-ttu-id="f2e3d-144">**Resolution:** Azure AD Domain Services can detect when this specific service principal is missing, misconfigured, or deleted.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-144">**Resolution:** Azure AD Domain Services can detect when this specific service principal is missing, misconfigured, or deleted.</span></span> <span data-ttu-id="f2e3d-145">The service automatically recreates this service principal.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-145">The service automatically recreates this service principal.</span></span> <span data-ttu-id="f2e3d-146">However, you will need to delete the application and object that worked with the deleted application, as when the certification rolls over, the application and object will no longer be able to be modified by the new service principal.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-146">However, you will need to delete the application and object that worked with the deleted application, as when the certification rolls over, the application and object will no longer be able to be modified by the new service principal.</span></span> <span data-ttu-id="f2e3d-147">This will lead to a new error on your domain.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-147">This will lead to a new error on your domain.</span></span> <span data-ttu-id="f2e3d-148">Follow the steps outlined in the [section for AADDS105](#alert-aadds105-password-synchronization-application-is-out-of-date) to prevent this problem.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-148">Follow the steps outlined in the [section for AADDS105](#alert-aadds105-password-synchronization-application-is-out-of-date) to prevent this problem.</span></span> <span data-ttu-id="f2e3d-149">After, check your managed domain's health after two hours to ensure that the new service principal has been recreated.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-149">After, check your managed domain's health after two hours to ensure that the new service principal has been recreated.</span></span>


## <a name="alert-aadds105-password-synchronization-application-is-out-of-date"></a><span data-ttu-id="f2e3d-150">Alert AADDS105: Password synchronization application is out of date</span><span class="sxs-lookup"><span data-stu-id="f2e3d-150">Alert AADDS105: Password synchronization application is out of date</span></span>

<span data-ttu-id="f2e3d-151">**Alert message:** The service principal with the application ID “d87dcbc6-a371-462e-88e3-28ad15ec4e64” was deleted and then recreated.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-151">**Alert message:** The service principal with the application ID “d87dcbc6-a371-462e-88e3-28ad15ec4e64” was deleted and then recreated.</span></span> <span data-ttu-id="f2e3d-152">The recreation leaves behind inconsistent permissions on Azure AD Domain Services resources needed to service your managed domain.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-152">The recreation leaves behind inconsistent permissions on Azure AD Domain Services resources needed to service your managed domain.</span></span> <span data-ttu-id="f2e3d-153">Synchronization of passwords on your managed domain could be affected.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-153">Synchronization of passwords on your managed domain could be affected.</span></span>


<span data-ttu-id="f2e3d-154">**Resolution:** You need Azure AD PowerShell to complete these steps.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-154">**Resolution:** You need Azure AD PowerShell to complete these steps.</span></span> <span data-ttu-id="f2e3d-155">For information on installing Azure AD PowerShell, see [this article](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0.).</span><span class="sxs-lookup"><span data-stu-id="f2e3d-155">For information on installing Azure AD PowerShell, see [this article](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0.).</span></span>

<span data-ttu-id="f2e3d-156">To address this issue, type the following commands in a PowerShell window:</span><span class="sxs-lookup"><span data-stu-id="f2e3d-156">To address this issue, type the following commands in a PowerShell window:</span></span>
1. <span data-ttu-id="f2e3d-157">Install the Azure AD PowerShell module and import it.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-157">Install the Azure AD PowerShell module and import it.</span></span>

    ```powershell
    Install-Module AzureAD
    Import-Module AzureAD
    ```
2. <span data-ttu-id="f2e3d-158">Delete the old application and object using the following PowerShell commands</span><span class="sxs-lookup"><span data-stu-id="f2e3d-158">Delete the old application and object using the following PowerShell commands</span></span>

    ```powershell
    $app = Get-AzureADApplication -Filter "IdentifierUris eq 'https://sync.aaddc.activedirectory.windowsazure.com'"
    Remove-AzureADApplication -ObjectId $app.ObjectId
    $spObject = Get-AzureADServicePrincipal -Filter "DisplayName eq 'Azure AD Domain Services Sync'"
    Remove-AzureADServicePrincipal -ObjectId $app.ObjectId
    ```
3. <span data-ttu-id="f2e3d-159">After you have deleted both, the system will remediate itself and recreate the applications needed for password synchronization.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-159">After you have deleted both, the system will remediate itself and recreate the applications needed for password synchronization.</span></span> <span data-ttu-id="f2e3d-160">To ensure the alert has been remediated, wait two hours and check your domain's health.</span><span class="sxs-lookup"><span data-stu-id="f2e3d-160">To ensure the alert has been remediated, wait two hours and check your domain's health.</span></span>


## <a name="contact-us"></a><span data-ttu-id="f2e3d-161">Contact Us</span><span class="sxs-lookup"><span data-stu-id="f2e3d-161">Contact Us</span></span>
<span data-ttu-id="f2e3d-162">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span><span class="sxs-lookup"><span data-stu-id="f2e3d-162">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span></span>
