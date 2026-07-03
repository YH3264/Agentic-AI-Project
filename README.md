# Agentic AI Project Course Workspace

Welcome to the workspace for the Agentic AI Crash Course! This repository contains 8 progressive projects demonstrating the building blocks of LLM integration, Retrieval-Augmented Generation (RAG), and advanced Agentic workflows with memory, multi-modality, and tools.

---

## Workspace Directory Structure & Projects Overview

Here is an overview of the 8 projects included in this folder:

| Folder Name | Project Type | Description |
| :--- | :--- | :--- |
| [1_simple_call_to_LLM](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/1_simple_call_to_LLM) | Notebook | **Introduction to LLMs**: Demonstrates basic setup, model loading, and making standard textual completions using LangChain and ChatGroq. |
| [2_health_analysis](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/2_health_analysis) | Notebook & Streamlit App | **Structured Health Analysis**: Analyzes raw blood work report texts (using Google Gemini model) to identify abnormal values, categorize health risks, and run a dedicated web interface using Streamlit. |
| [3_vector_db](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/3_vector_db) | Notebook | **Vector Database Fundamentals**: Explores embeddings, document splitting, and storing/querying vector vectors using Chroma DB. |
| [4_RAG_basic](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/4_RAG_basic) | Notebook | **Retrieval-Augmented Generation (RAG)**: Connects a vector store populated with content from a PDF document (`telecom_guide.pdf`) to an LLM, answering queries grounded in document context. |
| [5_single_agent](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/5_single_agent) | Notebook | **Tool-using Agent**: Introduces the concept of an AI agent with functional tools (looking up product details and product reviews in dictionary data structures). |
| [6_memory](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/6_memory) | Notebook | **Agent with Conversation Memory**: Enhances the product-query agent by keeping track of the chat message history to reference previous interactions. |
| [7_multimodal](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/7_multimodal) | Notebook | **Multimodal Vision Agent**: Sends base64-encoded health report images directly to a vision LLM, extracts conditions, and triggers tools to suggest tailored diet plans. |
| [8_project_shopping_agent](file:///c:/Users/lathi/OneDrive/Desktop/lathika/code/Agentic%20ai%20project/8_project_shopping_agent) | Capstone Streamlit Web App | **AI Shopping Assistant**: An end-to-end, multi-tool conversational agent capable of image-based product discovery, database product searches, rating validation, and ordering. |

---

## Detailed Focus: Project 8 (AI Shopping Assistant)

The **AI Shopping Assistant** (`8_project_shopping_agent`) is a comprehensive web application showcasing how LLMs can act as intelligent orchestrators to perform database actions, call APIs, and execute complex business logic via tool calls.

### Features
1. **Interactive Chat Interface**: Conversational UI built with Streamlit allowing users to search products, ask questions, and confirm checkout orders.
2. **Shop by Image (Multimodal Discovery)**:
   - Users upload a product photo (e.g., of honey or oats) in the sidebar.
   - The app saves it to a temp file and invokes the agent.
   - The agent calls the `describe_product_image` tool, which uses a vision model (`meta-llama/llama-4-scout-17b-16e-instruct`) to analyze the visual label, identifying the product name, organic status, and product type.
3. **Database Product Search**: Querying a SQLite database (`store.db`) filterable by search term, max price, and organic status.
4. **API Integration (Product Ratings)**: Calls the ratings API to aggregate reviews and ensure products meet specified star limits (e.g., minimum 4.5 stars).
5. **Checkout & Ordering**: Records confirmed purchases directly inside the database orders table, returning an order confirmation ID.

### Core Files
- `app.py`: Streamlit frontend managing conversational UI state, sidebar image uploads, and agent invoking logic.
- `shopping_agent.py`: Agent backend definition compiling tools (`search_products`, `get_rating`, `checkout`, `describe_product_image`) and instructions using Groq's `qwen/qwen3-32b` model.
- `reviews_api.py`: Python module handling SQLite aggregation to return product ratings and review counts.
- `store.db`: SQLite database containing three main tables: `products`, `reviews`, and `orders`.

---

## Getting Started

### 1. Installation & Environment Setup

Ensure you have Python installed, then clone or navigate to the workspace folder. 

1. **Install Dependencies**
   Run the following command to install the required packages:
   ```bash
   pip install -r requirements.txt
   ```
   *(Alternatively, if you are using `uv`, you can run `uv sync` to set up your virtual environment automatically.)*

2. **Configure API Keys**
   Create a `.env` file in the root workspace folder (`Agentic ai project/`) and populate it with your Groq and Google API keys:
   ```env
   GOOGLE_API_KEY=your_gemini_api_key
   GROQ_API_KEY=your_groq_api_key
   ```

---

### 2. How to Run the Projects

#### Running Jupyter Notebooks (Projects 1 to 7)
Launch Jupyter Notebook in your workspace root:
```bash
jupyter notebook
```
Open and run cells in sequence inside each project folder (e.g. `1_simple_call_to_LLM/call_llm.ipynb`).

#### Running Streamlit Applications (Projects 2 and 8)
- **To run Project 2 (Blood Work Analyzer app)**:
  ```bash
  streamlit run 2_health_analysis/streamlit_app/app.py
  ```

- **To run Project 8 (AI Shopping Assistant)**:
  ```bash
  streamlit run 8_project_shopping_agent/app.py
  ```
  Open the local address provided by Streamlit (typically `http://localhost:8501`) in your web browser. Upload an image from `8_project_shopping_agent/resources/` (e.g., `honey.png` or `oats.png`) in the sidebar, click **Find similar products**, and watch the AI search and recommend items from the store database!
