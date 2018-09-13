---
title: Deploy with Terraform from Bash in Azure Cloud Shell | Microsoft Docs
description: Deploy with Terraform from Bash in Azure Cloud Shell
services: Azure
documentationcenter: ''
author: tomarcher
manager: routlaw
tags: azure-cloud-shell
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: tarcher
ms.openlocfilehash: c9e0a5a40d1c354de0873a57b4d42e74dbb5727e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869482"
---
# <a name="deploy-with-terraform-from-bash-in-azure-cloud-shell"></a><span data-ttu-id="71db8-103">Deploy with Terraform from Bash in Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="71db8-103">Deploy with Terraform from Bash in Azure Cloud Shell</span></span>
<span data-ttu-id="71db8-104">This article walks you through creating a resource group with the [Terraform AzureRM provider](https://www.terraform.io/docs/providers/azurerm/index.html).</span><span class="sxs-lookup"><span data-stu-id="71db8-104">This article walks you through creating a resource group with the [Terraform AzureRM provider](https://www.terraform.io/docs/providers/azurerm/index.html).</span></span> 

<span data-ttu-id="71db8-105">[Hashicorp Terraform](https://www.terraform.io/) is an open source tool that codifies APIs into declarative configuration files that can be shared amongst team members to be edited, reviewed, and versioned.</span><span class="sxs-lookup"><span data-stu-id="71db8-105">[Hashicorp Terraform](https://www.terraform.io/) is an open source tool that codifies APIs into declarative configuration files that can be shared amongst team members to be edited, reviewed, and versioned.</span></span> <span data-ttu-id="71db8-106">The Microsoft AzureRM provider is used to interact with resources supported by Azure Resource Manager via the AzureRM APIs.</span><span class="sxs-lookup"><span data-stu-id="71db8-106">The Microsoft AzureRM provider is used to interact with resources supported by Azure Resource Manager via the AzureRM APIs.</span></span> 

## <a name="automatic-authentication"></a><span data-ttu-id="71db8-107">Automatic authentication</span><span class="sxs-lookup"><span data-stu-id="71db8-107">Automatic authentication</span></span>
<span data-ttu-id="71db8-108">Terraform is installed in Bash in Cloud Shell by default.</span><span class="sxs-lookup"><span data-stu-id="71db8-108">Terraform is installed in Bash in Cloud Shell by default.</span></span> <span data-ttu-id="71db8-109">Additionally, Cloud Shell automatically authenticates your default Azure CLI 2.0 subscription to deploy resources through the Terraform Azure modules.</span><span class="sxs-lookup"><span data-stu-id="71db8-109">Additionally, Cloud Shell automatically authenticates your default Azure CLI 2.0 subscription to deploy resources through the Terraform Azure modules.</span></span>

<span data-ttu-id="71db8-110">Terraform uses the default Azure CLI 2.0 subscription that is set.</span><span class="sxs-lookup"><span data-stu-id="71db8-110">Terraform uses the default Azure CLI 2.0 subscription that is set.</span></span> <span data-ttu-id="71db8-111">To update default subscriptions, run:</span><span class="sxs-lookup"><span data-stu-id="71db8-111">To update default subscriptions, run:</span></span>

```azurecli-interactive
az account set --subscription mySubscriptionName
```

## <a name="walkthrough"></a><span data-ttu-id="71db8-112">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="71db8-112">Walkthrough</span></span>
### <a name="launch-bash-in-cloud-shell"></a><span data-ttu-id="71db8-113">Launch Bash in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="71db8-113">Launch Bash in Cloud Shell</span></span>
1. <span data-ttu-id="71db8-114">Launch Cloud Shell from your preferred location</span><span class="sxs-lookup"><span data-stu-id="71db8-114">Launch Cloud Shell from your preferred location</span></span>
2. <span data-ttu-id="71db8-115">Verify your preferred subscription is set</span><span class="sxs-lookup"><span data-stu-id="71db8-115">Verify your preferred subscription is set</span></span>

```azurecli-interactive
az account show
```

### <a name="create-a-terraform-template"></a><span data-ttu-id="71db8-116">Create a Terraform template</span><span class="sxs-lookup"><span data-stu-id="71db8-116">Create a Terraform template</span></span>
<span data-ttu-id="71db8-117">Create a new Terraform template named main.tf with your preferred text editor.</span><span class="sxs-lookup"><span data-stu-id="71db8-117">Create a new Terraform template named main.tf with your preferred text editor.</span></span>

```
vim main.tf
```

<span data-ttu-id="71db8-118">Copy/paste the following code into Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="71db8-118">Copy/paste the following code into Cloud Shell.</span></span>

```
resource "azurerm_resource_group" "myterraformgroup" {
    name = "myRgName"
    location = "West US"
}
```

<span data-ttu-id="71db8-119">Save your file and exit your text editor.</span><span class="sxs-lookup"><span data-stu-id="71db8-119">Save your file and exit your text editor.</span></span>

### <a name="terraform-init"></a><span data-ttu-id="71db8-120">Terraform init</span><span class="sxs-lookup"><span data-stu-id="71db8-120">Terraform init</span></span>
<span data-ttu-id="71db8-121">Begin by running `terraform init`.</span><span class="sxs-lookup"><span data-stu-id="71db8-121">Begin by running `terraform init`.</span></span>

```
justin@Azure:~$ terraform init

Initializing provider plugins...

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking
changes, it is recommended to add version = "..." constraints to the
corresponding provider blocks in configuration, with the constraint strings
suggested below.

* provider.azurerm: version = "~> 0.2"

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

<span data-ttu-id="71db8-122">The [terraform init command](https://www.terraform.io/docs/commands/init.html) is used to initialize a working directory containing Terraform configuration files.</span><span class="sxs-lookup"><span data-stu-id="71db8-122">The [terraform init command](https://www.terraform.io/docs/commands/init.html) is used to initialize a working directory containing Terraform configuration files.</span></span> <span data-ttu-id="71db8-123">The `terraform init` command is the first command that should be run after writing a new Terraform configuration or cloning an existing one from version control.</span><span class="sxs-lookup"><span data-stu-id="71db8-123">The `terraform init` command is the first command that should be run after writing a new Terraform configuration or cloning an existing one from version control.</span></span> <span data-ttu-id="71db8-124">It is safe to run this command multiple times.</span><span class="sxs-lookup"><span data-stu-id="71db8-124">It is safe to run this command multiple times.</span></span>

### <a name="terraform-plan"></a><span data-ttu-id="71db8-125">Terraform plan</span><span class="sxs-lookup"><span data-stu-id="71db8-125">Terraform plan</span></span>
<span data-ttu-id="71db8-126">Preview the resources to be created by the Terraform template with `terraform plan`.</span><span class="sxs-lookup"><span data-stu-id="71db8-126">Preview the resources to be created by the Terraform template with `terraform plan`.</span></span>

```
justin@Azure:~$ terraform plan
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or remote state storage.


------------------------------------------------------------------------

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  + azurerm_resource_group.demo
      id:       <computed>
      location: "westus"
      name:     "myRGName"
      tags.%:   <computed>


Plan: 1 to add, 0 to change, 0 to destroy.

------------------------------------------------------------------------

Note: You didn't specify an "-out" parameter to save this plan, so Terraform
can't guarantee that exactly these actions will be performed if
"terraform apply" is subsequently run.
```

<span data-ttu-id="71db8-127">The [terraform plan command](https://www.terraform.io/docs/commands/plan.html) is used to create an execution plan.</span><span class="sxs-lookup"><span data-stu-id="71db8-127">The [terraform plan command](https://www.terraform.io/docs/commands/plan.html) is used to create an execution plan.</span></span> <span data-ttu-id="71db8-128">Terraform performs a refresh, unless explicitly disabled, and then determines what actions are necessary to achieve the desired state specified in the configuration files.</span><span class="sxs-lookup"><span data-stu-id="71db8-128">Terraform performs a refresh, unless explicitly disabled, and then determines what actions are necessary to achieve the desired state specified in the configuration files.</span></span> <span data-ttu-id="71db8-129">The plan can be saved using -out, and then provided to terraform apply to ensure only the pre-planned actions are executed.</span><span class="sxs-lookup"><span data-stu-id="71db8-129">The plan can be saved using -out, and then provided to terraform apply to ensure only the pre-planned actions are executed.</span></span>

### <a name="terraform-apply"></a><span data-ttu-id="71db8-130">Terraform apply</span><span class="sxs-lookup"><span data-stu-id="71db8-130">Terraform apply</span></span>
<span data-ttu-id="71db8-131">Provision the Azure resources with `terraform apply`.</span><span class="sxs-lookup"><span data-stu-id="71db8-131">Provision the Azure resources with `terraform apply`.</span></span>

```
justin@Azure:~$ terraform apply
azurerm_resource_group.demo: Creating...
  location: "" => "westus"
  name:     "" => "myRGName"
  tags.%:   "" => "<computed>"
azurerm_resource_group.demo: Creation complete after 0s (ID: /subscriptions/mySubIDmysub/resourceGroups/myRGName)

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

<span data-ttu-id="71db8-132">The [terraform apply command](https://www.terraform.io/docs/commands/apply.html) is used to apply the changes required to reach the desired state of the configuration.</span><span class="sxs-lookup"><span data-stu-id="71db8-132">The [terraform apply command](https://www.terraform.io/docs/commands/apply.html) is used to apply the changes required to reach the desired state of the configuration.</span></span>

### <a name="verify-deployment-with-azure-cli-20"></a><span data-ttu-id="71db8-133">Verify deployment with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="71db8-133">Verify deployment with Azure CLI 2.0</span></span>
<span data-ttu-id="71db8-134">Run `az group show -n myRgName` to verify the resource has succeeded provisioning.</span><span class="sxs-lookup"><span data-stu-id="71db8-134">Run `az group show -n myRgName` to verify the resource has succeeded provisioning.</span></span>

```azcliinteractive
az group show -n myRgName
```

### <a name="clean-up-with-terraform-destroy"></a><span data-ttu-id="71db8-135">Clean up with terraform destroy</span><span class="sxs-lookup"><span data-stu-id="71db8-135">Clean up with terraform destroy</span></span>
<span data-ttu-id="71db8-136">Clean up the resource group created with the [Terraform destroy command](https://www.terraform.io/docs/commands/destroy.html) to clean up Terraform-created infrastructure.</span><span class="sxs-lookup"><span data-stu-id="71db8-136">Clean up the resource group created with the [Terraform destroy command](https://www.terraform.io/docs/commands/destroy.html) to clean up Terraform-created infrastructure.</span></span>

```
justin@Azure:~$ terraform destroy
azurerm_resource_group.demo: Refreshing state... (ID: /subscriptions/mySubID/resourceGroups/myRGName)

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  - azurerm_resource_group.demo


Plan: 0 to add, 0 to change, 1 to destroy.

Do you really want to destroy?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

azurerm_resource_group.demo: Destroying... (ID: /subscriptions/mySubID/resourceGroups/myRGName)
azurerm_resource_group.demo: Still destroying... (ID: /subscriptions/mySubID/resourceGroups/myRGName, 10s elapsed)
azurerm_resource_group.demo: Still destroying... (ID: /subscriptions/mySubID/resourceGroups/myRGName, 20s elapsed)
azurerm_resource_group.demo: Still destroying... (ID: /subscriptions/mySubID/resourceGroups/myRGName, 30s elapsed)
azurerm_resource_group.demo: Still destroying... (ID: /subscriptions/mySubID/resourceGroups/myRGName, 40s elapsed)
azurerm_resource_group.demo: Destruction complete after 45s

Destroy complete! Resources: 1 destroyed.
```

<span data-ttu-id="71db8-137">You have successfully created an Azure resource through Terraform.</span><span class="sxs-lookup"><span data-stu-id="71db8-137">You have successfully created an Azure resource through Terraform.</span></span> <span data-ttu-id="71db8-138">Visit next steps to continue learning about Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="71db8-138">Visit next steps to continue learning about Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71db8-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="71db8-139">Next steps</span></span>
[<span data-ttu-id="71db8-140">Learn about the Terraform Azure provider</span><span class="sxs-lookup"><span data-stu-id="71db8-140">Learn about the Terraform Azure provider</span></span>](https://www.terraform.io/docs/providers/azurerm/#)<br>
[<span data-ttu-id="71db8-141">Bash in Cloud Shell quickstart</span><span class="sxs-lookup"><span data-stu-id="71db8-141">Bash in Cloud Shell quickstart</span></span>](quickstart.md)