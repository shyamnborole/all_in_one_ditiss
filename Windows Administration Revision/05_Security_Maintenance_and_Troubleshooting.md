# 05: Security, Maintenance, and Troubleshooting

This section covers the tools and practices used to secure, maintain, and troubleshoot a Windows Server environment.

## 1. Security Policies

### Group Policy Objects (GPOs)

-   **Purpose**: GPOs are virtual collections of policy settings that can be applied to users and computers in an Active Directory domain. They are the primary tool for enforcing security and configuration settings across an enterprise.
-   **Management**: GPOs are created and managed using the **Group Policy Management Console (GPMC)**.
-   **Application Order (LSDOU)**: GPOs are applied in a specific order, with later policies overwriting earlier ones if there are conflicts.
    1.  **L**ocal Policies
    2.  **S**ite GPOs
    3.  **D**omain GPOs
    4.  **O**rganizational **U**nit (OU) GPOs (including nested OUs)

-   **Common Uses**:
    -   Enforcing password complexity requirements.
    -   Restricting access to Control Panel applets.
    -   Mapping network drives.
    -   Deploying printers.
    -   Installing software.
    -   Configuring Windows Firewall settings.

### Local Policies

-   **Purpose**: Every Windows computer has a set of local policies, which are applied before any domain-based GPOs.
-   **Management**: Edited using the **Local Group Policy Editor** (`gpedit.msc`).
-   **Key Difference**: Local policies only affect the computer they are configured on, whereas domain-based GPOs can affect thousands of computers. In a domain environment, domain GPOs will override conflicting local policy settings.

## 2. Windows Server Backup (WSB)

-   **Purpose**: A feature that provides backup and recovery options for Windows Server.
-   **Installation**: WSB is not installed by default and must be added as a feature through Server Manager.
-   **Backup Types**:
    -   **Full Server Backup**: Backs up all server data, applications, and system state.
    -   **Bare Metal Recovery**: A type of full server backup that allows you to restore your server to a new piece of hardware.
    -   **System State Backup**: Backs up critical system components, including Active Directory, the registry, and boot files. Essential for recovering a domain controller.
    -   **Specific Files/Folders/Volumes**: Allows for granular backups.

-   **Backup Destinations**: Backups can be stored on a local drive, an external drive, or a network share.

## 3. General Maintenance and Troubleshooting

### Event Viewer (`eventvwr.msc`)

-   **Purpose**: A tool that displays detailed information about significant events on a computer. It is the first place you should look when troubleshooting an issue.
-   **Windows Logs**:
    -   **Application**: Logs events from applications and programs.
    -   **Security**: Logs security-related events, such as successful and failed logon attempts. Auditing must be configured for this log to be populated.
    -   **System**: Logs events from Windows system components, such as driver failures or services starting/stopping.
    -   **Setup**: Logs events related to application setup.
-   **Event Levels**:
    -   **Information**: An event that describes the successful operation of a task.
    -   **Warning**: An event that is not necessarily significant, but might indicate a possible future problem.
    -   **Error**: A significant problem, such as a loss of data or loss of functionality.

### Performance Monitor (`perfmon.msc`)

-   **Purpose**: A tool for analyzing how programs you run affect your computer's performance, both in real time and by collecting log data for later analysis.
-   **Counters**: You can monitor thousands of counters related to CPU, memory, disk, and network performance.
-   **Data Collector Sets**: Allow you to collect performance data over a period of time and save it to a log file.

### Task Manager (`taskmgr.exe`)

-   **Purpose**: Provides a real-time view of the performance of your computer.
-   **Key Tabs**:
    -   **Processes**: Shows running applications and background processes, along with their CPU, memory, disk, and network usage.
    -   **Performance**: Displays real-time graphs of CPU, memory, disk, and network utilization.
    -   **Services**: Allows you to view the status of services and start or stop them.
    -   **Startup**: Shows which applications are configured to run at startup.
