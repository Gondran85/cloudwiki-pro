# ☁️ CloudWiki Pro

> A lightweight knowledge management platform built with Flask, MySQL, and deployed on AWS infrastructure.

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-2.x-black.svg)](https://flask.palletsprojects.com/)
[![AWS](https://img.shields.io/badge/AWS-EC2%20%7C%20RDS-FF9900.svg)](https://aws.amazon.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📋 Overview

**CloudWiki Pro** is a wiki-style web application where users can register, log in, and contribute articles to a shared knowledge base. The project demonstrates a full-stack deployment on AWS using EC2 for compute and RDS (MySQL) for managed database services.

This project was built as part of my AWS Cloud portfolio to demonstrate hands-on skills in cloud architecture, security best practices, and full-stack web development.

---

## 🚀 Features

- 🔐 **User authentication** with hashed passwords (SHA-256)
- 📝 **CRUD operations** for articles (create, read, update, delete)
- 👤 **Personal dashboard** showing user-specific articles
- 🛡️ **Secure configuration** using environment variables (no hardcoded secrets)
- ☁️ **Cloud-native deployment** on AWS infrastructure
- 📱 **Responsive UI** built with Bootstrap 5

---

## 🏗️ Architecture

```
┌──────────────┐         ┌──────────────────┐         ┌──────────────────┐
│   End User   │────────▶│  EC2 (Ubuntu)    │────────▶│  RDS (MySQL)     │
│  (Browser)   │  HTTP   │  Flask App       │  SQL    │  wikidb          │
└──────────────┘         │  Port 8080       │         └──────────────────┘
                         └──────────────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │  Security Group  │
                         │  (port 22, 8080) │
                         └──────────────────┘
```

| Component | Service | Purpose |
|-----------|---------|---------|
| Compute | **Amazon EC2** (Ubuntu) | Hosts the Flask application |
| Database | **Amazon RDS** (MySQL) | Stores users and articles |
| Network | **VPC + Security Groups** | Controls inbound/outbound traffic |
| Access | **EC2 Instance Connect** | Browser-based SSH access |

---

## 🛠️ Tech Stack

- **Backend:** Python 3 · Flask · WTForms · passlib
- **Database:** MySQL (Amazon RDS)
- **Frontend:** Bootstrap 5 · Jinja2 templates
- **Cloud:** AWS EC2 · AWS RDS · AWS VPC
- **Security:** python-dotenv (environment variables)

---

## 📦 Installation

### Prerequisites

- Python 3.10+
- MySQL database (local or AWS RDS)
- pip + virtualenv

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/Gondran85/cloudwiki-pro.git
cd cloudwiki-pro

# 2. Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure environment variables
cp .env.example .env
# Edit .env with your actual database credentials

# 5. Set up the database
mysql -h <YOUR_DB_HOST> -u <USER> -p < dump.sql

# 6. Run the application
python wiki.py
```

The app will be available at `http://localhost:8080`

---

## 🔐 Environment Variables

Create a `.env` file based on `.env.example`:

```env
MYSQL_HOST=your-rds-endpoint.region.rds.amazonaws.com
MYSQL_USER=your_db_user
MYSQL_PASSWORD=your_secure_password
MYSQL_DB=wikidb
SECRET_KEY=generate-a-random-secret-key
```

> ⚠️ **Never commit your `.env` file.** It's already in `.gitignore`.

---
## 📸 Screenshots

### 🏠 Home Page

![Home page](<Pagina Inicial.jpg>)

![Login page](<Pagina Login.jpg>)

![Registration page](<Pagina Registro.jpg>)


### ☁️ AWS VPC / EC2 Instance / Subnets / RDS / Security Groups / Route Tables

![VPC](<Screenshot - VPC bootcamp.jpg>)

![EC2 instance running on AWS console](<Instancia EC2 - Funcionando.jpg>)

![Private Subnet 1](<Screenshot - private subnet - 1.jpg>)

![Private Subnet RDS](<Screenshot - private subnet - RDS.jpg>)

![Public Subnet](<Screenshot - publica subnet .jpg>)

![RDS](<Screenshot - Database MySql - RDS.jpg>)

![Security Groups](<Screenshot - Security Groups VPC.jpg>)

![Route Tables](<Screenshot - route tables.jpg>)

### 📖 About Page
![About page describing the project](<Screenshot - About.jpg>)

---

## 💰 Cost Estimate (AWS Free Tier)

When deployed entirely on AWS Free Tier:

| Service | Free Tier | Estimated Cost |
|---------|-----------|----------------|
| EC2 t2.micro | 750 hours/month | $0 |
| RDS db.t3.micro | 750 hours/month | $0 |
| Data transfer | 1 GB/month outbound | $0 |
| **Total** | — | **$0/month** |

Outside Free Tier: ~$15–25/month for the same setup.

---

## 🛡️ Security Best Practices Applied

- ✅ Credentials stored in environment variables (`.env`)
- ✅ `.env` excluded from version control via `.gitignore`
- ✅ Passwords hashed with SHA-256 before storage
- ✅ Flask `debug=False` in production
- ✅ Security Group restricts inbound traffic to necessary ports
- ✅ `.env.example` provided for safe onboarding

---

## 📚 What I Learned

Building this project taught me:

- How to **deploy a Python web app on AWS EC2** with proper user management
- How to **provision and connect to Amazon RDS** as a managed database
- The importance of **separating secrets from code** using environment variables
- How **Security Groups** act as virtual firewalls in AWS
- The difference between **Bootstrap 3 and 5** and how to migrate between them
- Practical use of **Jinja2 templates** in Flask applications

---

## 🚧 Future Improvements

- [ ] Migrate infrastructure to **Terraform** (Infrastructure as Code)
- [ ] Add **CI/CD pipeline** with GitHub Actions
- [ ] Containerize the app with **Docker**
- [ ] Add **HTTPS** via AWS Certificate Manager + Application Load Balancer
- [ ] Implement **search functionality** for articles
- [ ] Add **comments** and **likes** on articles
- [ ] Set up **CloudWatch** for application monitoring
- [ ] Migrate to **AWS RDS Aurora Serverless** for cost optimization

---

## 🧹 Cleanup (Avoid Unexpected AWS Charges)

To avoid charges after testing:

```bash
# 1. Stop the EC2 instance (or terminate if not needed)
# Console: EC2 → Instance → Instance State → Stop

# 2. Delete the RDS instance
# Console: RDS → Databases → Actions → Delete

# 3. Release any Elastic IPs (if used)
# Console: EC2 → Elastic IPs → Release
```

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Jefferson Gondran** — Aspiring AWS Cloud Engineer

- 🔗 LinkedIn:[www.linkedin.com/in/jefferson-santos-2136b2264](#)
- 🌐 Portfolio: Soon
- 📧 Email gondran.jefferson@gmail.com

---

⭐ **If you found this project useful, consider giving it a star on GitHub!**
