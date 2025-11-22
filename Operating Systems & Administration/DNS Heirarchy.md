# 🌐 DNS Hierarchy Workflow: How Domain Names Become IP Addresses

The Domain Name System (DNS) hierarchy workflow describes the steps a DNS Resolver takes to find the IP address corresponding to a domain name (e.g., `example.com`). This process involves a collaboration between four main types of servers.

---

## 1. The Local Request (The Start) 🖥️

| Step | Action | Description |
| :--- | :--- | :--- |
| **Initial Check** | User types a URL. | The operating system first checks its local **cache** and **hosts file** for the IP address. |
| **Request Sent** | Request to Resolver. | If the IP is not found locally, the request is sent to the configured **DNS Resolver** (usually your ISP's server or a public one). |

---

## 2. Iterative Query Process 🔁

The DNS Resolver now performs a series of **iterative queries** down the DNS hierarchy until it finds the final IP address.

### A. Root Server Query 🌳

1.  **Resolver Asks:** The DNS Resolver sends a query for the full domain name to one of the **Root Name Servers** (there are 13 logical sets worldwide).
2.  **Root Responds:** The Root Server does not know the IP address, but it directs the Resolver to the server responsible for the **Top-Level Domain (TLD)**, like `.com`, `.org`, or `.net`.
3.  **Result:** Address of the **TLD Name Server**.

### B. TLD Server Query 🏷️

1.  **Resolver Asks:** The Resolver sends the query to the specified **TLD Name Server** (e.g., the server handling all `.com` domains).
2.  **TLD Responds:** The TLD Server doesn't know the final IP address, but it knows the authoritative server for the specific domain name (e.g., `google.com`).
3.  **Result:** Address of the **Authoritative Name Server**.

### C. Authoritative Server Query 🏛️

1.  **Resolver Asks:** The Resolver sends the query to the **Authoritative Name Server** (the server managed by the domain owner).
2.  **Authoritative Responds:** This server holds the actual **DNS records** (A record, CNAME, etc.) and is the final source for the IP address.
3.  **Result:** The correct **IP Address** for the requested hostname.

---

## 3. Final Resolution and Caching 💾

1.  **Response to Client:** The DNS Resolver sends the final IP address back to the user's computer.
2.  **Connection:** The computer uses this IP address to open a connection to the website's server.
3.  **Caching:** The Resolver also stores this mapping (Domain $\rightarrow$ IP) in its **cache** for the specified **Time-To-Live (TTL)**. Subsequent requests for the same domain will be answered immediately from the cache, skipping the hierarchy.

---

## 🔑 Key Components and Hierarchy

| Component                | Function in the Hierarchy                                                                      | Example                       |
| :----------------------- | :--------------------------------------------------------------------------------------------- | :---------------------------- |
| **Resolver**             | Initiates the query and performs the iterative search.                                         | ISP DNS server ($8.8.8.8$)    |
| **Root Server**          | The top of the hierarchy; directs traffic to the correct TLD server.                           | The **.** (dot) in the domain |
| **TLD Server**           | Manages all domains under a specific TLD; directs traffic to the correct Authoritative server. | `.com`, `.org`, `.net`        |
| **Authoritative Server** | Holds the definitive DNS records and IP addresses for a specific domain.                       | Server for `google.com`       |