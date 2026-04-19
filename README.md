<div align="center">

<img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" width="120" alt="AWS" />

<h1>Cyberarians Secure Cloud Infrastructure</h1>

<p>Production-grade AWS deployment — WordPress · RDS · SSM Zero-Trust Access · Custom Domain</p>

<br/>

<p>
  <img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=FF9900" />
  <img src="https://img.shields.io/badge/WordPress-21759B?style=for-the-badge&logo=wordpress&logoColor=white" />
  <img src="https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white" />
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" />
  <img src="https://img.shields.io/badge/Apache-D22128?style=for-the-badge&logo=apache&logoColor=white" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" />
</p>

<p>
  <img src="https://img.shields.io/badge/Status-Live-brightgreen?style=flat-square" />
  <img src="https://img.shields.io/badge/SSL-Enforced-0078D4?style=flat-square&logo=letsencrypt&logoColor=white" />
  <img src="https://img.shields.io/badge/SSH_Port_22-Disabled-critical?style=flat-square" />
  <img src="https://img.shields.io/badge/Access-SSM_Only-FF9900?style=flat-square&logo=amazon-aws&logoColor=white" />
</p>

<br/>

**Live URL:** [http://cyberarians.duckdns.org](http://cyberarians.duckdns.org) &nbsp;|&nbsp; **Team:** Hanzla (22F-3686) & Saad (22F-3654) — FAST NUCES

</div>

---

## Table of Contents

- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Security Posture](#security-posture)
- [AWS Services](#aws-services)
- [Deployment Guide](#deployment-guide)
- [Troubleshooting Log](#troubleshooting-log)
- [Team](#team)

---

## Project Overview

A **production-ready, security-hardened cloud environment** built entirely on AWS, demonstrating enterprise-grade infrastructure patterns:

- Zero-trust server access via **AWS Systems Manager** — SSH port permanently closed
- Encrypted database communication with **enforced SSL/TLS** at the RDS layer
- Network segmentation through a **custom VPC** with public/private subnet isolation
- Managed access governance via **least-privilege IAM role binding**

The stack runs a fully operational **WordPress CMS** served by Apache on EC2, backed by a **managed Amazon RDS MySQL** instance, exposed to the internet via a custom DuckDNS domain.

---

## Architecture

```mermaid
graph TD
    User(["Internet User"]) --> Domain["cyberarians.duckdns.org\nDuckDNS DDNS"]
    Domain --> IGW["Internet Gateway"]
    IGW --> VPC

    subgraph VPC["Custom VPC  10.0.0.0/16"]
        subgraph PublicSubnet["Public Subnet  10.0.1.0/24"]
            EC2["EC2 Web Server\nApache + PHP + WordPress\nAmazon Linux 2"]
        end
        subgraph PrivateSubnet["Private Subnet  10.0.2.0/24"]
            RDS[("Amazon RDS\nMySQL 8.0")]
        end
    end

    SSM["AWS Systems Manager\nCyberarians-SSM-Role"]
    IAM["IAM\nLeast Privilege Policy"]

    SSM -.->|"Secure Session Tunnel\nPort 22 CLOSED"| EC2
    EC2 -->|"Enforced SSL/TLS\nMYSQLI_CLIENT_SSL"| RDS
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

## Security Posture

| Layer | Feature | Implementation |
|-------|---------|----------------|
| ![](https://img.shields.io/badge/Access_Control-232F3E?style=flat-square&logo=amazon-aws&logoColor=FF9900) | Zero-Trust Server Access | AWS SSM Session Manager — Port 22 permanently closed |
| ![](https://img.shields.io/badge/Data_in_Transit-232F3E?style=flat-square&logo=letsencrypt&logoColor=white) | Encrypted DB Connections | `MYSQLI_CLIENT_SSL` enforced at application layer |
| ![](https://img.shields.io/badge/Network-232F3E?style=flat-square&logo=amazonvpc&logoColor=white) | Subnet Isolation | RDS in private subnet — unreachable from the public internet |
| ![](https://img.shields.io/badge/Firewall-232F3E?style=flat-square&logo=amazonaws&logoColor=white) | Multi-Layer Security Groups | Only EC2 security group permitted to reach RDS on port 3306 |
| ![](https://img.shields.io/badge/IAM-232F3E?style=flat-square&logo=amazon-aws&logoColor=FF9900) | Least-Privilege Role | `Cyberarians-SSM-Role` scoped to `AmazonSSMManagedInstanceCore` only |
| ![](https://img.shields.io/badge/Credentials-232F3E?style=flat-square&logo=amazonaws&logoColor=white) | No Hardcoded Keys | All AWS access via IAM instance profile — no access key pairs |

---

## AWS Services

<div align="center">

<table>
  <tr>
    <td align="center">
      <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" width="52" /><br/>
      <b>EC2</b><br/><sub>Web server host</sub>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" width="52" /><br/>
      <b>VPC</b><br/><sub>Network isolation</sub>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" width="52" /><br/>
      <b>RDS MySQL</b><br/><sub>Managed database</sub>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" width="52" /><br/>
      <b>SSM</b><br/><sub>Zero-trust access</sub>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/apache/apache-original-wordmark.svg" width="52" /><br/>
      <b>Apache</b><br/><sub>HTTP server</sub>
    </td>
    <td align="center">
      <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/php/php-original.svg" width="52" /><br/>
      <b>PHP</b><br/><sub>Runtime</sub>
    </td>
  </tr>
</table>

</div>

---

## Deployment Guide

### 1. Environment Provisioning

Provision an **Amazon Linux 2** EC2 instance, attach the `Cyberarians-SSM-Role` IAM role before launch, then connect via **Systems Manager > Session Manager** — no key pair required.

```bash
# Update system and install full LAMP stack
sudo yum update -y
sudo yum install -y httpd wget php mariadb105 php-mysqlnd

# Start Apache and enable on boot
sudo systemctl start httpd
sudo systemctl enable httpd

# Confirm SSM Agent is running (pre-installed on Amazon Linux 2)
sudo systemctl status amazon-ssm-agent
```

---

### 2. WordPress Core Installation

```bash
# Download and extract WordPress into web root
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzvf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz

# Transfer ownership to Apache process user
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html
```

---

### 3. Database Security Integration

> **Critical:** The RDS parameter group has `require_secure_transport = ON`. Any plain TCP connection is rejected with `ERROR 3159`. The fix is one constant in `wp-config.php`.

```bash
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
```

```php
define( 'DB_NAME',     'wordpress' );
define( 'DB_USER',     'admin' );
define( 'DB_PASSWORD', 'Your_Secure_Password_Here' );
define( 'DB_HOST',     'cyberarians-db.ce50igc46iwv.us-east-1.rds.amazonaws.com' );
define( 'DB_CHARSET',  'utf8mb4' );

/**
 * Force SSL transport for all RDS connections.
 * Fixes: "Connections using insecure transport are prohibited (ERROR 3159)"
 * Required: RDS parameter group enforces require_secure_transport = ON
 */
define( 'MYSQL_CLIENT_FLAGS', MYSQLI_CLIENT_SSL );
```

---

### 4. Domain Mapping via DuckDNS

```bash
# Auto-update DuckDNS with EC2 public IP every 5 minutes
echo "*/5 * * * * curl -s 'https://www.duckdns.org/update?domains=cyberarians&token=YOUR_TOKEN&ip=' > /dev/null" | crontab -

# Verify DNS resolution
nslookup cyberarians.duckdns.org
```

---

## Troubleshooting Log

### Issue 1 — `ERROR 3159: Connections using insecure transport are prohibited`

| Field | Detail |
|-------|--------|
| **Root Cause** | RDS parameter group has `require_secure_transport = ON`, silently dropping non-SSL connections |
| **Discovery** | Error surfaced during WordPress database setup via the `wp-admin` install wizard |
| **Resolution** | Added `define('MYSQL_CLIENT_FLAGS', MYSQLI_CLIENT_SSL)` to `wp-config.php` |
| **Lesson** | RDS Secure Transport is a per-parameter-group setting — audit it before any application provisioning |

---

### Issue 2 — SSM Agent Offline in Console

| Field | Detail |
|-------|--------|
| **Root Cause** | Stale credential cache in SSM Agent after IAM role was reassigned to the instance |
| **Discovery** | Session Manager showed instance as "offline" despite EC2 running normally |
| **Resolution** | `sudo systemctl restart amazon-ssm-agent` |
| **Lesson** | IAM role changes on a live instance require an agent restart to pick up new credentials |

---

### Issue 3 — `403 Forbidden` on WordPress Root

| Field | Detail |
|-------|--------|
| **Root Cause** | Web files owned by `root`, not the `apache` process user |
| **Resolution** | `sudo chown -R apache:apache /var/www/html` |

---

## Team

<div align="center">

<table>
  <tr>
    <th>Developer</th>
    <th>Roll Number</th>
    <th>Contributions</th>
  </tr>
  <tr>
    <td><a href="https://github.com/Hanzlase"><img src="https://img.shields.io/badge/Hanzla-181717?style=flat-square&logo=github&logoColor=white" /></a></td>
    <td>22F-3686</td>
    <td>Infrastructure provisioning, SSM configuration, RDS SSL security</td>
  </tr>
  <tr>
    <td><img src="https://img.shields.io/badge/Saad-181717?style=flat-square&logo=github&logoColor=white" /></td>
    <td>22F-3654</td>
    <td>WordPress setup, VPC networking, domain mapping</td>
  </tr>
</table>

<br/>

<img src="https://img.shields.io/badge/FAST_NUCES-Software_Engineering-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=FF9900" />

</div>
