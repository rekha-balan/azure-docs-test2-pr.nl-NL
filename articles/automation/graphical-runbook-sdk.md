---
title: Overview of the Azure Automation Grpahical runbook SDK
description: This article describes how to use the Azure Automation Graphical Runbook SDK
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 07/20/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 702af8311887afc94e7127704d3377e944503324
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966593"
---
# <a name="use-the-azure-automation-graphical-runbook-sdk"></a><span data-ttu-id="69f3e-103">Use the Azure Automation Graphical runbook SDK</span><span class="sxs-lookup"><span data-stu-id="69f3e-103">Use the Azure Automation Graphical runbook SDK</span></span>

<span data-ttu-id="69f3e-104">[Graphical runbooks](automation-graphical-authoring-intro.md) are runbooks that help manage the complexities of the underlying Windows PowerShell or PowerShell Workflow code.</span><span class="sxs-lookup"><span data-stu-id="69f3e-104">[Graphical runbooks](automation-graphical-authoring-intro.md) are runbooks that help manage the complexities of the underlying Windows PowerShell or PowerShell Workflow code.</span></span> <span data-ttu-id="69f3e-105">The Microsoft Azure Automation Graphical Authoring SDK enables developers to create and edit Graphical Runbooks for use with the Azure Automation service.</span><span class="sxs-lookup"><span data-stu-id="69f3e-105">The Microsoft Azure Automation Graphical Authoring SDK enables developers to create and edit Graphical Runbooks for use with the Azure Automation service.</span></span> <span data-ttu-id="69f3e-106">The following code snippets show the basic flow of creating a graphical runbook from your code.</span><span class="sxs-lookup"><span data-stu-id="69f3e-106">The following code snippets show the basic flow of creating a graphical runbook from your code.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="69f3e-107">Pre-requisites</span><span class="sxs-lookup"><span data-stu-id="69f3e-107">Pre-requisites</span></span>

<span data-ttu-id="69f3e-108">To start, import the `Microsoft.Azure.Automation.GraphicalRunbook.Model` package into your project.</span><span class="sxs-lookup"><span data-stu-id="69f3e-108">To start, import the `Microsoft.Azure.Automation.GraphicalRunbook.Model` package into your project.</span></span>

## <a name="create-a-runbook-object-instance"></a><span data-ttu-id="69f3e-109">Create a runbook object instance</span><span class="sxs-lookup"><span data-stu-id="69f3e-109">Create a runbook object instance</span></span>

<span data-ttu-id="69f3e-110">Reference the `Orchestrator.GraphRunbook.Model` assembly and create an instance of the `Orchestrator.GraphRunbook.Model.GraphRunbook` class:</span><span class="sxs-lookup"><span data-stu-id="69f3e-110">Reference the `Orchestrator.GraphRunbook.Model` assembly and create an instance of the `Orchestrator.GraphRunbook.Model.GraphRunbook` class:</span></span>

```csharp
using Orchestrator.GraphRunbook.Model;
using Orchestrator.GraphRunbook.Model.ExecutableView;

var runbook = new GraphRunbook();
```

## <a name="add-runbook-parameters"></a><span data-ttu-id="69f3e-111">Add runbook parameters</span><span class="sxs-lookup"><span data-stu-id="69f3e-111">Add runbook parameters</span></span>

<span data-ttu-id="69f3e-112">Instantiate `Orchestrator.GraphRunbook.Model.Parameter` objects and add them to the runbook:</span><span class="sxs-lookup"><span data-stu-id="69f3e-112">Instantiate `Orchestrator.GraphRunbook.Model.Parameter` objects and add them to the runbook:</span></span>

```csharp
runbook.AddParameter(
 new Parameter("YourName") {
  TypeName = typeof(string).FullName,
   DefaultValue = "World",
   Optional = true
 });

runbook.AddParameter(
 new Parameter("AnotherParameter") {
  TypeName = typeof(int).FullName, ...
 });
```

## <a name="add-activities-and-links"></a><span data-ttu-id="69f3e-113">Add activities and links</span><span class="sxs-lookup"><span data-stu-id="69f3e-113">Add activities and links</span></span>

<span data-ttu-id="69f3e-114">Instantiate activities of appropriate types and add them to the runbook:</span><span class="sxs-lookup"><span data-stu-id="69f3e-114">Instantiate activities of appropriate types and add them to the runbook:</span></span>

```csharp
var writeOutputActivityType = new CommandActivityType {
 CommandName = "Write-Output",
  ModuleName = "Microsoft.PowerShell.Utility",
 InputParameterSets = new [] {
  new ParameterSet {
   Name = "Default",
    new [] {
     new Parameter("InputObject"), ...
    }
  },
  ...
 }
};

var outputName = runbook.AddActivity(
 new CommandActivity("Output name", writeOutputActivityType) {
  ParameterSetName = "Default",
   Parameters = new ActivityParameters {
    {
     "InputObject",
     new RunbookParameterValueDescriptor("YourName")
    }
   },
   PositionX = 0,
   PositionY = 0
 });

var initializeRunbookVariable = runbook.AddActivity(
 new WorkflowScriptActivity("Initialize variable") {
  Process = "$a = 0",
   PositionX = 0,
   PositionY = 100
 });
```

<span data-ttu-id="69f3e-115">Activities are implemented by the following classes in the `Orchestrator.GraphRunbook.Model` namespace:</span><span class="sxs-lookup"><span data-stu-id="69f3e-115">Activities are implemented by the following classes in the `Orchestrator.GraphRunbook.Model` namespace:</span></span>

|<span data-ttu-id="69f3e-116">Class</span><span class="sxs-lookup"><span data-stu-id="69f3e-116">Class</span></span>  |<span data-ttu-id="69f3e-117">Activity</span><span class="sxs-lookup"><span data-stu-id="69f3e-117">Activity</span></span>  |
|---------|---------|
|<span data-ttu-id="69f3e-118">CommandActivity</span><span class="sxs-lookup"><span data-stu-id="69f3e-118">CommandActivity</span></span>     | <span data-ttu-id="69f3e-119">Invokes a PowerShell command (cmdlet, function, etc.).</span><span class="sxs-lookup"><span data-stu-id="69f3e-119">Invokes a PowerShell command (cmdlet, function, etc.).</span></span>        |
|<span data-ttu-id="69f3e-120">InvokeRunbookActivity</span><span class="sxs-lookup"><span data-stu-id="69f3e-120">InvokeRunbookActivity</span></span>     | <span data-ttu-id="69f3e-121">Invokes another runbook inline.</span><span class="sxs-lookup"><span data-stu-id="69f3e-121">Invokes another runbook inline.</span></span>        |
|<span data-ttu-id="69f3e-122">JunctionActivity</span><span class="sxs-lookup"><span data-stu-id="69f3e-122">JunctionActivity</span></span>     | <span data-ttu-id="69f3e-123">Waits for all incoming branches to finish.</span><span class="sxs-lookup"><span data-stu-id="69f3e-123">Waits for all incoming branches to finish.</span></span>        |
|<span data-ttu-id="69f3e-124">WorkflowScriptActivity</span><span class="sxs-lookup"><span data-stu-id="69f3e-124">WorkflowScriptActivity</span></span>     | <span data-ttu-id="69f3e-125">Executes a block of PowerShell or PowerShell Workflow code (depending on the runbook type) in the context of the runbook.</span><span class="sxs-lookup"><span data-stu-id="69f3e-125">Executes a block of PowerShell or PowerShell Workflow code (depending on the runbook type) in the context of the runbook.</span></span> <span data-ttu-id="69f3e-126">This is a powerful tool, but do not overuse it: the UI will show this script block as text; the execution engine will treat the provided block as a black box, and will make no attempts to analyze its content, except for a basic syntax check.</span><span class="sxs-lookup"><span data-stu-id="69f3e-126">This is a powerful tool, but do not overuse it: the UI will show this script block as text; the execution engine will treat the provided block as a black box, and will make no attempts to analyze its content, except for a basic syntax check.</span></span> <span data-ttu-id="69f3e-127">If you just need to invoke a single PowerShell command, prefer CommandActivity.</span><span class="sxs-lookup"><span data-stu-id="69f3e-127">If you just need to invoke a single PowerShell command, prefer CommandActivity.</span></span>        |

> [!NOTE]
> <span data-ttu-id="69f3e-128">Do not derive your own activities from the provided classes: Azure Automation will not be able to use runbooks with custom activity types.</span><span class="sxs-lookup"><span data-stu-id="69f3e-128">Do not derive your own activities from the provided classes: Azure Automation will not be able to use runbooks with custom activity types.</span></span>

<span data-ttu-id="69f3e-129">CommandActivity and InvokeRunbookActivity parameters must be provided as value descriptors, not direct values.</span><span class="sxs-lookup"><span data-stu-id="69f3e-129">CommandActivity and InvokeRunbookActivity parameters must be provided as value descriptors, not direct values.</span></span> <span data-ttu-id="69f3e-130">Value descriptors specify how the actual parameter values should be produced.</span><span class="sxs-lookup"><span data-stu-id="69f3e-130">Value descriptors specify how the actual parameter values should be produced.</span></span> <span data-ttu-id="69f3e-131">The following value descriptors are currently provided:</span><span class="sxs-lookup"><span data-stu-id="69f3e-131">The following value descriptors are currently provided:</span></span>


|<span data-ttu-id="69f3e-132">Descriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-132">Descriptor</span></span>  |<span data-ttu-id="69f3e-133">Definition</span><span class="sxs-lookup"><span data-stu-id="69f3e-133">Definition</span></span>  |
|---------|---------|
|<span data-ttu-id="69f3e-134">ConstantValueDescriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-134">ConstantValueDescriptor</span></span>     | <span data-ttu-id="69f3e-135">Refers to a hard-coded constant value.</span><span class="sxs-lookup"><span data-stu-id="69f3e-135">Refers to a hard-coded constant value.</span></span>        |
|<span data-ttu-id="69f3e-136">RunbookParameterValueDescriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-136">RunbookParameterValueDescriptor</span></span>     | <span data-ttu-id="69f3e-137">Refers to a runbook parameter by name.</span><span class="sxs-lookup"><span data-stu-id="69f3e-137">Refers to a runbook parameter by name.</span></span>        |
|<span data-ttu-id="69f3e-138">ActivityOutputValueDescriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-138">ActivityOutputValueDescriptor</span></span>     | <span data-ttu-id="69f3e-139">Refers to an upstream activity output, allowing one activity to "subscribe" to data produced by another activity.</span><span class="sxs-lookup"><span data-stu-id="69f3e-139">Refers to an upstream activity output, allowing one activity to "subscribe" to data produced by another activity.</span></span>        |
|<span data-ttu-id="69f3e-140">AutomationVariableValueDescriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-140">AutomationVariableValueDescriptor</span></span>     | <span data-ttu-id="69f3e-141">Refers to an Automation Variable asset by name.</span><span class="sxs-lookup"><span data-stu-id="69f3e-141">Refers to an Automation Variable asset by name.</span></span>         |
|<span data-ttu-id="69f3e-142">AutomationCredentialValueDescriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-142">AutomationCredentialValueDescriptor</span></span>     | <span data-ttu-id="69f3e-143">Refers to an Automation Certificate asset by name.</span><span class="sxs-lookup"><span data-stu-id="69f3e-143">Refers to an Automation Certificate asset by name.</span></span>        |
|<span data-ttu-id="69f3e-144">AutomationConnectionValueDescriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-144">AutomationConnectionValueDescriptor</span></span>     | <span data-ttu-id="69f3e-145">Refers to an Automation Connection asset by name.</span><span class="sxs-lookup"><span data-stu-id="69f3e-145">Refers to an Automation Connection asset by name.</span></span>        |
|<span data-ttu-id="69f3e-146">PowerShellExpressionValueDescriptor</span><span class="sxs-lookup"><span data-stu-id="69f3e-146">PowerShellExpressionValueDescriptor</span></span>     | <span data-ttu-id="69f3e-147">Specifies a free-form PowerShell expression that will be evaluated just before invoking the activity.</span><span class="sxs-lookup"><span data-stu-id="69f3e-147">Specifies a free-form PowerShell expression that will be evaluated just before invoking the activity.</span></span>  <br/><span data-ttu-id="69f3e-148">This is a powerful tool, but do not overuse it: the UI will show this expression as text; the execution engine will treat the provided block as a black box, and will make no attempts to analyze its content, except for a basic syntax check.</span><span class="sxs-lookup"><span data-stu-id="69f3e-148">This is a powerful tool, but do not overuse it: the UI will show this expression as text; the execution engine will treat the provided block as a black box, and will make no attempts to analyze its content, except for a basic syntax check.</span></span> <span data-ttu-id="69f3e-149">When possible, prefer more specific value descriptors.</span><span class="sxs-lookup"><span data-stu-id="69f3e-149">When possible, prefer more specific value descriptors.</span></span>      |

> [!NOTE]
> <span data-ttu-id="69f3e-150">Do not derive your own value descriptors from the provided classes: Azure Automation will not be able to use runbooks with custom value descriptor types.</span><span class="sxs-lookup"><span data-stu-id="69f3e-150">Do not derive your own value descriptors from the provided classes: Azure Automation will not be able to use runbooks with custom value descriptor types.</span></span>

<span data-ttu-id="69f3e-151">Instantiate links connecting activities and add them to the runbook:</span><span class="sxs-lookup"><span data-stu-id="69f3e-151">Instantiate links connecting activities and add them to the runbook:</span></span>

```csharp
runbook.AddLink(new Link(activityA, activityB, LinkType.Sequence));

runbook.AddLink(
 new Link(activityB, activityC, LinkType.Pipeline) {
  Condition = string.Format("$ActivityOutput['{0}'] -gt 0", activityB.Name)
 });
```

## <a name="save-the-runbook-to-a-file"></a><span data-ttu-id="69f3e-152">Save the runbook to a file</span><span class="sxs-lookup"><span data-stu-id="69f3e-152">Save the runbook to a file</span></span>

<span data-ttu-id="69f3e-153">Use `Orchestrator.GraphRunbook.Model.Serialization.RunbookSerializer` to serialize a runbook to a string:</span><span class="sxs-lookup"><span data-stu-id="69f3e-153">Use `Orchestrator.GraphRunbook.Model.Serialization.RunbookSerializer` to serialize a runbook to a string:</span></span>

```csharp
var serialized = RunbookSerializer.Serialize(runbook);
```

<span data-ttu-id="69f3e-154">This string can be saved to a file with the **.graphrunbook** extension, and this file can be imported into Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="69f3e-154">This string can be saved to a file with the **.graphrunbook** extension, and this file can be imported into Azure Automation.</span></span>
<span data-ttu-id="69f3e-155">The serialized format may change in the future versions of `Orchestrator.GraphRunbook.Model.dll`.</span><span class="sxs-lookup"><span data-stu-id="69f3e-155">The serialized format may change in the future versions of `Orchestrator.GraphRunbook.Model.dll`.</span></span> <span data-ttu-id="69f3e-156">We promise backward compatibility: any runbook serialized with an older version of `Orchestrator.GraphRunbook.Model.dll` can be deserialized by any newer version.</span><span class="sxs-lookup"><span data-stu-id="69f3e-156">We promise backward compatibility: any runbook serialized with an older version of `Orchestrator.GraphRunbook.Model.dll` can be deserialized by any newer version.</span></span> <span data-ttu-id="69f3e-157">Forward compatibility is not guaranteed: a runbook serialized with a newer version may not be deserializable by older versions.</span><span class="sxs-lookup"><span data-stu-id="69f3e-157">Forward compatibility is not guaranteed: a runbook serialized with a newer version may not be deserializable by older versions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69f3e-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="69f3e-158">Next steps</span></span>

<span data-ttu-id="69f3e-159">To learn more about Graphical Runbooks in Azure Automation, see [Graphical Authoring introduction](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="69f3e-159">To learn more about Graphical Runbooks in Azure Automation, see [Graphical Authoring introduction](automation-graphical-authoring-intro.md)</span></span>
