# MailO - Enterprise Email Server Platform

<div align="center">

![MailO Logo](https://via.placeholder.com/200x200/1a202c/ffffff?text=MailO)

**A Modern, Self-Hosted Email Server Solution**

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Node Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)](https://nodejs.org)
[![Docker](https://img.shields.io/badge/docker-ready-blue.svg)](https://www.docker.com/)
[![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-2088FF.svg)](https://github.com/features/actions)

**Developed by [Limitless Infotech Solution Pvt Ltd.](https://limitlessinfotech.com)**

[Features](#-features) • [Quick Start](#-quick-start) • [Documentation](#-documentation) • [Demo](#-demo) • [Support](#-support)

</div>

---

## 📖 Overview

**MailO** is a comprehensive, enterprise-grade email server platform that gives you complete control over your email infrastructure. Built with modern technologies and designed for scalability, MailO provides everything you need to run your own email service.

### Why MailO?

- 🔒 **Privacy First**: Your data stays on your servers
- 💰 **Cost Effective**: No per-user licensing fees
- 🎨 **Modern UI**: Beautiful, responsive webmail interface
- 🚀 **High Performance**: Optimized for speed and reliability
- 🔧 **Easy to Deploy**: Docker-based deployment in minutes
- 📊 **Feature Rich**: Calendar, contacts, tasks, campaigns, and more
- 🌍 **Self-Hosted**: Complete control over your email infrastructure

---

## ✨ Features

### Core Email Functionality

- ✉️ **Full Email Server**: SMTP, IMAP, and POP3 support
- 📬 **Modern Webmail**: React-based responsive interface with dark mode
- 🔍 **Advanced Search**: Fast, full-text email search
- 📎 **Attachments**: Support for large file attachments via MinIO
- ⏰ **Send Later**: Schedule emails for future delivery
- ↩️ **Undo Send**: 10-second window to cancel sent emails
- ⏱️ **Snooze**: Temporarily hide emails until a specified time
- ⭐ **Folders & Labels**: Organize emails your way

### Productivity Tools

- 📅 **Calendar**: Event scheduling with reminders and recurrence
- 👥 **Contacts**: Comprehensive address book management
- ✅ **Tasks**: To-do lists with priorities and due dates
- 📝 **Notes**: Quick note-taking with rich text support
- 📢 **Email Campaigns**: Bulk email marketing with templates

### Administration

- 🛡️ **Multi-Tenancy**: Support for multiple domains
- 👨‍💼 **Role-Based Access**: User, Domain Admin, Super Admin roles
- 📊 **Analytics**: Email statistics and usage reports
- 🔐 **2FA**: Two-factor authentication for enhanced security
- 💾 **Quota Management**: Storage limits per user/domain
- 🔄 **Real-time Updates**: WebSocket-based notifications

### Developer Features

- 🐳 **Docker Ready**: Complete Docker Compose setup
- 🔄 **CI/CD**: Automated testing and deployment
- 📡 **REST API**: Comprehensive API for integrations
- 🔌 **WebSocket**: Real-time communication
- 📦 **Modular**: Microservices architecture
- 🧪 **Testable**: Built with testing in mind

---

## 🚀 Quick Start

### Prerequisites

- Docker & Docker Compose V2
- Node.js 18+ (for local development)
- 2GB RAM minimum (4GB recommended)
- 10GB disk space

### Installation

#### Option 1: Docker (Recommended)

```bash
# Clone the repository
git clone https://github.com/limitlessinfotechsolution/mailo.git
cd mailo

# Copy environment template
cp .env.example .env

# Edit configuration (set your domain, passwords, etc.)
nano .env

# Start all services
docker compose up -d

# Check status
docker compose ps
```

#### Option 2: Local Development

```bash
# Clone the repository
git clone https://github.com/limitlessinfotechsolution/mailo.git
cd mailo

# Install dependencies
npm install

# Start development servers
npm run dev
```

### Access the Application

- **Webmail**: http://localhost (or http://localhost:5173 in dev mode)
- **Backend API**: http://localhost:5000
- **MinIO Console**: http://localhost:9001

### Default Credentials

```
Email: admin@localhost
Password: admin123
```

> ⚠️ **Important**: Change the default password immediately!

---

## 📚 Documentation

### For Users

- [User Guide](docs/USER_GUIDE.md) - How to use MailO
- [FAQ](docs/FAQ.md) - Frequently asked questions

### For Developers

- [Developer Documentation](DEVELOPER_DOCS.md) - Complete development guide
- [API Reference](docs/API_REFERENCE.md) - REST API documentation
- [Architecture](docs/ARCHITECTURE.md) - System architecture overview

### For Administrators

- [Deployment Guide](DEPLOYMENT.md) - Production deployment
- [CI/CD Automation](CI_CD_AUTOMATION.md) - Automated workflows
- [Security Guide](docs/SECURITY.md) - Security best practices
- [Backup & Recovery](docs/BACKUP.md) - Data backup procedures

---

## 🏗️ Architecture

```
┌─────────────┐
│   Webmail   │  React 19 + Vite + TailwindCSS
│  (Nginx)    │
└──────┬──────┘
       │
┌──────▼──────┐
│  Backend    │  Node.js + Express + Socket.IO
│    API      │
└──────┬──────┘
       │
   ┌───┴────┬────────┬─────────┐
   │        │        │         │
┌──▼──┐  ┌─▼──┐  ┌──▼───┐  ┌─▼────┐
│Mongo│  │Redis│ │MinIO │  │BullMQ│
│ DB  │  │Cache│ │ S3   │  │Queue │
└─────┘  └────┘  └──────┘  └──────┘
```

---

## 💻 Technology Stack

### Frontend
- **React 19** - UI framework
- **Vite** - Build tool
- **TailwindCSS** - Styling
- **Socket.IO** - Real-time updates
- **Axios** - HTTP client

### Backend
- **Node.js 18+** - Runtime
- **Express** - Web framework
- **MongoDB** - Database
- **Redis** - Caching & sessions
- **MinIO** - Object storage
- **BullMQ** - Job queue

### Infrastructure
- **Docker** - Containerization
- **Nginx** - Web server
- **GitHub Actions** - CI/CD

---

## 🎯 Use Cases

- **Corporate Email**: Replace expensive hosted email solutions
- **Educational Institutions**: Provide email for students and staff
- **Government Organizations**: Maintain data sovereignty
- **Privacy-Focused Businesses**: Keep email data in-house
- **Email Service Providers**: White-label email hosting
- **Development Teams**: Internal communication platform

---

## 🛣️ Roadmap

### Version 1.0 (Current)
- ✅ Core email functionality
- ✅ Webmail interface
- ✅ Calendar, Contacts, Tasks, Notes
- ✅ Email campaigns
- ✅ Admin panel
- ✅ CI/CD automation

### Version 1.1 (Q1 2026)
- [ ] End-to-end encryption (PGP/GPG)
- [ ] Mobile applications (iOS/Android)
- [ ] Advanced spam filtering
- [ ] Email templates library
- [ ] Shared mailboxes
- [ ] Email rules and filters

### Version 2.0 (Q3 2026)
- [ ] AI-powered features
- [ ] Video conferencing
- [ ] Team collaboration
- [ ] Advanced analytics
- [ ] Multi-language support
- [ ] Plugin ecosystem

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

```bash
# Fork and clone
git clone https://github.com/YOUR_USERNAME/mailo.git
cd mailo

# Install dependencies
npm install

# Create a feature branch
git checkout -b feature/amazing-feature

# Make your changes and commit
git commit -m 'Add amazing feature'

# Push and create PR
git push origin feature/amazing-feature
```

### Code of Conduct

Please read our [Code of Conduct](CODE_OF_CONDUCT.md) before contributing.

---

## 📊 Project Stats

- **Lines of Code**: ~50,000+
- **Components**: 15+ React components
- **API Endpoints**: 40+ REST endpoints
- **Database Models**: 10+ Mongoose schemas
- **Docker Images**: 5 services
- **Test Coverage**: Growing (contributions welcome!)

---

## 🔒 Security

### Reporting Vulnerabilities

If you discover a security vulnerability, please email:
**security@limitlessinfotech.com**

Do not open public issues for security vulnerabilities.

### Security Features

- JWT-based authentication
- bcrypt password hashing
- Two-factor authentication (2FA)
- Rate limiting
- CORS protection
- Helmet.js security headers
- Input sanitization
- SQL injection prevention

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**Copyright © 2025 Limitless Infotech Solution Pvt Ltd.**

---

## 🙏 Acknowledgments

- Built with ❤️ by [Limitless Infotech Solution Pvt Ltd.](https://limitlessinfotech.com)
- Inspired by modern email platforms
- Thanks to all open-source contributors

---

## 📞 Support & Contact

### Commercial Support

For enterprise support, custom development, or licensing:
- **Email**: sales@limitlessinfotech.com
- **Website**: https://limitlessinfotech.com
- **Phone**: +1-XXX-XXX-XXXX

### Community Support

- **Documentation**: https://docs.mailo.io
- **GitHub Issues**: https://github.com/limitlessinfotechsolution/mailo/issues
- **Discussions**: https://github.com/limitlessinfotechsolution/mailo/discussions
- **Discord**: https://discord.gg/mailo (coming soon)

### Social Media

- **Twitter**: [@MailOPlatform](https://twitter.com/MailOPlatform)
- **LinkedIn**: [Limitless Infotech](https://linkedin.com/company/limitlessinfotech)
- **YouTube**: [MailO Tutorials](https://youtube.com/@MailOPlatform)

---

## ⭐ Star History

If you find MailO useful, please consider giving it a star!

[![Star History Chart](https://api.star-history.com/svg?repos=limitlessinfotechsolution/mailo&type=Date)](https://star-history.com/#limitlessinfotechsolution/mailo&Date)

---

<div align="center">

**Made with ❤️ by Limitless Infotech Solution Pvt Ltd.**

[Website](https://limitlessinfotech.com) • [Documentation](DEVELOPER_DOCS.md) • [Support](mailto:support@limitlessinfotech.com)

</div>
