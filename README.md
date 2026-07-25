# FAQ Chatbot

A sophisticated FAQ chatbot that matches user questions to relevant answers using NLP preprocessing and cosine similarity matching.

## Features

✨ **Core Features:**
- 🤖 Intelligent question matching using TF-IDF vectorization and cosine similarity
- 🧹 NLP preprocessing with NLTK (tokenization, stopword removal, lemmatization)
- 🎯 Configurable similarity threshold for answer matching
- 💬 Interactive CLI chatbot interface
- 🌐 Web UI with Streamlit for easy interaction
- 📊 Conversation analytics and chat history
- 💡 Suggestion system for low-confidence matches

## Project Structure

```
faq-chatbot/
├── data/
│   └── faqs.json                 # FAQ database
├── src/
│   ├── preprocessor.py           # NLP preprocessing module
│   ├── faq_matcher.py            # FAQ matching with cosine similarity
│   ├── chatbot.py                # CLI chatbot interface
│   └── streamlit_app.py          # Web UI
├── requirements.txt              # Python dependencies
└── README.md                      # This file
```

## Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)

### Setup

1. **Clone/Navigate to the project:**
   ```bash
   cd faq-chatbot
   ```

2. **Create a virtual environment (optional but recommended):**
   ```bash
   # On Windows
   python -m venv venv
   venv\Scripts\activate
   
   # On macOS/Linux
   python -m venv venv
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Option 1: CLI Chatbot (Interactive Mode)

```bash
cd src
python chatbot.py
```

**Available commands:**
- `ask <question>` - Ask a specific question
- `suggest` - Get random FAQ suggestions
- `browse` - View all FAQs
- `history` - Show conversation history
- `help` - Show help menu
- `quit` - Exit the chatbot

**Example:**
```
You: How long does shipping take?
Bot: Standard shipping takes 5-7 business days. Express shipping takes 2-3 business days. 
Overnight shipping is available for an additional fee.
[Matched FAQ #2 with 95% relevance]
```

### Option 2: Web UI with Streamlit

```bash
cd src
streamlit run streamlit_app.py
```

Then open your browser to `http://localhost:8501`

**Features:**
- 💬 **Chat Tab:** Ask questions and get answers with relevance scores
- 📚 **Browse Tab:** View all FAQs in expandable format
- 📊 **Analytics Tab:** View conversation statistics and patterns
- ⚙️ **Settings:** Adjust similarity threshold in real-time

## How It Works

### 1. **Text Preprocessing (preprocessor.py)**
- **Cleaning:** Removes special characters, converts to lowercase
- **Tokenization:** Splits text into individual words using NLTK
- **Stopword Removal:** Removes common words (the, is, a, etc.)
- **Lemmatization:** Converts words to base form (running → run)

### 2. **FAQ Matching (faq_matcher.py)**
- **TF-IDF Vectorization:** Converts text into numerical vectors
- **Cosine Similarity:** Measures similarity between user question and FAQ questions
- **Threshold Filtering:** Only returns answers above confidence threshold
- **Top-K Matching:** Can return multiple suggestions

### 3. **Similarity Scoring**
- Scores range from 0.0 (no match) to 1.0 (perfect match)
- Default threshold: 0.3 (30% similarity)
- Adjustable via settings in web UI or code

## Configuration

### Adjusting Similarity Threshold

**In CLI:**
Edit `src/chatbot.py`:
```python
chatbot = FAQChatbot(threshold=0.3)  # Increase for stricter matching
```

**In Web UI:**
Use the slider in the left sidebar to adjust in real-time.

### Adding Custom FAQs

Edit `data/faqs.json`:
```json
{
  "faqs": [
    {
      "id": 11,
      "question": "Your custom question?",
      "answer": "Your custom answer here."
    }
  ]
}
```

## Example Interactions

### Exact Match
```
User: How long does shipping take?
Bot: Standard shipping takes 5-7 business days...
[Relevance: 95%]
```

### Paraphrased Question
```
User: What's your shipping timeline?
Bot: Standard shipping takes 5-7 business days...
[Relevance: 82%]
```

### Low Confidence
```
User: Do you have a purple unicorn?
Bot: I'm not sure about your question. Please rephrase it.
[Relevance: 15%]

Did you mean:
1. Do you have a loyalty program?
2. What payment methods do you accept?
3. Do you offer international shipping?
```

## Dependencies

- **nltk** (3.8.1) - Natural Language Toolkit for text processing
- **spacy** (3.7.2) - Industrial-strength NLP (optional, for advanced use)
- **scikit-learn** (1.3.2) - Machine learning library for TF-IDF and similarity
- **numpy** (1.24.3) - Numerical computing
- **pandas** (2.0.3) - Data manipulation
- **streamlit** (1.28.1) - Web framework for UI

## Performance Notes

- **Small FAQ Database:** ✅ Excellent performance (instant responses)
- **Medium FAQ Database (100-1000 FAQs):** ✅ Good performance
- **Large FAQ Database (1000+ FAQs):** Consider caching or indexing optimizations

## Troubleshooting

### Issue: "No module named 'nltk'"
**Solution:** Install dependencies: `pip install -r requirements.txt`

### Issue: NLTK data not found
**Solution:** The preprocessor automatically downloads required data on first run. If it fails:
```python
import nltk
nltk.download('punkt')
nltk.download('stopwords')
nltk.download('wordnet')
```

### Issue: Questions not matching well
**Solution:** 
- Lower the similarity threshold in settings
- Add more varied FAQs
- Verify FAQs are clear and specific

### Issue: Streamlit app won't start
**Solution:** Ensure you're in the `src` directory and run:
```bash
streamlit run streamlit_app.py
```

## Future Enhancements

- 🧠 Add semantic understanding with transformers (BERT)
- 💾 Implement FAQ database with SQLite
- 📈 Add learning from user feedback
- 🌍 Multi-language support
- 🔐 User authentication and personalization
- 📞 Integration with support ticketing systems
- 🎨 Enhanced UI with conversation styling
- 📱 Mobile app version

## License

This project is open source and available for educational and commercial use.

## Author

Created as a comprehensive FAQ chatbot demonstration with modern NLP techniques.

## Support

For issues, suggestions, or improvements, please refer to the code comments and documentation.
