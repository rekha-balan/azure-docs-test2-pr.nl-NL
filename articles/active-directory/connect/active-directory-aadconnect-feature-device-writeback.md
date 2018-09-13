---
title: 'Azure AD Connect: Enabling device writeback | Microsoft Docs'
description: This document details how to enable device writeback using Azure AD Connect
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: billmath
ms.openlocfilehash: 787148f1868ea751adb15f052e835f898bcc5414
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540937"
---
# <a name="azure-ad-connect-enabling-device-writeback"></a><span data-ttu-id="7c5c5-103">Azure AD Connect: Enabling device writeback</span><span class="sxs-lookup"><span data-stu-id="7c5c5-103">Azure AD Connect: Enabling device writeback</span></span>
> [!NOTE]
> <span data-ttu-id="7c5c5-104">A subscription to Azure AD Premium is required for device writeback.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-104">A subscription to Azure AD Premium is required for device writeback.</span></span>
> 
> 

<span data-ttu-id="7c5c5-105">The following documentation provides information on how to enable the device writeback feature in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-105">The following documentation provides information on how to enable the device writeback feature in Azure AD Connect.</span></span> <span data-ttu-id="7c5c5-106">Device Writeback is used in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-106">Device Writeback is used in the following scenarios:</span></span>

* <span data-ttu-id="7c5c5-107">Enable conditional access based on devices to ADFS (2012 R2 or higher) protected applications (relying party trusts).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-107">Enable conditional access based on devices to ADFS (2012 R2 or higher) protected applications (relying party trusts).</span></span>

<span data-ttu-id="7c5c5-108">This provides additional security and assurance that access to applications is granted only to trusted devices.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-108">This provides additional security and assurance that access to applications is granted only to trusted devices.</span></span> <span data-ttu-id="7c5c5-109">For more information on conditional access, see [Managing Risk with Conditional Access](../active-directory-conditional-access.md) and [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](https://msdn.microsoft.com/library/azure/dn788908.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-109">For more information on conditional access, see [Managing Risk with Conditional Access](../active-directory-conditional-access.md) and [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](https://msdn.microsoft.com/library/azure/dn788908.aspx).</span></span>

> [!IMPORTANT]
> <li><span data-ttu-id="7c5c5-110">Devices must be located in the same forest as the users.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-110">Devices must be located in the same forest as the users.</span></span> <span data-ttu-id="7c5c5-111">Since devices must be written back to a single forest, this feature does not currently support a deployment with multiple user forests.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-111">Since devices must be written back to a single forest, this feature does not currently support a deployment with multiple user forests.</span></span></li>
> <li><span data-ttu-id="7c5c5-112">Only one device registration configuration object can be added to the on-premises Active Directory forest.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-112">Only one device registration configuration object can be added to the on-premises Active Directory forest.</span></span> <span data-ttu-id="7c5c5-113">This feature is not compatible with a topology where the on-premises Active Directory is synchronized to multiple Azure AD directories.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-113">This feature is not compatible with a topology where the on-premises Active Directory is synchronized to multiple Azure AD directories.</span></span></li>> 

## <a name="part-1-install-azure-ad-connect"></a><span data-ttu-id="7c5c5-114">Part 1: Install Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="7c5c5-114">Part 1: Install Azure AD Connect</span></span>
1. <span data-ttu-id="7c5c5-115">Install Azure AD Connect using Custom or Express settings.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-115">Install Azure AD Connect using Custom or Express settings.</span></span> <span data-ttu-id="7c5c5-116">Microsoft recommends to start with all users and groups successfully synchronized before you enable device writeback.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-116">Microsoft recommends to start with all users and groups successfully synchronized before you enable device writeback.</span></span>

## <a name="part-2-prepare-active-directory"></a><span data-ttu-id="7c5c5-117">Part 2: Prepare Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c5c5-117">Part 2: Prepare Active Directory</span></span>
<span data-ttu-id="7c5c5-118">Use the following steps to prepare for using device writeback.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-118">Use the following steps to prepare for using device writeback.</span></span>

1. <span data-ttu-id="7c5c5-119">From the machine where Azure AD Connect is installed, launch PowerShell in elevated mode.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-119">From the machine where Azure AD Connect is installed, launch PowerShell in elevated mode.</span></span>
2. <span data-ttu-id="7c5c5-120">If the Active Directory PowerShell module is NOT installed, install it using the following command:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-120">If the Active Directory PowerShell module is NOT installed, install it using the following command:</span></span>
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. <span data-ttu-id="7c5c5-121">If the Azure Active Directory PowerShell module is NOT installed, then download and install it from [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-121">If the Azure Active Directory PowerShell module is NOT installed, then download and install it from [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span> <span data-ttu-id="7c5c5-122">This component has a dependency on the sign-in assistant, which is installed with Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-122">This component has a dependency on the sign-in assistant, which is installed with Azure AD Connect.</span></span>
4. <span data-ttu-id="7c5c5-123">With enterprise admin credentials, run the following commands and then exit PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-123">With enterprise admin credentials, run the following commands and then exit PowerShell.</span></span>
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

<span data-ttu-id="7c5c5-124">Enterprise admin credentials are required since changes to the configuration namespace are needed.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-124">Enterprise admin credentials are required since changes to the configuration namespace are needed.</span></span> <span data-ttu-id="7c5c5-125">A domain admin will not have enough permissions.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-125">A domain admin will not have enough permissions.</span></span>

![Powershell for enabling device writeback](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/powershell.png)

<span data-ttu-id="7c5c5-127">Description:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-127">Description:</span></span>

* <span data-ttu-id="7c5c5-128">If they do not exist already, creates and configures new containers and objects under CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].</span><span class="sxs-lookup"><span data-stu-id="7c5c5-128">If they do not exist already, creates and configures new containers and objects under CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].</span></span>
* <span data-ttu-id="7c5c5-129">If they do not exist already, creates and configures new containers and objects under CN=RegisteredDevices,[domain-dn].</span><span class="sxs-lookup"><span data-stu-id="7c5c5-129">If they do not exist already, creates and configures new containers and objects under CN=RegisteredDevices,[domain-dn].</span></span> <span data-ttu-id="7c5c5-130">Device objects will be created in this container.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-130">Device objects will be created in this container.</span></span>
* <span data-ttu-id="7c5c5-131">Sets necessary permissions on the Azure AD Connector account, to manage devices on your Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-131">Sets necessary permissions on the Azure AD Connector account, to manage devices on your Active Directory.</span></span>
* <span data-ttu-id="7c5c5-132">Only needs to run on one forest, even if Azure AD Connect is being installed on multiple forests.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-132">Only needs to run on one forest, even if Azure AD Connect is being installed on multiple forests.</span></span>

<span data-ttu-id="7c5c5-133">Parameters:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-133">Parameters:</span></span>

* <span data-ttu-id="7c5c5-134">DomainName: Active Directory Domain where device objects will be created.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-134">DomainName: Active Directory Domain where device objects will be created.</span></span> <span data-ttu-id="7c5c5-135">Note: All devices for a given Active Directory forest will be created in a single domain.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-135">Note: All devices for a given Active Directory forest will be created in a single domain.</span></span>
* <span data-ttu-id="7c5c5-136">AdConnectorAccount: Active Directory account that will be used by Azure AD Connect to manage objects in the directory.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-136">AdConnectorAccount: Active Directory account that will be used by Azure AD Connect to manage objects in the directory.</span></span> <span data-ttu-id="7c5c5-137">This is the account used by Azure AD Connect sync to connect to AD.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-137">This is the account used by Azure AD Connect sync to connect to AD.</span></span> <span data-ttu-id="7c5c5-138">If you installed using express settings, it is the account prefixed with MSOL_.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-138">If you installed using express settings, it is the account prefixed with MSOL_.</span></span>

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a><span data-ttu-id="7c5c5-139">Part 3: Enable device writeback in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="7c5c5-139">Part 3: Enable device writeback in Azure AD Connect</span></span>
<span data-ttu-id="7c5c5-140">Use the following procedure to enable device writeback in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-140">Use the following procedure to enable device writeback in Azure AD Connect.</span></span>

1. <span data-ttu-id="7c5c5-141">Run the installation wizard again.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-141">Run the installation wizard again.</span></span> <span data-ttu-id="7c5c5-142">Select **customize synchronization options** from the Additional Tasks page and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-142">Select **customize synchronization options** from the Additional Tasks page and click **Next**.</span></span>
   <span data-ttu-id="7c5c5-143">![Custom Install customize synchronization options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span><span class="sxs-lookup"><span data-stu-id="7c5c5-143">![Custom Install customize synchronization options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)</span></span>
2. <span data-ttu-id="7c5c5-144">In the Optional Features page, device writeback will no longer be grayed out. Please note that if the Azure AD Connect prep steps are not completed device writeback will be grayed out in the Optional features page.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-144">In the Optional Features page, device writeback will no longer be grayed out. Please note that if the Azure AD Connect prep steps are not completed device writeback will be grayed out in the Optional features page.</span></span> <span data-ttu-id="7c5c5-145">Check the box for device writeback and click **next**.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-145">Check the box for device writeback and click **next**.</span></span> <span data-ttu-id="7c5c5-146">If the checkbox is still disabled, see the [troubleshooting section](#the-writeback-checkbox-is-still-disabled).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-146">If the checkbox is still disabled, see the [troubleshooting section](#the-writeback-checkbox-is-still-disabled).</span></span>
   <span data-ttu-id="7c5c5-147">![Custom install Device Writeback optional features](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span><span class="sxs-lookup"><span data-stu-id="7c5c5-147">![Custom install Device Writeback optional features](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)</span></span>
3. <span data-ttu-id="7c5c5-148">On the writeback page, you will see the supplied domain as the default Device writeback forest.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-148">On the writeback page, you will see the supplied domain as the default Device writeback forest.</span></span>
   <span data-ttu-id="7c5c5-149">![Custom Install device writeback target forest](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span><span class="sxs-lookup"><span data-stu-id="7c5c5-149">![Custom Install device writeback target forest](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)</span></span>
4. <span data-ttu-id="7c5c5-150">Complete the installation of the Wizard with no additional configuration changes.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-150">Complete the installation of the Wizard with no additional configuration changes.</span></span> <span data-ttu-id="7c5c5-151">If needed, refer to [Custom installation of Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)</span><span class="sxs-lookup"><span data-stu-id="7c5c5-151">If needed, refer to [Custom installation of Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)</span></span>

## <a name="enable-conditional-access"></a><span data-ttu-id="7c5c5-152">Enable conditional access</span><span class="sxs-lookup"><span data-stu-id="7c5c5-152">Enable conditional access</span></span>
<span data-ttu-id="7c5c5-153">Detailed instructions to enable this scenario are available within [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](https://msdn.microsoft.com/library/azure/dn788908.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-153">Detailed instructions to enable this scenario are available within [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](https://msdn.microsoft.com/library/azure/dn788908.aspx).</span></span>

## <a name="verify-devices-are-synchronized-to-active-directory"></a><span data-ttu-id="7c5c5-154">Verify Devices are synchronized to Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c5c5-154">Verify Devices are synchronized to Active Directory</span></span>
<span data-ttu-id="7c5c5-155">Device writeback should now be working properly.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-155">Device writeback should now be working properly.</span></span> <span data-ttu-id="7c5c5-156">Be aware that it can take up to 3 hours for device objects to be written-back to AD.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-156">Be aware that it can take up to 3 hours for device objects to be written-back to AD.</span></span>  <span data-ttu-id="7c5c5-157">To verify that your devices are being synced properly, do the following after the sync rules complete:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-157">To verify that your devices are being synced properly, do the following after the sync rules complete:</span></span>

1. <span data-ttu-id="7c5c5-158">Launch Active Directory Administrative Center.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-158">Launch Active Directory Administrative Center.</span></span>
2. <span data-ttu-id="7c5c5-159">Expand RegisteredDevices, within the Domain that is being federated.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-159">Expand RegisteredDevices, within the Domain that is being federated.</span></span>
   <span data-ttu-id="7c5c5-160">![Active Directory Admin Center Registered Devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span><span class="sxs-lookup"><span data-stu-id="7c5c5-160">![Active Directory Admin Center Registered Devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)</span></span>
3. <span data-ttu-id="7c5c5-161">Current registered devices will be listed there.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-161">Current registered devices will be listed there.</span></span>
   <span data-ttu-id="7c5c5-162">![Active Directory Admin Center Registered Devices List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span><span class="sxs-lookup"><span data-stu-id="7c5c5-162">![Active Directory Admin Center Registered Devices List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7c5c5-163">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="7c5c5-163">Troubleshooting</span></span>
### <a name="the-writeback-checkbox-is-still-disabled"></a><span data-ttu-id="7c5c5-164">The writeback checkbox is still disabled</span><span class="sxs-lookup"><span data-stu-id="7c5c5-164">The writeback checkbox is still disabled</span></span>
<span data-ttu-id="7c5c5-165">If the checkbox for device writeback is not enabled even though you have followed the steps above, the following steps will guide you through what the installation wizard is verifying before the box is enabled.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-165">If the checkbox for device writeback is not enabled even though you have followed the steps above, the following steps will guide you through what the installation wizard is verifying before the box is enabled.</span></span>

<span data-ttu-id="7c5c5-166">First things first:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-166">First things first:</span></span>

* <span data-ttu-id="7c5c5-167">Make sure at least one forest has Windows Server 2012R2.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-167">Make sure at least one forest has Windows Server 2012R2.</span></span> <span data-ttu-id="7c5c5-168">The device object type must be present.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-168">The device object type must be present.</span></span>
* <span data-ttu-id="7c5c5-169">If the installation wizard is already running, then any changes will not be detected.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-169">If the installation wizard is already running, then any changes will not be detected.</span></span> <span data-ttu-id="7c5c5-170">In this case, complete the installation wizard and run it again.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-170">In this case, complete the installation wizard and run it again.</span></span>
* <span data-ttu-id="7c5c5-171">Make sure the account you provide in the initialization script is actually the correct user used by the Active Directory Connector.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-171">Make sure the account you provide in the initialization script is actually the correct user used by the Active Directory Connector.</span></span> <span data-ttu-id="7c5c5-172">To verify this, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-172">To verify this, follow these steps:</span></span>
  * <span data-ttu-id="7c5c5-173">From the start menu, open **Synchronization Service**.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-173">From the start menu, open **Synchronization Service**.</span></span>
  * <span data-ttu-id="7c5c5-174">Open the **Connectors** tab.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-174">Open the **Connectors** tab.</span></span>
  * <span data-ttu-id="7c5c5-175">Find the Connector with type Active Directory Domain Services and select it.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-175">Find the Connector with type Active Directory Domain Services and select it.</span></span>
  * <span data-ttu-id="7c5c5-176">Under **Actions**, select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-176">Under **Actions**, select **Properties**.</span></span>
  * <span data-ttu-id="7c5c5-177">Go to **Connect to Active Directory Forest**.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-177">Go to **Connect to Active Directory Forest**.</span></span> <span data-ttu-id="7c5c5-178">Verify that the domain and user name specified on this screen match the account provided to the script.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-178">Verify that the domain and user name specified on this screen match the account provided to the script.</span></span>
    <span data-ttu-id="7c5c5-179">![Connector account in Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span><span class="sxs-lookup"><span data-stu-id="7c5c5-179">![Connector account in Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)</span></span>

<span data-ttu-id="7c5c5-180">Verify configuration in Active Directory:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-180">Verify configuration in Active Directory:</span></span>

* <span data-ttu-id="7c5c5-181">Verify that the Device Registration Service is located in the location below (CN=DeviceRegistrationService,CN=Device Registration Services,CN=Device Registration Configuration,CN=Services,CN=Configuration) under configuration naming context.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-181">Verify that the Device Registration Service is located in the location below (CN=DeviceRegistrationService,CN=Device Registration Services,CN=Device Registration Configuration,CN=Services,CN=Configuration) under configuration naming context.</span></span>

![Troubleshoot, DeviceRegistrationService in configuration namespace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* <span data-ttu-id="7c5c5-183">Verify there is only one configuration object by searching the configuration namespace.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-183">Verify there is only one configuration object by searching the configuration namespace.</span></span> <span data-ttu-id="7c5c5-184">If there is more than one, delete the duplicate.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-184">If there is more than one, delete the duplicate.</span></span>

![Troubleshoot, search for the duplicate objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* <span data-ttu-id="7c5c5-186">On the Device Registration Service object, make sure the attribute msDS-DeviceLocation is present and has a value.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-186">On the Device Registration Service object, make sure the attribute msDS-DeviceLocation is present and has a value.</span></span> <span data-ttu-id="7c5c5-187">Lookup this location and make sure it is present with the objectType msDS-DeviceContainer.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-187">Lookup this location and make sure it is present with the objectType msDS-DeviceContainer.</span></span>

![Troubleshoot, msDS-DeviceLocation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Troubleshoot, RegisteredDevices object class](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* <span data-ttu-id="7c5c5-190">Verify the account used by the Active Directory Connector has required permissions on the Registered Devices container found by the previous step.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-190">Verify the account used by the Active Directory Connector has required permissions on the Registered Devices container found by the previous step.</span></span> <span data-ttu-id="7c5c5-191">This is the expected permissions on this container:</span><span class="sxs-lookup"><span data-stu-id="7c5c5-191">This is the expected permissions on this container:</span></span>

![Troubleshoot, verify permissions on container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* <span data-ttu-id="7c5c5-193">Verify the Active Directory account has permissions on the CN=Device Registration Configuration,CN=Services,CN=Configuration object.</span><span class="sxs-lookup"><span data-stu-id="7c5c5-193">Verify the Active Directory account has permissions on the CN=Device Registration Configuration,CN=Services,CN=Configuration object.</span></span>

![Troubleshoot, verify permissions on Device Registration Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a><span data-ttu-id="7c5c5-195">Additional Information</span><span class="sxs-lookup"><span data-stu-id="7c5c5-195">Additional Information</span></span>
* [<span data-ttu-id="7c5c5-196">Managing Risk With Conditional Access</span><span class="sxs-lookup"><span data-stu-id="7c5c5-196">Managing Risk With Conditional Access</span></span>](../active-directory-conditional-access.md)
* [<span data-ttu-id="7c5c5-197">Setting up On-premises Conditional Access using Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="7c5c5-197">Setting up On-premises Conditional Access using Azure Active Directory Device Registration</span></span>](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a><span data-ttu-id="7c5c5-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c5c5-198">Next steps</span></span>
<span data-ttu-id="7c5c5-199">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="7c5c5-199">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>














