# Imagify - Image Generation App

A full-stack MERN application for generating AI images using ClipDrop API with Razorpay payment integration.

## Tech Stack

**Frontend:**

- React 19
- Vite
- Tailwind CSS
- React Router
- Axios
- Framer Motion

**Backend:**

- Node.js + Express
- MongoDB
- JWT Authentication
- Bcrypt
- Razorpay

**APIs:**

- ClipDrop (Text-to-Image)
- Razorpay (Payment Processing)

## Features

- User authentication (Sign up/Login)
- AI image generation from text prompts
- Credit-based system
- Payment integration with Razorpay
- Responsive UI

## Local Development

### Prerequisites

- Node.js 16+
- MongoDB Atlas account
- ClipDrop API key
- Razorpay account

### Setup

1. Clone the repository

```bash
git clone <your-repo-url>
cd imagify
```

2. **Backend Setup**

```bash
cd server
npm install
```

Create `.env` in `server/`:

```
MONGO_URL=mongodb+srv://username:password@cluster.mongodb.net/imagify
JWT_SECRET=your_jwt_secret
CLIPDROP_API=your_clipdrop_api_key
RAZORPAY_KEY_ID=your_razorpay_key
RAZORPAY_KEY_SECRET=your_razorpay_secret
CURRENCY=INR
PORT=4000
```

Run server:

```bash
npm run server
```

3. **Frontend Setup**

```bash
cd client
npm install
```

Create `.env` in `client/`:

```
VITE_BACKEND_URL=http://localhost:4000
VITE_RAZORPAY_KEY_ID=your_razorpay_key
```

Run client:

```bash
npm run dev
```

Visit `http://localhost:5174`

## Deployment

### Option 1: Render (Recommended)

**Backend:**

1. Push code to GitHub
2. Create New Web Service on [render.com](https://render.com)
3. Connect GitHub repo
4. Add environment variables
5. Build: `npm install`
6. Start: `npm start`

**Frontend:**

1. Create Static Site on Render
2. Build: `npm run build`
3. Publish dir: `dist`
4. Set `VITE_BACKEND_URL` to your Render backend URL

### Option 2: Vercel (Frontend) + Railway/Render (Backend)

**Frontend on Vercel:**

- Connect GitHub
- Build: `npm run build`
- Output: `dist`

**Backend on Railway/Render:**

- Follow backend deployment steps above

### Option 3: Heroku (if available)

Use Heroku CLI or GitHub integration with similar environment setup.

## Project Structure

```
imagify/
├── client/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── context/
│   │   └── assets/
│   ├── package.json
│   └── vite.config.js
├── server/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middlewares/
│   ├── config/
│   ├── package.json
│   └── server.js
└── .gitignore
```

## Environment Variables

### Server (.env)

- `MONGO_URL` - MongoDB connection string
- `JWT_SECRET` - Secret key for JWT tokens
- `CLIPDROP_API` - ClipDrop API key
- `RAZORPAY_KEY_ID` - Razorpay public key
- `RAZORPAY_KEY_SECRET` - Razorpay secret key
- `CURRENCY` - Currency code (INR)
- `PORT` - Server port (default: 4000)

### Client (.env)

- `VITE_BACKEND_URL` - Backend API URL
- `VITE_RAZORPAY_KEY_ID` - Razorpay public key

## API Endpoints

### User Routes

- `POST /api/user/register` - Register user
- `POST /api/user/login` - Login user
- `GET /api/user/credits` - Get user credits (protected)
- `POST /api/user/pay-razor` - Create Razorpay order (protected)
- `POST /api/user/verify-razor` - Verify payment

### Image Routes

- `POST /api/image/generate-image` - Generate image (protected)

## License

MIT
