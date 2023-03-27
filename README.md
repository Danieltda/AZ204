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
 

 Explore Azure monitor:
 - Azure Monitor delivers a comprehensive solution for collecting, analyzing, and acting on telemetry from your cloud and on-premises environments.

 Application insights:
 - Application Insights monitors the availability, performance, and usage of your web applications whether they're hosted in the cloud or on-premises. It leverages the powerful data analysis platform in Azure Monitor to provide you with deep insights into your application's operations. It enables you to diagnose errors without waiting for a user to report them.

 What application insights monitors:
 - Request rates, response times, and failure rates - Find out which pages are most popular, at what times of day, and where your users are. See which pages perform best. If your response times and failure rates go high when there are more requests, then perhaps you have a resourcing problem.
- Dependency rates, response times, and failure rates - Find out whether external services are slowing you down.
- Exceptions - Analyze the aggregated statistics, or pick specific instances and drill into the stack trace and related requests. Both server and browser exceptions are reported.
- Page views and load performance - reported by your users' browsers.
- AJAX calls from web pages - rates, response times, and failure rates.
- User and session counts.
- Performance counters from your Windows or Linux server machines, such as CPU, memory, and network usage.
- Host diagnostics from Docker or Azure.
- Diagnostic trace logs from your app - so that you can correlate trace events with requests.
- Custom events and metrics that you write yourself in the client or server code, to track business events such as items sold or games won.

Availability sets:
- URL ping test (classic): You can create this simple test through the portal to validate whether an endpoint is responding and measure performance associated with that response. You can also set custom success criteria coupled with more advanced features, like parsing dependent requests and allowing for retries.
- Standard test (Preview): This single request test is similar to the URL ping test. It includes SSL certificate validity, proactive lifetime check, HTTP request verb (for example GET, HEAD, or POST), custom headers, and custom data associated with your HTTP request.
- Custom TrackAvailability test: If you decide to create a custom application to run availability tests, you can use the TrackAvailability() method to send the results to Application Insights.

What are application maps:

- Application Map helps you spot performance bottlenecks or failure hotspots across all components of your distributed application. Each node on the map represents an application component or its dependencies; and has health KPI and alerts status. You can click through from any component to more detailed diagnostics, such as Application Insights events. If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.

What are components:
Components are independently deployable parts of your distributed/microservices application. Developers and operations teams have code-level visibility or access to telemetry generated by these application components.

- Components are different from "observed" external dependencies such as SQL, Event Hubs, etc. which your team/organization may not have access to (code or telemetry).
- Components run on any number of server/role/container instances.
- Components can be separate Application Insights instrumentation keys (even if subscriptions are different) or different roles reporting to a single Application Insights instrumentation key. The preview map experience shows the components regardless of how they are set up.


------------

Handle responses effectively:

- Pagination: When querying resource collections, you should expect that Microsoft Graph will return the result set in multiple pages, due to server-side page size limits. Your application should always handle the possibility that the responses are paged in nature, and use the @odata.nextLink property to obtain the next paged set of results, until all pages of the result set have been read. The final page will not contain an @odata.nextLink property. For more details, see paging.
- Evolvable enumerations: Adding members to existing enumerations can break applications already using these enums. Evolvable enums is a mechanism that Microsoft Graph API uses to add new members to existing enumerations without causing a breaking change for applications. By default, a GET operation returns only known members for properties of evolvable enum types and your application needs to handle only the known members. If you design your application to handle unknown members as well, you can opt-in to receive those members by using an HTTP Prefer request header.
 
Azure Key Vault:

Azure Key Vault is a cloud service for securely storing and accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, certificates, or cryptographic keys.

Two types of Azure key vault containers:

The Azure Key Vault service supports two types of containers: vaults and managed hardware security module(HSM) pools. Vaults support storing software and HSM-backed keys, secrets, and certificates. Managed HSM pools only support HSM-backed keys.
 

Azure Key Vault helps solve the following problems:

- Secrets Management: Azure Key Vault can be used to Securely store and tightly control access to tokens, passwords, certificates, API keys, and other secrets
- Key Management: Azure Key Vault can also be used as a Key Management solution. Azure Key Vault makes it easy to create and control the encryption keys used to encrypt your data.
- Certificate Management: Azure Key Vault is also a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with Azure and your internal connected resources.
 
Azure key vault authentication:

- Managed identities for Azure resources: When you deploy an app on a virtual machine in Azure, you can assign an identity to your virtual machine that has access to Key Vault. You can also assign identities to other Azure resources. The benefit of this approach is that the app or service isn't managing the rotation of the first secret. Azure automatically rotates the service principal client secret associated with the identity. We recommend this approach as a best practice.
- Service principal and certificate: You can use a service principal and an associated certificate that has access to Key Vault. We don't recommend this approach because the application owner or developer must rotate the certificate.
- Service principal and secret: Although you can use a service principal and a secret to authenticate to Key Vault, we don't recommend it. It's hard to automatically rotate the bootstrap secret that's used to authenticate to Key Vault.
 
Types of managed identities:

- A system-assigned managed identity is enabled directly on an Azure service instance. When the identity is enabled, Azure creates an identity for the instance in the Azure AD tenant that's trusted by the subscription of the instance. After the identity is created, the credentials are provisioned onto the instance. The lifecycle of a system-assigned identity is directly tied to the Azure service instance that it's enabled on. If the instance is deleted, Azure automatically cleans up the credentials and the identity in Azure AD.
- A user-assigned managed identity is created as a standalone Azure resource. Through a create process, Azure creates an identity in the Azure AD tenant that's trusted by the subscription in use. After the identity is created, the identity can be assigned to one or more Azure service instances. The lifecycle of a user-assigned identity is managed separately from the lifecycle of the Azure service instances to which it's assigned.

Queue mechanisms:
Azure supports two types of queue mechanisms
- Service Bus queues -> Service Bus queues are part of a broader Azure messaging infrastructure that supports queuing, publish/subscribe, and more advanced integration patterns. They're designed to integrate applications or application components that may span multiple communication protocols, data contracts, trust domains, or network environments.
- Storage queues -> Storage queues are part of the Azure Storage infrastructure. They allow you to store large numbers of messages. You access messages from anywhere in the world via authenticated calls using HTTP or HTTPS. A queue message can be up to 64 KB in size. A queue may contain millions of messages, up to the total capacity limit of a storage account. Queues are commonly used to create a backlog of work to process asynchronously.

When to use Service Bus Queus:git a
- Your solution needs to receive messages without having to poll the queue. With Service Bus, you can achieve it by using a long-polling receive operation using the TCP-based protocols that Service Bus supports.
- Your solution requires the queue to provide a guaranteed first-in-first-out (FIFO) ordered delivery.
- Your solution needs to support automatic duplicate detection.
- You want your application to process messages as parallel long-running streams (messages are associated with a stream using the session ID property on the message). In this model, each node in the consuming application competes for streams, as opposed to messages. When a stream is given to a consuming node, the node can examine the state of the application stream state using transactions.
- Your solution requires transactional behavior and atomicity when sending or receiving multiple messages from a queue.
- Your application handles messages that can exceed 64 KB but won't likely approach the 256-KB limit.

When to use Storage queues:
- Your application must store over 80 gigabytes of messages in a queue.
- Your application wants to track progress for processing a message in the queue. It's useful if the worker processing a message crashes. Another worker can then use that information to continue from where the prior worker left off.
- You require server side logs of all of the transactions executed against your queues.
 
Azure service bus:
- Microsoft Azure Service Bus is a fully managed enterprise integration message broker. Service Bus can decouple applications and services. Data is transferred between different applications and services using messages. A message is a container decorated with metadata, and contains data. The data can be any kind of information, including structured data encoded with the common formats such as the following ones: JSON, XML, Apache Avro, Plain Text.

 
Receive modes:
- You can specify two different modes in which Service Bus receives messages: Receive and delete or Peek lock.

Receive and delete
- In this mode, when Service Bus receives the request from the consumer, it marks the message as being consumed and returns it to the consumer application. This mode is the simplest model. It works best for scenarios in which the application can tolerate not processing a message if a failure occurs. For example, consider a scenario in which the consumer issues the receive request and then crashes before processing it. As Service Bus marks the message as being consumed, the application begins consuming messages upon restart. It will miss the message that it consumed before the crash.

Peek lock:
- In this mode, the receive operation becomes two-stage, which makes it possible to support applications that can't tolerate missing messages.
- Finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then, return the message to the application.
- After the application finishes processing the message, it requests the Service Bus service to complete the second stage of the receive process. Then, the service marks the message as being consumed.
 
If the application is unable to process the message for some reason, it can request the Service Bus service to abandon the message. Service Bus unlocks the message and makes it available to be received again, either by the same consumer or by another competing consumer. Secondly, there's a timeout associated with the lock. If the application fails to process the message before the lock timeout expires, Service Bus unlocks the message and makes it available to be received again.

--------------------

Pricing tier:

As mentioned in the last unit, there are three pricing tiers available for an Azure Cache for Redis.

- Basic: Basic cache ideal for development/testing. Is limited to a single server, 53 GB of memory, and 20,000 connections. There is no SLA for this service tier.
- Standard: Production cache which supports replication and includes an SLA. It supports two servers, and has the same memory/connection limits as the Basic tier.
- Premium: Enterprise tier which builds on the Standard tier and includes persistence, clustering, and scale-out cache support. This is the highest performing tier with up to 530 GB of memory and 40,000 simultaneous connections.

-------------------

How Azure Content Delivery Network works:
1. A user (Alice) requests a file (also called an asset) by using a URL with a special domain name, such as <endpoint name>.azureedge.net. This name can be an endpoint hostname or a custom domain. The DNS routes the request to the best performing POP location, which is usually the POP that is geographically closest to the user.

2. If no edge servers in the POP have the file in their cache, the POP requests the file from the origin server. The origin server can be an Azure Web App, Azure Cloud Service, Azure Storage account, or any publicly accessible web server.

3. The origin server returns the file to an edge server in the POP.

4. An edge server in the POP caches the file and returns the file to the original requestor (Alice). The file remains cached on the edge server in the POP until the time-to-live (TTL) specified by its HTTP headers expires. If the origin server didn't specify a TTL, the default TTL is seven days.

5. Additional users can then request the same file by using the same URL that Alice used, and can also be directed to the same POP.

6. If the TTL for the file hasn't expired, the POP edge server returns the file directly from the cache. This process results in a faster, more responsive user experience.

----------

Controlling caching behavior:

- Caching rules. Caching rules can be either global (apply to all content from a specified endpoint) or custom. Custom rules apply to specific paths and file extensions.

- Query string caching. Query string caching enables you to configure how Azure CDN responds to a query string. Query string caching has no effect on files that can't be cached.


------

- Azure Storage events allow applications to react to events. Common Blob storage event scenarios include image or video processing, search indexing, or any file- oriented workflow.
Events are pushed using Azure Event Grid to subscribers such as Azure Functions, Azure Logic Apps, or even to your own http listener.
Note: Only storage accounts of kind StorageV2 (general purpose v2) and BlobStorage support event integration. Storage (general purpose v1) does not support integration with Event Grid.

- The purpose of the change feed is to provide transaction logs of all the changes that occur to the blobs and the blob metadata in your storage account. The change feed provides ordered, guaranteed, durable, immutable, read-only log of these changes. Client applications can read these logs at any time, either in streaming or in batch mode. The change feed enables you to build efficient and scalable solutions that process change events that occur in your Blob Storage account at a low cost.

- Box 1: CMD [..]
Cmd starts a new instance of the command interpreter, Cmd.exe.
Syntax: CMD <string>
Specifies the command you want to carry out.
Box 2: FROM microsoft/aspnetcore-build:latest

Box 3: WORKDIR /apps/ContosoApp -
Bxo 4: COPY ./ .
Box 5: RUN powershell ./setupScript.ps1

-------------

- Box 1: Azure Powershell -
Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS disk and any data disks.
Before you begin, make sure that you have the latest version of the Azure PowerShell module.
You use Sysprep to generalize the virtual machine, then use Azure PowerShell to create the image.

- Box 2: Azure Blob Storage -
You can store images in Azure Blob Storage.

--------------

- A: In Azure, you can run your functions directly from a deployment package file in your function app. The other option is to deploy your files in the d:\home\site
\wwwroot directory of your function app (see A above).
To enable your function app to run from a package, you just add a WEBSITE_RUN_FROM_PACKAGE setting to your function app settings.
Note: The host.json metadata file contains global configuration options that affect all functions for a function app.
- D: To customize your deployment, include a .deployment file in the repository root.
You just need to add a file to the root of your repository with the name .deployment and the content:
[config]
command = YOUR COMMAND TO RUN FOR DEPLOYMENT
this command can be just running a script (batch file) that has all that is required for your deployment, like copying files from the repository to the web root directory for example.

-----

You have two Hyper-V hosts named Host1 and Host2. Host1 has an Azure virtual machine named VM1 that was deployed by using a custom Azure Resource
Manager template.
You need to move VM1 to Host2.
What should you do?

C. From the Redeploy blade, click Redeploy. Most Voted


----------


Your company has an Azure Kubernetes Service (AKS) cluster that you manage from an Azure AD-joined device. The cluster is located in a resource group.
Developers have created an application named MyApp. MyApp was packaged into a container image.
You need to deploy the YAML manifest file for the application.
Solution: You install the Azure CLI on the device and run the kubectl apply `"f myapp.yaml command.
Does this meet the goal?

A. Yes, kubectl apply -f myapp.yaml applies a configuration change to a resource from a file or stdin.


---------------

Your company has a web app named WebApp1.
You use the WebJobs SDK to design a triggered App Service background task that automatically invokes a function in the code every time new data is received in a queue.
You are preparing to configure the service processes a queue data item.
Which of the following is the service you should use?

- WebJobs, Usually you'll host the WebJobs SDK in Azure WebJobs, but you can also run your jobs in a Worker Role. The Azure WebJobs feature of Azure Web Apps provides an easy way for you to run programs such as services or background tasks in a Web App.

-----------

Your company has an Azure subscription.
You need to deploy a number of Azure virtual machines to the subscription by using Azure Resource Manager (ARM) templates. The virtual machines will be included in a single availability set.
You need to ensure that the ARM template allows for as many virtual machines as possible to remain accessible in the event of fabric failure or maintenance.
Which of the following is the value that you should configure for the platformFaultDomainCount property?

- Max Value, The number of fault domains for managed availability sets varies by region - either two or three per region.

------------

This question requires that you evaluate the underlined text to determine if it is correct.
You company has an on-premises deployment of MongoDB, and an Azure Cosmos DB account that makes use of the MongoDB API.
You need to devise a strategy to migrate MongoDB to the Azure Cosmos DB account.
You include the Data Management Gateway tool in your migration strategy.
Instructions: Review the underlined text. If it makes the statement correct, select `No change required.` If the statement is incorrect, select the answer choice that makes the statement correct.

-  mongorestore

----------

You are developing an e-Commerce Web App.
You want to use Azure Key Vault to ensure that sign-ins to the e-Commerce Web App are secured by using Azure App Service authentication and Azure Active
Directory (AAD).
What should you do on the e-Commerce Web App?

- Enable Managed Service Identity (MSI).



------------

You have an Azure Active Directory (Azure AD) tenant.
You want to implement multi-factor authentication by making use of a conditional access policy. The conditional access policy must be applied to all users when they access the Azure portal.
Which three settings should you configure?

- Box 1:
The conditional access policy must be applied or assigned to Users and Groups.
Box 2:
The conditional access policy must be applied when users access the Azure portal, which is a cloud app. That is: Microsoft Azure Management
Box 3:
Access control must require multi-factor authentication when granting access

-----------

You manage an Azure SQL database that allows for Azure AD authentication.
You need to make sure that database developers can connect to the SQL database via Microsoft SQL Server Management Studio (SSMS). You also need to make sure the developers use their on-premises Active Directory account for authentication. Your strategy should allow for authentication prompts to be kept to a minimum.
Which of the following should you implement?

- Active Directory integrated authentication

-----

You are developing an application to transfer data between on-premises file servers and Azure Blob storage. The application stores keys, secrets, and certificates in Azure Key Vault and makes use of the Azure Key Vault APIs.
You want to configure the application to allow recovery of an accidental deletion of the key vault or key vault objects for 90 days after deletion.

What should you do?

- B. Run the az keyvault update --enable-soft-delete true --enable-purge-protection true CLI. Most Voted


-----


You are configuring a web app that delivers streaming video to users. The application makes use of continuous integration and deployment.
You need to ensure that the application is highly available and that the users' streaming experience is constant. You also want to configure the application to store data in a geographic location that is nearest to the user.
Solution: You include the use of an Azure Content Delivery Network (CDN) in your design.


- Yes

--------

You are configuring a web app that delivers streaming video to users. The application makes use of continuous integration and deployment.
You need to ensure that the application is highly available and that the users' streaming experience is constant. You also want to configure the application to store data in a geographic location that is nearest to the user.
Solution: You include the use of a Storage Area Network (SAN) in your design.
Does the solution meet the goal?

- No

--------

You develop a Web App on a tier D1 app service plan.
You notice that page load times increase during periods of peak traffic.
You want to implement automatic scaling when CPU load is above 80 percent. Your solution must minimize costs.
What should you do first?

- C. Switch to the Standard App Service tier plan. 

Configure the web app to the Standard App Service Tier. The Standard tier supports auto-scaling, and we should minimize the cost. We can then enable autoscaling on the web app, add a scale rule and add a Scale condition.

---------

Your company's Azure subscription includes an Azure Log Analytics workspace.
Your company has a hundred on-premises servers that run either Windows Server 2012 R2 or Windows Server 2016, and is linked to the Azure Log Analytics workspace. The Azure Log Analytics workspace is set up to gather performance counters associated with security from these linked servers.
You must configure alerts based on the information gathered by the Azure Log Analytics workspace.
You have to make sure that alert rules allow for dimensions, and that alert creation time should be kept to a minimum. Furthermore, a single alert notification must be created when the alert is created and when the alert is resolved.
You need to make use of the necessary signal type when creating the alert rules.
Which of the following is the option you should use?

- C. The Metric signal type.

Metric alerts in Azure Monitor provide a way to get notified when one of your metrics cross a threshold. Metric alerts work on a range of multi-dimensional platform metrics, custom metrics, Application Insights standard and custom metrics.
Note: Signals are emitted by the target resource and can be of several types. Metric, Activity log, Application Insights, and Log.

---------

You are developing a .NET Core MVC application that allows customers to research independent holiday accommodation providers.
You want to implement Azure Search to allow the application to search the index by using various criteria to locate documents related to accommodation.
You want the application to allow customers to search the index by using regular expressions.
What should you do?

- B. Configure the QueryType property of the SearchParameters class.

---------

You are a developer at your company.
You need to update the definitions for an existing Logic App.
What should you use?

- B. the Logic App Code View

Edit JSON - Azure portal -
1. Sign in to the Azure portal.
2. From the left menu, choose All services. In the search box, find "logic apps", and then from the results, select your logic app.
3. On your logic app's menu, under Development Tools, select Logic App Code View.
4. The Code View editor opens and shows your logic app definition in JSON format


----------

Note: The question is included in a number of questions that depicts the identical set-up. However, every question has a distinctive result. Establish if the solution satisfies the requirements.
You are developing a solution for a public facing API.
The API back end is hosted in an Azure App Service instance. You have implemented a RESTful service for the API back end.
You must configure back-end authentication for the API Management service instance.
Solution: You configure Basic gateway credentials for the Azure resource.
Does the solution meet the goal?

-  B. No

API Management allows to secure access to the back-end service of an API using client certificates.

----------

You are developing an application that applies a set of governance policies for internal and external services, as well as for applications.
You develop a stateful ASP.NET Core 2.1 web application named PolicyApp and deploy it to an Azure App Service Web App. The PolicyApp reacts to events from
Azure Event Grid and performs policy actions based on those events.
You have the following requirements:
✑ Authentication events must be used to monitor users when they sign in and sign out.
✑ All authentication events must be processed by PolicyApp.
✑ Sign outs must be processed as fast as possible.
What should you do?

- D. Add a subject prefix to sign-out events. Create an Azure Event Grid subscription. Configure the subscription to use the subjectBeginsWith filter.

-------

You are developing a C++ application that compiles to a native application named process.exe. The application accepts images as input and returns images in one of the following image formats: GIF, PNG, or JPEG.
You must deploy the application as an Azure Function.
You need to configure the function and host json files.
How should you complete the json files? To answer, select the appropriate options in the answer area.
NOTE: Each correct selection is worth one point.
Hot Area:

- Box 1: "type": "http"
Box 2: "customHandler": { "description":{
A custom handler is defined by configuring the host.json file with details on how to run the web server via the customHandler section.
The customHandler section points to a target as defined by the defaultExecutablePath.
Example:
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
Box 3: "enableForwardingHttpRequest": false


-------

You are building a software-as-a-service (SaaS) application that analyzes DNA data that will run on Azure virtual machines (VMs) in an availability zone. The data is stored on managed disks attached to the VM. The performance of the analysis is determined by the speed of the disk attached to the VM.

You have the following requirements:

• The application must be able to quickly revert to the previous day’s data if a systemic error is detected.
• The application must minimize downtime in the case of an Azure datacenter outage.

You need to provision the managed disk for the VM to maximize performance while meeting the requirements.

Which type of Azure Managed Disk should you use?

- Disk type --> Premium SSD
- Geo redundant storage (GRS)

-------------

You are implementing a software as a service (SaaS) ASP.NET Core web service that will run as an Azure Web App. The web service will use an on-premises
SQL Server database for storage. The web service also includes a WebJob that processes data updates. Four customers will use the web service.
✑ Each instance of the WebJob processes data for a single customer and must run as a singleton instance.
✑ Each deployment must be tested by using deployment slots prior to serving production data.
✑ Azure costs must be minimized.
✑ Azure resources must be located in an isolated network.
You need to configure the App Service plan for the Web App.
How should you configure the App Service plan? To answer, select the appropriate settings in the answer area.

- Number of VM instances: 4 -
You are not charged extra for deployment slots.

- Pricing tier: Isolated -
The App Service Environment (ASE) is a powerful feature offering of the Azure App Service that gives network isolation and improved scale capabilities. It is essentially a deployment of the Azure App Service into a subnet of a customer's Azure Virtual Network (VNet).

----------

You are a developer for a software as a service (SaaS) company that uses an Azure Function to process orders. The Azure Function currently runs on an Azure
Function app that is triggered by an Azure Storage queue.
You are preparing to migrate the Azure Function to Kubernetes using Kubernetes-based Event Driven Autoscaling (KEDA).
You need to configure Kubernetes Custom Resource Definitions (CRD) for the Azure Function.
Which CRDs should you configure?

- Box 1: Deployment -
To deploy Azure Functions to Kubernetes use the func kubernetes deploy command has several attributes that directly control how our app scales, once it is deployed to Kubernetes.

Box 2: ScaledObject -
With --polling-interval, we can control the interval used by KEDA to check Azure Service Bus Queue for messages.
Example of ScaledObject with polling interval
apiVersion: keda.k8s.io/v1alpha1
kind: ScaledObject
metadata:
name: transformer-fn
namespace: tt
labels:
deploymentName: transformer-fn
spec:
scaleTargetRef:
deploymentName: transformer-fn
pollingInterval: 5
minReplicaCount: 0
maxReplicaCount: 100

Box 3: Secret -
Store connection strings in Kubernetes Secrets.
Example: to create the Secret in our demo Namespace:
# create the k8s demo namespace
kubectl create namespace tt
# grab connection string from Azure Service Bus
KEDA_SCALER_CONNECTION_STRING=$(az servicebus queue authorization-rule keys list \
-g $RG_NAME \
--namespace-name $SBN_NAME \
--queue-name inbound \
-n keda-scaler \
--query "primaryConnectionString" \
-o tsv)
# create the kubernetes secret
kubectl create secret generic tt-keda-auth \
--from-literal KedaScaler=$KEDA_SCALER_CONNECTION_STRING \
--namespace tt

------

You develop a software as a service (SaaS) offering to manage photographs. Users upload photos to a web service which then stores the photos in Azure
Storage Blob storage. The storage account type is General-purpose V2.
When photos are uploaded, they must be processed to produce and save a mobile-friendly version of the image. The process to produce a mobile-friendly version of the image must start in less than one minute.
You need to design the process that starts the photo processing.
Solution: Trigger the photo processing from Blob storage events.
Does the solution meet the goal?

- No

-----------------

You develop and deploy an Azure App Service API app to a Windows-hosted deployment slot named Development. You create additional deployment slots named Testing and Production. You enable auto swap on the Production deployment slot.
You need to ensure that scripts run and resources are available before a swap operation occurs.
Solution: Update the web.config file to include the applicationInitialization configuration element. Specify custom initialization actions to run the scripts.
Does the solution meet the goal?

- Yes

-----

You develop and deploy an Azure App Service API app to a Windows-hosted deployment slot named Development. You create additional deployment slots named Testing and Production. You enable auto swap on the Production deployment slot.
You need to ensure that scripts run and resources are available before a swap operation occurs.
Solution: Enable auto swap for the Testing slot. Deploy the app to the Testing slot.

- No, Some apps might require custom warm-up actions before the swap. The applicationInitialization configuration element in web.config lets you specify custom initialization actions. The swap operation waits for this custom warm-up to finish before swapping with the target slot. Here's a sample web.config fragment.
<system.webServer>
<applicationInitialization>
<add initializationPage="/" hostName="[app hostname]" />
<add initializationPage="/Home/About" hostName="[app hostname]" />
</applicationInitialization>
</system.webServer>
Reference:
https://docs.microsoft.com/en-us/azure/app-service/deploy-staging-slots#troubleshoot-swaps

-------

You are developing an Azure Web App. You configure TLS mutual authentication for the web app.
You need to validate the client certificate in the web app.

- HTTP request header
- Base64

----------

You are developing a Docker/Go using Azure App Service Web App for Containers. You plan to run the container in an App Service on Linux. You identify a
Docker container image to use.
None of your current resource groups reside in a location that supports Linux. You must minimize the number of resource groups required.
You need to create the application and perform an initial deployment.
Which three Azure CLI commands should you use to develop the solution?

- You can host native Linux applications in the cloud by using Azure Web Apps. To create a Web App for Containers, you must run Azure CLI commands that create a group, then a service plan, and finally the web app itself.

Step 1: az group create -
In the Cloud Shell, create a resource group with the az group create command.
Step 2: az appservice plan create
In the Cloud Shell, create an App Service plan in the resource group with the az appservice plan create command.

Step 3: az webapp create -
In the Cloud Shell, create a web app in the myAppServicePlan App Service plan with the az webapp create command. Don't forget to replace with a unique app name, and <docker-ID> with your Docker ID.

---------

ou are developing a serverless Java application on Azure. You create a new Azure Key Vault to work with secrets from a new Azure Functions application.
The application must meet the following requirements:
✑ Reference the Azure Key Vault without requiring any changes to the Java code.
✑ Dynamically add and remove instances of the Azure Functions host based on the number of incoming application events.
✑ Ensure that instances are perpetually warm to avoid any cold starts.
✑ Connect to a VNet.
✑ Authentication to the Azure Key Vault instance must be removed if the Azure Function application is deleted.
You need to grant the Azure Functions application access to the Azure Key Vault.
Which three actions should you perform in sequence?

- Step 1: Create the Azure Functions app with a Consumption plan type.
Use the Consumption plan for serverless.
Step 2: Create a system-assigned managed identity for the application.
Create a system-assigned managed identity for your application.
Key Vault references currently only support system-assigned managed identities. User-assigned identities cannot be used.
Step 3: Create an access policy in Key Vault for the application identity.
Create an access policy in Key Vault for the application identity you created earlier. Enable the "Get" secret permission on this policy. Do not configure the
"authorized application" or applicationId settings, as this is not compatible with a managed identity.
Reference:
https://docs.microsoft.com/en-us/azure/app-service/app-service-key-vault-references

---------------

You develop a website. You plan to host the website in Azure. You expect the website to experience high traffic volumes after it is published.
You must ensure that the website remains available and responsive while minimizing cost.
You need to deploy the website.
What should you do?

- D. Deploy the website to an App Service that uses the Standard service tier. Configure the App Service plan to automatically scale when the CPU load is high. Most Voted


---------

A company is developing a Java web app. The web app code is hosted in a GitHub repository located at https://github.com/Contoso/webapp.
The web app must be evaluated before it is moved to production. You must deploy the initial code release to a deployment slot named staging.
You need to create the web app and deploy the code.
How should you complete the commands? 

- Box 1: group -
# Create a resource group.
az group create --location westeurope --name myResourceGroup

Box 2: appservice plan -
# Create an App Service plan in STANDARD tier (minimum required by deployment slots). az appservice plan create --name $webappname --resource-group myResourceGroup --sku S1

Box 3: webapp -
# Create a web app.
az webapp create --name $webappname --resource-group myResourceGroup \
--plan $webappname

Box 4: webapp deployment slot -
#Create a deployment slot with the name "staging".
az webapp deployment slot create --name $webappname --resource-group myResourceGroup \
--slot staging

Box 5: webapp deployment source -
# Deploy sample code to "staging" slot from GitHub.
az webapp deployment source config --name $webappname --resource-group myResourceGroup \
--slot staging --repo-url $gitrepo --branch master --manual-integration


--------------

You develop an HTTP triggered Azure Function app to process Azure Storage blob data. The app is triggered using an output binding on the blob.
The app continues to time out after four minutes. The app must process the blob data.
You need to ensure the app does not time out and processes the blob data.
Solution: Use the Durable Function async pattern to process the blob data.
Does the solution meet the goal?

- B. No -> Instead pass the HTTP trigger payload into an Azure Service Bus queue to be processed by a queue trigger function and return an immediate HTTP success response.
Note: Large, long-running functions can cause unexpected timeout issues.

--------

You develop an HTTP triggered Azure Function app to process Azure Storage blob data. The app is triggered using an output binding on the blob.
The app continues to time out after four minutes. The app must process the blob data.
You need to ensure the app does not time out and processes the blob data.
Solution: Pass the HTTP trigger payload into an Azure Service Bus queue to be processed by a queue trigger function and return an immediate HTTP success response.
Does the solution meet the goal?

- A, Large, long-running functions can cause unexpected timeout issues. General best practices include:
Whenever possible, refactor large functions into smaller function sets that work together and return responses fast. For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it's common for webhooks to require an immediate response. You can pass the
HTTP trigger payload into a queue to be processed by a queue trigger function. This approach lets you defer the actual work and return an immediate response.

--------

After you answer a question in this section, you will NOT be able to return to it. As a result, these questions will not appear in the review screen.
You develop an HTTP triggered Azure Function app to process Azure Storage blob data. The app is triggered using an output binding on the blob.
The app continues to time out after four minutes. The app must process the blob data.
You need to ensure the app does not time out and processes the blob data.
Solution: Configure the app to use an App Service hosting plan and enable the Always On setting.

- No, Instead pass the HTTP trigger payload into an Azure Service Bus queue to be processed by a queue trigger function and return an immediate HTTP success response.
Note: Large, long-running functions can cause unexpected timeout issues. General best practices include:
Whenever possible, refactor large functions into smaller function sets that work together and return responses fast. For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it's common for webhooks to require an immediate response. You can pass the
HTTP trigger payload into a queue to be processed by a queue trigger function. This approach lets you defer the actual work and return an immediate response.


--------


You develop a software as a service (SaaS) offering to manage photographs. Users upload photos to a web service which then stores the photos in Azure
Storage Blob storage. The storage account type is General-purpose V2.
When photos are uploaded, they must be processed to produce and save a mobile-friendly version of the image. The process to produce a mobile-friendly version of the image must start in less than one minute.
You need to design the process that starts the photo processing.
Solution: Move photo processing to an Azure Function triggered from the blob upload.
Does the solution meet the goal?

- A, Yes -> Azure Storage events allow applications to react to events. Common Blob storage event scenarios include image or video processing, search indexing, or any file- oriented workflow.
Events are pushed using Azure Event Grid to subscribers such as Azure Functions, Azure Logic Apps, or even to your own http listener.
Note: Only storage accounts of kind StorageV2 (general purpose v2) and BlobStorage support event integration. Storage (general purpose v1) does not support integration with Event Grid.

--------

