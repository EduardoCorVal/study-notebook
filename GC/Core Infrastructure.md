# M1. Introducing GC

IaaS - Infrastruture as a service: _Pay for what they allocate_
    - Raw compute
    - Storage
    - Network capabilities

PaaS - Platform as a service: _Pay for what they use_

*RPCs: Remote produce calls:* Services can communicate with each other. It's encrypted between data centers

# M2. Resources and Access in the Cloud

Resources are hiererchical. 

An Organization has:
    - Folders (it can contain subfolders): 
      - Projects:
        - Resources:

`Hierarchy determines policies -> Policies are inherited downward`

IAM roles: What a person/resource can do. Roles have permissions associated
    - Note: Predefine roles are not mutable -> You can create your own custom role

*Service accounts* -> Are assgined roles

_Cloud identity:_ Manages team and organization access:
  - Gmail account:
  - GC Console:
  - Google groups:

*Services and APIs are enabled on a per-project basis*

# M3 Virtual Machines and Networks in the Cloud

VPC networks connect GC resources to each other and to the internet:
  - Segmenting networks
  - Using firewall rules to restrict access to instances
  - Creating static routes to forward traffic to specific destinations

* A VPC can have subnets in diferents regions/zones
* VPCs do not require a router to be provisioned
* VPCs do not require a firewall to be provisioned
  * _Rules can be dfined through neetwork tags on instances_

**VPC peering**
VPCs belong to GC projects. Peering allows you to establish a relationshipt between two VPCs. They can be estabished to exchange traffic. 
  
**Load balancing**
Distributes traffic across instances It has types:
  - Global HTTP(S)
  - Global SSL Proxy: Secure Sockets Layer
  - Global TCP Proxy
  - Regional
  - Regional internal
  - Internal HTTP(S)

**DNS**
Domain Name Service. Uses 8.8.8.8
  - Low latency, high availability, cost-effective way to make applications and services availaible to users
  - Served redundant locations around the world
  - Cloud DNS is programmable. You can publish and manage millions of DNS zones and records

**Edge caching**
The use of caching servers to store content closer to users

**CDN: Content Delivery Network**
Meant to _lower network latency_ -> Origins of content will experience reduced load -> Save money

**Ways to connect to other networks**
  - *Cloud VPN*: Uses cloud Router to make connection dynamic (uses border gateway protocol). Has security concerns and bandwidth reliability
  - *Direct peering*: _Puts a router in the same public datacenter as a Google point of presence (PoP)_. Uses router to exchange traffic between networks. Connects to more than 100 Google points of presence around the world
  - *Carrier peering*: Gives direct access from an on-premises network through a service provider's network (Google workspace and GC products). Note: **Not covered by SLA**
  - *Dedicated Interconnect*: A direct connection to Google. 1 or more direct, private connections to google. Can be **covered up to 99% SLA**. Connections can be backed up by a VPN for even grater reliability
  - *Partner interconnect*: Connectivity between an on-premises network and a VPC network through a supported service provider. Can support mission-critical services or applications that **can tolerate 99.99% SLA**
  - *Cross-Cloud Interconnect*: Establish high-bandwidth dedicated connectivity between GC and another cloud service provider. Multicloud strategy. Two connection sizes: 10 Gbps or 100 Gbps

# M4 Storage

**Cloud Storage**
  - *File storage:* Folder hierarchy
  - *Block storage:* Chunks of a disk
  - *Object storage:* Binary form of the actual data itself -> They are **immutable**. You can not edit them, but instead a new version is created with every change made. I allows rerversions. **Larger than 10 MG. Petabytes -> Max unit 5TB per object**

_Commoun uses: Binary large-object (BLOB) storage_: 
  * Online content
  * Backup and archiving
  * Storage of intermediate results

_Storage classes_:
How constant you want to access the data
  - Stardard: Hot data
  - Nearline: Once per month
  - Coldline: Once every 90 days
  - Archive: Once a year
And **Autoclass** -> Automatically transitions objects to appropiate storage classes based on each object's access pattern

**SQL**
Fully managed relational databases: MySQL, PostgreSQL, SQL server **Up to 64TB**

**Spanner**
Fully managed relational database. _Scales horizontally_. Good for joins and secondary indexes **Petabytes**

**Firestore**
For mobile and web development. A NoSQL database -> Data as documents (that live in a collection) **Terabytes. Max unit size: 1 MB per entity**

**Big table**
NoSQL big data database. Grear for operational applications and analytical applications (good for machine learning algorithms). It's used to _stream data_. **Petabytes. Max unit 10 MB p/cell, 100 MB p/row**

# M5 Containers

It scales like a PaaS, but gives nearly the sam flexibility as IaaS -> _You can scale by duplicating single containers. Also scale an application with multiple containers_

**Kubernetes**
- Platform for managing containerized workloads and services
- It makes it easy to orchestrate many containers on many hosts, scale them as microservices, and deploy rollouts and rollbacks
- At the highest level, **it's a set of API's to deploy containers on a set of nodes called a cluster**
- It's divided into a set of primary components that run as the control plane and a set of nodes that run containers
- You can describe a set of applications and how they should interact with each other and Kubernates figures how to make that happen

*Containers run in groups called 'pods'*:
- Cluster K1:
  - Pod (Unique ID) -> Smallest unit (Node). It represents *a running process on your cluster as either a componen of you application or an entire app*: 
    - It has one OR multuple containers

*Pods have fixes IP's to connect to services*
Kubernates creates a Service with a fixes IP address for Pods -> It attaches a network load balancer woth publick IP to the cluster
  - A client reaches that IP and will be routed to a pod behind the service. _Service: Defines a logical set of pods and a policy by whitch to access them_
  - Each Pod will be assigned their own IP address, but those addresses don't remain stable over time
  - _Service group is a set of pods and provides a stable endpoint (or fixed IP address) for them_

*Deployments can be scaled on command*

- Kubernates are defined and manipulated by config file (.yaml)
- Endpoints can be discovered using kubectl command
- Rolling updates can by triggered on the command line or by updating the configuration file

**GKE: Google's managed Kubernates service**:
GKE manages all the control plane components for us. It's responsible for provisioning and managing all the control plane infrastructure behind it
  - *Autopilot mode:* Optimized for production, strong security posture

# Discounts

- VMs: _Sustained-use discounts_ starts to apply automatically to vms the longer they run. For each vm that runs for more than 25% of a month, Compute engine automatically applies a discount for every addtional minute
- _Committted-use discounts_: For stable and predictable workloads, a specific amount of vCPUs and memory can be purchased for up to 57% discount off normal prices in return for committing to a usage term of one year or three years
- _Preemptible and Spot VMs:_: Workloads that doesn't requiere a human to monitor, like a batch job of anaylzing a dataset. It can save up to 90%. Compute Engine has permissions to terminate a job if its resources are needed elsewhere. While savings can be had, you'll need to ensure yout job can be stopped and restarted
- _Spot VMs_: Preemptible can only run for yp to 24 hours at a time. Spot VMs do not have a maximimun runtime