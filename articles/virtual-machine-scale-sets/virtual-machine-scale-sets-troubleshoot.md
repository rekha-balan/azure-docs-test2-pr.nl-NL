---
title: Troubleshoot autoscale with Virtual Machine Scale Sets | Microsoft Docs
description: Troubleshoot autoscale with Virtual Machine Scale Sets. Understand typical problems encountered and how to resolve them.
services: virtual-machine-scale-sets
documentationcenter: ''
author: gbowerman
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: fd3e74b4816305c9cb993666a00c526262defbd3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549229"
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Troubleshooting autoscale with Virtual Machine Scale Sets
**Problem** – you’ve created an autoscaling infrastructure in Azure Resource Manager using VM Scale Sets –  for example by deploying a template like this: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale  – you have your scale rules defined and it works great, except that no matter how much load you put on the VMs, it won’t autoscale.

## <a name="troubleshooting-steps"></a>Troubleshooting steps
Some things to consider include:

* How many cores does each VM have, and are you loading each core?
  The example Azure Quickstart template above has a do_work.php script, which loads a single core. If you’re using a VM bigger than a single core VM size like Standard_A1 or D1 then you’d need to run this load multiple times. Check how many cores your VMs by reviewing [Sizes for Windows virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* How many VMs in the VM Scale Set, are you doing work on each one?
  
    A scale out event will only take place when the average CPU across **all** the VMs in a scale set exceeds the threshold value, over the time internal defined in the autoscale rules.
* Did you miss any scale events?
  
    Check the audit logs in the Azure portal for scale events. Maybe there was a scale up and a scale down which was missed. You can filter by “Scale”..
  
    ![Audit Logs][audit]
* Are your scale-in and scale-out thresholds sufficiently different?
  
    Suppose you set a rule to scale out when average CPU is greater than 50% over 5 minutes, and to scale in when average CPU is less than 50%. This would cause a “flapping” problem when CPU usage is close to this threshold, with scale actions constantly increasing and decreasing the size of the set. Because of this, the autoscale service tries to prevent “flapping”, which can manifest as not scaling. Therefore make sure your scale-out and scale-in thresholds are sufficiently different to allow some space in between scaling.
* Did you write your own JSON template?
  
    It is easy to make mistakes, so start with a template like the one above which is proven to work, and make small incremental changes. 
* Can you manually scale in or out?
  
    Try redeploying the VM Scale Set resource with a different “capacity” setting to change the number of VMs manually. An example template to do this is here: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – you may need to edit the template to make sure it has the same machine size as your Scale Set is using. If you can successfully change the number of VMs manually, then you know the problem is isolated to autoscale.
* Check your Microsoft.Compute/virtualMachineScaleSet, and Microsoft.Insights resources in the [Azure Resource Explorer](https://resources.azure.com/)
  
    This is an indispensable troubleshooting tool which shows you the state of your Azure Resource Manager resources. Click on your subscription and look at the Resource Group you are troubleshooting. Under the Compute resource provider look at the VM Scale Set you created and check the Instance View, which shows you the state of a deployment. Also check the instance view of VMs in the VM Scale Set. Then go into the Microsoft.Insights resource provider and check the autoscale rules look good.
* Is the Diagnostic extension working and emitting performance data?
  
    **Update:** Azure autoscale has been enhanced to use a host based metrics pipeline which no longer requires a diagnostics extension to be installed. This means the next few paragraphs no longer apply if you create an autoscaling application using the new pipeline. An example of Azure templates which have been converted to use the host pipeline is: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    Using host based metrics for autoscale is better for the following reasons:
  
  * Fewer moving parts as no diagnostics extensions need to be installed.
  * Simpler templates. Just add insights autoscale rules to an existing scale set template.
  * More reliable reporting and faster launching of new VMs.
    
    The only reasons you might want to keep using a diagnostic extension would be if you need memory diagnostics reporting/scaling. Host based metrics doesn't report memory.
    
    With that in mind, only follow the rest of this article if you are still using diagnostic extensions for your autoscaling.
    
    Autoscale in Azure Resource Manager can work (but no longer has to) by means of a VM extension called the Diagnostics Extension. It emits performance data to a storage account you define in the template. This data is then aggregated by the Azure Monitor service.
    
    If the Insights service can’t read data from the VMs, it is supposed to send you an email – for example if the VMs were down, so check your email (the one you specified when creating the Azure account).
    
    You can also go and look at the data yourself. Look at the Azure storage account using a cloud explorer. For example using the [Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), log in and pick the Azure subscription you’re using, and the Diagnostics storage account name referenced in the Diagnostics extension definition in your deployment template..
    
    ![Cloud Explorer][explorer]
    
    Here you will see a bunch of tables where the data from each VM is being stored. Taking Linux and the CPU metric as an example, look at the most recent rows. The Visual Studio cloud explorer supports a query language so you can run a query like “Timestamp gt datetime’2016-02-02T21:20:00Z’” to make sure you get the most recent events (assume time is in UTC). Does the data you see in there correspond to the scale rules you set up? In the example below, the CPU for machine 20 started increasing to 100% over the last 5 minutes..
    
    ![Storage Tables][tables]
    
    If the data is not there, then it implies the problem is with the diagnostic extension running in the VMs. If the data is there, it implies there is either a problem with your scale rules, or with the Insights service. Check [Azure Status](https://azure.microsoft.com/status/).
    
    Once you’ve been through these steps, if you are still having autoscale problems you could try the forums on [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), or [Stack overflow](http://stackoverflow.com/questions/tagged/azure), or log a support call. Be prepared to share the template and a view of the performance data.

[audit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-troubleshoot/image4.png



