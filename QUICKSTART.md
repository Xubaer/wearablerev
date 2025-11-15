# Quick Start Guide

## Prerequisites
- Node.js 20.x or later
- pnpm 10.x or later (install with `npm install -g pnpm`)
- Docker and Docker Compose

## Initial Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd wearablerev
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Configure environment variables**
   ```bash
   cp .env.example .env
   # Edit .env and replace all 'replace-with-random-value' with secure random strings
   ```

4. **Start services**
   
   Option A: Using Docker (Recommended)
   ```bash
   pnpm docker:up
   ```
   
   Option B: Without Docker (Development)
   ```bash
   # Start PostgreSQL only
   docker compose up -d postgres
   
   # Start all apps
   pnpm dev
   ```

## Access Applications

- **Next.js Frontend**: http://localhost:3000
- **Strapi Admin**: http://localhost:1337/admin
- **Directus**: http://localhost:8055

## Strapi First-Time Setup

When accessing Strapi for the first time at http://localhost:1337/admin, you'll need to create an admin user:

1. Fill in your details:
   - First Name
   - Last Name
   - Email
   - Password (min 8 characters)
2. Click "Let's start"

## Directus First-Time Setup

When using Docker, Directus is pre-configured with:
- Email: admin@example.com
- Password: d1r3ctu5

**Important**: Change these credentials after first login!

## Common Commands

```bash
# Install dependencies
pnpm install

# Start all apps in development
pnpm dev

# Build all apps
pnpm build

# Docker commands
pnpm docker:up      # Start all Docker services
pnpm docker:down    # Stop all Docker services
pnpm docker:logs    # View Docker logs

# Individual app commands
cd apps/frontend && pnpm dev      # Next.js
cd apps/strapi && pnpm develop    # Strapi
cd apps/directus && pnpm dev      # Directus
```

## Database Information

PostgreSQL is configured with two separate databases:
- `strapi` - For Strapi CMS
- `directus` - For Directus
- `wearablerev` - Main database (if needed)

Default credentials (change in production):
- Host: localhost
- Port: 5432
- Username: admin
- Password: adminpassword

## Troubleshooting

### Port already in use
If you get port conflicts, check if services are already running:
```bash
docker compose ps
lsof -i :3000  # Check Next.js port
lsof -i :1337  # Check Strapi port
lsof -i :8055  # Check Directus port
lsof -i :5432  # Check PostgreSQL port
```

### Database connection issues
Ensure PostgreSQL is running:
```bash
docker compose ps postgres
docker compose logs postgres
```

### Strapi build issues
Clear cache and rebuild:
```bash
cd apps/strapi
rm -rf .cache build
pnpm build
```

### pnpm install issues
Clear the pnpm store and reinstall:
```bash
pnpm store prune
pnpm install --force
```

## Production Deployment

Before deploying to production:

1. **Generate secure secrets**
   ```bash
   node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
   ```
   Use these values for all secret keys in `.env`

2. **Update environment variables**
   - Set `NODE_ENV=production`
   - Use strong passwords
   - Configure proper database URLs
   - Set correct PUBLIC_URL for Directus

3. **Configure CORS**
   - Update Strapi middleware configuration
   - Set allowed origins for both CMSs

4. **Enable SSL/TLS**
   - Use HTTPS for all services
   - Configure proper certificates

5. **Database backups**
   - Set up regular PostgreSQL backups
   - Test restore procedures

## Next Steps

- Configure Strapi content types
- Set up Directus collections
- Connect Next.js to your CMS of choice
- Add authentication
- Configure file uploads
- Set up CI/CD pipeline

For more details, see the main [README.md](README.md)
