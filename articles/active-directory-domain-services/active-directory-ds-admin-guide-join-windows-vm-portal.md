---
title: 'Azure Active Directory Domain Services: Join a Windows Server VM to a managed domain | Microsoft Docs'
description: Join a Windows Server virtual machine to Azure AD DS
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 29316313-c76c-4fb9-8954-5fa5ec82609e
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/21/2018
ms.author: maheshu
ms.openlocfilehash: f9ee68fda3bb5e0f5302c8d5c96da0515c05ce1d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966811"
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="1396c-103">Join a Windows Server virtual machine to a managed domain</span><span class="sxs-lookup"><span data-stu-id="1396c-103">Join a Windows Server virtual machine to a managed domain</span></span>
<span data-ttu-id="1396c-104">This article shows how to deploy a Windows Server virtual machine by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1396c-104">This article shows how to deploy a Windows Server virtual machine by using the Azure portal.</span></span> <span data-ttu-id="1396c-105">It then shows how to join the virtual machine to an Azure Active Directory Domain Services (Azure AD DS) managed domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-105">It then shows how to join the virtual machine to an Azure Active Directory Domain Services (Azure AD DS) managed domain.</span></span>

[!INCLUDE [active-directory-ds-prerequisites.md](../../includes/active-directory-ds-prerequisites.md)]

## <a name="step-1-create-a-windows-server-virtual-machine"></a><span data-ttu-id="1396c-106">Step 1: Create a Windows Server virtual machine</span><span class="sxs-lookup"><span data-stu-id="1396c-106">Step 1: Create a Windows Server virtual machine</span></span>
<span data-ttu-id="1396c-107">To create a Windows virtual machine that's joined to the virtual network in which you've enabled Azure AD DS, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="1396c-107">To create a Windows virtual machine that's joined to the virtual network in which you've enabled Azure AD DS, do the following steps:</span></span>

1. <span data-ttu-id="1396c-108">Sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1396c-108">Sign in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="1396c-109">At the top of the left pane, select **New**.</span><span class="sxs-lookup"><span data-stu-id="1396c-109">At the top of the left pane, select **New**.</span></span>
3. <span data-ttu-id="1396c-110">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="1396c-110">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span>

    ![The Windows Server 2016 Datacenter link](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)

4. <span data-ttu-id="1396c-112">In the **Basics** pane of the wizard, configure the basic settings for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1396c-112">In the **Basics** pane of the wizard, configure the basic settings for the virtual machine.</span></span>

    ![The Basics pane](./media/active-directory-domain-services-admin-guide/create-windows-vm-basics.png)

    > [!TIP]
    > <span data-ttu-id="1396c-114">The username and password you enter here are for a local administrator account that's used to log on to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1396c-114">The username and password you enter here are for a local administrator account that's used to log on to the virtual machine.</span></span> <span data-ttu-id="1396c-115">Pick a strong password to protect the virtual machine against password brute-force attacks.</span><span class="sxs-lookup"><span data-stu-id="1396c-115">Pick a strong password to protect the virtual machine against password brute-force attacks.</span></span> <span data-ttu-id="1396c-116">Do not enter a domain user account's credentials here.</span><span class="sxs-lookup"><span data-stu-id="1396c-116">Do not enter a domain user account's credentials here.</span></span>
    >

5. <span data-ttu-id="1396c-117">Select a **Size** for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1396c-117">Select a **Size** for the virtual machine.</span></span> <span data-ttu-id="1396c-118">To view more sizes, select **View all** or change the **Supported disk type** filter.</span><span class="sxs-lookup"><span data-stu-id="1396c-118">To view more sizes, select **View all** or change the **Supported disk type** filter.</span></span>

    ![The "Choose a size" pane](./media/active-directory-domain-services-admin-guide/create-windows-vm-size.png)

6. <span data-ttu-id="1396c-120">In the **Settings** pane, select the virtual network in which your Azure AD DS-managed domain is deployed.</span><span class="sxs-lookup"><span data-stu-id="1396c-120">In the **Settings** pane, select the virtual network in which your Azure AD DS-managed domain is deployed.</span></span> <span data-ttu-id="1396c-121">Pick a different subnet than the one that your managed domain is deployed into.</span><span class="sxs-lookup"><span data-stu-id="1396c-121">Pick a different subnet than the one that your managed domain is deployed into.</span></span> <span data-ttu-id="1396c-122">For the other settings, keep the defaults, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1396c-122">For the other settings, keep the defaults, and then select **OK**.</span></span>

    ![Virtual network settings for the virtual machine](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

    > [!TIP]
    > <span data-ttu-id="1396c-124">**Pick the right virtual network and subnet.**</span><span class="sxs-lookup"><span data-stu-id="1396c-124">**Pick the right virtual network and subnet.**</span></span>
    >
    > <span data-ttu-id="1396c-125">Select either the virtual network in which your managed domain is deployed or a virtual network that is connected to it by using virtual network peering.</span><span class="sxs-lookup"><span data-stu-id="1396c-125">Select either the virtual network in which your managed domain is deployed or a virtual network that is connected to it by using virtual network peering.</span></span> <span data-ttu-id="1396c-126">If you select an unconnected virtual network, you cannot join the virtual machine to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-126">If you select an unconnected virtual network, you cannot join the virtual machine to the managed domain.</span></span>
    >
    > <span data-ttu-id="1396c-127">We recommend deploying your managed domain into a dedicated subnet.</span><span class="sxs-lookup"><span data-stu-id="1396c-127">We recommend deploying your managed domain into a dedicated subnet.</span></span> <span data-ttu-id="1396c-128">Therefore, do not pick the subnet in which you've enabled your managed domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-128">Therefore, do not pick the subnet in which you've enabled your managed domain.</span></span>

7. <span data-ttu-id="1396c-129">For the other settings, keep the defaults, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1396c-129">For the other settings, keep the defaults, and then select **OK**.</span></span>
8. <span data-ttu-id="1396c-130">On the **Purchase** page, review the settings, and then select **OK** to deploy the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1396c-130">On the **Purchase** page, review the settings, and then select **OK** to deploy the virtual machine.</span></span>
9. <span data-ttu-id="1396c-131">The VM deployment is pinned to the Azure portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="1396c-131">The VM deployment is pinned to the Azure portal dashboard.</span></span>

    ![Done](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
10. <span data-ttu-id="1396c-133">After the deployment is completed, you can view information about the VM on the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="1396c-133">After the deployment is completed, you can view information about the VM on the **Overview** page.</span></span>


## <a name="step-2-connect-to-the-windows-server-virtual-machine-by-using-the-local-administrator-account"></a><span data-ttu-id="1396c-134">Step 2: Connect to the Windows Server virtual machine by using the local administrator account</span><span class="sxs-lookup"><span data-stu-id="1396c-134">Step 2: Connect to the Windows Server virtual machine by using the local administrator account</span></span>
<span data-ttu-id="1396c-135">Next, connect to the newly created Windows Server virtual machine to join it to the domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-135">Next, connect to the newly created Windows Server virtual machine to join it to the domain.</span></span> <span data-ttu-id="1396c-136">Use the local administrator credentials that you specified when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1396c-136">Use the local administrator credentials that you specified when you created the virtual machine.</span></span>

<span data-ttu-id="1396c-137">To connect to the virtual machine, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1396c-137">To connect to the virtual machine, perform the following steps:</span></span>

1. <span data-ttu-id="1396c-138">In the **Overview** pane, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="1396c-138">In the **Overview** pane, select **Connect**.</span></span>  
    <span data-ttu-id="1396c-139">A Remote Desktop Protocol (.rdp) file is created and downloaded.</span><span class="sxs-lookup"><span data-stu-id="1396c-139">A Remote Desktop Protocol (.rdp) file is created and downloaded.</span></span>

    ![Connect to Windows virtual machine](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)

2. <span data-ttu-id="1396c-141">To connect to your VM, open the downloaded RDP file.</span><span class="sxs-lookup"><span data-stu-id="1396c-141">To connect to your VM, open the downloaded RDP file.</span></span> <span data-ttu-id="1396c-142">If prompted, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="1396c-142">If prompted, select **Connect**.</span></span>
3. <span data-ttu-id="1396c-143">Enter your **local administrator credentials**, which you specified when you created the virtual machine (for example, *localhost\mahesh*).</span><span class="sxs-lookup"><span data-stu-id="1396c-143">Enter your **local administrator credentials**, which you specified when you created the virtual machine (for example, *localhost\mahesh*).</span></span>
4. <span data-ttu-id="1396c-144">If you see a certificate warning during the sign-in process, select **Yes** or **Continue** to connect.</span><span class="sxs-lookup"><span data-stu-id="1396c-144">If you see a certificate warning during the sign-in process, select **Yes** or **Continue** to connect.</span></span>

<span data-ttu-id="1396c-145">At this point, you should be logged on to the newly created Windows virtual machine with your local administrator credentials.</span><span class="sxs-lookup"><span data-stu-id="1396c-145">At this point, you should be logged on to the newly created Windows virtual machine with your local administrator credentials.</span></span> <span data-ttu-id="1396c-146">The next step is to join the virtual machine to the domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-146">The next step is to join the virtual machine to the domain.</span></span>


## <a name="step-3-join-the-windows-server-virtual-machine-to-the-azure-ad-ds-managed-domain"></a><span data-ttu-id="1396c-147">Step 3: Join the Windows Server virtual machine to the Azure AD DS-managed domain</span><span class="sxs-lookup"><span data-stu-id="1396c-147">Step 3: Join the Windows Server virtual machine to the Azure AD DS-managed domain</span></span>
<span data-ttu-id="1396c-148">To join the Windows Server virtual machine to the Azure AD DS-managed domain, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="1396c-148">To join the Windows Server virtual machine to the Azure AD DS-managed domain, complete the following steps:</span></span>

1. <span data-ttu-id="1396c-149">Connect to the Windows Server VM, as shown in "Step 2."</span><span class="sxs-lookup"><span data-stu-id="1396c-149">Connect to the Windows Server VM, as shown in "Step 2."</span></span> <span data-ttu-id="1396c-150">On the **Start** screen, open **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="1396c-150">On the **Start** screen, open **Server Manager**.</span></span>
2. <span data-ttu-id="1396c-151">In the left pane of the **Server Manager** window, select **Local Server**.</span><span class="sxs-lookup"><span data-stu-id="1396c-151">In the left pane of the **Server Manager** window, select **Local Server**.</span></span>

    ![The Server Manager window on the virtual machine](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)

3. <span data-ttu-id="1396c-153">Under **Properties**, select **Workgroup**.</span><span class="sxs-lookup"><span data-stu-id="1396c-153">Under **Properties**, select **Workgroup**.</span></span>
4. <span data-ttu-id="1396c-154">In the **System Properties** window, select **Change** to join the domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-154">In the **System Properties** window, select **Change** to join the domain.</span></span>

    ![The System Properties window](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)

5. <span data-ttu-id="1396c-156">In the **Domain** box, specify the name of your Azure AD DS-managed domain, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1396c-156">In the **Domain** box, specify the name of your Azure AD DS-managed domain, and then select **OK**.</span></span>

    ![Specify the domain to be joined](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)

6. <span data-ttu-id="1396c-158">You're asked to enter your credentials to join the domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-158">You're asked to enter your credentials to join the domain.</span></span> <span data-ttu-id="1396c-159">Use the credentials for a *user that belongs to the Azure AD DC administrators group*.</span><span class="sxs-lookup"><span data-stu-id="1396c-159">Use the credentials for a *user that belongs to the Azure AD DC administrators group*.</span></span> <span data-ttu-id="1396c-160">Only members of this group have privileges to join machines to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-160">Only members of this group have privileges to join machines to the managed domain.</span></span>

    ![The Windows Security window for specifying credentials](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)

7. <span data-ttu-id="1396c-162">You can specify credentials in either of the following ways:</span><span class="sxs-lookup"><span data-stu-id="1396c-162">You can specify credentials in either of the following ways:</span></span>

   * <span data-ttu-id="1396c-163">**UPN format**: (Recommended) Specify the user principal name (UPN) suffix for the user account, as configured in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1396c-163">**UPN format**: (Recommended) Specify the user principal name (UPN) suffix for the user account, as configured in Azure AD.</span></span> <span data-ttu-id="1396c-164">In this example, the UPN suffix of the user *bob* is *bob@domainservicespreview.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="1396c-164">In this example, the UPN suffix of the user *bob* is *bob@domainservicespreview.onmicrosoft.com*.</span></span>

   * <span data-ttu-id="1396c-165">**SAMAccountName format**: You can specify the account name in the SAMAccountName format.</span><span class="sxs-lookup"><span data-stu-id="1396c-165">**SAMAccountName format**: You can specify the account name in the SAMAccountName format.</span></span> <span data-ttu-id="1396c-166">In this example, the user *bob* would need to enter *CONTOSO100\bob*.</span><span class="sxs-lookup"><span data-stu-id="1396c-166">In this example, the user *bob* would need to enter *CONTOSO100\bob*.</span></span>

     > [!TIP]
     > <span data-ttu-id="1396c-167">**We recommend using the UPN format to specify credentials.**</span><span class="sxs-lookup"><span data-stu-id="1396c-167">**We recommend using the UPN format to specify credentials.**</span></span>
     >
     > <span data-ttu-id="1396c-168">If a user's UPN prefix is overly long (for example, *joehasareallylongname*), the SAMAccountName might be auto-generated.</span><span class="sxs-lookup"><span data-stu-id="1396c-168">If a user's UPN prefix is overly long (for example, *joehasareallylongname*), the SAMAccountName might be auto-generated.</span></span> <span data-ttu-id="1396c-169">If multiple users have the same UPN prefix (for example, *bob*) in your Azure AD tenant, their SAMAccountName format might be auto-generated by the service.</span><span class="sxs-lookup"><span data-stu-id="1396c-169">If multiple users have the same UPN prefix (for example, *bob*) in your Azure AD tenant, their SAMAccountName format might be auto-generated by the service.</span></span> <span data-ttu-id="1396c-170">In these cases, the UPN format can be used reliably to log on to the domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-170">In these cases, the UPN format can be used reliably to log on to the domain.</span></span>
     >

8. <span data-ttu-id="1396c-171">After you've successfully joined a domain, the following message welcomes you to the domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-171">After you've successfully joined a domain, the following message welcomes you to the domain.</span></span>

    ![Welcome to the domain](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

9. <span data-ttu-id="1396c-173">To complete joining the domain, restart the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1396c-173">To complete joining the domain, restart the virtual machine.</span></span>

## <a name="troubleshoot-joining-a-domain"></a><span data-ttu-id="1396c-174">Troubleshoot joining a domain</span><span class="sxs-lookup"><span data-stu-id="1396c-174">Troubleshoot joining a domain</span></span>
### <a name="connectivity-issues"></a><span data-ttu-id="1396c-175">Connectivity issues</span><span class="sxs-lookup"><span data-stu-id="1396c-175">Connectivity issues</span></span>
<span data-ttu-id="1396c-176">If the virtual machine is unable to find the domain, try the following troubleshooting steps:</span><span class="sxs-lookup"><span data-stu-id="1396c-176">If the virtual machine is unable to find the domain, try the following troubleshooting steps:</span></span>

* <span data-ttu-id="1396c-177">Verify the virtual machine is connected to the same virtual network Azure AD DS is enabled in.</span><span class="sxs-lookup"><span data-stu-id="1396c-177">Verify the virtual machine is connected to the same virtual network Azure AD DS is enabled in.</span></span> <span data-ttu-id="1396c-178">Otherwise, the virtual machine is unable to connect to or join the domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-178">Otherwise, the virtual machine is unable to connect to or join the domain.</span></span>

* <span data-ttu-id="1396c-179">Verify the virtual machine is on a virtual network that is in turn connected to the virtual network Azure AD DS is enabled in.</span><span class="sxs-lookup"><span data-stu-id="1396c-179">Verify the virtual machine is on a virtual network that is in turn connected to the virtual network Azure AD DS is enabled in.</span></span>

* <span data-ttu-id="1396c-180">Try to ping the DNS domain name of the managed domain (for example, *ping contoso100.com*).</span><span class="sxs-lookup"><span data-stu-id="1396c-180">Try to ping the DNS domain name of the managed domain (for example, *ping contoso100.com*).</span></span> <span data-ttu-id="1396c-181">If you're unable to do so, try to ping the IP addresses for the domain that's displayed on the page where you enabled Azure AD DS (for example, *ping 10.0.0.4*).</span><span class="sxs-lookup"><span data-stu-id="1396c-181">If you're unable to do so, try to ping the IP addresses for the domain that's displayed on the page where you enabled Azure AD DS (for example, *ping 10.0.0.4*).</span></span> <span data-ttu-id="1396c-182">If you can ping the IP address but not the domain, DNS may be incorrectly configured.</span><span class="sxs-lookup"><span data-stu-id="1396c-182">If you can ping the IP address but not the domain, DNS may be incorrectly configured.</span></span> <span data-ttu-id="1396c-183">Check to see whether the IP addresses of the domain are configured as DNS servers for the virtual network.</span><span class="sxs-lookup"><span data-stu-id="1396c-183">Check to see whether the IP addresses of the domain are configured as DNS servers for the virtual network.</span></span>

* <span data-ttu-id="1396c-184">Try flushing the DNS resolver cache on the virtual machine (*ipconfig /flushdns*).</span><span class="sxs-lookup"><span data-stu-id="1396c-184">Try flushing the DNS resolver cache on the virtual machine (*ipconfig /flushdns*).</span></span>

<span data-ttu-id="1396c-185">If a window is displayed that asks for credentials to join the domain, you do not have connectivity issues.</span><span class="sxs-lookup"><span data-stu-id="1396c-185">If a window is displayed that asks for credentials to join the domain, you do not have connectivity issues.</span></span>

### <a name="credentials-related-issues"></a><span data-ttu-id="1396c-186">Credentials-related issues</span><span class="sxs-lookup"><span data-stu-id="1396c-186">Credentials-related issues</span></span>
<span data-ttu-id="1396c-187">If you're having trouble with credentials and are unable to join the domain, try the following troubleshooting steps:</span><span class="sxs-lookup"><span data-stu-id="1396c-187">If you're having trouble with credentials and are unable to join the domain, try the following troubleshooting steps:</span></span>

* <span data-ttu-id="1396c-188">Try using the UPN format to specify credentials.</span><span class="sxs-lookup"><span data-stu-id="1396c-188">Try using the UPN format to specify credentials.</span></span> <span data-ttu-id="1396c-189">If there are many users with the same UPN prefix in your tenant or if your UPN prefix is overly long, the SAMAccountName for your account may be auto-generated.</span><span class="sxs-lookup"><span data-stu-id="1396c-189">If there are many users with the same UPN prefix in your tenant or if your UPN prefix is overly long, the SAMAccountName for your account may be auto-generated.</span></span> <span data-ttu-id="1396c-190">In these cases, the SAMAccountName format for your account may be different from what you expect or use in your on-premises domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-190">In these cases, the SAMAccountName format for your account may be different from what you expect or use in your on-premises domain.</span></span>

* <span data-ttu-id="1396c-191">Try to use the credentials of a user account that belongs to the *AAD DC Administrators* group.</span><span class="sxs-lookup"><span data-stu-id="1396c-191">Try to use the credentials of a user account that belongs to the *AAD DC Administrators* group.</span></span>

* <span data-ttu-id="1396c-192">Check that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) to your managed domain.</span><span class="sxs-lookup"><span data-stu-id="1396c-192">Check that you have [enabled password synchronization](active-directory-ds-getting-started-password-sync.md) to your managed domain.</span></span>

* <span data-ttu-id="1396c-193">Check that you've used the UPN of the user as configured in Azure AD (for example, *bob@domainservicespreview.onmicrosoft.com*) to sign in.</span><span class="sxs-lookup"><span data-stu-id="1396c-193">Check that you've used the UPN of the user as configured in Azure AD (for example, *bob@domainservicespreview.onmicrosoft.com*) to sign in.</span></span>

* <span data-ttu-id="1396c-194">Wait long enough for password synchronization to be completed, as specified in the getting started guide.</span><span class="sxs-lookup"><span data-stu-id="1396c-194">Wait long enough for password synchronization to be completed, as specified in the getting started guide.</span></span>

## <a name="related-content"></a><span data-ttu-id="1396c-195">Related content</span><span class="sxs-lookup"><span data-stu-id="1396c-195">Related content</span></span>
* [<span data-ttu-id="1396c-196">Azure AD DS getting started guide</span><span class="sxs-lookup"><span data-stu-id="1396c-196">Azure AD DS getting started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="1396c-197">Administer an Azure AD DS-managed domain</span><span class="sxs-lookup"><span data-stu-id="1396c-197">Administer an Azure AD DS-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
