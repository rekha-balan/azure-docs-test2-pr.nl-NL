---
author: manish-shukla01
ms.author: manshuk
ms.service: virtual-machines-windows
ms.topic: include
ms.date: 08-03-2018
ms.openlocfilehash: 41216fe12e10f72f76043f1a8bc361b538259ac1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857242"
---
# <a name="virtual-machine-size-flexibility-with-reserved-vm-instances"></a><span data-ttu-id="97039-101">Virtual machine size flexibility with Reserved VM Instances</span><span class="sxs-lookup"><span data-stu-id="97039-101">Virtual machine size flexibility with Reserved VM Instances</span></span>

<span data-ttu-id="97039-102">With a reserved virtual machine instance that's optimized for instance size flexibility, the reservation you buy can apply to the virtual machines (VMs) sizes in the same size series group.</span><span class="sxs-lookup"><span data-stu-id="97039-102">With a reserved virtual machine instance that's optimized for instance size flexibility, the reservation you buy can apply to the virtual machines (VMs) sizes in the same size series group.</span></span> <span data-ttu-id="97039-103">For example, if you buy a reservation for a VM size that's listed in the DSv2-series table, like Standard_DS5_v2, the reservation discount can apply to the other four sizes that are listed in that same table:</span><span class="sxs-lookup"><span data-stu-id="97039-103">For example, if you buy a reservation for a VM size that's listed in the DSv2-series table, like Standard_DS5_v2, the reservation discount can apply to the other four sizes that are listed in that same table:</span></span>

- <span data-ttu-id="97039-104">Standard_DS1_v2</span><span class="sxs-lookup"><span data-stu-id="97039-104">Standard_DS1_v2</span></span>
- <span data-ttu-id="97039-105">Standard_DS2_v2</span><span class="sxs-lookup"><span data-stu-id="97039-105">Standard_DS2_v2</span></span>
- <span data-ttu-id="97039-106">Standard_DS3_v2</span><span class="sxs-lookup"><span data-stu-id="97039-106">Standard_DS3_v2</span></span>
- <span data-ttu-id="97039-107">Standard_DS4_v2</span><span class="sxs-lookup"><span data-stu-id="97039-107">Standard_DS4_v2</span></span>

<span data-ttu-id="97039-108">But that reservation discount doesn't apply to VMs sizes that are listed in different tables, like what's in the DSv2-series high memory table: Standard_DS11_v2, Standard_DS12_v2, and so on.</span><span class="sxs-lookup"><span data-stu-id="97039-108">But that reservation discount doesn't apply to VMs sizes that are listed in different tables, like what's in the DSv2-series high memory table: Standard_DS11_v2, Standard_DS12_v2, and so on.</span></span>

<span data-ttu-id="97039-109">Within the size series group, the number of VMs the reservation discount applies to depends on the VM size you pick when you buy a reservation.</span><span class="sxs-lookup"><span data-stu-id="97039-109">Within the size series group, the number of VMs the reservation discount applies to depends on the VM size you pick when you buy a reservation.</span></span> <span data-ttu-id="97039-110">It also depends on the sizes of the VMs that you have running.</span><span class="sxs-lookup"><span data-stu-id="97039-110">It also depends on the sizes of the VMs that you have running.</span></span> <span data-ttu-id="97039-111">The ratio column that's listed in the following tables compares the relative footprint for each VM size in that group.</span><span class="sxs-lookup"><span data-stu-id="97039-111">The ratio column that's listed in the following tables compares the relative footprint for each VM size in that group.</span></span> <span data-ttu-id="97039-112">Use the ratio value to calculate how the reservation discount applies to the VMs you have running.</span><span class="sxs-lookup"><span data-stu-id="97039-112">Use the ratio value to calculate how the reservation discount applies to the VMs you have running.</span></span>

## <a name="examples"></a><span data-ttu-id="97039-113">Examples</span><span class="sxs-lookup"><span data-stu-id="97039-113">Examples</span></span>

<span data-ttu-id="97039-114">The following examples use the sizes and ratios in the DSv2-series table.</span><span class="sxs-lookup"><span data-stu-id="97039-114">The following examples use the sizes and ratios in the DSv2-series table.</span></span>

 <span data-ttu-id="97039-115">You buy a reserved VM instance with the size Standard_DS4_v2 where the ratio or relative footprint compared to the other sizes in that series is 8.</span><span class="sxs-lookup"><span data-stu-id="97039-115">You buy a reserved VM instance with the size Standard_DS4_v2 where the ratio or relative footprint compared to the other sizes in that series is 8.</span></span>

- <span data-ttu-id="97039-116">Scenario 1: Run eight Standard_DS1_v2 sized VMs with a ratio of 1.</span><span class="sxs-lookup"><span data-stu-id="97039-116">Scenario 1: Run eight Standard_DS1_v2 sized VMs with a ratio of 1.</span></span> <span data-ttu-id="97039-117">Your reservation discount applies to all eight of those VMs.</span><span class="sxs-lookup"><span data-stu-id="97039-117">Your reservation discount applies to all eight of those VMs.</span></span>
- <span data-ttu-id="97039-118">Scenario 2: Run two Standard_DS2_v2 sized VMs with a ratio of 2 each.</span><span class="sxs-lookup"><span data-stu-id="97039-118">Scenario 2: Run two Standard_DS2_v2 sized VMs with a ratio of 2 each.</span></span> <span data-ttu-id="97039-119">Also run a Standard_DS3_v2 sized VM with a ratio of 4.</span><span class="sxs-lookup"><span data-stu-id="97039-119">Also run a Standard_DS3_v2 sized VM with a ratio of 4.</span></span> <span data-ttu-id="97039-120">The total footprint is 2+2+4=8.</span><span class="sxs-lookup"><span data-stu-id="97039-120">The total footprint is 2+2+4=8.</span></span> <span data-ttu-id="97039-121">So your reservation discount applies to all three of those VMs.</span><span class="sxs-lookup"><span data-stu-id="97039-121">So your reservation discount applies to all three of those VMs.</span></span>
- <span data-ttu-id="97039-122">Scenario 3: Run one Standard_DS5_v2 with a ratio of 16.</span><span class="sxs-lookup"><span data-stu-id="97039-122">Scenario 3: Run one Standard_DS5_v2 with a ratio of 16.</span></span> <span data-ttu-id="97039-123">Your reservation discount applies to half that VM's compute cost.</span><span class="sxs-lookup"><span data-stu-id="97039-123">Your reservation discount applies to half that VM's compute cost.</span></span>

<span data-ttu-id="97039-124">The following sections show what sizes are in the same size series group when you buy a reserved VM instance optimized for instance size flexibility.</span><span class="sxs-lookup"><span data-stu-id="97039-124">The following sections show what sizes are in the same size series group when you buy a reserved VM instance optimized for instance size flexibility.</span></span>

## <a name="b-series"></a><span data-ttu-id="97039-125">B-series</span><span class="sxs-lookup"><span data-stu-id="97039-125">B-series</span></span>

| <span data-ttu-id="97039-126">Size</span><span class="sxs-lookup"><span data-stu-id="97039-126">Size</span></span> | <span data-ttu-id="97039-127">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-127">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-128">Standard_B1s</span><span class="sxs-lookup"><span data-stu-id="97039-128">Standard_B1s</span></span> | <span data-ttu-id="97039-129">1</span><span class="sxs-lookup"><span data-stu-id="97039-129">1</span></span> |
|<span data-ttu-id="97039-130">Standard_B2s</span><span class="sxs-lookup"><span data-stu-id="97039-130">Standard_B2s</span></span>|<span data-ttu-id="97039-131">4</span><span class="sxs-lookup"><span data-stu-id="97039-131">4</span></span>|

<span data-ttu-id="97039-132">For more information, see [B-series burstable virtual machine sizes](../articles/virtual-machines/windows/b-series-burstable.md).</span><span class="sxs-lookup"><span data-stu-id="97039-132">For more information, see [B-series burstable virtual machine sizes](../articles/virtual-machines/windows/b-series-burstable.md).</span></span>

## <a name="b-series-high-memory"></a><span data-ttu-id="97039-133">B-series high memory</span><span class="sxs-lookup"><span data-stu-id="97039-133">B-series high memory</span></span>

| <span data-ttu-id="97039-134">Size</span><span class="sxs-lookup"><span data-stu-id="97039-134">Size</span></span> | <span data-ttu-id="97039-135">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-135">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-136">Standard_B1ms</span><span class="sxs-lookup"><span data-stu-id="97039-136">Standard_B1ms</span></span> |<span data-ttu-id="97039-137">1</span><span class="sxs-lookup"><span data-stu-id="97039-137">1</span></span>|
|<span data-ttu-id="97039-138">Standard_B2ms</span><span class="sxs-lookup"><span data-stu-id="97039-138">Standard_B2ms</span></span>|<span data-ttu-id="97039-139">4</span><span class="sxs-lookup"><span data-stu-id="97039-139">4</span></span>|
|<span data-ttu-id="97039-140">Standard_B4ms</span><span class="sxs-lookup"><span data-stu-id="97039-140">Standard_B4ms</span></span>|<span data-ttu-id="97039-141">8</span><span class="sxs-lookup"><span data-stu-id="97039-141">8</span></span>|
|<span data-ttu-id="97039-142">Standard_B8ms</span><span class="sxs-lookup"><span data-stu-id="97039-142">Standard_B8ms</span></span>|<span data-ttu-id="97039-143">16</span><span class="sxs-lookup"><span data-stu-id="97039-143">16</span></span>|

<span data-ttu-id="97039-144">For more information, see [B-series burstable virtual machine sizes](../articles/virtual-machines/windows/b-series-burstable.md).</span><span class="sxs-lookup"><span data-stu-id="97039-144">For more information, see [B-series burstable virtual machine sizes](../articles/virtual-machines/windows/b-series-burstable.md).</span></span>

## <a name="d-series"></a><span data-ttu-id="97039-145">D-series</span><span class="sxs-lookup"><span data-stu-id="97039-145">D-series</span></span>

| <span data-ttu-id="97039-146">Size</span><span class="sxs-lookup"><span data-stu-id="97039-146">Size</span></span> | <span data-ttu-id="97039-147">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-147">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-148">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="97039-148">Standard_D1</span></span>|<span data-ttu-id="97039-149">1</span><span class="sxs-lookup"><span data-stu-id="97039-149">1</span></span>|
|<span data-ttu-id="97039-150">Standard_D2</span><span class="sxs-lookup"><span data-stu-id="97039-150">Standard_D2</span></span>|<span data-ttu-id="97039-151">2</span><span class="sxs-lookup"><span data-stu-id="97039-151">2</span></span>|
|<span data-ttu-id="97039-152">Standard_D3</span><span class="sxs-lookup"><span data-stu-id="97039-152">Standard_D3</span></span>|<span data-ttu-id="97039-153">4</span><span class="sxs-lookup"><span data-stu-id="97039-153">4</span></span>|
|<span data-ttu-id="97039-154">Standard_D4</span><span class="sxs-lookup"><span data-stu-id="97039-154">Standard_D4</span></span>|<span data-ttu-id="97039-155">8</span><span class="sxs-lookup"><span data-stu-id="97039-155">8</span></span>|

<span data-ttu-id="97039-156">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span><span class="sxs-lookup"><span data-stu-id="97039-156">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span></span>

## <a name="d-series-high-memory"></a><span data-ttu-id="97039-157">D-series high memory</span><span class="sxs-lookup"><span data-stu-id="97039-157">D-series high memory</span></span>

| <span data-ttu-id="97039-158">Size</span><span class="sxs-lookup"><span data-stu-id="97039-158">Size</span></span> | <span data-ttu-id="97039-159">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-159">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-160">Standard_D11</span><span class="sxs-lookup"><span data-stu-id="97039-160">Standard_D11</span></span>|<span data-ttu-id="97039-161">1</span><span class="sxs-lookup"><span data-stu-id="97039-161">1</span></span>|
|<span data-ttu-id="97039-162">Standard_D12</span><span class="sxs-lookup"><span data-stu-id="97039-162">Standard_D12</span></span>|<span data-ttu-id="97039-163">2</span><span class="sxs-lookup"><span data-stu-id="97039-163">2</span></span>|
|<span data-ttu-id="97039-164">Standard_D13</span><span class="sxs-lookup"><span data-stu-id="97039-164">Standard_D13</span></span>|<span data-ttu-id="97039-165">4</span><span class="sxs-lookup"><span data-stu-id="97039-165">4</span></span>|
|<span data-ttu-id="97039-166">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="97039-166">Standard_D14</span></span>|<span data-ttu-id="97039-167">8</span><span class="sxs-lookup"><span data-stu-id="97039-167">8</span></span>|

<span data-ttu-id="97039-168">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span><span class="sxs-lookup"><span data-stu-id="97039-168">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span></span>

## <a name="ds-series"></a><span data-ttu-id="97039-169">Ds-series</span><span class="sxs-lookup"><span data-stu-id="97039-169">Ds-series</span></span>

| <span data-ttu-id="97039-170">Size</span><span class="sxs-lookup"><span data-stu-id="97039-170">Size</span></span> | <span data-ttu-id="97039-171">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-171">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-172">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="97039-172">Standard_DS1</span></span>|<span data-ttu-id="97039-173">1</span><span class="sxs-lookup"><span data-stu-id="97039-173">1</span></span>|
|<span data-ttu-id="97039-174">Standard_DS2</span><span class="sxs-lookup"><span data-stu-id="97039-174">Standard_DS2</span></span>|<span data-ttu-id="97039-175">2</span><span class="sxs-lookup"><span data-stu-id="97039-175">2</span></span>|
|<span data-ttu-id="97039-176">Standard_DS3</span><span class="sxs-lookup"><span data-stu-id="97039-176">Standard_DS3</span></span>|<span data-ttu-id="97039-177">4</span><span class="sxs-lookup"><span data-stu-id="97039-177">4</span></span>|
|<span data-ttu-id="97039-178">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="97039-178">Standard_DS4</span></span>|<span data-ttu-id="97039-179">8</span><span class="sxs-lookup"><span data-stu-id="97039-179">8</span></span>|

<span data-ttu-id="97039-180">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span><span class="sxs-lookup"><span data-stu-id="97039-180">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span></span>

## <a name="ds-series-high-memory"></a><span data-ttu-id="97039-181">Ds-series high memory</span><span class="sxs-lookup"><span data-stu-id="97039-181">Ds-series high memory</span></span>

| <span data-ttu-id="97039-182">Size</span><span class="sxs-lookup"><span data-stu-id="97039-182">Size</span></span> | <span data-ttu-id="97039-183">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-183">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-184">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="97039-184">Standard_DS11</span></span>|<span data-ttu-id="97039-185">1</span><span class="sxs-lookup"><span data-stu-id="97039-185">1</span></span>|
|<span data-ttu-id="97039-186">Standard_DS12</span><span class="sxs-lookup"><span data-stu-id="97039-186">Standard_DS12</span></span>|<span data-ttu-id="97039-187">2</span><span class="sxs-lookup"><span data-stu-id="97039-187">2</span></span>|
|<span data-ttu-id="97039-188">Standard_DS13</span><span class="sxs-lookup"><span data-stu-id="97039-188">Standard_DS13</span></span>|<span data-ttu-id="97039-189">4</span><span class="sxs-lookup"><span data-stu-id="97039-189">4</span></span>|
|<span data-ttu-id="97039-190">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="97039-190">Standard_DS14</span></span>|<span data-ttu-id="97039-191">8</span><span class="sxs-lookup"><span data-stu-id="97039-191">8</span></span>|

<span data-ttu-id="97039-192">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span><span class="sxs-lookup"><span data-stu-id="97039-192">For more information, see [Previous generations of virtual machine sizes](../articles/virtual-machines/windows/sizes-previous-gen.md).</span></span>

## <a name="dsv2-series"></a><span data-ttu-id="97039-193">DSv2-series</span><span class="sxs-lookup"><span data-stu-id="97039-193">DSv2-series</span></span>

| <span data-ttu-id="97039-194">Size</span><span class="sxs-lookup"><span data-stu-id="97039-194">Size</span></span> | <span data-ttu-id="97039-195">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-195">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-196">Standard_DS1_v2</span><span class="sxs-lookup"><span data-stu-id="97039-196">Standard_DS1_v2</span></span>|<span data-ttu-id="97039-197">1</span><span class="sxs-lookup"><span data-stu-id="97039-197">1</span></span>|
|<span data-ttu-id="97039-198">Standard_DS2_v2</span><span class="sxs-lookup"><span data-stu-id="97039-198">Standard_DS2_v2</span></span>|<span data-ttu-id="97039-199">2</span><span class="sxs-lookup"><span data-stu-id="97039-199">2</span></span>|
|<span data-ttu-id="97039-200">Standard_DS3_v2</span><span class="sxs-lookup"><span data-stu-id="97039-200">Standard_DS3_v2</span></span>|<span data-ttu-id="97039-201">4</span><span class="sxs-lookup"><span data-stu-id="97039-201">4</span></span>|
|<span data-ttu-id="97039-202">Standard_DS4_v2</span><span class="sxs-lookup"><span data-stu-id="97039-202">Standard_DS4_v2</span></span>|<span data-ttu-id="97039-203">8</span><span class="sxs-lookup"><span data-stu-id="97039-203">8</span></span>|
|<span data-ttu-id="97039-204">Standard_DS5_v2</span><span class="sxs-lookup"><span data-stu-id="97039-204">Standard_DS5_v2</span></span>|<span data-ttu-id="97039-205">16</span><span class="sxs-lookup"><span data-stu-id="97039-205">16</span></span>|

<span data-ttu-id="97039-206">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dv2-series).</span><span class="sxs-lookup"><span data-stu-id="97039-206">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dv2-series).</span></span>

## <a name="dsv2-series-high-memory"></a><span data-ttu-id="97039-207">DSv2-series high memory</span><span class="sxs-lookup"><span data-stu-id="97039-207">DSv2-series high memory</span></span>

| <span data-ttu-id="97039-208">Size</span><span class="sxs-lookup"><span data-stu-id="97039-208">Size</span></span> | <span data-ttu-id="97039-209">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-209">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-210">Standard_DS11_v2</span><span class="sxs-lookup"><span data-stu-id="97039-210">Standard_DS11_v2</span></span>|<span data-ttu-id="97039-211">1</span><span class="sxs-lookup"><span data-stu-id="97039-211">1</span></span>|
|<span data-ttu-id="97039-212">Standard_DS12_v2</span><span class="sxs-lookup"><span data-stu-id="97039-212">Standard_DS12_v2</span></span>|<span data-ttu-id="97039-213">2</span><span class="sxs-lookup"><span data-stu-id="97039-213">2</span></span>|
|<span data-ttu-id="97039-214">Standard_DS13_v2</span><span class="sxs-lookup"><span data-stu-id="97039-214">Standard_DS13_v2</span></span>|<span data-ttu-id="97039-215">4</span><span class="sxs-lookup"><span data-stu-id="97039-215">4</span></span>|
|<span data-ttu-id="97039-216">Standard_DS14_v2</span><span class="sxs-lookup"><span data-stu-id="97039-216">Standard_DS14_v2</span></span>|<span data-ttu-id="97039-217">8</span><span class="sxs-lookup"><span data-stu-id="97039-217">8</span></span>|
|<span data-ttu-id="97039-218">Standard_DS15_v2</span><span class="sxs-lookup"><span data-stu-id="97039-218">Standard_DS15_v2</span></span>|<span data-ttu-id="97039-219">10</span><span class="sxs-lookup"><span data-stu-id="97039-219">10</span></span>|

<span data-ttu-id="97039-220">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#dsv2-series-11-15).</span><span class="sxs-lookup"><span data-stu-id="97039-220">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#dsv2-series-11-15).</span></span>

## <a name="dsv3-series"></a><span data-ttu-id="97039-221">DSv3-series</span><span class="sxs-lookup"><span data-stu-id="97039-221">DSv3-series</span></span>

| <span data-ttu-id="97039-222">Size</span><span class="sxs-lookup"><span data-stu-id="97039-222">Size</span></span> | <span data-ttu-id="97039-223">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-223">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-224">Standard_D2s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-224">Standard_D2s_v3</span></span>|<span data-ttu-id="97039-225">1</span><span class="sxs-lookup"><span data-stu-id="97039-225">1</span></span>|
|<span data-ttu-id="97039-226">Standard_D4s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-226">Standard_D4s_v3</span></span>|<span data-ttu-id="97039-227">2</span><span class="sxs-lookup"><span data-stu-id="97039-227">2</span></span>|
|<span data-ttu-id="97039-228">Standard_D8s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-228">Standard_D8s_v3</span></span>|<span data-ttu-id="97039-229">4</span><span class="sxs-lookup"><span data-stu-id="97039-229">4</span></span>|
|<span data-ttu-id="97039-230">Standard_D16s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-230">Standard_D16s_v3</span></span>|<span data-ttu-id="97039-231">8</span><span class="sxs-lookup"><span data-stu-id="97039-231">8</span></span>|
|<span data-ttu-id="97039-232">Standard_D32s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-232">Standard_D32s_v3</span></span>|<span data-ttu-id="97039-233">16</span><span class="sxs-lookup"><span data-stu-id="97039-233">16</span></span>|
|<span data-ttu-id="97039-234">Standard_D64s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-234">Standard_D64s_v3</span></span>|<span data-ttu-id="97039-235">32</span><span class="sxs-lookup"><span data-stu-id="97039-235">32</span></span>|

<span data-ttu-id="97039-236">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dsv3-series-sup1sup).</span><span class="sxs-lookup"><span data-stu-id="97039-236">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dsv3-series-sup1sup).</span></span>

## <a name="dv2-series"></a><span data-ttu-id="97039-237">Dv2-series</span><span class="sxs-lookup"><span data-stu-id="97039-237">Dv2-series</span></span>

| <span data-ttu-id="97039-238">Size</span><span class="sxs-lookup"><span data-stu-id="97039-238">Size</span></span> | <span data-ttu-id="97039-239">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-239">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-240">Standard_D1_v2</span><span class="sxs-lookup"><span data-stu-id="97039-240">Standard_D1_v2</span></span>|<span data-ttu-id="97039-241">1</span><span class="sxs-lookup"><span data-stu-id="97039-241">1</span></span>|
|<span data-ttu-id="97039-242">Standard_D2_v2</span><span class="sxs-lookup"><span data-stu-id="97039-242">Standard_D2_v2</span></span>|<span data-ttu-id="97039-243">2</span><span class="sxs-lookup"><span data-stu-id="97039-243">2</span></span>|
|<span data-ttu-id="97039-244">Standard_D3_v2</span><span class="sxs-lookup"><span data-stu-id="97039-244">Standard_D3_v2</span></span>|<span data-ttu-id="97039-245">4</span><span class="sxs-lookup"><span data-stu-id="97039-245">4</span></span>|
|<span data-ttu-id="97039-246">Standard_D4_v2</span><span class="sxs-lookup"><span data-stu-id="97039-246">Standard_D4_v2</span></span>|<span data-ttu-id="97039-247">8</span><span class="sxs-lookup"><span data-stu-id="97039-247">8</span></span>|
|<span data-ttu-id="97039-248">Standard_D5_v2</span><span class="sxs-lookup"><span data-stu-id="97039-248">Standard_D5_v2</span></span>|<span data-ttu-id="97039-249">16</span><span class="sxs-lookup"><span data-stu-id="97039-249">16</span></span>|

<span data-ttu-id="97039-250">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dv2-series).</span><span class="sxs-lookup"><span data-stu-id="97039-250">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dv2-series).</span></span>

## <a name="dv2-series-high-memory"></a><span data-ttu-id="97039-251">Dv2-series high memory</span><span class="sxs-lookup"><span data-stu-id="97039-251">Dv2-series high memory</span></span>

| <span data-ttu-id="97039-252">Size</span><span class="sxs-lookup"><span data-stu-id="97039-252">Size</span></span> | <span data-ttu-id="97039-253">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-253">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-254">Standard_D11_v2</span><span class="sxs-lookup"><span data-stu-id="97039-254">Standard_D11_v2</span></span>|<span data-ttu-id="97039-255">1</span><span class="sxs-lookup"><span data-stu-id="97039-255">1</span></span>|
|<span data-ttu-id="97039-256">Standard_D12_v2</span><span class="sxs-lookup"><span data-stu-id="97039-256">Standard_D12_v2</span></span>|<span data-ttu-id="97039-257">2</span><span class="sxs-lookup"><span data-stu-id="97039-257">2</span></span>|
|<span data-ttu-id="97039-258">Standard_D13_v2</span><span class="sxs-lookup"><span data-stu-id="97039-258">Standard_D13_v2</span></span>|<span data-ttu-id="97039-259">4</span><span class="sxs-lookup"><span data-stu-id="97039-259">4</span></span>|
|<span data-ttu-id="97039-260">Standard_D14_v2</span><span class="sxs-lookup"><span data-stu-id="97039-260">Standard_D14_v2</span></span>|<span data-ttu-id="97039-261">8</span><span class="sxs-lookup"><span data-stu-id="97039-261">8</span></span>|
|<span data-ttu-id="97039-262">Standard_D15_v2</span><span class="sxs-lookup"><span data-stu-id="97039-262">Standard_D15_v2</span></span>|<span data-ttu-id="97039-263">10</span><span class="sxs-lookup"><span data-stu-id="97039-263">10</span></span>|

<span data-ttu-id="97039-264">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#dv2-series-11-15).</span><span class="sxs-lookup"><span data-stu-id="97039-264">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#dv2-series-11-15).</span></span>

## <a name="dv3-series"></a><span data-ttu-id="97039-265">Dv3-series</span><span class="sxs-lookup"><span data-stu-id="97039-265">Dv3-series</span></span>

| <span data-ttu-id="97039-266">Size</span><span class="sxs-lookup"><span data-stu-id="97039-266">Size</span></span> | <span data-ttu-id="97039-267">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-267">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-268">Standard_D2_v3</span><span class="sxs-lookup"><span data-stu-id="97039-268">Standard_D2_v3</span></span>|<span data-ttu-id="97039-269">1</span><span class="sxs-lookup"><span data-stu-id="97039-269">1</span></span>|
|<span data-ttu-id="97039-270">Standard_D4_v3</span><span class="sxs-lookup"><span data-stu-id="97039-270">Standard_D4_v3</span></span>|<span data-ttu-id="97039-271">2</span><span class="sxs-lookup"><span data-stu-id="97039-271">2</span></span>|
|<span data-ttu-id="97039-272">Standard_D8_v3</span><span class="sxs-lookup"><span data-stu-id="97039-272">Standard_D8_v3</span></span>|<span data-ttu-id="97039-273">4</span><span class="sxs-lookup"><span data-stu-id="97039-273">4</span></span>|
|<span data-ttu-id="97039-274">Standard_D16_v3</span><span class="sxs-lookup"><span data-stu-id="97039-274">Standard_D16_v3</span></span>|<span data-ttu-id="97039-275">8</span><span class="sxs-lookup"><span data-stu-id="97039-275">8</span></span>|
|<span data-ttu-id="97039-276">Standard_D32_v3</span><span class="sxs-lookup"><span data-stu-id="97039-276">Standard_D32_v3</span></span>|<span data-ttu-id="97039-277">16</span><span class="sxs-lookup"><span data-stu-id="97039-277">16</span></span>|
|<span data-ttu-id="97039-278">Standard_D64_v3</span><span class="sxs-lookup"><span data-stu-id="97039-278">Standard_D64_v3</span></span>|<span data-ttu-id="97039-279">32</span><span class="sxs-lookup"><span data-stu-id="97039-279">32</span></span>|

<span data-ttu-id="97039-280">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dv3-series-sup1sup).</span><span class="sxs-lookup"><span data-stu-id="97039-280">For more information, see [General purpose virtual machine sizes](../articles/virtual-machines/windows/sizes-general.md#dv3-series-sup1sup).</span></span>

## <a name="esv3-series"></a><span data-ttu-id="97039-281">ESv3-series</span><span class="sxs-lookup"><span data-stu-id="97039-281">ESv3-series</span></span>

| <span data-ttu-id="97039-282">Size</span><span class="sxs-lookup"><span data-stu-id="97039-282">Size</span></span> | <span data-ttu-id="97039-283">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-283">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-284">Standard_E2s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-284">Standard_E2s_v3</span></span>|<span data-ttu-id="97039-285">1</span><span class="sxs-lookup"><span data-stu-id="97039-285">1</span></span>|
|<span data-ttu-id="97039-286">Standard_E4s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-286">Standard_E4s_v3</span></span>|<span data-ttu-id="97039-287">2</span><span class="sxs-lookup"><span data-stu-id="97039-287">2</span></span>|
|<span data-ttu-id="97039-288">Standard_E8s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-288">Standard_E8s_v3</span></span>|<span data-ttu-id="97039-289">4</span><span class="sxs-lookup"><span data-stu-id="97039-289">4</span></span>|
|<span data-ttu-id="97039-290">Standard_E16s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-290">Standard_E16s_v3</span></span>|<span data-ttu-id="97039-291">8</span><span class="sxs-lookup"><span data-stu-id="97039-291">8</span></span>|
|<span data-ttu-id="97039-292">Standard_E32s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-292">Standard_E32s_v3</span></span>|<span data-ttu-id="97039-293">16</span><span class="sxs-lookup"><span data-stu-id="97039-293">16</span></span>|
|<span data-ttu-id="97039-294">Standard_E64s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-294">Standard_E64s_v3</span></span>|<span data-ttu-id="97039-295">32</span><span class="sxs-lookup"><span data-stu-id="97039-295">32</span></span>|

<span data-ttu-id="97039-296">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#esv3-series).</span><span class="sxs-lookup"><span data-stu-id="97039-296">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#esv3-series).</span></span>

## <a name="ev3-series"></a><span data-ttu-id="97039-297">Ev3-series</span><span class="sxs-lookup"><span data-stu-id="97039-297">Ev3-series</span></span>

| <span data-ttu-id="97039-298">Size</span><span class="sxs-lookup"><span data-stu-id="97039-298">Size</span></span> | <span data-ttu-id="97039-299">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-299">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-300">Standard_E2_v3</span><span class="sxs-lookup"><span data-stu-id="97039-300">Standard_E2_v3</span></span>|<span data-ttu-id="97039-301">1</span><span class="sxs-lookup"><span data-stu-id="97039-301">1</span></span>|
|<span data-ttu-id="97039-302">Standard_E4_v3</span><span class="sxs-lookup"><span data-stu-id="97039-302">Standard_E4_v3</span></span>|<span data-ttu-id="97039-303">2</span><span class="sxs-lookup"><span data-stu-id="97039-303">2</span></span>|
|<span data-ttu-id="97039-304">Standard_E8_v3</span><span class="sxs-lookup"><span data-stu-id="97039-304">Standard_E8_v3</span></span>|<span data-ttu-id="97039-305">4</span><span class="sxs-lookup"><span data-stu-id="97039-305">4</span></span>|
|<span data-ttu-id="97039-306">Standard_E16_v3</span><span class="sxs-lookup"><span data-stu-id="97039-306">Standard_E16_v3</span></span>|<span data-ttu-id="97039-307">8</span><span class="sxs-lookup"><span data-stu-id="97039-307">8</span></span>|
|<span data-ttu-id="97039-308">Standard_E32_v3</span><span class="sxs-lookup"><span data-stu-id="97039-308">Standard_E32_v3</span></span>|<span data-ttu-id="97039-309">16</span><span class="sxs-lookup"><span data-stu-id="97039-309">16</span></span>|
|<span data-ttu-id="97039-310">Standard_E64_v3</span><span class="sxs-lookup"><span data-stu-id="97039-310">Standard_E64_v3</span></span>|<span data-ttu-id="97039-311">32</span><span class="sxs-lookup"><span data-stu-id="97039-311">32</span></span>|

<span data-ttu-id="97039-312">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#ev3-series).</span><span class="sxs-lookup"><span data-stu-id="97039-312">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#ev3-series).</span></span>

## <a name="f-series"></a><span data-ttu-id="97039-313">F-series</span><span class="sxs-lookup"><span data-stu-id="97039-313">F-series</span></span>

| <span data-ttu-id="97039-314">Size</span><span class="sxs-lookup"><span data-stu-id="97039-314">Size</span></span> | <span data-ttu-id="97039-315">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-315">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-316">Standard_F1</span><span class="sxs-lookup"><span data-stu-id="97039-316">Standard_F1</span></span>|<span data-ttu-id="97039-317">1</span><span class="sxs-lookup"><span data-stu-id="97039-317">1</span></span>|
|<span data-ttu-id="97039-318">Standard_F2</span><span class="sxs-lookup"><span data-stu-id="97039-318">Standard_F2</span></span>|<span data-ttu-id="97039-319">2</span><span class="sxs-lookup"><span data-stu-id="97039-319">2</span></span>|
|<span data-ttu-id="97039-320">Standard_F4</span><span class="sxs-lookup"><span data-stu-id="97039-320">Standard_F4</span></span>|<span data-ttu-id="97039-321">4</span><span class="sxs-lookup"><span data-stu-id="97039-321">4</span></span>|
|<span data-ttu-id="97039-322">Standard_F8</span><span class="sxs-lookup"><span data-stu-id="97039-322">Standard_F8</span></span>|<span data-ttu-id="97039-323">8</span><span class="sxs-lookup"><span data-stu-id="97039-323">8</span></span>|
<span data-ttu-id="97039-324">Standard_F16</span><span class="sxs-lookup"><span data-stu-id="97039-324">Standard_F16</span></span>|<span data-ttu-id="97039-325">16</span><span class="sxs-lookup"><span data-stu-id="97039-325">16</span></span>|

<span data-ttu-id="97039-326">For more information, see [Compute optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-compute.md#f-series).</span><span class="sxs-lookup"><span data-stu-id="97039-326">For more information, see [Compute optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-compute.md#f-series).</span></span>

## <a name="fs-series"></a><span data-ttu-id="97039-327">FS-series</span><span class="sxs-lookup"><span data-stu-id="97039-327">FS-series</span></span>

| <span data-ttu-id="97039-328">Size</span><span class="sxs-lookup"><span data-stu-id="97039-328">Size</span></span> | <span data-ttu-id="97039-329">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-329">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-330">Standard_F1s</span><span class="sxs-lookup"><span data-stu-id="97039-330">Standard_F1s</span></span>|<span data-ttu-id="97039-331">1</span><span class="sxs-lookup"><span data-stu-id="97039-331">1</span></span>|
|<span data-ttu-id="97039-332">Standard_F2s</span><span class="sxs-lookup"><span data-stu-id="97039-332">Standard_F2s</span></span>|<span data-ttu-id="97039-333">2</span><span class="sxs-lookup"><span data-stu-id="97039-333">2</span></span>|
|<span data-ttu-id="97039-334">Standard_F4s</span><span class="sxs-lookup"><span data-stu-id="97039-334">Standard_F4s</span></span>|<span data-ttu-id="97039-335">4</span><span class="sxs-lookup"><span data-stu-id="97039-335">4</span></span>|
|<span data-ttu-id="97039-336">Standard_F8s</span><span class="sxs-lookup"><span data-stu-id="97039-336">Standard_F8s</span></span>|<span data-ttu-id="97039-337">8</span><span class="sxs-lookup"><span data-stu-id="97039-337">8</span></span>|
|<span data-ttu-id="97039-338">Standard_F16s</span><span class="sxs-lookup"><span data-stu-id="97039-338">Standard_F16s</span></span>|<span data-ttu-id="97039-339">16</span><span class="sxs-lookup"><span data-stu-id="97039-339">16</span></span>|

<span data-ttu-id="97039-340">For more information, see [Compute optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-compute.md#fs-series-sup1sup).</span><span class="sxs-lookup"><span data-stu-id="97039-340">For more information, see [Compute optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-compute.md#fs-series-sup1sup).</span></span>

## <a name="fsv2-series"></a><span data-ttu-id="97039-341">Fsv2-series</span><span class="sxs-lookup"><span data-stu-id="97039-341">Fsv2-series</span></span>

| <span data-ttu-id="97039-342">Size</span><span class="sxs-lookup"><span data-stu-id="97039-342">Size</span></span> | <span data-ttu-id="97039-343">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-343">Ratio</span></span>|
|---|---|
|<span data-ttu-id="97039-344">Standard_F2s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-344">Standard_F2s_v2</span></span>|<span data-ttu-id="97039-345">1</span><span class="sxs-lookup"><span data-stu-id="97039-345">1</span></span>|
|<span data-ttu-id="97039-346">Standard_F4s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-346">Standard_F4s_v2</span></span>|<span data-ttu-id="97039-347">2</span><span class="sxs-lookup"><span data-stu-id="97039-347">2</span></span>|
|<span data-ttu-id="97039-348">Standard_F8s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-348">Standard_F8s_v2</span></span>|<span data-ttu-id="97039-349">4</span><span class="sxs-lookup"><span data-stu-id="97039-349">4</span></span>|
|<span data-ttu-id="97039-350">Standard_F16s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-350">Standard_F16s_v2</span></span>|<span data-ttu-id="97039-351">8</span><span class="sxs-lookup"><span data-stu-id="97039-351">8</span></span>|
|<span data-ttu-id="97039-352">Standard_F32s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-352">Standard_F32s_v2</span></span>|<span data-ttu-id="97039-353">16</span><span class="sxs-lookup"><span data-stu-id="97039-353">16</span></span>|
|<span data-ttu-id="97039-354">Standard_F64s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-354">Standard_F64s_v2</span></span>|<span data-ttu-id="97039-355">32</span><span class="sxs-lookup"><span data-stu-id="97039-355">32</span></span>|
|<span data-ttu-id="97039-356">Standard_F72s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-356">Standard_F72s_v2</span></span>|<span data-ttu-id="97039-357">36</span><span class="sxs-lookup"><span data-stu-id="97039-357">36</span></span>|

<span data-ttu-id="97039-358">For more information, see [Compute optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-compute.md#fsv2-series-sup1sup).</span><span class="sxs-lookup"><span data-stu-id="97039-358">For more information, see [Compute optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-compute.md#fsv2-series-sup1sup).</span></span>

## <a name="h-series"></a><span data-ttu-id="97039-359">H-series</span><span class="sxs-lookup"><span data-stu-id="97039-359">H-series</span></span>

| <span data-ttu-id="97039-360">Size</span><span class="sxs-lookup"><span data-stu-id="97039-360">Size</span></span> | <span data-ttu-id="97039-361">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-361">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-362">Standard_H8</span><span class="sxs-lookup"><span data-stu-id="97039-362">Standard_H8</span></span>|<span data-ttu-id="97039-363">1</span><span class="sxs-lookup"><span data-stu-id="97039-363">1</span></span>|
|<span data-ttu-id="97039-364">Standard_H16</span><span class="sxs-lookup"><span data-stu-id="97039-364">Standard_H16</span></span>|<span data-ttu-id="97039-365">2</span><span class="sxs-lookup"><span data-stu-id="97039-365">2</span></span>|

<span data-ttu-id="97039-366">For more information, see [High performance compute VM sizes](../articles/virtual-machines/windows/sizes-hpc.md).</span><span class="sxs-lookup"><span data-stu-id="97039-366">For more information, see [High performance compute VM sizes](../articles/virtual-machines/windows/sizes-hpc.md).</span></span>

## <a name="h-series-high-memory"></a><span data-ttu-id="97039-367">H-series high memory</span><span class="sxs-lookup"><span data-stu-id="97039-367">H-series high memory</span></span>

| <span data-ttu-id="97039-368">Size</span><span class="sxs-lookup"><span data-stu-id="97039-368">Size</span></span> | <span data-ttu-id="97039-369">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-369">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-370">Standard_H8m</span><span class="sxs-lookup"><span data-stu-id="97039-370">Standard_H8m</span></span>|<span data-ttu-id="97039-371">1</span><span class="sxs-lookup"><span data-stu-id="97039-371">1</span></span>|
|<span data-ttu-id="97039-372">Standard_H16m</span><span class="sxs-lookup"><span data-stu-id="97039-372">Standard_H16m</span></span>|<span data-ttu-id="97039-373">2</span><span class="sxs-lookup"><span data-stu-id="97039-373">2</span></span>|

<span data-ttu-id="97039-374">For more information, see [High performance compute VM sizes](../articles/virtual-machines/windows/sizes-hpc.md).</span><span class="sxs-lookup"><span data-stu-id="97039-374">For more information, see [High performance compute VM sizes](../articles/virtual-machines/windows/sizes-hpc.md).</span></span>

## <a name="ls-series"></a><span data-ttu-id="97039-375">Ls-series</span><span class="sxs-lookup"><span data-stu-id="97039-375">Ls-series</span></span>

| <span data-ttu-id="97039-376">Size</span><span class="sxs-lookup"><span data-stu-id="97039-376">Size</span></span> | <span data-ttu-id="97039-377">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-377">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-378">Standard_L4s</span><span class="sxs-lookup"><span data-stu-id="97039-378">Standard_L4s</span></span>|<span data-ttu-id="97039-379">1</span><span class="sxs-lookup"><span data-stu-id="97039-379">1</span></span>|
|<span data-ttu-id="97039-380">Standard_L8s</span><span class="sxs-lookup"><span data-stu-id="97039-380">Standard_L8s</span></span>|<span data-ttu-id="97039-381">2</span><span class="sxs-lookup"><span data-stu-id="97039-381">2</span></span>|
|<span data-ttu-id="97039-382">Standard_L16s</span><span class="sxs-lookup"><span data-stu-id="97039-382">Standard_L16s</span></span>|<span data-ttu-id="97039-383">4</span><span class="sxs-lookup"><span data-stu-id="97039-383">4</span></span>|
|<span data-ttu-id="97039-384">Standard_L32s</span><span class="sxs-lookup"><span data-stu-id="97039-384">Standard_L32s</span></span>|<span data-ttu-id="97039-385">8</span><span class="sxs-lookup"><span data-stu-id="97039-385">8</span></span>|

<span data-ttu-id="97039-386">For more information, see [Storage optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-storage.md).</span><span class="sxs-lookup"><span data-stu-id="97039-386">For more information, see [Storage optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-storage.md).</span></span>

## <a name="m-series"></a><span data-ttu-id="97039-387">M-series</span><span class="sxs-lookup"><span data-stu-id="97039-387">M-series</span></span>

| <span data-ttu-id="97039-388">Size</span><span class="sxs-lookup"><span data-stu-id="97039-388">Size</span></span> | <span data-ttu-id="97039-389">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-389">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-390">Standard_M64s</span><span class="sxs-lookup"><span data-stu-id="97039-390">Standard_M64s</span></span>|<span data-ttu-id="97039-391">1</span><span class="sxs-lookup"><span data-stu-id="97039-391">1</span></span>|
|<span data-ttu-id="97039-392">Standard_M128s</span><span class="sxs-lookup"><span data-stu-id="97039-392">Standard_M128s</span></span>|<span data-ttu-id="97039-393">2</span><span class="sxs-lookup"><span data-stu-id="97039-393">2</span></span>|

<span data-ttu-id="97039-394">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span><span class="sxs-lookup"><span data-stu-id="97039-394">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span></span>

## <a name="m-series-fractional"></a><span data-ttu-id="97039-395">M-series fractional</span><span class="sxs-lookup"><span data-stu-id="97039-395">M-series fractional</span></span>

| <span data-ttu-id="97039-396">Size</span><span class="sxs-lookup"><span data-stu-id="97039-396">Size</span></span> | <span data-ttu-id="97039-397">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-397">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-398">Standard_M16s</span><span class="sxs-lookup"><span data-stu-id="97039-398">Standard_M16s</span></span>|<span data-ttu-id="97039-399">1</span><span class="sxs-lookup"><span data-stu-id="97039-399">1</span></span>|
|<span data-ttu-id="97039-400">Standard_M32s</span><span class="sxs-lookup"><span data-stu-id="97039-400">Standard_M32s</span></span>|<span data-ttu-id="97039-401">2</span><span class="sxs-lookup"><span data-stu-id="97039-401">2</span></span>|

<span data-ttu-id="97039-402">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span><span class="sxs-lookup"><span data-stu-id="97039-402">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span></span>

## <a name="m-series-fractional-high-memory"></a><span data-ttu-id="97039-403">M-series fractional high memory</span><span class="sxs-lookup"><span data-stu-id="97039-403">M-series fractional high memory</span></span>

| <span data-ttu-id="97039-404">Size</span><span class="sxs-lookup"><span data-stu-id="97039-404">Size</span></span> | <span data-ttu-id="97039-405">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-405">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-406">Standard_M8ms</span><span class="sxs-lookup"><span data-stu-id="97039-406">Standard_M8ms</span></span>|<span data-ttu-id="97039-407">1</span><span class="sxs-lookup"><span data-stu-id="97039-407">1</span></span>|
|<span data-ttu-id="97039-408">Standard_M16ms</span><span class="sxs-lookup"><span data-stu-id="97039-408">Standard_M16ms</span></span>|<span data-ttu-id="97039-409">2</span><span class="sxs-lookup"><span data-stu-id="97039-409">2</span></span>|
|<span data-ttu-id="97039-410">Standard_M32ms</span><span class="sxs-lookup"><span data-stu-id="97039-410">Standard_M32ms</span></span>|<span data-ttu-id="97039-411">4</span><span class="sxs-lookup"><span data-stu-id="97039-411">4</span></span>|

<span data-ttu-id="97039-412">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span><span class="sxs-lookup"><span data-stu-id="97039-412">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span></span>

## <a name="m-series-fractional-large"></a><span data-ttu-id="97039-413">M-series fractional large</span><span class="sxs-lookup"><span data-stu-id="97039-413">M-series fractional large</span></span>

| <span data-ttu-id="97039-414">Size</span><span class="sxs-lookup"><span data-stu-id="97039-414">Size</span></span> | <span data-ttu-id="97039-415">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-415">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-416">Standard_M32ls</span><span class="sxs-lookup"><span data-stu-id="97039-416">Standard_M32ls</span></span>|<span data-ttu-id="97039-417">1</span><span class="sxs-lookup"><span data-stu-id="97039-417">1</span></span>|
|<span data-ttu-id="97039-418">Standard_M64ls</span><span class="sxs-lookup"><span data-stu-id="97039-418">Standard_M64ls</span></span>|<span data-ttu-id="97039-419">2</span><span class="sxs-lookup"><span data-stu-id="97039-419">2</span></span>|

<span data-ttu-id="97039-420">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span><span class="sxs-lookup"><span data-stu-id="97039-420">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span></span>

## <a name="m-series-high-memory"></a><span data-ttu-id="97039-421">M-series high memory</span><span class="sxs-lookup"><span data-stu-id="97039-421">M-series high memory</span></span>

| <span data-ttu-id="97039-422">Size</span><span class="sxs-lookup"><span data-stu-id="97039-422">Size</span></span> | <span data-ttu-id="97039-423">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-423">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-424">Standard_M64ms</span><span class="sxs-lookup"><span data-stu-id="97039-424">Standard_M64ms</span></span>|<span data-ttu-id="97039-425">1</span><span class="sxs-lookup"><span data-stu-id="97039-425">1</span></span>|
|<span data-ttu-id="97039-426">Standard_M128ms</span><span class="sxs-lookup"><span data-stu-id="97039-426">Standard_M128ms</span></span>|<span data-ttu-id="97039-427">2</span><span class="sxs-lookup"><span data-stu-id="97039-427">2</span></span>|

<span data-ttu-id="97039-428">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span><span class="sxs-lookup"><span data-stu-id="97039-428">For more information, see [Memory optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-memory.md#m-series).</span></span>

## <a name="nc-series"></a><span data-ttu-id="97039-429">NC-series</span><span class="sxs-lookup"><span data-stu-id="97039-429">NC-series</span></span>

| <span data-ttu-id="97039-430">Size</span><span class="sxs-lookup"><span data-stu-id="97039-430">Size</span></span> | <span data-ttu-id="97039-431">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-431">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-432">Standard_NC6</span><span class="sxs-lookup"><span data-stu-id="97039-432">Standard_NC6</span></span>|<span data-ttu-id="97039-433">1</span><span class="sxs-lookup"><span data-stu-id="97039-433">1</span></span>|
|<span data-ttu-id="97039-434">Standard_NC12</span><span class="sxs-lookup"><span data-stu-id="97039-434">Standard_NC12</span></span>|<span data-ttu-id="97039-435">2</span><span class="sxs-lookup"><span data-stu-id="97039-435">2</span></span>|
|<span data-ttu-id="97039-436">Standard_NC24</span><span class="sxs-lookup"><span data-stu-id="97039-436">Standard_NC24</span></span>|<span data-ttu-id="97039-437">4</span><span class="sxs-lookup"><span data-stu-id="97039-437">4</span></span>|

<span data-ttu-id="97039-438">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-gpu.md).</span><span class="sxs-lookup"><span data-stu-id="97039-438">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows/sizes-gpu.md).</span></span>

## <a name="ncv2-series"></a><span data-ttu-id="97039-439">NCv2-series</span><span class="sxs-lookup"><span data-stu-id="97039-439">NCv2-series</span></span>

| <span data-ttu-id="97039-440">Size</span><span class="sxs-lookup"><span data-stu-id="97039-440">Size</span></span> | <span data-ttu-id="97039-441">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-441">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-442">Standard_NC6s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-442">Standard_NC6s_v2</span></span>|<span data-ttu-id="97039-443">1</span><span class="sxs-lookup"><span data-stu-id="97039-443">1</span></span>|
|<span data-ttu-id="97039-444">Standard_NC12s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-444">Standard_NC12s_v2</span></span>|<span data-ttu-id="97039-445">2</span><span class="sxs-lookup"><span data-stu-id="97039-445">2</span></span>|
|<span data-ttu-id="97039-446">Standard_NC24s_v2</span><span class="sxs-lookup"><span data-stu-id="97039-446">Standard_NC24s_v2</span></span>|<span data-ttu-id="97039-447">4</span><span class="sxs-lookup"><span data-stu-id="97039-447">4</span></span>|

<span data-ttu-id="97039-448">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#ncv2-series).</span><span class="sxs-lookup"><span data-stu-id="97039-448">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#ncv2-series).</span></span>

## <a name="ncv3-series"></a><span data-ttu-id="97039-449">NCv3-series</span><span class="sxs-lookup"><span data-stu-id="97039-449">NCv3-series</span></span>

| <span data-ttu-id="97039-450">Size</span><span class="sxs-lookup"><span data-stu-id="97039-450">Size</span></span> | <span data-ttu-id="97039-451">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-451">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-452">Standard_NC6s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-452">Standard_NC6s_v3</span></span>|<span data-ttu-id="97039-453">1</span><span class="sxs-lookup"><span data-stu-id="97039-453">1</span></span>|
|<span data-ttu-id="97039-454">Standard_NC12s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-454">Standard_NC12s_v3</span></span>|<span data-ttu-id="97039-455">2</span><span class="sxs-lookup"><span data-stu-id="97039-455">2</span></span>|
|<span data-ttu-id="97039-456">Standard_NC24s_v3</span><span class="sxs-lookup"><span data-stu-id="97039-456">Standard_NC24s_v3</span></span>|<span data-ttu-id="97039-457">4</span><span class="sxs-lookup"><span data-stu-id="97039-457">4</span></span>|

<span data-ttu-id="97039-458">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#ncv3-series).</span><span class="sxs-lookup"><span data-stu-id="97039-458">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#ncv3-series).</span></span>

## <a name="nd-series"></a><span data-ttu-id="97039-459">ND-series</span><span class="sxs-lookup"><span data-stu-id="97039-459">ND-series</span></span>

| <span data-ttu-id="97039-460">Size</span><span class="sxs-lookup"><span data-stu-id="97039-460">Size</span></span> | <span data-ttu-id="97039-461">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-461">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-462">Standard_ND6s</span><span class="sxs-lookup"><span data-stu-id="97039-462">Standard_ND6s</span></span>|<span data-ttu-id="97039-463">1</span><span class="sxs-lookup"><span data-stu-id="97039-463">1</span></span>|
|<span data-ttu-id="97039-464">Standard_ND12s</span><span class="sxs-lookup"><span data-stu-id="97039-464">Standard_ND12s</span></span>|<span data-ttu-id="97039-465">2</span><span class="sxs-lookup"><span data-stu-id="97039-465">2</span></span>|
|<span data-ttu-id="97039-466">Standard_ND24s</span><span class="sxs-lookup"><span data-stu-id="97039-466">Standard_ND24s</span></span>|<span data-ttu-id="97039-467">4</span><span class="sxs-lookup"><span data-stu-id="97039-467">4</span></span>|

<span data-ttu-id="97039-468">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#nd-series).</span><span class="sxs-lookup"><span data-stu-id="97039-468">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#nd-series).</span></span>

## <a name="nv-series"></a><span data-ttu-id="97039-469">NV-series</span><span class="sxs-lookup"><span data-stu-id="97039-469">NV-series</span></span>

| <span data-ttu-id="97039-470">Size</span><span class="sxs-lookup"><span data-stu-id="97039-470">Size</span></span> | <span data-ttu-id="97039-471">Ratio</span><span class="sxs-lookup"><span data-stu-id="97039-471">Ratio</span></span>|
|---|---|
| <span data-ttu-id="97039-472">Standard_NV6</span><span class="sxs-lookup"><span data-stu-id="97039-472">Standard_NV6</span></span>|<span data-ttu-id="97039-473">1</span><span class="sxs-lookup"><span data-stu-id="97039-473">1</span></span>|
|<span data-ttu-id="97039-474">Standard_NV12</span><span class="sxs-lookup"><span data-stu-id="97039-474">Standard_NV12</span></span>|<span data-ttu-id="97039-475">2</span><span class="sxs-lookup"><span data-stu-id="97039-475">2</span></span>|
|<span data-ttu-id="97039-476">Standard_NV24</span><span class="sxs-lookup"><span data-stu-id="97039-476">Standard_NV24</span></span>|<span data-ttu-id="97039-477">4</span><span class="sxs-lookup"><span data-stu-id="97039-477">4</span></span>|

<span data-ttu-id="97039-478">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#nv-series).</span><span class="sxs-lookup"><span data-stu-id="97039-478">For more information, see [GPU optimized virtual machine sizes](../articles/virtual-machines/windows//sizes-gpu.md#nv-series).</span></span>


