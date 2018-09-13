---
title: Submit jobs to an HPC Pack cluster in Azure | Microsoft Docs
description: Learn how to set up an on-premises computer to submit jobs to an HPC Pack cluster in Azure
services: virtual-machines-windows
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 05/14/2018
ms.author: danlep
ms.openlocfilehash: e6a3a5b7cdaac2fbc535a8ccc9dab5d0b824c2e0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809054"
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-to-an-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="06d28-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span><span class="sxs-lookup"><span data-stu-id="06d28-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="06d28-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="06d28-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="06d28-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="06d28-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span></span> <span data-ttu-id="06d28-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="06d28-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span></span>

![Submit a job to a cluster in Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="06d28-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="06d28-108">Prerequisites</span></span>
* <span data-ttu-id="06d28-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) to deploy the head node and cluster.</span><span class="sxs-lookup"><span data-stu-id="06d28-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) to deploy the head node and cluster.</span></span> <span data-ttu-id="06d28-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span><span class="sxs-lookup"><span data-stu-id="06d28-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>
* <span data-ttu-id="06d28-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="06d28-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="06d28-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span><span class="sxs-lookup"><span data-stu-id="06d28-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="06d28-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack is available from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56360).</span><span class="sxs-lookup"><span data-stu-id="06d28-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack is available from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56360).</span></span> <span data-ttu-id="06d28-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span><span class="sxs-lookup"><span data-stu-id="06d28-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span></span>

## <a name="step-1-install-and-configure-the-web-components-on-the-head-node"></a><span data-ttu-id="06d28-115">Step 1: Install and configure the web components on the head node</span><span class="sxs-lookup"><span data-stu-id="06d28-115">Step 1: Install and configure the web components on the head node</span></span>
<span data-ttu-id="06d28-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span><span class="sxs-lookup"><span data-stu-id="06d28-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span></span> <span data-ttu-id="06d28-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span><span class="sxs-lookup"><span data-stu-id="06d28-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="06d28-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="06d28-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="06d28-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="06d28-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="06d28-120">Certain Azure quickstart templates for HPC Pack clusters install and configure the web components automatically.</span><span class="sxs-lookup"><span data-stu-id="06d28-120">Certain Azure quickstart templates for HPC Pack clusters install and configure the web components automatically.</span></span>
> 
> 

<span data-ttu-id="06d28-121">**To install the web components**</span><span class="sxs-lookup"><span data-stu-id="06d28-121">**To install the web components**</span></span>

1. <span data-ttu-id="06d28-122">Connect to the head node VM by using the credentials of a cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="06d28-122">Connect to the head node VM by using the credentials of a cluster administrator.</span></span>
1. <span data-ttu-id="06d28-123">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span><span class="sxs-lookup"><span data-stu-id="06d28-123">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span></span>
1. <span data-ttu-id="06d28-124">Follow the steps in the wizard to install the web components</span><span class="sxs-lookup"><span data-stu-id="06d28-124">Follow the steps in the wizard to install the web components</span></span>

<span data-ttu-id="06d28-125">**To configure the web components**</span><span class="sxs-lookup"><span data-stu-id="06d28-125">**To configure the web components**</span></span>

1. <span data-ttu-id="06d28-126">On the head node, start HPC PowerShell as an administrator.</span><span class="sxs-lookup"><span data-stu-id="06d28-126">On the head node, start HPC PowerShell as an administrator.</span></span>
1. <span data-ttu-id="06d28-127">To change directory to the location of the configuration script, type the following command:</span><span class="sxs-lookup"><span data-stu-id="06d28-127">To change directory to the location of the configuration script, type the following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
1. <span data-ttu-id="06d28-128">To configure the REST interface and start the HPC Web Service, type the following command:</span><span class="sxs-lookup"><span data-stu-id="06d28-128">To configure the REST interface and start the HPC Web Service, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
1. <span data-ttu-id="06d28-129">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span><span class="sxs-lookup"><span data-stu-id="06d28-129">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span></span> <span data-ttu-id="06d28-130">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="06d28-130">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="06d28-131">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="06d28-131">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="06d28-132">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="06d28-132">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span></span> <span data-ttu-id="06d28-133">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="06d28-133">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
1. <span data-ttu-id="06d28-134">To configure the web portal for job submission, type the following command:</span><span class="sxs-lookup"><span data-stu-id="06d28-134">To configure the web portal for job submission, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
1. <span data-ttu-id="06d28-135">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span><span class="sxs-lookup"><span data-stu-id="06d28-135">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-the-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="06d28-136">Step 2: Install the HPC Pack client utilities on an on-premises computer</span><span class="sxs-lookup"><span data-stu-id="06d28-136">Step 2: Install the HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="06d28-137">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56360).</span><span class="sxs-lookup"><span data-stu-id="06d28-137">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=56360).</span></span> <span data-ttu-id="06d28-138">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span><span class="sxs-lookup"><span data-stu-id="06d28-138">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="06d28-139">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span><span class="sxs-lookup"><span data-stu-id="06d28-139">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span></span> <span data-ttu-id="06d28-140">The certificate must be in .CER format.</span><span class="sxs-lookup"><span data-stu-id="06d28-140">The certificate must be in .CER format.</span></span>

<span data-ttu-id="06d28-141">**To export the certificate from the head node**</span><span class="sxs-lookup"><span data-stu-id="06d28-141">**To export the certificate from the head node**</span></span>

1. <span data-ttu-id="06d28-142">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span><span class="sxs-lookup"><span data-stu-id="06d28-142">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span></span> <span data-ttu-id="06d28-143">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="06d28-143">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
1. <span data-ttu-id="06d28-144">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span><span class="sxs-lookup"><span data-stu-id="06d28-144">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
1. <span data-ttu-id="06d28-145">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="06d28-145">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
1. <span data-ttu-id="06d28-146">Right-click the certificate, and click **All Tasks** > **Export**.</span><span class="sxs-lookup"><span data-stu-id="06d28-146">Right-click the certificate, and click **All Tasks** > **Export**.</span></span>
1. <span data-ttu-id="06d28-147">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span><span class="sxs-lookup"><span data-stu-id="06d28-147">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span></span>
1. <span data-ttu-id="06d28-148">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span><span class="sxs-lookup"><span data-stu-id="06d28-148">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="06d28-149">**To import the certificate on the client computer**</span><span class="sxs-lookup"><span data-stu-id="06d28-149">**To import the certificate on the client computer**</span></span>

1. <span data-ttu-id="06d28-150">Copy the certificate that you exported from the head node to a folder on the client computer.</span><span class="sxs-lookup"><span data-stu-id="06d28-150">Copy the certificate that you exported from the head node to a folder on the client computer.</span></span>
1. <span data-ttu-id="06d28-151">On the client computer, run certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="06d28-151">On the client computer, run certmgr.msc.</span></span>
1. <span data-ttu-id="06d28-152">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span><span class="sxs-lookup"><span data-stu-id="06d28-152">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
1. <span data-ttu-id="06d28-153">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span><span class="sxs-lookup"><span data-stu-id="06d28-153">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="06d28-154">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span><span class="sxs-lookup"><span data-stu-id="06d28-154">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span></span> <span data-ttu-id="06d28-155">For testing purposes, you can ignore this warning and complete the certificate import.</span><span class="sxs-lookup"><span data-stu-id="06d28-155">For testing purposes, you can ignore this warning and complete the certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-the-cluster"></a><span data-ttu-id="06d28-156">Step 3: Run test jobs on the cluster</span><span class="sxs-lookup"><span data-stu-id="06d28-156">Step 3: Run test jobs on the cluster</span></span>
<span data-ttu-id="06d28-157">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="06d28-157">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span></span> <span data-ttu-id="06d28-158">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span><span class="sxs-lookup"><span data-stu-id="06d28-158">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span></span> <span data-ttu-id="06d28-159">You can also use a web-based portal to submit jobs.</span><span class="sxs-lookup"><span data-stu-id="06d28-159">You can also use a web-based portal to submit jobs.</span></span>

<span data-ttu-id="06d28-160">**To run job submission commands on the client computer**</span><span class="sxs-lookup"><span data-stu-id="06d28-160">**To run job submission commands on the client computer**</span></span>

1. <span data-ttu-id="06d28-161">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span><span class="sxs-lookup"><span data-stu-id="06d28-161">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span></span>
1. <span data-ttu-id="06d28-162">Type a sample command.</span><span class="sxs-lookup"><span data-stu-id="06d28-162">Type a sample command.</span></span> <span data-ttu-id="06d28-163">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span><span class="sxs-lookup"><span data-stu-id="06d28-163">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="06d28-164">or</span><span class="sxs-lookup"><span data-stu-id="06d28-164">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="06d28-165">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span><span class="sxs-lookup"><span data-stu-id="06d28-165">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span></span> <span data-ttu-id="06d28-166">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span><span class="sxs-lookup"><span data-stu-id="06d28-166">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span></span>
   > 
   > 
1. <span data-ttu-id="06d28-167">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span><span class="sxs-lookup"><span data-stu-id="06d28-167">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="06d28-168">You can choose to store the credentials locally for more job operations.</span><span class="sxs-lookup"><span data-stu-id="06d28-168">You can choose to store the credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="06d28-169">A list of jobs appears.</span><span class="sxs-lookup"><span data-stu-id="06d28-169">A list of jobs appears.</span></span>

<span data-ttu-id="06d28-170">**To use HPC Job Manager on the client computer**</span><span class="sxs-lookup"><span data-stu-id="06d28-170">**To use HPC Job Manager on the client computer**</span></span>

1. <span data-ttu-id="06d28-171">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span><span class="sxs-lookup"><span data-stu-id="06d28-171">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="06d28-172">a.</span><span class="sxs-lookup"><span data-stu-id="06d28-172">a.</span></span> <span data-ttu-id="06d28-173">In Control Panel on the client computer, start Credential Manager.</span><span class="sxs-lookup"><span data-stu-id="06d28-173">In Control Panel on the client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="06d28-174">b.</span><span class="sxs-lookup"><span data-stu-id="06d28-174">b.</span></span> <span data-ttu-id="06d28-175">Click **Windows Credentials** > **Add a generic credential**.</span><span class="sxs-lookup"><span data-stu-id="06d28-175">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="06d28-176">c.</span><span class="sxs-lookup"><span data-stu-id="06d28-176">c.</span></span> <span data-ttu-id="06d28-177">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span><span class="sxs-lookup"><span data-stu-id="06d28-177">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span></span>
1. <span data-ttu-id="06d28-178">On the client computer, start HPC Job Manager.</span><span class="sxs-lookup"><span data-stu-id="06d28-178">On the client computer, start HPC Job Manager.</span></span>
1. <span data-ttu-id="06d28-179">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="06d28-179">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="06d28-180">HPC Job Manager opens and shows a list of jobs on the head node.</span><span class="sxs-lookup"><span data-stu-id="06d28-180">HPC Job Manager opens and shows a list of jobs on the head node.</span></span>

<span data-ttu-id="06d28-181">**To use the web portal running on the head node**</span><span class="sxs-lookup"><span data-stu-id="06d28-181">**To use the web portal running on the head node**</span></span>

1. <span data-ttu-id="06d28-182">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span><span class="sxs-lookup"><span data-stu-id="06d28-182">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="06d28-183">or</span><span class="sxs-lookup"><span data-stu-id="06d28-183">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
1. <span data-ttu-id="06d28-184">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="06d28-184">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="06d28-185">(You can also add other cluster users in different roles.</span><span class="sxs-lookup"><span data-stu-id="06d28-185">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="06d28-186">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="06d28-186">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="06d28-187">The web portal opens to the job list view.</span><span class="sxs-lookup"><span data-stu-id="06d28-187">The web portal opens to the job list view.</span></span>
1. <span data-ttu-id="06d28-188">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span><span class="sxs-lookup"><span data-stu-id="06d28-188">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span></span>
1. <span data-ttu-id="06d28-189">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="06d28-189">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="06d28-190">The job submission page appears.</span><span class="sxs-lookup"><span data-stu-id="06d28-190">The job submission page appears.</span></span>
1. <span data-ttu-id="06d28-191">Click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="06d28-191">Click **Submit**.</span></span> <span data-ttu-id="06d28-192">If prompted, provide the domain credentials of the HPC cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="06d28-192">If prompted, provide the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="06d28-193">The job is submitted, and the job ID appears on the **My Jobs** page.</span><span class="sxs-lookup"><span data-stu-id="06d28-193">The job is submitted, and the job ID appears on the **My Jobs** page.</span></span>
1. <span data-ttu-id="06d28-194">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span><span class="sxs-lookup"><span data-stu-id="06d28-194">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="06d28-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="06d28-195">Next steps</span></span>
* <span data-ttu-id="06d28-196">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="06d28-196">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="06d28-197">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="06d28-197">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
