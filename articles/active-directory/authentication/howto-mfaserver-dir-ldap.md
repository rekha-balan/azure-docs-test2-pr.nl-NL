---
title: LDAP Authentication and Azure MFA Server | Microsoft Docs
description: Deploying LDAP Authentication and Azure Multi-Factor Authentication Server.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: 2b6573182500df6a43a28eeba99ec932d95a5232
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965537"
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="1c0ca-103">LDAP authentication and Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="1c0ca-103">LDAP authentication and Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="1c0ca-104">By default, the Azure Multi-Factor Authentication Server is configured to import or synchronize users from Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-104">By default, the Azure Multi-Factor Authentication Server is configured to import or synchronize users from Active Directory.</span></span> <span data-ttu-id="1c0ca-105">However, it can be configured to bind to different LDAP directories, such as an ADAM directory, or specific Active Directory domain controller.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-105">However, it can be configured to bind to different LDAP directories, such as an ADAM directory, or specific Active Directory domain controller.</span></span> <span data-ttu-id="1c0ca-106">When connected to a directory via LDAP, the Azure Multi-Factor Authentication Server can act as an LDAP proxy to perform authentications.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-106">When connected to a directory via LDAP, the Azure Multi-Factor Authentication Server can act as an LDAP proxy to perform authentications.</span></span> <span data-ttu-id="1c0ca-107">It also allows for the use of LDAP bind as a RADIUS target, for pre-authentication of users with IIS Authentication, or for primary authentication in the Azure MFA user portal.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-107">It also allows for the use of LDAP bind as a RADIUS target, for pre-authentication of users with IIS Authentication, or for primary authentication in the Azure MFA user portal.</span></span>

<span data-ttu-id="1c0ca-108">To use Azure Multi-Factor Authentication as an LDAP proxy, insert the Azure Multi-Factor Authentication Server between the LDAP client (for example, VPN appliance, application) and the LDAP directory server.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-108">To use Azure Multi-Factor Authentication as an LDAP proxy, insert the Azure Multi-Factor Authentication Server between the LDAP client (for example, VPN appliance, application) and the LDAP directory server.</span></span> <span data-ttu-id="1c0ca-109">The Azure Multi-Factor Authentication Server must be configured to communicate with both the client servers and the LDAP directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-109">The Azure Multi-Factor Authentication Server must be configured to communicate with both the client servers and the LDAP directory.</span></span> <span data-ttu-id="1c0ca-110">In this configuration, the Azure Multi-Factor Authentication Server accepts LDAP requests from client servers and applications and forwards them to the target LDAP directory server to validate the primary credentials.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-110">In this configuration, the Azure Multi-Factor Authentication Server accepts LDAP requests from client servers and applications and forwards them to the target LDAP directory server to validate the primary credentials.</span></span> <span data-ttu-id="1c0ca-111">If the LDAP directory validates the primary credentials, Azure Multi-Factor Authentication performs a second identity verification and sends a response back to the LDAP client.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-111">If the LDAP directory validates the primary credentials, Azure Multi-Factor Authentication performs a second identity verification and sends a response back to the LDAP client.</span></span> <span data-ttu-id="1c0ca-112">The entire authentication succeeds only if both the LDAP server authentication and the second-step verification succeed.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-112">The entire authentication succeeds only if both the LDAP server authentication and the second-step verification succeed.</span></span>

## <a name="configure-ldap-authentication"></a><span data-ttu-id="1c0ca-113">Configure LDAP authentication</span><span class="sxs-lookup"><span data-stu-id="1c0ca-113">Configure LDAP authentication</span></span>
<span data-ttu-id="1c0ca-114">To configure LDAP authentication, install the Azure Multi-Factor Authentication Server on a Windows server.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-114">To configure LDAP authentication, install the Azure Multi-Factor Authentication Server on a Windows server.</span></span> <span data-ttu-id="1c0ca-115">Use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="1c0ca-115">Use the following procedure:</span></span>

### <a name="add-an-ldap-client"></a><span data-ttu-id="1c0ca-116">Add an LDAP client</span><span class="sxs-lookup"><span data-stu-id="1c0ca-116">Add an LDAP client</span></span>

1. <span data-ttu-id="1c0ca-117">In the Azure Multi-Factor Authentication Server, select the LDAP Authentication icon in the left menu.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-117">In the Azure Multi-Factor Authentication Server, select the LDAP Authentication icon in the left menu.</span></span>
2. <span data-ttu-id="1c0ca-118">Check the **Enable LDAP Authentication** checkbox.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-118">Check the **Enable LDAP Authentication** checkbox.</span></span>

   ![LDAP Authentication](./media/howto-mfaserver-dir-ldap/ldap2.png)

3. <span data-ttu-id="1c0ca-120">On the Clients tab, change the TCP port and SSL port if the Azure Multi-Factor Authentication LDAP service should bind to non-standard ports to listen for LDAP requests.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-120">On the Clients tab, change the TCP port and SSL port if the Azure Multi-Factor Authentication LDAP service should bind to non-standard ports to listen for LDAP requests.</span></span>
4. <span data-ttu-id="1c0ca-121">If you plan to use LDAPS from the client to the Azure Multi-Factor Authentication Server, an SSL certificate must be installed on the same server as MFA Server.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-121">If you plan to use LDAPS from the client to the Azure Multi-Factor Authentication Server, an SSL certificate must be installed on the same server as MFA Server.</span></span> <span data-ttu-id="1c0ca-122">Click **Browse** next to the SSL certificate box, and select a certificate to use for the secure connection.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-122">Click **Browse** next to the SSL certificate box, and select a certificate to use for the secure connection.</span></span>
5. <span data-ttu-id="1c0ca-123">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-123">Click **Add**.</span></span>
6. <span data-ttu-id="1c0ca-124">In the Add LDAP Client dialog box, enter the IP address of the appliance, server, or application that authenticates to the Server and an Application name (optional).</span><span class="sxs-lookup"><span data-stu-id="1c0ca-124">In the Add LDAP Client dialog box, enter the IP address of the appliance, server, or application that authenticates to the Server and an Application name (optional).</span></span> <span data-ttu-id="1c0ca-125">The Application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-125">The Application name appears in Azure Multi-Factor Authentication reports and may be displayed within SMS or Mobile App authentication messages.</span></span>
7. <span data-ttu-id="1c0ca-126">Check the **Require Azure Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to two-step verification.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-126">Check the **Require Azure Multi-Factor Authentication user match** box if all users have been or will be imported into the Server and subject to two-step verification.</span></span> <span data-ttu-id="1c0ca-127">If a significant number of users have not yet been imported into the Server and/or are exempt from two-step verification, leave the box unchecked.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-127">If a significant number of users have not yet been imported into the Server and/or are exempt from two-step verification, leave the box unchecked.</span></span> <span data-ttu-id="1c0ca-128">See the MFA Server help file for additional information on this feature.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-128">See the MFA Server help file for additional information on this feature.</span></span>

<span data-ttu-id="1c0ca-129">Repeat these steps to add additional LDAP clients.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-129">Repeat these steps to add additional LDAP clients.</span></span>

### <a name="configure-the-ldap-directory-connection"></a><span data-ttu-id="1c0ca-130">Configure the LDAP directory connection</span><span class="sxs-lookup"><span data-stu-id="1c0ca-130">Configure the LDAP directory connection</span></span>

<span data-ttu-id="1c0ca-131">When the Azure Multi-Factor Authentication is configured to receive LDAP authentications, it must proxy those authentications to the LDAP directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-131">When the Azure Multi-Factor Authentication is configured to receive LDAP authentications, it must proxy those authentications to the LDAP directory.</span></span> <span data-ttu-id="1c0ca-132">Therefore, the Target tab only displays a single, grayed out option to use an LDAP target.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-132">Therefore, the Target tab only displays a single, grayed out option to use an LDAP target.</span></span>

1. <span data-ttu-id="1c0ca-133">To configure the LDAP directory connection, click the **Directory Integration** icon.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-133">To configure the LDAP directory connection, click the **Directory Integration** icon.</span></span>
2. <span data-ttu-id="1c0ca-134">On the Settings tab, select the **Use specific LDAP configuration** radio button.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-134">On the Settings tab, select the **Use specific LDAP configuration** radio button.</span></span>
3. <span data-ttu-id="1c0ca-135">Select **Edit…**</span><span class="sxs-lookup"><span data-stu-id="1c0ca-135">Select **Edit…**</span></span>
4. <span data-ttu-id="1c0ca-136">In the Edit LDAP Configuration dialog box, populate the fields with the information required to connect to the LDAP directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-136">In the Edit LDAP Configuration dialog box, populate the fields with the information required to connect to the LDAP directory.</span></span> <span data-ttu-id="1c0ca-137">Descriptions of the fields are included in the Azure Multi-Factor Authentication Server help file.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-137">Descriptions of the fields are included in the Azure Multi-Factor Authentication Server help file.</span></span>

    ![Directory Integration](./media/howto-mfaserver-dir-ldap/ldap.png)

5. <span data-ttu-id="1c0ca-139">Test the LDAP connection by clicking the **Test** button.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-139">Test the LDAP connection by clicking the **Test** button.</span></span>
6. <span data-ttu-id="1c0ca-140">If the LDAP connection test was successful, click the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-140">If the LDAP connection test was successful, click the **OK** button.</span></span>
7. <span data-ttu-id="1c0ca-141">Click the **Filters** tab. The Server is pre-configured to load containers, security groups, and users from Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-141">Click the **Filters** tab. The Server is pre-configured to load containers, security groups, and users from Active Directory.</span></span> <span data-ttu-id="1c0ca-142">If binding to a different LDAP directory, you probably need to edit the filters displayed.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-142">If binding to a different LDAP directory, you probably need to edit the filters displayed.</span></span> <span data-ttu-id="1c0ca-143">Click the **Help** link for more information on filters.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-143">Click the **Help** link for more information on filters.</span></span>
8. <span data-ttu-id="1c0ca-144">Click the **Attributes** tab. The Server is pre-configured to map attributes from Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-144">Click the **Attributes** tab. The Server is pre-configured to map attributes from Active Directory.</span></span>
9. <span data-ttu-id="1c0ca-145">If you're binding to a different LDAP directory or to change the pre-configured attribute mappings, click **Edit…**</span><span class="sxs-lookup"><span data-stu-id="1c0ca-145">If you're binding to a different LDAP directory or to change the pre-configured attribute mappings, click **Edit…**</span></span>
10. <span data-ttu-id="1c0ca-146">In the Edit Attributes dialog box, modify the LDAP attribute mappings for your directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-146">In the Edit Attributes dialog box, modify the LDAP attribute mappings for your directory.</span></span> <span data-ttu-id="1c0ca-147">Attribute names can be typed in or selected by clicking the **…**</span><span class="sxs-lookup"><span data-stu-id="1c0ca-147">Attribute names can be typed in or selected by clicking the **…**</span></span> <span data-ttu-id="1c0ca-148">button next to each field.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-148">button next to each field.</span></span> <span data-ttu-id="1c0ca-149">Click the **Help** link for more information on attributes.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-149">Click the **Help** link for more information on attributes.</span></span>
11. <span data-ttu-id="1c0ca-150">Click the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-150">Click the **OK** button.</span></span>
12. <span data-ttu-id="1c0ca-151">Click the **Company Settings** icon and select the **Username Resolution** tab.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-151">Click the **Company Settings** icon and select the **Username Resolution** tab.</span></span>
13. <span data-ttu-id="1c0ca-152">If you're connecting to Active Directory from a domain-joined server, leave the **Use Windows security identifiers (SIDs) for matching usernames** radio button selected.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-152">If you're connecting to Active Directory from a domain-joined server, leave the **Use Windows security identifiers (SIDs) for matching usernames** radio button selected.</span></span> <span data-ttu-id="1c0ca-153">Otherwise, select the **Use LDAP unique identifier attribute for matching usernames** radio button.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-153">Otherwise, select the **Use LDAP unique identifier attribute for matching usernames** radio button.</span></span> 

<span data-ttu-id="1c0ca-154">When the **Use LDAP unique identifier attribute for matching usernames** radio button is selected, the Azure Multi-Factor Authentication Server attempts to resolve each username to a unique identifier in the LDAP directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-154">When the **Use LDAP unique identifier attribute for matching usernames** radio button is selected, the Azure Multi-Factor Authentication Server attempts to resolve each username to a unique identifier in the LDAP directory.</span></span> <span data-ttu-id="1c0ca-155">An LDAP search is performed on the Username attributes defined in the Directory Integration -> Attributes tab. When a user authenticates, the username is resolved to the unique identifier in the LDAP directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-155">An LDAP search is performed on the Username attributes defined in the Directory Integration -> Attributes tab. When a user authenticates, the username is resolved to the unique identifier in the LDAP directory.</span></span> <span data-ttu-id="1c0ca-156">The unique identifier is used for matching the user in the Azure Multi-Factor Authentication data file.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-156">The unique identifier is used for matching the user in the Azure Multi-Factor Authentication data file.</span></span> <span data-ttu-id="1c0ca-157">This allows for case-insensitive comparisons, and long and short username formats.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-157">This allows for case-insensitive comparisons, and long and short username formats.</span></span>

<span data-ttu-id="1c0ca-158">After you complete these steps, the MFA Server listens on the configured ports for LDAP access requests from the configured clients, and acts as a proxy for those requests to the LDAP directory for authentication.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-158">After you complete these steps, the MFA Server listens on the configured ports for LDAP access requests from the configured clients, and acts as a proxy for those requests to the LDAP directory for authentication.</span></span>

## <a name="configure-ldap-client"></a><span data-ttu-id="1c0ca-159">Configure LDAP client</span><span class="sxs-lookup"><span data-stu-id="1c0ca-159">Configure LDAP client</span></span>
<span data-ttu-id="1c0ca-160">To configure the LDAP client, use the guidelines:</span><span class="sxs-lookup"><span data-stu-id="1c0ca-160">To configure the LDAP client, use the guidelines:</span></span>

* <span data-ttu-id="1c0ca-161">Configure your appliance, server, or application to authenticate via LDAP to the Azure Multi-Factor Authentication Server as though it were your LDAP directory.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-161">Configure your appliance, server, or application to authenticate via LDAP to the Azure Multi-Factor Authentication Server as though it were your LDAP directory.</span></span> <span data-ttu-id="1c0ca-162">Use the same settings that you would normally use to connect directly to your LDAP directory, except for the server name or IP address, which will be that of the Azure Multi-Factor Authentication Server.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-162">Use the same settings that you would normally use to connect directly to your LDAP directory, except for the server name or IP address, which will be that of the Azure Multi-Factor Authentication Server.</span></span>
* <span data-ttu-id="1c0ca-163">Configure the LDAP timeout to 30-60 seconds so that there is time to validate the user’s credentials with the LDAP directory, perform the second-step verification, receive their response, and respond to the LDAP access request.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-163">Configure the LDAP timeout to 30-60 seconds so that there is time to validate the user’s credentials with the LDAP directory, perform the second-step verification, receive their response, and respond to the LDAP access request.</span></span>
* <span data-ttu-id="1c0ca-164">If using LDAPS, the appliance or server making the LDAP queries must trust the SSL certificate installed on the Azure Multi-Factor Authentication Server.</span><span class="sxs-lookup"><span data-stu-id="1c0ca-164">If using LDAPS, the appliance or server making the LDAP queries must trust the SSL certificate installed on the Azure Multi-Factor Authentication Server.</span></span>
