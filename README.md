# 🧠 Senti-Mental Health Analysis App

A comprehensive web application that combines **sentiment analysis** and **mental health concern detection** using Natural Language Processing (NLP) and machine learning. Built with Streamlit, this application analyzes text data to provide insights into emotional tone and potential mental health concerns.

---

## 📋 Table of Contents

- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Requirements](#requirements)
- [Usage](#usage)
- [How It Works](#how-it-works)
- [Application Pages](#application-pages)
- [Technologies & Libraries](#technologies--libraries)
- [Dataset](#dataset)
- [Model Training](#model-training)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

## ✨ Features

### 🎯 Core Functionalities

1. **Mental Health Concern Prediction**
   - Predicts whether input text may indicate potential mental health concerns
   - Uses a trained Logistic Regression model
   - Based on Twitter mental health dataset

2. **Sentiment Analysis**
   - Classifies text as Positive, Negative, or Neutral
   - Powered by VADER (Valence Aware Dictionary and sEntiment Reasoner)
   - Provides compound sentiment score for detailed analysis

3. **Data Visualizations**
   - Top 20 most common words in the training dataset
   - Tweet length distribution analysis
   - Interactive word cloud visualization
   - Sentiment distribution pie and bar charts

### 🎨 User Interface

- Clean, modern interface with custom CSS styling
- Interactive sidebar navigation
- Real-time text analysis with results displayed in styled cards
- Responsive design for desktop and mobile devices
- Visual icons and emojis for better UX

---

## 📁 Project Structure

```
sentimentanalysis/
├── app.py                          # Main Streamlit application
├── train_model.py                  # Model training script (required to generate pkl files)
├── mental_health_model.pkl         # Pre-trained Logistic Regression model
├── tfidf_vectorizer.pkl            # Pre-trained TF-IDF vectorizer
├── Mental-Health-Twitter.csv       # Training dataset
├── sentiment-analysis.jpg          # Home page background image
└── README.md                       # Project documentation
```

---

## 🚀 Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)

### Step 1: Clone the Repository

```bash
git clone https://github.com/SaiSampathKumar5/sentimentanalysis.git
cd sentimentanalysis
```

### Step 2: Create Virtual Environment (Optional but Recommended)

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Required Packages

```bash
pip install -r requirements.txt
```

Or manually install:

```bash
pip install streamlit pandas nltk scikit-learn wordcloud matplotlib plotly pillow joblib
```

### Step 4: Download NLTK Data

The application automatically downloads required NLTK data on first run, but you can manually download it:

```bash
python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt'); nltk.download('wordnet'); nltk.download('vader_lexicon')"
```

---

## 📦 Requirements

Create a `requirements.txt` file:

```
streamlit>=1.28.0
pandas>=1.5.0
nltk>=3.8.0
scikit-learn>=1.3.0
wordcloud>=1.9.0
matplotlib>=3.7.0
plotly>=5.17.0
Pillow>=10.0.0
joblib>=1.3.0
```

---

## 💻 Usage

### Running the Application

```bash
streamlit run app.py
```

The application will open in your default browser at `http://localhost:8501`

### Using the App

#### **Home Page**
- Overview of the application
- Explanation of features
- Beautiful hero image

#### **Analysis Page**
1. Enter or paste any text in the text area
2. Click "Analyze" button
3. View results:
   - **Left Card**: Mental Health Concern Prediction (⚠️ or ✅)
   - **Right Card**: Sentiment Analysis (😊 😐 😞) with compound score

#### **Visualizations Page**
- Explore the dataset statistics
- View patterns in mental health-related tweets
- Analyze word frequencies and sentiment distribution

---

## 🔍 How It Works

### Text Preprocessing Pipeline

1. **Lowercasing**: Converts all text to lowercase for uniformity
2. **URL & Mention Removal**: Removes URLs and @mentions
3. **Special Character Removal**: Strips non-alphabetic characters
4. **Tokenization**: Splits text into individual words
5. **Stopword Removal**: Eliminates common English words (the, is, etc.)
6. **Stemming**: Reduces words to their root form (e.g., "running" → "run")
7. **Lemmatization**: Converts words to their base dictionary form

### Mental Health Prediction

- **Algorithm**: Logistic Regression
- **Vectorization**: TF-IDF (Term Frequency-Inverse Document Frequency)
- **Output**: Binary classification (0 = Concern, 1 = No Concern)

### Sentiment Analysis

- **Tool**: VADER (Valence Aware Dictionary and sEntiment Reasoner)
- **Scores**:
  - Compound ≥ 0.05 → **Positive** (😊)
  - Compound ≤ -0.05 → **Negative** (😞)
  - Compound between -0.05 and 0.05 → **Neutral** (😐)

---

## 📊 Application Pages

### Page 1: Home
- Welcome message
- Application overview
- Feature descriptions
- Navigation guidance

### Page 2: Analysis
- **Input**: Text area for user input
- **Processing**: Real-time text analysis
- **Output**: 
  - Mental health prediction with confidence indicator
  - Sentiment classification with compound score
  - Visual progress bar

### Page 3: Visualizations
- **Top 20 Words**: Bar chart of most frequent words
- **Tweet Length**: Histogram showing distribution
- **Word Cloud**: Visual representation of common terms
- **Sentiment Distribution**: Analysis of sentiment breakdown

---

## 🛠️ Technologies & Libraries

| Library | Purpose |
|---------|---------|
| **Streamlit** | Web framework for building interactive apps |
| **NLTK** | Natural Language Toolkit for NLP tasks |
| **scikit-learn** | Machine learning algorithms and vectorization |
| **Pandas** | Data manipulation and analysis |
| **Plotly** | Interactive data visualizations |
| **WordCloud** | Visual word frequency representation |
| **Matplotlib** | Plotting library |
| **Joblib** | Model serialization and loading |
| **Pillow** | Image processing |

---

## 📈 Dataset

- **Name**: Mental-Health-Twitter.csv
- **Contents**: Twitter posts labeled with mental health concerns
- **Columns**:
  - `post_text`: The text content of the tweet
  - `label`: Binary label (0 = Concern, 1 = No Concern)
- **Size**: Thousands of tweets with manual annotations

### Data Cleaning
- Removes rows with missing `post_text` or `label` values
- Keeps only relevant columns for analysis

---

## 🎓 Model Training

To retrain the model or create new model files:

1. Ensure `Mental-Health-Twitter.csv` is in the project directory
2. Run the training script:

```bash
python train_model.py
```

This generates:
- `mental_health_model.pkl` - Trained Logistic Regression model
- `tfidf_vectorizer.pkl` - TF-IDF vectorizer

**Note**: The `train_model.py` file should contain the training pipeline and must be created separately if it doesn't exist.

---

## 🎨 Customization

### Changing Colors
Edit the CSS section in `app.py` (lines 83-157):
- `.positive-text { color: #28a745; }` - Green for positive
- `.negative-text { color: #dc3545; }` - Red for negative
- `.neutral-text { color: #6c757d; }` - Gray for neutral

### Updating the Home Image
Replace `sentiment-analysis.jpg` with your own image in the project directory.

### Modifying Sentiment Thresholds
In the `Analysis` page section, adjust these lines:
```python
if compound_score >= 0.05:  # Change threshold
    sentiment = "Positive"
elif compound_score <= -0.05:  # Change threshold
    sentiment = "Negative"
```

### Adding More Visualizations
Add new sections in the `Visualizations` page to create custom charts using Plotly or Matplotlib.

---

## ⚠️ Troubleshooting

### Issue: "Model files not found" Error
**Solution**: Run the training script first
```bash
python train_model.py
```

### Issue: NLTK Data Not Downloading
**Solution**: Manual download
```bash
python -c "import nltk; nltk.download('all')"
```

### Issue: "Mental-Health-Twitter.csv not found"
**Solution**: Ensure the CSV file is in the same directory as `app.py`

### Issue: Home Page Image Not Loading
**Solution**: 
1. Ensure `sentiment-analysis.jpg` exists in the project directory
2. Check file name matches exactly (case-sensitive on Linux/Mac)

### Issue: Streamlit Won't Start
**Solution**: Clear Streamlit cache
```bash
streamlit cache clear
```

---

## 📝 Example Usage

### Input
```
I've been feeling really overwhelmed and anxious lately. 
I can't seem to concentrate on anything.
```

### Expected Output
- **Mental Health Prediction**: ⚠️ Potential mental health concern detected
- **Sentiment**: 😞 Negative (Compound Score: -0.65)

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 👨‍💼 Author

**Sai Sampath Kumar**

- GitHub: [@SaiSampathKumar5](https://github.com/SaiSampathKumar5)
- Project: [sentimentanalysis](https://github.com/SaiSampathKumar5/sentimentanalysis)

---

## 📞 Support & Feedback

For issues, questions, or suggestions, please:
- Open an [Issue](https://github.com/SaiSampathKumar5/sentimentanalysis/issues)
- Contact the author directly

---

## 🔗 Quick Links

- [Streamlit Documentation](https://docs.streamlit.io/)
- [NLTK Documentation](https://www.nltk.org/)
- [scikit-learn Documentation](https://scikit-learn.org/)
- [VADER Sentiment Analysis](https://github.com/cjhutto/vaderSentiment)

---

**Last Updated**: June 2026
**Version**: 1.0.0
