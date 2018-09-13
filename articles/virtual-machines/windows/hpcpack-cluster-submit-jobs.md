---
title: Submit jobs to an HPC Pack cluster in Azure | Microsoft Docs
description: Learn how to set up an on-premises computer to submit jobs to an HPC Pack cluster in Azure
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 5cd3de3a34ab0935de183bad8de3ec3dd5c5137d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553793"
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-to-an-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="1b5fd-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span><span class="sxs-lookup"><span data-stu-id="1b5fd-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1b5fd-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="1b5fd-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span></span> <span data-ttu-id="1b5fd-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span></span>

![Submit a job to a cluster in Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="1b5fd-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1b5fd-108">Prerequisites</span></span>
* <span data-ttu-id="1b5fd-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to deploy the head node and cluster.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to deploy the head node and cluster.</span></span> <span data-ttu-id="1b5fd-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>
* <span data-ttu-id="1b5fd-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="1b5fd-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="1b5fd-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="1b5fd-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span></span>

## <a name="step-1-install-and-configure-the-web-components-on-the-head-node"></a><span data-ttu-id="1b5fd-115">Step 1: Install and configure the web components on the head node</span><span class="sxs-lookup"><span data-stu-id="1b5fd-115">Step 1: Install and configure the web components on the head node</span></span>
<span data-ttu-id="1b5fd-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span></span> <span data-ttu-id="1b5fd-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="1b5fd-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="1b5fd-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="1b5fd-120">Certain Azure quickstart templates for HPC Pack install and configure the web components automatically.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-120">Certain Azure quickstart templates for HPC Pack install and configure the web components automatically.</span></span> <span data-ttu-id="1b5fd-121">If you use the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to create the cluster, you can optionally install and configure the web components as part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-121">If you use the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to create the cluster, you can optionally install and configure the web components as part of the deployment.</span></span>
> 
> 

<span data-ttu-id="1b5fd-122">**To install the web components**</span><span class="sxs-lookup"><span data-stu-id="1b5fd-122">**To install the web components**</span></span>

1. <span data-ttu-id="1b5fd-123">Connect to the head node VM by using the credentials of a cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-123">Connect to the head node VM by using the credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="1b5fd-124">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-124">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span></span>
3. <span data-ttu-id="1b5fd-125">Follow the steps in the wizard to install the web components</span><span class="sxs-lookup"><span data-stu-id="1b5fd-125">Follow the steps in the wizard to install the web components</span></span>

<span data-ttu-id="1b5fd-126">**To configure the web components**</span><span class="sxs-lookup"><span data-stu-id="1b5fd-126">**To configure the web components**</span></span>

1. <span data-ttu-id="1b5fd-127">On the head node, start HPC PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-127">On the head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="1b5fd-128">To change directory to the location of the configuration script, type the following command:</span><span class="sxs-lookup"><span data-stu-id="1b5fd-128">To change directory to the location of the configuration script, type the following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="1b5fd-129">To configure the REST interface and start the HPC Web Service, type the following command:</span><span class="sxs-lookup"><span data-stu-id="1b5fd-129">To configure the REST interface and start the HPC Web Service, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="1b5fd-130">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-130">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span></span> <span data-ttu-id="1b5fd-131">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-131">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="1b5fd-132">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-132">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1b5fd-133">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-133">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span></span> <span data-ttu-id="1b5fd-134">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-134">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="1b5fd-135">To configure the web portal for job submission, type the following command:</span><span class="sxs-lookup"><span data-stu-id="1b5fd-135">To configure the web portal for job submission, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="1b5fd-136">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span><span class="sxs-lookup"><span data-stu-id="1b5fd-136">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-the-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="1b5fd-137">Step 2: Install the HPC Pack client utilities on an on-premises computer</span><span class="sxs-lookup"><span data-stu-id="1b5fd-137">Step 2: Install the HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="1b5fd-138">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-138">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="1b5fd-139">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-139">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="1b5fd-140">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-140">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span></span> <span data-ttu-id="1b5fd-141">The certificate must be in .CER format.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-141">The certificate must be in .CER format.</span></span>

<span data-ttu-id="1b5fd-142">**To export the certificate from the head node**</span><span class="sxs-lookup"><span data-stu-id="1b5fd-142">**To export the certificate from the head node**</span></span>

1. <span data-ttu-id="1b5fd-143">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-143">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span></span> <span data-ttu-id="1b5fd-144">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-144">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="1b5fd-145">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-145">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="1b5fd-146">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-146">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="1b5fd-147">Right-click the certificate, and click **All Tasks** > **Export**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-147">Right-click the certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="1b5fd-148">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-148">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span></span>
6. <span data-ttu-id="1b5fd-149">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-149">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="1b5fd-150">**To import the certificate on the client computer**</span><span class="sxs-lookup"><span data-stu-id="1b5fd-150">**To import the certificate on the client computer**</span></span>

1. <span data-ttu-id="1b5fd-151">Copy the certificate that you exported from the head node to a folder on the client computer.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-151">Copy the certificate that you exported from the head node to a folder on the client computer.</span></span>
2. <span data-ttu-id="1b5fd-152">On the client computer, run certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-152">On the client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="1b5fd-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="1b5fd-154">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-154">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="1b5fd-155">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-155">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span></span> <span data-ttu-id="1b5fd-156">For testing purposes, you can ignore this warning and complete the certificate import.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-156">For testing purposes, you can ignore this warning and complete the certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-the-cluster"></a><span data-ttu-id="1b5fd-157">Step 3: Run test jobs on the cluster</span><span class="sxs-lookup"><span data-stu-id="1b5fd-157">Step 3: Run test jobs on the cluster</span></span>
<span data-ttu-id="1b5fd-158">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-158">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span></span> <span data-ttu-id="1b5fd-159">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-159">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span></span> <span data-ttu-id="1b5fd-160">You can also use a web-based portal to submit jobs.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-160">You can also use a web-based portal to submit jobs.</span></span>

<span data-ttu-id="1b5fd-161">**To run job submission commands on the client computer**</span><span class="sxs-lookup"><span data-stu-id="1b5fd-161">**To run job submission commands on the client computer**</span></span>

1. <span data-ttu-id="1b5fd-162">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-162">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="1b5fd-163">Type a sample command.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-163">Type a sample command.</span></span> <span data-ttu-id="1b5fd-164">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span><span class="sxs-lookup"><span data-stu-id="1b5fd-164">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="1b5fd-165">or</span><span class="sxs-lookup"><span data-stu-id="1b5fd-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="1b5fd-166">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-166">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span></span> <span data-ttu-id="1b5fd-167">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span><span class="sxs-lookup"><span data-stu-id="1b5fd-167">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="1b5fd-168">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-168">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="1b5fd-169">You can choose to store the credentials locally for more job operations.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-169">You can choose to store the credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="1b5fd-170">A list of jobs appears.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-170">A list of jobs appears.</span></span>

<span data-ttu-id="1b5fd-171">**To use HPC Job Manager on the client computer**</span><span class="sxs-lookup"><span data-stu-id="1b5fd-171">**To use HPC Job Manager on the client computer**</span></span>

1. <span data-ttu-id="1b5fd-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="1b5fd-173">a.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-173">a.</span></span> <span data-ttu-id="1b5fd-174">In Control Panel on the client computer, start Credential Manager.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-174">In Control Panel on the client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="1b5fd-175">b.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-175">b.</span></span> <span data-ttu-id="1b5fd-176">Click **Windows Credentials** > **Add a generic credential**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="1b5fd-177">c.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-177">c.</span></span> <span data-ttu-id="1b5fd-178">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-178">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="1b5fd-179">On the client computer, start HPC Job Manager.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-179">On the client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="1b5fd-180">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-180">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="1b5fd-181">HPC Job Manager opens and shows a list of jobs on the head node.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-181">HPC Job Manager opens and shows a list of jobs on the head node.</span></span>

<span data-ttu-id="1b5fd-182">**To use the web portal running on the head node**</span><span class="sxs-lookup"><span data-stu-id="1b5fd-182">**To use the web portal running on the head node**</span></span>

1. <span data-ttu-id="1b5fd-183">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span><span class="sxs-lookup"><span data-stu-id="1b5fd-183">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="1b5fd-184">or</span><span class="sxs-lookup"><span data-stu-id="1b5fd-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="1b5fd-185">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-185">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="1b5fd-186">(You can also add other cluster users in different roles.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="1b5fd-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="1b5fd-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="1b5fd-188">The web portal opens to the job list view.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-188">The web portal opens to the job list view.</span></span>
3. <span data-ttu-id="1b5fd-189">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-189">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span></span>
4. <span data-ttu-id="1b5fd-190">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-190">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="1b5fd-191">The job submission page appears.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-191">The job submission page appears.</span></span>
5. <span data-ttu-id="1b5fd-192">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-192">Click **Submit**.</span></span> <span data-ttu-id="1b5fd-193">If prompted, provide the domain credentials of the HPC cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-193">If prompted, provide the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="1b5fd-194">The job is submitted, and the job ID appears on the **My Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="1b5fd-194">The job is submitted, and the job ID appears on the **My Jobs** page.</span></span>
6. <span data-ttu-id="1b5fd-195">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-195">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b5fd-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b5fd-196">Next steps</span></span>
* <span data-ttu-id="1b5fd-197">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-197">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="1b5fd-198">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="1b5fd-198">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png

