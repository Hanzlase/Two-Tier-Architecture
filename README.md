<div align="center">

<!-- AWS SVG Logo from SimpleIcons -->
<img src="https://cdn.simpleicons.org/amazonaws/FF9900" width="90" alt="AWS Logo" />

<h1>🔐 Cyberarians Secure Cloud Infrastructure</h1>

<p><em>Production-grade AWS deployment featuring WordPress, RDS, SSM Zero-Trust Access & Custom Domain Mapping</em></p>

<br/>

<!-- Tech Badges -->
<p>
  <img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=FF9900" alt="AWS" />
  <img src="https://img.shields.io/badge/WordPress-21759B?style=for-the-badge&logo=wordpress&logoColor=white" alt="WordPress" />
  <img src="https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux" />
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Apache-D22128?style=for-the-badge&logo=apache&logoColor=white" alt="Apache" />
</p>

<!-- Status Badges -->
<p>
  <img src="https://img.shields.io/badge/Status-Live-brightgreen?style=flat-square&logo=statuspage&logoColor=white" alt="Live" />
  <img src="https://img.shields.io/badge/SSL-Enforced-blue?style=flat-square&logo=letsencrypt&logoColor=white" alt="SSL" />
  <img src="https://img.shields.io/badge/SSH-Disabled-red?style=flat-square&logo=gnubash&logoColor=white" alt="No SSH" />
  <img src="https://img.shields.io/badge/Access-SSM%20Only-orange?style=flat-square&logo=amazonaws&logoColor=white" alt="SSM Access" />
</p>

<br/>

> 🌐 **Live Deployment:** [http://cyberarians.duckdns.org](http://cyberarians.duckdns.org)  
> 👨‍💻 **Authors:** Hanzla & Saad — FAST NUCES (22F-3686 & 22F-3654)

</div>

---

## 📑 Table of Contents

- [Project Overview](#-project-overview)
- [Architecture Diagram](#-architecture-diagram)
- [Security Posture](#-security-posture)
- [AWS Services Used](#-aws-services-used)
- [Deployment Documentation](#-deployment-documentation)
- [Critical Troubleshooting Logs](#-critical-troubleshooting-logs)
- [Team](#-team)

---

## 🏛️ Project Overview

This project delivers a **production-ready, security-hardened cloud environment** built entirely on AWS. It demonstrates enterprise-grade infrastructure patterns including:

- **Zero-trust server access** via AWS Systems Manager — no SSH port ever opened
- **Encrypted database communication** with enforced SSL/TLS on the RDS layer
- **Network segmentation** through a custom VPC with public/private subnet isolation
- **Managed IAM governance** using least-privilege role binding

The stack runs a fully functional **WordPress CMS** served by Apache on EC2, backed by a **managed Amazon RDS MySQL** instance — accessible only over the public internet via a custom DuckDNS domain.

---

## 🏗️ Architecture Diagram

```mermaid
graph TD
    User(["🌐 Internet User"]) --> Domain["cyberarians.duckdns.org<br/><small>DuckDNS DDNS</small>"]
    Domain --> IGW["🔀 Internet Gateway"]
    IGW --> VPC

    subgraph VPC["🏠 Custom VPC  ·  10.0.0.0/16"]
        subgraph PublicSubnet["📡 Public Subnet  ·  10.0.1.0/24"]
            EC2["🖥️ EC2 Web Server<br/>Apache + PHP + WordPress<br/><small>Amazon Linux 2</small>"]
        end
        subgraph PrivateSubnet["🔒 Private Subnet  ·  10.0.2.0/24"]
            RDS[("🗄️ Amazon RDS<br/>MySQL 8.0<br/><small>Multi-AZ Ready</small>")]
        end
    end

    SSM["🛡️ AWS Systems Manager<br/><small>Cyberarians-SSM-Role</small>"]
    IAM["🔑 IAM<br/><small>Least Privilege Policy</small>"]

    SSM -.->|"🔐 Secure Session Tunnel<br/><small>Port 22 — CLOSED</small>"| EC2
    EC2 -->|"🔒 Enforced SSL/TLS<br/><small>MYSQLI_CLIENT_SSL</small>"| RDS
    IAM -->|"Policy Binding"| SSM

    style VPC fill:#1a1a2e,stroke:#FF9900,stroke-width:2px,color:#fff
    style PublicSubnet fill:#16213e,stroke:#00d4ff,stroke-width:1px,color:#fff
    style PrivateSubnet fill:#16213e,stroke:#ff4757,stroke-width:1px,color:#fff
    style EC2 fill:#FF9900,stroke:#fff,color:#000
    style RDS fill:#4479A1,stroke:#fff,color:#fff
    style SSM fill:#232F3E,stroke:#FF9900,color:#FF9900
    style IAM fill:#232F3E,stroke:#FF9900,color:#FF9900
```

---

## 🔒 Security Posture

| Layer | Feature | Implementation |
|-------|---------|----------------|
| 🚪 **Access Control** | Zero-Trust Server Access | AWS Systems Manager (SSM) — Port 22 permanently closed |
| 🔐 **Data in Transit** | Encrypted DB Connections | `MYSQLI_CLIENT_SSL` enforced at application layer |
| 🌐 **Network Security** | Subnet Isolation | RDS resides in private subnet — unreachable from internet |
| 🛡️ **Security Groups** | Multi-Layer Firewalling | Only EC2 SG allows DB ingress on port 3306 |
| 👤 **IAM Governance** | Least-Privilege Role | `Cyberarians-SSM-Role` scoped to `AmazonSSMManagedInstanceCore` |
| 🔑 **Credential Management** | No Hardcoded Keys | All AWS access via IAM role, not access key pairs |

---

## ☁️ AWS Services Used

<table>
<tr>
  <td align="center"><img src="https://cdn.simpleicons.org/amazonaws/FF9900" width="32"/><br/><strong>EC2</strong><br/><sub>Web server host</sub></td>
  <td align="center"><img src="https://cdn.simpleicons.org/amazons3/569A31" width="32"/><br/><strong>VPC</strong><br/><sub>Network isolation</sub></td>
  <td align="center"><img src="https://cdn.simpleicons.org/mysql/4479A1" width="32"/><br/><strong>RDS MySQL</strong><br/><sub>Managed database</sub></td>
  <td align="center"><img src="https://cdn.simpleicons.org/amazonaws/FF9900" width="32"/><br/><strong>SSM</strong><br/><sub>Zero-trust access</sub></td>
  <td align="center"><img src="https://cdn.simpleicons.org/amazonaws/FF9900" width="32"/><br/><strong>IAM</strong><br/><sub>Role governance</sub></td>
</tr>
</table>

---

## 💻 Deployment Documentation

### 1. 🖥️ Environment Provisioning

Provision an **Amazon Linux 2** EC2 instance, attach the `Cyberarians-SSM-Role` IAM role, and connect via Systems Manager Session Manager.

```bash
# Update system & install full LAMP stack
sudo yum update -y
sudo yum install -y httpd wget php mariadb105 php-mysqlnd

# Start and enable Apache on boot
sudo systemctl start httpd
sudo systemctl enable httpd

# Verify SSM Agent is running (pre-installed on Amazon Linux 2)
sudo systemctl status amazon-ssm-agent
```

---

### 2. 📦 WordPress Core Installation

```bash
# Navigate to web root and download WordPress
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz

# Extract and flatten directory structure
sudo tar -xzvf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz

# Set Apache as owner of all web files
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html
```

---

### 3. ⚙️ WordPress Configuration

```bash
# Create config from sample
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```

---

### 4. 🔐 Database Security Integration

> ⚠️ **Critical:** The RDS parameter group has `require_secure_transport = ON`. Connections without SSL are rejected with `ERROR 3159`. The fix is a single constant in `wp-config.php`.

```php
<?php
// Database credentials
define( 'DB_NAME',     'wordpress' );
define( 'DB_USER',     'admin' );
define( 'DB_PASSWORD', 'Your_Secure_Password_Here' );
define( 'DB_HOST',     'cyberarians-db.ce50igc46iwv.us-east-1.rds.amazonaws.com' );
define( 'DB_CHARSET',  'utf8mb4' );
define( 'DB_COLLATE',  '' );

/**
 * SECURITY: Force SSL transport for all RDS connections.
 * Resolves: "Connections using insecure transport are prohibited (ERROR 3159)"
 * Required because RDS parameter group enforces require_secure_transport=ON
 */
define( 'MYSQL_CLIENT_FLAGS', MYSQLI_CLIENT_SSL );
```

---

### 5. 🔗 Domain Mapping (DuckDNS)

```bash
# Install and configure DuckDNS auto-update cron job
echo "*/5 * * * * curl -s 'https://www.duckdns.org/update?domains=cyberarians&token=YOUR_TOKEN&ip=' > /dev/null" | crontab -

# Verify EC2 public IP reflects in DNS
nslookup cyberarians.duckdns.org
```

---

## 🛠️ Critical Troubleshooting Logs

### ❌ Issue 1: `ERROR 3159 — Connections using insecure transport are prohibited`

| | Details |
|---|---|
| **Root Cause** | RDS MySQL parameter group has `require_secure_transport = ON`, rejecting plain TCP connections |
| **Discovery** | Error surfaced during WordPress database connection test via `wp-admin` setup wizard |
| **Fix** | Added `define('MYSQL_CLIENT_FLAGS', MYSQLI_CLIENT_SSL)` to `wp-config.php`, forcing `mysqli` to negotiate TLS on connect |
| **Lesson** | RDS Secure Transport is a **per-parameter-group** setting — always check before provisioning WordPress |

---

### ❌ Issue 2: `SSM Agent Offline in Console`

| | Details |
|---|---|
| **Root Cause** | SSM Agent stale credential cache after IAM role reassignment to the instance |
| **Discovery** | Session Manager showed instance as "offline" despite EC2 being fully running |
| **Fix** | `sudo systemctl restart amazon-ssm-agent` — forces re-registration with SSM endpoints |
| **Lesson** | IAM role changes on a running instance require an agent restart to pick up new credentials |

---

### ❌ Issue 3: `403 Forbidden on WordPress Root`

| | Details |
|---|---|
| **Root Cause** | Apache serving files owned by `root`, not `apache` user |
| **Fix** | `sudo chown -R apache:apache /var/www/html` |

---

## 👨‍💻 Team

<div align="center">

| | Developer | Roll No | Contribution |
|---|---|---|---|
| <img src="https://cdn.simpleicons.org/github/white" width="20"/> | **Hanzla** | 22F-3686 | Infrastructure, SSM Config, RDS Security |
| <img src="https://cdn.simpleicons.org/github/white" width="20"/> | **Saad** | 22F-3654 | WordPress Setup, Networking, Domain Mapping |

</div>

---

<div align="center">

<img src="https://cdn.simpleicons.org/amazonaws/FF9900" width="40" alt="AWS" />


<br/>

<img src="https://img.shields.io/badge/Made%20with-❤️%20at%20FAST%20NUCES-FF9900?style=for-the-badge" alt="Made at FAST NUCES" />

</div>
