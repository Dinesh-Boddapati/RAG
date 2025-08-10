# PDF Question-Answering with RAG and Gemini AI

This project demonstrates a complete Retrieval-Augmented Generation (RAG) pipeline built in a Python notebook. It allows a user to upload a PDF document, and then ask questions about its content. The system leverages the Google Gemini AI model to provide accurate, context-aware answers based on the information within the document.

This entire project can be run in a Google Colab environment.

## How It Works

The project follows the core principles of Retrieval-Augmented Generation to connect a large language model with custom data.

1.  **Load & Chunk**: A user-uploaded PDF document is read using the `pypdf` library. The extracted text is then broken down into smaller, manageable chunks.
2.  **Embed**: Each text chunk is converted into a numerical representation (a vector embedding) using Google's `models/embedding-001` model. These embeddings capture the semantic meaning of the text.
3.  **Index**: The vector embeddings are stored and indexed in `FAISS` (Facebook AI Similarity Search), a library that enables highly efficient similarity searches.
4.  **Retrieve**: When a user asks a question, the question itself is converted into an embedding. FAISS is then used to search the index for the text chunks with the most similar embeddings to the question's embedding.
5.  **Generate**: The most relevant text chunks (the "context") are passed along with the original question to the Gemini generative model. The model is prompted to formulate an answer based *only* on the provided context, ensuring the response is grounded in the source document.

## Tech Stack

* **Language**: Python
* **AI Model**: Google Gemini (`gemini-2.5-flash`, `embedding-001`)
* **Vector Database**: `faiss-cpu`
* **PDF Processing**: `pypdf`
* **Environment**: Google Colab / Jupyter Notebook

---

## 🚀 Setup and Usage

Follow these steps to run the notebook yourself.

### Prerequisites
* A Google Account
* A  API Key. You can obtain one from [Google AI Studio](https://aistudio.google.com/app/apikey).


**Open in Google Colab**
    Open [Google Colab](https://colab.research.google.com/) and upload the `RAG.ipynb` notebook.
    * For the **Name**, enter `GEMINI_API_KEY`.
    * In the **Value** field, paste your actual Gemini API key.
    * Ensure the **"Notebook access"** toggle is enabled.


  **Run the Notebook Cells**
    Execute the cells in order from top to bottom:
    * **Install Libraries**: The first cell installs all necessary dependencies (`google-generativeai`, `faiss-cpu`, `pypdf`).
    * **Configure API Key**: The second cell securely loads your key from the Secrets manager.
    * **Upload PDF**: Run the upload cell and a button will appear. Click it to choose and upload the PDF file you want to query.
    * **Process and Index**: The subsequent cells will automatically chunk the text, create embeddings, and build the FAISS index.
    * **Ask a Question**: In the final cell, modify the question inside the `answer_question()` function call and run it to receive your answer.
    ```python
    # In the last cell, change the question to whatever you want to ask
    print(answer_question("What is the main topic of this document?"))
    ```
