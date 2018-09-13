---
title: Update resources in Azure managed applications | Microsoft Docs
description: Describes how to work on resources in the managed resource group for an Azure managed application.
services: managed-applications
author: tfitzmac
manager: timlt
ms.service: managed-applications
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.date: 10/26/2017
ms.author: tomfitz
ms.openlocfilehash: 7c2b38055771dae458e4a3a56c2c98231335ae03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869873"
---
# <a name="work-with-resources-in-the-managed-resource-group-for-azure-managed-application"></a><span data-ttu-id="61812-103">Work with resources in the managed resource group for Azure managed application</span><span class="sxs-lookup"><span data-stu-id="61812-103">Work with resources in the managed resource group for Azure managed application</span></span>

<span data-ttu-id="61812-104">This article describes how to update resources that are deployed as part of a managed application.</span><span class="sxs-lookup"><span data-stu-id="61812-104">This article describes how to update resources that are deployed as part of a managed application.</span></span> <span data-ttu-id="61812-105">As the publisher of a managed application, you have access to the resources in the managed resource group.</span><span class="sxs-lookup"><span data-stu-id="61812-105">As the publisher of a managed application, you have access to the resources in the managed resource group.</span></span> <span data-ttu-id="61812-106">To update these resources, you need to find the managed resource group associated with a managed application, and access the resource in that resource group.</span><span class="sxs-lookup"><span data-stu-id="61812-106">To update these resources, you need to find the managed resource group associated with a managed application, and access the resource in that resource group.</span></span>

<span data-ttu-id="61812-107">This article assumes you have deployed the managed application in the [Managed Web Application (IaaS) with Azure management services](https://github.com/Azure/azure-managedapp-samples/tree/master/samples/201-managed-web-app) sample project.</span><span class="sxs-lookup"><span data-stu-id="61812-107">This article assumes you have deployed the managed application in the [Managed Web Application (IaaS) with Azure management services](https://github.com/Azure/azure-managedapp-samples/tree/master/samples/201-managed-web-app) sample project.</span></span> <span data-ttu-id="61812-108">That managed application includes a **Standard_D1_v2** virtual machine.</span><span class="sxs-lookup"><span data-stu-id="61812-108">That managed application includes a **Standard_D1_v2** virtual machine.</span></span> <span data-ttu-id="61812-109">If you have not deployed that managed application, you can still use this article to become familiar with the steps for updating a managed resource group.</span><span class="sxs-lookup"><span data-stu-id="61812-109">If you have not deployed that managed application, you can still use this article to become familiar with the steps for updating a managed resource group.</span></span>

<span data-ttu-id="61812-110">The following image shows the deployed managed application.</span><span class="sxs-lookup"><span data-stu-id="61812-110">The following image shows the deployed managed application.</span></span>

![Deployed managed application](./media/update-managed-resources/deployed.png)

<span data-ttu-id="61812-112">In this article, you use Azure CLI to:</span><span class="sxs-lookup"><span data-stu-id="61812-112">In this article, you use Azure CLI to:</span></span>

* <span data-ttu-id="61812-113">Identify the managed application</span><span class="sxs-lookup"><span data-stu-id="61812-113">Identify the managed application</span></span>
* <span data-ttu-id="61812-114">Identify the managed resource group</span><span class="sxs-lookup"><span data-stu-id="61812-114">Identify the managed resource group</span></span>
* <span data-ttu-id="61812-115">Identify the virtual machine resource(s) in the managed resource group</span><span class="sxs-lookup"><span data-stu-id="61812-115">Identify the virtual machine resource(s) in the managed resource group</span></span>
* <span data-ttu-id="61812-116">Change the VM size (either to a smaller size if not utilized, or a larger to support more load)</span><span class="sxs-lookup"><span data-stu-id="61812-116">Change the VM size (either to a smaller size if not utilized, or a larger to support more load)</span></span>
* <span data-ttu-id="61812-117">Assign a policy to the managed resource group that specifies the allowed locations</span><span class="sxs-lookup"><span data-stu-id="61812-117">Assign a policy to the managed resource group that specifies the allowed locations</span></span>

## <a name="get-managed-application-and-managed-resource-group"></a><span data-ttu-id="61812-118">Get managed application and managed resource group</span><span class="sxs-lookup"><span data-stu-id="61812-118">Get managed application and managed resource group</span></span>

<span data-ttu-id="61812-119">To get the managed applications in a resource group, use:</span><span class="sxs-lookup"><span data-stu-id="61812-119">To get the managed applications in a resource group, use:</span></span>

```azurecli-interactive
az managedapp list --query "[?contains(resourceGroup,'DemoApp')]"
```

<span data-ttu-id="61812-120">To get the ID of the managed resource group, use:</span><span class="sxs-lookup"><span data-stu-id="61812-120">To get the ID of the managed resource group, use:</span></span>

```azurecli-interactive
az managedapp list --query "[?contains(resourceGroup,'DemoApp')].{ managedResourceGroup:managedResourceGroupId }"
```

## <a name="resize-vms-in-managed-resource-group"></a><span data-ttu-id="61812-121">Resize VMs in managed resource group</span><span class="sxs-lookup"><span data-stu-id="61812-121">Resize VMs in managed resource group</span></span>

<span data-ttu-id="61812-122">To see the virtual machines in the managed resource group, provide the name of the managed resource group.</span><span class="sxs-lookup"><span data-stu-id="61812-122">To see the virtual machines in the managed resource group, provide the name of the managed resource group.</span></span>

```azurecli-interactive
az vm list -g DemoApp6zkevchqk7sfq --query "[].{VMName:name,OSType:storageProfile.osDisk.osType,VMSize:hardwareProfile.vmSize}"
```

<span data-ttu-id="61812-123">To update the size of the VMs, use:</span><span class="sxs-lookup"><span data-stu-id="61812-123">To update the size of the VMs, use:</span></span>

```azurecli-interactive
az vm resize --size Standard_D2_v2 --ids $(az vm list -g DemoApp6zkevchqk7sfq --query "[].id" -o tsv)
```

<span data-ttu-id="61812-124">After the operation completes, verify the application is running on Standard D2 v2.</span><span class="sxs-lookup"><span data-stu-id="61812-124">After the operation completes, verify the application is running on Standard D2 v2.</span></span>

![Managed application using Standard D2 v2](./media/update-managed-resources/upgraded.png)

## <a name="apply-policy-to-managed-resource-group"></a><span data-ttu-id="61812-126">Apply policy to managed resource group</span><span class="sxs-lookup"><span data-stu-id="61812-126">Apply policy to managed resource group</span></span>

<span data-ttu-id="61812-127">Get the managed resource group and assignment a policy at that scope.</span><span class="sxs-lookup"><span data-stu-id="61812-127">Get the managed resource group and assignment a policy at that scope.</span></span> <span data-ttu-id="61812-128">The policy **e56962a6-4747-49cd-b67b-bf8b01975c4c** is a built-in policy for specifying allowed locations.</span><span class="sxs-lookup"><span data-stu-id="61812-128">The policy **e56962a6-4747-49cd-b67b-bf8b01975c4c** is a built-in policy for specifying allowed locations.</span></span>

```azurecli-interactive
managedGroup=$(az managedapp show --name <app-name> --resource-group DemoApp --query managedResourceGroupId --output tsv)

az policy assignment create --name locationAssignment --policy e56962a6-4747-49cd-b67b-bf8b01975c4c --scope $managedGroup --params '{
                            "listofallowedLocations": {
                                "value": [
                                    "northeurope",
                                    "westeurope"
                                ]
                            }
                        }'
```

<span data-ttu-id="61812-129">To see the allowed locations, use:</span><span class="sxs-lookup"><span data-stu-id="61812-129">To see the allowed locations, use:</span></span>

```azurecli-interactive
az policy assignment show --name locationAssignment --scope $managedGroup --query parameters.listofallowedLocations.value
```

<span data-ttu-id="61812-130">The policy assignment appears in the portal.</span><span class="sxs-lookup"><span data-stu-id="61812-130">The policy assignment appears in the portal.</span></span>

![View policy assignment](./media/update-managed-resources/assignment.png)

## <a name="next-steps"></a><span data-ttu-id="61812-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="61812-132">Next steps</span></span>

* <span data-ttu-id="61812-133">For an introduction to managed applications, see [Managed application overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="61812-133">For an introduction to managed applications, see [Managed application overview](overview.md).</span></span>
* <span data-ttu-id="61812-134">For sample projects, see [Sample projects for Azure managed applications](sample-projects.md).</span><span class="sxs-lookup"><span data-stu-id="61812-134">For sample projects, see [Sample projects for Azure managed applications](sample-projects.md).</span></span>
