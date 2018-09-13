---
title: Consumption Model in Azure Maps | Microsoft Docs
description: Learn about consumption model in Azure Maps
author: subbarayudukamma
ms.author: skamma
ms.date: 05/08/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.openlocfilehash: cf20c7dbfbf7cd3f09579b03b835148c1c295137
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857771"
---
# <a name="consumption-model"></a><span data-ttu-id="99db0-103">Consumption model</span><span class="sxs-lookup"><span data-stu-id="99db0-103">Consumption model</span></span>

<span data-ttu-id="99db0-104">Online Routing provides a set of parameters for a detailed description of vehicle-specific Consumption Model.</span><span class="sxs-lookup"><span data-stu-id="99db0-104">Online Routing provides a set of parameters for a detailed description of vehicle-specific Consumption Model.</span></span>
<span data-ttu-id="99db0-105">Depending on the value of **vehicleEngineType**, two principal Consumption Models are supported: _Combustion_ and _Electric_.</span><span class="sxs-lookup"><span data-stu-id="99db0-105">Depending on the value of **vehicleEngineType**, two principal Consumption Models are supported: _Combustion_ and _Electric_.</span></span> <span data-ttu-id="99db0-106">Specifying parameters that belong to different models in the same request is an error.</span><span class="sxs-lookup"><span data-stu-id="99db0-106">Specifying parameters that belong to different models in the same request is an error.</span></span>
<span data-ttu-id="99db0-107">Consumption Model cannot be used with **travelMode** values _bicycle_ and _pedestrian_.</span><span class="sxs-lookup"><span data-stu-id="99db0-107">Consumption Model cannot be used with **travelMode** values _bicycle_ and _pedestrian_.</span></span>

## <a name="parameter-constraints-for-consumption-model"></a><span data-ttu-id="99db0-108">Parameter constraints for consumption model</span><span class="sxs-lookup"><span data-stu-id="99db0-108">Parameter constraints for consumption model</span></span>

<span data-ttu-id="99db0-109">In both Consumption Models, explicitly specifying some parameters requires specifying some others as well.</span><span class="sxs-lookup"><span data-stu-id="99db0-109">In both Consumption Models, explicitly specifying some parameters requires specifying some others as well.</span></span> <span data-ttu-id="99db0-110">These dependencies are:</span><span class="sxs-lookup"><span data-stu-id="99db0-110">These dependencies are:</span></span>

* <span data-ttu-id="99db0-111">All parameters require **constantSpeedConsumption** to be specified by the user.</span><span class="sxs-lookup"><span data-stu-id="99db0-111">All parameters require **constantSpeedConsumption** to be specified by the user.</span></span> <span data-ttu-id="99db0-112">It is an error to specify any other consumption model parameter, with the exception of **vehicleWeight**, if **constantSpeedConsumption**\* is not specified.</span><span class="sxs-lookup"><span data-stu-id="99db0-112">It is an error to specify any other consumption model parameter, with the exception of **vehicleWeight**, if **constantSpeedConsumption**\* is not specified.</span></span>
* <span data-ttu-id="99db0-113">**accelerationEfficiency** and **decelerationEfficiency** must always be specified as a pair (i.e. both or none).</span><span class="sxs-lookup"><span data-stu-id="99db0-113">**accelerationEfficiency** and **decelerationEfficiency** must always be specified as a pair (i.e. both or none).</span></span>
* <span data-ttu-id="99db0-114">If **accelerationEfficiency** and **decelerationEfficiency** are specified, product of their values must not be greater than 1 (to prevent perpetual motion).</span><span class="sxs-lookup"><span data-stu-id="99db0-114">If **accelerationEfficiency** and **decelerationEfficiency** are specified, product of their values must not be greater than 1 (to prevent perpetual motion).</span></span>
* <span data-ttu-id="99db0-115">**uphillEfficiency** and **downhillEfficiency** must always be specified as a pair (i.e. both or none).</span><span class="sxs-lookup"><span data-stu-id="99db0-115">**uphillEfficiency** and **downhillEfficiency** must always be specified as a pair (i.e. both or none).</span></span>
* <span data-ttu-id="99db0-116">If **uphillEfficiency** and **downhillEfficiency** are specified, product of their values must not be greater than 1 (to prevent perpetual motion).</span><span class="sxs-lookup"><span data-stu-id="99db0-116">If **uphillEfficiency** and **downhillEfficiency** are specified, product of their values must not be greater than 1 (to prevent perpetual motion).</span></span>
* <span data-ttu-id="99db0-117">If \***Efficiency** parameters are specified by the user, then **vehicleWeight** must also be specified.</span><span class="sxs-lookup"><span data-stu-id="99db0-117">If \***Efficiency** parameters are specified by the user, then **vehicleWeight** must also be specified.</span></span> <span data-ttu-id="99db0-118">When **vehicleEngineType** is _combustion_, **fuelEnergyDensityInMJoulesPerLiter** must be specified as well.</span><span class="sxs-lookup"><span data-stu-id="99db0-118">When **vehicleEngineType** is _combustion_, **fuelEnergyDensityInMJoulesPerLiter** must be specified as well.</span></span>
* <span data-ttu-id="99db0-119">**maxChargeInkWh** and **currentChargeInkWh** must always be specified as a pair (i.e. both or none).</span><span class="sxs-lookup"><span data-stu-id="99db0-119">**maxChargeInkWh** and **currentChargeInkWh** must always be specified as a pair (i.e. both or none).</span></span>

> [!NOTE]
> <span data-ttu-id="99db0-120">If only **constantSpeedConsumption** is specified, no other consumption aspects like slopes and vehicle acceleration are taken into account for consumption computations.</span><span class="sxs-lookup"><span data-stu-id="99db0-120">If only **constantSpeedConsumption** is specified, no other consumption aspects like slopes and vehicle acceleration are taken into account for consumption computations.</span></span>

## <a name="combustion-consumption-model"></a><span data-ttu-id="99db0-121">Combustion consumption model</span><span class="sxs-lookup"><span data-stu-id="99db0-121">Combustion consumption model</span></span>

<span data-ttu-id="99db0-122">The Combustion Consumption Model is used when **vehicleEngineType** is set to _combustion_.</span><span class="sxs-lookup"><span data-stu-id="99db0-122">The Combustion Consumption Model is used when **vehicleEngineType** is set to _combustion_.</span></span>
<span data-ttu-id="99db0-123">The list of parameters that belong to this model are below.</span><span class="sxs-lookup"><span data-stu-id="99db0-123">The list of parameters that belong to this model are below.</span></span> <span data-ttu-id="99db0-124">Refer to the Parameters section for detailed description.</span><span class="sxs-lookup"><span data-stu-id="99db0-124">Refer to the Parameters section for detailed description.</span></span>

* <span data-ttu-id="99db0-125">constantSpeedConsumptionInLitersPerHundredkm</span><span class="sxs-lookup"><span data-stu-id="99db0-125">constantSpeedConsumptionInLitersPerHundredkm</span></span>
* <span data-ttu-id="99db0-126">vehicleWeight</span><span class="sxs-lookup"><span data-stu-id="99db0-126">vehicleWeight</span></span>
* <span data-ttu-id="99db0-127">currentFuelInLiters</span><span class="sxs-lookup"><span data-stu-id="99db0-127">currentFuelInLiters</span></span>
* <span data-ttu-id="99db0-128">auxiliaryPowerInLitersPerHour</span><span class="sxs-lookup"><span data-stu-id="99db0-128">auxiliaryPowerInLitersPerHour</span></span>
* <span data-ttu-id="99db0-129">fuelEnergyDensityInMJoulesPerLiter</span><span class="sxs-lookup"><span data-stu-id="99db0-129">fuelEnergyDensityInMJoulesPerLiter</span></span>
* <span data-ttu-id="99db0-130">accelerationEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-130">accelerationEfficiency</span></span>
* <span data-ttu-id="99db0-131">decelerationEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-131">decelerationEfficiency</span></span>
* <span data-ttu-id="99db0-132">uphillEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-132">uphillEfficiency</span></span>
* <span data-ttu-id="99db0-133">downhillEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-133">downhillEfficiency</span></span>

## <a name="electric-consumption-model"></a><span data-ttu-id="99db0-134">Electric consumption model</span><span class="sxs-lookup"><span data-stu-id="99db0-134">Electric consumption model</span></span>

<span data-ttu-id="99db0-135">The Electric Consumption Model is used when **vehicleEngineType** is set to _electric_.</span><span class="sxs-lookup"><span data-stu-id="99db0-135">The Electric Consumption Model is used when **vehicleEngineType** is set to _electric_.</span></span>
<span data-ttu-id="99db0-136">The list of parameters that belong to this model are below.</span><span class="sxs-lookup"><span data-stu-id="99db0-136">The list of parameters that belong to this model are below.</span></span> <span data-ttu-id="99db0-137">Refer to the Parameters section for detailed description.</span><span class="sxs-lookup"><span data-stu-id="99db0-137">Refer to the Parameters section for detailed description.</span></span>

* <span data-ttu-id="99db0-138">constantSpeedConsumptionInkWhPerHundredkm</span><span class="sxs-lookup"><span data-stu-id="99db0-138">constantSpeedConsumptionInkWhPerHundredkm</span></span>
* <span data-ttu-id="99db0-139">vehicleWeight</span><span class="sxs-lookup"><span data-stu-id="99db0-139">vehicleWeight</span></span>
* <span data-ttu-id="99db0-140">currentChargeInkWh</span><span class="sxs-lookup"><span data-stu-id="99db0-140">currentChargeInkWh</span></span>
* <span data-ttu-id="99db0-141">maxChargeInkWh</span><span class="sxs-lookup"><span data-stu-id="99db0-141">maxChargeInkWh</span></span>
* <span data-ttu-id="99db0-142">auxiliaryPowerInkW</span><span class="sxs-lookup"><span data-stu-id="99db0-142">auxiliaryPowerInkW</span></span>
* <span data-ttu-id="99db0-143">accelerationEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-143">accelerationEfficiency</span></span>
* <span data-ttu-id="99db0-144">decelerationEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-144">decelerationEfficiency</span></span>
* <span data-ttu-id="99db0-145">uphillEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-145">uphillEfficiency</span></span>
* <span data-ttu-id="99db0-146">downhillEfficiency</span><span class="sxs-lookup"><span data-stu-id="99db0-146">downhillEfficiency</span></span>

## <a name="sensible-values-of-consumption-parameters"></a><span data-ttu-id="99db0-147">Sensible values of consumption parameters</span><span class="sxs-lookup"><span data-stu-id="99db0-147">Sensible values of consumption parameters</span></span>

<span data-ttu-id="99db0-148">A particular set of consumption parameters can be rejected, even though it might fulfill all the explicit requirements specified above.</span><span class="sxs-lookup"><span data-stu-id="99db0-148">A particular set of consumption parameters can be rejected, even though it might fulfill all the explicit requirements specified above.</span></span> <span data-ttu-id="99db0-149">It happens when the value of a specific parameter, or a combination of values of several parameters, is deemed to lead to unreasonable magnitudes of consumption values.</span><span class="sxs-lookup"><span data-stu-id="99db0-149">It happens when the value of a specific parameter, or a combination of values of several parameters, is deemed to lead to unreasonable magnitudes of consumption values.</span></span> <span data-ttu-id="99db0-150">If that happens, it most likely indicates an input error, as proper care is taken to accommodate all sensible values of consumption parameters.</span><span class="sxs-lookup"><span data-stu-id="99db0-150">If that happens, it most likely indicates an input error, as proper care is taken to accommodate all sensible values of consumption parameters.</span></span> <span data-ttu-id="99db0-151">In case a particular set of consumption parameters is rejected, the accompanying error message will contain a textual explanation of the reason(s).</span><span class="sxs-lookup"><span data-stu-id="99db0-151">In case a particular set of consumption parameters is rejected, the accompanying error message will contain a textual explanation of the reason(s).</span></span>
<span data-ttu-id="99db0-152">The detailed descriptions of the parameters have examples of sensible values for both models.</span><span class="sxs-lookup"><span data-stu-id="99db0-152">The detailed descriptions of the parameters have examples of sensible values for both models.</span></span>
