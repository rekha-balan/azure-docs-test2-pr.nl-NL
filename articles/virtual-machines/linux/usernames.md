---
title: Selecting User Names for Linux | Microsoft Docs
description: Learn how to select user names for a Linux virtual machine in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 554d2e1fa1a8c3660afefcacabb516a0120ba305
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563881"
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="e937a-103">Selecting User Names for Linux on Azure</span><span class="sxs-lookup"><span data-stu-id="e937a-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e937a-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span><span class="sxs-lookup"><span data-stu-id="e937a-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="e937a-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span><span class="sxs-lookup"><span data-stu-id="e937a-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="e937a-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="e937a-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="e937a-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span><span class="sxs-lookup"><span data-stu-id="e937a-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="e937a-108">**However**, Linux defines a set of user names that should not be used.</span><span class="sxs-lookup"><span data-stu-id="e937a-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="e937a-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span><span class="sxs-lookup"><span data-stu-id="e937a-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="e937a-110">A typical example is the `root` user, which has UID 0.</span><span class="sxs-lookup"><span data-stu-id="e937a-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="e937a-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="e937a-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="e937a-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span><span class="sxs-lookup"><span data-stu-id="e937a-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="e937a-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span><span class="sxs-lookup"><span data-stu-id="e937a-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="e937a-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="e937a-114">CentOS</span></span>
* <span data-ttu-id="e937a-115">abrt</span><span class="sxs-lookup"><span data-stu-id="e937a-115">abrt</span></span>
* <span data-ttu-id="e937a-116">adm</span><span class="sxs-lookup"><span data-stu-id="e937a-116">adm</span></span>
* <span data-ttu-id="e937a-117">audio</span><span class="sxs-lookup"><span data-stu-id="e937a-117">audio</span></span>
* <span data-ttu-id="e937a-118">bin</span><span class="sxs-lookup"><span data-stu-id="e937a-118">bin</span></span>
* <span data-ttu-id="e937a-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="e937a-119">cdrom</span></span>
* <span data-ttu-id="e937a-120">cgred</span><span class="sxs-lookup"><span data-stu-id="e937a-120">cgred</span></span>
* <span data-ttu-id="e937a-121">daemon</span><span class="sxs-lookup"><span data-stu-id="e937a-121">daemon</span></span>
* <span data-ttu-id="e937a-122">dbus</span><span class="sxs-lookup"><span data-stu-id="e937a-122">dbus</span></span>
* <span data-ttu-id="e937a-123">dialout</span><span class="sxs-lookup"><span data-stu-id="e937a-123">dialout</span></span>
* <span data-ttu-id="e937a-124">dip</span><span class="sxs-lookup"><span data-stu-id="e937a-124">dip</span></span>
* <span data-ttu-id="e937a-125">disk</span><span class="sxs-lookup"><span data-stu-id="e937a-125">disk</span></span>
* <span data-ttu-id="e937a-126">floppy</span><span class="sxs-lookup"><span data-stu-id="e937a-126">floppy</span></span>
* <span data-ttu-id="e937a-127">ftp</span><span class="sxs-lookup"><span data-stu-id="e937a-127">ftp</span></span>
* <span data-ttu-id="e937a-128">ftp</span><span class="sxs-lookup"><span data-stu-id="e937a-128">ftp</span></span>
* <span data-ttu-id="e937a-129">games</span><span class="sxs-lookup"><span data-stu-id="e937a-129">games</span></span>
* <span data-ttu-id="e937a-130">gopher</span><span class="sxs-lookup"><span data-stu-id="e937a-130">gopher</span></span>
* <span data-ttu-id="e937a-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="e937a-131">haldaemon</span></span>
* <span data-ttu-id="e937a-132">halt</span><span class="sxs-lookup"><span data-stu-id="e937a-132">halt</span></span>
* <span data-ttu-id="e937a-133">kmem</span><span class="sxs-lookup"><span data-stu-id="e937a-133">kmem</span></span>
* <span data-ttu-id="e937a-134">lock</span><span class="sxs-lookup"><span data-stu-id="e937a-134">lock</span></span>
* <span data-ttu-id="e937a-135">lp</span><span class="sxs-lookup"><span data-stu-id="e937a-135">lp</span></span>
* <span data-ttu-id="e937a-136">mail</span><span class="sxs-lookup"><span data-stu-id="e937a-136">mail</span></span>
* <span data-ttu-id="e937a-137">man</span><span class="sxs-lookup"><span data-stu-id="e937a-137">man</span></span>
* <span data-ttu-id="e937a-138">mem</span><span class="sxs-lookup"><span data-stu-id="e937a-138">mem</span></span>
* <span data-ttu-id="e937a-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="e937a-139">nfsnobody</span></span>
* <span data-ttu-id="e937a-140">nobody</span><span class="sxs-lookup"><span data-stu-id="e937a-140">nobody</span></span>
* <span data-ttu-id="e937a-141">ntp</span><span class="sxs-lookup"><span data-stu-id="e937a-141">ntp</span></span>
* <span data-ttu-id="e937a-142">operator</span><span class="sxs-lookup"><span data-stu-id="e937a-142">operator</span></span>
* <span data-ttu-id="e937a-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="e937a-143">oprofile</span></span>
* <span data-ttu-id="e937a-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="e937a-144">postdrop</span></span>
* <span data-ttu-id="e937a-145">postfix</span><span class="sxs-lookup"><span data-stu-id="e937a-145">postfix</span></span>
* <span data-ttu-id="e937a-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="e937a-146">qpidd</span></span>
* <span data-ttu-id="e937a-147">root</span><span class="sxs-lookup"><span data-stu-id="e937a-147">root</span></span>
* <span data-ttu-id="e937a-148">rpc</span><span class="sxs-lookup"><span data-stu-id="e937a-148">rpc</span></span>
* <span data-ttu-id="e937a-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="e937a-149">rpcuser</span></span>
* <span data-ttu-id="e937a-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="e937a-150">saslauth</span></span>
* <span data-ttu-id="e937a-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="e937a-151">shutdown</span></span>
* <span data-ttu-id="e937a-152">slocate</span><span class="sxs-lookup"><span data-stu-id="e937a-152">slocate</span></span>
* <span data-ttu-id="e937a-153">sshd</span><span class="sxs-lookup"><span data-stu-id="e937a-153">sshd</span></span>
* <span data-ttu-id="e937a-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="e937a-154">stapdev</span></span>
* <span data-ttu-id="e937a-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="e937a-155">stapusr</span></span>
* <span data-ttu-id="e937a-156">sync</span><span class="sxs-lookup"><span data-stu-id="e937a-156">sync</span></span>
* <span data-ttu-id="e937a-157">sys</span><span class="sxs-lookup"><span data-stu-id="e937a-157">sys</span></span>
* <span data-ttu-id="e937a-158">tape</span><span class="sxs-lookup"><span data-stu-id="e937a-158">tape</span></span>
* <span data-ttu-id="e937a-159">test</span><span class="sxs-lookup"><span data-stu-id="e937a-159">test</span></span>
* <span data-ttu-id="e937a-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="e937a-160">tcpdump</span></span>
* <span data-ttu-id="e937a-161">tty</span><span class="sxs-lookup"><span data-stu-id="e937a-161">tty</span></span>
* <span data-ttu-id="e937a-162">users</span><span class="sxs-lookup"><span data-stu-id="e937a-162">users</span></span>
* <span data-ttu-id="e937a-163">utempter</span><span class="sxs-lookup"><span data-stu-id="e937a-163">utempter</span></span>
* <span data-ttu-id="e937a-164">utmp</span><span class="sxs-lookup"><span data-stu-id="e937a-164">utmp</span></span>
* <span data-ttu-id="e937a-165">uucp</span><span class="sxs-lookup"><span data-stu-id="e937a-165">uucp</span></span>
* <span data-ttu-id="e937a-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="e937a-166">vcsa</span></span>
* <span data-ttu-id="e937a-167">video</span><span class="sxs-lookup"><span data-stu-id="e937a-167">video</span></span>
* <span data-ttu-id="e937a-168">wheel</span><span class="sxs-lookup"><span data-stu-id="e937a-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="e937a-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e937a-169">Ubuntu</span></span>
* <span data-ttu-id="e937a-170">adm</span><span class="sxs-lookup"><span data-stu-id="e937a-170">adm</span></span>
* <span data-ttu-id="e937a-171">admin</span><span class="sxs-lookup"><span data-stu-id="e937a-171">admin</span></span>
* <span data-ttu-id="e937a-172">audio</span><span class="sxs-lookup"><span data-stu-id="e937a-172">audio</span></span>
* <span data-ttu-id="e937a-173">backup</span><span class="sxs-lookup"><span data-stu-id="e937a-173">backup</span></span>
* <span data-ttu-id="e937a-174">bin</span><span class="sxs-lookup"><span data-stu-id="e937a-174">bin</span></span>
* <span data-ttu-id="e937a-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="e937a-175">cdrom</span></span>
* <span data-ttu-id="e937a-176">crontab</span><span class="sxs-lookup"><span data-stu-id="e937a-176">crontab</span></span>
* <span data-ttu-id="e937a-177">daemon</span><span class="sxs-lookup"><span data-stu-id="e937a-177">daemon</span></span>
* <span data-ttu-id="e937a-178">dialout</span><span class="sxs-lookup"><span data-stu-id="e937a-178">dialout</span></span>
* <span data-ttu-id="e937a-179">dip</span><span class="sxs-lookup"><span data-stu-id="e937a-179">dip</span></span>
* <span data-ttu-id="e937a-180">disk</span><span class="sxs-lookup"><span data-stu-id="e937a-180">disk</span></span>
* <span data-ttu-id="e937a-181">fax</span><span class="sxs-lookup"><span data-stu-id="e937a-181">fax</span></span>
* <span data-ttu-id="e937a-182">floppy</span><span class="sxs-lookup"><span data-stu-id="e937a-182">floppy</span></span>
* <span data-ttu-id="e937a-183">fuse</span><span class="sxs-lookup"><span data-stu-id="e937a-183">fuse</span></span>
* <span data-ttu-id="e937a-184">games</span><span class="sxs-lookup"><span data-stu-id="e937a-184">games</span></span>
* <span data-ttu-id="e937a-185">gnats</span><span class="sxs-lookup"><span data-stu-id="e937a-185">gnats</span></span>
* <span data-ttu-id="e937a-186">irc</span><span class="sxs-lookup"><span data-stu-id="e937a-186">irc</span></span>
* <span data-ttu-id="e937a-187">kmem</span><span class="sxs-lookup"><span data-stu-id="e937a-187">kmem</span></span>
* <span data-ttu-id="e937a-188">landscape</span><span class="sxs-lookup"><span data-stu-id="e937a-188">landscape</span></span>
* <span data-ttu-id="e937a-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="e937a-189">libuuid</span></span>
* <span data-ttu-id="e937a-190">list</span><span class="sxs-lookup"><span data-stu-id="e937a-190">list</span></span>
* <span data-ttu-id="e937a-191">lp</span><span class="sxs-lookup"><span data-stu-id="e937a-191">lp</span></span>
* <span data-ttu-id="e937a-192">mail</span><span class="sxs-lookup"><span data-stu-id="e937a-192">mail</span></span>
* <span data-ttu-id="e937a-193">man</span><span class="sxs-lookup"><span data-stu-id="e937a-193">man</span></span>
* <span data-ttu-id="e937a-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="e937a-194">messagebus</span></span>
* <span data-ttu-id="e937a-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="e937a-195">mlocate</span></span>
* <span data-ttu-id="e937a-196">netdev</span><span class="sxs-lookup"><span data-stu-id="e937a-196">netdev</span></span>
* <span data-ttu-id="e937a-197">news</span><span class="sxs-lookup"><span data-stu-id="e937a-197">news</span></span>
* <span data-ttu-id="e937a-198">nobody</span><span class="sxs-lookup"><span data-stu-id="e937a-198">nobody</span></span>
* <span data-ttu-id="e937a-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="e937a-199">nogroup</span></span>
* <span data-ttu-id="e937a-200">operator</span><span class="sxs-lookup"><span data-stu-id="e937a-200">operator</span></span>
* <span data-ttu-id="e937a-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="e937a-201">plugdev</span></span>
* <span data-ttu-id="e937a-202">proxy</span><span class="sxs-lookup"><span data-stu-id="e937a-202">proxy</span></span>
* <span data-ttu-id="e937a-203">root</span><span class="sxs-lookup"><span data-stu-id="e937a-203">root</span></span>
* <span data-ttu-id="e937a-204">sasl</span><span class="sxs-lookup"><span data-stu-id="e937a-204">sasl</span></span>
* <span data-ttu-id="e937a-205">shadow</span><span class="sxs-lookup"><span data-stu-id="e937a-205">shadow</span></span>
* <span data-ttu-id="e937a-206">src</span><span class="sxs-lookup"><span data-stu-id="e937a-206">src</span></span>
* <span data-ttu-id="e937a-207">ssh</span><span class="sxs-lookup"><span data-stu-id="e937a-207">ssh</span></span>
* <span data-ttu-id="e937a-208">sshd</span><span class="sxs-lookup"><span data-stu-id="e937a-208">sshd</span></span>
* <span data-ttu-id="e937a-209">staff</span><span class="sxs-lookup"><span data-stu-id="e937a-209">staff</span></span>
* <span data-ttu-id="e937a-210">sudo</span><span class="sxs-lookup"><span data-stu-id="e937a-210">sudo</span></span>
* <span data-ttu-id="e937a-211">sync</span><span class="sxs-lookup"><span data-stu-id="e937a-211">sync</span></span>
* <span data-ttu-id="e937a-212">sys</span><span class="sxs-lookup"><span data-stu-id="e937a-212">sys</span></span>
* <span data-ttu-id="e937a-213">syslog</span><span class="sxs-lookup"><span data-stu-id="e937a-213">syslog</span></span>
* <span data-ttu-id="e937a-214">tape</span><span class="sxs-lookup"><span data-stu-id="e937a-214">tape</span></span>
* <span data-ttu-id="e937a-215">tty</span><span class="sxs-lookup"><span data-stu-id="e937a-215">tty</span></span>
* <span data-ttu-id="e937a-216">users</span><span class="sxs-lookup"><span data-stu-id="e937a-216">users</span></span>
* <span data-ttu-id="e937a-217">utmp</span><span class="sxs-lookup"><span data-stu-id="e937a-217">utmp</span></span>
* <span data-ttu-id="e937a-218">uucp</span><span class="sxs-lookup"><span data-stu-id="e937a-218">uucp</span></span>
* <span data-ttu-id="e937a-219">video</span><span class="sxs-lookup"><span data-stu-id="e937a-219">video</span></span>
* <span data-ttu-id="e937a-220">voice</span><span class="sxs-lookup"><span data-stu-id="e937a-220">voice</span></span>
* <span data-ttu-id="e937a-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="e937a-221">whoopsie</span></span>
* <span data-ttu-id="e937a-222">www-data</span><span class="sxs-lookup"><span data-stu-id="e937a-222">www-data</span></span>

