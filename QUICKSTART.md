# Quick Start Guide for FAQ Chatbot

## Installation (2 minutes)

```bash
cd faq-chatbot
pip install -r requirements.txt
```

## Choose Your Interface

### Option A: CLI Chatbot (Fastest)

```bash
cd src
python chatbot.py
```

Then interact with the chatbot:
```
You: How long does shipping take?
Bot: Standard shipping takes 5-7 business days...
[Matched FAQ #2 with 95% relevance]
```

**Commands:**
- Type any question directly
- Type `browse` to see all FAQs
- Type `suggest` for random FAQs
- Type `help` for more commands
- Type `quit` to exit

---

### Option B: Web UI (Most User-Friendly)

```bash
cd src
streamlit run streamlit_app.py
```

Open browser to `http://localhost:8501`

Features:
- 💬 **Chat Tab** - Ask questions interactively
- 📚 **Browse Tab** - View all FAQs
- 📊 **Analytics Tab** - See statistics
- ⚙️ **Settings** - Adjust similarity threshold

---

### Option C: Python API (For Developers)

```python
from faq_matcher import FAQMatcher

matcher = FAQMatcher(threshold=0.3)
result = matcher.find_best_match("How long does shipping take?")

if result['success']:
    print(result['answer'])
    print(f"Confidence: {result['similarity_score']:.1%}")
else:
    print("No good match found")
    suggestions = matcher.find_top_matches("How long does shipping take?", top_k=3)
    for match in suggestions:
        print(f"- {match['question']}")
```

---

### Option D: Flask REST API (For Web Integration)

```python
from api import create_flask_app

app = create_flask_app()
app.run(debug=True, port=5000)
```

Then make requests:
```bash
# Ask a question
curl -X POST http://localhost:5000/api/ask \
  -H "Content-Type: application/json" \
  -d '{"question": "How long does shipping take?"}'

# Get suggestions
curl -X POST http://localhost:5000/api/suggest \
  -H "Content-Type: application/json" \
  -d '{"question": "What about returns?", "top_k": 3}'

# Search FAQs
curl http://localhost:5000/api/search?keyword=shipping

# List all FAQs
curl http://localhost:5000/api/faqs
```

---

## Test Examples

Run example demonstrations:

```bash
cd src
python examples.py
```

This shows:
1. Basic question matching
2. Top-K matching
3. Text preprocessing
4. Batch processing
5. Threshold impact
6. Similarity comparison

---

## Customize FAQs

Edit `data/faqs.json` to add your own questions and answers:

```json
{
  "faqs": [
    {
      "id": 1,
      "question": "Your question here?",
      "answer": "Your answer here."
    }
  ]
}
```

---

## How It Works (30-second version)

1. **You ask a question** - User inputs a query
2. **Text preprocessing** - Question is cleaned, tokenized, lemmatized
3. **Vectorization** - Question converted to numerical vector using TF-IDF
4. **Similarity search** - Compared against all FAQ questions using cosine similarity
5. **Return answer** - Best matching FAQ answer is returned with confidence score

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| NLTK data not found | Data downloads automatically on first run. If stuck, run: `python -m nltk.downloader punkt stopwords wordnet` |
| Questions don't match | Try lowering the similarity threshold in settings |
| Streamlit won't start | Make sure you're in the `src` directory |
| Import errors | Run: `pip install -r requirements.txt` |

---

## Files Overview

- **data/faqs.json** - Your FAQ database
- **src/preprocessor.py** - NLP preprocessing (tokenization, lemmatization)
- **src/faq_matcher.py** - TF-IDF vectorization and similarity matching
- **src/chatbot.py** - CLI interface
- **src/streamlit_app.py** - Web UI
- **src/api.py** - REST API and Flask integration
- **src/examples.py** - Usage examples

---

## Next Steps

1. ✅ Run the chatbot in your preferred interface
2. ✅ Test with the provided sample FAQs
3. ✅ Add your own FAQs to `data/faqs.json`
4. ✅ Adjust similarity threshold as needed
5. ✅ Deploy as API or web app in production

---

## Questions?

Check the full README.md for detailed documentation and advanced features!
