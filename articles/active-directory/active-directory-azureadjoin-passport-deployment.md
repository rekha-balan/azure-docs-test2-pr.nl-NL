---
title: Enable Microsoft Windows Hello for Business in your organization | Microsoft Docs
description: Deployment instructions to enable Microsoft Passport in your organization.
services: active-directory
documentationcenter: ''
keywords: configure Microsoft Passport, Microsoft Windows Hello for Business deployment
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: a2b429281b602295a362b80e256b7755083fbace
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555950"
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="913f9-104">Enable Microsoft Windows Hello for Business in your organization</span><span class="sxs-lookup"><span data-stu-id="913f9-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="913f9-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span><span class="sxs-lookup"><span data-stu-id="913f9-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="913f9-106">Deploy System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="913f9-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="913f9-107">Configure policy settings</span><span class="sxs-lookup"><span data-stu-id="913f9-107">Configure policy settings</span></span>
3. <span data-ttu-id="913f9-108">Configure the certificate profile</span><span class="sxs-lookup"><span data-stu-id="913f9-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="913f9-109">Deploy System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="913f9-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="913f9-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span><span class="sxs-lookup"><span data-stu-id="913f9-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="913f9-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span><span class="sxs-lookup"><span data-stu-id="913f9-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="913f9-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="913f9-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="913f9-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span><span class="sxs-lookup"><span data-stu-id="913f9-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="913f9-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span><span class="sxs-lookup"><span data-stu-id="913f9-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="913f9-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="913f9-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="913f9-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="913f9-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="913f9-117">Configure policy settings</span><span class="sxs-lookup"><span data-stu-id="913f9-117">Configure policy settings</span></span>
<span data-ttu-id="913f9-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span><span class="sxs-lookup"><span data-stu-id="913f9-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="913f9-119">Group Policy in Active Directory</span><span class="sxs-lookup"><span data-stu-id="913f9-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="913f9-120">The System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="913f9-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="913f9-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span><span class="sxs-lookup"><span data-stu-id="913f9-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="913f9-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span><span class="sxs-lookup"><span data-stu-id="913f9-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="913f9-123">This scenario:</span><span class="sxs-lookup"><span data-stu-id="913f9-123">This scenario:</span></span>

* <span data-ttu-id="913f9-124">Ensures compatibility with the newer deployment scenarios</span><span class="sxs-lookup"><span data-stu-id="913f9-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="913f9-125">Requires on the client side Windows 10 Version 1607 or better.</span><span class="sxs-lookup"><span data-stu-id="913f9-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="913f9-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span><span class="sxs-lookup"><span data-stu-id="913f9-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="913f9-127">**Steps**:</span><span class="sxs-lookup"><span data-stu-id="913f9-127">**Steps**:</span></span>

1. <span data-ttu-id="913f9-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span><span class="sxs-lookup"><span data-stu-id="913f9-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="913f9-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="913f9-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="913f9-130">Right-click **Group Policy Objects**, and select **New**.</span><span class="sxs-lookup"><span data-stu-id="913f9-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="913f9-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="913f9-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="913f9-132">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="913f9-132">Click **OK**.</span></span>
4. <span data-ttu-id="913f9-133">Right-click your new Group Policy Object, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="913f9-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="913f9-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span><span class="sxs-lookup"><span data-stu-id="913f9-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="913f9-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="913f9-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="913f9-136">Select the **Enabled** option button, and then click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="913f9-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="913f9-137">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="913f9-137">Click **OK**.</span></span>
8. <span data-ttu-id="913f9-138">You can now link the Group Policy Object to a location of your choice.</span><span class="sxs-lookup"><span data-stu-id="913f9-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="913f9-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span><span class="sxs-lookup"><span data-stu-id="913f9-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="913f9-140">For example:</span><span class="sxs-lookup"><span data-stu-id="913f9-140">For example:</span></span>
   * <span data-ttu-id="913f9-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span><span class="sxs-lookup"><span data-stu-id="913f9-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="913f9-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span><span class="sxs-lookup"><span data-stu-id="913f9-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="913f9-143">Configure Windows Hello for Business using System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="913f9-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="913f9-144">**Steps**:</span><span class="sxs-lookup"><span data-stu-id="913f9-144">**Steps**:</span></span>

1. <span data-ttu-id="913f9-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span><span class="sxs-lookup"><span data-stu-id="913f9-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Configure Windows Hello for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="913f9-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span><span class="sxs-lookup"><span data-stu-id="913f9-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Configure Windows Hello for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="913f9-149">On the **General** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="913f9-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![Configure Windows Hello for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="913f9-151">a.</span><span class="sxs-lookup"><span data-stu-id="913f9-151">a.</span></span> <span data-ttu-id="913f9-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span><span class="sxs-lookup"><span data-stu-id="913f9-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="913f9-153">b.</span><span class="sxs-lookup"><span data-stu-id="913f9-153">b.</span></span> <span data-ttu-id="913f9-154">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="913f9-154">Click **Next**.</span></span>
4. <span data-ttu-id="913f9-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="913f9-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Configure Windows Hello for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="913f9-157">On the **Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="913f9-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![Configure Windows Hello for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="913f9-159">a.</span><span class="sxs-lookup"><span data-stu-id="913f9-159">a.</span></span> <span data-ttu-id="913f9-160">As **Configure Windows Hello for Business**, select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="913f9-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="913f9-161">b.</span><span class="sxs-lookup"><span data-stu-id="913f9-161">b.</span></span> <span data-ttu-id="913f9-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span><span class="sxs-lookup"><span data-stu-id="913f9-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="913f9-163">c.</span><span class="sxs-lookup"><span data-stu-id="913f9-163">c.</span></span> <span data-ttu-id="913f9-164">As **Authentication method**, select **Certificate-based**.</span><span class="sxs-lookup"><span data-stu-id="913f9-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="913f9-165">d.</span><span class="sxs-lookup"><span data-stu-id="913f9-165">d.</span></span> <span data-ttu-id="913f9-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="913f9-166">Click **Next**.</span></span>
6. <span data-ttu-id="913f9-167">On the **Summary** dialog, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="913f9-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="913f9-168">On the **Completion** dialog, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="913f9-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="913f9-169">In the toolbar on the top, click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="913f9-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![Configure Windows Hello for Business](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="913f9-171">Configure the certificate profile</span><span class="sxs-lookup"><span data-stu-id="913f9-171">Configure the certificate profile</span></span>
<span data-ttu-id="913f9-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span><span class="sxs-lookup"><span data-stu-id="913f9-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="913f9-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="913f9-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="913f9-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="913f9-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="913f9-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span><span class="sxs-lookup"><span data-stu-id="913f9-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="913f9-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span><span class="sxs-lookup"><span data-stu-id="913f9-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="913f9-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span><span class="sxs-lookup"><span data-stu-id="913f9-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="913f9-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="913f9-178">Next steps</span></span>
* [<span data-ttu-id="913f9-179">Windows 10 for the enterprise: Ways to use devices for work</span><span class="sxs-lookup"><span data-stu-id="913f9-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="913f9-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="913f9-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="913f9-181">Authenticating identities without passwords through Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="913f9-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="913f9-182">Learn about usage scenarios for Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="913f9-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="913f9-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span><span class="sxs-lookup"><span data-stu-id="913f9-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="913f9-184">Set up Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="913f9-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)







