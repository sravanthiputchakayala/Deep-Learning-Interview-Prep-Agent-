Deep Learning Interview Prep Agent
A RAG-powered study assistant for deep learning interview preparation, built with Python, LangChain, LangGraph, ChromaDB, and Streamlit.
The application uses uploaded study material to support interview practice: ask questions, generate interview-style questions, submit answers for evaluation, and review explanations with source references.
Overview
Preparing for deep learning interviews involves understanding concepts and explaining them clearly. This project connects a language model to a searchable collection of study notes so that practice and explanations can be grounded in the user's material.
It demonstrates an end-to-end Retrieval-Augmented Generation (RAG) application, from document ingestion and embedding generation to retrieval, response generation, and an interactive interface.
This project uses existing language and embedding models; it does not train a new deep learning model.
Key Features
- Document-based study: Build a searchable knowledge base from uploaded deep learning material.
- Contextual question answering: Retrieve relevant passages to support explanations.
- Interview question generation: Practice questions about concepts covered in the material.
- Answer evaluation: Receive model-generated feedback and a score on a 0–10 scale.
- Source references: Review the material supporting generated explanations.
- Persistent vector storage: Keep indexed document chunks in a local ChromaDB database.
- Interactive interface: Use Streamlit to upload material and interact with the assistant.
Topics can include artificial neural networks (ANNs), convolutional neural networks (CNNs), recurrent neural networks (RNNs), and long short-term memory networks (LSTMs), depending on the uploaded content.
How It Works
1. Document ingestion
Uploaded documents are processed into text and divided into smaller chunks. Metadata, such as the source filename, is attached to each chunk so that retrieved content can be traced to its origin.
Chunk identifiers are derived from the source filename and chunk text using SHA-256. These identifiers help detect repeated chunks during subsequent uploads.
2. Embedding and storage
An embedding model converts each chunk into a numerical vector representing its meaning. ChromaDB stores the chunk text, embedding, identifier, and metadata. The local index is stored under data/chroma_db.
3. Retrieval
When a user asks a question, the application searches the indexed material for relevant chunks. Those passages provide context for the language model.
4. Interview preparation
LangChain connects the retrieval and model components, while LangGraph orchestrates the application workflow. The assistant uses the retrieved context to support explanations, interview questions, and answer feedback.
5. Response display
Streamlit displays the response and source references so that the user can review the supporting material and continue practicing.
Technology Stack
Technology	Role
Python	Application logic and document processing
Streamlit	Interactive study interface
LangChain	Integration of models, prompts, and retrieval components
LangGraph	Workflow orchestration
ChromaDB	Persistent vector storage and similarity search
Embedding model	Numerical representations of document chunks
Language model	Question generation, explanations, and answer feedback


Getting Started
Prerequisites
- Git and a Python version compatible with the repository's dependencies.
- Access to the language model provider configured in the project.
- Any API credentials required by that configuration.
- Study documents in formats supported by the application's uploader.
1. Clone the repository
git clone https://github.com/sravanthiputchakayala/Deep-Learning-Interview-Prep-Agent.git
cd Deep-Learning-Interview-Prep-Agent
2. Create a virtual environment
python -m venv .venv
Windows PowerShell:
.\.venv\Scripts\Activate.ps1
macOS / Linux:
source .venv/bin/activate
3. Install dependencies
If the repository provides requirements.txt, run:
python -m pip install -r requirements.txt
If dependencies are managed through pyproject.toml, use the package manager configured for that file instead.
4. Configure the model
Set the API credentials and model settings expected by the project's configuration code. If a .env.example file is provided, copy it to .env and supply your values. Keep API keys out of Git and ensure .env is ignored.
5. Launch the interface
For a Streamlit entry point named app.py, run:
python -m streamlit run app.py
If the entry point has a different name or location, substitute that path. Open the local URL printed in the terminal.
Example Usage
1. Upload notes covering CNNs, RNNs, or another deep learning topic.
2. Allow the application to index the material.
3. Ask a concept question or request an interview question.
4. Submit your answer when practicing.
5. Review the explanation, feedback, and supporting source references.
Example prompts:
- “Explain convolution and pooling using my uploaded notes.”
- “Generate an interview question about recurrent neural networks.”
- “What problem does an LSTM address?”
- “Explain the difference between a CNN and an RNN.”
These examples illustrate intended use; response quality depends on the uploaded material and configured model.
Design Highlights
- RAG: Supplies retrieved study material as context for generation.
- Metadata: Preserves the connection between a chunk and its source document.
- Deterministic chunk identifiers: Help recognize repeated content during ingestion.
- Local persistence: Allows stored vectors to remain available across application restarts.
- Workflow orchestration: Coordinates application steps through LangGraph.
Limitations
- Retrieval quality depends on document quality, chunking, and the embedding model.
- Generated answers and citations still require review; RAG does not guarantee correctness.
- Answer scores are model-generated study feedback, not a standardized assessment.
- Questions outside the uploaded material may have insufficient supporting context.
- API availability, usage limits, and latency depend on the configured provider.
- Document text may be sent to the configured model provider during generation.
Possible Improvements
- Add a retrieval evaluation dataset and measure answer grounding.
- Introduce topic and difficulty filters for interview practice.
- Track study progress and answer history across sessions.
- Add timed mock interviews and downloadable feedback summaries.
- Improve handling of questions with insufficient supporting material.
These are proposed enhancements rather than claims about existing functionality.
