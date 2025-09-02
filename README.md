# 🎥 YouTube RAG Pipeline with LangChain

![Python](https://img.shields.io/badge/python-3.12+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![RAG](https://img.shields.io/badge/RAG-LangChain-orange.svg)
[![Issues](https://img.shields.io/github/issues/ZohaibCodez/rag-using-langchain.svg)](https://github.com/ZohaibCodez/rag-using-langchain/issues)
![Last Commit](https://img.shields.io/github/last-commit/ZohaibCodez/rag-using-langchain)
[![Stars](https://img.shields.io/github/stars/ZohaibCodez/rag-using-langchain?style=social)](https://github.com/ZohaibCodez/rag-using-langchain/stargazers)
[![Forks](https://img.shields.io/github/forks/ZohaibCodez/rag-using-langchain?style=social)](https://github.com/ZohaibCodez/rag-using-langchain/network/members)

A minimal **Retrieval-Augmented Generation (RAG)** pipeline built in Jupyter/Colab that transforms YouTube videos into an intelligent Q&A system. Extract transcripts, build vector embeddings, and chat with video content using Google's Gemini AI.

## 🚀 What This Project Does

- **📥 Ingests** YouTube transcripts via `youtube-transcript-api`
- **✂️ Splits** text into chunks using `RecursiveCharacterTextSplitter`
- **🧠 Embeds** chunks with Google's `embedding-001` model
- **🔍 Indexes** vectors in FAISS (in-memory vector store)
- **🎯 Retrieves** top-k most relevant chunks for questions
- **💬 Generates** contextual answers using Gemini 1.5 Flash
- **⚡ Processes** ~30min video transcripts in ~2-3 minutes

## 🏗️ Project Structure

```
├── rag_notebook.ipynb     # Main pipeline (Colab-friendly)
├── pyproject.toml         # Dependencies & project config
├── uv.lock               # Locked dependencies
├── data/
│   └── sample_data.json  # Sample transcript data
├── .env.example          # Environment variables template
├── .gitignore           # Git ignore file
└── README.md            # This file
```

## 🛠️ Installation

### Option 1: Using `uv` (Recommended)
```bash
git clone https://github.com/yourusername/youtube-rag-langchain
cd youtube-rag-langchain
uv sync
```

### Option 2: Using `pip`
```bash
git clone https://github.com/yourusername/youtube-rag-langchain
cd youtube-rag-langchain
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## ⚙️ Setup

1. **Get Google API Key**: Visit [Google AI Studio](https://makersuite.google.com/app/apikey)

2. **Create `.env` file**:
```bash
cp .env.example .env
# Edit .env and add your key:
GOOGLE_API_KEY=your_google_api_key_here
```

3. **Open the notebook**:
```bash
jupyter lab rag_notebook.ipynb
# OR open in VS Code, Colab, etc.
```

## 🎮 Usage

1. **Run the notebook cells in order**
2. **Set your target video**:
   ```python
   video_id = "your_youtube_video_id_here"  # From URL: youtube.com/watch?v=VIDEO_ID
   ```
3. **Ask questions about the video**:
   ```python
   query = "What are the main points discussed?"
   answer = chain.invoke({"input": query})
   print(answer)
   ```

## 💡 Demo Example

```python
# Using the sample data (Lex Fridman podcast excerpt)
query = "What topics are covered in this conversation?"

# Output:
"""
Based on the retrieved context, the conversation covers several key topics:
1. Artificial intelligence and machine learning developments
2. The future of technology and its impact on society
3. Philosophical discussions about consciousness and intelligence
4. Personal experiences in the tech industry
...
"""
```

## 📋 Requirements

- **Python**: 3.12+
- **Google API Key**: With Gemini access
- **Dependencies**: Managed via `uv` or `pip`
- **Memory**: ~500MB for typical video transcripts

## 🔧 Key Components

| Component | Purpose | Model/Config |
|-----------|---------|--------------|
| **Transcript Extraction** | Get video captions | `youtube-transcript-api` |
| **Text Splitting** | Chunk into manageable pieces | 1000 chars, 200 overlap |
| **Embeddings** | Convert text to vectors | `models/embedding-001` |
| **Vector Store** | Similarity search | FAISS (in-memory) |
| **Retrieval** | Find relevant chunks | Top-4 similar |
| **Generation** | Answer questions | `gemini-1.5-flash` |

## ⚠️ Current Limitations

- **Memory-only storage**: FAISS index doesn't persist between sessions
- **No citations**: Answers don't show which video segments were used
- **Single video**: Processes one video at a time
- **Caption dependency**: Requires available YouTube captions
- **Rate limits**: YouTube may block frequent transcript requests

## 🔮 Potential Extensions

- [ ] **Persistent storage**: Save FAISS index to disk
- [ ] **Web UI**: Streamlit/Gradio interface
- [ ] **Multi-video support**: Index multiple videos simultaneously
- [ ] **Citation tracking**: Show source timestamps in answers
- [ ] **Evaluation metrics**: Add RAGAS or similar evaluation
- [ ] **Docker support**: Containerized deployment
- [ ] **Streaming responses**: Real-time answer generation

## 🐛 Troubleshooting

**"Transcripts are disabled"**: Video doesn't have captions available
- Try a different video with captions enabled

**Authentication errors**: Invalid Google API key
- Verify your `GOOGLE_API_KEY` in `.env`
- Check API key has Gemini access enabled

**Empty/poor answers**: Low-quality retrieval
- Increase `k` parameter (more chunks retrieved)
- Adjust chunk size/overlap in text splitter
- Refine the prompt template

**Rate limiting**: YouTube blocking transcript requests
- Use the provided `sample_data.json` for testing
- Wait between requests or use different videos

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **LangChain** for the RAG framework
- **FAISS** for efficient vector similarity search
- **Google** for Gemini AI and embedding models
- **YouTube Transcript API** for transcript extraction

---

**⭐ If this project helps you, please star the repository!**

Built with ❤️ for learning and sharing RAG concepts.