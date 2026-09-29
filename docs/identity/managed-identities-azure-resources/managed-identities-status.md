---
layout: Conceptual
title: Azure Services and resources with managed identities - Managed identities for Azure resources | Microsoft Learn
canonicalUrl: https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/managed-identities-status
uhfHeaderId: MSDocsHeader-Entra
breadcrumb_path: /entra/breadcrumb/toc.json
feedback_system: Standard
feedback_product_url: https://feedback.azure.com/d365community/forum/22920db1-ad25-ec11-b6e6-000d3a4f0789
author: kengaderdus
ms.author: kengaderdus
ms.service: entra-id
ms.subservice: managed-identities
manager: CelesteDG
description: Explore Azure services and resource types supporting managed identities for secure, credential-free authentication.
ms.date: 2025-05-09T00:00:00.0000000Z
ms.topic: concept-article
locale: en-us
document_id: 93ddd42a-d6a8-ca3c-9666-b1b55675ce71
document_version_independent_id: 453717cc-7bc5-c4bc-aac9-17fe2f735d8d
original_content_git_url: https://github.com/MicrosoftDocs/entra-docs-pr/blob/live/docs/identity/managed-identities-azure-resources/managed-identities-status.md
site_name: Docs
depot_name: MSDN.entra-docs
page_type: conceptual
toc_rel: toc.json
feedback_help_link_type: ''
feedback_help_link_url: ''
asset_id: identity/managed-identities-azure-resources/managed-identities-status
moniker_range_name: 
monikers: []
item_type: Content
source_path: docs/identity/managed-identities-azure-resources/managed-identities-status.md
cmProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/68ec7f3a-2bc6-459f-b959-19beb729907d
spProducts:
- https://authoring-docs-microsoft.poolparty.biz/devrel/90370425-aca4-4a39-9533-d52e5e002a5d
platformId: 069deaab-0bbb-802d-49c2-e1c3c0c2ae56
---

# Azure Services and resources with managed identities - Managed identities for Azure resources | Microsoft Learn

Managed identities for Azure resources provide an automatically managed identity in Microsoft Entra ID, enabling secure, credential-free authentication to Azure services. This article lists Azure services and resource types that support managed identities.

This page provides links to services' content that can use managed identities to access other Azure resources as well as a list of Azure resource providers and resource types that support managed identities.

Additional resource provider namespace information is available in [Resource providers for Azure services](/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).

Important

New technical content is added daily. This list does not include every article that talks about managed identities. Please refer to each service's content set for details on their managed identities support.

## Services supporting managed identities

The following Azure services support managed identities for Azure resources:

| Service Name | Documentation |
| --- | --- |
| API Management | [Use managed identities in Azure API Management](/en-us/azure/api-management/api-management-howto-use-managed-service-identity) |
| Application Gateway | [TLS termination with Key Vault certificates](/en-us/azure/application-gateway/key-vault-certs) |
| Azure App Configuration | [How to use managed identities for Azure App Configuration](/en-us/azure/azure-app-configuration/overview-managed-identity) |
| Azure App Services | [How to use managed identities for App Service and Azure Functions](/en-us/azure/app-service/overview-managed-identity) |
| Azure Arc enabled Kubernetes | [Quickstart: Connect an existing Kubernetes cluster to Azure Arc](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster) |
| Azure Arc enabled servers | [Authenticate against Azure resources with Azure Arc-enabled servers](/en-us/azure/azure-arc/servers/managed-identity-authentication) |
| Azure Automanage | [Repair an Automanage Account](/en-us/azure/automanage/repair-automanage-account) |
| Azure Automation | [Azure Automation account authentication overview](/en-us/azure/automation/automation-security-overview#managed-identities) |
| Azure Batch | [Configure customer-managed keys for your Azure Batch account with Azure Key Vault and Managed Identity](/en-us/azure/batch/batch-customer-managed-key)[Configure managed identities in Batch pools](/en-us/azure/batch/managed-identity-pools) |
| Azure Blueprints | [Stages of a blueprint deployment](/en-us/azure/governance/blueprints/concepts/deployment-stages) |
| Azure Cache for Redis | [Managed identity for storage accounts with Azure Cache for Redis](/en-us/azure/azure-cache-for-redis/cache-managed-identity) |
| Azure Chaos Studio | [Permissions and identity in Chaos Studio Workspaces](/en-us/azure/chaos-studio/chaos-studio-workspace-permissions)[Permissions and security in Azure Chaos Studio (classic)](/en-us/azure/chaos-studio/chaos-studio-permissions-security#user-assigned-managed-identity) |
| Azure Communications Gateway | [Deploy Azure Communications Gateway](/en-us/azure/communications-gateway/deploy) |
| Azure Communication Services | [How to use Managed Identity with Azure Communication Services](/en-us/azure/communication-services/how-tos/managed-identity) |
| Azure Container Apps | [Managed identities in Azure Container Apps](/en-us/azure/container-apps/managed-identity) |
| Azure Container Instance | [How to use managed identities with Azure Container Instances](/en-us/azure/container-instances/container-instances-managed-identity) |
| Azure Container Registry | [Use an Azure-managed identity in ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-authentication-managed-identity) |
| Azure CycleCloud | [Using Managed Identities](/en-us/azure/cyclecloud/how-to/managed-identities?view=cyclecloud-8&amp;preserve-view=true) |
| Azure AI services | [Configure customer-managed keys with Azure Key Vault for Azure AI services](/en-us/azure/ai-services/encryption/cognitive-services-encryption-keys-portal) |
| Azure Data Box | [Use customer-managed keys in Azure Key Vault for Azure Data Box](/en-us/azure/databox/data-box-customer-managed-encryption-key-portal) |
| Azure Data Explorer | [Configure managed identities for your Azure Data Explorer cluster](/en-us/azure/data-explorer/configure-managed-identities-cluster?tabs=portal) |
| Azure Data Factory | [Managed identity for Data Factory](/en-us/azure/data-factory/data-factory-service-identity) |
| Azure Data Lake Storage Gen1 | [Customer-managed keys for Azure Storage encryption](/en-us/azure/storage/common/customer-managed-keys-overview) |
| Azure Data Share | [Roles and requirements for Azure Data Share](/en-us/azure/data-share/concepts-roles-permissions) |
| Azure DevTest Labs | [Enable user-assigned managed identities on lab virtual machines in Azure DevTest Labs](/en-us/azure/devtest-labs/enable-managed-identities-lab-vms) |
| Azure Digital Twins | [Enable a managed identity for routing Azure Digital Twins events](/en-us/azure/digital-twins/how-to-enable-managed-identities-portal) |
| Azure Event Grid | [Event delivery with a managed identity](/en-us/azure/event-grid/managed-service-identity) |
| Azure Event Hubs | [Authenticate a managed identity with Microsoft Entra ID to access Event Hubs Resources](/en-us/azure/event-hubs/authenticate-managed-identity) |
| Azure File Sync | [How to use managed identities with Azure File Sync](/en-us/azure/storage/file-sync/file-sync-managed-identities) |
| Azure Files | [Access SMB Azure file shares using managed identities with Microsoft Entra ID](/en-us/azure/storage/files/files-managed-identities) |
| Azure Health Data Services workspace services | [Authentication and authorization for Azure Health Data Services](/en-us/azure/healthcare-apis/authentication-authorization) |
| Azure Health Data Services de-identification service | [Use managed identities with the de-identification service](/en-us/azure/healthcare-apis/deidentification/managed-identities) |
| Azure Image Builder | [Azure Image Builder overview](/en-us/azure/virtual-machines/image-builder-overview#permissions) |
| Azure Import/Export | [Use customer-managed keys in Azure Key Vault for Import/Export service](/en-us/azure/import-export/storage-import-export-encryption-key-portal) |
| Azure IoT Hub | [IoT Hub support for virtual networks with Private Link and Managed Identity](/en-us/azure/iot-hub/virtual-network-support) |
| Azure Kubernetes Service (AKS) | [Use managed identities in Azure Kubernetes Service](/en-us/azure/aks/use-managed-identity) |
| Azure Load Testing | [Use managed identities for Azure Load Testing](/en-us/azure/load-testing/how-to-use-a-managed-identity) |
| Azure Logic Apps | [Authenticate access to Azure resources using managed identities in Azure Logic Apps](/en-us/azure/logic-apps/create-managed-service-identity) |
| Azure Log Analytics workspace | [Enable managed identity for Log Analytics workspace](/en-us/azure/azure-monitor/logs/private-storage?tabs=azure-portal##link-storage-accounts-to-your-log-analytics-workspace) |
| Azure Log Analytics cluster | [Azure Monitor customer-managed key](/en-us/azure/azure-monitor/logs/customer-managed-keys) |
| Azure Machine Learning Services | [Use Managed identities with Azure Machine Learning](/en-us/azure/machine-learning/how-to-identity-based-service-authentication?tabs=python) |
| Azure Managed Disk | [Use the Azure portal to enable server-side encryption with customer-managed keys for managed disks](/en-us/azure/virtual-machines/disks-enable-customer-managed-keys-portal) |
| Azure Media services | [Managed identities](/en-us/azure/media-services/latest/concept-managed-identities) |
| Azure Monitor | [Azure Monitor customer-managed key](/en-us/azure/azure-monitor/logs/customer-managed-keys?tabs=portal) |
| Azure Policy | [Remediate non-compliant resources with Azure Policy](/en-us/azure/governance/policy/how-to/remediate-resources) |
| Microsoft Purview | [Credentials for source authentication in Microsoft Purview](/en-us/purview/manage-credentials) |
| Azure Quantum | [Authenticate using a managed identity](/en-us/azure/quantum/optimization-authenticate-managed-identity) |
| Azure Resource Mover | [Move resources across regions (from resource group)](/en-us/azure/resource-mover/move-region-within-resource-group) |
| Azure Site Recovery | [Replicate machines with private endpoints](/en-us/azure/site-recovery/azure-to-azure-how-to-enable-replication-private-endpoints#enable-the-managed-identity-for-the-vault) |
| Azure Search | [Set up an indexer connection to a data source using a managed identity](/en-us/azure/search/search-howto-managed-identities-data-sources) |
| Azure Service Bus | [Authenticate a managed identity with Microsoft Entra ID to access Azure Service Bus resources](/en-us/azure/service-bus-messaging/service-bus-managed-service-identity) |
| Azure Service Fabric | [Using Managed identities for Azure with Service Fabric](/en-us/azure/service-fabric/concepts-managed-identity) |
| Azure SignalR Service | [Managed identities for Azure SignalR Service](/en-us/azure/azure-signalr/howto-use-managed-identity) |
| Azure Spring Apps | [Enable system-assigned managed identity for an application in Azure Spring Apps](/en-us/azure/spring-apps/how-to-enable-system-assigned-managed-identity) |
| Azure SQL | [Managed identities in Microsoft Entra for Azure SQL](/en-us/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity) |
| Azure SQL Managed Instance | [Managed identities in Microsoft Entra for Azure SQL](/en-us/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity) |
| Azure Stack Edge | [Manage Azure Stack Edge secrets using Azure Key Vault](/en-us/azure/databox-online/azure-stack-edge-gpu-activation-key-vault#recover-managed-identity-access) |
| Azure Static Web Apps | [Securing authentication secrets in Azure Key Vault](/en-us/azure/static-web-apps/key-vault-secrets) |
| Azure Stream Analytics | [Authenticate Stream Analytics to Azure Data Lake Storage Gen1 using managed identities](/en-us/azure/stream-analytics/stream-analytics-managed-identities-adls) |
| Azure Synapse | [Azure Synapse workspace managed identity](/en-us/azure/data-factory/data-factory-service-identity) |
| Azure VM image builder | [Configure Azure Image Builder Service permissions using Azure CLI](/en-us/azure/virtual-machines/linux/image-builder-permissions-cli#using-managed-identity-for-azure-storage-access) |
| Azure Virtual Machine Scale Sets | [Configure managed identities on virtual machine scale set - Azure CLI](qs-configure-cli-windows-vmss) |
| Azure Virtual Machines | [Secure and use policies on virtual machines in Azure](/en-us/azure/virtual-machines/windows/security-policy#managed-identities-for-azure-resources) |
| Azure Web PubSub Service | [Managed identities for Azure Web PubSub Service](/en-us/azure/azure-web-pubsub/howto-use-managed-identity) |

## Resource providers and resource types supporting managed identities

The following resource providers and resource types support managed identities:

| Namespace | ResourceType | Identity types(s) |
| --- | --- | --- |
| Microsoft.AVS | privateClouds | System-assignedUser-assigned |
| Microsoft.ApiManagement | service | System-assignedUser-assigned |
| Microsoft.App | builders | System-assignedUser-assigned |
| Microsoft.App | containerApps | System-assignedUser-assigned |
| Microsoft.App | jobs | System-assignedUser-assigned |
| Microsoft.App | managedEnvironments | System-assignedUser-assigned |
| Microsoft.App | sessionPools | System-assignedUser-assigned |
| Microsoft.AppConfiguration | configurationStores | System-assignedUser-assigned |
| Microsoft.AppPlatform | Spring | System-assigned |
| Microsoft.AppPlatform | Spring/apps | System-assignedUser-assigned |
| Microsoft.Automation | automationAccounts | System-assignedUser-assigned |
| Microsoft.AzureStackHCI | clusters | System-assigned |
| Microsoft.AzureStackHCI | devicePools | System-assigned |
| Microsoft.AzureStackHCI | edgeMachines | System-assigned |
| Microsoft.AzureStackHCI | virtualMachines | System-assigned |
| Microsoft.Batch | batchAccounts | System-assignedUser-assigned |
| Microsoft.Batch | batchAccounts/pools | User-assigned |
| Microsoft.Blueprint | blueprintAssignments | System-assignedUser-assigned |
| Microsoft.Cache | Redis | System-assignedUser-assigned |
| Microsoft.Cache | redisEnterprise | System-assignedUser-assigned |
| Microsoft.Cdn | profiles | System-assignedUser-assigned |
| Microsoft.ChangeAnalysis | profile | System-assigned |
| Microsoft.CognitiveServices | accounts | System-assignedUser-assigned |
| Microsoft.CognitiveServices | accounts/encryptionScopes |  |
| Microsoft.Communication | CommunicationServices | System-assignedUser-assigned |
| Microsoft.Compute | diskEncryptionSets | System-assignedUser-assigned |
| Microsoft.Compute | galleries | System-assignedUser-assigned |
| Microsoft.Compute | virtualMachineScaleSets | System-assignedUser-assigned |
| Microsoft.Compute | virtualMachines | System-assignedUser-assigned |
| Microsoft.ContainerInstance | containerGroups | System-assignedUser-assigned |
| Microsoft.ContainerInstance | containerScaleSets | System-assignedUser-assigned |
| Microsoft.ContainerInstance | nGroups | System-assignedUser-assigned |
| Microsoft.ContainerRegistry | registries | System-assignedUser-assigned |
| Microsoft.ContainerRegistry | registries/credentialSets | System-assigned |
| Microsoft.ContainerRegistry | registries/exportPipelines | System-assignedUser-assigned |
| Microsoft.ContainerRegistry | registries/importPipelines | System-assignedUser-assigned |
| Microsoft.ContainerRegistry | registries/taskRuns | User-assigned |
| Microsoft.ContainerRegistry | registries/tasks | System-assignedUser-assigned |
| Microsoft.ContainerService | fleets | System-assignedUser-assigned |
| Microsoft.ContainerService | managedClusters | System-assignedUser-assigned |
| Microsoft.ContainerService | managedclustersnapshots | System-assignedUser-assigned |
| Microsoft.ContainerService | snapshots | System-assignedUser-assigned |
| Microsoft.CustomProviders | resourceProviders | System-assigned |
| Microsoft.DBforMariaDB | servers | System-assigned |
| Microsoft.DBforMySQL | flexibleServers | User-assigned |
| Microsoft.DBforMySQL | servers | System-assigned |
| Microsoft.DBforPostgreSQL | flexibleServers | System-assignedUser-assigned |
| Microsoft.DBforPostgreSQL | serverGroupsv2 | User-assigned |
| Microsoft.DBforPostgreSQL | servers | System-assigned |
| Microsoft.DataBox | jobs | System-assignedUser-assigned |
| Microsoft.DataBoxEdge | DataBoxEdgeDevices | System-assigned |
| Microsoft.DataFactory | factories | System-assignedUser-assigned |
| Microsoft.DataLakeStore | accounts | System-assigned |
| Microsoft.DataMigration | SqlMigrationServices | System-assigned |
| Microsoft.DataMigration | migrationServices | System-assigned |
| Microsoft.DataProtection | BackupVaults | System-assignedUser-assigned |
| Microsoft.DataShare | accounts | System-assigned |
| Microsoft.Databricks | accessConnectors | System-assignedUser-assigned |
| Microsoft.DesktopVirtualization | hostpools | System-assignedUser-assigned |
| Microsoft.DevCenter | devcenters | System-assignedUser-assigned |
| Microsoft.DevCenter | devcenters/encryptionsets | System-assignedUser-assigned |
| Microsoft.DevCenter | projects | System-assignedUser-assigned |
| Microsoft.DevCenter | projects/environmentTypes | System-assignedUser-assigned |
| Microsoft.DevOpsInfrastructure | pools | User-assigned |
| Microsoft.DevTestLab | labs | System-assignedUser-assigned |
| Microsoft.DevTestLab | labs/serviceRunners | System-assignedUser-assigned |
| Microsoft.DeviceUpdate | accounts | System-assignedUser-assigned |
| Microsoft.DeviceUpdate | updateAccounts | System-assignedUser-assigned |
| Microsoft.Devices | IotHubs | System-assignedUser-assigned |
| Microsoft.Devices | ProvisioningServices | System-assignedUser-assigned |
| Microsoft.DigitalTwins | digitalTwinsInstances | System-assignedUser-assigned |
| Microsoft.DocumentDB | cassandraClusters | System-assigned |
| Microsoft.DocumentDB | databaseAccounts | System-assignedUser-assigned |
| Microsoft.DocumentDB | databaseAccounts/encryptionScopes | User-assigned |
| Microsoft.DocumentDB | garnetClusters | System-assigned |
| Microsoft.DocumentDB | managedResources | System-assigned |
| Microsoft.DocumentDB | throughputPools | System-assigned |
| Microsoft.DocumentDB | throughputPools/throughputPoolAccounts | System-assigned |
| Microsoft.ElasticSan | elasticSans/volumeGroups | System-assignedUser-assigned |
| Microsoft.EventGrid | domains | System-assignedUser-assigned |
| Microsoft.EventGrid | namespaces | System-assignedUser-assigned |
| Microsoft.EventGrid | partnerTopics | System-assignedUser-assigned |
| Microsoft.EventGrid | systemTopics | System-assignedUser-assigned |
| Microsoft.EventGrid | topics | System-assignedUser-assigned |
| Microsoft.EventHub | namespaces | System-assignedUser-assigned |
| Microsoft.HDInsight | clusters | System-assignedUser-assigned |
| Microsoft.HybridCompute | machines | System-assigned |
| Microsoft.HybridNetwork | networkfunctions | System-assignedUser-assigned |
| Microsoft.HybridNetwork | publishers | System-assigned |
| Microsoft.HybridNetwork | serviceManagementContainers | System-assignedUser-assigned |
| Microsoft.HybridNetwork | siteNetworkServices | System-assignedUser-assigned |
| Microsoft.IoTCentral | IoTApps | System-assigned |
| Microsoft.KeyVault | managedHSMs | User-assigned |
| Microsoft.Kubernetes | connectedClusters | System-assigned |
| Microsoft.KubernetesConfiguration | extensions | System-assigned |
| Microsoft.Kusto | clusters | System-assignedUser-assigned |
| Microsoft.LoadTestService | loadtests | System-assignedUser-assigned |
| Microsoft.Logic | integrationAccounts | System-assignedUser-assigned |
| Microsoft.Logic | integrationServiceEnvironments | System-assignedUser-assigned |
| Microsoft.Logic | workflows | System-assignedUser-assigned |
| Microsoft.MachineLearningServices | registries | System-assignedUser-assigned |
| Microsoft.MachineLearningServices | workspaces | System-assignedUser-assigned |
| Microsoft.MachineLearningServices | workspaces/batchEndpoints | System-assigned |
| Microsoft.MachineLearningServices | workspaces/computes | System-assignedUser-assigned |
| Microsoft.MachineLearningServices | workspaces/inferencePools/groups | System-assignedUser-assigned |
| Microsoft.MachineLearningServices | workspaces/linkedServices | System-assigned |
| Microsoft.MachineLearningServices | workspaces/onlineEndpoints | System-assignedUser-assigned |
| Microsoft.Maps | accounts | System-assignedUser-assigned |
| Microsoft.Media | mediaservices | System-assignedUser-assigned |
| Microsoft.Migrate | migrateprojects | System-assigned |
| Microsoft.Migrate | modernizeProjects | System-assigned |
| Microsoft.Migrate | moveCollections | System-assigned |
| Microsoft.MobileNetwork | mobileNetworks | User-assigned |
| Microsoft.MobileNetwork | packetCoreControlPlanes | User-assigned |
| Microsoft.MobileNetwork | simGroups | System-assignedUser-assigned |
| Microsoft.NetApp | netAppAccounts | System-assignedUser-assigned |
| Microsoft.Network | networkWatchers/flowLogs | User-assigned |
| Microsoft.OperationalInsights | clusters | System-assignedUser-assigned |
| Microsoft.OperationalInsights | workspaces | System-assignedUser-assigned |
| Microsoft.PowerPlatform | enterprisePolicies | System-assignedUser-assigned |
| Microsoft.Purview | accounts | System-assignedUser-assigned |
| Microsoft.Quantum | Workspaces | System-assigned |
| Microsoft.RecoveryServices | vaults | System-assignedUser-assigned |
| Microsoft.RedHatOpenShift | OpenShiftClusters | System-assigned |
| Microsoft.Search | searchServices | System-assignedUser-assigned |
| Microsoft.Security | dataScanners | System-assigned |
| Microsoft.Security | pricings/securityOperators | System-assigned |
| Microsoft.ServiceBus | namespaces | System-assignedUser-assigned |
| Microsoft.ServiceFabric | clusters | System-assignedUser-assigned |
| Microsoft.ServiceFabric | clusters/applications | System-assignedUser-assigned |
| Microsoft.ServiceFabric | managedclusters | System-assignedUser-assigned |
| Microsoft.ServiceFabric | managedclusters/applications | System-assignedUser-assigned |
| Microsoft.SignalRService | SignalR | System-assignedUser-assigned |
| Microsoft.SignalRService | WebPubSub | System-assignedUser-assigned |
| Microsoft.Solutions | applications | System-assignedUser-assigned |
| Microsoft.Sql | managedInstances | System-assignedUser-assigned |
| Microsoft.Sql | servers | System-assignedUser-assigned |
| Microsoft.Sql | servers/databases | User-assigned |
| Microsoft.Sql | servers/jobAgents | User-assigned |
| Microsoft.Storage | storageAccounts | System-assignedUser-assigned |
| Microsoft.Storage | storageTasks | System-assigned |
| Microsoft.StorageCache | amlFilesystems | User-assigned |
| Microsoft.StorageCache | caches | System-assignedUser-assigned |
| Microsoft.StorageSync | storageSyncServices | System-assignedUser-assigned |
| Microsoft.StreamAnalytics | streamingjobs | System-assignedUser-assigned |
| Microsoft.Synapse | workspaces | System-assignedUser-assigned |
| Microsoft.VirtualMachineImages | imageTemplates | User-assigned |
| Microsoft.Web | hostingEnvironments | System-assignedUser-assigned |
| Microsoft.Web | sites | System-assignedUser-assigned |
| Microsoft.Web | sites/slots | System-assignedUser-assigned |
| Microsoft.Web | staticSites | System-assignedUser-assigned |