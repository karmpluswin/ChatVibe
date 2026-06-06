# ChatVibe

> Real-time chat app with 1-on-1 & group messaging, emoji reactions, file sharing, typing indicators, and OAuth, built with Next.js 14, Socket.io, MongoDB & Framer Motion.

**Live demo:** [`ChatVibe`](https://chatvibe-online.vercel.app) &nbsp;

---

## Tech Stack

**Frontend** — Next.js 14 (App Router), TypeScript, Tailwind CSS, Framer Motion, Zustand, TanStack Query, NextAuth.js v5, React Hook Form, Zod

**Backend** — Socket.io on Render, MongoDB with Mongoose, Upstash Redis, Cloudinary, bcryptjs

---

## Features

- Real-time messaging powered by Socket.io
- 1-on-1 and group conversations
- Live message deletion and emoji reactions without page refresh
- Image and file sharing via Cloudinary
- Typing indicators with animated dots
- Online and offline status tracking
- Read receipts with double checkmarks
- Unread message badges per conversation
- Tab filters for All Chats, Groups, and Unread
- Authentication via email/password, Google, and GitHub OAuth
- Dark and light theme toggle
- Responsive design for mobile and desktop
- Drag and drop file uploads

---

## Project Structure

```
chatvibe/
├── app/
│   ├── (auth)/                  # Login and register pages
│   ├── (main)/                  # Protected app pages
│   │   ├── chat/                # Chat pages
│   │   ├── contacts/            # Find people and groups
│   │   ├── settings/            # User settings
│   │   └── profile/             # User profile
│   └── api/                     # REST API routes
│       ├── auth/                # NextAuth handlers and register
│       ├── conversations/       # Conversation CRUD and seen tracking
│       ├── messages/            # Message CRUD and reactions
│       ├── users/               # User search and updates
│       └── upload/              # Cloudinary file upload
├── components/
│   ├── auth/                    # Login and register forms
│   ├── chat/                    # Chat header, bubbles, input, typing
│   ├── sidebar/                 # Sidebar, conversation list and items
│   └── modals/                  # Create group modal
├── server/
│   └── index.ts                 # Socket.io server entry point
├── models/                      # Mongoose schemas
├── lib/                         # Database, auth, Redis, Cloudinary, utils
├── providers/                   # React context providers
├── store/                       # Zustand state stores
├── hooks/                       # Custom React hooks
└── types/                       # TypeScript type definitions
```

---

## Local Development

### Prerequisites

- Node.js 18+
- MongoDB Atlas account
- Cloudinary account
- Upstash Redis account

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/chatvibe.git
cd chatvibe
npm install --legacy-peer-deps
```

### 2. Configure environment variables

Create `.env.local` in the root directory:

```env
# Database
MONGODB_URI=your_mongodb_atlas_connection_string

# NextAuth
NEXTAUTH_SECRET=your_random_secret_min_32_chars
NEXTAUTH_URL=http://localhost:3000

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# GitHub OAuth
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Upstash Redis
UPSTASH_REDIS_REST_URL=your_upstash_url
UPSTASH_REDIS_REST_TOKEN=your_upstash_token

# Socket Server
NEXT_PUBLIC_SOCKET_URL=http://localhost:3001
```

### 3. Run the dev servers

```bash
# Terminal 1
npm run dev:next

# Terminal 2
npm run dev:socket
```

Open http://localhost:3000.

---

## Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Run Next.js and socket server together |
| `npm run dev:next` | Next.js only |
| `npm run dev:socket` | Socket server only with ts-node |
| `npm run build` | Build Next.js for production |
| `npm run build:socket` | Compile socket server TypeScript to `dist/` |
| `npm run start:socket` | Run the compiled socket server |
| `npm run lint` | Run ESLint |

---

## Deployment

### Frontend on Vercel

1. Push the repo to GitHub and import it on vercel.com
2. Add all environment variables from `.env.local`
3. Set `NEXTAUTH_URL` to your Vercel production domain
4. Set `NEXT_PUBLIC_SOCKET_URL` to your Render socket server URL
5. Deploy

### Socket Server on Render

```
Build Command:  npm ci && npm run build:socket
Start Command:  npm run start:socket
```

`PORT` is injected automatically by Render — no extra config needed.

### MongoDB Atlas

Go to Network Access and add `0.0.0.0/0` so both Vercel and Render can connect.

### OAuth Callback URLs

After deploying, update your OAuth apps:

**Google Console — Authorized Redirect URIs:**
```
https://your-app.vercel.app/api/auth/callback/google
```

**GitHub OAuth App — Callback URL:**
```
https://your-app.vercel.app/api/auth/callback/github
```

---

## Database Schemas

**User** — name, email, hashed password, avatar, bio, online status, friends list, settings

**Conversation** — participants, group info, last message reference, timestamps

**Message** — sender, content, type (text/image/file), reactions, read receipts, soft delete flag

**FriendRequest** — sender, receiver, status (pending/accepted/rejected)

---

## Free Services Used

| Service | Purpose | Free Tier |
|---------|---------|-----------|
| Vercel | Frontend hosting | Unlimited deployments |
| Render | Socket.io server | 750 hours/month |
| MongoDB Atlas | Database | 512 MB storage |
| Cloudinary | Image and file storage | 25 GB |
| Upstash Redis | Online status caching | 10,000 requests/day |

---

## License

MIT — feel free to use this as a learning reference or as a base for your own project.

---

Built by Karmjeet Chauhan.
