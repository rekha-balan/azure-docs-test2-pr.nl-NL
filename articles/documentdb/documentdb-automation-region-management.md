---
title: DocumentDB Automation - Managing Regions | Microsoft Docs
description: Use Azure CLI 1.0 and Azure Resource Manager to manage regions in a DocumentDB database account. DocumentDB is a cloud-based NoSQL database for JSON data.
services: documentdb
author: dmakwana
manager: jhubbard
editor: ''
tags: azure-resource-manager
documentationcenter: ''
ms.assetid: 7f765c17-8549-4108-9475-46394fc3a218
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: dimakwan
ms.openlocfilehash: 598cdc91e9fc019b473d6e85bfc7167aaa95ef93
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563454"
---
# <a name="automate-documentdb-account-region-management-using-azure-cli-10-and-azure-resource-manager-templates"></a>Automate DocumentDB account region management using Azure CLI 1.0 and Azure Resource Manager templates

This article shows you how to add/remove a region in your Azure DocumentDB account by using Azure CLI 1.0 commands and Azure Resource Manager templates. Region management can also be accomplished through the [Azure Portal](documentdb-portal-global-replication.md). Note that the commands in the following tutorial do not allow you to change failover priorities of the various regions. Only read regions can  be added or removed. The write region of a database account (failover priority of 0) cannot be added/removed.

DocumentDB database accounts are currently the only DocumentDB resource that can be created/modified using [Azure Resource Manager templates and Azure CLI 1.0](documentdb-automation-resource-manager-cli.md).

## <a name="getting-ready"></a>Getting ready

Before you can use Azure CLI 1.0 with Azure resource groups, you need to have the right Azure CLI 1.0 version and an Azure account. If you don't have Azure CLI 1.0, [install it](../cli-install-nodejs.md).

### <a name="update-your-azure-cli-10-version"></a>Update your Azure CLI 1.0 version

At the command prompt, type `azure --version` to see whether you have already installed version 0.10.4 or later. You may be prompted to participate in Microsoft Azure CLI 1.0 data collection at this step, and can select y or n to opt-in or opt-out.

    azure --version
    0.10.4 (node: 4.2.4)

If your version is not 0.10.4 or later, you need to either [install Azure CLI 1.0](../cli-install-nodejs.md) or update by using one of the native installers, or through **npm** by typing `npm update -g azure-cli` to update or `npm install -g azure-cli` to install.

### <a name="set-your-azure-account-and-subscription"></a>Set your Azure account and subscription

If you don't already have an Azure subscription but you do have a Visual Studio subscription, you can activate your [Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).

You need to have a work or school account or a Microsoft account identity to use Azure resource management templates. If you have one of these accounts, type the following command.

    azure login

Which produces the following output: 

    info:    Executing command login
    |info:    To sign in, use a web browser to open the page https://aka.ms/devicelogin. 
    Enter the code E1A2B3C4D to authenticate.

> [!NOTE]
> If you don't have an Azure account, you'll see an error message indicating that you need a different type of account. To create one from your current Azure account, see [Creating a work or school identity in Azure Active Directory](../virtual-machines/windows/create-aad-work-id.md).

Open [https://aka.ms/devicelogin](https://aka.ms/devicelogin) in a browser and enter the code provided in the command output.

![Screenshot showing the device login screen for Microsoft Azure CLI 1.0](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/azure-cli-login-code.png)

Once you've entered the code, select the identity you want to use in the browser and provide your user name and password if needed.

![Screenshot showing where to select the Microsoft identity account associated with the Azure subscription you want to use](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/identity-cli-login.png)

You'll receive the following confirmation screen when you're successfully logged in, and you can then close the browser window.

![Screenshot showing confirmation of login to the Microsoft Azure Cross-platform Command Line Interface](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/login-confirmation.png)

The command shell also provides the following output.

    /info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

In addition to the interactive login method described here, there are additional Azure CLI 1.0 login methods available. For more information about the other methods and information about handling multiple subscriptions, see [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI 1.0)](../xplat-cli-connect.md).

### <a name="switch-to-azure-cli-10-resource-group-mode"></a>Switch to Azure CLI 1.0 resource group mode

By default, Azure CLI 1.0 starts in the service management mode (**asm** mode). Type the following to switch to resource group mode.

    azure config mode arm

Which provides the following output:

    info:    Executing command config mode
    info:    New mode is arm
    info:    config mode command OK

If needed, you can switch back to the default set of commands by typing `azure config mode asm`.

### <a name="create-or-retrieve-your-resource-group"></a>Create or retrieve your resource group

In order to create a DocumentDB account, you first need a resource group. If you already know the name of the resource group that you'd like to use, then skip to [Step 2](#create-documentdb-account-cli). 

To review a list of all of your current resource groups, run the following command and take note of the resource group name you'd like to use: 

    azure group list

To create a new resource group, run the following command, specify the name of the new resource group to create, and the region in which to create the resource group: 

    azure group create <resourcegroupname> <resourcegrouplocation>

 - `<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period. 
 - `<resourcegrouplocation>` must be one of the regions in which DocumentDB is generally available. The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).

Example input:

    azure group create new_res_group westus

Which produces the following output:

    info:    Executing command group create
    + Getting resource group new_res_group
    + Creating resource group new_res_group
    info:    Created resource group new_res_group
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/new_res_group
    data:    Name:                new_res_group
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

If you encounter errors, see [Troubleshooting](#troubleshooting). 

## <a name="understanding-azure-resource-manager-templates-and-resource-groups"></a>Understanding Azure Resource Manager templates and resource groups

Most applications are built from a combination of different resource types (such as one or more DocumentDB account, storage accounts, a virtual network, or a content delivery network). The default Azure service management API and the Azure portal represented these items by using a service-by-service approach. This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.

*Azure Resource Manager templates* make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion. Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.

You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md). If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).


## <a id="add-region-documentdb-account"></a>Task: Add Region to a DocumentDB account

DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services). The instructions in this section describe how to add a read region to an existing DocumentDB account with Azure CLI 1.0 and Resource Manager templates. This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.

### <a id="add-region-documentdb-account-cli"></a> Add Region to a DocumentDB account using Azure CLI 1.0 without Resource Manager templates

Add a region to an existing DocumentDB account in the new or existing resource group by entering the command below at the command prompt. Note that the "locations" array should reflect the current region configuration within the DocumentDB account with the exception of the new region to be added. The example below shows a command to add a second region to the account.

Match the failover priority values to the existing configuration. One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally]. The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions. The new region will be a "Read" region and must have a failover priority value greater than 0.

> [!TIP]
> If you run this command in Azure PowerShell or Windows PowerShell you will receive an error about an unexpected token. Instead, run this command at the Windows Command Prompt.

    azure resource create -g <resourcegroupname> -n <databaseaccountname> -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l <resourcegrouplocation> -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"<ip-range-filter>\",\"locations\":["{\"locationName\":\"<databaseaccountlocation>\",\"failoverPriority\":\"<failoverPriority1>\"},{\"locationName\":\"<newdatabaseaccountlocation>\",\"failoverPriority\":\"<failoverPriority2>\"}"]}"

 - `<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.
 - `<resourcegrouplocation>` is the region of the current resource group.
 - `<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account. IP addresses/ranges must be comma separated and must not contain any spaces. For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)
 - `<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.
 - `<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available. The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).
 - `<newdatabaseaccountlocation>` is the new region to be added and must be one of the regions in which DocumentDB is generally available. The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).


Example input for adding the "East US" region as a read region in the DocumentDB account: 

    azure resource create -g new_res_group -n samplecliacct -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l westus -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"\",\"locations\":["{\"locationName\":\"westus\",\"failoverPriority\":\"0\"},{\"locationName\":\"eastus\",\"failoverPriority\":\"1\"}"]}"

Which produces the following output as your new account is provisioned:

    info:    Executing command resource create
    + Getting resource samplecliacct
    + Creating resource samplecliacct
    info:    Resource samplecliacct is updated
    data:
    data:    Id:        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/new_res_group/providers/Microsoft.DocumentDB/databaseAccounts/samplecliacct
    data:    Name:      samplecliacct
    data:    Type:      Microsoft.DocumentDB/databaseAccounts
    data:    Parent:
    data:    Location:  West US
    data:    Tags:
    data:
    info:    resource create command OK

If you encounter errors, see [Troubleshooting](#troubleshooting). 

After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use. You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.

### <a id="add-region-documentdb-account-cli-arm"></a> Add Region to a DocumentDB account using Azure CLI 1.0 with Resource Manager templates

The instructions in this section describe how to add a region to an existing DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files. Using a template enables you to describe exactly what you want and repeat it without errors.

Match the failover priority values to the existing configuration. One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally]. The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions. The new region will be a "Read" region and must have a failover priority value greater than 0.

Create a local template file similar to the one below that matches your current DocumentDB region configuration. The "locations" array should contain all of the existing regions in the database account alongside the new region to be added. Name the file azuredeploy.json.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "type": "string"
            },
            "locationName1": {
                "type": "string"
            },
            "locationName2": {
                "type": "string"
            },
            "newLocationName": {
                "type": "string"
            }
        },
        "variables": {},
        "resources": [
            {
                "apiVersion": "2015-04-08",
                "type": "Microsoft.DocumentDb/databaseAccounts",
                "name": "[parameters('databaseAccountName')]",
                "location": "[resourceGroup().location]",
                "properties": {
                    "databaseAccountOfferType": "Standard",
                    "ipRangeFilter": "",
                    "locations": [
                        {
                            "failoverPriority": 0,
                            "locationName": "[parameters('locationName1')]"
                        },
                        {
                            "failoverPriority": 1,
                            "locationName": "[parameters('locationName2')]"
                        },
                        {
                            "failoverPriority": 2,
                            "locationName": "[parameters('newLocationName')]"
                        }
                    ]
                }
            }
        ]
    }

The above template file demonstrates an example where a new region is being added to a DocumentDB account which already has 2 regions.

You can either enter the parameter values at the command line, or create a parameter file to specify the value.

To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json. If you plan on specifying the database account name at the command prompt, you can continue without creating this file.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "value": "samplearmacct"
            },
            "locationName1": {
                "value": "westus"
            },
            "locationName2": {
                "value": "eastus"
            },
            "newLocationName": {
                "value": "northeurope"
            }
        }
    }

In the azuredeploy.parameters.json file, update the value field of  `"databaseAccountName"` to the database name you'd like to use, then save the file. `"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters. Update the value fields of `"locationName1"` and `"locationName2"` to the regions where your DocumentDB account exists. Update the value field of `"newLocationName"` to the region that you would like to add.

To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional). 

To use a parameter file:

    azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g <resourcegroupname> -n <deploymentname>

 - `<PathToTemplate>` is the path to the azuredeploy.json file created in step 1. If your path name has spaces in it, put double quotes around this parameter.
 - `<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1. If your path name has spaces in it, put double quotes around this parameter.
 - `<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account. 
 - `<deploymentname>` is the optional name of the deployment.

Example input: 

    azure group deployment create -f azuredeploy.json -e azuredeploy.parameters.json -g new_res_group -n azuredeploy

OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:

    azure group deployment create -f <PathToTemplate> -g <resourcegroupname> -n <deploymentname>

Example input which shows the prompt and entry for a database account named samplearmacct:

    azure group deployment create -f azuredeploy.json -g new_res_group -n azuredeploy
    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    databaseAccountName: samplearmacct

As the account is provisioned, you will receive the following information: 

    info:    Executing command group deployment create
    + Initializing template configurations and parameters
    + Creating a deployment
    info:    Created template deployment "azuredeploy"
    + Waiting for deployment to complete
    + 
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Running
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Succeeded
    data:    DeploymentName     : azuredeploy
    data:    ResourceGroupName  : new_res_group
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          : 2015-11-30T18:50:23.6300288Z
    data:    Mode               : Incremental
    data:    CorrelationId      : 4a5d4049-c494-4053-bad4-cc804d454700
    data:    DeploymentParameters :
    data:    Name                 Type    Value
    data:    -------------------  ------  ------------------
    data:    locationName1        String  westus
    data:    locationName2        String  eastus
    data:    newLocationName      String  eastus
    data:    databaseAccountName  String  samplearmacct
    info:    group deployment create command OK

If you encounter errors, see [Troubleshooting](#troubleshooting).  

After the command returns, the account will be in the **Creating** state for a few minutes, before it changes to the **Online** state in which it is ready for use. You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.

## <a id="remove-region-documentdb-account"></a>Task: Remove Region from a DocumentDB account

DocumentDB has the capability to [distribute your data globally][distribute-globally] across various [Azure regions](https://azure.microsoft.com/regions/#services). The instructions in this section describe how to remove a region from an existing DocumentDB account with Azure CLI 1.0 and Resource Manager Templates. This can be accomplished using Azure CLI 1.0 with or without Resource Manager templates.

### <a id="remove-region-documentdb-account-cli"></a> Remove Region to a DocumentDB account using Azure CLI 1.0 without Resource Manager templates

To remove a region from an existing DocumentDB account, the command below can be executed with Azure CLI 1.0. The "locations" array should contain only the regions that are to remain after the removal of the region. **The omitted location will be removed from the DocumentDB account**. Enter the following command in the command prompt.

One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally]. The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions. 

> [!TIP]
> If you run this command in Azure PowerShell or Windows PowerShell you will receive an error about an unexpected token. Instead, run this command at the Windows Command Prompt.

    azure resource create -g <resourcegroupname> -n <databaseaccountname> -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l <resourcegrouplocation> -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"<ip-range-filter>\",\"locations\":["{\"locationName\":\"<databaseaccountlocation>\",\"failoverPriority\":\"<failoverPriority>\"}"]}"

 - `<resourcegroupname>` can only use alphanumeric characters, periods, underscores, the '-' character, and parenthesis and cannot end in a period.
 - `<resourcegrouplocation>` is the region of the current resource group.
 - `<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account. IP addresses/ranges must be comma separated and must not contain any spaces. For more information, see [DocumentDB Firewall Support](documentdb-firewall-support.md)
 - `<databaseaccountname>` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.
 - `<databaseaccountlocation>` must be one of the regions in which DocumentDB is generally available. The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).

Example input: 

    azure resource create -g new_res_group -n samplecliacct -r "Microsoft.DocumentDB/databaseAccounts" -o 2015-04-08 -l westus -p "{\"databaseAccountOfferType\":\"Standard\",\"ipRangeFilter\":\"\",\"locations\":["{\"locationName\":\"westus\",\"failoverPriority\":\"0\"}"]}"

Which produces the following output as your new account is provisioned:

    info:    Executing command resource create
    + Getting resource samplecliacct
    + Creating resource samplecliacct
    info:    Resource samplecliacct is updated
    data:
    data:    Id:        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/new_res_group/providers/Microsoft.DocumentDB/databaseAccounts/samplecliacct
    data:    Name:      samplecliacct
    data:    Type:      Microsoft.DocumentDB/databaseAccounts
    data:    Parent:
    data:    Location:  West US
    data:    Tags:
    data:
    info:    resource create command OK

If you encounter errors, see [Troubleshooting](#troubleshooting). 

After the command returns, the account will be in the **Updating** state for a few minutes, before it changes to the **Online** state in which it is ready for use. You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.

### <a id="remove-region-documentdb-account-cli-arm"></a> Remove Region from a DocumentDB account using Azure CLI 1.0 with Resource Manager templates

The instructions in this section describe how to remove a region from an existing DocumentDB account with an Azure Resource Manager template and an optional parameters file, both of which are JSON files. Using a template enables you to describe exactly what you want and repeat it without errors.

One of the regions must have a failoverPriority value of 0 to indicate that this region be kept as the [write region for the DocumentDB account][scaling-globally]. The failover priority values must be unique amongst the locations and the highest failover priority value must be less than the total number of regions. 

Create a local template file similar to the one below that matches your current DocumentDB region configuration. The "locations" array should contain only the regions that are to remain after the removal of the region. **The omitted location will be removed from the DocumentDB account**. Name the file azuredeploy.json.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "type": "string"
            },
            "locationName1": {
                "type": "string"
            }
        },
        "variables": {},
        "resources": [
            {
                "apiVersion": "2015-04-08",
                "type": "Microsoft.DocumentDb/databaseAccounts",
                "name": "[parameters('databaseAccountName')]",
                "location": "[resourceGroup().location]",
                "properties": {
                    "databaseAccountOfferType": "Standard",
                    "ipRangeFilter": "",
                    "locations": [
                        {
                            "failoverPriority": 0,
                            "locationName": "[parameters('locationName1')]"
                        }
                    ]
                }
            }
        ]
    }

You can either enter the parameter values at the command line, or create a parameter file to specify the value.

To create a parameters file, copy the following content into a new file and name the file azuredeploy.parameters.json. If you plan on specifying the database account name at the command prompt, you can continue without creating this file. Be sure to add the necessary parameters that are defined in your Azure Resource Manager template.

    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "databaseAccountName": {
                "value": "samplearmacct"
            },
            "locationName1": {
                "value": "westus"
            }
        }
    }

In the azuredeploy.parameters.json file, update the value field of  `"databaseAccountName"` to the database name you'd like to use, then save the file. `"databaseAccountName"` can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters. Update the value field of `"locationName1"` to the regions where you want the DocumentDB account to exist after the removal of the region.

To create a DocumentDB account in your resource group, run the following command and provide the path to the template file, the path to the parameter file or the parameter value, the name of the resource group in which to deploy, and a deployment name (-n is optional). 

To use a parameter file:

    azure group deployment create -f <PathToTemplate> -e <PathToParameterFile> -g <resourcegroupname> -n <deploymentname>

 - `<PathToTemplate>` is the path to the azuredeploy.json file created in step 1. If your path name has spaces in it, put double quotes around this parameter.
 - `<PathToParameterFile>` is the path to the azuredeploy.parameters.json file created in step 1. If your path name has spaces in it, put double quotes around this parameter.
 - `<resourcegroupname>` is the name of the existing resource group in which to add a DocumentDB database account. 
 - `<deploymentname>` is the optional name of the deployment.

Example input: 

    azure group deployment create -f azuredeploy.json -e azuredeploy.parameters.json -g new_res_group -n azuredeploy

OR to specify the database account name parameter without a parameter file, and instead get prompted for the value, run the following command:

    azure group deployment create -f <PathToTemplate> -g <resourcegroupname> -n <deploymentname>

Example input which shows the prompt and entry for a database account named samplearmacct:

    azure group deployment create -f azuredeploy.json -g new_res_group -n azuredeploy
    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    databaseAccountName: samplearmacct

As the account is provisioned, you will receive the following information: 

    info:    Executing command group deployment create
    + Initializing template configurations and parameters
    + Creating a deployment
    info:    Created template deployment "azuredeploy"
    + Waiting for deployment to complete
    + 
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Running
    + 
    info:    Resource 'new_res_group' of type 'Microsoft.DocumentDb/databaseAccounts' provisioning status is Succeeded
    data:    DeploymentName     : azuredeploy
    data:    ResourceGroupName  : new_res_group
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          : 2015-11-30T18:50:23.6300288Z
    data:    Mode               : Incremental
    data:    CorrelationId      : 4a5d4049-c494-4053-bad4-cc804d454700
    data:    DeploymentParameters :
    data:    Name                 Type    Value
    data:    -------------------  ------  ------------------
    data:    databaseAccountName  String  samplearmacct
    data:    locationName1        String  westus
    info:    group deployment create command OK

If you encounter errors, see [Troubleshooting](#troubleshooting).  

After the command returns, the account will be in the **Updating** state for a few minutes, before it changes to the **Online** state in which it is ready for use. You can check on the status of the account in the [Azure portal](https://portal.azure.com), on the **DocumentDB Accounts** blade.

## <a name="troubleshooting"></a>Troubleshooting

If you receive errors like `Deployment provisioning state was not successful` while creating your resource group or database account, you have a few troubleshooting options. 

> [!NOTE]
> Providing incorrect characters in the database account name or providing a location in which DocumentDB is not available will cause deployment errors. Database account names can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters. All valid database account locations are listed on the [Azure Regions page](https://azure.microsoft.com/regions/#services).

- If your output contains the following `Error information has been recorded to C:\Users\wendy\.azure\azure.err`, then review the error info in the azure.err file.

- You may find useful info in the log file for the resource group. To view the log file, run the following command:

        azure group log show <resourcegroupname> --last-deployment

    Example input:       azure group log show new_res_group --last-deployment

    Then see [Troubleshooting resource group deployments in Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md) for additional information.

- Error information is also available in the Azure Portal as shown in the following screenshot. To navigate to the error info: click Resource Groups in the Jumpbar, select the Resource Group that had the error, then in the Essentials area of the Resource group blade click the date of the Last Deployment, then in the Deployment history blade select the failed deployment, then in the Deployment blade click the Operation detail with the red exclamation mark. The Status Message for the failed deployment is displayed in the Operation details blade. 

    ![Screenshot of the Azure portal showing how to navigate to the deployment error message](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-automation-resource-manager-cli/portal-troubleshooting-deploy.png) 

## <a name="next-steps"></a>Next steps

Now that you have a DocumentDB account, the next step is to create a DocumentDB database. You can create a database by using one of the following:

- The Azure portal, as described in [Create a DocumentDB collection and database using the Azure portal](documentdb-create-collection.md).
- The C# .NET samples in the [DatabaseManagement](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples/DatabaseManagement) project of the [azure-documentdb-dotnet](https://github.com/Azure/azure-documentdb-net/tree/master/samples/code-samples) repository on GitHub.
- The [DocumentDB SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx). DocumentDB has .NET, Java, Python, Node.js, and JavaScript API SDKs. 

After creating your database, you need to [add one or more collections](documentdb-create-collection.md) to the database, then [add documents](documentdb-view-json-document-explorer.md) to the collections. 

After you have documents in a collection, you can use [DocumentDB SQL](documentdb-sql-query.md) to [execute queries](documentdb-sql-query.md#ExecutingSqlQueries) against your documents by using the [Query Explorer](documentdb-query-collections-query-explorer.md) in the portal, the [REST API](https://msdn.microsoft.com/library/azure/dn781481.aspx), or one of the [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).

To learn more about DocumentDB, explore these resources:

-   [Learning path for DocumentDB](https://azure.microsoft.com/documentation/learning-paths/documentdb/)
-   [DocumentDB resource model and concepts](documentdb-resources.md)

For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/).

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[distribute-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally
[scaling-globally]: https://azure.microsoft.com/en-us/documentation/articles/documentdb-distribute-data-globally/#scaling-across-the-planet




