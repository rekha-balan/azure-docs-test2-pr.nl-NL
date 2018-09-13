---
title: Connect to SQL Database using SQL Server Management Studio in Azure RemoteApp | Microsoft Docs
description: Use this tutorial to learn how to use SQL Server Management Studio in Azure RemoteApp for security and performance when connecting to SQL Database
services: sql-database
documentationcenter: ''
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: manage-how-to
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 82793c51df86805fb25ba285e78ec8cf8b6bf9bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552273"
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a><span data-ttu-id="1b26a-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span><span class="sxs-lookup"><span data-stu-id="1b26a-103">Use SQL Server Management Studio in Azure RemoteApp to connect to SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b26a-104">Azure RemoteApp is being discontinued.</span><span class="sxs-lookup"><span data-stu-id="1b26a-104">Azure RemoteApp is being discontinued.</span></span> <span data-ttu-id="1b26a-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="1b26a-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
>

## <a name="introduction"></a><span data-ttu-id="1b26a-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="1b26a-106">Introduction</span></span>
<span data-ttu-id="1b26a-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1b26a-107">This tutorial shows you how to use SQL Server Management Studio (SSMS) in Azure RemoteApp to connect to SQL Database.</span></span> <span data-ttu-id="1b26a-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b26a-108">It walks you through the process of setting up SQL Server Management Studio in Azure RemoteApp, explains the benefits, and shows security features that you can use in Azure Active Directory.</span></span>

<span data-ttu-id="1b26a-109">**Estimated time to complete:** 45 minutes</span><span class="sxs-lookup"><span data-stu-id="1b26a-109">**Estimated time to complete:** 45 minutes</span></span>

## <a name="ssms-in-azure-remoteapp"></a><span data-ttu-id="1b26a-110">SSMS in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1b26a-110">SSMS in Azure RemoteApp</span></span>
<span data-ttu-id="1b26a-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span><span class="sxs-lookup"><span data-stu-id="1b26a-111">Azure RemoteApp is an RDS service in Azure that delivers applications.</span></span> <span data-ttu-id="1b26a-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="1b26a-112">You can learn more about it here: [What is RemoteApp?](../remoteapp/remoteapp-whatis.md)</span></span>

<span data-ttu-id="1b26a-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span><span class="sxs-lookup"><span data-stu-id="1b26a-113">SSMS running in Azure RemoteApp gives you the same experience as running SSMS locally.</span></span>

![Screenshot showing SSMS running in Azure RemoteApp][1]

## <a name="benefits"></a><span data-ttu-id="1b26a-115">Benefits</span><span class="sxs-lookup"><span data-stu-id="1b26a-115">Benefits</span></span>
<span data-ttu-id="1b26a-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span><span class="sxs-lookup"><span data-stu-id="1b26a-116">There are many benefits to using SSMS in Azure RemoteApp, including:</span></span>

* <span data-ttu-id="1b26a-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span><span class="sxs-lookup"><span data-stu-id="1b26a-117">Port 1433 on Azure SQL server does not have to be exposed externally (outside of Azure).</span></span>
* <span data-ttu-id="1b26a-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span><span class="sxs-lookup"><span data-stu-id="1b26a-118">No need to keep adding and removing IP addresses in the Azure SQL server firewall.</span></span>
* <span data-ttu-id="1b26a-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span><span class="sxs-lookup"><span data-stu-id="1b26a-119">All Azure RemoteApp connections occur over HTTPS on port 443 using encrypted Remote Desktop protocol</span></span>
* <span data-ttu-id="1b26a-120">It is multi-user and can scale.</span><span class="sxs-lookup"><span data-stu-id="1b26a-120">It is multi-user and can scale.</span></span>
* <span data-ttu-id="1b26a-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1b26a-121">There is a performance gain from having SSMS in the same region as the SQL Database.</span></span>
* <span data-ttu-id="1b26a-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span><span class="sxs-lookup"><span data-stu-id="1b26a-122">You can audit use of Azure RemoteApp with the Premium edition of Azure Active Directory which has user activity reports.</span></span>
* <span data-ttu-id="1b26a-123">You can enable multi-factor authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="1b26a-123">You can enable multi-factor authentication (MFA).</span></span>
* <span data-ttu-id="1b26a-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span><span class="sxs-lookup"><span data-stu-id="1b26a-124">Access SSMS anywhere when using any of the supported Azure RemoteApp clients which includes iOS, Android, Mac, Windows Phone, and Windows PC’s.</span></span>

## <a name="create-the-azure-remoteapp-collection"></a><span data-ttu-id="1b26a-125">Create the Azure RemoteApp collection</span><span class="sxs-lookup"><span data-stu-id="1b26a-125">Create the Azure RemoteApp collection</span></span>
<span data-ttu-id="1b26a-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span><span class="sxs-lookup"><span data-stu-id="1b26a-126">Here are the steps to create your Azure RemoteApp collection with SSMS:</span></span>

### <a name="1-create-a-new-windows-vm-from-image"></a><span data-ttu-id="1b26a-127">1. Create a new Windows VM from Image</span><span class="sxs-lookup"><span data-stu-id="1b26a-127">1. Create a new Windows VM from Image</span></span>
<span data-ttu-id="1b26a-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span><span class="sxs-lookup"><span data-stu-id="1b26a-128">Use the "Windows Server Remote Desktop Session Host Windows Server 2012 R2" Image from the Gallery to make your new VM.</span></span>

### <a name="2-install-ssms-from-sql-express"></a><span data-ttu-id="1b26a-129">2. Install SSMS from SQL Express</span><span class="sxs-lookup"><span data-stu-id="1b26a-129">2. Install SSMS from SQL Express</span></span>
<span data-ttu-id="1b26a-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span><span class="sxs-lookup"><span data-stu-id="1b26a-130">Go onto the new VM and navigate to this download page: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)</span></span>

<span data-ttu-id="1b26a-131">There is an option to only download SSMS.</span><span class="sxs-lookup"><span data-stu-id="1b26a-131">There is an option to only download SSMS.</span></span> <span data-ttu-id="1b26a-132">After download, go into the install directory and run Setup to install SSMS.</span><span class="sxs-lookup"><span data-stu-id="1b26a-132">After download, go into the install directory and run Setup to install SSMS.</span></span>

<span data-ttu-id="1b26a-133">You also need to install SQL Server 2014 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="1b26a-133">You also need to install SQL Server 2014 Service Pack 1.</span></span> <span data-ttu-id="1b26a-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span><span class="sxs-lookup"><span data-stu-id="1b26a-134">You can download it here: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)</span></span>

<span data-ttu-id="1b26a-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1b26a-135">SQL Server 2014 Service Pack 1 includes essential functionality for working with Azure SQL Database.</span></span>

### <a name="3-run-validate-script-and-sysprep"></a><span data-ttu-id="1b26a-136">3. Run Validate script and Sysprep</span><span class="sxs-lookup"><span data-stu-id="1b26a-136">3. Run Validate script and Sysprep</span></span>
<span data-ttu-id="1b26a-137">On the desktop of the VM is a PowerShell script called Validate.</span><span class="sxs-lookup"><span data-stu-id="1b26a-137">On the desktop of the VM is a PowerShell script called Validate.</span></span> <span data-ttu-id="1b26a-138">Run this by double-clicking.</span><span class="sxs-lookup"><span data-stu-id="1b26a-138">Run this by double-clicking.</span></span> <span data-ttu-id="1b26a-139">It will verify that the VM is ready to be used for remote hosting of applications.</span><span class="sxs-lookup"><span data-stu-id="1b26a-139">It will verify that the VM is ready to be used for remote hosting of applications.</span></span> <span data-ttu-id="1b26a-140">When verification is complete, it will ask to run sysprep - choose to run it.</span><span class="sxs-lookup"><span data-stu-id="1b26a-140">When verification is complete, it will ask to run sysprep - choose to run it.</span></span>

<span data-ttu-id="1b26a-141">When sysprep completes, it will shut down the VM.</span><span class="sxs-lookup"><span data-stu-id="1b26a-141">When sysprep completes, it will shut down the VM.</span></span>

<span data-ttu-id="1b26a-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="1b26a-142">To learn more about creating a Azure RemoteApp image, see: [How to create a RemoteApp template image in Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)</span></span>

### <a name="4-capture-image"></a><span data-ttu-id="1b26a-143">4. Capture image</span><span class="sxs-lookup"><span data-stu-id="1b26a-143">4. Capture image</span></span>
<span data-ttu-id="1b26a-144">When the VM has stopped running, find it in the current portal and capture it.</span><span class="sxs-lookup"><span data-stu-id="1b26a-144">When the VM has stopped running, find it in the current portal and capture it.</span></span>

<span data-ttu-id="1b26a-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1b26a-145">To learn more about capturing an image, see [Capture an image of an Azure Windows virtual machine created with the classic deployment model](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

### <a name="5-add-to-azure-remoteapp-template-images"></a><span data-ttu-id="1b26a-146">5. Add to Azure RemoteApp Template images</span><span class="sxs-lookup"><span data-stu-id="1b26a-146">5. Add to Azure RemoteApp Template images</span></span>
<span data-ttu-id="1b26a-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span><span class="sxs-lookup"><span data-stu-id="1b26a-147">In the Azure RemoteApp section of the current portal, go to the Template Images tab and click Add.</span></span> <span data-ttu-id="1b26a-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span><span class="sxs-lookup"><span data-stu-id="1b26a-148">In the pop-up box, select "Import an image from your Virtual Machines library" and then choose the Image that you just created.</span></span>

### <a name="6-create-cloud-collection"></a><span data-ttu-id="1b26a-149">6. Create cloud collection</span><span class="sxs-lookup"><span data-stu-id="1b26a-149">6. Create cloud collection</span></span>
<span data-ttu-id="1b26a-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span><span class="sxs-lookup"><span data-stu-id="1b26a-150">In the current portal, create a new Azure RemoteApp Cloud Collection.</span></span> <span data-ttu-id="1b26a-151">Choose the Template Image that you just imported with SSMS installed on it.</span><span class="sxs-lookup"><span data-stu-id="1b26a-151">Choose the Template Image that you just imported with SSMS installed on it.</span></span>

![Create new cloud collection][2]

### <a name="7-publish-ssms"></a><span data-ttu-id="1b26a-153">7. Publish SSMS</span><span class="sxs-lookup"><span data-stu-id="1b26a-153">7. Publish SSMS</span></span>
<span data-ttu-id="1b26a-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span><span class="sxs-lookup"><span data-stu-id="1b26a-154">On the Publishing tab of your new cloud collection, select Publish an application from the Start Menu and then choose SSMS from the list.</span></span>

![Publish App][5]

### <a name="8-add-users"></a><span data-ttu-id="1b26a-156">8. Add users</span><span class="sxs-lookup"><span data-stu-id="1b26a-156">8. Add users</span></span>
<span data-ttu-id="1b26a-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span><span class="sxs-lookup"><span data-stu-id="1b26a-157">On the User Access tab you can select the users that will have access to this Azure RemoteApp collection which only includes SSMS.</span></span>

![Add User][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a><span data-ttu-id="1b26a-159">9. Install the Azure RemoteApp client application</span><span class="sxs-lookup"><span data-stu-id="1b26a-159">9. Install the Azure RemoteApp client application</span></span>
<span data-ttu-id="1b26a-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span><span class="sxs-lookup"><span data-stu-id="1b26a-160">You can download and install a Azure RemoteApp client here: [Download | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)</span></span>

## <a name="configure-azure-sql-server"></a><span data-ttu-id="1b26a-161">Configure Azure SQL server</span><span class="sxs-lookup"><span data-stu-id="1b26a-161">Configure Azure SQL server</span></span>
<span data-ttu-id="1b26a-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span><span class="sxs-lookup"><span data-stu-id="1b26a-162">The only configuration needed is to ensure that Azure Services is enabled for the firewall.</span></span> <span data-ttu-id="1b26a-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span><span class="sxs-lookup"><span data-stu-id="1b26a-163">If you use this solution, then you do not need to add any IP addresses to open the firewall.</span></span> <span data-ttu-id="1b26a-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span><span class="sxs-lookup"><span data-stu-id="1b26a-164">The network traffic that is allowed to the SQL Server is from other Azure services.</span></span>

![Azure Allow][4]

## <a name="multi-factor-authentication-mfa"></a><span data-ttu-id="1b26a-166">Multi-Factor Authentication (MFA)</span><span class="sxs-lookup"><span data-stu-id="1b26a-166">Multi-Factor Authentication (MFA)</span></span>
<span data-ttu-id="1b26a-167">MFA can be enabled for this application specifically.</span><span class="sxs-lookup"><span data-stu-id="1b26a-167">MFA can be enabled for this application specifically.</span></span> <span data-ttu-id="1b26a-168">Go to the Applications tab of your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b26a-168">Go to the Applications tab of your Azure Active Directory.</span></span> <span data-ttu-id="1b26a-169">You will find an entry for Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1b26a-169">You will find an entry for Microsoft Azure RemoteApp.</span></span> <span data-ttu-id="1b26a-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span><span class="sxs-lookup"><span data-stu-id="1b26a-170">If you click that application and then configure, you will see the page below where you can enable MFA for this application.</span></span>

![Enable MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a><span data-ttu-id="1b26a-172">Audit user activity with Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="1b26a-172">Audit user activity with Azure Active Directory Premium</span></span>
<span data-ttu-id="1b26a-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span><span class="sxs-lookup"><span data-stu-id="1b26a-173">If you do not have Azure AD Premium, then you have to turn it on in the Licenses section of your directory.</span></span> <span data-ttu-id="1b26a-174">With Premium enabled, you can assign users to the Premium level.</span><span class="sxs-lookup"><span data-stu-id="1b26a-174">With Premium enabled, you can assign users to the Premium level.</span></span>

<span data-ttu-id="1b26a-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1b26a-175">When you go to a user in your Azure Active Directory, you can then go to the Activity tab to see login information to Azure RemoteApp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b26a-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b26a-176">Next steps</span></span>
<span data-ttu-id="1b26a-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span><span class="sxs-lookup"><span data-stu-id="1b26a-177">After completing all the above steps, you will be able to run the Azure RemoteApp client and log-in with an assigned user.</span></span> <span data-ttu-id="1b26a-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="1b26a-178">You will be presented with SSMS as one of your applications, and you can run it as you would if it were installed on your computer with access to Azure SQL server.</span></span>

<span data-ttu-id="1b26a-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="1b26a-179">For more information on how to make the connection to SQL Database, see [Connect to SQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>

<span data-ttu-id="1b26a-180">That's everything for now.</span><span class="sxs-lookup"><span data-stu-id="1b26a-180">That's everything for now.</span></span> <span data-ttu-id="1b26a-181">Enjoy!</span><span class="sxs-lookup"><span data-stu-id="1b26a-181">Enjoy!</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/ssms.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/mfa.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/allowazure.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/publish.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-ssms-remoteapp/user.png





