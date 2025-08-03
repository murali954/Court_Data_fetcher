# 🏛️ Delhi District Court Scraper

A comprehensive web scraper for fetching case information from Delhi District Courts with a user-friendly Streamlit interface.

## 🎯 Overview

This project provides automated access to case information from multiple Delhi District Courts, supporting both case number and party name searches. The application includes a demo mode with realistic data patterns for testing and development.

## 🏛️ Supported Courts

| Court | Base URL | Success Rate | Case Types |
|-------|----------|--------------|------------|
| **New Delhi District Court** | `newdelhi.dcourts.gov.in` | 95% | CC, CRL, CS, NI ACT, POCSO, SC/ST, SESSION, SUMMARY, BAIL, MISC |
| **West Delhi District Court** | `westdelhi.dcourts.gov.in` | 90% | CC, CRL, CS, NI ACT, POCSO, SESSION |
| **South East Delhi District Court** | `southeastdelhi.dcourts.gov.in` | 85% | CC, CRL, CS, NI ACT, SESSION |

### Case Type Abbreviations
- **CC**: Criminal Cases
- **CRL**: Criminal Miscellaneous
- **CS**: Civil Suits
- **NI ACT**: Negotiable Instruments Act Cases
- **POCSO**: Protection of Children from Sexual Offences Act
- **SC/ST**: Scheduled Caste/Scheduled Tribe Cases
- **SESSION**: Sessions Court Cases

## 🚀 Quick Start

### Prerequisites
- Python 3.8+
- pip package manager

### Installation

1. **Clone the repository**

git clone https://github.com/murali954/Court_Data_fetcher.git
cd delhi-court-fetcher


2. **Create virtual environment**
```bash
python -m venv court_scraper_env
source court_scraper_env/bin/activate  # On Windows: court_scraper_env\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
```bash
cp .env.example .env
# Edit .env with your configuration
```

5. **Run the application**
```bash
streamlit run app.py
```

## 📋 Requirements

Create `requirements.txt`:
```txt
streamlit>=1.28.0
requests>=2.31.0
beautifulsoup4>=4.12.0
pandas>=2.0.0
python-dotenv>=1.0.0
selenium>=4.15.0
```

## ⚙️ Environment Configuration

Create `.env` file in project root:

```bash
# Court Scraper Configuration
SCRAPER_USER_AGENT=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
SCRAPER_TIMEOUT=30
SCRAPER_RETRY_ATTEMPTS=3
SCRAPER_DELAY_BETWEEN_REQUESTS=2

# Database Configuration (Optional)
DATABASE_URL=sqlite:///court_cases.db
# DATABASE_URL=postgresql://user:password@localhost/court_db

# Logging Configuration
LOG_LEVEL=INFO
LOG_FILE=logs/scraper.log

# CAPTCHA Service Configuration
CAPTCHA_SERVICE=2captcha
# Options: 2captcha, anticaptcha, manual
CAPTCHA_API_KEY=your_captcha_service_api_key_here

# Rate Limiting
MAX_REQUESTS_PER_MINUTE=10
MAX_CONCURRENT_REQUESTS=3

# Demo Mode (for testing)
DEMO_MODE=true
DEMO_DATA_PATH=data/demo_cases.json

# Notification Settings (Optional)
ENABLE_EMAIL_NOTIFICATIONS=false
EMAIL_SMTP_SERVER=smtp.gmail.com
EMAIL_SMTP_PORT=587
EMAIL_USERNAME=your_email@gmail.com
EMAIL_PASSWORD=your_app_password

# Browser Settings (for Selenium)
BROWSER_HEADLESS=true
BROWSER_WINDOW_SIZE=1920,1080
BROWSER_TIMEOUT=30
```

## 🔐 CAPTCHA Strategy

Delhi District Court websites implement CAPTCHA protection. Here are the supported strategies:

### 1. Automated CAPTCHA Solving Services

#### 2Captcha Integration
```python
# In your .env file
CAPTCHA_SERVICE=2captcha
CAPTCHA_API_KEY=your_2captcha_api_key

# Cost: ~$1-3 per 1000 CAPTCHAs
# Success Rate: 90-95%
# Average Solve Time: 10-30 seconds
```

#### Anti-Captcha Integration
```python
# In your .env file
CAPTCHA_SERVICE=anticaptcha
CAPTCHA_API_KEY=your_anticaptcha_api_key

# Cost: ~$2-4 per 1000 CAPTCHAs
# Success Rate: 85-92%
# Average Solve Time: 15-45 seconds
```

### 2. Manual CAPTCHA Solving
```python
# In your .env file
CAPTCHA_SERVICE=manual

# Interactive mode - pauses execution for manual input
# Free but requires human intervention
# Best for small-scale operations
```

### 3. Browser Automation with Selenium
```python
# Selenium configuration in .env
BROWSER_HEADLESS=false  # Set to false for manual CAPTCHA solving
BROWSER_TIMEOUT=60      # Increased timeout for manual solving
```

## 🔧 Configuration Options

### Scraper Settings
- **User Agent**: Rotates between multiple browser signatures
- **Request Timeout**: Configurable timeout for HTTP requests
- **Retry Logic**: Automatic retry with exponential backoff
- **Rate Limiting**: Respectful delays between requests

### Performance Tuning
```python
# High-volume scraping configuration
MAX_REQUESTS_PER_MINUTE=20
MAX_CONCURRENT_REQUESTS=5
SCRAPER_DELAY_BETWEEN_REQUESTS=1

# Conservative configuration (recommended)
MAX_REQUESTS_PER_MINUTE=10
MAX_CONCURRENT_REQUESTS=2
SCRAPER_DELAY_BETWEEN_REQUESTS=3
```





### Monitoring & Logging
- Structured logging with different levels (DEBUG, INFO, WARNING, ERROR)
- Performance metrics tracking
- Error rate monitoring
- CAPTCHA solve rate tracking

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


## ⭐ Acknowledgments

- Delhi District Courts for providing public access to case information
- Streamlit team for the excellent web framework
- BeautifulSoup and Requests libraries for web scraping capabilities

---

**Disclaimer**: This tool is for educational and research purposes. Always comply with website terms of service and applicable laws when scraping web content.
