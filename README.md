# GroundedQA: An Enterprise Knowledge Engine

> A Retrieval-Augmented Generation (RAG) system that enables knowledge workers to ask natural language questions and receive accurate, source-grounded answers from internal, proprietary documents.

This repository contains the implementation of a prototype RAG system using LangChain, OpenAI, and ChromaDB. It demonstrates a core AI product capability: grounding Large Language Model (LLM) responses in factual, verifiable data to build user trust and deliver real business value.

## The Problem & The Opportunity (The "Why")

In fast-growing companies, critical information is often fragmented across countless PDFs, reports, and internal wikis. This creates a significant drag on productivity and decision-making.

*   * User Persona:** **Enterprise Knowledge Workers** (e.g., Product Managers, Strategy Analysts, new employees).
*   **The Problem:** These professionals spend hours each week searching for specific answers. Keyword search is inefficient and often misses the context required for complex decisions, leading to wasted time, inconsistent actions, and a high risk of using outdated information.
*   **The Hypothesis:** By leveraging an LLM grounded in a curated set of internal documents, we can create a single source of truth that **reduces information retrieval time by over 90%** and **dramatically increases the accuracy and trustworthiness of answers**.

## The Solution (The "What")

This project is a functional prototype of a RAG-based knowledge engine that provides accurate, cited answers from a given PDF document.

### Core Features
*   **Document Ingestion:** Loads and processes external PDF documents (in this case, the research paper `LLMAutonomousAgents.pdf`).
*   **Intelligent Chunking & Indexing:** Splits documents into semantically relevant chunks and stores them as vector embeddings in a ChromaDB database for efficient similarity search.
*   **Conversational Q&A:** Allows a user to ask questions in natural language.
*   **Grounded Responses with Citations:** Generates answers based **only** on the provided document context and includes the source page number for verification, effectively eliminating hallucinations.

### Tech Stack Highlights
*   **Orchestration:** LangChain
*   **LLM:** OpenAI's `gpt-3.5-turbo`
*   **Embeddings:** OpenAI's `text-embedding-ada-002`
*   **Vector Store:** ChromaDB (for fast, in-memory prototyping)
*   **Document Loading:** PyPDF
*   **Text Splitting:** Tiktoken (via LangChain's `RecursiveCharacterTextSplitter`)

### Visuals: User & System Flow

The system follows a classic RAG architecture, transforming unstructured data into a queryable knowledge base.
![RAG: User & System Flow](/images/rag.png)


## Results & Impact (The "So What?")

This prototype successfully proves the core hypothesis and demonstrates tangible value.

*   **Primary KPI (User Value):** **Answer Relevance Score.** The system successfully answered specific, nuanced questions about the source document (`LLMAutonomousAgents.pdf`) and provided accurate source citations, indicating high relevance.
*   **Business Metric (Impact):** **Time-to-Answer.** The prototype demonstrates the potential to reduce time-to-answer from minutes or hours of manual searching to mere seconds.

## Learnings & Future Roadmap (What's Next?)

This project served as a powerful proof-of-concept and highlighted key strategic trade-offs for building a production-ready system.

### Key Learnings & Strategic Trade-offs
*   **Vector DB Scalability:** **ChromaDB** was chosen for its rapid, in-memory prototyping capabilities. For an enterprise system handling millions of documents, a scalable, managed solution like **Pinecone, Weaviate, or Vertex AI Vector Search** would be necessary to manage cost, latency, and concurrent users.
*   **LLM & Embedding Choices:** **GPT-3.5-Turbo** and `ada-002` provided an excellent balance of cost, speed, and performance. A future iteration would involve A/B testing against more powerful models (like GPT-4 for complex reasoning) or fine-tuning smaller, open-source models (like Llama 3) for domain-specific tasks and enhanced data privacy.
*   **Chunking Strategy:** The **`RecursiveCharacterTextSplitter`** is a solid baseline. However, retrieval quality is highly dependent on the chunking method. The next step would be to experiment with different chunk sizes and overlap strategies to optimize for different document types (e.g., dense research papers vs. conversational meeting notes).

### Future Roadmap
*   **V2: User Interface & Feedback:** Develop a simple Streamlit or Gradio front-end to allow non-technical users to interact with the system and provide feedback (👍/👎) on answer quality, which can be used for evaluation and future fine-tuning.
*   **V3: Expanded Document Support:** Integrate loaders for other common enterprise formats like `.docx`, `.pptx`, and Confluence pages to create a more comprehensive knowledge engine.
*   **V4: Advanced Retrieval:** Implement more sophisticated retrieval strategies like HyDE (Hypothetical Document Embeddings) or a re-ranking model to improve the quality of context fed to the LLM, further increasing answer accuracy.

---

## Setup & Installation

To run this project locally, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd <your-repository-name>
    ```

2.  **Create and activate a virtual environment:**
    ```bash
    # For Mac/Linux
    python3 -m venv venv
    source venv/bin/activate

    # For Windows
    python -m venv venv
    .\venv\Scripts\activate
    ```

3.  **Install the required dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set up your OpenAI API Key:**
    You will need to have your OpenAI API key set as an environment variable named `OPENAI_API_KEY`. The script will prompt you to enter it if it's not found.

5.  **Run the Jupyter Notebook:**
    