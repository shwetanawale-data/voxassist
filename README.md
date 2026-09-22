# 🎙️ VoxAssist — Voice-Controlled AI Assistant

> A JARVIS-style voice assistant built with Python, Machine Learning, Generative AI, and real-time web search.

VoxAssist is a voice-controlled AI assistant that listens to spoken commands, converts speech into text, identifies the user's intent, performs predefined actions, or answers open-ended questions using a Generative AI model grounded with live web search.

The project combines a lightweight **Machine Learning intent classifier** with **LLM-based question answering and Retrieval-Augmented Generation (RAG)** to create a more flexible voice assistant.

---

## 🚀 Features

* 🎤 Speech-to-text using SpeechRecognition
* 🧠 Machine Learning-based intent classification
* 🔢 Text vectorization using CountVectorizer
* 🤖 Multinomial Naive Bayes classifier
* 🌐 Open websites such as Google and YouTube using voice commands
* 🎵 Music command handling
* 😂 Random joke generation
* 📅 Real-time date and time using Python's system clock
* 🔎 Live web search using Tavily
* 🧠 AI-generated answers using Groq and LLaMA
* 🔊 Text-to-speech using Windows SAPI
* 🔄 Hybrid architecture combining local ML and cloud-based AI

---

## 💡 Problem Statement

Many beginner voice assistants can only respond to a fixed set of commands. If the user asks something outside those predefined commands, the assistant cannot respond intelligently.

VoxAssist was developed to address this limitation by combining:

1. **Machine Learning** for recognizing common command categories
2. **Rule-based routing** for reliable predefined actions
3. **Generative AI** for open-ended questions
4. **Live web search** to provide more current information
5. **Text-to-speech** to make the interaction conversational

---

## 🏗️ How VoxAssist Works

The assistant follows this general pipeline:

```text
User Voice
    ↓
Microphone
    ↓
Speech Recognition
    ↓
Convert Speech → Text
    ↓
Command Analysis
    ↓
 ┌───────────────────────────────┐
 │ Known command?                │
 └───────────────┬───────────────┘
                 │
        ┌────────┴────────┐
        ↓                 ↓
   Direct Action      Open-ended
        │              Question
        │                 │
        ↓                 ↓
 Google / YouTube     Tavily Search
 Music / Joke             ↓
 Date / Time          Search Results
 Greeting                 ↓
        │             Groq LLaMA
        │                 ↓
        └────────┬────────┘
                 ↓
          Final Response
                 ↓
          Text-to-Speech
                 ↓
             User
```

---

## 🧠 Machine Learning Component

The project uses a small intent-classification model.

### Text Vectorization

`CountVectorizer` converts command text into numerical features that can be processed by a machine learning model.

### Classification Model

A **Multinomial Naive Bayes** classifier is trained on example commands belonging to different intents.

The current intents include:

* `open_app`
* `play_music`
* `search_web`
* `greeting`
* `joke`

Example:

```text
"open youtube" → open_app

"play a song" → play_music

"search weather" → search_web

"hello" → greeting

"tell me a joke" → joke
```

---

## 🤖 Generative AI + RAG

For questions that do not match the predefined actions, VoxAssist uses a Generative AI workflow.

The process is:

```text
User Question
     ↓
Tavily Web Search
     ↓
Relevant Search Results
     ↓
Groq LLaMA
     ↓
AI-Generated Answer
```

This approach is a form of **Retrieval-Augmented Generation (RAG)**.

Instead of relying only on the language model's internal knowledge, the assistant first retrieves information from the web and provides that information to the AI when generating the response.

---

## 🔊 Voice Output

VoxAssist uses the Windows **SAPI.SpVoice** engine through `pywin32` for text-to-speech.

This allows the assistant to respond verbally instead of displaying only text.

---

## 🛠️ Technologies Used

| Technology        | Purpose                   |
| ----------------- | ------------------------- |
| Python            | Core programming language |
| SpeechRecognition | Speech-to-text            |
| PyAudio           | Microphone input          |
| Scikit-learn      | Machine Learning          |
| CountVectorizer   | Text feature extraction   |
| MultinomialNB     | Intent classification     |
| Groq              | Generative AI             |
| LLaMA 3.3         | Language model            |
| Tavily            | Live web search           |
| pywin32           | Windows text-to-speech    |
| Webbrowser        | Opening websites          |

---

## 📁 Project Structure

```text
VoxAssist-Voice-Assistant/
│
├── VoxAssist_Voice_Assistant.ipynb
├── README.md
├── requirements.txt
├── .gitignore
│
└── screenshots/
    └── demo.png
```

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/VoxAssist-Voice-Assistant.git
```

```bash
cd VoxAssist-Voice-Assistant
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure API keys

VoxAssist requires:

* Groq API key
* Tavily API key

Create your API keys from their respective platforms and store them as environment variables.

For example:

```python
import os

GROQ_API_KEY = os.getenv("GROQ_API_KEY")
TAVILY_API_KEY = os.getenv("TAVILY_API_KEY")
```

**Never upload your actual API keys to GitHub.**

---

## ▶️ Running the Project

Open the notebook:

```bash
jupyter notebook VoxAssist_Voice_Assistant.ipynb
```

Run the cells in order.

When the assistant starts listening, speak a command into your microphone.

### Example commands

```text
"Open YouTube"

"Open Google"

"Play music"

"Tell me a joke"

"What is today's date?"

"What is the current time?"

"Who is the current Chief Minister of Maharashtra?"

"What is artificial intelligence?"
```

Known commands are handled directly, while open-ended questions are passed through the web-search + AI pipeline.

---

## 🔍 Key Learnings

### 1. Small ML models need sufficient training data

The initial Naive Bayes classifier was useful for demonstrating intent classification, but the small training dataset could lead to incorrect classifications.

The project therefore uses direct keyword checks for known actions and sends other questions to the AI system.

### 2. AI models can provide outdated information

Language models should not be treated as a live source of information.

For this reason, VoxAssist uses:

* Python's system clock for date/time
* Tavily for live web information

### 3. Hybrid AI architecture

The project demonstrates how different approaches can work together:

```text
Local ML
   +
Rule-Based Logic
   +
Generative AI
   +
Web Search / RAG
   =
Voice Assistant
```

### 4. Voice interaction requires multiple components

A complete voice assistant involves more than an LLM. It requires:

```text
Audio Input
→ Speech Recognition
→ Intent Understanding
→ Action / AI
→ Response Generation
→ Text-to-Speech
```

---

## 🔮 Future Improvements

* Add multilingual support such as Hindi + English
* Train the intent classifier using a larger real-world dataset
* Add wake-word detection such as "Hey VoxAssist"
* Add conversational memory
* Develop a graphical user interface
* Convert the notebook into a standalone desktop application
* Improve intent classification accuracy
* Add more voice-controlled actions

---

## 🎯 Project Highlights

**Machine Learning:**
Intent classification using CountVectorizer + Multinomial Naive Bayes

**Generative AI:**
Open-ended question answering using Groq and LLaMA

**RAG:**
Live web search through Tavily before generating answers

**Speech AI:**
Speech-to-text and text-to-speech interaction

**Automation:**
Voice-controlled website and music actions

---

## 👩‍💻 Author

**Shweta Nawale**

B.Sc. Graduate | PG Program in Data Science & Analytics with Generative AI

---

⭐ If you find this project interesting, feel free to explore the notebook and the implementation.
