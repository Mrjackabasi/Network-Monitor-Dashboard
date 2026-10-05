
Real-Time network monitoring dashboard built with ASP.NET Core10,signalR,and clean Architecture.
# 🖥️ Network Monitor Dashboard
---

## ✨ Features

- **Real-time Dashboard** — Live host status updates via SignalR (no page refresh needed)
- **Ping & TCP Monitoring** — Checks host availability and measures latency
- **Uptime History** — Stores check results per host with full historical data
- **Alert System** — Automatically creates alerts when a host goes down or recovers
- **Host Management** — Full CRUD for managing monitored hosts and check intervals
- **JWT Authentication** — Secured API endpoints with token-based auth

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | ASP.NET Core 8 Web API |
| Architecture | Clean Architecture |
| Real-time | SignalR |
| Background Jobs | `BackgroundService` (Hosted Service) |
| ORM | Entity Framework Core 8 |
| Database | SQL Server |
| Auth | ASP.NET Identity + JWT |
| Containerization | Docker |

---

## 📁 Project Structure

```
NetworkMonitor.sln
├── src/
│   ├── NetworkMonitor.Domain          # Entities, Enums, Repository Interfaces
│   ├── NetworkMonitor.Application     # Use Cases, DTOs, Service Interfaces
│   ├── NetworkMonitor.Infrastructure  # EF Core, Ping/TCP impl, SignalR Hubs
│   └── NetworkMonitor.API             # Controllers, Middleware, Program.cs
└── tests/
    └── NetworkMonitor.Tests
```

---

## 🚀 Getting Started

### Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download)
- [SQL Server](https://www.microsoft.com/en-us/sql-server) (or Docker)
- [Docker](https://www.docker.com/) *(optional)*

### Run Locally

```bash
# Clone the repository
git clone https://github.com/your-username/network-monitor-dashboard.git
cd network-monitor-dashboard

# Apply database migrations
dotnet ef database update --project src/NetworkMonitor.Infrastructure --startup-project src/NetworkMonitor.API

# Run the API
dotnet run --project src/NetworkMonitor.API
```

### Run with Docker

```bash
docker-compose up --build
```

---

## ⚙️ Configuration

In `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=NetworkMonitorDb;Trusted_Connection=True;"
  },
  "JwtSettings": {
    "SecretKey": "your-secret-key",
    "ExpiresInMinutes": 60
  }
}
```

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/hosts` | Get all monitored hosts |
| `POST` | `/api/hosts` | Add a new host |
| `PUT` | `/api/hosts/{id}` | Update a host |
| `DELETE` | `/api/hosts/{id}` | Remove a host |
| `GET` | `/api/hosts/{id}/results` | Get check history for a host |
| `GET` | `/api/alerts` | Get unread alerts |
| `POST` | `/api/auth/login` | Authenticate and get JWT token |

### SignalR Hub

```
/hubs/monitor
```

| Event | Direction | Description |
|---|---|---|
| `HostStatusUpdated` | Server → Client | Fired on every check result |
| `AlertCreated` | Server → Client | Fired when a host goes down or recovers |

---

## 🗂️ Domain Model

```
Host
 ├── CheckResults   (IsOnline, LatencyMs, CheckType, CheckedAt)
 └── Alerts         (AlertType: Down | Recovered, IsRead)
```

All entities inherit from `BaseEntity` (`Id`, `CreatedAt`).

---

## 📌 Roadmap

- [x] Domain Layer — Entities, Enums, Repository Interfaces
- [x] Application Layer — Use Cases, DTOs
- [x] Infrastructure — EF Core, Ping/TCP implementation
- [ ] BackgroundService — Scheduled host checking
- [ ] SignalR Hub — Real-time dashboard updates
- [ ] Alert System — Down/Recovered notifications
- [ ] JWT Auth — Secured endpoints
- [ ] Docker — Containerized deployment
- [ ] Frontend Dashboard — HTML/JS real-time UI

---

## 📄 License

This project is licensed under the MIT License.
