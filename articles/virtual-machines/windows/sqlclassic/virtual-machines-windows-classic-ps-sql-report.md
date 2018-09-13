---
title: Use PowerShell to Create a VM With a Native Mode Report Server | Microsoft Docs
description: 'This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine. '
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 6d7fac6939e8936de890c82cbf1d374620874db7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554729"
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="9649e-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span><span class="sxs-lookup"><span data-stu-id="9649e-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="9649e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9649e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9649e-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="9649e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9649e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="9649e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="9649e-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="9649e-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="9649e-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="9649e-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span><span class="sxs-lookup"><span data-stu-id="9649e-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="9649e-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span><span class="sxs-lookup"><span data-stu-id="9649e-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="9649e-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span><span class="sxs-lookup"><span data-stu-id="9649e-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="9649e-112">After you run the script, the report server is ready to use.</span><span class="sxs-lookup"><span data-stu-id="9649e-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="9649e-113">Prerequisites and Assumptions</span><span class="sxs-lookup"><span data-stu-id="9649e-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="9649e-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span><span class="sxs-lookup"><span data-stu-id="9649e-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="9649e-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span><span class="sxs-lookup"><span data-stu-id="9649e-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="9649e-116">If you use a VM size of **A2**, you need **2** available cores.</span><span class="sxs-lookup"><span data-stu-id="9649e-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="9649e-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9649e-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="9649e-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="9649e-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="9649e-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9649e-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="9649e-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9649e-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="9649e-121">For more information about using Windows PowerShell, see the following:</span><span class="sxs-lookup"><span data-stu-id="9649e-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="9649e-122">Starting Windows PowerShell on Windows Server</span><span class="sxs-lookup"><span data-stu-id="9649e-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="9649e-123">Getting Started with Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9649e-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="9649e-124">Step 1: Provision an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="9649e-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="9649e-125">Browse to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9649e-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="9649e-126">Click **Virtual Machines** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="9649e-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![microsoft azure virtual machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="9649e-128">Click **New**.</span><span class="sxs-lookup"><span data-stu-id="9649e-128">Click **New**.</span></span>
   
    ![new button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="9649e-130">Click **From Gallery**.</span><span class="sxs-lookup"><span data-stu-id="9649e-130">Click **From Gallery**.</span></span>
   
    ![new vm from gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="9649e-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span><span class="sxs-lookup"><span data-stu-id="9649e-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![next](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="9649e-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="9649e-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="9649e-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="9649e-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="9649e-136">On the **Virtual machine configuration** page, edit the following fields:</span><span class="sxs-lookup"><span data-stu-id="9649e-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="9649e-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span><span class="sxs-lookup"><span data-stu-id="9649e-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="9649e-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span><span class="sxs-lookup"><span data-stu-id="9649e-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="9649e-139">The DNS name must be unique across the Azure service.</span><span class="sxs-lookup"><span data-stu-id="9649e-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="9649e-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span><span class="sxs-lookup"><span data-stu-id="9649e-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="9649e-141">For example ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="9649e-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="9649e-142">**Tier**: Standard</span><span class="sxs-lookup"><span data-stu-id="9649e-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="9649e-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span><span class="sxs-lookup"><span data-stu-id="9649e-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="9649e-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span><span class="sxs-lookup"><span data-stu-id="9649e-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="9649e-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="9649e-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="9649e-146">**New User Name**: the name you provide is created as an administrator on the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="9649e-147">**New Password** and **confirm**.</span><span class="sxs-lookup"><span data-stu-id="9649e-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="9649e-148">This password is used for the new administrator account and it is recommended you use a strong password.</span><span class="sxs-lookup"><span data-stu-id="9649e-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="9649e-149">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9649e-149">Click **Next**.</span></span> <span data-ttu-id="9649e-150">![next](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="9649e-150">![next](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="9649e-151">On the next page, edit the following fields:</span><span class="sxs-lookup"><span data-stu-id="9649e-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="9649e-152">**Cloud Service**: select **Create a new Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="9649e-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="9649e-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="9649e-154">The default name is the name you typed in for the VM name.</span><span class="sxs-lookup"><span data-stu-id="9649e-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="9649e-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span><span class="sxs-lookup"><span data-stu-id="9649e-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="9649e-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span><span class="sxs-lookup"><span data-stu-id="9649e-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="9649e-157">**Storage Account**: Use an automatically generated storage account.</span><span class="sxs-lookup"><span data-stu-id="9649e-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="9649e-158">**Availability Set**: None.</span><span class="sxs-lookup"><span data-stu-id="9649e-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="9649e-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span><span class="sxs-lookup"><span data-stu-id="9649e-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="9649e-160">**HTTP**: The default public and private ports are **80**.</span><span class="sxs-lookup"><span data-stu-id="9649e-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="9649e-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span><span class="sxs-lookup"><span data-stu-id="9649e-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="9649e-162">**HTTPS**: The default public and private ports are **443**.</span><span class="sxs-lookup"><span data-stu-id="9649e-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="9649e-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span><span class="sxs-lookup"><span data-stu-id="9649e-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="9649e-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9649e-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="9649e-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span><span class="sxs-lookup"><span data-stu-id="9649e-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="9649e-166">Click next .</span><span class="sxs-lookup"><span data-stu-id="9649e-166">Click next .</span></span> ![next](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="9649e-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span><span class="sxs-lookup"><span data-stu-id="9649e-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="9649e-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span><span class="sxs-lookup"><span data-stu-id="9649e-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="9649e-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="9649e-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="9649e-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span><span class="sxs-lookup"><span data-stu-id="9649e-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="9649e-172">Click complete .</span><span class="sxs-lookup"><span data-stu-id="9649e-172">Click complete .</span></span> ![ok](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="9649e-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span><span class="sxs-lookup"><span data-stu-id="9649e-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="9649e-175">Step 2: Create a Server Certificate</span><span class="sxs-lookup"><span data-stu-id="9649e-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="9649e-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span><span class="sxs-lookup"><span data-stu-id="9649e-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="9649e-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span><span class="sxs-lookup"><span data-stu-id="9649e-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="9649e-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="9649e-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="9649e-179">Depending on your scenario, you can use one of the following two methods:</span><span class="sxs-lookup"><span data-stu-id="9649e-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="9649e-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9649e-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="9649e-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span><span class="sxs-lookup"><span data-stu-id="9649e-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="9649e-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="9649e-183">A self-signed certificate.</span><span class="sxs-lookup"><span data-stu-id="9649e-183">A self-signed certificate.</span></span> <span data-ttu-id="9649e-184">Self-signed certificates are not recommended for production environments.</span><span class="sxs-lookup"><span data-stu-id="9649e-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="9649e-185">To use a certificate created by a trusted Certificate Authority (CA)</span><span class="sxs-lookup"><span data-stu-id="9649e-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="9649e-186">**Request a server certificate for the website from a certification authority**.</span><span class="sxs-lookup"><span data-stu-id="9649e-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="9649e-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span><span class="sxs-lookup"><span data-stu-id="9649e-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="9649e-188">For example, Microsoft Certificate Services in Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="9649e-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="9649e-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span><span class="sxs-lookup"><span data-stu-id="9649e-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="9649e-190">For more information about requesting a server certificates, see the following:</span><span class="sxs-lookup"><span data-stu-id="9649e-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="9649e-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="9649e-192">Security Tools to Administer Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="9649e-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="9649e-193">Security Tools to Administer Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="9649e-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="9649e-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="9649e-195">**Install the server certificate on the Web server**.</span><span class="sxs-lookup"><span data-stu-id="9649e-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="9649e-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="9649e-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="9649e-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="9649e-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="9649e-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span><span class="sxs-lookup"><span data-stu-id="9649e-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="9649e-199">See the next section for details on how to obtain the thumbprint of the certificate.</span><span class="sxs-lookup"><span data-stu-id="9649e-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="9649e-200">Assign the server certificate to the report server.</span><span class="sxs-lookup"><span data-stu-id="9649e-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="9649e-201">The assignment is completed in the next section when you configure the report server.</span><span class="sxs-lookup"><span data-stu-id="9649e-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="9649e-202">To use the Virtual Machines Self-signed Certificate</span><span class="sxs-lookup"><span data-stu-id="9649e-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="9649e-203">A self-signed certificate was created on the VM when the VM was provisioned.</span><span class="sxs-lookup"><span data-stu-id="9649e-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="9649e-204">The certificate has the same name as the VM DNS name.</span><span class="sxs-lookup"><span data-stu-id="9649e-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="9649e-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span><span class="sxs-lookup"><span data-stu-id="9649e-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="9649e-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span><span class="sxs-lookup"><span data-stu-id="9649e-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="9649e-207">The following is a summary of the steps required.</span><span class="sxs-lookup"><span data-stu-id="9649e-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="9649e-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="9649e-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="9649e-209">From the Azure classic portal, select the VM and click connect.</span><span class="sxs-lookup"><span data-stu-id="9649e-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="9649e-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![connect to azure virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="9649e-212">Use the user VM name, user name and password you configured when you created the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="9649e-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span><span class="sxs-lookup"><span data-stu-id="9649e-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![login inlcudes vm name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="9649e-215">Run mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="9649e-215">Run mmc.exe.</span></span> <span data-ttu-id="9649e-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="9649e-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9649e-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="9649e-218">Select **Local Computer** to manage and then click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="9649e-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="9649e-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="9649e-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="9649e-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="9649e-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="9649e-221">Right-click the certificate name and click **Copy**.</span><span class="sxs-lookup"><span data-stu-id="9649e-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="9649e-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span><span class="sxs-lookup"><span data-stu-id="9649e-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="9649e-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span><span class="sxs-lookup"><span data-stu-id="9649e-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="9649e-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span><span class="sxs-lookup"><span data-stu-id="9649e-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="9649e-225">**To get the thumbprint value**, complete the following.</span><span class="sxs-lookup"><span data-stu-id="9649e-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="9649e-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="9649e-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="9649e-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="9649e-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="9649e-228">Click the **Details** tab.</span><span class="sxs-lookup"><span data-stu-id="9649e-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="9649e-229">Click **Thumbprint**.</span><span class="sxs-lookup"><span data-stu-id="9649e-229">Click **Thumbprint**.</span></span> <span data-ttu-id="9649e-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="9649e-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="9649e-231">Copy the thumbprint and save the value for later or edit the script now.</span><span class="sxs-lookup"><span data-stu-id="9649e-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="9649e-232">(\*) Before you run the script, remove the spaces in between the pairs of values.</span><span class="sxs-lookup"><span data-stu-id="9649e-232">(\*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="9649e-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="9649e-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="9649e-234">Assign the server certificate to the report server.</span><span class="sxs-lookup"><span data-stu-id="9649e-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="9649e-235">The assignment is completed in the next section when you configure the report server.</span><span class="sxs-lookup"><span data-stu-id="9649e-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="9649e-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="9649e-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span><span class="sxs-lookup"><span data-stu-id="9649e-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="9649e-238">Step 3: Configure the Report Server</span><span class="sxs-lookup"><span data-stu-id="9649e-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="9649e-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span><span class="sxs-lookup"><span data-stu-id="9649e-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="9649e-240">You can use one of the following methods to configure the report server:</span><span class="sxs-lookup"><span data-stu-id="9649e-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="9649e-241">Use the script to configure the report server</span><span class="sxs-lookup"><span data-stu-id="9649e-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="9649e-242">Use Configuration Manager to Configure the Report Server.</span><span class="sxs-lookup"><span data-stu-id="9649e-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="9649e-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="9649e-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="9649e-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span><span class="sxs-lookup"><span data-stu-id="9649e-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="9649e-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span><span class="sxs-lookup"><span data-stu-id="9649e-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="9649e-246">Use script to configure the report server and HTTP</span><span class="sxs-lookup"><span data-stu-id="9649e-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="9649e-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="9649e-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="9649e-248">The configuration includes HTTP, not HTTPS:</span><span class="sxs-lookup"><span data-stu-id="9649e-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="9649e-249">From the Azure classic portal, select the VM and click connect.</span><span class="sxs-lookup"><span data-stu-id="9649e-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="9649e-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![connect to azure virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="9649e-252">Use the user VM name, user name and password you configured when you created the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="9649e-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span><span class="sxs-lookup"><span data-stu-id="9649e-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![login inlcudes vm name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="9649e-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="9649e-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="9649e-256">The PowerShell ISE is installed by default on Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="9649e-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="9649e-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span><span class="sxs-lookup"><span data-stu-id="9649e-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="9649e-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span><span class="sxs-lookup"><span data-stu-id="9649e-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="9649e-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span><span class="sxs-lookup"><span data-stu-id="9649e-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="9649e-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="9649e-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="9649e-261">The script is currently configured for  Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="9649e-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="9649e-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span><span class="sxs-lookup"><span data-stu-id="9649e-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="9649e-263">Run the script.</span><span class="sxs-lookup"><span data-stu-id="9649e-263">Run the script.</span></span>

<span data-ttu-id="9649e-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span><span class="sxs-lookup"><span data-stu-id="9649e-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="9649e-265">Use script to configure the report server and HTTPS</span><span class="sxs-lookup"><span data-stu-id="9649e-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="9649e-266">To use Windows PowerShell to configure the report server, complete the following steps.</span><span class="sxs-lookup"><span data-stu-id="9649e-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="9649e-267">The configuration includes HTTPS, not HTTP.</span><span class="sxs-lookup"><span data-stu-id="9649e-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="9649e-268">From the Azure classic portal, select the VM and click connect.</span><span class="sxs-lookup"><span data-stu-id="9649e-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="9649e-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![connect to azure virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="9649e-271">Use the user VM name, user name and password you configured when you created the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="9649e-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span><span class="sxs-lookup"><span data-stu-id="9649e-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![login inlcudes vm name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="9649e-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="9649e-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="9649e-275">The PowerShell ISE is installed by default on Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="9649e-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="9649e-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span><span class="sxs-lookup"><span data-stu-id="9649e-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="9649e-277">To enable running scripts, run the following Windows PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="9649e-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="9649e-278">You can then run the following to verify the policy:</span><span class="sxs-lookup"><span data-stu-id="9649e-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="9649e-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span><span class="sxs-lookup"><span data-stu-id="9649e-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="9649e-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span><span class="sxs-lookup"><span data-stu-id="9649e-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="9649e-281">Modify the **$certificatehash** parameter in the script:</span><span class="sxs-lookup"><span data-stu-id="9649e-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="9649e-282">This is a **required** parameter.</span><span class="sxs-lookup"><span data-stu-id="9649e-282">This is a **required** parameter.</span></span> <span data-ttu-id="9649e-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span><span class="sxs-lookup"><span data-stu-id="9649e-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="9649e-284">On the VM, open Windows PowerShell ISE and run the following command:</span><span class="sxs-lookup"><span data-stu-id="9649e-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="9649e-285">The output will look similar to the following.</span><span class="sxs-lookup"><span data-stu-id="9649e-285">The output will look similar to the following.</span></span> <span data-ttu-id="9649e-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="9649e-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="9649e-287">OR</span><span class="sxs-lookup"><span data-stu-id="9649e-287">OR</span></span>
   * <span data-ttu-id="9649e-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span><span class="sxs-lookup"><span data-stu-id="9649e-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="9649e-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span><span class="sxs-lookup"><span data-stu-id="9649e-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="9649e-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="9649e-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="9649e-291">Click the **Details** tab.</span><span class="sxs-lookup"><span data-stu-id="9649e-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="9649e-292">Click **Thumbprint**.</span><span class="sxs-lookup"><span data-stu-id="9649e-292">Click **Thumbprint**.</span></span> <span data-ttu-id="9649e-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="9649e-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="9649e-294">**Before you run the script**, remove the spaces in between the pairs of values.</span><span class="sxs-lookup"><span data-stu-id="9649e-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="9649e-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="9649e-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="9649e-296">Modify the **$httpsport** parameter:</span><span class="sxs-lookup"><span data-stu-id="9649e-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="9649e-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span><span class="sxs-lookup"><span data-stu-id="9649e-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="9649e-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="9649e-299">Modify the **$DNSName** parameter:</span><span class="sxs-lookup"><span data-stu-id="9649e-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="9649e-300">The script is configured for a wild card certificate $DNSName="+".</span><span class="sxs-lookup"><span data-stu-id="9649e-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="9649e-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="9649e-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="9649e-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="9649e-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="9649e-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span><span class="sxs-lookup"><span data-stu-id="9649e-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="9649e-304">The script is currently configured for  Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="9649e-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="9649e-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span><span class="sxs-lookup"><span data-stu-id="9649e-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="9649e-306">Run the script.</span><span class="sxs-lookup"><span data-stu-id="9649e-306">Run the script.</span></span>

<span data-ttu-id="9649e-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span><span class="sxs-lookup"><span data-stu-id="9649e-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="9649e-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span><span class="sxs-lookup"><span data-stu-id="9649e-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="9649e-309">The result will include the following:</span><span class="sxs-lookup"><span data-stu-id="9649e-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="9649e-310">Use Configuration Manager to Configure the Report Server</span><span class="sxs-lookup"><span data-stu-id="9649e-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="9649e-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span><span class="sxs-lookup"><span data-stu-id="9649e-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="9649e-312">From the Azure classic portal, select the VM and click connect.</span><span class="sxs-lookup"><span data-stu-id="9649e-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="9649e-313">Use the user name and password you configured when you created the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![connect to azure virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="9649e-315">Run Windows update and install updates to the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="9649e-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9649e-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="9649e-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="9649e-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="9649e-318">Leave the default values for **Server Name** and **Report Server Instance**.</span><span class="sxs-lookup"><span data-stu-id="9649e-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="9649e-319">Click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="9649e-319">Click **Connect**.</span></span>
5. <span data-ttu-id="9649e-320">In the left pane, click **Web Service URL**.</span><span class="sxs-lookup"><span data-stu-id="9649e-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="9649e-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span><span class="sxs-lookup"><span data-stu-id="9649e-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="9649e-322">To add HTTPS:</span><span class="sxs-lookup"><span data-stu-id="9649e-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="9649e-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="9649e-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="9649e-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="9649e-325">Under **SSL Port**: choose 443.</span><span class="sxs-lookup"><span data-stu-id="9649e-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="9649e-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span><span class="sxs-lookup"><span data-stu-id="9649e-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="9649e-327">Click **Apply** and wait for the operation to complete.</span><span class="sxs-lookup"><span data-stu-id="9649e-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="9649e-328">In the left pane, click **Database**.</span><span class="sxs-lookup"><span data-stu-id="9649e-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="9649e-329">Click **Change Databas**e.</span><span class="sxs-lookup"><span data-stu-id="9649e-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="9649e-330">Click **Create a new report server database** and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9649e-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="9649e-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span><span class="sxs-lookup"><span data-stu-id="9649e-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="9649e-332">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9649e-332">Click **Next**.</span></span>
   4. <span data-ttu-id="9649e-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9649e-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="9649e-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9649e-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="9649e-335">Click **Next** on the **Summary** page.</span><span class="sxs-lookup"><span data-stu-id="9649e-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="9649e-336">When the configuration is complete, click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="9649e-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="9649e-337">In the left pane, click **Report Manager URL**.</span><span class="sxs-lookup"><span data-stu-id="9649e-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="9649e-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="9649e-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="9649e-339">Click **Exit** to close the Reporting Services Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="9649e-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="9649e-340">Step 4: Open Windows Firewall Port</span><span class="sxs-lookup"><span data-stu-id="9649e-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="9649e-341">If you used one of the scripts to configure the report server, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="9649e-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="9649e-342">The script included a step to open the firewall port.</span><span class="sxs-lookup"><span data-stu-id="9649e-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="9649e-343">The default was port 80 for HTTP and port 443 for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9649e-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="9649e-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="9649e-345">It is required to open the same port in the VM’s firewall.</span><span class="sxs-lookup"><span data-stu-id="9649e-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="9649e-346">The endpoint was created when the VM was provisioned.</span><span class="sxs-lookup"><span data-stu-id="9649e-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="9649e-347">This section provides basic information on how to open the firewall port.</span><span class="sxs-lookup"><span data-stu-id="9649e-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="9649e-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="9649e-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="9649e-349">If you used the script to configure the report server, you can skip this section.</span><span class="sxs-lookup"><span data-stu-id="9649e-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="9649e-350">The script included a step to open the firewall port.</span><span class="sxs-lookup"><span data-stu-id="9649e-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="9649e-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span><span class="sxs-lookup"><span data-stu-id="9649e-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="9649e-352">To open port **443** on the Windows Firewall, complete the following:</span><span class="sxs-lookup"><span data-stu-id="9649e-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="9649e-353">Open a Windows PowerShell window with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="9649e-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="9649e-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span><span class="sxs-lookup"><span data-stu-id="9649e-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="9649e-355">When the command completes, **Ok** is displayed in the command prompt.</span><span class="sxs-lookup"><span data-stu-id="9649e-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="9649e-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span><span class="sxs-lookup"><span data-stu-id="9649e-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="9649e-357">Verify the configuration</span><span class="sxs-lookup"><span data-stu-id="9649e-357">Verify the configuration</span></span>
<span data-ttu-id="9649e-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span><span class="sxs-lookup"><span data-stu-id="9649e-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="9649e-359">On the VM, browse to the report server URL:</span><span class="sxs-lookup"><span data-stu-id="9649e-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="9649e-360">On the VM, browse to the report manger URL:</span><span class="sxs-lookup"><span data-stu-id="9649e-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="9649e-361">From your local computer, browse to the **remote** report Manager on the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="9649e-362">Update the DNS name in the following example as appropriate.</span><span class="sxs-lookup"><span data-stu-id="9649e-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="9649e-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span><span class="sxs-lookup"><span data-stu-id="9649e-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="9649e-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="9649e-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="9649e-365">If you are not using HTTP**S**, remove the **s** in the URL.</span><span class="sxs-lookup"><span data-stu-id="9649e-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="9649e-366">See the next section for information on creating additional users on VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="9649e-367">From your local computer, browse to the remote report server URL.</span><span class="sxs-lookup"><span data-stu-id="9649e-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="9649e-368">Update the DNS name in the following example as appropriate.</span><span class="sxs-lookup"><span data-stu-id="9649e-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="9649e-369">If you are not using HTTPS, remove the s in the URL.</span><span class="sxs-lookup"><span data-stu-id="9649e-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="9649e-370">Create Users and Assign Roles</span><span class="sxs-lookup"><span data-stu-id="9649e-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="9649e-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span><span class="sxs-lookup"><span data-stu-id="9649e-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="9649e-372">For more information, see the following:</span><span class="sxs-lookup"><span data-stu-id="9649e-372">For more information, see the following:</span></span>

* [<span data-ttu-id="9649e-373">Create a local user account</span><span class="sxs-lookup"><span data-stu-id="9649e-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="9649e-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="9649e-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="9649e-375">Create and Manage Role Assignments</span><span class="sxs-lookup"><span data-stu-id="9649e-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="9649e-376">To Create and Publish Reports to the Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="9649e-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="9649e-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span><span class="sxs-lookup"><span data-stu-id="9649e-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="9649e-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="9649e-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="9649e-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="9649e-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span><span class="sxs-lookup"><span data-stu-id="9649e-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="9649e-381">To start Report builder the first time on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="9649e-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="9649e-382">Start your browser with administrative privileges.</span><span class="sxs-lookup"><span data-stu-id="9649e-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="9649e-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span><span class="sxs-lookup"><span data-stu-id="9649e-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="9649e-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="9649e-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9649e-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="9649e-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="9649e-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="9649e-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9649e-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="9649e-388">For more information, see the following:</span><span class="sxs-lookup"><span data-stu-id="9649e-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="9649e-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9649e-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="9649e-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="9649e-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="9649e-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="9649e-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="9649e-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span><span class="sxs-lookup"><span data-stu-id="9649e-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="9649e-393">Configure the project to connect to the web service URL.</span><span class="sxs-lookup"><span data-stu-id="9649e-393">Configure the project to connect to the web service URL.</span></span>
  
    ![ssdt project properties for SSRS project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sqlclassic/media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="9649e-395">**Use script**: Use script to copy report server content.</span><span class="sxs-lookup"><span data-stu-id="9649e-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="9649e-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="9649e-397">Minimize cost if you are not using the VM</span><span class="sxs-lookup"><span data-stu-id="9649e-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="9649e-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9649e-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="9649e-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span><span class="sxs-lookup"><span data-stu-id="9649e-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="9649e-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="9649e-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="9649e-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="9649e-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="9649e-402">More Information</span><span class="sxs-lookup"><span data-stu-id="9649e-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="9649e-403">Resources</span><span class="sxs-lookup"><span data-stu-id="9649e-403">Resources</span></span>
* <span data-ttu-id="9649e-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="9649e-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="9649e-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="9649e-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="9649e-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="9649e-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="9649e-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="9649e-408">Community Content</span><span class="sxs-lookup"><span data-stu-id="9649e-408">Community Content</span></span>
* <span data-ttu-id="9649e-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="9649e-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="9649e-410">Links to other resources for SQL Server in Azure VMs</span><span class="sxs-lookup"><span data-stu-id="9649e-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="9649e-411">SQL Server on Azure Virtual Machines Overview</span><span class="sxs-lookup"><span data-stu-id="9649e-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
















