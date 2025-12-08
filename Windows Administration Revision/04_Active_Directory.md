# 04: Server Roles and Active Directory

Active Directory (AD) is the heart of a Windows domain environment, providing centralized authentication and authorization.

## 1. Active Directory Domain Services (AD DS)

AD DS is the core service that stores directory data and manages communication between users and domains.

### Logical Components

-   **Domain**: A logical group of objects (users, computers, groups, printers) that share a common security database and policies. Example: `mycompany.com`.
-   **Organizational Unit (OU)**: A container within a domain that can hold users, groups, and computers. OUs are used to delegate administrative control and apply Group Policies.
-   **Tree**: A collection of one or more domains that share a contiguous namespace. The first domain is the parent, and subsequent domains are children (e.g., `mycompany.com` is the parent, and `sales.mycompany.com` is a child).
-   **Forest**: A collection of one or more domain trees that do not share a contiguous namespace but are connected by a two-way trust relationship. The first domain created in the forest is called the **forest root domain**.

### Physical Components

-   **Domain Controller (DC)**: A server running the AD DS role. It stores a writable copy of the Active Directory database (`NTDS.DIT`) and is responsible for authenticating users and enforcing security policies.
-   **Additional Domain Controller (ADC)**: A backup domain controller that also holds a writable copy of the AD database. It provides redundancy and load balancing for authentication requests.
-   **Sites**: Represent the physical topology of the network. A site is a group of well-connected computers (e.g., a single physical location with a fast LAN). Sites are used to control replication traffic and service requests.
-   **SYSVOL Folder**: A shared folder on every DC that stores a copy of public files, such as Group Policy information and logon scripts. This folder is replicated to all DCs in the domain.

### Disaster Recovery

-   **DSRM (Directory Services Restore Mode)**: A safe mode for Windows Server DCs that allows an administrator to repair or restore the Active Directory database.

## 2. User and Group Management

Managed through the **Active Directory Users and Computers** console (`dsa.msc`).

### User Accounts

-   Represents a person who can log in to the domain.
-   Each user account has a unique **Security Identifier (SID)**.
-   Can be configured with logon hours, password policies, and other security settings.

### Groups

Groups simplify administration by allowing you to assign permissions to a group of users rather than to individual users.

#### Group Types

-   **Security Groups**: Used to assign permissions to resources. Can also be used as an email distribution list.
-   **Distribution Groups**: Used only for email distribution lists. Cannot be used to assign permissions.

#### Group Scopes

-   **Domain Local**: Can contain users and groups from any domain in the forest. Can only be used to assign permissions to resources *within its own domain*.
-   **Global**: Can only contain users and groups *from its own domain*. Can be used to assign permissions to resources in any domain in the forest.
-   **Universal**: Can contain users and groups from any domain in the forest. Can be used to assign permissions to resources in any domain in the forest. Requires a Global Catalog server.

**Best Practice (AGDLP)**: **A**ccounts go into **G**lobal groups, which go into **D**omain **L**ocal groups, which are assigned **P**ermissions.

## 3. Trust Relationships

A trust is a relationship between two domains that allows users in one domain to be authenticated by a domain controller in the other domain.

-   **One-Way Trust**: `Domain A -> Domain B`. Users in Domain B can access resources in Domain A.
-   **Two-Way Trust**: `Domain A <-> Domain B`. Users in both domains can access resources in each other's domain.
-   **Transitive Trust**: If Domain A trusts Domain B, and Domain B trusts Domain C, then Domain A trusts Domain C.
-   **Forest Trust**: All domains within a forest automatically have a two-way, transitive trust with each other.

## 4. Active Directory Protocols

-   **LDAP (Lightweight Directory Access Protocol)**:
    -   **Port**: 389 (TCP/UDP)
    -   An application protocol for querying and modifying data in directory services like Active Directory.
-   **Kerberos**:
    -   **Port**: 88 (TCP/UDP)
    -   The default authentication protocol for Windows domain environments. It uses tickets to authenticate users and services without sending passwords over the network.

## 5. Other Key Server Roles

While AD DS is central, other roles are common in a Windows environment:

-   **IIS (Internet Information Services)**:
    -   Microsoft's web server, used to host websites and web applications.
-   **SQL Server**:
    -   A relational database management system used to store and retrieve data for applications. It's a separate product that integrates with Windows Server.
-   **Exchange Server**:
    -   A mail and calendaring server. It relies heavily on Active Directory for its user directory. It's also a separate product.

## 6. Flexible Single Master Operations (FSMO) Roles

FSMO roles (pronounced "fiz-mo") are specialized domain controller tasks that ensure consistency and prevent conflicts in Active Directory. These roles are critical for the proper functioning of a multi-domain controller environment.

### FSMO Roles Breakdown

There are five FSMO roles, divided into two categories:

**Per-Forest Roles (Unique in the entire forest):**

1.  **Schema Master**:
    *   **Function**: Controls all updates and modifications to the Active Directory schema (the definition of all objects and attributes that can be created in AD).
    *   **Importance**: Only one Schema Master exists per forest. Any schema change (e.g., extending the schema for Exchange Server) must be performed on this DC.

2.  **Domain Naming Master**:
    *   **Function**: Controls the addition or removal of domains and application partitions in the forest.
    *   **Importance**: Ensures that domain names are unique within the forest.

**Per-Domain Roles (Unique within each domain):**

3.  **PDC Emulator (Primary Domain Controller Emulator)**:
    *   **Function**: Acts as the primary time source for the domain, processes password changes, manages account lockouts, and is the target for Group Policy updates. In older networks, it also emulates the PDC role for down-level clients (NT4).
    *   **Importance**: Critical for password consistency, time synchronization, and Group Policy application.

4.  **RID Master (Relative ID Master)**:
    *   **Function**: Allocates blocks of unique Relative IDs (RIDs) to each Domain Controller in the domain. RIDs are used to create unique Security Identifiers (SIDs) for new objects (users, groups, computers).
    *   **Importance**: Prevents the creation of duplicate SIDs within the domain.

5.  **Infrastructure Master**:
    *   **Function**: Updates object SIDs and distinguished names in cross-domain object references (e.g., when a user from one domain is added to a group in another domain).
    *   **Importance**: Ensures cross-domain object consistency. To function correctly, the Infrastructure Master should *not* be a Global Catalog server, unless all DCs in the domain are Global Catalog servers.

### Practical: Viewing FSMO Role Holders

You can identify which domain controllers hold the FSMO roles using various tools.

#### 1. Using `netdom query fsmo` (Command Prompt)

This is the quickest way to see all five roles.

```bash
netdom query fsmo
```

#### 2. Using Active Directory Users and Computers (GUI)

*   **PDC Emulator, RID Master, Infrastructure Master (Per-Domain Roles):**
    1.  Open **Active Directory Users and Computers**.
    2.  Right-click on the domain name (e.g., `mycompany.com`).
    3.  Select **Operations Masters...**
    4.  You will see three tabs: **PDC**, **RID**, and **Infrastructure**, each showing the respective role holder.

#### 3. Using Active Directory Domains and Trusts (GUI)

*   **Domain Naming Master (Per-Forest Role):**
    1.  Open **Active Directory Domains and Trusts**.
    2.  Right-click on **Active Directory Domains and Trusts** in the left pane.
    3.  Select **Operations Master...**
    4.  The dialog box will show the **Domain Naming Master**.

#### 4. Using Active Directory Schema (GUI)

*   **Schema Master (Per-Forest Role):**
    1.  Register the Schema snap-in: `regsvr32 schmmgmt.dll` (run from an elevated Command Prompt).
    2.  Open **mmc.exe** (Microsoft Management Console).
    3.  Go to **File > Add/Remove Snap-in...**
    4.  Add **Active Directory Schema** and click **OK**.
    5.  Right-click on **Active Directory Schema** in the console tree.
    6.  Select **Operations Master...**
    7.  The dialog box will show the **Schema Master**.

### Practical: Transferring FSMO Roles

Transferring FSMO roles is typically done when gracefully demoting a DC that holds roles, or when moving roles to a more powerful or stable DC.

#### 1. Using `ntdsutil` (Command Prompt)

This is the most common and robust method.

```bash
# Open an elevated Command Prompt
ntdsutil
roles
connections
connect to server <NameOfTargetDC>
quit
transfer <role>
# Example: transfer schema master
# Example: transfer domain naming master
# Example: transfer rid master
# Example: transfer pdc
# Example: transfer infrastructure master
quit
quit
```

*   **`<NameOfTargetDC>`**: The name of the domain controller to which you want to transfer the role.
*   **`<role>`**: Can be `schema master`, `domain naming master`, `rid master`, `pdc`, or `infrastructure master`.

#### 2. Using Active Directory Users and Computers (GUI)

*   **PDC Emulator, RID Master, Infrastructure Master:**
    1.  Open **Active Directory Users and Computers**.
    2.  Right-click on the domain name, select **Operations Masters...**.
    3.  In the respective tabs (PDC, RID, Infrastructure), click the **Change** button.

#### 3. Using Active Directory Domains and Trusts (GUI)

*   **Domain Naming Master:**
    1.  Open **Active Directory Domains and Trusts**.
    2.  Right-click on **Active Directory Domains and Trusts** in the left pane, select **Operations Master...**.
    3.  Click the **Change** button.

#### 4. Using Active Directory Schema (GUI)

*   **Schema Master:**
    1.  Ensure the Schema snap-in is registered and opened in MMC (as described above).
    2.  Right-click on **Active Directory Schema**, select **Operations Master...**.
    3.  Click the **Change** button.

### Practical: Seizing FSMO Roles

Seizing FSMO roles is a disaster recovery operation, performed when the current FSMO role holder has failed catastrophically and cannot be brought back online. **Only seize roles as a last resort, as it can lead to inconsistencies if the original role holder later comes back online.**

#### 1. Using `ntdsutil` (Command Prompt)

```bash
# Open an elevated Command Prompt
ntdsutil
roles
connections
connect to server <NameOfHealthyDC_ToSeizeRolesTo>
quit
seize <role>
# Example: seize schema master
# Example: seize domain naming master
# Example: seize rid master
# Example: seize pdc
# Example: seize infrastructure master
quit
quit
```

*   **`<NameOfHealthyDC_ToSeizeRolesTo>`**: The name of a healthy domain controller to which you want to seize the role.
*   **`<role>`**: Can be `schema master`, `domain naming master`, `rid master`, `pdc`, or `infrastructure master`.