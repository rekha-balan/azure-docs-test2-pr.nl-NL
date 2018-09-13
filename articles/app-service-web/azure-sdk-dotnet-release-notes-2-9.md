---
title: Azure SDK for .NET 2.9 Release Notes
description: Azure SDK for .NET 2.9 Release Notes
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: ''
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako;mikhegn
ms.openlocfilehash: 3c3fb275a7c980f71a3a30e6875b9515321bad99
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661894"
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Azure SDK for .NET 2.9 release notes

This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Azure SDK for .NET 2.9.6 release summary

Release date: 11/16/2016
 
No breaking changes to the Azure SDK 2.9 have been introduced in this release. There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 Release Candidate

- In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload. All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward. For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI. We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product. Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Azure Diagnostics

- Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string. The actual storage key is now stored in the user profile folder so its access can be controlled. Visual Studio will read the storage key from user profile folder for local debugging and publishing process. 
- In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.
- We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 virtual machines

- Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines. For existing cloud services, you can change your settings to target the new OS Family. When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.  For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Known issues

- Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5. A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Azure In-Role Cache 

- Support for Azure In-Role Cache ends on November 30, 2016. For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Azure Resource Manager Templates for Azure Stack

- We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.


## <a name="azure-sdk-for-net-29-summary"></a>Azure SDK for .NET 2.9 summary

## <a name="overview"></a>Overview
This document contains the release notes for the Azure SDK for .NET 2.9 release. 

For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview
This update includes the following bug fixes:

* Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.
* Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.

This update includes the following new feature:

* Support for secondary App Services in the "Services" tab of the App Service provisioning dialog. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Azure Data Lake Tools for Visual Studio 2015 Update 2
This updates includes the following:

* **Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release. The tool is automatically installed when you install Azure SDK. 
  
    The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.
* **Server Explorer** now enables you to view all and create some U-SQL metadata entities. For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.

## <a name="hdinsight-tools"></a>HDInsight Tools
**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.

## <a name="azure-resource-manager"></a>Azure Resource Manager
This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.

## <a name="see-also"></a>See also
[Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

