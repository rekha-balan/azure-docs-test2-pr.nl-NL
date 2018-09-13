---
title: Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell
description: How to configure your azure cloud service application using PowerShell to allow remote desktop connections
services: cloud-services
documentationcenter: ''
author: thraka
manager: timlt
editor: ''
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: adegeo
ms.openlocfilehash: a78fc57d264e9f8074c94b334b24bbf1b7871d08
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555484"
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="3e154-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e154-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure classic portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="3e154-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span><span class="sxs-lookup"><span data-stu-id="3e154-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="3e154-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span><span class="sxs-lookup"><span data-stu-id="3e154-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="3e154-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e154-110">This article describes how to enable remote desktop on your Cloud Service Roles using PowerShell.</span></span> <span data-ttu-id="3e154-111">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the prerequisites needed for this article.</span><span class="sxs-lookup"><span data-stu-id="3e154-111">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the prerequisites needed for this article.</span></span> <span data-ttu-id="3e154-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span><span class="sxs-lookup"><span data-stu-id="3e154-112">PowerShell utilizes the Remote Desktop Extension so you can enable Remote Desktop after the application is deployed.</span></span>

## <a name="configure-remote-desktop-from-powershell"></a><span data-ttu-id="3e154-113">Configure Remote Desktop from PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e154-113">Configure Remote Desktop from PowerShell</span></span>
<span data-ttu-id="3e154-114">The [Set-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495117.aspx) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span><span class="sxs-lookup"><span data-stu-id="3e154-114">The [Set-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495117.aspx) cmdlet allows you to enable Remote Desktop on specified roles or all roles of your cloud service deployment.</span></span> <span data-ttu-id="3e154-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span><span class="sxs-lookup"><span data-stu-id="3e154-115">The cmdlet lets you specify the Username and Password for the remote desktop user through the *Credential* parameter that accepts a PSCredential object.</span></span>

<span data-ttu-id="3e154-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e154-116">If you are using PowerShell interactively, you can easily set the PSCredential object by calling the [Get-Credentials](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

```
$remoteusercredentials = Get-Credential
```

<span data-ttu-id="3e154-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span><span class="sxs-lookup"><span data-stu-id="3e154-117">This command displays a dialog box allowing you to enter the username and password for the remote user in a secure manner.</span></span>

<span data-ttu-id="3e154-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span><span class="sxs-lookup"><span data-stu-id="3e154-118">Since PowerShell helps in automation scenarios, you can also set up the **PSCredential** object in a way that doesn't require user interaction.</span></span> <span data-ttu-id="3e154-119">First, you need to set up a secure password.</span><span class="sxs-lookup"><span data-stu-id="3e154-119">First, you need to set up a secure password.</span></span> <span data-ttu-id="3e154-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e154-120">You begin with specifying a plain text password convert it to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span> <span data-ttu-id="3e154-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e154-121">Next you need to convert this secure string into an encrypted standard string using [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx).</span></span> <span data-ttu-id="3e154-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e154-122">Now you can save this encrypted standard string to a file using [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).</span></span>

<span data-ttu-id="3e154-123">You can also create a secure password file so that you don't have to type in the password every time.</span><span class="sxs-lookup"><span data-stu-id="3e154-123">You can also create a secure password file so that you don't have to type in the password every time.</span></span> <span data-ttu-id="3e154-124">Also, a secure password file is better than a plain text file.</span><span class="sxs-lookup"><span data-stu-id="3e154-124">Also, a secure password file is better than a plain text file.</span></span> <span data-ttu-id="3e154-125">Use the following PowerShell to create a secure password file:</span><span class="sxs-lookup"><span data-stu-id="3e154-125">Use the following PowerShell to create a secure password file:</span></span>

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> When setting the password, make sure that you meet the [complexity requirements](https://technet.microsoft.com/library/cc786468.aspx).
>
>

<span data-ttu-id="3e154-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e154-127">To create the credential object from the secure password file, you must read the file contents and convert them back to a secure string using [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).</span></span>

<span data-ttu-id="3e154-128">The [Set-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495117.aspx) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span><span class="sxs-lookup"><span data-stu-id="3e154-128">The [Set-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495117.aspx) cmdlet also accepts an *Expiration* parameter, which specifies a **DateTime** at which the user account expires.</span></span> <span data-ttu-id="3e154-129">For example, you could set the account to expire a few days from the current date and time.</span><span class="sxs-lookup"><span data-stu-id="3e154-129">For example, you could set the account to expire a few days from the current date and time.</span></span>

<span data-ttu-id="3e154-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span><span class="sxs-lookup"><span data-stu-id="3e154-130">This PowerShell example shows you how to set the Remote Desktop Extension on a cloud service:</span></span>

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
<span data-ttu-id="3e154-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span><span class="sxs-lookup"><span data-stu-id="3e154-131">You can also optionally specify the deployment slot and roles that you want to enable remote desktop on.</span></span> <span data-ttu-id="3e154-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span><span class="sxs-lookup"><span data-stu-id="3e154-132">If these parameters are not specified, the cmdlet enables remote desktop on all roles in the **Production** deployment slot.</span></span>

<span data-ttu-id="3e154-133">The Remote Desktop extension is associated with a deployment.</span><span class="sxs-lookup"><span data-stu-id="3e154-133">The Remote Desktop extension is associated with a deployment.</span></span> <span data-ttu-id="3e154-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span><span class="sxs-lookup"><span data-stu-id="3e154-134">If you create a new deployment for the service, you have to enable remote desktop on that deployment.</span></span> <span data-ttu-id="3e154-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span><span class="sxs-lookup"><span data-stu-id="3e154-135">If you always want to have remote desktop enabled, then you should consider integrating the PowerShell scripts into your deployment workflow.</span></span>

## <a name="remote-desktop-into-a-role-instance"></a><span data-ttu-id="3e154-136">Remote Desktop into a role instance</span><span class="sxs-lookup"><span data-stu-id="3e154-136">Remote Desktop into a role instance</span></span>
<span data-ttu-id="3e154-137">The [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span><span class="sxs-lookup"><span data-stu-id="3e154-137">The [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet is used to remote desktop into a specific role instance of your cloud service.</span></span> <span data-ttu-id="3e154-138">You can use the *LocalPath* parameter to download the RDP file locally.</span><span class="sxs-lookup"><span data-stu-id="3e154-138">You can use the *LocalPath* parameter to download the RDP file locally.</span></span> <span data-ttu-id="3e154-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span><span class="sxs-lookup"><span data-stu-id="3e154-139">Or you can use the *Launch* parameter to directly launch the Remote Desktop Connection dialog to access the cloud service role instance.</span></span>

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a><span data-ttu-id="3e154-140">Check if Remote Desktop extension is enabled on a service</span><span class="sxs-lookup"><span data-stu-id="3e154-140">Check if Remote Desktop extension is enabled on a service</span></span>
<span data-ttu-id="3e154-141">The [Get-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span><span class="sxs-lookup"><span data-stu-id="3e154-141">The [Get-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495261.aspx) cmdlet displays that remote desktop is enabled or disabled on a service deployment.</span></span> <span data-ttu-id="3e154-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span><span class="sxs-lookup"><span data-stu-id="3e154-142">The cmdlet returns the username for the remote desktop user and the roles that the remote desktop extension is enabled for.</span></span> <span data-ttu-id="3e154-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span><span class="sxs-lookup"><span data-stu-id="3e154-143">By default, this happens on the deployment slot and you can choose to use the staging slot instead.</span></span>

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a><span data-ttu-id="3e154-144">Remove Remote Desktop extension from a service</span><span class="sxs-lookup"><span data-stu-id="3e154-144">Remove Remote Desktop extension from a service</span></span>
<span data-ttu-id="3e154-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span><span class="sxs-lookup"><span data-stu-id="3e154-145">If you have already enabled the remote desktop extension on a deployment, and need to update the remote desktop settings, first remove the extension.</span></span> <span data-ttu-id="3e154-146">And enable it again with the new settings.</span><span class="sxs-lookup"><span data-stu-id="3e154-146">And enable it again with the new settings.</span></span> <span data-ttu-id="3e154-147">For example, if you want to set a new password for the remote user account, or the account expired.</span><span class="sxs-lookup"><span data-stu-id="3e154-147">For example, if you want to set a new password for the remote user account, or the account expired.</span></span> <span data-ttu-id="3e154-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span><span class="sxs-lookup"><span data-stu-id="3e154-148">Doing this is required on existing deployments that have the remote desktop extension enabled.</span></span> <span data-ttu-id="3e154-149">For new deployments, you can simply apply the extension directly.</span><span class="sxs-lookup"><span data-stu-id="3e154-149">For new deployments, you can simply apply the extension directly.</span></span>

<span data-ttu-id="3e154-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495280.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3e154-150">To remove the remote desktop extension from the deployment, you can use the [Remove-AzureServiceRemoteDesktopExtension](https://msdn.microsoft.com/library/azure/dn495280.aspx) cmdlet.</span></span> <span data-ttu-id="3e154-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span><span class="sxs-lookup"><span data-stu-id="3e154-151">You can also optionally specify the deployment slot and role from which you want to remove the remote desktop extension.</span></span>

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> To completely remove the extension configuration, you should call the *remove* cmdlet with the **UninstallConfiguration** parameter.
>
> The **UninstallConfiguration** parameter uninstalls any extension configuration that is applied to the service. Every extension configuration is associated with the service configuration. Calling the *remove* cmdlet without **UninstallConfiguration** disassociates the <mark>deployment</mark> from the extension configuration, thus effectively removing the extension. However, the extension configuration remains associated with the service.
>
>

## <a name="additional-resources"></a><span data-ttu-id="3e154-157">Additional resources</span><span class="sxs-lookup"><span data-stu-id="3e154-157">Additional resources</span></span>

<span data-ttu-id="3e154-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md#remote-desktop)</span><span class="sxs-lookup"><span data-stu-id="3e154-158">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md#remote-desktop)</span></span>
