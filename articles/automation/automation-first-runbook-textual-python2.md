---
title: My first Python runbook in Azure Automation
description: Tutorial that walks you through the creation, testing, and publishing of a simple Python runbook.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 06/26/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 386c2ecfdac44158f5d87034657491fa9598e3ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856037"
---
# <a name="my-first-python-runbook"></a><span data-ttu-id="a847b-103">My first Python runbook</span><span class="sxs-lookup"><span data-stu-id="a847b-103">My first Python runbook</span></span>

> [!div class="op_single_selector"]
> - [Graphical](automation-first-runbook-graphical.md)
> - [PowerShell](automation-first-runbook-textual-powershell.md)
> - [PowerShell Workflow](automation-first-runbook-textual.md)
> - [Python](automation-first-runbook-textual-python2.md)

<span data-ttu-id="a847b-108">This tutorial walks you through the creation of a [Python runbook](automation-runbook-types.md#python-runbooks) in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="a847b-108">This tutorial walks you through the creation of a [Python runbook](automation-runbook-types.md#python-runbooks) in Azure Automation.</span></span> <span data-ttu-id="a847b-109">You start with a simple runbook that you test and publish.</span><span class="sxs-lookup"><span data-stu-id="a847b-109">You start with a simple runbook that you test and publish.</span></span> <span data-ttu-id="a847b-110">Then you modify the runbook to actually manage Azure resources, in this case starting an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a847b-110">Then you modify the runbook to actually manage Azure resources, in this case starting an Azure virtual machine.</span></span> <span data-ttu-id="a847b-111">Lastly, you make the runbook more robust by adding runbook parameters.</span><span class="sxs-lookup"><span data-stu-id="a847b-111">Lastly, you make the runbook more robust by adding runbook parameters.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a847b-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a847b-112">Prerequisites</span></span>

<span data-ttu-id="a847b-113">To complete this tutorial, you need the following:</span><span class="sxs-lookup"><span data-stu-id="a847b-113">To complete this tutorial, you need the following:</span></span>

- <span data-ttu-id="a847b-114">Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a847b-114">Azure subscription.</span></span> <span data-ttu-id="a847b-115">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a847b-115">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>
- <span data-ttu-id="a847b-116">[Automation account](automation-offering-get-started.md) to hold the runbook and authenticate to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a847b-116">[Automation account](automation-offering-get-started.md) to hold the runbook and authenticate to Azure resources.</span></span> <span data-ttu-id="a847b-117">This account must have permission to start and stop the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a847b-117">This account must have permission to start and stop the virtual machine.</span></span>
- <span data-ttu-id="a847b-118">An Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a847b-118">An Azure virtual machine.</span></span> <span data-ttu-id="a847b-119">You stop and start this machine so it should not be a production VM.</span><span class="sxs-lookup"><span data-stu-id="a847b-119">You stop and start this machine so it should not be a production VM.</span></span>

## <a name="create-a-new-runbook"></a><span data-ttu-id="a847b-120">Create a new runbook</span><span class="sxs-lookup"><span data-stu-id="a847b-120">Create a new runbook</span></span>

<span data-ttu-id="a847b-121">You start by creating a simple runbook that outputs the text *Hello World*.</span><span class="sxs-lookup"><span data-stu-id="a847b-121">You start by creating a simple runbook that outputs the text *Hello World*.</span></span>

1. <span data-ttu-id="a847b-122">In the Azure portal, open your Automation account.</span><span class="sxs-lookup"><span data-stu-id="a847b-122">In the Azure portal, open your Automation account.</span></span>

    <span data-ttu-id="a847b-123">The Automation account page gives you a quick view of the resources in this account.</span><span class="sxs-lookup"><span data-stu-id="a847b-123">The Automation account page gives you a quick view of the resources in this account.</span></span> <span data-ttu-id="a847b-124">You should already have some assets.</span><span class="sxs-lookup"><span data-stu-id="a847b-124">You should already have some assets.</span></span> <span data-ttu-id="a847b-125">Most of those assets are the modules that are automatically included in a new Automation account.</span><span class="sxs-lookup"><span data-stu-id="a847b-125">Most of those assets are the modules that are automatically included in a new Automation account.</span></span> <span data-ttu-id="a847b-126">You should also have the Credential asset that's mentioned in the [prerequisites](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="a847b-126">You should also have the Credential asset that's mentioned in the [prerequisites](#prerequisites).</span></span><br>

1. <span data-ttu-id="a847b-127">Select **Runbooks** under **PROCESS MANAGEMENT** to open the list of runbooks.</span><span class="sxs-lookup"><span data-stu-id="a847b-127">Select **Runbooks** under **PROCESS MANAGEMENT** to open the list of runbooks.</span></span>
1. <span data-ttu-id="a847b-128">Select **+ Add a runbook** to create a new runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-128">Select **+ Add a runbook** to create a new runbook.</span></span>
1. <span data-ttu-id="a847b-129">Give the runbook the name *MyFirstRunbook-Python*.</span><span class="sxs-lookup"><span data-stu-id="a847b-129">Give the runbook the name *MyFirstRunbook-Python*.</span></span>
1. <span data-ttu-id="a847b-130">In this case, you're going to create a [Python runbook](automation-runbook-types.md#python-runbooks) so select **Python 2** for **Runbook type**.</span><span class="sxs-lookup"><span data-stu-id="a847b-130">In this case, you're going to create a [Python runbook](automation-runbook-types.md#python-runbooks) so select **Python 2** for **Runbook type**.</span></span>
1. <span data-ttu-id="a847b-131">Click **Create** to create the runbook and open the textual editor.</span><span class="sxs-lookup"><span data-stu-id="a847b-131">Click **Create** to create the runbook and open the textual editor.</span></span>

## <a name="add-code-to-the-runbook"></a><span data-ttu-id="a847b-132">Add code to the runbook</span><span class="sxs-lookup"><span data-stu-id="a847b-132">Add code to the runbook</span></span>

<span data-ttu-id="a847b-133">Now you add a simple command to print the text "Hello World":</span><span class="sxs-lookup"><span data-stu-id="a847b-133">Now you add a simple command to print the text "Hello World":</span></span>

```python
print("Hello World!")
```

<span data-ttu-id="a847b-134">Click **Save** to save the runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-134">Click **Save** to save the runbook.</span></span>

## <a name="test-the-runbook"></a><span data-ttu-id="a847b-135">Test the runbook</span><span class="sxs-lookup"><span data-stu-id="a847b-135">Test the runbook</span></span>

<span data-ttu-id="a847b-136">Before you publish the runbook to make it available in production, you want to test it to make sure that it works properly.</span><span class="sxs-lookup"><span data-stu-id="a847b-136">Before you publish the runbook to make it available in production, you want to test it to make sure that it works properly.</span></span> <span data-ttu-id="a847b-137">When you test a runbook, you run its **Draft** version and view its output interactively.</span><span class="sxs-lookup"><span data-stu-id="a847b-137">When you test a runbook, you run its **Draft** version and view its output interactively.</span></span>

1. <span data-ttu-id="a847b-138">Click **Test pane** to open the Test pane.</span><span class="sxs-lookup"><span data-stu-id="a847b-138">Click **Test pane** to open the Test pane.</span></span>
1. <span data-ttu-id="a847b-139">Click **Start** to start the test.</span><span class="sxs-lookup"><span data-stu-id="a847b-139">Click **Start** to start the test.</span></span> <span data-ttu-id="a847b-140">This should be the only enabled option.</span><span class="sxs-lookup"><span data-stu-id="a847b-140">This should be the only enabled option.</span></span>
1. <span data-ttu-id="a847b-141">A [runbook job](automation-runbook-execution.md) is created and its status displayed.</span><span class="sxs-lookup"><span data-stu-id="a847b-141">A [runbook job](automation-runbook-execution.md) is created and its status displayed.</span></span>
   <span data-ttu-id="a847b-142">The job status starts as *Queued* indicating that it is waiting for a runbook worker in the cloud to come available.</span><span class="sxs-lookup"><span data-stu-id="a847b-142">The job status starts as *Queued* indicating that it is waiting for a runbook worker in the cloud to come available.</span></span> <span data-ttu-id="a847b-143">It moves to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span><span class="sxs-lookup"><span data-stu-id="a847b-143">It moves to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>
1. <span data-ttu-id="a847b-144">When the runbook job completes, its output is displayed.</span><span class="sxs-lookup"><span data-stu-id="a847b-144">When the runbook job completes, its output is displayed.</span></span> <span data-ttu-id="a847b-145">In this case, you should see *Hello World*.</span><span class="sxs-lookup"><span data-stu-id="a847b-145">In this case, you should see *Hello World*.</span></span>
1. <span data-ttu-id="a847b-146">Close the Test pane to return to the canvas.</span><span class="sxs-lookup"><span data-stu-id="a847b-146">Close the Test pane to return to the canvas.</span></span>

## <a name="publish-and-start-the-runbook"></a><span data-ttu-id="a847b-147">Publish and start the runbook</span><span class="sxs-lookup"><span data-stu-id="a847b-147">Publish and start the runbook</span></span>

<span data-ttu-id="a847b-148">The runbook that you created is still in draft mode.</span><span class="sxs-lookup"><span data-stu-id="a847b-148">The runbook that you created is still in draft mode.</span></span> <span data-ttu-id="a847b-149">You need to publish it before you can run it in production.</span><span class="sxs-lookup"><span data-stu-id="a847b-149">You need to publish it before you can run it in production.</span></span>
<span data-ttu-id="a847b-150">When you publish a runbook, you overwrite the existing published version with the Draft version.</span><span class="sxs-lookup"><span data-stu-id="a847b-150">When you publish a runbook, you overwrite the existing published version with the Draft version.</span></span>
<span data-ttu-id="a847b-151">In this case, you don't have a published version yet because you just created the runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-151">In this case, you don't have a published version yet because you just created the runbook.</span></span>

1. <span data-ttu-id="a847b-152">Click **Publish** to publish the runbook and then **Yes** when prompted.</span><span class="sxs-lookup"><span data-stu-id="a847b-152">Click **Publish** to publish the runbook and then **Yes** when prompted.</span></span>
1. <span data-ttu-id="a847b-153">If you scroll left to view the runbook in the **Runbooks** pane now, it shows an **Authoring Status** of **Published**.</span><span class="sxs-lookup"><span data-stu-id="a847b-153">If you scroll left to view the runbook in the **Runbooks** pane now, it shows an **Authoring Status** of **Published**.</span></span>
1. <span data-ttu-id="a847b-154">Scroll back to the right to view the pane for **MyFirstRunbook-Python**.</span><span class="sxs-lookup"><span data-stu-id="a847b-154">Scroll back to the right to view the pane for **MyFirstRunbook-Python**.</span></span>
   <span data-ttu-id="a847b-155">The options across the top allow us to start the runbook, view the runbook, schedule it to start at some time in the future, or create a [webhook](automation-webhooks.md) so it can be started through an HTTP call.</span><span class="sxs-lookup"><span data-stu-id="a847b-155">The options across the top allow us to start the runbook, view the runbook, schedule it to start at some time in the future, or create a [webhook](automation-webhooks.md) so it can be started through an HTTP call.</span></span>
1. <span data-ttu-id="a847b-156">You want to start the runbook, so click **Start** and then click **Ok** when the Start Runbook blade opens.</span><span class="sxs-lookup"><span data-stu-id="a847b-156">You want to start the runbook, so click **Start** and then click **Ok** when the Start Runbook blade opens.</span></span>
1. <span data-ttu-id="a847b-157">A job pane is opened for the runbook job that you created.</span><span class="sxs-lookup"><span data-stu-id="a847b-157">A job pane is opened for the runbook job that you created.</span></span> <span data-ttu-id="a847b-158">You can close this pane, but in this case you leave it open so you can watch the job's progress.</span><span class="sxs-lookup"><span data-stu-id="a847b-158">You can close this pane, but in this case you leave it open so you can watch the job's progress.</span></span>
1. <span data-ttu-id="a847b-159">The job status is shown in **Job Summary** and matches the statuses that you saw when you tested the runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-159">The job status is shown in **Job Summary** and matches the statuses that you saw when you tested the runbook.</span></span>
1. <span data-ttu-id="a847b-160">Once the runbook status shows *Completed*, click **Output**.</span><span class="sxs-lookup"><span data-stu-id="a847b-160">Once the runbook status shows *Completed*, click **Output**.</span></span> <span data-ttu-id="a847b-161">The Output pane is opened, and you can see your *Hello World*.</span><span class="sxs-lookup"><span data-stu-id="a847b-161">The Output pane is opened, and you can see your *Hello World*.</span></span>
1. <span data-ttu-id="a847b-162">Close the Output pane.</span><span class="sxs-lookup"><span data-stu-id="a847b-162">Close the Output pane.</span></span>
1. <span data-ttu-id="a847b-163">Click **All Logs** to open the Streams pane for the runbook job.</span><span class="sxs-lookup"><span data-stu-id="a847b-163">Click **All Logs** to open the Streams pane for the runbook job.</span></span> <span data-ttu-id="a847b-164">You should only see *Hello World* in the output stream, but this can show other streams for a runbook job such as Verbose and Error if the runbook writes to them.</span><span class="sxs-lookup"><span data-stu-id="a847b-164">You should only see *Hello World* in the output stream, but this can show other streams for a runbook job such as Verbose and Error if the runbook writes to them.</span></span>
1. <span data-ttu-id="a847b-165">Close the Streams pane and the Job pane to return to the MyFirstRunbook-Python pane.</span><span class="sxs-lookup"><span data-stu-id="a847b-165">Close the Streams pane and the Job pane to return to the MyFirstRunbook-Python pane.</span></span>
1. <span data-ttu-id="a847b-166">Click **Jobs** to open the Jobs pane for this runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-166">Click **Jobs** to open the Jobs pane for this runbook.</span></span> <span data-ttu-id="a847b-167">This lists all of the jobs created by this runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-167">This lists all of the jobs created by this runbook.</span></span> <span data-ttu-id="a847b-168">You should only see one job listed since you only ran the job once.</span><span class="sxs-lookup"><span data-stu-id="a847b-168">You should only see one job listed since you only ran the job once.</span></span>
1. <span data-ttu-id="a847b-169">You can click this job to open the same Job pane that you viewed when you started the runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-169">You can click this job to open the same Job pane that you viewed when you started the runbook.</span></span> <span data-ttu-id="a847b-170">This allows you to go back in time and view the details of any job that was created for a particular runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-170">This allows you to go back in time and view the details of any job that was created for a particular runbook.</span></span>

## <a name="add-authentication-to-manage-azure-resources"></a><span data-ttu-id="a847b-171">Add authentication to manage Azure resources</span><span class="sxs-lookup"><span data-stu-id="a847b-171">Add authentication to manage Azure resources</span></span>

<span data-ttu-id="a847b-172">You've tested and published your runbook, but so far it doesn't do anything useful.</span><span class="sxs-lookup"><span data-stu-id="a847b-172">You've tested and published your runbook, but so far it doesn't do anything useful.</span></span> <span data-ttu-id="a847b-173">You want to have it manage Azure resources.</span><span class="sxs-lookup"><span data-stu-id="a847b-173">You want to have it manage Azure resources.</span></span>
<span data-ttu-id="a847b-174">To manage Azure resources, the script has to authenticate using the credentials from your [Automation account](automation-offering-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a847b-174">To manage Azure resources, the script has to authenticate using the credentials from your [Automation account](automation-offering-get-started.md).</span></span>

> [!NOTE]
> The Automation account must have been created with the service principal feature for there to be a runas certificate.
> If your automation account was not created with the service principal, you can authenticate by using the method described at [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).

1. <span data-ttu-id="a847b-177">Open the textual editor by clicking **Edit** on the MyFirstRunbook-Python pane.</span><span class="sxs-lookup"><span data-stu-id="a847b-177">Open the textual editor by clicking **Edit** on the MyFirstRunbook-Python pane.</span></span>

1. <span data-ttu-id="a847b-178">Add the following code to authenticate to Azure:</span><span class="sxs-lookup"><span data-stu-id="a847b-178">Add the following code to authenticate to Azure:</span></span>

   ```python
   import os
   from azure.mgmt.compute import ComputeManagementClient
   import azure.mgmt.resource
   import automationassets

   def get_automation_runas_credential(runas_connection):
       from OpenSSL import crypto
       import binascii
       from msrestazure import azure_active_directory
       import adal

       # Get the Azure Automation RunAs service principal certificate
       cert = automationassets.get_automation_certificate("AzureRunAsCertificate")
       pks12_cert = crypto.load_pkcs12(cert)
       pem_pkey = crypto.dump_privatekey(crypto.FILETYPE_PEM,pks12_cert.get_privatekey())

       # Get run as connection information for the Azure Automation service principal
       application_id = runas_connection["ApplicationId"]
       thumbprint = runas_connection["CertificateThumbprint"]
       tenant_id = runas_connection["TenantId"]

       # Authenticate with service principal certificate
       resource ="https://management.core.windows.net/"
       authority_url = ("https://login.microsoftonline.com/"+tenant_id)
       context = adal.AuthenticationContext(authority_url)
       return azure_active_directory.AdalAuthentication(
       lambda: context.acquire_token_with_client_certificate(
               resource,
               application_id,
               pem_pkey,
               thumbprint)
       )

   # Authenticate to Azure using the Azure Automation RunAs service principal
   runas_connection = automationassets.get_automation_connection("AzureRunAsConnection")
   azure_credential = get_automation_runas_credential(runas_connection)
   ```

## <a name="add-code-to-create-python-compute-client-and-start-the-vm"></a><span data-ttu-id="a847b-179">Add code to create Python Compute client and start the VM</span><span class="sxs-lookup"><span data-stu-id="a847b-179">Add code to create Python Compute client and start the VM</span></span>

<span data-ttu-id="a847b-180">To work with Azure VMs, create an instance of the [Azure Compute client for Python](https://docs.microsoft.com/python/api/azure.mgmt.compute.computemanagementclient?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="a847b-180">To work with Azure VMs, create an instance of the [Azure Compute client for Python](https://docs.microsoft.com/python/api/azure.mgmt.compute.computemanagementclient?view=azure-python).</span></span>

<span data-ttu-id="a847b-181">Use the Compute client to start the VM.</span><span class="sxs-lookup"><span data-stu-id="a847b-181">Use the Compute client to start the VM.</span></span> <span data-ttu-id="a847b-182">Add the following code to the runbook:</span><span class="sxs-lookup"><span data-stu-id="a847b-182">Add the following code to the runbook:</span></span>

```python
# Initialize the compute management client with the RunAs credential and specify the subscription to work against.
compute_client = ComputeManagementClient(
azure_credential,
  str(runas_connection["SubscriptionId"])
)


print('\nStart VM')
async_vm_start = compute_client.virtual_machines.start("MyResourceGroup", "TestVM")
async_vm_start.wait()
```

<span data-ttu-id="a847b-183">Where _MyResourceGroup_ is the name of the resource group that contains the VM, and _TestVM_ is the name of the VM you want to start.</span><span class="sxs-lookup"><span data-stu-id="a847b-183">Where _MyResourceGroup_ is the name of the resource group that contains the VM, and _TestVM_ is the name of the VM you want to start.</span></span> 

<span data-ttu-id="a847b-184">Test and run the runbook again to see that it starts the VM.</span><span class="sxs-lookup"><span data-stu-id="a847b-184">Test and run the runbook again to see that it starts the VM.</span></span>

## <a name="use-input-parameters"></a><span data-ttu-id="a847b-185">Use input parameters</span><span class="sxs-lookup"><span data-stu-id="a847b-185">Use input parameters</span></span>

<span data-ttu-id="a847b-186">The runbook currently uses hard-coded values for the names of the Resource Group and the VM.</span><span class="sxs-lookup"><span data-stu-id="a847b-186">The runbook currently uses hard-coded values for the names of the Resource Group and the VM.</span></span>
<span data-ttu-id="a847b-187">Now let's add code that gets these values from input parameters.</span><span class="sxs-lookup"><span data-stu-id="a847b-187">Now let's add code that gets these values from input parameters.</span></span>

<span data-ttu-id="a847b-188">You use the `sys.argv` variable to get the parameter values.</span><span class="sxs-lookup"><span data-stu-id="a847b-188">You use the `sys.argv` variable to get the parameter values.</span></span>
<span data-ttu-id="a847b-189">Add the following code to the runbook immediately after the other `import` statements:</span><span class="sxs-lookup"><span data-stu-id="a847b-189">Add the following code to the runbook immediately after the other `import` statements:</span></span>

```python
import sys

resource_group_name = str(sys.argv[1])
vm_name = str(sys.argv[2])
```

<span data-ttu-id="a847b-190">This imports the `sys` module, and creates two variables to hold the Resource Group and VM names.</span><span class="sxs-lookup"><span data-stu-id="a847b-190">This imports the `sys` module, and creates two variables to hold the Resource Group and VM names.</span></span>
<span data-ttu-id="a847b-191">Notice that the element of the argument list, `sys.argv[0]`, is the name of the script, and is not input by the user.</span><span class="sxs-lookup"><span data-stu-id="a847b-191">Notice that the element of the argument list, `sys.argv[0]`, is the name of the script, and is not input by the user.</span></span>

<span data-ttu-id="a847b-192">Now you can modify the last two lines of the runbook to use the input parameter values instead of using hard-coded values:</span><span class="sxs-lookup"><span data-stu-id="a847b-192">Now you can modify the last two lines of the runbook to use the input parameter values instead of using hard-coded values:</span></span>

```python
async_vm_start = compute_client.virtual_machines.start(resource_group_name, vm_name)
async_vm_start.wait()
```

<span data-ttu-id="a847b-193">When you start a Python runbook (either on the **Test** page or as a published runbook), you can enter the values for parameters in the **Start Runbook** page under **Parameters**.</span><span class="sxs-lookup"><span data-stu-id="a847b-193">When you start a Python runbook (either on the **Test** page or as a published runbook), you can enter the values for parameters in the **Start Runbook** page under **Parameters**.</span></span>

<span data-ttu-id="a847b-194">After you start entering a value in the first box, a second will appear, and so on, so that you can enter as many parameter values as necessary.</span><span class="sxs-lookup"><span data-stu-id="a847b-194">After you start entering a value in the first box, a second will appear, and so on, so that you can enter as many parameter values as necessary.</span></span>

<span data-ttu-id="a847b-195">The values are available to the script as the `sys.argv` array as in the code you just added.</span><span class="sxs-lookup"><span data-stu-id="a847b-195">The values are available to the script as the `sys.argv` array as in the code you just added.</span></span>

<span data-ttu-id="a847b-196">Enter the name of your resource group as the value for the first parameter, and the name of the VM to start as the value of the second parameter.</span><span class="sxs-lookup"><span data-stu-id="a847b-196">Enter the name of your resource group as the value for the first parameter, and the name of the VM to start as the value of the second parameter.</span></span>

![Enter parameter values](media/automation-first-runbook-textual-python/runbook-python-params.png)

<span data-ttu-id="a847b-198">Click **OK** to start the runbook.</span><span class="sxs-lookup"><span data-stu-id="a847b-198">Click **OK** to start the runbook.</span></span> <span data-ttu-id="a847b-199">The runbook runs and starts the VM that you specified.</span><span class="sxs-lookup"><span data-stu-id="a847b-199">The runbook runs and starts the VM that you specified.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a847b-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="a847b-200">Next steps</span></span>

- <span data-ttu-id="a847b-201">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a847b-201">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md)</span></span>
- <span data-ttu-id="a847b-202">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="a847b-202">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
- <span data-ttu-id="a847b-203">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="a847b-203">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
- <span data-ttu-id="a847b-204">To know more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="a847b-204">To know more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>
- <span data-ttu-id="a847b-205">To learn about developing for Azure with Python, see [Azure for Python developers](https://docs.microsoft.com/python/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="a847b-205">To learn about developing for Azure with Python, see [Azure for Python developers](https://docs.microsoft.com/python/azure/?view=azure-python)</span></span>
- <span data-ttu-id="a847b-206">To view sample Python 2 runbooks, see the [Azure Automation GitHub](https://github.com/azureautomation/runbooks/tree/master/Utility/Python)</span><span class="sxs-lookup"><span data-stu-id="a847b-206">To view sample Python 2 runbooks, see the [Azure Automation GitHub](https://github.com/azureautomation/runbooks/tree/master/Utility/Python)</span></span>