---
title: Use existing NPS servers to provide Azure MFA capabilities | Microsoft Docs
description: The Network Policy Server extension for Azure Multi-Factor Authentication is a simple solution to add cloud-based two-step vericiation capabilities to your existing authentication infrastructure.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: ''
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5d0ec19b5e670852a71b39bf44cc5105d58e241a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550270"
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication---public-preview"></a><span data-ttu-id="096ae-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication - Public preview</span><span class="sxs-lookup"><span data-stu-id="096ae-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication - Public preview</span></span>

<span data-ttu-id="096ae-104">The Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities to your authentication infrastructure using your existing servers.</span><span class="sxs-lookup"><span data-stu-id="096ae-104">The Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities to your authentication infrastructure using your existing servers.</span></span> <span data-ttu-id="096ae-105">With the NPS extension, you can add phone call, SMS, or phone app verification to your existing authentication flow without having to install, configure, and maintain new servers.</span><span class="sxs-lookup"><span data-stu-id="096ae-105">With the NPS extension, you can add phone call, SMS, or phone app verification to your existing authentication flow without having to install, configure, and maintain new servers.</span></span> 
 
<span data-ttu-id="096ae-106">When using the NPS extension for Azure MFA, the authentication flow includes the following components:</span><span class="sxs-lookup"><span data-stu-id="096ae-106">When using the NPS extension for Azure MFA, the authentication flow includes the following components:</span></span> 

1. <span data-ttu-id="096ae-107">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests to NPS servers.</span><span class="sxs-lookup"><span data-stu-id="096ae-107">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests to NPS servers.</span></span> 
2. <span data-ttu-id="096ae-108">**NPS Server** connects to Active Directory to perform the primary authentication for the RADIUS requests and, upon success, passes the request to any installed extensions.</span><span class="sxs-lookup"><span data-stu-id="096ae-108">**NPS Server** connects to Active Directory to perform the primary authentication for the RADIUS requests and, upon success, passes the request to any installed extensions.</span></span>  
3. <span data-ttu-id="096ae-109">**NPS Extension** triggers a request to Azure MFA for the secondary authentication.</span><span class="sxs-lookup"><span data-stu-id="096ae-109">**NPS Extension** triggers a request to Azure MFA for the secondary authentication.</span></span> <span data-ttu-id="096ae-110">Once the extension receives the response, and if the MFA challenge succeeds, it completes the authentication request by providing the NPS server with security tokens that include an MFA claim, issued by Azure STS.</span><span class="sxs-lookup"><span data-stu-id="096ae-110">Once the extension receives the response, and if the MFA challenge succeeds, it completes the authentication request by providing the NPS server with security tokens that include an MFA claim, issued by Azure STS.</span></span>  
4. <span data-ttu-id="096ae-111">**Azure MFA** communicates with Azure Active Directory to retrieve the user’s details and performs the secondary authentication using a verification method configured to the user.</span><span class="sxs-lookup"><span data-stu-id="096ae-111">**Azure MFA** communicates with Azure Active Directory to retrieve the user’s details and performs the secondary authentication using a verification method configured to the user.</span></span>

<span data-ttu-id="096ae-112">The following diagram illustrates this high-level authentication request flow:</span><span class="sxs-lookup"><span data-stu-id="096ae-112">The following diagram illustrates this high-level authentication request flow:</span></span> 

![Authentication flow diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a><span data-ttu-id="096ae-114">Plan your deployment</span><span class="sxs-lookup"><span data-stu-id="096ae-114">Plan your deployment</span></span>

<span data-ttu-id="096ae-115">The NPS extension automatically handles redundancy, so you don't need a special configuration.</span><span class="sxs-lookup"><span data-stu-id="096ae-115">The NPS extension automatically handles redundancy, so you don't need a special configuration.</span></span> 

<span data-ttu-id="096ae-116">You can create as many Azure Multi-Factor Authentication enabled NPS servers as you need.</span><span class="sxs-lookup"><span data-stu-id="096ae-116">You can create as many Azure Multi-Factor Authentication enabled NPS servers as you need.</span></span> <span data-ttu-id="096ae-117">If you do install multiple servers, you should use a difference client certificate for each one of them.</span><span class="sxs-lookup"><span data-stu-id="096ae-117">If you do install multiple servers, you should use a difference client certificate for each one of them.</span></span> <span data-ttu-id="096ae-118">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span><span class="sxs-lookup"><span data-stu-id="096ae-118">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span></span> 

<span data-ttu-id="096ae-119">VPN servers route authentication requests, so they need to be aware of the new Azure MFA-enabled NPS servers.</span><span class="sxs-lookup"><span data-stu-id="096ae-119">VPN servers route authentication requests, so they need to be aware of the new Azure MFA-enabled NPS servers.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="096ae-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="096ae-120">Prerequisites</span></span>

<span data-ttu-id="096ae-121">The NPS extension is meant to work with your existing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="096ae-121">The NPS extension is meant to work with your existing infrastructure.</span></span> <span data-ttu-id="096ae-122">Make sure you have the following prerequisites before you begin.</span><span class="sxs-lookup"><span data-stu-id="096ae-122">Make sure you have the following prerequisites before you begin.</span></span>

### <a name="licenses"></a><span data-ttu-id="096ae-123">Licenses</span><span class="sxs-lookup"><span data-stu-id="096ae-123">Licenses</span></span>

<span data-ttu-id="096ae-124">The NPS Extension for Azure MFA is available to customers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA subscription).</span><span class="sxs-lookup"><span data-stu-id="096ae-124">The NPS Extension for Azure MFA is available to customers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA subscription).</span></span>

### <a name="software"></a><span data-ttu-id="096ae-125">Software</span><span class="sxs-lookup"><span data-stu-id="096ae-125">Software</span></span>

<span data-ttu-id="096ae-126">Windows Server 2008 R2 SP1 or above.</span><span class="sxs-lookup"><span data-stu-id="096ae-126">Windows Server 2008 R2 SP1 or above.</span></span>

### <a name="libraries"></a><span data-ttu-id="096ae-127">Libraries</span><span class="sxs-lookup"><span data-stu-id="096ae-127">Libraries</span></span>

<span data-ttu-id="096ae-128">These libraries are installed automatically with the extension.</span><span class="sxs-lookup"><span data-stu-id="096ae-128">These libraries are installed automatically with the extension.</span></span> 
-   [<span data-ttu-id="096ae-129">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span><span class="sxs-lookup"><span data-stu-id="096ae-129">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
-   [<span data-ttu-id="096ae-130">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span><span class="sxs-lookup"><span data-stu-id="096ae-130">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a><span data-ttu-id="096ae-131">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="096ae-131">Azure Active Directory</span></span>

<span data-ttu-id="096ae-132">Everyone using the NPS extension must be synced to Azure Active Directory using Azure AD Connect, and must be enabled for MFA.</span><span class="sxs-lookup"><span data-stu-id="096ae-132">Everyone using the NPS extension must be synced to Azure Active Directory using Azure AD Connect, and must be enabled for MFA.</span></span>

<span data-ttu-id="096ae-133">When you install the extension, you need the directory ID and admin credentials for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="096ae-133">When you install the extension, you need the directory ID and admin credentials for your Azure AD tenant.</span></span> <span data-ttu-id="096ae-134">You can find your directory ID in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="096ae-134">You can find your directory ID in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="096ae-135">Sign in as an administrator, select the **Azure Active Directory** icon on the left, then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="096ae-135">Sign in as an administrator, select the **Azure Active Directory** icon on the left, then select **Properties**.</span></span> <span data-ttu-id="096ae-136">Copy the GUID in the **Directory ID** box and save it.</span><span class="sxs-lookup"><span data-stu-id="096ae-136">Copy the GUID in the **Directory ID** box and save it.</span></span> <span data-ttu-id="096ae-137">You'll use this GUID as the tenant ID when you install the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="096ae-137">You'll use this GUID as the tenant ID when you install the NPS extension.</span></span>

![Find your Directory ID under Azure Active Directory properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-nps-extension/find-directory-id.PNG)

## <a name="prepare-your-environment"></a><span data-ttu-id="096ae-139">Prepare your environment</span><span class="sxs-lookup"><span data-stu-id="096ae-139">Prepare your environment</span></span>

<span data-ttu-id="096ae-140">Before you install the NPS extension, you want to prepare you environment to handle the authentication traffic.</span><span class="sxs-lookup"><span data-stu-id="096ae-140">Before you install the NPS extension, you want to prepare you environment to handle the authentication traffic.</span></span> 

### <a name="enable-the-nps-role-on-a-domain-joined-server"></a><span data-ttu-id="096ae-141">Enable the NPS role on a domain-joined server</span><span class="sxs-lookup"><span data-stu-id="096ae-141">Enable the NPS role on a domain-joined server</span></span>

<span data-ttu-id="096ae-142">The NPS server connects to Azure Active Directory and authenticates the MFA requests.</span><span class="sxs-lookup"><span data-stu-id="096ae-142">The NPS server connects to Azure Active Directory and authenticates the MFA requests.</span></span> <span data-ttu-id="096ae-143">Choose one server for this role.</span><span class="sxs-lookup"><span data-stu-id="096ae-143">Choose one server for this role.</span></span> <span data-ttu-id="096ae-144">We recommend choosing a server that doesn't handle requests from other services, because the NPS extension throws errors for any requests that aren't RADIUS.</span><span class="sxs-lookup"><span data-stu-id="096ae-144">We recommend choosing a server that doesn't handle requests from other services, because the NPS extension throws errors for any requests that aren't RADIUS.</span></span>

1. <span data-ttu-id="096ae-145">On your server, open the **Add Roles and Features Wizard** from the Server Manager Quickstart menu.</span><span class="sxs-lookup"><span data-stu-id="096ae-145">On your server, open the **Add Roles and Features Wizard** from the Server Manager Quickstart menu.</span></span>
2. <span data-ttu-id="096ae-146">Choose **Role-based or feature-based installation** for your installation type.</span><span class="sxs-lookup"><span data-stu-id="096ae-146">Choose **Role-based or feature-based installation** for your installation type.</span></span>
3. <span data-ttu-id="096ae-147">Select the **Network Policy and Access Services** server role.</span><span class="sxs-lookup"><span data-stu-id="096ae-147">Select the **Network Policy and Access Services** server role.</span></span> <span data-ttu-id="096ae-148">A window may pop up to inform you of required features to run this role.</span><span class="sxs-lookup"><span data-stu-id="096ae-148">A window may pop up to inform you of required features to run this role.</span></span>
4. <span data-ttu-id="096ae-149">Continue through the wizard until the Confirmation page.</span><span class="sxs-lookup"><span data-stu-id="096ae-149">Continue through the wizard until the Confirmation page.</span></span> <span data-ttu-id="096ae-150">Select **Install**.</span><span class="sxs-lookup"><span data-stu-id="096ae-150">Select **Install**.</span></span> 

<span data-ttu-id="096ae-151">Now that you have a server designated for NPS, you should also configure this server to handle incoming RADIUS requests from the VPN solution.</span><span class="sxs-lookup"><span data-stu-id="096ae-151">Now that you have a server designated for NPS, you should also configure this server to handle incoming RADIUS requests from the VPN solution.</span></span> 

### <a name="configure-your-vpn-solution-to-communicate-with-the-nps-server"></a><span data-ttu-id="096ae-152">Configure your VPN solution to communicate with the NPS server</span><span class="sxs-lookup"><span data-stu-id="096ae-152">Configure your VPN solution to communicate with the NPS server</span></span>

<span data-ttu-id="096ae-153">Depending on which VPN solution you use, the steps to configure your RADIUS authentication policy vary.</span><span class="sxs-lookup"><span data-stu-id="096ae-153">Depending on which VPN solution you use, the steps to configure your RADIUS authentication policy vary.</span></span> <span data-ttu-id="096ae-154">Configure this policy to point to your RADIUS NPS server.</span><span class="sxs-lookup"><span data-stu-id="096ae-154">Configure this policy to point to your RADIUS NPS server.</span></span> 

### <a name="sync-domain-users-to-the-cloud"></a><span data-ttu-id="096ae-155">Sync domain users to the cloud</span><span class="sxs-lookup"><span data-stu-id="096ae-155">Sync domain users to the cloud</span></span>

<span data-ttu-id="096ae-156">This step may already be complete on your tenant, but it's good to double-check that Azure AD Connect has synchronized your databases recently.</span><span class="sxs-lookup"><span data-stu-id="096ae-156">This step may already be complete on your tenant, but it's good to double-check that Azure AD Connect has synchronized your databases recently.</span></span> 

1. <span data-ttu-id="096ae-157">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="096ae-157">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="096ae-158">Select **Azure Active Directory** > **Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="096ae-158">Select **Azure Active Directory** > **Azure AD Connect**</span></span>
3. <span data-ttu-id="096ae-159">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span><span class="sxs-lookup"><span data-stu-id="096ae-159">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span></span>

<span data-ttu-id="096ae-160">If you need to kick off a new round of synchronization, us the instructions in [Azure AD Connect sync: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span><span class="sxs-lookup"><span data-stu-id="096ae-160">If you need to kick off a new round of synchronization, us the instructions in [Azure AD Connect sync: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span></span>

### <a name="enable-users-for-mfa"></a><span data-ttu-id="096ae-161">Enable users for MFA</span><span class="sxs-lookup"><span data-stu-id="096ae-161">Enable users for MFA</span></span>

<span data-ttu-id="096ae-162">Before you deploy the full NPS extension, you need to enable MFA for the users that you want to perform two-step verification.</span><span class="sxs-lookup"><span data-stu-id="096ae-162">Before you deploy the full NPS extension, you need to enable MFA for the users that you want to perform two-step verification.</span></span> <span data-ttu-id="096ae-163">More immediately, to test the extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="096ae-163">More immediately, to test the extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span></span> 

<span data-ttu-id="096ae-164">Use these steps to get a test account started:</span><span class="sxs-lookup"><span data-stu-id="096ae-164">Use these steps to get a test account started:</span></span>
1. <span data-ttu-id="096ae-165">[Enable an account for MFA](multi-factor-authentication-get-started-user-states.md).</span><span class="sxs-lookup"><span data-stu-id="096ae-165">[Enable an account for MFA](multi-factor-authentication-get-started-user-states.md).</span></span>
2. <span data-ttu-id="096ae-166">Go to any website that kicks off an Azure AD authentication, like https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="096ae-166">Go to any website that kicks off an Azure AD authentication, like https://portal.azure.com.</span></span>
3. <span data-ttu-id="096ae-167">[Register for two-step verification](./end-user/multi-factor-authentication-end-user-first-time.md).</span><span class="sxs-lookup"><span data-stu-id="096ae-167">[Register for two-step verification](./end-user/multi-factor-authentication-end-user-first-time.md).</span></span>

## <a name="install-the-nps-extension"></a><span data-ttu-id="096ae-168">Install the NPS extension</span><span class="sxs-lookup"><span data-stu-id="096ae-168">Install the NPS extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="096ae-169">Install the NPS extension on a different server than the VPN access point.</span><span class="sxs-lookup"><span data-stu-id="096ae-169">Install the NPS extension on a different server than the VPN access point.</span></span> 

### <a name="download-and-install-the-nps-extension-for-azure-mfa"></a><span data-ttu-id="096ae-170">Download and install the NPS extension for Azure MFA</span><span class="sxs-lookup"><span data-stu-id="096ae-170">Download and install the NPS extension for Azure MFA</span></span> 

1.  <span data-ttu-id="096ae-171">[Download the NPS Extension](https://aka.ms/npsmfa) from the Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="096ae-171">[Download the NPS Extension](https://aka.ms/npsmfa) from the Microsoft Download Center.</span></span>
2.  <span data-ttu-id="096ae-172">Copy the binary to the Network Policy Server you want to configure.</span><span class="sxs-lookup"><span data-stu-id="096ae-172">Copy the binary to the Network Policy Server you want to configure.</span></span>
3.  <span data-ttu-id="096ae-173">Run *setup.exe* and follow the installation instructions.</span><span class="sxs-lookup"><span data-stu-id="096ae-173">Run *setup.exe* and follow the installation instructions.</span></span> <span data-ttu-id="096ae-174">If you encounter errors, double-check that the two libraries from the prerequisite section were succesfully installed.</span><span class="sxs-lookup"><span data-stu-id="096ae-174">If you encounter errors, double-check that the two libraries from the prerequisite section were succesfully installed.</span></span>

### <a name="run-the-powershell-script"></a><span data-ttu-id="096ae-175">Run the PowerShell script</span><span class="sxs-lookup"><span data-stu-id="096ae-175">Run the PowerShell script</span></span>

<span data-ttu-id="096ae-176">The installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span><span class="sxs-lookup"><span data-stu-id="096ae-176">The installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span></span> <span data-ttu-id="096ae-177">This PowerShell script performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="096ae-177">This PowerShell script performs the following actions:</span></span>

-   <span data-ttu-id="096ae-178">Create a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="096ae-178">Create a self-signed certificate.</span></span>
-   <span data-ttu-id="096ae-179">Associate the public key of the certificate to the service principal on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="096ae-179">Associate the public key of the certificate to the service principal on Azure AD.</span></span>
-   <span data-ttu-id="096ae-180">Store the cert in the local machine cert store.</span><span class="sxs-lookup"><span data-stu-id="096ae-180">Store the cert in the local machine cert store.</span></span>
-   <span data-ttu-id="096ae-181">Grant access to the certificate’s private key to Network User.</span><span class="sxs-lookup"><span data-stu-id="096ae-181">Grant access to the certificate’s private key to Network User.</span></span>
-   <span data-ttu-id="096ae-182">Restart the NPS.</span><span class="sxs-lookup"><span data-stu-id="096ae-182">Restart the NPS.</span></span>

<span data-ttu-id="096ae-183">Unless you want to use your own certificates (instead of the self-signed certificates that the PowerShell script generates), run the PowerShell Script to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="096ae-183">Unless you want to use your own certificates (instead of the self-signed certificates that the PowerShell script generates), run the PowerShell Script to complete the installation.</span></span> <span data-ttu-id="096ae-184">If you install the extension on multiple servers, each one should have its own certificate.</span><span class="sxs-lookup"><span data-stu-id="096ae-184">If you install the extension on multiple servers, each one should have its own certificate.</span></span>

1. <span data-ttu-id="096ae-185">Run Windows PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="096ae-185">Run Windows PowerShell as an administrator.</span></span>
2. <span data-ttu-id="096ae-186">Change directories.</span><span class="sxs-lookup"><span data-stu-id="096ae-186">Change directories.</span></span>

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. <span data-ttu-id="096ae-187">Run the PowerShell script created by the installer.</span><span class="sxs-lookup"><span data-stu-id="096ae-187">Run the PowerShell script created by the installer.</span></span>

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. <span data-ttu-id="096ae-188">PowerShell prompts for your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="096ae-188">PowerShell prompts for your tenant ID.</span></span> <span data-ttu-id="096ae-189">Use the Directory ID GUID that you copied from the Azure portal in the prerequisites section.</span><span class="sxs-lookup"><span data-stu-id="096ae-189">Use the Directory ID GUID that you copied from the Azure portal in the prerequisites section.</span></span> 
5. <span data-ttu-id="096ae-190">Sign in to Azure AD as an administrator.</span><span class="sxs-lookup"><span data-stu-id="096ae-190">Sign in to Azure AD as an administrator.</span></span>
6. <span data-ttu-id="096ae-191">PowerShell shows a success message when the script is finished.</span><span class="sxs-lookup"><span data-stu-id="096ae-191">PowerShell shows a success message when the script is finished.</span></span>  

## <a name="configure-your-nps-extension"></a><span data-ttu-id="096ae-192">Configure your NPS extension</span><span class="sxs-lookup"><span data-stu-id="096ae-192">Configure your NPS extension</span></span>

<span data-ttu-id="096ae-193">This section includes design considerations and suggestions for successful NPS extension deployments.</span><span class="sxs-lookup"><span data-stu-id="096ae-193">This section includes design considerations and suggestions for successful NPS extension deployments.</span></span>

### <a name="configurations-limitations"></a><span data-ttu-id="096ae-194">Configurations limitations</span><span class="sxs-lookup"><span data-stu-id="096ae-194">Configurations limitations</span></span>

- <span data-ttu-id="096ae-195">The NPS extension for Azure MFA does not include tools to migrate users and settings from MFA Server to the cloud.</span><span class="sxs-lookup"><span data-stu-id="096ae-195">The NPS extension for Azure MFA does not include tools to migrate users and settings from MFA Server to the cloud.</span></span> <span data-ttu-id="096ae-196">For this reason, we suggest using the extension for new deployments, rather than existing deployment.</span><span class="sxs-lookup"><span data-stu-id="096ae-196">For this reason, we suggest using the extension for new deployments, rather than existing deployment.</span></span> <span data-ttu-id="096ae-197">If you use the extension on an existing deployment, your users will have to perform proof-up again to populate their MFA details in the cloud.</span><span class="sxs-lookup"><span data-stu-id="096ae-197">If you use the extension on an existing deployment, your users will have to perform proof-up again to populate their MFA details in the cloud.</span></span>  
- <span data-ttu-id="096ae-198">The NPS extension uses the UPN from the on-premises Active directory to identify the user on Azure MFA for performing the Secondary Auth. The extension cannot be configured to use a different identifier like alternate login ID or custom AD field other than UPN.</span><span class="sxs-lookup"><span data-stu-id="096ae-198">The NPS extension uses the UPN from the on-premises Active directory to identify the user on Azure MFA for performing the Secondary Auth. The extension cannot be configured to use a different identifier like alternate login ID or custom AD field other than UPN.</span></span>  

### <a name="control-radius-clients-that-require-mfa"></a><span data-ttu-id="096ae-199">Control RADIUS clients that require MFA</span><span class="sxs-lookup"><span data-stu-id="096ae-199">Control RADIUS clients that require MFA</span></span>

<span data-ttu-id="096ae-200">Once you enable MFA for a RADIUS client using the NPS Extension, all authentications for this client are required to perform MFA.</span><span class="sxs-lookup"><span data-stu-id="096ae-200">Once you enable MFA for a RADIUS client using the NPS Extension, all authentications for this client are required to perform MFA.</span></span> <span data-ttu-id="096ae-201">If you want to enable MFA for some RADIUS clients but not others, you can configure two NPS servers and install the extension on only one of them.</span><span class="sxs-lookup"><span data-stu-id="096ae-201">If you want to enable MFA for some RADIUS clients but not others, you can configure two NPS servers and install the extension on only one of them.</span></span> <span data-ttu-id="096ae-202">Configure RADIUS clients that you want to require MFA to send requests to the NPS server configured with the extension, and other RADIUS clients to the NPS server not configured with the extension.</span><span class="sxs-lookup"><span data-stu-id="096ae-202">Configure RADIUS clients that you want to require MFA to send requests to the NPS server configured with the extension, and other RADIUS clients to the NPS server not configured with the extension.</span></span>

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a><span data-ttu-id="096ae-203">Prepare for users that aren't enrolled for MFA</span><span class="sxs-lookup"><span data-stu-id="096ae-203">Prepare for users that aren't enrolled for MFA</span></span>

<span data-ttu-id="096ae-204">If you have users that aren't enrolled for MFA, you can determine what happens when they try to authenticate.</span><span class="sxs-lookup"><span data-stu-id="096ae-204">If you have users that aren't enrolled for MFA, you can determine what happens when they try to authenticate.</span></span> <span data-ttu-id="096ae-205">Use the registry setting *REQUIRE_USER_MATCH* in the registry path *HKLM\Software\Microsoft\AzureMFA* to control the feature behavior.</span><span class="sxs-lookup"><span data-stu-id="096ae-205">Use the registry setting *REQUIRE_USER_MATCH* in the registry path *HKLM\Software\Microsoft\AzureMFA* to control the feature behavior.</span></span> <span data-ttu-id="096ae-206">This setting has a single configuration option:</span><span class="sxs-lookup"><span data-stu-id="096ae-206">This setting has a single configuration option:</span></span>

| <span data-ttu-id="096ae-207">Key</span><span class="sxs-lookup"><span data-stu-id="096ae-207">Key</span></span> | <span data-ttu-id="096ae-208">Value</span><span class="sxs-lookup"><span data-stu-id="096ae-208">Value</span></span> | <span data-ttu-id="096ae-209">Default</span><span class="sxs-lookup"><span data-stu-id="096ae-209">Default</span></span> |
| --- | ----- | ------- |
| <span data-ttu-id="096ae-210">REQUIRE_USER_MATCH</span><span class="sxs-lookup"><span data-stu-id="096ae-210">REQUIRE_USER_MATCH</span></span> | <span data-ttu-id="096ae-211">TRUE/FALSE</span><span class="sxs-lookup"><span data-stu-id="096ae-211">TRUE/FALSE</span></span> | <span data-ttu-id="096ae-212">Not set (equivalent to TRUE)</span><span class="sxs-lookup"><span data-stu-id="096ae-212">Not set (equivalent to TRUE)</span></span> |

<span data-ttu-id="096ae-213">The purpose of this setting is to determine what to do when a user is not enrolled for MFA.</span><span class="sxs-lookup"><span data-stu-id="096ae-213">The purpose of this setting is to determine what to do when a user is not enrolled for MFA.</span></span> <span data-ttu-id="096ae-214">When the key does not exist, is not set, or is set to TRUE, and the user is not enrolled, then the extension fails the MFA challenge.</span><span class="sxs-lookup"><span data-stu-id="096ae-214">When the key does not exist, is not set, or is set to TRUE, and the user is not enrolled, then the extension fails the MFA challenge.</span></span> <span data-ttu-id="096ae-215">When the key is set to FALSE and the user is not enrolled, authentication proceeds without performing MFA.</span><span class="sxs-lookup"><span data-stu-id="096ae-215">When the key is set to FALSE and the user is not enrolled, authentication proceeds without performing MFA.</span></span>

<span data-ttu-id="096ae-216">You can choose to create this key and set it to FALSE during user onboarding.</span><span class="sxs-lookup"><span data-stu-id="096ae-216">You can choose to create this key and set it to FALSE during user onboarding.</span></span> <span data-ttu-id="096ae-217">Since setting the key permits users that aren't enrolled for MFA to sign in, you should remove this key before going to production.</span><span class="sxs-lookup"><span data-stu-id="096ae-217">Since setting the key permits users that aren't enrolled for MFA to sign in, you should remove this key before going to production.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="096ae-218">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="096ae-218">Troubleshooting</span></span>

### <a name="how-do-i-verify-that-the-client-cert-is-installed-as-expected"></a><span data-ttu-id="096ae-219">How do I verify that the client cert is installed as expected?</span><span class="sxs-lookup"><span data-stu-id="096ae-219">How do I verify that the client cert is installed as expected?</span></span>

<span data-ttu-id="096ae-220">Look for the self-signed certificate created by the installer in the cert store, and check that the private key has permissions granted to user **NETWORK SERVICE**.</span><span class="sxs-lookup"><span data-stu-id="096ae-220">Look for the self-signed certificate created by the installer in the cert store, and check that the private key has permissions granted to user **NETWORK SERVICE**.</span></span> <span data-ttu-id="096ae-221">The cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span><span class="sxs-lookup"><span data-stu-id="096ae-221">The cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span></span>

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-to-my-tenant-in-azure-active-directory"></a><span data-ttu-id="096ae-222">How can I verify that my client cert is associated to my tenant in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="096ae-222">How can I verify that my client cert is associated to my tenant in Azure Active Directory?</span></span>

<span data-ttu-id="096ae-223">Open PowerShell command prompt and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="096ae-223">Open PowerShell command prompt and run the following commands:</span></span>

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

<span data-ttu-id="096ae-224">These commands print all the certificates associating your tenant with your instance of the NPS extension in your PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="096ae-224">These commands print all the certificates associating your tenant with your instance of the NPS extension in your PowerShell session.</span></span> <span data-ttu-id="096ae-225">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without the private key, and compare it with the list from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="096ae-225">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without the private key, and compare it with the list from PowerShell.</span></span>

<span data-ttu-id="096ae-226">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used to filter out obvious misfits if the command returns more than one cert.</span><span class="sxs-lookup"><span data-stu-id="096ae-226">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used to filter out obvious misfits if the command returns more than one cert.</span></span>

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a><span data-ttu-id="096ae-227">Why are my requests failing with ADAL token error?</span><span class="sxs-lookup"><span data-stu-id="096ae-227">Why are my requests failing with ADAL token error?</span></span>

<span data-ttu-id="096ae-228">This error could be due to one of several reasons.</span><span class="sxs-lookup"><span data-stu-id="096ae-228">This error could be due to one of several reasons.</span></span> <span data-ttu-id="096ae-229">Use these steps to help troubleshoot:</span><span class="sxs-lookup"><span data-stu-id="096ae-229">Use these steps to help troubleshoot:</span></span>

1. <span data-ttu-id="096ae-230">Restart your NPS server.</span><span class="sxs-lookup"><span data-stu-id="096ae-230">Restart your NPS server.</span></span>
2. <span data-ttu-id="096ae-231">Verify that that client cert is installed as expected.</span><span class="sxs-lookup"><span data-stu-id="096ae-231">Verify that that client cert is installed as expected.</span></span>
3. <span data-ttu-id="096ae-232">Verify that the certificate is associated with your tenant on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="096ae-232">Verify that the certificate is associated with your tenant on Azure AD.</span></span>
4. <span data-ttu-id="096ae-233">Verify that https://login.windows.net/ is accessible from the server running the extension.</span><span class="sxs-lookup"><span data-stu-id="096ae-233">Verify that https://login.windows.net/ is accessible from the server running the extension.</span></span>

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-the-user-is-not-found"></a><span data-ttu-id="096ae-234">Why does authentication fail with an error in HTTP logs stating that the user is not found?</span><span class="sxs-lookup"><span data-stu-id="096ae-234">Why does authentication fail with an error in HTTP logs stating that the user is not found?</span></span>

<span data-ttu-id="096ae-235">Verify that AD Connect is running, and that the user is present in both Windows Active Directory and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="096ae-235">Verify that AD Connect is running, and that the user is present in both Windows Active Directory and Azure Active Directory.</span></span>

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a><span data-ttu-id="096ae-236">Why do I see HTTP connect errors in logs with all my authentications failing?</span><span class="sxs-lookup"><span data-stu-id="096ae-236">Why do I see HTTP connect errors in logs with all my authentications failing?</span></span>

<span data-ttu-id="096ae-237">Verify that https://adnotifications.windowsazure.com is reachable from the server running the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="096ae-237">Verify that https://adnotifications.windowsazure.com is reachable from the server running the NPS extension.</span></span>

## <a name="next-steps"></a><span data-ttu-id="096ae-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="096ae-238">Next steps</span></span>

<span data-ttu-id="096ae-239">See how to integrate Azure MFA with [Active Directory](multi-factor-authentication-get-started-server-dirint.md), [RADIUS authentication](multi-factor-authentication-get-started-server-radius.md), and [LDAP authentication](multi-factor-authentication-get-started-server-ldap.md).</span><span class="sxs-lookup"><span data-stu-id="096ae-239">See how to integrate Azure MFA with [Active Directory](multi-factor-authentication-get-started-server-dirint.md), [RADIUS authentication](multi-factor-authentication-get-started-server-radius.md), and [LDAP authentication](multi-factor-authentication-get-started-server-ldap.md).</span></span>


