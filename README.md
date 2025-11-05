## Sharebnb

A full‑stack Airbnb‑style web application for discovering, listing, and booking stays. The project is organized as a two‑app workspace:

- `front-sharebnb-main/`: React + Vite single‑page application
- `back-sharebnb-f-backtofront/`: Node.js + Express API with MongoDB, Socket.IO, and email/workflow integrations


### Features
- **Browse stays**: rich catalog with filters, galleries, amenities, and maps
- **Booking flow**: date range picking, guest selection, order creation
- **Authentication**: login/signup with encrypted tokens
- **Reviews**: add and view reviews per stay
- **Realtime**: Socket.IO for live updates and messaging hooks
- **Email & workflows**: order confirmation emails and Upstash Workflows integration
- **Responsive UI**: mobile and desktop adaptive layout


### Tech Stack
- **Frontend**: React 18, Vite, React Router, Redux + Thunk, MUI, Day.js/Date‑Fns, TanStack Table, Framer Motion, Recharts, Socket.IO Client
- **Backend**: Node.js, Express, MongoDB (native driver), Socket.IO, Nodemailer, Upstash Workflow


### Repository Structure
```
sharebnb/
  back-sharebnb-f-backtofront/   # Express API server
  front-sharebnb-main/           # React SPA client
```


### Quick Start

Run backend and frontend in two terminals.

1) Backend (API server)
```
cd back-sharebnb-f-backtofront
npm install

# Create .env (see Environment Variables below), then:
npm run dev        # runs on PORT (default 3030)
```

2) Frontend (React app)
```
cd front-sharebnb-main
npm install
npm run dev        # Vite dev server on 5173 by default
```

Open the app at http://localhost:5173


### Environment Variables

Backend (`back-sharebnb-f-backtofront/.env`):
```
# Server
PORT=3030
NODE_ENV=development

# Database
MONGO_URL=mongodb://127.0.0.1:27017
DB_NAME=sharebnb

# Auth token encryption
SECRET=replace-with-strong-secret

# Email (optional if using email features)
SMTP_HOST=...
SMTP_PORT=...
SMTP_USER=...
SMTP_PASS=...

# Upstash/QStash/Workflow (optional if using workflows)
UPSTASH_WORKFLOW_URL=...
UPSTASH_TOKEN=...
```

Frontend (`front-sharebnb-main/.env` — optional):
```
# When you want the frontend to call a locally running backend
VITE_LOCAL=true
```


### Scripts

Backend (`back-sharebnb-f-backtofront/package.json`):
- `npm run dev`: start server (Node)
- `npm run start` / `npm run server:dev`: start with nodemon
- `npm run server:prod` / `server:prod:mac`: production mode

Frontend (`front-sharebnb-main/package.json`):
- `npm run dev`: Vite dev server
- `npm run build`: production build
- `npm run preview`: preview production build


### API Overview
- `POST   /api/auth/login`
- `POST   /api/auth/signup`
- `GET    /api/user/:id`
- `GET    /api/stay`
- `GET    /api/stay/:id`
- `POST   /api/order`
- `GET    /api/review?stayId=...`
- `POST   /api/review`
- `POST   /api/workflows/*` (workflow triggers)

Notes:
- CORS is enabled in development for `http://localhost:5173` and related ports.
- Static assets are served from `public/` in production mode.


### Notable Implementation Details
- **MongoDB connection**: configured via `config/dev.js` and `config/prod.js`. The app selects config by `NODE_ENV` and uses `MONGO_URL` / `DB_NAME`.
- **Auth**: password hashing with `bcrypt`; encrypted login tokens using `cryptr` and `SECRET`.
- **Sockets**: `Socket.IO` initialized in the server and consumed by the frontend client.
- **Email**: Nodemailer setup for sending order confirmations (see `utils/order-confirmation-template.js`).
- **Workflows**: Upstash Workflows can orchestrate tasks such as sending confirmations.


### Development Tips
- Ensure MongoDB is running locally or provide a remote connection string.
- Use separate terminals for API and client to keep logs readable.
- If changing ports, update frontend HTTP service base URL as needed.


### Screenshots (sample assets in repo)
You can replace these with your own screenshots:

![Home](front-sharebnb-main/src/assets/imgs/home-airbnb.png)
![Explore](front-sharebnb-main/src/assets/imgs/near-by.png)


### Production Build

1) Build the frontend
```
cd front-sharebnb-main
npm run build
```

2) Serve built assets from backend (copy or configure your CI/CD to place the frontend `dist/` into `back-sharebnb-f-backtofront/public/`). The backend already serves `public/index.html` in production.


### License
This repository is for learning and demonstration purposes.
