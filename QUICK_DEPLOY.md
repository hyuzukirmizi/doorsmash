# ⚡ Quick Reference - Copy & Paste Commands

## 🎯 Vercel Environment Variables

### 📦 Backend Project
**Go to:** https://vercel.com/hyuzukirmizis-projects/doorsmash-backend/settings/environment-variables

**Copy and paste these** (update with your actual keys):

```
FRONTEND_URL=https://www.udoorsmashorpass.tech
SUPABASE_URL=https://btevtyamuxysdmenjsdi.supabase.co
SUPABASE_KEY=your_supabase_service_role_key_here
GOOGLE_API_KEY=your_google_gemini_api_key_here
NUTRITION_API_BASE=https://doorsmash-backend.vercel.app
ORDERS_API_BASE=https://doorsmash-backend.vercel.app
```

> ⚠️ **Important:** Use your **service role key** for SUPABASE_KEY (not the anon key)

---

### 🎨 Frontend Project
**Go to:** https://vercel.com/hyuzukirmizis-projects/doorsmash/settings/environment-variables

**Copy and paste these:**

```
VITE_API_URL=https://doorsmash-backend.vercel.app
VITE_CHATBOT_API_URL=https://doorsmash-backend.vercel.app/api/chat
VITE_SUPABASE_URL=https://btevtyamuxysdmenjsdi.supabase.co
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImJ0ZXZ0eWFtdXh5c2RtZW5qc2RpIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjI1NTkzNjYsImV4cCI6MjA3ODEzNTM2Nn0.OAthz4oXewZpelvEn-ogSmpWW6q6o6erBGeRJJSzAwQ
```

> ✅ **Note:** Frontend uses the **anon key** (already filled in)

---

## 🚀 Deploy Commands

```powershell
# Commit and push to trigger auto-deployment
git add .
git commit -m "Configure Vercel deployment with CORS and env vars"
git push

# Or manually deploy
cd frontend
vercel --prod

cd ..\backend
vercel --prod
```

---

## 🧪 Test in Browser Console

**Visit:** https://www.udoorsmashorpass.tech

**Open Console** (F12) and paste:

```javascript
// Test 1: Health Check ✅
fetch('https://doorsmash-backend.vercel.app/api/health')
  .then(r => r.json())
  .then(d => console.log('✅ Health:', d));

// Test 2: Orders Endpoint ✅
fetch('https://doorsmash-backend.vercel.app/orders')
  .then(r => r.json())
  .then(d => console.log('✅ Orders:', d));

// Test 3: Chatbot ✅
fetch('https://doorsmash-backend.vercel.app/api/chat', {
  method: 'POST',
  headers: {'Content-Type': 'application/json'},
  body: JSON.stringify({message: 'test', user_id: 'test'})
})
  .then(r => r.json())
  .then(d => console.log('✅ Chatbot:', d));
```

**Expected Results:**
- ✅ No CORS errors
- ✅ Status 200 responses
- ✅ JSON data returned

---

## 📋 What Files Changed

| File | Status |
|------|--------|
| `backend/main.py` | ✏️ Updated CORS |
| `backend/chatbot_api.py` | ✏️ Updated CORS |
| `frontend/.env.production` | ➕ Created |

---

## ⏱️ Time to Deploy: ~5 minutes

1. ⏰ **2 min** - Add env vars to Vercel (both projects)
2. ⏰ **1 min** - Commit and push changes
3. ⏰ **2 min** - Wait for deployment + test

---

## 🎯 Success Checklist

After deployment, verify:

- [ ] No CORS errors in browser console
- [ ] Network tab shows status 200 for API calls
- [ ] Can browse dining hall menus
- [ ] Can create and view orders
- [ ] Chatbot responds to messages
- [ ] Profile page loads correctly

---

## 🆘 If Something Breaks

### CORS Error?
```
❌ Access blocked by CORS policy
```
**Fix:** 
1. Check env vars are set in Vercel
2. Redeploy backend: `vercel --prod`

### 404 Error?
```
❌ 404 Not Found
```
**Fix:** 
1. Verify endpoint exists in backend
2. Check Vercel deployment logs

### Env Vars Not Loading?
```
❌ SUPABASE_URL is not set
```
**Fix:** 
1. Verify no typos in variable names
2. Redeploy after adding vars
3. Check "Production" scope is selected

---

## 📞 Need Help?

1. **Deployment Logs:** Vercel dashboard → Deployments → View Logs
2. **Browser Console:** F12 → Console tab
3. **Network Tab:** F12 → Network tab
4. **Documentation:** See `DEPLOYMENT_CHECKLIST.md`

---

## 🎉 You're Ready!

Everything is configured. Just:
1. Set environment variables ⬆️
2. Deploy 🚀
3. Test 🧪
4. Celebrate! 🎊
