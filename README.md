# RAG
This repository contains the backend implementation of a document retrieval system designed to generate contextual information for Large Language Models (LLMs) to use during inference. The project involves storing documents in a database, retrieving them based on similarity to a query, and caching responses for efficient access.

## Approach 1 Overview(FASTAPI.py):
My approach involves building a document search system by integrating MongoDB with a Sentence Transformer model to handle document storage and similarity-based search. I designed this system using FastAPI, a Python framework, to expose two key endpoints for adding and searching documents. Here's a breakdown of the process:
1. **Document Storage with MongoDB:**
*	MongoDB was chosen as the database to store documents. Each document consists of a title and content.
*	After storing the document, you generate an embedding (a numerical vector representation) of the document's content using the Sentence-Transformer model.
*	This embedding is stored in MongoDB alongside the document’s title and content, allowing future semantic searches.
2. **Embedding Generation Using Sentence-Transformer:**
*	Then the SentenceTransformer model (all-MiniLM-L6-v2) was used to convert the document content and search queries into vector embeddings.
3. **Cosine Similarity for Document Search:**
*	Cosine similarity is applied to compare the query embedding with the embeddings of documents stored in the database.
*	Cosine similarity is ideal for this task because it measures the angle between two vectors in a high-dimensional space, allowing us to determine how similar two pieces of text are, irrespective of their length or vocabulary differences.
*	The similarity score is used to rank documents and determine relevance.
4. **FastAPI for API Endpoints:**
*	FastAPI is used to create an API that exposes two key endpoints:
  - **Document Insertion Endpoint (/documents/)**
      - Users can upload a document (with title and content).
      - The content is transformed into an embedding using the sentence-transformer model.
      -	The document, along with its title, content, and generated embedding, is then stored in MongoDB.
* **Search Endpoint (/search/):**
    -	Users can submit a search query.
    - The query is converted into an embedding and compared to the embeddings of all stored documents using cosine similarity.
    -	Based on the similarity score, the system returns the top relevant documents.
*	**Customizations are allowed such as:**
    -	Threshold: You could add a threshold for similarity scores, returning only documents with scores above this threshold.
    -	Number of Results: You return the top N results, where N is customizable (defaulting to 10 results).
5. **End Result:**
*	Users can easily add documents and search for relevant documents based on semantic similarity, rather than relying on simple keyword matching. This approach is effective for retrieving documents that might be conceptually similar to the search query, even if they don’t share the same keywords.
  
In summary, this approach combines the strengths of document storage (with MongoDB), semantic embedding (with Sentence Transformers), and cosine similarity to provide a robust API that supports efficient document retrieval based on meaning rather than exact keyword matches. FastAPI provides a lightweight and fast framework for building and exposing these capabilities as web endpoints.

![image](https://github.com/user-attachments/assets/54a76e87-654f-435a-bca2-75fcf3656437) ![image](https://github.com/user-attachments/assets/f6be8909-c6bf-4e59-a84a-f1766d083abd)



## Approach 2 Overview(RAG_IMPLEMENTATION.py):
![image](https://github.com/user-attachments/assets/e022e704-777a-42c9-be7c-70f7c773e7cd)

In this next approach, I’m enhancing the document search system by integrating **LangChain**, **FAISS**, and **HuggingFace** embeddings to handle various document types like text files, web pages, and PDFs. Using **LangChain** tools, I load and split documents, then generate embeddings with a **HuggingFace model**.

For efficient searches, I build a **FAISS index** to store document embeddings, enabling fast semantic search. The search function retrieves relevant documents based on a query, filters results by score threshold, and returns the top matches.

I’m also planning to integrate Streamlit for a user interface and FastAPI to expose the system as an API, making it more interactive and scalable. Tools like ChromaDB and ObjectBox will help with efficient storage and retrieval of document data. This approach aims to provide faster, more accurate semantic searches across different formats.

## Videos, Github repos and blogs referred

* https://www.youtube.com/watch?v=9Thc6hRw2Gs
* https://blog.gopenai.com/semantic-search-with-mongodb-and-fastapi-comprehensive-guide-204bb7ba95e2
* https://github.com/krishnaik06/Updated-Langchain
