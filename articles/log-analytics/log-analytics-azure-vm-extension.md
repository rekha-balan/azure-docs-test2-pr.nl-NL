---
title: Connect Azure virtual machines to Log Analytics  | Microsoft Docs
description: For Windows and Linux virtual machines running in Azure, the recommended way of collected logs and metrics is by installing the Log Analytics Azure VM extension. You can use the Azure portal or PowerShell to install the Log Analytics virtual machine extension onto Azure VMs.
services: log-analytics
documentationcenter: ''
author: richrundmsft
manager: jochan
editor: ''
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a258fdfb7d9b318432e9296ef999bfc497126fd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552505"
---
# <a name="connect-azure-virtual-machines-to-log-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="d881f-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span><span class="sxs-lookup"><span data-stu-id="d881f-104">Connect Azure virtual machines to Log Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="d881f-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span><span class="sxs-lookup"><span data-stu-id="d881f-105">For Windows and Linux computers, the recommended method for collecting logs and metrics is by installing the Log Analytics agent.</span></span>

<span data-ttu-id="d881f-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span><span class="sxs-lookup"><span data-stu-id="d881f-106">The easiest way to install the Log Analytics agent on Azure virtual machines is through the Log Analytics VM Extension.</span></span>  <span data-ttu-id="d881f-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span><span class="sxs-lookup"><span data-stu-id="d881f-107">Using the extension simplifies the installation process and automatically configures the agent to send data to the Log Analytics workspace that you specify.</span></span> <span data-ttu-id="d881f-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span><span class="sxs-lookup"><span data-stu-id="d881f-108">The agent is also upgraded automatically, ensuring that you have the latest features and fixes.</span></span>

<span data-ttu-id="d881f-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span><span class="sxs-lookup"><span data-stu-id="d881f-109">For Windows virtual machines, you enable the *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="d881f-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span><span class="sxs-lookup"><span data-stu-id="d881f-110">For Linux virtual machines, you enable the *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="d881f-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d881f-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and the [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d881f-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span><span class="sxs-lookup"><span data-stu-id="d881f-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics that you want to collect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d881f-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span><span class="sxs-lookup"><span data-stu-id="d881f-113">If you configure Log Analytics to index log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure the agent to collect the same logs, then the logs are collected twice.</span></span> <span data-ttu-id="d881f-114">You are charged for both data sources.</span><span class="sxs-lookup"><span data-stu-id="d881f-114">You are charged for both data sources.</span></span> <span data-ttu-id="d881f-115">If you have the agent installed, then you should collect log data by using the agent alone - don't configure Log Analytics to collect log data from Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="d881f-115">If you have the agent installed, then you should collect log data by using the agent alone - don't configure Log Analytics to collect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="d881f-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span><span class="sxs-lookup"><span data-stu-id="d881f-116">There are three easy ways to enable the Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="d881f-117">By using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d881f-117">By using the Azure portal</span></span>
* <span data-ttu-id="d881f-118">By using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d881f-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="d881f-119">By using an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="d881f-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-the-vm-extension-in-the-azure-portal"></a><span data-ttu-id="d881f-120">Enable the VM extension in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d881f-120">Enable the VM extension in the Azure portal</span></span>
<span data-ttu-id="d881f-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d881f-121">You can install the agent for Log Analytics and connect the Azure virtual machine that it runs on by using the [Azure portal](https://portal.azure.com).</span></span>

### <a name="to-install-the-log-analytics-agent-and-connect-the-virtual-machine-to-a-log-analytics-workspace"></a><span data-ttu-id="d881f-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="d881f-122">To install the Log Analytics agent and connect the virtual machine to a Log Analytics workspace</span></span>
1. <span data-ttu-id="d881f-123">Sign into the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d881f-123">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d881f-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span><span class="sxs-lookup"><span data-stu-id="d881f-124">Select **Browse** on the left side of the portal, and then go to **Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="d881f-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span><span class="sxs-lookup"><span data-stu-id="d881f-125">In your list of Log Analytics workspaces, select the one that you want to use with the Azure VM.</span></span>  
   ![OMS workspaces](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="d881f-127">Under **Log analytics management**, select **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="d881f-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="d881f-128">![Virtual machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="d881f-128">![Virtual machines](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="d881f-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span><span class="sxs-lookup"><span data-stu-id="d881f-129">In the list of **Virtual machines**, select the virtual machine on which you want to install the agent.</span></span> <span data-ttu-id="d881f-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span><span class="sxs-lookup"><span data-stu-id="d881f-130">The **OMS connection status** for the VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="d881f-131">![VM not connected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="d881f-131">![VM not connected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="d881f-132">In the details for your virtual machine, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="d881f-132">In the details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="d881f-133">The agent is automatically installed and configured for your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="d881f-133">The agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="d881f-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span><span class="sxs-lookup"><span data-stu-id="d881f-134">This process takes a few minutes, during which time the OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="d881f-135">![Connect VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="d881f-135">![Connect VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="d881f-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span><span class="sxs-lookup"><span data-stu-id="d881f-136">After you install and connect the agent, the **OMS connection** status will be updated to show **This workspace**.</span></span>  
   <span data-ttu-id="d881f-137">![Connected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="d881f-137">![Connected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-the-vm-extension-using-powershell"></a><span data-ttu-id="d881f-138">Enable the VM extension using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d881f-138">Enable the VM extension using PowerShell</span></span>
<span data-ttu-id="d881f-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="d881f-139">When you configure your virtual machine by using PowerShell, you need to provide the **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="d881f-140">Note that the property names in your json configuration are **case-sensitive**.</span><span class="sxs-lookup"><span data-stu-id="d881f-140">Note that the property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="d881f-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="d881f-141">You can find the Id and key on the **Settings** page of the OMS portal, or by using PowerShell as shown in the preceding example.</span></span>

![Workspace ID and primary key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="d881f-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d881f-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="d881f-144">Following are examples for both classic and Resource Manager virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d881f-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="d881f-145">For classic virtual machines, use the following PowerShell example:</span><span class="sxs-lookup"><span data-stu-id="d881f-145">For classic virtual machines, use the following PowerShell example:</span></span>

```
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment the following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="d881f-146">For Resource Manager virtual machines, use the following PowerShell example:</span><span class="sxs-lookup"><span data-stu-id="d881f-146">For Resource Manager virtual machines, use the following PowerShell example:</span></span>

```
Login-AzureRMAccount
Select-AzureSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable to find OMS Workspace $workspaceName. Do you need to run Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment the following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```

## <a name="deploy-the-vm-extension-using-a-template"></a><span data-ttu-id="d881f-147">Deploy the VM extension using a template</span><span class="sxs-lookup"><span data-stu-id="d881f-147">Deploy the VM extension using a template</span></span>
<span data-ttu-id="d881f-148">By using Azure Resource Manager, you can create a simple template (in JSON format) that defines the deployment and configuration of your application.</span><span class="sxs-lookup"><span data-stu-id="d881f-148">By using Azure Resource Manager, you can create a simple template (in JSON format) that defines the deployment and configuration of your application.</span></span> <span data-ttu-id="d881f-149">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span><span class="sxs-lookup"><span data-stu-id="d881f-149">This template is known as a Resource Manager template and provides a declarative way to define deployment.</span></span> <span data-ttu-id="d881f-150">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span><span class="sxs-lookup"><span data-stu-id="d881f-150">By using a template, you can repeatedly deploy your application throughout the app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="d881f-151">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="d881f-151">By including the Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured to report to your Log Analytics workspace.</span></span>

<span data-ttu-id="d881f-152">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d881f-152">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="d881f-153">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span><span class="sxs-lookup"><span data-stu-id="d881f-153">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with the Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="d881f-154">This template is a typical virtual machine template, with the following additions:</span><span class="sxs-lookup"><span data-stu-id="d881f-154">This template is a typical virtual machine template, with the following additions:</span></span>

* <span data-ttu-id="d881f-155">workspaceId and workspaceName parameters</span><span class="sxs-lookup"><span data-stu-id="d881f-155">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="d881f-156">Microsoft.EnterpriseCloud.Monitoring resource extension section</span><span class="sxs-lookup"><span data-stu-id="d881f-156">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="d881f-157">Outputs to look up the workspaceId and workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="d881f-157">Outputs to look up the workspaceId and workspaceSharedKey</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for the Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for the Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for the Public IP. Must be lowercase. It should match with the following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "The Windows version for the VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="d881f-158">You can deploy a template by using the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="d881f-158">You can deploy a template by using the following PowerShell command:</span></span>

```
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-the-log-analytics-vm-extension"></a><span data-ttu-id="d881f-159">Troubleshooting the Log Analytics VM extension</span><span class="sxs-lookup"><span data-stu-id="d881f-159">Troubleshooting the Log Analytics VM extension</span></span>
<span data-ttu-id="d881f-160">Usually you will receive a message when things don't work, from either Azure portal or Azure powershell.</span><span class="sxs-lookup"><span data-stu-id="d881f-160">Usually you will receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="d881f-161">Sign into the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d881f-161">Sign into the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d881f-162">Find the VM and open VM details.</span><span class="sxs-lookup"><span data-stu-id="d881f-162">Find the VM and open VM details.</span></span>
3. <span data-ttu-id="d881f-163">Click on **Extensions** to check if OMS extension is enabled or not.</span><span class="sxs-lookup"><span data-stu-id="d881f-163">Click on **Extensions** to check if OMS extension is enabled or not.</span></span>

   ![VM Extension View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="d881f-165">Click on the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span><span class="sxs-lookup"><span data-stu-id="d881f-165">Click on the *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![VM Extension Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="d881f-167">Troubleshooting Windows Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="d881f-167">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="d881f-168">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting you can perform the following steps to troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="d881f-168">If the *Microsoft Monitoring Agent* VM agent extension is not installing or reporting you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="d881f-169">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="d881f-169">Check if the Azure VM agent is installed and working correctly by using the steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="d881f-170">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="d881f-170">You can also review the VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="d881f-171">If the log does not exist, the VM agent is not installed.</span><span class="sxs-lookup"><span data-stu-id="d881f-171">If the log does not exist, the VM agent is not installed.</span></span>
     * [<span data-ttu-id="d881f-172">Install the Azure VM Agent on classic VMs</span><span class="sxs-lookup"><span data-stu-id="d881f-172">Install the Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="d881f-173">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span><span class="sxs-lookup"><span data-stu-id="d881f-173">Confirm the Microsoft Monitoring Agent extension heartbeat task is running using the following steps:</span></span>
   * <span data-ttu-id="d881f-174">Log in to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="d881f-174">Log in to the virtual machine</span></span>
   * <span data-ttu-id="d881f-175">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span><span class="sxs-lookup"><span data-stu-id="d881f-175">Open task scheduler and find the `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="d881f-176">Confirm the task is enabled and is running every one minute</span><span class="sxs-lookup"><span data-stu-id="d881f-176">Confirm the task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="d881f-177">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="d881f-177">Check the heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="d881f-178">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="d881f-178">Review the Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="d881f-179">Ensure the virtual machine can run PowerShell scripts</span><span class="sxs-lookup"><span data-stu-id="d881f-179">Ensure the virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="d881f-180">Ensure permissions on C:\Windows\temp haven’t been changed</span><span class="sxs-lookup"><span data-stu-id="d881f-180">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="d881f-181">View the status of the Microsoft Monitoring Agent by typing the following in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="d881f-181">View the status of the Microsoft Monitoring Agent by typing the following in an elevated PowerShell window on the virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="d881f-182">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="d881f-182">Review the Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="d881f-183">For more information, refer to [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d881f-183">For more information, refer to [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="d881f-184">Troubleshooting Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="d881f-184">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="d881f-185">If the *OMS Agent for Linux* VM agent extension is not installing or reporting you can perform the following steps to troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="d881f-185">If the *OMS Agent for Linux* VM agent extension is not installing or reporting you can perform the following steps to troubleshoot the issue.</span></span>

1. <span data-ttu-id="d881f-186">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="d881f-186">If the extension status is *Unknown* check if the Azure VM agent is installed and working correctly by reviewing the VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="d881f-187">If the log does not exist, the VM agent is not installed.</span><span class="sxs-lookup"><span data-stu-id="d881f-187">If the log does not exist, the VM agent is not installed.</span></span>
   * [<span data-ttu-id="d881f-188">Install the Azure VM Agent on Linux VMs</span><span class="sxs-lookup"><span data-stu-id="d881f-188">Install the Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="d881f-189">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="d881f-189">For other unhealthy statuses, review the OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="d881f-190">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="d881f-190">If the extension status is healthy, but data is not being uploaded review the OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

<span data-ttu-id="d881f-191">For more information, refer to [troubleshooting Linux extensions](../virtual-machines/linux/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d881f-191">For more information, refer to [troubleshooting Linux extensions](../virtual-machines/linux/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d881f-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="d881f-192">Next steps</span></span>
* <span data-ttu-id="d881f-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span><span class="sxs-lookup"><span data-stu-id="d881f-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) to specify the logs and metrics to collect.</span></span>
* <span data-ttu-id="d881f-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d881f-194">To gather data from virtual machines [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="d881f-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span><span class="sxs-lookup"><span data-stu-id="d881f-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="d881f-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span><span class="sxs-lookup"><span data-stu-id="d881f-196">For computers that are not in Azure, you can install the Log Analytics agent by using the methods that are described in the following articles:</span></span>

* [<span data-ttu-id="d881f-197">Connect Windows computers to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d881f-197">Connect Windows computers to Log Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="d881f-198">Connect Linux computers to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="d881f-198">Connect Linux computers to Log Analytics</span></span>](log-analytics-linux-agents.md)








