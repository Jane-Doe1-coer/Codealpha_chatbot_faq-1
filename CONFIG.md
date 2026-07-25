# FAQ Chatbot Configuration Guide

## Project Configuration Files

### requirements.txt
Contains all Python package dependencies with pinned versions:
```
nltk==3.8.1        # Natural Language Toolkit
spacy==3.7.2       # Advanced NLP (optional)
scikit-learn==1.3.2 # ML and similarity metrics
numpy==1.24.3      # Numerical computing
pandas==2.0.3      # Data manipulation
streamlit==1.28.1  # Web UI framework
```

## Feature Configuration

### 1. Similarity Threshold

**Default:** 0.3 (30%)

Controls how similar a question must be to match an FAQ.

**CLI Configuration:**
```python
# In src/chatbot.py, line ~189
chatbot = FAQChatbot(threshold=0.3)  # Lower = more matches
```

**Web UI Configuration:**
- Use the slider in the left sidebar (real-time adjustment)

**API Configuration:**
```python
matcher = FAQMatcher(threshold=0.4)  # More strict
```

### 2. FAQ Database

**Location:** `data/faqs.json`

**Format:**
```json
{
  "faqs": [
    {
      "id": 1,
      "question": "Sample question?",
      "answer": "Sample answer."
    }
  ]
}
```

**How to add FAQs:**
1. Edit `data/faqs.json`
2. Add new entry with unique ID
3. Restart chatbot (changes auto-load)

### 3. NLP Settings

**Tokenizer:** NLTK punkt

**Stopwords:** English language set

**Lemmatizer:** WordNet

To change language in `preprocessor.py`:
```python
preprocessor = TextPreprocessor(language='spanish')  # Or any NLTK language
```

## Advanced Configuration

### Multiple FAQ Categories

Create separate JSON files for different topics:
```
data/
├── faqs.json           # General FAQs
├── faqs_shipping.json  # Shipping FAQs
├── faqs_payment.json   # Payment FAQs
└── faqs_support.json   # Support FAQs
```

Then load specific category:
```python
matcher = FAQMatcher(faqs_path='../data/faqs_shipping.json')
```

### Custom Preprocessing

Edit `src/preprocessor.py`:

```python
class CustomPreprocessor(TextPreprocessor):
    def preprocess(self, text):
        # Custom processing logic
        cleaned = self.clean_text(text)
        tokens = self.tokenize(cleaned)
        tokens = self.remove_stopwords(tokens)
        # Add custom filters
        tokens = [t for t in tokens if len(t) > 2]  # Remove short words
        tokens = self.lemmatize(tokens)
        return tokens
```

### Performance Tuning

**For small FAQ databases (< 100):**
- Use default settings
- Threshold: 0.3

**For medium databases (100-1000):**
- Threshold: 0.35-0.4
- Consider caching vectors

**For large databases (1000+):**
- Implement indexing (e.g., Elasticsearch)
- Use sparse matrices instead of dense
- Cache TF-IDF vectors

### Memory Optimization

```python
# Current approach: TF-IDF vectors in memory
matcher = FAQMatcher()  # Fast, uses ~1MB per 1000 FAQs

# Alternative: For very large databases
# Save vectors to disk and load on demand
# See advanced_usage.py for examples
```

## Web UI Configuration (Streamlit)

### Customize Appearance

Edit `src/streamlit_app.py`:

```python
st.set_page_config(
    page_title="FAQ Chatbot",
    page_icon="🤖",
    layout="wide",
    initial_sidebar_state="expanded"
)
```

### Add Custom Styling

Add CSS in streamlit_app.py:
```python
st.markdown("""
    <style>
    .custom-class {
        color: red;
        font-weight: bold;
    }
    </style>
""", unsafe_allow_html=True)
```

### Deployment Configuration

**Local Streamlit:**
```bash
streamlit run src/streamlit_app.py
```

**Streamlit Cloud:**
1. Create GitHub repository
2. Push code
3. Go to share.streamlit.io
4. Deploy from GitHub

## API Configuration

### Flask API

Edit `src/api.py` for custom endpoints:

```python
@app.route('/api/custom', methods=['POST'])
def custom_endpoint():
    # Custom logic
    return jsonify({'result': 'data'})
```

### CORS Configuration (for cross-origin requests)

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # Enable CORS for all routes
```

### Authentication (Optional)

```python
from functools import wraps
from flask import request

def require_api_key(f):
    @wraps(f)
    def decorated_function(*args, **kwargs):
        api_key = request.headers.get('X-API-Key')
        if not api_key or api_key != 'your-secret-key':
            return {'error': 'Unauthorized'}, 401
        return f(*args, **kwargs)
    return decorated_function

@app.route('/api/ask', methods=['POST'])
@require_api_key
def ask_question():
    # Protected endpoint
    ...
```

## Logging Configuration

Add logging to track usage:

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    filename='faq_chatbot.log'
)

logger = logging.getLogger(__name__)

def process_question(question):
    logger.info(f"Processing question: {question}")
    result = matcher.find_best_match(question)
    logger.info(f"Result: {result['faq_id']} ({result['similarity_score']:.1%})")
    return result
```

## Database Integration (SQLite)

Replace JSON with SQLite:

```python
import sqlite3

class FAQDatabase:
    def __init__(self, db_path='faqs.db'):
        self.conn = sqlite3.connect(db_path)
        self.cursor = self.conn.cursor()
        self._create_tables()
    
    def _create_tables(self):
        self.cursor.execute('''
            CREATE TABLE IF NOT EXISTS faqs (
                id INTEGER PRIMARY KEY,
                question TEXT NOT NULL,
                answer TEXT NOT NULL
            )
        ''')
        self.conn.commit()
    
    def add_faq(self, question, answer):
        self.cursor.execute(
            'INSERT INTO faqs (question, answer) VALUES (?, ?)',
            (question, answer)
        )
        self.conn.commit()
    
    def get_all_faqs(self):
        self.cursor.execute('SELECT * FROM faqs')
        return [{'id': r[0], 'question': r[1], 'answer': r[2]} 
                for r in self.cursor.fetchall()]
```

## Environment Variables

Create `.env` file:

```
FAQ_DB_PATH=../data/faqs.json
SIMILARITY_THRESHOLD=0.3
LOG_LEVEL=INFO
API_PORT=5000
DEBUG_MODE=False
```

Load in Python:

```python
import os
from dotenv import load_dotenv

load_dotenv()

FAQ_DB = os.getenv('FAQ_DB_PATH', '../data/faqs.json')
THRESHOLD = float(os.getenv('SIMILARITY_THRESHOLD', '0.3'))
DEBUG = os.getenv('DEBUG_MODE') == 'True'
```

## Testing Configuration

Create `tests/test_chatbot.py`:

```python
import pytest
from src.faq_matcher import FAQMatcher

def test_exact_match():
    matcher = FAQMatcher()
    result = matcher.find_best_match("How long does shipping take?")
    assert result['success'] is True
    assert result['faq_id'] == 2

def test_threshold():
    matcher = FAQMatcher(threshold=0.9)
    result = matcher.find_best_match("purple unicorn")
    assert result['success'] is False

if __name__ == '__main__':
    pytest.main([__file__])
```

Run tests:
```bash
pip install pytest
pytest tests/
```

## Production Deployment Checklist

- [ ] Set `DEBUG=False`
- [ ] Configure proper error handling
- [ ] Set up logging
- [ ] Use environment variables for secrets
- [ ] Enable CORS if needed
- [ ] Add authentication
- [ ] Cache FAQ vectors
- [ ] Set up monitoring
- [ ] Configure rate limiting
- [ ] Use production WSGI server (Gunicorn, uWSGI)

## Performance Metrics

Monitor these metrics:

1. **Response Time:** < 100ms for similarity matching
2. **Memory Usage:** ~1MB per 1000 FAQs
3. **Accuracy:** % of user questions that get good matches
4. **User Satisfaction:** % of users satisfied with answers

## Troubleshooting Configuration Issues

| Issue | Check |
|-------|-------|
| Slow responses | Reduce FAQ database size or increase threshold |
| High memory | Implement lazy loading or external indexing |
| Poor matches | Lower threshold or add more FAQs |
| Unicode errors | Ensure `utf-8` encoding in JSON |
| NLTK data missing | Run `nltk.download()` or set NLTK_DATA path |

## References

- NLTK Documentation: https://www.nltk.org/
- Scikit-learn TF-IDF: https://scikit-learn.org/stable/modules/feature_extraction.html#tfidf
- Streamlit Docs: https://docs.streamlit.io/
- Flask Documentation: https://flask.palletsprojects.com/
