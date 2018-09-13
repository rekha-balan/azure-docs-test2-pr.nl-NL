---
title: LOB application test environment | Microsoft Docs
description: Learn how to create a web-based, line of business application in a hybrid cloud environment for IT pro or development testing.
services: virtual-machines-windows
documentationcenter: ''
author: JoeDavies-MSFT
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 678714ce07d4efd369f125bc12c9965d856bd68c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671221"
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="eb13c-103">Set up a web-based LOB application in a hybrid cloud for testing</span><span class="sxs-lookup"><span data-stu-id="eb13c-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="eb13c-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eb13c-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="eb13c-105">Here is the resulting configuration.</span><span class="sxs-lookup"><span data-stu-id="eb13c-105">Here is the resulting configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="eb13c-106">This configuration consists of:</span><span class="sxs-lookup"><span data-stu-id="eb13c-106">This configuration consists of:</span></span>

* <span data-ttu-id="eb13c-107">A simulated on-premises network hosted in Azure (the TestLab VNet).</span><span class="sxs-lookup"><span data-stu-id="eb13c-107">A simulated on-premises network hosted in Azure (the TestLab VNet).</span></span>
* <span data-ttu-id="eb13c-108">A cross-premises virtual network hosted in Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="eb13c-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="eb13c-109">A VNet-to-VNet VPN connection.</span><span class="sxs-lookup"><span data-stu-id="eb13c-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="eb13c-110">A web-based LOB server, SQL server, and secondary domain controller in the TestVNET virtual network.</span><span class="sxs-lookup"><span data-stu-id="eb13c-110">A web-based LOB server, SQL server, and secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="eb13c-111">This configuration provides a basis and common starting point from which you can:</span><span class="sxs-lookup"><span data-stu-id="eb13c-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="eb13c-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span><span class="sxs-lookup"><span data-stu-id="eb13c-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="eb13c-113">Perform testing of this simulated hybrid cloud-based IT workload.</span><span class="sxs-lookup"><span data-stu-id="eb13c-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="eb13c-114">There are three major phases to setting up this hybrid cloud test environment:</span><span class="sxs-lookup"><span data-stu-id="eb13c-114">There are three major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="eb13c-115">Set up the simulated hybrid cloud environment.</span><span class="sxs-lookup"><span data-stu-id="eb13c-115">Set up the simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="eb13c-116">Configure the SQL server computer (SQL1).</span><span class="sxs-lookup"><span data-stu-id="eb13c-116">Configure the SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="eb13c-117">Configure the LOB server (LOB1).</span><span class="sxs-lookup"><span data-stu-id="eb13c-117">Configure the LOB server (LOB1).</span></span>

<span data-ttu-id="eb13c-118">This workload requires an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="eb13c-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="eb13c-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="eb13c-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="eb13c-120">For an example of a production LOB application hosted in Azure, see the **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="eb13c-120">For an example of a production LOB application hosted in Azure, see the **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-the-simulated-hybrid-cloud-environment"></a><span data-ttu-id="eb13c-121">Phase 1: Set up the simulated hybrid cloud environment</span><span class="sxs-lookup"><span data-stu-id="eb13c-121">Phase 1: Set up the simulated hybrid cloud environment</span></span>
<span data-ttu-id="eb13c-122">Create the [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb13c-122">Create the [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="eb13c-123">Because this test environment does not require the presence of the APP1 server on the Corpnet subnet, you can shut it down for now.</span><span class="sxs-lookup"><span data-stu-id="eb13c-123">Because this test environment does not require the presence of the APP1 server on the Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="eb13c-124">This is your current configuration.</span><span class="sxs-lookup"><span data-stu-id="eb13c-124">This is your current configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-the-sql-server-computer-sql1"></a><span data-ttu-id="eb13c-125">Phase 2: Configure the SQL server computer (SQL1)</span><span class="sxs-lookup"><span data-stu-id="eb13c-125">Phase 2: Configure the SQL server computer (SQL1)</span></span>
<span data-ttu-id="eb13c-126">From the Azure portal, start the DC2 computer if needed.</span><span class="sxs-lookup"><span data-stu-id="eb13c-126">From the Azure portal, start the DC2 computer if needed.</span></span>

<span data-ttu-id="eb13c-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span><span class="sxs-lookup"><span data-stu-id="eb13c-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="eb13c-128">Prior to running these commands, fill in the variable values and remove the < and > characters.</span><span class="sxs-lookup"><span data-stu-id="eb13c-128">Prior to running these commands, fill in the variable values and remove the < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<the Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type the name and password of the local administrator account for the SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="eb13c-129">Use the Azure portal to connect to SQL1 using the local administrator account of SQL1.</span><span class="sxs-lookup"><span data-stu-id="eb13c-129">Use the Azure portal to connect to SQL1 using the local administrator account of SQL1.</span></span>

<span data-ttu-id="eb13c-130">Next, configure Windows Firewall rules to allow basic connectivity testing and SQL Server traffic.</span><span class="sxs-lookup"><span data-stu-id="eb13c-130">Next, configure Windows Firewall rules to allow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="eb13c-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span><span class="sxs-lookup"><span data-stu-id="eb13c-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="eb13c-132">The ping command should result in four successful replies from IP address 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="eb13c-132">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="eb13c-133">Next, add the extra data disk on SQL1 as a new volume with the drive letter F:.</span><span class="sxs-lookup"><span data-stu-id="eb13c-133">Next, add the extra data disk on SQL1 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="eb13c-134">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-134">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="eb13c-135">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span><span class="sxs-lookup"><span data-stu-id="eb13c-135">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="eb13c-136">Click **Tasks**, and then click **New Volume**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="eb13c-137">On the Before you begin page of the New Volume Wizard, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-137">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="eb13c-138">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-138">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="eb13c-139">When prompted, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="eb13c-140">On the Specify the size of the volume page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-140">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="eb13c-141">On the Assign to a drive letter or folder page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-141">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="eb13c-142">On the Select file system settings page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-142">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="eb13c-143">On the Confirm selections page, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-143">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="eb13c-144">When complete, click **Close**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-144">When complete, click **Close**.</span></span>

<span data-ttu-id="eb13c-145">Run these commands at the Windows PowerShell command prompt on SQL1:</span><span class="sxs-lookup"><span data-stu-id="eb13c-145">Run these commands at the Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="eb13c-146">Next, join SQL1 to the CORP Windows Server Active Directory domain with these commands at the Windows PowerShell prompt on SQL1.</span><span class="sxs-lookup"><span data-stu-id="eb13c-146">Next, join SQL1 to the CORP Windows Server Active Directory domain with these commands at the Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="eb13c-147">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span><span class="sxs-lookup"><span data-stu-id="eb13c-147">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="eb13c-148">After restarting, use the Azure portal to connect to SQL1 *with the local administrator account of SQL1*.</span><span class="sxs-lookup"><span data-stu-id="eb13c-148">After restarting, use the Azure portal to connect to SQL1 *with the local administrator account of SQL1*.</span></span>

<span data-ttu-id="eb13c-149">Next, configure SQL Server 2014 to use the F: drive for new databases and for user account permissions.</span><span class="sxs-lookup"><span data-stu-id="eb13c-149">Next, configure SQL Server 2014 to use the F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="eb13c-150">From the Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-150">From the Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="eb13c-151">In **Connect to Server**, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-151">In **Connect to Server**, click **Connect**.</span></span>
3. <span data-ttu-id="eb13c-152">In the Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-152">In the Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="eb13c-153">In the **Server Properties** window, click **Database Settings**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-153">In the **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="eb13c-154">Locate the **Database default locations** and set these values:</span><span class="sxs-lookup"><span data-stu-id="eb13c-154">Locate the **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="eb13c-155">For **Data**, type the path **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-155">For **Data**, type the path **f:\Data**.</span></span>
   * <span data-ttu-id="eb13c-156">For **Log**, type the path **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-156">For **Log**, type the path **f:\Log**.</span></span>
   * <span data-ttu-id="eb13c-157">For **Backup**, type the path **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-157">For **Backup**, type the path **f:\Backup**.</span></span>
   * <span data-ttu-id="eb13c-158">Note: Only new databases use these locations.</span><span class="sxs-lookup"><span data-stu-id="eb13c-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="eb13c-159">Click the **OK** to close the window.</span><span class="sxs-lookup"><span data-stu-id="eb13c-159">Click the **OK** to close the window.</span></span>
7. <span data-ttu-id="eb13c-160">In the **Object Explorer** tree pane, open **Security**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-160">In the **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="eb13c-161">Right-click **Logins** and then click **New Login**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="eb13c-162">In **Login name**, type **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="eb13c-163">On the **Server Roles** page, click **sysadmin**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-163">On the **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="eb13c-164">Close Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="eb13c-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="eb13c-165">This is your current configuration.</span><span class="sxs-lookup"><span data-stu-id="eb13c-165">This is your current configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-the-lob-server-lob1"></a><span data-ttu-id="eb13c-166">Phase 3: Configure the LOB server (LOB1)</span><span class="sxs-lookup"><span data-stu-id="eb13c-166">Phase 3: Configure the LOB server (LOB1)</span></span>
<span data-ttu-id="eb13c-167">First, create a virtual machine for LOB1 with these commands at the Azure PowerShell command prompt on your local computer.</span><span class="sxs-lookup"><span data-stu-id="eb13c-167">First, create a virtual machine for LOB1 with these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="eb13c-168">Next, use the Azure portal to connect to LOB1 with the credentials of the local administrator account of LOB1.</span><span class="sxs-lookup"><span data-stu-id="eb13c-168">Next, use the Azure portal to connect to LOB1 with the credentials of the local administrator account of LOB1.</span></span>

<span data-ttu-id="eb13c-169">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span><span class="sxs-lookup"><span data-stu-id="eb13c-169">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="eb13c-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span><span class="sxs-lookup"><span data-stu-id="eb13c-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="eb13c-171">The ping command should result in four successful replies from IP address 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="eb13c-171">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="eb13c-172">Next, join LOB1 to the CORP Active Directory domain with these commands at the Windows PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="eb13c-172">Next, join LOB1 to the CORP Active Directory domain with these commands at the Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="eb13c-173">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span><span class="sxs-lookup"><span data-stu-id="eb13c-173">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="eb13c-174">After restarting, use the Azure portal to connect to LOB1 with the CORP\User1 account and password.</span><span class="sxs-lookup"><span data-stu-id="eb13c-174">After restarting, use the Azure portal to connect to LOB1 with the CORP\User1 account and password.</span></span>

<span data-ttu-id="eb13c-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="eb13c-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="eb13c-176">From Server Manager, click **Add roles and features**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="eb13c-177">On the **Before you begin** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-177">On the **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="eb13c-178">On the **Select installation type** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-178">On the **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="eb13c-179">On the **Select destination server** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-179">On the **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="eb13c-180">On the **Server roles** page, click **Web Server (IIS)** in the list of **Roles**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-180">On the **Server roles** page, click **Web Server (IIS)** in the list of **Roles**.</span></span>
6. <span data-ttu-id="eb13c-181">When prompted, click **Add Features**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="eb13c-182">On the **Select features** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-182">On the **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="eb13c-183">On the **Web Server (IIS)** page, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-183">On the **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="eb13c-184">On the **Select role services** page, select or clear the check boxes for the services you need for testing your LOB application, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-184">On the **Select role services** page, select or clear the check boxes for the services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="eb13c-185">On the **Confirm installation selections** page, click **Install**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-185">On the **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="eb13c-186">Wait until the installation of components has completed and then click **Close**.</span><span class="sxs-lookup"><span data-stu-id="eb13c-186">Wait until the installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="eb13c-187">From the Azure portal, connect to the CLIENT1 computer with the CORP\User1 account credentials, and then start Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="eb13c-187">From the Azure portal, connect to the CLIENT1 computer with the CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="eb13c-188">In the Address bar, type **http://lob1/** and then press ENTER.</span><span class="sxs-lookup"><span data-stu-id="eb13c-188">In the Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="eb13c-189">You should see the default IIS 8 web page.</span><span class="sxs-lookup"><span data-stu-id="eb13c-189">You should see the default IIS 8 web page.</span></span>

<span data-ttu-id="eb13c-190">This is your current configuration.</span><span class="sxs-lookup"><span data-stu-id="eb13c-190">This is your current configuration.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="eb13c-191">This environment is now ready for you to deploy your web-based application on LOB1 and test functionality from CLIENT1 on the Corpnet subnet.</span><span class="sxs-lookup"><span data-stu-id="eb13c-191">This environment is now ready for you to deploy your web-based application on LOB1 and test functionality from CLIENT1 on the Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="eb13c-192">Next step</span><span class="sxs-lookup"><span data-stu-id="eb13c-192">Next step</span></span>
* <span data-ttu-id="eb13c-193">Add a new virtual machine using the [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb13c-193">Add a new virtual machine using the [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>





