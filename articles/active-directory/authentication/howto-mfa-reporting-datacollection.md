---
title: Azure Multi-Factor Authentication user data collection
description: What information is used to help authenticate users by Azure Multi-Factor Authentication?
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: 1b380bc20c9f80710ca62672b99649ce3498a8e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871473"
---
# <a name="azure-multi-factor-authentication-user-data-collection"></a><span data-ttu-id="8bd73-103">Azure Multi-Factor Authentication user data collection</span><span class="sxs-lookup"><span data-stu-id="8bd73-103">Azure Multi-Factor Authentication user data collection</span></span>

<span data-ttu-id="8bd73-104">This document explains how to find user information collected by Azure Multi-Factor Authentication Server (MFA Server) and Azure MFA (Cloud-based) in the event you would like to remove it.</span><span class="sxs-lookup"><span data-stu-id="8bd73-104">This document explains how to find user information collected by Azure Multi-Factor Authentication Server (MFA Server) and Azure MFA (Cloud-based) in the event you would like to remove it.</span></span>

[!INCLUDE [gdpr-hybrid-note](../../../includes/gdpr-hybrid-note.md)]

## <a name="information-collected"></a><span data-ttu-id="8bd73-105">Information collected</span><span class="sxs-lookup"><span data-stu-id="8bd73-105">Information collected</span></span>

<span data-ttu-id="8bd73-106">MFA Server, the NPS Extension, and the Windows Server 2016 Azure MFA AD FS Adapter collect and store the following information for 90 days.</span><span class="sxs-lookup"><span data-stu-id="8bd73-106">MFA Server, the NPS Extension, and the Windows Server 2016 Azure MFA AD FS Adapter collect and store the following information for 90 days.</span></span>

<span data-ttu-id="8bd73-107">Authentication Attempts (used for reporting and troubleshooting):</span><span class="sxs-lookup"><span data-stu-id="8bd73-107">Authentication Attempts (used for reporting and troubleshooting):</span></span>

- <span data-ttu-id="8bd73-108">Timestamp</span><span class="sxs-lookup"><span data-stu-id="8bd73-108">Timestamp</span></span>
- <span data-ttu-id="8bd73-109">Username</span><span class="sxs-lookup"><span data-stu-id="8bd73-109">Username</span></span>
- <span data-ttu-id="8bd73-110">First Name</span><span class="sxs-lookup"><span data-stu-id="8bd73-110">First Name</span></span>
- <span data-ttu-id="8bd73-111">Last Name</span><span class="sxs-lookup"><span data-stu-id="8bd73-111">Last Name</span></span>
- <span data-ttu-id="8bd73-112">Email Address</span><span class="sxs-lookup"><span data-stu-id="8bd73-112">Email Address</span></span>
- <span data-ttu-id="8bd73-113">User Group</span><span class="sxs-lookup"><span data-stu-id="8bd73-113">User Group</span></span>
- <span data-ttu-id="8bd73-114">Authentication Method (Phone Call, Text Message, Mobile App, OATH Token)</span><span class="sxs-lookup"><span data-stu-id="8bd73-114">Authentication Method (Phone Call, Text Message, Mobile App, OATH Token)</span></span>
- <span data-ttu-id="8bd73-115">Phone Call Mode (Standard, PIN)</span><span class="sxs-lookup"><span data-stu-id="8bd73-115">Phone Call Mode (Standard, PIN)</span></span>
- <span data-ttu-id="8bd73-116">Text Message Direction (One-Way, Two-Way)</span><span class="sxs-lookup"><span data-stu-id="8bd73-116">Text Message Direction (One-Way, Two-Way)</span></span>
- <span data-ttu-id="8bd73-117">Text Message Mode (OTP, OTP + PIN)</span><span class="sxs-lookup"><span data-stu-id="8bd73-117">Text Message Mode (OTP, OTP + PIN)</span></span>
- <span data-ttu-id="8bd73-118">Mobile App Mode (Standard, PIN)</span><span class="sxs-lookup"><span data-stu-id="8bd73-118">Mobile App Mode (Standard, PIN)</span></span>
- <span data-ttu-id="8bd73-119">OATH Token Mode (Standard, PIN)</span><span class="sxs-lookup"><span data-stu-id="8bd73-119">OATH Token Mode (Standard, PIN)</span></span>
- <span data-ttu-id="8bd73-120">Authentication Type</span><span class="sxs-lookup"><span data-stu-id="8bd73-120">Authentication Type</span></span>
- <span data-ttu-id="8bd73-121">Application Name</span><span class="sxs-lookup"><span data-stu-id="8bd73-121">Application Name</span></span>
- <span data-ttu-id="8bd73-122">Primary Call Country Code</span><span class="sxs-lookup"><span data-stu-id="8bd73-122">Primary Call Country Code</span></span>
- <span data-ttu-id="8bd73-123">Primary Call Phone Number</span><span class="sxs-lookup"><span data-stu-id="8bd73-123">Primary Call Phone Number</span></span>
- <span data-ttu-id="8bd73-124">Primary Call Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-124">Primary Call Extension</span></span>
- <span data-ttu-id="8bd73-125">Primary Call Authenticated</span><span class="sxs-lookup"><span data-stu-id="8bd73-125">Primary Call Authenticated</span></span>
- <span data-ttu-id="8bd73-126">Primary Call Result</span><span class="sxs-lookup"><span data-stu-id="8bd73-126">Primary Call Result</span></span>
- <span data-ttu-id="8bd73-127">Backup Call Country Code</span><span class="sxs-lookup"><span data-stu-id="8bd73-127">Backup Call Country Code</span></span>
- <span data-ttu-id="8bd73-128">Backup Call Phone Number</span><span class="sxs-lookup"><span data-stu-id="8bd73-128">Backup Call Phone Number</span></span>
- <span data-ttu-id="8bd73-129">Backup Call Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-129">Backup Call Extension</span></span>
- <span data-ttu-id="8bd73-130">Backup Call Authenticated</span><span class="sxs-lookup"><span data-stu-id="8bd73-130">Backup Call Authenticated</span></span>
- <span data-ttu-id="8bd73-131">Backup Call Result</span><span class="sxs-lookup"><span data-stu-id="8bd73-131">Backup Call Result</span></span>
- <span data-ttu-id="8bd73-132">Overall Authenticated</span><span class="sxs-lookup"><span data-stu-id="8bd73-132">Overall Authenticated</span></span>
- <span data-ttu-id="8bd73-133">Overall Result</span><span class="sxs-lookup"><span data-stu-id="8bd73-133">Overall Result</span></span>
- <span data-ttu-id="8bd73-134">Results</span><span class="sxs-lookup"><span data-stu-id="8bd73-134">Results</span></span>
- <span data-ttu-id="8bd73-135">Authenticated</span><span class="sxs-lookup"><span data-stu-id="8bd73-135">Authenticated</span></span>
- <span data-ttu-id="8bd73-136">Result</span><span class="sxs-lookup"><span data-stu-id="8bd73-136">Result</span></span>
- <span data-ttu-id="8bd73-137">Initiating IP Address</span><span class="sxs-lookup"><span data-stu-id="8bd73-137">Initiating IP Address</span></span>
- <span data-ttu-id="8bd73-138">Devices</span><span class="sxs-lookup"><span data-stu-id="8bd73-138">Devices</span></span>
- <span data-ttu-id="8bd73-139">Device Token</span><span class="sxs-lookup"><span data-stu-id="8bd73-139">Device Token</span></span>
- <span data-ttu-id="8bd73-140">Device Type</span><span class="sxs-lookup"><span data-stu-id="8bd73-140">Device Type</span></span>
- <span data-ttu-id="8bd73-141">Mobile App Version</span><span class="sxs-lookup"><span data-stu-id="8bd73-141">Mobile App Version</span></span>
- <span data-ttu-id="8bd73-142">OS Version</span><span class="sxs-lookup"><span data-stu-id="8bd73-142">OS Version</span></span>
- <span data-ttu-id="8bd73-143">Result</span><span class="sxs-lookup"><span data-stu-id="8bd73-143">Result</span></span>
- <span data-ttu-id="8bd73-144">Used Check for Notification</span><span class="sxs-lookup"><span data-stu-id="8bd73-144">Used Check for Notification</span></span>

<span data-ttu-id="8bd73-145">Activations (attempts to activate an account in the Microsoft Authenticator mobile app):</span><span class="sxs-lookup"><span data-stu-id="8bd73-145">Activations (attempts to activate an account in the Microsoft Authenticator mobile app):</span></span>
- <span data-ttu-id="8bd73-146">Username</span><span class="sxs-lookup"><span data-stu-id="8bd73-146">Username</span></span>
- <span data-ttu-id="8bd73-147">Account Name</span><span class="sxs-lookup"><span data-stu-id="8bd73-147">Account Name</span></span>
- <span data-ttu-id="8bd73-148">Timestamp</span><span class="sxs-lookup"><span data-stu-id="8bd73-148">Timestamp</span></span>
- <span data-ttu-id="8bd73-149">Get Activation Code Result</span><span class="sxs-lookup"><span data-stu-id="8bd73-149">Get Activation Code Result</span></span>
- <span data-ttu-id="8bd73-150">Activate Success</span><span class="sxs-lookup"><span data-stu-id="8bd73-150">Activate Success</span></span>
- <span data-ttu-id="8bd73-151">Activate Error</span><span class="sxs-lookup"><span data-stu-id="8bd73-151">Activate Error</span></span>
- <span data-ttu-id="8bd73-152">Activation Status Result</span><span class="sxs-lookup"><span data-stu-id="8bd73-152">Activation Status Result</span></span>
- <span data-ttu-id="8bd73-153">Device  Name</span><span class="sxs-lookup"><span data-stu-id="8bd73-153">Device  Name</span></span>
- <span data-ttu-id="8bd73-154">Device Type</span><span class="sxs-lookup"><span data-stu-id="8bd73-154">Device Type</span></span>
- <span data-ttu-id="8bd73-155">App Version</span><span class="sxs-lookup"><span data-stu-id="8bd73-155">App Version</span></span>
- <span data-ttu-id="8bd73-156">OATH Token Enabled</span><span class="sxs-lookup"><span data-stu-id="8bd73-156">OATH Token Enabled</span></span>

<span data-ttu-id="8bd73-157">Blocks (used to determine blocked state and for reporting):</span><span class="sxs-lookup"><span data-stu-id="8bd73-157">Blocks (used to determine blocked state and for reporting):</span></span>

- <span data-ttu-id="8bd73-158">Block Timestamp</span><span class="sxs-lookup"><span data-stu-id="8bd73-158">Block Timestamp</span></span>
- <span data-ttu-id="8bd73-159">Block By Username</span><span class="sxs-lookup"><span data-stu-id="8bd73-159">Block By Username</span></span>
- <span data-ttu-id="8bd73-160">Username</span><span class="sxs-lookup"><span data-stu-id="8bd73-160">Username</span></span>
- <span data-ttu-id="8bd73-161">Country Code</span><span class="sxs-lookup"><span data-stu-id="8bd73-161">Country Code</span></span>
- <span data-ttu-id="8bd73-162">Phone Number</span><span class="sxs-lookup"><span data-stu-id="8bd73-162">Phone Number</span></span>
- <span data-ttu-id="8bd73-163">Phone Number Formatted</span><span class="sxs-lookup"><span data-stu-id="8bd73-163">Phone Number Formatted</span></span>
- <span data-ttu-id="8bd73-164">Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-164">Extension</span></span>
- <span data-ttu-id="8bd73-165">Clean Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-165">Clean Extension</span></span>
- <span data-ttu-id="8bd73-166">Blocked</span><span class="sxs-lookup"><span data-stu-id="8bd73-166">Blocked</span></span>
- <span data-ttu-id="8bd73-167">Block Reason</span><span class="sxs-lookup"><span data-stu-id="8bd73-167">Block Reason</span></span>
- <span data-ttu-id="8bd73-168">Completion Timestamp</span><span class="sxs-lookup"><span data-stu-id="8bd73-168">Completion Timestamp</span></span>
- <span data-ttu-id="8bd73-169">Completion Reason</span><span class="sxs-lookup"><span data-stu-id="8bd73-169">Completion Reason</span></span>
- <span data-ttu-id="8bd73-170">Account Lockout</span><span class="sxs-lookup"><span data-stu-id="8bd73-170">Account Lockout</span></span>
- <span data-ttu-id="8bd73-171">Fraud Alert</span><span class="sxs-lookup"><span data-stu-id="8bd73-171">Fraud Alert</span></span>
- <span data-ttu-id="8bd73-172">Fraud Alert Not Blocked</span><span class="sxs-lookup"><span data-stu-id="8bd73-172">Fraud Alert Not Blocked</span></span>
- <span data-ttu-id="8bd73-173">Language</span><span class="sxs-lookup"><span data-stu-id="8bd73-173">Language</span></span>

<span data-ttu-id="8bd73-174">Bypasses (used for reporting):</span><span class="sxs-lookup"><span data-stu-id="8bd73-174">Bypasses (used for reporting):</span></span>

- <span data-ttu-id="8bd73-175">Bypass Timestamp</span><span class="sxs-lookup"><span data-stu-id="8bd73-175">Bypass Timestamp</span></span>
- <span data-ttu-id="8bd73-176">Bypass Seconds</span><span class="sxs-lookup"><span data-stu-id="8bd73-176">Bypass Seconds</span></span>
- <span data-ttu-id="8bd73-177">Bypass By Username</span><span class="sxs-lookup"><span data-stu-id="8bd73-177">Bypass By Username</span></span>
- <span data-ttu-id="8bd73-178">Username</span><span class="sxs-lookup"><span data-stu-id="8bd73-178">Username</span></span>
- <span data-ttu-id="8bd73-179">Country Code</span><span class="sxs-lookup"><span data-stu-id="8bd73-179">Country Code</span></span>
- <span data-ttu-id="8bd73-180">Phone Number</span><span class="sxs-lookup"><span data-stu-id="8bd73-180">Phone Number</span></span>
- <span data-ttu-id="8bd73-181">Phone Number Formatted</span><span class="sxs-lookup"><span data-stu-id="8bd73-181">Phone Number Formatted</span></span>
- <span data-ttu-id="8bd73-182">Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-182">Extension</span></span>
- <span data-ttu-id="8bd73-183">Clean Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-183">Clean Extension</span></span>
- <span data-ttu-id="8bd73-184">Bypass Reason</span><span class="sxs-lookup"><span data-stu-id="8bd73-184">Bypass Reason</span></span>
- <span data-ttu-id="8bd73-185">Completion Timestamp</span><span class="sxs-lookup"><span data-stu-id="8bd73-185">Completion Timestamp</span></span>
- <span data-ttu-id="8bd73-186">Completion Reason</span><span class="sxs-lookup"><span data-stu-id="8bd73-186">Completion Reason</span></span>
- <span data-ttu-id="8bd73-187">Bypass Used</span><span class="sxs-lookup"><span data-stu-id="8bd73-187">Bypass Used</span></span>

<span data-ttu-id="8bd73-188">Changes (used to sync user changes to MFA Server or AAD):</span><span class="sxs-lookup"><span data-stu-id="8bd73-188">Changes (used to sync user changes to MFA Server or AAD):</span></span>

- <span data-ttu-id="8bd73-189">Change Timestamp</span><span class="sxs-lookup"><span data-stu-id="8bd73-189">Change Timestamp</span></span>
- <span data-ttu-id="8bd73-190">Username</span><span class="sxs-lookup"><span data-stu-id="8bd73-190">Username</span></span>
- <span data-ttu-id="8bd73-191">New Country Code</span><span class="sxs-lookup"><span data-stu-id="8bd73-191">New Country Code</span></span>
- <span data-ttu-id="8bd73-192">New Phone Number</span><span class="sxs-lookup"><span data-stu-id="8bd73-192">New Phone Number</span></span>
- <span data-ttu-id="8bd73-193">New Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-193">New Extension</span></span>
- <span data-ttu-id="8bd73-194">New Backup Country Code</span><span class="sxs-lookup"><span data-stu-id="8bd73-194">New Backup Country Code</span></span>
- <span data-ttu-id="8bd73-195">New Backup Phone Number</span><span class="sxs-lookup"><span data-stu-id="8bd73-195">New Backup Phone Number</span></span>
- <span data-ttu-id="8bd73-196">New Backup Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-196">New Backup Extension</span></span>
- <span data-ttu-id="8bd73-197">New PIN</span><span class="sxs-lookup"><span data-stu-id="8bd73-197">New PIN</span></span>
- <span data-ttu-id="8bd73-198">PIN Change Required</span><span class="sxs-lookup"><span data-stu-id="8bd73-198">PIN Change Required</span></span>
- <span data-ttu-id="8bd73-199">Old Device Token</span><span class="sxs-lookup"><span data-stu-id="8bd73-199">Old Device Token</span></span>
- <span data-ttu-id="8bd73-200">New Device Token</span><span class="sxs-lookup"><span data-stu-id="8bd73-200">New Device Token</span></span>

## <a name="gather-data-from-mfa-server"></a><span data-ttu-id="8bd73-201">Gather data from MFA Server</span><span class="sxs-lookup"><span data-stu-id="8bd73-201">Gather data from MFA Server</span></span>

<span data-ttu-id="8bd73-202">For MFA Server version 8.0 or higher the following process allows administrators to export all data for users:</span><span class="sxs-lookup"><span data-stu-id="8bd73-202">For MFA Server version 8.0 or higher the following process allows administrators to export all data for users:</span></span>

- <span data-ttu-id="8bd73-203">Log in to your MFA Server, navigate to the **Users** tab, select the user in question, and click the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="8bd73-203">Log in to your MFA Server, navigate to the **Users** tab, select the user in question, and click the **Edit** button.</span></span> <span data-ttu-id="8bd73-204">Take screenshots (Alt-PrtScn) of each tab to provide the user their current MFA settings.</span><span class="sxs-lookup"><span data-stu-id="8bd73-204">Take screenshots (Alt-PrtScn) of each tab to provide the user their current MFA settings.</span></span>
- <span data-ttu-id="8bd73-205">From the command line of the MFA Server, run the following command changing the path according to your installation `C:\Program Files\Multi-Factor Authentication Server\MultiFactorAuthGdpr.exe export <username>` to produce a JSON formatted file.</span><span class="sxs-lookup"><span data-stu-id="8bd73-205">From the command line of the MFA Server, run the following command changing the path according to your installation `C:\Program Files\Multi-Factor Authentication Server\MultiFactorAuthGdpr.exe export <username>` to produce a JSON formatted file.</span></span>
- <span data-ttu-id="8bd73-206">Administrators can also use the Web Service SDK GetUserGdpr operation as an option to export all MFA cloud service information collected for a given user or  incorporate into a larger reporting solution.</span><span class="sxs-lookup"><span data-stu-id="8bd73-206">Administrators can also use the Web Service SDK GetUserGdpr operation as an option to export all MFA cloud service information collected for a given user or  incorporate into a larger reporting solution.</span></span>
- <span data-ttu-id="8bd73-207">Search `C:\Program Files\Multi-Factor Authentication Server\Logs\MultiFactorAuthSvc.log` and any backups for “<username>” (include the quotes in the search) to find all instances of the user record being added or changed.</span><span class="sxs-lookup"><span data-stu-id="8bd73-207">Search `C:\Program Files\Multi-Factor Authentication Server\Logs\MultiFactorAuthSvc.log` and any backups for “<username>” (include the quotes in the search) to find all instances of the user record being added or changed.</span></span>
   - <span data-ttu-id="8bd73-208">These records can be limited (but not eliminated) by unchecking **“Log user changes”** in the MFA Server UX, Logging section, Log Files tab.</span><span class="sxs-lookup"><span data-stu-id="8bd73-208">These records can be limited (but not eliminated) by unchecking **“Log user changes”** in the MFA Server UX, Logging section, Log Files tab.</span></span>
   - <span data-ttu-id="8bd73-209">If syslog is configured, and **“Log user changes”** is checked in the MFA Server UX, Logging section, Syslog tab, then the log entries can be gathered from syslog instead.</span><span class="sxs-lookup"><span data-stu-id="8bd73-209">If syslog is configured, and **“Log user changes”** is checked in the MFA Server UX, Logging section, Syslog tab, then the log entries can be gathered from syslog instead.</span></span>
- <span data-ttu-id="8bd73-210">Other occurrences of the username in MultiFactorAuthSvc.log and other MFA Server log files pertaining to authentication attempts are considered operational and duplicative to the information provided using MultiFactorAuthGdpr.exe export or Web Service SDK GetUserGdpr.</span><span class="sxs-lookup"><span data-stu-id="8bd73-210">Other occurrences of the username in MultiFactorAuthSvc.log and other MFA Server log files pertaining to authentication attempts are considered operational and duplicative to the information provided using MultiFactorAuthGdpr.exe export or Web Service SDK GetUserGdpr.</span></span>

## <a name="delete-data-from-mfa-server"></a><span data-ttu-id="8bd73-211">Delete data from MFA Server</span><span class="sxs-lookup"><span data-stu-id="8bd73-211">Delete data from MFA Server</span></span>

<span data-ttu-id="8bd73-212">From the command line of the MFA Server, run the following command changing the path according to your installation `C:\Program Files\Multi-Factor Authentication Server\MultiFactorAuthGdpr.exe delete <username>` to delete all MFA cloud service information collected for this user.</span><span class="sxs-lookup"><span data-stu-id="8bd73-212">From the command line of the MFA Server, run the following command changing the path according to your installation `C:\Program Files\Multi-Factor Authentication Server\MultiFactorAuthGdpr.exe delete <username>` to delete all MFA cloud service information collected for this user.</span></span>

- <span data-ttu-id="8bd73-213">Data included in the export is deleted in real time, but it may take up to 30 days for operational or duplicative data to be fully removed.</span><span class="sxs-lookup"><span data-stu-id="8bd73-213">Data included in the export is deleted in real time, but it may take up to 30 days for operational or duplicative data to be fully removed.</span></span>
- <span data-ttu-id="8bd73-214">Administrators can also use the Web Service SDK DeleteUserGdpr operation as an option to delete all MFA cloud service information collected for a given user or incorporate into a larger reporting solution.</span><span class="sxs-lookup"><span data-stu-id="8bd73-214">Administrators can also use the Web Service SDK DeleteUserGdpr operation as an option to delete all MFA cloud service information collected for a given user or incorporate into a larger reporting solution.</span></span>

## <a name="gather-data-from-nps-extension"></a><span data-ttu-id="8bd73-215">Gather data from NPS Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-215">Gather data from NPS Extension</span></span>

<span data-ttu-id="8bd73-216">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Export.</span><span class="sxs-lookup"><span data-stu-id="8bd73-216">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Export.</span></span>

- <span data-ttu-id="8bd73-217">MFA information is included in the export, which may take hours or days to complete.</span><span class="sxs-lookup"><span data-stu-id="8bd73-217">MFA information is included in the export, which may take hours or days to complete.</span></span>
- <span data-ttu-id="8bd73-218">Occurrences of the username in the AzureMfa/AuthN/AuthNOptCh, AzureMfa/AuthZ/AuthZAdminCh, and AzureMfa/AuthZ/AuthZOptCh event logs are considered operational and duplicative to the information provided in the export.</span><span class="sxs-lookup"><span data-stu-id="8bd73-218">Occurrences of the username in the AzureMfa/AuthN/AuthNOptCh, AzureMfa/AuthZ/AuthZAdminCh, and AzureMfa/AuthZ/AuthZOptCh event logs are considered operational and duplicative to the information provided in the export.</span></span>

## <a name="delete-data-from-nps-extension"></a><span data-ttu-id="8bd73-219">Delete data from NPS Extension</span><span class="sxs-lookup"><span data-stu-id="8bd73-219">Delete data from NPS Extension</span></span>

<span data-ttu-id="8bd73-220">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Account Close to delete all MFA cloud service information collected for this user.</span><span class="sxs-lookup"><span data-stu-id="8bd73-220">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Account Close to delete all MFA cloud service information collected for this user.</span></span>

- <span data-ttu-id="8bd73-221">It may take up to 30 days for data to be fully removed.</span><span class="sxs-lookup"><span data-stu-id="8bd73-221">It may take up to 30 days for data to be fully removed.</span></span>

## <a name="gather-data-from-windows-server-2016-azure-mfa-ad-fs-adapter"></a><span data-ttu-id="8bd73-222">Gather data from Windows Server 2016 Azure MFA AD FS Adapter</span><span class="sxs-lookup"><span data-stu-id="8bd73-222">Gather data from Windows Server 2016 Azure MFA AD FS Adapter</span></span>

<span data-ttu-id="8bd73-223">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Export.</span><span class="sxs-lookup"><span data-stu-id="8bd73-223">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Export.</span></span> 

- <span data-ttu-id="8bd73-224">MFA information is included in the export, which may take hours or days to complete.</span><span class="sxs-lookup"><span data-stu-id="8bd73-224">MFA information is included in the export, which may take hours or days to complete.</span></span>
- <span data-ttu-id="8bd73-225">Occurrences of the username in the AD FS Tracing/Debug event logs (if enabled) are considered operational and duplicative to the information provided in the export.</span><span class="sxs-lookup"><span data-stu-id="8bd73-225">Occurrences of the username in the AD FS Tracing/Debug event logs (if enabled) are considered operational and duplicative to the information provided in the export.</span></span>

## <a name="delete-data-from-windows-server-2016-azure-mfa-ad-fs-adapter"></a><span data-ttu-id="8bd73-226">Delete data from Windows Server 2016 Azure MFA AD FS Adapter</span><span class="sxs-lookup"><span data-stu-id="8bd73-226">Delete data from Windows Server 2016 Azure MFA AD FS Adapter</span></span>

<span data-ttu-id="8bd73-227">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Account Close to delete all MFA cloud service information collected for this user.</span><span class="sxs-lookup"><span data-stu-id="8bd73-227">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Account Close to delete all MFA cloud service information collected for this user.</span></span>

- <span data-ttu-id="8bd73-228">It may take up to 30 days for data to be fully removed.</span><span class="sxs-lookup"><span data-stu-id="8bd73-228">It may take up to 30 days for data to be fully removed.</span></span>

## <a name="gather-data-for-azure-mfa"></a><span data-ttu-id="8bd73-229">Gather data for Azure MFA</span><span class="sxs-lookup"><span data-stu-id="8bd73-229">Gather data for Azure MFA</span></span>

<span data-ttu-id="8bd73-230">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Export.</span><span class="sxs-lookup"><span data-stu-id="8bd73-230">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Export.</span></span>

- <span data-ttu-id="8bd73-231">MFA information is included in the export, which may take hours or days to complete.</span><span class="sxs-lookup"><span data-stu-id="8bd73-231">MFA information is included in the export, which may take hours or days to complete.</span></span>

## <a name="delete-data-for-azure-mfa"></a><span data-ttu-id="8bd73-232">Delete Data for Azure MFA</span><span class="sxs-lookup"><span data-stu-id="8bd73-232">Delete Data for Azure MFA</span></span>

<span data-ttu-id="8bd73-233">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Account Close to delete all MFA cloud service information collected for this user.</span><span class="sxs-lookup"><span data-stu-id="8bd73-233">Use the [Microsoft Privacy Portal](https://portal.azure.com/#blade/Microsoft_Azure_Policy/UserPrivacyMenuBlade/Overview) to make a request for Account Close to delete all MFA cloud service information collected for this user.</span></span>

- <span data-ttu-id="8bd73-234">It may take up to 30 days for data to be fully removed.</span><span class="sxs-lookup"><span data-stu-id="8bd73-234">It may take up to 30 days for data to be fully removed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bd73-235">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bd73-235">Next steps</span></span>

[<span data-ttu-id="8bd73-236">MFA Server reporting</span><span class="sxs-lookup"><span data-stu-id="8bd73-236">MFA Server reporting</span></span>](howto-mfa-reporting.md)
