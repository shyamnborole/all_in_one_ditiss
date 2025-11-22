# Network Defense and Countermeasures - Answers (1-15)

1. **What is the use of a firewall and how it can be implemented?**
   - **Purpose:** Controls incoming and outgoing network traffic based on security rules
   - **Uses:**
     - Block unauthorized access to internal networks
     - Prevent malware and cyber attacks
     - Control network traffic based on policies
     - Log network activity for auditing
   - **Implementation Methods:**
     - Hardware appliances (Cisco ASA, Palo Alto)
     - Software firewalls (Windows Firewall, iptables)
     - Cloud-based firewalls (AWS Security Groups, Azure Firewall)
     - Next-Generation Firewalls (NGFW) with deep packet inspection

2. **What is a packet filter firewall?**
   - **Definition:** First generation firewall that examines packet headers
   - **Operation:**
     - Filters based on source/destination IP addresses
     - Examines source/destination port numbers
     - Uses protocol types (TCP, UDP, ICMP)
   - **Characteristics:**
     - Stateless (no session tracking)
     - Fast processing but limited security
     - Operates at Network and Transport layers

3. **What is a proxy firewall? What are the advantages of using proxy firewall?**
   - **Definition:** Acts as intermediary between clients and servers
   - **Advantages:**
     - Hides internal network structure
     - Provides content filtering
     - Caches content for performance
     - Detailed logging capabilities
     - Protocol-specific security checks
   - **Operation:** Terminates and re-establishes connections

4. **What is a stateful packet inspection firewall?**
   - **Definition:** Tracks state of network connections
   - **Features:**
     - Maintains state table of active connections
     - Makes decisions based on connection state
     - Can distinguish legitimate packets for established connections
     - More secure than packet filtering
     - Operates at multiple OSI layers

5. **Why SSL man in the middle is required for proxy firewalls?**
   - **Purpose:** To inspect encrypted HTTPS traffic
   - **Requirements:**
     - Prevents malware hiding in encrypted traffic
     - Enforces content filtering on HTTPS
     - Provides DLP (Data Loss Prevention)
   - **Implementation:**
     - Firewall acts as Certificate Authority
     - Generates certificates for inspected sites
     - Decrypts, inspects, then re-encrypts traffic

6. **What are the basic differences between iptables and firewalls? What are the tables used in iptables? Explain in short.**
   - **iptables vs Firewalls:**
     - iptables is Linux kernel-level packet filtering
     - Traditional firewalls are dedicated hardware/software
     - iptables provides more granular control
   - **iptables Tables:**
     - **filter:** Default table for packet filtering
     - **nat:** Network Address Translation
     - **mangle:** Special packet alteration
     - **raw:** Connection tracking exemption

7. **What is time based ACL in Squid?**
   - **Definition:** Access control based on time periods in Squid proxy
   - **Implementation:**
     - Restricts access during specific hours/days
     - Uses time specifications (S for Sunday, M for Monday, etc.)
     - Example: `acl workhours time MTWHF 09:00-17:00`
   - **Use Cases:** Bandwidth management, productivity control

8. **What are the types of IDS/IPS? What is false positive and false negative in IDS/IPS?**
   - **IDS/IPS Types:**
     - **Network-based (NIDS/NIPS):** Monitors network traffic
     - **Host-based (HIDS/HIPS):** Monitors individual systems
     - **Signature-based:** Matches known attack patterns
     - **Anomaly-based:** Detects deviations from normal behavior
   - **False Positive:** Legitimate activity flagged as malicious
   - **False Negative:** Malicious activity not detected

9. **What is snort rule format? Give an example.**
   - **Rule Format:** `action protocol source_ip source_port -> dest_ip dest_port (options)`
   - **Example Rule:**
     ```
     alert tcp any any -> 192.168.1.0/24 80 (msg:"Web Attack Attempt"; content:"/etc/passwd"; sid:1000001;)
     ```
   - **Components:**
     - Action: alert, log, pass, drop
     - Protocol: TCP, UDP, ICMP
     - Source/Destination with IP and port
     - Options: message, content match, classification

10. **What is the use of VPN? What is site to site VPN and Dial up VPN?**
    - **VPN Purpose:** Creates secure encrypted tunnels over public networks
    - **Site-to-Site VPN:**
      - Connects entire networks together
      - Used for branch office connectivity
      - Router-to-router configuration
    - **Dial-up VPN (Remote Access VPN):**
      - Individual users connecting to corporate network
      - Client-to-gateway configuration
      - Uses SSL/TLS or IPsec

11. **What is IPSec? What is Encapsulating Security Payload in IPSec? What is Authentication Header in IPSec?**
    - **IPSec:** Protocol suite for securing IP communications
    - **ESP (Encapsulating Security Payload):**
      - Provides confidentiality, integrity, authentication
      - Encrypts packet payload
      - Supports encryption algorithms (AES, 3DES)
    - **AH (Authentication Header):**
      - Provides integrity and authentication only
      - No encryption capability
      - Protects against replay attacks

12. **What is IKE protocol/Framework?**
    - **IKE (Internet Key Exchange):** Protocol for establishing security associations in IPsec
    - **Functions:**
      - Authenticates VPN peers
      - Negotiates encryption algorithms
      - Establishes shared secret keys
      - Manages security associations
    - **Phases:**
      - Phase 1: Establishes secure channel
      - Phase 2: Establishes IPsec tunnel

13. **What is difference between forward and reverse proxy? What are uses of reverse proxy? Which reverse proxy you have configured?**
    - **Forward Proxy:**
      - Client-side proxy
      - Hides client identities from servers
      - Content filtering, caching
    - **Reverse Proxy:**
      - Server-side proxy
      - Hides server infrastructure from clients
      - Load balancing, SSL termination, caching
    - **Configured:** Nginx, Apache, HAProxy

14. **What is phishing and how it can be prevented?**
    - **Phishing:** Social engineering attack to steal sensitive information
    - **Prevention Methods:**
      - User education and awareness training
      - Email filtering and anti-spam solutions
      - Multi-factor authentication
      - URL filtering and web protection
      - Regular security updates
      - Suspicious email reporting procedures

15. **How do you defend wireless access point/router at your home?**
    - **Security Measures:**
      - Change default admin credentials
      - Use WPA3 or WPA2 encryption
      - Disable WPS (Wi-Fi Protected Setup)
      - Enable MAC address filtering
      - Change default SSID and disable broadcasting
      - Keep firmware updated
      - Use strong, unique passwords
      - Enable firewall and disable remote administration
      - Create guest network for visitors
