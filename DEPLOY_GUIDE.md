# Complete Deployment Guide for Imagify

## Summary of Deployed Files

✅ **Deployment configuration files created:**

- `.gitignore` - Excludes node_modules and sensitive files
- `DEPLOYMENT.md` - Complete project documentation
- `.github/workflows/ci-cd.yml` - GitHub Actions CI/CD pipeline
- `server/Procfile` - Heroku/Render server configuration
- `server/render.yaml` - Render.com specific configuration
- `client/vercel.json` - Vercel deployment configuration

---

## Option 1: Deploy to Render (Recommended ⭐)

### Step 1: Push to GitHub

1. If you don't have a GitHub repo yet, create one:
   - Go to [github.com/new](https://github.com/new)
   - Create a new repository (e.g., `imagify`)
   - Don't initialize with README (we have one)

2. Push your code:

```bash
cd C:\Users\ASUS\OneDrive\Desktop\imagify
git remote add origin https://github.com/YOUR_USERNAME/imagify.git
git branch -M main
git push -u origin main
```

### Step 2: Deploy Backend to Render

1. Go to [render.com](https://render.com) and sign up
2. Click **New +** → **Web Service**
3. Connect your GitHub repository
4. Fill in the details:
   - **Name**: `imagify-api` (or any name)
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Root Directory**: `server`

5. Add Environment Variables:
   - Click **Add Environment Variable** for each:
     ```
     MONGO_URL=mongodb+srv://username:password@cluster.mongodb.net/imagify
     JWT_SECRET=your_secure_secret_key_here
     CLIPDROP_API=your_clipdrop_api_key
     RAZORPAY_KEY_ID=your_razorpay_key_id
     RAZORPAY_KEY_SECRET=your_razorpay_secret
     CURRENCY=INR
     PORT=4000
     ```

6. Click **Create Web Service**
7. Wait for deployment (2-5 minutes)
8. Copy the URL (e.g., `https://imagify-api.onrender.com`)

### Step 3: Deploy Frontend to Vercel or Render

**Option A: Vercel (Recommended for frontend)**

1. Go to [vercel.com](https://vercel.com) and sign up with GitHub
2. Click **Import Project**
3. Select your `imagify` repository
4. Configure:
   - **Framework Preset**: Vite
   - **Root Directory**: `client`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`

5. Add Environment Variables:
   - `VITE_BACKEND_URL=https://imagify-api.onrender.com` (use your Render URL)
   - `VITE_RAZORPAY_KEY_ID=your_razorpay_key_id`

6. Click **Deploy**

**Option B: Render Static Site**

1. In Render Dashboard, click **New +** → **Static Site**
2. Connect your GitHub repo
3. Configure:
   - **Name**: `imagify-client`
   - **Build Command**: `cd client && npm run build`
   - **Publish Directory**: `client/dist`

4. Add Environment Variables:
   - Same as above

5. Deploy

---

## Option 2: Deploy Backend to Railway + Frontend to Vercel

### Backend on Railway:

1. Go to [railway.app](https://railway.app)
2. Click **New Project** → **Deploy from GitHub**
3. Select your repository
4. Configure:
   - **Root Directory**: `server`
   - Add Environment Variables (same as above)

5. Railway will auto-detect and deploy

### Frontend on Vercel:

- Follow the Vercel steps above

---

## Option 3: Heroku Deployment (Legacy)

⚠️ **Note**: Heroku's free tier has ended, but you can still deploy paid apps.

If using Heroku, install Heroku CLI and run:

```bash
heroku login
heroku create imagify-api
git push heroku main
heroku config:set MONGO_URL=...
# etc for other env vars
```

---

## After Deployment

### 1. Update Frontend Environment

Once backend is deployed, update your client `.env`:

```
VITE_BACKEND_URL=https://your-deployed-backend-url.com
VITE_RAZORPAY_KEY_ID=your_razorpay_key_id
```

Then redeploy frontend.

### 2. Test Your Application

1. Visit your deployed frontend URL
2. Create an account (should save to MongoDB)
3. Try generating an image
4. Test payment flow

### 3. Monitor & Maintain

- **Render**: Dashboard shows logs and metrics
- **Vercel**: Analytics tab shows performance
- **Check logs** regularly for errors

---

## Troubleshooting

### Backend not connecting to MongoDB?

- Verify `MONGO_URL` is correct
- Check MongoDB Atlas IP whitelist (add `0.0.0.0/0`)

### Images not generating?

- Verify `CLIPDROP_API` key is correct
- Check ClipDrop API rate limits

### Payment not working?

- Verify `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET`
- Test in sandbox mode first

### Frontend build failing?

- Check `VITE_BACKEND_URL` is set correctly
- Verify `npm run build` works locally first

---

## Environment Variables Reference

### Server (.env)

```
MONGO_URL=mongodb+srv://user:pass@cluster.mongodb.net/imagify
JWT_SECRET=your_random_secret_string_min_32_chars
CLIPDROP_API=your_api_key_from_clipdrop
RAZORPAY_KEY_ID=rzp_test_or_live_key_id
RAZORPAY_KEY_SECRET=your_razorpay_secret
CURRENCY=INR
PORT=4000
```

### Client (.env)

```
VITE_BACKEND_URL=https://your-backend-url.com
VITE_RAZORPAY_KEY_ID=rzp_test_or_live_key_id
```

---

## Next Steps After Deployment

1. ✅ Set up custom domain (optional)
2. ✅ Enable HTTPS (automatic on Render/Vercel)
3. ✅ Set up monitoring/alerts
4. ✅ Create backup strategy for MongoDB
5. ✅ Set up CI/CD for auto-deployment on push

---

## Support

For issues:

- **Render Support**: support.render.com
- **Vercel Support**: vercel.com/support
- **MongoDB**: docs.mongodb.com

Good luck! 🚀
