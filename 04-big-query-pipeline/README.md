# Cloud Data Pipeline & Performance Validation
**Tech Stack:** Google Cloud Platform (GCS, BigQuery), Apache JMeter, BlazeMeter.

## 🎯 Project Objective
This project demonstrates an end-to-end data engineering workflow: ingesting raw CSV data into a cloud data warehouse (BigQuery) and performing high-concurrency load testing to ensure system reliability and performance monitoring.

---

## 🏗 Phase 1: Data Ingestion & Transformation
I established a robust "Source-to-Sink" pipeline to move data from Google Cloud Storage into a production-ready BigQuery table.

* **Source Data:** `sample_data.csv` (Standardized date formats to ISO 8601).
* **Automation:** Configured **BigQuery Data Transfer Service** using the **"Mirror/Overwrite"** preference.
* **Why Mirror?** This ensures data idempotency—every run replaces the table with the exact 5-row source file, preventing data duplication and maintaining a "Single Source of Truth."
* **Schema Strategy:** Utilized BigQuery's **Auto-detect** feature to map CSV columns to appropriate SQL data types.

---

## 🚀 Phase 2: Performance Testing (JMeter + BlazeMeter)
To validate the architecture's ability to handle concurrent traffic, I designed and executed a cloud-based stress test.

* **Scripting:** Developed a custom `.jmx` script in **Apache JMeter** featuring a **Thread Group** with 10 concurrent users and a 5-minute sustained duration.
* **Troubleshooting & Implementation:**
    * **Initial Issue:** Enountered a `java.net.ConnectException` (Connection Refused) and `UserProjectAccountProblem`. Diagnostics revealed a GCP billing verification hold on the public storage endpoint.
    * **The Debug Process:** Identified that the default **Java implementation** in JMeter was attempting to resolve DNS via a local loopback (`127.0.0.1`) within the BlazeMeter engine environment.
    * **The Workaround:** To validate the performance testing logic without delay, I pivoted the target to a stable public endpoint (`bing.com`) and switched the sampler to the **HttpClient4** implementation.
* **Validation:** Implemented **Response Assertions** to ensure a 100% success rate during the 5-minute peak load.

---

## 📊 Evidence of Success

| Component | Status | Verification Detail |
| :--- | :--- | :--- |
| **BigQuery Table** | ✅ Success | Preview tab confirms exactly 5 rows of cleaned data. |
| **Data Transfer** | ✅ Success | Transfer logs show "Succeeded" status using WRITE_TRUNCATE. |
| **Load Test** | ✅ Success | BlazeMeter Timeline Report shows stable Hits/sec and 0% Error Rate. |

---

## 🛠 Lessons Learned
* **Data Idempotency:** The importance of using `WRITE_TRUNCATE` in automated transfers to maintain data integrity across multiple runs.
* **Network Debugging:** Gained experience in reading JMeter stack traces to identify DNS resolution issues and proxy conflicts in cloud-based testing engines.
* **Cloud Infrastructure:** Navigated GCP billing IAM permissions and "Public Access" settings for GCS object delivery.

---

## 📂 Project Structure
* `/scripts`: Contains the `gcp_load_test.jmx` file.
* `/assets`: Screenshots of BigQuery, Data Transfer logs, and BlazeMeter graphs.
* `README.md`: Project documentation and troubleshooting report.
