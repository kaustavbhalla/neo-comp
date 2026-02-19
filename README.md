# NeoComp 🚀

<div align="center">

![neoComp Logo](https://via.placeholder.com/150x150?text=nC)

**A Modern Competitive Programming Platform**

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Node.js](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/typescript-%5E5.0.0-blue.svg)](https://www.typescriptlang.org/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

[Features](#features) • [Quick Start](#quick-start) • [Documentation](#documentation) • [Contributing](#contributing)

</div>

---

## 📖 Overview

neoComp is a next-generation competitive programming platform built with modern web technologies. Inspired by platforms like LeetCode and Codeforces, it provides a secure, scalable environment for coding challenges with real-time feedback and contest support.

**Built as a learning project** to demonstrate enterprise-grade software engineering practices, cloud-native architecture, and DevOps workflows.

### 🎯 Key Highlights

- ⚡ **Real-time feedback** on code submissions via WebSockets
- 🔒 **Secure code execution** with sandboxed environments (Docker → nsjail)
- 📈 **Horizontal scalability** with Kubernetes and auto-scaling
- 🎨 **Modern UI** with Next.js 14 and TailwindCSS
- 🏆 **Contest system** with live leaderboards
- 📊 **Comprehensive monitoring** with Prometheus & Grafana

---

## ✨ Features

### Current (Phase 1 - MVP)

- 🔜 User authentication (JWT-based)
- 🔜 Problem library with difficulty ratings
- 🔜 Code submission and execution (Python, C++, Java)
- 🔜 Real-time verdict updates
- 🔜 Submission history and user dashboard
- 🔜 Basic leaderboard

### Coming Soon (Phase 2)

- 🔜 Contest system with live standings
- 🔜 Discussion forums and editorials
- 🔜 Advanced language support (Go, Rust, JavaScript)
- 🔜 Problem tags and advanced filtering
- 🔜 Rating system (ELO-based)

### Future (Phase 3)

- 💡 AI-powered hints
- 💡 Live coding interviews
- 💡 Collaborative coding sessions
- 💡 Learning paths and analytics

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         Client Layer                         │
│                    (Next.js + React 18)                      │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                    Load Balancer / CDN                       │
│                   (NGINX / Cloudflare)                       │
└────────────────────┬────────────────────────────────────────┘
                     │
        ┌────────────┴────────────┐
        ▼                         ▼
┌──────────────┐          ┌──────────────┐
│   Backend    │◄────────►│    Redis     │
│  API Server  │          │ (Cache +     │
│  (Node.js)   │          │  Queue)      │
└──────┬───────┘          └──────────────┘
       │
       ├─────────────┬─────────────┐
       ▼             ▼             ▼
┌──────────┐  ┌──────────┐  ┌──────────┐
│PostgreSQL│  │  Judge   │  │    S3    │
│(Database)│  │ Workers  │  │ (Storage)│
└──────────┘  │(Docker/  │  └──────────┘
              │ nsjail)  │
              └──────────┘
```

### Component Overview

- **Frontend**: Next.js 14, React 18, TypeScript, TailwindCSS, Monaco Editor
- **Backend API**: Node.js, Express, TypeScript, Prisma ORM
- **Database**: PostgreSQL 15 (primary), Redis (cache + queue)
- **Judge Workers**: Node.js → Go (Phase 3), Docker → nsjail (Phase 2)
- **Message Queue**: Redis with Bull
- **Object Storage**: AWS S3 / MinIO
- **Orchestration**: Docker Compose (dev) → Kubernetes (prod)

---

## 🛠️ Tech Stack

### Frontend

- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript 5.x
- **UI**: TailwindCSS, Radix UI
- **Code Editor**: Monaco Editor (VS Code engine)
- **State Management**: Zustand / React Query
- **Real-time**: Socket.io Client

### Backend

- **Runtime**: Node.js 20.x
- **Framework**: Express.js
- **Language**: TypeScript 5.x
- **ORM**: Prisma
- **Authentication**: JWT (jsonwebtoken, bcrypt)
- **Validation**: Zod
- **WebSockets**: Socket.io

### Database & Storage

- **Primary DB**: PostgreSQL 15
- **Cache/Queue**: Redis 7.x
- **Object Storage**: AWS S3 / MinIO
- **ORM**: Prisma

### Infrastructure

- **Containerization**: Docker & Docker Compose
- **Orchestration**: Kubernetes (EKS/GKE/AKS)
- **CI/CD**: GitHub Actions
- **Monitoring**: Prometheus, Grafana, Jaeger
- **Logging**: Winston (structured JSON logs)

### Code Execution

- **Phase 1**: Docker containers
- **Phase 2**: nsjail (Linux sandboxing)
- **Phase 3**: Firecracker MicroVMs (optional)

---

## 🚀 Quick Start

### Prerequisites

- **Node.js** >= 18.0.0
- **Docker** & Docker Compose
- **PostgreSQL** 15+ (or use Docker)
- **Redis** 7+ (or use Docker)
- **Git**

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/neocomp.git
   cd neocomp
   ```

2. **Install dependencies**

   ```bash
   # Install backend dependencies
   cd backend
   npm install

   # Install frontend dependencies
   cd ../frontend
   npm install

   # Install judge worker dependencies
   cd ../judge-worker
   npm install
   ```

3. **Set up environment variables**

   ```bash
   # Backend (.env)
   cp backend/.env.example backend/.env
   # Edit backend/.env with your configuration

   # Frontend (.env.local)
   cp frontend/.env.example frontend/.env.local
   # Edit frontend/.env.local
   ```

4. **Start infrastructure with Docker Compose**

   ```bash
   docker-compose up -d
   ```

   This starts:
   - PostgreSQL (port 5432)
   - Redis (port 6379)
   - MinIO (port 9000)

5. **Run database migrations**

   ```bash
   cd backend
   npx prisma migrate dev
   npx prisma db seed  # Optional: seed with sample data
   ```

6. **Start development servers**

   ```bash
   # Terminal 1: Backend API
   cd backend
   npm run dev  # Runs on http://localhost:3001

   # Terminal 2: Frontend
   cd frontend
   npm run dev  # Runs on http://localhost:3000

   # Terminal 3: Judge Worker
   cd judge-worker
   npm run dev
   ```

7. **Open your browser**
   - Frontend: http://localhost:3000
   - API: http://localhost:3001
   - API Docs: http://localhost:3001/api/docs

---

## 📁 Project Structure

```
neocomp/
├── backend/                 # Node.js API Server
│   ├── src/
│   │   ├── controllers/     # Route handlers
│   │   ├── middleware/      # Auth, validation, error handling
│   │   ├── routes/          # API routes
│   │   ├── services/        # Business logic
│   │   ├── utils/           # Helpers
│   │   ├── types/           # TypeScript types
│   │   └── app.ts           # Express app setup
│   ├── prisma/
│   │   ├── schema.prisma    # Database schema
│   │   └── migrations/      # DB migrations
│   ├── tests/               # Unit & integration tests
│   ├── .env.example
│   └── package.json
│
├── frontend/                # Next.js Frontend
│   ├── src/
│   │   ├── app/             # App Router pages
│   │   ├── components/      # React components
│   │   ├── lib/             # Utilities
│   │   ├── hooks/           # Custom hooks
│   │   └── types/           # TypeScript types
│   ├── public/              # Static assets
│   ├── .env.example
│   └── package.json
│
├── judge-worker/            # Code Execution Service
│   ├── src/
│   │   ├── executors/       # Language-specific executors
│   │   ├── sandbox/         # Sandboxing logic
│   │   ├── queue/           # Queue consumer
│   │   └── index.ts
│   ├── configs/             # nsjail configs
│   └── package.json
│
├── infrastructure/          # Infrastructure as Code
│   ├── docker/
│   │   ├── Dockerfile.backend
│   │   ├── Dockerfile.frontend
│   │   └── Dockerfile.judge
│   ├── k8s/                 # Kubernetes manifests
│   │   ├── deployments/
│   │   ├── services/
│   │   └── ingress/
│   └── terraform/           # Cloud infrastructure
│
├── docs/                    # Documentation
│   ├── api/                 # API documentation
│   ├── architecture/        # Architecture diagrams
│   └── setup/               # Setup guides
│
├── scripts/                 # Utility scripts
│   ├── setup-dev.sh         # Dev environment setup
│   ├── seed-db.ts           # Database seeding
│   └── load-test.js         # Load testing
│
├── docker-compose.yml       # Local development
├── .github/
│   └── workflows/           # CI/CD pipelines
├── README.md
├── CONTRIBUTING.md
├── LICENSE
└── .gitignore
```

---

## 🔧 Environment Variables

### Backend (`backend/.env`)

```bash
# Server
NODE_ENV=development
PORT=3001
API_URL=http://localhost:3001

# Database
DATABASE_URL="postgresql://postgres:password@localhost:5432/neocomp?schema=public"

# Redis
REDIS_URL=redis://localhost:6379

# JWT
JWT_SECRET=your-super-secret-jwt-key-change-in-production
JWT_REFRESH_SECRET=your-refresh-token-secret
JWT_EXPIRES_IN=15m
JWT_REFRESH_EXPIRES_IN=7d

# AWS S3 (or MinIO for local dev)
S3_ENDPOINT=http://localhost:9000
S3_BUCKET=neocomp-testcases
S3_ACCESS_KEY=minioadmin
S3_SECRET_KEY=minioadmin
S3_REGION=us-east-1

# Email (optional, for notifications)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# CORS
CORS_ORIGIN=http://localhost:3000
```

### Frontend (`frontend/.env.local`)

```bash
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_WS_URL=ws://localhost:3001
NEXT_PUBLIC_ENV=development
```

### Judge Worker (`judge-worker/.env`)

```bash
NODE_ENV=development
REDIS_URL=redis://localhost:6379
DATABASE_URL="postgresql://postgres:password@localhost:5432/neocomp"
S3_ENDPOINT=http://localhost:9000
S3_BUCKET=neocomp-testcases
S3_ACCESS_KEY=minioadmin
S3_SECRET_KEY=minioadmin
```

---

## 🐳 Docker Compose

Start all services locally:

```bash
docker-compose up -d
```

Services included:

- **postgres**: PostgreSQL database (port 5432)
- **redis**: Redis cache & queue (port 6379)
- **minio**: S3-compatible storage (port 9000, console: 9001)

Stop all services:

```bash
docker-compose down
```

View logs:

```bash
docker-compose logs -f [service-name]
```

---

## 📚 Development

### Running Tests

```bash
# Backend tests
cd backend
npm test                  # Run all tests
npm run test:watch        # Watch mode
npm run test:coverage     # Coverage report

# Frontend tests
cd frontend
npm test
```

### Database Management

```bash
# Create a new migration
npx prisma migrate dev --name add-contests-table

# Apply migrations
npx prisma migrate deploy

# Open Prisma Studio (DB GUI)
npx prisma studio

# Reset database (⚠️ deletes all data)
npx prisma migrate reset
```

### Code Quality

```bash
# Linting
npm run lint

# Type checking
npm run type-check

# Format code
npm run format
```

### Building for Production

```bash
# Backend
cd backend
npm run build
npm start

# Frontend
cd frontend
npm run build
npm start
```

---

## 🧪 Testing

### Unit Tests

```bash
# Backend unit tests
cd backend
npm run test:unit

# Frontend unit tests
cd frontend
npm test
```

### Integration Tests

```bash
cd backend
npm run test:integration
```

### End-to-End Tests

```bash
cd frontend
npm run test:e2e
```

### Load Testing

```bash
# Using k6
cd scripts
k6 run load-test.js

# Or using Artillery
artillery run load-test.yml
```

---

## 🚢 Deployment

### Docker Deployment

Build images:

```bash
docker build -f infrastructure/docker/Dockerfile.backend -t neocomp/backend:latest .
docker build -f infrastructure/docker/Dockerfile.frontend -t neocomp/frontend:latest .
docker build -f infrastructure/docker/Dockerfile.judge -t neocomp/judge:latest .
```

### Kubernetes Deployment

```bash
# Apply all manifests
kubectl apply -f infrastructure/k8s/

# Check deployments
kubectl get deployments -n neocomp

# Check pods
kubectl get pods -n neocomp

# View logs
kubectl logs -f deployment/backend -n neocomp
```

### CI/CD

GitHub Actions automatically:

- Runs tests on every PR
- Builds Docker images on merge to `main`
- Deploys to staging environment
- Deploys to production on tagged releases

---

## 📊 Monitoring & Observability

### Metrics (Prometheus)

Access Prometheus: http://localhost:9090

```bash
# View metrics endpoint
curl http://localhost:3001/metrics
```

### Dashboards (Grafana)

Access Grafana: http://localhost:3001

- Default credentials: admin/admin
- Pre-configured dashboards for system metrics

### Logs

```bash
# View backend logs
docker-compose logs -f backend

# View judge worker logs
docker-compose logs -f judge-worker

# Search logs
docker-compose logs backend | grep ERROR
```

### Tracing (Jaeger)

Access Jaeger UI: http://localhost:16686

---

## 🔒 Security

### Code Execution Sandbox

**Phase 1 (MVP)**: Docker containers with resource limits

```bash
docker run --rm \
  --memory=256m \
  --cpus=1 \
  --network=none \
  python:3.11 python solution.py
```

**Phase 2 (Production)**: nsjail sandboxing

```bash
nsjail --config /etc/nsjail/python.cfg \
  -- python3 solution.py < input.txt > output.txt
```

### Security Best Practices

- ✅ JWT authentication with refresh tokens
- ✅ Password hashing with bcrypt (12 rounds)
- ✅ Rate limiting on all endpoints
- ✅ Input validation with Zod
- ✅ Parameterized SQL queries (Prisma)
- ✅ CORS configuration
- ✅ Helmet.js for security headers
- ✅ HTTPS in production (TLS 1.3)

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Style

- Follow the [TypeScript Style Guide](https://typescript-eslint.io/rules/)
- Use Prettier for formatting
- Write meaningful commit messages (Conventional Commits)

---

## 📝 API Documentation

API documentation is available at:

- **Development**: http://localhost:3001/api/docs

### Key Endpoints

```
Authentication:
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/refresh
POST   /api/auth/logout

Problems:
GET    /api/problems
GET    /api/problems/:id
POST   /api/problems              (Admin only)

Submissions:
POST   /api/submissions
GET    /api/submissions/:id
GET    /api/submissions/user/:userId

Leaderboard:
GET    /api/leaderboard/global
GET    /api/leaderboard/problem/:id
```

---

## 🗺️ Roadmap

### Phase 1: Foundation (Weeks 1-4) ✅

- [ ] Basic authentication
- [ ] Problem CRUD
- [ ] Code submission with Docker
- [ ] Simple verdict system

### Phase 2: Production Ready (Weeks 5-8) 🚧

- [ ] Message queue integration
- [ ] nsjail sandboxing
- [ ] WebSocket real-time updates
- [ ] Caching layer
- [ ] Monitoring & logging

### Phase 3: Scale & Features (Weeks 9-12) 📅

- [ ] Kubernetes deployment
- [ ] Contest system
- [ ] Rating system
- [ ] Advanced language support

### Future Enhancements

- [ ] AI-powered hints
- [ ] Live coding interviews
- [ ] Collaborative sessions
- [ ] Mobile app

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Authors

- **Kaustav Bhalla** - [@kaustavbhalla](https://github.com/kaustavbhalla)

---

## 🙏 Acknowledgments

- Inspired by [LeetCode](https://leetcode.com), [Codeforces](https://codeforces.com), and [HackerRank](https://hackerrank.com)
- Built with amazing open-source technologies
- Special thanks to the competitive programming community

---

## 🌟 Star History

If you find this project helpful, please consider giving it a star ⭐

[![Star History Chart](https://api.star-history.com/svg?repos=kaustavbhalla/neo-comp&type=Date)](https://star-history.com/#kaustavbhalla/neo-comp&Date)

---

<div align="center">

**Built with ❤️ for the competitive programming community**

[⬆ Back to Top](#neocomp-)

</div>
