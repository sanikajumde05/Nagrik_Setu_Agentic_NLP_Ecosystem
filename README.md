# Nagrik Setu
## An Agentic NLP Ecosystem for Multilingual Citizen Grievance Redressal and Resolution Tracking

## 1. Project Overview

Nagrik Setu is a multilingual and multimodal citizen grievance management system designed to simplify complaint registration, classification, department routing, and resolution tracking. It uses Natural Language Processing (NLP) techniques to process complaints submitted in English, Hindi, and Marathi.

The system provides text, voice, and image-based complaint input. It processes supported inputs, extracts relevant information, assigns complaint categories, estimates priority, and routes cases to configured departments. It also supports duplicate complaint suggestions, Service-Level Agreement (SLA) monitoring, notifications, and an administrative dashboard.

## 2. Key Features

- **Multilingual Complaint Processing:** Supports English, Hindi, and Marathi complaint text.
- **Voice-Based Input:** Uses speech recognition to convert audio complaints into text.
- **Image Classification:** Analyses uploaded images using a vision-language model.
- **Automated Classification:** Uses keyword-based rules and zero-shot classification to identify complaint categories.
- **Named Entity Recognition:** Extracts relevant information from complaint text.
- **Sentiment Analysis:** Estimates the sentiment expressed in a complaint.
- **Priority Estimation:** Applies configured rules to estimate complaint urgency.
- **Department Routing:** Maps predicted categories to configured departments.
- **Duplicate Detection:** Identifies potentially similar complaints using text similarity and geographic proximity.
- **SLA Monitoring:** Tracks configured deadlines and supports reminders and escalations.
- **Analytics Dashboard:** Provides staff with complaint and workflow information.

## 3. Technologies and Tools Used

| Technology / Tool | Purpose |
|---|---|
| Python 3.11 | Main programming language |
| FastAPI | Backend API development |
| Uvicorn | Backend application server |
| SQLAlchemy | Database interaction and ORM |
| SQLite | Persistent case storage |
| Streamlit | Administrative dashboard |
| HTML, CSS and JavaScript | Citizen portal interface |
| Transformers | Loading and running NLP models |
| mDeBERTa | Zero-shot complaint classification |
| IndicTrans2 | Hindi and Marathi translation when required |
| XLM-R | Multilingual language identification and sentiment processing |
| MuRIL / HiNER | Hindi and Marathi named entity recognition |
| BERT-based NER | English named entity recognition |
| Whisper | Speech-to-text transcription |
| FFmpeg | Audio processing support |
| CLIP | Image classification |
| Scikit-learn | TF-IDF and text similarity calculations |
| OpenStreetMap Nominatim | Geographic reverse geocoding |
| Haversine Formula | Geographic distance calculation |

*Note: Model availability and execution depend on the installed dependencies, model configuration, and hardware.*

## 4. System Requirements

### Software Requirements
- Python 3.11
- pip package manager
- Git (optional, for repository management)
- Modern web browser
- FFmpeg for audio processing
- Required Python packages and configured model dependencies

### Hardware Requirements
- A laptop or desktop computer
- Recommended 8 GB RAM or more, depending on the models loaded
- Sufficient disk space for Python packages and downloaded model weights
- GPU support is optional but may improve transformer and image-model inference speed

## 5. Project Structure

The main project components are organized as follows:

```text
Nagrik-Setu/
│
├── app/
│   ├── main.py
│   ├── database.py
│   ├── geo.py
│   ├── chatbot.py
│   ├── llm_chat.py
│   │
│   └── pipeline/
│       ├── orchestrator.py
│       ├── script_lang.py
│       ├── language_detect.py
│       ├── translate.py
│       ├── classify.py
│       ├── ner.py
│       ├── sentiment.py
│       ├── priority.py
│       ├── routing.py
│       ├── speech_to_text.py
│       └── image_classify.py
│
├── dashboard/
│   └── Streamlit dashboard files
│
├── frontend/
│   └── citizen-portal.html
│
├── requirements.txt
└── README.md
```

*The structure above is representative. Confirm the exact filenames and folders in the submitted project directory before using it as a repository tree.*

## 6. Installation and Setup

### Step 1: Obtain the Project

Download or clone the Nagrik Setu project repository and open its root directory.

```bash
git clone <repository-url>
cd Nagrik-Setu
```

If the project is provided as a ZIP file, extract it and open the extracted folder instead.

### Step 2: Create a Virtual Environment

Create an isolated Python environment to manage project dependencies.

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**Linux / macOS:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

Upgrade pip and install the packages listed in the project's dependency file.

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If FFmpeg is required for voice processing, install it separately and ensure that it is accessible through the system PATH.

### Step 4: Configure the Environment

Set any required environment variables or API credentials according to the project's configuration.

If the optional Anthropic-powered chatbot is enabled, configure its API key securely. Do not upload API keys or other secrets to a public repository.

### Step 5: Initialize the Database

The application uses SQLAlchemy with SQLite for persistent case storage. Run the application's configured database initialization process before submitting complaints.

Verify the database setup instructions against the actual initialization code in `app/database.py`.

## 7. Running the Project

### Step 1: Start the FastAPI Backend

From the project root directory, activate the virtual environment and run:

```bash
uvicorn app.main:app --reload
```

The backend will generally be available at:

```text
http://127.0.0.1:8000
```

FastAPI's interactive API documentation can be accessed at:

```text
http://127.0.0.1:8000/docs
```

### Step 2: Open the Citizen Portal

Open the citizen portal file in a modern web browser:

```text
frontend/citizen-portal.html
```

The portal provides the interface for submitting complaints and interacting with the grievance management system. Ensure that its configured backend URL points to the running FastAPI server.

### Step 3: Start the Administrative Dashboard

Open a separate terminal, activate the same virtual environment, and run the dashboard using Streamlit:

```bash
streamlit run dashboard/<dashboard-file>.py
```

Replace `<dashboard-file>.py` with the actual Streamlit entry-point filename in the project.

The dashboard provides staff-facing access to complaint records, case status, workflow information, and analytics.

## 8. How to Use the Application

### Citizen Portal

1. Open the citizen portal in a browser.
2. Enter the complaint details in the available input field.
3. Select or provide the supported complaint input type: text, voice, or image.
4. Submit the complaint.
5. For voice input, the audio is transcribed into text using Whisper.
6. For text complaints, the NLP pipeline identifies the language and processes the complaint.
7. The system generates relevant outputs such as category, extracted entities, sentiment, priority, and department assignment, depending on the input and configured processing path.
8. The complaint is registered for subsequent tracking.

### NLP Processing

The text-processing workflow follows these main stages:

1. Language detection.
2. Translation when required.
3. Keyword-based category matching.
4. Zero-shot classification when no keyword override applies.
5. Named entity recognition.
6. Sentiment analysis.
7. Priority estimation.
8. Department routing.

The pipeline follows a configured sequence of processing steps. Its outputs are model predictions and rule-based recommendations that may require staff review.

### Administrative Dashboard

1. Open the Streamlit dashboard.
2. View registered complaints and their available details.
3. Review predicted categories, priority levels, and department assignments.
4. Monitor complaint status and SLA deadlines.
5. Review possible duplicate complaints suggested by the system.
6. Use available dashboard analytics to examine complaint trends and workflow performance.

## 9. Duplicate Detection and SLA Monitoring

The duplicate-detection component uses TF-IDF cosine similarity to identify complaints with similar text. When geographic coordinates are available, Haversine distance is used to estimate proximity between complaint locations. The system suggests potentially related cases for review; it does not automatically merge or reject complaints.

SLA monitoring checks complaint deadlines based on configured priority rules. It supports reminders, overdue escalations, notifications, and audit logging. These functions assist staff in monitoring cases but do not independently guarantee complaint resolution.

## 10. Dataset and Evaluation

The project uses a synthetic grievance dataset for development and evaluation. The available dataset files include:

- `grievances_synthetic.csv`
- `grievances_holdout_templates.csv`

The dataset contains complaint text and category labels across 14 grievance categories. A separate pilot benchmark described in the project report contains 105 annotated examples across English, Hindi, and Marathi.

The reported pilot results include:

| Classification Approach | Accuracy |
|---|---:|
| Hybrid Pipeline | 86.67% |
| Zero-Shot Only | 60.00% |
| Independent Keyword Baseline | 93.33% |

These figures represent the reported pilot benchmark and should not be interpreted as production performance or proof of real-world effectiveness. The independent keyword baseline performed better than the hybrid pipeline on this particular benchmark.

## 11. Important Notes and Limitations

- The evaluation dataset is synthetic and may not represent the full diversity of real citizen complaints.
- Classification performance depends on language, spelling, complaint context, and category definitions.
- Voice transcription may be affected by background noise, accents, and recording quality.
- Image classification follows a separate processing path and does not independently verify an incident's location or severity.
- Duplicate detection provides suggestions rather than confirmed duplicate decisions.
- Priority estimation uses configured rules and should be reviewed by authorized staff.
- Department routing depends on the correctness of the category prediction and department mapping.
- Real-world deployment requires appropriate privacy controls, authentication, authorization, security testing, and operational validation.

## 12. Future Enhancements

Potential future improvements include:

- Expanding support to additional Indian languages.
- Improving classification with larger, human-validated datasets.
- Adding human review for uncertain predictions.
- Improving voice and image processing accuracy.
- Strengthening duplicate detection and priority estimation.
- Integrating with authorized government grievance-management platforms.
- Conducting controlled pilot deployments and scalability testing.

## 13. Conclusion

Nagrik Setu demonstrates how multilingual NLP, multimodal input processing, and workflow automation can support citizen grievance management. By combining complaint classification, information extraction, department routing, duplicate suggestions, SLA monitoring, and dashboard analytics, the project provides an integrated prototype for managing grievance records and supporting administrative follow-up.

The system is intended as a decision-support and case-management prototype. Its predictions and automated workflow actions should be reviewed appropriately, and further validation is required before large-scale operational deployment.
