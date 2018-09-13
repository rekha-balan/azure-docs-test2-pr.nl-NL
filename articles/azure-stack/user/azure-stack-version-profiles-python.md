---
title: Using API version profiles with Python in Azure Stack | Microsoft Docs
description: Learn about using API version profiles with Python in Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.reviewer: sijuman
<!-- dev: viananth -->
ms.openlocfilehash: c55dcf0736642690f245f680db5cb1620c2175e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871489"
---
# <a name="use-api-version-profiles-with-python-in-azure-stack"></a><span data-ttu-id="00d50-103">Use API version profiles with Python in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="00d50-103">Use API version profiles with Python in Azure Stack</span></span>

<span data-ttu-id="00d50-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="00d50-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

## <a name="python-and-api-version-profiles"></a><span data-ttu-id="00d50-105">Python and API version profiles</span><span class="sxs-lookup"><span data-stu-id="00d50-105">Python and API version profiles</span></span>

<span data-ttu-id="00d50-106">The Python SDK supports API version profiles to target different cloud platforms such as Azure Stack and global Azure.</span><span class="sxs-lookup"><span data-stu-id="00d50-106">The Python SDK supports API version profiles to target different cloud platforms such as Azure Stack and global Azure.</span></span> <span data-ttu-id="00d50-107">You can use API profiles in creating solutions for a hybrid cloud.</span><span class="sxs-lookup"><span data-stu-id="00d50-107">You can use API profiles in creating solutions for a hybrid cloud.</span></span> <span data-ttu-id="00d50-108">The Python SDK supports the following API profiles:</span><span class="sxs-lookup"><span data-stu-id="00d50-108">The Python SDK supports the following API profiles:</span></span>

1. <span data-ttu-id="00d50-109">**latest**</span><span class="sxs-lookup"><span data-stu-id="00d50-109">**latest**</span></span>  
    <span data-ttu-id="00d50-110">The profile targets the most recent API versions for all service providers in the Azure Platform.</span><span class="sxs-lookup"><span data-stu-id="00d50-110">The profile targets the most recent API versions for all service providers in the Azure Platform.</span></span>
2.  <span data-ttu-id="00d50-111">**2017-03-09-profile**</span><span class="sxs-lookup"><span data-stu-id="00d50-111">**2017-03-09-profile**</span></span>  
    <span data-ttu-id="00d50-112">**2017-03-09-profile**</span><span class="sxs-lookup"><span data-stu-id="00d50-112">**2017-03-09-profile**</span></span>  
    <span data-ttu-id="00d50-113">The profile targets the API versions of the resource providers supported by Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="00d50-113">The profile targets the API versions of the resource providers supported by Azure Stack.</span></span>

    <span data-ttu-id="00d50-114">For more information about API profiles and Azure Stack, see [Manage API version profiles in Azure Stack](azure-stack-version-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="00d50-114">For more information about API profiles and Azure Stack, see [Manage API version profiles in Azure Stack](azure-stack-version-profiles.md).</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="00d50-115">Install Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="00d50-115">Install Azure Python SDK</span></span>

1.  <span data-ttu-id="00d50-116">Install Git from [the official site](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="00d50-116">Install Git from [the official site](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
2.  <span data-ttu-id="00d50-117">For Instructions to install the Python SDK, see [Azure for Python developers](https://docs.microsoft.com/python/azure/python-sdk-azure-install?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="00d50-117">For Instructions to install the Python SDK, see [Azure for Python developers](https://docs.microsoft.com/python/azure/python-sdk-azure-install?view=azure-python).</span></span>
3.  <span data-ttu-id="00d50-118">If not available, create a subscription and save the Subscription ID to be used later.</span><span class="sxs-lookup"><span data-stu-id="00d50-118">If not available, create a subscription and save the Subscription ID to be used later.</span></span> <span data-ttu-id="00d50-119">For Instructions to create a subscription, see [Create subscriptions to offers in Azure Stack](../azure-stack-subscribe-plan-provision-vm.md).</span><span class="sxs-lookup"><span data-stu-id="00d50-119">For Instructions to create a subscription, see [Create subscriptions to offers in Azure Stack](../azure-stack-subscribe-plan-provision-vm.md).</span></span> 
4.  <span data-ttu-id="00d50-120">Create a service principal and save its ID and secret.</span><span class="sxs-lookup"><span data-stu-id="00d50-120">Create a service principal and save its ID and secret.</span></span> <span data-ttu-id="00d50-121">For instructions to create a service principal for Azure Stack, see [Provide applications access to Azure Stack](../azure-stack-create-service-principals.md).</span><span class="sxs-lookup"><span data-stu-id="00d50-121">For instructions to create a service principal for Azure Stack, see [Provide applications access to Azure Stack](../azure-stack-create-service-principals.md).</span></span> 
5.  <span data-ttu-id="00d50-122">Make sure your service principal has contributor/owner role on your subscription.</span><span class="sxs-lookup"><span data-stu-id="00d50-122">Make sure your service principal has contributor/owner role on your subscription.</span></span> <span data-ttu-id="00d50-123">For instructions on how to assign role to service principal, see [Provide applications access to Azure Stack](../azure-stack-create-service-principals.md).</span><span class="sxs-lookup"><span data-stu-id="00d50-123">For instructions on how to assign role to service principal, see [Provide applications access to Azure Stack](../azure-stack-create-service-principals.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00d50-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="00d50-124">Prerequisites</span></span>

<span data-ttu-id="00d50-125">In order to use Python Azure SDK with Azure Stack, you must supply the following values, and then set values with environment variables.</span><span class="sxs-lookup"><span data-stu-id="00d50-125">In order to use Python Azure SDK with Azure Stack, you must supply the following values, and then set values with environment variables.</span></span> <span data-ttu-id="00d50-126">See the instructions after the table for your operating system on setting the environmental variables.</span><span class="sxs-lookup"><span data-stu-id="00d50-126">See the instructions after the table for your operating system on setting the environmental variables.</span></span> 

| <span data-ttu-id="00d50-127">Value</span><span class="sxs-lookup"><span data-stu-id="00d50-127">Value</span></span> | <span data-ttu-id="00d50-128">Environment variables</span><span class="sxs-lookup"><span data-stu-id="00d50-128">Environment variables</span></span> | <span data-ttu-id="00d50-129">Description</span><span class="sxs-lookup"><span data-stu-id="00d50-129">Description</span></span> |
|---------------------------|-----------------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="00d50-130">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="00d50-130">Tenant ID</span></span> | <span data-ttu-id="00d50-131">AZURE_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="00d50-131">AZURE_TENANT_ID</span></span> | <span data-ttu-id="00d50-132">The value of your Azure Stack [tenant ID](../azure-stack-identity-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00d50-132">The value of your Azure Stack [tenant ID](../azure-stack-identity-overview.md).</span></span> |
| <span data-ttu-id="00d50-133">Client ID</span><span class="sxs-lookup"><span data-stu-id="00d50-133">Client ID</span></span> | <span data-ttu-id="00d50-134">AZURE_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="00d50-134">AZURE_CLIENT_ID</span></span> | <span data-ttu-id="00d50-135">The service principal application ID saved when service principal was created on the previous section of this document.</span><span class="sxs-lookup"><span data-stu-id="00d50-135">The service principal application ID saved when service principal was created on the previous section of this document.</span></span> |
| <span data-ttu-id="00d50-136">Subscription ID</span><span class="sxs-lookup"><span data-stu-id="00d50-136">Subscription ID</span></span> | <span data-ttu-id="00d50-137">AZURE_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="00d50-137">AZURE_SUBSCRIPTION_ID</span></span> | <span data-ttu-id="00d50-138">The [subscription ID](../azure-stack-plan-offer-quota-overview.md#subscriptions) is how you access offers in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="00d50-138">The [subscription ID](../azure-stack-plan-offer-quota-overview.md#subscriptions) is how you access offers in Azure Stack.</span></span> |
| <span data-ttu-id="00d50-139">Client Secret</span><span class="sxs-lookup"><span data-stu-id="00d50-139">Client Secret</span></span> | <span data-ttu-id="00d50-140">AZURE_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="00d50-140">AZURE_CLIENT_SECRET</span></span> | <span data-ttu-id="00d50-141">The service principal application Secret saved when service principal was created.</span><span class="sxs-lookup"><span data-stu-id="00d50-141">The service principal application Secret saved when service principal was created.</span></span> |
| <span data-ttu-id="00d50-142">Resource Manager Endpoint</span><span class="sxs-lookup"><span data-stu-id="00d50-142">Resource Manager Endpoint</span></span> | <span data-ttu-id="00d50-143">ARM_ENDPOINT</span><span class="sxs-lookup"><span data-stu-id="00d50-143">ARM_ENDPOINT</span></span> | <span data-ttu-id="00d50-144">See [the Azure Stack resource manager endpoint](azure-stack-version-profiles-ruby.md#the-azure-stack-resource-manager-endpoint).</span><span class="sxs-lookup"><span data-stu-id="00d50-144">See [the Azure Stack resource manager endpoint](azure-stack-version-profiles-ruby.md#the-azure-stack-resource-manager-endpoint).</span></span> |


## <a name="python-samples-for-azure-stack"></a><span data-ttu-id="00d50-145">Python samples for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="00d50-145">Python samples for Azure Stack</span></span> 

<span data-ttu-id="00d50-146">You can use the following code samples to perform common management tasks for virtual machines in your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="00d50-146">You can use the following code samples to perform common management tasks for virtual machines in your Azure Stack.</span></span>

<span data-ttu-id="00d50-147">The code samples show you to:</span><span class="sxs-lookup"><span data-stu-id="00d50-147">The code samples show you to:</span></span>

- <span data-ttu-id="00d50-148">Create virtual machines:</span><span class="sxs-lookup"><span data-stu-id="00d50-148">Create virtual machines:</span></span>
    - <span data-ttu-id="00d50-149">Create a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="00d50-149">Create a Linux virtual machine</span></span>
    - <span data-ttu-id="00d50-150">Create a Windows virtual machine</span><span class="sxs-lookup"><span data-stu-id="00d50-150">Create a Windows virtual machine</span></span>
- <span data-ttu-id="00d50-151">Update a virtual machine:</span><span class="sxs-lookup"><span data-stu-id="00d50-151">Update a virtual machine:</span></span>
    - <span data-ttu-id="00d50-152">Expand a drive</span><span class="sxs-lookup"><span data-stu-id="00d50-152">Expand a drive</span></span>
    - <span data-ttu-id="00d50-153">Tag a virtual machine</span><span class="sxs-lookup"><span data-stu-id="00d50-153">Tag a virtual machine</span></span>
    - <span data-ttu-id="00d50-154">Attach data disks</span><span class="sxs-lookup"><span data-stu-id="00d50-154">Attach data disks</span></span>
    - <span data-ttu-id="00d50-155">Detach data disks</span><span class="sxs-lookup"><span data-stu-id="00d50-155">Detach data disks</span></span>
- <span data-ttu-id="00d50-156">Operate a virtual machine:</span><span class="sxs-lookup"><span data-stu-id="00d50-156">Operate a virtual machine:</span></span>
    - <span data-ttu-id="00d50-157">Start a virtual machine</span><span class="sxs-lookup"><span data-stu-id="00d50-157">Start a virtual machine</span></span>
    - <span data-ttu-id="00d50-158">Stop a virtual machine</span><span class="sxs-lookup"><span data-stu-id="00d50-158">Stop a virtual machine</span></span>
    - <span data-ttu-id="00d50-159">Restart a virtual machine</span><span class="sxs-lookup"><span data-stu-id="00d50-159">Restart a virtual machine</span></span>
- <span data-ttu-id="00d50-160">List virtual machines</span><span class="sxs-lookup"><span data-stu-id="00d50-160">List virtual machines</span></span>
- <span data-ttu-id="00d50-161">Delete a virtual machine</span><span class="sxs-lookup"><span data-stu-id="00d50-161">Delete a virtual machine</span></span>

<span data-ttu-id="00d50-162">To review the code to perform these operations, check out the **run_example()** function in the Python script **Hybrid/unmanaged-disks/example.py** in the GitHub Repo [virtual-machines-python-manage](https://github.com/viananth/virtual-machines-python-manage/tree/8643ed4bec62aae6fdb81518f68d835452872f88).</span><span class="sxs-lookup"><span data-stu-id="00d50-162">To review the code to perform these operations, check out the **run_example()** function in the Python script **Hybrid/unmanaged-disks/example.py** in the GitHub Repo [virtual-machines-python-manage](https://github.com/viananth/virtual-machines-python-manage/tree/8643ed4bec62aae6fdb81518f68d835452872f88).</span></span>

<span data-ttu-id="00d50-163">Each operation is clearly labeled with a comment and a print function.</span><span class="sxs-lookup"><span data-stu-id="00d50-163">Each operation is clearly labeled with a comment and a print function.</span></span>
<span data-ttu-id="00d50-164">The examples are not necessarily in the order shown in the above list.</span><span class="sxs-lookup"><span data-stu-id="00d50-164">The examples are not necessarily in the order shown in the above list.</span></span>


## <a name="run-the-python-sample"></a><span data-ttu-id="00d50-165">Run the Python sample</span><span class="sxs-lookup"><span data-stu-id="00d50-165">Run the Python sample</span></span>

1.  <span data-ttu-id="00d50-166">If you don't already have it, [install Python](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="00d50-166">If you don't already have it, [install Python](https://www.python.org/downloads/).</span></span>

    <span data-ttu-id="00d50-167">This sample (and the SDK) is compatible with Python 2.7, 3.4, 3.5 and 3.6.</span><span class="sxs-lookup"><span data-stu-id="00d50-167">This sample (and the SDK) is compatible with Python 2.7, 3.4, 3.5 and 3.6.</span></span>

2.  <span data-ttu-id="00d50-168">General recommendation for Python development is to use a Virtual Environment.</span><span class="sxs-lookup"><span data-stu-id="00d50-168">General recommendation for Python development is to use a Virtual Environment.</span></span> 
    <span data-ttu-id="00d50-169">For more information, see https://docs.python.org/3/tutorial/venv.html</span><span class="sxs-lookup"><span data-stu-id="00d50-169">For more information, see https://docs.python.org/3/tutorial/venv.html</span></span>
    
    <span data-ttu-id="00d50-170">Install and initialize the virtual environment with the "venv" module on Python 3 (you must install [virtualenv](https://pypi.python.org/pypi/virtualenv) for Python 2.7):</span><span class="sxs-lookup"><span data-stu-id="00d50-170">Install and initialize the virtual environment with the "venv" module on Python 3 (you must install [virtualenv](https://pypi.python.org/pypi/virtualenv) for Python 2.7):</span></span>

    ````bash
    python -m venv mytestenv # Might be "python3" or "py -3.6" depending on your Python installation
    cd mytestenv
    source bin/activate      # Linux shell (Bash, ZSH, etc.) only
    ./scripts/activate       # PowerShell only
    ./scripts/activate.bat   # Windows CMD only
    ````

3.  <span data-ttu-id="00d50-171">Clone the repository.</span><span class="sxs-lookup"><span data-stu-id="00d50-171">Clone the repository.</span></span>

    ````bash
    git clone https://github.com/Azure-Samples/virtual-machines-python-manage.git
    ````

4.  <span data-ttu-id="00d50-172">Install the dependencies using pip.</span><span class="sxs-lookup"><span data-stu-id="00d50-172">Install the dependencies using pip.</span></span>

    ````bash
    cd virtual-machines-python-manage\Hybrid
    pip install -r requirements.txt
    ````

5.  <span data-ttu-id="00d50-173">Create a [service principal](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals) to work with Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="00d50-173">Create a [service principal](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals) to work with Azure Stack.</span></span> <span data-ttu-id="00d50-174">Make sure your service principal has [contributor/owner role](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#assign-role-to-service-principal) on your subscription.</span><span class="sxs-lookup"><span data-stu-id="00d50-174">Make sure your service principal has [contributor/owner role](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#assign-role-to-service-principal) on your subscription.</span></span>

6.  <span data-ttu-id="00d50-175">Set the following variables and export these environment variables into your current shell.</span><span class="sxs-lookup"><span data-stu-id="00d50-175">Set the following variables and export these environment variables into your current shell.</span></span> 

    ```bash
    export AZURE_TENANT_ID={your tenant id}
    export AZURE_CLIENT_ID={your client id}
    export AZURE_CLIENT_SECRET={your client secret}
    export AZURE_SUBSCRIPTION_ID={your subscription id}
    export ARM_ENDPOINT={your AzureStack Resource Manager Endpoint}
    ```

7.  <span data-ttu-id="00d50-176">In order to run this sample, Ubuntu 16.04-LTS and WindowsServer 2012-R2-Datacenter images must be present in Azure Stack market place.</span><span class="sxs-lookup"><span data-stu-id="00d50-176">In order to run this sample, Ubuntu 16.04-LTS and WindowsServer 2012-R2-Datacenter images must be present in Azure Stack market place.</span></span> <span data-ttu-id="00d50-177">These can be either [downloaded from Azure](https://docs.microsoft.com/azure/azure-stack/azure-stack-download-azure-marketplace-item) or [added to Platform Image Repository](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-vm-image).</span><span class="sxs-lookup"><span data-stu-id="00d50-177">These can be either [downloaded from Azure](https://docs.microsoft.com/azure/azure-stack/azure-stack-download-azure-marketplace-item) or [added to Platform Image Repository](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-vm-image).</span></span>

8. <span data-ttu-id="00d50-178">Run the sample.</span><span class="sxs-lookup"><span data-stu-id="00d50-178">Run the sample.</span></span>

    ```
    python unmanaged-disks\example.py
    ```

## <a name="notes"></a><span data-ttu-id="00d50-179">Notes</span><span class="sxs-lookup"><span data-stu-id="00d50-179">Notes</span></span>

<span data-ttu-id="00d50-180">You may be tempted to try to retrieve a VM's OS disk by using `virtual_machine.storage_profile.os_disk`.</span><span class="sxs-lookup"><span data-stu-id="00d50-180">You may be tempted to try to retrieve a VM's OS disk by using `virtual_machine.storage_profile.os_disk`.</span></span>
<span data-ttu-id="00d50-181">In some cases, this may do what you want, but be aware that it gives you an `OSDisk` object.</span><span class="sxs-lookup"><span data-stu-id="00d50-181">In some cases, this may do what you want, but be aware that it gives you an `OSDisk` object.</span></span>
<span data-ttu-id="00d50-182">In order to update the OS Disk's size, as `example.py` does, you need not an `OSDisk` object but a `Disk` object.</span><span class="sxs-lookup"><span data-stu-id="00d50-182">In order to update the OS Disk's size, as `example.py` does, you need not an `OSDisk` object but a `Disk` object.</span></span>
<span data-ttu-id="00d50-183">`example.py` gets the `Disk` object with the following:</span><span class="sxs-lookup"><span data-stu-id="00d50-183">`example.py` gets the `Disk` object with the following:</span></span>

```python
os_disk_name = virtual_machine.storage_profile.os_disk.name
os_disk = compute_client.disks.get(GROUP_NAME, os_disk_name)
```

## <a name="next-steps"></a><span data-ttu-id="00d50-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="00d50-184">Next steps</span></span>

- [<span data-ttu-id="00d50-185">Azure Python Development Center</span><span class="sxs-lookup"><span data-stu-id="00d50-185">Azure Python Development Center</span></span>](https://azure.microsoft.com/develop/python/)
- [<span data-ttu-id="00d50-186">Azure Virtual Machines documentation</span><span class="sxs-lookup"><span data-stu-id="00d50-186">Azure Virtual Machines documentation</span></span>](https://azure.microsoft.com/services/virtual-machines/)
- [<span data-ttu-id="00d50-187">Learning Path for Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="00d50-187">Learning Path for Virtual Machines</span></span>](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
- <span data-ttu-id="00d50-188">If you don't have a Microsoft Azure subscription, you can get a FREE trial account [here](http://go.microsoft.com/fwlink/?LinkId=330212).</span><span class="sxs-lookup"><span data-stu-id="00d50-188">If you don't have a Microsoft Azure subscription, you can get a FREE trial account [here](http://go.microsoft.com/fwlink/?LinkId=330212).</span></span>
