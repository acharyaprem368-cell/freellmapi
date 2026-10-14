# Deploy to Vercel Free Hosting

## Prerequisites
- GitHub repo `freellmapi` pushed to origin/main
- Vercel account logged in

## Steps
1. Go to https://vercel.com/new
2. Import Git Repository → select `acharyaprem368-cell/freellmapi`
3. Framework Preset: Other
4. Vercel will detect `vercel.json` with container runtime
5. Environment Variables (optional, defaults already in vercel.json):
   - NODE_ENV=production
   - PORT=3001
   - FREEAPI_DB_PATH=/app/server/data/freeapi.db
   - FREEAPI_DB_BACKUP_PATH=/app/server/data/backups
6. Deploy

## What happens
- Vercel builds Docker image from Dockerfile at repo root
- Container runs `node server/dist/index.js` on port 3001
- Server serves UI + API from same container
- SQLite DB persists in container filesystem

## Notes
- Free tier containers sleep after inactivity
- First request may be slow cold start
- Backup DB via /api/backups regularly

## Post-Deploy Smoke Test
1. Open https://your-project.vercel.app/
2. Verify UI loads and shows FreeLLMAPI header
3. Visit https://your-project.vercel.app/api/ping → should return {"status":"ok"}
4. Visit https://your-project.vercel.app/keys → should show Keys page
5. Check logs in Vercel dashboard for "Database initialized at /app/server/data/freeapi.db"
