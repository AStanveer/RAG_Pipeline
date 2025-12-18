# 📚 Enhanced RAG Document Q&A System

A multi-document RAG system I built for intelligent PDF analysis and question answering.

## ✨ What I Built

### 🔍 **Smart Document Processing**
- **Multi-Document Detection**: Can automatically identify and separate different documents within a single PDF file (like finding resumes, contracts, and invoices all in one PDF)
- **Intelligent Classification**: Uses AI to figure out what type of document it's looking at (Resume, Contract, Invoice, Mortgage, etc.)
- **Smart Chunking**: Breaks documents into meaningful chunks while keeping track of where information came from

### 🧠 **Intelligent Search System**
- **Query Routing**: Predicts which document type would best answer your question
- **Fast Vector Search**: Uses FAISS for efficient similarity matching
- **Context-Aware Answers**: Provides answers with clear citations showing source documents and page numbers

### 💬 **Clean Q&A Interface**
- **Source Attribution**: Shows exactly which document and pages the answer came from
- **Confidence Scores**: Tells you how confident the system is in its answer
- **Performance Tracking**: Logs response times and accuracy metrics

### 🎨 **User-Friendly Design**
- **Modern UI**: Clean cyan-themed interface built with Gradio
- **Real-time Processing**: Live updates while documents process
- **Built-in PDF Viewer**: See your documents right in the app
- **Example Questions**: Quick buttons to try common queries

## 🛠️ Technologies I Used

| Component | Technology | Why I Chose It |
|-----------|------------|---------|
| **Frontend** | Gradio | Fast prototyping, great for AI apps |
| **Document Processing** | PyMuPDF, pdfplumber, Tesseract | Reliable text extraction with OCR fallback |
| **Embeddings** | Sentence Transformers | High-quality semantic understanding |
| **Vector Search** | FAISS | Lightning-fast similarity search |
| **LLM** | LlamaCPP (Qwen3-4B) | Efficient local model that runs on CPU |
| **Document Intelligence** | LlamaIndex | Excellent tools for chunking and indexing |
| **Utilities** | NumPy, PyPDF2, regex | Essential data processing tools |

## 📋 How to Run It

### Step 1: Install Requirements
```bash
# Install system dependencies
sudo apt-get install tesseract-ocr

# Install Python packages
pip install gradio gradio_pdf
pip install pypdf PyPDF2 pymupdf pdfplumber
pip install sentence-transformers transformers
pip install faiss-cpu
pip install llama-index llama-index-readers-file
pip install llama-index-embeddings-huggingface
pip install llama-index-vector-stores-faiss
pip install llama-index-llms-llama-cpp
pip install llama-cpp-python sentencepiece
pip install pytesseract pillow
pip install numpy pandas
```

## 🚀 How to Use It

### 1. Upload a PDF
- Drag & drop any PDF file
- The system works best with multi-page documents like:
  - Resumes with cover letters
  - Contract packages
  - Financial documents
  - Academic papers

### 2. Let It Process
The system will:
- Extract text from all pages
- Identify different document types
- Create searchable chunks
- Build vector indexes

### 3. Ask Questions
Try questions like:
- "What's the main summary?"
- "What skills are listed in the resume?"
- "What are the payment terms?"
- "Find all the monetary amounts mentioned"

### 4. Get Answers with Sources
Each answer shows:
- The actual answer
- Which documents it came from
- Page numbers
- Confidence score

## 🏗️ How It Works (Technical Overview)

### Step 1: Text Extraction
Combines three methods for best results:
1. **PyMuPDF**: Fast extraction from text-based PDFs
2. **pdfplumber**: Better for complex layouts
3. **Tesseract OCR**: For scanned/image PDFs

### Step 2: Document Classification
Uses the Qwen LLM to analyze text and decide:
- "Is this a resume or contract?"
- "Where does one document end and another begin?"

### Step 3: Smart Chunking
- Breaks documents into 300-word chunks
- Adds 80-word overlap for context
- Preserves metadata (document type, page numbers)

### Step 4: Vector Search
- Converts chunks to embeddings using MPNet
- Stores in FAISS for fast similarity search
- Creates separate indexes for each document type

### Step 5: Query & Answer
1. Routes query to relevant document type
2. Finds most similar chunks
3. Combines context and generates answer
4. Cites sources with page numbers

## 📊 What I Learned Building This

### Technical Challenges Solved
1. **Mixed Document PDFs**: Figuring out how to detect boundaries between different documents in one file
2. **OCR Integration**: Making text extraction work reliably for both digital and scanned PDFs
3. **Memory Management**: Handling large documents without crashing
4. **Response Quality**: Balancing answer accuracy with response speed

### Key Insights
- **Metadata Matters**: Keeping track of document types and page numbers makes answers much more useful
- **Chunking Strategy**: Overlapping chunks preserve context much better
- **User Experience**: Clean UI and clear explanations make AI systems more trustworthy
- **Performance Trade-offs**: There's always a balance between speed, accuracy, and resource usage

## ⚙️ Customization Options

You can tweak these settings in the code:

```python
# In the IntelligentRetriever class:
chunk_size = 300       # Smaller = faster, larger = more context
chunk_overlap = 80     # How much chunks overlap
num_retrieve = 4       # How many chunks to use for answers

# In the classification function:
max_length = 800       # How much text to analyze for classification
```

## 🔧 Common Issues & Fixes

### If it's running slow:
- Try smaller PDFs first
- Reduce `chunk_size` to 200
- Lower `num_retrieve` to 3

### If OCR isn't working:
- Make sure `tesseract-ocr` is installed
- Check PDF quality (scanned PDFs need to be clear)
- Try different DPI settings in the code

### If models won't download:
- Check internet connection
- May need VPN for HuggingFace in some regions
- Can use smaller models by changing the model names

## 📈 Future Improvements I'd Make

### If I had more time:
1. **Better Table Extraction**: Current OCR struggles with complex tables
2. **Multi-language Support**: Add support for non-English documents
3. **Batch Processing**: Handle multiple PDFs at once
4. **Export Features**: Save conversations and extracted data
5. **Advanced Analytics**: Document comparison and trend analysis

## 💡 Cool Features to Try

1. **Mixed Document Testing**: Upload a PDF with both a resume and an invoice
2. **Specific Queries**: Ask about particular sections like "What are the terms in section 4.2?"
3. **Comparison Questions**: "Compare the skills in this resume to typical software engineering requirements"
4. **Extraction Tasks**: "List all the email addresses found in the documents"

## 🎯 Project Scope & Constraints

### What it does well:
- **Multi-document PDFs**: Excellent at separating different documents
- **Source attribution**: Very clear about where answers come from
- **Fast setup**: Runs locally without cloud dependencies
- **Flexible queries**: Handles a wide variety of question types

### Current limitations:
- **Large PDFs**: Very large documents (100+ pages) can be slow
- **Complex layouts**: Tables and forms sometimes lose formatting
- **Real-time processing**: Initial indexing takes time
- **Model size**: 4B parameter LLM has limits on complex reasoning
