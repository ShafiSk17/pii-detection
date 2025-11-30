🔒 Enterprise PII Detection Demo
✨ What is this app?
This is a super easy web app that finds sensitive personal information (PII) in your files and makes them safe by hiding it. Think of it like a digital redaction tool for companies.

Examples of PII it finds:

Emails (john@example.com)

Phone numbers (555-123-4567)

Social Security Numbers (123-45-6789)

Credit card numbers

Your custom IDs (like school_id: 223j1ao5g)

🎯 What can it do?
File Type	✅ Works Perfectly
📄 CSV	Upload → Detect → Download safe CSV
📄 PDF	Extracts text → Finds PII → Shows results
📄 Text	Any .txt file → Highlights PII
📄 JSON	Reads data → Detects sensitive fields
🚀 How to use it (3 clicks)
text
1. Open app → See upload area
2. Pick file type (CSV/PDF/Text/JSON)
3. Upload file → See PII results instantly!
4. Download "Safe Version" with hidden PII
Bonus: Add your own custom rules in sidebar!

text
Example: School ID "223j1ao5g" → Gets tagged as <SCHOOL_ID>
🛠️ How it works (Simple explanation)
text
Your File → LangChain Loaders → Presidio AI → PII Tags → Safe Download
       📄           📥             🤖       🔍         ⬇️
Step by step:

Upload any file (CSV, PDF, etc.)

LangChain reads the file content

Presidio AI scans for 20+ PII types + your custom rules

Results table shows what was found (with confidence scores)

One-click download of safe version

💻 Tech used (Beginner friendly)
What it does	Tool used
Web interface	Streamlit (like PowerPoint for code)
File reading	LangChain (reads PDF/CSV like magic)
PII Detection	Presidio (Microsoft AI for sensitive data)
NLP Brain	spaCy (understands human language)
Data tables	Pandas (Excel for Python)
📱 Live Demo Features
text
✅ Beautiful dashboard with metrics
✅ Sidebar for custom whitelist/regex rules
✅ Real-time PII highlighting 
✅ Download safe files (CSV/Text)
✅ Works with your test files perfectly
✅ Mobile-friendly design
🚀 Quick Start (Local)
bash
# 1. Clone or download files
git clone your-repo

# 2. Install everything
pip install -r requirements.txt

# 3. Download spaCy model (one time)
python -m spacy download en_core_web_lg

# 4. Run app
streamlit run main.py
App opens at: http://localhost:8501

☁️ Deploy to Internet (Free!)
Option 1: Streamlit Cloud (2 minutes)
text
1. Push code to GitHub
2. Go to share.streamlit.io
3. Connect GitHub repo
4. Deploy → Live URL ready!
Option 2: Hugging Face Spaces
text
1. Fork this repo
2. Create new Space
3. Deploy → Free hosting!
📁 Files you need
text
📄 main.py              # Main app code
📦 requirements.txt     # Install commands
📋 README.md           # This file!
🧪 test_employees.csv  # Test CSV (20+ PII)
📄 confidential_pii_employee_records.pdf  # Test PDF (50+ PII)
🧪 Test with these files
CSV: test_employees.csv → Detects emails + school_ids

PDF: confidential_pii_employee_records.pdf → 50+ PII instances

Add rule: SCHOOL_ID → "223j1ao5g" → See custom detection!

🎉 Example Results
Upload CSV → See this:

text
Total PII Found: 16
┌────────────┬────────────┬──────────────┬────────────┐
│ PII Type   │ Text       │ Confidence   │ Location   │
├────────────┼────────────┼──────────────┼────────────┤
│ EMAIL      │ john@...   │ 0.98         │ 5-18       │
│ PHONE      │ 555-123... │ 0.95         │ 25-36      │
│ SCHOOL_ID  │ 223j1ao5g  │ 0.90         │ 45-54      │
└────────────┴────────────┴──────────────┴────────────┘
Download safe CSV:

text
name,email,school_id
John,<EMAIL_ADDRESS>,<SCHOOL_ID>
🔒 Safe & Production Ready
✅ No data stored on server

✅ Instant processing

✅ Downloadable safe files

✅ Custom enterprise rules

✅ Ready for Airflow integration

🤝 Built With
text
♥️ Streamlit (UI)
🤖 Presidio (PII Detection) 
📚 LangChain (File Loaders)
🧠 spaCy (NLP Engine)
📊 Pandas (Data Processing)
📞 Need Help?
Demo Flow:

Add custom rule: SCHOOL_ID = 223j1ao5g

Upload test CSV

See detections table

Download safe version 🎯

Real-world use: Companies use this to protect customer data before sharing files.

🎯 Supported File Types & Capabilities
File Type	How it Works	Technical Implementation
📄 CSV	Reads rows → finds PII in each cell → creates safe CSV	pandas.read_csv() + cell-by-cell Presidio scanning
📄 PDF	Extracts all pages → scans text → shows results	PyPDFLoader.load() from LangChain → joins page_content
📄 Text	Reads entire file → highlights PII locations	Direct file read + analyzer.analyze()
📄 JSON	Parses as DataFrame → scans all fields	pd.read_json() + structured PII detection
🛠️ Technical Architecture (How each part works)
text
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   File Upload   │───▶│  LangChain       │───▶│  Presidio AI    │
│ CSV/PDF/TXT/JSON│    │ Loaders          │    │ Analyzer Engine │
└─────────────────┘    │                  │    │                 │
                       │ • PyPDFLoader    │    │ • spaCy NLP     │
                       │ • CSVLoader      │    │ • 20+ PII Types │
                       │ • lazy_load()    │    │ • Custom Rules  │
└──────────────────┘    └─────────────────┘
         │                        │
         ▼                        ▼
┌─────────────────┐    ┌─────────────────┐
│  Results Table  │◀───│ AnonymizerEngine│
│ Confidence %    │    │ • <PII> Tags    │
└─────────────────┘    └─────────────────┘
         │
         ▼
┌─────────────────┐
│ Safe Download   │
└─────────────────┘
🔍 Core Technical Components
1. File Loading Pipeline
python
# PDF Processing
loader = PyPDFLoader(tmp_path)  # LangChain PDF Loader
docs = loader.load()            # Loads all pages as Document objects
content = " ".join([doc.page_content for doc in docs])  # Merge pages

# CSV Processing  
content = pd.read_csv(tmp_path)  # Pandas DataFrame
for col in df.columns:           # Scan each cell individually
    for value in df[col]:
        findings = analyzer.analyze(str(value))
2. PII Detection Engine
python
# Presidio Analyzer with spaCy NLP
nlp_engine = NlpEngineProvider(
    nlp_configuration={
        "nlp_engine_name": "spacy",
        "models": [{"lang_code": "en", "model_name": "en_core_web_lg"}]
    }
)
analyzer = AnalyzerEngine(nlp_engine=nlp_engine)

# Detects automatically:
# PERSON, PHONE_NUMBER, EMAIL_ADDRESS, CREDIT_CARD, US_SSN, URL, IP_ADDRESS
3. Custom Rule System (Your Innovation!)
python
# Dynamic Whitelist (Sidebar)
detector.add_custom_whitelist("SCHOOL_ID", ["223j1ao5g", "school123"])

# Dynamic Regex  
detector.add_custom_regex("CUSTOM_ID", r"^[A-Za-z0-9]{8,12}$")
4. Smart Anonymization
python
# Creates proper RecognizerResult objects (not dicts!)
recognizer_result = RecognizerResult(
    entity_type="EMAIL_ADDRESS",
    start=0, end=15,
    score=0.98
)
anonymized = anonymizer.anonymize(text, [recognizer_result])
# Result: "john@example.com" → "<EMAIL_ADDRESS>"
💻 Tech Stack Breakdown
Purpose	Library	Specific Feature Used
Web UI	Streamlit	st.file_uploader(), st.columns(), custom CSS
File Parsing	LangChain	PyPDFLoader.load(), CSVLoader, Document objects
PII Detection	Presidio	AnalyzerEngine, RecognizerResult, spaCy integration
NLP Engine	spaCy	en_core_web_lg model (large English)
Data Processing	Pandas	DataFrame scanning, CSV export
File Handling	tempfile	Secure temporary file processing
🚀 Key Features (Technical)
text
✅ Multi-format support: CSV (pandas), PDF (PyPDFLoader), Text, JSON
✅ Real-time custom rules: Dynamic registry.add_recognizer()
✅ Cell-level CSV scanning: enumerate(df[col].dropna())
✅ Proper anonymization: RecognizerResult objects (not dicts)
✅ Page merging: " ".join([doc.page_content for doc in docs])
✅ Confidence scoring: f"{finding.score:.2f}"
✅ Position-aware highlighting: text[f.start:f.end]
🧪 Test Data Results
CSV Input:

text
name,email,school_id
John,john.doe@company.com,223j1ao5g
Detected PII:

text
EMAIL_ADDRESS: "john.doe@company.com" (0.98 confidence)
SCHOOL_ID: "223j1ao5g" (0.90 confidence - custom rule)
Safe CSV Output:

text
name,email,school_id
John,<EMAIL_ADDRESS>,<SCHOOL_ID>
📦 Deployment Ready
requirements.txt
text
streamlit==1.38.0
presidio-analyzer==2.2.351
presidio-anonymizer==2.2.351
spacy==3.7.5
langchain-community==0.2.10
pypdf==4.2.0
pandas==2.2.2
One-time spaCy setup:
bash
python -m spacy download en_core_web_lg
🌐 Deploy Anywhere
text
1. Streamlit Cloud: GitHub → share.streamlit.io → Deploy
2. Local: pip install -r requirements.txt → streamlit run main.py
3. Docker: Dockerfile with spaCy pre-download
🎬 Demo Flow for Presentations
text
1. Upload test_employees.csv → Show PII table (16 findings)
2. Sidebar → Add SCHOOL_ID rule → Re-upload → Show custom detection
3. Download safe CSV → Open in Excel → Show <PII> redactions
4. Upload PDF → Demo 50+ PII detections across pages
