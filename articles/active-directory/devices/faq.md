---
title: Azure Active Directory device management FAQ | Microsoft Docs
description: Azure Active Directory device management FAQ.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 72035c2f13f5a2a749feabbb26db5500f6c3fc0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967703"
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="34c0d-103">Azure Active Directory device management FAQ</span><span class="sxs-lookup"><span data-stu-id="34c0d-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="34c0d-104">**Q: Can I register Android or iOS BYOD devices?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-104">**Q: Can I register Android or iOS BYOD devices?**</span></span>

<span data-ttu-id="34c0d-105">**A:** Yes, but only with Azure device registration service and for hybrid customers.</span><span class="sxs-lookup"><span data-stu-id="34c0d-105">**A:** Yes, but only with Azure device registration service and for hybrid customers.</span></span> <span data-ttu-id="34c0d-106">It is not supported with on-premises device registration service in AD FS.</span><span class="sxs-lookup"><span data-stu-id="34c0d-106">It is not supported with on-premises device registration service in AD FS.</span></span>

<span data-ttu-id="34c0d-107">**Q: How can I register a macOS device?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-107">**Q: How can I register a macOS device?**</span></span>

<span data-ttu-id="34c0d-108">**A:** To register macOS device:</span><span class="sxs-lookup"><span data-stu-id="34c0d-108">**A:** To register macOS device:</span></span>

1.  [<span data-ttu-id="34c0d-109">Create a compliance policy</span><span class="sxs-lookup"><span data-stu-id="34c0d-109">Create a compliance policy</span></span>](https://docs.microsoft.com/intune/compliance-policy-create-mac-os)
2.  [<span data-ttu-id="34c0d-110">Define a conditional access policy for macOS devices</span><span class="sxs-lookup"><span data-stu-id="34c0d-110">Define a conditional access policy for macOS devices</span></span>](../active-directory-conditional-access-azure-portal.md) 

<span data-ttu-id="34c0d-111">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="34c0d-111">**Remarks:**</span></span>

- <span data-ttu-id="34c0d-112">The users that are included in your conditional access policy need a [supported version of Office for macOS](../conditional-access/technical-reference.md#client-apps-condition) to access resources.</span><span class="sxs-lookup"><span data-stu-id="34c0d-112">The users that are included in your conditional access policy need a [supported version of Office for macOS](../conditional-access/technical-reference.md#client-apps-condition) to access resources.</span></span> 

- <span data-ttu-id="34c0d-113">During the first access attempt, your users are prompted to enroll the device using the company portal.</span><span class="sxs-lookup"><span data-stu-id="34c0d-113">During the first access attempt, your users are prompted to enroll the device using the company portal.</span></span>

---

<span data-ttu-id="34c0d-114">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-114">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="34c0d-115">**A:** Windows 10 devices that are hybrid Azure AD joined do not show up under the USER devices.</span><span class="sxs-lookup"><span data-stu-id="34c0d-115">**A:** Windows 10 devices that are hybrid Azure AD joined do not show up under the USER devices.</span></span>
<span data-ttu-id="34c0d-116">You need to use All devices view in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="34c0d-116">You need to use All devices view in Azure portal.</span></span> <span data-ttu-id="34c0d-117">You can also use PowerShell [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34c0d-117">You can also use PowerShell [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

<span data-ttu-id="34c0d-118">Only the following devices are listed under the USER devices:</span><span class="sxs-lookup"><span data-stu-id="34c0d-118">Only the following devices are listed under the USER devices:</span></span>

- <span data-ttu-id="34c0d-119">All personal devices that are not hybrid Azure AD joined.</span><span class="sxs-lookup"><span data-stu-id="34c0d-119">All personal devices that are not hybrid Azure AD joined.</span></span> 
- <span data-ttu-id="34c0d-120">All non-Windows 10 / Windows Server 2016 devices.</span><span class="sxs-lookup"><span data-stu-id="34c0d-120">All non-Windows 10 / Windows Server 2016 devices.</span></span>
- <span data-ttu-id="34c0d-121">All non-Windows devices</span><span class="sxs-lookup"><span data-stu-id="34c0d-121">All non-Windows devices</span></span> 

--- 

<span data-ttu-id="34c0d-122">**Q: How do I know what the device registration state of the client is?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-122">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="34c0d-123">**A:** You can use the Azure portal, go to All devices and search for the device using device ID.</span><span class="sxs-lookup"><span data-stu-id="34c0d-123">**A:** You can use the Azure portal, go to All devices and search for the device using device ID.</span></span> <span data-ttu-id="34c0d-124">Check the value under the join type column.</span><span class="sxs-lookup"><span data-stu-id="34c0d-124">Check the value under the join type column.</span></span>

<span data-ttu-id="34c0d-125">If you want to check the local device registration state from a registered device:</span><span class="sxs-lookup"><span data-stu-id="34c0d-125">If you want to check the local device registration state from a registered device:</span></span>

- <span data-ttu-id="34c0d-126">For Windows 10 and Windows Server 2016 or later devices, run dsregcmd.exe /status.</span><span class="sxs-lookup"><span data-stu-id="34c0d-126">For Windows 10 and Windows Server 2016 or later devices, run dsregcmd.exe /status.</span></span>
- <span data-ttu-id="34c0d-127">For down-level OS versions, run "%programFiles%\Microsoft Workplace Join\autoworkplace.exe"</span><span class="sxs-lookup"><span data-stu-id="34c0d-127">For down-level OS versions, run "%programFiles%\Microsoft Workplace Join\autoworkplace.exe"</span></span>

---

<span data-ttu-id="34c0d-128">**Q: I have deleted in the Azure portal or using Windows PowerShell, but the local state on the device says that it is still registered?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-128">**Q: I have deleted in the Azure portal or using Windows PowerShell, but the local state on the device says that it is still registered?**</span></span>

<span data-ttu-id="34c0d-129">**A:** This is by design.</span><span class="sxs-lookup"><span data-stu-id="34c0d-129">**A:** This is by design.</span></span> <span data-ttu-id="34c0d-130">The device will not have access to resources in the cloud.</span><span class="sxs-lookup"><span data-stu-id="34c0d-130">The device will not have access to resources in the cloud.</span></span> 

<span data-ttu-id="34c0d-131">If you want to re-register again, a manual action must be to be taken on the device.</span><span class="sxs-lookup"><span data-stu-id="34c0d-131">If you want to re-register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="34c0d-132">To clear the join state from Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span><span class="sxs-lookup"><span data-stu-id="34c0d-132">To clear the join state from Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="34c0d-133">Open the command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="34c0d-133">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="34c0d-134">Type `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="34c0d-134">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="34c0d-135">Sign out and sign in to trigger the scheduled task that registers the device with Azure AD again.</span><span class="sxs-lookup"><span data-stu-id="34c0d-135">Sign out and sign in to trigger the scheduled task that registers the device with Azure AD again.</span></span> 

<span data-ttu-id="34c0d-136">For down-level Windows OS versions that are on-premises AD domain-joined:</span><span class="sxs-lookup"><span data-stu-id="34c0d-136">For down-level Windows OS versions that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="34c0d-137">Open the command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="34c0d-137">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="34c0d-138">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="34c0d-138">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="34c0d-139">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="34c0d-139">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---
<span data-ttu-id="34c0d-140">**Q: How do I unjoin an Azure AD Joined device locally on the device?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-140">**Q: How do I unjoin an Azure AD Joined device locally on the device?**</span></span>

<span data-ttu-id="34c0d-141">**A:**</span><span class="sxs-lookup"><span data-stu-id="34c0d-141">**A:**</span></span> 
- <span data-ttu-id="34c0d-142">For hybrid Azure AD Joined devices, make sure to turn off auto registration so that the scheduled task does not register the device again.</span><span class="sxs-lookup"><span data-stu-id="34c0d-142">For hybrid Azure AD Joined devices, make sure to turn off auto registration so that the scheduled task does not register the device again.</span></span> <span data-ttu-id="34c0d-143">Next, open command prompt as an administrator and type `dsregcmd.exe /debug /leave`.</span><span class="sxs-lookup"><span data-stu-id="34c0d-143">Next, open command prompt as an administrator and type `dsregcmd.exe /debug /leave`.</span></span> <span data-ttu-id="34c0d-144">Alternatively, this command can be run as a script across multiple devices to unjoin in bulk.</span><span class="sxs-lookup"><span data-stu-id="34c0d-144">Alternatively, this command can be run as a script across multiple devices to unjoin in bulk.</span></span>

- <span data-ttu-id="34c0d-145">For pure Azure AD Joined devices, make sure you have an offline local administrator account or create one, as you won't be able to sign in with any Azure AD user credentials.</span><span class="sxs-lookup"><span data-stu-id="34c0d-145">For pure Azure AD Joined devices, make sure you have an offline local administrator account or create one, as you won't be able to sign in with any Azure AD user credentials.</span></span> <span data-ttu-id="34c0d-146">Next, go to **Settings** > **Accounts** > **Access Work or School**.</span><span class="sxs-lookup"><span data-stu-id="34c0d-146">Next, go to **Settings** > **Accounts** > **Access Work or School**.</span></span> <span data-ttu-id="34c0d-147">Select your account and click on **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="34c0d-147">Select your account and click on **Disconnect**.</span></span> <span data-ttu-id="34c0d-148">Follow the prompts and provide the local administrator credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="34c0d-148">Follow the prompts and provide the local administrator credentials when prompted.</span></span> <span data-ttu-id="34c0d-149">Reboot the device to complete the unjoin process.</span><span class="sxs-lookup"><span data-stu-id="34c0d-149">Reboot the device to complete the unjoin process.</span></span>

---

<span data-ttu-id="34c0d-150">**Q: My users cannot search printers from Azure AD Joined devices. How can I enable printing from Azure AD Joined devices ?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-150">**Q: My users cannot search printers from Azure AD Joined devices. How can I enable printing from Azure AD Joined devices ?**</span></span>

<span data-ttu-id="34c0d-151">**A:** For deploying printers for Azure AD Joined devices, see [Hybrid cloud print](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-deploy).</span><span class="sxs-lookup"><span data-stu-id="34c0d-151">**A:** For deploying printers for Azure AD Joined devices, see [Hybrid cloud print](https://docs.microsoft.com/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-deploy).</span></span> <span data-ttu-id="34c0d-152">You will need an on-premises Windows Server to deploy hybrid cloud print.</span><span class="sxs-lookup"><span data-stu-id="34c0d-152">You will need an on-premises Windows Server to deploy hybrid cloud print.</span></span> <span data-ttu-id="34c0d-153">Currently, cloud-based print service is not available.</span><span class="sxs-lookup"><span data-stu-id="34c0d-153">Currently, cloud-based print service is not available.</span></span> 

---

<span data-ttu-id="34c0d-154">**Q: How do I connect to a remote Azure AD joined device?**
**A:** Refer to the article https://docs.microsoft.com/windows/client-management/connect-to-remote-aadj-pc for details.</span><span class="sxs-lookup"><span data-stu-id="34c0d-154">**Q: How do I connect to a remote Azure AD joined device?**
**A:** Refer to the article https://docs.microsoft.com/windows/client-management/connect-to-remote-aadj-pc for details.</span></span>

---

<span data-ttu-id="34c0d-155">**Q: Why do I see duplicate device entries in Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-155">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="34c0d-156">**A:**</span><span class="sxs-lookup"><span data-stu-id="34c0d-156">**A:**</span></span>

-   <span data-ttu-id="34c0d-157">For Windows 10 and Windows Server 2016, if there are repeated attempts to unjoin and rejoin the same device, there might be duplicate entries.</span><span class="sxs-lookup"><span data-stu-id="34c0d-157">For Windows 10 and Windows Server 2016, if there are repeated attempts to unjoin and rejoin the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="34c0d-158">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span><span class="sxs-lookup"><span data-stu-id="34c0d-158">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="34c0d-159">For down-level Windows OS versions that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span><span class="sxs-lookup"><span data-stu-id="34c0d-159">For down-level Windows OS versions that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="34c0d-160">An Azure AD joined machine that has been wiped, reinstalled, and rejoined with the same name, will show up as another record with the same device name.</span><span class="sxs-lookup"><span data-stu-id="34c0d-160">An Azure AD joined machine that has been wiped, reinstalled, and rejoined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="34c0d-161">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-161">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="34c0d-162">**A:** It can take up to an hour for a revoke to be applied.</span><span class="sxs-lookup"><span data-stu-id="34c0d-162">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="34c0d-163">For enrolled devices, we recommend wiping the device to ensure that users cannot access the resources.</span><span class="sxs-lookup"><span data-stu-id="34c0d-163">For enrolled devices, we recommend wiping the device to ensure that users cannot access the resources.</span></span> <span data-ttu-id="34c0d-164">For more information, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="34c0d-164">For more information, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="34c0d-165">**Q: Why do my users see “You can’t get there from here”?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-165">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="34c0d-166">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span><span class="sxs-lookup"><span data-stu-id="34c0d-166">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="34c0d-167">Please evaluate the conditional access policy rules and ensure that the device is able to meet the criteria to avoid this message.</span><span class="sxs-lookup"><span data-stu-id="34c0d-167">Please evaluate the conditional access policy rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---

<span data-ttu-id="34c0d-168">**Q: Why do some of my users do not get MFA prompts on Azure AD joined devices?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-168">**Q: Why do some of my users do not get MFA prompts on Azure AD joined devices?**</span></span>

<span data-ttu-id="34c0d-169">**A:** If user joins or registers a device with Azure AD using multi-factor auth, the device itself will become a trusted second factor for that particular user.</span><span class="sxs-lookup"><span data-stu-id="34c0d-169">**A:** If user joins or registers a device with Azure AD using multi-factor auth, the device itself will become a trusted second factor for that particular user.</span></span> <span data-ttu-id="34c0d-170">Subsequently, whenever the same user signs in to the device and accesses an application, Azure AD considers the device as a second factor and enables that user to seamlessly access their applications without additional MFA prompts.</span><span class="sxs-lookup"><span data-stu-id="34c0d-170">Subsequently, whenever the same user signs in to the device and accesses an application, Azure AD considers the device as a second factor and enables that user to seamlessly access their applications without additional MFA prompts.</span></span> <span data-ttu-id="34c0d-171">This behavior is not applicable to any other user signing into that device, so all other users accessing that device would still be prompted with an MFA challenge before accessing applications that require MFA.</span><span class="sxs-lookup"><span data-stu-id="34c0d-171">This behavior is not applicable to any other user signing into that device, so all other users accessing that device would still be prompted with an MFA challenge before accessing applications that require MFA.</span></span>

---

<span data-ttu-id="34c0d-172">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the device. Am I setup correctly for using conditional access?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-172">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the device. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="34c0d-173">**A:** The device join state, reflected by deviceID, must match with that on Azure AD and meet any evaluation criteria for conditional access.</span><span class="sxs-lookup"><span data-stu-id="34c0d-173">**A:** The device join state, reflected by deviceID, must match with that on Azure AD and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="34c0d-174">For more information, see [Require managed devices for cloud app access with conditional access](../conditional-access/require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="34c0d-174">For more information, see [Require managed devices for cloud app access with conditional access](../conditional-access/require-managed-devices.md).</span></span>

---

<span data-ttu-id="34c0d-175">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-175">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="34c0d-176">**A:** Common reasons for this scenario are:</span><span class="sxs-lookup"><span data-stu-id="34c0d-176">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="34c0d-177">Your user credentials are no longer valid.</span><span class="sxs-lookup"><span data-stu-id="34c0d-177">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="34c0d-178">Your computer is unable to communicate with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="34c0d-178">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="34c0d-179">Check for any network connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="34c0d-179">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="34c0d-180">Federated logins requires your federation server to support a WS-Trust active endpoint.</span><span class="sxs-lookup"><span data-stu-id="34c0d-180">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

- <span data-ttu-id="34c0d-181">You have enabled Pass through Authentication and the user has a temporary password that needs to be changed on logon.</span><span class="sxs-lookup"><span data-stu-id="34c0d-181">You have enabled Pass through Authentication and the user has a temporary password that needs to be changed on logon.</span></span>

---

<span data-ttu-id="34c0d-182">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do Azure AD join my PC?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-182">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do Azure AD join my PC?**</span></span>

<span data-ttu-id="34c0d-183">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span><span class="sxs-lookup"><span data-stu-id="34c0d-183">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="34c0d-184">Please make sure that the user attempting to do Azure AD join has correct Intune license assigned.</span><span class="sxs-lookup"><span data-stu-id="34c0d-184">Please make sure that the user attempting to do Azure AD join has correct Intune license assigned.</span></span> <span data-ttu-id="34c0d-185">For more information, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="34c0d-185">For more information, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="34c0d-186">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-186">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="34c0d-187">**A:** A likely cause is that the user is logged in to the device using the local built-in administrator account.</span><span class="sxs-lookup"><span data-stu-id="34c0d-187">**A:** A likely cause is that the user is logged in to the device using the local built-in administrator account.</span></span> <span data-ttu-id="34c0d-188">Please create a different local account before using Azure Active Directory Join to complete the setup.</span><span class="sxs-lookup"><span data-stu-id="34c0d-188">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 


---

<span data-ttu-id="34c0d-189">**Q: Where can I find troubleshooting information about the automatic device registration?**</span><span class="sxs-lookup"><span data-stu-id="34c0d-189">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="34c0d-190">**A:** For troubleshooting information, see:</span><span class="sxs-lookup"><span data-stu-id="34c0d-190">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="34c0d-191">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="34c0d-191">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](troubleshoot-hybrid-join-windows-current.md)

- [<span data-ttu-id="34c0d-192">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span><span class="sxs-lookup"><span data-stu-id="34c0d-192">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](troubleshoot-hybrid-join-windows-legacy.md)
 

---

