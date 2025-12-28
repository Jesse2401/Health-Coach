# ⚠️ IMPORTANT: Vercel Root Directory Configuration

## ✅ Correct Setup

In the Vercel deployment dialog, you **MUST** set:

**Root Directory: `Health-Coach`** (the repository root)

OR

**Leave Root Directory EMPTY** (defaults to repo root)

## ❌ DO NOT SET

- ❌ `frontend` 
- ❌ `frontend/public`
- ❌ `backend`
- ❌ Any subdirectory

## Why?

The `vercel.json` is configured to:
1. Build the frontend from `frontend/` directory
2. Run backend API from `api/` directory  
3. Both need to be relative to the **repository root**

If you set root directory to a subdirectory, the paths in `vercel.json` won't work!

## Quick Fix

1. **Cancel** the current deployment
2. **Go back** to the project settings
3. **Set Root Directory to:** `Health-Coach` (or leave empty)
4. **Deploy again**

The `vercel.json` will handle everything automatically!

