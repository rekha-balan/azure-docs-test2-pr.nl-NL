---
title: Command-line build for Azure | Microsoft Docs
description: Command-line build for Azure
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: tarcher
ms.openlocfilehash: 5add8703b7b16ba8d9dc49f42f5e71b195c46653
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564174"
---
# <a name="building-azure-projects-from-the-command-line"></a>Building Azure projects from the command line
Using the Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed. MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft. Using the MSBuild file format, you can describe what items must be built for one or more platforms and configurations.

You can also run MSBuild at the command line, and this topic describes that approach. By setting properties on the command line, you can build specific configurations of a project. Similarly, you can also define the targets that MSBuild builds. For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>MSBuild parameters
The simplest way to create a package is to run MSBuild with the `/t:Publish` option. By default, this command creates a directory in relation to the root folder for the project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`. When you build an Azure project, two files are generated: the package file itself and the accompanying configuration file:

* Package File (`project.cspkg`)
* Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)

By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds. However, you can add or remove service-configuration files as needed. When you build a package within Visual Studio, you are asked which service-configuration file to include alongside the package. When you build a package by using MSBuild, the local service-configuration file is included by default. To include a different service-configuration file, set the `TargetProfile` property of the MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

If you want to use an alternate directory for the stored package and configuration files, set the path by using the `/p:PublishDir=Directory\` option, including the trailing backslash separator.

## <a name="next-steps"></a>Next steps
After the package is built, you can deploy it to Azure. For a tutorial that demonstrates how to automate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

