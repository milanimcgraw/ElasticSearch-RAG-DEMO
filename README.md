# ElasticSearch RAG DEMO

## ⚙️ Project Overview          
This repository demonstrates a lightweight Retrieval-Augmented Generation (RAG) pipeline applied to structured FAQ data. It uses [Elasticsearch](https://github.com/elastic/elasticsearch/tree/main) for keyword-based document retrieval, [Docker](https://www.docker.com/) to run Elasticsearch locally, and [OpenAI’s GPT-4o](https://openai.com/gpt-4o) as the LLM for final answer generation. Elasticsearch is a free and open source, distributed, RESTful search engine.

## ⚙️ Elasticsearch

Elasticsearch is a distributed search and analytics engine, scalable data store, and vector database optimized for speed and relevance on production-scale workloads. Elasticsearch is the foundation of Elastic's open Stack platform. Search in near real-time over massive datasets, perform vector searches, and integrate with generative AI applications.

> To access information on [machine learning innovations](https://www.elastic.co/search-labs) and [Lucene contributions from Elastic](https://www.elastic.co/search-labs), more information can be found in Elastic’s [Search Labs](https://www.elastic.co/search-labs) and [product page](https://www.elastic.co/products/elasticsearch).

### Use cases
- [Retrieval Augmented Generation (RAG)](https://www.elastic.co/blog/building-an-rag-system-using-elasticsearch-and-langchain)
- [Vector search](https://www.elastic.co/blog/vector-database-elasticsearch)
- Full-text search
- Logs
- Metrics
- Application performance monitoring (APM)
- Security logs


## 🛠️ Technical Stack
- **Knowledge Base**: `documents.json` containing course-related FAQ documents from the [LLM Zoomcamp](https://github.com/DataTalksClub/llm-zoomcamp/tree/main) course
- **Retriever**: MinSearch (lightweight local lexical search using TF-IDF and keyword matching)  
- **Search Method**: Hybrid (TF-IDF + keyword field filtering)  
- **Embedding/Vectorization**: Internal MinSearch vectorizer (TF-IDF)
- **Interface**: Jupyter Notebook

## ⚙️ Datasets
* `documents.json`: Small-scale keyword-only dataset
* `documents-llm.json`: Extended document set with LLM formatting in mind

>### FAQ Documents
> * [**DE Zoomcamp**](https://docs.google.com/document/d/19bnYs80DwuUimHM65UV3sylsCn2j1vizrPOwzBwQrebw/edit)

> * [**ML Zoomcamp**](https://docs.google.com/document/d/1LpPanc33QJJ6BSsyxVg-pWWNplal84TdZtQ1oaIhD8/edit)

> * [**MLOps Zoomcamp**](https://docs.google.com/document/d/12TlBfhIiktyBv8RnsoJR6F72bkPDGEvPOltJIxaEzE0/edit)


## ⚙️ Notebooks
* `elasticsearch-rag.ipynb`: RAG pipeline
* `parse-faq.ipynb`: Script to convert JSON-formatted FAQ content into usable input format
* `envconfig`: Testing OpenAI API in sample notebook

## ⚙️ Dependencies
Dependencies are listed in `requirements.txt`. Key packages:

* `elasticsearch`: for indexing and retrieving documents using Elasticsearch engine  
* `docker`: to run Elasticsearch as a local containerized service  
* `pandas`: for handling and structuring JSON data  
* `scikit-learn`: for evaluation utilities and potential preprocessing  
* `ipywidgets`: for interactive controls in Jupyter notebooks  
* `tqdm`: for progress tracking  
* `notebook`: Jupyter Notebook interface
  
**Install with:**

```bash
pip install -r requirements.txt
```

## ⚙️ Running Elastic Search 

>**Note:** Requires Docker to be installed and running on your machine. [Install Docker](https://www.docker.com/get-started/)

```bash
docker run -it \
    --rm \
    --name elasticsearch \
    -m 4GB \
    -p 9200:9200 \
    -p 9300:9300 \
    -e "discovery.type=single-node" \
    -e "xpack.security.enabled=false" \
    docker.elastic.co/elasticsearch/elasticsearch:8.4.3
```

If the previous command doesn't work (i.e. you see "error pulling image configuration"), try to run ElasticSearch directly from Docker Hub:

```bash
docker run -it \
    --rm \
    --name elasticsearch \
    -p 9200:9200 \
    -p 9300:9300 \
    -e "discovery.type=single-node" \
    -e "xpack.security.enabled=false" \
    elasticsearch:8.4.3
```

### 🛠️ Index settings:

```python
{
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
    },
    "mappings": {
        "properties": {
            "text": {"type": "text"},
            "section": {"type": "text"},
            "question": {"type": "text"},
            "course": {"type": "keyword"} 
        }
    }
}
```

### ✍️ Query:

```python
{
    "size": 5,
    "query": {
        "bool": {
            "must": {
                "multi_match": {
                    "query": query,
                    "fields": ["question^3", "text", "section"],
                    "type": "best_fields"
                }
            },
            "filter": {
                "term": {
                    "course": "data-engineering-zoomcamp"
                }
            }
        }
    }
}
```


---
> ## 📌 Credits
> 📦  This project uses[Elasticsearch](https://github.com/elastic/elasticsearch/tree/main), developed and maintained by [Elastic](https://github.com/elastic). Knowledge base and code adapted from the [LLM Zoomcamp](https://github.com/DataTalksClub/llm-zoomcamp/tree/main) by DataTalks.Club. 

## ⚙️ License
This project is released under MIT license. 


