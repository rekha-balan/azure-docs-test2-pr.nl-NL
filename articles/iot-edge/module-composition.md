---
title: Azure IoT Edge module composition | Microsoft Docs
description: Learn how a deployment manifest declares which modules to deploy, how to deploy them, and how to create message routes between them.
author: kgremban
manager: timlt
ms.author: kgremban
ms.date: 06/06/2018
ms.topic: conceptual
ms.service: iot-edge
services: iot-edge
ms.openlocfilehash: af4a831c084ae10b381b8e08fd0ce4798b21b394
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868272"
---
# <a name="learn-how-to-use-deployment-manifests-to-deploy-modules-and-establish-routes"></a><span data-ttu-id="ace4c-103">Learn how to use deployment manifests to deploy modules and establish routes</span><span class="sxs-lookup"><span data-stu-id="ace4c-103">Learn how to use deployment manifests to deploy modules and establish routes</span></span>

<span data-ttu-id="ace4c-104">Each IoT Edge device runs at least two modules: $edgeAgent and $edgeHub, which make up the IoT Edge runtime.</span><span class="sxs-lookup"><span data-stu-id="ace4c-104">Each IoT Edge device runs at least two modules: $edgeAgent and $edgeHub, which make up the IoT Edge runtime.</span></span> <span data-ttu-id="ace4c-105">In addition to those standard two, any IoT Edge device can run multiple modules to perform any number of processes.</span><span class="sxs-lookup"><span data-stu-id="ace4c-105">In addition to those standard two, any IoT Edge device can run multiple modules to perform any number of processes.</span></span> <span data-ttu-id="ace4c-106">When you deploy all these modules to a device at once, you need a way to declare which modules are included and how they interact with each other.</span><span class="sxs-lookup"><span data-stu-id="ace4c-106">When you deploy all these modules to a device at once, you need a way to declare which modules are included and how they interact with each other.</span></span> 

<span data-ttu-id="ace4c-107">The *deployment manifest* is a JSON document that describes:</span><span class="sxs-lookup"><span data-stu-id="ace4c-107">The *deployment manifest* is a JSON document that describes:</span></span>

* <span data-ttu-id="ace4c-108">The configuration of the Edge agent, which includes the container image for each module, the credentials to access private container registries, and instructions for how each module should be created and managed.</span><span class="sxs-lookup"><span data-stu-id="ace4c-108">The configuration of the Edge agent, which includes the container image for each module, the credentials to access private container registries, and instructions for how each module should be created and managed.</span></span>
* <span data-ttu-id="ace4c-109">The configuration of the Edge hub, which includes how messages flow between modules and eventually to IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ace4c-109">The configuration of the Edge hub, which includes how messages flow between modules and eventually to IoT Hub.</span></span>
* <span data-ttu-id="ace4c-110">Optionally, the desired properties of the module twins.</span><span class="sxs-lookup"><span data-stu-id="ace4c-110">Optionally, the desired properties of the module twins.</span></span>

<span data-ttu-id="ace4c-111">All IoT Edge devices need to be configured with a deployment manifest.</span><span class="sxs-lookup"><span data-stu-id="ace4c-111">All IoT Edge devices need to be configured with a deployment manifest.</span></span> <span data-ttu-id="ace4c-112">A newly installed IoT Edge runtime reports an error code until configured with a valid manifest.</span><span class="sxs-lookup"><span data-stu-id="ace4c-112">A newly installed IoT Edge runtime reports an error code until configured with a valid manifest.</span></span> 

<span data-ttu-id="ace4c-113">In the Azure IoT Edge tutorials, you build a deployment manifest by going through a wizard in the Azure IoT Edge portal.</span><span class="sxs-lookup"><span data-stu-id="ace4c-113">In the Azure IoT Edge tutorials, you build a deployment manifest by going through a wizard in the Azure IoT Edge portal.</span></span> <span data-ttu-id="ace4c-114">You can also apply a deployment manifest programmatically using REST or the IoT Hub Service SDK.</span><span class="sxs-lookup"><span data-stu-id="ace4c-114">You can also apply a deployment manifest programmatically using REST or the IoT Hub Service SDK.</span></span> <span data-ttu-id="ace4c-115">For more information, see [Understand IoT Edge deployments][lnk-deploy].</span><span class="sxs-lookup"><span data-stu-id="ace4c-115">For more information, see [Understand IoT Edge deployments][lnk-deploy].</span></span>

## <a name="create-a-deployment-manifest"></a><span data-ttu-id="ace4c-116">Create a deployment manifest</span><span class="sxs-lookup"><span data-stu-id="ace4c-116">Create a deployment manifest</span></span>

<span data-ttu-id="ace4c-117">At a high level, the deployment manifest configures a module twin's desired properties for IoT Edge modules deployed on an IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="ace4c-117">At a high level, the deployment manifest configures a module twin's desired properties for IoT Edge modules deployed on an IoT Edge device.</span></span> <span data-ttu-id="ace4c-118">Two of these modules are always present: `$edgeAgent`, and `$edgeHub`.</span><span class="sxs-lookup"><span data-stu-id="ace4c-118">Two of these modules are always present: `$edgeAgent`, and `$edgeHub`.</span></span>

<span data-ttu-id="ace4c-119">A deployment manifest that contains only the IoT Edge runtime (agent and hub) is valid.</span><span class="sxs-lookup"><span data-stu-id="ace4c-119">A deployment manifest that contains only the IoT Edge runtime (agent and hub) is valid.</span></span>

<span data-ttu-id="ace4c-120">The manifest follows this structure:</span><span class="sxs-lookup"><span data-stu-id="ace4c-120">The manifest follows this structure:</span></span>

```json
{
    "modulesContent": {
        "$edgeAgent": {
            "properties.desired": {
                // desired properties of the Edge agent
                // includes the image URIs of all modules
                // includes container registry credentials
            }
        },
        "$edgeHub": {
            "properties.desired": {
                // desired properties of the Edge hub
                // includes the routing information between modules, and to IoT Hub
            }
        },
        "{module1}": {  // optional
            "properties.desired": {
                // desired properties of module with id {module1}
            }
        },
        "{module2}": {  // optional
            ...
        },
        ...
    }
}
```

## <a name="configure-modules"></a><span data-ttu-id="ace4c-121">Configure modules</span><span class="sxs-lookup"><span data-stu-id="ace4c-121">Configure modules</span></span>

<span data-ttu-id="ace4c-122">You need to tell the IoT Edge runtime how to install the modules in your deployment.</span><span class="sxs-lookup"><span data-stu-id="ace4c-122">You need to tell the IoT Edge runtime how to install the modules in your deployment.</span></span> <span data-ttu-id="ace4c-123">The configuration and management information for all modules goes inside the **$edgeAgent** desired properties.</span><span class="sxs-lookup"><span data-stu-id="ace4c-123">The configuration and management information for all modules goes inside the **$edgeAgent** desired properties.</span></span> <span data-ttu-id="ace4c-124">This information includes the configuration parameters for the Edge agent itself.</span><span class="sxs-lookup"><span data-stu-id="ace4c-124">This information includes the configuration parameters for the Edge agent itself.</span></span> 

<span data-ttu-id="ace4c-125">For a complete list of properties that can or must be included, see [Properties of the Edge agent and Edge hub](module-edgeagent-edgehub.md).</span><span class="sxs-lookup"><span data-stu-id="ace4c-125">For a complete list of properties that can or must be included, see [Properties of the Edge agent and Edge hub](module-edgeagent-edgehub.md).</span></span>

<span data-ttu-id="ace4c-126">The $edgeAgent properties follow this structure:</span><span class="sxs-lookup"><span data-stu-id="ace4c-126">The $edgeAgent properties follow this structure:</span></span>

```json
"$edgeAgent": {
    "properties.desired": {
        "schemaVersion": "1.0",
        "runtime": {
            "settings":{
                "registryCredentials":{ // give the edge agent access to container images that aren't public
                    }
                }
            }
        },
        "systemModules": {
            "edgeAgent": {
                // configuration and management details
            },
            "edgeHub": {
                // configuration and management details
            }
        },
        "modules": {
            "{module1}": { // optional
                // configuration and management details
            },
            "{module2}": { // optional
                // configuration and management details
            }
        }
    }
},
```

## <a name="declare-routes"></a><span data-ttu-id="ace4c-127">Declare routes</span><span class="sxs-lookup"><span data-stu-id="ace4c-127">Declare routes</span></span>

<span data-ttu-id="ace4c-128">Edge hub provides a way to declaratively route messages between modules, and between modules and IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ace4c-128">Edge hub provides a way to declaratively route messages between modules, and between modules and IoT Hub.</span></span> <span data-ttu-id="ace4c-129">The Edge hub manages all communication, so the route information goes inside the **$edgeHub** desired properties.</span><span class="sxs-lookup"><span data-stu-id="ace4c-129">The Edge hub manages all communication, so the route information goes inside the **$edgeHub** desired properties.</span></span> <span data-ttu-id="ace4c-130">You can have multiple routes within the same deployment.</span><span class="sxs-lookup"><span data-stu-id="ace4c-130">You can have multiple routes within the same deployment.</span></span>

<span data-ttu-id="ace4c-131">Routes are declared in the **$edgeHub** desired properties with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="ace4c-131">Routes are declared in the **$edgeHub** desired properties with the following syntax:</span></span>

```json
"$edgeHub": {
    "properties.desired": {
        "routes": {
            "{route1}": "FROM <source> WHERE <condition> INTO <sink>",
            "{route2}": "FROM <source> WHERE <condition> INTO <sink>"
        },
    }
}
```

<span data-ttu-id="ace4c-132">Every route needs a source and a sink, but the condition is an optional piece that you can use to filter messages.</span><span class="sxs-lookup"><span data-stu-id="ace4c-132">Every route needs a source and a sink, but the condition is an optional piece that you can use to filter messages.</span></span> 


### <a name="source"></a><span data-ttu-id="ace4c-133">Source</span><span class="sxs-lookup"><span data-stu-id="ace4c-133">Source</span></span>
<span data-ttu-id="ace4c-134">The source specifies where the messages come from.</span><span class="sxs-lookup"><span data-stu-id="ace4c-134">The source specifies where the messages come from.</span></span> <span data-ttu-id="ace4c-135">It can be any of the following values:</span><span class="sxs-lookup"><span data-stu-id="ace4c-135">It can be any of the following values:</span></span>

| <span data-ttu-id="ace4c-136">Source</span><span class="sxs-lookup"><span data-stu-id="ace4c-136">Source</span></span> | <span data-ttu-id="ace4c-137">Description</span><span class="sxs-lookup"><span data-stu-id="ace4c-137">Description</span></span> |
| ------ | ----------- |
| `/*` | <span data-ttu-id="ace4c-138">All device-to-cloud messages from any device or module</span><span class="sxs-lookup"><span data-stu-id="ace4c-138">All device-to-cloud messages from any device or module</span></span> |
| `/messages/*` | <span data-ttu-id="ace4c-139">Any device-to-cloud message sent by a device or a module through some or no output</span><span class="sxs-lookup"><span data-stu-id="ace4c-139">Any device-to-cloud message sent by a device or a module through some or no output</span></span> |
| `/messages/modules/*` | <span data-ttu-id="ace4c-140">Any device-to-cloud message sent by a module through some or no output</span><span class="sxs-lookup"><span data-stu-id="ace4c-140">Any device-to-cloud message sent by a module through some or no output</span></span> |
| `/messages/modules/{moduleId}/*` | <span data-ttu-id="ace4c-141">Any device-to-cloud message sent by {moduleId} with no output</span><span class="sxs-lookup"><span data-stu-id="ace4c-141">Any device-to-cloud message sent by {moduleId} with no output</span></span> |
| `/messages/modules/{moduleId}/outputs/*` | <span data-ttu-id="ace4c-142">Any device-to-cloud message sent by {moduleId} with some output</span><span class="sxs-lookup"><span data-stu-id="ace4c-142">Any device-to-cloud message sent by {moduleId} with some output</span></span> |
| `/messages/modules/{moduleId}/outputs/{output}` | <span data-ttu-id="ace4c-143">Any device-to-cloud message sent by {moduleId} using {output}</span><span class="sxs-lookup"><span data-stu-id="ace4c-143">Any device-to-cloud message sent by {moduleId} using {output}</span></span> |

### <a name="condition"></a><span data-ttu-id="ace4c-144">Condition</span><span class="sxs-lookup"><span data-stu-id="ace4c-144">Condition</span></span>
<span data-ttu-id="ace4c-145">The condition is optional in a route declaration.</span><span class="sxs-lookup"><span data-stu-id="ace4c-145">The condition is optional in a route declaration.</span></span> <span data-ttu-id="ace4c-146">If you want to pass all messages from the sink to the source, just leave out the **WHERE** clause entirely.</span><span class="sxs-lookup"><span data-stu-id="ace4c-146">If you want to pass all messages from the sink to the source, just leave out the **WHERE** clause entirely.</span></span> <span data-ttu-id="ace4c-147">Or you can use the [IoT Hub query language][lnk-iothub-query] to filter for certain messages or message types that satisfy the condition.</span><span class="sxs-lookup"><span data-stu-id="ace4c-147">Or you can use the [IoT Hub query language][lnk-iothub-query] to filter for certain messages or message types that satisfy the condition.</span></span>

<span data-ttu-id="ace4c-148">The messages that pass between modules in IoT Edge are formatted the same as the messages that pass between your devices and Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ace4c-148">The messages that pass between modules in IoT Edge are formatted the same as the messages that pass between your devices and Azure IoT Hub.</span></span> <span data-ttu-id="ace4c-149">All messages are formatted as JSON and have **systemProperties**, **appProperties**, and **body** parameters.</span><span class="sxs-lookup"><span data-stu-id="ace4c-149">All messages are formatted as JSON and have **systemProperties**, **appProperties**, and **body** parameters.</span></span> 

<span data-ttu-id="ace4c-150">You can build queries around all three parameters with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="ace4c-150">You can build queries around all three parameters with the following syntax:</span></span> 

* <span data-ttu-id="ace4c-151">System properties: `$<propertyName>` or `{$<propertyName>}`</span><span class="sxs-lookup"><span data-stu-id="ace4c-151">System properties: `$<propertyName>` or `{$<propertyName>}`</span></span>
* <span data-ttu-id="ace4c-152">Application properties: `<propertyName>`</span><span class="sxs-lookup"><span data-stu-id="ace4c-152">Application properties: `<propertyName>`</span></span>
* <span data-ttu-id="ace4c-153">Body properties: `$body.<propertyName>`</span><span class="sxs-lookup"><span data-stu-id="ace4c-153">Body properties: `$body.<propertyName>`</span></span> 

<span data-ttu-id="ace4c-154">For examples about how to create queries for message properties, see [Device-to-cloud message routes query expressions](../iot-hub/iot-hub-devguide-query-language.md#device-to-cloud-message-routes-query-expressions).</span><span class="sxs-lookup"><span data-stu-id="ace4c-154">For examples about how to create queries for message properties, see [Device-to-cloud message routes query expressions](../iot-hub/iot-hub-devguide-query-language.md#device-to-cloud-message-routes-query-expressions).</span></span>

<span data-ttu-id="ace4c-155">An example that is specific to IoT Edge is when you want to filter for messages that arrived at a gateway device from a leaf device.</span><span class="sxs-lookup"><span data-stu-id="ace4c-155">An example that is specific to IoT Edge is when you want to filter for messages that arrived at a gateway device from a leaf device.</span></span> <span data-ttu-id="ace4c-156">Messages that come from modules contain a system property called **connectionModuleId**.</span><span class="sxs-lookup"><span data-stu-id="ace4c-156">Messages that come from modules contain a system property called **connectionModuleId**.</span></span> <span data-ttu-id="ace4c-157">So if you want to route messages from leaf devices directly to IoT Hub, use the following route to exclude module messages:</span><span class="sxs-lookup"><span data-stu-id="ace4c-157">So if you want to route messages from leaf devices directly to IoT Hub, use the following route to exclude module messages:</span></span>

```sql
FROM /messages/\* WHERE NOT IS_DEFINED($connectionModuleId) INTO $upstream
```

### <a name="sink"></a><span data-ttu-id="ace4c-158">Sink</span><span class="sxs-lookup"><span data-stu-id="ace4c-158">Sink</span></span>
<span data-ttu-id="ace4c-159">The sink defines where the messages are sent.</span><span class="sxs-lookup"><span data-stu-id="ace4c-159">The sink defines where the messages are sent.</span></span> <span data-ttu-id="ace4c-160">It can be any of the following values:</span><span class="sxs-lookup"><span data-stu-id="ace4c-160">It can be any of the following values:</span></span>

| <span data-ttu-id="ace4c-161">Sink</span><span class="sxs-lookup"><span data-stu-id="ace4c-161">Sink</span></span> | <span data-ttu-id="ace4c-162">Description</span><span class="sxs-lookup"><span data-stu-id="ace4c-162">Description</span></span> |
| ---- | ----------- |
| `$upstream` | <span data-ttu-id="ace4c-163">Send the message to IoT Hub</span><span class="sxs-lookup"><span data-stu-id="ace4c-163">Send the message to IoT Hub</span></span> |
| `BrokeredEndpoint("/modules/{moduleId}/inputs/{input}")` | <span data-ttu-id="ace4c-164">Send the message to input `{input}` of module `{moduleId}`</span><span class="sxs-lookup"><span data-stu-id="ace4c-164">Send the message to input `{input}` of module `{moduleId}`</span></span> |

<span data-ttu-id="ace4c-165">IoT Edge provides at-least-once guarantees.</span><span class="sxs-lookup"><span data-stu-id="ace4c-165">IoT Edge provides at-least-once guarantees.</span></span> <span data-ttu-id="ace4c-166">The Edge hub stores messages locally in case a route cannot deliver the message to its sink.</span><span class="sxs-lookup"><span data-stu-id="ace4c-166">The Edge hub stores messages locally in case a route cannot deliver the message to its sink.</span></span> <span data-ttu-id="ace4c-167">For example, if the Edge hub cannot connect to IoT Hub, or the target module is not connected.</span><span class="sxs-lookup"><span data-stu-id="ace4c-167">For example, if the Edge hub cannot connect to IoT Hub, or the target module is not connected.</span></span>

<span data-ttu-id="ace4c-168">Edge hub stores the messages up to the time specified in the `storeAndForwardConfiguration.timeToLiveSecs` property of the [Edge hub desired properties](module-edgeagent-edgehub.md).</span><span class="sxs-lookup"><span data-stu-id="ace4c-168">Edge hub stores the messages up to the time specified in the `storeAndForwardConfiguration.timeToLiveSecs` property of the [Edge hub desired properties](module-edgeagent-edgehub.md).</span></span>

## <a name="define-or-update-desired-properties"></a><span data-ttu-id="ace4c-169">Define or update desired properties</span><span class="sxs-lookup"><span data-stu-id="ace4c-169">Define or update desired properties</span></span> 

<span data-ttu-id="ace4c-170">The deployment manifest can specify desired properties for the module twin of each module deployed to the IoT Edge device.</span><span class="sxs-lookup"><span data-stu-id="ace4c-170">The deployment manifest can specify desired properties for the module twin of each module deployed to the IoT Edge device.</span></span> <span data-ttu-id="ace4c-171">When the desired properties are specified in the deployment manifest, they overwrite any desired properties currently in the module twin.</span><span class="sxs-lookup"><span data-stu-id="ace4c-171">When the desired properties are specified in the deployment manifest, they overwrite any desired properties currently in the module twin.</span></span>

<span data-ttu-id="ace4c-172">If you do not specify a module twin's desired properties in the deployment manifest, IoT Hub will not modify the module twin in any way, and you will be able to set the desired properties programmatically.</span><span class="sxs-lookup"><span data-stu-id="ace4c-172">If you do not specify a module twin's desired properties in the deployment manifest, IoT Hub will not modify the module twin in any way, and you will be able to set the desired properties programmatically.</span></span>

<span data-ttu-id="ace4c-173">The same mechanisms that allow you to modify device twins are used to modify module twins.</span><span class="sxs-lookup"><span data-stu-id="ace4c-173">The same mechanisms that allow you to modify device twins are used to modify module twins.</span></span> <span data-ttu-id="ace4c-174">For more information, see the [device twin developer guide](../iot-hub/iot-hub-devguide-device-twins.md).</span><span class="sxs-lookup"><span data-stu-id="ace4c-174">For more information, see the [device twin developer guide](../iot-hub/iot-hub-devguide-device-twins.md).</span></span>   

## <a name="deployment-manifest-example"></a><span data-ttu-id="ace4c-175">Deployment manifest example</span><span class="sxs-lookup"><span data-stu-id="ace4c-175">Deployment manifest example</span></span>

<span data-ttu-id="ace4c-176">This an example of a deployment manifest JSON document.</span><span class="sxs-lookup"><span data-stu-id="ace4c-176">This an example of a deployment manifest JSON document.</span></span>

```json
{
  "modulesContent": {
    "$edgeAgent": {
      "properties.desired": {
        "schemaVersion": "1.0",
        "runtime": {
          "type": "docker",
          "settings": {
            "minDockerVersion": "v1.25",
            "loggingOptions": "",
            "registryCredentials": {
              "ContosoRegistry": {
                "username": "myacr",
                "password": "{password}",
                "address": "myacr.azurecr.io"
              }
            }
          }
        },
        "systemModules": {
          "edgeAgent": {
            "type": "docker",
            "settings": {
              "image": "mcr.microsoft.com/azureiotedge-agent:1.0",
              "createOptions": ""
            }
          },
          "edgeHub": {
            "type": "docker",
            "status": "running",
            "restartPolicy": "always",
            "settings": {
              "image": "mcr.microsoft.com/azureiotedge-hub:1.0",
              "createOptions": ""
            }
          }
        },
        "modules": {
          "tempSensor": {
            "version": "1.0",
            "type": "docker",
            "status": "running",
            "restartPolicy": "always",
            "settings": {
              "image": "mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0",
              "createOptions": "{}"
            }
          },
          "filtermodule": {
            "version": "1.0",
            "type": "docker",
            "status": "running",
            "restartPolicy": "always",
            "settings": {
              "image": "myacr.azurecr.io/filtermodule:latest",
              "createOptions": "{}"
            }
          }
        }
      }
    },
    "$edgeHub": {
      "properties.desired": {
        "schemaVersion": "1.0",
        "routes": {
          "sensorToFilter": "FROM /messages/modules/tempSensor/outputs/temperatureOutput INTO BrokeredEndpoint(\"/modules/filtermodule/inputs/input1\")",
          "filterToIoTHub": "FROM /messages/modules/filtermodule/outputs/output1 INTO $upstream"
        },
        "storeAndForwardConfiguration": {
          "timeToLiveSecs": 10
        }
      }
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ace4c-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="ace4c-177">Next steps</span></span>

* <span data-ttu-id="ace4c-178">For a complete list of properties that can or must be included in $edgeAgent and $edgeHub, see [Properties of the Edge agent and Edge hub](module-edgeagent-edgehub.md).</span><span class="sxs-lookup"><span data-stu-id="ace4c-178">For a complete list of properties that can or must be included in $edgeAgent and $edgeHub, see [Properties of the Edge agent and Edge hub](module-edgeagent-edgehub.md).</span></span>

* <span data-ttu-id="ace4c-179">Now that you know how IoT Edge modules are used, [Understand the requirements and tools for developing IoT Edge modules][lnk-module-dev].</span><span class="sxs-lookup"><span data-stu-id="ace4c-179">Now that you know how IoT Edge modules are used, [Understand the requirements and tools for developing IoT Edge modules][lnk-module-dev].</span></span>

[lnk-deploy]: module-deployment-monitoring.md
[lnk-iothub-query]: ../iot-hub/iot-hub-devguide-query-language.md
[lnk-docker-create-options]: https://docs.docker.com/engine/api/v1.32/#operation/ContainerCreate
[lnk-docker-logging-options]: https://docs.docker.com/engine/admin/logging/overview/
[lnk-module-dev]: module-development.md
