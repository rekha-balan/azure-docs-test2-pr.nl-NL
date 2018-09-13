---
title: Azure AD Connect - Update the SSL certificate for an AD FS farm | Microsoft Docs
description: This document details the steps to update the SSL certificate of an AD FS farm by using Azure AD Connect.
services: active-directory
manager: mtillman
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/09/2018
ms.component: hybrid
author: billmath
ms.custom: seohack1
ms.author: billmath
ms.openlocfilehash: 0eeb3f7d54617ff060481795bcdaa8b54e36dfa8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808436"
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="57f1c-103">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span><span class="sxs-lookup"><span data-stu-id="57f1c-103">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="57f1c-104">Overview</span><span class="sxs-lookup"><span data-stu-id="57f1c-104">Overview</span></span>
<span data-ttu-id="57f1c-105">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span><span class="sxs-lookup"><span data-stu-id="57f1c-105">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="57f1c-106">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span><span class="sxs-lookup"><span data-stu-id="57f1c-106">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="57f1c-107">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span><span class="sxs-lookup"><span data-stu-id="57f1c-107">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Three steps](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="57f1c-109">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="57f1c-109">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57f1c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="57f1c-110">Prerequisites</span></span>

* <span data-ttu-id="57f1c-111">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span><span class="sxs-lookup"><span data-stu-id="57f1c-111">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="57f1c-112">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.553.0 or higher.</span><span class="sxs-lookup"><span data-stu-id="57f1c-112">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.553.0 or higher.</span></span> <span data-ttu-id="57f1c-113">You'll use the task **Update AD FS SSL certificate**.</span><span class="sxs-lookup"><span data-stu-id="57f1c-113">You'll use the task **Update AD FS SSL certificate**.</span></span>

![Update SSL task](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="57f1c-115">Step 1: Provide AD FS farm information</span><span class="sxs-lookup"><span data-stu-id="57f1c-115">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="57f1c-116">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span><span class="sxs-lookup"><span data-stu-id="57f1c-116">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="57f1c-117">Querying the farm information from AD FS (Windows Server 2016 or later).</span><span class="sxs-lookup"><span data-stu-id="57f1c-117">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="57f1c-118">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="57f1c-118">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="57f1c-119">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="57f1c-119">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="57f1c-120">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span><span class="sxs-lookup"><span data-stu-id="57f1c-120">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![AD FS server info](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="57f1c-122">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="57f1c-122">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![Offline server in list](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="57f1c-124">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span><span class="sxs-lookup"><span data-stu-id="57f1c-124">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="57f1c-125">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span><span class="sxs-lookup"><span data-stu-id="57f1c-125">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="57f1c-126">Step 2: Provide a new SSL certificate</span><span class="sxs-lookup"><span data-stu-id="57f1c-126">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="57f1c-127">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="57f1c-127">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="57f1c-128">Provide a password-protected PFX certificate to continue the installation.</span><span class="sxs-lookup"><span data-stu-id="57f1c-128">Provide a password-protected PFX certificate to continue the installation.</span></span>

![SSL certificate](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="57f1c-130">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span><span class="sxs-lookup"><span data-stu-id="57f1c-130">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="57f1c-131">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span><span class="sxs-lookup"><span data-stu-id="57f1c-131">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="57f1c-132">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span><span class="sxs-lookup"><span data-stu-id="57f1c-132">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="57f1c-133">The certificate is valid for more than 30 days.</span><span class="sxs-lookup"><span data-stu-id="57f1c-133">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="57f1c-134">The certificate trust chain is valid.</span><span class="sxs-lookup"><span data-stu-id="57f1c-134">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="57f1c-135">The certificate is password protected.</span><span class="sxs-lookup"><span data-stu-id="57f1c-135">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="57f1c-136">Step 3: Select servers for the update</span><span class="sxs-lookup"><span data-stu-id="57f1c-136">Step 3: Select servers for the update</span></span>

<span data-ttu-id="57f1c-137">In the next step, select the servers that need to have the SSL certificate updated.</span><span class="sxs-lookup"><span data-stu-id="57f1c-137">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="57f1c-138">Servers that are offline can't be selected for the update.</span><span class="sxs-lookup"><span data-stu-id="57f1c-138">Servers that are offline can't be selected for the update.</span></span>

![Select servers to update](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="57f1c-140">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span><span class="sxs-lookup"><span data-stu-id="57f1c-140">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![Configuration complete](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="57f1c-142">FAQs</span><span class="sxs-lookup"><span data-stu-id="57f1c-142">FAQs</span></span>

* <span data-ttu-id="57f1c-143">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span><span class="sxs-lookup"><span data-stu-id="57f1c-143">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="57f1c-144">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span><span class="sxs-lookup"><span data-stu-id="57f1c-144">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="57f1c-145">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="57f1c-145">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="57f1c-146">Wildcard certificates are also accepted.</span><span class="sxs-lookup"><span data-stu-id="57f1c-146">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="57f1c-147">**Why am I asked for credentials again on the WAP server page?**</span><span class="sxs-lookup"><span data-stu-id="57f1c-147">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="57f1c-148">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span><span class="sxs-lookup"><span data-stu-id="57f1c-148">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="57f1c-149">**The server is shown as offline. What should I do?**</span><span class="sxs-lookup"><span data-stu-id="57f1c-149">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="57f1c-150">Azure AD Connect can't perform any operation if the server is offline.</span><span class="sxs-lookup"><span data-stu-id="57f1c-150">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="57f1c-151">If the server is part of the AD FS farm, then check the connectivity to the server.</span><span class="sxs-lookup"><span data-stu-id="57f1c-151">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="57f1c-152">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span><span class="sxs-lookup"><span data-stu-id="57f1c-152">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="57f1c-153">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span><span class="sxs-lookup"><span data-stu-id="57f1c-153">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="57f1c-154">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span><span class="sxs-lookup"><span data-stu-id="57f1c-154">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="57f1c-155">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span><span class="sxs-lookup"><span data-stu-id="57f1c-155">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="57f1c-156">**Can I update a subset of my farm servers with the new SSL certificate?**</span><span class="sxs-lookup"><span data-stu-id="57f1c-156">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="57f1c-157">Yes.</span><span class="sxs-lookup"><span data-stu-id="57f1c-157">Yes.</span></span> <span data-ttu-id="57f1c-158">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span><span class="sxs-lookup"><span data-stu-id="57f1c-158">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="57f1c-159">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span><span class="sxs-lookup"><span data-stu-id="57f1c-159">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="57f1c-160">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span><span class="sxs-lookup"><span data-stu-id="57f1c-160">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="57f1c-161">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="57f1c-161">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="57f1c-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span><span class="sxs-lookup"><span data-stu-id="57f1c-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="57f1c-163">If the server is still present in the AD FS configuration, it will be listed back in the list.</span><span class="sxs-lookup"><span data-stu-id="57f1c-163">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="57f1c-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="57f1c-164">Next steps</span></span>

- [<span data-ttu-id="57f1c-165">Azure AD Connect and federation</span><span class="sxs-lookup"><span data-stu-id="57f1c-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="57f1c-166">Active Directory Federation Services management and customization with Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="57f1c-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
