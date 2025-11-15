# wearablerev

WearableRevolution.com monorepo with Next.js, Strapi, and Directus.

## 🏗️ Architecture

This monorepo contains:

- **Frontend** (`apps/frontend`): Next.js 16 application with TypeScript, Tailwind CSS, and App Router
- **Strapi** (`apps/strapi`): Strapi 5 headless CMS
- **Directus** (`apps/directus`): Directus 11 data platform
- **PostgreSQL**: Database for both Strapi and Directus

## 📋 Prerequisites

- Node.js 20.x or later
- pnpm 10.x or later
- Docker and Docker Compose

## 🚀 Getting Started

### 1. Install Dependencies

```bash
# Install pnpm globally if not already installed
npm install -g pnpm

# Install all dependencies
pnpm install
```

### 2. Configure Environment Variables

```bash
# Copy the example environment file
cp .env.example .env

# Edit .env and replace all 'replace-with-random-value' with secure random strings
# You can generate random values using:
# node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
```

### 3. Start with Docker (Recommended)

```bash
# Start all services (PostgreSQL, Strapi, Directus)
pnpm docker:up

# View logs
pnpm docker:logs

# Stop all services
pnpm docker:down
```

### 4. Start Without Docker (Development)

```bash
# Start PostgreSQL with Docker only
docker-compose up -d postgres

# Start all applications in development mode
pnpm dev

# Or start individually:
cd apps/frontend && pnpm dev  # Next.js on http://localhost:3000
cd apps/strapi && pnpm develop  # Strapi on http://localhost:1337
cd apps/directus && pnpm dev  # Directus on http://localhost:8055
```

## 📦 Applications

### Next.js Frontend
- **URL**: http://localhost:3000
- **Technology**: Next.js 16, React 19, TypeScript, Tailwind CSS 4

### Strapi CMS
- **URL**: http://localhost:1337
- **Admin Panel**: http://localhost:1337/admin
- **Technology**: Strapi 5.31.0
- **Database**: PostgreSQL (strapi database)

### Directus CMS
- **URL**: http://localhost:8055
- **Technology**: Directus 11.13.2
- **Database**: PostgreSQL (directus database)
- **Default Credentials** (when using Docker):
  - Email: admin@example.com
  - Password: d1r3ctu5

## 🛠️ Available Scripts

### Root Level
- `pnpm dev` - Start all applications in development mode
- `pnpm build` - Build all applications
- `pnpm docker:up` - Start Docker services
- `pnpm docker:down` - Stop Docker services
- `pnpm docker:logs` - View Docker logs

### Frontend (apps/frontend)
- `pnpm dev` - Start Next.js development server
- `pnpm build` - Build for production
- `pnpm start` - Start production server
- `pnpm lint` - Run ESLint

### Strapi (apps/strapi)
- `pnpm develop` - Start Strapi in development mode
- `pnpm start` - Start Strapi in production mode
- `pnpm build` - Build Strapi admin panel
- `pnpm strapi` - Run Strapi CLI commands

### Directus (apps/directus)
- `pnpm dev` - Start Directus
- `pnpm start` - Start Directus
- `pnpm bootstrap` - Bootstrap Directus

## 🗄️ Database

The PostgreSQL container creates two separate databases:
- `strapi` - For Strapi CMS
- `directus` - For Directus
- `wearablerev` - Main database (if needed)

### Database Connection
- **Host**: localhost
- **Port**: 5432
- **Username**: admin (configurable in .env)
- **Password**: adminpassword (configurable in .env)

## 🐳 Docker Services

### Ports
- **PostgreSQL**: 5432
- **Next.js**: 3000 (not in Docker by default)
- **Strapi**: 1337
- **Directus**: 8055

### Volumes
- `postgres_data` - PostgreSQL data persistence
- `strapi_uploads` - Strapi uploaded files
- `directus_uploads` - Directus uploaded files
- `directus_extensions` - Directus extensions

## 📝 Notes

- This is a pnpm workspace monorepo
- All packages share dependencies where possible
- Docker Compose handles service orchestration
- Each application can be developed independently
- Hot reload is enabled for all applications in development mode

## 🔒 Security

**Important**: Before deploying to production:
1. Generate secure random values for all secrets in `.env`
2. Use strong passwords for database and admin accounts
3. Configure proper CORS settings
4. Enable SSL/TLS for production
5. Review and update security settings in each application

## 📚 Documentation

- [Next.js Documentation](https://nextjs.org/docs)
- [Strapi Documentation](https://docs.strapi.io)
- [Directus Documentation](https://docs.directus.io)
- [pnpm Documentation](https://pnpm.io)

## 📄 License

ISC
