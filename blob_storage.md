#             Blob storage

```
What is blob storage?

Blob storage is a type of cloud storage service provided by cloud computing platforms such as Microsoft Azure or Amazon Web Services (AWS). It is designed to store and manage unstructured data, typically large files such as documents, images, videos, and audio files.
```

```
Difference between blob storage and the file system of Linux/Windows/Mac (hierachical file storage)

Blob Storage: Blob storage is a flat storage system that organizes data in the form of binary large objects (BLOBs) or files. It does not have a hierarchical structure like traditional file systems.
File System: Linux, Windows, and macOS file systems are hierarchical, meaning they organize data in a directory-based structure. Files and directories are arranged in a tree-like hierarchy, allowing for easy organization and navigation.
Access Methods:

Blob Storage: Blob storage is often accessed through a Representational State Transfer (REST) API or software development kits (SDKs) provided by cloud storage providers. It is primarily used for cloud-based applications and object storage scenarios.
File System: The file systems in Linux, Windows, and macOS are typically accessed through the operating system's file management APIs. They provide access to files and directories through file paths, allowing applications and users to interact with the file system directly.
Metadata and Attributes:

Blob Storage: Blob storage allows users to associate custom metadata with individual objects or files. This metadata can provide additional information about the stored data but is typically limited to key-value pairs.
File System: Hierarchical file systems support a broader range of metadata and attributes for files and directories. This can include permissions, ownership, timestamps, file types, and more. File systems often provide extended metadata for better file management and security.
Storage Efficiency:

Blob Storage: Blob storage is optimized for storing large amounts of unstructured data efficiently. It provides excellent scalability and can handle massive datasets without requiring the overhead of maintaining a hierarchical structure.
File System: Hierarchical file systems are designed to provide efficient access to individual files within a directory structure. They are well-suited for organizing and managing smaller sets of files, with features like indexing and file search capabilities.
Use Cases:

Blob Storage: Blob storage is commonly used for scenarios such as cloud backup, archival storage, content distribution, and serving static assets for web applications. It is ideal for scenarios where data is accessed as a whole object rather than in a file-by-file manner.
File System: Hierarchical file systems are used in a wide range of applications and operating systems. They provide the foundation for managing user files, system files, software installations, and facilitating file sharing and collaboration.
```

```
## Advantages/disadvantages of blob storage

Blob storage, such as Azure Blob Storage or Amazon S3, is a popular solution for storing unstructured data like images, videos, documents, and other files. Here are some advantages and disadvantages of using blob storage:

Advantages of Blob Storage:

Scalability: Blob storage provides virtually unlimited scalability, allowing you to store and manage large amounts of data without worrying about capacity constraints. It can seamlessly handle a wide range of workloads, from small-scale applications to enterprise-level storage needs.

Cost-effective: Blob storage offers a cost-effective solution for storing massive amounts of data. It typically follows a pay-as-you-go pricing model, where you pay only for the storage you consume, without any upfront costs or long-term commitments. This makes it suitable for both small startups and large enterprises.

Durability and Redundancy: Blob storage systems are designed with high durability and redundancy in mind. They store multiple copies of your data across different physical locations or data centers, ensuring data availability even in the event of hardware failures or natural disasters.

Accessibility: Blob storage provides easy and convenient access to your data. You can access your blobs programmatically through APIs or use graphical interfaces provided by the cloud provider. This accessibility makes it suitable for various applications, including web and mobile apps, data backups, and content distribution.

Security: Blob storage platforms offer robust security features to protect your data. They typically provide authentication mechanisms, access controls, encryption at rest and in transit, and compliance certifications to meet regulatory requirements. This helps in safeguarding sensitive information stored in the blobs.

Disadvantages of Blob Storage:

Limited Querying Capabilities: Blob storage is primarily designed for storing and retrieving objects as a whole. While you can retrieve individual files, the querying capabilities are limited compared to structured databases. If you need complex querying or advanced search functionalities, you might need to consider additional services or tools to complement blob storage.

Lack of Transactional Support: Blob storage is optimized for storing large objects and does not provide transactional support at the object level. This means that updating or modifying parts of a blob can be challenging. If you require transactional operations or atomicity for your data modifications, a different storage solution like a database might be more suitable.

Latency and Performance: Blob storage is designed for high scalability and availability, but it may have higher latency and lower performance compared to storage solutions optimized for structured data. The time it takes to retrieve or upload large blobs can be longer compared to accessing smaller pieces of data in a structured storage system.

Learning Curve: Utilizing blob storage effectively may require a learning curve, especially if you are new to cloud storage concepts or the specific platform you are using. Understanding the APIs, access controls, and other features may take some time and effort, particularly if you have a complex storage architecture.
```




![img_1.png](../img_1.png)




![img.png](../img.png)


![img_2.png](../img_2.png)

```
## Parts of Azure blob storage: account, container, blobs - how do they relate?

In Azure Blob Storage, the three main components are the storage account, containers, and blobs. Here's how they relate to each other:

Storage Account: A storage account is the top-level entity in Azure Blob Storage. It provides a unique namespace for your storage resources and acts as a container for your containers and blobs. When you create a storage account, you specify a globally unique name that identifies it, such as "myblobstorage."

Containers: Containers are logical units used for organizing and categorizing blobs within a storage account. They are similar to folders in a file system and help you manage and secure your blobs. You can think of containers as a way to group related blobs together. For example, you might have containers for storing images, documents, or backups. Containers have a flat hierarchy, meaning that they cannot be nested within each other.

Blobs: Blobs (Binary Large Objects) are the actual data objects stored in Azure Blob Storage. They can store any type of data, such as text, images, videos, or binary files. Blobs are stored inside containers and are uniquely identified by a name within their container. Blob names can include slashes to simulate a hierarchical structure, but it's important to note that this is just a naming convention and does not represent actual folder hierarchy.
```


![img_3.png](../img_3.png)


![img_4.png](../img_4.png)

![img_5.png](../img_5.png)

```
# Research Task 5.1b: Redundancy

In Microsoft Azure, block blob storage provides a reliable and scalable solution for storing large amounts of unstructured data, such as documents, images, videos, and backups. To ensure data durability and availability, Azure offers different types of redundancy for block blob storage. Here are the primary redundancy options available:

Redundancy in the primary region
Data in an Azure Storage account is always replicated three times in the primary region. Azure Storage offers two options for how your data is replicated in the primary region:

Locally redundant storage (LRS) copies your data synchronously three times within a single physical location in the primary region. LRS is the least expensive replication option, but isn't recommended for applications requiring high availability or durability.

Zone-redundant storage (ZRS) copies your data synchronously across three Azure availability zones in the primary region. For applications requiring high availability, Microsoft recommends using ZRS in the primary region, and also replicating to a secondary region.

Geo-Redundant Storage (GRS): GRS provides data replication across multiple regions, ensuring data durability even in the event of a regional outage. In addition to the locally redundant copies within the primary region, GRS asynchronously replicates the data to a secondary region, located hundreds of miles away from the primary region. GRS offers higher durability and availability than LRS or ZRS, making it suitable for business-critical applications.

Read-Access Geo-Redundant Storage (RA-GRS): RA-GRS provides the same redundancy as GRS, with the added benefit of read access to the data in the secondary region. This means that even if the primary region is unavailable, you can read the data from the secondary region. It provides an option for read-only access to data during primary region disruptions, making it useful for scenarios that require continuous access to data.

GZRS (Geo-Zone-Redundant Storage): GZRS combines the benefits of ZRS and GRS by synchronously replicating data across multiple availability zones within the primary region and asynchronously replicating it to a secondary region for enhanced durability and availability.

RA-GZRS (Read-Access Geo-Zone-Redundant Storage): RA-GZRS combines the features of RA-GRS and GZRS, providing synchronous replication across availability zones in the primary region, asynchronous replication to a secondary region, and read access to the replicated data in both regions for maximum durability, availability, and data access capabilities.
```

