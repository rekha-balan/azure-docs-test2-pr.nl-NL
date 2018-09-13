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
ms.openlocfilehash: b1f1c85cea9aa7c48478ef6ee1c9a4609a3df8e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855583"
---
# <a name="tutorial-configure-hybrid-azure-active-directory-join-for-managed-domains"></a><span data-ttu-id="337d3-103">Tutorial: Configure hybrid Azure Active Directory join for managed domains</span><span class="sxs-lookup"><span data-stu-id="337d3-103">Tutorial: Configure hybrid Azure Active Directory join for managed domains</span></span>

<span data-ttu-id="337d3-104">In a similar way to a user, a device is becoming another identity you want to protect and also use to protect your resources at any time and location.</span><span class="sxs-lookup"><span data-stu-id="337d3-104">In a similar way to a user, a device is becoming another identity you want to protect and also use to protect your resources at any time and location.</span></span> <span data-ttu-id="337d3-105">You can accomplish this goal by bringing your devices' identities to Azure AD using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="337d3-105">You can accomplish this goal by bringing your devices' identities to Azure AD using one of the following methods:</span></span>

- <span data-ttu-id="337d3-106">Azure AD join</span><span class="sxs-lookup"><span data-stu-id="337d3-106">Azure AD join</span></span>
- <span data-ttu-id="337d3-107">Hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="337d3-107">Hybrid Azure AD join</span></span>
- <span data-ttu-id="337d3-108">Azure AD registration</span><span class="sxs-lookup"><span data-stu-id="337d3-108">Azure AD registration</span></span>

<span data-ttu-id="337d3-109">By bringing your devices to Azure AD, you maximize your users' productivity through single sign-on (SSO) across your cloud and on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="337d3-109">By bringing your devices to Azure AD, you maximize your users' productivity through single sign-on (SSO) across your cloud and on-premises resources.</span></span> <span data-ttu-id="337d3-110">At the same time, you can secure access to your cloud and on-premises resources with [conditional access](../active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="337d3-110">At the same time, you can secure access to your cloud and on-premises resources with [conditional access](../active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="337d3-111">In this tutorial, you learn how to configure hybrid Azure AD join for devices in managed domains.</span><span class="sxs-lookup"><span data-stu-id="337d3-111">In this tutorial, you learn how to configure hybrid Azure AD join for devices in managed domains.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="337d3-112">Configure hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="337d3-112">Configure hybrid Azure AD join</span></span>
> * <span data-ttu-id="337d3-113">Enable Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="337d3-113">Enable Windows down-level devices</span></span>
> * <span data-ttu-id="337d3-114">Verify joined devices</span><span class="sxs-lookup"><span data-stu-id="337d3-114">Verify joined devices</span></span> 
> * <span data-ttu-id="337d3-115">Troubleshoot</span><span class="sxs-lookup"><span data-stu-id="337d3-115">Troubleshoot</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="337d3-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="337d3-116">Prerequisites</span></span>

<span data-ttu-id="337d3-117">This tutorial assumes that you are familiar with:</span><span class="sxs-lookup"><span data-stu-id="337d3-117">This tutorial assumes that you are familiar with:</span></span>
    
-  [<span data-ttu-id="337d3-118">Introduction to device management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="337d3-118">Introduction to device management in Azure Active Directory</span></span>](../device-management-introduction.md)
    
-  [<span data-ttu-id="337d3-119">How to plan your hybrid Azure Active Directory join implementation</span><span class="sxs-lookup"><span data-stu-id="337d3-119">How to plan your hybrid Azure Active Directory join implementation</span></span>](hybrid-azuread-join-plan.md)

-  [<span data-ttu-id="337d3-120">How to control the hybrid Azure AD join of your devices</span><span class="sxs-lookup"><span data-stu-id="337d3-120">How to control the hybrid Azure AD join of your devices</span></span>](hybrid-azuread-join-control.md)
  

<span data-ttu-id="337d3-121">To configure the scenario in this article, you need the [latest version of Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 or higher) to be installed.</span><span class="sxs-lookup"><span data-stu-id="337d3-121">To configure the scenario in this article, you need the [latest version of Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 or higher) to be installed.</span></span> 

<span data-ttu-id="337d3-122">Verify that Azure AD Connect has synchronized the computer objects of the devices you want to be hybrid Azure AD joined to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="337d3-122">Verify that Azure AD Connect has synchronized the computer objects of the devices you want to be hybrid Azure AD joined to Azure AD.</span></span> <span data-ttu-id="337d3-123">If the computer objects belong to specific organizational units (OU), then these OUs need to be configured for synchronization in Azure AD connect as well.</span><span class="sxs-lookup"><span data-stu-id="337d3-123">If the computer objects belong to specific organizational units (OU), then these OUs need to be configured for synchronization in Azure AD connect as well.</span></span>

<span data-ttu-id="337d3-124">Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="337d3-124">Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join.</span></span> <span data-ttu-id="337d3-125">The wizard enables you to significantly simplify the configuration process.</span><span class="sxs-lookup"><span data-stu-id="337d3-125">The wizard enables you to significantly simplify the configuration process.</span></span> <span data-ttu-id="337d3-126">The related wizard configures the service connection points (SCP) for device registration.</span><span class="sxs-lookup"><span data-stu-id="337d3-126">The related wizard configures the service connection points (SCP) for device registration.</span></span>

<span data-ttu-id="337d3-127">The configuration steps in this article are based on this wizard.</span><span class="sxs-lookup"><span data-stu-id="337d3-127">The configuration steps in this article are based on this wizard.</span></span> 

<span data-ttu-id="337d3-128">Hybrid Azure AD join requires the devices to have access to the following Microsoft resources from inside your organization's network:</span><span class="sxs-lookup"><span data-stu-id="337d3-128">Hybrid Azure AD join requires the devices to have access to the following Microsoft resources from inside your organization's network:</span></span>  

- https://enterpriseregistration.windows.net
- https://login.microsoftonline.com
- https://device.login.microsoftonline.com
- <span data-ttu-id="337d3-129">https://autologon.microsoftazuread-sso.com (If you are using or planning to use Seamless SSO)</span><span class="sxs-lookup"><span data-stu-id="337d3-129">https://autologon.microsoftazuread-sso.com (If you are using or planning to use Seamless SSO)</span></span>

<span data-ttu-id="337d3-130">If your organization requires access to the Internet via an outbound proxy, starting with Windows 10 1709, you can configure proxy settings on your computer using a group policy object (GPO).</span><span class="sxs-lookup"><span data-stu-id="337d3-130">If your organization requires access to the Internet via an outbound proxy, starting with Windows 10 1709, you can configure proxy settings on your computer using a group policy object (GPO).</span></span> <span data-ttu-id="337d3-131">If your computer is running anything older than Windows 10 1709, you must implement Web Proxy Auto-Discovery (WPAD) to enable Windows 10 computers to do device registration with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="337d3-131">If your computer is running anything older than Windows 10 1709, you must implement Web Proxy Auto-Discovery (WPAD) to enable Windows 10 computers to do device registration with Azure AD.</span></span> 

<span data-ttu-id="337d3-132">If your organization requires access to the Internet via an authenticated outbound proxy, you must make sure that your Windows 10 computers can successfully authenticate to the outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="337d3-132">If your organization requires access to the Internet via an authenticated outbound proxy, you must make sure that your Windows 10 computers can successfully authenticate to the outbound proxy.</span></span> <span data-ttu-id="337d3-133">Because Windows 10 computers run device registration using machine context, it is necessary to configure outbound proxy authentication using machine context.</span><span class="sxs-lookup"><span data-stu-id="337d3-133">Because Windows 10 computers run device registration using machine context, it is necessary to configure outbound proxy authentication using machine context.</span></span> <span data-ttu-id="337d3-134">Follow up with your outbound proxy provider on the configuration requirements.</span><span class="sxs-lookup"><span data-stu-id="337d3-134">Follow up with your outbound proxy provider on the configuration requirements.</span></span> 



## <a name="configure-hybrid-azure-ad-join"></a><span data-ttu-id="337d3-135">Configure hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="337d3-135">Configure hybrid Azure AD join</span></span>

<span data-ttu-id="337d3-136">To configure a hybrid Azure AD join using Azure AD Connect, you need:</span><span class="sxs-lookup"><span data-stu-id="337d3-136">To configure a hybrid Azure AD join using Azure AD Connect, you need:</span></span>

- <span data-ttu-id="337d3-137">The credentials of a global administrator for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="337d3-137">The credentials of a global administrator for your Azure AD tenant.</span></span>  

- <span data-ttu-id="337d3-138">The enterprise administrator credentials for each of the forests.</span><span class="sxs-lookup"><span data-stu-id="337d3-138">The enterprise administrator credentials for each of the forests.</span></span>


<span data-ttu-id="337d3-139">**To configure a hybrid Azure AD join using Azure AD Connect:**</span><span class="sxs-lookup"><span data-stu-id="337d3-139">**To configure a hybrid Azure AD join using Azure AD Connect:**</span></span>

1. <span data-ttu-id="337d3-140">Launch Azure AD Connect, and then click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="337d3-140">Launch Azure AD Connect, and then click **Configure**.</span></span>

    ![Welcome](./media/hybrid-azuread-join-managed-domains/11.png)

2. <span data-ttu-id="337d3-142">On the **Additional tasks** page, select **Configure device options**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="337d3-142">On the **Additional tasks** page, select **Configure device options**, and then click **Next**.</span></span> 

    ![Additional tasks](./media/hybrid-azuread-join-managed-domains/12.png)

3. <span data-ttu-id="337d3-144">On the **Overview** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="337d3-144">On the **Overview** page, click **Next**.</span></span> 

    ![Overview](./media/hybrid-azuread-join-managed-domains/13.png)

4. <span data-ttu-id="337d3-146">On the **Connect to Azure AD** page, enter the credentials of a global administrator for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="337d3-146">On the **Connect to Azure AD** page, enter the credentials of a global administrator for your Azure AD tenant.</span></span>  

    ![Connect to Azure AD](./media/hybrid-azuread-join-managed-domains/14.png)

5. <span data-ttu-id="337d3-148">On the **Device options** page, select **Configure Hybrid Azure AD join**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="337d3-148">On the **Device options** page, select **Configure Hybrid Azure AD join**, and then click **Next**.</span></span> 

    ![Device options](./media/hybrid-azuread-join-managed-domains/15.png)

6. <span data-ttu-id="337d3-150">On the **SCP** page, for each forest you want Azure AD Connect to configure the SCP, perform the following steps, and then click **Next**:</span><span class="sxs-lookup"><span data-stu-id="337d3-150">On the **SCP** page, for each forest you want Azure AD Connect to configure the SCP, perform the following steps, and then click **Next**:</span></span> 

    ![SCP](./media/hybrid-azuread-join-managed-domains/16.png)

    <span data-ttu-id="337d3-152">a.</span><span class="sxs-lookup"><span data-stu-id="337d3-152">a.</span></span> <span data-ttu-id="337d3-153">Select the forest.</span><span class="sxs-lookup"><span data-stu-id="337d3-153">Select the forest.</span></span>

    <span data-ttu-id="337d3-154">b.</span><span class="sxs-lookup"><span data-stu-id="337d3-154">b.</span></span> <span data-ttu-id="337d3-155">Select the authentication service.</span><span class="sxs-lookup"><span data-stu-id="337d3-155">Select the authentication service.</span></span>

    <span data-ttu-id="337d3-156">c.</span><span class="sxs-lookup"><span data-stu-id="337d3-156">c.</span></span> <span data-ttu-id="337d3-157">Click **Add** to enter the enterprise administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="337d3-157">Click **Add** to enter the enterprise administrator credentials.</span></span>


7. <span data-ttu-id="337d3-158">On the **Device operating systems** page, select the operating systems used by devices in your Active Directory environment, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="337d3-158">On the **Device operating systems** page, select the operating systems used by devices in your Active Directory environment, and then click **Next**.</span></span> 

    ![Device operating system](./media/hybrid-azuread-join-managed-domains/17.png)


8. <span data-ttu-id="337d3-160">On the **Ready to configure** page, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="337d3-160">On the **Ready to configure** page, click **Configure**.</span></span> 

    ![Ready to configure](./media/hybrid-azuread-join-managed-domains/19.png)

9. <span data-ttu-id="337d3-162">On the **Configuration complete** page, click **Exit**.</span><span class="sxs-lookup"><span data-stu-id="337d3-162">On the **Configuration complete** page, click **Exit**.</span></span> 

    ![Configuration complete](./media/hybrid-azuread-join-managed-domains/20.png)




## <a name="enable-windows-down-level-devices"></a><span data-ttu-id="337d3-164">Enable Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="337d3-164">Enable Windows down-level devices</span></span>

<span data-ttu-id="337d3-165">If some of your domain-joined devices are Windows down-level devices, you need to:</span><span class="sxs-lookup"><span data-stu-id="337d3-165">If some of your domain-joined devices are Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="337d3-166">Update device settings</span><span class="sxs-lookup"><span data-stu-id="337d3-166">Update device settings</span></span>
 
- <span data-ttu-id="337d3-167">Configure the local intranet settings for device registration</span><span class="sxs-lookup"><span data-stu-id="337d3-167">Configure the local intranet settings for device registration</span></span>

### <a name="update-device-settings"></a><span data-ttu-id="337d3-168">Update device settings</span><span class="sxs-lookup"><span data-stu-id="337d3-168">Update device settings</span></span> 

<span data-ttu-id="337d3-169">To register Windows down-level devices, you need to make sure that the device settings to allow users to register devices in Azure AD are set.</span><span class="sxs-lookup"><span data-stu-id="337d3-169">To register Windows down-level devices, you need to make sure that the device settings to allow users to register devices in Azure AD are set.</span></span> <span data-ttu-id="337d3-170">In the Azure portal, you can find this setting  under:</span><span class="sxs-lookup"><span data-stu-id="337d3-170">In the Azure portal, you can find this setting  under:</span></span>

`Home > [Name of your tenant] > Devices - Device settings`  


    
<span data-ttu-id="337d3-171">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span><span class="sxs-lookup"><span data-stu-id="337d3-171">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Register devices](media/hybrid-azuread-join-managed-domains/23.png)



### <a name="configure-the-local-intranet-settings-for-device-registration"></a><span data-ttu-id="337d3-173">Configure the local intranet settings for device registration</span><span class="sxs-lookup"><span data-stu-id="337d3-173">Configure the local intranet settings for device registration</span></span>

<span data-ttu-id="337d3-174">To successfully complete hybrid Azure AD join of your Windows down-level devices, and to avoid certificate prompts when devices authenticate authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URLs to the Local Intranet zone in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="337d3-174">To successfully complete hybrid Azure AD join of your Windows down-level devices, and to avoid certificate prompts when devices authenticate authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URLs to the Local Intranet zone in Internet Explorer:</span></span>

- `https://device.login.microsoftonline.com`

- <span data-ttu-id="337d3-175">`https://autologon.microsoftazuread-sso.com`.</span><span class="sxs-lookup"><span data-stu-id="337d3-175">`https://autologon.microsoftazuread-sso.com`.</span></span>

<span data-ttu-id="337d3-176">Additionally, you need to enable **Allow updates to status bar via script** in the user’s local intranet zone.</span><span class="sxs-lookup"><span data-stu-id="337d3-176">Additionally, you need to enable **Allow updates to status bar via script** in the user’s local intranet zone.</span></span>

## <a name="verify-the-registration"></a><span data-ttu-id="337d3-177">Verify the registration</span><span class="sxs-lookup"><span data-stu-id="337d3-177">Verify the registration</span></span>

<span data-ttu-id="337d3-178">To verify the device registration state in your Azure tenant, you can use the **[Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)** cmdlet in the **[Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0)**.</span><span class="sxs-lookup"><span data-stu-id="337d3-178">To verify the device registration state in your Azure tenant, you can use the **[Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)** cmdlet in the **[Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0)**.</span></span>

<span data-ttu-id="337d3-179">When using the **Get-MSolDevice** cmdlet to check the service details:</span><span class="sxs-lookup"><span data-stu-id="337d3-179">When using the **Get-MSolDevice** cmdlet to check the service details:</span></span>

- <span data-ttu-id="337d3-180">An object with the **device id** that matches the ID on the Windows client must exist.</span><span class="sxs-lookup"><span data-stu-id="337d3-180">An object with the **device id** that matches the ID on the Windows client must exist.</span></span>
- <span data-ttu-id="337d3-181">The value for **DeviceTrustType** must be **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="337d3-181">The value for **DeviceTrustType** must be **Domain Joined**.</span></span> <span data-ttu-id="337d3-182">This is equivalent to the **Hybrid Azure AD joined** state on the Devices page in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="337d3-182">This is equivalent to the **Hybrid Azure AD joined** state on the Devices page in the Azure AD portal.</span></span>
- <span data-ttu-id="337d3-183">The value for **Enabled** must be **True** for devices that are used in conditional access.</span><span class="sxs-lookup"><span data-stu-id="337d3-183">The value for **Enabled** must be **True** for devices that are used in conditional access.</span></span> 


<span data-ttu-id="337d3-184">**To check the service details:**</span><span class="sxs-lookup"><span data-stu-id="337d3-184">**To check the service details:**</span></span>

1. <span data-ttu-id="337d3-185">Open **Windows PowerShell** as administrator.</span><span class="sxs-lookup"><span data-stu-id="337d3-185">Open **Windows PowerShell** as administrator.</span></span>

2. <span data-ttu-id="337d3-186">Type `Connect-MsolService` to connect to your Azure tenant.</span><span class="sxs-lookup"><span data-stu-id="337d3-186">Type `Connect-MsolService` to connect to your Azure tenant.</span></span>  

3. <span data-ttu-id="337d3-187">Type `get-msoldevice -deviceId <deviceId>`.</span><span class="sxs-lookup"><span data-stu-id="337d3-187">Type `get-msoldevice -deviceId <deviceId>`.</span></span>

6. <span data-ttu-id="337d3-188">Verify that **Enabled** is set to **True**.</span><span class="sxs-lookup"><span data-stu-id="337d3-188">Verify that **Enabled** is set to **True**.</span></span>





## <a name="troubleshoot-your-implementation"></a><span data-ttu-id="337d3-189">Troubleshoot your implementation</span><span class="sxs-lookup"><span data-stu-id="337d3-189">Troubleshoot your implementation</span></span>

<span data-ttu-id="337d3-190">If you are experiencing issues with completing hybrid Azure AD join for domain joined Windows devices, see:</span><span class="sxs-lookup"><span data-stu-id="337d3-190">If you are experiencing issues with completing hybrid Azure AD join for domain joined Windows devices, see:</span></span>

- [<span data-ttu-id="337d3-191">Troubleshooting Hybrid Azure AD join for Windows current devices</span><span class="sxs-lookup"><span data-stu-id="337d3-191">Troubleshooting Hybrid Azure AD join for Windows current devices</span></span>](troubleshoot-hybrid-join-windows-current.md)
- [<span data-ttu-id="337d3-192">Troubleshooting Hybrid Azure AD join for Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="337d3-192">Troubleshooting Hybrid Azure AD join for Windows down-level devices</span></span>](troubleshoot-hybrid-join-windows-legacy.md)


## <a name="next-steps"></a><span data-ttu-id="337d3-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="337d3-193">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="337d3-194">[Configure hybrid Azure Active Directory join for federated domains](hybrid-azuread-join-federated-domains.md)
> [Configure hybrid Azure Active Directory join manually](hybrid-azuread-join-manual-steps.md)</span><span class="sxs-lookup"><span data-stu-id="337d3-194">[Configure hybrid Azure Active Directory join for federated domains](hybrid-azuread-join-federated-domains.md)
[Configure hybrid Azure Active Directory join manually](hybrid-azuread-join-manual-steps.md)</span></span>

