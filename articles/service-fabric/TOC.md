
# Overview
## [What is Service Fabric?](service-fabric-overview.md)
## [Understand microservices](service-fabric-overview-microservices.md)
## [Application scenarios](service-fabric-application-scenarios.md)
## [Architecture](service-fabric-architecture.md)
## [Terminology](service-fabric-technical-overview.md)
## [Primer](service-fabric-content-roadmap.md)

# Get Started
## Set up your development environment
### [Windows](service-fabric-get-started.md)
### [Linux](service-fabric-get-started-linux.md)
### [Mac OS](service-fabric-get-started-mac.md)
## Create your first application
### [C# on Windows](service-fabric-create-your-first-application-in-visual-studio.md)
### [Java on Linux](service-fabric-create-your-first-linux-application-with-java.md)
### [C# on Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
## [Deploy apps on a local cluster](service-fabric-get-started-with-a-local-cluster.md)
## [Create your first cluster on Azure](service-fabric-get-started-azure-cluster.md)
## [Create your first standalone cluster](service-fabric-get-started-standalone-cluster.md)

# How To
## Build an application
### [Patterns and scenarios](service-fabric-patterns-and-scenarios.md)
### Basics
#### [Application model](service-fabric-application-model.md)
#### [Package an application](service-fabric-package-apps.md)
#### [Supported programming model](service-fabric-choose-framework.md)
#### [Service state](service-fabric-concepts-state.md)
#### [Service communication](service-fabric-connect-and-communicate-with-services.md)
#### [Add a web front end](service-fabric-add-a-web-frontend.md)
#### [Service manifest resources](service-fabric-service-manifest-resources.md)
#### [Get started with Eclipse plugin for Java development](service-fabric-get-started-eclipse.md)
#### [Manage apps in Visual Studio](service-fabric-manage-application-in-visual-studio.md)
#### [Configure secure connections in Visual Studio](service-fabric-visualstudio-configure-secure-connections.md)
#### Debug
##### [Debug a C# service in VS](service-fabric-debugging-your-application.md)
##### [Debug a Java service in Eclipse](service-fabric-debugging-your-application-java.md)
#### Monitor and diagnose
##### [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
##### [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
#### [Manage application secrets](service-fabric-application-secret-management.md)  
#### [Configure security policies for your application](service-fabric-application-runas-security.md)  
#### [Configure your application for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md)  
#### [Common errors and exceptions](service-fabric-errors-and-exceptions.md) 

### Guest executable application
#### [Deploy a guest executable](service-fabric-deploy-existing-app.md)
#### [Deploy multiple guest executables](service-fabric-deploy-multiple-apps.md)

### Container application
#### [Overview](service-fabric-containers-overview.md)
#### [Deploy Windows container](service-fabric-deploy-container.md)
#### [Deploy Docker container](service-fabric-deploy-container-linux.md)

### Reliable Service application
#### [Overview](service-fabric-reliable-services-introduction.md)
#### Get started
##### [C# on Windows](service-fabric-reliable-services-quick-start.md)
##### [Java on Linux](service-fabric-reliable-services-quick-start-java.md)
#### [Reliable Services lifecycle - C#](service-fabric-reliable-services-lifecycle.md)
#### [Reliable Services lifecycle - Java](service-fabric-reliable-services-lifecycle-java.md)
#### [Reliable Collections](service-fabric-reliable-services-reliable-collections.md)
#### [Use Reliable Collections](service-fabric-work-with-reliable-collections.md)
#### [Configure](service-fabric-reliable-services-configuration.md)
#### [Notifications](service-fabric-reliable-services-notifications.md)
#### [Backup and restore](service-fabric-reliable-services-backup-restore.md)
#### [Communicate with Reliable Services](service-fabric-reliable-services-communication.md)
#### [Secure communications with Reliable Services - C#](service-fabric-reliable-services-secure-communication.md)
#### [Secure communications with Reliable Services - Java](service-fabric-reliable-services-secure-communication-java.md)
##### [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)
##### [Service Remoting - C#](service-fabric-reliable-services-communication-remoting.md)
##### [Service Remoting - Java](service-fabric-reliable-services-communication-remoting-java.md)
##### [WCF](service-fabric-reliable-services-communication-wcf.md)
##### [Reverse Proxy](service-fabric-reverseproxy.md)
#### [Advanced usage](service-fabric-reliable-services-advanced-usage.md)

### Reliable Actor application
#### [Overview](service-fabric-reliable-actors-introduction.md)
#### Get Started
##### [C# on Windows](service-fabric-reliable-actors-get-started.md)
##### [Java on Linux](service-fabric-reliable-actors-get-started-java.md)
#### [Architecture](service-fabric-reliable-actors-platform.md)
#### [Lifecycle and garbage collection](service-fabric-reliable-actors-lifecycle.md)
#### [Polymorphism](service-fabric-reliable-actors-polymorphism.md)
#### [Reentrancy](service-fabric-reliable-actors-reentrancy.md)
#### [Events](service-fabric-reliable-actors-events.md) 
#### [Timers and reminders](service-fabric-reliable-actors-timers-reminders.md)
#### [State management](service-fabric-reliable-actors-state-management.md)
#### [Configure KvsActorStateProvider](service-fabric-reliable-actors-kvsactorstateprovider-configuration.md)
#### [Type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)
#### [Configure communications settings](service-fabric-reliable-actors-fabrictransportsettings.md) 
#### [Configure ReliableDictionaryActorStateProvider](service-fabric-reliable-actors-reliabledictionarystateprovider-configuration.md)

## Migrate from Cloud Services
### [Compare Cloud Services with Service Fabric](service-fabric-cloud-services-migration-differences.md)
### [Migrate to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md)
### [Recomended practices](/azure/architecture/service-fabric/migrate-from-cloud-services)

## Create and manage clusters

### Basics
#### [Overview](service-fabric-deploy-anywhere.md)
#### [Describe a cluster](service-fabric-cluster-resource-manager-cluster-description.md)
#### [Capacity planning](service-fabric-cluster-capacity.md)
#### [Visualize a cluster](service-fabric-visualizing-your-cluster.md)
#### [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md)
#### [Manage a cluster using Azure CLI](service-fabric-azure-cli.md) 
#### [Secure a cluster](service-fabric-cluster-security.md)
#### [Disaster recovery](service-fabric-disaster-recovery.md)
#### [Feature differences between Linux and Windows](service-fabric-linux-windows-differences.md)

### Clusters on Azure
#### Create a cluster on Azure
##### [Azure portal](service-fabric-cluster-creation-via-portal.md)
##### [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
##### [Visual Studio and Azure Resource Manager](service-fabric-cluster-creation-via-visual-studio.md)
#### [Cluster networking patterns](service-fabric-patterns-networking.md)
#### [Node types and VM Scale Sets](service-fabric-cluster-nodetypes.md)
#### [Scale a cluster](service-fabric-cluster-scale-up-down.md)
#### [Scale a cluster programmatically](service-fabric-cluster-programmatic-scaling.md)
#### [Upgrade a cluster](service-fabric-cluster-upgrade.md)
#### [Delete a cluster](service-fabric-cluster-delete.md)
#### [Access control](service-fabric-cluster-security-roles.md)
#### [Configure a cluster](service-fabric-cluster-fabric-settings.md)
#### [Add or rollover cluster certificates](service-fabric-cluster-security-update-certs-azure.md) 

### Standalone clusters
#### [Plan and prepare for your deployment](service-fabric-cluster-standalone-deployment-preparation.md)
#### [Contents of the Service Fabric standalone package](service-fabric-cluster-standalone-package-contents.md)
#### [Create a standalone cluster](service-fabric-cluster-creation-for-windows-server.md)
#### [Create a standalone cluster on Azure Virtual Machines](service-fabric-cluster-creation-with-windows-azure-vms.md)
#### [Scale a cluster](service-fabric-cluster-windows-server-add-remove-nodes.md)
#### [Upgrade a cluster](service-fabric-cluster-upgrade-windows-server.md)
#### [Access control](service-fabric-cluster-security-roles.md)
#### [Configure a cluster](service-fabric-cluster-manifest.md)
#### [Secure a cluster using certs](service-fabric-windows-cluster-x509-security.md)  
#### [Secure a cluster using Windows security](service-fabric-windows-cluster-windows-security.md) 

## Manage application lifecycle
### [Overview](service-fabric-application-lifecycle.md)
### [Set up continuous integration with VSTS](service-fabric-set-up-continuous-integration.md)
### [Deploy your Linux Java app using Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
### [Understand the ImageStoreConnectionString setting](service-fabric-image-store-connection-string.md)
### Deploy or remove applications
#### [PowerShell](service-fabric-deploy-remove-applications.md)
#### [Visual Studio](service-fabric-publish-app-remote-cluster.md)
#### [FabricClient APIs](service-fabric-deploy-remove-applications-fabricclient.md)
### [Application upgrade overview](service-fabric-application-upgrade.md)
### [Configure application upgrade](service-fabric-visualstudio-configure-upgrade.md)
### [Application upgrade parameters](service-fabric-application-upgrade-parameters.md)
### Upgrade an application
#### [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
#### [Visual Studio](service-fabric-application-upgrade-tutorial.md)
### [Troubleshoot application upgrades](service-fabric-application-upgrade-troubleshooting.md)
### [Data serialization in application upgrades](service-fabric-application-upgrade-data-serialization.md)
### [Application upgrades advanced topics](service-fabric-application-upgrade-advanced.md)

## Inspect application and cluster health
### [Monitor Service Fabric health](service-fabric-health-introduction.md)
### [Report and check service health](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
### [Add custom health reports](service-fabric-report-health.md)
### [Troubleshoot with system health reports](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
### [View health reports](service-fabric-view-entities-aggregated-health.md)

## Monitor and diagnose
### [Monitor and diagnose applications](service-fabric-diagnostics-overview.md)
### Monitor and diagnose services locally
#### [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
#### [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
### Azure Diagnostics logs
#### [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
#### [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
### [Collect logs from a service process](service-fabric-diagnostic-collect-logs-without-an-agent.md)
### [Diagnostics in stateful Reliable Services](service-fabric-reliable-services-diagnostics.md)
### [Diagnostics in Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
### [Troubleshoot your local cluster](service-fabric-troubleshoot-local-cluster-setup.md)

## Scale applications
### [Partition Reliable Services](service-fabric-concepts-partitioning.md)
### [Availability of services](service-fabric-availability-services.md)
### [Scale applications](service-fabric-concepts-scalability.md)
### [Plan capacity of applications](service-fabric-capacity-planning.md)

## Test applications and services
### [Fault Analysis overview](service-fabric-testability-overview.md)
### [Test service-to-service communication](service-fabric-testability-scenarios-service-communication.md)
### Simulate failures
#### [Using controlled Chaos](service-fabric-controlled-chaos.md)
#### [Using Test actions](service-fabric-testability-actions.md)
#### [During workloads](service-fabric-testability-workload-tests.md)
#### [Using Test scenarios](service-fabric-testability-scenarios.md)
#### [Using the node transition APIs](service-fabric-node-transition-apis.md)
### [Load test your application](service-fabric-vso-load-test.md)

## Manage and orchestrate cluster resources
### [Cluster Resource Manager overview](service-fabric-cluster-resource-manager-introduction.md)
### [Cluster Resource Manager architecture](service-fabric-cluster-resource-manager-architecture.md)
### [Describe a cluster](service-fabric-cluster-resource-manager-cluster-description.md)
### [Application groups overview](service-fabric-cluster-resource-manager-application-groups.md)
### [Configure Cluster Resource Manager settings](service-fabric-cluster-resource-manager-configure-services.md)
### [Resource consumption metrics](service-fabric-cluster-resource-manager-metrics.md)
### [Use service affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
### [Service placement policies](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
### [Manage a cluster](service-fabric-cluster-resource-manager-management-integration.md)
### [Cluster defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
### [Balance a cluster](service-fabric-cluster-resource-manager-balancing.md)
### [Throttling](service-fabric-cluster-resource-manager-advanced-throttling.md)
### [Service movement](service-fabric-cluster-resource-manager-movement-cost.md)

# Reference
## [PowerShell](/powershell/module/ServiceFabric/)
## [Java API](/java/api/)
## [.NET](/dotnet/api/)
## [REST](/rest/api/servicefabric)

# Resources
## [Common questions about Service Fabric](service-fabric-common-questions.md)
## [Service Fabric support options](service-fabric-support.md)
## [Sample code](http://aka.ms/servicefabricsamples)
## [Learning path](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
## [Pricing](https://azure.microsoft.com/pricing/details/service-fabric/)
## [Service Updates](https://azure.microsoft.com/updates/?product=service-fabric)
## [MSDN Forum](https://social.msdn.microsoft.com/Forums/home?forum=AzureServiceFabric)
## [Videos](https://azure.microsoft.com/documentation/videos/index/?services=service-fabric)
