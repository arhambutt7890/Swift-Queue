# Swift-Queue
Live doctor queues, advance booking, QR queue passes and admin-verified doctors. A Laravel + MySQL healthcare queue management platform.
# SwiftQueue

Smart healthcare queue and appointment management for doctors and patients, built with Laravel and MySQL.

Patients join a doctor's live queue or book an advance slot, follow their turn in real time, and arrive when it counts. Doctors manage their own schedule and queue, and admins verify doctors before they go live.

## Features

**Available now**
- Role-based authentication for patients, doctors and admins
- Separate patient and doctor registration, with the user and profile created in one transaction
- Admin dashboard with doctor verification (approve and revoke)
- Server-side role protection on every route
- Dark, responsive UI built on a custom design system
- Specialty categories seeded for doctor registration

**Planned**
- Doctor clinic profile with Google Maps location, average service time and queue limit
- Doctor-defined available days and time slots
- Live queue with wait-time estimates
- Advance appointment booking
- 40% prepayment with a payment verification workflow
- QR queue pass
- Notifications and patient reviews
- Automated tests

## Tech Stack

| Layer | Technology |
| --- | --- |
| Backend | PHP 8.2, Laravel 12 |
| Database | MySQL |
| Frontend | Blade, Tailwind CSS, Alpine.js |
| Tooling | Vite, Laravel Breeze, Composer, npm |

## Requirements

- PHP 8.2 or higher
- Composer
- Node.js and npm
- MySQL (XAMPP works well on Windows)

## Installation

```bash
git clone https://github.com/arhambutt7890/swiftqueue.git
cd swiftqueue

composer install
npm install

cp .env.example .env
php artisan key:generate
```

Create an empty MySQL database named `swiftqueue`, then set these values in `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=swiftqueue
DB_USERNAME=root
DB_PASSWORD=

ADMIN_NAME="SwiftQueue Admin"
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD="choose-a-strong-password"
```

Run the migrations and seeders:

```bash
php artisan migrate --seed
```

This creates the tables, the specialty categories and the admin account from `.env`.

## Running Locally

Use two terminals:

```bash
php artisan serve
npm run dev
```

Then open `http://127.0.0.1:8000`.

## User Roles

| Role | How it is created | Access |
| --- | --- | --- |
| Patient | Public registration | Patient dashboard |
| Doctor | Public registration, unverified until approved by an admin | Doctor dashboard |
| Admin | Seeded from `.env` only, never through registration | Admin dashboard and doctor verification |

## Project Structure

```
app/
  Enums/UserRole.php            Role definitions
  Http/Controllers/             Auth, Admin, Doctor and Patient controllers
  Http/Middleware/              EnsureUserHasRole
  Http/Requests/Auth/           Registration validation
  Models/                       User, Doctor, Patient, Category
  Services/                     Business logic (registration, doctor verification)
database/
  migrations/
  seeders/                      Categories and admin account
resources/
  css/app.css                   Design system
  views/                        Blade views and UI components
routes/web.php
```

## Security Notes

- `role` is not mass-assignable and is never read from request input
- Doctor verification, ratings and review counts can only be changed by server-side services
- Admin credentials come from `.env` and are never committed
- Registration and verification run inside database transactions

## Roadmap

Development follows a phased plan. The next phase is the doctor clinic profile, followed by availability scheduling, the live queue engine, booking, payments and notifications.

## Author

Built by Muhammad Arham Butt.
