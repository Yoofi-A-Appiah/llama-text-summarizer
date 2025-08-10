# LLaMA Text Summarizer

A full-stack AI application that leverages the LLaMA 2 model via Ollama to provide intelligent text summarization. This project demonstrates how to build and deploy a complete AI service with a FastAPI backend and Streamlit frontend.

## Features

- **AI-Powered Summarization**: Uses LLaMA 2 model for high-quality text summarization
- **RESTful API**: FastAPI backend with clean endpoints
- **User-Friendly Interface**: Interactive Streamlit web application
- **Local Processing**: Runs entirely on your machine using Ollama
- **Fast Response**: Optimized for quick summarization tasks

## Architecture

```
┌─────────────────┐    HTTP    ┌─────────────────┐    HTTP    ┌─────────────────┐
│  Streamlit UI   │ ────────── │  FastAPI        │ ────────── │     Ollama      │
│  (Port 8501)    │            │  (Port 8000)    │            │  (Port 11434)   │
└─────────────────┘            └─────────────────┘            └─────────────────┘
```

## Project Structure

```
text-summarizer-llama/
├── README.md                 # Project documentation
├── requirements.txt          # Python dependencies
├── backend/
│   └── main.py              # FastAPI backend server
├── frontend/
│   └── app.py               # Streamlit frontend application
└── venv/                    # Virtual environment (created after setup)
```

## Prerequisites

- Python 3.8 or higher
- [Ollama](https://ollama.ai/) installed and running
- LLaMA 2 model downloaded via Ollama

## Installation & Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd text-summarizer-llama
```

### 2. Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Setup Ollama & LLaMA 2
First, install [Ollama](https://ollama.ai/) on your system, then:

```bash
# Pull the LLaMA 2 model
ollama pull llama2

# Verify the model is available
ollama list
```

### 5. Start the Services

**Terminal 1 - Start Ollama (if not already running):**
```bash
ollama serve
```

**Terminal 2 - Start FastAPI Backend:**
```bash
uvicorn backend.main:app --reload
```

**Terminal 3 - Start Streamlit Frontend:**
```bash
streamlit run frontend/app.py
```

## Usage

### Web Interface
1. Open your browser to `http://localhost:8501`
2. Enter the text you want to summarize in the text area
3. Click "Summarize" to get your AI-generated summary

### API Endpoints

#### POST /summarize/
Summarizes the provided text using LLaMA 2.

**Request:**
```bash
curl -X POST "http://localhost:8000/summarize/" \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -d "text=Your long text here that you want to summarize..."
```

**Response:**
```json
{
  "summary": "AI-generated summary of your text..."
}
```

## API Documentation

Once the FastAPI server is running, you can access:
- **Interactive API docs**: `http://localhost:8000/docs`
- **OpenAPI schema**: `http://localhost:8000/redoc`

## Configuration

### Default Ports
- Streamlit Frontend: `8501`
- FastAPI Backend: `8000`
- Ollama Service: `11434`

### Model Configuration
The application uses the `llama2` model by default. You can modify this in `backend/main.py`:

```python
"model": "llama2",  # Change to other available models
```

## Troubleshooting

### Common Issues

**1. Ollama Connection Error**
```
Error: Connection refused to localhost:11434
```
**Solution:** Ensure Ollama is running with `ollama serve`

**2. Model Not Found**
```
Error: model 'llama2' not found
```
**Solution:** Pull the model with `ollama pull llama2`

**3. Port Already in Use**
```
Error: Port 8000 is already in use
```
**Solution:** Kill the process or use a different port:
```bash
uvicorn backend.main:app --reload --port 8001
```

**4. Frontend Can't Connect to Backend**
```
Connection Error in Streamlit
```
**Solution:** Verify the FastAPI server is running on `http://localhost:8000`

### Performance Tips

- Use shorter texts for faster responses
- Consider using smaller models like `llama2:7b` for better performance
- Ensure adequate RAM (8GB+ recommended for LLaMA 2)

## Development

### Adding New Features
1. Backend changes: Modify `backend/main.py`
2. Frontend changes: Modify `frontend/app.py`
3. Dependencies: Update `requirements.txt`

### Testing the API
Use the interactive docs at `http://localhost:8000/docs` or tools like Postman.

## Requirements

- **Python**: 3.8+
- **RAM**: 8GB+ (for LLaMA 2 model)
- **Storage**: 4GB+ (for model files)
- **OS**: Windows, macOS, or Linux

## License

This project is for educational purposes. Please check the respective licenses for FastAPI, Streamlit, and Ollama/LLaMA usage.

## Contributing

Feel free to submit issues, fork the repository, and create pull requests for any improvements.