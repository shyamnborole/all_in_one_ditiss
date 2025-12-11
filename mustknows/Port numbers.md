Here's a comprehensive guide to essential port numbers for cybersecurity:

## 🌐 **Common Port Numbers Every Cybersecurity Professional Should Know**

### **Top 20 Most Essential Ports**

| Port        | Protocol | Service | Purpose                        | Security Notes                                                   |
| ----------- | -------- | ------- | ------------------------------ | ---------------------------------------------------------------- |
| **20/21**   | TCP      | FTP     | File Transfer                  | Unencrypted, avoid if possible( User Authentication is Required) |
| **22**      | TCP      | SSH     | Secure Shell                   | Encrypted remote access                                          |
| **23**      | TCP      | Telnet  | Remote Login                   | **Insecure** - no encryption                                     |
| **25**      | TCP      | SMTP    | Email Sending                  | Mail transfer between servers                                    |
| **53**      | TCP/UDP  | DNS     | Domain Name System             | Converts names to IP addresses                                   |
| **67/68**   | UDP      | DHCP    | Dynamic Host Config            | IP address assignment                                            |
| **80**      | TCP      | HTTP    | Web Traffic                    | **Unencrypted** web browsing                                     |
| **110**     | TCP      | POP3    | Email Retrieval                | Receive email from server                                        |
| **123**     | UDP      | NTP     | Network Time Protocol          | Time synchronization                                             |
| **3306**    | TCP      | MySQL   | MySQL Database                 | Popular database                                                 |
| **139**     | TCP      | NetBIOS | File/Printer Sharing           | Windows network services                                         |
| **143**     | TCP      | IMAP    | Email Access                   | More advanced than POP3                                          |
| **161/162** | UDP      | SNMP    | Network Management             | Device monitoring                                                |
| **443**     | TCP      | HTTPS   | Secure Web Traffic             | **Encrypted** web browsing                                       |
| **445**     | TCP      | SMB     | File Sharing                   | Windows file sharing                                             |
| **993**     | TCP      | IMAPS   | Secure IMAP                    | IMAP over SSL/TLS                                                |
| **135**     | TCP      | RPC     | Remote Procedure Call          | Windows services                                                 |
| **995**     | TCP      | POP3S   | Secure POP3                    | POP3 over SSL/TLS                                                |
| **1433**    | TCP      | MSSQL   | Microsoft SQL Server           | Database service                                                 |
| **3389**    | TCP      | RDP     | Remote Desktop                 | Windows remote access                                            |
| 69          | UDP      | TFTP    | Trivial File Transfer Protocol | Unencrypted, Unreliable, Simple, No User Authentication          |
|             |          |         |                                |                                                                  |

## 🛡️ **Port Categories for Security Analysis**

### **Common Attack Vectors (High Risk)**
- **21 (FTP)**: Credential sniffing, anonymous access
- **22 (SSH)**: Brute force attacks
- **23 (Telnet)**: Credentials transmitted in clear text
- **135-139 (NetBIOS)**: Network enumeration, SMB exploits
- **443 (HTTPS)**: SSL stripping, certificate issues
- **445 (SMB)**: EternalBlue, WannaCry vulnerability
- **3389 (RDP)**: BlueKeep, brute force attacks

### **Database Ports**
- **1433**: Microsoft SQL Server
- **1521**: Oracle Database
- **3306**: MySQL
- **5432**: PostgreSQL
- **27017**: MongoDB

### **Web Service Ports**
- **80**: HTTP
- **443**: HTTPS
- **8080**: HTTP Alternate
- **8443**: HTTPS Alternate
- **8000-8009**: Development web servers

### **Email Service Ports**
- **25**: SMTP (Mail transfer)
- **110**: POP3 (Mail retrieval)
- **143**: IMAP (Mail access)
- **465**: SMTPS (SMTP over SSL)
- **587**: SMTP Submission
- **993**: IMAPS (IMAP over SSL)
- **995**: POP3S (POP3 over SSL)

### **Remote Access Ports**
- **22**: SSH (Secure)
- **23**: Telnet (Insecure)
- **3389**: RDP (Remote Desktop)
- **5900**: VNC (Virtual Network Computing)

## 🔍 **Port Ranges Explained**

### **Well-Known Ports (0-1023)**
- System/services ports
- Require administrator privileges to bind
- Standardized by IANA

### **Registered Ports (1024-49151)**
- Application-specific ports
- Assigned by IANA to organizations
- Don't require admin privileges

### **Dynamic/Private Ports (49152-65535)**
- Ephemeral ports for client connections
- Temporary use for outbound connections

## 🚨 **Common Security Scenarios**

### **Port Scanning with Nmap**
```bash
# Scan common ports
nmap -sS -p 21,22,23,25,53,80,110,443,445,3389 target_ip

# Scan top 1000 ports
nmap -sS target_ip

# Scan all ports (comprehensive)
nmap -sS -p- target_ip

# Service version detection
nmap -sS -sV target_ip
```

### **Checking Local Ports**
```bash
# See what's listening locally
netstat -tuln
ss -tuln

# Check specific port
netstat -tuln | grep :22
ss -tuln | grep :22
```

### **Common Attack Ports to Monitor**
```bash
# Suspicious ports often used by malware
# 4444 - Metasploit default
# 31337 - Back Orifice
# 12345 - NetBus
# 54320 - Back Construction
```

## 📊 **Port Reference Tables**

### **Network Services**
| Port | Service | Risk Level |
|------|---------|------------|
| 53 | DNS | Medium |
| 67/68 | DHCP | Low |
| 161 | SNMP | High (if misconfigured) |

### **File Sharing**
| Port | Service | Risk Level |
|------|---------|------------|
| 21 | FTP | High |
| 2049 | NFS | Medium |
| 139/445 | SMB | High |

### **Database Services**
| Port | Service | Default Credentials Risk |
|------|---------|--------------------------|
| 1433 | MSSQL | High |
| 3306 | MySQL | High |
| 5432 | PostgreSQL | High |

## 🛠️ **Practical Security Commands**

### **Port Monitoring**
```bash
# Real-time port monitoring
watch -n 1 'ss -tuln'

# Find processes using specific port
lsof -i :80
fuser -n tcp 443

# Check if port is open remotely
nc -zv target_ip 22
telnet target_ip 80
```

### **Firewall Examples**
```bash
# iptables examples
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# Block specific port
iptables -A INPUT -p tcp --dport 23 -j DROP
```

## 💡 **Memory Aids**

### **Common Sequences**
- **Web**: 80 (HTTP) → 443 (HTTPS) → 8080 (Alt HTTP)
- **Email**: 25 (SMTP) → 110 (POP3) → 143 (IMAP)
- **Remote**: 22 (SSH) → 23 (Telnet) → 3389 (RDP)
- **Files**: 21 (FTP) → 139/445 (SMB)

### **Key Security Points**
1. **Ports below 1024** require root privileges
2. **Even ports** often used for standard services
3. **High-numbered ports** often used for malware/C2
4. **Always verify** what should be open vs. what is open

This port knowledge is essential for:
- Network scanning and enumeration
- Firewall configuration
- Intrusion detection
- Vulnerability assessment
- Incident response

Would you like me to elaborate on any specific category or show practical examples of port security analysis?