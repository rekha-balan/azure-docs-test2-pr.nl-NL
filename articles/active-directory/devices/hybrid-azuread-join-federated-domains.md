---
title: How to configure hybrid Azure Active Directory joined devices | Microsoft Docs
description: Learn how to configure hybrid Azure Active Directory joined devices.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 08/25/2018
ms.author: markvi
ms.reviewer: sandeo
ms.openlocfilehash: f4659d2dc8dfd52ae6f7ec19dc29ec31c9b3ca6b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858045"
---
# <a name="tutorial-configure-hybrid-azure-active-directory-join-for-federated-domains"></a><span data-ttu-id="d4894-103">Tutorial: Configure hybrid Azure Active Directory join for federated domains</span><span class="sxs-lookup"><span data-stu-id="d4894-103">Tutorial: Configure hybrid Azure Active Directory join for federated domains</span></span>

<span data-ttu-id="d4894-104">In a similar way to a user, a device is becoming another identity you want to protect and also use to protect your resources at any time and location.</span><span class="sxs-lookup"><span data-stu-id="d4894-104">In a similar way to a user, a device is becoming another identity you want to protect and also use to protect your resources at any time and location.</span></span> <span data-ttu-id="d4894-105">You can accomplish this goal by bringing your devices' identities to Azure AD using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="d4894-105">You can accomplish this goal by bringing your devices' identities to Azure AD using one of the following methods:</span></span>

- <span data-ttu-id="d4894-106">Azure AD join</span><span class="sxs-lookup"><span data-stu-id="d4894-106">Azure AD join</span></span>
- <span data-ttu-id="d4894-107">Hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="d4894-107">Hybrid Azure AD join</span></span>
- <span data-ttu-id="d4894-108">Azure AD registration</span><span class="sxs-lookup"><span data-stu-id="d4894-108">Azure AD registration</span></span>

<span data-ttu-id="d4894-109">By bringing your devices to Azure AD, you maximize your users' productivity through single sign-on (SSO) across your cloud and on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="d4894-109">By bringing your devices to Azure AD, you maximize your users' productivity through single sign-on (SSO) across your cloud and on-premises resources.</span></span> <span data-ttu-id="d4894-110">At the same time, you can secure access to your cloud and on-premises resources with [conditional access](../active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d4894-110">At the same time, you can secure access to your cloud and on-premises resources with [conditional access](../active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="d4894-111">In this tutorial, you learn how to configure hybrid Azure AD join for devices that federated using ADFS.</span><span class="sxs-lookup"><span data-stu-id="d4894-111">In this tutorial, you learn how to configure hybrid Azure AD join for devices that federated using ADFS.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d4894-112">Configure hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="d4894-112">Configure hybrid Azure AD join</span></span>
> * <span data-ttu-id="d4894-113">Enable Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="d4894-113">Enable Windows down-level devices</span></span>
> * <span data-ttu-id="d4894-114">Verify the registration</span><span class="sxs-lookup"><span data-stu-id="d4894-114">Verify the registration</span></span>
> * <span data-ttu-id="d4894-115">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="d4894-115">Troubleshoot</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d4894-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d4894-116">Prerequisites</span></span>

<span data-ttu-id="d4894-117">This tutorial assumes that you are familiar with:</span><span class="sxs-lookup"><span data-stu-id="d4894-117">This tutorial assumes that you are familiar with:</span></span>

-  [<span data-ttu-id="d4894-118">Introduction to device management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4894-118">Introduction to device management in Azure Active Directory</span></span>](../device-management-introduction.md)

-  [<span data-ttu-id="d4894-119">How to plan your hybrid Azure Active Directory join implementation</span><span class="sxs-lookup"><span data-stu-id="d4894-119">How to plan your hybrid Azure Active Directory join implementation</span></span>](hybrid-azuread-join-plan.md)

-  [<span data-ttu-id="d4894-120">How to control the hybrid Azure AD join of your devices</span><span class="sxs-lookup"><span data-stu-id="d4894-120">How to control the hybrid Azure AD join of your devices</span></span>](hybrid-azuread-join-control.md)


<span data-ttu-id="d4894-121">To configure the scenario in this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="d4894-121">To configure the scenario in this tutorial, you need:</span></span>

- <span data-ttu-id="d4894-122">Windows Server 2012 R2 with AD FS</span><span class="sxs-lookup"><span data-stu-id="d4894-122">Windows Server 2012 R2 with AD FS</span></span>

- <span data-ttu-id="d4894-123">[Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) version 1.1.819.0 or higher.</span><span class="sxs-lookup"><span data-stu-id="d4894-123">[Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) version 1.1.819.0 or higher.</span></span> 
 

<span data-ttu-id="d4894-124">Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="d4894-124">Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join.</span></span> <span data-ttu-id="d4894-125">The wizard enables you to significantly simplify the configuration process.</span><span class="sxs-lookup"><span data-stu-id="d4894-125">The wizard enables you to significantly simplify the configuration process.</span></span> <span data-ttu-id="d4894-126">The related wizard:</span><span class="sxs-lookup"><span data-stu-id="d4894-126">The related wizard:</span></span>

- <span data-ttu-id="d4894-127">Configures the service connection points (SCP) for device registration</span><span class="sxs-lookup"><span data-stu-id="d4894-127">Configures the service connection points (SCP) for device registration</span></span>

- <span data-ttu-id="d4894-128">Backs up your existing Azure AD relying party trust</span><span class="sxs-lookup"><span data-stu-id="d4894-128">Backs up your existing Azure AD relying party trust</span></span>

- <span data-ttu-id="d4894-129">Updates the claim rules in your Azure AD trust</span><span class="sxs-lookup"><span data-stu-id="d4894-129">Updates the claim rules in your Azure AD trust</span></span>

<span data-ttu-id="d4894-130">The configuration steps in this article are based on this wizard.</span><span class="sxs-lookup"><span data-stu-id="d4894-130">The configuration steps in this article are based on this wizard.</span></span> <span data-ttu-id="d4894-131">If you have an older version of Azure AD Connect installed, you need upgrade it to 1.1.819 or higher.</span><span class="sxs-lookup"><span data-stu-id="d4894-131">If you have an older version of Azure AD Connect installed, you need upgrade it to 1.1.819 or higher.</span></span> <span data-ttu-id="d4894-132">If installing the latest version of Azure AD Connect is not an option for you, see [how to manually configure device registration](../device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d4894-132">If installing the latest version of Azure AD Connect is not an option for you, see [how to manually configure device registration](../device-management-hybrid-azuread-joined-devices-setup.md).</span></span>

<span data-ttu-id="d4894-133">Hybrid Azure AD join requires the devices to have access to the following Microsoft resources from inside your organization's network:</span><span class="sxs-lookup"><span data-stu-id="d4894-133">Hybrid Azure AD join requires the devices to have access to the following Microsoft resources from inside your organization's network:</span></span>  

- https://enterpriseregistration.windows.net
- https://login.microsoftonline.com
- https://device.login.microsoftonline.com
- <span data-ttu-id="d4894-134">Your organization's STS (federated domains)</span><span class="sxs-lookup"><span data-stu-id="d4894-134">Your organization's STS (federated domains)</span></span>
- <span data-ttu-id="d4894-135">https://autologon.microsoftazuread-sso.com (If you are using or planning to use Seamless SSO)</span><span class="sxs-lookup"><span data-stu-id="d4894-135">https://autologon.microsoftazuread-sso.com (If you are using or planning to use Seamless SSO)</span></span>

<span data-ttu-id="d4894-136">If your organization requires access to the Internet via an outbound proxy, starting with Windows 10 1709, you can configure proxy settings on your computer using a group policy object (GPO).</span><span class="sxs-lookup"><span data-stu-id="d4894-136">If your organization requires access to the Internet via an outbound proxy, starting with Windows 10 1709, you can configure proxy settings on your computer using a group policy object (GPO).</span></span> <span data-ttu-id="d4894-137">If your computer is running anything older than Windows 10 1709, you must implement Web Proxy Auto-Discovery (WPAD) to enable Windows 10 computers to do device registration with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4894-137">If your computer is running anything older than Windows 10 1709, you must implement Web Proxy Auto-Discovery (WPAD) to enable Windows 10 computers to do device registration with Azure AD.</span></span> 

<span data-ttu-id="d4894-138">If your organization requires access to the Internet via an authenticated outbound proxy, you must make sure that your Windows 10 computers can successfully authenticate to the outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d4894-138">If your organization requires access to the Internet via an authenticated outbound proxy, you must make sure that your Windows 10 computers can successfully authenticate to the outbound proxy.</span></span> <span data-ttu-id="d4894-139">Because Windows 10 computers run device registration using machine context, it is necessary to configure outbound proxy authentication using machine context.</span><span class="sxs-lookup"><span data-stu-id="d4894-139">Because Windows 10 computers run device registration using machine context, it is necessary to configure outbound proxy authentication using machine context.</span></span> <span data-ttu-id="d4894-140">Follow up with your outbound proxy provider on the configuration requirements.</span><span class="sxs-lookup"><span data-stu-id="d4894-140">Follow up with your outbound proxy provider on the configuration requirements.</span></span> 


## <a name="configure-hybrid-azure-ad-join"></a><span data-ttu-id="d4894-141">Configure hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="d4894-141">Configure hybrid Azure AD join</span></span>

<span data-ttu-id="d4894-142">To configure a hybrid Azure AD join using Azure AD Connect, you need:</span><span class="sxs-lookup"><span data-stu-id="d4894-142">To configure a hybrid Azure AD join using Azure AD Connect, you need:</span></span>

- <span data-ttu-id="d4894-143">The credentials of a global administrator for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="d4894-143">The credentials of a global administrator for your Azure AD tenant.</span></span>  

- <span data-ttu-id="d4894-144">The enterprise administrator credentials for each of the forests.</span><span class="sxs-lookup"><span data-stu-id="d4894-144">The enterprise administrator credentials for each of the forests.</span></span>

- <span data-ttu-id="d4894-145">The credentials of your AD FS administrator.</span><span class="sxs-lookup"><span data-stu-id="d4894-145">The credentials of your AD FS administrator.</span></span> 


<span data-ttu-id="d4894-146">**To configure a hybrid Azure AD join using Azure AD Connect:**</span><span class="sxs-lookup"><span data-stu-id="d4894-146">**To configure a hybrid Azure AD join using Azure AD Connect:**</span></span>

1. <span data-ttu-id="d4894-147">Launch Azure AD Connect, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="d4894-147">Launch Azure AD Connect, and then click **Configure**.</span></span>

    ![Welcome](./media/hybrid-azuread-join-federated-domains/11.png)

2. <span data-ttu-id="d4894-149">On the **Additional tasks** page, select **Configure device options**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d4894-149">On the **Additional tasks** page, select **Configure device options**, and then click **Next**.</span></span> 

    ![Additional tasks](./media/hybrid-azuread-join-federated-domains/12.png)

3. <span data-ttu-id="d4894-151">On the **Overview** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d4894-151">On the **Overview** page, click **Next**.</span></span> 

    ![Overview](./media/hybrid-azuread-join-federated-domains/13.png)

4. <span data-ttu-id="d4894-153">On the **Connect to Azure AD** page, enter the credentials of a global administrator for your Azure AD tenant, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d4894-153">On the **Connect to Azure AD** page, enter the credentials of a global administrator for your Azure AD tenant, and then click **Next**.</span></span>   

    ![Connect to Azure AD](./media/hybrid-azuread-join-federated-domains/14.png)

5. <span data-ttu-id="d4894-155">On the **Device options** page, select **Configure Hybrid Azure AD join**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d4894-155">On the **Device options** page, select **Configure Hybrid Azure AD join**, and then click **Next**.</span></span> 

    ![Device options](./media/hybrid-azuread-join-federated-domains/15.png)

6. <span data-ttu-id="d4894-157">On the **SCP** page, perform the following steps, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="d4894-157">On the **SCP** page, perform the following steps, and then click **Next**:</span></span> 

    ![SCP](./media/hybrid-azuread-join-federated-domains/16.png)

    <span data-ttu-id="d4894-159">a.</span><span class="sxs-lookup"><span data-stu-id="d4894-159">a.</span></span> <span data-ttu-id="d4894-160">Select the forest.</span><span class="sxs-lookup"><span data-stu-id="d4894-160">Select the forest.</span></span>

    <span data-ttu-id="d4894-161">b.</span><span class="sxs-lookup"><span data-stu-id="d4894-161">b.</span></span> <span data-ttu-id="d4894-162">Select the authentication service.</span><span class="sxs-lookup"><span data-stu-id="d4894-162">Select the authentication service.</span></span>

    <span data-ttu-id="d4894-163">c.</span><span class="sxs-lookup"><span data-stu-id="d4894-163">c.</span></span> <span data-ttu-id="d4894-164">Click **Add** to enter the enterprise administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="d4894-164">Click **Add** to enter the enterprise administrator credentials.</span></span>


7. <span data-ttu-id="d4894-165">On the **Device operating systems** page, select the operating systems used by devices in your Active Directory environment, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d4894-165">On the **Device operating systems** page, select the operating systems used by devices in your Active Directory environment, and then click **Next**.</span></span> 

    ![Device operating system](./media/hybrid-azuread-join-federated-domains/17.png)

8. <span data-ttu-id="d4894-167">On the **Federation configuration** page, enter the credentials of your AD FS administrator, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d4894-167">On the **Federation configuration** page, enter the credentials of your AD FS administrator, and then click **Next**.</span></span> 

    ![Federation configuration](./media/hybrid-azuread-join-federated-domains/18.png)

9. <span data-ttu-id="d4894-169">On the **Ready to configure** page, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="d4894-169">On the **Ready to configure** page, click **Configure**.</span></span> 

    ![Ready to configure](./media/hybrid-azuread-join-federated-domains/19.png)

10. <span data-ttu-id="d4894-171">On the **Configuration complete** page, click **Exit**.</span><span class="sxs-lookup"><span data-stu-id="d4894-171">On the **Configuration complete** page, click **Exit**.</span></span> 

    ![Configuration complete](./media/hybrid-azuread-join-federated-domains/20.png)




## <a name="enable-windows-down-level-devices"></a><span data-ttu-id="d4894-173">Enable Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="d4894-173">Enable Windows down-level devices</span></span>

<span data-ttu-id="d4894-174">If some of your domain-joined devices are Windows down-level devices, you need to:</span><span class="sxs-lookup"><span data-stu-id="d4894-174">If some of your domain-joined devices are Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="d4894-175">Update device settings</span><span class="sxs-lookup"><span data-stu-id="d4894-175">Update device settings</span></span>
 
- <span data-ttu-id="d4894-176">Configure the local intranet settings for device registration</span><span class="sxs-lookup"><span data-stu-id="d4894-176">Configure the local intranet settings for device registration</span></span>


### <a name="update-device-settings"></a><span data-ttu-id="d4894-177">Update device settings</span><span class="sxs-lookup"><span data-stu-id="d4894-177">Update device settings</span></span> 

<span data-ttu-id="d4894-178">To register Windows down-level devices, you need to make sure that the device settings to allow users to register devices in Azure AD are set.</span><span class="sxs-lookup"><span data-stu-id="d4894-178">To register Windows down-level devices, you need to make sure that the device settings to allow users to register devices in Azure AD are set.</span></span> <span data-ttu-id="d4894-179">In the Azure portal, you can find this setting  under:</span><span class="sxs-lookup"><span data-stu-id="d4894-179">In the Azure portal, you can find this setting  under:</span></span>

`Home > [Name of your tenant] > Devices - Device settings`  


    
<span data-ttu-id="d4894-180">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span><span class="sxs-lookup"><span data-stu-id="d4894-180">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Register devices](./media/hybrid-azuread-join-federated-domains/23.png)


### <a name="configure-the-local-intranet-settings-for-device-registration"></a><span data-ttu-id="d4894-182">Configure the local intranet settings for device registration</span><span class="sxs-lookup"><span data-stu-id="d4894-182">Configure the local intranet settings for device registration</span></span>

<span data-ttu-id="d4894-183">To successfully complete hybrid Azure AD join of your Windows down-level devices, and to avoid certificate prompts when devices authenticate authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URLs to the Local Intranet zone in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="d4894-183">To successfully complete hybrid Azure AD join of your Windows down-level devices, and to avoid certificate prompts when devices authenticate authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URLs to the Local Intranet zone in Internet Explorer:</span></span>

- `https://device.login.microsoftonline.com`

- `https://device.login.microsoftonline.com`

- <span data-ttu-id="d4894-184">Your organization's Security Token Service (STS - federated domains)</span><span class="sxs-lookup"><span data-stu-id="d4894-184">Your organization's Security Token Service (STS - federated domains)</span></span>

- <span data-ttu-id="d4894-185">`https://autologon.microsoftazuread-sso.com` (for Seamless SSO).</span><span class="sxs-lookup"><span data-stu-id="d4894-185">`https://autologon.microsoftazuread-sso.com` (for Seamless SSO).</span></span>

<span data-ttu-id="d4894-186">Additionally, you need to enable **Allow updates to status bar via script** in the user’s local intranet zone.</span><span class="sxs-lookup"><span data-stu-id="d4894-186">Additionally, you need to enable **Allow updates to status bar via script** in the user’s local intranet zone.</span></span>



## <a name="verify-the-registration"></a><span data-ttu-id="d4894-187">Verify the registration</span><span class="sxs-lookup"><span data-stu-id="d4894-187">Verify the registration</span></span>

<span data-ttu-id="d4894-188">To verify the device registration state in your Azure tenant, you can use the **[Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)** cmdlet in the **[Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0)**.</span><span class="sxs-lookup"><span data-stu-id="d4894-188">To verify the device registration state in your Azure tenant, you can use the **[Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)** cmdlet in the **[Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0)**.</span></span>

<span data-ttu-id="d4894-189">When using the **Get-MSolDevice** cmdlet to check the service details:</span><span class="sxs-lookup"><span data-stu-id="d4894-189">When using the **Get-MSolDevice** cmdlet to check the service details:</span></span>

- <span data-ttu-id="d4894-190">An object with the **device id** that matches the ID on the Windows client must exist.</span><span class="sxs-lookup"><span data-stu-id="d4894-190">An object with the **device id** that matches the ID on the Windows client must exist.</span></span>
- <span data-ttu-id="d4894-191">The value for **DeviceTrustType** must be **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="d4894-191">The value for **DeviceTrustType** must be **Domain Joined**.</span></span> <span data-ttu-id="d4894-192">This is equivalent to the **Hybrid Azure AD joined** state on the Devices page in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="d4894-192">This is equivalent to the **Hybrid Azure AD joined** state on the Devices page in the Azure AD portal.</span></span>
- <span data-ttu-id="d4894-193">The value for **Enabled** must be **True** for devices that are used in conditional access.</span><span class="sxs-lookup"><span data-stu-id="d4894-193">The value for **Enabled** must be **True** for devices that are used in conditional access.</span></span> 


<span data-ttu-id="d4894-194">**To check the service details:**</span><span class="sxs-lookup"><span data-stu-id="d4894-194">**To check the service details:**</span></span>

1. <span data-ttu-id="d4894-195">Open **Windows PowerShell** as administrator.</span><span class="sxs-lookup"><span data-stu-id="d4894-195">Open **Windows PowerShell** as administrator.</span></span>

2. <span data-ttu-id="d4894-196">Type `Connect-MsolService` to connect to your Azure tenant.</span><span class="sxs-lookup"><span data-stu-id="d4894-196">Type `Connect-MsolService` to connect to your Azure tenant.</span></span>  

3. <span data-ttu-id="d4894-197">Type `get-msoldevice -deviceId <deviceId>`.</span><span class="sxs-lookup"><span data-stu-id="d4894-197">Type `get-msoldevice -deviceId <deviceId>`.</span></span>

6. <span data-ttu-id="d4894-198">Verify that **Enabled** is set to **True**.</span><span class="sxs-lookup"><span data-stu-id="d4894-198">Verify that **Enabled** is set to **True**.</span></span>





## <a name="troubleshoot-your-implementation"></a><span data-ttu-id="d4894-199">Troubleshoot your implementation</span><span class="sxs-lookup"><span data-stu-id="d4894-199">Troubleshoot your implementation</span></span>

<span data-ttu-id="d4894-200">If you are experiencing issues with completing hybrid Azure AD join for domain joined Windows devices, see:</span><span class="sxs-lookup"><span data-stu-id="d4894-200">If you are experiencing issues with completing hybrid Azure AD join for domain joined Windows devices, see:</span></span>

- [<span data-ttu-id="d4894-201">Troubleshooting Hybrid Azure AD join for Windows current devices</span><span class="sxs-lookup"><span data-stu-id="d4894-201">Troubleshooting Hybrid Azure AD join for Windows current devices</span></span>](troubleshoot-hybrid-join-windows-current.md)
- [<span data-ttu-id="d4894-202">Troubleshooting Hybrid Azure AD join for Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="d4894-202">Troubleshooting Hybrid Azure AD join for Windows down-level devices</span></span>](troubleshoot-hybrid-join-windows-legacy.md)



## <a name="next-steps"></a><span data-ttu-id="d4894-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4894-203">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="d4894-204">[Configure hybrid Azure Active Directory join for managed domains](hybrid-azuread-join-managed-domains.md)
> [Configure hybrid Azure Active Directory join manually](hybrid-azuread-join-manual-steps.md)</span><span class="sxs-lookup"><span data-stu-id="d4894-204">[Configure hybrid Azure Active Directory join for managed domains](hybrid-azuread-join-managed-domains.md)
[Configure hybrid Azure Active Directory join manually](hybrid-azuread-join-manual-steps.md)</span></span>




<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
