# Mindfuel App (Dockerized)

A Dockerized Python application that fetches inspirational quotes and sends them via email.  
This project demonstrates containerization, environment variable management, logging, and integration with external services like PostgreSQL and Gmail SMTP.

---

## 🚀 Features
- Fetches random inspirational quotes
- Saves quotes to a log file (`logs/quote_fetched.txt`)
- Sends quotes to users via email
- Connects to PostgreSQL for persistence
- Fully containerized with Docker

---

## 🛠️ Prerequisites
- [Docker](https://docs.docker.com/get-docker/) installed
- A PostgreSQL database (either local or in a container)
- Gmail account with **App Passwords** enabled for SMTP

---

## ⚙️ Environment Variables
Create a `.env` file in the project root:

```env
# Database
PGHOST=host.docker.internal   # or container name if using Docker network
PGPORT=5432
PGUSER=postgres
PGPASSWORD=your_password
PGDATABASE=app_db

# Email
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=465
SENDER_EMAIL=your_email@gmail.com
EMAIL_PASSWORD=your_16_char_app_password
