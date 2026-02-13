OPEN-DROID

OPEN-DROID is an ASGI-based backend system built with Django and Uvicorn.
It supports:

WebSockets

Background task processing using Celery

Scheduled jobs using Celery Beat

Redis as message broker

ASGI deployment

🚀 Project Setup Guide
1️⃣ Clone the Repository
git clone https://github.com/albertthomas2205/OPEN-DROID

2️⃣ Create & Activate Virtual Environment
Windows
python -m venv venv
venv\Scripts\activate

Linux / WSL
python3 -m venv venv
source venv/bin/activate

3️⃣ Install Dependencies
pip install -r requirements.txt

🧰 Redis Setup (Port 6380)

Redis is required for Celery background tasks.

Install Redis (Linux / WSL)
sudo apt update
sudo apt install redis-server

Start Redis on Port 6380
redis-server --port 6380


Make sure your Django settings use:

CELERY_BROKER_URL = "redis://127.0.0.1:6380/0"

🚀 Run ASGI Server (Port 8000)
uvicorn asgi_uk_medical_bot.asgi:application --host 0.0.0.0 --port 8000


Access in browser:

http://localhost:8000


Access from LAN:

http://<your-ip>:8000

⚙️ Run Celery Worker

Open a new terminal (inside project root):

celery -A asgi_uk_medical_bot worker --loglevel=info

⏰ Run Celery Beat (Scheduler)

Open another terminal:

celery -A asgi_uk_medical_bot beat --loglevel=info

🔥 Optional: Run Worker + Beat Together (Development Only)
celery -A asgi_uk_medical_bot worker --beat --loglevel=info


⚠️ Not recommended for production.

✔ Full Setup Summary
Step	Action
1	Clone repository
2	Create & activate virtual environment
3	Install dependencies
4	Start Redis (port 6380)
5	Run ASGI server (port 8000)
6	Run Celery worker
7	Run Celery beat
🏗 Architecture Overview

ASGI Server → Uvicorn

Background Tasks → Celery

Task Scheduler → Celery Beat

Message Broker → Redis (Port 6380)

Real-time Communication → WebSockets
