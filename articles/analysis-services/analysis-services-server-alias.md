---
title: Azure Analysis Services alias server names | Microsoft Docs
description: Describes how to create and use server name aliases.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: d0aebbe115be9e9af697b5d93d158a263fefe55c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857395"
---
# <a name="alias-server-names"></a><span data-ttu-id="e7233-103">Alias server names</span><span class="sxs-lookup"><span data-stu-id="e7233-103">Alias server names</span></span>

<span data-ttu-id="e7233-104">By using a server name alias, users can connect to your Azure Analysis Services server with a shorter *alias* instead of the server name.</span><span class="sxs-lookup"><span data-stu-id="e7233-104">By using a server name alias, users can connect to your Azure Analysis Services server with a shorter *alias* instead of the server name.</span></span> <span data-ttu-id="e7233-105">When connecting from a client application, the alias is specified as an endpoint using the **link://** protocol format.</span><span class="sxs-lookup"><span data-stu-id="e7233-105">When connecting from a client application, the alias is specified as an endpoint using the **link://** protocol format.</span></span> <span data-ttu-id="e7233-106">The endpoint then returns the real server name in order to connect.</span><span class="sxs-lookup"><span data-stu-id="e7233-106">The endpoint then returns the real server name in order to connect.</span></span>

<span data-ttu-id="e7233-107">Alias server names are good for:</span><span class="sxs-lookup"><span data-stu-id="e7233-107">Alias server names are good for:</span></span>

- <span data-ttu-id="e7233-108">Migrating models between servers without affecting users.</span><span class="sxs-lookup"><span data-stu-id="e7233-108">Migrating models between servers without affecting users.</span></span> 
- <span data-ttu-id="e7233-109">Friendly server names are easier for users to remember.</span><span class="sxs-lookup"><span data-stu-id="e7233-109">Friendly server names are easier for users to remember.</span></span> 
- <span data-ttu-id="e7233-110">Direct users to different servers at different times of the day.</span><span class="sxs-lookup"><span data-stu-id="e7233-110">Direct users to different servers at different times of the day.</span></span> 
- <span data-ttu-id="e7233-111">Direct users in different regions to instances that are geographically closer, like when using Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="e7233-111">Direct users in different regions to instances that are geographically closer, like when using Azure Traffic Manager.</span></span> 

<span data-ttu-id="e7233-112">Any HTTPS endpoint that returns a valid Azure Analysis Services server name can serve as an alias.</span><span class="sxs-lookup"><span data-stu-id="e7233-112">Any HTTPS endpoint that returns a valid Azure Analysis Services server name can serve as an alias.</span></span> <span data-ttu-id="e7233-113">The endpoint must support HTTPS over port 443 and the port must not be specified in the URI.</span><span class="sxs-lookup"><span data-stu-id="e7233-113">The endpoint must support HTTPS over port 443 and the port must not be specified in the URI.</span></span>

![Alias using link format](media/analysis-services-alias/aas-alias-browser.png)

<span data-ttu-id="e7233-115">When connecting from a client, the alias server name is entered using **link://** protocol format.</span><span class="sxs-lookup"><span data-stu-id="e7233-115">When connecting from a client, the alias server name is entered using **link://** protocol format.</span></span> <span data-ttu-id="e7233-116">For example, in Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="e7233-116">For example, in Power BI Desktop:</span></span>

![Power BI Desktop connection](media/analysis-services-alias/aas-alias-connect-pbid.png)

## <a name="create-an-alias"></a><span data-ttu-id="e7233-118">Create an alias</span><span class="sxs-lookup"><span data-stu-id="e7233-118">Create an alias</span></span>

<span data-ttu-id="e7233-119">To create an alias endpoint, you can use any method that returns a valid Azure Analysis Services server name.</span><span class="sxs-lookup"><span data-stu-id="e7233-119">To create an alias endpoint, you can use any method that returns a valid Azure Analysis Services server name.</span></span> <span data-ttu-id="e7233-120">For example, a reference to a file in Azure Blob Storage containing the real server name, or create and publish an ASP.NET Web Forms application.</span><span class="sxs-lookup"><span data-stu-id="e7233-120">For example, a reference to a file in Azure Blob Storage containing the real server name, or create and publish an ASP.NET Web Forms application.</span></span>

<span data-ttu-id="e7233-121">In this example, an ASP.NET Web Forms Application is created in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e7233-121">In this example, an ASP.NET Web Forms Application is created in Visual Studio.</span></span> <span data-ttu-id="e7233-122">The master page reference and user control are removed from the Default.aspx page.</span><span class="sxs-lookup"><span data-stu-id="e7233-122">The master page reference and user control are removed from the Default.aspx page.</span></span> <span data-ttu-id="e7233-123">The contents of Default.aspx are simply the following Page directive:</span><span class="sxs-lookup"><span data-stu-id="e7233-123">The contents of Default.aspx are simply the following Page directive:</span></span>

```
<%@ Page Title="Home Page" Language="C#" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="FriendlyRedirect._Default" %>
```

<span data-ttu-id="e7233-124">The Page_Load event in Default.aspx.cs uses the Response.Write() method to return the Azure Analysis Services server name.</span><span class="sxs-lookup"><span data-stu-id="e7233-124">The Page_Load event in Default.aspx.cs uses the Response.Write() method to return the Azure Analysis Services server name.</span></span>

```
protected void Page_Load(object sender, EventArgs e)
{
    this.Response.Write("asazure://<region>.asazure.windows.net/<servername>");
}
```

## <a name="see-also"></a><span data-ttu-id="e7233-125">See also</span><span class="sxs-lookup"><span data-stu-id="e7233-125">See also</span></span>

<span data-ttu-id="e7233-126">[Client libraries](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="e7233-126">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="e7233-127">Connect from Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="e7233-127">Connect from Power BI Desktop</span></span>](analysis-services-connect-pbi.md)
