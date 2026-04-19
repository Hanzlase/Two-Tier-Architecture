<div align="center">
<img src="https://www.google.com/search?q=https://upload.wikimedia.org/wikipedia/commons/9/93/Amazon_Web_Services_Logo.svg" width="100" alt="AWS Logo">
<h1>Cyberarians Secure Cloud Infrastructure</h1>
<p><strong>Advanced AWS Deployment: WordPress + RDS + SSM + Domain Mapping</strong></p>

<p>
<img src="https://www.google.com/search?q=https://img.shields.io/badge/AWS-232F3E%3Fstyle%3Dfor-the-badge%26logo%3Damazon-aws%26logoColor%3Dwhite" alt="AWS">
<img src="https://www.google.com/search?q=https://img.shields.io/badge/WordPress-21759B%3Fstyle%3Dfor-the-badge%26logo%3Dwordpress%26logoColor%3Dwhite" alt="WordPress">
<img src="https://www.google.com/search?q=https://img.shields.io/badge/PHP-777BB4%3Fstyle%3Dfor-the-badge%26logo%3Dphp%26logoColor%3Dwhite" alt="PHP">
<img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux">
</p>
</div>

<hr />

🏛️ Project Overview

This project showcases a production-ready cloud environment built on AWS. It features a hardened EC2 web server, a managed RDS database backend with enforced SSL encryption, and zero-trust access management via AWS Systems Manager.

Live URL: http://cyberarians.duckdns.org

Developers: Hanzla & Saad (FAST NUCES)

🏗️ Architecture Diagram

graph TD
    User([Internet User]) --> Domain[cyberarians.duckdns.org]
    Domain --> IGW[Internet Gateway]
    IGW --> VPC[Custom VPC]
    subgraph VPC
        subgraph PublicSubnet[Public Subnet]
            EC2[EC2 Web Server: Apache/PHP]
        end
        subgraph PrivateSubnet[Database Layer]
            RDS[(Amazon RDS: MySQL)]
        end
    end
    SSM[AWS Systems Manager] -.->|Secure Tunnel| EC2
    EC2 -->|Enforced SSL| RDS


🔒 Security Posture

Feature

Implementation

Access Control

Zero-trust via AWS Systems Manager (SSM). No SSH Port 22 required.

Data in Transit

Application-level enforcement of SSL/TLS for DB connections.

Network Security

Multi-layered Security Groups isolating the DB from the public web.

IAM Governance

Cyberarians-SSM-Role providing least-privilege managed access.

💻 Deployment Documentation

1. Environment Provisioning

# Update and install LAMP stack
sudo yum update -y
sudo yum install -y httpd wget php mariadb105 php-mysqlnd

# Service Management
sudo systemctl start httpd
sudo systemctl enable httpd


2. WordPress Core Installation

cd /var/www/html
sudo wget [https://wordpress.org/latest.tar.gz](https://wordpress.org/latest.tar.gz)
sudo tar -xzvf latest.tar.gz
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
sudo chown -R apache:apache /var/www/html


3. Database Security Integration

Crucial configuration inside wp-config.php to handle RDS Secure Transport requirements:

define( 'DB_NAME', 'wordpress' );
define( 'DB_USER', 'admin' );
define( 'DB_PASSWORD', 'Your_Password' );
define( 'DB_HOST', 'cyberarians-db.ce50igc46iwv.us-east-1.rds.amazonaws.com' );

/* Force SSL Connection - Fixes ERROR 3159 */
define( 'MYSQL_CLIENT_FLAGS', MYSQLI_CLIENT_SSL );


🛠️ Critical Troubleshooting Logs

Issue: Connections using insecure transport are prohibited.

Solution: Identified that RDS parameter group had require_secure_transport enabled. Resolved by injecting MYSQLI_CLIENT_SSL flags into the WordPress core configuration.

Issue: SSM Agent Offline.

Solution: Re-initiated agent credentials by restarting the service: sudo systemctl restart amazon-ssm-agent.

<div align="center">
<p>Final Semester Project - Software Engineering Department</p>
<p><strong>FAST National University of Computer and Emerging Sciences</strong></p>
</div>
