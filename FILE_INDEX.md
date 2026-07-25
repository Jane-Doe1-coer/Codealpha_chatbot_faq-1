# FAQ Chatbot - File Index

## 📁 Complete File Structure

### Root Directory: `d:\ai\faq-chatbot\`

```
faq-chatbot/
│
├── 📄 README.md                    ⭐ MAIN DOCUMENTATION
│   └── Complete feature guide, installation, troubleshooting
│
├── 📄 QUICKSTART.md                ⭐ START HERE (2 min)
│   └── Quick setup and 4 interface options
│
├── 📄 PROJECT_SUMMARY.md           ⭐ THIS PROJECT OVERVIEW
│   └── What's been created, features, examples
│
├── 📄 CONFIG.md                    🔧 ADVANCED CONFIGURATION
│   └── Threshold, FAQs, performance tuning, deployment
│
├── 📄 requirements.txt             📦 DEPENDENCIES
│   └── All Python packages needed
│
├── data/
│   └── 📄 faqs.json               📚 FAQ DATABASE
│       └── 10 sample FAQs about e-commerce (edit to customize)
│
└── src/
    ├── 📄 preprocessor.py         🧹 NLP PREPROCESSING
    │   ├── TextPreprocessor class
    │   ├── Text cleaning, tokenization, lemmatization
    │   └── Uses NLTK library
    │
    ├── 📄 faq_matcher.py          🎯 SIMILARITY MATCHING
    │   ├── FAQMatcher class
    │   ├── TF-IDF vectorization
    │   ├── Cosine similarity calculation
    │   └── Threshold-based filtering
    │
    ├── 📄 chatbot.py              💬 CLI INTERFACE
    │   ├── FAQChatbot class
    │   ├── Interactive command-line mode
    │   ├── Commands: ask, suggest, browse, history
    │   └── run_interactive_mode() main entry point
    │
    ├── 📄 streamlit_app.py        🌐 WEB UI (RECOMMENDED)
    │   ├── 3-tab interface: Chat, Browse, Analytics
    │   ├── Real-time threshold adjustment
    │   ├── Conversation history
    │   └── Beautiful charts and statistics
    │
    ├── 📄 api.py                  🔌 REST API & FLASK
    │   ├── FAQChatbotAPI class
    │   ├── REST endpoints for integration
    │   ├── create_flask_app() function
    │   ├── Session management
    │   └── Example curl commands included
    │
    └── 📄 examples.py             📖 DEMONSTRATIONS
        ├── 6 runnable examples
        ├── Example 1: Basic matching
        ├── Example 2: Top-K matches
        ├── Example 3: Preprocessing
        ├── Example 4: Batch processing
        ├── Example 5: Threshold impact
        └── Example 6: Similarity comparison
```

## 🎯 File Usage Guide

### For Getting Started
1. **First read:** QUICKSTART.md (2 minutes)
2. **Then run:** One of the 4 interfaces
3. **Understand:** How it works in PROJECT_SUMMARY.md

### For Using the Chatbot
- **CLI Users:** Run `python src/chatbot.py`
- **Web Users:** Run `streamlit run src/streamlit_app.py`
- **Developers:** Use `src/faq_matcher.py` directly
- **API Users:** Deploy `src/api.py` with Flask

### For Customization
- **FAQ Content:** Edit `data/faqs.json`
- **Behavior:** Read `CONFIG.md`
- **Advanced:** Study code in `src/` directory
- **Examples:** Run `python src/examples.py`

### For Understanding
- **Full Details:** README.md (comprehensive)
- **Architecture:** PROJECT_SUMMARY.md (technical overview)
- **Configuration:** CONFIG.md (settings & tuning)
- **Code Examples:** examples.py (runnable code)

## 📚 Documentation Priority

```
START HERE
    ↓
QUICKSTART.md (get it running)
    ↓
Depends on your use case...
    │
    ├→ CLI User? → Read "CLI Chatbot" section in README.md
    ├→ Web User? → Streamlit UI is self-explanatory  
    ├→ Developer? → Read PROJECT_SUMMARY.md + code comments
    └→ Need details? → Read full README.md
    ↓
CONFIG.md (if customizing)
    ↓
examples.py (if coding)
```

## 🔍 File Dependencies

```
faqs.json (data source)
    ↓
preprocessor.py → faq_matcher.py
    ↓
    ├→ chatbot.py (CLI)
    ├→ streamlit_app.py (Web UI)
    └→ api.py (REST API)
        ↓
    examples.py (demonstrations)
```

## 📖 Documentation by Topic

### Getting Started
- **QUICKSTART.md** - Installation & running
- **PROJECT_SUMMARY.md** - What's included
- **README.md** - Full features

### Using the Chatbot
- **CLI:** chatbot.py + README.md
- **Web:** streamlit_app.py (self-explanatory UI)
- **API:** api.py + CONFIG.md
- **Code:** examples.py + docstrings

### Customization
- **Add FAQs:** Edit data/faqs.json
- **Change behavior:** CONFIG.md
- **Extend features:** Study src/ code
- **Deploy:** CONFIG.md + README.md

### Troubleshooting
- **Installation issues:** QUICKSTART.md
- **Runtime errors:** README.md troubleshooting section
- **Configuration:** CONFIG.md
- **Code errors:** Check code comments and docstrings

## 🎓 Code Structure

### preprocessor.py
```
TextPreprocessor class
├── __init__(language='english')
├── clean_text(text) → str
├── tokenize(text) → list
├── remove_stopwords(tokens) → list
├── lemmatize(tokens) → list
└── preprocess(text) → list [MAIN]
    preprocess_to_string(text) → str
```

### faq_matcher.py
```
FAQMatcher class
├── __init__(faqs_path, threshold)
├── _load_faqs(faqs_path) → list
├── _build_vectors() → None
├── find_best_match(question) → dict [MAIN]
├── find_top_matches(question, k) → list
└── get_all_faqs() → list
```

### chatbot.py
```
FAQChatbot class
├── __init__(faqs_path, threshold)
├── process_question(user_input) → dict
├── get_suggestions(user_input) → list
├── get_random_faq() → dict
├── get_conversation_history() → list
├── reset_conversation() → None
├── print_welcome_message() → None
├── print_help() → None
├── print_faq(faq) → None
├── display_all_faqs() → None
└── run_interactive_mode() [MAIN]
```

### streamlit_app.py
```
Main Components:
├── Page configuration
├── Session state management
├── Sidebar (settings & help)
├── Tab 1: Chat
│   ├── Conversation display
│   ├── Question input
│   ├── Ask button
│   └── Suggestions button
├── Tab 2: Browse FAQs
│   ├── Expandable FAQ list
│   └── FAQ table
└── Tab 3: Analytics
    ├── Statistics (questions, responses)
    └── Charts (similarity distribution)
```

### api.py
```
FAQChatbotAPI class
├── __init__(faqs_path, threshold)
├── create_session() → dict
├── ask_question(question, session_id) → dict
├── get_suggestions(question, top_k) → dict
├── search_faq(keyword) → dict
├── get_faq_by_id(faq_id) → dict
├── list_all_faqs(skip, limit) → dict
├── get_stats() → dict
└── update_threshold(new_threshold) → dict

Flask Integration:
└── create_flask_app() → Flask app
    ├── /api/ask [POST]
    ├── /api/suggest [POST]
    ├── /api/search [GET]
    ├── /api/faq/<id> [GET]
    ├── /api/faqs [GET]
    ├── /api/stats [GET]
    └── /api/threshold [POST]
```

### examples.py
```
Demonstrations:
├── example_basic_matching()
├── example_top_matches()
├── example_preprocessing()
├── example_batch_processing()
├── example_custom_threshold()
└── example_similarity_comparison()
```

## 🚀 Quick Reference

### Run CLI Chatbot
```bash
cd d:\ai\faq-chatbot\src
python chatbot.py
```

### Run Web UI
```bash
cd d:\ai\faq-chatbot\src
streamlit run streamlit_app.py
```

### Run Examples
```bash
cd d:\ai\faq-chatbot\src
python examples.py
```

### Use in Code
```python
from faq_matcher import FAQMatcher
matcher = FAQMatcher()
result = matcher.find_best_match("Your question?")
```

### Start Flask API
```bash
cd d:\ai\faq-chatbot\src
python api.py
```

## 📊 File Sizes & Complexity

| File | Size | Complexity | Purpose |
|------|------|-----------|---------|
| preprocessor.py | ~4KB | Low | NLP preprocessing |
| faq_matcher.py | ~5KB | Medium | Similarity matching |
| chatbot.py | ~8KB | Medium | CLI interface |
| streamlit_app.py | ~9KB | Medium | Web UI |
| api.py | ~9KB | Medium | REST API |
| examples.py | ~6KB | Low | Code examples |
| faqs.json | ~2KB | None | Data file |
| README.md | ~12KB | None | Documentation |
| CONFIG.md | ~10KB | None | Configuration |

**Total Project:** ~65KB of code + documentation

## 🎯 Entry Points

**For End Users:**
- `python src/chatbot.py` (CLI)
- `streamlit run src/streamlit_app.py` (Web)

**For Developers:**
- `from faq_matcher import FAQMatcher`
- `from api import FAQChatbotAPI`
- `python src/examples.py`

**For Integration:**
- `python src/api.py` (Flask API)
- Import and use classes directly

## ✅ All Files Ready

All files are created and ready to use. No further setup needed beyond:
1. `pip install -r requirements.txt`
2. Choose your interface
3. Run!

Enjoy your FAQ Chatbot! 🚀
