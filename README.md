AZ 204
--------

Azure Virtual Network(Vnet): 
An Azure Virtual Network(Vnet) is a representation of your own network in the cloud. It is a logical isolation of the Azure cloud dedicated to your subscription. Vnet is similar to a traditional network that you'd operate in your own data center, but brings with it additional benefits of Azure's infrastructure such as scale, availability, and isolation. 


Azure Cosmos DB: 
Used for data that is constantly updated. It supports schema-less data 

Azure Blob Storage: 
Supports unstructured data, and large files 

Azure Queue: 
Service for storing large numbers of messages that can be accessed from anywhere in the world.  Used to pass messages between different Azure web servers 

Azure Redundancy:
Locally redundant storage -> Locally redundant storage (LRS) replicates your storage account three times within a single data center in the primary region.
Zone-redundant storage -> Zone-redundant storage (ZRS) replicates your storage account synchronously across three Azure availability zones in the primary region. Each availability zone is a separate physical location with independent power, cooling, and networking.

AZ webapp current list linux:
az webapp list-runtimes --os-type linux

Azure App Service Plans:
App service plan -> App(s)

Isolate your app into a new App Service plan when:
The app is resource-intensive.
You want to scale the app independently from the other apps in the existing plan.
The app needs resource in a different geographical region

