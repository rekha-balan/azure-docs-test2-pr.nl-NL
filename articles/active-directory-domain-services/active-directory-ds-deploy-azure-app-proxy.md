---
title: 'Azure Active Directory Domain Services: Deploy Azure Active Directory Application Proxy | Microsoft Docs'
description: Use Azure AD Application Proxy on Azure Active Directory Domain Services managed domains
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d78ad9082f0cd8bf3f038fdf42b827597897d0c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552651"
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="2ca94-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="2ca94-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="2ca94-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span><span class="sxs-lookup"><span data-stu-id="2ca94-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="2ca94-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span><span class="sxs-lookup"><span data-stu-id="2ca94-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span></span> <span data-ttu-id="2ca94-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span><span class="sxs-lookup"><span data-stu-id="2ca94-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span></span>

<span data-ttu-id="2ca94-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ca94-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="2ca94-108">Before you begin</span><span class="sxs-lookup"><span data-stu-id="2ca94-108">Before you begin</span></span>
<span data-ttu-id="2ca94-109">To perform the tasks listed in this article, you need:</span><span class="sxs-lookup"><span data-stu-id="2ca94-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="2ca94-110">A valid **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="2ca94-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="2ca94-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span><span class="sxs-lookup"><span data-stu-id="2ca94-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="2ca94-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="2ca94-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="2ca94-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="2ca94-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="2ca94-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="2ca94-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="2ca94-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="2ca94-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="2ca94-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="2ca94-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="2ca94-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ca94-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="2ca94-118">Click **Azure Active Directory** to bring up the directory overview.</span><span class="sxs-lookup"><span data-stu-id="2ca94-118">Click **Azure Active Directory** to bring up the directory overview.</span></span> <span data-ttu-id="2ca94-119">Click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2ca94-119">Click **Enterprise applications**.</span></span>

    ![Select Azure AD directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="2ca94-121">Click **Application proxy**.</span><span class="sxs-lookup"><span data-stu-id="2ca94-121">Click **Application proxy**.</span></span> <span data-ttu-id="2ca94-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span><span class="sxs-lookup"><span data-stu-id="2ca94-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span></span> <span data-ttu-id="2ca94-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2ca94-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span></span>

    ![Enable App Proxy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="2ca94-125">To download the connector, click the **Connector** button.</span><span class="sxs-lookup"><span data-stu-id="2ca94-125">To download the connector, click the **Connector** button.</span></span>

    ![Download connector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="2ca94-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span><span class="sxs-lookup"><span data-stu-id="2ca94-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span></span>

    ![Confirm download](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-to-deploy-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="2ca94-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span><span class="sxs-lookup"><span data-stu-id="2ca94-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="2ca94-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span><span class="sxs-lookup"><span data-stu-id="2ca94-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span></span> <span data-ttu-id="2ca94-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span><span class="sxs-lookup"><span data-stu-id="2ca94-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span></span> <span data-ttu-id="2ca94-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span><span class="sxs-lookup"><span data-stu-id="2ca94-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="2ca94-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="2ca94-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="2ca94-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span></span>

<span data-ttu-id="2ca94-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2ca94-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="2ca94-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span><span class="sxs-lookup"><span data-stu-id="2ca94-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="2ca94-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span></span> <span data-ttu-id="2ca94-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2ca94-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="2ca94-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span><span class="sxs-lookup"><span data-stu-id="2ca94-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="2ca94-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2ca94-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span></span> <span data-ttu-id="2ca94-141">Accept the software license terms.</span><span class="sxs-lookup"><span data-stu-id="2ca94-141">Accept the software license terms.</span></span>

    ![Accept terms for install](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="2ca94-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="2ca94-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="2ca94-144">Provide your **Azure AD global administrator credentials**.</span><span class="sxs-lookup"><span data-stu-id="2ca94-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="2ca94-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="2ca94-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="2ca94-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span><span class="sxs-lookup"><span data-stu-id="2ca94-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="2ca94-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="2ca94-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span><span class="sxs-lookup"><span data-stu-id="2ca94-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span></span> <span data-ttu-id="2ca94-149">To allow access, follow the instructions in the error message.</span><span class="sxs-lookup"><span data-stu-id="2ca94-149">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="2ca94-150">Make sure that Internet Explorer Enhanced Security is off.</span><span class="sxs-lookup"><span data-stu-id="2ca94-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="2ca94-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="2ca94-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![Connector installed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="2ca94-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span><span class="sxs-lookup"><span data-stu-id="2ca94-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="2ca94-154">You should see a successful report after running the troubleshooter.</span><span class="sxs-lookup"><span data-stu-id="2ca94-154">You should see a successful report after running the troubleshooter.</span></span>

    ![Troubleshooter success](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="2ca94-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="2ca94-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="2ca94-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="2ca94-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span></span> <span data-ttu-id="2ca94-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2ca94-159">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2ca94-159">Next Steps</span></span>
<span data-ttu-id="2ca94-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="2ca94-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span></span> <span data-ttu-id="2ca94-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span><span class="sxs-lookup"><span data-stu-id="2ca94-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="2ca94-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="2ca94-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span></span> <span data-ttu-id="2ca94-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="2ca94-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="2ca94-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span><span class="sxs-lookup"><span data-stu-id="2ca94-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="2ca94-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span><span class="sxs-lookup"><span data-stu-id="2ca94-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="2ca94-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span></span> <span data-ttu-id="2ca94-168">Use the resource-based KCD mechanism on managed domains for increased security.</span><span class="sxs-lookup"><span data-stu-id="2ca94-168">Use the resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="2ca94-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span><span class="sxs-lookup"><span data-stu-id="2ca94-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="2ca94-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span><span class="sxs-lookup"><span data-stu-id="2ca94-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span></span> <span data-ttu-id="2ca94-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="2ca94-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="2ca94-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span><span class="sxs-lookup"><span data-stu-id="2ca94-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="2ca94-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="2ca94-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2ca94-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2ca94-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="2ca94-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span><span class="sxs-lookup"><span data-stu-id="2ca94-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="2ca94-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span><span class="sxs-lookup"><span data-stu-id="2ca94-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="2ca94-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span><span class="sxs-lookup"><span data-stu-id="2ca94-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="2ca94-178">Related Content</span><span class="sxs-lookup"><span data-stu-id="2ca94-178">Related Content</span></span>
* [<span data-ttu-id="2ca94-179">Azure AD Domain Services - Getting Started guide</span><span class="sxs-lookup"><span data-stu-id="2ca94-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2ca94-180">Configure Kerberos Constrained Delegation on a managed domain</span><span class="sxs-lookup"><span data-stu-id="2ca94-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="2ca94-181">Kerberos Constrained Delegation Overview</span><span class="sxs-lookup"><span data-stu-id="2ca94-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)








