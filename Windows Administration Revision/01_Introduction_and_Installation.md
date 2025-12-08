# 01: Windows OS Fundamentals & Installation

## 1. Overview of Windows Operating Systems

Windows operating systems can be broadly categorized into two families: **Desktop OS** and **Server OS**.

### Windows Desktop OS

-   **Purpose**: Designed for end-users in home or small office environments.
-   **Examples**: Windows 10, Windows 11.
-   **Key Features**:
    -   User-friendly graphical interface (GUI).
    -   Optimized for foreground applications (e.g., web browsers, office suites, games).
    -   Limited to 20 concurrent network connections.

#### Windows 10 Editions

| Edition            | Key Features                                                                                                 | Target Audience                               |
| ------------------ | ------------------------------------------------------------------------------------------------------------ | --------------------------------------------- |
| **Home**           | Core features like Cortana, Microsoft Edge, Windows Hello, and device encryption.                            | Home users                                    |
| **Pro**            | Includes all Home features plus Active Directory, BitLocker, Remote Desktop, and Hyper-V.                      | Small to medium businesses, IT professionals  |
| **Enterprise**     | All Pro features plus advanced security and management features like AppLocker, Credential Guard, DirectAccess. | Large organizations                           |
| **Education**      | Builds on Enterprise with education-specific defaults.                                                       | Academic institutions                         |

### Windows Server OS

-   **Purpose**: Designed for medium to large enterprises to manage network resources and provide services to clients.
-   **Examples**: Windows Server 2016, Windows Server 2019, Windows Server 2022.
-   **Key Features**:
    -   **Scalability**: Supports significantly more RAM and CPU cores than desktop editions (e.g., Windows Server 2022 supports up to 48TB of RAM and 64 sockets with up to 2048 logical processors).
    -   **Unlimited Connections**: Can handle a virtually unlimited number of incoming network connections (requires appropriate licensing).
    -   **Network Services**: Built-in support for critical network services like **DHCP**, **DNS**, **Active Directory**, and **IIS (Web Server)**.
    -   **Performance**: Optimized for background tasks and services.

---

## 2. Windows Licensing

-   **Retail (FPP - Full Packaged Product)**: Purchased from a retail store. Can be transferred to a new computer.
-   **OEM (Original Equipment Manufacturer)**: Pre-installed by the hardware manufacturer. Tied to the specific device it was installed on.
-   **Volume Licensing**: A single license key can be used for multiple installations. Typically used by large organizations.

---

## 3. Virtualization and Hyper-V

**Virtualization** is the process of creating a virtual (rather than actual) version of something, such as a server, desktop, storage device, or network.

### Hypervisors

A **hypervisor** is a software layer that creates and runs virtual machines (VMs).

-   **Type 1 (Bare Metal)**: Runs directly on the host's hardware. It is more efficient and secure.
    -   **Examples**: Microsoft Hyper-V, VMware ESXi.
-   **Type 2 (Hosted)**: Runs as an application on top of an existing operating system.
    -   **Examples**: Oracle VirtualBox, VMware Workstation Player.

### Microsoft Hyper-V

-   A **Type 1 hypervisor** included with Windows Pro, Enterprise, and all Windows Server editions.
-   Allows you to create and manage VMs to run different operating systems on a single physical server.
-   **Key Features**:
    -   **Live Migration**: Move running VMs from one Hyper-V host to another without downtime.
    -   **Replication**: Replicate VMs to another location for disaster recovery.
    -   **Checkpoints**: Save the state of a VM, which you can revert to later.

---

## 4. Windows Server Installation

Installing Windows Server involves the following general steps:

1.  **Obtain Installation Media**: Download the Windows Server ISO from Microsoft or create a bootable USB drive.
2.  **Boot from Media**: Start the server and boot from the installation media.
3.  **Choose Installation Options**:
    -   Select language, time, and keyboard preferences.
    -   Enter the product key (if required).
    -   Choose the edition to install (e.g., Standard or Datacenter).
    -   Select the installation type:
        -   **Server Core**: A minimal installation with no GUI. Managed via command line (PowerShell/CMD) or remotely. More secure and has a smaller footprint.
        -   **Desktop Experience**: A full installation with the standard GUI.
4.  **Disk Partitioning**: Select the drive and partition where you want to install the OS.
5.  **Complete Installation**: The installer will copy files and restart the server.
6.  **Post-Installation Tasks**:
    -   Set the Administrator password.
    -   Configure networking (static IP address).
    -   Change the computer name.
    -   Activate Windows.
    -   Install updates.
    -   Install necessary roles and features (e.g., Active Directory, DNS).

---

## 5. Windows Deployment Services (WDS)

-   **Purpose**: A server role used to deploy Windows operating systems over the network. It allows for unattended installations, which saves time and reduces errors.
-   **How it Works**:
    1.  A client computer with a PXE-enabled network card boots up and contacts the WDS server.
    2.  The WDS server provides a boot image to the client.
    3.  The client loads the boot image, which then connects back to the WDS server to download and install the full operating system image.
-   **Requirements**:
    -   Active Directory
    -   DHCP
    -   DNS
    -   An NTFS partition on the WDS server to store images.
