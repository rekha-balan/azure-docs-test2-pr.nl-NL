---
title: 'Troubleshooting: Azure AD Password Management | Microsoft Docs'
description: Common troubleshooting steps for Azure AD Password Management, including reset, change, writeback, registration, and what information to include when looking for help.
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: femila
editor: curtand
ms.assetid: 18f3dcf7-9314-4a2b-8fed-54b00c0026dd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: joflore
ms.openlocfilehash: 34ecb3c25d0379d45c8645040246036247177c18
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552644"
---
# <a name="how-to-troubleshoot-password-management"></a><span data-ttu-id="4620b-103">How to troubleshoot Password Management</span><span class="sxs-lookup"><span data-stu-id="4620b-103">How to troubleshoot Password Management</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4620b-104">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="4620b-104">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="4620b-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="4620b-105">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
>
>

<span data-ttu-id="4620b-106">If you are having issues with Password Management, we're here to help.</span><span class="sxs-lookup"><span data-stu-id="4620b-106">If you are having issues with Password Management, we're here to help.</span></span> <span data-ttu-id="4620b-107">Most problems you may run into can be solved with a few simple troubleshooting steps which you can read about below to troubleshoot your deployment:</span><span class="sxs-lookup"><span data-stu-id="4620b-107">Most problems you may run into can be solved with a few simple troubleshooting steps which you can read about below to troubleshoot your deployment:</span></span>

* [<span data-ttu-id="4620b-108">**Information to include when you need help**</span><span class="sxs-lookup"><span data-stu-id="4620b-108">**Information to include when you need help**</span></span>](#information-to-include-when-you-need-help)
* [<span data-ttu-id="4620b-109">**Problems with Password Management configuration in the Azure Management Portal**</span><span class="sxs-lookup"><span data-stu-id="4620b-109">**Problems with Password Management configuration in the Azure Management Portal**</span></span>](#troubleshoot-password-reset-configuration-in-the-azure-management-portal)
* [<span data-ttu-id="4620b-110">**Problems with Password Managment reports in the Azure Management Portal**</span><span class="sxs-lookup"><span data-stu-id="4620b-110">**Problems with Password Managment reports in the Azure Management Portal**</span></span>](#troubleshoot-password-management-reports-in-the-azure-management-portal)
* [<span data-ttu-id="4620b-111">**Problems with the Password Reset Registration Portal**</span><span class="sxs-lookup"><span data-stu-id="4620b-111">**Problems with the Password Reset Registration Portal**</span></span>](#troubleshoot-the-password-reset-registration-portal)
* [<span data-ttu-id="4620b-112">**Problems with the Password Reset Portal**</span><span class="sxs-lookup"><span data-stu-id="4620b-112">**Problems with the Password Reset Portal**</span></span>](#troubleshoot-the-password-reset-portal)
* [<span data-ttu-id="4620b-113">**Problems with Password Writeback**</span><span class="sxs-lookup"><span data-stu-id="4620b-113">**Problems with Password Writeback**</span></span>](#troubleshoot-password-writeback)
  * [<span data-ttu-id="4620b-114">Password Writeback event log error codes</span><span class="sxs-lookup"><span data-stu-id="4620b-114">Password Writeback event log error codes</span></span>](#password-writeback-event-log-error-codes)
  * [<span data-ttu-id="4620b-115">Problems with Password Writeback connectivity</span><span class="sxs-lookup"><span data-stu-id="4620b-115">Problems with Password Writeback connectivity</span></span>](#troubleshoot-password-writeback-connectivity)

<span data-ttu-id="4620b-116">If you've tried the troubleshooting steps below and are still running into problems, you can post a question on the [Azure AD Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD) or contact support and we'll take a look at your problem as soon as we can.</span><span class="sxs-lookup"><span data-stu-id="4620b-116">If you've tried the troubleshooting steps below and are still running into problems, you can post a question on the [Azure AD Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=WindowsAzureAD) or contact support and we'll take a look at your problem as soon as we can.</span></span>

## <a name="information-to-include-when-you-need-help"></a><span data-ttu-id="4620b-117">Information to include when you need help</span><span class="sxs-lookup"><span data-stu-id="4620b-117">Information to include when you need help</span></span>
<span data-ttu-id="4620b-118">If you cannot solve your issue with the guidance below, you can contact our support engineers.</span><span class="sxs-lookup"><span data-stu-id="4620b-118">If you cannot solve your issue with the guidance below, you can contact our support engineers.</span></span> <span data-ttu-id="4620b-119">When you contact them, it is recommended to include the following information:</span><span class="sxs-lookup"><span data-stu-id="4620b-119">When you contact them, it is recommended to include the following information:</span></span>

* <span data-ttu-id="4620b-120">**General description of the error** – what exact error message did the user see?</span><span class="sxs-lookup"><span data-stu-id="4620b-120">**General description of the error** – what exact error message did the user see?</span></span>  <span data-ttu-id="4620b-121">If there was no error message, describe the unexpected behavior you noticed, in detail.</span><span class="sxs-lookup"><span data-stu-id="4620b-121">If there was no error message, describe the unexpected behavior you noticed, in detail.</span></span>
* <span data-ttu-id="4620b-122">**Page** – what page were you on when you saw the error (include the URL)?</span><span class="sxs-lookup"><span data-stu-id="4620b-122">**Page** – what page were you on when you saw the error (include the URL)?</span></span>
* <span data-ttu-id="4620b-123">**Date / Time / Timezone** – what was the precise date and time you saw the error (include the timezone)?</span><span class="sxs-lookup"><span data-stu-id="4620b-123">**Date / Time / Timezone** – what was the precise date and time you saw the error (include the timezone)?</span></span>
* <span data-ttu-id="4620b-124">**Support Code** – what was the support code generated when the user saw the error (to find this, reproduce the error, then click the Support Code link at the bottom of the screen and send the support engineer the GUID that results).</span><span class="sxs-lookup"><span data-stu-id="4620b-124">**Support Code** – what was the support code generated when the user saw the error (to find this, reproduce the error, then click the Support Code link at the bottom of the screen and send the support engineer the GUID that results).</span></span>

  * <span data-ttu-id="4620b-125">If you are on a page without a support code at the bottom, press F12 and search for SID and CID and send those two results to the support engineer.</span><span class="sxs-lookup"><span data-stu-id="4620b-125">If you are on a page without a support code at the bottom, press F12 and search for SID and CID and send those two results to the support engineer.</span></span>

    ![][001]
* <span data-ttu-id="4620b-126">**User ID** – what was the ID of the user who saw the error (e.g. user@contoso.com)?</span><span class="sxs-lookup"><span data-stu-id="4620b-126">**User ID** – what was the ID of the user who saw the error (e.g. user@contoso.com)?</span></span>
* <span data-ttu-id="4620b-127">**Information about the user** – was the user federated, password hash synced, cloud only?</span><span class="sxs-lookup"><span data-stu-id="4620b-127">**Information about the user** – was the user federated, password hash synced, cloud only?</span></span>  <span data-ttu-id="4620b-128">Did the user have an AAD Premium or AAD Basic license assigned?</span><span class="sxs-lookup"><span data-stu-id="4620b-128">Did the user have an AAD Premium or AAD Basic license assigned?</span></span>
* <span data-ttu-id="4620b-129">**Application Event Log** – if you are using Password Writeback and the error is in your on-premises infrastructure, please zip up a copy of your application event log from your Azure AD Connect server and send along with your request.</span><span class="sxs-lookup"><span data-stu-id="4620b-129">**Application Event Log** – if you are using Password Writeback and the error is in your on-premises infrastructure, please zip up a copy of your application event log from your Azure AD Connect server and send along with your request.</span></span>

<span data-ttu-id="4620b-130">Including this information will help us to solve your problem as quickly as possible.</span><span class="sxs-lookup"><span data-stu-id="4620b-130">Including this information will help us to solve your problem as quickly as possible.</span></span>

## <a name="troubleshoot-password-reset-configuration-in-the-azure-management-portal"></a><span data-ttu-id="4620b-131">Troubleshoot password reset configuration in the Azure Management Portal</span><span class="sxs-lookup"><span data-stu-id="4620b-131">Troubleshoot password reset configuration in the Azure Management Portal</span></span>
<span data-ttu-id="4620b-132">If you encounter an error when configuring password reset, you might be able to resolve it by following the troubleshooting steps below:</span><span class="sxs-lookup"><span data-stu-id="4620b-132">If you encounter an error when configuring password reset, you might be able to resolve it by following the troubleshooting steps below:</span></span>

<table>
          <tbody><tr>
            <td>
              <p><span data-ttu-id="4620b-133">
                <strong>Error Case</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-133">
                <strong>Error Case</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-134">
                <strong>What error does a user see?</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-134">
                <strong>What error does a user see?</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-135">
                <strong>Solution</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-135">
                <strong>Solution</strong>
              </span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-136">I don’t see the <strong>User Password Reset Policy </strong>section under the <strong>Configure</strong> tab in the Azure management portal</span><span class="sxs-lookup"><span data-stu-id="4620b-136">I don’t see the <strong>User Password Reset Policy </strong>section under the <strong>Configure</strong> tab in the Azure management portal</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-137">The <strong>User Password Reset Policy </strong>section is not visible on the <strong>Configure</strong> tab in the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="4620b-137">The <strong>User Password Reset Policy </strong>section is not visible on the <strong>Configure</strong> tab in the Azure Management Portal.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-138">This can occur if you do not have an AAD Premium or AAD Basic license assigned to the admin performing this operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-138">This can occur if you do not have an AAD Premium or AAD Basic license assigned to the admin performing this operation.</span></span> </p>
              <p><span data-ttu-id="4620b-139">To rectify this, assign an AAD Premium or AAD Basic license to the admin account in question by navigating to the <strong>Licenses</strong> tab and try again.</span><span class="sxs-lookup"><span data-stu-id="4620b-139">To rectify this, assign an AAD Premium or AAD Basic license to the admin account in question by navigating to the <strong>Licenses</strong> tab and try again.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-140">I don’t see any of the configuration options under the <strong>User Password Reset Policy</strong> section that are described in the documentation.</span><span class="sxs-lookup"><span data-stu-id="4620b-140">I don’t see any of the configuration options under the <strong>User Password Reset Policy</strong> section that are described in the documentation.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-141">The <strong>User Password Reset Policy </strong>section is visible, but the only flag that appears under it is the <strong>Users Enabled for Password Reset</strong> flag.</span><span class="sxs-lookup"><span data-stu-id="4620b-141">The <strong>User Password Reset Policy </strong>section is visible, but the only flag that appears under it is the <strong>Users Enabled for Password Reset</strong> flag.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-142">The rest of the UI will appear when you switch the <strong>Users Enabled for Password Reset</strong> flag to <strong>Yes.</strong></span><span class="sxs-lookup"><span data-stu-id="4620b-142">The rest of the UI will appear when you switch the <strong>Users Enabled for Password Reset</strong> flag to <strong>Yes.</strong></span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-143">I don’t see a particular configuration option.</span><span class="sxs-lookup"><span data-stu-id="4620b-143">I don’t see a particular configuration option.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-144">For example, I do not see the <strong>Number of days before a user must confirm their contact data</strong> option when I scroll through the <strong>User Password Reset Policy</strong> section (or other examples of the same issue).</span><span class="sxs-lookup"><span data-stu-id="4620b-144">For example, I do not see the <strong>Number of days before a user must confirm their contact data</strong> option when I scroll through the <strong>User Password Reset Policy</strong> section (or other examples of the same issue).</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-145">Many elements of UI are hidden until they are needed.</span><span class="sxs-lookup"><span data-stu-id="4620b-145">Many elements of UI are hidden until they are needed.</span></span> <span data-ttu-id="4620b-146">Try enabling all the options on the page if you want to see.</span><span class="sxs-lookup"><span data-stu-id="4620b-146">Try enabling all the options on the page if you want to see.</span></span></p>
              <p><span data-ttu-id="4620b-147">See <a href="active-directory-passwords-customize.md#password-management-behavior">Password Management behavior</a> for more info about all of the controls that are available to you.</span><span class="sxs-lookup"><span data-stu-id="4620b-147">See <a href="active-directory-passwords-customize.md#password-management-behavior">Password Management behavior</a> for more info about all of the controls that are available to you.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-148">I don’t see the <strong>Write Back Passwords to On-Premises</strong> configuration option</span><span class="sxs-lookup"><span data-stu-id="4620b-148">I don’t see the <strong>Write Back Passwords to On-Premises</strong> configuration option</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-149">The <strong>Write Back Passwords to On-Premises</strong> option is not visible under the <strong>Configure</strong> tab in the Azure Management Portal</span><span class="sxs-lookup"><span data-stu-id="4620b-149">The <strong>Write Back Passwords to On-Premises</strong> option is not visible under the <strong>Configure</strong> tab in the Azure Management Portal</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-150">This option is only visible if you have downloaded Azure AD Connect and configured Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-150">This option is only visible if you have downloaded Azure AD Connect and configured Password Writeback.</span></span> <span data-ttu-id="4620b-151">When you have done this, that option appears and allows you to enable or disable writeback from the cloud.</span><span class="sxs-lookup"><span data-stu-id="4620b-151">When you have done this, that option appears and allows you to enable or disable writeback from the cloud.</span></span></p>
              <p><span data-ttu-id="4620b-152">See <a href="active-directory-passwords-getting-started.md#step-2-enable-password-writeback-in-azure-ad-connect">Enable Password Writeback in Azure AD Connect</a> for more information on how to do this.</span><span class="sxs-lookup"><span data-stu-id="4620b-152">See <a href="active-directory-passwords-getting-started.md#step-2-enable-password-writeback-in-azure-ad-connect">Enable Password Writeback in Azure AD Connect</a> for more information on how to do this.</span></span></p>
            </td>
          </tr>
        </tbody></table>

## <a name="troubleshoot-password-management-reports-in-the-azure-management-portal"></a><span data-ttu-id="4620b-153">Troubleshoot password management reports in the Azure Management Portal</span><span class="sxs-lookup"><span data-stu-id="4620b-153">Troubleshoot password management reports in the Azure Management Portal</span></span>
<span data-ttu-id="4620b-154">If you encounter an error when using the password management reports, you might be able to resolve it by following the troubleshooting steps below:</span><span class="sxs-lookup"><span data-stu-id="4620b-154">If you encounter an error when using the password management reports, you might be able to resolve it by following the troubleshooting steps below:</span></span>

<table>
          <tbody><tr>
            <td>
              <p><span data-ttu-id="4620b-155">
                <strong>Error Case</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-155">
                <strong>Error Case</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-156">
                <strong>What error does a user see?</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-156">
                <strong>What error does a user see?</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-157">
                <strong>Solution</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-157">
                <strong>Solution</strong>
              </span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-158">I don’t see any password management reports</span><span class="sxs-lookup"><span data-stu-id="4620b-158">I don’t see any password management reports</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-159">The <strong>Password reset activity</strong> and <strong>Password reset registration activity</strong> reports are not visible under the <strong>Activity Log</strong> reports in the <strong>Reports</strong> tab.</span><span class="sxs-lookup"><span data-stu-id="4620b-159">The <strong>Password reset activity</strong> and <strong>Password reset registration activity</strong> reports are not visible under the <strong>Activity Log</strong> reports in the <strong>Reports</strong> tab.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-160">This can occur if you do not have an AAD Premium or AAD Basic license assigned to the admin performing this operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-160">This can occur if you do not have an AAD Premium or AAD Basic license assigned to the admin performing this operation.</span></span> </p>
              <p><span data-ttu-id="4620b-161">To rectify this, assign an AAD Premium or AAD Basic license to the admin account in question by navigating to the <strong>Licenses</strong> tab and try again.</span><span class="sxs-lookup"><span data-stu-id="4620b-161">To rectify this, assign an AAD Premium or AAD Basic license to the admin account in question by navigating to the <strong>Licenses</strong> tab and try again.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-162">User registrations show multiple times</span><span class="sxs-lookup"><span data-stu-id="4620b-162">User registrations show multiple times</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-163">When a user registers alternate email, mobile phone, and security questions, they each show up as separate lines instead of a single line.</span><span class="sxs-lookup"><span data-stu-id="4620b-163">When a user registers alternate email, mobile phone, and security questions, they each show up as separate lines instead of a single line.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-164">Currently, when a user registers, we cannot assume that they will register everything present on the registration page.</span><span class="sxs-lookup"><span data-stu-id="4620b-164">Currently, when a user registers, we cannot assume that they will register everything present on the registration page.</span></span> <span data-ttu-id="4620b-165">As a result, we currently log each individual piece of data that is registered as a separate event.</span><span class="sxs-lookup"><span data-stu-id="4620b-165">As a result, we currently log each individual piece of data that is registered as a separate event.</span></span></p>
              <p><span data-ttu-id="4620b-166">If you want to aggregate this data, you can download the report and open the data as a pivot table in excel to have more flexibility.</span><span class="sxs-lookup"><span data-stu-id="4620b-166">If you want to aggregate this data, you can download the report and open the data as a pivot table in excel to have more flexibility.</span></span></p>
            </td>
          </tr>
        </tbody></table>

## <a name="troubleshoot-the-password-reset-registration-portal"></a><span data-ttu-id="4620b-167">Troubleshoot the password reset registration portal</span><span class="sxs-lookup"><span data-stu-id="4620b-167">Troubleshoot the password reset registration portal</span></span>
<span data-ttu-id="4620b-168">If you encounter an error when registering a user for password reset, you might be able to resolve it by following the troubleshooting steps below:</span><span class="sxs-lookup"><span data-stu-id="4620b-168">If you encounter an error when registering a user for password reset, you might be able to resolve it by following the troubleshooting steps below:</span></span>

<table>
          <tbody><tr>
            <td>
              <p><span data-ttu-id="4620b-169">
                <strong>Error Case</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-169">
                <strong>Error Case</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-170">
                <strong>What error does a user see?</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-170">
                <strong>What error does a user see?</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-171">
                <strong>Solution</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-171">
                <strong>Solution</strong>
              </span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-172">Directory is not enabled for password reset</span><span class="sxs-lookup"><span data-stu-id="4620b-172">Directory is not enabled for password reset</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-173">Your administrator has not enabled you to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4620b-173">Your administrator has not enabled you to use this feature.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-174">Switch the <strong>Users Enabled for Password Reset</strong> flag to <strong>Yes</strong> and hit <strong>Save</strong> in the Azure Management Portal directory configuration tab. You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-174">Switch the <strong>Users Enabled for Password Reset</strong> flag to <strong>Yes</strong> and hit <strong>Save</strong> in the Azure Management Portal directory configuration tab. You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-175">User does not have an AAD Premium or AAD Basic license assigned</span><span class="sxs-lookup"><span data-stu-id="4620b-175">User does not have an AAD Premium or AAD Basic license assigned</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-176">Your administrator has not enabled you to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4620b-176">Your administrator has not enabled you to use this feature.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-177">Assign an Azure AD Premium or Azure AD Basic license to the user under the <strong>Licenses</strong> tab in the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="4620b-177">Assign an Azure AD Premium or Azure AD Basic license to the user under the <strong>Licenses</strong> tab in the Azure Management Portal.</span></span> <span data-ttu-id="4620b-178">You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-178">You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-179">Error processing request</span><span class="sxs-lookup"><span data-stu-id="4620b-179">Error processing request</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-180">User sees an error that states:</span><span class="sxs-lookup"><span data-stu-id="4620b-180">User sees an error that states:</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-181">Error processing request</span><span class="sxs-lookup"><span data-stu-id="4620b-181">Error processing request</span></span> </p>
              <p><span data-ttu-id="4620b-182">When attempting to reset a password.</span><span class="sxs-lookup"><span data-stu-id="4620b-182">When attempting to reset a password.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-183">This can be caused by many issues, but generally this error is caused by either a service outage or configuration issue that cannot be resolved.</span><span class="sxs-lookup"><span data-stu-id="4620b-183">This can be caused by many issues, but generally this error is caused by either a service outage or configuration issue that cannot be resolved.</span></span> </p>
              <p><span data-ttu-id="4620b-184">If you see this error and it is impacting your business, please contact support and we will assist you ASAP.</span><span class="sxs-lookup"><span data-stu-id="4620b-184">If you see this error and it is impacting your business, please contact support and we will assist you ASAP.</span></span> <span data-ttu-id="4620b-185">See <a href="#information-to-include-when-you-need-help">Information to include when you need help</a> to see what you should provide to the support engineer to aid in a speedy resolution.</span><span class="sxs-lookup"><span data-stu-id="4620b-185">See <a href="#information-to-include-when-you-need-help">Information to include when you need help</a> to see what you should provide to the support engineer to aid in a speedy resolution.</span></span></p>
            </td>
          </tr>
        </tbody></table>

## <a name="troubleshoot-the-password-reset-portal"></a><span data-ttu-id="4620b-186">Troubleshoot the password reset portal</span><span class="sxs-lookup"><span data-stu-id="4620b-186">Troubleshoot the password reset portal</span></span>
<span data-ttu-id="4620b-187">If you encounter an error when resetting a password for a user, you might be able to resolve it by following the troubleshooting steps below:</span><span class="sxs-lookup"><span data-stu-id="4620b-187">If you encounter an error when resetting a password for a user, you might be able to resolve it by following the troubleshooting steps below:</span></span>

<table>
          <tbody><tr>
            <td>
              <p><span data-ttu-id="4620b-188">
                <strong>Error Case</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-188">
                <strong>Error Case</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-189">
                <strong>What error does a user see?</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-189">
                <strong>What error does a user see?</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-190">
                <strong>Solution</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-190">
                <strong>Solution</strong>
              </span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-191">Directory is not enabled for password reset</span><span class="sxs-lookup"><span data-stu-id="4620b-191">Directory is not enabled for password reset</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-192">Your account is not enabled for password reset</span><span class="sxs-lookup"><span data-stu-id="4620b-192">Your account is not enabled for password reset</span></span></p>
              <p><span data-ttu-id="4620b-193">We're sorry, but your administrator has not set up your account for use with this service.</span><span class="sxs-lookup"><span data-stu-id="4620b-193">We're sorry, but your administrator has not set up your account for use with this service.</span></span> </p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-194">If you'd like, we can contact an administrator in your organization to reset your password for you.</span><span class="sxs-lookup"><span data-stu-id="4620b-194">If you'd like, we can contact an administrator in your organization to reset your password for you.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-195">Switch the <strong>Users Enabled for Password Reset</strong> flag to <strong>Yes</strong> and hit <strong>Save</strong> in the Azure Management Portal directory configuration tab. You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-195">Switch the <strong>Users Enabled for Password Reset</strong> flag to <strong>Yes</strong> and hit <strong>Save</strong> in the Azure Management Portal directory configuration tab. You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-196">User does not have an AAD Premium or AAD Basic license assigned</span><span class="sxs-lookup"><span data-stu-id="4620b-196">User does not have an AAD Premium or AAD Basic license assigned</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-197">While we cannot reset non-admin account passwords automatically, we can contact your organization's admin to do it for you.</span><span class="sxs-lookup"><span data-stu-id="4620b-197">While we cannot reset non-admin account passwords automatically, we can contact your organization's admin to do it for you.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-198">Assign an Azure AD Premium or Azure AD Basic license to the user under the <strong>Licenses</strong> tab in the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="4620b-198">Assign an Azure AD Premium or Azure AD Basic license to the user under the <strong>Licenses</strong> tab in the Azure Management Portal.</span></span> <span data-ttu-id="4620b-199">You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-199">You must have an Azure AD Premium or Basic License assigned to the admin performing this operation.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-200">Directory is enabled for password reset, but user has missing or mal-formed authentication information</span><span class="sxs-lookup"><span data-stu-id="4620b-200">Directory is enabled for password reset, but user has missing or mal-formed authentication information</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-201">Your account is not enabled for password reset</span><span class="sxs-lookup"><span data-stu-id="4620b-201">Your account is not enabled for password reset</span></span></p>
              <p><span data-ttu-id="4620b-202">We're sorry, but your administrator has not set up your account for use with this service.</span><span class="sxs-lookup"><span data-stu-id="4620b-202">We're sorry, but your administrator has not set up your account for use with this service.</span></span> </p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-203">If you'd like, we can contact an administrator in your organization to reset your password for you.</span><span class="sxs-lookup"><span data-stu-id="4620b-203">If you'd like, we can contact an administrator in your organization to reset your password for you.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-204">Ensure that user has properly formed contact data on file in the directory before proceeding.</span><span class="sxs-lookup"><span data-stu-id="4620b-204">Ensure that user has properly formed contact data on file in the directory before proceeding.</span></span> <span data-ttu-id="4620b-205">See <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a> for information on how to configure authentication information in the directory so that users do not see this error.</span><span class="sxs-lookup"><span data-stu-id="4620b-205">See <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a> for information on how to configure authentication information in the directory so that users do not see this error.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-206">Directory is enabled for password reset, but a user only has one piece of contact data on file when policy is set to require two verification steps</span><span class="sxs-lookup"><span data-stu-id="4620b-206">Directory is enabled for password reset, but a user only has one piece of contact data on file when policy is set to require two verification steps</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-207">Your account is not enabled for password reset</span><span class="sxs-lookup"><span data-stu-id="4620b-207">Your account is not enabled for password reset</span></span></p>
              <p><span data-ttu-id="4620b-208">We're sorry, but your administrator has not set up your account for use with this service.</span><span class="sxs-lookup"><span data-stu-id="4620b-208">We're sorry, but your administrator has not set up your account for use with this service.</span></span> </p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-209">If you'd like, we can contact an administrator in your organization to reset your password for you.</span><span class="sxs-lookup"><span data-stu-id="4620b-209">If you'd like, we can contact an administrator in your organization to reset your password for you.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-210">Ensure that user has at least two properly configured contact methods (e.g., both Mobile Phone and Office Phone) before proceeding.</span><span class="sxs-lookup"><span data-stu-id="4620b-210">Ensure that user has at least two properly configured contact methods (e.g., both Mobile Phone and Office Phone) before proceeding.</span></span> <span data-ttu-id="4620b-211">See <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a> for information on how to configure authentication information in the directory so that users do not see this error.</span><span class="sxs-lookup"><span data-stu-id="4620b-211">See <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a> for information on how to configure authentication information in the directory so that users do not see this error.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-212">Directory is enabled for password reset, and user is properly configured, but user is unable to be contacted</span><span class="sxs-lookup"><span data-stu-id="4620b-212">Directory is enabled for password reset, and user is properly configured, but user is unable to be contacted</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-213">Oops!</span><span class="sxs-lookup"><span data-stu-id="4620b-213">Oops!</span></span>  <span data-ttu-id="4620b-214">We encountered an unexpected error while contacting you.</span><span class="sxs-lookup"><span data-stu-id="4620b-214">We encountered an unexpected error while contacting you.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-215">This could be the result of a temporary service error or misconfigured contact data that we could not properly detect.</span><span class="sxs-lookup"><span data-stu-id="4620b-215">This could be the result of a temporary service error or misconfigured contact data that we could not properly detect.</span></span> <span data-ttu-id="4620b-216">If the user waits 10 seconds, a try again and “contact your administrator” link appears.</span><span class="sxs-lookup"><span data-stu-id="4620b-216">If the user waits 10 seconds, a try again and “contact your administrator” link appears.</span></span> <span data-ttu-id="4620b-217">Clicking try again will re-dispatch the call, whereas clicking “contact your administrator” will send a form email to user, password, or global admins (in that precedence order) requesting a password reset to be performed for that user account.</span><span class="sxs-lookup"><span data-stu-id="4620b-217">Clicking try again will re-dispatch the call, whereas clicking “contact your administrator” will send a form email to user, password, or global admins (in that precedence order) requesting a password reset to be performed for that user account.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-218">User never receives the password reset SMS or phone call</span><span class="sxs-lookup"><span data-stu-id="4620b-218">User never receives the password reset SMS or phone call</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-219">User clicks “text me” or “call me” and then never receives anything.</span><span class="sxs-lookup"><span data-stu-id="4620b-219">User clicks “text me” or “call me” and then never receives anything.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-220">This could be the result of a mal-formed phone number in the directory.</span><span class="sxs-lookup"><span data-stu-id="4620b-220">This could be the result of a mal-formed phone number in the directory.</span></span> <span data-ttu-id="4620b-221">Make sure the phone number is in the format “+ccc xxxyyyzzzzXeeee”.</span><span class="sxs-lookup"><span data-stu-id="4620b-221">Make sure the phone number is in the format “+ccc xxxyyyzzzzXeeee”.</span></span> <span data-ttu-id="4620b-222">To learn more about formatting phone numbers for use with password reset see <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a>.</span><span class="sxs-lookup"><span data-stu-id="4620b-222">To learn more about formatting phone numbers for use with password reset see <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a>.</span></span></p>
              <p><span data-ttu-id="4620b-223">If you require an extension to be routed to the user in question, note that password reset does not support extensions, even if you specify one in the directory (they are stripped before the call is dispatched).</span><span class="sxs-lookup"><span data-stu-id="4620b-223">If you require an extension to be routed to the user in question, note that password reset does not support extensions, even if you specify one in the directory (they are stripped before the call is dispatched).</span></span> <span data-ttu-id="4620b-224">Try using a number without an extension, or integrating the extension into the phone number in your PBX.</span><span class="sxs-lookup"><span data-stu-id="4620b-224">Try using a number without an extension, or integrating the extension into the phone number in your PBX.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-225">User never receives password reset email</span><span class="sxs-lookup"><span data-stu-id="4620b-225">User never receives password reset email</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-226">User clicks “email me” and then never receives anything.</span><span class="sxs-lookup"><span data-stu-id="4620b-226">User clicks “email me” and then never receives anything.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-227">The most common cause for this issue is that the message is rejected by a spam filter.</span><span class="sxs-lookup"><span data-stu-id="4620b-227">The most common cause for this issue is that the message is rejected by a spam filter.</span></span> <span data-ttu-id="4620b-228">Check your spam, junk, or deleted items folder for the email.</span><span class="sxs-lookup"><span data-stu-id="4620b-228">Check your spam, junk, or deleted items folder for the email.</span></span></p>
              <p><span data-ttu-id="4620b-229">Also ensure that you are checking the right email for the message…lots of people have very similar email addresses and end up checking the wrong inbox for the message.</span><span class="sxs-lookup"><span data-stu-id="4620b-229">Also ensure that you are checking the right email for the message…lots of people have very similar email addresses and end up checking the wrong inbox for the message.</span></span> <span data-ttu-id="4620b-230">If neither of these options work, it’s also possible that the email address in the directory is malformed, check to make sure the email address is the right one and try again.</span><span class="sxs-lookup"><span data-stu-id="4620b-230">If neither of these options work, it’s also possible that the email address in the directory is malformed, check to make sure the email address is the right one and try again.</span></span> <span data-ttu-id="4620b-231">To learn more about formatting email addresses for use with password reset see <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a>.</span><span class="sxs-lookup"><span data-stu-id="4620b-231">To learn more about formatting email addresses for use with password reset see <a href="active-directory-passwords-learn-more.md#what-data-is-used-by-password-reset">What data is used by password reset</a>.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-232">I have set a password reset policy, but when an admin account uses password reset, that policy is not applied</span><span class="sxs-lookup"><span data-stu-id="4620b-232">I have set a password reset policy, but when an admin account uses password reset, that policy is not applied</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-233">Admin accounts resetting their passwords see the same options enabled for password reset, email and mobile phone, no matter what policy is set under the <strong>User Password Reset Policy</strong> section of the <strong>Configure</strong> tab.</span><span class="sxs-lookup"><span data-stu-id="4620b-233">Admin accounts resetting their passwords see the same options enabled for password reset, email and mobile phone, no matter what policy is set under the <strong>User Password Reset Policy</strong> section of the <strong>Configure</strong> tab.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-234">The options configured under the <strong>User Password Reset Policy</strong> section of the <strong>Configure</strong> tab only apply to end users in your organization.</span><span class="sxs-lookup"><span data-stu-id="4620b-234">The options configured under the <strong>User Password Reset Policy</strong> section of the <strong>Configure</strong> tab only apply to end users in your organization.</span></span></p>
              <p><span data-ttu-id="4620b-235">Microsoft manages and controls the Admin password reset policy in order to ensure the highest level of security</span><span class="sxs-lookup"><span data-stu-id="4620b-235">Microsoft manages and controls the Admin password reset policy in order to ensure the highest level of security</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-236">User prevented from attempting password reset too many times in a day</span><span class="sxs-lookup"><span data-stu-id="4620b-236">User prevented from attempting password reset too many times in a day</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-237">User sees an error stating:</span><span class="sxs-lookup"><span data-stu-id="4620b-237">User sees an error stating:</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-238">Please use another option.</span><span class="sxs-lookup"><span data-stu-id="4620b-238">Please use another option.</span></span></p>
              <p><span data-ttu-id="4620b-239">You've tried to verify your account too many times in the last 1 hour(s).</span><span class="sxs-lookup"><span data-stu-id="4620b-239">You've tried to verify your account too many times in the last 1 hour(s).</span></span> <span data-ttu-id="4620b-240">For security reasons, you'll have to wait 24 hour(s) before you can try again.</span><span class="sxs-lookup"><span data-stu-id="4620b-240">For security reasons, you'll have to wait 24 hour(s) before you can try again.</span></span> </p>
              <p><span data-ttu-id="4620b-241">If you'd like, we can contact an administrator in your organization to reset your password for you.</span><span class="sxs-lookup"><span data-stu-id="4620b-241">If you'd like, we can contact an administrator in your organization to reset your password for you.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-242">We implement an automatic throttling mechanism to block users from attempting to reset their passwords too many times in a short period of time.</span><span class="sxs-lookup"><span data-stu-id="4620b-242">We implement an automatic throttling mechanism to block users from attempting to reset their passwords too many times in a short period of time.</span></span> <span data-ttu-id="4620b-243">This occurs when:</span><span class="sxs-lookup"><span data-stu-id="4620b-243">This occurs when:</span></span></p>
              <ol class="ordered">
                <li>
<span data-ttu-id="4620b-244">User attempts to validate a phone number 5 times in one hour.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-244">User attempts to validate a phone number 5 times in one hour.<br\><br\></span></span></li>
                <li>
<span data-ttu-id="4620b-245">User attempts to use the security questions gate 5 times in one hour.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-245">User attempts to use the security questions gate 5 times in one hour.<br\><br\></span></span></li>
                <li>
<span data-ttu-id="4620b-246">User attempts to reset a password for the same user account 5 times in one hour.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-246">User attempts to reset a password for the same user account 5 times in one hour.<br\><br\></span></span></li>
              </ol>
              <p><span data-ttu-id="4620b-247">To fix this, instruct the user to wait 24 hours after the last attempt, and the user will then be able to reset his or her password.</span><span class="sxs-lookup"><span data-stu-id="4620b-247">To fix this, instruct the user to wait 24 hours after the last attempt, and the user will then be able to reset his or her password.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-248">User sees an error when validating his or her phone number</span><span class="sxs-lookup"><span data-stu-id="4620b-248">User sees an error when validating his or her phone number</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-249">When attempting to verify a phone to use as an authentication method, the user sees an error stating:</span><span class="sxs-lookup"><span data-stu-id="4620b-249">When attempting to verify a phone to use as an authentication method, the user sees an error stating:</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-250">Incorrect phone number specified.</span><span class="sxs-lookup"><span data-stu-id="4620b-250">Incorrect phone number specified.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-251">This error occurs when the phone number entered does not match the phone number on file.</span><span class="sxs-lookup"><span data-stu-id="4620b-251">This error occurs when the phone number entered does not match the phone number on file.</span></span></p>
              <p><span data-ttu-id="4620b-252">Make sure the user is entering the complete phone number, including area and country code, when attempting to use a phone-based method for password reset.</span><span class="sxs-lookup"><span data-stu-id="4620b-252">Make sure the user is entering the complete phone number, including area and country code, when attempting to use a phone-based method for password reset.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-253">Error processing request</span><span class="sxs-lookup"><span data-stu-id="4620b-253">Error processing request</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-254">User sees an error that states:</span><span class="sxs-lookup"><span data-stu-id="4620b-254">User sees an error that states:</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-255">Error processing request</span><span class="sxs-lookup"><span data-stu-id="4620b-255">Error processing request</span></span> </p>
              <p><span data-ttu-id="4620b-256">When attempting to reset a password.</span><span class="sxs-lookup"><span data-stu-id="4620b-256">When attempting to reset a password.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-257">This can be caused by many issues, but generally this error is caused by either a service outage or configuration issue that cannot be resolved.</span><span class="sxs-lookup"><span data-stu-id="4620b-257">This can be caused by many issues, but generally this error is caused by either a service outage or configuration issue that cannot be resolved.</span></span> </p>
              <p><span data-ttu-id="4620b-258">If you see this error and it is impacting your business, please contact support and we will assist you ASAP.</span><span class="sxs-lookup"><span data-stu-id="4620b-258">If you see this error and it is impacting your business, please contact support and we will assist you ASAP.</span></span> <span data-ttu-id="4620b-259">See <a href="#information-to-include-when-you-need-help">Information to include when you need help</a> to see what you should provide to the support engineer to aid in a speedy resolution.</span><span class="sxs-lookup"><span data-stu-id="4620b-259">See <a href="#information-to-include-when-you-need-help">Information to include when you need help</a> to see what you should provide to the support engineer to aid in a speedy resolution.</span></span></p>
            </td>
          </tr>
        </tbody></table>

## <a name="troubleshoot-password-writeback"></a><span data-ttu-id="4620b-260">Troubleshoot Password Writeback</span><span class="sxs-lookup"><span data-stu-id="4620b-260">Troubleshoot Password Writeback</span></span>
<span data-ttu-id="4620b-261">If you encounter an error when enabling, disabling, or using Password Writeback, you might be able to resolve it by following the troubleshooting steps below:</span><span class="sxs-lookup"><span data-stu-id="4620b-261">If you encounter an error when enabling, disabling, or using Password Writeback, you might be able to resolve it by following the troubleshooting steps below:</span></span>

<table>
          <tbody><tr>
            <td>
              <p><span data-ttu-id="4620b-262">
                <strong>Error Case</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-262">
                <strong>Error Case</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-263">
                <strong>What error does a user see?</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-263">
                <strong>What error does a user see?</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-264">
                <strong>Solution</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-264">
                <strong>Solution</strong>
              </span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-265">General onboarding and startup failures</span><span class="sxs-lookup"><span data-stu-id="4620b-265">General onboarding and startup failures</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-266">Password reset service does not start on premises with error 6800 in the Azure AD Connect machine’s application event log.</span><span class="sxs-lookup"><span data-stu-id="4620b-266">Password reset service does not start on premises with error 6800 in the Azure AD Connect machine’s application event log.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-267">After onboarding, federated or password hash synced users cannot reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="4620b-267">After onboarding, federated or password hash synced users cannot reset their passwords.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-268">When Password Writeback is enabled, the sync engine will call the writeback library to perform the configuration (onboarding) by talking to the cloud onboarding service.</span><span class="sxs-lookup"><span data-stu-id="4620b-268">When Password Writeback is enabled, the sync engine will call the writeback library to perform the configuration (onboarding) by talking to the cloud onboarding service.</span></span> <span data-ttu-id="4620b-269">Any errors encountered during onboarding or while starting the WCF endpoint for Password Writeback will result in errors in the Event log in your Azure AD Connect machine’s event log.</span><span class="sxs-lookup"><span data-stu-id="4620b-269">Any errors encountered during onboarding or while starting the WCF endpoint for Password Writeback will result in errors in the Event log in your Azure AD Connect machine’s event log.</span></span></p>
              <p><span data-ttu-id="4620b-270">During restart of ADSync service, if writeback was configured, the WCF endpoint will be started up.</span><span class="sxs-lookup"><span data-stu-id="4620b-270">During restart of ADSync service, if writeback was configured, the WCF endpoint will be started up.</span></span> <span data-ttu-id="4620b-271">However, if the startup of the endpoint fails, we will simply log event 6800 and let the sync service startup.</span><span class="sxs-lookup"><span data-stu-id="4620b-271">However, if the startup of the endpoint fails, we will simply log event 6800 and let the sync service startup.</span></span> <span data-ttu-id="4620b-272">Presence of this event means that the Password Writeback endpoint was not started up.</span><span class="sxs-lookup"><span data-stu-id="4620b-272">Presence of this event means that the Password Writeback endpoint was not started up.</span></span> <span data-ttu-id="4620b-273">Event log details for this event (6800) along with event log entries generate by PasswordResetService component will indicate why the endpoint could not be started up.</span><span class="sxs-lookup"><span data-stu-id="4620b-273">Event log details for this event (6800) along with event log entries generate by PasswordResetService component will indicate why the endpoint could not be started up.</span></span> <span data-ttu-id="4620b-274">Review these event log errors and try to re-start the Azure AD Connect if Password Writeback still isn’t working.</span><span class="sxs-lookup"><span data-stu-id="4620b-274">Review these event log errors and try to re-start the Azure AD Connect if Password Writeback still isn’t working.</span></span> <span data-ttu-id="4620b-275">If the problem persists, try to disable and re-enable Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-275">If the problem persists, try to disable and re-enable Password Writeback.</span></span></p>
            </td>
          </tr>
                    <tr>
            <td>
              <p><span data-ttu-id="4620b-276">When a user attempts to reset a password or unlock an account with password writeback enabled, the operation fails.</span><span class="sxs-lookup"><span data-stu-id="4620b-276">When a user attempts to reset a password or unlock an account with password writeback enabled, the operation fails.</span></span> <span data-ttu-id="4620b-277">In addition, you see an event in the Azure AD Connect event log containing: “Synchronization Engine returned an error hr=800700CE, message=The filename or extension is too long” after the unlock operation occurs.</span><span class="sxs-lookup"><span data-stu-id="4620b-277">In addition, you see an event in the Azure AD Connect event log containing: “Synchronization Engine returned an error hr=800700CE, message=The filename or extension is too long” after the unlock operation occurs.</span></span>
                            </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-278">This can occur if you had upgraded from older versions of Azure AD Connect or DirSync.</span><span class="sxs-lookup"><span data-stu-id="4620b-278">This can occur if you had upgraded from older versions of Azure AD Connect or DirSync.</span></span> <span data-ttu-id="4620b-279">Upgrading to older versions of Azure AD Connect set a 254 character password for the Azure AD Management Agent account (newer versions will set a 127 character length password).</span><span class="sxs-lookup"><span data-stu-id="4620b-279">Upgrading to older versions of Azure AD Connect set a 254 character password for the Azure AD Management Agent account (newer versions will set a 127 character length password).</span></span> <span data-ttu-id="4620b-280">Such long passwords work for AD Connector Import and Export operations but they are not supported by the Unlock operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-280">Such long passwords work for AD Connector Import and Export operations but they are not supported by the Unlock operation.</span></span>
                            </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-281">[Find the Active Directory account](connect/active-directory-aadconnect-accounts-permissions.md#active-directory-account) for Azure AD Connect and reset the password to contain no more than 127 characters.</span><span class="sxs-lookup"><span data-stu-id="4620b-281">[Find the Active Directory account](connect/active-directory-aadconnect-accounts-permissions.md#active-directory-account) for Azure AD Connect and reset the password to contain no more than 127 characters.</span></span> <span data-ttu-id="4620b-282">Then open **Synchronization Service** from the Start menu.</span><span class="sxs-lookup"><span data-stu-id="4620b-282">Then open **Synchronization Service** from the Start menu.</span></span> <span data-ttu-id="4620b-283">Navigate to **Connectors** and find the **Active Directory Connector**.</span><span class="sxs-lookup"><span data-stu-id="4620b-283">Navigate to **Connectors** and find the **Active Directory Connector**.</span></span> <span data-ttu-id="4620b-284">Select it and click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4620b-284">Select it and click **Properties**.</span></span> <span data-ttu-id="4620b-285">Navigate to the page **Credentials** and enter the new password.</span><span class="sxs-lookup"><span data-stu-id="4620b-285">Navigate to the page **Credentials** and enter the new password.</span></span> <span data-ttu-id="4620b-286">Select **OK** to close the page.</span><span class="sxs-lookup"><span data-stu-id="4620b-286">Select **OK** to close the page.</span></span>
                            </p>
            </td>
          </tr>
                    <tr>
            <td>
              <p><span data-ttu-id="4620b-287">Error configuring writeback during Azure AD Connect installation.</span><span class="sxs-lookup"><span data-stu-id="4620b-287">Error configuring writeback during Azure AD Connect installation.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-288">At the last step of the Azure AD Connect installation process, you see an error indicating that Password Writeback could not be configured.</span><span class="sxs-lookup"><span data-stu-id="4620b-288">At the last step of the Azure AD Connect installation process, you see an error indicating that Password Writeback could not be configured.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-289">The Azure AD Connect Application event log contains error 32009 with text “Error getting auth token”.</span><span class="sxs-lookup"><span data-stu-id="4620b-289">The Azure AD Connect Application event log contains error 32009 with text “Error getting auth token”.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-290">This error occurs in the following two cases:</span><span class="sxs-lookup"><span data-stu-id="4620b-290">This error occurs in the following two cases:</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-291">You have specified an incorrect password for the global administrator account specified at the beginning of the Azure AD Connect installation process.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-291">You have specified an incorrect password for the global administrator account specified at the beginning of the Azure AD Connect installation process.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-292">You have attempted to use a federated user for the global administrator account specified at the beginning of the Azure AD Connect installation process.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-292">You have attempted to use a federated user for the global administrator account specified at the beginning of the Azure AD Connect installation process.<br\><br\></span></span></li>
              </ul>
              <p><span data-ttu-id="4620b-293">To fix this error, please ensure that you are not using a federated account for the global administrator you specified at the beginning of the Azure AD Connect installation process, and that the password specified is correct.</span><span class="sxs-lookup"><span data-stu-id="4620b-293">To fix this error, please ensure that you are not using a federated account for the global administrator you specified at the beginning of the Azure AD Connect installation process, and that the password specified is correct.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-294">Error configuring writeback during Azure AD Connect installation.</span><span class="sxs-lookup"><span data-stu-id="4620b-294">Error configuring writeback during Azure AD Connect installation.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-295">The Azure AD Connect machine event log contains error 32002 thrown by the PasswordResetService.</span><span class="sxs-lookup"><span data-stu-id="4620b-295">The Azure AD Connect machine event log contains error 32002 thrown by the PasswordResetService.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-296">The error reads: “Error Connecting to ServiceBus, The token provider was unable to provide a security token…”</span><span class="sxs-lookup"><span data-stu-id="4620b-296">The error reads: “Error Connecting to ServiceBus, The token provider was unable to provide a security token…”</span></span></p>
              <p>

              </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-297">The root cause of this error is that the password reset service running in your on-premises environment is not able to connect to the service bus endpoint in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4620b-297">The root cause of this error is that the password reset service running in your on-premises environment is not able to connect to the service bus endpoint in the cloud.</span></span> <span data-ttu-id="4620b-298">This error is normally normally caused by a firewall rule blocking an outbound connection to a particular port or web address.</span><span class="sxs-lookup"><span data-stu-id="4620b-298">This error is normally normally caused by a firewall rule blocking an outbound connection to a particular port or web address.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-299">Make sure your firewall allows outbound connections for the following:</span><span class="sxs-lookup"><span data-stu-id="4620b-299">Make sure your firewall allows outbound connections for the following:</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-300">All traffic over TCP 443 (HTTPS)<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-300">All traffic over TCP 443 (HTTPS)<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-301">Outbound connections to <br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-301">Outbound connections to <br\><br\></span></span></li>
              </ul>
              <p>

              </p>
              <p><span data-ttu-id="4620b-302">Once you have updated these rules, reboot the Azure AD Connect machine and Password Writeback should start working again.</span><span class="sxs-lookup"><span data-stu-id="4620b-302">Once you have updated these rules, reboot the Azure AD Connect machine and Password Writeback should start working again.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-303">Password Writeback endpoint on-prem not reachable</span><span class="sxs-lookup"><span data-stu-id="4620b-303">Password Writeback endpoint on-prem not reachable</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-304">After working for some time, federated or password hash synced users cannot reset their passwords.</span><span class="sxs-lookup"><span data-stu-id="4620b-304">After working for some time, federated or password hash synced users cannot reset their passwords.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-305">In some rare cases, the Password Writeback service may fail to re-start when Azure AD Connect has re-started.</span><span class="sxs-lookup"><span data-stu-id="4620b-305">In some rare cases, the Password Writeback service may fail to re-start when Azure AD Connect has re-started.</span></span> <span data-ttu-id="4620b-306">In these cases, first, check whether Password Writeback appears to be enabled on-prem.</span><span class="sxs-lookup"><span data-stu-id="4620b-306">In these cases, first, check whether Password Writeback appears to be enabled on-prem.</span></span> <span data-ttu-id="4620b-307">This can be done using the Azure AD Connect wizard or powershell (See HowTos section above).If the feature appears to be enabled, try enabling or disabling the feature again either through the UI or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4620b-307">This can be done using the Azure AD Connect wizard or powershell (See HowTos section above).If the feature appears to be enabled, try enabling or disabling the feature again either through the UI or PowerShell.</span></span> <span data-ttu-id="4620b-308">See “Step 2: Enable Password Writeback on your Directory Sync computer &amp; configure firewall rules” in <a href="active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords">How to enable/disable Password Writeback</a> for more information on how to do this.</span><span class="sxs-lookup"><span data-stu-id="4620b-308">See “Step 2: Enable Password Writeback on your Directory Sync computer &amp; configure firewall rules” in <a href="active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords">How to enable/disable Password Writeback</a> for more information on how to do this.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-309">If this doesn’t work, try completely uninstalling and re-installing Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4620b-309">If this doesn’t work, try completely uninstalling and re-installing Azure AD Connect.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-310">Permissions errors</span><span class="sxs-lookup"><span data-stu-id="4620b-310">Permissions errors</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-311">Federated or password hash sync’d users who attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span><span class="sxs-lookup"><span data-stu-id="4620b-311">Federated or password hash sync’d users who attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-312">In addition to this, during password reset operations, you may see an error regarding management agent was denied access in your on premises event logs.</span><span class="sxs-lookup"><span data-stu-id="4620b-312">In addition to this, during password reset operations, you may see an error regarding management agent was denied access in your on premises event logs.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-313">If you see these errors in your event log, confirm that the AD MA account (that was specified in the wizard at the time of configuration) has the necessary permissions for Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-313">If you see these errors in your event log, confirm that the AD MA account (that was specified in the wizard at the time of configuration) has the necessary permissions for Password Writeback.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-314">NOTE that once this permission is given it can take up to 1 hour for the permissions to trickle down via sdprop background task on the DC.</span><span class="sxs-lookup"><span data-stu-id="4620b-314">NOTE that once this permission is given it can take up to 1 hour for the permissions to trickle down via sdprop background task on the DC.</span></span> </p>
              <p><span data-ttu-id="4620b-315">For password reset to work, the permission needs to be stamped on the security descriptor of the user object whose password is being reset.</span><span class="sxs-lookup"><span data-stu-id="4620b-315">For password reset to work, the permission needs to be stamped on the security descriptor of the user object whose password is being reset.</span></span> <span data-ttu-id="4620b-316">Until this permission shows up on the user object, password reset will continue to fail with access denied.</span><span class="sxs-lookup"><span data-stu-id="4620b-316">Until this permission shows up on the user object, password reset will continue to fail with access denied.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-317">Error when configuring Password Writeback from the Azure AD Connect configuration wizard</span><span class="sxs-lookup"><span data-stu-id="4620b-317">Error when configuring Password Writeback from the Azure AD Connect configuration wizard</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-318">“Unable to Locate MA” error in Wizard while enabling/disabling Password Writeback</span><span class="sxs-lookup"><span data-stu-id="4620b-318">“Unable to Locate MA” error in Wizard while enabling/disabling Password Writeback</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-319">There is a known bug in the released version of Azure AD Connect which manifests in the following situation:</span><span class="sxs-lookup"><span data-stu-id="4620b-319">There is a known bug in the released version of Azure AD Connect which manifests in the following situation:</span></span></p>
              <ol class="ordered">
                <li>
<span data-ttu-id="4620b-320">You configure Azure AD Connect for tenant abc.com (Verified domain) using creds .</span><span class="sxs-lookup"><span data-stu-id="4620b-320">You configure Azure AD Connect for tenant abc.com (Verified domain) using creds .</span></span> <span data-ttu-id="4620b-321">This results in AAD connector with name “abc.com – AAD” being created.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-321">This results in AAD connector with name “abc.com – AAD” being created.<br\><br\></span></span></li>
                <li>
<span data-ttu-id="4620b-322">You then then change the AAD creds for the connector (using old sync UI) to  (note it’s the same tenant but different domain name).</span><span class="sxs-lookup"><span data-stu-id="4620b-322">You then then change the AAD creds for the connector (using old sync UI) to  (note it’s the same tenant but different domain name).</span></span> <br\><br\></li>
                <li>
<span data-ttu-id="4620b-323">Now you try to enable/disable Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-323">Now you try to enable/disable Password Writeback.</span></span> <span data-ttu-id="4620b-324">The wizard will construct the name of the connector using the creds, as “abc.onmicrosoft.com – AAD” and pass to the Password Writeback cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4620b-324">The wizard will construct the name of the connector using the creds, as “abc.onmicrosoft.com – AAD” and pass to the Password Writeback cmdlet.</span></span> <span data-ttu-id="4620b-325">This will fail because there is no connector created with this name.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-325">This will fail because there is no connector created with this name.<br\><br\></span></span></li>
              </ol>
              <p><span data-ttu-id="4620b-326">This has been fixed in our latest builds.</span><span class="sxs-lookup"><span data-stu-id="4620b-326">This has been fixed in our latest builds.</span></span> <span data-ttu-id="4620b-327">If you have an older build, the one workaround is to use the powershell cmdlet to enable/disable the feature.</span><span class="sxs-lookup"><span data-stu-id="4620b-327">If you have an older build, the one workaround is to use the powershell cmdlet to enable/disable the feature.</span></span> <span data-ttu-id="4620b-328">See “Step 2: Enable Password Writeback on your Directory Sync computer &amp; configure firewall rules” in <a href="active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords">How to enable/disable Password Writeback</a> for more information on how to do this.</span><span class="sxs-lookup"><span data-stu-id="4620b-328">See “Step 2: Enable Password Writeback on your Directory Sync computer &amp; configure firewall rules” in <a href="active-directory-passwords-getting-started.md#enable-users-to-reset-or-change-their-ad-passwords">How to enable/disable Password Writeback</a> for more information on how to do this.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-329">Unable to reset password for users in special groups such as Domain Admins / Enterprise Admins etc.</span><span class="sxs-lookup"><span data-stu-id="4620b-329">Unable to reset password for users in special groups such as Domain Admins / Enterprise Admins etc.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-330">Federated or password hash sync’d users who are part of protected groups and attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span><span class="sxs-lookup"><span data-stu-id="4620b-330">Federated or password hash sync’d users who are part of protected groups and attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-331">Privileged users in Active Directory are protected using AdminSDHolder.</span><span class="sxs-lookup"><span data-stu-id="4620b-331">Privileged users in Active Directory are protected using AdminSDHolder.</span></span> <span data-ttu-id="4620b-332">See <a href="https://technet.microsoft.com/magazine/2009.09.sdadminholder.aspx">http://technet.microsoft.com/magazine/2009.09.sdadminholder.aspx</a> for more details.</span><span class="sxs-lookup"><span data-stu-id="4620b-332">See <a href="https://technet.microsoft.com/magazine/2009.09.sdadminholder.aspx">http://technet.microsoft.com/magazine/2009.09.sdadminholder.aspx</a> for more details.</span></span> </p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-333">This means the security descriptors on these objects are periodically checked to match the one specified in AdminSDHolder and are reset if they are different.</span><span class="sxs-lookup"><span data-stu-id="4620b-333">This means the security descriptors on these objects are periodically checked to match the one specified in AdminSDHolder and are reset if they are different.</span></span> <span data-ttu-id="4620b-334">The additional permissions that are needed for Password Writeback therefore do not trickle to such users.</span><span class="sxs-lookup"><span data-stu-id="4620b-334">The additional permissions that are needed for Password Writeback therefore do not trickle to such users.</span></span> <span data-ttu-id="4620b-335">This can result in Password Writeback not working for such users.As a result, we do not support managing passwords for users within these groups because it breaks the AD security model.</span><span class="sxs-lookup"><span data-stu-id="4620b-335">This can result in Password Writeback not working for such users.As a result, we do not support managing passwords for users within these groups because it breaks the AD security model.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-336">Reset operations fails with Object could not be found</span><span class="sxs-lookup"><span data-stu-id="4620b-336">Reset operations fails with Object could not be found</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-337">Federated or password hash sync’d users who attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span><span class="sxs-lookup"><span data-stu-id="4620b-337">Federated or password hash sync’d users who attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-338">In addition to this, during password reset operations, you may see an error in your event logs from the Azure AD Connect service indicating an “Object could not be found” error.</span><span class="sxs-lookup"><span data-stu-id="4620b-338">In addition to this, during password reset operations, you may see an error in your event logs from the Azure AD Connect service indicating an “Object could not be found” error.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-339">This error usually indicates that the sync engine is unable to find either the user object in the AAD connector space or the linked MV or AD connector space object.</span><span class="sxs-lookup"><span data-stu-id="4620b-339">This error usually indicates that the sync engine is unable to find either the user object in the AAD connector space or the linked MV or AD connector space object.</span></span> </p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-340">To troubleshoot this, make sure that the user is indeed synced from on-prem to AAD via the current instance of Azure AD Connect and inspect the state of the objects in the connector spaces and MV.</span><span class="sxs-lookup"><span data-stu-id="4620b-340">To troubleshoot this, make sure that the user is indeed synced from on-prem to AAD via the current instance of Azure AD Connect and inspect the state of the objects in the connector spaces and MV.</span></span> <span data-ttu-id="4620b-341">Confirm that the AD CS object is connector to the MV object via the “Microsoft.InfromADUserAccountEnabled.xxx” rule.</span><span class="sxs-lookup"><span data-stu-id="4620b-341">Confirm that the AD CS object is connector to the MV object via the “Microsoft.InfromADUserAccountEnabled.xxx” rule.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-342">Reset operations fails with Multiple matches found eror</span><span class="sxs-lookup"><span data-stu-id="4620b-342">Reset operations fails with Multiple matches found eror</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-343">Federated or password hash sync’d users who attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span><span class="sxs-lookup"><span data-stu-id="4620b-343">Federated or password hash sync’d users who attempt to reset their passwords see an error after submitting the password indicating there was a service problem.</span></span></p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-344">In addition to this, during password reset operations, you may see an error in your event logs from the Azure AD Connect service indicating a “Multiple maches found” error.</span><span class="sxs-lookup"><span data-stu-id="4620b-344">In addition to this, during password reset operations, you may see an error in your event logs from the Azure AD Connect service indicating a “Multiple maches found” error.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-345">This indicates that the sync engine detected that the MV object is connected to more than one AD CS objects via the “Microsoft.InfromADUserAccountEnabled.xxx”.</span><span class="sxs-lookup"><span data-stu-id="4620b-345">This indicates that the sync engine detected that the MV object is connected to more than one AD CS objects via the “Microsoft.InfromADUserAccountEnabled.xxx”.</span></span> <span data-ttu-id="4620b-346">This means that the user has an enabled account in more than one forest.</span><span class="sxs-lookup"><span data-stu-id="4620b-346">This means that the user has an enabled account in more than one forest.</span></span> </p>
              <p>

              </p>
              <p><span data-ttu-id="4620b-347">Currently this scenario is not supported for Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-347">Currently this scenario is not supported for Password Writeback.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-348">Password operations fail with a configuration error.</span><span class="sxs-lookup"><span data-stu-id="4620b-348">Password operations fail with a configuration error.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-349">Password operations fail with a configuration error.</span><span class="sxs-lookup"><span data-stu-id="4620b-349">Password operations fail with a configuration error.</span></span> <span data-ttu-id="4620b-350">The application event log contains Azure AD Connect error 6329 with text: 0x8023061f (The operation failed because password synchronization is not enabled on this Management Agent.)</span><span class="sxs-lookup"><span data-stu-id="4620b-350">The application event log contains Azure AD Connect error 6329 with text: 0x8023061f (The operation failed because password synchronization is not enabled on this Management Agent.)</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-351">This occurs if the Azure AD Connect configuration is changed to add&nbsp;a new AD forest (or to remove and re-add an existing forest) <strong>after</strong> the Password Writeback feature has already been enabled.</span><span class="sxs-lookup"><span data-stu-id="4620b-351">This occurs if the Azure AD Connect configuration is changed to add&nbsp;a new AD forest (or to remove and re-add an existing forest) <strong>after</strong> the Password Writeback feature has already been enabled.</span></span> <span data-ttu-id="4620b-352">Password operations for users in such newly added forests will fail.</span><span class="sxs-lookup"><span data-stu-id="4620b-352">Password operations for users in such newly added forests will fail.</span></span> <span data-ttu-id="4620b-353">To fix the problem, disable and re-enable the Password Writeback feature after the forest configuration changes have been completed.</span><span class="sxs-lookup"><span data-stu-id="4620b-353">To fix the problem, disable and re-enable the Password Writeback feature after the forest configuration changes have been completed.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-354">Writing back passwords that have been reset by users works properly, but writing back passwords changed by a user or reset for a user by an administrator fails.</span><span class="sxs-lookup"><span data-stu-id="4620b-354">Writing back passwords that have been reset by users works properly, but writing back passwords changed by a user or reset for a user by an administrator fails.</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-355">When attempting to reset a password on behalf of a user from the Azure Management Portal, you see a message stating: “The password reset service running in your on-premises environment does not support administrators resetting user passwords.</span><span class="sxs-lookup"><span data-stu-id="4620b-355">When attempting to reset a password on behalf of a user from the Azure Management Portal, you see a message stating: “The password reset service running in your on-premises environment does not support administrators resetting user passwords.</span></span> <span data-ttu-id="4620b-356">Please upgrade to the latest version of Azure AD Connect to resolve this.”</span><span class="sxs-lookup"><span data-stu-id="4620b-356">Please upgrade to the latest version of Azure AD Connect to resolve this.”</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-357">This occurs when the version of the synchronization engine does not support the particular Password Writeback operation that was used.</span><span class="sxs-lookup"><span data-stu-id="4620b-357">This occurs when the version of the synchronization engine does not support the particular Password Writeback operation that was used.</span></span> <span data-ttu-id="4620b-358">Versions of Azure AD Connect later than 1.0.0419.0911 support all password management operations, including password reset writeback, password change writeback, and administrator-initiated password reset writeback from the Azure Management Portal.&nbsp; DirSync versions later than 1.0.6862 support password reset writeback only.</span><span class="sxs-lookup"><span data-stu-id="4620b-358">Versions of Azure AD Connect later than 1.0.0419.0911 support all password management operations, including password reset writeback, password change writeback, and administrator-initiated password reset writeback from the Azure Management Portal.&nbsp; DirSync versions later than 1.0.6862 support password reset writeback only.</span></span> <span data-ttu-id="4620b-359">To resolve this issue, we highly recommend that you install the latest version of Azure AD Connect or Azure Active Directory Connect.</span><span class="sxs-lookup"><span data-stu-id="4620b-359">To resolve this issue, we highly recommend that you install the latest version of Azure AD Connect or Azure Active Directory Connect.</span></span> <span data-ttu-id="4620b-360">For more information, see [Integrating your on-premises identities](connect/active-directory-aadconnect.md) to resolve this issue and to get the most out of Password Writeback in your organization.</span><span class="sxs-lookup"><span data-stu-id="4620b-360">For more information, see [Integrating your on-premises identities](connect/active-directory-aadconnect.md) to resolve this issue and to get the most out of Password Writeback in your organization.</span></span></p>
            </td>
          </tr>
        </tbody></table>


## <a name="password-writeback-event-log-error-codes"></a><span data-ttu-id="4620b-361">Password Writeback event log error codes</span><span class="sxs-lookup"><span data-stu-id="4620b-361">Password Writeback event log error codes</span></span>
<span data-ttu-id="4620b-362">A best practice when troubleshooting issues with Password Writeback is to inspect that Application Event Log on your Azure AD Connect machine.</span><span class="sxs-lookup"><span data-stu-id="4620b-362">A best practice when troubleshooting issues with Password Writeback is to inspect that Application Event Log on your Azure AD Connect machine.</span></span> <span data-ttu-id="4620b-363">This event log will contain events from two sources of interest for Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-363">This event log will contain events from two sources of interest for Password Writeback.</span></span> <span data-ttu-id="4620b-364">The PasswordResetService source will describe operations and issues related to the operation of Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-364">The PasswordResetService source will describe operations and issues related to the operation of Password Writeback.</span></span> <span data-ttu-id="4620b-365">The ADSync source will describe operations and issues related to setting passwords in your AD environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-365">The ADSync source will describe operations and issues related to setting passwords in your AD environment.</span></span>

<table>
          <tbody><tr>
            <td>
              <p><span data-ttu-id="4620b-366">
                <strong>Code</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-366">
                <strong>Code</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-367">
                <strong>Name / Message</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-367">
                <strong>Name / Message</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-368">
                <strong>Source</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-368">
                <strong>Source</strong>
              </span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-369">
                <strong>Description</strong>
              </span><span class="sxs-lookup"><span data-stu-id="4620b-369">
                <strong>Description</strong>
              </span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-370">6329</span><span class="sxs-lookup"><span data-stu-id="4620b-370">6329</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-371">BAIL: MMS(4924) 0x80230619 – “A restriction prevents the password from being changed to the current one specified.”</span><span class="sxs-lookup"><span data-stu-id="4620b-371">BAIL: MMS(4924) 0x80230619 – “A restriction prevents the password from being changed to the current one specified.”</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-372">ADSync</span><span class="sxs-lookup"><span data-stu-id="4620b-372">ADSync</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-373">This event occurs when the Password Writeback service attempts to set a password on your local directory which does not meet the password age, history, complexity, or filtering requirements of the domain.</span><span class="sxs-lookup"><span data-stu-id="4620b-373">This event occurs when the Password Writeback service attempts to set a password on your local directory which does not meet the password age, history, complexity, or filtering requirements of the domain.</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-374">If you have a minimum password age, and have recently changed the password within that window of time, you will not be able to change the password again until it reaches the specified age in your domain.</span><span class="sxs-lookup"><span data-stu-id="4620b-374">If you have a minimum password age, and have recently changed the password within that window of time, you will not be able to change the password again until it reaches the specified age in your domain.</span></span> <span data-ttu-id="4620b-375">For testing purposes, minimum age should be set to 0.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-375">For testing purposes, minimum age should be set to 0.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-376">If you have password history requirements enabled, then you must select a password that has not been used in the last N times, where N is the password history setting.</span><span class="sxs-lookup"><span data-stu-id="4620b-376">If you have password history requirements enabled, then you must select a password that has not been used in the last N times, where N is the password history setting.</span></span> <span data-ttu-id="4620b-377">If you do select a password that has been used in the last N times, then you will see a failure in this case.</span><span class="sxs-lookup"><span data-stu-id="4620b-377">If you do select a password that has been used in the last N times, then you will see a failure in this case.</span></span> <span data-ttu-id="4620b-378">For testing purposes, history should be set to 0.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-378">For testing purposes, history should be set to 0.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-379">If you have password complexity requirements, all of them will be enforced when the user attempts to change or reset a password.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-379">If you have password complexity requirements, all of them will be enforced when the user attempts to change or reset a password.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-380">If you have password filters enabled, and a user selects a password which does not meet the filtering criteria, then the reset or change operation will fail.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-380">If you have password filters enabled, and a user selects a password which does not meet the filtering criteria, then the reset or change operation will fail.<br\><br\></span></span></li>
              </ul>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-381">HR 8023042</span><span class="sxs-lookup"><span data-stu-id="4620b-381">HR 8023042</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-382">Synchronization Engine returned an error hr=80230402, message=An attempt to get an object failed because there are duplicated entries with the same anchor</span><span class="sxs-lookup"><span data-stu-id="4620b-382">Synchronization Engine returned an error hr=80230402, message=An attempt to get an object failed because there are duplicated entries with the same anchor</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-383">ADSync</span><span class="sxs-lookup"><span data-stu-id="4620b-383">ADSync</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-384">This event occurs when the same user id is enabled in multiple domains.</span><span class="sxs-lookup"><span data-stu-id="4620b-384">This event occurs when the same user id is enabled in multiple domains.</span></span>  <span data-ttu-id="4620b-385">For example, if you are syncing Account/Resource forests, and have the same user id present and enabled in each, this error may occur.</span><span class="sxs-lookup"><span data-stu-id="4620b-385">For example, if you are syncing Account/Resource forests, and have the same user id present and enabled in each, this error may occur.</span></span>  </p>
              <p><span data-ttu-id="4620b-386">This error can also occur if you are using a non-unique anchor attribute (like alias or UPN) and two users share that same anchor attribute.</span><span class="sxs-lookup"><span data-stu-id="4620b-386">This error can also occur if you are using a non-unique anchor attribute (like alias or UPN) and two users share that same anchor attribute.</span></span></p>
              <p><span data-ttu-id="4620b-387">To resolve this issue, ensure that you do not have any duplicated users within your domains and that you are using a unique anchor attribute for each user.</span><span class="sxs-lookup"><span data-stu-id="4620b-387">To resolve this issue, ensure that you do not have any duplicated users within your domains and that you are using a unique anchor attribute for each user.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-388">31001</span><span class="sxs-lookup"><span data-stu-id="4620b-388">31001</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-389">PasswordResetStart</span><span class="sxs-lookup"><span data-stu-id="4620b-389">PasswordResetStart</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-390">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-390">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-391">This event indicates that the on-premises service detected a password reset request for a federated or password hash sync’d user originating from the cloud.</span><span class="sxs-lookup"><span data-stu-id="4620b-391">This event indicates that the on-premises service detected a password reset request for a federated or password hash sync’d user originating from the cloud.</span></span> <span data-ttu-id="4620b-392">This event is the first event in every password reset writeback operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-392">This event is the first event in every password reset writeback operation.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-393">31002</span><span class="sxs-lookup"><span data-stu-id="4620b-393">31002</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-394">PasswordResetSuccess</span><span class="sxs-lookup"><span data-stu-id="4620b-394">PasswordResetSuccess</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-395">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-395">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-396">This event indicates that a user selected a new password during a password reset operation, we determined that this password meets corporate password requirements, and that password has been successfully written back to the local AD environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-396">This event indicates that a user selected a new password during a password reset operation, we determined that this password meets corporate password requirements, and that password has been successfully written back to the local AD environment.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-397">31003</span><span class="sxs-lookup"><span data-stu-id="4620b-397">31003</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-398">PasswordResetFail</span><span class="sxs-lookup"><span data-stu-id="4620b-398">PasswordResetFail</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-399">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-399">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-400">This event indicates that a user selected a password, and that password arrived successfully to the on-premises environment, but when we attempted to set the password in the local AD environment, a failure occurred.</span><span class="sxs-lookup"><span data-stu-id="4620b-400">This event indicates that a user selected a password, and that password arrived successfully to the on-premises environment, but when we attempted to set the password in the local AD environment, a failure occurred.</span></span> <span data-ttu-id="4620b-401">This can happen for several reasons:</span><span class="sxs-lookup"><span data-stu-id="4620b-401">This can happen for several reasons:</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-402">The user’s password does not meet the age, history, complexity, or filter requirements for the domain.</span><span class="sxs-lookup"><span data-stu-id="4620b-402">The user’s password does not meet the age, history, complexity, or filter requirements for the domain.</span></span> <span data-ttu-id="4620b-403">Try a completely new password to resolve this.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-403">Try a completely new password to resolve this.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-404">The MA service account does not have the appropriate permissions to set the new password on the user account in question.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-404">The MA service account does not have the appropriate permissions to set the new password on the user account in question.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-405">The user’s account is in a protected group, such as domain or enterprise admins, which disallows password set operations.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-405">The user’s account is in a protected group, such as domain or enterprise admins, which disallows password set operations.<br\><br\></span></span></li>
              </ul>
              <p><span data-ttu-id="4620b-406">See <a href="#troubleshoot-password-writeback">Troubleshoot Password Writeback</a> to learn more about what other situtions can cause this error.</span><span class="sxs-lookup"><span data-stu-id="4620b-406">See <a href="#troubleshoot-password-writeback">Troubleshoot Password Writeback</a> to learn more about what other situtions can cause this error.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-407">31004</span><span class="sxs-lookup"><span data-stu-id="4620b-407">31004</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-408">OnboardingEventStart</span><span class="sxs-lookup"><span data-stu-id="4620b-408">OnboardingEventStart</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-409">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-409">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-410">This event occurs if you enable Password Writeback with Azure AD Connect and indicates that we started onboarding your organization to the Password Writeback web service.</span><span class="sxs-lookup"><span data-stu-id="4620b-410">This event occurs if you enable Password Writeback with Azure AD Connect and indicates that we started onboarding your organization to the Password Writeback web service.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-411">31005</span><span class="sxs-lookup"><span data-stu-id="4620b-411">31005</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-412">OnboardingEventSuccess</span><span class="sxs-lookup"><span data-stu-id="4620b-412">OnboardingEventSuccess</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-413">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-413">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-414">This event indicates the onboarding process was successful and that Password Writeback capability is ready to use.</span><span class="sxs-lookup"><span data-stu-id="4620b-414">This event indicates the onboarding process was successful and that Password Writeback capability is ready to use.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-415">31006</span><span class="sxs-lookup"><span data-stu-id="4620b-415">31006</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-416">ChangePasswordStart</span><span class="sxs-lookup"><span data-stu-id="4620b-416">ChangePasswordStart</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-417">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-417">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-418">This event indicates that the on-premises service detected a password change request for a federated or password hash sync’d user originating from the cloud.</span><span class="sxs-lookup"><span data-stu-id="4620b-418">This event indicates that the on-premises service detected a password change request for a federated or password hash sync’d user originating from the cloud.</span></span> <span data-ttu-id="4620b-419">This event is the first event in every password change writeback operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-419">This event is the first event in every password change writeback operation.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-420">31007</span><span class="sxs-lookup"><span data-stu-id="4620b-420">31007</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-421">ChangePasswordSuccess</span><span class="sxs-lookup"><span data-stu-id="4620b-421">ChangePasswordSuccess</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-422">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-422">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-423">This event indicates that a user selected a new password during a password change operation, we determined that this password meets corporate password requirements, and that password has been successfully written back to the local AD environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-423">This event indicates that a user selected a new password during a password change operation, we determined that this password meets corporate password requirements, and that password has been successfully written back to the local AD environment.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-424">31008</span><span class="sxs-lookup"><span data-stu-id="4620b-424">31008</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-425">ChangePasswordFail</span><span class="sxs-lookup"><span data-stu-id="4620b-425">ChangePasswordFail</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-426">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-426">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-427">This event indicates that a user selected a password, and that password arrived successfully to the on-premises environment, but when we attempted to set the password in the local AD environment, a failure occurred.</span><span class="sxs-lookup"><span data-stu-id="4620b-427">This event indicates that a user selected a password, and that password arrived successfully to the on-premises environment, but when we attempted to set the password in the local AD environment, a failure occurred.</span></span> <span data-ttu-id="4620b-428">This can happen for several reasons:</span><span class="sxs-lookup"><span data-stu-id="4620b-428">This can happen for several reasons:</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-429">The user’s password does not meet the age, history, complexity, or filter requirements for the domain.</span><span class="sxs-lookup"><span data-stu-id="4620b-429">The user’s password does not meet the age, history, complexity, or filter requirements for the domain.</span></span> <span data-ttu-id="4620b-430">Try a completely new password to resolve this.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-430">Try a completely new password to resolve this.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-431">The MA service account does not have the appropriate permissions to set the new password on the user account in question.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-431">The MA service account does not have the appropriate permissions to set the new password on the user account in question.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-432">The user’s account is in a protected group, such as domain or enterprise admins, which disallows password set operations.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-432">The user’s account is in a protected group, such as domain or enterprise admins, which disallows password set operations.<br\><br\></span></span></li>
              </ul>
              <p><span data-ttu-id="4620b-433">See <a href="#troubleshoot-password-writeback">Troubleshoot Password Writeback</a> to learn more about what other situations can cause this error.</span><span class="sxs-lookup"><span data-stu-id="4620b-433">See <a href="#troubleshoot-password-writeback">Troubleshoot Password Writeback</a> to learn more about what other situations can cause this error.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-434">31009</span><span class="sxs-lookup"><span data-stu-id="4620b-434">31009</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-435">ResetUserPasswordByAdminStart</span><span class="sxs-lookup"><span data-stu-id="4620b-435">ResetUserPasswordByAdminStart</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-436">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-436">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-437">The on-premises service detected a password reset request for a federated or password hash sync’d user originating from the administrator on behalf of a user.</span><span class="sxs-lookup"><span data-stu-id="4620b-437">The on-premises service detected a password reset request for a federated or password hash sync’d user originating from the administrator on behalf of a user.</span></span> <span data-ttu-id="4620b-438">This event is the first event in every admin-initiated password reset writeback operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-438">This event is the first event in every admin-initiated password reset writeback operation.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-439">31010</span><span class="sxs-lookup"><span data-stu-id="4620b-439">31010</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-440">ResetUserPasswordByAdminSuccess</span><span class="sxs-lookup"><span data-stu-id="4620b-440">ResetUserPasswordByAdminSuccess</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-441">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-441">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-442">The admin selected a new password during an admin-initiated password reset operation, we determined that this password meets corporate password requirements, and that password has been successfully written back to the local AD environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-442">The admin selected a new password during an admin-initiated password reset operation, we determined that this password meets corporate password requirements, and that password has been successfully written back to the local AD environment.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-443">31011</span><span class="sxs-lookup"><span data-stu-id="4620b-443">31011</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-444">ResetUserPasswordByAdminFail</span><span class="sxs-lookup"><span data-stu-id="4620b-444">ResetUserPasswordByAdminFail</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-445">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-445">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-446">The admin selected a password on behalf of a user, and that password arrived successfully to the on-premises environment, but when we attempted to set the password in the local AD environment, a failure occurred.</span><span class="sxs-lookup"><span data-stu-id="4620b-446">The admin selected a password on behalf of a user, and that password arrived successfully to the on-premises environment, but when we attempted to set the password in the local AD environment, a failure occurred.</span></span> <span data-ttu-id="4620b-447">This can happen for several reasons:</span><span class="sxs-lookup"><span data-stu-id="4620b-447">This can happen for several reasons:</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-448">The user’s password does not meet the age, history, complexity, or filter requirements for the domain.</span><span class="sxs-lookup"><span data-stu-id="4620b-448">The user’s password does not meet the age, history, complexity, or filter requirements for the domain.</span></span> <span data-ttu-id="4620b-449">Try a completely new password to resolve this.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-449">Try a completely new password to resolve this.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-450">The MA service account does not have the appropriate permissions to set the new password on the user account in question.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-450">The MA service account does not have the appropriate permissions to set the new password on the user account in question.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-451">The user’s account is in a protected group, such as domain or enterprise admins, which disallows password set operations.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-451">The user’s account is in a protected group, such as domain or enterprise admins, which disallows password set operations.<br\><br\></span></span></li>
              </ul>
              <p><span data-ttu-id="4620b-452">See <a href="#troubleshoot-password-writeback">Troubleshoot Password Writeback</a> to learn more about what other situtions can cause this error.</span><span class="sxs-lookup"><span data-stu-id="4620b-452">See <a href="#troubleshoot-password-writeback">Troubleshoot Password Writeback</a> to learn more about what other situtions can cause this error.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-453">31012</span><span class="sxs-lookup"><span data-stu-id="4620b-453">31012</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-454">OffboardingEventStart</span><span class="sxs-lookup"><span data-stu-id="4620b-454">OffboardingEventStart</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-455">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-455">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-456">This event occurs if you disable Password Writeback with Azure AD Connect and indicates that we started offboarding your organization to the Password Writeback web service.</span><span class="sxs-lookup"><span data-stu-id="4620b-456">This event occurs if you disable Password Writeback with Azure AD Connect and indicates that we started offboarding your organization to the Password Writeback web service.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-457">31013</span><span class="sxs-lookup"><span data-stu-id="4620b-457">31013</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-458">OffboardingEventSuccess</span><span class="sxs-lookup"><span data-stu-id="4620b-458">OffboardingEventSuccess</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-459">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-459">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-460">This event indicates the offboarding process was successful and that Password Writeback capability has been successfully disabled.</span><span class="sxs-lookup"><span data-stu-id="4620b-460">This event indicates the offboarding process was successful and that Password Writeback capability has been successfully disabled.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-461">31014</span><span class="sxs-lookup"><span data-stu-id="4620b-461">31014</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-462">OffboardingEventFail</span><span class="sxs-lookup"><span data-stu-id="4620b-462">OffboardingEventFail</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-463">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-463">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-464">This event indicates the offboarding process was not successful.</span><span class="sxs-lookup"><span data-stu-id="4620b-464">This event indicates the offboarding process was not successful.</span></span> <span data-ttu-id="4620b-465">This could be due to a permissions error on the cloud or on-premises administrator account specified during configuration, or because you are attempting to use a federated cloud global administrator when disabling Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-465">This could be due to a permissions error on the cloud or on-premises administrator account specified during configuration, or because you are attempting to use a federated cloud global administrator when disabling Password Writeback.</span></span> <span data-ttu-id="4620b-466">To fix this, check your administrative permissions and that you are not using any federated account while configuring the Password Writeback capability.</span><span class="sxs-lookup"><span data-stu-id="4620b-466">To fix this, check your administrative permissions and that you are not using any federated account while configuring the Password Writeback capability.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-467">31015</span><span class="sxs-lookup"><span data-stu-id="4620b-467">31015</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-468">WriteBackServiceStarted</span><span class="sxs-lookup"><span data-stu-id="4620b-468">WriteBackServiceStarted</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-469">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-469">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-470">This event indicates that the Password Writeback service has started successfully and is ready to accept password management requests from the cloud.</span><span class="sxs-lookup"><span data-stu-id="4620b-470">This event indicates that the Password Writeback service has started successfully and is ready to accept password management requests from the cloud.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-471">31016</span><span class="sxs-lookup"><span data-stu-id="4620b-471">31016</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-472">WriteBackServiceStopped</span><span class="sxs-lookup"><span data-stu-id="4620b-472">WriteBackServiceStopped</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-473">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-473">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-474">This event indicates that the Password Writeback service has stopped and that any password management requests from the cloud will not be successful.</span><span class="sxs-lookup"><span data-stu-id="4620b-474">This event indicates that the Password Writeback service has stopped and that any password management requests from the cloud will not be successful.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-475">31017</span><span class="sxs-lookup"><span data-stu-id="4620b-475">31017</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-476">AuthTokenSuccess</span><span class="sxs-lookup"><span data-stu-id="4620b-476">AuthTokenSuccess</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-477">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-477">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-478">This event indicates that we successfully retrieved an authorization token for the global admin specified during Azure AD Connect setup in order to start the offboarding or onboarding process.</span><span class="sxs-lookup"><span data-stu-id="4620b-478">This event indicates that we successfully retrieved an authorization token for the global admin specified during Azure AD Connect setup in order to start the offboarding or onboarding process.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-479">31018</span><span class="sxs-lookup"><span data-stu-id="4620b-479">31018</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-480">KeyPairCreationSuccess</span><span class="sxs-lookup"><span data-stu-id="4620b-480">KeyPairCreationSuccess</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-481">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-481">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-482">This event indicates that we successfully created the password encryption key that will be used to encrypt passwords from the cloud to be sent to your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-482">This event indicates that we successfully created the password encryption key that will be used to encrypt passwords from the cloud to be sent to your on-premises environment.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-483">32000</span><span class="sxs-lookup"><span data-stu-id="4620b-483">32000</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-484">UnknownError</span><span class="sxs-lookup"><span data-stu-id="4620b-484">UnknownError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-485">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-485">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-486">This event indicates an unknown error during a password management operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-486">This event indicates an unknown error during a password management operation.</span></span> <span data-ttu-id="4620b-487">Look at the exception text in the event for more details.</span><span class="sxs-lookup"><span data-stu-id="4620b-487">Look at the exception text in the event for more details.</span></span> <span data-ttu-id="4620b-488">If you are having problems, try disabling and re-enabling Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-488">If you are having problems, try disabling and re-enabling Password Writeback.</span></span> <span data-ttu-id="4620b-489">If this does not help, include a copy of your event log along with the tracking id specified insider to your support engineer.</span><span class="sxs-lookup"><span data-stu-id="4620b-489">If this does not help, include a copy of your event log along with the tracking id specified insider to your support engineer.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-490">32001</span><span class="sxs-lookup"><span data-stu-id="4620b-490">32001</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-491">ServiceError</span><span class="sxs-lookup"><span data-stu-id="4620b-491">ServiceError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-492">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-492">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-493">This event indicates there was an error connecting to the cloud password reset service, and generally occurs when the on-premises service was unable to connect to the password reset web service.</span><span class="sxs-lookup"><span data-stu-id="4620b-493">This event indicates there was an error connecting to the cloud password reset service, and generally occurs when the on-premises service was unable to connect to the password reset web service.</span></span> </p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-494">32002</span><span class="sxs-lookup"><span data-stu-id="4620b-494">32002</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-495">ServiceBusError</span><span class="sxs-lookup"><span data-stu-id="4620b-495">ServiceBusError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-496">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-496">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-497">This event indicates there was an error connecting to your tenant’s service bus instance.</span><span class="sxs-lookup"><span data-stu-id="4620b-497">This event indicates there was an error connecting to your tenant’s service bus instance.</span></span> <span data-ttu-id="4620b-498">This could happen because you are blocking outbound connections in your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-498">This could happen because you are blocking outbound connections in your on-premises environment.</span></span> <span data-ttu-id="4620b-499">Check your firewall to ensure you allow connections over TCP 443 and to <a href="https://ssprsbprodncu-sb.accesscontrol.windows.net/">https://ssprsbprodncu-sb.accesscontrol.windows.net/</a>, and try again.</span><span class="sxs-lookup"><span data-stu-id="4620b-499">Check your firewall to ensure you allow connections over TCP 443 and to <a href="https://ssprsbprodncu-sb.accesscontrol.windows.net/">https://ssprsbprodncu-sb.accesscontrol.windows.net/</a>, and try again.</span></span> <span data-ttu-id="4620b-500">If you are still having problems, try disabling and re-enabling Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-500">If you are still having problems, try disabling and re-enabling Password Writeback.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-501">32003</span><span class="sxs-lookup"><span data-stu-id="4620b-501">32003</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-502">InPutValidationError</span><span class="sxs-lookup"><span data-stu-id="4620b-502">InPutValidationError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-503">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-503">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-504">This event indicates that the input passed to our web service API was invalid.</span><span class="sxs-lookup"><span data-stu-id="4620b-504">This event indicates that the input passed to our web service API was invalid.</span></span> <span data-ttu-id="4620b-505">Try the operation again.</span><span class="sxs-lookup"><span data-stu-id="4620b-505">Try the operation again.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-506">32004</span><span class="sxs-lookup"><span data-stu-id="4620b-506">32004</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-507">DecryptionError</span><span class="sxs-lookup"><span data-stu-id="4620b-507">DecryptionError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-508">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-508">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-509">This event indicates that there was an error decrypting the password that arrived from the cloud.</span><span class="sxs-lookup"><span data-stu-id="4620b-509">This event indicates that there was an error decrypting the password that arrived from the cloud.</span></span> <span data-ttu-id="4620b-510">This could be because of a decryption key mismatch between the cloud service and your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-510">This could be because of a decryption key mismatch between the cloud service and your on-premises environment.</span></span> <span data-ttu-id="4620b-511">In order to resolve this, disable and re-enable Password Writeback in your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-511">In order to resolve this, disable and re-enable Password Writeback in your on-premises environment.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-512">32005</span><span class="sxs-lookup"><span data-stu-id="4620b-512">32005</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-513">ConfigurationError</span><span class="sxs-lookup"><span data-stu-id="4620b-513">ConfigurationError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-514">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-514">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-515">During onboarding, we save tenant-specific information in a configuration file in your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-515">During onboarding, we save tenant-specific information in a configuration file in your on-premises environment.</span></span> <span data-ttu-id="4620b-516">This event indicates there was an error saving this file or that when the service was started there was an error reading the file.</span><span class="sxs-lookup"><span data-stu-id="4620b-516">This event indicates there was an error saving this file or that when the service was started there was an error reading the file.</span></span> <span data-ttu-id="4620b-517">To fix this issue, try disabling and re-enabling Password Writeback to force a re-write of this configuration file.</span><span class="sxs-lookup"><span data-stu-id="4620b-517">To fix this issue, try disabling and re-enabling Password Writeback to force a re-write of this configuration file.</span></span> </p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-518">32006</span><span class="sxs-lookup"><span data-stu-id="4620b-518">32006</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-519">EndPointConfigurationError</span><span class="sxs-lookup"><span data-stu-id="4620b-519">EndPointConfigurationError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-520">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-520">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-521">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-521">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-522">32007</span><span class="sxs-lookup"><span data-stu-id="4620b-522">32007</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-523">OnBoardingConfigUpdateError</span><span class="sxs-lookup"><span data-stu-id="4620b-523">OnBoardingConfigUpdateError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-524">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-524">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-525">During onboarding, we send data from the cloud to the on-premises password reset service.</span><span class="sxs-lookup"><span data-stu-id="4620b-525">During onboarding, we send data from the cloud to the on-premises password reset service.</span></span> <span data-ttu-id="4620b-526">That data is then written to an in-memory file before being sent to the sync service to store this information securely on disk.</span><span class="sxs-lookup"><span data-stu-id="4620b-526">That data is then written to an in-memory file before being sent to the sync service to store this information securely on disk.</span></span> <span data-ttu-id="4620b-527">This event indicates a problem with writing or updating that data in memory.</span><span class="sxs-lookup"><span data-stu-id="4620b-527">This event indicates a problem with writing or updating that data in memory.</span></span> <span data-ttu-id="4620b-528">To fix this issue, try disabling and re-enabling Password Writeback to force a re-write of this configuration.</span><span class="sxs-lookup"><span data-stu-id="4620b-528">To fix this issue, try disabling and re-enabling Password Writeback to force a re-write of this configuration.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-529">32008</span><span class="sxs-lookup"><span data-stu-id="4620b-529">32008</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-530">ValidationError</span><span class="sxs-lookup"><span data-stu-id="4620b-530">ValidationError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-531">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-531">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-532">This event indicates we received an invalid response from the password reset web service.</span><span class="sxs-lookup"><span data-stu-id="4620b-532">This event indicates we received an invalid response from the password reset web service.</span></span> <span data-ttu-id="4620b-533">To fix this issue, try disabling and re-enabling Password Writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-533">To fix this issue, try disabling and re-enabling Password Writeback.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-534">32009</span><span class="sxs-lookup"><span data-stu-id="4620b-534">32009</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-535">AuthTokenError</span><span class="sxs-lookup"><span data-stu-id="4620b-535">AuthTokenError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-536">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-536">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-537">This event indicates that we could not get an authorization token for the global administrator account specified during Azure AD Connect setup.</span><span class="sxs-lookup"><span data-stu-id="4620b-537">This event indicates that we could not get an authorization token for the global administrator account specified during Azure AD Connect setup.</span></span> <span data-ttu-id="4620b-538">This error can be caused by a bad username or password specified for the global admin account or because the global admin account specified is federated.</span><span class="sxs-lookup"><span data-stu-id="4620b-538">This error can be caused by a bad username or password specified for the global admin account or because the global admin account specified is federated.</span></span> <span data-ttu-id="4620b-539">To fix this issue, re-run configuration with the correct username and password and ensure the administrator is a managed (cloud-only or password-sync’d) account.</span><span class="sxs-lookup"><span data-stu-id="4620b-539">To fix this issue, re-run configuration with the correct username and password and ensure the administrator is a managed (cloud-only or password-sync’d) account.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-540">32010</span><span class="sxs-lookup"><span data-stu-id="4620b-540">32010</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-541">CryptoError</span><span class="sxs-lookup"><span data-stu-id="4620b-541">CryptoError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-542">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-542">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-543">This event indicates there was an error when generating the password encryption key or decrypting a password that arrives from the cloud service.</span><span class="sxs-lookup"><span data-stu-id="4620b-543">This event indicates there was an error when generating the password encryption key or decrypting a password that arrives from the cloud service.</span></span> <span data-ttu-id="4620b-544">This error likely indicates an issue with your environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-544">This error likely indicates an issue with your environment.</span></span> <span data-ttu-id="4620b-545">Look at the details of your event log to learn more and resolve this issue.</span><span class="sxs-lookup"><span data-stu-id="4620b-545">Look at the details of your event log to learn more and resolve this issue.</span></span> <span data-ttu-id="4620b-546">You may also try disabling and re-enabling the Password Writeback service to resolve this.</span><span class="sxs-lookup"><span data-stu-id="4620b-546">You may also try disabling and re-enabling the Password Writeback service to resolve this.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-547">32011</span><span class="sxs-lookup"><span data-stu-id="4620b-547">32011</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-548">OnBoardingServiceError</span><span class="sxs-lookup"><span data-stu-id="4620b-548">OnBoardingServiceError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-549">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-549">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-550">This event indicates that the on-premises service could not properly communicate with the password reset web service to initiate the onboarding process.</span><span class="sxs-lookup"><span data-stu-id="4620b-550">This event indicates that the on-premises service could not properly communicate with the password reset web service to initiate the onboarding process.</span></span> <span data-ttu-id="4620b-551">This may be because of a firewall rule or problem getting an auth token for your tenant.</span><span class="sxs-lookup"><span data-stu-id="4620b-551">This may be because of a firewall rule or problem getting an auth token for your tenant.</span></span> <span data-ttu-id="4620b-552">To fix this, ensure that you are not blocking outbound connections over TCP 443 and TCP 9350-9354 or to <a href="https://ssprsbprodncu-sb.accesscontrol.windows.net/">https://ssprsbprodncu-sb.accesscontrol.windows.net/</a>, and that the AAD admin account you are using to onboard is not federated.</span><span class="sxs-lookup"><span data-stu-id="4620b-552">To fix this, ensure that you are not blocking outbound connections over TCP 443 and TCP 9350-9354 or to <a href="https://ssprsbprodncu-sb.accesscontrol.windows.net/">https://ssprsbprodncu-sb.accesscontrol.windows.net/</a>, and that the AAD admin account you are using to onboard is not federated.</span></span> </p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-553">32012</span><span class="sxs-lookup"><span data-stu-id="4620b-553">32012</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-554">OnBoardingServiceDisableError</span><span class="sxs-lookup"><span data-stu-id="4620b-554">OnBoardingServiceDisableError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-555">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-555">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-556">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-556">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-557">32013</span><span class="sxs-lookup"><span data-stu-id="4620b-557">32013</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-558">OffBoardingError</span><span class="sxs-lookup"><span data-stu-id="4620b-558">OffBoardingError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-559">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-559">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-560">This event indicates that the on-premises service could not properly communicate with the password reset web service to initiate the offboarding process.</span><span class="sxs-lookup"><span data-stu-id="4620b-560">This event indicates that the on-premises service could not properly communicate with the password reset web service to initiate the offboarding process.</span></span> <span data-ttu-id="4620b-561">This may be because of a firewall rule or problem getting an authorization token for your tenant.</span><span class="sxs-lookup"><span data-stu-id="4620b-561">This may be because of a firewall rule or problem getting an authorization token for your tenant.</span></span> <span data-ttu-id="4620b-562">To fix this, ensure that you are not blocking outbound connections over 443 or to <a href="https://ssprsbprodncu-sb.accesscontrol.windows.net/">https://ssprsbprodncu-sb.accesscontrol.windows.net/</a>, and that the AAD admin account you are using to offboard is not federated.</span><span class="sxs-lookup"><span data-stu-id="4620b-562">To fix this, ensure that you are not blocking outbound connections over 443 or to <a href="https://ssprsbprodncu-sb.accesscontrol.windows.net/">https://ssprsbprodncu-sb.accesscontrol.windows.net/</a>, and that the AAD admin account you are using to offboard is not federated.</span></span> </p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-563">32014</span><span class="sxs-lookup"><span data-stu-id="4620b-563">32014</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-564">ServiceBusWarning</span><span class="sxs-lookup"><span data-stu-id="4620b-564">ServiceBusWarning</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-565">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-565">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-566">This event indicates that we had to retry to connect to your tenant’s service bus instance.</span><span class="sxs-lookup"><span data-stu-id="4620b-566">This event indicates that we had to retry to connect to your tenant’s service bus instance.</span></span> <span data-ttu-id="4620b-567">Under normal conditions, this should not be a concern, but if you see this event many times, consider checking your network connection to service bus, especially if it’s a high latency or low-bandwidth connection.</span><span class="sxs-lookup"><span data-stu-id="4620b-567">Under normal conditions, this should not be a concern, but if you see this event many times, consider checking your network connection to service bus, especially if it’s a high latency or low-bandwidth connection.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-568">32015</span><span class="sxs-lookup"><span data-stu-id="4620b-568">32015</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-569">ReportServiceHealthError</span><span class="sxs-lookup"><span data-stu-id="4620b-569">ReportServiceHealthError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-570">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-570">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-571">In order to monitor the health of your Password Writeback service, we send heartbeat data to our password reset web service every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="4620b-571">In order to monitor the health of your Password Writeback service, we send heartbeat data to our password reset web service every 5 minutes.</span></span> <span data-ttu-id="4620b-572">This event indicates that there was an error when sending this health information back to the cloud web service.</span><span class="sxs-lookup"><span data-stu-id="4620b-572">This event indicates that there was an error when sending this health information back to the cloud web service.</span></span> <span data-ttu-id="4620b-573">This health information does not include an OII or PII data, and is purely a heartbeat and basic service statistics so that we can provide service status information in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4620b-573">This health information does not include an OII or PII data, and is purely a heartbeat and basic service statistics so that we can provide service status information in the cloud.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-574">33001</span><span class="sxs-lookup"><span data-stu-id="4620b-574">33001</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-575">ADUnKnownError</span><span class="sxs-lookup"><span data-stu-id="4620b-575">ADUnKnownError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-576">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-576">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-577">This event indicates that there was an unknown error returned by AD, check the Azure AD Connect server event log for events from the ADSync source for more information about this error.</span><span class="sxs-lookup"><span data-stu-id="4620b-577">This event indicates that there was an unknown error returned by AD, check the Azure AD Connect server event log for events from the ADSync source for more information about this error.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-578">33002</span><span class="sxs-lookup"><span data-stu-id="4620b-578">33002</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-579">ADUserNotFoundError</span><span class="sxs-lookup"><span data-stu-id="4620b-579">ADUserNotFoundError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-580">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-580">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-581">This event indicates that the user who is trying to reset or change a password was not found in the on-premises directory.</span><span class="sxs-lookup"><span data-stu-id="4620b-581">This event indicates that the user who is trying to reset or change a password was not found in the on-premises directory.</span></span> <span data-ttu-id="4620b-582">This could occur when the user has been deleted on-premises but not in the cloud, or if there is an issue with sync. Check your sync logs, as well as the last few sync run details for more information.</span><span class="sxs-lookup"><span data-stu-id="4620b-582">This could occur when the user has been deleted on-premises but not in the cloud, or if there is an issue with sync. Check your sync logs, as well as the last few sync run details for more information.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-583">33003</span><span class="sxs-lookup"><span data-stu-id="4620b-583">33003</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-584">ADMutliMatchError</span><span class="sxs-lookup"><span data-stu-id="4620b-584">ADMutliMatchError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-585">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-585">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-586">When a password reset or change request originates from the cloud, we use the cloud anchor specified during the setup process of Azure AD Connect to determine how to link that request back to a user in your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-586">When a password reset or change request originates from the cloud, we use the cloud anchor specified during the setup process of Azure AD Connect to determine how to link that request back to a user in your on-premises environment.</span></span> <span data-ttu-id="4620b-587">This event indicates that we found two users in your on-premises directory with the same cloud anchor attribute.</span><span class="sxs-lookup"><span data-stu-id="4620b-587">This event indicates that we found two users in your on-premises directory with the same cloud anchor attribute.</span></span> <span data-ttu-id="4620b-588">Check your sync logs, as well as the last few sync run details for more information.</span><span class="sxs-lookup"><span data-stu-id="4620b-588">Check your sync logs, as well as the last few sync run details for more information.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-589">33004</span><span class="sxs-lookup"><span data-stu-id="4620b-589">33004</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-590">ADPermissionsError</span><span class="sxs-lookup"><span data-stu-id="4620b-590">ADPermissionsError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-591">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-591">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-592">This event indicates that the Management Agent service account does not have the appropriate permissions on the account in question to set a new password.</span><span class="sxs-lookup"><span data-stu-id="4620b-592">This event indicates that the Management Agent service account does not have the appropriate permissions on the account in question to set a new password.</span></span> <span data-ttu-id="4620b-593">Ensure that the MA account in the user’s forest has Reset and Change password permissions on all objects in the forest.</span><span class="sxs-lookup"><span data-stu-id="4620b-593">Ensure that the MA account in the user’s forest has Reset and Change password permissions on all objects in the forest.</span></span>  <span data-ttu-id="4620b-594">For more information on how do to this, see <a href="active-directory-passwords-getting-started.md#step-4-set-up-the-appropriate-active-directory-permissions">Step 4: Set up the appropriate Active Directory permissions</a>.</span><span class="sxs-lookup"><span data-stu-id="4620b-594">For more information on how do to this, see <a href="active-directory-passwords-getting-started.md#step-4-set-up-the-appropriate-active-directory-permissions">Step 4: Set up the appropriate Active Directory permissions</a>.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-595">33005</span><span class="sxs-lookup"><span data-stu-id="4620b-595">33005</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-596">ADUserAccountDisabled</span><span class="sxs-lookup"><span data-stu-id="4620b-596">ADUserAccountDisabled</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-597">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-597">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-598">This event indicates that we attempted to reset or change a password for an account that was disabled on premises.</span><span class="sxs-lookup"><span data-stu-id="4620b-598">This event indicates that we attempted to reset or change a password for an account that was disabled on premises.</span></span> <span data-ttu-id="4620b-599">Enable the account and try the operation again.</span><span class="sxs-lookup"><span data-stu-id="4620b-599">Enable the account and try the operation again.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-600">33006</span><span class="sxs-lookup"><span data-stu-id="4620b-600">33006</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-601">ADUserAccountLockedOut</span><span class="sxs-lookup"><span data-stu-id="4620b-601">ADUserAccountLockedOut</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-602">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-602">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-603">Event indicates that we attempted to reset or change a password for an account that was locked out on premises.</span><span class="sxs-lookup"><span data-stu-id="4620b-603">Event indicates that we attempted to reset or change a password for an account that was locked out on premises.</span></span> <span data-ttu-id="4620b-604">Lockouts can occur when a user has tried a change or reset password operation too many times in a short period.</span><span class="sxs-lookup"><span data-stu-id="4620b-604">Lockouts can occur when a user has tried a change or reset password operation too many times in a short period.</span></span> <span data-ttu-id="4620b-605">Unlock the account and try the operation again.</span><span class="sxs-lookup"><span data-stu-id="4620b-605">Unlock the account and try the operation again.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-606">33007</span><span class="sxs-lookup"><span data-stu-id="4620b-606">33007</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-607">ADUserIncorrectPassword</span><span class="sxs-lookup"><span data-stu-id="4620b-607">ADUserIncorrectPassword</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-608">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-608">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-609">This event indicates that the user specified an incorrect current password when performing a password change operation.</span><span class="sxs-lookup"><span data-stu-id="4620b-609">This event indicates that the user specified an incorrect current password when performing a password change operation.</span></span> <span data-ttu-id="4620b-610">Specify the correct current password and try again.</span><span class="sxs-lookup"><span data-stu-id="4620b-610">Specify the correct current password and try again.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-611">33008</span><span class="sxs-lookup"><span data-stu-id="4620b-611">33008</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-612">ADPasswordPolicyError</span><span class="sxs-lookup"><span data-stu-id="4620b-612">ADPasswordPolicyError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-613">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-613">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-614">This event occurs when the Password Writeback service attempts to set a password on your local directory which does not meet the password age, history, complexity, or filtering requirements of the domain.</span><span class="sxs-lookup"><span data-stu-id="4620b-614">This event occurs when the Password Writeback service attempts to set a password on your local directory which does not meet the password age, history, complexity, or filtering requirements of the domain.</span></span></p>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-615">If you have a minimum password age, and have recently changed the password within that window of time, you will not be able to change the password again until it reaches the specified age in your domain.</span><span class="sxs-lookup"><span data-stu-id="4620b-615">If you have a minimum password age, and have recently changed the password within that window of time, you will not be able to change the password again until it reaches the specified age in your domain.</span></span> <span data-ttu-id="4620b-616">For testing purposes, minimum age should be set to 0.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-616">For testing purposes, minimum age should be set to 0.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-617">If you have password history requirements enabled, then you must select a password that has not been used in the last N times, where N is the password history setting.</span><span class="sxs-lookup"><span data-stu-id="4620b-617">If you have password history requirements enabled, then you must select a password that has not been used in the last N times, where N is the password history setting.</span></span> <span data-ttu-id="4620b-618">If you do select a password that has been used in the last N times, then you will see a failure in this case.</span><span class="sxs-lookup"><span data-stu-id="4620b-618">If you do select a password that has been used in the last N times, then you will see a failure in this case.</span></span> <span data-ttu-id="4620b-619">For testing purposes, history should be set to 0.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-619">For testing purposes, history should be set to 0.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-620">If you have password complexity requirements, all of them will be enforced when the user attempts to change or reset a password.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-620">If you have password complexity requirements, all of them will be enforced when the user attempts to change or reset a password.<br\><br\></span></span></li>
              </ul>
              <ul>
                <li class="unordered">
<span data-ttu-id="4620b-621">If you have password filters enabled, and a user selects a password which does not meet the filtering criteria, then the reset or change operation will fail.<br\><br\></span><span class="sxs-lookup"><span data-stu-id="4620b-621">If you have password filters enabled, and a user selects a password which does not meet the filtering criteria, then the reset or change operation will fail.<br\><br\></span></span></li>
              </ul>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-622">33009</span><span class="sxs-lookup"><span data-stu-id="4620b-622">33009</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-623">ADConfigurationError</span><span class="sxs-lookup"><span data-stu-id="4620b-623">ADConfigurationError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-624">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-624">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-625">This event indicates there was an issue writing a password back to your on-premises directory due to a configuration issue with Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4620b-625">This event indicates there was an issue writing a password back to your on-premises directory due to a configuration issue with Active Directory.</span></span> <span data-ttu-id="4620b-626">Check the Azure AD Connect machine’s Application event log for messages from the ADSync service for more information on what error occurred.</span><span class="sxs-lookup"><span data-stu-id="4620b-626">Check the Azure AD Connect machine’s Application event log for messages from the ADSync service for more information on what error occurred.</span></span> </p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-627">34001</span><span class="sxs-lookup"><span data-stu-id="4620b-627">34001</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-628">ADPasswordPolicyOrPermissionError</span><span class="sxs-lookup"><span data-stu-id="4620b-628">ADPasswordPolicyOrPermissionError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-629">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-629">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-630">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-630">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-631">34002</span><span class="sxs-lookup"><span data-stu-id="4620b-631">34002</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-632">ADNotReachableError</span><span class="sxs-lookup"><span data-stu-id="4620b-632">ADNotReachableError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-633">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-633">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-634">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-634">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span></span></p>
            </td>
          </tr>
          <tr>
            <td>
              <p><span data-ttu-id="4620b-635">34003</span><span class="sxs-lookup"><span data-stu-id="4620b-635">34003</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-636">ADInvalidAnchorError</span><span class="sxs-lookup"><span data-stu-id="4620b-636">ADInvalidAnchorError</span></span> </p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-637">PasswordResetService</span><span class="sxs-lookup"><span data-stu-id="4620b-637">PasswordResetService</span></span></p>
            </td>
            <td>
              <p><span data-ttu-id="4620b-638">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span><span class="sxs-lookup"><span data-stu-id="4620b-638">DEPRECATED – This event is not present in Azure AD Connect, only very early builds of DirSync which supported writeback.</span></span></p>
            </td>
          </tr>
        </tbody></table>

## <a name="troubleshoot-password-writeback-connectivity"></a><span data-ttu-id="4620b-639">Troubleshoot Password Writeback connectivity</span><span class="sxs-lookup"><span data-stu-id="4620b-639">Troubleshoot Password Writeback connectivity</span></span>
<span data-ttu-id="4620b-640">If you are experiencing service interruptions with the Password Writeback component of Azure AD Connect, here are some quick steps you can take to resolve this:</span><span class="sxs-lookup"><span data-stu-id="4620b-640">If you are experiencing service interruptions with the Password Writeback component of Azure AD Connect, here are some quick steps you can take to resolve this:</span></span>

* [<span data-ttu-id="4620b-641">Restart the Azure AD Connect Sync Service</span><span class="sxs-lookup"><span data-stu-id="4620b-641">Restart the Azure AD Connect Sync Service</span></span>](#restart-the-azure-AD-Connect-sync-service)
* [<span data-ttu-id="4620b-642">Disable and re-enable the Password Writeback feature</span><span class="sxs-lookup"><span data-stu-id="4620b-642">Disable and re-enable the Password Writeback feature</span></span>](#disable-and-re-enable-the-password-writeback-feature)
* [<span data-ttu-id="4620b-643">Install the latest Azure AD Connect release</span><span class="sxs-lookup"><span data-stu-id="4620b-643">Install the latest Azure AD Connect release</span></span>](#install-the-latest-azure-ad-connect-release)
* [<span data-ttu-id="4620b-644">Troubleshoot Password Writeback</span><span class="sxs-lookup"><span data-stu-id="4620b-644">Troubleshoot Password Writeback</span></span>](#troubleshoot-password-writeback)

<span data-ttu-id="4620b-645">In general, we recommend that you execute these steps in the order above in order to recover your service in the most rapid manner.</span><span class="sxs-lookup"><span data-stu-id="4620b-645">In general, we recommend that you execute these steps in the order above in order to recover your service in the most rapid manner.</span></span>

### <a name="restart-the-azure-ad-connect-sync-service"></a><span data-ttu-id="4620b-646">Restart the Azure AD Connect Sync Service</span><span class="sxs-lookup"><span data-stu-id="4620b-646">Restart the Azure AD Connect Sync Service</span></span>
<span data-ttu-id="4620b-647">Restarting the Azure AD Connect Sync Service can help to resolve connectivity issues or other transient issues with the service.</span><span class="sxs-lookup"><span data-stu-id="4620b-647">Restarting the Azure AD Connect Sync Service can help to resolve connectivity issues or other transient issues with the service.</span></span>

1. <span data-ttu-id="4620b-648">As an administrator, click **Start** on the server running **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="4620b-648">As an administrator, click **Start** on the server running **Azure AD Connect**.</span></span>
2. <span data-ttu-id="4620b-649">Type **“services.msc”** in the search box and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4620b-649">Type **“services.msc”** in the search box and press **Enter**.</span></span>
3. <span data-ttu-id="4620b-650">Look for the **Microsoft Azure AD Connect** entry.</span><span class="sxs-lookup"><span data-stu-id="4620b-650">Look for the **Microsoft Azure AD Connect** entry.</span></span>
4. <span data-ttu-id="4620b-651">Right-click on the service entry, click **Restart**, and wait for the operation to complete.</span><span class="sxs-lookup"><span data-stu-id="4620b-651">Right-click on the service entry, click **Restart**, and wait for the operation to complete.</span></span>

   ![][002]

<span data-ttu-id="4620b-652">These steps will re-establish your connection with the cloud service and resolve any interruptions you may be experiencing.</span><span class="sxs-lookup"><span data-stu-id="4620b-652">These steps will re-establish your connection with the cloud service and resolve any interruptions you may be experiencing.</span></span>  <span data-ttu-id="4620b-653">If restarting the Sync Service does not resolve your issue, we recommend that you try to disable and re-enable the Password Writeback feature as a next step.</span><span class="sxs-lookup"><span data-stu-id="4620b-653">If restarting the Sync Service does not resolve your issue, we recommend that you try to disable and re-enable the Password Writeback feature as a next step.</span></span>

### <a name="disable-and-re-enable-the-password-writeback-feature"></a><span data-ttu-id="4620b-654">Disable and re-enable the Password Writeback feature</span><span class="sxs-lookup"><span data-stu-id="4620b-654">Disable and re-enable the Password Writeback feature</span></span>
<span data-ttu-id="4620b-655">Disabling and re-enabling the Password Writeback feature can help to resolve connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="4620b-655">Disabling and re-enabling the Password Writeback feature can help to resolve connectivity issues.</span></span>

1. <span data-ttu-id="4620b-656">As an administrator, open the **Azure AD Connect configuration wizard**.</span><span class="sxs-lookup"><span data-stu-id="4620b-656">As an administrator, open the **Azure AD Connect configuration wizard**.</span></span>
2. <span data-ttu-id="4620b-657">On the **Connect to Azure AD** dialog, enter your **Azure AD global admin credentials**</span><span class="sxs-lookup"><span data-stu-id="4620b-657">On the **Connect to Azure AD** dialog, enter your **Azure AD global admin credentials**</span></span>
3. <span data-ttu-id="4620b-658">On the **Connect to AD DS** dialog, enter your **AD Domain Services admin credentials**.</span><span class="sxs-lookup"><span data-stu-id="4620b-658">On the **Connect to AD DS** dialog, enter your **AD Domain Services admin credentials**.</span></span>
4. <span data-ttu-id="4620b-659">On the **Uniquely identifying your users** dialog, click the **Next** button.</span><span class="sxs-lookup"><span data-stu-id="4620b-659">On the **Uniquely identifying your users** dialog, click the **Next** button.</span></span>
5. <span data-ttu-id="4620b-660">On the **Optional features** dialog, uncheck the **Password write-back** checkbox.</span><span class="sxs-lookup"><span data-stu-id="4620b-660">On the **Optional features** dialog, uncheck the **Password write-back** checkbox.</span></span>

   ![][003]
6. <span data-ttu-id="4620b-661">Click **Next** through the remaining dialog pages without changing anything until you get to the **Ready to configure** page.</span><span class="sxs-lookup"><span data-stu-id="4620b-661">Click **Next** through the remaining dialog pages without changing anything until you get to the **Ready to configure** page.</span></span>
7. <span data-ttu-id="4620b-662">Ensure that the configure page shows the **Password write-back option as disabled** and then click the green **Configure** button to commit your changes.</span><span class="sxs-lookup"><span data-stu-id="4620b-662">Ensure that the configure page shows the **Password write-back option as disabled** and then click the green **Configure** button to commit your changes.</span></span>
8. <span data-ttu-id="4620b-663">On the **Finished** dialog, deselect the **Synchronize now** option, and then click **Finish** to close the wizard.</span><span class="sxs-lookup"><span data-stu-id="4620b-663">On the **Finished** dialog, deselect the **Synchronize now** option, and then click **Finish** to close the wizard.</span></span>
9. <span data-ttu-id="4620b-664">Re-open the **Azure AD Connect configuration wizard**.</span><span class="sxs-lookup"><span data-stu-id="4620b-664">Re-open the **Azure AD Connect configuration wizard**.</span></span>
10. <span data-ttu-id="4620b-665">**Repeat steps 2-8**, except ensure you **check the Password write-back option** on the **Optional features** screen to re-enable the service.</span><span class="sxs-lookup"><span data-stu-id="4620b-665">**Repeat steps 2-8**, except ensure you **check the Password write-back option** on the **Optional features** screen to re-enable the service.</span></span>

    ![][004]

<span data-ttu-id="4620b-666">These steps will re-establish your connection with our cloud service and resolve any interruptions you may be experiencing.</span><span class="sxs-lookup"><span data-stu-id="4620b-666">These steps will re-establish your connection with our cloud service and resolve any interruptions you may be experiencing.</span></span>

<span data-ttu-id="4620b-667">If disabling and re-enabling the Password Writeback feature does not resolve your issue, we recommend that you try to re-install Azure AD Connect as a next step.</span><span class="sxs-lookup"><span data-stu-id="4620b-667">If disabling and re-enabling the Password Writeback feature does not resolve your issue, we recommend that you try to re-install Azure AD Connect as a next step.</span></span>

### <a name="install-the-latest-azure-ad-connect-release"></a><span data-ttu-id="4620b-668">Install the latest Azure AD Connect release</span><span class="sxs-lookup"><span data-stu-id="4620b-668">Install the latest Azure AD Connect release</span></span>
<span data-ttu-id="4620b-669">Re-installing the Azure AD Connect package will resolve any configuration issues which may be affecting your ability to either connect to our cloud services or to manage passwords in your local AD environment.</span><span class="sxs-lookup"><span data-stu-id="4620b-669">Re-installing the Azure AD Connect package will resolve any configuration issues which may be affecting your ability to either connect to our cloud services or to manage passwords in your local AD environment.</span></span>
<span data-ttu-id="4620b-670">We recommend, you perform this step only after attempting the first two steps described above.</span><span class="sxs-lookup"><span data-stu-id="4620b-670">We recommend, you perform this step only after attempting the first two steps described above.</span></span>

1. <span data-ttu-id="4620b-671">Download the latest version of Azure AD Connect [here](connect/active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="4620b-671">Download the latest version of Azure AD Connect [here](connect/active-directory-aadconnect.md#install-azure-ad-connect).</span></span>
2. <span data-ttu-id="4620b-672">Since you have already installed Azure AD Connect, you will only need to perform an in-place upgrade to update your Azure AD Connect installation to the latest version.</span><span class="sxs-lookup"><span data-stu-id="4620b-672">Since you have already installed Azure AD Connect, you will only need to perform an in-place upgrade to update your Azure AD Connect installation to the latest version.</span></span>
3. <span data-ttu-id="4620b-673">Execute the downloaded package and follow the on-screen instructions to update your Azure AD Connect machine.</span><span class="sxs-lookup"><span data-stu-id="4620b-673">Execute the downloaded package and follow the on-screen instructions to update your Azure AD Connect machine.</span></span>  <span data-ttu-id="4620b-674">No additional manual steps are required unless you have customized the out of box sync rules, in which case you should **back these up before proceeding with upgrade and manually re-deploy them after you are finished**.</span><span class="sxs-lookup"><span data-stu-id="4620b-674">No additional manual steps are required unless you have customized the out of box sync rules, in which case you should **back these up before proceeding with upgrade and manually re-deploy them after you are finished**.</span></span>

<span data-ttu-id="4620b-675">These steps will re-establish your connection with our cloud service and resolve any interruptions you may be experiencing.</span><span class="sxs-lookup"><span data-stu-id="4620b-675">These steps will re-establish your connection with our cloud service and resolve any interruptions you may be experiencing.</span></span>

<span data-ttu-id="4620b-676">If installing the latest version of the Azure AD Connect server does not resolve your issue, we recommend that you try disabling and re-enabling Password Writeback as a final step after installing the latest sync QFE.</span><span class="sxs-lookup"><span data-stu-id="4620b-676">If installing the latest version of the Azure AD Connect server does not resolve your issue, we recommend that you try disabling and re-enabling Password Writeback as a final step after installing the latest sync QFE.</span></span>

<span data-ttu-id="4620b-677">If that does not resolve your issue, then we recommend that you take a look at [Troubleshoot Password Writeback](#troubleshoot-password-writeback) and the [Azure AD password Management FAQ](active-directory-passwords-faq.md) to see if your issue may be discussed there.</span><span class="sxs-lookup"><span data-stu-id="4620b-677">If that does not resolve your issue, then we recommend that you take a look at [Troubleshoot Password Writeback](#troubleshoot-password-writeback) and the [Azure AD password Management FAQ](active-directory-passwords-faq.md) to see if your issue may be discussed there.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4620b-678">Next steps</span><span class="sxs-lookup"><span data-stu-id="4620b-678">Next steps</span></span>
<span data-ttu-id="4620b-679">Below are links to all of the Azure AD Password Reset documentation pages:</span><span class="sxs-lookup"><span data-stu-id="4620b-679">Below are links to all of the Azure AD Password Reset documentation pages:</span></span>

* <span data-ttu-id="4620b-680">**Are you here because you're having problems signing in?**</span><span class="sxs-lookup"><span data-stu-id="4620b-680">**Are you here because you're having problems signing in?**</span></span> <span data-ttu-id="4620b-681">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span><span class="sxs-lookup"><span data-stu-id="4620b-681">If so, [here's how you can change and reset your own password](active-directory-passwords-update-your-own-password.md#reset-my-password).</span></span>
* <span data-ttu-id="4620b-682">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span><span class="sxs-lookup"><span data-stu-id="4620b-682">[**How it works**](active-directory-passwords-how-it-works.md) - learn about the six different components of the service and what each does</span></span>
* <span data-ttu-id="4620b-683">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span><span class="sxs-lookup"><span data-stu-id="4620b-683">[**Getting started**](active-directory-passwords-getting-started.md) - learn how to allow you users to reset and change their cloud or on-premises passwords</span></span>
* <span data-ttu-id="4620b-684">[**Customize**](active-directory-passwords-customize.md) - learn how to customize the look & feel and behavior of the service to your organization's needs</span><span class="sxs-lookup"><span data-stu-id="4620b-684">[**Customize**](active-directory-passwords-customize.md) - learn how to customize the look & feel and behavior of the service to your organization's needs</span></span>
* <span data-ttu-id="4620b-685">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span><span class="sxs-lookup"><span data-stu-id="4620b-685">[**Best practices**](active-directory-passwords-best-practices.md) - learn how to quickly deploy and effectively manage passwords in your organization</span></span>
* <span data-ttu-id="4620b-686">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span><span class="sxs-lookup"><span data-stu-id="4620b-686">[**Get insights**](active-directory-passwords-get-insights.md) - learn about our integrated reporting capabilities</span></span>
* <span data-ttu-id="4620b-687">[**FAQ**](active-directory-passwords-faq.md) - get answers to frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="4620b-687">[**FAQ**](active-directory-passwords-faq.md) - get answers to frequently asked questions</span></span>
* <span data-ttu-id="4620b-688">[**Learn more**](active-directory-passwords-learn-more.md) - go deep into the technical details of how the service works</span><span class="sxs-lookup"><span data-stu-id="4620b-688">[**Learn more**](active-directory-passwords-learn-more.md) - go deep into the technical details of how the service works</span></span>

[001]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-troubleshoot/001.jpg "Image_001.jpg"
[002]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-troubleshoot/002.jpg "Image_002.jpg"
[003]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-troubleshoot/003.jpg "Image_003.jpg"
[004]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-passwords-troubleshoot/004.jpg "Image_004.jpg"




