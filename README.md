# Booking Platform API

REST API backend for a Booking Platform — built with Node.js, Express, Prisma & MySQL.
Includes JWT authentication, seed data, OpenAPI spec, and Postman test collections.

---

## Tech Stack

- Node.js + Express.js
- Prisma ORM
- MySQL
- JWT Authentication
- Winston (logging)
- Sentry (error monitoring)
- Newman (API testing)

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/aelyakoubi/booking-platform-api.git
cd booking-platform-api
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Copy `.env.example` to `.env` and fill in your own values:

```bash
cp .env.example .env
```

```env
AUTH_SECRET_KEY=your_secret_key_here
DATABASE_URL=mysql://user:password@localhost:3306/your_database_name
SHADOW_DATABASE_URL=mysql://user:password@localhost:3306/your_database_name_shadow
SENTRY_DSN=your_sentry_dsn_here
```

### 4. Generate Prisma Client

```bash
npx prisma generate
```

### 5. Push the database schema

```bash
npx prisma db push --force-reset
```

### 6. Seed the database

```bash
npm run seed
```

### 7. Start the server

```bash
npm run dev
```

Server runs on `http://localhost:3000`

---

## API Endpoints

| Resource   | Endpoint      |
| ---------- | ------------- |
| Users      | `/users`      |
| Bookings   | `/bookings`   |
| Properties | `/properties` |
| Reviews    | `/reviews`    |
| Hosts      | `/hosts`      |
| Amenities  | `/amenities`  |
| Login      | `/login`      |

Full API documentation is available in `openapi.yaml`.

---

## Running Tests

Tests are run using **Newman** (Postman CLI). The collections are located in the `postman/` folder.

### Start the server first

```bash
npm run dev
```

### Run all tests (positive + negative)

```bash
npm run test
```

Or run them separately:

```bash
npm run test-positive
npm run test-negative
```

> ⚠️ Some tests use `DELETE` endpoints and modify the database. Re-seed before re-running tests:
>
> ```bash
> npm run seed
> ```

### Postman environments

Located in `postman/environments/`. Default base URL is `http://localhost:3000`. Update if your port differs.

---

## Database

### Prisma Studio (visual database browser)

```bash
npx prisma studio
```

Opens at `http://localhost:5555`

---

## Project Structure

```
├── src/
│   ├── data/                  # Seed data (JSON)
│   │   ├── amenities.json
│   │   ├── bookings.json
│   │   ├── hosts.json
│   │   ├── properties.json
│   │   ├── reviews.json
│   │   └── users.json
│   ├── errors/
│   │   └── NotFoundError.js   # Custom error class
│   ├── middleware/
│   │   ├── auth.js            # JWT authentication
│   │   ├── errorHandler.js    # Global error handler
│   │   ├── logMiddleware.js   # Request logging
│   │   └── notFoundErrorHandler.js
│   ├── routes/
│   │   ├── amenities.js
│   │   ├── bookings.js
│   │   ├── hosts.js
│   │   ├── login.js
│   │   ├── properties.js
│   │   ├── reviews.js
│   │   └── users.js
│   ├── services/              # Business logic per resource
│   │   ├── amenities/
│   │   ├── auth/
│   │   ├── bookings/
│   │   ├── hosts/
│   │   ├── properties/
│   │   ├── reviews/
│   │   └── users/
│   ├── utils/
│   │   └── log.js
│   └── index.js               # App entry point
├── prisma/
│   ├── migrations/            # Database migration history
│   ├── schema.prisma          # Data model
│   └── seed.js                # Seed script
├── postman/
│   ├── collections/           # Positive & negative test collections
│   └── environments/          # Local environment config
├── openapi.yaml               # API documentation
├── .env.example               # Environment variable template
├── .gitignore
└── package.json
```

---

## Screenshots

![Positive API integration test](https://github.com/user-attachments/assets/1e5f9d15-4ee3-4a23-a61d-4bc3adccacb4)
![Negative API integration test](https://github.com/user-attachments/assets/1b85b179-7f3d-4448-914f-da480e75e8d8)
