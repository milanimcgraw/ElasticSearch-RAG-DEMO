# ElasticSearch RAG DEMO

## ⚙️ Project Overview          
This repository demonstrates a lightweight Retrieval-Augmented Generation (RAG) pipeline on structured FAQ data using [MinSearch](https://github.com/alexeygrigorev/minsearch), a minimalistic search engine that enables efficient keyword-based retrieval and simple appendable indexing.

## 🛠️ Technical Stack
- **Knowledge Base**: `documents.json` containing course-related FAQ documents from the [LLM Zoomcamp] (https://github.com/DataTalksClub/llm-zoomcamp/tree/main) course
- **Retriever**: MinSearch (lightweight local lexical search using TF-IDF and keyword matching)  
- **Search Method**: Hybrid (TF-IDF + keyword field filtering)  
- **Embedding/Vectorization**: Internal MinSearch vectorizer (TF-IDF)
- **Interface**: Jupyter Notebook   

## ⚙️ Dependencies
Dependencies are listed in `requirements.txt`. Key packages:

* `pandas`: for handling and structuring JSON data
* `scikit-learn`: for TF-IDF vectorization and cosine similarity
* `ipywidgets`: for interactive controls in Jupyter notebooks
* `tqdm`: for progress tracking
* `notebook`: Jupyter Notebook interface
* `minsearch`: text search engine that uses TF-IDF and cosine similarity for text fields and exact matching for keyword fields
  
**Install with:**

```bash
pip install -r requirements.txt
```

## ⚙️ Datasets
* `documents.json`: Small-scale keyword-only dataset
* `documents-llm.json`: Extended document set with LLM formatting in mind

> #### **FAQ Documents**
> * DE Zoomcamp: https://docs.google.com/document/d/19bnYs80DwuUimHM65UV3sylsCn2j1vziPOwzBwQrebw/edit
> * ML Zoomcamp: https://docs.google.com/document/d/1LpPanc33QJJ6BSsyxVg-pWNMplal84TdZtq10naIhD8/edit
> * MLOps Zoomcamp: https://docs.google.com/document/d/12TlBfhIiKtyBv8RnsoJR6F72bkPDGEvPOItJIxaEzE0/edit

## ⚙️ Notebooks
* `minsearch-rag.ipynb`: Walkthrough of keyword-based RAG pipeline
* `parse-faq.ipynb`: Script to convert JSON-formatted FAQ content into usable input format
* `minsearch_example.ipynb`: Example demo from [MinSearch](https://github.com/alexeygrigorev/minsearch) created by [**Alexey Grigorev**](https://github.com/alexeygrigorev).

## ⚙️ Quickstart
Clone the repo and install dependencies:

```bash
git clone https://github.com/milanimcgraw/Minsearch-RAG.git
cd Minsearch-RAG
pip install -r requirements.txt
````

Run the main notebook:

```bash
jupyter notebook Notebooks/minsearch-rag.ipynb
```
---
> ## 📌 Credits
> 📦 This project uses code adapted from the [LLM Zoomcamp](https://github.com/DataTalksClub/llm-zoomcamp/tree/main) by DataTalks.Club. 

## ⚙️ License
This project is released under MIT license. 

