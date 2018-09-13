---
title: Azure CredentialsCombo UI element | Microsoft Docs
description: Describes the Microsoft.Compute.CredentialsCombo UI element for Azure portal.
services: managed-applications
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: managed-applications
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2018
ms.author: tomfitz
ms.openlocfilehash: 183075f7407b0a0ca6ea53871e239ab8c2d89490
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870440"
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="6040e-103">Microsoft.Compute.CredentialsCombo UI element</span><span class="sxs-lookup"><span data-stu-id="6040e-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="6040e-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span><span class="sxs-lookup"><span data-stu-id="6040e-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6040e-105">UI sample</span><span class="sxs-lookup"><span data-stu-id="6040e-105">UI sample</span></span>

<span data-ttu-id="6040e-106">For Windows, users see:</span><span class="sxs-lookup"><span data-stu-id="6040e-106">For Windows, users see:</span></span>

![Microsoft.Compute.CredentialsCombo Windows](./media/managed-application-elements/microsoft.compute.credentialscombo-windows.png)

<span data-ttu-id="6040e-108">For Linux with password selected, users see:</span><span class="sxs-lookup"><span data-stu-id="6040e-108">For Linux with password selected, users see:</span></span>

![Microsoft.Compute.CredentialsCombo Linux password](./media/managed-application-elements/microsoft.compute.credentialscombo-linux-password.png)

<span data-ttu-id="6040e-110">For Linux with SSH public key selected, users see:</span><span class="sxs-lookup"><span data-stu-id="6040e-110">For Linux with SSH public key selected, users see:</span></span>

![Microsoft.Compute.CredentialsCombo Linux key](./media/managed-application-elements/microsoft.compute.credentialscombo-linux-key.png)

## <a name="schema"></a><span data-ttu-id="6040e-112">Schema</span><span class="sxs-lookup"><span data-stu-id="6040e-112">Schema</span></span>
<span data-ttu-id="6040e-113">For Windows, use the following schema:</span><span class="sxs-lookup"><span data-stu-id="6040e-113">For Windows, use the following schema:</span></span>

```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="6040e-114">For **Linux**, use the following schema:</span><span class="sxs-lookup"><span data-stu-id="6040e-114">For **Linux**, use the following schema:</span></span>

```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6040e-115">Remarks</span><span class="sxs-lookup"><span data-stu-id="6040e-115">Remarks</span></span>
- <span data-ttu-id="6040e-116">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="6040e-116">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="6040e-117">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must have values to validate successfully.</span><span class="sxs-lookup"><span data-stu-id="6040e-117">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must have values to validate successfully.</span></span> <span data-ttu-id="6040e-118">The default value is **true**.</span><span class="sxs-lookup"><span data-stu-id="6040e-118">The default value is **true**.</span></span>
- <span data-ttu-id="6040e-119">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span><span class="sxs-lookup"><span data-stu-id="6040e-119">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="6040e-120">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="6040e-120">The default value is **false**.</span></span>
- <span data-ttu-id="6040e-121">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span><span class="sxs-lookup"><span data-stu-id="6040e-121">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="6040e-122">It can be used only when `osPlatform` is **Linux**.</span><span class="sxs-lookup"><span data-stu-id="6040e-122">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="6040e-123">The default value is **false**.</span><span class="sxs-lookup"><span data-stu-id="6040e-123">The default value is **false**.</span></span>
- <span data-ttu-id="6040e-124">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span><span class="sxs-lookup"><span data-stu-id="6040e-124">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="6040e-125">The string in `customValidationMessage` is displayed when a password fails custom validation.</span><span class="sxs-lookup"><span data-stu-id="6040e-125">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="6040e-126">The default value for both properties is **null**.</span><span class="sxs-lookup"><span data-stu-id="6040e-126">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6040e-127">Sample output</span><span class="sxs-lookup"><span data-stu-id="6040e-127">Sample output</span></span>
<span data-ttu-id="6040e-128">If `osPlatform` is **Windows**, or `osPlatform` is **Linux** and the user provided a password instead of an SSH public key, the control returns the following output:</span><span class="sxs-lookup"><span data-stu-id="6040e-128">If `osPlatform` is **Windows**, or `osPlatform` is **Linux** and the user provided a password instead of an SSH public key, the control returns the following output:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="6040e-129">If `osPlatform` is **Linux** and the user provided an SSH public key, the control returns the following output:</span><span class="sxs-lookup"><span data-stu-id="6040e-129">If `osPlatform` is **Linux** and the user provided an SSH public key, the control returns the following output:</span></span>

```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="6040e-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="6040e-130">Next steps</span></span>
* <span data-ttu-id="6040e-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6040e-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](create-uidefinition-overview.md).</span></span>
* <span data-ttu-id="6040e-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="6040e-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](create-uidefinition-elements.md).</span></span>
