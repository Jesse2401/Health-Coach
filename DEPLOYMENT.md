# Single-Click Deployment Guide for Vercel

This project is configured for **single-click deployment** on Vercel with both frontend and backend.

## 🚀 Quick Deploy

1. **Push your code to GitHub**
2. **Go to [Vercel](https://vercel.com)**
3. **Import your GitHub repository**
4. **Vercel will auto-detect the configuration** - no manual settings needed!
5. **Add Environment Variables** (see below)
6. **Deploy!**

## 📋 Environment Variables to Set in Vercel

Go to **Project Settings → Environment Variables** and add:

### Database (Required)
```
DATABASE_URL=postgresql+asyncpg://user:password@host:port/database
```
**Note:** Use Vercel Postgres or any PostgreSQL service (Supabase, Neon, etc.)

### Redis (Required)
```
REDIS_URL=redis://user:password@host:port/db
```
**Note:** Use Upstash Redis (free tier available) or any Redis service

### LLM Provider (Required - choose one)

**For OpenAI:**
```
LLM_PROVIDER=openai
OPENAI_API_KEY=sk-your-key-here
```

**For Anthropic:**
```
LLM_PROVIDER=anthropic
ANTHROPIC_API_KEY=sk-ant-your-key-here
```

### Optional Settings
```
LLM_MODEL=gpt-4-turbo-preview
MAX_CONTEXT_TOKENS=8000
MAX_RESPONSE_TOKENS=1000
```

## 🏗️ Project Structure

```
├── api/
│   └── index.py          # Vercel serverless function entry point
├── backend/              # FastAPI backend code
├── frontend/             # React + Vite frontend
├── vercel.json          # Vercel configuration (auto-deploys both!)
└── requirements.txt     # Python dependencies
```

## 🔧 How It Works

1. **Frontend**: Built as static site from `frontend/` directory
2. **Backend**: Runs as serverless functions via `api/index.py`
3. **Routing**: 
   - `/api/*` → Backend (FastAPI)
   - `/*` → Frontend (React app)

## ⚠️ Important Notes

### Database Setup
- You **must** provide a PostgreSQL database
- Vercel Postgres is recommended (add it in Vercel dashboard)
- Or use external services like Supabase, Neon, or Railway

### Redis Setup
- You **must** provide a Redis instance
- Upstash Redis is recommended (free tier available)
- Or use Redis Cloud, Railway Redis, etc.

### First Deployment
- The database tables will be created automatically on first request
- You may want to run the seed script manually or add it to startup

## 🐛 Troubleshooting

### "vite: command not found"
- ✅ Fixed! The `vercel.json` now properly builds the frontend

### Database connection errors
- Check your `DATABASE_URL` environment variable
- Ensure the database is accessible from Vercel's servers
- Check firewall/network settings

### CORS errors
- The backend is configured to allow all origins in production
- If issues persist, check the CORS configuration in `backend/app/main.py`

## 📝 Next Steps After Deployment

1. **Seed the database** (optional):
   - You can add a one-time script or run it manually
   - Or modify the startup to auto-seed

2. **Update frontend API URL** (if needed):
   - The frontend uses relative URLs (`/api/chat/*`)
   - This should work automatically with the Vercel routing

3. **Monitor logs**:
   - Check Vercel dashboard → Functions → Logs
   - Monitor for any errors

## 🎉 That's It!

Your app should now be live with both frontend and backend running on a single Vercel deployment!

