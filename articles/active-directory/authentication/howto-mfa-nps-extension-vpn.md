---
title: Integrate VPN with Azure MFA by using the Network Policy Server extension | Microsoft Docs
description: Integrate your VPN infrastructure with Azure MFA by using the Network Policy Server extension for Microsoft Azure.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: c1247dfca6dea638da2113fef940b97ad3348b9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856351"
---
# <a name="integrate-your-vpn-infrastructure-with-azure-mfa-by-using-the-network-policy-server-extension-for-azure"></a><span data-ttu-id="ee1cb-103">Integrate your VPN infrastructure with Azure MFA by using the Network Policy Server extension for Azure</span><span class="sxs-lookup"><span data-stu-id="ee1cb-103">Integrate your VPN infrastructure with Azure MFA by using the Network Policy Server extension for Azure</span></span>

## <a name="overview"></a><span data-ttu-id="ee1cb-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ee1cb-104">Overview</span></span>

<span data-ttu-id="ee1cb-105">The Network Policy Server (NPS) extension for Azure allows organizations to safeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using cloud-based [Azure Multi-Factor Authentication (MFA)](howto-mfaserver-nps-rdg.md), which provides two-step verification.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-105">The Network Policy Server (NPS) extension for Azure allows organizations to safeguard Remote Authentication Dial-In User Service (RADIUS) client authentication using cloud-based [Azure Multi-Factor Authentication (MFA)](howto-mfaserver-nps-rdg.md), which provides two-step verification.</span></span>

<span data-ttu-id="ee1cb-106">This article provides instructions for integrating NPS infrastructure with MFA by using the NPS extension for Azure.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-106">This article provides instructions for integrating NPS infrastructure with MFA by using the NPS extension for Azure.</span></span> <span data-ttu-id="ee1cb-107">This process enables secure two-step verification for users who attempt to connect to your network by using a VPN.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-107">This process enables secure two-step verification for users who attempt to connect to your network by using a VPN.</span></span> 

<span data-ttu-id="ee1cb-108">Network Policy and Access Services gives organizations the ability to:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-108">Network Policy and Access Services gives organizations the ability to:</span></span>

* <span data-ttu-id="ee1cb-109">Assign a central location for the management and control of network requests to specify:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-109">Assign a central location for the management and control of network requests to specify:</span></span>

    * <span data-ttu-id="ee1cb-110">Who can connect</span><span class="sxs-lookup"><span data-stu-id="ee1cb-110">Who can connect</span></span> 
    
    * <span data-ttu-id="ee1cb-111">What times of day connections are allowed</span><span class="sxs-lookup"><span data-stu-id="ee1cb-111">What times of day connections are allowed</span></span> 
    
    * <span data-ttu-id="ee1cb-112">The duration of connections</span><span class="sxs-lookup"><span data-stu-id="ee1cb-112">The duration of connections</span></span>
    
    * <span data-ttu-id="ee1cb-113">The level of security that clients must use to connect</span><span class="sxs-lookup"><span data-stu-id="ee1cb-113">The level of security that clients must use to connect</span></span>

    <span data-ttu-id="ee1cb-114">Rather than specify policies on each VPN or Remote Desktop Gateway server, do so after they're in a central location.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-114">Rather than specify policies on each VPN or Remote Desktop Gateway server, do so after they're in a central location.</span></span> <span data-ttu-id="ee1cb-115">The RADIUS protocol is used to provide centralized Authentication, Authorization, and Accounting (AAA).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-115">The RADIUS protocol is used to provide centralized Authentication, Authorization, and Accounting (AAA).</span></span> 

* <span data-ttu-id="ee1cb-116">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access to network resources.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-116">Establish and enforce Network Access Protection (NAP) client health policies that determine whether devices are granted unrestricted or restricted access to network resources.</span></span>

* <span data-ttu-id="ee1cb-117">Provide a way to enforce authentication and authorization for access to 802.1x-capable wireless access points and Ethernet switches.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-117">Provide a way to enforce authentication and authorization for access to 802.1x-capable wireless access points and Ethernet switches.</span></span>   
<span data-ttu-id="ee1cb-118">For more information, see [Network Policy Server](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-118">For more information, see [Network Policy Server](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top).</span></span> 

<span data-ttu-id="ee1cb-119">To enhance security and provide a high level of compliance, organizations can integrate NPS with Azure Multi-Factor Authentication to ensure that users use two-step verification to connect to the virtual port on the VPN server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-119">To enhance security and provide a high level of compliance, organizations can integrate NPS with Azure Multi-Factor Authentication to ensure that users use two-step verification to connect to the virtual port on the VPN server.</span></span> <span data-ttu-id="ee1cb-120">For users to be granted access, they must provide their username and password combination and other information that they control.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-120">For users to be granted access, they must provide their username and password combination and other information that they control.</span></span> <span data-ttu-id="ee1cb-121">This information must be trusted and not easily duplicated.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-121">This information must be trusted and not easily duplicated.</span></span> <span data-ttu-id="ee1cb-122">It can include a cell phone number, a landline number, or an application on a mobile device.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-122">It can include a cell phone number, a landline number, or an application on a mobile device.</span></span>

<span data-ttu-id="ee1cb-123">Prior to the availability of the NPS extension for Azure, customers who wanted to implement two-step verification for integrated NPS and MFA environments had to configure and maintain a separate MFA server in an on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-123">Prior to the availability of the NPS extension for Azure, customers who wanted to implement two-step verification for integrated NPS and MFA environments had to configure and maintain a separate MFA server in an on-premises environment.</span></span> <span data-ttu-id="ee1cb-124">This type of authentication is offered by Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-124">This type of authentication is offered by Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS.</span></span>

<span data-ttu-id="ee1cb-125">With the NPS extension for Azure, organizations can secure RADIUS client authentication by deploying either an on-premises based MFA solution or a cloud-based MFA solution.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-125">With the NPS extension for Azure, organizations can secure RADIUS client authentication by deploying either an on-premises based MFA solution or a cloud-based MFA solution.</span></span>
 
## <a name="authentication-flow"></a><span data-ttu-id="ee1cb-126">Authentication flow</span><span class="sxs-lookup"><span data-stu-id="ee1cb-126">Authentication flow</span></span>
<span data-ttu-id="ee1cb-127">When users connect to a virtual port on a VPN server, they must first authenticate by using a variety of protocols.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-127">When users connect to a virtual port on a VPN server, they must first authenticate by using a variety of protocols.</span></span> <span data-ttu-id="ee1cb-128">The protocols allow the use of a combination of user name and password and certificate-based authentication methods.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-128">The protocols allow the use of a combination of user name and password and certificate-based authentication methods.</span></span> 

<span data-ttu-id="ee1cb-129">In addition to authenticating and verifying their identity, users must have the appropriate dial-in permissions.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-129">In addition to authenticating and verifying their identity, users must have the appropriate dial-in permissions.</span></span> <span data-ttu-id="ee1cb-130">In simple implementations, dial-in permissions that allow access are set directly on the Active Directory user objects.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-130">In simple implementations, dial-in permissions that allow access are set directly on the Active Directory user objects.</span></span> 

![User properties](./media/howto-mfa-nps-extension-vpn/image1.png)

<span data-ttu-id="ee1cb-132">In simple implementations, each VPN server grants or denies access based on policies that are defined on each local VPN server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-132">In simple implementations, each VPN server grants or denies access based on policies that are defined on each local VPN server.</span></span>

<span data-ttu-id="ee1cb-133">In larger and more scalable implementations, the policies that grant or deny VPN access are centralized on RADIUS servers.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-133">In larger and more scalable implementations, the policies that grant or deny VPN access are centralized on RADIUS servers.</span></span> <span data-ttu-id="ee1cb-134">In these cases, the VPN server acts as an access server (RADIUS client) that forwards connection requests and account messages to a RADIUS server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-134">In these cases, the VPN server acts as an access server (RADIUS client) that forwards connection requests and account messages to a RADIUS server.</span></span> <span data-ttu-id="ee1cb-135">To connect to the virtual port on the VPN server, users must be authenticated and meet the conditions that are defined centrally on RADIUS servers.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-135">To connect to the virtual port on the VPN server, users must be authenticated and meet the conditions that are defined centrally on RADIUS servers.</span></span> 

<span data-ttu-id="ee1cb-136">When the NPS extension for Azure is integrated with the NPS, a successful authentication flow results, as follows:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-136">When the NPS extension for Azure is integrated with the NPS, a successful authentication flow results, as follows:</span></span>

1. <span data-ttu-id="ee1cb-137">The VPN server receives an authentication request from a VPN user that includes the username and password for connecting to a resource, such as a Remote Desktop session.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-137">The VPN server receives an authentication request from a VPN user that includes the username and password for connecting to a resource, such as a Remote Desktop session.</span></span> 

2. <span data-ttu-id="ee1cb-138">Acting as a RADIUS client, the VPN server converts the request to a RADIUS *Access-Request* message and sends it (with an encrypted password) to the RADIUS server where the NPS extension is installed.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-138">Acting as a RADIUS client, the VPN server converts the request to a RADIUS *Access-Request* message and sends it (with an encrypted password) to the RADIUS server where the NPS extension is installed.</span></span> 

3. <span data-ttu-id="ee1cb-139">The username and password combination is verified in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-139">The username and password combination is verified in Active Directory.</span></span> <span data-ttu-id="ee1cb-140">If either the username or password is incorrect, the RADIUS Server sends an *Access-Reject* message.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-140">If either the username or password is incorrect, the RADIUS Server sends an *Access-Reject* message.</span></span> 

4. <span data-ttu-id="ee1cb-141">If all conditions, as specified in the NPS Connection Request and Network Policies, are met (for example, time of day or group membership restrictions), the NPS extension triggers a request for secondary authentication with Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-141">If all conditions, as specified in the NPS Connection Request and Network Policies, are met (for example, time of day or group membership restrictions), the NPS extension triggers a request for secondary authentication with Azure Multi-Factor Authentication.</span></span> 

5. <span data-ttu-id="ee1cb-142">Azure Multi-Factor Authentication communicates with Azure Active Directory, retrieves the user’s details, and performs the secondary authentication by using the method that's configured by the user (cell phone call, text message, or mobile app).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-142">Azure Multi-Factor Authentication communicates with Azure Active Directory, retrieves the user’s details, and performs the secondary authentication by using the method that's configured by the user (cell phone call, text message, or mobile app).</span></span> 

6. <span data-ttu-id="ee1cb-143">When the MFA challenge is successful, Azure Multi-Factor Authentication communicates the result to the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-143">When the MFA challenge is successful, Azure Multi-Factor Authentication communicates the result to the NPS extension.</span></span>

7. <span data-ttu-id="ee1cb-144">After the connection attempt is both authenticated and authorized, the NPS where the extension is installed sends a RADIUS *Access-Accept* message to the VPN server (RADIUS client).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-144">After the connection attempt is both authenticated and authorized, the NPS where the extension is installed sends a RADIUS *Access-Accept* message to the VPN server (RADIUS client).</span></span>

8. <span data-ttu-id="ee1cb-145">The user is granted access to the virtual port on the VPN server and establishes an encrypted VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-145">The user is granted access to the virtual port on the VPN server and establishes an encrypted VPN tunnel.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee1cb-146">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee1cb-146">Prerequisites</span></span>
<span data-ttu-id="ee1cb-147">This section details the prerequisites that must be completed before you can integrate MFA with the Remote Desktop Gateway.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-147">This section details the prerequisites that must be completed before you can integrate MFA with the Remote Desktop Gateway.</span></span> <span data-ttu-id="ee1cb-148">Before you begin, you must have the following prerequisites in place:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-148">Before you begin, you must have the following prerequisites in place:</span></span>

* <span data-ttu-id="ee1cb-149">VPN infrastructure</span><span class="sxs-lookup"><span data-stu-id="ee1cb-149">VPN infrastructure</span></span>
* <span data-ttu-id="ee1cb-150">Network Policy and Access Services role</span><span class="sxs-lookup"><span data-stu-id="ee1cb-150">Network Policy and Access Services role</span></span>
* <span data-ttu-id="ee1cb-151">Azure Multi-Factor Authentication license</span><span class="sxs-lookup"><span data-stu-id="ee1cb-151">Azure Multi-Factor Authentication license</span></span>
* <span data-ttu-id="ee1cb-152">Windows Server software</span><span class="sxs-lookup"><span data-stu-id="ee1cb-152">Windows Server software</span></span>
* <span data-ttu-id="ee1cb-153">Libraries</span><span class="sxs-lookup"><span data-stu-id="ee1cb-153">Libraries</span></span>
* <span data-ttu-id="ee1cb-154">Azure Active Directory (Azure AD) synced with on-premises Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee1cb-154">Azure Active Directory (Azure AD) synced with on-premises Active Directory</span></span> 
* <span data-ttu-id="ee1cb-155">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="ee1cb-155">Azure Active Directory GUID ID</span></span>

### <a name="vpn-infrastructure"></a><span data-ttu-id="ee1cb-156">VPN infrastructure</span><span class="sxs-lookup"><span data-stu-id="ee1cb-156">VPN infrastructure</span></span>
<span data-ttu-id="ee1cb-157">This article assumes that you have a working VPN infrastructure that uses Microsoft Windows Server 2016 and that your VPN server is currently not configured to forward connection requests to a RADIUS server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-157">This article assumes that you have a working VPN infrastructure that uses Microsoft Windows Server 2016 and that your VPN server is currently not configured to forward connection requests to a RADIUS server.</span></span> <span data-ttu-id="ee1cb-158">In the article, you configure the VPN infrastructure to use a central RADIUS server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-158">In the article, you configure the VPN infrastructure to use a central RADIUS server.</span></span>

<span data-ttu-id="ee1cb-159">If you do not have a working VPN infrastructure in place, you can quickly create one by following the guidance in numerous VPN setup tutorials that you can find on the Microsoft and third-party sites.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-159">If you do not have a working VPN infrastructure in place, you can quickly create one by following the guidance in numerous VPN setup tutorials that you can find on the Microsoft and third-party sites.</span></span> 
            
### <a name="the-network-policy-and-access-services-role"></a><span data-ttu-id="ee1cb-160">The Network Policy and Access Services role</span><span class="sxs-lookup"><span data-stu-id="ee1cb-160">The Network Policy and Access Services role</span></span>

<span data-ttu-id="ee1cb-161">Network Policy and Access Services provides the RADIUS server and client functionality.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-161">Network Policy and Access Services provides the RADIUS server and client functionality.</span></span> <span data-ttu-id="ee1cb-162">This article assumes that you have installed the Network Policy and Access Services role on a member server or domain controller in your environment.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-162">This article assumes that you have installed the Network Policy and Access Services role on a member server or domain controller in your environment.</span></span> <span data-ttu-id="ee1cb-163">In this guide, you configure RADIUS for a VPN configuration.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-163">In this guide, you configure RADIUS for a VPN configuration.</span></span> <span data-ttu-id="ee1cb-164">Install the Network Policy and Access Services role on a server *other than* your VPN server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-164">Install the Network Policy and Access Services role on a server *other than* your VPN server.</span></span>

<span data-ttu-id="ee1cb-165">For information about installing the Network Policy and Access Services role service Windows Server 2012 or later, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-165">For information about installing the Network Policy and Access Services role service Windows Server 2012 or later, see [Install a NAP Health Policy Server](https://technet.microsoft.com/library/dd296890.aspx).</span></span> <span data-ttu-id="ee1cb-166">NAP is deprecated in Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-166">NAP is deprecated in Windows Server 2016.</span></span> <span data-ttu-id="ee1cb-167">For a description of best practices for NPS, including the recommendation to install NPS on a domain controller, see [Best practices for NPS](https://technet.microsoft.com/library/cc771746).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-167">For a description of best practices for NPS, including the recommendation to install NPS on a domain controller, see [Best practices for NPS](https://technet.microsoft.com/library/cc771746).</span></span>

### <a name="azure-mfa-license"></a><span data-ttu-id="ee1cb-168">Azure MFA License</span><span class="sxs-lookup"><span data-stu-id="ee1cb-168">Azure MFA License</span></span>

<span data-ttu-id="ee1cb-169">A license is required for Azure Multi-Factor Authentication, and it is available through an Azure AD Premium, Enterprise Mobility + Security, or a Multi-Factor Authentication stand-alone license.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-169">A license is required for Azure Multi-Factor Authentication, and it is available through an Azure AD Premium, Enterprise Mobility + Security, or a Multi-Factor Authentication stand-alone license.</span></span> <span data-ttu-id="ee1cb-170">Consumption-based licenses for Azure MFA such as per user or per authentication licenses are not compatible with the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-170">Consumption-based licenses for Azure MFA such as per user or per authentication licenses are not compatible with the NPS extension.</span></span> <span data-ttu-id="ee1cb-171">For more information, see [How to get Azure Multi-Factor Authentication](concept-mfa-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-171">For more information, see [How to get Azure Multi-Factor Authentication](concept-mfa-licensing.md).</span></span> <span data-ttu-id="ee1cb-172">For testing purposes, you can use a trial subscription.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-172">For testing purposes, you can use a trial subscription.</span></span>

### <a name="windows-server-software"></a><span data-ttu-id="ee1cb-173">Windows Server software</span><span class="sxs-lookup"><span data-stu-id="ee1cb-173">Windows Server software</span></span>

<span data-ttu-id="ee1cb-174">The NPS extension requires Windows Server 2008 R2 SP1 or later, with the Network Policy and Access Services role installed.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-174">The NPS extension requires Windows Server 2008 R2 SP1 or later, with the Network Policy and Access Services role installed.</span></span> <span data-ttu-id="ee1cb-175">All the steps in this guide were performed with Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-175">All the steps in this guide were performed with Windows Server 2016.</span></span>

### <a name="libraries"></a><span data-ttu-id="ee1cb-176">Libraries</span><span class="sxs-lookup"><span data-stu-id="ee1cb-176">Libraries</span></span>

<span data-ttu-id="ee1cb-177">The following libraries are installed automatically with the NPS extension:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-177">The following libraries are installed automatically with the NPS extension:</span></span>

-   [<span data-ttu-id="ee1cb-178">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span><span class="sxs-lookup"><span data-stu-id="ee1cb-178">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
-   [<span data-ttu-id="ee1cb-179">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span><span class="sxs-lookup"><span data-stu-id="ee1cb-179">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

<span data-ttu-id="ee1cb-180">If the Microsoft Azure Active Directory PowerShell Module is not already present, it is installed with a configuration script that you run as part of the setup process.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-180">If the Microsoft Azure Active Directory PowerShell Module is not already present, it is installed with a configuration script that you run as part of the setup process.</span></span> <span data-ttu-id="ee1cb-181">There is no need to install the module ahead of time if it is not already installed.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-181">There is no need to install the module ahead of time if it is not already installed.</span></span>

### <a name="azure-active-directory-synced-with-on-premises-active-directory"></a><span data-ttu-id="ee1cb-182">Azure Active Directory synced with on-premises Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee1cb-182">Azure Active Directory synced with on-premises Active Directory</span></span> 

<span data-ttu-id="ee1cb-183">To use the NPS extension, on-premises users must be synced with Azure Active Directory and enabled for MFA.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-183">To use the NPS extension, on-premises users must be synced with Azure Active Directory and enabled for MFA.</span></span> <span data-ttu-id="ee1cb-184">This guide assumes that on-premises users are synced with Azure Active Directory via Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-184">This guide assumes that on-premises users are synced with Azure Active Directory via Azure AD Connect.</span></span> <span data-ttu-id="ee1cb-185">Instructions for enabling users for MFA are provided below.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-185">Instructions for enabling users for MFA are provided below.</span></span>

<span data-ttu-id="ee1cb-186">For information about Azure AD Connect, see [Integrate your on-premises directories with Azure Active Directory](../connect/active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-186">For information about Azure AD Connect, see [Integrate your on-premises directories with Azure Active Directory](../connect/active-directory-aadconnect.md).</span></span> 

### <a name="azure-active-directory-guid-id"></a><span data-ttu-id="ee1cb-187">Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="ee1cb-187">Azure Active Directory GUID ID</span></span> 

<span data-ttu-id="ee1cb-188">To install the NPS extension, you need to know the GUID of the Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-188">To install the NPS extension, you need to know the GUID of the Azure Active Directory.</span></span> <span data-ttu-id="ee1cb-189">Instructions for finding the GUID of the Azure Active Directory are provided in the next section.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-189">Instructions for finding the GUID of the Azure Active Directory are provided in the next section.</span></span>

## <a name="configure-radius-for-vpn-connections"></a><span data-ttu-id="ee1cb-190">Configure RADIUS for VPN connections</span><span class="sxs-lookup"><span data-stu-id="ee1cb-190">Configure RADIUS for VPN connections</span></span>

<span data-ttu-id="ee1cb-191">If you have installed the NPS role on a member server, you need to configure it to authenticate and authorize the VPN client that requests VPN connections.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-191">If you have installed the NPS role on a member server, you need to configure it to authenticate and authorize the VPN client that requests VPN connections.</span></span> 

<span data-ttu-id="ee1cb-192">This section assumes that you have installed the Network Policy and Access Services role but have not configured it for use in your infrastructure.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-192">This section assumes that you have installed the Network Policy and Access Services role but have not configured it for use in your infrastructure.</span></span>

> [!NOTE]
> <span data-ttu-id="ee1cb-193">If you already have a working VPN server that uses a centralized RADIUS server for authentication, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-193">If you already have a working VPN server that uses a centralized RADIUS server for authentication, you can skip this section.</span></span>
>

### <a name="register-server-in-active-directory"></a><span data-ttu-id="ee1cb-194">Register Server in Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee1cb-194">Register Server in Active Directory</span></span>
<span data-ttu-id="ee1cb-195">To function properly in this scenario, the NPS server must be registered in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-195">To function properly in this scenario, the NPS server must be registered in Active Directory.</span></span>

1. <span data-ttu-id="ee1cb-196">Open Server Manager.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-196">Open Server Manager.</span></span>

2. <span data-ttu-id="ee1cb-197">In Server Manager, select **Tools**, and then select **Network Policy Server**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-197">In Server Manager, select **Tools**, and then select **Network Policy Server**.</span></span> 

3. <span data-ttu-id="ee1cb-198">In the Network Policy Server console, right-click **NPS (Local)**, and then select **Register server in Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-198">In the Network Policy Server console, right-click **NPS (Local)**, and then select **Register server in Active Directory**.</span></span> <span data-ttu-id="ee1cb-199">Select **OK** two times.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-199">Select **OK** two times.</span></span>

    ![Network Policy Server](./media/howto-mfa-nps-extension-vpn/image2.png)

4. <span data-ttu-id="ee1cb-201">Leave the console open for the next procedure.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-201">Leave the console open for the next procedure.</span></span>

### <a name="use-wizard-to-configure-the-radius-server"></a><span data-ttu-id="ee1cb-202">Use wizard to configure the RADIUS server</span><span class="sxs-lookup"><span data-stu-id="ee1cb-202">Use wizard to configure the RADIUS server</span></span>
<span data-ttu-id="ee1cb-203">You can use a standard (wizard-based) or advanced configuration option to configure the RADIUS server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-203">You can use a standard (wizard-based) or advanced configuration option to configure the RADIUS server.</span></span> <span data-ttu-id="ee1cb-204">This section assumes that you're using the wizard-based standard configuration option.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-204">This section assumes that you're using the wizard-based standard configuration option.</span></span>

1. <span data-ttu-id="ee1cb-205">In the Network Policy Server console, select **NPS (Local)**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-205">In the Network Policy Server console, select **NPS (Local)**.</span></span>

2. <span data-ttu-id="ee1cb-206">Under **Standard Configuration**, select **RADIUS Server for Dial-Up or VPN Connections**, and then select **Configure VPN or Dial-Up**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-206">Under **Standard Configuration**, select **RADIUS Server for Dial-Up or VPN Connections**, and then select **Configure VPN or Dial-Up**.</span></span>

    ![Configure VPN](./media/howto-mfa-nps-extension-vpn/image3.png)

3. <span data-ttu-id="ee1cb-208">In the **Select Dial-up or Virtual Private Network Connections Type** window, select **Virtual Private Network Connections**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-208">In the **Select Dial-up or Virtual Private Network Connections Type** window, select **Virtual Private Network Connections**, and then select **Next**.</span></span>

    ![Virtual private network](./media/howto-mfa-nps-extension-vpn/image4.png)

4. <span data-ttu-id="ee1cb-210">In the **Specify Dial-Up or VPN Server** window, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-210">In the **Specify Dial-Up or VPN Server** window, select **Add**.</span></span>

5. <span data-ttu-id="ee1cb-211">In the **New RADIUS client** window, provide a friendly name, enter the resolvable name or IP address of the VPN server, and then enter a shared secret password.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-211">In the **New RADIUS client** window, provide a friendly name, enter the resolvable name or IP address of the VPN server, and then enter a shared secret password.</span></span> <span data-ttu-id="ee1cb-212">Make the shared secret password long and complex.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-212">Make the shared secret password long and complex.</span></span> <span data-ttu-id="ee1cb-213">Record it, because you'll need it in the next section.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-213">Record it, because you'll need it in the next section.</span></span>

    ![New RADIUS client](./media/howto-mfa-nps-extension-vpn/image5.png)

6. <span data-ttu-id="ee1cb-215">Select **OK**, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-215">Select **OK**, and then select **Next**.</span></span>

7. <span data-ttu-id="ee1cb-216">In the **Configure Authentication Methods** window, accept the default selection (**Microsoft Encrypted Authentication version 2 [MS-CHAPv2])** or choose another option, and select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-216">In the **Configure Authentication Methods** window, accept the default selection (**Microsoft Encrypted Authentication version 2 [MS-CHAPv2])** or choose another option, and select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee1cb-217">If you configure Extensible Authentication Protocol (EAP), you must use either Microsoft Challenge-Handshake Authentication Protocol (CHAPv2) or Protected Extensible Authentication Protocol (PEAP).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-217">If you configure Extensible Authentication Protocol (EAP), you must use either Microsoft Challenge-Handshake Authentication Protocol (CHAPv2) or Protected Extensible Authentication Protocol (PEAP).</span></span> <span data-ttu-id="ee1cb-218">No other EAP is supported.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-218">No other EAP is supported.</span></span>
 
8. <span data-ttu-id="ee1cb-219">In the **Specify User Groups** window, select **Add**, and then select an appropriate group.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-219">In the **Specify User Groups** window, select **Add**, and then select an appropriate group.</span></span> <span data-ttu-id="ee1cb-220">If no group exists, leave the selection blank to grant access to all users.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-220">If no group exists, leave the selection blank to grant access to all users.</span></span>

    ![The Specify User Groups window](./media/howto-mfa-nps-extension-vpn/image7.png)

9. <span data-ttu-id="ee1cb-222">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-222">Select **Next**.</span></span>

10. <span data-ttu-id="ee1cb-223">In the **Specify IP Filters** window, select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-223">In the **Specify IP Filters** window, select **Next**.</span></span>

11. <span data-ttu-id="ee1cb-224">In the **Specify Encryption Settings** window, accept the default settings, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-224">In the **Specify Encryption Settings** window, accept the default settings, and then select **Next**.</span></span>

    ![The Specify Encryption Settings window](./media/howto-mfa-nps-extension-vpn/image8.png)

12. <span data-ttu-id="ee1cb-226">In the **Specify a Realm Name** window, leave the realm name blank, accept the default setting, and then select **Next**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-226">In the **Specify a Realm Name** window, leave the realm name blank, accept the default setting, and then select **Next**.</span></span>

    ![The Specify a Realm Name window](./media/howto-mfa-nps-extension-vpn/image9.png)

13. <span data-ttu-id="ee1cb-228">In the **Completing New Dial-up or Virtual Private Network Connections and RADIUS clients** window, select **Finish**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-228">In the **Completing New Dial-up or Virtual Private Network Connections and RADIUS clients** window, select **Finish**.</span></span>

    ![The "Completing New Dial-up or Virtual Private Network Connections and RADIUS clients" window](./media/howto-mfa-nps-extension-vpn/image10.png)

### <a name="verify-the-radius-configuration"></a><span data-ttu-id="ee1cb-230">Verify the RADIUS configuration</span><span class="sxs-lookup"><span data-stu-id="ee1cb-230">Verify the RADIUS configuration</span></span>
<span data-ttu-id="ee1cb-231">This section details the configuration you created by using the wizard.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-231">This section details the configuration you created by using the wizard.</span></span>

1. <span data-ttu-id="ee1cb-232">On the Network Policy Server, in the NPS (local) console, expand **RADIUS Clients**, and then select **RADIUS Clients**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-232">On the Network Policy Server, in the NPS (local) console, expand **RADIUS Clients**, and then select **RADIUS Clients**.</span></span>

2. <span data-ttu-id="ee1cb-233">In the details pane, right-click the RADIUS client that you created, and then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-233">In the details pane, right-click the RADIUS client that you created, and then select **Properties**.</span></span> <span data-ttu-id="ee1cb-234">The properties of your RADIUS client (the VPN server) should be like those shown here:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-234">The properties of your RADIUS client (the VPN server) should be like those shown here:</span></span>

    ![VPN properties](./media/howto-mfa-nps-extension-vpn/image11.png)

3. <span data-ttu-id="ee1cb-236">Select **Cancel**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-236">Select **Cancel**.</span></span>

4. <span data-ttu-id="ee1cb-237">On the Network Policy Server, in the NPS (local) console, expand **Policies**, and then select **Connection Request Policies**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-237">On the Network Policy Server, in the NPS (local) console, expand **Policies**, and then select **Connection Request Policies**.</span></span> <span data-ttu-id="ee1cb-238">The VPN Connections policy is displayed as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-238">The VPN Connections policy is displayed as shown in the following image:</span></span>

    ![Connection requests](./media/howto-mfa-nps-extension-vpn/image12.png)

5. <span data-ttu-id="ee1cb-240">Under **Policies**, select **Network Policies**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-240">Under **Policies**, select **Network Policies**.</span></span> <span data-ttu-id="ee1cb-241">You should see a Virtual Private Network (VPN) Connections policy that resembles the policy shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-241">You should see a Virtual Private Network (VPN) Connections policy that resembles the policy shown in the following image:</span></span>

    ![Network Policies](./media/howto-mfa-nps-extension-vpn/image13.png)

## <a name="configure-your-vpn-server-to-use-radius-authentication"></a><span data-ttu-id="ee1cb-243">Configure your VPN server to use RADIUS authentication</span><span class="sxs-lookup"><span data-stu-id="ee1cb-243">Configure your VPN server to use RADIUS authentication</span></span>
<span data-ttu-id="ee1cb-244">In this section, you configure your VPN server to use RADIUS authentication.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-244">In this section, you configure your VPN server to use RADIUS authentication.</span></span> <span data-ttu-id="ee1cb-245">The instructions assume that you have a working configuration of a VPN server but have not configured it to use RADIUS authentication.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-245">The instructions assume that you have a working configuration of a VPN server but have not configured it to use RADIUS authentication.</span></span> <span data-ttu-id="ee1cb-246">After you configure the VPN server, confirm that your configuration is working as expected.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-246">After you configure the VPN server, confirm that your configuration is working as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="ee1cb-247">If you already have a working VPN server configuration that uses RADIUS authentication, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-247">If you already have a working VPN server configuration that uses RADIUS authentication, you can skip this section.</span></span>
>

### <a name="configure-authentication-provider"></a><span data-ttu-id="ee1cb-248">Configure authentication provider</span><span class="sxs-lookup"><span data-stu-id="ee1cb-248">Configure authentication provider</span></span>
1. <span data-ttu-id="ee1cb-249">On the VPN server, open Server Manager.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-249">On the VPN server, open Server Manager.</span></span>

2. <span data-ttu-id="ee1cb-250">In Server Manager, select **Tools**, and then select **Routing and Remote Access**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-250">In Server Manager, select **Tools**, and then select **Routing and Remote Access**.</span></span>

3. <span data-ttu-id="ee1cb-251">In the **Routing and Remote Access** window, right-click **\<server name> (local)**, and then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-251">In the **Routing and Remote Access** window, right-click **\<server name> (local)**, and then select **Properties**.</span></span>

    ![The Routing and Remote Access window](./media/howto-mfa-nps-extension-vpn/image14.png)
 
4. <span data-ttu-id="ee1cb-253">In the **\<server name> (local) Properties** window, select the **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-253">In the **\<server name> (local) Properties** window, select the **Security** tab.</span></span> 

5. <span data-ttu-id="ee1cb-254">On the **Security** tab, under **Authentication provider**, select **RADIUS Authentication**, and then select **Configure**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-254">On the **Security** tab, under **Authentication provider**, select **RADIUS Authentication**, and then select **Configure**.</span></span>

    ![RADIUS Authentication](./media/howto-mfa-nps-extension-vpn/image15.png)
 
6. <span data-ttu-id="ee1cb-256">In the **RADIUS Authentication** window, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-256">In the **RADIUS Authentication** window, select **Add**.</span></span>

7. <span data-ttu-id="ee1cb-257">In the **Add RADIUS Server** window, do the following:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-257">In the **Add RADIUS Server** window, do the following:</span></span>

    <span data-ttu-id="ee1cb-258">a.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-258">a.</span></span> <span data-ttu-id="ee1cb-259">In the **Server name** box, enter the name or IP address of the RADIUS server that you configured in the previous section.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-259">In the **Server name** box, enter the name or IP address of the RADIUS server that you configured in the previous section.</span></span>

    <span data-ttu-id="ee1cb-260">b.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-260">b.</span></span> <span data-ttu-id="ee1cb-261">For the **Shared secret**, select **Change**, and then enter the shared secret password that you created and recorded earlier.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-261">For the **Shared secret**, select **Change**, and then enter the shared secret password that you created and recorded earlier.</span></span>

    <span data-ttu-id="ee1cb-262">c.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-262">c.</span></span> <span data-ttu-id="ee1cb-263">In the **Time-out (seconds)** box, select a value from **30** through **60**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-263">In the **Time-out (seconds)** box, select a value from **30** through **60**.</span></span>  
    <span data-ttu-id="ee1cb-264">The timeout value is necessary to allow enough time to complete the second authentication factor.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-264">The timeout value is necessary to allow enough time to complete the second authentication factor.</span></span>
 
    ![The Add RADIUS Server window](./media/howto-mfa-nps-extension-vpn/image16.png)
 
8. <span data-ttu-id="ee1cb-266">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-266">Select **OK**.</span></span>

### <a name="test-vpn-connectivity"></a><span data-ttu-id="ee1cb-267">Test VPN connectivity</span><span class="sxs-lookup"><span data-stu-id="ee1cb-267">Test VPN connectivity</span></span>
<span data-ttu-id="ee1cb-268">In this section, you confirm that the VPN client is authenticated and authorized by the RADIUS server when you attempt to connect to the VPN virtual port.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-268">In this section, you confirm that the VPN client is authenticated and authorized by the RADIUS server when you attempt to connect to the VPN virtual port.</span></span> <span data-ttu-id="ee1cb-269">The instructions assume that you are using Windows 10 as a VPN client.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-269">The instructions assume that you are using Windows 10 as a VPN client.</span></span> 

> [!NOTE]
> <span data-ttu-id="ee1cb-270">If you already configured a VPN client to connect to the VPN server and have saved the settings, you can skip the steps related to configuring and saving a VPN connection object.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-270">If you already configured a VPN client to connect to the VPN server and have saved the settings, you can skip the steps related to configuring and saving a VPN connection object.</span></span>
>

1. <span data-ttu-id="ee1cb-271">On your VPN client computer, select the **Start** button, and then select the **Settings** button.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-271">On your VPN client computer, select the **Start** button, and then select the **Settings** button.</span></span>

2. <span data-ttu-id="ee1cb-272">In the **Windows Settings** window, select **Network & Internet**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-272">In the **Windows Settings** window, select **Network & Internet**.</span></span>

3. <span data-ttu-id="ee1cb-273">Select **VPN**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-273">Select **VPN**.</span></span>

4. <span data-ttu-id="ee1cb-274">Select **Add a VPN connection**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-274">Select **Add a VPN connection**.</span></span>

5. <span data-ttu-id="ee1cb-275">In the **Add a VPN connection** window, in the **VPN provider** box, select **Windows (built-in)**, complete the remaining fields, as appropriate, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-275">In the **Add a VPN connection** window, in the **VPN provider** box, select **Windows (built-in)**, complete the remaining fields, as appropriate, and then select **Save**.</span></span> 

    ![The "Add a VPN connection" window](./media/howto-mfa-nps-extension-vpn/image17.png)
 
6. <span data-ttu-id="ee1cb-277">Go to **Control Panel**, and then select **Network and Sharing Center**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-277">Go to **Control Panel**, and then select **Network and Sharing Center**.</span></span>

7. <span data-ttu-id="ee1cb-278">Select **Change adapter settings**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-278">Select **Change adapter settings**.</span></span>

    ![Change adapter settings](./media/howto-mfa-nps-extension-vpn/image18.png)

8. <span data-ttu-id="ee1cb-280">Right-click the VPN network connection, and then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-280">Right-click the VPN network connection, and then select **Properties**.</span></span> 

    ![VPN Network Properties](./media/howto-mfa-nps-extension-vpn/image19.png)

9. <span data-ttu-id="ee1cb-282">In the VPN properties window, select the **Security** tab.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-282">In the VPN properties window, select the **Security** tab.</span></span> 

10. <span data-ttu-id="ee1cb-283">On the **Security** tab, ensure that only **Microsoft CHAP Version 2 (MS-CHAP v2)** is selected, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-283">On the **Security** tab, ensure that only **Microsoft CHAP Version 2 (MS-CHAP v2)** is selected, and then select **OK**.</span></span>

    ![The "Allow  these protocols" option](./media/howto-mfa-nps-extension-vpn/image20.png)

11. <span data-ttu-id="ee1cb-285">Right-click the VPN connection, and then select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-285">Right-click the VPN connection, and then select **Connect**.</span></span>

12. <span data-ttu-id="ee1cb-286">In the **Settings** window, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-286">In the **Settings** window, select **Connect**.</span></span>  
    <span data-ttu-id="ee1cb-287">A successful connection appears in the Security log on the RADIUS server as Event ID 6272, as shown here:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-287">A successful connection appears in the Security log on the RADIUS server as Event ID 6272, as shown here:</span></span>

    ![The Event Properties window](./media/howto-mfa-nps-extension-vpn/image21.png)

## <a name="troubleshooting-radius"></a><span data-ttu-id="ee1cb-289">Troubleshooting RADIUS</span><span class="sxs-lookup"><span data-stu-id="ee1cb-289">Troubleshooting RADIUS</span></span>

<span data-ttu-id="ee1cb-290">Assume that your VPN configuration was working before you configured the VPN server to use a centralized RADIUS server for authentication and authorization.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-290">Assume that your VPN configuration was working before you configured the VPN server to use a centralized RADIUS server for authentication and authorization.</span></span> <span data-ttu-id="ee1cb-291">If the configuration was working, it is likely that the issue is caused by a misconfiguration of the RADIUS server or the use of an invalid username or password.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-291">If the configuration was working, it is likely that the issue is caused by a misconfiguration of the RADIUS server or the use of an invalid username or password.</span></span> <span data-ttu-id="ee1cb-292">For example, if you use the alternate UPN suffix in the username, the sign-in attempt might fail.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-292">For example, if you use the alternate UPN suffix in the username, the sign-in attempt might fail.</span></span> <span data-ttu-id="ee1cb-293">Use the same account name for best results.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-293">Use the same account name for best results.</span></span> 

<span data-ttu-id="ee1cb-294">To troubleshoot these issues, an ideal place to start is to examine the Security event logs on the RADIUS server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-294">To troubleshoot these issues, an ideal place to start is to examine the Security event logs on the RADIUS server.</span></span> <span data-ttu-id="ee1cb-295">To save time searching for events, you can use the role-based Network Policy and Access Server custom view in Event Viewer, as shown here.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-295">To save time searching for events, you can use the role-based Network Policy and Access Server custom view in Event Viewer, as shown here.</span></span> <span data-ttu-id="ee1cb-296">"Event ID 6273" indicates events where the NPS denied access to a user.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-296">"Event ID 6273" indicates events where the NPS denied access to a user.</span></span> 

![Event Viewer](./media/howto-mfa-nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a><span data-ttu-id="ee1cb-298">Configure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ee1cb-298">Configure Multi-Factor Authentication</span></span>

<span data-ttu-id="ee1cb-299">For assistance configuring users for Multi-Factor Authentication see the articles [How to require two-step verification for a user or group](howto-mfa-userstates.md) and [Set up my account for two-step verification](../user-help/multi-factor-authentication-end-user-first-time.md)</span><span class="sxs-lookup"><span data-stu-id="ee1cb-299">For assistance configuring users for Multi-Factor Authentication see the articles [How to require two-step verification for a user or group](howto-mfa-userstates.md) and [Set up my account for two-step verification](../user-help/multi-factor-authentication-end-user-first-time.md)</span></span>

## <a name="install-and-configure-the-nps-extension"></a><span data-ttu-id="ee1cb-300">Install and configure the NPS extension</span><span class="sxs-lookup"><span data-stu-id="ee1cb-300">Install and configure the NPS extension</span></span>

<span data-ttu-id="ee1cb-301">This section provides instructions for configuring VPN to use MFA for client authentication with the VPN server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-301">This section provides instructions for configuring VPN to use MFA for client authentication with the VPN server.</span></span>

<span data-ttu-id="ee1cb-302">After you install and configure the NPS extension, all RADIUS-based client authentication that is processed by this server is required to use MFA.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-302">After you install and configure the NPS extension, all RADIUS-based client authentication that is processed by this server is required to use MFA.</span></span> <span data-ttu-id="ee1cb-303">If all your VPN users are not enrolled in Azure Multi-Factor Authentication, you can do either of the following:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-303">If all your VPN users are not enrolled in Azure Multi-Factor Authentication, you can do either of the following:</span></span>

* <span data-ttu-id="ee1cb-304">Set up another RADIUS server to authenticate users who are not configured to use MFA.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-304">Set up another RADIUS server to authenticate users who are not configured to use MFA.</span></span> 

* <span data-ttu-id="ee1cb-305">Create a registry entry that allows challenged users to provide a second authentication factor if they are enrolled in Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-305">Create a registry entry that allows challenged users to provide a second authentication factor if they are enrolled in Azure Multi-Factor Authentication.</span></span> 

<span data-ttu-id="ee1cb-306">Create a new string value named _REQUIRE_USER_MATCH in HKLM\SOFTWARE\Microsoft\AzureMfa_, and set the value to *True* or *False*.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-306">Create a new string value named _REQUIRE_USER_MATCH in HKLM\SOFTWARE\Microsoft\AzureMfa_, and set the value to *True* or *False*.</span></span> 

![The "Require User Match" setting](./media/howto-mfa-nps-extension-vpn/image34.png)
 
<span data-ttu-id="ee1cb-308">If the value is set to *True* or is blank, all authentication requests are subject to an MFA challenge.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-308">If the value is set to *True* or is blank, all authentication requests are subject to an MFA challenge.</span></span> <span data-ttu-id="ee1cb-309">If the value is set to *False*, MFA challenges are issued only to users who are enrolled in Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-309">If the value is set to *False*, MFA challenges are issued only to users who are enrolled in Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="ee1cb-310">Use the *False* setting only in testing or in production environments during an onboarding period.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-310">Use the *False* setting only in testing or in production environments during an onboarding period.</span></span>

### <a name="obtain-the-azure-active-directory-guid-id"></a><span data-ttu-id="ee1cb-311">Obtain the Azure Active Directory GUID ID</span><span class="sxs-lookup"><span data-stu-id="ee1cb-311">Obtain the Azure Active Directory GUID ID</span></span>

<span data-ttu-id="ee1cb-312">As part of the configuration of the NPS extension, you must supply administrator credentials and the ID of your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-312">As part of the configuration of the NPS extension, you must supply administrator credentials and the ID of your Azure AD tenant.</span></span> <span data-ttu-id="ee1cb-313">Obtain the ID by doing the following:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-313">Obtain the ID by doing the following:</span></span>

1. <span data-ttu-id="ee1cb-314">Sign in to the [Azure portal](https://portal.azure.com) as the global administrator of the Azure tenant.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-314">Sign in to the [Azure portal](https://portal.azure.com) as the global administrator of the Azure tenant.</span></span>

2. <span data-ttu-id="ee1cb-315">In the left pane, select the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-315">In the left pane, select the **Azure Active Directory** button.</span></span>

3. <span data-ttu-id="ee1cb-316">Select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-316">Select **Properties**.</span></span>

4. <span data-ttu-id="ee1cb-317">To copy your Azure AD ID, select the **Copy** button.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-317">To copy your Azure AD ID, select the **Copy** button.</span></span>
 
    ![The Azure AD ID](./media/howto-mfa-nps-extension-vpn/image35.png)

### <a name="install-the-nps-extension"></a><span data-ttu-id="ee1cb-319">Install the NPS extension</span><span class="sxs-lookup"><span data-stu-id="ee1cb-319">Install the NPS extension</span></span>
<span data-ttu-id="ee1cb-320">The NPS extension must be installed on a server that has the Network Policy and Access Services role installed and that functions as the RADIUS server in your design.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-320">The NPS extension must be installed on a server that has the Network Policy and Access Services role installed and that functions as the RADIUS server in your design.</span></span> <span data-ttu-id="ee1cb-321">Do *not* install the NPS extension on your Remote Desktop server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-321">Do *not* install the NPS extension on your Remote Desktop server.</span></span>

1. <span data-ttu-id="ee1cb-322">Download the NPS extension from [Microsoft Download Center](https://aka.ms/npsmfa).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-322">Download the NPS extension from [Microsoft Download Center](https://aka.ms/npsmfa).</span></span> 

2. <span data-ttu-id="ee1cb-323">Copy the setup executable file (*NpsExtnForAzureMfaInstaller.exe*) to the NPS server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-323">Copy the setup executable file (*NpsExtnForAzureMfaInstaller.exe*) to the NPS server.</span></span>

3. <span data-ttu-id="ee1cb-324">On the NPS server, double-click **NpsExtnForAzureMfaInstaller.exe** and, if you are prompted, select **Run**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-324">On the NPS server, double-click **NpsExtnForAzureMfaInstaller.exe** and, if you are prompted, select **Run**.</span></span>

4. <span data-ttu-id="ee1cb-325">In the **NPS Extension For Azure MFA Setup** window, review the software license terms, select the **I agree to the license terms and conditions** check box, and then select **Install**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-325">In the **NPS Extension For Azure MFA Setup** window, review the software license terms, select the **I agree to the license terms and conditions** check box, and then select **Install**.</span></span>

    ![The "NPS Extension for Azure MFA Setup" window](./media/howto-mfa-nps-extension-vpn/image36.png)
 
5. <span data-ttu-id="ee1cb-327">In the **NPS Extension For Azure MFA Setup** window, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-327">In the **NPS Extension For Azure MFA Setup** window, select **Close**.</span></span>  

    ![The "Setup Successful" confirmation window](./media/howto-mfa-nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-the-nps-extension-by-using-a-powershell-script"></a><span data-ttu-id="ee1cb-329">Configure certificates for use with the NPS extension by using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="ee1cb-329">Configure certificates for use with the NPS extension by using a PowerShell script</span></span>
<span data-ttu-id="ee1cb-330">To ensure secure communications and assurance, configure certificates for use by the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-330">To ensure secure communications and assurance, configure certificates for use by the NPS extension.</span></span> <span data-ttu-id="ee1cb-331">The NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-331">The NPS components include a Windows PowerShell script that configures a self-signed certificate for use with NPS.</span></span> 

<span data-ttu-id="ee1cb-332">The script performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-332">The script performs the following actions:</span></span>

* <span data-ttu-id="ee1cb-333">Creates a self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-333">Creates a self-signed certificate.</span></span>
* <span data-ttu-id="ee1cb-334">Associates the public key of the certificate to the service principal on Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-334">Associates the public key of the certificate to the service principal on Azure AD.</span></span>
* <span data-ttu-id="ee1cb-335">Stores the certificate in the local machine store.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-335">Stores the certificate in the local machine store.</span></span>
* <span data-ttu-id="ee1cb-336">Grants the network user access to the certificate’s private key.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-336">Grants the network user access to the certificate’s private key.</span></span>
* <span data-ttu-id="ee1cb-337">Restarts the NPS service.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-337">Restarts the NPS service.</span></span>

<span data-ttu-id="ee1cb-338">If you want to use your own certificates, you must associate the public key of your certificate with the service principal on Azure AD, and so on.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-338">If you want to use your own certificates, you must associate the public key of your certificate with the service principal on Azure AD, and so on.</span></span>

<span data-ttu-id="ee1cb-339">To use the script, provide the extension with your Azure Active Directory administrative credentials and the Azure Active Directory tenant ID that you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-339">To use the script, provide the extension with your Azure Active Directory administrative credentials and the Azure Active Directory tenant ID that you copied earlier.</span></span> <span data-ttu-id="ee1cb-340">Run the script on each NPS server where you install the NPS extension.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-340">Run the script on each NPS server where you install the NPS extension.</span></span>

1. <span data-ttu-id="ee1cb-341">Run Windows PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-341">Run Windows PowerShell as an administrator.</span></span>

2. <span data-ttu-id="ee1cb-342">At the PowerShell command prompt, enter **cd "c:\Program Files\Microsoft\AzureMfa\Config"**, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-342">At the PowerShell command prompt, enter **cd "c:\Program Files\Microsoft\AzureMfa\Config"**, and then select Enter.</span></span>

3. <span data-ttu-id="ee1cb-343">At the next command prompt, enter **.\AzureMfsNpsExtnConfigSetup.ps1**, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-343">At the next command prompt, enter **.\AzureMfsNpsExtnConfigSetup.ps1**, and then select Enter.</span></span> <span data-ttu-id="ee1cb-344">The script checks to see whether the Azure AD PowerShell module is installed.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-344">The script checks to see whether the Azure AD PowerShell module is installed.</span></span> <span data-ttu-id="ee1cb-345">If it is not installed, the script installs the module for you.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-345">If it is not installed, the script installs the module for you.</span></span>
 
    ![PowerShell](./media/howto-mfa-nps-extension-vpn/image38.png)
 
    <span data-ttu-id="ee1cb-347">After the script verifies the installation of the PowerShell module, it displays the Azure Active Directory PowerShell module sign-in window.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-347">After the script verifies the installation of the PowerShell module, it displays the Azure Active Directory PowerShell module sign-in window.</span></span> 

4. <span data-ttu-id="ee1cb-348">Enter your Azure AD administrator credentials and password, and then select **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-348">Enter your Azure AD administrator credentials and password, and then select **Sign in**.</span></span> 
 
    ![The PowerShell sign-in window](./media/howto-mfa-nps-extension-vpn/image39.png)
 
5. <span data-ttu-id="ee1cb-350">At the command prompt, paste the tenant ID that you copied earlier, and then select Enter.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-350">At the command prompt, paste the tenant ID that you copied earlier, and then select Enter.</span></span> 

    ![Tenant ID](./media/howto-mfa-nps-extension-vpn/image40.png)

    <span data-ttu-id="ee1cb-352">The script creates a self-signed certificate and performs other configuration changes.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-352">The script creates a self-signed certificate and performs other configuration changes.</span></span> <span data-ttu-id="ee1cb-353">The output is like that in the following image:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-353">The output is like that in the following image:</span></span>

    ![Self-signed certificate](./media/howto-mfa-nps-extension-vpn/image41.png)

6. <span data-ttu-id="ee1cb-355">Reboot the server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-355">Reboot the server.</span></span>

### <a name="verify-the-configuration"></a><span data-ttu-id="ee1cb-356">Verify the configuration</span><span class="sxs-lookup"><span data-stu-id="ee1cb-356">Verify the configuration</span></span>
<span data-ttu-id="ee1cb-357">To verify the configuration, you must establish a new VPN connection with the VPN server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-357">To verify the configuration, you must establish a new VPN connection with the VPN server.</span></span> <span data-ttu-id="ee1cb-358">After you've successfully entered your credentials for primary authentication, the VPN connection waits for the secondary authentication to succeed before the connection is established, as shown below.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-358">After you've successfully entered your credentials for primary authentication, the VPN connection waits for the secondary authentication to succeed before the connection is established, as shown below.</span></span> 

![The Windows Settings VPN window](./media/howto-mfa-nps-extension-vpn/image42.png)

<span data-ttu-id="ee1cb-360">If you successfully authenticate with the secondary verification method that you previously configured in Azure MFA, you are connected to the resource.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-360">If you successfully authenticate with the secondary verification method that you previously configured in Azure MFA, you are connected to the resource.</span></span> <span data-ttu-id="ee1cb-361">However, if the secondary authentication is unsuccessful, you are denied access to the resource.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-361">However, if the secondary authentication is unsuccessful, you are denied access to the resource.</span></span> 

<span data-ttu-id="ee1cb-362">In the following example, the Microsoft Authenticator app on a Windows Phone provides the secondary authentication:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-362">In the following example, the Microsoft Authenticator app on a Windows Phone provides the secondary authentication:</span></span>

![Verify account](./media/howto-mfa-nps-extension-vpn/image43.png)

<span data-ttu-id="ee1cb-364">After you've successfully authenticated by using the secondary method, you are granted access to the virtual port on the VPN server.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-364">After you've successfully authenticated by using the secondary method, you are granted access to the virtual port on the VPN server.</span></span> <span data-ttu-id="ee1cb-365">Because you were required to use a secondary authentication method by using a mobile app on a trusted device, the sign-in process is more secure than if it were using only a username and password combination.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-365">Because you were required to use a secondary authentication method by using a mobile app on a trusted device, the sign-in process is more secure than if it were using only a username and password combination.</span></span>

### <a name="view-event-viewer-logs-for-successful-sign-in-events"></a><span data-ttu-id="ee1cb-366">View Event Viewer logs for successful sign-in events</span><span class="sxs-lookup"><span data-stu-id="ee1cb-366">View Event Viewer logs for successful sign-in events</span></span>
<span data-ttu-id="ee1cb-367">To view successful sign-in events in the Windows Event Viewer logs, query the Windows Security log on the NPS server by entering the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-367">To view successful sign-in events in the Windows Event Viewer logs, query the Windows Security log on the NPS server by entering the following PowerShell command:</span></span>

    _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL 

![PowerShell security Event Viewer](./media/howto-mfa-nps-extension-vpn/image44.png)
 
<span data-ttu-id="ee1cb-369">You can also view the security log or the Network Policy and Access Services custom view, as shown here:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-369">You can also view the security log or the Network Policy and Access Services custom view, as shown here:</span></span>

![Network Policy Server log](./media/howto-mfa-nps-extension-vpn/image45.png)

<span data-ttu-id="ee1cb-371">On the server where you installed the NPS extension for Azure Multi-Factor Authentication, you can find Event Viewer application logs that are specific to the extension at *Application and Services Logs\Microsoft\AzureMfa*.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-371">On the server where you installed the NPS extension for Azure Multi-Factor Authentication, you can find Event Viewer application logs that are specific to the extension at *Application and Services Logs\Microsoft\AzureMfa*.</span></span> 

    _Get-WinEvent -Logname Security_ | where {$_.ID -eq '6272'} | FL

![Event Viewer "Number of events" pane](./media/howto-mfa-nps-extension-vpn/image46.png)

## <a name="troubleshooting-guide"></a><span data-ttu-id="ee1cb-373">Troubleshooting guide</span><span class="sxs-lookup"><span data-stu-id="ee1cb-373">Troubleshooting guide</span></span>
<span data-ttu-id="ee1cb-374">If the configuration is not working as expected, begin troubleshooting by verifying that the user is configured to use MFA.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-374">If the configuration is not working as expected, begin troubleshooting by verifying that the user is configured to use MFA.</span></span> <span data-ttu-id="ee1cb-375">Have the user connect to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-375">Have the user connect to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ee1cb-376">If the user is prompted for secondary authentication and can successfully authenticate, you can eliminate an incorrect configuration of MFA as an issue.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-376">If the user is prompted for secondary authentication and can successfully authenticate, you can eliminate an incorrect configuration of MFA as an issue.</span></span>

<span data-ttu-id="ee1cb-377">If MFA is working for the user, review the relevant Event Viewer logs.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-377">If MFA is working for the user, review the relevant Event Viewer logs.</span></span> <span data-ttu-id="ee1cb-378">The logs include the security event, Gateway operational, and Azure Multi-Factor Authentication logs that are discussed in the previous section.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-378">The logs include the security event, Gateway operational, and Azure Multi-Factor Authentication logs that are discussed in the previous section.</span></span> 

<span data-ttu-id="ee1cb-379">An example of a security log that displays a failed sign-in event (event ID 6273) is shown here:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-379">An example of a security log that displays a failed sign-in event (event ID 6273) is shown here:</span></span>

![Security log showing a failed sign-in event](./media/howto-mfa-nps-extension-vpn/image47.png)

<span data-ttu-id="ee1cb-381">A related event from the Azure Multi-Factor Authentication log is shown here:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-381">A related event from the Azure Multi-Factor Authentication log is shown here:</span></span>

![Azure Multi-Factor Authentication logs](./media/howto-mfa-nps-extension-vpn/image48.png)

<span data-ttu-id="ee1cb-383">To do advanced troubleshooting, consult the NPS database format log files where the NPS service is installed.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-383">To do advanced troubleshooting, consult the NPS database format log files where the NPS service is installed.</span></span> <span data-ttu-id="ee1cb-384">The log files are created in the _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-384">The log files are created in the _%SystemRoot%\System32\Logs_ folder as comma-delimited text files.</span></span> <span data-ttu-id="ee1cb-385">For a description of the log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-385">For a description of the log files, see [Interpret NPS Database Format Log Files](https://technet.microsoft.com/library/cc771748.aspx).</span></span> 

<span data-ttu-id="ee1cb-386">The entries in these log files are difficult to interpret unless you export them to a spreadsheet or a database.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-386">The entries in these log files are difficult to interpret unless you export them to a spreadsheet or a database.</span></span> <span data-ttu-id="ee1cb-387">You can find many Internet Authentication Service (IAS) parsing tools online to assist you in interpreting the log files.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-387">You can find many Internet Authentication Service (IAS) parsing tools online to assist you in interpreting the log files.</span></span> <span data-ttu-id="ee1cb-388">The output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer) is shown here:</span><span class="sxs-lookup"><span data-stu-id="ee1cb-388">The output of one such downloadable [shareware application](http://www.deepsoftware.com/iasviewer) is shown here:</span></span> 

![Shareware application](./media/howto-mfa-nps-extension-vpn/image49.png)

<span data-ttu-id="ee1cb-390">To do additional troubleshooting, you can use a protocol analyzer such as Wireshark or [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-390">To do additional troubleshooting, you can use a protocol analyzer such as Wireshark or [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx).</span></span> <span data-ttu-id="ee1cb-391">The following image from Wireshark shows the RADIUS messages between the VPN server and the NPS.</span><span class="sxs-lookup"><span data-stu-id="ee1cb-391">The following image from Wireshark shows the RADIUS messages between the VPN server and the NPS.</span></span>

![Microsoft Message Analyzer](./media/howto-mfa-nps-extension-vpn/image50.png)

<span data-ttu-id="ee1cb-393">For more information, see [Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication](howto-mfa-nps-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ee1cb-393">For more information, see [Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication](howto-mfa-nps-extension.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ee1cb-394">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee1cb-394">Next steps</span></span>
[<span data-ttu-id="ee1cb-395">Get Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ee1cb-395">Get Azure Multi-Factor Authentication</span></span>](concept-mfa-licensing.md)

[<span data-ttu-id="ee1cb-396">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span><span class="sxs-lookup"><span data-stu-id="ee1cb-396">Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS</span></span>](howto-mfaserver-nps-rdg.md)

[<span data-ttu-id="ee1cb-397">Integrate your on-premises directories with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee1cb-397">Integrate your on-premises directories with Azure Active Directory</span></span>](../connect/active-directory-aadconnect.md)

