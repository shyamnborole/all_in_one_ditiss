# 02: Network Configuration and Services

Proper network configuration is critical for a functioning Windows environment. This section covers the core network services: IP addressing, DHCP, and DNS.

## 1. IP Addressing (IPv4 and IPv6)

-   **IPv4 (Internet Protocol version 4)**:
    -   A 32-bit address, written as four octets (e.g., `192.168.1.1`).
    -   The theoretical maximum is ~4.3 billion addresses.
    -   Uses a **subnet mask** (e.g., `255.255.255.0`) to define the network and host portions of the address.
-   **IPv6 (Internet Protocol version 6)**:
    -   A 128-bit address, written as eight groups of four hexadecimal digits (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).
    -   Offers a vastly larger address space.
    -   Uses a **prefix length** (e.g., `/64`) to define the network portion.
    -   **Link-Local Addresses**: Start with `fe80::` and are used for communication within a single network segment (not routable).

## 2. DHCP (Dynamic Host Configuration Protocol)

DHCP automates the assignment of IP addresses and other network configuration settings to clients.

-   **Port**: Operates on UDP ports 67 (server) and 68 (client).
-   **Role**:
    -   Prevents IP address conflicts.
    -   Simplifies network administration.
    -   Provides clients with an IP address, subnet mask, default gateway, and DNS server addresses.

### DORA Process

The DHCP process consists of four steps, known as **DORA**:

1.  **Discover**: The client broadcasts a `DHCPDISCOVER` message to find a DHCP server on the network.
2.  **Offer**: DHCP servers on the network respond with a `DHCPOFFER` message, offering an available IP address.
3.  **Request**: The client accepts one of the offers and broadcasts a `DHCPREQUEST` message, requesting the offered IP address.
4.  **Acknowledge**: The DHCP server that made the offer sends a `DHCPACK` message, confirming the IP address lease.

## 3. DNS (Domain Name System)

DNS translates human-readable domain names (e.g., `www.google.com`) into machine-readable IP addresses.

-   **Port**: Operates on Port 53 (UDP for queries, TCP for zone transfers).
-   **Hierarchy**: DNS is a hierarchical system, starting from the **Root Servers**, then **Top-Level Domain (TLD) Servers** (`.com`, `.org`), and finally **Authoritative Servers** for specific domains.

### DNS Zones

-   **Forward Lookup Zone**: Maps a hostname to an IP address (e.g., `server1.example.com` -> `192.168.1.10`).
-   **Reverse Lookup Zone**: Maps an IP address to a hostname (e.g., `192.168.1.10` -> `server1.example.com`).

### DNS Zone Types

-   **Primary Zone**: The main read-write copy of the zone data. All changes are made here.
-   **Secondary Zone**: A read-only copy of a primary zone, hosted on a different DNS server. It provides redundancy and load balancing. Zone data is replicated from the primary server.
-   **Stub Zone**: A read-only copy that contains only the records needed to identify the authoritative DNS servers for a master zone (NS, SOA, and glue A records). Used to improve name resolution performance.

### Common DNS Record Types

| Record | Name                   | Purpose                                                     |
| ------ | ---------------------- | ----------------------------------------------------------- |
| **A**  | Address                | Maps a hostname to an IPv4 address.                         |
| **AAAA** | Quad A                 | Maps a hostname to an IPv6 address.                         |
| **PTR**| Pointer                | Used in reverse lookups to map an IP address to a hostname. |
| **CNAME**| Canonical Name         | An alias, mapping one name to another (e.g., `ftp.example.com` to `server1.example.com`). |
| **MX** | Mail Exchanger         | Specifies the mail server for a domain.                     |
| **SRV**| Service                | Identifies the location (hostname and port) of a service.   |
| **NS** | Name Server            | Specifies the authoritative DNS servers for a zone.         |
| **SOA**| Start of Authority     | Contains administrative information about the zone.         |

### Useful DNS Commands (Windows)

-   `nslookup`: Query DNS for record information.
-   `ipconfig /displaydns`: View the local DNS resolver cache.
-   `ipconfig /flushdns`: Clear the local DNS resolver cache.

## 4. Network Policy Server (NPS)

-   **Purpose**: NPS is Microsoft's implementation of a RADIUS (Remote Authentication Dial-In User Service) server.
-   **Function**: It provides centralized authentication, authorization, and accounting (AAA) for network access.
-   **Use Cases**:
    -   **802.1x Wireless and Wired Connections**: Authenticate users and devices connecting to the network via Wi-Fi or Ethernet switches.
    -   **VPN Connections**: Enforce policies for remote access VPN connections.

## 5. Network Load Balancing (NLB)

-   **Purpose**: A Windows Server feature that distributes network traffic across multiple servers in a cluster.
-   **How it Works**: All servers in the NLB cluster share a single virtual IP address. NLB intercepts incoming traffic and distributes it to the individual servers based on a configured algorithm.
-   **Use Cases**:
    -   Providing high availability and scalability for stateless applications like web servers (IIS).
-   **Note**: NLB is not suitable for stateful applications like database servers, as each client request could be sent to a different server.
