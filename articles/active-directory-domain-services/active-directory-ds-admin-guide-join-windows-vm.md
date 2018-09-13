---
title: 'Azure Active Directory Domain Services: Join a Windows Server VM to a managed domain | Microsoft Docs'
description: Join a Windows Server virtual machine to Azure AD Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: f673bcc9872a4fe79f5a700722f85d95b838a820
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540925"
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="3b729-103">Join a Windows Server virtual machine to a managed domain</span><span class="sxs-lookup"><span data-stu-id="3b729-103">Join a Windows Server virtual machine to a managed domain</span></span>
> [!div class="op_single_selector"]
> * [Azure classic portal - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

<span data-ttu-id="3b729-106">This article shows you how to join a virtual machine running Windows Server 2012 R2 to an Azure AD Domain Services managed domain, using the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="3b729-106">This article shows you how to join a virtual machine running Windows Server 2012 R2 to an Azure AD Domain Services managed domain, using the Azure classic portal.</span></span>

## <a name="step-1-create-the-windows-server-virtual-machine"></a><span data-ttu-id="3b729-107">Step 1: Create the Windows Server virtual machine</span><span class="sxs-lookup"><span data-stu-id="3b729-107">Step 1: Create the Windows Server virtual machine</span></span>
<span data-ttu-id="3b729-108">Follow the instructions outlined in the [Create a virtual machine running Windows in the Azure classic portal](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial.</span><span class="sxs-lookup"><span data-stu-id="3b729-108">Follow the instructions outlined in the [Create a virtual machine running Windows in the Azure classic portal](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) tutorial.</span></span> <span data-ttu-id="3b729-109">It is important to ensure that this newly created virtual machine is joined to the same virtual network in which you enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="3b729-109">It is important to ensure that this newly created virtual machine is joined to the same virtual network in which you enabled Azure AD Domain Services.</span></span> <span data-ttu-id="3b729-110">The 'Quick Create' option does not enable you to join the virtual machine to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="3b729-110">The 'Quick Create' option does not enable you to join the virtual machine to a virtual network.</span></span> <span data-ttu-id="3b729-111">Therefore, you need to use the 'From Gallery' option to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3b729-111">Therefore, you need to use the 'From Gallery' option to create the virtual machine.</span></span>

<span data-ttu-id="3b729-112">Perform the following steps to create a Windows virtual machine joined to the virtual network in which you've enabled Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="3b729-112">Perform the following steps to create a Windows virtual machine joined to the virtual network in which you've enabled Azure AD Domain Services.</span></span>

1. <span data-ttu-id="3b729-113">In the Azure classic portal, on the command bar at the bottom of the window, click **New**.</span><span class="sxs-lookup"><span data-stu-id="3b729-113">In the Azure classic portal, on the command bar at the bottom of the window, click **New**.</span></span>
2. <span data-ttu-id="3b729-114">Under **Compute**, click **Virtual Machine**, then click **From Gallery**.</span><span class="sxs-lookup"><span data-stu-id="3b729-114">Under **Compute**, click **Virtual Machine**, then click **From Gallery**.</span></span>
3. <span data-ttu-id="3b729-115">The first screen lets you **Choose an Image** for your virtual machine from the list of available images.</span><span class="sxs-lookup"><span data-stu-id="3b729-115">The first screen lets you **Choose an Image** for your virtual machine from the list of available images.</span></span> <span data-ttu-id="3b729-116">Pick the appropriate image.</span><span class="sxs-lookup"><span data-stu-id="3b729-116">Pick the appropriate image.</span></span>

    ![Select image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. <span data-ttu-id="3b729-118">The second screen lets you pick a computer name, size, and administrative user name and password.</span><span class="sxs-lookup"><span data-stu-id="3b729-118">The second screen lets you pick a computer name, size, and administrative user name and password.</span></span> <span data-ttu-id="3b729-119">Use the tier and size required to run your app or workload.</span><span class="sxs-lookup"><span data-stu-id="3b729-119">Use the tier and size required to run your app or workload.</span></span> <span data-ttu-id="3b729-120">The user name you pick here is a local administrator user on the machine.</span><span class="sxs-lookup"><span data-stu-id="3b729-120">The user name you pick here is a local administrator user on the machine.</span></span> <span data-ttu-id="3b729-121">Do not enter a domain user account's credentials here.</span><span class="sxs-lookup"><span data-stu-id="3b729-121">Do not enter a domain user account's credentials here.</span></span>

    ![Configure virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. <span data-ttu-id="3b729-123">The third screen lets you configure resources for networking, storage, and availability.</span><span class="sxs-lookup"><span data-stu-id="3b729-123">The third screen lets you configure resources for networking, storage, and availability.</span></span> <span data-ttu-id="3b729-124">Ensure you select the virtual network in which you enabled Azure AD Domain Services from the **Region/Affinity Group/Virtual Network** dropdown.</span><span class="sxs-lookup"><span data-stu-id="3b729-124">Ensure you select the virtual network in which you enabled Azure AD Domain Services from the **Region/Affinity Group/Virtual Network** dropdown.</span></span> <span data-ttu-id="3b729-125">Specify a **Cloud Service DNS Name** as appropriate for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3b729-125">Specify a **Cloud Service DNS Name** as appropriate for the virtual machine.</span></span>

    ![Select virtual network for virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Ensure that you join the virtual machine to the same virtual network in which you've enabled Azure AD Domain Services. As a result, the virtual machine can 'see' the domain and perform tasks such as joining the domain. If you choose to create the virtual machine in a different virtual network, connect that virtual network to the virtual network in which you've enabled Azure AD Domain Services.
   >
   >
6. <span data-ttu-id="3b729-130">The fourth screen lets you install the VM Agent and configure some of the available extensions.</span><span class="sxs-lookup"><span data-stu-id="3b729-130">The fourth screen lets you install the VM Agent and configure some of the available extensions.</span></span>

    ![Done](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. <span data-ttu-id="3b729-132">After the virtual machine is created, the classic portal lists the new virtual machine under the **Virtual Machines** node.</span><span class="sxs-lookup"><span data-stu-id="3b729-132">After the virtual machine is created, the classic portal lists the new virtual machine under the **Virtual Machines** node.</span></span> <span data-ttu-id="3b729-133">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span><span class="sxs-lookup"><span data-stu-id="3b729-133">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

    ![Virtual machine is up and running](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-to-the-windows-server-virtual-machine-using-the-local-administrator-account"></a><span data-ttu-id="3b729-135">Step 2: Connect to the Windows Server virtual machine using the local administrator account</span><span class="sxs-lookup"><span data-stu-id="3b729-135">Step 2: Connect to the Windows Server virtual machine using the local administrator account</span></span>
<span data-ttu-id="3b729-136">Now, we connect to the newly created Windows Server virtual machine, to join it to the domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-136">Now, we connect to the newly created Windows Server virtual machine, to join it to the domain.</span></span> <span data-ttu-id="3b729-137">Use the local administrator credentials you specified when creating the virtual machine, to connect to it.</span><span class="sxs-lookup"><span data-stu-id="3b729-137">Use the local administrator credentials you specified when creating the virtual machine, to connect to it.</span></span>

<span data-ttu-id="3b729-138">Perform the following steps to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3b729-138">Perform the following steps to connect to the virtual machine.</span></span>

1. <span data-ttu-id="3b729-139">Navigate to **Virtual Machines** node in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="3b729-139">Navigate to **Virtual Machines** node in the classic portal.</span></span> <span data-ttu-id="3b729-140">Select the virtual machine you created in Step 1 and click **Connect** on the command bar at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="3b729-140">Select the virtual machine you created in Step 1 and click **Connect** on the command bar at the bottom of the window.</span></span>

    ![Connect to Windows virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. <span data-ttu-id="3b729-142">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3b729-142">The classic portal prompts you to open or save a file with a '.rdp' extension, which is used to connect to the virtual machine.</span></span> <span data-ttu-id="3b729-143">Click to open the file when it has finished downloading.</span><span class="sxs-lookup"><span data-stu-id="3b729-143">Click to open the file when it has finished downloading.</span></span>
3. <span data-ttu-id="3b729-144">At the login prompt, enter your **local administrator credentials**, which you specified while creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3b729-144">At the login prompt, enter your **local administrator credentials**, which you specified while creating the virtual machine.</span></span> <span data-ttu-id="3b729-145">For example, we've used 'localhost\mahesh' in this example.</span><span class="sxs-lookup"><span data-stu-id="3b729-145">For example, we've used 'localhost\mahesh' in this example.</span></span>

<span data-ttu-id="3b729-146">At this point, you should be logged in to the newly created Windows virtual machine using local Administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="3b729-146">At this point, you should be logged in to the newly created Windows virtual machine using local Administrator credentials.</span></span> <span data-ttu-id="3b729-147">The next step is to join the virtual machine to the domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-147">The next step is to join the virtual machine to the domain.</span></span>

## <a name="step-3-join-the-windows-server-virtual-machine-to-the-aad-ds-managed-domain"></a><span data-ttu-id="3b729-148">Step 3: Join the Windows Server virtual machine to the AAD-DS managed domain</span><span class="sxs-lookup"><span data-stu-id="3b729-148">Step 3: Join the Windows Server virtual machine to the AAD-DS managed domain</span></span>
<span data-ttu-id="3b729-149">Perform the following steps to join the Windows Server virtual machine to the AAD-DS managed domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-149">Perform the following steps to join the Windows Server virtual machine to the AAD-DS managed domain.</span></span>

1. <span data-ttu-id="3b729-150">Connect to the Windows Server as shown in Step 2.</span><span class="sxs-lookup"><span data-stu-id="3b729-150">Connect to the Windows Server as shown in Step 2.</span></span> <span data-ttu-id="3b729-151">From the Start screen, open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="3b729-151">From the Start screen, open **Server Manager**.</span></span>
2. <span data-ttu-id="3b729-152">Click **Local Server** in the left pane of the Server Manager window.</span><span class="sxs-lookup"><span data-stu-id="3b729-152">Click **Local Server** in the left pane of the Server Manager window.</span></span>

    ![Launch Server Manager on virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. <span data-ttu-id="3b729-154">Click **WORKGROUP** under the **PROPERTIES** section.</span><span class="sxs-lookup"><span data-stu-id="3b729-154">Click **WORKGROUP** under the **PROPERTIES** section.</span></span> <span data-ttu-id="3b729-155">In the **System Properties** property page, click **Change** to join the domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-155">In the **System Properties** property page, click **Change** to join the domain.</span></span>

    ![System Properties page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. <span data-ttu-id="3b729-157">Specify the domain name of your Azure AD Domain Services managed domain in the **Domain** textbox and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3b729-157">Specify the domain name of your Azure AD Domain Services managed domain in the **Domain** textbox and click **OK**.</span></span>

    ![Specify the domain to be joined](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. <span data-ttu-id="3b729-159">You are prompted to enter your credentials to join the domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-159">You are prompted to enter your credentials to join the domain.</span></span> <span data-ttu-id="3b729-160">Ensure that you **specify the credentials for a user belonging to the AAD DC Administrators** group.</span><span class="sxs-lookup"><span data-stu-id="3b729-160">Ensure that you **specify the credentials for a user belonging to the AAD DC Administrators** group.</span></span> <span data-ttu-id="3b729-161">Only members of this group have privileges to join machines to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-161">Only members of this group have privileges to join machines to the managed domain.</span></span>

    ![Specify credentials for domain join](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. <span data-ttu-id="3b729-163">You can specify credentials in either of the following ways:</span><span class="sxs-lookup"><span data-stu-id="3b729-163">You can specify credentials in either of the following ways:</span></span>

   * <span data-ttu-id="3b729-164">UPN format: Specify the UPN suffix for the user account, as configured in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b729-164">UPN format: Specify the UPN suffix for the user account, as configured in Azure AD.</span></span> <span data-ttu-id="3b729-165">In this example, the UPN suffix of the user 'bob' is 'bob@domainservicespreview.onmicrosoft.com'.</span><span class="sxs-lookup"><span data-stu-id="3b729-165">In this example, the UPN suffix of the user 'bob' is 'bob@domainservicespreview.onmicrosoft.com'.</span></span>
   * <span data-ttu-id="3b729-166">SAMAccountName format: You can specify the account name in the SAMAccountName format.</span><span class="sxs-lookup"><span data-stu-id="3b729-166">SAMAccountName format: You can specify the account name in the SAMAccountName format.</span></span> <span data-ttu-id="3b729-167">In this example, the user 'bob' would need to enter 'CONTOSO100\bob'.</span><span class="sxs-lookup"><span data-stu-id="3b729-167">In this example, the user 'bob' would need to enter 'CONTOSO100\bob'.</span></span>

     > [!NOTE]
     > **We recommend using the UPN format to specify credentials.** The SAMAccountName may be auto-generated if a user's UPN prefix is overly long (for example, 'joereallylongnameuser'). If multiple users have the same UPN prefix (for example, 'bob') in your Azure AD tenant, their SAMAccountName format may be auto-generated by the service. In these cases, the UPN format can be used reliably to log in to the domain.
     >
     >
7. <span data-ttu-id="3b729-172">After domain join is successful, you see the following message welcoming you to the domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-172">After domain join is successful, you see the following message welcoming you to the domain.</span></span> <span data-ttu-id="3b729-173">Restart the virtual machine for the domain join operation to complete.</span><span class="sxs-lookup"><span data-stu-id="3b729-173">Restart the virtual machine for the domain join operation to complete.</span></span>

    ![Welcome to the domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="3b729-175">Troubleshooting domain join</span><span class="sxs-lookup"><span data-stu-id="3b729-175">Troubleshooting domain join</span></span>
### <a name="connectivity-issues"></a><span data-ttu-id="3b729-176">Connectivity issues</span><span class="sxs-lookup"><span data-stu-id="3b729-176">Connectivity issues</span></span>
<span data-ttu-id="3b729-177">If the virtual machine is unable to find the domain, refer to the following troubleshooting steps:</span><span class="sxs-lookup"><span data-stu-id="3b729-177">If the virtual machine is unable to find the domain, refer to the following troubleshooting steps:</span></span>

* <span data-ttu-id="3b729-178">Ensure that the virtual machine is connected to the same virtual network as that you've enabled Domain Services in.</span><span class="sxs-lookup"><span data-stu-id="3b729-178">Ensure that the virtual machine is connected to the same virtual network as that you've enabled Domain Services in.</span></span> <span data-ttu-id="3b729-179">If not, the virtual machine is unable to connect to the domain and therefore is unable to join the domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-179">If not, the virtual machine is unable to connect to the domain and therefore is unable to join the domain.</span></span>
* <span data-ttu-id="3b729-180">If the virtual machine is connected to another virtual network, ensure that this virtual network is connected to the virtual network in which you've enabled Domain Services.</span><span class="sxs-lookup"><span data-stu-id="3b729-180">If the virtual machine is connected to another virtual network, ensure that this virtual network is connected to the virtual network in which you've enabled Domain Services.</span></span>
* <span data-ttu-id="3b729-181">Try to ping the domain using the domain name of the managed domain (for example, 'ping contoso100.com').</span><span class="sxs-lookup"><span data-stu-id="3b729-181">Try to ping the domain using the domain name of the managed domain (for example, 'ping contoso100.com').</span></span> <span data-ttu-id="3b729-182">If you're unable to do so, try to ping the IP addresses for the domain displayed on the page where you enabled Azure AD Domain Services (for example, 'ping 10.0.0.4').</span><span class="sxs-lookup"><span data-stu-id="3b729-182">If you're unable to do so, try to ping the IP addresses for the domain displayed on the page where you enabled Azure AD Domain Services (for example, 'ping 10.0.0.4').</span></span> <span data-ttu-id="3b729-183">If you're able to ping the IP address but not the domain, DNS may be incorrectly configured.</span><span class="sxs-lookup"><span data-stu-id="3b729-183">If you're able to ping the IP address but not the domain, DNS may be incorrectly configured.</span></span> <span data-ttu-id="3b729-184">You may not have configured the IP addresses of the domain as DNS servers for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="3b729-184">You may not have configured the IP addresses of the domain as DNS servers for the virtual network.</span></span>
* <span data-ttu-id="3b729-185">Try flushing the DNS resolver cache on the virtual machine ('ipconfig /flushdns').</span><span class="sxs-lookup"><span data-stu-id="3b729-185">Try flushing the DNS resolver cache on the virtual machine ('ipconfig /flushdns').</span></span>

<span data-ttu-id="3b729-186">If you get to the dialog box that asks for credentials to join the domain, you do not have connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="3b729-186">If you get to the dialog box that asks for credentials to join the domain, you do not have connectivity issues.</span></span>

### <a name="credentials-related-issues"></a><span data-ttu-id="3b729-187">Credentials-related issues</span><span class="sxs-lookup"><span data-stu-id="3b729-187">Credentials-related issues</span></span>
<span data-ttu-id="3b729-188">Refer to the following steps if you're having trouble with credentials and are unable to join the domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-188">Refer to the following steps if you're having trouble with credentials and are unable to join the domain.</span></span>

* <span data-ttu-id="3b729-189">Try using the UPN format to specify credentials.</span><span class="sxs-lookup"><span data-stu-id="3b729-189">Try using the UPN format to specify credentials.</span></span> <span data-ttu-id="3b729-190">The SAMAccountName for your account may be auto-generated if there are multiple users with the same UPN prefix in your tenant or if your UPN prefix is overly long.</span><span class="sxs-lookup"><span data-stu-id="3b729-190">The SAMAccountName for your account may be auto-generated if there are multiple users with the same UPN prefix in your tenant or if your UPN prefix is overly long.</span></span> <span data-ttu-id="3b729-191">Therefore, the SAMAccountName format for your account may be different from what you expect or use in your on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-191">Therefore, the SAMAccountName format for your account may be different from what you expect or use in your on-premises domain.</span></span>
* <span data-ttu-id="3b729-192">Try to use the credentials of a user account that belongs to the 'AAD DC Administrators' group to join machines to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="3b729-192">Try to use the credentials of a user account that belongs to the 'AAD DC Administrators' group to join machines to the managed domain.</span></span>
* <span data-ttu-id="3b729-193">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span><span class="sxs-lookup"><span data-stu-id="3b729-193">Ensure that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) in accordance with the steps outlined in the Getting Started guide.</span></span>
* <span data-ttu-id="3b729-194">Ensure that you use the UPN of the user as configured in Azure AD (for example, 'bob@domainservicespreview.onmicrosoft.com') to sign in.</span><span class="sxs-lookup"><span data-stu-id="3b729-194">Ensure that you use the UPN of the user as configured in Azure AD (for example, 'bob@domainservicespreview.onmicrosoft.com') to sign in.</span></span>
* <span data-ttu-id="3b729-195">Ensure that you have waited long enough for password synchronization to complete as specified in the Getting Started guide.</span><span class="sxs-lookup"><span data-stu-id="3b729-195">Ensure that you have waited long enough for password synchronization to complete as specified in the Getting Started guide.</span></span>

## <a name="related-content"></a><span data-ttu-id="3b729-196">Related Content</span><span class="sxs-lookup"><span data-stu-id="3b729-196">Related Content</span></span>
* [<span data-ttu-id="3b729-197">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="3b729-197">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="3b729-198">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="3b729-198">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)











