---
title: Run Ansible with Bash in Azure Cloud Shell
description: Learn how to perform various Ansible tasks with Bash in Azure Cloud Shell
ms.service: ansible
keywords: ansible, azure, devops, bash, cloudshell, playbook, bash
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.date: 08/07/2018
ms.topic: article
ms.openlocfilehash: 9928f646905dd0da4b15166ec55e5d8a183cb210
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867918"
---
# <a name="run-ansible-with-bash-in-azure-cloud-shell"></a>Run Ansible with Bash in Azure Cloud Shell

In this tutorial, you learn how to use Bash within Cloud Shell to configure an Azure subscription as your Ansible workspace. 

## <a name="prerequisites"></a>Prerequisites

- **Azure subscription** - If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).

- **Configure Azure Cloud Shell** - If you are new to Azure Cloud Shell, the article, [Quickstart for Bash in Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart), illustrates how to start and configure Cloud Shell. 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="automatic-credential-configuration"></a>Automatic credential configuration

When signed into the Cloud Shell, Ansible authenticates with Azure to manage infrastructure without any additional configuration. If you have more than one subscription, you can choose which subscription Ansible should work with by exporting the `AZURE_SUBSCRIPTION_ID` environment variable. To list all of your Azure subscriptions, run the following command:

```azurecli-interactive
az account list
```

Using the **id** of the subscription with which you want to work, set the **AZURE_SUBSCRIPTION_ID** as follows:

```azurecli-interactive
export AZURE_SUBSCRIPTION_ID=<your-subscription-id>
```

## <a name="verify-the-configuration"></a>Verify the configuration
To verify the successful configuration, use Ansible to create a resource group.

[!INCLUDE [create-resource-group-with-ansible.md](../../includes/ansible-create-resource-group.md)]

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"] 
> [Create a basic virtual machine in Azure with Ansible](/azure/virtual-machines/linux/ansible-create-vm)