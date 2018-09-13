---
title: Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java
description: How to display the Javadoc content for the Azure Libraries in Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 12/22/2016
ms.author: robmcm
ms.openlocfilehash: 871afe3ec0def802cd81ddeb54c23750efa776fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562927"
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="d5e0d-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span><span class="sxs-lookup"><span data-stu-id="d5e0d-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>
<span data-ttu-id="d5e0d-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="d5e0d-105">The following steps show you how to use this functionality within Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="d5e0d-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="d5e0d-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span><span class="sxs-lookup"><span data-stu-id="d5e0d-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>
* <span data-ttu-id="d5e0d-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="d5e0d-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span><span class="sxs-lookup"><span data-stu-id="d5e0d-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>
* <span data-ttu-id="d5e0d-110">Click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-110">Click **Properties**.</span></span>
* <span data-ttu-id="d5e0d-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="d5e0d-112">The **Javadoc Location** dialog is displayed.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-112">The **Javadoc Location** dialog is displayed.</span></span>
* <span data-ttu-id="d5e0d-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>
  * <span data-ttu-id="d5e0d-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>
  * <span data-ttu-id="d5e0d-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>
    <span data-ttu-id="d5e0d-116">Make your choice and browse/validate as needed.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="d5e0d-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>
    ![][ic553487]
* <span data-ttu-id="d5e0d-118">*Optional*: Click **Validate**.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-118">*Optional*: Click **Validate**.</span></span> <span data-ttu-id="d5e0d-119">Potential issues with the Javadoc JAR could be displayed here.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-119">Potential issues with the Javadoc JAR could be displayed here.</span></span>
* <span data-ttu-id="d5e0d-120">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-120">Click **OK**.</span></span>

<span data-ttu-id="d5e0d-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="d5e0d-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="d5e0d-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span><span class="sxs-lookup"><span data-stu-id="d5e0d-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="d5e0d-123">See Also</span><span class="sxs-lookup"><span data-stu-id="d5e0d-123">See Also</span></span>
<span data-ttu-id="d5e0d-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d5e0d-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="d5e0d-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d5e0d-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="d5e0d-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="d5e0d-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="d5e0d-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="d5e0d-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->


