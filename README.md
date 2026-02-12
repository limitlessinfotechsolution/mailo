# Mailto™ Platform

Enterprise-grade multi-tenant mail platform.

Licensed by & Designed and Developed by
Limitless Infotech Solution Pvt. Ltd.

## Tech Stack
- ASP.NET Core 10
- Blazor Server
- PostgreSQL
- Redis
- SMTP / IMAP

## Repository Structure
- `/src`: .NET Solution source code
- `/docs`: Architecture, Roadmap, and Guides
- `/scripts`: Database and Utility scripts
- `/tests`: Unit and Integration tests

## Run Locally
1. Ensure you have .NET 10 SDK and PostgreSQL/Redis installed.
2. `dotnet restore`
3. `dotnet ef database update`
4. `dotnet run --project src/Mailto.Api`

Alternatively, use Docker:
```bash
docker-compose up -d
```

## Features
- **Multi-Tenancy**: Isolated data per company.
- **Email**: Inbox, Sent, Drafts, Search.
- **Productivity**: Calendar and Contacts.
- **Admin**: Tenant and Domain management.
- **Modern UI**: iMac-inspired macOS-like interface.
