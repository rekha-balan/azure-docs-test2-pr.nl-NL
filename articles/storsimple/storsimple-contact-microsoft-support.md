---
title: Log Support ticket for StorSimple 8000 series | Microsoft Docs
description: Learn how to create a support request and start a support session on your StorSimple device.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 09c9842c3ff1db0fcde67877a12bb86e2ea0343b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562970"
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="dcd64-103">Contact Microsoft Support for your StorSimple</span><span class="sxs-lookup"><span data-stu-id="dcd64-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="dcd64-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span><span class="sxs-lookup"><span data-stu-id="dcd64-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="dcd64-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="dcd64-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="dcd64-106">This article walks you through:</span><span class="sxs-lookup"><span data-stu-id="dcd64-106">This article walks you through:</span></span>

* <span data-ttu-id="dcd64-107">How to create a support request.</span><span class="sxs-lookup"><span data-stu-id="dcd64-107">How to create a support request.</span></span>
* <span data-ttu-id="dcd64-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="dcd64-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="dcd64-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span><span class="sxs-lookup"><span data-stu-id="dcd64-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="dcd64-110">Create a support request</span><span class="sxs-lookup"><span data-stu-id="dcd64-110">Create a support request</span></span>
<span data-ttu-id="dcd64-111">Perform the following steps to create a support request:</span><span class="sxs-lookup"><span data-stu-id="dcd64-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="dcd64-112">To create a support request</span><span class="sxs-lookup"><span data-stu-id="dcd64-112">To create a support request</span></span>
1. <span data-ttu-id="dcd64-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span><span class="sxs-lookup"><span data-stu-id="dcd64-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Contact MS Support via ManagementPortal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="dcd64-115">You will be redirected to the new Azure portal (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dcd64-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="dcd64-116">Click the **New support request** tile.</span><span class="sxs-lookup"><span data-stu-id="dcd64-116">Click the **New support request** tile.</span></span>
   
    ![Contact MS Support via new portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="dcd64-118">On the right side of the screen, the **New support request** pane appears.</span><span class="sxs-lookup"><span data-stu-id="dcd64-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![New support request pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="dcd64-120">In the **Basics** dialog box, complete the following:</span><span class="sxs-lookup"><span data-stu-id="dcd64-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="dcd64-121">From the **Issue type** drop-down list , select **Technical**.</span><span class="sxs-lookup"><span data-stu-id="dcd64-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="dcd64-122">Select a **Subscription** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="dcd64-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="dcd64-123">From the **Service** drop-down list, select **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="dcd64-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="dcd64-124">Select a **Support plan** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="dcd64-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="dcd64-125">You need a paid support plan to enable Technical Support.</span><span class="sxs-lookup"><span data-stu-id="dcd64-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="dcd64-126">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dcd64-126">Click **Next**.</span></span> <span data-ttu-id="dcd64-127">The **Problem** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="dcd64-127">The **Problem** dialog box appears.</span></span>
   
    ![New support request pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="dcd64-129">In the **Problem** dialog box, complete the following:</span><span class="sxs-lookup"><span data-stu-id="dcd64-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="dcd64-130">Select a **Severity** level from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="dcd64-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="dcd64-131">Select a **Problem type** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="dcd64-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="dcd64-132">Select a **Category** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="dcd64-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="dcd64-133">In the **Details** box, briefly describe your issue.</span><span class="sxs-lookup"><span data-stu-id="dcd64-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="dcd64-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span><span class="sxs-lookup"><span data-stu-id="dcd64-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="dcd64-135">Under **File upload**, click the folder icon to browse to your support package.</span><span class="sxs-lookup"><span data-stu-id="dcd64-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="dcd64-136">Select the **Share diagnostic information** check box.</span><span class="sxs-lookup"><span data-stu-id="dcd64-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="dcd64-137">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dcd64-137">Click **Next**.</span></span> <span data-ttu-id="dcd64-138">The **Contact information** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="dcd64-138">The **Contact information** dialog box appears.</span></span>
   
    ![New support request pane](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="dcd64-140">Enter your contact information and select a contact method (phone or email).</span><span class="sxs-lookup"><span data-stu-id="dcd64-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="dcd64-141">Select the **Save contact changes for future support requests** check box.</span><span class="sxs-lookup"><span data-stu-id="dcd64-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="dcd64-142">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dcd64-142">Click **Create**.</span></span>

<span data-ttu-id="dcd64-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span><span class="sxs-lookup"><span data-stu-id="dcd64-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="dcd64-144">Start a support session in Windows PowerShell for StorSimple</span><span class="sxs-lookup"><span data-stu-id="dcd64-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="dcd64-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span><span class="sxs-lookup"><span data-stu-id="dcd64-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="dcd64-146">Microsoft Support may need to use a support session to log on to your device.</span><span class="sxs-lookup"><span data-stu-id="dcd64-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="dcd64-147">Perform the following steps to start a support session:</span><span class="sxs-lookup"><span data-stu-id="dcd64-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="dcd64-148">To start a support session</span><span class="sxs-lookup"><span data-stu-id="dcd64-148">To start a support session</span></span>
1. <span data-ttu-id="dcd64-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span><span class="sxs-lookup"><span data-stu-id="dcd64-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="dcd64-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="dcd64-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="dcd64-151">In the session that opens, press the **Enter** key to get a command prompt.</span><span class="sxs-lookup"><span data-stu-id="dcd64-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="dcd64-152">In the serial console menu, select option 1, **Log in with full access**.</span><span class="sxs-lookup"><span data-stu-id="dcd64-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="dcd64-153">At the prompt, type the following password:</span><span class="sxs-lookup"><span data-stu-id="dcd64-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="dcd64-154">At the prompt, type the following command:</span><span class="sxs-lookup"><span data-stu-id="dcd64-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="dcd64-155">An encrypted string will be presented to you.</span><span class="sxs-lookup"><span data-stu-id="dcd64-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="dcd64-156">Copy this string into a text editor such as Notepad.</span><span class="sxs-lookup"><span data-stu-id="dcd64-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="dcd64-157">Save this string and send it in an email message to Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="dcd64-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="dcd64-158">You can disable support access by running `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="dcd64-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="dcd64-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span><span class="sxs-lookup"><span data-stu-id="dcd64-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="dcd64-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span><span class="sxs-lookup"><span data-stu-id="dcd64-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 






