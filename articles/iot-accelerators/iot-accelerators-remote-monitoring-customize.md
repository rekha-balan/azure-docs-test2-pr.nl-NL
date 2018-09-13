---
title: Customize the Remote Monitoring solution UI - Azure | Microsoft Docs
description: This article provides information about how you can access the source code for the Remote Monitoring solution accelerator UI and make some customizations.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 36e63d26bf7ada2d23fa3cd9fddbb5ba90494527
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857598"
---
# <a name="customize-the-remote-monitoring-solution-accelerator"></a><span data-ttu-id="404b3-103">Customize the Remote Monitoring solution accelerator</span><span class="sxs-lookup"><span data-stu-id="404b3-103">Customize the Remote Monitoring solution accelerator</span></span>

<span data-ttu-id="404b3-104">This article provides information about how you can access the source code and customize the Remote Monitoring solution accelerator UI.</span><span class="sxs-lookup"><span data-stu-id="404b3-104">This article provides information about how you can access the source code and customize the Remote Monitoring solution accelerator UI.</span></span> <span data-ttu-id="404b3-105">The article describes:</span><span class="sxs-lookup"><span data-stu-id="404b3-105">The article describes:</span></span>

## <a name="prepare-a-local-development-environment-for-the-ui"></a><span data-ttu-id="404b3-106">Prepare a local development environment for the UI</span><span class="sxs-lookup"><span data-stu-id="404b3-106">Prepare a local development environment for the UI</span></span>

<span data-ttu-id="404b3-107">The Remote Monitoring solution accelerator UI code is implemented using the React.js framework.</span><span class="sxs-lookup"><span data-stu-id="404b3-107">The Remote Monitoring solution accelerator UI code is implemented using the React.js framework.</span></span> <span data-ttu-id="404b3-108">You can find the source code in the [azure-iot-pcs-remote-monitoring-webui](https://github.com/Azure/azure-iot-pcs-remote-monitoring-webui) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="404b3-108">You can find the source code in the [azure-iot-pcs-remote-monitoring-webui](https://github.com/Azure/azure-iot-pcs-remote-monitoring-webui) GitHub repository.</span></span>

<span data-ttu-id="404b3-109">To make changes to the UI, you can run a copy of it locally.</span><span class="sxs-lookup"><span data-stu-id="404b3-109">To make changes to the UI, you can run a copy of it locally.</span></span> <span data-ttu-id="404b3-110">The local copy connects to a deployed instance of the solution to perform actions such as retrieving telemetry.</span><span class="sxs-lookup"><span data-stu-id="404b3-110">The local copy connects to a deployed instance of the solution to perform actions such as retrieving telemetry.</span></span>

<span data-ttu-id="404b3-111">The following steps outline the process to set up a local environment for UI development:</span><span class="sxs-lookup"><span data-stu-id="404b3-111">The following steps outline the process to set up a local environment for UI development:</span></span>

1. <span data-ttu-id="404b3-112">Deploy a **basic** instance of the solution accelerator using the **pcs** CLI.</span><span class="sxs-lookup"><span data-stu-id="404b3-112">Deploy a **basic** instance of the solution accelerator using the **pcs** CLI.</span></span> <span data-ttu-id="404b3-113">Make a note of the name of your deployment and the credentials you provided for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="404b3-113">Make a note of the name of your deployment and the credentials you provided for the virtual machine.</span></span> <span data-ttu-id="404b3-114">For more information, see [Deploy using the CLI](iot-accelerators-remote-monitoring-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="404b3-114">For more information, see [Deploy using the CLI](iot-accelerators-remote-monitoring-deploy-cli.md).</span></span>

1. <span data-ttu-id="404b3-115">Use the Azure portal or the [az CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)  to enable SSH access to the virtual machine that hosts the microservices in your solution.</span><span class="sxs-lookup"><span data-stu-id="404b3-115">Use the Azure portal or the [az CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)  to enable SSH access to the virtual machine that hosts the microservices in your solution.</span></span> <span data-ttu-id="404b3-116">For example:</span><span class="sxs-lookup"><span data-stu-id="404b3-116">For example:</span></span>

    ```sh
    az network nsg rule update --name SSH --nsg-name {your solution name}-nsg --resource-group {your solution name} --access Allow
    ```

    <span data-ttu-id="404b3-117">You should only enable SSH access during test and development.</span><span class="sxs-lookup"><span data-stu-id="404b3-117">You should only enable SSH access during test and development.</span></span> <span data-ttu-id="404b3-118">If you enable SSH, [you should disable it again as soon as possible](../security/azure-security-network-security-best-practices.md#disable-rdpssh-access-to-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="404b3-118">If you enable SSH, [you should disable it again as soon as possible](../security/azure-security-network-security-best-practices.md#disable-rdpssh-access-to-azure-virtual-machines).</span></span>

1. <span data-ttu-id="404b3-119">Use the Azure portal or the [az CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) to find the name and public IP address of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="404b3-119">Use the Azure portal or the [az CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) to find the name and public IP address of your virtual machine.</span></span> <span data-ttu-id="404b3-120">For example:</span><span class="sxs-lookup"><span data-stu-id="404b3-120">For example:</span></span>

    ```sh
    az resource list --resource-group {your solution name} -o table
    az vm list-ip-addresses --name {your vm name from previous command} --resource-group {your solution name} -o table
    ```

1. <span data-ttu-id="404b3-121">Use SSH to connect to your virtual machine using the IP address from the previous step, and the credentials you provided when you ran **pcs** to deploy the solution.</span><span class="sxs-lookup"><span data-stu-id="404b3-121">Use SSH to connect to your virtual machine using the IP address from the previous step, and the credentials you provided when you ran **pcs** to deploy the solution.</span></span>

1. <span data-ttu-id="404b3-122">To allow the local UX to connect, run the following commands at the bash shell in the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="404b3-122">To allow the local UX to connect, run the following commands at the bash shell in the virtual machine:</span></span>

    ```sh
    cd /app
    sudo ./start.sh --unsafe
    ```

1. <span data-ttu-id="404b3-123">After you see the command completes and the web site starts, you can disconnect from the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="404b3-123">After you see the command completes and the web site starts, you can disconnect from the virtual machine.</span></span>

1. <span data-ttu-id="404b3-124">In your local copy of the [azure-iot-pcs-remote-monitoring-webui](https://github.com/Azure/azure-iot-pcs-remote-monitoring-webui) repository, edit the **.env** file to add the URL of your deployed solution:</span><span class="sxs-lookup"><span data-stu-id="404b3-124">In your local copy of the [azure-iot-pcs-remote-monitoring-webui](https://github.com/Azure/azure-iot-pcs-remote-monitoring-webui) repository, edit the **.env** file to add the URL of your deployed solution:</span></span>

    ```config
    NODE_PATH = src/
    REACT_APP_BASE_SERVICE_URL=https://{your solution name}.azurewebsites.net/
    ```

1. <span data-ttu-id="404b3-125">At a command prompt in your local copy of the `azure-iot-pcs-remote-monitoring-webui` folder, run the following commands to install the required libraries and run the UI locally:</span><span class="sxs-lookup"><span data-stu-id="404b3-125">At a command prompt in your local copy of the `azure-iot-pcs-remote-monitoring-webui` folder, run the following commands to install the required libraries and run the UI locally:</span></span>

    ```cmd/sh
    npm install
    npm start
    ```

1. <span data-ttu-id="404b3-126">The previous command runs the UI locally at http://localhost:3000/dashboard.</span><span class="sxs-lookup"><span data-stu-id="404b3-126">The previous command runs the UI locally at http://localhost:3000/dashboard.</span></span> <span data-ttu-id="404b3-127">You can edit the code while the site is running and see it update dynamically.</span><span class="sxs-lookup"><span data-stu-id="404b3-127">You can edit the code while the site is running and see it update dynamically.</span></span>

## <a name="customize-the-layout"></a><span data-ttu-id="404b3-128">Customize the layout</span><span class="sxs-lookup"><span data-stu-id="404b3-128">Customize the layout</span></span>

<span data-ttu-id="404b3-129">Each page in the Remote Monitoring solution is composed of a set of controls, referred to as *panels* in the source code.</span><span class="sxs-lookup"><span data-stu-id="404b3-129">Each page in the Remote Monitoring solution is composed of a set of controls, referred to as *panels* in the source code.</span></span> <span data-ttu-id="404b3-130">For example, the **Dashboard** page is made up of five panels: Overview, Map, Alarms, Telemetry, and KPIs.</span><span class="sxs-lookup"><span data-stu-id="404b3-130">For example, the **Dashboard** page is made up of five panels: Overview, Map, Alarms, Telemetry, and KPIs.</span></span> <span data-ttu-id="404b3-131">You can find the source code that defines each page and its panels in the [pcs-remote-monitoring-webui](https://github.com/Azure/pcs-remote-monitoring-webui) GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="404b3-131">You can find the source code that defines each page and its panels in the [pcs-remote-monitoring-webui](https://github.com/Azure/pcs-remote-monitoring-webui) GitHub repository.</span></span> <span data-ttu-id="404b3-132">For example, the code that defines the **Dashboard** page, its layout, and the panels on the page is located in the [src/components/pages/dashboard](https://github.com/Azure/pcs-remote-monitoring-webui/tree/master/src/components/pages/dashboard) folder.</span><span class="sxs-lookup"><span data-stu-id="404b3-132">For example, the code that defines the **Dashboard** page, its layout, and the panels on the page is located in the [src/components/pages/dashboard](https://github.com/Azure/pcs-remote-monitoring-webui/tree/master/src/components/pages/dashboard) folder.</span></span>

<span data-ttu-id="404b3-133">Because the panels manage their own layout and sizing, you can easily modify the layout of a page.</span><span class="sxs-lookup"><span data-stu-id="404b3-133">Because the panels manage their own layout and sizing, you can easily modify the layout of a page.</span></span> <span data-ttu-id="404b3-134">For example, the following changes to the **PageContent** element in the `src/components/pages/dashboard/dashboard.js` file swap the positions of the map and telemetry panels, and change the relative widths of the map and KPI panels:</span><span class="sxs-lookup"><span data-stu-id="404b3-134">For example, the following changes to the **PageContent** element in the `src/components/pages/dashboard/dashboard.js` file swap the positions of the map and telemetry panels, and change the relative widths of the map and KPI panels:</span></span>

```nodejs
<PageContent className="dashboard-container" key="page-content">
  <Grid>
    <Cell className="col-1 devices-overview-cell">
      <OverviewPanel
        openWarningCount={openWarningCount}
        openCriticalCount={openCriticalCount}
        onlineDeviceCount={onlineDeviceCount}
        offlineDeviceCount={offlineDeviceCount}
        isPending={kpisIsPending || devicesIsPending}
        error={devicesError || kpisError}
        t={t} />
    </Cell>
    <Cell className="col-5">
      <TelemetryPanel
        telemetry={telemetry}
        isPending={telemetryIsPending}
        error={telemetryError}
        colors={chartColorObjects}
        t={t} />
    </Cell>
    <Cell className="col-3">
      <CustAlarmsPanel
        alarms={currentActiveAlarmsWithName}
        isPending={kpisIsPending || rulesIsPending}
        error={rulesError || kpisError}
        t={t} />
    </Cell>
    <Cell className="col-4">
    <PanelErrorBoundary msg={t('dashboard.panels.map.runtimeError')}>
        <MapPanel
          azureMapsKey={azureMapsKey}
          devices={devices}
          devicesInAlarm={devicesInAlarm}
          mapKeyIsPending={azureMapsKeyIsPending}
          isPending={devicesIsPending || kpisIsPending}
          error={azureMapsKeyError || devicesError || kpisError}
          t={t} />
      </PanelErrorBoundary>
    </Cell>
    <Cell className="col-6">
      <KpisPanel
        topAlarms={topAlarmsWithName}
        alarmsPerDeviceId={alarmsPerDeviceType}
        criticalAlarmsChange={criticalAlarmsChange}
        warningAlarmsChange={warningAlarmsChange}
        isPending={kpisIsPending || rulesIsPending || devicesIsPending}
        error={devicesError || rulesError || kpisError}
        colors={chartColorObjects}
        t={t} />
    </Cell>
  </Grid>
</PageContent>
```

![Change panel layout](./media/iot-accelerators-remote-monitoring-customize/layout.png)

> [!NOTE]
> <span data-ttu-id="404b3-136">The map is not configured in the local deployment.</span><span class="sxs-lookup"><span data-stu-id="404b3-136">The map is not configured in the local deployment.</span></span>

<span data-ttu-id="404b3-137">You can also add multiple instances of the same panel, or multiple versions if you [duplicate and customize a panel](#duplicate-and-customize-an-existing-control).</span><span class="sxs-lookup"><span data-stu-id="404b3-137">You can also add multiple instances of the same panel, or multiple versions if you [duplicate and customize a panel](#duplicate-and-customize-an-existing-control).</span></span> <span data-ttu-id="404b3-138">The following example shows how to add two instances of the telemetry panel by editing the `src/components/pages/dashboard/dashboard.js` file:</span><span class="sxs-lookup"><span data-stu-id="404b3-138">The following example shows how to add two instances of the telemetry panel by editing the `src/components/pages/dashboard/dashboard.js` file:</span></span>

```nodejs
<PageContent className="dashboard-container" key="page-content">
  <Grid>
    <Cell className="col-1 devices-overview-cell">
      <OverviewPanel
        openWarningCount={openWarningCount}
        openCriticalCount={openCriticalCount}
        onlineDeviceCount={onlineDeviceCount}
        offlineDeviceCount={offlineDeviceCount}
        isPending={kpisIsPending || devicesIsPending}
        error={devicesError || kpisError}
        t={t} />
    </Cell>
    <Cell className="col-3">
      <TelemetryPanel
        telemetry={telemetry}
        isPending={telemetryIsPending}
        error={telemetryError}
        colors={chartColorObjects}
        t={t} />
    </Cell>
    <Cell className="col-3">
      <TelemetryPanel
        telemetry={telemetry}
        isPending={telemetryIsPending}
        error={telemetryError}
        colors={chartColorObjects}
        t={t} />
    </Cell>
    <Cell className="col-2">
      <CustAlarmsPanel
        alarms={currentActiveAlarmsWithName}
        isPending={kpisIsPending || rulesIsPending}
        error={rulesError || kpisError}
        t={t} />
    </Cell>
    <Cell className="col-4">
    <PanelErrorBoundary msg={t('dashboard.panels.map.runtimeError')}>
        <MapPanel
          azureMapsKey={azureMapsKey}
          devices={devices}
          devicesInAlarm={devicesInAlarm}
          mapKeyIsPending={azureMapsKeyIsPending}
          isPending={devicesIsPending || kpisIsPending}
          error={azureMapsKeyError || devicesError || kpisError}
          t={t} />
      </PanelErrorBoundary>
    </Cell>
    <Cell className="col-6">
      <KpisPanel
        topAlarms={topAlarmsWithName}
        alarmsPerDeviceId={alarmsPerDeviceType}
        criticalAlarmsChange={criticalAlarmsChange}
        warningAlarmsChange={warningAlarmsChange}
        isPending={kpisIsPending || rulesIsPending || devicesIsPending}
        error={devicesError || rulesError || kpisError}
        colors={chartColorObjects}
        t={t} />
    </Cell>
  </Grid>
</PageContent>
```

<span data-ttu-id="404b3-139">You can then view different telemetry in each panel:</span><span class="sxs-lookup"><span data-stu-id="404b3-139">You can then view different telemetry in each panel:</span></span>

![Multiple telemetry panels](./media/iot-accelerators-remote-monitoring-customize/multiple-telemetry.png)

> [!NOTE]
> <span data-ttu-id="404b3-141">The map is not configured in the local deployment.</span><span class="sxs-lookup"><span data-stu-id="404b3-141">The map is not configured in the local deployment.</span></span>

## <a name="duplicate-and-customize-an-existing-control"></a><span data-ttu-id="404b3-142">Duplicate and customize an existing control</span><span class="sxs-lookup"><span data-stu-id="404b3-142">Duplicate and customize an existing control</span></span>

<span data-ttu-id="404b3-143">The following steps outline how to use the **alarms** panel as an example of how to duplicate an existing panel, modify it, and use the modified version:</span><span class="sxs-lookup"><span data-stu-id="404b3-143">The following steps outline how to use the **alarms** panel as an example of how to duplicate an existing panel, modify it, and use the modified version:</span></span>

1. <span data-ttu-id="404b3-144">In your local copy of the repository, make a copy of the **alarms** folder in the `src/components/pages/dashboard/panels` folder.</span><span class="sxs-lookup"><span data-stu-id="404b3-144">In your local copy of the repository, make a copy of the **alarms** folder in the `src/components/pages/dashboard/panels` folder.</span></span> <span data-ttu-id="404b3-145">Name the new copy **cust_alarms**.</span><span class="sxs-lookup"><span data-stu-id="404b3-145">Name the new copy **cust_alarms**.</span></span>

1. <span data-ttu-id="404b3-146">In the **alarmsPanel.js** file in the **cust_alarms** folder, edit the name of the class to be **CustAlarmsPanel**:</span><span class="sxs-lookup"><span data-stu-id="404b3-146">In the **alarmsPanel.js** file in the **cust_alarms** folder, edit the name of the class to be **CustAlarmsPanel**:</span></span>

    ```nodejs
    export class CustAlarmsPanel extends Component {
    ```

1. <span data-ttu-id="404b3-147">Add the following line to the `src/components/pages/dashboard/panels/index.js` file:</span><span class="sxs-lookup"><span data-stu-id="404b3-147">Add the following line to the `src/components/pages/dashboard/panels/index.js` file:</span></span>

    ```nodejs
    export * from './cust_alarms';
    ```

1. <span data-ttu-id="404b3-148">Replace `AlarmsPanel` with `CustAlarmsPanel` in the `src/components/pages/dashboard/dashboard.js` file:</span><span class="sxs-lookup"><span data-stu-id="404b3-148">Replace `AlarmsPanel` with `CustAlarmsPanel` in the `src/components/pages/dashboard/dashboard.js` file:</span></span>

    ```nodejs
    import {
      OverviewPanel,
      CustAlarmsPanel,
      TelemetryPanel,
      KpisPanel,
      MapPanel,
      transformTelemetryResponse,
      chartColors
    } from './panels';

    ...

    <Cell className="col-3">
      <CustAlarmsPanel
        alarms={currentActiveAlarmsWithName}
        isPending={kpisIsPending || rulesIsPending}
        error={rulesError || kpisError}
        t={t} />
    </Cell>
    ```

<span data-ttu-id="404b3-149">You have now replaced the original **Alarms** panel with a copy called **CustAlarms**.</span><span class="sxs-lookup"><span data-stu-id="404b3-149">You have now replaced the original **Alarms** panel with a copy called **CustAlarms**.</span></span> <span data-ttu-id="404b3-150">This copy is identical to the original.</span><span class="sxs-lookup"><span data-stu-id="404b3-150">This copy is identical to the original.</span></span> <span data-ttu-id="404b3-151">You can now modify the copy.</span><span class="sxs-lookup"><span data-stu-id="404b3-151">You can now modify the copy.</span></span> <span data-ttu-id="404b3-152">For example, to change the column ordering in the **Alarms** panel:</span><span class="sxs-lookup"><span data-stu-id="404b3-152">For example, to change the column ordering in the **Alarms** panel:</span></span>

1. <span data-ttu-id="404b3-153">Open the `src/components/pages/dashboard/panels/cust_alarms/alarmsPanel.js` file.</span><span class="sxs-lookup"><span data-stu-id="404b3-153">Open the `src/components/pages/dashboard/panels/cust_alarms/alarmsPanel.js` file.</span></span>

1. <span data-ttu-id="404b3-154">Modify the column definitions as shown in the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="404b3-154">Modify the column definitions as shown in the following code snippet:</span></span>

    ```nodejs
    this.columnDefs = [
      rulesColumnDefs.severity,
      {
        headerName: 'rules.grid.count',
        field: 'count'
      },
      {
        ...rulesColumnDefs.ruleName,
        minWidth: 200
      },
      rulesColumnDefs.explore
    ];
    ```

<span data-ttu-id="404b3-155">The following screenshot shows the new version of the **Alarms** panel:</span><span class="sxs-lookup"><span data-stu-id="404b3-155">The following screenshot shows the new version of the **Alarms** panel:</span></span>

![Alarms panel updated](./media/iot-accelerators-remote-monitoring-customize/reorder-columns.png)

## <a name="customize-the-telemetry-chart"></a><span data-ttu-id="404b3-157">Customize the telemetry chart</span><span class="sxs-lookup"><span data-stu-id="404b3-157">Customize the telemetry chart</span></span>

<span data-ttu-id="404b3-158">The telemetry chart on the **Dashboard** page is defined by the files in the `src/components/pages/dashboard/panels/telemtry` folder.</span><span class="sxs-lookup"><span data-stu-id="404b3-158">The telemetry chart on the **Dashboard** page is defined by the files in the `src/components/pages/dashboard/panels/telemtry` folder.</span></span> <span data-ttu-id="404b3-159">The UI retrieves the telemetry from the solution back end in the `src/services/telemetryService.js` file.</span><span class="sxs-lookup"><span data-stu-id="404b3-159">The UI retrieves the telemetry from the solution back end in the `src/services/telemetryService.js` file.</span></span> <span data-ttu-id="404b3-160">The following steps show you how to change the time period displayed on the telemetry chart from 15 minutes to 5 minutes:</span><span class="sxs-lookup"><span data-stu-id="404b3-160">The following steps show you how to change the time period displayed on the telemetry chart from 15 minutes to 5 minutes:</span></span>

1. <span data-ttu-id="404b3-161">In the `src/services/telemetryService.js` file, locate the function called **getTelemetryByDeviceIdP15M**.</span><span class="sxs-lookup"><span data-stu-id="404b3-161">In the `src/services/telemetryService.js` file, locate the function called **getTelemetryByDeviceIdP15M**.</span></span> <span data-ttu-id="404b3-162">Make a copy of this function and modify the copy as follows:</span><span class="sxs-lookup"><span data-stu-id="404b3-162">Make a copy of this function and modify the copy as follows:</span></span>

    ```nodejs
    static getTelemetryByDeviceIdP5M(devices = []) {
      return TelemetryService.getTelemetryByMessages({
        from: 'NOW-PT5M',
        to: 'NOW',
        order: 'desc',
        devices
      });
    }
    ```

1. <span data-ttu-id="404b3-163">To use this new function to populate the telemetry chart, open the `src/components/pages/dashboard/dashboard.js` file.</span><span class="sxs-lookup"><span data-stu-id="404b3-163">To use this new function to populate the telemetry chart, open the `src/components/pages/dashboard/dashboard.js` file.</span></span> <span data-ttu-id="404b3-164">Locate the line that initializes the telemetry stream and modify it as follows:</span><span class="sxs-lookup"><span data-stu-id="404b3-164">Locate the line that initializes the telemetry stream and modify it as follows:</span></span>

    ```node.js
    const getTelemetryStream = ({ deviceIds = [] }) => TelemetryService.getTelemetryByDeviceIdP5M(deviceIds)
    ```

<span data-ttu-id="404b3-165">The telemetry chart now shows the five minutes of telemetry data:</span><span class="sxs-lookup"><span data-stu-id="404b3-165">The telemetry chart now shows the five minutes of telemetry data:</span></span>

![Telemetry chart showing one day](./media/iot-accelerators-remote-monitoring-customize/telemetry-period.png)

## <a name="add-a-new-kpi"></a><span data-ttu-id="404b3-167">Add a new KPI</span><span class="sxs-lookup"><span data-stu-id="404b3-167">Add a new KPI</span></span>

<span data-ttu-id="404b3-168">The **Dashboard** page displays KPIs in the **System KPIs** panel.</span><span class="sxs-lookup"><span data-stu-id="404b3-168">The **Dashboard** page displays KPIs in the **System KPIs** panel.</span></span> <span data-ttu-id="404b3-169">These KPIs are calculated in the `src/components/pages/dashboard/dashboard.js` file.</span><span class="sxs-lookup"><span data-stu-id="404b3-169">These KPIs are calculated in the `src/components/pages/dashboard/dashboard.js` file.</span></span> <span data-ttu-id="404b3-170">The KPIs are rendered by the `src/components/pages/dashboard/panels/kpis/kpisPanel.js` file.</span><span class="sxs-lookup"><span data-stu-id="404b3-170">The KPIs are rendered by the `src/components/pages/dashboard/panels/kpis/kpisPanel.js` file.</span></span> <span data-ttu-id="404b3-171">The following steps describe how to calculate and render a new KPI value on the **Dashboard** page.</span><span class="sxs-lookup"><span data-stu-id="404b3-171">The following steps describe how to calculate and render a new KPI value on the **Dashboard** page.</span></span> <span data-ttu-id="404b3-172">The example shown is to add a new percentage change in warning alarms KPI:</span><span class="sxs-lookup"><span data-stu-id="404b3-172">The example shown is to add a new percentage change in warning alarms KPI:</span></span>

1. <span data-ttu-id="404b3-173">Open the `src/components/pages/dashboard/dashboard.js` file.</span><span class="sxs-lookup"><span data-stu-id="404b3-173">Open the `src/components/pages/dashboard/dashboard.js` file.</span></span> <span data-ttu-id="404b3-174">Modify the **initialState** object to include a **warningAlarmsChange** property as follows:</span><span class="sxs-lookup"><span data-stu-id="404b3-174">Modify the **initialState** object to include a **warningAlarmsChange** property as follows:</span></span>

    ```nodejs
    const initialState = {
      ...

      // Kpis data
      currentActiveAlarms: [],
      topAlarms: [],
      alarmsPerDeviceId: {},
      criticalAlarmsChange: 0,
      warningAlarmsChange: 0,
      kpisIsPending: true,
      kpisError: null,

      ...
    };
    ```

1. <span data-ttu-id="404b3-175">Modify the **currentAlarmsStats** object to include **totalWarningCount** as a property:</span><span class="sxs-lookup"><span data-stu-id="404b3-175">Modify the **currentAlarmsStats** object to include **totalWarningCount** as a property:</span></span>

    ```nodejs
    return {
      openWarningCount: (acc.openWarningCount || 0) + (isWarning && isOpen ? 1 : 0),
      openCriticalCount: (acc.openCriticalCount || 0) + (isCritical && isOpen ? 1 : 0),
      totalWarningCount: (acc.totalWarningCount || 0) + (isWarning ? 1 : 0),
      totalCriticalCount: (acc.totalCriticalCount || 0) + (isCritical ? 1 : 0),
      alarmsPerDeviceId: updatedAlarmsPerDeviceId
    };
    ```

1. <span data-ttu-id="404b3-176">Calculate the new KPI.</span><span class="sxs-lookup"><span data-stu-id="404b3-176">Calculate the new KPI.</span></span> <span data-ttu-id="404b3-177">Find the calculation for the critical alarms count.</span><span class="sxs-lookup"><span data-stu-id="404b3-177">Find the calculation for the critical alarms count.</span></span> <span data-ttu-id="404b3-178">Duplicate the code and modify the copy as follows:</span><span class="sxs-lookup"><span data-stu-id="404b3-178">Duplicate the code and modify the copy as follows:</span></span>

    ```nodejs
    // ================== Warning Alarms Count - START
    const currentWarningAlarms = currentAlarmsStats.totalWarningCount;
    const previousWarningAlarms = previousAlarms.reduce(
      (cnt, { severity }) => severity === 'warning' ? cnt + 1 : cnt,
      0
    );
    const warningAlarmsChange = ((currentWarningAlarms - previousWarningAlarms) / currentWarningAlarms * 100).toFixed(2);
    // ================== Warning Alarms Count - END
    ```

1. <span data-ttu-id="404b3-179">Include the new **warningAlarmsChange** KPI in the KPI stream:</span><span class="sxs-lookup"><span data-stu-id="404b3-179">Include the new **warningAlarmsChange** KPI in the KPI stream:</span></span>

    ```nodejs
    return ({
      kpisIsPending: false,

      // Kpis data
      currentActiveAlarms,
      topAlarms,
      criticalAlarmsChange,
      warningAlarmsChange,
      alarmsPerDeviceId: currentAlarmsStats.alarmsPerDeviceId,

      ...
    });
    ```

1. <span data-ttu-id="404b3-180">Include the new **warningAlarmsChange** KPI in the state data used to render the UI:</span><span class="sxs-lookup"><span data-stu-id="404b3-180">Include the new **warningAlarmsChange** KPI in the state data used to render the UI:</span></span>

    ```nodejs
    const {
      ...

      currentActiveAlarms,
      topAlarms,
      alarmsPerDeviceId,
      criticalAlarmsChange,
      warningAlarmsChange,
      kpisIsPending,
      kpisError,

      ...
    } = this.state;
    ```

1. <span data-ttu-id="404b3-181">Update the data passed to the KPIs panel:</span><span class="sxs-lookup"><span data-stu-id="404b3-181">Update the data passed to the KPIs panel:</span></span>

    ```node.js
    <KpisPanel
      topAlarms={topAlarmsWithName}
      alarmsPerDeviceId={alarmsPerDeviceType}
      criticalAlarmsChange={criticalAlarmsChange}
      warningAlarmsChange={warningAlarmsChange}
      isPending={kpisIsPending || rulesIsPending || devicesIsPending}
      error={devicesError || rulesError || kpisError}
      colors={chartColorObjects}
      t={t} />
    ```

<span data-ttu-id="404b3-182">You have now finished the changes in the `src/components/pages/dashboard/dashboard.js` file.</span><span class="sxs-lookup"><span data-stu-id="404b3-182">You have now finished the changes in the `src/components/pages/dashboard/dashboard.js` file.</span></span> <span data-ttu-id="404b3-183">The following steps describe the changes to make in the `src/components/pages/dashboard/panels/kpis/kpisPanel.js` file to display the new KPI:</span><span class="sxs-lookup"><span data-stu-id="404b3-183">The following steps describe the changes to make in the `src/components/pages/dashboard/panels/kpis/kpisPanel.js` file to display the new KPI:</span></span>

1. <span data-ttu-id="404b3-184">Modify the following line of code to retrieve the new KPI value as follows:</span><span class="sxs-lookup"><span data-stu-id="404b3-184">Modify the following line of code to retrieve the new KPI value as follows:</span></span>

    ```nodejs
    const { t, isPending, criticalAlarmsChange, warningAlarmsChange, error } = this.props;
    ```

1. <span data-ttu-id="404b3-185">Modify the markup to display the new KPI value as follows:</span><span class="sxs-lookup"><span data-stu-id="404b3-185">Modify the markup to display the new KPI value as follows:</span></span>

    ```nodejs
    <div className="kpi-cell">
      <div className="kpi-header">{t('dashboard.panels.kpis.criticalAlarms')}</div>
      <div className="critical-alarms">
        {
          criticalAlarmsChange !== 0 &&
            <div className="kpi-percentage-container">
              <div className="kpi-value">{ criticalAlarmsChange }</div>
              <div className="kpi-percentage-sign">%</div>
            </div>
        }
      </div>
      <div className="kpi-header">{t('Warning alarms')}</div>
      <div className="critical-alarms">
        {
          warningAlarmsChange !== 0 &&
            <div className="kpi-percentage-container">
              <div className="kpi-value">{ warningAlarmsChange }</div>
              <div className="kpi-percentage-sign">%</div>
            </div>
        }
      </div>
    </div>
    ```

<span data-ttu-id="404b3-186">The **Dashboard** page now displays the new KPI value:</span><span class="sxs-lookup"><span data-stu-id="404b3-186">The **Dashboard** page now displays the new KPI value:</span></span>

![Warning KPI](./media/iot-accelerators-remote-monitoring-customize/new-kpi.png)

## <a name="customize-the-map"></a><span data-ttu-id="404b3-188">Customize the map</span><span class="sxs-lookup"><span data-stu-id="404b3-188">Customize the map</span></span>

<span data-ttu-id="404b3-189">See the [Customize map](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide#upgrade-map-key-to-see-devices-on-a-dynamic-map) page in GitHub for details of the map components in the solution.</span><span class="sxs-lookup"><span data-stu-id="404b3-189">See the [Customize map](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/wiki/Developer-Reference-Guide#upgrade-map-key-to-see-devices-on-a-dynamic-map) page in GitHub for details of the map components in the solution.</span></span>

<!--
### Connect an external visualization tool

See the [Connect an external visualization tool](https://github.com/Azure/azure-iot-pcs-remote-monitoring-dotnet/) page in GitHub for details of how to connect an external visualization tool.

-->

## <a name="other-customization-options"></a><span data-ttu-id="404b3-190">Other customization options</span><span class="sxs-lookup"><span data-stu-id="404b3-190">Other customization options</span></span>

<span data-ttu-id="404b3-191">To further modify the presentation and visualizations layer in the Remote Monitoring solution, you can edit the code.</span><span class="sxs-lookup"><span data-stu-id="404b3-191">To further modify the presentation and visualizations layer in the Remote Monitoring solution, you can edit the code.</span></span> <span data-ttu-id="404b3-192">The relevant GitHub repositories are:</span><span class="sxs-lookup"><span data-stu-id="404b3-192">The relevant GitHub repositories are:</span></span>

* [<span data-ttu-id="404b3-193">The configuration microservice for Azure IoT Solutions (.NET)</span><span class="sxs-lookup"><span data-stu-id="404b3-193">The configuration microservice for Azure IoT Solutions (.NET)</span></span>](https://github.com/Azure/pcs-ui-config-dotnet/)
* [<span data-ttu-id="404b3-194">The configuration microservice for Azure IoT Solutions  (Java)</span><span class="sxs-lookup"><span data-stu-id="404b3-194">The configuration microservice for Azure IoT Solutions  (Java)</span></span>](https://github.com/Azure/pcs-ui-config-java/)
* [<span data-ttu-id="404b3-195">Azure IoT PCS Remote Monitoring Web UI</span><span class="sxs-lookup"><span data-stu-id="404b3-195">Azure IoT PCS Remote Monitoring Web UI</span></span>](https://github.com/Azure/pcs-remote-monitoring-webui)

## <a name="next-steps"></a><span data-ttu-id="404b3-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="404b3-196">Next steps</span></span>

<span data-ttu-id="404b3-197">In this article, you learned about the resources available to help you customize the web UI in the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="404b3-197">In this article, you learned about the resources available to help you customize the web UI in the Remote Monitoring solution accelerator.</span></span>

<span data-ttu-id="404b3-198">For more conceptual information about the Remote Monitoring solution accelerator, see [Remote Monitoring architecture](iot-accelerators-remote-monitoring-sample-walkthrough.md)</span><span class="sxs-lookup"><span data-stu-id="404b3-198">For more conceptual information about the Remote Monitoring solution accelerator, see [Remote Monitoring architecture](iot-accelerators-remote-monitoring-sample-walkthrough.md)</span></span>

<span data-ttu-id="404b3-199">For more information about customizing the Remote Monitoring solution, see [Customize and redeploy a microservice](iot-accelerators-microservices-example.md)
<!-- Next tutorials in the sequence --></span><span class="sxs-lookup"><span data-stu-id="404b3-199">For more information about customizing the Remote Monitoring solution, see [Customize and redeploy a microservice](iot-accelerators-microservices-example.md)
<!-- Next tutorials in the sequence --></span></span>
