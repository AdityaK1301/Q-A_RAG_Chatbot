# Q-A_RAG_Chatbot
This project is an interactive Question Answering (Q&A) chatbot designed for CBSE Class 3 students. It uses a Retrieval-Augmented Generation (RAG) architecture to answer questions from the official syllabus, ensuring responses are accurate and syllabus-aligned.

## Features

- **Retrieval-Augmented Generation (RAG):** Combines semantic search over syllabus content (retrieval) with a local language model (generation) for high-quality answers.
- **Class 3 Syllabus Coverage:** Answers are based strictly on CBSE Class 3 chapters, including English, EVS, and Maths.
- **PDF Support:** Handles multiple chapters per subject, loading data from PDFs stored in ZIP archives.
- **Simple, Student-Friendly Responses:** Designed to explain concepts in a way that’s easy for young learners to understand.
- **Offline-Ready:** Works entirely on your local machine, using Ollama for running LLMs (e.g., `gemma:2b-instruct`) and sentence-transformers for embedding.

## Dataset Structure

- All syllabus content is stored in the `class3_books/` folder.
- This folder contains multiple `.zip` files (e.g., `ENGLISH.zip`, `MATHS.zip`, `EVS.zip`).
- Each `.zip` contains multiple chapter PDFs for the respective subject.

Example:
```
class3_books/
├── ENGLISH.zip
│   ├── Lesson1.pdf
│   ├── Lesson2.pdf
│   └── ...
├── EVS.zip
│   ├── Chapter1.pdf
│   └── ...
└── MATHS.zip
    ├── Chapter1.pdf
    └── ...
```

### Downloading the Dataset

**Note:** Due to file upload restrictions, the actual syllabus PDF files are not included in this repository.

To use the chatbot, you must manually download the official NCERT Class 3 textbooks in PDF format. Please follow these instructions:

1. **Go to the official NCERT textbook website:**  
   [https://ncert.nic.in/textbook.php](https://ncert.nic.in/textbook.php)

2. **Select Class 3** and choose the subjects (English, EVS, Maths).

3. **Download the chapter PDFs** for each subject.

4. **Organize the PDFs:** Place the PDFs into appropriately named `.zip` archives (e.g., `ENGLISH.zip`, `MATHS.zip`, `EVS.zip`), with each archive containing the individual chapter PDFs for the subject.

5. **Create the folder:** Place your zipped subject files in a folder named `class3_books/` in the project root.

Your folder structure should look like the example above.

## How It Works

1. **Data Loading:** All PDFs are extracted from the zip files, and text is extracted and cleaned.
2. **Chunking & Embedding:** The syllabus text is split into manageable chunks (max 200 words), and each chunk is embedded using Sentence Transformers.
3. **Retrieval:** When a user asks a question, the system retrieves the most relevant chunks using semantic similarity.
4. **Generation:** The retrieved context is passed to a local LLM via Ollama, which generates a student-friendly answer.
5. **User Interaction:** Users can interact via the command line to ask syllabus-related questions.

## RAG Architecture

This project implements a **Retrieval-Augmented Generation (RAG)** system:

- **Retriever:** Uses Sentence Transformers to retrieve the most relevant syllabus context for a given question.
- **Generator:** Uses a local LLM (running via Ollama, e.g., `gemma:2b-instruct`) to generate answers grounded in the retrieved content.
- This ensures that answers are both natural and factually accurate with respect to the syllabus.

## Requirements

- Python 3.8+
- [Ollama](https://ollama.com/) (for running local LLMs)
- Packages: `requests`, `sentence-transformers`, `pymupdf`, `torch`, `scikit-learn`, `numpy`, etc.

Install dependencies:
```bash
pip install requests sentence-transformers pymupdf
```

## Usage

1. Download the NCERT Class 3 subject chapter PDFs from the official NCERT site as described above.
2. Organize them into zipped subject files in the `class3_books/` folder.
3. Make sure Ollama is running with your preferred model (e.g., `ollama run gemma:2b-instruct`).
4. Run the notebook: `query_chatbot.ipynb`
5. Interact with the chatbot in the terminal or notebook output.

## Example Interaction

```
🤖 CBSE Class 3 Q/A Tool Ready! Ask syllabus questions (type 'quit' to exit)

You: what are word numerals
Bot: Word numerals are words that represent numbers. For example, the number 56 is written as "fifty-six".
```

## Customization

- You can add more subjects or chapters by including new zip files with additional PDFs in `class3_books/`.
- Change the underlying LLM or embedding model by modifying the configuration in the notebook.


**Note:** The chatbot delivers answers *only* from the uploaded syllabus content. For questions not covered by the syllabus, it will politely indicate so.
