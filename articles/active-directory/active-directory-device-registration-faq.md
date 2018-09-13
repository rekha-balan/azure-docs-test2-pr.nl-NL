---
title: Azure Active Directory automatic device registration FAQ | Microsoft Docs
description: Automatic device registration with Azure Active Directory FAQ.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: markvi
ms.openlocfilehash: 3fbb35a059b77f5e918f54e0fefe472893d8a974
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540931"
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="2c4f8-103">Azure Active Directory automatic device registration FAQ</span><span class="sxs-lookup"><span data-stu-id="2c4f8-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="2c4f8-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="2c4f8-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="2c4f8-106">You need to use PowerShell to see all devices.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="2c4f8-107">Only the following devices are listed under the USER info:</span><span class="sxs-lookup"><span data-stu-id="2c4f8-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="2c4f8-108">All personal devices that are not enterprise joined</span><span class="sxs-lookup"><span data-stu-id="2c4f8-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="2c4f8-109">All non-Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2c4f8-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="2c4f8-110">All non-Windows devices</span><span class="sxs-lookup"><span data-stu-id="2c4f8-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="2c4f8-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="2c4f8-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="2c4f8-113">You can use Azure PowerShell to find all devices.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="2c4f8-114">For more details, see the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-114">For more details, see the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet.</span></span>

--- 

<span data-ttu-id="2c4f8-115">**Q: How do I know what the device registration state of the client is?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="2c4f8-116">**A:** The device registration state depends on:</span><span class="sxs-lookup"><span data-stu-id="2c4f8-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="2c4f8-117">What the device is</span><span class="sxs-lookup"><span data-stu-id="2c4f8-117">What the device is</span></span>
- <span data-ttu-id="2c4f8-118">How it was registered</span><span class="sxs-lookup"><span data-stu-id="2c4f8-118">How it was registered</span></span> 
- <span data-ttu-id="2c4f8-119">Any details related to it.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="2c4f8-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="2c4f8-121">**A:** This is by design.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-121">**A:** This is by design.</span></span> <span data-ttu-id="2c4f8-122">The device will not have access to resources in the cloud.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="2c4f8-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="2c4f8-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span><span class="sxs-lookup"><span data-stu-id="2c4f8-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="2c4f8-125">Open the command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="2c4f8-126">Type `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="2c4f8-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="2c4f8-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="2c4f8-128">For other Windows platforms that are on-premises AD domain-joined:</span><span class="sxs-lookup"><span data-stu-id="2c4f8-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="2c4f8-129">Open the command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="2c4f8-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="2c4f8-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="2c4f8-132">**Q: Why do I see duplicate device entries in Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="2c4f8-133">**A:**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-133">**A:**</span></span>

-   <span data-ttu-id="2c4f8-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="2c4f8-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="2c4f8-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="2c4f8-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="2c4f8-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="2c4f8-139">**A:** It can take up to an hour for a revoke to be applied.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="2c4f8-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="2c4f8-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="2c4f8-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="2c4f8-142">**Q: Why do my users see “You can’t get there from here”?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="2c4f8-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="2c4f8-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="2c4f8-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="2c4f8-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="2c4f8-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="2c4f8-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="2c4f8-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="2c4f8-149">**A:** Common reasons for this scenario are:</span><span class="sxs-lookup"><span data-stu-id="2c4f8-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="2c4f8-150">Your user credentials are no longer valid.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="2c4f8-151">Your computer is unable to communicate with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="2c4f8-152">Check for any network connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="2c4f8-153">The Azure AD Join pre-requisites were not met.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="2c4f8-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c4f8-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="2c4f8-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="2c4f8-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="2c4f8-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="2c4f8-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="2c4f8-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="2c4f8-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="2c4f8-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="2c4f8-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span><span class="sxs-lookup"><span data-stu-id="2c4f8-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="2c4f8-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="2c4f8-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="2c4f8-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="2c4f8-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span><span class="sxs-lookup"><span data-stu-id="2c4f8-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="2c4f8-165">**A:** For troubleshooting information, see:</span><span class="sxs-lookup"><span data-stu-id="2c4f8-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="2c4f8-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2c4f8-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="2c4f8-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span><span class="sxs-lookup"><span data-stu-id="2c4f8-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

