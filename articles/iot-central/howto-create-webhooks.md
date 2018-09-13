---
title: Create webhooks on rules in Azure IoT Central | Microsoft Docs
description: Create webhooks in Azure IoT Central to automatically notify other applications when rules fire.
author: viv-liu
ms.author: viviali
ms.date: 07/17/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 1e21076cafe21e6c0efcdf5a8146278eabd9ebc4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867890"
---
# <a name="create-webhook-actions-on-rules-in-azure-iot-central"></a><span data-ttu-id="abfc0-103">Create webhook actions on rules in Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="abfc0-103">Create webhook actions on rules in Azure IoT Central</span></span>

<span data-ttu-id="abfc0-104">Webhooks enable you to connect your IoT Central app to other applications and services for remote monitoring and notifications.</span><span class="sxs-lookup"><span data-stu-id="abfc0-104">Webhooks enable you to connect your IoT Central app to other applications and services for remote monitoring and notifications.</span></span> <span data-ttu-id="abfc0-105">Webhooks automatically notify other applications and services you connect whenever a rule is triggered in your IoT Central app.</span><span class="sxs-lookup"><span data-stu-id="abfc0-105">Webhooks automatically notify other applications and services you connect whenever a rule is triggered in your IoT Central app.</span></span> <span data-ttu-id="abfc0-106">Your IoT Central app will send a POST request to the other application's HTTP endpoint whenever a rule is triggered.</span><span class="sxs-lookup"><span data-stu-id="abfc0-106">Your IoT Central app will send a POST request to the other application's HTTP endpoint whenever a rule is triggered.</span></span> <span data-ttu-id="abfc0-107">The payload will contain device details and rule trigger details.</span><span class="sxs-lookup"><span data-stu-id="abfc0-107">The payload will contain device details and rule trigger details.</span></span> 

## <a name="how-to-set-up-the-webhook"></a><span data-ttu-id="abfc0-108">How to set up the webhook</span><span class="sxs-lookup"><span data-stu-id="abfc0-108">How to set up the webhook</span></span>
<span data-ttu-id="abfc0-109">In this example, you will connect to RequestBin to get notified when rules fire using webhooks.</span><span class="sxs-lookup"><span data-stu-id="abfc0-109">In this example, you will connect to RequestBin to get notified when rules fire using webhooks.</span></span> 

1. <span data-ttu-id="abfc0-110">Open [RequestBin](http://requestbin.net/).</span><span class="sxs-lookup"><span data-stu-id="abfc0-110">Open [RequestBin](http://requestbin.net/).</span></span> 
1. <span data-ttu-id="abfc0-111">Create a new RequestBin and copy the **Bin URL**.</span><span class="sxs-lookup"><span data-stu-id="abfc0-111">Create a new RequestBin and copy the **Bin URL**.</span></span> 
1. <span data-ttu-id="abfc0-112">Create a [telemetry rule](howto-create-telemetry-rules.md) or an [event rule](howto-create-event-rules.md).</span><span class="sxs-lookup"><span data-stu-id="abfc0-112">Create a [telemetry rule](howto-create-telemetry-rules.md) or an [event rule](howto-create-event-rules.md).</span></span> <span data-ttu-id="abfc0-113">Save the rule and add a new action.</span><span class="sxs-lookup"><span data-stu-id="abfc0-113">Save the rule and add a new action.</span></span>
<span data-ttu-id="abfc0-114">![Webhook creation screen](media/howto-create-webhooks/webhookcreate.png)</span><span class="sxs-lookup"><span data-stu-id="abfc0-114">![Webhook creation screen](media/howto-create-webhooks/webhookcreate.png)</span></span>
1. <span data-ttu-id="abfc0-115">Choose the webhook action and provide a display name and paste the Bin URL as the Callback URL.</span><span class="sxs-lookup"><span data-stu-id="abfc0-115">Choose the webhook action and provide a display name and paste the Bin URL as the Callback URL.</span></span> 
1. <span data-ttu-id="abfc0-116">Save the rule</span><span class="sxs-lookup"><span data-stu-id="abfc0-116">Save the rule</span></span>

<span data-ttu-id="abfc0-117">Now when the rule fires, you should see a new request appear in RequestBin.</span><span class="sxs-lookup"><span data-stu-id="abfc0-117">Now when the rule fires, you should see a new request appear in RequestBin.</span></span>

## <a name="payload"></a><span data-ttu-id="abfc0-118">Payload</span><span class="sxs-lookup"><span data-stu-id="abfc0-118">Payload</span></span>
<span data-ttu-id="abfc0-119">When a rule is triggered, an HTTP POST request is made to the callback URL containing a json payload with the measurements, device, rule, and application details.</span><span class="sxs-lookup"><span data-stu-id="abfc0-119">When a rule is triggered, an HTTP POST request is made to the callback URL containing a json payload with the measurements, device, rule, and application details.</span></span> <span data-ttu-id="abfc0-120">For a telemetry rule, the payload can look like the following:</span><span class="sxs-lookup"><span data-stu-id="abfc0-120">For a telemetry rule, the payload can look like the following:</span></span>

```json
{
    "id": "ID",
    "timestamp": "date-time",
    "device" : {
        "id":"ID",
        "name":  "Refrigerator1",
        "simulated" : true,
        "deviceTemplate":{
            "id": "ID",
            "version":"1.0.0"
        },
        "properties":{
            "device":{
                "firmwareversion":"1.0"
            },
            "cloud":{
                "location":"One Microsoft Way"
            }
        },
        "measurements":{
            "telemetry":{
                "temperature":20,
                "pressure":10
            }
        }

    },
    "rule": {
        "id": "ID",
        "name": "High temperature alert",
        "enabled": true,
        "deviceTemplate": {
            "id":"GUID",
            "version":"1.0.0"
        }
    },
    "application": {
        "id": "ID",
        "name": "Contoso app",
        "subdomain":"contoso-app"
    }
}
```

## <a name="known-limitations"></a><span data-ttu-id="abfc0-121">Known limitations</span><span class="sxs-lookup"><span data-stu-id="abfc0-121">Known limitations</span></span>
<span data-ttu-id="abfc0-122">Currently there is no programmatic way of subscribing/unsubscribing from these webhooks through an API.</span><span class="sxs-lookup"><span data-stu-id="abfc0-122">Currently there is no programmatic way of subscribing/unsubscribing from these webhooks through an API.</span></span>

<span data-ttu-id="abfc0-123">If you have ideas for how to improve this feature, post your suggestions to our [Uservoice forum](https://feedback.azure.com/forums/911455-azure-iot-central).</span><span class="sxs-lookup"><span data-stu-id="abfc0-123">If you have ideas for how to improve this feature, post your suggestions to our [Uservoice forum](https://feedback.azure.com/forums/911455-azure-iot-central).</span></span>

## <a name="next-steps"></a><span data-ttu-id="abfc0-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="abfc0-124">Next steps</span></span>
<span data-ttu-id="abfc0-125">Now that you have learned how to set up and use webhooks, the suggested next step is to explore [building workflows in Microsoft Flow](howto-add-microsoft-flow.md).</span><span class="sxs-lookup"><span data-stu-id="abfc0-125">Now that you have learned how to set up and use webhooks, the suggested next step is to explore [building workflows in Microsoft Flow](howto-add-microsoft-flow.md).</span></span>
