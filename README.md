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



