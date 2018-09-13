---
title: Download the Azure SDK for Java | Microsoft Docs
description: Learn how to download the Azure SDK for Java, with sample code provided for Maven projects.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 4b8f8fe6-1b26-4bb4-9be9-6ae757a59e66
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm;asirveda
ms.openlocfilehash: 9e55eb52797f1363cbb65050574e549c575ca5d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662954"
---
# <a name="download-the-azure-sdk-for-java"></a><span data-ttu-id="294c7-103">Download the Azure SDK for Java</span><span class="sxs-lookup"><span data-stu-id="294c7-103">Download the Azure SDK for Java</span></span>
<span data-ttu-id="294c7-104">This article contains instructions for downloading and installing the Azure Management Libraries for Java.</span><span class="sxs-lookup"><span data-stu-id="294c7-104">This article contains instructions for downloading and installing the Azure Management Libraries for Java.</span></span>

> [!NOTE]
> <span data-ttu-id="294c7-105">The Azure Management Libraries for Java are distributed under the [Apache License, Version 2.0][license].</span><span class="sxs-lookup"><span data-stu-id="294c7-105">The Azure Management Libraries for Java are distributed under the [Apache License, Version 2.0][license].</span></span>
>

## <a name="azure-libraries-for-java---manual-download"></a><span data-ttu-id="294c7-106">Azure Libraries for Java - Manual Download</span><span class="sxs-lookup"><span data-stu-id="294c7-106">Azure Libraries for Java - Manual Download</span></span>
<span data-ttu-id="294c7-107">To manually install the Azure Management Libraries for Java, click <http://go.microsoft.com/fwlink/?LinkId=690320> to download a ZIP file which contains all of the libraries and all dependencies.</span><span class="sxs-lookup"><span data-stu-id="294c7-107">To manually install the Azure Management Libraries for Java, click <http://go.microsoft.com/fwlink/?LinkId=690320> to download a ZIP file which contains all of the libraries and all dependencies.</span></span>

<span data-ttu-id="294c7-108">Once you have downloaded the zip file to your computer, extract the contents and use one of the following options to add the JAR files to your project:</span><span class="sxs-lookup"><span data-stu-id="294c7-108">Once you have downloaded the zip file to your computer, extract the contents and use one of the following options to add the JAR files to your project:</span></span>

* <span data-ttu-id="294c7-109">Import the JAR files into your Java project in Eclipse or IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="294c7-109">Import the JAR files into your Java project in Eclipse or IntelliJ.</span></span>
* <span data-ttu-id="294c7-110">Configure the build paths for your Java projects in Eclipse or IntelliJ to include the path to the JAR files.</span><span class="sxs-lookup"><span data-stu-id="294c7-110">Configure the build paths for your Java projects in Eclipse or IntelliJ to include the path to the JAR files.</span></span>

> [!NOTE]
> <span data-ttu-id="294c7-111">See the license.txt and ThirdPartyNotices.txt file inside the ZIP for license and other information.</span><span class="sxs-lookup"><span data-stu-id="294c7-111">See the license.txt and ThirdPartyNotices.txt file inside the ZIP for license and other information.</span></span>
>

## <a name="azure-management-libraries-for-java---building-with-maven"></a><span data-ttu-id="294c7-112">Azure Management Libraries for Java - Building with Maven</span><span class="sxs-lookup"><span data-stu-id="294c7-112">Azure Management Libraries for Java - Building with Maven</span></span>
### <a name="step-1---set-up-your-project-to-use-maven-for-build"></a><span data-ttu-id="294c7-113">Step 1 - Set up your project to use Maven for build</span><span class="sxs-lookup"><span data-stu-id="294c7-113">Step 1 - Set up your project to use Maven for build</span></span>
<span data-ttu-id="294c7-114">To create Maven projects in Eclipse which use the Azure Management Libraries for Java, following the instructions in the [Getting Started with Azure Management Libraries for Java][maven-getting-started] article.</span><span class="sxs-lookup"><span data-stu-id="294c7-114">To create Maven projects in Eclipse which use the Azure Management Libraries for Java, following the instructions in the [Getting Started with Azure Management Libraries for Java][maven-getting-started] article.</span></span>

### <a name="step-2---configure-your-maven-settings-with-the-requisite-dependencies"></a><span data-ttu-id="294c7-115">Step 2 - Configure your Maven settings with the requisite dependencies</span><span class="sxs-lookup"><span data-stu-id="294c7-115">Step 2 - Configure your Maven settings with the requisite dependencies</span></span>
<span data-ttu-id="294c7-116">Once your project has been configured to use Maven for build, you can add the requisite dependencies to your pom.xml file using syntax like the following example.</span><span class="sxs-lookup"><span data-stu-id="294c7-116">Once your project has been configured to use Maven for build, you can add the requisite dependencies to your pom.xml file using syntax like the following example.</span></span> <span data-ttu-id="294c7-117">Note that you do not need to add every dependency that is listed in the following example; you only need to add the specific dependencies which your project requires.</span><span class="sxs-lookup"><span data-stu-id="294c7-117">Note that you do not need to add every dependency that is listed in the following example; you only need to add the specific dependencies which your project requires.</span></span>

> [!NOTE]
> <span data-ttu-id="294c7-118">Within each `<version>` element in the following sample, replace the "n.n.n" placeholders in this example with valid version numbers, which can be obtained from the [Azure Libraries Repository on Maven].</span><span class="sxs-lookup"><span data-stu-id="294c7-118">Within each `<version>` element in the following sample, replace the "n.n.n" placeholders in this example with valid version numbers, which can be obtained from the [Azure Libraries Repository on Maven].</span></span>
>
>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-compute</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-network</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-sql</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-storage</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-websites</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-svc-mgmt-media</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-servicebus</artifactId>
        <version>n.n.n</version>
    </dependency>
    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-serviceruntime</artifactId>
        <version>n.n.n</version>
    </dependency>

## <a name="see-also"></a><span data-ttu-id="294c7-119">See Also</span><span class="sxs-lookup"><span data-stu-id="294c7-119">See Also</span></span>
<span data-ttu-id="294c7-120">For more information about the Azure Toolkits for Java IDEs, see the following links:</span><span class="sxs-lookup"><span data-stu-id="294c7-120">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="294c7-121">[Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="294c7-121">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="294c7-122">[Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="294c7-122">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="294c7-123">[Create a Hello World Web App for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="294c7-123">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="294c7-124">[What's New in the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="294c7-124">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="294c7-125">[Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="294c7-125">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="294c7-126">[Installing the Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="294c7-126">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="294c7-127">[Create a Hello World Web App for Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="294c7-127">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="294c7-128">[What's New in the Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="294c7-128">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="294c7-129">For more information about using Azure with Java, see the [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="294c7-129">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

> [!NOTE]
> <span data-ttu-id="294c7-130">For detailed information on setting up build paths in Eclipse, see the [Java Build Path] article at the Eclipse website.</span><span class="sxs-lookup"><span data-stu-id="294c7-130">For detailed information on setting up build paths in Eclipse, see the [Java Build Path] article at the Eclipse website.</span></span>
>

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
[Azure Libraries Repository on Maven]: http://go.microsoft.com/fwlink/?LinkID=286274
[Java Build Path]: http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Freference%2Fref-properties-build-path.htm
[license]: http://www.apache.org/licenses/LICENSE-2.0.html
[maven-getting-started]: http://go.microsoft.com/fwlink/?LinkID=622998
