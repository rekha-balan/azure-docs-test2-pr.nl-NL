---
title: The structure of Azure Dashboards | Microsoft Docs
description: This article explains the JSON structure of an Azure Dashboard
services: azure-portal
documentationcenter: ''
author: adamabmsft
manager: dougeby
editor: tysonn
ms.service: azure-portal
ms.devlang: NA
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/01/2017
ms.author: adamab
ms.openlocfilehash: 2eb9289957968db04b78087413fb9df8ed1b085b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965949"
---
# <a name="the-structure-of-azure-dashboards"></a><span data-ttu-id="ab1c9-103">The structure of Azure Dashboards</span><span class="sxs-lookup"><span data-stu-id="ab1c9-103">The structure of Azure Dashboards</span></span>
<span data-ttu-id="ab1c9-104">This document walks through the structure of an Azure dashboard, using the following dashboard as an example:</span><span class="sxs-lookup"><span data-stu-id="ab1c9-104">This document walks through the structure of an Azure dashboard, using the following dashboard as an example:</span></span>

![sample dashboard](./media/azure-portal-dashboards-structure/sample-dashboard.png)

<span data-ttu-id="ab1c9-106">Since shared [Azure dashboards are resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), this dashboard can be represented as JSON.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-106">Since shared [Azure dashboards are resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview), this dashboard can be represented as JSON.</span></span>  <span data-ttu-id="ab1c9-107">The following JSON represents the dashboard visualized above.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-107">The following JSON represents the dashboard visualized above.</span></span>

```json

{
    "properties": {
        "lenses": {
            "0": {
                "order": 0,
                "parts": {
                    "0": {
                        "position": {
                            "x": 0,
                            "y": 0,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "content": "## Azure Virtual Machines Overview\r\nNew team members should watch this video to get familiar with Azure Virtual Machines.",
                                        "title": "",
                                        "subtitle": ""
                                    }
                                }
                            }
                        }
                    },
                    "1": {
                        "position": {
                            "x": 3,
                            "y": 0,
                            "rowSpan": 4,
                            "colSpan": 8
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "content": "This is the team dashboard for the test VM we use on our team. Here are some useful links:\r\n\r\n1. [Getting started](https://www.contoso.com/tsgs)\r\n1. [Troubleshooting guide](https://www.contoso.com/tsgs)\r\n1. [Architecture docs](https://www.contoso.com/tsgs)",
                                        "title": "Test VM Dashboard",
                                        "subtitle": "Contoso"
                                    }
                                }
                            }
                        }
                    },
                    "2": {
                        "position": {
                            "x": 0,
                            "y": 2,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [],
                            "type": "Extension[azure]/HubsExtension/PartType/VideoPart",
                            "settings": {
                                "content": {
                                    "settings": {
                                        "title": "",
                                        "subtitle": "",
                                        "src": "https://www.youtube.com/watch?v=YcylDIiKaSU&list=PLLasX02E8BPCsnETz0XAMfpLR1LIBqpgs&index=4",
                                        "autoplay": false
                                    }
                                }
                            }
                        }
                    },
                    "3": {
                        "position": {
                            "x": 0,
                            "y": 4,
                            "rowSpan": 3,
                            "colSpan": 11
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Percentage CPU",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "4": {
                        "position": {
                            "x": 0,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Disk Read Operations/Sec",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Disk Write Operations/Sec",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "5": {
                        "position": {
                            "x": 3,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Disk Read Bytes",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Disk Write Bytes",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "6": {
                        "position": {
                            "x": 6,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 3
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "queryInputs",
                                    "value": {
                                        "timespan": {
                                            "duration": "PT1H",
                                            "start": null,
                                            "end": null
                                        },
                                        "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
                                        "chartType": 0,
                                        "metrics": [
                                            {
                                                "name": "Network In",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            },
                                            {
                                                "name": "Network Out",
                                                "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                            }
                                        ]
                                    }
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart",
                            "settings": {}
                        }
                    },
                    "7": {
                        "position": {
                            "x": 9,
                            "y": 7,
                            "rowSpan": 2,
                            "colSpan": 2
                        },
                        "metadata": {
                            "inputs": [
                                {
                                    "name": "id",
                                    "value": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                                }
                            ],
                            "type": "Extension/Microsoft_Azure_Compute/PartType/VirtualMachinePart",
                            "asset": {
                                "idInputName": "id",
                                "type": "VirtualMachine"
                            },
                            "defaultMenuItemId": "overview"
                        }
                    }
                }
            }
        },
        "metadata": {
            "model": {
                "timeRange": {
                    "value": {
                        "relative": {
                            "duration": 24,
                            "timeUnit": 1
                        }
                    },
                    "type": "MsPortalFx.Composition.Configuration.ValueTypes.TimeRange"
                }
            }
        }
    },
    "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/dashboards/providers/Microsoft.Portal/dashboards/aa9786ae-e159-483f-b05f-1f7f767741a9",
    "name": "aa9786ae-e159-483f-b05f-1f7f767741a9",
    "type": "Microsoft.Portal/dashboards",
    "location": "eastasia",
    "tags": {
        "hidden-title": "Created via API"
    }
}

```

## <a name="common-resource-properties"></a><span data-ttu-id="ab1c9-108">Common resource properties</span><span class="sxs-lookup"><span data-stu-id="ab1c9-108">Common resource properties</span></span>

<span data-ttu-id="ab1c9-109">Let’s break down the relevant sections of the JSON.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-109">Let’s break down the relevant sections of the JSON.</span></span>  <span data-ttu-id="ab1c9-110">The top-level properties, __id__, __name__, __type__, __location__, and __tags__ properties are shared across all Azure resource types.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-110">The top-level properties, __id__, __name__, __type__, __location__, and __tags__ properties are shared across all Azure resource types.</span></span> <span data-ttu-id="ab1c9-111">That is, they don’t have much to do with the dashboard’s content.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-111">That is, they don’t have much to do with the dashboard’s content.</span></span>

### <a name="the-id-property"></a><span data-ttu-id="ab1c9-112">The id property</span><span class="sxs-lookup"><span data-stu-id="ab1c9-112">The id property</span></span>

<span data-ttu-id="ab1c9-113">The Azure resource id, subject to the [naming conventions of Azure resources](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="ab1c9-113">The Azure resource id, subject to the [naming conventions of Azure resources](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> <span data-ttu-id="ab1c9-114">When the portal creates a dashboard it generally chooses an id in the form of a guid, but you are free to use any valid name when you create them programmatically.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-114">When the portal creates a dashboard it generally chooses an id in the form of a guid, but you are free to use any valid name when you create them programmatically.</span></span> 

### <a name="the-name-property"></a><span data-ttu-id="ab1c9-115">The name property</span><span class="sxs-lookup"><span data-stu-id="ab1c9-115">The name property</span></span>
<span data-ttu-id="ab1c9-116">The name is the segment of the resource Id that does not include the subscription, resource type, or resource group information.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-116">The name is the segment of the resource Id that does not include the subscription, resource type, or resource group information.</span></span> <span data-ttu-id="ab1c9-117">Essentially, it is the last segment of the resource id.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-117">Essentially, it is the last segment of the resource id.</span></span>

### <a name="the-type-property"></a><span data-ttu-id="ab1c9-118">The type property</span><span class="sxs-lookup"><span data-stu-id="ab1c9-118">The type property</span></span>
<span data-ttu-id="ab1c9-119">All dashboards are of type __Microsoft.Portal/dashboards__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-119">All dashboards are of type __Microsoft.Portal/dashboards__.</span></span>

### <a name="the-location-property"></a><span data-ttu-id="ab1c9-120">The location property</span><span class="sxs-lookup"><span data-stu-id="ab1c9-120">The location property</span></span>
<span data-ttu-id="ab1c9-121">Unlike other resources, dashboards don’t have a runtime component.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-121">Unlike other resources, dashboards don’t have a runtime component.</span></span>  <span data-ttu-id="ab1c9-122">For dashboards, the location indicates the primary geographic location that stores the dashboard’s JSON representation.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-122">For dashboards, the location indicates the primary geographic location that stores the dashboard’s JSON representation.</span></span> <span data-ttu-id="ab1c9-123">The value should be one of the location codes that can be fetched using the [locations API on the subscriptions resource](https://docs.microsoft.com/rest/api/resources/subscriptions).</span><span class="sxs-lookup"><span data-stu-id="ab1c9-123">The value should be one of the location codes that can be fetched using the [locations API on the subscriptions resource](https://docs.microsoft.com/rest/api/resources/subscriptions).</span></span>

### <a name="the-tags-property"></a><span data-ttu-id="ab1c9-124">The tags property</span><span class="sxs-lookup"><span data-stu-id="ab1c9-124">The tags property</span></span>
<span data-ttu-id="ab1c9-125">Tags are a common feature of Azure resources that let you organize your resource by arbitrary name value pairs.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-125">Tags are a common feature of Azure resources that let you organize your resource by arbitrary name value pairs.</span></span> <span data-ttu-id="ab1c9-126">For dashboards, there is one special tag called __hidden-title__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-126">For dashboards, there is one special tag called __hidden-title__.</span></span> <span data-ttu-id="ab1c9-127">If your dashboard has this property populated, then it is used as the display name for your dashboard in the portal.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-127">If your dashboard has this property populated, then it is used as the display name for your dashboard in the portal.</span></span> <span data-ttu-id="ab1c9-128">Azure resource Ids cannot be renamed, but tags can.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-128">Azure resource Ids cannot be renamed, but tags can.</span></span> <span data-ttu-id="ab1c9-129">This tag gives you a way to have a renamable display name for your dashboard.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-129">This tag gives you a way to have a renamable display name for your dashboard.</span></span>

`"tags": { "hidden-title": "Created via API" }`

### <a name="the-properties-object"></a><span data-ttu-id="ab1c9-130">The properties object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-130">The properties object</span></span>
<span data-ttu-id="ab1c9-131">The properties object contains two properties, __lenses__ and __metadata__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-131">The properties object contains two properties, __lenses__ and __metadata__.</span></span> <span data-ttu-id="ab1c9-132">The __lenses__ property contains information about the tiles (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-132">The __lenses__ property contains information about the tiles (a.k.a.</span></span> <span data-ttu-id="ab1c9-133">parts) on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-133">parts) on the dashboard.</span></span>  <span data-ttu-id="ab1c9-134">The __metadata__ property is there for potential future features.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-134">The __metadata__ property is there for potential future features.</span></span>

### <a name="the-lenses-property"></a><span data-ttu-id="ab1c9-135">The lenses property</span><span class="sxs-lookup"><span data-stu-id="ab1c9-135">The lenses property</span></span>
<span data-ttu-id="ab1c9-136">The __lenses__ property contains the dashboard.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-136">The __lenses__ property contains the dashboard.</span></span> <span data-ttu-id="ab1c9-137">Note that the lenses object in this example contains a single property called “0”.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-137">Note that the lenses object in this example contains a single property called “0”.</span></span> <span data-ttu-id="ab1c9-138">Lenses are a grouping concept that is not currently implemented in dashboards.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-138">Lenses are a grouping concept that is not currently implemented in dashboards.</span></span> <span data-ttu-id="ab1c9-139">For now, all of your dashboards have this single property on the lens object, again, called “0”.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-139">For now, all of your dashboards have this single property on the lens object, again, called “0”.</span></span>

### <a name="the-lens-object"></a><span data-ttu-id="ab1c9-140">The lens object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-140">The lens object</span></span>
<span data-ttu-id="ab1c9-141">The object underneath the “0” contains two properties, __order__ and __parts__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-141">The object underneath the “0” contains two properties, __order__ and __parts__.</span></span>  <span data-ttu-id="ab1c9-142">In the current version of dashboards, __order__ is always 0.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-142">In the current version of dashboards, __order__ is always 0.</span></span> <span data-ttu-id="ab1c9-143">The __parts__ property contains an object that defines the individual parts (a.k.a.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-143">The __parts__ property contains an object that defines the individual parts (a.k.a.</span></span> <span data-ttu-id="ab1c9-144">tiles) on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-144">tiles) on the dashboard.</span></span>

<span data-ttu-id="ab1c9-145">The __parts__ object contains a property for each part, where the name of the property is a number.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-145">The __parts__ object contains a property for each part, where the name of the property is a number.</span></span> <span data-ttu-id="ab1c9-146">This number is not significant.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-146">This number is not significant.</span></span> 

### <a name="the-part-object"></a><span data-ttu-id="ab1c9-147">The part object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-147">The part object</span></span>
<span data-ttu-id="ab1c9-148">Each individual part object has a __position__, and __metadata__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-148">Each individual part object has a __position__, and __metadata__.</span></span>

### <a name="the-position-object"></a><span data-ttu-id="ab1c9-149">The position object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-149">The position object</span></span>
<span data-ttu-id="ab1c9-150">The __position__ property contains the size and location information for the part expressed as __x__, __y__, __rowSpan__, and __colSpan__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-150">The __position__ property contains the size and location information for the part expressed as __x__, __y__, __rowSpan__, and __colSpan__.</span></span> <span data-ttu-id="ab1c9-151">The values are in terms of grid units.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-151">The values are in terms of grid units.</span></span> <span data-ttu-id="ab1c9-152">These grid units are visible when the dashboard is in the customize mode as shown here.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-152">These grid units are visible when the dashboard is in the customize mode as shown here.</span></span> <span data-ttu-id="ab1c9-153">If you want a tile to have a width of two grid units, a height of one grid unit, and a location in the top left corner of the dashboard then the position obejct looks like this:</span><span class="sxs-lookup"><span data-stu-id="ab1c9-153">If you want a tile to have a width of two grid units, a height of one grid unit, and a location in the top left corner of the dashboard then the position obejct looks like this:</span></span>

`location: { x: 0, y: 0, rowSpan: 2, colSpan: 1 }`

![grid-units](./media/azure-portal-dashboards-structure/grid-units.png)

### <a name="the-metadata-object"></a><span data-ttu-id="ab1c9-155">The metadata object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-155">The metadata object</span></span>
<span data-ttu-id="ab1c9-156">Each part has a metadata property, an object has only one required property called __type__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-156">Each part has a metadata property, an object has only one required property called __type__.</span></span> <span data-ttu-id="ab1c9-157">This string tells the portal which tile to show.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-157">This string tells the portal which tile to show.</span></span> <span data-ttu-id="ab1c9-158">Our example dashboard uses these types of tiles:</span><span class="sxs-lookup"><span data-stu-id="ab1c9-158">Our example dashboard uses these types of tiles:</span></span>


1. <span data-ttu-id="ab1c9-159">`Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart` – Used to show monitoring metrics</span><span class="sxs-lookup"><span data-stu-id="ab1c9-159">`Extension/Microsoft_Azure_Monitoring/PartType/MetricsChartPart` – Used to show monitoring metrics</span></span>
1. <span data-ttu-id="ab1c9-160">`Extension[azure]/HubsExtension/PartType/MarkdownPart` – Used to show with text or images with basic formatting for lists, links, etc.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-160">`Extension[azure]/HubsExtension/PartType/MarkdownPart` – Used to show with text or images with basic formatting for lists, links, etc.</span></span>
1. <span data-ttu-id="ab1c9-161">`Extension[azure]/HubsExtension/PartType/VideoPart` – Used to show videos from YouTube, Channel9, and any other type of video that works in an html video tag.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-161">`Extension[azure]/HubsExtension/PartType/VideoPart` – Used to show videos from YouTube, Channel9, and any other type of video that works in an html video tag.</span></span>
1. <span data-ttu-id="ab1c9-162">`Extension/Microsoft_Azure_Compute/PartType/VirtualMachinePart` – Used to show the name and status of an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-162">`Extension/Microsoft_Azure_Compute/PartType/VirtualMachinePart` – Used to show the name and status of an Azure virtual machine.</span></span>

<span data-ttu-id="ab1c9-163">Each type of part has its own configuration.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-163">Each type of part has its own configuration.</span></span> <span data-ttu-id="ab1c9-164">The possible configuration properties are called __inputs__, __settings__, and __asset__.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-164">The possible configuration properties are called __inputs__, __settings__, and __asset__.</span></span> 

### <a name="the-inputs-object"></a><span data-ttu-id="ab1c9-165">The inputs object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-165">The inputs object</span></span>
<span data-ttu-id="ab1c9-166">The inputs object generally contains information that binds a tile to a resource instance.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-166">The inputs object generally contains information that binds a tile to a resource instance.</span></span>  <span data-ttu-id="ab1c9-167">The virtual machine part in our sample dashboard contains a single input that uses the Azure resource id to express the binding.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-167">The virtual machine part in our sample dashboard contains a single input that uses the Azure resource id to express the binding.</span></span>  <span data-ttu-id="ab1c9-168">This resource id format is consistent across all Azure resources.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-168">This resource id format is consistent across all Azure resources.</span></span>

```json
"inputs":
[
    {
        "name": "id",
        "value": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
    }
]

```
<span data-ttu-id="ab1c9-169">The metrics chart part has a single input that expresses the resource to bind to, as well as information about the metric(s) being displayed.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-169">The metrics chart part has a single input that expresses the resource to bind to, as well as information about the metric(s) being displayed.</span></span> <span data-ttu-id="ab1c9-170">Here is the input for the tile that’s showing the Network In and Network Out metrics.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-170">Here is the input for the tile that’s showing the Network In and Network Out metrics.</span></span>

```json
“inputs”:
[
    {
        "name": "queryInputs",
        "value": 
        {
            "timespan": 
            {
                "duration": "PT1H",
                "start": null,
                "end": null
           },
            "id": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1",
            "chartType": 0,
            "metrics": 
            [
                {
                    "name": "Network In",
                    "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                },
                {
                    "name": "Network Out",
                    "resourceId": "/subscriptions/6531c8c8-df32-4254-d717-b6e983273e5d/resourceGroups/contoso/providers/Microsoft.Compute/virtualMachines/myVM1"
                }
            ]
        }
    }
]

```

### <a name="the-settings-object"></a><span data-ttu-id="ab1c9-171">The settings object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-171">The settings object</span></span>
<span data-ttu-id="ab1c9-172">The settings object contains the configurable elements of a part.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-172">The settings object contains the configurable elements of a part.</span></span>  <span data-ttu-id="ab1c9-173">In our sample dashboard, the Markdown part uses settings to store the custom markdown content as well as a configurable title and subtitle.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-173">In our sample dashboard, the Markdown part uses settings to store the custom markdown content as well as a configurable title and subtitle.</span></span>

```json
"settings": 
{
    "content": 
    {
        "settings": 
        {
            "content": "This is the team dashboard for the test VM we use on our team. Here are some useful links:\r\n\r\n1. [Getting started](https://www.contoso.com/tsgs)\r\n1. [Troubleshooting guide](https://www.contoso.com/tsgs)\r\n1. [Architecture docs](https://www.contoso.com/tsgs)",
            "title": "Test VM Dashboard",
            "subtitle": "Contoso"
        }
    }
}

```

<span data-ttu-id="ab1c9-174">Similarly, the video tile has its own settings that contain a pointer to the video to play, an autoplay setting, and optional title information.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-174">Similarly, the video tile has its own settings that contain a pointer to the video to play, an autoplay setting, and optional title information.</span></span>

```json
"settings": 
{
   "content": 
    {
        "settings": 
        {
            "title": "",
            "subtitle": "",
            "src": "https://www.youtube.com/watch?v=YcylDIiKaSU&list=PLLasX02E8BPCsnETz0XAMfpLR1LIBqpgs&index=4",
            "autoplay": false
        }
    }
}

```

### <a name="the-asset-object"></a><span data-ttu-id="ab1c9-175">The asset object</span><span class="sxs-lookup"><span data-stu-id="ab1c9-175">The asset object</span></span>
<span data-ttu-id="ab1c9-176">Tiles that are bound to first class manageable portal objects (called assets) have this relationship expressed via the asset object.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-176">Tiles that are bound to first class manageable portal objects (called assets) have this relationship expressed via the asset object.</span></span>  <span data-ttu-id="ab1c9-177">In our example dashboard, the virtual machine tile contains this asset description.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-177">In our example dashboard, the virtual machine tile contains this asset description.</span></span>  <span data-ttu-id="ab1c9-178">The __idInputName__ property tells the portal that the id input contains the unique identifier for the asset, in this case the resource id. Most Azure resource types have assets defined in the portal.</span><span class="sxs-lookup"><span data-stu-id="ab1c9-178">The __idInputName__ property tells the portal that the id input contains the unique identifier for the asset, in this case the resource id. Most Azure resource types have assets defined in the portal.</span></span>

`"asset": {    "idInputName": "id",    "type": "VirtualMachine"    }`