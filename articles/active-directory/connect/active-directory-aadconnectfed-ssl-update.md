---
title: 'Azure AD Connect: Update the SSL certificate for an Active Directory Federation Services (AD FS) farm | Microsoft Docs'
description: This document details the steps to update the SSL certificate of an AD FS farm by using Azure AD Connect.
services: active-directory
keywords: azure ad connect, adfs ssl update, adfs certificate update, change adfs certificate, new adfs certificate, adfs certificate, update adfs ssl certificate, update ssl certificate adfs, configure adfs ssl certificate, adfs, ssl, certificate, adfs service communication certificate, update federation, configure federation, aad connect
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2016
ms.author: anandy
ms.openlocfilehash: 16b47f5a930746042f0456fa065675d28c3739a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555716"
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="18424-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span><span class="sxs-lookup"><span data-stu-id="18424-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="18424-105">Overview</span><span class="sxs-lookup"><span data-stu-id="18424-105">Overview</span></span>
<span data-ttu-id="18424-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span><span class="sxs-lookup"><span data-stu-id="18424-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="18424-107">If the sign-in method in Azure AD Connect is set as AD FS, you can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="18424-107">If the sign-in method in Azure AD Connect is set as AD FS, you can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm.</span></span> <span data-ttu-id="18424-108">You can do this across all federation and Web Application Proxy (WAP) servers in three simple steps:</span><span class="sxs-lookup"><span data-stu-id="18424-108">You can do this across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Three steps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="18424-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="18424-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18424-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="18424-111">Prerequisites</span></span>

* <span data-ttu-id="18424-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span><span class="sxs-lookup"><span data-stu-id="18424-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="18424-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span><span class="sxs-lookup"><span data-stu-id="18424-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="18424-114">You'll use the task **Update AD FS SSL certificate**.</span><span class="sxs-lookup"><span data-stu-id="18424-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![Update SSL task](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="18424-116">Step 1: Provide AD FS farm information</span><span class="sxs-lookup"><span data-stu-id="18424-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="18424-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span><span class="sxs-lookup"><span data-stu-id="18424-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="18424-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span><span class="sxs-lookup"><span data-stu-id="18424-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="18424-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="18424-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="18424-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="18424-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="18424-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span><span class="sxs-lookup"><span data-stu-id="18424-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![AD FS server info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="18424-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span><span class="sxs-lookup"><span data-stu-id="18424-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![Offline server in list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="18424-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span><span class="sxs-lookup"><span data-stu-id="18424-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="18424-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span><span class="sxs-lookup"><span data-stu-id="18424-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="18424-127">Step 2: Provide a new SSL certificate</span><span class="sxs-lookup"><span data-stu-id="18424-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="18424-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="18424-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="18424-129">Provide a password-protected PFX certificate to continue the installation.</span><span class="sxs-lookup"><span data-stu-id="18424-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![SSL certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="18424-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span><span class="sxs-lookup"><span data-stu-id="18424-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="18424-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span><span class="sxs-lookup"><span data-stu-id="18424-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="18424-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span><span class="sxs-lookup"><span data-stu-id="18424-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="18424-134">The certificate is valid for more than 30 days.</span><span class="sxs-lookup"><span data-stu-id="18424-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="18424-135">The certificate trust chain is valid.</span><span class="sxs-lookup"><span data-stu-id="18424-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="18424-136">The certificate is password protected.</span><span class="sxs-lookup"><span data-stu-id="18424-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="18424-137">Step 3: Select servers for the update</span><span class="sxs-lookup"><span data-stu-id="18424-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="18424-138">In the next step, select the servers that need to have the SSL certificate updated.</span><span class="sxs-lookup"><span data-stu-id="18424-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="18424-139">Servers that are offline can't be selected for the update.</span><span class="sxs-lookup"><span data-stu-id="18424-139">Servers that are offline can't be selected for the update.</span></span>

![Select servers to update](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="18424-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span><span class="sxs-lookup"><span data-stu-id="18424-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![Configuration complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="18424-143">FAQs</span><span class="sxs-lookup"><span data-stu-id="18424-143">FAQs</span></span>

* <span data-ttu-id="18424-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span><span class="sxs-lookup"><span data-stu-id="18424-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="18424-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span><span class="sxs-lookup"><span data-stu-id="18424-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="18424-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="18424-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="18424-147">Wildcard certificates are also accepted.</span><span class="sxs-lookup"><span data-stu-id="18424-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="18424-148">**Why am I asked for credentials again on the WAP server page?**</span><span class="sxs-lookup"><span data-stu-id="18424-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="18424-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span><span class="sxs-lookup"><span data-stu-id="18424-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="18424-150">**The server is shown as offline. What should I do?**</span><span class="sxs-lookup"><span data-stu-id="18424-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="18424-151">Azure AD Connect can't perform any operation if the server is offline.</span><span class="sxs-lookup"><span data-stu-id="18424-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="18424-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span><span class="sxs-lookup"><span data-stu-id="18424-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="18424-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span><span class="sxs-lookup"><span data-stu-id="18424-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="18424-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span><span class="sxs-lookup"><span data-stu-id="18424-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="18424-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span><span class="sxs-lookup"><span data-stu-id="18424-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="18424-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span><span class="sxs-lookup"><span data-stu-id="18424-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="18424-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span><span class="sxs-lookup"><span data-stu-id="18424-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="18424-158">Yes.</span><span class="sxs-lookup"><span data-stu-id="18424-158">Yes.</span></span> <span data-ttu-id="18424-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span><span class="sxs-lookup"><span data-stu-id="18424-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="18424-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span><span class="sxs-lookup"><span data-stu-id="18424-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="18424-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span><span class="sxs-lookup"><span data-stu-id="18424-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="18424-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="18424-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="18424-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span><span class="sxs-lookup"><span data-stu-id="18424-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="18424-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span><span class="sxs-lookup"><span data-stu-id="18424-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="18424-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="18424-165">Next steps</span></span>

- [<span data-ttu-id="18424-166">Azure AD Connect and federation</span><span class="sxs-lookup"><span data-stu-id="18424-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="18424-167">Active Directory Federation Services management and customization with Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="18424-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)







