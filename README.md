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

Three consent types:
Applications in Microsoft identity platform rely on consent in order to gain access to necessary resources or APIs.
- Static user content -> In the static user consent scenario, you must specify all the permissions it needs in the app's configuration in the Azure portal.
- Incremental and dynamic user consent
- Admin consent

Microsoft Authentication Library:
The Microsoft Authentication Library (MSAL) can be used to provide secure access to Microsoft Graph, other Microsoft APIs, third-party web APIs, or your own web API.
- No need to directly use the OAuth libraries or code against the protocol in your application.
- Acquires tokens on behalf of a user or on behalf of an application (when applicable to the platform).
- Maintains a token cache and refreshes tokens for you when they are close to expire. You don't need to handle token expiration on your own.
- Helps you specify which audience you want your application to sign in.
- Helps you set up your application from configuration files.
- Helps you troubleshoot your app by exposing actionable exceptions, logging, and telemetry.

<img width="913" alt="Screenshot 2023-01-10 at 06 19 37" src="https://user-images.githubusercontent.com/39561427/211476292-ee00d9e6-031e-425a-99bd-fee17f2f05ec.png">

Public client, and confidential client applications:
- Public client applications: Are apps that run on devices or desktop computers or in a web browser. They're not trusted to safely keep application secrets, so they only access web APIs on behalf of the user. (They support only public client flows.) Public clients can't hold configuration-time secrets, so they don't have client secrets.
- Confidential client applications: Are apps that run on servers (web apps, web API apps, or even service/daemon apps). They're considered difficult to access, and for that reason capable of keeping an application secret. Confidential clients can hold configuration-time secrets. Each instance of the client has a distinct configuration (including client ID and client secret).

What is a shared access signature:
- A shared access signature (SAS) is a URI that grants restricted access rights to Azure Storage resources. A shared access signature (SAS) is a signed URI that points to one or more storage resources and includes a token that contains a special set of query parameters. 

Types of shared access signature:
- User delegation SAS: A user delegation SAS is secured with Azure Active Directory credentials and also by the permissions specified for the SAS. A user delegation SAS applies to Blob storage only.
- Service SAS: A service SAS is secured with the storage account key. A service SAS delegates access to a resource in the following Azure Storage services: Blob storage, Queue storage, Table storage, or Azure Files.
- Account SAS: An account SAS is secured with the storage account key. An account SAS delegates access to resources in one or more of the storage services. All of the operations available via a service or user delegation SAS are also available via an account SAS.

How shared access signature works:
- When you use a SAS to access data stored in Azure Storage, you need two components. The first is a URI to the resource you want to access. The second part is a SAS token that you've created to authorize access to that resource.

In a single URI, such as https://medicalrecords.blob.core.windows.net/patient-images/patient-116139-nq8z7f.jpg?sp=r&st=2020-01-20T11:42:32Z&se=2020-01-20T19:42:32Z&spr=https&sv=2019-02-02&sr=b&sig=SrW1HZ5Nb6MbRzTbXCaPm%2BJiSEn15tC91Y4umMPwVZs%3D, you can separate the URI from the SAS token as follows:

URI: https://medicalrecords.blob.core.windows.net/patient-images/patient-116139-nq8z7f.jpg?
SAS token: sp=r&st=2020-01-20T11:42:32Z&se=2020-01-20T19:42:32Z&spr=https&sv=2019-02-02&sr=b&sig=SrW1HZ5Nb6MbRzTbXCaPm%2BJiSEn15tC91Y4umMPwVZs%3D

<img width="928" alt="Screenshot 2023-01-10 at 06 44 49" src="https://user-images.githubusercontent.com/39561427/211480340-6a1ef957-b36a-4f39-9bac-702a67612ea9.png">

Microsoft Graph:
- Microsoft Graph is the gateway to data and intelligence in Microsoft 365. It provides a unified programmability model that you can use to access the tremendous amount of data in Microsoft 365, Windows 10, and Enterprise Mobility + Security.

In the Microsoft 365 platform, three main components facilitate the access and flow of data:
- The Microsoft Graph API offers a single endpoint, https://graph.microsoft.com. You can use REST APIs or SDKs to access the endpoint. Microsoft Graph also includes a powerful set of services that manage user and device identity, access, compliance, security, and help protect organizations from data leakage or loss.
- Microsoft Graph connectors work in the incoming direction, delivering data external to the Microsoft cloud into Microsoft Graph services and applications, to enhance Microsoft 365 experiences such as Microsoft Search. Connectors exist for many commonly used data sources such as Box, Google Drive, Jira, and Salesforce.
- Microsoft Graph Data Connect provides a set of tools to streamline secure and scalable delivery of Microsoft Graph data to popular Azure data stores. The cached data serves as data sources for Azure development tools that you can use to build intelligent applications.

Microsoft graph SDK's include two components:
- Service Library -> The service library contains models and request builders that are generated from Microsoft Graph metadata to provide a rich, strongly typed, and discoverable experience when working with the many datasets available in Microsoft Graph.
- Core Library -> The core library provides a set of features that enhance working with all the Microsoft Graph services. Embedded support for retry handling, secure redirects, transparent authentication, and payload compression, improve the quality of your application's interactions with Microsoft Graph, with no added complexity, while leaving you completely in control. The core library also provides support for common tasks such as paging through collections and creating batch requests.

Acquire an access token:
- A client application can request managed identities for Azure resources app-only access token for accessing a given resource. The token is based on the managed identities for Azure resources service principal. As such, there is no need for the client to register itself to obtain an access token under its own service principal. The token is suitable for use as a bearer token in service-to-service calls requiring client credentials.

Feature management:
Feature management is a modern software-development practice that decouples feature release from code deployment and enables quick changes to feature availability on demand. It uses a technique called feature flags (also known as feature toggles, feature switches, and so on) to dynamically administer a feature's lifecycle.
- Feature flag: A feature flag is a variable with a binary state of on or off. The feature flag also has an associated code block. The state of the feature flag triggers whether the code block runs or not.
- Feature manager: A feature manager is an application package that handles the lifecycle of all the feature flags in an application. The feature manager typically provides additional functionality, such as caching feature flags and updating their states.
- Filter: A filter is a rule for evaluating the state of a feature flag. A user group, a device or browser type, a geographic location, and a time window are all examples of what a filter can represent.

Secure app configuration data:
- Customer managed keys
- Private endpoints
- Managed identities

Use private endpoints for Azure App Configuration:
- You can use private endpoints for Azure App Configuration to allow clients on a virtual network (VNet) to securely access data over a private link. The private endpoint uses an IP address from the VNet address space for your App Configuration store. Network traffic between the clients on the VNet and the App Configuration store traverses over the VNet using a private link on the Microsoft backbone network, eliminating exposure to the public internet.

Using private endpoints for your App Configuration store enables you to:

- Secure your application configuration details by configuring the firewall to block all connections to App Configuration on the public endpoint.
- Increase security for the virtual network (VNet) ensuring data doesn't escape from the VNet.
- Securely connect to the App Configuration store from on-premises networks that connect to the VNet using VPN or ExpressRoutes with private-peering.

API gateways:
An API gateway sits between clients and services. It acts as a reverse proxy, routing requests from clients to services. It may also perform various cross-cutting tasks such as authentication, SSL termination, and rate limiting.

Gateways can perform a number of different functions, and you may not need all of them. The functions can be grouped into the following design patterns:

Gateway routing: Use the gateway as a reverse proxy to route requests to one or more backend services, using layer 7 routing. The gateway provides a single endpoint for clients, and helps to decouple clients from services.

Gateway aggregation: Use the gateway to aggregate multiple individual requests into a single request. This pattern applies when a single operation requires calls to multiple backend services. The client sends one request to the gateway. The gateway dispatches requests to the various backend services, and then aggregates the results and sends them back to the client. This helps to reduce chattiness between the client and the backend.

Gateway Offloading: Use the gateway to offload functionality from individual services to the gateway, particularly cross-cutting concerns. It can be useful to consolidate these functions into one place, rather than making every service responsible for implementing them.

Here are some examples of functionality that could be offloaded to a gateway:

SSL termination
Authentication
IP allow/block list
Client rate limiting (throttling)
Logging and monitoring
Response caching
GZIP compression
Servicing static content

Azure event grid:
- Azure Event Grid is an eventing backplane that enables event-driven, reactive programming. It uses the publish-subscribe model. Publishers emit events, but have no expectation about how the events are handled. Subscribers decide on which events they want to handle.

Event grid connects sources and handlers:
- ![functional-model](https://user-images.githubusercontent.com/39561427/211992409-6f160889-e4e6-4f2c-9089-6eb5ce20792b.png)

Concepts in Azure event grid:
- Events - What happened.
- Event sources - Where the event took place.
- Topics - The endpoint where publishers send events.
- Event subscriptions - The endpoint or built-in mechanism to route events, sometimes to more than one handler. Subscriptions are also used by handlers to intelligently filter incoming events.
- Event handlers - The app or service reacting to the event

What is an event:
- An event is the smallest amount of information that fully describes something that happened in the system.

Topics:
The event grid topic provides an endpoint where the source sends events. The publisher creates the event grid topic, and decides whether an event source needs one topic or more than one topic. A topic is used for a collection of related events. To respond to certain types of events, subscribers decide which topics to subscribe to.

There are two topics:
- System topics are built-in topics provided by Azure services. You don't see system topics in your Azure subscription because the publisher owns the topics, but you can subscribe to them. To subscribe, you provide information about the resource you want to receive events from. As long as you have access to the resource, you can subscribe to its events.
- Custom topics are application and third-party topics. When you create or are assigned access to a custom topic, you see that custom topic in your subscription.

Retry policy:
You can customize the retry policy when creating an event subscription by using the following two configurations. An event will be dropped if either of the limits of the retry policy is reached.

- Maximum number of attempts - The value must be an integer between 1 and 30. The default value is 30.
- Event time-to-live (TTL) - The value must be an integer between 1 and 1440. The default value is 1440 minutes

Output batching:
You can configure Event Grid to batch events for delivery for improved HTTP performance in high-throughput scenarios. Batching is turned off by default and can be turned on per-subscription via the portal, CLI, PowerShell, or SDKs.

Batched delivery has two settings:

- Max events per batch - Maximum number of events Event Grid will deliver per batch. This number will never be exceeded, however fewer events may be delivered if no other events are available at the time of publish. Event Grid doesn't delay events to create a batch if fewer events are available. Must be between 1 and 5,000.

- Preferred batch size in kilobytes - Target ceiling for batch size in kilobytes. Similar to max events, the batch size may be smaller if more events aren't available at the time of publish. It's possible that a batch is larger than the preferred batch size if a single event is larger than the preferred size. For example, if the preferred size is 4 KB and a 10-KB event is pushed to Event Grid, the 10-KB event will still be delivered in its own batch rather than being dropped.

Dead-letter events:
When Event Grid can't deliver an event within a certain time period or after trying to deliver the event a certain number of times, it can send the undelivered event to a storage account. This process is known as dead-lettering. Event Grid dead-letters an event when one of the following conditions is met.

- Event isn't delivered within the time-to-live period.
- The number of tries to deliver the event exceeds the limit.

Receive events by using webhooks:
Webhooks are one of the many ways to receive events from Azure Event Grid. When a new event is ready, Event Grid service POSTs an HTTP request to the configured endpoint with the event in the request body.

Endpoint validation with Event Grid events:
If you're using any other type of endpoint, such as an HTTP trigger based Azure function, your endpoint code needs to participate in a validation handshake with Event Grid. Event Grid supports two ways of validating the subscription.

- Synchronous handshake: At the time of event subscription creation, Event Grid sends a subscription validation event to your endpoint. The schema of this event is similar to any other Event Grid event. The data portion of this event includes a validationCode property. Your application verifies that the validation request is for an expected event subscription, and returns the validation code in the response synchronously. This handshake mechanism is supported in all Event Grid versions.

- Asynchronous handshake: In certain cases, you can't return the ValidationCode in response synchronously. For example, if you use a third-party service (like Zapier or IFTTT), you can't programmatically respond with the validation code.

Filter events:
Three options for filitering -> 
- Event types
- Subject begins with or ends with
- Advanced fields and operators
 