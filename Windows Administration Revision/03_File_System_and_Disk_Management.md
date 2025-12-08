# 03: File System and Disk Management

Effective storage management is a core responsibility of a Windows Administrator. This involves understanding file systems, disk types, and technologies that provide redundancy and efficiency.

## 1. File Systems

-   **NTFS (New Technology File System)**:
    -   The standard file system for Windows.
    -   **Features**:
        -   **Security**: Supports file and folder-level permissions (ACLs - Access Control Lists).
        -   **Encryption**: Supports EFS (Encrypting File System) and BitLocker.
        -   **Compression**: Built-in file compression to save disk space.
        -   **Quotas**: Can limit the amount of disk space a user can consume.
        -   **Journaling**: Improves reliability by logging changes before they are written to the disk.

-   **ReFS (Resilient File System)**:
    -   A newer file system from Microsoft, designed for specific use cases.
    -   **Features**:
        -   **Resiliency**: Built to be more resilient to data corruption. It can automatically detect and repair corruption online.
        -   **Scalability**: Designed for very large data sets.
        -   **Not Bootable**: You cannot install Windows on an ReFS volume.
    -   **Use Cases**: Best suited for virtualization (Hyper-V) and large-scale file storage.

## 2. Disk Management

The **Disk Management** console (`diskmgmt.msc`) is used to manage physical and virtual disks.

### Partition Styles

-   **MBR (Master Boot Record)**:
    -   Older standard.
    -   Supports up to 4 primary partitions (or 3 primary and 1 extended).
    -   Limited to 2TB per partition.
-   **GPT (GUID Partition Table)**:
    -   Modern standard.
    -   Supports up to 128 partitions.
    -   Supports partitions larger than 2TB.
    -   Required for UEFI-based systems.

### Disk Types

-   **Basic Disks**: The standard disk type. Contains primary partitions, extended partitions, and logical drives. Simple and widely compatible.
-   **Dynamic Disks**: Offer more flexibility than basic disks. Support software-based RAID volumes (spanned, striped, mirrored, RAID-5).

## 3. RAID (Redundant Array of Independent Disks)

RAID combines multiple physical disks into a single logical unit to improve performance or provide redundancy. Windows Server supports software-based RAID using Dynamic Disks.

-   **RAID 0 (Striping)**:
    -   **How it works**: Data is split and written across multiple disks.
    -   **Pros**: Increased read/write performance.
    -   **Cons**: No redundancy. If one disk fails, all data is lost.
    -   **Minimum Disks**: 2.

-   **RAID 1 (Mirroring)**:
    -   **How it works**: Data is duplicated on two disks.
    -   **Pros**: High redundancy. If one disk fails, the other continues to work.
    -   **Cons**: 50% of storage capacity is used for mirroring.
    -   **Minimum Disks**: 2.

-   **RAID 5 (Striping with Parity)**:
    -   **How it works**: Data is striped across multiple disks, and a parity block is written to one of the disks.
    -   **Pros**: Good balance of performance and redundancy.
    -   **Cons**: Write performance is slower due to parity calculations. Can only tolerate the failure of a single disk.
    -   **Minimum Disks**: 3.

## 4. Distributed File System (DFS)

DFS is a set of services that allows you to group shared folders located on different servers into one or more logically structured namespaces.

-   **DFS Namespace**:
    -   Creates a virtual folder structure that presents shares from different servers as a single, unified folder.
    -   **Example**: `\yourdomain\
Public\
Software` could point to `\Server1\
Software` and `\yourdomain\
Public\
Documents` could point to `\Server2\
Docs`.
    -   Users don't need to know the actual server names.

-   **DFS Replication**:
    -   Synchronizes the content of folders between servers.
    -   Often used in combination with DFS Namespace to provide high availability and load balancing for file shares. If one server goes down, users are automatically redirected to another server with a replica of the data.

## 5. Encrypting File System (EFS)

-   **Purpose**: A feature of NTFS that provides file-level encryption.
-   **How it Works**:
    -   EFS uses a combination of symmetric and asymmetric encryption.
    -   When a user encrypts a file, a unique symmetric key (FEK - File Encryption Key) is generated. The file is encrypted with this FEK.
    -   The FEK is then encrypted with the user's public key and stored with the file.
    -   When the user opens the file, their private key is used to decrypt the FEK, which then decrypts the file.
-   **Key Point**: Encryption is tied to the user account. If another user tries to open the file, they won't have the correct private key and will be denied access, even if they have file permissions.

## 6. Data Deduplication

-   **Purpose**: A feature in Windows Server that saves disk space by finding and removing duplicate chunks of data.
-   **How it Works**:
    1.  The file is broken down into small chunks.
    2.  Each chunk is assigned a unique identifier.
    3.  If a chunk already exists in the "chunk store", the file is updated with a pointer to the existing chunk. If the chunk is new, it is added to the store.
-   **Benefits**:
    -   Significant space savings, especially for file shares that contain many similar files (e.g., user home directories, software installation files).
-   **Use Cases**: Best for general file shares, software deployment shares, and VHD libraries. Not recommended for running databases or other high-I/O applications.
