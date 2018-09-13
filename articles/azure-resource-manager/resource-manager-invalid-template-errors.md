---
title: Azure invalid template errors | Microsoft Docs
description: Describes how to resolve invalid template errors.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 03/08/2018
ms.author: tomfitz
ms.openlocfilehash: 59f07b9ba8116cb1a4b5ab50382d89d01a78853b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866387"
---
# <a name="resolve-errors-for-invalid-template"></a>Resolve errors for invalid template

This article describes how to resolve invalid template errors.

## <a name="symptom"></a>Symptom

When deploying a template, you receive an error indicating:

```
Code=InvalidTemplate
Message=<varies>
```

The error message depends on the type of error.

## <a name="cause"></a>Cause

This error can result from several different types of errors. They usually involve a syntax or structural error in the template.

<a id="syntax-error" />

## <a name="solution-1---syntax-error"></a>Solution 1 - syntax error

If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.

```
Code=InvalidTemplate
Message=Deployment template validation failed
```

This error is easy to make because template expressions can be intricate. For example, the following name assignment for a storage account has one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
```

If you don't provide the matching syntax, the template produces a value that is different than your intention.

When you receive this type of error, carefully review the expression syntax. Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.

<a id="incorrect-segment-lengths" />

## <a name="solution-2---incorrect-segment-lengths"></a>Solution 2 - incorrect segment lengths

Another invalid template error occurs when the resource name isn't in the correct format.

```
Code=InvalidTemplate
Message=Deployment template validation failed: 'The template resource {resource-name}'
for type {resource-type} has incorrect segment lengths.
```

A root level resource must have one less segment in the name than in the resource type. Each segment is differentiated by a slash. In the following example, the type has two segments and the name has one segment, so it's a **valid name**.

```json
{
  "type": "Microsoft.Web/serverfarms",
  "name": "myHostingPlanName",
  ...
}
```

But the next example is **not a valid name** because it has the same number of segments as the type.

```json
{
  "type": "Microsoft.Web/serverfarms",
  "name": "appPlan/myHostingPlanName",
  ...
}
```

For child resources, the type and name have the same number of segments. This number of segments makes sense because the full name and type for the child includes the parent name and type. Therefore, the full name still has one less segment than the full type.

```json
"resources": [
    {
        "type": "Microsoft.KeyVault/vaults",
        "name": "contosokeyvault",
        ...
        "resources": [
            {
                "type": "secrets",
                "name": "appPassword",
                ...
            }
        ]
    }
]
```

Getting the segments right can be tricky with Resource Manager types that are applied across resource providers. For example, applying a resource lock to a web site requires a type with four segments. Therefore, the name is three segments:

```json
{
    "type": "Microsoft.Web/sites/providers/locks",
    "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
    ...
}
```

<a id="parameter-not-valid" />

## <a name="solution-3---parameter-is-not-valid"></a>Solution 3 - parameter is not valid

If you provide a parameter value that is not one of the allowed values, you receive a message similar to the following error:

```
Code=InvalidTemplate;
Message=Deployment template validation failed: 'The provided value {parameter value}
for the template parameter {parameter name} is not valid. The parameter value is not
part of the allowed values
```

Double check the allowed values in the template, and provide one during deployment. For more information about allowed parameter values, see [Parameters section of Azure Resource Manager templates](resource-manager-templates-parameters.md).

<a id="too-many-resource-groups" />

## <a name="solution-4---too-many-target-resource-groups"></a>Solution 4 - Too many target resource groups

If you specify more than five target resource groups in a single deployment, you receive this error. Consider either consolidating the number of resource groups in your deployment, or deploying some of the templates as separate deployments. For more information, see [Deploy Azure resources to more than one subscription or resource group](resource-manager-cross-resource-group-deployment.md).

<a id="circular-dependency" />

## <a name="solution-5---circular-dependency-detected"></a>Solution 5 - circular dependency detected

You receive this error when resources depend on each other in a way that prevents the deployment from starting. A combination of interdependencies makes two or more resource wait for other resources that are also waiting. For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2. You can usually solve this problem by removing unnecessary dependencies.

To solve a circular dependency:

1. In your template, find the resource identified in the circular dependency. 
2. For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on. 
3. Examine those resources to see which resources they depend on. Follow the dependencies until you notice a resource that depends on the original resource.
5. For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed. Remove those dependencies. If you are unsure that a dependency is needed, try removing it. 
6. Redeploy the template.

Removing values from the **dependsOn** property can cause errors when you deploy the template. If you get an error, add the dependency back into the template. 

If that approach doesn't solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings). Configure those child resources to deploy after the resources involved in the circular dependency. For example, suppose you're deploying two virtual machines but you must set properties on each one that refer to the other. You can deploy them in the following order:

1. vm1
2. vm2
3. Extension on vm1 depends on vm1 and vm2. The extension sets values on vm1 that it gets from vm2.
4. Extension on vm2 depends on vm1 and vm2. The extension sets values on vm2 that it gets from vm1.

The same approach works for App Service apps. Consider moving configuration values into a child resource of the app resource. You can deploy two web apps in the following order:

1. webapp1
2. webapp2
3. config for webapp1 depends on webapp1 and webapp2. It contains app settings with values from webapp2.
4. config for webapp2 depends on webapp1 and webapp2. It contains app settings with values from webapp1.