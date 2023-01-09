AZ 204
--------

Azure Virtual Network(Vnet): 
- An Azure Virtual Network(Vnet) is a representation of your own network in the cloud. It is a logical isolation of the Azure cloud dedicated to your subscription. Vnet is similar to a traditional network that you'd operate in your own data center, but brings with it additional benefits of Azure's infrastructure such as scale, availability, and isolation. 


Azure Cosmos DB: 
- Used for data that is constantly updated. It supports schema-less data 

Azure Blob Storage: 
- Supports unstructured data, and large files 

Azure Queue: 
- Service for storing large numbers of messages that can be accessed from anywhere in the world.  Used to pass messages between different Azure web servers 

Azure Redundancy:
Locally redundant storage -> Locally redundant storage (LRS) replicates your storage account three times within a single data center in the primary region.
Zone-redundant storage -> Zone-redundant storage (ZRS) replicates your storage account synchronously across three Azure availability zones in the primary region. Each availability zone is a separate physical location with independent power, cooling, and networking.

AZ webapp current list linux:
az webapp list-runtimes --os-type linux

Azure App Service Plans:
- App service plan -> App(s)

Isolate your app into a new App Service plan when:
- The app is resource-intensive.
- You want to scale the app independently from the other apps in the existing plan.
- The app needs resource in a different geographical region

Configure connection strings:
- For ASP.NET and ASP.NET Core developers, the values you set in App Service override the ones in Web.config. For other language stacks, it's better to use app settings instead, because connection strings require special formatting in the variable keys in order to access the values.Connection strings are always encrypted when stored (encrypted-at-rest).
Tip:Connection strings are always encrypted when stored (encrypted-at-rest).

Configure security certificates:
- A certificate uploaded into an app is stored in a deployment unit that is bound to the app service plan's resource group and region combination (internally called a webspace). This makes the certificate accessible to other apps in the same resource group and region combination.

What is autoscaling?
- Autoscaling is a cloud system or process that adjusts available resources based on the current demand. Autoscaling performs scaling in and out, as opposed to scaling up and down.Autoscaling doesn't have any effect on the CPU power, memory, or storage capacity of the web servers powering the app, it only changes the number of web servers.

Azure provides two options for autoscaling:
- Scale based on a metric, such as the length of the disk queue, or the number of HTTP requests awaiting processing.
- Scale to a specific instance count according to a schedule. For example, you can arrange to scale out at a particular time of day, or on a specific date or day of the week. You also specify an end date, and the system will scale back in at this time.

Three main hosting plans for Functions:
- Consumption plan -> This is the default hosting plan. It scales automatically and you only pay for compute resources when your functions are running. Instances of the Functions host are dynamically added and removed based on the number of incoming events.
- Premium plan -> Automatically scales based on demand using pre-warmed workers, which run applications with no delay after being idle, runs on more powerful instances, and connects to virtual networks.
- Dedicated plan -> Run your functions within an App Service plan at regular App Service plan rates. Best for long-running scenarios where Durable Functions can't be used.

Azure functions:
- Triggers -> Triggers are what cause a function to run. A trigger defines how a function is invoked and a function must have exactly one trigger. Triggers have associated data, which is often provided as the payload of the function.
- Binding -> Binding to a function is a way of declaratively connecting another resource to the function; bindings may be connected as input bindings, output bindings, or both. Data from bindings is provided to the function as parameters.

Durable functions:
- Durable Functions is an extension of Azure Functions that lets you write stateful functions in a serverless compute environment.

Application patterns that can benefit from durable functions:
- Function chaining
- Fan-out/fan-in
- Async HTTP APIs
- Monitor
- Human interaction

Four durable functions type:
- Orchestrator
- Activity
- Entity
- Client

What is a task hub:
- A task hub in Durable Functions is a logical container for durable storage resources that are used for orchestrations and entities. 

Azure Blob Storage:
- Blob storage is optimized for storing massive amounts of unstructured data.

Access tiers for block blob data:
- Hot
- Cool
- Archive

Blob storage offers three types of resources:
- The storage account -> unique namespace in Azure for data
- A container in the storage account -> similar to a directory in a file system
- A blob in the container -> three types of blobs ->
1. Block blobs -> Store text and binary data
2. Append blobs -> Blocks like blobs
3. Page blobs -> Store random access files

Azure storage automatically encrypts data at rest

Azure Storage offers two options for copying your data to a secondary region:
- Geo-redundant storage (GRS) copies your data synchronously three times within a single physical location in the primary region using LRS.It then copies your data asynchronously to a single physical location in the secondary region. Within the secondary region, your data is copied synchronously three times using LRS
- Geo-zone-redundant storage (GZRS) copies your data synchronously across three Azure availability zones in the primary region using ZRS. It then copies your data asynchronously to a single physical location in the secondary region. Within the secondary region, your data is copied synchronously three times using LRS.

What is Azure Cosmos DB:
- Azure Cosmos DB is a globally distributed database system that allows you to read and write data from the local replicas of your database and it transparently replicates the data to all the regions associated with your Cosmos account

![cosmos-entities](https://user-images.githubusercontent.com/39561427/210715789-a3a91b63-c9d1-4f0a-a378-75a20013018d.png)

Data consistency from strongest to weakest:
- Strong
- Bounded staleness
- Session
- Consistent prefix
- Eventual

What are request units:
- The cost of all database operations is normalized by Azure Cosmos DB and is expressed by request units
- A request unit represents the system resources such as CPU, IOPS, and memory that are required to perform the database operations supported by Azure Cosmos DB.

The type of Azure Cosmos DB account you're using determines the way consumed RUs get charged. There are three modes in which you can create an account:
- Provisioned throughput mode
- Serverless mode
- Autoscale mode

Partitioning explained:
- In partitioning, the items in a container are divided into distinct subsets called logical partitions
- In addition to a partition key that determines the item's logical partition, each item in a container has an item ID which is unique within a logical partition. Combining the partition key and the item ID creates the item's index, which uniquely identifies the item. Choosing a partition key is an important decision that will affect your application's performance.

Partition key two components:
- Partition key path
- Partition key value

AZ CLI commands:
- Resource group-> az group create --location <myLocation> --name az204-cosmos-rg
- Auzure Cosmos DB account -> az cosmosdb create --name <myCosmosDBacct> --resource-group az204-cosmos-rg

Azure Virtual machines can be used for(examples):
- Development and test
- Applications in the cloud 
- Extended datacenter 

Two options for disk storage:
- Managed disks -> Managed disks are the newer and recommended disk storage model and they are managed by Azure
- Unmanaged disk -> With unmanaged disks, you’re responsible for the storage accounts that hold the virtual hard disks (VHDs) that correspond to your VM disks

What is an availability set:
- An availability set is a logical grouping of VMs that allows Azure to understand how your application is built to provide for redundancy and availability. An availability set is composed of two additional groupings that protect against hardware failures and allow updates to safely be applied - fault domains (FDs) and update domains (UDs).

Load balancer:
- It provides high availability by distributing traffic among healthy VMs
- Configure front-end IP configuration to allow the load balancer and applications to be accessible over the internet

Azure resource manager:
- Azure Resource Manager is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources in your Azure subscription

![consistent-management-layer](https://user-images.githubusercontent.com/39561427/210945731-cd14088a-ec5a-41c1-a9ab-ddcf57b9c4cc.png)

Azure resource manager advantages:
- Declarative syntax
- Repeatable results
- Orchestration

"resources": [
  {
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2019-04-01",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "StorageV2",
    "properties": {}
  }
]

-->

PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2019-04-01
REQUEST BODY
{
  "location": "westus",
  "sku": {
    "name": "Standard_LRS"
  },
  "kind": "StorageV2",
  "properties": {}
}

Azure container registry:
- Azure Container Registry (ACR) is a managed, private Docker registry service based on the open-source Docker Registry 2.0. Create and maintain Azure container registries to store and manage your private Docker container images

What is a dockerfile:
- A Dockerfile is a text file that contains the instructions we use to build and run a Docker image

What is a dockerimage:
- A Docker image is a file used to execute code in a Docker container. Docker images act as a set of instructions to build a Docker container, like a template. Docker images also act as the starting point when using Docker. An image is comparable to a snapshot in virtual machine (VM) environments. A Docker image has everything needed to run a containerized application, including code, config files, environment variables, libraries and runtimes. When the image is deployed to a Docker environment, it can be executed as a Docker container.

Azure Container Instances:
- Azure Container Instances (ACI) is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs

Azure container instances:
- Allocates resources such as CPUs, memory, and optionally GPUs (preview) to a container group by adding the resource requests of the instances in the group

Azure container groups share:
- IP address
- Port namespace on that IP address

Explanation on ARM/Bicep templates and YAML:
- ARM/Bicep is the template to specificy the resource
- YAML file to deploy the ARM/Bicep file/template
- https://ochzhen.com/blog/deploy-azure-bicep-in-cicd-pipeline -> YAML - ARM/bicep

What is a service principal:
- An Azure service principal is an identity created for use with applications, hosted services, and automated tools to access Azure resources

There are three type of service principal:
- Application -> This type of service principal is the local representation, or application instance, of a global application object in a single tenant or directory. The service principal object defines what the app can actually do in the specific tenant, who can access the app, and what resources the app can access.
- Managed identity -> Managed identities provide an identity for applications to use when connecting to resources that support Azure Active Directory authentication.
- Legacy -> This type of service principal represents a legacy app, which is an app created before app registrations were introduced or an app created through legacy experiences.

Permission types:
- The Microsoft identity platform supports two types of permissions: delegated permissions and application permissions.
- Delegated permissions -> For these apps, either the user or an administrator consents to the permissions that the app requests. The app is delegated with the permission to act as a signed-in user when it makes calls to the target resource.
- Application permissions -> are used by apps that run without a signed-in user present, for example, apps that run as background services or daemons. Only an administrator can consent to application permissions.

