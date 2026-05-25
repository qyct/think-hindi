# हिंदी शब्द संग्रह | Hindi Words Collection

A comprehensive Hindi learning toolkit combining a **web-based vocabulary practice app** with a **Python corpus processing pipeline** for generating frequency-ordered Hindi word datasets.

## 🌟 Features

### Web Application (`index.html`)
- 🎲 **Random Word Selection**: Generate random Hindi words from frequency-ordered datasets
- 🔢 **Dual Input Control**: 
  - **Words to Draw**: Number of words to randomly select (default: 50)
  - **FROM MOST FREQ**: Total words to load from most frequent (range: 500-30,000)
- 📊 **Frequency-Based Learning**: Words organized by usage frequency — most common words first
- 📋 **One-Click Copy**: Copy selected words or learning prompts to clipboard
- 🌐 **Modern Design**: Beautiful, responsive UI with warm color palette
- ⚡ **Fast & Lightweight**: Pure HTML/CSS/JS, no dependencies
- 📱 **Mobile Friendly**: Works seamlessly on desktop and mobile devices

### Corpus Processing Pipeline (`main.py`)
- 🔄 **Multi-Source Processing**: Downloads from Wikipedia, Leipzig corpora, HuggingFace, GitHub
- 📈 **Frequency Analysis**: Generates comprehensive word frequency statistics
- 🧹 **Text Cleaning**: Removes punctuation, non-Hindi characters, and normalizes text
- 💾 **Resume Support**: Checkpoint system for interrupted processing
- 📊 **Top 30K Words**: Pre-processed files ready for web app

## 🚀 Quick Start

### Web Application
Simply open `index.html` in your web browser. No build process or dependencies required!

### Corpus Processing
```bash
# Install dependencies
pip install requests beautifulsoup4 pyarrow datasets

# Run full pipeline (download + extract + process)
python main.py

# Or generate top 30,000 split files
python src/split_top_words.py
```

## 📁 Project Structure

```
r_think_hindi/
├── index.html              # Self-contained web app
├── main.py                 # Corpus processing entry point
├── favicon.svg            # Site icon
├── README.md              # This file
├── .gitignore             # Git ignore rules
├── src/                   # Processing modules
│   ├── sources.py        # Data source URLs
│   ├── downloader.py     # File downloaders
│   ├── extractor.py      # Archive extractors
│   ├── processor.py      # Text processing
│   └── split_top_words.py # Word splitting utilities
└── words/                 # Frequency-ordered word files
    ├── hw01.txt          # Words 1-3,000 (most common)
    ├── hw02.txt          # Words 3,001-6,000
    └── ...               # ... hw10.txt (words 27,001-30,000)
```

## 🎯 How It Works

### Web Application

**Word Data Structure**
The app fetches Hindi words from GitHub-hosted files, each containing 3,000 words in frequency order:

```
hw01.txt → Words 1-3,000      (most common)
hw02.txt → Words 3,001-6,000
hw03.txt → Words 6,001-9,000
...
hw10.txt → Words 27,001-30,000 (least common)
```

**Input Controls**
- **Words to Draw**: How many words to randomly select (1 to total loaded)
- **FROM MOST FREQ**: How many total words to load (500 to 30,000)

**Example Usage**

| FROM MOST FREQ | Files Loaded | Vocabulary Level | Best For |
|----------------|--------------|------------------|----------|
| 500 | hw01.txt (partial) | Beginner basics | Absolute starters |
| 3,000 | hw01.txt (full) | Conversational | Daily conversations |
| 10,000 | hw01-hw04.txt | Advanced | Professional/academic |
| 30,000 | hw01-hw10.txt | Comprehensive | Near-complete vocabulary |

**Using the App**
1. Set your parameters with the spinners
2. Click "Draw" to randomly select words
3. Copy words or learning prompts to clipboard
4. Use prompts with AI chatbots for personalized learning

### Corpus Processing Pipeline

**Data Sources**
- **Wikipedia**: All Hindi articles (1.6 GB extracted)
- **Leipzig Corpora**: 1M randomized web sentences
- **HuggingFace**: AI4Bharat Sangraha dataset
- **GitHub**: Hindi dictionaries and stop words

**Processing Pipeline**
1. **Download**: Fetches compressed files from multiple sources
2. **Extract**: Decompresses .tar.gz, .bz2, .zip files
3. **Process**: Cleans text, removes non-Hindi characters, counts frequencies
4. **Split**: Creates top 30,000 words in 10 manageable files

**Text Cleaning**
- ✅ Removes purna viram (।) and deergha viram (॥)
- ✅ Removes visarga (ः) character
- ✅ Only keeps Devanagari Unicode range (0x0900-0x097F)
- ✅ Splits on whitespace
- ✅ No length filtering (keeps short words like के, में, है)

## 📊 Current Statistics

- **Total unique words processed**: 3,664,322
- **Sources**: 5 major Hindi text corpora
- **Web app vocabulary**: Up to 30,000 frequency-ordered words
- **Top 20 words**: के, में, और, है, की, को, से, एक, का, किया, पर, ने, भी, लिए, कि, गया, था, यह, वह, हैं

## 🌐 Deployment

### GitHub Pages
1. Push to GitHub repository
2. Enable GitHub Pages in Settings → Pages
3. Set source to `main` branch, `/ (root)` folder
4. Access at `https://YOUR_USERNAME.github.io/r_think_hindi/`

### Other Static Hosting
Works with Netlify, Vercel, Cloudflare Pages, Surge.sh — simply upload the folder.

## 🛠️ Customization

### Adjust Default Values
Edit `index.html`:
```html
<!-- Words to Draw default -->
<input type="number" id="wordCount" value="50">

<!-- FROM MOST FREQ default -->
<input type="number" id="totalWords" value="3000">
```

### Modify Learning Prompt
Edit the `renderWords()` method in `<script>` section of `index.html`.

### Add New Data Sources
Edit `src/sources.py` and add to `HindiSources` class:
```python
class HindiSources:
    NEW_SOURCE = DataSource("https://example.com/hindi-corpus.tar.gz", "download")
```

## 🔧 Advanced Processing Options

```bash
# Resume from checkpoint
python main.py --resume

# Skip download step
python main.py --skip-download

# Skip extraction step
python main.py --skip-extract

# Custom output location
python main.py --output my_words.txt
```

## 💻 Browser Compatibility

Works in all modern browsers with JavaScript enabled:
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+

## 📦 Requirements

**Web Application**: None (pure HTML/CSS/JS)

**Corpus Processing**:
```bash
pip install requests beautifulsoup4 pyarrow datasets
```

## 🤝 Contributing

Contributions welcome! Areas for improvement:
- Additional data sources for corpus processing
- Parallel processing for faster performance
- Word filtering options (min frequency, word length)
- N-grams (bigrams, trigrams) support
- Part-of-speech tagging

## 📄 License

This project is open source under the MIT License. Please check licenses of original data sources before commercial use.

## 🙏 Credits

- **Word Data**: [FrequencyWords Project](https://github.com/hermitdave/FrequencyWords)
- **Corpora**: Wikimedia, Leipzig Corpora, AI4Bharat, various GitHub projects

---

Made with ❤️ for Hindi language learners

**Last Updated**: 2026-05-25  
**Version**: 5.0 (Combined web app + corpus processing)  
**Total Vocabulary**: Up to 30,000 frequency-ordered Hindi words
