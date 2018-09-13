---
title: 'Azure Active Directory Domain Services: Troubleshooting Guide | Microsoft Docs'
description: Troubleshooting guide for Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d6695b0c40f56093e8701dfe6394143268114453
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549372"
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a><span data-ttu-id="fe37d-103">Azure AD Domain Services - Troubleshooting guide</span><span class="sxs-lookup"><span data-stu-id="fe37d-103">Azure AD Domain Services - Troubleshooting guide</span></span>
<span data-ttu-id="fe37d-104">This article provides troubleshooting hints for issues you may encounter when setting up or administering Azure Active Directory (AD) Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-104">This article provides troubleshooting hints for issues you may encounter when setting up or administering Azure Active Directory (AD) Domain Services.</span></span>

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a><span data-ttu-id="fe37d-105">You cannot enable Azure AD Domain Services for your Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="fe37d-105">You cannot enable Azure AD Domain Services for your Azure AD directory</span></span>
<span data-ttu-id="fe37d-106">This section helps you troubleshoot errors when you try to enable Azure AD Domain Services for your directory and it fails or gets toggled back to 'Disabled'.</span><span class="sxs-lookup"><span data-stu-id="fe37d-106">This section helps you troubleshoot errors when you try to enable Azure AD Domain Services for your directory and it fails or gets toggled back to 'Disabled'.</span></span>

<span data-ttu-id="fe37d-107">Pick the troubleshooting steps that correspond to the error message you encounter.</span><span class="sxs-lookup"><span data-stu-id="fe37d-107">Pick the troubleshooting steps that correspond to the error message you encounter.</span></span>

| <span data-ttu-id="fe37d-108">**Error Message**</span><span class="sxs-lookup"><span data-stu-id="fe37d-108">**Error Message**</span></span> | <span data-ttu-id="fe37d-109">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="fe37d-109">**Resolution**</span></span> |
| --- |:--- |
| <span data-ttu-id="fe37d-110">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span><span class="sxs-lookup"><span data-stu-id="fe37d-110">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span> |[<span data-ttu-id="fe37d-111">Domain name conflict in the virtual network</span><span class="sxs-lookup"><span data-stu-id="fe37d-111">Domain name conflict in the virtual network</span></span>](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| <span data-ttu-id="fe37d-112">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span><span class="sxs-lookup"><span data-stu-id="fe37d-112">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="fe37d-113">Domain Services does not have adequate permissions to the Azure AD Domain Services Sync application</span><span class="sxs-lookup"><span data-stu-id="fe37d-113">Domain Services does not have adequate permissions to the Azure AD Domain Services Sync application</span></span>](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| <span data-ttu-id="fe37d-114">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span><span class="sxs-lookup"><span data-stu-id="fe37d-114">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="fe37d-115">The Domain Services application is not configured properly in your tenant</span><span class="sxs-lookup"><span data-stu-id="fe37d-115">The Domain Services application is not configured properly in your tenant</span></span>](active-directory-ds-troubleshooting.md#invalid-configuration) |
| <span data-ttu-id="fe37d-116">*Domain Services could not be enabled in this Azure AD tenant. The Microsoft Azure AD application is disabled in your Azure AD tenant. Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.*</span><span class="sxs-lookup"><span data-stu-id="fe37d-116">*Domain Services could not be enabled in this Azure AD tenant. The Microsoft Azure AD application is disabled in your Azure AD tenant. Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.*</span></span> |[<span data-ttu-id="fe37d-117">The Microsoft Graph application is disabled in your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="fe37d-117">The Microsoft Graph application is disabled in your Azure AD tenant</span></span>](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a><span data-ttu-id="fe37d-118">Domain Name conflict</span><span class="sxs-lookup"><span data-stu-id="fe37d-118">Domain Name conflict</span></span>
<span data-ttu-id="fe37d-119">**Error message:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-119">**Error message:**</span></span>

<span data-ttu-id="fe37d-120">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span><span class="sxs-lookup"><span data-stu-id="fe37d-120">*The name contoso100.com is already in use on this network. Specify a name that is not in use.*</span></span>

<span data-ttu-id="fe37d-121">**Remediation:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-121">**Remediation:**</span></span>

<span data-ttu-id="fe37d-122">Ensure that you do not have an existing domain with the same domain name available on that virtual network.</span><span class="sxs-lookup"><span data-stu-id="fe37d-122">Ensure that you do not have an existing domain with the same domain name available on that virtual network.</span></span> <span data-ttu-id="fe37d-123">For instance, assume you have a domain called 'contoso.com' already available on the selected virtual network.</span><span class="sxs-lookup"><span data-stu-id="fe37d-123">For instance, assume you have a domain called 'contoso.com' already available on the selected virtual network.</span></span> <span data-ttu-id="fe37d-124">Later, you try to enable an Azure AD Domain Services managed domain with the same domain name (that is, 'contoso.com') on that virtual network.</span><span class="sxs-lookup"><span data-stu-id="fe37d-124">Later, you try to enable an Azure AD Domain Services managed domain with the same domain name (that is, 'contoso.com') on that virtual network.</span></span> <span data-ttu-id="fe37d-125">You encounter a failure when trying to enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-125">You encounter a failure when trying to enable Azure AD Domain Services.</span></span>

<span data-ttu-id="fe37d-126">This failure is due to name conflicts for the domain name on that virtual network.</span><span class="sxs-lookup"><span data-stu-id="fe37d-126">This failure is due to name conflicts for the domain name on that virtual network.</span></span> <span data-ttu-id="fe37d-127">In this situation, you must use a different name to set up your Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="fe37d-127">In this situation, you must use a different name to set up your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="fe37d-128">Alternately, you can de-provision the existing domain and then proceed to enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-128">Alternately, you can de-provision the existing domain and then proceed to enable Azure AD Domain Services.</span></span>

### <a name="inadequate-permissions"></a><span data-ttu-id="fe37d-129">Inadequate permissions</span><span class="sxs-lookup"><span data-stu-id="fe37d-129">Inadequate permissions</span></span>
<span data-ttu-id="fe37d-130">**Error message:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-130">**Error message:**</span></span>

<span data-ttu-id="fe37d-131">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span><span class="sxs-lookup"><span data-stu-id="fe37d-131">*Domain Services could not be enabled in this Azure AD tenant. The service does not have adequate permissions to the application called 'Azure AD Domain Services Sync'. Delete the application called 'Azure AD Domain Services Sync' and then try to enable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="fe37d-132">**Remediation:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-132">**Remediation:**</span></span>

<span data-ttu-id="fe37d-133">Check to see if there is an application with the name 'Azure AD Domain Services Sync' in your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="fe37d-133">Check to see if there is an application with the name 'Azure AD Domain Services Sync' in your Azure AD directory.</span></span> <span data-ttu-id="fe37d-134">If this application exists, delete it and then re-enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-134">If this application exists, delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="fe37d-135">Perform the following steps to check for the presence of the application and to delete it, if the application exists:</span><span class="sxs-lookup"><span data-stu-id="fe37d-135">Perform the following steps to check for the presence of the application and to delete it, if the application exists:</span></span>

1. <span data-ttu-id="fe37d-136">Navigate to the **Azure classic portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="fe37d-136">Navigate to the **Azure classic portal** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).</span></span>
2. <span data-ttu-id="fe37d-137">Select the **Active Directory** node on the left pane.</span><span class="sxs-lookup"><span data-stu-id="fe37d-137">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="fe37d-138">Select the Azure AD tenant (directory) for which you would like to enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-138">Select the Azure AD tenant (directory) for which you would like to enable Azure AD Domain Services.</span></span>
4. <span data-ttu-id="fe37d-139">Navigate to the **Applications** tab.</span><span class="sxs-lookup"><span data-stu-id="fe37d-139">Navigate to the **Applications** tab.</span></span>
5. <span data-ttu-id="fe37d-140">Select the **Applications my company owns** option in the dropdown.</span><span class="sxs-lookup"><span data-stu-id="fe37d-140">Select the **Applications my company owns** option in the dropdown.</span></span>
6. <span data-ttu-id="fe37d-141">Check for an application called **Azure AD Domain Services Sync**. If the application exists, proceed to delete it.</span><span class="sxs-lookup"><span data-stu-id="fe37d-141">Check for an application called **Azure AD Domain Services Sync**. If the application exists, proceed to delete it.</span></span>
7. <span data-ttu-id="fe37d-142">Once you have deleted the application, try to enable Azure AD Domain Services once again.</span><span class="sxs-lookup"><span data-stu-id="fe37d-142">Once you have deleted the application, try to enable Azure AD Domain Services once again.</span></span>

### <a name="invalid-configuration"></a><span data-ttu-id="fe37d-143">Invalid configuration</span><span class="sxs-lookup"><span data-stu-id="fe37d-143">Invalid configuration</span></span>
<span data-ttu-id="fe37d-144">**Error message:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-144">**Error message:**</span></span>

<span data-ttu-id="fe37d-145">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span><span class="sxs-lookup"><span data-stu-id="fe37d-145">*Domain Services could not be enabled in this Azure AD tenant. The Domain Services application in your Azure AD tenant does not have the required permissions to enable Domain Services. Delete the application with the application identifier d87dcbc6-a371-462e-88e3-28ad15ec4e64 and then try to enable Domain Services for your Azure AD tenant.*</span></span>

<span data-ttu-id="fe37d-146">**Remediation:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-146">**Remediation:**</span></span>

<span data-ttu-id="fe37d-147">Check to see if you have an application with the name 'AzureActiveDirectoryDomainControllerServices' (with an application identifier of d87dcbc6-a371-462e-88e3-28ad15ec4e64) in your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="fe37d-147">Check to see if you have an application with the name 'AzureActiveDirectoryDomainControllerServices' (with an application identifier of d87dcbc6-a371-462e-88e3-28ad15ec4e64) in your Azure AD directory.</span></span> <span data-ttu-id="fe37d-148">If this application exists, you need to delete it and then re-enable Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-148">If this application exists, you need to delete it and then re-enable Azure AD Domain Services.</span></span>

<span data-ttu-id="fe37d-149">Use the following PowerShell script to find the application and delete it.</span><span class="sxs-lookup"><span data-stu-id="fe37d-149">Use the following PowerShell script to find the application and delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="fe37d-150">This script uses **Azure AD PowerShell version 2** cmdlets.</span><span class="sxs-lookup"><span data-stu-id="fe37d-150">This script uses **Azure AD PowerShell version 2** cmdlets.</span></span> <span data-ttu-id="fe37d-151">For a full list of all available cmdlets and to download the module, read the [AzureAD PowerShell reference documentation](https://msdn.microsoft.com/library/azure/mt757189.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe37d-151">For a full list of all available cmdlets and to download the module, read the [AzureAD PowerShell reference documentation](https://msdn.microsoft.com/library/azure/mt757189.aspx).</span></span>
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted the Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a><span data-ttu-id="fe37d-152">Microsoft Graph disabled</span><span class="sxs-lookup"><span data-stu-id="fe37d-152">Microsoft Graph disabled</span></span>
<span data-ttu-id="fe37d-153">**Error message:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-153">**Error message:**</span></span>

<span data-ttu-id="fe37d-154">Domain Services could not be enabled in this Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-154">Domain Services could not be enabled in this Azure AD tenant.</span></span> <span data-ttu-id="fe37d-155">The Microsoft Azure AD application is disabled in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-155">The Microsoft Azure AD application is disabled in your Azure AD tenant.</span></span> <span data-ttu-id="fe37d-156">Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-156">Enable the application with the application identifier 00000002-0000-0000-c000-000000000000 and then try to enable Domain Services for your Azure AD tenant.</span></span>

<span data-ttu-id="fe37d-157">**Remediation:**</span><span class="sxs-lookup"><span data-stu-id="fe37d-157">**Remediation:**</span></span>

<span data-ttu-id="fe37d-158">Check to see if you have disabled an application with the identifier 00000002-0000-0000-c000-000000000000.</span><span class="sxs-lookup"><span data-stu-id="fe37d-158">Check to see if you have disabled an application with the identifier 00000002-0000-0000-c000-000000000000.</span></span> <span data-ttu-id="fe37d-159">This application is the Microsoft Azure AD application and provides Graph API access to your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-159">This application is the Microsoft Azure AD application and provides Graph API access to your Azure AD tenant.</span></span> <span data-ttu-id="fe37d-160">Azure AD Domain Services needs this application to be enabled to synchronize your Azure AD tenant to your managed domain.</span><span class="sxs-lookup"><span data-stu-id="fe37d-160">Azure AD Domain Services needs this application to be enabled to synchronize your Azure AD tenant to your managed domain.</span></span>

<span data-ttu-id="fe37d-161">To resolve this error, enable this application and then try to enable Domain Services for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-161">To resolve this error, enable this application and then try to enable Domain Services for your Azure AD tenant.</span></span>

## <a name="users-are-unable-to-sign-in-to-the-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="fe37d-162">Users are unable to sign in to the Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="fe37d-162">Users are unable to sign in to the Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="fe37d-163">If one or more users in your Azure AD tenant are unable to sign in to the newly created managed domain, perform the following troubleshooting steps:</span><span class="sxs-lookup"><span data-stu-id="fe37d-163">If one or more users in your Azure AD tenant are unable to sign in to the newly created managed domain, perform the following troubleshooting steps:</span></span>

* <span data-ttu-id="fe37d-164">**Sign-in using UPN format:** Try to sign in using the UPN format (for example, 'joeuser@contoso.com') instead of the SAMAccountName format ('CONTOSO\joeuser').</span><span class="sxs-lookup"><span data-stu-id="fe37d-164">**Sign-in using UPN format:** Try to sign in using the UPN format (for example, 'joeuser@contoso.com') instead of the SAMAccountName format ('CONTOSO\joeuser').</span></span> <span data-ttu-id="fe37d-165">The SAMAccountName may be automatically generated for users whose UPN prefix is overly long or is the same as another user on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="fe37d-165">The SAMAccountName may be automatically generated for users whose UPN prefix is overly long or is the same as another user on the managed domain.</span></span> <span data-ttu-id="fe37d-166">The UPN format is guaranteed to be unique within an Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-166">The UPN format is guaranteed to be unique within an Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="fe37d-167">We recommend using the UPN format to sign in to the Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="fe37d-167">We recommend using the UPN format to sign in to the Azure AD Domain Services managed domain.</span></span>
>
>

* <span data-ttu-id="fe37d-168">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span><span class="sxs-lookup"><span data-stu-id="fe37d-168">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span></span>
* <span data-ttu-id="fe37d-169">**External accounts:** Ensure that the affected user account is not an external account in the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-169">**External accounts:** Ensure that the affected user account is not an external account in the Azure AD tenant.</span></span> <span data-ttu-id="fe37d-170">Examples of external accounts include Microsoft accounts (for example, 'joe@live.com') or user accounts from an external Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="fe37d-170">Examples of external accounts include Microsoft accounts (for example, 'joe@live.com') or user accounts from an external Azure AD directory.</span></span> <span data-ttu-id="fe37d-171">Since Azure AD Domain Services does not have credentials for such user accounts, these users cannot sign in to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="fe37d-171">Since Azure AD Domain Services does not have credentials for such user accounts, these users cannot sign in to the managed domain.</span></span>
* <span data-ttu-id="fe37d-172">**Synced accounts:** If the affected user accounts are synchronized from an on-premises directory, verify that:</span><span class="sxs-lookup"><span data-stu-id="fe37d-172">**Synced accounts:** If the affected user accounts are synchronized from an on-premises directory, verify that:</span></span>

  * <span data-ttu-id="fe37d-173">You have deployed or updated to the [latest recommended release of Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).</span><span class="sxs-lookup"><span data-stu-id="fe37d-173">You have deployed or updated to the [latest recommended release of Azure AD Connect](https://www.microsoft.com/en-us/download/details.aspx?id=47594).</span></span>
  * <span data-ttu-id="fe37d-174">You have configured Azure AD Connect to [perform a full synchronization](active-directory-ds-getting-started-password-sync.md).</span><span class="sxs-lookup"><span data-stu-id="fe37d-174">You have configured Azure AD Connect to [perform a full synchronization](active-directory-ds-getting-started-password-sync.md).</span></span>
  * <span data-ttu-id="fe37d-175">Depending on the size of your directory, it may take a while for user accounts and credential hashes to be available in Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-175">Depending on the size of your directory, it may take a while for user accounts and credential hashes to be available in Azure AD Domain Services.</span></span> <span data-ttu-id="fe37d-176">Ensure you wait long enough before retrying authentication (depending on the size of your directory - a few hours to a day or two for large directories).</span><span class="sxs-lookup"><span data-stu-id="fe37d-176">Ensure you wait long enough before retrying authentication (depending on the size of your directory - a few hours to a day or two for large directories).</span></span>
  * <span data-ttu-id="fe37d-177">If the issue persists after verifying the preceding steps, try restarting the Microsoft Azure AD Sync Service.</span><span class="sxs-lookup"><span data-stu-id="fe37d-177">If the issue persists after verifying the preceding steps, try restarting the Microsoft Azure AD Sync Service.</span></span> <span data-ttu-id="fe37d-178">From your sync machine, launch a command prompt and execute the following commands:</span><span class="sxs-lookup"><span data-stu-id="fe37d-178">From your sync machine, launch a command prompt and execute the following commands:</span></span>

    1. <span data-ttu-id="fe37d-179">net stop 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="fe37d-179">net stop 'Microsoft Azure AD Sync'</span></span>
    2. <span data-ttu-id="fe37d-180">net start 'Microsoft Azure AD Sync'</span><span class="sxs-lookup"><span data-stu-id="fe37d-180">net start 'Microsoft Azure AD Sync'</span></span>
* <span data-ttu-id="fe37d-181">**Cloud-only accounts**: If the affected user account is a cloud-only user account, ensure that the user has changed their password after you enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fe37d-181">**Cloud-only accounts**: If the affected user account is a cloud-only user account, ensure that the user has changed their password after you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="fe37d-182">This step causes the credential hashes required for Azure AD Domain Services to be generated.</span><span class="sxs-lookup"><span data-stu-id="fe37d-182">This step causes the credential hashes required for Azure AD Domain Services to be generated.</span></span>

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a><span data-ttu-id="fe37d-183">Users removed from your Azure AD tenant are not removed from your managed domain</span><span class="sxs-lookup"><span data-stu-id="fe37d-183">Users removed from your Azure AD tenant are not removed from your managed domain</span></span>
<span data-ttu-id="fe37d-184">Azure AD protects you from accidental deletion of user objects.</span><span class="sxs-lookup"><span data-stu-id="fe37d-184">Azure AD protects you from accidental deletion of user objects.</span></span> <span data-ttu-id="fe37d-185">When you delete a user account from your Azure AD tenant, the corresponding user object is moved to the Recycle Bin.</span><span class="sxs-lookup"><span data-stu-id="fe37d-185">When you delete a user account from your Azure AD tenant, the corresponding user object is moved to the Recycle Bin.</span></span> <span data-ttu-id="fe37d-186">When this delete operation is synchronized to your managed domain, it causes the corresponding user account to be marked disabled.</span><span class="sxs-lookup"><span data-stu-id="fe37d-186">When this delete operation is synchronized to your managed domain, it causes the corresponding user account to be marked disabled.</span></span> <span data-ttu-id="fe37d-187">This feature helps you recover or undelete the user account later.</span><span class="sxs-lookup"><span data-stu-id="fe37d-187">This feature helps you recover or undelete the user account later.</span></span>

<span data-ttu-id="fe37d-188">The user account remains in the disabled state in your managed domain, even if you re-create a user account with the same UPN in your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="fe37d-188">The user account remains in the disabled state in your managed domain, even if you re-create a user account with the same UPN in your Azure AD directory.</span></span> <span data-ttu-id="fe37d-189">To remove the user account from your managed domain, you need to force delete it from your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-189">To remove the user account from your managed domain, you need to force delete it from your Azure AD tenant.</span></span>

<span data-ttu-id="fe37d-190">To remove the user account fully from your managed domain, delete the user permanently from your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="fe37d-190">To remove the user account fully from your managed domain, delete the user permanently from your Azure AD tenant.</span></span> <span data-ttu-id="fe37d-191">Use the Remove-MsolUser PowerShell cmdlet with the '-RemoveFromRecycleBin' option, as described in this [MSDN article](https://msdn.microsoft.com/library/azure/dn194132.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe37d-191">Use the Remove-MsolUser PowerShell cmdlet with the '-RemoveFromRecycleBin' option, as described in this [MSDN article](https://msdn.microsoft.com/library/azure/dn194132.aspx).</span></span>

## <a name="contact-us"></a><span data-ttu-id="fe37d-192">Contact Us</span><span class="sxs-lookup"><span data-stu-id="fe37d-192">Contact Us</span></span>
<span data-ttu-id="fe37d-193">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span><span class="sxs-lookup"><span data-stu-id="fe37d-193">Contact the Azure Active Directory Domain Services product team to [share feedback or for support](active-directory-ds-contact-us.md).</span></span>
