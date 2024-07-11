# RAG--Vector-Database-Chatbot-using-Flowise-and-Pinecone-


## Introduction

This project involves the development of a responsive chatbot capable of handling document-based queries using advanced language processing and vector database technologies. The chatbot leverages Flowise for workflow orchestration, LLaMA 3 for embedding generation, and Pinecone for efficient similarity search.

## Features
- **PDF File Upload and Processing**
- **Text Chunking**
- **Embedding Generation using LLaMA 3**
- **Vector Storage and Retrieval with Pinecone**
- **Conversational Retrieval QA**

## Installation

### Prerequisites
- Python 3.7 or higher
- Pip (Python package installer)
- Pinecone account and API key
- Flowise framework

### Step-by-Step Installation


1. **Install Required Packages**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Set Up Pinecone**:
   - Sign up on [Pinecone](https://www.pinecone.io/) and get your API key.
   - Create an index on Pinecone.

### Configuration
1. **Configure Pinecone Connection**:
   - In your code, set up Pinecone connection credentials:
     ```python
     import pinecone

     pinecone.init(api_key='YOUR_PINECONE_API_KEY')
     index = pinecone.Index('your-index-name')
     ```

## Creating the Chatbot

### Workflow
The workflow is managed using Flowise and involves the following steps:

1. **PDF File Upload**:
   - Upload the PDF file that serves as the data source.

2. **Text Chunking**:
   - Use Recursive Character Text Splitter to break the document into chunks.
   - Configure chunk size and overlap:
     ```python
     chunk_size = 1000
     chunk_overlap = 200
     ```

3. **Embedding Generation**:
   - Generate embeddings for each text chunk using LLaMA 3:
     ```python
     
     model = LLaMA3(model_name='llama3')
     embeddings = model.encode(text_chunks)
     ```

4. **Storing Embeddings in Pinecone**:
   - Store the generated embeddings in Pinecone:
     ```python
     for i, embedding in enumerate(embeddings):
         index.upsert([(f'doc_{i}', embedding)])
     ```

5. **Handling User Queries**:
   - Process user queries to retrieve relevant information:
     ```python
     query_embedding = model.encode([user_query])
     results = index.query(query_embedding, top_k=3)
     ```

### Components

- **PDF File Handling**:
  - Upload and handle PDF files using the `Pdf File` component in Flowise.

- **Text Splitting**:
  - Use `Recursive Character Text Splitter` to manage text chunking.

- **Embedding Generation**:
  - Generate embeddings with `Ollama Embeddings` using the LLaMA 3 model.

- **Vector Database (Pinecone)**:
  - Store and retrieve embeddings with `Pinecone`.

- **Conversational Retrieval**:
  - Integrate chat model and vector store retriever using `Conversational Retrieval QA Chain`.

### Link to Youtube Video of demonstration:

[Watch the video](https://youtu.be/WusE53lVpfw)


