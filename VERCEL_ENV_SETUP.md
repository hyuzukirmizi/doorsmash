# 🚀 Vercel Environment Variables Setup

## 📦 Backend Environment Variables

Go to your **backend** project in Vercel Dashboard → Settings → Environment Variables

Add the following variables:

```bash
# Frontend URL for CORS
FRONTEND_URL=https://www.udoorsmashorpass.tech

# Supabase Configuration
SUPABASE_URL=your_supabase_project_url
SUPABASE_KEY=your_supabase_service_role_key

# Google Gemini API (for chatbot)
GOOGLE_API_KEY=your_google_gemini_api_key

# API Configuration
NUTRITION_API_BASE=https://doorsmash-backend.vercel.app
ORDERS_API_BASE=https://doorsmash-backend.vercel.app
```

---

## 🎨 Frontend Environment Variables

Go to your **frontend** project in Vercel Dashboard → Settings → Environment Variables

Add the following variables:

```bash
# Backend API URLs
VITE_API_URL=https://doorsmash-backend.vercel.app
VITE_CHATBOT_API_URL=https://doorsmash-backend.vercel.app/api/chat

# Supabase Configuration (use ANON key, NOT service role key)
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key

# ElevenLabs (if using voice features)
VITE_ELEVENLABS_API_KEY=your_elevenlabs_api_key
```

---

## ✅ After Adding Environment Variables

1. **Redeploy Backend:**
   ```bash
   cd backend
   vercel --prod
   ```

2. **Redeploy Frontend:**
   ```bash
   cd frontend
   vercel --prod
   ```

3. **Test the connection:**
   - Open browser console on your deployed frontend
   - Run: `fetch('https://doorsmash-backend.vercel.app/api/health').then(r => r.json()).then(console.log)`
   - Should return: `{"status": "healthy"}`

---

## 🔗 Your URLs

| Component | URL |
|-----------|-----|
| **Frontend (Production)** | https://doorsmash-git-main-hyuzukirmizis-projects.vercel.app |
| **Frontend (Preview)** | https://doorsmash-92mnnq0bn-hyuzukirmizis-projects.vercel.app |
| **Frontend (Custom Domain)** | https://www.udoorsmashorpass.tech |
| **Backend** | https://doorsmash-backend.vercel.app |
| **Backend Health Check** | https://doorsmash-backend.vercel.app/api/health |
| **Backend Orders API** | https://doorsmash-backend.vercel.app/api/orders |
| **Backend Chatbot API** | https://doorsmash-backend.vercel.app/api/chat |

---

## 🧪 Testing Endpoints

### Health Check
```bash
curl https://doorsmash-backend.vercel.app/api/health
```

### Orders Endpoint
```bash
curl https://doorsmash-backend.vercel.app/orders
```

### Chatbot Endpoint
```bash
curl -X POST https://doorsmash-backend.vercel.app/api/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello", "user_id": "test-user"}'
```

---

## ⚠️ Important Notes

1. **CORS Configuration**: Already updated in `main.py` and `chatbot_api.py` to allow all your frontend domains
2. **Wildcard Support**: The backend accepts `https://*.vercel.app` to support preview deployments
3. **Custom Domain**: Your custom domain `www.udoorsmashorpass.tech` is whitelisted
4. **Environment Scope**: Set all variables to "Production, Preview, and Development" in Vercel for maximum compatibility

---

## 🔧 Troubleshooting

### CORS Errors
- Verify frontend URLs are added to backend CORS middleware
- Check that environment variables are saved in Vercel
- Redeploy both projects after changing env vars

### 404 Errors
- Ensure API routes start with `/api/` for Vercel routing
- Check `vercel.json` configuration in backend
- Verify the endpoint exists in your FastAPI app

### Environment Variables Not Loading
- Redeploy after adding/changing env vars
- Check the env vars are in the correct project (frontend vs backend)
- Verify no typos in variable names
