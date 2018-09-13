---
title: What's New in the Azure Toolkit for IntelliJ | Microsoft Docs
description: Learn about the latest features in the Azure Toolkit for IntelliJ.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: a2006dbcf0d63ef38651a0859dc654d531fd875a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556185"
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a><span data-ttu-id="0f398-103">What's New in the Azure Toolkit for IntelliJ</span><span class="sxs-lookup"><span data-stu-id="0f398-103">What's New in the Azure Toolkit for IntelliJ</span></span>
## <a name="azure-toolkit-for-intellij-releases"></a><span data-ttu-id="0f398-104">Azure Toolkit for IntelliJ Releases</span><span class="sxs-lookup"><span data-stu-id="0f398-104">Azure Toolkit for IntelliJ Releases</span></span>
<span data-ttu-id="0f398-105">This article contains information on the various releases and latest updates to the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0f398-105">This article contains information on the various releases and latest updates to the Azure Toolkit for IntelliJ.</span></span>

> [!NOTE]
> <span data-ttu-id="0f398-106">There is also an Azure Toolkit for the Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="0f398-106">There is also an Azure Toolkit for the Eclipse IDE.</span></span> <span data-ttu-id="0f398-107">For more information, see [Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="0f398-107">For more information, see [Azure Toolkit for Eclipse].</span></span>
> 
> 

### <a name="august-26-2016"></a><span data-ttu-id="0f398-108">August 26, 2016</span><span class="sxs-lookup"><span data-stu-id="0f398-108">August 26, 2016</span></span>
<span data-ttu-id="0f398-109">The Azure Toolkit for IntelliJ - August 2016 release includes the following enhancements:</span><span class="sxs-lookup"><span data-stu-id="0f398-109">The Azure Toolkit for IntelliJ - August 2016 release includes the following enhancements:</span></span>

* <span data-ttu-id="0f398-110">**Custom JDK Distributions**.</span><span class="sxs-lookup"><span data-stu-id="0f398-110">**Custom JDK Distributions**.</span></span> <span data-ttu-id="0f398-111">The Azure Toolkit for IntelliJ now supports specifying and deploying an arbitrary JDK version to your Azure WebApp container:</span><span class="sxs-lookup"><span data-stu-id="0f398-111">The Azure Toolkit for IntelliJ now supports specifying and deploying an arbitrary JDK version to your Azure WebApp container:</span></span>
  * <span data-ttu-id="0f398-112">In addition to the JDKs provided by Azure, you can also choose from a wide selection of Zulu OpenJDK versions made available on Azure by Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="0f398-112">In addition to the JDKs provided by Azure, you can also choose from a wide selection of Zulu OpenJDK versions made available on Azure by Azul Systems.</span></span>
  * <span data-ttu-id="0f398-113">You can also specify your own JDK distribution if you upload it as a ZIP file to your storage account.</span><span class="sxs-lookup"><span data-stu-id="0f398-113">You can also specify your own JDK distribution if you upload it as a ZIP file to your storage account.</span></span>
* <span data-ttu-id="0f398-114">**Enhancements to the Azure Explorer view**:</span><span class="sxs-lookup"><span data-stu-id="0f398-114">**Enhancements to the Azure Explorer view**:</span></span>
  * <span data-ttu-id="0f398-115">Support for Virtual Machine management using Azure's new Resource Manager model: you can list, create and delete resource manager-based virtual machines without leaving the IDE.</span><span class="sxs-lookup"><span data-stu-id="0f398-115">Support for Virtual Machine management using Azure's new Resource Manager model: you can list, create and delete resource manager-based virtual machines without leaving the IDE.</span></span>
  * <span data-ttu-id="0f398-116">Support for Storage Account blob management using Azure's Resource Manager, which complements the existing functionality for managing "classic" storage accounts.</span><span class="sxs-lookup"><span data-stu-id="0f398-116">Support for Storage Account blob management using Azure's Resource Manager, which complements the existing functionality for managing "classic" storage accounts.</span></span>
* <span data-ttu-id="0f398-117">**Microsoft JDBC Driver 6.0 for SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0f398-117">**Microsoft JDBC Driver 6.0 for SQL Server**.</span></span> <span data-ttu-id="0f398-118">This update includes the latest JDBC driver for Microsoft SQL Server (v6.0), which is now included as a library that you can easily add to your Java projects, thereby replacing the older version.</span><span class="sxs-lookup"><span data-stu-id="0f398-118">This update includes the latest JDBC driver for Microsoft SQL Server (v6.0), which is now included as a library that you can easily add to your Java projects, thereby replacing the older version.</span></span>

### <a name="june-29-2016"></a><span data-ttu-id="0f398-119">June 29, 2016</span><span class="sxs-lookup"><span data-stu-id="0f398-119">June 29, 2016</span></span>
<span data-ttu-id="0f398-120">The Azure Toolkit for IntelliJ - June 2016 release includes the following enhancements:</span><span class="sxs-lookup"><span data-stu-id="0f398-120">The Azure Toolkit for IntelliJ - June 2016 release includes the following enhancements:</span></span>

* <span data-ttu-id="0f398-121">**Java 8 Requirement**.</span><span class="sxs-lookup"><span data-stu-id="0f398-121">**Java 8 Requirement**.</span></span> <span data-ttu-id="0f398-122">The Azure Toolkit for IntelliJ now requires Java 8, although this requirement is only for the toolkit - your applications can continue to use all versions of Java that are supported by Azure.</span><span class="sxs-lookup"><span data-stu-id="0f398-122">The Azure Toolkit for IntelliJ now requires Java 8, although this requirement is only for the toolkit - your applications can continue to use all versions of Java that are supported by Azure.</span></span>
* <span data-ttu-id="0f398-123">**Support for the latest Java JDKs**.</span><span class="sxs-lookup"><span data-stu-id="0f398-123">**Support for the latest Java JDKs**.</span></span> <span data-ttu-id="0f398-124">The latest versions of the Java JDKs are now supported by the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0f398-124">The latest versions of the Java JDKs are now supported by the Azure Toolkit for IntelliJ.</span></span>
* <span data-ttu-id="0f398-125">**Support for Azure SDK v2.9.1**.</span><span class="sxs-lookup"><span data-stu-id="0f398-125">**Support for Azure SDK v2.9.1**.</span></span> <span data-ttu-id="0f398-126">The latest version of the Azure SDK is now the minimum pre-requisite for the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0f398-126">The latest version of the Azure SDK is now the minimum pre-requisite for the Azure Toolkit for IntelliJ.</span></span>
* <span data-ttu-id="0f398-127">**Integrated Samples**.</span><span class="sxs-lookup"><span data-stu-id="0f398-127">**Integrated Samples**.</span></span> <span data-ttu-id="0f398-128">The Azure Toolkit for IntelliJ now features several sample applications to help developers get started.</span><span class="sxs-lookup"><span data-stu-id="0f398-128">The Azure Toolkit for IntelliJ now features several sample applications to help developers get started.</span></span>
* <span data-ttu-id="0f398-129">**HDInsight Tool Integration**.</span><span class="sxs-lookup"><span data-stu-id="0f398-129">**HDInsight Tool Integration**.</span></span> <span data-ttu-id="0f398-130">Azure's HDInsight Tools are now bundled with the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0f398-130">Azure's HDInsight Tools are now bundled with the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="0f398-131">For more information, see [HDInsight Tools Plugin for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="0f398-131">For more information, see [HDInsight Tools Plugin for IntelliJ].</span></span>
* <span data-ttu-id="0f398-132">**Remote Debugging of Java Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="0f398-132">**Remote Debugging of Java Web Apps**.</span></span> <span data-ttu-id="0f398-133">The Azure Toolkit for IntelliJ now supports remote debugging of Java web apps on Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0f398-133">The Azure Toolkit for IntelliJ now supports remote debugging of Java web apps on Azure App Service.</span></span>

### <a name="april-12-2016"></a><span data-ttu-id="0f398-134">April 12, 2016</span><span class="sxs-lookup"><span data-stu-id="0f398-134">April 12, 2016</span></span>
<span data-ttu-id="0f398-135">The Azure Toolkit for IntelliJ - April 2016 release includes the following enhancements:</span><span class="sxs-lookup"><span data-stu-id="0f398-135">The Azure Toolkit for IntelliJ - April 2016 release includes the following enhancements:</span></span>

* <span data-ttu-id="0f398-136">**Support for Azure SDK v2.9.0**.</span><span class="sxs-lookup"><span data-stu-id="0f398-136">**Support for Azure SDK v2.9.0**.</span></span> <span data-ttu-id="0f398-137">The latest version of the Azure SDK is now the minimum pre-requisite for the Azure Toolkit for IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0f398-137">The latest version of the Azure SDK is now the minimum pre-requisite for the Azure Toolkit for IntelliJ.</span></span>
* <span data-ttu-id="0f398-138">**Miscellaneous usability, responsiveness and performance improvements related to Azure Web App support**.</span><span class="sxs-lookup"><span data-stu-id="0f398-138">**Miscellaneous usability, responsiveness and performance improvements related to Azure Web App support**.</span></span> <span data-ttu-id="0f398-139">A number of performance optimizations in how the Toolkit communicates with Azure result in a more responsive UI.</span><span class="sxs-lookup"><span data-stu-id="0f398-139">A number of performance optimizations in how the Toolkit communicates with Azure result in a more responsive UI.</span></span>
* <span data-ttu-id="0f398-140">**Ability to delete an existing Web Application container in Azure from within IntelliJ**.</span><span class="sxs-lookup"><span data-stu-id="0f398-140">**Ability to delete an existing Web Application container in Azure from within IntelliJ**.</span></span> <span data-ttu-id="0f398-141">The Azure Toolkit for IntelliJ now allows you to delete an existing Azure Web container without leaving IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="0f398-141">The Azure Toolkit for IntelliJ now allows you to delete an existing Azure Web container without leaving IntelliJ.</span></span>

## <a name="see-also"></a><span data-ttu-id="0f398-142">See Also</span><span class="sxs-lookup"><span data-stu-id="0f398-142">See Also</span></span>
<span data-ttu-id="0f398-143">For more information about the Azure Toolkits for Java IDEs, see the following links:</span><span class="sxs-lookup"><span data-stu-id="0f398-143">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="0f398-144">[Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0f398-144">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0f398-145">[Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0f398-145">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="0f398-146">[Create a Hello World Web App for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0f398-146">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="0f398-147">[What's New in the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0f398-147">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="0f398-148">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0f398-148">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0f398-149">[Installing the Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0f398-149">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="0f398-150">[Create a Hello World Web App for Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="0f398-150">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="0f398-151">*What's New in the Azure Toolkit for IntelliJ (This Article)*</span><span class="sxs-lookup"><span data-stu-id="0f398-151">*What's New in the Azure Toolkit for IntelliJ (This Article)*</span></span>

<span data-ttu-id="0f398-152">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="0f398-152">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[What's New in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's New in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547

[HDInsight Tools Plugin for IntelliJ]: ./hdinsight/hdinsight-apache-spark-intellij-tool-plugin.md
