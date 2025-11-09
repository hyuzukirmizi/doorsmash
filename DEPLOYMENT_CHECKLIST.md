# 🎯 Final Deployment Checklist

## ✅ What's Been Configured

### Backend (`main.py` & `chatbot_api.py`)
- ✅ CORS middleware updated with all frontend URLs:
  - `https://doorsmash-git-main-hyuzukirmizis-projects.vercel.app`
  - `https://doorsmash-92mnnq0bn-hyuzukirmizis-projects.vercel.app`
  - `https://www.udoorsmashorpass.tech`
  - `https://*.vercel.app` (wildcard for previews)
  - Local development URLs

### Frontend
- ✅ `.env.production` created with backend URLs
- ✅ API client already configured to read environment variables
- ✅ Proper fallbacks for local development

---

## 📋 Next Steps

### 1️⃣ Set Environment Variables in Vercel

#### Backend Project
Go to: https://vercel.com/hyuzukirmizis-projects/doorsmash-backend/settings/environment-variables

Add these:
```
FRONTEND_URL=https://www.udoorsmashorpass.tech
SUPABASE_URL=<your_supabase_url>
SUPABASE_KEY=<your_supabase_service_role_key>
GOOGLE_API_KEY=<your_gemini_api_key>
NUTRITION_API_BASE=https://doorsmash-backend.vercel.app
ORDERS_API_BASE=https://doorsmash-backend.vercel.app
```

#### Frontend Project
Go to: https://vercel.com/hyuzukirmizis-projects/doorsmash/settings/environment-variables

Add these:
```
VITE_API_URL=https://doorsmash-backend.vercel.app
VITE_CHATBOT_API_URL=https://doorsmash-backend.vercel.app/api/chat
VITE_SUPABASE_URL=<your_supabase_url>
VITE_SUPABASE_ANON_KEY=<your_supabase_anon_key>
```

---

### 2️⃣ Redeploy Both Projects

```powershell
# Backend
cd c:\Users\yzkrm\Desktop\Github\doorsmash\backend
vercel --prod

# Frontend
cd c:\Users\yzkrm\Desktop\Github\doorsmash\frontend
vercel --prod
```

---

### 3️⃣ Test the Integration

Open your browser console on https://www.udoorsmashorpass.tech and run:

```javascript
// Test backend health
fetch('https://doorsmash-backend.vercel.app/api/health')
  .then(r => r.json())
  .then(console.log);
// Expected: {"status": "healthy", "services": {...}}

// Test orders endpoint
fetch('https://doorsmash-backend.vercel.app/orders')
  .then(r => r.json())
  .then(console.log);
// Expected: [] or array of orders

// Test chatbot endpoint
fetch('https://doorsmash-backend.vercel.app/api/chat', {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify({
    message: 'Hello',
    user_id: 'test-user-123'
  })
})
  .then(r => r.json())
  .then(console.log);
// Expected: {"response": "...", "timestamp": "..."}
```

---

### 4️⃣ Verify Frontend-Backend Communication

1. Open your app: https://www.udoorsmashorpass.tech
2. Open DevTools → Network tab
3. Try any action that calls the API (browse meals, create order, chat, etc.)
4. Look for:
   - ✅ Status 200 (success)
   - ❌ Status 403/CORS error → Check CORS config and redeploy
   - ❌ Status 404 → Check API route exists
   - ❌ Status 500 → Check backend logs in Vercel

---

## 🎉 Success Indicators

You'll know it's working when:

1. ✅ No CORS errors in browser console
2. ✅ API requests show status 200 in Network tab
3. ✅ Data loads correctly in your frontend
4. ✅ You can browse dining hall menus
5. ✅ You can create and view orders
6. ✅ Chatbot responds to messages
7. ✅ Nutrition tracking works

---

## 🐛 If Something Doesn't Work

### CORS Errors
```
Access to fetch at 'https://doorsmash-backend.vercel.app/...' from origin 'https://www.udoorsmashorpass.tech' has been blocked by CORS policy
```

**Fix:**
- Verify environment variables are set in Vercel
- Redeploy backend after setting env vars
- Check backend logs for startup errors

### 404 Errors
```
GET https://doorsmash-backend.vercel.app/api/health 404 (Not Found)
```

**Fix:**
- Check if `/api/health` endpoint exists in `main.py`
- Verify `vercel.json` routes configuration
- Check Vercel deployment logs

### Environment Variables Not Loading
```
Error: SUPABASE_URL is not set
```

**Fix:**
- Double-check variable names in Vercel dashboard (no typos)
- Ensure variables are set for "Production" environment
- Redeploy after adding variables

---

## 📞 Get Help

If you encounter issues:

1. Check Vercel deployment logs:
   - Backend: https://vercel.com/hyuzukirmizis-projects/doorsmash-backend
   - Frontend: https://vercel.com/hyuzukirmizis-projects/doorsmash

2. Review browser console for errors

3. Test endpoints individually with curl/Postman

4. Check this documentation: `VERCEL_ENV_SETUP.md`

---

## 🚀 You're Almost There!

Just need to:
1. Set environment variables in Vercel dashboard
2. Redeploy both projects
3. Test the connection
4. Celebrate! 🎉
