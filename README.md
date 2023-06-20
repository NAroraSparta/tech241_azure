```azure
What is AZURE cloud?
Azure is a cloud computing platform and a suite of services offered by Microsoft. It provides a wide range of cloud-based services for building, deploying, and managing applications and services through Microsoft-managed data centers. Azure offers a comprehensive set of tools and services that enable developers, IT professionals, and businesses to leverage the power of the cloud.

Some key features and services provided by Azure include:

Virtual machines: Azure allows you to create and manage virtual machines in the cloud, enabling you to run applications and services without the need for physical hardware.

Storage: Azure provides various storage options, including Blob storage for unstructured data, Azure Files for file-based storage, and Azure Disk Storage for durable, high-performance disk storage.

App Services: Azure App Service enables you to build, deploy, and scale web and mobile applications. It supports multiple programming languages and frameworks.

Databases: Azure offers managed database services such as Azure SQL Database for relational data, Azure Cosmos DB for globally distributed NoSQL databases, and Azure Database for MySQL and PostgreSQL.

Networking: Azure provides networking services to create and manage virtual networks, load balancers, VPN gateways, and other network-related resources.

AI and Machine Learning: Azure offers a suite of AI and machine learning services, including Azure Machine Learning, Azure Cognitive Services, and Azure Bot Service, to help developers build intelligent applications.

Analytics: Azure provides various services for data analytics, including Azure Synapse Analytics, Azure Data Lake Storage, and Azure HDInsight, which allow you to process and analyze large volumes of data.

Internet of Things (IoT): Azure IoT Suite helps you connect, monitor, and manage IoT devices and build IoT applications using Azure IoT Hub, Azure IoT Central, and other related services.

DevOps: Azure DevOps services enable teams to plan, develop, test, and deliver applications efficiently. It includes services like Azure DevOps Boards, Repos, Pipelines, and Test Plans.

Security and Identity: Azure provides robust security features and services to help protect your applications and data. It includes Azure Active Directory for identity and access management, Azure Security Center for threat detection and monitoring, and Azure Key Vault for securely storing and managing cryptographic keys and secrets.
```




```azure
The statement you provided outlines four levels of organization commonly used in cloud computing environments, particularly in Microsoft Azure. These levels are:

Management Groups: Management groups are the highest level of organization in Azure and are used to provide a hierarchical structure for managing resources. They help to establish a consistent set of policies and permissions across multiple Azure subscriptions. Management groups allow you to group subscriptions together to apply policies, access controls, and reporting at scale.

Subscriptions: Subscriptions represent a billing and management container in Azure. They act as a logical boundary for deploying and managing resources. Subscriptions are typically associated with an individual or an organization and provide access to Azure services based on the subscription type and associated permissions.

Resource Groups: Resource groups are containers that help organize and manage resources within an Azure subscription. They serve as a logical grouping mechanism for resources that belong to the same application, project, or deployment. Resources within a resource group share common lifecycle, permissions, and policies.

Resources: Resources are the individual components and services that you deploy and manage within Azure. Examples of resources include virtual machines, storage accounts, databases, virtual networks, and more. Resources are typically grouped within resource groups for better organization and management.
```

```python
Steps for setting up an Azure VM

1. Install Git Bash
2. Go to your Home directory using cd
3. Make .ssh folder using mkdir .ssh 
4. Alternately open .ssh folder using cd .ssh
5. Create a keypair on your local computer in the .ssh folder 
using this command:
ssh-keygen -t rsa -b 4096 -C <"personal email">
6. Give the name to the in which to save the key
 e.g. tech241-neha-az-key (git bash)
7. To access the key, use:
cat tech241-neha-az-key.pub (git bash)
8. Go to azure by using portal.azure.com
9. Go to SSH Keys
10. Fill in the name of the key you created using GitBash
in your local computer.
11. Use <upload existing public key>
12. Paste the key in the box provided.
13. Click review n create to validate your key.
14. Create a virtual azure machine using these specifications.
# Security type standard,
# Image Ubuntu Server 18.04 LTS. 
# Size standard_B1s. 
# Username adminuser. 
# Stored keys tech241-neha-az-key. 
# Inbound ports SSH and HTTP.
# Disk type Standard SSD
15. Click connect on virtual machine page (azure) and put your keyname in:
chmod 400 <keyname>
16. Copy this command and paste this into Git Bash
17. Use ls -l to see if it has worked. You'll see read permissions.
-r--r--r-- 1 Venkat 197121 3389 Jun 20 15:47 <tech421-neha-az-key>
18. Go back to azure VM and type in 
~/.ssh/tech421-neha-az-key in the private key path.
19.  Copy the path from Run the example command below to to connect to your VM.
 ssh -i ~/.ssh/tech421-neha-az-key adminuser@20.58.17.237
20. Enter yes to authenticity fingerprint and you have connected with your remote machine.
21. ls -a to check hidden files
22. Stop vm on azure portal if you are not using it. 
```


```
Virtulisation
What is virtualisation?
Virtualisation is the process of creating a virtual version of a resource, such as an operating system, server, storage device, or network, to simulate the behaviour of the physical counterpart.

What is a virtual machine?
A virtual machine (VM) is a software emulation of a physical computer, allowing multiple operating systems or applications to run on a single physical machine.

Where can they be run?
Virtual machines can be run on various platforms, including desktop computers, servers, cloud infrastructure, and data centres.

What determines how many can run?
The number of virtual machines that can run depends on the available resources, such as CPU, memory, storage, and network bandwidth of the underlying physical machine or virtualisation host.

What does a virtual machine include?
A virtual machine includes a virtualised hardware environment (processor, memory, storage), an operating system, and any software applications installed within it.

What software is required to orchestrate/run the virtual machines?
To orchestrate and run virtual machines, specialised software called a hypervisor or virtual machine monitor (VMM) is required. Examples include VMware vSphere, Microsoft Hyper-V, and KVM (Kernel-based Virtual Machine).

What is the importance of an image when creating an VM?
An image is a preconfigured software template or snapshot that contains the necessary files and settings to create a virtual machine. It serves as a blueprint for the VM's initial state and enables easy deployment and replication of virtual machines.
```


