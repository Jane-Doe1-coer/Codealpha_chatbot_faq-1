# 🚀 Web UI - Start Here!

## What You Get

A **beautiful, modern, professional web interface** for your FAQ Chatbot:
- 🌟 Modern glassmorphic design
- 💬 Real-time chat interface
- 📊 Live analytics dashboard
- 🎨 Dark mode support
- 📱 Fully responsive
- ⚡ Fast & smooth

## Quick Start (2 Minutes)

### 1️⃣ Install Dependencies
```bash
cd d:\ai\faq-chatbot
pip install -r requirements.txt
```

### 2️⃣ Start Web Server
```bash
cd src
python web_server.py
```

You should see:
```
============================================================
   FAQ CHATBOT - WEB UI SERVER
============================================================

✨ Starting Flask server...

🌐 Open your browser to: http://localhost:5000
...
```

### 3️⃣ Open Browser
**Go to:** http://localhost:5000

**Done!** 🎉 Your web UI is ready!

---

## 4 Main Tabs

### 💬 Chat Tab
Ask questions and get answers instantly!

**Features:**
- Type your question
- Click "Send" or press Enter
- See answer with confidence %
- Get suggestions for unclear questions
- "Get Suggestions" button
- "Random FAQ" button

**Example:**
```
Type: "How long does shipping take?"
Bot: "Standard shipping takes 5-7 business days..."
Relevance: 95% ✓
```

---

### 📚 Browse Tab
Explore all FAQs in one place

**Features:**
- Search box to filter FAQs
- Click to expand any FAQ
- See question & full answer
- FAQ ID badge
- Smooth animations

**How to:**
1. Type in search box (e.g., "shipping")
2. FAQs filter in real-time
3. Click to expand
4. Read answer

---

### 📊 Analytics Tab
See statistics and charts

**4 Statistics:**
- 📝 Total Questions asked
- ✅ Matched Answers
- 📈 Average Relevance %
- ⏱️ Session Duration

**2 Charts:**
- Relevance Score Distribution
- Match Success Rate

**Recent Activity:**
- Last 5 questions

*Updates live as you chat!*

---

### ⚙️ Settings Tab
Customize your experience

**Threshold Slider:**
- Lower (0.0) = More matches
- Higher (1.0) = Strict matching
- Default: 0.3 (30%)

**Checkboxes:**
- ☑️ Auto-show suggestions
- ☑️ Show relevance scores
- ☑️ Enable notifications

**Actions:**
- 💾 Save Settings (LocalStorage)
- 📥 Export Settings (JSON file)

---

## Top Navigation

### Left Side
🤖 **Logo** - Click to refresh

### Center
**Tabs:** Chat | Browse | Analytics | Settings

### Right Side
**Buttons:**
- 🌙 Dark Mode Toggle
- 🗑️ Clear Chat History

---

## Features Highlight

### 🌓 Dark Mode
Click moon icon in top-right to toggle dark/light mode. Your preference is saved!

### 🔔 Notifications
Toast messages appear at bottom for:
- ✓ Success (green)
- ✗ Error (red)
- ⚠️ Warning (yellow)

### 💬 Chat Messages
- **Blue bubbles** = Your questions
- **Gray bubbles** = Bot answers
- **Timestamps** = When sent

### 🎯 Relevance Badges
Shows confidence in answer:
- Green (80-100%) = Great match
- Yellow (40-80%) = Good match
- Red (0-40%) = Poor match

### 💡 Suggestions
If bot can't find good answer, shows similar FAQs you can click on!

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| **Enter** | Send message |
| **Escape** | Close any popup |
| **Tab** | Navigate between sections |

---

## Responsive Design

Works great on any device:

**Desktop** 🖥️
- Full experience
- All features visible
- Charts visible
- Optimal spacing

**Tablet** 📱
- Adapted layout
- Touch-friendly
- Readable text
- Optimized spacing

**Mobile** 📲
- Vertical layout
- Large buttons
- Full-width input
- Scrollable content

---

## Common Tasks

### Change Matching Sensitivity
1. Go to **Settings** tab
2. Move **Threshold Slider**
   - Move LEFT for more matches
   - Move RIGHT for stricter matching
3. Click **Save Settings**

### Add Your Own FAQs
1. Edit `data/faqs.json`
2. Add new FAQ entries:
   ```json
   {
     "id": 11,
     "question": "Your question?",
     "answer": "Your answer."
   }
   ```
3. Restart web server
4. FAQs automatically load!

### Enable Dark Mode
1. Click **Moon icon** (top-right)
2. Theme persists on refresh!

### Export Your Settings
1. Go to **Settings** tab
2. Click **Export Settings**
3. JSON file downloads with:
   - Your settings
   - Chat history
   - Session info

### Search FAQs
1. Go to **Browse** tab
2. Type in search box
3. Results filter in real-time
4. Click to expand
5. Read answer

---

## Troubleshooting

### Server won't start
```bash
# Is port 5000 in use?
# Try different port - edit web_server.py:
# Change: app.run(port=5000)
# To:     app.run(port=8000)
python web_server.py  # Try again
```

### Browser shows blank page
- Check browser console (F12)
- Ensure Flask server is running
- Clear cache (Ctrl+Shift+Delete)
- Try different browser

### Settings don't save
- Browser must allow localStorage
- Check privacy settings
- Try incognito mode
- Try different browser

### Charts not showing
- Charts need JavaScript enabled
- Try different browser
- Check console for errors

### Questions don't get answers
- Check similar questions in Browse
- Adjust threshold (lower = more matches)
- Ensure FAQs are in `data/faqs.json`
- Restart server if you added FAQs

---

## What's Happening Behind the Scenes?

```
1. You Type Question
        ↓
2. JavaScript sends to Flask Server
        ↓
3. Flask calls faq_matcher.py
        ↓
4. NLP preprocessing (clean, tokenize, lemmatize)
        ↓
5. TF-IDF vectorization
        ↓
6. Cosine similarity matching
        ↓
7. Flask returns answer
        ↓
8. JavaScript displays in chat
        ↓
9. Analytics updated
```

All happens in **< 100ms**! ⚡

---

## File Overview

| File | Purpose |
|------|---------|
| **index.html** | Web page structure |
| **styles.css** | Beautiful styling |
| **script.js** | Interactive features |
| **web_server.py** | Flask web server |

---

## API Endpoints (For Developers)

The web UI uses these APIs:

```
POST /api/ask              → Get answer
POST /api/suggest          → Get suggestions
GET  /api/search           → Search FAQs
GET  /api/faqs             → Get all FAQs
GET  /api/stats            → Get statistics
POST /api/threshold        → Change threshold
GET  /health               → Health check
```

---

## Tips & Tricks

💡 **Tip 1:** Use exact phrases for better matches
```
Good: "How long for shipping?"
Better: "What's the shipping time?"
```

💡 **Tip 2:** Try suggestions if first answer isn't helpful
```
If bot says "unclear", click suggested questions!
```

💡 **Tip 3:** Adjust threshold based on needs
```
Customer support? Lower threshold (0.2-0.3)
Strict answers? Higher threshold (0.5-0.7)
```

💡 **Tip 4:** Browse all FAQs first
```
Use Browse tab to see available questions
Makes it easier to ask good questions!
```

💡 **Tip 5:** Check analytics for patterns
```
What questions do people ask most?
Which topics need more FAQs?
```

---

## What Makes This UI Great? ✨

✅ **Modern Design**
- Gradient colors
- Smooth shadows
- Rounded corners
- Professional look

✅ **Fast Performance**
- No lag in chat
- Smooth animations
- Quick loading
- Responsive buttons

✅ **User Friendly**
- Intuitive layout
- Clear instructions
- Helpful messages
- Easy navigation

✅ **Feature Rich**
- 4 complete tabs
- Live charts
- Dark mode
- Export/settings

✅ **Fully Responsive**
- Desktop ✓
- Tablet ✓
- Mobile ✓
- All sizes

---

## Next Steps

1. ✅ Start web server
2. ✅ Open in browser
3. ✅ Try asking questions
4. ✅ Browse FAQs
5. ✅ Check analytics
6. ✅ Customize settings
7. ✅ Add your own FAQs

---

## Need More Help?

📖 **Full Documentation:** See `WEB_UI_GUIDE.md`
📚 **Main README:** See `README.md`
⚙️ **Configuration:** See `CONFIG.md`
💻 **Code Examples:** See `examples.py`

---

**Enjoy your FAQ Chatbot! 🚀**

*Built with HTML • CSS • JavaScript • Flask*
