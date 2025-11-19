# Local Testing Before Render Deployment

Quick guide to test locally before deploying to Render.com.

## Prerequisites Check

```bash
cd /Users/svl/Projects/gw

# 1. Install dependencies (if not already done)
pnpm install

# 2. Start Docker services (PostgreSQL & Redis)
docker compose up -d

# 3. Wait for services to be ready
sleep 5

# 4. Push database schema
pnpm push-dev
```

## Test API Build

```bash
# Build core packages first
pnpm build:core

# Build API
cd apps/api
pnpm build

# Test API start (should work with your .env)
pnpm start
# Should start on port 4002 (or PORT from .env)
```

## Test UI Build

```bash
# Make sure API is built first (for openapi.json)
cd /Users/svl/Projects/gw
pnpm build:core

# Build UI
cd apps/ui
pnpm generate  # Generates types from API openapi.json
pnpm build

# Test UI start
pnpm start
# Should start on port 3000 (or PORT from .env)
```

## Full Local Test

```bash
# From root directory
cd /Users/svl/Projects/gw

# 1. Ensure Docker is running
docker compose up -d

# 2. Build everything
pnpm build:core

# 3. Test API in one terminal
cd apps/api
pnpm start

# 4. Test UI in another terminal
cd apps/ui
pnpm start

# 5. Verify:
# - API: http://localhost:4002/
# - UI: http://localhost:3000
```

## Verify Render Build Commands

The build commands in `render.yaml` should match what works locally:

**API Build:**
```bash
pnpm install && pnpm build:core && cd apps/api && pnpm build
```

**UI Build:**
```bash
pnpm install && pnpm build:core && cd apps/ui && pnpm generate && pnpm build
```

## Common Issues

1. **Missing openapi.json**: Run `pnpm build:core` first to generate it
2. **Database connection**: Ensure Docker is running and `.env` has correct `DATABASE_URL`
3. **Redis connection**: Ensure Redis is running and `.env` has correct Redis settings
4. **Port conflicts**: Check if ports 3000, 4002 are available

## Ready for Render?

Once local builds work:
- ✅ API builds successfully
- ✅ UI builds successfully
- ✅ Both start without errors
- ✅ Database migrations work
- ✅ Services can connect to database and Redis

Then you're ready to deploy to Render.com!

