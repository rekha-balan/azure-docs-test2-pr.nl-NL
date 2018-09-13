---
title: Use existing NPS servers to provide Azure MFA capabilities
description: Add cloud-based two-step verification capabilities to your existing authentication infrastructure
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: a24988bb9866dde72769107f1c45fc461c039f9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870372"
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a><span data-ttu-id="e5083-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e5083-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="e5083-104">The Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities to your authentication infrastructure using your existing servers.</span><span class="sxs-lookup"><span data-stu-id="e5083-104">The Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities to your authentication infrastructure using your existing servers.</span></span> <span data-ttu-id="e5083-105">With the NPS extension, you can add phone call, text message, or phone app verification to your existing authentication flow without having to install, configure, and maintain new servers.</span><span class="sxs-lookup"><span data-stu-id="e5083-105">With the NPS extension, you can add phone call, text message, or phone app verification to your existing authentication flow without having to install, configure, and maintain new servers.</span></span> 

<span data-ttu-id="e5083-106">This extension was created for organizations that want to protect VPN connections without deploying the Azure MFA Server.</span><span class="sxs-lookup"><span data-stu-id="e5083-106">This extension was created for organizations that want to protect VPN connections without deploying the Azure MFA Server.</span></span> <span data-ttu-id="e5083-107">The NPS extension acts as an adapter between RADIUS and cloud-based Azure MFA to provide a second factor of authentication for federated or synced users.</span><span class="sxs-lookup"><span data-stu-id="e5083-107">The NPS extension acts as an adapter between RADIUS and cloud-based Azure MFA to provide a second factor of authentication for federated or synced users.</span></span>

<span data-ttu-id="e5083-108">When using the NPS extension for Azure MFA, the authentication flow includes the following components:</span><span class="sxs-lookup"><span data-stu-id="e5083-108">When using the NPS extension for Azure MFA, the authentication flow includes the following components:</span></span> 

1. <span data-ttu-id="e5083-109">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests to NPS servers.</span><span class="sxs-lookup"><span data-stu-id="e5083-109">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests to NPS servers.</span></span> 
2. <span data-ttu-id="e5083-110">**NPS Server** connects to Active Directory to perform the primary authentication for the RADIUS requests and, upon success, passes the request to any installed extensions.</span><span class="sxs-lookup"><span data-stu-id="e5083-110">**NPS Server** connects to Active Directory to perform the primary authentication for the RADIUS requests and, upon success, passes the request to any installed extensions.</span></span>  
3. <span data-ttu-id="e5083-111">**NPS Extension** triggers a request to Azure MFA for the secondary authentication.</span><span class="sxs-lookup"><span data-stu-id="e5083-111">**NPS Extension** triggers a request to Azure MFA for the secondary authentication.</span></span> <span data-ttu-id="e5083-112">Once the extension receives the response, and if the MFA challenge succeeds, it completes the authentication request by providing the NPS server with security tokens that include an MFA claim, issued by Azure STS.</span><span class="sxs-lookup"><span data-stu-id="e5083-112">Once the extension receives the response, and if the MFA challenge succeeds, it completes the authentication request by providing the NPS server with security tokens that include an MFA claim, issued by Azure STS.</span></span>  
4. <span data-ttu-id="e5083-113">**Azure MFA** communicates with Azure Active Directory to retrieve the user’s details and performs the secondary authentication using a verification method configured to the user.</span><span class="sxs-lookup"><span data-stu-id="e5083-113">**Azure MFA** communicates with Azure Active Directory to retrieve the user’s details and performs the secondary authentication using a verification method configured to the user.</span></span>

<span data-ttu-id="e5083-114">The following diagram illustrates this high-level authentication request flow:</span><span class="sxs-lookup"><span data-stu-id="e5083-114">The following diagram illustrates this high-level authentication request flow:</span></span> 

![Authentication flow diagram](./media/howto-mfa-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a><span data-ttu-id="e5083-116">Plan your deployment</span><span class="sxs-lookup"><span data-stu-id="e5083-116">Plan your deployment</span></span>

<span data-ttu-id="e5083-117">The NPS extension automatically handles redundancy, so you don't need a special configuration.</span><span class="sxs-lookup"><span data-stu-id="e5083-117">The NPS extension automatically handles redundancy, so you don't need a special configuration.</span></span>

<span data-ttu-id="e5083-118">You can create as many Azure MFA-enabled NPS servers as you need.</span><span class="sxs-lookup"><span data-stu-id="e5083-118">You can create as many Azure MFA-enabled NPS servers as you need.</span></span> <span data-ttu-id="e5083-119">If you do install multiple servers, you should use a difference client certificate for each one of them.</span><span class="sxs-lookup"><span data-stu-id="e5083-119">If you do install multiple servers, you should use a difference client certificate for each one of them.</span></span> <span data-ttu-id="e5083-120">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span><span class="sxs-lookup"><span data-stu-id="e5083-120">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span></span>

<span data-ttu-id="e5083-121">VPN servers route authentication requests, so they need to be aware of the new Azure MFA-enabled NPS servers.</span><span class="sxs-lookup"><span data-stu-id="e5083-121">VPN servers route authentication requests, so they need to be aware of the new Azure MFA-enabled NPS servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5083-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e5083-122">Prerequisites</span></span>

<span data-ttu-id="e5083-123">The NPS extension is meant to work with your existing infrastructure.</span><span class="sxs-lookup"><span data-stu-id="e5083-123">The NPS extension is meant to work with your existing infrastructure.</span></span> <span data-ttu-id="e5083-124">Make sure you have the following prerequisites before you begin.</span><span class="sxs-lookup"><span data-stu-id="e5083-124">Make sure you have the following prerequisites before you begin.</span></span>

### <a name="licenses"></a><span data-ttu-id="e5083-125">Licenses</span><span class="sxs-lookup"><span data-stu-id="e5083-125">Licenses</span></span>

<span data-ttu-id="e5083-126">The NPS Extension for Azure MFA is available to customers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA stand-alone license).</span><span class="sxs-lookup"><span data-stu-id="e5083-126">The NPS Extension for Azure MFA is available to customers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA stand-alone license).</span></span> <span data-ttu-id="e5083-127">Consumption-based licenses for Azure MFA such as per user or per authentication licenses are not compatible with the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="e5083-127">Consumption-based licenses for Azure MFA such as per user or per authentication licenses are not compatible with the NPS extension.</span></span> 

### <a name="software"></a><span data-ttu-id="e5083-128">Software</span><span class="sxs-lookup"><span data-stu-id="e5083-128">Software</span></span>

<span data-ttu-id="e5083-129">Windows Server 2008 R2 SP1 or above.</span><span class="sxs-lookup"><span data-stu-id="e5083-129">Windows Server 2008 R2 SP1 or above.</span></span>

### <a name="libraries"></a><span data-ttu-id="e5083-130">Libraries</span><span class="sxs-lookup"><span data-stu-id="e5083-130">Libraries</span></span>

<span data-ttu-id="e5083-131">These libraries are installed automatically with the extension.</span><span class="sxs-lookup"><span data-stu-id="e5083-131">These libraries are installed automatically with the extension.</span></span>

- [<span data-ttu-id="e5083-132">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span><span class="sxs-lookup"><span data-stu-id="e5083-132">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
- [<span data-ttu-id="e5083-133">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span><span class="sxs-lookup"><span data-stu-id="e5083-133">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://www.powershellgallery.com/packages/MSOnline/1.1.166.0)

<span data-ttu-id="e5083-134">The Microsoft Azure Active Directory Module for Windows PowerShell is installed, if it is not already present, through a configuration script you run as part of the setup process.</span><span class="sxs-lookup"><span data-stu-id="e5083-134">The Microsoft Azure Active Directory Module for Windows PowerShell is installed, if it is not already present, through a configuration script you run as part of the setup process.</span></span> <span data-ttu-id="e5083-135">There is no need to install this module ahead of time if it is not already installed.</span><span class="sxs-lookup"><span data-stu-id="e5083-135">There is no need to install this module ahead of time if it is not already installed.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="e5083-136">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e5083-136">Azure Active Directory</span></span>

<span data-ttu-id="e5083-137">Everyone using the NPS extension must be synced to Azure Active Directory using Azure AD Connect, and must be registered for MFA.</span><span class="sxs-lookup"><span data-stu-id="e5083-137">Everyone using the NPS extension must be synced to Azure Active Directory using Azure AD Connect, and must be registered for MFA.</span></span>

<span data-ttu-id="e5083-138">When you install the extension, you need the directory ID and admin credentials for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="e5083-138">When you install the extension, you need the directory ID and admin credentials for your Azure AD tenant.</span></span> <span data-ttu-id="e5083-139">You can find your directory ID in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e5083-139">You can find your directory ID in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e5083-140">Sign in as an administrator, select the **Azure Active Directory** icon on the left, then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="e5083-140">Sign in as an administrator, select the **Azure Active Directory** icon on the left, then select **Properties**.</span></span> <span data-ttu-id="e5083-141">Copy the GUID in the **Directory ID** box and save it.</span><span class="sxs-lookup"><span data-stu-id="e5083-141">Copy the GUID in the **Directory ID** box and save it.</span></span> <span data-ttu-id="e5083-142">You use this GUID as the tenant ID when you install the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="e5083-142">You use this GUID as the tenant ID when you install the NPS extension.</span></span>

![Find your Directory ID under Azure Active Directory properties](./media/howto-mfa-nps-extension/find-directory-id.png)

### <a name="network-requirements"></a><span data-ttu-id="e5083-144">Network requirements</span><span class="sxs-lookup"><span data-stu-id="e5083-144">Network requirements</span></span>

<span data-ttu-id="e5083-145">The NPS server needs to be able to communicate with the following URLs over ports 80 and 443.</span><span class="sxs-lookup"><span data-stu-id="e5083-145">The NPS server needs to be able to communicate with the following URLs over ports 80 and 443.</span></span>

* https://adnotifications.windowsazure.com  
* https://login.microsoftonline.com

## <a name="prepare-your-environment"></a><span data-ttu-id="e5083-146">Prepare your environment</span><span class="sxs-lookup"><span data-stu-id="e5083-146">Prepare your environment</span></span>

<span data-ttu-id="e5083-147">Before you install the NPS extension, you want to prepare you environment to handle the authentication traffic.</span><span class="sxs-lookup"><span data-stu-id="e5083-147">Before you install the NPS extension, you want to prepare you environment to handle the authentication traffic.</span></span>

### <a name="enable-the-nps-role-on-a-domain-joined-server"></a><span data-ttu-id="e5083-148">Enable the NPS role on a domain-joined server</span><span class="sxs-lookup"><span data-stu-id="e5083-148">Enable the NPS role on a domain-joined server</span></span>

<span data-ttu-id="e5083-149">The NPS server connects to Azure Active Directory and authenticates the MFA requests.</span><span class="sxs-lookup"><span data-stu-id="e5083-149">The NPS server connects to Azure Active Directory and authenticates the MFA requests.</span></span> <span data-ttu-id="e5083-150">Choose one server for this role.</span><span class="sxs-lookup"><span data-stu-id="e5083-150">Choose one server for this role.</span></span> <span data-ttu-id="e5083-151">We recommend choosing a server that doesn't handle requests from other services, because the NPS extension throws errors for any requests that aren't RADIUS.</span><span class="sxs-lookup"><span data-stu-id="e5083-151">We recommend choosing a server that doesn't handle requests from other services, because the NPS extension throws errors for any requests that aren't RADIUS.</span></span> <span data-ttu-id="e5083-152">The NPS server must be set up as the primary and secondary authentication server for your environment; it cannot proxy RADIUS requests to another server.</span><span class="sxs-lookup"><span data-stu-id="e5083-152">The NPS server must be set up as the primary and secondary authentication server for your environment; it cannot proxy RADIUS requests to another server.</span></span>

1. <span data-ttu-id="e5083-153">On your server, open the **Add Roles and Features Wizard** from the Server Manager Quickstart menu.</span><span class="sxs-lookup"><span data-stu-id="e5083-153">On your server, open the **Add Roles and Features Wizard** from the Server Manager Quickstart menu.</span></span>
2. <span data-ttu-id="e5083-154">Choose **Role-based or feature-based installation** for your installation type.</span><span class="sxs-lookup"><span data-stu-id="e5083-154">Choose **Role-based or feature-based installation** for your installation type.</span></span>
3. <span data-ttu-id="e5083-155">Select the **Network Policy and Access Services** server role.</span><span class="sxs-lookup"><span data-stu-id="e5083-155">Select the **Network Policy and Access Services** server role.</span></span> <span data-ttu-id="e5083-156">A window may pop up to inform you of required features to run this role.</span><span class="sxs-lookup"><span data-stu-id="e5083-156">A window may pop up to inform you of required features to run this role.</span></span>
4. <span data-ttu-id="e5083-157">Continue through the wizard until the Confirmation page.</span><span class="sxs-lookup"><span data-stu-id="e5083-157">Continue through the wizard until the Confirmation page.</span></span> <span data-ttu-id="e5083-158">Select **Install**.</span><span class="sxs-lookup"><span data-stu-id="e5083-158">Select **Install**.</span></span>

<span data-ttu-id="e5083-159">Now that you have a server designated for NPS, you should also configure this server to handle incoming RADIUS requests from the VPN solution.</span><span class="sxs-lookup"><span data-stu-id="e5083-159">Now that you have a server designated for NPS, you should also configure this server to handle incoming RADIUS requests from the VPN solution.</span></span>

### <a name="configure-your-vpn-solution-to-communicate-with-the-nps-server"></a><span data-ttu-id="e5083-160">Configure your VPN solution to communicate with the NPS server</span><span class="sxs-lookup"><span data-stu-id="e5083-160">Configure your VPN solution to communicate with the NPS server</span></span>

<span data-ttu-id="e5083-161">Depending on which VPN solution you use, the steps to configure your RADIUS authentication policy vary.</span><span class="sxs-lookup"><span data-stu-id="e5083-161">Depending on which VPN solution you use, the steps to configure your RADIUS authentication policy vary.</span></span> <span data-ttu-id="e5083-162">Configure this policy to point to your RADIUS NPS server.</span><span class="sxs-lookup"><span data-stu-id="e5083-162">Configure this policy to point to your RADIUS NPS server.</span></span>

### <a name="sync-domain-users-to-the-cloud"></a><span data-ttu-id="e5083-163">Sync domain users to the cloud</span><span class="sxs-lookup"><span data-stu-id="e5083-163">Sync domain users to the cloud</span></span>

<span data-ttu-id="e5083-164">This step may already be complete on your tenant, but it's good to double-check that Azure AD Connect has synchronized your databases recently.</span><span class="sxs-lookup"><span data-stu-id="e5083-164">This step may already be complete on your tenant, but it's good to double-check that Azure AD Connect has synchronized your databases recently.</span></span>

1. <span data-ttu-id="e5083-165">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e5083-165">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="e5083-166">Select **Azure Active Directory** > **Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="e5083-166">Select **Azure Active Directory** > **Azure AD Connect**</span></span>
3. <span data-ttu-id="e5083-167">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span><span class="sxs-lookup"><span data-stu-id="e5083-167">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span></span>

<span data-ttu-id="e5083-168">If you need to kick off a new round of synchronization, us the instructions in [Azure AD Connect sync: Scheduler](../connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span><span class="sxs-lookup"><span data-stu-id="e5083-168">If you need to kick off a new round of synchronization, us the instructions in [Azure AD Connect sync: Scheduler](../connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span></span>

### <a name="determine-which-authentication-methods-your-users-can-use"></a><span data-ttu-id="e5083-169">Determine which authentication methods your users can use</span><span class="sxs-lookup"><span data-stu-id="e5083-169">Determine which authentication methods your users can use</span></span>

<span data-ttu-id="e5083-170">There are two factors that affect which authentication methods are available with an NPS extension deployment:</span><span class="sxs-lookup"><span data-stu-id="e5083-170">There are two factors that affect which authentication methods are available with an NPS extension deployment:</span></span>

1. <span data-ttu-id="e5083-171">The password encryption algorithm used between the RADIUS client (VPN, Netscaler server, or other) and the NPS servers.</span><span class="sxs-lookup"><span data-stu-id="e5083-171">The password encryption algorithm used between the RADIUS client (VPN, Netscaler server, or other) and the NPS servers.</span></span>
   - <span data-ttu-id="e5083-172">**PAP** supports all the authentication methods of Azure MFA in the cloud: phone call, one-way text message, mobile app notification, and mobile app verification code.</span><span class="sxs-lookup"><span data-stu-id="e5083-172">**PAP** supports all the authentication methods of Azure MFA in the cloud: phone call, one-way text message, mobile app notification, and mobile app verification code.</span></span>
   - <span data-ttu-id="e5083-173">**CHAPV2** and **EAP** support phone call and mobile app notification.</span><span class="sxs-lookup"><span data-stu-id="e5083-173">**CHAPV2** and **EAP** support phone call and mobile app notification.</span></span>
2. <span data-ttu-id="e5083-174">The input methods that the client application (VPN, Netscaler server, or other) can handle.</span><span class="sxs-lookup"><span data-stu-id="e5083-174">The input methods that the client application (VPN, Netscaler server, or other) can handle.</span></span> <span data-ttu-id="e5083-175">For example, does the VPN client have some means to allow the user to type in a verification code from a text or mobile app?</span><span class="sxs-lookup"><span data-stu-id="e5083-175">For example, does the VPN client have some means to allow the user to type in a verification code from a text or mobile app?</span></span>

<span data-ttu-id="e5083-176">When you deploy the NPS extension, use these factors to evaluate which methods are available for your users.</span><span class="sxs-lookup"><span data-stu-id="e5083-176">When you deploy the NPS extension, use these factors to evaluate which methods are available for your users.</span></span> <span data-ttu-id="e5083-177">If your RADIUS client supports PAP, but the client UX doesn't have input fields for a verification code, then phone call and mobile app notification are the two supported options.</span><span class="sxs-lookup"><span data-stu-id="e5083-177">If your RADIUS client supports PAP, but the client UX doesn't have input fields for a verification code, then phone call and mobile app notification are the two supported options.</span></span>

<span data-ttu-id="e5083-178">You can [disable unsupported authentication methods](howto-mfa-mfasettings.md#selectable-verification-methods) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e5083-178">You can [disable unsupported authentication methods](howto-mfa-mfasettings.md#selectable-verification-methods) in Azure.</span></span>

### <a name="register-users-for-mfa"></a><span data-ttu-id="e5083-179">Register users for MFA</span><span class="sxs-lookup"><span data-stu-id="e5083-179">Register users for MFA</span></span>

<span data-ttu-id="e5083-180">Before you deploy and use the NPS extension, users that are required to perform two-step verification need to be registered for MFA.</span><span class="sxs-lookup"><span data-stu-id="e5083-180">Before you deploy and use the NPS extension, users that are required to perform two-step verification need to be registered for MFA.</span></span> <span data-ttu-id="e5083-181">More immediately, to test the extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="e5083-181">More immediately, to test the extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span></span>

<span data-ttu-id="e5083-182">Use these steps to get a test account started:</span><span class="sxs-lookup"><span data-stu-id="e5083-182">Use these steps to get a test account started:</span></span>
1. <span data-ttu-id="e5083-183">Sign in to [https://aka.ms/mfasetup](https://aka.ms/mfasetup) with a test account.</span><span class="sxs-lookup"><span data-stu-id="e5083-183">Sign in to [https://aka.ms/mfasetup](https://aka.ms/mfasetup) with a test account.</span></span> 
2. <span data-ttu-id="e5083-184">Follow the prompts to set up a verification method.</span><span class="sxs-lookup"><span data-stu-id="e5083-184">Follow the prompts to set up a verification method.</span></span>
3. <span data-ttu-id="e5083-185">Either create a conditional access policy or [change the user state](howto-mfa-userstates.md) to require two-step verification for the test account.</span><span class="sxs-lookup"><span data-stu-id="e5083-185">Either create a conditional access policy or [change the user state](howto-mfa-userstates.md) to require two-step verification for the test account.</span></span> 

<span data-ttu-id="e5083-186">Your users also need to follow these steps to enroll before they can authenticate with the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="e5083-186">Your users also need to follow these steps to enroll before they can authenticate with the NPS extension.</span></span>

## <a name="install-the-nps-extension"></a><span data-ttu-id="e5083-187">Install the NPS extension</span><span class="sxs-lookup"><span data-stu-id="e5083-187">Install the NPS extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5083-188">Install the NPS extension on a different server than the VPN access point.</span><span class="sxs-lookup"><span data-stu-id="e5083-188">Install the NPS extension on a different server than the VPN access point.</span></span>

### <a name="download-and-install-the-nps-extension-for-azure-mfa"></a><span data-ttu-id="e5083-189">Download and install the NPS extension for Azure MFA</span><span class="sxs-lookup"><span data-stu-id="e5083-189">Download and install the NPS extension for Azure MFA</span></span>

1. <span data-ttu-id="e5083-190">[Download the NPS Extension](https://aka.ms/npsmfa) from the Microsoft Download Center.</span><span class="sxs-lookup"><span data-stu-id="e5083-190">[Download the NPS Extension](https://aka.ms/npsmfa) from the Microsoft Download Center.</span></span>
2. <span data-ttu-id="e5083-191">Copy the binary to the Network Policy Server you want to configure.</span><span class="sxs-lookup"><span data-stu-id="e5083-191">Copy the binary to the Network Policy Server you want to configure.</span></span>
3. <span data-ttu-id="e5083-192">Run *setup.exe* and follow the installation instructions.</span><span class="sxs-lookup"><span data-stu-id="e5083-192">Run *setup.exe* and follow the installation instructions.</span></span> <span data-ttu-id="e5083-193">If you encounter errors, double-check that the two libraries from the prerequisite section were successfully installed.</span><span class="sxs-lookup"><span data-stu-id="e5083-193">If you encounter errors, double-check that the two libraries from the prerequisite section were successfully installed.</span></span>

### <a name="run-the-powershell-script"></a><span data-ttu-id="e5083-194">Run the PowerShell script</span><span class="sxs-lookup"><span data-stu-id="e5083-194">Run the PowerShell script</span></span>

<span data-ttu-id="e5083-195">The installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span><span class="sxs-lookup"><span data-stu-id="e5083-195">The installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span></span> <span data-ttu-id="e5083-196">This PowerShell script performs the following actions each time it is run:</span><span class="sxs-lookup"><span data-stu-id="e5083-196">This PowerShell script performs the following actions each time it is run:</span></span>

- <span data-ttu-id="e5083-197">Create a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="e5083-197">Create a self-signed certificate.</span></span>
- <span data-ttu-id="e5083-198">Associate the public key of the certificate to the service principal on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5083-198">Associate the public key of the certificate to the service principal on Azure AD.</span></span>
- <span data-ttu-id="e5083-199">Store the cert in the local machine cert store.</span><span class="sxs-lookup"><span data-stu-id="e5083-199">Store the cert in the local machine cert store.</span></span>
- <span data-ttu-id="e5083-200">Grant access to the certificate’s private key to Network User.</span><span class="sxs-lookup"><span data-stu-id="e5083-200">Grant access to the certificate’s private key to Network User.</span></span>
- <span data-ttu-id="e5083-201">Restart the NPS.</span><span class="sxs-lookup"><span data-stu-id="e5083-201">Restart the NPS.</span></span>

<span data-ttu-id="e5083-202">Unless you want to use your own certificates (instead of the self-signed certificates that the PowerShell script generates), run the PowerShell Script to complete the installation.</span><span class="sxs-lookup"><span data-stu-id="e5083-202">Unless you want to use your own certificates (instead of the self-signed certificates that the PowerShell script generates), run the PowerShell Script to complete the installation.</span></span> <span data-ttu-id="e5083-203">If you install the extension on multiple servers, each one should have its own certificate.</span><span class="sxs-lookup"><span data-stu-id="e5083-203">If you install the extension on multiple servers, each one should have its own certificate.</span></span>

1. <span data-ttu-id="e5083-204">Run Windows PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e5083-204">Run Windows PowerShell as an administrator.</span></span>
2. <span data-ttu-id="e5083-205">Change directories.</span><span class="sxs-lookup"><span data-stu-id="e5083-205">Change directories.</span></span>

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. <span data-ttu-id="e5083-206">Run the PowerShell script created by the installer.</span><span class="sxs-lookup"><span data-stu-id="e5083-206">Run the PowerShell script created by the installer.</span></span>

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. <span data-ttu-id="e5083-207">Sign in to Azure AD as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e5083-207">Sign in to Azure AD as an administrator.</span></span>
5. <span data-ttu-id="e5083-208">PowerShell prompts for your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="e5083-208">PowerShell prompts for your tenant ID.</span></span> <span data-ttu-id="e5083-209">Use the Directory ID GUID that you copied from the Azure portal in the prerequisites section.</span><span class="sxs-lookup"><span data-stu-id="e5083-209">Use the Directory ID GUID that you copied from the Azure portal in the prerequisites section.</span></span>
6. <span data-ttu-id="e5083-210">PowerShell shows a success message when the script is finished.</span><span class="sxs-lookup"><span data-stu-id="e5083-210">PowerShell shows a success message when the script is finished.</span></span>  

<span data-ttu-id="e5083-211">Repeat these steps on any additional NPS servers that you want to set up for load balancing.</span><span class="sxs-lookup"><span data-stu-id="e5083-211">Repeat these steps on any additional NPS servers that you want to set up for load balancing.</span></span>

> [!NOTE]
> <span data-ttu-id="e5083-212">If you use your own certificates instead of generating certificates with the PowerShell script, make sure that they align to the NPS naming convention.</span><span class="sxs-lookup"><span data-stu-id="e5083-212">If you use your own certificates instead of generating certificates with the PowerShell script, make sure that they align to the NPS naming convention.</span></span> <span data-ttu-id="e5083-213">The subject name must be **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span><span class="sxs-lookup"><span data-stu-id="e5083-213">The subject name must be **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span></span> 

## <a name="configure-your-nps-extension"></a><span data-ttu-id="e5083-214">Configure your NPS extension</span><span class="sxs-lookup"><span data-stu-id="e5083-214">Configure your NPS extension</span></span>

<span data-ttu-id="e5083-215">This section includes design considerations and suggestions for successful NPS extension deployments.</span><span class="sxs-lookup"><span data-stu-id="e5083-215">This section includes design considerations and suggestions for successful NPS extension deployments.</span></span>

### <a name="configuration-limitations"></a><span data-ttu-id="e5083-216">Configuration limitations</span><span class="sxs-lookup"><span data-stu-id="e5083-216">Configuration limitations</span></span>

- <span data-ttu-id="e5083-217">The NPS extension for Azure MFA does not include tools to migrate users and settings from MFA Server to the cloud.</span><span class="sxs-lookup"><span data-stu-id="e5083-217">The NPS extension for Azure MFA does not include tools to migrate users and settings from MFA Server to the cloud.</span></span> <span data-ttu-id="e5083-218">For this reason, we suggest using the extension for new deployments, rather than existing deployment.</span><span class="sxs-lookup"><span data-stu-id="e5083-218">For this reason, we suggest using the extension for new deployments, rather than existing deployment.</span></span> <span data-ttu-id="e5083-219">If you use the extension on an existing deployment, your users have to perform proof-up again to populate their MFA details in the cloud.</span><span class="sxs-lookup"><span data-stu-id="e5083-219">If you use the extension on an existing deployment, your users have to perform proof-up again to populate their MFA details in the cloud.</span></span>  
- <span data-ttu-id="e5083-220">The NPS extension uses the UPN from the on-premises Active directory to identify the user on Azure MFA for performing the Secondary Auth. The extension can be configured to use a different identifier like alternate login ID or custom Active Directory field other than UPN.</span><span class="sxs-lookup"><span data-stu-id="e5083-220">The NPS extension uses the UPN from the on-premises Active directory to identify the user on Azure MFA for performing the Secondary Auth. The extension can be configured to use a different identifier like alternate login ID or custom Active Directory field other than UPN.</span></span> <span data-ttu-id="e5083-221">For more information, see the article, [Advanced configuration options for the NPS extension for Multi-Factor Authentication](howto-mfa-nps-extension-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="e5083-221">For more information, see the article, [Advanced configuration options for the NPS extension for Multi-Factor Authentication](howto-mfa-nps-extension-advanced.md).</span></span>
- <span data-ttu-id="e5083-222">Not all encryption protocols support all verification methods.</span><span class="sxs-lookup"><span data-stu-id="e5083-222">Not all encryption protocols support all verification methods.</span></span>
   - <span data-ttu-id="e5083-223">**PAP** supports phone call, one-way text message, mobile app notification, and mobile app verification code</span><span class="sxs-lookup"><span data-stu-id="e5083-223">**PAP** supports phone call, one-way text message, mobile app notification, and mobile app verification code</span></span>
   - <span data-ttu-id="e5083-224">**CHAPV2** and **EAP** support phone call and mobile app notification</span><span class="sxs-lookup"><span data-stu-id="e5083-224">**CHAPV2** and **EAP** support phone call and mobile app notification</span></span>

### <a name="control-radius-clients-that-require-mfa"></a><span data-ttu-id="e5083-225">Control RADIUS clients that require MFA</span><span class="sxs-lookup"><span data-stu-id="e5083-225">Control RADIUS clients that require MFA</span></span>

<span data-ttu-id="e5083-226">Once you enable MFA for a RADIUS client using the NPS Extension, all authentications for this client are required to perform MFA.</span><span class="sxs-lookup"><span data-stu-id="e5083-226">Once you enable MFA for a RADIUS client using the NPS Extension, all authentications for this client are required to perform MFA.</span></span> <span data-ttu-id="e5083-227">If you want to enable MFA for some RADIUS clients but not others, you can configure two NPS servers and install the extension on only one of them.</span><span class="sxs-lookup"><span data-stu-id="e5083-227">If you want to enable MFA for some RADIUS clients but not others, you can configure two NPS servers and install the extension on only one of them.</span></span> <span data-ttu-id="e5083-228">Configure RADIUS clients that you want to require MFA to send requests to the NPS server configured with the extension, and other RADIUS clients to the NPS server not configured with the extension.</span><span class="sxs-lookup"><span data-stu-id="e5083-228">Configure RADIUS clients that you want to require MFA to send requests to the NPS server configured with the extension, and other RADIUS clients to the NPS server not configured with the extension.</span></span>

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a><span data-ttu-id="e5083-229">Prepare for users that aren't enrolled for MFA</span><span class="sxs-lookup"><span data-stu-id="e5083-229">Prepare for users that aren't enrolled for MFA</span></span>

<span data-ttu-id="e5083-230">If you have users that aren't enrolled for MFA, you can determine what happens when they try to authenticate.</span><span class="sxs-lookup"><span data-stu-id="e5083-230">If you have users that aren't enrolled for MFA, you can determine what happens when they try to authenticate.</span></span> <span data-ttu-id="e5083-231">Use the registry setting *REQUIRE_USER_MATCH* in the registry path *HKLM\Software\Microsoft\AzureMFA* to control the feature behavior.</span><span class="sxs-lookup"><span data-stu-id="e5083-231">Use the registry setting *REQUIRE_USER_MATCH* in the registry path *HKLM\Software\Microsoft\AzureMFA* to control the feature behavior.</span></span> <span data-ttu-id="e5083-232">This setting has a single configuration option:</span><span class="sxs-lookup"><span data-stu-id="e5083-232">This setting has a single configuration option:</span></span>

| <span data-ttu-id="e5083-233">Key</span><span class="sxs-lookup"><span data-stu-id="e5083-233">Key</span></span> | <span data-ttu-id="e5083-234">Value</span><span class="sxs-lookup"><span data-stu-id="e5083-234">Value</span></span> | <span data-ttu-id="e5083-235">Default</span><span class="sxs-lookup"><span data-stu-id="e5083-235">Default</span></span> |
| --- | ----- | ------- |
| <span data-ttu-id="e5083-236">REQUIRE_USER_MATCH</span><span class="sxs-lookup"><span data-stu-id="e5083-236">REQUIRE_USER_MATCH</span></span> | <span data-ttu-id="e5083-237">TRUE/FALSE</span><span class="sxs-lookup"><span data-stu-id="e5083-237">TRUE/FALSE</span></span> | <span data-ttu-id="e5083-238">Not set (equivalent to TRUE)</span><span class="sxs-lookup"><span data-stu-id="e5083-238">Not set (equivalent to TRUE)</span></span> |

<span data-ttu-id="e5083-239">The purpose of this setting is to determine what to do when a user is not enrolled for MFA.</span><span class="sxs-lookup"><span data-stu-id="e5083-239">The purpose of this setting is to determine what to do when a user is not enrolled for MFA.</span></span> <span data-ttu-id="e5083-240">When the key does not exist, is not set, or is set to TRUE, and the user is not enrolled, then the extension fails the MFA challenge.</span><span class="sxs-lookup"><span data-stu-id="e5083-240">When the key does not exist, is not set, or is set to TRUE, and the user is not enrolled, then the extension fails the MFA challenge.</span></span> <span data-ttu-id="e5083-241">When the key is set to FALSE and the user is not enrolled, authentication proceeds without performing MFA.</span><span class="sxs-lookup"><span data-stu-id="e5083-241">When the key is set to FALSE and the user is not enrolled, authentication proceeds without performing MFA.</span></span> <span data-ttu-id="e5083-242">If a user is enrolled in MFA, they must authenticate with MFA even if REQUIRE_USER_MATCH is set to FALSE.</span><span class="sxs-lookup"><span data-stu-id="e5083-242">If a user is enrolled in MFA, they must authenticate with MFA even if REQUIRE_USER_MATCH is set to FALSE.</span></span>

<span data-ttu-id="e5083-243">You can choose to create this key and set it to FALSE while your users are onboarding, and may not all be enrolled for Azure MFA yet.</span><span class="sxs-lookup"><span data-stu-id="e5083-243">You can choose to create this key and set it to FALSE while your users are onboarding, and may not all be enrolled for Azure MFA yet.</span></span> <span data-ttu-id="e5083-244">However, since setting the key permits users that aren't enrolled for MFA to sign in, you should remove this key before going to production.</span><span class="sxs-lookup"><span data-stu-id="e5083-244">However, since setting the key permits users that aren't enrolled for MFA to sign in, you should remove this key before going to production.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e5083-245">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="e5083-245">Troubleshooting</span></span>

### <a name="how-do-i-verify-that-the-client-cert-is-installed-as-expected"></a><span data-ttu-id="e5083-246">How do I verify that the client cert is installed as expected?</span><span class="sxs-lookup"><span data-stu-id="e5083-246">How do I verify that the client cert is installed as expected?</span></span>

<span data-ttu-id="e5083-247">Look for the self-signed certificate created by the installer in the cert store, and check that the private key has permissions granted to user **NETWORK SERVICE**.</span><span class="sxs-lookup"><span data-stu-id="e5083-247">Look for the self-signed certificate created by the installer in the cert store, and check that the private key has permissions granted to user **NETWORK SERVICE**.</span></span> <span data-ttu-id="e5083-248">The cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span><span class="sxs-lookup"><span data-stu-id="e5083-248">The cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span></span>

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-to-my-tenant-in-azure-active-directory"></a><span data-ttu-id="e5083-249">How can I verify that my client cert is associated to my tenant in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e5083-249">How can I verify that my client cert is associated to my tenant in Azure Active Directory?</span></span>

<span data-ttu-id="e5083-250">Open PowerShell command prompt and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="e5083-250">Open PowerShell command prompt and run the following commands:</span></span>

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

<span data-ttu-id="e5083-251">These commands print all the certificates associating your tenant with your instance of the NPS extension in your PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="e5083-251">These commands print all the certificates associating your tenant with your instance of the NPS extension in your PowerShell session.</span></span> <span data-ttu-id="e5083-252">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without the private key, and compare it with the list from PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5083-252">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without the private key, and compare it with the list from PowerShell.</span></span>

<span data-ttu-id="e5083-253">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used to filter out obvious misfits if the command returns more than one cert.</span><span class="sxs-lookup"><span data-stu-id="e5083-253">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used to filter out obvious misfits if the command returns more than one cert.</span></span>

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a><span data-ttu-id="e5083-254">Why are my requests failing with ADAL token error?</span><span class="sxs-lookup"><span data-stu-id="e5083-254">Why are my requests failing with ADAL token error?</span></span>

<span data-ttu-id="e5083-255">This error could be due to one of several reasons.</span><span class="sxs-lookup"><span data-stu-id="e5083-255">This error could be due to one of several reasons.</span></span> <span data-ttu-id="e5083-256">Use these steps to help troubleshoot:</span><span class="sxs-lookup"><span data-stu-id="e5083-256">Use these steps to help troubleshoot:</span></span>

1. <span data-ttu-id="e5083-257">Restart your NPS server.</span><span class="sxs-lookup"><span data-stu-id="e5083-257">Restart your NPS server.</span></span>
2. <span data-ttu-id="e5083-258">Verify that client cert is installed as expected.</span><span class="sxs-lookup"><span data-stu-id="e5083-258">Verify that client cert is installed as expected.</span></span>
3. <span data-ttu-id="e5083-259">Verify that the certificate is associated with your tenant on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e5083-259">Verify that the certificate is associated with your tenant on Azure AD.</span></span>
4. <span data-ttu-id="e5083-260">Verify that https://login.microsoftonline.com/ is accessible from the server running the extension.</span><span class="sxs-lookup"><span data-stu-id="e5083-260">Verify that https://login.microsoftonline.com/ is accessible from the server running the extension.</span></span>

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-the-user-is-not-found"></a><span data-ttu-id="e5083-261">Why does authentication fail with an error in HTTP logs stating that the user is not found?</span><span class="sxs-lookup"><span data-stu-id="e5083-261">Why does authentication fail with an error in HTTP logs stating that the user is not found?</span></span>

<span data-ttu-id="e5083-262">Verify that AD Connect is running, and that the user is present in both Windows Active Directory and Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e5083-262">Verify that AD Connect is running, and that the user is present in both Windows Active Directory and Azure Active Directory.</span></span>

-------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a><span data-ttu-id="e5083-263">Why do I see HTTP connect errors in logs with all my authentications failing?</span><span class="sxs-lookup"><span data-stu-id="e5083-263">Why do I see HTTP connect errors in logs with all my authentications failing?</span></span>

<span data-ttu-id="e5083-264">Verify that https://adnotifications.windowsazure.com is reachable from the server running the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="e5083-264">Verify that https://adnotifications.windowsazure.com is reachable from the server running the NPS extension.</span></span>

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a><span data-ttu-id="e5083-265">Managing the TLS/SSL Protocols and Cipher Suites</span><span class="sxs-lookup"><span data-stu-id="e5083-265">Managing the TLS/SSL Protocols and Cipher Suites</span></span>

<span data-ttu-id="e5083-266">It is recommended that older and weaker cipher suites be disabled or removed unless required by your organization.</span><span class="sxs-lookup"><span data-stu-id="e5083-266">It is recommended that older and weaker cipher suites be disabled or removed unless required by your organization.</span></span> <span data-ttu-id="e5083-267">Information on how to complete this task can be found in the article [Managing SSL/TLS Protocols and Cipher Suites for AD FS](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/manage-ssl-protocols-in-ad-fs)</span><span class="sxs-lookup"><span data-stu-id="e5083-267">Information on how to complete this task can be found in the article [Managing SSL/TLS Protocols and Cipher Suites for AD FS](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/manage-ssl-protocols-in-ad-fs)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5083-268">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5083-268">Next steps</span></span>

- <span data-ttu-id="e5083-269">Configure alternate IDs for login, or set up an exception list for IPs that shouldn't perform two-step verification in [Advanced configuration options for the NPS extension for Multi-Factor Authentication](howto-mfa-nps-extension-advanced.md)</span><span class="sxs-lookup"><span data-stu-id="e5083-269">Configure alternate IDs for login, or set up an exception list for IPs that shouldn't perform two-step verification in [Advanced configuration options for the NPS extension for Multi-Factor Authentication](howto-mfa-nps-extension-advanced.md)</span></span>

- <span data-ttu-id="e5083-270">Learn how to integrate [Remote Desktop Gateway](howto-mfa-nps-extension-rdg.md) and [VPN servers](howto-mfa-nps-extension-vpn.md) using the NPS extension</span><span class="sxs-lookup"><span data-stu-id="e5083-270">Learn how to integrate [Remote Desktop Gateway](howto-mfa-nps-extension-rdg.md) and [VPN servers](howto-mfa-nps-extension-vpn.md) using the NPS extension</span></span>

- [<span data-ttu-id="e5083-271">Resolve error messages from the NPS extension for Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="e5083-271">Resolve error messages from the NPS extension for Azure Multi-Factor Authentication</span></span>](howto-mfa-nps-extension-errors.md)
