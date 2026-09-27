# CodeAlpha_ECommerceStore

**Task 1 — Simple E-commerce Store** (CodeAlpha Full Stack Development Internship)

A full-stack e-commerce store: product listings, product details, shopping cart, order
processing, and user registration/login — built with vanilla HTML/CSS/JS on the frontend
and Node.js + Express + SQLite on the backend.

## Features
- User registration & login (JWT-based auth, hashed passwords)
- Product listing with search + category filter
- Product detail page
- Shopping cart (add / update quantity / remove)
- Order processing (checkout with shipping details, stock deducted, order history saved)
- Order history page per user
- Single server serves both the API and the frontend (no CORS setup needed)

## Tech Stack
- **Frontend:** HTML, CSS, JavaScript (no framework, no build step)
- **Backend:** Node.js, Express.js
- **Database:** SQLite via Node's built-in `node:sqlite` module (no native compiler/Visual Studio needed) — a single local file, no separate DB server required. Requires Node.js 22.5+ (24+ recommended, where it's stable with no warning).
- **Auth:** JSON Web Tokens (JWT) + bcrypt password hashing

---

## 1. Prerequisites
Install **Node.js** (v18 or newer recommended) from https://nodejs.org — this includes `npm`.
Check it's installed:
```bash
node -v
npm -v
```

## 2. Setup
Unzip the project, then open a terminal in the project folder.

```bash
cd CodeAlpha_ECommerceStore/backend
npm install
```

This installs Express, better-sqlite3, bcryptjs, jsonwebtoken, cors, and dotenv.
The database file (`store.db`) and 8 sample products are created automatically the first
time the server starts — you don't need to set up any database manually.

> The `.env` file already contains a default `JWT_SECRET` and `PORT=5000` for local testing.
> For a real deployment, change `JWT_SECRET` to a long random string.

## 3. Run the app
Still inside the `backend` folder:
```bash
npm start
```
You should see:
```
✅ Server running at http://localhost:5000
```
Open your browser at **http://localhost:5000** — the frontend and API are served from the
same address, so there's nothing else to start.

(Optional, for development with auto-restart on file changes: `npm run dev`, which uses nodemon.)

## 4. Try it out
1. Go to `http://localhost:5000` — browse products, search, filter by category.
2. Click a product → view details → **Register** an account (or log in).
3. Add items to your cart, adjust quantities on the **Cart** page.
4. Click **Proceed to Checkout**, fill in shipping name/address, **Place Order**.
5. View the order under **My Orders**.

## Project Structure
```
CodeAlpha_ECommerceStore/
├── backend/
│   ├── server.js            # Express app entry point
│   ├── db.js                 # SQLite schema + product seeding
│   ├── .env                  # PORT and JWT_SECRET
│   ├── package.json
│   ├── middleware/auth.js    # JWT auth middleware
│   └── routes/
│       ├── auth.js           # /api/auth/register, /api/auth/login
│       ├── products.js       # /api/products, /api/products/:id
│       ├── cart.js           # /api/cart (GET/POST/PUT/DELETE)
│       └── orders.js         # /api/orders (GET/POST)
├── frontend/
│   ├── index.html            # Product listing
│   ├── product.html          # Product detail
│   ├── cart.html             # Shopping cart + checkout
│   ├── login.html / register.html
│   ├── orders.html           # Order history
│   ├── css/style.css
│   └── js/                   # api.js, main.js, product.js, cart.js, orders.js, auth.js
└── README.md
```

## API Reference (for your own testing/documentation)
| Method | Endpoint             | Auth? | Description                     |
|--------|-----------------------|-------|----------------------------------|
| POST   | /api/auth/register    | No    | Create account, returns JWT     |
| POST   | /api/auth/login       | No    | Log in, returns JWT             |
| GET    | /api/products         | No    | List products (supports ?search=&category=) |
| GET    | /api/products/:id     | No    | Product details                 |
| GET    | /api/cart             | Yes   | View cart                       |
| POST   | /api/cart             | Yes   | Add item to cart                |
| PUT    | /api/cart/:id         | Yes   | Update quantity                 |
| DELETE | /api/cart/:id         | Yes   | Remove item                     |
| POST   | /api/orders           | Yes   | Place order (checkout)          |
| GET    | /api/orders           | Yes   | Order history                   |

---

## 5. Submission Steps (per CodeAlpha instructions)

1. **Create a GitHub repository** named exactly: `CodeAlpha_ECommerceStore`
2. Push this project to it:
   ```bash
   cd CodeAlpha_ECommerceStore
   git init
   git add .
   git commit -m "Task 1: Simple E-commerce Store - CodeAlpha Internship"
   git branch -M main
   git remote add origin https://github.com/<your-username>/CodeAlpha_ECommerceStore.git
   git push -u origin main
   ```
   (The included `.gitignore` already excludes `node_modules/`, the local `store.db` file,
   and `.env`, so your repo stays clean. If you want the grader to run it with zero setup,
   you may remove `.env` from `.gitignore` and commit it too, since it holds no real secret here.)
3. **Record a short screen-recording** demoing: registering/logging in, browsing products,
   adding to cart, checking out, and viewing order history. Upload it to LinkedIn, tag
   **@CodeAlpha**, and include your GitHub repo link in the post.
4. **Share your internship status** on LinkedIn tagging @CodeAlpha (per the internship instructions PDF).
5. **Submit the task** using the Submission Form shared in your CodeAlpha WhatsApp group —
   paste your GitHub repo link and LinkedIn post link there.
6. Repeat for at least one more task (2 or 3 total) to qualify for the completion certificate.

## Notes / Possible Extensions
- Product images use placeholder URLs (picsum.photos) — swap `image_url` values in `db.js`
  for your own product photos if you'd like.
- To reset the database, stop the server and delete `backend/store.db` — it will be
  recreated with fresh sample data on next start.
- Passwords are hashed with bcrypt; never stored in plain text.
- This uses SQLite for simplicity — if your mentor specifically wants MongoDB/MySQL/Postgres,
  the route logic can be adapted; ask if you'd like a version using one of those instead.
