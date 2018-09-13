---
title: Experimentation - Azure Cognitive Services | Microsoft Docs
description: This article is a guide for Azure Custom Decision Service experimentation.
services: cognitive-services
author: marco-rossi29
manager: marco-rossi29
ms.service: cognitive-services
ms.topic: article
ms.date: 05/10/2018
ms.author: marossi
ms.openlocfilehash: b0ac0bc049d556423493f0c48dd9a548929bcd41
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969007"
---
# <a name="experimentation"></a><span data-ttu-id="4076b-103">Experimentation</span><span class="sxs-lookup"><span data-stu-id="4076b-103">Experimentation</span></span>

<span data-ttu-id="4076b-104">Following the theory of [contextual bandits (CB)](https://www.microsoft.com/en-us/research/blog/contextual-bandit-breakthrough-enables-deeper-personalization/), Custom Decision Service repeatedly observes a context, takes an action, and observes a reward for the chosen action.</span><span class="sxs-lookup"><span data-stu-id="4076b-104">Following the theory of [contextual bandits (CB)](https://www.microsoft.com/en-us/research/blog/contextual-bandit-breakthrough-enables-deeper-personalization/), Custom Decision Service repeatedly observes a context, takes an action, and observes a reward for the chosen action.</span></span> <span data-ttu-id="4076b-105">An example is content personalization: the context describes a user, actions are candidate stories, and the reward measures how much the user liked the recommended story.</span><span class="sxs-lookup"><span data-stu-id="4076b-105">An example is content personalization: the context describes a user, actions are candidate stories, and the reward measures how much the user liked the recommended story.</span></span>

<span data-ttu-id="4076b-106">Custom Decision Service produces a policy, as it maps from contexts to actions.</span><span class="sxs-lookup"><span data-stu-id="4076b-106">Custom Decision Service produces a policy, as it maps from contexts to actions.</span></span> <span data-ttu-id="4076b-107">With a specific target policy, you want to know its expected reward.</span><span class="sxs-lookup"><span data-stu-id="4076b-107">With a specific target policy, you want to know its expected reward.</span></span> <span data-ttu-id="4076b-108">One way to estimate the reward is to use a policy online and let it choose actions (for example, recommend stories to users).</span><span class="sxs-lookup"><span data-stu-id="4076b-108">One way to estimate the reward is to use a policy online and let it choose actions (for example, recommend stories to users).</span></span> <span data-ttu-id="4076b-109">However, such online evaluation can be costly for two reasons:</span><span class="sxs-lookup"><span data-stu-id="4076b-109">However, such online evaluation can be costly for two reasons:</span></span>

* <span data-ttu-id="4076b-110">It exposes users to an untested, experimental policy.</span><span class="sxs-lookup"><span data-stu-id="4076b-110">It exposes users to an untested, experimental policy.</span></span>
* <span data-ttu-id="4076b-111">It doesn't scale to evaluating multiple target policies.</span><span class="sxs-lookup"><span data-stu-id="4076b-111">It doesn't scale to evaluating multiple target policies.</span></span>

<span data-ttu-id="4076b-112">Off-policy evaluation is an alternative paradigm.</span><span class="sxs-lookup"><span data-stu-id="4076b-112">Off-policy evaluation is an alternative paradigm.</span></span> <span data-ttu-id="4076b-113">If you have logs from an existing online system that follow a logging policy, off-policy evaluation can estimate the expected rewards of new target policies.</span><span class="sxs-lookup"><span data-stu-id="4076b-113">If you have logs from an existing online system that follow a logging policy, off-policy evaluation can estimate the expected rewards of new target policies.</span></span>

<span data-ttu-id="4076b-114">By using the log file, Experimentation seeks to find the policy with the highest estimated, expected reward.</span><span class="sxs-lookup"><span data-stu-id="4076b-114">By using the log file, Experimentation seeks to find the policy with the highest estimated, expected reward.</span></span> <span data-ttu-id="4076b-115">Target policies are parameterized by [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki) arguments.</span><span class="sxs-lookup"><span data-stu-id="4076b-115">Target policies are parameterized by [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki) arguments.</span></span> <span data-ttu-id="4076b-116">In the default mode, the script tests a variety of Vowpal Wabbit arguments by appending to the `--base_command`.</span><span class="sxs-lookup"><span data-stu-id="4076b-116">In the default mode, the script tests a variety of Vowpal Wabbit arguments by appending to the `--base_command`.</span></span> <span data-ttu-id="4076b-117">The script performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="4076b-117">The script performs the following actions:</span></span>

* <span data-ttu-id="4076b-118">Auto-detects features namespaces from the first `--auto_lines` lines of the input file.</span><span class="sxs-lookup"><span data-stu-id="4076b-118">Auto-detects features namespaces from the first `--auto_lines` lines of the input file.</span></span>
* <span data-ttu-id="4076b-119">Performs a first sweep over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`).</span><span class="sxs-lookup"><span data-stu-id="4076b-119">Performs a first sweep over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`).</span></span>
* <span data-ttu-id="4076b-120">Tests policy evaluation `--cb_type` (inverse propensity score (`ips`) or doubly robust (`dr`).</span><span class="sxs-lookup"><span data-stu-id="4076b-120">Tests policy evaluation `--cb_type` (inverse propensity score (`ips`) or doubly robust (`dr`).</span></span> <span data-ttu-id="4076b-121">For more information, see [Contextual Bandit example](https://github.com/JohnLangford/vowpal_wabbit/wiki/Contextual-Bandit-Example).</span><span class="sxs-lookup"><span data-stu-id="4076b-121">For more information, see [Contextual Bandit example](https://github.com/JohnLangford/vowpal_wabbit/wiki/Contextual-Bandit-Example).</span></span>
* <span data-ttu-id="4076b-122">Tests marginals.</span><span class="sxs-lookup"><span data-stu-id="4076b-122">Tests marginals.</span></span>
* <span data-ttu-id="4076b-123">Tests quadratic interaction features:</span><span class="sxs-lookup"><span data-stu-id="4076b-123">Tests quadratic interaction features:</span></span>
   * <span data-ttu-id="4076b-124">**brute-force phase**: Tests all combinations with `--q_bruteforce_terms` pairs or fewer.</span><span class="sxs-lookup"><span data-stu-id="4076b-124">**brute-force phase**: Tests all combinations with `--q_bruteforce_terms` pairs or fewer.</span></span>
   * <span data-ttu-id="4076b-125">**greedy phase**: Adds the best pair until there is no improvement for `--q_greedy_stop` rounds.</span><span class="sxs-lookup"><span data-stu-id="4076b-125">**greedy phase**: Adds the best pair until there is no improvement for `--q_greedy_stop` rounds.</span></span>
* <span data-ttu-id="4076b-126">Performs a second sweep over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`).</span><span class="sxs-lookup"><span data-stu-id="4076b-126">Performs a second sweep over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`).</span></span>

<span data-ttu-id="4076b-127">The parameters that control these steps include some Vowpal Wabbit arguments:</span><span class="sxs-lookup"><span data-stu-id="4076b-127">The parameters that control these steps include some Vowpal Wabbit arguments:</span></span>
- <span data-ttu-id="4076b-128">Example Manipulation options:</span><span class="sxs-lookup"><span data-stu-id="4076b-128">Example Manipulation options:</span></span>
  - <span data-ttu-id="4076b-129">shared namespaces</span><span class="sxs-lookup"><span data-stu-id="4076b-129">shared namespaces</span></span>
  - <span data-ttu-id="4076b-130">action namespaces</span><span class="sxs-lookup"><span data-stu-id="4076b-130">action namespaces</span></span>
  - <span data-ttu-id="4076b-131">marginal namespaces</span><span class="sxs-lookup"><span data-stu-id="4076b-131">marginal namespaces</span></span>
  - <span data-ttu-id="4076b-132">quadratic features</span><span class="sxs-lookup"><span data-stu-id="4076b-132">quadratic features</span></span>
- <span data-ttu-id="4076b-133">Update Rule options</span><span class="sxs-lookup"><span data-stu-id="4076b-133">Update Rule options</span></span>
  - <span data-ttu-id="4076b-134">learning rate</span><span class="sxs-lookup"><span data-stu-id="4076b-134">learning rate</span></span>
  - <span data-ttu-id="4076b-135">L1 regularization</span><span class="sxs-lookup"><span data-stu-id="4076b-135">L1 regularization</span></span>
  - <span data-ttu-id="4076b-136">t power value</span><span class="sxs-lookup"><span data-stu-id="4076b-136">t power value</span></span>

<span data-ttu-id="4076b-137">For an in-depth explanation of the above arguments, see [Vowpal Wabbit command-line arguments](https://github.com/JohnLangford/vowpal_wabbit/wiki/Command-line-arguments).</span><span class="sxs-lookup"><span data-stu-id="4076b-137">For an in-depth explanation of the above arguments, see [Vowpal Wabbit command-line arguments](https://github.com/JohnLangford/vowpal_wabbit/wiki/Command-line-arguments).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4076b-138">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4076b-138">Prerequisites</span></span>
- <span data-ttu-id="4076b-139">Vowpal Wabbit: Installed and on your path.</span><span class="sxs-lookup"><span data-stu-id="4076b-139">Vowpal Wabbit: Installed and on your path.</span></span>
  - <span data-ttu-id="4076b-140">Windows: [Use the `.msi` installer](https://github.com/eisber/vowpal_wabbit/releases).</span><span class="sxs-lookup"><span data-stu-id="4076b-140">Windows: [Use the `.msi` installer](https://github.com/eisber/vowpal_wabbit/releases).</span></span>
  - <span data-ttu-id="4076b-141">Other platforms: [Get the source code](https://github.com/JohnLangford/vowpal_wabbit/releases).</span><span class="sxs-lookup"><span data-stu-id="4076b-141">Other platforms: [Get the source code](https://github.com/JohnLangford/vowpal_wabbit/releases).</span></span>
- <span data-ttu-id="4076b-142">Python 3: Installed and on your path.</span><span class="sxs-lookup"><span data-stu-id="4076b-142">Python 3: Installed and on your path.</span></span>
- <span data-ttu-id="4076b-143">NumPy: Use the package manager of your choice.</span><span class="sxs-lookup"><span data-stu-id="4076b-143">NumPy: Use the package manager of your choice.</span></span>
- <span data-ttu-id="4076b-144">The *Microsoft/mwt-ds* repository: [Clone the repo](https://github.com/Microsoft/mwt-ds).</span><span class="sxs-lookup"><span data-stu-id="4076b-144">The *Microsoft/mwt-ds* repository: [Clone the repo](https://github.com/Microsoft/mwt-ds).</span></span>
- <span data-ttu-id="4076b-145">Decision Service JSON log file: By default, the base command includes `--dsjson`, which enables Decision Service JSON parsing of the input data file.</span><span class="sxs-lookup"><span data-stu-id="4076b-145">Decision Service JSON log file: By default, the base command includes `--dsjson`, which enables Decision Service JSON parsing of the input data file.</span></span> <span data-ttu-id="4076b-146">[Get an example of this format](https://github.com/JohnLangford/vowpal_wabbit/blob/master/test/train-sets/decisionservice.json).</span><span class="sxs-lookup"><span data-stu-id="4076b-146">[Get an example of this format](https://github.com/JohnLangford/vowpal_wabbit/blob/master/test/train-sets/decisionservice.json).</span></span>

## <a name="usage"></a><span data-ttu-id="4076b-147">Usage</span><span class="sxs-lookup"><span data-stu-id="4076b-147">Usage</span></span>
<span data-ttu-id="4076b-148">Go to `mwt-ds/DataScience` and run `Experimentation.py` with the relevant arguments, as detailed in the following code:</span><span class="sxs-lookup"><span data-stu-id="4076b-148">Go to `mwt-ds/DataScience` and run `Experimentation.py` with the relevant arguments, as detailed in the following code:</span></span>

```cmd
python Experimentation.py [-h] -f FILE_PATH [-b BASE_COMMAND] [-p N_PROC]
                          [-s SHARED_NAMESPACES] [-a ACTION_NAMESPACES]
                          [-m MARGINAL_NAMESPACES] [--auto_lines AUTO_LINES]
                          [--only_hp] [-l LR_MIN_MAX_STEPS]
                          [-r REG_MIN_MAX_STEPS] [-t PT_MIN_MAX_STEPS]
                          [--q_bruteforce_terms Q_BRUTEFORCE_TERMS]
                          [--q_greedy_stop Q_GREEDY_STOP]
```

<span data-ttu-id="4076b-149">A log of the results is appended to the  *mwt-ds/DataScience/experiments.csv* file.</span><span class="sxs-lookup"><span data-stu-id="4076b-149">A log of the results is appended to the  *mwt-ds/DataScience/experiments.csv* file.</span></span>

### <a name="parameters"></a><span data-ttu-id="4076b-150">Parameters</span><span class="sxs-lookup"><span data-stu-id="4076b-150">Parameters</span></span>
| <span data-ttu-id="4076b-151">Input</span><span class="sxs-lookup"><span data-stu-id="4076b-151">Input</span></span> | <span data-ttu-id="4076b-152">Description</span><span class="sxs-lookup"><span data-stu-id="4076b-152">Description</span></span> | <span data-ttu-id="4076b-153">Default</span><span class="sxs-lookup"><span data-stu-id="4076b-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4076b-154">`-h`, `--help`</span><span class="sxs-lookup"><span data-stu-id="4076b-154">`-h`, `--help`</span></span> | <span data-ttu-id="4076b-155">Show help message and exit.</span><span class="sxs-lookup"><span data-stu-id="4076b-155">Show help message and exit.</span></span> | |
| <span data-ttu-id="4076b-156">`-f FILE_PATH`, `--file_path FILE_PATH`</span><span class="sxs-lookup"><span data-stu-id="4076b-156">`-f FILE_PATH`, `--file_path FILE_PATH`</span></span> | <span data-ttu-id="4076b-157">Data file path (`.json` or `.json.gz` format - each line is a `dsjson`).</span><span class="sxs-lookup"><span data-stu-id="4076b-157">Data file path (`.json` or `.json.gz` format - each line is a `dsjson`).</span></span> | <span data-ttu-id="4076b-158">Required</span><span class="sxs-lookup"><span data-stu-id="4076b-158">Required</span></span> |  
| <span data-ttu-id="4076b-159">`-b BASE_COMMAND`, `--base_command BASE_COMMAND`</span><span class="sxs-lookup"><span data-stu-id="4076b-159">`-b BASE_COMMAND`, `--base_command BASE_COMMAND`</span></span> | <span data-ttu-id="4076b-160">Base Vowpal Wabbit command.</span><span class="sxs-lookup"><span data-stu-id="4076b-160">Base Vowpal Wabbit command.</span></span>  | `vw --cb_adf --dsjson -c` |  
| <span data-ttu-id="4076b-161">`-p N_PROC`, `--n_proc N_PROC`</span><span class="sxs-lookup"><span data-stu-id="4076b-161">`-p N_PROC`, `--n_proc N_PROC`</span></span> | <span data-ttu-id="4076b-162">Number of parallel processes to use.</span><span class="sxs-lookup"><span data-stu-id="4076b-162">Number of parallel processes to use.</span></span> | <span data-ttu-id="4076b-163">Logical processors</span><span class="sxs-lookup"><span data-stu-id="4076b-163">Logical processors</span></span> |  
| `-s SHARED_NAMESPACES, --shared_namespaces SHARED_NAMESPACES` | <span data-ttu-id="4076b-164">Shared feature namespaces (for example, `abc` means namespaces `a`, `b`, and `c`).</span><span class="sxs-lookup"><span data-stu-id="4076b-164">Shared feature namespaces (for example, `abc` means namespaces `a`, `b`, and `c`).</span></span>  | <span data-ttu-id="4076b-165">Auto-detect from data file</span><span class="sxs-lookup"><span data-stu-id="4076b-165">Auto-detect from data file</span></span> |  
| `-a ACTION_NAMESPACES, --action_namespaces ACTION_NAMESPACES` | <span data-ttu-id="4076b-166">Action feature namespaces.</span><span class="sxs-lookup"><span data-stu-id="4076b-166">Action feature namespaces.</span></span> | <span data-ttu-id="4076b-167">Auto-detect from data file</span><span class="sxs-lookup"><span data-stu-id="4076b-167">Auto-detect from data file</span></span> |  
| `-m MARGINAL_NAMESPACES, --marginal_namespaces MARGINAL_NAMESPACES` | <span data-ttu-id="4076b-168">Marginal feature namespaces.</span><span class="sxs-lookup"><span data-stu-id="4076b-168">Marginal feature namespaces.</span></span> | <span data-ttu-id="4076b-169">Auto-detect from data file</span><span class="sxs-lookup"><span data-stu-id="4076b-169">Auto-detect from data file</span></span> |  
| `--auto_lines AUTO_LINES` | <span data-ttu-id="4076b-170">Number of data file lines to scan to auto-detect features namespaces.</span><span class="sxs-lookup"><span data-stu-id="4076b-170">Number of data file lines to scan to auto-detect features namespaces.</span></span> | `100` |  
| `--only_hp` | <span data-ttu-id="4076b-171">Sweep only over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`).</span><span class="sxs-lookup"><span data-stu-id="4076b-171">Sweep only over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`).</span></span> | `False` |  
| <span data-ttu-id="4076b-172">`-l LR_MIN_MAX_STEPS`, `--lr_min_max_steps LR_MIN_MAX_STEPS`</span><span class="sxs-lookup"><span data-stu-id="4076b-172">`-l LR_MIN_MAX_STEPS`, `--lr_min_max_steps LR_MIN_MAX_STEPS`</span></span> | <span data-ttu-id="4076b-173">Learning rate range as positive values `min,max,steps`.</span><span class="sxs-lookup"><span data-stu-id="4076b-173">Learning rate range as positive values `min,max,steps`.</span></span> | `1e-5,0.5,4` |  
| <span data-ttu-id="4076b-174">`-r REG_MIN_MAX_STEPS`, `--reg_min_max_steps REG_MIN_MAX_STEPS`</span><span class="sxs-lookup"><span data-stu-id="4076b-174">`-r REG_MIN_MAX_STEPS`, `--reg_min_max_steps REG_MIN_MAX_STEPS`</span></span> | <span data-ttu-id="4076b-175">L1 regularization range as positive values `min,max,steps`.</span><span class="sxs-lookup"><span data-stu-id="4076b-175">L1 regularization range as positive values `min,max,steps`.</span></span> | `1e-9,0.1,5` |  
| <span data-ttu-id="4076b-176">`-t PT_MIN_MAX_STEPS`, `--pt_min_max_steps PT_MIN_MAX_STEPS`</span><span class="sxs-lookup"><span data-stu-id="4076b-176">`-t PT_MIN_MAX_STEPS`, `--pt_min_max_steps PT_MIN_MAX_STEPS`</span></span> | <span data-ttu-id="4076b-177">Power_t range as positive values `min,max,step`.</span><span class="sxs-lookup"><span data-stu-id="4076b-177">Power_t range as positive values `min,max,step`.</span></span> | `1e-9,0.5,5` |  
| `--q_bruteforce_terms Q_BRUTEFORCE_TERMS` | <span data-ttu-id="4076b-178">Number of quadratic pairs to test in brute-force phase.</span><span class="sxs-lookup"><span data-stu-id="4076b-178">Number of quadratic pairs to test in brute-force phase.</span></span> | `2` |  
| `--q_greedy_stop Q_GREEDY_STOP` | <span data-ttu-id="4076b-179">Rounds without improvements, after which quadratic greedy search phase is halted.</span><span class="sxs-lookup"><span data-stu-id="4076b-179">Rounds without improvements, after which quadratic greedy search phase is halted.</span></span> | `3` |  

### <a name="examples"></a><span data-ttu-id="4076b-180">Examples</span><span class="sxs-lookup"><span data-stu-id="4076b-180">Examples</span></span>
<span data-ttu-id="4076b-181">To use the preset default values:</span><span class="sxs-lookup"><span data-stu-id="4076b-181">To use the preset default values:</span></span>
```cmd
python Experimentation.py -f D:\multiworld\data.json
```

<span data-ttu-id="4076b-182">Equivalently, Vowpal Wabbit can also ingest `.json.gz` files:</span><span class="sxs-lookup"><span data-stu-id="4076b-182">Equivalently, Vowpal Wabbit can also ingest `.json.gz` files:</span></span>
```cmd
python Experimentation.py -f D:\multiworld\data.json.gz
```

<span data-ttu-id="4076b-183">To sweep only over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`, stopping after step 2):</span><span class="sxs-lookup"><span data-stu-id="4076b-183">To sweep only over hyper-parameters (`learning rate`, `L1 regularization`, and `power_t`, stopping after step 2):</span></span>
```cmd
python Experimentation.py -f D:\multiworld\data.json --only_hp
```
