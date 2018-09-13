---
title: Active Directory Federation Services management and customization with Azure AD Connect | Microsoft Docs
description: AD FS management with Azure AD Connect and customization of user AD FS sign-in experience with Azure AD Connect and PowerShell.
keywords: AD FS, ADFS, AD FS management, AAD Connect, Connect, sign-in, AD FS customization, repair trust, O365, federation, relying party
services: active-directory
documentationcenter: ''
author: anandyadavmsft
manager: femila
editor: ''
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/4/2016
ms.author: anandy
ms.openlocfilehash: 3491271fcf48a6dbaaeabe71d822906feff270dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556568"
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="f6f82-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="f6f82-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="f6f82-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span><span class="sxs-lookup"><span data-stu-id="f6f82-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="f6f82-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="f6f82-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="f6f82-107">Topic</span><span class="sxs-lookup"><span data-stu-id="f6f82-107">Topic</span></span> | <span data-ttu-id="f6f82-108">What it covers</span><span class="sxs-lookup"><span data-stu-id="f6f82-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="f6f82-109">**Manage AD FS**</span><span class="sxs-lookup"><span data-stu-id="f6f82-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="f6f82-110">Repair the trust</span><span class="sxs-lookup"><span data-stu-id="f6f82-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="f6f82-111">How to repair the federation trust with Office 365.</span><span class="sxs-lookup"><span data-stu-id="f6f82-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="f6f82-112">Federate with Azure AD using alternate login ID </span><span class="sxs-lookup"><span data-stu-id="f6f82-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="f6f82-113">Configure federation using alternate login ID</span><span class="sxs-lookup"><span data-stu-id="f6f82-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="f6f82-114">Add an AD FS server</span><span class="sxs-lookup"><span data-stu-id="f6f82-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="f6f82-115">How to expand an AD FS farm with an additional AD FS server.</span><span class="sxs-lookup"><span data-stu-id="f6f82-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="f6f82-116">Add an AD FS Web Application Proxy server</span><span class="sxs-lookup"><span data-stu-id="f6f82-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="f6f82-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span><span class="sxs-lookup"><span data-stu-id="f6f82-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="f6f82-118">Add a federated domain</span><span class="sxs-lookup"><span data-stu-id="f6f82-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="f6f82-119">How to add a federated domain.</span><span class="sxs-lookup"><span data-stu-id="f6f82-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="f6f82-120">Update the SSL certificate</span><span class="sxs-lookup"><span data-stu-id="f6f82-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="f6f82-121">How to update the SSL certificate for an AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="f6f82-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="f6f82-122">**Customize AD FS**</span><span class="sxs-lookup"><span data-stu-id="f6f82-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="f6f82-123">Add a custom company logo or illustration</span><span class="sxs-lookup"><span data-stu-id="f6f82-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="f6f82-124">How to customize an AD FS sign-in page with a company logo and illustration.</span><span class="sxs-lookup"><span data-stu-id="f6f82-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="f6f82-125">Add a sign-in description</span><span class="sxs-lookup"><span data-stu-id="f6f82-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="f6f82-126">How to add a sign-in page description.</span><span class="sxs-lookup"><span data-stu-id="f6f82-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="f6f82-127">Modify AD FS claim rules</span><span class="sxs-lookup"><span data-stu-id="f6f82-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="f6f82-128">How to modify AD FS claims for various federation scenarios.</span><span class="sxs-lookup"><span data-stu-id="f6f82-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="f6f82-129">Manage AD FS</span><span class="sxs-lookup"><span data-stu-id="f6f82-129">Manage AD FS</span></span>
<span data-ttu-id="f6f82-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span><span class="sxs-lookup"><span data-stu-id="f6f82-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="f6f82-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span><span class="sxs-lookup"><span data-stu-id="f6f82-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="f6f82-132">Repair the trust <a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="f6f82-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span><span class="sxs-lookup"><span data-stu-id="f6f82-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="f6f82-134">Follow these steps to repair your Azure AD and AD FS trust.</span><span class="sxs-lookup"><span data-stu-id="f6f82-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="f6f82-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span><span class="sxs-lookup"><span data-stu-id="f6f82-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="f6f82-136">![Repair AAD and ADFS Trust](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="f6f82-136">![Repair AAD and ADFS Trust](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="f6f82-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f6f82-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="f6f82-138">![Connect to Azure AD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="f6f82-138">![Connect to Azure AD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="f6f82-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span><span class="sxs-lookup"><span data-stu-id="f6f82-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![Remote access credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="f6f82-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span><span class="sxs-lookup"><span data-stu-id="f6f82-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![State of certificates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="f6f82-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span><span class="sxs-lookup"><span data-stu-id="f6f82-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![Ready to configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="f6f82-145">Click **Install** to repair the trust.</span><span class="sxs-lookup"><span data-stu-id="f6f82-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="f6f82-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span><span class="sxs-lookup"><span data-stu-id="f6f82-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="f6f82-147">Azure AD Connect can't repair third-party certificates.</span><span class="sxs-lookup"><span data-stu-id="f6f82-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="f6f82-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="f6f82-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span><span class="sxs-lookup"><span data-stu-id="f6f82-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="f6f82-150">If the on-premises UPN uses a non-routable domain (ex.</span><span class="sxs-lookup"><span data-stu-id="f6f82-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="f6f82-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span><span class="sxs-lookup"><span data-stu-id="f6f82-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="f6f82-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span><span class="sxs-lookup"><span data-stu-id="f6f82-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="f6f82-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6f82-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="f6f82-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span><span class="sxs-lookup"><span data-stu-id="f6f82-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="f6f82-155">An example of choosing a different attribute for User Principal Name is shown below:</span><span class="sxs-lookup"><span data-stu-id="f6f82-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Alternate ID attribute selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="f6f82-157">Configuring alternate login ID for AD FS consists of two main steps:</span><span class="sxs-lookup"><span data-stu-id="f6f82-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="f6f82-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span><span class="sxs-lookup"><span data-stu-id="f6f82-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="f6f82-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span><span class="sxs-lookup"><span data-stu-id="f6f82-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="f6f82-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span><span class="sxs-lookup"><span data-stu-id="f6f82-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="f6f82-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span><span class="sxs-lookup"><span data-stu-id="f6f82-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="f6f82-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span><span class="sxs-lookup"><span data-stu-id="f6f82-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Warning for missing KB on 2012R2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="f6f82-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="f6f82-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="f6f82-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="f6f82-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="f6f82-166">Add an AD FS server <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="f6f82-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span><span class="sxs-lookup"><span data-stu-id="f6f82-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="f6f82-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f6f82-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="f6f82-169">Select **Deploy an additional Federation Server**, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f6f82-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Additional federation server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="f6f82-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f6f82-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Connect to Azure AD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="f6f82-173">Provide the domain administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="f6f82-173">Provide the domain administrator credentials.</span></span>

   ![Domain administrator credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="f6f82-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f6f82-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="f6f82-176">Click **Enter Password** to provide the password for the PFX file.</span><span class="sxs-lookup"><span data-stu-id="f6f82-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![Certificate password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Specify SSL certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="f6f82-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="f6f82-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![AD FS servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="f6f82-181">Click **Next**, and go through the final **Configure** page.</span><span class="sxs-lookup"><span data-stu-id="f6f82-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="f6f82-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span><span class="sxs-lookup"><span data-stu-id="f6f82-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![Ready to configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installation complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="f6f82-185">Add an AD FS WAP server <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="f6f82-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span><span class="sxs-lookup"><span data-stu-id="f6f82-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="f6f82-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f6f82-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="f6f82-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span><span class="sxs-lookup"><span data-stu-id="f6f82-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![Deploy Web Application Proxy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="f6f82-190">Provide the Azure global administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="f6f82-190">Provide the Azure global administrator credentials.</span></span>

   ![Connect to Azure AD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="f6f82-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f6f82-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="f6f82-193">![Certificate password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="f6f82-193">![Certificate password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Specify SSL certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="f6f82-195">Add the server to be added as a WAP server.</span><span class="sxs-lookup"><span data-stu-id="f6f82-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="f6f82-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span><span class="sxs-lookup"><span data-stu-id="f6f82-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![Administrative server credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="f6f82-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="f6f82-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Proxy trust credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="f6f82-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span><span class="sxs-lookup"><span data-stu-id="f6f82-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![Ready to configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="f6f82-202">Click **Install** to finish the configuration.</span><span class="sxs-lookup"><span data-stu-id="f6f82-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="f6f82-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span><span class="sxs-lookup"><span data-stu-id="f6f82-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="f6f82-204">Click **Verify** to check connectivity.</span><span class="sxs-lookup"><span data-stu-id="f6f82-204">Click **Verify** to check connectivity.</span></span>

   ![Installation complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="f6f82-206">Add a federated domain <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="f6f82-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f6f82-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="f6f82-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6f82-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="f6f82-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span><span class="sxs-lookup"><span data-stu-id="f6f82-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![Additional Azure AD domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="f6f82-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6f82-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Connect to Azure AD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="f6f82-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="f6f82-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![Remote access credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="f6f82-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span><span class="sxs-lookup"><span data-stu-id="f6f82-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="f6f82-216">Choose the domain from the list.</span><span class="sxs-lookup"><span data-stu-id="f6f82-216">Choose the domain from the list.</span></span>

   ![Azure AD domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="f6f82-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span><span class="sxs-lookup"><span data-stu-id="f6f82-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="f6f82-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span><span class="sxs-lookup"><span data-stu-id="f6f82-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="f6f82-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="f6f82-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="f6f82-221">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f6f82-221">Click **Next**.</span></span> <span data-ttu-id="f6f82-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span><span class="sxs-lookup"><span data-stu-id="f6f82-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="f6f82-223">Click **Install** to finish the configuration.</span><span class="sxs-lookup"><span data-stu-id="f6f82-223">Click **Install** to finish the configuration.</span></span>

   ![Ready to configure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

## <a name="ad-fs-customization"></a><span data-ttu-id="f6f82-225">AD FS customization</span><span class="sxs-lookup"><span data-stu-id="f6f82-225">AD FS customization</span></span>
<span data-ttu-id="f6f82-226">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span><span class="sxs-lookup"><span data-stu-id="f6f82-226">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="f6f82-227">Add a custom company logo or illustration <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-227">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="f6f82-228">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span><span class="sxs-lookup"><span data-stu-id="f6f82-228">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="f6f82-229">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span><span class="sxs-lookup"><span data-stu-id="f6f82-229">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="f6f82-230">The *TargetName* parameter is required.</span><span class="sxs-lookup"><span data-stu-id="f6f82-230">The *TargetName* parameter is required.</span></span> <span data-ttu-id="f6f82-231">The default theme that's released with AD FS is named Default.</span><span class="sxs-lookup"><span data-stu-id="f6f82-231">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="f6f82-232">Add a sign-in description <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-232">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="f6f82-233">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span><span class="sxs-lookup"><span data-stu-id="f6f82-233">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="f6f82-234">Modify AD FS claim rules <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="f6f82-234">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="f6f82-235">AD FS supports a rich claim language that you can use to create custom claim rules.</span><span class="sxs-lookup"><span data-stu-id="f6f82-235">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="f6f82-236">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6f82-236">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="f6f82-237">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span><span class="sxs-lookup"><span data-stu-id="f6f82-237">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="f6f82-238">Immutable ID conditional on a value being present in the attribute</span><span class="sxs-lookup"><span data-stu-id="f6f82-238">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="f6f82-239">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6f82-239">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="f6f82-240">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span><span class="sxs-lookup"><span data-stu-id="f6f82-240">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="f6f82-241">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span><span class="sxs-lookup"><span data-stu-id="f6f82-241">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="f6f82-242">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span><span class="sxs-lookup"><span data-stu-id="f6f82-242">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="f6f82-243">You can construct the set of custom claim rules as described in the following section.</span><span class="sxs-lookup"><span data-stu-id="f6f82-243">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="f6f82-244">**Rule 1: Query attributes**</span><span class="sxs-lookup"><span data-stu-id="f6f82-244">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="f6f82-245">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6f82-245">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="f6f82-246">Change the store name to an appropriate store name in your AD FS deployment.</span><span class="sxs-lookup"><span data-stu-id="f6f82-246">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="f6f82-247">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="f6f82-247">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="f6f82-248">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span><span class="sxs-lookup"><span data-stu-id="f6f82-248">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="f6f82-249">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span><span class="sxs-lookup"><span data-stu-id="f6f82-249">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="f6f82-250">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span><span class="sxs-lookup"><span data-stu-id="f6f82-250">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="f6f82-251">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span><span class="sxs-lookup"><span data-stu-id="f6f82-251">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="f6f82-252">The logic behind this is the fact that AD FS doesn't allow empty claims.</span><span class="sxs-lookup"><span data-stu-id="f6f82-252">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="f6f82-253">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span><span class="sxs-lookup"><span data-stu-id="f6f82-253">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="f6f82-254">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span><span class="sxs-lookup"><span data-stu-id="f6f82-254">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="f6f82-255">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span><span class="sxs-lookup"><span data-stu-id="f6f82-255">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="f6f82-256">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span><span class="sxs-lookup"><span data-stu-id="f6f82-256">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="f6f82-257">This is an implicit **Exist** check.</span><span class="sxs-lookup"><span data-stu-id="f6f82-257">This is an implicit **Exist** check.</span></span> <span data-ttu-id="f6f82-258">If the value for the claim exists, then issue that as the immutable ID.</span><span class="sxs-lookup"><span data-stu-id="f6f82-258">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="f6f82-259">The previous example uses the **nameidentifier** claim.</span><span class="sxs-lookup"><span data-stu-id="f6f82-259">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="f6f82-260">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span><span class="sxs-lookup"><span data-stu-id="f6f82-260">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="f6f82-261">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span><span class="sxs-lookup"><span data-stu-id="f6f82-261">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="f6f82-262">In this rule, you're simply checking the temporary flag **idflag**.</span><span class="sxs-lookup"><span data-stu-id="f6f82-262">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="f6f82-263">You decide whether to issue the claim based on its value.</span><span class="sxs-lookup"><span data-stu-id="f6f82-263">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="f6f82-264">The sequence of these rules is important.</span><span class="sxs-lookup"><span data-stu-id="f6f82-264">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="f6f82-265">SSO with a subdomain UPN</span><span class="sxs-lookup"><span data-stu-id="f6f82-265">SSO with a subdomain UPN</span></span>
<span data-ttu-id="f6f82-266">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="f6f82-266">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="f6f82-267">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span><span class="sxs-lookup"><span data-stu-id="f6f82-267">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="f6f82-268">By default, the claim rule for issuer ID is set as:</span><span class="sxs-lookup"><span data-stu-id="f6f82-268">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Default issuer ID claim](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="f6f82-270">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span><span class="sxs-lookup"><span data-stu-id="f6f82-270">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="f6f82-271">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6f82-271">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="f6f82-272">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6f82-272">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="f6f82-273">The default issuer ID claim rule in AD FS handles it in the following manner:</span><span class="sxs-lookup"><span data-stu-id="f6f82-273">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="f6f82-274">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="f6f82-274">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="f6f82-275">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span><span class="sxs-lookup"><span data-stu-id="f6f82-275">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="f6f82-276">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6f82-276">Next steps</span></span>
<span data-ttu-id="f6f82-277">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="f6f82-277">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>





























