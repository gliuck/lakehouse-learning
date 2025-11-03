# 🏠 Lakehouse Learning

A **hands-on learning environment** for understanding modern **Data Lakehouse architecture** using industry-standard open-source tools.

## 🎯 What You'll Learn

This project provides a complete, containerized setup to explore:

- **Apache Iceberg** - Open table format with ACID transactions and time travel
- **Apache Trino** - Distributed SQL query engine
- **Apache Polaris** - REST catalog for Iceberg metadata management
- **MinIO** - S3-compatible object storage

All orchestrated through **Docker Compose** with an interactive **Jupyter notebook** that guides you through the complete data lakehouse workflow.

---

## 🚀 Quick Start

### Prerequisites

- Docker & Docker Compose installed
- Python 3.8+ (for Jupyter notebook)
- 4GB RAM available

### Launch the Environment

```bash
# Clone the repository
git clone https://github.com/gliuck/lakehouse-learning.git
cd lakehouse-learning

# Start all services
docker-compose up -d

# Wait ~30 seconds for services to initialize
docker-compose ps
```

### Open the Tutorial

```bash
# Launch Jupyter notebook
jupyter notebook new_york_taxi.ipynb
```

Or open `new_york_taxi.ipynb` directly in VS Code.

### Access Web Interfaces

| Service | URL | Credentials |
|---------|-----|-------------|
| **Trino UI** | http://localhost:8080 | - |
| **MinIO Console** | http://localhost:9001 | admin / password |
| **Polaris API** | http://localhost:8181 | - |

---

## 📚 What's Inside

The notebook (`new_york_taxi.ipynb`) walks you through:

1. **Setup** - Configure Polaris catalog and namespaces
2. **Landing Zone** - Ingest raw NYC taxi data into Iceberg
3. **Staging Zone** - Clean, validate, and transform data
4. **Curated Zone** - Create business-ready aggregations
5. **Time Travel** - Query historical data snapshots
6. **Analytics** - Run advanced SQL queries
7. **Destaging** - Export data for external consumption
8. **Visualizations** - Create charts from lakehouse data

### Architecture

```
┌─────────────────────────────────────────────┐
│       Jupyter Notebook (Trino Client)       │
│              Python + Pandas                │
└────────────────────┬────────────────────────┘
                     │ SQL queries
                     ▼
        ┌────────────────────────┐
        │   TRINO (SQL Engine)   │
        │     (Port: 8080)       │
        └────────────┬────────────┘
                     │ metadata
                     ▼
        ┌────────────────────────┐
        │   POLARIS (Catalog)    │
        │  (Port: 8181/8182)     │
        │                        │
        │  ✓ Table metadata      │
        │  ✓ Transaction logs    │
        │  ✓ Access control      │
        └─────────────┬──────────┘
                      │ S3 API
                      ▼
        ┌────────────────────────┐
        │  MinIO (Object Store)  │
        │   (Port: 9000/9001)    │
        │                        │
        │  ✓ Parquet files       │
        │  ✓ Snapshots           │
        │  ✓ Manifests           │
        └────────────────────────┘
```

---

## 📂 Project Structure

```
lakehouse-learning/
├── docker-compose.yml          # Service orchestration
├── new_york_taxi.ipynb         # Interactive tutorial
├── trino/
│   └── catalog/
│       └── iceberg.properties  # Trino catalog config
├── data/                       # Dataset storage (created at runtime)
└── exports/                    # Data export destination
```

---

## 🎓 Learning Path

This project is designed for:

- **Beginners** - Understand lakehouse fundamentals
- **Data Engineers** - Learn Iceberg, Trino, and Polaris integration
- **Data Analysts** - Practice SQL on modern table formats
- **Architects** - Study open lakehouse architecture patterns

---

## 🎓 Key Concepts

### 🧊 Apache Iceberg
- **ACID Transactions** on data lakes
- **Schema evolution** without downtime
- **Time travel**: query specific snapshots
- **Hidden partitioning**: partitions invisible to SQL

### 🔍 Trino (formerly PrestoDB)
- Distributed and parallel query engine
- Supports Iceberg, Hive, PostgreSQL, etc.
- Coordinator + Worker nodes (here: 1 coordinator)

### 📦 Polaris
- **Serverless catalog**: no Hive Metastore needed
- REST API for metadata
- OAuth2 multi-tenancy
- RBAC integration

### 🪣 MinIO
- Drop-in replacement for AWS S3
- Object-based file storage
- Versioning support
- Management console

---

## 📊 Dataset: NYC Yellow Taxi

Public dataset with 1M+ trips:
- **pickup_time**, **dropoff_time**
- **distance**, **fare_amount**, **tip_amount**
- **payment_type**, **passenger_count**
- **pickup_location_id**, **dropoff_location_id**

Perfect for learning:
- ✅ Complex SQL queries (JOINs, aggregations)
- ✅ Data cleaning and transformations
- ✅ Visualizations with Pandas/Plotly
- ✅ Query performance tuning

---


## 📚 Learning Resources

| Topic | Link |
|-------|------|
| **Apache Iceberg Docs** | https://iceberg.apache.org/ |
| **Trino Documentation** | https://trino.io/ |
| **Polaris Project** | https://github.com/apache/iceberg-polaris |
| **MinIO Docs** | https://min.io/docs/ |
| **NYC Taxi Dataset** | https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page |

---

## 🛑 Cleanup

```bash
# Stop services
docker-compose down

# Remove volumes (deletes all data)
docker-compose down -v
```

---

**Happy Learning! 🚀📊**

