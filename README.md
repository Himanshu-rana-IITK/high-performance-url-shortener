# 🚀 High-Performance URL Shortener

A production-ready URL shortening service built with **FastAPI**, **PostgreSQL**, and **Redis**, designed for **high concurrency**, **low-latency redirections**, and **asynchronous analytics tracking**. The system leverages caching, background processing, and rate limiting to ensure fast and reliable performance under heavy traffic.

---

## ✨ Features

- 🔗 Generate short URLs from long URLs
- ⚡ Sub-millisecond redirect resolution using Redis cache
- 📊 Asynchronous analytics tracking
- 🚦 IP-based rate limiting to prevent abuse
- 🗄️ PostgreSQL for persistent storage
- 🔄 Async database operations with FastAPI
- 📈 High-concurrency architecture
- 🐳 Docker support
- 🧪 Load tested with Locust

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| Backend | FastAPI |
| Database | PostgreSQL |
| Cache | Redis |
| ORM | SQLAlchemy |
| Async Runtime | AsyncIO |
| Server | Uvicorn |
| Testing | Pytest |
| Load Testing | Locust |
| Containerization | Docker |

---

## 🏗️ System Architecture

```text
                   Client
                      │
                      ▼
             FastAPI Application
                      │
        ┌─────────────┴─────────────┐
        │                           │
        ▼                           ▼
    Redis Cache               PostgreSQL
        │                           │
        └─────────────┬─────────────┘
                      ▼
          Background Analytics Worker
```

---

## 🔄 Request Flow

### URL Shortening

```text
User
 │
 ▼
POST /shorten
 │
 ▼
Generate Short Code
 │
 ▼
Store in PostgreSQL
 │
 ▼
Cache in Redis
 │
 ▼
Return Short URL
```

### URL Redirection

```text
User
 │
 ▼
GET /{short_code}
 │
 ▼
Redis Lookup
 │
 ├── Cache Hit ──► Redirect User
 │
 └── Cache Miss
       │
       ▼
Retrieve from PostgreSQL
       │
       ▼
Update Redis Cache
       │
       ▼
Redirect User
       │
       ▼
Track Analytics (Async)
```

---

## 📂 Project Structure

```text
high-performance-url-shortener/
│
├── app/
│   ├── api/
│   ├── core/
│   ├── db/
│   ├── schemas/
│   ├── services/
│   ├── workers/
│   ├── utils/
│   └── main.py
│
├── tests/
├── benchmarks/
├── docs/
├── docker/
├── requirements.txt
├── docker-compose.yml
├── .gitignore
├── LICENSE
└── README.md
```

---

## 📡 API Endpoints

### Create Short URL

```http
POST /shorten
```

Request

```json
{
    "url": "https://example.com/very/long/url"
}
```

Response

```json
{
    "short_url": "http://localhost:8000/abc123"
}
```

---

### Redirect

```http
GET /abc123
```

Returns

```
302 Redirect
```

---

### Analytics

```http
GET /analytics/{short_code}
```

Example Response

```json
{
    "clicks": 241,
    "unique_visitors": 178,
    "last_accessed": "2026-07-03T18:45:10Z"
}
```

---

## ⚙️ Installation

Clone the repository

```bash
git clone https://github.com/yourusername/high-performance-url-shortener.git
```

Move into the project directory

```bash
cd high-performance-url-shortener
```

Create a virtual environment

```bash
python -m venv venv
```

Activate the environment

Linux / macOS

```bash
source venv/bin/activate
```

Windows

```bash
venv\Scripts\activate
```

Install dependencies

```bash
pip install -r requirements.txt
```

Run the server

```bash
uvicorn app.main:app --reload
```

Open

```
http://localhost:8000/docs
```

for interactive Swagger documentation.

---

## 🐳 Docker

Build the containers

```bash
docker-compose up --build
```

---

## 🧪 Load Testing

Run Locust

```bash
locust -f benchmarks/locustfile.py
```

Open

```
http://localhost:8089
```

Configure the desired number of users and spawn rate to begin testing.

---

## 📈 Performance Results

| Metric | Value |
|---------|-------|
| Total Requests | 1614 |
| Throughput | 40+ Requests/sec |
| Failure Rate | **0%** |
| Median Response Time | **260 ms** |
| Cache | Redis |
| Analytics | Async Background Tasks |

---

## 🔐 Security Features

- IP-based rate limiting
- Input validation
- URL sanitization
- SQL injection protection
- Async request handling
- Safe database transactions

---

## 🚀 Future Improvements

- User authentication
- Custom aliases
- QR code generation
- URL expiration
- Redis Cluster support
- Kubernetes deployment
- Distributed analytics workers
- Click heatmaps
- Prometheus and Grafana monitoring

---

## 📷 Screenshots

You can place the following images inside the `docs/` folder.

```
docs/
├── architecture.png
├── workflow.png
├── database_schema.png
├── api_demo.png
└── load_testing_results.png
```

Then display them like this:

```markdown
## Architecture

![Architecture](docs/architecture.png)

## Workflow

![Workflow](docs/workflow.png)

## Load Testing

![Load Test](docs/load_testing_results.png)
```

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request for improvements and new features.

---

## 📄 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

**Himanshu Rana**

- GitHub: https://github.com/Himanshu-rana-IITK
- LinkedIn: *(Add your LinkedIn profile here)*

---

⭐ If you found this project useful, consider giving it a star!
