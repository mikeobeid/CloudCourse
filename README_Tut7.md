# 🐅 HW2_Tiger – Microservices Search Engine

HW2_Tiger is a microservices-based search engine developed for a cloud computing course.  
It features document indexing, logical search (AND/OR), result ranking, and modular services, all implemented in a simulated microservices architecture using Python.

---

## 📦 Architecture Overview

This system is designed following a **microservices pattern**, with each class functioning as a service.

| Service         | Description                                                           |
|----------------|-----------------------------------------------------------------------|
| `IndexService` | Manages documents and builds an inverted keyword index                |
| `QueryService` | Parses user search terms, supports logical operators, scores results  |
| `ResultService`| Formats search results and ranks them based on relevance              |

Each service is implemented as an independent Python class for modularity and clarity.

---

## 🛠️ Services Documentation

### `IndexService`
```python
add_document(doc: dict) → dict
get_document(doc_id: str) → dict
search_word(word: str) → List[str]
```

### `QueryService`
```python
create_query(query_data: dict) → dict
```
- `query_data` fields:
  - `terms`: list of keywords
  - `operator`: logical operator – 'AND' or 'OR'

### `ResultService`
```python
format_results(query_id: str) → dict
```
- Returns a ranked list of formatted results.

---

## 💡 Example Usage

```python
# Add documents
index_service.add_document({'title': 'MQTT Overview', 'content': 'MQTT is a lightweight messaging protocol'})
index_service.add_document({'title': 'IoT and MQTT', 'content': 'IoT devices use MQTT for communication'})

# Query
query = query_service.create_query({'terms': ['mqtt', 'protocol'], 'operator': 'OR'})
results = result_service.format_results(query['id'])

# Output
for r in results['formatted_results']:
    print(f"[{r['score']}] {r['title']} → {r['snippet']}")
```

---

## ✅ Test Results

Tests confirmed:
- Correct handling of AND/OR logic
- Accurate keyword frequency scoring
- Clean document ranking output
- Supports any number of documents
- Functional in a Colab notebook environment

---

## ☁️ Serverless Architecture (Bonus)

HW2_Tiger can be converted into a **serverless architecture** using cloud FaaS (Function as a Service) like **Google Cloud Functions** or **AWS Lambda**.

| Function Name     | Role                      | Trigger Type     |
|------------------|---------------------------|------------------|
| `add_document()`  | Index content             | HTTP / PubSub    |
| `search_query()`  | Process queries           | HTTP             |
| `format_results()`| Format and return results | HTTP             |

Each function would handle one job and scale independently, improving fault tolerance and scalability.

---

## 📂 Project Structure

```
HW2_Tiger/
│
├── index_service.py
├── query_service.py
├── result_service.py
├── main.py
└── README.md
```

---

## 📜 License

This project was built for educational use and demonstration in the Braude College cloud computing course.
