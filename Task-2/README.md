# Mindfuel Dockerized App

## 📖 Overview
This project demonstrates a **multi-container application** using Docker Compose.  
It includes:
- A **Python application** that fetches quotes and sends emails.
- A **PostgreSQL database** for persistence.
- **pgAdmin** for database management.

The stack is designed to be reproducible, persistent, and easy to rebuild.

---

## 📂 Folder Structure

'''
mindfuel-dockerized-app/ 
│ 
├── Task-2/ 
│ ├── docker-compose.yml    # Docker Compose file 
│ ├── Dockerfile            # Python app container definition 
│ ├── requirements.txt      # Python dependencies 
│ ├── src/ │                # Source folder for python codes
  │ └── main.py             
  | └── active_subscriber.py 
  | └── extract_quote.py
  | └── send_email.py
  | └── database.py 
│ ├── init.sql                 # Database initialization script 
│ └── .env # Environment variables
'''

---

## ⚙️ Services

### **App**
- Runs the Python application.
- Connects automatically to the Postgres database at startup.
- Can be rebuilt easily with:
  ```bash
  docker compose up --build

Postgres (DB)
Provides persistent storage using a named Docker volume.

Initializes with init.sql on first startup.

Exposes port 5432 for external access.

pgAdmin
Web-based database management tool.

Accessible at http://localhost:5000.

Uses credentials defined in .env.

---

📝 compose.yml Highlights
Multiple services: app, postgres, pgadmin.

Ports mapped:

Postgres → 5432:5432

pgAdmin → 5000:80

Volumes:

db_data:/var/lib/postgresql/data for persistent DB storage.

./init.sql:/docker-entrypoint-initdb.d/init.sql for initialization.

Environment variables: loaded securely from .env.

Dependencies: depends_on ensures the app waits for Postgres.

---

🚀 Commands
# Build and start the stack
docker compose up --build -d

# Check running containers
docker compose ps

# View logs for the app
docker logs task-2-app-1

# Stop and remove containers + volumes
docker compose down -v

🖼️ Architecture Diagram

                +-------------------+
                |    Python App     |
                |  (task-2-app-1)   |
                +---------+---------+
                          |
                          | connects via host "postgres"
                          |
                +---------v---------+
                |   PostgreSQL DB   |
                | (task-2-postgres) |
                +---------+---------+
                          |
                          | managed via host "postgres"
                          |
                +---------v---------+
                |      pgAdmin      |
                | (task-2-pgadmin)  |
                +-------------------+

   All services communicate over the shared Docker network: mindfuel_network

Mermaid Diagram

flowchart LR
    A[Python App<br/>task-2-app-1] --> B[Postgres DB<br/>task-2-postgres-1]
    C[pgAdmin<br/>task-2-pgadmin-1] --> B

    subgraph mindfuel_network
    A
    B
    C
    end

---
✅ Verification

# Start the stack
    docker compose up --build -d

# Check containers
    docker compose ps

🧠 Notes
Postgres only runs init.sql on first database creation.
Use docker compose down -v to reset volumes if you need to re-run initialization.

Retry logic in the app ensures stable DB connections during startup.

Secrets are managed via .env for security and flexibility.

