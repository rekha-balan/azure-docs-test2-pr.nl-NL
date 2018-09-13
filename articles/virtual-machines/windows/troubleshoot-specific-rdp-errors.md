---
title: Specific RDP error messages for Azure VMs | Microsoft Docs
description: Understand specific error messages that you may receive when trying use Remote Desktop connection to a Windows virtual machine in Azure
keywords: Remote desktop error,remote desktop connection error,cannot connect to VM,remote desktop troubleshooting
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 01/10/2017
ms.author: iainfou
ms.openlocfilehash: 6d24277ec347ea0c488b5ac343ea15d4a7faaaae
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551275"
---
# <a name="troubleshooting-specific-rdp-error-messages-to-a-windows-vm-in-azure"></a><span data-ttu-id="71aef-104">Troubleshooting specific RDP error messages to a Windows VM in Azure</span><span class="sxs-lookup"><span data-stu-id="71aef-104">Troubleshooting specific RDP error messages to a Windows VM in Azure</span></span>
<span data-ttu-id="71aef-105">You may receive a specific error message when using Remote Desktop connection to a Windows virtual machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="71aef-105">You may receive a specific error message when using Remote Desktop connection to a Windows virtual machine (VM) in Azure.</span></span> <span data-ttu-id="71aef-106">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span><span class="sxs-lookup"><span data-stu-id="71aef-106">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span> <span data-ttu-id="71aef-107">If you are having issues connecting to your VM using RDP but do not encounter a specific error message, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71aef-107">If you are having issues connecting to your VM using RDP but do not encounter a specific error message, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="71aef-108">For information on specific error messages, see the following:</span><span class="sxs-lookup"><span data-stu-id="71aef-108">For information on specific error messages, see the following:</span></span>

* <span data-ttu-id="71aef-109">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](#rdplicense).</span><span class="sxs-lookup"><span data-stu-id="71aef-109">[The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license](#rdplicense).</span></span>
* <span data-ttu-id="71aef-110">[Remote Desktop can't find the computer "name"](#rdpname).</span><span class="sxs-lookup"><span data-stu-id="71aef-110">[Remote Desktop can't find the computer "name"](#rdpname).</span></span>
* <span data-ttu-id="71aef-111">[An authentication error has occurred. The Local Security Authority cannot be contacted](#rdpauth).</span><span class="sxs-lookup"><span data-stu-id="71aef-111">[An authentication error has occurred. The Local Security Authority cannot be contacted](#rdpauth).</span></span>
* <span data-ttu-id="71aef-112">[Windows Security error: Your credentials did not work](#wincred).</span><span class="sxs-lookup"><span data-stu-id="71aef-112">[Windows Security error: Your credentials did not work](#wincred).</span></span>
* <span data-ttu-id="71aef-113">[This computer can't connect to the remote computer](#rdpconnect).</span><span class="sxs-lookup"><span data-stu-id="71aef-113">[This computer can't connect to the remote computer](#rdpconnect).</span></span>

<a id="rdplicense"></a>

## <a name="the-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-to-provide-a-license"></a><span data-ttu-id="71aef-114">The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license.</span><span class="sxs-lookup"><span data-stu-id="71aef-114">The remote session was disconnected because there are no Remote Desktop License Servers available to provide a license.</span></span>
<span data-ttu-id="71aef-115">Cause: The 120-day licensing grace period for the Remote Desktop Server role has expired and you need to install licenses.</span><span class="sxs-lookup"><span data-stu-id="71aef-115">Cause: The 120-day licensing grace period for the Remote Desktop Server role has expired and you need to install licenses.</span></span>

<span data-ttu-id="71aef-116">As a workaround, save a local copy of the RDP file from the portal and run this command at a PowerShell command prompt to connect.</span><span class="sxs-lookup"><span data-stu-id="71aef-116">As a workaround, save a local copy of the RDP file from the portal and run this command at a PowerShell command prompt to connect.</span></span> <span data-ttu-id="71aef-117">This step disables licensing for just that connection:</span><span class="sxs-lookup"><span data-stu-id="71aef-117">This step disables licensing for just that connection:</span></span>

        mstsc <File name>.RDP /admin

<span data-ttu-id="71aef-118">If you don't actually need more than two simultaneous Remote Desktop connections to the VM, you can use Server Manager to remove the Remote Desktop Server role.</span><span class="sxs-lookup"><span data-stu-id="71aef-118">If you don't actually need more than two simultaneous Remote Desktop connections to the VM, you can use Server Manager to remove the Remote Desktop Server role.</span></span>

<span data-ttu-id="71aef-119">For more information, see the blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span><span class="sxs-lookup"><span data-stu-id="71aef-119">For more information, see the blog post [Azure VM fails with "No Remote Desktop License Servers available"](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/).</span></span>

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-the-computer-name"></a><span data-ttu-id="71aef-120">Remote Desktop can't find the computer "name".</span><span class="sxs-lookup"><span data-stu-id="71aef-120">Remote Desktop can't find the computer "name".</span></span>
<span data-ttu-id="71aef-121">Cause: The Remote Desktop client on your computer can't resolve the name of the computer in the settings of the RDP file.</span><span class="sxs-lookup"><span data-stu-id="71aef-121">Cause: The Remote Desktop client on your computer can't resolve the name of the computer in the settings of the RDP file.</span></span>

<span data-ttu-id="71aef-122">Possible solutions:</span><span class="sxs-lookup"><span data-stu-id="71aef-122">Possible solutions:</span></span>

* <span data-ttu-id="71aef-123">If you're on an organization's intranet, make sure that your computer has access to the proxy server and can send HTTPS traffic to it.</span><span class="sxs-lookup"><span data-stu-id="71aef-123">If you're on an organization's intranet, make sure that your computer has access to the proxy server and can send HTTPS traffic to it.</span></span>
* <span data-ttu-id="71aef-124">If you're using a locally stored RDP file, try using the one that's generated by the portal.</span><span class="sxs-lookup"><span data-stu-id="71aef-124">If you're using a locally stored RDP file, try using the one that's generated by the portal.</span></span> <span data-ttu-id="71aef-125">This step ensures that you have the correct DNS name for the virtual machine, or the cloud service and the endpoint port of the VM.</span><span class="sxs-lookup"><span data-stu-id="71aef-125">This step ensures that you have the correct DNS name for the virtual machine, or the cloud service and the endpoint port of the VM.</span></span> <span data-ttu-id="71aef-126">Here is a sample RDP file generated by the portal:</span><span class="sxs-lookup"><span data-stu-id="71aef-126">Here is a sample RDP file generated by the portal:</span></span>
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

<span data-ttu-id="71aef-127">The address portion of this RDP file has:</span><span class="sxs-lookup"><span data-stu-id="71aef-127">The address portion of this RDP file has:</span></span>

* <span data-ttu-id="71aef-128">The fully qualified domain name of the cloud service that contains the VM ("tailspin-azdatatier.cloudapp.net" in this example).</span><span class="sxs-lookup"><span data-stu-id="71aef-128">The fully qualified domain name of the cloud service that contains the VM ("tailspin-azdatatier.cloudapp.net" in this example).</span></span>
* <span data-ttu-id="71aef-129">The external TCP port of the endpoint for Remote Desktop traffic (55919).</span><span class="sxs-lookup"><span data-stu-id="71aef-129">The external TCP port of the endpoint for Remote Desktop traffic (55919).</span></span>

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-the-local-security-authority-cannot-be-contacted"></a><span data-ttu-id="71aef-130">An authentication error has occurred.</span><span class="sxs-lookup"><span data-stu-id="71aef-130">An authentication error has occurred.</span></span> <span data-ttu-id="71aef-131">The Local Security Authority cannot be contacted.</span><span class="sxs-lookup"><span data-stu-id="71aef-131">The Local Security Authority cannot be contacted.</span></span>
<span data-ttu-id="71aef-132">Cause: The target VM can't locate the security authority in the user name portion of your credentials.</span><span class="sxs-lookup"><span data-stu-id="71aef-132">Cause: The target VM can't locate the security authority in the user name portion of your credentials.</span></span>

<span data-ttu-id="71aef-133">When your user name is in the form *SecurityAuthority*\\*UserName* (example: CORP\User1), the *SecurityAuthority* portion is either the VM's computer name (for the local security authority) or an Active Directory domain name.</span><span class="sxs-lookup"><span data-stu-id="71aef-133">When your user name is in the form *SecurityAuthority*\\*UserName* (example: CORP\User1), the *SecurityAuthority* portion is either the VM's computer name (for the local security authority) or an Active Directory domain name.</span></span>

<span data-ttu-id="71aef-134">Possible solutions:</span><span class="sxs-lookup"><span data-stu-id="71aef-134">Possible solutions:</span></span>

* <span data-ttu-id="71aef-135">If the account is local to the VM, make sure that the VM name is spelled correctly.</span><span class="sxs-lookup"><span data-stu-id="71aef-135">If the account is local to the VM, make sure that the VM name is spelled correctly.</span></span>
* <span data-ttu-id="71aef-136">If the account is on an Active Directory domain, check the spelling of the domain name.</span><span class="sxs-lookup"><span data-stu-id="71aef-136">If the account is on an Active Directory domain, check the spelling of the domain name.</span></span>
* <span data-ttu-id="71aef-137">If it is an Active Directory domain account and the domain name is spelled correctly, verify that a domain controller is available in that domain.</span><span class="sxs-lookup"><span data-stu-id="71aef-137">If it is an Active Directory domain account and the domain name is spelled correctly, verify that a domain controller is available in that domain.</span></span> <span data-ttu-id="71aef-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span><span class="sxs-lookup"><span data-stu-id="71aef-138">It's a common issue in Azure virtual networks that contain domain controllers that a domain controller is unavailable because it hasn't been started.</span></span> <span data-ttu-id="71aef-139">As a workaround, you can use a local administrator account instead of a domain account.</span><span class="sxs-lookup"><span data-stu-id="71aef-139">As a workaround, you can use a local administrator account instead of a domain account.</span></span>

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a><span data-ttu-id="71aef-140">Windows Security error: Your credentials did not work.</span><span class="sxs-lookup"><span data-stu-id="71aef-140">Windows Security error: Your credentials did not work.</span></span>
<span data-ttu-id="71aef-141">Cause: The target VM can't validate your account name and password.</span><span class="sxs-lookup"><span data-stu-id="71aef-141">Cause: The target VM can't validate your account name and password.</span></span>

<span data-ttu-id="71aef-142">A Windows-based computer can validate the credentials of either a local account or a domain account.</span><span class="sxs-lookup"><span data-stu-id="71aef-142">A Windows-based computer can validate the credentials of either a local account or a domain account.</span></span>

* <span data-ttu-id="71aef-143">For local accounts, use the *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span><span class="sxs-lookup"><span data-stu-id="71aef-143">For local accounts, use the *ComputerName*\\*UserName* syntax (example: SQL1\Admin4798).</span></span>
* <span data-ttu-id="71aef-144">For domain accounts, use the *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span><span class="sxs-lookup"><span data-stu-id="71aef-144">For domain accounts, use the *DomainName*\\*UserName* syntax (example: CONTOSO\peterodman).</span></span>

<span data-ttu-id="71aef-145">If you have promoted your VM to a domain controller in a new Active Directory forest, the local administrator account that you signed in with is converted to an equivalent account with the same password in the new forest and domain.</span><span class="sxs-lookup"><span data-stu-id="71aef-145">If you have promoted your VM to a domain controller in a new Active Directory forest, the local administrator account that you signed in with is converted to an equivalent account with the same password in the new forest and domain.</span></span> <span data-ttu-id="71aef-146">The local account is then deleted.</span><span class="sxs-lookup"><span data-stu-id="71aef-146">The local account is then deleted.</span></span>

<span data-ttu-id="71aef-147">For example, if you signed in with the local account DC1\DCAdmin, and then promoted the virtual machine as a domain controller in a new forest for the corp.contoso.com domain, the DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with the same password.</span><span class="sxs-lookup"><span data-stu-id="71aef-147">For example, if you signed in with the local account DC1\DCAdmin, and then promoted the virtual machine as a domain controller in a new forest for the corp.contoso.com domain, the DC1\DCAdmin local account gets deleted and a new domain account (CORP\DCAdmin) is created with the same password.</span></span>

<span data-ttu-id="71aef-148">Make sure that the account name is a name that the virtual machine can verify as a valid account, and that the password is correct.</span><span class="sxs-lookup"><span data-stu-id="71aef-148">Make sure that the account name is a name that the virtual machine can verify as a valid account, and that the password is correct.</span></span>

<span data-ttu-id="71aef-149">If you need to change the password of the local administrator account, see [How to reset a password or the Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71aef-149">If you need to change the password of the local administrator account, see [How to reset a password or the Remote Desktop service for Windows virtual machines](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-to-the-remote-computer"></a><span data-ttu-id="71aef-150">This computer can't connect to the remote computer.</span><span class="sxs-lookup"><span data-stu-id="71aef-150">This computer can't connect to the remote computer.</span></span>
<span data-ttu-id="71aef-151">Cause: The account that's used to connect does not have Remote Desktop sign-in rights.</span><span class="sxs-lookup"><span data-stu-id="71aef-151">Cause: The account that's used to connect does not have Remote Desktop sign-in rights.</span></span>

<span data-ttu-id="71aef-152">Every Windows computer has a Remote Desktop users local group, which contains the accounts and groups that can sign into it remotely.</span><span class="sxs-lookup"><span data-stu-id="71aef-152">Every Windows computer has a Remote Desktop users local group, which contains the accounts and groups that can sign into it remotely.</span></span> <span data-ttu-id="71aef-153">Members of the local administrators group also have access, even though those accounts are not listed in the Remote Desktop users local group.</span><span class="sxs-lookup"><span data-stu-id="71aef-153">Members of the local administrators group also have access, even though those accounts are not listed in the Remote Desktop users local group.</span></span> <span data-ttu-id="71aef-154">For domain-joined machines, the local administrators group also contains the domain administrators for the domain.</span><span class="sxs-lookup"><span data-stu-id="71aef-154">For domain-joined machines, the local administrators group also contains the domain administrators for the domain.</span></span>

<span data-ttu-id="71aef-155">Make sure that the account you're using to connect with has Remote Desktop sign-in rights.</span><span class="sxs-lookup"><span data-stu-id="71aef-155">Make sure that the account you're using to connect with has Remote Desktop sign-in rights.</span></span> <span data-ttu-id="71aef-156">As a workaround, use a domain or local administrator account to connect over Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="71aef-156">As a workaround, use a domain or local administrator account to connect over Remote Desktop.</span></span> <span data-ttu-id="71aef-157">To add the desired account to the Remote Desktop users local group, use the Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span><span class="sxs-lookup"><span data-stu-id="71aef-157">To add the desired account to the Remote Desktop users local group, use the Microsoft Management Console snap-in (**System Tools > Local Users and Groups > Groups > Remote Desktop Users**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71aef-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="71aef-158">Next steps</span></span>
<span data-ttu-id="71aef-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71aef-159">If none of these errors occurred and you have an unknown issue with connecting using RDP, see the [troubleshooting guide for Remote Desktop](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="71aef-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71aef-160">For troubleshooting steps in accessing applications running on a VM, see [Troubleshoot access to an application running on an Azure VM](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="71aef-161">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71aef-161">If you are having issues using Secure Shell (SSH) to connect to a Linux VM in Azure, see [Troubleshoot SSH connections to a Linux VM in Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

